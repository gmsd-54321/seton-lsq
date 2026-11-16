
# Generate DBMS MCQs

### User

give advanced expert level 60 mcq question not in quiz interface fundamental principles of dbms of data independence integrity, limitation of flat file, about dbms, functions of dbms, types of database hirearchial network no sql relational, relational model intro attirbute tuple relation, cardinality degree, find cardinality degree, domain,null, data integrity: entitty integrity, domain integrity, reference integrity, candidate key given scenarios find suitable candidate key, primary key, foreign key, given  multiple table find candidate key, find candidate key foreign key primary key of given tables dont give in quiz interface given 3-4 tables find primary key for those tables

### ChatGPT

# DBMS Fundamentals - 60 Advanced & Expert-Level MCQs

**Difficulty:** Advanced to Expert
**Level:** 2-year SQL Developer / DBMS technical assessment
**Format:** Questions with four options, followed immediately by the correct answer and explanation. No quiz interface.

**Topics covered:**

1. Fundamental principles of DBMS
2. Data independence
3. Data integrity
4. Limitations of flat-file systems
5. DBMS functions and responsibilities
6. Hierarchical, network, relational and NoSQL databases
7. Relational model: relation, tuple, attribute, domain
8. Cardinality and degree
9. NULL values
10. Entity, domain and referential integrity
11. Candidate keys, primary keys and foreign keys
12. Identifying keys across multiple related tables

---

## Section 1: DBMS Fundamentals and Data Independence

### Q1. A company changes its database storage mechanism from sequential file storage to indexed storage. The application queries remain unchanged. Which DBMS principle does this demonstrate?

A. Logical data independence
B. Physical data independence
C. Referential integrity
D. Domain independence

**Answer: B. Physical data independence**

**Explanation:** Physical data independence allows changes to the internal storage structure without requiring modifications to the conceptual schema or application programs.

Examples:

- Changing file organization.
- Creating or removing indexes.
- Changing storage devices.
- Changing data access methods.

### Q2. A database administrator adds a new attribute `middle_name` to the conceptual schema. Existing applications that do not use this attribute continue working without modification. Which concept is demonstrated?

A. Physical data independence
B. Logical data independence
C. Entity integrity
D. Data redundancy

**Answer: B. Logical data independence**

**Explanation:** Logical data independence allows modifications to the conceptual schema without requiring changes to external views or application programs, provided their required interfaces remain unaffected.

### Q3. Which statement correctly distinguishes physical and logical data independence?

A. Physical independence protects external schemas from conceptual changes.
B. Logical independence protects the conceptual schema from internal storage changes.
C. Physical independence concerns internal schema changes, whereas logical independence concerns conceptual schema changes.
D. Both refer exclusively to changes in storage devices.

**Answer: C**

**Explanation:**

- Physical: Internal schema changes without affecting conceptual schema.
- Logical: Conceptual schema changes without affecting external schemas.

Logical data independence is generally harder to achieve than physical data independence.

### Q4. Consider the following scenario:

A database contains an EMPLOYEE table. Initially, all employee details are stored in one physical file. Later, the DBA splits the storage across multiple physical files, but users continue accessing the same EMPLOYEE table.

Which schema level has primarily changed?

A. External
B. Conceptual
C. Internal
D. View

**Answer: C. Internal**

**Explanation:** The internal schema defines how data is physically stored, including file organization, storage structures and indexes.

### Q5. Which of the following is NOT a primary objective of a DBMS?

A. Reducing unnecessary data redundancy
B. Enforcing data integrity
C. Providing controlled concurrent access
D. Eliminating the need for all database administration

**Answer: D**

**Explanation:** DBMS simplifies database administration but does not eliminate the need for it.

### Q6. Two users simultaneously update the same bank account. The DBMS ensures that the final balance is correct and that one update does not accidentally overwrite another.

Which DBMS function is primarily responsible?

A. Data definition
B. Concurrency control
C. Data abstraction
D. Schema mapping

**Answer: B. Concurrency control**

**Explanation:** Concurrency control coordinates simultaneous transactions and prevents problems such as lost updates.

### Q7. A database administrator grants SELECT permission to one employee and UPDATE permission to another.

Which DBMS function is being used?

A. Transaction management
B. Authorization and access control
C. Data independence
D. Query optimization

**Answer: B. Authorization and access control**

### Q8. A database crashes during a transaction. After restarting, the DBMS restores the database to a consistent state using its recovery mechanisms.

Which DBMS responsibility is involved?

A. Data abstraction
B. Backup and recovery
C. Schema definition
D. Domain enforcement

**Answer: B. Backup and recovery**

### Q9. Which situation best demonstrates the advantage of a DBMS over a traditional flat-file system?

A. Each department maintains its own independent customer file.
B. Every application maintains its own duplicate employee records.
C. Multiple applications access a centrally managed customer database with controlled permissions.
D. Each user manually synchronizes their local files.

**Answer: C**

### Q10. Which statement about DBMS and data redundancy is correct?

A. A DBMS guarantees zero data redundancy.
B. A DBMS can control and minimize unnecessary redundancy but may intentionally maintain redundancy.
C. A DBMS always duplicates every record.
D. Redundancy cannot exist in relational databases.

**Answer: B**

**Explanation:** Redundancy may be intentionally introduced for performance, availability or other requirements. A DBMS helps manage it and prevent inconsistencies.

---

## Section 2: Limitations of Flat-File Systems

### Q11. A university maintains student information in three independent files:

- Admission file
- Examination file
- Library file

A student's address changes, but only the admission file gets updated.

Which problem occurs?

A. Insertion anomaly
B. Deletion anomaly
C. Update anomaly
D. Referential integrity

**Answer: C. Update anomaly**

**Explanation:** The same information is stored in multiple places. Updating only one copy creates inconsistent data.

### Q12. A company stores employee and department information in one flat file. A department has been created, but no employees have been assigned to it. The system cannot store the department without entering an employee record.

Which anomaly is demonstrated?

A. Update anomaly
B. Insertion anomaly
C. Deletion anomaly
D. Concurrency anomaly

**Answer: B. Insertion anomaly**

### Q13. Consider this flat-file data:

| Employee_ID | Employee_Name | Department |
| --- | --- | --- |
| 101 | Arun | HR |
| 102 | Banu | IT |
| 103 | Charan | IT |

If employee 102 is the only employee in the Finance department and that employee's record is deleted, the department information is also lost.

Which anomaly is demonstrated?

A. Insertion
B. Update
C. Deletion
D. Domain

**Answer: C. Deletion anomaly**

### Q14. Which is the most accurate explanation of data inconsistency in flat-file systems?

A. Data is always stored in binary format.
B. Different files may contain conflicting values for the same real-world entity.
C. Files cannot store numerical values.
D. Flat files automatically reject duplicate records.

**Answer: B**

### Q15. A company uses multiple independent files. Two users simultaneously modify the same customer's information in separate files. There is no mechanism to coordinate these changes.

Which DBMS capability is missing?

A. Data independence
B. Concurrency control
C. Data definition
D. Domain specification

**Answer: B**

---

## Section 3: Types of Databases

### Q16. An organization stores employee records in a structure where each employee can have only one parent department, and departments form a strict tree hierarchy.

Which database model is most suitable?

A. Network
B. Hierarchical
C. Relational
D. Graph-independent document model

**Answer: B. Hierarchical**

### Q17. In a hierarchical database, which relationship is naturally represented?

A. Many-to-many
B. One-to-many
C. Every entity must have multiple parents
D. Every record must be independent

**Answer: B. One-to-many**

**Explanation:** A child record generally has one parent, while a parent can have multiple children.

### Q18. A student can enroll in multiple courses, and each course can contain multiple students. The database uses records connected through multiple ownership relationships.

Which traditional database model supports this structure?

A. Hierarchical
B. Network
C. Flat-file
D. Key-value

**Answer: B. Network**

### Q19. Which statement correctly differentiates hierarchical and network database models?

A. Hierarchical supports multiple parents, while network supports only one parent.
B. Hierarchical uses a tree structure, while network allows records to have multiple relationships.
C. Both models exclusively use tables.
D. Network databases cannot represent one-to-many relationships.

**Answer: B**

### Q20. A company needs to store customer profiles with different attributes for different customers. Some documents contain social media details, while others contain payment preferences.

Which NoSQL database type is most suitable?

A. Key-value
B. Document-oriented
C. Hierarchical
D. Relational only

**Answer: B. Document-oriented**

**Explanation:** Document databases store semi-structured records, commonly using JSON-like documents. Different documents can have different fields.

### Q21. Which NoSQL database type is best suited for storing session information using a unique session ID and its associated value?

A. Graph database
B. Document database
C. Key-value database
D. Relational database

**Answer: C. Key-value database**

### Q22. A social networking application needs to efficiently query relationships such as:

- Person A follows Person B.
- Person B is friends with Person C.
- Person C works with Person D.

Which database model is most appropriate?

A. Hierarchical
B. Graph
C. Key-value
D. Flat-file

**Answer: B. Graph**

### Q23. A distributed system needs to store huge volumes of data across multiple machines, with flexible schemas and horizontal scalability.

Which category is most commonly associated with this requirement?

A. NoSQL
B. Hierarchical only
C. Flat-file only
D. Network database only

**Answer: A. NoSQL**

### Q24. Which statement about relational databases is correct?

A. Relationships are represented exclusively through physical pointers.
B. Data is represented using relations, and relationships between tables can be represented using keys.
C. Every table must contain exactly one row.
D. A relational database cannot enforce referential integrity.

**Answer: B**

### Q25. Which of the following is NOT a defining characteristic of the relational model?

A. Data is represented as relations.
B. Attributes have associated domains.
C. Tuples represent rows.
D. Every relationship must be represented using a tree hierarchy.

**Answer: D**

---

## Section 4: Relational Model - Relations, Attributes, Tuples, Cardinality and Degree

Consider the following EMPLOYEE relation for Q26-Q30.

| Emp_ID | Emp_Name | Department | Salary | City |
| --- | --- | --- | --- | --- |
| 101 | Arun | IT | 50000 | Chennai |
| 102 | Banu | HR | 45000 | Bengaluru |
| 103 | Charan | IT | 55000 | Chennai |
| 104 | Divya | Finance | 60000 | Hyderabad |
| 105 | Ezhil | HR | 48000 | Chennai |

### Q26. What is the cardinality of the EMPLOYEE relation?

A. 4
B. 5
C. 6
D. 25

**Answer: B. 5**

**Explanation:** Cardinality is the number of tuples (rows).

### Q27. What is the degree of the EMPLOYEE relation?

A. 4
B. 5
C. 6
D. 10

**Answer: B. 5**

**Explanation:** Degree is the number of attributes (columns).

### Q28. If two additional employee records are inserted, what happens to cardinality and degree?

A. Cardinality increases by 2; degree remains unchanged.
B. Degree increases by 2; cardinality remains unchanged.
C. Both increase by 2.
D. Neither changes.

**Answer: A**

### Q29. If a new attribute `Email` is added to the EMPLOYEE relation, what happens?

A. Cardinality increases by 1.
B. Degree increases by 1.
C. Cardinality decreases by 1.
D. Degree remains unchanged.

**Answer: B**

### Q30. Which statement about a relation in the classical relational model is correct?

A. Duplicate tuples are permitted.
B. Tuple order determines the meaning of the relation.
C. Attribute order has logical significance.
D. A relation is mathematically treated as a set of tuples.

**Answer: D**

**Explanation:** A classical relation is a set of tuples. Therefore, duplicate tuples are not permitted, and tuple ordering is irrelevant.

### Q31. A STUDENT relation contains 100 rows and 8 columns. The database administrator deletes 20 student records and adds 3 new attributes.

What is the resulting cardinality and degree?

A. 80 and 11
B. 103 and 8
C. 80 and 8
D. 100 and 11

**Answer: A. 80 and 11**

### Q32. Consider the following relation:

| Product_ID | Product_Name | Price |
| --- | --- | --- |
| P1 | Mouse | 500 |
| P2 | Keyboard | 800 |
| P3 | Monitor | 800 |
| P4 | Mouse | 500 |

Which statement is correct?

A. Cardinality is 3 because duplicate values exist.
B. Cardinality is 4 because all four tuples are distinct.
C. Degree is 4.
D. Degree is 2 because Product_Name has duplicate values.

**Answer: B**

**Explanation:** Even though some attribute values repeat, the complete tuples are distinct because Product_ID differs.

### Q33. The domain of an attribute `Age` is defined as integers from 18 to 60. Which value violates domain integrity?

A. 18
B. 45
C. 60
D. 61

**Answer: D**

### Q34. Which statement about NULL in a relational database is correct?

A. NULL always means zero.
B. NULL always means an empty string.
C. NULL represents missing, unknown or inapplicable information.
D. NULL is equivalent to FALSE.

**Answer: C**

### Q35. A table contains 10 rows. The `Salary` column has NULL values in 3 rows. What is the result of `COUNT(Salary)` and `COUNT(*)`?

A. 10 and 10
B. 7 and 10
C. 7 and 7
D. 10 and 7

**Answer: B**

**Explanation:**

- `COUNT(Salary)` counts non-NULL values.
- `COUNT(*)` counts all rows.

---

## Section 5: Data Integrity Constraints

### Q36. A STUDENT table has `Student_ID` as its primary key. A user attempts to insert two records with the same Student_ID.

Which integrity constraint prevents this?

A. Domain integrity
B. Entity integrity
C. Referential integrity
D. User-defined integrity

**Answer: B. Entity integrity**

**Explanation:** A primary key must be unique and cannot contain NULL values.

### Q37. A foreign key in the ORDER table references CUSTOMER(Customer_ID). A user attempts to insert an order with Customer_ID = 999, but no such customer exists.

Which constraint is violated?

A. Entity integrity
B. Domain integrity
C. Referential integrity
D. Candidate key constraint

**Answer: C. Referential integrity**

### Q38. A table has a `Gender` attribute whose permitted values are `Male`, `Female` and `Other`. A user inserts `Unknown`.

Which integrity constraint is violated?

A. Entity integrity
B. Referential integrity
C. Domain integrity
D. Primary key integrity

**Answer: C**

### Q39. Which statement regarding a foreign key is correct?

A. A foreign key must always be unique.
B. A foreign key must always be NOT NULL.
C. A foreign key can contain duplicate values.
D. A foreign key must always be the primary key of its own table.

**Answer: C**

**Explanation:** Multiple records can reference the same parent record. A foreign key may also contain NULL if the constraint permits it.

### Q40. Consider the following table:

**EMPLOYEE**

| Emp_ID | Emp_Name | Manager_ID |
| --- | --- | --- |
| 101 | Arun | NULL |
| 102 | Banu | 101 |
| 103 | Charan | 101 |
| 104 | Divya | 102 |

`Manager_ID` references `Emp_ID` in the same table.

Which statement is correct?

A. Manager_ID is a primary key.
B. Manager_ID is a self-referencing foreign key.
C. Emp_ID is a foreign key.
D. Both columns must contain unique values.

**Answer: B**

### Q41. Which statement about foreign key NULL values is correct?

A. A foreign key cannot contain NULL under any circumstances.
B. NULL in a foreign key necessarily violates referential integrity.
C. A nullable foreign key can contain NULL without referencing a parent row.
D. A foreign key containing NULL automatically becomes a candidate key.

**Answer: C**

### Q42. A table has a primary key consisting of `Country_Code` and `Passport_Number`. Which statement is correct?

A. Both columns must independently be unique.
B. Only the combination must be unique, and neither column can be NULL.
C. Either column can contain NULL.
D. The combination can contain duplicate values.

**Answer: B**

---

## Section 6: Candidate Key, Primary Key and Foreign Key - Scenario-Based

### Q43. A university maintains the following STUDENT table:

| Student_ID | Email | Aadhaar_No | Name |
| --- | --- | --- | --- |
| 101 | a@gmail.com | 12345 | Arun |
| 102 | b@gmail.com | 67890 | Banu |
| 103 | c@gmail.com | 45678 | Charan |

Business rules:

- Student_ID is unique.
- Email is unique.
- Aadhaar_No is unique.
- All three attributes are mandatory.

Which attributes are candidate keys?

A. Student_ID only
B. Email only
C. Aadhaar_No only
D. Student_ID, Email and Aadhaar_No

**Answer: D**

**Explanation:** Each attribute independently identifies a tuple and is minimal. Therefore, all three are candidate keys.

### Q44. Based on Q43, the DBA selects Student_ID as the primary key. What is the status of Email and Aadhaar_No?

A. Foreign keys
B. Alternate keys
C. Composite keys
D. Non-key attributes

**Answer: B. Alternate keys**

### Q45. Consider the following EMPLOYEE table:

| Employee_ID | Email | Phone | Name |
| --- | --- | --- | --- |
| 1 | a@gmail.com | 9876 | Arun |
| 2 | b@gmail.com | 9877 | Banu |
| 3 | c@gmail.com | 9878 | Charan |

Business rules:

- Employee_ID is unique.
- Email is unique.
- Phone is not unique.
- Name is not unique.

Which set contains all candidate keys?

A. Employee_ID
B. Email
C. Employee_ID and Email
D. Employee_ID, Email and Phone

**Answer: C**

### Q46. Consider a table containing the following attributes:

`Student_ID, Course_ID, Student_Name, Course_Name, Grade`

Business rules:

- A student can enroll in multiple courses.
- A course can contain multiple students.
- A student receives exactly one grade for each course.

What is the most appropriate candidate key?

A. Student_ID
B. Course_ID
C. Student_ID + Course_ID
D. Student_Name + Course_Name

**Answer: C**

**Explanation:** Neither Student_ID nor Course_ID uniquely identifies an enrollment. Their combination does.

### Q47. Consider a table:

`ORDER_ITEM(Order_ID, Product_ID, Quantity, Price)`

Business rules:

- An order can contain multiple products.
- A product can appear in multiple orders.
- A product appears at most once in a particular order.

What is the candidate key?

A. Order_ID
B. Product_ID
C. Order_ID + Product_ID
D. Quantity + Price

**Answer: C**

### Q48. A database table has these attributes:

`Vehicle_ID, Registration_Number, Chassis_Number, Model`

Business rules:

- Vehicle_ID is unique.
- Registration_Number is unique.
- Chassis_Number is unique.
- All are mandatory.

Which is a valid choice of primary key?

A. Model
B. Vehicle_ID
C. Registration_Number + Chassis_Number
D. Model + Vehicle_ID

**Answer: B**

**Explanation:** Vehicle_ID is a minimal candidate key. Registration_Number and Chassis_Number are also candidate keys and could alternatively be chosen.

### Q49. A relation contains:

`A, B, C, D`

Given functional dependencies:

- A → B
- B → C
- C → D

Which is the candidate key?

A. A
B. B
C. C
D. D

**Answer: A**

**Explanation:** A determines B, B determines C, and C determines D. Therefore, A determines every attribute. A is minimal.

### Q50. Consider the following table:

`EMPLOYEE(Emp_ID, Email, Dept_ID, Name)`

Business rules:

- Emp_ID uniquely identifies each employee.
- Email is unique.
- Dept_ID can repeat.
- Every Dept_ID must reference an existing department.

Which statement is correct?

A. Emp_ID and Dept_ID are candidate keys.
B. Email and Dept_ID are candidate keys.
C. Emp_ID and Email are candidate keys; Dept_ID is a foreign key.
D. Dept_ID is the primary key.

**Answer: C**

---

## Section 7: Identify Primary Keys and Foreign Keys Across Multiple Tables

For Q51-Q60, analyze the following four-table database.

### Table 1: DEPARTMENT

| Dept_ID | Dept_Name | Location |
| --- | --- | --- |
| D01 | IT | Chennai |
| D02 | HR | Bengaluru |
| D03 | Finance | Hyderabad |

Business rules:

- Dept_ID is unique.
- Dept_Name is unique.

### Table 2: EMPLOYEE

| Emp_ID | Emp_Name | Email | Dept_ID |
| --- | --- | --- | --- |
| E101 | Arun | a@gmail.com | D01 |
| E102 | Banu | b@gmail.com | D02 |
| E103 | Charan | c@gmail.com | D01 |
| E104 | Divya | d@gmail.com | D03 |

Business rules:

- Emp_ID is unique.
- Email is unique.
- Each employee belongs to exactly one department.

### Table 3: PROJECT

| Project_ID | Project_Name | Dept_ID |
| --- | --- | --- |
| P01 | ERP | D01 |
| P02 | Payroll | D02 |
| P03 | Analytics | D01 |

Business rules:

- Project_ID is unique.
- Project_Name is unique.
- Each project belongs to exactly one department.

### Table 4: EMPLOYEE_PROJECT

| Emp_ID | Project_ID | Hours |
| --- | --- | --- |
| E101 | P01 | 20 |
| E101 | P03 | 15 |
| E102 | P02 | 30 |
| E103 | P01 | 25 |
| E104 | P03 | 10 |

Business rules:

- An employee can work on multiple projects.
- A project can have multiple employees.
- An employee can be assigned to a particular project only once.

### Q51. What is the primary key of DEPARTMENT?

A. Dept_Name
B. Dept_ID
C. Location
D. Dept_ID + Dept_Name

**Answer: B. Dept_ID**

