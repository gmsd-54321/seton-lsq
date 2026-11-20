
# Generate DBMS MCQs

### User

give advanced expert level 30 covering all topics mcq question not in quiz interface fundamental principles of dbms of data independence integrity, limitation of flat file, about dbms, functions of dbms, types of database hirearchial network no sql relational, relational model intro attirbute tuple relation, cardinality degree, find cardinality degree, domain,null, data integrity: entitty integrity, domain integrity, reference integrity, candidate key given scenarios find suitable candidate key, primary key, foreign key, given multiple table find candidate key, find candidate key foreign key primary key of given tables dont give in quiz interface given 3-4 tables find primary key for those tables

### ChatGPT

# DBMS - 30 Advanced & Expert-Level MCQs

(Expert Level) (30 Questions) (Conceptual + Scenario-Based)

**Topics covered:**

1. Fundamental principles of DBMS
2. Data independence
3. Limitations of flat-file systems
4. DBMS functions and advantages
5. Database models - Hierarchical, Network, Relational, NoSQL
6. Relational model - Attributes, Tuples, Relations
7. Cardinality and Degree
8. Domain and NULL values
9. Entity, Domain and Referential Integrity
10. Candidate keys, Primary keys and Foreign keys
11. Identifying keys from multiple related tables

**Instructions:** Select the single correct answer (A, B, C or D). These are deliberately tricky questions involving scenarios, multiple tables and edge cases. No quiz interface.

---

## Section 1: DBMS Fundamentals and Data Independence

**Q1.** A banking application initially stores customer information in individual files. When a customer changes their address, the address must be updated in multiple files. Some files are updated while others retain the old address.

Which fundamental DBMS problem does this scenario primarily demonstrate?

A. Data isolation and update anomaly due to redundancy

B. Lack of physical data independence

C. Violation of entity integrity

D. Lack of logical data independence

**Q2.** A database administrator changes the physical storage structure of a database from an unordered heap file to a B+ tree indexed organization. The application queries and conceptual schema remain unchanged.

Which type of data independence allows this change?

A. Logical data independence

B. Physical data independence

C. Referential independence

D. Structural independence

**Q3.** Consider the following change:

Initially, an employee database has:

`EMPLOYEE(EmpID, EmpName, Salary)`

Later, the DBA modifies the conceptual schema by splitting it into:

- EMPLOYEE(EmpID, EmpName)
- EMPLOYEE_SALARY(EmpID, Salary)

The application continues accessing the original logical representation through a view.

Which concept is demonstrated?

A. Physical data independence

B. Logical data independence

C. Data redundancy

D. Entity integrity

**Q4.** Which statement about the three-schema architecture of DBMS is CORRECT?

A. External schema describes physical disk storage.

B. Internal schema describes individual user views.

C. Conceptual schema describes the overall logical structure of the database.

D. External schema directly determines the physical file organization.

**Q5.** An organization uses separate flat files for payroll, attendance and employee information. The following problems occur:

- Duplicate employee details
- Inconsistent employee addresses
- Difficulty accessing combined information
- Multiple users overwriting each other's changes

Which combination identifies the limitations of the flat-file approach?

A. Redundancy, inconsistency, data isolation and concurrency problems

B. Referential integrity, entity integrity and domain integrity

C. Physical independence, logical independence and normalization

D. Atomicity, consistency, isolation and durability

**Q6.** Which of the following is NOT a fundamental function of a DBMS?

A. Managing transactions and concurrency

B. Enforcing database constraints

C. Managing authorization and access control

D. Automatically guaranteeing that every stored query is computationally optimal

---

## Section 2: Database Models

**Q7.** An organization maintains the following structure:

- One company has multiple departments.
- Each department belongs to exactly one company.
- Each department has multiple employees.
- Every employee belongs to exactly one department.

The database uses a tree-like structure where every child has exactly one parent.

Which database model is most naturally suited to this structure?

A. Network model

B. Hierarchical model

C. Relational model

D. Document-oriented NoSQL model

**Q8.** A student can enroll in multiple courses, and each course can have multiple students. The database model supports a record having multiple parent records and multiple child records through interconnected links.

Which model historically supports this structure?

A. Hierarchical model

B. Network model

C. Flat-file model

D. Key-value model

**Q9.** Which statement accurately distinguishes hierarchical and network database models?

A. Hierarchical databases support many-to-many relationships natively, whereas network databases support only one-to-many.

B. Hierarchical databases organize records in a tree, whereas network databases allow more flexible interconnected record relationships.

C. Both models require every record to have exactly one parent.

D. Network databases store information exclusively as JSON documents.

**Q10.** An application stores the following data:

```json
{
  "customer_id": 101,
  "name": "Arun",
  "addresses": [
    {"city": "Chennai"},
    {"city": "Bengaluru"}
  ]
}
```

Different customer documents can have different fields and nested structures.

Which statement is most accurate?

A. It violates the fundamental requirement that all relational tuples have identical attributes.

B. It represents a document-oriented NoSQL data model that supports flexible document structures.

C. It represents a hierarchical database because all NoSQL databases use tree structures.

D. It represents a network database because arrays establish multiple parent relationships.

**Q11.** A company requires the following:

- Strong support for structured relationships
- Foreign-key constraints
- SQL querying
- ACID transactions
- Consistent enforcement of relational constraints

Which database model is the most appropriate choice?

A. Key-value

B. Document-oriented

C. Relational

D. Graph-oriented

---

## Section 3: Relational Model - Attributes, Tuples, Cardinality and Degree

Consider the following relation:

**EMPLOYEE**

| EmpID | EmpName | DeptID | Salary |
| --- | --- | --- | --- |
| 101 | Arun | D1 | 40000 |
| 102 | Bala | D2 | 50000 |
| 103 | Charan | D1 | 45000 |
| 104 | Divya | D3 | 60000 |
| 105 | Ezhil | D2 | 55000 |

**Q12.** What are the cardinality and degree of the EMPLOYEE relation?

A. Cardinality = 4, Degree = 5

B. Cardinality = 5, Degree = 4

C. Cardinality = 20, Degree = 4

D. Cardinality = 5, Degree = 5

**Q13.** Consider the following relation:

**PRODUCT**

| ProductID | ProductName | Price | Category |
| --- | --- | --- | --- |
| P1 | Laptop | 50000 | Electronics |
| P2 | Mouse | 500 | Electronics |
| P3 | Chair | 3000 | Furniture |
| P4 | Keyboard | 1500 | Electronics |

A query retrieves only ProductID and Price for products with Price greater than 1000.

What are the cardinality and degree of the resulting relation?

A. Cardinality = 3, Degree = 2

B. Cardinality = 2, Degree = 3

C. Cardinality = 4, Degree = 2

D. Cardinality = 3, Degree = 4

**Q14.** Consider a relation R(A, B, C, D, E) containing 12 tuples.

The following operations are performed:

1. Select tuples where C = 10, resulting in 7 tuples.
2. Project attributes A, B and D.
3. Two projected tuples have identical values for all three attributes.

What is the cardinality and degree of the final relation?

A. Cardinality = 7, Degree = 3

B. Cardinality = 6, Degree = 3

C. Cardinality = 7, Degree = 5

D. Cardinality = 12, Degree = 3

**Q15.** Which statement about NULL in a relational database is CORRECT?

A. NULL always means zero.

B. NULL always means an empty string.

C. NULL represents missing, unknown or inapplicable information, and comparisons involving NULL generally produce UNKNOWN.

D. NULL values are always equal to each other.

**Q16.** A column `Age` is defined with domain INTEGER and CHECK constraint `Age >= 18`.

Which inserted value violates domain integrity?

A. 25

B. 18

C. NULL, when the column permits NULL

D. 17

---

## Section 4: Data Integrity and Constraints

**Q17.** Consider the following table:

**STUDENT**

| StudentID | Name | Age |
| --- | --- | --- |
| 101 | Arun | 20 |
| 102 | Bala | 21 |
| NULL | Charan | 22 |

Assume StudentID is declared as PRIMARY KEY.

Which integrity rule is violated?

A. Domain integrity

B. Entity integrity

C. Referential integrity

D. User-defined integrity only

**Q18.** Consider the following tables:

**DEPARTMENT**

| DeptID | DeptName |
| --- | --- |
| D1 | CSE |
| D2 | ECE |

**EMPLOYEE**

| EmpID | EmpName | DeptID |
| --- | --- | --- |
| 101 | Arun | D1 |
| 102 | Bala | D2 |
| 103 | Charan | D5 |

Assume Employee.DeptID is a foreign key referencing Department.DeptID.

What is violated?

A. Entity integrity

B. Domain integrity

C. Referential integrity

D. Attribute integrity

**Q19.** Consider a table:

```sql
CREATE TABLE Employee (
    EmpID INT PRIMARY KEY,
    Name VARCHAR(30) NOT NULL,
    Age INT CHECK (Age >= 18),
    Salary DECIMAL(10,2) CHECK (Salary > 0)
);
```

Which insertion violates domain integrity but does not violate entity integrity?

A. `(101, 'Arun', 25, 30000)`

B. `(NULL, 'Bala', 22, 25000)`

C. `(102, 'Charan', 16, 20000)`

D. `(103, 'Divya', 30, 40000)`

**Q20.** Which of the following statements about integrity constraints is CORRECT?

A. A foreign key must always contain unique values.

B. A primary key can contain NULL if the column is declared UNIQUE.

C. A foreign key may contain duplicate values, and it may contain NULL if NULL is permitted by its column definition and constraints.

D. A candidate key can contain duplicate values as long as it is not selected as the primary key.

---

## Section 5: Candidate Key, Primary Key and Foreign Key - Multi-table Scenarios

This section is particularly important. You must identify candidate keys, primary keys and foreign keys by examining functional uniqueness and relationships.

### Q21. Identify all candidate keys

Consider:

**EMPLOYEE**

| EmpID | Email | AadhaarNo | Name | DeptID |
| --- | --- | --- | --- | --- |
| 101 | a@gmail.com | A100 | Arun | D1 |
| 102 | b@gmail.com | A200 | Bala | D2 |
| 103 | c@gmail.com | A300 | Charan | D1 |
| 104 | d@gmail.com | A400 | Divya | D3 |

Business rules:

- EmpID is unique.
- Email is unique.
- AadhaarNo is unique.
- Name is not unique.
- DeptID is not unique.

Which option correctly identifies all candidate keys?

A. EmpID only

B. EmpID, Email and AadhaarNo

C. EmpID, Email, AadhaarNo and Name

D. EmpID, DeptID and Email

### Q22. Find the candidate key using a composite attribute

Consider:

**ENROLLMENT**

| StudentID | CourseID | Semester | Grade |
| --- | --- | --- | --- |
| S1 | C1 | 1 | A |
| S1 | C2 | 1 | B |
| S2 | C1 | 1 | A |
| S1 | C1 | 2 | B |

Business rule:

A student can enroll in the same course in different semesters, but cannot enroll in the same course more than once in the same semester.

Which is the minimal candidate key?

A. StudentID

B. CourseID

C. (StudentID, CourseID)

D. (StudentID, CourseID, Semester)

### Q23. Identify the correct primary and foreign keys

Consider three tables:

**CUSTOMER**

| CustomerID | CustomerName |
| --- | --- |
| C1 | Arun |
| C2 | Bala |
| C3 | Charan |

**ORDERS**

