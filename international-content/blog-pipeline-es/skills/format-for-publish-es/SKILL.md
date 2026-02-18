---
name: format-for-publish-es
description: Formatear un borrador en español con shortcodes de WordPress y exportar a .docx
argument-hint: [draft-file]
allowed-tools: Read, Write, Bash
---

# Format for Publish Skill (Español)

Transforma un borrador finalizado en español en un documento listo para WordPress con shortcodes de Ahrefs, y exporta a formato .docx.

## Input

**Ruta al borrador** — Path al borrador citado (e.g., `./5-drafts-cited/visibilidad-ia.md`)

## Dependencias

**pandoc** es necesario para la exportación a .docx. Instalar:
```bash
# macOS
brew install pandoc
# Ubuntu/Debian
sudo apt-get install pandoc
```

Si pandoc no está instalado, el skill guarda el .md formateado y nota que se necesita conversión manual.

---

## Referencia de shortcodes de WordPress

### Estructura de contenido

| Shortcode | Propósito | Cuándo usar |
|-----------|----------|-------------|
| `[intro_text][/intro_text]` | Envuelve el párrafo de introducción | Primer párrafo después del título |
| `[intro_toc]` | Auto-genera tabla de contenidos | Después de la intro, antes del primer H2 |
| `[post_nav_link]` | Ancla de navegación de sección | Envuelve cada heading H2 |

### Callouts y destacados

| Shortcode | Propósito | Cuándo usar |
|-----------|----------|-------------|
| `[recommendation title="Consejo"][/recommendation]` | Caja de consejo destacada | Consejos accionables, recomendaciones de herramientas |
| `[sidenote][/sidenote]` | Nota al margen | Info tangencial pero útil |
| `[editor_note][/editor_note]` | Atribución de editor | Comentarios editoriales o actualizaciones |

### Citas y atribución

| Shortcode | Propósito | Cuándo usar |
|-----------|----------|-------------|
| `[blockquote]` | Cita estilizada con autor | Citas de expertos, testimonios |

### Media y widgets

| Shortcode | Propósito | Cuándo usar |
|-----------|----------|-------------|
| `[caption][/caption]` | Imagen con pie de foto | Todas las imágenes que necesiten contexto |
| `[toolWidget]` | Embed de herramienta Ahrefs | Al referenciar herramientas gratuitas de Ahrefs |

### Cierre

| Shortcode | Propósito | Cuándo usar |
|-----------|----------|-------------|
| `[further_reading][/further_reading]` | Lista de artículos relacionados | Final del artículo, 2-4 posts relacionados |

---

## Sintaxis de shortcodes

### intro_text
```
[intro_text]Primer párrafo del artículo que engancha al lector.[/intro_text]
```

### post_nav_link
```
[post_nav_link link_text="Título de la sección" section="titulo-de-la-seccion"]

## Título de la sección

[/post_nav_link]
```

**Reglas para el slug de sección:**
- Minúsculas
- Guiones en lugar de espacios
- Sin caracteres especiales (ni tildes ni ñ en el slug)
- Sin signos de interrogación
- Ejemplo: "¿Qué es el SEO local?" → `section="que-es-el-seo-local"`
- Ejemplo: "Cómo funciona Brand Radar" → `section="como-funciona-brand-radar"`

**Transliteración de caracteres españoles en slugs:**
- á → a, é → e, í → i, ó → o, ú → u
- ñ → n
- ü → u

### recommendation
```
[recommendation title="Consejo"]

Tu contenido de consejo aquí. Puede incluir párrafos, listas e imágenes.

[/recommendation]
```

**Títulos comunes en español:** "Consejo", "Consejo pro", "Importante", "Nota", "No te pierdas..."

### sidenote
```
[sidenote]

Contexto adicional que es útil pero no esencial para el punto principal.

[/sidenote]
```

### editor_note
```
[editor_note editor="Nombre del Editor" editor_photo="URL_FOTO" editor_job="Cargo"]

Comentario editorial o aviso de actualización.

[/editor_note]
```

### blockquote
```
[blockquote size="small" author="John Mueller" author_photo="https://ahrefs.com/blog/wp-content/uploads/2022/02/john-mueller-google.png" author_job="Search Advocate," link_text="Google" link_url="https://www.google.com"]

_El texto citado va aquí, normalmente en cursiva._

[/blockquote]
```

### caption
```
[caption id="attachment_000000" align="alignnone" width="1365"]![Texto alt](URL_IMAGEN) Pie de foto describiendo la imagen.[/caption]
```

**Nota:** Usar ID placeholder `attachment_000000` — el CMS asignará el ID real al subir.

### toolWidget
```
[toolWidget tool="Keyword Generator" heading="Encuentra miles de ideas de keywords en segundos"]
```

