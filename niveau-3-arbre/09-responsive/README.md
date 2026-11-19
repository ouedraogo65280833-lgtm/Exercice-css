# Exercice 09 — Responsive : du téléphone à l'ordinateur

**Niveau 3 · Arbre** · ★★★☆ · Durée : 1 h · Notions : `meta viewport`, mode appareil de F12, *mobile first*, `@media (min-width: …)`, largeurs fluides (`max-width`, `%`), images fluides, unités relatives (`rem`), cibles tactiles

> Le site du « Marché du samedi » est superbe… sur l'ordinateur du développeur. Mais le samedi matin, les visiteurs le consultent **sur leur téléphone**, entre deux stands : le texte est minuscule, le menu est caché hors de l'écran, il faut faire défiler la page sur le côté pour lire les cartes. Votre mission : rendre le site agréable sur **toutes** les tailles d'écran.

## Objectifs

- Tester une page à différentes largeurs avec le **mode appareil** des outils de développement.
- Repérer ce qui empêche une page de s'adapter (largeurs fixes, images trop grandes, textes en `px`…).
- Écrire une feuille de style **mobile first** : d'abord le téléphone, puis on ajoute ce qui change pour les grands écrans.
- Écrire des **media queries** `@media (min-width: …)` et choisir ses points de rupture (*breakpoints*).

## Fichiers fournis

```
09-responsive/
├── README.md          ← cette consigne
├── index.html         ← la page (déjà complète : vous ne touchez qu'au CSS, sauf à l'étape 9)
├── css/
│   └── style.css      ← la feuille de style « ordinateur seulement » à rendre responsive
└── images/            ← logo, photo de la parcelle (WebP + JPG), 6 illustrations SVG
```

## Consigne

**Étape 0 — Diagnostic (10 min).** Ouvrez `index.html` avec Live Server. Sur ordinateur, tout va bien. Maintenant :

1. ouvrez les outils de développement (**F12**) ;
2. activez le **mode appareil** : icône téléphone/tablette en haut à gauche des outils, ou `Ctrl + Maj + M` (`Cmd + Maj + M` sur Mac) ;
3. en haut de la page, choisissez **Dimensions : Responsive** et tapez la largeur **375** (un téléphone courant) ;
4. faites défiler la page dans tous les sens.

Notez **au moins 5 problèmes**, puis cherchez dans `css/style.css` la règle responsable de chacun :

| Ce que je vois à 375 px | La règle CSS responsable (sélecteur + propriété) |
|---|---|
| | |
| | |
| | |
| | |
| | |

Corrigez ensuite `css/style.css` en suivant les étapes (les numéros correspondent aux commentaires `TODO` du fichier). Gardez le mode appareil ouvert pendant tout l'exercice : vous travaillez **d'abord pour le téléphone**.

1. **La largeur de la page.** Le `body` mesure toujours exactement 1100 px, même sur un écran de 375 px. Remplacez `width` par `max-width` : « au maximum 1100 px, mais moins si l'écran est plus petit ». Ajoutez un `padding` de `1rem` à gauche et à droite pour que le texte ne colle pas aux bords de l'écran.
2. **Les images fluides.** Écrivez une règle pour **toutes** les images de la page : elles ne doivent jamais dépasser la largeur de leur conteneur (`max-width: 100%`) et leur hauteur doit suivre automatiquement (`height: auto`) pour ne pas être déformées. Ajoutez `display: block` (cela supprime le petit espace sous les images). Supprimez ensuite les largeurs et hauteurs fixes de `.accueil img` et `.carte img`. Pour que l'illustration remplisse toujours toute la largeur de sa carte, donnez à `.carte img` une largeur de `100%`.
3. **Les tailles de texte.** `14px` et `12px` sont trop petits sur un téléphone. Supprimez le `font-size` du `body` (la taille par défaut du navigateur est 16 px = `1rem`) et celui de `.menu a`. Convertissez les tailles restantes en `rem` (rappel : `1rem` = 16 px, donc 28 px = `1.75rem`, 20 px = `1.25rem`…). Faites de même pour les marges en `px` des titres si vous le souhaitez.
4. **L'en-tête et le menu, version téléphone.**
   - L'en-tête reste en `flex`, mais avec `flex-wrap: wrap` : le menu a le droit de passer **sous** le logo.
   - Donnez au `nav` de l'en-tête une largeur de `100%` pour qu'il prenne toute la ligne.
   - Le menu devient une **grille de 2 colonnes** (2 × 2 boutons). Supprimez le `white-space: nowrap`.
   - Les liens deviennent de **gros boutons faciles à toucher** : au moins **44 px de haut** (un `padding` de `0.75rem` en haut et en bas suffit), texte centré.
