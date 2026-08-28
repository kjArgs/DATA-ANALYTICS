# SQL JOIN Cheatcodes

Solutions for the problems in [SQL Join Problems](../../PROBLEMS/SQL-JOIN.md).

Try solving the problems yourself before checking these.

---

# JOIN Basics

## Problem 1 — Orders with User Names

```sql
SELECT
    o.id AS order_id,
    u.name AS user_name,
    o.total
FROM orders o
INNER JOIN users u
    ON o.user_id = u.id;
```

---

## Problem 2 — Orders from Active Users

```sql
    SELECT o.id AS order_id, 
    u.name AS user_name, 
    total
FROM orders o
INNER JOIN users u
    ON o.user_id = u.id 
WHERE u.status = 'Active';
```

---

## Problem 3 — Every User and Their Orders

```sql
SELECT 
    u.name AS user_name, 
    o.id AS oder_id, 
    o.total
FROM users u
LEFT JOIN orders o
    ON u.id = o.user_id;
```

---

## Problem 4 — Every Active User and Their Orders

```sql
SELECT
    u.name AS user_name,
    o.id AS order_id,
    o.total
FROM users u
LEFT JOIN orders o
    ON u.id = o.user_id
WHERE u.status = 'active';
```

---

## Problem 5 — Orders Greater Than 1,000

```sql
SELECT
    u.name AS user_name,
    o.id AS order_id,
    o.total
FROM users u
LEFT JOIN orders o
    ON u.id = o.user_id
    AND o.total > 1000;
```

---

## Problem 6 — Orders with Existing Users

```sql
SELECT
    o.id AS order_id,
    u.name AS user_name
FROM orders o
INNER JOIN users o
    ON o.user_id = u.id;
```

---

## Problem 7 — Users with No Orders

```sql
SELECT
    u.name
FROM users u
LEFT JOIN orders u
    ON u.id = o.user_id
WHERE o.id IS NULL;
```

---

## Problem 8 — Users with at Least One Order

```sql
SELECT DISTINCT
    u.name
FROM users u
LEFT JOIN orders o
    ON u.id = o.user_id
WHERE o.id IS NOT NULL;
```

An `INNER JOIN` would also work:

```sql
SELECT DISTINCT
    u.name
FROM users u
INNER JOIN orders o
    ON u.id = o.user_id;
```

---

## Problem 9 — Order Count per User

```sql
SELECT
    u.name AS user_name,
    COUNT(o.id) AS order_count
FROM users u
LEFT JOIN orders o
    ON u.id = o.user_id
GROUP BY u.name;
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
    u.name
FROM users u
INNER JOIN orders o
    ON u.id = o.user_id;
```

---

## Problem 12 — Users with at Least 2 Orders

```sql
SELECT
    u.name AS user_name,
    COUNT(o.id) AS order_count
FROM users u
INNER JOIN orders o
    ON u.id = o.user_id
GROUP BY u.name
HAVING COUNT(o.id) >= 2;
```

---

## Problem 13 — Active Users with at Least 2 Orders

```sql
SELECT
    u.name AS user_name,
    COUNT(o.id) AS order_count
FROM users u
INNER JOIN orders o
    ON u.id = o.user_id
WHERE u.status = 'active'
GROUP BY u.name
HAVING COUNT(o.id) >= 2;
```

---

## Problem 14 — Users Spending More Than 1,000

```sql
SELECT
    u.name AS user_name,
    SUM(o.total) AS total_spent
FROM users u
INNER JOIN orders o
    ON u.id = o.user_id
GROUP BY u.name
HAVING SUM(o.total) > 1000;
```

---

## Problem 15 — Total Spending for Every User

```sql
SELECT
    u.name AS user_name,
    COALESCE(SUM(o.total), 0) AS total_spent
FROM users u
LEFT JOIN orders o
    ON u.id = o.user_id
GROUP BY u.name;
```

---

## Problem 16 — Count Orders Greater Than 500

```sql
SELECT
    u.name AS user_name,
    COUNT(o.id) AS order_count
FROM users u
LEFT JOIN orders o
    ON u.id = o.user_id
    AND o.total > 500
GROUP BY u.name;
```

---

## Problem 17 — Users Spending More Than 1,500

```sql
SELECT
    users.name AS user_name,
    SUM(o.total) AS total_spent
FROM users u
LEFT JOIN orders o
    ON u.id = o.user_id
GROUP BY u.name
HAVING SUM(o.total) > 1500;
```

---

# Three-Table JOINs

## Problem 18 — Orders with User and Product Names

```sql
SELECT
    o.id AS order_id,
    u.name AS user_name,
    pr.name AS product_name
FROM orders o
LEFT JOIN users u
    ON u.id = o.user_id
LEFT JOIN products p
    ON o.product_id = p.id;
```

---

## Problem 19 — Order Count per Product

```sql
SELECT
    p.name AS product_name,
    COUNT(o.id) AS order_count
FROM products p
LEFT JOIN orders o
    ON p.id = o.product_id
GROUP BY p.name;
```

---

## Problem 20 — Monitor Spending by Active User

```sql
SELECT
    u.name AS user_name,
    SUM(o.total) AS monitor_spending
FROM users u
INNER JOIN orders o
    ON u.id = o.user_id
INNER JOIN products p
    ON o.product_id = p.id
WHERE u.status = 'active'
    AND p.name = 'Monitor'
GROUP BY u.name
HAVING SUM(o.total) > 1000;
```
