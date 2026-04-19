# Changelog

All notable changes to the SEO Audit Plugin are documented here.

The format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

---

## [1.3.0] — 2026-04-19

### Added
- **`references/react-nextjs-architecture-profile.md`** — new universal architecture profile for React + Next.js projects. 14 sections covering multi-subdomain architecture, `next.config.js` SEO settings, middleware patterns, ISR strategy, environment-aware canonicals, shared layout + schema injection, API routes, `next/image`, font loading, edge runtime, common anti-patterns, and an audit checklist (RNJS-1 through RNJS-20).
- **Stack-profile roadmap** — the architecture profile explicitly names planned future profiles: Static HTML, WordPress, Shopify, Angular, PHP, Wix/Webflow. Forks can add their own profile for any stack by following the same 14-section template.

### Changed
- **Sanitized the plugin for public GitHub release.** All company-exclusive references, internal subdomain names, and domain-specific placeholders have been replaced with universal architecture-based examples (`example.com`, `jobs.example.com`, `learn.example.com`, etc.). The plugin is now safe to publish openly without leaking any specific employer / client context.
- Removed the former brand-specific architecture profile and replaced it with `react-nextjs-architecture-profile.md` — the same shape, but framed around stack architecture rather than any one brand.
- Refreshed every worked example in `geo-transaction.md`, `pseo-playbook.md`, `domain-discovery.md` to use generic product names (job board, learning platform, recruitment service) instead of any company's specific product names.

### Rationale
A plugin distributed publicly must not carry any employer / client-specific identity. v1.3 completes the universal pivot: anyone can clone, read, and audit any site — React, WordPress, Shopify, Angular — without tripping on leftover brand references.

---

## [1.2.0] — 2026-04-19

### Added
- **`references/domain-discovery.md`** — new mandatory Step 0 of every audit. Detects site archetype (10 common types: Marketing, Blog, E-commerce, SaaS, Job board, Staffing services, Course platform, Documentation, Multi-product conglomerate, Personal site) and tailors audit scope accordingly.
- Per-archetype Apply/Skip lists for all 20 reference files.
- Transparent "explicitly not audited" reporting in every audit output so users can verify the archetype was detected correctly.

### Changed
- `SKILL.md` now requires Step 0 domain discovery before loading any other reference file.
- `HANDOFF.md` — new Section 1a explains to engineers that the plugin tailors itself to the site's architecture.
- URL-level intent detection rules now defer to archetype classification (a SaaS site with `/jobs` meaning "jobs-to-be-done" no longer gets job-board treatment).
- `react-nextjs-architecture-profile.md` reframed as a worked example with an explicit instructional preamble — forks can delete it or adapt it to their own brand.

### Rationale
The v1.1 plugin risked producing noise findings when applied to a domain archetype it didn't understand (e.g. flagging missing `JobPosting` schema on a marketing page). Step 0 prevents that structurally.

---

## [1.1.0] — 2026-04-19

### Added
- **`references/seo-quality-score-rubric.md`** — 0–100 NLP-driven content quality score covering LSI terms, semantic variants, named entities, sentiment analysis, content depth, keyword targeting discipline, and trust-signal density. Separate rubrics for Landing/Money pages vs Blog/Article pages.
- **`references/eeat-score-rubric.md`** — 0–100 E-E-A-T score (Experience + Expertise + Authoritativeness + Trust) aligned with Google's Search Quality Rater Guidelines. Separate rubrics for Landing/Money vs Blog/Article with distinct weight distributions (Trust 35/100 on commercial; Experience 30/100 on editorial).
- Visual Scorecards section at the top of every `/full-audit` HTML report with per-dimension progress bars, color-coded sub-signals (green/amber/red pass/partial/fail), and a "Top improvements" list.
- `scores` field in findings JSON schema.

### Changed
- `SKILL.md` adds a new Step 6b: Compute scores whenever running `/full-audit` or on explicit user request.
- `issue-framework.md` documents the `scores` schema.
- Generator's `render_scores_block` + CSS added.

---

## [1.0.0] — 2026-04-19

### Added — first production-ready release

- **16 reference files** codifying a production-grade SEO / AEO / GEO audit methodology:
  - Core: `issue-framework.md`, `seo-audit.md`, `aeo.md`, `aeo-transaction.md`, `geo.md`, `geo-transaction.md`
  - Deep-dives: `crawlability-react.md`, `structured-data-advanced.md`, `ai-content-safety.md`, `image-optimization.md`, `product-experience-audit.md`, `pseo-playbook.md`, `transaction-intent-playbook.md`, `ai-overview-playbook.md`, `llm-citation-playbook.md`, `tracking-validation.md`, `robots-llms-txt-playbook.md`, `sitemap-playbook.md`, `react-nextjs-architecture-profile.md`
- **5 slash commands**: `/seo-audit`, `/aeo-audit`, `/geo-audit`, `/full-audit`, `/crawl-check`
- **Interactive HTML reports** with:
  - Navy + Playfair Display premium visual design
  - Two audit-group banners (Traditional SEO / LLM Visibility)
  - Per-finding cards with severity + confidence + evidence + pillars + page + before/after code + verification
  - Syntax highlighting for HTML / JSON / JSX / TSX / CSS / bash code blocks
  - Copy-to-clipboard buttons on all code blocks
  - Interactive "Mark as addressed" checkboxes with localStorage persistence
  - Sticky progress bar ("X of N addressed")
  - Re-run panel that appears when all findings are addressed
  - Signature band with author LinkedIn link
  - Print-friendly (interactive UI hides in print)
- **Confidence scoring** (0–100) with evidence source on every finding.
- **Per-page context** — each finding shows the specific URL(s) it applies to.
- **Governance process** — engineers don't edit the plugin directly. Extensions go through `NEW-CHECK-REQUEST-TEMPLATE.md` → Marketing Director/AVP/Manager review → Maintainer implementation.
- **`HANDOFF.md`** — engineer-facing usage guide with TL;DR, installation, first-audit walkthrough, troubleshooting, FAQs, and governance.
- Python 3 standalone report generator (`scripts/generate_report.py`) — takes a findings JSON, produces both Markdown and HTML outputs.

### Battle-tested on

- `www.example.com` (16 findings, 4 Critical)
- `product1.example.com` (14 findings, 0 Critical)
- `services.example.com` (9 findings, 0 Critical)

---

## Release policy

- **Major** (x.0.0) — breaking changes to findings schema or reference-file structure.
- **Minor** (1.x.0) — new reference files, new scoring models, new commands, significant UI changes.
- **Patch** (1.0.x) — bug fixes, clarifications in existing references, version-bumps of dependencies.

Maintainer (Girish Kumar G) is sole commit authority. Extension requests route through the governance process in `CONTRIBUTING.md`.
