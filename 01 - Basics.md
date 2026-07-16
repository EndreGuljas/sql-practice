# SQL Basics

This section covers the core SQL concepts used to retrieve, filter, sort, group, and summarize data.

## Topics

### Retrieving and filtering data

- [SELECT](SELECT.md)
- [DISTINCT](DISTINCT.md)
- [WHERE](WHERE.md)
- [ORDER BY](ORDER-BY.md)
- [LIMIT](LIMIT.md)

### Conditional filtering

- [CASE](CASE.md)
- [LIKE](LIKE.md)
- [IN](IN.md)
- [BETWEEN](BETWEEN.md)

### Aggregation

- [Aggregate Functions](AGGREGATE-FUNCTIONS.md)
- [GROUP BY](GROUP-BY.md)
- [HAVING](HAVING.md)

### NULL handling

- [NULL](NULL.md)
- [COALESCE](COALESCE.md)
- [NULLIF](NULLIF.md)

## General SQL query structure

```sql
SELECT column_name
FROM table_name
WHERE condition
GROUP BY column_name
HAVING aggregate_condition
ORDER BY column_name
LIMIT number_of_rows;
```

> [!IMPORTANT]
> SQL is written in one order but logically processed in another.

A simplified logical execution order is:

1. `FROM`
2. `WHERE`
3. `GROUP BY`
4. `HAVING`
5. `SELECT`
6. `DISTINCT`
7. `ORDER BY`
8. `LIMIT`

# SELECT

## What is it?

`SELECT` retrieves columns from a table.

You can select one column, several columns, calculated values, or every column in the table.

## Syntax

```sql
SELECT column_1, column_2
FROM table_name;
```

## Example table

### `customers`

| customer_id | customer_name | city |
|---:|---|---|
| 1 | Alice | Toronto |
| 2 | Bob | Montreal |
| 3 | Carol | Toronto |

## Example

```sql
SELECT
    customer_id,
    customer_name
FROM customers;
```

## Output

| customer_id | customer_name |
|---:|---|
| 1 | Alice |
| 2 | Bob |
| 3 | Carol |

## Selecting every column

```sql
SELECT *
FROM customers;
```

> [!TIP]
> `SELECT *` is useful when exploring a table, but selecting only the required columns is usually better in production queries.

## Creating a calculated column

```sql
SELECT
    shipment_id,
    cost,
    cost * 1.13 AS cost_with_tax
FROM shipments;
```

## Key points

- Separate selected columns with commas.
- Use `AS` to give a column an alias.
- SQL calculations can be included inside `SELECT`.
- Aliases make output easier to understand.

  # DISTINCT

## What is it?

`DISTINCT` removes duplicate rows from a query result.

It applies to the complete combination of columns listed after `SELECT`.

## Syntax

```sql
SELECT DISTINCT column_name
FROM table_name;
```

## Example table

### `shipments`

| shipment_id | carrier |
|---:|---|
| 101 | UPS |
| 102 | FedEx |
| 103 | UPS |
| 104 | DHL |

## Example

```sql
SELECT DISTINCT carrier
FROM shipments;
```

## Output

| carrier |
|---|
| UPS |
| FedEx |
| DHL |

## DISTINCT with multiple columns

```sql
SELECT DISTINCT
    customer_id,
    carrier
FROM customer_shipments;
```

This returns each unique `customer_id` and `carrier` combination.

> [!IMPORTANT]
> `DISTINCT` does not independently remove duplicates from each column. It removes duplicate combinations of all selected columns.

## Counting distinct values

```sql
SELECT COUNT(DISTINCT carrier) AS carrier_count
FROM shipments;
```

## Key points

- Use `DISTINCT` when you need unique values.
- It applies to the entire selected row.
- Avoid using it simply to hide duplicates caused by an incorrect join.

# WHERE

## What is it?

`WHERE` filters individual rows before grouping and aggregation occur.

Only rows that satisfy the condition are returned.

## Syntax

```sql
SELECT column_name
FROM table_name
WHERE condition;
```

## Example table

### `shipments`

| shipment_id | carrier | cost |
|---:|---|---:|
| 101 | UPS | 20.00 |
| 102 | FedEx | 35.00 |
| 103 | DHL | 15.00 |

## Example

```sql
SELECT
    shipment_id,
    carrier,
    cost
FROM shipments
WHERE cost > 20;
```

## Output

| shipment_id | carrier | cost |
|---:|---|---:|
| 102 | FedEx | 35.00 |

## Multiple conditions

```sql
SELECT *
FROM shipments
WHERE cost > 20
  AND carrier = 'FedEx';
```

