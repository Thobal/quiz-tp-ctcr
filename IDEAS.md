# Idées d'amélioration — Quiz TP CTCR

## À réaliser

- **Liens glossaire dans les questions de révision** — Dans l'écran de révision, les mots présents à la fois dans la question et dans le glossaire sont soulignés. Au tap/clic, une infobulle affiche la définition sans quitter l'écran, réduisant les allers-retours.

- **Compteur de sessions du jour sur l'accueil** — Un indicateur discret sous les KPI affichant le nombre de sessions jouées aujourd'hui (ex : "3 sessions aujourd'hui"), pour encourager une pratique quotidienne sans système de streak.


---

## Réalisées

- **Filtrage du glossaire par lettre initiale** — Index A–Z sur la même ligne que le compteur (calé à droite, wrap sur petit écran). Clic sur une lettre filtre les termes commençant par celle-ci ; combinable avec la recherche texte. Les lettres sans résultat sont grisées.

- **Surbrillance du terme recherché dans le glossaire** — Les occurrences du mot saisi dans le champ de recherche sont mises en évidence (fond bleu translucide) dans les titres et définitions affichés.

- **Compteur de termes dans l'en-tête du glossaire** — Affiche le nombre total de termes et, quand un filtre de recherche est actif, le nombre de résultats correspondants (ex : "5 / 42 termes").

- **Message de confirmation après un export réussi** — Toast en sur-impression avec barre de progression se vidant en 5 secondes, affiché après un export JSON ou PDF réussi.

- **Tri alphabétique optionnel dans le glossaire** — Bouton bascule pour trier les termes du glossaire par ordre alphabétique (ou dans l'ordre d'apparition par défaut).

- **Infobulle explicative sur le switch Strict / Yolo** — Redondant avec le message affiché lors de l'activation du mode Yolo, qui explique déjà le comportement du mode.

- **Masquage des réponses dans l'écran de révision** — Proche du "Mode entraînement sans impact sur les statistiques" déjà rejeté ; s'auto-tester visuellement sans lancer de quiz représente une complexité d'interface pour un bénéfice limité.

- **Import de statistiques par glisser-déposer** — Le bouton d'import existant couvre largement le besoin ; le drag-and-drop est un confort marginal peu justifié pour une action occasionnelle.

- **Infobulle sur les cellules de la heatmap** — "Graphique de progression par fiche — Sur la heatmap, au clic sur une cellule" est déjà rejeté ; une infobulle date + score par cellule relève du même principe de sur-détail de la heatmap.

- **Bouton "Retour en haut" dans l'écran de révision** — Bouton ↑ fixe en bas à droite, apparaissant après 250px de défilement, uniquement quand l'écran de révision est actif.

- **Explication affichée dans le feedback de réponse** — Déjà implémenté : `explHtml` est injecté dans le feedback aussi bien en cas de bonne que de mauvaise réponse (via `.expl-text`).

- **Navigation entre fiches dans l'écran de révision** — Boutons ‹ / › alignés à droite sur la ligne du titre, désactivés automatiquement sur la première et la dernière fiche.

- **Panneaux de signalisation dans "Mes 25 dernières erreurs"** — Pour les questions ayant un panneau associé, le SVG du panneau est affiché dans la carte d'erreur. Le champ `panel` est stocké dans `wrongHistory`.

- **Infobulles explicatives sur les barres de KPI de l'accueil** — Au survol (desktop) ou tap (mobile), une infobulle explique le calcul de chaque indicateur : "Maîtrise des fiches travaillées" (ratio bonnes réponses / questions posées sur les fiches jouées) et "Maîtrise globale" (moyenne sur les 20 fiches, non-jouées à 0 %).

- **Réinitialisation complète des données** — Bouton dans l'écran des statistiques (avec double confirmation) pour effacer intégralement toutes les données localStorage : scores, historique d'erreurs, sessions, paramètres.

- **Bouton de réinitialisation de l'historique des erreurs** — Bouton "Effacer l'historique" affiché en haut de la liste des 25 erreurs (avec confirmation), visible uniquement quand la liste n'est pas vide.

