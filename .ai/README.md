# AI Memory System Guide

## What This Is

The `.ai/` folder is your project's **persistent memory system** for AI-assisted development. It prevents context loss between Claude sessions by storing structured knowledge about your project.

### The Problem It Solves

Without this system:
- Claude "forgets" your project between sessions
- You repeat the same explanations constantly
- Architectural decisions get lost
- File locations are re-discovered every time
- Pattern inconsistency across features

With this system:
- Claude has instant access to project knowledge
- Zero repeated explanations
- Architecture stays consistent
- Files referenced with line numbers
- Patterns reused systematically

## Philosophy

**AI works best with persistent, structured knowledge.**

This system provides that knowledge in machine-readable formats (JSON) and human-readable documents (Markdown) that Claude consults before any work.

## The Files

### Core Concept

Each file serves a specific purpose. Together, they form a complete knowledge graph of your project.

---

## ARCHITECTURE.json

**Purpose**: Document your project's architectural patterns, data flows, and component relationships.

### What Goes Here

**1. Core Patterns**
Document the key architectural patterns you use:
```json
"corePatterns": {
  "servicePattern": {
    "description": "How services are structured",
    "keyFiles": ["ServiceName.ext:lineNumber"],
    "constraints": ["Limitation 1", "Limitation 2"],
    "benefits": ["Benefit 1", "Benefit 2"]
  }
}
```

**2. Data Flows**
Map how data moves through your system:
```json
"dataFlows": {
  "userAuthentication": {
    "steps": ["User submits credentials", "Validate", "Generate token", "Return to client"],
    "keyFiles": ["AuthService.ext:123", "TokenManager.ext:45"],
    "dataModel": "User + Token"
  }
}
```

**3. Layer Architecture**
Document your architectural layers:
```json
"layers": {
  "presentation": {
    "description": "UI layer",
    "pattern": "MVVM / MVC / Component-based",
    "keyFiles": ["components/", "views/"]
  },
  "business": {
    "description": "Business logic layer",
    "pattern": "Service classes / Managers",
    "keyFiles": ["services/", "managers/"]
  }
}
```

**4. Integration Points**
Document how external systems integrate:
```json
"integrationPoints": {
  "database": {
    "type": "PostgreSQL / MongoDB / etc.",
    "pattern": "Repository pattern / ORM",
    "keyFiles": ["repositories/", "models/"]
  },
  "externalAPIs": {
    "apis": ["API name", "Another API"],
    "pattern": "HTTP client pattern",
    "keyFiles": ["clients/ApiClient.ext"]
  }
}
```

### When to Update

- After implementing a new architectural pattern
- When data flows change
- When adding new integration points
- When refactoring architecture
- At end of each sprint

### Example Use Case

Claude reads ARCHITECTURE.json before implementing a feature to understand:
- Which pattern to follow
- Where files should go
- How components interact
- What constraints exist

---

## BUSINESS.json

**Purpose**: Document business logic, feature specifications, and product requirements.

### What Goes Here

**1. Feature Map**
Track all features and their status:
```json
"features": {
  "userAuthentication": {
    "status": "complete",
    "version": "v1.0",
    "description": "Email/password authentication with JWT",
    "keyComponents": ["AuthService", "TokenManager", "LoginUI"]
  },
  "dataExport": {
    "status": "in-progress",
    "version": "v0.5",
    "description": "Export user data to CSV/JSON",
    "keyComponents": ["ExportService", "FormatConverter"]
  }
}
```

**2. Business Rules**
Document key business logic:
```json
"businessRules": {
  "userRegistration": {
    "rules": [
      "Email must be unique",
      "Password minimum 8 characters",
      "Email verification required"
    ],
    "exceptions": ["Admin users skip email verification"]
  }
}
```

**3. User Flows**
Map critical user workflows:
```json
"userFlows": {
  "checkout": {
    "steps": [
      "Add items to cart",
      "Review cart",
      "Enter shipping info",
      "Enter payment",
      "Confirm order"
    ],
    "keyScreens": ["Cart", "Checkout", "Confirmation"],
    "keyFiles": ["CheckoutService.ext", "PaymentHandler.ext"]
  }
}
```

