# Website Launch Skills

<p align="center">
    <img src="./assets/banner-web.svg" alt="Website Launch Skills" width="900">
</p>

Focused skills for safer, evidence-backed website launches.

## Installation (30-second setup)

### 1. Get the skills

#### Claude Code

```bash
claude plugin marketplace add tombrajer/website-launch-skills
claude plugin install website-launch-skills@website-launch-skills
```

Or, from inside a session:

```text
/plugin marketplace add tombrajer/website-launch-skills
/plugin install website-launch-skills@website-launch-skills
```

#### Codex, and other agents

```bash
npx skills@latest add tombrajer/website-launch-skills
```

Pick the skills you want, and which coding agents to install them on. The installer lets you choose individual skills.

## Included skills

- [`launch-commander`](skills/launch-commander/) — complete launch readiness gate
- [`production-deploy-verifier`](skills/production-deploy-verifier/) — verify the intended revision is live
- [`seo-indexing-audit`](skills/seo-indexing-audit/) — check crawlability and indexing signals
- [`privacy-cmp-audit`](skills/privacy-cmp-audit/) — check consent and privacy behavior
- [`security-launch-gate`](skills/security-launch-gate/) — check pre-launch security boundaries
- [`mobile-accessibility-audit`](skills/mobile-accessibility-audit/) — check mobile UX and accessibility
- [`content-trust-audit`](skills/content-trust-audit/) — check public content and trust signals
- [`adsense-readiness-audit`](skills/adsense-readiness-audit/) — check official AdSense readiness criteria
- [`website-pre-launch-audit`](skills/website-pre-launch-audit/) — broader production-readiness audit
- [`post-launch-monitor`](skills/post-launch-monitor/) — safe checks after deployment

All audits are read-only by default. They do not deploy, publish CMP settings, change DNS, or modify production data without explicit authorization.
