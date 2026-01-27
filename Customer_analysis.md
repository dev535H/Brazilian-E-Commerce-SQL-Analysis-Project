## Customer Analysis
# 1.Who are the top 5 customers based on total spending?
Identifies high-value customers who contribute significantly to revenue.
```sql
select c.customer_id,sum(price) from
customers c join orders o
on c.customer_id=o.customer_id
join order_items oi
on oi.order_id=o.order_id
group by c.customer_id
order by sum(price) desc limit 5;
```

# 2.How many customers are repeat buyers?
Shows customer loyalty and retention by counting customers who placed more than one order.
```SQL
select count(*) as repeat_customer from(
select customer_id,count(customer_id) from
orders group by customer_id
having count(customer_id)<1
);
```
---
# 3.What is the average price per customer?
Helps estimate customer value and purchasing power.
```sql
select c.customer_id,avg(payment_value) from
customers c join orders o
on c.customer_id=o.customer_id
join payments p
on o.order_id=p.order_id
group by c.customer_id;
```
---
# 4.Which states have the highest number of customers?
Provides geographic insights into where most customers are located.
```sql
select c.customer_state,count(o.customer_id) from
customers c join orders o
on c.customer_id=o.customer_id
group by c.customer_state
order by count(o.customer_id) desc
limit 1;
```

---
# 5.Which cities generate the highest revenue?
Identifies high-performing cities that drive most of the sales
```sql
select c.customer_city,count(o.customer_id) from
customers c join orders o
on c.customer_id=o.customer_id
group by c.customer_city
order by count(o.customer_id) desc
limit 1;
```
