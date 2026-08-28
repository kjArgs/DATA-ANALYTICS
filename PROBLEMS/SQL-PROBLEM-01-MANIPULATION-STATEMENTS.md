# SQL Manipulation Problems

> Practice problems for building a strong foundation in SQL data manipulation.
>
> Try to solve each problem **before looking at the solutions**.
>
> These problems focus on modifying database structure and data using:
>
> ```text
> CREATE TABLE
> INSERT
> ALTER TABLE
> UPDATE
> DELETE
> ```
>
> Try to solve the problems yourself before checking the answer key in **[PROBLEM-01-MANIPULATION-STATEMENTS](../CHEATCODES/PROBLEMS/PROBLEM-01-MANIPULATION-STATEMENTS.md)** file.

---

# Reference Tables

Check [SQL-DATABASE-COPY-PASTE](../SQL-DATABASE-COPY-PASTE.md) for the starting database.

The main tables are:

```text
users
products
orders
```

For these problems, focus on **manipulating tables and their data**.

Do not use JOINs unless a problem specifically asks you to.

---

# MANIPULATION BASICS

## Problem 1 — Add a New User

Add a new user to the `users` table.

Use these values:

```text
name: Frank
email: frank@example.com
status: Active
age: 28
phone: 09301234567
```

After inserting the user, display the `users` table to verify the result.

---

## Problem 2 — Add Multiple Users

Add these two users to the `users` table:

```text
Grace
Email: grace@example.com
Status: Active
Age: 23
Phone: 09401234567

Henry
Email: henry@example.com
Status: Inactive
Age: 35
Phone: NULL
```

Verify that both users were added.

---

## Problem 3 — Add a Product

Add the following product to the `products` table:

```text
name: Headphones
price: 1500
```

Display the products table afterward.

---

## Problem 4 — Update a User's Email

Frank changed his email address.

Update his email to:

```text
frank.laurente@example.com
```

Verify that only Frank's email was changed.

---

## Problem 5 — Update a User's Status

Grace is no longer active.

Change Grace's status from:

```text
Active
```

to:

```text
Inactive
```

Verify the change.

---

# MANIPULATION LEVEL 2

## Problem 6 — Update Multiple Columns

Henry has provided a new phone number and is now active.

Update Henry's record so that:

```text
status: Active
phone: 09501234567
```

Do this in a single `UPDATE` statement.

---

## Problem 7 — Give Everyone a Small Price Increase

Increase the price of **every product by 100**.

For example:

```text
Keyboard → 1100
Mouse    → 600
Monitor  → 5100
```

Verify the result.

---

## Problem 8 — Increase Only Expensive Products

Increase the price of products costing more than `1000` by `500`.

Products costing `1000` or less should remain unchanged.

---

## Problem 9 — Add a New Column

The `users` table needs to store the user's city.

Add a new column:

```text
city
```

Use an appropriate string data type.

After adding the column, inspect the table structure.

---

## Problem 10 — Add Data to the New Column

Update the users so their cities are:

```text
Alice   → Manila
Bob     → Quezon City
Charlie → Pasig
Diana   → Makati
Ethan   → Manila
```

Verify the results.

---

# MANIPULATION LEVEL 3

## Problem 11 — Remove a User

Remove Henry from the `users` table.

Verify that Henry no longer exists.

---

## Problem 12 — Remove an Unwanted Product

The `Headphones` product is no longer being sold.

Delete it from the `products` table.

Verify that it was removed.

---

## Problem 13 — Delete Inactive Users

Remove all users whose status is:

```text
Inactive
```

Before executing the `DELETE`, use a `SELECT` statement to check which users will be affected.

---

## Problem 14 — Modify the Table Structure

The `users` table no longer needs the `city` column.

Remove the `city` column from the table.

Afterward, inspect the table structure to verify that the column was removed.

---

## Problem 15 — Manipulation Challenge

Perform the following changes in order:

### 1.

Add a new user:

```text
name: Iris
email: iris@example.com
status: Active
age: 26
phone: 09601234567
```

### 2.

Change Iris's age to `27`.

### 3.

Add a new column to `users`:

```text
membership
```

Use a suitable string data type.

### 4.

Set Iris's membership to:

```text
Premium
```

### 5.

Delete Iris from the table.

### 6.

Remove the `membership` column.

Finally, display the `users` table and inspect its structure.

---

# SAFETY CHECK

Before running `UPDATE` or `DELETE`, ask:

```text
What table am I changing?
        ↓
Which rows should change?
        ↓
What condition identifies those rows?
        ↓
Did I write WHERE?
        ↓
Can I SELECT the rows first?
```

For example:

```sql
SELECT *
FROM users
WHERE status = 'Inactive';
```

If the result is correct, then perform the modification:

```sql
DELETE FROM users
WHERE status = 'Inactive';
```

---

# FINAL CHALLENGE

Without looking at your notes, explain what each command is used for:

```text
INSERT
UPDATE
DELETE
ALTER TABLE
```

Then explain the difference between:

```text
changing data
```

and:

```text
changing table structure
```

---

# GOAL

By the end of these problems, you should be comfortable with:

```text
INSERT
    ↓
Add rows

UPDATE
    ↓
Change existing data

DELETE
    ↓
Remove rows

ALTER TABLE
    ↓
Change table structure
```

And most importantly:

```text
UPDATE / DELETE
        ↓
Always think about WHERE
        ↓
Check the affected rows first
```
