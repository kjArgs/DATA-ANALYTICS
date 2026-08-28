# SQL Aggregate Functions Problems

> Practice problems for using aggregate functions in SQL.
>
> Try to solve each problem **before looking at the solutions**.
>
> These problems focus on:
>
> ```text
> COUNT()
> SUM()
> MIN()
> MAX()
> AVG()
> ROUND()
> GROUP BY
> HAVING
> ORDER BY
> ```
>
> Try to solve the problems yourself before checking the answer key in **[PROBLEM-AGGREGATE-FUNCTIONS](../CHEATCODES/PROBLEMS/PROBLEM-AGGREGATE-FUNCTIONS.md)**.

---

# Reference Tables

Check [SQL-DATABASE-SETUP](../SQL-DATABASE-SETUP.md) for the whole schema.

The problems in this file use the `startups` table.

## Getting Started

## Problem 1 — Count All Companies

Take a look at the `startups` table. How many columns are there?

---

## Problem 2 — Total Company Count

Calculate the total number of companies in the table.

---

## Problem 3 — Total Valuation

Calculate the total value of all companies in the table by getting the `SUM()` of the `valuation` column.

---

## Problem 4 — Highest Amount Raised

What is the highest amount raised by a startup? Return the maximum amount of money `raised`.

---

## Problem 5 — Highest Amount Raised During Seed Stage

Edit the query so that it returns the maximum amount of money `raised` during the `Seed` stage.

---

## Problem 6 — Oldest Company

In what year was the oldest company on the list founded?

---

# Finding Valuations Among Different Sectors

## Problem 7 — Average Valuation

Return the average `valuation`.

---

## Problem 8 — Average Valuation per Category

Return the average `valuation` in each `category`.

---

## Problem 9 — Rounded Average Valuation per Category

Return the average `valuation` in each `category`. Round the averages to two decimal places.

---

## Problem 10 — Average Valuation per Category, Highest First

Return the average `valuation` in each `category`. Round the averages to two decimal places. Lastly, order the list from highest averages to lowest.

---

# What Are the Most Competitive Markets?

## Problem 11 — Company Count per Category

Return the name of each `category` with the total number of companies that belong to it.

---

## Problem 12 — Categories with More Than 3 Companies

Filter the result to only include categories that have more than three companies in them. What are the most competitive markets?

---

# Startup Sizes Among Different Locations

## Problem 13 — Average Startup Size per Location

What is the average size of a startup in each `location`?

---

## Problem 14 — Locations with Average Size Above 500

What is the average size of a startup in each `location`, with average sizes above 500?
