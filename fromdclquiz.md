
# Indexing MCQ Quiz

### User

indexing intro to indexing example why indexing working of index index tree search algo index for enforcing data integrity,index automatically created for constraint enforcement when u create primary and unique key,index types characterstics clustered index non clustered index clustered auto generated non clustered created manually max 249 per table max 1 clustered index per table clustererd sort table data non clustered do not sort table data, index of primarky key automatically created, consumes additional space, maintained automatically by databe once created we dont have to maintain,size oof index propertional to size of data, can be created on multiple attributes as well composite index , degratation of insert performance with addition of index numer of rows per unit time reduces as index increases, tabe scan examples give when large portion of rows in table must be accessed, index does not exist on column searched index exists cannot be used, index unique scan example give example working, index range scan  explain these 3 properly retieve one row index unique scan multiple row index range scan index, incorrect usage of index : no searching critera, no matching indexed using function on indexed column negative criteria no match on first column and express explain these crisply with single examples proeprly , index correct usage: search by primary key search on non unique column range search partial match like at end like at start multiple index match full match independent of order in where startement index advantages distdvantages index improve performance of select reduce performance of where , enforce integrity constraints how index can be located query for that ony questions give no theory what and all tricky mcqs can be asked from it make a quiz of 30 questions all tricky advanced take time and think and give based on above concepts give only give question mcq and asnwer not quiz interface only based on these topics give about index properties theory properties give table name index created on table and query whehter that query will be table scan index unique scan index range scan, which index will be used for particular query given table index on table and query and out of these index which will be used, given table index created on table which query will use the index which will not index give

### ChatGPT

# Database Indexing - Advanced Theory and 30 Tricky MCQs

This preparation set covers indexing concepts at an advanced SQL developer level, focusing on index creation, index structure, index scans, clustered/non-clustered indexes, index selection, and incorrect index usage.

**Important:** The examples use standard relational database indexing concepts. Exact optimizer decisions and index limits can differ between HSQLDB, SQL Server, Oracle, and other databases. In particular, the maximum of 249 indexes and the one-clustered-index rule are database-specific assumptions, not universal SQL rules.

## Part 1: Advanced MCQ Practice

### Section A - Indexing fundamentals and properties

**Q1.** What is the primary purpose of creating an index on a database table?

A. To reduce the physical size of the table
B. To improve the speed of data retrieval
C. To eliminate duplicate records automatically
D. To prevent INSERT operations

**Answer: B**

**Q2.** Consider the following table:

`EMPLOYEE(emp_id, emp_name, salary, dept_id)`

An index is created on `emp_id`.

```sql
CREATE INDEX idx_emp
ON EMPLOYEE(emp_id);
```

How does the database generally use this index?

A. It searches every row sequentially.
B. It maintains an organized search structure containing indexed values and row references.
C. It creates a duplicate copy of the entire table.
D. It permanently sorts the original table.

**Answer: B**

**Q3.** Which statement about indexes is INCORRECT?

A. Indexes consume additional storage space.
B. Indexes can improve SELECT performance.
C. Indexes can reduce INSERT performance.
D. Indexes eliminate the need for table storage.

**Answer: D**

**Q4.** A table contains 1 million records. An index is created on `emp_id`. Which operation generally benefits most?

A. Retrieving one employee using a unique employee ID
B. Retrieving every employee from the table
C. Updating every employee's salary
D. Deleting all employees

**Answer: A**

**Q5.** What happens when an index is created on a table?

A. Existing table records are permanently rearranged in every database.
B. The database creates an additional data structure for faster searching.
C. Existing records are deleted and reinserted.
D. The table becomes read-only.

**Answer: B**

**Q6.** Which of the following statements about index maintenance is correct?

A. Developers must manually update index entries after every INSERT.
B. The database automatically maintains indexes when records are inserted, updated, or deleted.
C. Indexes are updated only when SELECT statements execute.
D. Indexes are automatically deleted after every UPDATE.

**Answer: B**

**Q7.** A table has 100,000 records and no index. A query searches for one record using a column that is not indexed. Which operation is most likely?

A. Index Unique Scan
B. Index Range Scan
C. Table Scan
D. Clustered Index Seek

**Answer: C**

**Q8.** Which statement about index storage is correct?

A. Index storage is always equal to table storage.
B. Index storage is independent of the indexed columns.
C. Index storage increases with indexed data and index structure requirements.
D. Indexes never consume additional disk space.

**Answer: C**

### Section B - Indexes and data integrity constraints

**Q9.** Consider:

```sql
CREATE TABLE EMPLOYEE (
    emp_id INT PRIMARY KEY,
    emp_name VARCHAR(50),
    email VARCHAR(100) UNIQUE
);
```

Which statement is correct?

A. No index is created automatically.
B. An index is automatically created to support the primary key, and a unique index is generally created to enforce email uniqueness.
C. Only a non-clustered index is always created.
D. A table scan is mandatory for every constraint check.

**Answer: B**

**Q10.** Why does a database create an index for a PRIMARY KEY constraint?

A. To sort all columns alphabetically
B. To enforce uniqueness efficiently and support key lookups
C. To increase the number of duplicate values
D. To avoid storing the primary key

**Answer: B**

**Q11.** Which constraint generally requires the database to ensure that duplicate non-NULL values are not allowed?

A. NOT NULL
B. CHECK
C. UNIQUE
D. DEFAULT

**Answer: C**

**Q12.** An index is created on `salary`. The table contains 500,000 rows. A query retrieves 450,000 rows based on salary.

```sql
SELECT *
FROM EMPLOYEE
WHERE salary > 10000;
```

Which operation may be more efficient?

A. Always Index Unique Scan
B. Table Scan
C. Always Index Range Scan
D. No operation is possible

**Answer: B**

### Section C - Clustered and non-clustered indexes

**Q13.** Which statement correctly describes a clustered index?

A. It stores index entries separately without affecting the organization of table data.
B. It determines the physical/logical organization of table rows according to the index key.
C. It always creates a separate copy of the table.
D. Multiple clustered indexes can exist on the same table.

**Answer: B**

**Q14.** Why can a table have only one clustered index?

A. Because a table can have only one column.
B. Because table rows can have only one clustered ordering at a time.
C. Because clustered indexes do not support multiple columns.
D. Because clustered indexes cannot contain duplicate values.

**Answer: B**

**Q15.** Which statement about non-clustered indexes is correct?

A. They physically sort the original table data.
B. They store an independent index structure containing key values and references to the corresponding rows.
C. They cannot be created manually.
D. They cannot be created on multiple columns.

**Answer: B**

**Q16.** Consider a table:

```sql
EMPLOYEE(emp_id, emp_name, salary, dept_id)
```

A clustered index is created on `emp_id`, and a non-clustered index is created on `salary`.

Which statement is correct?

A. Both indexes physically sort the original table data.
B. The clustered index organizes table rows by `emp_id`; the non-clustered index maintains a separate search structure for `salary`.
C. The non-clustered index replaces the clustered index.
D. The table can no longer accept INSERT operations.

**Answer: B**

**Q17.** A database automatically creates an index when a PRIMARY KEY is defined. Which statement is correct?

A. The index must always be clustered.
B. The index must always be non-clustered.
C. The database generally creates an index to enforce uniqueness, but whether it is clustered or non-clustered depends on the DBMS and its configuration.
D. The primary key never requires an index.

**Answer: C**

**Q18.** According to the database-specific rules assumed in this question set, a table supports a maximum of 249 indexes and one clustered index. A table already has one clustered index and 248 non-clustered indexes. What happens if another non-clustered index is created?

A. It succeeds because there is no limit.
B. It fails because the assumed maximum of 249 indexes has been reached.
C. It replaces the clustered index.
D. It automatically deletes an existing index.

**Answer: B**

### Section D - Index tree and scan operations

**Q19.** Most traditional relational database indexes use which structure for efficient searching?

A. Stack
B. Queue
C. B-tree or B+ tree
D. Linked list only

**Answer: C**

**Q20.** An index is created on a UNIQUE column `emp_id`.

```sql
CREATE UNIQUE INDEX idx_emp
ON EMPLOYEE(emp_id);
```

Consider:

```sql
SELECT *
FROM EMPLOYEE
WHERE emp_id = 105;
```

Which scan is most appropriate?

A. Table Scan
B. Index Unique Scan
C. Index Range Scan
D. Full Table Scan followed by sorting

**Answer: B**

**Q21.** An index exists on a non-unique column `dept_id`.

```sql
CREATE INDEX idx_dept
ON EMPLOYEE(dept_id);
```

Consider:

```sql
SELECT *
FROM EMPLOYEE
WHERE dept_id = 10;
```

Multiple employees can belong to department 10. Which scan is generally appropriate?

A. Index Unique Scan
B. Index Range Scan
C. Table Scan is compulsory
D. No index operation is possible

**Answer: B**

**Q22.** An index exists on `salary`.

```sql
SELECT *
FROM EMPLOYEE
WHERE salary BETWEEN 30000 AND 60000;
```

Which operation is generally appropriate?

A. Index Unique Scan
B. Index Range Scan
C. Unique Constraint Scan
D. Primary Key Scan

**Answer: B**

**Q23.** Consider a unique index on `emp_id`.

```sql
SELECT *
FROM EMPLOYEE
WHERE emp_id = 105;
```

Suppose the record does not exist. What happens during an index unique scan?

A. The database must return the nearest employee.
B. The index search determines that no matching key exists and returns no rows.
C. The database automatically inserts the employee.
D. The database must always scan the entire table.

**Answer: B**

**Q24.** A table contains 10,000 rows. A query retrieves 9,500 rows using an indexed column. Which statement is most accurate?

A. An index must always be used because it exists.
B. The optimizer may choose a table scan because accessing most rows through the index may be more expensive.
C. Index Unique Scan is compulsory.
D. The query will fail because too many rows are returned.

**Answer: B**

**Q25.** Which statement correctly differentiates the three operations?

A. Index Unique Scan retrieves exactly one matching row; Index Range Scan retrieves a range or potentially multiple matching rows; Table Scan examines table rows directly.
B. Index Unique Scan retrieves all rows; Index Range Scan retrieves exactly one row.
C. Table Scan always uses an index.
D. Index Range Scan is possible only with primary keys.

**Answer: A**

### Section E - Incorrect and correct index usage

**Q26.** An index exists on `emp_name`.

```sql
SELECT *
FROM EMPLOYEE;
```

Which operation is most likely?

A. Index Unique Scan
B. Index Range Scan
C. Table Scan
D. Index Scan using `emp_name`

**Answer: C**

**Q27.** An index exists on `salary`.

Which query is least likely to use the index efficiently?

A.

```sql
SELECT * FROM EMPLOYEE
WHERE salary = 50000;
```

B.

```sql
SELECT * FROM EMPLOYEE
WHERE salary BETWEEN 30000 AND 50000;
```

C.

```sql
SELECT * FROM EMPLOYEE
WHERE salary + 1000 = 51000;
```

D.

```sql
SELECT * FROM EMPLOYEE
WHERE salary >= 50000;
```

**Answer: C**

**Q28.** An index exists on `emp_name`.

Which query is generally more suitable for using this index?

A.

```sql
SELECT * FROM EMPLOYEE
WHERE emp_name LIKE '%raj';
```

B.

```sql
SELECT * FROM EMPLOYEE
WHERE emp_name LIKE 'raj%';
```

C.

```sql
SELECT * FROM EMPLOYEE
WHERE NOT emp_name = 'Raj';
```

D.

```sql
SELECT * FROM EMPLOYEE
WHERE emp_name IS NOT NULL;
```

**Answer: B**

**Q29.** A composite index is created as follows:

```sql
CREATE INDEX idx_emp
ON EMPLOYEE(dept_id, salary, emp_name);
```

Which queries can generally use the index's leading-column prefix?

A.

```sql
SELECT * FROM EMPLOYEE
WHERE dept_id = 10;
```

B.

```sql
SELECT * FROM EMPLOYEE
WHERE salary = 50000;
```

C.

```sql
SELECT * FROM EMPLOYEE
WHERE emp_name = 'Raj';
```

D.

```sql
SELECT * FROM EMPLOYEE
WHERE salary = 50000
AND emp_name = 'Raj';
```

**Answer: A**

Explanation: The first column of the composite index is `dept_id`. Queries that do not constrain the leading column generally cannot perform an efficient seek using the complete index ordering. Some DBMSs can use skip scans or other optimizations, but that is not the normal left-prefix rule.

**Q30.** A composite index is created:

```sql
CREATE INDEX idx_emp
ON EMPLOYEE(dept_id, salary);
```

Which statement is CORRECT?

A. The following query cannot use the index because the WHERE conditions are written in a different order.

```sql
SELECT *
FROM EMPLOYEE
WHERE salary > 40000
AND dept_id = 10;
```

B. The following query can generally use the composite index because it specifies the leading column.

```sql
SELECT *
FROM EMPLOYEE
WHERE dept_id = 10;
```

C. The following query always uses the complete composite index efficiently.

```sql
SELECT *
FROM EMPLOYEE
WHERE salary > 40000;
```

D. A composite index cannot support equality and range conditions together.

**Answer: B**

Explanation: SQL optimizer decisions do not depend on the order of conditions in the WHERE clause. The index key order matters. An equality condition on the leading column followed by a range condition on the second column is generally an effective composite-index access pattern.

---

## Quick answer key

| Question | Answer | Question | Answer |
| --- | --- | --- | --- |
| 1 | B | 16 | B |
| 2 | B | 17 | C |
| 3 | D | 18 | B |
| 4 | A | 19 | C |
| 5 | B | 20 | B |
| 6 | B | 21 | B |
| 7 | C | 22 | B |
| 8 | C | 23 | B |
| 9 | B | 24 | B |
| 10 | B | 25 | A |
| 11 | C | 26 | C |
| 12 | B | 27 | C |
| 13 | B | 28 | B |
| 14 | B | 29 | A |
| 15 | B | 30 | B |

## Important tricky points to memorize

1. **Index exists ≠ index will always be used.** The optimizer considers selectivity, table size, statistics and retrieval cost.
2. **Unique Scan:** Equality lookup on a unique index.
3. **Range Scan:** Range conditions or lookups that can return multiple rows, including equality lookups on non-unique indexes.
4. **Table Scan:** Reads table rows directly; often preferable when most rows are needed.
5. **Clustered index:** Determines table-row organization; one clustered ordering per table in systems following this model.
6. **Non-clustered index:** Separate index structure; does not reorder the underlying table.
7. **Composite index:** Column order matters; the leftmost-prefix rule is important.
8. **WHERE condition order:** Does not determine index usage.
9. **Functions on indexed columns:** Can prevent ordinary index seeks unless a suitable function-based or computed-column index exists.
10. **LIKE:** `'Raj%'` can use an ordinary ordered index; `'%Raj'` generally cannot perform a normal prefix seek.
11. **Negative conditions:** `NOT`, `<>` and `!=` may result in scans, but index usage is not categorically impossible.
12. **Index maintenance:** Automatic, but every additional index adds write overhead and storage requirements.
13. **Integrity:** Primary key and UNIQUE constraints generally create supporting indexes. NOT NULL and CHECK constraints do not inherently require indexes.
14. **Maximum indexes:** 249 is not a universal database limit. Always follow the specific DBMS specification.

**Exam trap:** An index can exist, match the WHERE column, and still not be selected by the optimizer. Index availability and index utilization are two different things.

### User

indexing intro to indexing example why indexing working of index index tree search algo index for enforcing data integrity,index automatically created for constraint enforcement when u create primary and unique key,index types characterstics clustered index non clustered index clustered auto generated non clustered created manually max 249 per table max 1 clustered index per table clustererd sort table data non clustered do not sort table data, index of primarky key automatically created, consumes additional space, maintained automatically by databe once created we dont have to maintain,size oof index propertional to size of data, can be created on multiple attributes as well composite index , degratation of insert performance with addition of index numer of rows per unit time reduces as index increases, tabe scan examples give when large portion of rows in table must be accessed, index does not exist on column searched index exists cannot be used, index unique scan example give example working, index range scan  explain these 3 properly retieve one row index unique scan multiple row index range scan index, incorrect usage of index : no searching critera, no matching indexed using function on indexed column negative criteria no match on first column and express explain these crisply with single examples proeprly , index correct usage: search by primary key search on non unique column range search partial match like at end like at start multiple index match full match independent of order in where startement index advantages distdvantages index improve performance of select reduce performance of where , enforce integrity constraints how index can be located query for that ony questions give no theory what and all tricky mcqs can be asked from it make a quiz of 30 questions only based on this give given table name index created on table and query whehter that query will be table scan index unique scan index range scan, which index will be used for particular query given table index on table and query and out of these index which will be used, given table index created on table which query will use the index which will not index give

### ChatGPT

# Indexing - Advanced SQL Developer MCQ Test (30 Questions)

(Advanced difficulty) (30 questions)

Questions are based exclusively on your specified indexing topics. The test emphasizes query execution, index selection, composite indexes, scan identification, and tricky edge cases.

**Assumptions for this test:**

- Use the conventional B-tree/B+ tree indexing model.
- Assume indexes are valid and optimizer statistics are available.
- Unless stated otherwise, assume the optimizer chooses an index when it is an efficient access path.
- Index Unique Scan means a unique-key lookup; Index Range Scan includes non-unique equality lookups and range lookups.
- Ignore covering indexes and index-only scans.
- Assume SQL Server-style clustered/non-clustered terminology for the conceptual questions.

## Section A - Identify the execution method

**Q1.** Table: `EMPLOYEE`

Index created:

```sql
CREATE UNIQUE INDEX idx_emp_id
ON EMPLOYEE(emp_id);
```

Query:

```sql
SELECT *
FROM EMPLOYEE
WHERE emp_id = 105;
```

Which operation is most appropriate?

A. Table Scan
B. Index Unique Scan
C. Index Range Scan
D. Full Index Scan

**Answer: B - Index Unique Scan**

---

**Q2.** Table: `EMPLOYEE`

Index created:

```sql
CREATE INDEX idx_dept
ON EMPLOYEE(dept_id);
```

Query:

```sql
SELECT *
FROM EMPLOYEE
WHERE dept_id = 10;
```

Multiple employees can belong to the same department.

A. Table Scan
B. Index Unique Scan
C. Index Range Scan
D. No scan required

**Answer: C - Index Range Scan**

---

**Q3.** Table: `EMPLOYEE`

Index created:

```sql
CREATE INDEX idx_salary
ON EMPLOYEE(salary);
```

Query:

```sql
SELECT *
FROM EMPLOYEE
WHERE salary BETWEEN 30000 AND 50000;
```

A. Table Scan
B. Index Unique Scan
C. Index Range Scan
D. Full Table Sort

**Answer: C - Index Range Scan**

---

**Q4.** Table: `EMPLOYEE`

Available indexes:

```sql
CREATE INDEX idx_salary
ON EMPLOYEE(salary);
```

Query:

```sql
SELECT *
FROM EMPLOYEE;
```

A. Index Unique Scan
B. Index Range Scan
C. Table Scan
D. Index Scan on salary

**Answer: C - Table Scan**

---

**Q5.** Table: `EMPLOYEE`

Available indexes:

```sql
CREATE INDEX idx_salary
ON EMPLOYEE(salary);
```

Query:

```sql
SELECT *
FROM EMPLOYEE
WHERE emp_name = 'Raj';
```

A. Index Unique Scan
B. Index Range Scan on salary
C. Table Scan
D. Index Range Scan on emp_name

**Answer: C - Table Scan**

---

**Q6.** Table: `EMPLOYEE`

Available indexes:

```sql
CREATE INDEX idx_salary
ON EMPLOYEE(salary);
```

Query:

```sql
SELECT *
FROM EMPLOYEE
WHERE salary + 1000 = 51000;
```

Which is the most likely access method using an ordinary index?

A. Index Unique Scan
B. Index Range Scan
C. Table Scan
D. Index Scan on salary is guaranteed

**Answer: C - Table Scan**

---

**Q7.** Table: `EMPLOYEE`

Available indexes:

```sql
CREATE INDEX idx_salary
ON EMPLOYEE(salary);
```

Query:

```sql
SELECT *
FROM EMPLOYEE
WHERE salary >= 50000;
```

A. Index Unique Scan
B. Index Range Scan
C. Table Scan is compulsory
D. No operation

**Answer: B - Index Range Scan**

---

**Q8.** Table: `EMPLOYEE`

Available indexes:

```sql
CREATE INDEX idx_name
ON EMPLOYEE(emp_name);
```

Query:

```sql
SELECT *
FROM EMPLOYEE
WHERE emp_name LIKE 'Raj%';
```

A. Table Scan only
B. Index Unique Scan
C. Index Range Scan
D. No index can ever be used

**Answer: C - Index Range Scan**

---

**Q9.** Table: `EMPLOYEE`

Available indexes:

```sql
CREATE INDEX idx_name
ON EMPLOYEE(emp_name);
```

Query:

```sql
SELECT *
FROM EMPLOYEE
WHERE emp_name LIKE '%Raj';
```

A. Index Unique Scan
B. Index Range Scan using normal prefix lookup
C. Table Scan is generally expected
D. Primary Key Scan

**Answer: C - Table Scan is generally expected**

---

**Q10.** Table: `EMPLOYEE`

Available indexes:

```sql
CREATE INDEX idx_salary
ON EMPLOYEE(salary);
```

Query:

```sql
SELECT *
FROM EMPLOYEE
WHERE salary <> 50000;
```

Which is the most appropriate general answer?

A. Index Unique Scan
B. Index Range Scan is always compulsory
C. Table Scan may be preferred because a large portion of rows may qualify
D. Query is invalid

**Answer: C**

---

## Section B - Composite index and index selection

**Q11.** Table: `EMPLOYEE`

Composite index:

```sql
CREATE INDEX idx_emp
ON EMPLOYEE(dept_id, salary);
```

Which query can efficiently use the leading column of this index?

A.

```sql
SELECT * FROM EMPLOYEE
WHERE dept_id = 10;
```

B.

```sql
SELECT * FROM EMPLOYEE
WHERE salary = 50000;
```

C.

```sql
SELECT * FROM EMPLOYEE
WHERE salary > 50000;
```

D.

```sql
SELECT * FROM EMPLOYEE
WHERE salary = 50000
AND emp_name = 'Raj';
```

**Answer: A**

---

**Q12.** Composite index:

```sql
CREATE INDEX idx_emp
ON EMPLOYEE(dept_id, salary, emp_name);
```

Query:

```sql
SELECT *
FROM EMPLOYEE
WHERE dept_id = 10
AND salary = 50000;
```

Which index is most appropriate?

A. No index can be used because emp_name is missing.
B. `idx_emp` can be used.
C. Only an index on salary can be used.
D. Table Scan is compulsory.

**Answer: B**

---

**Q13.** Composite index:

```sql
CREATE INDEX idx_emp
ON EMPLOYEE(dept_id, salary);
```

Query:

```sql
SELECT *
FROM EMPLOYEE
WHERE salary = 50000
AND dept_id = 10;
```

Which statement is correct?

A. Index cannot be used because salary appears first in WHERE.
B. Index can be used because dept_id is the leading indexed column, regardless of WHERE condition order.
C. Index can be used only if WHERE conditions are written in index order.
D. Only Table Scan is possible.

**Answer: B**

---

**Q14.** Available indexes:

```sql
CREATE INDEX idx_dept_salary
ON EMPLOYEE(dept_id, salary);

CREATE INDEX idx_salary
ON EMPLOYEE(salary);
```

Query:

```sql
SELECT *
FROM EMPLOYEE
WHERE salary = 50000;
```

Which index is the most suitable?

A. `idx_dept_salary` only
B. `idx_salary`
C. Both must be used together
D. Neither index

**Answer: B**

---

**Q15.** Available indexes:

```sql
CREATE INDEX idx_dept_salary
ON EMPLOYEE(dept_id, salary);

CREATE INDEX idx_salary_name
ON EMPLOYEE(salary, emp_name);
```

Query:

```sql
SELECT *
FROM EMPLOYEE
WHERE salary = 50000
AND dept_id = 10;
```

Which index can be used as a suitable access path?

A. `idx_dept_salary` only
B. `idx_salary_name` only
C. Both indexes have a matching leading column for one of the predicates
D. Neither index

