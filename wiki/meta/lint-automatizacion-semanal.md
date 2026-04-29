---
type: decision
title: "Wiki Lint — Automatización Semanal con Claude Code Remote"
created: 2026-04-28
updated: 2026-04-28
decision_date: 2026-04-28
status: active
tags:
  - automatizacion
  - wiki
  - github
  - claude-code
  - routine
related:
  - "[[meta/claude-code-autonomia-maxima]]"
  - "[[meta/lint-report-2026-04-28]]"
---

# Wiki Lint — Automatización Semanal con Claude Code Remote

## Decisión

El wiki lint se ejecuta automáticamente cada lunes a las 9:00 AM hora Mérida (15:00 UTC) mediante un agente remoto de Claude Code (CCR — Claude Code Remote). El agente escanea, autocorrige, genera reporte y hace push — sin intervención humana.

## Rutina configurada

| Campo | Valor |
|-------|-------|
| **Routine ID** | `trig_017ZaJrA39655maDk5ELyvCs` |
| **Cron** | `0 15 * * 1` (lunes 9 AM Mérida) |
| **Modelo** | claude-sonnet-4-6 |
| **Repo** | `github.com/sebascarrillof/claude-obsidian` |
| **Próxima ejecución** | 2026-05-04 |

Administrar en: `https://claude.ai/code/routines/trig_017ZaJrA39655maDk5ELyvCs`

## Stack de credenciales

El agente remoto corre en la nube de Anthropic sin acceso a credenciales locales. La solución:

1. **GitHub CLI (`gh`)** instalado vía `brew install gh`
2. **Autenticación**: cuenta `sebascarrillof` con OAuth token `gho_*` (scopes: `repo`, `gist`, `workflow`)
3. **Fork**: `github.com/sebascarrillof/claude-obsidian` — propiedad del usuario, write access total
4. **Token embebido en URL**: `https://TOKEN@github.com/sebascarrillof/claude-obsidian` en el campo `sources` del job_config

El repo original `AgriciDaniel/claude-obsidian` solo tenía acceso READ para la cuenta. El fork resuelve el problema sin depender del propietario original.

## Lo que hace el agente cada lunes

1. **Configura identidad git** (`user.email`, `user.name`)
2. **Escanea** `wiki/` buscando: páginas huérfanas, links muertos, frontmatter incompleto, entradas stale en index, secciones vacías
3. **Autocorrige** (sin preguntar): frontmatter gaps, entradas stale en index.md, links muertos en index/log
4. **Genera reporte** en `wiki/meta/lint-report-YYYY-MM-DD.md`
5. **Actualiza** `wiki/index.md` (fecha + conteo de páginas)
6. **Añade entrada** al top de `wiki/log.md`
7. **Commit + push** a `origin main` (con rebase automático si hay divergencia)

## Resolución de merge conflict (setup inicial)

Al sincronizar el fork, el upstream (`AgriciDaniel/claude-obsidian`) tenía v1.6.0 con DragonScale features — mucho más avanzado que la copia local. Conflictos resueltos:

- `.claude-plugin/marketplace.json` → se tomó la versión upstream (más nueva)
- `wiki/hot.md` → se tomó la versión upstream (v1.6.0 context)
- `wiki/index.md` → merge manual: fecha local (2026-04-28), conteo real (52 páginas), secciones de ambas versiones preservadas

## Por qué fork y no deploy key

Un deploy key SSH requeriría generar un par de llaves, subir la pública a GitHub y guardar la privada en el entorno CCR — más pasos y mayor superficie de ataque. El OAuth token con scope `repo` embebido en la URL HTTPS es el método más simple y directamente soportado por git.

## Qué NO autocorrige el agente

- Páginas huérfanas (pueden estar aisladas intencionalmente)
- Secciones vacías (pueden ser placeholders activos)
- Borrado de archivos (nunca)

Estos casos quedan documentados en el reporte para revisión manual.
