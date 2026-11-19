# Exercice 10 — Interactivité sans JavaScript

**Niveau 3 · Arbre** · ★★★☆ · Durée : 1 h · Notions : `:hover`, `:focus-visible`, `:active`, `:focus-within`, `transition`, `transform`, `@keyframes` / `animation`, `:target`, `scroll-behavior`, `<details>` / `<summary>`, `::after`, `prefers-reduced-motion`

> Le jardin pédagogique de la ferme-école a son guide des épices. La page est propre… mais **figée** : rien ne réagit quand on passe la souris, on ne sait jamais où l'on se trouve, et le clic sur le sommaire fait « sauter » la page. Votre mission : la rendre vivante et agréable à utiliser, **à la souris comme au clavier**, avec seulement du CSS.

## Objectifs

- Réagir aux actions de l'utilisateur avec les **pseudo-classes** `:hover`, `:focus-visible`, `:active`, `:focus-within` et `:target`.
- Rendre les changements **progressifs** avec `transition`, et déplacer ou agrandir un élément avec `transform`.
- Créer une courte **animation** avec `@keyframes`.
- Styliser un accordéon natif `<details>` / `<summary>`.
- Penser à **tous** les visiteurs : navigation au clavier et réglage « réduire les animations ».

## Fichiers fournis

```
10-interactivite/
├── README.md          ← cette consigne
├── index.html         ← la page (complète : vous ne la modifiez pas)
├── css/
│   └── style.css      ← la mise en page est faite ; les TODO attendent votre interactivité
└── images/
    ├── gingembre.svg  piment.svg  citronnelle.svg  basilic.svg
```

## Consigne

**Étape 0 — Observation (5 min).** Ouvrez `index.html` avec Live Server, puis :

- passez la souris sur les liens du sommaire, le bouton jaune, les cartes : que se passe-t-il ?
- cliquez sur « Piment » dans le sommaire : comment arrive-t-on sur la carte ? Sait-on quelle carte on a demandée ?
- cliquez dans la barre d'adresse, puis appuyez plusieurs fois sur la touche **Tab** (`⇥`) : le **focus clavier** passe d'un lien à l'autre. Le voit-on bien ?
- cliquez sur une question de la FAQ : elle s'ouvre déjà ! C'est le rôle de la balise HTML `<details>`. Il reste à la rendre plus claire.

Complétez ensuite `css/style.css` (les numéros correspondent aux commentaires `TODO` du fichier) :

1. **Les liens du sommaire.**
   - Au **survol** (`.sommaire a:hover`) : fond vert (`var(--vert)`) et texte blanc.
   - Au **focus clavier** (`.sommaire a:focus-visible`) : un contour jaune bien visible, par exemple `outline: 3px solid var(--soleil);` et `outline-offset: 2px;`.
   - Pour que le changement soit **progressif**, ajoutez sur la règle **normale** `.sommaire a` (pas sur `:hover` !) : `transition: background-color 0.2s ease, color 0.2s ease;`.
   - Expérience : passez la durée à `2s`, observez, puis revenez à `0.2s`.
2. **Le bouton jaune.**
   - Au survol : un jaune plus clair (`#ffca28`).
   - Pendant le clic (`:active`) : le bouton « s'enfonce » de 2 px vers le bas grâce à `transform: translateY(2px);`.
   - Au focus clavier : un contour **blanc** (il est sur fond vert).
   - Une `transition` sur `background-color` et `transform`.
3. **Les cartes qui se soulèvent.** Quand la souris passe sur une carte, elle monte de 6 px (`transform: translateY(-6px);`) et son ombre grandit (`box-shadow: var(--ombre-forte);`), avec une transition de `0.3s` sur `transform` et `box-shadow`.
   **Au clavier aussi** : ajoutez le sélecteur `.carte:focus-within` à la même règle. Il s'applique quand un élément **à l'intérieur** de la carte (ici, le lien « Retour en haut ») a le focus. Testez avec la touche Tab.
4. **Le zoom d'image.** Au survol d'une carte, l'image grossit (`transform: scale(1.1);`) en douceur (transition de `0.4s` sur l'image). Testez : l'image déborde de son cadre ! Ajoutez `overflow: hidden;` sur `.cadre-image` : le cadre « coupe » ce qui dépasse. Essayez aussi `transform: scale(1.1) rotate(-2deg);`.
5. **Le défilement doux.** Ajoutez une règle pour `html` avec `scroll-behavior: smooth;`, puis cliquez sur les liens du sommaire et sur « Retour en haut ».
6. **La carte ciblée (`:target`).** Quand on clique sur « Piment », l'adresse de la page se termine par `#piment` et la carte `id="piment"` devient la **cible**. Mettez-la en valeur :
   - `.carte:target` : un contour jaune de 4 px, décalé de 4 px (`outline-offset`) ;
   - une **animation** qui fait passer le fond du jaune clair au blanc. Créez-la avec `@keyframes surligner { from { … } to { … } }`, puis appliquez-la à `.carte:target` avec `animation: surligner 1.5s ease-out;` ;
   - pour que la carte ne soit pas collée en haut de l'écran après le saut, ajoutez `scroll-margin-top: 1.5rem;` à la règle `.carte`.
