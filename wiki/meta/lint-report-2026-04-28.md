---
type: meta
title: "Wiki Lint Report — 2026-04-28"
created: 2026-04-28
updated: 2026-04-28
tags:
  - meta
  - lint
  - health-check
status: evergreen
related:
  - "[[index]]"
  - "[[dashboard]]"
  - "[[log]]"
---

# Wiki Lint Report — 2026-04-28

Run date: 2026-04-28 | Scope: full wiki (`wiki/`)

---

## Summary

- Pages scanned: 31
- Issues found: 23 (2 critical, 10 warnings, 11 suggestions)
- Auto-fix run: 2026-04-28 | Fixed: 13 issues (2 critical, 10 warnings, 1 suggestion)

---

## Critical (must fix)

### C-1. Dead wikilink — `[[AI Marketing Hub Cover Images Canvas]]` — FIXED 2026-04-28

- Affected page: [[overview]]
- Problem: `overview.md` line 60 links to `[[AI Marketing Hub Cover Images Canvas]]`. No canvas or markdown file with that name exists anywhere in the vault. This is a broken reference.
- Fix applied: Removed the entire line referencing `[[AI Marketing Hub Cover Images Canvas]]` from `overview.md`. The `## Canvases` section now only lists `[[claude-obsidian-presentation]]`, which resolves correctly.

### C-2. Dead wikilink — `[[Wiki Map]]` (linked from 5 pages as `.md`, resolves to `.canvas`) — FIXED 2026-04-28

- Affected pages: [[index]], [[hot]], [[getting-started]], [[concepts/_index]], and the `hot.md` `related:` frontmatter
- Problem: All five locations link `[[Wiki Map]]` expecting a Markdown page. The file that exists is `wiki/Wiki Map.canvas`.
- Fix applied: Created `wiki/Wiki Map.md` — a thin stub page that describes the canvas and embeds it with `![[Wiki Map.canvas]]`. The wikilink now resolves to a queryable Markdown file. Related frontmatter in `index.md` and `getting-started.md` already referenced `[[Wiki Map]]` and now resolve correctly.

---

## Warnings (should fix)

### W-1. Frontmatter missing `created` field — 8 pages — FIXED 2026-04-28

The following pages had all other required fields but were missing `created:`.

| Page | Fix |
|------|-----|
| [[index]] | Added `created: 2026-04-07` |
| [[hot]] | Added `created: 2026-04-07` |
| [[log]] | Added `created: 2026-04-07` |
| [[getting-started]] | Added `created: 2026-04-07` |
| [[meta/dashboard]] | Already had `created: 2026-04-07` — no change needed |
| [[concepts/_index]] | Added `created: 2026-04-07` |
| [[entities/_index]] | Added `created: 2026-04-07` |
| [[sources/_index]] | Added `created: 2026-04-07` |

### W-2. `entities/_index` is missing 6 of 7 entity pages — FIXED 2026-04-28

- Affected page: [[entities/_index]]
- Problem: Only `[[Andrej Karpathy]]` was listed under `## People`. The six ecosystem entity pages were not listed.
- Fix applied: Added `## Repos & Plugins` section to `entities/_index.md` listing all 6 repos: [[Ar9av-obsidian-wiki]], [[Nexus-claudesidian-mcp]], [[ballred-obsidian-claude-pkm]], [[rvk7895-llm-knowledge-bases]], [[kepano-obsidian-skills]], [[Claudian-YishenTu]]. Updated `related:` frontmatter to include all 6.

### W-3. `sources/_index` has no entries — FIXED 2026-04-28

- Affected page: [[sources/_index]]
- Problem: All section were placeholder comments. `[[claude-obsidian-ecosystem-research]]` was not listed.
- Fix applied: Added `[[claude-obsidian-ecosystem-research]]` under `## Articles`. Kept `## Transcripts` and `## Papers` as placeholders with comments. Updated `related:` frontmatter to include the source. Updated `updated:` to 2026-04-28.

### W-4. Stale index entry — `[[Wiki Map]]` in `index.md` frontmatter and navigation

- Affected page: [[index]]
- Problem: See C-2. Resolved by creation of `wiki/Wiki Map.md`.
- Status: Resolved by C-2 fix.

### W-5. `overview.md` counters stale — FIXED 2026-04-28

- Affected page: [[overview]]
- Problem: "Wiki pages: 26" and "Last activity: 2026-04-08".
- Fix applied: Updated `## Current State` to "Wiki pages: 31" and "Last activity: 2026-04-28". Also updated frontmatter `updated: 2026-04-28`.

### W-6. `questions/How does the LLM Wiki pattern work` status is `developing` — FIXED 2026-04-28

- Affected page: [[How does the LLM Wiki pattern work]]
- Problem: Status was `developing` but `answer_quality` is `definitive`.
- Fix applied: Changed `status: developing` to `status: mature`. Updated `updated: 2026-04-28`.

### W-7. `overview.md` page count and last activity stale — FIXED 2026-04-28

- Affected page: [[overview]]
- See W-5 — resolved in the same fix.

