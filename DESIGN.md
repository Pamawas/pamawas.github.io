# Pamawas — Design System
 
Reference doc for implementing/extending the Pamawas landing page and future pages. Direction: **Scandinavian / Nordic** — open, airy, honest. Structure comes from whitespace, color, and type weight, not borders or boxed cards.
 
## Design principles
 
1. **No boxy cards.** Never wrap content in a bordered rectangle with a background fill to create a "card." Separate content with whitespace, thin 1px hairline rules only where genuinely needed for scanning (e.g. between list rows), or a full-bleed section background wash.
2. **Structure is earned, not decorated.** Numbering (01/02/03) is only used where the content is a real sequence (the 5-stage workflow). Elsewhere, use color-coded dots/edges instead of numbered badges.
3. **One organic signature per page.** A soft topographic contour-line motif (SVG, low opacity) is the visual signature — evokes fjord/elevation maps, ties to the product's "evidence has terrain, not flat certainty" idea. Don't add more than one major decorative motif per page.
4. **Typed claims stay visually typed.** Anywhere the product surfaces a claim (fact / likely / hypothesis / unknown), it must carry its color coding — never render claims as plain undifferentiated text.
5. **Honest, plain copy.** Active voice, no filler, no marketing superlatives. Failure and "unknown" states are described plainly, not apologetically.
## Color tokens — light & dark
 
Both palettes stay in the same hue families (fjord green, falu rust, ochre, moss) — dark mode is not a different brand, it's the same one under polar-night light. Values shift for contrast, not hue.
 
| Token | Light | Dark | Use |
|---|---|---|---|
| `--paper` | `#F4F4F0` | `#14181B` | Page background |
| `--paper-warm` | `#EFEEE4` | `#1B2023` | Alternating section band background |
| `--ink` | `#1B1E1C` | `#EDEEE8` | Primary text; also the fill for the *opposite*-mode surfaces (code panel, filled buttons stay dark-on-light and light-on-dark respectively — see note below) |
| `--ink-soft` | `#5C655F` | `#A7AFA8` | Secondary/body text |
| `--ink-faint` | `#9A9F97` | `#6C746D` | Tertiary/meta text (timestamps, mono captions) |
| `--fjord` | `#2F5049` | `#6FA89C` | Primary accent — links, primary hover, headline accent word |
| `--fjord-tint` | `#E1E9E4` | `#20302B` | Pill backgrounds on fjord-tagged elements |
| `--falu` | `#9C4630` | `#D9805F` | Alert / "unknown" claim type, eyebrow dot |
| `--falu-tint` | `#F2E2DB` | `#332420` | Falu-tagged pill backgrounds |
| `--ochre` | `#A97A2E` | `#D9AC63` | "Likely" / "hypothesis" claim type |
| `--ochre-tint` | `#F0E5D2` | `#332A1B` | Ochre-tagged pill backgrounds |
| `--moss` | `#546E51` | `#8FB589` | "Fact" claim type, tag-row bullet dots |
| `--moss-tint` | `#E4EAE0` | `#212B1F` | Moss-tagged pill backgrounds |
 
**Why dark accents are lighter/brighter than light-mode accents:** the light-mode fjord/falu/ochre/moss values are tuned for AA contrast against `#F4F4F0`; the same hex values would fail contrast against `#14181B`, so the dark set is the same hue lifted in lightness until it clears AA again. Don't reuse light-mode accent hexes directly on dark backgrounds.
 
**Inverted surfaces (code panel, filled buttons):** these already sit outside the paper/ink pair — in light mode they're `--ink`-on-`--paper`; in dark mode they invert again to stay the "opposite" surface, i.e. still a dark panel, but pull from a slightly lifted near-black (`#0D1012`) rather than pure `--paper`, so it reads as a distinct surface, not a hole in the page. Give it its own token: `--panel: #0D1012` (dark mode only; light mode panel stays `--ink` `#1B1E1C`).
 
