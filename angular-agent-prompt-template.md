## Project overview

Build a single-page marketing/concept website for **BUSINESS NAME**, a [SECTOR] business located in LEBANON. This is a redesign pitch demo — not a real client site — whose job is to look like a finished product, with an interactive before/after comparison as the centerpiece.

This is a **frontend-only, static** site. No backend, no API calls, no database, no CMS, no form submissions. All content is hardcoded directly into the components.

## Tech stack — non-negotiable

- **Angular**, latest stable version, **standalone components** (no NgModules).
- Component-scoped **SCSS** — no Tailwind, no Bootstrap, no UI component library. Hand-rolled CSS using the design tokens below.
- No routing library needed (for now) — this is a single scrolling page. If Angular Router is scaffolded by default, that's fine, but don't build multiple routes.
- No state management library (no NgRx, no Signals store). Local component state only — plain Angular `signal()` or simple class fields are both acceptable; use whichever is more idiomatic for the Angular version you scaffold.
- Must build and run cleanly with `ng serve` and `ng build` with zero errors or warnings on a fresh `ng new` workspace (routing: no, SSR: no — this is a pure client-side static app, since it will be deployed to a static host like Cloudflare Pages or GitHub Pages).

## Out of scope (do not build)

- No backend, no database, no environment config for APIs.
- No real form submission — the only interactive elements are external links (WhatsApp deep link, Instagram link) and the before/after slider.
- No authentication, no CMS, no i18n setup.
- No SSR/prerendering — client-side rendering is fine for a static demo.
- No automated test suite required beyond whatever Angular CLI scaffolds by default — don't spend effort writing custom unit tests unless it's trivial.

## Design direction

Use these as SCSS variables or CSS custom properties on `:root`, applied globally via `styles.scss`:

```scss
--bg: #12151b;
--bg-elev: #181d25;
--panel: #1d232c;
--border: #2b323d;
--text: #eceef1;
--text-dim: #9ba4b0;
--brass: #c9a15c;
--brass-strong: #e3c184;
--brass-soft: rgba(201, 161, 92, 0.14);

/* Used only inside the "before" mock panel, to look like a dated 2014-era site */
--before-bg: #ece6d8;
--before-ink: #2e2a22;
--before-link: #1a4fbf;
```

Typography: two Google Fonts, loaded via `<link>` tags in `index.html`.
- **Display/headings:** `Fraunces` (serif, weights 500/600/700) — fallback: `Georgia, 'Times New Roman', serif`.
- **Body/UI:** `Inter` (weights 400/500/600) — fallback: `-apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif`.

Overall look: dark charcoal background, warm brass/gold accent (not neon, not a generic dark-mode SaaS look) — think "premium automotive," not "startup dashboard." Rounded corners in the 12–16px range, generous whitespace, mobile-first.

## Component structure

Break the page into standalone components, composed in `AppComponent`:

1. **`SiteHeaderComponent`** — sticky top nav. Logo mark [(BADGE + WORDMARK)], nav links (LINK1 / LINK2 / LINK3 / ETC.) that scroll-link to section IDs, and a primary WhatsApp button. Collapse nav links on narrow viewports (keep the WhatsApp button visible).
2. **`HeroComponent`** — headline, subheadline, one CTA button (WhatsApp primary), and a simple inline SVG [IMAGE] with one subtle one-time "shine sweep" animation on load (respect `prefers-reduced-motion`).
3. **`CompareSliderComponent`** — the centerpiece. See below.
4. **`[ServicesComponent]`** — a responsive grid of 4 service cards (icon, title, one-sentence description).
5. **`TrustStripComponent`** — one line of real, non-fabricated social proof + social media profiles + location grid (Google Maps).
6. **`ContactCtaComponent`** — closing call-to-action panel with WhatsApp buttons.
7. **`SiteFooterComponent`** — disclosure line.

Pass content into components via `@Input()` only if you want reusability; hardcoding the copy directly inside each component's template is also fine since this is a single-use page, not a template product.

## Content to fill in

- Hero eyebrow badge: [ONE FACT — e.g. "Serving Lebanon since 2009" / "Family-run since 1998"]
- Headline: [SHORT, DISTINCTIVE, 2 LINES MAX, TIED TO WHAT THE BUSINESS ACTUALLY DOES]
- Subheadline: [1–2 SENTENCES EXPANDING ON THE HEADLINE]
- Primary CTA: [BUTTON BODY]
- [SECONDARY CTA:]

**[SERVICES / PRODUCTS]:**
- Offerings (3–5 cards): for each — [NAME] — [ONE-SENTENCE, CUSTOMER-FACING DESCRIPTION, no marketing jargon]
- Trust strip: [ONE REAL, NON-FABRICATED FACT] + link to [INSTAGRAM HANDLE]
- Closing CTA heading: [e.g. "Want to see more?" / "Ready to order?" — match the verb to the business]
- Closing CTA subtext: [1 SENTENCE]
- Footer disclosure (**keep fixed across every project**): "Concept design & build by Ali, a Lebanon-based web developer — not affiliated with [BUSINESS NAME]'s current [website/social presence]." + "Interested in making this real? Let's talk." linking to the same WhatsApp number.

## Non-functional requirements

- Fully responsive down to a narrow phone screen (~360px wide) — this will primarily be viewed on a phone, since it's sent as a link in a WhatsApp/Instagram message.
- Visible keyboard focus states on every interactive element.
- Respect `prefers-reduced-motion: reduce` by disabling the hero's shine animation and any transitions.
- No layout shift or horizontal scroll on mobile.
- Keep total bundle lean — no heavy component libraries, no unused dependencies.

## Deliverable

Output a complete, runnable Angular workspace: full file tree, every component's `.ts` / `.html` / `.scss`, `index.html` with the Google Fonts `<link>` tags, and `styles.scss` with the design tokens. State any assumption you had to make (e.g., exact Angular version scaffolded) in one line at the end — don't stop mid-build to ask about it.
