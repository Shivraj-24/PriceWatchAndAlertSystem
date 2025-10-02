# 🛒 PriceWatch Data Engineering Platform

A **Data Engineering + Web App** project integrating **PySpark, AWS, Snowflake, Flask, and Orchestration** to build an end-to-end **price monitoring system**.

---

## 🎯 Project Objective

- Build a **production-like Data Engineering pipeline** for **price monitoring**.
- Users add items to wishlist via **Flask web app**.
- Periodically scrape prices from e-commerce sites (Amazon, Flipkart, Walmart).
- Store raw + processed data in **AWS S3**.
- Transform & clean data using **PySpark**.
- Store curated price history in **Snowflake**.
- Trigger **alerts** when price drops below thresholds.
- Provide **dashboard** to view price trends & comparisons.

---

## ✅ Things Implemented

1. **Web Scraping Layer**
   - Multi-site scrapers with configurable product specs
   - Raw JSON storage in S3

2. **Data Lake & ETL (PySpark)**
   - Cleaning, deduplication, normalization
   - Partitioned price history storage

3. **Data Warehouse (Snowflake)**
   - Tables: `wishlist`, `price_history`, `alerts`
   - Automated ingestion (Snowpipe)
   - Analytics queries for trends & lowest price detection

4. **Alerts & Notifications**
   - AWS SES for email notifications
   - Threshold-based triggers

5. **Web Application (Flask)**
   - User login & wishlist management
   - Dashboard with price trends and comparisons

6. **Orchestration**
   - Airflow DAG: `scrape → S3 → PySpark → Snowflake → Alert`
   - Cron jobs for quick experiments

7. **Deployment**
   - Dockerized application
   - EC2 deployment

---

## 📚 Fundamentals to Learn First (Phase 0)

### 1. Python & Web Scraping
- Python OOP, error handling, logging
- Requests, BeautifulSoup, Selenium
- Async scraping concepts

### 2. PySpark Basics & Environment Setup
- Install Spark locally or use AWS Glue/EMR
- DataFrames & RDDs
- Transformations, actions, aggregations, joins
- Window functions & partitioning
- Reading/Writing CSV, JSON, Parquet
- Spark optimizations (caching, broadcast joins)

### 3. Snowflake Fundamentals
- Create databases, schemas, warehouses
- Tables, Views, Materialized Views
- Loading data (Snowpipe/COPY INTO)
- Streams, Tasks, Time Travel

### 4. AWS Essentials
- S3 buckets for raw/processed storage
- IAM roles & permissions
- EC2, Lambda, Step Functions, SES basics

### 5. Flask Basics
- Routes, templates, forms
- REST APIs and session management

### 6. Tools & DevOps
- Git & GitHub
- Docker for containerization
- Linux terminal commands

✅ **Extended Learning**
- Set up PySpark environment locally and on cloud (EMR/Glue)
- Explore PySpark MLlib basics for optional ML add-ons

---

## 🏗 Architecture Diagram

```mermaid
flowchart LR
  U[User - Wishlist Input via Flask] --> SC[Scrapers - Amazon, Flipkart, Walmart]
  SC --> S3[(AWS S3 - Raw JSON Data Lake)]
  S3 --> GLUE[PySpark ETL - AWS Glue/EMR]
  GLUE --> SNOW[(Snowflake Data Warehouse)]
  SNOW --> ADMIN[Admin Dashboard - Price Trends]
  SNOW --> ALERT[AWS SES - Email Alerts]
  U --> SNOW
  ORCH[Airflow / Step Functions] --> SC
  ORCH --> GLUE
  ORCH --> SNOW
  ORCH --> ALERT
