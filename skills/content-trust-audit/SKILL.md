---
name: content-trust-audit
description: "Audit public content quality, trust pages, broken routes, placeholders, user-facing claims, ownership signals, and user-generated content before launch."
---

# Content and trust audit

Use read-only inspection by default. Do not invent claims, publish legal text, remove user content, or change copy without explicit authorization.

For AdSense/Search-related findings, use [Google site-readiness guidance](https://support.google.com/adsense/answer/7299563?hl=en), [AdSense policies](https://support.google.com/adsense/answer/48182?hl=en), and [Google Search spam policies](https://developers.google.com/search/docs/essentials/spam-policies). Clearly label practical trust advice as a recommendation, not a Google requirement.

## Workflow

1. Inventory public routes from navigation, sitemap, footer, and direct links. Visit them logged out and from a clean browser. Include homepage, product/app pages, rules/help, about, contact, pricing, privacy, terms, profiles/leaderboards, error pages, and any public UGC.
2. Assess whether each page has a clear purpose, complete copy, useful original contribution, readable rendering, working links, accurate claims, and a next step. Flag “coming soon”, placeholder, empty, duplicate, broken, or login-only pages that are presented as public content.
3. Check trust signals: identifiable operator, contact method, privacy/terms links, product explanation, pricing/payment disclosures, support path, language consistency, copyright/attribution, and claims that match the actual product. These are practical quality checks, not automatic approval requirements.
4. Check content integrity: scraped/copied material, uncredited images/text, misleading titles, keyword stuffing, fake functionality, broken promises, auto-generated low-value pages, and third-party content without meaningful publisher contribution.
5. For UGC, inspect sample content and verify moderation, report, block, edit/remove, rate limiting, abuse escalation, and ad-bearing-page controls. The site owner remains responsible for content around ads.
6. Test navigation and failure paths: internal links, footer, back button, 404/500, empty states, API failure, expired session, and mobile. Ensure users are not redirected to irrelevant or deceptive destinations.

## Report

Return a route/content table, strongest trust gaps, policy/content risks, exact owner actions, and verdict. Use `NO-GO` for deceptive functionality, widespread empty/broken public content, unmoderated high-risk UGC, serious copyright concerns, or critical trust/legal information missing from a site that relies on it. Do not use a word-count threshold or claim that a specific page list guarantees approval.
