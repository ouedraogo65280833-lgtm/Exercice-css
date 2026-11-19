# Exercice 11 — Chasse aux bugs et régime minceur

**Niveau 3 · Arbre** · ★★★☆ · Durée : 1 h · Notions : onglet *Réseau* (erreur 404), validateur CSS du W3C, panneau *Styles* (déclarations barrées, icône ⚠), sensibilité à la casse, héritage, variables CSS, regroupement de sélecteurs, propriétés raccourcies, outil *Coverage*, minification

> Le site de « La coopérative des planteurs » a été modifié par trois stagiaires successifs. Résultat : la page s'affiche **sans aucun style**, et quand on retrouve le style, plusieurs choses clochent. Pire : la feuille de style fait **plus de 350 lignes** pour une seule petite page ! Votre mission, en deux temps : **réparer** la page (8 bugs), puis mettre la feuille de style **au régime**… sans changer un seul pixel de l'apparence.

## Objectifs

- Trouver pourquoi une feuille de style ne se charge pas (onglet *Réseau*, erreur 404).
- Utiliser le validateur CSS et le panneau *Styles* des outils de développement pour repérer les erreurs de syntaxe.
- Comprendre qu'un CSS **valide** peut quand même viser les **mauvais** éléments.
- Alléger une feuille de style : héritage, variables, regroupement, propriétés raccourcies, suppression du code mort.
- Mesurer le poids d'un fichier et produire une version **minifiée**.

## Fichiers fournis

```
11-debogage-optimisation/
├── README.md            ← cette consigne
├── index.html           ← la page (1 bug se cache ici)
├── apercu-attendu.png   ← capture de la page telle qu'elle DOIT être une fois réparée (à 1280 px)
├── css/
│   └── style.css        ← la feuille de style buggée et « obèse » (7 bugs ici)
└── images/
    └── logo.svg  cacao.svg  banane.svg  mangue.svg
```

## Consigne

### Partie A — La chasse aux bugs (25 min)

La page contient **8 bugs** : **1** dans `index.html` et **7** dans `css/style.css` :

- **1** bug empêche complètement le CSS de se charger : on le trouve avec l'onglet *Réseau*.
- **5** bugs sont des erreurs de **syntaxe** CSS : le validateur, l'icône ⚠ de F12 ou le panneau *Problèmes* de VS Code vous mettront sur la piste.
- **2** bugs ne sont **pas** des erreurs de syntaxe : le CSS est valide… mais il vise des éléments qui n'existent pas. Seule l'**inspection** de la page permet de les trouver.

