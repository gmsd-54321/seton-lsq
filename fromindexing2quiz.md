
# Indexing MCQ Quiz

### ChatGPT

# Advanced SQL Indexing - 40 Expert-Level MCQs

**Difficulty:** 2-year SQL Developer | Advanced | Expert
**Coverage:** Index fundamentals, B-Tree index, clustered/non-clustered indexes, constraint indexes, table scan, index unique scan, index range scan, composite indexes, index selection, incorrect index usage, performance trade-offs and index properties.

**Important:** These questions use conventional B-Tree indexing and cost-based optimizer behaviour. Exact execution plans can vary by database engine, statistics, data distribution and optimizer decisions. Where necessary, the question specifies the expected execution strategy.

---

# Section 1: Index Fundamentals and Properties (Q1-Q8)

**Q1.** Consider the following table:

```sql
CREATE TABLE Employee (
    emp_id INT PRIMARY KEY,
    emp_name VARCHAR(50),
    salary DECIMAL(10,2),
    dept_id INT
);
```

Which statement about indexing is CORRECT?

A. A primary key automatically creates a clustered index in every SQL database.

B. A primary key automatically creates an index to enforce uniqueness, but whether it is clustered depends on the database.

C. An index is created only when the user explicitly executes CREATE INDEX.

D. A primary key does not require an index because uniqueness is checked using a table scan.

**Answer: B**

---

**Q2.** A table contains 10 million records. An index is created on `salary`.

Which statement correctly describes the impact of the index?

A. SELECT, INSERT, UPDATE and DELETE operations all become faster.

B. SELECT queries that can use the index may become faster, but INSERT and DELETE operations generally incur additional maintenance overhead.

C. The index permanently stores a second complete copy of the table.

D. The index eliminates the need for maintaining table statistics.

**Answer: B**

---

**Q3.** Which of the following statements about index storage is CORRECT?

A. Index storage remains constant regardless of the number of table records.

B. Index storage is generally related to the number of indexed entries, indexed column sizes and index structure.

C. Every index consumes exactly 10% of the table's storage.

D. Indexes consume no additional storage because they reference existing table records.

**Answer: B**

---

**Q4.** A table has 5 indexes. A transaction inserts 1,000 new records.

What happens internally in a typical database?

A. Only the table is updated; indexes are refreshed during SELECT operations.

B. The database updates the table and maintains the relevant index entries.

C. All indexes are deleted and recreated after insertion.

D. Index maintenance is the responsibility of the application developer.

**Answer: B**

---

**Q5.** Consider the following statement:

```sql
CREATE UNIQUE INDEX idx_email
ON Employee(email);
```

What is the primary purpose of this index?

A. To physically sort the entire Employee table by email.

B. To enforce uniqueness on email and potentially accelerate searches.

C. To create a foreign key relationship.

D. To prevent NULL values in email.

**Answer: B**

---

**Q6.** Which statement about indexes and data integrity is CORRECT?

A. A non-unique index automatically prevents duplicate values.

B. A unique index can enforce uniqueness of indexed key values.

C. A normal index guarantees that every column has a non-NULL value.

D. A clustered index automatically enforces referential integrity.

**Answer: B**

---

**Q7.** Consider:

```sql
CREATE TABLE Department (
    dept_id INT PRIMARY KEY,
    dept_name VARCHAR(50) UNIQUE
);
```

How many automatically created indexes are typically required to enforce these two constraints?

A. 0

B. 1

C. 2

D. 3

**Answer: C**

---

**Q8.** Which statement about the number of indexes per table is MOST accurate?

A. Every database allows exactly one index per table.

B. Every database allows exactly 249 indexes per table.

C. A table can have multiple indexes, subject to database-specific limits; clustered-index restrictions also depend on the database.

D. A table can have unlimited indexes without affecting performance.

**Answer: C**

---

# Section 2: Clustered and Non-Clustered Indexes (Q9-Q14)

**Q9.** Consider:

```sql
CREATE TABLE Employee (
    emp_id INT PRIMARY KEY,
    emp_name VARCHAR(50),
    salary INT
);
```

Assume the database uses a clustered primary key by default.

What happens when records are inserted with emp_id values 105, 101, 103?

A. The physical organization of the table follows the clustered key order, subject to the database's storage implementation.

B. The records are always physically stored in insertion order.

C. A separate non-clustered index is created automatically instead.

D. The database rejects records inserted out of order.

**Answer: A**

---

**Q10.** Which statement BEST differentiates clustered and non-clustered indexes?

A. Clustered indexes store only index keys, whereas non-clustered indexes store complete table records.

B. A clustered index determines the organization of table rows by its key, whereas a non-clustered index maintains a separate index structure with references to rows.

C. Both indexes always physically sort the complete table.

D. A non-clustered index cannot be created on a primary key.

**Answer: B**

---

**Q11.** A table already has a clustered index on `emp_id`.

The DBA executes:

```sql
CREATE INDEX idx_salary
ON Employee(salary);
```

What is the expected result?

A. The existing clustered index is replaced.

B. A second clustered index is created.

C. A non-clustered index is created on salary.

D. The table is physically sorted by salary.

**Answer: C**

---

**Q12.** Which statement is TRUE regarding clustered indexes?

A. A table can have multiple clustered indexes because each sorts a different column.

B. A table can have only one clustered organization at a time.

C. Clustered indexes cannot be created on primary keys.

D. Clustered indexes do not affect data retrieval.

**Answer: B**

---

**Q13.** A table contains 5 million employee records. A query frequently retrieves employees using:

```sql
SELECT *
FROM Employee
WHERE emp_id = 500;
```

Assume emp_id is the clustered primary key.

Why can this query be efficient?

A. The database searches every record sequentially.

B. The clustered index provides an ordered search structure that leads to the corresponding row.

C. The clustered index creates a duplicate copy of all employee records.

D. The database ignores the WHERE condition.

**Answer: B**

---

**Q14.** Which of the following is NOT a valid general characteristic of a non-clustered index?

A. It maintains a separate index structure.

B. It can contain references to corresponding table rows.

C. Multiple non-clustered indexes can exist on a table.

D. Creating a non-clustered index automatically physically sorts the complete table by that column.

**Answer: D**

---

# Section 3: Table Scan, Index Unique Scan and Index Range Scan (Q15-Q23)

For the following questions, assume:

- `Employee` contains 1 million records.
- `emp_id` has a unique B-Tree index.
- `salary` has a non-unique B-Tree index.
- `dept_id` has no index.
- The optimizer uses an index whenever the question explicitly describes a selective, index-supported lookup.

**Q15.** Consider:

```sql
SELECT *
FROM Employee
WHERE emp_id = 105;
```

Which access method is expected?

A. Table Scan

B. Index Unique Scan

C. Index Range Scan

D. Full Index Scan

**Answer: B**

---

**Q16.** Consider:

```sql
SELECT *
FROM Employee
WHERE salary = 50000;
```

Assume 500 employees have this salary.

Which access method is expected?

A. Table Scan

B. Index Unique Scan

C. Index Range Scan

D. No access method because salary is not unique

**Answer: C**

---

**Q17.** Consider:

```sql
SELECT *
FROM Employee
WHERE dept_id = 10;
```

No index exists on `dept_id`.

Which access method is expected?

A. Index Unique Scan

B. Index Range Scan

C. Table Scan

D. Composite Index Scan

**Answer: C**

---

**Q18.** Consider:

```sql
SELECT *
FROM Employee
WHERE emp_id BETWEEN 100 AND 200;
```

Assume emp_id has a unique B-Tree index.

Which access method is expected?

A. Index Unique Scan

B. Index Range Scan

C. Table Scan in every database

D. Unique Index Scan because emp_id is unique

**Answer: B**

---

**Q19.** Which combination is CORRECT?

A. Index Unique Scan → Retrieves multiple rows using a non-unique condition.

B. Index Range Scan → Retrieves rows matching an indexed range or non-unique key condition.

C. Table Scan → Requires a primary key.

D. Index Unique Scan → Retrieves all rows in the table.

**Answer: B**

---

**Q20.** Consider:

```sql
SELECT *
FROM Employee;
```

The table has an index on emp_id.

Which access method is generally expected?

A. Index Unique Scan

B. Index Range Scan

C. Table Scan

D. Index lookup on emp_id = NULL

**Answer: C**

---

**Q21.** Consider:

```sql
SELECT *
FROM Employee
WHERE emp_id = 100
   OR emp_id = 200;
```

Assume emp_id has a unique index.

Which statement is MOST accurate?

A. It must perform exactly one Index Unique Scan.

B. It can perform multiple index lookups or an equivalent index-based operation.

C. It must perform a table scan because OR is always incompatible with indexes.

D. It cannot use a unique index.

**Answer: B**

---

**Q22.** Consider:

```sql
SELECT *
FROM Employee
WHERE salary >= 30000
  AND salary <= 35000;
```

The salary index exists, but 70% of the table satisfies this condition.

Which execution strategy might the optimizer choose?

A. Index Unique Scan only.

B. Table Scan because retrieving a large portion of rows through the index may be more expensive.

C. Index Unique Scan because salary is numeric.

D. The query cannot execute because salary is not unique.

**Answer: B**

---

**Q23.** Which query is the BEST candidate for an Index Unique Scan?

Assume `emp_id` is a unique indexed column.

A.

```sql
SELECT * FROM Employee
WHERE emp_id > 100;
```

B.

```sql
SELECT * FROM Employee
WHERE emp_id = 100;
```

C.

```sql
SELECT * FROM Employee
WHERE emp_id BETWEEN 100 AND 200;
```

D.

```sql
SELECT * FROM Employee
WHERE emp_id IS NOT NULL;
```

**Answer: B**

---

# Section 4: Correct and Incorrect Index Usage (Q24-Q32)

Assume the following index:

```sql
CREATE INDEX idx_emp_name
ON Employee(emp_name);
```

**Q24.** Which query can directly use the index most effectively?

A.

```sql
SELECT * FROM Employee
WHERE emp_name = 'Arun';
```

B.

```sql
SELECT * FROM Employee
WHERE UPPER(emp_name) = 'ARUN';
```

C.

```sql
SELECT * FROM Employee
WHERE emp_name <> 'Arun';
```

D.

```sql
SELECT * FROM Employee
WHERE emp_name IS NULL;
```

**Answer: A**

---

**Q25.** Consider:

```sql
SELECT *
FROM Employee
WHERE UPPER(emp_name) = 'ARUN';
```

Why might the ordinary index on emp_name not be used?

A. UPPER() is not supported in SQL.

B. Applying a function to the indexed column changes the search expression, so the ordinary index may not directly support the lookup.

C. Indexes cannot be used with string columns.

D. The query always returns zero rows.

**Answer: B**

---

**Q26.** Consider:

```sql
SELECT *
FROM Employee
WHERE emp_name LIKE '%run';
```

Assume a conventional B-Tree index on emp_name.

Why is the index generally unsuitable for an efficient range lookup?

A. LIKE cannot be used with VARCHAR.

B. The leading wildcard prevents the database from identifying a fixed starting point in the index.

C. The index supports only numeric columns.

D. The query requires a unique index.

**Answer: B**

---

**Q27.** Consider:

```sql
SELECT *
FROM Employee
WHERE emp_name LIKE 'Arun%';
```

Which statement is CORRECT?

A. A conventional B-Tree index may support this prefix search.

B. A conventional B-Tree index can never support LIKE.

C. A table scan is compulsory.

D. The index can be used only if emp_name is a primary key.

**Answer: A**

---

**Q28.** Consider:

```sql
SELECT *
FROM Employee
WHERE salary <> 50000;
```

An index exists on salary.

Why might the optimizer choose a table scan?

A. Negative conditions are syntactically invalid.

B. The condition may match most records, making index access less efficient than scanning the table.

C. Indexes support only equality conditions.

D. The database automatically deletes the index when

is used.

**Answer: B**

---

**Q29.** Consider:

```sql
CREATE INDEX idx_emp_dept_salary
ON Employee(dept_id, salary);
```

Which query can use the index through its leading column?

A.

```sql
SELECT *
FROM Employee
WHERE salary = 50000;
```

B.

```sql
SELECT *
FROM Employee
WHERE dept_id = 10;
```

C.

```sql
SELECT *
FROM Employee
WHERE UPPER(dept_id) = 10;
```

D.

```sql
SELECT *
FROM Employee
WHERE salary > 50000;
```

**Answer: B**

---

**Q30.** Given:

```sql
CREATE INDEX idx_dept_salary
ON Employee(dept_id, salary);
```

Consider:

```sql
SELECT *
FROM Employee
WHERE salary = 50000
  AND dept_id = 10;
```

Will the index be usable?

A. No, because dept_id must appear first in the WHERE clause.

B. Yes, because the optimizer can use the indexed leading column regardless of the order of predicates in the WHERE clause.

C. No, because composite indexes cannot support equality conditions.

D. Yes, but only if salary is unique.

**Answer: B**

---

**Q31.** Given:

```sql
CREATE INDEX idx_dept_salary
ON Employee(dept_id, salary);
```

Consider:

```sql
SELECT *
FROM Employee
WHERE dept_id = 10
  AND salary > 50000;
```

