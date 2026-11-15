> https://chatgpt.com/c/6af09b69-041c-83ee-bb7a-af79fa90d354

# SQL Practice Workbook

### User

coding operators expressions create table all constraint example give each example should cover all topics  constraints alter table all all aterations drop table truncate dml insert  types insert update types delete all type select where caluse in where distinct like numeric , character datesubstring conversion to_char to_date aggregate functions dcase sstatement sorting order by joins all join cross self inner right/left outer full outer join group by having set operatins give questions totall 5-6 table related first creation give then insertion then based on those give advanced question each topic 20-30 queries give only topics said for ssql practice 10 insert statement per table enough give all sql queries question for dbms handson practice all moderate to advanced give question not sql queries what just give moderate to advanced queries in dml and data get seect statement

### ChatGPT

# HSQLDB - Complete SQL Hands-on Practice Workbook

This workbook is designed for **moderate-to-advanced DBMS practical examinations and SQL developer interviews**.

We will use one common database with 6 related tables. First create the tables, insert 10 records into each table, and then solve the practice questions using the same dataset.

**Important:** The practice section contains questions, not solutions. You should write the SQL statements yourself.

## 1. Database structure

We will create a retail management database with these six tables:

**DEPARTMENT**

department_id (PK) · department_name · location

**EMPLOYEE**

employee_id (PK)

department_id (FK)

manager_id (self FK)

**CUSTOMER**

customer_id (PK)

customer_name

city · email

**PRODUCT**

product_id (PK)

product_name

category · price

**ORDERS**

order_id (PK)

customer_id (FK)

employee_id (FK)

**ORDER_ITEM**

order_item_id (PK) · order_id (FK) · product_id (FK)

quantity · unit_price · discount

**Relationships**

- One department has many employees.
- One employee can manage multiple employees.
- One customer can place multiple orders.
- One employee can handle multiple orders.
- One order can contain multiple products.
- One product can appear in multiple orders.

---

## 2. CREATE TABLE - All constraints

```sql
CREATE TABLE Department (
    department_id INT PRIMARY KEY,
    department_name VARCHAR(40) NOT NULL UNIQUE,
    location VARCHAR(40) NOT NULL
);

CREATE TABLE Employee (
    employee_id INT PRIMARY KEY,
    employee_name VARCHAR(50) NOT NULL,
    email VARCHAR(80) UNIQUE,
    salary DECIMAL(10,2) CHECK (salary > 0),
    hire_date DATE NOT NULL,
    department_id INT,
    manager_id INT,
    FOREIGN KEY (department_id)
        REFERENCES Department(department_id),
    FOREIGN KEY (manager_id)
        REFERENCES Employee(employee_id)
);

CREATE TABLE Customer (
    customer_id INT PRIMARY KEY,
    customer_name VARCHAR(50) NOT NULL,
    email VARCHAR(80) UNIQUE,
    city VARCHAR(40) DEFAULT 'Chennai',
    age INT CHECK (age >= 18),
    credit_limit DECIMAL(10,2)
        CHECK (credit_limit >= 0)
);

CREATE TABLE Product (
    product_id INT PRIMARY KEY,
    product_name VARCHAR(60) NOT NULL,
    category VARCHAR(40) NOT NULL,
    price DECIMAL(10,2) CHECK (price > 0),
    stock INT DEFAULT 0 CHECK (stock >= 0),
    UNIQUE(product_name, category)
);

CREATE TABLE Orders (
    order_id INT PRIMARY KEY,
    customer_id INT NOT NULL,
    employee_id INT,
    order_date DATE NOT NULL,
    status VARCHAR(20)
        DEFAULT 'PENDING'
        CHECK (status IN ('PENDING', 'SHIPPED',
                          'DELIVERED', 'CANCELLED')),
    total_amount DECIMAL(12,2) CHECK (total_amount >= 0),
    FOREIGN KEY (customer_id)
        REFERENCES Customer(customer_id),
    FOREIGN KEY (employee_id)
        REFERENCES Employee(employee_id)
);

CREATE TABLE Order_Item (
    order_item_id INT PRIMARY KEY,
    order_id INT NOT NULL,
    product_id INT NOT NULL,
    quantity INT CHECK (quantity > 0),
    unit_price DECIMAL(10,2) CHECK (unit_price > 0),
    discount DECIMAL(5,2) DEFAULT 0
        CHECK (discount BETWEEN 0 AND 100),
    UNIQUE(order_id, product_id),
    FOREIGN KEY (order_id) REFERENCES Orders(order_id),
    FOREIGN KEY (product_id) REFERENCES Product(product_id)
);
```

This covers:

- PRIMARY KEY
- FOREIGN KEY
- NOT NULL
- UNIQUE
- CHECK
- DEFAULT
- Composite UNIQUE
- Self-referencing FOREIGN KEY
- Multiple constraints in one table

## 3. ALTER TABLE - All important alterations

```sql
-- Add a column
ALTER TABLE Employee ADD phone VARCHAR(15);

-- Add a column with default
ALTER TABLE Customer ADD country VARCHAR(30)
DEFAULT 'India';

-- Add a constraint
ALTER TABLE Employee
ADD CONSTRAINT chk_emp_salary CHECK (salary >= 10000);

-- Add a unique constraint
ALTER TABLE Customer
ADD CONSTRAINT uq_customer_phone UNIQUE (phone);

-- Add a foreign key
ALTER TABLE Employee
ADD CONSTRAINT fk_emp_dept
FOREIGN KEY (department_id)
REFERENCES Department(department_id);

-- Drop a constraint
ALTER TABLE Employee
DROP CONSTRAINT chk_emp_salary;

-- Drop a column
ALTER TABLE Employee DROP COLUMN phone;

-- Rename a column
ALTER TABLE Employee
ALTER COLUMN employee_name RENAME TO emp_name;

-- Change column datatype
ALTER TABLE Employee
ALTER COLUMN emp_name SET DATA TYPE VARCHAR(80);

-- Rename a table (HSQLDB)
ALTER TABLE Employee RENAME TO Staff;
```

Note: Some ALTER syntax varies between HSQLDB versions. Run the rename-table example only after completing the Employee exercises, because subsequent examples use the original table name.

## 4. DROP and TRUNCATE

```sql
-- Remove all records but retain table structure
TRUNCATE TABLE Order_Item;

-- Remove table and its structure
DROP TABLE Order_Item;

-- Drop a table only if it exists
DROP TABLE IF EXISTS Order_Item;
```

Remember: Foreign-key dependencies must be handled before dropping or truncating referenced tables.

---

## 5. INSERT - 10 records per table

The following records are designed to create useful scenarios for joins, grouping, aggregate functions, date filtering, NULL handling, subqueries (where applicable), and DML operations.

### 5.1 Department - 10 records

```sql
INSERT INTO Department VALUES (1, 'IT', 'Chennai');
INSERT INTO Department VALUES (2, 'HR', 'Bangalore');
INSERT INTO Department VALUES (3, 'Finance', 'Mumbai');
INSERT INTO Department VALUES (4, 'Sales', 'Chennai');
INSERT INTO Department VALUES (5, 'Marketing', 'Hyderabad');
INSERT INTO Department VALUES (6, 'Testing', 'Pune');
INSERT INTO Department VALUES (7, 'Support', 'Delhi');
INSERT INTO Department VALUES (8, 'Research', 'Coimbatore');
INSERT INTO Department VALUES (9, 'Operations', 'Mysore');
INSERT INTO Department VALUES (10, 'Legal', 'Kochi');
```

### 5.2 Employee - 10 records

```sql
INSERT INTO Employee VALUES
(101, 'Arun', 'arun@gmail.com', 75000, DATE '2022-01-10', 1, NULL);

INSERT INTO Employee VALUES
(102, 'Bala', 'bala@gmail.com', 55000, DATE '2022-03-15', 1, 101);

INSERT INTO Employee VALUES
(103, 'Charan', 'charan@gmail.com', 45000, DATE '2023-02-20', 2, 101);

INSERT INTO Employee VALUES
(104, 'Deepa', 'deepa@gmail.com', 85000, DATE '2021-06-10', 3, 101);

INSERT INTO Employee VALUES
(105, 'Ezhil', 'ezhil@gmail.com', 60000, DATE '2022-08-25', 4, 102);

INSERT INTO Employee VALUES
(106, 'Farhan', 'farhan@gmail.com', 40000, DATE '2023-11-05', 4, 105);

INSERT INTO Employee VALUES
(107, 'Gokul', 'gokul@gmail.com', 50000, DATE '2024-01-15', 5, 101);

INSERT INTO Employee VALUES
(108, 'Harini', 'harini@gmail.com', 65000, DATE '2021-12-01', 6, 102);

INSERT INTO Employee VALUES
(109, 'Irfan', 'irfan@gmail.com', 35000, DATE '2024-05-20', 7, 103);

INSERT INTO Employee VALUES
(110, 'Jaya', 'jaya@gmail.com', 70000, DATE '2022-09-12', 8, 104);
```

### 5.3 Customer - 10 records

