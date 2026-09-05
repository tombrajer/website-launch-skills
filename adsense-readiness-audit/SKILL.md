---
name: adsense-readiness-audit
description: "Audit a website for current Google AdSense readiness using official Google criteria and recommendations; check public crawler access, content, navigation, policy, privacy/CMP, ads.txt, robots.txt, account setup, and traffic risks, then give an ordered approval plan."
---

# AdSense readiness audit

Audit mode is read-only by default. Do not change code, deploy, create an AdSense account, change DNS, publish a CMP message, or request review unless the user explicitly asks for that action.

The goal is an evidence-backed readiness report, not an approval guarantee. Google makes the final decision and its policies can change. Use only the official Google sources in `references/google-criteria.md` for normative AdSense claims. If a fact is not evidenced, report `NEEDS VERIFICATION`; do not turn SEO folklore into a requirement.

## Hard boundaries

- Never recommend Googlebot-only access, user-agent detection, cloaking, hidden text, or a different page for reviewers. A reviewable public page must be the same experience normal users receive.
- Do not treat `robots.txt` as an authentication bypass. Check that applicable Google crawlers can fetch the normal public page and its required resources.
- Do not expose private data, secrets, `.env` values, tokens, database contents, or authenticated user pages during the audit.
- Do not claim that Google requires a particular word count, traffic volume, number of pages, blog format, Google Analytics, or a specific design. Mark these as non-requirements unless an official Google source says otherwise.
- Separate AdSense readiness from legal compliance. Flag consent/privacy work and link the official Google guidance, but say that the site owner must obtain appropriate legal advice for its jurisdiction.
- Separate publisher policies from publisher restrictions. Restrictions can reduce demand; policy violations can prevent or end serving/account participation.

## Best-chance order

Run the audit and give the user actions in this order. Do not start with ad placement or the application form.

1. **Account and ownership gate**
   - Confirm the owner controls the domain and HTML source, is eligible to contract, uses accurate payee/payment details, selects a supported primary language, and does not already have another AdSense account for the same publisher/payee.
   - If the user wants a second account, stop and explain that Google generally allows one account per publisher. A separate account needs a genuinely separate organization/payee and correct account type/details.

2. **Remove review blockers**
   - Verify the canonical site is live over HTTPS and the useful public pages return `200` without login, prelaunch/coming-soon gates, or a password.
   - Check that normal users, `Mediapartners-Google`, and relevant Google crawlers receive the same public content. If a site is login-protected, Google’s connection guidance says to temporarily remove the login so the crawler can reach it.
   - For an application, expose public, read-only product/content pages (for example rules, help, public leagues, leaderboard, and a non-interactive puzzle preview) while keeping play, submissions, profile changes, messaging, and other mutations authenticated. A public shell that only says “log in” is not useful review content.
   - Never create a crawler exception. If a prelaunch page is temporarily disabled, preserve the code so it can be restored later.

3. **Make the public site worth reviewing**
   - Check each important public URL for original, useful, relevant publisher content; complete copy; readable rendering; working links; clear navigation; and a clear purpose.
   - Flag placeholder, under-construction, empty, thin, broken, duplicated, scraped, copied, or automatically generated pages without meaningful publisher contribution.
   - Check that a visitor can understand who operates the site and what it offers. Treat About, Contact, Help/Rules, and pricing/product information as practical trust checks, not invented Google “required page” claims.
   - Check the primary language against Google’s supported-language list. Do not place Google ad code on primarily unsupported-language content.

4. **Scan all public and future ad-bearing content for policy risk**
   - Review publisher policies, publisher restrictions, ad-placement rules, search spam guidance, intellectual-property concerns, and user-generated content (UGC).
   - Include pages and UGC the owner did not write. The owner is responsible for policy compliance on pages carrying its ad code.
   - For UGC, verify moderation/reporting/removal controls and sample public content. If moderation cannot be evidenced, mark the ad-bearing area `NO-GO` until addressed.

