---
name: research-es
description: Investigar una keyword usando Ahrefs para el mercado español - encontrar keywords relacionadas y analizar contenido top
argument-hint: [keyword]
allowed-tools: Read, Write, Edit, Bash, WebFetch, mcp__ahrefs__*
---

# Research Skill (Español)

Recopila inteligencia de keywords y analiza el contenido mejor posicionado para una keyword objetivo usando Ahrefs MCP, con foco en el mercado de habla hispana.

## Input

**Opción A: El usuario proporciona keyword directamente**
Si `$ARGUMENTS` contiene una keyword, usarla y saltar a la sección Workflow.

**Opción B: Seleccionar de keyword-ideas.csv**
Si `$ARGUMENTS` está vacío:

1. **Leer `keyword-ideas.csv`** y filtrar para mostrar keywords disponibles:
   - Excluir filas donde la columna `selected` = "yes"
   - Ordenar por `business_potential` (desc), luego `priority`, luego `traffic_potential` (desc)

2. **Presentar las 10 mejores keywords disponibles:**

   ```
   ## Keywords disponibles (de keyword-ideas.csv)

   | # | Keyword | Volumen | TP | KD | Prioridad | BP | Producto |
   |---|---------|---------|-----|-----|-----------|-----|---------|
   | 1 | [keyword] | [vol] | [tp] | [kd] | [prioridad] | [bp] | [producto] |
   ...

   Selecciona una keyword por número, o escribe una keyword personalizada.
   ```

3. **Esperar selección del usuario.**

4. **Cuando el usuario selecciona:** Marcar como "yes" en columna `selected`.

---

## Configuración de mercado

**País por defecto**: `es` (España)

Para otros mercados hispanohablantes, el usuario puede especificar:
- `mx` — México
- `ar` — Argentina
- `co` — Colombia
- `cl` — Chile
- `pe` — Perú

El país se usa en todas las llamadas a Ahrefs MCP: volumen, SERP, competidores.

---

## Workflow

### Paso 1: Obtener métricas de keyword primaria y parent topic

Llamar a `mcp__ahrefs__keywords-explorer-overview` con:
- `keywords`: Keyword objetivo
- `country`: "es" (o el mercado objetivo)
- `select`: "keyword,volume,difficulty,traffic_potential,cpc,parent_topic"

**Extraer:**
- Volumen y dificultad de la keyword primaria
- **Parent topic** — Crucial para identificar qué keywords se pueden orientar juntas

---

### Paso 2: Encontrar variaciones long-tail (mismo parent topic)

Llamar a `mcp__ahrefs__keywords-explorer-matching-terms` con:
- `keywords`: Keyword objetivo
- `country`: "es"
- `select`: "keyword,volume,difficulty,traffic_potential,parent_topic"
- `order_by`: "volume:desc"
- `limit`: 50
- `where`:
```json
{"and": [
  {"field": "volume", "is": ["gte", 50]},
  {"field": "word_count", "is": ["gte", 3]}
]}
```

**Filtrar resultados para mantener solo keywords donde:**
- `parent_topic` coincide con el parent topic de la keyword objetivo, O
- `parent_topic` es la keyword objetivo en sí

**Organizar en:**
- **Keyword primaria** — El objetivo principal
- **Keywords secundarias** — Variaciones long-tail con mismo parent topic
- **Candidatos a artículo separado** — Keywords con parent topic diferente

---

### Paso 3: Extraer preguntas

Llamar a `mcp__ahrefs__keywords-explorer-matching-terms` con:
- `keywords`: Keyword objetivo
- `country`: "es"
- `select`: "keyword,volume,difficulty,parent_topic"
- `order_by`: "volume:desc"
- `limit`: 30
- `terms`: "questions"

**Organizar preguntas en:**

1. **Preguntas de alta prioridad (volumen 100+)** — Deben abordarse directamente
2. **Preguntas de apoyo (volumen 50-99)** — Buenas para FAQ
3. **Temas de preguntas** — Agrupar por tipo:
   - "¿Qué es..." → Definición necesaria
   - "¿Cómo..." → Tutorial necesario
   - "¿Por qué..." → Razonamiento necesario
   - "Mejor..." → Comparación necesaria

**Nota para español**: Las preguntas en español suelen empezar con signos de interrogación invertidos (¿) y pueden usar formas diferentes a las inglesas. Buscar también variaciones sin signos de interrogación.

---

### Paso 4: Obtener SERP Overview

Llamar a `mcp__ahrefs__serp-overview` con:
- `keyword`: Keyword objetivo
- `country`: "es"
- `select`: "position,url,title,domain_rating,traffic,refdomains,type"
- `top_positions`: 10

**Extraer para cada resultado:**
- URL y título
- Domain rating
- Tráfico estimado a esa página
- Tipo (orgánico, snippet, etc.)

**Nota**: Para keywords en español, es común ver resultados de dominios .es, .com con subdirectorio /es/, y dominios LATAM (.mx, .com.ar). Documentar la distribución geográfica.

---

### Paso 5: Analizar intención de búsqueda y formato de contenido

Basándose en los top 10 resultados SERP, determinar:

1. **Intención primaria**:
   - **Informativa** — Quiere aprender (guías, explicaciones, tutoriales)
   - **Investigación comercial** — Investigando antes de comprar (comparativas, reviews)
   - **Transaccional** — Listo para comprar/registrarse (páginas de producto, precios)
   - **Navegacional** — Busca un sitio específico

2. **Formato dominante de contenido**:
   - Guía integral, Listicle, Tutorial paso a paso, Herramienta, Comparativa, Definición