```sql
INSERT INTO Customer VALUES
(201, 'Karthik', 'karthik@gmail.com', 'Chennai', 25, 50000);

INSERT INTO Customer VALUES
(202, 'Lakshmi', 'lakshmi@gmail.com', 'Bangalore', 32, 75000);

INSERT INTO Customer VALUES
(203, 'Manoj', 'manoj@gmail.com', 'Mumbai', 28, 40000);

INSERT INTO Customer VALUES
(204, 'Nithya', 'nithya@gmail.com', 'Chennai', 35, 90000);

INSERT INTO Customer VALUES
(205, 'Praveen', 'praveen@gmail.com', 'Hyderabad', 22, 30000);

INSERT INTO Customer VALUES
(206, 'Rahul', 'rahul@gmail.com', 'Pune', 40, 100000);

INSERT INTO Customer VALUES
(207, 'Sneha', 'sneha@gmail.com', 'Delhi', 29, 60000);

INSERT INTO Customer VALUES
(208, 'Tamil', 'tamil@gmail.com', 'Coimbatore', 45, 80000);

INSERT INTO Customer VALUES
(209, 'Varun', 'varun@gmail.com', 'Mysore', 26, 35000);

INSERT INTO Customer VALUES
(210, 'Yamini', 'yamini@gmail.com', 'Kochi', 31, 55000);
```

### 5.4 Product - 10 records

```sql
INSERT INTO Product VALUES
(301, 'Laptop', 'Electronics', 65000, 20);

INSERT INTO Product VALUES
(302, 'Mobile', 'Electronics', 25000, 50);

INSERT INTO Product VALUES
(303, 'Keyboard', 'Accessories', 1500, 100);

INSERT INTO Product VALUES
(304, 'Mouse', 'Accessories', 800, 150);

INSERT INTO Product VALUES
(305, 'Monitor', 'Electronics', 18000, 30);

INSERT INTO Product VALUES
(306, 'Printer', 'Electronics', 12000, 15);

INSERT INTO Product VALUES
(307, 'Chair', 'Furniture', 7500, 40);

INSERT INTO Product VALUES
(308, 'Table', 'Furniture', 12000, 25);

INSERT INTO Product VALUES
(309, 'Headphones', 'Accessories', 3000, 60);

INSERT INTO Product VALUES
(310, 'Webcam', 'Accessories', 4500, 35);
```

### 5.5 Orders - 10 records

```sql
INSERT INTO Orders VALUES
(401, 201, 105, DATE '2024-01-10', 'DELIVERED', 66500);

INSERT INTO Orders VALUES
(402, 202, 106, DATE '2024-02-15', 'SHIPPED', 25000);

INSERT INTO Orders VALUES
(403, 203, 105, DATE '2024-03-20', 'DELIVERED', 33000);

INSERT INTO Orders VALUES
(404, 204, 107, DATE '2024-04-05', 'PENDING', 18000);

INSERT INTO Orders VALUES
(405, 205, 106, DATE '2024-05-12', 'CANCELLED', 12000);

INSERT INTO Orders VALUES
(406, 206, 108, DATE '2024-06-18', 'DELIVERED', 15000);

INSERT INTO Orders VALUES
(407, 207, 105, DATE '2024-07-22', 'SHIPPED', 12000);

INSERT INTO Orders VALUES
(408, 208, 109, DATE '2024-08-10', 'DELIVERED', 7500);

INSERT INTO Orders VALUES
(409, 201, 107, DATE '2024-09-15', 'PENDING', 4500);

INSERT INTO Orders VALUES
(410, 203, 108, DATE '2024-11-25', 'DELIVERED', 3000);
```

### 5.6 Order_Item - 10 records

```sql
INSERT INTO Order_Item VALUES
(501, 401, 301, 1, 65000, 0);

INSERT INTO Order_Item VALUES
(502, 401, 303, 1, 1500, 0);

INSERT INTO Order_Item VALUES
(503, 402, 302, 1, 25000, 0);

INSERT INTO Order_Item VALUES
(504, 403, 305, 1, 18000, 0);

INSERT INTO Order_Item VALUES
(505, 403, 306, 1, 12000, 0);

INSERT INTO Order_Item VALUES
(506, 403, 304, 3, 1000, 0);

INSERT INTO Order_Item VALUES
(507, 404, 305, 1, 18000, 0);

INSERT INTO Order_Item VALUES
(508, 405, 306, 1, 12000, 0);

INSERT INTO Order_Item VALUES
(509, 406, 307, 2, 7500, 0);

INSERT INTO Order_Item VALUES
(510, 407, 308, 1, 12000, 0);
```

All six tables now have 10 records each. Some customers, departments, and employees deliberately have no matching records in related tables. These are useful for outer joins and unmatched-record questions.

---

# 6. SQL practice question bank

(Moderate to advanced)

Write the SQL statements for every question. Do not create additional tables unless the question explicitly asks you to alter the existing schema.

## A. DDL, constraints and ALTER TABLE - 20 questions

1. Create a new table named `Project` with project ID as primary key, project name as NOT NULL, budget greater than zero, start date, and department ID as a foreign key.
2. Create a table with a composite primary key using two columns.
3. Create a table with a UNIQUE constraint on email and CHECK constraint on salary.
4. Create a table where the city column has a default value of Chennai.
5. Create a table with a composite UNIQUE constraint on product name and category.
6. Create a table with a self-referencing foreign key.
7. Add a new column called `bonus` to Employee.
8. Add a column called `joining_status` with a default value.
9. Add a CHECK constraint to ensure bonus is non-negative.
10. Add a UNIQUE constraint to the employee email column.
11. Add a foreign key to an existing table.
12. Add a composite UNIQUE constraint to two existing columns.
13. Drop an existing CHECK constraint.
14. Drop a UNIQUE constraint.
15. Drop a foreign key constraint.
16. Modify the datatype of employee name to VARCHAR(100).
17. Rename the employee name column.
18. Remove a column from Customer.
19. Rename the Product table.
20. Truncate a table containing records and explain what happens to its structure; then write the statement to drop the table completely.

## B. INSERT statements - 20 questions

1. Insert a new department using all column values.
2. Insert an employee by explicitly specifying column names.
3. Insert a customer while omitting the city column to use its default.
4. Insert a product while omitting the stock column.
5. Insert an order with only mandatory column values.
6. Insert multiple records into a table using separate INSERT statements.
7. Insert a customer with NULL in the email column.
8. Insert a new employee with no manager.
9. Insert a new employee who reports to an existing employee.
10. Insert a new product with a discount-related price using an arithmetic expression.
11. Insert an employee with a calculated salary using an expression.
12. Insert a new order with the current date.
13. Insert a record using a date literal.
14. Insert a new order item referencing an existing order and product.
15. Attempt to insert a duplicate primary key and observe the result.
16. Attempt to insert a duplicate email and observe the result.
17. Attempt to insert a negative salary and observe the result.
18. Attempt to insert a department ID that does not exist.
19. Attempt to insert a NULL value into a NOT NULL column.
20. Insert a new customer with a credit limit calculated from a fixed percentage of another value.

## C. UPDATE statements - 20 questions

1. Increase the salary of every employee by 10%.
2. Increase salary by 15% for employees in department 1.
3. Increase salary by 5000 for employees earning below 50000.
4. Reduce product prices by 5%.
5. Increase stock by 20 units for all products.
6. Update the city of customers from Chennai to Bangalore.
7. Change the status of all pending orders to SHIPPED.
8. Change the status of orders placed before June 2024 to DELIVERED.
9. Set the credit limit to 100000 for customers whose credit limit is below 50000.
10. Update employee salary using an arithmetic expression involving the existing salary.
11. Update the discount of order items to 10% for a particular order.
12. Update product prices based on their category.
13. Increase salary by 20% for employees whose salary is less than the average salary.
14. Update an employee's department based on their employee ID.
15. Update manager ID for an employee.
16. Update the order total for a particular order.
17. Update the customer city for customers who have placed at least one order.
18. Update the stock of products that have been ordered.
19. Update the salary of employees belonging to departments located in Chennai.
20. Update multiple columns in one UPDATE statement.

## D. DELETE statements - 20 questions

1. Delete a customer using customer ID.
2. Delete all customers from a particular city.
3. Delete products whose stock is zero.
4. Delete employees earning less than 40000.
5. Delete all cancelled orders.
6. Delete orders placed before January 2024.
7. Delete customers who have never placed an order.
8. Delete employees who do not belong to any department.
9. Delete products belonging to the Accessories category.
10. Delete all order items belonging to a particular order.
11. Delete customers whose credit limit is below 40000.
12. Delete orders having total amount below 5000.
13. Delete employees hired before 2022.
14. Delete employees who have no subordinates.
15. Delete products that have never been ordered.
16. Delete customers who have not placed any delivered orders.
17. Delete all employees belonging to a particular department.
18. Delete records from Order_Item based on a condition in Product.
19. Delete orders handled by a particular employee.
20. Delete all records from a table without deleting its structure.

---

## E. SELECT, WHERE and filtering - 30 questions

1. Display all employee records.
2. Display only employee name and salary.
3. Display employees earning more than 50000.
4. Display employees earning between 40000 and 70000.
5. Display employees whose salary is not equal to 50000.
6. Display employees belonging to departments 1, 3 and 5 using IN.
7. Display employees not belonging to departments 1 and 2.
8. Display customers whose city is Chennai or Bangalore.
9. Display products with prices between 3000 and 20000.
10. Display orders whose status is either SHIPPED or DELIVERED.
11. Display employees whose names start with A.
12. Display employees whose names end with a.
13. Display employees whose names contain the letter a.
14. Display employees whose names have exactly five characters.
15. Display employees whose second character is a.
16. Display customers whose email contains gmail.
17. Display customers whose email does not contain gmail.
18. Display products whose names start with M or L.
19. Display employees with salary greater than 50000 and belonging to department 1.
20. Display employees with salary greater than 50000 or belonging to department 2.
21. Display employees with salary greater than 40000 but not belonging to department 1.
22. Display customers whose age is between 25 and 40.
23. Display customers whose age is not between 25 and 40.
24. Display employees whose manager ID is NULL.
25. Display employees whose manager ID is NOT NULL.
26. Display unique cities from Customer using DISTINCT.
27. Display unique product categories.
28. Display unique combinations of city and age.
29. Display orders placed in November 2024.
30. Display orders placed between January and June 2024, excluding cancelled orders.

