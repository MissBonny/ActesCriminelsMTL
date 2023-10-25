# ActesCriminelsMTL
Un projet de science des données prédisant des actes criminels dans la ville de Montréal.

## Introduction
### Contexte du projet
Le projet << Prédiction de la criminalité à Montréal à l'aide des séries temporelles [2015-2022] >> vise à utiliser les données historiques de la criminalité pour développer des modèles prédictifs robustes, en utilisant la science des données et des techniques de séries chronologiques. Les données, provenant du site Web Données ouvertes de la Ville de Montréal, offrent une fenêtre sur les différents actes criminels enregistrés dans la ville, tout en respectant la vie privée des personnes touchées par l'obscurcissement des données.

Ce projet a été mis en œuvre à l'aide de R, RStudio, RMarkdown, Python, Jupyter Notebooks, Anaconda et GitHub, afin de naviguer à travers les différentes étapes du cycle de vie des données, de la collecte et du nettoyage des données à la modélisation, la visualisation et la présentation des résultats. L'objectif ultime est de créer deux modèles de prévision robustes pour anticiper la criminalité à Montréal et fournir des recommandations visuelles aux autorités et aux citoyens.

La période à l'étude, de janvier 2015 à décembre 2022, a été choisie pour donner un aperçu détaillé des tendances de la criminalité au cours des dernières années, tout en tenant compte des changements socioéconomiques et des événements mondiaux, comme la pandémie de COVID-19, qui peuvent avoir influencé les taux de criminalité. Les modèles de prévision, y compris le LSTM et l'amplification du gradient, ont été choisis sur la base de recherches préliminaires et d'études de cas similaires dans le domaine de la prévision de la criminalité, afin d'assurer une approche méthodologique robuste et fiable.

Le projet est également guidé par une planification détaillée et une gestion des risques, avec la reconnaissance des défis potentiels tels que les données incomplètes ou biaisées, la pertinence des modèles de prévision et les changements imprévus dans les tendances de la criminalité. En outre, notez que toutes les étapes du projet sont réalisées avec une attention particulière à l'éthique et à la vie privée, en veillant à ce que les données utilisées soient traitées de manière responsable.

### Objectifs du Projet
Concevoir et valider deux modèles prédictifs de science des données, à l'aide de techniques de séries chronologiques, pour anticiper les tendances de la criminalité à Montréal et traduire ces prédictions en visualisations et recommandations pour les autorités et les citoyens.

### Définition du projet (en quoi qu’il consiste)
Créer deux modèles de prévision robuste pour anticiper la criminalité à Montréal, et fournir des recommandations visuelles pour les autorités et citoyens. 
Les données sont fournies par le Site de web des données ouvertes de la Ville de Montréal (2023).
Les données consistent d'un fichier de GEOJSON ou CSV des Actes criminels (2023), et un fichier GEOJSON ou CSV ou SHP des Limites de poste de quartiers (2022). 

### Fichier des Actes Criminels
Le fichier des Actes criminels (2023) est composé d’un un tableau de données en CSV de 22,7 MB, à partir de Janvier 2015 jusqu’à Décembre 2022.

* CATÉGORIE - text ; liste - Introduction; Vol dans / sur véhicule à moteur; vol de véhicule à moteur; Méfait; Vol qualifié; infractions entraînant la mort.
* DATE - date - AAAA-MM-JJ
* QUART - text ; liste - jour : Entre 8h01 et 16h ; soir : Entre 16h01 et minuit ; nuit : Entre 00h01 et 8h
* PDQ - numérique - Numéro du poste de quartier couvrant le territoire où s'est passé l'événement.
* X - coordonnées spatiales - Position géospatiale selon la projection MTM8 (SRID 2950)
* Y coordonnées spatiales - Position géospatiale selon la projection MTM8 (SRID 2950)
* LONGITUDE - coordonnées spatiales - position géographique de l'événement après obfuscation à une intersection selon le référentiel géodésique WGS84
* LATITUDE - coordonnées spatiales - position géographique de l'événement après obfuscation à une intersection selon le référentiel géodésique WGS84

### Fichier des Limites de poste de quartiers
Selon le Site web des données ouvertes de la Ville de Montréal, le fichier des Limites de poste de quartiers (2023) est composé d’un très petit tableau de données (29 rangs), qui compris trois colonnes : 

* _id - numérique - Identifiant
* PDQ - numérique - Numéro du poste de quartier
* NOM_PDQ - texte - Nom du poste de quartier
* wkt - texte - Géométrie sous le format "well-known text" du polygone multiple correspondant au territoire du poste de quartier