1. **Observez.** Ouvrez `index.html` avec Live Server, puis ouvrez `apercu-attendu.png` à côté (glissez-le dans un onglet du navigateur). La page n'a aucun style !
2. **L'onglet Réseau.** Ouvrez les outils de développement (**F12**), onglet **Réseau** (*Network*), puis rechargez la page (`F5`). Une ligne est en **rouge** avec le code **404** (« fichier introuvable ») : quel fichier le navigateur cherche-t-il, et **où** ? Comparez avec l'endroit où il se trouve vraiment, puis corrigez `index.html`.
3. **Comparez.** La page a maintenant des couleurs… mais elle ne ressemble pas encore à l'aperçu. Notez **toutes** les différences que vous voyez (en-tête, menu, bannière, bouton, cartes, pied de page…).
4. **Le validateur CSS.** Ouvrez le [validateur CSS du W3C](https://jigsaw.w3.org/css-validator/#validate_by_input) (onglet *Saisie directe*), copiez-collez **tout** le contenu de `css/style.css` et cliquez sur **Vérifier**. Lisez la **première erreur** et son numéro de ligne, corrigez dans VS Code, recopiez, revalidez. Concentrez-vous sur les **erreurs** (les *avertissements* ne sont pas des bugs).
   En parallèle, dans F12 → **Éléments**, cliquez sur un élément mal affiché : dans le panneau **Styles**, une déclaration **barrée** accompagnée d'une icône **⚠** est une déclaration que le navigateur n'a pas comprise. Survolez l'icône pour lire la raison.
5. **Les 2 bugs invisibles.** Quand le validateur ne trouve plus d'erreur, deux problèmes restent visibles : les cartes de produits n'ont pas leur fond blanc, et le menu est une liste à puces. Faites un clic droit sur une carte → **Inspecter** : quelles règles s'appliquent à cet élément dans le panneau *Styles* ? Comparez **lettre par lettre** (majuscules comprises) l'attribut `class` ou `id` du HTML avec le sélecteur du CSS.
6. **Remplissez le rapport de bugs** ci-dessous, puis comparez votre page avec `apercu-attendu.png` : elles doivent être identiques (à la police près, qui peut varier selon votre ordinateur).

#### Mon rapport de bugs

| N° | Fichier et ligne | Problème trouvé | Ma correction | Trouvé grâce à… (Réseau / validateur / F12 Styles / inspection) |
|---|---|---|---|---|
| 1 | | | | |
| 2 | | | | |
| 3 | | | | |
| 4 | | | | |
| 5 | | | | |
| 6 | | | | |
| 7 | | | | |
| 8 | | | | |

### Partie B — Le régime minceur (35 min)

**Règle d'or :** après **chaque** étape, rechargez la page et comparez-la avec `apercu-attendu.png`. Si quelque chose a changé, annulez (`Ctrl + Z`) et réfléchissez.

7. **Mesurez avant.** Notez le nombre de lignes de `css/style.css` (numéro de la dernière ligne dans VS Code) et son poids en octets : clic droit sur le fichier dans l'explorateur de fichiers de votre ordinateur → **Propriétés** (*Lire les informations* sur Mac), ligne « Taille ». Reportez-les dans le tableau de l'étape 13.
8. **Supprimez le code mort.** Dans F12, tapez `Ctrl + Maj + P` (menu de commandes), puis `coverage` → **Show Coverage**. Dans le panneau qui s'ouvre, cliquez sur le bouton ⟳ (*recharger et enregistrer*), puis sur `style.css` dans la liste : les règles marquées en **rouge** n'ont servi à **rien** sur cette page. Supprimez :
   - les règles qui visent des éléments absents de la page (ancien carrousel, promotion de Noël, ancienne barre latérale, ancien tableau…) ;
   - le vieux code laissé en commentaire « au cas où » (c'est le rôle de Git de garder l'historique, pas de la feuille de style) ;
   - les déclarations qui ne servent à rien, comme `display: list-item; float: none;` sur des `<li>`.

   **Attention :** les règles `:hover` et `:focus-visible` apparaissent en rouge si vous n'avez pas survolé ou tabulé pendant l'enregistrement. **Ne les supprimez pas !**
9. **Profitez de l'héritage.** `font-family` et `color` sont des propriétés **héritées** : un paragraphe ou un élément de liste prend automatiquement la police et la couleur de texte de son parent. Gardez-les **une seule fois** sur `body`, puis supprimez :
   - **tous** les `font-family` répétés (combien en avez-vous supprimé ?) ;
   - les `color: #1f2a1f` répétés sur les paragraphes et les listes, et le `color` de `.pied p` (le pied de page l'a déjà).

   **Exception :** les **liens** ont leur propre couleur (bleue), donnée par le navigateur. Leur `color` n'est donc **pas** hérité : gardez les `color` écrits sur les liens (`.logo`, `#menu a`, `.bouton`, `.pied a`…).

   Les titres `h1`, `h2`, `h3` partagent une autre police : une seule règle `h1, h2, h3 { … }` suffit, avec aussi leur `line-height` et leur couleur.
10. **Créez des variables.** Avec `Ctrl + F`, comptez combien de fois `#1b5e20` est écrit dans le fichier. Créez une règle `:root { … }` avec une variable par couleur de la charte (vert, vert foncé, vert clair, vert pâle, jaune, jaune clair, crème, texte), puis remplacez chaque code couleur par `var(--…)` (`Ctrl + H` dans VS Code : remplacer tout).
11. **Regroupez les doublons.**
    - `.bouton` et `.lien-contact` ont exactement les mêmes déclarations : une seule règle avec deux sélecteurs séparés par une virgule. Idem pour leurs `:hover` et `:focus-visible`.
    - `#produits`, `.engagements` et `.contact` : trois règles identiques → une seule.
    - `h2` est défini **deux fois** dans le fichier : fusionnez.
    - Le sélecteur `body main section#produits div.grille article.produit img` est inutilement long : `.produit img` vise exactement les mêmes images.
12. **Utilisez les raccourcis et faites le ménage.**
    - `margin-top`, `margin-right`, `margin-bottom`, `margin-left` → une seule propriété `margin` (même chose pour `padding`) ;
    - `border-width` + `border-style` + `border-color` → `border` ; les quatre `border-…-radius` → `border-radius` ;
    - `0px` → `0` (zéro n'a pas besoin d'unité) ;
    - supprimez les `!important`. Si la couleur des prix change, c'est qu'une autre règle était plus **spécifique** : l'étape 9 aurait dû la faire disparaître… vérifiez !
13. **Mesurez après, puis minifiez.**
    - Validez de nouveau (0 erreur), comparez avec l'aperçu, mesurez le nouveau poids.
    - **Minifiez** : copiez tout votre CSS dans un outil de minification (par exemple [Toptal CSS Minifier](https://www.toptal.com/developers/cssminifier)) ou utilisez une extension VS Code comme *MinifyAll*. Enregistrez le résultat dans un **nouveau** fichier `css/style.min.css` : gardez `style.css` pour travailler !
    - Dans `index.html`, faites pointer le `<link>` vers `css/style.min.css`, avec un commentaire qui explique pourquoi. Vérifiez que la page n'a pas changé, puis mesurez.

    | Version | Lignes | Poids (octets) | Gain par rapport au départ |
    |---|---|---|---|
    | Départ (`style.css` buggé) | | | — |
    | Après le régime (`style.css`) | | | … % |
    | Minifiée (`style.min.css`) | | | … % |

    Calcul du gain : `(poids de départ − nouveau poids) ÷ poids de départ × 100`.

### Mémo — les 6 règles du régime

| Technique | Avant | Après |
|---|---|---|
| **Héritage** | `font-family` répété sur `p`, `li`, `a`… | une seule fois sur `body` (attention : la **couleur** des liens, elle, ne s'hérite pas) |
| **Variables** | `#1b5e20` écrit 8 fois | `--vert-fonce: #1b5e20;` dans `:root`, puis `var(--vert-fonce)` |
| **Regroupement** | deux règles identiques `.a { … }` et `.b { … }` | `.a, .b { … }` |
| **Raccourcis** | `margin-top: 0; margin-right: auto; margin-bottom: 0; margin-left: auto;` | `margin: 0 auto;` |
| **Code mort** | règles qui ne visent rien, code en commentaire | supprimés |
| **Minification** | espaces, retours à la ligne, commentaires | tout sur une ligne, dans `style.min.css` |

Rappel des raccourcis à 4 valeurs : `margin: haut droite bas gauche;` (sens des aiguilles d'une montre) ; 2 valeurs : `margin: haut-et-bas gauche-et-droite;` ; 3 valeurs : `margin: haut gauche-et-droite bas;`.

## Critères de réussite

- [ ] Mon rapport de bugs contient les 8 bugs, avec le fichier, la ligne, la correction et l'outil qui m'a permis de le trouver.
- [ ] La page est identique à `apercu-attendu.png`, et le validateur CSS n'affiche aucune erreur.
- [ ] Chaque couleur de la charte n'est écrite **qu'une fois**, dans `:root`.
- [ ] `font-family` n'apparaît que deux fois (`body` et les titres).
- [ ] Il ne reste ni `!important`, ni code en commentaire, ni règle qui ne vise aucun élément (sauf les états `:hover` / `:focus-visible`).
- [ ] Aucune règle n'est en double, et les propriétés raccourcies sont utilisées.
- [ ] `style.css` est toujours **lisible et commenté**, et pèse au moins **30 %** de moins qu'au départ.
- [ ] `style.min.css` existe, pèse au moins **50 %** de moins que le fichier de départ, et c'est lui que la page utilise.

## Indices

<details>
<summary>Indice 1 — Comment lire un message du validateur CSS ?</summary>

Le validateur affiche le **numéro de ligne**, le **sélecteur** concerné, puis le message. Petit dictionnaire (les messages peuvent être en anglais ou en français selon la langue choisie) :

| Message | Signification |
|---|---|
| *Property X doesn't exist* / *La propriété X n'existe pas* | propriété mal orthographiée |
| *Value Error : X … is not a X value* | valeur inconnue pour cette propriété |
| *Too many values or values are not recognized* | souvent un **point-virgule oublié** : deux déclarations collées en une seule |
| *Parse Error* | erreur de structure : accolade ou deux-points manquant… |

</details>

<details>
<summary>Indice 2 — Un point-virgule oublié casse… la ligne suivante</summary>

Le point-virgule **sépare** les déclarations. Sans lui, le navigateur lit `background-color: #f9a825 padding-top: 12px` comme **une seule** valeur, incompréhensible : il ignore **les deux** déclarations. Le bug est donc à la **fin** de la ligne au-dessus de celle qui semble ne pas marcher.

</details>

<details>
<summary>Indice 3 — Une accolade oubliée</summary>

Si une règle n'est jamais fermée par `}`, les règles **suivantes** se retrouvent « à l'intérieur » d'elle et ne s'appliquent plus correctement. Le message d'erreur n'est pas toujours clair : regardez plutôt **quelles règles de la fin du fichier** ne s'appliquent pas, puis remontez. Dans VS Code, cliquez juste après une accolade ouvrante : sa partenaire fermante est surlignée… si elle existe. Le panneau **Problèmes** (`Ctrl + Maj + M`) de VS Code signale aussi ce genre d'erreur.

</details>

<details>
<summary>Indice 4 — Les 2 bugs que le validateur ne voit pas</summary>

Le validateur vérifie que votre CSS est **bien écrit**, pas qu'il vise des éléments **qui existent** dans votre HTML. Or les sélecteurs sont **sensibles à la casse** et à la moindre lettre : `.titre` ne vise pas `class="titres"`, et `#Photo` ne vise pas `id="photo"`.

</details>

<details>
<summary>Indice 5 — J'ai enlevé un <code>!important</code> et la couleur a changé</summary>

`!important` sert souvent à « forcer » une règle qui perdait contre une autre plus **spécifique** (exercice 02). Cherchez dans le panneau *Styles* quelle règle gagne maintenant. Ici, elle fixe une couleur… qui est de toute façon héritée de `body` : en la supprimant (étape 9), vous n'avez plus besoin de `!important`.

</details>

## Bonus

- Comparez deux outils de minification différents : obtenez-vous exactement le même poids ?
- Validez aussi `style.min.css` : un fichier minifié doit rester valide !
- Créez à votre tour une petite page avec **3 bugs CSS** cachés (dont un que le validateur ne voit pas), et échangez-la avec un ou une camarade.

## Questions de compréhension

1. Une page s'affiche sans **aucun** style : quelle est la cause la plus probable ? Qu'est-ce qu'une erreur **404** ?
2. Pourquoi un point-virgule oublié annule-t-il **aussi** la déclaration suivante ?
3. Pourquoi le validateur n'a-t-il pas trouvé les bugs du menu et des cartes ?
4. Qu'est-ce qu'une propriété **héritée** ? Citez-en deux qui le sont et deux qui ne le sont pas.
5. Pourquoi garde-t-on deux fichiers, `style.css` et `style.min.css` ? Lequel est publié sur le site ?

## Lien avec le brief PlantEvo

Deux critères de performance du brief sont au cœur de cet exercice : « **Minimiser la taille du fichier CSS** » et « Code source correctement **commenté et organisé** ». Avant votre rendu, faites subir le même régime à votre propre feuille de style, notez les poids avant/après dans votre documentation technique, et préparez-vous à la « revue du code source » : le jury pourra vous demander d'expliquer n'importe quelle règle. Une règle que vous ne savez pas justifier est peut-être… une règle morte.

## Ressources

- [Validateur CSS du W3C](https://jigsaw.w3.org/css-validator/#validate_by_input)
- [MDN — Déboguer du CSS](https://developer.mozilla.org/fr/docs/Learn/CSS/Building_blocks/Debugging_CSS)
- [MDN — Propriétés raccourcies](https://developer.mozilla.org/fr/docs/Web/CSS/Shorthand_properties)
- [MDN — Héritage](https://developer.mozilla.org/fr/docs/Web/CSS/Inheritance)
- [MDN — Utiliser les variables CSS](https://developer.mozilla.org/fr/docs/Web/CSS/Using_CSS_custom_properties)
- [Chrome DevTools — Trouver le code CSS et JS inutilisé (*Coverage*)](https://developer.chrome.com/docs/devtools/coverage?hl=fr)

---

Exercice suivant : [12 — Défi : habiller « Le marché des saveurs »](../../niveau-4-recolte/12-defi-habiller-site/README.md)
