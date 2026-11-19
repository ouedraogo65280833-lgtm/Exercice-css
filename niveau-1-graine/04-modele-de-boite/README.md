# Exercice 04 — Le modèle de boîte

**Niveau 1 · Graine** · ★☆☆☆ · Durée : 45 min · Notions : `width`, `max-width`, `padding`, `border`, `margin`, `margin: 0 auto`, `box-sizing`, `display: block | inline | inline-block`, `border-radius`, `box-shadow`, propriétés raccourcies, fusion des marges

> La coopérative vend ses sachets de graines au marché, et maintenant sur son site. La page a déjà ses couleurs et ses polices… mais tout est collé : le texte touche les bords, les sachets se suivent sans séparation, et sur téléphone les images dépassent de l'écran. Votre mission : donner de l'**espace** et de la **forme** à chaque bloc.

## Objectifs

- Comprendre qu'en CSS, **chaque élément est une boîte** : contenu, marge intérieure, bordure, marge extérieure.
- Espacer et encadrer des blocs avec `padding`, `border` et `margin`.
- Centrer une colonne de contenu avec `max-width` et `margin: 0 auto`.
- Calculer la largeur réelle d'une boîte et la simplifier avec `box-sizing: border-box`.
- Connaître la différence entre les éléments `block`, `inline` et `inline-block`.

## Fichiers fournis

```
04-modele-de-boite/
├── README.md        ← cette consigne
├── index.html       ← la boutique de graines (HTML terminé, ne pas modifier)
├── css/
│   └── style.css    ← couleurs et polices déjà faites + TODO
└── images/
    └── tomate.svg  piment.svg  mais.svg  carotte.svg
```

## Le modèle de boîte

```
┌───────────────── margin (marge extérieure, transparente) ─────────────────┐
│   ┌───────────────────────── border (bordure) ─────────────────────────┐  │
│   │   ┌─────────────── padding (marge intérieure) ──────────────────┐  │  │
│   │   │                                                             │  │  │
│   │   │                 contenu (width × height)                    │  │  │
│   │   │                                                             │  │  │
│   │   └─────────────────────────────────────────────────────────────┘  │  │
│   └────────────────────────────────────────────────────────────────────┘  │
└───────────────────────────────────────────────────────────────────────────┘
```

Le **fond** (`background-color`) remplit le contenu **et** le padding, jamais la margin.

## Consigne

**Étape 0 — Observer (5 min).** Ouvrez `index.html` avec Live Server, puis F12. Inspectez le premier `<article class="sachet">` et ouvrez l'onglet **Calculé** (*Computed*) : le schéma coloré montre les 4 couches de sa boîte. Survolez chaque couche : elle s'illumine dans la page. Inspectez aussi le `<body>` : il a déjà une `margin` de 8 px, ajoutée par le navigateur.

Les numéros ci-dessous correspondent aux commentaires `TODO` de `css/style.css`.

1. **La page.** Supprimez la marge par défaut du `body` avec `margin: 0;` : la fine bande autour de la page disparaît.
2. **L'en-tête.** Pour `header` : fond `var(--vert-clair)`, une bordure seulement en bas `border-bottom: 4px solid var(--vert);`, une marge intérieure `padding: 2rem 1rem;` (2rem en haut et en bas, 1rem à gauche et à droite), un espace sous l'en-tête `margin-bottom: 2rem;` et le texte centré.
3. **La colonne centrale.** Pour `main` :
   - `max-width: 40rem;` : la colonne ne dépasse jamais 40rem (640 px), mais peut être plus étroite sur un téléphone ;
   - `margin: 0 auto;` : 0 en haut et en bas, et **auto** à gauche et à droite : le navigateur partage l'espace restant en deux parts égales → la colonne est **centrée** ;
   - `padding: 0 1rem;` : sur un petit écran, le texte ne touche pas les bords.
4. **Les cartes.** Chaque `.sachet` devient une carte : fond blanc, bordure `2px solid var(--bordure)`, coins arrondis `border-radius: 12px;`, marge intérieure de `1.5rem` et `2rem` d'espace sous chaque carte. Regardez à nouveau le schéma de l'onglet *Calculé*.
5. **Le calcul de la boîte.** Ajoutez **provisoirement** `width: 300px;` à `.sachet`.
   - **Prédisez** sur papier la largeur réelle d'une carte à l'écran, sachant que `1.5rem` = 24 px : 300 + … ?
   - Vérifiez : survolez la carte dans l'onglet *Éléments* de F12, une bulle affiche ses dimensions.
   - Par défaut (`box-sizing: content-box`), `width` ne règle que le **contenu** : le padding et la bordure s'ajoutent autour. C'est un piège classique ! Écrivez **tout en haut** du fichier (`TODO 5`) la règle que presque tous les sites utilisent :

     ```css
     *,
     *::before,
     *::after {
       box-sizing: border-box;
     }
     ```

   - Vérifiez à nouveau : la carte fait maintenant **exactement** 300 px, padding et bordure compris. Supprimez ensuite le `width: 300px;` provisoire.
