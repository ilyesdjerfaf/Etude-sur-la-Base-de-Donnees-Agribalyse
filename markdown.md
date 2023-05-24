# Projet Agribalyse

## Introduction

Dans le cadre du projet de fin semestre, L3 Informatique 2022-2023 à Sorbonne Université, de module IA & DATA SCIENCE, nous réalisons une étude sur la base de données Agribalyse (v3.1).

**Qu'est-ce qu'Agribalyse ?** Agribalyse est une base de données de référence des indicateurs d’impacts environnementaux des produits agricoles produits en France et des produits alimentaires consommés en France.

**Contenu des données :** Les données Agribalyse sont composées de trois fichiers CSV :

- AGRIBALYSE3-synthese.csv : contient des informations détaillées sur les différents produits alimentaires, ainsi que leurs impacts environnementaux.

- AGRIBALYSE3-etapes.csv : similaire à "synthese", mais contient les impacts sur l'environnement pendant chaque étape de production d'un produit alimentaire.

- AGRIBALYSE3-ingredients.csv : contient des informations détaillées sur les ingrédients de chaque produit alimentaire, ainsi que les mesures des impacts de chaque ingrédient sur l'environnement.

Dans cette étude, nous abordons deux problématiques différentes avec deux formes d'apprentissage différentes :

# Projet Agribalyse (v3.1)

## Introduction

Dans le cadre du projet de fin semestre, L3 Informatique 2022-2023 à Sorbonne Université, de module IA & DATA SCIENCE, nous réalisons une étude sur la base de données Agribalyse (v3.1).

**Qu'est-ce qu'Agribalyse ?** Agribalyse est une base de données de référence des indicateurs d’impacts environnementaux des produits agricoles produits en France et des produits alimentaires consommés en France.

Les données disponibles dans Agribalyse se composent de trois fichiers CSV :

- AGRIBALYSE3-synthese.csv : contient des informations détaillées sur les différents produits alimentaires, ainsi que des impacts environnementaux de ces derniers.
- AGRIBALYSE3-etapes.csv : similaire à "synthese", mais contient les impacts sur l'environnement pendant chaque étape de production d'un produit alimentaire.
- AGRIBALYSE3-ingredients.csv : contient des informations détaillées sur les ingrédients de chaque produit alimentaire, ainsi que les mesures des impacts de chaque ingrédient sur l'environnement.

Nous allons aborder deux problématiques différentes avec deux formes d'apprentissage distinctes :

1. Apprentissage supervisé : Prédiction de l'impact environnemental des produits alimentaires.
2. Apprentissage non supervisé : Analyse des Méthodes de Normalisation - Min-Max et StandardScalar - sur la Performance des Algorithmes Non Supervisé pour voir l'Impact Environnemental des types d'Emballages dans l'Industrie Agroalimentaire et les Effets toxicologiques sur la santé humaine : substances non cancérogènes

Dans le cadre de ce projet, nous nous concentrerons sur le fichier AGRIBALYSE3-synthese.csv.

## Problème 1 : Apprentissage supervisé - Prédiction de l'impact environnemental des produits alimentaires

### Nettoyage de la base de données

Avant d'effectuer l'apprentissage supervisé, nous allons nettoyer la base de données. Après avoir étudié les colonnes de AGRIBALYSE3-synthese.csv, nous avons décidé de supprimer les attributs suivants, car ils ne seront pas utiles lors de la classification :

- Code AGB et Code CIQUAL : ces codes ne sont pas très utiles pour prédire l'impact environnemental d'un produit alimentaire.
- Nom du produit FR/EN (LCI) : il s'agit d'un nom différent pour chaque produit, comme un identifiant, et cette colonne est inutile.
- Code saison : la plupart des produits ont un code saison égal à 2, ce qui rend cette variable peu informative.
- Code avion : la plupart des produits ont un code avion égal à 0, ce qui rend cette variable peu informative.
- DQR : Data Quality Ratio indique le niveau de confiance que l'on peut avoir dans le score.
- Livraison, Matériau d'emballage, Préparation, Groupe d'aliment et Sous-groupe d'aliment.

Nous conserverons uniquement les 16 indicateurs qui impliquent le calcul du Score EF.

