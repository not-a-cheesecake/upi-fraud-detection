# Results and interpretation

## Traditional ML baselines
Source: `results/Traditional_ML/model_comparison_results.csv`.

| Model | Split | Precision | Recall | F1-score | PR-AUC | ROC-AUC |
|---|---|---:|---:|---:|---:|---:|
| Logistic Regression | Random | 0.0238 | 0.9598 | 0.0464 | 0.5817 | 0.9908 |
| Logistic Regression | Temporal | 0.1102 | 0.8828 | 0.1959 | 0.6801 | 0.9880 |
| Random Forest | Random | 0.0983 | 0.9897 | 0.1789 | 0.9193 | 0.9994 |
| Random Forest | Temporal | 0.2796 | 0.9547 | 0.4325 | 0.8995 | 0.9991 |
| XGBoost | Random | 0.9730 | 0.8125 | 0.8856 | 0.9544 | 0.9997 |
| XGBoost | Temporal | 0.9997 | 0.7158 | 0.8343 | 0.9570 | 0.9998 |

The selected XGBoost temporal run has the highest temporal PR-AUC among the listed traditional ML runs. Logistic Regression and Random Forest show different precision/recall trade-offs. ROC-AUC alone should not summarize performance on this highly imbalanced dataset.

## GAT final temporal test
Source: saved GAT final-test results and confusion matrix.

| Metric | Value |
|---|---:|
| Test transactions | 1,293,523 |
| Actual fraud cases | 4,258 |
| Decision threshold | 0.75 |
| PR-AUC | 0.685268 |
| ROC-AUC | 0.812556 |
| Precision | 0.916696 |
| Recall | 0.617661 |
| F1-score | 0.738038 |
| Flagged transactions | 2,869 |

Confusion matrix (actual rows; predicted columns):

| | Predicted non-fraud | Predicted fraud |
|---|---:|---:|
| Actual non-fraud | 1,289,026 | 239 |
| Actual fraud | 1,628 | 2,630 |

At the recorded threshold, GAT precision is high while recall is lower: it flags many fraud transactions but misses some actual fraud. Threshold choice affects the trade-off between false alarms and missed fraud.

## GNNExplainer results
The saved explanation status reports one selected validation fraud transaction with full-graph and local-subgraph fraud probability approximately 0.937868 at threshold 0.75. The local subgraph contains 11 nodes and 9 directed edges.

Saved mean feature-mask scores:

| Feature | Mean importance |
|---|---:|
| sent_count | 0.3147 |
| sent_amount | 0.3064 |
| received_count | 0.0374 |
| received_amount | 0.0306 |

For this selected example, sent-count and sent-amount masks have the largest reported scores. These values are specific to this explainer run and sample; they are not universal feature rankings or causal effects.

The edge-removal diagnostic changed fraud probability by about 0.000124 after removing the top 1 edge, 0.000950 after removing the top 3, 0.002849 after removing the top 5, and 0.173727 after removing all 9. The report notes that differences between top-ranked and bottom-ranked edge removals were small for the tested 3- and 5-edge cases. This is limited, sample-specific evidence—not a dataset-wide validation of explanation quality.

## Comparison caveat
Traditional ML metrics and GAT metrics come from separate experiment workflows. Confirm feature sets, split boundaries, preprocessing, and threshold procedures before treating numerical differences as a strict head-to-head benchmark. 
