---
name: preview-es
description: Generar preview HTML con estilo Ahrefs de un borrador en español
argument-hint: [draft-file]
allowed-tools: Read, Write, Bash
---

# Preview Skill (Español)

Genera un preview HTML con estilo del blog de Ahrefs a partir de un borrador en markdown en español.

## Input

- `$ARGUMENTS`: Ruta a un borrador en markdown (e.g., `./5-drafts-cited/visibilidad-ia.md`)

## Workflow

1. **Leer el borrador** desde la ruta proporcionada
2. **Extraer el título** del primer heading H1 (`# Título`)
3. **Convertir markdown a HTML**:
   - Headings: `# ` → `<h1>`, `## ` → `<h2>`, etc.
   - Párrafos: Texto separado por líneas en blanco → etiquetas `<p>`
   - Listas: `- ` → `<ul><li>`, `1. ` → `<ol><li>`
   - Negrita: `**texto**` → `<strong>`
   - Cursiva: `*texto*` → `<em>`
   - Enlaces: `[texto](url)` → `<a href="url">texto</a>`
   - Código inline: `` `código` `` → `<code>`
   - Bloques de código: ``` → `<pre><code>`
   - Blockquotes: `> ` → `<blockquote>`
   - Imágenes: `![alt](src)` → `<img src="src" alt="alt">`
4. **Leer la plantilla** desde `templates/ahrefs-preview.html` (buscar primero en el directorio del skill ES, luego en el directorio del skill EN como fallback)
5. **Insertar contenido** reemplazando placeholders `{{TITLE}}` y `{{CONTENT}}`
6. **Añadir indicador de idioma**: Añadir `lang="es"` al tag `<html>` para renderizado correcto de caracteres españoles
7. **Derivar nombre de archivo** del input (e.g., `visibilidad-ia.md` → `visibilidad-ia.html`)
8. **Escribir HTML** en `6-preview/[slug].html`
9. **Abrir en navegador**: Ejecutar `open 6-preview/[slug].html`

## Nota sobre caracteres españoles

Asegurarse de que el HTML incluya:
- `<meta charset="UTF-8">` en el `<head>`
- `lang="es"` en el tag `<html>`

Esto garantiza el renderizado correcto de: á, é, í, ó, ú, ñ, ü, ¿, ¡

## Output

- Archivo HTML en `6-preview/[slug].html`
- Se abre automáticamente en el navegador por defecto

## Ejemplo

```
/preview-es ./5-drafts-cited/visibilidad-ia.md
```

Crea `6-preview/visibilidad-ia.html` y lo abre en el navegador.
