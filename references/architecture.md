# Architecture Practices

## 1.1 Structure by business components
- Organize into self-contained modules by domain (bounded contexts)
- Each component owns its API, logic, and data layer
- Anti-pattern: monolithic folders grouped by technical role (controllers/, models/, services/)

## 1.2 Three-tier layering
- Entry-points (controllers) → Domain logic (services) → Data-access (repositories)
- Web objects (req/res) must NOT leak into business logic
- Anti-pattern: passing Express `req` object into service functions

## 1.3 Wrap utilities as packages
- Shared code in dedicated folders with own `package.json`
- Use explicit `exports` or `main` field for public interface
- Anti-pattern: importing deep internal paths from utility modules

## 1.4 Environment-aware, secure config
- Read from both files and environment variables
- Secrets excluded from committed code
- Use hierarchical config with validation (convict, env-var, zod)
- Anti-pattern: hardcoded config values, committed .env files

## 1.5 Framework choice consequences
- Nest.js: large OOP apps. Fastify: microservices. Express: simple APIs
- Evaluate long-term implications before choosing

## 1.6 TypeScript usage
- Types catch ~20% of bugs; testing still needed for the other 80%
- Avoid over-engineering with advanced TS features unless genuinely needed
