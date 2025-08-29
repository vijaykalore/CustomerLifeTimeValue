# Customer Segmentation and Lifetime Value Prediction for Brazilian E-Commerce

This project performs an in-depth analysis of the Olist E-commerce dataset to understand customer behavior. The primary goals are to segment customers based on their purchasing habits using RFM analysis and to predict their future value to the company using probabilistic models.

## Table of Contents
- [Project Overview](#project-overview)
- [Dataset](#dataset)
- [Analysis Pipeline](#analysis-pipeline)
- [Key Findings & Visualizations](#key-findings--visualizations)
- [Models Used](#models-used)
- [How to Run This Project](#how-to-run-this-project)
- [Dependencies](#dependencies)

## Project Overview

In the competitive world of e-commerce, understanding your customers is key. Not all customers are equal; some purchase frequently, some spend a lot, and some have likely churned. This project aims to move beyond simple sales metrics and uncover deeper insights by:

1.  **Performing Exploratory Data Analysis (EDA)** to understand sales trends, customer acquisition, and retention over time.
2.  **Implementing RFM (Recency, Frequency, Monetary) Segmentation** to group customers into distinct categories based on their transaction history.
3.  **Predicting Customer Lifetime Value (CLV)** using the `lifetimes` library, which employs probabilistic models to forecast future customer activity and spending.
4.  **Creating a final, CLV-based segmentation** to identify the most valuable customer groups for targeted marketing and retention efforts.

## Dataset

This analysis uses the publicly available **Brazilian E-Commerce Public Dataset by Olist**, which can be found on [Kaggle](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce). It contains information on nearly 100,000 orders from 2016 to 2018.

The following files from the dataset were used:
- `olist_customers_dataset.csv`
- `olist_orders_dataset.csv`
- `olist_order_payments_dataset.csv`
- `olist_order_items_dataset.csv`

These files were merged to create a single, comprehensive dataset for the analysis.

## Analysis Pipeline

The project follows a structured approach, from data cleaning to advanced modeling:

1.  **Data Preparation:** The individual CSV files were loaded and merged. Date columns were converted to the proper datetime format, and missing values were handled. New features, such as `month_year` and `dayofweek`, were engineered to facilitate time-based analysis.

2.  **Exploratory Analysis & Visualization:**
    - Analyzed monthly revenue growth, identifying seasonal trends and overall business performance.
    - Tracked the number of active customers per month.
    - Compared the revenue contributions of new versus existing customers, highlighting the importance of customer retention.

3.  **RFM Segmentation:**
    - Calculated **Recency**, **Frequency**, and **Monetary** values for each unique customer.
    - Applied K-Means clustering to each of the R, F, and M metrics individually to create score-based clusters.
    - Combined these scores to create an overall RFM segment for each customer (e.g., "Low Value", "Mid Value", "High Value").

4.  **Customer Lifetime Value (CLV) Modeling:**
    - **BG/NBD Model (Beta-Geometric/Negative Binomial Distribution):** This model was trained to predict the number of future purchases a customer is likely to make. It analyzes the time between transactions and how recently a customer has been active.
    - **Gamma-Gamma Model:** This model was used to estimate the average monetary value of a customer's future transactions. It works by analyzing the monetary value of their past purchases.
    - **CLV Calculation:** The BG/NBD and Gamma-Gamma models were combined to calculate a projected CLV for each customer over the next 6 months.

5.  **Final Segmentation using CLV:**
    - The predicted CLV and other model outputs (like expected future purchases) were used as features for a final K-Means clustering model.
    - This resulted in three distinct, data-driven segments: **'Very Profitable'**, **'Profitable'**, and **'Non-Profitable'**.
    - Principal Component Analysis (PCA) was used to visualize these high-dimensional clusters in 2D space.

## Key Findings & Visualizations

#### Monthly Sales and New vs. Existing Customers
The analysis revealed a strong upward trend in sales, with a significant spike in November 2017 (likely due to Black Friday). While new customer acquisition drives a large portion of revenue, the contribution from existing customers grows steadily, showing the potential for a loyal customer base.


*(Image represents the type of plot generated in the notebook)*

#### RFM Segmentation
The RFM scatter plots clearly show distinct customer groups. For example, a cluster of high-value customers has both high frequency and high monetary value, while another group has made recent purchases but hasn't spent much.


*(Image represents the type of plot generated in the notebook)*

#### CLV-Based Customer Segments
The final segmentation provides a powerful way to view the customer base. The 'Very Profitable' segment, though small, represents customers with high predicted future value, making them prime candidates for loyalty programs. The 'Non-Profitable' group consists of customers who are unlikely to purchase again and have low expected value.


*(Image represents the type of plot generated in the notebook)*


## Models Used
- **K-Means Clustering:** For segmenting customers based on RFM scores and CLV predictions.
- **BG/NBD Model:** For predicting the number of future transactions.
- **Gamma-Gamma Model:** For estimating the average value of future transactions.
- **Principal Component Analysis (PCA):** For visualizing the final customer segments.
- **Linear Regression:** As an experimental approach to predict CLV based on historical monthly sales data.

## How to Run This Project

1.  **Clone the repository:**
    ```bash
    git clone [<repository-url>](https://github.com/vijaykalore/CustomerLifeTimeValue.git)
    ```
2.  **Install dependencies:** It's recommended to use a virtual environment.
    ```bash
    pip install -r requirements.txt
    ```
3.  **Download the data:** Place the Olist dataset CSV files in a `/content/` directory within the project folder, or update the file paths in the notebook.
4.  **Run the notebook:** Open and run the `project_notebook.ipynb` file using Jupyter Notebook or Google Colab.

## Dependencies

The project relies on the following Python libraries. You can install them using the command above.

- `pandas`
- `numpy`
- `matplotlib`
- `seaborn`
- `plotly`
- `scikit-learn`
- `lifetimes`
