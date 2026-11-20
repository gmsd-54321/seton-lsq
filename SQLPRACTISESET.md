> https://chatgpt.com/c/6b0089f5-20a8-83e8-be4b-91880c569051

# SQL Subquery Practice Set

### User

give 60 basic to advanced subquery questions covering all types group by  join inner having query problem set for practice progressive difficulty range till mastery of subqueries give 3 tables data insertion dml each table 15 data

### ChatGPT

# SQL Subqueries - Complete Practice Workbook (60 Questions)

(Beginner → Advanced → Expert) (HSQLDB / SQL)

This problem set is designed to take you from basic subquery understanding to solving complex SQL developer interview and practical assessment questions.

We will use **3 related tables with 15 records each**. Every question will use the same dataset so you can progressively master subqueries without changing the schema.

## 1. Database schema

We will use an Employee Management and Sales database.

**Relationship diagram**

## DEPARTMENT

Primary key: department_id

department_id · department_name · location

One department has many employees

## EMPLOYEE

Primary key: employee_id

employee_id · employee_name · salary · department_id · manager_id · hire_date

One employee can have many sales

## SALES

Primary key: sale_id

sale_id · employee_id · sale_amount · sale_date · sale_status

### Table 1: DEPARTMENT

| department_id | department_name | location |
| --- | --- | --- |
| 10 | IT | Chennai |
| 20 | HR | Bangalore |
| 30 | Finance | Mumbai |
| 40 | Sales | Chennai |
| 50 | Marketing | Hyderabad |

### Table 2: EMPLOYEE

| employee_id | employee_name | salary | department_id | manager_id |
| --- | --- | --- | --- | --- |
| 101 | Arun | 60000 | 10 | NULL |
| 102 | Bala | 45000 | 10 | 101 |
| 103 | Charan | 75000 | 10 | 101 |
| 104 | Divya | 50000 | 20 | NULL |
| 105 | Ezhil | 40000 | 20 | 104 |
| 106 | Farhan | 55000 | 20 | 104 |
| 107 | Gokul | 80000 | 30 | NULL |
| 108 | Hari | 65000 | 30 | 107 |
| 109 | Indhu | 45000 | 30 | 107 |
| 110 | Jai | 70000 | 40 | NULL |
| 111 | Karthik | 50000 | 40 | 110 |
| 112 | Lakshmi | 55000 | 40 | 110 |
| 113 | Manoj | 90000 | 10 | 101 |
| 114 | Nila | 35000 | 20 | 104 |
| 115 | Omkar | 60000 | 30 | 107 |

### Table 3: SALES

| sale_id | employee_id | sale_amount | sale_date | sale_status |
| --- | --- | --- | --- | --- |
| 1 | 101 | 50000 | 2025-01-10 | Completed |
| 2 | 102 | 30000 | 2025-01-15 | Completed |
| 3 | 103 | 80000 | 2025-02-05 | Completed |
| 4 | 104 | 25000 | 2025-02-10 | Pending |
| 5 | 105 | 20000 | 2025-02-15 | Completed |
| 6 | 106 | 45000 | 2025-03-01 | Completed |
| 7 | 107 | 100000 | 2025-03-05 | Completed |
| 8 | 108 | 65000 | 2025-03-10 | Pending |
| 9 | 109 | 35000 | 2025-03-15 | Completed |
| 10 | 110 | 90000 | 2025-04-01 | Completed |
| 11 | 111 | 40000 | 2025-04-05 | Completed |
| 12 | 112 | 60000 | 2025-04-10 | Pending |
| 13 | 113 | 120000 | 2025-04-15 | Completed |
| 14 | 101 | 70000 | 2025-05-01 | Completed |
| 15 | 107 | 50000 | 2025-05-05 | Completed |

---

## 2. Create tables - HSQLDB

Execute these statements in order.

```sql
CREATE TABLE Department (
    department_id INT PRIMARY KEY,
    department_name VARCHAR(30),
    location VARCHAR(30)
);

CREATE TABLE Employee (
    employee_id INT PRIMARY KEY,
    employee_name VARCHAR(30),
    salary DECIMAL(10,2),
    department_id INT,
    manager_id INT,
    hire_date DATE,
    FOREIGN KEY (department_id)
        REFERENCES Department(department_id)
);

CREATE TABLE Sales (
    sale_id INT PRIMARY KEY,
    employee_id INT,
    sale_amount DECIMAL(10,2),
    sale_date DATE,
    sale_status VARCHAR(20),
    FOREIGN KEY (employee_id)
        REFERENCES Employee(employee_id)
);
```