- **Date et heure de la dernière session dans les statistiques** — `s.lastSessionAt = Date.now()` enregistré à chaque session. Affiché sous le titre "Statistiques" : "Dernière session : le JJ/MM/YYYY à HH:MM".

- **Message d'encouragement contextuel en fin de quiz** — Déjà implémenté : 6 titres contextuels (`'À retravailler…'` → `'Excellent !'`) affichés selon le score via `score-title`.

- **Historique des erreurs étendu à 25** — Limite portée de 20 à 25 entrées dans `wrongHistory`. Le bouton "Mes 20 dernières erreurs" renommé en "Mes 25 dernières erreurs".

- **Manifeste PWA pour l'installation sur l'écran d'accueil** — Meta tags Apple (standalone, theme-color, titre) et manifeste injecté dynamiquement via Blob URL avec icône SVG. Installation possible sur Android (bannière Chrome) et iOS (Partager → Sur l'écran d'accueil).

- **Réduction de la taille du fichier** — Suppression des attributs inutiles (`version`, `xmlns`, `xmlns:xlink`) des SVG inline et arrondi des coordonnées à 2 décimales. Factorisation du calcul de maîtrise globale dupliqué (`computeGlobalMastery`). Fichier réduit de ~373 Ko à ~359 Ko.

- **Tri des fiches sur l'accueil** — Sélecteur permettant de trier les fiches par numéro ou par score croissant (fiches non travaillées en premier). Animation FLIP lors du réordonnancement. Le score s'affiche sur chaque bouton en mode tri par score. Les badges "À prioriser" sont masqués en mode score (redondants). La grille est recalculée à chaque retour sur l'accueil pour refléter les scores mis à jour. Le tri choisi est mémorisé dans le localStorage.

- **Barre de progression pendant le quiz** — Un compteur "Question X / 10" est affiché dans le bandeau supérieur du quiz.

- **Partage des statistiques PDF** — Le bouton "Exporter en PDF" détecte si l'API Web Share supporte les fichiers (mobile). Si oui, propose une modale "Partager…" ou "Télécharger". Sinon, déclenche le téléchargement directement.

- **Taux de maîtrise global affiché sur l'accueil** — Sous le titre, un chiffre synthétique affiche le pourcentage de maîtrise moyen sur l'ensemble des fiches travaillées (basé sur les 5 dernières sessions par fiche).

- **Vue hebdomadaire des scores dans les statistiques** — Tableau affichant semaine par semaine les valeurs des deux jauges (fiches travaillées / maîtrise globale), avec évolution et barres de couleur. Remplace le bloc "Dernières sessions".

- **Fiche source affichée pendant un quiz aléatoire ou thématique** — Déjà implémenté : le bandeau affiche "Quiz aléatoire · Question X — Fiche Y" ou "Thématique · … · Question X — Fiche Y".

- **Retour haptique sur mobile** — ~~Supprimé~~ : fonctionnalité jugée plus gênante qu'utile.

---

## Rejetées
*(conservées pour mémoire — ne pas reproposer)*

- **Score médian dans le tableau hebdomadaire** — Le tableau est déjà chargé sur mobile ; la médiane apporte peu de valeur supplémentaire par rapport à la lecture directe des valeurs semaine par semaine.

- **Compte à rebours avant l'examen** — La date d'examen est connue de l'utilisateur ; un compteur de jours restants apporte peu de valeur dans un outil centré sur la révision active.

- **Masquage des fiches maîtrisées sur l'accueil** — Le tri par score existant suffit à identifier les fiches prioritaires ; masquer complètement les fiches maîtrisées risque de donner une vision incomplète de la progression globale.

- **Progression du glossaire mémorisée** — Nécessite de tracer chaque ouverture de définition dans le localStorage, complexifiant le modèle de données pour un apport motivationnel limité.

- **Export des statistiques au format CSV** — L'export JSON existant couvre déjà le besoin de sauvegarde ; un format CSV supplémentaire représente une complexité disproportionnée pour un usage marginal.

- **Rappel du mode YOLO actif sur l'accueil** — Le switch YOLO est visible dans l'en-tête du quiz et son activation déclenche déjà un message explicatif ; un rappel supplémentaire sur l'accueil serait redondant.

