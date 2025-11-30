# NSL-KDD Network Intrusion Detection Using XGBoost

## Project Overview
This project implements a Network Intrusion Detection System (NIDS) using the **NSL-KDD dataset** and the **XGBoost classifier**. It performs both **multi-class** and **binary classification** to detect attacks in network traffic, providing insights into attack types and key features influencing anomalies.

## Dataset
- **Source:** [NSL-KDD (Kaggle)](https://www.kaggle.com/datasets/defcom17/NSL-KDD
)
- **Training file:** KDDTrain+.txt  
- **Testing file:** KDDTest+.txt  
- **Features:** 41  
- **Labels:** multiple attack categories + normal  
- **Handling unseen labels:** test samples with labels not present in training are removed automatically.

### Data Preprocessing
- Encodes categorical features (`protocol_type`, `service`, `flag`) using `LabelEncoder`.
- Handles unseen labels in the test set gracefully.

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

- **Binary Confusion Matrix**:
<img width="522" height="470" alt="image" src="https://github.com/user-attachments/assets/814a5cfc-12cc-4921-84e2-2171b12ac65b" />



## Top 10 Feature Importances

| Feature                         | Importance Score | Description 
|---------------------------------|-----------------|----------------------------------------------
| same_srv_rate                   | 0.509           | Proportion of connections to the same service 
| wrong_fragment                  | 0.063           | Number of wrong fragments in the connection  
| diff_srv_rate                   | 0.059           | Proportion of connections to different services 
| rerror_rate                     | 0.056           | Rate of failed connections or requests 
| src_bytes                       | 0.050           | Data volume sent by the host 
| dst_host_srv_diff_host_rate     | 0.033           | Rate of connections to different hosts for the same service 
| num_compromised                 | 0.033           | Number of compromised conditions 
| protocol_type                   | 0.030           | Type of protocol (TCP/UDP/ICMP)  
| count                           | 0.018           | Number of connections from the host                                     
| dst_host_diff_srv_rate          | 0.017           | Proportion of connections to different services at the destination host 



## Dependencies
- Python 3.x
- pandas
- numpy
- matplotlib
- seaborn
- scikit-learn
- xgboost


