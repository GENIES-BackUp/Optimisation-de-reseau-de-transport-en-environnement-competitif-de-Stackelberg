
***

# Optimisation de Réseaux de Hubs en Environnement Concurrentiel

Ce projet implémente une **métaheuristique génétique** pour résoudre un problème complexe de localisation d'arcs de hubs dans un cadre de compétition de **Stackelberg**. Le modèle se distingue par l'intégration d'une règle d'allocation **bi-critère (coût-temps)**, offrant une représentation plus fidèle du comportement des clients que les modèles monocritères classiques,,.

## 📌 Présentation du Problème

Le système modélise la compétition entre deux firmes :
*   **La Firme A (Leader) :** Prend sa décision en premier en anticipant la réaction optimale de son concurrent,.
*   **La Firme B (Suiveur) :** Observe le réseau du leader et déploie ses propres infrastructures pour maximiser ses revenus.

### Innovations majeures
*   **Allocation Bi-critère :** La demande est répartie selon un arbitrage entre le coût de transport et le temps de parcours (estimé par la distance),.
*   **Non-exclusivité des Hubs :** Les firmes ont la possibilité de partager les mêmes nœuds de hubs, intensifiant la concurrence sur les points stratégiques,.
*   **Modèle d'Arcs de Hubs :** Contrairement au modèle de hub médian complet, ce modèle localise des arcs spécifiques bénéficiant d'une réduction de coût ($\alpha$), favorisant les économies d'échelle,,.

## 🧬 L'Algorithme Génétique

Le problème étant **NP-difficile**, une approche heuristique est nécessaire pour traiter des instances de taille réelle,. L'algorithme génétique explore l'espace des solutions par des mécanismes inspirés de l'évolution naturelle,.

### Étapes clés de l'algorithme :
1.  **Initialisation :** Génération d'une population de taille $N$ représentant diverses configurations de réseaux pour le leader.
2.  **Évaluation (Fitness) :** Utilisation de l'heuristique **MRP (Meilleure Réponse Pratique)** pour calculer le revenu du leader face à la réponse optimale du suiveur,.
3.  **Sélection :** Choix des parents par tournoi .
4.  **Reproduction :** Application d'opérateurs de **croisement** et de **mutation** pour générer une nouvelle génération de solutions,.
5.  **Critère d'arrêt :** L'algorithme s'arrête après un nombre prédéfini de générations ou en cas de convergence,.

### Calcul de la Fitness (Méthode MRP)
L'évaluation d'un individu (réseau $A$) suit un processus rigoureux :
*   Identifier les hubs potentiels pour $B$ (nœuds non occupés ou partagés selon la variante).
*   Calculer les ratios de performance ($DRA$ pour la distance, $CRA$ pour le coût) pour chaque paire origine-destination,.
*   Déterminer la part de marché capturée via une **fonction en escalier à cinq niveaux**,,.

## 📊 Données et Simulations

Le modèle a été validé sur des jeux de données synthétiques représentant **16 configurations de pays**. Ces instances couvrent diverses typologies :
*   **Géographie :** Structures côtières (noyau central dense) ou régionales (sous-ensembles isolés).
*   **Demande :** Répartition équilibrée ou métropolitaine (concentration sur quelques pôles).
*   **Profils clients :** Clientèle "pressée" (sensible au temps) ou "non pressée" (sensibilité homogène).

## 💻 Implémentation

Le projet est implémenté sous forme de **Notebook Jupyter** en Python.
*   **Paramètres ajustables :** Nombre d'arcs ($q_A, q_B$), facteur de réduction ($\alpha$), et seuils de sélectivité ($r_1, r_2$),,.
*   **Visualisation :** Les résultats incluent des graphes montrant les stratégies de "verrouillage du marché" par le leader et "d'extension périphérique" par le suiveur,,.

***

**Note :** Cette implémentation s'appuie sur les travaux de Sasaki et al. (2014) et les extensions bi-critères développées par Asso Luc, Diarrassouba Yaya, Kpahiro Zagba et Bamba Gbango.