Which statement is CORRECT?

A. The index cannot be used because it contains two columns.

B. The index can use dept_id equality followed by a salary range lookup.

C. Only salary can be used because it has a range condition.

D. A table scan is compulsory.

**Answer: B**

---

**Q32.** Given:

```sql
CREATE INDEX idx_dept_salary
ON Employee(dept_id, salary);
```

Which query is the LEAST suitable for using this index through its leading key?

A.

```sql
SELECT * FROM Employee
WHERE dept_id = 10;
```

B.

```sql
SELECT * FROM Employee
WHERE dept_id = 10 AND salary = 50000;
```

C.

```sql
SELECT * FROM Employee
WHERE dept_id = 10 AND salary > 50000;
```

D.

```sql
SELECT * FROM Employee
WHERE salary = 50000;
```

**Answer: D**

---

# Section 5: Composite Indexes - Expert-Level Scenarios (Q33-Q37)

Consider this table and indexes:

```sql
CREATE TABLE Orders (
    order_id INT PRIMARY KEY,
    customer_id INT,
    order_date DATE,
    status VARCHAR(20),
    amount DECIMAL(10,2)
);
```

The following indexes exist:

```sql
CREATE INDEX idx_customer_date
ON Orders(customer_id, order_date);

CREATE INDEX idx_status_amount
ON Orders(status, amount);

CREATE INDEX idx_order_date
ON Orders(order_date);
```

**Q33.** Which query can most effectively use `idx_customer_date`?

A.

```sql
SELECT * FROM Orders
WHERE order_date = '2026-01-01';
```

B.

```sql
SELECT * FROM Orders
WHERE customer_id = 101;
```

C.

```sql
SELECT * FROM Orders
WHERE amount > 5000;
```

D.

```sql
SELECT * FROM Orders
WHERE status = 'DELIVERED';
```

**Answer: B**

---

**Q34.** Consider:

```sql
SELECT *
FROM Orders
WHERE customer_id = 101
  AND order_date BETWEEN '2026-01-01' AND '2026-01-31';
```

Which index is the best match?

A. idx_status_amount

B. idx_order_date

C. idx_customer_date

D. None of the indexes

**Answer: C**

---

**Q35.** Consider:

```sql
SELECT *
FROM Orders
WHERE status = 'DELIVERED'
  AND amount > 5000;
```

Which index is the best match?

A. idx_customer_date

B. idx_status_amount

C. idx_order_date

D. None of the indexes

**Answer: B**

---

**Q36.** Consider:

```sql
SELECT *
FROM Orders
WHERE amount > 5000
  AND status = 'DELIVERED';
```

Which statement is CORRECT?

A. The index cannot be used because amount appears first in the WHERE clause.

B. idx_status_amount can be used because the index's leading column is constrained, regardless of predicate order.

C. Only idx_order_date can be used.

D. The query must perform a table scan because it has two conditions.

**Answer: B**

---

**Q37.** Consider:

```sql
SELECT *
FROM Orders
WHERE customer_id = 101
  AND status = 'DELIVERED';
```

Available indexes:

- idx_customer_date(customer_id, order_date)
- idx_status_amount(status, amount)

Which statement is MOST accurate?

A. Both indexes necessarily provide an equally efficient lookup for the complete condition.

B. Either index may help with its leading-column predicate; the optimizer may choose one, combine access paths if supported, or choose another strategy based on cost.

C. Neither index can be used because both columns must be in the same composite index.

D. idx_order_date must be used.

**Answer: B**

---

# Section 6: Advanced Index Properties and Performance (Q38-Q40)

**Q38.** A table initially has one index. Over time, the DBA creates 15 additional indexes on frequently queried columns.

What is the most likely consequence?

A. All SELECT queries become faster and INSERT operations remain unchanged.

B. SELECT performance may improve for suitable queries, but INSERT, UPDATE and DELETE operations can become more expensive due to index maintenance.

C. Index storage decreases because indexes share the same structure.

D. The database automatically merges all indexes into one.

**Answer: B**

---

**Q39.** Consider:

```sql
CREATE TABLE Employee (
    emp_id INT PRIMARY KEY,
    email VARCHAR(100) UNIQUE,
    salary INT
);
```

Which statement is CORRECT?

A. No indexes are automatically created because indexes must always be created manually.

B. Indexes are typically created to enforce the primary key and unique constraint.

C. All three columns automatically receive unique indexes.

D. Only salary receives an automatic index.

**Answer: B**

---

**Q40.** A DBA wants to identify indexes associated with a table. Which statement is CORRECT?

A. Index information can be inspected through database-specific system catalog views or metadata tables.

B. Indexes can only be identified by running SELECT * on the table.

C. Index names are stored inside every table row.

D. Index metadata is never accessible to database users.

**Answer: A**

---

# Answer Key - Quick Revision

| Question | Answer | Question | Answer |
| --- | --- | --- | --- |
| 1 | B | 21 | B |
| 2 | B | 22 | B |
| 3 | B | 23 | B |
| 4 | B | 24 | A |
| 5 | B | 25 | B |
| 6 | B | 26 | B |
| 7 | C | 27 | A |
| 8 | C | 28 | B |
| 9 | A | 29 | B |
| 10 | B | 30 | B |
| 11 | C | 31 | B |
| 12 | B | 32 | D |
| 13 | B | 33 | B |
| 14 | D | 34 | C |
| 15 | B | 35 | B |
| 16 | C | 36 | B |
| 17 | C | 37 | B |
| 18 | B | 38 | B |
| 19 | B | 39 | B |
| 20 | C | 40 | A |

---

## Important exam traps to remember

| Concept | Correct understanding |
| --- | --- |
| Primary key | Typically creates an index automatically |
| UNIQUE constraint | Typically creates an index automatically |
| Clustered index | One clustered organization per table |
| Non-clustered index | Multiple can exist |
| Index Unique Scan | Unique key equality lookup |
| Index Range Scan | Range or non-unique indexed lookup |
| Table Scan | Reads table rows without relying on a selective index lookup |
| Composite index | Leading-column principle |
| WHERE condition order | Does not determine composite index usability |
| Function on indexed column | May prevent ordinary index usage |
| `LIKE 'ABC%'` | Can use a conventional B-Tree index |
| `LIKE '%ABC'` | Generally cannot use a conventional B-Tree prefix lookup |
| Negative criteria | May be inefficient when most rows qualify |
| Additional indexes | Increase storage and write overhead |
| Index maintenance | Generally automatic after creation |

**One important correction for HSQLDB preparation:** Don't memorize the claims that every primary key automatically creates a clustered index, that every database has a 249-index limit, or that every qualifying query must use an index. These are not universal SQL rules. Execution plans and index behavior are database-specific.

### ChatGPT

# DCL (Data Control Language) - 40 Advanced Expert-Level MCQs

(2-Year SQL Developer Level) (HSQLDB Focus)

**Topics covered:**

- DCL purpose and access control
- GRANT and REVOKE syntax
- Grantor, grantee and privileges
- Object privileges: SELECT, INSERT, UPDATE, DELETE, ALL
- Table-level and column-level privileges
- View privileges
- Routine (procedure/function) privileges
- Sequence privileges
- Granting privileges to users and roles
- Role-based access control
- Multiple grantees
- REVOKE edge cases
- Privilege inheritance and dependencies
- Tricky SQL statements and output-based questions

**Assumption:** Questions use SQL-standard-style privilege semantics supported by HSQLDB where applicable. Database-specific syntax and privilege support can differ by HSQLDB version.

---

# Section 1: DCL Fundamentals and GRANT Syntax (Q1-Q8)

**Q1.** Which of the following statements correctly describes DCL?

A. DCL is responsible for creating and modifying database structures.

B. DCL controls access permissions and privileges on database objects.

C. DCL is responsible for inserting and deleting table records.

D. DCL is responsible for transaction management only.

**Answer: B**

---

**Q2.** Consider the following statement:

```sql
GRANT SELECT ON Employee TO user1;
```

Identify the correct interpretation.

A. user1 receives permission to modify Employee records.

B. user1 receives permission to retrieve records from Employee.

C. user1 receives ownership of Employee.

D. user1 receives permission to create indexes on Employee.

**Answer: B**

---

**Q3.** Which is the correct general syntax for granting an object privilege?

A.

```sql
GRANT user1 ON Employee TO SELECT;
```

B.

```sql
GRANT SELECT ON Employee TO user1;
```

C.

```sql
GRANT Employee TO user1 SELECT;
```

D.

```sql
GRANT ON Employee SELECT FROM user1;
```

**Answer: B**

---

**Q4.** Consider:

```sql
GRANT SELECT, INSERT, UPDATE
ON Employee
TO user1;
```

Which statement is CORRECT?

A. user1 receives only SELECT permission.

B. user1 receives SELECT, INSERT and UPDATE permissions.

C. user1 receives all possible privileges on Employee.

D. user1 receives permission to delete Employee records.

**Answer: B**

---

**Q5.** Consider:

```sql
GRANT ALL PRIVILEGES
ON Employee
TO user1;
```

What does this statement mean?

A. user1 receives every possible system privilege in the database.

B. user1 receives all applicable grantable object privileges on Employee.

C. user1 becomes the database administrator.

D. user1 receives ownership of the entire database.

**Answer: B**

---

**Q6.** Which statement about GRANT is CORRECT?

A. GRANT can provide privileges only to users, never roles.

B. GRANT can provide privileges to users and roles.

C. GRANT can provide privileges only to database administrators.

D. GRANT can provide privileges only on tables.

**Answer: B**

---

**Q7.** Consider:

```sql
GRANT SELECT ON Employee
TO user1, user2, user3;
```

What is the result?

A. Only user1 receives SELECT permission.

B. All three specified grantees receive SELECT permission.

C. user1 receives SELECT, user2 receives INSERT and user3 receives UPDATE.

D. The statement is invalid because only one grantee is allowed.

**Answer: B**

---

**Q8.** Which of the following correctly identifies the components of this statement?

```sql
GRANT UPDATE ON Employee TO developer_role;
```

A. UPDATE = grantee, Employee = grantor, developer_role = privilege.

B. UPDATE = privilege, Employee = object, developer_role = grantee.

C. UPDATE = object, Employee = privilege, developer_role = grantor.

D. UPDATE = grantor, Employee = grantee, developer_role = object.

**Answer: B**

---

# Section 2: Table-Level and Column-Level Privileges (Q9-Q16)

Consider the following table:

```sql
Employee(
    emp_id,
    emp_name,
    salary,
    department
)
```

**Q9.** Consider:

```sql
GRANT SELECT ON Employee TO user1;
```

What can user1 do?

A. Retrieve only emp_id and emp_name.

B. Retrieve all columns from Employee, subject to other access restrictions.

C. Retrieve and update all columns.

D. Retrieve only the primary key.

**Answer: B**

---

**Q10.** Consider:

```sql
GRANT UPDATE(salary)
ON Employee
TO user1;
```

What permission is provided?

A. user1 can update every column in Employee.

B. user1 can update only the salary column through this column-level privilege.

C. user1 can retrieve only salary.

D. user1 can delete records having a particular salary.

**Answer: B**

---

**Q11.** Consider:

```sql
GRANT UPDATE(salary, department)
ON Employee
TO user1;
```

Which operation is permitted through the granted privilege?

A.

```sql
UPDATE Employee
SET salary = 50000;
```

B.

```sql
UPDATE Employee
SET department = 'IT';
```

C.

```sql
UPDATE Employee
SET salary = 50000,
    department = 'IT';
```

D. All of the above.

**Answer: D**

---

**Q12.** Consider:

```sql
GRANT UPDATE(salary)
ON Employee
TO user1;
```

Which query is permitted through this privilege alone?

A.

```sql
UPDATE Employee
SET emp_name = 'Arun'
WHERE emp_id = 10;
```

B.

```sql
UPDATE Employee
SET salary = 60000
WHERE emp_id = 10;
```

C.

```sql
DELETE FROM Employee
WHERE emp_id = 10;
```

D.

```sql
INSERT INTO Employee(emp_id, emp_name)
VALUES(10, 'Arun');
```

**Answer: B**

---

**Q13.** Consider:

```sql
GRANT SELECT(emp_id, emp_name)
ON Employee
TO user1;
```

Which statement is CORRECT under SQL column-level privilege semantics?

A. user1 can SELECT every column.

B. user1 can SELECT the specified columns, but not automatically salary.

C. user1 can update emp_id and emp_name.

D. user1 can delete Employee records.

**Answer: B**

---

**Q14.** Consider:

```sql
GRANT SELECT, UPDATE(salary)
ON Employee
TO user1;
```

Which statement is CORRECT?

A. user1 can retrieve all columns and update salary.

B. user1 can retrieve only salary and update all columns.

C. user1 can retrieve and update all columns.

D. The statement is invalid because SELECT and UPDATE cannot be combined.

**Answer: A**

---

**Q15.** Consider:

```sql
GRANT DELETE ON Employee TO user1;
```

Which operation is allowed?

A.

```sql
DELETE FROM Employee
WHERE emp_id = 10;
```

B.

