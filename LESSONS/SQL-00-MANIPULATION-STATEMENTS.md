# INTRODUCTION TO SQL

## What is SQL?

**SQL (Structured Query Language)** is a language used to **create, retrieve, modify, and manage data** in relational databases.

SQL can be used to:

* Create tables
* Insert data
* Retrieve data
* Update existing data
* Delete data
* Define relationships between tables
* Apply rules and constraints to data

---

# RELATIONAL DATABASE

A **relational database** organizes data into one or more **tables**.

Tables can be connected to each other using relationships.

For example:

```text
users
  ↓
orders
  ↓
products
```

In our database:

```text
users.user_id
      ↑
orders.user_id

products.product_id
        ↑
orders.product_id
```

This means an order belongs to a user and references a product.

---

# WHAT IS A TABLE?

A **table** is a collection of related data organized into **rows and columns**.

For example, our `users` table:

| user_id | name    | status   | age |
| ------: | ------- | -------- | --: |
|       1 | Alice   | Active   |  24 |
|       2 | Bob     | Inactive |  31 |
|       3 | Charlie | Active   |  19 |

A table can also be referred to as a **relation** in relational database terminology.

---

# ROWS AND COLUMNS

## Column

A **column** represents a specific attribute or type of information.

For example:

```text
user_id
name
email
status
age
phone
```

Each column has a **data type** that determines what kind of value it can store.

---

## Row

A **row** represents a single record in a table.

For example:

| user_id | name  | age |
| ------: | ----- | --: |
|       1 | Alice |  24 |

The entire row represents one user.

### Easy way to remember

```text
Column → What type of information?
Row    → One complete record
```

---

# DATA TYPES

A **data type** determines what kind of data a column can store.

Common SQL data types include:

| Data Type         | Meaning                    | Example                      |
| ----------------- | -------------------------- | ---------------------------- |
| `INTEGER` / `INT` | Whole number               | `24`, `500`, `-10`           |
| `VARCHAR`         | Variable-length text       | `'Alice'`                    |
| `TEXT`            | Longer text                | `'This is a description...'` |
| `DATE`            | Date                       | `'2026-08-28'`               |
| `DATETIME`        | Date and time              | `'2026-08-28 15:30:00'`      |
| `DECIMAL`         | Exact decimal number       | `99.99`                      |
| `FLOAT`           | Approximate decimal number | `3.14`                       |
| `BOOLEAN`         | True/false value           | `TRUE` / `FALSE`             |

### Important

The exact available data types depend on the database system.

For example, since you are using **MySQL**, `INT`, `VARCHAR`, `DATE`, `DATETIME`, and `DECIMAL` are commonly used.

---

# SQL STATEMENTS

A **SQL statement** is an instruction sent to the database to perform an operation.

For example:

```sql
SELECT *
FROM users;
```

This tells the database to retrieve all columns from the `users` table.

Another example:

```sql
INSERT INTO users (name, email)
VALUES ('Alice', 'alice@example.com');
```

This tells the database to insert a new record.

### Common SQL statements

| Statement | Purpose                                    |
| --------- | ------------------------------------------ |
| `CREATE`  | Create database objects                    |
| `INSERT`  | Add data                                   |
| `SELECT`  | Retrieve data                              |
| `UPDATE`  | Modify existing data                       |
| `DELETE`  | Remove data                                |
| `ALTER`   | Modify the structure of an existing object |
| `DROP`    | Delete a database object                   |

---

# CREATE TABLE

`CREATE TABLE` is used to create a new table.

### Syntax

```sql
CREATE TABLE table_name (
    column_1 data_type,
    column_2 data_type,
    column_3 data_type
);
```

### Example

```sql
CREATE TABLE users (
    user_id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100),
    email VARCHAR(100),
    status VARCHAR(20),
    age INT,
    phone VARCHAR(20)
);
```

### Breakdown

```text
CREATE TABLE
→ Creates a new table.

users
→ Name of the table.

user_id, name, email, status, age, phone
→ Columns of the table.

INT, VARCHAR(100), VARCHAR(20)
→ Data types of the columns.
```

---

# INSERT STATEMENT

`INSERT` is used to **add new rows** to a table.

### Syntax

```sql
INSERT INTO table_name (column_1, column_2)
VALUES (value_1, value_2);
```

### Example

```sql
INSERT INTO users (name, email, status, age, phone)
VALUES (
    'Alice',
    'alice@example.com',
    'Active',
    24,
    '09171234567'
);
```

### Breakdown

```text
INSERT INTO
→ Specifies that we want to add data.

users
→ The table where the data will be inserted.

(name, email, status, age, phone)
→ The columns receiving the values.

VALUES
→ Indicates the values being inserted.

('Alice', 'alice@example.com', 'Active', 24, '09171234567')
→ The actual data being inserted.
```

