# SQL Date & Time Functions

Date functions allow you to manipulate, filter, group, and calculate dates and timestamps.

They are extremely common in SQL interviews because businesses frequently analyze trends over time, such as monthly revenue, customer retention, and delivery performance.

> **Note:** Some date functions vary slightly between SQL dialects (PostgreSQL, MySQL, SQL Server, Snowflake, etc.). The examples below use PostgreSQL syntax unless otherwise noted.

## Topics

- [Working with Dates](#working-with-dates)
- [CURRENT_DATE & CURRENT_TIMESTAMP](#current_date--current_timestamp)
- [EXTRACT()](#extract)
- [DATE_TRUNC()](#date_trunc)
- [DATE_PART()](#date_part)
- [AGE()](#age)
- [DATE Arithmetic](#date-arithmetic)
- [Filtering Date Ranges](#filtering-date-ranges)
- [DATEDIFF()](#datediff)
- [Common Interview Patterns](#common-interview-patterns)
- [Common Interview Mistakes](#common-interview-mistakes)

---

# Working with Dates

Dates are stored using date or timestamp data types.

Example

| order_id | order_date |
|----------|------------|
|101|2024-01-15|
|102|2024-02-08|
|103|2024-02-21|

Timestamps include the time.

| shipment_id | shipped_at |
|-------------|------------|
|1|2024-08-01 14:25:33|

---

# CURRENT_DATE & CURRENT_TIMESTAMP

## What are they?

Return today's date or the current date and time.

### Example

```sql
SELECT CURRENT_DATE;
```

Output

```text
2026-07-16
```

Current timestamp

```sql
SELECT CURRENT_TIMESTAMP;
```

Output

```text
2026-07-16 15:32:10
```

### Use when

- Calculating age
- Rolling time windows
- Comparing against today's date

---

# EXTRACT()

## What is it?

Extracts a specific part of a date.

### Syntax

```sql
EXTRACT(part FROM date_column)
```

### Example

```sql
SELECT

order_date,

EXTRACT(YEAR FROM order_date) AS year,

EXTRACT(MONTH FROM order_date) AS month,

EXTRACT(DAY FROM order_date) AS day

FROM orders;
```

Output

| order_date | year | month | day |
|------------|------|-------|-----|
|2024-08-15|2024|8|15|

Common parts

- YEAR
- MONTH
- DAY
- WEEK
- QUARTER
- DOW (day of week)
- DOY (day of year)
- HOUR
- MINUTE

---

# DATE_TRUNC()

## What is it?

Rounds a timestamp down to a specified time period.

Useful for grouping.

### Example

Monthly sales

```sql
SELECT

DATE_TRUNC('month', order_date) AS month,

SUM(amount)

FROM orders

GROUP BY month

ORDER BY month;
```

Output

| month | revenue |
|--------|---------|
|2024-01-01|5200|
|2024-02-01|6100|

Other intervals

```sql
DATE_TRUNC('year', order_date)

DATE_TRUNC('quarter', order_date)

DATE_TRUNC('week', order_date)

DATE_TRUNC('day', order_date)
```

### Use when

- Monthly reports
- Weekly reports
- Quarterly revenue
- Time-series charts

---

# DATE_PART()

Returns a specific part of a date.

Similar to EXTRACT.

Example

```sql
SELECT

DATE_PART('month', order_date)

FROM orders;
```

Equivalent to

```sql
EXTRACT(MONTH FROM order_date)
```

---

# AGE()

## What is it?

Calculates the difference between two dates.

Example

```sql
SELECT

AGE(CURRENT_DATE, birth_date)

FROM employees;
```

Output

```text
28 years 3 mons
```

Useful for

- Employee age
- Customer tenure
- Membership duration

---

# Date Arithmetic

SQL can add or subtract dates.

Example

Tomorrow

```sql
SELECT CURRENT_DATE + INTERVAL '1 day';
```

Yesterday

```sql
SELECT CURRENT_DATE - INTERVAL '1 day';
```

One month later

```sql
SELECT CURRENT_DATE + INTERVAL '1 month';
```

Thirty days ago

```sql
SELECT CURRENT_DATE - INTERVAL '30 days';
```

---

# Filtering Date Ranges

Very common interview topic.

Example

Orders in August

```sql
SELECT *

FROM orders

WHERE order_date

BETWEEN '2024-08-01'

AND '2024-08-31';
```

Better for timestamps

```sql
SELECT *

FROM shipments

WHERE shipped_at >= '2024-08-01'

AND shipped_at < '2024-09-01';
```

Using half-open ranges avoids accidentally excluding rows later in the day on August 31.

---

# DATEDIFF()

## What is it?

Returns the difference between two dates.

Available in SQL Server, Snowflake, BigQuery, etc.

Example

```sql
SELECT

DATEDIFF(day,

order_date,

ship_date)

FROM orders;
```

Output

| days_to_ship |
|--------------|
|3|
|5|
|1|

### PostgreSQL equivalent

```sql
SELECT

ship_date - order_date

FROM orders;
```

---

# Common Interview Patterns

## Monthly Revenue

```sql
SELECT

DATE_TRUNC('month', order_date) AS month,

SUM(amount)

FROM orders

GROUP BY month;
```

---

## Orders This Year

```sql
SELECT *

FROM orders

WHERE EXTRACT(YEAR FROM order_date)

=

2024;
```

---

## Delivery Time

```sql
SELECT

delivered_at - shipped_at

AS delivery_time

FROM shipments;
```

---

## Customer Tenure

```sql
SELECT

customer_name,

AGE(CURRENT_DATE,

signup_date)

FROM customers;
```

---

## Orders in Last 30 Days

```sql
SELECT *

FROM orders

WHERE order_date >= CURRENT_DATE - INTERVAL '30 days';
```

---

# Common Interview Mistakes

## Comparing timestamps to dates

Incorrect

```sql
WHERE shipped_at = '2024-08-01'
```

This only matches midnight.

Better

```sql
WHERE shipped_at >= '2024-08-01'

AND shipped_at < '2024-08-02'
```

---

## Using BETWEEN with timestamps

```sql
BETWEEN '2024-08-01'

AND '2024-08-31'
```

May exclude timestamps later on August 31.

Prefer

```sql
>=

AND

<
```

---

## Forgetting DATE_TRUNC()

Grouping directly by timestamps

```sql
GROUP BY shipped_at
```

Usually creates one group per timestamp.

Instead

```sql
GROUP BY DATE_TRUNC('month', shipped_at)
```

---

## Hardcoding today's date

Instead of

```sql
WHERE order_date > '2026-07-01'
```

Use

```sql
WHERE order_date >= CURRENT_DATE - INTERVAL '30 days'
```

---

# Interview Tips

- Memorize `EXTRACT()` and `DATE_TRUNC()`. They appear in many interview questions.
- Use `DATE_TRUNC()` when grouping by weeks, months, or years.
- Use `EXTRACT()` when filtering by parts of a date.
- Prefer half-open ranges (`>=` and `<`) for timestamp filtering.
- Learn the date functions used by your target SQL dialect (PostgreSQL, MySQL, SQL Server, Snowflake, BigQuery).
- Many business metrics—monthly revenue, retention, churn, and delivery performance—depend on strong date handling skills.
