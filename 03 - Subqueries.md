# SQL Subqueries

A subquery is a query nested inside another SQL query.

Subqueries allow one query to use the result of another query, making them useful for filtering, comparisons, and building intermediate datasets.

## Topics

- [What is a Subquery?](#what-is-a-subquery)
- [Subquery in WHERE](#subquery-in-where)
- [Subquery in FROM](#subquery-in-from)
- [Subquery in SELECT](#subquery-in-select)
- [Correlated Subqueries](#correlated-subqueries)
- [EXISTS vs IN](#exists-vs-in)
- [When to Use a Subquery](#when-to-use-a-subquery)
- [Common Interview Mistakes](#common-interview-mistakes)

---

# What is a Subquery?

A subquery is a SQL query written inside another SQL query.

The inner query executes first, and its result is used by the outer query.

## General Syntax

```sql
SELECT columns
FROM table
WHERE column IN (
    SELECT column
    FROM another_table
);
```

Think of it as:

> "Run this query first, then use its result in the main query."

---

# Subquery in WHERE

## What is it?

The most common type of subquery.

Used to filter rows based on values returned from another query.

## Example

Find customers who have placed an order.

```sql
SELECT *
FROM customers
WHERE customer_id IN (
    SELECT customer_id
    FROM orders
);
```

### Inner query

```sql
SELECT customer_id
FROM orders;
```

Returns

| customer_id |
|--------------|
| 1 |
| 2 |

The outer query becomes

```sql
SELECT *
FROM customers
WHERE customer_id IN (1,2);
```

### Use when

- Filtering records
- Comparing against another table
- Finding matching values

---

# Subquery in FROM

## What is it?

A subquery can act as a temporary table.

The outer query treats its result like any other table.

## Example

Find the average order amount for customers who spent more than $100.

```sql
SELECT
    AVG(total_spent) AS average_customer_spend
FROM (

    SELECT
        customer_id,
        SUM(amount) AS total_spent
    FROM orders
    GROUP BY customer_id

) customer_totals
WHERE total_spent > 100;
```

### Why use it?

The first query creates customer totals.

The second query analyzes those totals.

---

# Subquery in SELECT

## What is it?

Returns a value for each row in the outer query.

## Example

Display every customer with their number of orders.

```sql
SELECT
    customer_name,

    (
        SELECT COUNT(*)
        FROM orders o
        WHERE o.customer_id = c.customer_id
    ) AS total_orders

FROM customers c;
```

Output

| customer_name | total_orders |
|---------------|--------------|
| Alice | 2 |
| Bob | 1 |
| Carol | 0 |

---

# Correlated Subqueries

## What are they?

A correlated subquery references columns from the outer query.

Unlike regular subqueries, it executes once for every outer row.

## Example

Find customers whose order is above the average order amount.

```sql
SELECT *
FROM orders o
WHERE amount >

(
    SELECT AVG(amount)
    FROM orders
    WHERE customer_id = o.customer_id
);
```

Notice:

```sql
o.customer_id
```

comes from the outer query.

The average is recalculated for every customer.

### Interview tip

Correlated subqueries are often less efficient than window functions or joins.

---

# EXISTS vs IN

## IN

Checks whether a value exists in a list.

```sql
SELECT *
FROM customers
WHERE customer_id IN

(
    SELECT customer_id
    FROM orders
);
```

---

## EXISTS

Checks whether at least one matching row exists.

```sql
SELECT *
FROM customers c

WHERE EXISTS (

    SELECT *

    FROM orders o

    WHERE o.customer_id = c.customer_id

);
```

### When to use EXISTS

- Large datasets
- Checking whether a match exists
- Correlated queries

### When to use IN

- Small lookup lists
- Simpler syntax
- Returning a single column

---

# When to Use a Subquery

Subqueries are useful when:

- Filtering using another table
- Performing calculations before the main query
- Creating temporary datasets
- Returning one calculated value per row

However, if the query becomes difficult to read, a **CTE** is often a better choice.

---

# Common Interview Mistakes

## Returning multiple rows with =

Incorrect

```sql
SELECT *
FROM customers
WHERE customer_id =

(
    SELECT customer_id
    FROM orders
);
```

If the subquery returns multiple rows, this causes an error.

Correct

```sql
WHERE customer_id IN (

    SELECT customer_id
    FROM orders

);
```

---

## Forgetting aliases

Incorrect

```sql
SELECT *

FROM (

    SELECT customer_id,
           COUNT(*) AS orders

    FROM orders

);
```

Most SQL databases require a name.

Correct

```sql
SELECT *

FROM (

    SELECT customer_id,
           COUNT(*) AS orders

    FROM orders

) order_summary;
```

---

## Using correlated subqueries unnecessarily

This works

```sql
SELECT
    customer_name,

(
    SELECT COUNT(*)
    FROM orders o
    WHERE o.customer_id = c.customer_id
)

FROM customers c;
```

But a JOIN with GROUP BY is often faster and easier to understand.

---

# Interview Tips

- Ask yourself if the inner query returns:
    - one value
    - one column
    - many rows
- If multiple rows are returned, use `IN` or `EXISTS`, not `=`.
- If the same subquery is reused multiple times, consider using a **CTE** instead.
- Correlated subqueries work well but can become slow on large datasets.
- Interviewers often ask whether a subquery, CTE, or JOIN would be the best solution—be prepared to explain your choice.
