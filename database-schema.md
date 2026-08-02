#  Database Schema

This document describes a recommended PostgreSQL schema for storing sales data used by the Sales Intelligence Automation workflow.

The schema is normalized to support KPI calculation, business analytics, AI reporting, and historical sales analysis.

---

# Entity Relationship Overview

```text
Customers
     │
     │
     ▼
Sales Orders
     │
     ├────────────┐
     │            │
     ▼            ▼
Order Items    Products
     │
     ▼
Sales Analytics
```

---

# Database Design Goals

The schema is designed to support:

- Revenue analytics
- Sales KPI generation
- Product performance analysis
- Customer analytics
- Regional analytics
- Historical reporting
- AI-powered business intelligence

---

# Tables

## 1. customers

Stores customer information.

| Column | Type | Description |
|---------|------|-------------|
| id | SERIAL | Primary Key |
| customer_name | VARCHAR(255) | Customer Name |
| email | VARCHAR(255) | Customer Email |
| city | VARCHAR(100) | City |
| country | VARCHAR(100) | Country |
| created_at | TIMESTAMP | Record Creation |

---

## 2. products

Stores the product catalog.

| Column | Type | Description |
|---------|------|-------------|
| id | SERIAL | Primary Key |
| sku | VARCHAR(100) | Product SKU |
| product_name | VARCHAR(255) | Product Name |
| category | VARCHAR(100) | Product Category |
| unit_price | DECIMAL | Selling Price |

---

## 3. sales_orders

Stores sales transactions.

| Column | Type |
|---------|------|
| id | SERIAL |
| order_number | VARCHAR(100) |
| customer_id | INTEGER |
| order_date | DATE |
| total_amount | DECIMAL |
| payment_method | VARCHAR(50) |

---

## 4. order_items

Stores individual products sold within each order.

| Column | Type |
|---------|------|
| id | SERIAL |
| order_id | INTEGER |
| product_id | INTEGER |
| quantity | INTEGER |
| selling_price | DECIMAL |

---

## 5. sales_analytics

Stores generated KPI snapshots.

| Column | Type |
|---------|------|
| id | SERIAL |
| report_date | DATE |
| total_revenue | DECIMAL |
| total_orders | INTEGER |
| average_order_value | DECIMAL |
| generated_at | TIMESTAMP |

---

# Relationships

```text
customers

      │

      └──────── sales_orders

sales_orders

      │

      └──────── order_items

products

      │

      └──────── order_items

sales_orders

      │

      └──────── sales_analytics
```

---

# Database Workflow

```text
Sales Data

↓

Store Orders

↓

Store Products

↓

Generate KPIs

↓

Generate Analytics

↓

AI Sales Analysis

↓

Dashboard

↓

Reports
```

---

# Database Technologies

- PostgreSQL
- SQL
- Foreign Keys
- Indexed Queries
- Aggregate Functions
- Transactions

---

# Design Considerations

- Normalized relational schema
- Referential integrity using foreign keys
- Optimized for KPI aggregation
- Historical reporting support
- AI-ready structured data
- Scalable for future CRM/ERP integrations

---

# Future Enhancements

Potential additions include:

- Sales Targets
- Sales Representatives
- Regional Offices
- Customer Segmentation
- Marketing Campaign Attribution
- Forecasting Tables
- Inventory Correlation
