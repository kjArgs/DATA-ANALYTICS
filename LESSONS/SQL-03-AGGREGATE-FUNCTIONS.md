# AGGREGATE FUNCTIONS

Aggregate functions perform a calculation on **multiple rows** and return a single result.

Common aggregate functions are:

| Function  
| --------- | -------------------------------- |
| `COUNT()` 
| `SUM()`  
| `MIN()`   
| `MAX()`   
| `AVG()`   

---

# COUNT()

`COUNT()` counts values or rows.

There are two commonly used forms:

```sql id="plj6tr"
COUNT(*)
```

and:

```sql id="syw7q5"
COUNT(column_name)
```

## COUNT(*)

`COUNT(*)` counts **all rows**, including rows containing `NULL` values.

### Example

How many users are in the `users` table?

```sql id="m1x1r4"
SELECT COUNT(*) AS total_users
FROM users;
```

Result:

| total_users |
| ----------: |
|           5 |

---

## COUNT(column)

`COUNT(column)` counts only the **non-NULL values** in that column.

### Example

How many users have a phone number?

```sql id="0qzq5j"
SELECT COUNT(phone) AS total_phones
FROM users;
```

Given our data:

| name    | phone       |
| ------- | ----------- |
| Alice   | 09171234567 |
| Bob     | `NULL`      |
| Charlie | 09181234567 |
| Diana   | `NULL`      |
| Ethan   | 09201234567 |

The result is:

| total_phones |
| -----------: |
|            3 |

### Important

```text id="8ihf0e"
COUNT(*)        → counts every row

COUNT(column)   → counts only non-NULL values
```

---

# SUM()

`SUM()` calculates the **total of numeric values** in a column.

### Example

What is the total amount purchased by the user with `user_id = 1`?

```sql id="r1f2rc"
SELECT SUM(total) AS total_amount
FROM orders
WHERE user_id = 1;
```

User `1` has these orders:

| order_id | user_id | total |
| -------: | ------: | ----: |
|        1 |       1 |   500 |
|        2 |       1 |  1200 |

Therefore:

```text id="3w4h7v"
500 + 1200 = 1700
```

Result:

| total_amount |
| -----------: |
|         1700 |

---

# MIN()

`MIN()` returns the **smallest value** in a column.

### Example

What is the cheapest order?

```sql id="5gd0b2"
SELECT MIN(total) AS lowest_purchase
FROM orders;
```

Result:

| lowest_purchase |
| --------------: |
|             300 |

---

# MAX()

`MAX()` returns the **largest value** in a column.

### Example

What is the most expensive order?

```sql id="jv5s9c"
SELECT MAX(total) AS highest_purchase
FROM orders;
```

Result:

| highest_purchase |
| ---------------: |
|             2500 |

---

# MIN() AND MAX() TOGETHER

You can use both functions in the same query.

### Example

Find the highest and lowest order amounts:

```sql id="6j3w4g"
SELECT
    MAX(total) AS highest_purchase,
    MIN(total) AS lowest_purchase
FROM orders;
```

Result:

| highest_purchase | lowest_purchase |
| ---------------: | --------------: |
|             2500 |             300 |

---

# AVG()

`AVG()` calculates the **average value** of a numeric column.

### Example

What is the average order amount?

```sql id="5t8k6r"
SELECT AVG(total) AS average
FROM orders;
```

The calculation is:

```text id="1z2g0c"
(500 + 1200 + 800 + 2500 + 300) / 5

= 5300 / 5

= 1060
```

Result:

| average |
| ------: |
|    1060 |

---

# ROUND()

`ROUND()` rounds a numeric value to a specified number of decimal places.

### Syntax

```sql id="xw6g20"
ROUND(number, decimal_places)
```

### Example

Calculate the average order amount and round it to 2 decimal places:

```sql id="a0u4wy"
SELECT ROUND(AVG(total), 2) AS average
FROM orders;
```

If the average were:

```text id="p3m7s1"
1060.666666
```

`ROUND()` would return:

```text id="6y9g40"
1060.67
```

### Important

`AVG()` calculates the average.

`ROUND()` controls how many decimal places are shown in the numeric result.

```text id="z4s9r2"
AVG(total)
    ↓
Calculate average
    ↓
ROUND(..., 2)
    ↓
Round to 2 decimal places
```

---

# GROUP BY

`GROUP BY` groups rows that have the **same value** in one or more columns.

It is commonly used with aggregate functions such as:

```text id="rx4k3v"
COUNT()
SUM()
AVG()
MIN()
MAX()
```

### Example

How many orders did each user make?

```sql id="v7n1cm"
SELECT
    user_id,
    COUNT(*) AS order_count
FROM orders
GROUP BY user_id;
```

Result:

| user_id | order_count |
| ------: | ----------: |
|       1 |           2 |
|       2 |           1 |
|       4 |           2 |

The database groups the orders like this:

```text id="oj5t8p"
user_id = 1
→ order 1
→ order 2
→ COUNT = 2

user_id = 2
→ order 3
→ COUNT = 1

user_id = 4
→ order 4
→ order 5
→ COUNT = 2
```

---

# GROUP BY WITH SUM()

`GROUP BY` becomes especially useful when you want to calculate a value **for each group**.

### Example

What is the total amount spent by each user?

```sql id="y5p4kr"
SELECT
    user_id,
    SUM(total) AS total_spent
FROM orders
GROUP BY user_id;
```

Result:

| user_id | total_spent |
| ------: | ----------: |
|       1 |        1700 |
|       2 |         800 |
|       4 |        2800 |

