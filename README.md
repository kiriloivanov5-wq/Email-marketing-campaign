# Email Marketing Campaigns & User Engagement SQL Analysis

## 📌 Project Overview
This project focuses on building an End-to-End Analytics Pipeline to evaluate user registration activity alongside email marketing performance. Using **Google BigQuery (SQL)**, the analysis aggregates key account metrics, tracks email delivery, open rates, and click/visit events, and ranks top-performing geographic regions using advanced SQL window functions.
* [Processed Output & Dataset](https://docs.google.com/spreadsheets/d/1aSqvzqGQFtwHmsP-mI0eLRBsADJ6-W514JdT7F7nvXQ/edit?usp=sharing)

---

## 🛠️ Tech Stack & Advanced SQL Concepts
* **Query Engine:** Google BigQuery (SQL)
* **Data Pipelines & Modeling:** Multi-stage Common Table Expressions (CTEs), `UNION DISTINCT` for metrics consolidation.
* **Date & Time Operations:** `DATE_ADD`, `INTERVAL` logic for temporal alignment.
* **Window Functions & Ranking:** `SUM() OVER(PARTITION BY ...)`, `DENSE_RANK() OVER(...)`.
* **Advanced Filtering:** `QUALIFY` clause for filtering windowed ranking results directly.

---

## 📊 Data Architecture & Query Pipeline Workflow
The SQL query processes data through a structured multi-stage CTE pipeline:

1. **`accounts` CTE:** Aggregates total distinct registered accounts grouped by acquisition date, country, send interval, verification, and subscription status.
2. **`emails` CTE:** Calculates email delivery metrics (`sent_msg`, `open_msg`, `visit_msg`) linked to account sessions and messaging events, with target date normalization (`DATE_ADD`).
3. **`unions` & `unions2` CTEs:** Consolidates account registration data and email activity metrics into a unified grain, aggregating total counts across user dimensions.
4. **`total` CTE & Final Output:** Applies window partitions (`PARTITION BY country`) to calculate overall country-level volumes and ranks the Top-10 countries by account volume and email engagement using `QUALIFY DENSE_RANK() <= 10`.

---

## 🔍 Key Business Metrics Calculated
* **Account Acquisition Volume:** Total distinct accounts created per segment/country.
* **Email Campaign Funnel:** Sent Emails ➔ Opened Emails ➔ Site Visits / Conversions.
* **Geographical Ranking:** Top 10 performing countries based on user density and campaign outreach.

---

## 📁 Repository Structure
* `/scripts` — Contains structured `.sql` code files (`email_engagement_pipeline.sql`).
* `README.md` — Project documentation and pipeline description.