5. **Tout sur une seule colonne.** Sur un téléphone, les blocs s'empilent :
   - `.accueil` : supprimez le `display: flex` (et ce qui va avec) : la photo et le texte s'empilent d'eux-mêmes ;
   - `.cartes` et `.infos` : gardez `display: grid` et le `gap`, mais **supprimez** `grid-template-columns` : une grille sans colonnes définies affiche ses éléments sur **une seule colonne** ;
   - le pied de page : sur téléphone, deux lignes centrées l'une sous l'autre (supprimez son `display: flex`).

   Vérifiez à 375 px : plus de défilement horizontal ! Regardez maintenant la page en grand écran (désactivez le mode appareil)… tout est sur une colonne. **C'est normal** : vous venez d'écrire la version téléphone. Il reste à dire ce qui change sur les écrans plus larges.
6. **Tablette (≥ 600 px).** À la fin du fichier, écrivez une media query `@media (min-width: 600px) { … }`. À l'intérieur :
   - les cartes passent sur **2 colonnes** ;
   - les 3 blocs d'infos pratiques se placent **côte à côte** ;
   - le pied de page repasse en `flex` (contact à gauche, copyright à droite).
7. **Ordinateur (≥ 900 px).** Écrivez une deuxième media query `@media (min-width: 900px) { … }`, **après** la première. À l'intérieur :
   - l'en-tête tient sur **une seule ligne** : logo à gauche, menu à droite (`flex-wrap: nowrap`, `justify-content: space-between`, et le `nav` reprend une largeur automatique) ;
   - le menu repasse en `flex` (une ligne de boutons arrondis) ;
   - l'accueil affiche la photo et le texte **côte à côte** (une grille de 2 colonnes, par exemple `3fr 2fr`) ;
   - les cartes passent sur **3 colonnes** ;
   - le titre `h1` peut grandir un peu.
8. **Testez à toutes les largeurs.** Dans le mode appareil, essayez chaque largeur du tableau ci-dessous. Pour chacune, vérifiez : pas de défilement horizontal, texte lisible sans zoomer, boutons faciles à toucher, rien de coupé.

   | Largeur | Exemple d'appareil | Nombre de colonnes de cartes | Défilement horizontal ? | OK ? |
   |---|---|---|---|---|
   | 320 px | petit téléphone | | | ☐ |
   | 375 px | téléphone courant | | | ☐ |
   | 600 px | grand téléphone couché / petite tablette | | | ☐ |
   | 768 px | tablette | | | ☐ |
   | 900 px | petit ordinateur portable | | | ☐ |
   | 1280 px | ordinateur | | | ☐ |

   Astuce : avec **Dimensions : Responsive**, vous pouvez aussi **tirer le bord droit** de la page pour la rétrécir doucement et voir le moment exact où la mise en page change.
