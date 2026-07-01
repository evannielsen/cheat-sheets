# Cheat Sheets

Quick-reference guides for developers, built with Jekyll and deployed via GitHub Pages.

## Available

- [**Git Cheatsheet**](cheatsheets/git-cheatsheet.html) — Beginner-friendly reference for version control. Print it out and keep it on your desk!
- [**LLM Benchmark & Model Selection Cheatsheet**](cheatsheets/llm-benchmark-cheatsheet.html) — Understand benchmarks, pick the right model for your task — Ollama & Hugging Face edition.

## Writing New Sheets

Each cheatsheet is a `.md` file in `cheatsheets/` with:

```yaml
---
layout: default
title: Sheet Title
---
```

The shared layout (`_layouts/default.html`) and centralized CSS are embedded via `_includes/head.html`. Use any of the CSS classes defined there (badges, cards, charts, tables) — no inline styles needed.

### Classes Cheat Sheet

| Category | Classes |
|----------|---------|
| Colored text | `accent-blue`, `accent-green`, `accent-purple`, `accent-orange`, `accent-red`, `accent-cyan`, `accent-pink` |
| Badges | `badge badge-blue`, `badge badge-green`, `badge badge-orange`, `badge badge-red`, `badge badge-purple`, `badge badge-cyan` |
| Scoring | `score-great`, `score-good`, `score-meh`, `score-bad` |
| Boxes | `card-grid .card-item`, `card-standalone`, `card-accent-left`, `note`, `tip-box`, `warning-box` |
| Grids | `mini-grid .mini-item`, `two-col` |
| Charts | `chart-row`, `chart-label`, `chart-bar-bg`, `chart-bar-fill`, `chart-desc` |
| Flow steps | `flow`, `flow-item data-num="N"`, `flow-connector` |
| Typography | Standard markdown (`#`, `**bold**`, ``code``, tables, lists) + HTML `<span class="model-tag">` for model names |

## Deployment

Deployed via GitHub Pages (Jekyll). All content is authored in Markdown with CSS classes applied via inline HTML. Push to `main` and the site rebuilds automatically.
