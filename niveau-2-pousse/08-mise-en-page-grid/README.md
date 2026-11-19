# Exercice 08 — Mettre en page un site entier avec Grid

**Niveau 2 · Pousse** · ★★☆☆ · Durée : 1 h · Notions : `grid-template-areas`, `grid-area`, `grid-template-rows`, `min-height: 100vh`, `margin-inline: auto`, `position: sticky`, première media query, Flexbox ou Grid ?

> Les apprenants de la ferme-école publient chaque semaine un petit journal en ligne. La page est parfaitement **sémantique** (`header`, `nav`, `main`, `article`, `aside`, `footer`) et la décoration est déjà faite… mais tout est empilé, d'un bord à l'autre de l'écran. Votre mission : dessiner le plan de la page, puis le donner à CSS Grid, **sans ajouter une seule classe**.

## Objectifs

- Décrire la mise en page d'un site entier avec `grid-template-areas`, comme un plan dessiné en texte.
- Placer chaque grand bloc sémantique dans sa zone avec `grid-area`.
- Garder le pied de page en bas de l'écran, même quand la page est courte.
- Centrer la page et limiter sa largeur.
- Changer complètement la mise en page sur téléphone en redessinant le plan dans une media query.
- Savoir choisir entre Flexbox et Grid.

## Fichiers fournis

```
08-mise-en-page-grid/
├── README.md        ← cette consigne
├── index.html       ← la page sémantique, sans aucune classe (vous n'y touchez pas)
├── css/
│   └── style.css    ← la décoration est faite ; les TODO sont pour la mise en page
└── images/
    ├── logo.svg
    ├── mais.svg
    └── poule.svg
```

## Consigne

**Étape 0 — Le plan sur papier (5 min).** Ouvrez `index.html` avec Live Server. Sur une feuille, dessinez la page telle que vous la voulez sur un **ordinateur**, et donnez un nom court à chaque zone :

```
┌──────────────────────────────────────────┐
│ entete                                   │   ← <header>
├──────────────────────────────────────────┤
│ menu                                     │   ← <nav>
├────────────────────────────┬─────────────┤
│ contenu                    │ encadre     │   ← <main> | <aside>
│ (les 3 articles)           │ (18rem)     │
├────────────────────────────┴─────────────┤
│ pied                                     │   ← <footer>
└──────────────────────────────────────────┘
```

Ce plan, vous allez maintenant **l'écrire presque tel quel** en CSS. Complétez `css/style.css` (les numéros correspondent aux `TODO`) :

1. **Nommer les zones.** Sous le commentaire `TODO 1`, écrivez cinq règles qui donnent à chaque bloc le nom de sa zone :
   ```css
   header {
     grid-area: entete;
   }
   ```
   … puis `nav` → `menu`, `main` → `contenu`, `aside` → `encadre`, `footer` → `pied`. Rien ne change encore : les zones existent, mais il n'y a pas de grille.
2. **La grille de la page.** Dans la règle `body` (`TODO 2`) :
   ```css
   display: grid;
   grid-template-columns: 1fr 18rem;
   grid-template-areas:
     "entete  entete"
     "menu    menu"
     "contenu encadre"
     "pied    pied";
   gap: 1.5rem;
   ```
   Chaque chaîne entre guillemets est une **rangée**, chaque mot une **colonne**. Répéter un nom (`"entete entete"`) étend la zone sur plusieurs colonnes. Rechargez : l'encadré se place à droite des articles. Dans `F12`, cliquez sur le badge `grid` à côté de `<body>`, puis, dans le panneau *Mise en page* (*Layout*), cochez **« Show area names »** : les noms de vos zones s'affichent sur la page !
3. **Le pied de page en bas.** Ajoutez dans `body` (`TODO 3`) :
   ```css
   grid-template-rows: auto auto 1fr auto;
   min-height: 100vh;
   ```
   `100vh` = 100 % de la hauteur de la fenêtre. Les rangées `auto` prennent la hauteur de leur contenu ; la rangée `1fr` (celle du contenu) **absorbe tout l'espace restant**. Pour le vérifier : dans l'inspecteur, supprimez deux articles (sélectionnez un `<article>` puis touche `Suppr`). Le pied de page reste collé en bas de la fenêtre. Rechargez la page pour récupérer les articles.
