# kydo Flowboard — Design System MASTER
> Source of Truth for all UI decisions. Generated via ui-ux-pro-max skill.
> Stack: Vanilla HTML / CSS custom properties / vanilla JS · Hebrew RTL

---

## Product Profile

| Attribute | Value |
|-----------|-------|
| Product Type | Lifestyle E-commerce · Physical product landing page |
| Pattern | Feature-Rich Showcase + Social Proof |
| Style | Minimal & Direct — high whitespace, clean typography, visual-centric |
| Performance Target | WCAG AA · Excellent load performance · No heavy animations |
| Audience | Hebrew-speaking adults, home/fitness lifestyle shoppers |

---

## Color Tokens

```css
:root {
  /* Backgrounds */
  --bg:         #E8F5F8;   /* main — light sky teal */
  --bg-alt:     #D8EDF2;   /* alternate sections */
  --card:       #FFFFFF;
  --card-2:     #F0F8FC;

  /* Dark sections (hero, CTA, footer) */
  --dark:       #030A15;
  --dark-2:     #050E1C;

  /* Text */
  --text:       #0C1C30;   /* primary — contrast 10:1 on --bg ✓ */
  --muted:      #4A6580;   /* secondary — contrast 4.6:1 on --bg ✓ */
  --white:      #FFFFFF;

  /* Brand */
  --accent:     #0E47A1;   /* on light backgrounds */
  --accent-hov: #0A3480;
  --accent-lt:  #2D70E8;   /* on dark backgrounds only */

  /* UI Chrome */
  --border:     #B4D4E4;
  --r:          12px;       /* border-radius base */
  --sh:         0 4px 24px rgba(14,71,161,0.08);
  --sh-lg:      0 16px 56px rgba(14,71,161,0.15);
}
```

### Contrast Audit (WCAG AA = 4.5:1)
| Pair | Ratio | Pass |
|------|-------|------|
| `--text` on `--bg` | ~10:1 | ✅ AAA |
| `--muted` on `--bg` | ~4.6:1 | ✅ AA |
| `--white` on `--dark` | ~18:1 | ✅ AAA |
| `--white` on `--accent` | ~5.8:1 | ✅ AA |
| `--accent` on `--bg` | ~7.2:1 | ✅ AAA |

---

## Typography

```css
/* Google Fonts — already loaded in <head> */
font-family: 'Heebo', sans-serif;

/* Scale */
--text-xs:   0.72rem;   /* 11.5px — eyebrow labels */
--text-sm:   0.83rem;   /* 13.3px — taglines, small labels */
--text-base: 0.91rem;   /* 14.6px — body copy in cards */
--text-md:   1rem;      /* 16px   — body default */
--text-lg:   1.05rem;   /* 16.8px — lead text */
--text-xl:   1.22rem;   /* 19.5px — card titles */
--text-2xl:  1.45rem;   /* 23.2px — prices, section sub-heads */
--text-3xl:  1.9rem;    /* 30.4px — lifestyle labels */
--text-4xl:  clamp(1.9rem, 4vw, 3rem);   /* section titles */
--text-hero: clamp(2.5rem, 6vw, 5rem);   /* hero h1 */

/* Line Heights */
--lh-tight:  1.08;   /* hero headlines */
--lh-snug:   1.14;   /* section titles */
--lh-normal: 1.6;    /* body */
--lh-loose:  1.82;   /* story / long text */

/* Weights: 300 / 400 / 500 / 600 / 700 / 800 / 900 (Heebo) */
```

---

## Spacing System (4/8px rhythm)

```css
--sp-1:  0.25rem;   /*  4px */
--sp-2:  0.5rem;    /*  8px */
--sp-3:  0.75rem;   /* 12px */
--sp-4:  1rem;      /* 16px */
--sp-5:  1.25rem;   /* 20px */
--sp-6:  1.5rem;    /* 24px */
--sp-8:  2rem;      /* 32px */
--sp-10: 2.5rem;    /* 40px */
--sp-12: 3rem;      /* 48px */
--sp-14: 3.5rem;    /* 56px */
--sp-16: 4rem;      /* 64px */
--sp-20: 5rem;      /* 80px */
--sp-22: 5.5rem;    /* 88px — default section padding */
```

---

## Icon System

**Library:** Heroicons v2 Outline (24×24 viewBox, stroke-width: 1.5)
**Sprite file:** `icons/sprite.svg`

### Usage Pattern
```html
<svg class="icon" aria-hidden="true">
  <use href="icons/sprite.svg#icon-NAME"></use>
</svg>
```

### CSS Class
```css
.icon {
  width: 24px;
  height: 24px;
  stroke: currentColor;
  flex-shrink: 0;
}
.icon-sm { width: 18px; height: 18px; }
.icon-lg { width: 28px; height: 28px; }
```