**Answer: C**

---

**Q16.** Available indexes:

```sql
CREATE INDEX idx_dept_salary
ON EMPLOYEE(dept_id, salary);
```

Query:

```sql
SELECT *
FROM EMPLOYEE
WHERE dept_id = 10
AND salary BETWEEN 30000 AND 50000;
```

Which statement is correct?

A. The index cannot be used because BETWEEN is a range condition.
B. The index can use dept_id equality followed by a salary range.
C. Only salary can be searched.
D. Table Scan is compulsory.

**Answer: B**

---

**Q17.** Available indexes:

```sql
CREATE INDEX idx_dept_salary
ON EMPLOYEE(dept_id, salary);
```

Query:

```sql
SELECT *
FROM EMPLOYEE
WHERE dept_id > 10
AND salary = 50000;
```

Which statement is most accurate?

A. Both columns can always be used equally as index seek conditions.
B. The index can generally use the leading dept_id range, but salary may be evaluated as a residual filter rather than narrowing the seek.
C. The index cannot be used at all.
D. Index Unique Scan is guaranteed.

**Answer: B**

---

**Q18.** Available indexes:

```sql
CREATE INDEX idx_emp
ON EMPLOYEE(dept_id, salary, emp_name);
```

Which query cannot normally use the leading prefix of this index?

A.

```sql
WHERE dept_id = 10
```

B.

```sql
WHERE dept_id = 10 AND salary = 50000
```

C.

```sql
WHERE dept_id = 10 AND salary = 50000
AND emp_name = 'Raj'
```

D.

```sql
WHERE salary = 50000 AND emp_name = 'Raj'
```

**Answer: D**

---

## Section C - Tricky index usage scenarios

**Q19.** Available index:

```sql
CREATE INDEX idx_salary
ON EMPLOYEE(salary);
```

Query:

```sql
SELECT *
FROM EMPLOYEE
WHERE NOT salary = 50000;
```

Which is the most accurate statement?

A. Index Unique Scan is compulsory.
B. Index Range Scan is always compulsory.
C. A Table Scan may be chosen because the negative condition may retrieve most rows.
D. The query cannot execute.

**Answer: C**

---

**Q20.** Available index:

```sql
CREATE INDEX idx_salary
ON EMPLOYEE(salary);
```

Which query is generally most suitable for using the index?

A.

```sql
WHERE salary = 50000
```

B.

```sql
WHERE salary + 100 = 50100
```

C.

```sql
WHERE salary * 2 = 100000
```

D.

```sql
WHERE salary / 2 = 25000
```

**Answer: A**

---

**Q21.** Available indexes:

```sql
CREATE UNIQUE INDEX idx_emp_id
ON EMPLOYEE(emp_id);

CREATE INDEX idx_dept
ON EMPLOYEE(dept_id);
```

Query:

```sql
SELECT *
FROM EMPLOYEE
WHERE emp_id = 100
AND dept_id = 10;
```

Which index is the most suitable starting access path?

A. `idx_dept`
B. `idx_emp_id`
C. Both must be used
D. Table Scan

**Answer: B**

---

**Q22.** Available indexes:

```sql
CREATE INDEX idx_dept
ON EMPLOYEE(dept_id);

CREATE INDEX idx_salary
ON EMPLOYEE(salary);
```

Query:

```sql
SELECT *
FROM EMPLOYEE
WHERE dept_id = 10
AND salary = 50000;
```

Which statement is correct?

A. Both indexes can never be considered together.
B. The optimizer may use one index, combine index access paths, or choose a scan depending on the DBMS and cost.
C. Only idx_salary can be used because it appears second.
D. Both indexes must always be used.

**Answer: B**

---

**Q23.** Available index:

```sql
CREATE INDEX idx_name
ON EMPLOYEE(emp_name);
```

Query:

```sql
SELECT *
FROM EMPLOYEE
WHERE emp_name LIKE 'A%';
```

Which statement is correct?

A. The index cannot be used because LIKE is present.
B. The index can generally be used because the search has a fixed starting prefix.
C. Index Unique Scan is guaranteed.
D. Table Scan is compulsory.

**Answer: B**

---

**Q24.** Available index:

```sql
CREATE INDEX idx_name
ON EMPLOYEE(emp_name);
```

Query:

```sql
SELECT *
FROM EMPLOYEE
WHERE emp_name LIKE '%A%';
```

Which is the most likely access method using an ordinary B-tree index?

A. Index Unique Scan
B. Index Range Scan using a fixed prefix
C. Table Scan
D. Primary Key Scan

**Answer: C**

---

## Section D - Index properties and constraints

**Q25.** Consider:

```sql
CREATE TABLE EMPLOYEE (
    emp_id INT PRIMARY KEY,
    email VARCHAR(100) UNIQUE,
    emp_name VARCHAR(50)
);
```

Which statement is correct?

A. No indexes are automatically created.
B. Indexes are generally automatically created to support the primary key and UNIQUE constraint.
C. Only emp_name receives an automatic index.
D. Only NOT NULL columns receive indexes.

**Answer: B**

---

**Q26.** A table has one clustered index and 10 non-clustered indexes. What happens when another row is inserted?

A. Only the table data is modified.
B. The database automatically updates the relevant entries in the applicable indexes as well as the table data.
C. All indexes must be manually recreated.
D. The clustered index is automatically removed.

**Answer: B**

---

**Q27.** A table has 5 indexes. A developer adds 15 more indexes.

Which consequence is most likely?

A. SELECT queries always become slower.
B. INSERT, UPDATE and DELETE operations may become slower because more index structures must be maintained.
C. Table storage becomes zero.
D. Duplicate values are automatically eliminated from every column.

**Answer: B**

---

**Q28.** Which statement about clustered and non-clustered indexes is correct?

A. A table can have multiple clustered indexes.
B. A clustered index determines the organization of table rows; a non-clustered index has a separate index structure.
C. Non-clustered indexes always physically sort the original table.
D. Clustered indexes never consume additional storage.

**Answer: B**

---

**Q29.** Which of the following statements is INCORRECT?

A. An index can be created on multiple columns.
B. An index requires additional storage.
C. Indexes are maintained automatically by the database.
D. An index guarantees that every SELECT query will execute faster.

**Answer: D**

---

**Q30.** Consider the following table:

```sql
CREATE TABLE EMPLOYEE (
    emp_id INT PRIMARY KEY,
    emp_name VARCHAR(50),
    dept_id INT,
    salary INT,
    email VARCHAR(100) UNIQUE
);
```

Additional indexes:

```sql
CREATE INDEX idx_dept_salary
ON EMPLOYEE(dept_id, salary);

CREATE INDEX idx_name
ON EMPLOYEE(emp_name);

CREATE INDEX idx_salary
ON EMPLOYEE(salary);
```

Which query is most likely to use an Index Unique Scan?

A.

```sql
SELECT *
FROM EMPLOYEE
WHERE dept_id = 10;
```

B.

```sql
SELECT *
FROM EMPLOYEE
WHERE salary BETWEEN 30000 AND 50000;
```

C.

```sql
SELECT *
FROM EMPLOYEE
WHERE emp_id = 101;
```

D.

```sql
SELECT *
FROM EMPLOYEE
WHERE emp_name LIKE 'Raj%';
```

**Answer: C**

---

## Final answer key

| Q | Answer | Q | Answer | Q | Answer |
| --- | --- | --- | --- | --- | --- |
| 1 | B | 11 | A | 21 | B |
| 2 | C | 12 | B | 22 | B |
| 3 | C | 13 | B | 23 | B |
| 4 | C | 14 | B | 24 | C |
| 5 | C | 15 | C | 25 | B |
| 6 | C | 16 | B | 26 | B |
| 7 | B | 17 | B | 27 | B |
| 8 | C | 18 | D | 28 | B |
| 9 | C | 19 | C | 29 | D |
| 10 | C | 20 | A | 30 | C |

**Important exam distinction:** An index's existence does not guarantee its selection. The optimizer considers the index's column order, the search condition, the number of matching rows and the cost of retrieving the data. Also, Index Unique Scan and Index Range Scan are execution-plan terminology whose exact names vary across database systems.

### User

for 2 year sql developer hsql database level give concepts needed from required topics all tricky advanced topics from these explanation and 15 question quiz at end all edge cases data control language why dcl,grant revoke syntax grant previlge object grantee previlage: select delete update all object tabe view routine sequence all example table particular column ny grant or revoke previlage be probided to both user and roles ony questions give no theory what and all tricky mcqs can be asked from it make a quiz of 60 questions all tricky advanced take time and think and give based on above concepts give only give question mcq and asnwer not quiz interface

### ChatGPT

# HSQLDB - Data Control Language (DCL): Advanced SQL Developer Preparation

(2-year SQL Developer level) (60 advanced MCQs)

The questions cover DCL, GRANT, REVOKE, privileges, users, roles, object permissions, column-level permissions, and tricky authorization scenarios.

**HSQLDB-specific assumptions:** These questions use SQL-standard-style authorization concepts, with HSQLDB syntax and behavior as the target. Some privileges and grant options vary by HSQLDB version. In particular, do not assume that every database supports every privilege on every object type.

## Section A - DCL fundamentals and GRANT syntax

**Q1.** What is the primary purpose of Data Control Language (DCL)?

A. To create and delete database tables
B. To control access permissions and privileges
C. To insert and update records
D. To define relationships between tables

**Answer: B**

**Q2.** Which two statements are primarily associated with DCL?

A. INSERT and UPDATE
B. CREATE and DROP
C. GRANT and REVOKE
D. COMMIT and ROLLBACK

**Answer: C**

**Q3.** Which is the correct general syntax for granting SELECT privilege on a table?

A.

```sql
GRANT SELECT ON EMPLOYEE TO USER1;
```

B.

```sql
GRANT EMPLOYEE SELECT TO USER1;
```

C.

```sql
GRANT SELECT USER1 ON EMPLOYEE;
```

D.

```sql
SELECT GRANT ON EMPLOYEE TO USER1;
```

**Answer: A**

**Q4.** Consider:

```sql
GRANT SELECT, INSERT, UPDATE
ON EMPLOYEE
TO USER1;
```

What privileges does USER1 receive?

A. SELECT only
B. SELECT, INSERT and UPDATE
C. All privileges including DELETE
D. SELECT and DELETE only

**Answer: B**

**Q5.** Which statement grants all available table privileges to USER1?

A.

```sql
GRANT ALL ON EMPLOYEE TO USER1;
```

B.

```sql
GRANT ALL PRIVILEGES TO EMPLOYEE;
```

C.

```sql
GRANT EMPLOYEE TO USER1;
```

D.

```sql
GRANT * ON EMPLOYEE TO USER1;
```

**Answer: A**

**Q6.** Which statement correctly grants DELETE privilege?

A.

```sql
GRANT DELETE ON EMPLOYEE TO USER1;
```

B.

```sql
GRANT REMOVE ON EMPLOYEE TO USER1;
```

C.

```sql
GRANT DROP ON EMPLOYEE TO USER1;
```

D.

```sql
GRANT ERASE ON EMPLOYEE TO USER1;
```

**Answer: A**

**Q7.** Which of the following is NOT a normal table-level data privilege?

A. SELECT
B. INSERT
C. UPDATE
D. CREATE TABLE ON EMPLOYEE

**Answer: D**

**Q8.** Which statement is correct regarding GRANT?

A. GRANT removes privileges.
B. GRANT assigns privileges to an authorization identifier such as a user or role.
C. GRANT deletes a user.
D. GRANT modifies table structure.

**Answer: B**

**Q9.** Consider:

```sql
GRANT SELECT ON EMPLOYEE TO USER1;
```

What is the grantee?

A. EMPLOYEE
B. SELECT
C. USER1
D. The database administrator

**Answer: C**

**Q10.** In the following statement:

```sql
GRANT UPDATE ON EMPLOYEE TO USER1;
```

Identify the privilege, object and grantee respectively.

A. USER1, EMPLOYEE, UPDATE
B. UPDATE, EMPLOYEE, USER1
C. EMPLOYEE, UPDATE, USER1
D. UPDATE, USER1, EMPLOYEE

**Answer: B**

## Section B - Object-level privileges

**Q11.** Consider:

```sql
GRANT SELECT ON EMPLOYEE TO USER1;
```

Which operation is permitted to USER1?

A. SELECT from EMPLOYEE
B. INSERT into EMPLOYEE
C. DELETE from EMPLOYEE
D. UPDATE EMPLOYEE

**Answer: A**

**Q12.** USER1 receives:

```sql
GRANT SELECT, UPDATE ON EMPLOYEE TO USER1;
```

Which operation is NOT permitted based on these grants?

A. SELECT employee records
B. UPDATE employee records
C. DELETE employee records
D. Read all accessible columns

**Answer: C**

**Q13.** A user receives SELECT privilege on a table. Which statement is correct?

A. The user automatically receives INSERT privilege.
B. The user automatically receives UPDATE privilege.
C. The user can retrieve data but does not automatically receive modification privileges.
D. The user can drop the table.

**Answer: C**

**Q14.** Which statement grants SELECT and DELETE on EMPLOYEE to USER1?

A.

```sql
GRANT SELECT, DELETE ON EMPLOYEE TO USER1;
```

B.

```sql
GRANT SELECT AND DELETE ON EMPLOYEE TO USER1;
```

C.

```sql
GRANT SELECT OR DELETE ON EMPLOYEE TO USER1;
```

D.

```sql
GRANT SELECT DELETE TO USER1;
```

**Answer: A**

**Q15.** Consider:

```sql
GRANT UPDATE ON EMPLOYEE TO USER1;
```

Which statement is correct?

A. USER1 can update the table's data but does not automatically receive permission to alter its structure.
B. USER1 can add columns.
C. USER1 can drop the table.
D. USER1 can create indexes on every database table.

**Answer: A**

**Q16.** A user receives DELETE privilege on EMPLOYEE. What does this privilege allow?

A. Deleting the table structure
B. Deleting rows from EMPLOYEE
C. Deleting the database
D. Dropping every constraint

**Answer: B**

**Q17.** Which privilege is most directly associated with allowing a user to reference a table's columns in a foreign key definition?

A. SELECT
B. UPDATE
C. REFERENCES
D. DELETE

**Answer: C**

**Q18.** A user receives INSERT privilege on EMPLOYEE. Which operation is authorized by that privilege?

A. Insert new rows into EMPLOYEE
B. Update existing rows
C. Delete existing rows
D. Drop EMPLOYEE

**Answer: A**

**Q19.** Consider:

```sql
GRANT SELECT ON EMPLOYEE TO USER1;
GRANT INSERT ON EMPLOYEE TO USER1;
```

Which statement is correct?

A. The second GRANT replaces SELECT.
B. USER1 receives both SELECT and INSERT privileges.
C. USER1 loses all privileges.
D. USER1 receives DELETE automatically.

**Answer: B**

**Q20.** Which privilege combination permits reading, inserting, modifying and deleting table records?

A.

```sql
GRANT SELECT, INSERT, UPDATE, DELETE
ON EMPLOYEE TO USER1;
```

B.

```sql
GRANT SELECT, CREATE, DROP, ALTER
ON EMPLOYEE TO USER1;
```

C.

```sql
GRANT ALL TABLES TO USER1;
```

D.

```sql
GRANT DML ON EMPLOYEE TO USER1;
```

**Answer: A**

## Section C - Column-level privileges

**Q21.** Which statement grants UPDATE permission only on the salary column?

A.

```sql
GRANT UPDATE(salary)
ON EMPLOYEE TO USER1;
```

B.

```sql
GRANT UPDATE ON EMPLOYEE(salary) TO USER1;
```

C.

```sql
GRANT UPDATE (salary)
ON EMPLOYEE TO USER1;
```

D.

```sql
GRANT salary UPDATE ON EMPLOYEE TO USER1;
```

**Answer: C**

**Q22.** Consider:

```sql
GRANT UPDATE (salary)
ON EMPLOYEE TO USER1;
```

Which operation is authorized by this grant?

A. Updating emp_name
B. Updating salary
C. Deleting salary
D. Inserting any column

**Answer: B**

**Q23.** USER1 receives:

```sql
GRANT UPDATE (salary)
ON EMPLOYEE TO USER1;
```

Which UPDATE statement is permitted by this column-level grant alone?

A.

```sql
UPDATE EMPLOYEE
SET salary = 50000
WHERE emp_id = 10;
```

B.

```sql
UPDATE EMPLOYEE
SET emp_name = 'Raj'
WHERE emp_id = 10;
```

C.

```sql
UPDATE EMPLOYEE
SET salary = 50000,
    emp_name = 'Raj'
WHERE emp_id = 10;
```

D. Both A and C

**Answer: A**

**Q24.** Consider:

```sql
GRANT UPDATE (salary, commission)
ON EMPLOYEE TO USER1;
```

Which columns can USER1 update through this grant?

A. salary only
B. commission only
C. salary and commission
D. All columns

**Answer: C**

**Q25.** USER1 receives:

```sql
GRANT SELECT ON EMPLOYEE TO USER1;
GRANT UPDATE (salary) ON EMPLOYEE TO USER1;
```

Which statement is correct?

A. USER1 can read the table and update salary.
B. USER1 can update every column.
C. USER1 can delete rows.
D. USER1 cannot read salary.

**Answer: A**

**Q26.** USER1 receives:

```sql
GRANT UPDATE (salary)
ON EMPLOYEE TO USER1;
```

Can USER1 automatically read the salary column?

A. Yes, UPDATE automatically includes SELECT.
B. No, UPDATE and SELECT are distinct privileges.
C. Yes, only if salary is numeric.
D. Yes, if the table has a primary key.

**Answer: B**

**Q27.** Which statement correctly grants SELECT permission on a view?

A.

```sql
GRANT SELECT ON EMPLOYEE_VIEW TO USER1;
```

B.

```sql
GRANT VIEW ON EMPLOYEE_VIEW TO USER1;
```

C.

```sql
GRANT READ VIEW TO USER1;
```

D.

```sql
GRANT SELECT VIEW TO USER1;
```

**Answer: A**

**Q28.** A user receives SELECT privilege on a view but no direct SELECT privilege on its underlying table. Which statement is most accurate?

A. SELECT on a view is never possible without direct table SELECT.
B. The user may query the view subject to the database's view authorization and underlying privilege rules.
C. The user automatically receives all privileges on the underlying table.
D. The user can drop the underlying table.

**Answer: B**

**Q29.** Consider:

```sql
GRANT SELECT ON EMPLOYEE TO USER1;
GRANT UPDATE (salary) ON EMPLOYEE TO USER1;
```

Which privilege does USER1 lack?

A. SELECT on EMPLOYEE
B. UPDATE on salary
C. UPDATE on emp_name
D. Both SELECT and UPDATE on salary

**Answer: C**

**Q30.** Which statement about column-level UPDATE privilege is correct?

A. It grants permission to update the entire row without restrictions.
B. It limits the columns that may be updated through that grant.
C. It automatically grants DELETE.
D. It automatically grants INSERT.

**Answer: B**

## Section E - REVOKE and privilege removal

**Q31.** Which is the correct syntax for revoking SELECT privilege?

A.

```sql
REVOKE SELECT ON EMPLOYEE FROM USER1;
```

B.

```sql
REVOKE SELECT ON EMPLOYEE TO USER1;
```

C.

```sql
REMOVE SELECT FROM USER1;
```

D.

```sql
DELETE SELECT ON EMPLOYEE FROM USER1;
```

**Answer: A**

**Q32.** Consider:

```sql
GRANT SELECT, INSERT, UPDATE
ON EMPLOYEE TO USER1;
```

Then:

```sql
REVOKE INSERT
ON EMPLOYEE FROM USER1;
```

Which privileges remain?

A. INSERT only
B. SELECT and UPDATE
C. UPDATE only
D. No privileges

**Answer: B**

**Q33.** Consider:

```sql
GRANT SELECT ON EMPLOYEE TO USER1;
GRANT UPDATE ON EMPLOYEE TO USER1;
REVOKE SELECT ON EMPLOYEE FROM USER1;
```

What can USER1 do?

A. SELECT only
B. UPDATE only
C. SELECT and UPDATE
D. Neither SELECT nor UPDATE

**Answer: B**

**Q34.** USER1 receives:

```sql
GRANT SELECT ON EMPLOYEE TO USER1;
GRANT INSERT ON EMPLOYEE TO USER1;
```

Which statement revokes both privileges?

A.

```sql
REVOKE ALL ON EMPLOYEE FROM USER1;
```

B.

```sql
REVOKE SELECT, INSERT ON EMPLOYEE FROM USER1;
```

C.

```sql
DROP USER USER1;
```

D.

```sql
DELETE ALL ON EMPLOYEE FROM USER1;
```

**Answer: B**

**Q35.** Consider:

```sql
GRANT UPDATE (salary)
ON EMPLOYEE TO USER1;
```

Which statement revokes only the column-level UPDATE privilege?

A.

```sql
REVOKE UPDATE (salary)
ON EMPLOYEE FROM USER1;
```

B.

```sql
REVOKE salary FROM USER1;
```

C.

```sql
REVOKE UPDATE ON salary FROM USER1;
```

D.

```sql
DROP COLUMN salary;
```

**Answer: A**

**Q36.** USER1 has:

```sql
GRANT UPDATE (salary, commission)
ON EMPLOYEE TO USER1;
```

Then:

```sql
REVOKE UPDATE (salary)
ON EMPLOYEE FROM USER1;
```

Which column-level UPDATE permission remains from this grant?

A. salary only
B. commission only
C. Both columns
D. Neither column

**Answer: B**

**Q37.** Which statement about REVOKE is correct?

A. REVOKE deletes the database object.
B. REVOKE withdraws specified privileges from a user or role.
C. REVOKE deletes all rows from a table.
D. REVOKE changes the table structure.

**Answer: B**

**Q38.** Consider:

```sql
GRANT SELECT ON EMPLOYEE TO USER1;
GRANT SELECT ON EMPLOYEE TO USER2;
```

Then:

```sql
REVOKE SELECT ON EMPLOYEE FROM USER1;
```

What happens to USER2's SELECT privilege?

A. It is also revoked.
B. It remains unaffected.
C. The EMPLOYEE table is dropped.
D. Both users lose all privileges.

**Answer: B**

**Q39.** Which statement correctly revokes DELETE privilege?

A.

```sql
REVOKE DELETE ON EMPLOYEE FROM USER1;
```

B.

```sql
REVOKE DROP ON EMPLOYEE FROM USER1;
```

C.

```sql
REVOKE REMOVE ON EMPLOYEE TO USER1;
```

D.

```sql
DELETE PRIVILEGE ON EMPLOYEE FROM USER1;
```

**Answer: A**

**Q40.** Consider:

```sql
GRANT ALL PRIVILEGES
ON EMPLOYEE TO USER1;
```

Which statement about the meaning of ALL PRIVILEGES is correct?

A. It grants every possible database administration privilege.
B. It grants all privileges the grantor is authorized to grant on that specified object.
C. It grants DBA automatically.
D. It grants access to every table in every schema.

**Answer: B**

## Section F - GRANT OPTION, CASCADE and RESTRICT

**Q41.** Consider:

```sql
GRANT SELECT
ON EMPLOYEE
TO USER1
WITH GRANT OPTION;
```

What additional capability does USER1 receive?

A. USER1 can grant the SELECT privilege to other users or roles.
B. USER1 becomes DBA.
C. USER1 can drop EMPLOYEE.
D. USER1 can grant every privilege on every table.

**Answer: A**

**Q42.** USER1 receives:

```sql
GRANT SELECT
ON EMPLOYEE
TO USER1
WITH GRANT OPTION;
```

USER1 executes:

```sql
GRANT SELECT ON EMPLOYEE TO USER2;
```

Which statement is correct?

A. USER1 cannot grant SELECT to USER2.
B. USER1 can grant SELECT because USER1 received the grant option.
C. USER2 becomes the owner of EMPLOYEE.
D. USER2 automatically receives UPDATE.

**Answer: B**

**Q43.** USER1 receives SELECT with GRANT OPTION and grants SELECT to USER2. The original grant to USER1 is subsequently revoked.

What is the relevant issue?

