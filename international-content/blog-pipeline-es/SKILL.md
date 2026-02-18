---
name: blog-pipeline-es
description: Ejecutar el pipeline completo de creación de artículos para el blog de Ahrefs en español, desde keyword hasta artículo listo para publicar
argument-hint: [keyword o paso]
allowed-tools: Read, Write, Edit, Skill
---

# Blog Pipeline (Español)

Orquesta el pipeline completo de creación de contenido para el blog de Ahrefs en español, ejecutando cada skill en secuencia desde investigación de keyword hasta artículo listo para publicar.

## Input

**Opción A: Pipeline completo desde keyword**
```
/blog-pipeline-es "marketing de contenidos"
```
Ejecuta todos los pasos desde investigación hasta publicación.

**Opción B: Reanudar desde un paso específico**
```
/blog-pipeline-es --from=draft "marketing de contenidos"
```
Reanuda el pipeline desde el paso especificado (útil si los pasos anteriores están completos).

**Opción C: Ejecutar sin argumentos**
```
/blog-pipeline-es
```
Muestra keywords disponibles de `keyword-ideas.csv` (igual que `/research-es` sin argumentos).

**Opción D: Especificar mercado**
```
/blog-pipeline-es --country=mx "marketing de contenidos"
```
Ejecuta el pipeline orientado a un mercado hispanohablante específico (por defecto: es).

---

## Pasos del pipeline

| Paso | Skill | Input | Carpeta de output |
|------|-------|-------|-------------------|
| 1 | `/research-es` | keyword | `1-research/` |
| 2 | `/outline-es` | archivo de investigación | `2-outlines/` |
| 3 | `/ahrefs-mentions-es` | archivo de outline | `3-outlines-annotated/` |
| 4 | `/draft-es` | outline anotado | `4-drafts/` |
| 5 | `/verify-claims-es` | archivo de borrador | `5-drafts-cited/` |
| 6 | `/preview-es` | borrador citado | `6-preview/` |
| 7 | `/format-for-publish-es` | borrador citado | `7-publish/` |

---

## Detalle de pasos

### Paso 1: Investigación
Recopilar inteligencia de keywords y analizar contenido top del mercado hispanohablante.

```
/research-es [keyword]
```

**Input:** Keyword (del argumento o seleccionada de CSV)
**Output:** `./1-research/[keyword-slug].md`

**Qué hace:**
- Obtener métricas de keyword (volumen, dificultad, traffic potential) para mercado ES
- Encontrar variaciones long-tail con mismo parent topic
- Extraer preguntas en español
- Analizar SERP y top 3 páginas (notar si están en español o inglés)
- Identificar gaps de contenido y oportunidades

---

### Paso 2: Outline
Crear un outline estructurado basado en la investigación, con convenciones del blog ES.

```
/outline-es ./1-research/[keyword-slug].md
```

**Input:** Archivo de investigación del Paso 1
**Output:** `./2-outlines/[keyword-slug].md`

**Qué hace:**
- Crear estructura H2/H3 basada en análisis de competidores
- Headers en tipo oración, en español
- Fórmula PAS para la introducción
- Incluir keywords secundarias a incorporar
- Añadir briefs con puntos clave a cubrir

---

### Paso 3: Menciones de Ahrefs
Anotar outline con menciones naturales de productos Ahrefs, con URLs en español.

```
/ahrefs-mentions-es ./2-outlines/[keyword-slug].md
```

**Input:** Archivo de outline del Paso 2
**Output:** `./3-outlines-annotated/[keyword-slug].md`

**Qué hace:**
- Identificar secciones donde herramientas de Ahrefs aportan valor
- Añadir menciones contextuales (no forzadas) **en español**
- Incluir recomendaciones de funciones específicas
- Usar URLs en español (ahrefs.com/es/, ahrefs.com/blog/es/)
- Preservar estructura original del outline

---

### Paso 4: Borrador
Expandir el outline anotado en un artículo completo en español.

```
/draft-es ./3-outlines-annotated/[keyword-slug].md
```

**Input:** Outline anotado del Paso 3
**Output:** `./4-drafts/[keyword-slug].md`

**Qué hace:**
- Escribir prosa completa para cada sección, sección por sección
- Seguir la guía de estilo del blog de Ahrefs en español
- Tuteo informal + primera persona plural para datos
- Incluir ejemplos y explicaciones con datos específicos
- Párrafos de máximo 3 líneas
- Formato español para números (3.922 / 45,7%)

---

### Paso 5: Verificar afirmaciones
Encontrar y añadir enlaces de fuentes a afirmaciones factuales.

```
/verify-claims-es ./4-drafts/[keyword-slug].md
```

**Input:** Archivo de borrador del Paso 4
**Output:** `./5-drafts-cited/[keyword-slug].md`

**Qué hace:**
- Identificar afirmaciones factuales que necesitan fuentes
- Buscar primero en ahrefs.com/blog/es/, luego ahrefs.com/blog/, luego fuentes oficiales
- Añadir hipervínculos a las afirmaciones
- Marcar afirmaciones que no pudieron verificarse
- Excluir competidores (semrush.com, sistrix.es, etc.)

---

### Paso 6: Preview
Generar preview HTML con estilo Ahrefs.