6. **Les images.** Réduisez la fenêtre (ou passez en mode téléphone avec `Ctrl + Maj + M` dans F12) : à 375 px de large, les images de 400 px **dépassent** des cartes. Écrivez une règle `.sachet img` :
   - `max-width: 100%;` et `height: auto;` : l'image ne dépasse jamais de sa boîte et garde ses proportions ;
   - `display: block;` puis `margin: 0 auto 1rem;` : l'image est centrée, avec 1rem d'espace en dessous ;
   - `border-radius: 8px;` pour adoucir les coins.

   Pourquoi `display: block` ? Une image est un élément **en ligne** (*inline*) : elle se place dans le texte comme un mot, et `margin: auto` n'a aucun effet sur elle. Devenue un **bloc**, elle peut être centrée.
7. **Le badge.** Pour `.badge` (le `<span>` « Saison sèche », « Facile »…), écrivez d'abord cette version, volontairement exagérée :

   ```css
   .badge {
     background-color: var(--soleil);
     border-radius: 999px;
     padding: 0.6rem 0.75rem;
     margin: 1rem;
   }
   ```

   Réduisez la fenêtre pour que le paragraphe tienne sur plusieurs lignes, puis observez : le fond jaune **déborde** sur les lignes voisines, et la marge du haut et du bas **n'a aucun effet**. Un `<span>` est un élément `inline` : ses marges et paddings verticaux ne repoussent pas les lignes.
   Ajoutez `display: inline-block;` : le badge reste dans la ligne, mais se comporte comme une vraie boîte. Enfin, remplacez les valeurs exagérées par les valeurs définitives : `padding: 0.2rem 0.75rem;`, `margin-right: 0.5rem;` (à la place de `margin: 1rem;`), texte en `0.8rem`, en gras et en majuscules.
8. **L'ombre.** Ajoutez à la règle `.sachet` une ombre légère : `box-shadow: 0 4px 12px rgb(0 0 0 / 0.08);` (décalage horizontal, décalage vertical, flou, couleur à 8 % d'opacité).
9. **Le pied de page.** Pour `footer` : `3rem` d'espace au-dessus, une marge intérieure `1.5rem 1rem`, une bordure en haut `2px solid var(--bordure)`, le texte centré en `0.9rem`.
10. **Expérience — la fusion des marges.** Ajoutez provisoirement `margin-top: 2rem;` à `.sachet`. L'espace **entre** deux cartes passe-t-il à 4rem ? Non ! Quand deux marges verticales se touchent, elles **fusionnent** : seule la plus grande compte. Vérifiez dans F12, puis supprimez cette ligne.

