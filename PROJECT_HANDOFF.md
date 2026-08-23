# PROJECT_HANDOFF.md — kydo Flowboard Landing Page

> **Last updated:** 2026-08-23  
> **Repo:** https://github.com/origat2510/flowboard_kydo_website  
> **Branch:** `main`  
> **File to edit:** `index.html` (single-file — all HTML, CSS, and JS inline)

---

## 1. Current Project Status

### Sprint 1 — Completed ✅

#### Navbar
- Permanent frosted-glass effect: `backdrop-filter: blur(16px)` with `background: rgba(232,245,248,0.75)`
- Scrolled state (`.scrolled` class via JS): switches to `rgba(232,245,248,0.95)` + subtle box-shadow
- Logo height reduced to **44px** (meets WCAG touch target minimum)
- Nav links: `min-height: 44px`, `padding-inline: 0.5rem` for proper touch targets
- Scroll-spy via `IntersectionObserver` with `rootMargin: -${navHeight+8}px 0px -60% 0px` so active link only updates after section clears the navbar

#### Hero Section
- `h1 em` color corrected to `var(--white)` (was inheriting an accent color — contrast failure)
- Secondary CTA changed to `btn-outline` (white border, no fill) — correct for dark hero background
- Hero stats bar: clean inline stats with border-top divider, no floating glass-morphism cards
- `min-height: 100vh`, image via `.hero-bg` div (not `<img>`), gradient overlay `rgba(6,16,30,0.96)→transparent`

#### Inline Heroicons (Critical Bug Fix)
- **Root cause:** `<svg><use href="icons/sprite.svg#icon-NAME"></use></svg>` fails on `file://` protocol due to browser CORS restrictions on external SVG fragment identifiers.
- **Fix:** All icons replaced with fully self-contained inline SVGs. `sprite.svg` file still exists but is no longer referenced anywhere in `index.html`.
- Icons replaced (11 total): `bolt`, `check-circle` ×2, `photo`, `sparkles` ×3, `compass`, `wrench`, `wave`, `chat`, `lock`
- All inline SVGs use: `viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"` — Heroicons v2 outline spec

#### Mobile Hamburger Menu
- **Trigger:** `<button id="menu-toggle" class="menu-btn">` — hidden by default (`display: none`), shown at `<768px` via `display: flex`
- **Overlay:** `<div id="mobile-menu" class="mobile-menu">` — full-screen, `position: fixed; inset: 0; z-index: 200`, reveals via `.open { opacity: 1; visibility: visible; }`
- **Close button:** `<button id="menu-close" class="menu-close-btn">` positioned at `inset-inline-end: 1.25rem; top: 1.25rem`
- **Accessibility:** `aria-expanded` on toggle, `aria-hidden` on overlay, `role="dialog"`, focus moves to close button on open and back to toggle on close, `Escape` key closes, `body.style.overflow = 'hidden'` prevents background scroll
- **Nav links in overlay** link to: `#concept`, `#gallery`, `#inbox`, `#story` + primary CTA button

#### KPI Strip
- Placed as standalone `<section id="kpi-strip">` **between** hero and lifestyle sections (not floating over hero image)
- Background: `var(--dark)` with subtle `border-top` and `border-bottom`
- 3 items: "120 ק״ג כושר נשיאה" (bolt icon), "3 עיצובים לבחירה" (check-circle icon), "מתלה קיר כלול" (photo icon)
- **Desktop:** `display: flex; gap: 3rem; justify-content: center`
- **Mobile `<768px`:** `display: grid; grid-template-columns: repeat(3, 1fr)` — strict 3-column, never stacks
- **Small mobile `<480px`:** same 3-column grid, tighter gap
- Font sizes on mobile: `.kpi-num: 0.85rem`, `.kpi-label: 0.75rem` (WCAG minimum 12px)
- Icons shrink to 32×32px container on mobile with 16×16px SVG inside

#### Concept Section — Z-Pattern Editorial Layout
- Header (eyebrow + h2 + subtitle) centered in `.container`
- Two alternating rows in `.concept-z-wrap` (full-bleed, no container):
  - Row 1: `grid-template-columns: 55fr 45fr` → image (55%, right in RTL) | text (45%, left in RTL)
  - Row 2: `grid-template-columns: 45fr 55fr` → text (45%, right in RTL) | image (55%, left in RTL)
- `.concept-z-img { height: 480px; overflow: hidden; }` with `object-fit: cover`
- `.concept-z-body` has **no background** — text sits directly on section's `var(--bg-alt)` for seamless editorial look
- Image zoom on hover: `transform: scale(1.04)` wrapped in `@media (prefers-reduced-motion: no-preference)`

