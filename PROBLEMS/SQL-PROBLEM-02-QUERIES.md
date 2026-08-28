# SQL Query Problems

> Practice problems for building a strong foundation in > SQL queries.
>
> Try to solve each problem **before looking at the solutions**.
>
> These problems focus on retrieving and filtering data using:
>
> ```text
> SELECT
> WHERE
> DISTINCT
> LIKE
> IS NULL
> IS NOT NULL
> BETWEEN
> AND
> OR
> ORDER BY
> LIMIT
> CASE
> ```
>
> Try to solve the problems yourself before checking the answer key in **[PROBLEM-02-QUERIES](../CHEATCODES/PROBLEMS/PROBLEM-02-QUERIES.md)** file.

---

# Reference Tables

Check [SQL-DATABASE-COPY-PASTE](../SQL-DATABASE-COPY-PASTE.md) for the starting database.

The main tables are:

```text
users
products
orders
```

For these problems, focus on **querying data**.

Do not use JOINs unless a problem specifically asks you to.

---

# QUERY BASICS

## Problem 1 — Display All Users

Display every column and every row from the `users` table.

---

## Problem 2 — Display User Names

Display only the names of all users.

The result should contain one column:

```text
name
```

---

## Problem 3 — Display User Information

Display the following columns from `users`:

```text
name
email
age
```

Do not display the other columns.

---

## Problem 4 — Active Users

Display all information for users whose status is `Active`.

---

## Problem 5 — Users Older Than 30

Display the name and age of every user whose age is greater than `30`.

Expected result:

```text
name   | age
-------|----
Bob    | 31
Diana  | 42
```

---

# QUERY LEVEL 2

## Problem 6 — Young Users

Display the name and age of users who are `25` or younger.

Sort the results by age from youngest to oldest.

---

## Problem 7 — Users Between Two Ages

Display the name and age of users whose age is between `20` and `30`.

Remember that `BETWEEN` includes both boundaries.

---

## Problem 8 — Names Starting With A

Find all users whose names begin with the letter `A`.

Display:

```text
name
email
```

---

## Problem 9 — Users Without Phone Numbers

Find all users who do not have a phone number.

Display:

```text
name
phone
```

The result should include users whose `phone` value is `NULL`.

---

## Problem 10 — Active Users With a Phone

Find users who:

- are `Active`
- have a phone number

Display:

```text
name
status
phone
```

---

# QUERY LEVEL 3

## Problem 11 — Multiple Age Conditions

Find users who are either:

- younger than `20`, or
- older than `40`

Display their:

```text
name
age
```

---

## Problem 12 — Active Users Within an Age Range

Find users who are:

- `Active`
- between `20` and `40` years old

Display:

```text
name
age
status
```

Sort the results from oldest to youngest.

---

## Problem 13 — Unique Order Users

Using the `orders` table, display the IDs of users who have placed orders.

Each user ID should appear **only once**.

Expected result:

```text
user_id
-------
1
2
4
```

Do not use a JOIN.

---

## Problem 14 — Most Expensive Products

Display the product name and price.

Sort the products from most expensive to least expensive.

Only display the **two most expensive products**.

Expected result:

```text
name     | price
---------|------
Monitor  | 5000
Keyboard | 1000
```

---

## Problem 15 — Categorize Users by Age

Display each user's:

```text
name
age
age_group
```

Create `age_group` using the following rules:

```text
age >= 40       → 'Senior'
age >= 30       → 'Adult'
age >= 20       → 'Young Adult'
otherwise       → 'Teen'
```

Expected result:

```text
name     | age | age_group
---------|-----|-----------
Alice    | 24  | Young Adult
Bob      | 31  | Adult
Charlie  | 19  | Teen
Diana    | 42  | Senior
Ethan    | 27  | Young Adult
```

---

# QUERY CHALLENGES

## Problem 16 — Active Users With Specific Ages

Find users who are either:

- Active and age `24`, or
- Active and age `42`

Display their name, status, and age.

Try solving this using `AND` and `OR`.

---

## Problem 17 — Products Within a Price Range

Find products whose price is between `500` and `5000`.

Display:

```text
name
price
```

Sort from cheapest to most expensive.

---

## Problem 18 — Search for Names

Find users whose names contain the letter `a`.

Display their names.

Try to use `LIKE`.

---

## Problem 19 — Top Three Oldest Users

Display the name and age of the three oldest users.

Sort from oldest to youngest.

---

## Problem 20 — User Summary

Create a query that displays:

```text
name
age
status
age_group
```

Create `age_group` using:

```text
age >= 40       → 'Senior'
age >= 30       → 'Adult'
age >= 20       → 'Young Adult'
otherwise       → 'Teen'
```

Only include users who are:

```text
Active
```

Sort the results from oldest to youngest.

---

# QUERY CHALLENGE — THINK BEFORE YOU WRITE

For each problem, ask:

```text
1. What information am I trying to see?
        ↓
2. Which table contains it?
        ↓
3. Which columns do I need?
        ↓
4. Do I need to filter rows?
        ↓
5. What conditions do I need?
        ↓
6. Do I need AND or OR?
        ↓
7. Am I checking for NULL?
        ↓
8. Do I need to sort?
        ↓
9. Do I need to limit the result?
        ↓
10. Do I need calculated/category output?
```

---

# CORE QUERY PATTERN

Most basic queries can be built like this:

```sql
SELECT columns
FROM table
WHERE condition
ORDER BY column
LIMIT number;
```

Not every query needs every clause.

Think:

```text
SELECT
→ What do I want to see?

FROM
→ Where is the data?

WHERE
→ Which rows do I want?

ORDER BY
→ How should they be arranged?

LIMIT
→ How many rows do I want?

CASE
→ How should I categorize/calcul­ate a result?
```
