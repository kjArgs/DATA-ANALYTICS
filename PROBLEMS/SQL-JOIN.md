# SQL JOIN Problems

Practice problems for building a strong foundation in SQL JOINs.

Try to solve each problem without looking at the answers.

Solutions will be kept separately in [CHEATCODES](../CHEATCODES/PROBLEMS/JOIN.md) folder.

---

# Reference Tables

## `users`

|  id | name    | email               | status   | age | phone       |
| --: | ------- | ------------------- | -------- | --: | ----------- |
|   1 | Alice   | alice@example.com   | active   |  24 | 09171234567 |
|   2 | Bob     | bob@example.com     | inactive |  31 | NULL        |
|   3 | Charlie | charlie@example.com | active   |  19 | 09181234567 |
|   4 | Diana   | diana@example.com   | active   |  42 | NULL        |
|   5 | Ethan   | ethan@example.com   | inactive |  27 | 09201234567 |

## `orders`

|  id | user_id | total |
| --: | ------: | ----: |
|   1 |       1 |   500 |
|   2 |       1 |  1200 |
|   3 |       2 |   800 |
|   4 |       4 |  2500 |
|   5 |       4 |   300 |

## `products`

|  id | name     | price |
| --: | -------- | ----: |
|   1 | Keyboard |  1000 |
|   2 | Mouse    |   500 |
|   3 | Monitor  |  5000 |

## `orders` with `product_id`

For the problems involving products, use this version of `orders`:

|  id | user_id | product_id | total |
| --: | ------: | ---------: | ----: |
|   1 |       1 |          1 |   500 |
|   2 |       1 |          3 |  1200 |
|   3 |       2 |          2 |   800 |
|   4 |       4 |          3 |  2500 |
|   5 |       4 |          1 |   300 |

## Relationships

```text
users.id
    ↑
orders.user_id

products.id
    ↑
orders.product_id
```

---

# JOIN Basics

## Problem 1 — Orders with User Names

Show each order along with the name of the user who placed it.

### Expected result

| order_id | user_name | total |
| -------: | --------- | ----: |
|        1 | Alice     |   500 |
|        2 | Alice     |  1200 |
|        3 | Bob       |   800 |
|        4 | Diana     |  2500 |
|        5 | Diana     |   300 |

---

## Problem 2 — Orders from Active Users

Show the order ID, user name, and total for orders where the user is active.

### Expected result

| order_id | user_name | total |
| -------: | --------- | ----: |
|        1 | Alice     |   500 |
|        2 | Alice     |  1200 |
|        4 | Diana     |  2500 |
|        5 | Diana     |   300 |

---

## Problem 3 — Every User and Their Orders

Show every user and the orders they've made.

Users who have no orders should still appear.

### Expected result

| user_name | order_id | total |
| --------- | -------: | ----: |
| Alice     |        1 |   500 |
| Alice     |        2 |  1200 |
| Bob       |        3 |   800 |
| Charlie   |     NULL |  NULL |
| Diana     |        4 |  2500 |
| Diana     |        5 |   300 |
| Ethan     |     NULL |  NULL |

---

## Problem 4 — Every Active User and Their Orders

Show every active user and their orders.

An active user with no orders should still appear.

### Expected result

| user_name | order_id | total |
| --------- | -------: | ----: |
| Alice     |        1 |   500 |
| Alice     |        2 |  1200 |
| Charlie   |     NULL |  NULL |
| Diana     |        4 |  2500 |
| Diana     |        5 |   300 |

---

## Problem 5 — Orders Greater Than 1,000

Show every user and only their orders greater than 1,000.

Users with no qualifying orders should still appear.

### Expected result

| user_name | order_id | total |
| --------- | -------: | ----: |
| Alice     |        2 |  1200 |
| Bob       |     NULL |  NULL |
| Charlie   |     NULL |  NULL |
| Diana     |        4 |  2500 |
| Ethan     |     NULL |  NULL |

---

## Problem 6 — Orders with Existing Users

Show every order along with the user's name.

Only include orders where the user actually exists.

### Expected result

| order_id | user_name |
| -------: | --------- |
|        1 | Alice     |
|        2 | Alice     |
|        3 | Bob       |
|        4 | Diana     |
|        5 | Diana     |

