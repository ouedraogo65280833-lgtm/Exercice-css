# Exercice 05 — Un menu avec Flexbox

**Niveau 2 · Pousse** · ★★☆☆ · Durée : 45 min · Notions : `display: flex`, axe principal / secondaire, `justify-content`, `align-items`, `gap`, `flex-wrap`, `flex-direction`, `list-style`, `:hover`, `:focus-visible`, `[aria-current="page"]`

> La ferme pédagogique a un petit site de 4 pages. Le contenu est prêt, mais l'en-tête ressemble à une liste de courses : un logo, un nom, puis quatre liens soulignés empilés les uns sous les autres. Votre mission : transformer cette liste en une vraie barre de navigation, avec le logo à gauche et le menu à droite.

## Objectifs

- Comprendre ce que fait `display: flex` sur un conteneur et sur ses enfants.
- Distinguer l'**axe principal** (où se rangent les éléments) et l'**axe secondaire** (perpendiculaire).
- Répartir et aligner des éléments avec `justify-content`, `align-items` et `gap`.
- Transformer une liste `<ul>` en menu horizontal, avec des états de survol, de focus et de « page en cours ».

## Fichiers fournis

```
05-menu-flexbox/
├── README.md        ← cette consigne
├── index.html       ← accueil (aria-current déjà en place : c'est le modèle)
├── animaux.html     ← 3 autres pages qui partagent le même en-tête
├── potager.html
├── infos.html
├── css/
│   └── style.css    ← la base est faite ; vous complétez les TODO
└── images/
    ├── logo.svg
    ├── poule.svg
    └── carotte.svg
```

Le HTML des quatre pages est **déjà écrit et déjà relié** à `css/style.css`. Vous ne touchez au HTML qu'à l'étape 7.

## Consigne

**Étape 0 — Observer (5 min).** Ouvrez `index.html` avec Live Server, puis ouvrez `css/style.css` dans VS Code. Repérez dans le HTML les trois boîtes qui nous intéressent : l'en-tête `.entete`, le lien `.logo` (image + nom) et la liste `.menu`. Dessinez sur papier, en trois rectangles, la barre que vous voulez obtenir :

```
┌──────────────────────────────────────────────────────────────────────┐
│ (logo) La ferme pédagogique      Accueil  Les animaux  Le potager  … │
└──────────────────────────────────────────────────────────────────────┘
```

Ensuite, complétez `css/style.css` (les numéros correspondent aux commentaires `TODO` du fichier) et rechargez la page après chaque étape :

1. **Une liste propre.** Dans `.menu`, retirez les puces (`list-style: none`), la marge (`margin: 0`) et le retrait à gauche (`padding: 0`). C'est la première chose à faire pour **tout** menu.
2. **Le menu à l'horizontale.** Toujours dans `.menu`, ajoutez `display: flex;`. Les `<li>`, qui sont les **enfants directs** de la liste, se rangent côte à côte. Ajoutez un espace entre eux avec `gap: 0.5rem;`.
3. **Des liens-boutons.** Dans `.menu a` : `display: block`, un `padding` (par exemple `0.5rem 1rem`), des coins arrondis (`border-radius`), du gras, la couleur `var(--vert-fonce)` et **pas** de soulignement (`text-decoration: none`).
4. **Le logo.** Dans `.logo`, placez l'image et le nom côte à côte avec `display: flex`, centrez-les verticalement avec `align-items: center` et espacez-les avec `gap`.
5. **L'en-tête.** Dans `.entete`, ajoutez `display: flex`. Ses deux enfants (le lien `.logo` et le `<nav>`) se mettent côte à côte. Poussez le logo à gauche et le menu à droite avec `justify-content: space-between`, puis centrez-les verticalement avec `align-items: center`.
6. **Survol et focus.** Ajoutez une règle `.menu a:hover` (fond `var(--vert-clair)`) et une règle `.menu a:focus-visible` avec un contour bien visible, par exemple `outline: 3px solid var(--vert-fonce);` et `outline-offset: 2px;` (le contour se décale de 2 px autour du lien). Testez au clavier : cliquez dans la barre d'adresse, puis appuyez plusieurs fois sur `Tab`.
7. **La page en cours.** Dans `index.html`, le lien « Accueil » porte l'attribut `aria-current="page"` : il dit aux lecteurs d'écran « vous êtes ici ».
   - Dans `animaux.html`, `potager.html` et `infos.html`, ajoutez `aria-current="page"` sur le **bon** lien (voir le `TODO 7` de chaque page).
   - Dans le CSS, ciblez ce lien avec le sélecteur d'attribut `.menu a[aria-current="page"]` : fond `var(--vert)`, texte blanc.
   - Naviguez entre les 4 pages : le bouton coloré doit suivre la page affichée.
