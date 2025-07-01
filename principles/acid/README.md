# <center>ACID</center>

ACID is a set of properties that guarantee reliable processing of database
transactions. These principles ensure data integrity even in cases of system
failures or concurrent access.

- ## **Automaticity:**

  **All or nothing** - A transaction is treated as a single, indivisible unit
  that either completes entirely or not at all.

  ```sql
  BEGIN TRANSACTION;
  UPDATE Accounts SET balance = balance - 100 WHERE id = 1;
  UPDATE Accounts SET balance = balance + 100 WHERE id = 2;
  -- If either update fails, both will be rolled back
  COMMIT;
  ```

  Real-world analogy: Imagine a bank transfer between two accounts. The money
  must both leave one account and arrive in the other - it can't just disappear
  from the source without reaching the destination.

<br>

- ## **Consistency:**

  **Follow the rules** - A transaction brings the database from one valid state
  to another, maintaining all defined rules (constraints, cascades, triggers).

  ```sql
  -- Database has constraint: balance >= 0
  BEGIN;
      UPDATE Accounts SET balance = balance - 150 WHERE id = 1;
      -- If this would make balance negative, the entire transaction is aborted
  COMMIT;
  ```

  **Example:** If a database requires that every order must have a customer, the
  consistency property prevents adding an order without a valid customer
  reference.

<br>

- ## **Isolation:**

  **Concurrent transactions don't interfere:** Transactions execute as if they
  were sequential, even when running concurrently.

  ```sql
  -- Transaction 1
  BEGIN;
      SELECT balance FROM Accounts WHERE id = 1; -- Reads 1000
      -- Meanwhile, Transaction 2 updates the balance to 900
      UPDATE Accounts SET balance = 1000 - 100 WHERE id = 1;
      -- Uses original 1000 value due to isolation
  COMMIT;
  ```

  **Isolation levels** (from weakest to strongest):

  - **Read Uncommitted**
  - **Read Committed (default in most databases)**
  - **Repeatable Read**
  - **Serializable**

<br>

- ## **Durability:**

  **Once committed, always there:** Once a transaction is committed, it remains
  committed even in the event of system failure.

  ```sql
  BEGIN;
  INSERT INTO Orders (product_id, quantity) VALUES (123, 5);
  -- After COMMIT, this data is safely stored even if power fails
  COMMIT;
  ```

  **Implementation mechanisms:**

  - **Write-ahead logging (WAL)**
  - **Battery-backed RAM caches**
  - **Replication** to standby servers

<br>
