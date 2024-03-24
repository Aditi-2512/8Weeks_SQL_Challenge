# A. Customer Nodes Exploration 💁
## Questions along with solution and logic 📖
### 1. How many unique nodes are there on the Data Bank system?
``` sql
SELECT COUNT(DISTINCT node_id) FROM data_bank.customer_nodes;
```
- In total there are 5 unique nodes.
- Logic - To get the unique value distinct is used which only takes a count of all the unique values in the table
