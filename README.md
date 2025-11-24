# Network-Anomaly-Detection-NSL-KDD

Network Traffic Anomaly Detection using XGBoost

A machine learning project that classifies network traffic as Normal or Attack using the NSL-KDD dataset. The model is built with XGBoost and designed to run in Google Colab or any Python environment.

## Dataset
- Source: [NSL-KDD Dataset](https://www.unb.ca/cic/datasets/nsl.html)
- Classes: Normal, multiple attack types (DoS, Probe, R2L, U2R)
- Training samples: 125,973
- Test samples: 22,544

## Data Processing
- Categorical features (`protocol_type`, `service`, `flag`) encoded using Label Encoding.
- Feature selection based on correlation and importance; redundant engineered features were removed.
- Binary labels created for Normal vs Attack classification.

## Model
- XGBoost classifier
- Parameters: 300 estimators, max depth 6, learning rate 0.1
- Multi-class classification (all known attacks) + binary classification (Normal vs Attack)

## Training
- Trained on NSL-KDD training set
- Evaluated on test set including unseen attack types
- Metrics: Accuracy, Precision, Recall, F1-score
- Feature importance analyzed and visualized

## Results
- Multi-class Test Accuracy: ~0.865
- Binary classification accuracy: ~0.99
- Top features: `count`, `srv_count`, `src_bytes`, `dst_bytes`, `protocol_type`, `flag`, `serror_rate`, `rerror_rate`

### Confusion Matrix (Binary)
<img width="400" height="400" src="images/binary_confusion_matrix.png" />

### Feature Importance
<img width="400" height="400" src="images/feature_importance.png" />

## Usage
```python
import joblib
import numpy as np

# Load model
clf = joblib.load('xgb_nslkdd_model.pkl')

# Example single network flow input (replace values with your flow)
x_sample = np.array([[0, 0, 0, 0, 100, 200, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 1, 10, 5, 0.0, 0.0, 0.0, 0.0, 1.0, 0.5, 0.0, 0, 0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0]])
prediction = clf.predict(x_sample)
print("Normal" if prediction[0]==0 else "Attack")
