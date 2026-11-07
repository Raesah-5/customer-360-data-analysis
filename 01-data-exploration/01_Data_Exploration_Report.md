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


---

## 3. Data Structure & Completeness

### 3.1 Data Types

The datasets were inspected to understand the data types of their columns and ensure that each variable is represented appropriately.

The inspection covered:

- Numerical variables.
- Categorical variables.
- Date and time variables.
- Identifier columns.

### 3.2 Missing Values

All five datasets were checked for missing values.

**Finding:** No missing values were identified in the inspected datasets.

### 3.3 Duplicate Records

The datasets were examined for exact duplicate rows.

**Finding:** No exact duplicate records were identified in any of the five datasets.

### 3.4 Key Uniqueness

Primary identifier uniqueness was examined to understand the structure of each dataset.

| Dataset | Identifier | Unique Records | Result |
|---|---|---:|---|
| customers | customer_id | 100,000 | Pass |
| transactions | transaction_id | 500,000 | Pass |
| app_usage | customer_id | 100,000 | Pass |
| churn | customer_id | 100,000 | Pass |
| support_tickets | ticket_id | 100,000 | Pass |

### 3.5 Repeated Customer Records

Repeated `customer_id` values were identified in datasets containing multiple records per customer.

| Dataset | Unique Customers | Repeated Customer Records |
|---|---:|---:|
| transactions | 99,285 | 400,715 |
| support_tickets | 63,277 | 36,723 |

These repeated customer references are expected based on the dataset granularity and do not represent exact duplicate records.

---

## 4. Categorical Data Exploration

### 4.1 Customer Profile

The customer dataset was explored to understand the distribution of demographic and profile-related attributes.

**Gender Distribution**

| Gender | Number of Customers |
|---|---:|
| Male | 50,120 |
| Female | 49,880 |

**Income Categories**

Income category labels were reviewed for consistency and normalized.

| Income Category | Number of Customers |
|---|---:|
| Low | 33,423 |
| Medium | 33,017 |
| High | 33,560 |

**Customer Locations**

| Location | Number of Customers |
|---|---:|
| Mumbai | 16,859 |
| Bangalore | 16,669 |
| Chennai | 16,668 |
| Hyderabad | 16,634 |
| Kolkata | 16,603 |
| Delhi | 16,567 |

### 4.2 Transaction Categories

Transaction records were examined to understand the distribution of purchase categories and payment methods.

**Transaction Categories**

| Category | Number of Transactions |
|---|---:|
| Clothing | 100,173 |
| Groceries | 100,050 |
| Health | 99,998 |
| Electronics | 99,915 |
| Travel | 99,864 |

**Payment Methods**

| Payment Method | Number of Transactions |
|---|---:|
| Net Banking | 125,407 |
| Wallet | 125,092 |
| UPI | 125,040 |
| Card | 124,461 |

### 4.3 Churn Distribution

The churn dataset was examined to understand the distribution of customer churn status.

| Churn Status | Number of Customers |
|---|---:|
| 0 (Not Churned) | 77,673 |
| 1 (Churned) | 22,327 |

**Churn Reasons**

| Churn Reason | Number of Records |
|---|---:|
| Price | 25,182 |
| Bad Experience | 24,966 |
| Competitor | 24,943 |
| Low Engagement | 24,909 |

**Observation:** Churn reasons are recorded for both churned and non-churned customers. This requires business clarification before interpreting the reason counts as churn-specific.

---

### 4.4 Support Ticket Categories

Support ticket records were explored to understand the distribution of reported issue types.

| Issue Type | Number of Tickets |
|---|---:|
| Technical | 20,148 |
| Other | 20,143 |
| Payment | 19,935 |
| Refund | 19,890 |
| Delivery | 19,884 |

---

## 5. Numerical Data Exploration

### 5.1 Customer Age

The customer age variable was examined to understand its range and distribution.

- Minimum age: 18
- Maximum age: 69

All observed ages fall within the identified range.

### 5.2 Transaction Amounts

