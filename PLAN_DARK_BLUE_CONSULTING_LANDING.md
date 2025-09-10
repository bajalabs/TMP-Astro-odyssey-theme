# Plan: Dark Blue Consulting Landing Experience
Status: Draft (awaiting approval)
Branch: dark-blue-consulting
Date: 2025-09-09

## 1. Objective
Introduce a new landing page variant inspired by the referenced dark blue consulting design (Dribbble screenshot) using existing Astro component architecture, adding only minimal new primitives where necessary. Theme variant should be non-breaking and opt-in via route (`/consulting` or replace `/`). Updated per stakeholder direction: strictly FLAT professional dark blue interface (no gradients, no noisy textures) with a disciplined blue ramp + white text.

## 2. Source Reference Summary (Screenshot Analysis)
Observed structural sections (top → bottom):
1. Hero (solid dark blue background) with:
  - Flat color (no gradients, no texture)
  - Compact upper nav (logo left, minimal links, CTA button right)
  - Large headline (2–3 line bold display font) with optional single accent underline or colored keyword (no gradient text)
   - Supporting paragraph (max-width ~60ch)
   - Primary CTA (solid accent) + secondary text link
   - Cluster of client logos or credibility badges belowfold
2. Value Proposition Cards (3–4 horizontally on desktop, stack on mobile) with icon, short title, concise sentence, subtle border & hover lift.
3. Problem / Pain Statement band (slightly different darker shade) with a contrasting statistic (e.g., % or metric pills).
4. Services / Consulting Pillars section (grid of 6) with numbered labels or progress vertical accent line.
5. Process Timeline / Engagement Flow (stepper with 4–5 steps, icons or numbers, connecting line).
6. Case Study Highlight (image / mockup left, copy right) alternating layout for multiple entries.
7. Testimonial slider or static quote block (avatar, name, role, quote length ~180–240 chars).
8. Knowledge / Insights Teaser (3 latest blog posts styled uniformly with minimal metadata).
9. Call To Action band (either the same dark base or a lighter blue band) with succinct prompt and large button (flat background, optional 1px top & bottom separators).
10. Footer (condensed, social icons, legal links, theme switch preserved if compatible).

Visual motifs (FLAT palette):
- Palette Ramp (proposed hex approximations — adjust after contrast audit):
  - Dark blue: `#0C1321` (hero / primary background)
  - Rich blue: `#033356`
  - Mid blue: `#00579A`
  - Bright blue: `#06A9F5`
  - Light blue: `#BFE5FB`
  - White: `#FFFFFF`
  - Neutral text muted: `#7A8899`
  - Optional focus cyan (AA compliant): `#1CC3FF` (only for focus ring, not large text blocks)
- Typography: Bold display for H1 (~ clamp(2.75rem,5vw,3.75rem)); body stays existing stack.
- Surfaces: No gradients; separation via 1px borders using `rgba(255,255,255,0.06)` or lighter blue (`#033A63`).
- Cards: Flat fill (slightly lighter dark: mix dark blue + white 8%), subtle border, minimal shadow (or none; rely on border & spacing).
- Icons: Monotone or duotone using Mid + Bright blues (no gradient fills).
- Emphasis: Single-color keywords (Bright blue) or an underline bar (`display:inline-block; height:3px; background: var(--color-blue-bright);`).

## 3. Functional Requirements
| ID | Requirement | Type |
|----|-------------|------|
| FR1 | New landing route `/consulting` | Routing |
| FR2 | Theming extension: introduce flat ramp tokens (`--color-blue-dark`, `--color-blue-rich`, `--color-blue-mid`, `--color-blue-bright`, `--color-blue-light`, plus text + border tokens) | Design Tokens |
| FR3 | Hero component variant (flat background, optional accent underline / colored keyword, dual CTA) | Component |
| FR4 | Reusable Card primitive (icon/title/body) if existing card insufficient | Component |
| FR5 | Process timeline/stepper component (responsive horizontal → vertical) | Component |
| FR6 | Case study spotlight section (image + content, alt layout prop) | Section |
| FR7 | Testimonial block (single or list support) | Section |
| FR8 | Blog teaser section (pull latest 3 posts) | Integration |
| FR9 | CTA band component (headline + button) | Section |
| FR10 | Accessibility: color contrast AA for text/buttons | A11y |
| FR11 | No blocking JS; pure Astro/HTML + minimal CSS | Performance |
| FR12 | Dark-theme-business coexistence; do not regress existing palette | Non‑breaking |

## 4. Non-Functional Goals
- Maintain Lighthouse performance ≥ 95.
- Reuse existing layout shell (`Base.astro` / `Page.astro`) to avoid duplication.
- Keep additional CSS under 8KB gzipped.
- Support graceful degradation with no JS executed.

