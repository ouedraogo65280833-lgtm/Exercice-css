# Sprint 1 — Exercices HTML + CSS

Bienvenue ! Vous savez maintenant **structurer** une page avec HTML. Place à la **mise en forme** : couleurs, polices, espacements, menus, grilles d'images, adaptation au téléphone… Ces **12 exercices** vous accompagnent en parallèle du brief **PlantEvo Viewer**. Ils sont classés en **4 niveaux**, comme une plante qui pousse : commencez par le niveau 1 et avancez à votre rythme.

> **Prérequis** : les exercices HTML du niveau 1 (01 → 05) et l'exercice 06 « page sémantique ». Le CSS habille du HTML : si la structure est mauvaise, le CSS devient vite un casse-tête.

| Niveau | Difficulté | Exercices | À la fin, vous saurez… |
|---|---|---|---|
| **1 · Graine** | ★☆☆☆ | 01 → 04 | lier une feuille de style, cibler les bons éléments, choisir couleurs et polices, maîtriser les marges et les bordures |
| **2 · Pousse** | ★★☆☆ | 05 → 08 | mettre en page un menu, des cartes, une galerie d'images et un site entier avec Flexbox et Grid |
| **3 · Arbre** | ★★★☆ | 09 → 11 | adapter une page au téléphone, la rendre interactive sans JavaScript, déboguer et alléger votre CSS |
| **4 · Récolte** | ★★★★ | 12 | habiller un mini-site complet à partir d'une maquette |

## Liste des exercices

### Niveau 1 · Graine — les bases du CSS

| N° | Exercice | Durée | Notions |
|---|---|---|---|
| 01 | [Ma première feuille de style](niveau-1-graine/01-premiere-feuille-de-style/README.md) | 30 min | syntaxe d'une règle, `style`, `<style>`, `<link>`, `color`, `background-color`, `font-family` |
| 02 | [Sélecteurs, classes et cascade](niveau-1-graine/02-selecteurs-cascade/README.md) | 45 min | `.classe`, `#id`, sélecteur descendant, héritage, cascade, spécificité |
| 03 | [Couleurs, polices et variables](niveau-1-graine/03-couleurs-polices/README.md) | 45 min | hex, `rgb()`, `hsl()`, contraste, variables `--…`, polices système, `rem`, `line-height` |
| 04 | [Le modèle de boîte](niveau-1-graine/04-modele-de-boite/README.md) | 45 min | `padding`, `border`, `margin`, `box-sizing`, `display`, `border-radius`, `box-shadow` |

### Niveau 2 · Pousse — mettre en page

