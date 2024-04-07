# Transaction Analysis 💰
## Questions along with solutions 📖
## 1. How many unique transactions were there?
```sql
SELECT COUNT(DISTINCT txn_id)  AS unique_transactions FROM balanced_tree.sales;
```
- Answer: There are 2500 unique transactions
## 2. What is the average unique products purchased in each transaction?
```sql
WITH unique_prod_count AS (
  SELECT sales.txn_id, SUM(sales.qty) AS unique_count
  FROM balanced_tree.sales JOIN balanced_tree.product_details
  ON sales.prod_id = product_details.product_id
  GROUP BY sales.txn_id
  )
SELECT ROUND(AVG(unique_count)) AS avg_unique_count FROM unique_prod_count;
```
- Answer: The average unique products purchased are 18.
## 3. What are the 25th, 50th and 75th percentile values for the revenue per transaction?
```sql
WITH revenue_per_txn AS (
  SELECT sales.txn_id, SUM(sales.qty * product_details.price) AS revenue
  FROM balanced_tree.sales
  JOIN balanced_tree.product_details
  ON sales.prod_id = product_details.product_id
  GROUP BY sales.txn_id
)
SELECT
  PERCENTILE_CONT(0.25) WITHIN GROUP (ORDER BY revenue) AS "25th Percentile",
  PERCENTILE_CONT(0.5) WITHIN GROUP (ORDER BY revenue) AS "50th Percentile (Median)",
  PERCENTILE_CONT(0.75) WITHIN GROUP (ORDER BY revenue) AS "75th Percentile"
FROM revenue_per_txn;
```
- Answer:
25th Percentile | 50th Percentile | 75th Percentile
  ---| ---| ---
  375.75| 509.5| 647

## 4. What is the average discount value per transaction?
```sql
WITH discount_sum AS (
SELECT SUM(discount) AS total_discount FROM balanced_tree.sales
GROUP BY txn_id
)
SELECT ROUND(AVG(total_discount)) AS avg_discount FROM discount_sum;
```
- Answer: The average discount value per transaction is 73
## 5. What is the average revenue for member transactions and non-member transactions?
```sql
WITH count_txn AS (
  SELECT member , COUNT(DISTINCT txn_id) AS transaction
  FROM balanced_tree.sales
  GROUP BY member
  )

SELECT member ,transaction, ROUND(transaction * 100 /(SELECT SUM(transaction) FROM count_txn)) FROM count_txn
GROUP BY member,transaction;
```
Answer:
member|transaction|round
---|---|---
false|995|40
true|1505|60
  