## 5. Data & Content Model Additions
No new MDX collection required initially. Case studies + testimonials can be hard-coded JSON arrays in `src/config/consulting.js` for MVP; optionally future MDX collections (phase 2).

## 6. Proposed File Additions
`src/config/consulting.js` – content arrays (services, steps, caseStudies, testimonials).
`src/components/consulting/HeroConsulting.astro`
`src/components/consulting/ValueCards.astro`
`src/components/consulting/ProcessTimeline.astro`
`src/components/consulting/CaseStudySpotlight.astro`
`src/components/consulting/Testimonials.astro`
`src/components/consulting/BlogTeaser.astro`
`src/components/consulting/CtaBand.astro`
`src/pages/consulting/index.astro` – page assembly.
`src/styles/consulting.css` – scoped additions (import via page or aggregated index).

## 7. Theme Token Extensions
Append in `theme.css` (or create `consulting.css` if isolation preferred):
```
:root {
  /* Flat Blue Ramp */
  --color-blue-dark: #0c1321;      /* primary background */
  --color-blue-rich: #033356;      /* secondary band / section split */
  --color-blue-mid:  #00579a;      /* interactive default */
  --color-blue-bright:#06a9f5;     /* highlights / primary CTA */
  --color-blue-light: #bfe5fb;     /* subtle backgrounds / badges */
  --color-text-on-dark: #ffffff;
  --color-text-muted: #7a8899;
  --color-border-low: rgba(255,255,255,0.06);
  --color-border-mid: rgba(255,255,255,0.12);
  --focus-ring: #1cc3ff;
}

/* Utility tokens */
:root {
  --elev-card-border: var(--color-border-mid);
  --elev-card-bg: rgba(255,255,255,0.04);
  --elev-card-bg-hover: rgba(255,255,255,0.06);
  --transition-base: 180ms ease;
}
```

## 8. Component Design Contracts (Condensed)
HeroConsulting
- Props: `headline (string|Astro slot)`, `subheading`, `primaryCta { label, href }`, `secondaryCta { label, href }`, `badges?: string[]|Slot`.
- Slots: `logos` (optional client logos row).

ValueCards
- Props: `items: Array<{ icon, title, body }>`.
- Layout: responsive grid (auto-fit minmax(220px,1fr)).

ProcessTimeline
- Props: `steps: Array<{ title, body, icon?, number? }>`.
- Responsive: horizontal with connecting line; vertical stacked on < 800px.

CaseStudySpotlight
- Props: `item: { title, summary, image, alt, link }`, `reverse?: boolean`.

Testimonials
- Props: `items: Array<{ quote, author, role, avatar? }>`.
- MVP: static list stacked; future slider optional.

BlogTeaser
- Logic: Astro.glob blog posts, sort by date desc, slice(0,3), reuse existing BlogPostPreview if adaptable.

CtaBand
- Props: `headline`, `cta { label, href }`, optional `subtext`.

## 9. Accessibility & UX Notes
- Maintain focus styles; ensure timeline is semantic (ordered list `<ol>` preferred).
- Provide `aria-label` for logos row if decorative.
- Use `prefers-reduced-motion` to disable any future animations.
- Color contrast: verify Bright blue on Dark blue for normal text; if below 4.5:1 restrict Bright blue to larger text or use Mid blue for body-sized interactive elements.

## 10. Risks & Mitigations
| Risk | Mitigation |
|------|-----------|
Inconsistent spacing vs existing theme | Adopt existing spacing CSS vars |
Insufficient contrast Bright blue on dark background | Use Mid blue for smaller text, run automated contrast audit |
Visual flatness (too austere) | Employ subtle 1px borders + spacing hierarchy instead of gradients |
Overuse of new CSS increasing bundle | Consolidate selectors, leverage existing utilities |
Future MDX migration complexity | Keep config-driven data shaped like potential frontmatter |

## 11. Phased Implementation
Phase 1 (MVP): Flat tokens, config, base components, static content, page assembly.
Phase 2 (Enhancements): Slider for testimonials, animation polish, MDX-driven case studies.
Phase 3 (SEO polish): Structured data (FAQ / Article if needed), OpenGraph tailored preview.

## 12. Acceptance Criteria (Phase 1)
- Visiting `/consulting` shows all described sections styled with navy background hero.
- No console errors, no client-side JS required for core rendering.
- Lighthouse performance ≥ 95 (desktop) & accessibility ≥ 90.
- Design tokens isolated; removal of page leaves no orphaned styles.

## 13. Out of Scope (Now)
- Full theming system refactor.
- Animation timeline / parallax.
- Client logo asset optimization pipeline.

## 14. Rollback Plan
Revert commit introducing `/consulting` and associated components; remove token additions; purge config file.

---
Awaiting approval before implementation.
