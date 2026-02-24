# Code Patterns and Style Practices

## 3.1 Use ESLint
- De-facto standard for detecting anti-patterns
- Pair with Prettier for formatting

## 3.2 Node.js ESLint plugins
- `eslint-plugin-node`, `eslint-plugin-security`, `eslint-plugin-mocha`
- Catches Node-specific issues (dynamic require, etc.)

## 3.3 Opening braces on same line
- Prevents ASI-related bugs
- Anti-pattern: opening brace on new line (K&R vs Allman in JS context)

## 3.4 Separate statements properly
- Use semicolons or rely on ESLint/Prettier to enforce consistency

## 3.5 Name your functions
- Avoid anonymous functions for callbacks and closures
- Named functions improve profiling and memory snapshots
- Anti-pattern: `arr.map(function(item) { ... })` or `arr.map((item) => { ... })` for complex logic

## 3.6 Naming conventions
- Variables/functions: `lowerCamelCase`
- Classes: `UpperCamelCase`
- Constants: `UPPER_SNAKE_CASE`

## 3.7 Prefer const over let; ditch var
- `const` prevents reassignment; `let` for block scope
- Anti-pattern: using `var` anywhere

## 3.8 Require/import modules at file top
- Not inside functions (blocks event loop with sync require)
- Anti-pattern: lazy require inside request handlers

## 3.9 Explicit module entry points
- Use `package.json` `exports`/`main` or `index.js`
- Prevents consumers importing internal files

## 3.10 Use strict equality (===)
- No type coercion
- Anti-pattern: `==` comparisons

## 3.11 Async-Await over callbacks
- Cleaner flow, try-catch support

## 3.12 Arrow functions
- Preserves lexical `this`, more compact

## 3.13 Avoid side effects outside functions
- Code at module top-level executes on import
- Use factory functions or init patterns
- Anti-pattern: DB connections or API calls at module scope
