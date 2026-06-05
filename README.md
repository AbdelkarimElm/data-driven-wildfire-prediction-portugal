# Wildfire Susceptibility – Portugal

Cartographie de la susceptibilité aux feux de forêt au Portugal continental à partir de données géospatiales (grille de 1 km × 1 km).
Projet Big Data de groupe, Master Informatique – Université Paris Cité (2025/2026).

## Pipeline
1. **Grille et occupation du sol** : grille de 1 km sur le Portugal continental, land cover (ESA GlobCover) et population (GHSL) via Google Earth Engine
2. **Feux** : détections MODIS/VIIRS (NASA FIRMS), filtrage par confiance et type, historique des feux
3. **Variables environnementales** : climat (WorldClim, agrégé par saison), altitude (GMTED), sol (HWSD v2), pente, exposition, TWI, NDVI, LST, vent et humidité (ERA5)
4. **Fusion et nettoyage** : jointure sur la grille, suppression des doublons et des variables corrélées, imputation par plus proches voisins
5. **Réimplémentation de deux articles** : méthode « Inde » (Uthappa) et méthode « Algérie » (Bouzeraa) – RF, SVM, XGBoost, K-Means, VIF, SHAP
6. **Modèle final** : ajout de variables (distances, densité de population, type de forêt, feux historiques, voisinage spatial), gradient boosting optimisé avec Optuna, interprétation SHAP et carte de susceptibilité

## Structure
| Dossier | Contenu |
|---|---|
| `Grid et landcover/` | Grille, authentification GEE, land cover, population |
| `Fire/`, `Historique_Fire/` | Nettoyage et visualisation des feux |
| `Processing/` | Climat, altitude, sol |
| `merge/` | Fusion des sources et traitement des valeurs manquantes |
| `Reimplementation_Methods_Papers/` | Prétraitement et modèles des deux articles |
| `model training and processing/` | Analyse exploratoire, ajout de variables, modèle final |

Les sources de données sont listées dans `DataSource.txt`. Les données brutes et les modèles entraînés ne sont pas versionnés (taille).

## Stack
Python, pandas, GeoPandas, rasterio, xarray, Google Earth Engine, scikit-learn, XGBoost, LightGBM, Optuna, SHAP, matplotlib
