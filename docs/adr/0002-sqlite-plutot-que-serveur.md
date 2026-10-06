# ADR 0002 : SQLite plutôt qu’un fichier JSON ou un serveur PostgreSQL

- Statut : proposé
- Date : 2026-10-06
- Décideurs : @DeeW69 @ludivine25

## Contexte

Biblio doit conserver le catalogue, les membres et les prêts entre deux utilisations. Les bénévoles de la bibliothèque associative installent l’application sur leur ordinateur et ne disposent pas nécessairement de compétences pour administrer une base de données. Nous devons choisir un stockage adapté à cet usage local, tout en prenant en compte deux commandes qui tenteraient d’enregistrer un prêt en même temps. Le code utilise déjà `sqlite3` et le fichier `biblio.db`.

## Options envisagées

1. **Un fichier JSON**
   - Pour : format texte lisible, accessible avec le module `json` de Python, sans serveur à installer.
   - Contre : il faudrait réécrire le stockage, les recherches et les liens entre livres, membres et prêts ; deux écritures simultanées nécessiteraient notre propre gestion du verrouillage et des mises à jour pour éviter de perdre des données.

2. **SQLite**
   - Pour : base locale avec requêtes SQL et transactions, sans serveur séparé ; le module `sqlite3` fourni avec Python permet de conserver l’implémentation existante.
   - Contre : une seule transaction d’écriture peut modifier une base à la fois ; il faut gérer les attentes ou erreurs de verrouillage et les évolutions du schéma. [Documentation Python](https://docs.python.org/3.12/library/sqlite3.html), [usages de SQLite](https://www.sqlite.org/whentouse.html).

3. **Un serveur PostgreSQL**
   - Pour : stockage centralisé adapté à plusieurs postes et à de nombreuses écritures concurrentes.
   - Contre : serveur, comptes, connexion et pilote Python à installer et maintenir ; cela alourdirait l’installation chez les bénévoles pour le besoin local actuel. [Bases locales et client-serveur](https://www.sqlite.org/whentouse.html).

## Décision

Nous conservons SQLite, utilisé avec le module `sqlite3` de Python, pour stocker localement les livres, les membres et les prêts de Biblio.

## Conséquences

L’installation reste simple pour les bénévoles et les requêtes existantes sont conservées. Les transactions permettent de regrouper des modifications qui doivent être validées ensemble.

L’équipe doit prévoir et tester les migrations du schéma, ainsi qu’une procédure de sauvegarde et de restauration. Les transactions d’écriture doivent rester courtes et les erreurs de verrouillage doivent être prises en compte.

SQLite ne garantit pas à lui seul qu’un livre ne soit prêté qu’une fois : les contrôles de disponibilité, les contraintes adaptées et les tests restent à prévoir pour empêcher les doubles prêts.

Si l’association a besoin de plusieurs postes écrivant fréquemment dans une base commune, nous réexaminerons cette décision ; le partage direct de `biblio.db` sur un lecteur réseau n’est pas la solution retenue. [Limites d’usage de SQLite](https://www.sqlite.org/whentouse.html).
