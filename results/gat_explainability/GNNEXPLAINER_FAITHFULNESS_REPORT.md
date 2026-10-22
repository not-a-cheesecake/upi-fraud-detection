# GNNExplainer Faithfulness Test

## Test scope
One selected validation fraud transaction.
This is a single-sample diagnostic, not a dataset-wide conclusion.

## Original prediction
- Fraud probability: 0.937868
- Decision threshold: 0.75

## Edge-removal test

| Condition | Fraud probability | Absolute change |
|---|---:|---:|
| Original | 0.937868 | 0.000000 |
| Remove top 1 edge | 0.937744 | 0.000124 |
| Remove top 3 edges | 0.936918 | 0.000950 |
| Remove top 5 edges | 0.935019 | 0.002849 |
| Remove all 9 edges | 0.764141 | 0.173727 |

## Top-ranked versus bottom-ranked edge removal

| Condition | Fraud probability | Absolute change |
|---|---:|---:|
| Remove top 3 edges | 0.936918 | 0.000950 |
| Remove bottom 3 edges | 0.937107 | 0.000760 |
| Remove top 5 edges | 0.935019 | 0.002849 |
| Remove bottom 5 edges | 0.935917 | 0.001950 |

## Interpretation
Removing the top-ranked edges caused slightly larger probability
changes than removing the same number of bottom-ranked edges.
However, the differences were small for 3- and 5-edge removals.
Removing all 9 edges caused a larger probability decrease, to
0.764141, which remains above the 0.75 decision threshold.

These results provide limited evidence of edge-ranking faithfulness
for this sample. They do not establish explanation quality across
the dataset. Further testing on additional samples is recommended.

## Important limitation
Edge deletion changes the input graph and may introduce distribution
shift. These results should be interpreted as a diagnostic rather
than proof of causality.
