# Limitations and Future Work

## 1. Limitations

### 1.1 Synthetic Dataset

The project uses PaySim, a synthetic financial transaction dataset. Although it supports experimentation with fraud detection methods, it does not represent actual UPI transaction records. Therefore, the reported results do not establish performance on live financial systems.

### 1.2 Class Imbalance

Fraudulent transactions represent a small proportion of the dataset. Accuracy alone can therefore be misleading. Precision, recall, F1-score, PR-AUC, and confusion-matrix counts are important for understanding model performance.

### 1.3 Different Evaluation Settings

The project includes random and temporal experiments. These settings measure different forms of generalization and should not be treated as interchangeable.

The traditional ML models, GCN, GraphSAGE, and GAT also have different saved evaluation artifacts. GraphSAGE results are represented by temporal validation figures, GCN results by performance figures, and GAT by a documented final temporal test evaluation. A definitive ranking across all models requires compatible evaluation settings.

### 1.4 Incomplete Consolidated GCN and GraphSAGE Metrics

The current `results/GCN_GraphSAGE/` directory contains GCN and GraphSAGE performance figures but does not contain a consolidated metrics CSV for both experiments.

Exporting the underlying metrics with their split names, evaluation stages, thresholds, and metric definitions would improve reproducibility.

### 1.5 Limited Explainability Evaluation

The saved GNNExplainer outputs focus on one selected validation fraud example. This does not establish that the same features and edges explain other predictions.

Feature and edge importance scores should not be interpreted as causal relationships. Explanation stability and faithfulness require further evaluation across multiple examples.

### 1.6 Notebook-Oriented Implementation

The tracked implementation is primarily notebook-based. The project does not currently provide a separate, validated reusable implementation under `src/`.

Organizing the code into reusable modules could improve maintainability, testing, and future deployment work.

### 1.7 Reproducibility

Reproducing all experiments requires consistent dataset preparation, preprocessing, graph construction, package versions, random seeds, model settings, and evaluation procedures. These details should be documented alongside the relevant outputs.

## 2. Future Work

1. **Consolidate metrics:** Export GCN and GraphSAGE metrics to CSV with explicit evaluation stages, thresholds, and metric definitions.
2. **Standardize evaluation:** Verify that model comparisons use compatible temporal splits, features, preprocessing, graph context, and threshold-selection procedures.
3. **Strengthen temporal evaluation:** Evaluate GCN and GraphSAGE on a clearly defined held-out temporal test set if the existing experiment design and saved artifacts support it.
4. **Expand explainability experiments:** Apply GNNExplainer to multiple correctly classified and misclassified fraud and non-fraud examples.
5. **Assess explanation stability:** Compare explanations across samples and repeated runs instead of relying on a single local example.
6. **Improve reproducibility:** Record random seeds, software versions, hyperparameters, dataset preparation steps, and artifact provenance.
7. **Improve code organization:** Consider extracting reusable preprocessing, graph construction, training, evaluation, and explainability code from notebooks into tested modules.
8. **Investigate additional methods:** Explore alternative GNN architectures and threshold-selection strategies under a consistent evaluation protocol.
9. **Pursue real-world validation:** If suitable data becomes lawfully available, evaluate generalization while protecting financial and personal information.

## 3. Conclusion

The project provides an experimental comparison of traditional machine-learning and graph-based approaches to financial transaction fraud detection using synthetic PaySim data. It also includes temporal GAT evaluation and a local GNNExplainer case study.

The current artifacts support further investigation, but differences in evaluation settings, incomplete consolidated GCN and GraphSAGE metrics, and the synthetic nature of the dataset limit the conclusions that can be drawn. Addressing these limitations would strengthen the reliability, reproducibility, and practical relevance of future work.
