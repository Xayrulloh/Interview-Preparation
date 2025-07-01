# SQL Interview Questions

## Database Fundamentals
1. ### **What is Database?**  
   *An organized collection of data stored and retrieved digitally from remote/local systems*

2. ### **What is RDBMS? How is it different from DBMS?**  
   - **DBMS:** *Software to define, create and maintain databases*
   - **RDBMS:** *Advanced version with relational capabilities (tables, relations)*

3. ### **Difference between SQL and MySQL?**  
   - **SQL:** *Language for RDBMS*  
   - **MySQL:** *Specific RDBMS product using SQL*

4. ### **Tables and Fields**  
   - **Tables:** *Collections of columns (fields) and rows (records)*  
   - **Fields:** *Columns defining data attributes*

## SQL Commands & Operations
5. ### **SQL Command Categories**  
   - DDL (CREATE, ALTER, DROP, TRUNCATE) \- *to work with tables*
   - DML (INSERT, UPDATE, DELETE) \- *to work with data actions*
   - DQL (SELECT) \- *to retrieve data* 
   - TCL (COMMIT, ROLLBACK) \- *to work with transactions* 
   - DCL (GRANT, REVOKE) \- *to grant/provoke permission*

6. ### **SELECT Statement Fundamentals**  
   - Retrieves data from tables  
   - Common clauses:  
        - **WHERE** *(filtering)*  
        - **ORDER BY** *(sorting*)  
        - **GROUP BY** *(aggregation)*  
        - **HAVING** *(filter groups)*

7. ### **Pattern Matching**  
   *Uses **LIKE/ILIKE** with wildcards:*  
    - **%** (any sequence)  
    - **_** (single character)  
    **Example:** 
        ```sql
        WHERE name LIKE 'J%'
        ```

## Database Objects
8. ### **Creating Table Copies**  
    ```sql
   CREATE TABLE new_table AS SELECT * FROM original_table WHERE 1=0;
   ```

9. ### **Views**  
   *Saved SQL queries acting as virtual tables*

10. ### **Indexes in PostgreSQL**  
    - **B-Tree:*** Default ordered index*  
    - **Hash:** *Fast equality checks*  
    - **Composite:** *Multiple columns*  
    - **Partial:** *Conditional indexing*  
    - **BRIN:** *For large sorted datasets*

## Constraints & Keys
11. ### **Primary Key**  
    *Uniquely identifies rows (UNIQUE + NOT NULL)*

12. ### **Foreign Key**  
    *References primary key in another table*

13. ### **UNIQUE Constraint**  
    *Ensures column values are distinct*

14. ### **Common Constraints**  
    ```sql
    NOT NULL, CHECK, DEFAULT, UNIQUE, PRIMARY KEY, FOREIGN KEY
    ```

## Joins & Relationships
15. ### **Join Types**  
    ![Joins](./images/joins.png)
    - **INNER:** *Matching rows only*  
    - **LEFT/RIGHT:** *All rows from one side*  
    - **FULL:** *All rows from both*  
    - **CROSS:** *Cartesian product*  ![Cross Join](./images/cross-join.png)
    - **SELF:** *Join table to itself*

16. ### **Table Relationships**  
    - One-to-One  
    - One-to-Many  
    - Many-to-Many  
    - Self-Referencing

## Advanced Queries
17. ### **Subqueries**  
    Nested queries used in:  
    - **WHERE** clauses  
    - **FROM** clauses  
    - **SELECT** expressions

18. ### **Set Operations**  
    - **UNION:** *Combine results*  
    - **INTERSECT:** *Common rows*  
    - **MINUS/EXCEPT:** *Row differences*

## Data Modification
19. ### **Data Modification Commands**  
    - **INSERT:** *Add new rows*  
    - **UPDATE:** *Modify existing rows*  
    - **DELETE:** *Remove rows*  
    - **TRUNCATE:** *Empty table*  
    - **DROP:** *Remove table*

20. ### **Column Modification**  
    ```sql
    ALTER TABLE table_name  
    ALTER COLUMN column_name TYPE new_data_type;
    ```

## PostgreSQL Specifics
21. ### **Database Management**  
    - **CREATE DATABASE:** *New database*  
    - **\l:** *List all databases*

22. ### **ACID Compliance**  
    PostgreSQL fully supports:  
    - **Atomicity**  
    - **Consistency**  
    - **Isolation**  
    - **Durability**

23. ### **Commit vs Checkpoint**  
    - **Commit:** *Finalizes transaction*  
    - **Checkpoint:** *Writes changes to disk*

## Database Design
24. ### **Data Normalization**  
    Process to:  
    - Reduce redundancy  
    - Improve integrity  
    Through normal forms (1NF, 2NF, 3NF etc.)

25. ### **Aliases**  
    *Temporary names for columns/tables:* 
    ```sql
    SELECT col AS alias FROM table t;
    ```

## Functions
26. ### **Aggregate Functions**  
    *Operate on value sets:*  
    ```sql
    COUNT(), SUM(), AVG(), MAX(), MIN()
    ```

27. ### **Scalar Functions**  
    *Single-value operations:*  
    ```sql
    UPPER(), LOWER(), ROUND(), NOW()
    ```