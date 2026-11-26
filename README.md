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

## What it misses
Recall is 86% overall, but this is driven by Neptune (SYN flood, 70% of test attacks, 100% caught).
Excluding Neptune, recall is ~53%.

| Attack | Recall |
|---|---|
| neptune | 100% |
| portsweep | 98.5% |
| ipsweep | 81.8% |
| satan | 62.6% |
| nmap | 45.2% |
| teardrop | 12.1% |
| smurf | 9.0% |
| warezclient | 7.8% |
| back | 0.7% |
| pod | 0% |

Unsupervised anomaly detection catches loud attacks (floods, scans) but misses attacks that
mimic normal traffic. Next step: a supervised baseline (Random Forest) for comparison.

## Limitations
The test set is ~50% attacks. Real networks are 99%+ normal, so expect more false alarms in production.

## Stack
Python, Pandas, scikit-learn, Google Colab