# Pamawas Landing Page Design Guideline

Date: 2026-08-17
Scope: Marketing landing page UX/UI direction for a modern minimalist, premium-feel first impression.

## 1. Design Objective

Create a landing page that feels calm, confident, and technical at first glance while clearly answering:

1. What Pamawas is.
2. Who it is for.
3. Why it is trustworthy.
4. What to do next.

Success criteria:

- A visitor understands the product value in under 5 seconds.
- The visual hierarchy is obvious without reading every line.
- The page feels premium through restraint, spacing, and clarity, not decoration.

## 2. Research Basis

This guideline is based on established UX principles:

1. Visual hierarchy through contrast, scale, and grouping.
   - NNGroup: https://www.nngroup.com/articles/visual-hierarchy-ux-definition/
2. Aesthetic-usability effect (better visuals increase perceived usability/trust).
   - Laws of UX: https://lawsofux.com/aesthetic-usability-effect/
3. Von Restorff effect (one distinctive element is most memorable).
   - Laws of UX: https://lawsofux.com/von-restorff-effect/

## 3. Core Visual Strategy

Use one dominant message, one dominant action, and one dominant visual anchor.

1. Dominant message:
   - Outcome-first headline.
   - No jargon in the first line.
2. Dominant action:
   - One primary CTA only.
   - One secondary CTA maximum.
3. Dominant visual anchor:
   - The incident brief panel is the hero focal object.
   - Avoid competing hero visuals.

Rule: If everything is emphasized, nothing is emphasized.

## 4. Information Hierarchy

## 4.1 Above-the-fold order

1. Eyebrow: short category/context signal.
2. Headline: 4-8 words, strong outcome statement.
3. Subhead: one sentence explaining mechanism/value.
4. CTA row: primary + secondary.
5. Trust strip: one short line of proof (open source, read-only, evidence-backed).
6. Hero artifact: representative incident brief.

## 4.2 Section pattern (for all major sections)

Each section should contain:

1. Section index + eyebrow.
2. A single primary claim.
3. Brief support copy (1-3 sentences).
4. One structured artifact (grid, panel, table, timeline, or code block).

Each section should communicate one idea only.

## 5. Typography Guideline

1. Use one sans family + one mono family only.
2. Limit hierarchy to 3 core tiers per section:
   - Display
   - Heading
   - Body
3. Keep headline weights lighter than typical SaaS pages to signal confidence.
4. Keep body text comfortable and readable (line-height around 1.55-1.7).
5. Avoid all-caps for long phrases; reserve uppercase for metadata labels only.

## 6. Color and Contrast Guideline

1. Use one primary accent color for actions and emphasis.
2. Use neutral surfaces to carry most layout structure.
3. Reserve semantic colors strictly for meaning:
   - Green: healthy/safe
   - Amber: caution/uncertainty
   - Red: critical/high severity
4. Keep accent usage sparse so highlighted items remain memorable.
5. Do not rely on color alone for meaning; reinforce with labels, icons, or text.

## 7. Spacing and Layout Rhythm

Premium feel is primarily a spacing discipline.

1. Increase whitespace around primary claims.
2. Keep related content tightly grouped.
3. Keep unrelated groups clearly separated.
4. Use consistent vertical rhythm section-to-section.
5. Avoid dense multi-column clusters unless comparison is the goal.

Practical rhythm:

- Large gaps between sections.
- Medium gaps between subsection blocks.
- Small gaps for tightly related label/value content.

## 8. Motion Guideline

Motion should clarify hierarchy and state change, never distract.

1. Use one load-in choreography for hero only.
2. Use subtle scroll-reveal for section blocks.
3. Use modest hover lift/glow on interactive cards and buttons.
4. Keep durations consistent (fast for micro, moderate for entrances).
5. Respect reduced-motion preferences with near-static fallbacks.

## 9. Copy Guideline

1. Lead with outcomes, then mechanism.
2. Replace feature lists with evidence-backed results.
3. Keep sentence length short to medium.
4. Remove repeated claims across sections.
5. Clearly distinguish:
   - Fact
   - Likely cause
   - Hypothesis
   - Unknown

Tone attributes:

- Calm
- Technical
- Precise
- Honest about uncertainty

## 10. Premium Minimalist Anti-Patterns

Avoid:

1. Too many accent colors.
2. Multiple "primary" CTAs.
3. Over-animated components competing for attention.
4. Excess decorative gradients/shadows with no hierarchy purpose.
5. Long blocks of generic marketing text above the fold.
6. Heavy card borders everywhere that create visual noise.

## 11. Accessibility and Trust Baseline

1. Maintain strong text/background contrast.
2. Ensure keyboard navigability and visible focus states.
3. Keep interactive targets comfortably tappable on mobile.
4. Preserve semantic landmarks and heading order.
5. Pair confidence statements with provenance or source context.

## 12. Component-Level Application in This Project

## 12.1 Hero

Target outcomes:

1. Immediate understanding of value proposition.
2. One memorable visual object.
3. One obvious next step.

Apply to current hero:

- Keep incident brief as focal object.
- Tighten headline/subhead to a single clear promise.
- Keep CTA pair minimal and unambiguous.

## 12.2 Workflow section

Target outcomes:

1. Fast cognitive scan.
2. Clear progression from noise to brief.

Apply:

- Keep 3-step structure.
- Keep numbers visually strong.
- Keep body copy short and concrete.

## 12.3 Investigation and architecture sections

Target outcomes:

1. Convey technical depth without clutter.
2. Preserve readability in dense information areas.

Apply:

- Use clear panel grouping.
- Keep labels consistent.
- Avoid adding new visual motifs that compete with hero language.

## 12.4 Trust and quick start

Target outcomes:

1. Increase credibility.
2. Reduce perceived adoption friction.

Apply:

- Keep trust principles concise and verifiable.
- Keep quick start commands simple and copy-friendly.

## 13. QA Checklist Before Shipping

Run this checklist for each major iteration:

1. 5-second test:
   - Can a first-time visitor explain what Pamawas does?
2. Squint test:
   - Is one element clearly dominant above the fold?
3. CTA test:
   - Is exactly one primary action visually dominant?
4. Noise audit:
   - Remove any non-essential decoration.
5. Mobile scan:
   - Does first viewport still communicate value + action clearly?
6. Accessibility check:
   - Contrast, keyboard, reduced motion, semantic structure.

## 14. Implementation Priority (Recommended)

1. Refine hero message clarity and CTA hierarchy.
2. Tighten spacing rhythm between all section headers and bodies.
3. Reduce any repeated claims across workflow/trust/architecture.
4. Run contrast and mobile-first-view QA pass.
5. Validate with a quick user comprehension test.

---

This document is a living guideline. Update it as user feedback, analytics, and usability findings reveal what improves comprehension and trust fastest.