**4. Performance Targets**
Document performance requirements:
```json
"performanceTargets": {
  "apiResponse": {
    "target": "< 200ms",
    "measured": "150ms average",
    "critical": true
  },
  "pageLoad": {
    "target": "< 2 seconds",
    "measured": "1.8 seconds",
    "critical": false
  }
}
```

**5. Data Models**
Document key data structures:
```json
"dataModels": {
  "User": {
    "fields": ["id", "email", "name", "createdAt"],
    "relationships": ["has many Orders", "has one Profile"]
  }
}
```

### When to Update

- When adding new features
- When business rules change
- When user flows are modified
- After measuring performance
- At end of each sprint

### Example Use Case

Claude reads BUSINESS.json to understand:
- What features exist
- What business rules to follow
- Performance targets to meet
- Data model structure

---

## FILES.json

**Purpose**: Smart file index with cross-references and quick navigation.

### What Goes Here

**1. By Purpose**
Organize files by their functional purpose:
```json
"byPurpose": {
  "authentication": {
    "primary": ["AuthService.ext:45", "TokenManager.ext:123"],
    "support": ["UserModel.ext", "AuthMiddleware.ext"],
    "tests": ["AuthService.test.ext"]
  },
  "dataProcessing": {
    "primary": ["DataProcessor.ext:67"],
    "support": ["Validator.ext", "Transformer.ext"],
    "tests": ["DataProcessor.test.ext"]
  }
}
```

**2. By Layer**
Organize files by architectural layer:
```json
"byLayer": {
  "presentation": {
    "files": ["components/", "views/", "screens/"],
    "pattern": "Component-based UI"
  },
  "business": {
    "files": ["services/", "managers/", "use-cases/"],
    "pattern": "Service layer"
  },
  "data": {
    "files": ["repositories/", "models/", "database/"],
    "pattern": "Repository pattern"
  }
}
```

**3. Dependencies**
Map file relationships:
```json
"dependencies": {
  "AuthService.ext": {
    "uses": ["TokenManager.ext", "UserRepository.ext"],
    "usedBy": ["LoginController.ext", "RegisterController.ext"],
    "tests": "AuthService.test.ext"
  }
}
```

**4. Key Interfaces**
Document critical interfaces/contracts:
```json
"keyInterfaces": {
  "IAuthService": {
    "file": "interfaces/IAuthService.ext",
    "implementations": ["AuthService.ext", "MockAuthService.ext"],
    "methods": ["login", "logout", "register", "validateToken"]
  }
}
```

### When to Update

- When adding new files
- When moving/renaming files
- When dependencies change
- When discovering new patterns
- At end of each sprint

### Example Use Case

Claude reads FILES.json to:
- Find where authentication code lives
- Understand file dependencies
- Locate test files
- Navigate to specific line numbers

---

## PATTERNS.md

**Purpose**: Implementation patterns and copy-paste templates.

### What Goes Here

**1. Architectural Patterns**
Document reusable patterns with code examples:

```markdown
## Service Layer Pattern

### When to Use
- Business logic that doesn't belong in controllers
- Logic used by multiple endpoints
- Complex operations requiring multiple data sources

### Template
```[language]
class UserService {
  constructor(private userRepo: UserRepository) {}

  async createUser(data: CreateUserDTO): Promise<User> {
    // Validate
    this.validateUserData(data);

    // Business logic
    const user = await this.userRepo.create(data);

    // Side effects
    await this.emailService.sendWelcome(user.email);

    return user;
  }
}
```

### Implementation Checklist
- [ ] Dependency injection for all dependencies
- [ ] Input validation
- [ ] Error handling with custom exceptions
- [ ] Logging at key points
- [ ] Unit tests with mocked dependencies

**Pattern Reference**: `services/UserService.ext:45`
```

