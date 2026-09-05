---
name: launch-commander
description: "Coordinate a complete website launch-readiness review across deployment, public access, SEO, privacy, security, accessibility, content, AdSense, and post-launch monitoring."
---

# Launch commander

This is a read-only launch gate by default. Do not deploy, publish CMP settings, change DNS, edit code, send external messages, or rollback unless the user explicitly authorizes that action.

Use the existing specialized skills when available: `website-pre-launch-audit`, `adsense-readiness-audit`, `production-deploy-verifier`, `seo-indexing-audit`, `privacy-cmp-audit`, `security-launch-gate`, `mobile-accessibility-audit`, `content-trust-audit`, and `post-launch-monitor`. Do not duplicate their work; combine their evidence.

## Order

1. **Scope and release identity** — target URL/environment, intended commit, launch date, supported countries/languages, user roles, ads/CMP status, and authorized test accounts.
2. **Deployment** — verify the intended revision is live and passes safe smoke tests.
3. **Public access** — verify public routes work without login while play, submissions, profile changes, payments, admin, and other mutations remain protected. For apps, confirm read-only public pages cannot mutate state.
4. **Content/trust** — check useful original content, navigation, trust/legal links, UGC moderation, placeholders, broken routes, and deceptive behavior.
5. **SEO/crawlers** — check metadata, canonical, sitemap, robots, rendering, noindex, and no crawler-only content.
6. **Privacy/CMP** — test no-choice, accept, reject, manage, revoke, regional gating, and ad/analytics request timing.
7. **Security** — check authz, API boundaries, secrets, headers, CORS/CSP, rate limits, data exposure, and recovery evidence.
8. **Mobile/accessibility** — test critical routes at supported widths, keyboard/focus, labels, contrast, touch, dialogs, and dynamic states.
9. **AdSense** — check eligibility/content/policy, public crawler access, correct account/domain, code/meta, `ads.txt`, robots, consent, and traffic safety. Use the dedicated skill’s official Google sources.
10. **Decision and follow-up** — produce the launch verdict and a post-launch monitoring schedule. Do not request review or deploy as a side effect of the audit.

## Gates

- `NO-GO`: any critical deployment, public-access, security, consent, policy, or data-protection blocker; wrong revision; or missing evidence that prevents a trustworthy release decision.
- `CONDITIONAL`: no known blocker, but material `HIGH` findings or unverified dashboard/runtime evidence remain.
- `GO`: no known blocker and required evidence is present. This is a launch recommendation, not a guarantee of uptime, indexing, AdSense approval, or legal compliance.

## Required report

Return a one-line verdict, release identity, scorecard by area, blocker list ordered by dependency, exact owner actions, evidence links/files, checks not run, deployment decision, AdSense/dashboard actions, and post-launch monitor plan. Keep user actions separate from developer actions and never include secrets.
