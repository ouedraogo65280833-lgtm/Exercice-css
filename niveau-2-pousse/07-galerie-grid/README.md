# Exercice 07 — Une galerie d'images avec Grid

**Niveau 2 · Pousse** · ★★☆☆ · Durée : 1 h · Notions : `display: grid`, `grid-template-columns`, unité `fr`, `repeat()`, `gap`, `auto-fill` + `minmax()`, `grid-column`, `grid-row: span 2`, `aspect-ratio`, `object-fit`, inspecteur de grille

> Le grand marché veut une galerie de photos pour son site : douze images, prises par différents producteurs… et donc toutes de tailles et de formes différentes. Une image très large, une en hauteur, une carrée, des paysages. Votre mission : les ranger dans une grille régulière, qui s'adapte toute seule à la largeur de l'écran, sans déformer aucune image.

## Objectifs

- Créer une grille avec `display: grid` et définir ses colonnes avec `grid-template-columns`.
- Comprendre l'unité `fr` (« une part de l'espace restant ») et la fonction `repeat()`.
- Construire une grille **responsive sans media query** avec `repeat(auto-fill, minmax(…))`.
- Obtenir des vignettes de même forme avec `aspect-ratio` et `object-fit: cover`.
- Faire occuper plusieurs cases à un élément (`grid-column`, `grid-row`).

## Fichiers fournis

```
07-galerie-grid/
├── README.md         ← cette consigne
├── index.html        ← la page complète : 12 <figure> dans un <div class="galerie">
├── css/
│   └── style.css     ← la base est faite ; vous complétez la partie GALERIE
└── images/
    ├── etal-du-marche.svg     ← panoramique (960 × 360)
    ├── ananas.svg             ← en hauteur (300 × 450)
    ├── panier-de-fruits.svg   ← carrée (400 × 400)
    ├── parcelle-800.webp      ← photo (800 × 533)
    └── mangue.svg  tomate.svg  piment.svg  banane.svg  cacao.svg  mais.svg  riz.svg  poule.svg  (400 × 300)
```

## Consigne

