---
name: seo-indexing-audit
description: "Audit public-site crawlability and search indexing signals including metadata, canonical URLs, sitemap, robots rules, noindex directives, rendering, and route discoverability before launch."
---

# SEO indexing audit

Run read-only checks by default. Do not submit URLs, change indexing settings, edit code, or alter `robots.txt` unless explicitly requested.

Use [Google Search Essentials](https://developers.google.com/search/docs/essentials), [Google crawling and indexing guidance](https://developers.google.com/search/docs/crawling-indexing), and [Google Search spam policies](https://developers.google.com/search/docs/essentials/spam-policies) for normative Google claims. Do not invent ranking requirements or promise indexing.

## Workflow

1. Define the canonical domain, protocol/host variant, launch environment, primary languages, important public routes, intentionally private routes, and whether the site is an SPA or server-rendered.
2. Build a route inventory from navigation, sitemap, route configuration, footer links, and direct known URLs. Test in a clean logged-out browser. A route that only shows “log in” is not useful public content unless that is intentional.
3. Inspect each important public page:
   - meaningful, accurate `<title>` and meta description;
   - one clear page purpose and useful visible content;
   - canonical URL resolving to the intended HTTPS host;
   - correct language/locale and viewport metadata;
   - no accidental `noindex`, `nofollow`, `nosnippet`, or `X-Robots-Tag`;
   - crawlable internal links with descriptive text;
   - truthful structured data only where appropriate.
4. Check `/robots.txt` at the correct host. Confirm it does not block important public pages or assets, and do not treat it as an access-control mechanism. Check that a `noindex` directive is not hidden behind a robots block.
5. Check `/sitemap.xml`: HTTP success, valid XML, canonical URLs only, no login/error/prelaunch URLs, accurate last-modified values, and a robots reference where applicable. A sitemap helps discovery but does not guarantee crawling or indexing.
6. Verify rendering. After JavaScript executes, the page must still expose the intended text, links, headings, and controls to users and crawlers. Check loading/error states and API failures; do not use crawler-specific content.
7. Compare normal browser delivery with safe Googlebot-style HTTP requests when appropriate. Flag user-agent variation, redirects to login, WAF blocks, rate-limit failures, cookie-only content, and inconsistent canonical/robots behavior.
8. Check Search Console evidence only when the user provides access or screenshots: domain/property verification, URL Inspection, indexing coverage, manual actions, security issues, and sitemap status.

## Report

Use `PASS`, `FAIL`, `NEEDS VERIFICATION`, or `NOT APPLICABLE`. Include URL/file evidence, Google source, impact, and action. Separate:

- technical crawl blockers;
- intentional exclusions that are working;
- Google recommendations;
- ordinary SEO improvements that are not AdSense requirements.

Verdict: `NO-GO` for inaccessible canonical public content, accidental site-wide noindex/robots blocking, cloaking, or a broken canonical/sitemap foundation; `CONDITIONAL` when dashboard/runtime evidence is missing; `READY` when no known blocker remains. Say explicitly that Google may still choose not to crawl or index a compliant page.
