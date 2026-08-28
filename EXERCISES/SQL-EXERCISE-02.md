# SQL EXERCISE 02 — QUERY FUNDAMENTALS

> **Prerequisite:** Complete [SQL-01-QUERIES](../LESSONS/SQL-01-QUERIES.md).
>
> **Database setup:** Run [SQL-DATABASE-COPY-PASTE](../SQL-DATABASE-COPY-PASTE.md) before starting.
>
> **Important:** These questions are read-only. Do not use `INSERT`, `UPDATE`, or `DELETE`.
>
> **Goal:** Practice retrieving, filtering, sorting, and categorizing data.

---

## PART 1 — BASIC QUERIES

1. Display all columns from the `users` table.

2. Display only the `name` and `email` of every user.

3. Display the `name` and `age` of every user, but rename `name` to `user_name` in the result.

4. Display all unique user statuses.

5. Display all unique `user_id` values from the `orders` table.

---

## PART 2 — FILTERING

6. Find all users who are older than `25`.

7. Find all users whose status is `Active`.

8. Find all users whose status is not `Active`.

9. Find all users between `20` and `30` years old.

10. Find all orders with a total greater than `1000`.

11. Find all orders with a total between `500` and `1500`.

12. Find all users whose name starts with `A`.

13. Find all users whose name contains the letter `a`.

---

## PART 3 — NULL VALUES

14. Find all users who do not have a phone number.

15. Find all users who have a phone number.

16. Find all orders where the `total` is not `NULL`.

---

## PART 4 — COMBINING CONDITIONS

17. Find all active users who are at least `20` years old.

18. Find all inactive users who are older than `25`.

19. Find products that cost less than `1000` OR more than `4000`.

20. Find orders with a total greater than `500` AND less than `2000`.

---

## PART 5 — SORTING AND LIMITING

21. Display all users from youngest to oldest.

22. Display all users from oldest to youngest.

23. Display the two oldest users.

24. Display the cheapest product.

25. Display the most expensive product.

---

## PART 6 — CASE

26. Display each user's name and age.

27. Add a calculated column named `age_group` using these rules:

- `30` or older → `Adult`
- `20` to `29` → `Young Adult`
- below `20` → `Teen`

28. Display each product's name and price.

29. Add a calculated column named `price_category` using these rules:

- `5000` or higher → `Expensive`
- `1000` or higher → `Moderate`
- below `1000` → `Cheap`

---

## CHALLENGE

30. Find the two oldest active users.

31. Find the three cheapest products.

32. Find all inactive users who have a phone number.

33. Find all users whose name contains the letter `i` and who are younger than `30`.

34. Display the names of users whose age is between `20` and `40`, sorted from oldest to youngest.

35. Display the name and price of the most expensive product.

---

## THINK ABOUT IT

36. Which users have never placed an order?

37. Which products have never been ordered?

> **Do not solve these using JOINs yet.**
>
> Think about whether the information needed to answer these questions exists entirely inside one table.