**Étape 0 — Observer (5 min).** Ouvrez `index.html` avec Live Server. Les figures sont empilées et les images ont toutes des formes différentes. Dans le HTML, repérez le conteneur `.galerie`, la figure `.panorama` (la première) et la figure `.haute` (l'ananas).

Complétez ensuite la partie « GALERIE » de `css/style.css` (les numéros correspondent aux `TODO`) :

1. **Une première grille.** Dans `.galerie`, écrivez :
   ```css
   display: grid;
   grid-template-columns: 1fr 1fr 1fr;
   gap: 1rem;
   ```
   Les figures se rangent sur 3 colonnes. Ouvrez les outils de développement (`F12`), onglet *Éléments* : à côté de `<div class="galerie">`, cliquez sur le petit badge **`grid`**. La grille s'affiche par-dessus la page, avec le **numéro de chaque ligne** de grille. Gardez-la affichée pour la suite.

   Essayez ensuite, l'une après l'autre, ces valeurs de `grid-template-columns` et observez :
   - `repeat(3, 1fr)` (même résultat, en plus court) ;
   - `repeat(4, 1fr)` ;
   - `200px 1fr 1fr` (la première colonne est fixe, les deux autres se partagent le reste) ;
   - `2fr 1fr 1fr` (la première colonne reçoit deux parts, les autres une part chacune).
2. **Une grille qui s'adapte toute seule.** Remplacez la valeur par :
   ```css
   grid-template-columns: repeat(auto-fill, minmax(12rem, 1fr));
   ```
   Lisez-la ainsi : « crée **autant de colonnes que possible** (`auto-fill`), chacune d'**au moins 12rem** et **au plus une part** de l'espace restant ». Rétrécissez lentement la fenêtre : 4 colonnes, puis 3, puis 2, puis 1. Vous venez de faire une galerie responsive **sans aucune media query**.
3. **Des vignettes de même forme.** Les rangées sont irrégulières, car les images n'ont pas les mêmes proportions. Dans `.galerie img`, ajoutez `width: 100%` et `aspect-ratio: 4 / 3`. Toutes les images ont maintenant la même forme… mais regardez l'ananas, le panier et la photo des champs : ils sont **déformés** (écrasés ou étirés). Les illustrations de 400 × 300, elles, ne bougent pas : elles sont déjà au format 4/3.
4. **Recadrer sans déformer.** Toujours dans `.galerie img`, ajoutez `object-fit: cover`. L'image remplit sa case **en gardant ses proportions** : ce qui dépasse est coupé. Essayez aussi `contain` et `fill` pour comparer, puis revenez à `cover`.
5. **Habiller les vignettes.** Dans `.galerie figure` :
   - `margin: 0` (un `<figure>` a par défaut une marge de 40px à gauche et à droite : vérifiez-le dans l'inspecteur, panneau *Calculé*, avant de la supprimer) ;
   - un fond blanc, des coins arrondis (`border-radius: 0.75rem`), une ombre (`box-shadow: var(--ombre)`) ;
   - `overflow: hidden` : l'image ne dépasse plus des coins arrondis.

   Dans `.galerie figcaption`, ajoutez un `padding` (par exemple `0.5rem 0.75rem`).
6. **Le panorama sur toute la largeur.** Créez une règle `.panorama` avec `grid-column: 1 / -1;`. Cela signifie : « de la **ligne de grille 1** à la **dernière ligne** » (`-1` compte depuis la fin). Regardez les numéros des lignes dans l'inspecteur de grille pour comprendre. Puis, pour ne pas couper ce paysage, créez la règle `.panorama img` avec `aspect-ratio: 8 / 3` (les vraies proportions de l'image : 960 × 360).
   > ⚠️ `.panorama img` et `.galerie img` ont la **même spécificité** (une classe + une balise) : c'est donc la règle écrite **en dernier** qui gagne (exercice 02). Écrivez bien vos nouvelles règles **après** `.galerie img`, comme le prévoit le fichier.
7. **L'ananas sur deux rangées.** Créez une règle `.haute` avec `grid-row: span 2;` : la figure s'étend sur deux rangées. La case est plus haute… mais l'image, elle, a gardé sa forme 4/3 et laisse un grand vide. Pour qu'elle remplisse toute la hauteur :
   - dans `.haute`, ajoutez `display: flex` et `flex-direction: column` (eh oui, on peut mettre Flexbox **dans** une case de Grid !) ;
   - créez une règle `.haute img` avec `flex: 1` (l'image prend toute la place libre) et `aspect-ratio: auto` (on annule le 4/3).
8. **Tester (5 min).** En mode appareil (`Ctrl + Maj + M`), testez 375 px, 768 px et 1280 px. Les rangées doivent être régulières, rien ne doit être déformé, aucun défilement horizontal.

### Mémo Grid

| Propriété | Sur | Rôle | Exemple |
|---|---|---|---|
| `display: grid` | parent | Les enfants directs se rangent dans une grille | — |
| `grid-template-columns` | parent | Nombre et largeur des colonnes | `1fr 1fr 1fr`, `200px 1fr` |
| `fr` | — | Une **part** de l'espace restant | `2fr 1fr` = deux tiers / un tiers |
| `repeat(n, taille)` | — | Répète une taille `n` fois | `repeat(4, 1fr)` |
| `minmax(min, max)` | — | Taille comprise entre un minimum et un maximum | `minmax(12rem, 1fr)` |
| `auto-fill` | — | « Autant de colonnes que possible » | `repeat(auto-fill, minmax(12rem, 1fr))` |
| `gap` | parent | Espace entre les cases | `1rem` |
| `grid-column` | enfant | Colonnes occupées : `début / fin` ou `span n` | `1 / -1`, `span 2` |
| `grid-row` | enfant | Rangées occupées | `span 2` |

| Propriété (sur l'image) | Rôle |
|---|---|
| `aspect-ratio: 4 / 3` | Impose une forme (largeur / hauteur) |
| `object-fit: fill` | Valeur par défaut : l'image est **déformée** pour remplir la case |
| `object-fit: cover` | L'image **remplit** la case sans être déformée ; le surplus est coupé |
| `object-fit: contain` | L'image est **entièrement visible** sans être déformée ; il peut rester des bandes vides |

```
lignes de grille :  1         2         3         4         5   (-1)
                    ┌─────────┬─────────┬─────────┬─────────┐
                    │          .panorama  (1 / -1)          │
                    ├─────────┬─────────┬─────────┬─────────┤
                    │ panier  │ ananas  │  photo  │ mangue  │
                    ├─────────┤ (span 2)├─────────┼─────────┤
                    │ tomate  │         │ piment  │ banane  │
                    └─────────┴─────────┴─────────┴─────────┘
```

## Critères de réussite

- [ ] La galerie est une grille dont le nombre de colonnes s'adapte à la largeur de l'écran (4 sur ordinateur, 1 sur téléphone).
- [ ] Je n'ai écrit **aucune** media query.
- [ ] Toutes les vignettes ont la même forme et **aucune image n'est déformée**.
- [ ] L'image panoramique occupe toute la largeur de la galerie et n'est pas recadrée.
- [ ] L'ananas occupe deux rangées et son image remplit toute la hauteur de sa case.
- [ ] Les figures n'ont plus leur marge par défaut ; elles ont un fond, des coins arrondis et une ombre.
- [ ] À 375 px, pas de défilement horizontal.
- [ ] Le validateur CSS du W3C n'affiche aucune erreur.

## Indices

<details>
<summary>Indice 1 — Je ne trouve pas le badge <code>grid</code> dans l'inspecteur</summary>

Il n'apparaît que si `display: grid` est **vraiment appliqué**. Vérifiez dans le panneau *Styles* que la déclaration n'est pas barrée, et que le sélecteur `.galerie` correspond bien à la classe du HTML. Dans Firefox, l'équivalent est le petit pictogramme de grille à côté de `display: grid` dans le panneau *Règles*.

</details>

<details>
<summary>Indice 2 — Quelle différence entre <code>1fr</code> et <code>33%</code> ?</summary>

Avec `33% 33% 33%`, il faut ajouter les `gap` : la grille devient plus large que son conteneur et déborde. Avec `1fr 1fr 1fr`, le navigateur retire d'abord les espaces, **puis** partage ce qui reste en parts égales. C'est pour cela qu'on utilise `fr` dans les grilles.

</details>

<details>
<summary>Indice 3 — Mon <code>object-fit: cover</code> ne fait rien</summary>

`object-fit` n'a d'effet que si la case de l'image a une forme **différente** de celle de l'image. Sans `aspect-ratio` (ou sans hauteur imposée), la case prend exactement la forme de l'image : il n'y a rien à recadrer.

</details>

<details>
<summary>Indice 4 — Pourquoi <code>1 / -1</code> plutôt que <code>span 4</code> pour le panorama ?</summary>

Le nombre de colonnes change selon l'écran ! Sur un téléphone, il n'y a qu'**une** colonne : un élément en `span 4` obligerait le navigateur à créer des colonnes supplémentaires… et la page déborderait. `1 / -1` signifie toujours « toute la largeur », quel que soit le nombre de colonnes.

</details>

## Bonus

- **Légende en surimpression** : placez la légende **sur** l'image, en bas, sur un bandeau sombre semi-transparent. Pistes : `position: relative` sur la figure, `position: absolute; bottom: 0; left: 0; right: 0;` sur la légende, et `background-color: rgba(0, 0, 0, 0.6)`.
- Ajoutez la classe `vedette` au panier et donnez-lui `grid-column: span 2; grid-row: span 2;`. Que se passe-t-il à 375 px ? (Revoyez l'indice 4.) Des « trous » apparaissent-ils dans la grille sur grand écran ? Essayez `grid-auto-flow: dense` sur `.galerie`.
- Testez `object-position: top` sur l'image du panier : quelle partie de l'image est gardée ?
- Jouez à **[Grid Garden](https://cssgridgarden.com/#fr)** (en français) : 28 niveaux pour arroser votre potager avec CSS Grid.

## Questions de compréhension

1. Que signifie l'unité `fr` ? Pourquoi est-elle plus pratique que des pourcentages dans une grille ?
2. Expliquez avec vos mots `repeat(auto-fill, minmax(12rem, 1fr))`.
3. Quelle est la différence entre `object-fit: cover` et `object-fit: contain` ? Dans quel cas préférer l'un ou l'autre ?
4. Que veut dire `grid-column: 1 / -1` ? Et `grid-row: span 2` ?
5. Flexbox ou Grid : lequel avez-vous utilisé pour la galerie, lequel pour l'ananas ? Pourquoi ?

## Lien avec le brief PlantEvo

Le brief impose que chaque partie consacrée à un type de végétal contienne « **80 % d'images et 20 % de texte** ». Une galerie en grille est la façon la plus efficace de présenter beaucoup d'images de façon claire et régulière, même si vos photos n'ont pas toutes le même format (`object-fit` fait le travail). Et comme elle s'adapte toute seule à la largeur de l'écran, votre page reste lisible sur le téléphone des visiteurs du stand.

## Ressources

- [MDN — Les grilles CSS (apprendre)](https://developer.mozilla.org/fr/docs/Learn/CSS/CSS_layout/Grids)
- MDN : [`grid-template-columns`](https://developer.mozilla.org/fr/docs/Web/CSS/grid-template-columns) · [`repeat()`](https://developer.mozilla.org/fr/docs/Web/CSS/repeat) · [`minmax()`](https://developer.mozilla.org/fr/docs/Web/CSS/minmax) · [`grid-column`](https://developer.mozilla.org/fr/docs/Web/CSS/grid-column)
- MDN : [`object-fit`](https://developer.mozilla.org/fr/docs/Web/CSS/object-fit) · [`aspect-ratio`](https://developer.mozilla.org/fr/docs/Web/CSS/aspect-ratio)
- [Grid Garden](https://cssgridgarden.com/#fr)
- [Validateur CSS du W3C](https://jigsaw.w3.org/css-validator/#validate_by_input)

---

Exercice suivant : [08 — Mettre en page un site entier avec Grid](../08-mise-en-page-grid/README.md)