Ensuite, nous supprimerons les colonnes qui peuvent être déduites à partir des autres en utilisant la matrice de corrélation (avec une forte corrélation).

### Création des labels

Nous allons créer des labels pour associer à chaque produit de notre dataset. L'attribut "Score Unique EF" est une caractéristique qui permet de savoir quel est l'impact environnemental d'un produit (plus le score est bas, plus son impact sur l'environnement est faible). Afin de transformer notre problème en un problème d'apprentissage supervisé, nous allons créer des labels en fonction de ce score.

1. Calculer un seuil égal à la moyenne des scores de tous les produits. Ce seuil nous permettra de distinguer les bons scores des mauvais.
2. Si le score EF d'un produit est inférieur au seuil, nous lui attribuons le label 1 (ce qui signifie que son impact environnemental est faible).
   Sinon, nous lui attribuons le label -1 (ce qui signifie que son impact environnemental est considérable).

### Analyse des performances de la classification

Nous analyserons le taux de bonne classification avec les différents classifieurs supervisés que nous avons implémentés pendant le semestre.

## Problème 2 : Apprentissage Non-Supervisé : Analyse des Méthodes de Normalisation - Min-Max et StandardScalar - sur la Performance des Algorithmes Non Supervisé pour voir l'Impact Environnemental des types d'Emballages dans l'Industrie Agroalimentaire et les Effets toxicologiques sur la santé humaine : substances non cancérogènes

### Introduction

L'analyse des méthodes de normalisation est une étape cruciale dans le processus d'exploration et de traitement des données, en particulier lorsqu'il s'agit de problèmes non supervisés tels que la classification non supervisée ou le clustering. La normalisation des données vise à mettre les variables à une échelle comparable, ce qui peut améliorer les performances des algorithmes non supervisés en permettant une meilleure comparaison et une meilleure discrimination des données.

### Problématique

La question qui se pose est de savoir quel impact la méthode de normalisation choisie, en particulier la normalisation Min-Max vue en cours et la normalisation StandardScaler, peut avoir sur la performance des algorithmes non supervisés. Chaque méthode de normalisation a ses avantages et ses limites, et il est important de comprendre comment elles affectent les résultats des algorithmes non supervisés.

### Réalisation

Pour répondre à cette problématique, nous réaliserons une étude comparative en appliquant différentes méthodes de normalisation sur un ensemble de données spécifique. Nous utiliserons des algorithmes non supervisés tels que le clustering, par exemple avec l'algorithme K-moyennes développé en cours, et évaluerons les performances de ces algorithmes en fonction des différentes méthodes de normalisation.

Nous comparerons la normalisation Min-Max, qui ramène les valeurs de chaque variable à l'intervalle [0, 1], avec la normalisation StandardScaler, qui standardise les données en les centrant autour de zéro et en les mettant à l'échelle en fonction de l'écart-type. Nous mesurerons les performances des algorithmes non supervisés en termes de précision du clustering, de séparation des clusters et d'autres métriques pertinentes.

Cette étude nous permettra de mieux comprendre l'impact des méthodes de normalisation sur les résultats des algorithmes non supervisés et de fournir des recommandations sur la méthode de normalisation à privilégier en fonction des caractéristiques spécifiques du jeu de données et des objectifs de l'analyse non supervisée.

### Comparaison

À la fin de cette étude, nous comparerons également les résultats de notre algorithme de clustering K-moyennes développé en interne avec les résultats de l'algorithme K-means de la bibliothèque scikit-learn. Cette comparaison nous permettra d'évaluer la performance de notre algorithme par rapport à une implémentation standard et de vérifier la cohérence de nos résultats avec ceux obtenus par une méthode largement utilisée et validée.

---

Ce fichier Markdown décrit les problématiques que nous aborderons dans le projet Agribalyse (v3.1) et les approches d'apprentissage supervisé et non supervisé que nous adopterons pour les résoudre. Il fournit également une brève introduction à Agribalyse et explique les données que nous utiliserons, ainsi que les étapes de nettoyage et d'analyse que nous entreprendrons.

Pour plus de détails sur chaque problème, les méthodologies utilisées et les résultats obtenus, veuillez vous référer au notebook et au poster inclus dans le dépôt.

Merci d'avoir consulté ce fichier et bonne exploration des données Agribalyse !
