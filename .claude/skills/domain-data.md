---
name: domain-data
domain: Data Layer Development
description: Patterns for database design, ORMs, migrations, query optimization, and data access. Covers transaction handling, caching strategies, N+1 prevention, and data validation at boundaries.
file_detection: ["*/models/*", "*/repositories/*", "*/migrations/*", "*/schemas/*", "*.prisma", "*.sql"]
---

# Data Layer Development Patterns

Domain-specific patterns for database design, data access, and query optimization.

---

## Patterns to Apply

### Query Optimization & N+1 Prevention
- **Eager Loading**: Use `.include()` or `.with()` for relationships needed in responses
- **Selective Select**: Query only required columns, not entire rows
- **Batch Operations**: Load related data with `IN` clauses, never in loops
- **Indexing**: Ensure WHERE and JOIN columns are indexed (verify with EXPLAIN)
- **Pagination**: Never fetch unlimited result sets; use LIMIT/OFFSET for > 1000 rows

### Transaction Handling
- **ACID Scope**: All multi-step operations wrapped in explicit transactions
- **Error Handling**: Catch exceptions and trigger rollback on failures
- **Minimal Duration**: Keep transactions < 1 second; avoid I/O or user input inside
- **Isolation Level**: Use READ_COMMITTED for most cases (safer than dirty read)
- **Lock Ordering**: Acquire locks in consistent order to prevent deadlocks

### Migration Best Practices
- **Reversibility**: Both UP and DOWN migrations must work correctly
- **Zero-Downtime**: Add nullable columns first, backfill, then add constraints
- **Batched Data**: Migrate in 1000-10000 row chunks to avoid locking tables
- **Index Timing**: Create indexes AFTER data insertion, not before
- **Deployment Order**: Run migration before code deployment to support both versions

### Caching Strategy
- **TTL-Based**: Set appropriate expiration (1 hour typical for user data, 24h for static)
- **Event Invalidation**: Delete cache keys on data mutations (UPDATE, DELETE)
- **Eviction Policy**: Configure LRU or similar to prevent unbounded memory growth
- **Stampede Prevention**: Use cache-aside locks or probabilistic TTL for high-traffic keys
- **Fallback Plan**: Serve slightly stale cache on backend failure vs returning 500 error

### Data Validation at Boundaries
- **Input Validation**: Validate ALL public API inputs before database operations
- **Type Safety**: Coerce types explicitly (string→number); don't rely on implicit conversion
- **Domain Rules**: Enforce business logic at application layer, not just database constraints
- **Error Messages**: Return specific, actionable error messages (not database error text)
- **Conflict Handling**: Catch UNIQUE violations separately; handle as ConflictError not 500

---

## Pitfalls to Avoid

1. **N+1 Queries** - Querying related entities in loops; kills performance with 100+ queries
2. **Over-fetching** - Selecting `*` when only 2 columns needed; wastes bandwidth and time
3. **Missing Indexes** - Queries on unindexed columns cause full table scans on production data
4. **Lazy Loading** - Accessing relationships outside transaction scope causes errors
5. **No Cache Invalidation** - Updates don't clear cache; old data served indefinitely
6. **Long Transactions** - Transactions > 5 seconds block other writers and cause deadlocks
7. **Silent Validation Failures** - No error returned when invalid data submitted
8. **Cartesian Products** - Joining multiple one-to-many without grouping creates duplicate rows
9. **Type Confusion** - String user IDs compared to integer columns cause silent query failures
10. **Non-Reversible Migrations** - Drop column without backup; can't rollback if needed

---

## Quality Checks

Before committing data layer code, verify:

- [ ] **No N+1 Queries**: Check query logs for repeated queries in loops; use EXPLAIN PLAN
- [ ] **Transactions Correct**: Multi-step operations wrapped; errors trigger rollback
- [ ] **Indexes Present**: WHERE, JOIN, and ORDER BY columns have indexes
- [ ] **Cache Invalidated**: Cache keys deleted on every write operation
- [ ] **Input Validated**: All API inputs checked before database use
- [ ] **Migrations Tested**: Up and down migrations work on production-size dataset
- [ ] **Error Handling**: Database exceptions caught and converted to domain errors
- [ ] **Performance Measured**: Query execution times logged and < 100ms for typical operations
- [ ] **Data Consistency**: Concurrent operations don't create inconsistent state
- [ ] **Documentation**: Complex queries/migrations have comments explaining intent

---

## Key References

**Common Problem Patterns**:
- N+1 detected by: Query logs showing same query repeated per row
- Lock contention: Transaction timeout or deadlock errors on UPDATE heavy operations
- Migration risk: Downtime > 30 seconds during schema changes on production tables
- Cache misses: Response times spike after cache invalidation or expiry
- Validation bypass: Invalid data reaching database due to missing boundary checks

**Recovery Strategies**:
- Add missing index: Non-blocking if using `CONCURRENTLY` keyword
- Fix N+1: Refactor to single query with JOIN + GROUP BY or separate batch query
- Migrate safely: Test on clone; schedule for low-traffic window; have rollback plan
- Cache stampede: Implement probabilistic TTL or cache-aside lock pattern
- Validation gap: Add check at API boundary; catch specific error codes from DB
