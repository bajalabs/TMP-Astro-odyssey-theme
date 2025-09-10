# UI / UX Reference: Dark Blue Consulting Landing
Status: Draft (visual brief, revised flat palette)

## 1. Screenshot Reference
Captured full reference image from source (Dribbble CDN). Store internally if needed; current path (local dev capture): `.playwright-mcp/page-2025-09-09T10-00-00-224Z.png` (not committed by default). Consider optimizing and checking license if ever bundled.

## 2. Visual System Summary
| Element | Spec (Approx) | Notes |
|---------|---------------|-------|
Hero BG | Solid Dark blue `#0C1321` | No gradients / textures |
Primary Action / Accent | Bright blue `#06A9F5` (buttons, key highlights) | Limit large text; verify contrast |
Secondary Interactive | Mid blue `#00579A` | Default button / link hover base |
Structural Bands | Rich blue `#033356` | Alternate section background bands |
Supportive Light Surface | Light blue `#BFE5FB` (sparingly) | Tags / subtle badges (ensure not over-bright) |
Text Primary | White `#FFFFFF` | Body & headings |
Text Muted | `#7A8899` | Secondary meta text |
Borders / Dividers | `rgba(255,255,255,0.06)` / mid at 0.12 | 1px lines for separation |
Card BG | `rgba(255,255,255,0.04)` | Flat card container |
Card Hover | Background +2% opacity, border from low → mid | Maintain no shadow or minimal shadow-off alternative |
Focus Ring | Cyan `#1CC3FF` 2px outline | Always visible on dark base |
Timeline Connector | 2px line using Mid blue | Vertical on narrow viewports |
Headline Accent | Underline bar in Bright blue (3–4px) | Avoid gradient text |
CTA Band | Reuse Dark or Rich blue with top & bottom 1px border | Keep consistent flat aesthetic |

## 3. Layout & Spacing
- Base container max-width: 1200px (existing `Container` component ok).
- Section vertical rhythm:  var(--section-margin) or custom: hero (top heavy ~140px), inner sections (~96px), CTA band (~120px).
- Grid gaps: 24px (desktop), 16px (mobile).

## 4. Interaction Guidelines
- Hover: color / border-opacity shifts (no shadows unless absolutely needed). If shadow used: `0 2px 4px rgba(0,0,0,0.3)` subtle only.
- Active: slight translateY(1px) for buttons.
- Focus: 2px solid `#1CC3FF` (token `--focus-ring`), maintain 2px offset via `outline-offset: 2px`.
- Reduced motion: no transform animations beyond 120ms fade/opacity.

## 5. Accessibility Notes
- Headings hierarchy: H1 hero, H2 per section.
- Decorative icons `aria-hidden="true"`.
- Underlines (or clear affordance) for textual links, especially Bright blue inline links.
- Contrast audit table to produce after implementation; fallback: use Mid blue for small (<18px) text links if Bright fails contrast.

## 6. Future Enhancements (Not in Phase 1)
- Animated gradient border cards.
- Scroll-linked progress indicator for timeline.
- Testimonial carousel (prefers-reduced-motion aware).
- Dynamic logos fetch via CMS.

## 7. Open Questions (to clarify prior to build if needed)
- Do we elevate consulting page to root later? (Routing impact)
- Should hero include embedded form (lead capture) variant? (Deferred)
- Are case study images placeholders or final assets? (Assume placeholder)

---
End of visual brief.
