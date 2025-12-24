Kattangal Grocery Store – Market Basket Analysis + Customer Clustering

## Objective
Improve profitability for Kattangal’s Grocery Store using:
1) **Market Basket Analysis (Apriori)** to find items that are frequently bought together and generate cross-sell / bundle recommendations.
2) **Customer Clustering (KMeans)** to segment customers and create targeted promotion strategies.

Dataset used: `Groceries data.csv` (primary) and `basket.csv` (optional/validation)

## Methodology

### 1) Data Preprocessing
- Converted `Date` to datetime.
- Cleaned `itemDescription` (lowercase, trimmed spaces).
- Created `TransactionID = Member_number + Date`  
  (One customer’s one-day purchase treated as one transaction/basket)
- Built baskets: list of unique items per transaction.
### 2) Exploratory Data Analysis (EDA)
Performed EDA to understand sales patterns:
- **Top frequently sold items**
- [Top frequent sold items](Screenshot2025-12-24225731.png)
- **Basket size distribution** 
- **Basket size box plot**
- [box plot](Screenshot2025-12-24225139.png)
- - **Co-occurrence heatmap** (top N items)
 - [Co-Occ Heatmap](Screenshot2025-12-24225008.png)
 
  - ### 3) Market Basket Analysis (Apriori)
Steps:
1. One-hot encoded baskets (14963 transactions × 167 items).
2. Applied Apriori with tuned `min_support` to get 2-itemsets.
3. Generated association rules using:
   - **support**
   - **confidence**
   - **lift**
4. Converted rules into store-friendly recommendations.

#### Key Rule Examples (Cross-sell)
- bottled beer → sausage (highest lift ~1.22)
- sausage → bottled beer
- frankfurter → other vegetables
- sausage ↔ yogurt
- sausage ↔ soda
#### Top Bundle Pairs (High Support)
- other vegetables + whole milk
- rolls/buns + whole milk
- soda + whole milk
- whole milk + yogurt
- other vegetables + rolls/buns

### 4) Customer Clustering (KMeans)
Customer features built from purchase behavior:
- `num_transactions`
- `avg_basket_size`
- `max_basket_size`
- `recency_days` (days since last purchase)

Model selection:
- Used **Elbow Method** + **Silhouette Score**
- Final clustering used **K=4** (interpretable business segments)

#### Cluster Interpretations
- **Frequent Regulars**: highest transaction frequency  
  Strategy: loyalty points, staple discounts
- **Bulk/Big-Basket Shoppers**: highest basket size  
  Strategy: bundle packs, “buy more save more”
- **Occasional Shoppers**: moderate frequency  
  Strategy: reminder offers + popular combos
- **Inactive/Lost Customers**: very high recency  
  Strategy: win-back coupons, limited-time deals



  ## Answers (Deliverable )

#### (i) Most frequently sold items
Top items include:
- whole milk, other vegetables, rolls/buns, soda, yogurt,
  root vegetables, tropical fruit, bottled water, sausage, citrus fruit

#### (ii) Most important items to always stock
**Must-stock staples (highest frequency + common bundles):**
- whole milk, other vegetables, rolls/buns, soda, yogurt
