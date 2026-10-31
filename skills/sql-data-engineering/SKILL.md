---
name: sql-data-engineering
description: Use when the user needs help writing SQL queries, optimizing database performance, designing schemas, building ETL/ELT pipelines, working with data warehouses, or performing data wrangling with SQL-based tools like BigQuery, PostgreSQL, MySQL, or Snowflake.
---

# SQL & Data Engineering

Write correct, performant, and maintainable SQL. Treat data pipelines as production software.

## 1. Understand the data model

Before writing queries, identify:

- The database engine (PostgreSQL, MySQL, BigQuery, Snowflake, SQLite, Redshift, etc.) — syntax and functions differ.
- Table relationships: primary keys, foreign keys, junction tables, and cardinality (one-to-one, one-to-many, many-to-many).
- Data types and nullability of relevant columns.
- Approximate table sizes to inform optimization decisions.
- Whether the query runs on transactional (OLTP) or analytical (OLAP) storage.

## 2. Query writing standards

- **SELECT only needed columns**. Never use `SELECT *` in production queries.
- **Explicit JOINs**: always use `JOIN ... ON` syntax, never comma-separated implicit joins.
- **NULL handling**: remember that `NULL != NULL`, `NULL NOT IN (...)` returns NULL, and aggregates ignore NULLs. Use `COALESCE`, `NULLIF`, and `IS NULL` / `IS NOT NULL` explicitly.
- **Aggregation**: every non-aggregated column must appear in `GROUP BY`. Use `HAVING` for post-aggregation filters.
- **Window functions**: use `ROW_NUMBER()`, `RANK()`, `LAG()`, `LEAD()`, `SUM() OVER()` for running totals, rankings, and row-level comparisons without self-joins.
- **CTEs over subqueries**: prefer `WITH` (Common Table Expressions) for readability and maintainability. Name CTEs descriptively.
- **Date handling**: use engine-appropriate date functions. Always be explicit about time zones when relevant.
- **String matching**: use `LIKE` for simple patterns, `REGEXP` / `SIMILAR TO` for complex patterns. Be aware of case sensitivity per engine.
- **UNION vs UNION ALL**: use `UNION ALL` unless deduplication is explicitly needed (UNION is slower).

## 3. Query optimization

- **Indexes**: suggest indexes for columns in `WHERE`, `JOIN ON`, `ORDER BY`, and `GROUP BY` clauses. Composite indexes should match query column order (leftmost prefix rule).
- **EXPLAIN / EXPLAIN ANALYZE**: always recommend checking the query plan for slow queries. Look for sequential scans on large tables, nested loop joins on large datasets, and sort operations without indexes.
- **Avoid**: `SELECT DISTINCT` as a fix for incorrect joins, correlated subqueries when a join works, functions on indexed columns in `WHERE` (e.g., `WHERE YEAR(date_col) = 2024` prevents index use — use range instead).
- **Partitioning**: recommend partition pruning strategies for large tables (date-partitioned tables in BigQuery/Snowflake).
- **Materialized views / pre-aggregation**: suggest for expensive, frequently-run analytical queries.

## 4. Schema design

- **Normalization**: explain trade-offs between normalized (3NF) for transactional systems and denormalized / star schema for analytical workloads.
- **Star schema**: fact tables (events, transactions) with dimension tables (users, products, dates). Use surrogate keys.
- **Slowly Changing Dimensions (SCD)**: Type 1 (overwrite), Type 2 (versioned rows with valid_from/valid_to), Type 3 (previous value column).
- **Naming conventions**: lowercase, snake_case, singular table names (e.g., `order_item` not `OrderItems`). Prefix staging tables.
- **Constraints**: primary keys, foreign keys, NOT NULL, CHECK constraints, and unique constraints where data integrity matters.

## 5. ETL / ELT pipeline design

- **Extract**: identify source systems, extraction frequency (batch vs streaming), incremental vs full load, and change data capture (CDC) when available.
- **Transform**: apply cleaning, deduplication, type casting, business logic, and aggregation. Document transformation rules.
- **Load**: choose insert strategy (append, upsert/merge, truncate-and-load) based on the use case and idempotency requirements.
- **Idempotency**: pipelines must produce the same result if re-run. Use `MERGE` / `INSERT ... ON CONFLICT` for upserts. Use partition-level overwrites for date-partitioned tables.
- **Data quality checks**: row counts, null checks, uniqueness, referential integrity, and value range assertions after each pipeline step.
- **Orchestration**: mention Airflow, dbt, Prefect, or Dagster patterns as appropriate. Keep SQL transformations in version control.

## 6. dbt patterns (when applicable)

- **Models**: staging → intermediate → marts layering.
- **Sources**: define sources with freshness checks.
- **Tests**: `unique`, `not_null`, `accepted_values`, `relationships`, and custom tests.
- **Incremental models**: use `is_incremental()` with appropriate unique key and merge strategy.
- **Documentation**: document models and columns in YAML schema files.

## 7. Security and best practices

- **Parameterized queries**: never concatenate user input into SQL strings. Use parameterized queries or ORM-generated queries.
- **Least privilege**: recommend appropriate `GRANT` permissions per role.
- **PII handling**: identify personally identifiable information and recommend masking, hashing, or access controls.
- **Cost awareness**: for cloud warehouses (BigQuery, Snowflake), warn about full table scans, cross-joins, and unbounded queries that may incur high costs.