3. **Señales de profundidad del contenido:**
   - Conteo promedio de palabras de los top 3
   - Presencia de herramientas (sub-intención transaccional)
   - Resultados de Reddit/foros (indica búsqueda de opiniones)
   - Resultados de video

---

### Paso 6: Analizar top 3 páginas

Para los top 3 resultados orgánicos del Paso 4, extraer y analizar su contenido.

**Para cada URL, usar WebFetch con este prompt:**
```
Extrae los headers H2 y H3 exactos de este artículo en orden. Formato:
## [texto H2]
### [texto H3]
También nota: conteo aproximado de palabras, idioma del artículo, y cualquier elemento especial (listas, tablas, imágenes).
```

**Registrar para cada artículo:**
1. **Estructura completa de headers**
2. **Conteo de palabras**
3. **Idioma** — ¿Está en español o es un resultado en inglés?
4. **Elementos especiales**

**Después de analizar los 3, identificar patrones:**
- Headers/temas cubiertos por los 3 (obligatorio incluir)
- Headers/temas cubiertos por 2/3 (debería incluir)
- Headers únicos (potenciales diferenciadores o gaps)

---

### Paso 7: Identificar gaps de contenido y oportunidades

**A. Análisis de gaps en headers/temas**

Crear matriz de comparación:

| Tema/Header | Art. 1 | Art. 2 | Art. 3 | ¿Gap? |
|-------------|--------|--------|--------|-------|
| [tema] | ✓ | ✓ | ✓ | No — obligatorio |
| [tema] | ✓ | ✓ | ✗ | No — recomendado |
| [tema] | ✓ | ✗ | ✗ | Tal vez — diferenciador |
| [tema no cubierto] | ✗ | ✗ | ✗ | Sí — oportunidad |

**B. Análisis de gaps en preguntas**

**C. Identificar oportunidades:**
1. **Temas ausentes**
2. **Preguntas sin responder**
3. **Gaps de profundidad**
4. **Gaps de actualización**
5. **Gaps de formato**

**D. Determinar ángulo** para diferenciarse

---

## Output

Guardar en `./1-research/[keyword-slug].md`:

```markdown
# Investigación: [Keyword]

**Fecha**: [YYYY-MM-DD]
**Mercado objetivo**: [país] (es/mx/ar/co/cl)

---

## Orientación de keywords

### Keyword primaria
| Keyword | Volumen | KD | Traffic Potential | Parent Topic |
|---------|---------|-----|-------------------|--------------|
| [keyword] | [vol] | [kd] | [tp] | [parent] |

### Keywords secundarias (mismo parent topic)
| Keyword | Volumen | KD | Parent Topic |
|---------|---------|-----|--------------|
| [keyword] | [vol] | [kd] | [parent] |

---

## Informe de preguntas

### Preguntas de alta prioridad (Volumen 100+)
| Pregunta | Volumen | ¿Cubierta por competidores? |
|----------|---------|----------------------------|
| [pregunta] | [vol] | [Sí / Parcial / No] |

### Preguntas de apoyo (Volumen 50-99)
- [pregunta] ([volumen])

### Temas de preguntas
- **"¿Qué es..." preguntas:** [lista]
- **"¿Cómo..." preguntas:** [lista]
- **"¿Por qué/Mejor..." preguntas:** [lista]

---

## Análisis SERP

### Top 10 resultados
| Pos | Título | Dominio | DR | Tráfico | Idioma |
|-----|--------|---------|-----|---------|--------|
| 1 | [título] | [dominio] | [dr] | [tráfico] | [es/en] |

### Análisis de intención de búsqueda

**Intención primaria:** [Informativa / Investigación comercial / Transaccional / Navegacional]

**Formato dominante:** [Guía integral / Listicle / Tutorial / Herramienta / Comparativa / Definición]

**Enfoque recomendado:** [1-2 frases sobre qué formato de contenido crear]

---

### Análisis de top 3

#### 1. [Título] - [Dominio]
**URL**: [url]
**Tráfico estimado**: [tráfico]
**Conteo de palabras**: ~[X] palabras
**Idioma**: [es/en]

**Estructura de headers:**
(...)

---

## Patrones comunes

**Headers/temas cubiertos por los 3 (obligatorio):**
- [...]

**Headers/temas cubiertos por 2/3 (recomendado):**
- [...]

---

## Gaps de contenido y oportunidades

### Matriz de cobertura de temas
| Tema | Art. 1 | Art. 2 | Art. 3 | Oportunidad |
|------|--------|--------|--------|-------------|
| [tema] | ✓ | ✓ | ✓ | Obligatorio |

### Preguntas sin responder
- [pregunta] ([volumen]) — No cubierta

### Resumen de gaps

**Temas ausentes:**
- [...]

**Oportunidades de profundidad:**
- [...]

---

## Enfoque recomendado

**Ángulo**: [ángulo único]

**Tipo de contenido**: [guía / listicle / tutorial / comparativa]

**Conteo de palabras objetivo**: [X palabras]

**Diferenciadores clave:**
- [...]

**Estructura H2 sugerida:**
1. [idea H2]
2. [idea H2]
...
```

---

## Parámetros MCP comunes

**Formato de fecha:**
- ✅ Correcto: `"2026-02-17"` (YYYY-MM-DD)

**Códigos de país para mercados hispanos:**
- `es` — España
- `mx` — México
- `ar` — Argentina
- `co` — Colombia
- `cl` — Chile
- `pe` — Perú

**Sintaxis de filtros:**
```json
{"field": "volume", "is": ["gte", 100]}
{"and": [filter1, filter2]}
```