| OrderID | OrderDate | CustomerID |
| --- | --- | --- |
| O1 | 2026-01-10 | C1 |
| O2 | 2026-01-11 | C2 |
| O3 | 2026-01-12 | C1 |

**ORDER_ITEM**

| OrderID | ProductID | Quantity |
| --- | --- | --- |
| O1 | P1 | 2 |
| O1 | P2 | 1 |
| O2 | P1 | 3 |
| O3 | P3 | 4 |

Assume each order can contain multiple products, but a product appears at most once in an order.

Which option is correct?

A. CUSTOMER PK = CustomerName; ORDERS PK = CustomerID; ORDER_ITEM PK = ProductID

B. CUSTOMER PK = CustomerID; ORDERS PK = OrderID; ORDER_ITEM PK = (OrderID, ProductID)

C. CUSTOMER PK = CustomerID; ORDERS PK = (OrderID, CustomerID); ORDER_ITEM PK = OrderID

D. CUSTOMER PK = CustomerID; ORDERS PK = OrderDate; ORDER_ITEM PK = Quantity

### Q24. Identify candidate keys and foreign keys across four tables

Consider the following schema:

**DEPARTMENT**

| DeptID | DeptName |
| --- | --- |
| D1 | CSE |
| D2 | ECE |
| D3 | MECH |

**EMPLOYEE**

| EmpID | Email | EmpName | DeptID |
| --- | --- | --- | --- |
| E1 | e1@gmail.com | Arun | D1 |
| E2 | e2@gmail.com | Bala | D2 |
| E3 | e3@gmail.com | Charan | D1 |

**PROJECT**

| ProjectID | ProjectName | DeptID |
| --- | --- | --- |
| P1 | Alpha | D1 |
| P2 | Beta | D2 |

**EMPLOYEE_PROJECT**

| EmpID | ProjectID | Hours |
| --- | --- | --- |
| E1 | P1 | 20 |
| E1 | P2 | 10 |
| E2 | P2 | 30 |

Business rules:

- EmpID uniquely identifies employees.
- Email is unique for every employee.
- DeptID uniquely identifies departments.
- ProjectID uniquely identifies projects.
- An employee can work on multiple projects.
- A project can have multiple employees.
- Each employee-project combination occurs only once.

Which option correctly identifies the primary keys?

A. DEPARTMENT: DeptID; EMPLOYEE: EmpID; PROJECT: ProjectID; EMPLOYEE_PROJECT: (EmpID, ProjectID)

B. DEPARTMENT: DeptName; EMPLOYEE: Email; PROJECT: DeptID; EMPLOYEE_PROJECT: EmpID

C. DEPARTMENT: DeptID; EMPLOYEE: DeptID; PROJECT: ProjectID; EMPLOYEE_PROJECT: ProjectID

D. DEPARTMENT: DeptID; EMPLOYEE: EmpID; PROJECT: ProjectID; EMPLOYEE_PROJECT: Hours

### Q25. Foreign key identification - Multiple relationships

Consider:

**BRANCH**

| BranchID | BranchName |
| --- | --- |
| B1 | Chennai |
| B2 | Bengaluru |

**ACCOUNT**

| AccountID | AccountType | BranchID |
| --- | --- | --- |
| A1 | Savings | B1 |
| A2 | Current | B1 |
| A3 | Savings | B2 |

**TRANSACTION**

| TransactionID | AccountID | Amount |
| --- | --- | --- |
| T1 | A1 | 1000 |
| T2 | A1 | 500 |
| T3 | A2 | 2000 |

Which option correctly identifies the foreign keys?

A. ACCOUNT.AccountID references BRANCH.BranchID; TRANSACTION.TransactionID references ACCOUNT.AccountID.

B. ACCOUNT.BranchID references BRANCH.BranchID; TRANSACTION.AccountID references ACCOUNT.AccountID.

C. ACCOUNT.BranchID references TRANSACTION.AccountID; TRANSACTION.AccountID references BRANCH.BranchID.

D. ACCOUNT.AccountID references TRANSACTION.TransactionID; TRANSACTION.TransactionID references BRANCH.BranchID.

### Q26. Find the minimal candidate key

Consider a relation:

`R(A, B, C, D)`

Functional dependencies:

- A → B
- B → A
- C → D
- D → C

Which of the following represents all candidate keys?

A. AC, AD, BC, BD

B. A, B, C, D

C. AB, CD

D. ABCD only

### Q27. Primary key versus candidate key

Consider:

**EMPLOYEE**

| EmpID | Email | PassportNo | Name |
| --- | --- | --- | --- |
| E1 | a@gmail.com | P101 | Arun |
| E2 | b@gmail.com | P102 | Bala |
| E3 | c@gmail.com | P103 | Charan |

Business rules:

- EmpID is unique and NOT NULL.
- Email is unique and NOT NULL.
- PassportNo is unique and NOT NULL.
- EmpID is selected as the primary key.

Which statement is correct?

A. Email and PassportNo stop being candidate keys after EmpID is selected.

B. Email and PassportNo remain candidate keys and are alternate keys.

C. Only EmpID is a candidate key because it is the primary key.

D. PassportNo becomes a foreign key automatically.

### Q28. Identify the correct primary key for a weak entity

Consider:

**EMPLOYEE**

| EmpID | EmpName |
| --- | --- |
| E1 | Arun |
| E2 | Bala |

**DEPENDENT**

| EmpID | DependentName | Relationship |
| --- | --- | --- |
| E1 | Ravi | Son |
| E1 | Priya | Daughter |
| E2 | Ravi | Son |

Business rule:

DependentName is unique only within a particular employee. Different employees may have dependents with the same name.

Which is the most suitable primary key for DEPENDENT?

A. DependentName

B. EmpID

C. (EmpID, DependentName)

D. Relationship

### Q29. Identify the invalid database design

Consider:

**STUDENT**

| StudentID | StudentName |
| --- | --- |
| S1 | Arun |
| S2 | Bala |

**COURSE**

| CourseID | CourseName |
| --- | --- |
| C1 | DBMS |
| C2 | Java |

**ENROLLMENT**

| StudentID | CourseID | Grade |
| --- | --- | --- |
| S1 | C1 | A |
| S1 | C2 | B |
| S2 | C1 | A |

Which database design correctly represents the many-to-many relationship?

A. STUDENT.StudentID is PK; COURSE.CourseID is PK; ENROLLMENT has composite PK (StudentID, CourseID), with both columns as foreign keys.

B. STUDENT.StudentID is PK; COURSE.CourseID is PK; ENROLLMENT has StudentID alone as PK.

C. STUDENT.StudentID is PK; COURSE.CourseID is PK; ENROLLMENT has CourseID alone as PK.

D. STUDENT.StudentName is PK; COURSE.CourseName is PK; ENROLLMENT has Grade as PK.

### Q30. Expert-level integrated key identification

Consider the following four tables:

**HOSPITAL**

| HospitalID | HospitalName |
| --- | --- |
| H1 | Apollo |
| H2 | Fortis |

**DOCTOR**

| DoctorID | LicenseNo | DoctorName | HospitalID |
| --- | --- | --- | --- |
| D1 | L101 | Arun | H1 |
| D2 | L102 | Bala | H1 |
| D3 | L103 | Charan | H2 |

**PATIENT**

| PatientID | PatientName |
| --- | --- |
| P1 | Ravi |
| P2 | Priya |

**APPOINTMENT**

| AppointmentID | DoctorID | PatientID | AppointmentDate |
| --- | --- | --- | --- |
| A1 | D1 | P1 | 2026-11-20 |
| A2 | D1 | P2 | 2026-11-20 |
| A3 | D2 | P1 | 2026-11-20 |

Business rules:

- HospitalID uniquely identifies hospitals.
- DoctorID and LicenseNo are individually unique.
- PatientID uniquely identifies patients.
- AppointmentID uniquely identifies appointments.
- A doctor can have many appointments.
- A patient can have many appointments.
- A patient may visit the same doctor multiple times, including on the same date.

Which option correctly identifies all primary keys and foreign keys?

A.

- HOSPITAL PK: HospitalID
- DOCTOR PK: DoctorID
- PATIENT PK: PatientID
- APPOINTMENT PK: AppointmentID
- DOCTOR.HospitalID → HOSPITAL.HospitalID
- APPOINTMENT.DoctorID → DOCTOR.DoctorID
- APPOINTMENT.PatientID → PATIENT.PatientID

B.

- HOSPITAL PK: HospitalName
- DOCTOR PK: HospitalID
- PATIENT PK: PatientName
- APPOINTMENT PK: (DoctorID, PatientID)
- DOCTOR.DoctorID → HOSPITAL.HospitalID

C.

- HOSPITAL PK: HospitalID
- DOCTOR PK: LicenseNo
- PATIENT PK: PatientID
- APPOINTMENT PK: (DoctorID, PatientID)
- APPOINTMENT.DoctorID → PATIENT.PatientID

D.

- HOSPITAL PK: HospitalID
- DOCTOR PK: DoctorID
- PATIENT PK: PatientID
- APPOINTMENT PK: AppointmentDate
- APPOINTMENT.PatientID → DOCTOR.DoctorID

---

## Answer Key - Try before checking

**Answer key**

## Important expert-level revision points

| Concept | Remember |
| --- | --- |
| Cardinality | Number of tuples (rows) |
| Degree | Number of attributes (columns) |
| Candidate key | Minimal superkey |
| Primary key | Selected candidate key |
| Alternate key | Candidate key not selected as PK |
| Composite key | Key consisting of multiple attributes |
| Foreign key | References a candidate/primary key in another or the same table |
| Entity integrity | Primary key cannot be NULL |
| Domain integrity | Values must satisfy their defined domain and constraints |
| Referential integrity | Foreign key values must reference existing parent keys or be NULL if allowed |
| Physical independence | Internal schema changes without affecting conceptual schema |
| Logical independence | Conceptual schema changes without affecting external views |

**Important trap:** A column being unique in the sample data does not automatically make it a candidate key. Candidate keys must be determined using the business rules and guaranteed uniqueness, not just the currently displayed rows.

### User

er model simple what i give content only based on that give quiz relationships self relationship 1:1 1:n m:n relationship, cardinalinity of relationship, correct way of mapping 1:1 relationship, 1:n relationship, m:n relationship, given situation find what type relationship is it 1:1,1:n and m:n between 2 tables give expert level questions quiz based on this just this topic only give expert advanced tricky level give 40 mcqs dont give in quiz interface

### ChatGPT

# ER Model - 40 Advanced & Expert-Level MCQs

(Expert Level) (40 Questions)

**Scope strictly limited to your requested topics:**

1. Self / Recursive relationships
2. One-to-One (1:1) relationships
3. One-to-Many (1:N) relationships
4. Many-to-Many (M:N) relationships
5. Relationship cardinality
6. Identifying relationship types from real-world scenarios
7. Correct mapping of 1:1 relationships into tables
8. Correct mapping of 1:N relationships into tables
9. Correct mapping of M:N relationships into tables
10. Identifying primary and foreign keys after ER-to-relational mapping

All questions are scenario-based, with tricky options and table-mapping problems. No questions outside these topics.

### User

