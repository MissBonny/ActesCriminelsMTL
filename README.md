# ActesCriminelsMTL
Un projet de science des données prédisant des actes criminels dans la ville de Montréal.

## Introduction
### Contexte du projet
Le projet << Prédiction de la criminalité à Montréal à l'aide des séries temporelles [2015-2022] >> vise à utiliser les données historiques de la criminalité pour développer des modèles prédictifs robustes, en utilisant la science des données et des techniques de séries chronologiques. Les données, provenant du site Web Données ouvertes de la Ville de Montréal, offrent une fenêtre sur les différents actes criminels enregistrés dans la ville, tout en respectant la vie privée des personnes touchées par l'obscurcissement des données.

Ce projet a été mis en œuvre à l'aide de R, RStudio, MySQL, Tableau, RMarkdown et GitHub, afin de naviguer à travers les différentes étapes du cycle de vie des données, de la collecte et du nettoyage des données à la modélisation, la visualisation et la présentation des résultats. L'objectif ultime est de créer deux modèles de prévision robustes pour anticiper la criminalité à Montréal et fournir des recommandations visuelles aux autorités et aux citoyens.

La période à l'étude, de janvier 2015 à décembre 2022, a été choisie pour donner un aperçu détaillé des tendances de la criminalité au cours des dernières années, tout en tenant compte des changements socioéconomiques et des événements mondiaux, comme la pandémie de COVID-19, qui peuvent avoir influencé les taux de criminalité. Les modèles de prévision, y compris le LSTM et l'amplification du gradient, ont été choisis sur la base de recherches préliminaires et d'études de cas similaires dans le domaine de la prévision de la criminalité, afin d'assurer une approche méthodologique robuste et fiable.

Le projet est également guidé par une planification détaillée et une gestion des risques, avec la reconnaissance des défis potentiels tels que les données incomplètes ou biaisées, la pertinence des modèles de prévision et les changements imprévus dans les tendances de la criminalité. En outre, notez que toutes les étapes du projet sont réalisées avec une attention particulière à l'éthique et à la vie privée, en veillant à ce que les données utilisées soient traitées de manière responsable.

### Objectifs du Projet
Concevoir et valider deux modèles prédictifs de science des données, à l'aide de techniques de séries chronologiques, pour anticiper les tendances de la criminalité à Montréal et traduire ces prédictions en visualisations et recommandations pour les autorités et les citoyens.

## Méthodologie

### Approche de Modélisation
L'approche est basée sur deux techniques distinctes de prédiction de séries chronologiques. Le premier, le modèle Gradient Boosting, a été choisi pour sa capacité à optimiser les prédictions en minimisant les erreurs par itérations successives et en ajustant progressivement les prédictions en fonction de la précision. Le second, le modèle de mémoire à long terme (LSTM), un type de réseau neuronal récurrent, a été sélectionné pour sa capacité à gérer les dépendances à long terme dans les séries chronologiques, ce qui est crucial pour comprendre les tendances et les modèles sous-jacents. Ces deux modèles ont été identifiés comme étant performants dans des études antérieures liées à la prédiction de la criminalité, fournissant une base solide pour leur application dans ce contexte particulier.

### Outils et Technologies Utilisés
Une série d'outils et de technologies ont été sélectionnés pour gérer chaque étape du processus analytique. Initialement, l'intention était d'utiliser MySQL pour le nettoyage et l'organisation des données, compte tenu de sa capacité à gérer de grands ensembles de données et de ma familiarité avec SQL. Cependant, en raison des erreurs de chargement rencontrées avec MySQL, il a été décidé de nettoyer et d'explorer les données entièrement dans R. Les modèles de prévision ont été créés et exécutés à l'aide de bibliothèques R spécifiques XGBoost, keras tensorflow. La visualisation des données a été effectuée principalement dans R, bien que l'utilisation de Tableau puisse toujours être envisagée pour des visualisations plus avancées. Pour documenter, suivre et rendre compte des résultats des projets, RMarkdown et GitHub ont été utilisés, assurant une gestion de projet transparente et reproductible.

### Gestion des Données
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
