---
type: session
title: "Contratos DEPAS — Depa 37, Inquilino Mexicano, Reglas INE"
created: 2026-04-20
updated: 2026-04-20
tags:
  - depas
  - contratos
  - ine
  - mexico
  - arrendamiento
status: evergreen
related:
  - "[[meta/yourenergy-session-2026-04-19]]"
---

# Contratos DEPAS — Depa 37, Inquilino Mexicano, Reglas INE

Sesión 2026-04-20. Contrato generado para Mariana Montserrat Medina Reynoso, primer inquilino mexicano del sistema. Se establecieron reglas nuevas para INE mexicana y se corrigieron bugs del script.

---

## Contrato Generado

| Campo | Valor |
|-------|-------|
| Depto | 37, Torre E |
| Inquilina | Mariana Montserrat Medina Reynoso |
| Duración | 1 año forzoso (01/ago/2026 - 31/jul/2027) |
| Renta | $12,000 MXN/mes |
| CURP | MERM060831MMCDYRA2 |
| N. credencial (OCR trasero) | 5223138175252 |
| Emergencia | Juan Manuel Medina Castro, 7223946992 |
| Carpeta | `DEPA_37_MARIANA_MONTSERRAT_MEDINA_REYNOSO/` |

---

## Reglas INE Mexicana (nuevas)

### Número de credencial para votar
El campo "credencial para votar con número X" en el contrato usa el **número OCR de la parte trasera** de la INE, no la Clave de Elector del frente.

- Leer la primera línea MRZ al reverso de la INE: `IDMEX{doc_num}<<{numero_ocr}`
- Tomar la secuencia después de `<<`
- Ejemplo: `IDMEX2672049918<<5223138175252` → usar `5223138175252`
- La Clave de Elector (ej. `MDRYMR06083115M700`) NO va en el contrato

### CURP en campo RFC
En la sección de Generales II del contrato, el campo "Registro Federal de Contribuyentes" se llena con la **CURP** del inquilino mexicano (funciona como RFC individual).

### Comando generar.py para mexicanos
```bash
python3 generar.py \
  --contrato N \
  --nombre "NOMBRE COMPLETO" \
  --titulo señorita|señor \
  --inicio DD/MM/YYYY --fin DD/MM/YYYY \
  --renta XXXXX --duracion "1 AÑO" --torre X \
  --nacionalidad mexicana \
  --estado-civil soltera|soltero|casado... \
  --ocupacion estudiante|... \
  --fecha-nac DD/MM/YYYY \
  --lugar-nac "Ciudad, Estado" \
  --pasaporte {numero_ocr_trasero_ine} \
  --tel "XXXXXXXXXX" \
  --emergencia "NOMBRE" --tel-emergencia "XXXXXXXXXX"
```

Diferencias vs. extranjeros:
- `--nacionalidad mexicana` (no "español")
- `--pasaporte` = número OCR trasero INE (no número de pasaporte)
- `--lugar-nac` = "Ciudad, Estado de México" (no "Ciudad, País")

---

## Bug: Títulos intercambiados en encabezado y Generales

El script pone "LA SEÑORITA" para el arrendador y "EL SEÑOR" para la arrendataria cuando el inquilino es femenino. Corrección manual siempre requerida:

| Párrafo | Run | Texto incorrecto | Texto correcto |
|---------|-----|-----------------|----------------|
| [0] Encabezado | [16] | `"QUE CELEBRAN POR UNA PARTE LA SEÑORITA "` | `"QUE CELEBRAN POR UNA PARTE EL SEÑOR "` |
| [0] Encabezado | [20] | `"; Y EL SEÑOR "` | `"; Y LA SEÑORITA "` |
| [56] Generales I | [2] | `"La señorita "` | `"El señor "` |

Script de corrección:
```python
from docx import Document
doc = Document("CONTRATO N_NUEVO.docx")
doc.paragraphs[0].runs[16].text = "QUE CELEBRAN POR UNA PARTE EL SEÑOR "
doc.paragraphs[0].runs[16].font.highlight_color = None
doc.paragraphs[0].runs[20].text = "; Y LA SEÑORITA "
doc.paragraphs[56].runs[2].text = "El señor "
doc.paragraphs[56].runs[2].font.highlight_color = None
doc.save("CONTRATO N_NUEVO.docx")
```

> Los índices de runs pueden variar entre templates. Verificar siempre antes de aplicar.

---

## Corrección manual — RFC y credencial en Generales II

Después de generar, el párrafo [57] (Generales II) contiene RFC y credencial del inquilino anterior. Reemplazar:

```python
p57 = doc.paragraphs[57]
# RFC → CURP del inquilino mexicano
p57.runs[35].text = "CURP_AQUI"
# Credencial → número OCR trasero
p57.runs[39].text = "numero_ocr_aqui"
# Letras del número (deletrear cada carácter)
p57.runs[41].text = "letras_del_numero) ---..."
```

> Los índices de runs varían por template. Identificarlos con un loop antes de reemplazar.

---

## Template Hoja de Contacto — Modificación Permanente (2026-04-20)

`HOJA_CONTACTO_TEMPLATE.docx` fue modificado para eliminar el segundo bloque de inquilino y segunda emergencia. Todos los contratos futuros generan hoja de contacto con:
- Un solo NOMBRE + CEL
- Una sola EMERGENCIA + CEL

No se requiere limpieza manual. Si en el futuro hay dos inquilinos, habrá que restaurar los campos en el template.

---

## Flujo Completo para Inquilino Mexicano

1. Foto frente INE → extraer: nombre completo, fecha nac, lugar nac, CURP
2. Foto reverso INE → leer primera línea MRZ, extraer número después de `<<`
3. Confirmar: depto, fecha inicio, renta, torre, duración
4. Ejecutar `generar.py` con `--pasaporte {numero_ocr}`, `--nacionalidad mexicana`
5. Corrección manual 1: títulos intercambiados (encabezado + Generales I)
6. Corrección manual 2: RFC → CURP, credencial → número OCR en Generales II
7. Verificar encabezado, montos (número = letras), firmas
