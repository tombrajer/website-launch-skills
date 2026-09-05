# Official Google criteria and suggestions

Last checked: 2026-09-05. Google changes policies and help pages. Re-open the linked official pages during each audit and treat the current page as authoritative.

This file is a source map for the skill. It intentionally paraphrases Google guidance instead of copying policy text. Use the links as the citations in audit reports.

## Eligibility, site content, and review

- [Google AdSense eligibility requirements](https://support.google.com/adsense/answer/9724?hl=en): the publisher must have original content that attracts an audience, comply with AdSense policies, be able to access/edit the site HTML, and meet the age/contracting requirements.
- [Make sure your site's pages are ready for AdSense](https://support.google.com/adsense/answer/7299563?hl=en): Google highlights unique and interesting content, clear/easy navigation, good user experience, readable/functioning pages, and original publisher contribution. It warns against scraped/copyrighted content and unmanaged or low-value user-generated content.
- [Your AdSense account wasn't approved](https://support.google.com/adsense/answer/81904?hl=en): common issues include insufficient content, content quality, policy violations, navigation, traffic sources, duplicate accounts, and unsupported language. Google may review the site beyond the URL used during signup.
- [Languages Google publisher products support](https://support.google.com/adsense/answer/9727?hl=en): the primary language must be supported for Google publisher products; Czech is listed in the current page checked above. Do not place ad code on pages primarily in an unsupported language.
- [One AdSense account per publisher](https://support.google.com/adsense/answer/9729?hl=en-GB): Google generally permits one account per publisher. A separate account is for a genuinely separate organization/payee with the correct account type and payment details, not a workaround for approval.

## Policies, restrictions, placement, and traffic

- [AdSense Program policies](https://support.google.com/adsense/answer/48182?hl=en): prohibited ad behavior, misleading navigation, private communications, pop-ups, software integration, non-content pages, deceptive implementation, and other publisher obligations.
- [Google Publisher Policies](https://support.google.com/adsense/answer/10008391?hl=en): policies apply to the page content around the ads, including publisher content, UGC, other ads, and links. The publisher is responsible for compliance.
- [Google Publisher Restrictions](https://support.google.com/adsense/answer/10437795?hl=en): restrictions may reduce or eliminate demand without being the same as a policy violation. Report this separately from a blocker.
- [Ad placement policies](https://support.google.com/adsense/answer/1346295?hl=en): avoid accidental clicks, unnatural attention, misleading labels, content-mimicking ads, incentives, pop-ups, auto-refresh, and ads on content Google cannot evaluate. It includes game-play placement guidance.
- [Top invalid traffic and policy violations that lead to account closure](https://support.google.com/adsense/answer/2660562?hl=en): self-clicks, encouragement, artificial/bought traffic, deceptive placement, more paid material than publisher content, and policy-risk content are common closure causes.
- [Invalid traffic](https://support.google.com/adsense/answer/16737?hl=en): never click own ads, ask others to click, buy/incentivize traffic, or use bots/repeated interactions. The publisher is responsible for traffic quality.
- [Google Search Essentials](https://developers.google.com/search/docs/essentials): use only as an adjacent crawl/search-quality check. Technical requirements, spam policies, and best practices are not a substitute for AdSense policy. Do not use cloaking or other spam tactics.
- [Google Search spam policies](https://developers.google.com/search/docs/essentials/spam-policies): use to flag cloaking, deceptive behavior, scaled/abusive content, and other search-spam risks. A crawler-only AdSense bypass is unacceptable.

## Site connection, code, ads.txt, and crawlability

- [Connect your site to AdSense](https://support.google.com/adsense/answer/7584263?hl=en): add the site, connect with code/ads.txt/meta tag, request review, and keep the site accessible. If a site is protected by login, Google says to temporarily remove the login so the crawler can access it; make sure the crawler is not blocked by `robots.txt`.
- [Verify your site's HTML code](https://support.google.com/adsense/answer/91205?hl=en): the publisher must control the HTML source and place the AdSense code in the page `<head>` when using that verification route.
- [Enter your site URL when you create an AdSense account](https://support.google.com/adsense/answer/2784438?hl=en): submit a standard domain, not a path, query string, or port.
- [AdSense code implementation guide](https://support.google.com/adsense/answer/9274634?hl=en): use the generated code for the ad product and place it on pages where ads should show; do not alter it in ways that inflate performance or harm advertisers.
- [About ads.txt](https://support.google.com/adsense/answer/12171612?hl=en): `ads.txt` is optional but highly recommended. Put the exact authorized seller entry at the root of the domain and include other legitimate ad partners if used.
- [Troubleshoot ads.txt issues](https://support.google.com/adsense/answer/7679060?hl=en): Google must be able to crawl the file; check HTTP success, syntax, exact publisher ID, root location, and robots access. Discovery can take time.
- [Google Crawling and Indexing](https://developers.google.com/search/docs/crawling-indexing): use normal crawl controls, HTTP status, robots rules, and server behavior. Do not use crawler-specific exceptions to show a different site.

## Privacy, consent, and CMP

- [AdSense and the EU user consent policy](https://support.google.com/adsense/answer/7670013?hl=en): for EEA/UK/Switzerland users, provide disclosures and obtain consent as required. Google points to its certified CMP options and the IAB TCF path for personalized ads.
- [Create a European regulations message](https://support.google.com/adsense/answer/10960768?hl=en-GB): use Privacy & messaging to select the site, add the privacy-policy URL, select language/options, and publish. Check the current referrer-policy requirement and the presence of AdSense code where the message is used.
- [About European regulations messages](https://support.google.com/adsense/answer/10961068?hl=en): current message behavior includes TCF integration, consent withdrawal, and Google CMP/consent mode options. Re-check the current TCF version and deadlines.
- [IAB TCF v2.3 requirements](https://support.google.com/adsense/answer/9804260?hl=en-GB): use the current Google notice for TCF v2.3, Purpose 1, and consent-signal requirements. Do not assume an old CMP integration remains valid.
- [Privacy policy requirements](https://support.google.com/adsense/answer/10961370?hl=en): make privacy information accessible; Google specifically cautions against putting consent-requiring scripts such as ad tags on the privacy-policy page.
- [Consent revocation](https://support.google.com/adsense/answer/10959060?hl=en): provide a way for users to revisit/revoke consent; test the real published message and revocation flow.
- [Privacy & messaging](https://support.google.com/adsense/answer/12226986?hl=en): Google provides tools and responsibilities for privacy messages; the publisher remains responsible for legal and framework compliance.
- [Test a Privacy & messaging message](https://support.google.com/adsense/answer/10924669?hl=en): test in a clean browser with Google’s documented preview/query parameters, after publishing the message and placing the required code.

## Monitoring after submission

- [Ad serving limits](https://support.google.com/adsense/answer/16906718?hl=en): new accounts, traffic-quality review, policy issues, `ads.txt`, and crawl problems can affect serving after approval. Monitor AdSense notifications and Policy Center.

## How to use this source map

1. Prefer the exact page linked above that covers the finding.
2. Quote as little as possible; paraphrase and link.
3. Label the result as `Google requirement/policy`, `Google recommendation`, or `project/site-specific check`.
4. If the official page does not state a threshold, do not invent one.
5. Re-check time-sensitive CMP, TCF, account, and ads.txt guidance during every audit.