```sql
UPDATE Employee
SET salary = 50000;
```

C.

```sql
INSERT INTO Employee(emp_id)
VALUES(10);
```

D.

```sql
ALTER TABLE Employee
ADD COLUMN age INT;
```

**Answer: A**

---

**Q16.** Consider:

```sql
GRANT SELECT ON Employee TO user1;

GRANT UPDATE(salary) ON Employee TO user1;
```

Which statement is CORRECT?

A. The second GRANT replaces the first GRANT.

B. user1 receives SELECT on Employee and UPDATE on salary.

C. user1 receives UPDATE on all columns.

D. The first GRANT becomes invalid after the second GRANT.

**Answer: B**

---

# Section 3: REVOKE and Its Edge Cases (Q17-Q24)

**Q17.** Which is the correct syntax for revoking a privilege?

A.

```sql
REVOKE SELECT ON Employee FROM user1;
```

B.

```sql
REVOKE user1 ON Employee SELECT;
```

C.

```sql
REMOVE SELECT ON Employee FROM user1;
```

D.

```sql
DELETE SELECT FROM Employee WHERE USER = user1;
```

**Answer: A**

---

**Q18.** Consider:

```sql
GRANT SELECT, INSERT, UPDATE
ON Employee
TO user1;
```

Then:

```sql
REVOKE INSERT
ON Employee
FROM user1;
```

Which privileges remain?

A. Only INSERT.

B. SELECT and UPDATE.

C. No privileges.

D. Only SELECT.

**Answer: B**

---

**Q19.** Consider:

```sql
GRANT UPDATE(salary, department)
ON Employee
TO user1;
```

Then:

```sql
REVOKE UPDATE(salary)
ON Employee
FROM user1;
```

Which statement is CORRECT under column-level privilege semantics?

A. All UPDATE privileges are revoked.

B. UPDATE permission on salary is revoked, while department permission remains.

C. SELECT permission is revoked.

D. The entire table is deleted.

**Answer: B**

---

**Q20.** Consider:

```sql
GRANT SELECT ON Employee TO user1;

REVOKE SELECT ON Employee FROM user1;
```

What is the resulting privilege state?

A. user1 retains SELECT permission.

B. user1 loses the directly granted SELECT permission, unless another authorization path provides it.

C. user1 becomes the owner of Employee.

D. All other users lose SELECT permission.

**Answer: B**

---

**Q21.** Consider:

```sql
GRANT SELECT ON Employee TO user1;

GRANT UPDATE ON Employee TO user1;

REVOKE SELECT ON Employee FROM user1;
```

Which privileges does user1 retain through these direct grants?

A. SELECT only.

B. UPDATE only.

C. SELECT and UPDATE.

D. No privileges.

**Answer: B**

---

**Q22.** Consider:

```sql
GRANT SELECT ON Employee TO user1;

GRANT SELECT ON Employee TO user2;
```

Then:

```sql
REVOKE SELECT ON Employee FROM user1;
```

What happens to user2's SELECT privilege?

A. It is also revoked.

B. It remains unaffected.

C. user2 becomes the owner of Employee.

D. The Employee table becomes inaccessible to everyone.

**Answer: B**

---

**Q23.** Consider:

```sql
GRANT SELECT ON Employee TO user1 WITH GRANT OPTION;
```

What additional capability does user1 receive?

A. user1 can grant SELECT permission on Employee to other users, within the authority of the grant.

B. user1 can drop Employee.

C. user1 becomes a database administrator.

D. user1 can grant every privilege on every database object.

**Answer: A**

---

**Q24.** Consider:

```sql
GRANT SELECT ON Employee TO user1 WITH GRANT OPTION;

GRANT SELECT ON Employee TO user2;
```

Assume user1 granted SELECT to user2. Later, user1's SELECT privilege is revoked with CASCADE.

What is the expected SQL-standard behavior?

A. user2 always retains the privilege.

B. user2's dependent grant can also be revoked.

C. user2 automatically becomes the table owner.

D. The Employee table is dropped.

**Answer: B**

---

# Section 4: Privileges on Views, Routines and Sequences (Q25-Q32)

Consider:

```sql
CREATE VIEW IT_Employees AS
SELECT emp_id, emp_name
FROM Employee
WHERE department = 'IT';
```

**Q25.** Consider:

```sql
GRANT SELECT ON IT_Employees TO user1;
```

What does user1 receive?

A. SELECT permission on the entire Employee table automatically.

B. SELECT permission on the IT_Employees view.

C. UPDATE permission on Employee.

D. Ownership of IT_Employees.

**Answer: B**

---

**Q26.** Assume user1 has SELECT permission on a view but no direct SELECT permission on its underlying table.

Which statement is MOST accurate?

A. Access through the view may be possible depending on view definition, ownership and underlying privilege-checking rules.

B. Access is always impossible.

C. user1 automatically receives permanent SELECT permission on the underlying table.

D. The view is automatically dropped.

**Answer: A**

---

**Q27.** Consider:

```sql
GRANT SELECT ON IT_Employees TO user1;

REVOKE SELECT ON IT_Employees FROM user1;
```

What is revoked?

A. SELECT permission on the Employee table in every case.

B. SELECT permission on the specified view.

C. UPDATE permission on Employee.

D. All database privileges belonging to user1.

**Answer: B**

---

**Q28.** Which privilege is associated with executing a stored procedure or function?

A. SELECT

B. EXECUTE

C. DELETE

D. ALTER

**Answer: B**

---

**Q29.** Consider the following conceptual statement:

```sql
GRANT EXECUTE ON PROCEDURE calculate_salary
TO user1;
```

What does it intend to provide?

A. Permission to retrieve procedure source code only.

B. Permission to execute the specified procedure.

C. Permission to drop the procedure.

D. Permission to modify all tables used by the procedure.

**Answer: B**

---

**Q30.** Consider a database sequence named `emp_seq`.

Which statement correctly identifies common sequence privileges in SQL-standard-style systems?

A. SELECT, INSERT and DELETE are the only sequence privileges.

B. USAGE and SELECT may be relevant sequence privileges, depending on the operation and implementation.

C. UPDATE(salary) is required to access a sequence.

D. DELETE is required to generate the next sequence value.

**Answer: B**

---

**Q31.** A user receives EXECUTE permission on a stored procedure that inserts records into Employee.

The user does not have direct INSERT permission on Employee.

Which statement is CORRECT?

A. The procedure can never execute.

B. The procedure may execute successfully depending on whether it uses definer or invoker rights and the applicable privilege rules.

C. EXECUTE automatically grants permanent INSERT permission on Employee.

D. The user automatically becomes the owner of Employee.

**Answer: B**

---

**Q32.** Which of the following object types can be associated with object-level privileges in SQL systems, depending on the database implementation?

A. Tables only.

B. Tables and views only.

C. Tables, views, routines and sequences.

D. Only database schemas.

**Answer: C**

---

# Section 5: Roles, Users and Privilege Inheritance (Q33-Q37)

**Q33.** Consider:

```sql
CREATE ROLE developer_role;

GRANT SELECT ON Employee
TO developer_role;

GRANT developer_role
TO user1;
```

What is the expected result?

A. user1 receives the role's privileges according to the role activation and authorization rules.

B. user1 becomes the owner of Employee.

C. developer_role receives ownership of user1.

D. user1 receives only INSERT permission.

**Answer: A**

---

**Q34.** Consider:

```sql
GRANT SELECT ON Employee TO user1;

GRANT UPDATE ON Employee TO developer_role;

GRANT developer_role TO user1;
```

Which statement is CORRECT?

A. user1 has SELECT and UPDATE through the direct grant and role membership, respectively.

B. user1 has only SELECT.

C. user1 has only UPDATE.

D. The direct SELECT privilege is replaced by the role membership.

**Answer: A**

---

**Q35.** Consider:

```sql
GRANT SELECT ON Employee TO developer_role;

GRANT developer_role TO user1;

REVOKE SELECT ON Employee FROM developer_role;
```

What happens to user1's SELECT access obtained through that role?

A. It remains permanently available through the revoked role privilege.

B. The role no longer supplies that SELECT privilege to user1.

C. user1 automatically receives direct SELECT permission.

D. The role is automatically deleted.

**Answer: B**

---

**Q36.** Consider:

```sql
GRANT SELECT ON Employee TO user1;

GRANT SELECT ON Employee TO developer_role;

GRANT developer_role TO user1;

REVOKE SELECT ON Employee FROM developer_role;
```

What is the resulting access state?

A. user1 loses SELECT completely.

B. user1 retains SELECT through the direct grant.

C. user1 receives DELETE permission.

D. user1 loses all privileges on Employee.

**Answer: B**

---

**Q37.** Which statement correctly differentiates granting a privilege to a user and granting a privilege to a role?

A. Both are impossible in SQL.

B. A privilege granted to a user is directly assigned to that user, whereas a privilege granted to a role can be made available to users who receive that role, subject to role activation and authorization rules.

C. A role cannot receive SELECT permission.

D. A user cannot receive multiple roles.

**Answer: B**

---

# Section 6: Expert-Level Mixed Scenarios (Q38-Q40)

**Q38.** Consider:

```sql
GRANT SELECT, UPDATE(salary)
ON Employee
TO user1;

GRANT DELETE
ON Employee
TO user1;

REVOKE UPDATE(salary)
ON Employee
FROM user1;
```

Which privileges remain?

A. SELECT and DELETE.

B. UPDATE and DELETE.

C. Only SELECT.

D. No privileges.

**Answer: A**

---

**Q39.** Consider:

```sql
GRANT ALL PRIVILEGES
ON Employee
TO developer_role;

GRANT developer_role TO user1;

REVOKE ALL PRIVILEGES
ON Employee
FROM developer_role;
```

Which statement is CORRECT?

A. user1 permanently retains all privileges previously obtained through developer_role.

B. Privileges supplied through developer_role are no longer available after their revocation, but independently granted privileges may remain.

C. user1 automatically becomes the owner of Employee.

D. All privileges of every database user are revoked.

**Answer: B**

---

**Q40.** A DBA executes:

```sql
GRANT SELECT ON Employee TO user1;

GRANT SELECT ON Employee TO developer_role;

GRANT developer_role TO user1;

REVOKE SELECT ON Employee FROM user1;
```

Assume the REVOKE removes the direct grant only.

What is the resulting access state?

A. user1 cannot SELECT Employee because all SELECT grants are revoked together.

B. user1 can still obtain SELECT access through developer_role.

C. developer_role loses SELECT permission.

D. Employee is no longer accessible to any user.

**Answer: B**

---

# Additional 15-Question Rapid Revision Quiz

These questions focus on subtle syntax, privilege boundaries and edge cases.

**Q41.** Which statement is valid for granting SELECT on a table to two roles?

A.

```sql
GRANT SELECT ON Employee TO role1, role2;
```

B.

```sql
GRANT role1, role2 ON Employee SELECT;
```

C.

```sql
GRANT Employee SELECT TO role1, role2;
```

D.

```sql
GRANT SELECT FROM Employee TO role1, role2;
```

**Answer: A**

---

**Q42.** A user has UPDATE(salary) but no SELECT privilege. Which statement is CORRECT?

A. The user automatically receives SELECT permission because UPDATE requires it.

B. The UPDATE privilege alone does not automatically grant SELECT permission.

C. The user automatically receives DELETE permission.

D. The user becomes the table owner.

**Answer: B**

---

**Q43.** Consider:

```sql
GRANT SELECT ON Employee TO user1 WITH GRANT OPTION;
```

Can user1 grant SELECT to another user?

A. Yes, within the scope of the grant option.

B. No, only database administrators can grant privileges.

C. Yes, and user1 automatically becomes the table owner.

D. No, SELECT cannot be granted to other users.

**Answer: A**

---

**Q44.** Which statement about REVOKE is CORRECT?

A. REVOKE deletes the database object.

B. REVOKE removes specified privileges from the specified grantee.

C. REVOKE permanently deletes the grantee.

D. REVOKE automatically removes every privilege from all users.

**Answer: B**

---

**Q45.** Consider:

```sql
GRANT SELECT ON Employee TO user1;

GRANT SELECT ON Employee TO user1;
```

Which statement is MOST accurate?

A. The second grant creates a second independent SELECT privilege that must always be revoked twice.

B. Repeating the grant does not normally create a second distinct effective privilege assignment.

C. The second grant removes SELECT permission.

D. The second grant changes SELECT into UPDATE.

**Answer: B**

---

**Q46.** A user has SELECT on a view but the view references three underlying tables.

Which statement is CORRECT?

A. SELECT on the view always grants direct SELECT on all three tables.

B. Access depends on the applicable view security and underlying object privilege rules.

C. SELECT on the view automatically grants UPDATE on all three tables.

D. The view cannot reference multiple tables.

**Answer: B**

---

**Q47.** Consider:

```sql
GRANT UPDATE(salary)
ON Employee
TO user1;
```

Which statement is CORRECT?

A. user1 can update salary for all rows if the statement is otherwise permitted.

B. user1 can update salary only for the row whose emp_id is 1.

C. user1 can update salary only when a WHERE clause is present.

D. user1 automatically receives SELECT on Employee.