functional dependency: fully functional dependency, partial functional dependency, transitive functional dependency, issues with bad design: insert anamoly, update anamoly, delete anamoly, data redundance for unnormalized table, identify correct relationship between attributes of a table, given functional dependancy of table identify if table is fully functional dependancy partial or transitive, given functional dependancy identify candidate key this type mcqs also give more based on this topic with table examples mcqs give, intro to normalization types of normal forms, how do we achieve 1st normal form, second normal form 3rd normal form give set of identify normal form of given table, then table -> final normal form for 1st second third which is correct mcq give 60 questions expert level questions mcq give give 5 nrmalization till 3nf questions given table decompose till 3nf give 10 dont give in quiz interface give 60 quiz + other question give aboe

### ChatGPT

# DBMS - Functional Dependency & Normalization: 60 Expert-Level MCQs + 10 Decomposition Problems

(Expert / Advanced) (60 MCQs) (10 Practical Problems)

This practice set covers only Functional Dependency, Database Anomalies and Normalization up to 3NF.

## Complete topic coverage

| Section | Topics | Questions |
| --- | --- | --- |
| 1 | Functional dependency fundamentals, attribute relationships | 1-8 |
| 2 | Full, partial and transitive dependency | 9-20 |
| 3 | Candidate keys using functional dependencies | 21-27 |
| 4 | Insert, update, delete anomalies and redundancy | 28-35 |
| 5 | Normalization introduction and 1NF | 36-42 |
| 6 | 2NF and 3NF concepts | 43-50 |
| 7 | Identify normal form and choose correct decomposition | 51-60 |
| 8 | Practical table decomposition up to 3NF | 10 problems |

---

# Section 1 - Functional Dependency Fundamentals

**Q1.** Consider the relation:

`STUDENT(StudentID, StudentName, Department, Phone)`

Given:

- StudentID uniquely identifies a student.
- Each student has one name and one department.
- A student can have multiple phone numbers.

Which functional dependency is valid?

A. StudentID → Phone

B. StudentID → StudentName, Department

C. Phone → StudentID

D. Department → StudentID

**Q2.** Consider the following table:

| EmpID | EmpName | DeptID | DeptName |
| --- | --- | --- | --- |
| E1 | Arun | D1 | CSE |
| E2 | Bala | D1 | CSE |
| E3 | Charan | D2 | ECE |
| E4 | Divya | D2 | ECE |

Assume each employee belongs to exactly one department, and each DeptID identifies one department name.

Which set of functional dependencies is valid?

A. EmpID → DeptID, EmpID → EmpName, DeptID → DeptName

B. DeptID → EmpID, EmpName → EmpID

C. DeptName → EmpID, EmpID → DeptName

D. EmpName → DeptID, DeptName → EmpID

**Q3.** Given the functional dependency:

`A, B → C`

Which interpretation is correct?

A. A alone determines C.

B. B alone determines C.

C. The combination of A and B determines C.

D. C determines both A and B.

**Q4.** Consider:

`R(A, B, C, D)`

Functional dependencies:

- A → B
- B → C
- C → D

Which attribute determines D through transitive dependency?

A. A

B. B

C. C

D. All of A, B and C can determine D, but through different dependency paths.

**Q5.** A company maintains:

`EMPLOYEE(EmpID, Email, Name, DeptID)`

Business rules:

- EmpID is unique.
- Email is unique.
- Each employee has exactly one email.
- Each employee belongs to one department.

Which is a valid functional dependency?

A. Email → EmpID

B. DeptID → EmpID

C. Name → EmpID

D. DeptID → Email

**Q6.** Given:

`A → B` and `B → C`

Which additional dependency can be inferred using Armstrong's transitivity rule?

A. C → A

B. A → C

C. B → A

D. C → B

**Q7.** Consider:

`R(A, B, C)`

Given:

- A → B
- A → C

Which dependency is guaranteed?

A. A → BC

B. BC → A

C. B → C

D. C → B

**Q8.** A table has the following functional dependencies:

- StudentID → StudentName
- CourseID → CourseName
- (StudentID, CourseID) → Grade

Which statement is correct?

A. StudentID alone determines Grade.

B. CourseID alone determines Grade.

C. The combination of StudentID and CourseID determines Grade.

D. Grade determines StudentID and CourseID.

---

# Section 2 - Full, Partial and Transitive Functional Dependency

**Q9.** Consider:

`ENROLLMENT(StudentID, CourseID, StudentName, CourseName, Grade)`

Primary key: `(StudentID, CourseID)`

Dependencies:

- StudentID → StudentName
- CourseID → CourseName
- (StudentID, CourseID) → Grade

Which attributes have partial dependencies?

A. StudentName and CourseName

B. Grade only

C. StudentName and Grade

D. CourseName and Grade

**Q10.** Given:

`(A, B) → C`

Neither A nor B alone determines C.

What type of dependency is this?

A. Partial dependency

B. Full functional dependency

C. Transitive dependency

D. Multivalued dependency

**Q11.** Consider:

`ORDER_DETAIL(OrderID, ProductID, ProductName, Quantity)`

Primary key: `(OrderID, ProductID)`

Dependencies:

- ProductID → ProductName
- (OrderID, ProductID) → Quantity

Which statement is correct?

A. ProductName has full functional dependency on the composite key.

B. Quantity has full functional dependency on the composite key.

C. Quantity has partial dependency on ProductID.

D. ProductID → Quantity.

**Q12.** Consider:

`R(A, B, C)`

Candidate key: `(A, B)`

Functional dependencies:

- AB → C
- A → C

Which classification applies to AB → C?

A. Fully functional dependency

B. Partial dependency exists because A alone determines C

C. Transitive dependency

D. No functional dependency exists

**Q13.** Consider:

`EMPLOYEE(EmpID, EmpName, DeptID, DeptName)`

Dependencies:

- EmpID → EmpName, DeptID
- DeptID → DeptName

Primary key: EmpID.

What type of dependency exists between EmpID and DeptName?

A. Full functional dependency

B. Partial dependency

C. Transitive dependency

D. No dependency

**Q14.** Consider:

`R(A, B, C, D)`

Candidate key: `(A, B)`

Dependencies:

- AB → C
- A → C
- AB → D

Which attributes have full functional dependency on the candidate key?

A. C only

B. D only

C. C and D

D. Neither C nor D

**Q15.** A relation has candidate key `(StudentID, SubjectID)`.

Dependencies:

- StudentID → StudentName
- SubjectID → SubjectName
- (StudentID, SubjectID) → Marks
- Marks → Grade

Which is the transitive dependency chain?

A. StudentID → StudentName

B. SubjectID → SubjectName

C. (StudentID, SubjectID) → Marks → Grade

D. StudentID → SubjectID

**Q16.** Consider:

`R(A, B, C, D)`

Candidate key: AB

Dependencies:

- AB → C
- C → D

Which statement is correct?

A. D is partially dependent on AB.

B. D is transitively dependent on AB through C.

C. C is partially dependent on AB.

D. AB is not a candidate key.

**Q17.** Which condition is required for a partial functional dependency?

A. A non-prime attribute must depend on a proper subset of a candidate key.

B. A non-prime attribute must depend on another non-prime attribute.

C. Every attribute must depend on the entire candidate key.

D. A foreign key must determine the primary key.

**Q18.** A relation has composite candidate key `(A, B)`.

Given:

- A → C
- B → D
- AB → E

Which classification is correct?

A. C and D are fully dependent; E is partially dependent.

B. C and D are partially dependent; E is fully dependent.

C. C, D and E are all transitively dependent.

D. C and E are partially dependent; D is fully dependent.

**Q19.** Consider:

`EMPLOYEE(EmpID, DeptID, DeptName, Location)`

Dependencies:

- EmpID → DeptID
- DeptID → DeptName, Location

Which attributes are transitively dependent on EmpID?

A. DeptID only

B. DeptName and Location

C. EmpID and DeptID

D. None

**Q20.** A relation has candidate key `(A, B)` and dependencies:

- AB → C
- C → D
- A → E

Which statement is correct?

A. C is partially dependent on AB.

B. D is transitively dependent on AB through C, and E is partially dependent on AB.

C. D is fully dependent on AB and E is transitively dependent.

D. C, D and E are all fully dependent on AB.

---

# Section 3 - Find Candidate Keys Using Functional Dependencies

For these questions, calculate attribute closure wherever necessary.

**Q21.** Given:

`R(A, B, C)`

Functional dependencies:

- A → B
- B → C

Find the candidate key.

A. A

B. B

C. C

D. AB

**Q22.** Given:

`R(A, B, C, D)`

Functional dependencies:

- A → B
- C → D
- B → C

Find the candidate key.

A. A

B. B

C. AC

D. D

**Q23.** Given:

`R(A, B, C, D, E)`

Functional dependencies:

- A → B
- B → C
- CD → E
- E → A

Find all candidate keys.

A. A, B, E

B. AD, BD, CD, DE

C. AB, BC, CD

D. ACD only

**Q24.** Given:

`R(A, B, C, D)`

Functional dependencies:

- AB → C
- C → D
- D → A

Find all candidate keys.

A. AB and BC

B. AB, BC and BD

C. A, B and C

D. ABCD only

**Q25.** Given:

`R(A, B, C, D, E)`

Functional dependencies:

- A → B
- B → A
- C → D
- D → C
- AC → E

Find all candidate keys.

A. AC, AD, BC, BD

B. AB and CD

C. A, B, C, D

D. ACE and BDE

**Q26.** Given:

`R(A, B, C, D)`

Functional dependencies:

- A → B
- B → C
- C → A
- C → D

Which is the set of candidate keys?

A. A, B, C

B. A, B, C, D

C. AD, BD, CD

D. ABC

**Q27.** Given:

`R(A, B, C, D, E)`

Functional dependencies:

- AB → C
- C → D
- D → E
- E → A

Find all candidate keys.

A. AB, BC, BD, BE

B. AB only

C. A, B, C and D

D. ABCDE only

---

# Section 4 - Database Design Problems and Anomalies

Consider the following unnormalized table.

**EMPLOYEE_DEPARTMENT**

| EmpID | EmpName | DeptID | DeptName | DeptLocation |
| --- | --- | --- | --- | --- |
| E1 | Arun | D1 | CSE | Chennai |
| E2 | Bala | D1 | CSE | Chennai |
| E3 | Charan | D2 | ECE | Bengaluru |
| E4 | Divya | D2 | ECE | Bengaluru |

Assume each employee belongs to exactly one department.

**Q28.** If the CSE department is newly created but no employees have joined it, what problem occurs if the organization stores department information only in this table?

A. Update anomaly

B. Insert anomaly

C. Delete anomaly

D. Transitive dependency

**Q29.** If the CSE department location changes from Chennai to Hyderabad, which problem occurs if only one employee's row is updated?

A. Insert anomaly

B. Delete anomaly

C. Update anomaly

D. Entity integrity violation

**Q30.** If E1 and E2 are the only employees in CSE and both records are deleted, what information may be unintentionally lost?

A. Employee names only

B. Department details

C. Primary key constraints

D. Employee IDs of other departments

**Q31.** Why does the above table contain data redundancy?

A. DeptName and DeptLocation are repeated for every employee in the same department.

B. EmpID is always repeated.

C. Every employee has a different department name.

D. Department details cannot be represented using attributes.

**Q32.** Consider:

**STUDENT_COURSE**

| StudentID | StudentName | CourseID | CourseName | Marks |
| --- | --- | --- | --- | --- |
| S1 | Arun | C1 | DBMS | 90 |
| S1 | Arun | C2 | Java | 85 |
| S2 | Bala | C1 | DBMS | 80 |
| S3 | Charan | C2 | Java | 88 |