## 3. Insert data - 15 records per table

### A. Department insertion

```sql
INSERT INTO Department VALUES
(10, 'IT', 'Chennai');

INSERT INTO Department VALUES
(20, 'HR', 'Bangalore');

INSERT INTO Department VALUES
(30, 'Finance', 'Mumbai');

INSERT INTO Department VALUES
(40, 'Sales', 'Chennai');

INSERT INTO Department VALUES
(50, 'Marketing', 'Hyderabad');
```

### B. Employee insertion

```sql
INSERT INTO Employee VALUES
(101, 'Arun', 60000, 10, NULL, DATE '2020-01-10');

INSERT INTO Employee VALUES
(102, 'Bala', 45000, 10, 101, DATE '2021-03-15');

INSERT INTO Employee VALUES
(103, 'Charan', 75000, 10, 101, DATE '2019-06-20');

INSERT INTO Employee VALUES
(104, 'Divya', 50000, 20, NULL, DATE '2020-05-12');

INSERT INTO Employee VALUES
(105, 'Ezhil', 40000, 20, 104, DATE '2022-02-10');

INSERT INTO Employee VALUES
(106, 'Farhan', 55000, 20, 104, DATE '2021-08-18');

INSERT INTO Employee VALUES
(107, 'Gokul', 80000, 30, NULL, DATE '2018-11-05');

INSERT INTO Employee VALUES
(108, 'Hari', 65000, 30, 107, DATE '2020-09-15');

INSERT INTO Employee VALUES
(109, 'Indhu', 45000, 30, 107, DATE '2022-04-25');

INSERT INTO Employee VALUES
(110, 'Jai', 70000, 40, NULL, DATE '2019-12-01');

INSERT INTO Employee VALUES
(111, 'Karthik', 50000, 40, 110, DATE '2021-01-20');

INSERT INTO Employee VALUES
(112, 'Lakshmi', 55000, 40, 110, DATE '2020-07-10');

INSERT INTO Employee VALUES
(113, 'Manoj', 90000, 10, 101, DATE '2017-03-05');

INSERT INTO Employee VALUES
(114, 'Nila', 35000, 20, 104, DATE '2023-06-15');

INSERT INTO Employee VALUES
(115, 'Omkar', 60000, 30, 107, DATE '2021-10-10');
```

### C. Sales insertion

```sql
INSERT INTO Sales VALUES
(1, 101, 50000, DATE '2025-01-10', 'Completed');

INSERT INTO Sales VALUES
(2, 102, 30000, DATE '2025-01-15', 'Completed');

INSERT INTO Sales VALUES
(3, 103, 80000, DATE '2025-02-05', 'Completed');

INSERT INTO Sales VALUES
(4, 104, 25000, DATE '2025-02-10', 'Pending');

INSERT INTO Sales VALUES
(5, 105, 20000, DATE '2025-02-15', 'Completed');

INSERT INTO Sales VALUES
(6, 106, 45000, DATE '2025-03-01', 'Completed');

INSERT INTO Sales VALUES
(7, 107, 100000, DATE '2025-03-05', 'Completed');

INSERT INTO Sales VALUES
(8, 108, 65000, DATE '2025-03-10', 'Pending');

INSERT INTO Sales VALUES
(9, 109, 35000, DATE '2025-03-15', 'Completed');

INSERT INTO Sales VALUES
(10, 110, 90000, DATE '2025-04-01', 'Completed');

INSERT INTO Sales VALUES
(11, 111, 40000, DATE '2025-04-05', 'Completed');

INSERT INTO Sales VALUES
(12, 112, 60000, DATE '2025-04-10', 'Pending');

INSERT INTO Sales VALUES
(13, 113, 120000, DATE '2025-04-15', 'Completed');

INSERT INTO Sales VALUES
(14, 101, 70000, DATE '2025-05-01', 'Completed');

INSERT INTO Sales VALUES
(15, 107, 50000, DATE '2025-05-05', 'Completed');
```

Verify:

```sql
SELECT * FROM Department;
SELECT * FROM Employee;
SELECT * FROM Sales;
```

---

# 4. Subquery concepts covered

