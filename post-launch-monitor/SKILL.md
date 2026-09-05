---
name: post-launch-monitor
description: "Run safe post-deployment checks for uptime, public routes, crawler files, critical read-only flows, errors, and meaningful production regressions after launch."
---

# Post-launch monitor

Monitoring is read-only by default. Do not auto-rollback, restart services, modify data, or change production configuration unless the user explicitly authorizes it. For recurring monitoring, use the product’s recurring monitor/heartbeat mechanism rather than an unapproved background loop.

## Check cadence

Run a baseline immediately after deployment, then repeat at a sensible interval such as 15 minutes, 1 hour, 24 hours, and 7 days when requested. Stay quiet while state is unchanged; report only meaningful failure, recovery, completion, or required user action.

## Checks

1. Confirm the live deployment revision and alias did not unexpectedly change.
2. Check HTTPS, DNS/redirects, homepage, critical public routes, `robots.txt`, `sitemap.xml`, and `/ads.txt`.
3. Test logged-out public routes and read-only flows. Verify protected mutations remain protected. Do not submit gameplay, forms, payments, or account changes.
4. Check health endpoints, error rates, frontend console/runtime errors, failed assets/API calls, latency, and obvious blank/error screens.
5. Check authentication/session health with authorized test accounts only when provided. Never print cookies, tokens, or personal data.
6. Check monitoring dashboards, incident logs, and deployment status. Compare with the previous baseline instead of treating one slow request as a failure without context.
7. If ads are live, verify presence and consent gating only; never click ads or generate traffic.

## Alert levels

- `CRITICAL`: site unavailable, wrong deployment, data exposure, auth bypass, payment/security failure.
- `HIGH`: critical public route broken, crawler file failure, widespread client/API errors, consent failure.
- `MEDIUM`: material regression or degraded performance with workaround.
- `INFO`: recovery, expected change, or observation.

## Report

Return timestamp, deployment revision, checks, baseline comparison, severity, evidence, user impact, and recommended next action. Ask before rollback or other mutation. Monitoring does not replace a full launch audit.
