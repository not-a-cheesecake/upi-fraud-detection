# GNN-Based UPI Fraud Detection

## Project Overview

This project compares traditional machine learning models and Graph Neural Network (GNN) models for detecting fraudulent financial transactions.

The experiments use the PaySim synthetic financial transaction dataset. The project investigates model performance under random and temporal evaluation settings, with a focus on fraud detection, temporal generalization, and explainability.

**Dataset limitation:** PaySim contains synthetic financial transactions and is not a dataset of actual UPI transactions. Findings will be interpreted within the limitations of this dataset.

## Objectives

- Compare traditional machine learning models with GNN-based models.
- Evaluate fraud detection using Precision, Recall, F1-score, PR-AUC (Average Precision), and ROC-AUC.
- Investigate model explainability to understand predictions.
- Evaluate temporal generalization by training on earlier transactions and testing on later transactions.
- Analyze performance differences between random and temporal evaluation settings.

## Models

### Traditional Machine Learning
- Logistic Regression
- Random Forest
- XGBoost

### Graph Neural Networks
- Graph Convolutional Network (GCN)
- GraphSAGE
- Graph Attention Network (GAT)

## Dataset

- **Dataset:** PaySim synthetic financial transaction dataset.
- **Target label:** `isFraud`
- **Dataset file:** `PS_20174392719_1491204439457_log.csv`

The dataset is not included in the Git repository. Each team member must obtain the same dataset version and place the CSV in the local `data/` directory.

Expected local path:

`data/PS_20174392719_1491204439457_log.csv`

## Evaluation Protocol

- **Random split:** 80% training and 20% testing, using `random_state=42` and stratification on `isFraud`.
- **Temporal split:** Training data uses `step < 355`; testing data uses `step >= 355`.
- Preprocessing is fitted on the corresponding training data only.
- Graph-based temporal experiments must prevent future transaction information from leaking into training.

## Project Structure

- `data/` — Local dataset files; excluded from Git.
- `notebooks/` — Data exploration, model experiments, and results analysis.
- `src/` — Reusable preprocessing, graph construction, and model code.
- `results/` — Experiment metrics and model comparison results.
- `docs/` — Project documentation and research notes.

## Current Status

### Completed
- Repository and Python environment setup.
- Initial dataset exploration and class-imbalance analysis.
- Random and temporal train-test split definitions.
- Initial Logistic Regression, Random Forest, and XGBoost experiments.
- Saved baseline metrics for both evaluation settings.
- Initial model-performance and PR-AUC comparison visualizations.

### In Progress / Planned
- Graph construction and GNN implementation.
- GCN, GraphSAGE, and GAT experiments.
- Explainability analysis.
- Temporal generalization analysis across traditional ML and GNN models.
- Consolidated model comparison and research paper preparation.

## Team Workflow

- Pull the latest changes before starting work.
- Work primarily in assigned notebooks or source files.
- Use descriptive commit messages and push completed changes to the shared repository.
- Keep the dataset local; do not commit the raw dataset.
- Use consistent evaluation splits and metric definitions across model experiments.
