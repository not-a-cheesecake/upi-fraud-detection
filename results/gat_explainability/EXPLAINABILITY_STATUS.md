# GAT Explainability Work Status

**Status updated:** 2026-10-20  
**Owner area:** Graph Attention Network (GAT) evaluation and explainability  
**Dataset:** PaySim synthetic financial transactions (not real UPI transaction records)

## Completed GAT evaluation

The existing GAT epoch-4 checkpoint was evaluated on the temporal test split using a decision threshold of 0.75.

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

Confusion matrix (rows = actual class [non-fraud, fraud], columns = predicted class [non-fraud, fraud]):

```text
                 Predicted non-fraud   Predicted fraud
Actual non-fraud       1,289,026              239
Actual fraud               1,628            2,630
```

These numbers document the saved evaluation output. They do not, by themselves, establish that the model's predictions are explainable.

## Current artifacts (to be added from the experiment workspace)

- GAT experiment notebook: `04.GAT.ipynb`
- Final test metrics: `final_test_results.csv`
- Validation threshold analysis: `gat_validation_threshold_results.csv`
- Evaluation plots: final metrics, confusion matrix, and validation threshold analysis
- Evaluation plot README

## Explainability status

**GNNExplainer attribution is still pending.** No verified GNNExplainer feature/node/edge attribution output is claimed in this report. A prediction probability or a confusion matrix is not a feature attribution explanation.

Before publishing an explanation, validate that the selected example, graph subgraph, model output, and explainer output are consistent with the saved model and temporal evaluation setup. The current runtime attempts encountered an implausible model output on some sampled graph inputs, so those samples must not be presented as valid explanations without further diagnosis.

Traditional-model SHAP results should be added only if the relevant baseline model outputs and attribution artifacts are available and their ownership is confirmed with the team.

## Data and reproducibility notes

- Do not commit the raw PaySim CSV to this repository.
- Do not commit large model checkpoints unless the team explicitly decides how to store them.
- Record the checkpoint, threshold, split, and explainer settings alongside any future explanation artifacts.
- Treat PaySim as synthetic data; avoid describing these records as real UPI transactions.

## Next steps

1. Add the notebook and existing evaluation CSV/plot files from the experiment workspace.
2. Resolve the graph/model-output issue for a suitable example.
3. Run and validate GNNExplainer on a manageable, correctly constructed subgraph.
4. Save the explanation outputs and update this status document with the actual method, settings, and findings.
