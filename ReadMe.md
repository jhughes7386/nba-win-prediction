## Project Overview

This project builds an end-to-end NBA game outcome and season win prediction system using Python and team-level statistics. The goal is to simulate how real-world sports analytics and betting models forecast game outcomes using only information available prior to each game.

The model leverages:

Historical NBA team statistics

Rolling (recent performance) metrics

Season-to-date aggregates

Tree-based machine learning models (Random Forest)

Predictions are evaluated both at the game level and aggregated into team-level season win projections, providing interpretable insights into team strength and model limitations.

# Key Questions Addressed

Can historical and rolling team statistics predict NBA game outcomes?

Which team metrics are most predictive of winning?

How well do probabilistic game predictions translate into season win totals?

Where do statistical models struggle without player-level or injury data?

Data Sources

NBA Official Stats API (nba_api)

Regular season game logs

Team box score statistics

Modeling Approach

Supervised classification (Win / Loss)

Time-aware train/test split to prevent data leakage

Random Forest classifier using rolling and season-to-date features

Probabilistic predictions aggregated into projected season wins

## Project Structure & Execution Order
# Phase 1 — Data Collection

Notebook: 01_data_collection_2023_24.ipynb

Pulls NBA game-level team statistics using the NBA API

Cleans and formats raw data

Outputs structured CSV files

Repeat for evaluation season:
01_data_collection_2024_25.ipynb

# Phase 2 — Feature Engineering

Notebook: 02_feature_engineering.ipynb

Creates season-to-date averages (PTS, AST, REB, etc.)

Creates rolling metrics (last 5 games)

Generates home/away indicators

Prevents data leakage using lagged features

Outputs model-ready datasets

# Phase 3 — Baseline & Model Training

Notebook: 03_model_training.ipynb

Trains Logistic Regression and tree-based models

Selects Random Forest as the primary model

Evaluates accuracy and confusion matrix

Saves trained model and feature list

Artifacts saved:

rf_win_model.pkl

model_features.pkl

# Phase 4 — Apply Model to Current Season

Notebook: 04_current_season_application.ipynb

Loads trained Random Forest model

Applies model to the next season using only pre-game data

Generates win probabilities for each game

Aggregates probabilities into projected team wins

Compares projected wins to actual standings

Performs feature importance and error analysis

# Results Summary
Model Performance

Random Forest accuracy: ~66%

Captures league-wide team strength hierarchy

Mid-tier teams predicted with reasonable accuracy

Feature Importance
Feature Group	Importance
Season-to-Date	~62%
Rolling (Last 5 Games)	~38%

Season-to-date metrics dominate, while recent performance provides meaningful but secondary signal.

# Error Analysis

Under-predicted breakout teams (e.g., OKC, CLE)

Over-predicted injury-affected or unstable teams (e.g., CHA, NOP)

Errors largely attributable to factors not included in team stats:

Injuries

Trades

Player development

# Key Takeaways

Team-level historical statistics provide strong baseline signal for forecasting.

Rolling metrics improve responsiveness to recent trends.

Purely statistical models struggle to capture non-linear changes driven by player availability and development.

This type of modeling mirrors foundational approaches used in sports analytics and betting markets, where probabilistic forecasts inform decision-making and risk management.

# Tools & Libraries

Python

pandas, numpy

scikit-learn

nba_api

matplotlib, seaborn

Google Colab

# Future Improvements

Incorporate player-level statistics

Model injuries and availability explicitly

Add opponent-adjusted metrics

Explore neural networks or Elo-based hybrid models

Weekly rolling retraining simulation
