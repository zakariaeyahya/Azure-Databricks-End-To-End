# Databricks End-to-End Project

Ce projet montre un pipeline de traitement de donnees sur Databricks, organise en plusieurs notebooks, du parametrage initial jusqu'aux tables Silver.

## Objectif

Construire un flux de donnees type medaillon (Bronze -> Silver) a partir de fichiers Parquet, avec verification de la qualite des donnees entre les etapes.

## Structure du projet

- `00_parameters.ipynb` : definition des parametres globaux (chemins, catalog/schema, options runtime).
- `01_bronze_ingestion.ipynb` : ingestion des donnees sources dans la couche Bronze.
- `02_verify_bronze.ipynb` : controles de qualite et verification des donnees Bronze.
- `silver_customer.ipynb` : transformation de la donnee client vers Silver.
- `silver_orders.ipynb` : transformation de la donnee commandes vers Silver.
- `silver region.ipynb` : transformation de la donnee region vers Silver.

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
2. Executer `01_bronze_ingestion.ipynb`
3. Executer `02_verify_bronze.ipynb`
4. Executer les notebooks Silver :
   - `silver_customer.ipynb`
   - `silver_orders.ipynb`
   - `silver region.ipynb`

## Notes

- Le fichier `Databricks ETE Project.dbc` peut etre importe directement dans Databricks pour recuperer les notebooks.
- Adaptez les chemins de stockage et noms de tables selon votre environnement.

