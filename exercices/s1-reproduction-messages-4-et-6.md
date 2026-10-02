# Séance 1 — Reproduction des messages 4 et 6

Groupe : Ludivine & Sébastien.

On a testé les messages de Lucie et de Théo le **2 octobre 2026**, sous **Windows 11** (build 26300), avec **Python 3.11.9**. La version utilisée est le commit `28423e8` (`Initial commit`).

Pour refaire les tests, il faut ouvrir un terminal dans le dossier `biblio-groupe-Ludivine-Sebastien`. On repart à chaque fois de `python biblio.py init` pour réinitialiser la base. Les sorties du terminal sont recopiées ci-dessous ; les dates et le nombre de jours de retard dépendront du jour où le test est relancé.

## Message 4 — Lucie : le prêt passe avec un adhérent inexistant

Lucie explique qu'elle s'est trompée de numéro d'adhérent et que le logiciel a quand même accepté le prêt.

On a essayé avec le numéro `999`. Après l'initialisation, seuls les adhérents 1, 2 et 3 existent : ce numéro est donc bien invalide. On a choisi le livre 1, `L'Etranger`, qui est disponible.

Commandes lancées :

```powershell
python biblio.py init
python biblio.py emprunter 1 999
```

Résultat dans le terminal :

```text
Base initialisee : 6 livres, 3 membres.
Emprunt enregistre : livre 1, membre 999.
```

Pour vérifier que le prêt avait vraiment été enregistré, on a regardé les données de la base. La commande suivante affiche d'abord les adhérents, puis les prêts en cours du livre 1. Elle ne change aucune donnée.

```powershell
python -c "import biblio; c=biblio.get_connection(); print(c.execute('SELECT id, name FROM members ORDER BY id').fetchall()); print(c.execute('SELECT book_id, member_id FROM loans WHERE book_id = 1 AND return_date IS NULL').fetchall()); c.close()"
```

Résultat :

```text
[(1, 'Alice Martin'), (2, 'Bilal Haddad'), (3, 'Chloe Nguyen')]
[(1, 999)]
```

On s'attendait à ce que Biblio refuse le prêt et indique que l'adhérent est introuvable. Pourtant, il affiche une confirmation et enregistre le prêt pour le membre `999`, qui n'existe pas.

**C'est donc un bug :** on peut enregistrer un prêt sans qu'il corresponde à un adhérent existant. Ici, on a testé un numéro inexistant. Si Lucie avait saisi le numéro d'un autre adhérent existant, le logiciel ne pourrait pas deviner son erreur.

## Message 6 — Théo : un emprunt d'hier n'apparaît pas dans les retards

Théo se demande pourquoi un livre emprunté hier n'apparaît pas dans les retards. Pour vérifier, on a utilisé le livre 3, `Le Petit Prince`, et l'adhérent 1, `Alice Martin`.

On a d'abord réinitialisé la base, puis enregistré le prêt :

```powershell
python biblio.py init
python biblio.py emprunter 3 1
```

Résultat dans le terminal :

```text
Base initialisee : 6 livres, 3 membres.
Emprunt enregistre : livre 3, membre 1.
```

Le prêt vient d'être créé, il date donc d'aujourd'hui. Comme la commande `emprunter` ne permet pas de choisir une date, on a mis ce prêt à la date d'hier directement dans la base de test. Cela permet de reproduire le cas de Théo sans attendre un jour. Seule la date de ce prêt est changée, pas le code de Biblio ni l'horloge du PC.

```powershell
python -c "import biblio; from datetime import date, timedelta; c=biblio.get_connection(); c.execute('UPDATE loans SET loan_date = ? WHERE book_id = ? AND return_date IS NULL', ((date.today()-timedelta(days=1)).isoformat(), 3)); c.commit(); print(c.execute('SELECT book_id, member_id, loan_date, return_date FROM loans WHERE book_id = ?', (3,)).fetchone()); c.close()"
```

Résultat :

```text
(3, 1, '2026-10-01', None)
```

On retrouve bien le livre 3, l'adhérent 1 et la date du 1er octobre 2026, soit la veille du test. `None` signifie que le livre n'a pas encore été rendu.

On a ensuite affiché les retards :

```powershell
python biblio.py retards
```

Résultat dans le terminal :

```text
Dune, emprunte par Alice Martin : 251 jours de retard
Fondation, emprunte par Bilal Haddad : 256 jours de retard
```

`Le Petit Prince` n'apparaît pas dans la liste, ce qui correspond bien à ce que décrit Théo.

**C'est un comportement normal :** la durée de prêt prévue dans `biblio.py` est de **14 jours** (`LOAN_DAYS = 14`). Un livre est considéré en retard une fois ce délai dépassé. Après un seul jour, on s'attend donc à ce qu'il soit absent de la liste, et c'est bien le résultat obtenu.

Dune et Fondation sont déjà présents dans les données de départ. Leur affichage ne change pas le résultat de ce test : c'est l'absence du Petit Prince qu'on vérifie ici. Le cas de Fondation, qui apparaît alors qu'il a été rendu, concerne le message 2.

## Bilan

| Message | Classification | Résultat de la reproduction |
|---|---|---|
| 4 — Lucie | Bug | Un prêt est enregistré pour l'adhérent inexistant 999. |
| 6 — Théo | Comportement normal | Un prêt datant d'hier ne dépasse pas le délai de 14 jours. |

Pour cette séance, on s'est arrêté aux tests et à la classification des deux messages. Le code n'a pas été corrigé ; les issues seront faites plus tard.