## F. Numeric, character and string functions - 20 questions

1. Display employee names in uppercase.
2. Display employee names in lowercase.
3. Display employee names with their character length.
4. Display the first three characters of every employee name using SUBSTRING.
5. Display the last two characters of every employee name.
6. Display employee names with the first character extracted.
7. Display employee names with their first and last characters concatenated.
8. Display employee name and salary rounded to the nearest thousand.
9. Display employee salary rounded to two decimal places.
10. Display employee salary truncated to the nearest integer.
11. Calculate the remainder when salary is divided by 10000.
12. Calculate annual salary from monthly salary.
13. Calculate salary after a 15% increment.
14. Calculate a 10% discount on every product.
15. Display the absolute difference between product price and 10000.
16. Display product prices using CEIL and FLOOR.
17. Extract the first five characters of product names.
18. Display customer names and the position of the letter a in their names.
19. Display employee names and their concatenated department IDs.
20. Display product names padded with a specified character.

## G. DATE functions and conversions - 20 questions

Use HSQLDB date functions and conversion functions such as `TO_CHAR`, `TO_DATE`, and `CAST` where supported by your version.

1. Display all orders with their order dates.
2. Extract the year from every order date.
3. Extract the month number from every order date.
4. Extract the day from every order date.
5. Display the month name of every order date using TO_CHAR.
6. Display dates in DD-MM-YYYY format.
7. Display dates in YYYY-MM-DD format.
8. Display orders placed in November.
9. Display orders placed in the year 2024.
10. Display orders placed between March and August.
11. Display employees hired in 2022.
12. Display employees hired in January.
13. Display employees hired before 2023.
14. Display employees hired after 2022.
15. Convert a character date into DATE using TO_DATE.
16. Convert a DATE value into a character value using TO_CHAR.
17. Convert a character number into a numeric value.
18. Calculate the difference between employee joining dates and a specified date.
19. Display employees who joined in the last five years.
20. Display orders sorted by year and month.

## H. Aggregate functions - 20 questions

1. Find the total number of employees.
2. Find the average salary of employees.
3. Find the maximum salary.
4. Find the minimum salary.
5. Find the total salary paid to all employees.
6. Find the average product price.
7. Find the total stock of all products.
8. Find the total number of customers.
9. Find the total order amount.
10. Find the maximum order amount.
11. Find the minimum order amount.
12. Find the number of orders in each status.
13. Find the average salary of employees in each department.
14. Find the total salary paid by each department.
15. Find the number of employees in each department.
16. Find the total quantity sold for each product.
17. Find the total revenue generated by each product.
18. Find the average credit limit of customers in each city.
19. Find the maximum and minimum salary in each department.
20. Find the number of distinct product categories.

## I. CASE statement - 20 questions

1. Display employee salary grades: above 70000 as High, 50000-70000 as Medium, and below 50000 as Low.
2. Categorize employees as Senior or Junior based on salary.
3. Categorize customers by age into Young, Adult and Senior.
4. Categorize products as Expensive, Moderate or Cheap.
5. Display order status with custom descriptions.
6. Display employee name and department classification using CASE.
7. Display employee bonus as 20% for salary above 70000, 10% for salary above 50000, otherwise 5%.
8. Display product availability as Available or Out of Stock.
9. Categorize orders based on total amount.
10. Display customer credit risk based on credit limit.
11. Display salary after increment based on department.
12. Display a message based on employee joining year.
13. Categorize orders as Recent or Old based on order date.
14. Display customer loyalty categories based on number of orders.
15. Display employee performance categories based on salary.
16. Display a custom label for each product category.
17. Display whether an employee is a manager or non-manager.
18. Display order status as Completed, In Progress or Failed.
19. Use CASE inside an aggregate function to count delivered and cancelled orders separately.
20. Use CASE inside SUM to calculate total revenue for different order statuses.

## J. ORDER BY and sorting - 15 questions

1. Display employees in ascending order of salary.
2. Display employees in descending order of salary.
3. Sort employees by department ID and salary.
4. Sort employees by hire date from newest to oldest.
5. Sort products by price from highest to lowest.
6. Sort customers alphabetically.
7. Sort orders by order date.
8. Sort orders by total amount and then order date.
9. Sort employees by department ID ascending and salary descending.
10. Sort products by category and price.
11. Display the top three highest-paid employees using ORDER BY and FETCH FIRST.
12. Display the three cheapest products.
13. Display the most recent five orders.
14. Sort customers by city and then age.
15. Sort orders by status and total amount.

---

## K. JOINS - 30 questions

### Inner Join - 5 questions

1. Display employee names along with their department names.
2. Display customer names and their order IDs.
3. Display order IDs, customer names and order dates.
4. Display employee names, order IDs and order amounts.
5. Display product names, order IDs and quantities purchased.

### LEFT OUTER JOIN - 5 questions

1. Display all customers along with their orders, including customers who have never placed an order.
2. Display all departments along with employees, including departments without employees.
3. Display all products along with their order item details, including products never ordered.
4. Display all employees with their department names, including employees without a department.
5. Display all customers and their delivered orders, retaining customers without delivered orders.

### RIGHT OUTER JOIN - 4 questions

1. Display all departments and their employees using RIGHT JOIN.
2. Display all products and their order item details using RIGHT JOIN.
3. Display all customers and their orders using RIGHT JOIN.
4. Display all employees and their departments using RIGHT JOIN.

### FULL OUTER JOIN - 4 questions

1. Display all employees and departments, including unmatched records from both tables.
2. Display all customers and orders, including customers without orders and orders without matching customers.
3. Display all products and order items, including unmatched records.
4. Display all employees and departments using FULL OUTER JOIN and identify unmatched records.

### CROSS JOIN - 3 questions

1. Generate every possible combination of employees and departments.
2. Generate every possible combination of products and customers.
3. Generate all possible combinations of employees and products, displaying employee names and product names.

### SELF JOIN - 4 questions

1. Display employee names alongside their manager names.
2. Display employees who report to Arun.
3. Display employees and their managers, including employees without managers.
4. Find employees working under the same manager.

### Multiple-table JOIN - 5 questions

1. Display customer name, order ID, employee name and order amount.
2. Display customer name, order ID, product name and quantity purchased.
3. Display employee name, department name, customer name and order amount.
4. Display customer name, product name, quantity, unit price and total item value.
5. Display order ID, customer name, employee name, product name, category and order date using all five related tables.

## L. GROUP BY and HAVING - 25 questions

1. Find the total salary of each department.
2. Find the average salary of each department.
3. Find the maximum salary in each department.
4. Find the minimum salary in each department.
5. Count the employees in each department.
6. Display departments having more than two employees.
7. Display departments having an average salary greater than 50000.
8. Display departments whose total salary exceeds 100000.
9. Find the number of customers in each city.
10. Display cities having more than one customer.
11. Find the average customer age in each city.
12. Find the total credit limit for each city.
13. Find the total number of orders placed by each customer.
14. Display customers who have placed more than one order.
15. Find the total order amount for each customer.
16. Display customers whose total order amount exceeds 30000.
17. Find the number of orders in each status.
18. Display order statuses having more than two orders.
19. Find the total quantity sold for each product.
20. Find products whose total quantity sold exceeds one.
21. Find the total revenue generated by each product.
22. Find product categories having an average price greater than 10000.
23. Find the total revenue generated by each product category.
24. Find employees who have handled more than one order.
25. Display department-wise employee count and average salary, but only for departments with at least two employees and average salary greater than 50000.

## M. SET OPERATIONS - 20 questions

Use `UNION`, `UNION ALL`, `INTERSECT` and `EXCEPT` (or `MINUS`, depending on HSQLDB version).

1. Display all cities appearing in Customer and Department location without duplicates.
2. Display all cities appearing in Customer and Department location including duplicates.
3. Find cities common to Customer and Department.
4. Find customer cities that do not appear in Department locations.
5. Find department locations that do not appear in Customer cities.
6. Combine employee names and customer names into one result.
7. Combine employee names and product names using UNION.
8. Combine employee names and customer names using UNION ALL.
9. Find cities common to customer records and department locations.
10. Find cities available only in customer records.
11. Find cities available only in department records.
12. Combine two lists of names after converting both to uppercase.
13. Combine employee IDs and customer IDs into one result.
14. Display all distinct numeric IDs from Employee and Customer.
15. Display all IDs from Employee and Customer while preserving duplicates.
16. Find IDs common to Employee and Customer.
17. Find employee IDs that do not exist in Customer.
18. Find customer IDs that do not exist in Employee.
19. Combine product names from two different product categories using UNION.
20. Compare the results of UNION and UNION ALL using customer cities and department locations.

---

# 7. Advanced mixed SQL examination questions

