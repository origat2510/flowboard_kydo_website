# Product

<!-- impeccable:product-schema 1 -->

## Platform

web

## Users

Everyone, not just surfers. Typical buyers are people who want to:
- strengthen their core muscles and improve posture and balance with a few minutes of practice at home;
- add a fitness tool to their routine (surfers, snowboarders and other athletes are one group among many);
- do rehab or physical recovery work;
- and own fitness equipment that looks good enough to hang on the wall instead of hiding it in a cupboard.

They browse on a phone in Hebrew, choose a design that suits their home, and order through WhatsApp.

## Product Purpose

KYDO sells **FlowBoard**, a wooden balance board that comes with a cork roller and a wooden wall mount. People train on it, and when they're done the board goes on the wall as an original piece of art. Success means a visitor picks a design and starts a WhatsApp order.

## Positioning

Two products, one price: real training equipment that is also decor. Because of the wall mount and the art prints, the board doesn't need to be put away after training. It hangs on the living-room, bedroom or office wall as a picture. This dual use is the product's core claim.

## Operating Context

- **Ordering:** through WhatsApp (`wa.me` link with a pre-filled message, number in `index.html`). The site promises "we'll get back to you within an hour · delivery across Israel".
- **Use:** at home: put the roller under the board, train, then hang it on the wall mount.
- **In the box:** a FlowBoard (plywood with a high-definition UV print), a natural cork roller, a wooden wall mount, and an installation kit (2 wall plugs + 2 screws).

## Capabilities and Constraints

- **Price: ₪329 for every model.** A flat price with no sale framing: no crossed-out price and no "now" or "regular price" wording.- **Lineup (3 designs):** לוטוס לבן (clean, bright, minimal), הגל הגדול (a powerful sea print inspired by Japanese art), לוטוס ורוד (warm tones).
- **Verified spec:** 120 kg weight capacity.
- **Language and layout:** fully Hebrew, RTL (`<html lang="he" dir="rtl">` on every page). The product name FlowBoard is in Latin letters inside the Hebrew text (`<bdi>`).
- **Stack:** static vanilla HTML/CSS/JS, single file `index.html`, no framework (see CLAUDE.md).
- **Currency:** always the `₪` symbol.

## Brand Commitments

- Brand name: **KYDO**. Product name: **FlowBoard**. This is the spelling in all visible text (the contact email `Buyflowboard@gmail.com` stays as it is).
- Logo: `images/website_logo.png`.
- Voice: plain, warm Hebrew speaking directly to the reader in the plural ("תבחרו", "תולים על הקיר").

## Evidence on Hand

- **Real customer reviews:** exist, but are not yet in the repo. The `#reviews` section in `index.html` is ready for them and stays hidden while it's empty. Use only the original text the user supplies. Never write, edit or invent reviews, names or ratings.
- **Spec:** 120 kg weight capacity (verified).
- **Video:** `videos/brand-video.mp4` (brand video), `videos/action-demo.mp4` (training demo).
- **Photos:** `images/`: the three designs (`white-lotus`, `wave`, `pink-lotus`), the board hanging on a wall (`hanging-wall`, `wall-new`), training (`training-new`, `action-mountain`), team (`team`), hero (`hero-bg`).
- **Don't make up:** press, certifications, sales figures, medical claims about rehab, or a discount.

## Product Principles

1. **Training and art equally.** Every surface presents both uses. Neither is a side feature.
2. **For everyone.** Core, posture, fitness, rehab and home decor. Never frame the product as surfers-only.
3. **One honest price.** ₪329 for every model, no fake discounts or artificial urgency.
4. **Real proof only.** Reviews and specs come from the user, never invented.
5. **Short path to WhatsApp.** From choosing a design to sending the message, with as little friction as possible.

## Accessibility & Inclusion

Israeli Standard 5568 / WCAG 2.1 AA is the legal minimum. The footer on every page must link to the accessibility statement, terms, privacy policy and cancellation policy. Any marketing consent checkbox must start unchecked. Full details are in CLAUDE.md, "Legal & Compliance (Israel)".
