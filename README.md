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

### Références
#### Articles Scientifiques
Corcoran, J., & Zahnow, R. (2022). Weather and crime: a systematic review of the empirical literature. Crime Science, 11(1). https://doi.org/10.1186/s40163-022-00179-8
Jenga, K., Catal, C., & Kar, G. (2023). Machine learning in crime prediction. Journal of Ambient Intelligence and Humanized Computing, 14(3), 2887–2913. https://doi.org/10.1007/s12652-023-04530-y
Saeed, R. M., & Abdulmohsin, H. A. (2023). A study on predicting crime rates through machine learning and data mining using text. Journal of Intelligent Systems, 32(1). https://doi.org/10.1515/jisys-2022-0223

#### Données
Actes criminels - Site web des données ouvertes de la Ville de Montréal. (2023, Septembre 5). https://donnees.montreal.ca/dataset/actes-criminels
Limite des secteurs de poste de quartier de police - Site web des données ouvertes de la Ville de Montréal. (2022). https://donnees.montreal.ca/dataset/limites-pdq-spvm
Montreal Crime data. (2021, Aout 24). Kaggle. https://www.kaggle.com/datasets/stevieknox/montreal-crime-data
Service de Police de la Ville de Montréal - SPVM. (n.d.). https://spvm.qc.ca/
