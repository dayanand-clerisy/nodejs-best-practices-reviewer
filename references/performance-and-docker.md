# Performance Practices

## 7.1 Don't block the event loop
- Move CPU-intensive work to worker threads or background processes
- Monitor event loop lag
- Anti-pattern: synchronous file I/O, heavy computation in request handlers

## 7.2 Prefer native JS over Lodash
- Modern JS has robust array/object/string methods
- Anti-pattern: importing Lodash for `_.map`, `_.filter`, `_.get` when native alternatives exist

# Docker Practices

## 8.1 Multi-stage builds
- Separate build deps from runtime; reduces image size and attack surface

## 8.2 Use `node` command, not `npm start`
- Bypasses npm overhead; simpler signal handling

## 8.3 Let Docker/K8s handle replication
- Anti-pattern: pm2 cluster mode inside containers

## 8.4 .dockerignore for secrets
- Exclude .env, keys, credentials from build context

## 8.5 Prune dev dependencies
- `npm prune --production` or multi-stage build

## 8.6 Graceful shutdown on SIGTERM
- Close server, finish pending ops, flush logs

## 8.7 Memory limits (Docker + V8)
- Align `--max-old-space-size` with container memory limits

## 8.8 Efficient layer caching
- Copy package*.json first, install, then copy source

## 8.9 Pin base image versions
- Anti-pattern: `FROM node:latest`

## 8.10 Use small base images
- Alpine or distroless variants

## 8.11 No secrets in build args
- Use BuildKit secret mounting or multi-stage builds

## 8.12 Scan images for vulnerabilities
- Trivy or Snyk before pushing to registry

## 8.13 Clean npm cache
- `npm cache clean --force` in Dockerfiles

## 8.14 Generic Docker best practices
- Non-root user, health checks, stdout/stderr logging

## 8.15 Lint Dockerfiles
- Use Hadolint for consistency and security
