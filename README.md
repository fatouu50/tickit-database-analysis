# TICKIT Database Analysis

Analyse d'un jeu de données relationnel inspiré de **TICKIT**, l'exemple standard fourni par AWS pour illustrer Amazon Redshift. TICKIT simule un site fictif de vente de billets en ligne (concerts, spectacles, événements sportifs), où des utilisateurs achètent et vendent des billets entre eux.

Ce projet a pour but de pratiquer, sur un jeu de données relationnel multi-tables, l'import et le nettoyage de données, l'analyse exploratoire avec pandas, et les requêtes SQL avancées (jointures, fonctions de fenêtrage).

## Objectifs

- Importer et nettoyer des données réparties sur plusieurs tables liées entre elles
- Fusionner ces tables pour construire une vue d'ensemble exploitable
- Réaliser une analyse exploratoire (univariée et bivariée) avec pandas
- Pratiquer des requêtes SQL complexes (jointures multiples, fonctions de fenêtrage, sous-requêtes)
- Répondre à des questions métier concrètes : ventes par catégorie, top vendeurs, tendances temporelles...

## Source des données

Les données proviennent du dépôt [garystafford/tickit-srv-data](https://github.com/garystafford/tickit-srv-data), une adaptation du schéma officiel [TICKIT documenté par AWS](https://docs.aws.amazon.com/redshift/latest/dg/c_sampledb.html).

**Format** : fichiers `.txt` délimités par le caractère pipe (`|`).

## Schéma de la base de données

7 tables au total (2 tables de faits, 5 tables de dimensions) :

| Table | Type | Description |
|---|---|---|
| `sale` | Fait | Détails des transactions (quantité, prix, commission) |
| `listing` | Fait | Billets mis en vente par les vendeurs |
| `users` | Dimension | Profils des acheteurs et vendeurs |
| `event` | Dimension | Détails des événements (concerts, matchs...) |
| `venue` | Dimension | Lieux physiques des événements |
| `category` | Dimension | Catégories d'événements (opéra, MLB, comédies musicales...) |
| `date` *(dérivée)* | Dimension | Recréée à partir des colonnes datetime, absente des fichiers sources |

### Relations entre les tables

```
sale.buyerid     → users.userid
sale.sellerid    → users.userid
sale.listid      → listing.listid
listing.sellerid → users.userid
listing.eventid  → event.eventid
event.venueid    → venue.venueid
event.catid      → category.catid
```

## Structure du dépôt

```
tickit-database-analysis/
├── data/
│   ├── tickit_public_user.txt
│   ├── tickit_public_venue.txt
│   ├── tickit_public_category.txt
│   ├── tickit_public_event.txt
│   ├── tickit_public_listing.txt
│   └── tickit_public_sale.txt
├── notebooks/
│   ├── 01_import_nettoyage.ipynb
│   ├── 02_pandas_analyse.ipynb
│   └── 03_sql_requetes.ipynb
└── README.md
```

## Notebooks

| Notebook | Contenu |
|---|---|
| `01_import_nettoyage.ipynb` | Import des 6 tables, inspection, nettoyage, typage des dates et booléens |
| `02_pandas_analyse.ipynb` | Fusion des tables, analyse univariée et bivariée, premiers insights |
| `03_sql_requetes.ipynb` | Chargement en base SQLite, jointures multiples, fonctions de fenêtrage, sous-requêtes |

## Compétences pratiquées

- Importation de données multi-format (fichiers délimités par pipe)
- Nettoyage et typage de données (booléens, dates)
- Jointures de DataFrames avec pandas (`pd.merge`)
- Agrégation et statistiques descriptives (`groupby`, `agg`)
- SQL : `JOIN`, `GROUP BY`, fonctions de fenêtrage (`RANK() OVER`, `SUM() OVER PARTITION BY`), CTE

## À venir

- Pipelines ETL/ELT (Airflow, dbt) — prévu dans une phase ultérieure
- Optimisation des performances de bases de données (clés de distribution, de tri) — nécessite un environnement Redshift réel

## Auteure

Projet réalisé en autodidacte, dans le cadre d'un apprentissage continu en data science.
