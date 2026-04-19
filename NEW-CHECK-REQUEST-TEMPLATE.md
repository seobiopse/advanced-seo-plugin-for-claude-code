# New Check Request — Template

Fill out every field. **Skipped fields signal the gap isn't well understood yet** — the Director / AVP / Manager will send it back.

Copy this file, rename to `request-<short-slug>-YYYY-MM-DD.md`, fill it in, submit to the Marketing Team Director / AVP / Manager via the team's standard channel (Linear / Confluence / email).

Do not edit the plugin's reference files directly. That's what this process prevents.

---

## 1. Summary

**One-sentence description of the proposed check:**
_Example: "Verify that every `<img>` with a width > 600px has `fetchpriority=\"high\"` when it's the LCP element."_

**Who is proposing this:**
- Name:
- Role:
- Team:
- Date submitted:

---

## 2. The gap — what the current plugin misses

**Describe the specific pattern you observed that existing checks don't catch.**

Include:
- What page / URL you were auditing
- What output the current audit gave
- What it should have flagged but didn't

_Example: "Audited /blog/post-abc with /full-audit. Page had a 1200×800 hero image with no fetchpriority attribute. Lighthouse shows LCP 3.8s on mobile. Current plugin's image-optimization.md has a check for `loading=\"lazy\"` but nothing about `fetchpriority`."_

---

## 3. Evidence this is a real pattern (not one-off)

**Show your work.** The Director needs to see that this isn't a niche issue you hit once.

Acceptable evidence:
- Links to 3+ URLs where the same pattern appears
- Citation from Google Search Central docs, schema.org, web.dev, MDN, RFC, or similar authoritative source
- Lighthouse / GSC / analytics data showing impact
- An issue thread or post-mortem where this came up

Unacceptable evidence:
- "I heard about this on a podcast"
- "Someone on Twitter said so"
- "It seems like a good idea"

**Paste links / screenshots / docs here:**

---

## 4. Where the check should live

**Which reference file should get this check?** If you don't know, put your best guess + reasoning.

- `issue-framework.md` — structural change only, rare
- `seo-audit.md` — general SEO checklist
- `aeo.md` / `aeo-transaction.md` — AEO / commercial AEO
- `geo.md` / `geo-transaction.md` — GEO / commercial GEO
- `crawlability-react.md` — React / Next.js rendering
- `structured-data-advanced.md` — schema patterns
- `ai-content-safety.md` — AI-assisted content policy
- `image-optimization.md` — images
- `product-experience-audit.md` — product architecture
- `pseo-playbook.md` — programmatic SEO
- `transaction-intent-playbook.md` — landing / money pages
- `ai-overview-playbook.md` — Google AI Overview specifics
- `llm-citation-playbook.md` — ChatGPT / Perplexity / Claude / Gemini / Copilot
- `tracking-validation.md` — GA4 / GTM / pixels
- `robots-llms-txt-playbook.md` — crawler policy
- `sitemap-playbook.md` — sitemap strategy
- `react-nextjs-architecture-profile.md` — React / Next.js-specific
- **NEW FILE** — if none of the above fit

**If you're proposing a NEW reference file**, also answer:
- Why doesn't this fit in an existing file?
- What's the file name you propose?
- Roughly how many checks would live in it (is it justified as a standalone file)?

---

## 5. The check itself

**Write the check exactly as you propose it would appear in the reference file.** Use the existing format.

```
- **CHECK-ID** Short imperative description of what to verify.
  - **Pass condition:** what counts as a pass
  - **Fail condition:** what counts as a fail
  - **How to test:** concrete command / tool / steps
```

_Example:_

```
- **IMG-18** For every <img> that is the LCP candidate on any page, the attribute `fetchpriority="high"` must be present in the raw HTML.
  - Pass: grep returns "fetchpriority=\"high\"" on the LCP image tag
  - Fail: the LCP image has no fetchpriority attribute
  - Test: Lighthouse report → LCP section → identify the element → inspect HTML
```

---

## 6. Severity and confidence

**Proposed severity:** Critical / High / Medium / Low / Info

**Why that severity** (1-2 sentences):

**Proposed confidence calibration** (when to rate this finding 95+ vs 70 vs 50):

---

## 7. Impact per pillar

Does this check matter for SEO, AEO, GEO, or some combination? Fill in each:

- **SEO:** _description of impact, or "no direct SEO impact"_
- **AEO:** _description of impact, or "no direct AEO impact"_
- **GEO:** _description of impact, or "no direct GEO impact"_

---

## 8. Fix pattern

**What does the fix look like in code?** Include broken-code and fixed-code examples in the same format the existing reference files use.

**Broken code:**
```html
<!-- your example of what's wrong -->
```

**Fixed code:**
```html
<!-- your example of the correction -->
```

---

## 9. Verification step

**How does an engineer confirm the fix landed?** Must be a concrete action (command, tool, URL parameter).

_Example: "Run `curl -s <url> | grep -oP 'fetchpriority=\"[^\"]+\"'` and confirm \"high\" appears on the LCP image."_

---

## 10. Overlap check

**Does this duplicate or partially overlap with an existing check?** Be honest — overlap isn't disqualifying, but hidden overlap is.

Searched existing reference files for:
- Keywords: _list the keywords you searched_
- Existing check IDs that look related: _list them_

**Is this truly net-new, or is it a refinement of an existing check?**

---

## 11. Stack relevance

**Is this specific to one stack (e.g. Next.js App Router only) or universal?**

- If stack-specific: name the stack, and note whether existing your brand / team properties use it.
- If universal: skip.

---

## 12. Effort estimate (for the plugin maintainer)

Your best guess of how much work this is:

- [ ] Tiny (< 30 min) — single bullet added to an existing reference file
- [ ] Small (< 2 hrs) — new check + fix examples + verification step, added to existing file
- [ ] Medium (< 1 day) — new check + new reference file subsection + SKILL.md update
- [ ] Large (> 1 day) — new reference file from scratch + SKILL.md table update + cross-linking from existing files

---

## 13. Anything else

- References / reading that informed the proposal:
- Team members you've discussed this with:
- Previous audits where this gap appeared:
- Anything the Director needs to know before reviewing:

---

## For the reviewer (Marketing Director / AVP / Manager)

| Field | Value |
|---|---|
| Date received |  |
| Decision | Approved / Approved with modifications / Deferred / Rejected |
| Reviewer name |  |
| Decision date |  |
| Modifications required (if any) |  |
| Routed to maintainer on |  |
| Target version for inclusion |  |
| Notes |  |

Rejection reason (if applicable):
_Be specific — future requests get stronger when engineers understand what bar wasn't met._

---

## For the maintainer (Girish Kumar G)

| Field | Value |
|---|---|
| PR number |  |
| Reference file(s) edited |  |
| Version bumped to |  |
| Changelog entry |  |
| Team notification sent |  |

---

*This template is part of the SEO Audit Plugin governance. See HANDOFF.md — "Extensions and changes — governance" section.*
