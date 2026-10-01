# 🛍️ Customer Behavior Analysis

An end-to-end **Customer Shopping Behavior Analysis** project using **Python, PostgreSQL, SQL, and Power BI** to analyze customer purchasing patterns, spending behavior, product preferences, subscriptions, discounts, shipping methods, and customer segments.

---

## 📌 Project Overview

Understanding customer behavior is essential for making data-driven decisions in e-commerce.

This project analyzes customer shopping data to answer important business questions such as:

- Which customer groups generate the most revenue?
- Do subscribed customers spend more than non-subscribers?
- Which products have the highest ratings?
- Which products are purchased most frequently?
- How frequently do customers make purchases?
- Which products have the highest discount usage?
- How can customers be segmented based on previous purchases?
- Which age groups contribute the most revenue?
- How does shipping method relate to customer spending?

The project follows a complete data analytics workflow:

```text
Raw Dataset
     ↓
Python & Pandas
     ↓
Data Cleaning & EDA
     ↓
Feature Engineering
     ↓
PostgreSQL
     ↓
SQL Business Analysis
     ↓
Power BI Dashboard
```

---

## 🎯 Objectives

The main objectives of this project are:

- Clean and preprocess the raw customer shopping dataset.
- Perform exploratory data analysis using Python.
- Handle missing values and inconsistent data.
- Create useful analytical features.
- Store the cleaned dataset in PostgreSQL.
- Perform business-oriented SQL analysis.
- Build an interactive Power BI dashboard.
- Generate meaningful insights into customer and product behavior.

---

## 🛠️ Technologies Used

| Technology | Purpose |
|---|---|
| 🐍 Python | Data analysis and preprocessing |
| 🐼 Pandas | Data manipulation |
| 📓 Jupyter Notebook | Exploratory Data Analysis |
| 🗄️ PostgreSQL | Database storage |
| 🔍 SQL | Business analysis |
| 🔗 SQLAlchemy | Python–PostgreSQL connection |
| 🐘 Psycopg2 | PostgreSQL connectivity |
| 📊 Power BI | Data visualization and dashboarding |

---

## 📂 Project Structure

```text
Customer_analysis/
│
├── Cleaning&EDA.ipynb
│   └── Data cleaning, preprocessing, EDA and feature engineering
│
├── customer_shopping_behavior.csv
│   └── Customer shopping dataset
│
├── customer_analysis_sql.sql
│   └── SQL business analysis queries
│
├── Customer_analysis.pbix
│   └── Power BI dashboard
│
├── Screenshot 2026-10-01 173831.png
│   └── Dashboard screenshot
│
└── README.md
    └── Project documentation
```

---

# 📊 Dataset

The project uses a customer shopping behavior dataset containing **3,900 customer purchase records** and **18 attributes**.

## Dataset Features

| Column | Description |
|---|---|
| `Customer ID` | Unique customer identifier |
| `Age` | Customer age |
| `Gender` | Customer gender |
| `Item Purchased` | Product purchased |
| `Category` | Product category |
| `Purchase Amount (USD)` | Purchase amount |
| `Location` | Customer location |
| `Size` | Product size |
| `Color` | Product color |
| `Season` | Season of purchase |
| `Review Rating` | Customer review rating |
| `Subscription Status` | Subscription status |
| `Shipping Type` | Shipping method |
| `Discount Applied` | Whether discount was applied |
| `Promo Code Used` | Whether promo code was used |
| `Previous Purchases` | Number of previous purchases |
| `Payment Method` | Payment method |
| `Frequency of Purchases` | Purchase frequency |

---

# 🧹 Data Cleaning & Preprocessing

The `Cleaning&EDA.ipynb` notebook performs multiple data preprocessing steps.

## 1. Data Loading

The dataset is loaded using Pandas:

```python
import pandas as pd

df = pd.read_csv("customer_shopping_behavior.csv")
```

---

## 2. Data Exploration

The dataset is explored using:

- Dataset dimensions
- Data types
- Summary statistics
- Missing value analysis
- Numerical distributions
- Categorical variables

The dataset contains:

- **3,900 rows**
- **18 columns**

---

## 3. Missing Value Treatment

The `Review Rating` column contains missing values.

Instead of removing those records, missing ratings are replaced using the **median review rating of the corresponding product category**.

```python
medians = df.groupby("Category")["Review Rating"].median()

df["Review Rating"] = df["Review Rating"].fillna(
    df["Category"].map(medians)
)
```

This approach preserves the available customer records while using category-specific information for imputation.

---

## 4. Column Name Standardization

Column names are converted into cleaner formats for easier use in Python and SQL.

