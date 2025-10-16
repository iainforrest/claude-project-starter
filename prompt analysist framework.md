# HIGH-POWERED PROMPT ANALYSIS FRAMEWORK v2.0
## Reference Document for System Prompt Analysis & Optimization

**Purpose:** Use this framework to evaluate existing system prompts against proven architectural patterns that maximize AI output quality, consistency, actionability, safety, and enterprise-readiness.

**How to Use:** When analyzing a prompt, check it against each criterion below. Identify gaps, structural weaknesses, and optimization opportunities WITHOUT making changes—only highlight what COULD be improved.

**NEW IN v2.0:** Added technical optimization, safety & ethics evaluation, testing protocols, and enterprise-grade quality controls.

---

## PART 1: FOUNDATIONAL ARCHITECTURE

### 1.1 AUTHORITY & ROLE FRAMING
**What it is:** The opening establishes WHO the AI is and WHAT expertise it brings.

**Quality Indicators:**
- ✅ Specific role title (not "helpful assistant" but "senior financial analyst" or "technical architect")
- ✅ Seniority/expertise level stated explicitly
- ✅ Domain context provided (industry, use case, type of work)
- ✅ Decision-making authority clarified (advisor, executor, reviewer)

**Anti-Patterns:**
- ❌ Generic positioning ("I'm here to help")
- ❌ No role specified or too vague ("expert in many fields")
- ❌ Missing context about WHY this role matters

**Evaluation Questions:**
1. Does the prompt establish a specific professional identity?
2. Would someone in that role recognize themselves in this framing?
3. Is the level of authority appropriate for the task?

---

### 1.2 TASK DEFINITION SPECIFICITY
**What it is:** Clear statement of WHAT the AI should produce and WHY.

