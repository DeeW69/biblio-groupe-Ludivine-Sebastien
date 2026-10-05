# Circulation de l'information : groupe Ludivine–Sébastien

Ce document décrit comment notre groupe se répartit le travail, échange les informations et conserve les décisions concernant Biblio. Il reprend le préremplissage de Ludivine et les compléments de Sébastien.

## 1. Rôles

Rédigé par : @DeeW69

Notre groupe comporte deux membres :

- **Sébastien (@DeeW69), membre A** : coordonne la répartition des issues et leur suivi. Pour le README, il rédige la présentation, les prérequis et l'installation. Il prend aussi les sections du rôle C : tests, structure du projet, contribution et auteurs.
- **Ludivine (@ludivine25), membre B** : rédige la section Utilisation du README, avec les commandes et leurs résultats, et relit la PR de documentation ouverte par Sébastien.

Les deux membres peuvent ouvrir une issue, proposer une correction et créer une PR. L'auteur d'une issue décrit le besoin ou le problème ; l'autre membre vérifie les informations et, pour un bug, essaie de le reproduire. Le responsable du travail est choisi ensemble et indiqué dans le champ **Assignees** de l'issue.

Chaque PR est relue par l'autre membre : Ludivine relit celles de Sébastien et Sébastien relit celles de Ludivine. Le relecteur vérifie les changements, laisse ses remarques et approuve lorsque les corrections sont terminées. L'auteur de la PR effectue ensuite la fusion lorsque l'approbation est obtenue et que les tests passent. Pour la PR du README, Sébastien effectue donc la fusion après la review de Ludivine.

## 2. Où circule chaque information

Rédigé par : @DeeW69 et @ludivine25

| Information | Qui la produit | Qui la valide | Où elle est stockée | Durée de vie |
|---|---|---|---|---|
| Code source | Le membre responsable de l'issue, Sébastien ou Ludivine | L'autre membre lors de la review, avec les tests | Fichiers du dépôt GitHub, notamment `biblio.py` et `tests/`, puis branche `main` après fusion | Maintenu pendant le projet ; versions précédentes conservées dans l'historique Git |
| Bug signalé | Le membre qui constate le problème | L'autre membre vérifie la reproduction et le comportement attendu | Issue GitHub avec le modèle « Signaler un bug » et le label `bug`, liée à la PR de correction | Ouvert jusqu'à résolution ; l'issue fermée reste consultable |
| Décision technique | Le membre qui propose un choix, après échange avec l'autre | Les deux membres, avec validation dans la PR | ADR dans `docs/adr/`, rédigé à partir du modèle et relié à l'issue ou à la PR concernée | Applicable jusqu'à son remplacement ; l'ancien ADR est conservé avec son statut mis à jour |
| Documentation d'installation | Sébastien pour les prérequis et l'installation ; Ludivine complète l'utilisation | Ludivine (@ludivine25) vérifie l'installation et ses commandes ; Sébastien relit les exemples d'utilisation | `README.md` à la racine du dépôt | Mise à jour à chaque changement concerné ; historique conservé dans Git |
| Question rapide entre membres | Sébastien ou Ludivine | Le membre concerné répond ; les deux confirment si une décision est nécessaire | Chat du groupe ; toute réponse utile au suivi est reportée dans une issue ou la documentation | Utile jusqu'à la réponse ; les décisions durables sont conservées dans le dépôt |
| Compte rendu de réunion | Un membre désigné au début de l'échange rédige les points et actions | L'autre membre complète et valide | Fichier Markdown daté dans `docs/`, créé lors de la réunion et partagé par PR | Conservé pendant le projet et dans l'historique Git pour retrouver les décisions |

Le chat sert aux échanges rapides. GitHub et les fichiers du dépôt conservent les informations nécessaires pour reprendre le travail : un accord dans le chat est reporté dans l'issue, la PR ou l'ADR concerné.

## 3. Règles de l'équipe

Rédigé par : @DeeW69

### Issues et répartition

- Avant d'ouvrir une issue, vérifier qu'une issue équivalente n'existe pas déjà.
- Utiliser un titre court et précis qui décrit le problème ou le besoin, par exemple « Le README ne permet pas d'installer le projet ». Aucun préfixe particulier n'est imposé.
- Choisir le modèle et son label : **Signaler un bug** (`bug`), **Proposer une évolution** (`enhancement`) ou **Poser une question** (`question`). Une amélioration de documentation peut utiliser le modèle d'évolution.
- Remplir les informations utiles : contexte, commandes de reproduction, résultat attendu et observé pour un bug ; besoin, proposition et critères d'acceptation pour une évolution.
- Sébastien coordonne le tri des issues avec Ludivine : vérifier les doublons, le label, les informations manquantes et la priorité. Les deux choisissent le responsable ; l'auteur de l'issue renseigne ensuite **Assignees**.
- Garder les échanges concernant une issue dans ses commentaires pour que l'autre membre puisse retrouver les explications.

### Branches, commits et synchronisation

- **À partir de la séance 2 : aucun push direct sur `main`. Toute modification passe par une pull request relue.**
- Avant une nouvelle tâche, revenir sur `main` et récupérer les changements distants avec **Fetch origin**, puis **Pull origin**.
- Créer une branche liée à l'issue, avec un nom explicite : `docs/<numero>-<sujet>` pour la documentation, `fix/<numero>-<sujet>` pour une correction ou `feature/<numero>-<sujet>` pour une fonctionnalité.
- Faire des commits limités à un sujet avec un message clair, par exemple `docs: complete la circulation de l'information` ou `fix: corrige le calcul des retards`.
- Publier la branche au premier envoi. Sur une branche partagée, se répartir les fichiers ou les sections avant de modifier le même document.
- Après un commit local, faire **Pull origin**, puis **Push origin**. Si un camarade a poussé entre-temps, récupérer ses changements et résoudre les éventuels conflits en conservant les contributions de chacun, puis pousser à nouveau.

### Review, validation et fusion

- Ouvrir une PR vers `main` pour un seul sujet et remplir le modèle : contexte, changements, impact et méthode de vérification. Ajouter `Closes #<numero>` lorsque la fusion doit fermer l'issue.
- Demander la review de l'autre membre. Pour la documentation, vérifier aussi le rendu Markdown dans **Files changed** et lancer réellement les commandes décrites.
- L'auteur corrige les remarques, met à jour la documentation concernée et vérifie les tests indiqués dans le [README](../README.md#tests). Le relecteur approuve la version finale.
- L'auteur fusionne après approbation et réussite des tests, puis supprime la branche devenue inutile. L'issue liée est fermée automatiquement ; pour une question sans changement de code, elle peut être fermée après une réponse validée.
- Les deux membres reviennent sur `main` et font **Pull origin** pour travailler à partir de la version commune à jour.