**2. Code Templates**
Provide copy-paste templates for common tasks:

```markdown
## API Endpoint Pattern

### Template
```[language]
@route('/api/resource')
class ResourceController {
  @get('/:id')
  async getById(req: Request): Promise<Response> {
    try {
      const id = req.params.id;
      const resource = await this.service.findById(id);
      return response.ok(resource);
    } catch (error) {
      return response.error(error);
    }
  }
}
```

**Pattern Reference**: `controllers/BaseController.ext:23`
```

**3. Testing Patterns**
Document testing approaches:

```markdown
## Unit Test Pattern

### Template
```[language]
describe('UserService', () => {
  let service: UserService;
  let mockRepo: jest.Mocked<UserRepository>;

  beforeEach(() => {
    mockRepo = {
      create: jest.fn(),
      findById: jest.fn(),
    };
    service = new UserService(mockRepo);
  });

  it('should create user with valid data', async () => {
    const userData = { email: 'test@example.com', name: 'Test' };
    mockRepo.create.mockResolvedValue({ id: 1, ...userData });

    const result = await service.createUser(userData);

    expect(result.id).toBe(1);
    expect(mockRepo.create).toHaveBeenCalledWith(userData);
  });
});
```

**Pattern Reference**: `tests/services/UserService.test.ext:12`
```

### When to Update

- When discovering new patterns
- When creating reusable templates
- When refactoring common code
- After code reviews reveal patterns
- At end of each sprint

### Example Use Case

Claude reads PATTERNS.md to:
- Copy templates for new features
- Follow established patterns
- Ensure consistency
- Avoid reinventing wheels

---

## QUICK.md

**Purpose**: Quick reference for commands, file locations, and debugging.

### What Goes Here

**1. Build & Development Commands**
```markdown
### Build Commands
[BUILD_COMMAND]          # Build the project
[TEST_COMMAND]           # Run tests
[DEV_COMMAND]            # Start development server
[DEPLOY_COMMAND]         # Deploy to production
```

**2. File Quick Lookup**
```markdown
### Critical File Locations
AuthService.ext:45       # Main authentication logic
UserModel.ext:12         # User data model
config.ext:23            # Application configuration
routes.ext:67            # API route definitions
```

**3. Debugging Commands**
```markdown
### Debugging
[DEBUG_COMMAND]          # Start with debugger
[LOG_COMMAND]            # View application logs
[TEST_SINGLE_COMMAND]    # Run single test file
```

**4. Performance Monitoring**
```markdown
### Performance
[PROFILE_COMMAND]        # Profile performance
[ANALYZE_COMMAND]        # Analyze bundle/build size
```

**5. Emergency Fixes**
```markdown
### Common Issues

**Issue**: Authentication not working
**Fix**: Check token expiry in TokenManager.ext:89

**Issue**: Database connection fails
**Fix**: Verify DATABASE_URL in .env

**Issue**: Tests failing
**Fix**: Clear test database: [COMMAND]
```

### When to Update

- When adding new commands
- When file locations change
- After discovering debugging techniques
- After fixing recurring issues
- Continuously as needed

### Example Use Case

Claude reads QUICK.md for:
- Build/test commands
- Quick file navigation
- Debugging approaches
- Emergency fixes

---

## SPRINT_UPDATE.md

**Purpose**: Process guide for updating the memory system.

### What's Already There

This file is mostly pre-written with the update process. You don't need to modify it much.

### What to Update

- Add any project-specific update procedures
- Document any custom validation steps

### When to Update

- Rarely - the process is mostly generic
- Only when you discover better update workflows

---

## TODO.md

**Purpose**: Track current and completed tasks.

### What Goes Here

**1. Current Sprint Tasks**
```markdown
## Current Sprint: Sprint 5 - User Notifications

- [ ] Design notification system architecture
- [ ] Implement push notification service
- [ ] Create notification UI components
- [ ] Add notification preferences to user settings
```

