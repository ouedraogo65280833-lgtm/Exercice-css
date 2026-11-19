# Exercice 01 — Ma première feuille de style

**Niveau 1 · Graine** · ★☆☆☆ · Durée : 30 min · Notions : syntaxe d'une règle CSS, attribut `style`, balise `<style>`, `<link rel="stylesheet">`, sélecteurs de balise, `color`, `background-color`, `font-family`, `font-size`, `text-align`, commentaires `/* */`

> Le potager de l'école a publié sa fiche sur le manioc. Le contenu est juste… mais la page est bien terne : noir sur blanc, police Times, liens bleus soulignés. Votre mission : lui donner des couleurs, avec **un seul fichier CSS** pour toutes les pages du site.

## Objectifs

- Comprendre le rôle du CSS : le HTML dit **ce qu'est** le contenu, le CSS dit **à quoi il ressemble**.
- Écrire une règle CSS correcte : sélecteur, accolades, `propriété: valeur;`.
- Connaître les trois façons d'ajouter du CSS et savoir pourquoi on choisit le **fichier externe**.
- Relier une feuille de style à plusieurs pages.
- Utiliser les outils de développement du navigateur (panneau *Styles*, onglet *Réseau*).

## Fichiers fournis

```
01-premiere-feuille-de-style/
├── README.md        ← cette consigne
├── index.html       ← la fiche du manioc (HTML terminé, aucun style)
├── recettes.html    ← une 2e page du même site
└── images/
    └── manioc.svg
```

Pas de fichier CSS : c'est vous qui allez le créer.

## Consigne

**Étape 0 — Observer (2 min).** Ouvrez `index.html` avec Live Server. La page s'affiche avec les **styles par défaut du navigateur** : titres en gras, liens bleus soulignés, marges autour des paragraphes… Même sans CSS de votre part, le navigateur en applique déjà un peu !

Les numéros ci-dessous correspondent aux commentaires `TODO` des fichiers.

### Méthode 1 — L'attribut `style`

1. Dans `index.html`, ajoutez un attribut `style` au `<h1>` :

   ```html
   <h1 style="color: green;">Le manioc</h1>
   ```

   Enregistrez et regardez le résultat. Ça marche… mais imaginez devoir l'écrire sur **chaque** titre de **chaque** page !

### Méthode 2 — La balise `<style>`

2. Supprimez l'attribut `style` du `<h1>`. Dans le `<head>`, juste après le `<title>`, ajoutez une balise `<style>` qui contient votre **première règle CSS** :

   ```html
   <style>
     h1 {
       color: green;
     }
   </style>
   ```

   Le titre est toujours vert. Cette fois, la règle vise **tous** les `<h1>` de la page. Mais la page `recettes.html`, elle, n'en profite pas.

### Méthode 3 — Le fichier externe (la bonne méthode)

3. Créez un dossier `css` dans le dossier de l'exercice, puis un fichier `style.css` dedans. Déplacez votre règle dans ce fichier **sans** les balises `<style>` (un fichier `.css` ne contient que du CSS). Supprimez la balise `<style>` devenue vide, et reliez la page à la feuille de style en ajoutant dans le `<head>` :

   ```html
   <link rel="stylesheet" href="css/style.css">
   ```

   Enregistrez les **deux** fichiers : le titre doit toujours être vert.

