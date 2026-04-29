---
type: synthesis
title: "Generación de Imágenes IA Gratis — Claude Banana + FLUX.1 Workflow"
created: 2026-04-28
updated: 2026-04-28
tags:
  - ia-generativa
  - imagenes
  - video
  - workflow
  - gratis
  - claude-banana
  - flux
status: developing
related:
  - "[[claude-code-autonomia-maxima]]"
question: "¿Cómo generar imágenes y video con IA de forma gratuita, con prompts profesionales?"
answer_quality: solid
---

# Generación de Imágenes IA Gratis — Claude Banana + FLUX.1 Workflow

## Claude Banana — Motor de Prompts

**Repo:** `~/claude-banana` (clonado de `github.com/Hainrixz/claude-banana`)

Claude Banana es un agente de prompt engineering para imágenes. No genera imágenes directamente — construye prompts optimizados usando una fórmula de 7 componentes, luego los pasa a un generador.

### La Fórmula de 7 Componentes

| # | Componente | Peso base | Qué controla |
|---|-----------|-----------|--------------|
| 1 | **Subject** | 25% | Sujeto principal — edad, apariencia, expresión |
| 2 | **Style & Aesthetic** | 20% | Lenguaje visual — arte, fotografía, ilustración |
| 3 | **Environment** | 15% | Escenario, fondo, clima, hora del día |
| 4 | **Lighting & Atmosphere** | 15% | Fuente de luz, dirección, temperatura de color |
| 5 | **Action & Dynamics** | 10% | Movimiento, gesto, pose — siempre en presente |
| 6 | **Composition & Camera** | 10% | Encuadre, tipo de lente, f-stop, ángulo |
| 7 | **Material & Texture** | 5% | Superficies, reflectividad, textura de piel |

**Regla crítica:** Prosa narrativa, no lista de palabras clave. "A young woman lies..." > "woman, spa, candles, 8K, masterpiece"

**Palabras prohibidas:** `4K`, `8K`, `masterpiece`, `highly detailed`, `photorealistic`, `award-winning`, `trending on ArtStation`

### Pesos por Dominio

| Dominio | Subject | Style | Env | Light | Action | Comp | Material |
|---------|---------|-------|-----|-------|--------|------|----------|
| Retrato | 30% | 20% | 7% | 18% | 12% | 10% | 3% |
| Cine | 22% | 20% | 15% | 20% | 8% | 12% | 3% |
| Producto | 25% | 20% | 10% | 15% | 3% | 12% | 15% |
| Paisaje | 15% | 20% | 25% | 20% | 5% | 10% | 5% |

### Longitud óptima del prompt
- Draft rápido: 20–60 palabras
- Producción estándar: 100–200 palabras ← usar este
- Complejo profesional: 200–300 palabras
- Los rendimientos decrecientes comienzan en ~250 palabras

### Archivos clave del repo
```
knowledge/prompt-formula.md     — fórmula + pesos
knowledge/domain-modes.md       — 9 perfiles de dominio
knowledge/techniques-catalog.md — 70+ técnicas creativas
knowledge/anti-patterns.md      — errores críticos y palabras prohibidas
scripts/generate.py             — generación vía API (requiere billing)
```

---

## FLUX.1 [dev] — Generación Gratuita sin Billing

**URL directa (sin iframe):** `https://black-forest-labs-flux-1-dev.hf.space`

### Workflow probado

1. Navegar a `black-forest-labs-flux-1-dev.hf.space`
2. Pegar el prompt en el campo de texto
3. Click "Run"
4. La imagen se genera en ~15 segundos
5. Descargar con el botón ↓ en la esquina superior derecha de la imagen

**Resultado real:** Imagen de mujer en spa + masaje facial — calidad editorial, iluminación cálida, exactamente lo pedido.

### Por qué esta URL y no la de HF

La URL `huggingface.co/spaces/black-forest-labs/FLUX.1-dev` embebe la app en un iframe cross-origin que Playwright no puede controlar. La URL directa `.hf.space` expone la app Gradio sin iframe y es completamente controlable por automation.

---

## Mapa de Herramientas Gratuitas 2025

### Imágenes

| Herramienta | Tipo | Free tier | Calidad |
|-------------|------|-----------|---------|
| **FLUX.1 [dev] HF Spaces** | Web UI | Ilimitado (cola) | ⭐⭐⭐⭐⭐ |
| **FLUX.1 [schnell] HF Spaces** | Web UI | Ilimitado (más rápido) | ⭐⭐⭐⭐ |
| Replicate "Try for Free" | API/Web | Sin tarjeta, limitado | ⭐⭐⭐⭐ |
| Craiyon | Web | Ilimitado | ⭐⭐ |
| HF Inference API | API | $0.10 USD/mes | ⭐⭐⭐⭐ |

### Video

| Herramienta | Free tier | Calidad |
|-------------|-----------|---------|
| **Kling AI** (`klingai.com`) | **66 créditos/día** (~6 videos de 5s) | ⭐⭐⭐⭐⭐ |
| Runway ML | 125 créditos al registro | ⭐⭐⭐⭐⭐ |
| Pika Labs | Free tier disponible | ⭐⭐⭐⭐ |
| Luma Dream Machine | Créditos mensuales | ⭐⭐⭐⭐ |

---

## Por qué Google AI (Nano Banana Pro) no es gratis

Todos los modelos de imagen de Google (Gemini, Imagen 4) tienen `limit: 0` en free tier — requieren billing activo en `aistudio.google.com`. Costo: ~$0.13/imagen en 2K con `gemini-3.1-flash-image-preview`.

El script `generate.py` de Claude Banana funciona correctamente una vez activado billing — el único bug fue `imageSize` en `GenerationConfig` (campo inválido), ya corregido.

---

## Ejemplo de Prompt Construido (Dominio: Retrato)

> A young woman in her early thirties lies face-up on a padded spa treatment table, eyes gently closed, her expression one of complete surrender and quiet peace. Over her stands an elderly healer in her late seventies — silver hair pulled back softly, deep laugh lines carved into warm brown skin, eyes half-closed in focused concentration — her weathered hands pressing with knowing deliberateness against the client's temples and cheekbones. Intimate editorial portraiture style, warm amber and honey tones. The spa room glows with candlelight and loose petals of white jasmine. Diffused golden warmth from above-left, the older woman's hands as visual anchor. Medium close-up, both women in frame, elder's hands centered against the younger face. 50mm f/1.8 lens, shallow depth of field, warm candlelit haze background.

Resultado: imagen generada exitosamente en FLUX.1 [dev] vía HF Spaces.