**Answer: A**

---

**Q48.** Which privilege is normally needed to insert a record into a table?

A. SELECT

B. INSERT

C. DELETE

D. EXECUTE

**Answer: B**

---

**Q49.** Consider:

```sql
GRANT SELECT ON Employee TO user1;

REVOKE ALL PRIVILEGES ON Employee FROM user1;
```

Which statement is CORRECT?

A. Only SELECT remains.

B. All applicable privileges granted to user1 on Employee are revoked, subject to applicable grantor and authorization rules.

C. The Employee table is dropped.

D. Only DELETE is revoked.

**Answer: B**

---

**Q50.** A role has SELECT permission on Employee. A user has been granted that role but has not activated it in a system where roles require explicit activation.

What happens?

A. The role's privilege is necessarily available in every session.

B. The role's privilege may be unavailable until the role is activated.

C. The user automatically gets ownership.

D. The role is automatically revoked.

**Answer: B**

---

**Q51.** Consider:

```sql
GRANT SELECT ON Employee TO user1;

GRANT DELETE ON Employee TO user1;

REVOKE ALL PRIVILEGES ON Employee FROM user1;
```

What remains from these direct grants?

A. SELECT only.

B. DELETE only.

C. Both SELECT and DELETE.

D. Neither SELECT nor DELETE.

**Answer: D**

---

**Q52.** Which statement about object privileges is CORRECT?

A. SELECT allows data retrieval, INSERT allows adding rows, UPDATE allows modifying permitted columns and DELETE allows deleting rows.

B. SELECT allows deleting rows and DELETE allows retrieving rows.

C. UPDATE automatically allows ALTER TABLE.

D. INSERT automatically allows CREATE INDEX.

**Answer: A**

---

**Q53.** Consider:

```sql
GRANT SELECT ON Employee TO user1;

GRANT UPDATE(salary) ON Employee TO user1;

REVOKE SELECT ON Employee FROM user1;
```

Can user1 still update salary?

A. Yes, because UPDATE(salary) remains independently granted.

B. No, because SELECT and UPDATE are always inseparable.

C. No, because revoking SELECT drops the table.

D. Yes, but only if user1 is the owner.

**Answer: A**

---

**Q54.** Which of the following is NOT an object privilege in the usual table-level SQL privilege model?

A. SELECT

B. INSERT

C. DELETE

D. CREATE USER

**Answer: D**

---

**Q55.** Consider:

```sql
GRANT SELECT ON Employee TO user1 WITH GRANT OPTION;

REVOKE SELECT ON Employee FROM user1 CASCADE;
```

What is the purpose of CASCADE?

A. It revokes dependent privileges granted onward through the revoked privilege, where applicable.

B. It deletes all database tables.

C. It transfers ownership to user1.

D. It grants SELECT to all users.

**Answer: A**

---

# Complete Answer Key

| Q | Ans | Q | Ans | Q | Ans |
| --- | --- | --- | --- | --- | --- |
| 1 | B | 20 | B | 39 | B |
| 2 | B | 21 | B | 40 | B |
| 3 | B | 22 | B | 41 | A |
| 4 | B | 23 | A | 42 | B |
| 5 | B | 24 | B | 43 | A |
| 6 | B | 25 | B | 44 | B |
| 7 | B | 26 | A | 45 | B |
| 8 | B | 27 | B | 46 | B |
| 9 | B | 28 | B | 47 | A |
| 10 | B | 29 | B | 48 | B |
| 11 | D | 30 | B | 49 | B |
| 12 | B | 31 | B | 50 | B |
| 13 | B | 32 | C | 51 | D |
| 14 | A | 33 | A | 52 | A |
| 15 | A | 34 | A | 53 | A |
| 16 | B | 35 | B | 54 | D |
| 17 | A | 36 | B | 55 | A |
| 18 | B | 37 | B |  |  |
| 19 | B | 38 | A |  |  |

**HSQLDB exam caution:** The conceptual questions above cover SQL-standard privilege semantics. For actual HSQLDB hands-on exams, verify the exact syntax supported by your installed version, especially column-level grants, routine privileges, sequence privileges, role activation, and `CASCADE`/`RESTRICT` behavior. Do not assume every feature of the SQL standard is implemented identically in HSQLDB.

### ChatGPT

# SQL Transactions, ACID, Concurrency Control & Transaction Processing - 60 Expert-Level MCQs

(2-Year SQL Developer Level) (HSQLDB Focus)

**Difficulty:** Advanced to Expert

The questions cover transaction theory, SQL transaction commands, autocommit, COMMIT, ROLLBACK, transaction states, ACID properties, batch/real-time/OLTP systems, concurrency problems, locking, lock compatibility matrix, two-phase locking, isolation levels, serializability, timestamp ordering and validation-based concurrency control.

**Important exam convention:** Unless a question specifies otherwise:

- Assume a single database connection.
- Assume successful SQL statements.
- Assume no triggers or cascading effects.
- Assume ordinary transactional tables.
- Treat COMMIT and ROLLBACK as transaction boundaries.
- HSQLDB's default transaction isolation is READ COMMITTED; autocommit is enabled by default in a standard JDBC connection, but client tools and session settings can affect the observed state.

---

# Section 1: Transaction Fundamentals and ACID Properties (Q1-Q10)

**Q1.** A banking application performs two operations:

```sql
UPDATE Account
SET balance = balance - 5000
WHERE account_id = 101;

UPDATE Account
SET balance = balance + 5000
WHERE account_id = 202;
```

The first operation succeeds, but the second fails because of a database error.

Which mechanism ensures that both operations succeed together or neither operation takes effect?

A. Indexing

B. Transaction management using COMMIT and ROLLBACK

C. Database normalization

D. Referential integrity alone

**Answer: B**

---

**Q2.** Which statement BEST describes a transaction?

A. A transaction is a collection of database tables.

B. A transaction is a logical unit of work containing one or more database operations that must be treated as a single unit.

C. A transaction is a query that can only retrieve data.

D. A transaction is a permanent database connection.

**Answer: B**

---

**Q3.** Consider the following transaction:

```sql
UPDATE Account
SET balance = balance - 1000
WHERE account_id = 1;

UPDATE Account
SET balance = balance + 1000
WHERE account_id = 2;

COMMIT;
```

Which ACID property ensures that both updates are treated as one indivisible unit?

A. Consistency

B. Isolation

C. Atomicity

D. Durability

**Answer: C**

---

**Q4.** A transaction transfers ₹5,000 between two accounts. Before the transaction, the total balance is ₹50,000. After the transaction, it must remain ₹50,000.

Which ACID property ensures that database constraints and consistency rules remain satisfied?

A. Atomicity

B. Consistency

C. Isolation

D. Durability

**Answer: B**

---

**Q5.** Transaction T1 updates an employee's salary. Before T1 commits, transaction T2 attempts to read that salary.

Which ACID property primarily concerns controlling interference between concurrent transactions?

A. Atomicity

B. Consistency

C. Isolation

D. Durability

**Answer: C**

---

**Q6.** A transaction executes:

```sql
UPDATE Employee
SET salary = 75000
WHERE emp_id = 101;

COMMIT;
```

Immediately after COMMIT, the database server crashes.

Which ACID property ensures that the committed change survives recovery?

A. Atomicity

B. Consistency

C. Isolation

D. Durability

**Answer: D**

---

**Q7.** Which of the following correctly matches ACID properties?

A. Atomicity - permanent storage; Consistency - concurrency; Isolation - rollback; Durability - constraints.

B. Atomicity - all or nothing; Consistency - valid database state; Isolation - concurrent transaction separation; Durability - committed changes persist.

C. Atomicity - data retrieval; Consistency - indexing; Isolation - normalization; Durability - locking.

D. Atomicity - query execution; Consistency - backup; Isolation - data integrity; Durability - SQL syntax.

**Answer: B**

---

**Q8.** Consider:

```sql
UPDATE Employee
SET salary = -1000
WHERE emp_id = 10;
```

Assume a CHECK constraint prohibits negative salaries.

Which statement is CORRECT?

A. The database must commit the transaction because the SQL syntax is valid.

B. The constraint violation can cause the statement to fail, preventing an invalid database state.

C. The database automatically disables the CHECK constraint.

D. Durability guarantees that the invalid salary is stored.

**Answer: B**

---

**Q9.** A transaction consists of five SQL statements. The first four execute successfully, but the fifth fails.

Which statement is CORRECT?

A. The first four statements are always permanently committed.

B. If the transaction is rolled back, its uncommitted changes are undone.

C. The database automatically deletes the affected table.

D. A failed statement automatically commits all previous statements.

**Answer: B**

---

**Q10.** Which of the following is NOT an objective of transaction management?

A. Maintaining database consistency.

B. Handling concurrent access.

C. Providing atomic execution of related operations.

D. Eliminating the need for database constraints.

**Answer: D**

---

# Section 2: Transaction Syntax, COMMIT, ROLLBACK and AUTOCOMMIT (Q11-Q25)

Assume the following initial table:

```sql
CREATE TABLE Employee (
    emp_id INT PRIMARY KEY,
    emp_name VARCHAR(30),
    salary INT
);

INSERT INTO Employee VALUES
(1, 'Arun', 30000),
(2, 'Bala', 40000),
(3, 'Charan', 50000);

COMMIT;
```

**Q11.** Consider:

```sql
SET AUTOCOMMIT FALSE;

INSERT INTO Employee
VALUES (4, 'David', 60000);

INSERT INTO Employee
VALUES (5, 'Ezhil', 70000);

COMMIT;
```

How many records are added permanently?

A. 0

B. 1

C. 2

D. 5

**Answer: C**

---

**Q12.** Consider:

```sql
SET AUTOCOMMIT FALSE;

INSERT INTO Employee
VALUES (4, 'David', 60000);

INSERT INTO Employee
VALUES (5, 'Ezhil', 70000);

ROLLBACK;
```

How many new records remain in the table?

A. 0

B. 1

C. 2

D. 3

**Answer: A**

---

**Q13.** Consider:

```sql
SET AUTOCOMMIT FALSE;

INSERT INTO Employee
VALUES (4, 'David', 60000);

COMMIT;

INSERT INTO Employee
VALUES (5, 'Ezhil', 70000);

ROLLBACK;
```

How many records are permanently added?

A. 0

B. 1

C. 2

D. 3

**Answer: B**

---

**Q14.** Consider:

```sql
SET AUTOCOMMIT TRUE;

INSERT INTO Employee
VALUES (4, 'David', 60000);

INSERT INTO Employee
VALUES (5, 'Ezhil', 70000);

ROLLBACK;
```

Assuming both INSERT statements succeed, what happens?

A. Both INSERT statements are undone.

B. Both INSERT statements are committed automatically; the subsequent ROLLBACK cannot undo them.

C. Only the first INSERT is committed.

D. Only the second INSERT is committed.

**Answer: B**

---

**Q15.** Consider:

```sql
SET AUTOCOMMIT FALSE;

INSERT INTO Employee
VALUES (4, 'David', 60000);

SET AUTOCOMMIT TRUE;
```

Which statement is MOST accurate?

A. The pending transaction is necessarily rolled back.

B. Changing autocommit from FALSE to TRUE generally commits the current transaction in JDBC/HSQLDB connection semantics.

C. The pending transaction remains indefinitely uncommitted.

D. The INSERT statement is automatically deleted.

**Answer: B**

---

**Q16.** Consider:

```sql
SET AUTOCOMMIT FALSE;

INSERT INTO Employee
VALUES (4, 'David', 60000);

INSERT INTO Employee
VALUES (5, 'Ezhil', 70000);

COMMIT;

INSERT INTO Employee
VALUES (6, 'Farhan', 80000);
```

How many new records are committed at this point?

A. 0

B. 1

C. 2

D. 3

**Answer: C**

---

**Q17.** In a standard JDBC connection, what is the default autocommit setting?

A. FALSE

B. TRUE

C. NULL

D. It is always determined by the number of tables.

**Answer: B**

---

**Q18.** Consider:

```sql
SET AUTOCOMMIT FALSE;

INSERT INTO Employee
VALUES (4, 'David', 60000);

UPDATE Employee
SET salary = 35000
WHERE emp_id = 1;

ROLLBACK;
```

What happens?

A. The inserted record remains, but the salary update is undone.

B. The inserted record is removed, and the salary is restored to 30000.

C. The inserted record remains, and the salary becomes 35000.

D. Only the INSERT is rolled back.

**Answer: B**

---

**Q19.** Consider:

```sql
SET AUTOCOMMIT FALSE;

INSERT INTO Employee
VALUES (4, 'David', 60000);

COMMIT;

UPDATE Employee
SET salary = 45000
WHERE emp_id = 2;

ROLLBACK;
```

What is the final salary of employee 2?

A. 30000

B. 40000

C. 45000

D. NULL

**Answer: B**

---

**Q20.** Which command explicitly makes the current transaction's successful changes permanent?

A. SAVEPOINT

B. ROLLBACK

C. COMMIT

D. GRANT

**Answer: C**

---

**Q21.** Which command cancels uncommitted changes in the current transaction?

A. COMMIT

B. ROLLBACK

C. CREATE

