# JOIN

## INNER JOIN

Only returns rows where there is a match.

```sql
SELECT ...
FROM users
INNER JOIN orders
    ON users.id = orders.user_id;
```

Think:

```text
users ∩ orders
```

---

## LEFT JOIN

Keeps **every row from the left table**.

```sql
SELECT ...
FROM users
LEFT JOIN orders
    ON users.id = orders.user_id;
```

If there is no matching order:

```text
orders.column → NULL
```

Think:

```text
KEEP EVERYTHING FROM THE LEFT
```

---

## CROSS JOIN

**combine all rows of one table with all rows of another table.**

```sql
SELECT u.id, o.total
FROM users u
CROSS JOIN orders o;
```
```text
if the it multiplies the table depending in how many rows are there from the CROSS JOIN table.
```

## UNION
**stack one dataset on top of the other**
```text
SQL has strict rules for appending data:

1. Tables must have the same number of columns.
2. The columns must have the same data types in the same order as the first table.
```
```sql
SELECT *
FROM table1
UNION
SELECT *
FROM table2;
```
## WITH

```text
 combine two tables, but one of the tables is the result of another calculation.
```
```sql
WITH previous_results AS (
   SELECT ...
   ...
   ...
   ...
)
SELECT *
FROM previous_results
JOIN customers
  ON _____ = _____;

```


## ON

Defines **how the tables connect**.

```sql
ON users.id = orders.user_id
```

You can also put conditions here when using an outer join:

```sql
ON users.id = orders.user_id
AND orders.total > 500
```

---

## WHERE

Filters individual rows.

```sql
WHERE users.status = 'active'
```

Be careful with `LEFT JOIN`:

```sql
LEFT JOIN orders
    ON users.id = orders.user_id
WHERE orders.total > 500;
```

This can remove users who have no matching orders.

---

## GROUP BY

Creates groups for aggregation.

```sql
GROUP BY users.name
```

Commonly used with:

```sql
COUNT()
SUM()
AVG()
MIN()
MAX()
```

---

## HAVING

Filters groups after aggregation.

```sql
GROUP BY users.name
HAVING COUNT(orders.id) >= 2;
```

Think:

```text
WHERE  → filter rows
HAVING → filter groups
```

---

## COUNT(\*) vs COUNT(column)

```sql
COUNT(*)
```

Counts rows.

```sql
COUNT(orders.id)
```

Counts non-NULL `orders.id` values.

This is especially important with `LEFT JOIN`.

---

## DISTINCT

Removes duplicate result rows.

```sql
SELECT DISTINCT users.name
FROM users
INNER JOIN orders
    ON users.id = orders.user_id;
```

Useful when one user can produce multiple joined rows but you only want the user once.

---

## COALESCE

Replaces `NULL` with another value.

```sql
COALESCE(SUM(orders.total), 0)
```

Means:

```text
If SUM(...) is NULL → use 0
Otherwise → use the SUM(...)
```

---
## PRIMARY KEY AND FOREIGN KEY
```text 
-- are the keys that uniquely identifies its rows

Primary keys have a few requirements:

1. None of the values can be NULL.

2. Each value must be unique (i.e., you can’t have two customers with the same customer_id in the customers table).

3. A table can not have more than one primary key column.

```

# Mental Model

When looking at a JOIN problem, think:

```text
1. What am I trying to return?

2. Which table contains that data?

3. Which tables need to be connected?

4. How are they related?

5. Do I need every row from one side?

6. Which rows should be filtered?

7. Do I need groups?

8. Do I need to filter those groups?
```

The core distinction:

```text
ON
→ How do the tables connect?

WHERE
→ Which rows do I want?

GROUP BY
→ How do I group the rows?

HAVING
→ Which groups do I want?
```
