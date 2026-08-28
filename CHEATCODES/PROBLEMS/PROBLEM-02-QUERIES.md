# SQL Queries Cheatcodes

> Solutions for the problems in **[SQL Query Fundamentals Problems](../../PROBLEMS/SQL-PROBLEM-02-QUERIES.md)**.
>
> Try solving the problems yourself **before checking these**.

---

# QUERY BASICS

## Problem 1 — Display All Users

```sql
SELECT *
FROM users;
```

---

## Problem 2 — Display User Names

```sql
SELECT name
FROM users;
```

---

## Problem 3 — Display User Information

```sql
SELECT
    name,
    email,
    age
FROM users;
```

---

## Problem 4 — Active Users

```sql
SELECT *
FROM users
WHERE status = 'Active';
```

---

## Problem 5 — Users Older Than 30

```sql
SELECT
    name,
    age
FROM users
WHERE age > 30;
```

---

# QUERY LEVEL 2

## Problem 6 — Young Users

```sql
SELECT
    name,
    age
FROM users
WHERE age <= 25
ORDER BY age ASC;
```

---

## Problem 7 — Users Between Two Ages

```sql
SELECT
    name,
    age
FROM users
WHERE age BETWEEN 20 AND 30;
```

---

## Problem 8 — Names Starting With A

```sql
SELECT
    name,
    email
FROM users
WHERE name LIKE 'A%';
```

---

## Problem 9 — Users Without Phone Numbers

```sql
SELECT
    name,
    phone
FROM users
WHERE phone IS NULL;
```

---

## Problem 10 — Active Users With a Phone

```sql
SELECT
    name,
    status,
    phone
FROM users
WHERE status = 'Active'
AND phone IS NOT NULL;
```

---

# QUERY LEVEL 3

## Problem 11 — Multiple Age Conditions

```sql
SELECT
    name,
    age
FROM users
WHERE age < 20
   OR age > 40;
```

---

## Problem 12 — Active Users Within an Age Range

```sql
SELECT
    name,
    age,
    status
FROM users
WHERE status = 'Active'
  AND age BETWEEN 20 AND 40
ORDER BY age DESC;
```

---

## Problem 13 — Unique Order Users

```sql
SELECT DISTINCT
    user_id
FROM orders;
```

---

## Problem 14 — Most Expensive Products

```sql
SELECT
    name,
    price
FROM products
ORDER BY price DESC
LIMIT 2;
```

---

## Problem 15 — Categorize Users by Age

```sql
SELECT
    name,
    age,
    CASE
        WHEN age >= 40 THEN 'Senior'
        WHEN age >= 30 THEN 'Adult'
        WHEN age >= 20 THEN 'Young Adult'
        ELSE 'Teen'
    END AS age_group
FROM users;
```

---

# QUERY CHALLENGES

## Problem 16 — Active Users With Specific Ages

```sql
SELECT
    name,
    status,
    age
FROM users
WHERE (status = 'Active' AND age = 24)
   OR (status = 'Active' AND age = 42);
```

A shorter equivalent version is:

```sql
SELECT
    name,
    status,
    age
FROM users
WHERE status = 'Active'
  AND age IN (24, 42);
```

---

## Problem 17 — Products Within a Price Range

```sql
SELECT
    name,
    price
FROM products
WHERE price BETWEEN 500 AND 5000
ORDER BY price ASC;
```

---

## Problem 18 — Search for Names

```sql
SELECT
    name
FROM users
WHERE name LIKE '%a%';
```

---

## Problem 19 — Top Three Oldest Users

```sql
SELECT
    name,
    age
FROM users
ORDER BY age DESC
LIMIT 3;
```

---

## Problem 20 — User Summary

```sql
SELECT
    name,
    age,
    status,
    CASE
        WHEN age >= 40 THEN 'Senior'
        WHEN age >= 30 THEN 'Adult'
        WHEN age >= 20 THEN 'Young Adult'
        ELSE 'Teen'
    END AS age_group
FROM users
WHERE status = 'Active'
ORDER BY age DESC;
```

---

# QUICK QUERY PATTERNS

### Select everything

```sql
SELECT *
FROM table_name;
```

### Select specific columns

```sql
SELECT column_1, column_2
FROM table_name;
```

### Filter

```sql
WHERE condition;
```

### Multiple conditions

```sql
WHERE condition_1
AND condition_2;
```

```sql
WHERE condition_1
OR condition_2;
```

### Search text

```sql
WHERE name LIKE 'A%';
```

```sql
WHERE name LIKE '%a%';
```

### Check NULL

```sql
WHERE column_name IS NULL;
```

```sql
WHERE column_name IS NOT NULL;
```

### Range

```sql
WHERE column_name BETWEEN value_1 AND value_2;
```

### Remove duplicate results

```sql
SELECT DISTINCT column_name
FROM table_name;
```

### Sort

```sql
ORDER BY column_name ASC;
```

```sql
ORDER BY column_name DESC;
```

### Limit results

```sql
LIMIT 3;
```

### Conditional output

```sql
CASE
    WHEN condition THEN result
    WHEN condition THEN result
    ELSE result
END AS column_name
```

---

# QUERY-BUILDING PATTERN

A common query can look like:

```sql
SELECT columns
FROM table_name
WHERE condition
ORDER BY column_name
LIMIT number;
```

Remember:

```text
SELECT
→ What do I want to see?

FROM
→ Where is the data?

WHERE
→ Which rows do I want?

ORDER BY
→ How should they be sorted?

LIMIT
→ How many rows do I want?

CASE
→ How should I categorize the result?
```