Before attempting the questions, understand which techniques you need to apply.

| Subquery type | Main operator / position |
| --- | --- |
| Scalar subquery | `=`, `>`, `<` |
| Multiple-row subquery | `IN`, `NOT IN` |
| Comparison subquery | `ANY`, `ALL` |
| Existence subquery | `EXISTS`, `NOT EXISTS` |
| Non-correlated | Independent inner query |
| Correlated | Inner query references outer query |
| Nested subquery | Subquery inside another subquery |
| Multiple-column subquery | Compare multiple columns |
| Inline view | Subquery inside FROM |
| SELECT subquery | Subquery inside SELECT |
| WHERE subquery | Subquery inside WHERE |
| HAVING subquery | Subquery inside HAVING |
| DML subquery | UPDATE / DELETE with subquery |

# 5. Practice questions - 60 questions

Difficulty progression: 1-15 Basic · 16-30 Intermediate · 31-45 Advanced · 46-60 Expert

## Level 1 - Basic subqueries (1-15)

Focus: Scalar subqueries, IN, NOT IN, aggregate functions and simple nested queries.

**Q1.** Find employees whose salary is greater than the average salary of all employees.

**Q2.** Find employees who earn the maximum salary in the company.

**Q3.** Find employees who earn the minimum salary in the company.

**Q4.** Find employees who work in the IT department using a subquery instead of a JOIN.

**Q5.** Find employees who work in the same department as Arun.

**Q6.** Find employees whose salary is greater than Arun's salary.

**Q7.** Find employees whose salary is less than the average salary of employees working in the Finance department.

**Q8.** Find the department details where Arun works.

**Q9.** Find all employees who work in departments located in Chennai.

**Q10.** Find employees whose department is either IT or Finance using IN and a subquery.

**Q11.** Find employees who do not belong to the IT department using NOT IN.

**Q12.** Find employees who have a salary equal to the second-highest distinct salary in the company.

**Q13.** Find employees who earn more than the average salary of their respective department.

**Q14.** Find employees whose salary is equal to the highest salary in their department.

**Q15.** Find employees who earn more than at least one employee in the HR department using ANY.

---

## Level 2 - Intermediate subqueries (16-30)

Focus: ANY, ALL, EXISTS, NOT EXISTS, correlated and multiple-row subqueries.

**Q16.** Find employees whose salary is greater than the salary of every employee in the HR department using ALL.

**Q17.** Find employees whose salary is less than at least one employee in the Finance department using ANY.

**Q18.** Find employees whose salary is greater than all employees in their own department.

**Q19.** Find employees who have made at least one sale using EXISTS.

**Q20.** Find employees who have never made any sale using NOT EXISTS.

**Q21.** Find departments that have at least one employee using EXISTS.

**Q22.** Find departments that do not have any employees using NOT EXISTS.

**Q23.** Find employees who have at least one completed sale.

**Q24.** Find employees who have made sales but none of their sales are pending.

**Q25.** Find employees whose total sales amount is greater than the average sale amount of all sales.

**Q26.** Find employees who work in departments where at least one employee earns more than ₹75,000.

**Q27.** Find employees whose salary is greater than the average salary of employees hired before 2021.

**Q28.** Find employees who belong to the same department as at least one employee who has made a sale greater than ₹80,000.

**Q29.** Find employees who have made a sale greater than the average sale amount of their department.

**Q30.** Find employees who have made more sales transactions than the average number of transactions per employee.

---

## Level 3 - Advanced subqueries with GROUP BY, JOIN and HAVING (31-45)

Focus: Correlated subqueries, grouped results, joins, nested aggregates and HAVING.

**Q31.** Find the department-wise average salary and display only departments whose average salary is greater than the company's overall average salary.

**Q32.** Find departments whose total employee salary is greater than the average of all department-wise total salary values.

**Q33.** Find departments having more employees than the average number of employees per department.

**Q34.** Find departments whose employee count is greater than the employee count of the HR department.

**Q35.** Find employees whose salary is greater than the average salary of their department, and display their department name using an INNER JOIN.

**Q36.** Find department names where the total completed sales amount is greater than ₹1,00,000.

**Q37.** Find departments whose total sales amount is greater than the average total sales amount across departments.

**Q38.** Find employees whose total sales amount is greater than the average total sales amount per employee.

**Q39.** Find the highest-paid employee in every department using a correlated subquery.