Transaction amounts were explored using descriptive statistics.

| Metric | Value |
|---|---:|
| Mean | 1,998.846 |
| Median | 1,385.92 |
| Minimum | 0 |
| Maximum | 24,176.67 |
| 99th Percentile | 9,215.895 |

**Initial Observations:**

- One transaction has an amount of zero.
- No negative transaction amounts were identified.
- The mean is higher than the median, indicating a right-skewed distribution.
- Some transaction amounts are considerably higher than the typical values.

### 5.3 Outlier Detection

The Interquartile Range (IQR) method was applied to identify potential high-value outliers.

| Metric | Value |
|---|---:|
| IQR Upper Bound | 6,061.311 |
| Values Above IQR Upper Bound | 24,188 |
| Values Above 99th Percentile | 5,000 |

These values represent potential outliers that may require further investigation. They should not automatically be considered incorrect or removed without additional business context.

### 5.4 App Usage Metrics

The application usage dataset was examined to understand customer engagement patterns.

| Metric | Mean | Minimum | Maximum |
|---|---:|---:|---:|
| Daily Sessions | 3.00 | 0 | — |
| Average Session Time | 20.47 | 1 | 40 |
| Features Used | 7.50 | 1 | 14 |
| Days Since Last Login | 29.41 | 0 | — |

Additional observations:

- 4,934 records have zero daily sessions.
- 1,701 records have zero days since last login.

### 5.5 Support Ticket Metrics

Numerical support-related variables were examined.

| Metric | Mean | Minimum | Maximum |
|---|---:|---:|---:|
| Resolution Time | 60.07 | 1 | 119 |

Customer satisfaction scores range from 1 to 5.

### 5.6 Initial Observations

- Transaction amounts show a difference between the mean and median.
- Potential high-value outliers were identified using statistical methods.
- Some customers have zero recorded daily sessions.
- Support resolution times vary across records.
- The units and business definitions of some numerical variables require clarification.

**Note:** Numerical findings describe the observed data. Potential anomalies require business context before any correction or removal is considered.

---

## 6. Data Relationships & Referential Integrity

### 6.1 Customer-Based Relationships

The five datasets were examined to understand how customer records are connected.

The `customer_id` column was used as the common identifier across the datasets.

The following relationship structure was identified:

| Dataset | Relationship with Customers |
|---|---|
| customers | One record per customer |
| transactions | One-to-many |
| app_usage | One-to-one |
| churn | One-to-one |
| support_tickets | One-to-many |

### 6.2 Referential Integrity Checks

Referential integrity checks were performed to identify records containing customer IDs that do not exist in the customers dataset.

**Finding:** No orphan customer records were identified in any of the four related datasets.

| Dataset | Orphan Records | Result |
|---|---:|---|
| transactions | 0 | Pass |
| app_usage | 0 | Pass |
| churn | 0 | Pass |
| support_tickets | 0 | Pass |

### 6.3 Relationship Validation

The relationship checks confirmed that:

- All customer references exist in the customers dataset.
- Transactions and support tickets contain multiple records for some customers.
- App usage and churn datasets contain one record per customer.
- The customer identifier can be used to connect the datasets for further analysis.

### 6.4 Conclusion

The datasets have valid customer references based on the checks performed. Their relationship structure provides a foundation for combining customer information and conducting further analysis in the next project phase.

---

## 7. Chronological Data Consistency

### 7.1 Transaction Dates vs. Customer Signup Dates

Transaction dates were compared with customer signup dates to identify transactions that occurred before the corresponding customer registration date.

**Finding:** A total of 218,693 transactions (43.74% of all transaction records) were dated before the associated customer signup date.

### 7.2 Time Difference Analysis

The time difference between transaction dates and signup dates was examined.

| Metric | Value |
|---|---:|
| Records Before Signup | 218,693 |
| Percentage of Transactions | 43.74% |
| Mean Time Difference | 853.83 days |
| Median Time Difference | 751 days |

### 7.3 Observation