### Vie privée
Selon la page Actes criminels - Site de web des données ouvertes de la Ville de Montréal (2023) : 
“Les données ont été obfusquées et modifiées pour garantir le respect à la vie privée et la protection des renseignements personnels :
Localisation : la position géographique de l'événement a été localisée à une des intersections du segment de rue où s'est passé l'événement.
Temporalité : le moment de l'événement est représenté par la date et le quart de travail (ou moment de la journée : jour, soir, nuit) durant lequel l'événement a été enregistré.”

## Planification du projet 
Les risques du projet: 

Qu’il y a des données incomplètes ou biaisées
On sait déjà qu’il manque les crimes liés à l'agression sans mort et les incendies. Je soupçonne que le plus grand groupe de données entre dans ces deux catégories. Bien que j'ai trouvé ces données ailleurs, elles ne correspondent pas au reste des données, donc je vais m'en tenir à ce que j'ai. Si je travaillais pour la Ville de Montréal, j'imagine que j'aurais accès à cette information.

Que les modèles de prévision sont inadéquats
Je suis au début de mon parcours en science des données, il est donc raisonnable de penser que je ne choisirais peut-être pas les modèles les plus performants ou le type d'analyse qui correspond le mieux à ces données. C'est pourquoi j'ai consulté deux articles de revues récents, pour voir quels modèles de science des données ont le mieux fonctionné avec les données sur la criminalité. Bien qu'il y ait eu de nombreuses options, le LSTM / apprentissage profond et le boosting de gradient semblaient bien fonctionner dans les deux articles.

Qu’il y a beaucoup de changements imprévus dans les tendances criminelles
La pandémie a tout changé, y compris les taux de criminalité. Je soupçonne que nous verrons des anomalies qui pourraient rendre les prédictions plus fiables. Je vais chercher à visualiser les dates de couvre-feu, et éventuellement supprimer ces dates du modèle, pour voir si cela fait une différence.
Qu'il y a d'autres facteurs qui ont une incidence sur la criminalité à Montréal

J'ai récemment lu une revue scientifique qui a trouvé une association positive et linéaire entre la température et les taux de criminalité violent (Corcoran & Zahnow, 2022). Ce facteur et d'autres peuvent avoir une incidence sur les taux de criminalité à Montréal et, par conséquent, nécessiter une étude plus approfondie. Si j'ai le temps, j'aimerais voir s'il y a une corrélation positive entre la température et les actes criminels à Montréal, mais ce n'est pas l'objectif de ce projet.

### Tâches
Les tâches sont énumérées dans un GANTT dans le section 'visualisation'. Chaque tâche prend 6 jours, sauf la dernière (Rapportage), qui prend neuf. 
Taches : 

* Importer les données en MySQL
* Nettoyer et regrouper les données
* Ajouter les points de données temporelles
* Combiner les lacunes lorsqu’un crime n’a pas été commis
* Importez les données dans R
* Créer et exécuter modèle #1
* Créer et exécuter modèle #2
* Faire face a les problèmes qui surgissent
* Visualiser les données et les analyses
* Rapportage

## Méthodologie

### Approche de Modélisation
L'approche est basée sur deux techniques distinctes de prédiction de séries chronologiques. Le premier, le modèle Gradient Boosting, a été choisi pour sa capacité à optimiser les prédictions en minimisant les erreurs par itérations successives et en ajustant progressivement les prédictions en fonction de la précision. Le second, le modèle de mémoire à long terme (LSTM), un type de réseau neuronal récurrent, a été sélectionné pour sa capacité à gérer les dépendances à long terme dans les séries chronologiques, ce qui est crucial pour comprendre les tendances et les modèles sous-jacents. Ces deux modèles ont été identifiés comme étant performants dans des études antérieures liées à la prédiction de la criminalité, fournissant une base solide pour leur application dans ce contexte particulier.

### Outils et Technologies Utilisés
Une série d'outils et de technologies ont été sélectionnés pour gérer chaque étape du processus analytique. Initialement, l'intention était d'utiliser MySQL pour le nettoyage et l'organisation des données, compte tenu de sa capacité à gérer de grands ensembles de données et de ma familiarité avec SQL. Cependant, en raison des erreurs de chargement rencontrées avec MySQL, il a été décidé de nettoyer et d'explorer les données entièrement dans R. Les modèles de prévision ont été créés et exécutés à l'aide de bibliothèques R spécifiques XGBoost, keras tensorflow. La visualisation des données a été effectuée principalement dans R, bien que l'utilisation de Tableau puisse toujours être envisagée pour des visualisations plus avancées. Pour documenter, suivre et rendre compte des résultats des projets, RMarkdown et GitHub ont été utilisés, assurant une gestion de projet transparente et reproductible.

