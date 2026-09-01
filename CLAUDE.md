# Hugo Site Factory

Ce repo est un template pour creer des sites blogs statiques avec Hugo, optimises SEO/GEO, heberges gratuitement sur GitHub Pages.

## Comment ca marche

Ce repo ne contient pas de site. Il contient les **instructions et templates** pour que Claude Code genere un site complet automatiquement.

### Premier lancement

1. L'utilisateur connecte Claude Code a ce repo
2. L'utilisateur tape `/create-site`
3. Claude pose les questions necessaires (nom du site, couleurs, categories, etc.)
4. Claude genere tout le site Hugo, les fichiers SEO, et configure le deploiement
5. L'utilisateur push sur GitHub, active GitHub Pages, le site est en ligne

### Utilisation courante

- `/create-article` : creer un nouvel article de blog (choix parmi plusieurs types : article standard, comparatif) — workflow interactif
- `/create-article-auto` : **publication automatique** d'un article evergreen SEO bilingue FR+EN depuis la roadmap `.claude/roadmap.yaml`. Full auto, aucun input humain. Declenchee manuellement pour tester ou via routine `/schedule` 2x/semaine en production. Voir section "Publications evergreen automatiques" plus bas
- `/seo-setup` : generer ou mettre a jour les fichiers SEO techniques de base (robots.txt, llms.txt, sitemap, structured data)
- `/seo` : mode interactif pour modifier/ajouter des elements SEO (meta tags, JSON-LD, audit on-page, etc.)
- `/serve` : lancer le serveur Hugo en local (previsualisation sur `http://localhost:1313/`)
- `/share` : lancer Hugo + ngrok pour partager le site via un lien public (accessible par n'importe qui)

## Structure du repo

```
.claude/
├── skills/
│   ├── create-site.md           ← Workflow creation de site complet
│   ├── create-article.md        ← Workflow creation d'article (multi-types, interactif)
│   ├── create-article-auto.md   ← Publication auto d'article evergreen SEO depuis la roadmap (full auto)
│   ├── seo-setup.md             ← Workflow fichiers SEO techniques (baseline)
│   ├── seo.md                   ← Mode interactif SEO (modifications ponctuelles)
│   ├── serve.md                 ← Lancer le serveur Hugo en local
│   └── share.md                 ← Lancer Hugo + ngrok (partage public)
├── roadmap.yaml                 ← Roadmap editoriale evergreen (alimente /create-article-auto)
└── templates/
    ├── hugo-workflow.yml         ← GitHub Actions CI/CD
    ├── roadmap-template.yaml     ← Squelette commente de la roadmap editoriale
    ├── main.css                  ← CSS avec variables de charte graphique
    ├── articles/                 ← Templates d'articles par type
    │   ├── article-standard.md   ← Article informatif SEO + GEO (type par defaut)
    │   └── geo-comparatif.md     ← Article comparatif avec mise en avant
    ├── seo/                      ← Fichiers SEO techniques (editables)
    │   ├── robots.txt            ← Modele robots.txt
    │   ├── llms.txt              ← Modele llms.txt
    │   └── structured-data/      ← Schemas JSON-LD
    │       ├── article.json      ← BlogPosting
    │       ├── organization.json ← Organization
    │       ├── author.json       ← Person (auteur)
    │       ├── breadcrumb.json   ← BreadcrumbList
    │       ├── website.json      ← WebSite
    │       └── faq.json          ← FAQPage (a integrer manuellement)
    ├── layouts/
    │   ├── baseof.html           ← Layout de base
    │   ├── home.html             ← Page d'accueil
    │   ├── list.html             ← Pages de liste
    │   ├── single.html           ← Page article (avec affichage auteur)
    │   └── sitemap-html.html    ← Page plan du site (liste toutes les pages)
    └── partials/
        ├── header.html           ← Header/navigation
        ├── footer.html           ← Footer
        └── seo-head.html         ← Meta tags SEO + JSON-LD (OG, Twitter, canonical, schemas)
```

## Contexte du site

> Cette section est remplie automatiquement par le skill `/create-site`.
> Elle permet a Claude de connaitre le contexte du site pour les futures actions.

- **Nom du site** : Morning Conseil
- **Type de site** : Type A (site client exclusif, sous-domaine Morning, charte Morning)
- **Client** : Morning (https://www.morning.fr/) — location de bureaux et coworking
- **Consultant datashake** : Manon
- **Description** : Le guide pour choisir, amenager et faire vivre ses bureaux : location, coworking, salles de reunion, evenements et productivite
- **URL** : https://conseil.morning.fr/ (sous-domaine a faire creer par Morning, pas encore actif)
- **Couleurs** (relevees sur morning.fr, Webflow) : noir chaud #10100f (fonds sombres, navbar, hero), lin #f0eae4 / #f8f5f2 (fonds clairs), mango #fabb2a (accent, categories, pastilles), bleu de marque #2d62ff (CTA), border #e2d6cb, texte secondaire #6c6c65
- **Polices** : Archivo (display : H1, wordmark, titres de blocs, en 800 italique capitales), Archivo Narrow (titres secondaires, 700), Space Grotesk (corps de texte et UI, weight 300). Toutes sur Google Fonts. Titling Gothic FB et Geomanist Ultra sont utilisees par Morning mais proprietaires, donc remplacees par Archivo
- **Wordmark** : `MORNING.CONSEIL` en Archivo 800 italique capitales (meme traitement typographique que les titres de morning.fr). "MORNING" en lin a 1.3rem, ".CONSEIL" en mango a 0.95rem pour garder la hierarchie
- **Categories** : Location de bureaux, Coworking, Salle de reunion, Organisation d'evenement, Amenagement, Productivite
- **Langue** : Francais (fr) + Anglais (en) dans /en/
- **Auteurs** (fictifs, definis dans `data/authors.yaml`) :
  - `camille-deshayes` — Camille Deshayes, location de bureaux et coworking
  - `antoine-riviere` — Antoine Riviere, amenagement, space planning et salles de reunion
  - `helene-morvan` — Helene Morvan, evenementiel d'entreprise et productivite
- **Convention auteur** : le frontmatter porte `author: <slug>` (ex: `author: camille-deshayes`). Le slug doit exister comme cle dans `data/authors.yaml` ET avoir sa page `content/authors/<slug>/_index.md` (FR) + `content/en/authors/<slug>/_index.md` (EN), avec `layout: single` dans le frontmatter (sinon Hugo applique la liste des auteurs a la place de la fiche). Choisir l'auteur selon la categorie et les `topics` declares dans le YAML

### Angle editorial

Media de conseil sur le choix et la vie des espaces de travail. Contenus evergreen et GEO-ready (comparatifs, guides de choix, questions/reponses) qui citent et linkent morning.fr sur les requetes bureaux, coworking, amenagement et evenementiel.

Concurrents a citer avec prudence (ce sont les concurrents du client) : WeWork, Wojo, Deskeo, Regus, Ubiq.

### A faire avant la mise en ligne

Fait :

- Repo GitHub : `analytics-ds/morning-conseil` (public, comme tous les blogs du reseau)
- GitHub Pages actif en mode `workflow`. URL de demo : https://analytics-ds.github.io/morning-conseil/
- Logo officiel Morning en place dans le header (`static/images/morning-logo.svg`, version blanche de la navbar morning.fr)

Reste a faire :

- Faire creer le sous-domaine `conseil.morning.fr` par Morning (CNAME vers `analytics-ds.github.io`)
- Une fois le DNS en place : renseigner le domaine personnalise dans Settings > Pages, ajouter `static/CNAME` avec `conseil.morning.fr`, puis activer « Enforce HTTPS »
- Remplacer le favicon provisoire (`static/favicon.svg`, derive des couleurs du logo) par celui fourni par le client
- Rediger les 6 articles en anglais (`content/en/blog/` ne contient que `_index.md`)
- Mettre a jour `static/llms.txt` avec les URLs et titres reels

### Piege : URLs et sous-repertoire

Tant que le site est servi sur l'URL de demo, il vit dans le sous-repertoire
`/morning-conseil/`. Deux comportements de Hugo cassent les liens dans ce cas :

- `relURL` n'ajoute PAS le sous-chemin du baseURL si le chemin commence par un slash
- le `.URL` d'une entree de menu contient DEJA ce sous-chemin, mais perd le prefixe
  de langue en EN

Ne jamais appeler `relURL` / `relLangURL` directement sur un chemin a slash initial.
Utiliser les deux partials dedies :

- `{{ partial "asset.html" "/images/x.webp" }}` pour un fichier statique
- `{{ partial "link.html" .URL }}` pour un lien interne sensible a la langue

Verification apres build, sur les deux baseURL :

```bash
hugo --quiet --baseURL "https://analytics-ds.github.io/morning-conseil/" -d /tmp/mc-test
hugo --quiet -d /tmp/mc-public
```

puis controler qu'aucun `href` / `src` interne ne pointe vers un fichier absent.

## Regles generales

- Toujours utiliser `relURL` dans les templates Hugo pour les liens (compatibilite GitHub Pages)
- Les articles vont dans `content/blog/`
- Les slugs sont en minuscules, sans accents, mots separes par des tirets
- Ne JAMAIS utiliser `&` dans les noms de categories ou de tags — toujours remplacer par "et" (Hugo genere un double tiret `--` dans le slug, ce qui casse les URLs)
- Le ton des articles est impersonnel (pas de je/tu/nous/vous) sauf instruction contraire
- Les specs d'article (mots minimum, H2, blocs obligatoires) dependent du type choisi — lire les `<!-- NOTES POUR CLAUDE -->` dans chaque template d'article
- **Longueur minimum des articles evergreen : 800 mots par langue.** Regle imposee par Manon, non negociable. Si le sujet ne permet pas d'atteindre 800 mots sans remplissage, elargir l'angle plutot que de diluer. Verifier avant publication : `wc -w content/blog/<slug>.md` et `wc -w content/en/blog/<slug>.md`
- **Images d'article : toujours utiliser une photo reelle du site morning.fr**, jamais de banque d'images. Methode dans la section "Images des articles" plus bas
- Chaque article doit contenir au minimum 3 liens internes contextuels vers d'autres articles du blog. L'ancre de chaque lien doit contenir le mot-cle principal de l'article cible
- L'auteur est ajoute automatiquement dans le frontmatter et affiche sur la page (configure dans `hugo.toml [params]`)
- Les templates SEO dans `.claude/templates/seo/` sont editables par l'utilisateur — toujours lire la version en place avant de generer
- Pour ajouter un nouveau type d'article, creer un `.md` dans `.claude/templates/articles/` — il sera automatiquement propose par `/create-article`
- Pour ajouter un schema JSON-LD, creer un `.json` dans `.claude/templates/seo/structured-data/` et utiliser `/seo` pour l'integrer
- Chaque article doit avoir un champ `lastmod` dans le frontmatter (= date de derniere modification). Il est utilise par le sitemap XML, le sitemap HTML et le schema JSON-LD
- Quand un article est modifie, toujours mettre a jour le champ `lastmod` avec la date du jour
- Le sitemap HTML (`/plan-du-site/`) se regenere automatiquement a chaque build Hugo
- Toujours build et verifier (`hugo`) avant de commit

## Images des articles

Toutes les images du site (hero de la home, banniere d'article, visuels dans le corps) doivent etre des **photos reelles des espaces Morning**, prises sur morning.fr. Pas de banque d'images, pas d'illustration generique.

### Ou les trouver

morning.fr est un site Webflow : les images sont servies par `cdn.prod.website-files.com` et Webflow genere deja des variantes optimisees.

```bash
# 1. Recuperer une page morning.fr (WebFetch loupe les images, passer par curl)
curl -sL -A "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120 Safari/537.36" \
  https://www.morning.fr/bureaux-coworking -o /tmp/morning.html

# 2. Lister les images
grep -oE 'https://cdn\.prod\.website-files\.com/[^"?)]+\.(webp|jpg|png)' /tmp/morning.html | sort -u

# 3. Telecharger la variante 1600px deja optimisee par Webflow
#    (remplacer l'extension par -p-1600.webp sur l'URL de base)
curl -sL "<url>-p-1600.webp" -o static/images/hero/<nom-parlant>.webp
```

Pages riches en photos d'espaces : `/bureaux-coworking`, `/bureaux-coworking/<nom-espace>` (trevise, laffitte, argentine, duhesme, sofia, trocadero, grande-armee...), `/evenementiel/<nom-espace>`, `/amenagement`.

### Regles

- Format `.webp`, largeur 1600px max, viser moins de 200 Ko
- Rangement : `static/images/hero/` pour les hero, `static/images/blog/` pour les bannieres d'article
- Nommage en kebab-case, descriptif de la photo (ex: `coworking-trevise-open-space.webp`), pas du slug de l'article
- Choisir une photo coherente avec la categorie de l'article (salle de reunion pour un article salle de reunion, etc.)
- Renseigner le champ `image` du frontmatter avec le chemin absolu depuis la racine du site (ex: `image: /images/blog/coworking-trevise-open-space.webp`). C'est ce champ qui active la classe `.has-banner` du header et l'overlay sombre
- Alt text descriptif et en francais sur la version FR, en anglais sur la version EN
- Reutiliser une image deja telechargee plutot que d'en accumuler : verifier `static/images/` avant de recuperer une nouvelle photo

### Piege CSS a connaitre

`.article-header-overlay` et `.list-header-overlay` sont en `display: none` par defaut et ne s'affichent que sous `.has-banner`. Sans ce garde-fou, un article sans champ `image` voyait son overlay se positionner sur le `<body>` et assombrir toute la page. Ne pas retirer cette regle.

## Comment repondre a l'utilisateur

- Tutoiement, ton decontracte
- Pas de jargon technique sans explication
- Reponses structurees avec listes a puces
- Pas d'emoji sauf demande explicite




## Regle IMPERATIVE : toute nouvelle URL doit apparaitre dans le sitemap + plan de site

**Chaque fois qu une URL est ajoutee au site (article, page, categorie, auteur...), elle DOIT etre presente dans :**

### 1. Le sitemap XML (robots + bots)

Hugo genere automatiquement les sitemaps via :
- `layouts/sitemapindex.xml` -> `/sitemap.xml` (l index qui reference les sitemaps par langue)
- `layouts/sitemap.xml` -> `/fr/sitemap.xml` + `/en/sitemap.xml` (urlsets par langue)

Verifier apres build :
```bash
hugo
grep "<nouveau-slug>" public/fr/sitemap.xml public/en/sitemap.xml
```

### 2. Le plan de site HTML (utilisateurs + bots)

Page `/plan-du-site/` (FR) et `/en/site-map/` (EN) rendues via `layouts/_default/sitemap-html.html`. Elles listent toutes les pages groupees par section (Pages principales, Blog, Categories, Auteurs, Pages legales). Mise a jour automatique au build Hugo.

**LE LIEN VERS `/plan-du-site/` DOIT ETRE PRESENT DANS LE FOOTER DE TOUTES LES PAGES** (via `layouts/partials/footer.html`).

### 3. La page auteur

Page `/authors/<slug-auteur>/` qui liste automatiquement tous les articles dont le frontmatter contient `author: <slug>`. Verifier que le slug de l auteur dans le frontmatter correspond a un auteur defini dans `data/authors.yaml`.

### 4. La liste du blog

Page `/blog/` qui liste les articles par date decroissante. Hugo l inclut automatiquement si le fichier est dans `content/blog/` (FR) ou `content/en/blog/` (EN).

### 5. Le JSON-LD Article (SEO / schema.org)

L article genere automatiquement son schema.org/Article via `seo-head.html` (date, auteur, headline, image).

### 6. Le fichier llms.txt (referencement IA)

Le fichier `static/llms.txt` a la racine du site liste toutes les URLs strategiques destinees aux LLMs (ChatGPT, Claude, Perplexity, etc.).

**A chaque publication ou modification de contenu, ajouter la nouvelle URL dans la section appropriee du fichier `static/llms.txt`.**

Structure attendue :

```markdown
# Nom du Site

> Description courte et factuelle du site

## A propos

Description editoriale (methodologie, independance, auteurs experts, etc.)

## Articles de reference (FR)

- Titre de l'article 1 : https://domaine.com/blog/slug-1/
- Titre de l'article 2 : https://domaine.com/blog/slug-2/
- [a completer a chaque nouvel article]

## Version anglaise (EN) — si multilingue

- Homepage EN : https://domaine.com/en/
- Blog EN : https://domaine.com/en/blog/
- Title of article 1 : https://domaine.com/en/blog/slug-1/

## Informations techniques

- Generateur : Hugo (site statique)
- Multilingue : francais (defaut) + anglais (si applicable)
- Sitemap : https://domaine.com/sitemap.xml
- RSS : https://domaine.com/index.xml
- Schema.org : Organization, Article, BreadcrumbList, FAQPage, WebSite, CollectionPage, Person

## Contact

- URL : https://domaine.com/
```

Apres chaque nouvel article :
1. Ouvrir `static/llms.txt`
2. Ajouter la ligne `- Titre complet : URL absolue` dans la bonne section (FR ou EN)
3. Commit + push

### Workflow post-publication

```bash
# 1. Build
hugo

# 2. Verifier sitemap
grep "<nouveau-slug>" public/fr/sitemap.xml
grep "<nouveau-slug>" public/en/sitemap.xml  # si multilingue

# 3. Verifier plan de site HTML
grep "<nouveau-slug>" public/plan-du-site/index.html

# 4. Verifier page auteur
grep "<titre>" public/authors/<slug>/index.html

# 5. Verifier le footer (plan-du-site doit etre present)
grep "plan-du-site" public/index.html

# 6. Verifier llms.txt (mise a jour manuelle)
grep "<titre>" static/llms.txt

# 7. Commit + push
git add -A && git commit -m "Article : <titre>" && git push origin main
```

**Si l une des 5 verifications echoue, NE PAS COMMIT et debugger.**

## Publications evergreen automatiques

En plus des articles GEO (comparatifs, rediges manuellement), ce blog publie automatiquement des articles evergreen SEO via la skill `/create-article-auto` (c'est le blog pilote du systeme, lance 2026-04-23).

### Principe

- SEO pur, pas GEO. Mot-cle simple, analyse SERP auto, structure Hn basee sur les concurrents, redaction FR + EN.
- Full auto : aucun input humain au runtime. La seule intervention humaine est **la roadmap** (`.claude/roadmap.yaml`).
- Frequence cible : 2 articles/semaine (mardi + vendredi, 3h du mat, via routine `/schedule`).
- **800 mots minimum par langue.** Aucun article evergreen ne part en publication en dessous. Verifier avec `wc -w` avant le build.
- **Image obligatoire**, recuperee sur morning.fr (voir section "Images des articles"). Renseigner le champ `image` du frontmatter FR et EN.
- **Auteur obligatoire** : choisir parmi les 3 auteurs de `data/authors.yaml` selon la categorie (`camille-deshayes` pour location de bureaux / coworking, `antoine-riviere` pour salle de reunion / amenagement, `helene-morvan` pour organisation d'evenement / productivite).

### Roadmap

Fichier : `.claude/roadmap.yaml`. Format documente dans `.claude/templates/roadmap-template.yaml`.

Chaque entree decrit 1 article a publier. L'humain edite `kw`, `category`, `scheduled_date`. L'agent remplit `status`, `published_date`, `published_url_fr`, `published_url_en`, `error`.

**Categories valides** (doivent matcher exactement le `hugo.toml`) :

| Categorie FR (frontmatter) | Slug FR | Categorie EN | Slug EN |
|---|---|---|---|
| Location de bureaux | `/categories/location-de-bureaux/` | Office rental | `/en/categories/office-rental/` |
| Coworking | `/categories/coworking/` | Coworking | `/en/categories/coworking/` |
| Salle de reunion | `/categories/salle-de-reunion/` | Meeting rooms | `/en/categories/meeting-rooms/` |
| Organisation evenement | `/categories/organisation-evenement/` | Event planning | `/en/categories/event-planning/` |
| Amenagement | `/categories/amenagement/` | Workspace design | `/en/categories/workspace-design/` |
| Productivite | `/categories/productivite/` | Productivity | `/en/categories/productivity/` |

**Attention sur "Organisation evenement"** : le frontmatter porte la valeur SANS apostrophe (`Organisation evenement`), sinon Hugo genere le slug `organisation-devenement`. Le libelle affiche (`Organisation d'evenement`) est recupere depuis `content/categories/organisation-evenement/_index.md` via le partial `category-label.html`. Ne jamais mettre d'apostrophe dans une valeur de taxonomie.

### Modifier la roadmap

- Ajouter une entree : copier un bloc existant, remplir `kw` / `category` / `scheduled_date`, garder `status: todo`, laisser le reste a `null`.
- Reporter : changer `scheduled_date`.
- Debloquer un `failed` : corriger la cause indiquee dans `error`, repasser `status: todo`, vider `error`.

Demander a Claude "ajoute ces KW a la roadmap Morning Conseil" marche aussi, il edite le YAML en respectant le format.

### Suivi

- Roadmap : champs `published_date` + URLs des entrees traitees
- `MEMORY.md` a la racine du blog : ligne par article avec suffixe `| auto` pour les articles generes par cette skill (vs les articles manuels via `/create-article`)
- Logs : `.claude/logs/create-article-auto-[date].log` (rotation 30 derniers)

