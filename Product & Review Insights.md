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
select p.product_category_name,round(avg(r.review_score),2) as avg_category_score from
reviews r join order_items oi
on r.order_id=oi.order_id
join products p
on oi.product_id=p.product_id
where p.product_category_name is not null 
group by p.product_category_name
order by round(avg(r.review_score),2) desc
limit 1;
```
**OUTPUT**
<img width="435" height="91" alt="{DA4DAB27-5A78-4507-A602-9B5962A9BD21}" src="https://github.com/user-attachments/assets/73ad4a2e-9ef7-4687-9257-a5a72dc024ba" />

---
## 3. Which product categories receive the lowest ratings?
Helps identify categories that may need quality improvement.
```sql

```
**OUTPUT**

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