**Explanation:** Dept_ID uniquely identifies each department and is minimal.

### Q52. Which columns are candidate keys in DEPARTMENT?

A. Dept_ID only
B. Dept_Name only
C. Dept_ID and Dept_Name
D. Dept_ID and Location

**Answer: C**

**Explanation:** Both Dept_ID and Dept_Name independently identify each department based on the stated business rules.

### Q53. What is the primary key of EMPLOYEE?

A. Emp_Name
B. Email
C. Emp_ID
D. Dept_ID

**Answer: C. Emp_ID**

**Explanation:** Emp_ID uniquely identifies an employee. Email is an alternate candidate key.

### Q54. Identify all candidate keys of EMPLOYEE.

A. Emp_ID only
B. Email only
C. Emp_ID and Email
D. Emp_ID, Email and Dept_ID

**Answer: C**

### Q55. Which column in EMPLOYEE is a foreign key?

A. Emp_ID
B. Emp_Name
C. Email
D. Dept_ID

**Answer: D. Dept_ID**

**Explanation:** EMPLOYEE.Dept_ID references DEPARTMENT.Dept_ID.

### Q56. What is the primary key of PROJECT?

A. Project_Name
B. Project_ID
C. Dept_ID
D. Dept_ID + Project_ID

**Answer: B. Project_ID**

**Explanation:** Project_ID is the selected primary key. Project_Name is an alternate candidate key.

### Q57. Which column in PROJECT is a foreign key?

A. Project_ID
B. Project_Name
C. Dept_ID
D. Both Project_ID and Project_Name

**Answer: C. Dept_ID**

### Q58. What is the most appropriate primary key for EMPLOYEE_PROJECT?

A. Emp_ID
B. Project_ID
C. Emp_ID + Project_ID
D. Emp_ID + Hours

**Answer: C**

**Explanation:** One employee can participate in multiple projects, and one project can have multiple employees.

The combination Emp_ID + Project_ID uniquely identifies an assignment.

### Q59. Identify all foreign keys in EMPLOYEE_PROJECT.

A. Emp_ID only
B. Project_ID only
C. Emp_ID and Project_ID
D. Hours and Emp_ID

**Answer: C**

**Explanation:**

- EMPLOYEE_PROJECT.Emp_ID references EMPLOYEE.Emp_ID.
- EMPLOYEE_PROJECT.Project_ID references PROJECT.Project_ID.

Both are foreign keys and together form the composite primary key.

### Q60. Consider the following statements about the four tables.

1. DEPARTMENT.Dept_ID is a primary key.
2. EMPLOYEE.Dept_ID is a foreign key.
3. PROJECT.Dept_ID is a foreign key.
4. EMPLOYEE_PROJECT.Emp_ID + Project_ID is a composite primary key.
5. EMPLOYEE.Email is an alternate key.
6. EMPLOYEE_PROJECT.Hours is a foreign key.

Which option contains all correct statements?

A. 1, 2, 3 and 4 only
B. 1, 2, 3, 4 and 5 only
C. 1, 2, 3, 4, 5 and 6
D. 2, 3, 5 and 6 only

**Answer: B. 1, 2, 3, 4 and 5 only**

**Explanation:**

| Statement | Result | Reason |
| --- | --- | --- |
| 1 | Correct | Dept_ID uniquely identifies departments |
| 2 | Correct | References DEPARTMENT |
| 3 | Correct | References DEPARTMENT |
| 4 | Correct | Composite primary key |
| 5 | Correct | Email is a candidate key not selected as primary key |
| 6 | Incorrect | Hours is an ordinary attribute |

---

## Final Answer Key - All 60 Questions

**1-15**

B B C C D B B B C B C B B B B

**16-30**

B B B B B C B A B B B D D C D

**31-45**

A B D C B B C C B B C C D C C

**46-60**

C C B A C B C C C B C B C C B

## Important expert-level concepts to remember

| Concept | Key point |
| --- | --- |
| Cardinality | Number of rows/tuples |
| Degree | Number of columns/attributes |
| Candidate key | Minimal superkey |
| Primary key | Selected candidate key |
| Alternate key | Candidate key not selected as primary |
| Composite key | Key containing multiple attributes |
| Foreign key | Attribute(s) referencing a candidate/unique key in another or same table |
| Entity integrity | Primary key must be unique and NOT NULL |
| Domain integrity | Values must belong to the permitted domain |
| Referential integrity | Foreign key must reference an existing eligible parent key or be NULL if permitted |
| Physical independence | Internal schema changes |
| Logical independence | Conceptual schema changes |
| Hierarchical DB | Tree-based parent-child structure |
| Network DB | Multiple interconnected record relationships |
| Relational DB | Relations (tables), tuples and attributes |
| NoSQL | Non-relational database family |

**Important exam trap:** A foreign key does not have to be unique. A candidate key must be minimal, whereas a superkey need only uniquely identify records. A primary key is always a candidate key, but not every candidate key is a primary key.

### User

give another 60 tricky advanced

### ChatGPT

# DBMS Fundamentals - Next 60 Tricky Advanced & Expert MCQs

(Advanced-Expert) (Set 2 · Questions 61-120)

This set focuses on tricky scenarios, closely related options, identifying keys from business rules, multiple-table relationships, NULL edge cases, integrity violations and relational model concepts.

**Format:** Four options, correct answer and explanation immediately after each question. No quiz interface.

---

## Section 1: DBMS Fundamentals, Data Independence and Architecture

### Q61. A database administrator changes a table's physical storage from an unordered heap file to a B+ tree-organized storage structure. The application programs continue working without modification.

Which statement is correct?

A. External schema has changed.
B. Conceptual schema has changed.
C. Internal schema has changed.
D. Logical data independence has been violated.

**Answer: C. Internal schema has changed.**

**Explanation:** Physical storage organization belongs to the internal level. Changing it without affecting higher levels demonstrates physical data independence.

### Q62. A database designer splits a single CUSTOMER table into CUSTOMER and CUSTOMER_CONTACT tables. Existing users continue accessing a view that presents the original combined structure.

Which concept is demonstrated?

A. Physical data independence
B. Logical data independence
C. Entity integrity
D. Domain integrity

**Answer: B. Logical data independence**

**Explanation:** The conceptual schema has changed, but the external view continues providing the original representation.

### Q63. Which change is most likely to violate physical data independence?

A. Creating an additional index on EMPLOYEE.
B. Moving database files to a different storage device.
C. Changing a table's physical file organization.
D. Changing the column names in an application-facing view.

**Answer: D**

**Explanation:** Changing an application-facing view can affect external schemas and applications. The other changes are physical-level changes.

### Q64. A DBMS provides multiple users with different views of the same database. Which DBMS objective is primarily achieved?

A. Data abstraction and security
B. Data duplication
C. Physical redundancy
D. File independence only

**Answer: A**

### Q65. A transaction transfers ₹5,000 from account A to account B. The system deducts ₹5,000 from A but crashes before crediting B.

Which ACID property is primarily responsible for ensuring that the transaction is not partially committed?

A. Consistency
B. Isolation
C. Atomicity
D. Durability

**Answer: C. Atomicity**

### Q66. A transaction completes successfully. Immediately afterward, the system loses power. After restarting, the committed transaction's changes are still available.

Which property is demonstrated?

A. Atomicity
B. Consistency
C. Isolation
D. Durability

**Answer: D. Durability**

### Q67. Two users simultaneously book the last available seat on a flight. The DBMS must prevent both transactions from successfully booking the same seat.

Which combination is most relevant?

A. Data abstraction and indexing
B. Concurrency control and integrity constraints
C. Physical data independence and backup
D. Domain integrity and file organization

**Answer: B**

### Q68. A DBMS uses a transaction log to reconstruct committed changes after a crash. Which function is being performed?

A. Query parsing
B. Recovery management
C. Schema mapping
D. Domain validation

**Answer: B**

### Q69. Which statement about logical data independence is most accurate?

A. It guarantees that every conceptual schema change will never affect any application.
B. It allows conceptual changes without affecting external schemas, provided suitable mappings or compatibility are maintained.
C. It concerns only changes to indexes.
D. It means that database users cannot see the conceptual schema.

**Answer: B**

### Q70. A company replaces its DBMS with another DBMS while retaining the same logical database structure. Applications require minimal modifications because they interact through a standard database interface.

Which concept is most closely related?

A. Data abstraction and application/database independence
B. Entity integrity
C. Referential integrity
D. Hierarchical data independence

**Answer: A**

---

## Section 2: Flat Files, DBMS Functions and Database Types

### Q71. An employee's department name is stored in 500 employee records. The department is renamed, but only 300 records are updated.

What is the immediate problem?

A. Insertion anomaly
B. Deletion anomaly
C. Update anomaly and data inconsistency
D. Entity integrity violation

**Answer: C**

### Q72. A company wants to store department information even when the department has no employees. Its current flat-file structure requires an employee record for every department.

Which anomaly prevents this?

A. Update anomaly
B. Insertion anomaly
C. Deletion anomaly
D. Concurrency anomaly

**Answer: B**

### Q73. A customer is the only customer associated with a particular sales representative. Deleting the customer record also removes the only stored information about that representative.

Which anomaly is demonstrated?

A. Insertion
B. Update
C. Deletion
D. Domain

**Answer: C**

### Q74. Which of the following is NOT inherently guaranteed merely because an organization uses a DBMS?

A. Centralized data management
B. Controlled access
C. Elimination of every data inconsistency
D. Transaction management

**Answer: C**

**Explanation:** A DBMS provides mechanisms to maintain consistency, but incorrect schema design, missing constraints and faulty transactions can still cause inconsistent data.

### Q75. A legacy banking application stores records in a structure where every child record has exactly one parent, and navigation follows predefined paths.

Which model is most likely being used?

A. Relational
B. Hierarchical
C. Graph
D. Document

**Answer: B**

### Q76. In a traditional network database, a record can participate in multiple owner-member relationships.

What advantage does this provide over a hierarchical model?

A. It eliminates all parent-child relationships.
B. It naturally supports more complex interconnected relationships.
C. It eliminates the need for record identifiers.
D. It guarantees a relational structure.

**Answer: B**

### Q77. Which pairing is incorrect?

A. Redis - Key-value database
B. MongoDB - Document database
C. Neo4j - Graph database
D. PostgreSQL - Hierarchical database

**Answer: D**

### Q78. A distributed application stores product details as JSON documents. Different products can have different attributes without requiring every document to have identical fields.

Which feature is being used?

A. Fixed relational degree
B. Flexible document schema
C. Hierarchical ownership
D. Strict fixed-width storage

**Answer: B**

### Q79. Which statement about NoSQL databases is correct?

A. NoSQL databases never support transactions.
B. NoSQL databases cannot represent relationships.
C. NoSQL is a broad family of non-relational database systems with different data models and consistency capabilities.
D. Every NoSQL database stores data as key-value pairs only.

**Answer: C**

### Q80. A company stores millions of product reviews. It frequently searches for reviews connected through products, customers and recommendations.

Which database type is most naturally suited to traversing these interconnected relationships?

A. Key-value
B. Graph
C. Flat-file
D. Hierarchical

**Answer: B**

---

## Section 3: Relational Model, Cardinality, Degree and NULL

Consider this relation for Q81-Q85.

**ENROLLMENT**

| Student_ID | Course_ID | Semester | Grade |
| --- | --- | --- | --- |
| S01 | C01 | 1 | A |
| S01 | C02 | 1 | B |
| S02 | C01 | 1 | A |
| S03 | C03 | 2 | NULL |
| S04 | C02 | 1 | C |
| S05 | C03 | 2 | B |

### Q81. What is the cardinality and degree of ENROLLMENT?

A. 4 and 6
B. 6 and 4
C. 5 and 4
D. 6 and 6

**Answer: B. 6 and 4**

### Q82. A new column `Enrollment_Date` is added, and three new enrollment records are inserted. What are the new cardinality and degree?

A. 9 and 5
B. 6 and 7
C. 9 and 4
D. 7 and 5

**Answer: A. 9 and 5**

### Q83. How many non-NULL values exist in the Grade column?

A. 3
B. 4
C. 5
D. 6

**Answer: C. 5**

**Explanation:** There are six tuples, one of which contains NULL in Grade.

### Q84. What is the result of `COUNT(*)` and `COUNT(Grade)`?

A. 6 and 5
B. 5 and 6
C. 6 and 6
D. 5 and 5

**Answer: A. 6 and 5**

### Q85. Which statement about the relation is correct?

A. The same Student_ID cannot occur more than once.
B. The same Course_ID cannot occur more than once.
C. Student_ID and Course_ID can repeat individually, even if their combination is unique.
D. Grade cannot contain NULL because it is an attribute.

**Answer: C**

### Q86. A relation has 12 attributes and 0 tuples. What are its cardinality and degree?

A. 0 and 12
B. 12 and 0
C. 0 and 0
D. Undefined and 12

**Answer: A**

**Explanation:** An empty relation can still have a defined schema. It has zero tuples but twelve attributes.

### Q87. A relation has 100 tuples and 10 attributes. After a projection operation, only four attributes are retained, and duplicate resulting tuples are eliminated.

Which statement is correct?

A. Degree becomes 4, and cardinality must remain 100.
B. Degree becomes 4, and cardinality can decrease.
C. Degree becomes 10, and cardinality becomes 4.
D. Both degree and cardinality must decrease.

**Answer: B**

**Explanation:** Projection reduces the degree. Duplicate elimination can reduce cardinality.

### Q88. Consider the SQL condition:

```sql
WHERE salary = NULL
```

What is the problem?

A. It always returns rows where salary is NULL.
B. It returns rows where salary is zero.
C. It evaluates to UNKNOWN for NULL comparisons.
D. It causes a syntax error in every SQL DBMS.

**Answer: C**

**Explanation:** SQL uses three-valued logic: TRUE, FALSE and UNKNOWN. Use `IS NULL` to test for NULL.

### Q89. Consider:

```sql
SELECT *
FROM EMPLOYEE
WHERE salary <> 50000;
```

An employee has NULL salary. Will that employee be returned?

A. Yes, because NULL is not equal to 50000.
B. Yes, because NULL is treated as zero.
C. No, because the comparison evaluates to UNKNOWN.
D. It depends on whether the salary is a primary key.

**Answer: C**

### Q90. Which statement about NULL and aggregate functions is correct?

A. SUM counts NULL as zero and includes it as a row.
B. AVG treats NULL as zero.
C. Most standard aggregate functions ignore NULL inputs, while COUNT(*) counts rows.
D. COUNT(column) counts both NULL and non-NULL values.

**Answer: C**

---

## Section 4: Integrity Constraints - Tricky Scenarios

### Q91. A table has the following definition:

```sql
CREATE TABLE STUDENT (
    Student_ID INT PRIMARY KEY,
    Name VARCHAR(30),
    Email VARCHAR(50) UNIQUE
);
```

Which insertion is permitted, assuming no existing records?

A. `(NULL, 'Arun', 'a@gmail.com')`
B. `(101, 'Arun', NULL)`
C. `(101, 'Arun', 'a@gmail.com')` followed by `(101, 'Banu', 'b@gmail.com')`
D. `(102, 'Banu', 'a@gmail.com')` after the first record has been inserted.

**Answer: B**

**Explanation:** A primary key cannot be NULL. A UNIQUE column can generally allow NULL, depending on DBMS-specific rules. Duplicate primary keys and duplicate non-NULL email values are rejected.

### Q92. A foreign key references a primary key in a parent table. The parent table contains no rows.

Can a child record be inserted with a NULL foreign key?

A. Never
B. Yes, if the foreign key column allows NULL
C. Only if the child primary key is NULL
D. Only if the parent has at least one row

**Answer: B**

### Q93. A parent table contains `Dept_ID = 10`. A child table has 100 records with `Dept_ID = 10`.

Is this allowed?

A. No, foreign keys must be unique.
B. Yes, multiple child records can reference the same parent record.
C. No, a parent key can be referenced only once.
D. Only if the child records have identical primary keys.

**Answer: B**

### Q94. Consider:

```sql
CREATE TABLE EMPLOYEE (
    Emp_ID INT PRIMARY KEY,
    Salary INT CHECK (Salary > 0)
);
```

An employee is inserted with Salary = NULL. What is the general SQL result?

A. Rejected because NULL is less than zero.
B. Rejected because CHECK automatically implies NOT NULL.
C. Accepted if no other constraint prohibits NULL.
D. Converted to zero.

**Answer: C**

**Explanation:** A CHECK condition rejects FALSE. An UNKNOWN result caused by NULL generally passes the CHECK constraint. Use `NOT NULL` separately when necessary.

### Q95. Which constraint guarantees that a column cannot contain NULL?

A. UNIQUE
B. CHECK
C. NOT NULL
D. FOREIGN KEY

**Answer: C**

### Q96. A child record references a parent record. The parent record is deleted.

Which action would preserve referential integrity while automatically deleting the corresponding child records?

A. ON DELETE SET NULL
B. ON DELETE CASCADE
C. ON UPDATE RESTRICT
D. UNIQUE

**Answer: B**

### Q97. A foreign key uses `ON DELETE SET NULL`. The parent row is deleted. What happens to matching child records?

A. Child records are deleted.
B. The foreign key values in child records become NULL.
C. Child records are automatically assigned a new parent.
D. The parent deletion always fails.

**Answer: B**

### Q98. Which statement is correct regarding a composite primary key `(A, B)`?

A. A can contain NULL if B is not NULL.
B. B can contain NULL if A is unique.
C. Neither A nor B can contain NULL.
D. Only the combination must be non-NULL.

**Answer: C**

### Q99. A table contains a foreign key referencing a UNIQUE column in the parent table, rather than its primary key.

Is this generally valid in SQL?

A. No, foreign keys can reference only primary keys.
B. Yes, a suitable UNIQUE key can also be referenced.
C. Only if the foreign key is also a primary key.
D. Only in NoSQL databases.

**Answer: B**

### Q100. Which of the following is NOT necessarily a violation of referential integrity?

A. A non-NULL foreign key references a nonexistent parent key.
B. A foreign key contains NULL and the column permits NULL.
C. A foreign key references a parent key that has been deleted without a permitted action.
D. A foreign key references an existing parent key.

**Answer: B**

---

## Section 5: Candidate Keys, Superkeys and Composite Keys

### Q101. A relation has attributes A, B, C, D and E.

Given:

- A → B
- B → C
- CD → E
- E → A

Which is a candidate key?

A. A
B. B
C. CD
D. E

**Answer: C. CD**

**Explanation:**

Calculate the closure of CD:

- CD → E
- E → A
- A → B
- B → C

Therefore:

$$
(CD)^+ = \{A,B,C,D,E\}
$$

Neither C nor D alone determines all attributes, so CD is minimal.

### Q102. A relation contains A, B, C and D.

Given:

- A → B
- B → A
- A → C
- C → D

Which are all candidate keys?

A. A only
B. B only
C. A and B
D. A, B and C

**Answer: C**

**Explanation:**

- A determines B, C and D.
- B determines A, then C and D.
- Neither A nor B can be reduced.

### Q103. A relation has attributes A, B, C and D.

Given:

- AB → C
- C → D
- D → B

Which is a candidate key?

A. A
B. AB
C. AC
D. AD

**Answer: A**

**Explanation:**

A alone does not determine anything else.

But examine the dependencies carefully: A is not present on the right side of any dependency, so every candidate key must contain A.

- AB determines C, then D.
- AC determines D, then B.
- AD determines B, then C.

Therefore, the candidate keys are AB, AC and AD.

**Corrected answer: No listed single A option is a candidate key. The correct option is none of the above.**

This is an important exam trap: always calculate closure instead of assuming a single attribute is sufficient.

### Q104. A relation has attributes A, B, C, D and E.

Given:

- A → BC
- C → D
- D → E

Which is the candidate key?

A. A
B. B
C. C
D. D

**Answer: A**

**Explanation:** A determines B and C, C determines D, and D determines E. Therefore A determines every attribute.

### Q105. A relation has attributes A, B, C, D.

Given:

- A → B
- B → C
- C → B
- D → A

Which is the candidate key?

A. A
B. D
C. AB
D. CD

**Answer: B**

**Explanation:** D determines A, A determines B, and B determines C. D determines all attributes and is minimal.

### Q106. A relation has attributes A, B, C, D and E.

Given:

- AB → C
- C → D
- D → E

Which of the following is a superkey but NOT a candidate key?

A. AB
B. ABC
C. A
D. B

**Answer: B. ABC**

**Explanation:**

- AB is a candidate key.
- ABC also determines every attribute, but C is unnecessary.
- Therefore ABC is a non-minimal superkey.

### Q107. A relation has attributes A, B, C and D.

Given:

- A → B
- C → D

Which is a candidate key?

A. A
B. C
C. AC
D. AD

**Answer: C**

**Explanation:** AC determines B through A and D through C. Neither A nor C alone determines all attributes.

### Q108. Which statement is correct?

A. Every superkey is a candidate key.
B. Every candidate key is a superkey.
C. Every foreign key is a candidate key.
D. Every alternate key is a foreign key.

**Answer: B**

### Q109. A relation has two candidate keys: `{A, B}` and `{C}`. The DBA chooses `{C}` as the primary key.