#### Story Section Mobile Order
- HTML order: text div first, image div second (correct for desktop RTL: text on right, image on left)
- Mobile fix: `.story-img { order: -1; }` at `<768px` so image appears above text on mobile

#### RTL & Accessibility
- All logical properties used throughout: `padding-inline`, `margin-inline`, `inset-inline`, `inset-inline-end`
- `prefers-reduced-motion` media query disables all transitions/animations globally
- `:focus-visible` ring: `2.5px solid var(--accent)` on all interactive elements
- `touch-action: manipulation` on all `.btn` and `.cta-chip` elements

---

## 2. Tech Stack & Architecture Notes

### Stack
- **Pure vanilla HTML + CSS custom properties + vanilla JS** — no framework, no build step, no npm
- **Font:** Heebo (Google Fonts), weights 300/400/500/600/700/800/900 — Hebrew-compatible
- **Language:** Hebrew RTL (`lang="he" dir="rtl"` on `<html>`)
- **Single file:** Everything lives in `index.html`. Open directly in browser — no server required.

### File Structure
```
balance-board/
├── index.html              ← entire site (HTML + CSS + JS)
├── icons/
│   └── sprite.svg          ← Heroicons v2 outline sprite (kept for reference, NOT used in HTML)
├── images/
│   ├── hero-bg.png
│   ├── action-mountain.jpg
│   ├── hanging-wall.jpg
│   ├── concept-training.jpg
│   ├── concept-wall.jpg
│   ├── pink-lotus.jpg
│   ├── wave.jpg
│   ├── white-lotus.jpg
│   ├── team.jpg
│   └── website_logo.png
├── design-system/
│   └── MASTER.md           ← design system reference (colors, typography, spacing, components)
├── CLAUDE.md               ← AI assistant instructions (read before any UI change)
└── PROJECT_HANDOFF.md      ← this file
```

### CSS Architecture

#### Custom Properties (`:root`)
```css
--bg: #E8F5F8       /* main light background */
--bg-alt: #D8EDF2   /* alternate sections */
--card: #FFFFFF
--dark: #030A15     /* hero, KPI strip, CTA, footer */
--text: #0C1C30
--muted: #4A6580
--accent: #0E47A1   /* brand blue — use on light backgrounds */
--accent-lt: #2D70E8 /* use ONLY on dark backgrounds */
--border: #B4D4E4
--r: 12px
--sh: 0 4px 24px rgba(14,71,161,0.08)
--sh-lg: 0 16px 56px rgba(14,71,161,0.15)
```

#### Responsive Breakpoints
| Breakpoint | Range | Key behaviors |
|-----------|-------|--------------|
| Desktop | ≥ 1100px | Default layout. Z-pattern 55/45, gallery 3-col, about 4-col |
| Tablet | 768px–1099px | Z-pattern 50/50, gallery 2-col, about 2-col |
| Mobile | < 768px | Hamburger menu, Z-pattern stacks, gallery 1-col, KPI 3-col grid |
| Small mobile | < 480px | Tighter padding, KPI 3-col tighter, hero stats stack |

#### Key CSS Classes
| Class | Purpose |
|-------|---------|
| `.container` | `max-width: 1100px; margin-inline: auto; padding-inline: 1.5rem` |
| `.btn`, `.btn-primary`, `.btn-outline`, `.btn-white`, `.btn-lg`, `.btn-sm` | Button variants |
| `.icon`, `.icon-sm`, `.icon-lg` | Inline SVG sizing (24px / 18px / 28px) |
| `.concept-z-row:first-of-type` | 55fr/45fr grid |
| `.concept-z-row:last-of-type` | 45fr/55fr grid |
| `.menu-btn` | Hamburger toggle (hidden desktop, flex mobile) |
| `.mobile-menu` | Full-screen overlay (opacity/visibility toggle) |
| `.mobile-menu.open` | Active state |
| `.kpi-grid` | KPI strip flex container → grid on mobile |
| `.cta-chip` | Design selector pill buttons |
| `.cta-chip.active` | Selected chip (accent background) |

#### Inline SVG Pattern
Every icon is self-contained. Template:
```html
<svg class="icon" aria-hidden="true"
     viewBox="0 0 24 24" fill="none" stroke="currentColor"
     stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round">
  <path d="...heroicons-v2-outline-path..."/>
</svg>
```
Use `class="icon icon-sm"` for 18px or `class="icon icon-lg"` for 28px.

