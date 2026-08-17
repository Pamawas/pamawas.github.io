# Pamawas — Design System
A minimalist, modern visual language for the Pamawas landing page, built around an original "night → dawn" color story rather than any existing brand's palette.

## 1. Design Philosophy

- **Confidence through restraint.** Large type, generous negative space, almost no decoration. Let the content carry the weight.
- **Color tells the product story.** Ink-indigo dark sections evoke the overnight alert chaos; the single teal accent is the "signal" cutting through noise; dawn amber marks uncertainty. Nothing is colored just to be colorful.
- **Structured rhythm.** Every section follows the same grid and spacing scale so the page feels engineered, not designed.
- **Technical credibility.** Monospace accents for code, metrics, and system labels reinforce that this is infrastructure tooling, not a marketing gimmick.

## 2. Color Palette — "Dusk Signal"

The product's whole premise is a story about time: chaos overnight, clarity by morning. The palette is built around that arc instead of borrowing a competitor's brand color. The base is a near-black **ink-indigo** (not a pure neutral gray/black like most SaaS sites) so the dark sections feel like "night," and the single accent is a **bioluminescent teal-cyan** — the color of a signal cutting through dark water, used exactly like a flare: rare, bright, and always meaningful. A warm **dawn amber** appears only as the secondary signal for "attention/uncertain" states, echoing the literal sunrise in "morning digest."

### Base
| Token | Hex | Usage |
|---|---|---|
| `--bg-primary` | `#0A0E17` | Dark section backgrounds (hero, footer, architecture) — ink-indigo, not flat black |
| `--bg-secondary` | `#FCFCFB` | Light section backgrounds (problem/solution, demo) — warm off-white, not stark white |
| `--bg-surface` | `#F1F1EE` | Cards, code blocks on light sections |
| `--bg-surface-dark` | `#111726` | Cards, code blocks on dark sections |
| `--border` | `#E3E2DD` | Hairline borders on light sections |
| `--border-dark` | `#1E2536` | Hairline borders on dark sections |

### Text
| Token | Hex | Usage |
|---|---|---|
| `--text-primary` | `#0A0E17` | Headlines on light bg |
| `--text-primary-inverse` | `#F4F5F3` | Headlines on dark bg |
| `--text-secondary` | `#54595F` | Body copy on light bg |
| `--text-secondary-inverse` | `#9AA3B5` | Body copy on dark bg |
| `--text-muted` | `#8B8F94` | Captions, labels, timestamps |

### Accent — signal teal
| Token | Hex | Usage |
|---|---|---|
| `--accent` | `#1FD1B8` | Primary CTA, active nav state, key numbers, active data-path in diagrams |
| `--accent-hover` | `#17B39D` | Hover state on accent elements |
| `--accent-subtle` | `#DEFBF5` | Accent tint background (light mode chips) |
| `--accent-glow` | `#1FD1B8` at 15% opacity | Soft radial glow behind hero headline / key stat on dark bg only — the one permitted "decorative" use of color |

### Secondary — dawn amber (used only for attention states, never as a second CTA color)
| Token | Hex | Usage |
|---|---|---|
| `--amber` | `#F0A83C` | HYPOTHESIS status, "needs attention" flags, warm highlight inside the demo digest |
| `--amber-subtle` | `#FDF1DF` | Amber tint background |

