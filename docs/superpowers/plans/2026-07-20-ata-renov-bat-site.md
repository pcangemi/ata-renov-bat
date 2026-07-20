# ATA Rénov'Bat One-Page Site Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Rebuild the ATA Rénov'Bat site as one static HTML page in a "spec-sheet editorial" 2026 design, deployed to GitHub Pages with auto-redeploy on push.

**Architecture:** A single `index.html` carrying all markup, CSS and vanilla JS (typed hero word, IntersectionObserver reveals, form success state, FAQ-less), an `images/` folder (real recovered photos + generated ones + partner SVGs + converted logo), and the same Actions Pages pipeline as drycups-site.

**Tech Stack:** Plain HTML/CSS/JS, Google Fonts (Space Grotesk, Inter, JetBrains Mono), GitHub Actions Pages deploy. No JS libraries, no build step.

## Global Constraints

- Repo: public `pcangemi/ata-renov-bat`, branch `main`, live at `https://pcangemi.github.io/ata-renov-bat/`.
- Colors: paper `#F7F6F2`, ink `#14181A`, accent `#03A678` only.
- All copy French, taken verbatim from the old React sources (quoted in Task 4).
- Location: Juan-les-Pins (NOT Vallauris). Phone `07 58 50 51 42`, email `ata.renov.bat@outlook.fr`, WhatsApp `https://wa.me/33670634666`.
- No Facebook, no analytics, no cookie banner, no map iframe, no external JS.
- `prefers-reduced-motion` disables typed loop + reveals.
- No horizontal overflow at 390px viewport.
- Scratchpad assets live in `<scratchpad>/ata-photos/` and `<scratchpad>/ata-src/` (already downloaded); old repo at `~/Library/Mobile Documents/com~apple~CloudDocs/ata-renov-bat-v2` (iCloud, slow — copy files individually).

---

### Task 1: Scaffolding (workflow, gitignore, README)