A. Whether USER2 has DBA privileges
B. Whether the dependent grant to USER2 is also revoked through CASCADE or prevents revocation through RESTRICT
C. Whether USER2 has INSERT privilege
D. Whether the table has a primary key

**Answer: B**

**Q44.** Which statement is used to revoke the ability to grant a privilege to others without necessarily revoking the underlying privilege itself?

A.

```sql
REVOKE GRANT OPTION FOR SELECT
ON EMPLOYEE FROM USER1 CASCADE;
```

B.

```sql
REVOKE SELECT
ON EMPLOYEE FROM USER1;
```

C.

```sql
DROP GRANT OPTION USER1;
```

D.

```sql
REVOKE DBA FROM USER1;
```

**Answer: A**

**Q45.** What does CASCADE mean in a REVOKE operation?

A. Revokes the privilege and handles dependent grants by cascading the revocation.
B. Automatically grants the privilege to all users.
C. Deletes the underlying table.
D. Revokes all privileges in the database.

**Answer: A**

**Q46.** What does RESTRICT generally mean in a REVOKE operation?

A. Always revoke the privilege regardless of dependent grants.
B. Prevent revocation if dependent privileges would be affected.
C. Delete the grantee.
D. Convert the privilege into a role.

**Answer: B**

**Q47.** Consider:

```sql
GRANT SELECT ON EMPLOYEE
TO USER1 WITH GRANT OPTION;

GRANT SELECT ON EMPLOYEE TO USER2;
```

Which statement is correct?

A. USER2 must also receive WITH GRANT OPTION automatically.
B. USER2 receives SELECT but does not automatically receive GRANT OPTION.
C. USER2 receives DBA.
D. USER1 loses SELECT.

**Answer: B**

**Q48.** Which statement is correct regarding grantors?

A. Any user can grant any privilege on any object.
B. A grantor must possess sufficient authority to grant the specified privilege.
C. Only the grantee can grant privileges.
D. A grantor must always be DBA, even when the schema owner has authority to grant the privilege.

**Answer: B**

## Section G - Roles and users

**Q49.** Which statement creates a role in HSQLDB?

A.

```sql
CREATE ROLE developer;
```

B.

```sql
CREATE USER ROLE developer;
```

C.

```sql
GRANT ROLE developer;
```

D.

```sql
ADD ROLE developer;
```

**Answer: A**

**Q50.** Consider:

```sql
CREATE ROLE DEV_ROLE;
GRANT SELECT, INSERT
ON EMPLOYEE TO DEV_ROLE;
GRANT DEV_ROLE TO USER1;
```

What is the result?

A. USER1 receives the privileges assigned to DEV_ROLE through role membership.
B. USER1 becomes the owner of EMPLOYEE.
C. DEV_ROLE is deleted.
D. USER1 receives only SELECT.

**Answer: A**

**Q51.** Which is the correct syntax for granting a role to a user?

A.

```sql
GRANT DEV_ROLE TO USER1;
```

B.

```sql
GRANT USER1 TO DEV_ROLE;
```

C.

```sql
GRANT ROLE TO USER1;
```

D.

```sql
CREATE ROLE USER1;
```

**Answer: A**

**Q52.** Consider:

```sql
CREATE ROLE R1;
CREATE ROLE R2;

GRANT SELECT ON EMPLOYEE TO R1;
GRANT R1 TO R2;
GRANT R2 TO USER1;
```

What can USER1 obtain through this role hierarchy?

A. SELECT privilege on EMPLOYEE
B. DBA automatically
C. DELETE privilege on EMPLOYEE
D. No privileges because roles cannot be granted to roles

**Answer: A**

**Q53.** Which statement removes a role from a user?

A.

```sql
REVOKE DEV_ROLE FROM USER1;
```

B.

```sql
DROP DEV_ROLE FROM USER1;
```

C.

```sql
DELETE ROLE DEV_ROLE FROM USER1;
```

D.

```sql
REVOKE USER1 FROM DEV_ROLE;
```

**Answer: A**

**Q54.** Consider:

```sql
CREATE ROLE DEV_ROLE;
GRANT SELECT ON EMPLOYEE TO DEV_ROLE;
GRANT DEV_ROLE TO USER1;
GRANT DEV_ROLE TO USER2;
```

Then:

```sql
REVOKE DEV_ROLE FROM USER1;
```

What happens?

A. USER1 loses access obtained through DEV_ROLE, while USER2 retains role membership.
B. DEV_ROLE is deleted.
C. USER2 also loses role membership.
D. EMPLOYEE is deleted.

**Answer: A**

**Q55.** Which statement about roles is correct?

A. A role can contain multiple privileges and can be assigned to multiple users.
B. A role can be assigned to only one user.
C. A role cannot contain object privileges.
D. A role is the same as a table.

**Answer: A**

## Section H - Object types and advanced HSQLDB edge cases

**Q56.** Consider the following objects:

- EMPLOYEE table
- EMPLOYEE_VIEW view
- EMP_SEQ sequence
- CALCULATE_SALARY procedure

Which combination of privileges is correct in HSQLDB?

A. SELECT on table, SELECT on view, USAGE on sequence, EXECUTE on routine
B. EXECUTE on table, DELETE on sequence, SELECT on procedure
C. INSERT on sequence, UPDATE on procedure, DELETE on view
D. CREATE on every object

**Answer: A**

**Q57.** Which statement correctly grants permission to use a sequence?

A.

```sql
GRANT USAGE ON SEQUENCE EMP_SEQ TO USER1;
```

B.

```sql
GRANT SELECT ON SEQUENCE EMP_SEQ TO USER1;
```

C.

```sql
GRANT UPDATE ON SEQUENCE EMP_SEQ TO USER1;
```

D.

```sql
GRANT INSERT ON SEQUENCE EMP_SEQ TO USER1;
```

**Answer: A**

**Q58.** Which statement correctly grants permission to execute a stored procedure?

A.

```sql
GRANT EXECUTE ON ROUTINE CALCULATE_SALARY TO USER1;
```

B.

```sql
GRANT SELECT ON ROUTINE CALCULATE_SALARY TO USER1;
```

C.

```sql
GRANT INSERT ON PROCEDURE CALCULATE_SALARY TO USER1;
```

D.

```sql
GRANT UPDATE ON ROUTINE CALCULATE_SALARY TO USER1;
```

**Answer: A**

**Q59.** Consider:

```sql
GRANT SELECT (emp_id, emp_name)
ON EMPLOYEE TO USER1;
```

Which query can USER1 execute based on this column-level grant alone?

A.

```sql
SELECT emp_id, emp_name
FROM EMPLOYEE;
```

B.

```sql
SELECT *
FROM EMPLOYEE;
```

C.

```sql
SELECT salary
FROM EMPLOYEE;
```

D. Both A and C

**Answer: A**

**Q60.** Consider:

```sql
GRANT INSERT (emp_id, emp_name)
ON EMPLOYEE TO USER1;
```

The table has the following columns:

- `emp_id` - NOT NULL, no default
- `emp_name` - NOT NULL, no default
- `salary` - DEFAULT 30000

Which statement is correct?

A. USER1 can insert a row by explicitly providing emp_id and emp_name while allowing salary to take its default value.
B. USER1 can insert any arbitrary column values.
C. USER1 can update salary.
D. USER1 can delete rows.

**Answer: A**

---

## Final HSQLDB exam traps

These are the HSQLDB-specific details behind the questions:

- Column-level `SELECT`, `INSERT` and `UPDATE` privileges are supported.
- `DELETE` is a table-level privilege, not a column-level privilege.
- `REFERENCES` can be granted at table or column level.
- Sequences use `USAGE`.
- Procedures and functions use `EXECUTE`.
- Tables and views support object-level privileges.
- A role can be granted to another role or to a user.
- `WITH GRANT OPTION` and `WITH ADMIN OPTION` are different: the former concerns object privileges; the latter concerns role administration.
- `ALL PRIVILEGES` means all privileges the grantor can grant on the specified object, not unrestricted DBA access.

Official reference: HSQLDB 2.7 - Chapter 8: Access Control.

**Total: 60 questions.** All questions include their answers immediately after the options.

### User

for 2 year sql developer hsql database level give concepts needed from required topics all tricky advanced topics from these explanation and 15 question quiz at end all edge cases data control language why dcl,grant revoke syntax grant previlge object grantee previlage: select delete update all object tabe view routine sequence all example table particular column ny grant or revoke previlage be probided to both user and roles ony questions give no theory what and all tricky mcqs can be asked from it make a quiz of 60 questions all tricky expert take time and think and give based on above concepts give only give question mcq and asnwer not quiz interface

### ChatGPT

# HSQLDB DCL - Expert-Level SQL Developer MCQ Test

(Expert difficulty) (60 questions)

**Scope:** HSQLDB 2.x, DCL, GRANT, REVOKE, object privileges, users, roles, column-level privileges, grant option, admin option, CASCADE, RESTRICT, tables, views, routines and sequences.

Questions are designed around actual SQL statements, authorization scenarios, privilege combinations, and execution edge cases.

## Section A - DCL, authorization and GRANT syntax

**Q1.** A database administrator creates a table named `EMPLOYEE`. A newly created user `DEV1` attempts:

```sql
SELECT * FROM EMPLOYEE;
```

The query fails due to insufficient privileges. Which statement correctly provides access?

A.

```sql
GRANT EMPLOYEE TO DEV1;
```

B.

```sql
GRANT SELECT ON EMPLOYEE TO DEV1;
```

C.

```sql
GRANT READ EMPLOYEE TO DEV1;
```

D.

```sql
GRANT ACCESS ON EMPLOYEE TO DEV1;
```

**Answer: B**

**Q2.** Which is the correct HSQLDB syntax for granting multiple privileges on a table to multiple grantees?

A.

```sql
GRANT SELECT, INSERT ON EMPLOYEE
TO DEV1, DEV2;
```

B.

```sql
GRANT SELECT AND INSERT ON EMPLOYEE
TO DEV1, DEV2;
```

C.

```sql
GRANT SELECT, INSERT TO DEV1, DEV2
ON EMPLOYEE;
```

D.

```sql
GRANT ALL SELECT, INSERT ON EMPLOYEE
TO DEV1, DEV2;
```

**Answer: A**

**Q3.** Consider:

```sql
GRANT ALL PRIVILEGES ON EMPLOYEE TO DEV1;
```

Which statement is correct?

A. DEV1 receives every privilege available in the entire database.
B. DEV1 receives all privileges that the grantor can grant on EMPLOYEE.
C. DEV1 automatically becomes the schema owner.
D. DEV1 receives DBA privileges.

**Answer: B**

**Q4.** A schema owner has SELECT, INSERT and UPDATE privileges on `EMPLOYEE`, but does not have DELETE privilege. The owner executes:

```sql
GRANT ALL PRIVILEGES ON EMPLOYEE TO DEV1;
```

Which statement is correct?

A. DEV1 receives SELECT, INSERT, UPDATE and DELETE.
B. DEV1 receives only the privileges the grantor can grant.
C. The statement automatically grants DBA.
D. The statement must fail because ALL cannot be used.

**Answer: B**

**Q5.** Which of the following correctly identifies the grantee in this statement?

```sql
GRANT SELECT ON EMPLOYEE TO DEV1;
```

A. SELECT
B. EMPLOYEE
C. DEV1
D. Current schema

**Answer: C**

**Q6.** Which statement about HSQLDB authorization is correct?

A. Every newly created user automatically receives SELECT on all tables.
B. A schema owner can grant privileges on schema objects to other users and roles.
C. Every user can grant privileges on every object.
D. Only DBA can ever grant object privileges.

**Answer: B**

**Q7.** Which statement correctly creates a user in HSQLDB?

A.

```sql
CREATE USER DEV1 PASSWORD 'pass123';
```

B.

```sql
CREATE LOGIN DEV1 PASSWORD 'pass123';
```

C.

```sql
CREATE ROLE DEV1 PASSWORD 'pass123';
```

D.

```sql
GRANT USER DEV1 PASSWORD 'pass123';
```

**Answer: A**

**Q8.** Consider:

```sql
CREATE USER DEV1 PASSWORD 'pass123' ADMIN;
```

What is the effect of ADMIN?

A. DEV1 receives only SELECT privilege.
B. DEV1 receives the DBA role.
C. DEV1 becomes a table owner automatically.
D. DEV1 receives only CREATE TABLE privilege.

**Answer: B**

**Q9.** Which statement is correct about the PUBLIC grantee?

A. PUBLIC represents only users created before the GRANT statement.
B. PUBLIC represents all non-admin users, including users created later.
C. PUBLIC represents only DBA users.
D. PUBLIC represents database roles only.

**Answer: B**

**Q10.** Consider:

```sql
GRANT SELECT ON EMPLOYEE TO PUBLIC;
```

A new non-admin user `DEV3` is subsequently created. What is the result?

A. DEV3 automatically receives SELECT access through PUBLIC.
B. DEV3 must receive an individual SELECT grant.
C. DEV3 cannot access EMPLOYEE.
D. The grant expires when a new user is created.

**Answer: A**

## Section B - Table and view privileges

**Q11.** Consider:

```sql
GRANT SELECT, UPDATE, DELETE
ON EMPLOYEE TO DEV1;
```

Which operation is not authorized by this statement?

A. SELECT employee records
B. UPDATE employee records
C. DELETE employee records
D. INSERT employee records

**Answer: D**

**Q12.** Which statement is valid in HSQLDB for granting SELECT on a view?

A.

```sql
GRANT SELECT ON EMPLOYEE_VIEW TO DEV1;
```

B.

```sql
GRANT VIEW ON EMPLOYEE_VIEW TO DEV1;
```

C.

```sql
GRANT READ VIEW TO DEV1;
```

D.

```sql
GRANT SELECT VIEW TO DEV1;
```

**Answer: A**

**Q13.** Consider:

```sql
GRANT SELECT ON EMPLOYEE TO DEV1;
```

Which statement is correct?

A. DEV1 can retrieve records but does not automatically receive UPDATE.
B. DEV1 can retrieve and delete records.
C. DEV1 can retrieve and insert records.
D. DEV1 receives all DML privileges.

**Answer: A**

**Q14.** Consider:

```sql
GRANT DELETE ON EMPLOYEE TO DEV1;
```

Which statement is correct?

A. DEV1 can delete only the `salary` column.
B. DEV1 receives table-level DELETE privilege, not a column-specific DELETE privilege.
C. DEV1 can drop EMPLOYEE.
D. DEV1 receives DELETE privilege on all database tables.

**Answer: B**

**Q15.** Which privilege combination is required for a user to perform ordinary INSERT, UPDATE and DELETE operations, assuming all referenced columns are accessible?

A. SELECT only
B. INSERT, UPDATE and DELETE
C. CREATE, ALTER and DROP
D. REFERENCES, USAGE and EXECUTE

**Answer: B**

**Q16.** Consider:

```sql
GRANT SELECT ON EMPLOYEE TO DEV1;
GRANT SELECT ON DEPARTMENT TO DEV1;
REVOKE SELECT ON EMPLOYEE FROM DEV1 CASCADE;
```

Which statement is correct?

A. SELECT is revoked from both tables.
B. SELECT is revoked from EMPLOYEE, but the independent grant on DEPARTMENT remains.
C. SELECT is revoked from DEPARTMENT only.
D. Both tables are dropped.

**Answer: B**

**Q17.** A user has SELECT privilege on `EMPLOYEE_VIEW`, but no direct SELECT privilege on the underlying EMPLOYEE table. Which statement is most accurate?

A. A view can never have separately granted SELECT privileges.
B. The user may access the view subject to HSQLDB's view and underlying authorization rules.
C. The user automatically receives all underlying table privileges.
D. The user automatically becomes the view owner.

**Answer: B**

**Q18.** Which statement about a table's TRIGGER privilege is correct?

A. It grants permission to add a trigger to that table.
B. It grants permission to execute every stored procedure.
C. It grants permission to delete all records.
D. It grants permission to create sequences.

**Answer: A**

**Q19.** Which privilege allows a user to define a foreign key referencing another table?

A. USAGE
B. EXECUTE
C. REFERENCES
D. TRIGGER

**Answer: C**

**Q20.** Consider:

```sql
GRANT REFERENCES(emp_id)
ON EMPLOYEE TO DEV1;
```

What does DEV1 receive?

A. Permission to update emp_id
B. Permission to reference emp_id in a foreign key definition on another table
C. Permission to delete emp_id
D. Permission to create a primary key on EMPLOYEE

**Answer: B**

## Section C - Column-level GRANT privileges

**Q21.** Which statement correctly grants column-level SELECT privilege in HSQLDB?

A.

```sql
GRANT SELECT(emp_id, emp_name)
ON EMPLOYEE TO DEV1;
```

B.

```sql
GRANT SELECT ON EMPLOYEE(emp_id, emp_name)
TO DEV1;
```

C.

```sql
GRANT SELECT COLUMN emp_id, emp_name
TO DEV1;
```

D.

```sql
GRANT emp_id, emp_name SELECT
ON EMPLOYEE TO DEV1;
```

**Answer: A**

**Q22.** Consider:

```sql
GRANT SELECT(emp_id, emp_name)
ON EMPLOYEE TO DEV1;
```

Which query is permitted by this grant alone?

A.

```sql
SELECT emp_id, emp_name FROM EMPLOYEE;
```

B.

```sql
SELECT salary FROM EMPLOYEE;
```

C.

```sql
SELECT * FROM EMPLOYEE;
```

D.

```sql
SELECT emp_id, salary FROM EMPLOYEE;
```

**Answer: A**

**Q23.** Consider:

```sql
GRANT UPDATE(salary)
ON EMPLOYEE TO DEV1;
```

Which query is authorized by this column-level UPDATE grant alone, assuming DEV1 has the necessary SELECT permission on the search column?

A.

```sql
UPDATE EMPLOYEE
SET salary = 60000
WHERE emp_id = 10;
```

B.

```sql
UPDATE EMPLOYEE
SET emp_name = 'Raj'
WHERE emp_id = 10;
```

C.

```sql
UPDATE EMPLOYEE
SET salary = 60000,
    emp_name = 'Raj'
WHERE emp_id = 10;
```

D. Both A and C

**Answer: A**

**Q24.** Consider:

```sql
GRANT INSERT(emp_id, emp_name)
ON EMPLOYEE TO DEV1;
```

The table contains:

| Column | Definition |
| --- | --- |
| emp_id | NOT NULL |
| emp_name | NOT NULL |
| salary | DEFAULT 30000 |

Which statement is correct?

A. DEV1 can insert a row by providing emp_id and emp_name and omitting salary.
B. DEV1 can explicitly insert any salary value.
C. DEV1 can update salary.
D. DEV1 can delete records.

**Answer: A**

**Q25.** Consider:

```sql
GRANT INSERT(emp_id, emp_name)
ON EMPLOYEE TO DEV1;
```

Which INSERT is not authorized by this grant alone?

A.

```sql
INSERT INTO EMPLOYEE(emp_id, emp_name)
VALUES(1, 'Raj');
```

B.

```sql
INSERT INTO EMPLOYEE(emp_id, emp_name, salary)
VALUES(2, 'Sam', 50000);
```

C.

```sql
INSERT INTO EMPLOYEE(emp_id)
VALUES(3);
```

D. Both B and C

**Answer: D**

**Q26.** Consider:

```sql
GRANT UPDATE(salary)
ON EMPLOYEE TO DEV1;
```

DEV1 executes:

```sql
UPDATE EMPLOYEE
SET salary = 60000
WHERE emp_id = 10;
```

DEV1 has no SELECT privilege on emp_id. What is the correct result?

A. The query succeeds because UPDATE automatically includes SELECT.
B. The query fails because emp_id is read in the search condition and SELECT privilege is required.
C. The query succeeds only when emp_id is a primary key.
D. The query fails because salary is numeric.

**Answer: B**

**Q27.** Consider:

```sql
GRANT SELECT(salary)
ON EMPLOYEE TO DEV1;

GRANT UPDATE(salary)
ON EMPLOYEE TO DEV1;
```

Can DEV1 execute the following statement?

```sql
UPDATE EMPLOYEE
SET salary = salary + 5000
WHERE salary > 30000;
```

A. Yes, both reading and updating salary are authorized.
B. No, UPDATE privilege cannot be combined with SELECT privilege.
C. No, salary cannot be used in WHERE.
D. Yes, but only if DEV1 has DELETE privilege.

**Answer: A**

**Q28.** Consider:

```sql
GRANT UPDATE(salary, commission)
ON EMPLOYEE TO DEV1;
```

Which statement is correct?

A. DEV1 can update all columns.
B. DEV1 can update salary and commission through this grant.
C. DEV1 can update only salary.
D. DEV1 can delete both columns.

**Answer: B**

**Q29.** Which privilege is required for the following query, in addition to any necessary UPDATE privilege?

```sql
UPDATE EMPLOYEE
SET salary = 60000
WHERE dept_id = 10;
```

A. SELECT on dept_id
B. DELETE on dept_id
C. REFERENCES on dept_id
D. USAGE on dept_id

**Answer: A**

**Q30.** Consider:

```sql
GRANT SELECT(emp_id, salary)
ON EMPLOYEE TO DEV1;
```

Which statement is correct?

A. DEV1 can use emp_id and salary in SELECT statements but not emp_name.
B. DEV1 can select every column because SELECT is granted.
C. DEV1 can update emp_id and salary.
D. DEV1 can delete rows based on salary.

**Answer: A**

## Section D - REVOKE and column-level revocation

**Q31.** Which statement correctly revokes SELECT privilege in HSQLDB?

A.

```sql
REVOKE SELECT ON EMPLOYEE
FROM DEV1 CASCADE;
```

B.

```sql
REVOKE SELECT ON EMPLOYEE
TO DEV1;
```

C.

```sql
REMOVE SELECT ON EMPLOYEE
FROM DEV1;
```

D.

```sql
DELETE SELECT ON EMPLOYEE
FROM DEV1;
```

**Answer: A**

**Q32.** Consider:

```sql
GRANT SELECT, INSERT, UPDATE
ON EMPLOYEE TO DEV1;
```

Then:

```sql
REVOKE INSERT
ON EMPLOYEE FROM DEV1 CASCADE;
```

Which privileges remain?

A. INSERT only
B. SELECT and UPDATE
C. UPDATE only
D. No privileges

**Answer: B**

**Q33.** Consider:

```sql
GRANT SELECT ON EMPLOYEE TO DEV1;
GRANT UPDATE ON EMPLOYEE TO DEV1;

REVOKE SELECT ON EMPLOYEE FROM DEV1 CASCADE;
```

What can DEV1 do?

A. SELECT only
B. UPDATE only
C. SELECT and UPDATE
D. Neither SELECT nor UPDATE

**Answer: B**

**Q34.** Which statement correctly revokes multiple privileges?

A.

```sql
REVOKE SELECT, INSERT
ON EMPLOYEE FROM DEV1 CASCADE;
```

B.

```sql
REVOKE SELECT AND INSERT
ON EMPLOYEE FROM DEV1;
```

C.

```sql
REVOKE SELECT, INSERT
TO DEV1 ON EMPLOYEE;
```

D.

```sql
DELETE SELECT, INSERT
FROM EMPLOYEE;
```

**Answer: A**

**Q35.** Consider:

```sql
GRANT UPDATE(salary, commission)
ON EMPLOYEE TO DEV1;
```

Which statement revokes only the salary UPDATE privilege?

A.

```sql
REVOKE UPDATE(salary)
ON EMPLOYEE FROM DEV1 CASCADE;
```

B.

```sql
REVOKE salary
ON EMPLOYEE FROM DEV1 CASCADE;
```

C.

```sql
REVOKE UPDATE ON salary FROM DEV1;
```

D.

```sql
REVOKE UPDATE(commission)
ON EMPLOYEE FROM DEV1 CASCADE;
```

**Answer: A**

**Q36.** Consider:

```sql
GRANT SELECT(emp_id, salary, emp_name)
ON EMPLOYEE TO DEV1;
```

Then:

```sql
REVOKE SELECT(salary)
ON EMPLOYEE FROM DEV1 CASCADE;
```

Which column-level SELECT permissions remain from this grant?

A. salary only
B. emp_id and emp_name
C. All three columns
D. None