---

## Problem 7 — Users with No Orders

Find every user who has never placed an order.

### Expected result

| name    |
| ------- |
| Charlie |
| Ethan   |

---

## Problem 8 — Users with at Least One Order

Find every user who has placed at least one order.

Each user should appear only once.

### Expected result

| name  |
| ----- |
| Alice |
| Bob   |
| Diana |

---

## Problem 9 — Order Count per User

Show each user's name and the number of orders they've placed.

Users with no orders should show `0`.

### Expected result

| user_name | order_count |
| --------- | ----------: |
| Alice     |           2 |
| Bob       |           1 |
| Charlie   |           0 |
| Diana     |           2 |
| Ethan     |           0 |

---

## Problem 10 — Total Spending per User

Show every user's name and their total amount spent.

A user with no orders should show `0`.

### Expected result

| user_name | total_spent |
| --------- | ----------: |
| Alice     |        1700 |
| Bob       |         800 |
| Charlie   |           0 |
| Diana     |        2800 |
| Ethan     |           0 |

---

# JOIN Level 2

## Problem 11 — Users with Orders

Show each user's name exactly once if they have placed at least one order.

### Expected result

| name  |
| ----- |
| Alice |
| Bob   |
| Diana |

---

## Problem 12 — Users with at Least 2 Orders

Show every user's name and the number of orders they've placed, but only show users who have placed at least 2 orders.

### Expected result

| user_name | order_count |
| --------- | ----------: |
| Alice     |           2 |
| Diana     |           2 |

---

## Problem 13 — Active Users with at Least 2 Orders

Show each active user's name and number of orders, but only include active users with at least 2 orders.

### Expected result

| user_name | order_count |
| --------- | ----------: |
| Alice     |           2 |

---

## Problem 14 — Users Spending More Than 1,000

For each user, calculate their total amount spent.

Only include users whose total spending is greater than 1,000.

### Expected result

| user_name | total_spent |
| --------- | ----------: |
| Alice     |        1700 |
| Diana     |        2800 |

---

## Problem 15 — Total Spending for Every User

Show every user and their total spending.

Users with no orders should show `0`.

### Expected result

| user_name | total_spent |
| --------- | ----------: |
| Alice     |        1700 |
| Bob       |         800 |
| Charlie   |           0 |
| Diana     |        2800 |
| Ethan     |           0 |

---

## Problem 16 — Count Orders Greater Than 500

Show every user and the number of orders they have placed that are worth more than 500.

Users with no qualifying orders should still appear with `0`.

### Expected result

| user_name | order_count |
| --------- | ----------: |
| Alice     |           1 |
| Bob       |           1 |
| Charlie   |           0 |
| Diana     |           1 |
| Ethan     |           0 |

---

## Problem 17 — Users Spending More Than 1,500

Show each user's name and their total spending.

Only include users whose combined spending is greater than 1,500.

Users with no orders do not need to appear.

### Expected result

| user_name | total_spent |
| --------- | ----------: |
| Alice     |        1700 |
| Diana     |        2800 |

---

## Problem 18 — Orders with User and Product Names

Show each order's ID, the user's name, and the product's name.

### Expected result

| order_id | user_name | product_name |
| -------: | --------- | ------------ |
|        1 | Alice     | Keyboard     |
|        2 | Alice     | Monitor      |
|        3 | Bob       | Mouse        |
|        4 | Diana     | Monitor      |
|        5 | Diana     | Keyboard     |

---

## Problem 19 — Order Count per Product

For each product, show the product name and how many times it has been ordered.

Products that have never been ordered should still appear with `0`.

### Expected result

| product_name | order_count |
| ------------ | ----------: |
| Keyboard     |           2 |
| Mouse        |           1 |
| Monitor      |           2 |

---

## Problem 20 — Monitor Spending by Active User

Show each active user's name and the total amount they have spent on Monitor products.

Only include users who have spent more than 1,000 on Monitor products.

### Expected result

| user_name | monitor_spending |
| --------- | ---------------: |
| Alice     |             1200 |
| Diana     |             2500 |