5. **Finish privacy and consent before connecting ads**
   - Verify an accessible privacy policy explains relevant data use, cookies/local storage, advertising, and consent choices in language the site visitors can understand. Do not present a generic template as legal advice.
   - For EEA, UK, or Switzerland traffic, check for a Google-certified CMP or an appropriate consent solution. If serving personalized ads under the IAB TCF, verify the current TCF requirements, Google Purpose 1 consent, consent withdrawal/revocation, and that the ad tag is not called before valid consent where required.
   - Check that the privacy-policy page itself does not load the ad tag or consent scripts that require consent, and that a user can reopen consent choices/revoke consent.
   - Give the exact AdSense UI actions when the user must do them: AdSense → Privacy & messaging → European regulations message → select site → add the privacy-policy URL → choose language/options → publish; then test in a clean/incognito session using Google’s documented test parameters.

6. **Connect the correct AdSense account and domain**
   - Use the standard domain only (for example `example.com`, not a path, query, port, or subdomain unless Google’s flow specifically supports it).
   - Tell the user to add the site in the intended AdSense account, connect using the provided code/meta tag or `ads.txt`, and request review only after steps 1–5 pass.
   - Check the head code/meta tag contains the intended publisher ID, that no old account ID remains, and that the code is not placed on private, policy-risk, or privacy-policy pages.

7. **Verify `ads.txt`, `robots.txt`, sitemap, and delivery**
   - Check `/ads.txt` at the domain root, exact publisher ID, valid syntax, HTTP `200`, no redirect/HTML/error page, and no robots rule blocking the fetch. `ads.txt` is optional but Google calls it highly recommended; it can take time to be discovered.
   - Check `robots.txt` does not block Google’s applicable crawlers or required public assets. Do not infer that `Disallow: /` is harmless.
   - Check canonical URLs, sitemap references, HTTPS, redirect loops, server errors, and that client-rendered content is visible after JavaScript execution.

8. **Protect traffic and ad behavior**
   - Confirm there is no self-clicking, repeated clicking/impressions, click encouragement, incentivized interaction, paid-to-click traffic, bot traffic, or other artificial traffic. Never click live ads during testing.
   - Before ads serve, verify ad placements will not resemble navigation/download controls, interrupt core use, appear in pop-ups, be auto-refreshed, appear on private communication screens, or exceed publisher content. For games, review game-play-specific spacing/placement guidance.

9. **Apply and monitor**
   - Only now request review from AdSense. Tell the user the review can take days and sometimes longer; do not promise a date.
   - After submission, monitor AdSense notifications/Policy Center, crawler issues, `ads.txt` status, and ad-serving limits. A review result is not proof that all future pages or UGC are compliant.

## Audit workflow

### 1. Establish scope

Identify the site URL, repository/worktree if supplied, framework/build commands, deployment host, intended publisher ID (never print secrets), logged-in and logged-out states, target countries/languages, ad product (AdSense for Content, Auto ads, or another Google product), and whether the request is audit-only. Read applicable `AGENTS.md` files and check `git status` before inspecting a repository. Preserve unrelated changes.

If no live URL or no repository is available, say exactly which checks are unavailable. Do not fill gaps with assumptions.

### 2. Inventory routes and access states

Build a route table with:

| Route | Public without login | HTTP result | Useful content | Read-only | Policy risk | Notes |
|---|---:|---:|---:|---:|---:|---|

Test the homepage, canonical landing pages, navigation destinations, rules/help, about/contact, privacy/cookie pages, pricing, public profiles/leaderboards, app/game previews, error pages, and any URL linked in the footer or sitemap. Test logged out in a clean/incognito browser. For interactive apps, verify that public access does not allow play, submission, resource consumption, account mutation, or other protected actions.

### 3. Test crawler-visible delivery

