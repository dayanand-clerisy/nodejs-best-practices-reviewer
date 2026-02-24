# Testing and Quality Practices

## 4.1 Write API/component tests at minimum
- Higher coverage than unit tests, easier to write
- Foundation before advancing to unit and performance testing

## 4.2 Three-part test names
- Format: `[unit] [scenario] [expected result]`
- Example: `ProductService.addProduct when price is negative should reject with error`
- Anti-pattern: `test('should work')`, `test('addProduct test')`

## 4.3 AAA pattern
- Arrange → Act → Assert (clearly separated)
- Anti-pattern: interleaving setup and assertions

## 4.4 Unified Node version
- Use `.nvmrc`, `.node-version`, or Volta
- Enforce across dev, CI, and production

## 4.5 No global test fixtures
- Each test manages its own data
- Anti-pattern: shared seed data that creates test coupling

## 4.6 Tag tests
- Use tags: `#cold`, `#api`, `#sanity` for selective execution
- Enables smoke vs full test suite runs

## 4.7 Coverage to detect gaps
- Use Istanbul/NYC; fail builds below thresholds
- Focus: untested error paths and catch clauses

## 4.8 Production-like test environments
- Use docker-compose for consistency
- Anti-pattern: testing against SQLite when production uses PostgreSQL

## 4.9 Static analysis in CI
- Sonarqube, Code Climate for duplications and complexity

## 4.10 Mock external HTTP services
- Use nock or Mock-Server to isolate tests
- Test error paths, timeouts, and slow responses
- Anti-pattern: tests that call real external APIs

## 4.11 Test middlewares in isolation
- Stub `req`, `res`, `next` objects
- Middleware bugs affect all requests

## 4.12 Randomize ports in testing
- Use port 0 for auto-assignment
- Anti-pattern: hardcoded test ports causing conflicts

## 4.13 Test five possible outcomes
1. Response (HTTP status, body)
2. State change (DB writes)
3. External API calls (outgoing requests)
4. Queue messages (events published)
5. Observability (logs emitted)
- Anti-pattern: only asserting on the response
