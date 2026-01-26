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