These questions combine multiple topics. They are especially useful for practical assessments where the examiner expects you to choose the correct SQL constructs yourself.

## Set 1 - Filtering, expressions, functions and CASE (20 questions)

1. Display employee names, monthly salaries, annual salaries and salaries after a 12% increment.
2. Display employees earning between 40000 and 80000, excluding employees from department 4.
3. Display employees whose names contain the letter 'a' and whose salaries are above the average salary of all employees.
4. Display product names, original prices, discounted prices and final prices after a 15% discount.
5. Display customers whose names contain exactly five characters and whose age is greater than 25.
6. Display employee names with the first three characters in uppercase and the remaining characters in lowercase.
7. Display orders placed during the first half of 2024 with their month names.
8. Display employees hired in 2022 or 2023, sorted by hire date.
9. Display products whose prices are not between 3000 and 20000.
10. Display customers whose city starts with C or ends with e.
11. Display employee names, salaries and salary grades using CASE.
12. Display orders with custom labels for each order status using CASE.
13. Calculate the final price of every product after applying a category-dependent discount.
14. Display employees whose salaries are divisible by 5000.
15. Display employees whose hire date falls in the first quarter of the year.
16. Display orders whose total amount is greater than 10000 and whose status is not CANCELLED.
17. Display customer names and their email domain extracted using string functions.
18. Display the product name and the number of characters in each product name, sorted by length.
19. Display employees with salary rounded to the nearest 1000.
20. Display orders with their year, month name and formatted order date.

## Set 2 - Advanced JOIN and aggregation (20 questions)

1. Display each department name and the number of employees working in it, including empty departments.
2. Display all customers and their total number of orders, including customers with zero orders.
3. Display all products and their total quantity sold, including products never ordered.
4. Display each employee's name, manager's name and department name.
5. Display customer name, number of orders and total order value.
6. Display each product category and total revenue generated.
7. Display employees who handled orders worth more than 20000 in total.
8. Display departments and their highest-paid employee.
9. Display all customers with their most recent order date.
10. Display products whose total sales quantity is greater than the average quantity sold per product.
11. Display customer name, order ID, product name and total item price after discount.
12. Display employees who have handled orders for customers from the same city as their department location.
13. Display department-wise employee count and total salary, sorted by total salary.
14. Display all products with the number of different orders in which they appear.
15. Display customers who have purchased products belonging to the Electronics category.
16. Display each employee and the number of distinct customers they have handled.
17. Display departments having more than one employee and a total salary above 100000.
18. Display each customer and the total amount spent on delivered orders.
19. Display each employee with their manager's salary and their own salary.
20. Display all customers, including customers without orders, along with the number of delivered, pending and cancelled orders using conditional aggregation.

## Set 3 - Advanced GROUP BY, HAVING and JOIN (20 questions)

1. Find the average order amount for each customer city.
2. Find customer cities whose total order value exceeds 30000.
3. Find products with total revenue greater than 10000.
4. Find departments where the highest salary is greater than 70000.
5. Find employees who have handled at least two orders and whose average order amount is greater than 10000.
6. Find product categories with more than two products.
7. Find customers who have purchased more than one distinct product.
8. Find order statuses where the average order amount is greater than 10000.
9. Find the department with the highest total salary.
10. Find the city with the highest number of customers.
11. Find the product category with the highest average price.
12. Find employees whose total handled order amount exceeds the average order amount of all orders.
13. Find customers who have placed orders in more than one month.
14. Find the number of orders handled by each employee for each order status.
15. Find the total quantity sold for every category.
16. Find customers whose total spending exceeds their credit limit.
17. Find employees whose salary is greater than their department's average salary.
18. Find departments with at least one employee earning more than 70000.
19. Find customers who have purchased products from more than one category.
20. Find the employee who handled the highest number of orders.

## Set 4 - SQL operators and expressions (20 questions)

1. Display employee names and salaries after adding a 10% increment using arithmetic operators.
2. Find employees whose salary is divisible by 2 and greater than 40000.
3. Find employees whose salary is not divisible by 2.
4. Find products whose price is greater than 10000 AND stock is greater than 20.
5. Find products whose price is less than 2000 OR stock is greater than 100.
6. Find employees whose department ID is not equal to 1 using NOT.
7. Find customers whose age is between 25 and 35 using BETWEEN.
8. Find customers whose city is IN Chennai, Mumbai or Bangalore.
9. Find employees whose salary is greater than 50000 AND whose department is either 1 or 3.
10. Find employees whose salary is greater than 50000 OR whose hire date is before 2022.
11. Display employee salary and bonus using the ternary-equivalent CASE expression.
12. Display product name, price and a calculated tax of 18%.
13. Calculate the final amount after applying a 10% discount and adding 18% tax.
14. Find products where stock multiplied by price exceeds 100000.
15. Display employee name and salary with a concatenated description.
16. Find customers whose age is NOT BETWEEN 20 AND 30.
17. Find employees who belong to department 1 or 2 but do not earn below 50000.
18. Find orders where the status is not PENDING or CANCELLED.
19. Calculate the percentage contribution of each order to the total order amount.
20. Display products where the price is greater than the average product price, using a suitable SQL expression.

---

## 8. Practical examination challenge - 15 mixed questions

Try these without looking at the topic headings. You must identify which SQL clauses and functions are required.

1. Generate a report showing employee name, department name, manager name, monthly salary, annual salary and salary grade. Include employees without managers.

2. Generate a customer report showing customer name, city, total orders, total spending and customer category. Include customers who have never placed orders.

3. Generate a product sales report showing product name, category, original price, total quantity sold, total revenue and stock availability. Include products never ordered.

4. Display the top three employees based on total order value handled.

5. Display the top three products based on total quantity sold.

6. Display department-wise employee count, average salary, maximum salary and minimum salary. Include departments without employees.

7. Generate a monthly sales report showing month name, number of orders and total order amount.

8. Display customers who have placed orders but have never purchased an Electronics product.

9. Display employees who earn more than their manager.

10. Display employees who have the same salary as at least one other employee.

11. Display customers whose total delivered order amount exceeds 50000.

12. Display products that have never been ordered and sort them by price.

13. Display employees who have handled orders for more than one customer.

14. Display customer name, order count, delivered order count, pending order count and cancelled order count in one report.

15. Generate a complete retail sales report containing customer, employee, department, order, product, quantity, discount and final item amount.

---

## 9. Topic coverage checklist



[Reset progress]

**Recommended order:** Complete table creation and insertion first, then DML, SELECT filtering, functions, joins, grouping, set operations and finally the mixed examination questions.

**HSQLDB note:** Check your installed HSQLDB version for function and ALTER TABLE syntax differences. In particular, `EXCEPT` versus `MINUS`, date formatting functions and full outer join support can vary by SQL dialect/version. Also, HSQLDB does not use MySQL's `LIMIT` syntax; use `FETCH FIRST n ROWS ONLY` for top-N questions.

### User

give 20 more  data select statement for each and add subquery along with it at end 20 subquery questions

### ChatGPT

# HSQLDB - 20 More Advanced SELECT Practice Questions + 20 Subquery Questions

These questions continue using the same six tables: `Department`, `Employee`, `Customer`, `Product`, `Orders`, and `Order_Item`.

No solutions included. Write the SQL queries yourself.

## Part 1 - 20 Advanced SELECT statement questions

These focus on combining WHERE, DISTINCT, LIKE, BETWEEN, IN, date functions, CASE, aggregate functions, GROUP BY, HAVING, ORDER BY and JOINs.

1. Display employee names, department names and salaries of employees who earn more than 45000 and work in departments located in Chennai or Bangalore.

2. Display customers who have placed orders in 2024, along with their order IDs, order dates and order statuses. Display each customer only once.

3. Display product names, categories, prices and stock values for products whose price is above 5000 and whose stock is below 50. Sort by category and price descending.

4. Display employee names and their hire dates in `DD-MON-YYYY` format. Display only employees hired between 2021 and 2023.

5. Display customer names and their email addresses where the email contains the letter 'a' at least twice.

6. Display employees whose salary is greater than 50000, whose names contain 'a', and who do not belong to departments 2, 4 or 7.

7. Display each department name, employee count, average salary and maximum salary. Include departments without employees.

8. Display each customer name, number of orders and total order amount. Sort customers by total spending in descending order.

9. Display product names, total quantities sold and total sales value after applying the discount percentage stored in Order_Item.

10. Display the employee name, department name, manager name and the difference between employee salary and manager salary.

11. Display customers who have placed orders with status DELIVERED and whose total order value is greater than 10000.

12. Display all products whose names have more than five characters, whose price is between 1000 and 20000, and whose category is not Electronics.

13. Display the number of orders and average order amount for each month of 2024, showing the month name rather than only the month number.

14. Display each employee's name, salary, department name and a CASE-based salary classification. Sort by salary classification and salary.

15. Display the top three customers based on the total amount of their orders.

16. Display each product category, number of products, minimum price, maximum price and average price. Only include categories with at least two products.

17. Display customers who purchased products from Electronics and Accessories categories, showing their customer name and product categories.

18. Display all employees and the total number of orders they handled, including employees who have not handled any orders.

19. Display the total quantity sold, total revenue and average selling price for every product. Include products that have never been ordered.

20. Generate a detailed order report with order ID, customer name, employee name, department name, product name, quantity, unit price, discount, final item value and order date. Sort by order date from newest to oldest.

---

