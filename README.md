# Portfolio

**English** · [Español](README.es.md)

Personal portfolio website in Spanish and English. Plain HTML5 + CSS3 with a single small JavaScript file (language switcher and screenshot viewer). No dependencies, no build step.

## Run locally

- Open `index.html` directly in the browser (double click), or
- from this folder: `python3 -m http.server 8000` and visit http://localhost:8000

## Structure

```text
portfolio/
├── index.html        Home: intro, about me, skills, experience, education
├── projects.html     Projects, with enlargeable screenshots
├── contact.html      Contact
├── css/styles.css    All styles (colour variables at the top)
├── js/script.js      ES/EN language switcher + screenshot viewer
└── assets/
    ├── images/       Photo and project screenshots (.webp)
    ├── docs/         CV (PDF)
    └── icons/        favicon.svg
```

## Features

- **Two languages (ES/EN).** The Spanish text lives in the HTML; the English translations live in the `EN` dictionary in `js/script.js`. The chosen language is saved in `localStorage` and applied on every page.
- **Dark mode.** It follows the visitor's system setting (`prefers-color-scheme`).
- **Screenshot viewer.** Clicking a project screenshot opens it enlarged in a `<dialog>`; it closes with Esc, the × button or a click anywhere. Without JavaScript, each screenshot is a plain link that opens the image.
- **Works without JavaScript.** The page is fully readable in Spanish even if the script does not load.

## Adding or changing content

### Translatable text

1. Write the Spanish text in the HTML with `data-i18n="my.key"`.
2. Add `'my.key': '…'` to the `EN` dictionary in `js/script.js`.

For attributes (`alt`, `aria-label`, `content`…) use `data-i18n-attr="attribute:my.key"`. If a key is missing, the browser console shows a warning and the Spanish text is kept.

### A new project

1. In `projects.html`, duplicate one of the `<li>` blocks in the project list and change its `id`s (`p5-title`…) and `data-i18n` keys (`proj.5.…`).
2. Add the screenshot to `assets/images/` as `.webp`, at **1060×662** (16:10 ratio, the same as the others). If the original has a different ratio, pad it with its background colour instead of cropping, so no text is cut off:

   ```bash
   convert capture.png -background white -gravity center \
     -extent <width>x<16:10 height> -resize 1060x662\! -quality 85 assets/images/project-x.webp
   ```

3. Keep the screenshot wrapped in its `<a class="zoom" href="…">` link (same path as the `<img>`) so it can be enlarged.
4. Add the English translations (`proj.5.title`, `proj.5.desc`, `proj.5.alt`…) to `js/script.js`.
