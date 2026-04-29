---
type: session
title: "YouREnergy — Instagram Content + Obsidian Auto-Linking System"
created: 2026-04-19
updated: 2026-04-19
tags:
  - session
  - yourenergy
  - canva
  - obsidian
  - auto-linking
  - microcorriente
status: evergreen
related:
  - "[[hot]]"
  - "[[index]]"
---

# YouREnergy — Instagram Content + Obsidian Auto-Linking System

Session: 2026-04-19. Project: YouREnergy (spa regenerativo, Mérida). Two main outputs: Canva Instagram designs completed, and an Obsidian auto-linking system built for project knowledge management.

---

## 1. Canva Instagram Designs — Completed

Four pieces produced using Canva MCP (`start-editing-transaction` → `perform-editing-operations` → `commit-editing-transaction`):

| Pieza | Canva URL | Estado |
|-------|-----------|--------|
| ATP Carrusel (microcorriente) | https://www.canva.com/d/7_U1isIdOi0aM9q | Guardado |
| Microcorriente Carrusel (portada) | https://www.canva.com/d/C0_6Ohp0SwpIKD1 | Guardado |
| Lifting Facial — Post Único | https://www.canva.com/d/wYZ_yRdeOU-nrlx | Guardado |
| 5 Señales (post único) | https://www.canva.com/d/eyf1tE2cLa54ZU9 | Guardado |

### Key Canva MCP Patterns

- `generate-design` creates only 1-page designs — true multi-page carousels must be built manually in Canva from a cover page
- When generation quota is exhausted, use `create-design-from-candidate` + editing transactions on existing candidates
- Font size reduction via `format_text` with `list_level: 0` is required to remove auto-numbering before replacing list text
- Upload logos via `upload-asset-from-url` using Vercel deployment URLs, then use `update_fill` / `insert_fill`
- MCP connection loss invalidates open transactions — always restart with `start-editing-transaction` on the same `design_id`

### Brand Rules (YouREnergy)

- Color: teal `#0d9488`
- Never mention "Acuscope" — only "Myopulse"
- Phone: (999) 366-9418
- Instagram: @yourenergy.mx
- Location: Temozon Norte, Mérida
- Tagline: "CONVIÉRTETE EN TU MEJOR VERSIÓN"

---

## 2. Obsidian Auto-Linking System — Built

### Problem

When the user downloads competitor or research content via Obsidian Web Clipper into `Clippings/`, the notes land without connection to any project. Context is lost.

### Solution

Three-layer system added to `cerebro-digital` vault (`_CLAUDE.md`):

**Layer 1 — Frontmatter tagging:** Add `project: ProjectName` + relevant tags (`competidor`, `spa`, `investigacion`) to every clipping.

**Layer 2 — Wikilink header:** Add `> Vinculado a [[Projects/X/X]]` at the top of each clipping.

**Layer 3 — Project table:** Maintain a `## Competidores Analizados` (or equivalent) section in the project's main note, with one row per linked clipping.

### Classification Rules (in `_CLAUDE.md`)

| Keywords in content | Project |
|---|---|
| spa, masaje, terapia, facial, microcorriente, regeneración | YouREnergy |
| retiro, meditación, yoga, holístico, naturaleza | Vive Retreats |
| agencia, automatización, chatbot, landing, funnel | Agencia Automatización Web |
| renta, departamento, arrendamiento, inquilino | La Sexta / Contratos DEPAS |

### Competitors Linked This Session

Three Instagram competitor accounts linked to YouREnergy:
- `@zamma_spa` (1.3K followers) — spa masajes + faciales, CDMX
- `@helaspamexico` (45K followers) — spa premium, CDMX
- `@desertika.spa` (11K followers) — spa urbano, 15 sucursales, CDMX

---

## 3. Scientific Evidence Stack — Built for YouREnergy

Two peer-reviewed sources saved to `Projects/YouREnergy/`:

### Lennox et al. 2002 — Clinical Study with Electro-Myopulse 75F

Published in *Int. J. Radiation Oncology Biology Physics*, Vol. 54, No. 1, pp. 23-34.

Uses the exact **Electro-Myopulse 75F** instrument. Results on 26 patients with radiation-induced fibrosis:
- 92% improved cervical rotation
- 85% improved extension/flexion
- 81% improved lateral flexion
- Benefits sustained at 3-month follow-up. Zero adverse effects.

Mechanism: microcurrent activates voltage-sensitive calcium ion channels → increased intracellular calcium → ATP synthesis → protein synthesis → cellular repair.

### Nobel Prize 1991 — Neher & Sakmann (Ion Channels)

Nobel Prize in Physiology or Medicine 1991 for discovering ion channel function and developing patch-clamp technique.

Connection to Myopulse: the Myopulse delivers fast-rise-time pulses that activate voltage-sensitive sodium and calcium ion channels — the exact structures the Nobel was awarded for discovering. This provides Nobel-level scientific grounding for why microcurrent therapy works.

**Marketing angle:** "La ciencia detrás del Myopulse tiene Premio Nobel."

### Combined Argument

The Nobel explains the mechanism (ion channels → ATP → cellular repair). The Lennox study proves the clinical outcome with the actual Myopulse instrument. Together they form a complete scientific case: Nobel explains *why*, Lennox study proves *results*.

---

## Files Created / Modified

| File | Action |
|---|---|
| `cerebro-digital/Projects/YouREnergy/Evidencia Científica — Microcorriente y Fibrosis (Lennox 2002).md` | Created |
| `cerebro-digital/Projects/YouREnergy/Evidencia Científica — Premio Nobel 1991 Canales Iónicos (Neher & Sakmann).md` | Created |
| `cerebro-digital/Projects/YouREnergy/YouREnergy.md` | Updated (competidores + evidencia) |
| `cerebro-digital/_CLAUDE.md` | Updated (auto-linking rules) |
| `cerebro-digital/Clippings/Zammá Spa...md` | Tagged + linked |
| `cerebro-digital/Clippings/Hela Home...md` | Tagged + linked |
| `cerebro-digital/Clippings/Desértika Spa...md` | Tagged + linked |
