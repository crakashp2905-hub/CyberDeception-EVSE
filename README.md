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

## Results & Visualizations

### Cyber-Deception Interface (Live System)
| | |
|---|---|
| ![Recon detection](images/deception_interface_recon_detection.jpg) | ![OCPP injection](images/deception_interface_ocpp_injection.jpg) |
| TCP Stealth/SYN Scan detected in real-time | CRITICAL: Malformed OCPP Packet / Injection Attempt |

### Model Results
![Loss Curve](images/loss_curve.jpg)
![Feature Correlation](images/feature_correlation_isDoS.jpg)

### Exploratory Data Analysis
| | |
|---|---|
| ![Attack dist](images/eda_attack_distribution.jpg) | ![Attack group](images/eda_attack_group_distribution.jpg) |
| ![Label dist](images/eda_label_distribution.jpg) | ![State dist](images/eda_state_distribution.jpg) |

### Power Consumption Sensor Distributions
| | |
|---|---|
| ![shunt voltage](images/power_shunt_voltage_dist.jpg) | ![bus voltage](images/power_bus_voltage_dist.jpg) |
| ![current](images/power_current_dist.jpg) | ![power mW](images/power_mW_dist.jpg) |

## Requirements

```
pandas
numpy
scikit-learn
xgboost
matplotlib
seaborn
```
