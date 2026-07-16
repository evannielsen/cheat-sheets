---
name: generate-cheat-sheet
description: Create a new developer cheat sheet, write the markdown content with coversheet and card-grid layout, and add it to the README index
---

## What This Skill Does

Generates a complete, styled cheat sheet that renders on the Jekyll-deployed site. It writes the markdown file in `cheatsheets/` and updates `README.md` so the sheet appears in the "Available" list.

## Step 1: Pick the topic

Ask the user what topic to cover. The sheet should be a **quick-reference** — commands, mappings, step-by-step workflows, or comparison tables that people keep open while working. Avoid tutorials or long-form explanations.

## Step 2: Create the markdown file

Write `cheatsheets/<topic-slug>.md`. Use this exact structure:

### Frontmatter (must be first line)

```yaml
---
layout: default
title: Display Title Here
---
```

### Coversheet (required, right after frontmatter)

```html
<div class="coversheet">
  <h1><span class="icon">&#x1F3A4;</span> Topic Name</h1>
  <p>A one-line description of what this sheet covers.</p>
</div>
```

Pick an emoji for the `&#x...;` entity that best represents the topic. See existing sheets for conventions: Git=📖, AWS/Azure=📖, OTel=📈, LLM=🤠, VS Code=🪟.

### Body sections

Use **section headings** to organize content:

```html
<h2 class="section-heading"><span class="icon">&#x1F4D8;</span> Getting Started</h2>
<p style="font-size:.88rem; color: var(--muted); margin-bottom: 1rem;">Brief intro paragraph.</p>
```

Icon recommendations for sections: 📖=overview, 🚀=getting started, ⚙️=configuration, 💡=tips, ❓=FAQ, 🔍=reference, 📝=examples.

#### Content patterns (pick what fits the topic)

**Quick-reference cards** — most common pattern:

```html
<div class="card-grid">
  <div class="card-item">
    <h3><span class="icon">&#x1F4E6;</span> <span class="accent-blue">Category Name</span></h3>
    <ul>
      <li><code>command arg</code> &mdash; What it does</li>
      <li><code>another-command</code> &mdash; Description here</li>
    </ul>
  </div>
  <!-- more card-items -->
</div>
```

**Standalone info cards** — for detailed content:

```html
<div class="card-standalone">
  <h3><span class="icon">&#x2699;&#xFE0F;</span> Configuration</h3>
  <p>Detailed explanation with code blocks.</p>
</div>
```

**Code examples** — with accent-colored comments:

```html
<pre><code><span class="accent-green"># This is a comment</span>
command arg1 arg2
<span class="accent-orange"># this is a warning note</span></code></pre>
```

**Mini-grid for quick tips:**

```html
<div class="mini-grid">
  <div class="mini-item">Tip one-liner here</div>
  <div class="mini-item">Another tip</div>
</div>
```

**Note boxes inside cards:**

```html
<div class="note"><strong>Tip:</strong> Always set this before running commands.</div>
<div class="tip-box"><strong>Tip:</strong> Start with auto-instrumentation for quick results.</div>
<div class="warning-box"><strong>Warning:</strong> Be careful with high cardinality attributes.</div>
```

**Scoring tables:**

```html
<table class="bench-table">
<tr><th>Score Range</th><th>Meaning</th><th>Typical</th></tr>
<tr><td class="score-great">90+</td><td>Excellent</td><td>Model X</td></tr>
<tr><td class="score-good">70&ndash;89</td><td>Good</td><td>Model Y</td></tr>
<tr><td class="score-meh">50&ndash;69</td><td>Adequate</td><td>Model Z</td></tr>
<tr><td class="score-bad">&lt;50</td><td>Poor</td><td>Avoid</td></tr>
</table>
```

**Comparison tables (↔ mapping style):**

```html
<div class="card-grid">
  <div class="card-item">
    <ul>
      <li><strong>Service A</strong> ↔ <strong>Service B</strong></li>
    </ul>
  </div>
</div>
```

