# Adventure Mail Club — Static Site

A complete 37-page static website for Adventure Mail Club, a children's personalised postal subscription service.

---

## Quick start

This is a flat-file static site. No build step required.

```bash
# Option 1 — Python (built in to macOS/Linux)
cd adventure-mail-club
python3 -m http.server 8080
# Open http://localhost:8080

# Option 2 — Node (if you have it)
npx serve .
# or
npx http-server . -p 8080

# Option 3 — VS Code
# Install the "Live Server" extension, right-click index.html → Open with Live Server
```

> **Important:** Open via a local server, not by double-clicking files. The CSS and fonts load via relative paths, so a server is needed for everything to work correctly.

---

## Folder structure

```
adventure-mail-club/
│
├── shared.css              ← All tokens, components, animations (34KB)
│
├── index.html              ← Homepage (cinematic hero, all sections)
│
├── ── Public pages ──
├── how-it-works.html
├── story.html
├── characters.html         ← Character profiles with base64 images
├── inside-the-pack.html
├── personalisation.html
├── pricing.html
├── reviews.html
├── faq.html
├── gift.html
├── schools.html
├── about.html
├── contact.html
├── blog.html
├── blog-article.html       ← Article template
│
├── ── Auth ──
├── login.html
├── signup.html
├── forgot-password.html
├── reset-password.html
├── account.html            ← Tabbed account dashboard
│
├── ── Checkout (5 steps) ──
├── checkout.html           ← Step 1: Plan selection
├── checkout-details.html   ← Step 2: Child details
├── checkout-pers.html      ← Step 3: Personalisation
├── checkout-payment.html   ← Step 4: Payment
├── checkout-review.html    ← Step 5: Order review
├── checkout-success.html   ← Confirmation
├── onboarding.html         ← Post-signup welcome
│
├── ── Portal ──
├── portal.html             ← Full portal (8 panels: Mission, Map, Inventory, Log, Characters, Achievements, Messages, Settings)
│
├── ── Growth ──
├── referral.html
├── affiliate.html
├── waitlist.html
├── lp-christmas.html       ← Seasonal paid landing page (template)
│
└── ── Legal & support ──
    ├── privacy.html
    ├── terms.html
    ├── cookies.html
    ├── returns.html
    └── help.html
```

---

## Design system (`shared.css`)

All pages import `shared.css` which contains:

**Tokens**
- `--bg`, `--bg2`, `--bg3`, `--bg4` — dark background scale
- `--pur`, `--pink`, `--gold`, `--teal`, `--green` — brand colours
- `--t1`, `--t2`, `--t3`, `--t4` — text opacity scale
- `--border`, `--border-hi` — border colours
- `--r`, `--r-lg`, `--r-xl` — border radius scale

**Components**
- `.btn`, `.btn-pur`, `.btn-gold`, `.btn-ghost`, `.btn-sm`, `.btn-lg`
- `.card`, `.card-sm`
- `.site-nav` (scrolled state: `.scrolled`)
- `.portal-nav`, `.portal-tab`, `.portal-badge`
- `.portal-stage`, `.portal-panel`, `.portal-panel.active`
- `.page-hero`, `.page-hero-inner`
- `.pill`, `.pill-pur`, `.pill-gold`, `.pill-green`
- `.faq-item`, `.faq-q`, `.faq-a`
- `.auth-screen`, `.auth-card`
- `.checkout-screen`, `.checkout-grid`
- `.tc` (testimonial), `.cc` (character card)
- `.inv-item`, `.inv-ico`, `.lock-overlay`
- `.tl-item`, `.tl-dot`
- `.ach` (achievement badge)
- `.choice`, `.choice-group`
- `.site-footer`, `.footer-grid`

**Animations**
- `floatY`, `floatSlow` — ambient floating
- `glowPulse` — portal glow
- `fadeUp` — scroll entry
- `marqueeAnim` — scrolling ticker
- `shootStar` — hero shooting star effect
- `twinkle` — star field

**Utility classes**
- `.rv` — scroll reveal (IntersectionObserver adds `.in`)
- `.gt-pur`, `.gt-gold`, `.gt-teal`, `.gt-white` — gradient text
- `.eyebrow` — uppercase section label
- `.s-title`, `.s-sub` — section heading + subtext
- `.wrap`, `.wrap-md`, `.wrap-sm` — max-width containers
- `.section`, `.section-sm` — section padding
- `.mesh-bg`, `.star-field`, `.shoot` — hero background layers
- `.form-group`, `.form-label`, `.form-input`, `.form-select`, `.form-textarea`

---

## Adding a new page

1. Copy `how-it-works.html` as a starting point
2. It already has: `<link rel="stylesheet" href="shared.css">`, nav, footer, shared JS
3. Use `subpage(title, active, h1, subtitle, body)` structure or `auth_page()` for auth screens
4. Add your page to the nav in `shared.css` and regenerate, or edit the nav HTML directly

---

## Moving to a framework

This site is designed to be straightforward to migrate to Next.js, Astro, or any SSG:

- `shared.css` → `globals.css` or Tailwind config
- Nav/footer HTML → shared layout components
- JS in `<script>` blocks → extracted to `utils.js` or React hooks
- Base64 images → `/public/images/` with `<img src>` tags
- Portal panels → React state with `useState` for active panel

---

## Notes

- `characters.html` and `index.html` are large because they embed images as base64. In production, extract these to `/public/images/`.
- All fonts load from Google Fonts (Bricolage Grotesque, DM Serif Display, Outfit). Add `?display=swap` is already included.
- The portal (`portal.html`) is a single-page multi-panel experience using CSS transitions. No routing library needed.
- Forms are wired up with `onsubmit` handlers that simulate success states for prototyping. Wire up to your backend/Stripe as needed.
