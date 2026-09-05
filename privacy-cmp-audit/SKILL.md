---
name: privacy-cmp-audit
description: "Audit privacy pages, consent management, ad and analytics gating, regional CMP behavior, consent withdrawal, and published messaging before website launch."
---

# Privacy and CMP audit

Audit-only by default. Do not publish a consent message, change tracking configuration, accept legal terms, or alter production code without explicit authorization. This is a technical audit, not legal advice.

For Google advertising integrations, use current official guidance such as [EU user consent policy](https://support.google.com/adsense/answer/7670013?hl=en), [European regulations messages](https://support.google.com/adsense/answer/10960768?hl=en-GB), [consent revocation](https://support.google.com/adsense/answer/10959060?hl=en), and the current [TCF guidance](https://support.google.com/adsense/answer/9804260?hl=en-GB). Re-check time-sensitive regional requirements.

## Workflow

1. Establish jurisdictions and data flows: EEA, UK, Switzerland, other target markets, analytics, advertising, personalization, cookies/local storage, pixels, embeds, chat, payments, and third-party scripts.
2. Inspect the privacy/cookie information from a logged-out clean session. Verify it is reachable without login, matches the actual data flows, identifies the operator/contact, explains purposes and providers, and links to the active consent controls. Do not label a page legally sufficient without legal review.
3. Inventory scripts and network requests before consent. Identify ad tags, analytics, pixels, fingerprinting/storage, embedded media, and CMP code. Verify region-appropriate requests are not made before required consent.
4. Test each state in a clean/incognito browser and after refresh/navigation:
   - first visit/no choice;
   - accept all;
   - reject/non-personalized choice;
   - manage purposes/providers;
   - close/dismiss behavior;
   - reopen and revoke/withdraw consent;
   - changed consent remains consistent across pages.
5. Confirm the banner is actually published, not merely visible in a local preview. For Google Privacy & Messaging, use Google’s documented test flow only on an authorized test site; do not click live ads.
6. Check that consent state reaches the intended ad/analytics integration, consent signals are valid, and scripts do not race ahead of the CMP. Inspect browser storage, API state, and network timing without collecting personal data.
7. Check special surfaces: privacy-policy page, login/register, child-directed content, public UGC, embedded third-party content, error pages, and mobile layout. The privacy-policy page should not accidentally load ad tags or other consent-requiring scripts.

## Report

Include a data-flow table, regional state table, observed requests, consent/revocation evidence, privacy-page gaps, and exact user actions. Classify findings as technical blocker, legal review needed, Google integration issue, or improvement.

Use `NO-GO` for ad/analytics firing before required consent, no withdrawal path, broken CMP state, or privacy information that contradicts the implementation. A functioning CMP does not prove legal compliance.