Which statement is correct?

A. A and B must individually become foreign keys.
B. `{A, B}` becomes an alternate key.
C. `{A, B}` ceases to be unique.
D. C is no longer a candidate key.

**Answer: B**

### Q110. Which of the following is the correct definition of a minimal superkey?

A. A superkey that contains every attribute.
B. A superkey from which no attribute can be removed without losing uniqueness.
C. A key that contains exactly one attribute.
D. A key that references another table.

**Answer: B**

---

## Section 6: Multi-Table Primary Key and Foreign Key Identification

Consider the following database design.

### Table 1: CUSTOMER

| Customer_ID | Email | Customer_Name |
| --- | --- | --- |
| C01 | a@gmail.com | Arun |
| C02 | b@gmail.com | Banu |
| C03 | c@gmail.com | Charan |

Rules:

- Customer_ID is unique.
- Email is unique.

### Table 2: ORDERS

| Order_ID | Customer_ID | Order_Date |
| --- | --- | --- |
| O101 | C01 | 2026-01-10 |
| O102 | C01 | 2026-01-12 |
| O103 | C02 | 2026-01-15 |

Rules:

- Order_ID is unique.
- Each order belongs to one customer.

### Table 3: PRODUCT

| Product_ID | Product_Name | SKU |
| --- | --- | --- |
| P01 | Laptop | SKU001 |
| P02 | Mouse | SKU002 |
| P03 | Keyboard | SKU003 |

Rules:

- Product_ID is unique.
- SKU is unique.

### Table 4: ORDER_DETAILS

| Order_ID | Product_ID | Quantity | Unit_Price |
| --- | --- | --- | --- |
| O101 | P01 | 1 | 50000 |
| O101 | P02 | 2 | 500 |
| O102 | P02 | 1 | 500 |
| O103 | P03 | 1 | 1000 |

Rules:

- An order can contain multiple products.
- A product can appear in multiple orders.
- A product appears at most once per order.

### Table 5: PAYMENT

| Payment_ID | Order_ID | Transaction_Ref | Amount |
| --- | --- | --- | --- |
| T01 | O101 | TXN001 | 51000 |
| T02 | O102 | TXN002 | 500 |
| T03 | O103 | TXN003 | 1000 |

Rules:

- Payment_ID is unique.
- Transaction_Ref is unique.
- Each payment belongs to exactly one order.

### Q111. Identify all candidate keys in CUSTOMER.

A. Customer_ID only
B. Email only
C. Customer_ID and Email
D. Customer_ID, Email and Customer_Name

**Answer: C**

### Q112. Which column is the primary key of ORDERS?

A. Customer_ID
B. Order_Date
C. Order_ID
D. Customer_ID + Order_ID

**Answer: C**

**Explanation:** A customer can place multiple orders, so Customer_ID cannot independently identify an order.

### Q113. Identify the foreign key in ORDERS.

A. Order_ID
B. Customer_ID
C. Order_Date
D. Both Order_ID and Order_Date

**Answer: B**

### Q114. Which attributes form the composite primary key of ORDER_DETAILS?

A. Order_ID
B. Product_ID
C. Order_ID + Product_ID
D. Order_ID + Quantity

**Answer: C**

### Q115. Which columns are foreign keys in ORDER_DETAILS?

A. Order_ID only
B. Product_ID only
C. Order_ID and Product_ID
D. Quantity and Unit_Price

**Answer: C**

### Q116. What is the primary key of PAYMENT?

A. Order_ID
B. Payment_ID
C. Transaction_Ref
D. Payment_ID and Order_ID

**Answer: B**

**Explanation:** Payment_ID and Transaction_Ref are both candidate keys. Payment_ID has been selected as the primary key.

### Q117. What is the alternate key of PAYMENT?

A. Order_ID
B. Amount
C. Transaction_Ref
D. Payment_ID

**Answer: C**

### Q118. Which statement about PAYMENT.Order_ID is correct?

A. It is a primary key because every payment belongs to one order.
B. It is a foreign key referencing ORDERS.Order_ID.
C. It is a candidate key because order IDs are unique in ORDERS.
D. It is a composite key.

**Answer: B**

**Explanation:** A foreign key's uniqueness in the parent table does not mean it must be unique in the child table. An order could have multiple payments unless the business rules prohibit that.

### Q119. Suppose the business rule changes: each order can have exactly one payment, and every order has a payment.

Which additional constraint is needed to enforce at most one payment per order?

A. UNIQUE on PAYMENT.Order_ID
B. NOT NULL on PAYMENT.Amount
C. CHECK on PAYMENT.Payment_ID
D. UNIQUE on PAYMENT.Amount

**Answer: A**

**Explanation:** A UNIQUE constraint on Order_ID ensures that the same order cannot appear in multiple payment records. Combined with NOT NULL, it enforces one payment per order for existing payment rows. Enforcing that every order has a payment requires an additional mechanism.

### Q120. Consider the following statements:

1. CUSTOMER.Customer_ID is a primary key.
2. CUSTOMER.Email is an alternate key.
3. ORDERS.Customer_ID is a foreign key.
4. ORDER_DETAILS has a composite primary key.
5. PAYMENT.Transaction_Ref is an alternate key.
6. PAYMENT.Order_ID must always be unique merely because it is a foreign key.

Which statements are correct?

A. 1, 2 and 3 only
B. 1, 2, 3, 4 and 5 only
C. 1, 2, 3, 4, 5 and 6
D. 2, 3, 4 and 6 only

**Answer: B**

**Explanation:** Statement 6 is incorrect. Foreign keys are not inherently unique. Uniqueness requires a separate constraint.

---

## Final Answer Key - Set 2

| Questions | Answers |
| --- | --- |
| 61-70 | C, B, D, A, C, D, B, B, B, A |
| 71-80 | C, B, C, C, B, B, D, B, C, B |
| 81-90 | B, A, C, A, C, A, B, C, C, C |
| 91-100 | B, B, B, C, C, B, B, C, B, B |
| 101-110 | C, C, None of the above, A, B, B, C, B, B, B |
| 111-120 | C, C, B, C, C, B, C, B, A, B |

**Correction note for Q103:** The correct candidate keys are AB, AC and AD. None of the listed options is correct. This is intentionally a closure-based reasoning trap, not a valid single-answer MCQ.

---

## Most important traps from this set

1. **Candidate key vs superkey:** Minimality is compulsory for a candidate key.
2. **Foreign key vs primary key:** A foreign key can contain duplicates and NULLs if permitted.
3. **UNIQUE vs NOT NULL:** UNIQUE does not automatically mean NOT NULL.
4. **CHECK and NULL:** A CHECK condition evaluating to UNKNOWN generally does not reject the row.
5. **Composite key:** Every participating primary-key column must be non-NULL.
6. **Cardinality and degree:** Projection can reduce both degree and cardinality.
7. **NULL:** Comparisons with NULL generally produce UNKNOWN, not TRUE or FALSE.
8. **Referential integrity:** A foreign key can reference a UNIQUE candidate key, not just a primary key.
9. **Logical independence:** Conceptual changes can be hidden through external views and mappings.
10. **Foreign key uniqueness:** A foreign key does not become unique simply because its referenced parent column is unique.

### User

er model simple what i give content only based on that give quiz relationships self relationship 1:1 1:n m:n relationship, cardinalinity of relationship, correct way of mapping 1:1 relationship, 1:n relationship, m:n relationship, given situation find what type relationship is it 1:1,1:n and m:n between 2 tables give expert level questions quiz based on this just this topic only give expert advanced tricky level give 60 mcqs dont give in quiz interface

### ChatGPT

# ER Model - 60 Advanced & Expert-Level MCQs

(Advanced-Expert) (Set 1 · 60 Questions)

**Scope strictly limited to your requested topics:**

1. Self / recursive relationships
2. One-to-one (1:1) relationships
3. One-to-many (1:N) relationships
4. Many-to-many (M:N) relationships
5. Relationship cardinality
6. Identifying relationship types from real-world scenarios
7. Mapping 1:1 relationships into tables
8. Mapping 1:N relationships into tables
9. Mapping M:N relationships into tables
10. Identifying primary keys and foreign keys after mapping

Each question has four options, followed immediately by its answer and explanation.

---

## Section 1: Identifying Relationship Types - Scenario Based

### Q1. A company assigns each employee to exactly one locker. Each locker is assigned to exactly one employee. Which relationship exists between EMPLOYEE and LOCKER?

A. One-to-one
B. One-to-many
C. Many-to-one
D. Many-to-many

**Answer: A. One-to-one**

**Explanation:** One employee corresponds to one locker, and one locker corresponds to one employee.

### Q2. A department employs multiple employees, but each employee belongs to exactly one department. What is the relationship?

A. 1:1
B. 1:N from DEPARTMENT to EMPLOYEE
C. M:N from DEPARTMENT to EMPLOYEE
D. M:N from EMPLOYEE to DEPARTMENT

**Answer: B**

**Explanation:** One department can have multiple employees, but each employee belongs to only one department.

### Q3. A student can register for multiple courses, and each course can have multiple students. Identify the relationship.

A. 1:1
B. 1:N
C. M:N
D. Recursive 1:N

**Answer: C. M:N**

### Q4. Every country has exactly one capital city, and every capital city belongs to exactly one country.

Which relationship exists?

A. 1:1
B. 1:N
C. M:N
D. Recursive

**Answer: A**

### Q5. A customer can place multiple orders. Every order belongs to exactly one customer.

Which relationship is correct?

A. CUSTOMER to ORDER is 1:1
B. CUSTOMER to ORDER is 1:N
C. CUSTOMER to ORDER is M:N
D. ORDER to CUSTOMER is M:N

**Answer: B**

### Q6. An order contains multiple products. A product can appear in multiple orders.

Which relationship exists?

A. ORDER to PRODUCT is 1:1
B. ORDER to PRODUCT is 1:N
C. ORDER to PRODUCT is M:N
D. PRODUCT to ORDER is 1:1

**Answer: C**

### Q7. Every employee may supervise multiple employees. Each employee can have at most one direct supervisor.

Which relationship is represented?

A. Employee to Supervisor is 1:1
B. Employee to Supervisor is 1:N
C. Employee to Supervisor is M:N
D. Employee to Supervisor is unrelated

**Answer: B. 1:N recursive relationship**

**Explanation:** One employee can supervise many employees. Each subordinate has at most one supervisor.

### Q8. A person can have multiple phone numbers. Each phone number is registered to exactly one person.

What is the relationship?

A. 1:1
B. 1:N
C. M:N
D. Recursive 1:1

**Answer: B**

### Q9. A doctor treats multiple patients, and a patient can consult multiple doctors.

Identify the relationship.

A. 1:1
B. 1:N
C. M:N
D. Recursive 1:N

**Answer: C**

### Q10. Each vehicle has exactly one registered engine. Each engine is installed in exactly one vehicle at a time.

What is the relationship?

A. 1:1
B. 1:N
C. M:N
D. Recursive

**Answer: A**

---

## Section 2: Cardinality and Relationship Direction

### Q11. Consider:

- One department has many employees.
- Each employee belongs to one department.

Which statement correctly describes cardinality?

A. EMPLOYEE (1) : DEPARTMENT (N)
B. DEPARTMENT (1) : EMPLOYEE (N)
C. DEPARTMENT (N) : EMPLOYEE (N)
D. DEPARTMENT (1) : EMPLOYEE (1)

**Answer: B**

### Q12. A student can enroll in at most five courses. Each course can have at most 100 students.

Which relationship type exists?

A. 1:1
B. 1:N
C. M:N
D. Recursive 1:N

**Answer: C**

**Explanation:** The maximum number on both sides is greater than one. The exact maximum values do not change the relationship category.

### Q13. One manager manages at most one branch, and each branch has at most one manager. Some managers and branches may currently have no association.

What is the maximum cardinality?

A. 1:1
B. 1:N
C. M:N
D. N:1

**Answer: A**

**Explanation:** Optional participation does not change the maximum cardinality.

### Q14. One company owns many buildings. Each building belongs to exactly one company.

What is the relationship from BUILDING to COMPANY?

A. 1:1
B. 1:N
C. N:1
D. M:N

**Answer: C. N:1**

**Explanation:** Direction matters.

- COMPANY to BUILDING: 1:N.
- BUILDING to COMPANY: N:1.

### Q15. A student can have multiple mentors. Each mentor can guide multiple students.

What is the relationship?

A. 1:1
B. 1:N
C. M:N
D. Recursive 1:1

**Answer: C**

### Q16. An employee can have exactly one company email address. Every company email address belongs to exactly one employee.

Which relationship is represented?

A. 1:1
B. 1:N
C. M:N
D. Recursive 1:N

**Answer: A**

### Q17. A library has many books. Each physical book copy belongs to exactly one library branch. A library branch can have many book copies.

Which relationship exists?

A. LIBRARY to BOOK_COPY = 1:1
B. LIBRARY to BOOK_COPY = 1:N
C. LIBRARY to BOOK_COPY = M:N
D. BOOK_COPY to LIBRARY = M:N

**Answer: B**

### Q18. A company has multiple projects. An employee can work on multiple projects, but a project can also have multiple employees.

Which statement is correct?

A. One employee has exactly one project.
B. One project has exactly one employee.
C. Employee and Project have an M:N relationship.
D. Employee and Project have a 1:1 relationship.

**Answer: C**

### Q19. Each student has one permanent university registration number. A registration number belongs to exactly one student.

Which relationship is correct?

A. Student to Registration_Number = 1:1
B. Student to Registration_Number = 1:N
C. Student to Registration_Number = M:N
D. Student to Registration_Number = N:1

**Answer: A**

### Q20. A parent can have multiple children. Each child has exactly two biological parents.

Considering PARENT and CHILD as entity types, what is the relationship?

A. 1:1
B. 1:N
C. M:N
D. Recursive 1:N

**Answer: C**

**Explanation:** One parent can be associated with many children, and one child can be associated with two parents. This is M:N.

---

## Section 3: Mapping One-to-One Relationships

### Q21. Consider two entities:

**PERSON**

- Person_ID (PK)
- Name

**PASSPORT**

- Passport_ID (PK)
- Issue_Date

Business rules:

- Each person has at most one passport.
- Each passport belongs to exactly one person.

Which is a correct mapping?

A. Add Person_ID as a foreign key in PASSPORT and enforce UNIQUE.
B. Add Passport_ID as a foreign key in PERSON without any constraint.
C. Create a bridge table without constraints.
D. Add Person_ID as a foreign key in PASSPORT without UNIQUE.

**Answer: A**

**Explanation:** PASSPORT.Person_ID references PERSON.Person_ID. UNIQUE ensures one passport per person.

### Q22. Consider:

**COUNTRY(Country_ID, Country_Name)**

**CAPITAL(Capital_ID, City_Name)**

Every country has exactly one capital, and every capital belongs to exactly one country.

Which mapping correctly enforces the relationship?

A. Add Country_ID as a foreign key in CAPITAL and make it UNIQUE and NOT NULL.
B. Add Capital_ID as a foreign key in COUNTRY without UNIQUE.
C. Add Country_ID as a foreign key in CAPITAL without UNIQUE.
D. Create a many-to-many junction table.

**Answer: A**

### Q23. In a 1:1 relationship, which mapping can enforce one-to-one cardinality?

A. Foreign key only
B. Foreign key with UNIQUE constraint
C. Foreign key with a non-unique index
D. Foreign key with a duplicate value allowed

**Answer: B**

### Q24. Consider:

**EMPLOYEE(Emp_ID, Name)**

**PARKING_SLOT(Slot_ID, Location)**

Each parking slot is assigned to at most one employee. Each employee can have at most one parking slot. Not every employee needs a parking slot.

Which is a valid mapping?

A. PARKING_SLOT contains Emp_ID as a nullable UNIQUE foreign key.
B. EMPLOYEE contains Slot_ID as a mandatory non-unique foreign key.
C. PARKING_SLOT contains Emp_ID as a non-unique foreign key.
D. Both tables contain each other's primary keys as mandatory foreign keys.

**Answer: A**

**Explanation:** A nullable foreign key allows an unassigned parking slot. UNIQUE prevents multiple parking slots from referencing the same employee.

### Q25. A 1:1 relationship exists between EMPLOYEE and EMPLOYEE_ID_CARD.

Every ID card must belong to an employee, but an employee may not yet have an ID card.

Where is the most appropriate place to store the foreign key?

A. EMPLOYEE
B. EMPLOYEE_ID_CARD
C. Both tables
D. A separate M:N junction table

**Answer: B**

**Explanation:** Put the foreign key on the ID card side because every card must reference an employee. This also avoids unnecessary NULL foreign keys in EMPLOYEE.

### Q26. Consider the following mapping:

```sql
EMPLOYEE(
    Emp_ID PRIMARY KEY,
    Name,
    Card_ID UNIQUE
)

ID_CARD(
    Card_ID PRIMARY KEY,
    Issue_Date
)
```

What is missing if the intended relationship is one-to-one?

A. EMPLOYEE.Card_ID must reference ID_CARD.Card_ID.
B. EMPLOYEE.Emp_ID must reference ID_CARD.Card_ID.
C. ID_CARD.Card_ID must reference EMPLOYEE.Name.
D. No constraint is missing.

**Answer: A**

**Explanation:** UNIQUE alone does not establish referential integrity. Card_ID must also be a foreign key.

### Q27. A 1:1 relationship has total participation on both sides. Both entities are always created together and have the same lifecycle.

Which mapping may be the simplest?

A. Merge both entities into one table, if their independent identity and lifecycle do not need to be maintained.
B. Always create three tables.
C. Always use an M:N junction table.
D. Store a non-unique foreign key in either table.

**Answer: A**

### Q28. Consider:

**PERSON(Person_ID, Name)**

**DRIVING_LICENSE(License_ID, Person_ID, Expiry_Date)**

Person_ID in DRIVING_LICENSE is a foreign key but has no UNIQUE constraint.

What relationship does the schema permit?

A. Strict 1:1
B. 1:N from PERSON to DRIVING_LICENSE
C. M:N
D. 1:N from DRIVING_LICENSE to PERSON

**Answer: B**

**Explanation:** One person can have multiple driving-license records because the foreign key is not unique. This may be useful for license history, but it does not enforce a current 1:1 relationship.

### Q29. A developer maps a 1:1 relationship using a separate relationship table:

**EMPLOYEE_DEPARTMENT(Emp_ID, Dept_ID)**

Both columns are foreign keys.

Which constraint combination can enforce the maximum 1:1 relationship?

A. PRIMARY KEY(Emp_ID) only
B. PRIMARY KEY(Dept_ID) only
C. UNIQUE(Emp_ID) and UNIQUE(Dept_ID)
D. Neither column needs a uniqueness constraint

**Answer: C**

**Explanation:** Both columns must be unique. A composite primary key alone would not prevent one employee from being associated with multiple departments.

### Q30. A company requires every employee to have at most one assigned company car, and each car can be assigned to at most one employee. Employees may have no car.

Which design correctly enforces the maximum relationship cardinality?

A. CAR(Car_ID PK, Emp_ID UNIQUE FK NULL)
B. CAR(Car_ID PK, Emp_ID FK without UNIQUE)
C. CAR(Car_ID PK, Emp_ID NOT NULL FK without UNIQUE)
D. EMPLOYEE(Emp_ID PK, Car_ID FK without UNIQUE)

**Answer: A**

---

## Section 4: Mapping One-to-Many Relationships

### Q31. Consider:

**DEPARTMENT(Dept_ID, Dept_Name)**

**EMPLOYEE(Emp_ID, Emp_Name)**

One department can have many employees. Each employee belongs to one department.

Where should the foreign key be placed?

A. DEPARTMENT
B. EMPLOYEE
C. Both tables
D. Separate relationship table is mandatory

**Answer: B**

**Explanation:** The foreign key is placed on the many side.

### Q32. Consider:

**CUSTOMER(Customer_ID, Name)**

**ORDER(Order_ID, Order_Date)**

A customer can place multiple orders. Every order belongs to exactly one customer.

Which is the correct mapping?

A. CUSTOMER contains Order_ID as FK.
B. ORDER contains Customer_ID as FK.
C. Both contain each other's primary key.
D. A bridge table is mandatory.

**Answer: B**

### Q33. A university has multiple courses. Each course belongs to exactly one department. A department may offer no courses.

Which mapping is correct?

A. DEPARTMENT contains Course_ID as FK.
B. COURSE contains Dept_ID as FK, which may be nullable if courses can exist without a department.
C. COURSE contains Dept_ID as a non-unique FK.
D. A junction table is compulsory.

**Answer: C**

**Explanation:** COURSE is the many side, so Dept_ID belongs there. Whether it is nullable depends on the participation requirement. Here, the scenario says each course belongs to exactly one department, so it must be NOT NULL.

### Q34. An employee belongs to exactly one department. A department may contain zero or more employees.

Which is the correct foreign key constraint?

A. EMPLOYEE.Dept_ID REFERENCES DEPARTMENT.Dept_ID and NOT NULL.
B. DEPARTMENT.Emp_ID REFERENCES EMPLOYEE.Emp_ID and NOT NULL.
C. EMPLOYEE.Dept_ID REFERENCES DEPARTMENT.Dept_ID and UNIQUE.
D. Both tables require composite primary keys.