Primary key: `(StudentID, CourseID)`.

Which attribute causes redundancy when repeated across multiple course registrations by the same student?

A. CourseID

B. Marks

C. StudentName

D. StudentID

**Q33.** Consider:

| OrderID | ProductID | ProductName | Quantity |
| --- | --- | --- | --- |
| O1 | P1 | Laptop | 2 |
| O1 | P2 | Mouse | 3 |
| O2 | P1 | Laptop | 1 |

Primary key: `(OrderID, ProductID)`.

Which anomaly occurs if Product P1 is renamed to Notebook but only one row is updated?

A. Insert anomaly

B. Update anomaly

C. Delete anomaly

D. No anomaly

**Q34.** A database stores student details and course details in the same table. A student has not registered for any course yet, so no row can be inserted without a CourseID.

Which anomaly is demonstrated?

A. Update anomaly

B. Delete anomaly

C. Insert anomaly

D. Transitive dependency

**Q35.** Which is the main purpose of normalization?

A. Increase the number of duplicate records

B. Eliminate all foreign keys

C. Reduce redundancy and prevent modification anomalies through better decomposition

D. Combine every table into one large table

---

# Section 5 - Introduction to Normalization and 1NF

**Q36.** Which statement best describes normalization?

A. A process of organizing relational tables to reduce redundancy and undesirable dependencies.

B. A process of increasing duplicate values to improve query performance.

C. A process of converting every relation into a single table.

D. A process of removing all candidate keys.

**Q37.** Consider:

| StudentID | StudentName | PhoneNumbers |
| --- | --- | --- |
| S1 | Arun | 9876, 8765 |
| S2 | Bala | 7654 |

Which condition prevents this table from satisfying 1NF?

A. StudentID is unique.

B. PhoneNumbers contains multiple values in a single cell.

C. StudentName is a character attribute.

D. There are only two records.

**Q38.** Which transformation correctly achieves 1NF?

Original:

| StudentID | Name | Subjects |
| --- | --- | --- |
| S1 | Arun | DBMS, Java |
| S2 | Bala | Python |

A.

| StudentID | Name | Subject |
| --- | --- | --- |
| S1 | Arun | DBMS |
| S1 | Arun | Java |
| S2 | Bala | Python |

B.

| StudentID | Name | Subjects |
| --- | --- | --- |
| S1 | Arun | DBMS, Java |
| S2 | Bala | Python |

C.

| StudentID | Name | Subject1 | Subject2 |
| --- | --- | --- | --- |
| S1 | Arun | DBMS | Java |
| S2 | Bala | Python | NULL |

D. Remove StudentID and retain only Name.

**Q39.** A table has a single-valued attribute in every cell and no repeating groups. However, a non-key attribute depends on only part of a composite primary key.

Which normal form can the table satisfy, assuming the dependencies otherwise permit it?

A. Only 1NF, not 2NF

B. Definitely 2NF

C. Definitely 3NF

D. BCNF

**Q40.** Which statement about 1NF is correct?

A. Every non-key attribute must depend on the whole primary key.

B. Every determinant must be a candidate key.

C. Each attribute value must be atomic within the chosen relational domain, with no repeating groups.

D. Transitive dependencies must be eliminated.

**Q41.** Consider:

| OrderID | CustomerID | Products |
| --- | --- | --- |
| O1 | C1 | P1, P2 |
| O2 | C2 | P3, P4, P5 |

Which modification most directly converts Products into a 1NF representation?

A. Store each product as a separate row with the relevant order information.

B. Store all product IDs in a comma-separated string.

C. Create additional columns Product1, Product2, Product3.

D. Remove the Products attribute.

**Q42.** A table is in 1NF but contains a composite primary key `(A, B)` and dependency `A → C`, where C is non-prime. Which normal form is definitely violated?

A. 1NF

B. 2NF

C. 3NF only, but not 2NF

D. No normal form is violated

---

# Section 6 - Second Normal Form and Third Normal Form

**Q43.** A relation is in 2NF when:

A. It is in 1NF and has no partial dependency of a non-prime attribute on any candidate key.

B. It has no transitive dependency only.

C. Every determinant is a superkey.

D. It contains no foreign keys.

**Q44.** Consider:

`ENROLLMENT(StudentID, CourseID, StudentName, CourseName, Marks)`

Primary key: `(StudentID, CourseID)`.

Dependencies:

- StudentID → StudentName
- CourseID → CourseName
- (StudentID, CourseID) → Marks

What is the highest normal form of the table, assuming atomic values?

A. Unnormalized

B. 1NF

C. 2NF

D. 3NF

**Q45.** Which decomposition correctly removes partial dependencies from the previous ENROLLMENT table?

A. STUDENT(StudentID, StudentName), COURSE(CourseID, CourseName), ENROLLMENT(StudentID, CourseID, Marks)

B. STUDENT(StudentID, CourseID), COURSE(StudentName, CourseName), ENROLLMENT(Marks)

C. STUDENT(StudentName), COURSE(CourseName), ENROLLMENT(StudentID, CourseID)

D. STUDENT(StudentID, StudentName, Marks), COURSE(CourseID, CourseName, Marks)

**Q46.** Consider:

`EMPLOYEE(EmpID, EmpName, DeptID, DeptName)`

Dependencies:

- EmpID → EmpName, DeptID
- DeptID → DeptName

The primary key is EmpID.

Assuming atomic attributes, what is the highest normal form?

A. 1NF

B. 2NF

C. 3NF

D. BCNF

**Q47.** What is the correct decomposition to eliminate the transitive dependency in the previous EMPLOYEE table?

A. EMPLOYEE(EmpID, EmpName, DeptID), DEPARTMENT(DeptID, DeptName)

B. EMPLOYEE(EmpID, EmpName), DEPARTMENT(DeptName, EmpName)

C. EMPLOYEE(DeptID, DeptName), DEPARTMENT(EmpID, EmpName)

D. EMPLOYEE(EmpID, DeptName), DEPARTMENT(EmpName, DeptID)

**Q48.** A relation is in 3NF if, for every non-trivial functional dependency X → A, at least one condition holds:

A. X is a superkey or A is a prime attribute.

B. X is always a single attribute.

C. A must be a primary key.

D. X and A must both be candidate keys.

**Q49.** Consider:

`R(A, B, C)`

Functional dependencies:

- AB → C
- C → B

Candidate keys: AB and AC.

Is this relation in 3NF?

A. No, because C → B violates 3NF.

B. Yes, because B is a prime attribute.

C. No, because AB is composite.

D. Yes, because there are no transitive dependencies.

**Q50.** Consider:

`R(A, B, C)`

Functional dependencies:

- A → B
- B → C

Candidate key: A.

Which is the highest normal form, assuming atomic attributes?

A. 1NF

B. 2NF

C. 3NF

D. BCNF

---

# Section 7 - Identify Normal Form and Correct Decomposition

**Q51.** Consider:

`R(A, B, C, D)`

Primary key: AB.

Dependencies:

- AB → C, D
- A → C

The table has atomic values.

What is the highest normal form?

A. 1NF

B. 2NF

C. 3NF

D. BCNF

**Q52.** Consider:

`R(A, B, C)`

Candidate key: A.

Dependencies:

- A → B
- B → C

The table contains atomic values.

Which is the highest normal form?

A. 1NF

B. 2NF

C. 3NF

D. BCNF

**Q53.** Consider:

`R(A, B, C)`

Candidate keys: AB and AC.

Dependencies:

- AB → C
- AC → B
- B → C

Which is the highest normal form?

A. 1NF

B. 2NF

C. 3NF

D. BCNF

**Q54.** Consider:

`R(A, B, C)`

Functional dependencies:

- A → B
- B → A

Candidate keys: AC and BC.

Which normal form does this relation satisfy, assuming atomic attributes?

A. 1NF only

B. 2NF but not 3NF

C. 3NF but not BCNF

D. BCNF

**Q55.** Consider:

`STUDENT(StudentID, DeptID, DeptName)`

Dependencies:

- StudentID → DeptID
- DeptID → DeptName

Which decomposition correctly achieves 3NF?

A. STUDENT(StudentID, DeptID), DEPARTMENT(DeptID, DeptName)

B. STUDENT(StudentID, DeptName), DEPARTMENT(DeptID, DeptName)

C. STUDENT(StudentID, DeptID, DeptName), DEPARTMENT(DeptName)

D. STUDENT(StudentID), DEPARTMENT(DeptID, DeptName)

**Q56.** Consider:

`R(A, B, C, D)`

Candidate key: AB.

Dependencies:

- AB → C
- C → D

Which decomposition removes the transitive dependency and preserves the dependency structure?

A. R1(A, B, C), R2(C, D)

B. R1(A, B), R2(C, D)

C. R1(A, C), R2(B, D)

D. R1(A, B, D), R2(C)

**Q57.** Consider:

`R(A, B, C)`

Functional dependencies:

- A → B
- B → C

A is the candidate key.

Which decomposition is correct for 3NF?

A. R1(A, B), R2(B, C)

B. R1(A, C), R2(A, B)

C. R1(A, B, C), R2(B, C)

D. R1(A), R2(B), R3(C)

**Q58.** Consider:

`R(A, B, C, D)`

Candidate key: AB.

Dependencies:

- AB → C
- C → D

Which statement is correct about the decomposition into R1(A, B, C) and R2(C, D)?

A. The decomposition is lossless because the common attribute C determines all attributes of R2.

B. The decomposition is lossy because C is not a primary key in the original relation.

C. The decomposition violates 1NF.

D. The decomposition cannot preserve AB → C.

**Q59.** Consider:

`R(A, B, C, D)`

Functional dependencies:

- A → B
- B → C
- C → D

Candidate key: A.

Which decomposition correctly removes the transitive dependencies while retaining a key-containing relation?

A. R1(A, B), R2(B, C), R3(C, D)

B. R1(A, C), R2(B, D)

C. R1(A, B, C, D) only

D. R1(A, D), R2(B, C)

**Q60.** Consider:

`R(A, B, C)`

Functional dependencies:

- AB → C
- C → B

Candidate keys: AB and AC.

Which statement about 3NF and BCNF is correct?

A. The relation is in BCNF because every determinant is a candidate key.

B. The relation is in 3NF but not BCNF because C is not a superkey but B is prime.

C. The relation violates 3NF because B is non-prime.

D. The relation is in 2NF only because it has composite keys.

---

# Section 8 - 10 Expert-Level Practical Normalization Problems

(Practical SQL / DBMS Exam Level)

For each problem, perform the following:

1. Identify the candidate key(s).
2. Identify all functional dependencies.
3. Identify partial dependencies.
4. Identify transitive dependencies.
5. Determine the highest normal form of the original table.
6. Decompose into 1NF, then 2NF, then 3NF.
7. Identify primary keys and foreign keys in the final tables.

These are decomposition exercises, not additional MCQs.

---

## Problem 1 - Student Enrollment System

Consider the following unnormalized relation:

`STUDENT_COURSE(StudentID, StudentName, CourseID, CourseName, InstructorID, InstructorName, Marks)`

| StudentID | StudentName | CourseID | CourseName | InstructorID | InstructorName | Marks |
| --- | --- | --- | --- | --- | --- | --- |
| S1 | Arun | C1 | DBMS | I1 | Kumar | 90 |
| S1 | Arun | C2 | Java | I2 | Ravi | 85 |
| S2 | Bala | C1 | DBMS | I1 | Kumar | 80 |
| S3 | Charan | C3 | Python | I3 | Anand | 95 |

