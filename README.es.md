# Portfolio

[English](README.md) · **Español**

Portfolio personal en español e inglés. HTML5 + CSS3 con un único script de JavaScript pequeño (selector de idioma y visor de capturas). Sin dependencias ni compilación.

## Ejecutar en local

- Abre `index.html` directamente en el navegador (doble clic), o
- desde esta carpeta: `python3 -m http.server 8000` y visita http://localhost:8000

## Estructura

```text
portfolio/
├── index.html        Inicio: presentación, sobre mí, habilidades, experiencia, formación
├── projects.html     Proyectos, con capturas ampliables
├── contact.html      Contacto
├── css/styles.css    Todos los estilos (variables de color al principio)
├── js/script.js      Selector de idioma ES/EN + visor de capturas
└── assets/
    ├── images/       Foto y capturas de los proyectos (.webp)
    ├── docs/         CV (PDF)
    └── icons/        favicon.svg
```

## Funcionalidades

- **Dos idiomas (ES/EN).** El texto en español vive en el HTML; las traducciones al inglés, en el diccionario `EN` de `js/script.js`. El idioma elegido se guarda en `localStorage` y se aplica en todas las páginas.
- **Modo oscuro.** Sigue la configuración del sistema del visitante (`prefers-color-scheme`).
- **Visor de capturas.** Al pulsar la captura de un proyecto se abre ampliada en un `<dialog>`; se cierra con Esc, con el botón × o pulsando en cualquier parte. Sin JavaScript, cada captura es un enlace normal que abre la imagen.
- **Funciona sin JavaScript.** La página se lee completa en español aunque el script no cargue.

## Añadir o cambiar contenido

### Textos traducibles

1. Escribe el texto en español en el HTML con `data-i18n="mi.clave"`.
2. Añade `'mi.clave': '…'` al diccionario `EN` de `js/script.js`.

Para atributos (`alt`, `aria-label`, `content`…) usa `data-i18n-attr="atributo:mi.clave"`. Si falta una clave, la consola del navegador muestra un aviso y se mantiene el texto en español.

### Un proyecto nuevo

1. En `projects.html`, duplica uno de los bloques `<li>` de la lista de proyectos y cambia sus `id` (`p5-title`…) y sus claves `data-i18n` (`proj.5.…`).
2. Añade la captura a `assets/images/` en `.webp`, a **1060×662** (proporción 16:10, igual que las demás). Si la original tiene otra proporción, rellénala con su color de fondo en vez de recortarla, para que no se corte texto:

   ```bash
   convert captura.png -background white -gravity center \
     -extent <ancho>x<alto 16:10> -resize 1060x662\! -quality 85 assets/images/proyecto-x.webp
   ```

3. Mantén la captura dentro de su enlace `<a class="zoom" href="…">` (con la misma ruta que el `<img>`) para que se pueda ampliar.
4. Añade las traducciones al inglés (`proj.5.title`, `proj.5.desc`, `proj.5.alt`…) en `js/script.js`.
