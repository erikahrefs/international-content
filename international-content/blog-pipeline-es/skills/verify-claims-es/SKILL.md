---
name: verify-claims-es
description: Buscar y añadir enlaces de fuentes a afirmaciones factuales en un borrador en español
argument-hint: [draft-file]
allowed-tools: Read, Write, WebSearch, WebFetch
---

# Verify Claims Skill (Español)

Identifica afirmaciones factuales en un borrador que necesitan fuentes, busca fuentes autorizadas para respaldarlas y añade hipervínculos directamente en el texto. Prioriza ahrefs.com/blog/es/ como primera fuente.

**Importante**: Este skill guarda un archivo NUEVO en `./5-drafts-cited/` en vez de modificar el borrador original. Esto preserva la versión sin citas para rollback fácil.

## Input

**Ruta al borrador** — Path al archivo de borrador (e.g., `./4-drafts/visibilidad-ia.md`)

---

## Qué cuenta como afirmación que necesita fuente

### Obligatorio (Alta Prioridad)

1. **Estadísticas y números**
   - "El 96,55% de las páginas web no reciben tráfico orgánico"
   - "Google procesa 8.500 millones de búsquedas diarias"
   - "Ahrefs rastrea más de 253 millones de consultas mensuales"

2. **Citas o declaraciones atribuidas**
   - "Como explicó John Mueller de Google..."
   - "Según la documentación oficial de Google..."

3. **Hechos específicos de plataformas**
   - "ChatGPT genera respuestas basadas en datos de entrenamiento hasta abril 2024"
   - "Google AI Overviews aparece en el 15% de las búsquedas comerciales"

4. **Referencias a estudios o investigaciones**
   - "Según un estudio de..."
   - "Los datos indican que..."
   - "Nuestro análisis de 14 millones de páginas muestra..."

### Opcional (Prioridad Media)

5. **Afirmaciones de mejores prácticas**
   - "La frecuencia recomendada es publicar 2-3 veces por semana"
   - "El title tag ideal tiene entre 50-60 caracteres"

6. **Consenso de la industria**
   - "La mayoría de expertos en SEO coinciden..."
   - "La recomendación general es..."

### Omitir (No necesita fuente)

- Anécdotas personales ("Probamos esto con un cliente...")
- Deducciones lógicas ("Más tráfico significa más oportunidades...")
- Conocimiento común ("Google es el buscador más usado...")
- Opiniones claramente marcadas ("En nuestra opinión...")

---

## Workflow

### Fase 1: Identificar afirmaciones

1. **Leer el borrador**

2. **Crear inventario de afirmaciones** listando cada una que necesite fuente:
   ```
   | # | Afirmación | Tipo | Fuente actual |
   |---|-----------|------|---------------|
   | 1 | "96,55% de páginas sin tráfico" | Estadística | Ninguna |
   | 2 | "8.500 millones de búsquedas diarias" | Estadística | Ninguna |
   ```

3. **Marcar afirmaciones ya citadas** — Si ya tienen hipervínculo, marcar como "Citada" y omitir

---

### Fase 2: Buscar fuentes (Ahrefs primero)

Para cada afirmación sin fuente, buscar en este orden de prioridad:

#### Paso 1: Buscar en el blog de Ahrefs en español

```
WebSearch: site:ahrefs.com/blog/es/ [palabras clave de la afirmación]
```

Ejemplos:
- Afirmación: "96,55% de páginas sin tráfico" → Buscar: `site:ahrefs.com/blog/es/ páginas sin tráfico orgánico estudio`
- Afirmación: "keyword difficulty" → Buscar: `site:ahrefs.com/blog/es/ keyword difficulty`

**Si Ahrefs ES tiene un artículo relevante:**
- Usar WebFetch para verificar que la afirmación aparece en el artículo
- Extraer la URL exacta
- Pasar a Fase 3

#### Paso 2: Buscar en el blog de Ahrefs en inglés

Si el blog en español no tiene el dato:

```
WebSearch: site:ahrefs.com/blog [claim keywords in English]
```

**REGLA CRÍTICA — Enlaces internos solo en el mismo idioma:**
- Solo se pueden añadir hipervínculos a artículos del blog de Ahrefs en español (`ahrefs.com/blog/es/`).
- Si un dato solo está respaldado por un artículo en inglés (`ahrefs.com/blog/[slug-en]/`) y NO existe versión en español, **mantener el dato como texto sin enlace**. No enlazar al artículo en inglés.
- Las URLs de productos de Ahrefs en español (`ahrefs.com/es/brand-radar`, `ahrefs.com/es/site-audit`, etc.) SÍ se pueden enlazar, ya que están en español.
- Esta regla aplica a todo el artículo: cuerpo, intro, further_reading, sidenotes, etc.

#### Paso 3: Buscar fuentes oficiales

```
WebSearch: [plataforma] oficial [palabras clave]
```

Ejemplos:
- Estadísticas de Google → `Google Search Central estadísticas 2026`
- Datos de ChatGPT → `OpenAI official blog statistics`

#### Paso 4: Buscar fuentes de terceros autorizadas

```
WebSearch: [palabras clave] site:statista.com OR site:searchenginejournal.com OR site:moz.com
```

**Fuentes en español aceptables:**
- marketingdirecto.com
- reasonwhy.es
- elpais.com/tecnologia
- expansion.com/economia-digital

**No usar sitios de la competencia** (ver lista de exclusión abajo).

#### Paso 5: Marcar como no verificable