**Q40.** Find the second-highest-paid employee in every department using a correlated subquery.

**Q41.** Find departments where the maximum employee salary is greater than the maximum salary of the HR department.

**Q42.** Find employees who have made sales greater than the average sale amount in their own department. Display employee name, department name and sale amount using JOIN and a correlated subquery.

**Q43.** Find employees who have made more sales transactions than the average transaction count of employees in their own department.

**Q44.** Find departments having at least two employees whose salary is greater than the company's average salary. Use GROUP BY and HAVING with a subquery.

**Q45.** Find employees working in departments whose average salary is greater than the average salary of the company, but whose individual salary is less than their department's average salary.

---

## Level 4 - Expert subqueries (46-60)

Focus: Multi-level nesting, multiple correlated conditions, inline views, HAVING subqueries and complex business scenarios.

**Q46.** Find employees whose salary is greater than the average salary of employees working in departments whose average salary is greater than the company's average salary.

**Q47.** Find the department with the second-highest average salary using nested subqueries.

**Q48.** Find departments whose total completed sales amount is greater than the total completed sales amount of the IT department.

**Q49.** Find employees who earn more than the average salary of employees who have generated sales above the overall average sale amount.

**Q50.** Find employees who have generated the highest total sales amount in their respective departments. Handle ties.

**Q51.** Find departments where every employee has a salary greater than ₹40,000. Use NOT EXISTS.

**Q52.** Find employees who have made sales in every month in which at least one sale transaction exists in the dataset. Use NOT EXISTS with nested NOT EXISTS.

**Q53.** Find employees who have completed sales in every month in which they have made at least one sale.

**Q54.** Find employees whose total sales amount is greater than the total sales amount of every employee in the HR department.

**Q55.** Find departments whose total completed sales amount is greater than the average completed sales amount of all employees who have completed at least one sale.

**Q56.** Find employees who have a salary greater than the average salary of their department and whose total sales amount is also greater than the average total sales amount of employees in their department.

**Q57.** Find the department where the difference between maximum and minimum employee salaries is greater than the average salary difference across all departments.

**Q58.** Find employees who have made at least one sale whose amount is greater than the average sale amount of their department, but whose total sales amount is less than the highest total sales amount of any employee in the company.

**Q59.** Find departments whose employee count is greater than the average employee count of departments that have at least one completed sale.

**Q60.** Find employees who satisfy all three conditions:

1. Their salary is greater than their department's average salary.
2. Their total completed sales amount is greater than the average completed sales amount of employees in their department.
3. Their total sales amount is greater than the total sales amount of at least one employee in every other department.

Display employee name, department name, salary and total sales amount.

---

# 6. Additional mastery challenges - Important edge cases

These are not additional numbered questions. They are concepts you should be able to reason about while solving the 60 questions.

| Concept | What to test |
| --- | --- |
| Scalar subquery | What happens if the inner query returns multiple rows? |
| IN | How does it handle duplicate values? |
| NOT IN | What happens if the subquery returns NULL? |
| ANY | What if the subquery returns an empty result? |
| ALL | What if the subquery returns an empty result? |
| EXISTS | Does the selected column inside EXISTS matter? |
| Correlated subquery | How does the inner query reference the outer query? |
| GROUP BY | Can you use aggregate conditions in WHERE? |
| HAVING | Can you put a subquery inside HAVING? |
| JOIN + subquery | Can JOIN and subquery be used in the same query? |
| Nested subquery | How many levels of nesting can you understand and debug? |
| Derived table | Does the subquery in FROM require an alias in your HSQLDB version? |

## 7. Recommended solving progression



## 8. Mastery checklist

By the end of these 60 questions, you should be able to:

- [ ] Identify whether a subquery is scalar or multi-row.
- [ ] Choose correctly between IN, ANY, ALL and EXISTS.
- [ ] Convert a JOIN-based solution into a subquery-based solution.
- [ ] Write correlated subqueries without confusing inner and outer aliases.
- [ ] Use GROUP BY and HAVING with nested queries.
- [ ] Find department-wise maximum, minimum and second-highest values.
- [ ] Compare aggregated results between departments.
- [ ] Write nested NOT EXISTS queries.
- [ ] Solve business problems involving multiple tables and conditions.
- [ ] Identify NULL-related problems with NOT IN.