## OR condition

```sql
SELECT *
FROM shipments
WHERE carrier = 'UPS'
   OR carrier = 'DHL';
```

## NOT condition

```sql
SELECT *
FROM shipments
WHERE NOT carrier = 'UPS';
```

## Common comparison operators

| Operator | Meaning |
|---|---|
| `=` | Equal to |
| `<>` or `!=` | Not equal to |
| `>` | Greater than |
| `<` | Less than |
| `>=` | Greater than or equal to |
| `<=` | Less than or equal to |

> [!IMPORTANT]
> `WHERE` filters rows. It cannot normally be used to filter the result of an aggregate function such as `COUNT()` or `SUM()`. Use `HAVING` for aggregate filters.

## Key points

- Text values normally use single quotation marks.
- Combine conditions with `AND`, `OR`, and `NOT`.
- Use parentheses when mixing `AND` and `OR`.

# ORDER BY

## What is it?

`ORDER BY` sorts the final query result.

Rows can be sorted in ascending or descending order.

## Syntax

```sql
SELECT column_name
FROM table_name
ORDER BY column_name ASC;
```

## Example table

### `shipments`

| shipment_id | carrier | cost |
|---:|---|---:|
| 101 | UPS | 20.00 |
| 102 | FedEx | 35.00 |
| 103 | DHL | 15.00 |

## Example

```sql
SELECT
    shipment_id,
    carrier,
    cost
FROM shipments
ORDER BY cost DESC;
```

## Output

| shipment_id | carrier | cost |
|---:|---|---:|
| 102 | FedEx | 35.00 |
| 101 | UPS | 20.00 |
| 103 | DHL | 15.00 |

## Sorting by multiple columns

```sql
SELECT
    carrier,
    cost
FROM shipments
ORDER BY
    carrier ASC,
    cost DESC;
```

SQL first sorts by `carrier`. Rows with the same carrier are then sorted by `cost`.

## Sorting using an alias

```sql
SELECT
    shipment_id,
    cost * 1.13 AS cost_with_tax
FROM shipments
ORDER BY cost_with_tax DESC;
```

## Key points

- `ASC` means ascending and is the default.
- `DESC` means descending.
- Multiple sorting rules are evaluated from left to right.
- `ORDER BY` is processed near the end of a query.

# LIMIT

## What is it?

`LIMIT` restricts the number of rows returned by a query.

It is commonly used with `ORDER BY` to find the highest, lowest, newest, or oldest records.

## Syntax

```sql
SELECT column_name
FROM table_name
LIMIT number_of_rows;
```

## Example

```sql
SELECT
    shipment_id,
    cost
FROM shipments
ORDER BY cost DESC
LIMIT 2;
```

This returns the two most expensive shipments.

## Output

| shipment_id | cost |
|---:|---:|
| 102 | 35.00 |
| 101 | 20.00 |

## Using OFFSET

```sql
SELECT
    shipment_id,
    cost
FROM shipments
ORDER BY cost DESC
LIMIT 5 OFFSET 5;
```

This skips the first five rows and returns the next five.

> [!WARNING]
> Using `LIMIT` without `ORDER BY` does not guarantee which rows will be returned.

## SQL dialect differences

PostgreSQL and MySQL:

```sql
LIMIT 5;
```

SQL Server:

```sql
SELECT TOP 5 *
FROM shipments;
```

Standard SQL and some other databases:

```sql
FETCH FIRST 5 ROWS ONLY;
```

## Key points

- Use `ORDER BY` when the row order matters.
- `LIMIT` is processed after sorting.
- Different databases use different syntax.

 # CASE

## What is it?

`CASE` adds conditional logic to a SQL query.

It works similarly to an `IF / ELSE` statement and returns a value based on the first matching condition.

## Syntax

```sql
CASE
    WHEN condition THEN result
    WHEN another_condition THEN another_result
    ELSE default_result
END
```

## Example table

### `shipments`

| shipment_id | cost |
|---:|---:|
| 101 | 15.00 |
| 102 | 35.00 |
| 103 | 75.00 |

## Example

```sql
SELECT
    shipment_id,
    cost,
    CASE
        WHEN cost >= 50 THEN 'High'
        WHEN cost >= 20 THEN 'Medium'
        ELSE 'Low'
    END AS cost_category
FROM shipments;
```

## Output

| shipment_id | cost | cost_category |
|---:|---:|---|
| 101 | 15.00 | Low |
| 102 | 35.00 | Medium |
| 103 | 75.00 | High |

## CASE inside an aggregate

