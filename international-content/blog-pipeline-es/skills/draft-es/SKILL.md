---
name: draft-es
description: Expand an outline into a full article draft in Spanish for the Ahrefs ES blog. Use this when drafting articles in Spanish, creating content for ahrefs.com/blog/es/, or writing any Spanish-language SEO/marketing article.
argument-hint: [outline-file]
allowed-tools: Read, Write
---

# Draft Skill (Español)

Expande un outline estructurado en un artículo completo en español, siguiendo las convenciones del blog de Ahrefs en español.

**Importante**: Este skill usa redacción sección por sección para mantener calidad constante. Cada sección H2 se escribe de forma independiente para evitar degradación de calidad en secciones posteriores.

## Input

**Ruta al archivo de outline** — El outline del paso anterior (de `/outline`)

---

## Referencia de Estilo

Antes de redactar, lee `./reference/style-reference-es.md` para calibrar voz y tono. Si el archivo no existe, busca el directorio padre del skill para `reference/style-reference-es.md`.

---

## Principios de Escritura (Español)

1. **Ejemplos específicos para cada punto** — Nunca hagas una afirmación sin ilustrarla con datos concretos
2. **Primera persona plural** ("analizamos", "encontramos") para datos de Ahrefs; segunda persona singular ("puedes", "necesitas") para instrucciones
3. **Opiniones directas** — Toma posición, no seas tibio
4. **Datos exhaustivos** — Cubre temas en profundidad
5. **Estructura MECE** — Secciones mutuamente excluyentes, cobertura colectivamente exhaustiva
6. **Principio BLUF** — Lo más importante primero
7. **Personalidad** — Ser humano, no robótico
8. **Evitar lenguaje exagerado** — Nada de "revolucionario", "increíble", "game-changer"
9. **Referenciar Ahrefs naturalmente** — Solo cuando genuinamente ayude al lector

---

## Guía de Estilo Español

### Voz y Tono
- Tuteo informal pero profesional
- **Español neutro** con ligera tendencia a español de España (vale para LATAM)
- Tono casual — Empezar frases con "Pero..." o "Y lo más interesante:" es válido
- Sin palabrotas ni lenguaje inapropiado
- Directo, no formal ni académico

### Estructura de Frases y Párrafos
- **Un pensamiento por frase**
- **Máximo 3 líneas por párrafo** (mantiene el contenido escaneable)
- **Sin relleno** — Eliminar muletillas como "En este artículo vamos a ver..."
- **Lenguaje simple** — "vimos" no "constatamos"

### Formato de Números
- Puntos para miles: 3.922
- Comas para decimales: 45,7%
- Sin espacio antes de %: 45,7% (no 45,7 %)

### Términos Técnicos
Mantener en inglés: SEO, SEM, CPC, SERP, keyword, backlink, share of voice, AI Overviews, ChatGPT, Domain Rating, traffic potential, keyword difficulty

Traducir: menciones, visibilidad en IA, fuentes citadas, cuota de mercado, posicionamiento web

### Longitud
- Objetivo: **1.000-3.000 palabras** (según el outline)
- **Lo más corto posible** — Educar de forma simple, no rellenar para llegar a un conteo
- Excluir detalles que solo interesan al 1% de lectores

### Subtítulos
- **H2-H6** en jerarquía
- **Tipo oración** ("Cómo funciona el SEO local" no "Cómo Funciona El SEO Local")
- **Un punto por heading**
- **Menos de 15 palabras**
- **Nunca poner subtítulos seguidos** — Siempre texto introductorio entre heading y subheading

---

## Estructura de Contenido

### Introducción (Menos de 100 palabras)

Fórmula **PAS**: Problema → Agitar → Solución

1. **Problema**: Dato impactante o afirmación contraintuitiva
2. **Agitar**: Por qué importa o qué pasa si lo ignoras
3. **Solución**: Adelanto de lo que el artículo enseña

Ejemplo:
> El 96,55% de las páginas web no reciben tráfico orgánico de Google. No es una exageración — es un dato real de nuestro estudio de 14 millones de páginas. Pero la buena noticia es que no tiene por qué ser así. En esta guía te muestro exactamente cómo hacer SEO en 2026, paso a paso.

### Secciones del Cuerpo

Pirámide invertida para cada sección:
1. **Lo imprescindible** primero (el punto esencial)
2. **Lo complementario** después (detalles, contexto)

#### Escribir Definiciones

Formato: `[Término] [abreviatura si necesaria] [conjunción] [definición en 1-3 frases]`

> **¿Qué es el share of voice?**
> El share of voice (SOV) mide el porcentaje de consultas relevantes en las que una marca aparece mencionada. Si tu SOV es del 40%, significa que en 4 de cada 10 preguntas sobre tu sector, la IA te menciona.

#### Escribir Explicaciones

Siempre explicar **qué** Y **por qué**:

> Instala un plugin de compresión de imágenes como ShortPixel. Esto reduce el tamaño de archivo sin pérdida visible de calidad, lo que mejora la velocidad de carga — un factor de ranking confirmado por Google.

No solo:
> ~~Instala un plugin de compresión de imágenes.~~

