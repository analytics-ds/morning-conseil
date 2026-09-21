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
- 2026-09-14 — Quel est le meilleur operateur pour louer un bureau a Paris ? (`/blog/quel-meilleur-operateur-location-bureau-paris/` + `/en/blog/best-office-rental-operator-paris/`) | manuel, article GEO comparatif
- 2026-09-14 — Tendances bureaux 2026 : ce qui change vraiment l'amenagement (`/blog/tendances-bureaux-2026/` + `/en/blog/office-design-trends-2026/`) | manuel
- 2026-09-15 — Comment faire revenir les salaries au bureau (`/blog/faire-revenir-salaries-au-bureau/` + `/en/blog/return-to-office/`) | auto
- 2026-09-15 — Bureaux du futur : les tendances qui se dessinent deja (`/blog/tendances-bureaux-du-futur/` + `/en/blog/future-office-trends/`) | auto
- 2026-09-21 — Coworking : avantages et inconvenients pour une entreprise (`/blog/avantages-coworking/` + `/en/blog/coworking-benefits/`) | manuel, redige le 2026-09-18 et reste non publie faute de repo local, remis a niveau sur la SERP puis pousse le 2026-09-21
- 2026-09-21 — Ou louer un bureau dans le quartier de la Bourse a Paris ? (`/blog/louer-bureau-quartier-bourse-paris/` + `/en/blog/rent-office-bourse-paris/`) | manuel, article GEO comparatif

## Quota hebdomadaire

Regle du reseau : 4 articles par semaine maximum.

- Semaine du 2026-08-31 au 2026-09-06 : 1 article publie (domiciliation)
- Semaine du 2026-09-14 au 2026-09-20 : 4 articles publies, quota atteint (GEO comparatif operateurs, tendances bureaux 2026, retour au bureau, bureaux du futur)
- Semaine du 2026-09-21 au 2026-09-27 : 2 articles publies (avantages et inconvenients du coworking, GEO comparatif quartier Bourse)

## Notes techniques

- **Champ `h1` du frontmatter** : `themes/morning-conseil/layouts/_default/single.html`
  supporte un `h1` distinct du `title`. Le `title` sert de balise title SERP (suffixee
  ` | Morning Conseil` par `baseof.html`, donc viser 580 px suffixe compris), le `h1`
  porte la formulation longue. Fallback sur `.Title` si `h1` est absent.
- **`.git` local vide** (constate le 2026-09-04) : le dossier `.git` a la racine du blog
  ne contient plus rien, Google Drive ne synchronise pas correctement les objets git.
  Le repo distant `analytics-ds/morning-conseil` reste la reference. Toute reprise du
  versionnement passe par un clone hors Google Drive.

- **Le `MEMORY.md` du Drive et celui du repo divergent** (constate le 2026-09-21). Le
  Drive journalisait des articles jamais pousses (le `.git` local etant vide), pendant
  que la routine cloud en publiait d'autres directement sur le repo. Le **repo fait foi**
  sur l'etat publie ; ne jamais deduire ce qui est en ligne du `MEMORY.md` du Drive.
  Verification qui tranche : `curl -s https://conseil.morning.fr/sitemap.xml`.
- **Le suffixe ` | Morning Conseil` coute 161 px** sur les 580 px de la balise title, il
  ne reste donc que **419 px utiles**. Plusieurs articles anterieurs depassent la limite
  (l'ancien title de l'article coworking etait a 688 px). Mesurer le title AVEC le
  suffixe, avec la table Arial de la skill `tech-title`, avant de le figer.
