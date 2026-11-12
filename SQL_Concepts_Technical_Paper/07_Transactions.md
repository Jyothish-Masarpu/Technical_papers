# SQL Transactions

## 1. Introduction

A transaction is a group of database operations treated as one unit. A transaction should complete successfully as a whole or be cancelled.

Transactions are important in banking, shopping, ticket booking, and other systems where partial updates can cause problems.

## 2. Main Transaction Commands

- `START TRANSACTION` or `BEGIN`: Starts a transaction.
- `COMMIT`: Saves the transaction's changes.
- `ROLLBACK`: Cancels uncommitted changes.
- `SAVEPOINT`: Creates a point to which we can roll back within a transaction.

Exact command support and behaviour can vary slightly between database systems.

## 3. Example: Bank Transfer

Assume Account 1 has ₹5,000 and Account 2 has ₹2,000. We want to transfer ₹500 from Account 1 to Account 2.

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

After a successful commit:
- Account 1 has ₹4,500.
- Account 2 has ₹2,500.

Both updates are saved together.

## 4. Using ROLLBACK

If an operation fails, the application can cancel the transaction.

```sql
START TRANSACTION;

UPDATE accounts
SET balance = balance - 500
WHERE account_id = 1;

-- If a problem occurs before commit:
ROLLBACK;
```

The uncommitted update is cancelled.

## 5. Using SAVEPOINT

A savepoint allows us to undo part of a transaction without cancelling everything.

```sql
START TRANSACTION;

UPDATE accounts
SET balance = balance - 500
WHERE account_id = 1;

SAVEPOINT after_debit;

UPDATE accounts
SET balance = balance + 500
WHERE account_id = 2;

ROLLBACK TO SAVEPOINT after_debit;

COMMIT;
```

This example rolls back the second update but commits the first one. It is only an illustration of savepoint behaviour; a real bank transfer should not commit only the debit. The application should roll back the entire transfer if the credit fails.

## 6. Autocommit

Many database tools run each statement in its own transaction by default. This is called autocommit. When we need several statements to succeed together, we should use an explicit transaction.

## 7. Important Points

- Keep transactions as short as possible.
- Commit only after all required operations succeed.
- Roll back when the operation cannot be completed safely.
- Handle errors in application code.
- Use suitable isolation and locking for concurrent updates.

## 8. Conclusion

Transactions help protect data from partial updates. `COMMIT` saves changes, while `ROLLBACK` cancels changes that have not been committed.
