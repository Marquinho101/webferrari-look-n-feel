# webferrari-look-n-feel

Sandbox de diseño para **La Pizzanesa** · No toca producción.

## Qué es

Prototipo HTML standalone (sin build, sin Node, sin framework) que replica la web de La Pizzanesa con un sistema de **CSS skins** intercambiables. El objetivo es explorar rediseños visuales, compartir el archivo con IAs externas (GEMA, Gemini, Perplexity) y traducir los tokens ganadores a `webferrari` (Next.js + Tailwind) cuando se apruebe un look.

## Cómo usarlo

1. Abrir `index.html` en el navegador — doble clic, no necesita servidor.
2. Usar los botones **Marca / Retro 80s / Kids** (toolbar inferior derecho) para cambiar el skin al instante.
3. El campo **☁ cloud** viene pre-configurado con `lastpos` — las imágenes de productos cargan solas.
4. Para prototipar un skin nuevo: copiar el bloque `body.retro{...}` en el CSS, darle un nombre de clase y añadir un botón al toolbar.

## Estructura

```
index.html    — todo en un solo archivo: CSS tokens, HTML, datos JS, render engine
README.md     — este archivo
```

## Sincronización con producción (sprint W8 · 2026-08-06)

| Cambio | Estado |
|---|---|
| Imágenes desde Cloudinary `lastpos` (cloud por defecto) | ✅ |
| Copy "Pedir" (sin flecha) | ✅ |
| Logos proveedores: Mutti, Caputo, Albe + bebidas | ✅ |
| Flash banner (2 líneas en mobile, 1 en desktop) | ✅ |
| WCAG muted contrast mejorado (alpha .65) | ✅ |
| Hero Carnivora opacidad sincronizada con prod (53%) | ✅ |

## Para GEMA / Gemini

Pasar el `index.html` completo como contexto. Prompt tipo:

> "Este es el prototipo HTML standalone de La Pizzanesa. Los skins están en el bloque `<style>`: `:root` es el skin Marca (default), `body.retro` y `body.kids` son los alternativos. Quiero que diseñes un nuevo skin llamado `[NOMBRE]` con la siguiente estética: [DESCRIPCIÓN]. Devuelve: 1) el bloque CSS del nuevo skin, 2) el botón para añadir al toolbar."

Cuando el skin esté aprobado por Marco, trasladar los tokens a `tailwind.config.ts` y los cambios visuales a los componentes `.tsx` de `webferrari`.

## Relación con producción

| Repo | Propósito | Deploy |
|---|---|---|
| `webferrari` | App Next.js 15, código fuente real | Vercel → webferrari.lapizzanesa.pizza |
| `webferrari-look-n-feel` | Sandbox visual (este repo) | Solo GitHub, no hay deploy |

**Flujo:** look-n-feel → aprobación Marco → webferrari → Vercel → DNS cutover → lapizzanesa.pizza
