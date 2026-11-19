# Exercice 02 — Sélecteurs, classes et cascade

**Niveau 1 · Graine** · ★☆☆☆ · Durée : 45 min · Notions : sélecteur de balise, `.classe`, `#id`, sélecteur descendant, regroupement `h1, h2`, plusieurs classes, héritage, cascade, spécificité, `!important`

> Le calendrier du potager indique quels légumes semer en saison des pluies et en saison sèche. Le jardinier voudrait qu'on repère d'un coup d'œil les deux saisons, et les légumes faciles ou difficiles. Avec `h1` ou `p`, on ne peut viser que **toutes** les balises d'un type… Il est temps d'apprendre à **viser juste**.

## Objectifs

- Ajouter des `class` et des `id` dans le HTML pour pouvoir cibler des éléments précis.
- Utiliser les principaux sélecteurs : balise, classe, identifiant, descendant, regroupement.
- Comprendre l'**héritage** : certaines propriétés passent du parent aux enfants, d'autres non.
- Prévoir quelle règle gagne quand deux règles se contredisent (**cascade** et **spécificité**).

## Fichiers fournis

```
02-selecteurs-cascade/
├── README.md          ← cette consigne
├── index.html         ← le calendrier du potager (à compléter : classes et id)
├── quiz.html          ← partie B : le quiz « Qui gagne ? » (à ne pas modifier)
└── css/
    ├── style.css      ← la feuille du calendrier, avec des TODO
    └── quiz.css       ← les 6 duels du quiz
```

## Consigne

Ouvrez `index.html` avec Live Server : la page est déjà reliée à `css/style.css`, qui ne contient que le style de base. Les numéros correspondent aux commentaires `TODO` des fichiers.

### Partie A — Viser juste (30 min)

**D'abord le HTML : poser des « étiquettes ».**

1. Dans `index.html`, ajoutez à la première `<section>` **deux** classes, séparées par un espace : `class="saison pluies"`. Faites de même pour la deuxième avec `class="saison seche"`. Un élément peut porter plusieurs classes : il reçoit alors les styles de chacune.
2. Ajoutez à chaque `<li>` la classe `facile` ou `difficile`, selon le mot écrit entre parenthèses.
3. Donnez à l'`<aside>` l'identifiant `id="conseil"`. Un `id` est **unique** : un seul élément par page peut le porter.

**Ensuite le CSS, dans `css/style.css` :**