4. Complétez `css/style.css` pour obtenir l'habillage ci-dessous. Une règle par ligne du tableau, une déclaration par ligne de code :

   | Sélecteur | Ce que vous devez obtenir | Propriétés à utiliser |
   |---|---|---|
   | `body` | fond crème `#fffaf0`, texte vert très foncé `#1f2a1f`, police sans empattement (voir ci-dessous) | `background-color`, `color`, `font-family` |
   | `header` | texte centré | `text-align` |
   | `h1` | vert `#2e7d32` (remplace `green`), grande taille : `2.5rem` | `color`, `font-size` |
   | `h2` | brun « terre » `#6d4c41`, police avec empattement : `Georgia, "Times New Roman", serif` | `color`, `font-family` |
   | `a` | vert foncé `#1b5e20`, en gras (`bold`) | `color`, `font-weight` |
   | `footer` | texte centré et plus petit : `0.9rem` | `text-align`, `font-size` |

   Pour le `body`, utilisez cette **pile de polices** : le navigateur prend la première qui existe sur l'ordinateur du visiteur.

   ```css
   font-family: system-ui, -apple-system, "Segoe UI", Roboto, Ubuntu, sans-serif;
   ```

   > `#2e7d32` est un code couleur **hexadécimal** (on en reparle à l'exercice 03). `1rem` correspond à la taille de base du texte (16 px en général) : `2.5rem` vaut donc 2,5 fois cette taille.

5. **Commentez** votre feuille de style : un commentaire en haut du fichier (à quoi sert-il, quelles pages l'utilisent), puis un commentaire avant chaque groupe de règles. En CSS, un commentaire s'écrit `/* comme ceci */` (et non `<!-- … -->` comme en HTML).

6. Ouvrez `recettes.html` et reliez-la à **la même** feuille de style (`TODO 6`). Sans rien écrire de plus, la page des recettes prend le même habillage. Cliquez sur les liens pour passer d'une page à l'autre : le site est cohérent.

### Les outils de développement

7. Sur `index.html`, faites un clic droit sur le titre → **Inspecter** (ou `F12`).
   - Dans le panneau **Styles** (à droite ou en bas), retrouvez votre règle `h1` et le nom du fichier `style.css` avec son numéro de ligne.
   - Décochez la case devant `color` : que se passe-t-il ? Recochez-la.
   - Cliquez sur le petit carré de couleur et choisissez une autre couleur : la page change en direct.
   - Rechargez la page (`F5`) : la couleur d'origine revient. **Les changements faits dans F12 ne sont jamais enregistrés** : c'est un terrain d'essai, la vraie modification se fait dans VS Code.

8. **Expérience — le chemin cassé.** Dans le `<link>` de `index.html`, remplacez `css/style.css` par `css/styles.css` (avec un « s » de trop) et enregistrez.
   - La page perd tout son style. Ouvrez F12 → onglet **Réseau** (*Network*), puis rechargez la page (`F5`) : une ligne `styles.css` apparaît en rouge avec le code **404** (fichier introuvable).
   - Corrigez le chemin. Retenez ce réflexe : *« plus aucun style ? → onglet Réseau → 404 ? »*

Pour finir, vérifiez votre feuille de style avec le [validateur CSS du W3C](https://jigsaw.w3.org/css-validator/#validate_by_input) (copiez-collez le contenu de `style.css`) : objectif **0 erreur**.

### Mémo — Anatomie d'une règle CSS

```css
h2 {                   /* sélecteur : QUELS éléments on habille           */
  color: #6d4c41;      /* déclaration = propriété: valeur;                */
  text-align: center;  /* une déclaration par ligne, terminée par « ; »   */
}                      /* les accolades { } entourent les déclarations    */
```

| Méthode | Où l'écrire ? | Avantage | Inconvénient |
|---|---|---|---|
| Attribut `style` | sur une balise : `<h1 style="…">` | rapide pour un test | à répéter sur chaque balise ; mélange le contenu et la présentation |
| Balise `<style>` | dans le `<head>` de la page | une seule fois par page | à recopier dans chaque page ; alourdit le HTML |
| **Fichier externe** `<link>` | dans un fichier `css/style.css` | **un seul fichier pour tout le site**, gardé en mémoire (cache) par le navigateur, HTML plus léger | un chemin à ne pas rater |

## Critères de réussite

- [ ] Le fichier `css/style.css` existe (dossier et fichier en minuscules).
- [ ] `index.html` et `recettes.html` contiennent `<link rel="stylesheet" href="css/style.css">` dans leur `<head>`.
- [ ] Il ne reste aucun attribut `style` ni aucune balise `<style>` dans les pages HTML.
- [ ] Les deux pages ont le même habillage : fond crème, titre principal vert et centré, sous-titres bruns, liens en gras.
- [ ] Chaque règle respecte la syntaxe : sélecteur, `{`, `propriété: valeur;`, `}`.
- [ ] La feuille de style est indentée (2 espaces) et contient au moins 3 commentaires.
- [ ] J'ai modifié une couleur en direct dans F12 et j'ai compris que ce changement n'est pas enregistré.
- [ ] J'ai provoqué puis corrigé l'erreur 404 de l'étape 8.
- [ ] Le validateur CSS du W3C n'affiche aucune erreur.

## Indices

<details>
<summary>Indice 1 — Mon CSS ne s'applique pas du tout !</summary>

Vérifiez dans l'ordre :
- Les **deux** fichiers (`.html` et `.css`) sont-ils enregistrés ? (un point blanc sur l'onglet de VS Code = non enregistré)
- La balise `<link>` est-elle bien **dans le `<head>`** ?
- Le chemin est-il exact ? Le fichier `style.css` doit être dans un dossier `css` placé **à côté** de `index.html`. Attention aux majuscules et aux fautes de frappe.
- Le fichier ne s'appelle-t-il pas `style.css.txt` ? (affichez les extensions de fichiers dans votre explorateur)
- Onglet **Réseau** de F12 : le fichier CSS est-il en 404 ?

</details>

<details>
<summary>Indice 2 — Faut-il écrire <code>&lt;style&gt;</code> dans le fichier <code>.css</code> ?</summary>

Non ! Les balises `<style>` et `</style>` sont du **HTML** : elles servent seulement à glisser du CSS dans une page HTML. Un fichier `.css` commence directement par la première règle (ou par un commentaire).

</details>

<details>
<summary>Indice 3 — Une seule déclaration ne marche pas</summary>

- Les noms de propriétés sont en **anglais** : `color` et non `couleur`, `background-color` et non `background-colour`.
- Entre la propriété et la valeur : deux-points `:`. À la fin de la déclaration : point-virgule `;`. Un `;` oublié peut annuler la déclaration **suivante**.
- Dans F12, une déclaration invalide apparaît **barrée**, avec un petit triangle d'avertissement.

</details>

<details>
<summary>Indice 4 — Pourquoi mon pied de page n'est-il pas centré comme le titre ?</summary>

Chaque règle ne vise que les éléments désignés par son sélecteur. La règle `header` centre le texte de l'en-tête ; pour centrer le pied de page, il faut une règle avec le sélecteur `footer`.

</details>

## Bonus

- Ajoutez une règle `li` avec `line-height: 1.6;` pour aérer les listes. Que fait cette propriété ?
- Ouvrez le site d'un grand journal en ligne, puis F12 → **Réseau** → filtre **CSS** et rechargez : combien de fichiers CSS ? Quel poids total ?
- Créez une 3e page `conservation.html` (« Comment conserver le manioc ? »), reliée à la même feuille de style, avec un lien depuis et vers la fiche.

## Questions de compréhension

1. Quelle est la différence de rôle entre le HTML et le CSS ?
2. Citez les trois façons d'ajouter du CSS à une page. Laquelle choisir pour un site de plusieurs pages, et pourquoi ?
3. Dans `color: #2e7d32;`, quel est le nom de la propriété ? Et la valeur ? Comment s'appelle l'ensemble ?
4. Pourquoi une page « sans CSS » affiche-t-elle quand même des titres en gras et des liens bleus ?
5. Toute la mise en forme a disparu d'un coup : quelle est la cause la plus probable, et comment la vérifier ?

## Lien avec le brief PlantEvo

Votre site PlantEvo aura plusieurs pages (l'accueil + une page par type de végétal) : elles doivent **toutes** partager **un seul** fichier `css/style.css`. C'est la base de deux critères du brief : « code source correctement commenté et organisé » et « minimiser la taille du fichier CSS ». Une seule feuille de style, chargée une fois puis gardée en cache par le navigateur, c'est plus léger et plus facile à modifier que du style recopié dans chaque page.

## Ressources

- [MDN — Premiers pas avec CSS](https://developer.mozilla.org/fr/docs/Learn/CSS/First_steps/Getting_started)
- [MDN — Comment CSS est structuré](https://developer.mozilla.org/fr/docs/Learn/CSS/First_steps/How_CSS_is_structured)
- MDN : [`color`](https://developer.mozilla.org/fr/docs/Web/CSS/color) · [`background-color`](https://developer.mozilla.org/fr/docs/Web/CSS/background-color) · [`font-family`](https://developer.mozilla.org/fr/docs/Web/CSS/font-family) · [`font-size`](https://developer.mozilla.org/fr/docs/Web/CSS/font-size) · [`text-align`](https://developer.mozilla.org/fr/docs/Web/CSS/text-align)
- [Validateur CSS du W3C (saisie directe)](https://jigsaw.w3.org/css-validator/#validate_by_input)
- [Validateur HTML du W3C](https://validator.w3.org/#validate_by_input)

---

Exercice suivant : [02 — Sélecteurs, classes et cascade](../02-selecteurs-cascade/README.md)