Business rules:

- A student can enroll in multiple courses.
- A course can have multiple students.
- Each course is assigned exactly one instructor.
- An instructor can teach multiple courses.

Functional dependencies:

- StudentID → StudentName
- CourseID → CourseName, InstructorID
- InstructorID → InstructorName
- (StudentID, CourseID) → Marks

**Questions:**

A. Identify the candidate key.

B. Which attributes have partial dependency?

C. Which attributes have transitive dependency?

D. Identify the highest normal form.

E. Decompose into 2NF and then 3NF.

F. Identify the final tables and their PK/FK relationships.

---

## Problem 2 - Employee and Department Management

`EMPLOYEE(EmpID, EmpName, DeptID, DeptName, ManagerID, ManagerName, Salary)`

| EmpID | EmpName | DeptID | DeptName | ManagerID | ManagerName | Salary |
| --- | --- | --- | --- | --- | --- | --- |
| E1 | Arun | D1 | CSE | M1 | Kumar | 50000 |
| E2 | Bala | D1 | CSE | M1 | Kumar | 45000 |
| E3 | Charan | D2 | ECE | M2 | Ravi | 60000 |
| E4 | Divya | D2 | ECE | M2 | Ravi | 55000 |

Business rules:

- Every employee belongs to one department.
- Every department has one manager.
- A manager can manage multiple employees.
- Each employee has one salary.

Functional dependencies:

- EmpID → EmpName, DeptID, Salary
- DeptID → DeptName, ManagerID
- ManagerID → ManagerName

**Questions:**

A. Identify the candidate key.

B. Identify partial and transitive dependencies, if any.

C. Determine the highest normal form.

D. Decompose the table into 2NF.

E. Decompose the resulting tables into 3NF.

F. Which table should contain ManagerID as a foreign key?

---

## Problem 3 - Order and Product Management

`ORDER_DETAILS(OrderID, ProductID, OrderDate, CustomerID, CustomerName, ProductName, UnitPrice, Quantity)`

| OrderID | ProductID | OrderDate | CustomerID | CustomerName | ProductName | UnitPrice | Quantity |
| --- | --- | --- | --- | --- | --- | --- | --- |
| O1 | P1 | 10-01-2026 | C1 | Arun | Laptop | 50000 | 2 |
| O1 | P2 | 10-01-2026 | C1 | Arun | Mouse | 500 | 3 |
| O2 | P1 | 11-01-2026 | C2 | Bala | Laptop | 50000 | 1 |
| O3 | P3 | 12-01-2026 | C1 | Arun | Keyboard | 1500 | 2 |

Business rules:

- An order contains multiple products.
- A product can appear in multiple orders.
- Every order belongs to one customer.
- Every customer has one name.
- ProductName and UnitPrice are determined by ProductID.

Functional dependencies:

- OrderID → OrderDate, CustomerID
- CustomerID → CustomerName
- ProductID → ProductName, UnitPrice
- (OrderID, ProductID) → Quantity

**Questions:**

A. Find the candidate key.

B. Identify all partial dependencies.

C. Identify all transitive dependencies.

D. Which attributes cause data redundancy?

E. Decompose into 2NF.

F. Decompose into 3NF and identify the final four tables.

---

## Problem 4 - Hospital Appointment System

`APPOINTMENT(PatientID, DoctorID, PatientName, DoctorName, Specialization, AppointmentDate, RoomNo)`

| PatientID | DoctorID | PatientName | DoctorName | Specialization | AppointmentDate | RoomNo |
| --- | --- | --- | --- | --- | --- | --- |
| P1 | D1 | Arun | Kumar | Cardiology | 10-11-2026 | R1 |
| P1 | D2 | Ravi | Bala | Neurology | 11-11-2026 | R2 |
| P2 | D1 | Priya | Kumar | Cardiology | 12-11-2026 | R1 |
| P3 | D3 | Charan | Orthopedic | Orthopedic | 13-11-2026 | R3 |

Assume the following rules:

- A patient can visit multiple doctors.
- A doctor can treat multiple patients.
- A doctor has one specialization.
- Each appointment is uniquely identified by PatientID, DoctorID and AppointmentDate.
- Each doctor has a fixed room number.

Functional dependencies:

- PatientID → PatientName
- DoctorID → DoctorName, Specialization, RoomNo
- (PatientID, DoctorID, AppointmentDate) → all appointment-specific information

**Questions:**

A. Identify the candidate key.

B. Identify partial dependencies.

C. Identify transitive dependencies.

D. What is the highest normal form?

E. Decompose into 2NF.

F. Decompose into 3NF.

G. Which table represents the M:N relationship?

---

## Problem 5 - University Examination System

`EXAM_RESULT(StudentID, SubjectID, StudentName, SubjectName, FacultyID, FacultyName, Marks, Grade)`

| StudentID | SubjectID | StudentName | SubjectName | FacultyID | FacultyName | Marks | Grade |
| --- | --- | --- | --- | --- | --- | --- | --- |
| S1 | SB1 | Arun | DBMS | F1 | Kumar | 90 | A |
| S1 | SB2 | Arun | Java | F2 | Ravi | 80 | B |
| S2 | SB1 | Bala | DBMS | F1 | Kumar | 75 | B |
| S3 | SB3 | Charan | Python | F3 | Anand | 95 | A |

Business rules:

- A student can write multiple subjects.
- A subject can have multiple students.
- Every subject is assigned one faculty member.
- FacultyID determines FacultyName.
- Grade is determined by Marks using a fixed grading scheme.

Functional dependencies:

- StudentID → StudentName
- SubjectID → SubjectName, FacultyID
- FacultyID → FacultyName
- (StudentID, SubjectID) → Marks
- Marks → Grade

**Questions:**

A. Identify the candidate key.

B. Identify partial dependencies.

C. Identify transitive dependencies.

D. Determine the highest normal form.

E. Decompose into 2NF.

F. Decompose into 3NF.

G. Which attributes belong in the STUDENT_SUBJECT relationship table?

---

## Problem 6 - Banking Transaction System

`ACCOUNT_TRANSACTION(AccountID, TransactionID, CustomerID, CustomerName, BranchID, BranchName, TransactionDate, Amount)`

| AccountID | TransactionID | CustomerID | CustomerName | BranchID | BranchName | TransactionDate | Amount |
| --- | --- | --- | --- | --- | --- | --- | --- |
| A1 | T1 | C1 | Arun | B1 | Chennai | 10-11-2026 | 5000 |
| A1 | T2 | C1 | Arun | B1 | Chennai | 11-11-2026 | 2000 |
| A2 | T3 | C2 | Bala | B2 | Bengaluru | 12-11-2026 | 10000 |
| A3 | T4 | C1 | Arun | B1 | Chennai | 13-11-2026 | 3000 |

Business rules:

- Each transaction belongs to one account.
- Each account belongs to one customer.
- A customer can have multiple accounts.
- Each branch has one branch name.
- Each account belongs to one branch.

Functional dependencies:

- TransactionID → AccountID, TransactionDate, Amount
- AccountID → CustomerID, BranchID
- CustomerID → CustomerName
- BranchID → BranchName

**Questions:**

A. Identify the candidate key.

B. Identify the partial dependencies.

C. Identify the transitive dependencies.

D. What is the highest normal form?

E. Decompose into 2NF.

F. Decompose into 3NF.

G. Identify the PK and FK of each final table.

---

## Problem 7 - Library Management System

`BOOK_ISSUE(MemberID, BookID, MemberName, BookName, AuthorID, AuthorName, IssueDate, ReturnDate)`

| MemberID | BookID | MemberName | BookName | AuthorID | AuthorName | IssueDate | ReturnDate |
| --- | --- | --- | --- | --- | --- | --- | --- |
| M1 | B1 | Arun | DBMS | A1 | Kumar | 01-11-2026 | 10-11-2026 |
| M1 | B2 | Arun | Java | A2 | Ravi | 05-11-2026 | 15-11-2026 |
| M2 | B1 | Bala | DBMS | A1 | Kumar | 03-11-2026 | 12-11-2026 |
| M3 | B3 | Charan | Python | A3 | Anand | 06-11-2026 | 16-11-2026 |

Business rules:

- A member can issue multiple books.
- A book can be issued multiple times over time.
- Each book has one author.
- Each author can write multiple books.
- A member can issue the same book again on another date.

Functional dependencies:

- MemberID → MemberName
- BookID → BookName, AuthorID
- AuthorID → AuthorName
- (MemberID, BookID, IssueDate) → ReturnDate

**Questions:**

A. Find the candidate key.

B. Identify partial dependencies.

C. Identify transitive dependencies.

D. Determine the highest normal form.

E. Decompose into 2NF.

F. Decompose into 3NF.

G. Explain why `(MemberID, BookID)` alone is not a suitable candidate key.

---

## Problem 8 - Project Allocation System

`PROJECT_ALLOCATION(EmpID, ProjectID, EmpName, DeptID, DeptName, ProjectName, Hours)`

| EmpID | ProjectID | EmpName | DeptID | DeptName | ProjectName | Hours |
| --- | --- | --- | --- | --- | --- | --- |
| E1 | P1 | Arun | D1 | CSE | Alpha | 20 |
| E1 | P2 | Arun | D1 | CSE | Beta | 15 |
| E2 | P1 | Bala | D1 | CSE | Alpha | 30 |
| E3 | P3 | Charan | D2 | ECE | Gamma | 25 |

Business rules:

- An employee can work on multiple projects.
- A project can have multiple employees.
- An employee belongs to one department.
- Each project has one project name.
- Hours depend on the employee-project combination.

Functional dependencies:

- EmpID → EmpName, DeptID
- DeptID → DeptName
- ProjectID → ProjectName
- (EmpID, ProjectID) → Hours

**Questions:**

A. Identify the candidate key.

B. Identify partial dependencies.

C. Identify transitive dependencies.

D. Find the highest normal form.

E. Decompose into 2NF.

F. Decompose into 3NF.

G. Which table stores Hours?

---

## Problem 9 - Online Shopping and Delivery

`DELIVERY(OrderID, ProductID, CustomerID, CustomerName, DeliveryAgentID, AgentName, ProductName, Quantity, DeliveryDate)`

Business rules:

- An order contains multiple products.
- A customer can place multiple orders.
- Each order belongs to one customer.
- Each order is assigned one delivery agent.
- One delivery agent can handle multiple orders.
- Each product has one name.

Functional dependencies:

- OrderID → CustomerID, DeliveryAgentID
- CustomerID → CustomerName
- DeliveryAgentID → AgentName
- ProductID → ProductName
- (OrderID, ProductID) → Quantity, DeliveryDate

**Questions:**

A. Find the candidate key.

B. Identify partial dependencies.

C. Identify transitive dependencies.

D. Determine the highest normal form.

E. Decompose into 2NF.

F. Decompose into 3NF.

G. Identify which final table represents the order-product relationship.

---

## Problem 10 - Employee Attendance and Payroll

`ATTENDANCE(EmpID, Date, EmpName, DeptID, DeptName, ManagerID, ManagerName, HoursWorked)`

Business rules:

