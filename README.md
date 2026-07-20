# ATA Rénov'Bat — site vitrine

Rebuild statique du site d'ATA Rénov'Bat (électricité générale, Juan-les-Pins),
reconstruit depuis les sources React d'origine dans un design 2026 « spec-sheet
editorial ». Une seule page `index.html` — HTML/CSS/JS vanilla, aucun build.

Photos : 3 photos réelles récupérées (archives du site d'origine) + images
d'illustration générées, signalées comme telles.

## Développement

```bash
python3 -m http.server 8000
# http://localhost:8000
```

## Déploiement

Chaque push sur `main` redéploie sur GitHub Pages via `.github/workflows/deploy.yml`.
URL : https://pcangemi.github.io/ata-renov-bat/