Pour finir, passez votre feuille au [validateur CSS du W3C](https://jigsaw.w3.org/css-validator/#validate_by_input) : objectif **0 erreur**.

### Mémo — Les propriétés de la boîte

| Propriété | Exemple | Rôle |
|---|---|---|
| `width` / `max-width` | `max-width: 40rem;` | largeur (fixe) / largeur **maximale** (plus souple) |
| `padding` | `padding: 1.5rem;` | marge **intérieure** : le fond la remplit |
| `border` | `border: 2px solid #e0d6cc;` | bordure : épaisseur, style (`solid`, `dashed`, `dotted`), couleur |
| `margin` | `margin: 0 auto;` | marge **extérieure** : toujours transparente |
| `box-sizing` | `box-sizing: border-box;` | `width` inclut le padding et la bordure |
| `border-radius` | `border-radius: 12px;` | coins arrondis (`999px` : forme de pilule, `50%` : cercle) |
| `box-shadow` | `box-shadow: 0 4px 12px rgb(0 0 0 / 0.08);` | ombre portée |

### Mémo — Les raccourcis (sens des aiguilles d'une montre)

| Écriture | Signifie |
|---|---|
| `margin: 1rem;` | 1rem sur les 4 côtés |
| `margin: 1rem 2rem;` | 1rem en haut et en bas · 2rem à droite et à gauche |
| `margin: 0 auto 1rem;` | 0 en haut · auto à droite et à gauche · 1rem en bas |
| `margin: 1rem 2rem 3rem 4rem;` | haut · droite · bas · gauche (moyen mnémotechnique : « **TRouBLe** », *Top Right Bottom Left*) |
| `margin-top`, `margin-right`, `margin-bottom`, `margin-left` | un seul côté (idem pour `padding-…` et `border-…`) |

### Mémo — `display`

| Valeur | Comportement | Exemples par défaut |
|---|---|---|
| `block` | prend toute la largeur disponible, commence sur une nouvelle ligne ; accepte `width`, marges et paddings | `<p>`, `<h1>`, `<article>`, `<ul>`, `<header>` |
| `inline` | se place dans le texte comme un mot ; ignore `width`, `height` et les marges verticales | `<span>`, `<a>`, `<strong>`, `<img>` |
| `inline-block` | se place dans le texte, **mais** se comporte comme une boîte complète | (à choisir soi-même : badges, boutons) |

## Critères de réussite

- [ ] Il n'y a plus de bande blanche autour de la page : l'en-tête occupe toute la largeur.
- [ ] Le contenu forme une colonne centrée de 40rem au maximum ; sur téléphone, le texte ne touche pas les bords.
- [ ] Chaque sachet est une carte : fond blanc, bordure, coins arrondis, marge intérieure, ombre légère, espace entre les cartes.
- [ ] J'ai prédit puis vérifié dans F12 la largeur réelle d'une carte en `content-box` et en `border-box`.
- [ ] La règle `box-sizing: border-box` est en haut du fichier.
- [ ] Les images sont centrées dans leur carte et ne dépassent jamais, même à 375 px de large.
- [ ] Les badges ne débordent plus sur les lignes voisines.
- [ ] J'utilise des propriétés raccourcies (`margin: 0 auto`, `padding: 2rem 1rem`…).
- [ ] Le validateur CSS du W3C n'affiche aucune erreur.

## Indices

<details>
<summary>Indice 1 — <code>margin: 0 auto</code> ne centre pas mon élément</summary>

Deux conditions pour que les marges `auto` centrent un élément :
- il doit être un **bloc** (`display: block`) : une image ou un `<span>` sont `inline` par défaut ;
- il doit être **moins large** que son parent : sans `width` ou `max-width`, un bloc prend déjà toute la largeur, il n'y a rien à partager.

</details>

<details>
<summary>Indice 2 — <code>padding</code> ou <code>margin</code> ?</summary>

Posez-vous la question : « l'espace doit-il être **dans** la boîte (coloré par le fond, à l'intérieur de la bordure) ou **entre** deux boîtes ? »
- Dans la boîte → `padding` (l'espace entre le texte d'une carte et sa bordure).
- Entre les boîtes → `margin` (l'espace entre deux cartes).

</details>

<details>
<summary>Indice 3 — Comment tester une valeur sans modifier mon fichier ?</summary>

Dans l'onglet *Calculé* de F12, double-cliquez sur un nombre du schéma de la boîte (padding, margin…) pour le modifier en direct. Dans le panneau *Styles*, cliquez sur une valeur et utilisez les flèches ↑ et ↓ du clavier pour l'augmenter ou la diminuer. Quand le résultat vous plaît, recopiez la valeur dans VS Code.

</details>

<details>
<summary>Indice 4 — Je ne vois pas où commence et où finit chaque boîte</summary>

Ajoutez provisoirement, à la fin de votre feuille, cette règle qui dessine le contour de **tous** les éléments :

```css
* {
  outline: 1px solid red;
}
```

`outline` dessine un contour qui ne prend aucune place (contrairement à `border`). Pensez à la supprimer ensuite !

</details>

## Bonus

- Donnez une couleur de badge différente selon la saison : ajoutez une deuxième classe (`class="badge pluies"`) et une règle `.pluies` avec un fond bleu clair. (Pensez au contraste du texte !)
- Testez `border-radius: 50%;` sur les images : sur une image carrée, on obtient un cercle ; et sur nos images 4:3 ?
- Remplacez la bordure des cartes par une seule bordure épaisse à gauche, couleur `--vert`. Quel style préférez-vous ?

## Questions de compréhension

1. Citez les quatre couches d'une boîte, de l'intérieur vers l'extérieur.
2. Quelle différence entre `padding` et `margin` ? Laquelle est colorée par le fond ?
3. Une boîte a `width: 200px`, `padding: 10px` et `border: 5px solid`. Quelle est sa largeur à l'écran en `content-box` ? Et en `border-box` ?
4. Quelle différence entre un élément `block`, `inline` et `inline-block` ? Donnez un exemple de chaque.
5. Comment centrer horizontalement un bloc ? Que faut-il pour que ça marche ?

## Lien avec le brief PlantEvo

Chaque type de végétal de votre site PlantEvo peut être présenté dans une **carte** : image, titre, court texte — exactement comme les sachets de graines. Une colonne centrée avec `max-width`, des espacements réguliers et des images qui ne dépassent jamais (`max-width: 100%`) rendent la règle « 80 % d'images » agréable à regarder, sur ordinateur comme sur téléphone (« web **mobile** », compétence C3N1).

## Ressources

- [MDN — Le modèle de boîte](https://developer.mozilla.org/fr/docs/Learn/CSS/Building_blocks/The_box_model)
- MDN : [`box-sizing`](https://developer.mozilla.org/fr/docs/Web/CSS/box-sizing) · [`margin`](https://developer.mozilla.org/fr/docs/Web/CSS/margin) · [`padding`](https://developer.mozilla.org/fr/docs/Web/CSS/padding) · [`border`](https://developer.mozilla.org/fr/docs/Web/CSS/border) · [`display`](https://developer.mozilla.org/fr/docs/Web/CSS/display) · [`box-shadow`](https://developer.mozilla.org/fr/docs/Web/CSS/box-shadow)
- [MDN — La fusion des marges](https://developer.mozilla.org/fr/docs/Web/CSS/CSS_box_model/Mastering_margin_collapsing)
- [Validateur CSS du W3C (saisie directe)](https://jigsaw.w3.org/css-validator/#validate_by_input)

---

Exercice suivant : [05 — Un menu avec Flexbox](../../niveau-2-pousse/05-menu-flexbox/README.md)
