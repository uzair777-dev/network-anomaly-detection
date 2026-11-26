# Network Anomaly Detection

Detects network attacks using an Isolation Forest trained only on normal traffic.

## Dataset
NSL-KDD: 125,973 connections, 41 features (67,343 normal, 58,630 attacks).

## Method
- One-hot encoded protocol, service and flag columns
- Trained Isolation Forest on normal traffic only
- Tested on a 30% held-out split (normal + attacks)

## Results (attack class)
| Metric | Score |
|---|---|
| Precision | 0.94 |
| Recall | 0.86 |
| F1 | 0.90 |
| Accuracy | 0.91 |

## Limitations
The test set is ~50% attacks. Real networks are 99%+ normal, so expect more false alarms in production.

## Stack
Python, Pandas, scikit-learn, Google Colab