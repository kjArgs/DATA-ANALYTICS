# SQL Manipulation Cheatcodes

> Solutions for the problems in **[SQL Join Problems](../../PROBLEMS/SQL-PROBLEM-01-MANIPULATION-STATEMENTS.md)**.
>
> Try solving the problems yourself **before checking these**.

---

# MANIPULATION BASICS

## Problem 1 — Add a New User

```sql
INSERT INTO users (name, email, status, age, phone)
VALUES ('Frank', 'frank@example.com', 'Active', 28, '09301234567');

SELECT *
FROM users;
```

---

## Problem 2 — Add Multiple Users

```sql
INSERT INTO users (name, email, status, age, phone)
VALUES
('Grace', 'grace@example.com', 'Active', 23, '09401234567'),
('Henry', 'henry@example.com', 'Inactive', 35, NULL);

SELECT *
FROM users;
```

---

## Problem 3 — Add a Product

```sql
INSERT INTO products (name, price)
VALUES ('Headphones', 1500);

SELECT *
FROM products;
```

---

## Problem 4 — Update a User's Email

```sql
UPDATE users
SET email = 'frank.laurente@example.com'
WHERE name = 'Frank';

SELECT *
FROM users
WHERE name = 'Frank';
```

---

## Problem 5 — Update a User's Status

```sql
UPDATE users
SET status = 'Inactive'
WHERE name = 'Grace';

SELECT *
FROM users
WHERE name = 'Grace';
```

---

# MANIPULATION LEVEL 2

## Problem 6 — Update Multiple Columns

```sql
UPDATE users
SET status = 'Active',
    phone = '09501234567'
WHERE name = 'Henry';

SELECT *
FROM users
WHERE name = 'Henry';
```

---

## Problem 7 — Give Everyone a Small Price Increase

```sql
UPDATE products
SET price = price + 100;

SELECT *
FROM products;
```

---

## Problem 8 — Increase Only Expensive Products

```sql
UPDATE products
SET price = price + 500
WHERE price > 1000;

SELECT *
FROM products;
```

---

## Problem 9 — Add a New Column

```sql
ALTER TABLE users
ADD COLUMN city VARCHAR(50);

DESCRIBE users;
```

---

## Problem 10 — Add Data to the New Column

```sql
UPDATE users
SET city = 'Manila'
WHERE name = 'Alice';

UPDATE users
SET city = 'Quezon City'
WHERE name = 'Bob';

UPDATE users
SET city = 'Pasig'
WHERE name = 'Charlie';

UPDATE users
SET city = 'Makati'
WHERE name = 'Diana';

UPDATE users
SET city = 'Manila'
WHERE name = 'Ethan';

SELECT *
FROM users;
```

---

# MANIPULATION LEVEL 3

## Problem 11 — Remove a User

```sql
DELETE FROM users
WHERE name = 'Henry';

SELECT *
FROM users;
```

---

## Problem 12 — Remove an Unwanted Product

```sql
DELETE FROM products
WHERE name = 'Headphones';

SELECT *
FROM products;
```

---

## Problem 13 — Delete Inactive Users

First, check which rows will be affected:

```sql
SELECT *
FROM users
WHERE status = 'Inactive';
```

Then delete them:

```sql
DELETE FROM users
WHERE status = 'Inactive';
```

Verify:

```sql
SELECT *
FROM users;
```

---

## Problem 14 — Modify the Table Structure

```sql
ALTER TABLE users
DROP COLUMN city;

DESCRIBE users;
```

---

# FINAL CHALLENGE

## Problem 15 — Manipulation Challenge

### 1. Add Iris

```sql
INSERT INTO users (name, email, status, age, phone)
VALUES ('Iris', 'iris@example.com', 'Active', 26, '09601234567');
```

### 2. Change Iris's age

```sql
UPDATE users
SET age = 27
WHERE name = 'Iris';
```

### 3. Add the membership column

```sql
ALTER TABLE users
ADD COLUMN membership VARCHAR(50);
```

### 4. Set Iris's membership

```sql
UPDATE users
SET membership = 'Premium'
WHERE name = 'Iris';
```

### 5. Delete Iris

```sql
DELETE FROM users
WHERE name = 'Iris';
```

### 6. Remove the membership column

```sql
ALTER TABLE users
DROP COLUMN membership;
```

### Final verification

```sql
SELECT *
FROM users;

DESCRIBE users;
```

---

# SAFETY CHECK

Before running an `UPDATE` or `DELETE`, check the rows first.

### Before UPDATE

```sql
SELECT *
FROM users
WHERE condition;
```

Then:

```sql
UPDATE users
SET column = value
WHERE condition;
```

### Before DELETE

```sql
SELECT *
FROM users
WHERE condition;
```

Then:

```sql
DELETE FROM users
WHERE condition;
```

---

# CORE PATTERNS

```text
INSERT
→ Add rows

UPDATE
→ Change existing data

DELETE
→ Remove rows

ALTER TABLE
→ Change table structure

SELECT
→ Check your work
```

The most important habit:

```text
UPDATE / DELETE
       ↓
Check the WHERE condition
       ↓
SELECT first
       ↓
Then modify the data
```
