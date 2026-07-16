# SQL Window Functions

Window functions perform calculations across a set of related rows while keeping every individual row in the result.

Unlike `GROUP BY`, window functions **do not collapse rows**. Instead, they add calculated values alongside the existing data.

Window functions are one of the most important SQL interview topics because they solve ranking, running totals, moving averages, and previous/next row problems.

## Topics

- [What are Window Functions?](#what-are-window-functions)
- [OVER()](#over)
- [PARTITION BY](#partition-by)
- [ORDER BY in Windows](#order-by-in-windows)
- [ROW_NUMBER()](#row_number)
- [RANK()](#rank)
- [DENSE_RANK()](#dense_rank)
- [LAG()](#lag)
- [LEAD()](#lead)
- [FIRST_VALUE()](#first_value)
- [LAST_VALUE()](#last_value)
- [Running Totals](#running-totals)
- [Moving Averages](#moving-averages)
- [Window Frames](#window-frames)
- [Common Interview Patterns](#common-interview-patterns)
- [Common Interview Mistakes](#common-interview-mistakes)

---

# What are Window Functions?

Window functions calculate values across a group of related rows while **keeping every row**.

Unlike `GROUP BY`, they do not reduce the number of rows.

## Example

Suppose we have:

| customer | amount |
|----------|--------|
| Alice | 50 |
| Alice | 75 |
| Bob | 100 |

Using GROUP BY

```sql
SELECT
    customer,
    SUM(amount)
FROM orders
GROUP BY customer;
```

Output

| customer | total |
|----------|------|
| Alice |125|
| Bob|100|

Notice we lost the individual orders.

Window function

```sql
SELECT
    customer,
    amount,
    SUM(amount) OVER(PARTITION BY customer) AS total_spent
FROM orders;
```

Output

| customer | amount | total_spent |
|----------|--------|------------|
|Alice|50|125|
|Alice|75|125|
|Bob|100|100|

Every row remains.

---

# OVER()

## What is it?

`OVER()` tells SQL that an aggregate should become a window function.

Without OVER

```sql
SUM(amount)
```

returns one result.

With OVER

```sql
SUM(amount) OVER()
```

returns the total beside every row.

Example

```sql
SELECT
    amount,
    SUM(amount) OVER() AS company_sales
FROM orders;
```

---

# PARTITION BY

## What is it?

Creates independent groups inside a window.

Think of it as a GROUP BY that **doesn't collapse rows**.

Example

```sql
SELECT
    customer,
    amount,
    SUM(amount)
        OVER(PARTITION BY customer)
FROM orders;
```

Each customer's running calculation is independent.

---

# ORDER BY in Windows

Inside a window function, ORDER BY determines calculation order.

Example

```sql
SUM(amount)
OVER(
    PARTITION BY customer
    ORDER BY order_date
)
```

Unlike normal ORDER BY, this does **not** sort the final query.

It only controls the window calculation.

---

# ROW_NUMBER()

## What is it?

Assigns a unique sequential number.

No ties.

Example

```sql
SELECT
    customer,
    amount,
    ROW_NUMBER()
    OVER(
        PARTITION BY customer
        ORDER BY amount DESC
    ) AS rn
FROM orders;
```

Output

|customer|amount|rn|
|---------|------|--|
|Alice|75|1|
|Alice|50|2|

### Use when

- Deduplication
- Top 1 per group
- Pagination

---

# RANK()

Allows ties.

Example

Scores

90

90

80

Output

1

1

3

Notice rank 2 is skipped.

Example

```sql
RANK()
OVER(
PARTITION BY department
ORDER BY salary DESC
)
```

---

# DENSE_RANK()

Similar to RANK but does not skip numbers.

Scores

90

90

80

Output

1

1

2

Interview tip

Need Top 3 salaries?

Usually use

```sql
DENSE_RANK()
```

---

# ROW_NUMBER vs RANK vs DENSE_RANK

|Function|Duplicates?|Skipped ranks?|
|---------|-----------|--------------|
|ROW_NUMBER|No|No|
|RANK|Yes|Yes|
|DENSE_RANK|Yes|No|

This comparison is one of the most common SQL interview questions.

---

# LAG()

Returns the previous row.

Example

```sql
SELECT
    order_date,
    amount,

    LAG(amount)
    OVER(
        ORDER BY order_date
    ) AS previous_amount

FROM orders;
```

Useful for

- Month-over-month growth
- Previous purchases
- Comparing consecutive rows

---

# LEAD()

Returns the next row.

Example

```sql
SELECT
    order_date,

    LEAD(order_date)
    OVER(
        ORDER BY order_date
    ) AS next_order

FROM orders;
```

Useful for

- Churn analysis
- Time until next purchase
- Consecutive events

---

# FIRST_VALUE()

Returns the first value in a window.

Example

```sql
SELECT

customer,

amount,

FIRST_VALUE(amount)
OVER(

PARTITION BY customer
ORDER BY order_date

)

FROM orders;
```

Useful for

- First purchase
- Initial salary
- Starting price

---

# LAST_VALUE()

Returns the final value.

Usually requires a window frame.

```sql
LAST_VALUE(amount)

OVER(

ORDER BY order_date

ROWS BETWEEN UNBOUNDED PRECEDING
AND UNBOUNDED FOLLOWING

)
```

Without specifying the frame, LAST_VALUE often returns unexpected results.

---

# Running Totals

One of the most common interview questions.

```sql
SELECT

order_date,

amount,

SUM(amount)

OVER(

ORDER BY order_date

) AS running_total

FROM orders;
```

Output

10

30

45

70

---

# Moving Averages

Calculates rolling averages.

Example

```sql
SELECT

order_date,

AVG(amount)

OVER(

ORDER BY order_date

ROWS BETWEEN 2 PRECEDING
AND CURRENT ROW

)

FROM orders;
```

Useful for

- Sales trends
- Stock prices
- Time-series analysis

---

# Window Frames

Window frames define **which rows** participate in a window calculation.

Common frame

```sql
ROWS BETWEEN UNBOUNDED PRECEDING
AND CURRENT ROW
```

Meaning

Start at the beginning

↓

End at current row

Used for running totals.

Another example

```sql
ROWS BETWEEN 6 PRECEDING
AND CURRENT ROW
```

Calculates a rolling 7-row window.

---

# Common Interview Patterns

### Top N per group

Use

```sql
ROW_NUMBER()

RANK()

DENSE_RANK()
```

---

### Running totals

```sql
SUM()

OVER(ORDER BY ...)
```

---

### Previous row comparison

```sql
LAG()
```

---

### Next row comparison

```sql
LEAD()
```

---

### Deduplication

```sql
ROW_NUMBER()

...

WHERE rn = 1
```

---

### First purchase

```sql
FIRST_VALUE()
```

---

### Rolling average

```sql
AVG()

OVER(

ROWS BETWEEN ...

)
```

---

# Common Interview Mistakes

## Forgetting PARTITION BY

Without it, calculations happen across the entire table.

---

## Forgetting ORDER BY

Functions like

- ROW_NUMBER
- RANK
- LAG
- LEAD

need an ordering.

---

## Using GROUP BY instead

GROUP BY removes rows.

Window functions do not.

---

## Choosing the wrong ranking function

Need unique numbering?

Use ROW_NUMBER.

Need ties?

Use RANK or DENSE_RANK.

---

## LAST_VALUE confusion

Without specifying the frame

```sql
ROWS BETWEEN UNBOUNDED PRECEDING
AND UNBOUNDED FOLLOWING
```

LAST_VALUE often returns the current row instead of the final row.

---

# Interview Tips

- Learn the difference between GROUP BY and window functions.
- Memorize the differences between ROW_NUMBER, RANK, and DENSE_RANK.
- Most "Top N per group" problems use ranking functions.
- Most running total problems use `SUM() OVER(ORDER BY ...)`.
- Most "previous row" questions use `LAG()`.
- Most "next row" questions use `LEAD()`.
- If a problem asks you to calculate something while keeping every row, think **window function** before `GROUP BY`.