**My recommendation:** Solve Q1-15 without looking at examples, Q16-30 with special attention to correlated subqueries, and Q31-60 without using JOIN as a substitute for the requested subquery logic. For questions explicitly requiring JOIN, combine both techniques.

This gives you a complete 60-question progression using one consistent 3-table database.

### User

give 20 joins questions 10 GROUP BY 5 SET OPERATION WITH ALL FUNCTIONS MIXED AND GIVE ADVANCED LEVEL ALL

### ChatGPT

# SQL Advanced Practice Set - 35 Questions

(Advanced to Expert) (HSQLDB)

Using the same three tables from the previous exercise: `Department`, `Employee`, and `Sales`, this set focuses on complex query construction, combining multiple SQL concepts rather than testing individual syntax.

**Question distribution:**

| Section | Questions | Focus |
| --- | --- | --- |
| JOINs | 20 | Multi-table, self, outer, aggregate joins |
| GROUP BY | 10 | Aggregations, HAVING, CASE, nested logic |
| SET OPERATIONS | 5 | UNION, UNION ALL, INTERSECT, EXCEPT |
| **Total** | **35** | **Advanced level** |

## Section A - JOINs (20 questions)

Difficulty: Advanced → Expert

These questions mix INNER JOIN, LEFT JOIN, RIGHT JOIN, FULL OUTER JOIN, SELF JOIN, CROSS JOIN, multiple joins, subqueries, CASE and aggregate functions.

**Q1. Department-wise salary and sales analysis**

Display department name, number of employees, average salary, maximum salary, total completed sales amount and total number of completed transactions.

Requirements:

- Use INNER JOIN.
- Use GROUP BY.
- Use COUNT, AVG, MAX and SUM.
- Include only departments having at least 2 employees.
- Sort by total completed sales in descending order.

**Q2. Employees earning more than their department average**

Display employee name, department name, salary and department average salary.

Requirements:

- Use INNER JOIN.
- Use a correlated subquery or a grouped derived table.
- Display only employees earning more than their department's average salary.

**Q3. Employee-manager hierarchy**

Display employee name, manager name, employee salary, manager salary and salary difference.

Requirements:

- Use SELF JOIN.
- Display employees who have managers.
- Display employees whose salary is greater than their manager's salary.

**Q4. Departments without sales**

Display all department names and their total sales amount.

Requirements:

- Use LEFT JOIN.
- Include departments with zero sales.
- Use COALESCE to display zero instead of NULL.
- Use GROUP BY and ORDER BY.

**Q5. Employees without completed sales**

Display employee ID, employee name, department name and salary for employees who have not made any completed sales.

Requirements:

- Use LEFT JOIN.
- Apply the appropriate NULL filtering.
- Ensure employees with only pending transactions are also included.

**Q6. Highest sales employee in each department**

Display department name, employee name and total sales amount of the employee generating the highest total sales in each department.

Requirements:

- Use at least two JOINs.
- Use GROUP BY.
- Use a correlated subquery or derived table.
- Handle ties.

**Q7. Employee salary and sales performance classification**

Display employee name, department name, salary, total sales and performance category.

Classification using CASE:

| Total sales | Category |
| --- | --- |
| Above 100000 | Excellent |
| 50000-100000 | Good |
| Below 50000 | Average |
| No sales | No Sales |

Requirements:

- Use LEFT JOIN.
- Use SUM and COALESCE.
- Use CASE WHEN.
- Group by employee details.

**Q8. Department comparison**

Display department name, average employee salary, total completed sales and number of completed transactions.

Requirements:

- Use INNER JOIN.
- Include only departments whose average salary is greater than ₹50,000.
- Include departments whose total completed sales exceed ₹1,00,000.
- Use GROUP BY and HAVING.

**Q9. Employees with sales greater than their manager's sales**

Display employee name, manager name, employee's total sales and manager's total sales.

Requirements:

- Use SELF JOIN on Employee.
- Join Sales twice.
- Use LEFT JOIN to handle employees without sales.
- Compare aggregated sales amounts.
- Exclude employees without a manager.

**Q10. Department and location combination**

Generate every possible combination of department and employee.

Requirements:

- Use CROSS JOIN.
- Display department name, employee name and employee's department.
- Display only combinations where the employee's department is different from the generated department.

**Q11. All employees and their sales transactions**

Display every employee, including those who have never made a sale.

