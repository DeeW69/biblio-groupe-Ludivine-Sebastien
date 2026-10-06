# ADR 0004 : convention de nommage des branches

- Statut : proposé
- Date : 2026-10-06
- Décideurs : @DeeW69 @ludivine25

## Contexte

Chaque modification de Biblio passe par une branche et une pull request vers `main`. Notre petite équipe doit distinguer les corrections et les améliorations destinées aux bénévoles de l’association, retrouver l’issue concernée et permettre à l’autre membre de reprendre le travail.

Le document [circulation.md](../circulation.md#branches-commits-et-synchronisation) utilise déjà les types `docs`, `fix` et `feature`. Nous devons formaliser cette convention pour éviter des noms ambigus dans la liste des branches, tout en respectant les noms de branches d’ADR imposés par l’atelier.

## Options envisagées

1. **Des noms libres**, par exemple `correction-retards` ou `documentation`.
   - Pour : création rapide, sans structure à mémoriser.
   - Contre : le nom peut être vague, ne distingue pas toujours deux tâches et ne permet pas de retrouver directement l’issue.

2. **La convention `type/numero-mots-cles`**, par exemple `fix/3-retards`, `docs/16-contributing` ou `feature/4-eviter-prets-multiples`.
   - Pour : le type indique la nature du changement, le numéro renvoie à l’issue et les mots-clés résument le sujet ; cette convention reprend les règles déjà documentées par le groupe.
   - Contre : il faut ouvrir l’issue avant de créer la branche, vérifier son numéro et appliquer une exception pour les branches d’ADR demandées par le cours.

## Décision

Nous retenons `type/numero-mots-cles` pour les nouvelles branches, avec les types `docs`, `fix` et `feature`, et l’exception `docs/adr-NNNN` pour les ADR de cet atelier, où `NNNN` désigne le numéro de l’ADR.

## Conséquences

- Il devient plus facile de repérer le sujet d’une branche et de retrouver son issue : `docs` désigne la documentation, `fix` une correction et `feature` une fonctionnalité.
- Chaque nouvelle branche ordinaire nécessite une issue préalable ; l’auteur vérifie le type et le numéro, puis choisit des mots-clés courts, en minuscules, sans espaces ni accents et séparés par des tirets.
- Les branches `docs/adr-0002`, `docs/adr-0003` et `docs/adr-0004` suivent l’exception de l’atelier ; aucune issue supplémentaire n’est nécessaire uniquement pour leur nommage.
- Les anciennes branches conservent leur nom afin de préserver les repères des PR et du travail déjà commencé ; la convention s’applique aux nouvelles branches.
- Le nom de branche ne ferme pas une issue : la description de la PR contient `Closes #<numero>` lorsque la fusion résout effectivement cette issue.
- L’équipe doit vérifier la convention lors des reviews ; le nommage seul ne remplace ni l’approbation de l’autre membre ni la réussite du check `tests`.
