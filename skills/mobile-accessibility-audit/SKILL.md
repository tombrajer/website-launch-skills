---
name: mobile-accessibility-audit
description: "Audit mobile layout and core accessibility behavior before launch, including keyboard access, focus, labels, contrast, touch targets, responsive failures, and dynamic states."
---

# Mobile accessibility audit

Audit-only by default. Do not redesign or change code unless explicitly requested. Use [W3C WCAG guidance](https://www.w3.org/WAI/standards-guidelines/wcag/) as the accessibility reference. Do not claim certification from an automated scan.

## Workflow

1. Define supported devices/orientations, critical routes, user roles, languages, browser targets, and whether the page is an app/game with keyboard or touch interactions.
2. Test representative mobile viewports and a short desktop width. Check zoom/text scaling, orientation, safe areas, no horizontal overflow, clipped content, sticky/fixed UI, scroll containers, modals, and the on-screen keyboard.
3. Check structure and operability:
   - semantic headings, landmarks, buttons, links, and lists;
   - every control has an accessible name and visible state;
   - keyboard-only tab order and visible focus;
   - touch controls have sufficient separation and do not depend on hover;
   - dialogs trap/release focus correctly and close accessibly;
   - form validation and async errors are perceivable;
   - dynamic content, loading, and disabled states are announced or otherwise understandable.
4. Check visual access: contrast, text readability, color-independent meaning, focus indicators, reduced motion, small-screen density, and content remaining usable at increased text size.
5. Check interaction-specific risks: game board/rack, drag/drop alternatives, keyboard shortcuts, timers, login/CMP dialogs, tables, menus, and scrollable leaderboard areas. A public read-only view must remain usable without accidentally enabling protected actions.
6. Use automated checks only as a starting point. Add manual keyboard, screen-reader or accessibility-tree inspection where available. Record browser/device and checks not performed.

## Report

Return route/viewport, issue, user impact, WCAG reference when applicable, evidence, severity, and remediation direction. Use `NO-GO` for inaccessible critical navigation, blocked login/payment/core task, severe mobile overflow, or a consent/auth dialog users cannot operate. Mark uncertain screen-reader behavior `NEEDS VERIFICATION`.
