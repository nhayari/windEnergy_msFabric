# windEnergy_msFabric

## Présentation du pipeline de données

Ce projet implémente un pipeline de données classique en architecture **Medallion** (Bronze → Silver → Gold).

Les trois notebooks suivants traitent les données de manière séquentielle et progressive :

- **`01_Ingestion_Journaliere_Bronze.ipynb`**  
  Ingestion quotidienne des données brutes.  
  → Récupération des sources externes (fichiers CSV)  
  → Chargement sans ou avec très peu de transformation  
  → Stockage dans la couche **Bronze** (zone raw / landing)  
  Objectif : conserver une copie fidèle et horodatée des données telles qu'elles arrivent.

- **`02_Transformation_to_Silver.ipynb`**  
  Nettoyage et préparation des données.  
  → Déduplication, correction des formats, gestion des valeurs manquantes  
  → Typage correct des colonnes (dates, nombres, booléens…)  
  → Application des règles de qualité / business rules de premier niveau  
  → Enrichissement léger si nécessaire  
  → Sauvegarde dans la couche **Silver** (zone cleaned / trusted)  
  Objectif : produire des données propres, cohérentes et exploitables.

- **`03_Agregation_to_Gold.ipynb`**  
  Agrégation, normalisation, modélisation et préparation pour la consommation finale.  
  → Calculs d'indicateurs, jointures, pivot, agrégations (par jour, semaine, mois…)  
  → Création de tables / vues métier optimisées (forme star/snowflake si applicable)  
  → Application des dernières règles business complexes  
  → Sauvegarde dans la couche **Gold** (zone presentation / curated)  
  Objectif : fournir des données prêtes à être consommées par les rapports, dashboards et data products.

## Notebooks du pipeline Medallion


| Notebook                           | Couche    | Objectif principal                            |
|------------------------------------|-----------|-----------------------------------------------|
| 01_Ingestion_Journaliere_Bronze    | Bronze    | Ingestion brute quotidienne – données raw     |
| 02_Transformation_to_Silver        | Silver    | Nettoyage, normalisation, qualité des données |
| 03_Agregation_to_Gold              | Gold      | Agrégations et tables finales métier          |