**Answer: A**

### Q35. A company has:

- One manager per department.
- One manager may manage multiple departments.

Which table should contain the foreign key?

A. MANAGER
B. DEPARTMENT
C. Both
D. A junction table is always mandatory.

**Answer: B**

**Explanation:** One manager can manage multiple departments. Manager_ID belongs in DEPARTMENT, the many side.

### Q36. Consider:

**AUTHOR(Author_ID, Name)**

**BOOK(Book_ID, Title)**

Each book has exactly one author. An author can write multiple books.

Which is the correct mapping?

A. AUTHOR contains Book_ID.
B. BOOK contains Author_ID.
C. Create an M:N junction table.
D. Both tables contain a composite primary key.

**Answer: B**

### Q37. A table is designed as:

```sql
DEPARTMENT(
    Dept_ID PRIMARY KEY,
    Dept_Name,
    Emp_ID
)
```

The intended relationship is one department to many employees.

What is the primary design error?

A. Emp_ID should be a foreign key in EMPLOYEE, not a repeating list of employee identifiers in DEPARTMENT.
B. Dept_ID cannot be a primary key.
C. Dept_Name must be a foreign key.
D. A department cannot have employees.

**Answer: A**

### Q38. A developer places the foreign key on the one side of a 1:N relationship and makes it unique. What does this generally result in?

A. It correctly implements 1:N.
B. It may restrict the relationship to 1:1.
C. It creates M:N.
D. It eliminates referential integrity.

**Answer: B**

### Q39. Consider:

```sql
EMPLOYEE(
    Emp_ID PRIMARY KEY,
    Name,
    Dept_ID FOREIGN KEY
)
```

The Dept_ID column is nullable.

What relationship does the structure permit?

A. Every employee must belong to a department.
B. An employee may exist without an associated department.
C. Every department must have exactly one employee.
D. Each department can have only one employee.

**Answer: B**

### Q40. In a 1:N relationship, what happens if the foreign key on the many side is declared UNIQUE?

A. Multiple child records can reference the same parent.
B. It restricts each parent to at most one matching child.
C. It automatically creates an M:N relationship.
D. It has no effect on cardinality.

**Answer: B**

---

## Section 5: Mapping Many-to-Many Relationships

### Q41. A STUDENT can enroll in multiple COURSES, and each COURSE can contain multiple STUDENTS.

Which is the correct relational mapping?

A. Put Course_ID in STUDENT without a junction table.
B. Put Student_ID in COURSE without a junction table.
C. Create STUDENT_COURSE with Student_ID and Course_ID as foreign keys.
D. Duplicate student and course details in both tables.

**Answer: C**

### Q42. Consider:

**STUDENT(Student_ID, Name)**

**COURSE(Course_ID, Course_Name)**

**ENROLLMENT(Student_ID, Course_ID, Grade)**

Each student can enroll in each course only once.

Which is the most appropriate primary key for ENROLLMENT?

A. Student_ID
B. Course_ID
C. Student_ID + Course_ID
D. Grade

**Answer: C**

### Q43. An ORDER contains multiple PRODUCTS, and each PRODUCT can belong to multiple ORDERS.

A developer creates:

```sql
ORDER(
    Order_ID PRIMARY KEY,
    Product_ID FOREIGN KEY
)
```

What is the design problem?

A. It cannot naturally represent multiple products in the same order without repeating or restructuring the order record.
B. It automatically creates a valid M:N relationship.
C. It prevents orders from having an ID.
D. It makes products unique across all orders.

**Answer: A**

### Q44. Which statement about an M:N mapping is correct?

A. A junction table is normally introduced to represent the relationship.
B. The primary key of one original table must become the primary key of the other.
C. The junction table contains only descriptive attributes and no foreign keys.
D. An M:N relationship cannot be represented relationally.

**Answer: A**

### Q45. A STUDENT can participate in multiple SPORTS, and each SPORT has multiple STUDENTS. A student can register for the same sport in multiple years, but only once per year.

Which should be the primary key of STUDENT_SPORT?

A. Student_ID
B. Sport_ID
C. Student_ID + Sport_ID
D. Student_ID + Sport_ID + Year

**Answer: D**

**Explanation:** The combination must distinguish the year-specific registrations.

### Q46. A developer creates this junction table:

```sql
STUDENT_COURSE(
    Student_ID,
    Course_ID,
    PRIMARY KEY(Student_ID, Course_ID)
)
```

What does this primary key prevent?

A. A student enrolling in multiple courses.
B. A course having multiple students.
C. The same student-course pair being inserted more than once.
D. Different students enrolling in the same course.

**Answer: C**

### Q47. An M:N relationship has attributes `Enrollment_Date` and `Grade`.

Where should these attributes be stored?

A. STUDENT
B. COURSE
C. STUDENT_COURSE junction table
D. Both original tables

**Answer: C**

**Explanation:** These attributes describe the association between a particular student and a particular course, not the student or course independently.

### Q48. A customer can purchase many products, and a product can be purchased by many customers. Each purchase is tracked with a separate Purchase_ID.

Which is a valid mapping?

A. CUSTOMER(Customer_ID PK), PRODUCT(Product_ID PK), PURCHASE(Purchase_ID PK, Customer_ID FK, Product_ID FK)
B. CUSTOMER(Customer_ID PK, Product_ID FK), PRODUCT(Product_ID PK)
C. PRODUCT(Product_ID PK, Customer_ID FK), CUSTOMER(Customer_ID PK)
D. CUSTOMER(Customer_ID PK), PRODUCT(Product_ID PK), without any relationship table.

**Answer: A**

### Q49. An M:N relationship is mapped using a junction table with two foreign keys. The developer creates a composite primary key using both foreign keys.

Which statement is correct?

A. This allows duplicate pairs.
B. This prevents duplicate pairs but still allows one entity to associate with multiple entities on the other side.
C. This restricts the relationship to 1:1.
D. This restricts the relationship to 1:N.

**Answer: B**

### Q50. Consider:

```sql
EMPLOYEE_PROJECT(
    Emp_ID,
    Project_ID,
    PRIMARY KEY(Emp_ID, Project_ID)
)
```

The company wants to allow the same employee to join the same project again in a different year.

What is the appropriate key?

A. Emp_ID only
B. Project_ID only
C. Emp_ID + Project_ID
D. Emp_ID + Project_ID + Year

**Answer: D**

---

## Section 6: Self / Recursive Relationships and Mapping

### Q51. An employee can supervise multiple employees. Each employee reports to at most one supervisor.

What type of relationship is this?

A. Unary 1:1
B. Unary 1:N
C. Unary M:N
D. Binary 1:N

**Answer: B. Unary 1:N**

**Explanation:** It is a recursive relationship because EMPLOYEE participates in the relationship with itself.

### Q52. Which is the correct mapping for an employee-supervises-employee relationship?

A. EMPLOYEE(Emp_ID PK, Name, Manager_ID FK referencing EMPLOYEE.Emp_ID)
B. EMPLOYEE(Emp_ID PK, Name, Department_ID FK referencing DEPARTMENT.Emp_ID)
C. EMPLOYEE(Emp_ID PK, Manager_ID PK)
D. SUPERVISOR(Emp_ID PK), EMPLOYEE(Manager_ID PK)

**Answer: A**

### Q53. In the employee-supervisor table, which value should be stored in Manager_ID for the top-level employee who has no supervisor?

A. The employee's own Emp_ID
B. A nonexistent employee ID
C. NULL, if permitted
D. A duplicate employee name

**Answer: C**

### Q54. An employee can mentor many employees, but an employee can also have multiple mentors.

What is the recursive relationship?

A. Unary 1:1
B. Unary 1:N
C. Unary M:N
D. Binary M:N

**Answer: C**

### Q55. Which is an appropriate relational mapping for the recursive M:N relationship in Q54?

A. EMPLOYEE(Emp_ID PK, Mentor_ID FK) only
B. EMPLOYEE(Emp_ID PK) and EMPLOYEE_MENTOR(Mentor_ID FK, Mentee_ID FK)
C. EMPLOYEE(Emp_ID PK, Mentor_ID UNIQUE FK)
D. EMPLOYEE(Emp_ID PK, Mentee_ID UNIQUE FK)

**Answer: B**

**Explanation:** The junction table represents multiple mentor-mentee associations. Both foreign keys reference EMPLOYEE.Emp_ID.

### Q56. An employee can be married to at most one other employee. An employee can appear as a spouse in at most one marriage record. The relationship is represented between EMPLOYEE records.

Which relationship is represented?

A. Unary 1:1
B. Unary 1:N
C. Unary M:N
D. Binary 1:N

**Answer: A**

### Q57. Consider:

```sql
EMPLOYEE(
    Emp_ID PRIMARY KEY,
    Name,
    Manager_ID
)
```

Manager_ID references Emp_ID in the same table.

Which statement is correct?

A. Manager_ID must always be unique.
B. Manager_ID can repeat because one manager can supervise multiple employees.
C. Manager_ID must equal Emp_ID.
D. Manager_ID is the primary key.

**Answer: B**

### Q58. A developer maps an employee mentoring relationship as:

```sql
EMPLOYEE(
    Emp_ID PRIMARY KEY,
    Mentor_ID REFERENCES EMPLOYEE(Emp_ID)
)
```

Business rule: An employee can have multiple mentors.

What is the problem?

A. A single Mentor_ID column cannot represent multiple mentors for one employee.
B. A self-referencing foreign key is never allowed.
C. Emp_ID cannot be a primary key.
D. Recursive relationships cannot be mapped to tables.

**Answer: A**

### Q59. Consider an employee hierarchy:

| Emp_ID | Manager_ID |
| --- | --- |
| 101 | NULL |
| 102 | 101 |
| 103 | 101 |
| 104 | 102 |
| 105 | 102 |

What is the maximum number of direct subordinates of employee 101 in the given records?

A. 1
B. 2
C. 3
D. 4

**Answer: B. 2**

**Explanation:** Employees 102 and 103 directly report to 101. Employees 104 and 105 report to 102, so they are not direct subordinates of 101.

### Q60. A university maintains the following relationships:

1. One department has multiple employees; each employee belongs to one department.
2. Students can register for multiple courses; courses can have multiple students.
3. An employee can supervise multiple employees; each employee has at most one supervisor.
4. Each employee has at most one parking slot; each parking slot belongs to at most one employee.

Which mapping combination is correct?

A. 1:N - FK on EMPLOYEE; M:N - junction table; recursive 1:N - self-referencing FK; 1:1 - UNIQUE FK.
B. 1:N - FK on DEPARTMENT; M:N - FK on STUDENT only; recursive 1:N - junction table always; 1:1 - non-unique FK.
C. 1:N - junction table; M:N - FK on COURSE only; recursive 1:N - two separate entity tables; 1:1 - non-unique FK.
D. 1:N - FK on EMPLOYEE; M:N - no junction table; recursive 1:N - self-referencing primary key; 1:1 - ordinary FK.

**Answer: A**

**Explanation:**

| Relationship | Correct mapping |
| --- | --- |
| Department-Employee | Dept_ID FK in EMPLOYEE |
| Student-Course | STUDENT_COURSE junction table |
| Employee-Supervisor | Manager_ID self-referencing FK |
| Employee-Parking Slot | UNIQUE FK on one side |

---

## Answer Key - 60 Questions

| Questions | Answers |
| --- | --- |
| 1-10 | A, B, C, A, B, C, B, B, C, A |
| 11-20 | B, C, A, C, C, A, B, C, A, C |
| 21-30 | A, A, B, A, B, A, A, B, C, A |
| 31-40 | B, B, C, A, B, B, A, B, B, B |
| 41-50 | C, C, A, A, D, C, C, A, B, D |
| 51-60 | B, A, C, C, B, A, B, A, B, A |

---

## Essential mapping rules - exam revision

**1. One-to-one (1:1)**

(FK + UNIQUE)

Place the foreign key in an appropriate table, preferably the side with total participation. Enforce UNIQUE to prevent multiple matches. Use NOT NULL when participation is mandatory.

```sql

PERSON(Person_ID PRIMARY KEY)

PASSPORT(
    Passport_ID PRIMARY KEY,
    Person_ID UNIQUE NOT NULL,
    FOREIGN KEY (Person_ID) REFERENCES PERSON(Person_ID)
)
```

---

**2. One-to-many (1:N)**

(FK on N side)

```sql

DEPARTMENT(Dept_ID PRIMARY KEY)

EMPLOYEE(
    Emp_ID PRIMARY KEY,
    Dept_ID,
    FOREIGN KEY (Dept_ID) REFERENCES DEPARTMENT(Dept_ID)
)
```

---

**3. Many-to-many (M:N)**

(Junction table)

```sql

STUDENT(Student_ID PRIMARY KEY)

COURSE(Course_ID PRIMARY KEY)

ENROLLMENT(
    Student_ID,
    Course_ID,
    PRIMARY KEY(Student_ID, Course_ID),
    FOREIGN KEY (Student_ID) REFERENCES STUDENT(Student_ID),
    FOREIGN KEY (Course_ID) REFERENCES COURSE(Course_ID)
)
```

---

**4. Self / recursive relationship**

(Self-referencing FK or junction table)

```sql

-- Recursive 1:N
EMPLOYEE(
    Emp_ID PRIMARY KEY,
    Manager_ID,
    FOREIGN KEY (Manager_ID) REFERENCES EMPLOYEE(Emp_ID)
)

-- Recursive M:N
EMPLOYEE_MENTOR(
    Mentor_ID,
    Mentee_ID,
    PRIMARY KEY(Mentor_ID, Mentee_ID),
    FOREIGN KEY (Mentor_ID) REFERENCES EMPLOYEE(Emp_ID),
    FOREIGN KEY (Mentee_ID) REFERENCES EMPLOYEE(Emp_ID)
)
```

**Four rules to never confuse in an exam:**

- 1:1 → Foreign key + UNIQUE.
- 1:N → Foreign key on the N side.
- M:N → Separate junction table with two foreign keys.
- Recursive → Same entity participates on both sides; mapping depends on whether the relationship is 1:1, 1:N or M:N.

### User

functional dependency: fully functional dependency, partial functional dependency, transitive functional dependency, issues with bad design: insert anamoly, update anamoly, delete anamoly, data redundance for unnormalized table, identify correct relationship between attributes of a table, given functional dependancy of table identify if table is fully functional dependancy partial or transitive, given functional dependancy identify candidate key this type mcqs also give more based on this topic with table examples mcqs give, intro to normalization types of normal forms, how do we achieve 1st normal form, second normal form 3rd normal form give set of identify normal form of given table, then table -> final normal form for 1st second third which is correct mcq give 60 questions expert level questions mcq give give 5 nrmalization till 3nf questions given table decompose till 3nf give 10 dont give in quiz interface give 60 quiz + other question give aboe

### ChatGPT

# DBMS - Functional Dependencies & Normalization: Advanced Expert MCQ Practice

(Expert Level) (60 MCQs + 10 Decomposition Problems)

This practice set covers only Functional Dependencies, database design problems and Normalization up to 3NF.

**Difficulty:** Advanced to Expert - suitable for SQL Developer / DBMS technical assessments.

## Complete topic coverage

| Section | Topics | Questions |
| --- | --- | --- |
| 1 | Functional dependency fundamentals | 1-10 |
| 2 | Full, partial and transitive dependencies | 11-20 |
| 3 | Candidate keys using functional dependencies | 21-30 |
| 4 | Bad database design and anomalies | 31-38 |
| 5 | 1NF, 2NF and 3NF concepts | 39-48 |
| 6 | Identify normal form and correct decomposition | 49-60 |
| 7 | Normalize given tables up to 3NF | 10 problems |

All questions have four options, with answers and explanations immediately after each question. No quiz interface.

---

# Section 1: Functional Dependency Fundamentals

### Q1. Consider a STUDENT table with the following attributes:

`Student_ID, Student_Name, Department, Department_HOD`

Given:

- Student_ID uniquely identifies a student.
- Each department has exactly one HOD.
- Multiple students can belong to the same department.

Which functional dependency is correct?

A. Department → Student_ID
B. Student_ID → Department
C. Department_HOD → Student_ID
D. Student_Name → Department

**Answer: B**

**Explanation:** Each student belongs to one department, so Student_ID determines Department. However, one department can contain multiple students, so Department cannot determine Student_ID.

### Q2. Consider:

`EMPLOYEE(Emp_ID, Emp_Name, Dept_ID, Dept_Name)`

Given:

- Emp_ID uniquely identifies an employee.
- Dept_ID uniquely identifies a department.
- Each employee belongs to one department.

Which set of functional dependencies is correct?

A. Emp_ID → Emp_Name, Dept_ID; Dept_ID → Dept_Name
B. Dept_ID → Emp_ID, Emp_Name
C. Emp_Name → Emp_ID, Dept_ID
D. Dept_Name → Emp_ID

**Answer: A**

**Explanation:**

- Emp_ID determines employee details, including Dept_ID.
- Dept_ID determines Dept_Name.

### Q3. If A → B, which statement is necessarily true?

A. B → A
B. Every A value must be unique.
C. Each A value determines at most one B value.
D. A and B must both be primary keys.

**Answer: C**

**Explanation:** Functional dependency does not necessarily mean that A is unique. Multiple rows can have the same A value, provided they have the same B value.

### Q4. Consider the following records:

| Employee_ID | Employee_Name | Department |
| --- | --- | --- |
| 101 | Arun | IT |
| 102 | Banu | HR |
| 103 | Charan | IT |
| 104 | Divya | Finance |

Which dependency is supported by the stated business rule that Employee_ID uniquely identifies an employee?

A. Department → Employee_ID
B. Employee_ID → Employee_Name
C. Employee_Name → Employee_ID
D. Department → Employee_Name

**Answer: B**

**Explanation:** Employee_ID uniquely identifies the employee, including their name. Repeated department values do not determine individual employees.

### Q5. A table has:

`A, B, C`

Given:

- A → B
- B → C

Which dependency can be derived using transitivity?

A. C → A
B. B → A
C. A → C
D. C → B

**Answer: C**

### Q6. Given:

- A → B
- A → C

Which statement is correct?

A. A → BC
B. B → AC
C. C → AB
D. BC → A

**Answer: A**

**Explanation:** By the union rule, if A determines B and A determines C, A determines the combination BC.

### Q7. Given:

- AB → C
- C → D

Which dependency can be derived?

A. A → D
B. B → D
C. AB → D
D. D → AB

**Answer: C**

### Q8. Consider:

`ORDER(Order_ID, Customer_ID, Customer_Name)`

Given:

- Each order belongs to one customer.
- Customer_ID determines Customer_Name.

Which dependency is correct?

A. Order_ID → Customer_ID
B. Customer_ID → Order_ID
C. Customer_Name → Order_ID
D. Order_ID → Customer_Name is impossible to derive.

**Answer: A**

**Explanation:** Order_ID determines Customer_ID, and Customer_ID determines Customer_Name. Therefore, Order_ID also determines Customer_Name.

### Q9. Which statement about functional dependencies is correct?

A. Functional dependencies are determined exclusively by the current sample data.
B. Functional dependencies represent business rules governing attribute relationships.
C. Functional dependencies always require a primary key.
D. Functional dependencies exist only in normalized tables.

**Answer: B**

### Q10. Consider:

`R(A, B, C, D)`

Given:

- A → B
- B → C
- C → D

What is the closure of A?

A.
B.
C.
D.

**Answer: C**

**Explanation:**

- A determines B.
- B determines C.
- C determines D.

Therefore, $A^+ = \{A,B,C,D\}$.

---

# Section 2: Full, Partial and Transitive Functional Dependencies

### Q11. Consider:

`ENROLLMENT(Student_ID, Course_ID, Student_Name, Course_Name, Grade)`

Primary key: `(Student_ID, Course_ID)`

Functional dependencies:

- Student_ID → Student_Name
- Course_ID → Course_Name
- (Student_ID, Course_ID) → Grade

Which dependencies are partial?

A. Student_ID → Student_Name only
B. Course_ID → Course_Name only
C. Both A and B
D. Composite key → Grade

**Answer: C**

**Explanation:** Student_Name depends only on Student_ID, and Course_Name depends only on Course_ID. Both are proper subsets of the composite primary key.

### Q12. Consider:

`ORDER_DETAILS(Order_ID, Product_ID, Quantity, Unit_Price)`

Primary key: `(Order_ID, Product_ID)`

Given:

- (Order_ID, Product_ID) → Quantity
- Product_ID → Unit_Price

Identify the dependency types.

A. Quantity: Partial; Unit_Price: Full
B. Quantity: Full; Unit_Price: Partial
C. Both are partial
D. Both are transitive

**Answer: B**

### Q13. Consider:

`EMPLOYEE(Emp_ID, Emp_Name, Dept_ID, Dept_Name)`

Primary key: Emp_ID.

Dependencies:

- Emp_ID → Emp_Name, Dept_ID
- Dept_ID → Dept_Name

What is the dependency of Dept_Name on Emp_ID?

A. Full functional dependency
B. Partial functional dependency
C. Transitive functional dependency
D. Multivalued dependency

**Answer: C**

**Explanation:**