For example:

```text
Customer ID
     ↓
customer_id
```

```text
Purchase Amount (USD)
     ↓
purchase_amount
```

---

## 5. Age Group Creation

Customers are grouped into different age categories:

| Age | Age Group |
|---|---|
| 0–30 | Young Adult |
| 31–40 | Adult |
| 41–50 | Middle Aged |
| 51+ | Senior |

This allows customer behavior and revenue to be analyzed across different age groups.

---

## 6. Purchase Frequency Transformation

Purchase frequency is converted into approximate days.

| Frequency | Days |
|---|---:|
| Weekly | 7 |
| Fortnightly | 14 |
| Bi-Weekly | 14 |
| Monthly | 30 |
| Quarterly | 90 |
| Every 3 Months | 90 |
| Annually | 365 |

A new feature is created:

```text
purchase_frequency_days
```

This feature allows purchase frequency to be analyzed quantitatively.

---

# 🗄️ PostgreSQL Integration

After cleaning and feature engineering, the dataset is loaded into PostgreSQL.

The project uses:

- PostgreSQL
- SQLAlchemy
- Psycopg2

The cleaned data is stored in a table named:

```text
customer
```

## Database Workflow

```text
CSV Dataset
     │
     ▼
Python / Pandas
     │
     ├── Data Cleaning
     ├── Missing Value Treatment
     ├── Feature Engineering
     └── Data Preparation
     │
     ▼
PostgreSQL
     │
     ▼
SQL Business Analysis
     │
     ▼
Power BI Dashboard
```

---

# 🔍 SQL Analysis

The `customer_analysis_sql.sql` file contains business-oriented SQL queries for analyzing customer and purchasing behavior.

## 1. Revenue by Gender

Calculates total revenue generated by each gender.

```sql
SELECT 
    gender,
    SUM(purchase_amount) AS revenue
FROM customer
GROUP BY gender;
```

---

## 2. Discounted Purchases Above Average

Identifies customers who received discounts while spending at least the average purchase amount.

---

## 3. Highest-Rated Products

Identifies products with the highest average review ratings.

---

## 4. Shipping Analysis

Compares average purchase amounts between Standard and Express shipping customers.

---

## 5. Subscriber vs Non-Subscriber Analysis

Compares:

- Customer count
- Average purchase amount
- Total revenue

between subscribers and non-subscribers.

---

## 6. Discount Usage

Calculates the percentage of purchases where discounts were applied for each product.

---

## 7. Customer Segmentation

Customers are segmented according to their previous purchases:

```text
1 Previous Purchase
        ↓
      New

2–10 Previous Purchases
        ↓
    Returning

More than 10 Previous Purchases
        ↓
      Loyal
```

This provides a simple behavioral segmentation framework.

---

## 8. Top Products by Category

Uses SQL window functions to identify the top products within each category.

---

## 9. Repeat Buyers & Subscription

Analyzes subscription behavior among customers with multiple previous purchases.

---

## 10. Revenue by Age Group

Calculates total revenue generated by different age groups.

---

# 📈 Power BI Dashboard

The project includes a Power BI dashboard:

```text
Customer_analysis.pbix
```

The dashboard provides an interactive view of customer and purchasing behavior.

## Dashboard Analysis

The dashboard can be used to explore:

- Customer demographics
- Revenue
- Product performance
- Customer segments
- Subscription status
- Discount usage
- Shipping methods
- Purchase frequency
- Age-group revenue
- Customer purchasing behavior

---

# 📊 Dashboard Preview

![Customer Shopping Behavior Dashboard](Screenshot%202026-10-01%20173831.png)

---

# 💡 Business Value

This project provides a framework for understanding customer behavior and supporting data-driven business decisions.

## 🎯 Customer Segmentation

Customers can be classified as **New, Returning, or Loyal** based on their previous purchase history.

## 💰 Revenue Analysis

Revenue can be compared across:

- Gender
- Age groups
- Subscription status
- Products
- Categories

## 🛒 Product Strategy

Product ratings, purchase frequency, categories, and discount usage can help identify product-level trends.

## 📣 Marketing Analysis

Discounts, promotional codes, subscriptions, and purchase frequency can be analyzed to understand customer engagement.

## 🚚 Shipping Analysis

Purchase behavior can be compared across different shipping methods to understand spending patterns.

---

# 🚀 How to Run the Project

## 1. Clone the Repository

```bash
git clone https://github.com/aniketaayush29/Customer_analysis.git

cd Customer_analysis
```

---

## 2. Install Dependencies

