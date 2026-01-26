## CUSTOMER TABLE

```sql
create table custumers(
custumer_id varchar(100) primary key,
custumerprefix_code int,
custumer_city varchar,
custumer_state varchar(10)
);
```
---
## PRODUCT TABLE

```sql
create table products(
product_id varchar primary key,
product_category_name text
);
```
---
## CATEGORY TABLE

```SQL
create table product_category(
product_name text,
product_name_english text
);
```
---
## ORDER TABLE
```SQL
create table orders(
order_id varchar primary key,
customer_id varchar,
order_status text,
order_purchase timestamp,
order_approved_at timestamp,
order_delivered_carrier_date timestamp,
order_delivered_customer_date timestamp,
order_estimated_delivery_date date,
constraint fk_custumer_id foreign key(custumer_id) references custumers(custumer_id)
);
);
```
---
##  SELLER TABLE
```SQL
create table sellers(
seller_id varchar primary key,
sellerprefix_code int,
seller_city text,
seller_state text
);
```
---
## ORDER ITEM TABLE
```SQL
create table order_items(
order_id varchar,
order_item_id int,
product_id varchar,
seller_id varchar,
shipping_limit_date timestamp,
price numeric(10,3),
freight_value numeric(10,3),
foreign key (order_id) references orders(order_id),
foreign key (product_id) references products(product_id),
foreign key (seller_id) references sellers(seller_id)
);
```
---
## PAYMENT TABLE
```SQL
create table payments(
order_id varchar,
payment_sequential int,
payment_type text,
installments int,
payment_value numeric (10,3),
foreign key (order_id) references orders(order_id)
);
```
---
