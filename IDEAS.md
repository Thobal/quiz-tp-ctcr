# Idées d'amélioration — Quiz TP CTCR

## À réaliser

1. **Chronomètre de session**
   Mesurer le temps total passé sur un quiz et l'afficher dans les résultats en fin de session. Permet de suivre si l'on répond plus vite au fil de l'entraînement, en plus du score.

2. **Filtre par fiche dans "Mes 20 dernières erreurs"**
   Ajouter un sélecteur permettant de n'afficher que les erreurs d'une fiche spécifique. Utile pour cibler une révision sur une fiche précise sans être distrait par les erreurs des autres fiches.

3. **Lecture audio des questions**
   Ajouter un bouton sur chaque question de quiz pour faire lire la question à voix haute via l'API Web Speech (intégrée dans tous les navigateurs modernes, aucune dépendance). Utile sur mobile pour s'entraîner mains libres.

4. **Graphique comparatif des scores par fiche**
   Un graphique en barres horizontales affichant le score moyen (5 dernières sessions) de chaque fiche travaillée, triées par score croissant. Permet d'identifier d'un coup d'œil les fiches les plus faibles sans parcourir la heatmap.

---

## Réalisées

- **Barre de progression pendant le quiz** — Un compteur "Question X / 10" est affiché dans le bandeau supérieur du quiz.

- **Partage des statistiques PDF** — Le bouton "Exporter en PDF" détecte si l'API Web Share supporte les fichiers (mobile). Si oui, propose une modale "Partager…" ou "Télécharger". Sinon, déclenche le téléchargement directement.

- **Taux de maîtrise global affiché sur l'accueil** — Sous le titre, un chiffre synthétique affiche le pourcentage de maîtrise moyen sur l'ensemble des fiches travaillées (basé sur les 5 dernières sessions par fiche).

- **Vue hebdomadaire des scores dans les statistiques** — Tableau affichant semaine par semaine les valeurs des deux jauges (fiches travaillées / maîtrise globale), avec évolution et barres de couleur. Remplace le bloc "Dernières sessions".

---

## Rejetées
*(conservées pour mémoire — ne pas reproposer)*

- **Questions marquées comme favorites** — Dans l'écran de révision, marquer des questions d'une étoile pour constituer une liste personnelle de questions à retravailler en priorité.

- **Mise en évidence des différences dans les corrections** — Dans "Mes 20 dernières erreurs" et dans la correction immédiate, mettre en évidence les caractères ou mots qui diffèrent entre la réponse donnée et la bonne réponse (style diff).

- **Animation sur score parfait** — Lorsque le score final est 100 %, déclencher une petite animation (confetti ou similaire) sur l'écran de résultats.

- **Résumé de fiche avant quiz** — Ajoute une étape supplémentaire à chaque démarrage de quiz, ce qui nuit à la fluidité de l'expérience utilisateur.

- **Quiz des questions non maîtrisées** — Un nouveau mode de quiz qui pioche uniquement parmi les questions dont le taux de réussite personnel est inférieur à 50 % (calculé sur l'historique), pour cibler ses lacunes de manière encore plus précise que la révision classique.

- **Détail d'une erreur cliquable dans la révision** — Dans "Mes 20 dernières erreurs", rendre chaque carte cliquable pour afficher une vue détaillée : question complète, réponse donnée, bonne réponse, explication et image de panneau si disponible.

- **Bouton "Rejouer" en fin de quiz** — Sur l'écran de résultats, ajouter un bouton "Rejouer" qui relance immédiatement le même quiz sans repasser par l'accueil.

- **Compteur de sessions sur les boutons de fiche** — Afficher discrètement le nombre de sessions jouées directement sur chaque bouton de la grille de l'accueil.

- **Filtre par fiche dans l'historique des sessions** — Dans la section "Dernières sessions" des statistiques, ajouter un sélecteur permettant de n'afficher que les sessions d'une fiche spécifique.

- **Mode révision ciblée des erreurs** — Depuis "Mes 20 dernières erreurs", un bouton "Se faire interroger sur mes erreurs" qui lance un mini-quiz uniquement sur les questions où tu as échoué.

- **Quiz du glossaire** — Dans l'écran Glossaire, ajouter un bouton "Se tester sur le glossaire". La validation des réponses libres sur des définitions longues est trop complexe à implémenter correctement.

- **Indicateur de tendance par fiche** — Sur les boutons de fiche de l'accueil, afficher une petite flèche ↑ ou ↓ indiquant si le score s'améliore ou se dégrade entre les deux dernières sessions.

- **Score en temps réel pendant le quiz** — Afficher discrètement un mini-compteur pendant le quiz (ex : "5 / 7 correctes").

- **Export des données en JSON** — Un bouton pour exporter toutes les statistiques brutes en JSON. *(Remplacé par l'export/import de statistiques déjà en place.)*

- **Mode apprentissage progressif** — En fin de quiz, les questions ratées sont reposées automatiquement jusqu'à ce que toutes soient maîtrisées.

- **Résumé "depuis la dernière visite"** — Au lancement, afficher un bandeau indiquant depuis combien de jours l'utilisateur n'a pas joué.

- **Graphique de progression par fiche** — Sur la heatmap, au clic sur une cellule, afficher un mini-graphique montrant l'évolution du score sur les 5 dernières sessions.

- **Indicateur de régularité (streak)** — Un KPI "Série en cours" comptant le nombre de jours consécutifs où au moins une session a été jouée.

- **Meilleur score et score moyen par fiche** — Afficher pour chaque fiche son record personnel et sa moyenne globale.

- **Réinitialisation sélective** — Permettre de remettre à zéro une fiche spécifique sans perdre l'historique des autres.

- **Indices progressifs** — Sur les questions texte libre, un bouton "Indice" qui révèle le premier mot ou le nombre de caractères de la réponse.

- **Affichage de la difficulté par question** — Calculer un taux d'échec par question et l'afficher dans la révision avec un indicateur rouge/jaune/vert.

- **Personnalisation du quiz aléatoire** — Permettre de choisir le nombre de questions et les fiches sources du tirage.

- **Mode examen blanc** — Un mode simulant les conditions réelles de l'examen, sans feedback immédiat et avec un seuil de réussite.

- **Signaler une erreur** — Un bouton sur chaque question pour signaler une imprécision, avec un message copié dans le presse-papier.