### Important

The values should correspond to the columns in the same order.

```text
name     → Alice
email    → alice@example.com
status   → Active
age      → 24
phone    → 09171234567
```

---

# SELECT STATEMENT

`SELECT` is used to **retrieve data** from a database.

### Syntax

```sql
SELECT column_name
FROM table_name;
```

### Example

```sql
SELECT name
FROM users;
```

Result:

| name    |
| ------- |
| Alice   |
| Bob     |
| Charlie |
| Diana   |
| Ethan   |

### Selecting multiple columns

```sql
SELECT name, email, age
FROM users;
```

### Selecting all columns

The `*` wildcard means **all columns**.

```sql
SELECT *
FROM users;
```

This returns every column from the `users` table.

### Basic structure

```text
SELECT → What columns do I want?
FROM   → Which table do they come from?
```

---

# ALTER TABLE

`ALTER TABLE` is used to **modify the structure of an existing table**.

It can be used to:

* Add columns
* Modify columns
* Rename columns
* Drop columns
* Add constraints
* Drop constraints

### Add a column

```sql
ALTER TABLE users
ADD COLUMN address VARCHAR(255);
```

This adds an `address` column to the `users` table.

### Basic structure

```text
ALTER TABLE
→ Modify an existing table.

users
→ The table being modified.

ADD COLUMN
→ The operation being performed.

address VARCHAR(255)
→ The new column and its data type.
```

---

# UPDATE STATEMENT

`UPDATE` is used to **modify existing records**.

### Syntax

```sql
UPDATE table_name
SET column_name = new_value
WHERE condition;
```

### Example

Change Alice's status:

```sql
UPDATE users
SET status = 'Inactive'
WHERE user_id = 1;
```

This changes Alice's status from `Active` to `Inactive`.

### Breakdown

```text
UPDATE
→ Specifies that existing data will be modified.

users
→ The table being modified.

SET
→ Specifies the new value.

status = 'Inactive'
→ The column and new value.

WHERE user_id = 1
→ Determines which row should be updated.
```

### ⚠️ Important

Be careful when using `UPDATE` without `WHERE`.

```sql
UPDATE users
SET status = 'Inactive';
```

This changes **every user's status** to `Inactive`.

---

# DELETE STATEMENT

`DELETE` is used to **remove rows from a table**.

### Syntax

```sql
DELETE FROM table_name
WHERE condition;
```

### Example

Delete a specific user:

```sql
DELETE FROM users
WHERE user_id = 5;
```

This removes the user whose `user_id` is `5`.

### Breakdown

```text
DELETE FROM
→ Specifies that rows will be deleted.

users
→ The table where the deletion happens.

WHERE
→ Determines which rows should be deleted.

user_id = 5
→ The condition identifying the row.
```

### ⚠️ Important

Be careful when using `DELETE` without `WHERE`.

```sql
DELETE FROM users;
```

This deletes **all rows** from the `users` table.

---

# CONSTRAINTS

**Constraints** are rules applied to columns that control what data can be stored.

They help maintain **data integrity and consistency**.

Common constraints include:

| Constraint    | Purpose                               |
| ------------- | ------------------------------------- |
| `PRIMARY KEY` | Uniquely identifies each row          |
| `FOREIGN KEY` | Creates a relationship between tables |
| `UNIQUE`      | Prevents duplicate values             |
| `NOT NULL`    | Prevents missing values               |
| `DEFAULT`     | Provides a default value              |
| `CHECK`       | Restricts values based on a condition |

---

# PRIMARY KEY

A `PRIMARY KEY` uniquely identifies each row in a table.

### Example

```sql
CREATE TABLE users (
    user_id INT PRIMARY KEY,
    name VARCHAR(100)
);
```

Here:

```text
user_id → PRIMARY KEY
```

Each user must have a unique `user_id`.

For example:

| user_id | name    |
| ------: | ------- |
|       1 | Alice   |
|       2 | Bob     |
|       3 | Charlie |

You cannot have:

```text
user_id = 1
```

twice in the same table.

### Important

A primary key:

* Must be unique
* Cannot contain `NULL`
* Identifies a specific row

---

# FOREIGN KEY

A `FOREIGN KEY` creates a relationship between two tables.

For example, `orders` contains:

```text
user_id
```

which references:

```text
users.user_id
```

### Example

```sql
CREATE TABLE orders (
    order_id INT AUTO_INCREMENT PRIMARY KEY,
    user_id INT,
    product_id INT,
    total DECIMAL(10, 2),

    FOREIGN KEY (user_id)
        REFERENCES users(user_id),

    FOREIGN KEY (product_id)
        REFERENCES products(product_id)
);
```

This creates two relationships:

```text
orders.user_id
        ↓
users.user_id
```

and:

