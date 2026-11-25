# Página de guías de estudio

Sitio estático publicado con GitHub Pages desde la rama `main` (carpeta raíz).
Repositorio: `Juaincha/resumen-dinamica`. URL pública: https://juaincha.github.io/resumen-dinamica/

No hay paso de compilación: lo que está en `main` es lo que se publica.

El sitio se publica con GitHub Actions mediante `.github/workflows/pages.yml` (cada push a `main` lanza una ejecución titulada con el mensaje del commit). No hay que volver a "Deploy from a branch" en la configuración de Pages.

## Estructura

```
index.html      Portada: lista las guías leyendo guias.js. No se edita para agregar guías.
guias.js        Lista de guías (window.GUIAS). Se regenera a partir de las etiquetas meta.
guias/          Una página HTML autocontenida por guía.
img/            Favicon e imágenes de vista previa para compartir (1200 × 630).
resumenes/      PDFs originales de las ayudantías. Está en .gitignore y nunca se sube.
.nojekyll       Evita que GitHub Pages procese el sitio con Jekyll.
```

## Cómo se agrega una guía

Normalmente Sebastián deja una guía nueva en `guias/` (la hace en el chat de Claude y queda escrita en esta carpeta). Cuando pida "publica las guías nuevas" o algo parecido:

1. Revisa cada archivo nuevo o modificado en `guias/`:
   - El nombre del archivo está en minúsculas, sin tildes ni espacios, con el formato `curso-fuente-tema.html`. Ejemplo: `fis1514-ayudantia-13-newton-rotacional.html`. Si no cumple, renómbralo.
   - Dentro del `<head>` tiene estas cinco etiquetas. Si falta alguna, agrégala deduciendo el valor del contenido de la guía:
     ```html
     <meta name="guia-curso" content="FIS1514 Dinámica">
     <meta name="guia-titulo" content="Newton rotacional y momentum angular">
     <meta name="guia-fuente" content="Ayudantía 13">
     <meta name="guia-fecha" content="2026-11-11">
     <meta name="guia-temas" content="Torque, Momentum angular, Rodadura">
     ```
   - Al principio del `<header>` hay un enlace `<a href="../index.html">← Todas las guías</a>`. Si no está, agrégalo con el mismo estilo que la guía de ejemplo.
   - Tiene el bloque de vista previa para compartir (etiquetas `og:` y `twitter:`, favicon y `theme-color`), igual que las guías existentes, con su propia URL, título, descripción e imagen. Las URL deben ser absolutas (`https://juaincha.github.io/resumen-dinamica/...`).
   - Existe su imagen de vista previa en `img/og-<curso>-<fuente>.jpg`, de 1200 × 630 px y menos de 300 KB, con el mismo estilo que las demás (fondo azul, título en blanco, una ilustración del tema a la derecha). Si no puedes generarla, usa `img/og-portada.jpg` y avísale a Sebastián.
2. Regenera `guias.js` con todas las guías de `guias/` a partir de sus etiquetas meta. Mantén el formato del archivo actual: `archivo`, `curso`, `titulo`, `fuente`, `fecha` y `temas` como lista.
3. Abre `index.html` y cada guía nueva en un navegador o con una revisión rápida, y verifica que no haya errores de JavaScript en la consola.
4. Haz commit con un mensaje en español que nombre las guías (por ejemplo, `Agrega guía FIS1514 Ayudantía 14: trabajo y energía`) y luego push a `main`.
5. Responde con la URL pública de cada guía nueva. GitHub Pages tarda uno o dos minutos en actualizarse.

## Si Sebastián te pasa un PDF para que hagas tú la guía

Guarda el PDF en `resumenes/` y crea la guía siguiendo el estilo de `guias/fis1514-ayudantia-13-newton-rotacional.html`:

- Una sola página HTML autocontenida en español de Chile: CSS y JS dentro del archivo, solo fuentes de Google Fonts.
- Banda azul de título, navegación por secciones, modo claro y oscuro, y que funcione bien en celular (400 px).
- Teoría completa del resumen, ampliada para que se pueda estudiar solo con la guía.
- Cada figura interactiva va dentro de su sección, en la columna derecha junto al texto que explica (nunca suelta arriba de la página, antes de la primera sección).
- En el panel de cada figura, los botones y controles van justo debajo de la figura, y las tarjetas de resultados después. El último control lleva el atributo `data-keep`, y la guía incluye el script `fitSticky` (cópialo de una guía existente) para que la figura y sus controles queden siempre a la vista mientras el panel acompaña la lectura.
- Figuras interactivas que muestren el mecanismo, ejemplos resueltos paso a paso, una sección de errores típicos, ejercicios con solución en `<details>` y preguntas rápidas de concepto.
- Verifica la aritmética de cada ejemplo y ejercicio ejecutando el cálculo, no de memoria.
- Al pie, indica de qué ayudantía sale y aclara que los ejemplos numéricos son de práctica.

Después sigue los pasos de la sección anterior.

## Reglas

- Nunca subas PDFs ni otro material original del curso. Solo se publican las guías HTML.
- No cambies el diseño de `index.html` ni de las guías existentes salvo que Sebastián lo pida.
- No hagas `push --force` ni reescribas el historial.
- Si algo falla (autenticación de `gh`, Pages, conflictos), explica qué pasó y qué tiene que hacer Sebastián, en vez de intentar soluciones arriesgadas.