D. GRANT

**Answer: B**

---

**Q22.** Consider:

```sql
SET TRANSACTION READ ONLY;
```

What does this specify?

A. The transaction can execute only INSERT statements.

B. The transaction is restricted to read operations, subject to the database's transaction rules.

C. The transaction automatically commits after every SELECT.

D. The transaction cannot read any table.

**Answer: B**

---

**Q23.** Consider:

```sql
SET TRANSACTION READ WRITE;
```

Which statement is CORRECT?

A. The transaction can perform permitted data modifications.

B. The transaction cannot execute SELECT.

C. The transaction automatically disables constraints.

D. The transaction must be rolled back.

**Answer: A**

---

**Q24.** Consider:

```sql
SET TRANSACTION READ ONLY;

UPDATE Employee
SET salary = 70000
WHERE emp_id = 1;
```

What is the expected outcome?

A. The UPDATE succeeds because salary is numeric.

B. The UPDATE is rejected because the transaction is read-only.

C. The UPDATE executes but cannot be committed.

D. The transaction automatically changes to READ WRITE.

**Answer: B**

---

**Q25.** Which statement about transaction characteristics is CORRECT?

A. Transaction access mode can be specified using READ ONLY or READ WRITE, subject to supported syntax and when the characteristic is set.

B. READ ONLY means that the transaction cannot retrieve data.

C. READ WRITE means that COMMIT is prohibited.

D. Transaction access mode permanently changes the table structure.

**Answer: A**

---

# Section 3: Transaction States and Transaction Lifecycle (Q26-Q32)

**Q26.** A transaction has started and is currently executing its SQL statements. It has not yet reached COMMIT or ROLLBACK.

What is its current state?

A. Active

B. Partially committed

C. Committed

D. Aborted

**Answer: A**

---

**Q27.** A transaction has executed its final statement successfully and is preparing to make its changes permanent, but COMMIT has not yet completed.

Which state does it enter?

A. Active

B. Partially committed

C. Failed

D. Aborted

**Answer: B**

---

**Q28.** A transaction successfully executes COMMIT, and its changes are permanently recorded.

What is its state?

A. Active

B. Failed

C. Committed

D. Aborted

**Answer: C**

---

**Q29.** A transaction encounters a constraint violation or system error that prevents it from continuing.

Which state does it enter?

A. Active

B. Partially committed

C. Failed

D. Committed

**Answer: C**

---

**Q30.** Consider the transaction lifecycle:

Active → Failed → Aborted

What does Aborted indicate?

A. The transaction is still executing SQL statements.

B. Its unsuccessful execution has been terminated and its uncommitted changes have been undone.

C. Its changes have been permanently committed.

D. It is waiting for another transaction to release a lock.

**Answer: B**

---

**Q31.** Which sequence represents the normal successful transaction lifecycle?

A. Active → Failed → Aborted → Committed

B. Active → Partially Committed → Committed

C. Committed → Active → Failed

D. Active → Aborted → Partially Committed

**Answer: B**

---

**Q32.** A transaction enters the Aborted state. What can happen next?

A. It can never execute again under any circumstances.

B. It may be restarted as a new transaction, depending on the failure and recovery policy.

C. It automatically becomes committed.

D. It automatically enters the partially committed state.

**Answer: B**

---

# Section 4: Transaction Processing Systems (Q33-Q38)

**Q33.** A bank processes 10,000 salary payments every month. The payments are collected and processed automatically in a scheduled sequence without individual user interaction during execution.

Which processing system is MOST suitable?

A. Online Transaction Processing

B. Batch Processing

C. Manual Transaction Processing

D. Interactive Query Processing

**Answer: B**

---

**Q34.** A stock trading application receives continuous market inputs, evaluates conditions and must respond within strict time deadlines.

Which processing system is MOST appropriate?

A. Batch Processing

B. Real-Time Processing

C. Offline Processing

D. Sequential File Processing

**Answer: B**

---

**Q35.** A customer uses an online banking application to transfer money, enters account details and receives an immediate response after submitting the transaction.

Which processing system is this?

A. Batch Processing

B. Online Transaction Processing (OLTP)

C. Offline Processing

D. Sequential Processing

**Answer: B**

---

**Q36.** Which statement correctly differentiates batch processing and OLTP?

A. Batch processing requires continuous user interaction, whereas OLTP never requires users.

B. Batch processing handles accumulated jobs in groups, whereas OLTP handles individual interactive transactions.

C. Both systems must execute only at midnight.

D. OLTP does not require data integrity.

**Answer: B**

---

**Q37.** Which is the BEST example of batch processing?

A. A customer checking an ATM balance.

B. A user transferring money through internet banking.

C. Generating monthly electricity bills for millions of customers automatically.

D. A stock trading platform responding to an order.

**Answer: C**

---

**Q38.** Which of the following is NOT a typical OLTP system requirement?

A. High concurrency.

B. Low transaction response time.

C. Data integrity.

D. Processing only large, scheduled groups of records without interactive requests.

**Answer: D**

---

# Section 5: Concurrency Problems and Anomalies (Q39-Q45)

Assume two transactions T1 and T2 are accessing the same database concurrently.

**Q39. Lost Update**

Initially:

```text
Account balance = 10000
```

T1 and T2 both read the balance as 10000.

- T1 deducts 2000 and writes 8000.
- T2 deducts 3000 and writes 7000.

What is the final balance if T2 overwrites T1's result?

A. 5000

B. 7000

C. 8000

D. 10000

**Answer: B**

---

**Q40. Dirty Read**

Consider the following sequence:

1. T1 updates salary from 30000 to 50000.
2. T1 has not committed.
3. T2 reads salary as 50000.
4. T1 executes ROLLBACK.

Which concurrency problem occurred?

A. Lost Update

B. Dirty Read

C. Phantom Read

D. Incorrect Summary

**Answer: B**

---

**Q41. Phantom Read**

T1 executes:

```sql
SELECT *
FROM Employee
WHERE salary > 50000;
```

It retrieves 5 rows.

While T1 is still running, T2 inserts another employee with salary 60000 and commits.

T1 executes the same query again and retrieves 6 rows.

Which anomaly is illustrated?

A. Dirty Read

B. Lost Update

C. Phantom Read

D. Incorrect Summary

**Answer: C**

---

**Q42. Incorrect Summary**

Consider a bank with two accounts:

```text
Account A = 10000
Account B = 20000
```

T1 calculates the total balance:

```sql
SELECT SUM(balance)
FROM Account;
```

During the calculation, T2 transfers 5000 from A to B. T1 reads A before the transfer and B after the transfer.

Which problem may occur?

A. Lost Update

B. Incorrect Summary

C. Dirty Read only

D. Phantom Read only

**Answer: B**

---

**Q43.** Which concurrency problem involves one transaction reading data written by another transaction that has not yet committed?

A. Lost Update

B. Dirty Read

C. Phantom Read

D. Incorrect Summary

**Answer: B**

---

**Q44.** Which concurrency anomaly involves a transaction executing the same condition-based query twice and receiving a different set of rows because another transaction inserted or deleted qualifying rows?

A. Dirty Read

B. Lost Update

C. Phantom Read

D. Write Skew

**Answer: C**

---

**Q45.** Which mapping is CORRECT?

| Problem | Description |
| --- | --- |
| A | One transaction overwrites another transaction's update |
| B | Reading uncommitted data |
| C | New qualifying rows appear in repeated query execution |
| D | Aggregate calculation observes inconsistent values |

A. A-Dirty Read, B-Phantom Read, C-Lost Update, D-Incorrect Summary

B. A-Lost Update, B-Dirty Read, C-Phantom Read, D-Incorrect Summary

C. A-Phantom Read, B-Lost Update, C-Dirty Read, D-Incorrect Summary

D. A-Incorrect Summary, B-Dirty Read, C-Lost Update, D-Phantom Read

**Answer: B**

---

# Section 6: Lock-Based Concurrency Control (Q46-Q52)

**Q46.** Transaction T1 acquires a Shared (S) lock on Account A to read its balance.

Which operation can transaction T2 perform on the same resource while T1 holds the Shared lock?

A. Acquire another Shared lock.

B. Acquire an Exclusive lock.

C. Both Shared and Exclusive locks.

D. Neither Shared nor Exclusive locks.

**Answer: A**

---

**Q47.** Transaction T1 acquires an Exclusive (X) lock on Employee record 101.

What happens when T2 requests a Shared lock on the same resource?

A. T2 immediately receives the Shared lock.

B. T2 must wait until T1 releases the Exclusive lock.

C. Both transactions can modify the record simultaneously.

D. T2 automatically receives an Exclusive lock.

**Answer: B**

---

**Q48.** Which lock compatibility matrix is CORRECT?

| Existing lock / Requested lock | Shared (S) | Exclusive (X) |
| --- | --- | --- |
| Shared (S) | ? | ? |
| Exclusive (X) | ? | ? |

A.

|  | S | X |
| --- | --- | --- |
| S | Compatible | Compatible |
| X | Compatible | Compatible |

B.

|  | S | X |
| --- | --- | --- |
| S | Compatible | Not compatible |
| X | Not compatible | Not compatible |

C.

|  | S | X |
| --- | --- | --- |
| S | Not compatible | Compatible |
| X | Compatible | Not compatible |

D.

|  | S | X |
| --- | --- | --- |
| S | Not compatible | Not compatible |
| X | Not compatible | Compatible |

**Answer: B**

---

**Q49.** Which statement about Shared and Exclusive locks is CORRECT?

A. Shared locks permit multiple concurrent readers, while an Exclusive lock prevents other transactions from acquiring conflicting Shared or Exclusive locks on the same resource.

B. Shared locks permit multiple writers.

C. Exclusive locks permit unlimited concurrent readers.

D. Shared locks always provide lower concurrency than Exclusive locks.

**Answer: A**

---

**Q50.** Consider two transactions:

```text
T1: Acquires S lock on Employee 101.
T2: Requests X lock on Employee 101.
```

What happens?

A. Both locks are granted immediately.

B. T2 waits until T1 releases its Shared lock.

C. T1 loses its Shared lock automatically.

D. T2 can update the record without a lock.

**Answer: B**

---

**Q51.** Which statement BEST describes Two-Phase Locking (2PL)?

A. A transaction must execute exactly two SQL statements.

B. A transaction has a growing phase, during which it acquires locks, and a shrinking phase, during which it releases locks and cannot acquire new ones.

C. A transaction must acquire only Shared locks.

D. A transaction must commit after every SELECT statement.

**Answer: B**

---

**Q52.** Consider the following locking sequence:

```text
T1: Acquire S lock on A
T1: Acquire X lock on B
T1: Release S lock on A
T1: Acquire S lock on C
```

Does this satisfy basic Two-Phase Locking?

A. Yes, because all locks are released before COMMIT.

B. Yes, because T1 acquires only one Exclusive lock.

C. No, because T1 acquires a new lock after releasing an existing lock.

D. No, because Shared and Exclusive locks cannot be used together.

**Answer: C**

---

# Section 7: Isolation, Serializability, Timestamp and Validation (Q53-Q60)

**Q53.** Which isolation level prevents Dirty Reads but may still permit Non-Repeatable Reads and Phantom Reads?

A. READ UNCOMMITTED

B. READ COMMITTED

C. REPEATABLE READ

D. SERIALIZABLE

**Answer: B**

---

**Q54.** HSQLDB uses READ COMMITTED as its default transaction isolation level in its standard configuration.

Which statement describes READ COMMITTED?

A. A transaction can read changes made by uncommitted transactions.

B. A transaction can read only data committed before the individual read operation.

C. A transaction can never observe any concurrent changes during its entire lifetime.

D. Every transaction executes without concurrency.

**Answer: B**

---

**Q55.** Consider two transactions:

```text
T1:
SELECT salary FROM Employee WHERE emp_id = 10;
-- returns 30000

T2:
UPDATE Employee SET salary = 50000 WHERE emp_id = 10;
COMMIT;

T1:
SELECT salary FROM Employee WHERE emp_id = 10;
-- returns 50000
```

Assume READ COMMITTED isolation.

Which statement is CORRECT?

A. This is impossible under READ COMMITTED.

B. T1 may observe different committed values in its two reads.

C. T1 must always read 30000 until it commits.

D. T2 cannot commit while T1 is active.

**Answer: B**

---

**Q56.** Which isolation level provides the strongest standard SQL isolation guarantee?

A. READ UNCOMMITTED

B. READ COMMITTED

C. REPEATABLE READ

D. SERIALIZABLE

**Answer: D**

---

**Q57.** Two transactions execute concurrently. Their combined result is equivalent to executing T1 completely followed by T2, or T2 completely followed by T1.

Which property is satisfied?

A. Durability

B. Serializability

C. Atomicity

D. Index consistency

**Answer: B**

---

**Q58.** In timestamp-ordering concurrency control, each transaction is assigned a timestamp.

What is the primary purpose of this timestamp?

A. To identify the database table.

B. To determine the permitted ordering of conflicting read and write operations.

C. To calculate the transaction's execution cost.

D. To automatically commit transactions.

**Answer: B**

---

**Q59.** Consider validation-based concurrency control.

