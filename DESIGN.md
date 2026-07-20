---
name: ATA Rénov'Bat
description: Spec-sheet editorial one-pager for an exacting independent electrician in Juan-les-Pins
colors:
  paper: "#F7F6F2"
  ink: "#14181A"
  ink-soft: "#4A5258"
  line: "#14181A29"
  chantier-green: "#03A678"
  chantier-green-deep: "#028763"
  green-wash: "#03A67814"
typography:
  display:
    fontFamily: "Space Grotesk, sans-serif"
    fontSize: "clamp(38px, 5vw, 64px)"
    fontWeight: 700
    lineHeight: 1.04
    letterSpacing: "-0.02em"
  headline:
    fontFamily: "Space Grotesk, sans-serif"
    fontSize: "clamp(28px, 3.6vw, 44px)"
    fontWeight: 500
    letterSpacing: "-0.02em"
  title:
    fontFamily: "Space Grotesk, sans-serif"
    fontSize: "21px"
    fontWeight: 500
    letterSpacing: "-0.02em"
  body:
    fontFamily: "Archivo, system-ui, sans-serif"
    fontSize: "16px"
    fontWeight: 400
    lineHeight: 1.6
  label:
    fontFamily: "JetBrains Mono, monospace"
    fontSize: "12px"
    fontWeight: 400
    letterSpacing: "0.14em"
rounded:
  sm: "4px"
  md: "6px"
spacing:
  gap: "22px"
  card: "24px"
  section: "96px"
components:
  button-primary:
    backgroundColor: "{colors.chantier-green}"
    textColor: "#FFFFFF"
    rounded: "{rounded.sm}"
    padding: "13px 24px"
    typography: "{typography.title}"
  button-primary-hover:
    backgroundColor: "{colors.chantier-green-deep}"
  button-ink:
    backgroundColor: "{colors.ink}"
    textColor: "{colors.paper}"
    rounded: "{rounded.sm}"
    padding: "13px 24px"
  button-outline:
    backgroundColor: "#00000000"
    textColor: "{colors.ink}"
    rounded: "{rounded.sm}"
    padding: "13px 24px"
  card:
    backgroundColor: "#00000000"
    rounded: "0px"
    padding: "24px 0 0"
  input:
    backgroundColor: "#FFFFFF"
    textColor: "{colors.ink}"
    rounded: "0px"
    padding: "14px 16px"
---

# Design System: ATA Rénov'Bat

## 1. Overview

**Creative North Star: "Le Dossier Technique"**

The site is composed like the technical dossier a meticulous electrician would hand you with his devis: photographs framed as numbered figures with monospace captions, schematic section labels, a faint drafting grid under everything, one engineer's-marker green for what matters. The presentation itself is the proof of rigor — if the site is this precise, so is the wiring. Warmth comes from real chantier photography and the artisan's own story, never from decorative softness.

The system explicitly rejects: the generic template look of the old site, interchangeable AI landing-page aesthetics, urgency marketing, and wellness-cream softness (see PRODUCT.md anti-references). Motion is choreographed but calm — GSAP entrance and scroll reveals with Lenis smoothing, always disabled under `prefers-reduced-motion`.

**Key Characteristics:**
- Paper-white drafting surface with a faint 72px grid
- One accent: the original brand green, used for action and emphasis only
- Content sits openly on the paper, structured by hairline rules — almost no boxes
- Two framed "document" figures only (hero, à propos) with mono captions
- Réalisations is an animated masonry of unframed photographs
- Giant outline section numerals drifting on scroll
- Grotesk display type over a workmanlike body sans, mono for labels

## 2. Colors

A restrained paper-and-ink base that lets the single chantier green read as signal, never decoration.

