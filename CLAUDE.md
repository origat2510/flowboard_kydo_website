# CLAUDE.md — kydo / Flowboard Landing Page

## Project Context

Vanilla HTML/CSS/JS landing page (no framework, no Tailwind, no React).  
Hebrew RTL (`dir="rtl"`, `direction: rtl`), font: Heebo (Google Fonts).  
File: `index.html`. Images: `images/`. Icons: `icons/sprite.svg`.  
Design system reference: `design-system/MASTER.md` — read this before any UI change.  
Stack: pure HTML + CSS custom properties + vanilla JS.

## Icon Usage
Icons are in `icons/sprite.svg` (Heroicons v2 outline, 24×24).  
Use: `<svg class="icon" aria-hidden="true"><use href="icons/sprite.svg#icon-NAME"></use></svg>`  
Available IDs: check, check-circle, shield-check, photo, bolt, compass, arrow-right, arrow-left, chevron-down, chat, star, cube, home, clock, map-pin, truck, wrench, heart, info, x, menu, sun, wave, lock, sparkles, tag

---

## UI/UX Pro Max — Auto-Activation

**Trigger this review automatically whenever the request involves:**
- Any layout or spacing change
- Adding, removing, or restyling a section or component
- Color, typography, or visual hierarchy changes
- Button, CTA, card, or form styling
- Navigation or scroll behavior
- Image sizing, cropping, or positioning
- Animations or transitions
- Mobile / responsive behavior
- Anything a product designer would need to approve before development

**Skip if:** the request is purely content text, file renaming, or server/config work.

**Decision rule:** If the task changes how something *looks*, *feels*, or *behaves* — run the UI/UX review below before touching code.

---

## Design Rules (Priority Order)

### 1. Accessibility — CRITICAL
- Text contrast ≥ 4.5:1 on light backgrounds; ≥ 3:1 for large headings
- Every interactive element must have a visible focus state
- Images must have meaningful `alt` text in Hebrew
- Heading hierarchy must be sequential (h1 → h2 → h3, no skipping)
- Color must never be the *only* indicator of meaning — always pair with text or icon
- Respect `prefers-reduced-motion`: disable or reduce CSS animations when requested

### 2. Touch & Click Targets — CRITICAL
- Minimum tap/click area: 44×44px for all buttons and links
- Minimum 8px gap between adjacent interactive elements
- Never rely on hover as the only interaction state — must work on touch

### 3. Performance — HIGH
- Use WebP or high-quality JPG for photos; PNG only for logos/transparency
- Images must have `width` and `height` attributes (or fixed CSS dimensions) to prevent layout shift
- Lazy-load images below the fold (`loading="lazy"`)
- No layout thrashing: avoid JS that reads and writes layout in the same frame

### 4. Style & Visual Consistency — HIGH
- **No emojis as structural icons** — use inline SVG (stroke-based, 24×24 viewBox)
- SVG icons must use `stroke="currentColor"` to inherit theme color
- Stroke width consistent: 2px throughout (never mix 1.5px and 2px)
- Icon sizes defined in CSS, not ad-hoc inline: `width: 24px; height: 24px`
- CSS custom properties (variables) for all colors — never hardcode hex in component rules
- Brand accent: `--accent: #0E47A1`; light-bg accent: `--accent` (not `--accent-lt`)
- `--accent-lt` is only for elements on dark backgrounds (hero overlay, CTA, footer)

### 5. Layout & Responsive — HIGH
- Mobile-first: test at 375px width before considering desktop
- No horizontal scroll at any viewport width
- `max-width: 1100px` container centered with `margin-inline: auto`
- Spacing rhythm: multiples of 4/8px — never arbitrary values like 13px or 27px
- Section vertical padding: `5.5rem 0` default; reduce for mobile
- RTL: use `padding-inline`, `margin-inline`, `inset-inline` — never `left`/`right` for logical properties