## Gestion des Données
Les données proviennent de deux sources principales:

* Les limites des postes de quartier: Ce jeu de données contient des informations sur les différents postes de quartier, y compris leur nom, identifiant et géolocalisation.
* Les actes criminels enregistrés: Cette base de données détaille les différents actes criminels enregistrés à Montréal, comprenant la catégorie du crime, le quart de l'année, les coordonnées géographiques, et la date.

#### Nettoyage et Prétraitement des Données (avec R et XBoost)

* Étape 1: Chargement des données: Les données ont été chargées à l'aide de la bibliothèque readr. Les fichiers CSV ont été spécifiquement lus avec un encodage UTF-8 pour assurer la bonne prise en charge des caractères spéciaux.
* Étape 2: Inspection initiale: Après le chargement des données, une inspection a été effectuée pour comprendre leur structure. Cette étape a révélé la présence de colonnes clés telles que DATE, QUART, et PDQ.
* Étape 3 : Gestion des valeurs manquantes: On a identifié la présence de valeurs manquantes, notamment dans les colonnes de latitude et de longitude. Plutôt que de supprimer ces données, on a choisi de les conserver, car presque chaque secteur (PDQ) avait au moins une entrée (exceptée 5).

#### Manipulation des données (avec R et XBoost)

* Étape 4 Validation croisée pour les séries temporelles: Nous avons utilisé une technique de validation croisée spécifique aux séries temporelles pour entraîner et tester le modèle en divisant la série en plusieurs périodes.
* Étape 5 Entraînement du modèle XGBoost: Un modèle de prévision basé sur XGBoost a été entraîné avec les données, et des prédictions ont été effectuées.
* Étape 6 Analyse des résidus: Nous avons visualisé et analysé les résidus pour évaluer la performance du modèle.

#### Nettoyage et Prétraitement des Données (avec Python, pour un LSTM)

*Étape 1  Chargement des données: Les données ont été chargées à l'aide de la bibliothèque pandas en Python. La prise en charge des formats et des encodages a été gérée automatiquement par la fonction read_csv.
* Étape 2 Inspection initiale : Une fois les données chargées, une première inspection a été réalisée pour comprendre la structure et le format des données.
* Étape 3 Gestion des valeurs manquantes: Après inspection des données, il a été constaté qu’il y avait cinq PDQs manquants. Ces entrées ont été supprimées du jeu de données. De plus, pour une analyse de série temporelle cohérente, nous avons décidé de combler les lacunes pour les dates et heures où aucun crime n'a été enregistré. Cette étape assurait une séquence continue de données pour le modèle LSTM.

#### Manipulation des données (avec Python, pour un LSTM)

* Étape 4 Préparation des données : Les données ont été transformées pour s'adapter à un modèle LSTM de série chronologique. Cela impliquait de normaliser les données et de diviser les données en compartiments d'entraînement et de test.
* Étape 5: Construction et Entraînement du modèle LSTM : Un modèle LSTM a été construit avec Keras, une API de réseaux de neurones en Python. Après avoir défini l'architecture du réseau, le modèle a été entraîné sur les données d'entraînement.
* Étape 6: Évaluation des prévisions : Les prédictions du modèle LSTM ont été comparées aux valeurs réelles de l'ensemble de test pour évaluer sa performance. Des métriques d'évaluation, telles que l'erreur moyenne au carré, l’erreur quadratique moyenne, et le R2, ont été utilisées pour quantifier la précision du modèle.
* Étape 7: Analyse des résidus : Tout comme avec le modèle XGBoost, les résidus entre les valeurs prédites et les valeurs réelles ont été visualisés et analysés pour évaluer la qualité des prévisions du modèle LSTM.

### Validation des Modèles

#### Critères d'évaluation pour les deux modèles (XBoost et LSTM)
La performance des modèles de prédiction de séries chronologiques a été évaluée à l'aide de l'erreur quadratique moyenne (RSME), de l'erreur quadratique moyenne (EMS) et du coefficient de détermination (R^2).

#### Méthode de Validation Croisée (XBoost)
La validation croisée est une technique utilisée pour évaluer les modèles en les divisant en un ensemble d'apprentissage et un ensemble de tests. Pour ce projet, une méthode de validation croisée « Time Series Split » a été utilisée. Contrairement à une validation croisée k-fold traditionnelle, cette méthode est spécialement conçue pour les séries chronologiques où les données sont divisées en plusieurs ensembles d'apprentissage / test en fonction de l'ordre de temps. Cela garantit que l'information du futur n'est pas utilisée pour prédire le passé, maintenant ainsi l'intégrité temporelle des prédictions.