9. **Expérience : le `meta viewport`.** Dans `index.html`, supprimez (ou mettez en commentaire) la ligne `<meta name="viewport" …>`, enregistrez et rechargez en mode appareil à 375 px. Que se passe-t-il ? Le téléphone fait comme si son écran mesurait environ 980 px, puis il **dézoome** : tout devient minuscule et vos media queries ne servent plus à rien. **Remettez la ligne.**
10. **Validez** votre CSS avec le [validateur CSS du W3C](https://jigsaw.w3.org/css-validator/#validate_by_input) (copiez-collez tout le fichier) : objectif **0 erreur**.

### Mémo — le responsive en 5 règles

| Règle | En CSS | Pourquoi |
|---|---|---|
| Le téléphone utilise sa vraie largeur | `<meta name="viewport" content="width=device-width, initial-scale=1.0">` dans le `<head>` | Sans elle, le téléphone simule un écran de 980 px et dézoome. |
| Pas de largeur fixe pour les grands blocs | `max-width: 1100px;` plutôt que `width: 1100px;` | « Au maximum », pas « exactement ». |
| Images fluides | `img { max-width: 100%; height: auto; }` | L'image rétrécit avec son conteneur sans se déformer. |
| Tailles relatives | `rem`, `%`, `fr` plutôt que `px` | Elles s'adaptent à l'écran et aux réglages de l'utilisateur. |
| Mobile first | règles de base = téléphone, puis `@media (min-width: …)` | On **ajoute** des colonnes quand il y a de la place. |

**Anatomie d'une media query** (exemple sur une autre page) :

```css
/* Base : téléphone — pas de media query */
.galerie {
  display: grid;
  gap: 1rem;
}

/* « Si l'écran mesure AU MOINS 700 px de large, alors… » */
@media (min-width: 700px) {
  .galerie {
    grid-template-columns: repeat(4, 1fr);
  }
}
```

À l'intérieur des accolades de `@media`, on écrit des règles CSS **normales**, avec leurs propres accolades. On n'y met **que ce qui change** : tout le reste est hérité des règles de base.

## Critères de réussite

- [ ] Mon tableau de diagnostic contient au moins 5 problèmes avec la règle CSS responsable.
- [ ] À 320 px et à 375 px, il n'y a **aucun défilement horizontal** et rien n'est coupé.
- [ ] Il ne reste aucune largeur fixe en `px` sur le `body`, les images ou les colonnes (les `px` restants concernent seulement les bordures, les ombres, les arrondis et les media queries).
- [ ] Les images s'adaptent à la largeur de l'écran sans être déformées.
- [ ] Sur téléphone : une seule colonne, menu en 2 × 2 avec des boutons d'au moins 44 px de haut.
- [ ] À partir de 600 px : cartes sur 2 colonnes, infos pratiques côte à côte.
- [ ] À partir de 900 px : en-tête sur une ligne, accueil en 2 colonnes, cartes sur 3 colonnes.
- [ ] Les media queries sont à la **fin** du fichier, dans l'ordre 600 px puis 900 px.
- [ ] Le validateur CSS du W3C n'affiche aucune erreur.

## Indices

<details>
<summary>Indice 1 — Comment trouver l'élément qui déborde ?</summary>

Ajoutez **temporairement** cette règle au début de votre CSS :

```css
* {
  outline: 1px solid red;
}
```

Chaque élément est entouré d'un trait rouge (`outline` ne change pas la taille des boîtes, contrairement à `border`). Repérez le bloc qui dépasse à droite de l'écran, puis cliquez dessus avec l'inspecteur (**F12 → Éléments**) pour voir sa largeur dans le panneau *Calculé*. Pensez à supprimer cette règle ensuite !

</details>

<details>
<summary>Indice 2 — <code>width</code> ou <code>max-width</code> ?</summary>

- `width: 1100px` : « mesure **exactement** 1100 px », même si l'écran n'en fait que 375 → ça déborde.
- `max-width: 1100px` : « mesure **au plus** 1100 px » → sur un écran de 375 px, la boîte prend les 375 px disponibles.

Combiné avec `margin: 0 auto`, `max-width` centre la page sur les grands écrans et la laisse occuper toute la largeur sur les petits.

</details>

<details>
<summary>Indice 3 — Mes media queries ne font rien !</summary>

Vérifiez dans l'ordre :

1. la **syntaxe** : `@media (min-width: 600px) {` avec les parenthèses, les deux-points et **deux** niveaux d'accolades (celles de `@media` et celles de chaque règle) ;
2. l'**ordre** : les media queries doivent être **après** les règles de base. À sélecteur égal, c'est la dernière règle écrite qui gagne (la cascade, exercice 02) ;
3. la **largeur** affichée en haut du mode appareil : à 375 px, il est normal que la media query `min-width: 600px` ne s'applique pas ;
4. le `meta viewport` dans `index.html`.

Dans **F12 → Éléments → Styles**, les règles venant d'une media query sont précédées de la mention `@media (min-width: 600px)` : vous voyez tout de suite si elles s'appliquent.

</details>

<details>
<summary>Indice 4 — Le menu en 2 × 2</summary>

C'est la liste `<ul class="menu">` qui devient une grille : `display: grid` et deux colonnes de même largeur (`1fr 1fr`). Pour que les liens remplissent leur case et soient faciles à toucher, ils sont en `display: block` avec un bon `padding`. Et pour que le menu passe sous le logo, c'est le `nav` (enfant de l'en-tête en flex) qui doit prendre `100%` de la largeur.

</details>

<details>
<summary>Indice 5 — Mon image est écrasée ou étirée</summary>

Si vous gardez une hauteur fixe (`height: 400px`) alors que la largeur change, l'image se déforme. Laissez le navigateur calculer la hauteur : `height: auto`. Les attributs `width` et `height` du HTML ne posent pas de problème : le CSS est prioritaire, et ils servent au navigateur à réserver la bonne place avant le chargement de l'image (exercice HTML 13).

</details>

## Bonus

- **Un titre qui grandit tout seul** : remplacez les tailles fixes du `h1` par `font-size: clamp(2rem, 1.2rem + 3vw, 2.75rem);` (« jamais moins de `2rem`, jamais plus de `2.75rem`, et entre les deux, proportionnel à la largeur de l'écran »). Observez en tirant le bord de la page.
- **Sur un vrai téléphone** : si votre ordinateur et votre téléphone sont sur le même réseau Wi-Fi, ouvrez sur le téléphone l'adresse IP de votre ordinateur suivie du port de Live Server (par exemple `http://192.168.1.20:5500`). Demandez au coach si le réseau de la salle le bloque.
- **Une étape intermédiaire** : ajoutez une troisième media query pour les très grands écrans (`min-width: 1400px`) qui agrandit un peu le texte de base. Est-ce vraiment utile ? Argumentez.

## Questions de compréhension

1. À quoi sert la balise `<meta name="viewport">` ? Que se passe-t-il sur un téléphone si on l'oublie ?
2. Que signifie *mobile first* ? Pourquoi écrit-on `min-width` (et pas `max-width`) dans les media queries avec cette méthode ?
3. Quelle est la différence entre `width: 1100px` et `max-width: 1100px` ?
4. Comment choisir ses *breakpoints* : selon le modèle de téléphone à la mode, ou selon le contenu ? Justifiez.
5. Pourquoi les boutons doivent-ils mesurer au moins 44 px de haut sur un écran tactile ?

## Lien avec le brief PlantEvo

La compétence visée est « Réaliser des interfaces utilisateur statiques **web ou web mobile** » (C3N1), et le jury évaluera la « convivialité » et « l'adaptabilité du site aux besoins des utilisateurs ». Sur un stand d'exposition, beaucoup de visiteurs ouvriront votre site **sur leur téléphone**. Pendant la démonstration, montrez votre page en mode appareil à 375 px **et** en grand écran : c'est un argument fort.

## Ressources

- [MDN — Le responsive design](https://developer.mozilla.org/fr/docs/Learn/CSS/CSS_layout/Responsive_Design)
- [MDN — Utiliser les media queries](https://developer.mozilla.org/fr/docs/Web/CSS/CSS_media_queries/Using_media_queries)
- [MDN — La balise meta viewport](https://developer.mozilla.org/fr/docs/Web/HTML/Viewport_meta_tag)
- [MDN — `max-width`](https://developer.mozilla.org/fr/docs/Web/CSS/max-width) · [`clamp()`](https://developer.mozilla.org/fr/docs/Web/CSS/clamp)
- [Chrome DevTools — Simuler des appareils mobiles](https://developer.chrome.com/docs/devtools/device-mode?hl=fr)
- [Validateur CSS du W3C](https://jigsaw.w3.org/css-validator/#validate_by_input)

---

Exercice suivant : [10 — Interactivité sans JavaScript](../10-interactivite/README.md)
