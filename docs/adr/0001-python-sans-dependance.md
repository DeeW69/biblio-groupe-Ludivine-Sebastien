# 1. Utiliser Python sans dépendance externe

* Statut : accepté
* Date : 2026-03-15
* Décideurs : Équipe de développement Biblio

## Contexte

Biblio est un logiciel destiné à être utilisé par des bénévoles dans des associations. Ces bénévoles ont des compétences informatiques variables et n'ont pas forcément les droits d'administration ou un environnement de développement complet sur leur ordinateur. L'installation de bibliothèques tierces via `pip` (comme `requests`, `pandas` ou des ORM) peut échouer selon les restrictions de sécurité du système ou la version de Python installée.

## Options envisagées

* **Option 1 : Utiliser uniquement la bibliothèque standard de Python**
  * *Pour* : Aucune étape d'installation complexe (`pip install`), le projet fonctionne immédiatement sur n'importe quelle installation Python standard.
  * *Contre* : Développement de certaines fonctionnalités plus long ou plus manuel (ex: requêtes SQLite brutes, gestion des arguments en CLI).

* **Option 2 : Utiliser des dépendances externes (ex: SQLAlchemy, Click, etc.)**
  * *Pour* : Code plus concis et abstraction de plus haut niveau pour la base de données et l'interface CLI.
  * *Contre* : Nécessite la création et l'activation d'un environnement virtuel (`venv`) ainsi que la gestion d'un fichier `requirements.txt`, ce qui augmente fortement le risque d'erreurs à l'installation chez les bénévoles.

## Décision

Nous choisissons d'utiliser uniquement **Python et sa bibliothèque standard**, sans dépendance externe.

## Conséquences

* **Ce qui devient plus facile** :
  * L'installation du projet est extrêmement simple et rapide (`python biblio.py init`).
  * Moins de maintenance de dépendances et aucun risque de conflits de versions chez les utilisateurs.
* **Ce qui devient plus difficile** :
  * Le code doit gérer directement les requêtes SQL et l'analyse des arguments en ligne de commande.
