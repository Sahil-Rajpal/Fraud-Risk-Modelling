# 📌 Credit Risk Modeling

## 🎯 Project Objective  

The goal of this project is to build a **machine learning model** to predict fraudulent credit card transactions. By analyzing transaction and customer data, the model helps stakeholders:  

- Detect fraudulent patterns in real-time  
- Minimize financial losses due to fraud  
- Improve trust and security in digital transactions  
- Optimize fraud prevention strategies for financial institutions  

## 📂 Dataset

- **Source:** [Credit Card Fraud Detection Dataset (Kaggle)](https://www.kaggle.com/datasets)   
- **Duration Covered:** 1st Jan 2019 – 31st Dec 2020  
- **Scale:**  
  - 1000 customers  
  - 800 merchants  
  - Transactions across multiple categories (e.g., food, travel, shopping, personal care, entertainment, etc.)  
- **Files:**  
  - `fraudTrain.csv` – Training dataset  
  - `fraudTest.csv` – Testing dataset  
- **Features:** 46 columns including:  
  - Transaction details (`trans_date_trans_time`, `cc_num`, `merchant`, `category`, `amt`)  
  - Customer details (`first`, `last`, `gender`, `street`)  
  - Target label: `is_fraud` (0 = Legitimate, 1 = Fraudulent)  

The dataset provides a realistic representation of both legitimate and fraudulent transactions, enabling the development of **fraud detection models** that can identify abnormal spending patterns and reduce financial risks. 


## 🎯 Business Objectives  

The primary objective of this project is to **assess credit risk** by predicting the likelihood of a customer defaulting on their credit obligations.  

### Specific Goals:  
- 📊 **Data Exploration & Preprocessing** – Understand data distribution, handle missing values, outliers, and perform feature engineering.  
- 🤖 **Model Development** – Train and evaluate multiple machine learning models (Decision Trees , Random Forest, XGBoost, etc.) to classify borrowers as *low-risk* or *high-risk*.  
- 📈 **Performance Evaluation** – Compare models using metrics like Accuracy, Precision, Recall, F1-score, AUC-ROC and KS Metrics to identify the best-performing model.  
- 🔎 **Interpretability** – Use feature importance and Woe-Iv values to explain which factors contribute most to Fraud risk.  
- 🏦 **Business Impact** – Provide a reliable tool for financial institutions to minimize risk of fruadlent transactions.


  


---

