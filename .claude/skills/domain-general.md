---
name: domain-general
domain: general-software-engineering
description: Fallback skill for senior developer best practices. Universal patterns for clean code, SOLID, error handling, testing, and documentation.
---

# Senior Developer Best Practices

Universal software engineering principles applied when no specialized domain is detected.

## Patterns to Apply

**Clean Code**: Clarity over cleverness. Meaningful names. Single responsibility. Small functions (20-30 lines). DRY. Self-documenting.

**SOLID**: Single Responsibility, Open/Closed, Liskov Substitution, Interface Segregation, Dependency Inversion.

**Error Handling**: Fail explicitly. Meaningful messages. Fail fast at boundaries. Test error paths. Log context.

**Testing**: Test critical paths and edge cases. Test behavior not implementation. Isolate tests. Clear test names.

**Documentation**: Comments explain "why". Public API docs. Document decisions. README with setup/run/test.

**Code Review Ready**: Logical commits. Descriptive messages. No debug code. Consistent style. Tests included.

## Pitfalls to Avoid

**Quality**: Overly complex logic. Magic numbers. God objects. Over-commenting.

**Errors**: Silent failures. Generic catches. Context-free messages. Unvalidated input. Unhandled cleanup.

**Testing**: Testing implementation. Shared mutable state. Over-mocking. No negative tests.

**Docs**: Outdated docs. Missing examples. Missing architecture. No migration guides.

**Design**: Premature optimization. Over-engineering. Leaky abstractions. Tight coupling.

## Quality Checks

- [ ] Readable? New developer understands without help?
- [ ] Error handling explicit? Failures informative?
- [ ] Critical paths and edge cases tested?
- [ ] Names clear and intent-expressing?
- [ ] Single responsibility? Focused scope?
- [ ] Non-obvious decisions documented?
- [ ] Safe to change and maintain?
- [ ] Follows codebase patterns?
- [ ] No obvious inefficiencies?
- [ ] Inputs validated? Secrets protected?

**Version**: 1.0 | **Updated**: 2026-01-12
