---
name: website-pre-launch-audit
description: Audit a web application before production launch. Use when asked whether a website is ready to launch, to perform a pre-launch review, security audit, production-readiness check, release gate, go/no-go assessment, or launch checklist. Inspect the repository and deployed environment when available; run relevant tests and scanners; identify launch blockers across security, authentication, payments, privacy, reliability, performance, accessibility, SEO, monitoring, backups, and abuse prevention. Do not use for a narrow code review unless the user asks for overall launch readiness.
---

# Website Pre-Launch Audit

Perform a strict, evidence-based production-readiness audit. Do not declare a product secure or ready merely because the build passes. Treat missing evidence as unverified, not passed.

## Core rules

- Inspect before recommending.
- Prefer repository evidence, configuration, test output, deployment settings, and live HTTP responses over assumptions.
- Never print secrets, tokens, private keys, complete environment files, personal data, or sensitive database contents.
- Do not run destructive tests against production.
- Do not perform denial-of-service, credential stuffing, broad fuzzing, spam, or data-changing attacks.
- Ask before making changes that affect production data, infrastructure, billing, DNS, authentication, access control, or external services.
- Safe local fixes may be implemented when the user requested fixes. Keep changes small and test them.
- A passing automated scanner is not proof of security.
- Separate confirmed findings from suspected risks and unverified controls.

## Required audit inputs

Use what is available. Do not block the audit because some inputs are missing.

Collect or infer:

- repository root and application structure
- frontend, backend, database, authentication, hosting, storage, email, analytics, payment, and third-party services
- production and staging URLs, if available
- launch scope and important user journeys
- whether real users, payments, minors, sensitive data, file uploads, public APIs, or user-generated content are involved

Record unavailable inputs under `Coverage gaps`.

## Workflow

### 1. Establish scope and architecture

Inspect the repository and summarize:

- frameworks, languages, package managers, runtime versions
- deployment platform and environment configuration
- trust boundaries and data flows
- authentication and authorization model
- database access model and migrations
- payment and entitlement flow
- external integrations, webhooks, background jobs, cron tasks, queues, and storage
- public, authenticated, admin, and internal endpoints

Identify the highest-risk flows before running generic checks.

### 2. Run baseline engineering checks

Run only commands appropriate to the detected stack. Reuse project scripts where possible.

Typical checks:

- dependency installation using the committed lockfile
- formatting or format check
- linting
- type checking
- unit tests
- integration tests
- end-to-end tests
- production build
- database migration validation
- dependency vulnerability audit
- secret scanning
- static analysis or security linting

Examples, only when applicable:

- JavaScript/TypeScript: `npm ci`, `npm run lint`, `npm run typecheck`, `npm test`, `npm run build`, `npm audit`
- Python: locked dependency install, `ruff`, `mypy`, `pytest`, `pip-audit`, `bandit`
- Ruby: `bundle exec rubocop`, tests, `bundle audit`, `brakeman`
- PHP: Composer audit, PHPStan/Psalm, tests
- Go: `go test ./...`, `go vet ./...`, `govulncheck ./...`
- Rust: `cargo test`, `cargo clippy`, `cargo audit`

Do not invent successful results. Record commands, exit status, and meaningful failures.

### 3. Review security controls

Use `references/audit-checklist.md`. Prioritize exploitable paths over cosmetic hardening.

At minimum inspect:

- exposed secrets and unsafe environment handling
- authentication, session management, password reset, email verification, MFA where appropriate
- authorization on every sensitive server-side action and object
- database row-level security or equivalent access controls
- input validation and output encoding
- SQL/NoSQL injection, XSS, CSRF, SSRF, command injection, path traversal, open redirects
- file upload restrictions and storage permissions
- CORS, CSP, HSTS, framing, MIME sniffing, referrer and permissions policies
- cookie flags and token storage
- rate limiting, bot resistance, abuse controls, enumeration, replay, race conditions
- webhook signature verification and idempotency
- dependency and supply-chain risk
- logging without leaking secrets or personal data
- admin routes, debug endpoints, source maps, internal APIs, and default credentials

For deployed URLs, inspect normal HTTP behavior and security headers. Use non-destructive checks only.

### 4. Review business-critical flows

Trace complete server-side behavior, not only UI states.

For each important flow, verify success, failure, retry, duplicate, cancellation, timeout, and unauthorized cases.

Common flows:

- sign-up, sign-in, sign-out, verification, password reset, account deletion
- role changes and admin actions
- subscriptions, one-time payments, refunds, charge failures, cancellations, grace periods
- entitlement assignment and revocation
- email delivery and bounce/failure handling
- uploads, exports, imports, invitations, sharing, and public links
- multiplayer, rankings, rewards, virtual goods, coupons, or other abuse-prone mechanics

Payments must be authoritative on the server. Never trust client-provided price, product, role, entitlement, score, or completion state.

### 5. Review production operations

Verify:

- separate development, staging, and production configuration
- HTTPS, domain redirects, DNS, and certificate behavior
- production-safe build flags and disabled debug mode
- environment-variable validation at startup
- database migrations and rollback strategy
- backups and a credible restore procedure
- error tracking, structured logs, uptime monitoring, and alert ownership
- health checks and graceful failure behavior
- resource limits, timeouts, retries, connection pooling, and queue handling
- cron/background job observability and duplicate-execution safety
- incident response and rollback path
- least-privilege service credentials and access

A backup is not considered verified unless restoration has been tested or there is credible evidence of a restore test.

### 6. Review privacy and legal launch requirements

Do not give definitive legal advice. Flag likely requirements based on actual product behavior and jurisdiction.

Check:

- privacy notice matches collected and shared data
- terms or acceptable-use rules where needed
- cookie/analytics consent behavior where applicable
- data retention and deletion
- account deletion and data export where required
- subprocessors and third-party disclosures
- age restrictions and parental-consent implications
- support, company, billing, refund, and contact information
- marketing email consent and unsubscribe handling

Mark jurisdiction-dependent items as requiring legal confirmation.

### 7. Review user experience, accessibility, SEO, and performance

Inspect core pages and journeys across mobile and desktop.

Check:

- broken routes, links, assets, and forms
- loading, empty, success, error, offline, expired-session, and permission-denied states
- keyboard navigation, focus visibility, labels, semantic HTML, contrast, reduced motion, and screen-reader basics
- titles, descriptions, canonical URLs, robots directives, sitemap, social metadata, and structured data where relevant
- image optimization, caching, compression, bundle size, rendering, and Core Web Vitals indicators
- browser compatibility appropriate to the audience

Accessibility, SEO, and performance issues are launch blockers only when they materially break access, discoverability, legal obligations, or core usage.

### 8. Validate findings

For each finding:

- cite the file and line, command output, configuration, endpoint behavior, or reproducible steps
- explain the realistic impact
- distinguish exploitability from theoretical weakness
- avoid duplicate findings with the same root cause
- provide a concrete remediation and a verification test

When a suspected issue cannot be confirmed, label it `Needs verification` rather than reporting it as fact.

### 9. Assign severity

Use these levels consistently:

- `BLOCKER`: credible risk of unauthorized access, data loss, secret exposure, payment/entitlement failure, legal inability to launch, broken core journey, unrecoverable deployment, or trivial severe abuse. Launch must stop.
- `HIGH`: serious security, integrity, reliability, privacy, or revenue risk that is likely or has substantial impact. Fix before public launch unless explicitly accepted by the accountable owner.
- `MEDIUM`: meaningful weakness with limited likelihood, impact, or workaround. Schedule promptly.
- `LOW`: hardening, maintainability, minor UX, or limited-impact issue.
- `INFO`: observation, improvement, or verified control.

Do not dilute severity to make the report look better.

### 10. Determine launch verdict

Use exactly one verdict:

- `NO-GO`: one or more unresolved blockers, or critical areas are too unverified to make launch responsible.
- `CONDITIONAL GO`: no blockers, but high-severity findings or material coverage gaps require explicit acceptance and a dated remediation plan.
- `GO`: no blockers or high findings, core flows are tested, and operational recovery controls are evidenced.

A `GO` verdict means reasonable readiness based on examined evidence. It is not a guarantee of security.

## Fix mode

When asked to fix findings:

1. Fix blockers first, then high-severity issues.
2. Preserve existing architecture unless it is the root cause.
3. Add regression tests for each fixed security or business-logic issue when feasible.
4. Run the narrowest relevant tests after each change, then the full applicable validation suite.
5. Do not silently change public behavior, billing, permissions, schema, or deployment configuration.
6. Re-audit affected flows and update the verdict.

## Required output

Use `references/report-template.md` as the structure.

The report must include:

- verdict and concise justification
- audited scope and coverage gaps
- architecture and attack-surface summary
- command/test results
- findings grouped by severity
- launch-blocking checklist
- prioritized remediation plan
- verified controls
- residual risks and explicit assumptions
- exact next actions

Keep the executive summary short. Put evidence and technical detail in findings.