# Part 2 - 20 Subquery practice questions

(Advanced SQL)

These questions specifically test scalar subqueries, multi-row subqueries, correlated subqueries, nested subqueries, EXISTS, NOT EXISTS, IN, ANY, ALL and subqueries inside SELECT, FROM and WHERE.

## A. Single-row and scalar subqueries - 5 questions

1. Display employees whose salary is greater than the average salary of all employees.

2. Display the employee who earns the maximum salary in the company.

3. Display products whose price is greater than the average price of all products.

4. Display customers whose credit limit is greater than the average credit limit of all customers.

5. Display employees who earn more than the employee named Bala.

## B. Multi-row subqueries - 5 questions

6. Display employees who work in departments located in Chennai or Bangalore using a subquery.

7. Display customers who have placed at least one order using IN.

8. Display products whose IDs appear in Order_Item.

9. Display employees whose salary is greater than ANY salary earned by employees in department 2.

10. Display employees whose salary is greater than ALL salaries earned by employees in department 4.

## C. Correlated subqueries - 5 questions

11. Display employees whose salary is greater than the average salary of their respective departments.

12. Display the highest-paid employee in each department using a correlated subquery.

13. Display customers who have placed more orders than the average number of orders per customer.

14. Display products whose price is greater than the average price of their own category.

15. Display employees who earn the maximum salary among employees having the same manager.

## D. EXISTS, NOT EXISTS and nested subqueries - 5 questions

16. Display customers who have placed at least one order using EXISTS.

17. Display customers who have never placed an order using NOT EXISTS.

18. Display products that have never been ordered using NOT EXISTS.

19. Display employees who have handled orders for customers from Chennai using nested EXISTS.

20. Display customers who have purchased every product belonging to the Electronics category using nested NOT EXISTS.

---

## Part 3 - Extra subquery challenges

Try these after completing the 20 questions above.

| No. | Challenge |
| --- | --- |
| 1 | Find the second-highest salary without using FETCH FIRST or LIMIT. |
| 2 | Find the third-highest product price. |
| 3 | Find employees earning the second-highest salary in each department. |
| 4 | Find customers who placed orders with amounts greater than the overall average order amount. |
| 5 | Find products whose total revenue is greater than the average product revenue. |
| 6 | Find departments whose average salary is greater than the company's average salary. |
| 7 | Find customers who have purchased the most expensive product. |
| 8 | Find employees who have never handled an order. |
| 9 | Find the customer who has spent the highest total amount. |
| 10 | Find employees whose salary is greater than their manager's salary. |

**Important HSQLDB practice:** Pay particular attention to correlated subqueries, `IN` versus `EXISTS`, `NOT IN` with NULL values, `ANY` versus `ALL`, and subqueries used in the SELECT list. Some advanced queries may need rewriting depending on HSQLDB version and supported syntax.

### User

give 30 more question on each all advanced questions

### ChatGPT

# HSQLDB - Advanced SQL Practice Set (60 Questions)

This is the next level of your SQL hands-on preparation. It contains **30 advanced SELECT questions and 30 advanced SUBQUERY questions** using the same six tables.

The questions are designed around complex conditions, multiple joins, aggregate calculations, correlated subqueries, nested queries, NULL handling, EXISTS, NOT EXISTS, ANY and ALL.

No solutions are provided. Your task is to write the complete SQL query for each question.

# Part 1 - 30 Advanced SELECT Questions

## A. Advanced WHERE, operators and expressions

1. Display employees whose salary is greater than the average salary of their department, but less than 80000. *(Use JOIN and GROUP BY.)*

2. Display employees whose names start with a vowel and whose salary is greater than 40000.

3. Display customers whose email contains their name (case-insensitive comparison) and whose credit limit is above 50000.

4. Display products whose price is between 1000 and 20000, stock is greater than 20, and category is either Accessories or Electronics.

5. Display orders placed during the second and fourth quarters of 2024, excluding cancelled orders.

6. Display employees whose hire date falls on a Monday or Friday. Use the appropriate HSQLDB date function.

7. Display employees whose salary is divisible by 5000 but not divisible by 10000.

8. Display customers whose names contain exactly two occurrences of the letter 'a'.

9. Display products whose names have an even number of characters and whose price is greater than 3000.

10. Display employees whose salary is between 40000 and 80000, but whose department location is not Chennai or Mumbai.

## B. Advanced JOIN questions

11. Display every customer with their total order amount, total number of products purchased and total quantity purchased. Include customers who have never ordered.

12. Display employees who have handled orders for customers from at least two different cities.

13. Display products purchased by customers from Chennai, along with customer name, product name and total quantity purchased.

14. Display all departments, their employees and their managers. Include departments without employees.

15. Display customers who purchased products from at least three different product categories.

16. Display employee names, department names, manager names and the total order amount handled by each employee. Include employees without orders.

17. Display each product with the number of distinct customers who purchased it.

18. Display all orders containing more than one product, showing order ID, customer name and number of distinct products.

19. Display pairs of employees working in the same department but reporting to different managers. Avoid duplicate employee pairs.

20. Display customers who purchased products handled by employees from departments located in a different city from the customer's city.

## C. Advanced GROUP BY and HAVING

21. Find departments where the difference between the highest and lowest employee salaries is greater than 30000.

22. Find customers whose average order value is greater than 15000 and who have placed at least two orders.

23. Find product categories where total revenue exceeds 20000 and average product price exceeds 5000.

24. Find employees who have handled orders for at least two customers and whose total handled order value exceeds 30000.

25. Find cities where the total customer credit limit exceeds 100000 and customer count is at least two.

26. Find products whose total quantity sold is greater than the average quantity sold across all products.

27. Find each department's percentage contribution to the total employee salary expenditure.

28. Find customers whose highest order amount is at least twice their lowest order amount.

29. Find employees who handled orders in at least two different months and whose total order value exceeds 20000.

30. Generate a department-wise report containing employee count, total salary, average salary, highest salary, lowest salary and salary range. Display only departments with an average salary above the company-wide average.

---

# Part 2 - 30 Advanced SUBQUERY Questions

(Advanced / Interview level)

## A. Scalar and single-row subqueries - 5 questions

1. Display employees earning more than the average salary of employees working in the IT department.

2. Display products whose price is greater than the average price of products belonging to the same category as the most expensive product.

3. Display customers whose credit limit is greater than the credit limit of the customer who placed the highest-value single order.

4. Display employees earning more than the salary of the employee who joined earliest in the company.

5. Display orders whose total amount is greater than the average order amount of all DELIVERED orders.

## B. IN, NOT IN, ANY and ALL - 5 questions

6. Display employees working in departments where at least one employee earns more than 70000.

7. Display customers who have placed orders handled by employees belonging to department 4.

8. Display products whose prices are greater than ANY product price in the Furniture category.

9. Display products whose prices are greater than ALL product prices in the Accessories category.

10. Display employees whose department IDs do not appear in the Department table. Consider how NULL values affect NOT IN.

## C. Correlated subqueries - 5 questions

11. Display employees whose salary is greater than the average salary of their own department.

12. Display the employee receiving the maximum salary in each department.

13. Display customers whose total spending is greater than the average total spending of customers who have placed orders.

14. Display products whose prices are greater than the average price of products in their own category.

15. Display orders whose total amount is greater than the average order amount for the same customer.

## D. EXISTS and NOT EXISTS - 5 questions

16. Display departments having at least one employee using EXISTS.

17. Display departments that do not have any employees using NOT EXISTS.

18. Display customers who have purchased at least one Electronics product using nested EXISTS.

19. Display customers who have never purchased a product from the Furniture category using NOT EXISTS.

20. Display employees who have handled orders for every customer who has placed an order.

## E. Nested and multi-level subqueries - 5 questions

21. Find employees who earn more than the average salary of employees working in the department with the highest average salary.

22. Find customers who purchased the product with the highest price.

23. Find the department whose total salary expenditure is the highest.

24. Find products purchased by customers whose total spending is greater than the average customer spending.

25. Find employees working in the department that has the maximum number of employees.

## F. Complex correlated and nested subqueries - 5 questions

26. Find the second-highest salary in each department without using window functions or FETCH FIRST.

27. Find customers who have purchased all products in the Electronics category.

28. Find products that have been purchased by every customer who has placed at least one order.

29. Find employees who have handled all orders placed by customers from Chennai.

30. Find customers whose number of distinct purchased products is greater than the number of distinct products purchased by every other customer.

---

# Part 3 - 20 Expert-level subquery challenges

These are intentionally more difficult. Some require multiple levels of nesting or combining correlated subqueries with aggregate functions.

1. Find the employee with the third-highest salary without using ORDER BY FETCH FIRST.

2. Find employees whose salaries are among the top two distinct salaries in their departments.

3. Find customers whose total spending is greater than the total spending of at least 80% of other customers.

4. Find products whose revenue is greater than the average revenue of all products that have been sold.

5. Find the customer who has purchased the maximum number of distinct product categories.

6. Find employees who have handled orders for all customers in their own department's location city.

7. Find departments where every employee earns more than 40000.

8. Find departments where at least one employee earns less than the company's average salary, but the department's average salary is greater than the company's average salary.

9. Find customers who have placed orders in every month in which at least one order was placed.

10. Find products purchased by customers who have never purchased any other product in the same category.

11. Find employees who earn more than all employees reporting to their manager.

12. Find customers whose maximum order amount is greater than the average order amount of all customers.