- **Rappel de sauvegarde dans l'écran des statistiques** — La pastille d'export (badge avec le nombre de sessions non sauvegardées) remplit déjà ce rôle de manière plus compacte et précise.

- **Taux de réussite dans "Mes 25 dernières erreurs"** — Information déjà accessible dans les statistiques ; l'en-tête de la liste d'erreurs n'est pas le lieu adapté pour ce KPI.

- **Animation de confirmation sur la bonne réponse** — Le feedback visuel existant (couleur verte + texte) est suffisant ; une animation supplémentaire risquerait d'être perçue comme distrayante lors d'une révision rapide.

- **Nombre de questions posées par fiche dans les statistiques** — La heatmap est déjà dense ; ajouter un compteur de questions par cellule surchargerait visuellement l'écran sans apport décisionnel significatif.

- **Fermeture du toast d'export au clic** — Le toast disparaît automatiquement en 5 secondes ; permettre de le fermer au clic représente une complexité d'interaction pour un gain de confort marginal.

- **Badge "Fiche N" sur les cartes d'erreur** — Le numéro de fiche source sur les cartes d'erreur apporte peu de valeur ; l'utilisateur reconnaît généralement la question sans avoir besoin de ce repère.

- **Bouton de partage du lien de l'application** — L'URL de l'application est fixe et facile à retrouver ; un bouton dédié représente une complexité d'interface disproportionnée pour un usage très occasionnel.

- **Animation d'expansion des cartes du glossaire** — Ouverture et fermeture animées via `grid-template-rows: 0fr → 1fr` pour une transition parfaitement fluide quelle que soit la hauteur de la définition.

- **Infobulle sur les boutons de thème du quiz thématique** — Redondant : le nombre de questions disponibles par thème est déjà affiché directement à l'écran.

- **Raccourci vers le glossaire depuis l'écran de révision** — L'accueil est accessible en un tap depuis n'importe quel écran ; le détour par l'accueil pour atteindre le glossaire représente une friction négligeable.

- **Nombre de termes sur le bouton "Glossaire" de l'accueil** — Information de faible valeur ajoutée ; le nombre de termes n'aide pas l'utilisateur à décider d'ouvrir le glossaire.

- **Tri du glossaire mémorisé dans le localStorage** — Sans objet : le glossaire est systématiquement affiché par ordre alphabétique, il n'y a pas de tri à mémoriser.

- **Mise en évidence de la semaine en cours dans le tableau de progression** — La semaine courante est toujours la première ligne du tableau ; la surligner n'apporterait aucune valeur.

- **Persistance de la dernière fiche consultée en révision** — La grille étant limitée à 20 fiches, retrouver visuellement la dernière fiche consultée ne représente pas de friction significative.

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

- **Graphique comparatif des scores par fiche** — Un graphique en barres horizontales affichant le score moyen (5 dernières sessions) de chaque fiche travaillée, triées par score croissant. Permet d'identifier d'un coup d'œil les fiches les plus faibles sans parcourir la heatmap.

- **Lecture audio des questions** — Bouton pour faire lire la question à voix haute via l'API Web Speech. Impact limité (usage bureau majoritaire, voix de synthèse peu adaptée aux termes techniques).

- **Filtre par fiche dans "Mes 20 dernières erreurs"** — Sélecteur pour n'afficher que les erreurs d'une fiche spécifique. Utile pour cibler une révision sur une fiche précise sans être distrait par les autres.

- **Résumé de toutes les explications en fin de quiz** — Section "Explications" listant les explications de chaque question y compris les bonnes réponses, pas seulement les erreurs.

- **Recherche textuelle dans l'écran de révision** — Champ de recherche pour trouver rapidement une question contenant un mot-clé précis.

- **Performance par thème dans les statistiques** — Regrouper les résultats par thème transversal (signalisation, temps de repos, chronotachygraphe…) plutôt que seulement par fiche.

- **Comparaison avec la session précédente sur l'écran de résultats** — Badge +X / −X points par rapport à la dernière session jouée sur la même fiche.

- **Raccourcis clavier pendant le quiz** — Répondre et naviguer au clavier (Entrée, flèches). Gain de fluidité sur ordinateur, mais impact limité sur mobile qui est le support principal.

