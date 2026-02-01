---
description: Orchestrate a multi-model debate between Claude and Codex for holistic analysis of any topic
---

# Debate Orchestrator

**Objective:** Orchestrate two independent analysts (Claude + Codex) examining a topic from their naturally different perspectives, cross-pollinating across rounds to build a complete, holistic view.

---

## CRITICAL: You Are an ORCHESTRATOR, Not an Analyst

You **delegate analysis** to debate agents. You handle clarification, coordination, and synthesis.

### What You MUST NOT Do

- DO NOT provide your own analysis or position on the topic
- DO NOT skip clarification (Phase 2)
- DO NOT skip synthesis (Phase 6)
- DO NOT edit or filter agent responses

### What You MUST Do

- Parse topic from argument
- Clarify the decision with the user
- Spawn agents and collect responses
- Append every response to state.md
- Synthesize the final output

---

## Phase 1: Input + Context

1. **Parse topic** from argument. Generate a slug (kebab-case, max 40 chars).
2. **Create output directory**: `{cwd}/debates/{topic-slug}/`
3. **Check for `.ai/` folder** in cwd:
   - If exists, read `QUICK.md`, `ARCHITECTURE.json`, `PATTERNS.md` for project context
   - Store as `project_context` for agent handoffs
4. If `.ai/` exists and topic seems code/architecture related, optionally run Explore agent:

```
Task(
  subagent_type: "Explore",
  prompt: """
  Explore this codebase for context relevant to this debate topic: {TOPIC}

  THOROUGHNESS: medium

  Read .ai/QUICK.md, .ai/ARCHITECTURE.json, .ai/PATTERNS.md
  Find relevant files, patterns, and constraints.

  Return max 300 words: key files, patterns, constraints, relevant context.
  """
)
```

5. If no `.ai/` folder, set `project_context` to null and proceed.

---

## Phase 2: Clarify (1 Round Only)

Ask the user 2-4 questions using AskUserQuestion or direct questions:

- What decision or outcome are you trying to reach?
- What constraints exist? (time, budget, team, technical)
- What does "good" look like? (success criteria)
- Any positions you're leaning toward?

**Lock the brief after answers.** Write `brief.md`:

```markdown
# Debate Brief

**Topic:** {topic}
**Date:** {ISO date}

## Decision
{What decision/outcome the user is trying to reach}

## Constraints
{Listed constraints}

## Success Criteria
{What "good" looks like}

## Initial Leaning
{Any positions the user is leaning toward, or "None stated"}

## Project Context
{Summary of .ai/ context if available, or "No project context"}
```

---

## Phase 3: Agent Array

```
agents = [
  { name: "Analyst A", type: "claude" },
  { name: "Analyst B", type: "codex" }
]
```

No forced personas or positions. Each model responds naturally. The value comes from inherent differences in how models approach, research, and frame problems.

---

## Phase 4: Round 1 (Parallel)

Spawn both agents in parallel. Each responds independently to the brief.

**Claude (Analyst A):** Task tool with debate-agent

```
Task(
  subagent_type: "general-purpose",
  model: "sonnet",
  prompt: """
  Read .claude/agents/debate-agent.md for your full protocol.

  ---
  topic: "{topic}"
  round: 1
  max_rounds: 3
  brief: |
    {brief.md content}
  context: |
    {project_context or "null"}
  previous_responses: ""
  analyst_name: "Analyst A"
  ---

  Provide your independent analysis following the debate-agent protocol.
  Use the Round 1: Opening Position schema.
  """
)
```

**Codex (Analyst B):** Bash with codex exec

```bash
codex exec --full-auto -- "$(cat <<'PROMPT'
You are an independent analyst providing your perspective on a topic.

Topic: {topic}

Brief:
{brief.md content}

Project Context:
{project_context or "None"}

Round 1 of 3. Provide your independent analysis.

Respond using this exact schema:

## Position
[1-3 sentences stating your core perspective]

## Key Arguments
- [Argument 1 with specific evidence/reasoning]
- [Up to 5 arguments]

## Risks & Failure Modes
- [Risk 1]
- [Up to 5 risks]

## Assumptions
- [What you're assuming]

## Confidence & Unknowns
- Confidence: High/Medium/Low
- Key unknowns: [What would change your view]

Be specific. Cite tradeoffs. Identify things others might miss.
PROMPT
)"
```

**After both return:**

Initialize and write `state.md`:

```markdown
# Debate State: {topic}

**Started:** {ISO timestamp}
**Rounds:** 3
**Agents:** Analyst A (Claude), Analyst B (Codex)

---

## Round 1

### Analyst A (Claude)

{Analyst A's full response}

### Analyst B (Codex)

{Analyst B's full response}
```

---

## Phase 5: Rounds 2-3 (Sequential Cross-Examination)

