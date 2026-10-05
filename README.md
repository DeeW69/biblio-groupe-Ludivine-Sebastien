# Biblio

Biblio est une application en ligne de commande destinée aux bénévoles d'une petite bibliothèque associative pour consulter le catalogue, rechercher des livres et gérer les emprunts, les retours et les retards.

## Prérequis

- Python 3 accessible depuis un terminal. Les commandes ci-dessous ont été vérifiées avec Python 3.11.9 ; les tests GitHub Actions sont configurés avec Python 3.12.
- Git pour récupérer le dépôt (GitHub Desktop peut aussi le cloner).
- Un terminal : PowerShell ou Invite de commandes sous Windows, Terminal sous macOS ou Linux.

Aucun paquet externe n'est nécessaire : SQLite et les outils de test font partie de la bibliothèque standard de Python. Aucune installation avec pip ni serveur de base de données n'est nécessaire.

Vérifier Python :

```console
python --version
```

Résultat obtenu sur le poste de validation (la version peut varier sur votre poste) :

```text
Python 3.11.9
```

Si votre installation utilise le nom `python3`, remplacez `python` par `python3` dans toutes les commandes de ce README :

```console
python3 --version
```

Résultat obtenu sur le poste de validation :

```text
Python 3.11.9
```

Sous Windows, le lanceur `py`, s'il est installé, peut également remplacer `python` :

```console
py --version
```

Résultat obtenu sur le poste de validation :

```text
Python 3.11.9
```

Vérifier Git :

```console
git --version
```

Résultat obtenu sur le poste de validation (la version peut varier) :

```text
git version 2.55.0.windows.3
```

Si une commande n'est pas reconnue, installer Python 3 ou Git selon le cas, vérifier que le programme est accessible dans le PATH, puis rouvrir le terminal.

## Installation

Ouvrir un terminal dans le dossier qui accueillera le projet et cloner le dépôt :

```console
git clone https://github.com/DeeW69/biblio-groupe-Ludivine-Sebastien.git
```

Résultat obtenu : un dossier `biblio-groupe-Ludivine-Sebastien` contenant le projet est créé. Le terminal affiche notamment :

```text
Cloning into 'biblio-groupe-Ludivine-Sebastien'...
```

Entrer dans ce dossier :

```console
cd biblio-groupe-Ludivine-Sebastien
```

Résultat : le terminal se trouve à la racine du projet, où est le fichier `biblio.py`. Cette commande n'affiche aucun message.

Toutes les commandes suivantes se lancent depuis ce dossier. Initialiser la base **avant toute commande d'utilisation** :

**Attention : l'initialisation remplace les données de la base par les données de démonstration. Ne la relancez pas sur une base dont vous souhaitez conserver les prêts.**

```console
python biblio.py init
```

Résultat obtenu :

```text
Base initialisee : 6 livres, 3 membres.
```

Le fichier SQLite `biblio.db` est créé dans le dossier courant. Les adhérents de démonstration sont Alice Martin (1), Bilal Haddad (2) et Chloe Nguyen (3). La variable d'environnement `BIBLIO_DB`, si elle est définie, permet de choisir un autre fichier de base. Les fichiers `.db` sont ignorés par Git.

## Utilisation

## Tests

Depuis la racine du projet, lancer la même commande que GitHub Actions :

```console
python -m unittest discover -s tests -t . -v
```

Résultat obtenu : les quatre tests réussissent. Extrait de la sortie du 5 octobre 2026 (la durée varie) :

```text
test_borrow_available_book (tests.test_biblio.BiblioTest.test_borrow_available_book) ... ok
test_borrow_unknown_book_fails (tests.test_biblio.BiblioTest.test_borrow_unknown_book_fails) ... ok
test_late_contains_dune (tests.test_biblio.BiblioTest.test_late_contains_dune) ... ok
test_search_finds_title (tests.test_biblio.BiblioTest.test_search_finds_title) ... ok

----------------------------------------------------------------------
Ran 4 tests in 0.218s

OK
```

Les tests utilisent une base temporaire indépendante de `biblio.db` et l'initialisent eux-mêmes. Les messages de l'application s'affichent aussi pendant les tests : « Erreur : livre 42 introuvable. » est attendu dans le test d'un livre inexistant. La conclusion `OK` confirme la réussite ; `FAILED` indique un échec.

## Structure du projet

```text
.
|-- biblio.py                         # commandes et accès à SQLite
|-- tests/
|   |-- __init__.py
|   `-- test_biblio.py                # quatre tests unittest
|-- docs/
|   |-- circulation.md               # circulation de l'information et règle des PR
|   `-- adr/0000-modele.md            # modèle de décision d'architecture
|-- exercices/                       # consignes et comptes rendus du TP
|-- .github/
|   |-- ISSUE_TEMPLATE/              # modèles : bug, évolution et question
|   |-- pull_request_template.md     # modèle de PR
|   `-- workflows/tests.yml          # tests automatiques sur PR et push sur main
|-- .gitignore                       # exclut les bases .db et __pycache__
`-- README.md
```

La base `biblio.db` apparaît après l'installation ; elle n'est pas versionnée.

## Contribuer

La règle de l'équipe est de passer par une **pull request relue, sans push direct sur `main`**, comme indiqué dans [la documentation de circulation de l'information](docs/circulation.md).

1. Ouvrir une issue avec le modèle adapté : **Signaler un bug**, **Proposer une évolution** ou **Poser une question**. Décrire le besoin ou les étapes de reproduction et noter le numéro.
2. Dans GitHub Desktop, sélectionner `main`, faire **Fetch origin**, puis **Pull origin** si des changements sont disponibles. Créer une branche liée à l'issue ; pour ce README, il s'agit de `docs/5-readme`, liée à l'issue #5.
3. Modifier uniquement les fichiers et sections concernés. Vérifier réellement les commandes documentées et lancer les tests de la section précédente.
4. Faire un commit au message explicite, puis **Publish branch** au premier envoi. Sur une branche partagée, faire **Pull origin** avant **Push origin**. Si le push est refusé parce qu'un autre membre a poussé, récupérer ses changements, résoudre les éventuels conflits en conservant les contributions de chacun, puis pousser à nouveau.
5. Ouvrir une PR vers `main`, remplir le modèle et ajouter `Closes #5` pour ce README (adapter le numéro pour une autre issue). Demander la review d'un autre membre ; Ludivine relit cette PR.
6. Le relecteur vérifie le rendu du README dans **Files changed**, teste les commandes et laisse ses commentaires, puis approuve lorsque les corrections sont terminées.
7. Après approbation et réussite des tests, fusionner la PR et supprimer la branche. L'issue liée est fermée automatiquement. Revenir sur `main` et faire **Pull origin** pour récupérer le résultat.

## Auteurs

Groupe Ludivine–Sébastien, B2, TP Travail collaboratif et documentation technique.

- Sébastien ([DeeW69](https://github.com/DeeW69)) : membre A — présentation, prérequis et installation ; prend aussi les sections du rôle C — tests, structure du projet, contribuer et auteurs.
- Ludivine ([ludivine25](https://github.com/ludivine25)) : membre B — utilisation et review de la PR.
