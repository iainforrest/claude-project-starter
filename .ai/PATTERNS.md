# Implementation Patterns

*Copy-paste templates for consistent implementation*

## Overview

This file contains reusable implementation patterns discovered in this project. Each pattern includes:
- **When to Use**: Guidance on when to apply the pattern
- **Template**: Copy-paste ready code
- **Implementation Checklist**: Steps to follow
- **Pattern Reference**: Link to actual implementation in codebase

## Architectural Patterns

### Example: Service Layer Pattern

**When to Use:**
- Business logic that doesn't belong in controllers
- Logic used by multiple endpoints
- Complex operations requiring multiple data sources

**Template:**
```[language]
class ExampleService {
  constructor(private repository: ExampleRepository) {}

  async createItem(data: CreateItemDTO): Promise<Item> {
    // 1. Validate input
    this.validateItemData(data);

    // 2. Business logic
    const item = await this.repository.create(data);

    // 3. Side effects (notifications, logging, etc.)
    await this.notificationService.sendNotification(item);

    return item;
  }

  private validateItemData(data: CreateItemDTO): void {
    // Validation logic
  }
}
```

**Implementation Checklist:**
- [ ] Dependency injection for all dependencies
- [ ] Input validation before processing
- [ ] Error handling with appropriate error types
- [ ] Logging at key decision points
- [ ] Unit tests with mocked dependencies

**Pattern Reference**: `services/ExampleService.ext:45`

---

## Code Templates

*Add specific code templates as you discover patterns in your project*

### Example: Error Handling Pattern

**Template:**
```[language]
try {
  const result = await this.someOperation();
  return { success: true, data: result };
} catch (error) {
  logger.error('Operation failed', error);
  return { success: false, error: error.message };
}
```

---

## Testing Patterns

*Add testing patterns as you establish testing approaches*

### Example: Unit Test Pattern

**Template:**
```[language]
describe('ExampleService', () => {
  let service: ExampleService;
  let mockRepository: MockRepository;

  beforeEach(() => {
    mockRepository = {
      create: jest.fn(),
      findById: jest.fn(),
    };
    service = new ExampleService(mockRepository);
  });

  it('should create item with valid data', async () => {
    const itemData = { name: 'Test', value: 123 };
    mockRepository.create.mockResolvedValue({ id: 1, ...itemData });

    const result = await service.createItem(itemData);

    expect(result.id).toBe(1);
    expect(mockRepository.create).toHaveBeenCalledWith(itemData);
  });
});
```

---

## UI Patterns

*Add UI component patterns as you discover them*

---

## Data Patterns

*Add data access and repository patterns as needed*

---

## Integration Patterns

*Add API integration and external service patterns*

---

## Notes

- Update this file as you discover new patterns
- Include working code examples from actual implementation
- Reference real file locations for pattern examples
- Keep patterns condensed and focused on core concepts