13. Find products that have never been purchased by customers from Chennai.

14. Find employees who have handled orders for customers who purchased every product in the Accessories category.

15. Find the department with the second-highest average employee salary.

16. Find customers whose total spending is equal to the highest total spending among all customers.

17. Find employees who have handled orders for customers from all cities represented in the Customer table.

18. Find customers who have purchased at least one product from every category.

19. Find products whose total revenue is greater than the total revenue of every product in the Furniture category.

20. Find employees who have handled more than the average number of orders handled by employees who have handled at least one order.

---

# Part 4 - Subquery pattern identification

Before solving the questions, identify the appropriate SQL technique.

| Requirement | Technique |
| --- | --- |
| Compare against one calculated value | Scalar subquery |
| Compare against multiple values | IN |
| Compare against at least one value | ANY |
| Compare against every value | ALL |
| Check whether matching records exist | EXISTS |
| Check whether matching records do not exist | NOT EXISTS |
| Compare each row against its group average | Correlated subquery |
| Find the maximum value per group | Correlated subquery |
| Find records satisfying multiple levels of conditions | Nested subquery |
| Find records matching every record in another set | Double NOT EXISTS |
| Find second/third-highest distinct value | Nested or correlated subquery |
| Calculate an aggregate from another result set | Subquery in FROM |

## Recommended solving order

1. **Level 1 - Advanced SELECT**  
Complete Part 1 questions 1-30.
2. **Level 2 - Basic subqueries**  
Complete Part 2 sections A and B.
3. **Level 3 - Correlated subqueries**  
Complete Part 2 sections C and D.
4. **Level 4 - Nested subqueries**  
Complete Part 2 sections E and F.
5. **Level 5 - Expert challenges**  
Complete all 20 questions in Part 3.

**Important examination practice:** For each question, first identify the output columns, source tables, relationships, filtering conditions and grouping requirements. Then decide whether a JOIN, subquery or both are necessary. Try solving the same problem using JOIN and EXISTS wherever both approaches are valid.

*Note: These questions stay within your requested SQL topics. They do not introduce window functions, CTEs, stored procedures or triggers.*

### User

advanced elect where caluse in where distinct like numeric , character datesubstring conversion to_char to_date aggregate functions dcase sstatement sorting order by joins all join cross self inner right/left outer full outer join group by having set operatins this each 20 question advanced leve

### ChatGPT

# HSQLDB - Advanced SQL Practice Question Bank

**400 advanced SQL questions - 20 questions for each of your 20 requested topics.**

All questions use the same six tables created earlier:

- `Department`
- `Employee`
- `Customer`
- `Product`
- `Orders`
- `Order_Item`

These are problem statements only, not solutions. The difficulty is aimed at SQL developers with approximately 1-2 years of experience and advanced DBMS practical examinations.

---

# 1. Advanced SELECT - 20 Questions

1. Display employee name, department name, salary and annual salary for employees whose annual salary exceeds the average annual salary of all employees.
2. Display customer details along with the total number of orders, total spending and average order value.
3. Display products with their original price, discounted price, stock value and estimated revenue.
4. Display employees with their manager names, department locations and salary differences.
5. Generate an order report containing customer name, employee name, product name, quantity, discount and final item amount.
6. Display each employee's salary as a percentage of the total salary expenditure.
7. Display customers whose total order value is greater than their credit limit.
8. Display products whose stock value exceeds the average stock value of all products.
9. Display each department's employee count and percentage contribution to the total workforce.
10. Display customers who purchased products from at least two distinct categories.
11. Display employees who handled orders worth more than 50% of their department's total salary.
12. Display all orders with customer details and the total number of products in each order.
13. Display the highest-value order for every customer.
14. Display employees with their department's highest and lowest salary.
15. Generate a product report showing category-wise price rank using aggregate comparisons (without window functions).
16. Display customers who have placed orders in at least two different months.
17. Display employees whose salary is greater than the average salary of employees hired in the same year.
18. Display products whose revenue contribution is greater than the average revenue contribution of sold products.
19. Generate a report containing each customer's total spending, highest order, lowest order and average order value.
20. Generate a complete employee performance report showing department, manager, salary, order count, customer count and total handled order value.

# 2. Advanced WHERE Clause - 20 Questions

1. Find employees whose salary is greater than 45000 but less than the average salary of employees in department 1.
2. Find customers whose age is between 25 and 40, credit limit exceeds 50000 and city is not Chennai.
3. Find products whose price is above 5000, stock is below 50 and category is not Furniture.
4. Find orders placed in the first and fourth quarters of 2024, excluding cancelled orders.
5. Find employees hired before 2023 whose salary is greater than 50000 and who report to a manager.
6. Find customers whose city is Chennai or Bangalore but whose credit limit is not between 40000 and 80000.
7. Find employees belonging to departments 1, 3 or 5 whose salaries are not divisible by 10000.
8. Find products whose price multiplied by stock is greater than 200000.
9. Find orders whose amount is above 10000 and whose status is either SHIPPED or DELIVERED.
10. Find employees whose names contain 'a' but do not start with 'a'.
11. Find customers who have a NULL email or a credit limit greater than 70000.
12. Find products whose names contain at least one occurrence of 'o' and whose stock is greater than 20.
13. Find employees whose salary is greater than the average company salary but whose department is not 1.
14. Find orders placed on dates between two specified dates, excluding weekends.
15. Find employees whose hire year is 2022 or 2023 and whose salary exceeds 50000.
16. Find customers whose age is not between 20 and 30 and whose credit limit exceeds 30000.
17. Find products belonging to Electronics or Accessories with price above their category's average price.
18. Find employees who either earn above 70000 or manage at least one employee.
19. Find customers who have placed orders but have not placed any cancelled orders.
20. Find employees whose salary is greater than their manager's salary but below 90000.

# 3. Advanced IN, BETWEEN, NOT IN and NULL filtering - 20 Questions

1. Find employees whose department IDs appear in departments located in Chennai, Bangalore or Mumbai.
2. Find customers whose IDs appear in orders having a total amount greater than 20000.
3. Find products whose IDs appear in order items having quantity greater than 2.
4. Find employees whose department IDs are not present in departments located in Chennai.
5. Find customers who have not placed any orders using NOT IN. Account for NULL values.
6. Find employees whose salaries are between the minimum and maximum salary of department 1.
7. Find orders whose customer IDs belong to customers aged between 25 and 35.
8. Find products whose prices are not between 3000 and 15000.
9. Find employees whose salaries are greater than salaries of employees in department 2 using ANY.
10. Find products whose prices are greater than all product prices in the Furniture category.
11. Find customers whose IDs belong to orders handled by employees earning more than 60000.
12. Find employees whose IDs do not appear as managers of any employee.
13. Find customers who have purchased products from the Electronics category using IN.
14. Find orders whose amounts are between the average and maximum order amount.
15. Find employees whose salaries are equal to any salary earned by employees in department 4.
16. Find products whose prices are greater than every product price in the Accessories category.
17. Find customers whose IDs are not present in orders with CANCELLED status.
18. Find employees belonging to departments whose locations are not among the locations of customers.
19. Find orders whose customer IDs are present in the customers with the highest credit limits.
20. Find products whose IDs are present in orders placed during the first half of 2024 but absent from orders placed during the second half of 2024.

# 4. Advanced DISTINCT - 20 Questions

1. Display all unique customer cities.
2. Display all unique department locations.
3. Display unique combinations of employee department ID and salary.
4. Find the number of distinct employee salaries.
5. Find the number of distinct customers who placed orders.
6. Find the number of distinct products purchased.
7. Display unique product categories purchased by customers from Chennai.
8. Display distinct customer IDs who purchased Electronics products.
9. Find the number of different cities from which customers have placed orders.
10. Display distinct combinations of order status and order year.
11. Find the number of distinct managers in Employee.
12. Find the number of different months in which orders were placed.
13. Display unique combinations of product category and price.
14. Find the number of distinct products purchased by each customer.
15. Find the number of distinct customers handled by each employee.
16. Display unique department and employee name combinations.
17. Find the number of distinct order statuses for each customer.
18. Find the number of unique product categories purchased by every customer.
19. Display distinct combinations of employee location and customer location for handled orders.
20. Find the number of distinct order dates for each customer.

# 5. Advanced LIKE and pattern matching - 20 Questions

1. Find employees whose names start and end with the same character.
2. Find customers whose names contain exactly two occurrences of the letter 'a'.
3. Find employees whose second character is a vowel.
4. Find products whose names contain consecutive repeated characters.
5. Find customers whose names start with a consonant and end with a vowel.
6. Find employees whose names have exactly six characters.
7. Find products whose names contain 'oo' or 'ee'.
8. Find customers whose names contain the letter 'a' but not the letter 'i'.
9. Find employees whose names have 'a' as their third character.
10. Find products whose names start with a letter between A and M.
11. Find employees whose names end in a consonant.
12. Find customers whose names contain at least one repeated letter.
13. Find products whose names contain exactly one occurrence of 'e'.
14. Find employees whose names do not contain vowels.
15. Find customers whose names have the letter 'a' in the second or fourth position.
16. Find product names with exactly seven characters.
17. Find employees whose names start with A, E, I, O or U.
18. Find customers whose names contain 'an' anywhere except at the beginning.
19. Find products whose names have a vowel as their final character.
20. Find employee names that match a specified pattern using `_` and `%` wildcards.