4. **Une page centrée.** Toujours dans `body` (`TODO 4`) : `max-width: 70rem`, `margin-inline: auto` (marges automatiques à gauche et à droite : c'est le raccourci de `margin-left` + `margin-right`) et `padding-inline: 1rem`. Élargissez la fenêtre au maximum : la page reste centrée et lisible.
5. **Le menu (rappel de l'exercice 05).** Dans `nav ul` : pas de puces, ni marge ni retrait, des liens côte à côte qui passent à la ligne, espacés de `0.5rem`.
6. **Un encadré qui suit le lecteur.** Dans `aside` (`TODO 6`) :
   ```css
   position: sticky;
   top: 1rem;
   align-self: start;
   ```
   Faites défiler la page : l'agenda reste visible, à 1rem du haut de la fenêtre. Supprimez `align-self: start` pour comprendre son rôle : par défaut, l'encadré s'étire sur toute la hauteur de sa rangée… et n'a donc plus de place pour « glisser ».
7. **Et sur téléphone ?** Passez en mode appareil (`Ctrl + Maj + M`), largeur 375 px : avec deux colonnes, les articles sont écrasés. Sous le commentaire `TODO 7`, ajoutez votre **première media query**. Son contenu ne s'applique **que** si la fenêtre fait 700px de large ou moins :
   ```css
   @media (max-width: 700px) {
     body {
       grid-template-columns: 1fr;
       grid-template-rows: auto auto 1fr auto auto;
       grid-template-areas:
         "entete"
         "menu"
         "contenu"
         "encadre"
         "pied";
     }
   }
   ```
   Sur un écran étroit, vous avez simplement **redessiné le plan** : une seule colonne, l'encadré passe sous les articles. Ajoutez aussi `aside { position: static; }` dans la media query : sur une seule colonne, l'encadré n'a plus besoin de « coller ».
8. **Tester (5 min).** Testez 375 px, 768 px et 1280 px. Puis, pour vous entraîner, modifiez **uniquement** `grid-template-areas` (et `grid-template-columns`) pour mettre l'encadré **à gauche** des articles sur ordinateur. Combien de lignes avez-vous changées ? Remettez-le à droite.

### Mémo : la mise en page par zones

| Propriété | Sur | Rôle |
|---|---|---|
| `grid-template-areas` | parent | Le plan de la page : une chaîne `"…"` par rangée, un nom par colonne (`.` = case vide) |
| `grid-area: nom` | enfant | Place l'élément dans la zone qui porte ce nom |
| `grid-template-rows` | parent | Hauteur des rangées : `auto` (selon le contenu), `1fr` (le reste) |
| `min-height: 100vh` | parent | Au moins la hauteur de la fenêtre |
| `margin-inline: auto` | élément | Centre horizontalement un bloc qui a une largeur maximale |
| `position: sticky` + `top` | élément | L'élément « colle » à cette distance du haut quand on fait défiler |
| `@media (max-width: 700px) { … }` | — | Les règles à l'intérieur ne s'appliquent que si la fenêtre fait 700px ou moins |

### Flexbox ou Grid ?

| | **Flexbox** | **Grid** |
|---|---|---|
| Dimension | **Une** direction : une ligne **ou** une colonne | **Deux** directions : des lignes **et** des colonnes |
| Point de départ | Le **contenu** : chaque élément prend la place dont il a besoin | La **structure** : on dessine les cases, puis on y range les éléments |
| Idéal pour | Un menu, une barre d'outils, le contenu d'une carte, centrer un élément | Une mise en page de site, une galerie, un tableau de cartes bien aligné |
| Dans cet exercice | Le menu (`nav ul`), l'en-tête (logo + titre) | La page entière (`body`), la liste des articles (`main`) |

Les deux se combinent très bien : une case de Grid peut contenir un conteneur Flexbox, et inversement.

## Critères de réussite

- [ ] Je n'ai ajouté **aucune classe** ni aucun `id` dans le HTML.
- [ ] Sur ordinateur, l'en-tête, le menu et le pied de page occupent toute la largeur ; l'encadré est à droite des articles.
- [ ] Le plan de la page est lisible dans mon CSS grâce à `grid-template-areas`.
- [ ] Le pied de page reste en bas de la fenêtre, même si je supprime des articles dans l'inspecteur.
- [ ] La page est centrée et ne dépasse pas 70rem de large.
- [ ] L'encadré reste visible quand je fais défiler la page sur ordinateur.
- [ ] À 375 px, tout est sur une seule colonne, dans l'ordre : en-tête, menu, articles, encadré, pied de page, sans défilement horizontal.
- [ ] Le validateur CSS du W3C n'affiche aucune erreur.

## Indices

<details>
<summary>Indice 1 — Ma grille est complètement désordonnée</summary>

`grid-template-areas` est très strict :
- chaque chaîne doit avoir **le même nombre de mots** (ici 2, puisqu'il y a 2 colonnes) ;
- une zone doit former un **rectangle** (pas de forme en L) ;
- les noms de `grid-area` doivent être écrits **exactement** comme dans le plan, **sans guillemets** : `grid-area: entete;`.

Si une seule de ces règles n'est pas respectée, toute la déclaration est ignorée (elle apparaît barrée dans l'inspecteur).

</details>

<details>
<summary>Indice 2 — Le pied de page ne descend pas en bas de la fenêtre</summary>

Il faut **les deux** : une hauteur minimale sur la grille (`min-height: 100vh`) **et** une rangée élastique (`1fr`) au bon endroit. Comptez vos rangées : 4 chaînes dans `grid-template-areas` = 4 valeurs dans `grid-template-rows`. Laquelle doit être élastique ?

</details>

<details>
<summary>Indice 3 — <code>position: sticky</code> ne fonctionne pas</summary>

Trois causes fréquentes : il manque `top` (l'élément ne sait pas où s'arrêter) ; l'élément est aussi haut que sa rangée (d'où `align-self: start`) ; ou vous êtes sur un écran étroit où la media query l'a remis en `static`.

</details>

<details>
<summary>Indice 4 — Pourquoi <code>max-width</code> dans la media query, et pas <code>min-width</code> ?</summary>

Ici, la page a d'abord été pensée pour l'ordinateur, puis **adaptée** au téléphone : on écrit donc « si l'écran est **plus petit** que… » (`max-width`). Dans l'exercice 09, vous apprendrez la démarche inverse, recommandée aujourd'hui : partir du téléphone (*mobile first*) et ajouter des règles pour les écrans **plus grands** (`min-width`).

</details>

## Bonus

- Ajoutez une colonne vide de chaque côté sur très grand écran en utilisant le point `.` dans `grid-template-areas` (une case sans nom). Observez le résultat avec l'inspecteur de grille.
- Créez une media query intermédiaire (par exemple entre 701px et 1000px) où l'encadré passe **au-dessus** des articles, sur toute la largeur.
- Jouez à **[Grid Garden](https://cssgridgarden.com/#fr)** si ce n'est pas déjà fait.

## Questions de compréhension

1. Que représente chaque chaîne entre guillemets dans `grid-template-areas` ? Et chaque mot ?
2. Pourquoi le pied de page reste-t-il en bas de la fenêtre ? Expliquez le rôle de `1fr` et de `min-height: 100vh`.
3. Quelle est la différence entre Flexbox et Grid ? Donnez un exemple où vous choisiriez chacun.
4. Pourquoi a-t-on pu faire toute la mise en page sans ajouter de classe ? Quel exercice de la série HTML vous a préparé à cela ?
5. Qu'est-ce qu'une media query ? Que fait `@media (max-width: 700px)` ?

## Lien avec le brief PlantEvo

Votre page PlantEvo aura elle aussi un `<header>`, un `<nav>` (le menu), un `<main>` et un `<footer>` : avec `grid-template-areas`, toute la structure de votre page tient en quelques lignes **lisibles**, que le jury comprendra d'un coup d'œil lors de la revue du code (« code correctement commenté et organisé »). Un `<aside>` peut accueillir un encadré « Le saviez-vous ? » ou un lexique à côté de votre contenu principal. Et la media query vous assure que le site reste utilisable sur le téléphone d'un visiteur du stand.

## Ressources

- [MDN — Les zones nommées (`grid-template-areas`)](https://developer.mozilla.org/fr/docs/Web/CSS/CSS_grid_layout/Grid_template_areas)
- MDN : [`grid-area`](https://developer.mozilla.org/fr/docs/Web/CSS/grid-area) · [`grid-template-rows`](https://developer.mozilla.org/fr/docs/Web/CSS/grid-template-rows) · [`position`](https://developer.mozilla.org/fr/docs/Web/CSS/position) · [`margin-inline`](https://developer.mozilla.org/fr/docs/Web/CSS/margin-inline)
- [MDN — Relations entre Grid et les autres méthodes de mise en page](https://developer.mozilla.org/fr/docs/Web/CSS/CSS_grid_layout/Relationship_of_grid_layout_with_other_layout_methods)
- [MDN — Les media queries](https://developer.mozilla.org/fr/docs/Web/CSS/CSS_media_queries/Using_media_queries)
- [Validateur CSS du W3C](https://jigsaw.w3.org/css-validator/#validate_by_input)

---

Exercice suivant : [09 — Responsive : du téléphone à l'ordinateur](../../niveau-3-arbre/09-responsive/README.md)