```bash
pip install pandas sqlalchemy psycopg2-binary jupyter
```

---

## 3. Run Jupyter Notebook

Start Jupyter Notebook:

```bash
jupyter notebook
```

Open:

```text
Cleaning&EDA.ipynb
```

Make sure the dataset is available in the same directory:

```text
customer_shopping_behavior.csv
```

---

## 4. Configure PostgreSQL

Create a PostgreSQL database:

```text
customer_analysis
```

Configure your own PostgreSQL connection details in the notebook.

> ⚠️ **Important:** Never commit real database passwords or credentials to GitHub. Use environment variables or a `.env` file instead.

---

## 5. Load Data into PostgreSQL

Run the PostgreSQL-loading section of the notebook.

The cleaned dataset will be stored in:

```text
customer
```

---

## 6. Run SQL Analysis

Open:

```text
customer_analysis_sql.sql
```

Execute the queries using PostgreSQL.

---

## 7. Open the Power BI Dashboard

Open:

```text
Customer_analysis.pbix
```

using **Microsoft Power BI Desktop**.

Configure the PostgreSQL connection if required.

---

# 📊 Project Workflow

```text
                  CUSTOMER SHOPPING DATA
                           │
                           ▼
                ┌─────────────────────┐
                │     Python / EDA    │
                │                     │
                │ • Data Inspection   │
                │ • Missing Values    │
                │ • Data Cleaning     │
                │ • Feature Creation  │
                └──────────┬──────────┘
                           │
                           ▼
                   CLEANED DATASET
                           │
                           ▼
                ┌─────────────────────┐
                │     PostgreSQL      │
                │                     │
                │   customer table    │
                └──────────┬──────────┘
                           │
                           ▼
                ┌─────────────────────┐
                │     SQL Analysis    │
                │                     │
                │ • Revenue           │
                │ • Products          │
                │ • Customers         │
                │ • Subscriptions     │
                │ • Segmentation      │
                └──────────┬──────────┘
                           │
                           ▼
                ┌─────────────────────┐
                │      Power BI       │
                │                     │
                │ • KPIs              │
                │ • Charts            │
                │ • Customer Insights │
                │ • Interactive Report│
                └─────────────────────┘
```

---

# 🧠 Skills Demonstrated

## Python & Data Analysis

- Python
- Pandas
- Data Cleaning
- Exploratory Data Analysis
- Missing Value Treatment
- Feature Engineering
- Data Transformation
- Data Profiling

## SQL

- `SELECT`
- `WHERE`
- `GROUP BY`
- `CASE`
- Aggregations
- Subqueries
- Common Table Expressions
- Window Functions
- `ROW_NUMBER()`
- `PARTITION BY`
- Conditional Aggregation
- Percentage Calculations
- Customer Segmentation

## Database

- PostgreSQL
- SQLAlchemy
- Psycopg2
- Relational Database Management
- Data Loading

## Power BI

- Dashboard Development
- Data Visualization
- KPI Analysis
- Business Intelligence
- Customer Analytics
- Interactive Reporting

---

# 📁 Important Files

| File | Description |
|---|---|
| `Cleaning&EDA.ipynb` | Data cleaning, EDA, preprocessing and feature engineering |
| `customer_shopping_behavior.csv` | Customer shopping dataset |
| `customer_analysis_sql.sql` | SQL business analysis queries |
| `Customer_analysis.pbix` | Power BI dashboard |
| `Screenshot 2026-10-01 173831.png` | Dashboard screenshot |
| `README.md` | Project documentation |

---

# 🔮 Future Improvements

- [ ] Add RFM (Recency, Frequency, Monetary) customer segmentation
- [ ] Add Customer Lifetime Value analysis
- [ ] Add customer churn and retention analysis
- [ ] Build an automated ETL pipeline
- [ ] Add time-based sales analysis
- [ ] Add automated data quality checks
- [ ] Add `requirements.txt`
- [ ] Add `.env.example` for database configuration
- [ ] Add automated tests
- [ ] Improve Power BI dashboard with additional KPIs and filters

---

# ⚠️ Notes

The dataset contains customer shopping information used for analytical purposes.

The analysis should be interpreted within the context and limitations of the available dataset.

If you reproduce this project, replace the PostgreSQL connection details with your own credentials.

---

# 👨‍💻 Author

**Aniket Aayush**

GitHub: [@aniketaayush29](https://github.com/aniketaayush29)

---

# ⭐ Support

If you found this project useful, consider giving the repository a ⭐ star!

Feel free to explore the Python notebook, SQL analysis, and Power BI dashboard to learn more about customer analytics and business intelligence.