Requirements:

- Use LEFT JOIN.
- Display employee name, sale ID, sale amount and sale status.
- Use CASE to classify transaction status.
- Sort employees by employee ID and sales by sale ID.

**Q12. Sales contribution percentage**

Display employee name, department name, employee's total sales and percentage contribution to the department's total sales.

Formula:

$$
\text{Contribution} =
\frac{\text{Employee Sales}}{\text{Department Sales}}\times100
$$

Requirements:

- Use JOIN.
- Use GROUP BY or derived tables.
- Use SUM.
- Use NULLIF to avoid division by zero.
- Round the percentage to two decimal places.

**Q13. Employees earning more than the average salary of departments in Chennai**

Display employee name, department name, salary and department location.

Requirements:

- Use INNER JOIN.
- Use a subquery to calculate the average salary of employees working in Chennai.
- Compare every employee's salary against that average.

**Q14. Department-wise completed versus pending sales**

Display department name, completed sales amount, pending sales amount and total sales amount.

Requirements:

- Use INNER JOIN.
- Use conditional aggregation with CASE WHEN.
- Use SUM.
- Group by department.
- Display only departments whose completed sales exceed pending sales.

**Q15. Employees with multiple sales transactions**

Display employee name, department name, transaction count, total sales, average sales and highest sale.

Requirements:

- Use INNER JOIN.
- Use COUNT, SUM, AVG and MAX.
- Use GROUP BY and HAVING.
- Include employees having at least 2 transactions.

**Q16. Find employees who have never generated sales in the same department as an employee who generated more than ₹80,000 in a single transaction.**

Requirements:

- Use multiple JOINs.
- Use NOT EXISTS or NOT IN.
- Use correlated subquery logic.
- Return employee name and department name.

**Q17. Department-wise salary ranking**

Display employee name, department name, salary and salary rank within the department.

Requirements:

- Use JOIN.
- Use DENSE_RANK() OVER (PARTITION BY department_id ORDER BY salary DESC).
- Include employees with the highest and second-highest salary ranks only.

**Q18. Find departments where the highest-paid employee also has the highest total sales in that department.**

Requirements:

- Use multiple JOINs.
- Use GROUP BY.
- Use subqueries or derived tables.
- Compare employee salary ranking and total sales ranking.
- Handle ties correctly.

**Q19. Find employees whose salary is greater than their manager's salary but whose total sales are lower than their manager's total sales.**

Requirements:

- Use SELF JOIN.
- Join the Sales table twice.
- Use aggregate functions.
- Use COALESCE.
- Display employee name, manager name, both salaries and both sales totals.

**Q20. Comprehensive employee performance report**

Generate a report with:

- Employee name
- Department name
- Manager name
- Salary
- Department average salary
- Total sales
- Completed sales
- Pending sales
- Transaction count
- Employee's contribution to department sales
- Salary rank within department

Requirements:

- Use at least three JOIN operations.
- Use SELF JOIN.
- Use conditional aggregation.
- Use GROUP BY.
- Use window functions.
- Use CASE WHEN.
- Include employees who have no sales.
- Sort by department and salary rank.

---

## Section B - GROUP BY and HAVING (10 questions)

Difficulty: Advanced → Expert

These questions focus on aggregate functions, conditional aggregation, nested aggregation, HAVING subqueries and multiple grouping conditions.

**Q21.** Find department-wise average salary, minimum salary, maximum salary, total salary and employee count. Display only departments whose average salary is greater than the company's overall average salary.

**Q22.** Find departments whose total employee salary is greater than the average department-wise total salary.

Use:

- GROUP BY
- SUM
- HAVING
- Nested aggregate subquery

**Q23.** Find employees who have generated more than the average total sales of employees who have at least one completed sale.

Display employee name, transaction count and total sales.

**Q24.** Find the department with the highest difference between maximum and minimum employee salary.

Display department name, maximum salary, minimum salary and salary difference.

If there is a tie, display all matching departments.

**Q25.** Find departments where the number of employees earning above the company's average salary is greater than the number of employees earning below the company's average salary.

Use conditional aggregation with CASE WHEN.

**Q26.** Find monthly sales statistics.

Display:

- Year and month.
- Total sales.
- Completed sales.
- Pending sales.
- Number of transactions.
- Average transaction amount.

Use GROUP BY and conditional aggregation.

