# SQL QUERY FUNDAMENTALS

## What is a Query?

A **query** is a request for information from a database.

We use SQL queries to retrieve, filter, sort, and analyze data stored in database tables.

For example:

```sql
SELECT *
FROM users;
```

This retrieves all columns and all rows from the `users` table.

---

# AS CLAUSE

The `AS` clause gives a **temporary name (alias)** to a column or table.

### Example

```sql
SELECT name AS user_name
FROM users;
```

### Result

| user_name |
| --------- |
| Alice     |
| Bob       |
| Charlie   |
| Diana     |
| Ethan     |

### Important Note

`AS` does **not rename the actual column** in the database.

It only changes the name displayed in the query result.

```text
Database:
name

Query result:
user_name
```

---

# DISTINCT

`DISTINCT` returns only **unique values** and removes duplicates from the result.

### Without DISTINCT

```sql
SELECT user_id
FROM orders;
```

Result:

| user_id |
| ------: |
|       1 |
|       1 |
|       2 |
|       4 |
|       4 |

There are duplicate `user_id` values.

### With DISTINCT

```sql
SELECT DISTINCT user_id
FROM orders;
```

Result:

| user_id |
| ------: |
|       1 |
|       2 |
|       4 |

### When is DISTINCT useful?

For example, if you want to know **which users have placed orders**, you can use:

```sql
SELECT DISTINCT user_id
FROM orders;
```

---

# WHERE CLAUSE

The `WHERE` clause is used to **filter rows**.

Only rows where the condition is `TRUE` are returned.

### Syntax

```sql
SELECT columns
FROM table_name
WHERE condition;
```

### Example

Find users who are at least 18 years old:

```sql
SELECT *
FROM users
WHERE age >= 18;
```

### Another Example

Find orders greater than 1,000:

```sql
SELECT *
FROM orders
WHERE total > 1000;
```

Result:

| order_id | user_id | product_id | total |
| -------: | ------: | ---------: | ----: |
|        2 |       1 |          3 |  1200 |
|        4 |       4 |          3 |  2500 |

---

# COMPARISON OPERATORS

These operators are commonly used with `WHERE`.

| Operator | Meaning                  |
| :------: | ------------------------ |
|    `=`   | Equal to                 |
|   `!=`   | Not equal to             |
|    `>`   | Greater than             |
|    `<`   | Less than                |
|   `>=`   | Greater than or equal to |
|   `<=`   | Less than or equal to    |

### Examples

```sql
SELECT *
FROM users
WHERE age = 24;
```

Find users older than 30:

```sql
SELECT *
FROM users
WHERE age > 30;
```

Find users who are not active:

```sql
SELECT *
FROM users
WHERE status != 'Active';
```

---

# LIKE OPERATOR

`LIKE` is used to search for **patterns in text**.

It is commonly used with `WHERE`.

### Syntax

```sql
SELECT columns
FROM table_name
WHERE column_name LIKE 'pattern';
```

---

## Wildcards

There are two important wildcard characters:

| Wildcard | Meaning                           |
| :------: | --------------------------------- |
|    `%`   | Zero, one, or multiple characters |
|    `_`   | Exactly one character             |

### Common Patterns

| Pattern  | Meaning                                                      |
| -------- | ------------------------------------------------------------ |
| `'A%'`   | Starts with `A`                                              |
| `'%A'`   | Ends with `A`                                                |
| `'%A%'`  | Contains `A` anywhere                                        |
| `'%or%'` | Contains `"or"` anywhere                                     |
| `'_r%'`  | Has `r` in the second position                               |
| `'A__%'` | Starts with `A` and has at least 3 characters                |
| `'A_z'`  | Starts with `A`, has exactly 3 characters, and ends with `z` |

### Example

Find users whose names start with `A`:

```sql
SELECT name
FROM users
WHERE name LIKE 'A%';
```

Result:

| name  |
| ----- |
| Alice |

### Another Example

Find products containing `"o"`:

```sql
SELECT *
FROM products
WHERE name LIKE '%o%';
```

Result:

| product_id | name    | price |
| ---------: | ------- | ----: |
|          2 | Mouse   |   500 |
|          3 | Monitor |  5000 |

