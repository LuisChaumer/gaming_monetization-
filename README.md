# Gaming Analytics – In-Game Monetization & Paying User Behavior 🎮💰

**Author:** Luis Chaumer  
**Role:** Data Analyst  
**Tools:** Python, SQL (SQLite), Pandas, NumPy, Matplotlib, Jupyter Notebook  
**Dataset:** Synthetic — 20,000 users, 100K+ purchases

---

## 📘 Project Overview

This project analyzes **monetization and spending behavior** in a fictional free-to-play (F2P) mobile game.  
Using synthetic datasets containing **20,000 users** and their **in-app purchases**, the goal is to understand how users spend, what segments drive revenue, and how acquisition channels and countries influence profitability.

The analysis mimics real-world workflows used by gaming studios, monetization teams, and mobile product analytics.

---

## 🎯 Project Objectives

- Calculate core monetization KPIs:
  - **ARPU (Average Revenue Per User)**
  - **ARPPU (Average Revenue Per Paying User)**
  - **Payer Conversion Rate**
- Segment spenders into:
  - **Whales**
  - **Dolphins**
  - **Minnows**
- Analyze revenue by:
  - Country
  - Acquisition channel
  - User segment
- Use **SQL + Python** for full-stack analytic workflow
- Provide business recommendations to improve monetization strategy

---

## 📊 Dataset Description

### **Users dataset (`gaming_users_dataset.csv`)**
Includes 20,000 players with fields:

- `user_id`
- `install_date`
- `country`
- `platform`
- `acquisition_channel`
- `is_payer`
- `sessions`

### **Purchases dataset (`gaming_purchases_dataset.csv`)**
Contains all in-app purchases:

- `purchase_id`
- `user_id`
- `purchase_datetime`
- `amount`
- `item_type` (small/medium/large pack)
- `currency`

---

## 📈 Key Monetization KPIs

ARPU  = total_revenue / total_users  
ARPPU = total_revenue / total_payers  
Payer Conversion = payers / total_users
📊 Exploratory Analysis
1. Revenue Distribution

2. Revenue Share by Spender Segment

3. ARPU by Country

4. ARPU by Acquisition Channel

🐳 Spender Segmentation (Whales, Dolphins, Minnows)
Users with revenue > 0 were segmented:

Segment	Description	Share of Users	Share of Revenue
Minnows	Small spenders	~50%	Low impact
Dolphins	Medium spenders	~40%	Moderate impact
Whales	Top spenders	~10%	Very high impact

Whales contribute a disproportionate share of revenue, consistent with the Pareto principle seen in most F2P games.

🗄 SQL Analysis (SQLite)
SQL is widely used in live-ops, BI systems, and monetization dashboards.

Revenue by country and platform
sql
Copiar código
SELECT 
    country,
    platform,
    COUNT(DISTINCT user_id) AS users,
    SUM(revenue) AS total_revenue,
    ROUND(AVG(revenue), 2) AS arpu
FROM users
GROUP BY country, platform
ORDER BY total_revenue DESC;
Payer conversion by acquisition channel
sql
Copiar código
SELECT 
    acquisition_channel,
    COUNT(*) AS users,
    SUM(CASE WHEN revenue > 0 THEN 1 END) AS payers,
    ROUND(AVG(revenue), 2) AS arpu,
    ROUND(SUM(revenue) / NULLIF(SUM(CASE WHEN revenue > 0 THEN 1 END),0), 2) AS arppu
FROM users
GROUP BY acquisition_channel
ORDER BY payers DESC;
Top whale countries
sql
Copiar código
SELECT 
    country,
    COUNT(*) AS payers,
    ROUND(AVG(revenue),2) AS arppu,
    SUM(revenue) AS total_revenue
FROM users
WHERE revenue > 0
GROUP BY country
HAVING COUNT(*) >= 50
ORDER BY arppu DESC
LIMIT 10;
🚀 Business Insights
A small group of whales generates the majority of revenue.

Countries like US, UK, CA show the highest ARPPU levels.

Paid channels (Facebook Ads, Google Ads, TikTok Ads) bring more high-value users.

Organic users have lower payer conversion but strong overall engagement.

Medium-spenders ("dolphins") present a major monetization opportunity via upsell.

💡 Recommendations
Increase UA investment in high-ARPU and high-ARPPU acquisition channels.

Create personalized offers targeting dolphins to push them toward higher spending tiers.

Develop whale retention strategies (exclusive items, VIP events, bundles).

Localize pricing and promotions by country to maximize conversion.

Expand analysis with retention and engagement metrics to build complete LTV models.

🧰 Tech Stack
Python: Pandas, NumPy, Matplotlib, Seaborn

SQL: SQLite

Jupyter Notebook

KPIs: ARPU, ARPPU, payer conversion, whale analysis

📁 Repository Structure
kotlin
Copiar código
gaming-monetization-analysis/
├── data/
│   ├── gaming_users_dataset.csv
│   └── gaming_purchases_dataset.csv
├── notebooks/
│   └── gaming_monetization_analysis.ipynb
├── images/
│   ├── revenue_distribution.png
│   ├── spender_segments.png
│   ├── arpu_by_country.png
│   └── arpu_by_channel.png
└── README.md
📬 Contact
Luis Chaumer
Data Analyst
📩 Email: luischaumer@gmail.com
🔗 LinkedIn: www.linkedin.com/in/luis-chaumer123
