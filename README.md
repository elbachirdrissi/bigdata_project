# Clustering et Analyse de Sentiments des Critiques de Livres Amazon

## Description du projet
Ce projet vise à analyser un ensemble de critiques de livres collectées sur Amazon en appliquant des techniques de clustering. L'algorithme K-Means a été utilisé pour regrouper ces critiques en clusters homogènes selon des critères sémantiques similaires.

## Objectifs du projet
- **Clustering de critiques de livres** : Regrouper efficacement un grand nombre de critiques pour identifier des tendances communes.
- **Gestion de grandes masses de données** : Utilisation de technologies Big Data telles que Hadoop et Mahout pour traiter de grandes quantités de données textuelles.
- **Amélioration de l'expérience utilisateur** : Faciliter la classification automatique des critiques afin d'optimiser les recommandations de livres.

## Technologies utilisées
- **Apache Mahout** : Utilisé pour l'implémentation de l'algorithme K-Means.
- **Hadoop HDFS** : Stockage et traitement distribué des données.
- **MapReduce** : Traitement parallèle des données textuelles.
- **Langage de programmation** : Java, Bash

## Dataset
Le dataset est constitué de **1 631 critiques** de livres collectées sur Amazon, au format texte (UTF-8). Ces critiques varient en longueur, vocabulaire et style, ce qui rend leur analyse complexe.

## Étapes de prétraitement
1. **Nettoyage des données** : Suppression du contenu web, ponctuation, chiffres et caractères spéciaux.
2. **Normalisation du texte** : Conversion en minuscules, stemming, suppression des stop words.
3. **Tokenisation** : Fractionnement du texte en mots individuels.
4. **Extraction des caractéristiques** : Construction d'une matrice TF-IDF.
5. **Conversion en SequenceFile** : Format utilisé par Mahout pour le traitement distribué.
6. **Vectorisation des données** : Transformation des textes en vecteurs numériques.
7. **Stockage sur HDFS** : Chargement des données prétraitées dans Hadoop.

## Implémentation de l'algorithme K-Means
1. **Choix de l'algorithme** : Utilisation de K-Means avec distance cosinus.
2. **Initialisation des centroïdes** : Utilisation de k-means++ pour une meilleure convergence.
3. **Exécution sur Hadoop** : Lancement du clustering avec un nombre de clusters fixé à 3.
4. **Analyse des résultats** : Extraction des centroïdes finaux et des attributions de clusters.

## Défis rencontrés et solutions apportées
- **Incompatibilités de versions entre Mahout et Hadoop** : Alignement des versions selon la documentation officielle.
- **Conversion de fichiers CSV en SequenceFile** : Validation stricte des fichiers avant conversion.
- **Gestion de la latence sur HDFS** : Optimisation de la taille des blocs et configuration de YARN.
- **Mesure de distance cosinus** : Utilisation de TF-IDF pour atténuer l'impact des termes non significatifs.

## Résultats obtenus
Le projet a permis de classifier efficacement les critiques de livres en groupes homogènes, ouvrant des perspectives pour des applications dans l'analyse de sentiments, la segmentation de marché et la personnalisation de services.

## Comment exécuter le projet
1. **Installation des dépendances** :
   ```bash
   sudo apt-get install hadoop mahout
   ```
2. **Prétraitement des données** :
   ```bash
   mahout seqdirectory -i input/ -o output-seqdir
   mahout seq2sparse -i output-seqdir -o output-vectors
   ```
3. **Exécution de K-Means** :
   ```bash
   mahout kmeans -i output-vectors -c clusters -o output-kmeans -k 3 -ow -cl
   ```

   ## Détails des commandes

Voici les commandes principales utilisées dans ce projet, accompagnées d'explications détaillées :

1. **Création du répertoire HDFS pour les données du projet** :
   ```bash
   hdfs dfs -mkdir -p /user/hadoop/mahout-kmeans
   ```
   Cette commande crée un répertoire sur HDFS pour stocker les fichiers nécessaires au projet.

2. **Chargement des données sur HDFS** :
   ```bash
   hdfs dfs -put /home/hadoop/mahout-kneans/bookreview_seq /user/hadoop/mahout-kmeans/
   ```
   Cette commande charge les données prétraitées depuis le système local vers le répertoire HDFS.

3. **Conversion des données en vecteurs TF-IDF** :
   ```bash
   mahout seq2sparse \
   -i hdfs:///user/hadoop/mahout-kmeans/bookreview_seq \
   -o hdfs:///user/hadoop/mahout-kmeans/bookreview_sparse \
   -ow --weight tfidf --maxDFPercent 85 --namedVector
   ```
   Cette commande transforme les fichiers de critiques textuelles en vecteurs TF-IDF utilisables par l'algorithme K-Means.

4. **Vérification des fichiers vectorisés** :
   ```bash
   hdfs dfs -ls /user/hadoop/mahout-kmeans/bookreview_sparse
   ```
   Elle permet de vérifier la présence et la structure des fichiers dans le répertoire spécifié.

5. **Exécution de l'algorithme K-Means** :
   ```bash
   mahout kmeans \
   -i hdfs:///user/hadoop/mahout-kmeans/bookreview_sparse/tf-vectors \
   -c hdfs:///user/hadoop/mahout-kmeans/clusters \
   -o hdfs:///user/hadoop/mahout-kmeans/output \
   -dm org.apache.mahout.common.distance.CosineDistanceMeasure \
   -x 10 -k 5 -ow --clustering
   ```
   Cette commande lance l'algorithme K-Means avec la mesure de distance cosinus, un nombre maximal d'itérations fixé à 10, et 5 clusters.

6. **Vérification des résultats du clustering** :
   ```bash
   hdfs dfs -ls /user/hadoop/mahout-kmeans/output
   ```
   Elle affiche les fichiers de sortie générés par K-Means, notamment les centroïdes et les clusters.

7. **Affichage des points assignés aux clusters** :
   ```bash
   hdfs dfs -ls /user/hadoop/mahout-kmeans/output/clusteredPoints
   ```
   Cette commande vérifie les fichiers contenant les points assignés à chaque cluster.


   ## Références
- [Apache Mahout Documentation](https://mahout.apache.org/documentation/users/clustering/k-means-clustering.html)
- [Exemple de projet similaire sur GitHub](https://github.com/mehulkatara/K-meansApacheMahout)
- [Tutoriel Hadoop et Mahout](https://hadooptutorial.weebly.com/k-means-clustering.html)