8. **Écran étroit.** Rétrécissez la fenêtre du navigateur (ou passez en mode appareil avec `Ctrl + Maj + M`, largeur 375 px) : le menu déborde ou s'écrase. Ajoutez `flex-wrap: wrap;` dans `.entete` **et** dans `.menu`, plus un `gap` dans `.entete`. Rétrécissez à nouveau : les éléments passent à la ligne au lieu de déborder.
9. **Laboratoire (5 min).** Ouvrez les outils de développement (`F12`), sélectionnez l'élément `<header class="entete">`. Dans le panneau *Styles*, une petite icône apparaît à côté de `display: flex` : c'est l'**éditeur Flexbox**. Cliquez dessus et essayez une à une toutes les valeurs de `justify-content` (`flex-start`, `center`, `flex-end`, `space-between`, `space-around`, `space-evenly`), puis `flex-direction: column`. Notez dans un coin de votre feuille ce que fait chaque valeur. (Ces essais ne modifient pas votre fichier : rechargez pour revenir à votre version.)

### Mémo Flexbox (propriétés du conteneur)

```
           axe principal (flex-direction: row) ──────────────►
         ┌──────────────────────────────────────────────────┐
  axe    │  ┌────────┐  ┌────────┐  ┌────────┐              │
  secon- │  │ enfant │  │ enfant │  │ enfant │   parent :   │
  daire  │  └────────┘  └────────┘  └────────┘ display:flex │
    │    └──────────────────────────────────────────────────┘
    ▼
  justify-content : répartit les enfants sur l'axe principal (→)
  align-items     : aligne les enfants sur l'axe secondaire (↓)
```

| Propriété (sur le **parent**) | Rôle | Valeurs utiles |
|---|---|---|
| `display: flex` | Les **enfants directs** deviennent des éléments flexibles, rangés sur une ligne | — |
| `flex-direction` | Sens de l'axe principal | `row` (par défaut), `column` |
| `justify-content` | Répartition sur l'axe **principal** | `flex-start`, `center`, `flex-end`, `space-between`, `space-around`, `space-evenly` |
| `align-items` | Alignement sur l'axe **secondaire** | `stretch` (par défaut), `flex-start`, `center`, `flex-end` |
| `gap` | Espace **entre** les enfants (pas sur les bords) | `0.5rem`, `1rem 2rem`… |
| `flex-wrap` | Passage à la ligne quand il n'y a plus de place | `nowrap` (par défaut), `wrap` |

| Sélecteur | Cible |
|---|---|
| `.menu a:hover` | un lien du menu **survolé** à la souris |
| `.menu a:focus-visible` | un lien du menu qui a le **focus clavier** |
| `.menu a[aria-current="page"]` | le lien du menu qui **possède l'attribut** `aria-current` avec la valeur `page` |

## Critères de réussite

- [ ] Le menu n'a plus de puces et ses liens sont alignés horizontalement, espacés régulièrement.
- [ ] Le logo et le nom du site sont côte à côte et centrés verticalement.
- [ ] Sur un grand écran, le logo est à gauche et le menu à droite, alignés sur la même ligne.
- [ ] Les liens ne sont plus soulignés, ont un fond au survol et un contour bien visible au clavier (`Tab`).
- [ ] Sur chacune des 4 pages, le lien de la page en cours est mis en valeur (et **un seul**).
- [ ] À 375 px de large, rien ne déborde : le menu passe sous le logo et les liens passent à la ligne.
- [ ] Je n'ai utilisé **aucune** marge ni `float` pour placer les éléments : uniquement Flexbox.
- [ ] Le validateur CSS du W3C n'affiche aucune erreur.

## Indices

<details>
<summary>Indice 1 — J'ai mis <code>display: flex</code> sur les liens, et rien ne bouge</summary>