**Answer: B**

**Q37.** Consider:

```sql
GRANT SELECT ON EMPLOYEE TO DEV1;
GRANT SELECT ON EMPLOYEE TO DEV2;

REVOKE SELECT ON EMPLOYEE FROM DEV1 CASCADE;
```

What happens?

A. Both users lose SELECT.
B. Only DEV1 loses the independent grant.
C. DEV2 loses SELECT.
D. EMPLOYEE is deleted.

**Answer: B**

**Q38.** Which statement correctly revokes the grant option without necessarily revoking the underlying SELECT privilege?

A.

```sql
REVOKE GRANT OPTION FOR SELECT
ON EMPLOYEE FROM DEV1 CASCADE;
```

B.

```sql
REVOKE SELECT
ON EMPLOYEE FROM DEV1 CASCADE;
```

C.

```sql
REVOKE ADMIN OPTION FOR SELECT
ON EMPLOYEE FROM DEV1;
```

D.

```sql
DROP GRANT OPTION DEV1;
```

**Answer: A**

**Q39.** Consider:

```sql
GRANT SELECT ON EMPLOYEE TO DEV1;
GRANT UPDATE ON EMPLOYEE TO DEV1;

REVOKE ALL PRIVILEGES
ON EMPLOYEE FROM DEV1 CASCADE;
```

Which statement is correct?

A. Only SELECT is revoked.
B. Only UPDATE is revoked.
C. All privileges on EMPLOYEE held by DEV1 through the applicable grant are revoked.
D. The EMPLOYEE table is dropped.

**Answer: C**

**Q40.** Which statement about the following operation is correct?

```sql
REVOKE DELETE ON EMPLOYEE
FROM DEV1 RESTRICT;
```

A. It always deletes EMPLOYEE.
B. It requests revocation but can fail if dependent grants prevent the operation.
C. It automatically revokes DELETE from every database user.
D. It converts DELETE into SELECT.

**Answer: B**

## Section E - GRANT OPTION, RESTRICT and CASCADE

**Q41.** Consider:

```sql
GRANT SELECT ON EMPLOYEE
TO DEV1 WITH GRANT OPTION;
```

What additional permission does DEV1 receive?

A. Permission to grant the SELECT privilege to other users or roles.
B. Permission to grant DBA to any user.
C. Permission to drop EMPLOYEE.
D. Permission to grant every privilege on every table.

**Answer: A**

**Q42.** Consider:

```sql
GRANT SELECT ON EMPLOYEE
TO DEV1 WITH GRANT OPTION;
```

DEV1 executes:

```sql
GRANT SELECT ON EMPLOYEE TO DEV2;
```

Which statement is correct?

A. DEV2 receives SELECT privilege.
B. DEV2 automatically receives WITH GRANT OPTION.
C. DEV1 loses SELECT.
D. DEV2 becomes the owner of EMPLOYEE.

**Answer: A**

**Q43.** Consider the authorization chain:

```sql
-- DBA grants SELECT with grant option to A
GRANT SELECT ON EMPLOYEE
TO A WITH GRANT OPTION;

-- A grants SELECT to B
GRANT SELECT ON EMPLOYEE TO B;

-- B grants SELECT to C
GRANT SELECT ON EMPLOYEE TO C;
```

What happens when the original grant to A is revoked using CASCADE?

A. Only A loses SELECT.
B. A, B and C lose the dependent SELECT grants.
C. Only C loses SELECT.
D. Nobody loses SELECT.

**Answer: B**

**Q44.** Consider the same authorization chain as Q43. What is the purpose of RESTRICT when revoking A's original privilege?

A. Force revocation of all dependent grants.
B. Prevent the revocation if dependent grants would be affected.
C. Grant SELECT to C directly.
D. Delete all three users.

**Answer: B**

**Q45.** Consider:

```sql
GRANT SELECT ON EMPLOYEE
TO DEV1 WITH GRANT OPTION;

GRANT SELECT ON EMPLOYEE
TO DEV2;
```

Which statement is correct?

A. Both users receive GRANT OPTION.
B. Only DEV1 receives GRANT OPTION.
C. Only DEV2 receives GRANT OPTION.
D. Neither receives SELECT.

**Answer: B**

**Q46.** Which statement distinguishes WITH GRANT OPTION from WITH ADMIN OPTION?

A. Both are identical and apply to all objects.
B. GRANT OPTION permits forwarding object privileges; ADMIN OPTION permits forwarding role membership.
C. GRANT OPTION creates a user; ADMIN OPTION creates a table.
D. GRANT OPTION applies only to sequences.

**Answer: B**

**Q47.** Consider:

```sql
GRANT SELECT ON EMPLOYEE
TO DEV1 WITH GRANT OPTION;

REVOKE GRANT OPTION FOR SELECT
ON EMPLOYEE FROM DEV1 CASCADE;
```

Which statement best describes the intended effect?

A. Remove DEV1's ability to grant SELECT further, while retaining DEV1's own SELECT privilege where applicable.
B. Remove SELECT from every user in the database.
C. Remove the EMPLOYEE table.
D. Grant SELECT to DEV1 again.

**Answer: A**

**Q48.** Which statement correctly specifies the grantor in HSQLDB?

A.

```sql
GRANT SELECT ON EMPLOYEE
TO DEV1 GRANTED BY CURRENT_USER;
```

B.

```sql
GRANT SELECT ON EMPLOYEE
FROM CURRENT_USER TO DEV1;
```

C.

```sql
GRANT CURRENT_USER SELECT
ON EMPLOYEE TO DEV1;
```

D.

```sql
GRANT SELECT CURRENT_ROLE
ON EMPLOYEE TO DEV1;
```

**Answer: A**

## Section F - Roles and role-based authorization

**Q49.** Consider:

```sql
CREATE ROLE DEVELOPER;

GRANT SELECT, UPDATE
ON EMPLOYEE TO DEVELOPER;

GRANT DEVELOPER TO DEV1;
```

Which statement is correct?

A. DEV1 receives the privileges assigned to DEVELOPER through role membership.
B. DEV1 becomes the owner of EMPLOYEE.
C. DEVELOPER becomes a table.
D. DEV1 receives DBA automatically.

**Answer: A**

**Q50.** Which statement correctly creates a role in HSQLDB?

A.

```sql
CREATE ROLE DEVELOPER;
```

B.

```sql
CREATE USER DEVELOPER ROLE;
```

C.

```sql
GRANT ROLE DEVELOPER;
```

D.

```sql
CREATE PRIVILEGE DEVELOPER;
```

**Answer: A**

**Q51.** Consider:

```sql
CREATE ROLE R1;
CREATE ROLE R2;

GRANT SELECT ON EMPLOYEE TO R1;
GRANT R1 TO R2;
GRANT R2 TO DEV1;
```

Which privilege can DEV1 obtain through the nested role memberships?

A. SELECT on EMPLOYEE
B. DELETE on EMPLOYEE
C. DBA automatically
D. No privileges because a role cannot be granted to another role

**Answer: A**

**Q52.** Which statement correctly grants role membership with the ability to administer that membership?

A.

```sql
GRANT DEVELOPER TO DEV1 WITH ADMIN OPTION;
```

B.

```sql
GRANT DEVELOPER TO DEV1 WITH GRANT OPTION;
```

C.

```sql
GRANT ADMIN ON DEVELOPER TO DEV1;
```

D.

```sql
GRANT DEVELOPER WITH SELECT TO DEV1;
```

**Answer: A**

**Q53.** Consider:

```sql
CREATE ROLE DEVELOPER;

GRANT SELECT ON EMPLOYEE TO DEVELOPER;

GRANT DEVELOPER TO DEV1;
GRANT DEVELOPER TO DEV2;
```

Then:

```sql
REVOKE DEVELOPER FROM DEV1 CASCADE;
```

Which statement is correct?

A. DEV1 loses the membership, while DEV2 retains the independent membership.
B. Both DEV1 and DEV2 lose membership.
C. The DEVELOPER role is dropped.
D. EMPLOYEE is deleted.

**Answer: A**

**Q54.** Consider:

```sql
CREATE ROLE R1;
CREATE ROLE R2;

GRANT R1 TO R2 WITH ADMIN OPTION;
GRANT R2 TO DEV1;
```

Which statement is correct?

A. DEV1 automatically receives ADMIN OPTION on R1.
B. R2 receives ADMIN OPTION on R1; DEV1 does not automatically receive it through membership in R2.
C. R1 becomes a user.
D. DEV1 becomes DBA.

**Answer: B**

**Q55.** Which statement correctly revokes the administration option associated with a role membership without necessarily removing the membership itself?

A.

```sql
REVOKE ADMIN OPTION FOR DEVELOPER
FROM DEV1 CASCADE;
```

B.

```sql
REVOKE GRANT OPTION FOR DEVELOPER
FROM DEV1 CASCADE;
```

C.

```sql
REVOKE SELECT ON DEVELOPER
FROM DEV1 CASCADE;
```

D.

```sql
DROP ADMIN DEVELOPER;
```

**Answer: A**

## Section G - Sequences, routines, views and advanced HSQLDB privileges

**Q56.** Consider:

```sql
CREATE SEQUENCE EMP_SEQ;

GRANT USAGE ON SEQUENCE EMP_SEQ TO DEV1;
```

Which operation is authorized by the grant?

A. Using the sequence directly in an SQL statement, subject to the applicable sequence operation
B. Dropping EMP_SEQ
C. Altering every sequence in the database
D. Creating a stored procedure

**Answer: A**

**Q57.** Which statement correctly grants permission to execute a stored procedure in HSQLDB?

A.

```sql
GRANT EXECUTE ON ROUTINE CALCULATE_SALARY
TO DEV1;
```

B.

```sql
GRANT SELECT ON ROUTINE CALCULATE_SALARY
TO DEV1;
```

C.

```sql
GRANT UPDATE ON ROUTINE CALCULATE_SALARY
TO DEV1;
```

D.

```sql
GRANT USAGE ON ROUTINE CALCULATE_SALARY
TO DEV1;
```

**Answer: A**

**Q58.** Consider:

```sql
CREATE SEQUENCE EMP_SEQ;

GRANT USAGE ON SEQUENCE EMP_SEQ TO DEV1;

REVOKE USAGE ON SEQUENCE EMP_SEQ
FROM DEV1 CASCADE;
```

What is the result?

A. EMP_SEQ is dropped.
B. DEV1 loses the granted USAGE privilege on EMP_SEQ.
C. DEV1 receives EXECUTE privilege.
D. All sequences are deleted.

**Answer: B**

**Q59.** Consider:

```sql
GRANT EXECUTE ON ROUTINE CALCULATE_SALARY
TO DEVELOPER;

GRANT DEVELOPER TO DEV1;
```

Which statement is correct?

A. DEV1 can obtain the routine execution privilege through DEVELOPER membership.
B. DEV1 receives SELECT on every table.
C. DEV1 receives DBA automatically.
D. DEV1 can modify the routine definition automatically.

**Answer: A**

**Q60.** Consider:

```sql
CREATE ROLE AUDITOR;

GRANT SELECT(emp_id, emp_name)
ON EMPLOYEE TO AUDITOR;

GRANT USAGE ON SEQUENCE EMP_SEQ TO AUDITOR;

GRANT EXECUTE ON ROUTINE GET_EMPLOYEE
TO AUDITOR;

GRANT AUDITOR TO DEV1;
```

Which combination of permissions can DEV1 obtain through AUDITOR?

A. SELECT on emp_id and emp_name, USAGE on EMP_SEQ, and EXECUTE on GET_EMPLOYEE
B. SELECT on every EMPLOYEE column, DELETE on EMPLOYEE, and DBA
C. UPDATE on every EMPLOYEE column and DROP on EMP_SEQ
D. INSERT, UPDATE, DELETE and ALTER on every database object

**Answer: A**

---

## Important correction to Q43

For the three-level grant chain to work, B must also receive the grant option:

```sql
GRANT SELECT ON EMPLOYEE TO A WITH GRANT OPTION;

GRANT SELECT ON EMPLOYEE TO B WITH GRANT OPTION;

GRANT SELECT ON EMPLOYEE TO C;
```

Now revoking A's original grant with CASCADE can revoke the dependent grants to B and C.

---

## HSQLDB reference

The questions follow the HSQLDB 2.x Access Control documentation, including its column-level privileges, object-specific privileges, role administration and revocation rules.

- HSQLDB - Access Control
- HSQLDB - GRANT and object privileges
- HSQLDB - REVOKE syntax and CASCADE/RESTRICT

**Total: 60 expert-level questions with answers.**

### User

for 2 year sql developer hsql database level give concepts needed from required topics all tricky advanced topics from these explanation and 15 question quiz at end all edge cases what is the need fr transactin handlling ensure data remains consistent user can access data concurrently transacrion done between2 users update 1 account reduce and that account add 2 update statement how do we ensure 2 complete successfully or none completes, what is transaction what it does for dbms,  how is transaction perfroms in database, transaction syntax set transaction mode: read only or read write query commit/rollback after end of each unit add commit or rollback ensure atomic consistent successfull, autocommit : if set autocommit true after every transaction commit is automatically issued default state of database, autocommit false: commit or rollback has to be manually added after set transactions show autocommit diplay status of autocommit property transaction states explain begin aactive partially commited commited failed aborted, transaction acid properties brief, transaction processisn systsem barch transaction processing ssystem explain real time transaction processing, online transaction processing system explain explaineach seperately , batch series of task to be executed in sequential order no user intervention automation of repeated tasks, real time processing system: handling expected to unexpected outputs application require user input stream of input at each stafes and have deadline for completion, online transaction: users to interact and provide input at stages in online and provide appropriate commands, requirements fr oltp system data inegrity scaabiity concurrency problems associated with cncurrent execution : lost update dirty read phantom record incrrect summary concurrecny techniqu: locking timestamp ordering, serializability, validation based crisply explain these locking explain shared mode exclusive mode shared lock higher transaction concurrency exclusive lock low transaction concurrency, when table locked in shared mode and read other transaction can also read it , exclusive lock : if t1 puts lock on resource no other transaction can put s or x lock on any resources lock matrix  explain 2 phase locking protocool for shared lock and exclusive lock read commited isolation + 2 phase locking used in hsql ony questions give no theory what and all tricky mcqs can be asked from it make a quiz of 60 questions all tricky expert take time and think and give based on above concepts give only give question mcq and asnwer not quiz interface give based on thery and autocommit transaction rollback commit based questions also give how many rows added and all theory

### ChatGPT

# HSQLDB - Transaction Management & Concurrency Control

(Expert SQL Developer Level) (60 MCQs)

**Difficulty:** 2-year SQL Developer / Advanced DBMS

The questions cover transaction fundamentals, transaction processing systems, ACID, transaction states, autocommit, COMMIT, ROLLBACK, concurrent transactions, lost updates, dirty reads, phantom reads, locking, shared/exclusive locks, lock compatibility, two-phase locking, isolation levels, serializability, timestamp ordering and validation-based concurrency control.

**Assumptions:** HSQLDB 2.x, standard SQL transaction syntax, and the default HSQLDB transaction isolation behavior unless a question specifies otherwise. Each transaction example starts from the stated initial data.

---

## Section A - Transaction fundamentals and transaction processing

**Q1.** Two bank accounts have balances of ₹10,000 and ₹5,000. A transfer of ₹2,000 is performed:

```sql
UPDATE ACCOUNT
SET balance = balance - 2000
WHERE account_id = 1;

UPDATE ACCOUNT
SET balance = balance + 2000
WHERE account_id = 2;
```

What is the primary purpose of using a transaction for these two statements?

A. To execute both statements simultaneously
B. To ensure both updates succeed together or neither update takes effect
C. To prevent SELECT queries from executing
D. To permanently disable concurrent transactions

**Answer: B**

**Q2.** Which statement best defines a database transaction?

A. A single SELECT statement only
B. A logical unit of database work consisting of one or more operations
C. A database backup operation
D. A database schema definition

**Answer: B**

**Q3.** Which of the following is a valid transaction-ending statement?

A. COMMIT
B. ROLLBACK
C. Both A and B
D. CREATE

**Answer: C**

**Q4.** Consider:

```sql
START TRANSACTION;

UPDATE EMPLOYEE
SET salary = 50000
WHERE emp_id = 101;

COMMIT;
```

What does COMMIT do?

A. Permanently saves the transaction's changes
B. Reverses all changes
C. Deletes the transaction log
D. Starts another transaction automatically in every DBMS

**Answer: A**

**Q5.** Which statement is correct about ROLLBACK?

A. It permanently saves modifications.
B. It undoes uncommitted changes in the current transaction.
C. It deletes the table structure.
D. It commits all previous transactions.

**Answer: B**

**Q6.** A transaction contains:

```sql
UPDATE ACCOUNT
SET balance = balance - 1000
WHERE account_id = 1;

UPDATE ACCOUNT
SET balance = balance + 1000
WHERE account_id = 2;
```

The first UPDATE succeeds, but the second UPDATE fails. What should happen to preserve atomicity?

A. Commit the first update.
B. Roll back the transaction.
C. Ignore the second update.
D. Execute another SELECT.

**Answer: B**

**Q7.** Which statement is the correct HSQLDB-style transaction configuration syntax?

A.

```sql
SET TRANSACTION READ ONLY;
```

B.

```sql
SET TRANSACTION MODE ONLY READ;
```

C.

```sql
TRANSACTION SET READ ONLY;
```

D.

```sql
SET DATABASE READ ONLY TRANSACTION;
```

**Answer: A**

**Q8.** Which statement is correct about transaction access modes?

A. READ ONLY transactions can freely modify table data.
B. READ WRITE transactions permit data modifications, subject to privileges and constraints.
C. READ ONLY and READ WRITE are identical.
D. READ WRITE disables concurrency.

**Answer: B**

**Q9.** Which statement about a READ ONLY transaction is correct?

A. It allows SELECT operations but prohibits data modifications.
B. It allows INSERT but prohibits DELETE.
C. It allows UPDATE but prohibits INSERT.
D. It allows all operations.

**Answer: A**

**Q10.** Consider:

```sql
SET TRANSACTION READ ONLY;

SELECT * FROM EMPLOYEE;

COMMIT;
```

Which statement is correct?

A. The SELECT is permitted, and COMMIT ends the transaction.
B. The SELECT is prohibited.
C. COMMIT changes the transaction to READ WRITE.
D. The transaction cannot be ended.

**Answer: A**

## Section B - Autocommit, COMMIT and ROLLBACK

**Q11.** What is the default JDBC autocommit mode for a newly established HSQLDB connection?

A. TRUE
B. FALSE
C. NULL
D. Depends on the number of tables

**Answer: A**

**Q12.** Consider:

```sql
SET AUTOCOMMIT TRUE;

INSERT INTO EMPLOYEE VALUES (101, 'Raj', 30000);
INSERT INTO EMPLOYEE VALUES (102, 'Sam', 40000);
```

What happens?

A. Both INSERT statements remain uncommitted.
B. Each successful statement is committed automatically.
C. Only the second statement is committed.
D. Both statements are rolled back automatically.

**Answer: B**

**Q13.** Consider:

```sql
SET AUTOCOMMIT FALSE;

INSERT INTO EMPLOYEE VALUES (101, 'Raj', 30000);
INSERT INTO EMPLOYEE VALUES (102, 'Sam', 40000);

ROLLBACK;
```

Initially, EMPLOYEE contains 10 rows. How many rows remain?

A. 12
B. 11
C. 10
D. 0

**Answer: C**

**Q14.** Consider:

```sql
SET AUTOCOMMIT FALSE;

INSERT INTO EMPLOYEE VALUES (101, 'Raj', 30000);
INSERT INTO EMPLOYEE VALUES (102, 'Sam', 40000);

COMMIT;
```

Initially, the table contains 10 rows. How many rows are present after COMMIT?

A. 10
B. 11
C. 12
D. 0

**Answer: C**

**Q15.** Consider:

```sql
SET AUTOCOMMIT FALSE;

INSERT INTO EMPLOYEE VALUES (101, 'Raj', 30000);

COMMIT;

INSERT INTO EMPLOYEE VALUES (102, 'Sam', 40000);

ROLLBACK;
```

Initially, the table contains 10 rows. How many rows remain?

A. 10
B. 11
C. 12
D. 9

**Answer: B**

**Q16.** Consider:

```sql
SET AUTOCOMMIT TRUE;

INSERT INTO EMPLOYEE VALUES (101, 'Raj', 30000);

ROLLBACK;
```

Which statement is correct?

A. The inserted row is guaranteed to be removed.
B. The successful INSERT was already committed, so the later ROLLBACK cannot undo it.
C. The table is dropped.
D. The INSERT remains pending.

**Answer: B**

**Q17.** Consider:

```sql
SET AUTOCOMMIT FALSE;

UPDATE EMPLOYEE
SET salary = 50000
WHERE emp_id = 101;

SELECT * FROM EMPLOYEE;

ROLLBACK;
```

What happens to the UPDATE?

A. It is committed because SELECT follows it.
B. It is rolled back.
C. SELECT automatically commits it.
D. It is permanently saved when the result is displayed.

**Answer: B**

**Q18.** Which statement correctly describes autocommit FALSE?

A. Every statement is committed automatically.
B. The transaction's changes remain pending until COMMIT or ROLLBACK.
C. SELECT statements are prohibited.
D. Every INSERT is automatically rolled back.

**Answer: B**

**Q19.** A connection has autocommit FALSE. The following operations are performed:

```sql
INSERT INTO EMPLOYEE VALUES (101, 'Raj', 30000);
UPDATE EMPLOYEE SET salary = 40000 WHERE emp_id = 101;
COMMIT;
DELETE FROM EMPLOYEE WHERE emp_id = 101;
```

What is the final result of the DELETE if no further COMMIT is issued and the connection remains open?

A. The row is permanently deleted.
B. The row is deleted within the current uncommitted transaction.
C. The row cannot be deleted because it was inserted earlier.
D. The entire transaction is automatically rolled back.

**Answer: B**

**Q20.** Which statement is correct about displaying autocommit status?

A. `SELECT AUTOCOMMIT FROM EMPLOYEE;`
B. JDBC `Connection.getAutoCommit()` reports the connection's autocommit setting.
C. `SHOW TABLE AUTOCOMMIT;`
D. `DISPLAY TRANSACTION STATUS;`

**Answer: B**

## Section C - Transaction states and ACID properties

**Q21.** A transaction has started and is currently executing its SQL statements. Which state does it occupy?

A. Active
B. Committed
C. Aborted
D. Terminated

**Answer: A**

**Q22.** A transaction has executed its last statement but has not yet completed its commit operation. Which state is it in?

A. Failed
B. Partially committed
C. Aborted
D. Active

**Answer: B**

**Q23.** A transaction has successfully completed COMMIT. Which state does it enter?

A. Active
B. Failed
C. Committed
D. Partially committed

**Answer: C**

**Q24.** A transaction encounters an error and cannot continue executing. Which state does it enter?

A. Committed
B. Failed
C. Partially committed
D. Active

**Answer: B**

**Q25.** A failed transaction has had all its changes undone through rollback. Which state does it enter?

A. Active
B. Committed
C. Aborted
D. Partially committed

**Answer: C**

**Q26.** Which ACID property ensures that all operations within a transaction succeed together or fail together?

A. Consistency
B. Isolation
C. Atomicity
D. Durability

**Answer: C**

**Q27.** An account transfer deducts ₹2,000 from one account and adds ₹2,000 to another. Which ACID property ensures that the total account balance remains consistent with the business rules?

A. Atomicity
B. Consistency
C. Isolation
D. Durability

**Answer: B**

**Q28.** Transaction T1 is updating an employee's salary. Transaction T2 should not observe an invalid intermediate state of T1. Which ACID property addresses this?

A. Durability
B. Consistency
C. Isolation
D. Atomicity

**Answer: C**

**Q29.** A transaction commits successfully. Immediately afterwards, the database server crashes. Which ACID property ensures that committed changes survive recovery?

A. Atomicity
B. Isolation
C. Consistency
D. Durability

**Answer: D**

**Q30.** Which of the following correctly matches ACID properties?

