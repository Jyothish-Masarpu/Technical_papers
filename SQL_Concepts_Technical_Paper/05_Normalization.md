# Database Normalization

## 1. Introduction

Normalization is the process of organizing database tables to reduce repeated data and avoid data problems.

When the same information is stored many times, updating it can become difficult. Normalization divides data into related tables and connects them using keys.

## 2. Why Normalization Is Needed

Consider a table that stores student and course information:

| student_id | student_name | course_id | course_name |
|---:|---|---:|---|
| 1 | Ravi | 10 | Java |
| 1 | Ravi | 20 | SQL |
| 2 | Priya | 10 | Java |

The student name and course name may be repeated. This can cause three problems:

- **Update anomaly:** If a course name changes, we may need to update many rows.
- **Insertion anomaly:** We may not be able to add a course until a student joins it.
- **Deletion anomaly:** Deleting the last student in a course may also remove the only record of that course.

## 3. First Normal Form (1NF)

A table is in 1NF when:
- Each column contains a single value in each row.
- There are no repeating groups or lists stored in one cell.
- Each row can be identified uniquely.

Bad design:

| student_id | student_name | courses |
|---:|---|---|
| 1 | Ravi | Java, SQL |

Better design:

| student_id | student_name | course |
|---:|---|---|
| 1 | Ravi | Java |
| 1 | Ravi | SQL |

Each cell now contains one value.

## 4. Second Normal Form (2NF)

A table is in 2NF when:
- It is already in 1NF.
- Every non-key column depends on the whole candidate key, not only part of a composite key.

For example, suppose a table uses `(student_id, course_id)` as its primary key. If `student_name` depends only on `student_id`, it does not depend on the full key. This is a partial dependency.

We can split the design into:

**students**

| student_id | student_name |
|---:|---|
| 1 | Ravi |
| 2 | Priya |

**student_courses**

| student_id | course_id |
|---:|---:|
| 1 | 10 |
| 1 | 20 |
| 2 | 10 |

## 5. Third Normal Form (3NF)

A table is in 3NF when:
- It is already in 2NF.
- Non-key columns do not depend on other non-key columns.

For example, if an employee table stores `employee_id`, `department_id`, and `department_name`, the department name depends on department ID, not directly on employee ID.

We can split it into:

**employees**

| employee_id | department_id |
|---:|---:|
| 1 | 10 |
| 2 | 20 |

**departments**

| department_id | department_name |
|---:|---|
| 10 | IT |
| 20 | HR |

## 6. Benefits

- Reduces unnecessary repeated data.
- Makes updates easier.
- Helps avoid insertion, update, and deletion anomalies.
- Improves data organization and consistency.

## 7. Is Normalization Always Better?

Not always. A highly normalized database may need more JOINs to retrieve information. Some systems use controlled denormalization to improve read performance. This should be done carefully to avoid inconsistent copies of data.

## 8. Conclusion

Normalization helps create a clean and reliable database structure. 1NF handles single values, 2NF removes partial dependencies, and 3NF removes transitive dependencies.