`display: flex` agit sur les **enfants directs** de l'élément qui le reçoit. Pour mettre les liens côte à côte, il faut viser leur parent commun. Regardez le HTML : les `<a>` sont chacun dans un `<li>`, et les `<li>` sont tous dans… ?

</details>

<details>
<summary>Indice 2 — <code>justify-content: space-between</code> ne fait rien sur l'en-tête</summary>

Vérifiez que `display: flex` est bien **dans la même règle** (`.entete`). Sans lui, `justify-content` est ignoré : dans les outils de développement, la déclaration apparaît alors en gris avec une petite icône d'information.

</details>

<details>
<summary>Indice 3 — Pourquoi <code>display: block</code> sur les liens ?</summary>

Un lien est un élément **en ligne** (`inline`). Mettez-lui un `padding` sans `display: block` et observez avec l'inspecteur : la zone colorée déborde de la ligne au lieu de pousser le reste. En `block` (ou `inline-block`), le lien devient une vraie boîte : toute la surface colorée est cliquable. Souvenez-vous de l'exercice 04.

</details>

<details>
<summary>Indice 4 — Écrire un sélecteur d'attribut</summary>

Entre crochets, on écrit le nom de l'attribut, et éventuellement sa valeur entre guillemets :

```css
img[alt=""] {
  /* toutes les images dont l'attribut alt est vide */
}
```

</details>

## Bonus

- Jouez à **[Flexbox Froggy](https://flexboxfroggy.com/#fr)** (en français) : 24 niveaux pour maîtriser `justify-content`, `align-items`, `flex-direction`… en aidant des grenouilles à rejoindre leur nénuphar.
- Ajoutez un léger soulignement coloré sous le lien de la page en cours, en plus du fond (`border-bottom` ou `text-decoration-color`).
- Créez une 5e page `contact.html` et ajoutez-la au menu des 5 pages. Combien de fichiers avez-vous dû modifier ? Combien de lignes de CSS ? (Réponse attendue : aucune ligne de CSS, grâce à la feuille de style commune.)

## Questions de compréhension

1. Sur quel élément faut-il écrire `display: flex` : le parent ou les enfants ? Pourquoi ?
2. Quelle est la différence entre `justify-content` et `align-items` ? Que se passe-t-il si on ajoute `flex-direction: column` ?
3. Pourquoi ne faut-il **jamais** supprimer le contour de focus (`outline: none`) sans le remplacer par autre chose ?
4. À quoi sert l'attribut `aria-current="page"` pour un visiteur aveugle ? Et pourquoi est-ce pratique de s'en servir aussi comme sélecteur CSS ?

## Lien avec le brief PlantEvo

Le brief exige « un **menu statique** avec des liens hypertexte permettant de se déplacer vers les informations sur les différents types de végétaux ». Avec cette technique, votre menu PlantEvo devient une vraie barre de navigation : horizontale sur ordinateur, qui passe à la ligne sur téléphone, et qui montre au visiteur où il se trouve. Le jury testera aussi la **convivialité** : survol, focus clavier et page en cours en font partie.

## Ressources

- [MDN — Les bases de Flexbox](https://developer.mozilla.org/fr/docs/Learn/CSS/CSS_layout/Flexbox)
- MDN : [`justify-content`](https://developer.mozilla.org/fr/docs/Web/CSS/justify-content) · [`align-items`](https://developer.mozilla.org/fr/docs/Web/CSS/align-items) · [`gap`](https://developer.mozilla.org/fr/docs/Web/CSS/gap) · [`flex-wrap`](https://developer.mozilla.org/fr/docs/Web/CSS/flex-wrap)
- [MDN — Sélecteurs d'attribut](https://developer.mozilla.org/fr/docs/Web/CSS/Attribute_selectors)
- [MDN — `:focus-visible`](https://developer.mozilla.org/fr/docs/Web/CSS/:focus-visible)
- [Flexbox Froggy](https://flexboxfroggy.com/#fr)
- [Validateur CSS du W3C](https://jigsaw.w3.org/css-validator/#validate_by_input) · [Validateur HTML du W3C](https://validator.w3.org/#validate_by_input)

---

Exercice suivant : [06 — Cartes et bannière avec Flexbox](../06-cartes-flexbox/README.md)
