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

  ## 🔧 Feature Engineering for Credit Card Fraud Detection

---

## 📌 1. Dropped / Irrelevant Columns
The following columns were removed as they don’t contribute directly to modeling:
- `Unnamed: 0` → index column  
- `cc_num` → card number (used only for aggregation, not modeling)  
- `merchant` → merchant name (irrelevant for fraud prediction)  
- `street`, `zip`, `city` → highly granular, less predictive  
- `first`, `last` → irrelevant personal identifiers  
- `trans_num` → unique transaction ID  

---

## 📌 2. Feature Engineering Steps

### 🗓️ 2.1 Date of Birth → Age
- Converted `dob` into `age`.  
- Created **age bins**:  
  - `0–18`, `19–30`, `31–45`, `46–60`, `61–75`, `76+`  
- Applied **One-Hot Encoding (OHE)** to bins.  
- Dropped original `dob` column.  

---

### 🚻 2.2 Gender
- Encoded gender (`M`, `F`) using **OHE**.  

---

### 🛒 2.3 Transaction Category
- Original categories (14 unique) grouped into **4 broader classes**:  

| Original Categories | Grouped Category |
|---------------------|------------------|
| `grocery_pos`, `grocery_net`, `gas_transport`, `home` | Essentials |
| `personal_care`, `health_fitness`, `kids_pets` | Lifestyle & Wellbeing |
| `entertainment`, `food_dining`, `travel` | Discretionary |
| `shopping_pos`, `shopping_net`, `misc_pos`, `misc_net` | Shopping & Misc |

- Applied **OHE** on grouped categories.  

---

### 🌍 2.4 Location Features
- Applied **reverse geocoding** on (`lat`, `long`) → extracted **State, City, Country**.  
- Dropped `City` and `Country`.  
- Engineered **State → Region mapping**:

| Region     | Example States |
|------------|----------------|
| Western    | California, Oregon, Washington, Nevada, Arizona |
| Northern   | Minnesota, Iowa, Illinois, Michigan, Ohio |
| Southern   | Texas, Florida, Georgia, Virginia, Alabama |
| Eastern    | New York, New Jersey, Pennsylvania, Massachusetts |

- Applied **OHE** on `Region`.  

---

### 🏙️ 2.5 City Population
- Population (`city_pop`) was highly skewed.  
- Created **population bins**:  
  - `Micro Town` → 0–25,000  
  - `Small Town` → 25,001–50,000  
  - `Mid City` → 50,001–100,000  
  - `Large City` → 100,001–200,000  
  - `Metro City` → 200,001+  

- Example fraud distribution by city category:  

| City Category | Total Txn | Fraud Txn | Fraud Rate |
|---------------|-----------|-----------|------------|
| Micro Town    | 426,735   | 1,757     | ~0%        |
| Small Town    | 25,467    | 44        | ~0%        |
| Mid City      | 27,601    | 136       | ~0%        |
| Large City    | 24,501    | 46        | ~0%        |
| Metro City    | 51,415    | 162       | ~0%        |

- Applied **OHE** on city categories.  

---

### 💳 2.6 Transaction Amount
- Retained `amt` (transaction amount) as-is.  
- Hypothesis: Fraud may occur more often at **smaller amounts** (to avoid detection) or at **sudden high-value transactions**.  

---

### 🕒 2.7 Transaction Time
- From `trans_date_trans_time`, derived additional temporal features:  
  - `hour` of transaction  
  - `day_of_week`  
  - `month`  
- Useful to capture fraud trends (e.g., late-night or weekend fraud).  

---

## ✅ Final Engineered Feature Set
1. **Demographics**  
   - `age_bin` (OHE)  
   - `gender` (OHE)  

2. **Transaction Info**  
   - `amt`  
   - `category_grouped` (OHE)  
   - `trans_time_features` (`hour`, `day_of_week`, `month`)  

3. **Geographic Info**  
   - `region` (OHE)  
   - `city_category` (OHE)  

---
# 🎯 Feature Selection  

After feature engineering, the dataset contained a large number of variables (including multiple one-hot encoded columns). To improve model performance, reduce noise, and avoid overfitting, **feature selection** techniques were applied.  

---

## 📌 Weight of Evidence (WOE)

The **Weight of Evidence (WOE)** is used to measure how well an independent variable separates the binary target classes (e.g., fraud vs. non-fraud).  
It transforms categorical or continuous predictors into a scale that reflects their predictive power.  

**Interpretation:**
- WOE > 0 → Higher likelihood of being a non-event (e.g., non-fraud).  
- WOE < 0 → Higher likelihood of being an event (e.g., fraud).  
- WOE = 0 → No predictive power.  

**Formula:**  

`WOE = ln( (% of non-events) / (% of events) )`  


---

## 📌 Information Value (IV)

The **Information Value (IV)** quantifies the predictive strength of a variable in relation to the target.  
It is derived from the distribution differences between events and non-events.  

