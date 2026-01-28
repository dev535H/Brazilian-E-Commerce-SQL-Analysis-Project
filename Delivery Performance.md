# 📦 Delivery Performance
## 1. What is the average delivery time for orders?
Measures logistics efficiency by calculating the time between purchase and delivery.
```sql
select avg(order_delivered_customer_date-order_purchase) as avrage_time
from orders;
```
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


## 4. What percentage of orders were delivered late?
Shows how often delivery promises were not met.

## 5. What is the average freight cost per order?
Analyzes shipping costs and their impact on overall expenses.