- **Chronomètre de session** — Mesurer le temps total passé sur un quiz et l'afficher dans les résultats. Apport discutable car le temps varie selon les interruptions, pas seulement la vitesse de réponse.

- **Dernière date de jeu sur les boutons de fiche** — Afficher la date de dernière session sous chaque fiche. Information déjà accessible dans les statistiques, doublon peu justifié.

- **Export d'une session en image** — Générer une image PNG du récapitulatif en fin de quiz. Complexité d'implémentation (canvas) élevée pour un usage occasionnel.

- **Mise en évidence des questions jamais tombées** — Marquer dans l'écran de révision les questions jamais tirées en quiz. Non rétroactif : tous les utilisateurs existants verraient toutes leurs questions marquées comme jamais vues.

- **Comparaison du score par rapport à sa propre moyenne** — Sur l'écran de résultats, indiquer si le score est au-dessus ou en dessous de sa moyenne habituelle sur cette fiche.
- **Taille de police ajustable pour les questions** — Un sélecteur petit / moyen / grand pour adapter la taille du texte des questions.

- **Copier une question dans le presse-papier** — Sur l'écran de révision, un petit bouton pour copier la question et sa réponse en texte brut, pratique pour étudier dans une autre appli.

- **Affichage des explications après une bonne réponse** — Option pour afficher également l'explication lorsque la réponse est correcte, pas seulement en cas d'erreur.

- **Filtre par maîtrise dans l'écran de révision** — Sélecteur pour n'afficher que les fiches en dessous d'un seuil de score (ex. < 50 %, < 70 %). Le tri par score existant sur l'accueil couvre déjà ce besoin de manière plus élégante.

- **Nombre de questions par fiche affiché sur l'accueil** — Inutile : toutes les fiches ont exactement 10 questions.

- **Statistiques de régularité : jours actifs par semaine** — Colonne dans le tableau de progression hebdomadaire. Redondant avec le nombre de fiches travaillées pour un usage solo.

- **Mini-résumé des erreurs sur l'écran de résultats** — Les erreurs sont déjà accessibles immédiatement dans "Mes 20 dernières erreurs" sur l'écran de révision.

- **Panneaux de signalisation affichés dans l'écran de révision** — Déjà implémenté : le panneau SVG est affiché pour chaque question qui en possède un (ligne ~3962).

- **Réorganisation manuelle des fiches par glisser-déposer** — Complexité d'implémentation (drag & drop natif ou bibliothèque) disproportionnée par rapport au bénéfice ; les tris par numéro et par score couvrent l'essentiel.

- **KPI "Questions vues"** — Nécessiterait de journaliser chaque question tirée individuellement, ce qui alourdirait les données stockées pour un apport limité.

- **Aide-mémoire PDF par fiche** — L'écran de révision remplit déjà ce rôle ; générer un PDF depuis une page HTML mono-fichier est complexe sans bibliothèque externe.

- **Mode plein écran pendant le quiz** — L'API Fullscreen est peu fiable sur mobile (iOS ne la supporte pas) et le gain est négligeable sur les usages principaux.

- **Annotation personnelle sur une question** — Complexité de l'interface d'édition inline et risque de pollution visuelle dans l'écran de révision.

- **KPI "Total de sessions jouées"** — Information disponible indirectement via le tableau de progression hebdomadaire ; apport limité en tant que KPI isolé.

- **Indicateur visuel "jouée aujourd'hui"** — Redondant avec le tri par score et la heatmap d'ancienneté ; la valeur ajoutée ne justifie pas la complexité.

- **Affichage des explications dans l'écran de révision** — Alourdit visuellement les cartes, surtout pour les explications longues ; l'écran de révision doit rester aéré.

- **Ordre aléatoire des réponses dans les QCM** — Inapplicable : le quiz ne contient aucune question QCM, uniquement du texte libre, Vrai/Faux et Oui/Non.

- **Objectif de score personnalisable** — Seuil cible visible sur les jauges et boutons de fiche. Complexité de paramétrage peu justifiée pour un usage personnel.

- **Partage du score par message** — Bouton "Partager mon score" via API Clipboard ou Web Share. L'export PDF existant couvre déjà le besoin de partage de statistiques.

