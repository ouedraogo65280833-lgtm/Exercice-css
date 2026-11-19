# Exercice 12 — Défi : habiller « Le marché des saveurs »

**Niveau 4 · Récolte** · ★★★★ · Durée : 3 h · Notions : toutes celles des exercices 01 à 11

> La coopérative « Le marché des saveurs » est ravie du site que vous avez construit au défi HTML 15… mais il est tout blanc, et le Salon de l'agriculture ouvre bientôt ! La graphiste vous a envoyé une charte graphique et des maquettes pour l'ordinateur et le téléphone. À vous de jouer : **une seule feuille de style** pour habiller les 5 pages, belle et lisible sur tous les écrans.

Ce défi est une **répétition générale de la partie CSS du brief PlantEvo** : même démarche (maquette → feuille de style commune → tests sur plusieurs écrans → documentation), sur un autre sujet.

## Prérequis

- Avoir terminé le **défi HTML 15** (série `exercices-html`, `niveau-4-recolte/15-defi-mini-site`) : vous allez habiller **votre propre site**.
- Copiez dans ce dossier (`12-defi-habiller-site/`) vos fichiers du défi HTML 15 : `index.html`, le dossier `pages/`, le dossier `images/` et votre `README.md`. Avant de copier votre `README.md`, **renommez cette consigne** en `CONSIGNE.md` pour ne pas l'écraser.
- Vous n'avez pas terminé le défi HTML 15 ? **Demandez au coach** un HTML de départ.

## Objectifs

- Passer d'une **charte graphique** et de **maquettes** à une feuille de style complète.
- Réutiliser **seul** toutes les notions de la série : sélecteurs, cascade, boîte, Flexbox, Grid, responsive, interactivité, variables.
- Écrire une seule feuille de style **organisée, commentée et légère**, partagée par plusieurs pages.
- Tester son site sur plusieurs largeurs d'écran et au clavier, le valider et le documenter.

## Fichiers fournis

```
12-defi-habiller-site/
├── README.md                            ← cette consigne (à renommer en CONSIGNE.md)
└── maquettes/
    ├── charte-graphique.svg             ← couleurs, polices, formes
    ├── maquette-accueil-ordinateur.svg  ← accueil sur grand écran (1280 px)
    ├── maquette-accueil-telephone.svg   ← accueil sur téléphone (375 px)
    ├── maquette-categorie-ordinateur.svg← une page catégorie (1280 px)
    └── maquette-contact-telephone.svg   ← page contact sur téléphone (375 px)
```

Ouvrez la charte et les quatre maquettes dans votre navigateur (glisser-déposer le fichier) avant de commencer. Les **étiquettes violettes** sont des annotations de la graphiste : elles expliquent la mise en page, elles ne font pas partie du site.

> Les maquettes montrent l'**esprit** du site, pas votre HTML exact : si votre page Fruits a 4 produits ou pas de tableau, adaptez. Ce qui compte, ce sont les exigences ci-dessous.

## Cahier des charges

### Arborescence attendue

```
12-defi-habiller-site/
├── index.html
├── CONSIGNE.md          ← cette consigne, renommée
├── README.md            ← VOTRE documentation, complétée par une partie « Choix CSS »
├── css/
│   └── style.css        ← UNE seule feuille de style pour les 5 pages
├── pages/
│   ├── fruits.html
│   ├── legumes.html
│   ├── cereales.html
│   └── contact.html
├── images/
└── maquettes/
```

### Charte graphique

| Variable | Couleur | Utilisation |
|---|---|---|
| `--vert-fonce` | `#1b5e20` | titres, fond du menu, pied de page, en-têtes du tableau |
| `--vert` | `#2e7d32` | liens, boutons, survol du menu |
| `--vert-clair` | `#e8f5e9` | fonds légers (une ligne sur deux du tableau) |
| `--soleil` | `#f9a825` | page en cours dans le menu, focus sur fond foncé |
| `--mangue` | `#ef6c00` | traits décoratifs sous les titres (**jamais** pour du texte : contraste trop faible) |
| `--creme` | `#fffaf0` | fond de la page |
| `--blanc` | `#ffffff` | en-tête, fond des cartes, du tableau et du formulaire |
| `--texte` | `#1f2a1f` | texte courant |
| `--bordure` | `#6b7b6b` | bordure des champs du formulaire |

