# Predicting Hotel Booking Cancellations: A LASSO Regression Approach

## 📌 Executive Summary
In the hospitality industry, high cancellation rates significantly disrupt revenue forecasting, inventory management, and dynamic pricing models. Accurately predicting which bookings are at risk of cancellation allows businesses to implement targeted retention strategies, adjust overbooking thresholds, and optimize room allocation.

This project builds a predictive machine learning pipeline to classify hotel bookings as likely to cancel or fulfill. By employing **Logistic Regression** and **LASSO (L1-Regularization)**, the model not only predicts outcomes but also performs automatic feature selection to identify the primary drivers behind guest cancellations.

## 🎯 The Business Problem
Hotel reservations are highly volatile. When a guest cancels late or no-shows, the hotel loses perishable inventory (a room-night) that cannot be resold. 
* **The Goal:** Develop a predictive model to identify high-risk bookings prior to the cancellation window.
* **The Value:** Enable proactive interventions (e.g., non-refundable upgrade offers, targeted email campaigns) and improve the accuracy of the hotel's revenue pipeline.

## 🛠️ Methodology & Approach
This project follows a complete end-to-end data science lifecycle, emphasizing robust data preprocessing and iterative model evaluation.

### 1. Exploratory Data Analysis (EDA) & Preprocessing
* **Data Cleaning:** Handled missing values, dropped irrelevant identifiers, and normalized numeric fields.
* **Categorical Encoding:** Applied One-Hot Encoding to transform categorical variables (e.g., room type, market segment) into machine-readable formats.
* **Feature Scaling:** Utilized `StandardScaler` to ensure continuous variables were on a uniform scale, a critical prerequisite for distance-based regularization techniques like LASSO.

### 2. Feature Engineering
* Introduced domain-specific, non-linear features to capture complex guest behaviors that standard linear models might miss.
* Analyzed correlation matrices to identify multicollinearity and drop redundant variables prior to modeling.

### 3. Model Architecture & Selection
I trained, evaluated, and compared four distinct classification models using **K-Fold Cross-Validation** to ensure generalizability and prevent overfitting:
1. **Baseline Logistic Regression:** To establish a performance benchmark.
2. **LASSO Logistic Regression (L1 Penalty):** To perform continuous shrinkage and automatic feature selection, dropping non-impactful variables to zero.
3. **Logistic Regression with Engineered Features:** Testing the hypothesis that derived features improve classification accuracy.
4. **LASSO + Engineered Features:** The final combined approach.

*Additionally, I performed explicit Forward and Backward Feature Selection wrappers to validate the features chosen by the LASSO penalty.*

## 📊 Results & Evaluation Metrics
The models were evaluated strictly on their ability to minimize false negatives (missing a cancellation) and false positives (annoying a loyal guest). Metrics tracked include:
* **Accuracy & F1-Score:** To measure overall model balance.
* **Precision:** To ensure interventions are targeted efficiently.
* **Confusion Matrices:** Plotted to visually interpret the exact breakdown of Type I and Type II errors.

*(Note: See the Jupyter Notebook for the exact output charts and final comparison tables).*

## 💻 Tech Stack
* **Language:** Python
* **Data Manipulation:** `pandas`, `numpy`
* **Machine Learning:** `scikit-learn` (LogisticRegression, KFold, StandardScaler, Feature Selection)
* **Data Visualization:** `matplotlib`, `seaborn`
* **Data Source:** [Kaggle Dataset API]

## 🚀 How to Run the Project
1. Clone this repository to your local machine.
2. Ensure the required Python libraries are installed:
   ```bash
   pip install pandas numpy scikit-learn matplotlib seaborn
