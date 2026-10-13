
# GNN-Based UPI Fraud Detection

## Project Overview
This project aims to explore Graph Neural Networks (GNNs) for detecting fraudulent financial transactions.

The project will compare traditional machine learning models with graph-based models and investigate explainability and temporal generalization.

## Objectives
- Compare traditional machine learning models with GNN-based models.
- Evaluate performance using fraud-relevant metrics such as Precision, Recall, F1-score, and PR-AUC.
- Explore model explainability to understand fraud predictions.
- Evaluate temporal generalization by testing on later transactions than those used for training.

## Planned Models
- Logistic Regression
- Random Forest
- XGBoost
- Graph Convolutional Network (GCN)
- GraphSAGE
- Graph Attention Network (GAT)

## Project Structure
- `data/` — Datasets and processed data
- `notebooks/` — Exploratory analysis and experiments
- `src/` — Source code
- `results/` — Evaluation results and visualizations
- `docs/` — Documentation and research notes

## Project Status
Initial repository setup is complete. Data preparation, model implementation, evaluation, and explainability are planned next.

## Note on Data
The dataset source and its suitability for representing UPI transactions will be documented before experiments. Results will be interpreted according to the dataset's limitations.