- Each employee belongs to one department.
- Each department has one manager.
- A manager can manage multiple departments? No: each manager manages exactly one department, and each department has exactly one manager.
- An employee can have multiple attendance records.
- HoursWorked is specific to an employee on a particular date.

Functional dependencies:

- EmpID → EmpName, DeptID
- DeptID → DeptName, ManagerID
- ManagerID → ManagerName
- (EmpID, Date) → HoursWorked

**Questions:**

A. Identify the candidate key.

B. Identify partial dependencies.

C. Identify transitive dependencies.

D. Determine the highest normal form.

E. Decompose into 2NF.

F. Decompose into 3NF.

G. Identify the final tables and foreign-key relationships.

---

---

# Section 9 - MCQ Answer Key

Try all 60 before revealing the answers.

**60-question answer key**

## Important concepts to master before attempting the 10 decomposition problems

| Normal form | Main condition | What must be eliminated? |
| --- | --- | --- |
| 1NF | Atomic attribute values; no repeating groups | Multivalued/repeating attributes |
| 2NF | 1NF + no partial dependency of non-prime attributes on candidate keys | Partial dependency |
| 3NF | 2NF + for every non-trivial X → A, X is a superkey or A is prime | Transitive dependency of non-prime attributes |

### Example: Understanding the complete transformation

Consider:

`ENROLLMENT(StudentID, CourseID, StudentName, CourseName, Marks, InstructorID, InstructorName)`

Functional dependencies:

- StudentID → StudentName
- CourseID → CourseName, InstructorID
- InstructorID → InstructorName
- (StudentID, CourseID) → Marks

**Original table**

Composite primary key: StudentID + CourseID

StudentID, CourseID, StudentName, CourseName, Marks, InstructorID, InstructorName

**After 2NF - remove partial dependencies**

**STUDENT**

StudentID (PK)

StudentName

**COURSE**

CourseID (PK)

CourseName

InstructorID

InstructorName

**ENROLLMENT**

StudentID (PK, FK)

CourseID (PK, FK)

Marks

**After 3NF - remove transitive dependency**

**STUDENT**

StudentID (PK)

StudentName

**INSTRUCTOR**

InstructorID (PK)

InstructorName

**COURSE**

CourseID (PK)

CourseName

InstructorID (FK)

**ENROLLMENT**

StudentID (PK, FK)

CourseID (PK, FK)

Marks

(3NF decomposition)

Each non-key attribute is stored with the entity or relationship that determines it. This example assumes the listed dependencies are complete and the keys are as specified.

**Important exam traps:**

1. A composite primary key does not automatically mean partial dependency exists.
2. A single-attribute candidate key cannot have a partial dependency.
3. A table can be in 3NF even when it is not in BCNF.
4. A transitive dependency must be evaluated using the actual functional dependencies, not simply because two columns appear related.
5. Every decomposition should preserve the necessary relationships using primary keys and foreign keys.
6. A decomposition should ideally be both lossless-join and dependency-preserving.

**My recommendation:** Attempt MCQs 1-60 first, then solve the 10 practical decomposition problems without looking at the answer key. The practical problems are especially useful for mastering the difference between 2NF and 3NF.

### User

what is a view syntax of view views example grant select on view revoke select on view dml on view dmls on view will dml on view update the original table what will happen drop view advantages disadvantages of views give 40 question expert level mcq dont give in quiz interface advanced tricky give

### ChatGPT

# DBMS - Views: Complete Study Notes + 40 Expert-Level MCQs

(Expert Level) (40 MCQs)

This covers views in SQL/HSQLDB, including creation, querying, privileges, DML operations, updating original tables through views, dropping views, advantages, disadvantages and tricky edge cases.

# Part 1 - What is a View?

A **View** is a virtual table created using a SQL query on one or more existing tables.

- A view generally does not store the actual result data separately.
- It stores a query definition.
- Whenever a view is queried, the DBMS retrieves data from the underlying tables, subject to the view implementation.
- A view can contain selected columns, filtered rows, joins and aggregate results.

Think of a view as a customized window through which users access data from existing tables.

## 1. Create a view - Syntax

```sql
CREATE VIEW view_name AS
SELECT column1, column2, ...
FROM table_name
WHERE condition;
```

Example: Consider the following table.

**EMPLOYEE**

| EmpID | EmpName | DeptID | Salary |
| --- | --- | --- | --- |
| 101 | Arun | 10 | 50000 |
| 102 | Bala | 20 | 60000 |
| 103 | Charan | 10 | 45000 |
| 104 | Divya | 30 | 70000 |
| 105 | Ezhil | 20 | 55000 |

Create a view containing only employees from department 10.

```sql
CREATE VIEW CSE_EMPLOYEES AS
SELECT EmpID, EmpName, Salary
FROM EMPLOYEE
WHERE DeptID = 10;
```

**View output: CSE_EMPLOYEES**

| EmpID | EmpName | Salary |
| --- | --- | --- |
| 101 | Arun | 50000 |
| 103 | Charan | 45000 |

Important: The view does not independently store these employee records in an ordinary virtual-view implementation. The underlying EMPLOYEE table provides the data.

## 2. Retrieve data from a view

The syntax is the same as querying a normal table.

```sql
SELECT * FROM CSE_EMPLOYEES;
```

You can also apply additional conditions:

```sql
SELECT EmpName
FROM CSE_EMPLOYEES
WHERE Salary > 45000;
```

Output:

| EmpName |
| --- |
| Arun |

The WHERE condition in the query is applied in addition to the view's existing condition.

## 3. Create a view with selected columns

```sql
CREATE VIEW EMPLOYEE_DETAILS AS
SELECT EmpID, EmpName
FROM EMPLOYEE;
```

Output:

| EmpID | EmpName |
| --- | --- |
| 101 | Arun |
| 102 | Bala |
| 103 | Charan |
| 104 | Divya |
| 105 | Ezhil |

The user accessing this view does not need direct access to the Salary or DeptID columns.

## 4. Create a view using multiple tables

Consider:

**DEPARTMENT**

| DeptID | DeptName |
| --- | --- |
| 10 | CSE |
| 20 | ECE |
| 30 | MECH |

Create a view joining employee and department information.

```sql
CREATE VIEW EMP_DEPT_VIEW AS
SELECT E.EmpID,
       E.EmpName,
       D.DeptName
FROM EMPLOYEE E
JOIN DEPARTMENT D
ON E.DeptID = D.DeptID;
```

Output:

| EmpID | EmpName | DeptName |
| --- | --- | --- |
| 101 | Arun | CSE |
| 102 | Bala | ECE |
| 103 | Charan | CSE |
| 104 | Divya | MECH |
| 105 | Ezhil | ECE |

This view combines information from two base tables.

---

# Part 2 - GRANT SELECT on a View

GRANT provides permissions to users.

**Syntax:**

```sql
GRANT SELECT ON view_name TO username;
```

Example:

```sql
GRANT SELECT ON CSE_EMPLOYEES TO user1;
```

This gives user1 permission to retrieve records through the view.

### What does this achieve?

Suppose EMPLOYEE contains:

- EmpID
- EmpName
- DeptID
- Salary
- PhoneNumber
- Address

But CSE_EMPLOYEES exposes only:

- EmpID
- EmpName
- Salary

If user1 is granted SELECT on the view but not on EMPLOYEE, the view can provide controlled access to the exposed data, provided the view owner's underlying privileges and the DBMS's authorization rules permit it.

**Important:** GRANT SELECT on a view does not automatically grant unrestricted SELECT on its original table.

## Part 3 - REVOKE SELECT on a View

REVOKE removes previously granted privileges.

**Syntax:**

```sql
REVOKE SELECT ON view_name FROM username;
```

Example:

```sql
REVOKE SELECT ON CSE_EMPLOYEES FROM user1;
```

After this, user1 cannot use that SELECT privilege on the view unless another applicable authorization path permits access.

### GRANT vs REVOKE

| GRANT | REVOKE |
| --- | --- |
| Provides privileges | Removes privileges |
| Authorizes specified operations | Withdraws specified authorization |
| GRANT SELECT | REVOKE SELECT |
| GRANT UPDATE | REVOKE UPDATE |

---

# Part 4 - DML Operations on Views

This is one of the most important exam topics.

DML operations include:

- INSERT
- UPDATE
- DELETE

**Critical concept:** When a view is updatable, performing DML through that view modifies the underlying base table. The view itself is not an independent copy of the data.

Let's understand each operation.

## 1. UPDATE on a View

Consider:

```sql
CREATE VIEW CSE_EMPLOYEES AS
SELECT EmpID, EmpName, Salary
FROM EMPLOYEE
WHERE DeptID = 10;
```

Execute:

```sql
UPDATE CSE_EMPLOYEES
SET Salary = 55000
WHERE EmpID = 101;
```

What happens?

The corresponding row in the original EMPLOYEE table is updated.

**Original EMPLOYEE table before UPDATE:**

| EmpID | EmpName | DeptID | Salary |
| --- | --- | --- | --- |
| 101 | Arun | 10 | 50000 |
| 102 | Bala | 20 | 60000 |
| 103 | Charan | 10 | 45000 |

**EMPLOYEE table after UPDATE:**

| EmpID | EmpName | DeptID | Salary |
| --- | --- | --- | --- |
| 101 | Arun | 10 | 55000 |
| 102 | Bala | 20 | 60000 |
| 103 | Charan | 10 | 45000 |

The change is reflected when the view is queried again.

## 2. INSERT on a View

Consider:

```sql
CREATE VIEW EMP_VIEW AS
SELECT EmpID, EmpName, Salary
FROM EMPLOYEE;
```

Execute:

```sql
INSERT INTO EMP_VIEW
VALUES (106, 'Gokul', 40000);
```

The DBMS attempts to insert the corresponding row into the underlying EMPLOYEE table.

However, this depends on whether all omitted columns can receive valid values.

For example, if DeptID is NOT NULL and has no default value, the insertion may fail because DeptID is missing.

**Important:** An INSERT through a view does not bypass constraints on the base table.

## 3. DELETE on a View

```sql
DELETE FROM EMP_VIEW
WHERE EmpID = 102;
```

If the view is updatable, the corresponding row is deleted from the original EMPLOYEE table.

The deletion is not restricted to a separate copy maintained by the view.

---

## Part 5 - When can a View be Updated?

Not every view supports INSERT, UPDATE and DELETE.

A view is generally updatable when it represents rows and columns of an underlying table without transformations that make the mapping ambiguous.

### Generally updatable views

| View characteristic | DML support |
| --- | --- |
| SELECT from one base table | Generally updatable |
| Selecting a subset of columns | Generally updatable |
| WHERE condition | Generally updatable, subject to restrictions |
| Renaming columns using aliases | Generally updatable |
| DISTINCT | Generally not updatable |
| GROUP BY | Generally not updatable |
| Aggregate functions | Generally not updatable |
| UNION | Generally not updatable |
| Computed columns | Computed columns themselves are not directly updatable |
| Complex multi-table JOIN | Generally not updatable as a whole |

Exact updateability rules can vary by DBMS.

### Example 1: View with WHERE condition

```sql
CREATE VIEW HIGH_SALARY_EMP AS
SELECT EmpID, EmpName, Salary
FROM EMPLOYEE
WHERE Salary > 50000;
```

Suppose the original table contains:

| EmpID | EmpName | Salary |
| --- | --- | --- |
| 101 | Arun | 40000 |
| 102 | Bala | 60000 |
| 103 | Charan | 70000 |

