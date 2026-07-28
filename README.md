# TICKIT Database Analysis

Ce projet explore la base de données **TICKIT**, un jeu de données standard d'AWS simulant un site de vente de billets en ligne (concerts, sport, spectacles). L'objectif est de pratiquer l'import et l'analyse de données relationnelles réparties sur plusieurs tables liées entre elles.

## Données
7 tables (2 faits, 5 dimensions) : `buyer`, `seller`, `venue`, `category`, `event`, `listing`, `sale`.

## Compétences utilisées
- Import de fichiers délimités par pipe (`|`)
- Nettoyage et typage de données (booléens, dates)
- Jointures entre plusieurs tables
- Agrégations et analyse de ventes

Source des données : [garystafford/tickit-srv-data](https://github.com/garystafford/tickit-srv-data), basé sur l'exemple officiel [AWS Redshift TICKIT](https://docs.aws.amazon.com/redshift/latest/dg/c_sampledb.html).