Which sequence correctly represents its general phases?

A. Validation → Read → Write

B. Read → Validation → Write

C. Write → Read → Validation

D. Commit → Read → Validation

**Answer: B**

---

**Q60.** Which statement about concurrency-control techniques is CORRECT?

A. Locking controls access to shared resources; timestamp ordering uses transaction timestamps; validation-based control checks whether concurrent execution can safely commit.

B. Locking is used only for SELECT statements.

C. Timestamp ordering eliminates the need to consider transaction conflicts.

D. Validation-based control always acquires Exclusive locks before reading data.

**Answer: A**

---

---

# Final Answer Key - Q1 to Q60

| Questions | Answers |
| --- | --- |
| 1-10 | B, B, C, B, C, D, B, B, B, D |
| 11-20 | C, A, B, B, B, C, B, B, B, C |
| 21-30 | B, B, A, B, A, A, B, C, C, B |
| 31-40 | B, B, B, B, B, B, C, D, B, B |
| 41-50 | B, B, B, B, B, A, B, B, A, B |
| 51-60 | B, C, B, B, B, D, B, B, B, A |

## Important HSQLDB exam traps

| Topic | Remember |
| --- | --- |
| Autocommit | JDBC default is generally TRUE |
| Autocommit FALSE | Explicit COMMIT or ROLLBACK required |
| COMMIT | Makes current transaction changes permanent |
| ROLLBACK | Undoes uncommitted changes |
| READ ONLY | Prevents transaction data modifications |
| READ WRITE | Allows permitted modifications |
| READ COMMITTED | Default HSQLDB isolation level in standard configuration |
| Dirty Read | Reading uncommitted data |
| Lost Update | One transaction overwrites another's update |
| Phantom Read | Repeated condition-based query returns additional or missing rows |
| Incorrect Summary | Aggregate observes inconsistent concurrent changes |
| Shared Lock | Multiple readers can coexist |
| Exclusive Lock | Prevents conflicting locks |
| 2PL | Growing phase followed by shrinking phase |
| Timestamp Ordering | Uses timestamps to order conflicting operations |
| Validation | Read → Validation → Write |

**Important distinction:** Two-phase locking is a theoretical locking protocol, not something you should automatically assume is the implementation behind every HSQLDB transaction. HSQLDB supports different transaction-control and isolation configurations. Also, READ COMMITTED does not guarantee that a transaction sees an unchanged snapshot throughout its lifetime.

The last 15 questions (Q46-Q60) serve as the final mixed expert-level revision section, covering locking, isolation, serializability and concurrency-control algorithms.

### ChatGPT

# Big Data & NoSQL Databases - 40 Advanced Expert-Level MCQs

(2-Year SQL Developer Level) (Advanced / Expert)

**Question distribution:**

| Section | Questions | Focus |
| --- | --- | --- |
| Big Data characteristics | 1-5 | 5 Vs |
| NoSQL fundamentals | 6-10 | SQL vs NoSQL, scalability |
| Key-Value databases | 11-15 | Characteristics and applications |
| Column-Family databases | 16-20 | Wide-column storage |
| Document-oriented databases | 21-27 | Schema, querying, applications |
| Graph databases | 28-32 | Relationships, graph theory, ACID |
| CAP theorem | 33-40 | Consistency, availability, partition tolerance |

---

# Section 1: Big Data Characteristics - 5 Vs (Q1-Q5)

**Q1.** An e-commerce platform generates 50 TB of customer transaction data every day. Which Big Data characteristic primarily describes the enormous quantity of generated data?

A. Velocity

B. Volume

C. Veracity

D. Value

**Answer: B - Volume**

---

**Q2.** A stock trading platform receives millions of transactions every second and must process them immediately.

Which Big Data characteristic is primarily involved?

A. Volume

B. Veracity

C. Velocity

D. Value

**Answer: C - Velocity**

---

**Q3.** A social media platform collects customer reviews, but many reviews contain fake information, incorrect details and misleading content.

Which Big Data characteristic addresses this problem?

A. Volume

B. Velocity

C. Veracity

D. Value

**Answer: C - Veracity**

---

**Q4.** A company collects massive amounts of customer data but extracts useful insights to improve product recommendations and increase revenue.

Which Big Data characteristic is demonstrated?

A. Value

B. Volume

C. Velocity

D. Veracity

**Answer: A - Value**

---

**Q5.** An organization collects structured customer records, JSON documents, videos, images and sensor data.

Which Big Data characteristic primarily describes the diversity of these data formats?

A. Volume

B. Velocity

C. Variety

D. Veracity

**Answer: C - Variety**

---

# Section 2: NoSQL Fundamentals and SQL vs NoSQL (Q6-Q10)

**Q6.** Which statement BEST describes NoSQL databases?

A. NoSQL databases cannot store structured data.

B. NoSQL databases provide alternative data models such as key-value, document, wide-column and graph storage.

C. NoSQL databases always use SQL syntax.

D. NoSQL databases cannot support transactions.

**Answer: B**

---

**Q7.** Which combination correctly differentiates traditional relational databases and NoSQL databases?

A. SQL - flexible schema; NoSQL - always rigid schema.

B. SQL - generally relational and structured; NoSQL - supports multiple data models and often flexible schemas.

C. SQL - only distributed storage; NoSQL - only centralized storage.

D. SQL - horizontal scaling only; NoSQL - vertical scaling only.

**Answer: B**

---

**Q8.** A company initially stores its application on one powerful database server. As traffic increases, it upgrades the CPU, RAM and storage of that server.

Which scaling approach is being used?

A. Horizontal scaling

B. Vertical scaling

C. Sharding

D. Replication

**Answer: B - Vertical scaling**

---

**Q9.** A database application distributes its data and workload across multiple database servers to handle increasing traffic.

Which scaling approach is being used?

A. Vertical scaling

B. Horizontal scaling

C. Normalization

D. Index partitioning only

**Answer: B - Horizontal scaling**

---

**Q10.** An e-commerce application uses:

- Relational database for financial transactions.
- Document database for product catalogues.
- Key-value database for shopping sessions.
- Graph database for product recommendations.

Which database design approach is demonstrated?

A. Database normalization

B. Polyglot persistence

C. Vertical partitioning

D. Data denormalization only

**Answer: B - Polyglot persistence**

---

# Section 3: Key-Value Store Databases (Q11-Q15)

**Q11.** An application stores user sessions in the following format:

```text
session_101 → {user_id: 101, login_time: "10:30"}
session_102 → {user_id: 102, login_time: "11:00"}
session_103 → {user_id: 103, login_time: "11:15"}
```

Which NoSQL database model is MOST suitable?

A. Graph database

B. Key-Value database

C. Relational database

D. Column-Family database

**Answer: B**

---

**Q12.** Which is the primary characteristic of a Key-Value database?

A. Data is stored as interconnected vertices and edges.

B. Data is stored as key-value pairs, where a key identifies its associated value.

C. Data is stored exclusively in rows and columns with fixed schemas.

D. Data is stored only as JSON documents with nested objects.

**Answer: B**

---

**Q13.** A company needs an extremely fast database for:

- Shopping cart sessions.
- User authentication sessions.
- Temporary application caching.
- Frequently accessed lookup values.

Which database is the BEST fit?

A. Neo4j

B. Redis

C. Cassandra

D. MongoDB

**Answer: B - Redis**

---

**Q14.** Which of the following is a Key-Value database?

A. MongoDB

B. Cassandra

C. Redis

D. Neo4j

**Answer: C**

---

**Q15.** An application stores customer preferences using unique identifiers. It primarily performs GET and PUT operations and rarely needs complex queries across the stored values.

Which database model is most appropriate?

A. Graph database

B. Key-Value database

C. Relational database

D. Document database

**Answer: B**

---

# Section 4: Column-Family / Wide-Column Databases (Q16-Q20)

**Q16.** A social media company generates billions of activity records every day. It needs distributed storage, high write throughput and horizontal scalability.

Which database is the BEST fit?

A. Redis

B. Cassandra

C. Neo4j

D. MongoDB

**Answer: B - Cassandra**

---

**Q17.** Which is the primary characteristic of a Column-Family database?

A. Data is stored exclusively as individual key-value pairs without additional structure.

B. Data is organized into rows with flexible columns grouped into column families or related wide-column structures.

C. Data is stored only as vertices and edges.

D. Data must follow a rigid relational schema with mandatory joins.

**Answer: B**

---

**Q18.** Which of the following is an example of a wide-column database?

A. Redis

B. MongoDB

C. Apache Cassandra

D. Neo4j

**Answer: C**

---

**Q19.** A telecommunications company stores:

- Customer ID.
- Call records.
- Network activity.
- Billions of time-series events.

It needs distributed storage and high write availability across multiple nodes.

Which database is the MOST suitable?

A. Cassandra

B. Neo4j

C. Redis

D. Traditional relational database only

**Answer: A**

---

**Q20.** Which statement about Cassandra is CORRECT?

A. Cassandra is primarily a graph database.

B. Cassandra is a distributed wide-column database designed for scalability and high availability.

C. Cassandra is a document-oriented database with MongoDB-compatible storage.

D. Cassandra requires every query to perform relational joins.

**Answer: B**

---

# Section 5: Document-Oriented Databases (Q21-Q27)

**Q21.** Consider the following MongoDB document:

```json
{
  "customer_id": 101,
  "name": "Arun",
  "address": {
    "city": "Chennai",
    "pincode": 600001
  },
  "orders": [
    {
      "order_id": 501,
      "amount": 5000
    },
    {
      "order_id": 502,
      "amount": 7000
    }
  ]
}
```

Which database model is being used?

A. Key-Value

B. Column-Family

C. Document-oriented

D. Graph

**Answer: C**

---

**Q22.** Which is a major advantage of document-oriented databases?

A. Every document must have exactly the same attributes.

B. Flexible schema allows documents in the same collection to have different structures.

C. Relationships can only be represented using foreign keys.

D. Documents cannot contain nested objects.

**Answer: B**

---

**Q23.** A company is rapidly developing an application where customer records frequently acquire new attributes such as:

```text
customer_id
name
email
loyalty_points
preferences
delivery_instructions
```

Different customers may have different optional fields.

Which database is MOST appropriate?

A. MongoDB

B. Redis

C. Neo4j

D. Cassandra

**Answer: A - MongoDB**

---

**Q24.** Which statement BEST describes rich querying capabilities in document-oriented databases?

A. They support only retrieval using primary keys.

B. They can support queries on document fields, nested attributes, arrays, filtering and aggregation.

C. They cannot search using multiple fields.

D. They support only simple key-value lookups.

**Answer: B**

---

**Q25.** A news application stores articles containing:

- Title
- Author
- Content
- Tags
- Comments
- Publication details

Most operations retrieve complete articles, and updates are relatively infrequent.

Which database model is MOST appropriate?

A. Graph database

B. Document-oriented database

C. Key-Value database

D. Column-Family database

**Answer: B**

---

**Q26.** Which of the following is NOT a characteristic of a document-oriented database?

A. Flexible document structure.

B. Support for nested objects and arrays.

C. Rich field-based querying.

D. Mandatory normalization into multiple relational tables for every entity.

**Answer: D**

---

**Q27.** Consider the following two MongoDB documents in the same collection:

```json
{
  "emp_id": 1,
  "name": "Arun",
  "salary": 50000
}
```

```json
{
  "emp_id": 2,
  "name": "Bala",
  "department": "IT",
  "skills": ["Java", "SQL"]
}
```

Which statement is CORRECT?

A. MongoDB rejects the second document because it has different attributes.

B. Both documents can exist in the same collection because MongoDB supports flexible document structures.

C. MongoDB automatically converts the second document into a relational table.

D. MongoDB requires every document to have an identical number of fields.

**Answer: B**

---

# Section 6: Graph Databases (Q28-Q32)

**Q28.** A social networking application stores millions of users and their relationships:

- User A follows User B.
- User B follows User C.
- User C is friends with User D.

The application frequently searches for mutual friends and relationship paths.

Which database is MOST appropriate?

A. Redis

B. Cassandra

C. Neo4j

D. MongoDB

**Answer: C - Neo4j**

---

**Q29.** Which components form the basic structure of a graph database?

A. Rows and columns only.

B. Keys and values only.

C. Nodes (vertices), relationships (edges) and properties.

D. Documents and collections only.

**Answer: C**

---

**Q30.** An organization maintains a fraud detection system. It needs to discover relationships between:

- Bank accounts.
- Customers.
- Phone numbers.
- IP addresses.
- Transactions.

Which graph database advantage is MOST relevant?

A. Avoiding all data relationships.

B. Efficient traversal of highly interconnected relationships without repeatedly performing traditional relational joins.

C. Storing every value as an independent key-value pair.

D. Enforcing a fixed document schema.

**Answer: B**

---

**Q31.** Which statement about graph databases is CORRECT?

A. Graph databases cannot represent properties on relationships.

B. Graph databases model relationships explicitly, making relationship traversal a central operation.

C. Graph databases cannot represent multiple relationships between two nodes.

D. Graph databases are designed exclusively for financial calculations.

**Answer: B**

---

