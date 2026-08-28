# DATABASE SETUP

Copy these commands to create the tables used on this lesson.

---

## USERS TABLE

### Creating the table

```sql
CREATE TABLE users(
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(50),
    email VARCHAR(50),
    status VARCHAR(20) DEFAULT 'Active' CHECK(status IN ('Active', 'Inactive')),
    age INT,
    phone VARCHAR(20)
);
```

---

### Insert data in `users` table

```sql
INSERT INTO users (name, email, status, age, phone)
VALUES
('Alice', 'alice@example.com', 'Active', 24, '09171234567'),
('Bob', 'bob@example.com', 'Inactive', 31, NULL),
('Charlie', 'charlie@example.com', 'Active', 19, '09181234567'),
('Diana', 'diana@example.com', 'Active', 42, NULL),
('Ethan', 'ethan@example.com', 'Inactive', 27, '09201234567');
```

---

## PRODUCTS TABLE

### Creating the table

```sql
CREATE TABLE products(
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100),
    price INT
);
```

---

### Insert data in `products` table

```sql
INSERT INTO products (name, price)
VALUES
('Keyboard', 1000),
('Mouse', 500),
('Monitor', 5000);
```

---

## ORDERS TABLE

### Creating the table

```sql
CREATE TABLE orders(
    id INT AUTO_INCREMENT PRIMARY KEY,
    user_id INT,
    product_id INT,
    total INT,
    FOREIGN KEY (user_id) REFERENCES users(id),
    FOREIGN KEY (product_id) REFERENCES products(id)
);
```

---

### Insert data in `orders` table

```sql
INSERT INTO orders (user_id, product_id, total)
VALUES
(1, 1, 500),
(1, 3, 1200),
(2, 2, 800),
(4, 3, 2500),
(4, 1, 300);
```

---

# RESULTING TABLES

By the end of the setup, the tables should look like this:

### `users`

|  id | name    | email                                             | status   | age | phone       |
| --: | ------- | ------------------------------------------------- | -------- | --: | ----------- |
|   1 | Alice   | [alice@example.com](mailto:alice@example.com)     | Active   |  24 | 09171234567 |
|   2 | Bob     | [bob@example.com](mailto:bob@example.com)         | Inactive |  31 | `NULL`      |
|   3 | Charlie | [charlie@example.com](mailto:charlie@example.com) | Active   |  19 | 09181234567 |
|   4 | Diana   | [diana@example.com](mailto:diana@example.com)     | Active   |  42 | `NULL`      |
|   5 | Ethan   | [ethan@example.com](mailto:ethan@example.com)     | Inactive |  27 | 09201234567 |

### `products`

|  id | name     | price |
| --: | -------- | ----: |
|   1 | Keyboard |  1000 |
|   2 | Mouse    |   500 |
|   3 | Monitor  |  5000 |

### `orders`

|  id | user_id | product_id | total |
| --: | ------: | ---------: | ----: |
|   1 |       1 |          1 |   500 |
|   2 |       1 |          3 |  1200 |
|   3 |       2 |          2 |   800 |
|   4 |       4 |          3 |  2500 |
|   5 |       4 |          1 |   300 |

---

### Table relationships

```text
users                         orders                         products
─────────────                 ─────────────                 ─────────────
id (PK) ◄──────────────────── user_id (FK)
name                          product_id (FK) ─────────────► id (PK)
email                         total                         name
status                                                        price
age
phone
```

Or, more simply:

```text
users
  │
  │ id
  │
  ▼
orders
  │
  │ product_id
  ▼
products
```
