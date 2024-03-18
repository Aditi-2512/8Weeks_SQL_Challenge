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
## 3. How many successful orders were delivered by each runner?
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
## 4. How many of each type of pizza was delivered?
``` sql
SELECT COUNT(customer_orders.pizza_id) AS pizza_count , pizza_names.pizza_name
FROM pizza_runner.customer_orders JOIN pizza_runner.pizza_names
ON customer_orders.pizza_id = pizza_names.pizza_id
JOIN runner_orders_clean ON customer_orders.order_id = runner_orders_clean.order_id
WHERE runner_orders_clean.cancellation IS NULL
GROUP BY pizza_names.pizza_name;
```
- 9 Meatlover and 3 Vegetarian pizzas were delivered.
## 5. How many Vegetarian and Meatlovers were ordered by each customer?
``` sql
SELECT pizza_names.pizza_name , COUNT(customer_orders.pizza_id)
FROM pizza_runner.customer_orders JOIN pizza_runner.pizza_names
ON customer_orders.pizza_id = pizza_names.pizza_id
GROUP BY pizza_names.pizza_name;
```
- 10 Meatlover and 4 Vegetarian pizzas were ordered by the customers
## 6. What was the maximum number of pizzas delivered in a single order?
``` sql
SELECT COUNT(order_id) , order_id
FROM customer_orders
GROUP BY order_id
ORDER BY COUNT(order_id) DESC LIMIT 1;
```
- The maximum number of pizzas delivered in a single order where 4 pizzas for order_id 3
## 7. How many pizzas were delivered that had both exclusions and extras?
``` sql
SELECT order_id, COUNT(pizza_id) FROM pizza_runner.customer_orders_clean
WHERE exclusions IS NOT NULL AND extras IS NOT NULL
GROUP BY order_id;
```
- 2 pizzas ( that is order 9 and 10) where delivered that had both exclusions and extras
## 8. What was the total volume of pizzas ordered for each hour of the day?
``` sql
SELECT EXTRACT(HOUR FROM order_time) AS hour_of_the_day, COUNT(customer_id)
FROM pizza_runner.customer_orders_clean
GROUP BY EXTRACT(HOUR FROM order_time);
```
- The answer :
<image src = "https://github.com/Aditi-2512/8Weeks_SQL_Challenge/assets/137753595/82d39688-24d6-4ce6-b12b-16a2f18c861b" height = '200' width = '250'>

   

