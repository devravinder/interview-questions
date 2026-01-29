# SQL

## Interview Qs: Ref1

- Types of Joins?
  - Inner, Left, Right, Full, Cross
- Self Join?  
- Find the 10th highest salary from the Employees table.  

  ```sql
  select * from employees order by salary desc limit (10,1) 
  -- using the inner query
  ```

- Find the duplicate records in the table

  ```sql
      SELECT * FROM employees WHERE (name, dept) IN (
        SELECT name, dept
        FROM employees
        GROUP BY name, dept
        HAVING COUNT(*) > 1
      )
    ORDER BY name;

  ```

  ```sql

    SELECT email, COUNT(*)  FROM users GROUP BY email HAVING COUNT(*) > 1; 
    <!-- by email -->


    SELECT name, dept, COUNT(*) FROM employees GROUP BY name, dept HAVING COUNT(*) > 1;
     <!-- Don't include primary key (id) in GROUP BY -->

  ```

- What is the difference between filter clauses → Where vs Having
- Find all the Employees whose salary is duplicated.

  ```sql
  select name, salary from employees group by name having count(salary) > 1
  ```

- What are indices(Index)?
- What are aggregate functions?
- When to use group by and having?
- Type of Indices [Hashing, B-Trees]
- Triggers?
- Stored Procedures?
- Delete vs Truncate vs Drop?
- Can you insert a null value in a unique column?
- Can we use a unique column as a foreign key?
- What is a composite key?
- ACID principles of a transaction?
  - [Ref1](https://www.ibm.com/docs/en/cics-ts/5.4.0?topic=processing-acid-properties-transactions)
  - [Ref2](https://www.geeksforgeeks.org/acid-properties-in-dbms/)
- Normalization rules?
- Master tables vs Ternary tables
- Normal index vs clustered index?
  - [Ref](https://www.geeksforgeeks.org/difference-between-clustered-and-non-clustered-index/)
- Transaction management
- What is a connection pool?
- How to remove/find duplicate records from the table?
  - [Ref1](https://stackoverflow.com/questions/2594829/finding-duplicate-values-in-a-sql-table)

  - ```sql
      SELECT  name, email, COUNT(*) FROM users
       GROUP BY name, email
       HAVING  COUNT(*) > 1
    ```

- Stored Procedure vs Functions
  - [Ref](https://www.dotnettricks.com/learn/sqlserver/difference-between-stored-procedure-and-function-in-sql-server)
- Views
- NVL() and NVL2()
- Sharding vs Partitioning
  - Sharding: Splitting data across MULTIPLE databases/servers
  - Partitioning: Splitting a large table into smaller pieces inside the SAME database/server

---

## NoSQL (Document Databases)

- When to use No-SQL databases?
- SQL vs NoSQL?
- Can we use foreign keys in NoSQL?
  - No
  - But the lookup feature is like foreign keys
- Do NoSQL databases follow ACID principles?
- What is BASE (Basically Available, Soft state, Eventually consistent) in NoSQL

## ACID vs BASE

---

## Links

**Interview Qs:**

1. [Database](https://javarevisited.blogspot.com/2021/05/sql-and-database-phone-interview-questions.html)
