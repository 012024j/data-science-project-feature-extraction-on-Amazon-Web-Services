#  Fruits! - Traitement Big Data sur le Cloud

## Contexte du projet

Ce projet s'inscrit dans le cadre d'une mission en tant que **Data Scientist** au sein de la start-up **Fruits!**, une entreprise de l'AgriTech qui développe des solutions innovantes pour la reconnaissance et la classification de fruits à partir d’images.

Dans le but de sensibiliser le grand public à la biodiversité fruitière et de poser les bases de futurs robots cueilleurs intelligents, **Fruits!** développe une application mobile permettant à l'utilisateur de prendre une photo d’un fruit et d’obtenir instantanément des informations sur celui-ci.

---

## Objectifs

- Réaliser un **traitement Big Data** sur un **jeu de données volumineux d’images de fruits**.
- Migrer le pipeline local vers une **infrastructure Cloud distribuée** (AWS).
- Exploiter **PySpark** et des outils comme **EMR, S3, EC2, IAM, EMR Studio** pour un traitement efficace.
- Appliquer une **réduction de dimension** par **ACP** (PCA).
- Préparer les données pour un futur pipeline de classification d’images.

---

## Données

- **Dataset utilisé** : [Fruits-360](https://www.kaggle.com/datasets/moltean/fruits)
- **Nombre d’images** : 138 704
- **Nombre de classes de fruits** : 206

---

## Architecture Big Data (AWS)

| Composant | Description |
|----------|-------------|
| **S3** | Stockage distribué pour les images d'entrée et les résultats (format parquet) |
| **EMR** | Traitement des données avec PySpark sur cluster distribué |
| **EC2** | Instances m5.xlarge pour exécuter les workers Spark |
| **EMR Studio** | Interface JupyterLab connectée au cluster pour développement interactif |
| **IAM** | Gestion des rôles et sécurité RGPD (région `eu-west-3`) |

---

## Pipeline de traitement PySpark

1. **Chargement des images** depuis S3 + redimensionnement (224x224x3)
2. **Extraction de caractéristiques visuelles** avec le modèle pré-entraîné **MobileNetV2** (embeddings 1280-dim)
3. **Diffusion des poids du modèle** à tous les workers Spark (broadcast)
4. **Stockage des embeddings** en **format Parquet** sur S3
5. **Réduction de dimension** avec une **ACP** (20 composantes) pour simplification et prévision
6. **Sauvegarde des résultats** réduits sur S3

---

## Technologies utilisées

- **PySpark**
- **AWS (S3, EMR, EMR Studio, EC2, IAM)**
- **Parquet**
- **TensorFlow / MobileNetV2**
- **PCA (ACP)** pour réduction de dimension

---

## Résultats

- Traitement distribué exécuté avec succès sur EMR
- Embeddings visuels extraits et compressés
- Réduction à 6 composantes expliquant 98% de la variance
- Pipeline évolutif, prêt à être connecté à un modèle de classification

---

##  Perspectives

- Tester d'autres modèles d'extraction (ResNet, EfficientNet)
- Entraîner un modèle de classification (MLP, SVM, etc.)
- Développer une interface mobile (Streamlit, API)
- Intégrer une surveillance automatisée (logs, métriques, drift)

---

## 🛡️ RGPD

Toutes les ressources AWS ont été déployées en **région européenne** (eu-west-3) pour garantir la conformité RGPD. Aucun traitement de données personnelles.

---


---

## Auteure

 **Oumou Faye**  
Projet réalisé dans le cadre de la formation **Data Scientist**  
Mentor : Medina Hadjem  




