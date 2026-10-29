# Methodology

## 1. Problem definition
The task is binary classification of financial transactions as fraudulent or legitimate using the PaySim synthetic transaction dataset. The target label is `isFraud`. PaySim is synthetic, so results should not be described as validated performance on real UPI transactions.

## 2. Dataset and class imbalance
The dataset contains transaction fields such as time step, transaction type, amount, origin/destination account identifiers, balances, and the fraud label. Fraud is rare relative to legitimate transactions. Evaluation therefore emphasizes precision, recall, F1-score, PR-AUC (average precision), and ROC-AUC.

## 3. Traditional ML experiments
The recorded baseline comparison includes Logistic Regression, Random Forest, and XGBoost under random and temporal experiment settings. Results are saved in `results/Traditional_ML/model_comparison_results.csv`.

Recorded temporal results:
- Random Forest: PR-AUC 0.8995, F1-score 0.4325.
- XGBoost: PR-AUC 0.9570, F1-score 0.8343.

See the corresponding notebook and CSV files for details of each run. Check preprocessing, split boundaries, and threshold selection per experiment before making cross-model comparisons.

## 4. Temporal graph/GAT experiment
The GAT workflow represents accounts as graph nodes and historical transactions as directed edges. Four account-level node features are used: `sent_count`, `received_count`, `sent_amount`, and `received_amount`. Transaction-level features are combined with source and destination account embeddings to classify each transaction.

The documented GAT architecture uses two graph-attention convolution layers followed by a transaction classifier. The first attention layer uses 16 hidden channels with 2 attention heads; the second maps the concatenated representation to 16 channels. The classifier concatenates the source embedding, destination embedding, and 10 transaction features, then applies a 16-unit hidden layer and a 2-class output.

The recorded temporal workflow separates historical graph context from later transaction examples: historical steps 1–279, training steps 280–319, validation steps 320–354, and final test steps 355–743. The reported final GAT test threshold is 0.75. Consult `notebooks/04.GAT.ipynb` for implementation details and the exact code path.

## 5. Explainability
The repository includes GNNExplainer outputs for one selected validation fraud transaction:
- feature-mask importance for four account features;
- edge importance for a local directed subgraph;
- plots and CSV outputs;
- an edge-removal faithfulness diagnostic.

The local subgraph contains 11 nodes and 9 directed edges, and its prediction matched the recorded full-graph probability for the selected sample. This is a local, single-example explanation. Importance masks are not causal explanations, and one example cannot establish explanation stability across the dataset. 

## 6. Evaluation protocol
Report confusion-matrix counts together with precision, recall, F1-score, PR-AUC, ROC-AUC, and the selected threshold. Because class imbalance is severe, PR-AUC and precision/recall are particularly important. Threshold selection should use validation data rather than final test labels.

Random and temporal results answer different evaluation questions. A fair model comparison requires consistent data partitions, feature availability, threshold-selection rules, and evaluation metrics. Where these differ, describe results as experiment-specific rather than directly comparable.
