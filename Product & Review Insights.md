# ⭐ Product & Review Insights
## 1. What is the overall average review score?
Provides a general measure of customer satisfaction.
```sql
select round(avg(review_score),2) as avg_score from reviews;
```
**OUTPUT**
<img width="179" height="90" alt="{F7F054FA-B688-4D46-8594-D284EB698043}" src="https://github.com/user-attachments/assets/ab829d76-3e4a-4036-afbc-479e91e83a7f" />

---
## 2. Which product categories receive the highest ratings?
Shows which types of products customers are most satisfied with.
```sql
select p.product_category_name,round(avg(r.review_score),2) as highest_category_score from
reviews r join order_items oi
on r.order_id=oi.order_id
join products p
on oi.product_id=p.product_id
where p.product_category_name is not null 
group by p.product_category_name
order by highest_category_review desc
limit 1;
```
**OUTPUT**
<img width="465" height="101" alt="{358C386A-9FE4-477D-A703-3C7A13763C0B}" src="https://github.com/user-attachments/assets/34ea5914-ab26-4dd6-b2aa-7f7758e9b11e" />


---
## 3. Which product categories receive the lowest ratings?
Helps identify categories that may need quality improvement.
```sql
select p.product_category_name,round(avg(r.review_score),2) as lowest_category_score from
reviews r join order_items oi
on r.order_id=oi.order_id
join products p
on oi.product_id=p.product_id
where p.product_category_name is not null 
group by p.product_category_name
order by lowest_category_score
limit 1;
```
**OUTPUT**
<img width="463" height="94" alt="{F0B306D0-9FD3-41A0-9836-7514B947B68D}" src="https://github.com/user-attachments/assets/ea051ab5-24e6-487b-ae2a-f69b881d0411" />

---
## 4. Do delayed deliveries lead to lower review scores?
Analyzes the relationship between delivery performance and customer satisfaction.
```sql

```
**OUTPUT**

---
## 5. What percentage of orders received a 5-star rating?
Indicates how often customers had an excellent experience.
```sql

```
**OUTPUT**

---
