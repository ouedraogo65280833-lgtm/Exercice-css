# Exercice 06 — Cartes et bannière avec Flexbox

**Niveau 2 · Pousse** · ★★☆☆ · Durée : 1 h · Notions : `flex-wrap`, `flex` (`flex-grow`, `flex-shrink`, `flex-basis`), `flex-direction: column`, `margin-top: auto`, `align-self`, centrage vertical, images fluides

> La coopérative Terre Fertile veut présenter ses six produits de saison sur une seule page : une grande bannière d'accueil, puis une rangée de cartes, chacune avec une image, un petit texte et un bouton « Commander ». Le HTML est prêt, les couleurs aussi. Il ne manque que la mise en page… et c'est Flexbox qui va s'en charger.

## Objectifs

- Centrer un contenu **horizontalement et verticalement** dans une bannière.
- Créer une rangée de cartes qui **passe à la ligne** et s'adapte à la largeur de l'écran.
- Comprendre le raccourci `flex: 1 1 16rem` (grandir, rétrécir, largeur de départ).
- Aligner les boutons de toutes les cartes en bas, même quand les textes n'ont pas la même longueur.
- Rendre les images **fluides** : elles ne débordent jamais de leur boîte.

## Fichiers fournis

```
06-cartes-flexbox/
├── README.md        ← cette consigne
├── index.html       ← la page complète (vous n'y touchez pas, sauf en bonus)
├── css/
│   └── style.css    ← couleurs, textes et boutons déjà faits ; les TODO sont pour la mise en page
└── images/
    ├── logo.svg
    └── mangue.svg  banane.svg  cacao.svg  tomate.svg  piment.svg  carotte.svg
```

## Consigne

**Étape 0 — Observer (5 min).** Ouvrez `index.html` avec Live Server. Tout est empilé : les cartes occupent toute la largeur, une par ligne. Dans le HTML, repérez les classes `.bandeau`, `.banniere`, `.cartes` (le conteneur), `.carte` (chaque produit) et `.pied-colonnes`. Pour chaque élément, demandez-vous : **qui est le parent, qui sont les enfants ?** C'est toujours le parent qui reçoit `display: flex`.

Complétez ensuite `css/style.css` (les numéros correspondent aux `TODO` du fichier) :