#### Methode de Validation Train-Test (LSTM)
Les données ont été divisées chronologiquement en un ensemble d'entraînement et un ensemble de tests. Cette division garantit que le modèle est formé sur des données antérieures et testé sur des données futures, en respectant l'ordre temporel des événements.

### Progrès Actuels

* Préparation des données : Nous avons réussi à nettoyer et prétraiter notre ensemble de données. Les colonnes contenant des données de type 'character' ont été converties en valeurs numériques afin qu'elles puissent être utilisées dans le modèle XGBoost.
* Visualisations préliminaires des données : On a visualisé les données pour mieux comprendre leur distribution et identifier les tendances potentielles.
* Conversion des données : Grâce à la manipulation des données en R, nous avons transformé notre dataframe en une matrice numérique, prête pour la modélisation.
* Création du modèle XBoost avec R : Nous avons initié la construction du modèle XGBoost. Ce modèle a été choisi en raison de ses performances éprouvées pour les problèmes de prédiction.
* Validation du modèle XBoost avec R: La validité du modèle a été évaluée. Bien que la validation initiale ait montré des résultats prometteurs, des ajustements supplémentaires sont nécessaires pour améliorer la précision.
* Création du modèle LSTM avec Python : Nous avons créé le modèle LSTM avec Python, parce qu’on voulait élargir les compétences Python avec un travail pratique. Il est également largement admis que Python est mieux adapté à l'analyse de réseaux neuronaux, tandis que R excelle avec les visualisations et les tableaux de bord.
* Validation du modèle LSTM avec Python : Le modèle LSTM a été validé, avec des prédictions très précises.

#### Sommaire du progrès avec le modèle XBoost
Après avoir visualisé le graphique des résidus, on a remarqué une anomalie flagrante autour de la date "2022-07". Cela indique que le modèle n'a pas pu bien prédire cette période.
Le RMSE (Root Mean Square Error) pour les données d'entraînement est de 0.004095299, ce qui est assez faible, indiquant que le modèle s'adapte bien aux données d'entraînement. Cependant, le RMSE pour les données de test est de 0.07965863, ce qui est plus élevé que celui des données d'entraînement. Cette différence de performance entre l'entraînement et les données de test pourrait indiquer un surapprentissage du modèle. Le surapprentissage se produit lorsque le modèle est trop complexe et qu'il mémorise les données d'entraînement plutôt que de généraliser à partir de celles-ci.
On va  considérer d'autres méthodes ou d'ajuster les hyperparamètres du modèle XGBoost pour voir si le modèle peut être amélioré. De plus, l'exploration de la cause des résidus élevés autour de la date "2022-07" pourraient fournir des informations précieuses pour améliorer la performance du modèle.

#### Sommaire du progrès avec le modèle LSTM
Les statistiques du modèle LSTM ont montré des performances exceptionnelles du modèle. L'erreur quadratique moyenne est de 0,0004788482177342861, ce qui est très faible. De même, l'erreur moyenne quadratique est de 0,021882600799134597, ce qui indique que les prévisions du modèle sont très proches des valeurs réelles.
Le coefficient de détermination R-squared est de 0.9994642884835777, ce qui suggère que le modèle LSTM a pu expliquer près de 99.95% de la variabilité des données cibles. C'est un indicateur d'une excellente performance du modèle.
Les visualisations de l'ACF et du PACF des résidus montrent qu'il n'y a pas d'autocorrélation significative après le premier lag, indiquant que le modèle a bien capté l'information temporelle présente dans les données. C'est une indication que les résidus sont proches du bruit blanc, ce qui est idéal pour un modèle de prédiction temporelle.
La visualisation des valeurs résiduelles révèle quelques pics notables, suggérant certaines périodes où le modèle n'a pas été aussi précis. Cependant, la majorité des résidus semble être proche de zéro.

### Défis et Solutions

