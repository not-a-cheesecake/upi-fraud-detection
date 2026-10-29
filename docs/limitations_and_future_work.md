# Limitations and future work

## Dataset limitations
- PaySim is synthetic transaction data, not actual UPI transaction records.
- Results may not generalize to real banking systems, payment behavior, or operational fraud patterns.

## Class imbalance and operational trade-offs
- Fraud cases are rare, so accuracy can be misleading.
- High precision may come with missed fraud cases; report precision, recall, F1-score, PR-AUC, and confusion-matrix counts together.
- Thresholds should be selected on validation data and assessed on an untouched test set.

## Model-comparison limitations
- Results originate from multiple notebooks and experiment configurations. Confirm consistent data partitions, preprocessing, feature sets, and threshold selection before claiming one model is definitively better.
- GNN and traditional ML models may consume different representations, so comparisons should explicitly describe those differences.

## Explainability limitations
- Current GNNExplainer artifacts document one selected validation fraud transaction.
- Feature and edge masks are model-specific importance signals, not causal claims.
- The edge-removal faithfulness check is a single-sample diagnostic. Removing graph edges may shift the input distribution, and differences for removing a few top versus bottom edges were small.
- More examples, repeated runs, stability checks, and controlled comparison baselines are needed for dataset-wide claims.

## Engineering next steps
- Experiment logic currently lives primarily in notebooks. A future refactor could extract shared preprocessing, graph construction, model definitions, evaluation, and explainability helpers into `src/` while preserving existing notebooks as experiment records.
- Add compatible PyTorch/PyTorch Geometric version notes for the GAT workflow.
- Add a consolidated comparison table documenting each model's split, features, threshold-selection procedure, and test metrics.
