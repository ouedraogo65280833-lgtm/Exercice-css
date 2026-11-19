# Exercice 03 — Couleurs, polices et variables

**Niveau 1 · Graine** · ★☆☆☆ · Durée : 45 min · Notions : formats de couleur (nom, hexadécimal, `rgb()`, `hsl()`, transparence), contraste, variables CSS `--nom` / `var()`, piles de polices système, `font-size` en `rem`, `font-weight`, `font-style`, `line-height`, `text-transform`, `letter-spacing`, `text-decoration`, longueur des lignes

> La ferme-école publie son carnet de recettes. Une graphiste a préparé une **charte graphique** : six couleurs et deux polices, à respecter sur toutes les pages. Votre mission : appliquer cette charte proprement… et faire en sorte qu'on puisse la modifier en **une seule ligne** le jour où la graphiste change d'avis.

## Objectifs

- Écrire une couleur de plusieurs façons et vérifier qu'un texte est **lisible** (contraste).
- Ranger les couleurs et les polices d'une charte graphique dans des **variables CSS**.
- Choisir des polices sans aucun lien externe (piles de polices système).
- Rendre un texte agréable à lire : tailles en `rem`, interligne, longueur des lignes.

## Fichiers fournis

```
03-couleurs-polices/
├── README.md        ← cette consigne
├── index.html       ← le carnet de recettes (HTML terminé, ne pas modifier)
├── css/
│   └── style.css    ← la feuille de style, avec des TODO
└── images/
    └── banane.svg
```

## La charte graphique

| Variable à créer | Valeur | Usage |
|---|---|---|
| `--vert` | `#2e7d32` | couleur principale : grands titres `h1` et `h2` |
| `--vert-fonce` | `#1b5e20` | liens |
| `--terre` | `#6d4c41` | couleur d'accent : intertitres `h3`, informations, légendes |
| `--soleil` | `#f9a825` | décoration : encadré « Astuce » — **jamais pour du texte** |
| `--creme` | `#fffaf0` | fond de la page |
| `--texte` | `#1f2a1f` | texte courant |
| `--police-titres` | `Georgia, "Times New Roman", serif` | titres `h1` et `h2` |
| `--police-texte` | `system-ui, -apple-system, "Segoe UI", Roboto, Ubuntu, sans-serif` | tout le reste |

## Consigne

Ouvrez `index.html` avec Live Server. Les numéros correspondent aux commentaires `TODO` de `css/style.css`.

1. **Les variables.** Dans la règle `:root` (l'élément racine de la page, c'est-à-dire `<html>`), déclarez les 8 variables de la charte. Le nom d'une variable commence par **deux tirets** :

   ```css
   :root {
     --vert: #2e7d32;
     /* … les 7 autres */
   }
   ```

   Rien ne change à l'écran : pour l'instant, les variables sont déclarées mais personne ne les utilise.

2. **La page.** Dans la règle `body`, utilisez les variables avec `var()` : fond `var(--creme)`, couleur du texte `var(--texte)`, police `var(--police-texte)`. Ajoutez un interligne confortable : `line-height: 1.6;` (1,6 fois la taille du texte).
3. **Les grands titres.** Une règle pour `h1` **et** `h2` (regroupement, exercice 02) : police des titres et couleur principale.
4. **Les tailles.** `h1` à `2.5rem`, `h2` à `1.75rem`, `h3` à `1rem`.
   Pourquoi `rem` et pas `px` ? `1rem` = la taille de texte choisie par le visiteur dans son navigateur (16 px par défaut). Une personne malvoyante qui agrandit le texte de son navigateur verra tout votre site grandir avec ; en `px`, rien ne bouge.
5. **Les intertitres `h3`** (« Ingrédients », « Préparation ») : en majuscules (`text-transform: uppercase`), lettres espacées (`letter-spacing: 0.1em`), couleur `--terre`.
   Remarquez : dans le HTML, « Ingrédients » est écrit normalement. Les majuscules sont un choix de **présentation**, donc du CSS.
6. **Les informations et les légendes.** Une seule règle pour `.infos` et `figcaption` : couleur `--terre`, taille `0.9rem`, en italique (`font-style: italic`).
7. **L'encadré `.astuce`.** On veut le jaune `--soleil`, mais très pâle, pour le fond. Écrivez-le au format `rgb()` avec une **transparence** de 20 % (voir le mémo) :

   ```css
   background-color: rgb(249 168 37 / 0.2);
   ```

   Ajoutez une barre à gauche `border-left: 4px solid var(--soleil);` et `padding: 0.75rem 1rem;` (`border` et `padding` : exercice 04).
