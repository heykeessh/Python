# E-Commerce Sales Performance & Customer Retention Analytics Capstone

[![Python Version](https://img.shields.io/badge/Python-3.10%2B-blue.svg)](https://www.python.org/)
[![Jupyter Notebook](https://img.shields.io/badge/Jupyter-Notebook-orange.svg)](YourNotebook.ipynb)
[![Status](https://img.shields.io/badge/Capstone-Certified%20Proof-success.svg)]()
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

An end-to-end e-commerce analytics capstone evaluating **13,696 completed customer orders** and **₱6,237,133.72 in net realized revenue** across 4,692 unique buyers in the Philippines between January 2024 and January 2026.

---

## 📌 Repository Contents

```text
├── Executive Summary.txt                      # Concise bulleted executive summary (8–15 lines)
├── YourNotebook.ipynb                         # Jupyter Notebook containing data cleaning, ETL, and EDA
├── Cleaned_customers.csv                      # Cleaned customer demographic and loyalty table
├── Cleaned_products.csv                       # Standardized product catalog with prices and costs
├── chart1_monthly_revenue_trend.png           # Monthly realized net revenue time series
├── chart2_revenue_by_category.png             # Total net revenue by product category
├── chart3_revenue_by_region.png               # Top 10 regions by realized revenue
├── chart4_aov_distribution.png                # Order value distribution and density analysis
├── chart5_cancellations_returns_trend.png     # Monthly order cancellation and return trends
├── dashboard_1920x1080.png                    # High-resolution (16:9) executive BI dashboard
├── Capstone_Project_Report_Sales_Performance.docx # Complete capstone report (Word format)
└── README.md                                  # Repository overview and documentation
```

---

## 📄 Executive Summary (`Executive Summary.txt`)

* **Total Realized Net Cash:** Generated **₱6,237,133.72** across 13,696 fulfilled orders, strictly excluding cancelled transactions.
* **Active Customer Base:** 4,692 unique customers placed an average of **2.92 orders** over the 25-month operating window.
* **Exceptional Retention:** Achieved an **80.8% repeat customer rate** (3,793 repeat buyers) versus 19.2% one-time buyers (899 customers).
* **Average Basket Value:** Attained an Average Order Value (AOV) of **₱455.40**, with the median basket resting at ~₱380.00.
* **Revenue Consistency:** Monthly revenue held a steady baseline between **₱220,000 and ₱270,000**, with peak surges in April and July.
* **Top Product Categories:** **Toys (₱877,812)** and **Electronics (₱851,340)** generated the highest top-line revenue.
* **Balanced Product Catalog:** All 8 merchandise categories yielded between ₱665K and ₱878K, showing low concentration risk.
* **Decentralized Regional Demand:** **Central Luzon (₱1.07M)** and **Central Visayas (₱1.06M)** surpassed Metro Manila / NCR (₱1.05M).
* **Fulfillment Leakage:** Monthly cancellations averaged **40 to 60 orders**, while return requests averaged **20 to 30 orders**.
* **Operational Imbalance:** Pre-delivery cancellations outnumber post-delivery returns 2:1, indicating dispatch lag rather than product defects.
* **Data Quality Engineering:** Automated pipeline resolved currency symbol contamination (`₱`, `$`, commas), missing unit prices, and mixed timestamps.
* **Commercial Opportunity:** Introducing a **₱499 free shipping threshold** and regional 3PL hubs can drive an estimated **12%–18% incremental revenue lift**.

---

## 📓 Notebook Pipeline (`YourNotebook.ipynb`)

The primary notebook contains the complete data engineering and statistical analysis pipeline written in Python (`pandas`, `numpy`, `matplotlib`, `seaborn`):

1. **Currency String Cleaning:** Strips symbols (`₱`, `$`, `,`) and converts string fields into standard numeric floats.
2. **Entity Deduplication:** Enforces unique primary keys across `customers`, `orders`, `products`, `payments`, `shipments`, and `returns`.
3. **Category Harmonization:** Standardizes typographical variations (e.g., `'Fashon'` $\rightarrow$ `'Fashion'`, `'Elec'` $\rightarrow$ `'Electronics'`).
4. **Missing Value Imputation:** Imputes missing transaction prices (`unit_price_at_purchase`) using catalog prices from `products.csv` via left joins.
5. **Denormalized Fact Table:** Merges order items, orders, products, and customers into an analytical fact table (`fact_sales`).
6. **KPI Calculation:** Calculates Net Revenue, Cost of Goods Sold (COGS), Gross Item Margin, AOV, and Customer Retention.

```bash
# Run the pipeline notebook
jupyter notebook YourNotebook.ipynb
```

---

## 🗄️ Cleaned Datasets

### 1. `Cleaned_customers.csv`
| Column Name | Data Type | Description | Cleaning / Imputation Rule |
| :--- | :--- | :--- | :--- |
| `customer_id` | String | Unique customer identifier | Deduplicated across records |
| `gender` | String | Customer gender | Nulls replaced with `'Unknown'` |
| `age` | Integer | Customer age | Imputed using sample median (`34`) |
| `loyalty_tier` | String | Loyalty status | Nulls defaulted to `'Standard'` |
| `signup_date` | Date (`YYYY-MM-DD`) | Customer registration date | Mixed formats parsed into ISO timestamps |

### 2. `Cleaned_products.csv`
| Column Name | Data Type | Description | Cleaning / Imputation Rule |
| :--- | :--- | :--- | :--- |
| `product_id` | String | Unique product identifier | Deduplicated across catalog |
| `product_name` | String | Title of product | Stripped whitespace and casing standardized |
| `category` | String | Standardized category | Mapped into 8 distinct categories |
| `unit_price` | Float (PHP) | Retail price per unit | Stripped currency symbols (`₱`, `$`, `,`) |
| `unit_cost` | Float (PHP) | Base manufacturing cost | Used for COGS and margin calculation |

---

## 📊 Visualizations (5 Exported PNG Charts)

### Chart 1: Monthly Realized Net Revenue Trend
*Tracks monthly cash revenue trajectory across the 25-month transactional window.*
![Chart 1 - Monthly Revenue Trend](chart1_monthly_revenue_trend.png)

### Chart 2: Net Revenue by Product Category
*Revenue breakdown across the 8 standardized commercial categories.*
![Chart 2 - Revenue by Category](chart2_revenue_by_category.png)

### Chart 3: Top 10 Regions by Realized Revenue
*Geographic sales distribution across Philippine administrative regions.*
![Chart 3 - Top Regions](chart3_revenue_by_region.png)

### Chart 4: Order Value Distribution & Outlier Analysis
*Histogram and boxplot showing the right-skewed basket spend (Median: ₱380 vs. Mean: ₱455).*
![Chart 4 - AOV Distribution](chart4_aov_distribution.png)

### Chart 5: Monthly Cancellations and Returns Trend
*Fulfillment leakage tracking pre-shipment cancellations versus post-delivery returns.*
![Chart 5 - Cancellations and Returns](chart5_cancellations_returns_trend.png)

---

## 🖥️ Executive BI Dashboard (1920 × 1080 / 16:9 Ratio)

A high-resolution, production-grade analytics dashboard combining high-level KPIs and multi-panel performance metrics:

![Executive Dashboard 1920x1080](dashboard_1920x1080.png)

---

## 💡 Key Business Recommendations

1. **AOV Optimization:** Introduce a **₱499.00 Free Shipping Threshold** to encourage single-item buyers (median spend ₱380.00) to add an impulse item, raising overall basket size.
2. **Cancellation Reduction:** Implement automated SMS/in-app order tracking within 15 minutes of checkout to reassure buyers and curb pre-dispatch order cancellation.
3. **Decentralized Logistics:** Partner with regional 3PL hubs in Central Luzon (Clark) and Central Visayas (Cebu) to shorten delivery windows from 5–7 days to 24–48 hours.
4. **Top-of-Funnel Acquisition:** Offer first-time customer acquisition vouchers (₱100 off on first order $\ge$ ₱500) to balance the high repeat buyer rate (80.8%) with new user growth.

---

## 🛠️ Tech Stack & Setup

* **Language:** Python 3.10+
* **Libraries:** `pandas`, `numpy`, `matplotlib`, `seaborn`
* **Dashboard Specifications:** 1920 × 1080 Resolution, 16:9 Aspect Ratio

```bash
# Clone the repository
git clone https://github.com/your-username/ecommerce-sales-capstone.git

# Install dependencies
pip install -r requirements.txt

# Run the notebook
jupyter lab
```