### Status colors (for FACT / LIKELY_CAUSE / HYPOTHESIS / UNKNOWN)
| Token | Hex | Meaning |
|---|---|---|
| `--status-fact` | `#2FBF71` | FACT — directly observed |
| `--status-likely` | `#1FD1B8` | LIKELY_CAUSE — strongly supported (matches the primary accent, since this is the tool's core value) |
| `--status-hypothesis` | `#F0A83C` | HYPOTHESIS — plausible, unverified (dawn amber) |
| `--status-unknown` | `#6B7280` | UNKNOWN — insufficient evidence, deliberately desaturated |

**Rule:** teal and amber never appear as equals on the same element. Teal = confidence/signal, amber = caution/uncertainty. Status colors stay inside the evidence/demo module only — everywhere else the page speaks in ink-indigo, off-white, and a single teal accent.

## 3. Tailwind CSS Setup (Astro)

Static-output Astro project (`output: 'static'`, deployed to GitHub Pages). Add Tailwind via the official integration — no separate CSS file needed beyond font imports.

```bash
npx astro add tailwind
```

```js
// tailwind.config.mjs
/** @type {import('tailwindcss').Config} */
export default {
  content: ['./src/**/*.{astro,html,js,jsx,md,mdx,svelte,ts,tsx,vue}'],
  theme: {
    extend: {
      colors: {
        ink: {
          DEFAULT: '#0A0E17', // --bg-primary
          surface: '#111726', // --bg-surface-dark
          border: '#1E2536',  // --border-dark
        },
        paper: {
          DEFAULT: '#FCFCFB', // --bg-secondary
          surface: '#F1F1EE', // --bg-surface
          border: '#E3E2DD',  // --border
        },
        signal: {
          DEFAULT: '#1FD1B8', // --accent
          hover: '#17B39D',   // --accent-hover
          subtle: '#DEFBF5',  // --accent-subtle
        },
        dawn: {
          DEFAULT: '#F0A83C', // --amber
          subtle: '#FDF1DF',  // --amber-subtle
        },
        status: {
          fact: '#2FBF71',
          likely: '#1FD1B8',
          hypothesis: '#F0A83C',
          unknown: '#6B7280',
        },
        ink_text: {
          DEFAULT: '#0A0E17',       // --text-primary
          inverse: '#F4F5F3',       // --text-primary-inverse
          secondary: '#54595F',     // --text-secondary
          'secondary-inverse': '#9AA3B5', // --text-secondary-inverse
          muted: '#8B8F94',         // --text-muted
        },
      },
      fontFamily: {
        display: ['Inter', 'sans-serif'],
        mono: ['"JetBrains Mono"', 'monospace'],
      },
      spacing: {
        18: '4.5rem', // 72px, fills a gap in the default scale used by the 120/96/64 rhythm
      },
      maxWidth: {
        content: '1200px',
      },
      borderRadius: {
        card: '12px',
        pill: '4px', // deliberately not rounded-full — keeps badges technical, not friendly
      },
    },
  },
  plugins: [],
}
```

**Usage pattern.** Reference tokens by name, never by raw hex, directly in `.astro` files — Astro's `<style>`/markup is just HTML, so the same classes apply with zero adaptation:

```astro
---
// src/components/ProblemSection.astro
---
<section class="bg-ink text-ink_text-inverse py-30 px-6 md:px-20">
  <span class="text-signal text-[13px] font-semibold uppercase tracking-[0.08em]">The Problem</span>
  <h2 class="text-ink_text-inverse font-display font-bold text-4xl md:text-6xl tracking-tight mt-4">
    Infrastructure teams drown in alerts.
  </h2>
</section>

<button class="bg-signal hover:bg-signal-hover text-ink font-semibold text-sm px-7 py-3.5 rounded-md transition-colors duration-150">
  View on GitHub
</button>

<button class="border border-ink-border text-ink_text-inverse hover:border-ink_text-inverse font-semibold text-sm px-7 py-3.5 rounded-md transition-colors duration-150">
  Quick Start
</button>

<span class="inline-flex items-center gap-1.5 rounded-pill border-l-2 border-status-hypothesis bg-paper-surface px-2.5 py-1 font-mono text-[11px] uppercase tracking-wide text-ink_text">
  Hypothesis
</span>
```

Since Tailwind's default `py-30`/`px-20` etc. already cover the 4/8/12/16/24/32/48/64/96 spacing scale via its default multiples of 4px, no custom spacing scale is needed beyond the `18` filler above — just use the standard scale consistently (`py-30` = 120px, `py-16` = 64px) rather than reaching for arbitrary `[120px]` values.

**No framework migration needed.** Astro's static output (`astro build` → GitHub Pages) ships plain HTML/CSS/JS. Tailwind compiles at build time same as with any other framework, and the site stays 100% static — nothing here requires SSR or a Node server.

## 4. Typography

**Font families**
- Display / headings: `Inter` or `Söhne` — tight tracking, weight 600–700
- Body: `Inter` — weight 400–500
- Code / technical labels / metrics: `JetBrains Mono` or `IBM Plex Mono`

**Scale (desktop / mobile)**
| Role | Size | Weight | Line-height | Letter-spacing |
|---|---|---|---|---|
| Hero H1 | 64px / 36px | 700 | 1.05 | -0.02em |
| Section H2 | 40px / 28px | 700 | 1.1 | -0.01em |
| Card H3 | 20px / 18px | 600 | 1.3 | 0 |
| Body large | 19px / 17px | 400 | 1.6 | 0 |
| Body | 16px / 15px | 400 | 1.6 | 0 |
| Caption / eyebrow | 13px | 600 | 1.4 | 0.08em, uppercase |
| Code / mono | 14px | 500 | 1.5 | 0 |

**Eyebrow pattern** (used above every section headline, e.g. "The Problem", "Architecture", "Demo"): small uppercase mono or semibold label in `--accent`, 13px, letter-spacing 0.08em.

## 5. Layout & Grid

- **Max content width:** 1200px, centered, with 24px side gutters on mobile / 80px on desktop.
- **Section vertical rhythm:** 120px padding top/bottom on desktop, 64px on mobile.
- **Grid:** 12-column, 24px gutter for desktop; single column stack under 768px.
- **Alternating background rule:** Hero (dark) → Problem/Solution (light) → Architecture (dark) → Demo (light) → Quick Start (light, surface cards) → Philosophy (dark) → Metrics (light) → Footer (dark). This high-contrast section pacing is the site's core structural signature.

## 6. Spacing Scale

`4 / 8 / 12 / 16 / 24 / 32 / 48 / 64 / 96 / 120` px — all margins, paddings, and gaps snap to this scale. No arbitrary values.

## 7. Components

### Buttons
- **Primary:** solid `--accent` fill, white text, 8px radius, 14px/28px padding, weight 600. Hover: `--accent-hover`, no scale/shadow tricks — instant, flat transition.
- **Secondary (ghost):** 1px `--border` (or `--border-dark`), transparent fill, text color inherits. Hover: border becomes `--text-primary` / `--text-primary-inverse`.
- Never use both filled buttons side by side — one primary + one ghost per CTA group, exactly like the "View on GitHub" + "Quick Start" pairing on the current site.

### Cards
- 1px hairline border, 12px radius, no drop shadow by default.
- On hover: border transitions to `--accent` at 40% opacity, background lifts by one surface step. No lift/scale transform.
- Padding: 32px desktop / 20px mobile.

### Code / terminal blocks
- Background `--bg-surface-dark` regardless of section, monospace font, 13–14px, 24px padding, 8px radius.
- Optional macOS-style traffic-light dots or a filename tab (`morning-digest.txt`, `pamawas-infra/docker-compose.local.yml`) to reinforce the "this is real tooling" feel.

### Architecture diagram
- Flat, line-based node diagram — no skeuomorphism, no gradients on nodes.
- Nodes: 1px border, 8px radius, mono label for the tech (Go, Python, PostgreSQL) in `--text-muted`, bold label for the component name.
- Connectors: 1.5px solid lines, `--accent` used only for the "active"/primary data path if one needs emphasis; otherwise neutral gray.

### Status badges (FACT / LIKELY_CAUSE / HYPOTHESIS / UNKNOWN)
- Pill shape, 4px radius (not fully rounded — keep it technical, not friendly), 11px uppercase mono label, colored left-border or dot indicator using the status color table above, rest of badge neutral background.

### Metrics module
- Big number in mono or display font, 48–56px, `--text-primary`, with the small label beneath in `--text-muted` uppercase caption style. Arrange in a 3–5 column grid on desktop collapsing to 2 columns on mobile — mirrors Cloudflare's stat-strip sections.

### Numbered lists (Before/After Pamawas, Design Principles)
- Large mono numeral (`01`, `02`...) in `--text-muted` or `--accent`, oversized (32–40px) and set apart from the text block with generous left padding — numerals function as design elements, not just list markers.

## 8. Motion (Motion for React)

Install: `npm install motion`

Astro components aren't React by default, so use Motion's framework-agnostic vanilla API (`animate` + `inView` from `"motion"`) inside a plain `<script>` tag — no React, no islands, no hydration cost. Only two motion patterns are allowed anywhere on the site, this is a deliberate constraint, not a starting point to expand from.

**1. Fade + 8px slide-up on scroll-into-view**, staggered per child. Used for every section entrance (headline, then supporting copy, then cards).

```astro
---
// src/components/Reveal.astro
const { class: className = "" } = Astro.props;
---
<div class={`reveal-group ${className}`}>
  <slot />
</div>

<script>
  import { animate, inView, stagger } from "motion";

  document.querySelectorAll(".reveal-group").forEach((group) => {
    const items = group.querySelectorAll(":scope > .reveal-item");
    inView(
      group,
      () => {
        animate(
          items,
          { opacity: [0, 1], y: [8, 0] },
          { duration: 0.2, easing: "ease-out", delay: stagger(0.06) } // 60ms stagger
        );
      },
      { margin: "-80px" }
    );
  });
</script>

<style>
  .reveal-item { opacity: 0; }
</style>
```

```astro
---
// Usage inside a section, e.g. Philosophy
import Reveal from "../components/Reveal.astro";
const principles = [/* ... */];
---
<Reveal class="grid grid-cols-1 md:grid-cols-2 gap-8">
  {principles.map((p) => (
    <div class="reveal-item border border-ink-border rounded-card p-8">
      <span class="font-mono text-4xl text-signal">{p.number}</span>
      <h3 class="font-display font-semibold text-xl text-ink_text-inverse mt-4">{p.title}</h3>
      <p class="text-ink_text-secondary-inverse mt-2">{p.body}</p>
    </div>
  ))}
</Reveal>
```

**2. 150ms color/border hover transitions.** Use plain Tailwind `transition-colors duration-150` for simple color/border changes — this covers the vast majority of hover states and needs zero JS. Reach for Motion's `hover` helper only where a hover state needs to *orchestrate* more than one property in sync (e.g. card border + background lift together):

```js
// For the rare multi-property hover case
import { hover, animate } from "motion";

hover(".card-orchestrated", (element) => {
  animate(element, { borderColor: "#1FD1B8", backgroundColor: "#F1F1EE" }, { duration: 0.15 });
  return () => animate(element, { borderColor: "#E3E2DD", backgroundColor: "#FCFCFB" }, { duration: 0.15 });
});
```

**Explicitly forbidden**, even though Motion makes them easy: scale-up on hover, parallax via scroll-linked transforms on background layers, spring-bounce easing (visible overshoot), and looping/auto-playing animations. Motion should feel like a fast, confident interface reacting to the user — never an animated marketing page playing at the user.

**Reduced motion.** Guard the reveal script with a media query check so it respects the OS setting:

```js
const prefersReducedMotion = window.matchMedia("(prefers-reduced-motion: reduce)").matches;
if (!prefersReducedMotion) {
  // run the inView/animate logic above
} else {
  // just set items to their final opacity/position with no animation
}
```

**Why this works on GitHub Pages.** All of this compiles to static HTML/CSS plus a small client-side JS bundle at `astro build` time — identical deployment story to any other static Astro site. No server, no SSR adapter, no framework change required.

## 9. Iconography

- Line icons only, 1.5px stroke, no fills, 20–24px default size, inherit `currentColor`.
- Used sparingly: nav/component icons (📥🔗🤖📤⏰🗄️☸️ in the current source should become custom line icons, not emoji, in the redesign).

## 10. Section-by-Section Mapping (current content → new visual treatment)

| Section | Background | Key visual pattern |
|---|---|---|
| Hero | Dark | Eyebrow + huge H1 + subdued subhead + primary/ghost CTA pair, optional faint grid/dot background texture at 4% opacity |
| The Problem | Light | Two-column Before/After with numbered mono list items, red-tinted subtle left border on "Before", accent-tinted on "After" |
| Architecture | Dark | Flat diagram centered, component cards below in a responsive grid, mono tech-stack tags |
| Demo | Light | Terminal-style card with filename tab, status badges legend beside/below it |
| Quick Start | Light | Single dark code block (`--bg-surface-dark`) with copy-button affordance, numbered steps beside it |
| Philosophy | Dark | 4 large numbered principle blocks in a 2×2 or 4-column grid, numerals in `--accent` |
| Metrics | Light | Stat-strip, 5 columns desktop |
| Footer | Dark | 4-column link grid + mono tagline quote, hairline top border |

## 11. Accessibility & Contrast

- Body text on dark: `#9AA3B5` on `#0A0E17` → passes AA for normal text.
- Teal accent (`#1FD1B8`) on white: only large text (24px+), icons, or bordered/filled buttons with dark text on top — thin teal body text on `#FCFCFB` fails AA contrast, so pair it with `--text-primary` for the actual copy and reserve teal for the button fill or numerals.
- Amber (`#F0A83C`) on white: same rule — large text or fills only, never small body copy.
- Maintain 4.5:1 minimum for all body text, 3:1 for large headings.