# EXERCISE 03 — CHEATCODES

> Quick syntax and reasoning reference for **[SQL Exercise 03 — Join](../../EXERCISES/SQL-EXERCISE-03.md)**.

---

# THE DATABASE RELATIONSHIP

```text
users
  │
  │ users.id = orders.user_id
  ▼
orders
  │
  │ orders.product_id = products.id
  ▼
products
```

Actual relationships:

```text
users.id
    ↑
orders.user_id

products.id
    ↑
orders.product_id
```

---

# INNER JOIN

Only returns rows where a match exists.

```sql
SELECT ...
FROM users
INNER JOIN orders
    ON users.id = orders.user_id;
```

Think:

```text
ONLY MATCHING ROWS
```

---

# LEFT JOIN

Keeps **every row from the left table**.

```sql
SELECT ...
FROM users
LEFT JOIN orders
    ON users.id = orders.user_id;
```

If there is no match:

```text
orders.column → NULL
```

Think:

```text
KEEP EVERYTHING FROM THE LEFT
```

---

# JOINING THREE TABLES

Start with the first relationship:

```sql
FROM users
JOIN orders
    ON users.id = orders.user_id
```

Then connect the next table:

```sql
JOIN products
    ON orders.product_id = products.id
```

Full pattern:

```sql
SELECT ...
FROM users
JOIN orders
    ON users.id = orders.user_id
JOIN products
    ON orders.product_id = products.id;
```

---

# ALIASES

Aliases can make JOINs easier to read.

```sql
SELECT u.name, p.name, o.total
FROM users AS u
JOIN orders AS o
    ON u.id = o.user_id
JOIN products AS p
    ON o.product_id = p.id;
```

Think:

```text
u → users
o → orders
p → products
```

---

# ON

`ON` defines **how the tables connect**.

```sql
ON users.id = orders.user_id
```

Another relationship:

```sql
ON orders.product_id = products.id
```

Think:

```text
ON
→ How are these tables related?
```

---

# WHERE

`WHERE` filters rows **after the join result is formed**.

```sql
SELECT ...
FROM users
JOIN orders
    ON users.id = orders.user_id
WHERE users.status = 'Active';
```

Think:

```text
ON
→ connect

WHERE
→ filter rows
```

---

# ON VS WHERE WITH LEFT JOIN

These can produce different results.

### Condition in ON

```sql
LEFT JOIN orders
    ON users.id = orders.user_id
    AND orders.total > 500
```

Users are still preserved.

### Condition in WHERE

```sql
LEFT JOIN orders
    ON users.id = orders.user_id
WHERE orders.total > 500
```

Users without a matching order may be removed.

Remember:

```text
ON
→ controls the matching

WHERE
→ filters the resulting rows
```

---

# DISTINCT

If one user has multiple orders, a JOIN can produce multiple rows for that user.

To return the user only once:

```sql
SELECT DISTINCT users.name
FROM users
INNER JOIN orders
    ON users.id = orders.user_id;
```

Think:

```text
JOIN
→ can create duplicate-looking results

DISTINCT
→ remove duplicate result rows
```

---

# GROUP BY

Use `GROUP BY` when you want to create groups for aggregation.

```sql
SELECT users.name, COUNT(orders.id)
FROM users
LEFT JOIN orders
    ON users.id = orders.user_id
GROUP BY users.name;
```

Common aggregate functions:

```text
COUNT()
SUM()
AVG()
MIN()
MAX()
```

Think:

```text
GROUP BY
→ Which rows belong together?
```

---

# COUNT

### Count rows

```sql
COUNT(*)
```

### Count non-NULL values

```sql
COUNT(orders.id)
```

This matters especially with `LEFT JOIN`.

Example:

```sql
SELECT users.name,
       COUNT(orders.id)
FROM users
LEFT JOIN orders
    ON users.id = orders.user_id
GROUP BY users.name;
```

A user with no orders:

```text
orders.id → NULL
```

Therefore:

```text
COUNT(orders.id) → 0
```

---

# SUM

Calculate a total.

```sql
SUM(orders.total)
```

Example:

```sql
SELECT users.name,
       SUM(orders.total)
FROM users
LEFT JOIN orders
    ON users.id = orders.user_id
GROUP BY users.name;
```

---

# HAVING

`HAVING` filters groups **after aggregation**.

```sql
SELECT users.name,
       COUNT(orders.id)
FROM users
LEFT JOIN orders
    ON users.id = orders.user_id
GROUP BY users.name
HAVING COUNT(orders.id) >= 2;
```

Think:

```text
WHERE
→ filter rows

HAVING
→ filter groups
```

---

# COALESCE

Replace `NULL` with another value.

```sql
COALESCE(SUM(orders.total), 0)
```

Meaning:

```text
SUM is NULL?
    ↓
use 0

Otherwise
    ↓
use SUM
```

Useful with `LEFT JOIN` when a user has no orders.

Example:

```sql
SELECT users.name,
       COALESCE(SUM(orders.total), 0) AS total_spent
FROM users
LEFT JOIN orders
    ON users.id = orders.user_id
GROUP BY users.name;
```

---

# COMMON JOIN PATTERNS

### User + order

```sql
SELECT users.name, orders.total
FROM users
JOIN orders
    ON users.id = orders.user_id;
```

### User + product

```sql
SELECT users.name, products.name
FROM users
JOIN orders
    ON users.id = orders.user_id
JOIN products
    ON orders.product_id = products.id;
```

### Every user, including users with no orders

```sql
FROM users
LEFT JOIN orders
    ON users.id = orders.user_id
```

### Users with no orders

```sql
WHERE orders.id IS NULL
```

### Number of orders per user

```sql
COUNT(orders.id)
GROUP BY users.name
```

### Users with at least 2 orders

```sql
GROUP BY users.name
HAVING COUNT(orders.id) >= 2
```

### Total spent per user

```sql
SUM(orders.total)
GROUP BY users.name
```

### Total spent, showing 0 instead of NULL

```sql
COALESCE(SUM(orders.total), 0)
```

---

# JOIN PROBLEM CHECKLIST

Before writing the query:

```text
1. What am I trying to return?
        ↓
2. Which table contains that data?
        ↓
3. Which tables need to be connected?
        ↓
4. How are they related?
        ↓
5. Do I need EVERY row from one table?
        ↓
6. Which rows should be filtered?
        ↓
7. Do I need groups?
        ↓
8. Do I need to filter those groups?
```

---

# THE CORE DISTINCTION

```text
ON
→ How do the tables connect?

WHERE
→ Which rows do I want?

GROUP BY
→ How do I group the rows?

HAVING
→ Which groups do I want?

COUNT / SUM / AVG / MIN / MAX
→ What do I calculate?

COALESCE
→ What should I show instead of NULL?
```

---

# JOIN DECISION GUIDE

```text
Do I need data from another table?
        │
       YES
        ↓
How are the tables related?
        ↓
Find the PK ↔ FK relationship
        ↓
Do I need every row from my starting table?
        │
    ┌───┴───┐
   YES     NO
    ↓       ↓
LEFT JOIN  INNER JOIN
    │       │
    └───┬───┘
        ↓
Do I need to filter rows?
        ↓
     WHERE
        ↓
Do I need one result per group?
        ↓
    GROUP BY
        ↓
Do I need to filter groups?
        ↓
     HAVING
        ↓
Do I have NULL aggregate results?
        ↓
   COALESCE(...)
```