A. Atomicity - all or nothing; Consistency - valid database state; Isolation - concurrent transaction separation; Durability - committed changes persist.
B. Atomicity - concurrent access; Consistency - rollback; Isolation - permanent storage; Durability - data validation.
C. Atomicity - permanent storage; Consistency - locking; Isolation - data validation; Durability - rollback.
D. All four properties mean the same thing.

**Answer: A**

## Section D - Transaction processing systems

**Q31.** A company processes 10,000 employee salary records every night without requiring individual user interaction. Which processing system is most appropriate?

A. Real-time transaction processing
B. Batch processing
C. Interactive OLTP
D. Manual processing

**Answer: B**

**Q32.** Which characteristic best describes batch processing?

A. Every task requires immediate user input.
B. A collection of tasks is executed sequentially or as a scheduled batch with minimal user intervention.
C. Every transaction must complete within milliseconds.
D. Data cannot be stored permanently.

**Answer: B**

**Q33.** A railway signalling application receives continuous input and must respond within strict deadlines. Which processing system is most appropriate?

A. Batch processing
B. Real-time processing
C. Offline reporting
D. Manual transaction processing

**Answer: B**

**Q34.** A customer uses an online banking application to enter an amount, select an account and confirm a transfer. Which system best describes this interaction?

A. Batch processing
B. Online Transaction Processing (OLTP)
C. Offline processing
D. Sequential file processing

**Answer: B**

**Q35.** Which statement best distinguishes real-time processing from OLTP?

A. Both are exactly the same.
B. Real-time processing emphasizes meeting response deadlines; OLTP emphasizes interactive processing of individual business transactions.
C. OLTP never involves user input.
D. Real-time processing never handles concurrent requests.

**Answer: B**

**Q36.** Which of the following is a key OLTP requirement?

A. High concurrency and transaction integrity
B. Only nightly processing
C. No transaction isolation
D. No data validation

**Answer: A**

**Q37.** An e-commerce website receives 5,000 simultaneous purchase requests. Which requirement is particularly important?

A. Concurrency control
B. Disabling transactions
C. Removing constraints
D. Avoiding all indexes

**Answer: A**

**Q38.** Which combination is most important for an OLTP database?

A. Data integrity, concurrency, scalability and transaction reliability
B. Only large sequential file processing
C. Only data visualization
D. Only offline storage

**Answer: A**

## Section E - Concurrency problems and isolation

**Q39.** Consider two transactions:

Initial balance = 10,000.

- T1 reads balance = 10,000.
- T2 reads balance = 10,000.
- T1 adds 1,000 and writes 11,000.
- T2 subtracts 2,000 and writes 8,000.

What concurrency problem occurs?

A. Dirty read
B. Lost update
C. Phantom read
D. Incorrect summary

**Answer: B - Lost update**

**Q40.** Transaction T1 executes:

```sql
UPDATE ACCOUNT
SET balance = 5000
WHERE account_id = 1;
```

T1 has not committed. T2 reads the updated balance of 5,000. T1 subsequently rolls back.

Which concurrency problem occurred?

A. Phantom read
B. Lost update
C. Dirty read
D. Incorrect summary

**Answer: C - Dirty read**

**Q41.** Transaction T1 executes:

```sql
SELECT COUNT(*)
FROM EMPLOYEE
WHERE salary > 50000;
```

T2 inserts a new employee with salary 60,000 and commits. T1 executes the same query again and gets a different count.

Which problem is demonstrated under an isolation level permitting this behavior?

A. Lost update
B. Dirty read
C. Phantom read
D. Deadlock

**Answer: C - Phantom read**

**Q42.** T1 calculates the total salary of all employees. While T1 is calculating, T2 modifies several employee salaries. T1 reads some old values and some new values, producing an incorrect total.

Which concurrency problem is this?

A. Incorrect summary
B. Dirty read only
C. Lost update
D. Phantom read only

**Answer: A - Incorrect summary**

**Q43.** Which concurrency problem occurs when one transaction overwrites another transaction's committed update without incorporating that update?

A. Dirty read
B. Lost update
C. Phantom read
D. Incorrect summary

**Answer: B**

**Q44.** Which isolation level permits dirty reads in the standard SQL isolation-level model?

A. READ UNCOMMITTED
B. READ COMMITTED
C. REPEATABLE READ
D. SERIALIZABLE

**Answer: A**

**Q45.** Under READ COMMITTED isolation, which statement is correct?

A. A transaction can read another transaction's uncommitted changes.
B. A transaction cannot read uncommitted changes, but repeated reads may return different committed values.
C. Phantom reads are always prevented.
D. All transactions execute sequentially.

**Answer: B**

**Q46.** Which isolation level provides the strongest standard SQL isolation guarantee?

A. READ UNCOMMITTED
B. READ COMMITTED
C. REPEATABLE READ
D. SERIALIZABLE

**Answer: D**

## Section F - Locking and lock compatibility

**Q47.** Transaction T1 acquires a Shared (S) lock on a resource. Which additional lock can transaction T2 acquire on the same resource?

A. Shared lock
B. Exclusive lock
C. Both S and X simultaneously
D. Neither lock

**Answer: A**

**Q48.** Transaction T1 holds an Exclusive (X) lock on a resource. What happens when T2 requests a Shared lock on that same resource?

A. T2 receives the lock immediately.
B. T2 must wait until the conflicting exclusive lock is released.
C. T2 automatically converts the X lock into an S lock.
D. Both transactions receive X locks.

**Answer: B**

**Q49.** Which lock compatibility matrix is correct?

A.

| Existing lock | Requested S | Requested X |
| --- | --- | --- |
| S | Compatible | Not compatible |
| X | Not compatible | Not compatible |

B.

| Existing lock | Requested S | Requested X |
| --- | --- | --- |
| S | Not compatible | Compatible |
| X | Compatible | Compatible |

C.

| Existing lock | Requested S | Requested X |
| --- | --- | --- |
| S | Compatible | Compatible |
| X | Compatible | Compatible |

D.

| Existing lock | Requested S | Requested X |
| --- | --- | --- |
| S | Not compatible | Not compatible |
| X | Compatible | Compatible |

**Answer: A**

**Q50.** Which statement about Shared locks is correct?

A. Multiple transactions can hold Shared locks on the same resource simultaneously.
B. Only one transaction can hold a Shared lock.
C. Shared locks allow other transactions to modify the resource simultaneously.
D. Shared locks automatically commit transactions.

**Answer: A**

**Q51.** Which statement about Exclusive locks is correct?

A. Multiple transactions can hold Exclusive locks on the same resource.
B. An Exclusive lock prevents other transactions from acquiring conflicting Shared or Exclusive locks on that resource.
C. Exclusive locks permit unrestricted simultaneous updates.
D. Exclusive locks are used only for SELECT operations.

**Answer: B**

**Q52.** Transaction T1 holds an S lock on row A. T2 also holds an S lock on row A. T1 now requests an X lock on row A.

What happens?

A. T1 immediately gets the X lock.
B. T1 must wait until the conflicting S lock held by T2 is released.
C. T2 is automatically terminated.
D. Both S locks become X locks.

**Answer: B**

## Section G - Two-phase locking and concurrency techniques

**Q53.** Which statement correctly describes the Two-Phase Locking (2PL) protocol?

A. A growing phase acquires locks, followed by a shrinking phase that releases locks; new locks cannot be acquired after the first lock is released.
B. Locks are acquired and released in any order.
C. All locks must be released before the transaction begins.
D. Only Shared locks are allowed.

**Answer: A**

**Q54.** Under 2PL, a transaction has already released one lock. It now requests a new Exclusive lock on another resource.

What happens?

A. It is permitted under basic 2PL.
B. It violates the two-phase locking protocol.
C. It automatically commits.
D. It automatically rolls back.

**Answer: B**

**Q55.** Which statement correctly describes Strict 2PL?

A. All locks, including write locks, are released immediately after each statement.
B. Exclusive locks are held until COMMIT or ROLLBACK.
C. No locks are acquired.
D. Shared locks are prohibited.

**Answer: B**

**Q56.** Which concurrency control technique orders transactions using timestamps assigned to them?

A. Lock-based protocol
B. Timestamp ordering protocol
C. Validation-based protocol
D. Batch processing

**Answer: B**

**Q57.** Which statement correctly describes validation-based concurrency control?

A. Transactions execute without acquiring locks initially and are validated before committing.
B. Transactions must acquire an Exclusive lock on every table before starting.
C. Every transaction commits immediately.
D. Transactions are always executed sequentially.

**Answer: A**

**Q58.** What does serializability ensure?

A. Every transaction executes in exactly one SQL statement.
B. A concurrent execution produces an outcome equivalent to some serial execution of those transactions.
C. Transactions cannot execute concurrently.
D. All transactions must use READ ONLY mode.

**Answer: B**

**Q59.** Consider two transactions:

- T1 locks resource A and waits for resource B.
- T2 locks resource B and waits for resource A.

What is the problem?

A. Dirty read
B. Deadlock
C. Phantom read
D. Incorrect summary

**Answer: B**

**Q60.** Consider HSQLDB transaction configuration:

```sql
SET TRANSACTION ISOLATION LEVEL READ COMMITTED;
```

Which statement best describes READ COMMITTED?

A. Uncommitted changes from other transactions can be read.
B. Each statement reads committed data; repeated statements may observe different committed results.
C. All phantom reads are prevented.
D. All transactions become serializable.

**Answer: B**

---

## Final answer key

| Q | Ans | Q | Ans | Q | Ans |
| --- | --- | --- | --- | --- | --- |
| 1 | B | 21 | A | 41 | C |
| 2 | B | 22 | B | 42 | A |
| 3 | C | 23 | C | 43 | B |
| 4 | A | 24 | B | 44 | A |
| 5 | B | 25 | C | 45 | B |
| 6 | B | 26 | C | 46 | D |
| 7 | A | 27 | B | 47 | A |
| 8 | B | 28 | C | 48 | B |
| 9 | A | 29 | D | 49 | A |
| 10 | A | 30 | A | 50 | A |
| 11 | A | 31 | B | 51 | B |
| 12 | B | 32 | B | 52 | B |
| 13 | C | 33 | B | 53 | A |
| 14 | C | 34 | B | 54 | B |
| 15 | B | 35 | B | 55 | B |
| 16 | B | 36 | A | 56 | B |
| 17 | B | 37 | A | 57 | A |
| 18 | B | 38 | A | 58 | B |
| 19 | B | 39 | B | 59 | B |
| 20 | B | 40 | C | 60 | B |

## Important expert-level distinctions

| Concept | Key distinction |
| --- | --- |
| COMMIT | Saves current transaction changes |
| ROLLBACK | Undoes uncommitted transaction changes |
| Autocommit TRUE | Successful statements are committed automatically |
| Autocommit FALSE | Explicit transaction completion is required |
| Atomicity | All or nothing |
| Consistency | Preserves database rules |
| Isolation | Controls concurrent transaction interference |
| Durability | Committed data survives failures |
| Dirty read | Reads uncommitted changes |
| Lost update | One update overwrites another |
| Phantom read | Re-execution returns additional or missing qualifying rows |
| Incorrect summary | Aggregate calculation is affected by concurrent modifications |
| Shared lock | Compatible with another Shared lock |
| Exclusive lock | Incompatible with Shared and Exclusive locks |
| 2PL | Growing phase followed by shrinking phase |
| Serializability | Equivalent to a serial transaction execution |
| Timestamp ordering | Orders operations according to transaction timestamps |
| Validation | Checks transaction conflicts before commit |

**HSQLDB-specific exam caution:** JDBC connections default to autocommit enabled, while the default isolation level in HSQLDB is READ COMMITTED. Do not confuse JDBC `setAutoCommit(false)` with SQL transaction access-mode configuration. Also, HSQLDB's transaction-control implementation and lock behavior depend on its transaction-control configuration; do not assume every implementation detail of textbook 2PL applies identically to every HSQLDB configuration.

### User

for 2 year sql developer hsql database level give concepts needed from required topics all tricky advanced topics from these explanation and 15 question quiz at end all edge cases what is the need fr transactin handlling ensure data remains consistent user can access data concurrently transacrion done between2 users update 1 account reduce and that account add 2 update statement how do we ensure 2 complete successfully or none completes, what is transaction what it does for dbms,  how is transaction perfroms in database, transaction syntax set transaction mode: read only or read write query commit/rollback after end of each unit add commit or rollback ensure atomic consistent successfull, autocommit : if set autocommit true after every transaction commit is automatically issued default state of database, autocommit false: commit or rollback has to be manually added after set transactions show autocommit diplay status of autocommit property transaction states explain begin aactive partially commited commited failed aborted, transaction acid properties brief, transaction processisn systsem barch transaction processing ssystem explain real time transaction processing, online transaction processing system explain explaineach seperately , batch series of task to be executed in sequential order no user intervention automation of repeated tasks, real time processing system: handling expected to unexpected outputs application require user input stream of input at each stafes and have deadline for completion, online transaction: users to interact and provide input at stages in online and provide appropriate commands, requirements fr oltp system data inegrity scaabiity concurrency problems associated with cncurrent execution : lost update dirty read phantom record incrrect summary concurrecny techniqu: locking timestamp ordering, serializability, validation based crisply explain these locking explain shared mode exclusive mode shared lock higher transaction concurrency exclusive lock low transaction concurrency, when table locked in shared mode and read other transaction can also read it , exclusive lock : if t1 puts lock on resource no other transaction can put s or x lock on any resources lock matrix  explain 2 phase locking protocool for shared lock and exclusive lock read commited isolation + 2 phase locking used in hsql ony questions give no theory what and all tricky mcqs can be asked from it make a quiz of 60 questions all tricky expert take time and think and give based on above concepts give only give question mcq and asnwer not quiz interface give based on thery and autocommit transaction rollback commit based questions also give how many rows added and all theory give different variety than above

### ChatGPT

# HSQLDB Transaction Management - Expert MCQ Set 2

(Expert / 2-year SQL Developer) (60 questions)

This is a fresh question set with different scenarios from the previous one. It emphasizes transaction execution traces, row counts, multiple connections, autocommit changes, failure handling, isolation anomalies, lock compatibility, 2PL and transaction scheduling.

**Assumptions for SQL questions:**

- HSQLDB 2.x, JDBC autocommit defaults to `TRUE`.
- Where autocommit is disabled, all statements belong to the current transaction until COMMIT or ROLLBACK.
- Unless specified, statements execute successfully.
- Each question specifies its initial data where needed.
- Standard SQL transaction and concurrency concepts are used.

## Section A - Transaction execution and atomicity

**Q1.** A bank transfer involves two accounts. Initial balances are:

| Account | Balance |
| --- | --- |
| A | 8000 |
| B | 4000 |

Transaction:

```sql
START TRANSACTION;

UPDATE ACCOUNT
SET balance = balance - 3000
WHERE account_id = 'A';

UPDATE ACCOUNT
SET balance = balance + 3000
WHERE account_id = 'B';

COMMIT;
```

What are the final balances?

A. A = 8000, B = 4000
B. A = 5000, B = 7000
C. A = 5000, B = 4000
D. A = 8000, B = 7000

**Answer: B**

**Q2.** Initial table:

| emp_id | salary |
| --- | --- |
| 1 | 30000 |
| 2 | 40000 |
| 3 | 50000 |

Execute:

```sql
SET AUTOCOMMIT FALSE;

UPDATE EMPLOYEE
SET salary = salary + 5000;

DELETE FROM EMPLOYEE
WHERE emp_id = 2;

ROLLBACK;
```

How many rows remain, and what is the salary of employee 1?

A. 2 rows, 35000
B. 3 rows, 30000
C. 3 rows, 35000
D. 2 rows, 30000

**Answer: B**

**Q3.** Initial table contains 20 rows.

```sql
SET AUTOCOMMIT FALSE;

INSERT INTO EMPLOYEE VALUES (101, 'A', 30000);
INSERT INTO EMPLOYEE VALUES (102, 'B', 40000);

COMMIT;

INSERT INTO EMPLOYEE VALUES (103, 'C', 50000);
INSERT INTO EMPLOYEE VALUES (104, 'D', 60000);

ROLLBACK;
```

How many rows remain?

A. 20
B. 21
C. 22
D. 24

**Answer: C**

**Q4.** Initial table contains 5 rows.

```sql
SET AUTOCOMMIT FALSE;

INSERT INTO EMPLOYEE VALUES (1, 'A', 10000);

SAVEPOINT S1;

INSERT INTO EMPLOYEE VALUES (2, 'B', 20000);

ROLLBACK TO SAVEPOINT S1;

COMMIT;
```

How many rows are present after COMMIT?

A. 5
B. 6
C. 7
D. 4

**Answer: B**

**Q5.** Initial table contains 10 rows. Autocommit is FALSE.

```sql
INSERT INTO EMPLOYEE VALUES (1, 'A', 10000);
COMMIT;

INSERT INTO EMPLOYEE VALUES (2, 'B', 20000);
SAVEPOINT S1;

DELETE FROM EMPLOYEE;

ROLLBACK TO SAVEPOINT S1;

COMMIT;
```

How many rows remain?

A. 0
B. 1
C. 11
D. 10

**Answer: C**

**Q6.** Initial table contains 10 rows. Autocommit is TRUE.

```sql
INSERT INTO EMPLOYEE VALUES (1, 'A', 10000);

UPDATE EMPLOYEE
SET salary = 20000
WHERE emp_id = 1;

DELETE FROM EMPLOYEE
WHERE emp_id = 1;
```

How many rows remain?

A. 10
B. 11
C. 9
D. 0

**Answer: A**

**Q7.** Initial table contains 10 rows. Autocommit is FALSE.

```sql
INSERT INTO EMPLOYEE VALUES (1, 'A', 10000);
COMMIT;

INSERT INTO EMPLOYEE VALUES (2, 'B', 20000);

DELETE FROM EMPLOYEE
WHERE emp_id = 1;

ROLLBACK;
```

How many rows remain?

A. 10
B. 11
C. 9
D. 12

**Answer: B**

**Q8.** Initial table contains 10 rows. Autocommit is FALSE.

```sql
INSERT INTO EMPLOYEE VALUES (1, 'A', 10000);
COMMIT;

INSERT INTO EMPLOYEE VALUES (2, 'B', 20000);
COMMIT;

DELETE FROM EMPLOYEE;
ROLLBACK;
```

How many rows remain?

A. 0
B. 10
C. 11
D. 12

**Answer: C**

**Q9.** A transaction executes three INSERT statements under autocommit FALSE. The first two succeed. The third violates a PRIMARY KEY constraint. Which statement is correct?

A. The first two INSERT statements are necessarily committed.
B. The third failure automatically guarantees that the entire transaction is rolled back in every DBMS.
C. The first two changes may remain pending; the transaction must be handled through appropriate rollback or recovery logic.
D. All three rows are inserted.

**Answer: C**

**Q10.** A transaction performs:

```sql
SET AUTOCOMMIT FALSE;

INSERT INTO EMPLOYEE VALUES (1, 'A', 10000);
COMMIT;

INSERT INTO EMPLOYEE VALUES (2, 'B', 20000);
ROLLBACK;
```

Which statement is correct?

A. Both inserted rows are removed.
B. Only the second inserted row is removed.
C. Only the first inserted row is removed.
D. Neither row is removed.

**Answer: B**

## Section B - Autocommit edge cases and transaction configuration

**Q11.** A JDBC connection starts with autocommit TRUE. The application executes:

```java
connection.setAutoCommit(false);
```

What happens to subsequent successful SQL statements?

A. Each statement is committed automatically.
B. They remain part of a transaction until explicitly committed or rolled back.
C. SELECT statements become invalid.
D. The database becomes read-only.

**Answer: B**

**Q12.** Autocommit is FALSE. A transaction inserts 3 rows. The application executes:

```java
connection.setAutoCommit(true);
```

What happens to the pending transaction?

A. Pending changes are automatically rolled back.
B. Pending changes are committed when switching autocommit from FALSE to TRUE through JDBC.
C. The connection is terminated.
D. The database becomes read-only.

**Answer: B**

**Q13.** Which JDBC method returns the current autocommit setting?

A. `getTransaction()`
B. `getAutoCommit()`
C. `isTransactionActive()`
D. `getCommitStatus()`

**Answer: B**

**Q14.** Consider:

```sql
SET TRANSACTION READ ONLY;
```

Which statement is correct?

A. It changes the database permanently to read-only mode.
B. It specifies the access mode of the current transaction.
C. It disables autocommit permanently.
D. It prevents every other user from accessing the database.

**Answer: B**

**Q15.** A transaction is configured as READ WRITE. Which operation is permitted, assuming appropriate privileges?

A. UPDATE
B. INSERT
C. DELETE
D. All of the above

**Answer: D**

**Q16.** Consider a transaction:

```sql
SET TRANSACTION READ ONLY;

SELECT * FROM EMPLOYEE;

UPDATE EMPLOYEE
SET salary = 50000
WHERE emp_id = 10;
```

What should happen?

A. Both statements succeed.
B. SELECT succeeds, but UPDATE violates the transaction's read-only access mode.
C. UPDATE succeeds because READ ONLY applies only to SELECT.
D. The table is automatically locked exclusively.

**Answer: B**

**Q17.** Which statement about COMMIT is correct?

A. COMMIT reverses the last SQL statement.
B. COMMIT makes the current transaction's changes permanent and ends that transaction.
C. COMMIT only applies to INSERT.
D. COMMIT changes autocommit to TRUE.

**Answer: B**

**Q18.** Consider:

```sql
SET AUTOCOMMIT FALSE;

INSERT INTO EMPLOYEE VALUES (1, 'A', 10000);
COMMIT;

INSERT INTO EMPLOYEE VALUES (2, 'B', 20000);
ROLLBACK;
```

What happens if the database connection is closed after ROLLBACK?

A. Both rows remain.
B. Only the first row remains.
C. Only the second row remains.
D. Neither row remains.

**Answer: B**

## Section C - Transaction states, ACID and processing systems

**Q19.** A transaction executes its final SQL statement successfully, but the commit record has not yet been successfully written. Which transaction state best describes this situation in the textbook transaction-state model?

A. Active
B. Partially committed
C. Aborted
D. Committed

**Answer: B**

**Q20.** A transaction has been rolled back completely after a failure. Which state does it enter?

A. Failed
B. Active
C. Aborted
D. Partially committed

**Answer: C**

**Q21.** A database server crashes after a transaction commits. During recovery, the transaction's committed changes are restored. Which ACID property is demonstrated?

A. Isolation
B. Consistency
C. Atomicity
D. Durability

**Answer: D**

**Q22.** Two transactions simultaneously attempt to book the last available seat on a flight. The database must prevent both transactions from successfully booking the same seat.

Which requirement is most relevant?

A. Data consistency and concurrency control
B. Batch processing
C. File compression
D. Database normalization alone

**Answer: A**

**Q23.** A company processes 50 lakh payroll records at midnight. The records are collected throughout the day and processed together without individual user interaction.

Which characteristic makes this batch processing?

A. Immediate response to every user action
B. Scheduled execution of accumulated tasks
C. Strict millisecond response deadlines
D. Interactive input at every processing stage

**Answer: B**

**Q24.** An industrial robot receives sensor readings continuously and must stop immediately when a dangerous condition is detected.

Which processing model is most appropriate?

A. Batch processing
B. Real-time processing
C. Offline analytical processing
D. Manual processing

**Answer: B**

**Q25.** A banking application allows customers to enter an amount, select a beneficiary, authenticate and confirm a payment.

Which processing model is most appropriate?

A. Batch processing
B. OLTP
C. Offline processing
D. Sequential processing

**Answer: B**

**Q26.** Which requirement is especially important when designing a high-volume OLTP application?

A. Supporting many concurrent users without compromising transaction correctness
B. Allowing dirty reads to increase speed
C. Disabling constraints
D. Performing all transactions only at midnight

**Answer: A**

**Q27.** Which scenario best represents real-time processing rather than ordinary OLTP?

A. Generating monthly bank statements
B. An online customer transferring money through a banking portal
C. Automatically shutting down industrial machinery when a dangerous temperature threshold is crossed
D. Generating a weekly payroll report

**Answer: C**

**Q28.** A transaction transfers ₹5,000 between two accounts. The total balance before and after the transfer must remain unchanged.

Which ACID property primarily protects this business rule?