**Interpretation (commonly used thresholds):**
- IV < 0.02 → Not predictive  
- 0.02 ≤ IV < 0.1 → Weak predictor  
- 0.1 ≤ IV < 0.3 → Medium predictor  
- 0.3 ≤ IV < 0.5 → Strong predictor  
- IV ≥ 0.5 → Suspiciously powerful (possible data leakage)  

**Formula:**  

`IV = Σ [ ( % of non-events - % of events ) * WOE ]`  


---

## 📊 IV Values of Features  
The following table summarizes the **calculated IV values** (from Excel results):  

| Feature                              | IV Value       |
|--------------------------------------|----------------|
| amt                                  | 3.8378         |
| category_bin_Shopping & Misc         | 0.2049         |
| category_bin_Lifestyle & Wellbeing   | 0.1531         |
| city_category_Small Town             | 0.0211         |
| city_category_Micro Town             | 0.0162         |
| age_group_61-75                      | 0.0093         |
| age_group_76+                        | 0.0058         |
| age_group_46-60                      | 0.0054         |
| city_category_Metro City             | 0.0038         |
| city_category_Mid City               | 0.0036         |
| category_bin_Essentials              | 0.0024         |
| region_Northern                      | 0.0017         |
| region_Southern                      | 0.0015         |
| age_group_31-45                      | 0.0015         |
| gender_M                             | 0.0001         |
| region_Western                       | 0.00006        |

---

## ⚖️ Feature Selection Approaches  

### ✅ Approach 1: High-IV Features Only  
- Use only features with **high IV values** (e.g., `amt`, `category_bin_Shopping & Misc`, `category_bin_Lifestyle & Wellbeing`).  
- Pros: Reduces dimensionality, highlights the strongest predictors.  
- Cons: Risk of oversimplifying → potential **overfitting** since multivariate effects are ignored.  

### ✅ Approach 2: Keep All Features  
- Use all engineered features, even those with **low IV values**, since in multivariate analysis their **combinations** can still contribute to detecting fraud.  
- Pros: Richer feature space for models like Random Forest, XGBoost.  
- Cons: Higher complexity, potential noise introduction.  

---

## 🎯 Final Choice  
We proceeded with **Approach 2 (All Engineered Features)** since fraud detection is often driven by **combinations of variables** rather than single predictors.  

Even though some features have low IV values, they may still provide **useful multivariate interactions** (e.g., transaction amount × region, age group × category).  
Tree-based models like **Random Forest** and **XGBoost** can effectively capture these relationships.  

📌 This approach ensures that the model has a **richer feature space** and can make more accurate splits, leading to better fraud detection performance in practice.

---

## ⚖️ Handling Imbalanced Data  

Our dataset is highly imbalanced:  
- **Class 0 (Non-Fraud):** 553,574 (~99.62%)  
- **Class 1 (Fraud):** 2,145 (~0.38%)  
- **Total:** 555,719 rows  

This imbalance can cause issues like:  
- Model bias toward the majority class  
- Unreliable evaluation metrics  

To address this, we applied **sampling and weighting techniques**:



### 🔹 1. SMOTE (Synthetic Minority Oversampling Technique)  
- Creates **synthetic samples** for the minority class (instead of just duplicating).  
- ✅ Pros: Better class balance, reduced bias, prevents overfitting.  
- ❌ Cons: Computationally heavy, may amplify noise, struggles with categorical/high-dimensional data.  



### 🔹 2. ADASYN (Adaptive Synthetic Sampling)  
- Extension of SMOTE that generates **more synthetic samples** for “hard-to-learn” cases (low density or near decision boundary).  
- ✅ Pros: Focuses on difficult examples, improves discrimination between classes.  
- ❌ Cons: More complex, sensitive to noise, risk of overfitting.  



### 🔹 3. Cost-Sensitive Learning  
- Modifies the **loss function** by assigning **higher weights** to the minority class and lower weights to the majority class.  
- ✅ Pros: Better performance on imbalanced data, useful in high-stakes domains (finance, healthcare).  
- ❌ Cons: Requires domain knowledge to set costs, adds complexity, can be computationally intensive.  



---

## 🤖 Model Training  

We experimented with multiple models to detect credit card fraud:  
- **Decision Tree**  
- **Random Forest**  
- **XGBoost**  
- **LightGBM**  

### 🔧 Training Approach  
- Built **baseline models** for comparison.  
- Applied **hyperparameter tuning** using **GridSearchCV**.  
- Incorporated **sampling techniques**:  
  - **SMOTE (oversampling)**  
  - **Cost-Sensitive Learning (class weighting)**  

---

### 🏆 Best Model  
The best results were obtained using a **combination of Cost-Sensitive Learning + XGBoost**.  

**Performance Metrics:**  
- ✅ **Accuracy:** 0.96  
- ✅ **Macro Avg Recall:** 0.93
- ✅ **AUC Score:** 0.98  
- ✅ **KS Metric Difference (Train vs Test):** 3.58  

**Fraud Detection Results:**  
- Detected **579 fraud transactions** out of **644** in test data.  
- Successfully detected **159,000+ legitimate transactions** out of **166,000+** in test data.  

📌 This combination offered the **best balance of accuracy, recall, and generalization**.  