**Herramientas disponibles (headings en español):**
- `Website Traffic Checker` — "Consulta las estimaciones de tráfico de búsqueda de cualquier sitio web"
- `Website Authority Checker` — "Comprueba la autoridad de tu dominio"
- `Backlink Checker` — "Echa un vistazo al poder de nuestra herramienta premium"
- `Keyword Generator` — "Encuentra miles de ideas de keywords en segundos"
- `Keyword Difficulty Checker` — "Descubre lo difícil que será entrar en el top 10"

### further_reading
```
[further_reading]

- [Título del artículo 1](https://ahrefs.com/blog/es/slug-1/)
- [Título del artículo 2](https://ahrefs.com/blog/es/slug-2/)
- [Título del artículo 3](https://ahrefs.com/blog/es/slug-3/)

[/further_reading]
```

**REGLA CRÍTICA — Enlaces internos solo en el mismo idioma:**
- Solo incluir artículos del blog de Ahrefs en español (`/blog/es/`).
- **NUNCA** incluir artículos en inglés (`/blog/[slug-en]/`) en further_reading ni en ningún otro enlace interno del artículo.
- Si no hay suficientes artículos en español relacionados, incluir menos artículos (mínimo 1) en lugar de rellenar con artículos en inglés.
- Las URLs de productos de Ahrefs en español (`ahrefs.com/es/brand-radar`, etc.) SÍ se pueden enlazar.

---

## Workflow

### Fase 1: Leer y analizar borrador

1. **Leer el borrador** desde la ruta proporcionada
2. **Identificar elementos** que necesitan shortcodes:
   - Párrafo de introducción (primer párrafo después del título)
   - Todos los headings H2 (necesitan post_nav_link)
   - Consejos o recomendaciones (convertir a [recommendation])
   - Citas de expertos (convertir a [blockquote])
   - Placeholders de imágenes (convertir a [caption])
   - Menciones de herramientas Ahrefs (considerar [toolWidget])

### Fase 2: Aplicar shortcodes

#### 1. Sección de intro
```markdown
# Título

Primer párrafo...
```
Se convierte en:
```
# Título

[intro_text]Primer párrafo...[/intro_text]

Resto de la intro...

[intro_toc]
```

#### 2. Secciones H2
```markdown
## ¿Qué es la visibilidad en IA?

Contenido...
```
Se convierte en:
```
[post_nav_link link_text="¿Qué es la visibilidad en IA?" section="que-es-la-visibilidad-en-ia"]

## ¿Qué es la visibilidad en IA?

[/post_nav_link]

Contenido...
```

#### 3. Consejos y recomendaciones
Buscar patrones como:
- Prefijos "Consejo:" o "Consejo pro:"
- Párrafos que empiezan con "Puedes usar Ahrefs..."
- Consejos accionables que merecen destacarse

#### 4. Citas de expertos
Convertir blockquotes con atribución al formato de shortcode.

#### 5. Imágenes
Convertir placeholders `[CAPTURA: descripción]` a:
```
[caption id="attachment_000000" align="alignnone" width="1365"]![Descripción](URL_IMAGEN_PLACEHOLDER) Descripción de lo que muestra la imagen.[/caption]
```

#### 6. Further reading
Añadir al final, antes del CTA de redes sociales:
```
[further_reading]

- [Artículo relacionado 1](https://ahrefs.com/blog/es/slug-1/)
- [Artículo relacionado 2](https://ahrefs.com/blog/es/slug-2/)
- [Artículo relacionado 3](https://ahrefs.com/blog/es/slug-3/)

[/further_reading]
```

### Fase 3: Limpieza

1. **Eliminar header de metadata** (Keyword objetivo, Conteo de palabras, Status, Ficha de estilo)
2. **Eliminar sección de notas del borrador** al final
3. **Eliminar comentarios HTML** (`<!-- ... -->`)
4. **Asegurar espaciado correcto** alrededor de shortcodes (líneas en blanco antes/después)
5. **Verificar que el CTA final** enlaza a las redes en español de Ahrefs:
   - LinkedIn: https://www.linkedin.com/company/ahrefs-en-espanol/posts/?feedView=all
   - X: https://twitter.com/AhrefsES

### Fase 4: Exportar a .docx

Usar pandoc para convertir:

```bash
pandoc input.md -o output.docx --from markdown --to docx
```

Si pandoc no está instalado, guardar como .md con nota de conversión manual necesaria.

---

## Output

1. **Markdown formateado** guardado en `7-publish/[slug].md`
2. **Documento Word** guardado en `7-publish/[slug].docx`

---

## Ejemplo de uso

```
/format-for-publish-es ./5-drafts-cited/visibilidad-ia.md
```

Crea:
- `7-publish/visibilidad-ia.md` (formateado con shortcodes)
- `7-publish/visibilidad-ia.docx` (documento Word)