### W-8. `index.md` total page count incorrect — FIXED 2026-04-28

- Affected page: [[index]]
- Problem: Header read "Total pages: 30".
- Fix applied: Updated header to "Total pages: 31". Updated `created: 2026-04-07` also added (W-1).

### W-9. `meta/claude-code-autonomia-maxima.md` uses non-standard `status: active` — FIXED 2026-04-28

- Affected page: [[meta/claude-code-autonomia-maxima]]
- Problem: `status: active` is not in the standard vocabulary.
- Fix applied: Changed to `status: current`.

### W-10. `log.md` entry [2026-04-07] ingest has no title — FIXED 2026-04-28

- Affected page: [[log]]
- Problem: Lines 72-75 were orphaned bullet points with no preceding heading.
- Fix applied: Added `## [2026-04-07] ingest | First source ingest` heading before the orphaned lines. The entry now follows the standard log format.

---

## Suggestions (worth considering)

### S-1. No dedicated page for `defuddle` — mentioned 23 times

- Referenced in: [[cherry-picks]], [[claude-obsidian-ecosystem]], [[kepano-obsidian-skills]], [[claude-obsidian-v1.4-release-session]], [[sources/claude-obsidian-ecosystem-research]]
- Problem: `defuddle` is mentioned 23 times across 5+ pages as a key tool, but there is no dedicated concept or entity page for it.
- Suggested fix: Create `wiki/entities/defuddle.md` or `wiki/concepts/defuddle.md` to centralize what it is, how to install it, and its role in the ingest pipeline.

### S-2. No dedicated page for `Obsidian Bases` — mentioned 11 times

- Referenced in: [[cherry-picks]], [[claude-obsidian-ecosystem]], [[kepano-obsidian-skills]], [[claude-obsidian-v1.4-release-session]], [[meta/dashboard]]
- Problem: Obsidian Bases is a major platform feature the vault depends on. It has no concept page.
- Suggested fix: Create `wiki/concepts/Obsidian Bases.md`.

### S-3. No dedicated page for `FLUX.1` — mentioned 10 times

- Referenced in: [[questions/generacion-imagenes-ia-gratis-claude-banana-flux]]
- Problem: FLUX.1 [dev] is the primary image generation model described in the question page, but has no entity page.
- Suggested fix: Create `wiki/entities/FLUX.1.md`.

### S-4. No dedicated page for `Marp` — mentioned 10 times

- Referenced in: [[cherry-picks]], [[claude-obsidian-ecosystem]], [[rvk7895-llm-knowledge-bases]], [[claude-obsidian-v1.4-release-session]]
- Problem: Marp is listed as a feature to add in multiple pages but has no concept page.
- Suggested fix: Create `wiki/concepts/Marp.md`.

### S-5. No dedicated page for `Myopulse` — mentioned 9 times

- Referenced in: [[meta/yourenergy-session-2026-04-19]], [[hot]]
- Problem: The Myopulse device is mentioned 9 times across two pages but has no entity page.
- Suggested fix: Create `wiki/entities/Myopulse.md`.

### S-6. No dedicated page for `Claude Banana` — mentioned 7 times

- Referenced in: [[questions/generacion-imagenes-ia-gratis-claude-banana-flux]]
- Problem: Claude Banana is the primary tool documented in the question page but has no entity page.
- Suggested fix: Create `wiki/entities/Claude Banana.md`.

### S-7. No dedicated page for `obsidian-memory-mcp` — mentioned 4 times

- Referenced in: [[cherry-picks]], [[claude-obsidian-ecosystem]], [[Nexus-claudesidian-mcp]]
- Problem: `obsidian-memory-mcp` is cherry-pick #11 and mentioned across 3 pages but has no entity page.
- Suggested fix: Create `wiki/entities/obsidian-memory-mcp.md`.

### S-8. No dedicated page for `ekadetov/llm-wiki` — mentioned 3 times

- Referenced in: [[cherry-picks]] (twice), [[claude-obsidian-ecosystem-research]]
- Problem: All 6 other ecosystem repos have entity pages, but `ekadetov/llm-wiki` does not.
- Suggested fix: Create `wiki/entities/ekadetov-llm-wiki.md`.

### S-9. No dedicated page for `JSON Canvas` — mentioned 3 times

- Referenced in: [[kepano-obsidian-skills]], [[claude-obsidian-v1.4-release-session]], [[claude-obsidian-ecosystem]]
- Problem: JSON Canvas is a spec the canvas skill depends on but has no concept page.
- Suggested fix: Create `wiki/concepts/JSON Canvas.md`.

### S-10. `concepts/_index` has duplicate entries in `related:` frontmatter — FIXED 2026-04-28

- Affected page: [[concepts/_index]]
- Problem: `related:` list included `[[LLM Wiki Pattern]]`, `[[Hot Cache]]`, and `[[Compounding Knowledge]]` twice each.
- Fix applied: Removed the three duplicate entries. The `related:` array now has one entry per link.