### Credits footer (required, at the end)

```html
<p class="credits">Made with <span style="color: var(--accent-pink);">&#x2764;</span> for developers &mdash; keep building! &#x1F680;</p>
```

### CSS classes cheat sheet

| Purpose | Class |
|---------|-------|
| Colored text | `accent-blue`, `accent-green`, `accent-purple`, `accent-orange`, `accent-red`, `accent-cyan`, `accent-pink` |
| Badges | `badge badge-blue`, `badge badge-green`, `badge badge-orange`, `badge badge-red`, `badge badge-purple`, `badge badge-cyan` |
| Scores | `score-great`, `score-good`, `score-meh`, `score-bad` |
| Card grid item | `<div class="card-grid">` + `<div class="card-item">` (inside it) |
| Standalone card | `card-standalone` |
| Left-accent card | `card-accent-left` |
| Tip/Note boxes | `note`, `tip-box`, `warning-box` |
| Mini-grid | `mini-grid` + `mini-item` (inside it) |
| Bar chart row | `chart-row` + `chart-label` + `chart-bar-bg` + `chart-bar-fill` |
| Flow steps | `flow` + `flow-item data-num="N"` + `flow-connector` |
| Two-column | `two-col` |

## Step 3: Update `index.html`

Open `index.html`. Inside the `<div class="cards">`, add a new `<a>` card block. Insert it **alphabetically by sheet name** among the existing cards, or append at the end if you can't determine the sort order easily.

### Card format (copy the style exactly)

```html
  <a href="cheatsheets/<topic-slug>.html" class="card">
    <div class="icon">&#x1F4D6;</div>
    <h2><Topic Name></h2>
    <p><One-line description></p>
  </a>
```

Required values:
- `href`: `cheatsheets/<topic-slug>.html` — must match the file name from Step 2.
- `icon`: a hex entity (e.g. `&#x1F4D6;`) that represents the topic.
- `<Topic Name>`: the display title from the sheet's frontmatter.
- `<One-line description>`: a brief, friendly summary of what the sheet covers.

### Example — adding an "OAuth2" cheat sheet

Find where in the card list it belongs alphabetically, then insert between the surrounding cards:

```html
  <a href="cheatsheets/oauth2-cheatsheet.html" class="card">
    <div class="icon">&#x1F512;</div>
    <h2>OAuth2 Cheatsheet</h2>
    <p>Flows, tokens, and scopes for authentication</p>
  </a>
```

### Important

- **Do NOT update `README.md`** for the index. The `index.html` file is the authoritative list of available cheat sheets. README.md's "Available" section is stale and should be ignored.

## Step 4: Verify

Check these before finishing:

1. **Frontmatter** — `layout: default` and `title:` are present on lines 1-3.
2. **Coversheet** — First HTML element after frontmatter is `<div class="coversheet">`.
3. **Credits footer** — Last non-blank content is `<p class="credits">...</p>`.
4. **No broken CSS classes** — Only use classes listed above; no inline `style=` except on the heart icon and `<pre>` padding backgrounds.
5. **README updated** — The new sheet appears in the "Available" list with correct link path (`cheatsheets/<slug>.html`).
6. **File naming** — Use kebab-case: `azure-aws-cheatsheet`, not `Azure_AWS_Cheatsheet`.

## Gotchas

- **The `_site/` directory is gitignored** — don't edit files there; it's auto-generated by Jekyll.
- **README.md "Available" section is stale** — the real index is `index.html`. Never update README for sheet registration.
- **"Getting Started with VS Code Extensions" exists in README but not on disk** — known gap. Don't create a file for it unless explicitly asked; it may be intentionally removed.
- **The azure-aws-cheatsheet IS in `index.html`** (unlike the README index) — no mismatch here. The skill's Step 3 will correctly include it if you're adding new sheets alongside it.
- **No `_includes/head.html` file exists** — the README mentions it, but CSS lives entirely in `_layouts/default.html`. Use classes defined there.
