## COPY THESE COMMANDS TO CREATE THE TABLES FOR USED ON THIS LESSON

### USERS TABLE

```sql
 CREATE TABLE users(
	id int AUTO_INCREMENT PRIMARY KEY,
 	name VARCHAR(50),
    email varchar(50),
    status varchar(20) DEFAULT 'Active' CHECK(status IN('Active', 'Inactive')),
    age int,
    phone int
);
```

---insert data in `users` table---

```sql
INSERT INTO users (name, email, status, age, phone)
VALUES
('Alice', 'alice@example.com', 'Active', 24, '09171234567'),
('Bob', 'bob@example.com', 'Inactive', 31, NULL),
('Charlie', 'charlie@example.com', 'Active', 19, '09181234567'),
('Diana', 'diana@example.com', 'Active', 42, NULL),
('Ethan', 'ethan@example.com', 'Inactive', 27, '09201234567');

```

## PRODUCTS TABLE

```sql
    CREATE TABLE products(
        id int AUTO_INCREMENT PRIMARY KEY,
        name varchar(100),
        price int
    );

```

-- insert data in `products` table

```sql
INSERT INTO products (product_id, name, price)
VALUES
(1, 'Keyboard', 1000),
(2, 'Mouse', 500),
(3, 'Monitor', 5000);

```

### ORDERS TABLE

```sql
CREATE TABLE orders(
	id int AUTO_INCREMENT PRIMARY KEY,
    user_id int,
    product_id int,
    total int,
    FOREIGN KEY (user_id) REFERENCES users(id),
    FOREIGN KEY (product_id) REFERENCES products(id)
);

```

---insert data in `orders` table

```sql
INSERT INTO orders (order_id, user_id, product_id, total)
VALUES
(1, 1, 1, 500),
(2, 1, 3, 1200),
(3, 2, 2, 800),
(4, 4, 3, 2500),
(5, 4, 1, 300);
```
