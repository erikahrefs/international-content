---
name: outline-es
description: Crear un outline estructurado de artículo a partir de un archivo de investigación, para el blog en español
argument-hint: [research-file]
allowed-tools: Read, Write
---

# Outline Skill (Español)

Transforma un archivo de investigación en un outline de artículo estructurado listo para redacción, siguiendo las convenciones del blog de Ahrefs en español.

## Input

**Ruta al archivo de investigación** — Path al archivo de investigación (del skill `/research-es`)

## Reglas de estructura del outline

### Los headers H2 deben:
- Apoyar lógicamente la tesis
- Cubrir el tema de forma completa
- Seguir la estructura del tipo de artículo
- Evitar palabras pasivas con "-ando/-endo" (usar verbos activos)
- Estar en **tipo oración** ("Cómo funciona el SEO local" no "Cómo Funciona El SEO Local")
- Tener **menos de 15 palabras**
- **Nunca poner subtítulos seguidos** — Siempre texto introductorio entre heading y subheading

### Bajo cada H2, incluir:
1. **BLUF** (Lo más importante primero): Un bullet con la idea principal de la sección
2. **Sub-puntos**: Detalles que expanden el BLUF
3. **Evidencia**: Ejemplos, datos, opiniones de expertos, objeciones a abordar

## Convenciones de español

- **Tuteo informal** pero profesional para instrucciones
- **Primera persona plural** ("analizamos", "encontramos") para datos de Ahrefs
- **Español neutro** con ligera tendencia a español de España
- **Términos técnicos en inglés**: SEO, SERP, keyword, backlink, share of voice, AI Overviews, Domain Rating
- **Términos traducidos**: menciones, visibilidad en IA, cuota de mercado, posicionamiento web
- **Números**: Puntos para miles (3.922), comas para decimales (45,7%)

## Workflow

1. Leer el archivo de investigación para entender:
   - Keyword objetivo y métricas
   - Keywords relacionadas a incorporar
   - Análisis de competidores y gaps
   - Ángulo recomendado

2. Redactar la tesis basada en el ángulo de la investigación

3. Crear headers H2 que:
   - Apoyen la tesis
   - Cubran todos los temas clave de la investigación
   - Rellenen gaps identificados en el contenido de competidores
   - Estén en español, tipo oración

4. Para cada H2, añadir:
   - Bullet BLUF
   - 2-4 sub-puntos de apoyo
   - Placeholders de evidencia o datos específicos de la investigación

5. Planificar la introducción:
   - Fórmula **PAS**: Problema → Agitar → Solución
   - Menos de 100 palabras
   - Dato impactante o afirmación contraintuitiva como gancho

6. Planificar la conclusión ("Conclusión" o "Reflexión final"):
   - Resumen del hallazgo principal
   - Siguiente paso accionable
   - CTA: "¿Tienes preguntas? Estamos en LinkedIn y en X."

7. **Revisión de edición estructural** — Antes de finalizar, revisar contra estos principios:

### Verificación MECE (Mutuamente Excluyentes, Colectivamente Exhaustivos)
- **Sin solapamiento**: Cada sección cubre una idea distinta
- **Cobertura completa**: Juntas, las secciones cubren todo el tema
- **Detalle suficiente**: No faltan subtemas que los lectores esperarían
- Si hay solapamiento → fusionar secciones o aclarar límites
- Si hay gaps → añadir secciones faltantes

### Verificación de Principio de Pirámide
- **Una idea por sección**: Cada H2 tiene un BLUF claro
- **Evidencia apoya la idea**: Los sub-puntos respaldan directamente el BLUF
- Si una sección tiene múltiples ideas principales → dividir en H2 separados

### Verificación de peso de secciones
- **Ideas importantes reciben más palabras**: Asignar conteo proporcional
- **Secciones core son sustanciales**: 60-70% del total
- **Secciones de soporte son concisas**: Intro, definiciones, conclusión = 30-40%
- Añadir conteos sugeridos a cada sección

### Verificación de promesa del título
- **El título establece expectativa**: ¿Qué promete al lector?
- **El outline cumple**: ¿Cada sección contribuye a cumplir esa promesa?

### Verificación de claridad de headers
- **Beneficios claros**: Cada header señala qué ganará el lector
- **Consejo explícito**: Headers específicos, no vagos
- **Valor escaneable**: Un lector leyendo solo los headers debe entender el valor

---

## Output

Guardar el outline en `./2-outlines/[keyword-slug].md` con esta estructura:

```markdown
# [Título del artículo]

**Keyword objetivo**: [keyword]
**Conteo de palabras objetivo**: [X palabras]
**Tesis**: [tesis en una frase]
**Mercado**: [es/mx/ar/co/cl]

---

## Revisión de edición estructural

| Verificación | Estado | Notas |
|-------------|--------|-------|
| MECE | ✓ | [Sin solapamiento; cubre tema completo] |
| Principio de Pirámide | ✓ | [Una idea por sección con evidencia] |
| Peso de secciones | ✓ | [Secciones core: X%; Soporte: Y%] |
| Promesa del título | ✓ | [El outline cumple: "..."] |
| Claridad de headers | ✓ | [Todos los headers orientados a beneficios] |

---

## Introducción
**Objetivo**: <100 palabras (fórmula PAS)

**Gancho (Problema)**: [dato impactante o afirmación contraintuitiva]

**Agitar**: [por qué importa o qué pasa si lo ignoras]

**Solución**: [adelanto de lo que el artículo enseña]

---

## [Header H2 1]
**Objetivo**: ~[X] palabras

- **BLUF**: [punto principal de esta sección]
- [Sub-punto 1]
- [Sub-punto 2]
- **Evidencia**: [ejemplo específico, dato o experto a citar]

## [Header H2 2]
**Objetivo**: ~[X] palabras

...

---

## Conclusión
**Objetivo**: <150 palabras

- **Resumen**: [replantear hallazgo principal]
- **Siguiente paso**: [paso accionable para el lector]
- **CTA**: Enlace a LinkedIn y X de Ahrefs ES
```

## Ejemplo de uso

```
/outline-es ./1-research/visibilidad-ia.md
```