```sql
SELECT
    SUM(
        CASE
            WHEN carrier = 'UPS' THEN 1
            ELSE 0
        END
    ) AS ups_shipments
FROM shipments;
```

## Key points

- Conditions are checked from top to bottom.
- SQL stops at the first matching condition.
- `ELSE` is optional, but without it unmatched rows return `NULL`.
- Always include `END`.
- `CASE` is commonly used for categorization and conditional aggregation.

# LIKE

## What is it?

`LIKE` filters text values using pattern matching.

It is commonly used when an exact equality comparison is not enough.

## Wildcards

| Wildcard | Meaning |
|---|---|
| `%` | Zero or more characters |
| `_` | Exactly one character |

## Example table

### `customers`

| customer_id | customer_name |
|---:|---|
| 1 | Alice |
| 2 | Albert |
| 3 | Bob |
| 4 | Alicia |

## Starts with

```sql
SELECT *
FROM customers
WHERE customer_name LIKE 'Ali%';
```

This matches `Alice` and `Alicia`.

## Ends with

```sql
SELECT *
FROM customers
WHERE customer_name LIKE '%ert';
```

This matches `Albert`.

## Contains

```sql
SELECT *
FROM customers
WHERE customer_name LIKE '%lic%';
```

This matches values containing `lic`.

## Exactly one unknown character

```sql
SELECT *
FROM customers
WHERE customer_name LIKE 'A_ice';
```

This matches a five-character value such as `Alice`.

## Case-insensitive search in PostgreSQL

```sql
SELECT *
FROM customers
WHERE customer_name ILIKE 'ali%';
```

> [!NOTE]
> Whether `LIKE` is case-sensitive depends on the database and its collation settings.

## Key points

- `%text%` means contains.
- `text%` means starts with.
- `%text` means ends with.
- `_` represents exactly one character.

# IN

## What is it?

`IN` checks whether a value matches any value in a list.

It is cleaner than writing several `OR` conditions.

## Syntax

```sql
SELECT column_name
FROM table_name
WHERE column_name IN (value_1, value_2, value_3);
```

## Example

```sql
SELECT *
FROM shipments
WHERE carrier IN ('UPS', 'FedEx', 'DHL');
```

## Equivalent OR logic

```sql
SELECT *
FROM shipments
WHERE carrier = 'UPS'
   OR carrier = 'FedEx'
   OR carrier = 'DHL';
```

## NOT IN

```sql
SELECT *
FROM shipments
WHERE carrier NOT IN ('UPS', 'FedEx');
```

## IN with a subquery

```sql
SELECT *
FROM customers
WHERE customer_id IN (
    SELECT customer_id
    FROM orders
);
```

This returns customers who have placed at least one order.

> [!WARNING]
> `NOT IN` can produce unexpected results when the list or subquery contains `NULL`. `NOT EXISTS` is often safer for anti-join problems.

## Key points

- `IN` compares against a list of possible values.
- It can contain fixed values or a subquery.
- It is usually easier to read than multiple `OR` conditions.

# BETWEEN

## What is it?

`BETWEEN` filters values within an inclusive range.

Both the lower and upper boundaries are included.

## Syntax

```sql
SELECT column_name
FROM table_name
WHERE column_name BETWEEN lower_value AND upper_value;
```

## Numeric example

```sql
SELECT *
FROM shipments
WHERE cost BETWEEN 20 AND 50;
```

This includes shipments costing exactly `20` or exactly `50`.

## Equivalent condition

```sql
SELECT *
FROM shipments
WHERE cost >= 20
  AND cost <= 50;
```

## Date example

```sql
SELECT *
FROM orders
WHERE order_date BETWEEN '2024-08-01' AND '2024-08-31';
```

## Safer timestamp filtering

When a column contains timestamps, use a half-open range:

```sql
SELECT *
FROM shipments
WHERE shipped_at >= '2024-08-01'
  AND shipped_at < '2024-09-01';
```

This captures every timestamp in August without depending on the final time of August 31.

## NOT BETWEEN

```sql
SELECT *
FROM shipments
WHERE cost NOT BETWEEN 20 AND 50;
```

## Key points

- `BETWEEN` includes both boundaries.
- It works with numbers, dates, timestamps, and text.
- Half-open ranges are often safer for timestamps.

# Aggregate Functions

## What are they?

Aggregate functions summarize multiple rows and return a single result.

The most common aggregate functions are:

- `COUNT()`
- `SUM()`
- `AVG()`
- `MIN()`
- `MAX()`

## Example table

### `shipments`

| shipment_id | carrier | cost |
|---:|---|---:|
| 101 | UPS | 20.00 |
| 102 | FedEx | 35.00 |
| 103 | UPS | 15.00 |

