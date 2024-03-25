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

- 