# 6. Advanced Numeric Functions and Expressions - 20 Questions

1. Display employee salaries rounded to the nearest thousand.
2. Display employee salaries truncated to two decimal places.
3. Calculate the difference between each employee's salary and the company average salary.
4. Calculate the percentage of salary increment required to reach 100000.
5. Calculate annual salary, annual bonus and total annual compensation.
6. Display the remainder when each employee's salary is divided by 7000.
7. Calculate the square root of each product's price.
8. Display product prices rounded up and rounded down to the nearest thousand.
9. Calculate total inventory value for each product.
10. Calculate the percentage contribution of each product to the total inventory value.
11. Calculate the average revenue per unit sold for each product.
12. Calculate the final order item price after discount and 18% tax.
13. Calculate the absolute difference between the maximum and minimum salary in each department.
14. Calculate the percentage difference between each customer's credit limit and total spending.
15. Find products whose stock multiplied by price is divisible by 10000.
16. Calculate the ratio between an employee's salary and their manager's salary.
17. Calculate the total salary expense after a 12.5% increment.
18. Calculate the discount amount and net amount for every order item.
19. Display product prices rounded to the nearest multiple of 500.
20. Calculate the percentage of total company salary expenditure represented by each department.

# 7. Advanced Character Functions - 20 Questions

1. Display employee names in uppercase and lowercase together.
2. Extract the first and last three characters of every employee name.
3. Display employee names with their character count and reverse of their names.
4. Extract the portion of each customer email before the `@` symbol.
5. Extract the domain portion of each customer email.
6. Display employee names padded with `*` to a length of 15.
7. Remove leading and trailing spaces from customer names.
8. Concatenate employee name and department ID into one display column.
9. Find the position of the first occurrence of 'a' in every employee name.
10. Display product names after replacing all occurrences of 'o' with '0'.
11. Extract the middle characters of product names.
12. Display customer names with the first character capitalized and the remaining characters lowercase.
13. Display employee names and the number of vowels in each name.
14. Find employees whose names have more consonants than vowels.
15. Display customer names after removing all occurrences of the letter 'a'.
16. Display product names with their first three characters repeated twice.
17. Compare the length of each product name with the length of its category.
18. Extract the first word from a full employee name, assuming names may contain spaces.
19. Display customer names and emails concatenated with a separator.
20. Find employees whose names are palindromes.

# 8. Advanced Date and SUBSTRING - 20 Questions

Use `DATE`, `TO_CHAR`, `TO_DATE`, `EXTRACT` and string functions as supported by your HSQLDB version.

1. Display employee names and joining dates in `DD-MON-YYYY` format.
2. Display order IDs, order dates and month names.
3. Find employees who joined during the first quarter of 2022.
4. Find customers whose orders were placed during November 2024.
5. Extract year, month and day from every order date.
6. Display orders grouped by year and month.
7. Find employees who joined before the earliest order date.
8. Calculate the difference between employee joining dates and a specified date.
9. Find the oldest and newest employee joining dates.
10. Convert a character date in `DD-MM-YYYY` format into a DATE value.
11. Convert a DATE value into `YYYYMMDD` character format.
12. Find employees hired in the same month but different years.
13. Display customer orders placed on the last day of a month.
14. Find orders placed during weekends.
15. Extract the year portion from a formatted date string using SUBSTRING and compare it with 2024.
16. Extract the month portion from a character date and display only November records.
17. Find employees who joined during the same month as the first order placed by the company.
18. Display the number of days between each employee's joining date and a specified date.
19. Display order dates formatted as `Month YYYY` and sort chronologically.
20. Find customers who placed orders during consecutive months.

# 9. Advanced TO_CHAR, TO_DATE and Conversion - 20 Questions

1. Convert employee hire dates into `DD-MM-YYYY` format using TO_CHAR.
2. Convert order dates into `YYYY/MM/DD` format.
3. Display order dates using full month names.
4. Convert a character date `15-11-2024` into a DATE value.
5. Convert a character date `2024/11/15` into a DATE value.
6. Convert character values representing numeric salaries into DECIMAL.
7. Convert numeric employee IDs into character strings.
8. Convert character values into INTEGER and calculate their sum.
9. Display the current date in a specified format using TO_CHAR.
10. Convert dates represented in `DD-MON-YYYY` format into DATE.
11. Convert product prices into formatted character values with two decimal places.
12. Display salary values with thousands separators using an appropriate format model.
13. Convert order dates into character values and extract the year using SUBSTRING.
14. Compare dates after converting character date values into DATE.
15. Convert customer age from a character representation into INTEGER and filter ages above 30.
16. Convert a character amount into DECIMAL and calculate a 10% tax.
17. Display date values in `YYYY-MM` format and group by the formatted month.
18. Find records whose character date represents a valid date in the required format.
19. Convert a character value containing a year and month into a DATE using appropriate parsing.
20. Generate a report with formatted date, formatted salary and formatted total order amount.

# 10. Advanced Aggregate Functions - 20 Questions

1. Find the second-highest employee salary using aggregate functions.
2. Find the average salary of employees excluding the highest and lowest salaries.
3. Find the total salary paid to employees in each department.
4. Find the department with the highest total salary.
5. Find the average order amount per customer.
6. Find customers with the highest total spending.
7. Find the number of distinct products purchased by each customer.
8. Find the total quantity sold for each product category.
9. Find the average discount percentage for each product.
10. Find products with the highest total revenue.
11. Find the difference between maximum and minimum order amounts for each customer.
12. Find the number of orders handled by each employee, including employees without orders.
13. Find departments with more employees than the average department employee count.
14. Calculate total revenue, average revenue, maximum revenue and minimum revenue for each category.
15. Find customers whose total order amount exceeds the average customer spending.
16. Find the number of employees hired in each year.
17. Find the average employee salary by department and joining year.
18. Calculate delivered order revenue and cancelled order value separately using conditional aggregation.
19. Find the product category contributing the largest percentage of total revenue.
20. Calculate the number of orders, total sales and average order value for each month.

---

# 11. Advanced CASE Statements - 20 Questions

1. Classify employees into five salary grades based on salary ranges.
2. Calculate employee bonus using different percentages for each department.
3. Classify customers based on their total spending.
4. Classify products based on price and available stock simultaneously.
5. Display order status using custom descriptions for all possible status values.
6. Calculate employee tax based on salary slabs.
7. Display employees as Manager, Senior Employee or Junior Employee based on their role and salary.
8. Classify customers as High Risk, Medium Risk or Low Risk based on credit limit and total spending.
9. Calculate product discounts based on category and price.
10. Classify orders as Small, Medium, Large or Premium based on order amount.
11. Use CASE inside SUM to calculate revenue separately for each order status.
12. Use CASE inside COUNT to calculate employee counts by salary category.
13. Display employee joining status based on the year of joining.
14. Display product availability based on stock and price.
15. Classify customers based on their number of orders.
16. Calculate different bonuses for employees depending on whether they have handled more than one order.
17. Calculate delivered, pending, shipped and cancelled order counts in a single grouped report.
18. Generate a department report with separate columns for high-, medium- and low-salary employee counts.
19. Calculate total sales separately for Electronics, Furniture and Accessories using conditional aggregation.
20. Display customer loyalty classification based on number of orders and total spending.

---

# 12. Advanced ORDER BY and Sorting - 20 Questions

1. Sort employees by department, then salary descending, then hire date ascending.
2. Sort customers by total spending, with customers having no orders at the end.
3. Sort products by category, price and stock.
4. Display the top five highest-paid employees using FETCH FIRST.
5. Display the three most expensive products from each category using correlated subqueries.
6. Sort orders by year, month and day.
7. Sort employees by salary grade using CASE expressions.
8. Sort departments by employee count, including departments with zero employees.
9. Sort customers by city and then total order value descending.
10. Sort products by revenue contribution rather than individual price.
11. Display the five most recent orders.
12. Sort employees by manager name and employee name.
13. Sort customer records by the number of distinct categories purchased.
14. Sort order statuses in the custom order DELIVERED, SHIPPED, PENDING and CANCELLED.
15. Sort products by the difference between price and category average price.
16. Sort departments by average salary and then maximum salary.
17. Sort employees with NULL manager IDs last.
18. Display the highest revenue-generating products first and products never ordered last.
19. Sort customers by total spending and then customer age.
20. Display the top three customers in each city based on total order amount using correlated subqueries.

---

# 13. INNER JOIN - 20 Questions

1. Display employees and their department names.
2. Display customers and their order details.
3. Display orders with customer names and employee names.
4. Display products and their order item details.
5. Display employee names, department names and department locations.
6. Display customers who purchased Electronics products.
7. Display products purchased by customers from Chennai.
8. Display employees who handled orders worth more than 20000.
9. Display customer names and their total purchased quantity.
10. Display products and their total quantity sold.
11. Display order ID, customer name, product name and order date.
12. Display employees who handled orders for customers from their own city, where city and department location match.
13. Display customer names and the total revenue generated by their purchases.
14. Display employees and the distinct number of customers they handled.
15. Display all order items with product category and customer city.
16. Display customers who purchased more than one product category.
17. Display employees who handled orders in November.
18. Display products that were purchased in at least two different orders.
19. Display department-wise sales handled by employees.
20. Generate a five-table sales report with customer, employee, department, product and order details.

# 14. LEFT OUTER JOIN - 20 Questions

