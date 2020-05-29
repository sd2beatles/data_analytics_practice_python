```sql
-- drop table if exists olist_order_reviews_dataset,olist_orders_dataset,olist_order_payement_dataset
--                      ,olist_order_customer_datset,olist_order_items_dataset,olist_products_dataset. 
-- 					 seller_dataset;
create table olist_order_reviews_dataset(
  review_id varchar,
  order_id varchar,
  review_score int,
  review_comment_title varchar,
  review_comment_message varchar,
  review_creation_date varchar,
  review_answer_timestamp varchar); 

create table olist_orders_dataset
(
  customer_id varchar,
  order_status varchar,
  order_purchase_timestamp varchar,
  order_approved_at varchar,
  order_delivered_carrier_data varchar,
  order_delivered_customer_date varchar,
  order_estimated_delivery_date varchar
);

create table olist_order_payement_dataset 
(
 order_id varchar,
 payment_sequential int,
 payment_type varchar,
 payment_installments int,
 payment_value real
);

create table olist_order_customer_dataset
(
  customer_id varchar,
  customer_unique_id varchar,
  customer_zip_code int,
  customer_city varchar,
  customer_state varchar
);

create table olist_order_items_dataset
(
 order_id varchar,
 order_items_id varchar,
 product_id varchar,
 seller_id varchar,
 shipping_limit varchar,
 price real,
 freight_value real
);

create table olist_products_dataset
(
 product_id varchar,
 product_category_name varchar,
 product_name_length int,
 product_description_length int,
 product_photos_qty int,
 product_weigth_g int,
 product_length_cm int,
 product_height_cm int,
 product_width_cm int
);

create table seller_dataset(
 seller_id varchar,
	    seller_zip int,
	    seller_city varchar,
	    seller_state varchar
);

create table olist_geolocation_dataset(
 seller_zip int,
	    lati real,
	    lng  real,
	    seller_city varchar,
        seller_state varchar
);




```
