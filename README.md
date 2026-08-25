# Customer Churn Analysis

## Project Overview

This project focuses on analyzing customer churn using customer, subscription, and customer-support data stored in a SQLite database.

The objective is to identify patterns and factors associated with customer churn, evaluate customer retention, measure revenue exposure, and segment customers based on their churn risk.

The analysis was performed using Python, Pandas, SQL/SQLite, Matplotlib, and Seaborn within a Jupyter Notebook.

---

## Business Objective

Customer churn is an important business metric because the loss of existing customers can directly impact recurring revenue and customer lifetime value.

This analysis aims to answer key business questions such as:

* What is the overall customer churn rate?
* Which customer plans have the highest churn?
* How does churn vary across subscription types and locations?
* What is the average revenue per user?
* How much revenue is potentially at risk due to churn?
* What is the average customer tenure?
* How are customers distributed across different churn-risk categories?
* Is there a relationship between customer support activity and churn?

---

## Dataset

The analysis uses the following SQLite database:

`customer_churn.db`

The database contains three primary tables.

### Customer Table — `db_customer`

Contains customer demographic and profile information.

| Column       | Description                |
| ------------ | -------------------------- |
| `customerid` | Unique customer identifier |
| `name`       | Customer name              |
| `country`    | Customer country           |
| `state`      | Customer state             |
| `gender`     | Customer gender            |
| `dob`        | Customer date of birth     |
| `interests`  | Customer interests         |
| `pincode`    | Customer postal code       |

### Subscription Table — `db_subscription`

Contains customer subscription, contract, cancellation, and revenue information.

| Column                    | Description                          |
| ------------------------- | ------------------------------------ |
| `customerid`              | Unique customer identifier           |
| `subscription_start_date` | Subscription start date              |
| `subscription_type`       | Subscription acquisition/source type |
| `renewal_date`            | Subscription renewal date            |
| `plan_type`               | Customer plan                        |
| `contract_type`           | Contract type                        |
| `cancellation_date`       | Cancellation date                    |
| `cancellation_reason`     | Reason for cancellation              |
| `monthly_charges`         | Monthly customer charges             |
| `cltv`                    | Customer lifetime value              |
| `churn_score`             | Existing customer churn score        |

### Support Table — `db_support`

Contains customer-support and satisfaction information.

| Column           | Description                 |
| ---------------- | --------------------------- |
| `customerid`     | Customer identifier         |
| `complaint_date` | Complaint date              |
| `escalations`    | Escalation information      |
| `csat_score`     | Customer satisfaction score |
| `comment`        | Customer-support comment    |

---

## Data Preparation

The following preprocessing steps were performed as part of the analysis:

* Renamed the customer `name` column to `customer_name`.
* Removed unused customer attributes.
* Converted date columns into appropriate datetime formats.
* Standardized gender values.
* Filled missing country information using state-country mapping.
* Processed subscription start, renewal, and cancellation dates.
* Processed customer-support complaint dates.
* Created a complaint count for customers.
* Removed duplicate support records while retaining the latest complaint information.
* Joined customer, subscription, and support data using `customerid`.

The resulting dataset was used for the subsequent churn analysis.

---

## Feature Engineering

### Churn Flag

A binary churn indicator was created using the cancellation date.

* `1` — Customer has a cancellation date
* `0` — Customer is active

### Customer Tenure

Customer tenure was calculated based on the subscription start date and the applicable end date.

### Churn Risk

Customers were segmented using the existing `churn_score`.

|  Churn Score | Risk Category |
| -----------: | ------------- |
| Less than 50 | Low           |
|        50–69 | Medium        |
|  70 or above | High          |

---

## Key Performance Indicators

The analysis calculates the following customer and churn metrics:

| Metric                          |     Result |
| ------------------------------- | ---------: |
| Churn Rate                      |     28.57% |
| Retention Rate                  |     71.43% |
| Average Revenue Per User (ARPU) |      18.85 |
| Average Customer Tenure         | 1,522 days |
| Revenue at Risk                 |      73.94 |
| Escalation Rate                 |     19.05% |
| Average Complaints per User     |       0.43 |

---

## Churn Analysis

### Churn by Plan Type

The analysis indicates a significant difference in churn across customer plans.

| Plan Type | Churn Rate |
| --------- | ---------: |
| Basic     |     60.00% |
| Standard  |     22.22% |
| Premium   |     14.29% |

The Basic plan has the highest observed churn rate, while the Premium plan has the lowest.

This suggests that plan-level customer behavior may be an important area for further retention analysis.

### Churn by Subscription Type

| Subscription Type | Churn Rate |
| ----------------- | ---------: |
| Organic           |      0.00% |
| Paid              |     16.67% |
| Refferal          |     83.33% |