**Q27.** Find departments where the total completed sales amount is greater than the average total completed sales amount across departments.

Important: First calculate total completed sales for each department, then calculate the average of those department totals.

**Q28.** Find employees whose completed sales contribution is greater than 20% of their department's completed sales.

Display employee name, department name, employee completed sales, department completed sales and percentage contribution.

**Q29.** Find departments having at least two employees whose salary is above the department's average salary.

Use:

- GROUP BY
- HAVING
- Correlated subquery
- COUNT

**Q30.** Generate a department performance report with the following conditions:

1. Department must have at least 2 employees.
2. Average salary must be above ₹50,000.
3. Total completed sales must be greater than ₹1,00,000.
4. At least 50% of employees must have generated a completed sale.

Display department name, employee count, average salary, total completed sales and completed-sale employee percentage.

Use JOIN, GROUP BY, HAVING and conditional aggregation.

---

## Section C - SET OPERATIONS (5 questions)

(Watch out for duplicate handling and column compatibility)

These questions test UNION, UNION ALL, INTERSECT and EXCEPT.

Remember:

| Operator | Purpose |
| --- | --- |
| UNION | Combines results and removes duplicates |
| UNION ALL | Combines results and retains duplicates |
| INTERSECT | Returns common rows |
| EXCEPT | Returns rows in first query but not second |

All corresponding SELECT statements must have compatible column counts and datatypes.

**Q31. UNION - Employees with high salary or high sales**

Find employees who satisfy either condition:

- Salary greater than ₹70,000.
- Total sales greater than ₹1,00,000.

Display employee ID and employee name.

Use UNION. Duplicate employees must appear only once.

**Q32. UNION ALL - Transaction-based employee list**

Generate two lists:

- Employees who have completed sales.
- Employees who have pending sales.

Display employee ID, employee name and transaction category.

Use UNION ALL.

Employees satisfying both conditions should appear in both result sets.

**Q33. INTERSECT - Employees satisfying two conditions**

Find employees who:

- Earn more than ₹50,000.
- Have made at least one completed sale.

Display employee ID and employee name.

Use INTERSECT between the two queries.

**Q34. EXCEPT - Employees without completed sales**

Find all employees and subtract employees who have made completed sales.

Display employee ID and employee name.

Use EXCEPT.

**Q35. Mixed SET OPERATIONS - Advanced**

Generate a list of employees satisfying the following logic:

- Employees earning more than ₹70,000.
- UNION with employees having total sales greater than ₹1,00,000.
- INTERSECT with employees working in IT or Finance.
- EXCEPT employees who have no completed sales.

Display employee ID and employee name.

Write the solution using multiple set operations. Pay attention to the grouping and evaluation order of the operations.

---

# 8. Function usage checklist

Make sure you use these functions throughout the 35 questions rather than solving everything with basic SELECT and JOIN.

| Category | Functions / operators |
| --- | --- |
| Aggregate | COUNT, SUM, AVG, MIN, MAX |
| Numeric | ROUND, ABS, MOD, CEIL, FLOOR |
| NULL handling | COALESCE, NULLIF |
| Conditional | CASE WHEN |
| String | UPPER, LOWER, LENGTH, SUBSTRING, CONCAT, TRIM |
| Date | EXTRACT, YEAR/MONTH functions where supported, date comparisons |
| Window | ROW_NUMBER, RANK, DENSE_RANK, SUM OVER, AVG OVER |
| Filtering | IN, EXISTS, ANY, ALL, BETWEEN, LIKE |
| Grouping | GROUP BY, HAVING |
| Set operations | UNION, UNION ALL, INTERSECT, EXCEPT |

*HSQLDB note:* Some functions have dialect-specific syntax. Check your HSQLDB version for `CEIL`, `EXTRACT`, date-part and window-function support. The set-operation questions assume support for the standard operators.

## 9. Recommended exam-level challenge

For each question, follow these rules:

1. First write the query without looking at solutions.
2. Predict the output columns and expected rows.
3. Check NULL handling and duplicate rows.
4. Try to solve questions using an alternative approach wherever possible.
5. Avoid unnecessary DISTINCT and GROUP BY.

**35-question completion tracker**

# /35

**Target:** Be able to solve all 35 questions independently, especially Q18-20, Q27-30 and Q35. These are the questions that combine multiple SQL concepts and require you to reason about the result before writing the query.