**Q32.** Which statement about Neo4j and ACID is CORRECT?

A. Neo4j cannot support ACID transactions because it is a NoSQL database.

B. Neo4j supports ACID transactions, demonstrating that NoSQL does not inherently mean absence of ACID properties.

C. Neo4j supports only eventual consistency.

D. Graph databases cannot guarantee atomicity.

**Answer: B**

---

# Section 7: CAP Theorem - Expert-Level Questions (Q33-Q40)

**Q33.** According to the CAP theorem, what do C, A and P represent?

A. Concurrency, Atomicity, Processing

B. Consistency, Availability, Partition Tolerance

C. Consistency, Atomicity, Persistence

D. Centralization, Availability, Performance

**Answer: B**

---

**Q34.** According to CAP theorem, when a network partition occurs, a distributed database must make a trade-off between which two guarantees?

A. Volume and Velocity

B. Consistency and Availability

C. Atomicity and Durability

D. Variety and Veracity

**Answer: B**

---

**Q35.** A distributed database experiences a network partition. It refuses to process some requests until communication between nodes is restored to ensure that clients do not receive conflicting data.

Which CAP category does this behavior represent?

A. AP

B. CP

C. CA

D. NoSQL

**Answer: B - CP**

---

**Q36.** A distributed database experiences a network partition. It continues accepting requests from reachable nodes, but different clients may temporarily receive different values.

Which CAP category does this behavior represent?

A. CP

B. CA

C. AP

D. ACID

**Answer: C - AP**

---

**Q37.** Which statement about Cassandra is MOST accurate?

A. Cassandra is a traditional CA database.

B. Cassandra is commonly classified as AP-oriented, although its configurable consistency levels allow different consistency/availability trade-offs.

C. Cassandra is exclusively a CP database and cannot provide eventual consistency.

D. Cassandra is a relational database.

**Answer: B**

---

**Q38.** Which of the following is the conventional CAP classification used in introductory database examinations?

A. MongoDB - AP; Cassandra - CP; Neo4j - CA.

B. MongoDB - CP; Cassandra - AP; Neo4j - typically treated as CA in simplified classifications.

C. MongoDB - CA; Cassandra - CA; Neo4j - AP.

D. MongoDB - AP; Cassandra - CA; Neo4j - CP.

**Answer: B**

---

**Q39.** Which statement BEST describes eventual consistency?

A. All replicas must contain identical data at every instant.

B. Replicas may temporarily contain different values but are expected to converge if updates stop and synchronization succeeds.

C. Transactions cannot be committed.

D. Data is permanently inconsistent.

**Answer: B**

---

**Q40.** A distributed e-commerce system has the following requirements:

- Customers must be able to browse products even during network partitions.
- Temporary differences in inventory information are acceptable.
- Inventory replicas should eventually synchronize.

Which architecture is MOST appropriate?

A. CP-oriented system that rejects every request during a partition.

B. AP-oriented system with eventual consistency.

C. Traditional centralized database without replication.

D. A system that completely disables data synchronization.

**Answer: B**

---

# Complete Answer Key

| Q | Answer | Q | Answer |
| --- | --- | --- | --- |
| 1 | B | 21 | C |
| 2 | C | 22 | B |
| 3 | C | 23 | A |
| 4 | A | 24 | B |
| 5 | C | 25 | B |
| 6 | B | 26 | D |
| 7 | B | 27 | B |
| 8 | B | 28 | C |
| 9 | B | 29 | C |
| 10 | B | 30 | B |
| 11 | B | 31 | B |
| 12 | B | 32 | B |
| 13 | B | 33 | B |
| 14 | C | 34 | B |
| 15 | B | 35 | B |
| 16 | B | 36 | C |
| 17 | B | 37 | B |
| 18 | C | 38 | B |
| 19 | A | 39 | B |
| 20 | B | 40 | B |

---

## Final revision: Database selection scenarios

These are particularly important for scenario-based SQL/DBMS examinations.

| Requirement / Application | Best database choice | Example |
| --- | --- | --- |
| Shopping cart and user sessions | Key-Value | Redis |
| Distributed activity logs | Column-Family | Apache Cassandra |
| IoT sensor data at massive scale | Column-Family | Apache Cassandra |
| Product catalogue | Document | MongoDB |
| Customer profiles with flexible attributes | Document | MongoDB |
| News articles and nested content | Document | MongoDB |
| Social networking connections | Graph | Neo4j |
| Fraud detection and relationship discovery | Graph | Neo4j |
| Product recommendations based on relationships | Graph | Neo4j |
| Financial transactions with relational constraints | Relational | PostgreSQL |

## Five critical exam traps

1. **NoSQL does not mean no ACID.** Neo4j and MongoDB support ACID transactions.
2. **NoSQL does not mean no schema.** Document databases can enforce validation rules.
3. **CAP:** Partition tolerance matters in distributed systems; during a partition, consistency and availability cannot both be fully guaranteed.
4. **Cassandra:** Its classification is commonly AP-oriented, but consistency levels are configurable.
5. **MongoDB:** Commonly classified as CP-oriented in introductory CAP questions, but actual behavior depends on replication, read/write concerns and failure scenarios.

**Important CAP correction:** The simplified classification of MongoDB as CP, Cassandra as AP and Neo4j as CA is an exam convention, not an absolute classification of every configuration. In particular, a distributed Neo4j deployment can also experience network partitions and must make availability/consistency trade-offs.

### ChatGPT

# MongoDB - Sequential Update() and Remove() Practice (20 Questions)

(2-Year SQL Developer Level) (Easy-Moderate)

**Instructions:**

- Each question starts with 7 existing documents.
- Execute operations in the exact order given.
- Find the final resultant collection after all operations.
- For deletion questions, identify the number of remaining documents.
- For update questions, identify the final document values.
- Assume all `_id` values are unique.
- `update()` without `multi: true` updates only one matching document.
- `remove(criteria)` deletes all matching documents by default.
- `$set` adds a field if it does not exist.
- Replacement updates replace document contents, preserving `_id`.

---

## Q1. Basic $set Update

**Initial Collection: Employee**

```javascript
[
  { _id: 1, name: "Arun", age: 25, dept: "IT" },
  { _id: 2, name: "Bala", age: 30, dept: "HR" },
  { _id: 3, name: "Charan", age: 28, dept: "IT" },
  { _id: 4, name: "Divya", age: 26, dept: "Sales" },
  { _id: 5, name: "Ezhil", age: 32, dept: "HR" },
  { _id: 6, name: "Farhan", age: 29, dept: "IT" },
  { _id: 7, name: "Gokul", age: 24, dept: "Sales" }
]
```

Execute:

```javascript
db.Employee.update(
  { dept: "IT" },
  { $set: { salary: 50000 } },
  { multi: true }
)
```

**Question:** What is the final resultant collection?

A. Only Arun receives salary 50000.

B. Arun, Charan and Farhan receive salary 50000.

C. All seven employees receive salary 50000.

D. No document is updated.

**Answer: B**

Final changes:

```javascript
{ _id: 1, name: "Arun", age: 25, dept: "IT", salary: 50000 }
{ _id: 3, name: "Charan", age: 28, dept: "IT", salary: 50000 }
{ _id: 6, name: "Farhan", age: 29, dept: "IT", salary: 50000 }
```

---

## Q2. Remove All Matching Documents

**Initial Collection: Student**

```javascript
[
  { _id: 1, name: "Arun", marks: 80, city: "Chennai" },
  { _id: 2, name: "Bala", marks: 45, city: "Madurai" },
  { _id: 3, name: "Charan", marks: 90, city: "Chennai" },
  { _id: 4, name: "Divya", marks: 35, city: "Salem" },
  { _id: 5, name: "Ezhil", marks: 60, city: "Chennai" },
  { _id: 6, name: "Farhan", marks: 40, city: "Madurai" },
  { _id: 7, name: "Gokul", marks: 75, city: "Salem" }
]
```

Execute:

```javascript
db.Student.remove({ city: "Chennai" })
```

**Question:** How many documents remain?

A. 3

B. 4

C. 5

D. 6

**Answer: B - 4 documents**

---

## Q3. Sequential Update and Delete

**Initial Collection: Employee**

```javascript
[
  { _id: 1, name: "Arun", age: 25, dept: "IT" },
  { _id: 2, name: "Bala", age: 30, dept: "HR" },
  { _id: 3, name: "Charan", age: 28, dept: "IT" },
  { _id: 4, name: "Divya", age: 26, dept: "Sales" },
  { _id: 5, name: "Ezhil", age: 32, dept: "HR" },
  { _id: 6, name: "Farhan", age: 29, dept: "IT" },
  { _id: 7, name: "Gokul", age: 24, dept: "Sales" }
]
```

Execute:

```javascript
db.Employee.update(
  { dept: "HR" },
  { $set: { dept: "Finance" } },
  { multi: true }
)

db.Employee.remove({ age: 30 })
```

**Question:** How many documents remain, and which department does Ezhil belong to?

A. 6 documents, HR

B. 6 documents, Finance

C. 5 documents, Finance

D. 7 documents, Finance

**Answer: B - 6 documents, Finance**

---

## Q4. Update Without multi: true

**Initial Collection: Product**

```javascript
[
  { _id: 1, name: "Laptop", price: 50000, category: "Electronics" },
  { _id: 2, name: "Mouse", price: 500, category: "Electronics" },
  { _id: 3, name: "Keyboard", price: 1000, category: "Electronics" },
  { _id: 4, name: "Chair", price: 3000, category: "Furniture" },
  { _id: 5, name: "Table", price: 7000, category: "Furniture" },
  { _id: 6, name: "Phone", price: 20000, category: "Electronics" },
  { _id: 7, name: "Bottle", price: 300, category: "Accessories" }
]
```

Execute:

```javascript
db.Product.update(
  { category: "Electronics" },
  { $set: { available: true } }
)
```

**Question:** What happens?

A. All four Electronics products are updated.

B. Only one matching Electronics product is updated.

C. No product is updated.

D. All seven products are updated.

**Answer: B**

---

## Q5. Delete Based on Numeric Condition

**Initial Collection: Employee**

```javascript
[
  { _id: 1, name: "Arun", salary: 20000 },
  { _id: 2, name: "Bala", salary: 30000 },
  { _id: 3, name: "Charan", salary: 40000 },
  { _id: 4, name: "Divya", salary: 25000 },
  { _id: 5, name: "Ezhil", salary: 50000 },
  { _id: 6, name: "Farhan", salary: 35000 },
  { _id: 7, name: "Gokul", salary: 15000 }
]
```

Execute:

```javascript
db.Employee.remove({ salary: { $gte: 30000 } })
```

**Question:** How many documents remain?

A. 2

B. 3

C. 4

D. 5

**Answer: B - 3 documents**

---

## Q6. Sequential Update With Different Conditions

**Initial Collection: Student**

```javascript
[
  { _id: 1, name: "Arun", marks: 80 },
  { _id: 2, name: "Bala", marks: 40 },
  { _id: 3, name: "Charan", marks: 90 },
  { _id: 4, name: "Divya", marks: 50 },
  { _id: 5, name: "Ezhil", marks: 60 },
  { _id: 6, name: "Farhan", marks: 30 },
  { _id: 7, name: "Gokul", marks: 70 }
]
```

Execute:

```javascript
db.Student.update(
  { marks: { $gte: 70 } },
  { $set: { result: "Pass" } },
  { multi: true }
)

db.Student.update(
  { marks: { $lt: 50 } },
  { $set: { result: "Fail" } },
  { multi: true }
)
```

**Question:** What is Bala's result, and how many students have the Pass result?

A. Pass, 4

B. Fail, 3

C. Fail, 4

D. No result, 3

**Answer: B - Fail, 3**

---

## Q7. Replacement Update

**Initial Collection: Employee**

```javascript
[
  { _id: 1, name: "Arun", age: 25, dept: "IT", salary: 30000 },
  { _id: 2, name: "Bala", age: 30, dept: "HR", salary: 40000 },
  { _id: 3, name: "Charan", age: 28, dept: "IT", salary: 35000 },
  { _id: 4, name: "Divya", age: 26, dept: "Sales", salary: 45000 },
  { _id: 5, name: "Ezhil", age: 32, dept: "HR", salary: 50000 },
  { _id: 6, name: "Farhan", age: 29, dept: "IT", salary: 55000 },
  { _id: 7, name: "Gokul", age: 24, dept: "Sales", salary: 25000 }
]
```

Execute:

```javascript
db.Employee.update(
  { _id: 2 },
  { name: "Bala Kumar", salary: 60000 }
)
```

**Question:** What is the resulting document with `_id: 2`?

A.

```javascript
{ _id: 2, name: "Bala Kumar", age: 30,
  dept: "HR", salary: 60000 }
```

B.

```javascript
{ _id: 2, name: "Bala Kumar", salary: 60000 }
```

C.

```javascript
{ name: "Bala Kumar", salary: 60000 }
```

D. The update fails because `$set` is missing.

**Answer: B**

---

## Q8. Delete Followed by Update

**Initial Collection: Product**

