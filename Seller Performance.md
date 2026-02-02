# 🏪 Seller Performance
1. Which sellers have completed the highest number of orders?
Identifies the most active sellers on the platform.
```sql
select s.seller_id,count(distinct oi.order_id) as total_orders from sellers s join order_items oi
on oi.seller_id=s.seller_id
group by s.seller_id
order by total_orders desc
limit 1;
```
**OUTPUT**
<img width="469" height="87" alt="{581380E0-D1D4-42B1-8BD2-36B8E23FE210}" src="https://github.com/user-attachments/assets/38b0e183-89f9-475c-9076-06a164c79c90" />

---
2. Which sellers generated the most revenue?
Highlights top-performing sellers based on sales value.
```sql

```
**OUTPUT**

---
3. What is the average review score for each seller?
Measures seller quality based on customer feedback.
```sql

```
**OUTPUT**

---
4. Which sellers have high sales but low ratings?
Detects sellers who perform well in volume but may have service or product quality issues.
```sql

```
**OUTPUT**

---
