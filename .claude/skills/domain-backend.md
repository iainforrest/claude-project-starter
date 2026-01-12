---
name: Backend/API Development
domain: backend
description: Patterns and best practices for server-side development across Node.js, Python, Java, Go, and general backend work. Covers service layers, data access, API design, error handling, validation, and auth awareness.
file_patterns:
  - "*/api/*"
  - "*/services/*"
  - "*/controllers/*"
  - "*/routes/*"
  - "*/handlers/*"
---

## Patterns to Apply

### Service Layer Architecture
- Encapsulate business logic in service classes/modules separate from routes/controllers
- Services handle orchestration, validation rules, and complex operations
- Controllers/routes delegate to services, handle HTTP concerns only
- Example: `UserService.create()` validates input, checks uniqueness, hashes password, returns domain object

### Repository/Data Access Pattern
- Abstract database queries behind repository interfaces
- Single repository per entity/aggregate root
- Repositories handle CRUD operations and complex queries
- Services use repositories; controllers don't access data directly
- Enables easy testing (mock repositories) and database swaps

### API Design
- **REST conventions:** Use appropriate HTTP methods (GET, POST, PUT, PATCH, DELETE)
- **Versioning:** Consider `/v1/`, `/v2/` in path or Content-Type header
- **Status codes:** Return correct codes (200, 201, 204, 400, 401, 403, 404, 409, 500)
- **Pagination:** Use `offset`/`limit` or cursor-based patterns consistently
- **Filtering:** Design query params clearly; document supported filters
- **Error responses:** Consistent error shape with code, message, details

### Error Handling & Logging
- Create custom error classes for domain errors vs system errors
- Log errors with context: request ID, user ID, operation type, stack trace
- Never log sensitive data (passwords, tokens, PII)
- Distinguish between client errors (4xx) and server errors (5xx) in responses
- Use structured logging (JSON format) for easier parsing

### Input Validation
- Validate at API boundary before passing to services
- Use schema validation libraries (Joi, Zod, Pydantic, Jackson, etc.)
- Validate types, required fields, format (email, URL), length constraints
- Return validation errors with specific field paths and messages
- Don't trust client input; validate consistently across all endpoints

### Authentication & Authorization
- Don't store auth logic in controllers; delegate to auth middleware/services
- Use middleware to verify tokens/sessions before route handlers execute
- Separate authentication (who are you?) from authorization (what can you do?)
- Include auth checks early in request pipeline
- Log authentication failures and suspicious access patterns

## Pitfalls to Avoid

- **Anemic services:** Services that only delegate to repositories without business logic
- **God objects:** Controllers/services that handle multiple concerns (validation, logging, caching, data access)
- **Direct database queries in routes:** Breaks testability and separation of concerns
- **Inconsistent error handling:** Mix of exceptions, status codes, error shapes across endpoints
- **No input validation:** Trusting client data leads to bugs, security issues, data corruption
- **Logging in production:** Debug logs in production code reduce performance and expose internals
- **Hardcoded auth checks:** Auth logic scattered across handlers instead of centralized middleware
- **Missing transaction handling:** Multi-step operations not wrapped in transactions causing partial failures
- **N+1 queries:** Loading related data in loops instead of batching or joining
- **Storing state in class fields:** Makes code non-thread-safe; use dependency injection with immutable config

## Quality Checks

- [ ] Service layer exists and contains business logic (not just delegation)
- [ ] Repositories abstract all data access; no direct DB queries in services/controllers
- [ ] Error handling is consistent across all endpoints (same error shape/status codes)
- [ ] Input validation occurs at API boundary using schema validator
- [ ] Sensitive data never logged (credentials, tokens, PII)
- [ ] Auth middleware checks tokens/sessions before route handlers execute
- [ ] No hardcoded auth checks; authorization is centralized or consistent
- [ ] Tests exist for services (with mocked repositories) and integration tests for APIs
- [ ] HTTP method and status code choices match REST conventions
- [ ] API documentation exists (comments, OpenAPI spec, or README examples)
