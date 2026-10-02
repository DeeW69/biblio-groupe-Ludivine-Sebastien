Issue 1 — BUG (Bilal)
Modèle : Bug report
Titre : Fondation apparaît en retard alors qu’il a déjà été rendu

Description :  
Après avoir réinitialisé la base avec python biblio.py init, la commande python biblio.py retards affiche Fondation comme non rendu, avec 256 jours de retard.
Dans le scénario messages adhérents, ce livre est pourtant indiqué comme rendu en janvier.
Le logiciel signale donc un retard qui ne devrait pas exister.

Comportement attendu :  
Un livre rendu ne doit plus apparaître dans la liste des retards.

Étapes pour reproduire :

python biblio.py init

python biblio.py retards

Constater que Fondation est toujours listé comme en retard

Gravité : moyenne


Issue 2 — ÉVOLUTION (Karim)
Modèle : Feature request / Evolution
Titre : Bloquer ou signaler le prêt d’un livre déjà emprunté

Description :  
Actuellement, le logiciel permet de prêter un livre déjà emprunté à un autre adhérent sans afficher le moindre avertissement.
Dans le scénario messages adhérents, Fondation a été emprunté par Bilal, puis immédiatement par Karim, sans message d’erreur.
Le système ne vérifie donc pas si un livre est déjà en cours d’emprunt.

Comportement attendu :  
Lorsqu’un livre est déjà emprunté, le logiciel devrait :

soit empêcher un second emprunt,

soit afficher un message d’avertissement ou de confirmation.

Étapes pour reproduire :

python biblio.py init

python biblio.py emprunter 4 2 (Fondation → Bilal)

python biblio.py emprunter 4 3 (Fondation → Karim)

Le logiciel accepte les deux emprunts sans signaler de problème

Proposition :  
Ajouter une vérification avant chaque emprunt pour éviter les prêts simultanés du même livre.