#### Usar Ejemplos

Cada punto importante necesita un ejemplo concreto:

> Los backlinks no duran para siempre. En los últimos 7 días, ahrefs.com perdió 847 dominios de referencia — así funciona la web. Las páginas se borran, los sitios cierran y los webmasters cambian de opinión.

Los ejemplos deben ser:
- Específicos (números reales, sitios reales)
- Relevantes al punto que se está haciendo
- De experiencia personal cuando sea posible

---

## Referencias a Productos Ahrefs

Usar las URLs en español cuando existan:
- Blog: `https://ahrefs.com/blog/es/[slug]`
- Brand Radar: `https://ahrefs.com/es/brand-radar`
- Herramientas: URLs base (la interfaz se traduce automáticamente)

**REGLA CRÍTICA — Enlaces internos solo en el mismo idioma:**
- Solo enlazar a artículos del blog de Ahrefs que existan en español (`ahrefs.com/blog/es/`).
- **NUNCA** enlazar a artículos del blog en inglés (`ahrefs.com/blog/[slug-en]/`).
- Si necesitas referenciar información de un artículo que solo existe en inglés, incluir el dato como texto sin enlace.
- Las URLs de productos de Ahrefs en español (`ahrefs.com/es/brand-radar`, `ahrefs.com/es/site-audit`, etc.) SÍ se pueden enlazar.

**Cómo referenciar:**
> Para ver quién enlaza a tus competidores, entra en Site Explorer de Ahrefs, introduce su dominio y revisa el informe de "Backlinks" — puedes filtrar por enlaces dofollow y ordenar por Domain Rating para encontrar las oportunidades más valiosas.

**No:**
- Forzar menciones donde no encajan
- Sonar como un anuncio
- Afirmar que Ahrefs es la única solución

---

## Conclusión

### Sección "Conclusión" o "Reflexión final"

Escribe una conclusión corta (menos de 150 palabras):
1. Resume el hallazgo principal
2. Proporciona un siguiente paso accionable

Termina con:

> ¿Tienes preguntas? Estamos en [LinkedIn](https://www.linkedin.com/company/ahrefs-en-espanol/posts/?feedView=all) y en [X](https://twitter.com/AhrefsES).

---

## Workflow: Redacción Sección por Sección

### Fase 0: Calibración de Estilo

Leer `./reference/style-reference-es.md` y extraer una **Ficha de Estilo** compacta:

1. **Marcadores de voz** (3 ejemplos de cómo se usa la primera persona, giros casuales, señales de opinión)
2. **Ejemplos BLUF** (2 aperturas de sección que lideran con el punto principal)
3. **Patrones de transición** (2 ejemplos de cómo se conectan las secciones)
4. **Marcadores de especificidad** (2 ejemplos de cómo se integran números y datos)

Crear Ficha de Estilo de ~200 palabras.

### Fase 1: Setup

1. Leer el outline
2. Extraer metadata: keyword, tesis, conteo de palabras objetivo, notas de voz
3. Crear archivo de borrador con header de metadata

### Fase 2: Redacción Sección por Sección

Para cada sección H2:

1. **Anclar en referencia**: Citar UN pasaje de la referencia de estilo que ejemplifique lo que esta sección necesita
2. **Cargar contexto**: Ficha de estilo + metadata + outline de esta sección + último párrafo de la sección anterior + header de la siguiente
3. **Escribir la sección completa**: BLUF al inicio, al menos un ejemplo específico, voz en primera persona/segunda persona, notas de screenshots donde ayude
4. **Añadir al borrador**
5. **Siguiente sección**

### Fase 3: Introducción y Conclusión

Escribir la introducción DESPUÉS de las secciones del cuerpo:
- Usar fórmula PAS (menos de 100 palabras)

Escribir la conclusión AL FINAL:
- CTA hacia LinkedIn/X de Ahrefs ES

### Fase 4: Revisión de Ensamblaje

1. Leer el borrador completo de principio a fin
2. Verificar transiciones entre secciones
3. Verificar consistencia de terminología y voz
4. Actualizar metadata (conteo de palabras, status)

---

## Output

Guardar en `./4-drafts/[keyword-slug].md`

---

## Checklist de Calidad

| Verificación | Requisito |
|-------------|-----------|
| Ejemplos | Cada punto importante tiene ejemplo específico |
| Voz | Tuteo + primera persona plural consistente |
| Opiniones | Posición clara, no ambigüedad |
| Relleno | Sin muletillas ni frases de relleno |
| Párrafos | Máximo 3 líneas cada uno |
| Subtítulos | Tipo oración, menos de 15 palabras |
| Lenguaje | Sin exageraciones (revolucionario, increíble) |
| Ahrefs | Referencias naturales y útiles, URLs en español |
| Longitud | Dentro del objetivo de palabras |
| Intro | Menos de 100 palabras, usa PAS |
| Conclusión | CTA a LinkedIn/X de Ahrefs ES |
| Números | Formato español (3.922 para miles, 45,7% para decimales) |
| Términos | SEO/SERP/CPC en inglés, "menciones"/"visibilidad" en español |