---

# IS NULL

`NULL` represents a **missing or unknown value**.

You should not use:

```sql
WHERE phone = NULL
```

or:

```sql
WHERE phone != NULL
```

Instead, use `IS NULL` or `IS NOT NULL`.

### IS NULL

Find users who do not have a phone number:

```sql
SELECT name
FROM users
WHERE phone IS NULL;
```

Result:

| name  |
| ----- |
| Bob   |
| Diana |

### IS NOT NULL

Find users who have a phone number:

```sql
SELECT name
FROM users
WHERE phone IS NOT NULL;
```

Result:

| name    |
| ------- |
| Alice   |
| Charlie |
| Ethan   |

### Remember

```text
IS NULL
→ value is missing

IS NOT NULL
→ value exists
```

---

# BETWEEN

`BETWEEN` filters values within a range.

### Syntax

```sql
WHERE column_name BETWEEN value1 AND value2;
```

`BETWEEN` is **inclusive**, meaning both values are included.

### Example

Find users between 20 and 30 years old:

```sql
SELECT name, age
FROM users
WHERE age BETWEEN 20 AND 30;
```

Result:

| name  | age |
| ----- | --: |
| Alice |  24 |
| Ethan |  27 |

Because:

```text
20 ≤ age ≤ 30
```

### Another Example

Find orders between 500 and 1,500:

```sql
SELECT *
FROM orders
WHERE total BETWEEN 500 AND 1500;
```

Result:

| order_id | user_id | product_id | total |
| -------: | ------: | ---------: | ----: |
|        1 |       1 |          1 |   500 |
|        2 |       1 |          3 |  1200 |
|        3 |       2 |          2 |   800 |

### Important

`BETWEEN 500 AND 1500` includes:

```text
500
...
1500
```

---

# AND

`AND` combines multiple conditions.

**All conditions must be TRUE.**

### Example

Find active users who are at least 18:

```sql
SELECT name, age, status
FROM users
WHERE status = 'Active'
AND age >= 18;
```

The user must satisfy:

```text
status = 'Active'
        AND
age >= 18
```

### Another Example

Find orders greater than 500 but less than 2,000:

```sql
SELECT *
FROM orders
WHERE total > 500
AND total < 2000;
```

---

# OR

`OR` combines multiple conditions where **at least one condition must be TRUE**.

### Example

Find users who are either Alice or Bob:

```sql
SELECT *
FROM users
WHERE name = 'Alice'
OR name = 'Bob';
```

### Another Example

Find products that cost less than 1,000 or greater than 4,000:

```sql
SELECT *
FROM products
WHERE price < 1000
OR price > 4000;
```

Result:

| product_id | name    | price |
| ---------: | ------- | ----: |
|          2 | Mouse   |   500 |
|          3 | Monitor |  5000 |

### AND vs OR

| Operator | Meaning                             |
| :------: | ----------------------------------- |
|   `AND`  | All conditions must be TRUE         |
|   `OR`   | At least one condition must be TRUE |

---

# ORDER BY

`ORDER BY` is used to **sort the query result**.

### Syntax

```sql
SELECT columns
FROM table_name
ORDER BY column_name;
```

By default, results are sorted in **ascending order (`ASC`)**.

### Example

Sort users by age:

```sql
SELECT name, age
FROM users
ORDER BY age;
```

Result:

| name    | age |
| ------- | --: |
| Charlie |  19 |
| Alice   |  24 |
| Ethan   |  27 |
| Bob     |  31 |
| Diana   |  42 |

---

## ASC

`ASC` means **ascending**.

```sql
SELECT name, age
FROM users
ORDER BY age ASC;
```

Numbers:

```text
1 → 2 → 3 → 4 → 5
```

Text:

```text
A → B → C → D
```

`ASC` is the default:

```sql
ORDER BY age;
```

is the same as:

```sql
ORDER BY age ASC;
```

---

## DESC

`DESC` means **descending**.

```sql
SELECT name, age
FROM users
ORDER BY age DESC;
```

Result:

