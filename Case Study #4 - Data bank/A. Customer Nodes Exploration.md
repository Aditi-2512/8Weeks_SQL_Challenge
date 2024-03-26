# A. Customer Nodes Exploration 💁
## Questions along with solution and logic 📖
### 1. How many unique nodes are there on the Data Bank system?
``` sql
SELECT COUNT(DISTINCT node_id) FROM data_bank.customer_nodes;
```
- In total there are 5 unique nodes.
- Logic - To get the unique value distinct is used which only takes a count of all the unique values in the table
## 2. What is the number of nodes per region?
``` sql
SELECT region_id, COUNT ( node_id) FROM data_bank.customer_nodes
GROUP BY region_id
ORDER BY region_id ASC;
```
- Answer:

| region_id | count |
|-----------|-------|
| 2         | 735   |
| 3         | 714   |
| 4         | 665   |
| 5         | 616   |

- Logic - To get the number of nodes per region , we have grouped by "region_id" using GROUP BY function and then counted number of nodes.
## 3. How many customers are allocated to each region?
``` sql
SELECT regions.region_name, COUNT (customer_nodes.customer_id) FROM data_bank.customer_nodes
JOIN data_bank.regions ON regions.region_id = customer_nodes.region_id
GROUP BY  regions.region_name;
```
- Answer:

| region_id | count |
|-----------|-------|
| America   | 735   |
| Australia | 770   |
| Africa    | 714   |
| Asia      | 665   |
| Europe    | 616   |

- To get the count of customers per region, we have used GROUP BY function to group together customers as per their region and then count them.
## 4. How many days on average are customers reallocated to a different node?
``` sql
With node_days AS (
  SELECT customer_id, node_id, end_date-start_date AS days_in_node
  FROM data_bank.customer_nodes
  WHERE end_date != '9999-12-31'
  GROUP BY customer_id, node_id, start_date,end_date
  ) , total_node_days AS (
    SELECT customer_id , node_id , SUM(days_in_node) AS sum_nodes
    FROM node_days 
    GROUP BY customer_id,node_id
    )
    
    SELECT ROUND(AVG(sum_nodes)) AS avg__number_of_nodes FROM total_node_days;
```
- Answer: The average days for customers to get reallocated are 24 days.
- Logic: We have used date functions to get a count of the number of days and then used SUM function to get the total number of days. Using CTE's has helped us to simplify and write a clean code.
- Important Note - At the end of this dataset there are values given where the end date is 999-12-31. We are not considering that value while calculating the average as it won't give an accurate answer.