7. **La FAQ en accordéon.**
   - Sur `summary` : `cursor: pointer;` (la petite main), `list-style: none;` (supprime le triangle), et un `display: flex` avec `justify-content: space-between` pour placer la question à gauche et un signe à droite.
   - Le signe : `summary::after { content: "+"; }` (agrandissez-le et ajoutez une transition sur `transform`).
   - Quand la question est ouverte, le navigateur ajoute l'attribut `open` à `<details>` : utilisez le sélecteur `details[open]` pour colorer la bordure en vert, et `details[open] summary::after` pour tourner le « + » de 45° (il devient un « × »).
   - Ajoutez un fond vert clair au survol de `summary` et un contour au focus clavier.
8. **Respecter les préférences de l'utilisateur.** Certaines personnes ont des vertiges ou des nausées devant les animations ; elles activent « Réduire les animations » dans les réglages de leur téléphone ou de leur ordinateur. À la fin du fichier, ajoutez une media query `@media (prefers-reduced-motion: reduce) { … }` qui :
   - remet `scroll-behavior: auto` sur `html` ;
   - met `transition: none` sur tous les éléments qui ont une transition ;
   - met `animation: none` sur `.carte:target`.

   Pour tester sans changer les réglages de votre ordinateur : **F12**, puis `Ctrl + Maj + P` (menu de commandes), tapez `reduced motion` et choisissez **Emulate CSS prefers-reduced-motion: reduce**.
9. **Test au clavier, sans souris.** Rechargez la page et parcourez-la uniquement avec **Tab**, **Maj + Tab** (revenir en arrière), **Entrée** (suivre un lien) et **Espace** (ouvrir une question de la FAQ). À chaque instant, vous devez voir où se trouve le focus.
10. **Validez** votre CSS avec le [validateur CSS du W3C](https://jigsaw.w3.org/css-validator/#validate_by_input) : objectif **0 erreur**.

### Mémo — l'interactivité en CSS

| Sélecteur | S'applique quand… | Exemple |
|---|---|---|
| `a:hover` | la souris passe sur l'élément | changer le fond d'un lien |
| `a:focus-visible` | l'élément a le focus **clavier** | contour bien visible |
| `.bouton:active` | on est en train de cliquer | le bouton s'enfonce |
| `.carte:focus-within` | un élément **à l'intérieur** a le focus | soulever la carte au clavier |
| `.carte:target` | l'`id` de l'élément est dans l'adresse (`page.html#piment`) | surligner la section visée |
| `details[open]` | l'élément a l'attribut `open` | accordéon ouvert |

| Propriété | Exemple | À retenir |
|---|---|---|
| `transition` | `transition: transform 0.3s ease;` | propriété animée, durée, rythme. Se place sur l'état **normal** : elle joue à l'aller **et** au retour. |
| `transform` | `translateY(-6px)`, `scale(1.1)`, `rotate(45deg)` | déplace, agrandit ou tourne l'élément **sans bousculer** ses voisins. |
| `@keyframes` + `animation` | `@keyframes surligner { from { … } to { … } }` puis `animation: surligner 1.5s ease-out;` | une animation qui se joue toute seule (ici, une fois). |
| `::after` | `summary::after { content: "+"; }` | ajoute un petit élément **décoratif** à la fin ; `content` est obligatoire. |
| `scroll-behavior` | `html { scroll-behavior: smooth; }` | défilement doux vers les ancres. |

## Critères de réussite

- [ ] Les liens du sommaire et le bouton changent d'aspect au survol, **en douceur**.
- [ ] Le bouton s'enfonce légèrement pendant le clic.
- [ ] En naviguant avec Tab, je vois **toujours** où est le focus (aucun `outline: none` sans remplacement).
- [ ] Les cartes se soulèvent au survol **et** quand leur lien a le focus clavier.
- [ ] L'image zoome au survol sans sortir de son cadre.
- [ ] Le clic sur le sommaire fait défiler la page en douceur, et la carte visée est encadrée et brièvement surlignée.
- [ ] La FAQ affiche une main au survol, un « + » qui devient « × » à l'ouverture, et s'utilise au clavier (Espace / Entrée).
- [ ] Avec « prefers-reduced-motion: reduce » émulé, plus rien ne bouge, mais tout fonctionne encore.
- [ ] Le validateur CSS du W3C n'affiche aucune erreur.

## Indices

<details>
<summary>Indice 1 — Ma transition ne marche que dans un sens</summary>

Vous avez sans doute écrit la `transition` dans la règle `:hover`. Elle ne s'applique alors que **pendant** le survol : à l'aller, la transition joue ; au retour, la règle `:hover` ne s'applique plus… et sa transition non plus. Placez la `transition` sur l'état **normal** de l'élément (`.carte`, `.sommaire a`…).

</details>

<details>
<summary>Indice 2 — Pourquoi <code>:focus-visible</code> plutôt que <code>:focus</code> ?</summary>

`:focus` s'applique aussi quand on **clique** à la souris sur certains éléments : beaucoup de développeurs suppriment alors le contour parce qu'ils le trouvent laid… et la page devient inutilisable au clavier. `:focus-visible` ne s'applique que lorsque le navigateur juge l'indicateur utile, en particulier pendant la navigation au **clavier**. Règle d'or : ne jamais écrire `outline: none` sans proposer un autre indicateur bien visible.

</details>

<details>
<summary>Indice 3 — La carte ne se soulève pas au clavier</summary>

Une carte `<article>` ne peut pas recevoir le focus : seul le **lien** qu'elle contient le peut. `.carte:focus` ne s'appliquera donc jamais. Il faut un sélecteur qui veut dire « la carte, quand quelque chose **à l'intérieur** a le focus ». Relisez le mémo.

</details>

<details>
<summary>Indice 4 — Mon image déborde quand elle grossit</summary>

`transform: scale(1.1)` agrandit l'image… et elle dépasse de son conteneur. C'est le **parent** (`.cadre-image`) qui doit cacher ce qui dépasse, pas l'image elle-même. Le `border-radius` du cadre arrondit alors aussi les coins de l'image.

</details>

<details>
<summary>Indice 5 — L'animation ne se rejoue pas quand je reclique</summary>

C'est normal : l'animation se joue au moment où la carte **devient** la cible. Si elle l'est déjà (l'adresse se termine déjà par `#piment`), un nouveau clic ne change rien. Cliquez sur une autre épice, puis revenez. Rechargez aussi la page avec `#piment` dans l'adresse : la carte est toujours ciblée !

