# Spotify Song Popularity Prediction — Erel Katzman

## Project Overview
This project applies Machine Learning to predict the popularity of songs on Spotify using their musical and contextual features. The dataset (≈29,000 songs) includes audio metrics such as danceability, energy, valence, loudness, and tempo, as well as metadata like genre, subgenre, release year, and artist. The objective is to build a data-driven model that identifies which song attributes most influence popularity.

## Guiding Questions
* ### What are we trying to find out?
  To identify the main factors that influence Spotify track popularity and build a regression model capable of predicting it.
* ### What do we already know?
  Previous research and Spotify’s API reveal that song attributes such as energy, tempo, and danceability often correlate with higher popularity.
* ### What are we aiming to achieve?
  A predictive model that generalizes well, offering clear interpretability and measurable performance (R², RMSE, MAE).
* ### What factors affect our results?
  Genre, subgenre, and production characteristics (energy, loudness, danceability) have strong influence, while year of release and duration play secondary roles.
* ### Is there something new we can use?
  We combine feature engineering (domain-driven transformations) with boosted models (LightGBM, XGBoost, CatBoost) and leakage-safe target encoding for high-cardinality features like artist.

## Workflow Summary (Stages 1–7)
## 1. Data Preparation
* Merged and cleaned raw data into a unified dataset.
* Parsed release date into separate `release_year` and `release_month`.
* Unified text casing and handled missing values (median for numeric, “Unknown” for text).

## 2. Exploratory Data Analysis (EDA)
* Visualized feature distributions and correlations.
* Identified relationships between popularity, danceability, energy, and loudness.
* Observed genre-level variation and moderate correlation between key audio features.

## 3. Data Cleansing
* Detected and reviewed outliers via IQR analysis.
* Verified no missing or inconsistent data post-cleaning.
* Confirmed data types and value ranges were consistent.

## 4. One-Hot Encoding
* Applied One-Hot Encoding (OHE) for categorical variables with low to medium cardinality (genre, subgenre, release year/month).
* Maintained artist column for later Target Encoding to prevent data leakage.

## 5. Feature Engineering & Feature Selection
* Created domain-specific features: `dance_energy`, `energy_diff`, `valence_energy`, `acoustic_instru`, `speech_loud_ratio`, `log_duration`, `release_age`.
* Standardized numeric features for uniform scale.
* Selected key predictors using L1 regularization (Lasso) and model-based feature importance (Ridge, Random Forest).

## 6. Model Selection & Fine-Tuning
* Compared linear (Ridge, Lasso) and ensemble models (Random Forest, Gradient Boosting, XGBoost, LightGBM, CatBoost).
* Applied cross-validation (5-fold) for robust model comparison.
* Fine-tuned best model (LightGBM) using RandomizedSearchCV for hyperparameter optimization.
* Trained model pipeline saved locally for later evaluation and deployment.

## 7. Model Evaluation
* Split dataset into Train/Validation/Test sets (80/10/10).
* Evaluated model performance with RMSE, MAE, and R² metrics.
* Visual diagnostics: predicted vs actual plots, residual distributions, and error by genre.
* Best model achieved *R² ≈ 0.33, RMSE ≈ 24*, showing moderate predictive strength and strong interpretability.

## Project Summary: Deployment and Beneficiaries of Machine Learning
* ### Deployment:
  The final trained model can be easily re-trained or integrated into an API environment to predict song popularity from new track metadata or audio features.
* ### Beneficiaries:
  * Artists and producers can analyze what makes tracks successful.
  * Playlist curators can identify potential hits or optimize playlists by predicted engagement.
  * Streaming platforms gain insights into user preference trends.

*Data Science – ML Module by Orit Ophir*

Author: Erel Katzman

Date: November 2025
