# Database Isolation Levels

## 1. Introduction

Isolation is one of the ACID properties. It controls how much one transaction can see the work of other transactions that are running at the same time.

Isolation levels provide different balances between data correctness and concurrency.

## 2. Common Concurrency Problems

### Dirty Read

A transaction reads a change made by another transaction before that change is committed.

If the other transaction rolls back, the first transaction has read data that was never permanently saved.

### Non-Repeatable Read

A transaction reads the same row twice and gets different values because another transaction updated and committed that row between the reads.

### Phantom Read

A transaction runs the same search condition twice and gets a different set of rows because another transaction inserted or deleted rows that match the condition.

## 3. Four Standard Isolation Levels

### Read Uncommitted

- Lowest standard isolation level.
- May allow dirty reads.
- Can provide more concurrency.
- Not supported in the same way by every database.

### Read Committed

- A transaction reads only committed data.
- Prevents dirty reads.
- A repeated read may return a changed value.
- Commonly used as a default in PostgreSQL and Oracle.

### Repeatable Read

- Re-reading a row generally gives a stable result within the transaction.
- Prevents dirty reads and non-repeatable reads.
- Phantom-read behaviour depends on the database implementation. Some systems provide stronger protection than the minimum standard.

### Serializable

- Strongest standard isolation level.
- Transactions behave as if they ran one after another in some serial order.
- Provides strong protection against concurrency anomalies.
- May cause transactions to fail and need retrying.

## 4. Comparison

| Isolation level | Dirty read | Non-repeatable read | Phantom read |
|---|---|---|---|
| Read Uncommitted | Possible | Possible | Possible |
| Read Committed | Prevented | Possible | Possible |
| Repeatable Read | Prevented | Prevented | Possible under the SQL standard |
| Serializable | Prevented | Prevented | Prevented |

Actual database behaviour can be stronger than this table. For example, PostgreSQL treats Read Uncommitted as Read Committed and uses snapshot-based behaviour for Repeatable Read.

## 5. Setting an Isolation Level

The syntax differs by database. In PostgreSQL, for example:

```sql
BEGIN TRANSACTION ISOLATION LEVEL SERIALIZABLE;

SELECT *
FROM accounts
WHERE account_id = 1;

COMMIT;
```

The application should handle serialization failures by retrying the complete transaction when it is safe to do so.

## 6. Choosing an Isolation Level

- Use Read Committed for many normal application operations.
- Use Repeatable Read when a transaction needs a stable view of data.
- Use Serializable when correctness requires the strongest standard isolation and the application can handle retries.
- Choose based on the business rules and test concurrent operations.

## 7. Conclusion

Isolation levels control how transactions interact. A higher isolation level can prevent more concurrency problems, but it may reduce concurrency or require retries.