- **Thème clair / sombre** — Basculer entre thème sombre et thème clair. L'application étant utilisée principalement sur mobile, le thème sombre est déjà bien adapté ; la complexité de maintenance d'un second thème n'est pas justifiée.
- **Zoom sur les panneaux de signalisation** — Les panneaux sont déjà suffisamment lisibles sur les écrans modernes et sont également visibles dans l'écran de révision.
- **Record personnel affiché sur l'écran de résultats** — En fin de quiz de fiche, indiquer si le score obtenu est le meilleur jamais réalisé sur cette fiche.
- **Compteur de fiches maîtrisées sur l'accueil** — L'information est déjà partiellement couverte par le taux de maîtrise global affiché sous le titre.

- **Badges de niveau par fiche (Bronze / Argent / Or)** — Dimension gamifiée peu adaptée à un outil de révision professionnel ; le score affiché en mode tri par score couvre déjà ce besoin.

- **Filtre par thématique sur l'accueil** — Complexité d'interface (sélecteur supplémentaire) disproportionnée ; le quiz thématique existant permet déjà de cibler un thème précis.

- **Synthèse des erreurs par thème en fin de quiz** — Les erreurs sont déjà accessibles dans "Mes 20 dernières erreurs" ; un tableau par thème ajouterait de la complexité pour un apport limité.

- **Raccourci "Reprendre la dernière fiche"** — La grille étant limitée à 20 fiches, retrouver visuellement la dernière fiche jouée ne représente pas de friction significative.

- **Indicateur visuel de maîtrise sur les boutons en mode tri par numéro** — Redondant avec le mode tri par score qui affiche déjà le niveau de maîtrise ; ajouter une information supplémentaire en mode numéro surcharge inutilement l'interface.

- **Couleur dégradée sur l'anneau de score de l'écran de résultats** — L'anneau a déjà sa propre logique de couleur ; appliquer scoreColor() serait une cohérence cosmétique de faible valeur ajoutée.

- **Résumé de la semaine courante sur l'accueil** — L'information est déjà accessible dans le tableau de progression hebdomadaire des statistiques ; la dupliquer sur l'accueil serait redondant.

- **Normalisation des accents et de la casse pour la validation des réponses libres** — Déjà implémenté : la fonction `normalize()` applique `toLowerCase()` + suppression des accents sur toutes les validations de réponses.

- **Confirmation avant de quitter un quiz en cours** — Un quiz se termine en quelques minutes et la perte de progression est anecdotique ; la modale ajouterait une friction inutile à chaque retour accidentel.

- **Ordre aléatoire des questions dans un quiz de fiche** — Difficulté de mise en œuvre du toggle sans surcharger l'interface ; l'ordre fixe favorise une progression méthodique par fiche.

- **Compte à rebours optionnel par question** — Risque d'ajouter du stress contre-productif lors de la révision ; le mode examen blanc (déjà rejeté) couvrait ce besoin plus complètement.

- **Mode entraînement sans impact sur les statistiques** — Complexité de maintenance d'un double chemin de code (avec/sans enregistrement) pour un usage occasionnel ; effacer les données d'une session via l'import/export existant couvre déjà ce besoin.

- **Swipe horizontal pour passer à la question suivante sur mobile** — Le bouton "Question suivante" est suffisamment accessible ; le swipe introduit un risque de déclenchement accidentel pendant la saisie.

- **Distinction visuelle des fiches jamais jouées sur l'accueil** — En mode tri par score, les fiches non jouées affichent déjà "—" ce qui les distingue clairement ; ajouter une opacité différente en mode numéro serait redondant.

- **Score coloré sur les boutons de fiche en mode tri par score** — Déjà implémenté : la fonction `scoreCouleur()` applique le même dégradé continu rouge→vert à la valeur affichée sur chaque bouton.

- **Affichage de la bonne réponse dans le feedback en mode YOLO** — Déjà implémenté : le feedback affiche "⚡ Sauvé par le mode YOLO — en mode strict, la réponse attendue était : …" lorsqu'une mauvaise réponse est sauvée.

- **Indicateur de progression par points colorés** — La barre de progression et le texte "Question X / 10" existants sont suffisants ; ajouter 10 cercles surchargerait le bandeau sans apport significatif.

