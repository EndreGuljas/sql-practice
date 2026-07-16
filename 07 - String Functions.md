# SQL String Functions

String functions allow you to manipulate, clean, search, and transform text values.

These functions are commonly used to standardize data, extract information, clean customer records, and prepare text for analysis.

> **Note:** Function names may vary slightly between SQL dialects, but the concepts are the same.

## Topics

- [Working with Strings](#working-with-strings)
- [CONCAT()](#concat)
- [SUBSTRING()](#substring)
- [LEFT() & RIGHT()](#left--right)
- [LENGTH()](#length)
- [LOWER() & UPPER()](#lower--upper)
- [TRIM()](#trim)
- [REPLACE()](#replace)
- [POSITION()](#position)
- [Common Interview Patterns](#common-interview-patterns)
- [Common Interview Mistakes](#common-interview-mistakes)

---

# Working with Strings

String functions operate on text columns.

Example table

| customer_id | customer_name | email |
|-------------|---------------|-----------------------|
|1|Alice Smith|alice@gmail.com|
|2|Bob Jones|bob@yahoo.com|

---

# CONCAT()

## What is it?

Combines two or more strings together.

## Syntax

```sql
CONCAT(string1, string2, ...)
```

## Example

```sql
SELECT

CONCAT(first_name, ' ', last_name) AS full_name

FROM customers;
```

Output

| full_name |
|------------|
|Alice Smith|
|Bob Jones|

PostgreSQL also supports

```sql
first_name || ' ' || last_name
```

---

# SUBSTRING()

## What is it?

Extracts part of a string.

## Syntax

```sql
SUBSTRING(column FROM start FOR length)
```

## Example

```sql
SELECT

SUBSTRING(customer_name FROM 1 FOR 5)

FROM customers;
```

Output

| substring |
|------------|
|Alice|
|Bob J|

Useful for

- Area codes
- Postal codes
- Product codes

---

# LEFT() & RIGHT()

Return characters from either end of a string.

## LEFT

```sql
SELECT

LEFT(customer_name,5)

FROM customers;
```

Result

Alice

---

## RIGHT

```sql
SELECT

RIGHT(email,9)

FROM customers;
```

Result

gmail.com

---

# LENGTH()

Returns the number of characters.

```sql
SELECT

customer_name,

LENGTH(customer_name)

FROM customers;
```

Output

| customer_name | length |
|---------------|--------|
|Alice Smith|11|

Useful for

- Validation
- Finding long values
- Data cleaning

---

# LOWER() & UPPER()

Convert text to lowercase or uppercase.

Lowercase

```sql
SELECT LOWER(customer_name)
FROM customers;
```

Uppercase

```sql
SELECT UPPER(customer_name)
FROM customers;
```

Useful when performing case-insensitive comparisons.

Example

```sql
WHERE LOWER(email) = 'alice@gmail.com'
```

---

# TRIM()

Removes spaces from the beginning and end of a string.

Example

```sql
SELECT

TRIM('   Alice   ');
```

Result

```text
Alice
```

Useful for cleaning imported datasets.

---

# REPLACE()

Replaces one piece of text with another.

Example

```sql
SELECT

REPLACE(email,

'@gmail.com',

'@company.com')

FROM customers;
```

Output

alice@company.com

Useful for

- Data cleaning
- Standardization
- Removing unwanted characters

---

# POSITION()

Returns the location of text inside another string.

Example

```sql
SELECT

POSITION('@' IN email)

FROM customers;
```

Output

| position |
|----------|
|6|

Useful for parsing emails and identifiers.

---

# Common Interview Patterns

## Extract Email Domain

```sql
SELECT

SUBSTRING(

email

FROM POSITION('@' IN email)+1

)

FROM customers;
```

Output

gmail.com

---

## Standardize Names

```sql
SELECT

UPPER(TRIM(customer_name))

FROM customers;
```

---

## Find Gmail Users

```sql
SELECT *

FROM customers

WHERE email LIKE '%gmail.com';
```

---

## Replace Missing Characters

```sql
SELECT

REPLACE(phone,

'-',

'')

FROM customers;
```

---

## Build Full Name

```sql
SELECT

CONCAT(first_name,

' ',

last_name)

FROM customers;
```

---

# Common Interview Mistakes

## Forgetting Case Sensitivity

Incorrect

```sql
WHERE customer_name = 'alice'
```

Better

```sql
WHERE LOWER(customer_name) = 'alice'
```

---

## Forgetting to TRIM()

Imported data often contains hidden spaces.

```sql
' Alice '
```

is different from

```sql
'Alice'
```

---

## Using LIKE Instead of Equality

If you know the exact value

```sql
WHERE email = 'alice@gmail.com'
```

is usually better than

```sql
LIKE 'alice@gmail.com'
```

---

## Counting Characters Incorrectly

Remember

```sql
LENGTH('SQL')
```

returns

```text
3
```

Spaces count as characters.

---

# Interview Tips

- `TRIM()`, `LOWER()`, and `UPPER()` are common data-cleaning functions.
- `CONCAT()` and `SUBSTRING()` are among the most frequently tested string functions.
- Learn how to extract parts of emails, phone numbers, and IDs.
- Combine string functions to clean messy datasets.
- Interviewers often ask you to standardize names or parse values from text columns.
