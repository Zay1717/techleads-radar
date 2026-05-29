# TechLeads Radar 🎯

Outil de veille quotidienne pour cabinet de recrutement tech. Scrape **7 sources** tous les matins et génère un dashboard filtrable avec scoring automatique.

## Sources scrapées (~2000–5000 offres/jour)

| Source | Type | Offres attendues |
|---|---|---|
| France Travail API | API officielle | ~1000–1500 |
| APEC | API publique | ~100–200 |
| Welcome to the Jungle | Scraping | ~500–1000 |
| HelloWork | Scraping | ~300–800 |
| Collective.work | API/scraping | ~100–300 |
| Station F | Scraping | ~50–200 |
| **14 fonds VC** (Partech, Elaia, Alven, XAnge, Serena, Isai, Daphni, Breega, 360 Capital, Sequoia, Kima, Newfund, Balderton, Idinvest) | WelcomeKit API | ~200–600 |

## Installation

```bash
git clone https://github.com/TON-USERNAME/techleads-radar
cd techleads-radar
pip install -r requirements.txt
```

## Lancer le scraper

```bash
# Sans France Travail (aucune credential nécessaire)
python src/scrape.py

# Avec France Travail (credentials gratuits sur https://pole-emploi.io)
FT_CLIENT_ID=xxx FT_CLIENT_SECRET=yyy python src/scrape.py
```

Ouvre `index.html` dans ton navigateur.

## Déploiement GitHub Pages (automatique)

1. **Fork ou push** ce repo sur GitHub
2. Va dans **Settings → Pages** → Source: `gh-pages` branch
3. Va dans **Settings → Secrets** → Ajoute :
   - `FT_CLIENT_ID` (optionnel mais recommandé — +1000 offres)
   - `FT_CLIENT_SECRET`
4. Le scraper tourne **automatiquement du lundi au vendredi à 8h Paris**

L'URL sera : `https://TON-USERNAME.github.io/techleads-radar/`

## Credentials France Travail (gratuits)

1. Inscription sur https://pole-emploi.io/login
2. Crée une application → coche `api_offresdemploiv2`
3. Récupère `client_id` et `client_secret`
4. Ajoute-les dans les secrets GitHub

## Scoring (0–100)

| Critère | Points |
|---|---|
| Taille 50–200 salariés | +20 |
| Secteur Data/IA ou Architecture | +15 |
| Offre publiée aujourd'hui | +15 |
| Source fonds VC (startup garantie) | +10 |
| Taille 201–500 salariés | +15 |

## Structure

```
techleads-radar/
├── src/
│   └── scrape.py          # Scraper Python multi-sources
├── .github/workflows/
│   └── daily_scrape.yml   # Automatisation GitHub Actions
├── index.html             # Dashboard (généré automatiquement)
├── jobs.json              # Données brutes (généré automatiquement)
└── requirements.txt
```