## COUNT

Counts rows or non-NULL values.

```sql
SELECT COUNT(*) AS shipment_count
FROM shipments;
```

Result:

```text
3
```

### COUNT with a column

```sql
SELECT COUNT(delivered_at) AS delivered_shipments
FROM shipments;
```

`COUNT(column)` ignores rows where the column is `NULL`.

### COUNT distinct values

```sql
SELECT COUNT(DISTINCT carrier) AS carrier_count
FROM shipments;
```

## SUM

Adds numeric values.

```sql
SELECT SUM(cost) AS total_cost
FROM shipments;
```

Result:

```text
70.00
```

## AVG

Calculates the average of non-NULL numeric values.

```sql
SELECT AVG(cost) AS average_cost
FROM shipments;
```

## MIN

Returns the smallest value.

```sql
SELECT MIN(cost) AS cheapest_shipment
FROM shipments;
```

## MAX

Returns the largest value.

```sql
SELECT MAX(cost) AS most_expensive_shipment
FROM shipments;
```

## Multiple aggregates

```sql
SELECT
    COUNT(*) AS shipment_count,
    SUM(cost) AS total_cost,
    AVG(cost) AS average_cost,
    MIN(cost) AS minimum_cost,
    MAX(cost) AS maximum_cost
FROM shipments;
```

> [!IMPORTANT]
> Most aggregate functions ignore `NULL`. `COUNT(*)` is different because it counts rows regardless of whether individual columns contain `NULL`.

## Key points

- Aggregate functions summarize multiple rows.
- Use `GROUP BY` to calculate aggregates separately for different groups.
- Use `HAVING` to filter aggregated results.

# GROUP BY

## What is it?

`GROUP BY` combines rows that share the same value and calculates aggregate results for each group.

Without `GROUP BY`, an aggregate function summarizes the entire table.

## Example table

### `shipments`

| shipment_id | carrier | cost |
|---:|---|---:|
| 101 | UPS | 20.00 |
| 102 | FedEx | 35.00 |
| 103 | UPS | 15.00 |
| 104 | FedEx | 25.00 |

## Example

```sql
SELECT
    carrier,
    COUNT(*) AS shipment_count,
    SUM(cost) AS total_cost
FROM shipments
GROUP BY carrier;
```

## Output

| carrier | shipment_count | total_cost |
|---|---:|---:|
| UPS | 2 | 35.00 |
| FedEx | 2 | 60.00 |

## Grouping by multiple columns

```sql
SELECT
    carrier,
    DATE(shipped_at) AS shipment_date,
    COUNT(*) AS shipment_count
FROM shipments
GROUP BY
    carrier,
    DATE(shipped_at);
```

## Important rule

Every selected column must normally be either:

1. Included in `GROUP BY`, or
2. Wrapped in an aggregate function.

Correct:

```sql
SELECT
    carrier,
    COUNT(*) AS shipment_count
FROM shipments
GROUP BY carrier;
```

Incorrect:

```sql
SELECT
    carrier,
    shipment_id,
    COUNT(*)
FROM shipments
GROUP BY carrier;
```

`shipment_id` is neither grouped nor aggregated.

## Key points

- `GROUP BY` changes the level of detail of the result.
- One result row is returned for each unique group.
- It is commonly used with `COUNT`, `SUM`, `AVG`, `MIN`, and `MAX`.

# HAVING

## What is it?

`HAVING` filters groups after aggregation.

It is similar to `WHERE`, but it is used for aggregate conditions.

## Example table

### `shipments`

| shipment_id | carrier | cost |
|---:|---|---:|
| 101 | UPS | 20.00 |
| 102 | FedEx | 35.00 |
| 103 | UPS | 15.00 |
| 104 | UPS | 25.00 |

## Example

```sql
SELECT
    carrier,
    COUNT(*) AS shipment_count
FROM shipments
GROUP BY carrier
HAVING COUNT(*) > 1;
```

## Output

| carrier | shipment_count |
|---|---:|
| UPS | 3 |

## WHERE versus HAVING

```sql
SELECT
    carrier,
    COUNT(*) AS expensive_shipment_count
FROM shipments
WHERE cost > 20
GROUP BY carrier
HAVING COUNT(*) >= 2;
```

In this query:

- `WHERE cost > 20` removes individual rows before grouping.
- `HAVING COUNT(*) >= 2` removes groups after aggregation.

## Incorrect use of WHERE

```sql
SELECT
    carrier,
    COUNT(*) AS shipment_count
FROM shipments
WHERE COUNT(*) > 1
GROUP BY carrier;
```

