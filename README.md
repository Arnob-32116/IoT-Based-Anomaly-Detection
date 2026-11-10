# IoT-Based Anomaly Detection 🛡️

A **hybrid machine learning framework** that detects abnormal behaviour in IoT network traffic and identifies the type of attack, using the **IoT-23** dataset.

## 🧠 Architecture
```
Network traffic ──► Stage 1: Autoencoder (anomaly detection)
                        │  high reconstruction error = anomaly
                        ▼
                    Stage 2: Classifier (attack type)
                        Random Forest (primary) / Decision Tree
                        ▼
                    Optional: INT8 dynamic quantization for edge deployment
```
- **Autoencoder (PyTorch)** – bottleneck `N → 64 → 32 → 16 → 32 → 64 → N`, trained on benign traffic only. The anomaly threshold is the 95th percentile of reconstruction error on benign validation data.
- **Random Forest / Decision Tree (scikit-learn)** – trained on SMOTE-balanced multiclass data to classify the attack type; Random Forest is also used for feature-importance ranking.
- **Quantization** – PyTorch dynamic quantization of the autoencoder's linear layers to INT8 to cut model size and latency for IoT devices.

## 📂 Notebooks
| Notebook | Purpose |
|---|---|
| `IoT23_Preprocessing_v2-4-2.ipynb` | Latest preprocessing pipeline → `.npy` arrays |
| `IoT23_Preprocessing_v2-2.ipynb`, `v2-3` | Earlier preprocessing versions |
| `IoT23_ModelTraining_v1_Final.ipynb` | Autoencoder + classifier training, evaluation and quantization |

## 🛠️ Tech stack
Python · PyTorch · scikit-learn · imbalanced-learn (SMOTE) · Pandas · NumPy · Matplotlib · Seaborn · Google Colab

## 🚀 Running
1. Open the preprocessing notebook in Google Colab and point it at the IoT-23 dataset in your Drive.
2. Run the training notebook on the generated `.npy` arrays.
