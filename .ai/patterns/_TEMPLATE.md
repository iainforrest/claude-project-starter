# [DOMAIN] Patterns

*[Domain]-specific implementation patterns for [Project Name]*

## Pattern Template

Each pattern follows this structure:

```markdown
## Pattern Name

### When to Use
- Trigger condition 1
- Trigger condition 2

### Template
```[language]
// Copy-paste ready code
// Minimal, focused implementation
```

### Checklist
- [ ] Implementation step 1
- [ ] Implementation step 2
- [ ] Verification step

**Reference**: FileName.ext:lineNumber
**Benefits**: Key advantages (optional)
**Impact**: Performance/cost metrics (optional)
```

---

## How to Create Domain Pattern Files

### 1. Identify Your Domains

Common domains (create files as needed):
- `WEB.md` - Frontend patterns (components, state, routing)
- `API.md` - Backend patterns (endpoints, middleware, validation)
- `DATABASE.md` - Data access patterns (queries, migrations, repositories)
- `TESTING.md` - Test patterns (unit, integration, e2e)
- `INFRASTRUCTURE.md` - DevOps patterns (deployment, logging, monitoring)
- `AUTH.md` - Authentication/authorization patterns
- `[CUSTOM].md` - Project-specific domains

### 2. Keep Patterns Focused

- One domain per file (~300-500 lines)
- Each pattern should be copy-paste ready
- Include actual file:line references from your codebase
- Update references when code changes

### 3. Update PATTERNS.md Index

When adding a new domain file:
1. Create `patterns/[DOMAIN].md`
2. Add entry to `PATTERNS.md` index
3. Add to Quick Pattern Lookup table

---

## Example Pattern

## Service Layer Pattern

### When to Use
- Business logic that doesn't belong in controllers
- Logic shared across multiple endpoints
- Complex operations with transactions

### Template
```typescript
@Injectable()
export class UserService {
  constructor(
    private readonly userRepo: UserRepository,
    private readonly emailService: EmailService
  ) {}

  async createUser(data: CreateUserDto): Promise<User> {
    // Validate
    await this.validateUserData(data);

    // Business logic
    const user = await this.userRepo.create(data);

    // Side effects
    await this.emailService.sendWelcome(user.email);

    return user;
  }
}
```

### Checklist
- [ ] Dependency injection for all dependencies
- [ ] Input validation before processing
- [ ] Error handling with typed exceptions
- [ ] Unit tests with mocked dependencies

**Reference**: services/UserService.ts:45
**Benefits**: Testable, reusable, single responsibility

---

## Pattern Categories

Organize patterns within domain files by:

### By Complexity
- **Basic** - Simple, common patterns
- **Intermediate** - Patterns with some nuance
- **Advanced** - Complex patterns for edge cases

### By Purpose
- **Creation** - Creating new entities/resources
- **Modification** - Updating existing data
- **Query** - Reading/searching data
- **Integration** - Connecting systems

---

## Maintenance

### When to Add Patterns
- After implementing a reusable solution
- When you copy-paste the same code structure
- After code review identifies a good pattern
- When onboarding reveals common questions

### When to Update Patterns
- Line number references change significantly
- Better implementation discovered
- Framework/library updates require changes
- Pattern causes issues in practice

### Token Budget
- Target: ~400 lines per domain file
- Token cost: ~2,500 tokens per file
- Load only the domain you need for current task

---

*Replace this template content with your actual patterns as you discover them.*