```
/preview-es ./5-drafts-cited/[keyword-slug].md
```

**Input:** Borrador citado del Paso 5
**Output:** `./6-preview/[keyword-slug].html`

**Qué hace:**
- Convertir markdown a HTML estilizado
- Aplicar CSS del blog de Ahrefs
- Asegurar renderizado correcto de caracteres españoles (á, é, ñ, ¿, ¡)
- Crear preview visual para revisión

---

### Paso 7: Formatear para publicación
Aplicar shortcodes de WordPress y exportar a .docx.

```
/format-for-publish-es ./5-drafts-cited/[keyword-slug].md
```

**Input:** Borrador citado del Paso 5
**Output:**
- `./7-publish/[keyword-slug].md` (con shortcodes)
- `./7-publish/[keyword-slug].docx` (documento Word)

**Qué hace:**
- Convertir callouts a shortcodes de WordPress
- Slugs de sección sin tildes ni ñ (á→a, ñ→n)
- Títulos de recommendation en español ("Consejo", "Consejo pro")
- Further reading con URLs del blog ES cuando existan
- Formatear para compatibilidad con CMS
- Exportar a .docx para subida

---

## Ejecución del workflow

Al ejecutar el pipeline completo:

1. **Parsear keyword** de argumentos (o pedir selección de CSV)
2. **Convertir a slug** (minúsculas, guiones: "marketing de contenidos" → "marketing-de-contenidos")
3. **Determinar mercado** (por defecto: es)
4. **Ejecutar cada paso en secuencia:**

```
Paso 1: /research-es "[keyword]"
   → Verificar: ./1-research/[slug].md existe

Paso 2: /outline-es ./1-research/[slug].md
   → Verificar: ./2-outlines/[slug].md existe

Paso 3: /ahrefs-mentions-es ./2-outlines/[slug].md
   → Verificar: ./3-outlines-annotated/[slug].md existe

Paso 4: /draft-es ./3-outlines-annotated/[slug].md
   → Verificar: ./4-drafts/[slug].md existe

Paso 5: /verify-claims-es ./4-drafts/[slug].md
   → Verificar: ./5-drafts-cited/[slug].md existe

Paso 6: /preview-es ./5-drafts-cited/[slug].md
   → Verificar: ./6-preview/[slug].html existe

Paso 7: /format-for-publish-es ./5-drafts-cited/[slug].md
   → Verificar: ./7-publish/[slug].md y .docx existen
```

5. **Reportar completado** con todas las ubicaciones de archivos

---

## Reanudar desde paso

Para reanudar desde un paso específico (si los outputs anteriores existen):

```
/blog-pipeline-es --from=outline "marketing de contenidos"
```

Valores válidos de `--from`:
- `research` (Paso 1 — por defecto, pipeline completo)
- `outline` (Paso 2)
- `ahrefs-mentions` (Paso 3)
- `draft` (Paso 4)
- `verify-claims` (Paso 5)
- `preview` (Paso 6)
- `format-for-publish` (Paso 7)

Antes de reanudar, verificar que el archivo de input requerido del paso anterior existe.

---

## Mercados soportados

| Código | Mercado | Notas |
|--------|---------|-------|
| `es` | España | Por defecto. Español neutro con tendencia a España |
| `mx` | México | Ajustar coloquialismos si necesario |
| `ar` | Argentina | Considerar voseo si el público es local |
| `co` | Colombia | Español neutro |
| `cl` | Chile | Español neutro |
| `pe` | Perú | Español neutro |

**Nota**: El estilo de escritura es español neutro para todos los mercados. El código de país afecta principalmente a:
- Datos de keyword research (volumen local)
- SERP analysis (resultados locales)
- Fuentes de verificación (medios locales relevantes)

---

## Resumen de output

Después de un pipeline completo:

```
## Pipeline completado: [keyword]

| Paso | Output |
|------|--------|
| 1. Investigación | ./1-research/[slug].md |
| 2. Outline | ./2-outlines/[slug].md |
| 3. Anotado | ./3-outlines-annotated/[slug].md |
| 4. Borrador | ./4-drafts/[slug].md |
| 5. Citado | ./5-drafts-cited/[slug].md |
| 6. Preview | ./6-preview/[slug].html |
| 7. Publicación | ./7-publish/[slug].md, .docx |

Listo para subida a WordPress: ./7-publish/[slug].docx
```

---

## Manejo de errores

- **Paso falla:** Detener pipeline, reportar error, preservar outputs completados
- **Input faltante:** Verificar que el output del paso anterior existe antes de proceder
- **Directorio faltante:** Crear directorio de output si no existe

Cada paso es independiente — si el pipeline falla a mitad de camino, puedes corregir el problema y reanudar desde ese paso.

---

## Ejemplos de uso

**Pipeline completo:**
```
/blog-pipeline-es "keyword research"
```

**Pipeline para México:**
```
/blog-pipeline-es --country=mx "keyword research"
```

**Seleccionar de CSV:**
```
/blog-pipeline-es
```

**Reanudar desde borrador:**
```
/blog-pipeline-es --from=draft "keyword research"
```

**Solo investigación + outline (parar temprano):**
```
/blog-pipeline-es --to=outline "keyword research"
```