Emp_ID → Dept_ID → Dept_Name.

Dept_Name depends on Emp_ID through a non-key attribute.

### Q14. Consider:

`R(A, B, C)`

Primary key: AB.

Dependencies:

- AB → C
- A → C

What type of dependency exists for C on the primary key?

A. Full functional dependency
B. Partial functional dependency
C. Transitive functional dependency
D. No dependency

**Answer: B**

**Explanation:** C is determined by A alone, which is a proper subset of the composite key AB.

### Q15. Consider:

`R(A, B, C, D)`

Primary key: AB.

Dependencies:

- AB → C
- AB → D
- A → C

Which attribute is fully functionally dependent on the complete key?

A. C only
B. D only
C. Both C and D
D. Neither C nor D

**Answer: B**

### Q16. Consider:

`STUDENT(Student_ID, Student_Name, Dept_ID, Dept_Name)`

Dependencies:

- Student_ID → Student_Name, Dept_ID
- Dept_ID → Dept_Name

Which is the correct interpretation?

A. Student_Name is transitive and Dept_Name is partial.
B. Dept_Name is transitively dependent on Student_ID.
C. Dept_ID is partially dependent on Student_ID.
D. Student_ID → Dept_ID is a transitive dependency.

**Answer: B**

### Q17. Consider:

`R(A, B, C, D)`

Primary key: AB.

Dependencies:

- AB → C
- AB → D
- B → D

Which statement is correct?

A. C and D are fully dependent on AB.
B. C is fully dependent; D is partially dependent.
C. C is partially dependent; D is fully dependent.
D. Both are transitive.

**Answer: B**

### Q18. Consider:

`RESULT(Student_ID, Subject_ID, Exam_ID, Marks)`

Primary key: `(Student_ID, Subject_ID, Exam_ID)`.

Business rule:

- Marks are determined only by Student_ID and Exam_ID.
- Subject_ID is not needed to determine Marks.

What type of dependency exists?

A. Full functional dependency
B. Partial functional dependency
C. Transitive functional dependency
D. No functional dependency

**Answer: B**

**Explanation:** Student_ID and Exam_ID together are a proper subset of the composite key.

### Q19. Consider:

`R(A, B, C, D)`

Primary key: A.

Dependencies:

- A → B
- B → C
- C → D

Which statement is correct?

A. C is partially dependent on A.
B. D is partially dependent on A.
C. C and D are transitively dependent on A.
D. A → D is invalid.

**Answer: C**

### Q20. A relation has a single-attribute candidate key A.

A → B and B → C.

Can B → C represent a partial dependency of the primary key A?

A. Yes, because B is a non-key attribute.
B. Yes, because C depends indirectly on A.
C. No, partial dependency requires a proper subset of a composite candidate key.
D. No, because transitive dependency is impossible with a single-attribute key.

**Answer: C**

---

# Section 3: Identify Candidate Keys Using Functional Dependencies

For these questions, calculate attribute closures. A candidate key must determine every attribute and must be minimal.

### Q21. Relation R(A, B, C).

FDs:

- A → B
- B → C

Identify the candidate key.

A. A
B. B
C. C
D. BC

**Answer: A**

**Explanation:** A+ = ABC. Neither B nor C determines A.

### Q22. Relation R(A, B, C, D).

FDs:

- A → B
- C → D

Identify the candidate key.

A. A
B. C
C. AC
D. AD

**Answer: C**

### Q23. Relation R(A, B, C, D).

FDs:

- AB → C
- C → D
- D → A

Identify all candidate keys.

A. AB only
B. AB and BC
C. AB, BC and BD
D. A, B and C

**Answer: C**

**Explanation:**

- AB determines C, D and A.
- BC determines D, A and B.
- BD determines A, B and C.

Each is minimal.

### Q24. Relation R(A, B, C, D, E).

FDs:

- A → BC
- C → D
- D → E

Candidate key?

A. A
B. B
C. C
D. D

**Answer: A**

### Q25. Relation R(A, B, C, D).

FDs:

- A → B
- B → A
- C → D

Identify all candidate keys.

A. A and B
B. AC and BC
C. AB and CD
D. A, B and C

**Answer: B**

### Q26. Relation R(A, B, C, D).

FDs:

- AB → C
- C → D

Which is a superkey but not a candidate key?

A. AB
B. ABC
C. A
D. B

**Answer: B**

**Explanation:** AB is a candidate key. ABC is a superkey, but C is unnecessary.

### Q27. Relation R(A, B, C, D, E).

FDs:

- A → B
- BC → D
- D → E

What is a candidate key?

A. A
B. AC
C. BC
D. BD

**Answer: B**

**Explanation:** AC determines B, then D through BC, then E through D. Neither A nor C alone determines all attributes.

### Q28. Relation R(A, B, C, D, E).

FDs:

- AB → C
- C → D
- D → E
- E → B

Which is a candidate key?

A. A
B. AB
C. AC
D. AD

**Answer: A**

**Explanation:** A is not present on any right-hand side, so every candidate key must contain A. But A alone does not determine B, C, D or E.

**Correction: None of the listed options is a candidate key.** The candidate keys are AB, AC, AD and AE.

### Q29. Relation R(A, B, C, D).

FDs:

- A → B
- B → C
- C → A
- A → D

Which set contains all candidate keys?

A. A only
B. B only
C. C only
D. A, B and C

**Answer: D**

### Q30. Relation R(A, B, C, D, E).

FDs:

- AB → C
- C → D
- D → E
- E → C

Which attributes must appear in every candidate key?

A. A and B
B. C and D
C. A only
D. B and E

**Answer: A**

**Explanation:** Neither A nor B appears on the right side of any dependency. Both must therefore be included in every candidate key. AB determines all remaining attributes.

---

# Section 4: Bad Database Design - Anomalies and Redundancy

Consider the following unnormalized business table.

**EMPLOYEE_DEPARTMENT**

| Emp_ID | Emp_Name | Dept_ID | Dept_Name | Dept_Location |
| --- | --- | --- | --- | --- |
| 101 | Arun | D01 | IT | Chennai |
| 102 | Banu | D01 | IT | Chennai |
| 103 | Charan | D02 | HR | Bengaluru |
| 104 | Divya | D02 | HR | Bengaluru |

Business rules:

- Emp_ID identifies an employee.
- Dept_ID identifies a department.
- Each employee belongs to one department.

### Q31. The department name IT is stored repeatedly for multiple employees. Which problem is present?

A. Data redundancy
B. Entity integrity
C. Referential integrity
D. Domain integrity

**Answer: A**

### Q32. The IT department changes its name to Technology. Only employee 101's record is updated.

What happens?

A. Insertion anomaly
B. Update anomaly
C. Deletion anomaly
D. No anomaly

**Answer: B**

### Q33. A new department D03 is created, but it has no employees. The current table cannot store the department without inserting an employee record.

Which anomaly is present?

A. Update anomaly
B. Deletion anomaly
C. Insertion anomaly
D. Referential anomaly

**Answer: C**

### Q34. Employee 103 is the only employee in the HR department. When employee 103 is deleted, the only stored record of the HR department is also lost.

Which anomaly occurs?

A. Insertion
B. Update
C. Deletion
D. No anomaly

**Answer: C**

### Q35. Which decomposition best addresses the redundancy in the above table?

A. EMPLOYEE(Emp_ID, Emp_Name, Dept_ID); DEPARTMENT(Dept_ID, Dept_Name, Dept_Location)
B. EMPLOYEE(Emp_ID, Emp_Name); DEPARTMENT(Emp_Name, Dept_Name)
C. EMPLOYEE(Dept_ID, Emp_Name); DEPARTMENT(Emp_ID, Dept_Location)
D. Keep the original table and add an index.

**Answer: A**

### Q36. Consider:

| Student_ID | Course_ID | Student_Name | Course_Name | Grade |
| --- | --- | --- | --- | --- |
| S01 | C01 | Arun | DBMS | A |
| S01 | C02 | Arun | Java | B |
| S02 | C01 | Banu | DBMS | A |

Primary key: `(Student_ID, Course_ID)`.

Which redundancy occurs?

A. Student_Name repeats because it depends only on Student_ID.
B. Course_Name repeats because it depends only on Student_ID.
C. Grade repeats because it depends only on Course_ID.
D. No redundancy exists.

**Answer: A**

### Q37. Consider a table storing:

`Order_ID, Product_ID, Product_Name, Quantity`

An order contains several products. Product_ID determines Product_Name.

What problem occurs if Product_Name changes?

A. Every occurrence of that product name may require an update.
B. The order's primary key becomes invalid.
C. The product cannot be inserted.
D. Referential integrity is automatically violated.

**Answer: A**

### Q38. Which of the following is the most accurate statement?

A. Normalization eliminates every form of data redundancy.
B. Normalization organizes attributes and relations to reduce undesirable redundancy and anomalies.
C. Normalization always increases redundancy.
D. Normalization guarantees that no joins are needed.

**Answer: B**

---

# Section 5: Normalization Fundamentals - 1NF, 2NF and 3NF

### Q39. What is the primary requirement of First Normal Form (1NF)?

A. Every non-key attribute must depend on the complete primary key.
B. Every attribute must contain atomic values, with no repeating groups.
C. Every non-key attribute must depend directly on the primary key.
D. Every determinant must be a candidate key.

**Answer: B**

**Explanation:** 1NF requires atomic attribute values and no repeating groups or multivalued fields within a single cell.

### Q40. Consider:

| Student_ID | Student_Name | Phone_Numbers |
| --- | --- | --- |
| 101 | Arun | 9876, 8765 |
| 102 | Banu | 7654 |

Which requirement of 1NF is violated?

A. Entity integrity
B. Atomicity of attribute values
C. Referential integrity
D. Transitive dependency

**Answer: B**

### Q41. Which transformation correctly converts the following table into 1NF?

Original:

| Student_ID | Name | Course |
| --- | --- | --- |
| 101 | Arun | DBMS, Java |
| 102 | Banu | Python |

A.

| Student_ID | Name | Course |
| --- | --- | --- |
| 101 | Arun | DBMS |
| 101 | Arun | Java |
| 102 | Banu | Python |

B.

| Student_ID | Name | Course |
| --- | --- | --- |
| 101 | Arun | DBMS, Java |
| 102 | Banu | Python |

C.

| Student_ID | Name | Course |
| --- | --- | --- |
| 101 | Arun | DBMS |
| 102 | Banu | Python |

D. Delete the Course column.

**Answer: A**

### Q42. A table is in 1NF. Its primary key is `(Student_ID, Course_ID)`. Student_Name depends only on Student_ID.

Which normal form is violated?

A. 1NF
B. 2NF
C. 3NF only
D. No normal form is violated

**Answer: B**

**Explanation:** A non-prime attribute has a partial dependency on a proper subset of the composite candidate key.

### Q43. Which condition is required for a relation to be in 2NF?

A. It must be in 1NF and have no partial dependency of non-prime attributes on any candidate key.
B. It must contain no foreign keys.
C. It must have exactly one candidate key.
D. It must have no functional dependencies.

**Answer: A**

### Q44. A table has a single-attribute primary key `Employee_ID`.

Dependencies:

- Employee_ID → Employee_Name
- Employee_ID → Dept_ID
- Dept_ID → Dept_Name

The table is in 2NF but violates which normal form?

A. 1NF
B. 2NF
C. 3NF
D. None

**Answer: C**

**Explanation:** There cannot be a partial dependency on a single-attribute key. However, Dept_ID → Dept_Name creates a transitive dependency.

### Q45. Which condition correctly describes 3NF?

A. Every determinant must be a primary key.
B. For every non-trivial FD X → A, X must be a superkey or A must be a prime attribute.
C. Every relation must have a single-column primary key.
D. No relation can contain foreign keys.

**Answer: B**

**Explanation:** This is the formal 3NF condition. It is more precise than simply saying that transitive dependencies must be removed.

### Q46. Consider:

`EMPLOYEE(Emp_ID, Emp_Name, Dept_ID, Dept_Name)`

Dependencies:

- Emp_ID → Emp_Name, Dept_ID
- Dept_ID → Dept_Name

Assume the table is in 1NF.

Which decomposition produces 3NF?

A. EMPLOYEE(Emp_ID, Emp_Name, Dept_ID); DEPARTMENT(Dept_ID, Dept_Name)
B. EMPLOYEE(Emp_ID, Emp_Name); DEPARTMENT(Dept_Name, Dept_ID)
C. EMPLOYEE(Emp_ID, Dept_Name); DEPARTMENT(Emp_Name, Dept_ID)
D. EMPLOYEE(Emp_ID, Emp_Name, Dept_Name); DEPARTMENT(Dept_ID)

**Answer: A**

### Q47. A relation is in 3NF. Which statement must be true?

A. It is also in 2NF and 1NF.
B. It must have no foreign keys.
C. It cannot contain any composite candidate keys.
D. Every attribute must be part of a candidate key.

**Answer: A**

### Q48. Consider a relation with a composite candidate key `(A, B)` and another candidate key `C`.

Given:

- A → D
- C → E

Which statement is correct regarding 2NF?

A. A → D violates 2NF because A is a proper subset of candidate key AB and D is non-prime.
B. C → E violates 2NF because C is a candidate key.
C. Both dependencies violate 2NF.
D. Neither dependency can affect 2NF.

**Answer: A**

**Explanation:** 2NF must be checked against every candidate key, not only the selected primary key. A is a proper subset of AB. C is itself a complete candidate key, so C → E is not partial.

---

# Section 6: Identify the Normal Form and Correct Decomposition

For these questions, assume all tables are already in 1NF unless otherwise mentioned.

### Q49. Consider:

`R(A, B, C)`

Primary key: AB.

FDs:

- AB → C
- A → C

What is the highest normal form?

A. 1NF only
B. 2NF
C. 3NF
D. Not even 1NF

**Answer: A**

**Explanation:** C is non-prime and partially depends on A, which is a proper subset of the candidate key AB. Thus 2NF is violated.

### Q50. Consider:

`R(A, B, C)`

Primary key: A.

FDs:

- A → B
- B → C

What is the highest normal form?

A. 1NF
B. 2NF
C. 3NF
D. None

**Answer: B**

**Explanation:** A is a single-attribute key, so partial dependency is impossible. But B → C causes a transitive dependency of C on A.

### Q51. Consider:

`R(A, B, C)`

Primary key: AB.

FDs:

- AB → C
- C → A

What is the highest normal form?

A. 1NF
B. 2NF
C. 3NF
D. Not in 1NF

**Answer: C**

**Explanation:**

Candidate keys:

- AB
- BC

All attributes are prime because each appears in at least one candidate key.

For C → A:

- C is not a superkey.
- A is a prime attribute.

Therefore, the FD satisfies 3NF.

### Q52. Consider:

`EMPLOYEE(Emp_ID, Emp_Name, Dept_ID, Dept_Name)`

FDs:

- Emp_ID → Emp_Name, Dept_ID
- Dept_ID → Dept_Name

What is the highest normal form?

A. 1NF
B. 2NF
C. 3NF
D. 4NF

**Answer: B**

### Q53. Consider:

`ENROLLMENT(Student_ID, Course_ID, Grade)`

Primary key: `(Student_ID, Course_ID)`.

FD:

- (Student_ID, Course_ID) → Grade

Assuming there are no other non-trivial functional dependencies, what is the highest normal form?

A. 1NF
B. 2NF only
C. 3NF
D. Not in 1NF

**Answer: C**

**Explanation:** Grade depends on the complete composite key. There are no partial or transitive dependencies.

### Q54. Consider:

`R(A, B, C, D)`

Candidate key: A.

FDs:

- A → B
- B → C
- C → D

What is the highest normal form?

A. 1NF
B. 2NF
C. 3NF
D. Not in 1NF

**Answer: B**

### Q55. Consider:

`R(A, B, C, D)`

Candidate keys:

- AB
- AC

FDs:

- AB → D
- AC → D
- B → C

Which normal form is violated?

A. 1NF only
B. 2NF
C. 3NF only
D. Neither 2NF nor 3NF

**Answer: B**

**Explanation:**

All attributes are prime except D.

B is a proper subset of candidate key AB, and B → C.

C is prime, so this dependency does not violate 2NF. However, check D: it is fully dependent on AB and AC.

There is no partial dependency of a non-prime attribute. Therefore, the relation actually satisfies 2NF. The dependency B → C satisfies 3NF because C is prime.

**Correct answer: D. Neither 2NF nor 3NF.**

### Q56. Consider:

`R(A, B, C)`

Candidate keys: AB and AC.

FD:

- B → C

Which is the highest normal form?

A. 1NF only
B. 2NF
C. 3NF
D. BCNF

**Answer: C**

**Explanation:** All attributes A, B and C are prime because they appear in candidate keys AB and AC. B is not a superkey, but C is prime, so the FD satisfies 3NF.

### Q57. Consider:

`R(A, B, C, D)`

Primary key: AB.

FDs:

- AB → C
- C → D

Which is the correct decomposition to remove the transitive dependency?

A. R1(A, B, C), R2(C, D)
B. R1(A, B), R2(A, D)
C. R1(A, C), R2(B, D)
D. R1(A, B, C, D), R2(C)

**Answer: A**

### Q58. Consider:

`R(Student_ID, Course_ID, Student_Name, Course_Name, Grade)`

Primary key: `(Student_ID, Course_ID)`.

FDs:

- Student_ID → Student_Name
- Course_ID → Course_Name
- (Student_ID, Course_ID) → Grade

Which is the correct 2NF decomposition?

A. STUDENT(Student_ID, Student_Name); COURSE(Course_ID, Course_Name); ENROLLMENT(Student_ID, Course_ID, Grade)
B. STUDENT(Student_ID, Course_ID, Student_Name); COURSE(Course_ID, Course_Name); ENROLLMENT(Grade)
C. STUDENT(Student_ID, Student_Name, Course_Name); COURSE(Course_ID, Grade)
D. STUDENT(Student_ID, Student_Name); COURSE(Course_ID, Course_Name, Grade)

**Answer: A**

### Q59. Consider:

`ORDER_DETAILS(Order_ID, Product_ID, Quantity, Product_Name, Category_ID, Category_Name)`

Primary key: `(Order_ID, Product_ID)`.

FDs:

- (Order_ID, Product_ID) → Quantity
- Product_ID → Product_Name, Category_ID
- Category_ID → Category_Name

Which decomposition removes both partial and transitive dependencies?

A. ORDER_DETAILS(Order_ID, Product_ID, Quantity); PRODUCT(Product_ID, Product_Name, Category_ID); CATEGORY(Category_ID, Category_Name)
B. ORDER_DETAILS(Order_ID, Product_ID, Quantity, Product_Name); CATEGORY(Category_ID, Category_Name)
C. ORDER_DETAILS(Order_ID, Product_ID, Category_Name); PRODUCT(Product_ID, Product_Name)
D. ORDER_DETAILS(Order_ID, Product_ID, Quantity); PRODUCT(Product_ID, Category_Name)

**Answer: A**

### Q60. A table is already in 2NF. It contains:

`R(A, B, C, D)`

Primary key: A.

FDs:

- A → B
- B → C
- C → D

Which decomposition is a valid 3NF decomposition?

A. R1(A, B), R2(B, C), R3(C, D)
B. R1(A, B, C), R2(A, D)
C. R1(A, C), R2(B, D)
D. R1(A, B, C, D) only

**Answer: A**

**Explanation:** Each relation represents one direct dependency. The transitive chain is separated, and the original key A is retained in R1.

---

# Section 7: 10 Practical Normalization Problems - Decompose Up to 3NF

(Expert Practical Problems)

These are table-based problems. For every question:

1. Identify the candidate key.
2. Identify the functional dependencies.
3. Determine the current normal form.
4. Identify partial and transitive dependencies.
5. Decompose into 1NF, 2NF and 3NF.
6. Identify primary keys and foreign keys in the final tables.

The solutions are provided immediately after each problem.

---

## Problem 1: Student - Course - Department

**Given table: STUDENT_COURSE**

| Student_ID | Student_Name | Course_ID | Course_Name | Dept_ID | Dept_Name | Grade |
| --- | --- | --- | --- | --- | --- | --- |
| S01 | Arun | C01 | DBMS | D01 | CSE | A |
| S01 | Arun | C02 | Java | D02 | IT | B |
| S02 | Banu | C01 | DBMS | D01 | CSE | A |
| S03 | Charan | C03 | Python | D01 | CSE | B |

Business rules:

- A student can enroll in multiple courses.
- A course belongs to one department.
- A department has multiple courses.
- Each student receives one grade per course.

Functional dependencies:

- Student_ID → Student_Name
- Course_ID → Course_Name, Dept_ID
- Dept_ID → Dept_Name
- (Student_ID, Course_ID) → Grade

**Question:** Decompose this table up to 3NF.

**Solution:**

Candidate key: `(Student_ID, Course_ID)`

**1NF:** All values are atomic, so the table is in 1NF.

**2NF:** Remove partial dependencies:

- Student_ID → Student_Name
- Course_ID → Course_Name, Dept_ID, Dept_Name

Create:

STUDENT:

| Student_ID (PK) | Student_Name |
| --- | --- |
| S01 | Arun |
| S02 | Banu |
| S03 | Charan |

COURSE:

| Course_ID (PK) | Course_Name | Dept_ID | Dept_Name |
| --- | --- | --- | --- |
| C01 | DBMS | D01 | CSE |
| C02 | Java | D02 | IT |
| C03 | Python | D01 | CSE |

ENROLLMENT:

| Student_ID (PK, FK) | Course_ID (PK, FK) | Grade |
| --- | --- | --- |
| S01 | C01 | A |
| S01 | C02 | B |
| S02 | C01 | A |
| S03 | C03 | B |

**3NF:** Remove the transitive dependency:

Dept_ID → Dept_Name.

Final tables:

- STUDENT(Student_ID PK, Student_Name)
- DEPARTMENT(Dept_ID PK, Dept_Name)
- COURSE(Course_ID PK, Course_Name, Dept_ID FK)
- ENROLLMENT(Student_ID PK/FK, Course_ID PK/FK, Grade)

---

## Problem 2: Employee - Department - Location

**Given table: EMPLOYEE**

| Emp_ID | Emp_Name | Dept_ID | Dept_Name | Location_ID | Location_Name |
| --- | --- | --- | --- | --- | --- |
| E01 | Arun | D01 | IT | L01 | Chennai |
| E02 | Banu | D01 | IT | L01 | Chennai |
| E03 | Charan | D02 | HR | L02 | Bengaluru |
| E04 | Divya | D03 | Finance | L03 | Hyderabad |

FDs:

- Emp_ID → Emp_Name, Dept_ID
- Dept_ID → Dept_Name, Location_ID
- Location_ID → Location_Name

**Question:** Decompose up to 3NF.

**Solution:**

Candidate key: Emp_ID.

1NF: Already satisfied.

2NF: No partial dependency because the key is a single attribute.

3NF: Remove transitive dependencies:

- Emp_ID → Dept_ID
- Dept_ID → Location_ID
- Location_ID → Location_Name

Final tables:

**EMPLOYEE**

| Emp_ID (PK) | Emp_Name | Dept_ID (FK) |
| --- | --- | --- |
| E01 | Arun | D01 |
| E02 | Banu | D01 |
| E03 | Charan | D02 |
| E04 | Divya | D03 |

**DEPARTMENT**

| Dept_ID (PK) | Dept_Name | Location_ID (FK) |
| --- | --- | --- |
| D01 | IT | L01 |
| D02 | HR | L02 |
| D03 | Finance | L03 |

**LOCATION**

| Location_ID (PK) | Location_Name |
| --- | --- |
| L01 | Chennai |
| L02 | Bengaluru |
| L03 | Hyderabad |

---

## Problem 3: Order - Product - Supplier

**Given table: ORDER_DETAILS**

| Order_ID | Product_ID | Product_Name | Supplier_ID | Supplier_Name | Quantity |
| --- | --- | --- | --- | --- | --- |
| O01 | P01 | Laptop | S01 | Dell | 2 |
| O01 | P02 | Mouse | S02 | Logitech | 5 |
| O02 | P01 | Laptop | S01 | Dell | 1 |
| O03 | P03 | Keyboard | S02 | Logitech | 3 |

FDs:

- (Order_ID, Product_ID) → Quantity
- Product_ID → Product_Name, Supplier_ID
- Supplier_ID → Supplier_Name

**Question:** Decompose up to 3NF.

**Solution:**

Candidate key: `(Order_ID, Product_ID)`.

Partial dependencies:

- Product_ID → Product_Name
- Product_ID → Supplier_ID

Transitive dependency:

- Supplier_ID → Supplier_Name

Final 3NF tables:

**ORDERS**

| Order_ID (PK) |
| --- |
| O01 |
| O02 |
| O03 |

**SUPPLIER**

| Supplier_ID (PK) | Supplier_Name |
| --- | --- |
| S01 | Dell |
| S02 | Logitech |

**PRODUCT**

| Product_ID (PK) | Product_Name | Supplier_ID (FK) |
| --- | --- | --- |
| P01 | Laptop | S01 |
| P02 | Mouse | S02 |
| P03 | Keyboard | S02 |

**ORDER_DETAILS**

| Order_ID (PK, FK) | Product_ID (PK, FK) | Quantity |
| --- | --- | --- |
| O01 | P01 | 2 |
| O01 | P02 | 5 |
| O02 | P01 | 1 |
| O03 | P03 | 3 |

---

## Problem 4: Hospital - Doctor - Department

**Given table: DOCTOR_PATIENT**

| Doctor_ID | Doctor_Name | Dept_ID | Dept_Name | Patient_ID | Patient_Name | Diagnosis |
| --- | --- | --- | --- | --- | --- | --- |
| D01 | Ravi | DP01 | Cardiology | P01 | Arun | BP |
| D01 | Ravi | DP01 | Cardiology | P02 | Banu | Heart |
| D02 | Kumar | DP02 | Neurology | P01 | Arun | Migraine |
| D03 | Meena | DP01 | Cardiology | P03 | Charan | BP |

FDs:

- Doctor_ID → Doctor_Name, Dept_ID
- Dept_ID → Dept_Name
- Patient_ID → Patient_Name
- (Doctor_ID, Patient_ID) does not uniquely identify a visit if the same patient can visit the same doctor multiple times.

Assume each visit is uniquely identified by Visit_ID, and:

- Visit_ID → Doctor_ID, Patient_ID, Diagnosis

**Question:** What is the correct 3NF design?

**Solution:**

Candidate keys:

- DOCTOR: Doctor_ID
- DEPARTMENT: Dept_ID
- PATIENT: Patient_ID
- VISIT: Visit_ID

Final tables:

- DOCTOR(Doctor_ID PK, Doctor_Name, Dept_ID FK)
- DEPARTMENT(Dept_ID PK, Dept_Name)
- PATIENT(Patient_ID PK, Patient_Name)
- VISIT(Visit_ID PK, Doctor_ID FK, Patient_ID FK, Diagnosis)

**Important:** A composite key based on Doctor_ID and Patient_ID would be insufficient if repeated visits are allowed.

---

## Problem 5: Company Project Allocation

**Given table: EMPLOYEE_PROJECT**

| Emp_ID | Emp_Name | Project_ID | Project_Name | Manager_ID | Manager_Name | Hours |
| --- | --- | --- | --- | --- | --- | --- |
| E01 | Arun | P01 | ERP | M01 | Ravi | 20 |
| E01 | Arun | P02 | CRM | M02 | Kumar | 15 |
| E02 | Banu | P01 | ERP | M01 | Ravi | 25 |
| E03 | Charan | P02 | CRM | M02 | Kumar | 30 |

FDs:

- Emp_ID → Emp_Name
- Project_ID → Project_Name, Manager_ID
- Manager_ID → Manager_Name
- (Emp_ID, Project_ID) → Hours

**Question:** Normalize up to 3NF.

**Solution:**

Candidate key: `(Emp_ID, Project_ID)`.

Partial dependencies:

- Emp_ID → Emp_Name
- Project_ID → Project_Name, Manager_ID

Transitive dependency:

- Manager_ID → Manager_Name

Final tables:

- EMPLOYEE(Emp_ID PK, Emp_Name)
- MANAGER(Manager_ID PK, Manager_Name)
- PROJECT(Project_ID PK, Project_Name, Manager_ID FK)
- EMPLOYEE_PROJECT(Emp_ID PK/FK, Project_ID PK/FK, Hours)

---

## Problem 6: Student Examination Results

**Given table: EXAM_RESULT**

| Student_ID | Subject_ID | Exam_ID | Student_Name | Subject_Name | Exam_Date | Marks |
| --- | --- | --- | --- | --- | --- | --- |
| S01 | SUB01 | E01 | Arun | DBMS | 10-01-2026 | 90 |
| S01 | SUB02 | E01 | Arun | Java | 10-01-2026 | 85 |
| S02 | SUB01 | E01 | Banu | DBMS | 10-01-2026 | 88 |
| S01 | SUB01 | E02 | Arun | DBMS | 15-02-2026 | 95 |

Business rules:

- Student_ID identifies students.
- Subject_ID identifies subjects.
- Exam_ID identifies an exam session.
- A student's marks are recorded for each subject in each exam session.

FDs:

- Student_ID → Student_Name
- Subject_ID → Subject_Name
- Exam_ID → Exam_Date
- (Student_ID, Subject_ID, Exam_ID) → Marks

**Question:** Decompose up to 3NF.

**Solution:**

Candidate key: `(Student_ID, Subject_ID, Exam_ID)`.

All three descriptive dependencies are partial because each depends on one component of the composite key.

Final tables:

- STUDENT(Student_ID PK, Student_Name)
- SUBJECT(Subject_ID PK, Subject_Name)
- EXAM(Exam_ID PK, Exam_Date)
- EXAM_RESULT(Student_ID PK/FK, Subject_ID PK/FK, Exam_ID PK/FK, Marks)

---

## Problem 7: Banking Transaction System

**Given table: TRANSACTION_DETAILS**

| Transaction_ID | Account_ID | Customer_ID | Customer_Name | Branch_ID | Branch_Name | Amount |
| --- | --- | --- | --- | --- | --- | --- |
| T01 | A01 | C01 | Arun | B01 | Chennai | 5000 |
| T02 | A01 | C01 | Arun | B01 | Chennai | 2000 |
| T03 | A02 | C02 | Banu | B02 | Bengaluru | 3000 |
| T04 | A03 | C01 | Arun | B01 | Chennai | 1000 |

Business rules:

- Account_ID identifies an account.
- Customer_ID identifies a customer.
- Branch_ID identifies a branch.
- Transaction_ID identifies a transaction.
- Each account belongs to one customer and one branch.

FDs:

- Transaction_ID → Account_ID, Amount
- Account_ID → Customer_ID, Branch_ID
- Customer_ID → Customer_Name
- Branch_ID → Branch_Name

**Question:** Normalize up to 3NF.

**Solution:**

Candidate key: Transaction_ID.

There are no partial dependencies because the key is a single attribute.

Transitive dependencies:

- Transaction_ID → Account_ID → Customer_ID → Customer_Name
- Transaction_ID → Account_ID → Branch_ID → Branch_Name

Final tables:

- CUSTOMER(Customer_ID PK, Customer_Name)
- BRANCH(Branch_ID PK, Branch_Name)
- ACCOUNT(Account_ID PK, Customer_ID FK, Branch_ID FK)
- TRANSACTION(Transaction_ID PK, Account_ID FK, Amount)

---

## Problem 8: Online Shopping with Category

**Given table: PRODUCT_ORDER**

| Order_ID | Product_ID | Product_Name | Category_ID | Category_Name | Quantity | Price |
| --- | --- | --- | --- | --- | --- | --- |
| O01 | P01 | Laptop | C01 | Electronics | 1 | 50000 |
| O01 | P02 | Mouse | C01 | Electronics | 2 | 500 |
| O02 | P03 | Chair | C02 | Furniture | 1 | 3000 |
| O03 | P01 | Laptop | C01 | Electronics | 1 | 50000 |

FDs:

- Product_ID → Product_Name, Category_ID, Price
- Category_ID → Category_Name
- (Order_ID, Product_ID) → Quantity

**Question:** Decompose into 3NF.

**Solution:**

Candidate key: `(Order_ID, Product_ID)`.

Partial dependency:

Product_ID → Product_Name, Category_ID, Price.

Transitive dependency:

Category_ID → Category_Name.

Final tables:

- CATEGORY(Category_ID PK, Category_Name)
- PRODUCT(Product_ID PK, Product_Name, Category_ID FK, Price)
- ORDERS(Order_ID PK)
- ORDER_ITEM(Order_ID PK/FK, Product_ID PK/FK, Quantity)

---

## Problem 9: University - Faculty - Course Allocation

**Given table: FACULTY_COURSE**

| Faculty_ID | Faculty_Name | Department_ID | Department_Name | Course_ID | Course_Name | Semester |
| --- | --- | --- | --- | --- | --- | --- |
| F01 | Ravi | D01 | CSE | C01 | DBMS | 1 |
| F01 | Ravi | D01 | CSE | C02 | Java | 2 |
| F02 | Kumar | D02 | IT | C03 | Python | 1 |
| F03 | Meena | D01 | CSE | C01 | DBMS | 2 |

Business rules:

- Faculty_ID determines Faculty_Name and Department_ID.
- Department_ID determines Department_Name.
- Course_ID determines Course_Name.
- A faculty member can teach a course in multiple semesters.
- A faculty-course-semester combination uniquely identifies an allocation.

FDs:

- Faculty_ID → Faculty_Name, Department_ID
- Department_ID → Department_Name
- Course_ID → Course_Name
- (Faculty_ID, Course_ID, Semester) → Allocation

**Question:** Decompose up to 3NF.

**Solution:**

Candidate key: `(Faculty_ID, Course_ID, Semester)`.

Partial dependencies:

- Faculty_ID → Faculty_Name, Department_ID
- Course_ID → Course_Name

Transitive dependency:

- Department_ID → Department_Name

Final tables:

- DEPARTMENT(Department_ID PK, Department_Name)
- FACULTY(Faculty_ID PK, Faculty_Name, Department_ID FK)
- COURSE(Course_ID PK, Course_Name)
- FACULTY_COURSE(Faculty_ID PK/FK, Course_ID PK/FK, Semester PK)

---

## Problem 10: Vehicle Insurance System

**Given table: INSURANCE**

| Policy_ID | Vehicle_ID | Registration_No | Owner_ID | Owner_Name | Agent_ID | Agent_Name | Premium |
| --- | --- | --- | --- | --- | --- | --- | --- |
| P01 | V01 | TN01 | O01 | Arun | A01 | Ravi | 10000 |
| P02 | V02 | TN02 | O02 | Banu | A02 | Kumar | 12000 |
| P03 | V01 | TN01 | O01 | Arun | A01 | Ravi | 9000 |
| P04 | V03 | KA01 | O03 | Charan | A01 | Ravi | 11000 |

Business rules:

- Policy_ID uniquely identifies a policy.
- Vehicle_ID identifies a vehicle.
- Owner_ID identifies an owner.
- Agent_ID identifies an insurance agent.
- A vehicle has one owner.
- An agent can handle multiple policies.
- Each policy has one vehicle and one agent.

FDs:

- Policy_ID → Vehicle_ID, Agent_ID, Premium
- Vehicle_ID → Registration_No, Owner_ID
- Owner_ID → Owner_Name
- Agent_ID → Agent_Name

**Question:** Decompose up to 3NF.

**Solution:**

Candidate key: Policy_ID.

Partial dependencies: None.

Transitive dependencies:

- Policy_ID → Vehicle_ID → Registration_No, Owner_ID
- Policy_ID → Vehicle_ID → Owner_ID → Owner_Name
- Policy_ID → Agent_ID → Agent_Name

Final tables:

- OWNER(Owner_ID PK, Owner_Name)
- VEHICLE(Vehicle_ID PK, Registration_No, Owner_ID FK)
- AGENT(Agent_ID PK, Agent_Name)
- INSURANCE_POLICY(Policy_ID PK, Vehicle_ID FK, Agent_ID FK, Premium)

---

# Final Revision: Normalization Decision Table

| Normal form | What to identify | What to eliminate |
| --- | --- | --- |
| 1NF | Atomic values | Repeating groups and multivalued cells |
| 2NF | Complete candidate keys | Partial dependencies of non-prime attributes |
| 3NF | Direct dependency structure | Transitive dependencies, subject to the formal 3NF rule |

## Expert-level examination traps

1. **Partial dependency:** A non-prime attribute depends on a proper subset of a candidate key.
2. **Full dependency:** Removing any attribute from the determinant makes it insufficient to determine the dependent attribute.
3. **Transitive dependency:** A non-key determinant determines another non-key attribute, creating an indirect dependency from a candidate key.
4. **2NF:** Check all candidate keys, not just the selected primary key.
5. **3NF:** Remember the prime-attribute exception in the formal definition.
6. **1NF:** Atomicity is relative to the intended domain; it does not mean a string can never contain spaces or punctuation.
7. **Decomposition:** Preserve the original information and relationships through appropriate keys and joins.
8. **Candidate key:** Calculate attribute closure and verify minimality.
9. **Normalization:** A single-column candidate key cannot have a partial dependency.
10. **3NF decomposition:** A transitive chain such as A → B → C can be separated into relations for A-B and B-C, while preserving the original key.

---

## Corrections to the 60-MCQ answer key

Two important answer-key corrections:

- **Q28:** Correct answer is **B (AB)**. AB is a candidate key because it determines all five attributes and neither A nor B alone does.
- **Q55:** Correct answer is **D (Neither 2NF nor 3NF)**. All attributes are prime, and the given dependency B → C does not violate 3NF. There is also no partial dependency of a non-prime attribute.

**Recommended solving order:** First master candidate-key closure, then classify full/partial/transitive dependencies, and finally practice decomposing tables. These three skills form the foundation for solving most 1NF-3NF normalization problems.

### User

what is a view syntax of view views example grant select on view revoke select on view dml on view dmls on view will dml on view update the original table what will happen drop view advantages disadvantages of views give 60 question expert level mcq dont give in quiz interface advanced tricky give

### ChatGPT

# DBMS - SQL Views: 60 Advanced & Expert-Level MCQs

(Advanced-Expert) (60 Questions · Set 1)

**Scope strictly limited to SQL Views:**

| Section | Topics | Questions |
| --- | --- | --- |
| 1 | View fundamentals, purpose and syntax | 1-10 |
| 2 | CREATE VIEW, column aliases, complex views | 11-18 |
| 3 | GRANT and REVOKE on views | 19-26 |
| 4 | DML operations on views | 27-40 |
| 5 | DML on views and original tables | 41-48 |
| 6 | DROP VIEW, dependencies and limitations | 49-54 |
| 7 | Advantages, disadvantages and tricky scenarios | 55-60 |

Questions include four options, answers and explanations immediately after each question.

*SQL examples use standard SQL principles. Some DML and privilege details can vary between DBMS implementations, particularly HSQLDB.*

---

# Section 1: View Fundamentals

### Q1. What is a view in SQL?

A. A physical copy of an existing table
B. A virtual table based on the result of a query
C. A temporary database
D. A database index

**Answer: B**

**Explanation:** A conventional view stores a query definition, not a separate copy of the underlying table data. When queried, its result is derived from the underlying objects.

### Q2. Which statement creates a view?

A.

```sql
CREATE TABLE V1 AS SELECT * FROM EMPLOYEE;
```

B.

```sql
CREATE VIEW V1 AS SELECT * FROM EMPLOYEE;
```

C.

```sql
INSERT VIEW V1 SELECT * FROM EMPLOYEE;
```

D.

```sql
ALTER VIEW V1 AS EMPLOYEE;
```

**Answer: B**

**Explanation:** CREATE VIEW defines a virtual table using a SELECT query.

### Q3. Consider:

```sql
CREATE VIEW IT_EMP AS
SELECT Emp_ID, Emp_Name
FROM EMPLOYEE
WHERE Dept_ID = 10;
```

What does IT_EMP contain?

A. A physical copy of all EMPLOYEE records
B. Only employee IDs and names satisfying Dept_ID = 10 when the view is queried
C. Only the original EMPLOYEE primary key
D. A separate database table containing duplicated data

**Answer: B**

### Q4. Which statement about a conventional view is correct?

A. It always occupies the same storage as a base table.
B. It stores the SELECT definition and derives its result from underlying data.
C. It cannot be queried using SELECT.
D. It must contain a primary key.

**Answer: B**

### Q5. Consider:

```sql
CREATE VIEW EMP_VIEW AS
SELECT *
FROM EMPLOYEE;
```

The DBA inserts a new record into EMPLOYEE.

What happens when EMP_VIEW is queried again?

A. The new record is never visible.
B. The view automatically contains the newly inserted record if it satisfies the view definition.
C. The view must be recreated.
D. The new record is copied into a separate view table.

**Answer: B**

### Q6. Which command retrieves data from a view?

A.

```sql
GET EMP_VIEW;
```

B.

```sql
SELECT * FROM EMP_VIEW;
```

C.

```sql
SHOW VIEW EMP_VIEW;
```

D.

```sql
FETCH VIEW EMP_VIEW;
```

**Answer: B**

### Q7. A view is created using:

```sql
CREATE VIEW EMP_SALARY AS
SELECT Emp_ID, Salary
FROM EMPLOYEE;
```

Which statement is correct?

A. EMP_SALARY and EMPLOYEE are independent physical copies.
B. EMP_SALARY reads data from the underlying EMPLOYEE table.
C. EMPLOYEE automatically becomes a view.
D. The original table is deleted.

**Answer: B**

### Q8. Which of the following is a valid purpose of a view?

A. Restricting users to selected columns of a table
B. Automatically creating a backup of every row
C. Guaranteeing that duplicate records cannot exist
D. Replacing the database transaction manager

**Answer: A**

### Q9. Consider:

```sql
CREATE VIEW EMP_VIEW AS
SELECT Emp_ID, Emp_Name
FROM EMPLOYEE;
```

Can a user query only Emp_Name from the view?

A. No, all columns must be selected.
B. Yes, using `SELECT Emp_Name FROM EMP_VIEW`.
C. Only if EMP_VIEW is converted into a table.
D. Only if Emp_ID is a foreign key.