**Quality Indicators:**
- ✅ Specific deliverable named (not "analysis" but "quarterly business review with action items")
- ✅ Purpose/goal stated explicitly
- ✅ Success criteria defined
- ✅ Scope boundaries clear (what's included/excluded)

**Anti-Patterns:**
- ❌ Vague objectives ("help the user")
- ❌ No clear deliverable specified
- ❌ Missing success criteria
- ❌ Scope creep potential (no boundaries)

**Evaluation Questions:**
1. Can you describe the output in one sentence?
2. Is it clear when the task is "complete"?
3. Are boundaries explicit (this not that)?

---

## PART 2: INPUT ARCHITECTURE

### 2.1 THREE-LAYER INPUT STRUCTURE
**What it is:** Organized approach to receiving information from the user.

**The Three Layers:**

**Layer 1: Raw Data Ingestion**
- Triple-quoted section for unstructured paste
- Clear label for what goes here
- Format agnostic (CSV, notes, emails, logs, etc.)
- Example provided if format is ambiguous
- **Multimodal handling:** Specifications for images, PDFs, audio/video

**Layer 2: Structured Context Variables**
- Specific fields to fill in
- Data type indicated (number, date, text, selection)
- Default values or ranges where applicable
- Required vs. optional clearly marked

**Layer 3: Constraints & Requirements**
- Limitations stated explicitly
- Non-negotiables identified
- Compliance/regulatory requirements
- Resource constraints

**Quality Indicators:**
- ✅ All three layers present and distinct
- ✅ Clear instructions for each layer
- ✅ No ambiguity about where information goes
- ✅ Multimodal inputs addressed when relevant (images, PDFs, documents)

**Anti-Patterns:**
- ❌ Everything mixed together
- ❌ No clear data ingestion point
- ❌ Constraints buried in prose
- ❌ User must guess what information is needed
- ❌ No guidance for non-text inputs

**Evaluation Questions:**
1. Is there a dedicated section for pasting raw data?
2. Are structured variables clearly defined?
3. Are constraints and requirements explicit?
4. Are multimodal inputs addressed if relevant?

---

## PART 3: OUTPUT ARCHITECTURE

### 3.1 HIERARCHICAL STRUCTURE SPECIFICATION
**What it is:** Pre-defined output format with nested levels of organization.

**Quality Indicators:**
- ✅ Multiple header levels defined (H2, H3, H4)
- ✅ Each section has a clear purpose
- ✅ Nesting logic is apparent (category → sub-category → detail)
- ✅ Order is intentional (priority-based or workflow-based)

**Anti-Patterns:**
- ❌ Flat structure (just one level)
- ❌ No clear organization principle
- ❌ Random ordering of sections
- ❌ Missing subsections for complex topics

**Evaluation Questions:**
1. Can you draw a visual hierarchy of the output?
2. Is there logical progression between sections?
3. Does each level serve a distinct purpose?

---

### 3.2 TABLE & DATA STRUCTURE MANDATES
**What it is:** Explicit use of tables with predefined columns for structured data presentation.

**Quality Indicators:**
- ✅ Tables used for comparative data
- ✅ Column headers specified in advance
- ✅ Data types per column clear (text, number, percentage, status)
- ✅ Sorting or ordering specified
- ✅ "Repeat for each X" instructions given

**Anti-Patterns:**
- ❌ Everything in prose when tables would be clearer
- ❌ Tables mentioned but structure not defined
- ❌ Inconsistent use across similar content types
- ❌ No guidance on how many rows/items

**Evaluation Questions:**
1. Where would tables improve clarity?
2. Are table structures fully specified?
3. Is there consistency in how similar data is presented?

---

### 3.3 COMPLETENESS REQUIREMENTS
**What it is:** Explicit instructions to be exhaustive, not selective.

**Quality Indicators:**
- ✅ "List ALL X" not "list some X"
- ✅ "For EACH item, provide Y" instructions
- ✅ Checklists for verification
- ✅ "Missing information" sections to flag gaps
- ✅ Minimum/maximum counts specified

**Anti-Patterns:**
- ❌ "Provide examples" (how many?)
- ❌ "List key points" (what makes something "key"?)
- ❌ No guidance on comprehensiveness
- ❌ Selective coverage allowed

**Evaluation Questions:**
1. Is it clear whether to be comprehensive or selective?
2. Are quantity expectations stated?
3. Is there a mechanism to flag missing data?

---

## PART 4: ANALYTICAL METHODOLOGY

### 4.1 DECISION FRAMEWORKS & FORMULAS
**What it is:** Explicit mathematical or logical systems for making judgments.

**Quality Indicators:**
- ✅ Prioritization formula stated (e.g., "Score = Impact × Urgency / Cost")
- ✅ Scoring systems defined (1-10 scale with anchor points)
- ✅ Rating criteria explicit (what makes something "high" vs "medium")
- ✅ Calculations shown in output (not just final scores)
- ✅ Multiple dimensions weighted appropriately

**Anti-Patterns:**
- ❌ "Prioritize based on importance" (no definition)
- ❌ Subjective ratings without criteria
- ❌ Hidden logic (scores without formulas)
- ❌ Inconsistent application of criteria

**Evaluation Questions:**
1. Are decision criteria mathematically defined?
2. Can someone else replicate the prioritization?
3. Are weights and factors explicit?

---

### 4.2 PATTERN RECOGNITION REQUIREMENTS
**What it is:** Instructions to identify trends, anomalies, and recurring themes.

**Quality Indicators:**
- ✅ "Red flags" section defined
- ✅ "Green lights" or positive indicators listed
- ✅ Threshold-based alerts (if X > Y, then Z)
- ✅ Pattern categories predefined
- ✅ Statistical vs. anecdotal distinction

**Anti-Patterns:**
- ❌ No guidance on what patterns matter
- ❌ Everything treated as equally important
- ❌ No threshold-based triggering
- ❌ Patterns mentioned but not categorized

**Evaluation Questions:**
1. What patterns should the AI look for?
2. Are thresholds for concern defined?
3. Is there a "watchlist" mechanism?

---

### 4.3 ROOT CAUSE & CAUSAL ANALYSIS
**What it is:** Multi-layer investigation beyond surface symptoms.

**Quality Indicators:**
- ✅ "Why" questions cascaded (Why → Why → Why)
- ✅ Primary vs. contributing factors separated
- ✅ Correlation vs. causation distinguished
- ✅ Evidence requirements stated
- ✅ Alternative explanations considered

**Anti-Patterns:**
- ❌ Stops at first-level symptoms
- ❌ Assumes causation from correlation
- ❌ No evidence standards
- ❌ Single explanation without alternatives

**Evaluation Questions:**
1. Does the prompt push beyond symptoms?
2. Are multiple causal layers required?
3. Is evidence explicitly demanded?

---

## PART 5: ACTION & ACCOUNTABILITY

### 5.1 OWNERSHIP ASSIGNMENT STRUCTURE
**What it is:** Every action has a specific owner, not vague "team" responsibility.

**Quality Indicators:**
- ✅ "Owner: [Specific role/person]" for each action
- ✅ Individual accountability, not diffused
- ✅ Escalation paths defined
- ✅ Approval authorities clear
- ✅ Cross-functional dependencies mapped

**Anti-Patterns:**
- ❌ "Team should do X" (which person?)
- ❌ No owner specified
- ❌ Shared accountability with no lead
- ❌ Missing escalation paths

**Evaluation Questions:**
1. Is every action assigned to someone?
2. Are accountability chains clear?
3. Who has authority at each level?

---

### 5.2 TIMELINE & DEADLINE SPECIFICITY
**What it is:** Temporal precision for every action.

**Quality Indicators:**
- ✅ Specific dates or relative timeframes ("by Q2 end", "within 2 weeks")
- ✅ Sequencing clear (A before B before C)
- ✅ Milestones defined
- ✅ Time-boxing applied (not open-ended)
- ✅ Critical path identified

**Anti-Patterns:**
- ❌ "Soon" or "eventually"
- ❌ "As soon as possible" (when exactly?)
- ❌ No sequencing logic
- ❌ Infinite timelines

**Evaluation Questions:**
1. Does every action have a deadline?
2. Is sequencing explicit?
3. What's the critical path?

---

### 5.3 SUCCESS METRICS PER ACTION
**What it is:** Verifiable completion criteria for each recommended action.

**Quality Indicators:**
- ✅ "Success Criteria: [Observable outcome]" for each action
- ✅ Quantitative where possible
- ✅ Qualitative with clear evidence
- ✅ Binary verification (done/not done)
- ✅ Inspection methods specified

**Anti-Patterns:**
- ❌ No definition of "done"
- ❌ Subjective completion criteria
- ❌ No measurement specified
- ❌ Cannot verify objectively

**Evaluation Questions:**
1. How do you know an action is complete?
2. Are metrics measurable or observable?
3. Who verifies completion?

---

## PART 6: QUALITY CONTROLS

### 6.1 ASSUMPTION VALIDATION MECHANISMS
**What it is:** Explicit acknowledgment and testing of assumptions.

**Quality Indicators:**
- ✅ "Assumptions:" section in analysis
- ✅ Each assumption labeled
- ✅ "Risk if wrong:" for each assumption
- ✅ Validation methods specified
- ✅ Confidence levels indicated

**Anti-Patterns:**
- ❌ Hidden assumptions
- ❌ Treating assumptions as facts
- ❌ No risk assessment of being wrong
- ❌ No validation plan

**Evaluation Questions:**
1. Are assumptions surfaced explicitly?
2. Are risks of wrong assumptions stated?
3. How are assumptions tested?

---

### 6.2 EDGE CASE & EXCEPTION HANDLING
**What it is:** Planning for non-standard scenarios.

**Quality Indicators:**
- ✅ "Edge cases:" section defined
- ✅ "If X happens, then Y" contingencies
- ✅ Exception handling procedures
- ✅ Boundary conditions specified
- ✅ Fallback options provided

**Anti-Patterns:**
- ❌ Only happy-path planning
- ❌ No contingency plans
- ❌ Ignoring outliers
- ❌ No guidance for exceptions

**Evaluation Questions:**
1. What could go wrong?
2. Are contingencies planned?
3. How are outliers handled?

---

### 6.3 CROSS-VALIDATION REQUIREMENTS
**What it is:** Internal consistency checks and external benchmarking.

**Quality Indicators:**
- ✅ Benchmark comparisons required
- ✅ Sanity checks defined
- ✅ Cross-referencing between sections
- ✅ Historical comparison included
- ✅ Peer/industry standards referenced

**Anti-Patterns:**
- ❌ Analysis in isolation
- ❌ No reality checks
- ❌ Inconsistencies across sections
- ❌ No external references

**Evaluation Questions:**
1. Are benchmarks specified?
2. What sanity checks exist?
3. Is cross-section consistency verified?

---

### 6.4 TESTING & EVALUATION FRAMEWORKS
**What it is:** Systematic methods for validating prompt performance.

**Quality Indicators:**
- ✅ A/B testing protocol defined
- ✅ Evaluation rubric with scoring criteria
- ✅ Success metrics clearly specified
- ✅ Comparison methodology established
- ✅ Statistical significance thresholds
- ✅ Sample size requirements for testing
- ✅ Performance tracking over time

**Anti-Patterns:**
- ❌ No testing plan
- ❌ Subjective evaluation only
- ❌ No success criteria defined
- ❌ Can't measure improvement
- ❌ One-shot testing without iteration

**Evaluation Questions:**
1. How will this prompt be tested?
2. What metrics determine success?
3. Is there a systematic evaluation approach?
4. Can performance be tracked over time?

---

### 6.5 DEBUGGING & TROUBLESHOOTING PROTOCOLS
**What it is:** Structured approaches to fixing prompt problems.

**Quality Indicators:**
- ✅ Common error patterns identified
- ✅ TRACE method or similar debugging workflow
  - Test: Run prompt and identify issues
  - Refine: Adjust one element at a time
  - Analyze: Compare results to requirements
  - Clarify: Add missing context/constraints
  - Evaluate: Check if fix worked
- ✅ Fix strategies for typical failures
- ✅ Escalation path for persistent issues
- ✅ Documentation of known issues and solutions

**Anti-Patterns:**
- ❌ No troubleshooting guidance
- ❌ Trial and error without system
- ❌ No error pattern recognition
- ❌ No knowledge base of fixes

**Evaluation Questions:**
1. Are common failure modes anticipated?
2. Is there a systematic debugging approach?
3. Are fix strategies documented?
4. Is there an escalation process for unsolvable issues?

---

## PART 7: SCENARIO & CONTINGENCY PLANNING

### 7.1 MULTI-SCENARIO MODELING
**What it is:** Best/worst/likely case analysis built into the structure.

**Quality Indicators:**
- ✅ Three scenarios required (optimistic/realistic/pessimistic)
- ✅ Probability estimates for each
- ✅ Assumptions per scenario explicit
- ✅ Impact quantified for each
- ✅ Trigger points defined (when scenario activates)

**Anti-Patterns:**
- ❌ Single-path prediction
- ❌ No scenario planning
- ❌ Best case assumed as likely
- ❌ No probabilistic thinking

**Evaluation Questions:**
1. Are multiple scenarios required?
2. Are probabilities assigned?
3. What triggers scenario changes?

---

### 7.2 IF-THEN DECISION TREES
**What it is:** Pre-programmed responses to specific conditions.

**Quality Indicators:**
- ✅ "If [condition], then [action]" statements
- ✅ Threshold-based triggering
- ✅ Escalation conditions defined
- ✅ Automatic vs. manual decisions separated
- ✅ Multiple condition branches

**Anti-Patterns:**
- ❌ Reactive only (no pre-planning)
- ❌ No conditional logic
- ❌ Everything requires judgment
- ❌ No automated responses

**Evaluation Questions:**
1. What conditions trigger specific actions?
2. Are thresholds defined?
3. What's automated vs. human decision?

---

## PART 8: COMMUNICATION & STAKEHOLDER MANAGEMENT

### 8.1 AUDIENCE-SPECIFIC OUTPUTS
**What it is:** Different summaries for different stakeholder levels.

**Quality Indicators:**
- ✅ Executive summary (leadership level)
- ✅ Technical details (implementation level)
- ✅ Communication templates provided
- ✅ Key messages per audience
- ✅ Jargon appropriate to each group

**Anti-Patterns:**
- ❌ One-size-fits-all output
- ❌ No summary for executives
- ❌ Wrong detail level for audience
- ❌ Missing communication plans

**Evaluation Questions:**
1. Who are the audiences?
2. Is content tailored to each?
3. Are communication templates included?

---

### 8.2 ESCALATION & REPORTING PROTOCOLS
**What it is:** When and how to communicate issues upward.

**Quality Indicators:**
- ✅ Escalation triggers defined
- ✅ Reporting cadence specified
- ✅ Information hierarchy (what to whom)
- ✅ Urgency indicators built in
- ✅ Communication channels specified

**Anti-Patterns:**
- ❌ No escalation criteria
- ❌ Ad hoc reporting only
- ❌ Everyone gets everything
- ❌ No urgency flagging

**Evaluation Questions:**
1. When should issues escalate?
2. What's the reporting schedule?
3. Who needs what information?

---

## PART 9: ITERATIVE IMPROVEMENT MECHANISMS

### 9.1 FEEDBACK LOOPS & LEARNING
**What it is:** Built-in mechanisms to improve over time.

**Quality Indicators:**
- ✅ "What worked / What didn't" reflection
- ✅ Metrics tracking over time
- ✅ Lessons learned documentation
- ✅ Prompt refinement suggestions
- ✅ Performance comparison (iteration N vs. N-1)

**Anti-Patterns:**
- ❌ Static, never-improving system
- ❌ No performance tracking
- ❌ Lessons not captured
- ❌ Same approach every time

**Evaluation Questions:**
1. How does the system learn?
2. Are improvements tracked?
3. Is feedback incorporated?

---

### 9.2 VERSION CONTROL & CHANGE TRACKING
**What it is:** Documentation of what changed and why.

**Quality Indicators:**
- ✅ Version numbers or dates
- ✅ Change log section
- ✅ Rationale for changes
- ✅ "What's new in this version"
- ✅ Backward compatibility notes

**Anti-Patterns:**
- ❌ No versioning
- ❌ Changes without documentation
- ❌ No change rationale
- ❌ Breaking changes without notice

**Evaluation Questions:**
1. Is versioning implemented?
2. Are changes documented?
3. Is there a changelog?

---

### 9.3 VERSION CONTROL & PERFORMANCE TRACKING
**What it is:** Systematic documentation of prompt evolution and performance.

**Quality Indicators:**
- ✅ Version numbering system (v1.0, v1.1, v2.0)
- ✅ Change log with rationale for each version
- ✅ Performance metrics per version
- ✅ Rollback capability to previous versions
- ✅ A/B test results documented
- ✅ User feedback integrated into versions

**Example Version Log:**
```
Version 1.0: Original prompt
- Performance: 75% satisfaction, avg 3.2s response time
- Issues: Too vague, inconsistent formatting

Version 1.1: Added specific examples (2025-01-15)
- Performance: 82% satisfaction, avg 3.5s response time
- Improvement: +7% satisfaction
- Change: Added 3 few-shot examples

Version 1.2: Refined tone instructions (2025-01-20)
- Performance: 79% satisfaction, avg 3.4s response time
- Result: -3% satisfaction (reverted to v1.1)

Version 2.0: Major restructure with new framework (2025-02-01)
- Performance: Testing in progress...
```

**Anti-Patterns:**
- ❌ No version tracking
- ❌ Changes without documentation
- ❌ Can't compare performance over time
- ❌ No rollback capability
- ❌ Lost history of what worked

**Evaluation Questions:**
1. Is version control implemented?
2. Are performance metrics tracked per version?
3. Can previous versions be restored?
4. Is there a systematic improvement process?

---

## PART 10: ANTI-PATTERN CATALOG

### Common Weaknesses in System Prompts

**10.1 Vagueness Vectors**
- Imprecise quantities ("some", "several", "a few")
- Subjective judgments without criteria ("important", "significant")
- Open-ended timelines ("soon", "later")
- Unspecified audiences ("stakeholders")
- Generic role framing ("assistant", "helper")

**10.2 Structural Deficiencies**
- Flat structure (no hierarchy)
- Inconsistent formatting
- Missing input specifications
- No output templates
- Prose-only (no tables or structured data)

**10.3 Analytical Gaps**
- No prioritization framework
- Missing decision criteria
- Assumption blindness
- No edge case handling
- Single-scenario thinking

**10.4 Accountability Voids**
- No owners assigned
- Vague deadlines
- Missing success metrics
- No escalation paths
- Shared responsibility without lead

**10.5 Quality Control Absences**
- No validation mechanisms
- Missing sanity checks
- No benchmarking
- Assumption risks unstated
- No cross-checking

---

## PART 11: TECHNICAL OPTIMIZATION

### 11.1 MODEL SUITABILITY ASSESSMENT
**What it is:** Evaluating if the prompt is optimized for the target AI model.

**Quality Indicators:**
- ✅ Model-specific strengths leveraged (e.g., Claude for analysis, GPT for creativity, Gemini for current info)
- ✅ Appropriate for model's context window limitations
- ✅ Parameters considered (temperature, top-p suggestions when relevant)
- ✅ Cost-efficiency considered (token usage optimization)
- ✅ Model limitations acknowledged (knowledge cutoff, hallucination risks)
- ✅ Fallback models specified if primary fails

**Anti-Patterns:**
- ❌ One-size-fits-all prompt ignoring model differences
- ❌ Prompt too long for model's context window
- ❌ No consideration of cost/token efficiency
- ❌ Parameter settings not specified when critical
- ❌ Doesn't account for model weaknesses

**Evaluation Questions:**
1. Is this prompt optimized for a specific model or model-agnostic?
2. Are parameter recommendations included where relevant?
3. Is token efficiency considered for cost control?
4. Are model limitations accounted for?

---

### 11.2 PROMPT CHAINING ASSESSMENT
**What it is:** Determining if complex tasks should be broken into sequential prompts.

**Quality Indicators:**
- ✅ Complex tasks broken into logical sub-tasks
- ✅ Clear handoff points between prompt steps
- ✅ Each step has defined inputs and outputs
- ✅ Workflow reduces cognitive load on single prompt
- ✅ Context preservation strategy between steps
- ✅ Error handling between chain steps

**Anti-Patterns:**
- ❌ Single mega-prompt trying to do too much
- ❌ No consideration of breaking into steps
- ❌ Tasks that would benefit from iteration crammed into one shot
- ❌ No strategy for passing context between steps

**Evaluation Questions:**
1. Should this be a prompt chain instead of a single prompt?
2. Are there natural breaking points in the workflow?
3. Would sequential prompts improve quality?
4. Is there a strategy for maintaining context across steps?

---

### 11.3 MULTIMODAL CAPABILITY LEVERAGE
**What it is:** Using multiple input types effectively (text, images, documents, data).

**Quality Indicators:**
- ✅ Clear instructions for each input type
- ✅ Appropriate use of multimodal inputs
- ✅ File format specifications when needed (PDF, PNG, MP3, etc.)
- ✅ Instructions for interpreting different data types
- ✅ Guidance on optimal image resolution or file sizes
- ✅ Fallback instructions if multimodal processing fails

**Anti-Patterns:**
- ❌ Ignoring multimodal capabilities when relevant
- ❌ No guidance on file formats accepted
- ❌ Unclear how different inputs relate to each other
- ❌ No file size or quality specifications
- ❌ Assumes all models support same multimodal features

**Evaluation Questions:**
1. Could images, PDFs, or other media improve this prompt?
2. Are instructions clear for handling multiple input types?
3. Are file format requirements specified?
4. Is there guidance for optimal file preparation?

---

## PART 12: SAFETY & ETHICAL SAFEGUARDS

### 12.1 BIAS DETECTION & MITIGATION
**What it is:** Mechanisms to prevent biased, discriminatory, or non-inclusive outputs.

**Quality Indicators:**
- ✅ Explicit instructions for inclusive language
- ✅ Warnings against stereotypical assumptions
- ✅ Requirements for diverse perspectives
- ✅ Checks for cultural sensitivity
- ✅ Gender-neutral language requirements
- ✅ Accessibility considerations (reading level, jargon avoidance)
- ✅ Geographic/cultural neutrality when appropriate

**Anti-Patterns:**
- ❌ No bias awareness in prompt design
- ❌ Assumptions about demographics embedded
- ❌ Single perspective without considering alternatives
- ❌ Language that could exclude or offend
- ❌ Western-centric assumptions
- ❌ Gendered language as default

**Evaluation Questions:**
1. Does the prompt guard against biased outputs?
2. Are inclusive language requirements specified?
3. Are diverse perspectives required in responses?
4. Is there cultural sensitivity awareness?

---

### 12.2 PRIVACY & CONFIDENTIALITY CONTROLS
**What it is:** Protections against exposing sensitive information.

**Quality Indicators:**
- ✅ Explicit prohibition on PII in outputs
- ✅ Confidentiality requirements stated
- ✅ Compliance frameworks referenced (GDPR, HIPAA, SOC 2, etc.)
- ✅ Instructions to anonymize examples
- ✅ Data handling protocols defined
- ✅ Redaction guidelines for sensitive info
- ✅ Clear boundaries on what can/cannot be shared

**Anti-Patterns:**
- ❌ No privacy considerations
- ❌ Could expose personal information
- ❌ Missing compliance requirements
- ❌ No anonymization instructions
- ❌ Unclear data retention implications
- ❌ No guidance on handling confidential business info

**Evaluation Questions:**
1. Does the prompt protect privacy appropriately?
2. Are confidentiality requirements clear?
3. Are compliance frameworks addressed if needed?
4. Is there guidance on anonymizing sensitive data?

---

### 12.3 CONTENT SAFETY MECHANISMS
**What it is:** Filters and guidelines to prevent harmful or inappropriate content.

**Quality Indicators:**
- ✅ Clear boundaries on acceptable content
- ✅ Fact vs. opinion distinction required
- ✅ Disclaimers for sensitive topics (medical, legal, financial advice)
- ✅ Refusal instructions for inappropriate requests
- ✅ Verification requirements for claims
- ✅ Source citation requirements for factual statements
- ✅ Transparency about AI limitations

**Anti-Patterns:**
- ❌ No content safety guidelines
- ❌ Could generate harmful advice
- ❌ No distinction between facts and opinions
- ❌ Missing disclaimers for sensitive topics
- ❌ No verification process for claims
- ❌ Could be mistaken for professional advice

**Evaluation Questions:**
1. Are content safety boundaries defined?
2. Are disclaimers included where needed?
3. Is fact verification required for claims?
4. Are AI limitations acknowledged?

---

## EVALUATION RUBRIC SUMMARY

Use this scoring system for overall prompt quality:

**Tier 1: Enterprise-Grade (90-100 points)**
- All 12 framework parts strongly present
- Decision frameworks explicit and mathematical
- Comprehensive input/output architecture
- Complete accountability structure
- Quality controls embedded throughout
- Technical optimization implemented
- Safety & ethical safeguards comprehensive

**Tier 2: Production-Ready (70-89 points)**
- Most framework parts present (10-11 of 12)
- Some decision frameworks defined
- Good input/output structure
- Basic accountability
- Some quality controls
- Basic technical considerations
- Some safety measures

**Tier 3: Functional Professional (50-69 points)**
- Core framework parts present (7-9 of 12)
- Minimal decision frameworks
- Basic structure exists
- Vague accountability
- Few quality controls
- Limited technical optimization
- Minimal safety considerations

**Tier 4: Needs Significant Work (<50 points)**
- Most framework parts missing (<7 of 12)
- No explicit decision frameworks
- Poor or absent structure
- No accountability mechanisms
- No quality controls
- No technical optimization
- No safety safeguards

---

## USAGE INSTRUCTIONS FOR PROMPT ANALYSIS

When analyzing an existing system prompt using this framework:

**Step 1: Initial Assessment**
- Read the prompt completely
- Identify which framework sections are present (all 12 parts)
- Note which are missing or weak

**Step 2: Section-by-Section Evaluation**
- For each framework part (1-12), score the prompt:
  - 🟢 Strong (all quality indicators present)
  - 🟡 Moderate (some indicators present)
  - 🔴 Weak (few/no indicators present)
  - ⚪ Absent (section not addressed)

**Step 3: Pattern Recognition**
- Identify recurring weaknesses (same score across multiple sections)
- Note anti-patterns from catalog
- Look for inconsistencies in approach
- Check for enterprise-readiness gaps

**Step 4: Prioritized Recommendations**
- **Critical:** Issues that undermine core functionality or safety
- **High:** Missing elements that significantly reduce quality or create risk
- **Medium:** Structural improvements for better consistency
- **Low:** Nice-to-have optimizations

**Step 5: Specific Callouts**
For each recommendation, provide:
- Current state (quote relevant section)
- Issue identified (which framework element is weak/missing)
- Potential improvement (what COULD be added/changed)
- Expected impact (why this matters)
- **DO NOT rewrite the prompt—only highlight opportunities**

**Step 6: Quick Wins vs. Deep Restructuring**
- Separate easy fixes (add a section) from major rework (reorganize entire structure)
- Estimate effort level for each recommendation
- Sequence recommendations logically
- Identify which improvements provide best ROI

---

## FINAL REMINDER

The goal of using this framework is to:
1. **Identify** what's working well (preserve these elements)
2. **Highlight** what could be improved (without making changes)
3. **Prioritize** recommendations by impact
4. **Estimate** effort required for each improvement
5. **Respect** the existing prompt's intent and domain
6. **Ensure** enterprise-grade quality, safety, and ethics

**DO NOT:**
- Rewrite the prompt automatically
- Change the core purpose or domain
- Remove elements without explaining why
- Make assumptions about the user's goals
- Ignore safety or ethical implications

**DO:**
- Point out structural opportunities
- Reference this framework explicitly
- Provide specific, actionable observations
- Highlight safety and technical gaps
- Let the user decide what to change

**NEW IN v2.0:** This framework now evaluates technical optimization (Part 11), safety & ethical safeguards (Part 12), and enhanced testing protocols (Part 6.4-6.5). These additions reflect the maturation of prompt engineering from prototype to production-ready, enterprise-grade systems.