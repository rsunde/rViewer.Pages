# AGENTS.md

Single source of truth for **every** AI coding agent on this repository — Claude Code, OpenAI
Codex, Cursor, GitHub Copilot, Gemini CLI, Windsurf, Aider, etc. Edit **this** file; the
tool-specific files (`CLAUDE.md`, `GEMINI.md`, `.cursor/rules/`, `.github/copilot-instructions.md`,
`.windsurfrules`) are thin pointers that import or defer to it. Keep it concise — instructions,
not full docs.

---

## 1. Project Overview

- **rViewer.Pages** — the companion GitHub Pages site for the [rViewer](../rViewer) project.
  Currently a near-empty placeholder: `index.md` is a single "Welcome to rViewer" heading, nothing
  else.
- **Stack**: Jekyll static site, served via GitHub's classic Pages build pipeline (no GitHub
  Actions workflow, no `Gemfile`/`Gemfile.lock` — Ruby/Jekyll versions are unpinned). Theme:
  `jekyll-theme-architect` (set in `_config.yml`, one of the themes the `github-pages` gem
  supports natively).
- **Layout**: only `_config.yml` (theme selection) and `index.md` (the sole page) exist. No
  `_layouts/`, `_includes/`, `_posts/`, `_data/`, `assets/`, or `CNAME`. Repo only has a
  `gh-pages` branch (no `main`).

---

## 2. Commands

```bash
# No Gemfile exists yet — set one up before serving locally:
bundle init
# add: gem "github-pages", group: :jekyll_plugins
bundle install
bundle exec jekyll serve   # http://localhost:4000
```

Deploy is GitHub's legacy/classic Pages pipeline, auto-triggered on push to `gh-pages` — there is
no in-repo build/deploy script to quote (`.github/` has no `workflows/`, only
`copilot-instructions.md`).

---

## 3. Architecture

Trivial today: `_config.yml` selects the `jekyll-theme-architect` theme, which supplies the
default layout GitHub Pages injects since no `_layouts/` override exists in this repo;
`index.md` is the only rendered page and implicitly uses that theme's default layout. A content
change today means editing `index.md` or adding new `.md` pages at the root or in new
directories — there is no theme-override or include infrastructure to touch yet. If this site
grows real content, expect to add a `Gemfile`, `_layouts/`, and possibly a GitHub Actions deploy
workflow at that point.

---

## 4. Conventions

- Write clean, modern, readable code. Prioritise readability and maintainability.
- Explain complex logic or significant architectural decisions.
- Keep markup semantic and assets organised.

---

## 5. Rules (non-negotiable — these override default agent behaviour)

1. **Source of Truth**: this `AGENTS.md` is the single source of truth. Make all changes here,
   never in the pointer files.
2. **No root clutter**: don't create temporary files in the repo root; clean up after yourself.
3. **Safety**: never delete data or implementation files (or delete markdown content) without
   explicit confirmation. Prefer moving superseded files aside over deleting them.
4. **Delegate to sub-agents** for any multi-step or multi-file work. Reserve the main thread for
   orchestration — planning, dispatching, summarising. The conductor, not the player.

---

## 6. Testing & Definition of Done

A feature isn't done when it compiles — it's done when it builds, tests pass, and the
docs/README reflect it.

- No test suite exists (static Jekyll site) — "done" means: `bundle exec jekyll build` (or
  `jekyll serve`) completes without errors and the page renders correctly, no new root-level
  clutter.

---

## 7. Do-not-touch / gotchas

- No `Gemfile`/`Gemfile.lock` — Jekyll/Ruby versions are unpinned and unverified; don't assume a
  specific version without checking what GitHub's `github-pages` gem currently supports.
- `README.md` is generic boilerplate unrelated to this project's actual purpose — don't treat it
  as authoritative content.
- A prior `AGENTS.md` existed and was explicitly deleted in this repo's most recent commit before
  this file was regenerated — if content conflicts with git history, the history is stale, not a
  signal to revert this file.
- If a local Jekyll build/serve is run, watch for a generated `_site/` output directory — it is
  **not** currently listed in `.gitignore` (only `.claude/settings.local.json` is, added by this
  task), so don't accidentally commit build artifacts.