A. Atomicity
B. Consistency
C. Isolation
D. Durability

**Answer: B**

## Section D - Concurrency anomalies and transaction schedules

**Q29.** Initial stock quantity is 100.

- T1 reads quantity = 100.
- T2 reads quantity = 100.
- T1 sells 20 units and writes 80.
- T2 sells 30 units and writes 70.

What is the final incorrect result?

A. 50
B. 70
C. 80
D. 100

**Answer: B**

**Q30.** In Q29, what should the correct final quantity be?

A. 50
B. 70
C. 80
D. 130

**Answer: A**

**Q31.** T1 updates an account balance from 10,000 to 7,000 but has not committed. T2 reads 7,000. T1 subsequently commits.

Which statement is correct?

A. Dirty read occurred.
B. T2 read an uncommitted value, even though T1 eventually committed.
C. Lost update occurred.
D. Phantom read occurred.

**Answer: B**

**Q32.** T1 executes:

```sql
SELECT *
FROM EMPLOYEE
WHERE dept_id = 10;
```

T2 inserts another employee with `dept_id = 10` and commits. T1 executes the same SELECT again and sees an additional row.

Which anomaly is demonstrated?

A. Lost update
B. Dirty read
C. Phantom read
D. Incorrect summary

**Answer: C**

**Q33.** T1 calculates the average salary of all employees. During the calculation, T2 updates several salaries and commits. T1 reads some rows before the updates and others after them.

Which problem can occur?

A. Incorrect summary
B. Lost update only
C. Dirty read necessarily
D. Phantom read necessarily

**Answer: A**

**Q34.** Which scenario represents a non-repeatable read rather than a phantom read?

A. T1 reads employee 101's salary twice; T2 changes that salary and commits between the reads.
B. T1 queries employees with salary above 50,000 twice; T2 inserts a new qualifying employee.
C. T1 reads an uncommitted update.
D. T1 overwrites another transaction's update.

**Answer: A**

**Q35.** Which statement is correct about READ COMMITTED isolation?

A. It permits dirty reads.
B. It prevents dirty reads, but repeated reads may see newer committed values.
C. It guarantees serial execution.
D. It always prevents phantom reads.

**Answer: B**

**Q36.** A transaction executes two SELECT statements. Another transaction inserts a new qualifying record and commits between those statements. Which isolation level in the standard SQL model prevents the resulting phantom read?

A. READ UNCOMMITTED
B. READ COMMITTED
C. REPEATABLE READ
D. SERIALIZABLE

**Answer: D**

**Q37.** Two transactions read the same record and then both attempt to update it. Which problem can arise if concurrency control is inadequate?

A. Lost update
B. Phantom read only
C. Dirty read only
D. Batch failure

**Answer: A**

**Q38.** A transaction reads a record that another transaction has updated but not committed. The second transaction rolls back. What is the main anomaly?

A. Phantom read
B. Dirty read
C. Incorrect summary
D. Non-repeatable read

**Answer: B**

## Section E - Shared locks, Exclusive locks and lock compatibility

**Q39.** Transaction T1 obtains a Shared lock on row 101. Transaction T2 requests a Shared lock on the same row. What happens?

A. T2 waits until T1 commits.
B. T2 can obtain the Shared lock because S and S are compatible.
C. T2 automatically obtains an Exclusive lock.
D. T1 is rolled back.

**Answer: B**

**Q40.** T1 holds an Exclusive lock on row 101. T2 requests an Exclusive lock on the same row.

What happens?

A. Both transactions obtain X locks.
B. T2 waits until the conflicting lock is released.
C. T2 receives an S lock.
D. T1 automatically commits.

**Answer: B**

**Q41.** Which lock combination is compatible?

A. S and X
B. X and X
C. S and S
D. None of these

**Answer: C**

**Q42.** Consider the lock compatibility matrix:

| Existing lock | Requested S | Requested X |
| --- | --- | --- |
| S | ? | ? |
| X | ? | ? |

Which option correctly fills the four positions?

A. Compatible, incompatible, incompatible, incompatible
B. Compatible, compatible, incompatible, incompatible
C. Incompatible, compatible, compatible, incompatible
D. Incompatible, incompatible, compatible, compatible

**Answer: A**

**Q43.** T1 holds a Shared lock on a table. T2 wants to read the same table.

Which statement is correct?

A. T2 cannot read because another transaction already holds a lock.
B. T2 can generally acquire another Shared lock.
C. T2 must obtain an Exclusive lock.
D. T1 must roll back.

**Answer: B**

**Q44.** T1 holds an Exclusive lock on a resource. T2 wants to read the same resource.

Which statement is correct?

A. T2 can always read immediately.
B. T2's conflicting Shared lock request must wait.
C. T2 receives an Exclusive lock automatically.
D. T1's lock becomes Shared.

**Answer: B**

**Q45.** Why do Shared locks generally allow higher concurrency than Exclusive locks?

A. Shared locks allow multiple readers to access the same resource simultaneously.
B. Shared locks automatically commit transactions.
C. Shared locks allow unrestricted simultaneous updates.
D. Shared locks do not require database resources.

**Answer: A**

**Q46.** T1 holds an S lock on resource A. T2 holds an S lock on resource A. T1 requests conversion from S to X.

What is the likely result?

A. Immediate conversion is always guaranteed.
B. T1 may wait for T2's S lock to be released.
C. T2 automatically receives an X lock.
D. Both transactions are committed.

**Answer: B**

## Section F - Two-Phase Locking (2PL)

**Q47.** A transaction follows this sequence:

1. Acquire S lock on A.
2. Acquire X lock on B.
3. Release S lock on A.
4. Request S lock on C.

Does this follow basic 2PL?

A. Yes, because all requested locks are valid.
B. No, because a new lock is requested after a lock has been released.
C. Yes, because the new lock is Shared.
D. Yes, because X locks are not involved.

**Answer: B**

**Q48.** Which sequence correctly follows basic 2PL?

A. Acquire S(A), acquire X(B), release S(A), acquire S(C).
B. Acquire S(A), acquire X(B), release S(A), release X(B).
C. Acquire X(A), release X(A), acquire S(B), acquire X(C).
D. Release S(A), acquire X(B).

**Answer: B**

**Q49.** Under 2PL, when does the shrinking phase begin?

A. When the first lock is acquired.
B. When the transaction executes its first COMMIT.
C. When the transaction releases its first lock.
D. When the first SELECT executes.

**Answer: C**

**Q50.** Which statement distinguishes Strict 2PL from basic 2PL?

A. Strict 2PL holds Exclusive locks until transaction completion.
B. Strict 2PL does not acquire locks.
C. Strict 2PL allows new locks after releasing old locks.
D. Strict 2PL prohibits UPDATE statements.

**Answer: A**

**Q51.** Which is the primary advantage of Strict 2PL?

A. It eliminates every possible deadlock.
B. It prevents cascading rollback by retaining write locks until transaction completion.
C. It allows dirty reads.
D. It removes the need for COMMIT.

**Answer: B**

**Q52.** T1 locks A and requests B. T2 locks B and requests A. Neither transaction can proceed.

Which situation exists?

A. Starvation only
B. Deadlock
C. Phantom read
D. Dirty read

**Answer: B**

## Section G - Serializability and alternative concurrency techniques

**Q53.** Consider two transactions:

```text
T1: Read(A)
T1: Write(A)

T2: Read(A)
T2: Write(A)
```

If the execution order is:

```text
T1: Read(A)
T1: Write(A)
T2: Read(A)
T2: Write(A)
```

Which statement is correct?

A. It is equivalent to serial execution T1 followed by T2.
B. It is equivalent to serial execution T2 followed by T1.
C. It is necessarily non-serializable.
D. It produces a dirty read.

**Answer: A**

**Q54.** Which statement defines serializability?

A. All transactions must execute one after another physically.
B. Concurrent execution must produce an outcome equivalent to some serial ordering of the transactions.
C. Transactions cannot read the same table.
D. Every transaction must be READ ONLY.

**Answer: B**

**Q55.** Consider the schedule:

```text
T1: Read(A)
T2: Read(A)
T1: Write(A)
T2: Write(A)
```

Assume both transactions write A and the conflict order forms a cycle in the precedence graph. What does this indicate?

A. Conflict-serializable schedule
B. Non-conflict-serializable schedule
C. Strictly serial schedule
D. Read-only schedule

**Answer: B**

**Q56.** Which concurrency technique assigns timestamps to transactions and uses them to determine whether operations are permitted?

A. Lock-based concurrency control
B. Timestamp ordering
C. Validation-based control
D. Batch processing

**Answer: B**

**Q57.** Transaction T1 has timestamp 10 and T2 has timestamp 20. Under basic timestamp ordering, T1 is older than T2.

Which statement is correct?

A. T1 must always execute after T2.
B. The protocol enforces an ordering consistent with the assigned timestamps.
C. T2 cannot execute any SQL statements.
D. Both transactions must acquire Exclusive locks.

**Answer: B**

**Q58.** Which statement correctly describes validation-based concurrency control?

A. Transactions acquire all locks before reading any data.
B. Transactions perform their work and undergo validation before committing to detect conflicting executions.
C. Transactions never require validation.
D. All transactions execute in batch mode.

**Answer: B**

**Q59.** Which situation is most suitable for optimistic or validation-based concurrency control?

A. An environment with frequent conflicting updates and heavy contention
B. An environment where conflicts are relatively rare
C. An environment where transactions must always be serialized physically
D. An environment where no transactions read data

**Answer: B**

**Q60.** Consider two transactions operating on the same account:

```text
T1:
    Read(balance)
    balance = balance - 1000
    Write(balance)

T2:
    Read(balance)
    balance = balance + 500
    Write(balance)
```

Initial balance = 10,000.

Both transactions read 10,000 before either writes. T1 writes 9,000, and T2 subsequently writes 10,500.

What is the final balance, and what is the problem?

A. 9,500; correct execution
B. 10,500; lost update
C. 9,000; dirty read
D. 11,500; phantom read

**Answer: B**

---

## Consolidated answer key

| Q | Ans | Q | Ans | Q | Ans |
| --- | --- | --- | --- | --- | --- |
| 1 | B | 21 | D | 41 | C |
| 2 | B | 22 | A | 42 | A |
| 3 | C | 23 | B | 43 | B |
| 4 | B | 24 | B | 44 | B |
| 5 | C | 25 | B | 45 | A |
| 6 | A | 26 | A | 46 | B |
| 7 | B | 27 | C | 47 | B |
| 8 | C | 28 | B | 48 | B |
| 9 | C | 29 | B | 49 | C |
| 10 | B | 30 | A | 50 | A |
| 11 | B | 31 | B | 51 | B |
| 12 | B | 32 | C | 52 | B |
| 13 | B | 33 | A | 53 | A |
| 14 | B | 34 | A | 54 | B |
| 15 | D | 35 | B | 55 | B |
| 16 | B | 36 | D | 56 | B |
| 17 | B | 37 | A | 57 | B |
| 18 | B | 38 | B | 58 | B |
| 19 | B | 39 | B | 59 | B |
| 20 | C | 40 | B | 60 | B |

## Important HSQLDB-specific exam notes

- JDBC connections default to autocommit TRUE.
- HSQLDB's default transaction isolation is READ COMMITTED.
- Changing JDBC autocommit from FALSE to TRUE commits the current transaction.
- A failed SQL statement does not universally imply that the entire transaction has been rolled back.
- A savepoint allows partial rollback within a transaction.
- Shared locks are compatible with Shared locks; Exclusive locks conflict with both.
- Basic 2PL has growing and shrinking phases.
- Strict 2PL retains Exclusive locks until transaction completion.
- Do not assume that textbook 2PL is the exact internal implementation of every HSQLDB transaction-control mode. HSQLDB supports different transaction-control models, including MVCC-based modes.

