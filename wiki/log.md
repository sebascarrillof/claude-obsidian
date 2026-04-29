---
type: meta
title: "Operation Log"
created: 2026-04-07
updated: 2026-04-08
tags:
  - meta
  - log
status: evergreen
related:
  - "[[index]]"
  - "[[hot]]"
  - "[[overview]]"
  - "[[sources/_index]]"
---

# Operation Log

Navigation: [[index]] | [[hot]] | [[overview]]

Append-only. New entries go at the TOP. Never edit past entries.

## [2026-04-28] save | Generación de Imágenes IA Gratis — Claude Banana + FLUX.1 Workflow
- Type: synthesis
- Location: wiki/questions/generacion-imagenes-ia-gratis-claude-banana-flux.md
- From: instalación claude-banana, fórmula 7 componentes, investigación herramientas gratuitas, generación exitosa con FLUX.1 [dev] vía HF Spaces sin billing

## [2026-04-28] save | Claude Code — Configuración de Autonomía Máxima
- Type: decision
- Location: wiki/meta/claude-code-autonomia-maxima.md
- From: configuración de settings.json (defaultMode auto + allow list), CLAUDE.md (flujo un paso), memoria persistente de preferencia de autonomía

## [2026-04-20] save | Contratos DEPAS — Depa 37, Inquilino Mexicano, Reglas INE
- Type: session
- Location: wiki/meta/contratos-depas-37-mariana-session-2026-04-20.md
- From: Contrato depa 37 (Mariana Medina Reynoso), reglas INE mexicana (OCR trasero), bug títulos intercambiados, template hoja de contacto modificado para inquilino único

## [2026-04-19] save | YouREnergy — Instagram Content + Obsidian Auto-Linking System
- Type: session
- Location: wiki/meta/yourenergy-session-2026-04-19.md
- From: YouREnergy Instagram Canva designs (4 piezas), sistema auto-linking Obsidian Clippings → proyectos, stack evidencia científica Myopulse (Nobel 1991 + Lennox 2002)

Entry format: `## [YYYY-MM-DD] operation | Title`

Parse recent entries: `grep "^## \[" wiki/log.md | head -10`

---

## [2026-04-08] save | claude-obsidian v1.4 Release Session
- Type: session
- Location: wiki/meta/claude-obsidian-v1.4-release-session.md
- From: full release cycle covering v1.1 (URL/vision/delta tracking, 3 new skills), v1.4.0 (audit response, multi-agent compat, Bases dashboard, em dash scrub, security history rewrite), and v1.4.1 (plugin install command hotfix)
- Key lessons: plugin install is 2-step (marketplace add then install), allowed-tools is not valid frontmatter, Bases uses filters/views/formulas not Dataview syntax, hook context does not survive compaction, git filter-repo needs 2 passes for full scrub

## [2026-04-08] ingest | Claude + Obsidian Ecosystem Research
- Type: research ingest
- Source: `.raw/claude-obsidian-ecosystem-research.md`
- Queries: 6 parallel web searches + 12 repo deep-reads
- Pages created: [[claude-obsidian-ecosystem]], [[cherry-picks]], [[claude-obsidian-ecosystem-research]], [[Ar9av-obsidian-wiki]], [[Nexus-claudesidian-mcp]], [[ballred-obsidian-claude-pkm]], [[rvk7895-llm-knowledge-bases]], [[kepano-obsidian-skills]], [[Claudian-YishenTu]]
- Key finding: 16+ active Claude+Obsidian projects; 13 cherry-pick features identified for v1.3.0+
- Top gap confirmed: no delta tracking, no URL ingestion, no auto-commit

## [2026-04-07] session | Full Audit, System Setup & Plugin Installation
- Type: session
- Location: wiki/meta/full-audit-and-system-setup-session.md
- From: 12-area repo audit, 3 fixes, plugin installed to local system, folder renamed

## [2026-04-07] session | claude-obsidian v1.2.0 Release Session
- Type: session
- Location: wiki/meta/claude-obsidian-v1.2.0-release-session.md
- From: full build session — v1.2.0 plan execution, cosmic-brain→claude-obsidian rename, legal/security audit, branded GIFs, PDF install guide, dual GitHub repos

## [2026-04-07] ingest | First source ingest
- Source: `.raw/` (first ingest)
- Pages updated: [[index]], [[log]], [[hot]], [[overview]]
- Key insight: The wiki pattern turns ephemeral AI chat into compounding knowledge — one user dropped token usage by 95%.

## [2026-04-07] setup | Vault initialized

- Plugin: claude-obsidian v1.1.0
- Structure: seed files + first ingest complete
- Skills: wiki, wiki-ingest, wiki-query, wiki-lint, save, autoresearch
