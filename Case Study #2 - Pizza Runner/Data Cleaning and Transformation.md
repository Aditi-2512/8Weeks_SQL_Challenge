# Data Cleaning and Transformation :shower:
After seeing all the tables I realised we had to get some cleaning done in order to process the queries effectively. 
## Table - customer_orders :raising_hand:
Created a new table with all the improvements from customer_orders table. The changes made in the customer_orders table are :
- All the blank and 'null' values in exclusions and extras column had to be converted to *Null*
``` sql
CREATE TABLE pizza_runner.customer_orders_clean AS
SELECT order_id , customer_id, pizza_id,
CASE WHEN exclusions = '' THEN NULL
	 WHEN exclusions = 'null' THEN NULL
	 ELSE exclusions
	 END AS exclusions,
CASE WHEN extras = '' THEN NULL
	   WHEN extras = 'null' THEN NULL
	   ELSE extras
	   END AS extras,
order_time
FROM pizza_runner.customer_orders;
```
### New Table : 
<img src="https://github.com/Aditi-2512/8Weeks_SQL_Challenge/assets/137753595/58cb366e-f955-425e-bb4e-235628bedaef " width="500" height="300">

## Table - runner_orders :runner:
Created a new table with all the improvements from runner_orders table. The changes made in the runner_orders table are :
- All the blank and 'null' values in pickup_time, distance, duration and cancellation columns had to be converted to *Null*
``` sql
CREATE TABLE runner_orders_clean AS 
SELECT order_id,runner_id , 
CASE WHEN pickup_time = 'null' THEN NULL
  ELSE pickup_time
  END AS pickup_time,
CASE WHEN distance LIKE '%km' THEN TRIM('km' FROM distance)
	 WHEN distance = 'null' THEN NULL
   ELSE distance END AS distance,
CASE WHEN duration LIKE '%minutes' THEN TRIM('minutes' FROM duration)
	 WHEN duration LIKE '%mins' THEN TRIM('mins' FROM duration)
	 WHEN duration LIKE '%minute' THEN TRIM('minute' FROM duration)
	 WHEN duration = 'null' THEN NULL
ELSE duration END AS duration,
CASE WHEN cancellation = 'null' THEN NULL
	   WHEN cancellation = '' THEN NULL
ELSE cancellation END AS cancellation
FROM pizza_runner.runner_orders;
```
### New Table :
<img src="https://github.com/Aditi-2512/8Weeks_SQL_Challenge/assets/137753595/36841af2-a7d6-45c2-9197-69d5f26a5868" width="650" height="300">
