# NSL-KDD Network Intrusion Detection Using XGBoost

## Project Overview
This project implements a Network Intrusion Detection System (NIDS) using the **NSL-KDD dataset** and the **XGBoost classifier**. It performs both **multi-class** and **binary classification** to detect attacks in network traffic, providing insights into attack types and key features influencing anomalies.

## Features

### Data Handling
- Loads **NSL-KDD dataset** from Kaggle.
- Converts raw `.txt` files into `.csv` for easier processing.
- Splits data into features (`X`) and labels (`y`).

### Data Preprocessing
- Encodes categorical features (`protocol_type`, `service`, `flag`) using `LabelEncoder`.
- Handles unseen labels in the test set gracefully.

### Exploratory Data Analysis (EDA)
- Visualizes **class distribution** of the training set using log-scale plots.
- Shows **attack type distribution** in the dataset.
- Provides **summary statistics** of network traffic features.

### Model Training
- Uses **XGBoost classifier** with the following hyperparameters:
  - `n_estimators=300`
  - `max_depth=6`
  - `learning_rate=0.1`
  - `use_label_encoder=False`
  - `eval_metric='mlogloss'`
  - `random_state=42`
  - `n_jobs=-1`
- Trains on the processed training dataset.
- Predicts both **multi-class** (specific attack type) and **binary** (normal vs attack) labels.

### Evaluation
- **Multi-Class Classification**:
  - Test Accuracy: `0.865` 
  - Classification report:
    <img width="411" height="488" alt="Screenshot 2025-11-24 233405" src="https://github.com/user-attachments/assets/e78486bd-2217-4f35-b9f9-1f36bb22f7fa" />

- **Binary Classification (Normal vs Attack)**:
  - Test Accuracy: `0.871`
  - Classification report:
    <img width="402" height="147" alt="Screenshot 2025-11-24 233225" src="https://github.com/user-attachments/assets/675863f1-c939-45eb-bd50-0ae0e192467c" />

- **Binary Confusion Matrices**:
  <img width="522" height="470" alt="image" src="https://github.com/user-attachments/assets/814a5cfc-12cc-4921-84e2-2171b12ac65b" />


### Top Network Features
<img width="489" height="329" alt="Screenshot 2025-11-24 233014" src="https://github.com/user-attachments/assets/ba90a0ca-4083-499b-8226-6909a71be099" />

## Dependencies
- Python 3.x
- pandas
- numpy
- matplotlib
- seaborn
- scikit-learn
- xgboost