### Primary
- **Chantier Green** (#03A678): the original ATA logo green, kept as the sole accent. Primary buttons, links, active labels, the WhatsApp float, the caret of the typed headline. Its deep variant (#028763) is the hover state and link color on paper.

### Neutral
- **Paper** (#F7F6F2): the body surface, overlaid with a 1px drafting grid at 2.5% ink.
- **Ink** (#14181A): headings, body emphasis, the nav CTA, the footer surface.
- **Soft Ink** (#4A5258): body and caption text on paper (≈7:1 contrast — never lighten it).
- **Line** (#14181A at 16%): every rule — figure frames, list separators, form fields. Hairline only.
- **Green Wash** (#03A678 at 8%): tinted background for the MAAF callout and contact icons.

### Named Rules
**The One Green Rule.** Green appears only where it means something: an action, an active state, a key term. If a screen is more than ~10% green, it has stopped being signal.
**The Hairline Rule.** All structure is drawn with 1px lines at 16% ink. No shadows-as-borders, no thick strokes, no side-stripes.
**The Open Paper Rule.** Content is not boxed. Services, reviews and contact rows sit directly on the paper, separated by hairline top-rules. Full borders are reserved for the two framed figures (hero, à propos), the MAAF décennale callout (the one sanctioned box, green-washed), and buttons. There is no form: contact is direct-only (tel:, WhatsApp, mailto:). The owner's verdict on bordered card grids: "too much boxes, feels way too AI generated".

## 3. Typography

**Display Font:** Space Grotesk (sans-serif fallback)
**Body Font:** Archivo (system-ui fallback)
**Label/Mono Font:** JetBrains Mono

**Character:** A drafting-table pairing — Space Grotesk's slightly quirky engineering geometry for statements, Archivo's plainspoken neutrality for reading, JetBrains Mono in uppercase for the schematic apparatus (section labels, figure captions).

### Hierarchy
- **Display** (700, clamp(38px, 5vw, 64px), 1.04): the hero headline only, with the typed green rotating word.
- **Headline** (500, clamp(28px, 3.6vw, 44px), 1.05): section titles.
- **Title** (500–700, 17–21px): card and work titles.
- **Body** (400, 14.5–18px, 1.6): all prose, in Soft Ink; ledes at 18px.
- **Label** (400, 11–12px, +0.14em, UPPERCASE, mono): section eyebrows (`01 / Prestations`), figure captions (`Fig. 02`), footer column heads.

### Named Rules
**The Apparatus Rule.** Mono uppercase is reserved for the documentary apparatus — numbering, captions, column labels. Never for persuasive copy or CTAs.

## 4. Elevation

Essentially flat: depth is conveyed by hairline rules and the drafting grid, not by shadows or fills. Exactly two shadows exist — the WhatsApp float (`0 10px 26px -8px` green at 65%, it must read as touchable above everything) and none elsewhere at rest. The dark footer is tonal inversion, not elevation.

### Named Rules
**The Flat Dossier Rule.** Surfaces sit on the paper, they do not hover over it. If a card casts a shadow, it's a bug.

## 5. Components

### Buttons
- **Shape:** barely rounded (4px) — tool, not pill.
- **Primary (green):** Chantier Green fill, white text, Space Grotesk 15px; hover deepens to #028763.
- **Ink:** solid #14181A fill with paper text (the nav phone CTA); hover goes green-deep.
- **Outline:** 1px ink border, transparent fill; hover inverts to ink fill.
- **Hover / Focus:** color shifts only, 0.2s; no scale, no glow.

### Open list items (services, reviews, contact rows)
- **Structure:** hairline top-rule (1px Line), no background, no side/bottom borders, no radius.
- **Internal spacing:** 24px below the rule; content directly on paper.
- **Emphasis variant:** the MAAF callout uses a 1px Ink top-rule (heavier voice, same grammar).

### Navigation
- Fixed, paper at 85% with backdrop blur, hairline bottom border. Logo left, Archivo 14px links center (hidden ≤1020px), ink phone-CTA right. Anchor scrolling glides via Lenis.

### Testimonials
Open quotes on hairline rules: a green 5-star row (12px) heads each review; the three long reviews sit in wide cells set as Space Grotesk pull-quotes (20px, ink); attribution uses 36px green-wash mono initial tags, not photo avatars. The partner marquee is full-bleed (11 brands ×3 sets for seamless wide-screen looping: Schneider Electric, Legrand, Hager, Nexans, Otio, Siemens, Bosch, ABB, Philips Hue, TP-Link, Shelly).

### The Figure Frame (hero and à propos only)
The two "document" photographs sit in a bordered frame: image (saturation 0.82, contrast 1.04), hairline caption bar with mono `Fig. 0X` label. Images scale in from 1.09 inside a clipped wrapper on reveal.

### The Masonry Gallery (signature)
Réalisations is a 3-lane balanced masonry: three explicit columns of three unframed photos whose aspect ratios (3/4, 4/5, 4/3, 1/1, 6/5) are chosen so every lane's total height is identical — the gallery starts and ends on exact shared lines. Uniform text blocks (one-line title, two-line clamped description) preserve the balance. On scroll the lanes enter vertically offset (42/110/68px) and converge to perfect alignment via scrubbed GSAP; hover zooms photos 1.045 inside clipped 6px-radius wrappers. 1 column ≤620px.

## 6. Do's and Don'ts

### Do:
- **Do** keep Soft Ink (#4A5258) as the floor for text on paper; never lighter.
- **Do** frame every photo as a numbered figure with a mono caption — no naked images.
- **Do** keep motion in the established grammar: GSAP power3.out reveals, Lenis smoothing, marquee partners — all gated behind `prefers-reduced-motion`.
- **Do** keep every fold one action away from `tel:` or WhatsApp (PRODUCT.md: "One call away").
- **Do** keep the page a single self-contained HTML file; no build step, no framework.

### Don't:
- **Don't** produce "generic AI landing-page aesthetics" (PRODUCT.md's words): gradient text, glassmorphism, hero-metric templates, identical icon-card grids.
- **Don't** add urgency furniture — countdowns, discount banners, popup chat. The register is calm confidence.
- **Don't** drift toward wellness-cream softness: no serif italics, no warm beige drench, no rounded-pill everything.
- **Don't** introduce a second accent color or use green decoratively (One Green Rule).
- **Don't** add shadows to resting surfaces (Flat Dossier Rule) or side-stripe borders thicker than 1px.
- **Don't** box content into bordered cards — hairline top-rules only (Open Paper Rule).
- **Don't** re-label photos with provenance badges (réel/illustration) — the owner removed them deliberately.
