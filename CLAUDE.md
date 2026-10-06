# CLAUDE.md — Estudio Altiplano (studio website)

Context for Claude Code. Read this before every task in this repo.

> Lines marked **[TODO]** are open decisions the owner hasn't made yet. Don't invent answers for them; ask.

---

## The business

- **What it is:** a small web studio in San Luis Potosí, México, that designs and builds websites for local businesses.
- **Who runs it:** two people, both shown in the site's Equipo section. Frida Carlota Cordero Casados (commercial & creative direction: sales, design, identity, photography) and Daniel Ledezma Nájera (technical direction: code, hosting, security, local SEO). The site promises "Tratas directamente con quien escribe el código". Never write copy that implies a large agency or people who don't exist.
- **Ideal client:** a local, owner-run business in SLP (restaurants, cafés, shops, workshops, local services) that needs a fast, credible site and needs to be found on Google and Maps.
- **Positioning against generic freelancers, template builders and heavier agencies:**
  - Local and reachable, not a faceless agency
  - Fixed price agreed before starting
  - Domain and hosting registered in the client's name
  - No bloated plugins, no recurring license traps
  - WhatsApp-first contact
  - Bilingual ES/EN capability
- **Studio name, domain and email:** "Estudio Altiplano", live at `estudioaltiplano.mx`, contact `hola@estudioaltiplano.mx`. The README still calls these placeholders; that section is outdated.
- **[TODO]** Named competitors, if any.

## The packages

Pricing is fixed per project. Prices are **never shown on the public site** (deliberate decision; see README).

| Package | Includes |
|---|---|
| **Esencial** | One-page site, mobile-first, menu/services section, WhatsApp/call/Maps buttons, Google Business Profile setup, hosting + SSL + domain setup, 1 month of support |
| **Profesional** | Everything in Esencial + up to 5 pages, gallery/testimonials, contact form, professional email, analytics + Search Console, 3 months of support |
| **Completo** | Everything in Profesional + self-editable menu/catalog, bilingual ES/EN, reservation or pre-order form, team training, monthly maintenance plan |

**[TODO]** Internal price ranges, so copy and proposals stay consistent. They must never appear on the site.

## Goals (next 3–6 months)

1. **Generate WhatsApp leads** from local business owners. Every CTA ends in a prefilled `wa.me` chat.
2. **Rank locally** for searches like "diseño web San Luis Potosí" / "páginas web SLP".
3. **Serve as the live demo:** this site is the proof of quality. Performance, accessibility and polish are part of the sales pitch.
4. **Fill the work section** with real client projects as they ship. It currently shows "Próximamente".

## Brand

- **Tone:** casual but polished. Professional, warm, direct, local. Spanish copy uses **tú**. Never childish, never stiff corporate.
- **Personality:** premium, sober, strategic, contemporary, reliable.
- **Colors:**
  - Deep green `#2F3F36` (primary)
  - Cream `#E9E1D6`
  - Charcoal `#1C1A18`
  - Sand, stone and moss as accents
- **Logo:** a line-art seal: a yucca in front of the altiplano sierra, with "ESTUDIO / ALTIPLANO" around it (`assets/img/logo-sello.webp`, a transparent image used as a CSS mask so it can take any color). Small sizes use a simplified inline SVG mark (`.logo-mark`) next to a tracked uppercase wordmark. Fine line art and generous whitespace are part of the look.
- **Orange** is **not** a brand color. The old orange palma logo and the dark theme are retired.
- **Fonts:** Manrope (headings), Inter (body).
- **Full briefs:** `estudio-altiplano-brand-brief.md` and `ui-ux-design-brief.md`. Those take precedence over this summary.
- **Bilingual is strategic,** not decorative. It serves tourism, export and businesses selling beyond the state.

## Architecture

- **Code:** one static `index.html` with inline CSS and vanilla JS, plus `404.html`, `legal.html` (privacy notice and terms), `robots.txt`, `sitemap.xml` and `_headers`. No framework, no build step, no dependencies.
- **Share image:** `assets/img/og.jpg` is rendered from `assets/og-template.html` at 1200×630. Re-render it when the brand changes.
- **Hosting:** GitHub (`estudio-altiplano/sitio-estudio`) → Cloudflare Pages project `sitio-estudio-web`. Every push to `main` deploys to production automatically; every other branch gets its own preview URL. `main` is protected by a ruleset: changes go through a pull request.
- **Contact:** `CONFIG.whatsapp` in `index.html` controls WhatsApp mode versus email-only mode.
- **i18n:**
  - Spanish is the source text in the HTML.
  - English goes in a `data-en` attribute.
  - Translatable elements must be **leaf elements** with no children. Split inline markup into sibling `<span>`s.
  - Every new piece of visible text needs a `data-en`.
- **No contact form** on the studio site. This avoids the LFPDPPP privacy-notice obligation and WhatsApp converts better.
- **No cookies, no consent banner.** Only cookieless analytics are allowed. The site uses Umami Cloud (`CONFIG.umamiId`), with custom events for CTAs, packages, sections, FAQ, language and scroll depth.
- **CSP** lives in `_headers`. If you add any external origin (fonts, scripts, images), update the CSP or it will break in production.
- **[TODO]** Will client sites live in separate repos, or will this become a reusable template?

## Working rules for Claude

- **Never push to `main`.** It deploys straight to production. Work on a branch and open a PR.
- Don't add frameworks, build tools, npm packages or external JS without explicit approval.
- Don't restructure the site (sections, file layout) without approval.
- Spanish stays the source language. Write natural Mexican Spanish, not translated-from-English Spanish.
- Every change must keep:
  - Mobile at 320 px working
  - Lighthouse at ≥ 90 performance, ≥ 95 accessibility and 100 SEO
  - The ES/EN toggle working in both directions
- Never add prices, fake testimonials or fake client logos to the site.
- Before finishing a task, test locally with `python3 -m http.server 8000` and check both languages.

## Known open issues

- The README checklist still says `assets/img/og.jpg` doesn't exist, but it does now (1200×630).
- The README checklist says "4 find-and-replace edits" but the table lists 3.
- The README still describes the name, domain, email and logo as placeholders, and its file list and analytics notes are outdated.