8. **Les liens** : couleur `--vert-fonce`, en gras, et un soulignement couleur soleil : `text-decoration-color: var(--soleil);`.
9. **La longueur des lignes.** À 1280 px de large, une ligne de texte fait plus de 150 caractères : l'œil se perd en revenant à la ligne suivante. On lit mieux avec **50 à 75 caractères par ligne**. Écrivez une règle pour `header`, `main` et `footer` :

   ```css
   max-width: 70ch;   /* 70 fois la largeur du caractère « 0 » */
   margin: 0 auto;    /* centre la colonne (expliqué à l'exercice 04) */
   ```

10. **Le contraste.** Ouvrez F12 et inspectez un paragraphe. Dans le panneau *Styles*, cliquez sur le petit carré de couleur à côté de `color` : Chrome affiche le **ratio de contraste** (*Contrast ratio*) entre le texte et le fond. Il faut **au moins 4,5** pour un texte normal (une coche ✓ s'affiche).
    - Notez le ratio du texte courant et celui des liens.
    - **Expérience** : donnez provisoirement la couleur `var(--soleil)` aux `h3`. Quel ratio ? Le texte est-il lisible sur un vidéoprojecteur ? Remettez `var(--terre)`. Vous comprenez maintenant pourquoi la charte dit « jamais pour du texte » !
11. **Expérience — le pouvoir des variables.** Dans `:root`, remplacez la valeur de `--vert` par `#8e24aa` (violet) : **tous** les titres changent d'un coup. Essayez aussi `--police-titres: "Courier New", monospace;`. Remettez ensuite les valeurs de la charte.

Pour finir, passez votre feuille au [validateur CSS du W3C](https://jigsaw.w3.org/css-validator/#validate_by_input) : objectif **0 erreur**.

### Mémo — Écrire une couleur

| Format | Le vert de la charte | À savoir |
|---|---|---|
| Nom | `green` | environ 140 noms prédéfinis ; pratique pour tester, peu précis |
| Hexadécimal | `#2e7d32` | le plus courant : rouge `2e`, vert `7d`, bleu `32`, chacun de `00` à `ff` |
| `rgb()` | `rgb(46 125 50)` | rouge, vert, bleu de 0 à 255 (ancienne écriture : `rgb(46, 125, 50)`) |
| `rgb()` + transparence | `rgb(46 125 50 / 0.2)` | après la barre : opacité de `0` (invisible) à `1` (opaque) |
| `hsl()` | `hsl(123 46% 34%)` | teinte (0 à 360°), saturation, luminosité : facile pour éclaircir ou foncer une couleur |

### Mémo — Mettre en forme le texte

| Propriété | Exemple | Effet |
|---|---|---|
| `font-family` | `var(--police-texte)` | la police (avec des polices de secours) |
| `font-size` | `1.75rem` | la taille |
| `font-weight` | `bold` ou `700` | la graisse (gras) |
| `font-style` | `italic` | l'italique |
| `line-height` | `1.6` | l'interligne (sans unité : multiple de la taille du texte) |
| `text-transform` | `uppercase` | majuscules à l'affichage |
| `letter-spacing` | `0.1em` | l'espace entre les lettres |
| `text-decoration` | `none`, `underline` | le soulignement |
| `text-align` | `center` | l'alignement |

### Pourquoi pas une police Google Fonts ?

Une police Google Fonts, c'est un **lien vers un serveur externe** et un ou plusieurs fichiers de police à télécharger (souvent 20 à 100 Ko chacun) avant que le texte ne s'affiche correctement. Le brief demande de **minimiser les liens externes** : une pile de polices système s'affiche instantanément, sans rien télécharger, et reste très lisible.

## Critères de réussite

- [ ] Les 8 variables de la charte sont déclarées dans `:root`.
- [ ] Aucun code couleur ni nom de police n'apparaît en dehors de `:root`, sauf le `rgb(… / 0.2)` de l'encadré.
- [ ] Les tailles de texte sont en `rem` (aucune en `px`).
- [ ] Les intertitres `h3` s'affichent en majuscules alors qu'ils sont écrits normalement dans le HTML.
- [ ] Le texte occupe une colonne centrée et lisible, même sur un grand écran.
- [ ] Le ratio de contraste du texte courant et des liens est d'au moins 4,5 (vérifié dans F12).
- [ ] En changeant **une seule** valeur dans `:root`, j'ai changé la couleur de tous les titres.
- [ ] La page n'utilise aucune ressource externe (pas de lien vers des polices en ligne).
- [ ] Le validateur CSS du W3C n'affiche aucune erreur.

## Indices

<details>
<summary>Indice 1 — Comment utiliser une variable ?</summary>

On la **déclare** une fois (avec deux tirets), on l'**utilise** autant qu'on veut avec `var()` :

```css
:root {
  --rouge: #b71c1c;
}

.alerte {
  color: var(--rouge);
}
```

Erreurs fréquentes : `var(rouge)` (tirets oubliés), `color: --rouge;` (`var()` oublié), `var(--Rouge)` (les majuscules comptent).

</details>

<details>
<summary>Indice 2 — Ma variable ne marche pas</summary>

- Est-elle bien déclarée **dans** les accolades de `:root`, avec un `;` à la fin ?
- Le nom est-il écrit exactement pareil à la déclaration et à l'utilisation ?
- Dans F12, survolez `var(--vert)` dans le panneau *Styles* : Chrome affiche la valeur de la variable, ou signale qu'elle n'est pas définie.

</details>

<details>
<summary>Indice 3 — Je ne trouve pas le ratio de contraste</summary>

Il faut inspecter un élément qui contient du **texte** (un `<p>`, un `<a>`), puis cliquer sur le **petit carré de couleur** devant la valeur de `color` dans le panneau *Styles*. Le ratio apparaît en bas du sélecteur de couleur. Dans Firefox : onglet *Accessibilité* de F12, ou l'outil en ligne [WebAIM Contrast Checker](https://webaim.org/resources/contrastchecker/).

</details>

<details>
<summary>Indice 4 — <code>rem</code>, <code>em</code>, <code>px</code> : lequel choisir ?</summary>

- `px` : taille fixe, qui ignore les réglages du visiteur. À réserver aux bordures.
- `rem` : relatif à la taille de base de la page. Le plus simple et le plus prévisible pour les tailles de texte.
- `em` : relatif à la taille du texte de l'élément lui-même. Pratique pour `letter-spacing` (l'espacement suit la taille de la lettre).

</details>

## Bonus

- Ajoutez une variable `--vert-clair` en `hsl()` en gardant la teinte et la saturation du vert, mais avec une luminosité de 94 % : `hsl(123 46% 94%)`. Utilisez-la comme fond pour la `figure`.
- Créez une **autre** charte (par exemple « Le carnet du pêcheur », en bleus) en ne modifiant **que** les valeurs des variables. Vérifiez les contrastes !
- Générez une palette avec un outil comme [Coolors](https://coolors.co/) et testez-la sur la page.

## Questions de compréhension

1. Écrivez le blanc de trois façons différentes.
2. Quel est l'intérêt des variables CSS ? Donnez un exemple concret.
3. Pourquoi une pile de polices contient-elle plusieurs noms, et pourquoi se termine-t-elle par `serif` ou `sans-serif` ?
4. Pourquoi préférer `rem` à `px` pour les tailles de texte ?
5. Qu'est-ce que le ratio de contraste et quelle valeur minimale viser pour un texte normal ?

## Lien avec le brief PlantEvo

Le jury évalue la **créativité** et la **convivialité** de votre site : une charte de 4 à 6 couleurs bien contrastées et une ou deux polices suffisent à donner une identité à PlantEvo (pourquoi pas des verts pour les végétaux et des bruns pour la terre ?). Rangées dans des variables, elles se modifient en une ligne. Et en utilisant des polices système, vous respectez le critère « **minimiser le nombre de liens externes** ». Pensez enfin que votre site sera montré sur un vidéoprojecteur lors de la soutenance : un bon contraste n'est pas un luxe.

## Ressources

- [MDN — Valeurs de couleur](https://developer.mozilla.org/fr/docs/Web/CSS/color_value)
- [MDN — Utiliser les variables CSS (propriétés personnalisées)](https://developer.mozilla.org/fr/docs/Web/CSS/Using_CSS_custom_properties)
- [MDN — Mise en forme fondamentale du texte](https://developer.mozilla.org/fr/docs/Learn/CSS/Styling_text/Fundamentals)
- MDN : [`font-family`](https://developer.mozilla.org/fr/docs/Web/CSS/font-family) · [`line-height`](https://developer.mozilla.org/fr/docs/Web/CSS/line-height) · [`text-transform`](https://developer.mozilla.org/fr/docs/Web/CSS/text-transform) · [`letter-spacing`](https://developer.mozilla.org/fr/docs/Web/CSS/letter-spacing)
- [WebAIM Contrast Checker](https://webaim.org/resources/contrastchecker/)
- [Validateur CSS du W3C (saisie directe)](https://jigsaw.w3.org/css-validator/#validate_by_input)

---

Exercice suivant : [04 — Le modèle de boîte](../04-modele-de-boite/README.md)
