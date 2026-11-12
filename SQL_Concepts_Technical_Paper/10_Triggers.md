# SQL Triggers

## 1. Introduction

A trigger is a database program that runs automatically when a specified event happens on a table or view.

Common trigger events include:
- INSERT
- UPDATE
- DELETE

Triggers are often used for audit records, automatic checks, and maintaining related data.

## 2. Why Triggers Are Used

Suppose a company wants to keep a record whenever an employee's salary changes. Instead of asking every application to insert an audit record, a trigger can do it automatically in the database.

## 3. Trigger Example in PostgreSQL

First, create an employee table and an audit table.

```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    employee_name VARCHAR(100),
    salary DECIMAL(10, 2)
);

CREATE TABLE salary_audit (
    audit_id SERIAL PRIMARY KEY,
    employee_id INT,
    old_salary DECIMAL(10, 2),
    new_salary DECIMAL(10, 2),
    changed_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

Create a trigger function. In PostgreSQL, a trigger function returns `TRIGGER`.

```sql
CREATE OR REPLACE FUNCTION record_salary_change()
RETURNS TRIGGER AS $$
BEGIN
    INSERT INTO salary_audit (
        employee_id,
        old_salary,
        new_salary
    )
    VALUES (
        OLD.employee_id,
        OLD.salary,
        NEW.salary
    );

    RETURN NEW;
END;
$$ LANGUAGE plpgsql;
```

Now create the trigger:

```sql
CREATE TRIGGER salary_update_trigger
AFTER UPDATE OF salary ON employees
FOR EACH ROW
WHEN (OLD.salary IS DISTINCT FROM NEW.salary)
EXECUTE FUNCTION record_salary_change();
```

When an employee's salary is changed, the trigger automatically inserts the old and new salary into `salary_audit`.

Test it:

```sql
INSERT INTO employees (employee_id, employee_name, salary)
VALUES (1, 'Ravi', 30000);

UPDATE employees
SET salary = 35000
WHERE employee_id = 1;

SELECT * FROM salary_audit;
```

The audit table should contain the old salary 30000 and new salary 35000.

## 4. BEFORE and AFTER Triggers

- **BEFORE trigger:** Runs before the database completes the triggering operation. It can be used to validate or change values before they are stored.
- **AFTER trigger:** Runs after the triggering operation. It is useful for audit work and related actions.

Trigger syntax and available timing options vary between database systems.

## 5. Row-Level and Statement-Level Triggers

- **Row-level trigger:** Runs once for each affected row.
- **Statement-level trigger:** Runs once for the SQL statement, even if it affects many rows.

In PostgreSQL, `FOR EACH ROW` creates a row-level trigger, while `FOR EACH STATEMENT` creates a statement-level trigger.

## 6. Advantages

- Runs automatically when the event occurs.
- Can keep audit information.
- Applies database-side logic even when changes come from different applications.
- Can help maintain related data.

## 7. Disadvantages

- The logic may be hidden from people reading application code.
- Too many triggers can make debugging difficult.
- A trigger can add extra work to INSERT, UPDATE, or DELETE operations.
- Poorly designed triggers can create unexpected side effects.

## 8. Conclusion

Triggers are useful when a database must automatically perform an action after or before a data change. They should be kept simple, documented, and tested carefully.

**Note:** The working trigger example in this paper uses PostgreSQL syntax. MySQL and SQL Server use different trigger syntax.