For the public route set, inspect normal HTTP responses and, where safe, Google crawler user agents such as `Mediapartners-Google` and `AdsBot-Google`. Compare status, redirect chain, meaningful body, canonical, robots meta, and required resources. A crawler result must not be better than the normal user result. Check:

- `https://site.example/robots.txt`
- `https://site.example/sitemap.xml`
- `https://site.example/ads.txt`
- canonical URL and HTTPS redirects
- server-rendered or post-JavaScript text/content
- password/prelaunch/auth middleware and API calls

Do not send credentials or bypass controls to a crawler. Do not run ad clicks, click simulation, or traffic generation.

### 4. Inspect implementation and configuration

Search only relevant files for route guards, prelaunch rewrites, auth redirects, robots headers, `noindex`, canonical generation, sitemap generation, privacy/CMP code, ad scripts, `ads.txt`, UGC moderation, and duplicate publisher IDs. Inspect deployment configuration and response headers. Redact all secrets in notes and output.

### 5. Browser and consent checks

Use a clean/incognito browser when practical. Verify keyboard/readability/basic mobile layout as part of user experience. On an approved/testable CMP implementation, follow Google’s documented test flow (for example `?fc=alwaysshow` or the current official equivalent), confirm the message is actually published, exercise accept/reject/manage/revoke, and check that consent state gates the Google ad request as intended. Do not report “CMP ready” merely because a banner appears.

### 6. Validation

Run the smallest relevant tests/build/typecheck/lint and direct HTTP checks. For UI issues, inspect rendered behavior at the affected viewport. Report commands actually run, failures, warnings, and checks not run. Do not deploy as part of an audit.

## Evidence and verdicts

Every finding must include the URL/file/route, observed evidence, source classification, impact, and next action.

- `PASS`: evidence satisfies the cited Google criterion or the check is explicitly a Google recommendation and evidence is present.
- `FAIL`: evidence conflicts with an applicable Google requirement/policy or blocks review/crawler access.
- `NEEDS VERIFICATION`: missing live access, dashboard evidence, consent state, account data, or runtime proof.
- `NOT APPLICABLE`: explain why.

Use these severities:

- `BLOCKER`: likely prevents review, violates a policy, exposes private data, or prevents Google from evaluating content.
- `HIGH`: strong approval risk or required setup missing.
- `MEDIUM`: official recommendation or material quality/UX/operational risk.
- `LOW/INFO`: useful improvement or monitoring note.

Overall verdict:

- `NO-GO`: any unresolved `BLOCKER` or unverified gate that prevents a trustworthy review.
- `CONDITIONAL GO`: no known blocker, but one or more `HIGH`/material `NEEDS VERIFICATION` items remain.
- `READY TO SUBMIT`: no known blocker and the required evidence is present. Still state that Google can approve or reject after its own review.

## Required report

Return a concise but evidence-backed report in this order:

1. Verdict and one-sentence reason.
2. Ordered user action plan using the best-chance order above.
3. Findings table: severity, status, area, evidence, official Google source, action.
4. Public-route/access table, including which pages are intentionally read-only.
5. CMP/privacy, `robots.txt`, `ads.txt`, sitemap, canonical, and crawler results.
6. AdSense dashboard/account steps the user must perform themselves.
7. Tests/checks run and not run.
8. Remaining risks and what would change the verdict.

Use official source links from `references/google-criteria.md` near relevant findings. Cite the source as a direct Markdown link, not as an internal search reference. If a source is ambiguous or has changed, say so and re-check the current official page before making a policy claim.

## App-specific access pattern

For a game or logged-in web app, the safe pattern is:

- public: landing/about/help/rules, public leaderboard/league views, public puzzle explanation or preview;
- read-only: public puzzle page may render the puzzle but must disable play, submit, hints that consume quota, score recording, and account mutations;
- authenticated: play, submissions, profile, private matches, chat, payments, admin tools, and any state-changing action.

This is an audit/reviewability pattern, not a Google promise that these exact routes are required. Confirm each route’s real behavior, including direct URL access and API authorization.