This does not work because `WHERE` is processed before aggregation.

## Correct version

```sql
SELECT
    carrier,
    COUNT(*) AS shipment_count
FROM shipments
GROUP BY carrier
HAVING COUNT(*) > 1;
```

## Key points

- `WHERE` filters rows.
- `HAVING` filters groups.
- Aggregate conditions normally belong in `HAVING`.
- A query can contain both `WHERE` and `HAVING`.

# NULL

## What is it?

`NULL` represents a missing, unknown, or unavailable value.

It is not the same as:

- Zero
- An empty string
- `FALSE`
- The text `'NULL'`

## Example table

### `shipments`

| shipment_id | shipped_at | delivered_at |
|---:|---|---|
| 101 | 2024-08-01 | 2024-08-03 |
| 102 | 2024-08-02 | NULL |
| 103 | 2024-08-03 | 2024-08-05 |

## Finding NULL values

```sql
SELECT *
FROM shipments
WHERE delivered_at IS NULL;
```

## Finding non-NULL values

```sql
SELECT *
FROM shipments
WHERE delivered_at IS NOT NULL;
```

## Incorrect comparison

```sql
WHERE delivered_at = NULL
```

This does not work because `NULL` represents an unknown value.

## NULL and COUNT

```sql
SELECT
    COUNT(*) AS total_shipments,
    COUNT(delivered_at) AS delivered_shipments
FROM shipments;
```

- `COUNT(*)` counts all rows.
- `COUNT(delivered_at)` ignores rows where `delivered_at` is `NULL`.

## NULL in arithmetic

```sql
SELECT cost + additional_fee
FROM shipments;
```

When `additional_fee` is `NULL`, the result is usually also `NULL`.

Use `COALESCE` when a replacement value is appropriate:

```sql
SELECT cost + COALESCE(additional_fee, 0)
FROM shipments;
```

## Key points

- Use `IS NULL`, not `= NULL`.
- Use `IS NOT NULL`, not `!= NULL`.
- Most aggregate functions ignore `NULL`.
- Arithmetic involving `NULL` usually returns `NULL`.

# COALESCE

## What is it?

`COALESCE` returns the first non-NULL value from a list of expressions.

It is commonly used to replace missing values with a default.

## Syntax

```sql
COALESCE(value_1, value_2, value_3)
```

## Example table

### `customers`

| customer_id | preferred_name | customer_name |
|---:|---|---|
| 1 | Ally | Alice Smith |
| 2 | NULL | Bob Jones |

## Example

```sql
SELECT
    customer_id,
    COALESCE(preferred_name, customer_name) AS display_name
FROM customers;
```

## Output

| customer_id | display_name |
|---:|---|
| 1 | Ally |
| 2 | Bob Jones |

## Replacing NULL with zero

```sql
SELECT
    shipment_id,
    cost + COALESCE(additional_fee, 0) AS total_cost
FROM shipments;
```

## Multiple fallback values

```sql
SELECT
    COALESCE(
        mobile_phone,
        home_phone,
        work_phone,
        'No phone number'
    ) AS contact_number
FROM customers;
```

## Key points

- Values are checked from left to right.
- The first non-NULL value is returned.
- All arguments should have compatible data types.
- It does not change the stored data; it only changes the query result.

# NULLIF

## What is it?

`NULLIF` compares two expressions.

- If they are equal, it returns `NULL`.
- If they are different, it returns the first expression.

## Syntax

```sql
NULLIF(expression_1, expression_2)
```

## Simple example

```sql
SELECT NULLIF(10, 10);
```

Result:

```text
NULL
```

```sql
SELECT NULLIF(10, 5);
```

Result:

```text
10
```

## Preventing division by zero

```sql
SELECT
    successful_deliveries * 1.0
        / NULLIF(total_deliveries, 0) AS success_rate
FROM delivery_metrics;
```

When `total_deliveries` equals zero, `NULLIF(total_deliveries, 0)` returns `NULL`, preventing a division-by-zero error.

## Converting placeholder values to NULL

```sql
SELECT
    NULLIF(customer_phone, '') AS customer_phone
FROM customers;
```

An empty string becomes `NULL`, while a real phone number remains unchanged.

## Combining NULLIF and COALESCE

```sql
SELECT
    COALESCE(
        revenue / NULLIF(order_count, 0),
        0
    ) AS revenue_per_order
FROM customer_metrics;
```

## Key points

- `NULLIF(a, b)` returns `NULL` when `a = b`.
- It is commonly used to prevent division by zero.
- It can convert placeholder values into proper `NULL` values.
   
