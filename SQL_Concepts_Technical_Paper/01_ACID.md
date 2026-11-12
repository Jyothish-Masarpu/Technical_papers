# ACID Properties in DBMS

## 1. Introduction

ACID is a group of four properties that help a database handle transactions safely. A transaction is one complete unit of database work. For example, transferring money from one bank account to another is a transaction.

ACID stands for:

- Atomicity
- Consistency
- Isolation
- Durability

These properties help prevent incomplete or incorrect data.

## 2. Atomicity

Atomicity means **all operations in a transaction happen, or none of them happen**.

Imagine transferring ₹500 from Account A to Account B. The database must:
1. Subtract ₹500 from Account A.
2. Add ₹500 to Account B.

If the first operation succeeds but the second fails, the database should undo the first operation. This prevents money from disappearing.

```sql
START TRANSACTION;

UPDATE accounts
SET balance = balance - 500
WHERE account_id = 1;

UPDATE accounts
SET balance = balance + 500
WHERE account_id = 2;

COMMIT;
```

If an error occurs before `COMMIT`, we can use `ROLLBACK` to cancel the changes.

## 3. Consistency

Consistency means a transaction must keep the database in a valid state. It should follow all rules such as primary keys, foreign keys, unique values, and check constraints.

For example, an account balance should not become negative if the business rule does not allow it.

```sql
CREATE TABLE accounts (
    account_id INT PRIMARY KEY,
    balance DECIMAL(10, 2) CHECK (balance >= 0)
);
```

The `CHECK` constraint prevents inserting or updating a negative balance.

## 4. Isolation

Isolation means that transactions running at the same time should not create incorrect results by interfering with each other.

For example, two users may try to book the last available seat. The database must manage their transactions so that the same seat is not given to both users.

Database isolation levels control how much one transaction can see the changes made by another transaction.

## 5. Durability

Durability means that once a transaction is committed, its changes are saved permanently. Even if the database server restarts, committed data should remain available.

For example, after a bank transfer is successfully committed, the updated balances should not disappear after a power failure.

## 6. Summary

| Property | Simple meaning |
|---|---|
| Atomicity | All operations succeed or all are cancelled |
| Consistency | Data follows database rules |
| Isolation | Concurrent transactions do not interfere incorrectly |
| Durability | Committed changes are saved permanently |

## 7. Conclusion

ACID properties are important for systems where data correctness matters, such as banking, payments, booking systems, and order processing. They make database transactions reliable and safe.