### 6. Typography & Color — MEDIUM
- Body text minimum: 14px (`0.875rem`); preferred: 16px+
- Line-height: 1.6 for body, 1.14–1.2 for headings
- Letter-spacing: negative (`-0.025em`) for large headings only
- On light backgrounds (`--bg`, `--bg-alt`, `--card`): text = `var(--text)` (#0C1C30), muted = `var(--muted)` (#4A6580)
- On dark backgrounds (`--dark`): text = `var(--white)`, muted = `rgba(255,255,255,0.75)`
- Never use gray-on-gray combinations

### 7. Animation — MEDIUM
- Micro-interactions: 150–300ms duration max
- Use `ease` or `cubic-bezier` — never `linear` for UI transitions
- Hover effects: `transform: translateY(-Xpx)` + `box-shadow` (never animate `width`/`height`)
- Image zoom on hover: `transform: scale(1.04–1.06)` with `overflow: hidden` on parent
- All animations must be wrapped in `@media (prefers-reduced-motion: no-preference)` if decorative

### 8. Navigation — HIGH
- Navbar: fixed, transparent over hero, switches to frosted glass on scroll
- On scroll (light theme): `background: rgba(232,245,248,0.95)` + dark logo/links
- Smooth scroll: `scroll-behavior: smooth` on `html`
- Active/hover nav links: clear color change, never layout shift
- CTA button in nav: always `btn-primary` style, never just a text link

### 9. RTL-Specific — CRITICAL for this project
- All flex/grid layouts must be verified in RTL direction
- Text alignment: `text-align: right` default; `text-align: center` for hero/headers
- Arrows in CTAs: use `→` (→) which correctly points left-to-right even in RTL contexts
- Absolute positioned labels: use `right` for start-of-text side in RTL

### 10. Images — HIGH
- `object-fit: cover` with explicit container height for cropped images
- `object-fit: contain` with padding for product photos on cards
- `object-position` must be set intentionally — never rely on default `center center` without checking
- Lifestyle photos: gradient overlay (`rgba(6,16,30,0.78)` → transparent) for text legibility on dark
- Hero: full-viewport background image with `background-size: cover; background-position: center`

---

## Pre-Delivery Checklist

Before delivering any UI change:

**Visual**
- [ ] No emojis used as icons — SVG only
- [ ] All colors use CSS variables, not hardcoded hex
- [ ] Consistent stroke width on SVG icons (2px)
- [ ] Contrast ratios pass on both light and dark sections

**Layout**
- [ ] Tested at 375px mobile width — no horizontal scroll
- [ ] Spacing follows 4/8px rhythm
- [ ] RTL layout verified (flex direction, text alignment, logical properties)

**Interaction**
- [ ] Hover states defined for all clickable elements
- [ ] Transition duration 150–300ms with `ease`
- [ ] No layout shift on hover/click

**Images**
- [ ] `object-position` explicitly set for all cropped images
- [ ] Alt text in Hebrew for all images
- [ ] No unconstrained images causing layout reflow

---

## Current CSS Variables Reference

```css
:root {
  --bg:         #E8F5F8;   /* main light background */
  --bg-alt:     #D8EDF2;   /* alternate section background */
  --card:       #FFFFFF;
  --card-2:     #F0F8FC;
  --dark:       #030A15;   /* hero, CTA, footer */
  --dark-2:     #050E1C;   /* footer */
  --text:       #0C1C30;
  --muted:      #4A6580;
  --accent:     #0E47A1;   /* brand blue */
  --accent-hov: #0A3480;
  --accent-lt:  #2D70E8;   /* accent on dark backgrounds only */
  --border:     #B4D4E4;
  --white:      #FFFFFF;
  --r:          12px;
  --sh:         0 4px 24px rgba(14,71,161,0.08);
  --sh-lg:      0 16px 56px rgba(14,71,161,0.15);
}
```

---

## Legal & Compliance (Israel)

This section defines the Israeli regulatory and accessibility baseline for every page on this site. It applies in addition to the Design Rules above — accessibility requirements here are the legal floor, not just UX polish.

### 1. Directionality & Language — CRITICAL
- Every HTML document's `<html>` tag must declare both: `<html lang="he" dir="rtl">`
- Never rely on CSS `direction: rtl` alone as a substitute for the `dir` attribute — screen readers, form controls, and browser UI chrome (e.g. `<select>`, date pickers) key off the HTML attribute, not just the computed style
- Any future additional page (not just `index.html`) must carry the same `lang="he" dir="rtl"` pair

### 2. Accessibility — ת"י 5568 / WCAG 2.1 AA — CRITICAL
Israel's Equal Rights for Persons with Disabilities regulations (תקנות נגישות השירות) adopt ת"י 5568, which is Israel's localization of WCAG 2.0/2.1 Level AA. Treat AA as the legal minimum, not an aspirational target.
- Every `<img>` has a meaningful `alt` attribute **written in Hebrew**, describing the image's content/purpose — never a transliterated filename, never left empty unless the image is purely decorative (in which case use `alt=""` deliberately, not an omission)
- Every icon-only interactive element (a button or link with no visible text label) has an `aria-label` in Hebrew describing its action (e.g. `aria-label="סגור תפריט"`, not `aria-label="Close"`)
- Heading hierarchy is sequential on every page: `h1` → `h2` → `h3`, never skipping a level (e.g. `h2` straight to `h4`) and never more than one `h1` per page
- Every interactive element has a visible `:focus-visible` state (already defined globally — see Design Rules §1) — never remove or suppress it with `outline: none` without supplying a replacement indicator
- This builds on, and does not replace, Design Rule §1 (contrast ratios, color-not-as-sole-indicator, `prefers-reduced-motion`) and §2 (44×44px touch targets)

### 3. E-commerce Legal Requirements — CRITICAL
Baseline obligations under Israeli consumer-protection and e-commerce law (חוק הגנת הצרכן, תקנות הגנת הצרכן (ביטול עסקה), and the anti-spam provision of חוק התקשורת — "חוק הספאם"):
- **Persistent footer, every page:** must include links to an accessibility statement (הצהרת נגישות), the site's terms (תקנון), a privacy policy (מדיניות פרטיות), and the right-of-cancellation / return policy (ביטול עסקה). These are not optional decoration — their absence is a compliance gap, not a design choice.
- **Marketing opt-in checkboxes:** any checkbox for newsletter/SMS/marketing consent must default to **unchecked**. Never pre-check a marketing opt-in on behalf of the user — under חוק הספאם, consent must be an affirmative, un-coerced action.
- **Currency display:** all prices are shown in New Israeli Shekels using the `₪` symbol (not `ILS`, not `NIS`, not a bare number) — consistent with how pricing already appears across `index.html` (e.g. `₪390`).

**Current gap (as of this branch):** `index.html`'s `<footer>` does not yet contain accessibility/terms/privacy/cancellation links, and the site has no marketing opt-in checkbox at all. Implementing those pages/links is tracked as follow-up work, not covered by this document alone — this section defines the standard that work must meet when it lands.
