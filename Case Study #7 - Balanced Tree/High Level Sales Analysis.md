## High Level Sales Analysis 📈
## Questions along with solutions 📖
## 1. What was the total quantity sold for all products?
```sql
SELECT SUM(qty) FROM balanced_tree.sales AS total_quantity;
```
Answer: 45216
## 2. What is the total generated revenue for all products before discounts?
```sql
SELECT product_details.product_name, SUM(sales.qty) * SUM(sales.price) 
FROM balanced_tree.product_details JOIN balanced_tree.sales
ON product_details.product_id = sales.prod_id
GROUP BY product_details.product_name;
```
- Answer :

product_name | total_revenue
--- | ---
White Tee Shirt - Mens | 192736000
Navy Solid Socks - Mens | 174871872
Grey Fashion Jacket - Womens |	266862600
Navy Oversized Jeans - Womens	| 63863072
Pink Fluro Polkadot Socks - Mens  | 137537140
Khaki Suit Jacket - Womens | 107611112
Black Straight Jeans - Womens | 150955392
White Striped Socks - Mens | 77233805
Blue Polo Shirt - Mens	| 276022044
Indigo Rain Jacket - Womens | 89228750
Cream Relaxed Jeans - Womens | 46078010
Teal Button Up Shirt - Mens |45283320
## 3. What was the total discount amount for all products?
```sql
SELECT product_details.product_name, SUM(sales.qty * sales.price * sales.discount/100) AS total_discount
FROM balanced_tree.sales JOIN balanced_tree.product_details ON
sales.prod_id = product_details.product_id
GROUP BY product_details.product_name;
```
- Answer :

product_name| total_discount
--- | ---
White Tee Shirt - Mens |	17968
Navy Solid Socks - Mens	| 16059
Grey Fashion Jacket - Womens |	24781
Navy Oversized Jeans - Womens	|5538
Pink Fluro Polkadot Socks - Mens|	12344
Khaki Suit Jacket - Womens	| 9660
Black Straight Jeans - Womens	| 14156
White Striped Socks - Mens	| 6877
Blue Polo Shirt - Mens	| 26189
Indigo Rain Jacket - Womens |	8010
Cream Relaxed Jeans - Womens |	3979
Teal Button Up Shirt - Mens	| 3925