The view displays:

| EmpID | EmpName | Salary |
| --- | --- | --- |
| 102 | Bala | 60000 |
| 103 | Charan | 70000 |

Now execute:

```sql
UPDATE HIGH_SALARY_EMP
SET Salary = 45000
WHERE EmpID = 102;
```

What happens?

- The underlying EMPLOYEE row is updated.
- Bala's salary becomes 45000.
- Bala no longer satisfies the view's WHERE condition.
- Bala disappears from HIGH_SALARY_EMP when the view is queried again.

(Important exam trap)

The row is not deleted from the original table. It simply stops appearing in the view.

### Example 2: WITH CHECK OPTION

This clause prevents DML through a view from creating rows that do not satisfy the view's WHERE condition.

Syntax:

```sql
CREATE VIEW HIGH_SALARY_EMP AS
SELECT EmpID, EmpName, Salary
FROM EMPLOYEE
WHERE Salary > 50000
WITH CHECK OPTION;
```

Try:

```sql
INSERT INTO HIGH_SALARY_EMP
VALUES (106, 'Gokul', 40000);
```

(Rejected)

The inserted row does not satisfy `Salary > 50000`.

Similarly:

```sql
UPDATE HIGH_SALARY_EMP
SET Salary = 30000
WHERE EmpID = 102;
```

This update is rejected because the updated row would no longer satisfy the view condition.

Without CHECK OPTION, a DBMS may allow such an update through an otherwise updatable view, causing the row to disappear from that view.

### Example 3: View containing GROUP BY

```sql
CREATE VIEW DEPT_SALARY AS
SELECT DeptID, AVG(Salary) AS AvgSalary
FROM EMPLOYEE
GROUP BY DeptID;
```

Output:

| DeptID | AvgSalary |
| --- | --- |
| 10 | 47500 |
| 20 | 57500 |
| 30 | 70000 |

Can you execute?

```sql
UPDATE DEPT_SALARY
SET AvgSalary = 60000
WHERE DeptID = 10;
```

Generally, no.

Why?

The AvgSalary value is calculated from multiple employee rows. The DBMS cannot unambiguously determine which underlying employee salaries should change.

### Example 4: View containing JOIN

```sql
CREATE VIEW EMP_DEPT_VIEW AS
SELECT E.EmpID, E.EmpName, D.DeptName
FROM EMPLOYEE E
JOIN DEPARTMENT D
ON E.DeptID = D.DeptID;
```

This view combines two tables.

An update to a column belonging to one base table may be supported by some DBMSs under certain conditions, but updating both tables through a joined view is generally restricted.

For exam purposes, remember:

- A simple single-table view is the safest updatable-view example.
- Aggregate and GROUP BY views are generally non-updatable.
- A joined view is not automatically fully updatable.

---

# Part 6 - DROP VIEW

DROP VIEW removes the view definition from the database.

**Syntax:**

```sql
DROP VIEW view_name;
```

Example:

```sql
DROP VIEW CSE_EMPLOYEES;
```

What happens?

1. The view is removed.
2. The view definition is removed.
3. The original EMPLOYEE table remains.
4. Original employee records remain unchanged.
5. Other independent views and tables are not automatically deleted.

**Very important:** DROP VIEW is different from DELETE FROM VIEW.

| DROP VIEW | DELETE FROM VIEW |
| --- | --- |
| Removes the view definition | Removes selected underlying records if the view is updatable |
| Does not delete base-table records | Can delete base-table records |
| View can no longer be queried | View continues to exist |
| DDL operation | DML operation |

### DROP VIEW with RESTRICT and CASCADE

In SQL implementations supporting these options:

```sql
DROP VIEW view_name RESTRICT;
```

RESTRICT prevents dropping the view if dependent objects prevent the operation.

```sql
DROP VIEW view_name CASCADE;
```

CASCADE allows dependent objects to be dropped along with the view, subject to DBMS rules.

Be careful: CASCADE does not mean delete all records from the original base tables.

---

# Part 7 - Advantages and Disadvantages of Views

## Advantages

1. **Security:** Restrict users to selected columns and rows.
2. **Data abstraction:** Hide underlying table complexity.
3. **Simplification:** Avoid repeatedly writing complex JOIN queries.
4. **Logical independence:** Provide a stable logical interface when underlying changes can be hidden through compatible views.
5. **Reusability:** Reuse frequently required query definitions.
6. **Customized presentation:** Different users can access different representations of the same data.
7. **Reduced query complexity:** Users can query a view instead of writing complicated queries.

## Disadvantages

1. **Performance overhead:** Complex views can involve expensive queries and joins.
2. **DML restrictions:** Not all views support INSERT, UPDATE and DELETE.
3. **Dependency issues:** Altering or dropping base tables may affect dependent views.
4. **Nested-view complexity:** Views built on other views can become difficult to maintain.
5. **No automatic independent storage:** Ordinary views do not store their own result data.
6. **Limited control over updates:** Aggregate and joined views can be difficult or impossible to update.
7. **Maintenance complexity:** Changes to underlying schemas may require view definitions to be modified.

### Ordinary View vs Materialized View

| Ordinary View | Materialized View |
| --- | --- |
| Stores query definition | Stores query result data |
| Normally retrieves current base-table data when queried | Stores a previously computed result |
| Usually no separate result-storage requirement | Requires storage |
| No separate refresh needed for ordinary query results | Requires refresh or maintenance |
| Useful for abstraction and security | Useful for performance in suitable workloads |

Note: Materialized-view availability and refresh syntax depend on the DBMS. Do not assume every SQL database supports them.

---

---

# Part 8 - 40 Advanced & Expert-Level MCQs on Views

(Expert Level) (40 Questions)

**Instructions:** Choose the single correct answer. Questions include SQL output reasoning, DML effects on original tables, privilege management, updateability and edge cases.

## Section A - View Fundamentals and Creation (Q1-Q8)

**Q1.** Which statement accurately describes an ordinary view?

A. It always stores a separate physical copy of the selected records.

B. It stores a query definition that provides a virtual representation of underlying data.

C. It permanently duplicates all rows from the original table.

D. It automatically creates a primary key on every selected column.

**Q2.** Consider:

```sql
CREATE VIEW EMP_VIEW AS
SELECT EmpID, EmpName
FROM EMPLOYEE
WHERE DeptID = 10;
```

Which statement is correct?

A. EMP_VIEW contains a physically independent copy of employees from department 10.

B. EMP_VIEW contains all employees but hides their department names.

C. EMP_VIEW represents employees satisfying DeptID = 10 and exposes only EmpID and EmpName.

D. EMP_VIEW permanently deletes employees from other departments.

**Q3.** Consider:

```sql
CREATE VIEW HIGH_SALARY AS
SELECT EmpID, EmpName, Salary
FROM EMPLOYEE
WHERE Salary > 50000;
```

The base table contains employees with salaries 40000, 60000 and 80000. How many rows appear in the view?

A. 1

B. 2

C. 3

D. 0

**Q4.** A user executes:

```sql
SELECT EmpName
FROM EMP_VIEW
WHERE Salary > 50000;
```

But EMP_VIEW exposes only EmpID and EmpName.

What happens?

A. The query automatically accesses Salary from the original table.

B. The query succeeds if Salary exists in the base table.

C. The query fails because Salary is not available through the view's exposed columns.

D. Salary is automatically added to the view.

**Q5.** Consider:

```sql
CREATE VIEW V1 AS
SELECT EmpID, Salary * 12 AS AnnualSalary
FROM EMPLOYEE;
```

Which statement is correct?

A. AnnualSalary becomes a permanently stored column in EMPLOYEE.

B. AnnualSalary is a derived expression exposed by the view.

C. Salary is automatically replaced by AnnualSalary in EMPLOYEE.

D. V1 becomes a materialized view automatically.

**Q6.** Which statement about views is correct?

A. Every view must contain a primary key.

B. A view can be created using a SELECT query involving multiple tables.

C. A view cannot contain a WHERE clause.

D. A view must expose every column of the underlying table.

**Q7.** Consider:

```sql
CREATE VIEW V2 AS
SELECT DISTINCT DeptID
FROM EMPLOYEE;
```

Which statement is generally correct?

A. The view contains one row per employee.

B. The view removes duplicate DeptID values from its result.

C. The view automatically updates the primary key of EMPLOYEE.

D. The view is always fully updatable.

**Q8.** A DBA creates two views:

```sql
CREATE VIEW V1 AS
SELECT EmpID, EmpName FROM EMPLOYEE;

CREATE VIEW V2 AS
SELECT EmpID FROM V1;
```

What is V2?

A. A materialized view.

B. A nested view built using another view.

C. A temporary table.

D. A separate physical copy of EMPLOYEE.

## Section B - GRANT and REVOKE (Q9-Q15)

**Q9.** Which SQL statement grants SELECT permission on a view?

A. `GRANT SELECT ON EMP_VIEW TO USER1;`

B. `GRANT EMP_VIEW SELECT TO USER1;`

C. `GRANT SELECT FROM EMP_VIEW TO USER1;`

D. `GRANT USER1 ON EMP_VIEW SELECT;`

**Q10.** Consider:

```sql
GRANT SELECT ON EMP_VIEW TO USER1;
```

Assume USER1 has no direct SELECT privilege on EMPLOYEE, and the DBMS permits access through the view owner's privileges.

Which statement is correct?

A. USER1 automatically receives unrestricted SELECT access to EMPLOYEE.

B. USER1 can access the data exposed through EMP_VIEW under the applicable authorization rules.

C. USER1 can access every column of EMPLOYEE.

D. USER1 becomes the owner of EMP_VIEW.

**Q11.** Which statement revokes SELECT permission from USER1 on EMP_VIEW?

A. `DELETE SELECT ON EMP_VIEW FROM USER1;`

B. `REMOVE SELECT FROM EMP_VIEW USER1;`

C. `REVOKE SELECT ON EMP_VIEW FROM USER1;`

D. `DROP SELECT ON EMP_VIEW;`

**Q12.** Consider:

```sql
GRANT SELECT, UPDATE
ON EMP_VIEW
TO USER1;
```

What permissions are granted?

A. SELECT only

B. UPDATE only

C. Both SELECT and UPDATE

D. INSERT and DELETE

**Q13.** USER1 has SELECT permission on EMP_VIEW but has no INSERT permission. USER1 executes:

```sql
INSERT INTO EMP_VIEW
VALUES (101, 'Arun');
```

Assuming the view is otherwise insertable, what happens?

A. The insertion succeeds because SELECT permission implies INSERT permission.

B. The insertion fails due to insufficient INSERT authorization.

C. The insertion succeeds only if the base table has no primary key.

D. The insertion automatically grants INSERT permission.

**Q14.** Consider:

```sql
GRANT SELECT ON EMP_VIEW TO USER1;

REVOKE SELECT ON EMP_VIEW FROM USER1;
```

What is the final privilege state, assuming no other applicable grant exists?

A. SELECT remains granted.

B. SELECT is revoked.

C. USER1 becomes the owner.

D. EMP_VIEW is dropped.

**Q15.** Which statement about privileges on views is correct?

A. GRANT SELECT on a view always grants SELECT on all its base tables.

B. REVOKE SELECT on a view deletes its underlying records.

C. View privileges and base-table privileges are distinct authorization concepts.

D. Granting UPDATE on a view automatically grants DELETE and INSERT.

