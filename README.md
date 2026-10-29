# GNN-Based UPI Fraud Detection

## Project Overview

This project studies financial transaction fraud detection using the PaySim synthetic transaction dataset. It combines traditional machine-learning models with graph neural networks (GNNs) to investigate fraud detection performance, temporal evaluation, and model explainability.

**Dataset note:** PaySim is synthetic financial transaction data, not real UPI transaction data. These results do not establish performance on live UPI systems.

## Models Implemented

### Traditional Machine Learning
- Logistic Regression
- Random Forest
- XGBoost

### Graph Neural Networks
- Graph Convolutional Network (GCN)
- GraphSAGE
- Graph Attention Network (GAT)

The experiments have different evaluation artifacts and should not automatically be treated as directly comparable.

## Dataset

- **Dataset:** PaySim synthetic financial transaction dataset
- **Target variable:** `isFraud`
- **Expected local path:** `data/PS_20174392719_1491204439457_log.csv`

The raw dataset is not included in this repository and must be obtained separately.

## Repository Structure

- `notebooks/01_data_exploration.ipynb` — dataset exploration
- `notebooks/02_traditional_ml_results_analysis.ipynb` — traditional ML analysis
- `notebooks/03_graph_construction.ipynb` — graph construction
- `notebooks/04.GAT.ipynb` — GAT implementation and evaluation
- `results/Traditional_ML/` — traditional ML result files
- `results/GCN_GraphSAGE/` — GCN and GraphSAGE performance figures
- `results/gat_explainability/` — GAT evaluation and explainability artifacts
- `docs/methodology.md` — project methodology
- `docs/results_analysis.md` — results and interpretation
- `docs/limitations_and_future_work.md` — limitations and future work

The tracked implementation is primarily notebook-based.

## Selected Results

### Traditional ML — Temporal Evaluation

| Model | Precision | Recall | F1-score | PR-AUC | ROC-AUC |
|---|---:|---:|---:|---:|---:|
| Logistic Regression | 0.1102 | 0.8828 | 0.1959 | 0.6801 | 0.9880 |
| Random Forest | 0.2796 | 0.9547 | 0.4325 | 0.8995 | 0.9991 |
| XGBoost | 0.9997 | 0.7158 | 0.8343 | 0.9570 | 0.9998 |

### GAT — Final Temporal Test

The saved GAT test run used a decision threshold of 0.75.

| Metric | Value |
|---|---:|
| Test transactions | 1,293,523 |
| Actual fraud cases | 4,258 |
| Precision | 0.9167 |
| Recall | 0.6177 |
| F1-score | 0.7380 |
| PR-AUC | 0.6853 |
| ROC-AUC | 0.8126 |

The GAT model's confusion matrix and additional evaluation details are documented in `docs/results_analysis.md`.

GCN and GraphSAGE results are represented by saved performance figures. Their exact metrics should be taken from the original experiment outputs rather than estimated from filenames.

## Explainability

The project includes GNNExplainer outputs for a selected GAT validation fraud example, including feature-importance scores, edge-importance results, and an edge-removal diagnostic.

These explanations describe a specific example and should not be interpreted as causal evidence or as explanations that necessarily apply to every prediction.

## Evaluation Notes

- Fraud detection involves severe class imbalance, so precision, recall, F1-score, PR-AUC, and confusion-matrix counts are important.
- Random and temporal evaluation measure different forms of generalization.
- Direct model comparisons require compatible data splits, features, preprocessing, thresholds, and metric definitions.
- The experiments use synthetic PaySim data and do not demonstrate readiness for real-world financial deployment.

## Future Improvements

- Export consolidated GCN and GraphSAGE metrics to CSV.
- Standardize evaluation settings for fair model comparisons.
- Test explanation stability across multiple examples.
- Document package versions, random seeds, and experiment configurations.
- Evaluate on suitable real-world data if it becomes lawfully available.
