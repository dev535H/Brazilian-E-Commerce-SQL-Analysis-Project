📈 Advanced Business Insights

26. What is the customer retention rate?
Measures how many customers return to make additional purchases.
Retention Rate=(Repeat Customers/Total Customers)×100
```sql
SELECT 
    ROUND(
        100.0 * COUNT(DISTINCT CASE 
                                WHEN order_count > 1 THEN customer_id 
                              END)
        / COUNT(DISTINCT customer_id),
    2) AS customer_retention_rate
FROM (
    SELECT 
        customer_id,
        COUNT(order_id) AS order_count
    FROM orders
    GROUP BY customer_id
) AS customer_orders;
```


28. What is the lifetime value of the top customers?
Estimates total revenue contributed by the most valuable customers.

29. Which product categories have high sales but low ratings?
Identifies “risk categories” that sell well but may hurt customer satisfaction.

30. How does delivery time affect customer satisfaction?
Examines whether longer delivery times reduce review scores.

31. Which state generates the highest revenue per customer?
Combines geographic and financial data to measure customer value by region.
