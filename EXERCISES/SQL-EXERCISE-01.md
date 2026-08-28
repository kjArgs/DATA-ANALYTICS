# SQL EXERCISE 01 — DATABASE MANIPULATION

> **Prerequisite:** Complete [SQL-0-MANIPULATION-STATEMENTS](../LESSONS/SQL-0-MANIPULATION-STATEMENTS.md).
>
> **Database setup:** Run [SQL-DATABASE-COPY-PASTE](../SQL-DATABASE-COPY-PASTE.md) before starting.
>
> **Important:** Do not create a new database or replace the existing tables. Work with the existing `users`, `products`, and `orders` tables.
>
> **Goal:** Practice adding, modifying, and removing data.

---

## PART 1 — USERS

1. Add a new user named `Frank` with:
   - email: `frank@example.com`
   - status: `Active`
   - age: `28`
   - phone: `09301234567`

2. Display all users to verify that Frank was added.

3. Change Frank's age to `29`.

4. Change Frank's status to `Inactive`.

5. Change Frank's phone number to `09309876543`.

6. Display Frank's record to verify the changes.

7. Delete Frank from the `users` table.

8. Display all users again to verify that Frank was removed.

---

## PART 2 — PRODUCTS

9. Add a new product named `Headset` with a price of `1500`.

10. Display all products to verify that the product was added.

11. Change the price of `Headset` to `1800`.

12. Delete `Headset` from the `products` table.

13. Display all products again to verify that `Headset` was removed.

---

## PART 3 — ALTER TABLE

14. Add a new column named `address` to the `users` table.

15. Add an address for Alice.

16. Display Alice's record to verify that the address was added.

17. Remove the `address` column from the `users` table.

---

## CHALLENGE

18. Add a new user named `Grace`.

19. Give Grace an email and age of your choice.

20. Update Grace's status to `Inactive`.

21. Delete Grace.

22. Verify that the `users` table has returned to its original state.

---

## FINAL CHECK

After completing the exercise, the original database should still contain:

- 5 users
- 3 products
- 5 orders

The temporary records and columns created during the exercise should be removed.
