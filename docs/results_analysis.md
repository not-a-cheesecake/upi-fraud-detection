# Results and Interpretation

## 1. Traditional Machine-Learning Results

Source: `results/Traditional_ML/model_comparison_results.csv`

### 1.1 Random Evaluation

| Model | Precision | Recall | F1-score | PR-AUC | ROC-AUC |
|---|---:|---:|---:|---:|---:|
| Logistic Regression | 0.0238 | 0.9598 | 0.0464 | 0.5817 | 0.9908 |
| Random Forest | 0.0983 | 0.9897 | 0.1789 | 0.9193 | 0.9994 |
| XGBoost | 0.9730 | 0.8125 | 0.8856 | 0.9544 | 0.9997 |

### 1.2 Temporal Evaluation

| Model | Precision | Recall | F1-score | PR-AUC | ROC-AUC |
|---|---:|---:|---:|---:|---:|
| Logistic Regression | 0.1102 | 0.8828 | 0.1959 | 0.6801 | 0.9880 |
| Random Forest | 0.2796 | 0.9547 | 0.4325 | 0.8995 | 0.9991 |
| XGBoost | 0.9997 | 0.7158 | 0.8343 | 0.9570 | 0.9998 |

Among these recorded traditional ML experiments, XGBoost achieves the highest temporal PR-AUC and F1-score. Random Forest has higher temporal recall but lower precision, illustrating the trade-off between detecting fraud and generating false alarms.

Random and temporal results should be interpreted separately because they represent different evaluation settings.

## 2. GCN Results

The repository contains the following GCN performance artifacts:

- `results/GCN_GraphSAGE/GCN_Performance_Matrices.jpeg`
- `results/GCN_GraphSAGE/gcn_prototype_performance.png`

These figures document the available GCN experiment results. The current results directory does not contain a consolidated GCN metrics CSV, so exact numerical values are not reproduced here.

Before using GCN results in a research paper, verify the metrics against the original experiment output and record the evaluation split and threshold.

## 3. GraphSAGE Temporal Validation

The repository includes two GraphSAGE validation figures:

- `results/GCN_GraphSAGE/temporal_graphsage_validation_metrics.png`
- `results/GCN_GraphSAGE/temporal_graphsage_validation_confusion_matrix.png`

These artifacts represent temporal validation results, not necessarily final held-out test performance.

The original experiment output should be consulted before transcribing exact numerical metrics. A consolidated GraphSAGE metrics CSV is not currently available in this results directory.

## 4. GAT Final Temporal Test Results

The saved GAT final-test evaluation uses a decision threshold of `0.75`.

### 4.1 Evaluation Summary

| Metric | Value |
|---|---:|
| Test transactions | 1,293,523 |
| Actual fraud cases | 4,258 |
| Decision threshold | 0.75 |
| Precision | 0.916696 |
| Recall | 0.617661 |
| F1-score | 0.738038 |
| PR-AUC | 0.685268 |
| ROC-AUC | 0.812556 |
| Flagged transactions | 2,869 |

### 4.2 Confusion Matrix

Rows represent actual classes and columns represent predicted classes.

| | Predicted non-fraud | Predicted fraud |
|---|---:|---:|
| Actual non-fraud | 1,289,026 | 239 |
| Actual fraud | 1,628 | 2,630 |

At the recorded threshold, the model identifies many flagged transactions correctly, resulting in high precision. However, it misses some actual fraud cases, as reflected in its recall.

The decision threshold influences the balance between false positives and false negatives. Operational use would require choosing a threshold according to the costs of missed fraud and unnecessary alerts.

## 5. GNNExplainer Results

The saved GNNExplainer report describes one selected validation fraud example.

The reported full-graph and local-subgraph fraud probability was approximately `0.937868`, above the decision threshold of `0.75`.

The selected local subgraph contains 11 nodes and 9 directed edges.

### 5.1 Feature Importance

| Account feature | Mean importance |
|---|---:|
| `sent_count` | 0.3147 |
| `sent_amount` | 0.3064 |
| `received_count` | 0.0374 |
| `received_amount` | 0.0306 |

For this selected example, `sent_count` and `sent_amount` have the largest reported feature-mask importance scores.

These values are specific to this example and explainer run. They should not be interpreted as causal effects or as universal feature rankings across the dataset.

### 5.2 Edge-Removal Diagnostic

The saved diagnostic reports the following approximate changes in fraud probability after removing edges from the selected local subgraph:

| Edges removed | Change in fraud probability |
|---|---:|
| Top 1 edge | 0.000124 |
| Top 3 edges | 0.000950 |
| Top 5 edges | 0.002849 |
| All 9 edges | 0.173727 |

The probability changes indicate that removing all selected local edges affects the prediction more than removing only a few edges in this example. This is a limited, sample-specific diagnostic and does not establish explanation faithfulness across the full dataset.

## 6. Cross-Model Interpretation

The available traditional ML, GCN, GraphSAGE, and GAT artifacts do not all represent identical evaluation settings.

- Traditional ML results include random and temporal evaluations.
- GCN results are currently represented by performance figures without a consolidated metrics CSV in the corresponding results directory.
- GraphSAGE artifacts document temporal validation.
- GAT has a documented final temporal test evaluation and local explainability outputs.

Therefore, a definitive ranking across all models should not be claimed until the data splits, feature sets, preprocessing, graph context, thresholds, and metric definitions have been verified and aligned.

Finally, all reported experiments use synthetic PaySim data. Further validation would be necessary before drawing conclusions about real-world UPI fraud detection.