The identified records indicate a chronological inconsistency between transaction dates and customer signup dates.

However, the available data does not establish the reason for this inconsistency.

### 7.4 Recommended Investigation

Further investigation is required to clarify:

- Whether the signup date represents the customer's original registration date.
- Whether historical transactions were imported from another system.
- Whether the transaction and signup dates follow different business definitions.
- Whether any date transformation or data integration issue occurred.

**Important:** The original date values should be preserved until the underlying business rules and data sources are clarified. These records should not be automatically deleted or modified.

---

## 8. Text & Categorical Consistency Checks

### 8.1 Text Consistency

Text-based columns were examined for inconsistent formatting and variations in text values.

The review focused on identifying differences in spelling, capitalization, and categorical labels.

### 8.2 Identified Inconsistencies

The following inconsistencies were identified during the exploration process:

| Dataset | Column | Original Value | Standardized Value |
|---|---|---|---|
| customers | income_category | LOW | Low |
| customers | location | Chennal | Chennai |

These variations were standardized to maintain consistent categorical values during analysis.

### 8.3 Categorical Value Consistency

Categorical columns were reviewed to identify inconsistent labels and unexpected variations.

The review covered customer attributes, transaction categories, payment methods, churn-related fields, and support issue types.

### 8.4 Additional Observation

The `churn_reason` column contains values for both churned and non-churned customers.

This requires clarification of the business definition of the column and whether churn reasons are expected to be recorded only for customers with a churn status of 1.

### 8.5 Conclusion

Text and categorical consistency checks helped identify variations that could affect grouping, filtering, and reporting.

Standardizing inconsistent labels improves consistency and supports more reliable analysis.

---

## 9. Key Findings

The exploration phase revealed several important findings across the five datasets:

1. **Dataset Completeness:** No missing values or exact duplicate records were identified.
2. **Customer Relationships:** All customer references passed the referential integrity checks.
3. **Customer Distribution:** Gender, income categories, and customer locations have relatively balanced distributions.
4. **Churn:** A total of 22,327 customers (22.327%) are marked as churned.
5. **Transaction Amounts:** Potential high-value outliers were identified and require further investigation.
6. **Customer Engagement:** Some customers have zero recorded daily sessions.
7. **Chronological Inconsistency:** 218,693 transactions (43.74%) occurred before the associated customer signup dates.
8. **Categorical Consistency:** Inconsistent labels were identified and standardized.
9. **Churn Reason:** The presence of churn reasons for non-churned customers requires business clarification.

---

## 10. Limitations & Recommendations

### 10.1 Limitations

Several observations require additional business context before further conclusions can be drawn:

- The currency used for transaction amounts has not been specified.
- The unit of measurement for average session time is not confirmed.
- The unit of measurement for support resolution time is not confirmed.
- The business definition of the customer satisfaction scale (1–5) requires clarification.
- The reason for transactions occurring before signup dates is unknown.
- The `churn_reason` field contains values for both churned and non-churned customers.
- Potential transaction outliers require business validation.

### 10.2 Recommendations

Based on the exploration findings, the following actions are recommended:

1. Confirm business definitions and units for numerical variables.
2. Investigate transactions recorded before customer signup dates.
3. Validate the expected relationship between churn status and churn reasons.
4. Review potential transaction outliers with business stakeholders.
5. Preserve original data values until validation rules are confirmed.
6. Use the validated dataset relationships as a foundation for deeper analysis.

---

## 11. Phase 1 Conclusion

Phase 1 established an understanding of the five Customer 360 datasets through data exploration and profiling.

The work covered dataset structures, data types, completeness, duplicates, categorical and numerical distributions, outlier detection, dataset relationships, date consistency, and text standardization.

The exploration identified several important observations requiring further investigation, particularly transactions recorded before signup dates, potential transaction outliers, and unclear business definitions.

The findings documented in this phase provide a foundation for the next stage of the project.

**Next Phase:** Phase 2 — Business Questions & Data Analysis.

