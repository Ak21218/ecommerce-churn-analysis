# E-commerce Customer Churn Analysis

This project analyzes a small e-commerce dataset to understand the factors contributing to customer churn. It includes an exploratory data analysis (EDA) to find patterns in user behavior and a predictive model (Logistic Regression) built to identify customers at high risk of churning.

## Project Overview

The primary goal is to analyze user engagement, support interactions, and purchase history to build a model that can predict whether a customer will churn.

The analysis in `notebook.ipynb` covers:

1.  **Data Loading & Cleaning:** Importing the dataset and converting categorical 'Yes'/'No' fields to numerical (0/1) values.
2.  **Exploratory Data Analysis (EDA):** Visualizing the data to answer key questions:
      * What is the overall churn rate?
      * Do users who file support tickets churn more?
      * Is there a "danger zone" for `TimeOnSite`?
3.  **Predictive Modeling:** Building a `scikit-learn` `Pipeline` to scale features and train a Logistic Regression classifier.
4.  **Evaluation:** Assessing the model's performance on a held-out test set.

## Dataset

The model is trained on the `ecommerce_churn[1].xlsx` dataset.

**Note:** The dataset is not included in this repository. You must provide this file in the project's root directory to run the notebook.

### Features

  * `VisitsLast30Days`: Number of visits in the last 30 days.
  * `TimeOnSite`: Total time spent on the site.
  * `PurchaseCount`: Number of purchases made.
  * `HasSupportTicket`: (Yes/No) Whether the user has filed a support ticket.

### Target Variable

  * `Churned`: (Yes/No) Whether the user has churned.

## Exploratory Data Analysis (EDA)

The notebook contains several visualizations to understand the drivers of churn:

1.  **Churn Distribution:** A countplot showing the total number of churned vs. non-churned users.
2.  **Churn by Support Ticket:** This plot compares the churn rate for users who have filed a support ticket against those who have not.
3.  **Time on Site vs. Churn:** A histogram that explores the relationship between the time a user spends on the site and their likelihood of churning.

## Modeling & Results

A Logistic Regression model was used for classification. All features were scaled using `StandardScaler` as part of a `scikit-learn` `Pipeline`.

### Model Performance

The model's performance on the test set (`test_size=0.2`, `random_state=42`) was poor, achieving an accuracy of only **40%**.

The detailed classification report shows the model's key weakness:

```
Classification Report:
                 precision    recall  f1-score   support

Not Churned (0)       0.40      1.00      0.57         4
    Churned (1)       0.00      0.00      0.00         6

       accuracy                           0.40        10
      macro avg       0.20      0.50      0.29        10
   weighted avg       0.16      0.40      0.23        10
```

### Analysis of Results

As the report indicates, the model has **0.00 precision and recall** for the "Churned (1)" class. This means it fails to identify *any* of the churned customers in the test set and simply predicts "Not Churned (0)" for every user.

This poor performance is likely due to:

  * **A very small dataset**, which makes it difficult to find a generalizable pattern.
  * **Significant class imbalance** (which can be seen in the EDA plots).
  * **Features that are not strongly predictive** of churn.

Further steps would involve gathering more data, feature engineering, and experimenting with different models or techniques to handle class imbalance (e.g., SMOTE).

## How to Run

1.  **Clone the repository:**

    ```bash
    git clone https://github.com/Ak21218/your-repository-name.git
    cd ecommerce-churn-analysis
    ```

2.  **Install dependencies:**
    It is recommended to use a virtual environment.

    ```bash
    pip install -r requirements.txt
    ```

3.  **Add the dataset:**
    Place your `ecommerce_churn[1].xlsx` file in the root of the project directory.

4.  **Launch Jupyter:**

    ```bash
    jupyter notebook
    ```

5.  Open and run the `notebook.ipynb` file.

## Requirements

You can create a `requirements.txt` file with the following content:

```
pandas
scikit-learn
seaborn
matplotlib
openpyxl  # Required by pandas for reading .xlsx files
```