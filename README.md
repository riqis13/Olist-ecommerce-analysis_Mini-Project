# Olist E-Commerce Data Analysis

This repository contains an exploratory data analysis project using the **Brazilian E-Commerce Public Dataset by Olist**. The analysis focuses on customer behavior, order patterns, seller performance, product categories, payment behavior, delivery performance, and review scores in the Brazilian e-commerce marketplace.

## Dataset

The dataset used in this project is the **Brazilian E-Commerce Public Dataset by Olist**, available on Kaggle:

```text
https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce
```

## Download Dataset

The dataset can be downloaded directly using `kagglehub`.

```python
import kagglehub

# Download latest version
path = kagglehub.dataset_download("olistbr/brazilian-ecommerce")

print("Path to dataset files:", path)
```

After running the code above, KaggleHub will download the dataset and return the local path where the CSV files are stored.

## Project Overview

The goal of this project is to analyze Olist e-commerce transactions by combining multiple relational datasets into a single analytical workflow. The project includes:

- Data loading
- Data cleaning
- Data merging
- Feature preparation
- Exploratory data analysis
- KPI calculation
- Data visualization

## Dataset Files

The Olist dataset consists of several CSV files:

```text
olist_orders_dataset.csv
olist_order_items_dataset.csv
olist_order_payments_dataset.csv
olist_order_reviews_dataset.csv
olist_customers_dataset.csv
olist_sellers_dataset.csv
olist_products_dataset.csv
olist_geolocation_dataset.csv
product_category_name_translation.csv
```

## Data Flow Description

The Olist dataset consists of several tables connected through different ID fields.

```text
olist_order_items_dataset
        |
        |-- order_id   --> olist_orders_dataset
        |                       |
        |                       |-- customer_id --> olist_customers_dataset
        |
        |-- product_id --> olist_products_dataset
        |                       |
        |                       |-- product_category_name --> product_category_name_translation
        |
        |-- seller_id  --> olist_sellers_dataset
        |
        |-- order_id   --> olist_order_payments_dataset
        |
        |-- order_id   --> olist_order_reviews_dataset
```

Location data is added using ZIP code prefixes:

```text
customer_zip_code_prefix --> olist_geolocation_dataset
seller_zip_code_prefix   --> olist_geolocation_dataset
```

Merge strategy:

- The main table starts from `order_items` because each row represents one item in an order.
- `payments` and `reviews` are aggregated by `order_id` to avoid duplicated rows after merging.
- `geolocation` data is aggregated by ZIP code prefix so that location merging does not inflate the number of rows.

## Analysis Objectives

This project aims to answer several analytical questions:

- How many orders, customers, sellers, and products are available in the dataset?
- Which product categories generate the highest revenue?
- Which product categories have the highest sales volume?
- What are the most common payment methods?
- How does delivery time vary across orders?
- How are review scores distributed?
- Which states contribute the most to transactions?
- Is there any relationship between delivery performance and customer review score?
