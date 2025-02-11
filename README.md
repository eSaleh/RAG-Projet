## 1. Introduction

### 1.1. Description du projet

Dans ce projet, nous travaillons sur un système de **génération augmentée de récupération** (**RAG** - Retrieval Augmented Generation) qui combine des modèles de langue génératifs et des techniques de recherche d'information. Les données se trouvent dans cette compétition kaggle : [text](https://www.kaggle.com/competitions/inf-8460-aut-2024-tp-4).

Lorsqu'une question est posée, nous devons retrouver les passages les plus pertinents à l'aide d'un modèle de recherche. Ensuite, nous utilisons ces passages pour générer une réponse à la question. Enfin, nous explorons différentes approches pour améliorer les performances de notre modèle RAG.

### 1.2. Améliorations et Résultats

Nous avons apporté deux améliorations principales à notre modèle :

1. **Affinage du modèle de récupération** : Plutôt que de simplement entraîner le modèle pour maximiser le score-F1, nous avons adopté une approche d'entraînement contrastif. Pour chaque question, nous avons généré des exemples négatifs en utilisant l'algorithme BM-25, en sélectionnant des documents proches de la question mais non pertinents. Cette méthode a surpassé l'approche utilisant des exemples négatifs choisis aléatoirement.

2. **Ajout d'un processus de reclassement** : Inspirés par Kim et Lee (2024), nous avons intégré l'encodeur croisé **'bge-reranker-large'** de HuggingFace. Cet encodeur a été combiné avec notre modèle affiné pour une seconde évaluation des documents récupérés. Nous avons aussi testé sa combinaison avec le modèle initial et un modèle plus grand de la même famille.

### 1.3. Limites et Observations

Notre principale limite est que nous avons peu modifié la partie génération de notre modèle. Le générateur produit parfois des réponses correctes sur le fond mais mal formulées. Malgré un score-F1 stagnant autour de 62% pour la récupération des documents, notre modèle semble bien identifier les informations pertinentes. Cependant, l'évaluation automatique ne prend pas en compte la sémantique des réponses, ce qui reste un obstacle majeur.

Nous avons tenté d'améliorer la formulation des réponses via du prompting en langage naturel, mais cette méthode reste limitée. Une amélioration plus poussée du générateur pourrait être nécessaire pour mieux adapter les réponses au format attendu.

