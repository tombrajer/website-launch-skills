---
name: production-deploy-verifier
description: "Verify that the intended website revision is actually deployed to the intended production environment and passes safe live smoke tests before launch or release."
---

# Production deploy verifier

Use read-only verification by default. Do not deploy, promote, rollback, edit environment variables, migrate data, or change DNS unless the user explicitly authorizes that exact action.

## Outcome

Prove that the intended revision is live, the important public routes work, protected actions remain protected, and launch-critical files/configuration are present. A local build, a deployment-created message, or a green CI run is not proof that production behaves correctly.

## Workflow

1. Establish the target: production URL, deployment provider, expected branch/commit/tag, intended environment, critical routes, and allowed test accounts. If the target revision or URL is unclear, mark it `NEEDS VERIFICATION`.
2. Inspect repository state and deployment metadata. Record the current branch, commit, dirty files, build version, deployment ID/URL, alias, status, and timestamp. Preserve unrelated work and never expose secrets.
3. Confirm revision identity. Compare the live build marker, deployment metadata, or response asset fingerprint with the intended commit. Do not accept “latest” without resolving it to a revision.
4. Check the live transport: HTTPS, certificate, host redirects, redirect loops, DNS resolution, response status, cache behavior, and obvious server errors.
5. Run safe smoke tests in a clean logged-out browser and direct HTTP checks:
   - homepage and key public routes return expected status/content;
   - direct URLs do not unexpectedly require login;
   - protected pages and APIs still reject unauthenticated access;
   - forms, buttons, and read-only views do not show obvious runtime errors;
   - `robots.txt`, `sitemap.xml`, `ads.txt`, canonical, and required public assets load;
   - no console/runtime error blocks the primary experience.
6. If the provider is Vercel, verify the deployment is `Ready`, the production alias points to that deployment, and the inspected deployment matches the intended commit. Do not infer live success from `vercel build` or a preview URL.
7. Check monitoring, error tracking, logs, and rollback information without changing them. Verify that a human can identify the previous known-good deployment.

## Guardrails

- Use only authorized URLs and test accounts. Do not guess credentials or bypass access controls.
- Use idempotent or read-only checks. Do not submit gameplay, payments, account changes, or production forms.
- Never run ad clicks, synthetic traffic, load tests, or destructive probes in production.
- If live and intended revision differ, report the mismatch. Do not silently redeploy.

## Report

Return:

- verdict: `GO`, `CONDITIONAL`, or `NO-GO`;
- intended revision versus verified live revision;
- deployment/provider evidence;
- route smoke-test table with URL, status, expected result, observed result;
- auth boundary results;
- infrastructure/configuration warnings;
- checks not run and why;
- exact next action.

Use `NO-GO` for a wrong revision, unavailable production, broken critical route, exposed protected action, or missing evidence for a launch-critical check. State that this verifies the deployment, not every future runtime condition.
