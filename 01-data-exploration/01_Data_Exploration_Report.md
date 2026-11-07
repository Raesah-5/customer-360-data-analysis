# Customer 360 — Data Exploration Report

## 1. Project Overview

### 1.1 Introduction

The Customer 360 project is an end-to-end data analysis project designed to explore customer-related data and uncover patterns in customer behavior, transactions, application usage, customer support, and churn.

This phase focuses on understanding the available datasets, examining their structure, assessing data completeness, exploring data distributions, and identifying potential data quality issues before conducting deeper business analysis.

### 1.2 Objectives

The main objectives of this phase are:

- Understand the structure and characteristics of each dataset.
- Examine data types, missing values, and duplicate records.
- Explore categorical and numerical variables.
- Identify potential outliers and unusual values.
- Examine relationships between datasets.
- Assess referential integrity and key uniqueness.
- Identify inconsistencies that may require further investigation.

### 1.3 Tools & Technologies

- Python
- Pandas
- NumPy
- Jupyter Notebook


---

## 2. Dataset Overview

### 2.1 Available Datasets

The project consists of five datasets containing customer-related information across different business areas.

| Dataset | Number of Records | Description |
|---|---:|---|
| customers.csv | 100,000 | Customer demographic and profile information |
| transactions.csv | 500,000 | Customer transaction records |
| app_usage.csv | 100,000 | Customer application usage and engagement |
| churn.csv | 100,000 | Customer churn status and related information |
| support_tickets.csv | 100,000 | Customer support interactions and satisfaction |

**Total Records:** 800,000

### 2.2 Dataset Granularity

Each dataset represents a different level of detail:

| Dataset | Data Granularity |
|---|---|
| customers | One record per customer |
| transactions | Multiple transaction records per customer |
| app_usage | One record per customer |
| churn | One record per customer |
| support_tickets | Multiple support ticket records per customer |

### 2.3 Key Identifiers

The datasets use identifiers to connect customer information:

- `customer_id`: Common identifier used to link customer-related records across datasets.
- `transaction_id`: Unique identifier for each transaction.
- `ticket_id`: Unique identifier for each support ticket.

The `customer_id` field serves as the primary customer reference across the project datasets.