```text
orders.product_id
        ↓
products.product_id
```

### Purpose

A foreign key helps prevent invalid relationships.

For example, if there is no user with:

```text
user_id = 999
```

the database can prevent an order from referencing that nonexistent user.

---

# UNIQUE

`UNIQUE` prevents duplicate values in a column.

### Example

```sql
CREATE TABLE users (
    user_id INT PRIMARY KEY,
    email VARCHAR(100) UNIQUE
);
```

This means every user's email must be different.

Valid:

| user_id | email                                         |
| ------: | --------------------------------------------- |
|       1 | [alice@example.com](mailto:alice@example.com) |
|       2 | [bob@example.com](mailto:bob@example.com)     |

Invalid:

| user_id | email                                         |
| ------: | --------------------------------------------- |
|       1 | [alice@example.com](mailto:alice@example.com) |
|       2 | [alice@example.com](mailto:alice@example.com) |

because the email is duplicated.

### PRIMARY KEY vs UNIQUE

| `PRIMARY KEY`                  | `UNIQUE`                                |
| ------------------------------ | --------------------------------------- |
| Identifies the row             | Prevents duplicate values               |
| Only one primary key per table | Multiple UNIQUE constraints can exist   |
| Cannot be `NULL`               | `NULL` handling depends on the database |

---

# NOT NULL

`NOT NULL` prevents a column from containing `NULL`.

### Example

```sql
CREATE TABLE users (
    user_id INT PRIMARY KEY,
    name VARCHAR(100) NOT NULL
);
```

A user must have a value for `name`.

This would fail:

```sql
INSERT INTO users (user_id)
VALUES (1);
```

because `name` is required.

---

# DEFAULT

`DEFAULT` provides a value automatically when an inserted row does not specify one.

### Example

```sql
CREATE TABLE users (
    user_id INT PRIMARY KEY,
    name VARCHAR(100),
    status VARCHAR(20) DEFAULT 'Active'
);
```

Now:

```sql
INSERT INTO users (user_id, name)
VALUES (1, 'Alice');
```

The database automatically uses:

```text
status = 'Active'
```

Result:

| user_id | name  | status |
| ------: | ----- | ------ |
|       1 | Alice | Active |

---

# CHECK

`CHECK` restricts the values that can be inserted into a column based on a condition.

### Example

```sql
CREATE TABLE users (
    user_id INT PRIMARY KEY,
    name VARCHAR(100),
    age INT CHECK (age >= 18)
);
```

This means the age must be at least `18`.

Valid:

```sql
INSERT INTO users (user_id, name, age)
VALUES (1, 'Alice', 24);
```

Invalid:

```sql
INSERT INTO users (user_id, name, age)
VALUES (2, 'Bob', 15);
```

because:

```text
15 >= 18
FALSE
```

---

# COMBINING CONSTRAINTS

You can use multiple constraints on the same table.

### Example

```sql
CREATE TABLE users (
    user_id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    status VARCHAR(20) DEFAULT 'Active',
    age INT CHECK (age >= 18)
);
```

Here:

```text
user_id
→ PRIMARY KEY
→ AUTO_INCREMENT

name
→ NOT NULL

email
→ UNIQUE
→ NOT NULL

status
→ DEFAULT 'Active'

age
→ CHECK (age >= 18)
```

---

# QUICK REFERENCE

## SQL Statements

| Statement      | Purpose                |
| -------------- | ---------------------- |
| `CREATE TABLE` | Create a new table     |
| `INSERT INTO`  | Add rows               |
| `SELECT`       | Retrieve data          |
| `UPDATE`       | Modify existing rows   |
| `DELETE FROM`  | Delete rows            |
| `ALTER TABLE`  | Modify table structure |
| `DROP TABLE`   | Delete a table         |

## Constraints

| Constraint    | Purpose                     |
| ------------- | --------------------------- |
| `PRIMARY KEY` | Uniquely identifies a row   |
| `FOREIGN KEY` | Connects related tables     |
| `UNIQUE`      | Prevents duplicate values   |
| `NOT NULL`    | Requires a value            |
| `DEFAULT`     | Provides an automatic value |
| `CHECK`       | Restricts allowed values    |

---

# THE BASIC SQL MENTAL MODEL

When working with SQL, think about the task first:

```text
Do I need to CREATE something?
        ↓
CREATE

Do I need to ADD data?
        ↓
INSERT

Do I need to READ data?
        ↓
SELECT

Do I need to CHANGE data?
        ↓
UPDATE

Do I need to REMOVE data?
        ↓
DELETE

Do I need to CHANGE the table structure?
        ↓
ALTER
```

A useful CRUD shortcut is:

```text
C → CREATE
R → READ    → SELECT
U → UPDATE
D → DELETE
```

These four operations form the foundation of working with data in a database.