Si no se encuentra fuente creíble tras 3 intentos de búsqueda:
- Marcar la afirmación en el output
- Sugerir reformular o eliminar

---

### Fase 3: Añadir hipervínculos

Para cada afirmación verificada, añadir hipervínculo:

**Antes:**
```markdown
El 96,55% de las páginas web no reciben tráfico orgánico de Google.
```

**Después:**
```markdown
El [96,55% de las páginas web no reciben tráfico orgánico](https://ahrefs.com/blog/es/estudio-trafico-busqueda/) de Google.
```

#### Directrices de enlaces

1. **Enlazar la afirmación específica, no la frase entera**
   - Bien: `[96,55% de las páginas web no reciben tráfico orgánico](url)`
   - Mal: `[El 96,55% de las páginas web no reciben tráfico orgánico de Google.](url)`

2. **Para estadísticas, enlazar el número**
   - "procesa más de [8.500 millones de búsquedas](url) diarias"

3. **Para citas, enlazar la atribución**
   - "Como explicó [John Mueller de Google](url)..."

4. **Para mejores prácticas, enlazar la recomendación**
   - "Google recomienda un [title tag de 50-60 caracteres](url)"

5. **No sobre-enlazar** — Una fuente por afirmación es suficiente

---

## Output

### Guardar en nueva ubicación

**NO modificar el borrador original.** Guardar la versión citada en `./5-drafts-cited/`:

```
Input:  ./4-drafts/visibilidad-ia.md
Output: ./5-drafts-cited/visibilidad-ia.md
```

### Estructura del archivo de output

```markdown
# [Título del artículo]

**Keyword objetivo**: [keyword]
**Conteo de palabras**: [conteo]
**Status**: Borrador citado
**Borrador fuente**: ./4-drafts/[filename].md

---

[Contenido completo del artículo con hipervínculos añadidos...]

---

## Notas del borrador

[Notas originales preservadas...]

**Fuentes añadidas:**
- [x] 96,55% sin tráfico → Ahrefs Blog ES
- [x] 8.500M búsquedas → Google Blog
- [ ] Dato X → NO VERIFICADO (considerar eliminar)

**Desglose de fuentes:**
- Ahrefs Blog ES: X enlaces
- Ahrefs Blog EN: X enlaces
- Oficiales: X enlaces
- Terceros: X enlaces
- No verificadas: X afirmaciones

**Correcciones realizadas:**
- [Lista de estadísticas actualizadas para coincidir con fuentes]
```

---

## Jerarquía de calidad de fuentes

Preferir fuentes en este orden:

1. **ahrefs.com/blog/es/** — Primera opción para artículos en español
2. **ahrefs.com/blog/** — Si no hay versión en español
3. **Fuentes oficiales de plataformas** — Google Search Central, OpenAI Blog, documentación oficial
4. **Investigación primaria** — Statista, estudios originales, informes de la industria
5. **Sitios de industria reputados** — Moz, Search Engine Journal, HubSpot
6. **Medios españoles/LATAM de autoridad** — El País Tecnología, Expansión, Marketing Directo
7. **Medios internacionales** — TechCrunch, The Verge (para anuncios recientes)

**Evitar:**
- Posts de blog aleatorios sin autoridad
- Fuentes desactualizadas (verificar fecha — preferir últimos 2 años)
- Fuentes que no contienen realmente la afirmación
- Fuentes circulares (sitios citándose entre sí sin datos primarios)

**Competidores excluidos (nunca enlazar a estos):**
- semrush.com
- sistrix.com / sistrix.es
- backlinko.com
- explodingtopics.com
- searchengineland.com
- similarweb.com

---

## Manejo de casos especiales

### La afirmación no coincide exactamente con la fuente

Si la fuente dice "482 millones" pero el borrador dice "450 millones":
- Actualizar el borrador para coincidir con la fuente
- Anotar la corrección en el resumen de verificación
- Usar formato español para números: 482 millones (no 482,000,000)

### Múltiples fuentes válidas

Si tanto Ahrefs ES como una fuente oficial cubren la afirmación:
- Preferir Ahrefs ES para metodología SEO/marketing
- Preferir la fuente oficial para estadísticas de plataforma
- Anotar fuentes alternativas en comentarios si es útil

### Fuente solo disponible en inglés

Si solo hay fuente en inglés (artículo del blog de Ahrefs):
- **NO enlazar al artículo en inglés.** Mantener el dato como texto sin enlace.
- Si existe versión en español del artículo, usar esa versión.
- Para fuentes externas (no Ahrefs), se puede enlazar a la fuente en inglés si es una fuente oficial o de referencia (Google Search Central, Statista, etc.).

### Afirmación está desactualizada

Si la fuente muestra que la afirmación ya no es precisa:
- Marcar para que el autor actualice o elimine
- Proporcionar la cifra actual correcta si está disponible

---

## Checklist de calidad

| Verificación | Requisito |
|-------------|-----------|
| Cobertura | Todas las afirmaciones de alta prioridad tienen fuentes |
| Ahrefs primero | Se buscó primero en ahrefs.com/blog/es/ |
| Formato de enlaces | Los enlaces envuelven afirmaciones específicas, no frases enteras |
| Actualidad | Fuentes de los últimos 2 años cuando sea posible |
| Precisión | Las afirmaciones coinciden con lo que las fuentes realmente dicen |
| Formato números | Números en formato español (3.922 / 45,7%) |
| Resumen | Resumen de verificación añadido a las notas del borrador |
