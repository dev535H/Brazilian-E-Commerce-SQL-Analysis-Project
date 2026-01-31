# 📦 Delivery Performance
## 1. What is the average delivery time for orders?
Measures logistics efficiency by calculating the time between purchase and delivery.
```sql
select avg(order_delivered_customer_date-order_purchase) as avrage_time
from orders;
```
**OUTPUT**
![](screenshots/{6EDDD1EF-D4BD-4D96-B2BA-FA4EF61F6562}.png)
---
## 2. Which states have the fastest average delivery time?
Highlights regions where delivery operations are most efficient.
```sql
select customer_state,avg(extract(day from order_estimated_delivery_date-order_delivered_customer_date)) as average_dilvery
from customers c join orders o
on c.customer_id=o.customer_id
where o.order_delivered_customer_date is not null
group by c.customer_state
order by average_dilvery desc
limit 1;
```
**OUTPUT**

---
## 3. Which states experience the most delivery delays?
Identifies areas with logistics challenges.
```sql
select customer_state,avg(extract(day from order_estimated_delivery_date-order_delivered_customer_date)) as average_dilvery_delay
from customers c join orders o
on c.customer_id=o.customer_id
where o.order_delivered_customer_date is not null
group by c.customer_state
order by average_dilvery_delay asc
limit 1;
```
**OUTPUT**

---
## 4. What percentage of orders were delivered late?
Shows how often delivery promises were not met.
```sql
SELECT ROUND( 100.0 * SUM(
            CASE 
                WHEN order_delivered_customer_date > order_estimated_delivery_date 
                THEN 1 ELSE 0 
            END
        ) 
        / COUNT(order_id),2) AS percent_late_orders
FROM orders
WHERE order_delivered_customer_date IS NOT NULL;
```
**OUTPUT**

---
## 5. What is the average freight cost per order?
Analyzes shipping costs and their impact on overall expenses.
```sql
select avg(order_freight) from (select o.order_id ,sum(oi.freight_value) as order_freight from 
orders o left join order_items oi
on o.order_id=oi.order_id
group by o.order_id) as freight_per_order ;
```
**OUTPUT**
