---
type: decision
title: "Claude Code — Configuración de Autonomía Máxima"
created: 2026-04-28
updated: 2026-04-28
decision_date: 2026-04-28
status: current
tags:
  - claude-code
  - configuracion
  - permisos
  - workflow
related:
  - "[[full-audit-and-system-setup-session]]"
---

# Claude Code — Configuración de Autonomía Máxima

## Decisión

Claude Code se configura para operar con máxima autonomía: ejecuta tareas de corrido sin pedir confirmación en cada paso intermedio. Solo muestra un resumen antes de ejecutar y solicita una única aprobación.

## Cambios realizados

### 1. `~/.claude/settings.json` — permisos globales

Se agrega el bloque `permissions` con `defaultMode: "auto"` y una lista explícita de operaciones auto-aprobadas:

**Auto-aprobado (allow):**
- Bash: `git *`, `npm *`, `npx *`, `node *`, `python *`, `pip *`, `pnpm *`, `bun *`
- Bash: `ls`, `find *`, `grep *`, `cat *`, `head *`, `tail *`, `echo *`
- Bash: `mkdir *`, `touch *`, `cp *`, `mv *`, `open *`, `brew *`
- Bash: `curl *`, `gh *`, `vercel *`, `astro *`, `jq *`, `sed *`, `awk *`, `diff *`, `chmod *`
- Herramientas: `Read`, `Edit`, `Write`, `Glob`, `Grep`, `WebFetch`, `WebSearch`, `Task`

**Siempre bloqueado (deny):**
- `rm -rf *`, `sudo rm *`, `git push --force *`, `git reset --hard *`, `git branch -D *`

### 2. `~/.claude/CLAUDE.md` — instrucción de flujo

Se agrega sección "Autonomía y flujo de ejecución" con la regla:

> 1. Analizar la tarea en silencio  
> 2. Mostrar un único resumen de lo que se va a hacer  
> 3. El usuario aprueba una sola vez → ejecutar todo de corrido  
> 4. Entregar resultado final

Las únicas excepciones donde sí pausar: operaciones destructivas irreversibles, push a remoto, o acciones que afecten sistemas externos.

### 3. Memoria persistente

Se crea `feedback_autonomia_ejecucion.md` en `~/.claude/projects/-Users-carrillo/memory/` para que la preferencia aplique en todas las sesiones futuras.

## Rationale

El usuario concede acceso y consentimiento por adelantado para tareas seguras. Interrumpir en cada herramienta rompe el flujo y es redundante cuando la intención ya está clara desde el mensaje inicial. Las operaciones destructivas irreversibles siguen requiriendo confirmación explícita.

## Scope de la autonomía

| Situación | Comportamiento |
|-----------|---------------|
| Lectura, búsqueda, análisis | Ejecutar sin preguntar |
| Edición de archivos locales | Ejecutar sin preguntar |
| Comandos git de lectura (status, log, diff) | Ejecutar sin preguntar |
| Comandos npm/node/python | Ejecutar sin preguntar |
| Inicio de tarea multi-paso | Mostrar resumen → una aprobación |
| `rm -rf`, push --force, reset --hard | Siempre preguntar |
| Push a remoto, deploy a producción | Siempre preguntar |
| Acciones en sistemas externos (email, APIs) | Siempre preguntar |
