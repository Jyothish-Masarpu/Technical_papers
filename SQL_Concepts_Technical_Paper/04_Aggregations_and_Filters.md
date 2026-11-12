# SQL Aggregations and Filters

## 1. Introduction

SQL filters help us select only the rows we need. Aggregate functions calculate a result from multiple rows, such as a total, average, or count.

These features are commonly used in reports, dashboards, and data analysis.

## 2. Sample Table

Assume we have an `employees` table:

| employee_id | name | department | salary |
|---:|---|---|---:|
| 1 | Ravi | IT | 40000 |
| 2 | Priya | HR | 35000 |
| 3 | Arun | IT | 50000 |
| 4 | Neha | HR | 45000 |

## 3. WHERE

`WHERE` filters individual rows before grouping.

```sql
SELECT *
FROM employees
WHERE salary > 40000;
```

This returns employees whose salary is greater than 40000.

Common operators include `=`, `<>`, `>`, `<`, `>=`, and `<=`.

## 4. AND, OR, and NOT

```sql
SELECT *
FROM employees
WHERE department = 'IT' AND salary > 40000;
```

`AND` requires both conditions to be true.

```sql
SELECT *
FROM employees
WHERE department = 'IT' OR department = 'HR';
```

`OR` requires at least one condition to be true.

```sql
SELECT *
FROM employees
WHERE NOT department = 'HR';
```

`NOT` reverses a condition.

## 5. Other Useful Filters

### IN

Checks whether a value matches any value in a list.

```sql
SELECT *
FROM employees
WHERE department IN ('IT', 'HR');
```

### BETWEEN

Checks whether a value is inside a range, including both limits.

```sql
SELECT *
FROM employees
WHERE salary BETWEEN 35000 AND 45000;
```

### LIKE

Searches text using a pattern. `%` means any number of characters, and `_` means one character.

```sql
SELECT *
FROM employees
WHERE name LIKE 'P%';
```

### IS NULL

Checks for missing values. Do not use `= NULL`.

```sql
SELECT *
FROM employees
WHERE department IS NULL;
```

## 6. Aggregate Functions

Aggregate functions calculate one result from multiple rows.

```sql
SELECT COUNT(*) FROM employees;
```

Common functions:

| Function | Purpose |
|---|---|
| COUNT(*) | Counts rows |
| SUM(salary) | Adds values |
| AVG(salary) | Calculates average |
| MIN(salary) | Finds the smallest value |
| MAX(salary) | Finds the largest value |

Most aggregate functions ignore `NULL` values. `COUNT(*)` counts rows, including rows containing NULLs.

## 7. GROUP BY

`GROUP BY` creates groups of rows with the same value. Aggregate functions can then calculate a result for each group.

```sql
SELECT department, AVG(salary) AS average_salary
FROM employees
GROUP BY department;
```

This returns one average salary for each department.

## 8. HAVING

`HAVING` filters groups after `GROUP BY`. `WHERE` filters rows before grouping.

```sql
SELECT department, AVG(salary) AS average_salary
FROM employees
GROUP BY department
HAVING AVG(salary) > 40000;
```

This returns only departments whose average salary is greater than 40000.

## 9. ORDER BY and LIMIT

```sql
SELECT name, salary
FROM employees
ORDER BY salary DESC
LIMIT 2;
```

`ORDER BY` sorts the result. `DESC` means descending and `ASC` means ascending. `LIMIT` restricts the number of returned rows in PostgreSQL and MySQL.

## 10. Conclusion

Filtering and aggregation help us answer questions such as how many employees are in each department, what the average salary is, and which departments meet a condition.
