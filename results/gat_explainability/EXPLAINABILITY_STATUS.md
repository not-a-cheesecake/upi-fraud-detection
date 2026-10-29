# GAT Explainability Status

**Status:** GAT evaluation and a local GNNExplainer case study completed  
**Dataset:** PaySim synthetic financial transaction data  
**Model:** Graph Attention Network (GAT)

## 1. GAT Evaluation

The saved epoch-4 GAT checkpoint was evaluated on the temporal test split using a decision threshold of 0.75.

| Metric | Result |
|---|---:|
| Test transactions | 1,293,523 |
| Actual fraud cases | 4,258 |
| Decision threshold | 0.75 |
| PR-AUC / Average Precision | 0.685268 |
| ROC-AUC | 0.812556 |
| Precision | 0.916696 |
| Recall | 0.617661 |
| F1-score | 0.738038 |
| Flagged transactions | 2,869 |

### Confusion Matrix

Rows represent actual classes; columns represent predicted classes.

| | Predicted non-fraud | Predicted fraud |
|---|---:|---:|
| Actual non-fraud | 1,289,026 | 239 |
| Actual fraud | 1,628 | 2,630 |

These results describe the saved temporal test evaluation. They do not, by themselves, establish explainability.

## 2. GNNExplainer

GNNExplainer was run on a local subgraph for one selected validation fraud transaction using the existing GAT checkpoint. The GAT model was not retrained for this explanation.

### Selected Example

- Validation position: 44505
- Actual label: Fraud (1)
- Full-graph fraud probability: approximately 0.937868
- Local-subgraph fraud probability: approximately 0.937868
- Decision threshold: 0.75
- Local subgraph: 11 nodes and 9 directed edges
- Node features: `sent_count`, `received_count`, `sent_amount`, `received_amount`

The selected example was classified as fraud by the saved model.

### Feature Importance

The saved mean feature-mask importance scores are:

| Feature | Mean importance |
|---|---:|
| `sent_count` | 0.3147 |
| `sent_amount` | 0.3064 |
| `received_count` | 0.0374 |
| `received_amount` | 0.0306 |

For this example, `sent_count` and `sent_amount` received the largest feature-mask importance scores. These values are specific to this example and explainer run; they are not causal effects or universal rankings.

### Edge Importance and Diagnostic

The edge-importance scores are saved in `gnnexplainer_edge_importance.csv`. A separate edge-removal diagnostic is documented in `GNNEXPLAINER_FAITHFULNESS_REPORT.md`.

Removing the top-ranked edges caused slightly larger probability changes than removing the same number of bottom-ranked edges in the selected example. However, the differences for removing three or five edges were small. Removing all nine edges produced a larger probability change.

This is a limited, sample-specific diagnostic. It does not establish explanation faithfulness across the dataset.

## 3. Explainability Artifacts

The repository contains:

- `gnnexplainer_feature_importance.csv`
- `gnnexplainer_edge_importance.csv`
- `gnnexplainer_feature_importance.png`
- `gnnexplainer_edge_importance.png`
- `gnnexplainer_edge_comparison_test.csv`
- `gnnexplainer_faithfulness_test.csv`
- `GNNEXPLAINER_STATUS.md`
- `GNNEXPLAINER_FAITHFULNESS_REPORT.md`

GAT evaluation plots and related result files are also stored in this directory.

## 4. Limitations

1. The explanation covers one selected validation fraud example, not the entire dataset.
2. Feature and edge importance scores describe model-specific behavior and do not establish causality.
3. Edge removal changes the graph input and may introduce distribution shift.
4. The faithfulness diagnostic is not a dataset-wide evaluation of explanation quality.
5. PaySim is synthetic financial transaction data, not real UPI transaction records.
6. The saved temporal test results and the selected validation explanation represent different evaluation stages.

## 5. Future Work

- Run explanations on multiple fraud and non-fraud examples, including correct and incorrect predictions.
- Evaluate explanation stability across samples and repeated runs.
- Expand faithfulness testing using clearly documented comparison procedures.
- Record model checkpoints, preprocessing, graph construction, explainer settings, and sample identifiers for reproducibility.
- Avoid claiming real-world UPI performance without suitable external validation.

## Conclusion

The repository contains a completed GAT temporal test evaluation and saved GNNExplainer artifacts for a selected validation fraud example. The explanation provides a local case study, not a general guarantee of model interpretability or causal evidence.
