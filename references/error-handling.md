# Error Handling Practices

## 2.1 Async-Await for async error handling
- Use async/await with try-catch instead of callbacks
- Anti-pattern: callback pyramids, unhandled promise chains

## 2.2 Extend built-in Error object
- Custom error classes extending Error with `code`, `isCatastrophic`, `httpStatus`
- Enforce with `no-throw-literal` ESLint rule
- Anti-pattern: `throw "error string"`, `throw { message: "..." }`

## 2.3 Distinguish catastrophic vs operational errors
- Operational: invalid input, API timeout → handle gracefully
- Catastrophic: undefined variable, failed assertion → restart process
- Anti-pattern: treating all errors the same way

## 2.4 Centralized error handler
- Single error handler for logging, crash decisions, metrics
- All entry-points (APIs, cron, queues) route errors here
- Anti-pattern: error handling duplicated in every middleware/route

## 2.5 Document API errors with OpenAPI
- Publish expected error responses for consumers
- Anti-pattern: undocumented error shapes that vary by endpoint

## 2.6 Graceful exit on catastrophic errors
- Close connections, flush logs, then exit
- Let orchestrator (Docker/K8s) handle restart
- Anti-pattern: swallowing fatal errors to keep process alive

## 2.7 Use mature logger (Pino/Winston)
- Structured logging with levels, not `console.log`
- Log to stdout; infrastructure handles routing
- Anti-pattern: `console.log` scattered through codebase

## 2.8 Test error flows
- Verify correct error types and messages for failure cases
- Test centralized error handler behavior

## 2.9 APM for error discovery
- Proactive monitoring without manual instrumentation

## 2.10 Catch unhandled promise rejections
- Subscribe to `process.unhandledRejection`
- Anti-pattern: missing global rejection handler

## 2.11 Validate arguments early (fail fast)
- Use ajv, zod, or typebox at function boundaries
- Anti-pattern: discovering bad input deep in business logic

## 2.12 Always await before returning
- `return await fn()` not `return fn()` — preserves full stack trace
- Anti-pattern: `return promise` losing caller context in traces

## 2.13 Subscribe to emitter/stream 'error' events
- try-catch does NOT capture EventEmitter errors
- Use `{ captureRejections: true }` for async handlers
- Anti-pattern: unhandled 'error' events crashing the process silently
