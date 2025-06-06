# 🛡️ Intrusion Detection System using Autoencoders (Semi-Supervised Learning)

A high-performing Intrusion Detection System (IDS) built using a **semi-supervised deep learning approach** with **autoencoders**. This project detects cyber attacks using the UNSW-NB15 dataset by modeling normal network behavior and identifying anomalies based on reconstruction error.

---

## 📌 Project Highlights

- 🔍 **Semi-Supervised Approach**: Trained only on normal data, detecting attacks without needing labeled attack samples.
- 📈 **Optimized Threshold Selection**: Uses F1-based thresholding instead of ROC to improve both precision and recall.
- 📊 **Visual Interpretability**: Includes reconstruction error plots, ROC curves, and classification metrics.
<!-- - 🚀 **Exceptional Results**:
  - **F1-score (attack class)**: 0.90  
  - **Recall**: 0.98  
  - **ROC-AUC**: 0.986  
  - **Precision**: 0.84  
  - **Overall Accuracy**: 95% -->

---

## 📂 Dataset

- **Dataset**: [UNSW-NB15 (Sample)](https://www.unsw.adfa.edu.au/unsw-canberra-cyber/cybersecurity/ADFA-NB15-Datasets/)
- Size: ~115MB (used Git LFS for versioning)
- Features: 44 numerical features + binary `Class` label (0 = normal, 1 = attack)

---

## ⚙️ How the Project Works

### 🔸 Step 1: Data Preprocessing
- Split into normal (Dn) and attack (Da) data.
- Train/Validation split on Dn (80/20).
- Combine validation with attack data → test set (Dts).

### 🔸 Step 2: Feature Scaling
- Standardized all input features using `StandardScaler`.

### 🔸 Step 3: Autoencoder Model
- Deep architecture: 64 → 32 → 16 → 32 → 64
- Trained on only normal data to learn a compact representation.

### 🔸 Step 4: Threshold Optimization
- Replaced ROC-based thresholding with **F1-optimized threshold**:
  ```python
  precision, recall, thresholds = precision_recall_curve(labels, errors)
  f1 = 2 * (precision * recall) / (precision + recall + 1e-8)
  best_threshold = thresholds[np.argmax(f1)]
