# EXERCISE 02 — CHEATCODES

> Quick syntax reference for **[SQL Exercise 02 — Query Fundamentals](../../EXERCISES/SQL-EXERCISE-02.md)**.

---

## BASIC SELECT

Select specific columns:

```sql
SELECT column_1, column_2
FROM table_name;
```

Select everything:

```sql
SELECT *
FROM table_name;
```

---

## AS

Give a temporary name to a result column.

```sql
SELECT name AS user_name
FROM users;
```

`AS` does **not** rename the actual database column.

---

## DISTINCT

Remove duplicate results.

```sql
SELECT DISTINCT user_id
FROM orders;
```

Useful when you only want each value once.

---

# WHERE

Filter rows.

```sql
SELECT *
FROM users
WHERE condition;
```

### Comparison operators

```text
=       equal
!=      not equal
>       greater than
<       less than
>=      greater than or equal
<=      less than or equal
```

### Examples

```sql
WHERE age > 25
```

```sql
WHERE status = 'Active'
```

```sql
WHERE price <= 1000
```

---

# LIKE

Search for text patterns.

```sql
SELECT *
FROM users
WHERE name LIKE 'pattern';
```

### Wildcards

```text
% → zero, one, or multiple characters
_ → exactly one character
```

### Common patterns

```sql
'A%'       -- starts with A
'%A'       -- ends with A
'%A%'      -- contains A
'_r%'      -- r is the second character
```

---

# NULL

Do not use:

```sql
WHERE phone = NULL
```

or:

```sql
WHERE phone != NULL
```

Use:

```sql
WHERE phone IS NULL
```

or:

```sql
WHERE phone IS NOT NULL
```

---

# BETWEEN

Filter within an inclusive range.

```sql
SELECT *
FROM users
WHERE age BETWEEN 20 AND 30;
```

`BETWEEN` includes both boundaries.

```text
20 ≤ age ≤ 30
```

---

# AND

All conditions must be true.

```sql
WHERE status = 'Active'
AND age >= 20;
```

Think:

```text
condition 1
    AND
condition 2
    ↓
BOTH must be TRUE
```

---

# OR

At least one condition must be true.

```sql
WHERE name = 'Alice'
OR name = 'Bob';
```

Think:

```text
condition 1
    OR
condition 2
    ↓
ONE OR BOTH can be TRUE
```

---

# ORDER BY

Sort the result.

Ascending:

```sql
ORDER BY age ASC;
```

Descending:

```sql
ORDER BY age DESC;
```

`ASC` is the default:

```sql
ORDER BY age;
```

---

# LIMIT

Restrict the number of rows returned.

```sql
SELECT *
FROM users
LIMIT 3;
```

### Find the top N

Usually combine:

```sql
ORDER BY
LIMIT
```

Example:

```sql
SELECT name, age
FROM users
ORDER BY age DESC
LIMIT 2;
```

---

# CASE

Create conditional logic.

```sql
SELECT name, age,
       CASE
           WHEN age >= 30 THEN 'Adult'
           WHEN age >= 20 THEN 'Young Adult'
           ELSE 'Teen'
       END AS age_group
FROM users;
```

### Important

`CASE` checks conditions from **top to bottom**.

The first `WHEN` that is true is used.

---

# COMBINING CLAUSES

A common query structure:

```sql
SELECT columns
FROM table_name
WHERE condition
ORDER BY column_name
LIMIT number;
```

Example:

```sql
SELECT name AS user_name, age
FROM users
WHERE status = 'Active'
ORDER BY age DESC
LIMIT 2;
```

Think:

```text
SELECT    → What do I want to see?
FROM      → Where is the data?
WHERE     → Which rows?
ORDER BY  → How should they be sorted?
LIMIT     → How many?
```

---

# QUERY-BUILDING CHECKLIST

When given a question:

```text
1. What information do I need?
        ↓
2. Which table contains it?
        ↓
3. Which columns do I need?
        ↓
4. Do I need to filter rows?
        ↓
5. Do I need multiple conditions?
        ↓
6. Do I need to sort?
        ↓
7. Do I need to limit the result?
        ↓
8. Do I need calculated/category output?
```

---

# QUICK PATTERNS

### Active users

```sql
WHERE status = 'Active'
```

### Users older than 25

```sql
WHERE age > 25
```

### Users between 20 and 30

```sql
WHERE age BETWEEN 20 AND 30
```

### Names beginning with A

```sql
WHERE name LIKE 'A%'
```

### Missing phone numbers

```sql
WHERE phone IS NULL
```

### Sort oldest first

```sql
ORDER BY age DESC
```

### Get the two oldest

```sql
ORDER BY age DESC
LIMIT 2
```

### Unique users who ordered

```sql
SELECT DISTINCT user_id
FROM orders;
```
