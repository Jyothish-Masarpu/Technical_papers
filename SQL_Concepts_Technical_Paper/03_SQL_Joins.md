# SQL Joins

## 1. Introduction

A JOIN is used to combine rows from two or more tables using a related column. In a relational database, data is usually stored in separate tables to avoid unnecessary repetition.

For example, we can store customer details in one table and their orders in another table. A JOIN helps us display customer names along with their orders.

## 2. Sample Tables

**customers**

| customer_id | customer_name |
|---:|---|
| 1 | Ravi |
| 2 | Priya |
| 3 | Arun |

**orders**

| order_id | customer_id | amount |
|---:|---:|---:|
| 101 | 1 | 500 |
| 102 | 1 | 300 |
| 103 | 2 | 700 |

## 3. INNER JOIN

INNER JOIN returns only rows that have matching values in both tables.

```sql
SELECT c.customer_name, o.order_id, o.amount
FROM customers AS c
INNER JOIN orders AS o
    ON c.customer_id = o.customer_id;
```

Ravi and Priya appear because they have orders. Arun does not appear because he has no matching order.

## 4. LEFT JOIN

LEFT JOIN returns every row from the left table and matching rows from the right table. If there is no match, the right-side columns contain `NULL`.

```sql
SELECT c.customer_name, o.order_id
FROM customers AS c
LEFT JOIN orders AS o
    ON c.customer_id = o.customer_id;
```

Arun also appears, with `NULL` for the order columns.

## 5. RIGHT JOIN

RIGHT JOIN returns every row from the right table and matching rows from the left table.

```sql
SELECT c.customer_name, o.order_id
FROM customers AS c
RIGHT JOIN orders AS o
    ON c.customer_id = o.customer_id;
```

Every order appears. If an order has no matching customer, the customer columns are `NULL`.

## 6. FULL OUTER JOIN

FULL OUTER JOIN returns matching rows and also unmatched rows from both tables.

```sql
SELECT c.customer_name, o.order_id
FROM customers AS c
FULL OUTER JOIN orders AS o
    ON c.customer_id = o.customer_id;
```

Note: PostgreSQL supports `FULL OUTER JOIN`. MySQL does not provide it directly; it can be written using a `UNION` of a LEFT JOIN and a RIGHT JOIN.

## 7. CROSS JOIN

CROSS JOIN returns every possible combination of rows from the two tables. If the first table has 3 rows and the second has 2 rows, the result has 6 rows.

```sql
SELECT c.customer_name, o.order_id
FROM customers AS c
CROSS JOIN orders AS o;
```

Use it only when all combinations are needed.

## 8. SELF JOIN

A SELF JOIN joins a table with itself. It is useful when rows in the same table are related.

Example: an employee table may store each employee's manager using `manager_id`.

```sql
SELECT
    e.employee_name AS employee,
    m.employee_name AS manager
FROM employees AS e
LEFT JOIN employees AS m
    ON e.manager_id = m.employee_id;
```

## 9. Quick Comparison

| Join | What it returns |
|---|---|
| INNER JOIN | Matching rows from both tables |
| LEFT JOIN | All left rows and matching right rows |
| RIGHT JOIN | All right rows and matching left rows |
| FULL OUTER JOIN | All rows from both sides |
| CROSS JOIN | Every possible combination |
| SELF JOIN | A table joined with itself |

## 10. Conclusion

JOINs are used in real applications to retrieve related information from different tables. The join type depends on whether we need only matching rows or also unmatched rows.
