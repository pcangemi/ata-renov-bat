# ATA Rénov'Bat — one-page site rebuild (2026 design)

**Date**: 2026-07-20 · **Status**: approved by user ("lets go")

## Context

ATA Rénov'Bat was an independent electrician business (Atallah Hassani, active since 2011,
now closed; the artisan is now based in Juan-les-Pins, no longer Vallauris). Its site was a React 17 / MUI
"theFront" template deployed on a VPS that is now offline. The owner of this rebuild
(Pierre) wants the same content and feeling in a modern 2026 design, drastically
simplified, hosted free on GitHub Pages with redeploy-on-push.

Sources: `~/Library/Mobile Documents/com~apple~CloudDocs/ata-renov-bat-v2` (React
sources — canonical text content), Wayback Machine (real photos), `social.png`
(screenshot of original site — logo + hero photo reference).

## Goals

1. One `index.html` — plain HTML/CSS/vanilla JS. No build step, no React, no
   Facebook integration, no analytics, no cookie banner.
2. Same content structure and features as the old site, one page with anchors.
3. Distinctive "spec-sheet editorial" design (not generic-AI-looking).
4. Public repo `pcangemi/ata-renov-bat`, GitHub Pages via Actions, auto-deploy
   on every push to `main`.

## Visual system

- Paper background `#F7F6F2`, ink text `#14181A`, single accent: brand green
  `#03A678` (kept from original logo).
- Type: Space Grotesk (display), Inter (text), JetBrains Mono (schematic labels
  like `01 / PRESTATIONS`). Google Fonts.
- Motifs: dashed circuit-trace separators, oversized outline section numerals,
  duotone/desaturated photo treatment, mono uppercase eyebrows.
- Motion: scroll reveals via IntersectionObserver + CSS transitions; typed
  rotating word in hero (~30 lines vanilla JS); honors `prefers-reduced-motion`.
- Responsive: desktop-first grid collapsing to one column; nav links hidden on
  small screens (logo + tel CTA remain); no horizontal overflow at 390px.

## Page structure & content (all French, from the old sources verbatim)

1. **Nav** (fixed): real ATA logo (SVG recovered from `src/svg/logo/Logo.js`) +
   links Prestations / À propos / Réalisations / Avis / Contact + `tel:` CTA
   button "07 58 50 51 42".
2. **Hero**: eyebrow `ÉLECTRICITÉ GÉNÉRALE · JUAN-LES-PINS`; headline "Nous assurons
   votre installation électrique de sa **[conception. / mise aux normes. /
   maintenance. / modernisation.]**" (typed loop); subline "Nous avons
   l'expérience, le personnel et les ressources…"; CTAs "Nos réalisations"
   (anchor) and "Demander un devis" (anchor to contact); fact chips
   "Depuis 2011 · 4,9/5 Google · Décennale MAAF". Hero photo: real sparks
   action shot (bg-3.jpg).
3. **Partners**: Schneider Electric, Legrand, Hager, Nexans, Otio SVGs (from old
   repo `public/companies/`), grayscale strip.
4. **Prestations**: content from CaseStudy1 + hero rotation recomposed as cards:
   conception & installation, mise aux normes, maintenance & dépannage,
   modernisation, performance énergétique — plus MAAF **assurance décennale**
   callout (maaf.svg + original text "Nous sommes désormais couverts par une
   assurance décennale…").
5. **À propos**: "Demandez l'excellence" story (artisan indépendant depuis 2011,
   14+ ans d'expérience — full original paragraph). Photo: plasterboard worksite
   crop from social.png.
6. **Réalisations**: 6-card grid. One real photo — tableau électrique
   (bg-5.jpg) — plus 5 Higgsfield-generated documentary-style images (éclairage
   extérieur, domotique, gaines/saignées, luminaires, rénovation pièce) matched
   in tone. Titles are real service names, not lorem. (The other two real photos
   are used in Hero and À propos.)
7. **Avis**: "Nous sommes notés 4,9/5 par nos clients !" + original intro + the
   6 real Google reviews verbatim (Mathieu Parigot, Jacob Nielsen, Marc Pey,
   Stephanie Froc, Jeremy Lemercier, Pierre Cangemi) with initial-letter avatars.
8. **Contact**: cards — ☎ 07 58 50 51 42 (`tel:`), ✉ ata.renov.bat@outlook.fr
   (`mailto:`), 📍 Juan-les-Pins — Antibes (06160), interventions dans les
   Alpes-Maritimes (no street address published, no map iframe). WhatsApp CTA. Simple form (nom,
   téléphone, message) with success state, not wired — Formspree-ready.
9. **Footer**: logo, anchor nav, contact, legal line "© 2026 ATA Rénov'Bat ·
   Juan-les-Pins".
10. **Floating WhatsApp button** → `https://wa.me/33670634666` (replaces the
    React widget).
11. **404.html**: minimal, same visual language, link back home.

## Assets

- `images/logo.svg` — converted from Logo.js React component (mechanical JSX→SVG).
- Real photos (Wayback/-social.png): hero sparks, tableau électrique, plasterboard
  crop. Optimized (max ~1600px, JPEG q80).
- Generated (Higgsfield, via higgsfield-generate skill): 3–4 réalisations fill
  images, documentary tone, no identifiable faces presented as the artisan.
- Partner SVGs + favicon (real logo mark).

## Deploy

Same pipeline as drycups-site: `.github/workflows/deploy.yml` (checkout →
configure-pages → upload-pages-artifact → deploy-pages), Pages `build_type=workflow`,
CDN scripts (none — no external JS libs at all; fonts only). SRI n/a.

## Out of scope

- Custom domain, form backend wiring (Formspree endpoint to be provided later),
  Actualités/blog (old nav had it; page never existed), multi-language.

## Acceptance

- Page renders identically-structured content to old site, in the new design.
- No console errors; no horizontal overflow at 390px; reduced-motion respected.
- Repo public, Pages live, push-to-deploy verified.
