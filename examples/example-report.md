# SEO / AEO / GEO Audit — FULL

**Target:** https://example.com/  
**Date:** 2026-01-15  
**Environment:** production  
**Input method:** live-url
  
**Project:** your brand Homepage Audit
  
**Stack:** Next.js App Router
  
**Prepared by:** Your Name — Your Team

## Summary

- Checks run: **180**
- Passed: **140**
- Warnings: **37**
- Failures: **3**

### Findings by severity

| Severity | Count |
|---|---|
| Critical | 0 |
| High | 1 |
| Medium | 1 |
| Low | 0 |
| Info | 0 |

### Scorecard

- **Detected archetype:** auto → **Marketing site** — No course/event/product-catalog checks applied
- **Pages audited:** 0 → **3** — Homepage + About + Pricing
- **Findings:** 0 → **2** — 1 High, 1 Medium — no Critical

### Overview

Full audit of example.com — a B2B marketing site. Detected archetype: Marketing / corporate brand. Audit scope tailored accordingly. No Critical findings. Two issues worth addressing: one duplicate canonical that blocks ranking on a key page, one missing OG image that hurts social share CTR.

---

## Findings

### 1. [High]  (confidence 95/100) About page canonicalises to homepage — will never rank as a separate page

**ID:** `TSEO-OP-001`  
**Pillars:** SEO | AEO | GEO  
**Category:** On-Page  
**Location:** `—`
  
**Evidence:** `curl -s https://example.com/about | grep -oE '<link rel="canonical"[^>]*>' returns href='https://example.com/' — points to homepage, not self.`

The /about page has <link rel='canonical' href='https://example.com/'> — pointing to the homepage instead of itself. That tells Google the /about URL is a variant of the homepage and shouldn't be indexed as a separate page.

**SEO Audit Finding**

The /about page has a canonical tag pointing to the homepage. Google interprets this as 'this URL is a variant of the homepage — don't index it separately.' Ranking signals from any backlinks to /about flow to the homepage instead.

The result: the /about page cannot rank for queries like 'example about' or 'example team' — Google doesn't index it as a distinct page.

```html
<link rel="canonical" href="https://example.com/">
```

**Revamp Implementation**

Set the canonical to the page's own URL. Every page should self-canonical unless it's explicitly a duplicate of another page.

```html
<link rel="canonical" href="https://example.com/about">
```

**How to verify:** curl -s https://example.com/about | grep -oE '<link rel="canonical"[^>]*>' — href should end with '/about'. Repeat for every non-homepage URL.

---

### 2. [Medium]  (confidence 98/100) Pricing page has no og:image — social shares show default icon

**ID:** `TSEO-OP-002`  
**Pillars:** SEO | AEO  
**Category:** On-Page  
**Location:** `—`
  
**Evidence:** `curl -s https://example.com/pricing returns no og:image meta tag. Social preview falls back to the platform default image.`

When someone shares the pricing page on LinkedIn / Twitter / WhatsApp, the social preview shows the platform's default image (or no image at all), not a branded card. That hurts CTR on shared links.

**SEO Audit Finding**

The pricing page has no &lt;meta property="og:image"&gt; tag. Social platforms fall back to their default image behavior — typically a generic thumbnail or no preview at all.

For a commercial page where shared links drive conversions, this is a small but consistent CTR drain.

```html
<!-- pricing page <head> — og:image missing -->
<meta property="og:title" content="Pricing | Example">
<meta property="og:description" content="...">
<!-- no og:image -->
```

**Revamp Implementation**

Add og:image + og:image:width + og:image:height + og:image:alt. Use an absolute URL (Facebook/LinkedIn reject relative paths).

```html
<meta property="og:image" content="https://example.com/images/og/pricing-og.webp">
<meta property="og:image:width" content="1200">
<meta property="og:image:height" content="630">
<meta property="og:image:alt" content="Example pricing plans">
```

**How to verify:** Paste the pricing URL into https://www.linkedin.com/post-inspector/ — expect a preview with a proper branded image. Repeat on https://developers.facebook.com/tools/debug/ and https://cards-dev.twitter.com/validator.

---
