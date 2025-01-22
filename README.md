Clustering et Analyse de Sentiments des Critiques de Livres Amazon

Description du projet

Ce projet vise à analyser un ensemble de critiques de livres collectées sur Amazon en appliquant des techniques de clustering. L'algorithme K-Means a été utilisé pour regrouper ces critiques en clusters homogènes selon des critères sémantiques similaires.

Objectifs du projet

Clustering de critiques de livres : Regrouper efficacement un grand nombre de critiques pour identifier des tendances communes.

Gestion de grandes masses de données : Utilisation de technologies Big Data telles que Hadoop et Mahout pour traiter de grandes quantités de données textuelles.

Amélioration de l'expérience utilisateur : Faciliter la classification automatique des critiques afin d'optimiser les recommandations de livres.

Technologies utilisées

Apache Mahout : Utilisé pour l'implémentation de l'algorithme K-Means.

Hadoop HDFS : Stockage et traitement distribué des données.

MapReduce : Traitement parallèle des données textuelles.

Langage de programmation : Java, Bash

Dataset

Le dataset est constitué de 1 631 critiques de livres collectées sur Amazon, au format texte (UTF-8). Ces critiques varient en longueur, vocabulaire et style, ce qui rend leur analyse complexe.

Étapes de prétraitement

Nettoyage des données : Suppression du contenu web, ponctuation, chiffres et caractères spéciaux.

Normalisation du texte : Conversion en minuscules, stemming, suppression des stop words.

Tokenisation : Fractionnement du texte en mots individuels.

Extraction des caractéristiques : Construction d'une matrice TF-IDF.

Conversion en SequenceFile : Format utilisé par Mahout pour le traitement distribué.

Vectorisation des données : Transformation des textes en vecteurs numériques.

Stockage sur HDFS : Chargement des données prétraitées dans Hadoop.

Implémentation de l'algorithme K-Means

Choix de l'algorithme : Utilisation de K-Means avec distance cosinus.

Initialisation des centroïdes : Utilisation de k-means++ pour une meilleure convergence.

Exécution sur Hadoop : Lancement du clustering avec un nombre de clusters fixé à 3.

Analyse des résultats : Extraction des centroïdes finaux et des attributions de clusters.

Défis rencontrés et solutions apportées

Incompatibilités de versions entre Mahout et Hadoop : Alignement des versions selon la documentation officielle.

Conversion de fichiers CSV en SequenceFile : Validation stricte des fichiers avant conversion.

Gestion de la latence sur HDFS : Optimisation de la taille des blocs et configuration de YARN.

Mesure de distance cosinus : Utilisation de TF-IDF pour atténuer l'impact des termes non significatifs.

Résultats obtenus

Le projet a permis de classifier efficacement les critiques de livres en groupes homogènes, ouvrant des perspectives pour des applications dans l'analyse de sentiments, la segmentation de marché et la personnalisation de services.
