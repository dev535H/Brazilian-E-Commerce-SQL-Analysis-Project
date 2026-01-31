# Customer Analysis
## 1.Who are the top 5 customers based on total spending?
Identifies high-value customers who contribute significantly to revenue.
```sql
select c.customer_id,round(sum(oi.price+oi.freight_value),2) as total_revenue from 
customers c join orders o
on c.customer_id=o.customer_id
join order_items oi
on oi.order_id=o.order_id
group by c.customer_id
order by total_revenue desc
limit 5;
```
**OUTPUT**
<img width="467" height="205" alt="{F0EF2512-D59F-422A-B17E-D647CD78DEC5}" src="https://github.com/user-attachments/assets/de3b6f30-79bd-4e92-9bba-82c023299af9" />


## 2.How many customers are repeat buyers?
Shows customer loyalty and retention by counting customers who placed more than one order.
```SQL
select count(*) as repeat_customer from(
select customer_id,count(customer_id) from
orders group by customer_id
having count(customer_id)1
);
```
**OUTPUT**
<img width="305" height="83" alt="{7F6F3AEC-68FF-4413-A656-C77F844303B7}" src="https://github.com/user-attachments/assets/bf71a145-6f42-4f1f-b1f8-1a2519bff697" />

---
## 3.Which states have the highest number of customers?
Provides geographic insights into where most customers are located.
```sql
select c.customer_state,count(o.customer_id) as customer_count from
customers c join orders o
on c.customer_id=o.customer_id
group by c.customer_state
order by customer_count desc
limit 1;
```
**OUTPUT**
<img width="395" height="87" alt="{55179646-9A15-4A7D-B483-565A29F81C3E}" src="https://github.com/user-attachments/assets/bd0b2015-c6de-40ae-a296-f901cd2e4fa1" />

---
## 4.Which cities generate the highest revenue?
Identifies high-performing cities that drive most of the sales
```sql
select c.customer_city,round(sum(payment_value),2) as revenue from
customers c join orders o
on c.customer_id=o.customer_id
join payments p
on o.order_id=p.order_id
group by c.customer_city
order by revenue desc
limit 1;
```
**OUTPUT**