**Files:**
- Create: `.github/workflows/deploy.yml` (byte-identical to drycups-site's)
- Create: `.gitignore` (`.DS_Store`, `.claude/`, `.playwright-mcp/`)
- Create: `README.md` (project description, no-build dev instructions, deploy pipeline, content provenance note)

**Interfaces:** Produces the deploy pipeline every later push relies on.

- [ ] Step 1: Copy `deploy.yml` from `/Users/pcangemi/Documents/Projects/drycups-site/.github/workflows/deploy.yml` unchanged.
- [ ] Step 2: Write `.gitignore` and `README.md`.
- [ ] Step 3: Verify: `ls .github/workflows/deploy.yml .gitignore README.md` → all exist.
- [ ] Step 4: Commit `chore: scaffolding (Pages workflow, gitignore, README)`.

### Task 2: Static assets (photos, logos, favicon)

**Files:**
- Create: `images/hero-sparks.jpg` (from scratchpad `ata-photos/bg-3.jpg`, resized ≤1600px, q80)
- Create: `images/tableau.jpg` (from `ata-photos/bg-5.jpg`, same treatment)
- Create: `images/chantier-placo.jpg` (crop of `scratchpad/social.png` photo region ≈ x1276-2450, y409-1356, saved JPEG q85)
- Create: `images/logo.svg` (mechanical conversion of old `src/svg/logo/Logo.js` JSX → plain SVG: strip imports/exports, `{...props}`, convert `style={{k:v}}` to `style="k:v"`, `clipPath`→`clip-path` attr syntax)
- Create: `images/partners/{schneider-electric,legrand,hager,nexans,otio,maaf}.svg` (copied one-by-one from old repo `public/companies/`)
- Create: `images/favicon.png` (from `ata-photos/favicon.png` as-is)

**Interfaces:** Produces exact filenames Task 4's HTML references.

- [ ] Step 1: Python/PIL script: resize/save the two JPEGs, crop social.png region, verify each output opens with PIL and is <350KB.
- [ ] Step 2: Python script converts Logo.js → logo.svg; verify with `xmllint --noout images/logo.svg` (or Python XML parse) and by rendering: file starts `<svg viewBox='0 0 1587.52 700'`.
- [ ] Step 3: Copy the 6 partner SVGs individually (iCloud: one `cp` per file, 45s timeout each).
- [ ] Step 4: Commit `feat: real recovered assets (photos, logo, partner SVGs)`.

### Task 3: Generated réalisations images (Higgsfield)

**Files:**
- Create: `images/real-eclairage.jpg`, `images/real-domotique.jpg`, `images/real-gaines.jpg`, `images/real-luminaires.jpg`, `images/real-renovation.jpg`

**Interfaces:** Produces exact filenames Task 4 references. REQUIRED SUB-SKILL: `higgsfield-generate` before any `mcp__higgsfield__*` call.

- [ ] Step 1: Invoke higgsfield-generate skill; generate 5 documentary-style photos (French residential worksites: applique extérieure en façade, thermostat/domotique mural, saignées + gaines ICTA dans mur, luminaires suspendus posés dans séjour rénové, pièce en cours de rénovation avec câblage). Tone: natural light, realistic imperfection, no visible faces, 4:3.
- [ ] Step 2: Download results into `images/` with the names above; resize ≤1400px q80; verify each <300KB and opens.
- [ ] Step 3: Commit `feat: illustrative réalisations photos (generated)`.

### Task 4: index.html (full page)

**Files:**
- Create: `index.html`

**Interfaces:** Consumes every image filename from Tasks 2–3. Produces anchors `#prestations #apropos #realisations #avis #contact` used by nav, footer and 404.

Copy (verbatim from old sources): hero headline "Nous assurons votre installation électrique de sa" + rotation `['conception.','mise aux normes.','maintenance.','modernisation.']`; subline "Nous avons l'expérience, le personnel et les ressources pour que votre projet se réalise selon vos envies. Et dans les temps ..."; CaseStudy1 texts (Perfomance énergétique / Normes / Électricité paragraph / MAAF décennale paragraph); "Demandez l'excellence" à-propos paragraph; reviews header "Nous sommes notés 4.9/5 par nos clients!" + intro + the 6 reviews (Mathieu Parigot, Jacob Nielsen, Marc Pey, Stephanie Froc, Jeremy Lemercier, Pierre Cangemi — text, name, service title); contact intro "Pour tout renseignement ou demande de devis, nous sommes à votre écoute également par téléphone ou mail."

JS (all inline, ~80 lines): typed-word loop (type/erase with setTimeout, 80ms/40ms, 1.6s hold, skipped under reduced-motion — word shown statically); IntersectionObserver adding `.in` to `[data-reveal]` at threshold .15; form button click → hide form, show success block; year stamp.

- [ ] Step 1: Write full `index.html` (sections per spec: nav, hero, partners, prestations, à propos, réalisations, avis, contact, footer, WhatsApp float).
- [ ] Step 2: `python3 -m http.server 8742` + Playwright: desktop 1280 screenshot, mobile 390 screenshot, console messages (expect 0 errors), overflow check (`document.documentElement.scrollWidth === 375..390`), typed word visibly changes, form success toggles.
- [ ] Step 3: Fix anything found; re-verify.
- [ ] Step 4: Commit `feat: one-page site`.

### Task 5: 404.html

**Files:**
- Create: `404.html` (paper bg, mono `404 / PAGE INTROUVABLE`, link `← Retour à l'accueil` to `/ata-renov-bat/`)

- [ ] Step 1: Write file; Playwright screenshot to confirm styling.
- [ ] Step 2: Commit `feat: 404 page`.

### Task 6: Publish (repo, Pages, live verification)

- [ ] Step 1: `gh repo create pcangemi/ata-renov-bat --public --source . --push` (or create + `git remote add` + push).
- [ ] Step 2: `gh api -X POST repos/pcangemi/ata-renov-bat/pages -f build_type=workflow`.
- [ ] Step 3: `gh run watch <id> --exit-status` → success.
- [ ] Step 4: `curl` live URL → 200, title contains "ATA Rénov'Bat"; spot-check one image 200.
- [ ] Step 5: Update memory file with new repo info.

## Self-Review

- Spec coverage: nav/hero/partners/prestations/à-propos/réalisations/avis/contact/footer/WhatsApp/404/deploy → Tasks 1–6 ✓; reduced-motion + overflow acceptance in Task 4 Step 2 ✓; Juan-les-Pins constraint global ✓.
- Placeholders: none — copy quoted or referenced to exact source strings gathered during exploration (visible in session context; Task 4 lists every text block).
- Naming consistency: image filenames defined in Tasks 2–3 match Task 4 usage ✓.