1. Display all customers, including those who have never placed orders.
2. Display all departments, including those without employees.
3. Display all products, including products never ordered.
4. Display all employees, including employees without a department.
5. Display all employees and their managers, including employees without managers.
6. Display all customers with their delivered orders, retaining customers without delivered orders.
7. Display all employees and the total value of orders they handled, including employees with zero orders.
8. Display all products and their total sales quantity, including unsold products.
9. Display all departments with employee count and average salary, including empty departments.
10. Display all customers with the number of distinct products they purchased, including customers with zero purchases.
11. Display all products with revenue and inventory value.
12. Display all employees with the number of customers they handled.
13. Display all customers and the date of their latest order, including customers without orders.
14. Display all departments and their highest-paid employee.
15. Display all employees and their total order amount, with zero displayed for employees without orders.
16. Display all products and the number of different customers who purchased them.
17. Display all customers and separate counts for delivered, pending and cancelled orders.
18. Display all employees with their department names and manager names, including unmatched records.
19. Display all categories and their total sales, including categories with no sold products.
20. Generate a complete customer report with customer information, order information and product information, retaining customers without purchases.

---

# 15. RIGHT OUTER JOIN - 20 Questions

1. Display all departments and their employees using RIGHT JOIN.
2. Display all products and their order items using RIGHT JOIN.
3. Display all customers and their orders using RIGHT JOIN.
4. Display all employees and their departments using RIGHT JOIN.
5. Display all orders and their customers, including unmatched orders.
6. Display all order items and their products, including unmatched products.
7. Display all departments with employee counts, including empty departments.
8. Display all products with total quantities sold, including unsold products.
9. Display all customers with their order totals.
10. Display all employees with their handled order counts.
11. Display all department locations with their employees.
12. Display all products and the customers who purchased them.
13. Display all orders with employee details, including orders without assigned employees.
14. Display all customers and their delivered orders.
15. Display all departments with their average employee salary.
16. Display all products with the total revenue generated.
17. Display all employees with their managers, retaining employees without managers.
18. Display all order items with order and product information.
19. Display all products and the number of different orders in which they appear.
20. Generate a complete report of all products, including products with no matching order item records.

---

# 16. FULL OUTER JOIN - 20 Questions

1. Display all employees and departments, including unmatched records from both sides.
2. Display all customers and orders, including customers without orders and orders without customers.
3. Display all products and order items, retaining unmatched records.
4. Display all employees and managers using a self-referencing FULL OUTER JOIN.
5. Display all customers and employees, matching their city and department location.
6. Display all departments and employees with unmatched departments and employees included.
7. Display all products and their sales records, including products never sold.
8. Display all customers and their order statuses, including customers without orders.
9. Display all departments and their salary expenditure.
10. Display all employees and orders they handled.
11. Display all products and customer purchases.
12. Display all customers and products purchased, including unmatched records.
13. Display all departments and product categories by matching location and category name where applicable.
14. Display employees and customers with matching names, retaining unmatched records.
15. Display customer cities and department locations, including locations appearing in only one table.
16. Display all employees and departments with an indicator showing whether a match exists.
17. Display all customers and orders, showing a CASE-based classification for matched and unmatched records.
18. Display all products and order items, identifying products never ordered.
19. Display all employee and order combinations based on employee ID and assigned order employee ID.
20. Generate a reconciliation report showing all matching and unmatched customer-order records.

---

# 17. CROSS JOIN - 20 Questions

1. Generate every possible combination of employees and departments.
2. Generate every possible combination of customers and products.
3. Generate every possible combination of products and department locations.
4. Generate all possible combinations of employees and product categories.
5. Generate every possible combination of customers and order statuses.
6. Generate all possible combinations of employees and salary grades.
7. Generate all possible combinations of product categories and customer cities.
8. Generate every combination of department names and product names.
9. Generate all combinations of employees and customers.
10. Generate every combination of customers and department locations.
11. Generate all possible combinations of products and order statuses.
12. Generate every combination of employees and months from a predefined set of months.
13. Generate all combinations of customers and product categories, then identify which combinations have purchases.
14. Generate every combination of departments and order statuses.
15. Generate all combinations of products and customers, displaying a hypothetical 10% discount price for each combination.
16. Generate every combination of employee salary categories and departments.
17. Generate all possible combinations of customer cities and product categories.
18. Generate every possible employee and manager pair, excluding the same employee.
19. Generate a hypothetical price comparison for all product pairs.
20. Generate all possible combinations of product categories and order statuses, including combinations with zero matching sales.

---

# 18. SELF JOIN - 20 Questions

1. Display employee names alongside their manager names.
2. Find employees earning more than their managers.
3. Find employees earning less than their managers.
4. Display employees who report to the same manager.
5. Find managers who supervise more than one employee.
6. Find employees who joined before their managers.
7. Find employees who joined after their managers.
8. Find employees who earn the same salary as another employee in the same department.
9. Find employees who have the same salary but work in different departments.
10. Find pairs of employees who work in the same department but have different managers.
11. Find employees whose salaries differ by less than 10000 from another employee in their department.
12. Find pairs of employees who joined in the same year.
13. Find employees whose salary is greater than every other employee reporting to the same manager.
14. Find employees who have the same manager and joined in different years.
15. Find employees who report directly to employees who themselves manage other employees.
16. Display manager names, employee names and the number of employees reporting to each manager.
17. Find employees whose hire dates are later than all employees reporting to the same manager.
18. Find pairs of employees with salaries differing by exactly 10000.
19. Find employees whose department is the same as their manager's department.
20. Display the complete employee-manager hierarchy for the available levels in the dataset.

---

# 19. GROUP BY and HAVING - 20 Questions

1. Find departments with an average salary greater than the company-wide average salary.
2. Find customers who have placed more than two orders.
3. Find products with total revenue greater than 20000.
4. Find cities having more than three customers.
5. Find departments whose salary expenditure exceeds 150000.
6. Find employees who have handled orders for more than two distinct customers.
7. Find customers whose average order amount is greater than 15000.
8. Find categories whose average product price is greater than 10000.
9. Find products purchased in at least three different orders.
10. Find departments where the maximum salary exceeds 70000 and minimum salary is below 50000.
11. Find customers whose total delivered order amount exceeds 30000.
12. Find employees who handled orders in at least two different months.
13. Find product categories with total stock value exceeding 100000.
14. Find cities whose total credit limit exceeds 150000.
15. Find departments having at least two employees and an average salary greater than 50000.
16. Find customers who have purchased more than two distinct product categories.
17. Find employees whose total handled order amount is greater than the average order amount.
18. Find order statuses whose average order amount exceeds 10000.
19. Find customers whose highest order amount is at least twice their lowest order amount.
20. Generate a monthly report showing total orders, average order amount, maximum amount and minimum amount. Display only months having more than one order.

---

# 20. SET OPERATIONS - 20 Questions

Use `UNION`, `UNION ALL`, `INTERSECT` and `EXCEPT` (or `MINUS` if required by your HSQLDB version).

1. Display all unique cities appearing in Customer and Department.
2. Display all cities appearing in Customer and Department, preserving duplicates.
3. Find cities common to Customer and Department.
4. Find customer cities that do not appear in Department locations.
5. Find department locations that do not appear in Customer cities.
6. Combine employee names and customer names into one result.
7. Combine employee IDs and customer IDs using UNION ALL.
8. Find IDs common to Employee and Customer.
9. Find employee IDs that do not appear in Customer.
10. Find customer IDs that do not appear in Employee.
11. Combine product names and department names into a single result.
12. Display unique employee names and customer names in uppercase using UNION.
13. Find common numeric values between employee salaries and product prices.
14. Find locations appearing in Customer, Department and Employee-related department records.
15. Display all distinct order statuses and department locations in one result, after converting them into compatible character columns.
16. Find product IDs appearing in two separately defined order-date ranges.
17. Find products purchased during the first half of 2024 but not during the second half.
18. Combine customer cities and employee department locations using UNION ALL, then compare the number of occurrences of each location.
19. Find customers who appear in two separately constructed customer lists based on age and credit limit.
20. Construct three result sets representing high-, medium- and low-salary employees, then combine them using UNION ALL while displaying a salary classification.

---

## Practice completion tracker



1. `NOT IN` can produce unexpected results when its subquery returns NULL.
2. `WHERE` filters rows before grouping; `HAVING` filters groups after aggregation.
3. Every non-aggregated column in a grouped SELECT generally needs to appear in GROUP BY.
4. `COUNT(*)` counts rows, while `COUNT(column)` ignores NULL values.
5. `COUNT(DISTINCT column)` counts unique non-NULL values.
6. LEFT JOIN conditions on the right-hand table placed in WHERE can unintentionally eliminate unmatched rows.
7. CROSS JOIN produces a Cartesian product.
8. SELF JOIN requires table aliases.
9. UNION removes duplicates; UNION ALL preserves them.
10. INTERSECT returns common rows.
11. EXCEPT/MINUS returns rows in the first result that are absent from the second.
12. Set-operation queries must have compatible column counts and datatypes.
13. `TO_CHAR` and `TO_DATE` format models can differ between HSQLDB versions and Oracle-style syntax.
14. For top-N queries, use `FETCH FIRST n ROWS ONLY` rather than MySQL's LIMIT syntax.

**My recommendation:** Complete these 400 questions using your existing dataset without changing the table relationships. This will give you extensive practice across filtering, expressions, aggregation, all major joins and set operations.
