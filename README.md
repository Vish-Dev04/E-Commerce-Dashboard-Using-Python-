# E-Commerce Customer Segmentation using RFM Analysis & K-Means Clustering

![Customer Segments](https://placehold.co/800x400/4F46E5/FFFFFF?text=Customer+Segment+Distribution)

## 📖 Overview

This project performs customer segmentation on an e-commerce dataset using RFM (Recency, Frequency, Monetary) analysis and the K-Means clustering algorithm. The primary goal is to identify distinct customer groups based on their purchasing behavior to enable targeted and effective marketing strategies.

The analysis involves data cleaning, feature engineering to calculate RFM metrics, and applying machine learning to group customers into meaningful segments like "Loyal Customers," "At-Risk Customers," and "Potential High-Value."

---

## 📂 Dataset

The project utilizes the "Online Retail" dataset, which contains transactional data for a UK-based online retail company.

* **Source:** The dataset can be found on the [UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/datasets/online+retail).
* **Attributes:**
    * `InvoiceNo`: Invoice number. A 6-digit integral number uniquely assigned to each transaction.
    * `StockCode`: Product (item) code. A 5-digit integral number uniquely assigned to each distinct product.
    * `Description`: Product (item) name.
    * `Quantity`: The quantities of each product (item) per transaction.
    * `InvoiceDate`: The day and time when each transaction was generated.
    * `UnitPrice`: Product price per unit in sterling (£).
    * `CustomerID`: Customer number. A 5-digit integral number uniquely assigned to each customer.
    * `Country`: The name of the country where each customer resides.

---

## 🛠️ Project Pipeline

The analysis follows these key steps:

1.  **Data Loading & Initial Exploration:**
    * The dataset is loaded from an Excel file.
    * Initial checks are performed to understand the data's structure, identify missing values, and view summary statistics.

2.  **Data Cleaning & Preprocessing:**
    * Rows with missing `CustomerID` are dropped.
    * Duplicate transactions are removed.
    * Transactions with negative `Quantity` (returns) or zero `UnitPrice` are filtered out.
    * Data types are corrected where necessary (e.g., `CustomerID` to integer, `InvoiceDate` to datetime).

3.  **Feature Engineering (RFM Calculation):**
    * **Recency (R):** Calculated as the number of days between a customer's last purchase and the latest date in the dataset.
    * **Frequency (F):** Calculated as the total number of unique invoices for each customer.
    * **Monetary (M):** Calculated as the total revenue generated from each customer.

4.  **Data Transformation & Scaling:**
    * The RFM metrics are highly skewed. A logarithmic transformation (`log1p`) is applied to normalize their distributions.
    * The log-transformed data is then scaled using `StandardScaler` to ensure each feature has a mean of 0 and a standard deviation of 1, which is crucial for K-Means.

5.  **Clustering with K-Means:**
    * The **Elbow Method** and **Silhouette Analysis** are used to determine the optimal number of clusters (k).
    * The K-Means algorithm is trained on the scaled RFM data to partition customers into distinct groups. For this analysis, `k=3` was chosen.

6.  **Segmentation & Visualization:**
    * Each cluster is analyzed based on its mean Recency, Frequency, and Monetary values to create a customer persona.
    * Segments are named:
        * **Loyal Customers:** High frequency and monetary value, low recency.
        * **Potential High-Value:** Low recency, with moderate frequency and monetary value.
        * **At-Risk Customers:** High recency (haven't purchased in a while) and low frequency/monetary value.
    * Visualizations are created using `seaborn` and `matplotlib` to display segment distributions and characteristics.

---

## 🚀 How to Run

To replicate this analysis, follow these steps:

1.  **Clone the repository:**
    ```bash
    git clone [https://github.com/your-username/your-repo-name.git](https://github.com/your-username/your-repo-name.git)
    cd your-repo-name
    ```

2.  **Install dependencies:**
    Ensure you have Python 3 installed. Then, install the required libraries:
    ```bash
    pip install pandas numpy matplotlib seaborn scikit-learn jupyterlab
    ```

3.  **Add the Dataset:**
    * Download the `Online Retail.xlsx` file.
    * Place it in the root directory of the project.

4.  **Run the Jupyter Notebook:**
    Launch Jupyter Lab and open the `E-Commerce Dashboard .ipynb` notebook to execute the analysis.
    ```bash
    jupyter lab
    ```

---

## 📈 Results & Recommendations

The analysis successfully segmented customers into three distinct groups, providing actionable insights for the marketing team:

* **Loyal Customers:**
    * **Characteristics:** Frequent buyers, high spenders, and recent shoppers. They are the most valuable customers.
    * **Recommendation:** Focus on retention. Engage them with loyalty programs, exclusive access to new products, and premium support.

* **Potential High-Value:**
    * **Characteristics:** Recent shoppers with average frequency and spending. They have the potential to become loyal customers.
    * **Recommendation:** Nurture these relationships. Use personalized marketing, recommend related products, and offer limited-time discounts to encourage repeat purchases.

* **At-Risk Customers:**
    * **Characteristics:** Haven't purchased in a long time, low purchase frequency, and low overall spending.
    * **Recommendation:** Implement reactivation campaigns. Target them with special "we miss you" offers, highlight new products, or solicit feedback to understand their inactivity.

---