| N° | Exercice | Durée | Notions |
|---|---|---|---|
| 05 | [Un menu avec Flexbox](niveau-2-pousse/05-menu-flexbox/README.md) | 45 min | `display: flex`, `justify-content`, `align-items`, `gap`, `:hover`, `:focus-visible`, `[aria-current]` |
| 06 | [Cartes et bannière avec Flexbox](niveau-2-pousse/06-cartes-flexbox/README.md) | 1 h | `flex-wrap`, `flex`, cartes alignées, bannière centrée, images fluides |
| 07 | [Une galerie d'images avec Grid](niveau-2-pousse/07-galerie-grid/README.md) | 1 h | `display: grid`, `fr`, `repeat()`, `minmax()`, `span`, `object-fit`, `aspect-ratio` |
| 08 | [Mettre en page un site entier avec Grid](niveau-2-pousse/08-mise-en-page-grid/README.md) | 1 h | `grid-template-areas`, pied de page en bas, Flexbox ou Grid ? |

### Niveau 3 · Arbre — adapter, animer, optimiser

| N° | Exercice | Durée | Notions |
|---|---|---|---|
| 09 | [Responsive : du téléphone à l'ordinateur](niveau-3-arbre/09-responsive/README.md) | 1 h | `meta viewport`, mobile first, `@media`, largeurs fluides, mode appareil de F12 |
| 10 | [Interactivité sans JavaScript](niveau-3-arbre/10-interactivite/README.md) | 1 h | `transition`, `transform`, `:target`, `details`/`summary`, `prefers-reduced-motion` |
| 11 | [Chasse aux bugs et régime minceur](niveau-3-arbre/11-debogage-optimisation/README.md) | 1 h | validateur CSS, F12, variables, factorisation, minification |

### Niveau 4 · Récolte — le défi

| N° | Exercice | Durée | Notions |
|---|---|---|---|
| 12 | [Défi : habiller « Le marché des saveurs »](niveau-4-recolte/12-defi-habiller-site/README.md) | 3 h | tout ! maquette → CSS → tests → documentation |

## Comment travailler

1. **Ouvrez le dossier de l'exercice** dans VS Code (*Fichier → Ouvrir le dossier…*).
2. **Lisez tout le `README.md`** avant d'écrire la moindre ligne de code.
3. **Ouvrez la page avec Live Server** (clic droit sur `index.html` → *Open with Live Server*) et placez le navigateur à côté de VS Code : chaque `Ctrl + S` met la page à jour.
4. **Travaillez avec les outils de développement** (`F12`) : onglet *Éléments* → panneau *Styles* pour voir quelles règles s'appliquent (une règle **barrée** a perdu face à une autre) et tester des valeurs en direct. Mode appareil (`Ctrl + Maj + M`) pour voir la page comme sur un téléphone.
5. **Cochez les critères de réussite** un par un.
6. **Validez votre code** : HTML sur [validator.w3.org](https://validator.w3.org/#validate_by_input), CSS sur [jigsaw.w3.org/css-validator](https://jigsaw.w3.org/css-validator/#validate_by_input). Objectif **0 erreur**.
7. **Bloqué ?** Dans l'ordre : relisez la consigne → ouvrez un indice (cliquez dessus pour le déplier) → demandez à votre binôme → appelez le coach.

## Règles du jeu

- **Tapez le code vous-même.** Pas de copier-coller depuis Internet ou une IA : c'est en tapant qu'on retient.
- **Une seule feuille de style externe**, rangée dans `css/style.css` et liée avec `<link>`. Pas de CSS dans les attributs `style="…"` (sauf quand la consigne le demande pour une expérience).
- **Pas de ressources externes** : polices du système plutôt que Google Fonts, pas de bibliothèque CSS toute faite (Bootstrap…). Le brief demande de **minimiser les liens externes** et **la taille du fichier CSS**.
- **Commentez et rangez votre CSS** : un commentaire `/* ===== EN-TÊTE ===== */` au début de chaque partie, les règles dans l'ordre de la page, **indentation de 2 espaces**, une déclaration par ligne.
- **Le HTML d'abord, le CSS ensuite** : on n'ajoute pas une `<div>` ou une `<br>` « pour la mise en page » si une propriété CSS sait le faire.
- **Pensez à tout le monde** : texte bien contrasté, focus clavier visible, page lisible sur un petit téléphone.
- **Noms de fichiers et de classes** en minuscules, sans espace ni accent (`carte-produit`, pas `Carte Produit`).
- **Entraidez-vous** : expliquer à un camarade est la meilleure façon de vérifier qu'on a compris.

## Outils

| Outil | À quoi ça sert |
|---|---|
| [VS Code](https://code.visualstudio.com/) + extension *Live Server* | Écrire le code et voir le résultat en direct |
| Chrome ou Firefox + **F12** | Inspecter les styles, tester en direct, simuler un téléphone, mesurer les contrastes |
| [Validateur HTML du W3C](https://validator.w3.org/#validate_by_input) | Vérifier votre HTML |
| [Validateur CSS du W3C](https://jigsaw.w3.org/css-validator/#validate_by_input) | Vérifier votre CSS |
| [MDN en français — CSS](https://developer.mozilla.org/fr/docs/Web/CSS) | La référence de toutes les propriétés CSS |
| [Flexbox Froggy](https://flexboxfroggy.com/#fr) · [Grid Garden](https://cssgridgarden.com/#fr) | S'entraîner à Flexbox et Grid en jouant (en français) |

Bon courage, et belle floraison !