Never introduce a new accent color without a semantic reason. If a new claim type or status is added, derive both a light and dark value the same way (same hue, contrast-matched lightness) — no saturated/neon colors, no gradients other than the contour motif.
 
## Dark mode mechanics
 
- Default to the user's system preference (`prefers-color-scheme`), with a manual toggle that overrides it and persists (e.g. `localStorage`). This is the one piece of client-side JS the "no unnecessary interactivity" principle allows — it's functional, not decorative.
- Implement by toggling a `dark` class on `<html>`, with all tokens above defined twice: once under `:root`, once under `:root.dark` (or via Tailwind's `dark:` variant if using Tailwind — see `spec.md`).
- The toggle control itself follows the same design language: no boxed button — a simple icon (sun/moon) with the same hover treatment as nav links, no pill background.
- Test both modes against every rule in "Layout rules" and "Motion & accessibility" below — nothing about those rules changes between modes, only the token values do.
## Typography
 
| Role | Font | Weight | Notes |
|---|---|---|---|
| Display (h1/h2/h3) | Archivo | 700–800 | Tight letter-spacing (-0.01em), used for headlines and section titles only |
| Body | Manrope | 400–600 | Default text, 16px base, 1.6 line-height |
| Mono / data | IBM Plex Mono | 400–500 | Eyebrows, run IDs, evidence sources, code, pill labels — anything that reads as "system output" |
 
Load via Google Fonts CDN (`fonts.googleapis.com`). Eyebrows are always mono, uppercase, 12px, letter-spacing 0.14em, preceded by a small falu-colored dot.
 
## Layout rules
 
- Max content width: `1180px`, side padding `32px` (`20px` under 520px).
- Section vertical padding: `110px` desktop, tighten to ~`70px` on mobile.
- Alternate section backgrounds between `--paper` and `--paper-warm` to create rhythm without borders.
- Two-column section heads (`eyebrow + h2` on left, one descriptive sentence on right) — never center-align headlines.
- Claim rows use a `3px` colored left edge (not a full border) at padding-left 18px — this is the only "border" pattern permitted, and only for typed claims.
- Buttons: fully rounded (`border-radius: 999px`), never sharp-cornered.
- No drop shadows. No gradients except the topographic hero motif.
## Signature element: topographic contour
 
- Inline SVG, 4–6 nested irregular closed bezier paths, `fill: none`, `stroke` alternating between fjord/falu/ochre at 0.14–0.28 opacity, stroke-width ~1–1.4px.
- Positioned bleeding off the right/top edge of the hero only. Do not repeat it elsewhere on the page — one signature per page keeps it meaningful.
- Must degrade gracefully: `opacity` reduced and `inset` tightened at `max-width: 900px`.
- In dark mode, use the dark-mode accent hexes for the strokes and raise opacity slightly (add ~0.05 to each value) — the same low-opacity strokes read as nearly invisible against `#14181B` otherwise.
## Motion & accessibility
 
- Respect `prefers-reduced-motion`: disable smooth scroll and transitions.
- All interactive elements need visible `:focus-visible` outline (`2px solid var(--fjord)`, 3px offset).
- Hover states: color/background shift only, optional `translateY(-1px)` on primary buttons — nothing more elaborate.
- Maintain WCAG AA contrast for text on `--paper` / `--paper-warm` backgrounds in both modes (ink and ink-soft both pass in each; ink-faint is for non-essential meta text only in either mode).
## Content voice
 
- Sentence case, no title case in headings.
- Claim/status labels are always uppercase mono (`FACT`, `LIKELY`, `HYPOTHESIS`, `UNKNOWN`).
- Never fabricate demo data as if it were live — label illustrative content explicitly (e.g. "Illustrative data, not a production benchmark").
- Numbered workflow steps (01–05) reflect the actual pipeline order and must stay in sync with the real system if stages are added, removed, or reordered.