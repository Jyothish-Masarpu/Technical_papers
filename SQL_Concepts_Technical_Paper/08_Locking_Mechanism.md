# Locking Mechanism in Databases

## 1. Introduction

A lock is a mechanism used by a database to control access to data when multiple transactions run at the same time.

Locks help prevent conflicting operations. For example, two users should not update the same bank balance in a way that causes one update to overwrite the other.

## 2. Why Locks Are Needed

Imagine a product has only one item left. Two customers try to buy it at the same time.

Without proper concurrency control, both requests might read the stock as 1 and both might try to reduce it. The database needs to coordinate these operations so that stock does not become incorrect.

## 3. Shared Lock

A shared lock is generally used when a transaction reads data. Multiple transactions can usually hold shared locks on the same data at the same time.

The exact lock behaviour depends on the database system and isolation level.

## 4. Exclusive Lock

An exclusive lock is generally used when a transaction changes data. It prevents other transactions from making conflicting changes to the same locked data.

For example:

```sql
BEGIN;

UPDATE products
SET stock = stock - 1
WHERE product_id = 10 AND stock > 0;

COMMIT;
```

The database obtains the necessary write lock while performing the update. The condition `stock > 0` also helps prevent stock from becoming negative.

## 5. SELECT FOR UPDATE

Some databases support `SELECT ... FOR UPDATE`. It reads selected rows and locks them for updating until the transaction ends.

```sql
BEGIN;

SELECT stock
FROM products
WHERE product_id = 10
FOR UPDATE;

UPDATE products
SET stock = stock - 1
WHERE product_id = 10 AND stock > 0;

COMMIT;
```

This is useful when an application needs to read a value and then make a decision based on it. Support and details vary by database.

## 6. Row-Level and Table-Level Locks

- **Row-level lock:** Locks selected rows. Other rows may still be available for work.
- **Table-level lock:** Locks a whole table or restricts operations on it.

Row-level locking often allows more concurrent work, while table-level locking can affect many queries.

## 7. Deadlock

A deadlock happens when two or more transactions wait for each other and none can continue.

Example:
- Transaction A locks Row 1 and waits for Row 2.
- Transaction B locks Row 2 and waits for Row 1.

The database usually detects the deadlock and cancels one transaction. The application should be ready to retry a transaction that is safely retryable.

## 8. Good Practices

- Keep transactions short.
- Access rows in a consistent order where possible.
- Do not wait for user input while holding locks.
- Handle deadlock errors and retry when appropriate.
- Lock only the data that needs protection.

## 9. Conclusion

Locking helps databases manage simultaneous reads and writes safely. Good transaction design reduces waiting, conflicts, and deadlocks.
