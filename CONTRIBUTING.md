# Comment contribuer ?

Merci de prendre le temps de contribuer ! 🎉

Voici quelques informations pour démarrer :

## Rapport de bug, nouvelles fonctionnalités

Nous utilisons GitHub pour suivre tous les bugs et discussions sur les nouvelles fonctionnalités. Pour rapporter un bug ou proposer une évolution vous pouvez [ouvrir une nouvelle discussion](https://github.com/betagouv/mon-entreprise/issues/new). N'hésitez pas à utiliser la recherche pour vérifier si le sujet n'est pas déjà traité dans une discussion ouverte.

## Développement

Si vous voulez participer au développement de nouvelles fonctionnalités, vous pouvez consulter la liste des «[good first issue](https://github.com/betagouv/mon-entreprise/issues?q=is%3Aopen+is%3Aissue+label%3A%22%3Anew%3A+good+first+issue%22) ». Ce sont des fonctionnalités intéressantes qui ne sont normalement pas trop complexe à implémenter. N'hésitez pas à poser toutes vos questions sur ces issues !

### Technologies

L'application est écrite en JavaScript, elle est exécuté uniquement côté client — il n'y a pas de serveur applicatif, nous générons des fichiers `.html` statiques

Nous utilisons :

-   [TypeScript](https://www.typescriptlang.org) pour ajouter un système de typage à notre code JavaScript. Le typage n'est pas utilisé partout et il n'est pas obligatoire de le prendre en compte pour contribuer.
-   [Yarn](https://yarnpkg.com/fr) pour la gestion des dépendances (à la place de NPM qui est souvent utilisé dans les applications JavaScript)
-   [React](https://reactjs.org) pour la gestion de l'interface utilisateur
-   [Redux](https://redux.js.org) pour gérer le “state” de l'application côté client
-   [Prettier](https://prettier.io/) pour formater le code source, l'idéal est de configurer votre éditeur de texte pour que les fichiers soit formatés automatiquement quand vous sauvegardez un fichier. Si vous utilisez [VS Code](https://code.visualstudio.com/) cette configuration est automatique.
-   [Webpack](https://webpack.js.org) pour le “bundling”
-   [Eslint](http://eslint.org) qui permet par exemple d'éviter de garder des variables inutilisées
-   [Ramda](https://ramdajs.com) comme libraire d'utilitaires pour manipuler les listes/objects/etc (c'est une alternative à lodash ou underscore)
-   [Mocha](https://mochajs.org), [Jest](https://jestjs.io) et [Cypress](https://www.cypress.io) pour les l'execution des tests. Plus d'informations dans la section consacrée aux tests.

### Démarrage

Tout d'abord assurez-vous d'avoir toutes les clés d'API nécessaires dans votre fichier `mon-entreprise/.env`.
Demandez les détails à vos collègues (ces informations n'étant pas publiques).

Si l'historique des commits est trop volumineux, vous pouvez utiliser le paramètre `depth` de git pour ne télécharger que les derniers commits.

```
# Clone this repo on your computer
git clone --depth 100 git@github.com:betagouv/mon-entreprise.git && cd mon-entreprise

# Install the Javascript dependencies through Yarn
yarn install

# Download some data
yarn prepare

# Watch changes in publicodes and run the server for mon-entreprise
yarn start
```

L'application est exécuté sur https://localhost:8080/mon-entreprise pour la version française et http://localhost:8080/infrance pour la version anglaise.

Pour activer le tracing Redux:

```
REDUX_TRACE=true yarn start
```

### Messages de commit

A mettre sans retenue dans les messages de commit :

https://github.com/atom/atom/blob/master/CONTRIBUTING.md#git-commit-messages

-   🎨 `:art:` when working on the app's visual style
-   🐎 `:racehorse:` when improving performance
-   📝 `:memo:` when writing docs
-   🐛 `:bug:` when fixing a bug
-   🔥 `:fire:` when removing code or files
-   💚 `:green_heart:` when fixing the CI build
-   ✅ `:white_check_mark:` when adding tests
-   ⬆️ `:arrow_up:` when upgrading dependencies
-   :sparkles: `:sparkles:` when formatting, renaming, reorganizing files

Et ceux spécifiques au projet :

-   :gear: `:gear:` pour une contribution au moteur qui traite les YAML
-   :hammer: `:hammer:` pour une contribution à la base de règles
-   :calendar: `:calendar:` pour un changement de règle du à une évolution temporelle (en attendant mieux)
-   :chart_with_upwards_trend: `:chart_with_upwards_trend:` pour une amélioration du tracking
-   :alien: `:alien:` pour ajouter des traductions
-   :wheelchair: `:wheelchair:` pour corriger les problèmes liés à l'accessibilité
-   :fountain_pen: `:fountain_pen:` pour séparer les commits liés à la modification du contenu
-   :mag: `:mag:` pour les modifications liées au référencement naturel

### Tests

Pour executer les tests unitaires :

```sh
$ yarn run test-common
```

Pour le snapshot testing :

```sh
$ yarn run test:regressions
```

Si vous souhaitez mettre à jour les snapshots vous pouvez utiliser le paramètre `--updateSnapshot`, son raccourci `-u`, ou encore le [mode interactif](https://jestjs.io/docs/en/snapshot-testing#interactive-snapshot-mode).

Enfin pour les tests d'intégration :

```sh
$ yarn run cypress run
```

### Traduction 👽

Le site est disponible en français, et en anglais sur https://mycompanyinfrance.com

Les traductions se trouvent dans le répertoire `source/locales`.

La librairie utilisée pour la traduction de l'UI est
[react-i18next](https://react.i18next.com/).

Lorsque l'on introduit une nouvelle chaîne de caractère dans l'UI il faut
systématiquement penser à gérer sa traduction, via un composant `<Trans>`, ou
via la fonction `t`

Le circle-ci fait une analyse statique du code pour repérer les chaînes non
traduites, dans le moteur et l'UI :

```sh
$ yarn run i18n:rules:check
$ yarn run i18n:ui:check
```

Pour traduire automatiquement les chaînes manquantes via l'api Deepl :

```sh
$ yarn run i18n:rules:translate
$ yarn run i18n:ui:translate
```

N'oubliez pas de vérifier sur le diff que rien n'est choquant.

### CI/CD

-   Nous utilisons des [Github actions](https://github.com/features/actions) pour faire tourner les builds et
    tests.
-   [Netlify](https://www.netlify.com/), s'occupe de l’hébergement du site sur Internet avec gestion des DNS.

### Analyse des bundles

La commande `yarn run build:analyse-bundle` gènere une visualisation interactive du
contenu packagé, cf.
[webpack-bundle-analyzer](https://github.com/webpack-contrib/webpack-bundle-analyzer)

### Modifier publicodes

Publicodes dispose désormais de son propre dépôt GitHub https://github.com/betagouv/publicodes

Néanmoins pour certaines nouvelles fonctionnalités de mon-entreprise nous concervons le besoin de modifier publicodes avec le moins de frictions possible. Pour tester une évolution du moteur il serait en effet trop lourd d'avoir à ouvrir d'abord une PR côté publicodes, la merger, publier une nouvelle version du paquet, puis ré-intégrer cette nouvelle version sur mon-entreprise.

C'est pourquoi nous intégrons le code source du publicode dans le sous-répertoire `publicodes/`. La commande `git subtree` nous permet de synchroniser les changements effectués dans l'un ou l'autre des dépôts.

La première chose à faire est d'ajouter une nouvelle `remote` pour `betagouv/publicodes`, ici nous l'appelons simplement `publicodes` :

```sh
git remote add publicodes git@github.com:betagouv/publicodes.git
```

Ensuite il est possible de remonter les changements effectués dans le sous-repertoire `publicodes/` vers la branche master de la remote `publicodes`.

```sh
$ git subtree push --prefix=publicodes publicodes master
```

Dans l'autre sens il est possible de rapatrier les changements avec la commande

```sh
$ git subtree pull --prefix=publicodes publicodes master --squash
```

## Développement de modèles Publicodes

### Traduction des normes (lois) en règles Publicodes

Checklist:

-   [ ] Lire les articles de vulgarisation (sur le site de l'URSSAF, des impôts, etc.).
-   [ ] Utiliser un moteur de recherche spécialisé, comme [RFPaye](https://rfpaye.grouperf.com/).
-   [ ] [Lire les normes][wiki normes] et noter leurs référence dans les règles Publicodes.

[wiki normes]: https://github.com/betagouv/mon-entreprise/wiki/Comment-lire-les-normes-(la-loi)-efficacement-pour-r%C3%A9diger-des-r%C3%A8gles-Publicodes%3F

### Tests

Pour tester les règles, il est recommandé de:

-   faire tourner un simulateur et vérifier à la main l'adéquation des règles avec les normes
    traduites ;
-   créer des cas de tests de non-régression sous la forme de nouveaux snapshots (cf.
    `mon-entreprise/test/regressions`).

## Documentation

### Publicodes

Un tutoriel sur publicodes est disponible sur https://publi.codes.

Un wiki contenant des informations intéressantes sur publicodes et le
raisonnement ayant abouti à ce langage sont dispos sur le repository
[betagouv/publicodes](https://github.com/betagouv/publicodes/wiki), qui est par
ailleurs inutilisé.

Pour se familiariser avec les règles, vous pouvez jeter un œil aux fichiers
contenant les règles elles-mêmes (dans le dossier `rules`) mais cela peut
s'avérer assez abrupt.

Essayez plutôt de jeter un oeil [aux tests](./publicodes/test/mécanismes/expressions.yaml)
dans un premier temps, puis au [mécanismes en
place](./publicodes/source/mecanisms).

## Publier une nouvelle version des paquets publicodes

<!-- TODO: action à déplacer dans le dépot betagouv/publicodes -->

Voici la marche à suivre pour publier une nouvelle version :

1. Renseigner les modifications dans publicodes/CHANGELOG.md
2. Remplacer les références à la précédente version par la nouvelle version dans les packages.json
3. Ajouter tous les changement dans un commit avec le message suivant :
    ```
     📦 Publicodes v1.0.0-beta.<n>
    ```
    > **Important** Le message doit être exactement celui-ci (emoji compris), car le script de déploiement automatique sur le CI se base sur ce dernier.
4. Laisser faire le CI, une fois le commit mergé sur master, le paquet sera déployé effectivement