**Answer: B**

### Q10. Which statement is true about the relationship between views and base tables?

A. Every view must be created from exactly one table.
B. A view can be defined using multiple tables through joins.
C. A view cannot contain a WHERE clause.
D. A view cannot contain aggregate functions.

**Answer: B**

---

# Section 2: CREATE VIEW - Syntax and Complex Examples

For Q11-Q15, assume these tables:

**EMPLOYEE**

| Emp_ID | Emp_Name | Dept_ID | Salary |
| --- | --- | --- | --- |
| 101 | Arun | 10 | 50000 |
| 102 | Banu | 20 | 60000 |
| 103 | Charan | 10 | 55000 |
| 104 | Divya | 30 | 70000 |

**DEPARTMENT**

| Dept_ID | Dept_Name |
| --- | --- |
| 10 | IT |
| 20 | HR |
| 30 | Finance |

### Q11. Which statement correctly creates a view containing employees earning more than 55000?

A.

```sql
CREATE VIEW HIGH_SALARY AS
SELECT *
FROM EMPLOYEE
WHERE Salary > 55000;
```

B.

```sql
CREATE TABLE HIGH_SALARY AS
VIEW EMPLOYEE;
```

C.

```sql
CREATE VIEW HIGH_SALARY
FROM EMPLOYEE
WHERE Salary > 55000;
```

D.

```sql
SELECT VIEW HIGH_SALARY
FROM EMPLOYEE;
```

**Answer: A**

### Q12. Consider:

```sql
CREATE VIEW EMP_DEPT AS
SELECT E.Emp_ID, E.Emp_Name, D.Dept_Name
FROM EMPLOYEE E
JOIN DEPARTMENT D
ON E.Dept_ID = D.Dept_ID;
```

How many base tables are referenced by this view?

A. One
B. Two
C. Three
D. Zero

**Answer: B**

### Q13. A DBA creates:

```sql
CREATE VIEW DEPT_SUMMARY AS
SELECT Dept_ID, COUNT(*) AS Emp_Count,
       AVG(Salary) AS Avg_Salary
FROM EMPLOYEE
GROUP BY Dept_ID;
```

Which statement is correct?

A. The view contains one row per employee.
B. The view contains one row per department represented in the query result.
C. The view contains one row per salary.
D. The view stores a physical backup of EMPLOYEE.

**Answer: B**

### Q14. What is the purpose of column aliases in a view?

A. To create primary keys automatically
B. To provide meaningful or different column names in the view
C. To physically rename base table columns
D. To prevent DML operations

**Answer: B**

### Q15. Consider:

```sql
CREATE VIEW EMP_INFO
(Employee_No, Employee_Name)
AS
SELECT Emp_ID, Emp_Name
FROM EMPLOYEE;
```

What are the column names exposed by EMP_INFO?

A. Emp_ID and Emp_Name
B. Employee_No and Employee_Name
C. EMPLOYEE and EMP_INFO
D. Both sets simultaneously as separate columns

**Answer: B**

### Q16. Which clause can be used when creating a view to require its rows to satisfy the view condition during certain DML operations?

A. WITH CHECK OPTION
B. WITH GRANT OPTION
C. WITH INDEX OPTION
D. WITH UPDATE OPTION

**Answer: A**

**Explanation:** WITH CHECK OPTION prevents modifications through the view that would cause the affected row to stop satisfying the view's defining condition. Exact behavior and supported syntax depend on the DBMS.

### Q17. Consider:

```sql
CREATE VIEW IT_EMP AS
SELECT *
FROM EMPLOYEE
WHERE Dept_ID = 10
WITH CHECK OPTION;
```

A user executes:

```sql
UPDATE IT_EMP
SET Dept_ID = 20
WHERE Emp_ID = 101;
```

What happens?

A. The update succeeds, and the employee disappears from IT_EMP.
B. The update is rejected because the row would no longer satisfy the view condition.
C. The employee is deleted from EMPLOYEE.
D. The entire EMPLOYEE table becomes inaccessible.

**Answer: B**

### Q18. Consider:

```sql
CREATE VIEW HIGH_SALARY AS
SELECT *
FROM EMPLOYEE
WHERE Salary > 50000;
```

The view does not contain WITH CHECK OPTION.

A user updates an employee's salary from 60000 to 40000 through the view. Assuming the DBMS supports the update, what happens?

A. The update is necessarily rejected.
B. The base table is updated, and the employee no longer appears in the view.
C. The salary remains 60000.
D. The employee is deleted from the base table.

**Answer: B**

---

# Section 3: GRANT and REVOKE on Views

### Q19. Which statement grants SELECT permission on a view to USER1?

A.

```sql
GRANT SELECT ON EMP_VIEW TO USER1;
```

B.

```sql
GRANT EMP_VIEW SELECT TO USER1;
```

C.

```sql
ALLOW SELECT EMP_VIEW USER1;
```

D.

```sql
GRANT VIEW EMP_VIEW TO USER1;
```

**Answer: A**

### Q20. Which statement revokes SELECT permission on EMP_VIEW from USER1?

A.

```sql
DELETE SELECT ON EMP_VIEW FROM USER1;
```

B.

```sql
REVOKE SELECT ON EMP_VIEW FROM USER1;
```

C.

```sql
DROP SELECT ON EMP_VIEW USER1;
```

D.

```sql
REMOVE VIEW EMP_VIEW FROM USER1;
```

**Answer: B**

### Q21. Consider:

```sql
GRANT SELECT ON EMP_VIEW TO USER1;
```

What permission does USER1 receive?

A. SELECT on every table in the database
B. SELECT on EMP_VIEW
C. UPDATE on EMP_VIEW
D. SELECT and DELETE on EMP_VIEW

**Answer: B**

### Q22. A DBA creates a view:

```sql
CREATE VIEW EMP_PUBLIC AS
SELECT Emp_ID, Emp_Name
FROM EMPLOYEE;
```

Then executes:

```sql
GRANT SELECT ON EMP_PUBLIC TO USER1;
```

What is the primary security advantage?

A. USER1 can automatically access all EMPLOYEE columns.
B. USER1 can be restricted to the columns exposed by the view.
C. USER1 receives UPDATE permission on EMPLOYEE.
D. USER1 becomes the owner of EMPLOYEE.

**Answer: B**

### Q23. A user has SELECT permission on a view but does not have direct SELECT permission on its underlying table.

Can the user query the view?

A. Never
B. It depends on the DBMS's view security and privilege-checking rules; conventional SQL view authorization can permit this when the view owner has the required privileges.
C. Only if the user is the database administrator
D. Only if the view has a primary key

**Answer: B**

**Explanation:** Views can provide controlled access without granting direct access to base tables. SQL authorization behavior depends on ownership, privilege chains and implementation.

### Q24. Which statement is correct about GRANT and REVOKE?

A. GRANT removes permissions.
B. REVOKE creates permissions.
C. GRANT assigns privileges, while REVOKE removes privileges.
D. Both commands delete views.

**Answer: C**

### Q25. Consider:

```sql
GRANT SELECT, UPDATE ON EMP_VIEW TO USER1;
```

What permissions are granted?

A. SELECT only
B. UPDATE only
C. SELECT and UPDATE
D. INSERT and DELETE

**Answer: C**

### Q26. A user has SELECT and UPDATE permissions on a view. The DBA executes:

```sql
REVOKE SELECT ON EMP_VIEW FROM USER1;
```

What is the intended effect?

A. Both SELECT and UPDATE are necessarily revoked.
B. SELECT is revoked, while UPDATE is not directly revoked by this statement.
C. The view is deleted.
D. The base table is dropped.

**Answer: B**

---

# Section 4: DML Operations on Views

(Important exam section)

Remember that DML operations on a view may modify the underlying base table when the view is updatable.

### Q27. Which DML operation can be used on an updatable view?

A. INSERT
B. UPDATE
C. DELETE
D. All of the above, subject to view and DBMS restrictions

**Answer: D**

### Q28. Consider:

```sql
CREATE VIEW IT_EMP AS
SELECT Emp_ID, Emp_Name, Dept_ID
FROM EMPLOYEE
WHERE Dept_ID = 10;
```

Execute:

```sql
UPDATE IT_EMP
SET Emp_Name = 'Arun Kumar'
WHERE Emp_ID = 101;
```

What happens if the view is updatable?

A. Only the view's stored copy is updated.
B. EMPLOYEE.Emp_Name is updated in the original table.
C. A new EMPLOYEE table is created.
D. The update is automatically rejected.

**Answer: B**

### Q29. Consider:

```sql
CREATE VIEW IT_EMP AS
SELECT Emp_ID, Emp_Name, Dept_ID
FROM EMPLOYEE
WHERE Dept_ID = 10;
```

A user executes:

```sql
DELETE FROM IT_EMP
WHERE Emp_ID = 101;
```

What happens if DELETE is supported on this view?

A. The row is deleted from the underlying EMPLOYEE table.
B. The row is deleted only from the view definition.
C. The view itself is deleted.
D. Only the WHERE condition is removed.

**Answer: A**

### Q30. Consider:

```sql
CREATE VIEW EMP_VIEW AS
SELECT Emp_ID, Emp_Name
FROM EMPLOYEE;
```

Can a user insert a row through EMP_VIEW?

A. Never
B. Yes, if the view is updatable and the omitted base-table columns can be supplied through defaults, generated values or nullability rules.
C. Only if the view contains every base-table column.
D. Only if the view contains GROUP BY.

**Answer: B**

### Q31. Consider:

```sql
CREATE VIEW EMP_VIEW AS
SELECT Emp_ID, Emp_Name
FROM EMPLOYEE;
```

The original EMPLOYEE table contains:

- Emp_ID NOT NULL
- Emp_Name NOT NULL
- Salary NOT NULL, with no default

Can a user insert through EMP_VIEW without providing Salary?

A. Always yes
B. No, because the underlying NOT NULL Salary column has no default or generated value
C. Yes, because Salary is hidden
D. Yes, because a view ignores base-table constraints

**Answer: B**

### Q32. Which view is generally the most straightforward candidate for UPDATE operations?

A.

```sql
SELECT Emp_ID, Emp_Name FROM EMPLOYEE;
```

B.

```sql
SELECT Dept_ID, COUNT(*) FROM EMPLOYEE GROUP BY Dept_ID;
```

C.

```sql
SELECT DISTINCT Dept_ID FROM EMPLOYEE;
```

D.

```sql
SELECT Dept_ID, AVG(Salary) FROM EMPLOYEE GROUP BY Dept_ID;
```

**Answer: A**

**Explanation:** A simple single-table projection without aggregation or duplicate elimination is generally updatable.

### Q33. Consider:

```sql
CREATE VIEW DEPT_COUNT AS
SELECT Dept_ID, COUNT(*) AS Total
FROM EMPLOYEE
GROUP BY Dept_ID;
```

Can a user directly update Total using this view?

A. Yes, it updates every employee salary.
B. Yes, it updates the underlying employee count.
C. Generally no, because the aggregate is derived from multiple rows.
D. Yes, if Total is the primary key.

**Answer: C**

### Q34. Which view is generally non-updatable under standard SQL view-update restrictions?

A. A simple projection from one base table
B. A simple selection from one base table
C. A view containing GROUP BY and aggregate functions
D. A view selecting ordinary columns from one table

**Answer: C**

### Q35. Consider:

```sql
CREATE VIEW HIGH_SALARY AS
SELECT Emp_ID, Emp_Name, Salary
FROM EMPLOYEE
WHERE Salary > 50000;
```

A user inserts a record with Salary = 30000 through this view. No CHECK OPTION is specified.

What is the general behavior if the DBMS supports the insert?

A. The insert is rejected because the row fails the view condition.
B. The row may be inserted into EMPLOYEE but will not appear in HIGH_SALARY.
C. The row is inserted with Salary = 50000.
D. The base table is dropped.

**Answer: B**

### Q36. Consider:

```sql
CREATE VIEW IT_EMP AS
SELECT Emp_ID, Emp_Name
FROM EMPLOYEE
WHERE Dept_ID = 10
WITH CHECK OPTION;
```

Can a user insert an employee through IT_EMP without supplying Dept_ID?

A. Yes, and the employee automatically belongs to department 10.
B. Only if the underlying table supplies Dept_ID = 10 through a default or another mechanism.
C. Always no, because views cannot accept INSERT.
D. Yes, because CHECK OPTION creates a default value.

**Answer: B**

### Q37. Consider a view created from two tables using an INNER JOIN:

```sql
CREATE VIEW EMP_DEPT AS
SELECT E.Emp_ID, E.Emp_Name, D.Dept_Name
FROM EMPLOYEE E
JOIN DEPARTMENT D
ON E.Dept_ID = D.Dept_ID;
```

Which statement is most accurate?

A. Every DML operation is always supported.
B. Every DML operation is always prohibited.
C. DML support depends on the DBMS and view structure; a join view generally has restrictions on which underlying table can be modified.
D. Only DELETE is possible in every DBMS.

**Answer: C**

### Q38. Consider:

```sql
CREATE VIEW EMP_VIEW AS
SELECT Emp_ID, Emp_Name
FROM EMPLOYEE
WHERE Dept_ID = 10;
```

A user executes:

```sql
UPDATE EMP_VIEW
SET Emp_Name = 'New Name'
WHERE Emp_ID = 101;
```

Which column of the original table is modified?

A. Emp_ID
B. Emp_Name
C. Dept_ID
D. All three

**Answer: B**

### Q39. A view exposes only Emp_ID and Emp_Name. The underlying table has Emp_ID, Emp_Name, Salary and Dept_ID.

Can a user update Salary through the view?

A. Yes, because Salary exists in the underlying table.
B. Generally no, because Salary is not exposed by the view.
C. Yes, because all base-table columns are automatically exposed.
D. Only if Salary is a primary key.

**Answer: B**

### Q40. Which statement about DELETE through a simple filtered view is correct?

A. Deleting a row through the view deletes the corresponding base-table row.
B. It only hides the row temporarily.
C. It deletes the view definition.
D. It automatically deletes all rows in the base table.

**Answer: A**

---

# Section 5: DML on Views - Effect on Original Tables

For Q41-Q46, assume:

**EMPLOYEE**

| Emp_ID | Emp_Name | Dept_ID | Salary |
| --- | --- | --- | --- |
| 101 | Arun | 10 | 50000 |
| 102 | Banu | 20 | 60000 |
| 103 | Charan | 10 | 55000 |
| 104 | Divya | 30 | 70000 |

View:

```sql
CREATE VIEW IT_EMP AS
SELECT Emp_ID, Emp_Name, Dept_ID, Salary
FROM EMPLOYEE
WHERE Dept_ID = 10;
```

### Q41. Execute:

```sql
UPDATE IT_EMP
SET Salary = 65000
WHERE Emp_ID = 101;
```

What is the resulting salary of employee 101 in EMPLOYEE?

A. 50000
B. 55000
C. 65000
D. NULL

**Answer: C**

**Explanation:** DML on an updatable view modifies the underlying EMPLOYEE row.

### Q42. Execute:

```sql
DELETE FROM IT_EMP
WHERE Emp_ID = 103;
```

How many rows remain in the original EMPLOYEE table?

A. 2
B. 3
C. 4
D. 1

**Answer: B**

**Explanation:** Employee 103 is deleted from the base table. Three rows remain.

### Q43. Execute:

```sql
INSERT INTO IT_EMP
VALUES (105, 'Ezhil', 10, 45000);
```

Assuming the view is updatable and base-table constraints are satisfied, what happens?

A. The record is inserted only into IT_EMP.
B. The record is inserted into EMPLOYEE and appears in IT_EMP.
C. The record is inserted into DEPARTMENT.
D. The original table is not modified.

**Answer: B**

### Q44. Consider:

```sql
CREATE VIEW IT_EMP AS
SELECT Emp_ID, Emp_Name, Dept_ID
FROM EMPLOYEE
WHERE Dept_ID = 10;
```

Without CHECK OPTION, execute:

```sql
UPDATE IT_EMP
SET Dept_ID = 20
WHERE Emp_ID = 101;
```

Assuming this UPDATE is supported, what happens?

A. The base-table row is updated to Dept_ID = 20 and disappears from IT_EMP.
B. The update is necessarily rejected.
C. The row remains in IT_EMP with Dept_ID = 10.
D. The employee is deleted.

**Answer: A**

### Q45. Repeat Q44, but this time the view is defined with CHECK OPTION.

What happens?

A. The update succeeds.
B. The update is rejected because the modified row no longer satisfies Dept_ID = 10.
C. The entire table is deleted.
D. The view automatically changes to Dept_ID = 20.

**Answer: B**

### Q46. A user deletes all records through a simple updatable view:

```sql
DELETE FROM IT_EMP;
```

Which statement is correct?

A. Only the view definition is removed.
B. All rows visible through IT_EMP are deleted from the underlying EMPLOYEE table.
C. Every row in EMPLOYEE is deleted, including other departments.
D. The database is dropped.

**Answer: B**

### Q47. A view is created:

```sql
CREATE VIEW HIGH_SALARY AS
SELECT Emp_ID, Salary
FROM EMPLOYEE
WHERE Salary > 50000;
```

An employee's salary changes from 70000 to 40000 through the view.

What happens to the view result?

A. The employee continues to appear because the view is a snapshot.
B. The employee disappears from the view after the update.
C. The employee is deleted from EMPLOYEE.
D. The employee's salary becomes NULL.

**Answer: B**

### Q48. Which statement correctly describes a conventional view after base-table data is modified?

A. The view automatically maintains a permanent copy of old values.
B. A subsequent query of the view derives its result from the underlying data, subject to transaction visibility.
C. The view must always be dropped and recreated.
D. The base table no longer exists.

**Answer: B**

---

# Section 6: DROP VIEW and Dependencies

### Q49. Which command deletes a view definition?

A.

```sql
DELETE VIEW EMP_VIEW;
```

B.

```sql
DROP VIEW EMP_VIEW;
```

C.

```sql
REMOVE EMP_VIEW;
```

D.

```sql
TRUNCATE VIEW EMP_VIEW;
```

**Answer: B**

### Q50. What happens when a normal view is dropped?

A. The underlying base table is automatically deleted.
B. The view definition is removed, but the underlying base-table records remain.
C. All base-table rows are deleted.
D. The database is dropped.

**Answer: B**

### Q51. Consider:

```sql
CREATE VIEW V1 AS
SELECT Emp_ID, Emp_Name
FROM EMPLOYEE;
```

Then:

```sql
DROP VIEW V1;
```

What happens to EMPLOYEE?

A. EMPLOYEE is deleted.
B. EMPLOYEE remains unchanged.
C. EMPLOYEE becomes a view.
D. EMPLOYEE loses all rows.

**Answer: B**

### Q52. Which command is used to delete all records from a base table rather than deleting the view definition?

A. DROP VIEW
B. DELETE FROM table_name
C. DROP DATABASE
D. REVOKE VIEW

**Answer: B**

### Q53. A view V1 depends on another view V2. The DBA attempts to drop V2 while V1 still depends on it.

What may happen?

A. Every DBMS automatically drops V1.
B. The DBMS may reject the operation because of the dependency, or require an appropriate cascading operation.
C. The entire database is deleted.
D. V1 becomes an independent physical table automatically.

**Answer: B**

### Q54. Which statement about DROP VIEW is correct?

A. DROP VIEW removes the view's query definition, not the underlying table data.
B. DROP VIEW removes every table referenced in the view.
C. DROP VIEW is equivalent to DELETE FROM base_table.
D. DROP VIEW removes all user permissions from the database.

**Answer: A**

---

# Section 7: Advantages, Disadvantages and Expert Scenarios

### Q55. Which is NOT an advantage of views?

A. Restricting access to selected columns
B. Simplifying complex joins
C. Providing logical abstraction
D. Automatically eliminating all data redundancy in base tables

**Answer: D**

### Q56. A company has a complex query joining five tables. Multiple applications need the same result.

Which view advantage is most relevant?

A. Query simplification and reuse
B. Automatic database backup
C. Elimination of transaction processing
D. Guaranteed faster execution in every case

**Answer: A**

### Q57. Which is a potential disadvantage of conventional views?

A. They cannot be queried with SELECT.
B. Complex views may have limited DML support and can make query performance harder to predict.
C. They always duplicate every base-table row.
D. They cannot reference multiple tables.

**Answer: B**

### Q58. A DBA exposes a view containing only Employee_ID and Employee_Name to a junior user, hiding Salary.

Which benefit is achieved?

A. Data abstraction and restricted data exposure
B. Physical data independence only
C. Automatic indexing
D. Referential integrity

**Answer: A**

### Q59. Which statement about view performance is correct?

A. Every view makes a query faster.
B. Every view makes a query slower.
C. A conventional view generally does not store its result; the optimizer processes its query definition, and performance depends on the query and execution plan.
D. Views cannot use indexes on underlying tables.

**Answer: C**

### Q60. Consider the following complete scenario:

```sql
CREATE VIEW IT_EMP AS
SELECT Emp_ID, Emp_Name, Dept_ID, Salary
FROM EMPLOYEE
WHERE Dept_ID = 10
WITH CHECK OPTION;

GRANT SELECT, UPDATE, DELETE
ON IT_EMP TO USER1;
```

