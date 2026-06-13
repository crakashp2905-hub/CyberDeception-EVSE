# ML for Cyber Deception in EV Charging Systems

Machine-learning pipeline for detecting cyberattacks on Electric Vehicle Supply Equipment (EVSE) using multi-modal sensor data — network traffic, host hardware events, and power consumption measurements.

## Dataset

The notebooks use the **EVSE dataset**, which covers two EVSE devices (EVSE-A and EVSE-B) under 17+ distinct attack scenarios captured across three modalities:

| Modality | Source | Size |
|---|---|---|
| Network Traffic | NFStream flow features (86 columns) | ~2.7M flows |
| Host Events | HPC + Kernel events | ~8.5K samples × 915 features |
| Power Consumption | INA219 sensor readings | ~115K samples |

**Attack types covered:** SYN-Flood, TCP-Flood, UDP-Flood, ICMP-Flood, Push-ACK Flood, Port Scan, Aggressive Scan, Vulnerability Scan, SYN-Stealth, OS Fingerprinting, Service Detection, Synonymous IP, Cryptojacking, and more.

> Dataset source: [EVSE Cybersecurity Dataset](https://github.com/Western-OC2-Lab/EVSE-Cybersecurity-Dataset) — not included in this repo.

## Notebooks

| Notebook | Description |
|---|---|
| `EVSE.ipynb` | Data exploration and preprocessing pipeline for all three modalities |
| `EVSE1.ipynb` | Cross-device generalization — train on EVSE-A, evaluate on EVSE-B (network traffic) |
| `EVSE2.ipynb` | Power consumption anomaly detection (Isolation Forest, Random Forest) and network traffic classification |
| `EVSE3.ipynb` | EVSE-B network traffic classification with correlation-based feature selection |

All notebooks are designed for **Google Colab** with data loaded from Google Drive.

## Approach

1. **Preprocessing** — drop identifier columns (IP/MAC), impute NaN/Inf with column medians, binary-encode labels (benign=0, attack=1)
2. **Feature selection** — correlation filtering, removing leakage columns (attack metadata)
3. **Models** — Isolation Forest, Logistic Regression, Random Forest, XGBoost, MLP, LSTM
4. **Evaluation** — accuracy, F1-score, confusion matrix; cross-device generalization tested explicitly

## Setup

Clone the repo and open any notebook in Google Colab. Mount your Google Drive and place the EVSE dataset at `/content/drive/MyDrive/EVSE/`.

```bash
git clone https://github.com/crakashp2905-hub/CyberDeception-EVSE.git
```

## Requirements

```
pandas
numpy
scikit-learn
xgboost
matplotlib
seaborn
```
