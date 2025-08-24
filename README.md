# 📈 E-Commerce Customer Segmentation & CLV Analysis

![Customer Segmentation](https://github.com/user-attachments/assets/7b257d34-675f-44f1-8fb3-309ec183a9ea)  
*Unlocking key customer groups—VIPs, loyal buyers, mass-market, and at-risk segments—with RFM & CLV analysis.*


---

# 📊 Executive Summary

Many online stores struggle to answer three big questions:  
**Who are my best customers? Who might leave soon? And where should I focus my money?**  
Without clear answers, businesses often waste time and budget on the wrong people.

To solve this problem for an ecommerce store, I analyzed customer transaction data using **RFM (Recency, Frequency, Monetary)** and **Customer Lifetime Value (CLV)**. I then applied **clustering methods (K-Means and Hierarchical Clustering)** to group customers with similar shopping behavior. This moved the business away from guesswork and towards data-driven segmentation.

The results gave the business a **clear customer map with 4 distinct groups**:  
- A **tiny VIP segment** (≈5–7 customers) who buy very often (64–118 orders) and spend the most, with an average lifetime value of **$58k–$73k**.  
- A **large mid-value group** (≈476–602 customers) that buys occasionally (3–4 orders) and spends around **$1.2k–$1.4k** each.  
- A **profitable loyal segment** (≈39–56 customers) who purchase regularly (18–23 orders) and bring **$5k–$6k CLV**.  
- An **at-risk group** (≈170–207 customers) who rarely return (≈1 order) and have very low CLV (**$280–$298**).  

🎉 With these insights, the store can now:  
- **Protect its revenue** by giving VIPs special care (they are <1% of customers but drive most sales).  
- **Grow profits** by nurturing the high-value loyal group and encouraging the mass segment to buy more often.  
- **Reduce losses** by targeting the at-risk group with win-back campaigns instead of spending blindly.  

---

# 🎯 Project Objectives

The objective of this project is to help an e-commerce business **understand its customers better and make smarter marketing decisions using data**.  

To achieve this, the project focuses on three main goals:

1. **Segment Customers Effectively**  
   - Apply **RFM (Recency, Frequency, Monetary)** and **Customer Lifetime Value (CLV)** to capture shopping behavior.  
   - Use **unsupervised learning (K-Means & Hierarchical Clustering)** to create meaningful customer groups.  

2. **Validate and Interpret Clusters**  
   - Ensure clusters are reliable using the **Elbow Method** and **Silhouette Score**.  
   - Profile each cluster to uncover patterns in recency, frequency, spending, and CLV.  

3. **Enable Actionable Business Strategies**  
   - Identify **VIP customers** who drive the majority of revenue.  
   - Detect **at-risk customers** for re-engagement campaigns.  
   - Highlight **growth opportunities** in mid-value and loyal customer groups.  

📌 By achieving these objectives, the project provides e-commerce teams with **clear customer insights** to:  
- Spend marketing budgets more wisely  
- Keep their most valuable customers happy  
- Re-engage those at risk of leaving  
- Grow overall revenue in a data-driven way  

---

# 📂 Data Collection

The dataset for this project was sourced from **Kaggle** and contains detailed e-commerce transactions.  
It includes key fields such as customer IDs, product details, transaction dates, purchase quantities, and monetary values.  

This dataset is well-suited for customer segmentation because it provides enough information to calculate **RFM metrics (Recency, Frequency, Monetary)** and estimate **Customer Lifetime Value (CLV)**. These features make it possible to group customers based on their purchasing behavior and uncover meaningful insights for business strategy.

---

# 🔍 Exploratory Data Analysis (EDA)

EDA was performed on the training dataset to understand its structure, quality, and customer purchasing behavior. The dataset contained over **228k transactions**, with no missing values in key fields (CustomerID, InvoiceDate, Quantity, UnitPrice).  

### Key Findings
- **Data Quality**: No missing values, but extreme outliers were observed in `Quantity` (ranging from -80k to +80k) and `UnitPrice` (up to 38k).  
- **Country Analysis**: The majority of transactions came from the **United Kingdom**, followed by a few other European countries.  
- **Sales Trends**: Monthly sales showed clear seasonal patterns with noticeable spikes around peak shopping periods.  
- **Top Products**: A small number of products contributed a large share of sales, reflecting the 80/20 Pareto principle common in retail.  

### Visualizations
- 📊 **Top 10 Countries by Transactions**  
    ![Top Countries](https://github.com/user-attachments/assets/ee71912e-3a13-4e5b-914f-3ab1b2cd015d)


- 📈 **Monthly Sales Trend**  
  ![Monthly Sales](https://github.com/user-attachments/assets/e5680e97-8d8d-4320-8fc7-756362e65ea5)


- 🛍️ **Top 10 Products by Sales Value**  
  ![Top Product](https://github.com/user-attachments/assets/0299a35e-ec16-458f-9caa-8ec5ddbdacae)

---

# ⚙️ Feature Engineering & Preprocessing  

The data preparation process ensured that the dataset was clean, structured, and ready for modeling. It involved three key stages:  

### 1. Cleaning the Data  
From EDA, we identified invalid records such as negative quantities (product returns) and zero-priced items (free samples or errors). These were removed, along with duplicate rows. After cleaning, the dataset reduced from **228,139 rows** to **222,857 valid transactions**, ensuring higher data quality for downstream analysis.  

### 2. Feature Engineering  
Since the goal was customer segmentation, we transformed the dataset from **transaction-level** to **customer-level**. Key steps included:  
- Creating **TotalPrice** per transaction (`Quantity × UnitPrice`).  
- Extracting **date components** (month, day, hour) from `InvoiceDate`.  
- Aggregating customer behavior into **RFM features**:  
  - **Recency**: Days since last purchase.  
  - **Frequency**: Number of unique purchase occasions.  
  - **Monetary**: Total spending.  
- Adding extended features such as:  
  - **Average basket size** (mean quantity per transaction).  
  - **Total quantity purchased**.  
  - **Average unit price paid**.  
  - **Country** of the customer.  

This transformation resulted in a dataset of **2,776 unique customers** with rich behavioral profiles.  

### 3. Scaling & Encoding  
To make the features suitable for machine learning:  
- **Numerical features** (Recency, Frequency, Monetary, etc.) were scaled using **StandardScaler** so that no variable dominated due to magnitude differences.  
- **Categorical feature** (Country) was encoded using **OneHotEncoding**, expanding into **37 binary columns** representing each country.  
- **CustomerID** was dropped, as it’s only an identifier.  

The final processed dataset contained **2,776 customers × 37 features**, standardized and ready for clustering and predictive modeling.  

This structured pipeline was applied consistently across **train, validation, and test sets** to ensure comparability and prevent data leakage.  

---


# 🤖 Modeling & Model Selection  

Since the goal of this project is **customer segmentation** using RFM and CLV features, the task is inherently **unsupervised learning**. I experimented with several clustering approaches, each offering different strengths:  

- **K-Means**: Fast, scalable, and highly interpretable — a strong baseline for business applications.  
- **Hierarchical Clustering**: Useful for visualizing relationships between clusters, though less scalable.  
- **DBSCAN**: Good for detecting anomalies and irregular clusters, but struggled here due to noise.  
- **Gaussian Mixture Models (GMM)**: Provided flexibility with soft assignments (probabilistic memberships).  

---

# 🤖 Modeling & Model Selection  

Since the goal of this project is **customer segmentation** using RFM and CLV features, the task is inherently **unsupervised learning**. I experimented with several clustering approaches, each offering different strengths:  

- **K-Means**: Fast, scalable, and highly interpretable — a strong baseline for business applications.  
- **Hierarchical Clustering**: Useful for visualizing relationships between clusters, though less scalable.  
- **DBSCAN**: Good for detecting anomalies and irregular clusters, but struggled here due to noise.  
- **Gaussian Mixture Models (GMM)**: Provided flexibility with soft assignments (probabilistic memberships).  

### Model Evaluation  
Cluster quality was assessed using the **Silhouette Score**, balancing cohesion within clusters and separation between them.  

- **K-Means (k=6)**: **0.515** (best balance of performance and interpretability).  
- **Hierarchical (k=6)**: **0.489** (slightly lower, with some imbalance across clusters).  
- **GMM (k=6)**: **0.510** (close to K-Means but less stable).  
- **DBSCAN**: Failed to form meaningful clusters without excessive noise.  

### Choice of Number of Clusters  
While the **Elbow Method** suggested diminishing returns beyond 5–6 clusters, the **Silhouette analysis** showed that although k=2 achieved the highest score (>0.92), it was too simplistic for actionable insights. At **k=6**, the clusters achieved both good separation (~0.52 Silhouette) and meaningful business differentiation (e.g., high-value loyalists, bargain seekers, new but promising customers).  

### Final Model  
- **K-Means with 6 clusters** was selected as the primary model, as it delivered the most stable and interpretable segmentation.  
- **GMM (k=6)** was kept as a backup option, since it performed comparably and may add flexibility in future scenarios.  
- On the **test set**, K-Means maintained a **Silhouette Score of 0.516**, confirming its reliability for customer segmentation.  

---

## 📌 Recommendations  

Based on the customer segmentation and profiling:  

- **Focus on VIPs (Cluster 1):** These few customers bring in a huge share of revenue. Keep them happy with personal care, loyalty rewards, and early access to products. Losing them would mean big revenue loss.  

- **Grow High-Value Customers (Cluster 4):** This group spends a lot and buys often. They should be nurtured with referral programs, upselling, and membership perks to scale profits further.  

- **Re-Engage At-Risk Customers (Cluster 3):** These customers have stopped buying. Use win-back campaigns, discounts, and surveys to understand their needs. If they cannot be reactivated, reduce marketing spend on them.  

- **Activate Mid-Value Buyers (Cluster 0):** They form the largest group. Even a small increase in spending or frequency could drive strong growth. Offer loyalty perks (like discounts on repeat purchases) and cross-sell related products.  

---

## ⚠️ Limitations  

- **Data Scope:** The analysis is based only on past transactions within the dataset. Customer behavior outside this period (or across other channels) is not captured.  

- **CLV Assumption:** CLV was estimated with a fixed gross margin (60%). Actual margins may differ across products, which could change results.  

- **Dynamic Behavior:** Customer behavior can change over time (e.g., seasonality, market shifts). Clusters found here may not remain stable in the long term.  

- **Sample Size:** Some clusters (e.g., VIPs) have very few customers, so small changes in their behavior may heavily affect results.  

---

## 🚀 Future Work  

- **Add More Features:** Include marketing response data, demographics, or browsing behavior to improve segmentation.  

- **Time-Series Modeling:** Use survival models or churn prediction to better capture customer life cycles over time.  

- **Profit-Based Segmentation:** Instead of only revenue, also analyze net profit contribution per customer.  

- **Automated Updates:** Build a pipeline to refresh clusters regularly (e.g., monthly) so strategies remain current.  

- **A/B Testing:** Run experiments (like loyalty offers vs. discounts) to measure the real business impact of segmentation strategies.  

---

## 🏁 Conclusion  

This project showed how customer segmentation combined with CLV analysis can give clear, actionable insights. By identifying VIPs, high-value customers, mid-value buyers, and at-risk groups, businesses can focus on what truly drives growth.  

The findings highlight that **a few VIPs drive most revenue**, **mid-value customers hold growth potential**, and **at-risk buyers need reactivation strategies**. With targeted actions, companies can boost loyalty, prevent churn, and increase overall profitability.  

Future improvements like adding more data sources, using advanced models, and running experiments will make the insights even more powerful and business-ready.  


---

## 🏁 Closing Remark  

This project shows how customer segmentation and CLV analysis can uncover hidden growth opportunities and guide smarter business strategies.  

I am passionate about using data to solve real business problems and drive measurable value.  

I am open to exploring full-time opportunities where I can contribute to business strategy through analytics, as well as freelance collaborations with organizations seeking to leverage data for smarter decision-making.

🔗 LinkedIn: [Osaretin Idiagbonmwen](www.linkedin.com/in/osaretin-idiagbonmwen-33ab85339)  
📩 Email: oidiagbonmwen@gmail.com  
