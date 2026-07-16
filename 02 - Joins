# SQL Joins

Joins combine rows from two or more tables using a related column.

Understanding joins is one of the most important SQL interview skills. Most real-world queries require combining data from multiple tables.

## Topics

- [What is a Join?](#what-is-a-join)
- [INNER JOIN](#inner-join)
- [LEFT JOIN](#left-join)
- [RIGHT JOIN](#right-join)
- [FULL OUTER JOIN](#full-outer-join)
- [CROSS JOIN](#cross-join)
- [Choosing the Correct Join](#choosing-the-correct-join)
- [Common Interview Mistakes](#common-interview-mistakes)

---

# What is a Join?

A join combines rows from two or more tables based on a matching column.

Suppose we have two tables:

### Customers

| customer_id | customer_name |
|-------------|---------------|
| 1 | Alice |
| 2 | Bob |
| 3 | Carol |

### Orders

| order_id | customer_id | amount |
|----------|-------------|--------|
| 101 | 1 | 50 |
| 102 | 1 | 75 |
| 103 | 2 | 100 |

Both tables contain **customer_id**, which allows them to be joined.

```sql
SELECT
    c.customer_name,
    o.order_id
FROM customers c
JOIN orders o
    ON c.customer_id = o.customer_id;
```

---

# INNER JOIN

## What is it?

Returns only rows where a match exists in **both** tables.

## Syntax

```sql
SELECT columns
FROM table_a
INNER JOIN table_b
    ON table_a.id = table_b.id;
```

## Example

```sql
SELECT
    c.customer_name,
    o.order_id
FROM customers c
INNER JOIN orders o
    ON c.customer_id = o.customer_id;
```

## Output

| customer_name | order_id |
|---------------|----------|
| Alice | 101 |
| Alice | 102 |
| Bob | 103 |

Notice Carol is missing because she has no orders.

### Use when

- Matching records only
- Most common interview join

---

# LEFT JOIN

## What is it?

Returns **every row from the left table**.

If there is no matching row on the right, SQL fills the right-side columns with **NULL**.

## Example

```sql
SELECT
    c.customer_name,
    o.order_id
FROM customers c
LEFT JOIN orders o
    ON c.customer_id = o.customer_id;
```

## Output

| customer_name | order_id |
|---------------|----------|
| Alice | 101 |
| Alice | 102 |
| Bob | 103 |
| Carol | NULL |

### Use when

- Keep every customer
- Find customers with no orders
- Data quality checks

---

# RIGHT JOIN

## What is it?

Returns every row from the **right table**.

If no match exists on the left, those columns become NULL.

## Example

```sql
SELECT
    c.customer_name,
    o.order_id
FROM customers c
RIGHT JOIN orders o
    ON c.customer_id = o.customer_id;
```

### Notes

Many SQL developers rarely use RIGHT JOIN because swapping the table order and using LEFT JOIN usually makes queries easier to read.

---

# FULL OUTER JOIN

## What is it?

Returns every row from both tables.

Matching rows are merged.

Non-matching rows receive NULLs.

## Example

```sql
SELECT
    c.customer_name,
    o.order_id
FROM customers c
FULL OUTER JOIN orders o
    ON c.customer_id = o.customer_id;
```

### Use when

Comparing two datasets to identify missing records.

---

# CROSS JOIN

## What is it?

Returns **every possible combination** of rows.

No matching condition is used.

## Example

Customers

| customer |
|----------|
| Alice |
| Bob |

Carriers

| carrier |
|----------|
| UPS |
| FedEx |

```sql
SELECT
    c.customer_name,
    s.carrier
FROM customers c
CROSS JOIN carriers s;
```

## Output

| customer | carrier |
|----------|----------|
| Alice | UPS |
| Alice | FedEx |
| Bob | UPS |
| Bob | FedEx |

### Interview use

One of the most common interview patterns.

For example:

> Show all customer–carrier combinations that have never been used.

The solution is often:

1. CROSS JOIN
2. LEFT JOIN
3. WHERE right_table.column IS NULL

---

# Choosing the Correct Join

| Join | Returns |
|------|----------|
| INNER JOIN | Matching rows only |
| LEFT JOIN | Everything on the left |
| RIGHT JOIN | Everything on the right |
| FULL OUTER JOIN | Everything from both tables |
| CROSS JOIN | Every possible combination |

---

# Common Interview Mistakes

## Forgetting the ON clause

Incorrect

```sql
SELECT *
FROM customers
JOIN orders;
```

Correct

```sql
SELECT *
FROM customers c
JOIN orders o
ON c.customer_id = o.customer_id;
```

---

## Filtering after a LEFT JOIN

Incorrect

```sql
SELECT *
FROM customers c
LEFT JOIN orders o
ON c.customer_id = o.customer_id
WHERE o.order_id > 100;
```

The `WHERE` clause removes the NULL rows, effectively turning the LEFT JOIN into an INNER JOIN.

Instead:

```sql
SELECT *
FROM customers c
LEFT JOIN orders o
ON c.customer_id = o.customer_id
AND o.order_id > 100;
```

---

## Interview Tips

- Always identify the relationship between tables before writing SQL.
- Draw the schema if necessary.
- Ask yourself:
    - What should appear in the final output?
    - Which table must keep all its rows?
    - Which rows can be discarded?
- If you're looking for missing relationships (e.g., customers with no orders), think **LEFT JOIN + IS NULL**.
- If you're generating every possible pairing (e.g., customers and carriers), think **CROSS JOIN**.
