# Olist E-Commerce Data Analysis

This repository contains an exploratory data analysis project using the **Brazilian E-Commerce Public Dataset by Olist**. The project analyzes customer behavior, order patterns, seller performance, product categories, payment behavior, delivery performance, and review scores in the Brazilian e-commerce marketplace.

## Dataset

The dataset used in this project is the **Brazilian E-Commerce Public Dataset by Olist**, available on Kaggle.

Dataset source:

```text
https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce
```

The dataset contains information on approximately 100,000 orders made from 2016 to 2018 in Brazil. It includes order status, price, payment, freight performance, customer location, product attributes, seller information, and customer reviews.

The dataset is anonymized and publicly available for non-commercial use under the **Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License (CC BY-NC-SA 4.0)**.

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

The main objective of this project is to perform exploratory data analysis on Olist e-commerce transaction data by combining multiple relational datasets into a single analytical workflow.

This project includes:

- Data loading
- Data inspection
- Data cleaning
- Data merging
- Feature preparation
- Exploratory data analysis
- KPI calculation
- Data visualization
- Business insight generation

## Dataset Files

The Olist dataset consists of 9 CSV files:

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
- Which sellers generate the highest sales?
- Is there any relationship between delivery performance and customer review score?
- What business insights can be derived from the Olist marketplace data?

## Requirements

The main libraries used in this project are:

```text
pandas
numpy
matplotlib
seaborn
jupyter
kagglehub
```

## How to Run the Project

Open the notebook:

```text
notebooks/olist_ecommerce_analysis.ipynb
```

Then run all cells from top to bottom.

The dataset will be downloaded using KaggleHub with the following code:

```python
import kagglehub

# Download latest version
path = kagglehub.dataset_download("olistbr/brazilian-ecommerce")

print("Path to dataset files:", path)
```

After the dataset path is returned, the CSV files can be loaded using Pandas.

Example:

```python
import os
import pandas as pd

orders = pd.read_csv(os.path.join(path, "olist_orders_dataset.csv"))
order_items = pd.read_csv(os.path.join(path, "olist_order_items_dataset.csv"))
payments = pd.read_csv(os.path.join(path, "olist_order_payments_dataset.csv"))
reviews = pd.read_csv(os.path.join(path, "olist_order_reviews_dataset.csv"))
customers = pd.read_csv(os.path.join(path, "olist_customers_dataset.csv"))
sellers = pd.read_csv(os.path.join(path, "olist_sellers_dataset.csv"))
products = pd.read_csv(os.path.join(path, "olist_products_dataset.csv"))
geolocation = pd.read_csv(os.path.join(path, "olist_geolocation_dataset.csv"))
category_translation = pd.read_csv(os.path.join(path, "product_category_name_translation.csv"))
```

## Main Analysis Steps

The analysis workflow follows these steps:

1. Download the dataset using KaggleHub.
2. Load all CSV files into Pandas DataFrames.
3. Inspect the structure, columns, and missing values of each table.
4. Aggregate payment and review data by `order_id`.
5. Aggregate geolocation data by ZIP code prefix.
6. Merge order item data with orders, customers, products, sellers, payments, reviews, and location data.
7. Create additional features such as delivery time and estimated delivery delay.
8. Calculate key performance indicators.
9. Visualize sales, order distribution, payment methods, product categories, and review scores.
10. Generate insights from the analysis.

## Key Metrics

Some key metrics analyzed in this project include:

- Total orders
- Total customers
- Total sellers
- Total products
- Total revenue
- Average order value
- Average freight value
- Average review score
- Average delivery time
- Top product categories by revenue
- Top states by number of orders
- Payment method distribution

## Tools and Libraries

This project uses:

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Jupyter Notebook
- KaggleHub

## Output

The analysis produces summary tables, visualizations, and processed results. Generated outputs can be stored in:

```text
outputs/
```

## Notes

The raw dataset files are not included directly in this repository because they are available from Kaggle and are subject to Kaggle/Olist dataset licensing terms.

Users should download the dataset directly from Kaggle using KaggleHub or from the Kaggle dataset page.

## Dataset License

The dataset used in this project is licensed under:

```text
Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International
CC BY-NC-SA 4.0
```

This means the dataset can be used under the following conditions:

- **Attribution**: Credit must be given to the original dataset provider.
- **NonCommercial**: The dataset cannot be used for commercial purposes.
- **ShareAlike**: Any derivative work based on the dataset should be shared under the same license.

Dataset source:

```text
https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce
```

## Repository License

This repository does not include the raw dataset files. The dataset remains under the original Kaggle/Olist license: **CC BY-NC-SA 4.0**.

Unless otherwise stated, this repository is intended for educational and non-commercial data analysis purposes.

## Acknowledgements

Thanks to Olist and Kaggle for providing the Brazilian E-Commerce Public Dataset.