```javascript
[
  { _id: 1, name: "Pen", price: 10 },
  { _id: 2, name: "Pencil", price: 5 },
  { _id: 3, name: "Book", price: 50 },
  { _id: 4, name: "Bag", price: 500 },
  { _id: 5, name: "Eraser", price: 8 },
  { _id: 6, name: "Scale", price: 20 },
  { _id: 7, name: "Bottle", price: 100 }
]
```

Execute:

```javascript
db.Product.remove({ price: { $lt: 10 } })

db.Product.update(
  { price: { $gte: 100 } },
  { $set: { discount: 10 } },
  { multi: true }
)
```

**Question:** How many documents remain, and how many have a discount field?

A. 5 documents, 2 discounted

B. 6 documents, 2 discounted

C. 5 documents, 1 discounted

D. 7 documents, 3 discounted

**Answer: A - 5 documents, 2 discounted**

---

## Q9. Multiple Sequential Updates

**Initial Collection: Employee**

```javascript
[
  { _id: 1, name: "Arun", dept: "IT", salary: 30000 },
  { _id: 2, name: "Bala", dept: "HR", salary: 40000 },
  { _id: 3, name: "Charan", dept: "IT", salary: 35000 },
  { _id: 4, name: "Divya", dept: "HR", salary: 45000 },
  { _id: 5, name: "Ezhil", dept: "Sales", salary: 50000 },
  { _id: 6, name: "Farhan", dept: "IT", salary: 55000 },
  { _id: 7, name: "Gokul", dept: "Sales", salary: 25000 }
]
```

Execute:

```javascript
db.Employee.update(
  { dept: "IT" },
  { $set: { location: "Chennai" } },
  { multi: true }
)

db.Employee.update(
  { salary: { $gte: 40000 } },
  { $set: { grade: "A" } },
  { multi: true }
)
```

**Question:** Which employee receives both `location: "Chennai"` and `grade: "A"`?

A. Arun

B. Charan

C. Farhan

D. Bala

**Answer: C - Farhan**

---

## Q10. Remove One Matching Document

**Initial Collection: Student**

```javascript
[
  { _id: 1, name: "Arun", city: "Chennai" },
  { _id: 2, name: "Bala", city: "Chennai" },
  { _id: 3, name: "Charan", city: "Madurai" },
  { _id: 4, name: "Divya", city: "Chennai" },
  { _id: 5, name: "Ezhil", city: "Salem" },
  { _id: 6, name: "Farhan", city: "Madurai" },
  { _id: 7, name: "Gokul", city: "Chennai" }
]
```

Execute:

```javascript
db.Student.remove(
  { city: "Chennai" },
  true
)
```

**Question:** What is the expected number of remaining documents?

A. 3

B. 4

C. 6

D. 7

**Answer: C - 6 documents**

---

## Q11. Updating an Existing Field

**Initial Collection: Product**

```javascript
[
  { _id: 1, name: "Laptop", price: 50000, stock: 10 },
  { _id: 2, name: "Mouse", price: 500, stock: 20 },
  { _id: 3, name: "Keyboard", price: 1000, stock: 15 },
  { _id: 4, name: "Chair", price: 3000, stock: 5 },
  { _id: 5, name: "Table", price: 7000, stock: 8 },
  { _id: 6, name: "Phone", price: 20000, stock: 12 },
  { _id: 7, name: "Bottle", price: 300, stock: 30 }
]
```

Execute:

```javascript
db.Product.update(
  { stock: { $gte: 15 } },
  { $set: { stock: 0 } },
  { multi: true }
)
```

**Question:** How many products have stock equal to zero?

A. 2

B. 3

C. 4

D. 5

**Answer: B - 3 products**

---

## Q12. Delete Then Insert

**Initial Collection: Student**

```javascript
[
  { _id: 1, name: "Arun", marks: 80 },
  { _id: 2, name: "Bala", marks: 40 },
  { _id: 3, name: "Charan", marks: 90 },
  { _id: 4, name: "Divya", marks: 50 },
  { _id: 5, name: "Ezhil", marks: 60 },
  { _id: 6, name: "Farhan", marks: 30 },
  { _id: 7, name: "Gokul", marks: 70 }
]
```

Execute:

```javascript
db.Student.remove({ marks: { $lt: 50 } })

db.Student.insert({
  _id: 8,
  name: "Hari",
  marks: 85
})
```

**Question:** How many documents exist after both operations?

A. 5

B. 6

C. 7

D. 8

**Answer: B - 6 documents**

---

## Q13. Update Then Delete Using Updated Value

**Initial Collection: Employee**

```javascript
[
  { _id: 1, name: "Arun", salary: 20000 },
  { _id: 2, name: "Bala", salary: 30000 },
  { _id: 3, name: "Charan", salary: 40000 },
  { _id: 4, name: "Divya", salary: 25000 },
  { _id: 5, name: "Ezhil", salary: 50000 },
  { _id: 6, name: "Farhan", salary: 35000 },
  { _id: 7, name: "Gokul", salary: 15000 }
]
```

Execute:

```javascript
db.Employee.update(
  { salary: { $lt: 30000 } },
  { $set: { salary: 30000 } },
  { multi: true }
)

db.Employee.remove({ salary: 30000 })
```

**Question:** How many documents remain?

A. 2

B. 3

C. 4

D. 5

**Answer: A - 2 documents**

---

## Q14. Replacement Update on One Document

**Initial Collection: Student**

```javascript
[
  { _id: 1, name: "Arun", age: 20, city: "Chennai" },
  { _id: 2, name: "Bala", age: 21, city: "Madurai" },
  { _id: 3, name: "Charan", age: 22, city: "Salem" },
  { _id: 4, name: "Divya", age: 23, city: "Chennai" },
  { _id: 5, name: "Ezhil", age: 24, city: "Madurai" },
  { _id: 6, name: "Farhan", age: 25, city: "Salem" },
  { _id: 7, name: "Gokul", age: 26, city: "Chennai" }
]
```

Execute:

```javascript
db.Student.update(
  { city: "Chennai" },
  { name: "New Student", marks: 90 }
)
```

**Question:** Which statement is CORRECT?

A. All three Chennai students are replaced.

B. Only one Chennai student is replaced, and the other matching documents remain unchanged.

C. All seven students are replaced.

D. The update fails because city is missing from the replacement.

**Answer: B**

---

## Q15. Two Updates and One Delete

**Initial Collection: Employee**

```javascript
[
  { _id: 1, name: "Arun", dept: "IT", salary: 30000 },
  { _id: 2, name: "Bala", dept: "HR", salary: 40000 },
  { _id: 3, name: "Charan", dept: "IT", salary: 35000 },
  { _id: 4, name: "Divya", dept: "HR", salary: 45000 },
  { _id: 5, name: "Ezhil", dept: "Sales", salary: 50000 },
  { _id: 6, name: "Farhan", dept: "IT", salary: 55000 },
  { _id: 7, name: "Gokul", dept: "Sales", salary: 25000 }
]
```

Execute:

```javascript
db.Employee.update(
  { dept: "HR" },
  { $set: { dept: "Finance" } },
  { multi: true }
)

db.Employee.update(
  { salary: { $gte: 50000 } },
  { $set: { bonus: 5000 } },
  { multi: true }
)

db.Employee.remove({ dept: "Sales" })
```

**Question:** How many documents remain, and how many have a bonus field?

A. 5 documents, 2 with bonus

B. 5 documents, 1 with bonus

C. 4 documents, 2 with bonus

D. 6 documents, 2 with bonus

**Answer: A - 5 documents, 2 with bonus**

---

## Q16. Sequential Remove Operations

**Initial Collection: Product**

```javascript
[
  { _id: 1, name: "Pen", price: 10, category: "Stationery" },
  { _id: 2, name: "Pencil", price: 5, category: "Stationery" },
  { _id: 3, name: "Book", price: 50, category: "Stationery" },
  { _id: 4, name: "Bag", price: 500, category: "Accessories" },
  { _id: 5, name: "Eraser", price: 8, category: "Stationery" },
  { _id: 6, name: "Scale", price: 20, category: "Stationery" },
  { _id: 7, name: "Bottle", price: 100, category: "Accessories" }
]
```

Execute:

```javascript
db.Product.remove({ price: { $lt: 10 } })

db.Product.remove({ category: "Accessories" })
```

**Question:** How many documents remain?

A. 2

B. 3

C. 4

D. 5

**Answer: A - 2 documents**

---

## Q17. Update Adds a New Field

**Initial Collection: Student**

```javascript
[
  { _id: 1, name: "Arun", marks: 80 },
  { _id: 2, name: "Bala", marks: 40 },
  { _id: 3, name: "Charan", marks: 90 },
  { _id: 4, name: "Divya", marks: 50 },
  { _id: 5, name: "Ezhil", marks: 60 },
  { _id: 6, name: "Farhan", marks: 30 },
  { _id: 7, name: "Gokul", marks: 70 }
]
```

Execute:

```javascript
db.Student.update(
  { marks: { $gte: 80 } },
  { $set: { grade: "A" } },
  { multi: true }
)

db.Student.remove({ marks: { $lt: 50 } })
```

**Question:** What is the final number of documents, and how many have grade A?

A. 5 documents, 2 with grade A

B. 4 documents, 2 with grade A

C. 5 documents, 3 with grade A

D. 6 documents, 2 with grade A

**Answer: A - 5 documents, 2 with grade A**

---

## Q18. Update Without multi Followed by Delete

**Initial Collection: Employee**

```javascript
[
  { _id: 1, name: "Arun", dept: "IT" },
  { _id: 2, name: "Bala", dept: "HR" },
  { _id: 3, name: "Charan", dept: "IT" },
  { _id: 4, name: "Divya", dept: "IT" },
  { _id: 5, name: "Ezhil", dept: "HR" },
  { _id: 6, name: "Farhan", dept: "IT" },
  { _id: 7, name: "Gokul", dept: "Sales" }
]
```

Execute:

```javascript
db.Employee.update(
  { dept: "IT" },
  { $set: { dept: "Development" } }
)

db.Employee.remove({ dept: "IT" })
```

**Question:** How many documents remain?

A. 3

B. 4

C. 5

D. 6

**Answer: B - 4 documents**

---

## Q19. Multiple Updates Affecting Same Documents

**Initial Collection: Product**

```javascript
[
  { _id: 1, name: "Laptop", price: 50000 },
  { _id: 2, name: "Mouse", price: 500 },
  { _id: 3, name: "Keyboard", price: 1000 },
  { _id: 4, name: "Chair", price: 3000 },
  { _id: 5, name: "Table", price: 7000 },
  { _id: 6, name: "Phone", price: 20000 },
  { _id: 7, name: "Bottle", price: 300 }
]
```

Execute:

```javascript
db.Product.update(
  { price: { $gte: 1000 } },
  { $set: { status: "Available" } },
  { multi: true }
)

db.Product.update(
  { price: { $gte: 5000 } },
  { $set: { status: "Premium" } },
  { multi: true }
)
```

**Question:** What is the final status of the Laptop and Mouse?

A. Laptop - Available, Mouse - Available

B. Laptop - Premium, Mouse - No status

C. Laptop - Available, Mouse - No status

D. Laptop - Premium, Mouse - Premium

**Answer: B**

---

## Q20. Final Combined Operation

**Initial Collection: Employee**

```javascript
[
  { _id: 1, name: "Arun", dept: "IT", salary: 30000 },
  { _id: 2, name: "Bala", dept: "HR", salary: 40000 },
  { _id: 3, name: "Charan", dept: "IT", salary: 35000 },
  { _id: 4, name: "Divya", dept: "Sales", salary: 45000 },
  { _id: 5, name: "Ezhil", dept: "HR", salary: 50000 },
  { _id: 6, name: "Farhan", dept: "IT", salary: 55000 },
  { _id: 7, name: "Gokul", dept: "Sales", salary: 25000 }
]
```

Execute:

```javascript
db.Employee.update(
  { dept: "IT" },
  { $set: { location: "Chennai" } },
  { multi: true }
)

db.Employee.remove({ salary: { $lt: 30000 } })

db.Employee.update(
  { dept: "HR" },
  { $set: { bonus: 5000 } },
  { multi: true }
)

db.Employee.remove({ salary: { $gte: 50000 } })
```

**Question:** How many documents remain, and how many remaining employees have a bonus field?

A. 3 documents, 2 with bonus

B. 4 documents, 2 with bonus

C. 4 documents, 1 with bonus

D. 5 documents, 2 with bonus

**Answer: B - 4 documents, 2 with bonus**

---

## Quick Answer Key

| Question | Answer |
| --- | --- |
| 1 | B |
| 2 | B |
| 3 | B |
| 4 | B |
| 5 | B |
| 6 | B |
| 7 | B |
| 8 | A |
| 9 | C |
| 10 | C |
| 11 | B |
| 12 | B |
| 13 | A |
| 14 | B |
| 15 | A |
| 16 | A |
| 17 | A |
| 18 | B |
| 19 | B |
| 20 | B |

**Exam tip:** For every question, maintain a small document count after each operation. The most common mistakes are forgetting that `remove()` deletes all matching documents by default, assuming `update()` modifies every matching document without `multi: true`, and forgetting that replacement updates remove unspecified fields.