#### JS Modules (all inline in `<script>` at bottom of `index.html`)
1. **Nav scroll** — adds `.scrolled` to `#navbar` after 40px
2. **Smooth scroll** — intercepts all `a[href^="#"]` clicks
3. **CTA chip selection** — updates `.active` class and dynamically rewrites WhatsApp URL with selected design name
4. **Scroll-spy** — `IntersectionObserver` with rootMargin offset, updates `.active` on `.nav-links a`
5. **Mobile menu** — `openMobileMenu()` / `closeMobileMenu()` with focus management, Escape key, body scroll lock

---

## 3. Next Steps — Sprint 2 Roadmap

### High Priority

#### S2-1 — WhatsApp Number & CTA Wiring
- Replace `972XXXXXXXXX` in the WhatsApp `href` (two places: `#whatsapp-btn` and the JS `waBase` constant) with the real phone number
- Test that the chip selection correctly updates the URL message for all 3 designs

#### S2-2 — Payment / Checkout Integration
- Decision needed: **Stripe Payment Links** vs **Shopify Buy Button** vs **custom checkout**
- If Stripe: create a Payment Link per design, replace the WhatsApp button with a Stripe link (or keep WhatsApp as fallback)
- If Shopify: embed a Buy Button widget in the CTA section
- Remove the `<div class="payment-notice">` placeholder once real payment is live

#### S2-3 — Image Optimization
- Convert all JPG/PNG photos to **WebP** (target: 60–80% size reduction)
  - Priority order: `hero-bg.png` (LCP), `action-mountain.jpg`, `concept-training.jpg`, `concept-wall.jpg`
- Add `width` and `height` attributes to all `<img>` tags (prevents CLS)
- Add `fetchpriority="high"` to the hero background element
- All below-fold images already have `loading="lazy"` ✅

#### S2-4 — Copy & Pricing Finalization
- Confirm final price (currently hardcoded `₪490` in all 3 gallery cards)
- Finalize shipping copy ("משלוח בכל הארץ" — add estimated days if known)
- Decide whether to add a "shipping cost" line to the gallery card or CTA section

### Medium Priority

#### S2-5 — Social Proof Section
- Add a reviews/testimonials section between `#gallery` and `#inbox`
- Recommended pattern: 3-column card grid with star rating, quote, reviewer name
- Star icon: `icon-star` is already in `sprite.svg` (inline the path when adding)
- High conversion impact — Indo Board benchmark shows "1,000+ 5 Star Reviews" above the fold

#### S2-6 — Trust Badges Row
- Add a horizontal strip of trust signals (e.g., "משלוח חינם", "30 יום החזרה", "תשלום מאובטח", "ייצור ישראלי")
- Place between KPI strip and lifestyle section, or between gallery and inbox
- Use existing icon set: `icon-truck`, `icon-shield-check`, `icon-lock`, `icon-heart`

#### S2-7 — Navbar "הסיפור שלנו" Link
- The mobile menu includes `#story` but the desktop nav does not
- Decide whether to add it to desktop nav (currently 3 links: concept, gallery, inbox)

#### S2-8 — Accessibility TODOs (from design-system/MASTER.md)
- Add `aria-label` to icon-only elements (the hamburger close button already has it ✅, verify others)
- Audit tab order through the full page at 375px

### Low Priority / Future

#### S2-9 — Analytics
- Add Google Analytics 4 or Plausible snippet in `<head>`
- Track: CTA chip clicks (design selection), WhatsApp button clicks, scroll depth

#### S2-10 — OG / SEO Meta Tags
- Add `<meta property="og:title">`, `og:description`, `og:image` for social sharing
- Add `<meta name="description">` for search engines
- Set canonical URL once domain is confirmed

#### S2-11 — Domain & Hosting
- Options: GitHub Pages (free, just enable in repo settings), Netlify (drag-and-drop deploy), Cloudflare Pages
- For GitHub Pages: Settings → Pages → Branch: main → Folder: / (root) → Save

---

## Quick Resume Checklist for Next Session

Before starting any new work, run through:
- [ ] Read `CLAUDE.md` — project rules and auto-activation triggers
- [ ] Read `design-system/MASTER.md` — color tokens, spacing, component specs
- [ ] Open `index.html` in browser at 375px (mobile) and 1440px (desktop) to assess current state
- [ ] Check this file's "Next Steps" section for priority order
- [ ] Confirm which sprint tasks have been completed since this handoff was written

---

*Generated at end of session 2026-08-23. Next session should pick up from Sprint 2 High Priority tasks above.*
