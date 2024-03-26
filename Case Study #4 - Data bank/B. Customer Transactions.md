# B. Customer Transactions 💰
## Questions with solutions and logic 📖
## 1. What is the unique count and total amount for each transaction type?
```sql
SELECT txn_type, COUNT(DISTINCT customer_id) , SUM(txn_amount) 
FROM data_bank.customer_transactions
GROUP BY txn_type;
```
Answer:
transaction_type | count | total_amount 
--- | --- | ---
deposit | 500 | 1359168
purchase | 448 | 806537
withdrawal | 439 | 793003

- Logic: We have used GROUP BY to collect the count and sum as per the transaction type and then used COUNT(DISTINCT) and SUM to get unique values as well as the sum.
## What is the average total historical deposit counts and amounts for all customers?
```sql
SELECT ROUND(AVG(sum_deposit),2) , COUNT(DISTINCT customer_id) 
FROM (
  SELECT customer_id, SUM(txn_amount) AS sum_deposit 
  FROM data_bank.customer_transactions 
  WHERE txn_type = 'deposit'
  GROUP BY customer_id
  ) AS deposit_amount;
```
- Answer: The average historical deposits are 2718.34 for the customers
- Logic: We have used subquery to calculate sum of all the customer where the transaction type is deposit . After calculating the sum we have calculated the average to understand the average total historical deposit. We had to use a subquery as we aggregate functions cannot be nested in SQL.
## For each month - how many Data Bank customers make more than 1 deposit and either 1 purchase or 1 withdrawal in a single month?
```sql


