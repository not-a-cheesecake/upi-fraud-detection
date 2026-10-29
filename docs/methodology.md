# Methodology

## 1. Problem Definition and Dataset

This project investigates binary classification of potentially fraudulent financial transactions using the `isFraud` label in the PaySim synthetic financial transaction dataset.

The objective is to compare traditional machine-learning approaches with graph neural network approaches for fraud detection.

PaySim is synthetic data. Therefore, the experiments do not directly establish performance on real UPI transactions.

Fraud is a minority class, so the evaluation uses metrics such as precision, recall, F1-score, Precision-Recall AUC (PR-AUC), and ROC-AUC rather than relying on accuracy alone.

## 2. Traditional Machine-Learning Models

Three traditional machine-learning models are included:

- Logistic Regression
- Random Forest
- XGBoost

The repository records experiments using random and temporal evaluation settings. The consolidated results are stored in:

`results/Traditional_ML/model_comparison_results.csv`

### Recorded temporal results

| Model | Precision | Recall | F1-score | PR-AUC | ROC-AUC |
|---|---:|---:|---:|---:|---:|
| Logistic Regression | 0.1102 | 0.8828 | 0.1959 | 0.6801 | 0.9880 |
| Random Forest | 0.2796 | 0.9547 | 0.4325 | 0.8995 | 0.9991 |
| XGBoost | 0.9997 | 0.7158 | 0.8343 | 0.9570 | 0.9998 |

These values are taken from the saved traditional ML comparison results. Comparisons with GNN models should account for differences in preprocessing, features, evaluation splits, and threshold selection.

## 3. Graph Construction

The graph-based experiments represent financial activity through account nodes and transaction relationships.

For the GAT experiment, account nodes use four historical features:

- `sent_count`
- `received_count`
- `sent_amount`
- `received_amount`

Historical transactions provide graph edges, while transaction-level features and source/destination account representations are used for transaction classification.

The graph context and temporal boundaries are described in the GAT notebook.

## 4. Graph Neural Network Experiments

### 4.1 Graph Convolutional Network (GCN)

The project includes GCN prototype experiments and saved performance visualizations:

- `results/GCN_GraphSAGE/GCN_Performance_Matrices.jpeg`
- `results/GCN_GraphSAGE/gcn_prototype_performance.png`

These artifacts document the available GCN performance analysis. A consolidated GCN metrics CSV is not currently available in this results directory, so exact numerical values should be taken from the original experiment outputs rather than estimated.

### 4.2 GraphSAGE

The repository includes temporal GraphSAGE validation artifacts:

- `results/GCN_GraphSAGE/temporal_graphsage_validation_metrics.png`
- `results/GCN_GraphSAGE/temporal_graphsage_validation_confusion_matrix.png`

These figures correspond to validation results. They should not be presented as final held-out test results unless a separate test evaluation is available.

### 4.3 Graph Attention Network (GAT)

The GAT experiment uses graph-attention layers to learn account representations and combines them with transaction features for binary transaction classification.

The documented temporal split is:

| Stage | Transaction steps |
|---|---|
| Historical graph context | 1–279 |
| Training | 280–319 |
| Validation | 320–354 |
| Final test | 355–743 |

The saved final-test evaluation uses a decision threshold of `0.75`.

Implementation and experiment details are available in `notebooks/04.GAT.ipynb`.

## 5. GAT Explainability

GNNExplainer was applied to a selected validation fraud example to investigate the local model prediction.

The saved outputs include:

- Feature-mask importance scores for the four account features.
- Edge-importance results for a local directed subgraph.
- Explanation visualizations and CSV outputs.
- An edge-removal diagnostic.

The selected local subgraph contains 11 nodes and 9 directed edges.

These results provide a local explanation for one example. They do not establish causal relationships or guarantee that the same features and edges explain every fraud prediction.

## 6. Evaluation Principles

The experiments use several evaluation settings and model-specific artifacts.

The following principles guide interpretation:

1. Report precision, recall, F1-score, PR-AUC, ROC-AUC, and confusion-matrix counts where available.
2. Select decision thresholds using validation data rather than final test labels.
3. Distinguish random evaluation from temporal evaluation.
4. Identify whether a result is from training, validation, or final testing.
5. Compare models directly only when their splits, features, preprocessing, graph context, thresholds, and metric definitions are sufficiently aligned.
6. Treat results on synthetic PaySim data as experimental evidence, not proof of real-world deployment performance.