- **Défilement automatique vers la carte après validation** — Le problème ne se produit pas en pratique, notamment grâce à l'affichage du panneau à droite de la question qui réduit la hauteur de la carte.

- **Résumé du score par type de question sur l'écran de résultats** — La répartition Vrai/Faux / Oui/Non / texte libre est déséquilibrée selon les fiches, rendant la comparaison peu fiable ; l'apport analytique ne justifie pas la complexité.

- **Bandeau "Nouvelle version appliquée"** — Information de faible valeur ajoutée ; l'utilisateur n'a généralement pas besoin de savoir qu'une mise à jour a eu lieu.

- **Indicateur de connexion perdue** — L'application étant une page statique sans fonctionnalités temps réel, la perte de connexion n'a d'impact que si l'utilisateur tente de recharger, ce qui est déjà géré par le navigateur.

- **Mémorisation du dernier onglet actif dans les statistiques** — L'écran des statistiques est court à parcourir ; le gain de confort ne justifie pas la complexité de persistance.

- **Retour haptique discret sur bonne réponse** — Le retour positif est déjà assuré visuellement (✅ vert) ; ajouter une vibration sur les bonnes réponses risque d'être perçu comme intrusif.

- **Scores des sessions précédentes sur l'écran de résultats** — Information déjà accessible dans le tableau hebdomadaire des statistiques et via la heatmap ; ajouter une ligne de scores sous l'anneau surchargerait l'écran de résultats.

- **Date de la première session dans les statistiques** — Apport informationnel faible ; la date de première session n'est pas actionnable et l'écran de statistiques est déjà dense.

- **Numéro de question (Q1–Q10) dans l'écran de révision** — Les questions sont déjà présentées dans l'ordre ; ajouter un label numérique n'apporte pas de valeur fonctionnelle.

- **Compteur de fiches jamais pratiquées dans les statistiques** — Information redondante avec la grille de l'accueil qui distingue déjà visuellement les fiches non pratiquées (score "—" en mode tri par score).

- **Indicateur de récurrence dans "Mes 25 dernières erreurs"** — L'historique étant limité à 25 entrées, la récurrence d'une même question y est déjà visible à l'œil ; un badge chiffré ajouterait de la complexité pour un gain limité.

- **Colorisation des cellules du tableau de progression hebdomadaire** — Déjà implémenté : `weeklyScoreColor()` applique le dégradé rouge→vert à la barre et à la valeur textuelle dans `renderWeeklyHistory()`.

- **KPI "Total de questions répondues (all-time)"** — Information peu actionnable ; l'utilisateur ne peut pas agir dessus, contrairement aux taux de maîtrise.

- **Bouton "Tester cette fiche" dans l'écran de révision** — Le bouton de démarrage de quiz sur l'accueil est suffisamment accessible ; ajouter un second point d'entrée dans la révision fragmenterait le parcours utilisateur.

- **Détection automatique de nouvelle version** — L'application est un fichier statique unique ; la gestion du cache navigateur et le rechargement manuel suffisent pour ce cas d'usage.

- **Étiquette thématique sur les boutons de fiche** — Nécessiterait d'ajouter des métadonnées thématiques pour les 20 fiches ; la numérotation est déjà mémorisée par l'utilisateur régulier et le quiz thématique existant couvre le besoin d'accès par thème.

- **Mise à jour du titre de l'onglet avec le taux de maîtrise** — Apport cosmétique limité ; l'application est généralement ouverte dans un onglet dédié et le titre n'est pratiquement jamais lu.

- **Fiche la plus faible mise en avant sur l'accueil** — Le tri par score existant sur l'accueil remplit déjà ce rôle de manière plus complète en classant toutes les fiches par niveau de maîtrise.

- **Animation de transition entre les écrans** — Même à 33 ms, l'effet est imperceptible ; au-delà, il ralentit la navigation. Le gain visuel ne justifie pas l'ajout.

- **Mise en page améliorée sur tablette** — L'usage principal est mobile ; optimiser pour tablette représente une complexité de maintenance disproportionnée par rapport à l'usage réel.

- **Résumé textuel des statistiques copiable** — L'export PDF existant couvre déjà le besoin de partage ; un doublon texte apporterait peu de valeur supplémentaire.
