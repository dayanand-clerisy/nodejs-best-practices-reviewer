# Production Practices

## 5.1 Monitoring (4 layers)
- Uptime, user-facing metrics, Node.js metrics (event loop lag), distributed tracing
- Use OpenTelemetry for flow measurement

## 5.2 Smart logging
- Plan log infrastructure from day one
- Design for collection, storage, analysis, and dashboards

## 5.3 Reverse proxy for CPU tasks
- Offload gzip, SSL to nginx/HAproxy/cloud LB
- Anti-pattern: Node handling SSL termination or static file compression

## 5.4 Lock dependencies
- Commit `package-lock.json`
- Anti-pattern: `.gitignore`-ing the lockfile

## 5.5 Process uptime via platform
- Docker/K8s: platform handles restart
- Bare metal: use systemd
- Anti-pattern: pm2 inside containers

## 5.6 Utilize all CPU cores
- Use platform-level replication (K8s replicas, cluster module)

## 5.7 Maintenance endpoint
- Expose memory/diagnostics via secured API
- Reduces diagnostic deploys

## 5.8 APM for unknowns
- Identifies slow transactions and bottlenecks automatically

## 5.9 Production-ready from start
- Consider deployment, monitoring, debugging during initial design

## 5.10 Monitor memory usage
- V8 ~1.4GB soft limit; watch for leaks
- Embed in observability systems

## 5.11 Serve static assets elsewhere
- Use nginx, S3, or CDN (except for SSR)
- Anti-pattern: Express serving static files in production

## 5.12 Be stateless
- Store sessions, caches, uploads externally
- Enables horizontal scaling

## 5.13 Automated vulnerability scanning
- `npm audit`, Snyk in CI/CD
- Anti-pattern: manual, infrequent dependency audits

## 5.14 Transaction/correlation IDs
- UUID per request via `AsyncLocalStorage`
- Essential for distributed tracing

## 5.15 NODE_ENV=production
- Enables package optimizations
- Anti-pattern: running production without this set

## 5.16 Automated zero-downtime deployments
- Docker + CI for atomic deploys
- Anti-pattern: manual SSH-and-restart deploys

## 5.17 Use LTS Node.js
- Security updates, module compatibility

## 5.18 Log to stdout
- Let infrastructure route to aggregators
- Anti-pattern: writing log files from app code

## 5.19 Use npm ci
- Strictly enforces lockfile; fails on mismatch
- Anti-pattern: `npm install` in CI/CD