## Section C - DML Operations on Views (Q16-Q27)

For Q16-Q19, consider:

**EMPLOYEE**

| EmpID | EmpName | DeptID | Salary |
| --- | --- | --- | --- |
| 101 | Arun | 10 | 50000 |
| 102 | Bala | 20 | 60000 |
| 103 | Charan | 10 | 45000 |
| 104 | Divya | 30 | 70000 |

View:

```sql
CREATE VIEW DEPT10_EMP AS
SELECT EmpID, EmpName, Salary
FROM EMPLOYEE
WHERE DeptID = 10;
```

**Q16.** Execute:

```sql
UPDATE DEPT10_EMP
SET Salary = 55000
WHERE EmpID = 101;
```

What happens, assuming this view is updatable and the operation is authorized?

A. Only the view's independent copy is updated.

B. The original EMPLOYEE row for EmpID 101 is updated.

C. All employees in department 10 are updated.

D. The EMPLOYEE table is deleted and recreated.

**Q17.** Execute:

```sql
UPDATE DEPT10_EMP
SET Salary = 30000
WHERE EmpID = 101;
```

Assuming no WITH CHECK OPTION, what is the expected result for a DBMS that permits updates through this filtered view?

A. The update is rejected because salary must be greater than 50000.

B. The base-table salary becomes 30000, and the row no longer appears in DEPT10_EMP.

C. The original employee row is deleted.

D. The employee's DeptID automatically changes to 20.

**Q18.** Execute:

```sql
DELETE FROM DEPT10_EMP
WHERE EmpID = 103;
```

What happens?

A. The row is removed from the original EMPLOYEE table.

B. Only the view definition is removed.

C. The employee's salary becomes NULL.

D. All department 10 employees are deleted.

**Q19.** Execute:

```sql
INSERT INTO DEPT10_EMP
VALUES (105, 'Ezhil', 40000);
```

Which statement is correct?

A. DeptID is automatically set to 10 because the view has a WHERE clause.

B. The insertion always succeeds.

C. The insertion cannot supply the required DeptID through this view unless the base table provides an applicable default or other mechanism.

D. The insertion changes every existing employee's department.

**Q20.** Consider:

```sql
CREATE VIEW EMP_VIEW AS
SELECT EmpID, EmpName, Salary
FROM EMPLOYEE;
```

The original table also contains DeptID, declared NOT NULL without a default.

Which statement is correct?

A. INSERT through EMP_VIEW must always succeed.

B. INSERT through EMP_VIEW omitting DeptID may fail because the base table's NOT NULL constraint still applies.

C. The view automatically supplies DeptID = NULL.

D. The view disables base-table constraints.

**Q21.** Which operation generally modifies the original base table through an updatable view?

A. `UPDATE view_name SET ...`

B. `ALTER VIEW view_name ...`

C. `DROP VIEW view_name`

D. `CREATE VIEW view_name AS ...`

**Q22.** Consider:

```sql
CREATE VIEW DEPT_VIEW AS
SELECT DeptID, COUNT(*) AS TotalEmployees
FROM EMPLOYEE
GROUP BY DeptID;
```

Which operation is generally not permitted on this view?

A. SELECT

B. UPDATE TotalEmployees

C. Filtering the view result using WHERE in an outer SELECT

D. Retrieving all rows

**Q23.** Consider:

```sql
CREATE VIEW V AS
SELECT EmpID, EmpName
FROM EMPLOYEE
WHERE DeptID = 10
WITH CHECK OPTION;
```

Execute:

```sql
UPDATE V
SET EmpID = 200
WHERE EmpID = 101;
```

Assume EmpID is not referenced by other constraints and the operation is otherwise valid. What happens?

A. The update is rejected because EmpID cannot change through a view.

B. The update can succeed because the updated row still satisfies DeptID = 10.

C. The employee automatically moves to another department.

D. The view is dropped.

**Q24.** Consider a filtered view created with WITH CHECK OPTION:

```sql
CREATE VIEW CSE_VIEW AS
SELECT EmpID, EmpName, DeptID
FROM EMPLOYEE
WHERE DeptID = 10
WITH CHECK OPTION;
```

Execute:

```sql
INSERT INTO CSE_VIEW
VALUES (106, 'Gokul', 20);
```

What happens?

A. The insertion succeeds, but the row is hidden.

B. The insertion is rejected because the new row violates the view condition.

C. The row is inserted into department 10.

D. The view is converted into a table.

**Q25.** A view contains:

```sql
SELECT DeptID, AVG(Salary)
FROM EMPLOYEE
GROUP BY DeptID;
```

Why is direct UPDATE of AVG(Salary) generally not allowed?

A. AVG is a string function.

B. The aggregate represents multiple underlying rows, and the intended base-row changes are ambiguous.

C. Views cannot contain numeric columns.

D. GROUP BY deletes duplicate employees.

**Q26.** Consider a view joining EMPLOYEE and DEPARTMENT.

```sql
CREATE VIEW EMP_DEPT AS
SELECT E.EmpID, E.EmpName, D.DeptName
FROM EMPLOYEE E
JOIN DEPARTMENT D
ON E.DeptID = D.DeptID;
```

Which statement is generally correct?

A. Both base tables can always be modified through every column of this view.

B. Joined views may have restricted updateability; updating multiple base tables through one statement is generally not supported.

C. All joins automatically produce read-only views in every DBMS.

D. A joined view permanently merges the two original tables.

**Q27.** A view exposes only EmpID and EmpName. A user attempts:

```sql
DELETE FROM EMP_VIEW
WHERE Salary > 50000;
```

What happens?

A. All employees with salary greater than 50000 are deleted automatically.

B. The query fails because Salary is not exposed by the view.

C. Salary is automatically included.

D. The view becomes a materialized view.

## Section D - DROP VIEW and Dependencies (Q28-Q33)

**Q28.** Execute:

```sql
DROP VIEW EMP_VIEW;
```

What happens to the underlying EMPLOYEE table?

A. It is automatically dropped.

B. Its records are deleted.

C. It remains unchanged; the view definition is removed.

D. It is converted into a temporary table.

**Q29.** Which SQL statement removes all rows from a base table through an updatable view, without dropping the view definition?

A. `DROP VIEW EMP_VIEW;`

B. `DELETE FROM EMP_VIEW;`

C. `DROP TABLE EMPLOYEE;`

D. `REVOKE SELECT ON EMP_VIEW FROM USER1;`

**Q30.** Consider:

```sql
CREATE VIEW V1 AS
SELECT EmpID, EmpName FROM EMPLOYEE;

CREATE VIEW V2 AS
SELECT EmpID FROM V1;
```

If V1 is dropped, what is the likely consequence for V2?

A. V2 automatically becomes a standalone table.

B. V2 may become invalid because its dependency on V1 is broken.

C. EMPLOYEE is automatically dropped.

D. V2 automatically recreates V1.

**Q31.** What is the purpose of DROP VIEW ... RESTRICT in SQL implementations supporting it?

A. Drop the view and all dependent objects.

B. Prevent dropping the view when dependent objects block the operation.

C. Delete all rows from the base table.

D. Remove only SELECT privilege.

**Q32.** What is the purpose of DROP VIEW ... CASCADE?

A. Drop the view and permit dependent objects to be dropped as part of the operation.

B. Drop all base tables unconditionally.

C. Remove every database user.

D. Convert the view into a physical table.

**Q33.** Which statement correctly distinguishes DROP VIEW from REVOKE SELECT ON VIEW?

A. Both delete the underlying base-table rows.

B. DROP VIEW removes the view definition; REVOKE SELECT removes a specified user's SELECT privilege.

C. REVOKE SELECT drops the view.

D. DROP VIEW only removes one user's permission.

## Section E - Advantages, Disadvantages and Expert Scenarios (Q34-Q40)

**Q34.** A company creates a view exposing only EmployeeID and EmployeeName, hiding Salary and BankAccount. What is the primary advantage?

A. Data normalization

B. Security through restricted data exposure

C. Automatic indexing

D. Elimination of all foreign keys

**Q35.** Which is a genuine disadvantage of ordinary views?

A. They cannot use SELECT statements.

B. Every view requires a separate copy of the original data.

C. Complex views can introduce query-performance overhead and may be difficult to maintain.

D. They cannot be used to restrict access to columns.

**Q36.** An organization has a complex query joining five tables. Different applications repeatedly execute the same query. Which advantage of a view is most relevant?

A. Simplification and query reuse

B. Automatic removal of all duplicate base-table records

C. Automatic enforcement of all foreign keys

D. Elimination of the need for base tables

**Q37.** Which statement correctly compares an ordinary view and a materialized view?

A. Both always store separate physical result data.

B. An ordinary view generally stores a query definition, whereas a materialized view stores computed results.

C. An ordinary view stores results permanently, whereas a materialized view stores only SQL text.

D. Neither can be queried using SELECT.

**Q38.** A DBA modifies the structure of a base table by renaming a column referenced in a view. What may happen?

A. The view is guaranteed to continue working unchanged.

B. The view may become invalid or require modification.

C. All records in the base table are automatically deleted.

D. All privileges are automatically granted again.

**Q39.** Consider:

```sql
CREATE VIEW V AS
SELECT EmpID, Salary
FROM EMPLOYEE
WHERE Salary > 40000;
```

A user executes:

```sql
SELECT *
FROM V
WHERE Salary < 60000;
```

Which condition determines the resulting rows?

A. Salary > 40000 only

B. Salary < 60000 only

C. Both Salary > 40000 and Salary < 60000

D. Neither condition

**Q40.** A view is created using:

```sql
CREATE VIEW V AS
SELECT EmpID, EmpName, Salary
FROM EMPLOYEE;
```

The DBA later executes:

```sql
UPDATE V
SET Salary = Salary + 5000
WHERE EmpID = 101;
```

Which statement is correct, assuming the view is updatable and the user has permission?

A. The original employee's salary increases by 5000.

B. Only the stored query definition changes.

C. A new employee row is inserted.

D. The original table is dropped and recreated.

---

# Section F - Answer Key

Try all 40 before revealing the answers.

**Expert MCQ answer key**

## Last-minute exam revision - View concepts

| Question | Correct concept |
| --- | --- |
| Does UPDATE on an updatable view affect the original table? | Yes |
| Does DELETE on an updatable view affect the original table? | Yes |
| Does INSERT on a view insert into the original table? | Yes, if insertable |
| Does DROP VIEW delete the original table? | No |
| Does REVOKE SELECT delete data? | No |
| Can GROUP BY views generally be updated? | No |
| Can aggregate views generally be updated? | No |
| Can a view expose selected columns only? | Yes |
| Does a view store an independent copy of ordinary query results? | No |
| Does WITH CHECK OPTION enforce the view condition on DML? | Yes |
| Does GRANT SELECT imply GRANT UPDATE? | No |
| Does a base-table constraint still apply to view DML? | Yes |
| Does deleting a row through an updatable view delete its underlying row? | Yes |

**Three particularly important traps for your exam:**

1. Updating a row through a filtered view can make that row disappear from the view without deleting it from the original table.
2. `WITH CHECK OPTION` prevents inserts and updates that make rows violate the view condition.
3. `DROP VIEW` removes the view, whereas `DELETE FROM VIEW` can remove underlying records.

These notes and 40 questions use standard SQL concepts. Check exact syntax and supported privilege/dependency options against your HSQLDB version when practicing.
