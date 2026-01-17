# 🛒 ETL Pipeline & Web Scraping - E-commerce Data

![Python](https://img.shields.io/badge/Python-3.10-blue?style=for-the-badge&logo=python)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas)
![BeautifulSoup](https://img.shields.io/badge/BeautifulSoup-Scraping-yellow?style=for-the-badge)

## 📌 Overview

This project consists of an **ETL (Extract, Transform, Load)** pipeline developed to process raw HTML data from a fictional e-commerce site. The objective is to structure unorganized information, apply business rules for pricing, and standardize data for further analysis.

The project simulates a real-world scenario where data is extracted from the front-end or a crawler and needs to be cleaned before being stored.

---

## ⚙️ Pipeline Architecture

The process was divided into three classic data engineering stages:

### 1. Extraction (Extract)
Using the **BeautifulSoup** library, the script parses the raw HTML (`HTML_DATA`).
* **Integrity Filter:** A strict rule was implemented where products without a price tag (`<p class="price">`) are identified and immediately **discarded**, generating an alert log.
* **Collection:** Extraction of ID, Name, Raw Price, Rating, Image, Date, and Discount.

### 2. Transformation (Transform)
With the extracted data, **Pandas** and **Regex** are used for cleaning and typing:
* **String Cleaning:** Removal of currency symbols (`R$`) and percentage signs (`% OFF`).
* **Type Conversion:** Transformation of prices and discounts into `float`.
* **Rating Normalization:** Conversion of the "x/5.0" scale to a percentage scale (0-100).
* **Date Standardization:** Changing the format from `dd/mm/yyyy` to `dd-mm-yyyy`.
* **Business Rule:** Creation of the calculated `net_price` field, applying the discount to the original value.

### 3. Loading (Load)
The processed and structured data is exported to a CSV file (`calculated_offers.csv`), ready to be consumed by BI tools or other systems.

---

## 📊 Results

From unstructured HTML, the pipeline generated the following clean tabular structure:

| name | numerical_price | discount_percentage | net_price | rating_percentage | date |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Smartphone X10 | 1999.99 | 10.0 | 1799.99 | 90.0 | 27-11-2025 |
| Notebook Ultraline | 4500.00 | 0.0 | 4500.00 | 96.0 | 28-11-2025 |
| Bluetooth Pro Headphones | 549.50 | 5.0 | 522.02 | 78.0 | 28-11-2025 |
| Smartwatch Z | 1250.00 | 20.0 | 1000.00 | 100.0 | 27-11-2025 |

---

### 👨‍💻 Author

**Alexander Lira** Data Analyst | Python | Data Engineering