For each remaining round, each agent sees all previous responses.

**For each round (2, 3):**

**Claude (Analyst A):**

```
Task(
  subagent_type: "general-purpose",
  model: "sonnet",
  prompt: """
  Read .claude/agents/debate-agent.md for your full protocol.

  ---
  topic: "{topic}"
  round: {N}
  max_rounds: 3
  brief: |
    {brief.md content}
  context: |
    {project_context or "null"}
  previous_responses: |
    {All previous rounds from state.md}
  analyst_name: "Analyst A"
  ---

  Provide your cross-examination following the debate-agent protocol.
  Use the Rounds 2+: Cross-Examination schema.
  Build on what's useful, challenge what you disagree with, add what's missing.
  """
)
```

**Codex (Analyst B):**

```bash
codex exec --full-auto -- "$(cat <<'PROMPT'
You are an independent analyst cross-examining another analyst's perspective.

Topic: {topic}

Brief:
{brief.md content}

Project Context:
{project_context or "None"}

Round {N} of 3.

Previous rounds:
{All previous rounds from state.md}

Build on what's useful from Analyst A, challenge what you disagree with,
and add anything they missed. The goal is a more complete picture, not winning.

Respond using this exact schema:

## Position
[1-3 sentences - your core perspective]

## Key Arguments
- [Arguments with evidence]

## Risks & Failure Modes
- [Risks]

## Assumptions
- [What you're assuming]

## Confidence & Unknowns
- Confidence: High/Medium/Low
- Key unknowns: [What would change your view]

## What I Concede
[Points from the other analyst that are valid]

## What I Still Disagree With
[Points you maintain, with reasoning]

## New Evidence/Arguments
[New points not yet raised]

## Refined Position
[1-3 sentences - evolved position]

Be specific. Concede when warranted. Add what's missing.
PROMPT
)"
```

**After each agent responds:** Append to `state.md`:

```markdown
---

## Round {N}

### Analyst A (Claude)

{response}

### Analyst B (Codex)

{response}
```

### Codex Session Handling

If `codex exec resume` is available, use it for context persistence across rounds. Fall back to fresh `codex exec` with full state.md history injected if resume fails or is unavailable.

### Codex Failure Handling

If Codex fails (non-zero exit, empty output, rate limit):
1. Log: "Codex failed for Round {N}. Falling back to Claude."
2. Spawn a second Claude agent (Task tool, model: "haiku") with the same prompt
3. Label response as "Analyst B (Claude fallback)"
4. Continue the debate

---

## Phase 6: Synthesis

After all 3 rounds complete, read the full `state.md` and produce synthesis.

The orchestrator (you) synthesizes - do NOT spawn an agent for this.

### Synthesis Schema

```markdown
## Consensus
[Points both analysts agree on]

## Key Divergences
[Points where analysts still disagree, and why]

## Recommendation
[Based on the full debate, what the user should do]

## What to Validate Next
[Open questions, experiments to run, data to gather]

## Action Plan
1. [Step 1]
2. [Step 2]
3. [Up to 10 steps]
```

---

## Phase 7: Final Output

Assemble `debate.md` from all artifacts:

```markdown
# Debate: {topic}

**Date:** {ISO date}
**Rounds:** 3
**Analysts:** Claude (Analyst A), Codex (Analyst B)

---

{brief.md content}

---

{All rounds from state.md}

---

# Synthesis

{Synthesis content from Phase 6}
```

Write `debate.md` to `{cwd}/debates/{topic-slug}/debate.md`.

Print summary:

```
Debate complete.

Files:
- debates/{topic-slug}/brief.md
- debates/{topic-slug}/state.md
- debates/{topic-slug}/debate.md

{2-3 sentence summary of the recommendation}
```

---

## Error Handling

### Codex Not Available

If `codex` command is not found:
- Fall back to running Analyst B as a second Claude agent (Task tool, model: "haiku")
- Label as "Analyst B (Claude-haiku)"
- Log: "Codex not available. Using Claude-haiku as Analyst B."

### Agent Timeout

If an agent doesn't respond within 5 minutes (300s timeout on Bash):
- Log timeout
- Ask user: continue without that response, or retry?

### State File Corruption

If state.md can't be read:
- Reconstruct from agent responses collected in memory
- Log warning

---

## Quality Gates

- [ ] Topic parsed and slug generated
- [ ] Brief written and locked after clarification
- [ ] All 3 rounds completed with both agents
- [ ] state.md contains all responses
- [ ] Synthesis covers: consensus, divergences, recommendation, validation, action plan
- [ ] debate.md assembled with all sections
- [ ] File paths printed to user

---

**This orchestrator transforms complex decisions into structured multi-perspective analysis, leveraging the natural differences between models to build a more complete understanding than any single viewpoint could provide.**
