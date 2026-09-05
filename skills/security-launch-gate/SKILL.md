---
name: security-launch-gate
description: "Run a focused, authorized pre-launch security gate for authentication, authorization, secrets, browser protections, API exposure, and abuse controls."
---

# Security launch gate

Use only on systems the user owns or explicitly authorizes. Default to read-only review and safe validation. Do not exploit, delete data, bypass authentication, brute-force, scan unrelated hosts, or change production controls without explicit authorization.

Use [OWASP ASVS](https://owasp.org/www-project-application-security-verification-standard/) and the [OWASP Top 10](https://owasp.org/Top10/) as review frameworks, not as proof of certification. A code review is not a penetration test.

## Workflow

1. Define scope: production/staging host, repositories, APIs, admin surfaces, test accounts, data classes, allowed tools, and stop conditions. Confirm whether testing is passive, authenticated, or active.
2. Inspect authentication boundaries:
   - public pages are intentionally public;
   - protected routes cannot be opened by direct URL without authorization;
   - logout/session expiry/revocation behave correctly;
   - reset, email verification, OAuth callbacks, and cookies have safe boundaries;
   - public leaderboard/profile data does not expose private fields.
3. Inspect authorization at the API/resource level, not only the UI. Test safe deny cases with owned test data for IDOR/BOLA, role changes, tenant boundaries, admin endpoints, and state-changing methods. Never use another user’s data without authorization.
4. Search configuration and build output for exposed secrets, private keys, tokens, debug flags, source maps containing sensitive values, unsafe defaults, and accidental test accounts. Redact findings; never print secret values.
5. Review browser/server protections: HTTPS, secure cookie attributes, CSRF protection where relevant, CORS allowlists, CSP/security headers, clickjacking protection, MIME handling, cache rules, error leakage, dependency warnings, and upload/download handling.
6. Review abuse controls: rate limits, brute-force protection, spam/UGC controls, bot protection, payment/webhook verification, replay resistance, audit logging, and safe failure behavior.
7. Run focused checks only: tests, typecheck/build, dependency audit where available, route/API authorization tests, and passive HTTP/header checks. Record tool versions and limits.

## Severity and report

- `BLOCKER`: exposed secret, auth bypass, unauthorized data/action, exploitable production path, or missing control around critical data.
- `HIGH`: likely exploitable weakness or missing boundary with material impact.
- `MEDIUM/LOW`: hardening or defense-in-depth gap.
- `NEEDS VERIFICATION`: evidence unavailable.

Return scope, verdict (`NO-GO`, `CONDITIONAL`, or `GO`), finding, evidence, impact, affected route/file, safe remediation direction, and validation status. Do not implement fixes unless separately requested.
