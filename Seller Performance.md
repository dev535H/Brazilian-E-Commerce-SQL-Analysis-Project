# 🏪 Seller Performance
## 1. Which sellers have completed the highest number of orders?
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
## 2. Which sellers generated the most revenue?
Highlights top-performing sellers based on sales value.
```sql
select s.seller_id,round(sum(oi.price+oi.freight_value),2) as total_revenue from sellers s join order_items oi
on oi.seller_id=s.seller_id
group by s.seller_id
order by total_revenue desc
limit 1;
```
**OUTPUT**
<img width="478" height="93" alt="{672A3036-0F65-4D8C-BFCF-F7E1E3705126}" src="https://github.com/user-attachments/assets/569812b2-178e-41e6-8415-159a63b0b4e2" />

---
## 3. What is the average review score for each seller?
Measures seller quality based on customer feedback.
```sql
select s.seller_id,round(avg(r.review_score),2) as avg_review,count(distinct oi.order_id) as total_order from sellers s join order_items oi
on oi.seller_id=s.seller_id
join reviews r
on oi.order_id=r.order_id
group by s.seller_id;

```
**OUTPUT**
<img width="569" height="522" alt="{FFECA63D-7C53-485F-83FB-00BF80CF3927}" src="https://github.com/user-attachments/assets/df0f292e-8531-4dda-95f9-6cc6a060ea1b" />

---
## 4. Which sellers have high sales but low ratings?
Detects sellers who perform well in volume but may have service or product quality issues.
```sql
select s.seller_id,round(avg(r.review_score),2) as avg_review,round(sum(oi.price+oi.freight_value),2) as total_revenue from sellers s join order_items oi
on oi.seller_id=s.seller_id
join reviews r
on oi.order_id=r.order_id
group by s.seller_id
order by avg_review, total_revenue desc;
```
**OUTPUT**
<img width="591" height="514" alt="{CA1F7DB7-399C-4BCD-8C4C-531E1166B296}" src="https://github.com/user-attachments/assets/86ef54a3-8711-4134-9276-b1795f37bce9" />

---
