# A. Pizza Metrics 🍕
# Questions along with solutions and logic 📖
## 1. How many pizzas were ordered?
``` sql
SELECT COUNT(customer_id) FROM customer_orders;
```
- In total *14* pizzas were ordered
## 2. How many unique customer orders were made?
``` sql
SELECT COUNT(DISTINCT customer_id) AS unique_customers FROM customer_orders;
```
- There are 5 unique customer orders.
## How many successful orders were delivered by each runner?
``` sql
SELECT * FROM pizza_runner.runner_orders;
SELECT runner_id,COUNT(order_id) 
FROM pizza_runner.runner_orders
WHERE distance != 'null'
GROUP BY runner_id;
```
- Runner 1 delivered 4 successful orders.
- Runner 2 delivered 3 successful orders.
- Runner 3 delivered 1 successful order.
### 
   

