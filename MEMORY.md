# MEMORY — Morning Conseil

Journal des publications. Une ligne par article, suffixe `| auto` pour les articles
generes par `/create-article-auto`, `| manuel` pour ceux crees via `/create-article`.

## Publications

- 2026-08-27 — Prix d'un coworking a Paris : les tarifs reels en 2026 (`/blog/prix-coworking-paris/` + `/en/blog/coworking-prices-paris/`) | manuel
- 2026-08-27 — Bureau prive ou open space : comment choisir (`/blog/bureau-prive-ou-open-space/` + `/en/blog/private-office-vs-open-space/`) | manuel
- 2026-08-27 — Ou installer ses bureaux a Paris : les quartiers a comparer (`/blog/ou-installer-ses-bureaux-paris/` + `/en/blog/where-to-locate-offices-paris/`) | manuel
- 2026-08-27 — Flex office : mode d'emploi et pieges a eviter (`/blog/flex-office-mode-emploi/` + `/en/blog/flex-office-guide/`) | manuel
- 2026-08-27 — Amenager une salle de reunion : acoustique, lumiere, mobilier (`/blog/amenager-salle-de-reunion/` + `/en/blog/meeting-room-design/`) | manuel
- 2026-08-27 — Privatiser un lieu pour un seminaire a Paris (`/blog/privatiser-un-lieu-seminaire/` + `/en/blog/private-hire-venue-paris/`) | manuel
- 2026-09-04 — Domiciliation d'entreprise a Paris : le guide (`/blog/domiciliation-entreprise-paris/` + `/en/blog/company-registered-address-paris/`) | auto
- 2026-09-07 — Budget team building : le prix par personne (`/blog/budget-team-building/` + `/en/blog/team-building-budget-per-person/`) | auto

## Quota hebdomadaire

Regle du reseau : 4 articles par semaine maximum.

- Semaine du 2026-08-31 au 2026-09-06 : 1 article publie (domiciliation)
- Semaine du 2026-09-07 au 2026-09-13 : 1 article publie (budget team building)

## Notes techniques

- **Champ `h1` du frontmatter** : `themes/morning-conseil/layouts/_default/single.html`
  supporte un `h1` distinct du `title`. Le `title` sert de balise title SERP (suffixee
  ` | Morning Conseil` par `baseof.html`, donc viser 580 px suffixe compris), le `h1`
  porte la formulation longue. Fallback sur `.Title` si `h1` est absent.
- **`.git` local vide** (constate le 2026-09-04) : le dossier `.git` a la racine du blog
  ne contient plus rien, Google Drive ne synchronise pas correctement les objets git.
  Le repo distant `analytics-ds/morning-conseil` reste la reference. Toute reprise du
  versionnement passe par un clone hors Google Drive.