### Available Icons
| ID | Usage |
|----|-------|
| `icon-check` | List checkmarks |
| `icon-check-circle` | Success / confirm |
| `icon-shield-check` | Safety / trust |
| `icon-photo` | Wall art / image |
| `icon-bolt` | Strength / energy |
| `icon-compass` | Any time, anywhere |
| `icon-arrow-right` | CTA direction |
| `icon-arrow-left` | Back / RTL |
| `icon-chevron-down` | Accordion / dropdown |
| `icon-chat` | WhatsApp / message |
| `icon-star` | Rating / review |
| `icon-cube` | Package / in the box |
| `icon-home` | Home / living room |
| `icon-clock` | Time / delivery |
| `icon-map-pin` | Location / delivery |
| `icon-truck` | Delivery / shipping |
| `icon-wrench` | Installation |
| `icon-heart` | Wishlist / love |
| `icon-info` | Info / tooltip |
| `icon-x` | Close / cancel |
| `icon-menu` | Mobile hamburger |
| `icon-sun` | Outdoor / lifestyle |
| `icon-wave` | Surf / kydo brand |
| `icon-lock` | Secure payment |
| `icon-sparkles` | Premium / art |
| `icon-tag` | Price / discount |

---

## Page Structure (Validated vs skill recommendations)

Recommended pattern: **Feature-Rich Showcase + Social Proof**

| # | Section | ID | Notes |
|---|---------|-----|-------|
| 1 | Hero (full-bleed image + text) | `#hero` | Single primary CTA |
| 2 | Lifestyle Split (2-panel) | `#lifestyle` | No text overlay clutter |
| 3 | Concept 2-col (image + checklist) | `#concept` | Problem → Solution |
| 4 | About / Features grid | `#about` | 4 benefits with SVG icons |
| 5 | Gallery (3 designs) | `#gallery` | Product showcase |
| 6 | In the Box + Specs | `#inbox` | Trust & completeness |
| 7 | Story | `#story` | Founder credibility |
| 8 | CTA | `#cta` | Design selector + WhatsApp |
| 9 | Footer | `footer` | Minimal |

**Missing (consider adding):**
- Social proof / reviews section (high conversion impact)
- Trust badges row (payment security, free returns, etc.)

---

## Component Specs

### Buttons
```css
/* Base */
.btn { min-height: 44px; min-width: 44px; cursor: pointer; touch-action: manipulation; }

/* Primary */
.btn-primary { background: var(--accent); color: var(--white); }
/* Hover: background → var(--accent-hov), translateY(-2px), box-shadow */
/* Transition: all 0.22s ease */

/* Outline (on dark bg) */
.btn-outline { border: 2px solid rgba(255,255,255,0.35); color: var(--white); }

/* White (on dark bg) */
.btn-white { background: var(--white); color: var(--dark); }
```

### Cards
```css
.card {
  background: var(--card);
  border-radius: var(--r);
  border: 1px solid var(--border);
  box-shadow: var(--sh);
}
/* Hover: translateY(-7px), box-shadow → var(--sh-lg), border-color hint */
/* Transition: transform 0.3s ease, box-shadow 0.3s ease */
```

### Icons in Feature Cards
```css
.feat-icon {
  width: 48px; height: 48px;
  background: rgba(14,71,161,0.08);
  border-radius: 12px;
  display: flex; align-items: center; justify-content: center;
  color: var(--accent);
}
```

---

## Animation Rules

| Type | Duration | Easing |
|------|----------|--------|
| Button hover | 220ms | ease |
| Card hover | 300ms | ease |
| Image zoom | 400–700ms | ease |
| Lifestyle panel zoom | 700ms | ease |
| Nav background | 300ms | ease |
| Color transitions | 200ms | ease |

**Always include:**
```css
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    transition-duration: 0.01ms !important;
  }
}
```

---

## Accessibility Checklist

- [x] `dir="rtl"` on `<html>` 
- [x] `lang="he"` on `<html>`
- [x] Alt text on all images (Hebrew)
- [x] Heading hierarchy: h1 → h2 → h3 ✓
- [x] SVG icons replace emojis in About section
- [ ] **TODO:** Add `cursor: pointer` to all `.btn` elements
- [ ] **TODO:** Add focus styles (visible ring on keyboard nav)
- [ ] **TODO:** Add `loading="lazy"` to below-fold images
- [ ] **TODO:** Add `prefers-reduced-motion` media query
- [ ] **TODO:** Add `touch-action: manipulation` to buttons
- [ ] **TODO:** Add `aria-label` to icon-only interactive elements

---

## RTL Rules

- Use `padding-inline` / `margin-inline` / `inset-inline` (never `left`/`right` for logical props)
- Flex rows are naturally mirrored in RTL — verify visual order
- Absolute positioned text labels: use `right:` for text start side
- Arrows in buttons: `→` renders correctly in RTL context
- Logo and nav: `justify-content: space-between` works correctly in RTL

---

## Performance Targets

| Metric | Target |
|--------|--------|
| LCP | < 2.5s |
| CLS | < 0.1 |
| FID/INP | < 100ms |
| Page weight | < 1MB (excluding images) |

**Image optimization TODO:**
- Convert JPG hero/lifestyle images to WebP
- Add `width` + `height` to all `<img>` tags
- Add `loading="lazy"` to all below-fold images
- Add `fetchpriority="high"` to hero background

---

## Anti-Patterns (from skill — avoid these)

- ❌ Emojis as icons
- ❌ Hardcoded hex colors in component styles
- ❌ `left`/`right` CSS properties for layout (use logical properties)
- ❌ Animating `width`/`height`/`top`/`left` (use `transform` only)
- ❌ Hover-only interactions (must work on touch)
- ❌ Missing `cursor: pointer` on clickable elements
- ❌ Vibrant/playful color scheme (brand is minimal elegant)
- ❌ Continuous/infinite decorative animations
- ❌ Layout shift from images without dimensions
