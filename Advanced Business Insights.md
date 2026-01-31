# 📈 Advanced Business Insights

## 1. What is the customer retention rate?
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
**OUTPUT**
<img width="266" height="79" alt="{538C0C75-E4FF-4134-A49E-DEF92D778932}" src="https://github.com/user-attachments/assets/d1223148-1140-480f-baeb-3196f18d244a" />
---

## 2. What is the lifetime value of the top customers?
Estimates total revenue contributed by the most valuable customers.
```sql
select o.customer_id,sum(payment_value) as total_revenue from customers c join orders o on o.customer_id=c.customer_id join payments p on 
o.order_id=p.order_id
group by o.customer_id
order by total_revenue desc
limit 10;
```
*OUTPUT*
<img width="481" height="204" alt="{469A3596-1EB7-4CC8-8FAE-8FC529CDD95D}" src="https://github.com/user-attachments/assets/27686a4f-703b-4340-b83e-afc44f9faf7c" />

---

## 3. Which product categories have high sales but low ratings?
Identifies “risk categories” that sell well but may hurt customer satisfaction.
```sql
select p.product_category_name,round(sum(oi.price+oi.freight_value),2) as revenue, round(avg(review_score),2) as rating 
from order_items oi join reviews r 
on oi.order_id=r.order_id
join products p
on p.product_id=oi.product_id
group by product_category_name
order by revenue desc , rating asc;
```
**OUTPUT**
![](screenshots/{D27FE45D-B76E-409E-B50B-2BCFC4360ABA}.png)
---

## 4. How does delivery time affect customer satisfaction?
Examines whether longer delivery times reduce review scores.
```sql
select extract(day from order_delivered_customer_date-order_purchase) as delay_date,round(avg(review_score),2) as rating,
count(*) as total_orders
from orders o join reviews r
on o.order_id=r.order_id
where order_delivered_customer_date is not null
group by extract(day from order_delivered_customer_date-order_purchase) 
order by delay_date desc;
```
**output**
![result](screenshots/{D7227A6F-04A6-4808-AF90-254379620BDA}.png)
---

## 5. Which state generates the highest revenue per customer?
Combines geographic and financial data to measure customer value by region.
```sql
select c.customer_state as customer_state,round(sum(p.payment_value)/count(distinct c.customer_id),2) as revenue_state
from customers c join orders o on o.customer_id=c.customer_id join payments p on 
o.order_id=p.order_id
group by c.customer_state
order by revenue_state desc;
```
*OUTPUT*
<img width="384" height="224" alt="{8A2D4757-6B60-4C7F-829F-A3D95C2B71B0}" src="https://github.com/user-attachments/assets/07b777c7-c442-4194-b7e6-5c5063e444b9" />

