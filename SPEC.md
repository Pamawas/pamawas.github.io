# Pamawas — Build Spec
 
What to build this with, and how it should be structured. Companion to `design.md` (visual system) — this doc covers the technical stack only.
 
## Recommendation: Astro, static output, deployed to GitHub Pages
 
The current site is a single static HTML file hosted on GitHub Pages (`pamawas.github.io`, repo `Pamawas/pamawas.github.io`). That constraint doesn't change — no server, no runtime backend. What changes is how the HTML gets *authored*, so the design system in `design.md` stays consistent as the site grows past one page.
 
**Use [Astro](https://astro.build) in static output mode (`output: 'static'`).** Reasons:
- Ships zero JS by default — matches the "no unnecessary motion/interactivity" design principle.
- Component-based (`.astro` files) without needing React/Vue/a client framework — this is a marketing/docs site, not an app.
- Builds straight to static HTML/CSS, deployable to GitHub Pages with the official `withastro/action` GitHub Action.
- Trivial to add MDX later if docs pages are needed.
If you'd rather not introduce a build step at all, **plain HTML + CSS (no framework)** — i.e. what exists today — is a legitimate fallback. Only reach for Astro once the site grows past ~2–3 pages or the same header/footer/evidence-card markup needs to be reused.
 
Do **not** use a full client framework (Next.js, Nuxt, CRA/Vite+React) for this site — there's no interactivity, state, or data-fetching that needs it, and it would work against the "static, honest, no fabricated complexity" ethos of the product itself.
 
### Add Tailwind CSS (v4) once dark mode is in scope
 
Plain hand-written CSS custom properties work fine for a single-theme site, but once every token needs a light *and* dark value, Tailwind's `dark:` variant is worth the dependency — it avoids duplicating every rule under a `.dark` selector by hand. Use **Tailwind v4** with its CSS-first config (`@theme`), which maps directly onto the token tables in `design.md`:
 
```css
/* src/styles/tokens.css */
@import "tailwindcss";
 
@theme {
  --color-paper: #F4F4F0;
  --color-paper-warm: #EFEEE4;
  --color-ink: #1B1E1C;
  --color-fjord: #2F5049;
  --color-falu: #9C4630;
  --color-ochre: #A97A2E;
  --color-moss: #546E51;
  /* ...remaining tokens from design.md */
}
 
:root.dark {
  --color-paper: #14181B;
  --color-paper-warm: #1B2023;
  --color-ink: #EDEEE8;
  --color-fjord: #6FA89C;
  --color-falu: #D9805F;
  --color-ochre: #D9AC63;
  --color-moss: #8FB589;
  /* ...remaining dark values from design.md */
}
```
 
Install: `@astrojs/tailwind` integration in `astro.config.mjs`. Set `darkMode: 'class'` behavior by toggling `class="dark"` on `<html>` (see "Dark mode mechanics" in `design.md`).
 
Keep using plain CSS (not Tailwind utility classes) for the two custom, non-utility bits — the contour SVG motif and the claim-row left-edge treatment — since those aren't naturally expressed as utility classes. Tailwind handles spacing, typography scale, and the color system; hand-written CSS handles the two bespoke visual signatures.
 
If dark mode is *not* in scope yet, stick with plain CSS custom properties as originally spec'd — don't add Tailwind purely for a single-theme, low-component-count site.
 
## Project structure (Astro)
 
```
/
├── astro.config.mjs
├── package.json
├── public/
│   └── favicon.svg
├── src/
│   ├── components/
│   │   ├── Header.astro
│   │   ├── Hero.astro
│   │   ├── ContourMotif.astro      # the signature SVG, as one reusable component
│   │   ├── EvidenceFlow.astro      # typed-claim list, props: title, run id, severity, claims[]
│   │   ├── WorkflowStep.astro
│   │   ├── TrustItem.astro
│   │   ├── CodePanel.astro
│   │   └── Footer.astro
│   ├── layouts/
│   │   └── BaseLayout.astro        # <head>, font links, meta tags, header/footer slot
│   ├── styles/
│   │   └── tokens.css              # CSS custom properties from design.md, as-is
│   └── pages/
│       └── index.astro
└── .github/workflows/deploy.yml
```
 
Keep `tokens.css` a direct, unmodified translation of the color/type tables in `design.md` — it should be possible to diff the two and catch drift.
 
## Fonts
 
Self-host or use Google Fonts CDN as today:
- Archivo (700, 800)
- Manrope (400, 500, 600, 700)
- IBM Plex Mono (400, 500)
If self-hosting for performance, use `@fontsource/archivo`, `@fontsource/manrope`, `@fontsource/ibm-plex-mono` npm packages and import in `BaseLayout.astro`.
 
## Config
 
`astro.config.mjs`:
```js
import { defineConfig } from 'astro/config';
 
export default defineConfig({
  site: 'https://pamawas.github.io',
  output: 'static',
});
```
 
## Deployment (GitHub Pages)
 
Use the official Astro GitHub Actions workflow — build on push to `main`, deploy the `dist/` output to Pages:
 
```yaml
# .github/workflows/deploy.yml
name: Deploy to GitHub Pages
on:
  push:
    branches: [main]
permissions:
  contents: read
  pages: write
  id-token: write
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: withastro/action@v3
  deploy:
    needs: build
    runs-on: ubuntu-latest
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    steps:
      - id: deployment
        uses: actions/deploy-pages@v4
```
 
Repo settings → Pages → Source: "GitHub Actions."
 
## What NOT to add
 
- No client-side JS framework/state library — the only JS on the page should be the dark-mode toggle script (a few lines: read `localStorage`/`prefers-color-scheme`, toggle a class). Nothing else needs it.
- No CSS framework beyond Tailwind for tokens/utilities as described above — don't add a component library (Bootstrap, MUI, shadcn, etc.) on top of it.
- No CMS — copy changes are infrequent and reviewed like code; keep it in the `.astro` files.
- No analytics/tracking scripts unless explicitly requested later — keep the page's actual footprint matching its "bounded, no unnecessary side effects" product ethos.
## Local development
 
```
npm create astro@latest -- --template minimal
npm install
npm run dev      # localhost:4321
npm run build    # outputs to dist/
npm run preview
```