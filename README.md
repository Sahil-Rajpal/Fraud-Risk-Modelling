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

## 📂 Data Description  

The project uses the **fraudTrain.csv** and **fraudTest.csv** dataset, which contains detailed information about credit card transactions.  
Below are the key fields:  

- **Unnamed: 0** → Unique ID for each transaction  
- **trans_date_trans_time** → Date and time of the transaction  
- **cc_num** → Credit card number  
- **merchant** → Merchant name where the transaction occurred  
- **category** → Transaction category (e.g., personal_care, health_fitness, travel, misc_pos, etc.)  
- **first** → First name of the cardholder  
- **last** → Last name of the cardholder  
- **gender** → Gender of the cardholder (M/F)  
- **amt** → Transaction amount (value spent)  
- **street** → Street address of the transaction location  
- **city** → City where the transaction occurred (200+ cities)  
- **state** → State where the transaction occurred  
- **zip** → Zip or pincode of the transaction region  
- **lat, long** → Latitude and longitude of the cardholder’s location  
- **city_pop** → Population of the city (e.g., 10,000; 23,000, etc.)  
- **job** → Occupation of the cardholder  
- **dob** → Date of birth of the cardholder  
- **trans_num** → Unique transaction number generated for each transaction  
- **merch_lat, merch_long** → Latitude and longitude of the merchant/business location  
- **is_fraud** → Target variable (0 = Legitimate, 1 = Fraudulent)  


## 🔎 Exploratory Data Analysis (EDA)  

A detailed exploratory data analysis (EDA) was performed to understand the dataset, remove irrelevant features, and identify patterns useful for fraud detection.  

### Feature-Wise Insights  

- **Unnamed: 0** → Contains 555,719 counts; only an index column, hence **dropped**.  
- **trans_date_trans_time** → Date & time of transaction; used for time-based analysis but not directly for modeling.  
- **cc_num** → Unique card number; not used in modeling but helpful for calculating **total number of transactions** and **transaction volume per card**.  
- **merchant** → Merchant names; removed due to high cardinality and irrelevance for modeling.  
- **category** → Transaction category (e.g., *personal_care, health_fitness, travel, misc_pos*).  
  - Categories were **grouped into 4–5 bins** based on fraud transaction counts and relevance.  
- **first, last** → First/last names of cardholders; **removed** as irrelevant.  
- **gender** → Gender distribution of transactions shows:  
  - Female: **54.86%**  
  - Male: **45.13%**  
  - Fraud rate varies slightly between genders, making it relevant for modeling.  
- **amt** → Transaction amount; critical for modeling since fraud may depend on transaction value (small or large).  
- **street** → Street address; **dropped** due to irrelevance.  
- **city, state** → Geographic information. Certain states show higher fraud rates. Example:  

| State | Total Txn | Fraud Txn | Fraud Rate |
|-------|-----------|-----------|------------|
| NY    | 35,918    | 175       | 0.49       |
| IN    | 11,959    | 75        | 0.63       |
| VA    | 12,506    | 75        | 0.60       |
| OR    | 7,811     | 48        | 0.61       |
| MS    | 8,833     | 54        | 0.61       |

- **zip** → High cardinality; not useful for modeling.  
- **lat, long** → Latitude & longitude of cardholder; potential for fraud hotspot analysis.  
- **city_pop** → Population of the cardholder’s city; can help detect fraud trends in **small vs. large cities**.  
- **job** → Occupation of the cardholder; may provide socioeconomic insight into fraud likelihood.  
- **dob** → Date of birth; used to derive **age feature**, which can influence fraud risk.  
- **trans_num** → Unique transaction ID; dropped from modeling.   


✅ After EDA, irrelevant columns (e.g., *Unnamed: 0, first, last, merchant, street, zip, trans_num etc) were removed, while meaningful features were **transformed or engineered** for modeling.  

  


---

