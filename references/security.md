# Security Practices

## 6.1 Linter security rules
- Use `eslint-plugin-security` to detect eval, dynamic require, child_process risks

## 6.2 Rate limiting
- Use `rate-limiter-flexible`, `express-rate-limit`, or cloud LB rules
- Anti-pattern: no rate limiting on public endpoints

## 6.3 Secrets management
- Use Vault, K8s Secrets, or env vars — never commit secrets
- Pre-commit hooks to prevent exposure
- Anti-pattern: secrets in config files, hardcoded API keys

## 6.4 ORM/ODM for query safety
- Use parameterized queries via Sequelize, Knex, Mongoose
- Anti-pattern: string interpolation in SQL/NoSQL queries

## 6.5 Generic security principles
- Apply OWASP Top 10 universally

## 6.6 Security headers (Helmet.js)
- Prevent XSS, clickjacking, MIME sniffing
- Anti-pattern: default Express headers exposing tech stack

## 6.7 Dependency vulnerability scanning
- `npm audit` and Snyk in CI/CD

## 6.8 Password hashing (bcrypt/scrypt)
- Hash with salt; avoid pbkdf2 unless required
- Anti-pattern: storing plaintext or MD5/SHA hashed passwords

## 6.9 Escape HTML/JS/CSS output
- Use dedicated escaping libraries
- Anti-pattern: rendering raw user input in templates

## 6.10 Validate incoming JSON schemas
- Use ajv, Zod, or Typebox at API boundaries
- Anti-pattern: trusting request body shape without validation

## 6.11 JWT blocklisting
- Maintain revoked token list; check on each request
- Anti-pattern: no way to invalidate issued JWTs

## 6.12 Brute-force protection
- Track and block excessive failed auth attempts per user/IP

## 6.13 Run as non-root
- Create dedicated users; apply in Docker images
- Anti-pattern: running Node process as root

## 6.14 Limit payload size
- Configure at edge (firewall/ELB) and app level (body-parser)
- Anti-pattern: accepting unlimited request body sizes

## 6.15 No eval()
- Never use `eval`, `new Function()`, or dynamic code in `setTimeout`/`setInterval`

## 6.16 Safe regex
- Use `safe-regex` or `validator.js` over custom patterns
- Anti-pattern: complex regex causing ReDoS (event loop blocking)

## 6.17 No dynamic module loading from user input
- Never use user-supplied paths in `require`/`import`

## 6.18 Sandbox unsafe code
- Use `cluster.fork()`, serverless, or sandbox packages

## 6.19 Child process safety
- Prefer `execFile` over `exec` (no shell expansion)
- Validate and sanitize all input

## 6.20 Hide error details from clients
- Never expose stack traces, file paths, or internal module names
- Anti-pattern: sending full Error objects in HTTP responses

## 6.21 2FA for npm
- Prevents credential compromise and supply chain attacks

## 6.22 Secure session middleware
- Hide tech stack, secure cookies, remove `X-Powered-By`

## 6.23 Controlled crash behavior
- Wrap routes with error handlers; validate input to prevent crash triggers
- Consider not crashing on request-scoped errors

## 6.24 Prevent unsafe redirects
- Validate all user-supplied redirect URLs

## 6.25 Avoid publishing secrets to npm
- Use `.npmignore` or `files` allowlist in `package.json`

## 6.26 Check outdated packages
- `npm outdated` or `npm-check-updates` in CI

## 6.27 Use 'node:' protocol for built-ins
- `import { createServer } from "node:http"` — removes ambiguity
- Enforce with eslint-plugin-unicorn
- Anti-pattern: `require('http')` without `node:` prefix