| name    | age |
| ------- | --: |
| Diana   |  42 |
| Bob     |  31 |
| Ethan   |  27 |
| Alice   |  24 |
| Charlie |  19 |

Numbers:

```text
5 → 4 → 3 → 2 → 1
```

Text:

```text
Z → Y → X → W
```

---

# ORDER BY + WHERE

You can combine `WHERE` and `ORDER BY`.

### Example

Find active users and sort them from oldest to youngest:

```sql
SELECT name, age
FROM users
WHERE status = 'Active'
ORDER BY age DESC;
```

Result:

| name    | age |
| ------- | --: |
| Diana   |  42 |
| Alice   |  24 |
| Charlie |  19 |

SQL first filters the users and then sorts the resulting rows.

---

# LIMIT

`LIMIT` specifies the **maximum number of rows** returned.

### Syntax

```sql
SELECT columns
FROM table_name
LIMIT number;
```

### Example

Return only 3 users:

```sql
SELECT *
FROM users
LIMIT 3;
```

### LIMIT + ORDER BY

Find the 2 oldest users:

```sql
SELECT name, age
FROM users
ORDER BY age DESC
LIMIT 2;
```

Result:

| name  | age |
| ----- | --: |
| Diana |  42 |
| Bob   |  31 |

### Important Note

In MySQL, `LIMIT` is normally placed at the **end of the query**.

---

# CASE

`CASE` allows SQL to perform **IF / ELSE-style logic**.

It is commonly used inside `SELECT` to create a calculated or categorized column.

### Basic Syntax

```sql
CASE
    WHEN condition THEN result
    WHEN condition THEN result
    ELSE result
END
```

### Example

Let's categorize users based on age:

```text
Age >= 30 → Adult
Age >= 20 → Young Adult
Otherwise → Teen
```

Query:

```sql
SELECT name, age,
       CASE
           WHEN age >= 30 THEN 'Adult'
           WHEN age >= 20 THEN 'Young Adult'
           ELSE 'Teen'
       END AS age_group
FROM users;
```

### Result

| name    | age | age_group   |
| ------- | --: | ----------- |
| Alice   |  24 | Young Adult |
| Bob     |  31 | Adult       |
| Charlie |  19 | Teen        |
| Diana   |  42 | Adult       |
| Ethan   |  27 | Young Adult |

### Another Example with Products

Categorize products based on price:

```sql
SELECT name, price,
       CASE
           WHEN price >= 5000 THEN 'Expensive'
           WHEN price >= 1000 THEN 'Moderate'
           ELSE 'Cheap'
       END AS price_category
FROM products;
```

### Important

`CASE` checks conditions **from top to bottom**.

Once a condition is `TRUE`, SQL uses that `THEN` result.

---

# QUICK REFERENCE

| SQL Feature   | Purpose                                   |
| ------------- | ----------------------------------------- |
| `SELECT`      | Choose columns to retrieve                |
| `FROM`        | Specify the table                         |
| `AS`          | Create a temporary alias                  |
| `DISTINCT`    | Remove duplicate results                  |
| `WHERE`       | Filter rows                               |
| `LIKE`        | Search text patterns                      |
| `IS NULL`     | Find missing values                       |
| `IS NOT NULL` | Find existing values                      |
| `BETWEEN`     | Filter within a range                     |
| `AND`         | Require all conditions to be true         |
| `OR`          | Require at least one condition to be true |
| `ORDER BY`    | Sort results                              |
| `ASC`         | Sort from low → high / A → Z              |
| `DESC`        | Sort from high → low / Z → A              |
| `LIMIT`       | Limit the number of returned rows         |
| `CASE`        | Create conditional logic                  |

---

# Example Combining Multiple Clauses

You can combine several SQL features in one query.

For example, find the **2 oldest active users**:

```sql
SELECT name AS user_name, age
FROM users
WHERE status = 'Active'
ORDER BY age DESC
LIMIT 2;
```

Result:

| user_name | age |
| --------- | --: |
| Diana     |  42 |
| Alice     |  24 |

The query contains:

```text
SELECT  → choose columns
FROM    → choose table
WHERE   → filter users
ORDER BY → sort users
LIMIT   → restrict results
```