**HSQLDB reference:** [HSQLDB - Sessions and Transactions](https://hsqldb.org/doc/2.0/guide/sessions-chapt.html).

### User

big data characterstics briefly explain variery volume velocity veracity value, types of no sql databases proper examples for them each where it is used applications key value store column family store document oriented database graph database why each document oriented flexible schema rich querying language, rapid application development, suitable for storing data which requires no frequent updates but read many times, graph db charactersitcs data heavily interconnected relationship no need joins graph theory ensure acid properties only this ensure acid properties, sql vs no sql felxible vs rigid schema, small vs large storage, centralized vs distributed storage vertical vs horizontal scalbility, polyglot persistence ecommerce each category where will u store, cap therem database availabllity mre imprtant then cnsistency mre important then ap: cassandra cp mngdb neo4j ca sql database no sql databases have partition tolerance compulsory, eric brewer theorem eventual consistency strong consistency how no sql ensures consisency through eventual consistency ony questions give no theory what and all tricky mcqs can be asked from it make a quiz of 60 questions all tricky advanced take time and think and give based on above concepts give only give question mcq and asnwer not quiz interface types of database which will be used for which based characterstics of each and what db it is based on each type of no sql db properties ask questions which db like that based on cap theorem ask questions theory 5-8 qns give more emphasis on no sql and types of no sql

### ChatGPT

# Big Data & NoSQL Databases - Advanced SQL Developer MCQ Test

(Expert difficulty) (60 MCQs)

**Level:** 2-year SQL Developer

**Question distribution:**

- Big Data characteristics (5 Vs): 5 questions
- NoSQL fundamentals and SQL vs NoSQL: 7 questions
- NoSQL database types and applications: 28 questions
- Polyglot persistence and database selection: 7 questions
- CAP theorem and consistency models: 13 questions

The emphasis is on identifying the correct database from its characteristics, choosing databases for real-world applications, and tricky CAP theorem scenarios.

## Section A - Big Data characteristics

**Q1.** An e-commerce platform stores billions of customer transactions, product images, videos and clickstream records. Which Big Data characteristic describes the amount of data?

A. Velocity
B. Variety
C. Volume
D. Veracity

**Answer: C - Volume**

**Q2.** A stock trading platform receives thousands of transactions every second and must process them immediately. Which characteristic is being demonstrated?

A. Volume
B. Velocity
C. Variety
D. Value

**Answer: B - Velocity**

**Q3.** A company collects structured SQL records, JSON documents, audio files, videos and sensor readings. Which characteristic describes this?

A. Veracity
B. Velocity
C. Variety
D. Value

**Answer: C - Variety**

**Q4.** A company receives inaccurate, duplicated and incomplete customer records from different sources. Which Big Data characteristic addresses the reliability and quality of this data?

A. Volume
B. Value
C. Velocity
D. Veracity

**Answer: D - Veracity**

**Q5.** A company analyzes customer purchasing patterns to improve recommendations and increase revenue. Which Big Data characteristic describes the business benefit obtained from data?

A. Value
B. Variety
C. Volume
D. Velocity

**Answer: A - Value**

## Section B - NoSQL fundamentals and SQL vs NoSQL

**Q6.** Which statement best describes NoSQL databases?

A. Databases that cannot store structured data
B. Databases designed with non-relational data models and flexible distributed data storage approaches
C. Databases that cannot perform queries
D. Databases that do not support any consistency guarantees

**Answer: B**

**Q7.** Which is a major difference between traditional relational databases and many NoSQL databases?

A. SQL databases cannot store strings.
B. NoSQL databases generally offer more flexible data models, while relational databases commonly use predefined schemas.
C. SQL databases cannot support transactions.
D. NoSQL databases cannot scale horizontally.

**Answer: B**

**Q8.** Which scalability approach is most closely associated with traditional relational databases?

A. Horizontal scaling only
B. Vertical scaling by increasing CPU, RAM and storage resources
C. Removing database servers
D. Adding graph nodes

**Answer: B**

**Q9.** A company wants to distribute its database workload across multiple machines by adding more servers. Which scaling method is this?

A. Vertical scaling
B. Horizontal scaling
C. Schema normalization
D. Index clustering

**Answer: B**

**Q10.** Which statement about NoSQL databases is correct?

A. All NoSQL databases are eventually consistent.
B. All NoSQL databases reject ACID transactions.
C. NoSQL databases have different consistency and transaction models depending on the database.
D. NoSQL databases cannot support distributed transactions.

**Answer: C**

**Q11.** Which scenario is most suitable for a traditional relational database?

A. Storing highly interconnected social network relationships without joins
B. Banking transactions requiring relational constraints and strong transactional consistency
C. Storing millions of independent sensor readings with flexible structures
D. Storing frequently changing JSON documents with different attributes

**Answer: B**

**Q12.** A company needs to store customer information where each customer document can have different attributes, without requiring a fixed relational table structure.

Which database category is most appropriate?

A. Relational database
B. Document-oriented database
C. Graph database
D. Key-value database only

**Answer: B**

## Section C - NoSQL database types and their characteristics

### Key-value databases

**Q13.** Which NoSQL database type stores information as a collection of key-value pairs?

A. Graph database
B. Column-family database
C. Key-value database
D. Relational database

**Answer: C**

**Q14.** An e-commerce application needs extremely fast retrieval of user sessions using a unique session ID. Which database is most appropriate?

A. Redis
B. Neo4j
C. Cassandra
D. MongoDB

**Answer: A**

**Q15.** Consider the following data:

```text
user_101 → {name: "Raj", city: "Chennai"}
user_102 → {name: "Sam", city: "Bangalore"}
```

Which database model best represents this structure when the entire value is retrieved using its key?

A. Graph
B. Key-value
C. Column-family
D. Relational

**Answer: B**

**Q16.** Which application is best suited for a key-value store?

A. Finding the shortest path between two cities
B. Retrieving shopping cart data using a cart ID
C. Performing complex multi-table joins
D. Querying relationships between millions of connected entities

**Answer: B**

**Q17.** Which statement best describes Redis?

A. A graph database based on nodes and edges
B. An in-memory data structure store commonly used as a key-value database
C. A relational database supporting SQL joins
D. A column-family database only

**Answer: B**

**Q18.** Which operation is generally a strength of key-value databases?

A. Complex relational joins
B. Direct retrieval using a known key
C. Recursive relationship traversal
D. Arbitrary multi-document analytical joins

**Answer: B**

### Document-oriented databases

**Q19.** Which of the following is a document-oriented NoSQL database?

A. Cassandra
B. Redis
C. MongoDB
D. Neo4j

**Answer: C**

**Q20.** A company stores customer records in JSON-like documents. Some customers have additional attributes such as loyalty status, preferences and multiple addresses, while others do not.

Which database is most appropriate?

A. MongoDB
B. Redis
C. Neo4j
D. Cassandra only

**Answer: A**

**Q21.** Which characteristic makes document databases suitable for rapid application development?

A. Every document must have exactly the same attributes.
B. Flexible document structures allow application data models to evolve without requiring identical table schemas.
C. They prohibit nested data.
D. They require all data to be normalized into separate tables.

**Answer: B**

**Q22.** Which statement about document-oriented databases is correct?

A. They store only key-value pairs without querying capabilities.
B. They support rich queries over document fields and nested structures.
C. They store data only as graph edges.
D. They cannot index document fields.

**Answer: B**

**Q23.** A content management system stores articles, images metadata, author information, tags and embedded comments. Which database is a natural choice?

A. MongoDB
B. Redis
C. Neo4j
D. Cassandra

**Answer: A**

**Q24.** Which statement about the claim that document databases are suitable for read-heavy workloads is most accurate?

A. All document databases prohibit frequent updates.
B. Document databases can efficiently retrieve complete documents, making them useful for read-heavy access patterns, but they also support updates.
C. Document databases cannot update individual fields.
D. Document databases are exclusively read-only.

**Answer: B**

**Q25.** Which of the following is NOT a typical advantage of document-oriented databases?

A. Flexible schema
B. Nested document storage
C. Rich querying
D. Mandatory fixed columns across all records

**Answer: D**

**Q26.** Which statement best describes MongoDB's document model?

A. Data is represented using BSON documents organized into collections.
B. Data is stored only in graph nodes and edges.
C. Data is stored only in column families.
D. Data is stored only as strings associated with keys.

**Answer: A**

### Column-family databases

**Q27.** Which of the following is a column-family NoSQL database?

A. MongoDB
B. Redis
C. Apache Cassandra
D. Neo4j

**Answer: C - Apache Cassandra**

**Q28.** A telecommunications company generates billions of time-series records across geographically distributed servers. It requires high write throughput and horizontal scalability.

Which database is most appropriate?

A. Cassandra
B. Neo4j
C. Redis
D. MongoDB only

**Answer: A - Cassandra**

**Q29.** Which characteristic best describes a column-family database?

A. Data is stored exclusively as nodes and edges.
B. Data is organized into rows and flexible groups of columns, often called column families.
C. Data is stored only as JSON documents.
D. Data is stored only in memory.

**Answer: B**

**Q30.** Which database is particularly suitable for a globally distributed application requiring high write availability across multiple data centres?

A. Neo4j
B. Cassandra
C. Redis
D. SQLite

**Answer: B - Cassandra**

**Q31.** A company needs to store billions of IoT sensor readings. Its main requirements are high write throughput, distributed storage and horizontal scalability.

Which database would be the strongest candidate?

A. Cassandra
B. Neo4j
C. Redis
D. Traditional single-server relational database

**Answer: A**

**Q32.** Which statement about Cassandra is correct?

A. It is primarily a graph database.
B. It is a distributed wide-column/column-family database.
C. It is exclusively a document database.
D. It is an in-memory key-value database only.

**Answer: B**

**Q33.** Which database model is most suitable when queries are primarily designed around partition keys and clustering columns, rather than arbitrary relational joins?

A. Cassandra's wide-column model
B. Neo4j's graph model
C. MongoDB's document model only
D. Traditional relational model only

**Answer: A**

### Graph databases

**Q34.** Which database is an example of a graph database?

A. MongoDB
B. Cassandra
C. Neo4j
D. Redis

**Answer: C - Neo4j**

**Q35.** A social networking application needs to find friends of friends, mutual connections and shortest relationship paths.

Which database is most suitable?

A. Redis
B. Neo4j
C. Cassandra
D. Traditional file storage

**Answer: B**

**Q36.** What are the primary components of a property graph?

A. Tables and columns
B. Keys and values only
C. Nodes, relationships and properties
D. Rows and foreign keys only

**Answer: C**

**Q37.** Which statement describes a major advantage of graph databases?

A. They eliminate the need to store relationships.
B. They efficiently represent and traverse highly interconnected data.
C. They are designed exclusively for storing images.
D. They cannot represent many-to-many relationships.

**Answer: B**

**Q38.** An organization maintains a fraud detection system. It needs to discover relationships between bank accounts, devices, IP addresses and suspicious transactions.

Which database is the best fit?

A. Neo4j
B. Redis
C. MongoDB only
D. Cassandra only

**Answer: A**

**Q39.** Why can graph databases be more suitable than relational databases for deeply interconnected data?

A. Graph databases do not store data.
B. Relationships are represented directly, allowing traversal without repeatedly constructing complex relational joins.
C. Graph databases cannot use indexes.
D. Graph databases do not support transactions.

**Answer: B**

**Q40.** Which statement about Neo4j is correct?

A. It is a graph database that supports ACID transactions.
B. It is an eventually consistent key-value store only.
C. It is a column-family database.
D. It cannot enforce transactional consistency.

**Answer: A**

**Q41.** A company needs to model a knowledge graph connecting people, products, organizations, locations and their relationships.

Which database should be preferred?

A. Redis
B. Cassandra
C. Neo4j
D. SQLite

**Answer: C**

## Section D - Database selection and polyglot persistence

**Q42.** An e-commerce application has the following requirements:

1. Shopping cart retrieval using cart ID
2. Product catalog with flexible attributes
3. Customer relationship recommendations
4. Large-scale order event storage

Which combination is the most appropriate?

A. Redis, MongoDB, Neo4j, Cassandra
B. Neo4j, Redis, MongoDB, SQLite
C. Cassandra, Neo4j, Redis, MongoDB
D. MongoDB, Cassandra, SQLite, Redis

**Answer: A**

**Q43.** An e-commerce platform needs to store shopping cart information that is frequently retrieved and updated using a unique cart identifier.

Which database is the best choice?

A. Neo4j
B. Redis
C. Cassandra
D. Neo4j and no other database

**Answer: B**

**Q44.** An online shopping platform stores products where each category has different attributes.

For example:

- Mobile: RAM, storage, battery
- Laptop: processor, RAM, graphics card
- Shoes: size, material, colour

Which database is most appropriate?

A. Redis
B. Neo4j
C. MongoDB
D. Cassandra only

**Answer: C**

**Q45.** A shopping application needs to recommend products based on relationships between customers, products, brands and purchases.

Which database is most suitable?

A. Neo4j
B. Redis
C. Cassandra
D. Flat-file database

**Answer: A**

**Q46.** A large e-commerce platform collects millions of order events every day from geographically distributed locations. It requires high write availability and scalable storage.

Which database is most appropriate for the event data?

A. Neo4j
B. Cassandra
C. Redis only
D. SQLite

**Answer: B**

**Q47.** A company uses multiple databases for different requirements: Redis for sessions, MongoDB for product catalogs, Neo4j for recommendations and Cassandra for event storage.

What is this architecture called?

A. Database normalization
B. Polyglot persistence
C. Vertical partitioning only
D. Single-database architecture

**Answer: B**

**Q48.** Which statement best describes polyglot persistence?

A. Using only one database for every application requirement.
B. Using different database technologies based on the data model and workload requirements.
C. Converting all NoSQL databases into SQL databases.
D. Storing all data in memory.

**Answer: B**

**Q49.** An application requires the following:

- Extremely fast session lookup
- Flexible product documents
- Complex social relationship traversal
- Large distributed write-heavy event storage

Which mapping is correct?

A. Redis - sessions; MongoDB - product documents; Neo4j - relationships; Cassandra - events
B. Neo4j - sessions; Cassandra - documents; Redis - relationships; MongoDB - events
C. MongoDB - sessions; Neo4j - documents; Cassandra - relationships; Redis - events
D. Cassandra - sessions; Redis - documents; MongoDB - relationships; Neo4j - events

**Answer: A**

**Q50.** A business wants to store customer profiles, shopping carts, product recommendations and transaction records. Which architecture is most appropriate?

A. Force all information into Redis.
B. Select one database based solely on storage capacity.
C. Use polyglot persistence, choosing suitable databases for each workload while maintaining necessary data consistency across them.
D. Store everything in a graph database.

**Answer: C**

## Section E - CAP theorem and consistency models

**Q51.** What does CAP stand for?

A. Consistency, Availability, Partition Tolerance
B. Concurrency, Atomicity, Performance
C. Consistency, Accuracy, Processing
D. Concurrency, Availability, Persistence

**Answer: A**

**Q52.** According to the CAP theorem, when a network partition occurs, a distributed database must make a trade-off between which two properties?

A. Volume and Velocity
B. Consistency and Availability
C. Durability and Atomicity
D. Scalability and Performance

**Answer: B**

**Q53.** What does Consistency mean in the CAP theorem?

A. Every request must always succeed.
B. Every read receives the most recent successful write or an error, according to the system's consistency guarantee.
C. Data is stored on multiple servers.
D. Every database node has a different copy of data.

**Answer: B**

**Q54.** What does Availability mean in the CAP theorem?

A. Every request received by a non-failing node receives a response, even if it cannot guarantee the latest data.
B. Every read always returns the latest value.
C. Every transaction must execute serially.
D. Every database must use a centralized server.

**Answer: A**

**Q55.** What does Partition Tolerance mean?

A. The database must prevent every network failure.
B. The system continues operating despite network communication failures between distributed nodes, potentially sacrificing consistency or availability.
C. The database must store data in one location.
D. The database must prevent duplicate records.

**Answer: B**

**Q56.** Which database is commonly classified as AP under its typical distributed architecture?

A. Cassandra
B. Neo4j
C. Traditional single-node SQL database
D. MongoDB replica set in its typical CP classification

**Answer: A - Cassandra**

**Q57.** Which database is commonly classified as CP in introductory CAP classifications?

A. Cassandra
B. MongoDB
C. Redis in every possible deployment
D. Every relational database

**Answer: B - MongoDB**

**Q58.** Which statement about Neo4j is correct in the commonly taught CAP classification?

A. AP
B. CP
C. CA under all distributed network failures
D. It does not have a consistency model

**Answer: B - CP**

**Q59.** A distributed application chooses to remain available during a network partition, even if some nodes temporarily return stale data. Which consistency model is most closely associated with this approach?

A. Strong consistency
B. Eventual consistency
C. Immediate serializability
D. Strict two-phase locking

**Answer: B**

**Q60.** Which statement about eventual consistency is correct?

A. All nodes must return identical values immediately after every update.
B. Replicas may temporarily contain different values, but if no new updates occur and synchronization succeeds, they eventually converge.
C. The database never replicates data.
D. Eventual consistency guarantees that dirty reads are impossible.

**Answer: B**

---

## Consolidated answer key

| Q | Answer | Q | Answer | Q | Answer |
| --- | --- | --- | --- | --- | --- |
| 1 | C | 21 | B | 41 | C |
| 2 | B | 22 | B | 42 | A |
| 3 | C | 23 | A | 43 | B |
| 4 | D | 24 | B | 44 | C |
| 5 | A | 25 | D | 45 | A |
| 6 | B | 26 | A | 46 | B |
| 7 | B | 27 | C | 47 | B |
| 8 | B | 28 | A | 48 | B |
| 9 | B | 29 | B | 49 | A |
| 10 | C | 30 | B | 50 | C |
| 11 | B | 31 | A | 51 | A |
| 12 | B | 32 | B | 52 | B |
| 13 | C | 33 | A | 53 | B |
| 14 | A | 34 | C | 54 | A |
| 15 | B | 35 | B | 55 | B |
| 16 | B | 36 | C | 56 | A |
| 17 | B | 37 | B | 57 | B |
| 18 | B | 38 | A | 58 | B |
| 19 | B | 39 | B | 59 | B |
| 20 | B | 40 | A | 60 | B |

## Additional expert-level CAP traps

These are important distinctions that can appear in advanced interviews and MCQs.

| Concept | Correct understanding |
| --- | --- |
| CA | Consistency and availability when there is no partition; cannot guarantee both during a partition in a distributed system. |
| CP | Preserves consistency during a partition, potentially rejecting or delaying some requests. |
| AP | Preserves availability during a partition, potentially allowing temporarily inconsistent responses. |
| Cassandra | Commonly classified as AP, but supports tunable consistency levels. |
| MongoDB | Commonly classified as CP for replica-set partition behavior; configuration and read/write concerns matter. |
| Neo4j | Commonly classified as CP in distributed-cluster CAP discussions. |
| SQL databases | Not automatically CA; distributed SQL databases also make CAP trade-offs. |
| NoSQL | Not every NoSQL database is eventually consistent. |
| Eventual consistency | Replicas converge after updates stop and replication completes. |
| Strong consistency | Reads observe the latest committed write according to the consistency guarantee. |

**One important correction for exams:** Partition tolerance is not a property exclusive to NoSQL. CAP applies to distributed systems, both SQL and NoSQL. Also, Cassandra's tunable consistency means it is not accurate to assume every Cassandra read is eventually consistent.

**Most important database identification to memorize:**

- Redis → Key-value
- MongoDB → Document-oriented
- Cassandra → Column-family / wide-column
- Neo4j → Graph database

These four database-identification patterns, their real-world applications, and their CAP classifications are particularly important for scenario-based questions.

### User

big data characterstics briefly explain variery volume velocity veracity value, types of no sql databases proper examples for them each where it is used applications key value store column family store document oriented database graph database why each document oriented flexible schema rich querying language, rapid application development, suitable for storing data which requires no frequent updates but read many times, graph db charactersitcs data heavily interconnected relationship no need joins graph theory ensure acid properties only this ensure acid properties, sql vs no sql felxible vs rigid schema, small vs large storage, centralized vs distributed storage vertical vs horizontal scalbility, polyglot persistence ecommerce each category where will u store, cap therem database availabllity mre imprtant then cnsistency mre important then ap: cassandra cp mngdb neo4j ca sql database no sql databases have partition tolerance compulsory, eric brewer theorem eventual consistency strong consistency how no sql ensures consisency through eventual consistency ony questions give no theory what and all tricky mcqs can be asked from it make a quiz of 60 questions all tricky advanced take time and think and give based on above concepts give only give question mcq and asnwer not quiz interface types of database which will be used for which based characterstics of each and what db it is based on each type of no sql db properties ask questions which db like that based on cap theorem ask questions theory 5-8 qns give more emphasis on no sql and types of no sql

### ChatGPT

# Big Data & NoSQL - Expert-Level MCQ Set 2

(Advanced / 2-year SQL Developer) (60 MCQs)

This is a new set with different scenarios, focusing heavily on identifying database types from their internal characteristics, choosing the correct database for a business requirement, database architecture, polyglot persistence and CAP theorem.

## Section A - Big Data characteristics

**Q1.** A healthcare organization stores 20 years of medical records, MRI images, prescriptions and patient videos. Which Big Data characteristic is primarily represented by the enormous quantity of stored information?

A. Variety
B. Velocity
C. Volume
D. Veracity

**Answer: C - Volume**

**Q2.** A financial application receives thousands of stock price updates per second and must process them immediately. Which characteristic is involved?

A. Value
B. Velocity
C. Veracity
D. Variety

**Answer: B - Velocity**

**Q3.** A company receives data in CSV, JSON, XML, audio, video and image formats. Which characteristic is demonstrated?

A. Volume
B. Value
C. Veracity
D. Variety

**Answer: D - Variety**

**Q4.** An analytics platform receives contradictory customer information, duplicate records and inaccurate sensor measurements. Which characteristic addresses this problem?

A. Veracity
B. Volume
C. Velocity
D. Value

**Answer: A - Veracity**

**Q5.** A retail company analyzes historical purchases to identify profitable products and improve customer retention. Which Big Data characteristic represents the benefit derived from analysis?

A. Velocity
B. Value
C. Variety
D. Volume

**Answer: B - Value**

## Section B - Identify the NoSQL database from its characteristics

**Q6.** A database stores information using a unique identifier and its associated value. The application retrieves the complete value directly using the identifier.

Which database type is this?

A. Graph
B. Document
C. Key-value
D. Column-family

**Answer: C**

**Q7.** A system needs to store millions of temporary authentication tokens. Each token is accessed using a unique session key, and retrieval must be extremely fast.

Which database should be selected?

A. Neo4j
B. Redis
C. Cassandra
D. MongoDB

**Answer: B - Redis**

**Q8.** A database stores customer information as independent documents. Each document can have different fields, nested objects and arrays.

Which database model is being used?

A. Key-value
B. Document-oriented
C. Graph
D. Column-family

**Answer: B**

**Q9.** A database is designed for massive distributed data storage, high write throughput and flexible column families. Which database is most suitable?

A. Redis
B. MongoDB
C. Cassandra
D. Neo4j

**Answer: C**

**Q10.** A database represents entities as nodes and their associations as edges. Queries frequently traverse several levels of relationships.

Which database is most suitable?

A. MongoDB
B. Redis
C. Neo4j
D. Cassandra

**Answer: C**

**Q11.** An application requires retrieving a value using a known key. It does not need to query individual attributes inside that value.

Which database model is the simplest fit?

A. Graph
B. Key-value
C. Column-family
D. Relational

**Answer: B**

**Q12.** Which database type is best suited for storing highly interconnected data such as people, friendships, transactions and relationships?

A. Document-oriented
B. Key-value
C. Graph
D. Column-family

**Answer: C**

**Q13.** A database organizes records into rows, with each row potentially containing a different number of columns grouped into column families. Which model is this?

A. Graph
B. Wide-column
C. Document
D. Key-value

**Answer: B**

**Q14.** A company needs to store product information in JSON-like structures and query nested fields such as `specifications.ram` and `specifications.processor`.

Which database is the best fit?

A. Redis
B. Cassandra
C. MongoDB
D. Neo4j

**Answer: C**

**Q15.** A database must support extremely fast access to shopping cart data using a cart ID. The entire cart can be retrieved as one value.

Which database type is most suitable?

A. Graph
B. Key-value
C. Column-family
D. Relational

**Answer: B**

**Q16.** A company wants to discover whether two bank accounts are connected through shared devices, IP addresses or transaction relationships.

Which database model is most suitable?

A. Document
B. Key-value
C. Graph
D. Column-family

**Answer: C**

**Q17.** Which database is most appropriate for geographically distributed IoT data with enormous write volume and predictable partition-key-based queries?

A. Neo4j
B. Cassandra
C. Redis
D. SQLite

**Answer: B**

**Q18.** Which database model is most appropriate when an application frequently retrieves an entire JSON document rather than performing joins across multiple tables?

A. Document-oriented
B. Graph
C. Relational only
D. Column-family only

**Answer: A**

## Section C - Document, key-value, column-family and graph database properties

**Q19.** Which characteristic of document-oriented databases allows different documents in the same collection to contain different attributes?

A. Fixed schema
B. Flexible schema
C. Mandatory normalization
D. Foreign key enforcement

**Answer: B**

**Q20.** A startup changes its customer data model frequently. New fields are introduced without requiring every existing document to contain them.

Which document database advantage is being used?

A. Strict schema enforcement
B. Flexible schema
C. Mandatory relational joins
D. Centralized storage

**Answer: B**

**Q21.** Which feature of document-oriented databases supports rapid application development?

A. Every document must have identical columns.
B. Developers can evolve document structures as application requirements change.
C. Developers must create separate tables for every nested object.
D. Documents cannot contain arrays.

**Answer: B**

**Q22.** A company stores product descriptions that are frequently read but rarely modified. The entire product document is usually retrieved in one operation.

Which characteristic makes a document database suitable?

A. Document-oriented storage can efficiently retrieve complete documents.
B. Document databases prohibit updates.
C. Document databases require a separate table for each attribute.
D. Document databases cannot index fields.

**Answer: A**

**Q23.** Which statement about document databases is INCORRECT?

A. They support nested documents.
B. They can support rich queries on document fields.
C. They require all documents to have exactly the same structure.
D. They are useful for rapidly evolving application data.

**Answer: C**

**Q24.** A developer needs to retrieve a nested value using:

```text
customer.address.city
```

Which database is most naturally suited to this type of data representation?

A. MongoDB
B. Redis
C. Neo4j
D. Cassandra exclusively

**Answer: A**

**Q25.** Which statement correctly describes key-value databases?

A. They are primarily optimized for recursive relationship traversal.
B. They retrieve values through keys and are especially useful for caching and session management.
C. They require SQL joins for every retrieval.
D. They store data only as relational rows.

**Answer: B**

**Q26.** Which application is LEAST suitable for a simple key-value database?

A. Session storage
B. Shopping cart retrieval by cart ID
C. Cache lookup using a known key
D. Finding all friends of friends up to four relationship levels

**Answer: D**

**Q27.** Which database is commonly associated with wide-column storage?

A. Cassandra
B. MongoDB
C. Neo4j
D. Redis

**Answer: A**

**Q28.** A company stores time-series data with millions of records per day. Queries are usually based on device ID and time range. Which database is a strong candidate?

A. Neo4j
B. Cassandra
C. Redis
D. A graph database

**Answer: B**

**Q29.** Which statement best explains why Cassandra is appropriate for write-intensive distributed applications?

A. It is designed for distributed operation, horizontal scalability and high write throughput.
B. It requires a single centralized database server.
C. It depends on complex joins.
D. It stores all data exclusively in RAM.

**Answer: A**

**Q30.** Which statement about graph databases is correct?

A. They represent relationships indirectly using foreign keys only.
B. They represent nodes and relationships explicitly, making traversal of connected data natural.
C. They cannot represent cycles.
D. They are designed exclusively for caching.

**Answer: B**

**Q31.** A recommendation engine needs to identify:

- Customers who purchased a product
- Customers who viewed similar products
- Products purchased by those customers
- Products related to the original product

Which database is most appropriate?

A. Redis
B. Cassandra
C. Neo4j
D. A simple key-value database

**Answer: C**

**Q32.** Which statement about graph databases and joins is most accurate?

A. Graph databases cannot execute joins.
B. Graph databases represent relationships directly, so relationship traversal often avoids complex relational joins.
C. Graph databases do not support queries.
D. Graph databases store only unconnected records.

**Answer: B**

**Q33.** Which statement about ACID support is correct?

A. Only relational databases support ACID.
B. NoSQL databases never support ACID.
C. NoSQL databases such as MongoDB and Neo4j can support ACID transactions, with guarantees depending on the database and transaction scope.
D. Graph databases cannot support atomic transactions.

**Answer: C**

**Q34.** Which database is most appropriate when the application requires traversing millions of interconnected relationships rather than retrieving isolated records?

A. Redis
B. Neo4j
C. MongoDB
D. Cassandra

**Answer: B**

## Section D - SQL vs NoSQL and polyglot persistence

**Q35.** Which statement correctly compares relational and NoSQL databases?

A. SQL databases generally use predefined relational schemas; many NoSQL databases support more flexible data models.
B. SQL databases cannot store large datasets.
C. NoSQL databases cannot store structured data.
D. NoSQL databases cannot scale horizontally.

**Answer: A**

**Q36.** A company has a traditional centralized relational database running on one powerful server. It wants to increase its processing capacity by adding more CPU and RAM.

Which scalability approach is being used?

A. Horizontal
B. Vertical
C. Graph scaling
D. Document scaling

**Answer: B**

**Q37.** A distributed database increases capacity by adding more machines to the cluster.

Which scalability approach is this?

A. Vertical
B. Horizontal
C. Schema-based
D. Centralized

**Answer: B**

**Q38.** Which statement is the most accurate comparison of SQL and NoSQL storage architecture?

A. Every SQL database is centralized and every NoSQL database is distributed.
B. SQL databases are always vertical, and NoSQL databases are always horizontal.
C. Traditional relational deployments commonly scale vertically, while many NoSQL systems are designed for distributed horizontal scaling; neither is an absolute rule.
D. NoSQL databases cannot run on a single machine.

**Answer: C**

**Q39.** An online retailer uses:

- Redis for shopping carts
- MongoDB for product catalogs
- Cassandra for clickstream events
- Neo4j for recommendations

Which architectural principle does this demonstrate?

A. Data redundancy
B. Polyglot persistence
C. Database normalization
D. Vertical partitioning

**Answer: B**

**Q40.** Why is polyglot persistence useful?

A. It forces every application component to use the same database.
B. It allows different data stores to be selected according to their workload and data model.
C. It eliminates all data synchronization requirements.
D. It guarantees that every database has identical consistency properties.

**Answer: B**

**Q41.** A business uses MongoDB for product details and Cassandra for large-scale order events. Both databases store related product and order information.

What challenge should the application account for?

A. Cross-database data consistency and synchronization
B. Both databases must use identical schemas
C. MongoDB cannot store product details
D. Cassandra cannot store order events

**Answer: A**

**Q42.** Which mapping is the BEST choice?

| Requirement | Database |
| --- | --- |
| A. Fast session lookup | Neo4j |
| B. Product JSON documents | MongoDB |
| C. Social relationship traversal | Cassandra |
| D. Massive write-heavy events | Redis |

**Answer: B**

**Q43.** A company wants a database for banking transactions with strict relational constraints, multi-row transactions and established SQL support. Which is the most appropriate choice?

A. Redis
B. Cassandra
C. Relational SQL database
D. A simple key-value store

**Answer: C**

**Q44.** Which statement about storage size is correct?

A. SQL databases can store only small amounts of data.
B. NoSQL databases can store only large amounts of data.
C. Both SQL and NoSQL databases can handle large datasets, depending on architecture and deployment.
D. NoSQL databases cannot store small datasets.

**Answer: C**

## Section E - CAP theorem and consistency

**Q45.** In CAP theorem, what does C represent?

A. Concurrency
B. Consistency
C. Centralization
D. Compression

**Answer: B**

**Q46.** In CAP theorem, what does A represent?

A. Atomicity
B. Availability
C. Accuracy
D. Authorization

**Answer: B**

**Q47.** What does P represent in CAP theorem?

A. Persistence
B. Performance
C. Partition Tolerance
D. Processing

**Answer: C**

**Q48.** According to Eric Brewer's CAP theorem, when a network partition occurs, which two properties must a distributed system trade off?

A. Volume and Variety
B. Consistency and Availability
C. Atomicity and Durability
D. Scalability and Velocity

**Answer: B**

**Q49.** A distributed database rejects certain read and write requests during a network partition to prevent returning conflicting data.

Which CAP category does this behavior represent?

A. AP
B. CP
C. CA
D. None of these

**Answer: B**

**Q50.** A distributed database continues accepting requests from reachable nodes during a network partition, even though some clients may receive stale data.

Which CAP category does this behavior represent?

A. CP
B. CA
C. AP
D. ACID

**Answer: C**

**Q51.** Which statement about Partition Tolerance is correct?

A. It means network partitions can never happen.
B. It means the system is designed to operate despite network communication failures between distributed nodes.
C. It means every transaction must be serializable.
D. It means all replicas always have identical data.

**Answer: B**

**Q52.** Which database is commonly classified as AP in introductory CAP-theorem examples?

A. Cassandra
B. Neo4j
C. MongoDB replica set
D. Traditional single-node relational database

**Answer: A**

**Q53.** Which database is commonly classified as CP in introductory CAP-theorem examples?

A. Cassandra
B. MongoDB
C. Every SQL database
D. Redis in every deployment configuration

**Answer: B**

**Q54.** Which statement about CA databases is correct?

A. They guarantee consistency and availability even during network partitions.
B. A purely CA distributed system cannot guarantee both properties during a partition; a single-node system or system without partition handling is a different case.
C. They are always eventually consistent.
D. They do not require data replication.

**Answer: B**

**Q55.** A distributed NoSQL database must continue serving requests during a network partition, even if different nodes temporarily return different values.

Which consistency approach is most appropriate?

A. Strong consistency
B. Eventual consistency
C. Strict serializability at all times
D. Immediate synchronization before every response

**Answer: B**

**Q56.** Which statement best defines eventual consistency?

A. All replicas must contain identical data immediately after every write.
B. Replicas may temporarily differ but converge if updates stop and replication successfully completes.
C. Every read must always return the latest value.
D. Data is never replicated.

**Answer: B**

**Q57.** Which statement best describes strong consistency?

A. A read can return any replica's stale value.
B. A read observes the latest committed write according to the system's consistency guarantee.
C. Replicas never synchronize.
D. A database cannot process concurrent requests.

**Answer: B**

**Q58.** Which statement about Cassandra is correct?

A. Cassandra always provides eventual consistency regardless of configuration.
B. Cassandra supports tunable consistency levels, allowing applications to choose different consistency and availability trade-offs.
C. Cassandra is a graph database.
D. Cassandra cannot replicate data across data centres.

**Answer: B**

**Q59.** A distributed database has three replicas. A write is acknowledged after reaching one replica. A subsequent read is performed from another replica before replication completes.

What can happen?

A. The read must return the latest value.
B. The read may return stale data.
C. The database automatically deletes all replicas.
D. The read must fail in every case.

**Answer: B**

**Q60.** A company operates a globally distributed payment system. During a network partition, it prefers rejecting certain operations rather than accepting conflicting account balances.

Which design priority is most appropriate?

A. AP - availability over consistency
B. CP - consistency over availability during partition
C. CA - guarantee all three CAP properties
D. Eventual consistency with unrestricted writes

**Answer: B**

---

## Consolidated answer key

| Q | Answer | Q | Answer | Q | Answer |
| --- | --- | --- | --- | --- | --- |
| 1 | C | 21 | B | 41 | A |
| 2 | B | 22 | A | 42 | B |
| 3 | D | 23 | C | 43 | C |
| 4 | A | 24 | A | 44 | C |
| 5 | B | 25 | B | 45 | B |
| 6 | C | 26 | D | 46 | B |
| 7 | B | 27 | A | 47 | C |
| 8 | B | 28 | B | 48 | B |
| 9 | C | 29 | A | 49 | B |
| 10 | C | 30 | B | 50 | C |
| 11 | B | 31 | A | 51 | B |
| 12 | B | 32 | B | 52 | A |
| 13 | B | 33 | C | 53 | B |
| 14 | C | 34 | B | 54 | B |
| 15 | B | 35 | A | 55 | B |
| 16 | C | 36 | B | 56 | B |
| 17 | B | 37 | B | 57 | B |
| 18 | A | 38 | C | 58 | B |
| 19 | B | 39 | B | 59 | B |
| 20 | A | 40 | B | 60 | B |

## Final expert exam traps

1. **Redis:** Key-value, in-memory data structures, caching and sessions.
2. **MongoDB:** Document-oriented, BSON, flexible schema and rich queries.
3. **Cassandra:** Wide-column, distributed storage, high write throughput and tunable consistency.
4. **Neo4j:** Graph, nodes, relationships, relationship traversal and ACID transactions.
5. **Document database:** Flexible schema does not mean absence of structure or validation.
6. **Graph database:** Relationships are first-class data, not necessarily implemented through relational joins.
7. **Polyglot persistence:** Different databases for different workloads; synchronization becomes an architectural responsibility.
8. **CAP:** The consistency/availability trade-off matters when a network partition occurs.
9. **AP:** Availability is prioritized during partition, potentially returning stale data.
10. **CP:** Consistency is prioritized during partition, potentially rejecting requests.
11. **CA:** Cannot guarantee both consistency and availability during a network partition in a distributed system.
12. **NoSQL does not mean no ACID:** MongoDB and Neo4j both support ACID transactions.

**Most important exam distinction:** Do not confuse CAP consistency with ACID consistency. CAP consistency concerns the behavior of distributed reads and writes, while ACID consistency concerns preserving database constraints and valid states.

### User

give simple level ony not advanced moderate

### ChatGPT

# Big Data and NoSQL - 60 MCQs

Difficulty: Simple to Moderate | Answers immediately after each question

## Section A - Big Data Characteristics (8 Questions)

**Q1.** Which Big Data characteristic refers to the enormous amount of data generated and stored?

A. Variety
B. Volume
C. Velocity
D. Veracity

**Answer: B - Volume**

**Q2.** Which characteristic refers to the speed at which data is generated and processed?

A. Velocity
B. Variety
C. Value
D. Veracity

**Answer: A - Velocity**

**Q3.** A company collects data in the form of images, videos, JSON files and spreadsheets. Which characteristic is represented?

A. Volume
B. Value
C. Variety
D. Velocity

**Answer: C - Variety**

**Q4.** Incorrect, duplicate and inconsistent data relate to which Big Data characteristic?

A. Value
B. Veracity
C. Volume
D. Velocity

**Answer: B - Veracity**

**Q5.** Extracting useful business insights from large datasets represents:

A. Variety
B. Velocity
C. Veracity
D. Value

**Answer: D - Value**

**Q6.** A social media platform receives millions of posts every minute. Which two characteristics are most directly involved?

A. Volume and Velocity
B. Value and Veracity
C. Variety and Value
D. Veracity and Volume

**Answer: A - Volume and Velocity**

**Q7.** Which of the following is an example of Variety?

A. Processing 10,000 transactions per second
B. Storing 10 TB of data
C. Storing text, audio, video and images
D. Removing duplicate records

**Answer: C - Storing text, audio, video and images**

**Q8.** Identifying useful customer purchasing patterns from collected data represents:

A. Value
B. Velocity
C. Volume
D. Variety

**Answer: A - Value**

## Section B - Types of NoSQL Databases (20 Questions)

**Q9.** Which NoSQL database stores data as key-value pairs?

A. MongoDB
B. Redis
C. Neo4j
D. Cassandra

**Answer: B - Redis**

**Q10.** Which database is a document-oriented NoSQL database?

A. Redis
B. Cassandra
C. MongoDB
D. Neo4j

**Answer: C - MongoDB**

**Q11.** Which database is a wide-column or column-family database?

A. Cassandra
B. MongoDB
C. Redis
D. Neo4j

**Answer: A - Cassandra**

**Q12.** Which database stores data using nodes and relationships?

A. Redis
B. MongoDB
C. Cassandra
D. Neo4j

**Answer: D - Neo4j**

**Q13.** Which database type is most suitable for storing user login sessions?

A. Graph database
B. Key-value database
C. Column-family database
D. Relational database only

**Answer: B - Key-value database**

**Q14.** An application needs to store product details in JSON-like documents. Which database is suitable?

A. MongoDB
B. Redis
C. Neo4j
D. Cassandra

**Answer: A - MongoDB**

**Q15.** Which database is most suitable for storing social network relationships such as friends, followers and connections?

A. Redis
B. Cassandra
C. Neo4j
D. MongoDB

**Answer: C - Neo4j**

**Q16.** A company needs to store a large amount of sensor data generated continuously by IoT devices. Which database is a suitable choice?

A. Neo4j
B. Cassandra
C. Redis
D. MongoDB only

**Answer: B - Cassandra**

**Q17.** Which database type stores data using a unique key to retrieve its associated value?

A. Document
B. Graph
C. Key-value
D. Column-family

**Answer: C - Key-value**

**Q18.** Which database type is suitable for storing data with complex relationships between entities?

A. Graph
B. Key-value
C. Document
D. Column-family

**Answer: A - Graph**

**Q19.** Which database is commonly used for caching frequently accessed data?

A. Neo4j
B. Redis
C. Cassandra
D. MongoDB

**Answer: B - Redis**

**Q20.** Which database is suitable for storing customer profiles where different customers may have different attributes?

A. Redis
B. Neo4j
C. MongoDB
D. Cassandra only

**Answer: C - MongoDB**

**Q21.** Which database type is most suitable for storing product information with nested objects and arrays?

A. Key-value
B. Document-oriented
C. Graph
D. Column-family

**Answer: B - Document-oriented**

**Q22.** Which database type is most suitable for applications that need to find connections between people?

A. Key-value
B. Document
C. Graph
D. Column-family

**Answer: C - Graph**

**Q23.** Which of the following is an example of a column-family database?

A. Redis
B. Cassandra
C. MongoDB
D. Neo4j

**Answer: B - Cassandra**

**Q24.** Which of the following is an example of a graph database?

A. Neo4j
B. Redis
C. MongoDB
D. Cassandra

**Answer: A - Neo4j**

**Q25.** Which database model is most suitable when the application retrieves data using a known identifier?

A. Graph
B. Key-value
C. Column-family
D. Relational

**Answer: B - Key-value**

**Q26.** Which database is suitable for storing and querying flexible product catalog documents?

A. MongoDB
B. Redis
C. Neo4j
D. Cassandra

**Answer: A - MongoDB**

**Q27.** Which database type is particularly useful when data is heavily interconnected?

A. Key-value
B. Document
C. Graph
D. Column-family

**Answer: C - Graph**

**Q28.** Which of the following correctly matches the database and its type?

A. Redis - Graph
B. MongoDB - Document
C. Cassandra - Key-value
D. Neo4j - Column-family

**Answer: B - MongoDB - Document**

## Section C - Characteristics of NoSQL Database Types (12 Questions)

**Q29.** Which database type generally supports flexible document structures?

A. Document-oriented
B. Relational only
C. Graph only
D. Key-value only

**Answer: A - Document-oriented**

**Q30.** Different documents in the same MongoDB collection can have:

A. Exactly the same fields only
B. Different fields
C. No fields
D. Only numeric fields

**Answer: B - Different fields**

**Q31.** Which feature of document databases helps developers modify application data structures easily?

A. Fixed schema
B. Flexible schema
C. Mandatory joins
D. Centralized storage

**Answer: B - Flexible schema**

**Q32.** Why are document databases useful in rapid application development?

A. They require every document to have identical fields.
B. They allow document structures to evolve as application requirements change.
C. They do not allow new fields.
D. They support only fixed data types.

**Answer: B**

**Q33.** A product catalog contains product descriptions that are frequently read and rarely updated. Which database type can be suitable?

A. Document-oriented
B. Graph only
C. Key-value only
D. None of these

**Answer: A - Document-oriented**

**Q34.** Which database type directly represents relationships between data entities?

A. Key-value
B. Document
C. Graph
D. Column-family

**Answer: C - Graph**

**Q35.** Why are graph databases useful for social networking applications?

A. They store only key-value pairs.
B. They represent people as nodes and connections as relationships.
C. They cannot store relationships.
D. They require every relationship to be stored as a separate document.

**Answer: B**

**Q36.** Which statement about graph databases is correct?

A. They are useful for highly interconnected data.
B. They are designed only for caching.
C. They cannot represent multiple relationships.
D. They store data only in tables.

**Answer: A**

**Q37.** Which database type is generally suitable for high-speed retrieval using keys?

A. Graph
B. Key-value
C. Document
D. Relational

**Answer: B - Key-value**

**Q38.** Which database type is commonly used for large-scale distributed storage with high write throughput?

A. Cassandra
B. Neo4j
C. Redis
D. SQLite

**Answer: A - Cassandra**

**Q39.** Which statement about NoSQL databases is correct?

A. All NoSQL databases use the same data model.
B. Different NoSQL databases use different data models.
C. NoSQL databases cannot store structured data.
D. NoSQL databases do not support queries.

**Answer: B**

**Q40.** Which statement about ACID properties is correct?

A. Only SQL databases can support ACID.
B. NoSQL databases never support ACID.
C. Some NoSQL databases, such as MongoDB and Neo4j, support ACID transactions.
D. ACID is applicable only to key-value databases.

**Answer: C**

## Section D - SQL vs NoSQL (8 Questions)

**Q41.** Traditional relational databases generally use:

A. Flexible document structures
B. Predefined schemas
C. Key-value pairs only
D. Nodes and edges only

**Answer: B - Predefined schemas**

**Q42.** Many NoSQL databases are known for:

A. Flexible data models
B. Mandatory fixed tables
C. Only relational storage
D. Mandatory SQL joins

**Answer: A - Flexible data models**

**Q43.** Which scalability approach involves adding more powerful hardware to an existing server?

A. Horizontal scaling
B. Vertical scaling
C. Distributed scaling
D. Document scaling

**Answer: B - Vertical scaling**

**Q44.** Which scalability approach involves adding more servers to a system?

A. Vertical scaling
B. Horizontal scaling
C. Centralized scaling
D. Schema scaling

**Answer: B - Horizontal scaling**

**Q45.** Which statement is generally correct?

A. SQL databases cannot store large data.
B. NoSQL databases cannot store small data.
C. Both SQL and NoSQL databases can store large amounts of data.
D. SQL databases cannot be distributed.

**Answer: C**

**Q46.** Which of the following is commonly associated with NoSQL databases?

A. Distributed storage
B. Only centralized storage
C. Mandatory fixed schema
D. Only vertical scaling

**Answer: A - Distributed storage**

**Q47.** Which statement correctly describes SQL and NoSQL?

A. All SQL databases are centralized.
B. All NoSQL databases are distributed.
C. SQL and NoSQL databases can have different architectures and scalability approaches.
D. NoSQL databases cannot support transactions.

**Answer: C**

**Q48.** A company uses Redis for caching, MongoDB for product details and Cassandra for large-scale event data. What is this approach called?

A. Normalization
B. Polyglot persistence
C. Vertical scaling
D. Data duplication

**Answer: B - Polyglot persistence**

## Section E - Polyglot Persistence and CAP Theorem (12 Questions)

**Q49.** What is polyglot persistence?

A. Using only one database for every application
B. Using different database technologies for different requirements
C. Storing only unstructured data
D. Converting NoSQL databases into SQL databases

**Answer: B**

**Q50.** An e-commerce application needs to store shopping cart information for fast retrieval using a cart ID. Which database is suitable?

A. Redis
B. Neo4j
C. Cassandra
D. MongoDB

**Answer: A - Redis**

**Q51.** An e-commerce application needs to store product details, descriptions, specifications and images metadata in flexible documents. Which database is suitable?

A. Neo4j
B. MongoDB
C. Redis
D. Cassandra

**Answer: B - MongoDB**

**Q52.** An e-commerce application needs to store millions of customer activity events. Which database is a suitable choice?

A. Neo4j
B. Redis
C. Cassandra
D. SQLite

**Answer: C - Cassandra**

**Q53.** An e-commerce application needs to recommend

### User

give simple level ony not advanced moderate quiz on above topics give 60 qns on this

### ChatGPT

# Big Data and NoSQL - 60 MCQs

(Simple to Moderate Level)

**Topics covered:** Big Data characteristics, NoSQL database types, SQL vs NoSQL, database selection, polyglot persistence, CAP theorem, strong consistency and eventual consistency.

## Section A - Big Data Characteristics (8 Questions)

**Q1.** Which Big Data characteristic refers to the amount of data generated and stored?

A. Variety
B. Volume
C. Velocity
D. Veracity

**Answer: B - Volume**

**Q2.** Which characteristic refers to the speed at which data is generated?

A. Velocity
B. Variety
C. Value
D. Veracity

**Answer: A - Velocity**

**Q3.** A company collects images, videos, audio files and text documents. Which characteristic is represented?

A. Volume
B. Velocity
C. Variety
D. Value

**Answer: C - Variety**

**Q4.** Incorrect, duplicate and inconsistent data represent which characteristic?

A. Value
B. Veracity
C. Volume
D. Velocity

**Answer: B - Veracity**

**Q5.** Extracting useful business insights from data represents:

A. Value
B. Variety
C. Volume
D. Velocity

**Answer: A - Value**

**Q6.** A website receives millions of customer transactions every day. Which characteristic is represented by the large quantity of transactions?

A. Variety
B. Veracity
C. Volume
D. Value

**Answer: C - Volume**

**Q7.** Processing real-time stock market updates represents:

A. Volume
B. Velocity
C. Variety
D. Veracity

**Answer: B - Velocity**

**Q8.** Which Big Data characteristic focuses on the trustworthiness and accuracy of data?

A. Value
B. Volume
C. Variety
D. Veracity

**Answer: D - Veracity**

## Section B - Types of NoSQL Databases (20 Questions)

**Q9.** How many major types of NoSQL databases are commonly discussed?

A. Two
B. Three
C. Four
D. Five

**Answer: C - Four**

**Q10.** Which of the following is a key-value database?

A. MongoDB
B. Redis
C. Neo4j
D. Cassandra

**Answer: B - Redis**

**Q11.** Which of the following is a document-oriented database?

A. MongoDB
B. Redis
C. Neo4j
D. Cassandra

**Answer: A - MongoDB**

**Q12.** Which of the following is a column-family database?

A. Redis
B. MongoDB
C. Cassandra
D. Neo4j

**Answer: C - Cassandra**

**Q13.** Which of the following is a graph database?

A. MongoDB
B. Redis
C. Cassandra
D. Neo4j

**Answer: D - Neo4j**

**Q14.** Which database type stores information as key-value pairs?

A. Graph database
B. Key-value database
C. Document database
D. Column-family database

**Answer: B**

**Q15.** Which database type stores information in documents?

A. Document-oriented database
B. Graph database
C. Key-value database
D. Column-family database

**Answer: A**

**Q16.** Which database type stores information using nodes and relationships?

A. Key-value
B. Document
C. Graph
D. Column-family

**Answer: C**

**Q17.** Which database type organizes data using column families?

A. Document
B. Column-family
C. Graph
D. Key-value

**Answer: B**

**Q18.** Which database is commonly used for caching?

A. Neo4j
B. Cassandra
C. Redis
D. MongoDB

**Answer: C - Redis**

**Q19.** Which database is suitable for storing customer details in JSON-like documents?

A. MongoDB
B. Redis
C. Neo4j
D. Cassandra

**Answer: A - MongoDB**

**Q20.** Which database is suitable for storing social media relationships?

A. Redis
B. MongoDB
C. Cassandra
D. Neo4j

**Answer: D - Neo4j**

**Q21.** Which database is suitable for storing large amounts of distributed IoT data?

A. Neo4j
B. Cassandra
C. Redis
D. MongoDB

**Answer: B - Cassandra**

**Q22.** Which database is suitable for storing shopping cart information using a cart ID?

A. Redis
B. Neo4j
C. Cassandra
D. MongoDB

**Answer: A - Redis**

**Q23.** Which database is suitable for storing product descriptions with different attributes?

A. Neo4j
B. Redis
C. MongoDB
D. Cassandra

**Answer: C - MongoDB**

**Q24.** Which database is suitable for finding relationships between people in a social network?

A. Redis
B. Cassandra
C. MongoDB
D. Neo4j

**Answer: D - Neo4j**

**Q25.** Which database is commonly used for large-scale, write-intensive applications?

A. Cassandra
B. Neo4j
C. Redis
D. MongoDB

**Answer: A - Cassandra**

**Q26.** Which database model is most suitable when data is accessed mainly through a unique key?

A. Graph
B. Key-value
C. Document
D. Column-family

**Answer: B - Key-value**

**Q27.** Which database type is most suitable for storing nested objects and arrays?

A. Graph
B. Key-value
C. Document
D. Column-family

**Answer: C - Document**

**Q28.** Which database type is best suited for data with many interconnected relationships?

A. Key-value
B. Graph
C. Document
D. Column-family

**Answer: B - Graph**

## Section C - Characteristics of NoSQL Databases (10 Questions)

**Q29.** What is the main characteristic of a document-oriented database?

A. Data is stored only in tables.
B. Data is stored as documents.
C. Data is stored only as key-value pairs.
D. Data is stored only as nodes and edges.

**Answer: B**

**Q30.** What does flexible schema mean?

A. Every document must have identical fields.
B. Different documents can have different fields.
C. Documents cannot contain new fields.
D. All documents must have the same number of attributes.

**Answer: B**

**Q31.** Which feature makes document databases useful for rapid application development?

A. Flexible document structure
B. Mandatory fixed schema
C. Mandatory relational joins
D. Centralized storage only

**Answer: A**

**Q32.** Which database type is suitable for storing product information that is frequently read and rarely updated?

A. Graph database
B. Document-oriented database
C. Key-value database only
D. Column-family database only

**Answer: B**

**Q33.** Which database type represents relationships directly?

A. Key-value
B. Document
C. Graph
D. Column-family

**Answer: C**

**Q34.** Why are graph databases useful for social networking applications?

A. They store only numbers.
B. They represent people and their connections.
C. They store only key-value pairs.
D. They do not support relationships.

**Answer: B**

**Q35.** Which database type is commonly suitable for fast session retrieval?

A. Key-value
B. Graph
C. Document
D. Column-family

**Answer: A**

**Q36.** Which database type is commonly suitable for distributed data storage across multiple machines?

A. Only relational databases
B. NoSQL databases such as Cassandra
C. Only graph databases
D. Only key-value databases

**Answer: B**

**Q37.** Which statement about NoSQL databases is correct?

A. All NoSQL databases use the same data model.
B. NoSQL databases support different data models.
C. NoSQL databases cannot store structured data.
D. NoSQL databases cannot perform queries.

**Answer: B**

**Q38.** Which statement about ACID properties is correct?

A. Only SQL databases support ACID.
B. NoSQL databases never support ACID.
C. Some NoSQL databases, such as MongoDB and Neo4j, support ACID transactions.
D. ACID is applicable only to Redis.

**Answer: C**

## Section D - SQL vs NoSQL (8 Questions)

**Q39.** SQL databases generally follow which type of schema?

A. Flexible schema
B. Predefined or fixed schema
C. No schema
D. Graph schema only

**Answer: B**

**Q40.** NoSQL databases are generally known for:

A. Flexible data models
B. Mandatory fixed tables
C. Only relational storage
D. Mandatory joins

**Answer: A**

**Q41.** Adding more RAM and CPU to an existing server is called:

A. Horizontal scaling
B. Vertical scaling
C. Distributed scaling
D. Data replication

**Answer: B - Vertical scaling**

**Q42.** Adding more servers to increase system capacity is called:

A. Vertical scaling
B. Horizontal scaling
C. Centralized scaling
D. Schema scaling

**Answer: B - Horizontal scaling**

**Q43.** Which statement about data storage is correct?

A. SQL databases can store only small amounts of data.
B. NoSQL databases can store only large amounts of data.
C. Both SQL and NoSQL databases can store large amounts of data.
D. SQL databases cannot store structured data.

**Answer: C**

**Q44.** Which approach is commonly associated with distributed NoSQL databases?

A. Storing data on only one machine
B. Distributing data across multiple machines
C. Avoiding data replication completely
D. Using only centralized storage

**Answer: B**

**Q45.** Which statement about scalability is correct?

A. SQL databases support only vertical scaling.
B. NoSQL databases support only horizontal scaling.
C. Both SQL and NoSQL systems can support different scaling approaches.
D. Neither SQL nor NoSQL databases support scaling.

**Answer: C**

**Q46.** Which database type is generally preferred when an application requires complex relational queries and structured data?

A. Relational SQL database
B. Key-value database
C. Graph database only
D. Document database only

**Answer: A**

## Section E - Polyglot Persistence and CAP Theorem (14 Questions)

**Q47.** What is polyglot persistence?

A. Using only one database for all applications
B. Using different database technologies for different requirements
C. Using only relational databases
D. Storing all data in one collection

**Answer: B**

**Q48.** An e-commerce application uses Redis for shopping carts, MongoDB for product details and Cassandra for customer activity data. What is this approach called?

A. Normalization
B. Polyglot persistence
C. Vertical scaling
D. Data compression

**Answer: B**

**Q49.** Which database is suitable for storing shopping cart information?

A. Redis
B. Neo4j
C. Cassandra
D. MongoDB

**Answer: A - Redis**

**Q50.** Which database is suitable for storing product catalog information?

A. Neo4j
B. MongoDB
C. Redis
D. Cassandra

**Answer: B - MongoDB**

**Q51.** Which database is suitable for storing large volumes of customer activity events?

A. Neo4j
B. Redis
C. Cassandra
D. SQLite

**Answer: C - Cassandra**

**Q52.** Which database is suitable for storing customer relationships and product recommendations based on connections?

A. Redis
B. Cassandra
C. MongoDB
D. Neo4j

**Answer: D - Neo4j**

**Q53.** CAP theorem was proposed by:

A. Edgar Codd
B. Eric Brewer
C. James Gosling
D. Dennis Ritchie

**Answer: B - Eric Brewer**

**Q54.** What does C represent in CAP theorem?

A. Concurrency
B. Consistency
C. Centralization
D. Compression

**Answer: B - Consistency**

**Q55.** What does A represent in CAP theorem?

A. Availability
B. Atomicity
C. Accuracy
D. Authorization

**Answer: A - Availability**

**Q56.** What does P represent in CAP theorem?

A. Performance
B. Persistence
C. Partition Tolerance
D. Processing

**Answer: C - Partition Tolerance**

**Q57.** According to CAP theorem, during a network partition, a distributed system must choose between:

A. Volume and Velocity
B. Consistency and Availability
C. Atomicity and Durability
D. Variety and Value

**Answer: B**

**Q58.** Which database is commonly classified as AP in basic CAP-theorem examples?

A. Cassandra
B. MongoDB replica set
C. Neo4j
D. Traditional single-server SQL database

**Answer: A - Cassandra**

**Q59.** Which database is commonly classified as CP in basic CAP-theorem examples?

A. Cassandra
B. MongoDB replica set
C. Traditional single-server SQL database
D. A non-distributed database

**Answer: B - MongoDB replica set**

**Q60.** What is eventual consistency?

A. All replicas must always contain identical data immediately.
B. Replicas may temporarily contain different values but eventually become consistent.
C. Data is never replicated.
D. Every read must always return the latest value.

**Answer: B - Replicas eventually become consistent**

---

## Important concepts to remember for the exam

| Concept | Remember |
| --- | --- |
| Volume | Amount of data |
| Velocity | Speed of data generation |
| Variety | Different data formats |
| Veracity | Accuracy and trustworthiness |
| Value | Useful insights |
| Redis | Key-value |
| MongoDB | Document |
| Cassandra | Column-family |
| Neo4j | Graph |
| Flexible schema | Documents can have different fields |
| Vertical scaling | Increase machine capacity |
| Horizontal scaling | Add more machines |
| Polyglot persistence | Multiple database types in one application |
| CAP - C | Consistency |
| CAP - A | Availability |
| CAP - P | Partition tolerance |
| AP | Availability prioritized during partition |
| CP | Consistency prioritized during partition |
| Eventual consistency | Replicas converge over time |

**Exam note:** CAP classifications such as Cassandra = AP and MongoDB = CP are common introductory examples. Actual consistency and availability behavior depends on database configuration and deployment.
 
