# SQL JOIN Cheatcodes

Solutions for the problems in [SQL Join Problems](../../PROBLEMS/SQL-JOIN.md).

Try solving the problems yourself before checking these.

---

# JOIN Basics

## Problem 1 — Orders with User Names

```sql
SELECT
    orders.id AS order_id,
    users.name AS user_name,
    orders.total
FROM orders
INNER JOIN users
    ON orders.user_id = users.id;
```

---

## Problem 2 — Orders from Active Users

```sql
SELECT
    orders.id AS order_id,
    users.name AS user_name,
    orders.total
FROM orders
INNER JOIN users
    ON orders.user_id = users.id
WHERE users.status = 'active';
```

---

## Problem 3 — Every User and Their Orders

```sql
SELECT
    users.name AS user_name,
    orders.id AS order_id,
    orders.total
FROM users
LEFT JOIN orders
    ON users.id = orders.user_id;
```

---

## Problem 4 — Every Active User and Their Orders

```sql
SELECT
    users.name AS user_name,
    orders.id AS order_id,
    orders.total
FROM users
LEFT JOIN orders
    ON users.id = orders.user_id
WHERE users.status = 'active';
```

---

## Problem 5 — Orders Greater Than 1,000

```sql
SELECT
    users.name AS user_name,
    orders.id AS order_id,
    orders.total
FROM users
LEFT JOIN orders
    ON users.id = orders.user_id
    AND orders.total > 1000;
```

---

## Problem 6 — Orders with Existing Users

```sql
SELECT
    orders.id AS order_id,
    users.name AS user_name
FROM orders
INNER JOIN users
    ON orders.user_id = users.id;
```

---

## Problem 7 — Users with No Orders

```sql
SELECT
    users.name
FROM users
LEFT JOIN orders
    ON users.id = orders.user_id
WHERE orders.id IS NULL;
```

---

## Problem 8 — Users with at Least One Order

```sql
SELECT DISTINCT
    users.name
FROM users
LEFT JOIN orders
    ON users.id = orders.user_id
WHERE orders.id IS NOT NULL;
```

An `INNER JOIN` would also work:

```sql
SELECT DISTINCT
    users.name
FROM users
INNER JOIN orders
    ON users.id = orders.user_id;
```

---

## Problem 9 — Order Count per User

```sql
SELECT
    users.name AS user_name,
    COUNT(orders.id) AS order_count
FROM users
LEFT JOIN orders
    ON users.id = orders.user_id
GROUP BY users.name;
```

---

## Problem 10 — Total Spending per User

```sql
SELECT
    users.name AS user_name,
    COALESCE(SUM(orders.total), 0) AS total_spent
FROM users
LEFT JOIN orders
    ON users.id = orders.user_id
GROUP BY users.name;
```

---

# JOIN Level 2

## Problem 11 — Users with Orders

```sql
SELECT DISTINCT
    users.name
FROM users
INNER JOIN orders
    ON users.id = orders.user_id;
```

---

## Problem 12 — Users with at Least 2 Orders

```sql
SELECT
    users.name AS user_name,
    COUNT(orders.id) AS order_count
FROM users
INNER JOIN orders
    ON users.id = orders.user_id
GROUP BY users.name
HAVING COUNT(orders.id) >= 2;
```

---

## Problem 13 — Active Users with at Least 2 Orders

```sql
SELECT
    users.name AS user_name,
    COUNT(orders.id) AS order_count
FROM users
INNER JOIN orders
    ON users.id = orders.user_id
WHERE users.status = 'active'
GROUP BY users.name
HAVING COUNT(orders.id) >= 2;
```

---

## Problem 14 — Users Spending More Than 1,000

```sql
SELECT
    users.name AS user_name,
    SUM(orders.total) AS total_spent
FROM users
INNER JOIN orders
    ON users.id = orders.user_id
GROUP BY users.name
HAVING SUM(orders.total) > 1000;
```

---

## Problem 15 — Total Spending for Every User

```sql
SELECT
    users.name AS user_name,
    COALESCE(SUM(orders.total), 0) AS total_spent
FROM users
LEFT JOIN orders
    ON users.id = orders.user_id
GROUP BY users.name;
```

---

## Problem 16 — Count Orders Greater Than 500

```sql
SELECT
    users.name AS user_name,
    COUNT(orders.id) AS order_count
FROM users
LEFT JOIN orders
    ON users.id = orders.user_id
    AND orders.total > 500
GROUP BY users.name;
```

---

## Problem 17 — Users Spending More Than 1,500

```sql
SELECT
    users.name AS user_name,
    SUM(orders.total) AS total_spent
FROM users
LEFT JOIN orders
    ON users.id = orders.user_id
GROUP BY users.name
HAVING SUM(orders.total) > 1500;
```

---

# Three-Table JOINs

## Problem 18 — Orders with User and Product Names

```sql
SELECT
    orders.id AS order_id,
    users.name AS user_name,
    products.name AS product_name
FROM orders
LEFT JOIN users
    ON users.id = orders.user_id
LEFT JOIN products
    ON orders.product_id = products.id;
```

---

## Problem 19 — Order Count per Product

```sql
SELECT
    products.name AS product_name,
    COUNT(orders.id) AS order_count
FROM products
LEFT JOIN orders
    ON products.id = orders.product_id
GROUP BY products.name;
```

---

## Problem 20 — Monitor Spending by Active User

```sql
SELECT
    users.name AS user_name,
    SUM(orders.total) AS monitor_spending
FROM users
INNER JOIN orders
    ON users.id = orders.user_id
INNER JOIN products
    ON orders.product_id = products.id
WHERE users.status = 'active'
    AND products.name = 'Monitor'
GROUP BY users.name
HAVING SUM(orders.total) > 1000;
```