1. **En-tête (rappel de l'exercice 05).** Dans `.bandeau`, placez le logo et le nom du site côte à côte, centrés verticalement, avec un espace de `0.75rem`.
2. **Images fluides.** Dans la règle `img`, écrivez les trois déclarations que vous réutiliserez dans **tous** vos projets :
   ```css
   display: block;   /* supprime le petit espace sous l'image */
   max-width: 100%;  /* jamais plus large que son conteneur */
   height: auto;     /* garde les proportions */
   ```
   Rétrécissez la fenêtre : les images rétrécissent avec elle au lieu de déborder.
3. **Bannière centrée.** Dans `.banniere` :
   - `display: flex` et `flex-direction: column` : le titre, le texte et le bouton se placent **les uns sous les autres** ;
   - `align-items: center` : ils sont centrés horizontalement (avec `column`, l'axe secondaire est horizontal !) ;
   - `min-height: 22rem` puis `justify-content: center` : le bloc est centré verticalement dans la bannière.

   Observez le paragraphe : avant cette étape, il était collé à gauche. Pourquoi ? (Indice : il a un `max-width`.)
4. **Une rangée de cartes.** Dans `.cartes`, ajoutez `display: flex` et `gap: 1.5rem`. Rechargez : les six cartes sont sur **une seule ligne**, toutes écrasées. C'est normal : par défaut, Flexbox ne passe jamais à la ligne.
5. **Passer à la ligne.**
   - Dans `.cartes`, ajoutez `flex-wrap: wrap`.
   - Dans `.carte`, ajoutez `flex: 1 1 16rem;`. Cette ligne veut dire : « pars d'une largeur de **16rem** (`flex-basis`), **grandis** pour remplir la place restante (`flex-grow: 1`) et **rétrécis** si besoin (`flex-shrink: 1`) ».
   - Élargissez puis rétrécissez la fenêtre : 3 cartes par ligne, puis 2, puis 1.
6. **Des boutons alignés.** Les textes n'ont pas la même longueur : les boutons sont à des hauteurs différentes. Corrigez-le :
   - dans `.carte`, ajoutez `display: flex` et `flex-direction: column` (la carte devient à son tour un conteneur flexible : image, titre, texte et bouton sont ses enfants) ;
   - dans `.carte .bouton`, ajoutez `margin-top: auto` : cette marge automatique **absorbe tout l'espace libre** au-dessus du bouton et le pousse en bas ;
   - le bouton s'étire maintenant sur toute la largeur (c'est le comportement par défaut, `align-items: stretch`). Ajoutez `align-self: flex-start` pour qu'il reprenne sa taille.
7. **Pied de page en colonnes.** Dans `.pied-colonnes`, ajoutez `display: flex`, `flex-wrap: wrap` et `gap: 1rem 2rem` (1rem entre les lignes, 2rem entre les colonnes). Dans `.pied-colonnes section`, ajoutez `flex: 1 1 12rem`.
8. **Tester (5 min).** Passez en mode appareil (`Ctrl + Maj + M`) et testez 375 px, 768 px et 1280 px. Rien ne doit déborder, aucun défilement horizontal. Puis, dans les outils de développement, remplacez temporairement `flex: 1 1 16rem` par :
   - `flex: 0 0 16rem` → que se passe-t-il quand la fenêtre est large ? et étroite ?
   - `flex: 1 1 30rem` → combien de cartes par ligne sur grand écran ?

### Mémo : les propriétés des enfants flexibles

| Propriété (sur l'**enfant**) | Rôle | Exemple |
|---|---|---|
| `flex-basis` | Largeur de départ (sur l'axe principal) | `16rem` |
| `flex-grow` | Part de l'espace **libre** que l'enfant récupère (0 = ne grandit pas) | `1` |
| `flex-shrink` | Capacité à rétrécir quand la place manque (0 = ne rétrécit pas) | `1` |
| `flex` | Raccourci : `flex-grow flex-shrink flex-basis` | `flex: 1 1 16rem` |
| `align-self` | Alignement de **cet** enfant seulement sur l'axe secondaire | `flex-start`, `center` |
| `margin-top: auto` (ou `margin-left: auto`…) | La marge prend tout l'espace libre : pousse l'enfant au bout | bouton en bas d'une carte |

| Propriété (sur le **parent**) | Rôle |
|---|---|
| `flex-wrap: wrap` | Autorise les enfants à passer à la ligne |
| `flex-direction: column` | Les enfants s'empilent ; l'axe principal devient **vertical** |
| `gap: 1rem 2rem` | Espace entre les lignes, puis entre les colonnes |

## Critères de réussite

- [ ] Le logo et le nom du site sont alignés dans l'en-tête.
- [ ] Le contenu de la bannière (titre, texte, bouton) est centré horizontalement **et** verticalement.
- [ ] Sur grand écran, les cartes sont 3 par ligne ; elles passent à 2, puis à 1 quand l'écran rétrécit.
- [ ] Dans chaque rangée, les cartes ont la même hauteur et **tous les boutons sont alignés en bas**.
- [ ] Les boutons des cartes ne sont pas étirés sur toute la largeur.
- [ ] Les images ne débordent jamais, et elles gardent leurs proportions.
- [ ] Les trois colonnes du pied de page passent les unes sous les autres sur téléphone.
- [ ] À 375 px, pas de défilement horizontal.
- [ ] Le validateur CSS du W3C n'affiche aucune erreur.

## Indices

<details>
<summary>Indice 1 — <code>justify-content: center</code> ne centre pas verticalement ma bannière</summary>

Deux causes possibles :
- Avec `flex-direction: column`, l'axe **principal** est vertical : c'est bien `justify-content` qui centre verticalement… à condition qu'il y ait de la place en trop ! Sans `min-height`, la bannière est exactement aussi haute que son contenu : il n'y a rien à centrer.
- Vous avez écrit `align-items` à la place de `justify-content` (ou l'inverse). Relisez le mémo de l'exercice 05 : les deux propriétés « échangent leur rôle » quand on passe en `column`.

</details>

<details>
<summary>Indice 2 — Mes cartes n'ont pas toutes la même hauteur</summary>

Par défaut, les enfants d'un conteneur flexible s'étirent sur toute la hauteur de la ligne (`align-items: stretch`). Si une carte est plus courte que ses voisines, vérifiez que vous n'avez pas mis `align-items` sur `.cartes`, ni de `height` sur `.carte`.

</details>

<details>
<summary>Indice 3 — <code>margin-top: auto</code> ne pousse pas mon bouton</summary>

La marge automatique ne fonctionne que si **le parent du bouton** est un conteneur flexible en colonne. Le parent du bouton, c'est la carte (`.carte`), pas la rangée (`.cartes`). Attention au « s » !

</details>

<details>
<summary>Indice 4 — À quoi sert <code>display: block</code> sur une image ?</summary>

Une image est un élément en ligne, comme une lettre : elle s'aligne sur la ligne de base du texte, et le navigateur laisse en dessous un petit espace (pour les jambages des lettres comme « g » ou « p »). Inspectez une image avant et après : les quelques pixels vides disparaissent.

</details>

## Bonus

- Ajoutez une **7e carte** dans `index.html` (le sorgho, par exemple : copiez une carte existante). Sur grand écran, regardez la dernière ligne : la carte seule s'étire sur toute la largeur. Essayez de limiter sa largeur avec `max-width` sur `.carte`. Vous verrez à l'exercice 07 que **Grid** règle ce problème plus proprement.
- Ajoutez à la bannière une photo de fond (`background-image`) en gardant un dégradé vert semi-transparent par-dessus pour que le texte reste lisible.
- Faites en sorte que l'image de chaque carte soit légèrement agrandie au survol de la carte (`.carte:hover img { transform: scale(1.03); }`) : vous approfondirez cela à l'exercice 10.

## Questions de compréhension

1. Dans `flex: 1 1 16rem`, que signifie chacun des trois nombres ?
2. Pourquoi faut-il `flex-wrap: wrap` pour que les cartes passent à la ligne ? Que fait Flexbox sans lui ?
3. Quand on écrit `flex-direction: column`, que deviennent les rôles de `justify-content` et de `align-items` ?
4. Une même boîte peut-elle être à la fois un **enfant** flexible et un **conteneur** flexible ? Donnez un exemple tiré de cet exercice.
5. Citez les trois déclarations qui rendent une image fluide, et expliquez chacune.

## Lien avec le brief PlantEvo

Votre page d'accueil PlantEvo peut présenter les grands groupes de végétaux sous forme de **cartes** (une image, un titre, une phrase, un lien vers la page détail), et commencer par une **bannière** qui donne envie de lire la suite. Le brief demande « 80 % d'images » : des images fluides, qui s'adaptent à la largeur de l'écran, sont indispensables, en particulier pour que le site reste lisible sur téléphone (« web **mobile** », compétence C3N1).

## Ressources

- [MDN — Flexbox (apprendre)](https://developer.mozilla.org/fr/docs/Learn/CSS/CSS_layout/Flexbox)
- MDN : [`flex`](https://developer.mozilla.org/fr/docs/Web/CSS/flex) · [`flex-wrap`](https://developer.mozilla.org/fr/docs/Web/CSS/flex-wrap) · [`align-self`](https://developer.mozilla.org/fr/docs/Web/CSS/align-self)
- [MDN — Contrôler les proportions des éléments flexibles](https://developer.mozilla.org/fr/docs/Web/CSS/CSS_flexible_box_layout/Controlling_ratios_of_flex_items_along_the_main_axis)
- [Flexbox Froggy](https://flexboxfroggy.com/#fr)
- [Validateur CSS du W3C](https://jigsaw.w3.org/css-validator/#validate_by_input)

---

Exercice suivant : [07 — Une galerie d'images avec Grid](../07-galerie-grid/README.md)
