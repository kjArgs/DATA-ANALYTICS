# EXERCISE 01 — CHEATCODES

> Quick syntax reference for **[SQL Exercise 01 — Database Manipulation](../../EXERCISES/SQL-EXERCISE-01.md)**.

---

## INSERT

Add a new row to a table.

```sql
INSERT INTO table_name (column_1, column_2, column_3)
VALUES (value_1, value_2, value_3);
```

### Example

```sql
INSERT INTO users (name, email, status, age, phone)
VALUES ('Frank', 'frank@example.com', 'Active', 28, '09301234567');
```

---

## SELECT

Check the table after making a change.

```sql
SELECT *
FROM table_name;
```

Check a specific record:

```sql
SELECT *
FROM users
WHERE id = 1;
```

---

## UPDATE

Modify an existing row.

```sql
UPDATE table_name
SET column_name = new_value
WHERE condition;
```

### Update multiple columns

```sql
UPDATE users
SET age = 29,
    status = 'Inactive',
    phone = '09309876543'
WHERE id = 6;
```

⚠️ **Always think about `WHERE` before running `UPDATE`.**

Without `WHERE`:

```sql
UPDATE users
SET status = 'Inactive';
```

Every row is updated.

---

## DELETE

Remove rows from a table.

```sql
DELETE FROM table_name
WHERE condition;
```

### Example

```sql
DELETE FROM users
WHERE id = 6;
```

⚠️ Without `WHERE`:

```sql
DELETE FROM users;
```

Every row is deleted.

---

## ALTER TABLE — ADD COLUMN

Add a new column.

```sql
ALTER TABLE table_name
ADD COLUMN column_name data_type;
```

### Example

```sql
ALTER TABLE users
ADD COLUMN address VARCHAR(255);
```

---

## ALTER TABLE — DROP COLUMN

Remove a column.

```sql
ALTER TABLE table_name
DROP COLUMN column_name;
```

### Example

```sql
ALTER TABLE users
DROP COLUMN address;
```

---

## CHECK YOUR WORK

After `INSERT`:

```sql
SELECT *
FROM users;
```

After `UPDATE`:

```sql
SELECT *
FROM users
WHERE id = ...;
```

After `DELETE`:

```sql
SELECT *
FROM users;
```

After `ALTER TABLE`:

```sql
DESCRIBE users;
```

---

## MENTAL CHECKLIST

Before changing data:

```text
What table am I changing?
        ↓
What column(s)?
        ↓
What value(s)?
        ↓
Which row(s)?
        ↓
Do I need WHERE?
        ↓
Run SELECT to verify.
```

### Core patterns

```text
ADD DATA
→ INSERT

CHANGE DATA
→ UPDATE ... SET ... WHERE

REMOVE DATA
→ DELETE FROM ... WHERE

CHANGE TABLE STRUCTURE
→ ALTER TABLE
```
