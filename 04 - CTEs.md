# Common Table Expressions (CTEs)

A Common Table Expression (CTE) is a temporary named result set that exists only for the duration of a single SQL query.

CTEs improve readability, simplify complex queries, and allow large problems to be broken into smaller logical steps.

## Topics

- [What is a CTE?](#what-is-a-cte)
- [Basic CTE](#basic-cte)
- [Multiple CTEs](#multiple-ctes)
- [CTE vs Subquery](#cte-vs-subquery)
- [Recursive CTEs](#recursive-ctes)
- [When to Use a CTE](#when-to-use-a-cte)
- [Common Interview Mistakes](#common-interview-mistakes)

---

# What is a CTE?

A CTE is a temporary table created using the `WITH` keyword.

Instead of writing one large query, you can build it step by step.

Think of a CTE as creating a temporary table that only exists while the query runs.

## General Syntax

```sql
WITH cte_name AS (

    SELECT ...

)

SELECT *
FROM cte_name;
```

The query inside the CTE executes first.

The outer query then treats the CTE like a normal table.

---

# Basic CTE

## Example

Find customers who have spent more than $100.

Without a CTE:

```sql
SELECT *
FROM (

    SELECT
        customer_id,
        SUM(amount) AS total_spent
    FROM orders
    GROUP BY customer_id

) customer_totals

WHERE total_spent > 100;
```

With a CTE:

```sql
WITH customer_totals AS (

    SELECT
        customer_id,
        SUM(amount) AS total_spent
    FROM orders
    GROUP BY customer_id

)

SELECT *
FROM customer_totals
WHERE total_spent > 100;
```

Much easier to read.

---

# Multiple CTEs

You can define several CTEs in one query.

Each CTE can reference the previous ones.

## Example

```sql
WITH customer_totals AS (

    SELECT
        customer_id,
        SUM(amount) AS total_spent
    FROM orders
    GROUP BY customer_id

),

top_customers AS (

    SELECT *
    FROM customer_totals
    WHERE total_spent > 100

)

SELECT *
FROM top_customers;
```

Execution order:

1. customer_totals
2. top_customers
3. Final SELECT

---

# CTE vs Subquery

Both produce temporary results, but they are used differently.

## Subquery

```sql
SELECT *

FROM (

    SELECT
        customer_id,
        SUM(amount) AS total_spent

    FROM orders

    GROUP BY customer_id

) totals;
```

## CTE

```sql
WITH totals AS (

    SELECT
        customer_id,
        SUM(amount) AS total_spent

    FROM orders

    GROUP BY customer_id

)

SELECT *
FROM totals;
```

### Why CTEs are preferred

- Easier to read
- Easier to debug
- Can be reused multiple times
- Better for multi-step analysis

---

# Recursive CTEs

## What are they?

A recursive CTE repeatedly references itself.

They are commonly used for:

- Organizational hierarchies
- Bill of materials
- Tree structures
- Parent-child relationships

## Example

```sql
WITH RECURSIVE numbers AS (

    SELECT 1 AS n

    UNION ALL

    SELECT n + 1
    FROM numbers
    WHERE n < 5

)

SELECT *
FROM numbers;
```

Output

| n |
|---|
|1|
|2|
|3|
|4|
|5|

Most SQL interviews do **not** require recursive CTEs, but they are occasionally asked in senior-level interviews.

---

# When to Use a CTE

CTEs are best when:

- A query has multiple logical steps
- The same result needs to be referenced multiple times
- You want to improve readability
- Breaking down complex business logic
- Building layered calculations

Common examples include:

- Customer lifetime value
- Sales funnels
- Multi-step KPI calculations
- Data cleaning
- Ranking and filtering

---

# Common Interview Mistakes

## Forgetting the final SELECT

Incorrect

```sql
WITH totals AS (

    SELECT *
    FROM orders

);
```

Every CTE must be followed by another query.

Correct

```sql
WITH totals AS (

    SELECT *
    FROM orders

)

SELECT *
FROM totals;
```

---

## Forgetting commas between multiple CTEs

Incorrect

```sql
WITH cte1 AS (...)

cte2 AS (...)
```

Correct

```sql
WITH cte1 AS (...),

cte2 AS (...)
```

---

## Overusing CTEs

Not every query needs one.

Sometimes a simple query is clearer.

Good

```sql
SELECT *
FROM customers
WHERE city = 'Toronto';
```

No CTE required.

---

## Assuming CTEs are always faster

CTEs primarily improve readability.

Depending on the database, they may or may not improve performance.

Always prioritize writing a correct and readable query first.

---

# Interview Tips

- Think of a CTE as creating a temporary table.
- Break large SQL problems into smaller steps.
- Give CTEs descriptive names (`customer_totals`, `monthly_sales`, `ranked_orders`).
- If you find yourself nesting several subqueries, consider replacing them with CTEs.
- CTEs are commonly combined with:
  - Window functions
  - Joins
  - Aggregations
  - Ranking
  - Date analysis

---

# CTE Interview Pattern

Many interview problems can be solved with this structure:

```sql
WITH first_step AS (

    ...

),

second_step AS (

    ...

),

third_step AS (

    ...

)

SELECT *
FROM third_step;
```

Rather than trying to solve everything in one query, build the solution one logical step at a time. This approach makes your SQL easier to understand, debug, and explain during technical interviews.
