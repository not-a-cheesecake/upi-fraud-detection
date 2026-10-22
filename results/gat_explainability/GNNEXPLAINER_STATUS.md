# GNNExplainer Status

## Status
GNNExplainer successfully executed on a local subgraph for one
selected fraud transaction. Existing GAT checkpoint was used;
GAT was not retrained for this explanation.

## Selected transaction
- Validation position: 44505
- Actual label: Fraud (1)
- Full-graph fraud probability: 0.9378675
- Local-subgraph fraud probability: 0.9378675
- Decision threshold: 0.75
- Prediction: Fraud

## Local subgraph
- Nodes: 11
- Directed edges: 9
- Node features: 4
- Local prediction matched the full-graph probability.

## Node features
Features: sent_count, received_count, sent_amount, received_amount.

Mean GNNExplainer mask scores are saved in
`gnnexplainer_feature_importance.csv`.

## Edges
Edge importance scores are saved in
`gnnexplainer_edge_importance.csv`.
Global node IDs identify the directed edges in the historical graph.

## Deliverables
- gnnexplainer_feature_importance.csv
- gnnexplainer_edge_importance.csv
- gnnexplainer_feature_importance.png
- gnnexplainer_edge_importance.png
- GNNEXPLAINER_STATUS.md

## Limitations
This explanation covers one selected validation fraud transaction,
not the entire dataset. Mask scores indicate model-specific
importance and do not establish causality or generalization.
