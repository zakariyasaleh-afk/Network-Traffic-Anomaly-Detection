# Network Anomaly Detection Using XGBoost on NSL-KDD Dataset

Detecting network intrusions and anomalies using machine learning. This project implements an **XGBoost classifier** to identify normal and attack traffic using the NSL-KDD dataset.

---

## Dataset
- **Source:** [NSL-KDD Dataset](https://www.kaggle.com/datasets/hassan06/nslkdd)  
- **Type:** Network traffic flows  
- **Training set:** `KDDTrain+.txt` (~125,973 samples)  
- **Test set:** `KDDTest+.txt` (~22,544 samples)  
- **Classes:** Normal traffic + 37 attack types  
- **Purpose:** Evaluate anomaly detection and classification performance  

---

## Data Preprocessing
- Removed `label` and `difficulty_level` from features.  
- Encoded categorical features (`protocol_type`, `service`, `flag`) using **Label Encoding**.  
- Filtered test samples that contain attack types **not present in training set**.  
- No additional feature engineering was performed; all features are original from NSL-KDD.  

---

## Model
- **Algorithm:** XGBoost Classifier (`XGBClassifier`)  
- **Parameters:**  
  - `n_estimators=300`  
  - `max_depth=6`  
  - `learning_rate=0.1`  
  - `eval_metric='mlogloss'`  
  - `use_label_encoder=False`  
- Multi-class classification across all known attack types.  
- Binary classification derived from mapping `normal` → 0, `attack` → 1.

---

## Training & Evaluation
- Trained on **entire training set**.  
- Evaluated on **filtered test set** (only attack types seen during training).  

### Results

**Binary Classification (Normal vs Attack):**
- **Accuracy:** 0.871  
- Confusion matrix visualized using Seaborn.  

**Multi-class Classification:**
- Classification report with precision, recall, and F1-score per attack type.

---

## Feature Importance
- Top 10 features contributing to classification:

| Feature        | Description                                      | Importance |
|----------------|--------------------------------------------------|-----------|
| count          | Number of connections from a host                | 0.XXX     |
| srv_count      | Number of connections to a specific service     | 0.XXX     |
| src_bytes      | Data volume sent by host                          | 0.XXX     |
| dst_bytes      | Data volume received by host                     | 0.XXX     |
| protocol_type  | Protocol used (TCP/UDP/ICMP)                    | 0.XXX     |
| flag           | Connection status flags                           | 0.XXX     |
| serror_rate    | Rate of TCP connection errors                     | 0.XXX     |
| rerror_rate    | Rate of failed connections                        | 0.XXX     |
| same_srv_rate  | Proportion of connections to same service       | 0.XXX     |
| diff_srv_rate  | Proportion of connections to different services | 0.XXX     |

*Importance scores are derived from XGBoost feature importance.*

---

## Visualization
- Class distribution in training set shown using log-scaled count plots.  
- Attack type distribution plotted for exploratory analysis.  
- Binary confusion matrix heatmap visualized for Normal vs Attack classification.

---

## Usage
1. **Download model:** `xgb_nslkdd_model.pkl`  
2. **Load in Python:**

```python
import joblib
clf = joblib.load("xgb_nslkdd_model.pkl")

# Example: predict using new network traffic sample
import numpy as np

sample = np.array([[...feature_values...]])
prediction = clf.predict(sample)
print("Prediction:", prediction[0])

