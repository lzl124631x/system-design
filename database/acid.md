# ACID

## Atomicity

Either the entire transaction takes place at once or doesn’t happen at all.

There is no midway i.e. transactions do not occur partially. Each transaction is considered as one unit and either runs to completion or is not executed at all. It involves the following two operations.

* **Abort**: If a transaction aborts, changes made to database are not visible.
* **Commit**: If a transaction commits, changes made are visible.

Atomicity is also known as the ‘All or nothing rule’.

## Consistency

This means that integrity constraints must be maintained so that the database is consistent before and after the transaction.

Example: 

The total amount before and after the transaction must be maintained.  
Total **before T** occurs = **500 + 200 = 700**.  
Total **after T occurs** = **400 + 300 = 700**.

## Isolation

This property ensures that multiple transactions can occur concurrently without leading to the inconsistency of database state.

Transactions occur independently without interference. Changes occurring in a particular transaction will not be visible to any other transaction until that particular change in that transaction is written to memory or has been committed. This property ensures that the execution of transactions concurrently will result in a state that is equivalent to a state achieved these were executed serially in some order.

## Durability

This property ensures that once the transaction has completed execution, the updates and modifications to the database are stored in and written to disk and they persist even if a system failure occurs. These updates now become permanent and are stored in non-volatile memory. The effects of the transaction, thus, are never lost.

## Reference

[https://www.geeksforgeeks.org/acid-properties-in-dbms/](https://www.geeksforgeeks.org/acid-properties-in-dbms/)