The referral segment has the highest observed churn rate in the dataset.

Because the dataset contains a limited number of customers, these segment-level percentages should be interpreted as exploratory findings rather than statistically representative results.

### Churn by State

The analysis also evaluates churn across geographic locations.

| State         | Churn Rate |
| ------------- | ---------: |
| Karnataka     |    100.00% |
| Meghalaya     |     66.67% |
| Telangana     |     50.00% |
| Delhi         |     25.00% |
| Kathmandu     |      0.00% |
| Maharashtra   |      0.00% |
| Nagaland      |      0.00% |
| Rajasthan     |      0.00% |
| Uttar Pradesh |      0.00% |

State-level results should be interpreted carefully because some locations contain relatively few customers.

---

## Churn Risk Distribution

Customers were categorized according to their existing churn scores.

| Risk Category | Number of Customers |
| ------------- | ------------------: |
| Low           |                  13 |
| Medium        |                   2 |
| High          |                   6 |

The risk segmentation can be used as a starting point for identifying customers who may require targeted retention strategies.

---

## Visual Analysis

The notebook contains several visualizations to support the analysis, including:

* Monthly churn trends
* Churn rate by plan type
* Churn rate by state
* Churn-risk distribution
* Correlation analysis
* Customer and subscription-related comparisons

These visualizations help identify patterns that may not be immediately apparent from aggregated metrics.

---

## Technology Stack

The project was developed using the following technologies:

* **Python**
* **Pandas**
* **NumPy**
* **Matplotlib**
* **Seaborn**
* **SQLite**
* **Jupyter Notebook**

---

## Project Structure

```text
customer-churn-analysis/
│
├── churn_analysis.ipynb
├── customer_churn.db
├── exported_chrun_data.csv
└── README.md
```

### File Description

**`churn_analysis.ipynb`**
Jupyter Notebook containing the complete data preparation, analysis, feature engineering, KPI calculations, and visualizations.

**`customer_churn.db`**
SQLite database containing the customer, subscription, and support datasets.

**`exported_chrun_data.csv`**
Processed dataset generated during the analysis.

**`README.md`**
Documentation describing the project, methodology, findings, and results.

---

## How to Run the Project

### 1. Clone the Repository

```bash
git clone https://github.com/<your-username>/<repository-name>.git
cd <repository-name>
```

### 2. Install Dependencies

```bash
pip install pandas numpy matplotlib seaborn jupyter
```

SQLite is accessed using Python's built-in `sqlite3` library.

### 3. Launch Jupyter Notebook

```bash
jupyter notebook
```

Open:

```text
churn_analysis.ipynb
```

### 4. Run the Notebook

Execute the notebook cells sequentially to reproduce the data preparation, analysis, KPI calculations, and visualizations.

---

## Key Business Insights

The analysis provides several notable observations:

1. The overall churn rate is **28.57%**, indicating that a significant portion of the customer base has churned.

2. The **Basic plan has the highest churn rate at 60%**, compared with 22.22% for Standard and 14.29% for Premium.

3. The observed churn rate for the **referral subscription segment is 83.33%**, making it an area that may require additional investigation.

4. The analysis estimates **73.94 in revenue at risk** from churned customers.

5. **Six customers** are classified as high-risk based on the available churn score.

6. Customer-support activity was incorporated into the analysis through complaint and escalation metrics.

---

## Limitations

This analysis should be considered an exploratory customer churn analysis because of the limited dataset size.

Key limitations include:

* The dataset contains a relatively small number of customers.
* Segment-level churn rates can be strongly influenced by small sample sizes.
* Correlation does not imply causation.
* The analysis uses an existing churn score rather than developing a new predictive model.
* The results may not generalize to a larger customer population.

---

## Future Scope

The project can be extended in several ways:

* Develop a machine-learning model for churn prediction.
* Perform feature importance analysis.
* Analyze the relationship between customer satisfaction and churn.
* Analyze cancellation reasons and their relationship with customer characteristics.
* Perform customer cohort and retention analysis.
* Build an interactive dashboard using Power BI, Tableau, or Streamlit.
* Develop customer-level retention recommendations.
* Apply statistical testing to validate differences between customer segments.
* Evaluate different machine-learning algorithms such as Logistic Regression, Decision Trees, Random Forest, and Gradient Boosting.

---

## Conclusion

This project demonstrates an end-to-end customer churn analysis workflow, beginning with data extraction from SQLite and progressing through data cleaning, transformation, feature engineering, exploratory analysis, KPI calculation, customer segmentation, and visualization.

The analysis identifies meaningful differences in churn across customer plans and subscription segments and provides a foundation for developing more advanced churn prediction and customer-retention strategies.

