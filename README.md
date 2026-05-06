# Databricks End-to-End Project

Ce projet montre un pipeline de traitement de donnees sur Databricks, organise en notebooks Jupyter, du parametrage initial jusqu'aux tables Gold.

## Objectif

Construire un flux de donnees type medaillon (Bronze -> Silver) a partir de fichiers Parquet, avec verification de la qualite des donnees entre les etapes.

## Structure du projet

- `00_parameters.ipynb` : construit les parametres de job (storage account, containers, datasets) via widgets et expose une liste de datasets a traiter.
- `01_bronze_ingestion.ipynb` : ingestion Auto Loader (`cloudFiles`) des fichiers Parquet source vers Delta en Bronze, avec schema et checkpoint par dataset.
- `02_verify_bronze.ipynb` : verification de la qualite Bronze par comparaison des volumes source vs Bronze.
- `silver_customer.ipynb` : nettoyage/standardisation de `customers` depuis Bronze, ecriture Delta en Silver, puis creation de `databrick_cata.silver.customers_silver`.
- `silver_orders.ipynb` : transformations de `orders` (dont logique de fenetrage), ecriture Delta en Silver, puis creation de `databrick_cata.silver.orders_silver`.
- `silver region.ipynb` : transformation de la table `regions` depuis Bronze vers Silver.
- `gold_product.ipynb` : pipeline Lakeflow/DLT pour construire la dimension produit (`DimProducts`) en mode SCD Type 1 a partir de `databrick_cata.silver.products_silver`.
- `gold_orders.ipynb` : construction de la table de faits `databrick_cata.gold.FactOrders` a partir de `orders_silver` et jointures avec dimensions Gold.

## Jeux de donnees inclus

Le projet contient des fichiers Parquet de demonstration, par exemple :

- `customer_first.parquet`, `customers_second.parquet`
- `orders_first.parquet`, `orders_second.parquet`
- `products_first.parquet`, `products_second.parquet`
- `regions.parquet`

## Pre-requis

- Un workspace Databricks
- Un cluster Databricks actif (runtime Spark compatible)
- Permissions de lecture/ecriture sur le stockage cible (DBFS, Unity Catalog ou autre emplacement configure)

## Ordre d'execution recommande

1. Executer `00_parameters.ipynb`
2. Executer `01_bronze_ingestion.ipynb` (pour chaque dataset)
3. Executer `02_verify_bronze.ipynb`
4. Executer les notebooks Silver :
   - `silver_customer.ipynb`
   - `silver_orders.ipynb`
   - `silver region.ipynb`
5. Executer les notebooks Gold :
   - `gold_product.ipynb`
   - `gold_orders.ipynb`

## Notes

- Le fichier `Databricks ETE Project.dbc` peut etre importe directement dans Databricks pour recuperer les notebooks.
- Adaptez les chemins de stockage et noms de tables selon votre environnement.
- Certains notebooks contiennent des sorties d'execution volumineuses; il est recommande de nettoyer les outputs avant versioning si besoin.