**2. Completed Tasks**
```markdown
## Completed Tasks

- [x] Sprint 4 - User Dashboard (Completed: 2025-10-15)
  - Implemented dashboard layout
  - Added analytics widgets
  - Created customization options

- [x] Sprint 3 - User Profile (Completed: 2025-10-08)
  - Profile editing functionality
  - Avatar upload
  - Privacy settings
```

**3. Backlog**
```markdown
## Backlog

- [ ] Implement dark mode
- [ ] Add export to PDF feature
- [ ] Optimize database queries
```

### When to Update

- At start of each sprint (add new tasks)
- At end of each sprint (move completed)
- When priorities change
- Continuously as tasks evolve

---

## How to Use the Memory System

### Daily Workflow

**Before implementing any feature:**

1. **Read QUICK.md** - Get oriented with file locations and commands
2. **Read ARCHITECTURE.json** - Understand architectural approach
3. **Read PATTERNS.md** - Find relevant templates
4. **Read BUSINESS.json** - Check business rules and requirements
5. **Implement** - Using knowledge from memory

**This takes 30 seconds and prevents hours of mistakes.**

### When to Update

**After each sprint:**
1. Follow SPRINT_UPDATE.md process
2. Update all relevant files
3. Add new patterns discovered
4. Update performance measurements

**Continuously:**
- Add files to FILES.json as created
- Update TODO.md as tasks evolve
- Add debugging solutions to QUICK.md

### Validation

**Periodically check:**
- Are file references still accurate?
- Are patterns still current?
- Is architecture documentation up-to-date?
- Are performance targets being met?

## Benefits

### Short Term
- Claude always knows your project context
- Faster feature development
- Consistent implementation patterns
- No repeated explanations

### Long Term
- Living documentation that stays current
- Onboarding new team members is instant
- Architecture decisions are preserved
- Project knowledge isn't lost

## Tips

**Start Small**
- Don't try to document everything at once
- Add to memory files as you learn
- Grow the system organically

**Keep It Current**
- Update after each sprint (minimum)
- Quick updates are better than perfect documentation
- Accuracy > Completeness

**Use It Actively**
- Reference memory before every feature
- Let Claude read memory before tasks
- Trust the system to prevent mistakes

**Make It Yours**
- Adapt the structure to your project
- Add sections that make sense for you
- Remove what doesn't work

## Memory File Sizes

Target sizes (guidelines, not limits):
- ARCHITECTURE.json: 200-500 lines
- BUSINESS.json: 300-800 lines
- FILES.json: 200-600 lines
- PATTERNS.md: 500-2000 lines
- QUICK.md: 100-400 lines
- TODO.md: 50-200 lines
- SPRINT_UPDATE.md: ~200 lines (mostly static)

**Total: ~3000 lines across all files**

Keep it condensed and efficient.

## Common Mistakes

**Mistake 1**: Creating separate documentation files
- ❌ Don't: Create SPRINT_X_COMPLETION.md files
- ✅ Do: Update the core memory files with sprint learnings

**Mistake 2**: Letting memory get stale
- ❌ Don't: Forget to update after sprints
- ✅ Do: Update regularly, even if briefly

**Mistake 3**: Over-documenting
- ❌ Don't: Document every single detail
- ✅ Do: Focus on patterns, architecture, and key decisions

**Mistake 4**: Not using the memory
- ❌ Don't: Let Claude work without reading memory
- ✅ Do: Always reference memory before features

## Getting Started

After bootstrap completes:

1. **Review initialized files** - See what bootstrap created
2. **Add project-specific details** - Enhance with your knowledge
3. **Start first feature** - Use memory immediately
4. **Update after implementation** - Add what you learned
5. **Repeat** - Memory grows with your project

## Questions?

The system is self-documenting:
- Read this file for memory system guidance
- Read ../README.md for overall system guidance
- Read ../.claude/*.md for workflow guidance

Everything you need is here.

---

**The memory system is your project's brain. Keep it healthy and it will keep your project healthy.** 🧠