USER1 executes:

```sql
UPDATE IT_EMP
SET Dept_ID = 20
WHERE Emp_ID = 101;
```

Which statement is correct?

A. The update succeeds and the employee disappears from the view.
B. The update is rejected because CHECK OPTION prevents the row from leaving the view's defined condition.
C. The original EMPLOYEE table is dropped.
D. The update changes the view definition to include department 20.

**Answer: B**

---

# Complete Answer Key

| Questions | Answers |
| --- | --- |
| 1-10 | B, B, B, B, B, B, B, A, B, B |
| 11-20 | A, B, B, B, B, A, B, B, A, B |
| 21-30 | B, B, B, C, C, B, D, B, A, B |
| 31-40 | B, A, C, C, B, B, C, B, B, A |
| 41-50 | C, B, B, A, B, B, B, B, B, B |
| 51-60 | B, B, B, A, D, A, B, A, C, B |

---

# Important SQL View Syntax Cheat Sheet

## 1. Create a simple view

```sql
CREATE VIEW EMP_VIEW AS
SELECT Emp_ID, Emp_Name, Salary
FROM EMPLOYEE;
```

## 2. Create a filtered view

```sql
CREATE VIEW IT_EMP AS
SELECT *
FROM EMPLOYEE
WHERE Dept_ID = 10;
```

## 3. Create a view with column aliases

```sql
CREATE VIEW EMP_VIEW
(Employee_No, Employee_Name)
AS
SELECT Emp_ID, Emp_Name
FROM EMPLOYEE;
```

## 4. Create a view using JOIN

```sql
CREATE VIEW EMP_DEPT AS
SELECT E.Emp_ID,
       E.Emp_Name,
       D.Dept_Name
FROM EMPLOYEE E
JOIN DEPARTMENT D
ON E.Dept_ID = D.Dept_ID;
```

## 5. Create a view with GROUP BY

```sql
CREATE VIEW DEPT_SUMMARY AS
SELECT Dept_ID,
       COUNT(*) AS Total_Employees,
       AVG(Salary) AS Average_Salary
FROM EMPLOYEE
GROUP BY Dept_ID;
```

## 6. Create a view with CHECK OPTION

```sql
CREATE VIEW IT_EMP AS
SELECT *
FROM EMPLOYEE
WHERE Dept_ID = 10
WITH CHECK OPTION;
```

## 7. Grant SELECT on a view

```sql
GRANT SELECT ON EMP_VIEW TO USER1;
```

## 8. Grant multiple privileges

```sql
GRANT SELECT, UPDATE, DELETE
ON EMP_VIEW TO USER1;
```

## 9. Revoke SELECT on a view

```sql
REVOKE SELECT ON EMP_VIEW FROM USER1;
```

## 10. UPDATE through a view

```sql
UPDATE EMP_VIEW
SET Salary = 60000
WHERE Emp_ID = 101;
```

If supported, the underlying EMPLOYEE table is updated.

## 11. INSERT through a view

```sql
INSERT INTO EMP_VIEW
VALUES (105, 'Ezhil', 55000);
```

This requires the view to be insertable and all base-table constraints to be satisfied.

## 12. DELETE through a view

```sql
DELETE FROM EMP_VIEW
WHERE Emp_ID = 101;
```

If supported, the corresponding base-table record is deleted.

## 13. Drop a view

```sql
DROP VIEW EMP_VIEW;
```

This removes the view definition, not the underlying table.

---

# Most Important Exam Traps

| Scenario | Correct understanding |
| --- | --- |
| UPDATE through simple view | Updates base table |
| DELETE through simple view | Deletes base-table rows |
| INSERT through simple view | Inserts into base table if permitted |
| View without CHECK OPTION | Can allow rows to move outside its filter |
| View with CHECK OPTION | Prevents modifications violating its view condition |
| GROUP BY view | Generally not directly updatable |
| Aggregate view | Generally not directly updatable |
| JOIN view | DML has restrictions and DBMS-specific behavior |
| DROP VIEW | Does not drop base tables |
| GRANT SELECT ON VIEW | Grants access to the view |
| REVOKE SELECT ON VIEW | Removes that privilege |
| Conventional view | Does not ordinarily store a separate copy of data |
| Base table changes | Reflected in subsequent view queries |
| Hidden column | Cannot ordinarily be directly updated through the view |

**One particularly important distinction:** A view is not a snapshot of the original table. For a conventional view, INSERT, UPDATE and DELETE operations, when supported, operate on underlying base tables. The view's query definition determines which rows are visible when queried.

### User

give 30 more

### ChatGPT

## Views in SQL - Advanced MCQs (Next Batch: 30 Questions)

**Q61.** Consider the following view:

```sql
CREATE VIEW EMP_VIEW AS
SELECT EMP_ID, EMP_NAME, SALARY
FROM EMPLOYEE
WHERE DEPT_ID = 10;
```

An employee with `DEPT_ID = 20` is updated through the view by changing their department to 10. What happens?

A. The update always succeeds because the new department is 10.
B. The update fails because the employee is not currently in the view.
C. The employee cannot be accessed through this view before the update.
D. The update automatically inserts a new employee.

**Answer: C**

**Explanation:** A view exposes only rows satisfying its query condition. An employee belonging to department 20 is not visible through this view, so they cannot be updated through it.

---

**Q62.** Consider:

```sql
CREATE VIEW DEPT10_EMP AS
SELECT *
FROM EMPLOYEE
WHERE DEPT_ID = 10
WITH CHECK OPTION;
```

Which operation is prevented?

A. Updating the salary of an employee in department 10.
B. Inserting an employee into department 10.
C. Updating an employee's department from 10 to 20 through the view.
D. Selecting employees from the view.

**Answer: C**

**Explanation:** `WITH CHECK OPTION` ensures that modifications made through the view do not cause affected rows to violate its `WHERE` condition.

---

**Q63.** A view is created as follows:

```sql
CREATE VIEW HIGH_SALARY AS
SELECT EMP_ID, SALARY
FROM EMPLOYEE
WHERE SALARY > 50000;
```

An employee currently earning 60,000 is updated through this view to earn 40,000. Assume the view is updatable and has no CHECK OPTION. What happens?

A. The update is rejected.
B. The update succeeds, and the employee disappears from the view.
C. The update succeeds, but the employee remains visible.
D. The base table is not modified.

**Answer: B**

**Explanation:** Without `CHECK OPTION`, the update can make the row stop satisfying the view condition. The base table is updated, but the row is no longer visible in the view.

---

**Q64.** Which statement about a conventional SQL view is correct?

A. It stores a separate physical copy of every selected row.
B. It stores the query definition and retrieves data from underlying tables.
C. It stores only the primary key of the base table.
D. It automatically creates a backup of the base table.

**Answer: B**

**Explanation:** A conventional view is a virtual table based on a stored query definition. It does not independently store the result rows.

---

**Q65.** Consider:

```sql
CREATE VIEW EMP_COUNT AS
SELECT DEPT_ID, COUNT(*) AS TOTAL
FROM EMPLOYEE
GROUP BY DEPT_ID;
```

Why is this view generally not directly updatable?

A. It contains a foreign key.
B. It contains an aggregate function and GROUP BY.
C. It contains a numeric column.
D. It references only one table.

**Answer: B**

**Explanation:** Aggregation combines multiple base rows into summary rows. There is no straightforward way to determine which individual base row should be modified through the summary.

---

**Q66.** Consider:

```sql
CREATE VIEW EMP_BASIC AS
SELECT EMP_ID, EMP_NAME
FROM EMPLOYEE;
```

Which operation is generally possible if the view is updatable?

A. Insert a valid employee through the view.
B. Insert an employee without satisfying base-table constraints.
C. Delete the EMPLOYEE table through the view.
D. Change the table's primary key definition through the view.

**Answer: A**

**Explanation:** An insert through an updatable view can insert into the base table, provided required base-table columns receive valid values through the view, defaults, or permitted NULLs.

---

**Q67.** A user has been granted SELECT permission on a view but not directly on its base table. Which statement is most accurate?

A. The user can never query the view.
B. The user may query the view depending on the DBMS's privilege and security rules.
C. Granting SELECT on a view automatically grants ownership of the base table.
D. The user can modify the base table without restrictions.

**Answer: B**

**Explanation:** Access through a view can be permitted without direct base-table SELECT privileges, depending on ownership, authorization, and definer/invoker security rules.

---

**Q68.** Consider:

```sql
CREATE VIEW EMP_VIEW AS
SELECT EMP_ID, EMP_NAME
FROM EMPLOYEE;
```

What happens when the following command is executed?

```sql
DROP VIEW EMP_VIEW;
```

A. The EMPLOYEE table is deleted.
B. All employee records are deleted.
C. Only the view definition is removed.
D. The EMPLOYEE table is converted into a view.

**Answer: C**

**Explanation:** `DROP VIEW` removes the view object. It does not delete the underlying table or its records.

---

**Q69.** Which view definition is most likely to be directly updatable?

A.

```sql
SELECT DEPT_ID, COUNT(*)
FROM EMPLOYEE
GROUP BY DEPT_ID;
```

B.

```sql
SELECT DISTINCT DEPT_ID
FROM EMPLOYEE;
```

C.

```sql
SELECT EMP_ID, EMP_NAME
FROM EMPLOYEE
WHERE DEPT_ID = 10;
```

D.

```sql
SELECT DEPT_ID, AVG(SALARY)
FROM EMPLOYEE
GROUP BY DEPT_ID;
```

**Answer: C**

**Explanation:** A simple single-table view containing ordinary columns and a filtering condition is generally updatable.

---

**Q70.** Suppose a view contains only the following columns:

```sql
CREATE VIEW EMP_NAMES AS
SELECT EMP_NAME
FROM EMPLOYEE;
```

The base table has `EMP_ID` as its primary key. What is the main concern when inserting through this view?

A. EMP_NAME cannot be inserted because it is a character column.
B. EMP_ID is not exposed by the view, so the insert must still satisfy the base table's primary-key requirement.
C. The view automatically generates EMP_ID in every DBMS.
D. The insert always fails because primary keys cannot be omitted from views.

**Answer: B**

**Explanation:** If `EMP_ID` has no default or automatic generation and does not permit NULL, an insert through this view cannot satisfy the primary-key requirement.

---

**Q71.** Consider:

```sql
CREATE VIEW EMP_DEPT AS
SELECT E.EMP_ID, E.EMP_NAME, D.DEPT_NAME
FROM EMPLOYEE E
JOIN DEPARTMENT D
ON E.DEPT_ID = D.DEPT_ID;
```

Which statement is correct?

A. Every join view is always fully updatable.
B. Every join view is always non-updatable.
C. Updatability depends on the DBMS and properties of the joined tables.
D. Join views cannot be queried.

**Answer: C**

**Explanation:** Join-view updates depend on rules such as key preservation and DBMS-specific restrictions. Some DBMSs allow updates to selected underlying tables but not all columns.

---

**Q72.** Which command grants SELECT access to a view?

A.

```sql
GRANT SELECT ON EMP_VIEW TO USER1;
```

B.

```sql
ALLOW SELECT EMP_VIEW TO USER1;
```

C.

```sql
GRANT EMP_VIEW SELECT TO USER1;
```

D.

```sql
PERMIT EMP_VIEW TO USER1;
```

**Answer: A**

**Explanation:** The general SQL privilege syntax is `GRANT privilege ON object TO user`.

---

**Q73.** What is the effect of the following command?

```sql
REVOKE SELECT ON EMP_VIEW FROM USER1;
```

A. Deletes EMP_VIEW.
B. Deletes all records from EMPLOYEE.
C. Removes USER1's SELECT privilege on EMP_VIEW.
D. Removes USER1 from the database.

**Answer: C**

**Explanation:** `REVOKE` removes the specified privilege. It does not delete the view or its underlying data.

---

**Q74.** Consider:

```sql
CREATE VIEW EMP_VIEW AS
SELECT EMP_ID, EMP_NAME, SALARY
FROM EMPLOYEE;
```

A user executes:

```sql
UPDATE EMP_VIEW
SET SALARY = 70000
WHERE EMP_ID = 101;
```

Assuming the view is updatable and the user has sufficient privileges, what happens?

A. Only the view's stored data changes.
B. The corresponding EMPLOYEE row is updated.
C. A new table named EMP_VIEW is created.
D. The update changes every employee's salary.

**Answer: B**

**Explanation:** An update through an ordinary updatable view modifies the corresponding underlying base-table row.

---

**Q75.** Which of the following is a disadvantage of views?

A. They can simplify complex queries.
B. They can restrict access to selected columns.
C. Complex views may have update limitations and can make query performance harder to predict.
D. They can provide a customized representation of data.

**Answer: C**

**Explanation:** Views offer abstraction and security, but complex view definitions may restrict DML operations and can introduce query optimization or performance considerations.

---

**Q76.** Consider:

```sql
CREATE VIEW EMP_VIEW AS
SELECT EMP_ID, EMP_NAME
FROM EMPLOYEE;
```

If a new column `EMAIL` is added to the EMPLOYEE table, what happens to the existing view?

A. EMAIL automatically becomes part of the view output.
B. The view definition automatically changes to include EMAIL.
C. The view continues to expose the columns defined in its query.
D. The base table is dropped.

**Answer: C**

**Explanation:** The view's defined projection remains EMP_ID and EMP_NAME. Adding a base-table column does not automatically add it to the view.

---

**Q77.** Consider:

```sql
CREATE VIEW EMP_VIEW AS
SELECT EMP_ID, EMP_NAME
FROM EMPLOYEE;
```

Which statement correctly describes the relationship between the view and the base table?

A. The view owns the employee records.
B. The view is dependent on the underlying EMPLOYEE table.
C. The EMPLOYEE table depends on the view for its existence.
D. The view and EMPLOYEE table are independent physical copies.

**Answer: B**

**Explanation:** The view definition references the base table. Changes to or removal of the base table can affect the view's validity or usability.

---

**Q78.** A view is defined with a `WHERE` condition. Which operation can cause a row to disappear from the view without deleting it from the base table?

A. Updating a column so that the row no longer satisfies the WHERE condition.
B. Updating a column that is not used in the WHERE condition.
C. Selecting the row from the view.
D. Creating another view.

**Answer: A**

**Explanation:** A view displays rows that satisfy its query condition. If an update changes a row so that it no longer qualifies, the row disappears from the view but remains in the base table.

---

**Q79.** Which statement about `WITH CHECK OPTION` is correct?

A. It prevents SELECT statements on a view.
B. It checks whether modifications through the view preserve the view's filtering condition.
C. It prevents all UPDATE operations.
D. It automatically validates foreign keys in every base table.

**Answer: B**

**Explanation:** `WITH CHECK OPTION` enforces the view's condition for modifications made through that view. It does not replace primary-key, foreign-key, or other base-table constraints.

---

**Q80.** Consider:

```sql
CREATE VIEW EMP_VIEW AS
SELECT EMP_ID, EMP_NAME
FROM EMPLOYEE
WHERE DEPT_ID = 10;
```

A user inserts a row through the view but does not provide DEPT_ID. What is the correct conclusion?

A. DEPT_ID is always automatically assigned 10.
B. The insert always succeeds.
C. The insert's success depends on how the underlying DEPT_ID column is populated and the view's check-option behavior.
D. The view automatically creates a new department.

**Answer: C**

**Explanation:** Since DEPT_ID is not exposed, the base-table column must be populated through a default, permitted NULL, or another mechanism. With `CHECK OPTION`, the resulting row must satisfy `DEPT_ID = 10`.

---

**Q81.** Which of the following statements about a view is FALSE?

A. A view can hide selected columns.
B. A view can simplify complex queries.
C. A conventional view stores an independent copy of all its result rows.
D. A view can be used as a query source.

**Answer: C**

**Explanation:** A conventional view stores its query definition, not an independent copy of its result rows. A materialized view is a different concept.

---

**Q82.** Consider:

```sql
CREATE VIEW EMP_SALARY AS
SELECT EMP_ID, SALARY
FROM EMPLOYEE;
```

If a user has SELECT permission on EMP_SALARY but no direct SELECT permission on EMPLOYEE, what does the view provide?

A. A possible controlled access path to selected employee data.
B. Full administrative access to EMPLOYEE.
C. Permission to drop EMPLOYEE.
D. Automatic permission to update every column in EMPLOYEE.

**Answer: A**

**Explanation:** Views can expose a restricted subset of data. The exact access behavior depends on the DBMS's authorization and view-security rules.

---

**Q83.** Which view is generally unsuitable for direct row-level deletion?

A.

```sql
SELECT EMP_ID, EMP_NAME FROM EMPLOYEE;
```

B.

```sql
SELECT EMP_ID, SALARY FROM EMPLOYEE WHERE DEPT_ID = 20;
```

C.

```sql
SELECT DEPT_ID, COUNT(*) FROM EMPLOYEE GROUP BY DEPT_ID;
```

D.

```sql
SELECT EMP_ID FROM EMPLOYEE;
```

**Answer: C**

**Explanation:** A grouped result represents multiple employees as one summary row. Deleting a summary row does not identify a single base-table employee to delete.

---

**Q84.** Suppose two views are defined:

```sql
CREATE VIEW V1 AS
SELECT *
FROM EMPLOYEE
WHERE DEPT_ID = 10;

CREATE VIEW V2 AS
SELECT *
FROM V1
WHERE SALARY > 50000;
```

What does V2 display?

A. All employees in department 10.
B. Employees earning more than 50,000 in any department.
C. Employees in department 10 earning more than 50,000.
D. All employees earning less than 50,000.

**Answer: C**

**Explanation:** V2 queries V1, which already restricts rows to department 10. V2 further restricts those rows by salary.

---

**Q85.** If the underlying EMPLOYEE table is dropped, what is the likely consequence for a view referencing it?

A. The view automatically becomes a physical table.
B. The view may become invalid or unusable because its dependency is gone.
C. The view automatically recreates EMPLOYEE.
D. The view retains a complete independent copy of all employee records.

**Answer: B**

**Explanation:** A conventional view depends on its referenced objects. Dropping a base table can invalidate or prevent use of the view, depending on DBMS behavior.

---

**Q86.** Which statement about indexes and views is most accurate?

A. Every conventional view automatically gets its own independent index.
B. A conventional view necessarily stores all its rows in indexed form.
C. A conventional view generally relies on the underlying tables' access paths and indexes.
D. Creating a view deletes existing base-table indexes.

**Answer: C**

**Explanation:** A conventional view is normally a query definition. Query execution can use indexes on its underlying tables. Some DBMSs also support special indexed or materialized views, but these are distinct features.

---

**Q87.** Consider:

```sql
CREATE VIEW EMP_VIEW AS
SELECT EMP_ID, EMP_NAME
FROM EMPLOYEE
WHERE DEPT_ID = 10;
```

Which statement is correct when querying the view?

A. Only EMP_ID and EMP_NAME are exposed by the view.
B. All columns of EMPLOYEE are exposed automatically.
C. The WHERE condition is ignored when querying the view.
D. The view exposes only the primary key.

**Answer: A**

**Explanation:** The SELECT list determines the columns exposed by the view. The WHERE clause determines which rows are included.

---

**Q88.** A view is created using:

```sql
CREATE VIEW EMP_VIEW AS
SELECT EMP_ID, EMP_NAME
FROM EMPLOYEE
WHERE DEPT_ID = 10;
```

Which query retrieves employees from the view whose names begin with 'A'?

A.

```sql
SELECT *
FROM EMPLOYEE
WHERE EMP_NAME LIKE 'A%';
```

B.

```sql
SELECT *
FROM EMP_VIEW
WHERE EMP_NAME LIKE 'A%';
```

C.

```sql
SELECT EMP_VIEW
WHERE EMP_NAME = 'A%';
```

D.

```sql
SELECT EMP_NAME
FROM EMP_VIEW
GROUP BY EMP_ID;
```

**Answer: B**

**Explanation:** Querying the view applies an additional condition to the rows already restricted by the view definition.

---

**Q89.** What is the key difference between a conventional view and a materialized view?

A. A conventional view stores query results permanently, whereas a materialized view stores only a query.
B. Both always store independent physical copies.
C. A conventional view generally stores a query definition, whereas a materialized view stores query results physically.
D. A materialized view cannot be queried.

**Answer: C**

**Explanation:** A materialized view physically stores its result data and may need refreshing to reflect changes in underlying tables. A conventional view typically evaluates its defining query when accessed.

---

**Q90.** Consider:

```sql
CREATE VIEW EMP_VIEW AS
SELECT EMP_ID, EMP_NAME
FROM EMPLOYEE
WHERE DEPT_ID = 10;
```

Which statement best describes the effect of inserting a row directly into EMPLOYEE with `DEPT_ID = 20`?

A. The insertion is rejected because EMP_VIEW only displays department 10.
B. The insertion succeeds if base-table constraints permit it, but the new row is not displayed in EMP_VIEW.
C. The row is automatically changed to department 10.
D. EMP_VIEW is automatically deleted.

**Answer: B**

**Explanation:** A view's filtering condition does not restrict direct modifications to the base table. It controls which rows the view displays. Direct inserts are governed by the base table's constraints and permissions.

---

**End of Batch 2: Q61-Q90.**