### Why?

The database groups the orders by `user_id`.

```text id="f7p6f0"
User 1:
500 + 1200 = 1700

User 2:
800 = 800

User 4:
2500 + 300 = 2800
```

---

# GROUP BY WITH MULTIPLE AGGREGATES

You can use multiple aggregate functions with `GROUP BY`.

### Example

Show each user's:

* `user_id`
* total spending
* number of orders

```sql id="8m7e4w"
SELECT
    user_id,
    SUM(total) AS total_spent,
    COUNT(*) AS order_count
FROM orders
GROUP BY user_id;
```

Result:

| user_id | total_spent | order_count |
| ------: | ----------: | ----------: |
|       1 |        1700 |           2 |
|       2 |         800 |           1 |
|       4 |        2800 |           2 |

---

# GROUP BY COLUMN REFERENCES

In some SQL databases, including MySQL, you can reference the position of a selected column in `GROUP BY`.

For example:

```sql id="y2p6q1"
SELECT
    user_id,
    SUM(total) AS total_spent,
    COUNT(*) AS order_count
FROM orders
GROUP BY 1;
```

`1` refers to the **first expression in the `SELECT` list**.

```text id="x7r4g8"
SELECT
    user_id,          ← 1
    SUM(total),       ← 2
    COUNT(*)          ← 3
```

Therefore:

```sql id="4l3o8b"
GROUP BY 1
```

means:

```sql id="b0v6i2"
GROUP BY user_id
```

### You can also use:

```sql id="j7v9g3"
GROUP BY 2
```

which refers to:

```text id="5g8s2k"
SUM(total)
```

However, **grouping by the actual column name is generally clearer and more maintainable**:

```sql id="w4e1kc"
GROUP BY user_id;
```

rather than:

```sql id="4c5f7n"
GROUP BY 1;
```

---

# HAVING

`HAVING` is used to **filter groups after `GROUP BY`**.

This is different from `WHERE`.

### WHERE vs HAVING

| `WHERE`                          | `HAVING`                           |
| -------------------------------- | ---------------------------------- |
| Filters individual rows          | Filters groups                     |
| Used before grouping             | Used after grouping                |
| Commonly filters regular columns | Commonly filters aggregate results |

### Example

Find users whose total spending is greater than `1,000`.

```sql id="w7n5h3"
SELECT
    user_id,
    SUM(total) AS total_spent
FROM orders
GROUP BY user_id
HAVING SUM(total) > 1000;
```

Result:

| user_id | total_spent |
| ------: | ----------: |
|       1 |        1700 |
|       4 |        2800 |

### How it works

First, `GROUP BY` creates the groups:

```text id="8d6y3q"
User 1 → 1700
User 2 → 800
User 4 → 2800
```

Then `HAVING` filters those groups:

```text id="7t3v5m"
1700 > 1000 → TRUE  → Keep
800  > 1000 → FALSE → Remove
2800 > 1000 → TRUE  → Keep
```

---

# WHERE + GROUP BY + HAVING

You can use `WHERE` and `HAVING` in the same query.

### Example

Find active users and show only those who have spent more than `1,000`.

```sql id="b8r2w5"
SELECT
    u.name,
    SUM(o.total) AS total_spent
FROM users AS u
JOIN orders AS o
    ON u.user_id = o.user_id
WHERE u.status = 'Active'
GROUP BY u.user_id, u.name
HAVING SUM(o.total) > 1000;
```

Result:

| name  | total_spent |
| ----- | ----------: |
| Alice |        1700 |
| Diana |        2800 |

The process is:

```text id="q1v8c4"
FROM / JOIN
    ↓
WHERE
    ↓
GROUP BY
    ↓
HAVING
    ↓
SELECT
```

In simple terms:

```text id="g5z8w2"
WHERE
→ Filter rows first

GROUP BY
→ Create groups

HAVING
→ Filter the groups
```

---

# AGGREGATE FUNCTION QUICK REFERENCE

| Function  | Purpose             | Example                |
| --------- | ------------------- | ---------------------- |
| `COUNT()` | Count rows/values   | `COUNT(*)`             |
| `SUM()`   | Calculate total     | `SUM(total)`           |
| `AVG()`   | Calculate average   | `AVG(total)`           |
| `MIN()`   | Find smallest value | `MIN(total)`           |
| `MAX()`   | Find largest value  | `MAX(total)`           |
| `ROUND()` | Round a number      | `ROUND(AVG(total), 2)` |

---

# GROUP BY + AGGREGATE CHEAT SHEET

```sql id="x8p4s1"
-- Count orders per user
SELECT user_id, COUNT(*)
FROM orders
GROUP BY user_id;
```

```sql id="3v6h2j"
-- Total spending per user
SELECT user_id, SUM(total)
FROM orders
GROUP BY user_id;
```

```sql id="m7q2k5"
-- Average order amount per user
SELECT user_id, ROUND(AVG(total), 2)
FROM orders
GROUP BY user_id;
```

```sql id="c5n8w1"
-- Highest order per user
SELECT user_id, MAX(total)
FROM orders
GROUP BY user_id;
```

```sql id="f4r9t6"
-- Lowest order per user
SELECT user_id, MIN(total)
FROM orders
GROUP BY user_id;
```

```sql id="z2k6p8"
-- Users whose total spending exceeds 1,000
SELECT user_id, SUM(total) AS total_spent
FROM orders
GROUP BY user_id
HAVING SUM(total) > 1000;
```