</details>

## Bonus

- Le bouton jaune de l'en-tête mène à `#faq` : mettez aussi en valeur la section FAQ quand elle est ciblée (par exemple `.faq:target h2`).
- Essayez d'autres rythmes de transition : `linear`, `ease-in-out`, ou un `transition-delay` de `0.1s`. Lequel trouvez-vous le plus naturel ?
- Gardez le sommaire toujours visible en haut de l'écran avec `position: sticky; top: 0;` sur `.sommaire`. Quel réglage faut-il alors adapter pour que la carte ciblée ne soit pas cachée dessous ?
- **Pour aller plus loin** (sélecteur récent, hors programme) : `.carte:has(.retour:focus-visible)` permet de soulever la carte **seulement** pendant la navigation au clavier, et pas après un clic à la souris.

## Questions de compréhension

1. Quelle est la différence entre `:hover` et `:focus-visible` ? Pourquoi faut-il toujours prévoir les deux ?
2. Pourquoi écrit-on la `transition` sur l'état normal plutôt que sur `:hover` ?
3. `transform: translateY(-6px)` et `margin-top: -6px` font-ils la même chose ? Que deviennent les éléments voisins dans chaque cas ?
4. Qu'est-ce que la pseudo-classe `:target` ? Que voit-on dans la barre d'adresse quand elle s'applique ?
5. À quoi sert `@media (prefers-reduced-motion: reduce)` ?

## Lien avec le brief PlantEvo

Le brief demande une présentation « synoptique et **interactive** ». Sans une ligne de JavaScript, vous pouvez déjà : faire réagir les vignettes de votre menu au survol et au clavier, mettre en valeur la partie atteinte depuis le menu avec `:target`, et cacher les explications plus longues dans des `<details>` pour respecter la règle « 80 % d'images, 20 % de texte » à l'écran. Attention à ne pas en faire trop : une animation doit **aider** le visiteur (montrer où il est, ce qui est cliquable), pas le distraire.

## Ressources

- MDN : [`:hover`](https://developer.mozilla.org/fr/docs/Web/CSS/:hover) · [`:focus-visible`](https://developer.mozilla.org/fr/docs/Web/CSS/:focus-visible) · [`:focus-within`](https://developer.mozilla.org/fr/docs/Web/CSS/:focus-within) · [`:target`](https://developer.mozilla.org/fr/docs/Web/CSS/:target)
- MDN : [`transition`](https://developer.mozilla.org/fr/docs/Web/CSS/transition) · [`transform`](https://developer.mozilla.org/fr/docs/Web/CSS/transform) · [`@keyframes`](https://developer.mozilla.org/fr/docs/Web/CSS/@keyframes) · [`::after`](https://developer.mozilla.org/fr/docs/Web/CSS/::after)
- MDN : [`<details>`](https://developer.mozilla.org/fr/docs/Web/HTML/Element/details) · [`scroll-behavior`](https://developer.mozilla.org/fr/docs/Web/CSS/scroll-behavior) · [`prefers-reduced-motion`](https://developer.mozilla.org/fr/docs/Web/CSS/@media/prefers-reduced-motion)
- [Validateur CSS du W3C](https://jigsaw.w3.org/css-validator/#validate_by_input)

---

Exercice suivant : [11 — Chasse aux bugs et régime minceur](../11-debogage-optimisation/README.md)
