# Contribuer à Biblio

Les règles communes sont conservées dans [docs/circulation.md](docs/circulation.md). Notre groupe comporte deux membres : Sébastien (@DeeW69), membre A qui reprend aussi le rôle C, et Ludivine (@ludivine25), membre B.

## Avant de coder

Chercher d’abord si une issue décrit déjà le même problème. Sinon, ouvrir **Issues > New issue** et choisir **Signaler un bug**, **Proposer une évolution** ou **Poser une question**. Une amélioration de documentation utilise le modèle **Proposer une évolution**.

Pour une évolution, remplir **Besoin**, **Proposition** et **Critères d’acceptation**. Pour un bug, préciser l’environnement, les commandes de reproduction et les résultats attendu et observé. Noter le numéro de l’issue et choisir ensemble le responsable à indiquer dans **Assignees**.

## Branches

Récupérer la dernière version de `main` avec **Fetch origin**, puis **Pull origin**, avant de créer une branche. Aucun push direct sur `main` : chaque modification passe par une PR relue. Pour créer un fichier sur GitHub, partir de `main`, choisir **Add file > Create new file**, puis enregistrer le commit sur une nouvelle branche.

Les conventions déjà validées dans [circulation.md](docs/circulation.md#branches-commits-et-synchronisation) sont :

- `docs/<numero>-<sujet>` pour la documentation, par exemple `docs/16-contributing` pour l’issue #16 ;
- `fix/<numero>-<sujet>` pour une correction ;
- `feature/<numero>-<sujet>` pour une fonctionnalité.

Publier la branche au premier envoi. Sur une branche partagée, répartir les fichiers ou sections, puis récupérer les changements des autres avant de pousser. Résoudre les conflits en conservant les contributions de chacun.

L’ADR 0004 demandé dans le cours n’est pas encore présent dans `docs/adr/`. Les conventions ci-dessus devront être confrontées à cette décision dès qu’elle sera disponible.

## Commits

Un commit traite un seul sujet. Utiliser le format `type: message`, avec une action précise, par exemple :

- `docs: ajoute les règles de contribution` ;
- `fix: exclut les prêts rendus du calcul des retards` ;
- `feat: ajoute l’export du catalogue en CSV`.

Vérifier les fichiers sélectionnés avant de créer le commit. Les bases `.db` et les dossiers `__pycache__` restent exclus par `.gitignore`.

## Pull requests

Ouvrir une PR de la branche de travail vers `main`. Remplir les sections du [modèle de PR](.github/pull_request_template.md) : **Contexte**, **Changements**, **Impact** et **Comment tester**. Indiquer les commandes réellement exécutées et leurs résultats.

Ajouter `Closes #<numero>` dans la description, par exemple `Closes #16` pour l’issue #16. Garder un seul sujet par PR et demander la review de l’autre membre.

L’auteur fusionne après approbation et réussite du check `tests`, puis supprime la branche. La fusion ferme automatiquement l’issue liée. Les deux membres reviennent sur `main` et récupèrent les changements.

## Review

Ludivine relit les PR de Sébastien ; Sébastien relit celles de Ludivine. L’auteur ne peut pas approuver sa propre PR. Les deux membres sont désignés dans `.github/CODEOWNERS` pour permettre cette review croisée.

Dans **Files changed**, comparer les modifications aux critères d’acceptation de l’issue, vérifier le rendu des documents et exécuter les commandes concernées. Pour cet atelier, relire d’abord la PR du formulaire de blocage, nécessaire à la partie suivante.

Choisir **Request changes** si un critère manque, si les tests échouent, si une commande ne fonctionne pas ou si la documentation est incorrecte. Indiquer le fichier concerné, le problème constaté et la correction attendue. L’auteur corrige ; le relecteur vérifie la nouvelle version et choisit **Approve** lorsque les remarques sont résolues.

## Definition of Done

Cette checklist reprend les règles vérifiables du dépôt. Elle reste à confronter à la liste exacte du cours, qui n’est pas encore disponible dans le dépôt.

Avant la fusion :

- [ ] Les critères d’acceptation de l’issue sont satisfaits.
- [ ] La PR traite un seul sujet et référence l’issue avec `Closes #<numero>`.
- [ ] Les tests locaux passent : `python -m unittest discover -s tests -t . -v`.
- [ ] Le check GitHub Actions `tests` est vert.
- [ ] La documentation concernée est à jour ; les commandes décrites ont été vérifiées.
- [ ] Les remarques de review sont résolues et l’autre membre a approuvé.

Après la fusion, vérifier que l’issue est fermée, supprimer la branche de travail et récupérer `main` à jour.

## Signaler un blocage

Ouvrir **Issues > New issue > Signaler un blocage**, le formulaire défini dans `.github/ISSUE_TEMPLATE/blocage.yml`. Remplir ses cinq champs obligatoires :

1. **Tâche** : indiquer l’issue ou la PR concernée.
2. **Blocage** : décrire ce qui empêche d’avancer et copier le message d’erreur exact.
3. **Ce que j’ai déjà essayé** : donner les commandes ou actions tentées et leurs résultats.
4. **Ce dont j’ai besoin** : préciser qui doit faire quoi et mentionner la personne avec `@pseudo`.
5. **Échéance** : indiquer quand l’absence de solution compromet le travail.

Conserver la suite des échanges et la solution dans cette issue pour que l’autre membre puisse reprendre le travail.