4. **Sélecteur de balise** — Tous les `<h2>` en vert `#2e7d32`.
5. **Regroupement** — `<h1>` et `<h2>` avec la police `Georgia, "Times New Roman", serif`. Écrivez **une seule** règle avec deux sélecteurs séparés par une virgule.
6. **Sélecteur de classe** (un point devant le nom) — Pour `.saison`, recopiez ces déclarations (les propriétés `border`, `padding` et `margin` seront expliquées à l'exercice 04) :

   ```css
   border-left: 6px solid #2e7d32;
   padding: 0.5rem 1rem;
   margin-bottom: 1rem;
   ```

7. **Plusieurs classes** — Une règle `.pluies` avec un fond bleu clair `#e3f2fd`, une règle `.seche` avec un fond orangé `#fff3e0`. Chaque section cumule maintenant la règle `.saison` **et** sa règle de saison.
8. `.facile` en vert foncé `#1b5e20` ; `.difficile` en rouge `#b71c1c` et en gras (`font-weight: bold`).
   On **garde** le mot entre parenthèses : une information ne doit jamais être donnée **uniquement** par la couleur (pensez aux personnes daltoniennes).
9. **Sélecteur d'identifiant** (un dièse devant le nom) — Pour `#conseil` : fond `#fff8e1`, texte brun `#6d4c41`, bordure `3px dashed #f9a825`, `padding: 0.5rem 1rem`.
10. **Observation : l'héritage** (pas de TODO, rien à écrire). Regardez l'encadré :
    - le **paragraphe** est brun, alors qu'aucune règle ne vise les `<p>` : il a **hérité** la couleur de son parent `#conseil`. Dans F12, sélectionnez ce `<p>` : le panneau *Styles* affiche « Hérité de aside#conseil » ;
    - le paragraphe n'a **pas** de bordure à lui : `border` ne s'hérite pas (heureusement !) ;
    - le **titre** `<h2>` de l'encadré, lui, reste vert : la règle `h2` de l'étape 4 le vise directement, et **une règle qui vise un élément gagne toujours contre une valeur héritée**.
11. **Sélecteur descendant** — Écrivez une règle `#conseil h2` (avec un espace) qui met en brun `#6d4c41` uniquement les `<h2>` situés **dans** `#conseil`. Les autres `<h2>` restent verts.

### Partie B — Qui gagne ? (15 min)

Quand plusieurs règles donnent une valeur différente à la même propriété d'un même élément, le navigateur doit choisir. C'est la **cascade**.

12. **Sans ouvrir `quiz.html` dans le navigateur**, lisez `quiz.html` puis `css/quiz.css` dans VS Code. Recopiez ce tableau sur une feuille (ou dans un fichier `reponses.md`) et **prédisez** le résultat de chaque duel, en vous aidant du mémo ci-dessous :

    | Duel | Élément | Ma prédiction | Pourquoi ? | Résultat observé |
    |---|---|---|---|---|
    | 1 | `p.graine` | | | |
    | 2 | `h2.recolte` | | | |
    | 3 | `p#arrosoir.outil` | | | |
    | 4 | `p.engrais` | | | |
    | 5 | le `<p>` dans `div.sol` (couleur ? bordure ?) | | | |
    | 6 | `p#tracteur.machine` | | | |

13. Ouvrez maintenant `quiz.html` et remplissez la dernière colonne. Pour chaque duel, inspectez l'élément dans F12 : les règles perdantes sont **barrées**. Si vous vous êtes trompé, relisez le mémo et trouvez pourquoi.
14. Modifiez `css/quiz.css` pour changer l'issue de trois duels :
    - **Duel 1** : faites gagner le bleu **sans changer aucune valeur** ;
    - **Duel 2** : faites gagner le rouge en complétant **seulement** le sélecteur `h2` (sans toucher à la règle `.recolte`) ;
    - **Duel 6** : supprimez `!important`. Qui gagne maintenant ? Pourquoi ?

Pour finir, passez `css/style.css` au [validateur CSS du W3C](https://jigsaw.w3.org/css-validator/#validate_by_input) : objectif **0 erreur**.

### Mémo — Les sélecteurs

| Sélecteur | Exemple | Vise… |
|---|---|---|
| Balise | `h2` | tous les `<h2>` |
| Classe | `.facile` | tous les éléments qui ont `class="… facile …"` |
| Identifiant | `#conseil` | **l'**élément qui a `id="conseil"` (unique dans la page) |
| Descendant | `#conseil h2` | les `<h2>` situés **à l'intérieur** de `#conseil` (à n'importe quelle profondeur) |
| Regroupement | `h1, h2` | les `<h1>` **et** les `<h2>` (même règle pour les deux) |
| Balise + classe | `li.facile` | les `<li>` qui ont la classe `facile` (sans espace !) |

### Mémo — Qui gagne ? (la spécificité)

Quand deux règles se contredisent, on compare leur **force**, de la plus forte à la plus faible :

| Force | Origine de la déclaration | Exemple |
|---|---|---|
| 1 (la plus forte) | attribut `style` dans le HTML | `<p style="color: purple;">` |
| 2 | sélecteur avec un **identifiant** | `#conseil` |
| 3 | sélecteur avec une **classe** (ou un attribut, une pseudo-classe) | `.facile`, `[aria-current]`, `:hover` |
| 4 | sélecteur de **balise** | `p`, `h2` |
| 5 (la plus faible) | valeur **héritée** du parent | — |

- Un sélecteur combiné **additionne** ses morceaux : `#conseil h2` (1 id + 1 balise) est plus fort que `.saison h2` (1 classe + 1 balise), lui-même plus fort que `h2`.
- À force **égale**, c'est la règle écrite **en dernier** qui gagne.
- `!important` passe devant tout le reste… et casse cette logique : on l'**évite**. Si vous en avez besoin, c'est souvent qu'un sélecteur est mal choisi.

## Critères de réussite

- [ ] Les deux `<section>` ont deux classes chacune, et chaque `<li>` a la classe `facile` ou `difficile`.
- [ ] L'encadré a l'`id="conseil"`, et cet `id` n'est utilisé qu'une fois.
- [ ] Ma feuille contient au moins un sélecteur de chaque sorte : balise, classe, identifiant, descendant, regroupement.
- [ ] Les deux saisons ont un fond différent et une barre verte à gauche ; les légumes difficiles sont en rouge et en gras.
- [ ] Le titre de l'encadré est brun, les autres `<h2>` sont verts.
- [ ] Je sais expliquer pourquoi le paragraphe de l'encadré est brun sans avoir de bordure.
- [ ] J'ai rempli le tableau du quiz **avant** d'ouvrir la page, et je sais expliquer chacun des 6 résultats.
- [ ] Je n'ai utilisé aucun `!important` dans `style.css`.
- [ ] Le validateur CSS du W3C n'affiche aucune erreur.

## Indices

<details>
<summary>Indice 1 — Comment écrire deux classes sur un élément ?</summary>

Dans **un seul** attribut `class`, les noms séparés par un espace :

```html
<p class="carte importante">…</p>
```

Écrire deux attributs `class` sur la même balise est une erreur : le navigateur ignore le second.

</details>

<details>
<summary>Indice 2 — Ma règle <code>.facile</code> ne s'applique pas</summary>

- Dans le CSS, la classe s'écrit **avec un point** : `.facile`. Dans le HTML, **sans point** : `class="facile"`.
- Les noms doivent être **identiques**, majuscules comprises : `.Facile` ne vise pas `class="facile"`.
- Vérifiez dans F12 que l'élément a bien la classe (onglet *Éléments*).

</details>

<details>
<summary>Indice 3 — Quelle différence entre <code>#conseil h2</code> et <code>#conseil, h2</code> ?</summary>

L'**espace** veut dire « à l'intérieur de » : `#conseil h2` vise seulement les `<h2>` contenus dans `#conseil`.
La **virgule** veut dire « et aussi » : `#conseil, h2` vise l'élément `#conseil` **et** tous les `<h2>` de la page. Un seul caractère, deux résultats très différents !

</details>

<details>
<summary>Indice 4 — Comment voir qui a gagné dans F12 ?</summary>

Inspectez l'élément (clic droit → *Inspecter*). Le panneau *Styles* liste toutes les règles qui le visent, **de la plus forte (en haut) à la plus faible (en bas)**. Les déclarations perdantes sont barrées. L'onglet *Calculé* (*Computed*) donne la valeur finale.

</details>

## Bonus

- Jouez à [CSS Diner](https://flukeout.github.io/) : un jeu pour s'entraîner aux sélecteurs (niveaux 1 à 10 pour commencer).
- Ajoutez une classe `nouveau` à un légume de votre choix (par exemple « Gombo ») et écrivez une règle `.nouveau` qui le met en italique. Il cumule maintenant `facile` et `nouveau`.
- Écrivez une règle `.seche h2` qui donne une autre couleur au titre de la saison sèche seulement. Est-elle plus forte ou plus faible que `h2` ? Et que `#conseil h2` ?

## Questions de compréhension

1. Quelle est la différence entre une classe et un identifiant ? Quand utiliser l'une ou l'autre ?
2. Que vise le sélecteur `nav a` ? Et `nav, a` ?
3. Qu'est-ce que l'héritage ? Citez une propriété qui s'hérite et une qui ne s'hérite pas.
4. Deux règles de même force se contredisent : laquelle gagne ?
5. Pourquoi faut-il éviter `!important` ?

## Lien avec le brief PlantEvo

Sur votre site PlantEvo, toutes les fiches de végétaux auront la **même apparence** : c'est le rôle d'une classe (par exemple `.fiche` ou `.carte`), écrite une fois dans le CSS et posée sur chaque bloc dans le HTML. Des sélecteurs bien choisis, sans `!important`, rendent le code plus court et plus lisible : c'est exactement ce que regarde le jury pour le critère « code source correctement commenté et organisé ».

## Ressources

- [MDN — Les sélecteurs CSS](https://developer.mozilla.org/fr/docs/Learn/CSS/Building_blocks/Selectors)
- [MDN — Cascade et héritage](https://developer.mozilla.org/fr/docs/Learn/CSS/Building_blocks/Cascade_and_inheritance)
- [MDN — Spécificité](https://developer.mozilla.org/fr/docs/Web/CSS/Specificity)
- [CSS Diner — le jeu des sélecteurs](https://flukeout.github.io/)
- [Validateur CSS du W3C (saisie directe)](https://jigsaw.w3.org/css-validator/#validate_by_input)

---

Exercice suivant : [03 — Couleurs, polices et variables](../03-couleurs-polices/README.md)