- **Polices** (système, rien à télécharger) : titres en `Georgia, "Times New Roman", serif` ; texte en `system-ui, -apple-system, "Segoe UI", Roboto, Ubuntu, sans-serif`.
- **Formes** : cartes avec des coins arrondis de `0.75rem` et une ombre légère `0 2px 8px rgba(0, 0, 0, 0.12)` ; boutons et liens du menu en « pastilles » (coins arrondis de `2rem`).
- **Largeur** : le contenu ne dépasse pas `70rem` de large et reste centré.

Vous pouvez personnaliser la charte (c'est votre site !), à condition de garder des contrastes d'au moins **4,5:1** pour le texte.

### Exigences visuelles

| N° | Exigence |
|----|----------|
| V1 | **En-tête** identique sur les 5 pages : logo et nom du site alignés côte à côte. |
| V2 | **Menu** horizontal en pastilles, qui passe à la ligne sur téléphone. La page en cours (`aria-current="page"`) est mise en valeur ; le survol est visible. |
| V3 | **Accueil** : photo fluide (jamais déformée), texte de présentation aux lignes courtes, **3 cartes** catégories (image, titre, phrase, bouton) côte à côte sur ordinateur et les unes sous les autres sur téléphone. Les boutons des 3 cartes sont alignés en bas. |
| V4 | **Pages catégories** : produits en **grille** (au moins 2 colonnes sur ordinateur, 1 sur téléphone). Les images dominent : **80 % d'images, 20 % de texte**. Le lien « ↑ Retour au menu » ressemble à un bouton. |
| V5 | **Tableau** lisible : titre (`caption`), en-têtes colorés, bordures fines, une ligne sur deux colorée. |
| V6 | **Formulaire** : labels au-dessus des champs, champs sur toute la largeur et avec la même police que la page, bouton aux couleurs de la charte. |
| V7 | **Pied de page** aux couleurs de la charte sur toutes les pages. |
| V8 | **Interactivité** : survol **et** focus clavier visibles sur tous les liens, boutons et champs ; au moins un effet animé (`transition`), coupé quand l'utilisateur demande moins d'animations (`prefers-reduced-motion`). |

### Exigences techniques

| N° | Exigence |
|----|----------|
| T1 | **Une seule** feuille `css/style.css`, liée aux 5 pages par un `<link>` (attention au `../` depuis `pages/`). Aucun attribut `style`, aucune balise `<style>`. |
| T2 | Les couleurs et les polices de la charte sont des **variables CSS** déclarées dans `:root`. |
| T3 | **Aucun lien externe** : polices système, pas de Google Fonts, pas de bibliothèque CSS. |
| T4 | **Mobile first** : les règles de base visent le téléphone, puis au moins une `@media (min-width: …)` pour les grands écrans. **Aucun défilement horizontal** de 320 px à 1440 px de large. |
| T5 | **Flexbox** pour au moins l'en-tête et le menu ; **Grid** pour au moins une grille (cartes ou produits). |
| T6 | Images fluides (`max-width: 100%` et `height: auto`), jamais déformées. |
| T7 | Accessibilité : contrastes ≥ 4,5:1 (vérifiés avec la pipette de F12), focus jamais supprimé, liens du menu d'au moins 44 px de haut (faciles à toucher), score **Accessibilité ≥ 90** dans Lighthouse. |
| T8 | Code organisé : une section commentée par partie du site (`/* ===== MENU ===== */`), dans l'ordre de la page ; indentation de 2 espaces ; une déclaration par ligne. |
| T9 | Poids : `style.css` pèse **moins de 10 Ko** (sans minification). |
| T10 | **0 erreur** au validateur CSS du W3C, et toujours 0 erreur au validateur HTML. |
| T11 | Le HTML ne change que **pour le CSS** : ajout du `<link>`, de `class` ou d'une `<div>` de regroupement. Chaque ajout est signalé par un commentaire. Le contenu ne change pas. |

## Étapes conseillées

1. **Préparation (15 min)** — Copiez vos fichiers (voir *Prérequis*). Ouvrez la charte et les maquettes. Sur papier, pour chaque bloc de la maquette, notez : le sélecteur que vous utiliserez, et s'il faut **Flexbox** (une ligne) ou **Grid** (une grille). Comparez avec votre HTML : où faut-il ajouter une `class` ou une `<div>` ?
2. **Base commune (25 min)** — Créez `css/style.css` avec le plan de vos sections en commentaires. Écrivez les variables, `box-sizing`, le `body`, les titres, les liens et les images fluides. Liez la feuille aux 5 pages, puis **vérifiez que les 5 pages ont changé** (sinon : chemin du `<link>`).
3. **En-tête, menu et pied de page (30 min)** — Ils sont communs à toutes les pages. Travaillez **d'abord en largeur téléphone** (mode appareil de F12, `Ctrl + Maj + M`, 375 px), puis élargissez.
4. **Accueil (30 min)** — Photo, texte de présentation, grille des 3 cartes, boutons en bas des cartes.
5. **Pages catégories (25 min)** — Grille de produits, tableau, lien « ↑ Retour au menu ».
6. **Contact (15 min)** — Formulaire et adresse.
7. **Grands écrans et interactivité (10 min)** — Media queries, survol, focus, transition, `prefers-reduced-motion`.
8. **Tests (15 min)** — Remplissez la grille ci-dessous, passez le validateur CSS et le validateur HTML, lancez Lighthouse, mesurez le poids de `style.css`.
9. **Régime et documentation (15 min)** — Supprimez les règles inutiles, regroupez les sélecteurs (exercice 11), puis ajoutez la partie « Choix CSS » à votre `README.md`.

### Grille de test

Pour chaque page et chaque largeur (mode appareil de F12), cochez quand : **pas de défilement horizontal**, rien ne se chevauche, aucune image n'est déformée, le menu est utilisable. Dans la colonne « Clavier », parcourez la page avec `Tab` : le focus doit toujours être visible.

| Page ↓ / Largeur → | 375 px | 768 px | 1280 px | Clavier (`Tab`) |
|---|---|---|---|---|
| index.html | ☐ | ☐ | ☐ | ☐ |
| fruits.html | ☐ | ☐ | ☐ | ☐ |
| legumes.html | ☐ | ☐ | ☐ | ☐ |
| cereales.html | ☐ | ☐ | ☐ | ☐ |
| contact.html | ☐ | ☐ | ☐ | ☐ |

Et aussi :

- [ ] Validateur CSS : 0 erreur sur `style.css`.
- [ ] Validateur HTML : 0 erreur sur les 5 pages (vos ajouts de `class` et de `<div>` sont valides).
- [ ] Lighthouse, onglet *Lighthouse* de F12, catégorie *Accessibilité* : score ≥ 90 sur l'accueil.
- [ ] Poids de `style.css` (clic droit → *Propriétés*, ou onglet *Réseau* de F12) : ………… Ko.
- [ ] Tous les liens fonctionnent toujours (menu, cartes, « Retour au menu »).

### Documentation : la partie « Choix CSS »

Ajoutez cette partie à votre `README.md`, juste après « Choix techniques » :

```markdown
## Choix CSS

- Organisation du fichier : (les sections, dans quel ordre)
- Charte graphique : (les variables et leur rôle)
- Mise en page : (où j'ai utilisé Flexbox, où j'ai utilisé Grid, et pourquoi)
- Responsive : (mobile first ? quelles largeurs dans mes media queries, et pourquoi)
- Accessibilité : (contrastes vérifiés, focus, prefers-reduced-motion…)
- Poids : style.css = … Ko
- Modifications du HTML pour le CSS : (les class et div ajoutées)
```

Complétez aussi « Tests réalisés » (validateur CSS, grille de test, Lighthouse) et « Difficultés rencontrées et solutions ».

## Grille d'auto-évaluation (/20)

| Critère | Points | Mon score |
|---|---|---|
| **Maquettes et charte** — le site ressemble aux maquettes : en-tête, menu, cartes, produits, pied de page (2), charte en variables (1) | 3 | |
| **Mise en page** — Flexbox pour l'en-tête et le menu (1), Grid pour une grille (1), images jamais déformées (1) | 3 | |
| **Responsive** — mobile first avec au moins une media query (1), aucun défilement horizontal de 320 à 1440 px (2), menu et formulaire faciles à utiliser au doigt (1) | 4 | |
| **Interactivité et accessibilité** — survol et focus visibles (1), page en cours mise en valeur (1), contrastes ≥ 4,5:1 et Lighthouse ≥ 90 (1), `prefers-reduced-motion` (1) | 4 | |
| **Tableau et formulaire** — tableau lisible (1), formulaire stylé : labels, champs, focus, bouton (1) | 2 | |
| **Qualité du code** — 0 erreur au validateur CSS (1), sections commentées et indentation (1), < 10 Ko et aucun lien externe (1) | 3 | |
| **Documentation** — partie « Choix CSS » complète | 1 | |
| **Total** | **20** | |

## Indices

<details>
<summary>Indice 1 — Une seule feuille de style pour 5 pages dans deux dossiers</summary>

Le chemin du `<link>` part de la page **qui contient le lien**. Depuis `index.html`, le dossier `css/` est juste à côté ; depuis `pages/fruits.html`, il faut d'abord remonter d'un dossier. Pour vérifier en 10 secondes : mettez temporairement un fond rouge vif sur le `body`, et ouvrez les 5 pages. Une page reste blanche ? Son `<link>` est faux. Revoyez l'exercice 01.

</details>

<details>
<summary>Indice 2 — Le nom du site est un <code>&lt;h1&gt;</code> sur l'accueil, mais un <code>&lt;p&gt;</code> ailleurs</summary>

Pas besoin de changer le HTML : un **sélecteur regroupé** applique la même règle aux deux cas. Ciblez « le `h1` qui est dans le `header` » et « le `p` qui est dans le `header` », séparés par une virgule. Revoyez l'exercice 02.

</details>

<details>
<summary>Indice 3 — Mettre en grille des éléments mélangés à d'autres</summary>

- **Les produits** : dans `<main>`, vos `<figure>` sont mélangées avec le `<h1>`, des paragraphes, le tableau… Regroupez-les dans une `<div>` avec une classe (et un commentaire qui explique pourquoi), puis faites de cette `<div>` une grille.
- **Les cartes de l'accueil** : la section contient un `<h2>` puis les 3 cartes. Vous pouvez faire de la section une grille, à condition que le titre occupe **toute la ligne** : cherchez la valeur `1 / -1` de `grid-column`.
- Pour que le nombre de colonnes s'adapte tout seul à la largeur, revoyez `repeat(auto-fill, minmax(…, 1fr))` (exercice 07).

</details>

<details>
<summary>Indice 4 — Les boutons des cartes ne sont pas alignés</summary>

Les phrases des cartes n'ont pas la même longueur, donc les boutons ne tombent pas à la même hauteur. Faites de chaque carte une **colonne flex**, puis donnez au bouton une marge du haut **automatique** : elle prend toute la place libre et pousse le bouton en bas. Revoyez l'exercice 06.

</details>

<details>
<summary>Indice 5 — La photo d'accueil est déformée ou floue</summary>

- **Déformée** : les attributs `width` et `height` de votre `<img>` s'appliquent toujours. Une largeur fluide sans `height: auto` écrase l'image.
- **Bandeau sur grand écran** : `aspect-ratio` donne la forme, `object-fit: cover` recadre au lieu de déformer (exercice 07).
- **Floue** sur grand écran : si votre `<picture>` a un attribut `sizes`, il doit correspondre à la largeur réelle d'affichage, sinon le navigateur choisit la petite version.

</details>

<details>
<summary>Indice 6 — Styler « Retour au menu » sans ajouter de classe</summary>

Un sélecteur d'attribut peut viser les liens selon leur adresse : `a[href$="…"]` signifie « les liens dont le `href` **se termine par** … ». Une classe ajoutée dans le HTML marche aussi : c'est votre choix, mais justifiez-le dans votre documentation.

</details>

<details>
<summary>Indice 7 — Les champs du formulaire ont une autre police</summary>

Les `input`, `select`, `textarea` et `button` n'héritent **pas** de la police de la page par défaut. Une seule déclaration règle le problème : `font: inherit;`.

</details>

<details>
<summary>Indice 8 — Ma feuille dépasse 10 Ko</summary>

Revoyez la partie « Régime minceur » de l'exercice 11 : sélecteurs regroupés pour les règles identiques (par exemple tous vos boutons), propriétés raccourcies (`margin`, `padding`, `border`), suppression des règles qui ne servent à rien (outil *Coverage* de Chrome). Gardez les commentaires utiles : ils comptent dans le poids, mais aussi dans la note « code commenté » !

</details>

## Bonus

- **Mode sombre** : avec `@media (prefers-color-scheme: dark)`, redéfinissez **seulement vos variables** de couleur. Si votre charte est bien en variables, une dizaine de lignes suffit ! Pour tester : F12 → `Ctrl + Maj + P` → tapez « dark » → *Emulate CSS prefers-color-scheme: dark*. Vérifiez les contrastes dans les deux modes.
- **Version minifiée** : créez `css/style.min.css` (outil en ligne de minification ou extension VS Code), comparez les deux poids dans votre README et expliquez quel fichier vous publieriez.
- **`:target`** : quand on clique sur « ↑ Retour au menu », mettez en valeur la section des catégories de l'accueil (exercice 10).
- **GitHub Pages** : publiez le site et testez-le sur un **vrai téléphone**.
- **Oral** : préparez une présentation de 3 minutes sur **un** choix CSS de votre site (par exemple : « comment mon menu s'adapte au téléphone »). C'est un entraînement à la soutenance du brief.

## Questions de compréhension

1. Pourquoi une seule feuille de style pour les 5 pages, plutôt qu'une feuille par page ou du CSS dans chaque page ?
2. Qu'est-ce que l'approche « mobile first » ? Pourquoi écrire les règles du téléphone **avant** celles de l'ordinateur ?
3. Flexbox ou Grid : lequel avez-vous utilisé pour le menu, lequel pour les produits ? Pourquoi ?
4. Comment avez-vous vérifié que votre site est lisible et utilisable au clavier ?
5. Combien pèse votre feuille de style ? Qu'avez-vous fait pour la garder légère ?

## Lien avec le brief PlantEvo

Tout y est : une feuille de style commune à toutes les pages, un menu clair qui signale la page en cours, des pages de détail à 80 % d'images en grille, un lien de retour au menu bien visible, une interface agréable sur téléphone comme sur ordinateur, un code commenté et organisé, un fichier CSS léger sans aucun lien externe, et une documentation technique. Ce sont exactement les critères du brief : « Fonctionnalité et convivialité de l'interface utilisateur », « Créativité dans la conception et l'adaptabilité du site », « Code source correctement commenté et organisé », « Minimiser le nombre de liens externes », « Minimiser la taille du fichier CSS ». Si vous réussissez ce défi, vous savez faire **toute la partie CSS** du brief.

## Ressources

- [Validateur CSS du W3C (saisie directe)](https://jigsaw.w3.org/css-validator/#validate_by_input)
- [Validateur HTML du W3C (saisie directe)](https://validator.w3.org/#validate_by_input)
- [MDN — Flexbox](https://developer.mozilla.org/fr/docs/Learn/CSS/CSS_layout/Flexbox)
- [MDN — Grilles CSS](https://developer.mozilla.org/fr/docs/Learn/CSS/CSS_layout/Grids)
- [MDN — Le responsive design](https://developer.mozilla.org/fr/docs/Learn/CSS/CSS_layout/Responsive_Design)
- [MDN — Les propriétés personnalisées (variables CSS)](https://developer.mozilla.org/fr/docs/Web/CSS/Using_CSS_custom_properties)
- [MDN — Sélecteurs d'attribut](https://developer.mozilla.org/fr/docs/Web/CSS/Attribute_selectors)
- [MDN — `prefers-color-scheme`](https://developer.mozilla.org/fr/docs/Web/CSS/@media/prefers-color-scheme)
- [GitHub Pages — documentation](https://docs.github.com/fr/pages/getting-started-with-github-pages)

---

Bravo, vous avez terminé la série ! Retour au [sommaire des exercices](../../README.md).
