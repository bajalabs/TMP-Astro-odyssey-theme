# Task Breakdown: Dark Blue Consulting Landing
Status: Draft (pending approval)
Plan Ref: `PLAN_DARK_BLUE_CONSULTING_LANDING.md`

| ID | Task | Description | Effort | Depends | Output |
|----|------|-------------|--------|---------|--------|
| T1 | Create tokens | Add flat blue ramp CSS vars (no gradients) | S | - | Token diff |
| T2 | Config seed | Add `src/config/consulting.js` with arrays (valueCards, steps, caseStudies, testimonials) | S | T1 | Config file |
| T3 | Hero component | Implement `HeroConsulting.astro` (flat dark background, underline accent, dual CTAs) | M | T1 | Component |
| T4 | Value cards | Build `ValueCards.astro` grid | S | T2 | Component |
| T5 | Timeline | Build `ProcessTimeline.astro` (responsive) | M | T2 | Component |
| T6 | Case study spotlight | Build `CaseStudySpotlight.astro` | M | T2 | Component |
| T7 | Testimonials | Build `Testimonials.astro` (static) | S | T2 | Component |
| T8 | Blog teaser | Build `BlogTeaser.astro` reusing existing blog preview comp | S | Blog content present | Component |
| T9 | CTA band | Build `CtaBand.astro` | S | T1 | Component |
| T10 | Page assembly | Create `/consulting/index.astro` assembling sections | M | T3-T9 | Page file |
| T11 | Style sheet | Add `consulting.css` (if not inlined) & import | S | T3 | CSS file |
| T12 | Accessibility audit | Manual contrast + headings outline + keyboard nav | S | T10 | Report notes |
| T13 | Performance check | Lighthouse / size check; adjust if >8KB added CSS | S | T10 | Metrics |
| T14 | Docs addition | Add section in `docs/architecture.md` describing variant | S | T10 | Doc update |
| T15 | Commit & PR | Commit as `feat(consulting): add dark blue consulting landing variant` | XS | T10 | PR |
| T16 | Phase 2 backlog | Create FUTURE.md notes for sliders / MDX expansions | XS | T15 | FUTURE delta |

Effort Legend: XS (<5m) S (5–10m) M (10–25m) L (25–45m) XL (>45m)

## Content Seed Draft (for `consulting.js`)
```js
export const valueCards = [
  { icon: 'strategy', title: 'Strategic Clarity', body: 'Define actionable roadmaps aligned to measurable outcomes.' },
  { icon: 'delivery', title: 'Operational Acceleration', body: 'Streamline delivery with lean execution frameworks.' },
  { icon: 'enablement', title: 'Team Enablement', body: 'Upskill teams via embedded coaching & knowledge systems.' },
  { icon: 'innovation', title: 'Innovation Velocity', body: 'De-risk experimentation while scaling validated bets.' },
];

export const steps = [
  { title: 'Discovery', body: 'Context, alignment & baseline metrics.' },
  { title: 'Strategy', body: 'Define north star, value levers & roadmap.' },
  { title: 'Design', body: 'Blueprint processes, architectures & org enablement.' },
  { title: 'Execution', body: 'Iterative delivery with embedded coaching.' },
  { title: 'Scale', body: 'Institutionalize wins; adapt & optimize.' },
];

export const caseStudies = [
  { title: 'Platform Modernization', summary: 'Reduced cloud spend 28% while increasing deployment frequency 3×.', image: '/assets/images/placeholder-screenshot.png', alt: 'Platform modernization dashboard', link: '/blog/platform-modernization' },
  { title: 'Data Enablement Initiative', summary: 'Unified fragmented data sources enabling real-time insights.', image: '/assets/images/placeholder-screenshot.png', alt: 'Data initiative visualization', link: '/blog/data-enablement' },
];

export const testimonials = [
  { quote: 'They helped us unlock a transformation we had delayed for years—fast, pragmatic, outcome-focused.', author: 'Jamie L.', role: 'VP Engineering' },
  { quote: 'Clear frameworks and hands-on partnership. We achieved in 3 months what previously took 12.', author: 'Priya S.', role: 'Head of Product Ops' },
];

export const cta = { headline: 'Ready to accelerate strategic outcomes?', cta: { label: 'Engage Consulting', href: '/contact' } };
```

## QA Checklist (Phase 1)
- [ ] All sections render without horizontal scroll at 360px width.
- [ ] Headline clamps properly across breakpoints.
- [ ] Card grid collapses gracefully < 640px.
- [ ] Timeline switches to vertical stack < 800px.
- [ ] Images have descriptive alt text.
- [ ] No unused console logs or commented dead code.
- [ ] Contrast: Bright blue usage limited to roles passing AA (verify with tool).
- [ ] Link & button focus ring visible on dark background (focus color >= 3:1 against dark blue).

---
Awaiting approval.
