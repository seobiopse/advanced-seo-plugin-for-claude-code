# Advanced SEO & VDS Audit Toolkit (Tools-to-Use Guide)

This guide documents the core toolset required to execute high-fidelity Visibility-to-Demand System (VDS), SEO, AEO, and GEO audits. These tools allow the auditing agent to interact with live web elements, retrieve competitive market intelligence, and output standardized technical reports.

---

## 1. Browser-Specific Audits via Playwright

To capture dynamic client-side renders, analyze hydration loops, and simulate crawl behavior across different browser viewports (mobile, tablet, desktop) and user-agents, the agent uses **Playwright**.

### 📦 Setup & Installation
Run the following commands in the workspace to set up the browser automation layer:

```bash
# Initialize Playwright in the project
npm init playwright@latest -- --yes --quiet --browser=chromium

# Or install playwright directly as a dependency
npm install -D playwright

# Install browser binaries
npx playwright install chromium
```

### 🤖 Sample Automation Script
Use this script template to capture raw vs. rendered HTML and take screenshots under simulated bots:

```javascript
const { chromium } = require('playwright');

(async () => {
  const browser = await chromium.launch({ headless: true });
  const context = await browser.newContext({
    userAgent: 'Mozilla/5.0 (compatible; Googlebot/2.1; +http://www.google.com/bot.html)',
    viewport: { width: 375, height: 812 }, // Mobile viewport
    isMobile: true
  });
  
  const page = await context.newPage();
  
  // Navigate to target domain
  await page.goto('http://localhost:8000', { waitUntil: 'networkidle' });
  
  // Extract rendered DOM and screenshot
  const renderedHTML = await page.content();
  await page.screenshot({ path: './screenshots/mobile-viewport.png', fullPage: true });
  
  console.log("Rendered HTML length:", renderedHTML.length);
  await browser.close();
})();
```

---

## 2. Model Context Protocol (MCP) Integrations

Model Context Protocol (MCP) allows the LLM agent to connect directly to professional SEO platforms and desktop crawlers to audit technical parameters, search visibility, backlink networks, and AI search presence.

### 🔗 Core MCP Servers to Install
Add these servers to your `.claude-plugin/manifest.json` or local Claude Code config:

- **Ahrefs MCP Server**
  - **Purpose:** Connects backlink authority profiling, page-level crawl status, search index errors, and keyword rankings directly to the chat context.
  - **Reference:** [Ahrefs Developer Portal / MCP Server](https://github.com/ahrefs/mcp-server-ahrefs)
- **Semrush MCP Server**
  - **Purpose:** Query search volumes, domain analytics, keyword difficulty, intent categorization, and organic visibility scores.
  - **Reference:** [Semrush API / MCP Connector](https://github.com/semrush/mcp-server-semrush)
- **Screaming Frog Crawler MCP Server**
  - **Purpose:** Automate site crawls to isolate XML sitemap gaps, redirection loops (301 chains), 404 targets, missing metadata, and invalid header sizes.
  - **Reference:** [Screaming Frog CLI Integration Guide](https://github.com/mcp-community/mcp-screamingfrog)

---

## 3. Public Search Analytics & Scraping Opportunities

When API keys are unavailable, the agent can leverage public analytics URLs. By dynamically replacing target domain query parameters, the browser automation layer can scrape ranking summaries, search traffic volumes, and page-level statistics.

### 📊 Semrush Public Analytics
Semrush exposes public domain overview analytics that can be fetched by substituting the target domain in the URL query string:

- **URL Pattern:**
  `https://www.semrush.com/analytics/overview/?searchType=domain&q=https%3A%2F%2F{target_domain}`
- **Example for Girish Kumar G:**
  `https://www.semrush.com/analytics/overview/?searchType=domain&q=https%3A%2F%2Fgirishkumarg.com`

**Automation Rule:** To retrieve organic traffic curves, ranking keywords, and referring domains without an API key, instruct Playwright to navigate to this public URL, wait for the metrics charts to render, and extract screenshot elements or read JSON responses via network requests.

---

## 4. Report Formatting & Template Standardization

Every completed VDS/SEO audit must be compiled into both **Markdown** and **HTML** formats. To maintain a premium look and consistent ticketing structure, follow the templates configured in the plugin assets.

### 📝 Markdown Audit File (.md)
Standardized for developer tickets and task backlogs.
- **Header:** Include target URL, date, stack, and auditor metadata.
- **Body:** Document issues grouped by severity (Critical, High, Medium, Low, Info) pairing **broken code** side-by-side with **fixed code** examples.
- **Footer:** Append the mandatory VDS/SEO signature blocks as defined in the `references/signature.md` guide.

### 🎨 Interactive HTML Report (.html)
Standardized for client-facing dashboards.
- **TOC Sidebar & Progress Bar:** Include a sticky progress counter showing completed tasks (`X of Y addressed`).
- **Interactive Checklists:** Every finding card must have a tick-box that persists the resolved state to browser `localStorage`.
- **Developer Snippets:** Embed code blocks with copy-to-clipboard buttons and clear `How to verify` guidelines.
- **Brand Signature Band:** Ensure the footer renders the signature:
  `Crafted with care by Giriish · Father of SEO · Want to colaborate (http://t.me/spcgbot)`