* Erreurs avec MySQL : On n’a pas été en mesure d'obtenir les jeux de données téléchargés dans MySQL, après plusieurs heures. Il a donc été décidé de déplacer le nettoyage et l'optimisation des données vers R, pour économiser du temps et de l'énergie.
* Erreurs de type de données : Lors de nos premières tentatives de création du modèle XGBoost avec R, on a rencontré des erreurs liées au type de données. Ces erreurs ont été résolues en convertissant toutes les colonnes du dataframe en valeurs numériques.
* Optimisation du modèle XBoost : Des travaux supplémentaires seront nécessaires pour optimiser le modèle, notamment en ajustant les hyperparamètres et en s'assurant que le modèle ne surapprend pas.
* Création du modèle LSTM : Nous avons eu plusieurs problèmes autour de la création des données de séries chronologiques avec le LSTM. Nous avons dû redémarrer plusieurs fois avant de trouver quelque chose qui fonctionnait.
* Décisions d’analyse : Il y avait beaucoup de décisions à prendre sur la façon de structurer et d'analyser les données. Cela devient probablement plus facile avec l'expérience, et peut-être un projet moins difficile. Analysons-nous par longitude et latitude, sachant que cela intégrera probablement un biais? Ou est-ce qu'on analyse à un niveau plus élevé, donc le PDQ (id de poste de police), qui généralise davantage les lieux, mais fournit quand même suffisamment d'informations à des fins de dotation? Enfin, nous avons décidé d'opter pour les données de niveau PDQ, laissant la spécificité de l'analyse de longitude et de latitude pour un moment où nous aurons acquis plus d'expérience en science des données.
* Problèmes constants avec RStudio : Chaque jour où je travaillais sur cet ensemble de données, j'avais des problèmes avec RStudio. Certains jours, il ne reconnaissait pas les caractères français. Pour d'autres, cela ne chargerait pas les bibliothèques. Et la plupart du temps, il refusait d’afficher des visualisations dans RMarkdown. Je n'ai pas de solution ici, autre que de continuer à le réinstaller, jusqu'à ce que je trouve une version qui fonctionne de manière cohérente. C'est la première fois en un an que j'ai des problèmes avec RStudio ; c'est pourquoi j'ai choisi d'exécuter mon projet en R, car il s'est avéré si fiable pour moi.

### Comparaison des modèles XBoost et LSTM
Il y a quelques jours, le code R fonctionnait. Puis RStudio a décidé d'arrêter de fonctionner. Je l'ai réinstallé deux fois et il n'analyse toujours pas correctement UTM-8. J'ai donc migré vers Anaconda, et après quelques problèmes supplémentaires lors du chargement de RStudio, cela a fonctionné.
J'ai soumis ce qui fonctionnait (à l'époque) le code R pour le TN 3.
Maintenant, je n'arrive pas à faire fonctionner le code. Je vois des erreurs constantes, je n'arrive pas à résoudre les problèmes, Anaconda ne reconnaît plus RStudio...
Tout ce que je veux faire, c'est comparer les deux modèles, et je ne peux pas, même si je sais très bien que le LSTM a bien mieux fonctionné et avec moins de problèmes.
Malheureusement, je n'ai plus de temps, c'est donc là que nous devrons en rester. Cela me brise le cœur de ne pas pouvoir comprendre cela et de le terminer.

Si on peut corriger le code, on le mettrait à jour dans GitHub.

### Références
#### Articles Scientifiques

* Corcoran, J., & Zahnow, R. (2022). Weather and crime: a systematic review of the empirical literature. Crime Science, 11(1). https://doi.org/10.1186/s40163-022-00179-8
* Jenga, K., Catal, C., & Kar, G. (2023). Machine learning in crime prediction. Journal of Ambient Intelligence and Humanized Computing, 14(3), 2887–2913. https://doi.org/10.1007/s12652-023-04530-y
* Saeed, R. M., & Abdulmohsin, H. A. (2023). A study on predicting crime rates through machine learning and data mining using text. Journal of Intelligent Systems, 32(1). https://doi.org/10.1515/jisys-2022-0223

#### Données

* Actes criminels - Site web des données ouvertes de la Ville de Montréal. (2023, Septembre 5). https://donnees.montreal.ca/dataset/actes-criminels
* Limite des secteurs de poste de quartier de police - Site web des données ouvertes de la Ville de Montréal. (2022). https://donnees.montreal.ca/dataset/limites-pdq-spvm
* Montreal Crime data. (2021, Aout 24). Kaggle. https://www.kaggle.com/datasets/stevieknox/montreal-crime-data
* Service de Police de la Ville de Montréal - SPVM. (n.d.). https://spvm.qc.ca/

#### Journal des activités

* 12, 13, 20, 24 juillet; 1, 3, 17, 24 août; 4, 5, 6, 9, 10, 20, 21 septembre; 4, 5, 6, 16, 17, 19, 20, 22, 23, 24 octobre. (25 jours)
* Nombre d’heures investi ~ 140
