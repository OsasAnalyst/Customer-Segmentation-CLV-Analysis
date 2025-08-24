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

