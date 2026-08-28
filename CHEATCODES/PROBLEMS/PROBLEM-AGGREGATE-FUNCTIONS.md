# SQL AGGREGATE FUNCTIONS CHEATCODES

> Solutions for the problems in **[SQL Aggregate Functions Problems](../../PROBLEMS/SQL-PROBLEM-AGGREGATE-FUNCTION.md)**.
>
> Try solving the problems yourself **before checking these**.

---

# AGGREGATE FUNCTIONS

## Problem 1 — Count All Companies

```sql
SELECT COUNT(*)
AS total_company
FROM startups;
```

---

## Problem 2 — Total Company Count

```sql
SELECT COUNT(*)
AS total_company
FROM startups;
```

---

## Problem 3 — Total Valuation

```sql
SELECT SUM(valuation)
AS valuation_sum
FROM startups;
```

---

## Problem 4 — Highest Amount Raised

```sql
SELECT MAX(raised)
AS max_raised_all_time
FROM startups;
```

---

## Problem 5 — Highest Amount Raised During Seed Stage

```sql
SELECT MAX(raised)
AS max_raised_during_seed
FROM startups
WHERE stage = 'Seed';
```

---

## Problem 6 — Oldest Company

```sql
SELECT MIN(founded)
AS oldest_company
FROM startups;
```

---

# AVG() AND GROUP BY

## Problem 7 — Average Valuation

```sql
SELECT AVG(valuation)
AS average
FROM startups;
```

---

## Problem 8 — Average Valuation per Category

```sql
SELECT
    category,
    AVG(valuation) AS average
FROM startups
GROUP BY category;
```

---

## Problem 9 — Rounded Average Valuation per Category

```sql
SELECT
    category,
    ROUND(AVG(valuation), 2) AS average
FROM startups
GROUP BY category;
```

---

## Problem 10 — Average Valuation per Category, Highest First

```sql
SELECT
    category,
    ROUND(AVG(valuation), 2) AS average
FROM startups
GROUP BY category
ORDER BY average DESC;
```

---

# GROUP BY AND COUNT()

## Problem 11 — Company Count per Category

```sql
SELECT
    category,
    COUNT(name) AS company_count
FROM startups
GROUP BY category;
```

---

## Problem 12 — Categories with More Than 3 Companies

```sql
SELECT
    category,
    COUNT(name) AS company_count
FROM startups
GROUP BY category
HAVING COUNT(name) > 3
ORDER BY company_count DESC;
```

---

# AVG() AND GROUP BY — LOCATIONS

## Problem 13 — Average Startup Size per Location

```sql
SELECT
    location,
    ROUND(AVG(employees), 2) AS average_employees
FROM startups
GROUP BY location
ORDER BY average_employees DESC;
```

---

## Problem 14 — Locations with Average Size Above 500

```sql
SELECT
    location,
    ROUND(AVG(employees), 2) AS average_employees
FROM startups
GROUP BY location
HAVING ROUND(AVG(employees), 2) > 500
ORDER BY average_employees DESC;
```