### S-11. `cherry-picks.md` `[[wikilinks]]` appears as a dead wikilink in raw parsing

- Affected page: [[cherry-picks]]
- Problem: Line 107 contains `[[wikilinks]]` inside backticks. Obsidian does NOT render it as a real link. External link checkers that don't strip code spans may flag it.
- Suggested fix: No action needed. The current text is intentional.

---

## Auto-fix Status

Auto-fix run completed 2026-04-28. Summary of changes:

| Issue | File(s) Modified | Change |
|-------|-----------------|--------|
| C-1 | `wiki/overview.md` | Removed dead `[[AI Marketing Hub Cover Images Canvas]]` link |
| C-2 | `wiki/Wiki Map.md` (new) | Created stub page embedding `Wiki Map.canvas` |
| W-1 | `wiki/index.md`, `wiki/hot.md`, `wiki/log.md`, `wiki/getting-started.md`, `wiki/concepts/_index.md`, `wiki/entities/_index.md`, `wiki/sources/_index.md` | Added `created: 2026-04-07` to frontmatter |
| W-2 | `wiki/entities/_index.md` | Added `## Repos & Plugins` section with all 6 ecosystem repos; updated `related:` |
| W-3 | `wiki/sources/_index.md` | Added `[[claude-obsidian-ecosystem-research]]` under `## Articles`; updated `related:` |
| W-5 | `wiki/overview.md` | Updated page count to 31 and last activity to 2026-04-28 |
| W-6 | `wiki/questions/How does the LLM Wiki pattern work.md` | Changed `status: developing` to `status: mature` |
| W-8 | `wiki/index.md` | Updated header to "Total pages: 31" |
| W-9 | `wiki/meta/claude-code-autonomia-maxima.md` | Changed `status: active` to `status: current` |
| W-10 | `wiki/log.md` | Added `## [2026-04-07] ingest | First source ingest` heading to orphaned entry |
| S-10 | `wiki/concepts/_index.md` | Removed 3 duplicate entries from `related:` frontmatter |

Remaining open: S-1 through S-9 (concept/entity stub pages) and S-11 (no action needed).

---

## Appendix: Pages Scanned

| Page | Status | Last Updated | Age (days) |
|------|--------|-------------|------------|
| [[index]] | evergreen | 2026-04-07 | 21 |
| [[hot]] | evergreen | 2026-04-08 | 20 |
| [[log]] | evergreen | 2026-04-08 | 20 |
| [[overview]] | developing | 2026-04-07 | 21 |
| [[getting-started]] | evergreen | 2026-04-07 | 21 |
| [[meta/dashboard]] | evergreen | 2026-04-08 | 20 |
| [[meta/claude-code-autonomia-maxima]] | current | 2026-04-28 | 0 |
| [[meta/claude-obsidian-v1.2.0-release-session]] | evergreen | 2026-04-07 | 21 |
| [[meta/claude-obsidian-v1.4-release-session]] | evergreen | 2026-04-08 | 20 |
| [[meta/full-audit-and-system-setup-session]] | evergreen | 2026-04-07 | 21 |
| [[meta/contratos-depas-37-mariana-session-2026-04-20]] | evergreen | 2026-04-20 | 8 |
| [[meta/yourenergy-session-2026-04-19]] | evergreen | 2026-04-19 | 9 |
| [[concepts/_index]] | evergreen | 2026-04-07 | 21 |
| [[concepts/LLM Wiki Pattern]] | mature | 2026-04-07 | 21 |
| [[concepts/Hot Cache]] | mature | 2026-04-07 | 21 |
| [[concepts/Compounding Knowledge]] | mature | 2026-04-07 | 21 |
| [[concepts/cherry-picks]] | current | 2026-04-08 | 20 |
| [[entities/_index]] | evergreen | 2026-04-07 | 21 |
| [[entities/Andrej Karpathy]] | mature | 2026-04-07 | 21 |
| [[entities/Ar9av-obsidian-wiki]] | current | 2026-04-08 | 20 |
| [[entities/Nexus-claudesidian-mcp]] | current | 2026-04-08 | 20 |
| [[entities/ballred-obsidian-claude-pkm]] | current | 2026-04-08 | 20 |
| [[entities/rvk7895-llm-knowledge-bases]] | current | 2026-04-08 | 20 |
| [[entities/kepano-obsidian-skills]] | current | 2026-04-08 | 20 |
| [[entities/Claudian-YishenTu]] | current | 2026-04-08 | 20 |
| [[sources/_index]] | evergreen | 2026-04-07 | 21 |
| [[sources/claude-obsidian-ecosystem-research]] | current | 2026-04-08 | 20 |
| [[comparisons/Wiki vs RAG]] | mature | 2026-04-07 | 21 |
| [[comparisons/claude-obsidian-ecosystem]] | current | 2026-04-08 | 20 |
| [[questions/How does the LLM Wiki pattern work]] | mature | 2026-04-28 | 0 |
| [[questions/generacion-imagenes-ia-gratis-claude-banana-flux]] | developing | 2026-04-28 | 0 |
