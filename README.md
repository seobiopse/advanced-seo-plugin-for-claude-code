# SEO Audit Plugin for Claude Code

**Production-ready v1.3.0** — a Claude Code plugin that runs comprehensive SEO, AEO (Answer Engine Optimization), and GEO (Generative Engine Optimization) audits on any website. Produces ticket-ready Markdown reports and interactive HTML reports with before/after code, confidence scores, interactive checklists, and quantitative scoring.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Version](https://img.shields.io/badge/version-1.3.0-blue.svg)](CHANGELOG.md)
[![Plugin type](https://img.shields.io/badge/type-Claude%20Code%20plugin-navy.svg)](https://docs.claude.com)

---

## Why this plugin exists

SEO audits are mostly the same work, done badly, over and over, by every team. Engineers either skip SEO entirely (shipping invisible pages) or drown in 200-item checklists they can't triage. Marketing teams hand over audit spreadsheets that don't connect to code. Meanwhile, the rules have gotten more complex — Google AI Overviews, ChatGPT citations, Perplexity source cards, Claude web search, Gemini, Bing Copilot each need different signals.

This plugin fixes that by:

1. **Codifying a production-grade checklist** across 20 reference files covering every major SEO/AEO/GEO pillar.
2. **Adapting to YOUR site's architecture** — it detects whether you're a blog, SaaS, e-commerce, job board, bootcamp, docs site, or multi-product conglomerate, and tailors the audit scope accordingly.
3. **Producing engineer-actionable reports** — every finding has confidence scores, evidence sources, broken-code-vs-fixed-code examples, and a verification step.
4. **Quantifying quality** with two 0–100 scoring models — SEO Quality (NLP-driven: LSI, semantic, entities, sentiment) and E-E-A-T (Google's Search Quality Rater Guidelines).
5. **Enforcing governance** so extensions go through review, not ad-hoc edits.

---

## Is this plugin right for you?

**Yes if:**
- Your team uses Claude Code for development.
- You have at least one web property to audit — any architecture (React / Next.js / Remix / plain HTML / WordPress / Webflow / etc.).
- You want a repeatable, standards-based SEO / AEO / GEO audit workflow.
- You want engineering to own technical SEO, and marketing to own strategy.

**Probably not if:**
- You need automated daily crawling with dashboards (use Ahrefs / Semrush / Screaming Frog for that).
- You want a drop-in audit UI for non-technical users (this one requires the Claude Code CLI).

---

## Is this plugin universal or React / Next.js-specific?

**Universal.** The plugin is built around **site-architecture archetypes**, not any specific client:

- `domain-discovery.md` covers 10 common archetypes (Marketing, Blog, E-commerce, SaaS, Job board, Staffing services, Course platform, Documentation, Multi-product conglomerate, Personal site).
- Every other reference file is stack-agnostic (React/Next.js patterns are called out where relevant, but the underlying checks apply to any HTML-producing website).
- The scoring rubrics and finding schema are fully generic.

**One worked-example file** (`react-nextjs-architecture-profile.md`) demonstrates how to write a site-specific profile for a multi-subdomain brand. Forks should delete it OR duplicate it as `<your-brand>-profile.md` and adapt the contents. Instructions are inside that file.

The plugin was battle-tested on three real domains during development (one marketing site, one bootcamp subdomain, one staffing services subdomain), but there's no React / Next.js-specific code, rule, or default elsewhere in the plugin.

---

## Quick start

### Installation (end users)

If your team has published this plugin to a marketplace:

```bash
/plugin marketplace add <org>/<repo>
/plugin install seo-audit
```

Or install from a local clone:

```bash
git clone <this-repo>
# In Claude Code:
/plugin install <path-to-cloned-repo>
```

### Your first audit

In Claude Code:

```
/full-audit https://your-domain.com/
```

Claude asks a few clarifying questions, detects your site's archetype, and produces two files in your workspace folder:

- `seo-audit-<mode>-<date>.html` — interactive HTML report
- `seo-audit-<mode>-<date>.md` — Markdown for tickets

Open the HTML. Tick off findings as you ship fixes. A "Ready to re-run" panel appears when you've addressed every finding.

### Five slash commands

| Command | Purpose |
|---|---|
| `/seo-audit` | Full technical SEO audit (~80 checks) |
| `/aeo-audit` | Answer-Engine Optimization (AI Overviews, featured snippets) |
| `/geo-audit` | Generative-Engine Optimization (ChatGPT, Perplexity, Claude, Gemini, Copilot) |
| `/full-audit` | All three pillars + scoring + comprehensive deep-dives |
| `/crawl-check` | Fast 14-check rendering-only audit for React/Next.js/SPA sites |

---

## What's inside

### Plugin structure

```
seo-audit-plugin/
├── plugin.json                     # Plugin manifest
├── README.md                       # (this file)
├── HANDOFF.md                      # Engineer-facing usage guide
├── NEW-CHECK-REQUEST-TEMPLATE.md   # Governance template for proposing extensions
├── CHANGELOG.md                    # Version history
├── CONTRIBUTING.md                 # How to contribute + governance
├── LICENSE                         # MIT
├── commands/                       # 5 slash-command definitions
│   ├── seo-audit.md
│   ├── aeo-audit.md
│   ├── geo-audit.md
│   ├── full-audit.md
│   └── crawl-check.md
└── skills/
    └── seo-audit/
        ├── SKILL.md                # The skill's "brain"
        ├── assets/
        │   ├── report-template.md
        │   └── report-template.html
        ├── references/             # 20 reference files
        │   ├── domain-discovery.md           # STEP 0 (mandatory first read)
        │   ├── issue-framework.md            # Finding schema + reporting template
        │   ├── seo-audit.md                  # Core SEO checklist
        │   ├── aeo.md                        # AEO for informative content
        │   ├── aeo-transaction.md            # AEO for money pages
        │   ├── geo.md                        # GEO for informative content
        │   ├── geo-transaction.md            # GEO for money pages
        │   ├── ai-overview-playbook.md       # Google AI Overview specifics
        │   ├── llm-citation-playbook.md      # ChatGPT/Perplexity/Claude/Gemini/Copilot
        │   ├── crawlability-react.md         # React/Next.js rendering deep-dive
        │   ├── structured-data-advanced.md   # @graph, schema recipes, cross-references
        │   ├── ai-content-safety.md          # Google policies for AI-assisted content
        │   ├── image-optimization.md         # Alt text, WebP, LCP, schema requirements
        │   ├── product-experience-audit.md   # Non-technical product architecture
        │   ├── pseo-playbook.md              # Programmatic SEO (jobs/courses/events/etc)
        │   ├── transaction-intent-playbook.md # Landing/money pages
        │   ├── tracking-validation.md        # GA4, GTM, pixels, consent mode
        │   ├── robots-llms-txt-playbook.md   # Crawler policy + llms.txt spec
        │   ├── sitemap-playbook.md           # Sitemap strategy (changefreq/priority/lastmod)
        │   ├── seo-quality-score-rubric.md   # 0-100 content quality score
        │   ├── eeat-score-rubric.md          # 0-100 E-E-A-T score
        │   └── react-nextjs-architecture-profile.md         # WORKED EXAMPLE — adapt for your brand
        └── scripts/
            └── generate_report.py             # Findings JSON → MD + interactive HTML
```

### 20 reference files — organized by purpose

- **Mandatory first read** (1): `domain-discovery.md`
- **Reporting framework** (1): `issue-framework.md`
- **Core checklists** (4): `seo-audit.md`, `aeo.md`, `aeo-transaction.md`, `geo.md`, `geo-transaction.md` (5 actually)
- **Engine-specific playbooks** (2): `ai-overview-playbook.md`, `llm-citation-playbook.md`
- **Technical deep-dives** (4): `crawlability-react.md`, `structured-data-advanced.md`, `robots-llms-txt-playbook.md`, `sitemap-playbook.md`
- **Content + trust** (3): `ai-content-safety.md`, `image-optimization.md`, `product-experience-audit.md`
- **Programmatic + commercial** (2): `pseo-playbook.md`, `transaction-intent-playbook.md`
- **Tracking** (1): `tracking-validation.md`
- **Scoring** (2): `seo-quality-score-rubric.md`, `eeat-score-rubric.md`
- **Worked example** (1): `react-nextjs-architecture-profile.md`

### The report's interactive features

- **Domain archetype badge** at the top — transparent about what was audited and what was skipped.
- **Two scorecards**: SEO Quality (0–100) + E-E-A-T (0–100), each with per-dimension progress bars, sub-signal status chips (pass/partial/fail), and a "Top improvements" list.
- **Two audit-group banners**: Traditional SEO (crawl/index/rank) + LLM Visibility (AIO + other LLMs).
- **Per-finding cards** with severity badge, confidence score, evidence source, pillar chips (SEO/AEO/GEO), broken-vs-fixed code side-by-side with copy buttons, and a verification step.
- **Interactive checklist** — each finding has a "Mark as addressed" toggle. Progress persists in browser localStorage.
- **Sticky progress bar** — live "X of N addressed" counter.
- **Re-run panel** — appears when all findings are addressed; includes suggested re-run commands.
- **Print-friendly** — all interactive UI hides for PDFs.

---

## Architecture principles

### 1. Site-architecture-driven, not client-specific

The plugin reasons about domains via their architecture archetype (marketing / blog / SaaS / job board / etc.), not by name. No hardcoded rules for any specific brand. Every "special case" in the audit logic comes from `domain-discovery.md`, which is itself generic.

### 2. Checklist + scoring, not opinion

Every finding is tied to a standard — Google Search Central, schema.org, RFC, web.dev, WCAG, OpenAI crawler docs, Anthropic crawler docs. Severity is calibrated against documented best practice. Confidence scores separate direct observation from inference.

### 3. Engineer-actionable

Every finding has broken-code and fixed-code examples, tied to the specific file or template they apply to. Every fix has a concrete verification step (curl command, DevTools check, Rich Results Test).

### 4. Governance

Engineers don't edit the plugin directly. Changes go through Marketing Director / AVP / Manager review via the `NEW-CHECK-REQUEST-TEMPLATE.md` form. Maintainer has sole commit access. See `CONTRIBUTING.md`.

### 5. Transparent skip logic

When the plugin doesn't apply a check (because the domain archetype doesn't include it), the report explicitly says so. The user can correct a misclassification before reading findings.

---

## Development

### Running an audit locally (without Claude Code)

The reference files are Markdown — you can read them as a manual checklist. The `scripts/generate_report.py` script is standalone:

```bash
python3 skills/seo-audit/scripts/generate_report.py \
  --input your-findings.json \
  --output-dir /path/to/output \
  --name my-audit-2026-01-15
```

See `examples/` for a sample findings JSON showing the schema.

### Extending the plugin

Don't edit the reference files directly — use the governance process. See `CONTRIBUTING.md` and `NEW-CHECK-REQUEST-TEMPLATE.md`.

### Reporting a bug

Open a GitHub issue with:
- Plugin version (`plugin.json`)
- Expected behavior
- Observed behavior
- Sample HTML report or findings JSON if applicable
- Your site's domain archetype + stack

### Maintainer

[Girish Kumar G](https://in.linkedin.com/in/girisshgk) — Father of SEO

For audit questions → LinkedIn DM or your team's SEO Slack / Linear channel.

---

## Version history

See [CHANGELOG.md](CHANGELOG.md) for the full history. Highlights:

- **v1.3.0 (2026-04-19)** — Universal pivot for public release. Replaced any company-specific profile with a generic `react-nextjs-architecture-profile.md`; sanitized all worked examples to use generic `example.com` subdomains. Added roadmap for future stack profiles (Static HTML, WordPress, Shopify, Angular, PHP, Wix/Webflow).
- **v1.2.0 (2026-04-19)** — Step 0 domain discovery added as mandatory first step. Plugin now detects site archetype + tailors audit scope. No more false-positive findings on wrong-archetype pages.
- **v1.1.0 (2026-04-19)** — SEO Quality Score (NLP-driven) + E-E-A-T Score (Google Guidelines) added, with per-page-type rubrics and visual scorecards.
- **v1.0.0 (2026-04-19)** — First production-ready release. 16 reference files, 5 slash commands, interactive checklist with progress bar + re-run panel, governance process, battle-tested on 3 domains.

---

## License

MIT — see [LICENSE](LICENSE) for full terms.

You can use, modify, and distribute this plugin freely for commercial and non-commercial projects. Attribution appreciated but not required. The signature band in generated reports (by default showing the plugin author's name) can be customised or removed by editing `_HTML_TEMPLATE` in `scripts/generate_report.py`.

---

*Crafted with care by [Girish Kumar G](https://in.linkedin.com/in/girisshgk) · Father of SEO*
