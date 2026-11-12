# Indexes in SQL

## 1. Introduction

An index is a database object that helps the database find rows faster. It works somewhat like the index at the back of a book. Instead of reading every page, we use the index to find the required topic.

Without a suitable index, the database may need to scan many or all rows in a table. This is called a table scan.

## 2. Creating an Index

Suppose we often search employees by email.

```sql
CREATE INDEX idx_employees_email
ON employees(email);
```

Now the database has an index it may use when running:

```sql
SELECT *
FROM employees
WHERE email = 'ravi@example.com';
```

The database query planner decides whether using the index is useful. Creating an index does not guarantee that every query will use it.

## 3. Unique Index

A unique index prevents duplicate values in the indexed column or combination of columns.

```sql
CREATE UNIQUE INDEX idx_employees_email_unique
ON employees(email);
```

A `UNIQUE` constraint is often the clearer way to express a business rule:

```sql
ALTER TABLE employees
ADD CONSTRAINT uq_employees_email UNIQUE (email);
```

## 4. Composite Index

A composite index contains more than one column.

```sql
CREATE INDEX idx_department_salary
ON employees(department, salary);
```

It can help queries that filter by `department`, or by `department` and `salary` together. The order of columns matters. This index may not be as useful for a query that filters only by `salary`.

## 5. Advantages

- Can make searches faster.
- Can help with joins, sorting, and filtering.
- Unique indexes can prevent duplicate values.
- Can improve query performance on large tables.

## 6. Disadvantages

- Indexes use additional storage.
- INSERT, UPDATE, and DELETE operations may become slower because indexes also need updating.
- Too many indexes waste space and maintenance effort.
- An index may not help a query that returns a large part of a table.

## 7. Viewing and Removing Indexes

The commands for listing indexes depend on the database system. To remove a known index:

```sql
DROP INDEX idx_employees_email;
```

This form works in PostgreSQL. MySQL uses a different form, such as `DROP INDEX idx_employees_email ON employees`.

## 8. Conclusion

Indexes are useful for improving query performance, especially on columns used often in searches and joins. They should be created based on actual query needs, not on every column.
