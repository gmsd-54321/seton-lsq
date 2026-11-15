> https://chatgpt.com/c/6af00783-b140-83ee-a13b-1e83c3ef38b7

# SQL HSQLDB Advanced Preparation

### User

for 2 year sql developer hsql database level give concepts needed from required topics all tricky advanced topics from these explanation and 15 question quiz at end all edge cases and all what is sql types of hsql command hsql datatypes char varchar storage characterstics use example sql numeric datatypes integer numeric(p,s) maximum bit they can hold default bit precision example if scale not provided it stores integral values all allowed values for numeric how to know if it is correct or not, date, time, timestamp, clob(character large object), blob(binary large object) how much data it suppotts, Boolean what does it store, varchar datastorage with trailing space and length greater than > length declared remoces trailing spaces, 8 length string without trailing space given varchar(6) returns error, 3 length given to string char(6) stores with trailing spaces, cast('grammar' as char(4)) char(6) stored as 'gram  ' cast('smile' as char(3) in varchar(6) stored as 'smi' cast('we' as char(4) in varchar(6) first it is convert to char(4) 'smi ' and then stored the same in varchar(6) wind varchar(6) cannot be stored in char(3), integer sorage if decimal given it rounds to nearest neighbour give examples then numeric(2) cannot store 134, 23.6 at numeric(2) round to 24 since cannot have decimal values 23.4 to 23, 23.5 to 23, give examples to learn numeric(p,s) type conversion easily for all edge cases give date to char conversion char to date conversion each type integer to varchar conversion varchar to integer conversion integer to numeric conversion numeric to integer conversion all functions example give , hsql operators arithmetic, relational, logical arithmetic +,-,*,/ when decimal value added or subtracted resulting scalre higher value scale of term,multiplied sum of scale of terms, division and average higher scale of value of terms involved, in course it is either 5 or higher scale value of terms what is maximum chosen, comparison operators -=,>,>=,<,<=, logical and or not special between, in (list of values), like, is null, is not null

### ChatGPT

# HSQLDB - Advanced SQL Developer Guide (2 Years Experience)

This guide covers SQL fundamentals, HSQLDB data types, storage characteristics, type conversions, numeric precision and scale, operators, edge cases, and tricky interview/examination scenarios.

The target level is **2-year SQL Developer**, so we will go beyond syntax and cover:

- What happens internally when values are inserted or converted.
- Why certain queries generate errors.
- How precision and scale affect calculations.
- Differences between `CHAR`, `VARCHAR`, `INTEGER`, and `NUMERIC`.
- Implicit versus explicit type conversion.
- Boundary conditions and unexpected SQL results.

# 1. What is SQL?

**SQL (Structured Query Language)** is a language used to communicate with relational database management systems (RDBMS).

It allows us to:

1. Create databases and tables.
2. Insert, update and delete records.
3. Retrieve and filter data.
4. Perform calculations and aggregations.
5. Control transactions.
6. Manage database permissions.
7. Define relationships and constraints.

Example:

```sql
SELECT employee_name, salary
FROM employee
WHERE salary > 50000;
```

SQL is declarative: you specify *what result you want*, while the database determines how to retrieve it.

## 1.1 What is HSQLDB?

**HSQLDB (HyperSQL Database)** is a relational database management system written in Java.

Its characteristics include:

- Supports SQL and relational database operations.
- Can run in-memory or in file-based mode.
- Supports JDBC connectivity.
- Supports transactions.
- Supports primary keys, foreign keys, constraints, views, indexes and stored routines.
- Supports SQL data types and standard SQL expressions.

Example JDBC URL:

```text
jdbc:hsqldb:mem:testdb
```

This creates an in-memory database.

```text
jdbc:hsqldb:file:mydb
```

This uses a file-based database.

# 2. Types of SQL Commands

SQL commands are commonly divided into five categories.

| Category | Full form | Purpose |
| --- | --- | --- |
| DDL | Data Definition Language | Defines database structures |
| DML | Data Manipulation Language | Modifies table data |
| DQL | Data Query Language | Retrieves data |
| DCL | Data Control Language | Controls permissions |
| TCL | Transaction Control Language | Controls transactions |

## 2.1 DDL - Data Definition Language

Used to create or modify database objects.

| Command | Purpose |
| --- | --- |
| `CREATE` | Create a table, schema, view, etc. |
| `ALTER` | Modify an existing object |
| `DROP` | Delete an object |
| `TRUNCATE` | Remove all rows from a table |
| `COMMENT` | Add descriptive metadata |

Examples:

```sql
CREATE TABLE employee (
    emp_id INTEGER,
    emp_name VARCHAR(50)
);
```

```sql
ALTER TABLE employee
ADD salary NUMERIC(10,2);
```

```sql
DROP TABLE employee;
```

**Important distinction:**

- `DELETE` removes rows and supports a `WHERE` condition.
- `TRUNCATE` removes all rows without selecting individual rows.
- `DROP` removes the database object itself.

## 2.2 DML - Data Manipulation Language

| Command | Purpose |
| --- | --- |
| `INSERT` | Add records |
| `UPDATE` | Modify records |
| `DELETE` | Remove records |
| `MERGE` | Perform conditional insert/update operations |

```sql
INSERT INTO employee
VALUES (101, 'Arun', 45000);
```

```sql
UPDATE employee
SET salary = 50000
WHERE emp_id = 101;
```

```sql
DELETE FROM employee
WHERE emp_id = 101;
```

## 2.3 DQL - Data Query Language

Primarily uses `SELECT`.

```sql
SELECT *
FROM employee;
```

Other important clauses:

- `WHERE`
- `GROUP BY`
- `HAVING`
- `ORDER BY`
- `DISTINCT`
- `JOIN`
- `UNION`
- `INTERSECT`
- `EXCEPT`

## 2.4 DCL - Data Control Language

| Command | Purpose |
| --- | --- |
| `GRANT` | Give privileges |
| `REVOKE` | Remove privileges |

```sql
GRANT SELECT ON employee TO analyst;
```

```sql
REVOKE SELECT ON employee FROM analyst;
```

## 2.5 TCL - Transaction Control Language

| Command | Purpose |
| --- | --- |
| `COMMIT` | Permanently commit a transaction |
| `ROLLBACK` | Undo uncommitted changes |
| `SAVEPOINT` | Establish a rollback point |

Example:

```sql
START TRANSACTION;

UPDATE employee
SET salary = 60000
WHERE emp_id = 101;

SAVEPOINT sp1;

UPDATE employee
SET salary = 70000
WHERE emp_id = 102;

ROLLBACK TO SAVEPOINT sp1;

COMMIT;
```

The first update is committed; the second update is rolled back.

**Developer-level distinction:** DDL transaction behaviour can depend on the database implementation and command. Do not assume every DDL statement can be rolled back like ordinary DML.

# 3. HSQLDB Data Types - Complete Classification

A data type determines:

- What kind of value a column can store.
- The range of permitted values.
- How much precision is retained.
- How values are compared and converted.
- What happens when an invalid value is inserted.

## 3.1 Numeric data types

HSQLDB supports the following important numeric types.

| Data type | Storage precision | Value range / characteristics |
| --- | --- | --- |
| TINYINT | 8 bits | -128 to 127 |
| SMALLINT | 16 bits | -32,768 to 32,767 |
| INTEGER | 32 bits | -2,147,483,648 to 2,147,483,647 |
| BIGINT | 64 bits | Signed 64-bit integer |
| NUMERIC(p,s) | Decimal precision | Exact decimal |
| DECIMAL(p,s) | Decimal precision | Exact decimal |
| REAL | 32-bit floating point | Approximate |
| DOUBLE | 64-bit floating point | Approximate |

`INT` is a synonym for `INTEGER`. `DEC` is a synonym for `DECIMAL`.

**Important distinction:**

- `INTEGER` stores whole numbers.
- `NUMERIC` and `DECIMAL` store exact decimal numbers within their declared precision and scale.
- `REAL` and `DOUBLE` store approximate floating-point values.

For financial calculations, prefer `DECIMAL` or `NUMERIC` instead of `DOUBLE`.

### 3.2 Understanding NUMERIC(p,s)

This is one of the most important concepts for SQL developers.

Syntax:

```sql
NUMERIC(precision, scale)
```

Where:

- `p` = total number of digits.
- `s` = number of digits after the decimal point.
- `p - s` = maximum number of digits before the decimal point.

For example:

```sql
salary NUMERIC(8,2)
```

It allows:

- 6 digits before the decimal.
- 2 digits after the decimal.
- 8 digits in total.

**NUMERIC(8,2) digit allocation**

# .

6 integral digits 2 fractional digits

# 999999.99

Maximum positive value for NUMERIC(8,2)

The maximum positive value is:

$$
10^{p-s}-10^{-s}
$$

The minimum negative value is its negative equivalent.

For `NUMERIC(8,2)`:

```text
999999.99     Valid
-999999.99    Valid
1000000.00    Invalid
12345.67      Valid
123456.78     Valid
1234567.89    Invalid
```

### 3.3 What happens when scale is not specified?

Consider:

```sql
CREATE TABLE test_num (
    a NUMERIC(5),
    b NUMERIC(5,0),
    c NUMERIC(5,2)
);
```

Here:

| Declaration | Effective precision | Effective scale |
| --- | --- | --- |
| NUMERIC(5) | 5 | 0 |
| NUMERIC(5,0) | 5 | 0 |
| NUMERIC(5,2) | 5 | 2 |

Therefore:

```sql
INSERT INTO test_num(a)
VALUES (12345);
```

Valid.

```sql
INSERT INTO test_num(a)
VALUES (12345.67);
```

The fractional portion must be converted to scale zero. It is not simply an automatic rejection.

**Remember:** In HSQLDB, the default scale of NUMERIC/DECIMAL is zero.

### 3.4 All possible scale combinations

For a precision of 5:

| Declaration | Integral digits | Decimal digits | Maximum positive value |
| --- | --- | --- | --- |
| NUMERIC(5,0) | 5 | 0 | 99999 |
| NUMERIC(5,1) | 4 | 1 | 9999.9 |
| NUMERIC(5,2) | 3 | 2 | 999.99 |
| NUMERIC(5,3) | 2 | 3 | 99.999 |
| NUMERIC(5,4) | 1 | 4 | 9.9999 |
| NUMERIC(5,5) | 0 | 5 | 0.99999 |

In standard declarations, precision must be positive and scale cannot exceed precision.

**How to determine whether a value fits:**

Take `NUMERIC(p,s)` and count the integral digits after applying the conversion to the declared scale.

For example:

```text
NUMERIC(5,2)

123.45       Valid
999.99       Valid
1000.00      Invalid
12.345       Converted to scale 2
12345.00     Invalid
0.123        Converted to scale 2
```

The important point is that fractional digits can be rounded, but the integral part must fit.

### 3.5 Numeric rounding and truncation

This is a frequent source of mistakes.

HSQLDB allows fractional digits to be lost during numeric conversion. This can involve rounding, rather than simply deleting everything after the decimal point.

For example, when converting to an integer-scale numeric type, the following are useful expected examples:

| Original value | NUMERIC(3,0) |
| --- | --- |
| 23.1 | 23 |
| 23.4 | 23 |
| 23.5 | 24 |
| 23.6 | 24 |
| 23.9 | 24 |
| -23.4 | -23 |
| -23.5 | -24 |
| -23.6 | -24 |

Do not confuse numeric conversion with the `FLOOR()` function.

```sql
SELECT
    FLOOR(23.9),
    CEILING(23.1),
    ROUND(23.6),
    TRUNC(23.9);
```

These are different operations:

- `FLOOR()` moves towards negative infinity.
- `CEILING()` moves towards positive infinity.
- `ROUND()` rounds to a specified number of decimal places.
- `TRUNC()` removes fractional digits without rounding.

### 3.6 Numeric edge cases

Consider `NUMERIC(2,0)`.

| Input | Result |
| --- | --- |
| 99 | Valid |
| 100 | Error |
| -99 | Valid |
| -100 | Error |
| 9.4 | 9 |
| 9.5 | 10 |
| 99.4 | 99 |
| 99.5 | Error after rounding to 100 |
| 134 | Error |

Why is `99.5` interesting?

Because its rounded result is `100`, which requires three integral digits. The declared type permits only two.

This is a critical distinction between the original input and the final converted value.

---

# 4. Character Data Types - CHAR, VARCHAR and CLOB

These three types are particularly important for real-world SQL development.

## 4.1 CHAR(n) - Fixed-length character storage

Syntax:

```sql
CHAR(6)
```

`CHAR` is a fixed-length character type.

If you insert a string shorter than the declared length, HSQLDB pads it with trailing spaces.

Example:

```sql
CREATE TABLE char_test (
    name CHAR(6)
);

INSERT INTO char_test
VALUES ('ABC');
```

Conceptually, the stored value is:

```text
'ABC   '
```

There are three trailing spaces.

**CHAR(6) example**

␠ represents a trailing space added by the database.

What if you insert a string longer than the declared length?

```sql
INSERT INTO char_test
VALUES ('ABCDEFG');
```

This is not automatically accepted.

HSQLDB permits truncation on assignment to `CHAR` when all characters beyond the declared length are spaces.

Example:

```sql
INSERT INTO char_test
VALUES ('ABCDEF   ');
```

The extra trailing spaces can be discarded.

But:

```sql
INSERT INTO char_test
VALUES ('ABCDEFG');
```

Produces a data exception because the extra character is not a space.

## 4.2 VARCHAR(n) - Variable-length character storage

Syntax:

```sql
VARCHAR(6)
```

Unlike CHAR, VARCHAR does not pad shorter values with spaces.

Example:

```sql
CREATE TABLE varchar_test (
    name VARCHAR(6)
);

INSERT INTO varchar_test
VALUES ('ABC');
```

The value remains:

```text
'ABC'
```

It is not padded to six characters.

| Input | VARCHAR(6) |
| --- | --- |
| `'A'` | Valid |
| `'ABC'` | Valid |
| `'ABCDEF'` | Valid |
| `'ABCDEFG'` | Error |
| `'ABC   '` | Valid, if total length is within limit |

**Storage characteristic:** The actual stored string length determines its data size. Declaring `VARCHAR(1000)` does not mean every row reserves 1000 characters.

## 4.3 CHAR versus VARCHAR

| Feature | CHAR(6) | VARCHAR(6) |
| --- | --- | --- |
| Length | Fixed | Variable |
| Shorter input | Padded | Not padded |
| Longer input | Only excess spaces may be discarded | Excess spaces may be discarded; non-space excess causes error |
| Storage | Fixed-width character value | Variable-length value |
| Suitable for | Fixed-format codes | Names, emails, addresses |

## 4.4 Important VARCHAR and CHAR edge cases

Let's understand the examples you mentioned.

**Case 1: VARCHAR(6), input of eight non-space characters**

```sql
INSERT INTO varchar_test
VALUES ('ABCDEFGH');
```

(Error)

The value exceeds the declared length and contains non-space characters beyond the limit.

**Case 2: CHAR(6), input of three characters**

```sql
INSERT INTO char_test
VALUES ('ABC');
```

(Valid)

Stored as:

```text
'ABC   '
```

**Case 3: Explicit CAST to CHAR(4)**

```sql
SELECT CAST('grammar' AS CHAR(4))
FROM (VALUES(0)) AS t(x);
```

Result:

```text
'gram'
```

The remaining characters are truncated.

**Case 4: Explicit CAST to CHAR(6)**

```sql
SELECT CAST('ABC' AS CHAR(6))
FROM (VALUES(0)) AS t(x);
```

Result:

```text
'ABC   '
```

**Case 5: CAST to VARCHAR(6)**

```sql
SELECT CAST('smile' AS VARCHAR(6))
FROM (VALUES(0)) AS t(x);
```

Result:

```text
'smile'
```

**Case 6: CHAR to VARCHAR conversion**

```sql
SELECT CAST(
    CAST('we' AS CHAR(4))
    AS VARCHAR(6)
)
FROM (VALUES(0)) AS t(x);
```

Conceptual result:

```text
'we  '
```

Why?

1. `'we'` is converted to `CHAR(4)`.
2. Two spaces are appended.
3. The resulting four-character value is converted to `VARCHAR(6)`.
4. VARCHAR does not automatically remove the spaces already present in the input.

**Case 7: VARCHAR(6) to CHAR(3)**

```sql
SELECT CAST('winter' AS CHAR(3))
FROM (VALUES(0)) AS t(x);
```

(Valid explicit CAST)

Result:

```text
'win'
```

An explicit CAST can truncate a string.

However, inserting a six-character non-space string directly into a `CHAR(3)` column fails.

**Important distinction:** Explicit CAST truncation and implicit assignment conversion are not identical operations.

These rules are documented in HyperSQL's type conversion guide.

## 4.5 Trailing spaces and LENGTH()

Trailing spaces are a common interview trap.

```sql
SELECT LENGTH('ABC');
```

Returns:

```text
3
```

Compare:

```sql
SELECT LENGTH('ABC   ');
```

The literal contains six characters, so its length is six.

Do not assume that VARCHAR automatically removes trailing spaces.

Also, character comparison can use padding semantics. Two values that look different in terms of trailing spaces may compare equal.

```sql
SELECT
    CASE
        WHEN 'ABC' = 'ABC   ' THEN 'EQUAL'
        ELSE 'NOT EQUAL'
    END
FROM (VALUES(0)) AS t(x);
```

In HyperSQL character comparison, trailing padding spaces are generally insignificant.

For exact storage and comparison investigations, use `LENGTH()`, `OCTET_LENGTH()` where applicable, and explicit casts.

## 4.6 CLOB - Character Large Object

CLOB stands for Character Large Object.

Used for large text content.

Examples:

- Books.
- Long descriptions.
- Documents.
- Large text logs.
- Article content.

Syntax:

```sql
CREATE TABLE documents (
    document_id INTEGER,
    content CLOB
);
```

You can specify a size:

```sql
content CLOB(10M)
```

This represents a maximum length of approximately 10 MiB in the declared character-length units.

Without an explicit length, HyperSQL uses an implementation-defined default of 1 GB for CLOB.

**CHAR versus VARCHAR versus CLOB:**

- CHAR: Fixed-length text.
- VARCHAR: Variable-length text.
- CLOB: Large variable-length text.

---

# 5. BLOB - Binary Large Object

BLOB stands for Binary Large Object.

It stores binary data instead of ordinary character strings.

Examples:

- Images.
- PDFs.
- Audio.
- Videos.
- Binary files.

Syntax:

```sql
CREATE TABLE file_storage (
    file_id INTEGER,
    file_data BLOB
);
```

You can specify a size:

```sql
file_data BLOB(20M)
```

Without a specified length, HyperSQL uses an implementation-defined default of 1 GB.

| Type | Data |
| --- | --- |
| CHAR | Fixed-length text |
| VARCHAR | Variable-length text |
| CLOB | Large text |
| BINARY | Fixed-length binary |
| VARBINARY | Variable-length binary |
| BLOB | Large binary |

**Important:** CLOB and BLOB are not interchangeable.

A CLOB is character-oriented, whereas a BLOB is binary-oriented.

# 6. DATE, TIME and TIMESTAMP

These three types are frequently confused.

## 6.1 DATE

Stores a calendar date.

```sql
CREATE TABLE date_test (
    joining_date DATE
);
```

Insertion:

```sql
INSERT INTO date_test
VALUES (DATE '2026-11-08');
```

Format:

```text
YYYY-MM-DD
```

It stores:

- Year
- Month
- Day

It does not store hours, minutes or seconds.

## 6.2 TIME

Stores the time of day.

```sql
CREATE TABLE time_test (
    login_time TIME
);
```

Insertion:

```sql
INSERT INTO time_test
VALUES (TIME '10:30:45');
```

Stores:

- Hour
- Minute
- Second
- Optional fractional seconds

Example:

```sql
TIME(3)
```

Supports three fractional-second digits.

```text
10:30:45.123
```

## 6.3 TIMESTAMP

Stores both date and time.

```sql
CREATE TABLE timestamp_test (
    created_at TIMESTAMP
);
```

Insertion:

```sql
INSERT INTO timestamp_test
VALUES (TIMESTAMP '2026-11-08 10:30:45.123456');
```

The default fractional-second precision for HSQLDB TIMESTAMP is 6. TIME defaults to 0. Both can be declared with fractional precision from 0 to 9.

| Type | Example | Information |
| --- | --- | --- |
| DATE | 2026-11-08 | Date |
| TIME | 10:30:45 | Time |
| TIMESTAMP | 2026-11-08 10:30:45 | Date and time |

## 6.4 Extracting date components

```sql
SELECT
    EXTRACT(YEAR FROM joining_date),
    EXTRACT(MONTH FROM joining_date),
    EXTRACT(DAY FROM joining_date)
FROM employee;
```

Month name:

```sql
SELECT MONTHNAME(joining_date)
FROM employee;
```

Other useful functions:

```sql
SELECT
    YEAR(joining_date),
    MONTH(joining_date),
    DAYOFMONTH(joining_date)
FROM employee;
```

## 6.5 BOOLEAN

BOOLEAN represents logical values.

It supports three logical states:

| Value | Meaning |
| --- | --- |
| TRUE | Condition is true |
| FALSE | Condition is false |
| UNKNOWN | Usually represents NULL in a logical expression |

Example:

```sql
CREATE TABLE employee_status (
    emp_id INTEGER,
    is_active BOOLEAN
);
```

```sql
INSERT INTO employee_status
VALUES
(1, TRUE),
(2, FALSE),
(3, NULL);
```

Query:

```sql
SELECT *
FROM employee_status
WHERE is_active = TRUE;
```

Returns only employee 1.

Important distinction:

- `FALSE` is a known Boolean value.
- `NULL` means the value is unknown or missing.
- `NULL` is not the same as `FALSE`.

# 7. Type Conversion - CAST and Implicit Conversion

Type conversion means changing a value from one data type to another.

There are two types:

1. Explicit conversion - Developer specifies the conversion.
2. Implicit conversion - Database automatically converts compatible types.

## 7.1 CAST syntax

```sql
CAST(expression AS target_data_type)
```

Example:

```sql
SELECT CAST(123 AS VARCHAR(10))
FROM (VALUES(0)) AS t(x);
```

Result:

```text
'123'
```

## 7.2 Conversion compatibility table

| From | To | Supported? |
| --- | --- | --- |
| INTEGER | VARCHAR | Yes |
| VARCHAR | INTEGER | Yes, if valid numeric text |
| INTEGER | NUMERIC | Yes |
| NUMERIC | INTEGER | Yes, subject to conversion and range |
| DATE | CHAR | Yes |
| CHAR | DATE | Yes, if valid date representation |
| TIMESTAMP | DATE | Yes, date portion |
| DATE | TIMESTAMP | Yes, time defaults appropriately |
| BOOLEAN | VARCHAR | Yes |
| VARCHAR | BOOLEAN | Yes, if valid Boolean text |

Let's understand each conversion.

## 7.3 INTEGER to VARCHAR

```sql
SELECT CAST(12345 AS VARCHAR(10))
FROM (VALUES(0)) AS t(x);
```

Result:

```text
'12345'
```

The numeric value becomes a character string.

Important:

```sql
CAST(12345 AS VARCHAR(3))
```

An explicit character CAST can truncate:

```text
'123'
```

This differs from assigning a longer string directly to a smaller VARCHAR column.

## 7.4 VARCHAR to INTEGER

```sql
SELECT CAST('12345' AS INTEGER)
FROM (VALUES(0)) AS t(x);
```

Result:

```text
12345
```

Valid:

```sql
CAST('100' AS INTEGER)
CAST('-100' AS INTEGER)
CAST('+100' AS INTEGER)
CAST(' 100 ' AS INTEGER)
```

Invalid:

```sql
CAST('100A' AS INTEGER)
CAST('12.5' AS INTEGER)
CAST('ABC' AS INTEGER)
CAST('' AS INTEGER)
```

A decimal string is not automatically a valid INTEGER representation.

If you want to convert decimal text, convert it to NUMERIC first:

```sql
SELECT CAST(
    CAST('123.45' AS NUMERIC(6,2))
    AS INTEGER
)
FROM (VALUES(0)) AS t(x);
```

The final integer conversion follows the database's numeric conversion rules.

## 7.5 INTEGER to NUMERIC

```sql
SELECT CAST(123 AS NUMERIC(5,2))
FROM (VALUES(0)) AS t(x);
```

Result:

```text
123.00
```

The integer is represented using two fractional digits.

Examples:

| Source | Target | Result |
| --- | --- | --- |
| 123 | NUMERIC(5,2) | 123.00 |
| 12 | NUMERIC(4,2) | 12.00 |
| 12345 | NUMERIC(5,2) | Error |
| 99 | NUMERIC(2,0) | 99 |

The last two cases demonstrate why precision matters.

`NUMERIC(5,2)` permits only three integral digits.

## 7.6 NUMERIC to INTEGER

```sql
SELECT CAST(123.45 AS INTEGER)
FROM (VALUES(0)) AS t(x);
```

The fractional component is lost during conversion.

**HSQLDB-specific warning:** Do not apply one universal rounding rule to every numeric type.

HSQLDB has a database setting called:

```sql
SET DATABASE SQL CONVERT TRUNCATE TRUE;
```

This controls conversion from `DOUBLE` to integral types.

- `TRUE` (default): truncate the fractional part.
- `FALSE`: use rounding instead.

For example, converting a DOUBLE value of `1234.56` to an integer produces `1234` with the default setting, and `1235` when the setting is FALSE. This setting specifically concerns DOUBLE conversion, not every exact NUMERIC conversion.

For predictable application logic, explicitly choose the required operation:

```sql
SELECT
    CAST(FLOOR(123.9) AS INTEGER),
    CAST(ROUND(123.9) AS INTEGER),
    CAST(TRUNC(123.9) AS INTEGER)
FROM (VALUES(0)) AS t(x);
```

Results:

```text
123
124
123
```

## 7.7 DATE to CHAR / VARCHAR

```sql
SELECT CAST(
    DATE '2026-11-08'
    AS VARCHAR(20)
)
FROM (VALUES(0)) AS t(x);
```

Result:

```text
2026-11-08
```

You can also use:

```sql
SELECT CAST(
    DATE '2026-11-08'
    AS CHAR(10)
)
FROM (VALUES(0)) AS t(x);
```

Result:

```text
2026-11-08
```

The CHAR result has a fixed length of 10.

## 7.8 CHAR / VARCHAR to DATE

```sql
SELECT CAST(
    '2026-11-08'
    AS DATE
)
FROM (VALUES(0)) AS t(x);
```

Result:

```text
2026-11-08
```

Valid:

```sql
CAST('2026-11-08' AS DATE)
```

Invalid:

```sql
CAST('2026-13-08' AS DATE)
CAST('2026-11-35' AS DATE)
CAST('08-11-2026' AS DATE)
CAST('2026/11/08' AS DATE)
```

The input must represent a valid date in a format accepted by HSQLDB.

**Important real-world scenario:**

Suppose a CSV contains:

```text
16-06-2023
```

But your database expects an ISO-style date:

```text
2023-06-16
```

You cannot assume that casting the original string will work.

You can rearrange the text:

```sql
SELECT CAST(
    SUBSTRING('16-06-2023', 7, 4) || '-' ||
    SUBSTRING('16-06-2023', 4, 2) || '-' ||
    SUBSTRING('16-06-2023', 1, 2)
    AS DATE
)
FROM (VALUES(0)) AS t(x);
```

Result:

```text
2023-06-16
```

This is particularly useful when importing CSV files.

## 7.9 TIMESTAMP to DATE

```sql
SELECT CAST(
    TIMESTAMP '2026-11-08 10:30:45'
    AS DATE
)
FROM (VALUES(0)) AS t(x);
```

Result:

```text
2026-11-08
```

The time portion is removed.

## 7.10 DATE to TIMESTAMP

```sql
SELECT CAST(
    DATE '2026-11-08'
    AS TIMESTAMP
)
FROM (VALUES(0)) AS t(x);
```

Conceptual result:

```text
2026-11-08 00:00:00
```

The missing time portion is initialized to midnight.

## 7.11 Implicit versus explicit conversion

Consider:

```sql
CREATE TABLE conversion_test (
    amount NUMERIC(8,2)
);
```

This may accept compatible numeric expressions without an explicit CAST:

```sql
INSERT INTO conversion_test
VALUES (100);
```

But explicit conversion is useful when:

- You want to control precision.
- You want to force truncation.
- You need to interpret a string as a date.
- You need to resolve an ambiguous expression type.
- You need to avoid unexpected implicit conversions.

**Developer rule:** Never rely on implicit conversion when processing untrusted input from CSV files, APIs or external applications.

---

# 8. SQL Operators in HSQLDB

An operator performs an operation on one or more values.

Major operator categories:

1. Arithmetic operators.
2. Comparison/relational operators.
3. Logical operators.
4. Special predicates.
5. String concatenation operators.

## 8.1 Arithmetic operators

| Operator | Meaning | Example | Result |
| --- | --- | --- | --- |
| `+` | Addition | 10 + 5 | 15 |
| `-` | Subtraction | 10 - 5 | 5 |
| `*` | Multiplication | 10 * 5 | 50 |
| `/` | Division | 10 / 5 | 2 |
| `MOD()` | Remainder | MOD(10,3) | 1 |

Examples:

```sql
SELECT
    10 + 5,
    10 - 5,
    10 * 5,
    10 / 5,
    MOD(10,3)
FROM (VALUES(0)) AS t(x);
```

### Important division edge case

HSQLDB's default division result scale is not automatically five decimal places.

By default, division preserves the scale of the numeric type involved.

For example:

```sql
SELECT 7 / 3
FROM (VALUES(0)) AS t(x);
```

The result is `2` by default.

You can change the database's default division/AVG scale using:

```sql
SET DATABASE SQL AVG SCALE 2;
```

Then division and average results can use scale 2 when the property applies.

For example:

```text
7 / 3 = 2.33
```

The setting supports values from 0 to 10 and does not affect DOUBLE values.

### 8.2 Precision and scale in arithmetic

Let:

- `p1`, `p2` = precision of the operands.
- `s1`, `s2` = scale of the operands.

The general SQL precision/scale rules are:

| Operation | Result scale concept |
| --- | --- |
| Addition | Maximum of the operand scales |
| Subtraction | Maximum of the operand scales |
| Multiplication | Sum of operand scales |
| Division | Depends on database division-scale rules |

For example:

```text
12.34 + 1.2 = 13.54
```

The scale is 2.

```text
12.34 * 1.2 = 14.808
```

The scale is 3.

```text
12.34 - 1.2 = 11.14
```

The scale is 2.

**Important HSQLDB distinction:** These are the conceptual decimal arithmetic rules. The actual result metadata and division/AVG scale should be checked against HSQLDB's expression rules and `sql.avg_scale` setting. Do not memorize a universal rule that division always produces five decimal places.

### 8.3 Integer division versus decimal division

Try:

```sql
SELECT 10 / 4
FROM (VALUES(0)) AS t(x);
```

Then:

```sql
SELECT
    CAST(10 AS NUMERIC(5,2)) /
    CAST(4 AS NUMERIC(5,2))
FROM (VALUES(0)) AS t(x);
```

The second expression uses decimal operands.

For a developer, the important lesson is to control the operand types and result scale instead of assuming division always behaves like a calculator.

### 8.4 Division by zero

```sql
SELECT 10 / 0
FROM (VALUES(0)) AS t(x);
```

This causes a division-by-zero exception for exact numeric values.

Protect calculations:

```sql
SELECT
    CASE
        WHEN quantity = 0 THEN NULL
        ELSE amount / quantity
    END
FROM sales;
```

---

# 9. Relational / Comparison Operators

These operators compare two values and return a Boolean result.

| Operator | Meaning |
| --- | --- |
| `=` | Equal |
| `<>` | Not equal |
| `!=` | Not equal |
| `>` | Greater than |
| `<` | Less than |
| `>=` | Greater than or equal |
| `<=` | Less than or equal |

Example:

```sql
SELECT *
FROM employee
WHERE salary >= 50000;
```

### Tricky cases

```sql
SELECT *
FROM employee
WHERE salary <> 50000;
```

This does not return rows where salary is NULL.

Why?

Because comparison with NULL produces UNKNOWN.

Use:

```sql
WHERE salary IS NULL;
```

For two NULL values:

```sql
NULL = NULL
```

The result is UNKNOWN, not TRUE.

---

# 10. Logical Operators

There are three fundamental logical operators.

| Operator | Meaning |
| --- | --- |
| AND | Both conditions must be TRUE |
| OR | At least one condition must be TRUE |
| NOT | Reverses TRUE/FALSE |

Example:

```sql
SELECT *
FROM employee
WHERE salary > 30000
AND department_id = 10;
```

## 10.1 Truth table

SQL uses three-valued logic: TRUE, FALSE and UNKNOWN.

| A | B | A AND B | A OR B |
| --- | --- | --- | --- |
| TRUE | TRUE | TRUE | TRUE |
| TRUE | FALSE | FALSE | TRUE |
| TRUE | UNKNOWN | UNKNOWN | TRUE |
| FALSE | FALSE | FALSE | FALSE |
| FALSE | UNKNOWN | FALSE | UNKNOWN |
| UNKNOWN | UNKNOWN | UNKNOWN | UNKNOWN |

For NOT:

| A | NOT A |
| --- | --- |
| TRUE | FALSE |
| FALSE | TRUE |
| UNKNOWN | UNKNOWN |

**Very important:** UNKNOWN is not the same as FALSE.

A WHERE clause returns only rows for which its condition evaluates to TRUE.

---

# 11. Special SQL Operators and Predicates

These are particularly important for SQL developer interviews.

## 11.1 BETWEEN

Used to check whether a value falls within a range.

```sql
SELECT *
FROM employee
WHERE salary BETWEEN 30000 AND 50000;
```

Equivalent to:

```sql
WHERE salary >= 30000
AND salary <= 50000;
```

**Edge case:** BETWEEN is inclusive of both boundaries.

| Salary | Returned? |
| --- | --- |
| 29999 | No |
| 30000 | Yes |
| 40000 | Yes |
| 50000 | Yes |
| 50001 | No |

NOT BETWEEN:

```sql
WHERE salary NOT BETWEEN 30000 AND 50000;
```

NULL values still produce UNKNOWN.

## 11.2 IN

Checks whether a value matches any value in a list.

```sql
SELECT *
FROM employee
WHERE department_id IN (10,20,30);
```

Equivalent to:

```sql
WHERE department_id = 10
OR department_id = 20
OR department_id = 30;
```

### Important NULL edge case

```sql
SELECT *
FROM employee
WHERE department_id IN (10,20,NULL);
```

For a department ID of 30:

- It does not match 10.
- It does not match 20.
- It compares with NULL, resulting in UNKNOWN.
- The overall condition is UNKNOWN.

Therefore, the row is not returned.

### NOT IN trap

```sql
WHERE department_id NOT IN (10,20,NULL);
```

This can return no rows because non-matching values produce UNKNOWN.

**Professional rule:** Be careful when using `NOT IN` with a subquery that may return NULL. `NOT EXISTS` is often safer.

## 11.3 LIKE

Used for pattern matching.

Two wildcard characters:

| Wildcard | Meaning |
| --- | --- |
| `%` | Zero or more characters |
| `_` | Exactly one character |

Examples:

```sql
-- Names beginning with A
WHERE emp_name LIKE 'A%';

-- Names ending with n
WHERE emp_name LIKE '%n';

-- Names containing ar
WHERE emp_name LIKE '%ar%';

-- Second character is a
WHERE emp_name LIKE '_a%';

-- Exactly five characters, beginning with A
WHERE emp_name LIKE 'A____';
```

### LIKE edge cases

```sql
WHERE emp_name LIKE 'A%'
```

Matches:

```text
Arun
Anand
A
```

```sql
WHERE emp_name LIKE 'A_'
```

Matches a two-character string beginning with A.

`LIKE` is generally case-sensitive under the default HyperSQL collation. Collation settings can change this behaviour.

### ESCAPE in LIKE

Suppose you want to search for an actual `%` character.

```sql
SELECT *
FROM products
WHERE product_name LIKE '%\%%' ESCAPE '\';
```

This searches for a literal percent sign.

## 11.4 IS NULL

Checks whether a value is NULL.

Correct:

```sql
WHERE salary IS NULL;
```

Incorrect:

```sql
WHERE salary = NULL;
```

Similarly:

```sql
WHERE salary IS NOT NULL;
```

## 11.5 Additional useful predicates

| Predicate | Purpose |
| --- | --- |
| `EXISTS` | Checks whether a subquery returns rows |
| `NOT EXISTS` | Checks whether a subquery returns no rows |
| `ANY` | Compares against any value returned by a subquery |
| `ALL` | Compares against every value returned by a subquery |
| `IS TRUE` | Checks whether Boolean value is TRUE |
| `IS FALSE` | Checks whether Boolean value is FALSE |
| `IS UNKNOWN` | Checks whether Boolean value is UNKNOWN |
| `IS DISTINCT FROM` | NULL-safe comparison |
| `IS NOT DISTINCT FROM` | NULL-safe equality comparison |

Example:

```sql
SELECT *
FROM employee
WHERE EXISTS (
    SELECT 1
    FROM department d
    WHERE d.department_id = employee.department_id
);
```

### NULL-safe comparison

```sql
SELECT
    NULL IS NOT DISTINCT FROM NULL
FROM (VALUES(0)) AS t(x);
```

Result:

```text
TRUE
```

Unlike ordinary equality, `IS NOT DISTINCT FROM` treats two NULL values as equal for comparison purposes.

---

# 12. Operator Precedence

When multiple operators are used in one expression, SQL follows precedence rules.

From higher to lower precedence:

| Priority | Operators |
| --- | --- |
| 1 | Unary `+`, `-` |
| 2 | `*`, `/`, `MOD` |
| 3 | `+`, `-` |
| 4 | Comparison operators |
| 5 | `IS NULL`, `BETWEEN`, `IN`, `LIKE` |
| 6 | `NOT` |
| 7 | `AND` |
| 8 | `OR` |

Parentheses override precedence.

Example:

```sql
SELECT 10 + 5 * 2
FROM (VALUES(0)) AS t(x);
```

Result:

```text
20
```

Because multiplication happens first.

```sql
SELECT (10 + 5) * 2
FROM (VALUES(0)) AS t(x);
```

Result:

```text
30
```

### Tricky example

```sql
SELECT *
FROM employee
WHERE department_id = 10
   OR department_id = 20
  AND salary > 50000;
```

Equivalent to:

```sql
WHERE department_id = 10
   OR (department_id = 20 AND salary > 50000);
```

It does NOT mean:

```sql
WHERE (department_id = 10 OR department_id = 20)
AND salary > 50000;
```

This is a common production-query bug.

---

# 13. Additional HSQLDB Data Types You Should Know

For a two-year SQL developer, do not restrict your knowledge to the basic types.

| Type | Purpose |
| --- | --- |
| BINARY(n) | Fixed-length binary data |
| VARBINARY(n) | Variable-length binary data |
| BIT(n) | Fixed-length bit string |
| ARRAY | Collection of values of a declared element type |
| INTERVAL | Duration between date/time values |
| UUID | Universally unique identifier |
| OTHER | Serializable Java objects |

Some additional important details:

**BINARY versus VARBINARY**

Similar to CHAR versus VARCHAR, but for binary data.

- BINARY pads shorter values with zero bytes.
- VARBINARY does not pad shorter values.

**INTERVAL**

Used to represent durations.

Examples:

```sql
INTERVAL '2' DAY
INTERVAL '3' MONTH
INTERVAL '5:30' HOUR TO MINUTE
```

Useful for date/time calculations.

**UUID**

Used for unique identifiers.

Example:

```sql
CREATE TABLE users (
    user_id UUID,
    username VARCHAR(50)
);
```

**BIT**

Stores bit strings rather than ordinary text.

The maximum declared BIT length in HyperSQL is 1024.

---

# 14. Advanced Developer-Level Edge Cases

These are the concepts that distinguish someone who knows SQL syntax from someone who understands database behaviour.

## 14.1 NULL versus empty string versus spaces

Consider:

```sql
INSERT INTO employee(emp_name)
VALUES (NULL);

INSERT INTO employee(emp_name)
VALUES ('');

INSERT INTO employee(emp_name)
VALUES ('   ');
```

These are three different values:

| Value | Meaning |
| --- | --- |
| NULL | Missing/unknown |
| `''` | Empty string |
| `'   '` | String containing spaces |

Check them separately:

```sql
SELECT *
FROM employee
WHERE emp_name IS NULL;
```

```sql
SELECT *
FROM employee
WHERE emp_name = '';
```

## 14.2 COALESCE

Returns the first non-NULL value.

```sql
SELECT COALESCE(salary, 0)
FROM employee;
```

If salary is NULL, returns zero.

## 14.3 NULLIF

Returns NULL if two expressions are equal.

```sql
SELECT NULLIF(100,100)
FROM (VALUES(0)) AS t(x);
```

Result:

```text
NULL
```

Useful for preventing division by zero:

```sql
SELECT amount / NULLIF(quantity, 0)
FROM sales;
```

## 14.4 CASE WHEN

Conditional logic in SQL.

```sql
SELECT
    emp_name,
    CASE
        WHEN salary >= 100000 THEN 'HIGH'
        WHEN salary >= 50000 THEN 'MEDIUM'
        WHEN salary IS NULL THEN 'UNKNOWN'
        ELSE 'LOW'
    END AS salary_category
FROM employee;
```

Remember that CASE evaluates conditions in order. The first matching condition determines the result.

## 14.5 ROUND versus TRUNC versus FLOOR

| Function | Input | Result |
| --- | --- | --- |
| ROUND(23.76,1) | 23.76 | 23.8 |
| TRUNC(23.76,1) | 23.76 | 23.7 |
| FLOOR(23.76) | 23.76 | 23 |
| CEILING(23.76) | 23.76 | 24 |

Negative values are particularly tricky:

| Function | Input | Result |
| --- | --- | --- |
| FLOOR(-23.2) | -23.2 | -24 |
| CEILING(-23.2) | -23.2 | -23 |
| TRUNC(-23.2) | -23.2 | -23 |

## 14.6 Aggregate functions and NULL

Consider:

| ID | Salary |
| --- | --- |
| 1 | 1000 |
| 2 | 2000 |
| 3 | NULL |
| 4 | 3000 |

```sql
SELECT
    COUNT(*),
    COUNT(salary),
    SUM(salary),
    AVG(salary)
FROM employee;
```

Results:

| Function | Result |
| --- | --- |
| COUNT(*) | 4 |
| COUNT(salary) | 3 |
| SUM(salary) | 6000 |
| AVG(salary) | 2000 |

COUNT(column) ignores NULL values.

COUNT(*) counts rows regardless of NULL values.

## 14.7 Important HSQLDB configuration traps

HSQLDB exposes several SQL compatibility settings that can change results.

| Setting | Default | What it affects |
| --- | --- | --- |
| `sql.avg_scale` | 0 | Division and AVG result scale |
| `sql.convert_trunc` | TRUE | DOUBLE-to-integral conversion |
| `sql.pad_space` | TRUE | String comparison with trailing spaces |
| `sql.ignore_case` | FALSE | Case-insensitive VARCHAR comparison |
| `sql.concat_nulls` | TRUE | Concatenation involving NULL |
| `sql.double_nan` | TRUE | DOUBLE division-by-zero behaviour |

For example, HSQLDB defaults to padding shorter character values during string comparisons.

Thus:

```sql
SELECT 'ABC' = 'ABC   '
FROM (VALUES(0)) AS t(x);
```

Normally returns TRUE under the default PAD SPACE behaviour.

The configuration can be changed, so verify database settings when investigating surprising results.

---

# 15. Practice Quiz - 15 Advanced HSQLDB Questions

(2-year SQL developer level) (15 MCQs)

These questions cover numeric precision, conversion, string storage, operators, NULL and HSQLDB-specific behaviour.

Try answering before checking the solutions.

**HSQLDB advanced assessment** (/15 answered)

---

# 16. What You Should Master as a 2-Year SQL Developer

Use this checklist to evaluate your preparation.



## Official HSQLDB references

For version-specific behaviour, particularly precision, conversions and configuration:

1. HyperSQL User Guide - Complete documentation.
2. SQL Language and Data Types.
3. Data Access, CAST and SQL Expressions.
4. HSQLDB 2.7 Documentation Portal.

**My recommendation:** Master Sections 3-11 first. Numeric precision, string padding, implicit conversion, NULL logic, and `NOT IN` are especially important because they cause subtle bugs in real SQL applications.

The examples above target HSQLDB 2.7.x. Some behaviours are controlled by database configuration, so always check the actual version and settings when debugging an existing system.

### User

for 2 year sql developer hsql database level give concepts needed from required topics all tricky advanced topics from these explanation and 15 question quiz at end all edge cases DDL: Create table syntax minimum 1 column required data type, will fail if table already exist unique name rows columns organized, constrains not null primary key check unique foreign key defnition, types of constraint constraint classification single column constriaint composite constraint column level constraint table level contraint how each defined example single column constraint can be specified at column or table level, composite constraint at table level only not null only at column level, how constraint can be define in create syntax after defining in column for each constraint give, not null column insert record in table insert where fname is null, insert space in not null column insert empty string in not null column what will happen, primary key insert valid record insert where col is null, insert duplicate record what will happen, need for composite primary key student course marks example how isit defined after declaring column in create table syntax give, check constraint value not allowed by check, insert record with null value, unique constraint insert null value insert duplicate record in column what will happen eahc time, freign key inserting marks of studnet present in student table inserting marks of student not present in student tabe inserting null in student id in studentid courseid marks table, default constraint insert recird witg yser specified value insert null insert without any data, alter table adding a column: alter table tablename add column colname datatype, modifiying a column: alter table tablename alter column colname new datatype increase or decrease also same, renaming a column: alter table tablename alter column colname rename to newcolname, deleting a column: alter table employee drop column columnname, adding a constraint all constraint give alter table tabname add constriant constraing tname constraint(col) , deleting a constraint alter table tabname drop constraint constriant name, drop table: drop table delete record as well as structure drop table tablename tabe withut reference, if reference there 2 ways drop child table then parent table else drop table if exists parentablename cascade; drops parent table as well as foreign key constraint from child table that refers to parent table, truncate table table name just removes rows not table and structure

### ChatGPT

# HSQLDB - Advanced DDL, Constraints and Table Management

(2-Year SQL Developer Level) (15 MCQ Assessment)

This guide covers DDL commands and constraints in HSQLDB, from basic table creation to advanced constraint behaviour, composite keys, foreign-key relationships, ALTER TABLE operations, DROP, TRUNCATE and tricky insertion scenarios.

The focus is on understanding **what happens to the database when a statement executes**, not just memorising SQL syntax.

# 1. DDL - Data Definition Language

DDL stands for Data Definition Language.

It is used to create, modify and delete database structures such as:

- Tables
- Columns
- Constraints
- Views
- Schemas
- Indexes

The major DDL commands are:

| Command | Purpose |
| --- | --- |
| CREATE | Creates database objects |
| ALTER | Modifies existing objects |
| DROP | Removes database objects |
| TRUNCATE | Removes all rows from a table |

## 1.1 CREATE TABLE

The `CREATE TABLE` statement creates a new table in the database.

**Syntax:**

```sql
CREATE TABLE table_name (
    column1 datatype,
    column2 datatype,
    column3 datatype
);
```

Example:

```sql
CREATE TABLE employee (
    emp_id INTEGER,
    fname VARCHAR(30),
    lname VARCHAR(30),
    salary NUMERIC(10,2)
);
```

This creates an employee table with four columns.

### Important rules

1. A table must contain at least one column.
2. Every column must have a name and data type.
3. Column names within a table must be unique.
4. Table names must be unique within their schema.
5. You cannot create a table with an already-existing name in the same schema.
6. A table can contain zero or more rows immediately after creation.
7. A table can have multiple constraints.
8. Column definitions and table-level constraints are specified inside parentheses.

Example of an invalid statement:

```sql
CREATE TABLE employee (
);
```

This fails because a table must have at least one column.

### What happens if the table already exists?

```sql
CREATE TABLE employee (
    emp_id INTEGER
);
```

If `employee` already exists, HSQLDB raises an error.

To avoid that error:

```sql
CREATE TABLE IF NOT EXISTS employee (
    emp_id INTEGER
);
```

This creates the table only if it does not already exist.

**Important:** `IF NOT EXISTS` does not modify an existing table. It simply avoids recreating it.

---

# 2. Constraints in SQL

A constraint is a rule enforced by the database to maintain data integrity.

Suppose you have an employee table.

You want to ensure:

- Employee ID cannot be NULL.
- Employee ID must be unique.
- Salary cannot be negative.
- Department ID must refer to an existing department.

These rules are implemented using constraints.

## 2.1 Types of constraints

There are six important constraints you should master.

| Constraint | Purpose |
| --- | --- |
| NOT NULL | Prevents NULL values |
| PRIMARY KEY | Uniquely identifies each row |
| UNIQUE | Prevents duplicate values |
| CHECK | Enforces a condition |
| FOREIGN KEY | Enforces referential integrity |
| DEFAULT | Supplies a value when one is omitted |

Technically, `DEFAULT` is a column default rather than a constraint in the same sense as a CHECK or UNIQUE constraint. It is nevertheless commonly taught alongside SQL constraints.

## 2.2 Constraint classification

Constraints can be classified based on where and how they are declared.

There are two important classifications:

**Classification A - By declaration location**

1. Column-level constraints.
2. Table-level constraints.

**Classification B - By number of columns involved**

1. Single-column constraints.
2. Composite constraints.

These classifications are related but not identical.

### A. Column-level constraint

A constraint is defined directly alongside a column definition.

Example:

```sql
CREATE TABLE employee (
    emp_id INTEGER PRIMARY KEY,
    fname VARCHAR(30) NOT NULL,
    salary NUMERIC(10,2) CHECK (salary >= 0)
);
```

Here:

- PRIMARY KEY is declared alongside `emp_id`.
- NOT NULL is declared alongside `fname`.
- CHECK is declared alongside `salary`.

### B. Table-level constraint

A constraint is declared separately after all column definitions.

Example:

```sql
CREATE TABLE employee (
    emp_id INTEGER,
    fname VARCHAR(30),
    salary NUMERIC(10,2),

    PRIMARY KEY (emp_id),
    CHECK (salary >= 0)
);
```

### C. Single-column constraint

A constraint involving only one column.

Example:

```sql
CREATE TABLE employee (
    emp_id INTEGER,
    email VARCHAR(100),

    UNIQUE (email)
);
```

This is a single-column UNIQUE constraint, although declared at table level.

### D. Composite constraint

A constraint involving two or more columns.

Example:

```sql
CREATE TABLE student_marks (
    student_id INTEGER,
    course_id INTEGER,
    marks INTEGER,

    PRIMARY KEY (student_id, course_id)
);
```

The combination of `student_id` and `course_id` must be unique.

**Important classification table**

| Constraint | Column-level | Table-level |
| --- | --- | --- |
| NOT NULL | Yes | No |
| PRIMARY KEY | Yes, single column | Yes, single or composite |
| UNIQUE | Yes | Yes, single or composite |
| CHECK | Yes | Yes |
| FOREIGN KEY | Yes, single column | Yes, single or composite |
| DEFAULT | Yes | No |

NOT NULL and DEFAULT are specified as column properties. A composite constraint must be declared at table level.

# 3. NOT NULL Constraint

The NOT NULL constraint ensures that a column cannot contain a NULL value.

### 3.1 Column-level syntax

```sql
CREATE TABLE student (
    student_id INTEGER,
    fname VARCHAR(30) NOT NULL
);
```

### 3.2 Named NOT NULL constraint

HSQLDB also supports naming a NOT NULL constraint:

```sql
CREATE TABLE student (
    student_id INTEGER,
    fname VARCHAR(30)
        CONSTRAINT nn_fname NOT NULL
);
```

### 3.3 What happens during INSERT?

Assume:

```sql
CREATE TABLE student (
    student_id INTEGER,
    fname VARCHAR(30) NOT NULL
);
```

**Case 1: Insert a valid value**

```sql
INSERT INTO student
VALUES (1, 'Arun');
```

(Success)

Both columns receive valid values.

**Case 2: Insert NULL**

```sql
INSERT INTO student
VALUES (2, NULL);
```

(Error)

The NOT NULL constraint is violated.

**Case 3: Insert an empty string**

```sql
INSERT INTO student
VALUES (3, '');
```

(Success)

An empty string is not NULL in HSQLDB.

The column contains a string with zero characters.

**Case 4: Insert spaces**

```sql
INSERT INTO student
VALUES (4, '   ');
```

(Success)

Spaces are actual character data, not NULL.

**Case 5: Omit the column**

```sql
INSERT INTO student(student_id)
VALUES (5);
```

(Error)

The omitted column receives NULL because there is no default value.

### Important interview question

Does NOT NULL prevent empty strings?

**No.**

Does NOT NULL prevent spaces?

**No.**

Does NOT NULL prevent NULL?

**Yes.**

If you want to prevent both NULL and empty strings, use:

```sql
CREATE TABLE student (
    student_id INTEGER,
    fname VARCHAR(30) NOT NULL,
    CHECK (LENGTH(TRIM(fname)) > 0)
);
```

This rejects empty strings and strings containing only spaces.

---

# 4. PRIMARY KEY Constraint

A primary key uniquely identifies every record in a table.

A primary key has two fundamental properties:

1. Every value must be unique.
2. No primary-key column can contain NULL.

A table can have only one primary key constraint, but that primary key can contain multiple columns.

## 4.1 Single-column primary key

Column-level definition:

```sql
CREATE TABLE student (
    student_id INTEGER PRIMARY KEY,
    fname VARCHAR(30),
    age INTEGER
);
```

Table-level definition:

```sql
CREATE TABLE student (
    student_id INTEGER,
    fname VARCHAR(30),
    age INTEGER,

    PRIMARY KEY (student_id)
);
```

Both definitions create the same type of primary key.

## 4.2 Primary key insertion scenarios

Consider:

```sql
CREATE TABLE student (
    student_id INTEGER PRIMARY KEY,
    fname VARCHAR(30)
);
```

**Case 1: Valid record**

```sql
INSERT INTO student
VALUES (101, 'Arun');
```

(Success)

**Case 2: NULL primary key**

```sql
INSERT INTO student
VALUES (NULL, 'Kumar');
```

(Error)

Primary keys cannot contain NULL.

**Case 3: Duplicate primary key**

```sql
INSERT INTO student
VALUES (101, 'Ravi');
```

(Error)

Student ID 101 already exists.

**Case 4: Different primary key**

```sql
INSERT INTO student
VALUES (102, 'Ravi');
```

(Success)

Different primary key values are permitted.

### PRIMARY KEY versus UNIQUE

| Feature | PRIMARY KEY | UNIQUE |
| --- | --- | --- |
| Duplicate values | Not allowed | Not allowed |
| NULL | Not allowed | NULL generally permitted |
| Number per table | One | Multiple |
| Composite columns | Supported | Supported |
| Identifies a row | Yes | Not necessarily the designated identifier |

In HSQLDB, a UNIQUE constraint allows multiple NULL values because NULL values are treated as distinct for uniqueness purposes.

---

# 5. Composite Primary Key

This is a very important real-world SQL concept.

A composite primary key is a primary key consisting of two or more columns.

### Real-world scenario: Student and course marks

Suppose a student can enroll in multiple courses.

A course can have multiple students.

Consider:

**STUDENT table**

| student_id | student_name |
| --- | --- |
| 101 | Arun |
| 102 | Ravi |
| 103 | Kumar |

**COURSE table**

| course_id | course_name |
| --- | --- |
| 10 | Java |
| 20 | SQL |
| 30 | Python |

**STUDENT_MARKS table**

| student_id | course_id | marks |
| --- | --- | --- |
| 101 | 10 | 90 |
| 101 | 20 | 85 |
| 102 | 10 | 78 |
| 103 | 30 | 95 |

Can student 101 appear more than once?

Yes, because that student can take multiple courses.

Can course 10 appear more than once?

Yes, because multiple students can enroll in course 10.

But can the combination `(101,10)` appear twice?

No.

That is why we need a composite primary key.

### Syntax

```sql
CREATE TABLE student_marks (
    student_id INTEGER,
    course_id INTEGER,
    marks INTEGER,

    PRIMARY KEY (student_id, course_id)
);
```

Notice that the primary key is defined after the individual column definitions.

### Test the constraint

Valid:

```sql
INSERT INTO student_marks
VALUES (101, 10, 90);
```

Valid:

```sql
INSERT INTO student_marks
VALUES (101, 20, 85);
```

Valid:

```sql
INSERT INTO student_marks
VALUES (102, 10, 78);
```

Invalid:

```sql
INSERT INTO student_marks
VALUES (101, 10, 95);
```

Why?

The combination of student ID 101 and course ID 10 already exists.

### Composite primary key edge cases

| student_id | course_id | Result |
| --- | --- | --- |
| 101 | 10 | Valid |
| 101 | 20 | Valid |
| 102 | 10 | Valid |
| 101 | 10 | Duplicate error |
| NULL | 10 | Error |
| 101 | NULL | Error |
| NULL | NULL | Error |

**Important:** Every column participating in a composite primary key becomes NOT NULL.

---

# 6. UNIQUE Constraint

The UNIQUE constraint ensures that duplicate values are not allowed in a column or combination of columns.

Example:

```sql
CREATE TABLE employee (
    emp_id INTEGER PRIMARY KEY,
    email VARCHAR(100) UNIQUE,
    phone VARCHAR(15) UNIQUE
);
```

Here:

- Employee ID is the primary key.
- Email must be unique.
- Phone must be unique.

### 6.1 Column-level UNIQUE

```sql
CREATE TABLE employee (
    emp_id INTEGER PRIMARY KEY,
    email VARCHAR(100) UNIQUE
);
```

### 6.2 Table-level UNIQUE

```sql
CREATE TABLE employee (
    emp_id INTEGER,
    email VARCHAR(100),

    PRIMARY KEY (emp_id),
    UNIQUE (email)
);
```

### 6.3 Named UNIQUE constraint

```sql
CREATE TABLE employee (
    emp_id INTEGER,
    email VARCHAR(100),

    CONSTRAINT uq_email UNIQUE (email)
);
```

### 6.4 INSERT scenarios

Consider:

```sql
CREATE TABLE employee (
    emp_id INTEGER PRIMARY KEY,
    email VARCHAR(100) UNIQUE
);
```

**Case 1: First email**

```sql
INSERT INTO employee
VALUES (1, 'a@gmail.com');
```

(Success)

**Case 2: Duplicate email**

```sql
INSERT INTO employee
VALUES (2, 'a@gmail.com');
```

(Error)

**Case 3: NULL email**

```sql
INSERT INTO employee
VALUES (3, NULL);
```

(Success)

**Case 4: Another NULL email**

```sql
INSERT INTO employee
VALUES (4, NULL);
```

(Success)

HSQLDB permits multiple NULL values under a UNIQUE constraint.

**Case 5: Empty string**

```sql
INSERT INTO employee
VALUES (5, '');
```

(Success)

Another empty string:

```sql
INSERT INTO employee
VALUES (6, '');
```

(Error)

An empty string is a value, and it is equal to the previously stored empty string.

### 6.5 Composite UNIQUE constraint

```sql
CREATE TABLE employee_project (
    emp_id INTEGER,
    project_id INTEGER,
    role VARCHAR(30),

    UNIQUE (emp_id, project_id)
);
```

The combination must be unique.

| emp_id | project_id | Result |
| --- | --- | --- |
| 101 | 10 | Valid |
| 101 | 20 | Valid |
| 102 | 10 | Valid |
| 101 | 10 | Duplicate |

Neither column individually needs to be unique.

---

# 7. CHECK Constraint

The CHECK constraint validates a condition before allowing a record to be inserted or updated.

Example:

```sql
CREATE TABLE employee (
    emp_id INTEGER,
    age INTEGER CHECK (age >= 18),
    salary NUMERIC(10,2) CHECK (salary >= 0)
);
```

Conditions:

- Age must be at least 18.
- Salary must not be negative.

## 7.1 Column-level CHECK

```sql
CREATE TABLE employee (
    emp_id INTEGER,
    age INTEGER CHECK (age >= 18)
);
```

## 7.2 Table-level CHECK

```sql
CREATE TABLE employee (
    emp_id INTEGER,
    age INTEGER,
    salary NUMERIC(10,2),

    CHECK (age >= 18),
    CHECK (salary >= 0)
);
```

## 7.3 Named CHECK constraint

```sql
CREATE TABLE employee (
    emp_id INTEGER,
    age INTEGER,

    CONSTRAINT chk_age CHECK (age >= 18)
);
```

## 7.4 INSERT scenarios

Assume:

```sql
CREATE TABLE employee (
    emp_id INTEGER,
    age INTEGER CHECK (age >= 18)
);
```

**Case 1: Valid value**

```sql
INSERT INTO employee
VALUES (1, 25);
```

(Success)

**Case 2: Value violating CHECK**

```sql
INSERT INTO employee
VALUES (2, 15);
```

(Error)

15 is less than 18.

**Case 3: NULL value**

```sql
INSERT INTO employee
VALUES (3, NULL);
```

(Success)

This is a very important edge case.

Why does it succeed?

Because:

```sql
NULL >= 18
```

Produces UNKNOWN.

A CHECK constraint rejects FALSE, but UNKNOWN is accepted.

If you want to reject NULL as well:

```sql
CREATE TABLE employee (
    emp_id INTEGER,
    age INTEGER NOT NULL CHECK (age >= 18)
);
```

### 7.5 CHECK involving multiple columns

Suppose an employee's joining date must not be after their resignation date.

```sql
CREATE TABLE employee (
    emp_id INTEGER,
    joining_date DATE,
    resignation_date DATE,

    CONSTRAINT chk_dates
    CHECK (
        resignation_date IS NULL
        OR joining_date <= resignation_date
    )
);
```

This is a table-level CHECK because it references multiple columns.

**Important limitation:** A CHECK constraint cannot generally be used to enforce conditions that depend on other rows or other tables. Use foreign keys, unique constraints, or triggers depending on the requirement.

---

# 8. FOREIGN KEY Constraint

A foreign key creates a relationship between two tables.

It ensures that a value in the child table references an existing candidate key in the parent table.

Example:

- STUDENT is the parent table.
- STUDENT_MARKS is the child table.

## 8.1 Create the parent table

```sql
CREATE TABLE student (
    student_id INTEGER PRIMARY KEY,
    student_name VARCHAR(50)
);
```

Insert records:

```sql
INSERT INTO student
VALUES
(101, 'Arun'),
(102, 'Ravi'),
(103, 'Kumar');
```

## 8.2 Create the child table

```sql
CREATE TABLE student_marks (
    student_id INTEGER,
    course_id INTEGER,
    marks INTEGER,

    FOREIGN KEY (student_id)
    REFERENCES student(student_id)
);
```

The `student_id` in the child table references `student_id` in the parent table.

## 8.3 Named foreign key

```sql
CREATE TABLE student_marks (
    student_id INTEGER,
    course_id INTEGER,
    marks INTEGER,

    CONSTRAINT fk_student
    FOREIGN KEY (student_id)
    REFERENCES student(student_id)
);
```

## 8.4 INSERT scenarios

**Case 1: Parent ID exists**

```sql
INSERT INTO student_marks
VALUES (101, 10, 90);
```

(Success)

101 exists in the STUDENT table.

**Case 2: Parent ID does not exist**

```sql
INSERT INTO student_marks
VALUES (999, 10, 90);
```

(Error)

999 does not exist in the parent table.

**Case 3: NULL foreign key**

```sql
INSERT INTO student_marks
VALUES (NULL, 10, 90);
```

(Success)

A foreign key does not automatically mean NOT NULL.

If the foreign-key column is nullable, NULL is allowed.

To prevent NULL:

```sql
student_id INTEGER NOT NULL
```

## 8.5 Composite foreign key

Consider a parent table with a composite primary key.

```sql
CREATE TABLE student_course (
    student_id INTEGER,
    course_id INTEGER,

    PRIMARY KEY (student_id, course_id)
);
```

Child table:

```sql
CREATE TABLE student_marks (
    student_id INTEGER,
    course_id INTEGER,
    marks INTEGER,

    CONSTRAINT fk_student_course
    FOREIGN KEY (student_id, course_id)
    REFERENCES student_course(student_id, course_id)
);
```

The referenced column list must correspond to an eligible unique or primary key.

This means:

- `(101,10)` must exist in the parent.
- `(101,20)` must exist in the parent.
- `(101,999)` is invalid if the combination does not exist.

A partial match is insufficient.

### 8.6 ON DELETE and ON UPDATE actions

Foreign keys also support referential actions.

| Action | Behaviour |
| --- | --- |
| NO ACTION | Prevents an operation that violates referential integrity |
| RESTRICT | Restricts deletion/update of referenced rows |
| CASCADE | Propagates deletion/update |
| SET NULL | Sets child foreign-key values to NULL |
| SET DEFAULT | Sets child foreign-key values to their defaults |

Example:

```sql
CREATE TABLE student_marks (
    student_id INTEGER,
    course_id INTEGER,

    FOREIGN KEY (student_id)
    REFERENCES student(student_id)
    ON DELETE CASCADE
);
```

If student 101 is deleted from the parent table, all related rows in `student_marks` are deleted automatically.

Example with SET NULL:

```sql
CREATE TABLE employee (
    emp_id INTEGER PRIMARY KEY,
    manager_id INTEGER,

    FOREIGN KEY (manager_id)
    REFERENCES employee(emp_id)
    ON DELETE SET NULL
);
```

If a manager is deleted, the corresponding manager IDs in child rows become NULL.

The child column must permit NULL for SET NULL to work.

**Interview trap:** A foreign key can reference a UNIQUE column as well as a PRIMARY KEY, provided it satisfies the referenced-key requirements.

---

# 9. DEFAULT Constraint / DEFAULT Clause

DEFAULT specifies the value to use when an INSERT statement does not provide a value for a column.

Example:

```sql
CREATE TABLE employee (
    emp_id INTEGER,
    fname VARCHAR(30),
    status VARCHAR(20) DEFAULT 'ACTIVE',
    salary NUMERIC(10,2) DEFAULT 0
);
```

## 9.1 Insertion scenarios

**Case 1: User specifies a value**

```sql
INSERT INTO employee
VALUES (1, 'Arun', 'INACTIVE', 30000);
```

Result:

| emp_id | fname | status | salary |
| --- | --- | --- | --- |
| 1 | Arun | INACTIVE | 30000 |

The user's value overrides the default.

**Case 2: Column omitted**

```sql
INSERT INTO employee(emp_id, fname)
VALUES (2, 'Ravi');
```

Result:

| emp_id | fname | status | salary |
| --- | --- | --- | --- |
| 2 | Ravi | ACTIVE | 0 |

Defaults are applied.

**Case 3: Explicit NULL**

```sql
INSERT INTO employee
VALUES (3, 'Kumar', NULL, NULL);
```

Result:

| emp_id | fname | status | salary |
| --- | --- | --- | --- |
| 3 | Kumar | NULL | NULL |

The DEFAULT value is not applied because NULL was explicitly supplied.

**Case 4: DEFAULT keyword**

```sql
INSERT INTO employee
VALUES (4, 'Suresh', DEFAULT, DEFAULT);
```

The default values are applied.

**Case 5: Insert without specifying any values**

```sql
INSERT INTO employee
DEFAULT VALUES;
```

HSQLDB attempts to insert a row using the default value of each column.

If a column has no default, its implicit value is NULL. This will fail if that column is NOT NULL or participates in a primary key.

### Important DEFAULT versus NOT NULL

```sql
CREATE TABLE employee (
    emp_id INTEGER,
    status VARCHAR(20) DEFAULT 'ACTIVE' NOT NULL
);
```

Here:

- Omitting status gives ACTIVE.
- Explicitly inserting NULL gives an error.
- Explicitly inserting INACTIVE gives INACTIVE.

DEFAULT does not override an explicitly supplied NULL.

---

# 10. ALTER TABLE - Modifying an Existing Table

`ALTER TABLE` is used to change the structure of an existing table without dropping and recreating it.

The major operations are:

1. Add a column.
2. Modify a column's data type.
3. Rename a column.
4. Drop a column.
5. Add a constraint.
6. Drop a constraint.
7. Set or remove a default.
8. Change column nullability.

## 10.1 ADD COLUMN

Syntax:

```sql
ALTER TABLE table_name
ADD COLUMN column_name datatype;
```

Example:

```sql
ALTER TABLE employee
ADD COLUMN department VARCHAR(30);
```

The department column is added to the employee table.

Before:

| emp_id | fname | salary |
| --- | --- | --- |
| 1 | Arun | 30000 |
| 2 | Ravi | 40000 |

After:

| emp_id | fname | salary | department |
| --- | --- | --- | --- |
| 1 | Arun | 30000 | NULL |
| 2 | Ravi | 40000 | NULL |

**Important edge case: Adding a column to a populated table**

HSQLDB requires an appropriate DEFAULT or GENERATED value when adding a column to a table that already contains rows.

Example:

```sql
ALTER TABLE employee
ADD COLUMN status VARCHAR(20) DEFAULT 'ACTIVE';
```

Existing rows receive the default value.

If the table is populated, do not assume that adding a NOT NULL column without a default will work.

You can also use:

```sql
ALTER TABLE employee
ADD COLUMN IF NOT EXISTS department VARCHAR(30);
```

This avoids an error if that column already exists.

## 10.2 MODIFY / CHANGE DATA TYPE

This is where HSQLDB syntax differs from some other databases.

The HSQLDB syntax is:

```sql
ALTER TABLE table_name
ALTER COLUMN column_name
SET DATA TYPE new_datatype;
```

Example:

```sql
ALTER TABLE employee
ALTER COLUMN fname
SET DATA TYPE VARCHAR(100);
```

This increases the permitted character length.

### Increasing the size

Before:

```sql
fname VARCHAR(30)
```

After:

```sql
ALTER TABLE employee
ALTER COLUMN fname
SET DATA TYPE VARCHAR(100);
```

(Generally safe)

Existing values fit within the new maximum.

### Decreasing the size

Before:

```sql
fname VARCHAR(100)
```

After:

```sql
ALTER TABLE employee
ALTER COLUMN fname
SET DATA TYPE VARCHAR(10);
```

(Potentially fails)

Suppose the existing data is:

| fname |
| --- |
| Arun |
| Raj |
| Christopher |

Christopher has 11 characters.

The database cannot silently discard existing data to satisfy the smaller size.

The alteration will fail if existing values cannot be converted.

**Developer rule:** Before reducing column size, check existing data.

```sql
SELECT *
FROM employee
WHERE LENGTH(fname) > 10;
```

### Changing INTEGER to NUMERIC

```sql
ALTER TABLE employee
ALTER COLUMN salary
SET DATA TYPE NUMERIC(12,2);
```

The existing data must be convertible to the target type.

### Changing VARCHAR to INTEGER

```sql
ALTER TABLE employee
ALTER COLUMN emp_code
SET DATA TYPE INTEGER;
```

This may succeed if all existing values are valid integer representations.

If the column contains:

```text
101
102
ABC
103
```

The conversion fails because `ABC` cannot be converted to INTEGER.

**Important:** Changing a column's type is different from changing its name. The former converts existing data; the latter does not.

## 10.3 RENAME COLUMN

HSQLDB supports:

```sql
ALTER TABLE employee
ALTER COLUMN fname
RENAME TO first_name;
```

Before:

```text
fname
```

After:

```text
first_name
```

Existing data remains unchanged.

The table itself is not renamed.

## 10.4 DROP COLUMN

Syntax:

```sql
ALTER TABLE employee
DROP COLUMN department;
```

This permanently removes the department column and its stored values.

Example:

Before:

| emp_id | fname | department |
| --- | --- | --- |
| 1 | Arun | IT |
| 2 | Ravi | HR |

After:

| emp_id | fname |
| --- | --- |
| 1 | Arun |
| 2 | Ravi |

**Important:** If the column participates in a constraint, index, view or other dependent object, the operation may fail unless the required dependencies are removed or CASCADE is specified.

Example:

```sql
ALTER TABLE employee
DROP COLUMN department CASCADE;
```

CASCADE can remove dependent database objects as well. Use it carefully.

---

# 11. ALTER TABLE - Adding Constraints

You do not need to drop and recreate a table to add a constraint.

You can add constraints to an existing table.

General syntax:

```sql
ALTER TABLE table_name
ADD CONSTRAINT constraint_name
constraint_definition;
```

**Important:** Existing records must satisfy the new constraint. If even one existing row violates it, the ALTER operation fails.

Let's understand each constraint.

## 11.1 Adding NOT NULL

In HSQLDB, use `ALTER COLUMN ... SET NOT NULL`.

```sql
ALTER TABLE employee
ALTER COLUMN fname
SET NOT NULL;
```

Equivalent column property: the column cannot contain NULL.

If existing rows have NULL values, the operation fails.

Check first:

```sql
SELECT *
FROM employee
WHERE fname IS NULL;
```

To remove NOT NULL:

```sql
ALTER TABLE employee
ALTER COLUMN fname
SET NULL;
```

This makes the column nullable.

## 11.2 Adding PRIMARY KEY

```sql
ALTER TABLE employee
ADD CONSTRAINT pk_employee
PRIMARY KEY (emp_id);
```

Existing data must satisfy:

- No NULL values.
- No duplicate values.

If either condition is violated, the constraint cannot be added.

## 11.3 Adding composite PRIMARY KEY

```sql
ALTER TABLE student_marks
ADD CONSTRAINT pk_student_course
PRIMARY KEY (student_id, course_id);
```

The combination must be unique and neither column may contain NULL.

## 11.4 Adding UNIQUE

```sql
ALTER TABLE employee
ADD CONSTRAINT uq_email
UNIQUE (email);
```

Existing duplicate non-NULL email values prevent the constraint from being added.

Multiple NULL values are permitted.

## 11.5 Adding composite UNIQUE

```sql
ALTER TABLE student_marks
ADD CONSTRAINT uq_student_course
UNIQUE (student_id, course_id);
```

The combination must be unique.

## 11.6 Adding CHECK

```sql
ALTER TABLE employee
ADD CONSTRAINT chk_salary
CHECK (salary >= 0);
```

Existing negative salary values cause the operation to fail.

## 11.7 Adding FOREIGN KEY

```sql
ALTER TABLE student_marks
ADD CONSTRAINT fk_student
FOREIGN KEY (student_id)
REFERENCES student(student_id);
```

Existing child records must reference existing parent records, except that nullable foreign keys can contain NULL.

## 11.8 Adding DEFAULT

In HSQLDB, a default is set using `ALTER COLUMN ... SET DEFAULT`, not `ADD CONSTRAINT`.

```sql
ALTER TABLE employee
ALTER COLUMN status
SET DEFAULT 'ACTIVE';
```

To remove the default:

```sql
ALTER TABLE employee
ALTER COLUMN status
DROP DEFAULT;
```

**Important:** Setting a default does not automatically update existing rows.

---

# 12. ALTER TABLE - Dropping Constraints

A named constraint can be removed using:

```sql
ALTER TABLE table_name
DROP CONSTRAINT constraint_name;
```

Example:

```sql
ALTER TABLE employee
DROP CONSTRAINT uq_email;
```

This removes the UNIQUE constraint.

It does not delete the email column or existing email values.

### Removing different constraints

| Constraint | Example |
| --- | --- |
| UNIQUE | `DROP CONSTRAINT uq_email` |
| PRIMARY KEY | `DROP CONSTRAINT pk_employee` |
| CHECK | `DROP CONSTRAINT chk_salary` |
| FOREIGN KEY | `DROP CONSTRAINT fk_student` |

Example:

```sql
ALTER TABLE student_marks
DROP CONSTRAINT fk_student;
```

The student ID column remains, but the referential integrity restriction is removed.

### Important dependency scenario

Suppose:

- STUDENT has a primary key.
- STUDENT_MARKS references it through a foreign key.

You cannot simply remove the referenced primary key while the foreign key depends on it.

You need to remove the child foreign key first, or use an appropriate CASCADE operation.

HSQLDB supports:

```sql
ALTER TABLE student
DROP CONSTRAINT pk_student CASCADE;
```

This can remove dependent foreign-key constraints, but it does not drop the child table itself.

---

# 13. DROP TABLE

`DROP TABLE` permanently removes a table.

Syntax:

```sql
DROP TABLE table_name;
```

Example:

```sql
DROP TABLE employee;
```

What gets deleted?

1. Table structure.
2. Columns.
3. Rows.
4. Constraints belonging to the table.
5. Associated indexes and table objects.

After dropping the table:

```sql
SELECT *
FROM employee;
```

Produces an error because the table no longer exists.

### 13.1 DROP TABLE IF EXISTS

```sql
DROP TABLE IF EXISTS employee;
```

If the table exists, it is dropped.

If the table does not exist, the statement does not raise the usual missing-table error.

### 13.2 Dropping a parent table without references

Suppose:

```sql
CREATE TABLE student (
    student_id INTEGER PRIMARY KEY
);
```

No child table references it.

Then:

```sql
DROP TABLE student;
```

(Success)

### 13.3 Dropping a parent table with a foreign-key reference

Suppose:

```sql
CREATE TABLE student (
    student_id INTEGER PRIMARY KEY
);
```

```sql
CREATE TABLE student_marks (
    student_id INTEGER,

    FOREIGN KEY (student_id)
    REFERENCES student(student_id)
);
```

Now:

```sql
DROP TABLE student;
```

(Fails by default)

Why?

The STUDENT table is referenced by a foreign key in STUDENT_MARKS.

### Solution 1: Drop the child table first

```sql
DROP TABLE student_marks;

DROP TABLE student;
```

This is the straightforward approach.

### Solution 2: Use CASCADE

```sql
DROP TABLE student CASCADE;
```

This drops the parent table and removes the referencing foreign-key constraint from the child table.

**Critical interview distinction:**

`DROP TABLE student CASCADE` does NOT automatically drop the entire STUDENT_MARKS table just because it references STUDENT.

The child table remains, but its foreign-key constraint is removed.

Other dependent objects, such as referencing views, may be dropped as well.

---

# 14. TRUNCATE TABLE

TRUNCATE removes all rows from a table while preserving its structure.

Syntax:

```sql
TRUNCATE TABLE employee;
```

After execution:

- Table remains.
- Columns remain.
- Constraints remain.
- Indexes remain.
- All records are removed.

Example:

Before:

| emp_id | fname |
| --- | --- |
| 1 | Arun |
| 2 | Ravi |
| 3 | Kumar |

Execute:

```sql
TRUNCATE TABLE employee;
```

After:

| emp_id | fname |
| --- | --- |
| No records |  |

The table still exists.

You can insert new rows afterwards.

## 14.1 DELETE versus TRUNCATE versus DROP

This is a very common interview question.

| Feature | DELETE | TRUNCATE | DROP |
| --- | --- | --- | --- |
| Removes rows | Yes | Yes, all | Yes |
| Removes table | No | No | Yes |
| Removes columns | No | No | Yes |
| WHERE condition | Yes | No | No |
| Structure remains | Yes | Yes | No |
| Constraints remain | Yes | Yes | No |
| Can delete selected records | Yes | No | No |

### DELETE example

```sql
DELETE FROM employee
WHERE emp_id = 101;
```

Only employee 101 is removed.

### TRUNCATE example

```sql
TRUNCATE TABLE employee;
```

All rows are removed.

### DROP example

```sql
DROP TABLE employee;
```

The table itself is removed.

## 14.2 TRUNCATE and foreign keys

Suppose STUDENT is referenced by STUDENT_MARKS.

```sql
TRUNCATE TABLE student;
```

HSQLDB does not permit truncating a referenced parent table when the relevant child table contains rows.

You must first clear the referencing child rows or otherwise resolve the relationship.

Example:

```sql
TRUNCATE TABLE student_marks;

TRUNCATE TABLE student;
```

## 14.3 TRUNCATE and identity columns

HSQLDB supports two options:

```sql
TRUNCATE TABLE employee RESTART IDENTITY;
```

Resets identity generation to its starting value.

```sql
TRUNCATE TABLE employee CONTINUE IDENTITY;
```

Preserves the identity sequence progression.

Example:

Suppose the last generated employee ID was 105.

After truncating with RESTART IDENTITY, the next generated value starts from the sequence's configured starting value.

With CONTINUE IDENTITY, it continues the existing sequence.

## 14.4 TRUNCATE AND COMMIT

HSQLDB also supports:

```sql
TRUNCATE TABLE employee AND COMMIT;
```

This form commits the transaction and performs the truncate operation without the ordinary row-by-row deletion process.

`TRUNCATE` should not be treated as universally equivalent to `DELETE FROM table`; transaction and trigger behaviour differ.

---

# 15. Advanced DDL Edge Cases - Interview Revision Table

Before attempting the quiz, understand these scenarios.

| Scenario | Expected behaviour |
| --- | --- |
| Insert NULL into NOT NULL | Error |
| Insert empty string into NOT NULL VARCHAR | Success |
| Insert spaces into NOT NULL VARCHAR | Success |
| Insert NULL into PRIMARY KEY | Error |
| Insert duplicate PRIMARY KEY | Error |
| Insert NULL into nullable UNIQUE | Success |
| Insert duplicate non-NULL UNIQUE | Error |
| Insert NULL into CHECK(age >= 18) | Success |
| Insert age 15 into CHECK(age >= 18) | Error |
| Insert valid parent ID into FK | Success |
| Insert nonexistent parent ID into FK | Error |
| Insert NULL into nullable FK | Success |
| Omit DEFAULT column | Default applied |
| Explicitly insert NULL into DEFAULT column | NULL, not default |
| Add CHECK when existing data violates it | Error |
| Add PRIMARY KEY when duplicates exist | Error |
| Add NOT NULL when existing NULLs exist | Error |
| Drop parent table with FK reference | Error by default |
| Drop parent table CASCADE | Parent and dependent FK constraint removed |
| Truncate table | All rows removed, structure retained |
| Drop table | Structure and records removed |

# 16. Complete Practical Example - Student Database

Let's combine all six constraint types in one practical schema.

## Parent table: STUDENT

```sql
CREATE TABLE student (
    student_id INTEGER,
    student_name VARCHAR(50) NOT NULL,
    email VARCHAR(100),
    age INTEGER,
    status VARCHAR(20) DEFAULT 'ACTIVE',

    CONSTRAINT pk_student
        PRIMARY KEY (student_id),

    CONSTRAINT uq_student_email
        UNIQUE (email),

    CONSTRAINT chk_student_age
        CHECK (age >= 18)
);
```

## Parent table: COURSE

```sql
CREATE TABLE course (
    course_id INTEGER PRIMARY KEY,
    course_name VARCHAR(50) UNIQUE NOT NULL
);
```

## Child table: STUDENT_MARKS

```sql
CREATE TABLE student_marks (
    student_id INTEGER,
    course_id INTEGER,
    marks NUMERIC(5,2),

    CONSTRAINT pk_student_marks
        PRIMARY KEY (student_id, course_id),

    CONSTRAINT fk_marks_student
        FOREIGN KEY (student_id)
        REFERENCES student(student_id),

    CONSTRAINT fk_marks_course
        FOREIGN KEY (course_id)
        REFERENCES course(course_id),

    CONSTRAINT chk_marks
        CHECK (marks BETWEEN 0 AND 100)
);
```

### Insert sample data

```sql
INSERT INTO student
VALUES (101, 'Arun', 'arun@gmail.com', 22, DEFAULT);

INSERT INTO course
VALUES (10, 'Java');

INSERT INTO course
VALUES (20, 'SQL');

INSERT INTO student_marks
VALUES (101, 10, 95);

INSERT INTO student_marks
VALUES (101, 20, 88);
```

All five INSERT statements succeed.

### Now test these statements

| Statement | Expected |
| --- | --- |
| Insert student ID 101 again | Error - PK |
| Insert duplicate email | Error - UNIQUE |
| Insert age 15 | Error - CHECK |
| Insert age NULL | Allowed by CHECK |
| Insert student ID 999 into marks | Error - FK |
| Insert student ID 101 and course ID 10 again | Error - Composite PK |
| Insert marks 105 | Error - CHECK |
| Insert NULL marks | Allowed by CHECK |
| Delete student 101 while marks exist | Error - FK |
| Delete student 101 after deleting marks | Success |

Notice that age NULL and marks NULL are allowed because CHECK alone does not reject UNKNOWN.

---

# 17. Advanced MCQ Quiz - 15 Questions

(2-year SQL developer assessment)

These questions test syntax, constraints, referential integrity, DDL operations and edge cases.

**DDL & Constraints Assessment** (/15 answered)

# 18. Final Revision Checklist

For a two-year SQL developer, make sure you can independently perform all these operations.



## Official HSQLDB documentation

For HSQLDB-specific syntax and behaviour:

- HyperSQL User Guide - Table Creation, ALTER and DROP.
- HyperSQL 2.7.4 - Database Guide PDF.
- HyperSQL SQL Features and Compatibility.

**My recommendation:** Pay particular attention to the following five tricky areas:

1. CHECK constraints allow UNKNOWN but reject FALSE.
2. UNIQUE permits multiple NULL values in HSQLDB.
3. Composite primary keys enforce uniqueness on the combination, not on individual columns.
4. ALTER TABLE validates existing records when adding constraints or changing column definitions.
5. DROP TABLE CASCADE removes dependent foreign-key constraints but does not automatically drop the referencing child table.

These are excellent areas to practise because they test actual database behaviour rather than just SQL syntax.

### User

for 2 year sql developer hsql database level give concepts needed from required topics all tricky advanced topics from these explanation and 15 question quiz at end all edge cases insert statement is used to add tuples into the table insert statement syntax 3 types: 1: if column name not specified after insert cause then vaue must be specified in rder of specification during tabe creation, insert statment 2: if cumns are specified in insert clause then in values clause as per order of insert clause, insert statement 3: mutipe rws can be inserted when it is used with seect statemnt insert statement 4: inserting multiple rows with , , if column is of string date date time time must be enclosed in single quotes, string data case sensitive null not to be enclosed within quotes, if only values written and column nt mentined all column values must be specified if unknwn column must be null, shoud be in correct order, values must be specified for all columns of table any missing value will result in faulure , insertin will fai due to constraint violation also, null can be omitted if columns specfied and value not specified, comitting default can be done if column speciied if column not specified then do we have to specift value or default value will be given, can insert null values in uniqu constraint column and multiple null values can be inserted, insertion will fail if foreign key insertion for which it is not in parent table, cannot insert null value in primarky key column and cannt insert duplicate value in primary key column, update statement: update all rows, update single row, update single column, update multiple column where optional, duplicate column update what will happen will update fail update emp set s=100,s=200, multiple conditions in where , value of column with not null constraint cannot be updaet to null, all column in table including primary key can be updated using update statement, update fails if primarky key violated, check constraint violation, unique key violation, any attempt to update a record with value do not exist in referencd table will result in failure, attempt made to update value in master table that is referenced in child table will lead to foreign key in update violation, delete from employee deletes all rows, delete with where delete specfici rows, trunate statement more efficient than delete from table;, delete filter from single row, filter multiple rows, foreign key violation, select all rows columns, select all rows specific column select specific column specific rows where select clause with alias name, select clause withiut comma between 2 columns make model only model shown, select clause with expression select price*0.25 as "discount", where comparions > opearator, and operator, or operator between operator, where in opeator example where null comparios is null is not null, strings compariosn same size string, compare different size string with traiing space 'pm  ' can match pm, leading spaces cant be matched with 'pm', select clause with distinct,remove duplicate from multiple column, use distinct to remove duplicate null values, distinct cannot be used in between columns, count(distinct column), like start pattern 'e%', end pattern '%e', anywhere pattern '%m%' like fixed date pattern fixed position pattern character a at second position, order of query execution give give all explain briefly all

### ChatGPT

# HSQLDB - Advanced DML, SELECT and Data Manipulation Guide

(2-Year SQL Developer Level) (15 MCQ Quiz)

This guide covers four major areas of SQL development:

1. **INSERT** - inserting single and multiple records, defaults, NULLs and constraint violations.
2. **UPDATE** - updating individual columns, multiple columns, multiple records and handling constraint violations.
3. **DELETE and TRUNCATE** - deleting selected records, deleting all records and understanding foreign-key restrictions.
4. **SELECT** - retrieving records, filtering, aliases, expressions, DISTINCT, LIKE, NULL comparisons and query execution order.

The focus is on tricky scenarios, especially what happens when a statement violates constraints or encounters NULL values.

# 1. INSERT Statement

The `INSERT` statement is a DML command used to add new rows (tuples) to an existing table.

A table can contain zero or more rows. INSERT adds new rows without changing the table structure.

## 1.1 Three important INSERT formats

### Type 1: INSERT without specifying column names

Syntax:

```sql
INSERT INTO table_name
VALUES (value1, value2, value3);
```

Example:

```sql
CREATE TABLE employee (
    emp_id INTEGER,
    fname VARCHAR(30),
    salary NUMERIC(10,2),
    department VARCHAR(30)
);
```

Insert:

```sql
INSERT INTO employee
VALUES (101, 'Arun', 45000, 'IT');
```

Here, values must be supplied in the exact order in which columns were defined during table creation.

The mapping is:

| Column | Inserted value |
| --- | --- |
| emp_id | 101 |
| fname | Arun |
| salary | 45000 |
| department | IT |

**Important rules:**

- All columns must have corresponding values.
- Values must follow the table's column-definition order.
- Data types must be compatible.
- You cannot skip a column in the middle.
- Constraints must be satisfied.

Example of an incorrect INSERT:

```sql
INSERT INTO employee
VALUES (101, 45000, 'Arun', 'IT');
```

(Error)

The second value is being assigned to `fname`, which is a VARCHAR column. The third value is assigned to `salary`.

The order is incorrect.

### Type 2: INSERT with specified column names

Syntax:

```sql
INSERT INTO table_name (column1, column2)
VALUES (value1, value2);
```

Example:

```sql
INSERT INTO employee (emp_id, fname)
VALUES (102, 'Ravi');
```

Result:

| emp_id | fname | salary | department |
| --- | --- | --- | --- |
| 102 | Ravi | NULL | NULL |

The omitted columns receive their default values, or NULL if no default is defined.

This is one of the most useful INSERT formats in real-world development.

**Important rules:**

- Values must follow the order of the column list in the INSERT statement.
- You do not need to specify every column.
- Omitted columns receive their defaults or NULL.
- NOT NULL and other constraints still apply.

Example:

```sql
INSERT INTO employee (fname, emp_id)
VALUES ('Kumar', 103);
```

This is valid.

Notice that the order is different from the table definition. The database uses the INSERT column list to determine the mapping.

### Type 3: INSERT using SELECT

Used to insert the result of a SELECT query into another table.

Syntax:

```sql
INSERT INTO target_table (column1, column2)
SELECT source_column1, source_column2
FROM source_table
WHERE condition;
```

Example:

```sql
INSERT INTO employee_backup (emp_id, fname)
SELECT emp_id, fname
FROM employee
WHERE department = 'IT';
```

All employees from IT are copied into `employee_backup`.

Important rules:

1. The number of selected expressions must match the number of target columns.
2. The corresponding data types must be compatible.
3. The order of SELECT expressions must match the target column order.
4. Constraints on the target table must be satisfied.
5. The SELECT query can return zero, one or multiple rows.

Example of an invalid statement:

```sql
INSERT INTO employee_backup (emp_id, fname)
SELECT fname, emp_id
FROM employee;
```

(Potential type conversion error)

The SELECT expression order does not match the target columns.

## 1.2 INSERT multiple rows using VALUES

HSQLDB also supports inserting multiple rows in one statement.

Syntax:

```sql
INSERT INTO table_name
VALUES
(value1, value2),
(value1, value2),
(value1, value2);
```

Example:

```sql
INSERT INTO employee
(emp_id, fname, salary, department)
VALUES
(101, 'Arun', 45000, 'IT'),
(102, 'Ravi', 50000, 'HR'),
(103, 'Kumar', 55000, 'IT');
```

Three records are inserted using one INSERT statement.

(Multi-row INSERT supported)

**Important:** If any row violates a constraint or cannot be converted to the target data type, the statement fails. Do not assume that valid rows will be committed individually.

---

# 2. INSERT - Data Types and Value Representation

When inserting data, the value must be compatible with the target column.

| Data type | Example |
| --- | --- |
| INTEGER | `101` |
| NUMERIC | `45000.50` |
| VARCHAR | `'Arun'` |
| CHAR | `'A'` |
| DATE | `DATE '2026-11-08'` |
| TIME | `TIME '10:30:00'` |
| TIMESTAMP | `TIMESTAMP '2026-11-08 10:30:00'` |
| BOOLEAN | `TRUE` |
| NULL | `NULL` |

### 2.1 String values

Strings must be enclosed in single quotes.

```sql
INSERT INTO employee
VALUES (101, 'Arun', 45000, 'IT');
```

Incorrect:

```sql
INSERT INTO employee
VALUES (101, Arun, 45000, IT);
```

The database will interpret unquoted words as identifiers rather than string literals.

### 2.2 Date values

You can use SQL date literals:

```sql
INSERT INTO employee_details
VALUES (101, DATE '2026-11-08');
```

You can also use compatible character-to-date conversion:

```sql
INSERT INTO employee_details
VALUES (102, '2026-11-08');
```

The latter depends on successful implicit conversion.

Prefer the DATE literal for predictable behaviour.

### 2.3 NULL values

NULL must not be enclosed in single quotes.

Correct:

```sql
INSERT INTO employee
VALUES (101, 'Arun', NULL, 'IT');
```

Incorrect:

```sql
INSERT INTO employee
VALUES (101, 'Arun', 'NULL', 'IT');
```

The second statement inserts the text `NULL`, not a database NULL.

### 2.4 Case sensitivity of strings

Consider:

```sql
INSERT INTO employee
VALUES (101, 'Arun', 45000, 'IT');
```

The strings `'Arun'`, `'ARUN'` and `'arun'` are different character representations.

However, whether comparisons treat them as equal depends on the database collation and HSQLDB's case-insensitive comparison setting.

Under the default HSQLDB configuration, VARCHAR comparisons are case-sensitive.

Example:

```sql
SELECT *
FROM employee
WHERE fname = 'arun';
```

This does not match `'Arun'` under the default case-sensitive comparison.

### 2.5 What happens if you do not specify columns?

Consider:

```sql
CREATE TABLE employee (
    emp_id INTEGER,
    fname VARCHAR(30),
    salary INTEGER,
    status VARCHAR(20) DEFAULT 'ACTIVE'
);
```

You execute:

```sql
INSERT INTO employee
VALUES (101, 'Arun', 45000);
```

(Error)

Four columns exist, but only three values are supplied.

You must either:

```sql
INSERT INTO employee
VALUES (101, 'Arun', 45000, DEFAULT);
```

Or:

```sql
INSERT INTO employee (emp_id, fname, salary)
VALUES (101, 'Arun', 45000);
```

The second statement automatically uses the default for status.

**Remember:**

- No column list: supply one value for every column.
- Column list: supply one value for every listed column.
- Omitted columns receive DEFAULT or NULL.
- Explicit NULL is not the same as omitting a column.

# 3. Multiple INSERT Edge Cases

These are important for interviews and practical SQL examinations.

Consider:

```sql
CREATE TABLE employee (
    emp_id INTEGER PRIMARY KEY,
    fname VARCHAR(30) NOT NULL,
    salary INTEGER DEFAULT 30000,
    email VARCHAR(100) UNIQUE
);
```

## 3.1 Omitting a column with DEFAULT

```sql
INSERT INTO employee (emp_id, fname, email)
VALUES (101, 'Arun', 'arun@gmail.com');
```

Result:

| emp_id | fname | salary | email |
| --- | --- | --- | --- |
| 101 | Arun | 30000 | arun@gmail.com |

The omitted salary column receives its DEFAULT value.

## 3.2 Explicitly inserting NULL

```sql
INSERT INTO employee
VALUES (102, 'Ravi', NULL, 'ravi@gmail.com');
```

Result:

| emp_id | fname | salary | email |
| --- | --- | --- | --- |
| 102 | Ravi | NULL | ravi@gmail.com |

The DEFAULT value is not applied because NULL was explicitly supplied.

## 3.3 Using DEFAULT explicitly

```sql
INSERT INTO employee
VALUES (103, 'Kumar', DEFAULT, 'kumar@gmail.com');
```

Salary becomes 30000.

## 3.4 Inserting only some columns

```sql
INSERT INTO employee (emp_id, fname)
VALUES (104, 'Suresh');
```

This works because:

- emp_id is supplied.
- fname is supplied.
- salary receives its DEFAULT.
- email receives NULL.

## 3.5 Inserting without any values

```sql
INSERT INTO employee
DEFAULT VALUES;
```

(Error in this table)

Why?

- emp_id has no default and is part of the primary key.
- fname is NOT NULL and has no default.

Both prevent the insertion.

## 3.6 Multiple NULLs in UNIQUE columns

```sql
INSERT INTO employee
VALUES (105, 'Ajay', 30000, NULL);

INSERT INTO employee
VALUES (106, 'Vijay', 30000, NULL);
```

(Both succeed)

HSQLDB allows multiple NULLs in a UNIQUE column.

But:

```sql
INSERT INTO employee
VALUES (107, 'Manoj', 30000, 'ajay@gmail.com');
```

This fails if that email already exists.

## 3.7 Foreign key insertion violation

Parent:

```sql
CREATE TABLE department (
    dept_id INTEGER PRIMARY KEY,
    dept_name VARCHAR(30)
);
```

Child:

```sql
CREATE TABLE employee_dept (
    emp_id INTEGER PRIMARY KEY,
    dept_id INTEGER,

    FOREIGN KEY (dept_id)
    REFERENCES department(dept_id)
);
```

Insert parent:

```sql
INSERT INTO department
VALUES (10, 'IT');
```

Valid child insertion:

```sql
INSERT INTO employee_dept
VALUES (101, 10);
```

Invalid child insertion:

```sql
INSERT INTO employee_dept
VALUES (102, 99);
```

The department ID 99 does not exist in the parent table.

The foreign-key constraint rejects the insertion.

---

# 4. UPDATE Statement

UPDATE is a DML command used to modify existing records in a table.

It can update:

- A single column.
- Multiple columns.
- A single row.
- Multiple rows.
- Every row in a table.

## 4.1 Basic UPDATE syntax

```sql
UPDATE table_name
SET column_name = value
WHERE condition;
```

Example:

```sql
UPDATE employee
SET salary = 50000
WHERE emp_id = 101;
```

Only the employee with ID 101 is updated.

## 4.2 Updating a single row and single column

```sql
UPDATE employee
SET fname = 'Arun Kumar'
WHERE emp_id = 101;
```

Only fname changes.

All other columns retain their previous values.

## 4.3 Updating multiple columns

Syntax:

```sql
UPDATE table_name
SET
    column1 = value1,
    column2 = value2
WHERE condition;
```

Example:

```sql
UPDATE employee
SET
    salary = 60000,
    fname = 'Arun',
    email = 'arun_new@gmail.com'
WHERE emp_id = 101;
```

All three columns are updated for the matching row.

## 4.4 Updating multiple rows

```sql
UPDATE employee
SET salary = salary + 5000
WHERE department = 'IT';
```

Every employee in the IT department receives a salary increase of 5000.

Suppose the table contains:

| emp_id | department | salary |
| --- | --- | --- |
| 101 | IT | 40000 |
| 102 | IT | 50000 |
| 103 | HR | 45000 |

After execution:

| emp_id | department | salary |
| --- | --- | --- |
| 101 | IT | 45000 |
| 102 | IT | 55000 |
| 103 | HR | 45000 |

## 4.5 UPDATE without WHERE

This is one of the most important edge cases.

```sql
UPDATE employee
SET salary = 50000;
```

(Updates every row)

Every employee receives a salary of 50000.

The WHERE clause is optional, but omitting it means there is no row-level filtering.

**Developer rule:** Always verify the WHERE condition before executing an UPDATE on production data.

## 4.6 UPDATE with multiple WHERE conditions

```sql
UPDATE employee
SET salary = 60000
WHERE department = 'IT'
AND salary < 50000;
```

Both conditions must be TRUE.

Another example:

```sql
UPDATE employee
SET salary = 60000
WHERE department = 'IT'
OR department = 'HR';
```

Employees from either department are updated.

### Complex conditions

```sql
UPDATE employee
SET salary = salary * 1.10
WHERE (department = 'IT' OR department = 'HR')
AND salary < 100000;
```

Parentheses determine which conditions are grouped.

---

# 5. UPDATE - Important Tricky Scenarios

## 5.1 Updating a NOT NULL column to NULL

Assume:

```sql
fname VARCHAR(30) NOT NULL
```

Execute:

```sql
UPDATE employee
SET fname = NULL
WHERE emp_id = 101;
```

(Error)

The NOT NULL constraint is violated.

## 5.2 Updating a PRIMARY KEY

Can a primary key be updated?

**Yes.**

A primary key is not immutable. It can be updated as long as the new value satisfies all applicable constraints.

Example:

```sql
UPDATE employee
SET emp_id = 200
WHERE emp_id = 101;
```

(Can succeed)

Provided:

- 200 does not already exist.
- No other constraint is violated.
- No referencing foreign key prevents the update.

### What if the new primary key already exists?

Suppose employee IDs 101 and 102 exist.

```sql
UPDATE employee
SET emp_id = 102
WHERE emp_id = 101;
```

(Error)

A duplicate primary key is created.

## 5.3 Updating a UNIQUE column to an existing value

```sql
UPDATE employee
SET email = 'ravi@gmail.com'
WHERE emp_id = 101;
```

If another employee already has that email, the update fails.

The UNIQUE constraint is checked after the proposed modification.

## 5.4 Updating a CHECK-constrained column

Suppose:

```sql
salary INTEGER CHECK (salary >= 0)
```

Execute:

```sql
UPDATE employee
SET salary = -5000
WHERE emp_id = 101;
```

(Error)

The new value violates the CHECK condition.

## 5.5 Updating a foreign-key column

Suppose employee_dept references department.

```sql
UPDATE employee_dept
SET dept_id = 99
WHERE emp_id = 101;
```

If department 99 does not exist:

(Error)

The foreign-key constraint is violated.

## 5.6 Updating the parent key referenced by a child

Consider:

DEPARTMENT:

| dept_id | dept_name |
| --- | --- |
| 10 | IT |
| 20 | HR |

EMPLOYEE_DEPT:

| emp_id | dept_id |
| --- | --- |
| 101 | 10 |
| 102 | 20 |

Now execute:

```sql
UPDATE department
SET dept_id = 100
WHERE dept_id = 10;
```

(Error by default)

Why?

Employee 101 references department 10.

Changing the parent key would leave the child foreign key pointing to a nonexistent parent key.

### Solution: ON UPDATE CASCADE

Define the foreign key as:

```sql
FOREIGN KEY (dept_id)
REFERENCES department(dept_id)
ON UPDATE CASCADE
```

Now updating department 10 to 100 automatically changes the referencing child rows from 10 to 100.

Other possible actions include `ON UPDATE SET NULL` and `ON UPDATE SET DEFAULT`, subject to their requirements.

## 5.7 Updating the same column twice

Consider:

```sql
UPDATE employee
SET salary = 10000,
    salary = 20000
WHERE emp_id = 101;
```

(Invalid assignment list)

Do not assign the same target column twice in one UPDATE statement.

Use:

```sql
UPDATE employee
SET salary = 20000
WHERE emp_id = 101;
```

If you need a calculation, use one assignment:

```sql
UPDATE employee
SET salary = salary + 10000
WHERE emp_id = 101;
```

## 5.8 UPDATE with NULL conditions

Incorrect:

```sql
UPDATE employee
SET salary = 0
WHERE department = NULL;
```

Correct:

```sql
UPDATE employee
SET salary = 0
WHERE department IS NULL;
```

NULL comparison requires `IS NULL`.

## 5.9 UPDATE with CASE

This is an important developer-level operation.

```sql
UPDATE employee
SET salary =
    CASE
        WHEN department = 'IT' THEN salary * 1.10
        WHEN department = 'HR' THEN salary * 1.05
        ELSE salary
    END;
```

Different employees receive different salary updates in one statement.

## 5.10 UPDATE with DEFAULT

HSQLDB supports setting a column back to its default.

```sql
UPDATE employee
SET status = DEFAULT
WHERE emp_id = 101;
```

This does not mean NULL. It uses the column's defined default value.

---

# 6. DELETE Statement

DELETE is used to remove records from a table.

It does not remove the table structure.

## 6.1 DELETE all records

Syntax:

```sql
DELETE FROM table_name;
```

Example:

```sql
DELETE FROM employee;
```

All records are deleted.

The table remains available for future INSERT operations.

## 6.2 DELETE a single row

```sql
DELETE FROM employee
WHERE emp_id = 101;
```

Only employee 101 is deleted.

## 6.3 DELETE multiple rows

```sql
DELETE FROM employee
WHERE department = 'IT';
```

All IT department records are deleted.

## 6.4 DELETE using multiple conditions

```sql
DELETE FROM employee
WHERE department = 'IT'
AND salary < 30000;
```

Only IT employees whose salaries are below 30000 are deleted.

## 6.5 DELETE using BETWEEN

```sql
DELETE FROM employee
WHERE salary BETWEEN 20000 AND 30000;
```

Both boundary values are included.

## 6.6 DELETE without WHERE versus DELETE with WHERE

| Query | Result |
| --- | --- |
| `DELETE FROM employee` | Deletes all records |
| `DELETE FROM employee WHERE emp_id = 101` | Deletes one matching ID |
| `DELETE FROM employee WHERE department = 'IT'` | Deletes matching IT records |
| `DELETE FROM employee WHERE 1=0` | Deletes no records |
| `DELETE FROM employee WHERE 1=1` | Deletes all records |

## 6.7 Foreign-key violation during DELETE

Suppose DEPARTMENT is the parent table and EMPLOYEE_DEPT is the child table.

If department 10 is referenced by an employee:

```sql
DELETE FROM department
WHERE dept_id = 10;
```

(Error by default)

The parent row cannot be deleted because child rows reference it.

Possible solutions:

**Solution 1: Delete the child first**

```sql
DELETE FROM employee_dept
WHERE dept_id = 10;

DELETE FROM department
WHERE dept_id = 10;
```

**Solution 2: Define ON DELETE CASCADE**

```sql
FOREIGN KEY (dept_id)
REFERENCES department(dept_id)
ON DELETE CASCADE
```

Now deleting department 10 automatically deletes related employee-department records.

**Important:** DELETE from a child table does not delete the parent record.

---

# 7. DELETE versus TRUNCATE

You have already covered the basic distinction, but understand the performance and transaction differences.

| Feature | DELETE | TRUNCATE |
| --- | --- | --- |
| Removes all records | Yes, without WHERE | Yes |
| Supports WHERE | Yes | No |
| Table remains | Yes | Yes |
| Structure remains | Yes | Yes |
| Constraints remain | Yes | Yes |
| Can delete selected rows | Yes | No |
| Referential restrictions | Yes | Yes, with additional restrictions |
| Identity handling | Generally continues | Can restart or continue |
| Row-level DELETE triggers | Can fire | Not equivalent to row-by-row DELETE |

### Why is TRUNCATE generally more efficient?

DELETE processes row deletions and associated row-level operations.

TRUNCATE is a bulk table operation. It avoids the ordinary row-by-row deletion process and can be more efficient when removing an entire table's contents.

However, actual performance depends on table size, indexes, foreign keys, transaction logging and database implementation.

**Interview trap:** TRUNCATE is not universally faster in every situation, and it is not universally non-rollbackable. HSQLDB has its own transaction behaviour and supports the `AND COMMIT` variant.

---

# 8. SELECT Statement

SELECT is used to retrieve data from tables.

It is the most frequently used SQL command.

## 8.1 Selecting all columns and all rows

```sql
SELECT *
FROM employee;
```

`*` represents all columns.

This returns every row and every column.

## 8.2 Selecting specific columns

```sql
SELECT emp_id, fname
FROM employee;
```

Returns only the specified columns.

All rows are returned unless a filtering condition is provided.

## 8.3 Selecting specific columns and specific rows

```sql
SELECT emp_id, fname
FROM employee
WHERE salary > 50000;
```

This returns employee ID and name only for employees earning more than 50000.

**Important distinction:**

- SELECT determines which columns are returned.
- WHERE determines which rows are returned.

This is called projection and selection respectively.

## 8.4 SELECT with aliases

Aliases temporarily rename columns in the query result.

Syntax:

```sql
SELECT column_name AS alias_name
FROM table_name;
```

Example:

```sql
SELECT
    emp_id AS employee_id,
    fname AS employee_name
FROM employee;
```

The underlying table structure does not change.

You can also omit AS:

```sql
SELECT fname employee_name
FROM employee;
```

Both are valid.

### Quoted aliases

```sql
SELECT fname AS "Employee Name"
FROM employee;
```

Double quotes allow spaces and preserve the specified identifier case in the result label.

---

# 9. SELECT Without a Comma Between Columns

This is an important syntax trap.

Consider:

```sql
SELECT fname salary
FROM employee;
```

You might expect two columns, but this is interpreted as:

```sql
SELECT fname AS salary
FROM employee;
```

The result contains only one column, with the output label `salary`.

It does NOT return fname and salary separately.

Correct syntax:

```sql
SELECT fname, salary
FROM employee;
```

**Remember:** A comma separates SELECT expressions. A space can separate an expression from its alias.

---

# 10. SELECT with Expressions and Calculations

You can perform calculations directly inside SELECT.

Example:

```sql
SELECT
    emp_id,
    salary,
    salary * 0.25 AS discount
FROM employee;
```

Suppose salary is 40000.

The result is:

| emp_id | salary | discount |
| --- | --- | --- |
| 101 | 40000 | 10000 |

The discount column is calculated when the query executes.

It is not automatically stored in the original table.

### More examples

```sql
SELECT
    salary,
    salary + 5000 AS revised_salary,
    salary * 12 AS annual_salary
FROM employee;
```

### Expression involving multiple columns

```sql
SELECT
    product_name,
    price,
    quantity,
    price * quantity AS total_amount
FROM sales;
```

### Expression with NULL

Suppose salary is NULL.

```sql
SELECT salary + 5000
FROM employee;
```

The result is NULL.

Arithmetic involving NULL normally produces NULL.

Use:

```sql
SELECT COALESCE(salary, 0) + 5000
FROM employee;
```

This substitutes zero for NULL before calculating.

---

# 11. WHERE Clause - Filtering Records

WHERE filters rows based on a condition.

Syntax:

```sql
SELECT column_list
FROM table_name
WHERE condition;
```

Consider this employee table:

| emp_id | fname | department | salary |
| --- | --- | --- | --- |
| 101 | Arun | IT | 50000 |
| 102 | Ravi | HR | 35000 |
| 103 | Kumar | IT | 60000 |
| 104 | Suresh | Finance | 45000 |
| 105 | Ajay | HR | NULL |

## 11.1 Comparison operators

| Operator | Meaning |
| --- | --- |
| `=` | Equal to |
| `<>` | Not equal to |
| `!=` | Not equal to |
| `>` | Greater than |
| `<` | Less than |
| `>=` | Greater than or equal |
| `<=` | Less than or equal |

Examples:

```sql
SELECT *
FROM employee
WHERE salary > 40000;
```

Returns Arun, Kumar and Suresh.

```sql
SELECT *
FROM employee
WHERE department <> 'IT';
```

Returns HR and Finance employees, excluding rows with NULL department values.

### Important: String comparisons

```sql
SELECT *
FROM employee
WHERE fname = 'Arun';
```

The comparison depends on the column's collation and case-sensitivity configuration.

Under default case-sensitive settings, `'Arun'` and `'arun'` are different.

---

# 12. WHERE with AND and OR

## 12.1 AND operator

Both conditions must be TRUE.

```sql
SELECT *
FROM employee
WHERE department = 'IT'
AND salary > 50000;
```

Returns employees who belong to IT AND earn more than 50000.

## 12.2 OR operator

At least one condition must be TRUE.

```sql
SELECT *
FROM employee
WHERE department = 'IT'
OR department = 'HR';
```

Returns employees belonging to either IT or HR.

## 12.3 AND and OR together

```sql
SELECT *
FROM employee
WHERE department = 'IT'
AND salary > 40000
OR department = 'HR';
```

Equivalent to:

```sql
WHERE (department = 'IT' AND salary > 40000)
OR department = 'HR';
```

AND has higher precedence than OR.

For clarity, always use parentheses in complicated conditions.

## 12.4 NOT operator

```sql
SELECT *
FROM employee
WHERE NOT department = 'IT';
```

Equivalent to:

```sql
WHERE department <> 'IT';
```

However, rows with NULL department values are not returned by either condition.

---

# 13. BETWEEN Operator

BETWEEN checks whether a value is within a specified range.

Syntax:

```sql
WHERE column BETWEEN lower_value AND upper_value;
```

Example:

```sql
SELECT *
FROM employee
WHERE salary BETWEEN 30000 AND 50000;
```

Equivalent to:

```sql
WHERE salary >= 30000
AND salary <= 50000;
```

### Boundary cases

| Salary | Returned? |
| --- | --- |
| 29999 | No |
| 30000 | Yes |
| 35000 | Yes |
| 50000 | Yes |
| 50001 | No |
| NULL | No |

BETWEEN is inclusive of both endpoints.

### NOT BETWEEN

```sql
SELECT *
FROM employee
WHERE salary NOT BETWEEN 30000 AND 50000;
```

Returns values below 30000 or above 50000, excluding NULL.

### BETWEEN with DATE

```sql
SELECT *
FROM employee
WHERE joining_date
BETWEEN DATE '2026-01-01'
AND DATE '2026-12-31';
```

This includes both dates.

**Timestamp trap:** If you use a timestamp column, an upper boundary of `2026-12-31 00:00:00` does not include the remainder of December 31.

A safer full-year filter is:

```sql
WHERE created_at >= TIMESTAMP '2026-01-01 00:00:00'
AND created_at < TIMESTAMP '2027-01-01 00:00:00';
```

---

# 14. IN Operator

IN checks whether a value matches any value from a specified list.

Syntax:

```sql
WHERE column IN (value1, value2, value3);
```

Example:

```sql
SELECT *
FROM employee
WHERE department IN ('IT', 'HR', 'Finance');
```

Equivalent to:

```sql
WHERE department = 'IT'
OR department = 'HR'
OR department = 'Finance';
```

### NOT IN

```sql
SELECT *
FROM employee
WHERE department NOT IN ('IT', 'HR');
```

Returns employees whose department is neither IT nor HR.

### IN with NULL

```sql
SELECT *
FROM employee
WHERE salary IN (30000, 40000, NULL);
```

A salary of 50000 produces UNKNOWN because it matches neither number and cannot be established as unequal to NULL.

### NOT IN with NULL

```sql
SELECT *
FROM employee
WHERE salary NOT IN (30000, 40000, NULL);
```

This is a major SQL trap.

For nonmatching salary values, the comparison involving NULL results in UNKNOWN.

Consequently, ordinary nonmatching rows are not returned.

**Developer rule:** Be extremely careful when using `NOT IN` with subqueries that may return NULL. Consider `NOT EXISTS` instead.

---

# 15. NULL Comparison - IS NULL and IS NOT NULL

NULL represents a missing or unknown value.

You cannot correctly check NULL using `=` or `<>`.

Incorrect:

```sql
SELECT *
FROM employee
WHERE salary = NULL;
```

Correct:

```sql
SELECT *
FROM employee
WHERE salary IS NULL;
```

To retrieve non-NULL values:

```sql
SELECT *
FROM employee
WHERE salary IS NOT NULL;
```

### Important NULL edge cases

| Expression | Result |
| --- | --- |
| `NULL = NULL` | UNKNOWN |
| `NULL <> NULL` | UNKNOWN |
| `NULL > 10` | UNKNOWN |
| `NULL IS NULL` | TRUE |
| `NULL IS NOT NULL` | FALSE |
| `NOT (NULL = 10)` | UNKNOWN |

Remember: WHERE only returns rows for which the condition is TRUE.

UNKNOWN is not returned.

---

# 16. String Comparison and Trailing Spaces

This is a particularly important HSQLDB-specific topic.

HSQLDB 2.x uses space-padding semantics when comparing character strings under its default PAD SPACE collation.

When two strings have different lengths, the shorter string is conceptually padded with trailing spaces for comparison.

## 16.1 Comparing strings of equal length

```sql
SELECT
    CASE
        WHEN 'PM' = 'PM' THEN 'MATCH'
        ELSE 'NO MATCH'
    END
FROM (VALUES(0)) AS t(x);
```

Result:

```text
MATCH
```

## 16.2 Comparing strings of different lengths

```sql
SELECT
    CASE
        WHEN 'PM' = 'PM  ' THEN 'MATCH'
        ELSE 'NO MATCH'
    END
FROM (VALUES(0)) AS t(x);
```

Under default PAD SPACE comparison:

```text
MATCH
```

The shorter value is padded for comparison.

## 16.3 Leading spaces

```sql
SELECT
    CASE
        WHEN 'PM' = ' PM' THEN 'MATCH'
        ELSE 'NO MATCH'
    END
FROM (VALUES(0)) AS t(x);
```

Result:

```text
NO MATCH
```

Leading spaces are significant.

The database does not remove leading spaces automatically.

## 16.4 Comparison summary

| First value | Second value | Default HSQLDB result |
| --- | --- | --- |
| `'PM'` | `'PM'` | Equal |
| `'PM'` | `'PM '` | Equal |
| `'PM'` | `'PM  '` | Equal |
| `'PM'` | `' PM'` | Not equal |
| `'PM'` | `'pm'` | Not equal under default case-sensitive settings |

**Important:** PAD SPACE comparison and VARCHAR storage are two different concepts. A trailing space can remain part of a VARCHAR value even when it is insignificant in a comparison.

---

# 17. DISTINCT - Removing Duplicate Records

DISTINCT is used to eliminate duplicate rows from the query result.

Syntax:

```sql
SELECT DISTINCT column_name
FROM table_name;
```

Consider:

| emp_id | department |
| --- | --- |
| 101 | IT |
| 102 | HR |
| 103 | IT |
| 104 | Finance |
| 105 | HR |
| 106 | NULL |
| 107 | NULL |

## 17.1 DISTINCT on a single column

```sql
SELECT DISTINCT department
FROM employee;
```

Result:

| department |
| --- |
| IT |
| HR |
| Finance |
| NULL |

Duplicate department values are removed.

Notice that the two NULL values produce one distinct NULL result.

## 17.2 DISTINCT on multiple columns

```sql
SELECT DISTINCT department, salary
FROM employee;
```

Here, DISTINCT applies to the complete combination of selected columns.

Consider:

| department | salary |
| --- | --- |
| IT | 50000 |
| IT | 50000 |
| IT | 60000 |
| HR | 50000 |
| HR | 50000 |

Result:

| department | salary |
| --- | --- |
| IT | 50000 |
| IT | 60000 |
| HR | 50000 |

Notice:

- IT, 50000 occurs twice, so one row remains.
- IT, 60000 is a different combination.
- HR, 50000 is also a different combination.

### Important trap

Incorrect:

```sql
SELECT department, DISTINCT salary
FROM employee;
```

(Invalid syntax)

Correct:

```sql
SELECT DISTINCT department, salary
FROM employee;
```

DISTINCT applies to the entire SELECT result row, not independently to each column.

## 17.3 DISTINCT with NULL values

```sql
SELECT DISTINCT email
FROM employee;
```

If multiple rows contain NULL, only one NULL appears in the result.

This differs from COUNT(column), which ignores NULL.

## 17.4 COUNT(DISTINCT column)

```sql
SELECT COUNT(DISTINCT department)
FROM employee;
```

Counts the distinct non-NULL department values.

For the previous example:

```text
3
```

Because IT, HR and Finance are the three distinct non-NULL values.

### COUNT(DISTINCT) versus DISTINCT

| Query | Behaviour |
| --- | --- |
| `SELECT DISTINCT department` | Returns unique values, including one NULL |
| `COUNT(DISTINCT department)` | Counts unique non-NULL values |
| `COUNT(department)` | Counts all non-NULL values |
| `COUNT(*)` | Counts all rows |

### COUNT(DISTINCT multiple columns)

If you need to count unique combinations of two columns, use a derived table:

```sql
SELECT COUNT(*)
FROM (
    SELECT DISTINCT department, salary
    FROM employee
) AS unique_combinations;
```

This is a clear and portable way to count unique combinations.

---

# 18. LIKE Operator - Pattern Matching

LIKE is used to search for text matching a particular pattern.

It has two important wildcards:

| Wildcard | Meaning |
| --- | --- |
| `%` | Zero or more characters |
| `_` | Exactly one character |

## 18.1 Starts with a pattern

```sql
SELECT *
FROM employee
WHERE fname LIKE 'e%';
```

Returns names beginning with `e`.

Examples:

```text
E
Ethan
Edward
```

Under the default case-sensitive configuration, uppercase `E` does not match lowercase `e`.

## 18.2 Ends with a pattern

```sql
SELECT *
FROM employee
WHERE fname LIKE '%e';
```

Returns names ending with `e`.

Examples:

```text
Mike
Bruce
Steve
```

## 18.3 Contains a pattern anywhere

```sql
SELECT *
FROM employee
WHERE fname LIKE '%m%';
```

Returns names containing the character `m` anywhere.

Examples:

```text
Kumar
Manoj
Ramesh
```

## 18.4 Fixed-position pattern

Suppose you want names whose second character is `a`.

```sql
SELECT *
FROM employee
WHERE fname LIKE '_a%';
```

Explanation:

- First `_` represents exactly one character.
- Second character must be `a`.
- `%` represents any remaining characters.

Matches:

```text
Ravi
Karan
Manoj
```

## 18.5 Exact length matching

Find names containing exactly five characters:

```sql
SELECT *
FROM employee
WHERE fname LIKE '_____';
```

Five underscores mean exactly five characters.

Find names starting with A and containing exactly four characters:

```sql
SELECT *
FROM employee
WHERE fname LIKE 'A___';
```

## 18.6 Multiple wildcard combinations

| Pattern | Meaning |
| --- | --- |
| `'A%'` | Starts with A |
| `'%A'` | Ends with A |
| `'%A%'` | Contains A |
| `'_A%'` | A at second position |
| `'A_%'` | Starts with A and has at least two characters |
| `'__A%'` | A at third position |
| `'A___'` | Exactly four characters, starts with A |
| `'____%'` | At least four characters |

## 18.7 NOT LIKE

```sql
SELECT *
FROM employee
WHERE fname NOT LIKE 'A%';
```

Returns names not beginning with A.

NULL names are excluded because the LIKE condition evaluates to UNKNOWN.

## 18.8 LIKE with dates

A DATE column should not be treated as an ordinary VARCHAR column.

If you want to search for a year/month pattern, convert the date to character data first.

Example:

```sql
SELECT *
FROM employee
WHERE CAST(joining_date AS VARCHAR(10))
LIKE '2026-11-%';
```

This searches dates belonging to November 2026.

For production date filtering, however, use a date range instead:

```sql
SELECT *
FROM employee
WHERE joining_date >= DATE '2026-11-01'
AND joining_date < DATE '2026-12-01';
```

Date ranges are preferable to applying CAST or other functions to the column.

## 18.9 Searching for actual % and _ characters

Suppose product names contain an actual percent sign.

Use ESCAPE:

```sql
SELECT *
FROM products
WHERE product_name LIKE '%\%%' ESCAPE '\';
```

The escaped `%` is treated as a literal character instead of a wildcard.

**Important:** LIKE pattern matching is not the same as ordinary equality comparison. Do not assume that trailing-space padding rules for `=` also make LIKE patterns interchangeable.

---

# 19. ORDER BY - Sorting Query Results

ORDER BY sorts the final result.

Syntax:

```sql
SELECT *
FROM employee
ORDER BY salary;
```

By default, sorting is ascending.

### Ascending order

```sql
SELECT *
FROM employee
ORDER BY salary ASC;
```

### Descending order

```sql
SELECT *
FROM employee
ORDER BY salary DESC;
```

### Sorting by multiple columns

```sql
SELECT *
FROM employee
ORDER BY department ASC, salary DESC;
```

First sorts by department, then by salary within each department.

### ORDER BY using an alias

```sql
SELECT
    fname,
    salary * 12 AS annual_salary
FROM employee
ORDER BY annual_salary DESC;
```

This is valid.

### NULL sorting in HSQLDB

By default, NULL values are sorted first in ascending order.

You can explicitly control their position:

```sql
SELECT *
FROM employee
ORDER BY salary ASC NULLS LAST;
```

Or:

```sql
SELECT *
FROM employee
ORDER BY salary DESC NULLS FIRST;
```

### Important distinction

Without ORDER BY, SQL does not guarantee the order in which rows are returned.

Do not rely on insertion order or primary-key order.

---

# 20. Logical SQL Query Execution Order

This is one of the most important topics for SQL developers.

The written query starts with SELECT, but the logical processing of a query follows a different sequence.

Consider:

```sql
SELECT
    department,
    AVG(salary) AS average_salary
FROM employee
WHERE salary > 20000
GROUP BY department
HAVING AVG(salary) > 40000
ORDER BY average_salary DESC;
```

The logical execution sequence is:

## SQL logical execution order

1. **FROM**  
Identify the source table(s) and produce the initial row set.
2. **JOIN / ON**  
Combine tables and apply join matching conditions.
3. **WHERE**  
Filter individual rows before grouping.
4. **GROUP BY**  
Group the remaining rows.
5. **HAVING**  
Filter groups based on aggregate conditions.
6. **SELECT**  
Calculate selected expressions and output columns.
7. **DISTINCT**  
Remove duplicate result rows.
8. **ORDER BY**  
Sort the final result.
9. **OFFSET / FETCH / LIMIT**  
Restrict the number of returned rows.

The exact processing details can vary with query features, but this is the standard logical order for learning SQL. HyperSQL's documentation describes its data-access operations in a corresponding conceptual sequence.

## 20.1 Why can you use an alias in ORDER BY but not WHERE?

Example:

```sql
SELECT salary * 12 AS annual_salary
FROM employee
ORDER BY annual_salary;
```

Valid.

But:

```sql
SELECT salary * 12 AS annual_salary
FROM employee
WHERE annual_salary > 500000;
```

Normally invalid because WHERE is processed before SELECT creates the output alias.

Instead:

```sql
SELECT salary * 12 AS annual_salary
FROM employee
WHERE salary * 12 > 500000;
```

## 20.2 WHERE versus HAVING

WHERE filters rows before grouping.

HAVING filters groups after aggregation.

Example:

```sql
SELECT department, AVG(salary)
FROM employee
WHERE salary > 20000
GROUP BY department
HAVING AVG(salary) > 40000;
```

Processing:

1. Remove employees whose salary is 20000 or less.
2. Group remaining employees by department.
3. Calculate average salary per department.
4. Keep departments whose average is greater than 40000.

## 20.3 Can WHERE use aggregate functions?

Normally, no.

Incorrect:

```sql
SELECT department, AVG(salary)
FROM employee
WHERE AVG(salary) > 40000
GROUP BY department;
```

Correct:

```sql
SELECT department, AVG(salary)
FROM employee
GROUP BY department
HAVING AVG(salary) > 40000;
```

## 20.4 Can GROUP BY use SELECT aliases?

In HyperSQL, SELECT aliases are not available in GROUP BY under its SQL-standard label scope.

Use the original column or expression.

```sql
SELECT department AS dept, COUNT(*)
FROM employee
GROUP BY department;
```

This is valid.

---

# 21. Advanced HSQLDB Interview Edge Cases - Quick Revision

| Scenario | Expected behaviour |
| --- | --- |
| INSERT without column names and fewer values | Error |
| INSERT with column names and omitted nullable column | NULL |
| INSERT with omitted DEFAULT column | Default value |
| INSERT with explicit NULL into DEFAULT column | NULL, not default |
| INSERT with DEFAULT keyword | Default value |
| INSERT multiple rows using VALUES | Supported |
| INSERT using SELECT returning zero rows | Zero rows inserted |
| INSERT violating PRIMARY KEY | Error |
| INSERT violating UNIQUE | Error |
| INSERT multiple NULLs into nullable UNIQUE | Allowed |
| INSERT nonexistent foreign key | Error |
| UPDATE without WHERE | All rows updated |
| UPDATE with WHERE | Matching rows updated |
| UPDATE NOT NULL column to NULL | Error |
| UPDATE primary key to unused value | Can succeed |
| UPDATE primary key to duplicate value | Error |
| UPDATE UNIQUE column to duplicate value | Error |
| UPDATE CHECK column with invalid value | Error |
| UPDATE child FK to nonexistent parent | Error |
| UPDATE referenced parent key without action | Error |
| DELETE without WHERE | All rows deleted |
| DELETE with WHERE | Matching rows deleted |
| DELETE referenced parent row | Error by default |
| SELECT * | All columns |
| SELECT col1, col2 | Two selected columns |
| SELECT col1 col2 | col1 with alias col2 |
| SELECT expression AS alias | Calculated result column |
| WHERE column = NULL | UNKNOWN, not a NULL test |
| WHERE column IS NULL | Finds NULL records |
| BETWEEN | Both boundaries included |
| IN | Matches any list value |
| NOT IN containing NULL | Can produce UNKNOWN for all nonmatching values |
| DISTINCT on multiple columns | Removes duplicate combinations |
| COUNT(DISTINCT column) | Ignores NULL |
| LIKE 'A%' | Starts with A |
| LIKE '%A' | Ends with A |
| LIKE '%A%' | Contains A |
| LIKE '_A%' | A at second position |
| ORDER BY | Sorts returned rows |
| WHERE | Filters before GROUP BY |
| HAVING | Filters after GROUP BY |

---

# 22. Advanced Quiz - 15 Questions

(2-Year SQL Developer Assessment) (15 MCQs)

These questions combine INSERT, UPDATE, DELETE, SELECT, WHERE, DISTINCT and LIKE. They include tricky syntax, constraint violations and unexpected SQL results.

**Advanced SQL Quiz** (/15 answered)

# 23. Preparation Checklist - SQL Developer

Use this to track your practical knowledge.



## Official HSQLDB documentation

- HyperSQL 2.7.4 - INSERT statement reference.
- HyperSQL - Data Access and Change.
- HyperSQL - SELECT, LIKE, DISTINCT and ORDER BY.
- HyperSQL - String comparison and collation.
- HyperSQL - DML features and multi-row INSERT/UPDATE.

**My recommendation:** For a two-year SQL developer assessment, practise writing queries rather than only reading their syntax. Pay particular attention to UPDATE without WHERE, parent-child foreign-key updates, explicit NULL versus DEFAULT, trailing-space comparisons, DISTINCT across multiple columns, and the logical execution order. These are common sources of subtle SQL errors.

### User

for 2 year sql developer hsql database level give concepts needed from required topics all tricky advanced topics from these explanation and 15 question quiz at end all edge cases single row function return single row iperates on single row, multi row function returns single row operates on multuoke rows, numeric: ceil,floor, abs, round function roynd can be given parameter if 0 upto 0 decimal digit 1 decimal digit to be specified 0 no need to give , character function upper lower concat length nested concat and any other popular there give, substring function : to extract first4 chra, extract 10 char from second position extract last second last char, conversion function to_char() date to string  part of date extract parts of date in desired format using to_char,, to_date string to date (s,'dd-mm-yy') desired formar, aggreagate function multi row function sum,max,min,avg,count, date function sysdate current timestamp, current_date current date add_months months_between, dayname,monthname,yearname, day,month,year functions and other popular date fucntions give, miscalleneous function nvl(min,0) nvl(min,'not recorded'),user- retturns current logged in user case when case column name when se then salary*1.2 when.. end when values of single column have to be compared with various expressions searcged case expression case when mark >=35 and mark<=95 then excellent else option if no else null returned by case statement search used to compare multiple boolen expression on same or differed columns , cast function to convert numeric and date to varchar and to truncate decimal digits

### ChatGPT

# HSQLDB - Advanced SQL Functions Guide

(2-Year SQL Developer Level) (15 MCQ Quiz)

This guide covers SQL functions used in real-world database development, including numeric calculations, string manipulation, type conversion, date operations, aggregate functions, NULL handling, CASE expressions and advanced function combinations.

The most important distinction is understanding **how many rows a function operates on and how many rows it returns**.

# 1. Types of SQL Functions

SQL functions are broadly classified into two categories.

## 1.1 Single-row functions (Scalar functions)

A single-row function operates on an individual row and returns one result for that row.

If a table contains 100 rows, applying a single-row function normally produces 100 corresponding results.

Example:

```sql
SELECT UPPER(fname)
FROM employee;
```

Input:

| fname |
| --- |
| Arun |
| Ravi |
| Kumar |

Output:

| UPPER(fname) |
| --- |
| ARUN |
| RAVI |
| KUMAR |

Each input row produces one output value.

Common single-row functions:

- Numeric functions
- Character functions
- Conversion functions
- Date functions
- NULL-handling functions
- Conditional functions

## 1.2 Multiple-row functions (Aggregate functions)

Aggregate functions operate on a collection of rows and return one result for the group.

Example:

```sql
SELECT SUM(salary)
FROM employee;
```

Input:

| salary |
| --- |
| 30000 |
| 40000 |
| 50000 |

Output:

| SUM(salary) |
| --- |
| 120000 |

Three rows are processed, but one result is returned.

Common aggregate functions:

| Function | Purpose |
| --- | --- |
| SUM() | Total |
| AVG() | Average |
| MIN() | Minimum |
| MAX() | Maximum |
| COUNT() | Count |

## 1.3 Single-row versus aggregate functions

| Feature | Single-row | Aggregate |
| --- | --- | --- |
| Input | Individual row | Multiple rows |
| Output | One result per input row | One result per group |
| Example | UPPER() | SUM() |
| Example | ROUND() | AVG() |
| Example | LENGTH() | COUNT() |
| Example | ABS() | MAX() |

**Important:** Aggregate functions can also return multiple results when used with GROUP BY, because each group produces one result.

Example:

```sql
SELECT department, AVG(salary)
FROM employee
GROUP BY department;
```

This returns one average per department.

---

# 2. Numeric Functions

Numeric functions operate on numeric values and return numeric results.

Important HSQLDB functions:

| Function | Purpose |
| --- | --- |
| ABS() | Absolute value |
| CEIL() / CEILING() | Round upwards |
| FLOOR() | Round downwards |
| ROUND() | Round to specified decimal places |
| TRUNC() | Remove fractional digits |
| MOD() | Remainder |
| POWER() | Raise to a power |
| SQRT() | Square root |
| SIGN() | Sign of a number |
| EXP() | Exponential |
| LN() | Natural logarithm |
| LOG10() | Base-10 logarithm |

## 2.1 ABS() - Absolute value

Returns the non-negative magnitude of a number.

Syntax:

```sql
ABS(number)
```

Examples:

```sql
SELECT
    ABS(10),
    ABS(-10),
    ABS(0)
FROM (VALUES(0)) AS t(x);
```

Results:

| Expression | Result |
| --- | --- |
| ABS(10) | 10 |
| ABS(-10) | 10 |
| ABS(0) | 0 |

Example with a table:

```sql
SELECT
    emp_id,
    salary,
    ABS(salary - 50000) AS salary_difference
FROM employee;
```

This calculates the absolute difference between employee salary and 50000.

## 2.2 CEIL() / CEILING()

Returns the smallest integer greater than or equal to the input.

Syntax:

```sql
CEIL(number)
```

Examples:

```sql
SELECT
    CEIL(10.2),
    CEIL(10.8),
    CEIL(10.0),
    CEIL(-10.2)
FROM (VALUES(0)) AS t(x);
```

| Input | Result |
| --- | --- |
| 10.2 | 11 |
| 10.8 | 11 |
| 10.0 | 10 |
| -10.2 | -10 |

**Tricky point:** CEIL(-10.2) is -10, not -11.

It moves towards positive infinity.

## 2.3 FLOOR()

Returns the greatest integer less than or equal to the input.

Syntax:

```sql
FLOOR(number)
```

Examples:

```sql
SELECT
    FLOOR(10.2),
    FLOOR(10.8),
    FLOOR(-10.2),
    FLOOR(-10.8)
FROM (VALUES(0)) AS t(x);
```

| Input | Result |
| --- | --- |
| 10.2 | 10 |
| 10.8 | 10 |
| -10.2 | -11 |
| -10.8 | -11 |

**Important:** FLOOR and TRUNC are not identical for negative numbers.

## 2.4 ROUND()

ROUND rounds a numeric value to a specified number of decimal places.

Syntax:

```sql
ROUND(number, decimal_places)
```

The second argument specifies how many digits to retain after the decimal point.

### Without decimal-place specification

```sql
SELECT ROUND(123.456)
FROM (VALUES(0)) AS t(x);
```

Result:

```text
123
```

The default is zero decimal places.

### ROUND with zero

```sql
SELECT ROUND(123.456, 0)
FROM (VALUES(0)) AS t(x);
```

Result:

```text
123
```

### ROUND with one decimal place

```sql
SELECT ROUND(123.456, 1)
FROM (VALUES(0)) AS t(x);
```

Result:

```text
123.5
```

### ROUND with two decimal places

```sql
SELECT ROUND(123.456, 2)
FROM (VALUES(0)) AS t(x);
```

Result:

```text
123.46
```

### ROUND with three decimal places

```sql
SELECT ROUND(123.456, 3)
FROM (VALUES(0)) AS t(x);
```

Result:

```text
123.456
```

### ROUND edge cases

| Expression | Result |
| --- | --- |
| ROUND(12.34) | 12 |
| ROUND(12.50) | 13 |
| ROUND(12.56) | 13 |
| ROUND(12.34,1) | 12.3 |
| ROUND(12.36,1) | 12.4 |
| ROUND(12.345,2) | 12.35 |
| ROUND(-12.34,1) | -12.3 |
| ROUND(-12.36,1) | -12.4 |

### Rounding to the left of the decimal point

You can also use negative decimal-place arguments.

```sql
SELECT
    ROUND(1234.56, -1),
    ROUND(1234.56, -2),
    ROUND(1234.56, -3)
FROM (VALUES(0)) AS t(x);
```

Conceptual results:

| Expression | Result |
| --- | --- |
| ROUND(1234.56,-1) | 1230 |
| ROUND(1234.56,-2) | 1200 |
| ROUND(1234.56,-3) | 1000 |

This is useful when rounding to tens, hundreds or thousands.

## 2.5 TRUNC()

TRUNC removes fractional digits without rounding.

Syntax:

```sql
TRUNC(number)
TRUNC(number, decimal_places)
```

Examples:

```sql
SELECT
    TRUNC(123.456),
    TRUNC(123.456, 1),
    TRUNC(123.456, 2)
FROM (VALUES(0)) AS t(x);
```

Results:

| Expression | Result |
| --- | --- |
| TRUNC(123.456) | 123 |
| TRUNC(123.456,1) | 123.4 |
| TRUNC(123.456,2) | 123.45 |

### ROUND versus TRUNC versus FLOOR versus CEIL

| Input | ROUND | TRUNC | FLOOR | CEIL |
| --- | --- | --- | --- | --- |
| 12.8 | 13 | 12 | 12 | 13 |
| 12.2 | 12 | 12 | 12 | 13 |
| -12.8 | -13 | -12 | -13 | -12 |
| -12.2 | -12 | -12 | -13 | -12 |

These differences are frequently tested in SQL interviews.

## 2.6 MOD()

Returns the remainder after division.

Syntax:

```sql
MOD(number1, number2)
```

Examples:

```sql
SELECT
    MOD(10,3),
    MOD(15,5),
    MOD(17,2)
FROM (VALUES(0)) AS t(x);
```

Results:

```text
1
0
1
```

Practical example: Find even employee IDs.

```sql
SELECT *
FROM employee
WHERE MOD(emp_id, 2) = 0;
```

Find odd employee IDs:

```sql
SELECT *
FROM employee
WHERE MOD(emp_id, 2) = 1;
```

## 2.7 POWER() and SQRT()

```sql
SELECT
    POWER(2,3),
    POWER(5,2),
    SQRT(64),
    SQRT(144)
FROM (VALUES(0)) AS t(x);
```

Results:

| Function | Result |
| --- | --- |
| POWER(2,3) | 8 |
| POWER(5,2) | 25 |
| SQRT(64) | 8 |
| SQRT(144) | 12 |

## 2.8 SIGN()

Returns the sign of a number.

```sql
SELECT
    SIGN(100),
    SIGN(-100),
    SIGN(0)
FROM (VALUES(0)) AS t(x);
```

Results:

| Input | Result |
| --- | --- |
| 100 | 1 |
| -100 | -1 |
| 0 | 0 |

---

# 3. Character Functions (String Functions)

Character functions operate on strings and return character or numeric values.

They are commonly used for:

- Formatting names.
- Searching strings.
- Extracting substrings.
- Removing spaces.
- Combining columns.
- Validating text.
- Transforming case.

## 3.1 UPPER()

Converts all lowercase characters to uppercase.

Syntax:

```sql
UPPER(string)
```

Example:

```sql
SELECT UPPER('hello world')
FROM (VALUES(0)) AS t(x);
```

Result:

```text
HELLO WORLD
```

With a table:

```sql
SELECT
    fname,
    UPPER(fname) AS uppercase_name
FROM employee;
```

## 3.2 LOWER()

Converts all uppercase characters to lowercase.

```sql
SELECT LOWER('HELLO WORLD')
FROM (VALUES(0)) AS t(x);
```

Result:

```text
hello world
```

Practical example:

```sql
SELECT *
FROM employee
WHERE LOWER(fname) = 'arun';
```

This can match names regardless of their stored case.

**Performance consideration:** Applying LOWER() to a column in a WHERE clause can prevent an ordinary index from being used efficiently, depending on the execution plan. For large tables, consider a suitable functional index or normalized search column.

## 3.3 CONCAT()

Combines two or more strings.

Syntax:

```sql
CONCAT(string1, string2)
```

Example:

```sql
SELECT CONCAT('Hello', ' World')
FROM (VALUES(0)) AS t(x);
```

Result:

```text
Hello World
```

With table columns:

```sql
SELECT
    CONCAT(fname, lname) AS full_name
FROM employee;
```

If fname is Arun and lname is Kumar:

```text
ArunKumar
```

To add a space:

```sql
SELECT
    CONCAT(fname, ' ', lname) AS full_name
FROM employee;
```

Result:

```text
Arun Kumar
```

### Nested CONCAT()

```sql
SELECT
    CONCAT(
        CONCAT(fname, ' '),
        lname
    ) AS full_name
FROM employee;
```

This is nested concatenation.

HSQLDB also supports the `||` concatenation operator:

```sql
SELECT fname || ' ' || lname AS full_name
FROM employee;
```

### CONCAT with NULL

This is an important HSQLDB-specific edge case.

HSQLDB's default `sql.concat_nulls` setting is TRUE.

Therefore:

```sql
SELECT CONCAT('Arun', NULL)
FROM (VALUES(0)) AS t(x);
```

Returns NULL under the default setting.

The `||` operator follows the same concatenation NULL setting.

To avoid losing the non-NULL part:

```sql
SELECT CONCAT(
    COALESCE(fname, ''),
    COALESCE(lname, '')
)
FROM employee;
```

## 3.4 LENGTH()

Returns the number of characters in a string.

Syntax:

```sql
LENGTH(string)
```

Examples:

```sql
SELECT
    LENGTH('HELLO'),
    LENGTH('SQL'),
    LENGTH('')
FROM (VALUES(0)) AS t(x);
```

Results:

| Input | Length |
| --- | --- |
| HELLO | 5 |
| SQL | 3 |
| Empty string | 0 |

Practical example:

```sql
SELECT *
FROM employee
WHERE LENGTH(fname) > 5;
```

Returns employees whose first names contain more than five characters.

**Edge case:** LENGTH counts trailing spaces in a string value.

```sql
SELECT LENGTH('ABC   ')
FROM (VALUES(0)) AS t(x);
```

Result:

```text
6
```

## 3.5 SUBSTRING()

SUBSTRING extracts part of a string.

Syntax:

```sql
SUBSTRING(string FROM start_position FOR length)
```

HSQLDB also accepts the commonly used form:

```sql
SUBSTRING(string, start_position, length)
```

Positions are 1-based, not 0-based.

### Case 1: Extract first four characters

```sql
SELECT SUBSTRING('PROGRAMMING', 1, 4)
FROM (VALUES(0)) AS t(x);
```

Result:

```text
PROG
```

### Case 2: Extract ten characters starting from second position

```sql
SELECT SUBSTRING('ABCDEFGHIJKLM', 2, 10)
FROM (VALUES(0)) AS t(x);
```

Result:

```text
BCDEFGHIJK
```

### Case 3: Extract last two characters

```sql
SELECT SUBSTRING(
    'PROGRAMMING',
    LENGTH('PROGRAMMING') - 1,
    2
)
FROM (VALUES(0)) AS t(x);
```

Result:

```text
NG
```

### Case 4: Extract the last character

```sql
SELECT SUBSTRING(
    'PROGRAMMING',
    LENGTH('PROGRAMMING'),
    1
)
FROM (VALUES(0)) AS t(x);
```

Result:

```text
G
```

### Case 5: Extract second-last character

```sql
SELECT SUBSTRING(
    'PROGRAMMING',
    LENGTH('PROGRAMMING') - 1,
    1
)
FROM (VALUES(0)) AS t(x);
```

Result:

```text
N
```

### Case 6: Extract characters from a specific position to the end

```sql
SELECT SUBSTRING('PROGRAMMING' FROM 4)
FROM (VALUES(0)) AS t(x);
```

Result:

```text
GRAMMING
```

### Case 7: Substring with length exceeding remaining characters

```sql
SELECT SUBSTRING('HELLO' FROM 3 FOR 10)
FROM (VALUES(0)) AS t(x);
```

Result:

```text
LLO
```

It returns the remaining characters rather than producing an error.

### Case 8: Starting position exceeds string length

```sql
SELECT SUBSTRING('HELLO' FROM 10 FOR 2)
FROM (VALUES(0)) AS t(x);
```

Returns an empty string.

### Case 9: Extract first three characters from a column

```sql
SELECT
    fname,
    SUBSTRING(fname, 1, 3) AS short_name
FROM employee;
```

### Important SUBSTRING rules

| Situation | Behaviour |
| --- | --- |
| Starting position = 1 | First character |
| Starting position = 2 | Second character |
| Length = 1 | One character |
| Length exceeds remaining characters | Remaining characters returned |
| Starting position beyond string | Empty string |
| Input is NULL | NULL |

## 3.6 TRIM()

Removes leading and trailing spaces.

Syntax:

```sql
TRIM(string)
```

Example:

```sql
SELECT TRIM('   HELLO   ')
FROM (VALUES(0)) AS t(x);
```

Result:

```text
HELLO
```

### LTRIM()

Removes leading spaces.

```sql
SELECT LTRIM('   HELLO   ')
FROM (VALUES(0)) AS t(x);
```

Result:

```text
HELLO
```

### RTRIM()

Removes trailing spaces.

```sql
SELECT RTRIM('   HELLO   ')
FROM (VALUES(0)) AS t(x);
```

Result:

```text
   HELLO
```

### Practical example

```sql
SELECT
    TRIM(fname) AS clean_name
FROM employee;
```

Useful when importing CSV data containing unnecessary spaces.

## 3.7 REPLACE()

Replaces occurrences of a substring with another substring.

Syntax:

```sql
REPLACE(original_string, search_string, replacement_string)
```

Example:

```sql
SELECT REPLACE(
    'SQL DEVELOPER',
    'SQL',
    'JAVA'
)
FROM (VALUES(0)) AS t(x);
```

Result:

```text
JAVA DEVELOPER
```

Another example:

```sql
SELECT REPLACE(
    '111-222-333',
    '-',
    ''
)
FROM (VALUES(0)) AS t(x);
```

Result:

```text
111222333
```

## 3.8 POSITION()

Returns the position of a substring within another string.

Syntax:

```sql
POSITION(search_string IN source_string)
```

Example:

```sql
SELECT POSITION('GRAM' IN 'PROGRAMMING')
FROM (VALUES(0)) AS t(x);
```

Result:

```text
4
```

If the substring is not found, the result is zero.

```sql
SELECT POSITION('XYZ' IN 'PROGRAMMING')
FROM (VALUES(0)) AS t(x);
```

Result:

```text
0
```

## 3.9 Other useful character functions

| Function | Purpose | Example |
| --- | --- | --- |
| CHAR_LENGTH() | Character count | `CHAR_LENGTH('HELLO')` |
| OCTET_LENGTH() | Byte length | `OCTET_LENGTH('ABC')` |
| LEFT() | Leftmost characters | `LEFT('HELLO',2)` |
| RIGHT() | Rightmost characters | `RIGHT('HELLO',2)` |
| REPEAT() | Repeat a string | `REPEAT('A',3)` |
| REVERSE() | Reverse a string | `REVERSE('ABC')` |
| ASCII() | Numeric code of first character | `ASCII('A')` |
| SPACE() | Generate spaces | `SPACE(5)` |
| INITCAP() | Capitalize words | `INITCAP('hello world')` |

Examples:

```sql
SELECT
    LEFT('PROGRAMMING', 4),
    RIGHT('PROGRAMMING', 4),
    REVERSE('SQL'),
    REPEAT('AB', 3),
    INITCAP('hello world')
FROM (VALUES(0)) AS t(x);
```

Results:

```text
PROG
MING
LQS
ABABAB
Hello World
```

These are useful for string formatting and data cleaning.

---

# 4. Conversion Functions

Conversion functions change values from one data type to another or format values for presentation.

Important functions:

| Function | Purpose |
| --- | --- |
| CAST() | Standard type conversion |
| TO_CHAR() | Format numeric or date/time values as text |
| TO_DATE() | Parse formatted text into timestamp |
| TO_TIMESTAMP() | Parse text into timestamp |
| TO_NUMBER() | Convert numeric text into decimal |

## 4.1 CAST()

Syntax:

```sql
CAST(expression AS target_datatype)
```

### Integer to VARCHAR

```sql
SELECT CAST(12345 AS VARCHAR(10))
FROM (VALUES(0)) AS t(x);
```

Result:

```text
12345
```

### NUMERIC to VARCHAR

```sql
SELECT CAST(
    123.45 AS VARCHAR(10)
)
FROM (VALUES(0)) AS t(x);
```

Result:

```text
123.45
```

### DATE to VARCHAR

```sql
SELECT CAST(
    DATE '2026-11-08' AS VARCHAR(20)
)
FROM (VALUES(0)) AS t(x);
```

Result:

```text
2026-11-08
```

### VARCHAR to DATE

```sql
SELECT CAST(
    '2026-11-08' AS DATE
)
FROM (VALUES(0)) AS t(x);
```

Result:

```text
2026-11-08
```

### NUMERIC to INTEGER

```sql
SELECT CAST(123.45 AS INTEGER)
FROM (VALUES(0)) AS t(x);
```

This converts the decimal value to an integer using the applicable HSQLDB numeric conversion rules.

### Important distinction

CAST performs data-type conversion.

TO_CHAR performs formatted character conversion.

For example:

```sql
SELECT CAST(1234.5 AS VARCHAR(20))
FROM (VALUES(0)) AS t(x);
```

Produces a string representation of the number.

But:

```sql
SELECT TO_CHAR(1234.5, '99999.99')
FROM (VALUES(0)) AS t(x);
```

Formats the number according to the specified template.

## 4.2 TO_CHAR() - Date to string conversion

HSQLDB supports TO_CHAR for date/time values and numeric values.

Syntax:

```sql
TO_CHAR(datetime_value, format)
```

Example:

```sql
SELECT TO_CHAR(
    DATE '2026-11-08',
    'DD-MM-YYYY'
)
FROM (VALUES(0)) AS t(x);
```

Result:

```text
08-11-2026
```

### Common date format elements

| Format | Meaning | Example |
| --- | --- | --- |
| YYYY | Four-digit year | 2026 |
| YY | Two-digit year | 26 |
| MM | Month number | 11 |
| MON | Short month name | NOV |
| MONTH | Full month name | November |
| DD | Day of month | 08 |
| DAY | Full weekday name | Sunday |
| DY | Short weekday name | SUN |
| HH24 | Hour, 00-23 | 14 |
| HH12 | Hour, 00-11 | 02 |
| MI | Minutes | 30 |
| SS | Seconds | 45 |
| AM / PM | Meridiem | PM |

### Examples

Extract only year:

```sql
SELECT TO_CHAR(
    DATE '2026-11-08',
    'YYYY'
)
FROM (VALUES(0)) AS t(x);
```

Result:

```text
2026
```

Extract month:

```sql
SELECT TO_CHAR(
    DATE '2026-11-08',
    'MM'
)
FROM (VALUES(0)) AS t(x);
```

Result:

```text
11
```

Extract month name:

```sql
SELECT TO_CHAR(
    DATE '2026-11-08',
    'MONTH'
)
FROM (VALUES(0)) AS t(x);
```

Result:

```text
November
```

Format a complete date:

```sql
SELECT TO_CHAR(
    DATE '2026-11-08',
    'DAY, DD MONTH YYYY'
)
FROM (VALUES(0)) AS t(x);
```

Result contains the weekday, day, month and year.

### Date and time formatting

```sql
SELECT TO_CHAR(
    TIMESTAMP '2026-11-08 14:30:45',
    'DD-MM-YYYY HH24:MI:SS'
)
FROM (VALUES(0)) AS t(x);
```

Result:

```text
08-11-2026 14:30:45
```

**Important:** The TO_CHAR format elements are not Java date format patterns. For example, HSQLDB uses `YYYY` and `MM`, not Java's `yyyy` and `MM` convention.

## 4.3 TO_CHAR() - Numeric to string conversion

Syntax:

```sql
TO_CHAR(number, format)
```

Example:

```sql
SELECT TO_CHAR(1234.56, '99999.99')
FROM (VALUES(0)) AS t(x);
```

The number is converted to a formatted character value.

Important format elements:

| Element | Meaning |
| --- | --- |
| 9 | Digit or blank |
| 0 | Digit or zero |
| FM | Removes leading formatting spaces |
| S | Includes sign |
| MI | Places minus sign at the end |
| PR | Displays negative values in angle brackets |

Example:

```sql
SELECT TO_CHAR(1234.5, 'FM99999.00')
FROM (VALUES(0)) AS t(x);
```

Result:

```text
1234.50
```

This is particularly useful when preparing reports.

## 4.4 TO_DATE() - String to date/time conversion

Syntax:

```sql
TO_DATE(string, format)
```

Important HSQLDB distinction: `TO_DATE()` returns a `TIMESTAMP(0)`, not a DATE data type. It does not retain fractional seconds.

Example:

```sql
SELECT TO_DATE(
    '08-11-2026',
    'DD-MM-YYYY'
)
FROM (VALUES(0)) AS t(x);
```

Result:

```text
2026-11-08 00:00:00
```

### Another example

```sql
SELECT TO_DATE(
    '25-12-2025',
    'DD-MM-YYYY'
)
FROM (VALUES(0)) AS t(x);
```

Result:

```text
2025-12-25 00:00:00
```

### Two-digit year

```sql
SELECT TO_DATE(
    '08-11-26',
    'DD-MM-YY'
)
FROM (VALUES(0)) AS t(x);
```

Two-digit year interpretation follows the HSQLDB format rules. For business data, prefer four-digit years to avoid ambiguity.

### CSV date conversion

Suppose the CSV contains:

```text
16-06-2023
```

You can convert it using:

```sql
SELECT TO_DATE(
    '16-06-2023',
    'DD-MM-YYYY'
)
FROM (VALUES(0)) AS t(x);
```

Result:

```text
2023-06-16 00:00:00
```

### Invalid date

```sql
SELECT TO_DATE(
    '35-13-2026',
    'DD-MM-YYYY'
)
FROM (VALUES(0)) AS t(x);
```

(Date conversion error)

The day and month are invalid.

## 4.5 TO_TIMESTAMP()

Used to convert formatted strings into timestamp values.

```sql
SELECT TO_TIMESTAMP(
    '08-11-2026 14:30:45',
    'DD-MM-YYYY HH24:MI:SS'
)
FROM (VALUES(0)) AS t(x);
```

Result:

```text
2026-11-08 14:30:45
```

Unlike TO_DATE, TO_TIMESTAMP supports fractional-second precision.

Example:

```sql
SELECT TO_TIMESTAMP(
    '08-11-2026 14:30:45.123',
    'DD-MM-YYYY HH24:MI:SS.FF3'
)
FROM (VALUES(0)) AS t(x);
```

HSQLDB 2.7.3 and later also support Java DateTimeFormatter patterns using the `JAVA:` prefix for these formatted date/time functions.

---

# 5. Aggregate Functions (Multiple-Row Functions)

Aggregate functions perform calculations over multiple rows and return a result for the entire set or each group.

Consider the following EMPLOYEE table:

| emp_id | department | salary |
| --- | --- | --- |
| 101 | IT | 30000 |
| 102 | IT | 40000 |
| 103 | HR | 50000 |
| 104 | HR | 60000 |
| 105 | IT | NULL |

## 5.1 SUM()

Returns the sum of non-NULL values.

Syntax:

```sql
SUM(column_name)
```

Example:

```sql
SELECT SUM(salary)
FROM employee;
```

Result:

```text
180000
```

NULL is ignored.

### SUM with WHERE

```sql
SELECT SUM(salary)
FROM employee
WHERE department = 'IT';
```

Result:

```text
70000
```

## 5.2 AVG()

Returns the average of non-NULL values.

```sql
SELECT AVG(salary)
FROM employee;
```

Result:

$$
\frac{30000+40000+50000+60000}{4}=45000
$$

NULL is excluded from both the sum and count used in the average.

### Important AVG edge case

```sql
SELECT AVG(salary)
FROM employee
WHERE salary IS NULL;
```

Result:

```text
NULL
```

There are no non-NULL values to average.

## 5.3 MAX()

Returns the maximum value.

```sql
SELECT MAX(salary)
FROM employee;
```

Result:

```text
60000
```

MAX works with numeric, date and character values, subject to the applicable comparison rules.

Example:

```sql
SELECT MAX(joining_date)
FROM employee;
```

Returns the latest non-NULL joining date.

## 5.4 MIN()

Returns the minimum value.

```sql
SELECT MIN(salary)
FROM employee;
```

Result:

```text
30000
```

Example:

```sql
SELECT MIN(fname)
FROM employee;
```

Returns the alphabetically smallest non-NULL name according to the column's collation.

## 5.5 COUNT()

COUNT is used to count rows or non-NULL values.

There are three important variations.

### COUNT(*)

```sql
SELECT COUNT(*)
FROM employee;
```

Result:

```text
5
```

Counts every row, including rows containing NULL.

### COUNT(column)

```sql
SELECT COUNT(salary)
FROM employee;
```

Result:

```text
4
```

Counts only non-NULL salary values.

### COUNT(DISTINCT column)

```sql
SELECT COUNT(DISTINCT department)
FROM employee;
```

Result:

```text
2
```

Counts distinct non-NULL department values.

## 5.6 Aggregate functions and NULL

Suppose:

| ID | Salary |
| --- | --- |
| 1 | 1000 |
| 2 | 2000 |
| 3 | NULL |
| 4 | 3000 |
| 5 | NULL |

Results:

| Function | Result |
| --- | --- |
| COUNT(*) | 5 |
| COUNT(salary) | 3 |
| SUM(salary) | 6000 |
| AVG(salary) | 2000 |
| MIN(salary) | 1000 |
| MAX(salary) | 3000 |

**Important edge cases:**

- SUM ignores NULL.
- AVG ignores NULL.
- MIN ignores NULL.
- MAX ignores NULL.
- COUNT(column) ignores NULL.
- COUNT(*) counts all rows.
- An aggregate over an empty input set generally returns NULL, except COUNT, which returns zero.

## 5.7 Aggregate functions with GROUP BY

Suppose employees belong to IT, HR and Finance.

```sql
SELECT
    department,
    SUM(salary) AS total_salary,
    AVG(salary) AS average_salary,
    MAX(salary) AS maximum_salary,
    MIN(salary) AS minimum_salary,
    COUNT(*) AS employee_count
FROM employee
GROUP BY department;
```

This calculates aggregate values separately for each department.

## 5.8 Aggregate functions with HAVING

```sql
SELECT
    department,
    AVG(salary) AS average_salary
FROM employee
GROUP BY department
HAVING AVG(salary) > 40000;
```

Only departments whose average salary exceeds 40000 are returned.

### Important: Aggregate versus scalar functions

You can combine both types.

```sql
SELECT
    ROUND(AVG(salary), 2) AS average_salary
FROM employee;
```

Execution concept:

1. AVG calculates one aggregate result.
2. ROUND formats that result to two decimal places.

This is a very common SQL pattern.

---

# 6. Date and Time Functions

Date functions are especially important in SQL developer roles because databases frequently store joining dates, transaction dates, order dates and timestamps.

HSQLDB supports SQL-standard date/time expressions and JDBC-compatible functions.

## 6.1 CURRENT_DATE

Returns the current date of the SQL session.

```sql
SELECT CURRENT_DATE
FROM (VALUES(0)) AS t(x);
```

Example result:

```text
2026-11-08
```

It returns a DATE value.

No parentheses are required.

## 6.2 CURRENT_TIME

Returns the current session time with time-zone information.

```sql
SELECT CURRENT_TIME
FROM (VALUES(0)) AS t(x);
```

You can specify fractional-second precision:

```sql
SELECT CURRENT_TIME(3)
FROM (VALUES(0)) AS t(x);
```

## 6.3 CURRENT_TIMESTAMP

Returns the current session timestamp with time-zone information.

```sql
SELECT CURRENT_TIMESTAMP
FROM (VALUES(0)) AS t(x);
```

Example:

```text
2026-11-08 14:30:45.123456+05:30
```

The displayed offset depends on the SQL session time zone.

You can specify precision:

```sql
SELECT CURRENT_TIMESTAMP(3)
FROM (VALUES(0)) AS t(x);
```

## 6.4 SYSDATE

HSQLDB supports:

```sql
SELECT SYSDATE
FROM (VALUES(0)) AS t(x);
```

SYSDATE returns the timestamp of the HyperSQL server rather than the session-local timestamp. It does not include fractional seconds.

### CURRENT_DATE versus CURRENT_TIMESTAMP versus SYSDATE

| Function | Return information |
| --- | --- |
| CURRENT_DATE | Current session date |
| CURRENT_TIME | Current session time with time zone |
| CURRENT_TIMESTAMP | Current session timestamp with time zone |
| LOCALTIMESTAMP | Current session timestamp without time zone |
| SYSDATE | Server timestamp without fractional seconds |
| NOW() | Equivalent to LOCALTIMESTAMP |
| TODAY | Equivalent to CURRENT_DATE |
| CURDATE() | Equivalent to CURRENT_DATE |

**Important:** These are not all interchangeable. Session time zone and server time zone can differ.

## 6.5 YEAR()

Extracts the year from a date or timestamp.

```sql
SELECT YEAR(
    DATE '2026-11-08'
)
FROM (VALUES(0)) AS t(x);
```

Result:

```text
2026
```

## 6.6 MONTH()

Returns the numeric month.

```sql
SELECT MONTH(
    DATE '2026-11-08'
)
FROM (VALUES(0)) AS t(x);
```

Result:

```text
11
```

## 6.7 DAY() / DAYOFMONTH()

Returns the day of the month.

```sql
SELECT DAY(
    DATE '2026-11-08'
)
FROM (VALUES(0)) AS t(x);
```

Result:

```text
8
```

You can also use:

```sql
SELECT DAYOFMONTH(
    DATE '2026-11-08'
)
FROM (VALUES(0)) AS t(x);
```

## 6.8 MONTHNAME()

Returns the month name.

```sql
SELECT MONTHNAME(
    DATE '2026-11-08'
)
FROM (VALUES(0)) AS t(x);
```

Result:

```text
November
```

## 6.9 DAYNAME()

Returns the weekday name.

```sql
SELECT DAYNAME(
    DATE '2026-11-08'
)
FROM (VALUES(0)) AS t(x);
```

Result:

```text
Sunday
```

## 6.10 EXTRACT()

EXTRACT is the standard SQL approach for retrieving individual date/time components.

Syntax:

```sql
EXTRACT(field FROM date_expression)
```

Examples:

```sql
SELECT
    EXTRACT(YEAR FROM CURRENT_DATE),
    EXTRACT(MONTH FROM CURRENT_DATE),
    EXTRACT(DAY FROM CURRENT_DATE)
FROM (VALUES(0)) AS t(x);
```

Other supported fields include:

| Field | Purpose |
| --- | --- |
| YEAR | Year |
| MONTH | Month |
| DAY | Day of month |
| HOUR | Hour |
| MINUTE | Minute |
| SECOND | Second |
| DAY_OF_WEEK | Weekday number |
| DAY_OF_YEAR | Day number in year |
| QUARTER | Quarter |
| WEEK | Week number |
| MONTH_NAME | Month name |
| DAY_NAME | Day name |

Example:

```sql
SELECT
    EXTRACT(QUARTER FROM DATE '2026-11-08'),
    EXTRACT(DAY_OF_YEAR FROM DATE '2026-11-08'),
    EXTRACT(DAY_NAME FROM DATE '2026-11-08')
FROM (VALUES(0)) AS t(x);
```

Results:

```text
4
312
Sunday
```

**Important correction:** HSQLDB does not have a standard `YEARNAME()` function. Use `YEAR()` or `EXTRACT(YEAR FROM ...)` to retrieve a year. Use `TO_CHAR(date, 'YYYY')` when you specifically need the year as text.

## 6.11 DAYOFWEEK()

Returns a numeric weekday.

```sql
SELECT DAYOFWEEK(
    DATE '2026-11-08'
)
FROM (VALUES(0)) AS t(x);
```

HSQLDB numbers Sunday as 1, Monday as 2 and Saturday as 7.

## 6.12 DAYOFYEAR()

Returns the day number within the year.

```sql
SELECT DAYOFYEAR(
    DATE '2026-11-08'
)
FROM (VALUES(0)) AS t(x);
```

Result:

```text
312
```

Useful for annual reporting and date-based analytics.

---

# 7. Date Arithmetic Functions

These functions add, subtract or compare dates.

## 7.1 ADD_MONTHS()

Adds or subtracts a specified number of months.

Syntax:

```sql
ADD_MONTHS(date_expression, number_of_months)
```

Example:

```sql
SELECT ADD_MONTHS(
    DATE '2026-01-15',
    3
)
FROM (VALUES(0)) AS t(x);
```

Result:

```text
2026-04-15 00:00:00
```

### Subtract months

```sql
SELECT ADD_MONTHS(
    DATE '2026-11-08',
    -2
)
FROM (VALUES(0)) AS t(x);
```

Result:

```text
2026-09-08 00:00:00
```

### Important month-end edge case

```sql
SELECT ADD_MONTHS(
    DATE '2026-01-31',
    1
)
FROM (VALUES(0)) AS t(x);
```

Result:

```text
2026-02-28 00:00:00
```

Why?

February does not have 31 days, so ADD_MONTHS adjusts to the last day of the target month.

For a leap year:

```sql
SELECT ADD_MONTHS(
    DATE '2024-01-31',
    1
)
FROM (VALUES(0)) AS t(x);
```

Result:

```text
2024-02-29 00:00:00
```

**Important HSQLDB behaviour:** ADD_MONTHS returns TIMESTAMP(0), even when the input is DATE.

## 7.2 MONTHS_BETWEEN()

Returns the number of months between two date/time values.

Syntax:

```sql
MONTHS_BETWEEN(date1, date2)
```

Example:

```sql
SELECT MONTHS_BETWEEN(
    DATE '2026-04-15',
    DATE '2026-01-15'
)
FROM (VALUES(0)) AS t(x);
```

Result:

```text
3
```

### Reverse order

```sql
SELECT MONTHS_BETWEEN(
    DATE '2026-01-15',
    DATE '2026-04-15'
)
FROM (VALUES(0)) AS t(x);
```

Result:

```text
-3
```

The argument order matters.

### Fractional month calculation

```sql
SELECT MONTHS_BETWEEN(
    DATE '2026-02-15',
    DATE '2026-01-01'
)
FROM (VALUES(0)) AS t(x);
```

The dates are not on the same day of the month or both at month-end.

HSQLDB calculates the fractional part based on 31 days per month.

Conceptually:

$$
1+\frac{14}{31}=1.4516129\ldots
$$

### Month-end rule

If both dates are on the last day of their respective months, HSQLDB returns an exact integral month difference.

For example:

```sql
SELECT MONTHS_BETWEEN(
    DATE '2026-02-28',
    DATE '2026-01-31'
)
FROM (VALUES(0)) AS t(x);
```

Result:

```text
1
```

## 7.3 LAST_DAY()

Returns the last day of the month.

```sql
SELECT LAST_DAY(
    DATE '2026-02-10'
)
FROM (VALUES(0)) AS t(x);
```

Result:

```text
2026-02-28 00:00:00
```

For leap year:

```sql
SELECT LAST_DAY(
    DATE '2024-02-10'
)
FROM (VALUES(0)) AS t(x);
```

Result:

```text
2024-02-29 00:00:00
```

## 7.4 NEXT_DAY()

Returns the next occurrence of a specified weekday.

```sql
SELECT NEXT_DAY(
    DATE '2026-11-08',
    'WEDNESDAY'
)
FROM (VALUES(0)) AS t(x);
```

Returns the next Wednesday after the supplied date.

It means the next occurrence, not the current day if the supplied date is already Wednesday.

## 7.5 TIMESTAMPADD()

Adds a specified time interval to a date or timestamp.

```sql
SELECT TIMESTAMPADD(
    SQL_TSI_DAY,
    10,
    DATE '2026-11-08'
)
FROM (VALUES(0)) AS t(x);
```

Adds 10 days.

Other units include:

- SQL_TSI_DAY
- SQL_TSI_WEEK
- SQL_TSI_MONTH
- SQL_TSI_YEAR
- SQL_TSI_HOUR
- SQL_TSI_MINUTE
- SQL_TSI_SECOND

Example:

```sql
SELECT TIMESTAMPADD(
    SQL_TSI_MONTH,
    3,
    DATE '2026-11-08'
)
FROM (VALUES(0)) AS t(x);
```

Adds three months.

## 7.6 TIMESTAMPDIFF()

Calculates the difference between two date/time values in the requested unit.

```sql
SELECT TIMESTAMPDIFF(
    SQL_TSI_DAY,
    DATE '2026-11-01',
    DATE '2026-11-08'
)
FROM (VALUES(0)) AS t(x);
```

Result:

```text
7
```

Important: HSQLDB evaluates the difference as second argument minus first argument.

```sql
TIMESTAMPDIFF(unit, start_date, end_date)
```

The result is BIGINT.

## 7.7 Date arithmetic using INTERVAL

HSQLDB also supports direct interval arithmetic.

Add days:

```sql
SELECT DATE '2026-11-08' + 5 DAY
FROM (VALUES(0)) AS t(x);
```

Subtract days:

```sql
SELECT DATE '2026-11-08' - 5 DAY
FROM (VALUES(0)) AS t(x);
```

Add months:

```sql
SELECT DATE '2026-11-08' + 2 MONTH
FROM (VALUES(0)) AS t(x);
```

This is standard SQL date/time arithmetic.

**Important difference:** Adding a month interval and using ADD_MONTHS can produce different results at month-end.

For example:

```sql
SELECT
    ADD_MONTHS(DATE '2026-01-31', 1),
    DATE '2026-01-31' + 1 MONTH
FROM (VALUES(0)) AS t(x);
```

ADD_MONTHS adjusts to the last day of February. Direct interval arithmetic preserves the day-of-month where possible and can raise an exception if the resulting date is invalid.

---

# 8. Miscellaneous and NULL-Handling Functions

These functions are used to handle NULL values, retrieve database information and compare expressions.

## 8.1 NVL()

NVL returns an alternative value when the first expression is NULL.

Syntax:

```sql
NVL(expression, replacement_value)
```

Example:

```sql
SELECT NVL(NULL, 0)
FROM (VALUES(0)) AS t(x);
```

Result:

```text
0
```

If the first expression is not NULL, its original value is returned.

```sql
SELECT NVL(100, 0)
FROM (VALUES(0)) AS t(x);
```

Result:

```text
100
```

### Example 1: Numeric replacement

Suppose employee salaries contain NULL values.

```sql
SELECT NVL(salary, 0)
FROM employee;
```

NULL salaries are displayed as zero.

### Example 2: String replacement

```sql
SELECT NVL(fname, 'Not Recorded')
FROM employee;
```

If fname is NULL, the result is:

```text
Not Recorded
```

### Example 3: Aggregate with NVL

```sql
SELECT NVL(MIN(salary), 0)
FROM employee;
```

If all salaries are NULL, MIN returns NULL, and NVL returns zero.

### Important NVL edge case

HSQLDB determines the result type based on the first argument.

For example, if the first expression is INTEGER and the replacement is DOUBLE, the replacement may be converted to INTEGER.

Therefore, use compatible data types.

```sql
SELECT NVL(
    CAST(NULL AS NUMERIC(10,2)),
    0.00
)
FROM (VALUES(0)) AS t(x);
```

## 8.2 COALESCE()

Returns the first non-NULL expression from a list.

Syntax:

```sql
COALESCE(value1, value2, value3, ...)
```

Example:

```sql
SELECT COALESCE(NULL, NULL, 100, 200)
FROM (VALUES(0)) AS t(x);
```

Result:

```text
100
```

Practical example:

```sql
SELECT
    COALESCE(phone, alternate_phone, 'Not Available')
FROM employee;
```

Processing:

1. Check phone.
2. If NULL, check alternate_phone.
3. If both NULL, return Not Available.

**NVL versus COALESCE:**

| NVL | COALESCE |
| --- | --- |
| Two arguments | Two or more arguments |
| HSQLDB-specific extension | SQL standard |
| Returns first argument if non-NULL | Returns first non-NULL argument |
| Result type follows first argument | Uses compatible common type |

For portable SQL, COALESCE is generally preferable.

## 8.3 NULLIF()

Returns NULL when two expressions are equal.

Syntax:

```sql
NULLIF(expression1, expression2)
```

Example:

```sql
SELECT NULLIF(100, 100)
FROM (VALUES(0)) AS t(x);
```

Result:

```text
NULL
```

Another example:

```sql
SELECT NULLIF(100, 200)
FROM (VALUES(0)) AS t(x);
```

Result:

```text
100
```

### Practical example: Prevent division by zero

```sql
SELECT
    amount / NULLIF(quantity, 0)
FROM sales;
```

If quantity is zero, NULLIF returns NULL.

The division therefore returns NULL instead of producing a division-by-zero exception.

## 8.4 NVL2()

HSQLDB also supports NVL2.

Syntax:

```sql
NVL2(expression, value_if_not_null, value_if_null)
```

Example:

```sql
SELECT NVL2(
    NULL,
    'AVAILABLE',
    'NOT AVAILABLE'
)
FROM (VALUES(0)) AS t(x);
```

Result:

```text
NOT AVAILABLE
```

When the first expression is non-NULL:

```sql
SELECT NVL2(
    100,
    'AVAILABLE',
    'NOT AVAILABLE'
)
FROM (VALUES(0)) AS t(x);
```

Result:

```text
AVAILABLE
```

## 8.5 USER

Returns the current database user.

```sql
SELECT USER
FROM (VALUES(0)) AS t(x);
```

Equivalent:

```sql
SELECT CURRENT_USER
FROM (VALUES(0)) AS t(x);
```

Useful for auditing and identifying the current database authorization.

## 8.6 SESSION_USER and SYSTEM_USER

These functions retrieve session identity information.

| Function | Purpose |
| --- | --- |
| USER | Current database user |
| CURRENT_USER | Current authorization user |
| SESSION_USER | Session authorization user |
| SYSTEM_USER | User who initially connected |

In HSQLDB, CURRENT_USER can change through SET AUTHORIZATION, whereas SYSTEM_USER identifies the original connecting user.

---

# 9. CASE Expression

CASE is one of the most important conditional expressions in SQL.

It allows you to implement conditional logic inside SELECT, UPDATE, ORDER BY and other expressions.

There are two main types:

1. Simple CASE expression.
2. Searched CASE expression.

## 9.1 Simple CASE expression

Used when one column or expression needs to be compared against multiple values.

Syntax:

```sql
CASE column_name
    WHEN value1 THEN result1
    WHEN value2 THEN result2
    WHEN value3 THEN result3
    ELSE default_result
END
```

### Example

Suppose employee records have department codes.

```sql
SELECT
    fname,
    department,
    CASE department
        WHEN 'IT' THEN 'Technology'
        WHEN 'HR' THEN 'Human Resources'
        WHEN 'FIN' THEN 'Finance'
        ELSE 'Other Department'
    END AS department_name
FROM employee;
```

Here:

- If department is IT, return Technology.
- If department is HR, return Human Resources.
- If department is FIN, return Finance.
- Otherwise, return Other Department.

### Simple CASE with salary increase

```sql
SELECT
    fname,
    salary,
    CASE department
        WHEN 'IT' THEN salary * 1.20
        WHEN 'HR' THEN salary * 1.10
        WHEN 'FIN' THEN salary * 1.15
        ELSE salary
    END AS revised_salary
FROM employee;
```

The CASE expression compares one column against different values.

## 9.2 Searched CASE expression

Used when you need to compare multiple Boolean conditions.

Syntax:

```sql
CASE
    WHEN condition1 THEN result1
    WHEN condition2 THEN result2
    WHEN condition3 THEN result3
    ELSE default_result
END
```

### Example: Student marks

```sql
SELECT
    student_name,
    marks,
    CASE
        WHEN marks >= 85 AND marks <= 100
            THEN 'Excellent'

        WHEN marks >= 70 AND marks < 85
            THEN 'Very Good'

        WHEN marks >= 50 AND marks < 70
            THEN 'Good'

        WHEN marks >= 35 AND marks < 50
            THEN 'Pass'

        WHEN marks >= 0 AND marks < 35
            THEN 'Fail'

        ELSE 'Invalid Marks'
    END AS result
FROM student;
```

Here, each WHEN condition can contain:

- AND
- OR
- NOT
- BETWEEN
- IN
- Comparison operators
- IS NULL

## 9.3 Simple CASE versus Searched CASE

| Simple CASE | Searched CASE |
| --- | --- |
| Compares one expression against values | Evaluates Boolean conditions |
| Uses CASE column_name | Uses CASE |
| Uses WHEN value | Uses WHEN condition |
| Equality-style matching | Supports ranges and complex conditions |

### Simple CASE

```sql
CASE department
    WHEN 'IT' THEN 'Technology'
    WHEN 'HR' THEN 'Human Resources'
END
```

### Searched CASE

```sql
CASE
    WHEN salary >= 50000 THEN 'High'
    WHEN salary >= 30000 THEN 'Medium'
    ELSE 'Low'
END
```

## 9.4 CASE without ELSE

Consider:

```sql
SELECT
    CASE department
        WHEN 'IT' THEN 'Technology'
        WHEN 'HR' THEN 'Human Resources'
    END
FROM employee;
```

What happens if department is Finance?

Result:

```text
NULL
```

**Important:** If no WHEN condition matches and ELSE is not specified, CASE returns NULL.

## 9.5 CASE with NULL

Consider:

```sql
SELECT
    CASE department
        WHEN NULL THEN 'Not Assigned'
        ELSE 'Assigned'
    END
FROM employee;
```

This does not match NULL department values.

Why?

Because simple CASE comparisons use equality semantics, and NULL = NULL evaluates to UNKNOWN.

Correct:

```sql
SELECT
    CASE
        WHEN department IS NULL THEN 'Not Assigned'
        ELSE 'Assigned'
    END
FROM employee;
```

This is an important interview edge case.

## 9.6 CASE evaluation order

```sql
SELECT
    CASE
        WHEN salary >= 50000 THEN 'HIGH'
        WHEN salary >= 30000 THEN 'MEDIUM'
        WHEN salary >= 10000 THEN 'LOW'
        ELSE 'VERY LOW'
    END
FROM employee;
```

CASE evaluates WHEN conditions in order.

The first matching condition determines the returned result.

Suppose salary is 60000.

Both of these are TRUE:

- salary >= 50000
- salary >= 30000

But the first condition is selected, so the result is HIGH.

**Developer rule:** Place more specific or higher-priority conditions before broader conditions.

## 9.7 Nested CASE

You can place one CASE inside another CASE.

```sql
SELECT
    fname,
    CASE
        WHEN department = 'IT' THEN
            CASE
                WHEN salary >= 50000 THEN 'Senior IT'
                ELSE 'Junior IT'
            END

        WHEN department = 'HR' THEN
            CASE
                WHEN salary >= 40000 THEN 'Senior HR'
                ELSE 'Junior HR'
            END

        ELSE 'Other'
    END AS employee_category
FROM employee;
```

Useful when business rules have multiple levels.

## 9.8 CASE inside UPDATE

CASE can be used to update different records with different values.

```sql
UPDATE employee
SET salary =
    CASE
        WHEN department = 'IT' THEN salary * 1.20
        WHEN department = 'HR' THEN salary * 1.10
        ELSE salary
    END;
```

All employees are updated, but the calculation differs according to their department.

## 9.9 CASE with aggregate functions

```sql
SELECT
    SUM(
        CASE
            WHEN department = 'IT' THEN salary
            ELSE 0
        END
    ) AS it_salary,

    SUM(
        CASE
            WHEN department = 'HR' THEN salary
            ELSE 0
        END
    ) AS hr_salary

FROM employee;
```

This calculates the total salary for IT and HR separately without requiring separate queries.

This is called conditional aggregation.

---

# 10. Important Function Combinations - Real SQL Developer Examples

Knowing individual functions is not enough. You should know how to combine them.

## Example 1: Full name in uppercase

```sql
SELECT UPPER(
    CONCAT(fname, CONCAT(' ', lname))
) AS full_name
FROM employee;
```

## Example 2: First three characters of employee name

```sql
SELECT
    fname,
    SUBSTRING(fname, 1, 3) AS short_name
FROM employee;
```

## Example 3: Extract year and month from joining date

```sql
SELECT
    YEAR(joining_date) AS joining_year,
    MONTH(joining_date) AS joining_month
FROM employee;
```

## Example 4: Display date in DD-MM-YYYY format

```sql
SELECT
    TO_CHAR(joining_date, 'DD-MM-YYYY')
FROM employee;
```

## Example 5: Calculate salary after 15% increment

```sql
SELECT
    emp_id,
    salary,
    ROUND(salary * 1.15, 2) AS revised_salary
FROM employee;
```

## Example 6: Display NULL salary as Not Recorded

```sql
SELECT
    fname,
    NVL(
        CAST(salary AS VARCHAR(20)),
        'Not Recorded'
    ) AS salary
FROM employee;
```

## Example 7: Calculate employee experience in months

```sql
SELECT
    emp_id,
    MONTHS_BETWEEN(
        CURRENT_DATE,
        joining_date
    ) AS experience_months
FROM employee;
```

## Example 8: Calculate retirement eligibility

```sql
SELECT
    fname,
    age,
    CASE
        WHEN age >= 60 THEN 'Eligible'
        ELSE 'Not Eligible'
    END AS retirement_status
FROM employee;
```

## Example 9: Display current user and date

```sql
SELECT
    USER AS database_user,
    CURRENT_DATE AS today,
    CURRENT_TIMESTAMP AS current_time
FROM (VALUES(0)) AS t(x);
```

## Example 10: Calculate average salary and round to two digits

```sql
SELECT ROUND(AVG(salary), 2)
FROM employee;
```

## Example 11: Find names with at least six characters

```sql
SELECT *
FROM employee
WHERE LENGTH(fname) >= 6;
```

## Example 12: Extract last four digits of a phone number

```sql
SELECT
    RIGHT(phone, 4) AS last_four_digits
FROM employee;
```

## Example 13: Replace spaces with hyphens

```sql
SELECT REPLACE(
    'SQL DEVELOPER',
    ' ',
    '-'
)
FROM (VALUES(0)) AS t(x);
```

Result:

```text
SQL-DEVELOPER
```

## Example 14: Display month and weekday names

```sql
SELECT
    MONTHNAME(joining_date),
    DAYNAME(joining_date)
FROM employee;
```

## Example 15: Handle NULL and calculate salary category

```sql
SELECT
    fname,
    CASE
        WHEN salary IS NULL THEN 'Not Recorded'
        WHEN salary >= 100000 THEN 'High'
        WHEN salary >= 50000 THEN 'Medium'
        ELSE 'Low'
    END AS salary_category
FROM employee;
```

---

# 11. HSQLDB Function Quick Reference

This is your revision table.

| Category | Function | Purpose |
| --- | --- | --- |
| Numeric | ABS | Absolute value |
| Numeric | CEIL / CEILING | Round up |
| Numeric | FLOOR | Round down |
| Numeric | ROUND | Round decimal |
| Numeric | TRUNC | Truncate decimal |
| Numeric | MOD | Remainder |
| Numeric | POWER | Exponent |
| Numeric | SQRT | Square root |
| Numeric | SIGN | Sign of number |
| Character | UPPER | Uppercase |
| Character | LOWER | Lowercase |
| Character | CONCAT | Join strings |
| Character | LENGTH | Character count |
| Character | SUBSTRING | Extract characters |
| Character | LEFT | Leftmost characters |
| Character | RIGHT | Rightmost characters |
| Character | TRIM | Remove both-side spaces |
| Character | LTRIM | Remove leading spaces |
| Character | RTRIM | Remove trailing spaces |
| Character | REPLACE | Replace substring |
| Character | POSITION | Find substring position |
| Character | REVERSE | Reverse string |
| Character | REPEAT | Repeat string |
| Character | LPAD | Left padding |
| Character | RPAD | Right padding |
| Conversion | CAST | Change data type |
| Conversion | TO_CHAR | Format number/date as text |
| Conversion | TO_DATE | Parse formatted date text |
| Conversion | TO_TIMESTAMP | Parse timestamp text |
| Conversion | TO_NUMBER | Convert numeric text |
| Aggregate | SUM | Total |
| Aggregate | AVG | Average |
| Aggregate | MAX | Maximum |
| Aggregate | MIN | Minimum |
| Aggregate | COUNT | Count |
| Date | CURRENT_DATE | Current session date |
| Date | CURRENT_TIME | Current session time |
| Date | CURRENT_TIMESTAMP | Current session timestamp |
| Date | SYSDATE | Server timestamp |
| Date | YEAR | Extract year |
| Date | MONTH | Extract month |
| Date | DAY / DAYOFMONTH | Extract day |
| Date | DAYNAME | Weekday name |
| Date | MONTHNAME | Month name |
| Date | DAYOFWEEK | Weekday number |
| Date | DAYOFYEAR | Day number in year |
| Date | ADD_MONTHS | Add/subtract months |
| Date | MONTHS_BETWEEN | Difference in months |
| Date | LAST_DAY | Last day of month |
| Date | NEXT_DAY | Next named weekday |
| Date | TIMESTAMPADD | Add date/time interval |
| Date | TIMESTAMPDIFF | Difference between dates |
| Miscellaneous | NVL | Replace NULL |
| Miscellaneous | NVL2 | Conditional NULL handling |
| Miscellaneous | COALESCE | First non-NULL |
| Miscellaneous | NULLIF | Return NULL if equal |
| Miscellaneous | USER | Current database user |
| Conditional | CASE | Conditional expression |

HSQLDB's official function reference includes additional string, numeric, date/time, general and system functions.

---

# 12. Advanced MCQ Quiz - 15 Questions

(2-Year SQL Developer Level) (15 MCQs)

These questions cover numeric functions, character manipulation, conversion, date functions, aggregates, NULL handling and CASE expressions.

Try answering all questions before viewing the explanations.

**SQL Functions Assessment** (/15 answered)

# 13. Preparation Checklist



## Official HSQLDB references

- HyperSQL 2.7 - Built-in Functions.
- Numeric functions reference.
- Date/time arithmetic reference.
- NULL-handling functions reference.
- System and user functions reference.

**Five concepts I would prioritise for a two-year SQL developer assessment:**

1. ROUND versus TRUNC versus FLOOR for negative numbers.
2. SUBSTRING indexing and string manipulation.
3. TO_CHAR versus CAST versus TO_DATE.
4. ADD_MONTHS versus MONTHS_BETWEEN, especially month-end dates.
5. Aggregate functions combined with NVL, CASE and GROUP BY.

These concepts are useful not only for examinations but also for reporting, data transformation, ETL and production SQL development.

### User

for 2 year sql developer hsql database level give concepts needed from required topics all tricky advanced topics from these explanation and 15 question quiz at end all edge cases order by singe column order by multiple column hw does it work by default asc if you want to specify for multi column order by dept asc salary desc like that positional sorting also explain order by multiple column with same sorting order , with different sorting order positional sorting order by column which is not in select clause,
group by: why grup by total saary paid in each depearmtment use that grup by syntax grup by more than one column example group by mutiple functins in select group by on nullable column, having having clause allws aggreagate function to be used as filter criteria which cant be done using where clause filter result of summaries difference between where and having group by where and having 1 exampe give where faster than having aggregatin functin cannt be used in where dos and donts dos: group by mandatry if list of aggregate and non aggregate column in select statement having after group by only condition on aggregate having, select column in group by clause and affrefate function,

### ChatGPT

# HSQLDB: ORDER BY, GROUP BY and HAVING - Advanced SQL Developer Guide

These clauses are closely connected, but they solve different problems:

- **ORDER BY** sorts the rows returned by a query.
- **GROUP BY** combines rows into groups so aggregate functions can calculate one result per group.
- **HAVING** filters those groups after aggregation.
- **WHERE** filters individual rows before grouping.

We’ll cover syntax, execution order, multiple-column sorting, positional sorting, grouping by multiple columns, NULL handling, aggregate edge cases, and common interview/exam traps.

## 1. ORDER BY - Sorting query results

### 1.1 Basic syntax

```sql
SELECT column1, column2
FROM table_name
ORDER BY column1 [ASC | DESC];
```

- `ASC` means ascending order.
- `DESC` means descending order.
- If you omit the direction, **ASC is the default**.

```sql
SELECT *
FROM employee
ORDER BY salary;
```

Equivalent to:

```sql
SELECT *
FROM employee
ORDER BY salary ASC;
```

Example:

| Employee | Salary |
| --- | --- |
| Arun | 30000 |
| Bala | 45000 |
| Charan | 60000 |
| Divya | 80000 |

For ascending numeric order, the smallest value comes first. For descending order, the largest comes first.

### 1.2 ORDER BY a single column

```sql
SELECT emp_name, salary
FROM employee
ORDER BY salary ASC;
```

Sorts employees by salary, lowest to highest.

```sql
SELECT emp_name, salary
FROM employee
ORDER BY salary DESC;
```

Sorts employees by salary, highest to lowest.

**Important:** Sorting does not change the physical order of records in the table. It changes only the order of rows in that query's result.

### 1.3 ORDER BY multiple columns

This is one of the most important concepts.

```sql
SELECT emp_name, dept_id, salary
FROM employee
ORDER BY dept_id ASC, salary DESC;
```

The database applies sorting in this priority:

1. First, sort by `dept_id` ascending.
2. If multiple employees have the same `dept_id`, sort those employees by `salary` descending.
3. If both `dept_id` and `salary` are equal, their relative order is not guaranteed unless another sort key is specified.

Example input:

| Employee | Department | Salary |
| --- | --- | --- |
| Arun | 20 | 40000 |
| Bala | 10 | 50000 |
| Charan | 20 | 70000 |
| Divya | 10 | 60000 |
| Ezhil | 20 | 50000 |

Query:

```sql
SELECT emp_name, dept_id, salary
FROM employee
ORDER BY dept_id ASC, salary DESC;
```

Result:

| Employee | Department | Salary |
| --- | --- | --- |
| Divya | 10 | 60000 |
| Bala | 10 | 50000 |
| Charan | 20 | 70000 |
| Ezhil | 20 | 50000 |
| Arun | 20 | 40000 |

**Remember:** The first ORDER BY expression has the highest priority. The second is used only to break ties in the first expression.

### 1.4 Multiple columns with the same sorting direction

You can specify the same direction for all columns:

```sql
SELECT *
FROM employee
ORDER BY dept_id ASC, salary ASC, emp_name ASC;
```

All three columns are sorted ascending, in the order written.

You can also omit `ASC`:

```sql
ORDER BY dept_id, salary, emp_name;
```

This is equivalent to:

```sql
ORDER BY dept_id ASC, salary ASC, emp_name ASC;
```

### 1.5 Multiple columns with different sorting directions

Each column can have its own direction.

```sql
SELECT *
FROM employee
ORDER BY dept_id ASC, salary DESC, emp_name ASC;
```

This means:

- Department: ascending.
- Salary within each department: descending.
- Employee name when department and salary are tied: ascending.

The direction of one column does not automatically affect the next column.

### 1.6 Positional sorting - ORDER BY column number

SQL allows you to sort by the position of a column in the SELECT list.

```sql
SELECT emp_name, dept_id, salary
FROM employee
ORDER BY 3 DESC;
```

Here:

| Position | SELECT expression |
| --- | --- |
| 1 | emp_name |
| 2 | dept_id |
| 3 | salary |

Therefore, `ORDER BY 3 DESC` means sort by salary descending.

Multiple positional sort keys are also possible:

```sql
SELECT emp_name, dept_id, salary
FROM employee
ORDER BY 2 ASC, 3 DESC;
```

This means department ascending, then salary descending.

**Critical:** Positional numbers refer to the SELECT-list position, not the physical column number in the table.

### 1.7 ORDER BY a column that is not in SELECT

In a normal non-DISTINCT query, you can generally sort by a column that you do not display.

```sql
SELECT emp_name, salary
FROM employee
ORDER BY dept_id ASC;
```

Here, `dept_id` is used for sorting but is not returned in the result.

You can also sort by an expression:

```sql
SELECT emp_name, salary
FROM employee
ORDER BY salary * 12 DESC;
```

This sorts by calculated annual salary.

You can use an alias for a SELECT expression:

```sql
SELECT emp_name, salary * 12 AS annual_salary
FROM employee
ORDER BY annual_salary DESC;
```

**Important exception:** With `SELECT DISTINCT`, ordering by an expression or column that is not part of the selected result may be restricted. For portable SQL, include the sort expression in the SELECT list or use a derived table.

### 1.8 Sorting NULL values

NULL means the value is unknown or absent. It is not equal to zero or an empty string.

HSQLDB supports explicit NULL placement:

```sql
SELECT emp_name, salary
FROM employee
ORDER BY salary ASC NULLS LAST;
```

```sql
SELECT emp_name, salary
FROM employee
ORDER BY salary DESC NULLS FIRST;
```

You can specify `NULLS FIRST` or `NULLS LAST` to avoid relying on the default NULL ordering.

### 1.9 Important ORDER BY edge cases

- Rows with identical sort-key values have no guaranteed relative order.
- Add a unique tie-breaker when you need deterministic ordering:

```sql
ORDER BY salary DESC, emp_id ASC;
```

- ORDER BY sorts the final result; it does not update table storage.
- ORDER BY can use multiple columns, expressions, aliases and positional references, subject to DISTINCT and query-context restrictions.
- A column's data type affects sorting. Numeric values sort numerically; character values sort according to character comparison/collation rules.

## 2. GROUP BY - Grouping rows for aggregation

### 2.1 Why do we need GROUP BY?

Suppose an employee table contains:

| emp_id | emp_name | dept_id | salary |
| --- | --- | --- | --- |
| 1 | Arun | 10 | 30000 |
| 2 | Bala | 10 | 40000 |
| 3 | Charan | 20 | 50000 |
| 4 | Divya | 20 | 60000 |
| 5 | Ezhil | 30 | 35000 |

Suppose the requirement is:

**Find the total salary paid by each department.**

A simple `SUM(salary)` calculates the total across all qualifying employees:

```sql
SELECT SUM(salary) AS total_salary
FROM employee;
```

But it does not tell us the total for each department separately.

Use `GROUP BY`:

```sql
SELECT dept_id, SUM(salary) AS total_salary
FROM employee
GROUP BY dept_id;
```

Result:

| dept_id | total_salary |
| --- | --- |
| 10 | 70000 |
| 20 | 110000 |
| 30 | 35000 |

What happened?

1. Rows with the same department ID were grouped together.
2. `SUM(salary)` was calculated separately for each group.
3. One result row was returned for each department group.

**Think of GROUP BY as dividing rows into buckets based on common values. Aggregate functions calculate something for each bucket.**

### 2.2 GROUP BY syntax

```sql
SELECT column1, AGGREGATE_FUNCTION(column2)
FROM table_name
[WHERE condition]
GROUP BY column1;
```

Example:

```sql
SELECT dept_id, COUNT(*) AS employee_count
FROM employee
GROUP BY dept_id;
```

This counts employees in each department.

### 2.3 GROUP BY with multiple columns

You can group by more than one column.

```sql
SELECT dept_id, job_role, SUM(salary) AS total_salary
FROM employee
GROUP BY dept_id, job_role;
```

Here, the database groups rows by the **combination** of `dept_id` and `job_role`.

Consider this data:

| Employee | Department | Role | Salary |
| --- | --- | --- | --- |
| Arun | 10 | Developer | 30000 |
| Bala | 10 | Developer | 40000 |
| Charan | 10 | Tester | 35000 |
| Divya | 20 | Developer | 50000 |
| Ezhil | 20 | Tester | 30000 |

Result:

| Department | Role | Total salary |
| --- | --- | --- |
| 10 | Developer | 70000 |
| 10 | Tester | 35000 |
| 20 | Developer | 50000 |
| 20 | Tester | 30000 |

The combination of department and role determines each group.

**Important:** `GROUP BY dept_id, job_role` is not the same as independently grouping by each column. It creates groups for unique combinations.

### 2.4 GROUP BY with multiple aggregate functions

You can use multiple aggregate functions in the same SELECT statement.

```sql
SELECT
    dept_id,
    COUNT(*) AS employee_count,
    SUM(salary) AS total_salary,
    AVG(salary) AS average_salary,
    MAX(salary) AS maximum_salary,
    MIN(salary) AS minimum_salary
FROM employee
GROUP BY dept_id;
```

Each aggregate function is calculated separately for every department group.

For example, if department 10 has salaries 30000 and 40000:

- `COUNT(*)` = 2
- `SUM(salary)` = 70000
- `AVG(salary)` = 35000
- `MAX(salary)` = 40000
- `MIN(salary)` = 30000

You are not required to use only one aggregate function per GROUP BY.

### 2.5 GROUP BY with expressions

You can group by an expression rather than only a column.

Example: group employees by the year they joined.

```sql
SELECT
    YEAR(join_date) AS joining_year,
    COUNT(*) AS employee_count
FROM employee
GROUP BY YEAR(join_date);
```

You can also group by calculations:

```sql
SELECT
    salary / 10000 AS salary_band,
    COUNT(*) AS employee_count
FROM employee
GROUP BY salary / 10000;
```

The expression used in the SELECT list must be compatible with the grouping rules. In this example, the same expression appears in GROUP BY.

### 2.6 Important rule: SELECT columns and GROUP BY

When using ordinary GROUP BY, every non-aggregated expression in the SELECT list must be represented in the grouping expressions.

**Valid:**

```sql
SELECT dept_id, SUM(salary)
FROM employee
GROUP BY dept_id;
```

**Valid:**

```sql
SELECT dept_id, job_role, SUM(salary)
FROM employee
GROUP BY dept_id, job_role;
```

**Invalid:**

```sql
SELECT dept_id, emp_name, SUM(salary)
FROM employee
GROUP BY dept_id;
```

Why is the last query invalid?

Suppose department 10 contains Arun and Bala. The database calculates one total salary for department 10, but which employee name should it display: Arun or Bala?

There is no single unambiguous answer.

Correct it by grouping on both columns:

```sql
SELECT dept_id, emp_name, SUM(salary)
FROM employee
GROUP BY dept_id, emp_name;
```

Or remove `emp_name` if you need only department-level totals.

**Exam trap:** Do not assume HSQLDB will automatically choose one employee name from a group. Follow the grouping rules.

### 2.7 GROUP BY on a nullable column

Suppose the department column allows NULL:

| emp_name | dept_id | salary |
| --- | --- | --- |
| Arun | 10 | 30000 |
| Bala | 10 | 40000 |
| Charan | NULL | 25000 |
| Divya | NULL | 35000 |
| Ezhil | 20 | 50000 |

Query:

```sql
SELECT dept_id, SUM(salary)
FROM employee
GROUP BY dept_id;
```

Result:

| dept_id | SUM(salary) |
| --- | --- |
| 10 | 70000 |
| 20 | 50000 |
| NULL | 60000 |

**Important:** Rows with NULL in the grouping column are grouped together into one NULL group.

This does not mean NULL values are equal in ordinary comparisons. It is the grouping operation that collects them into one group.

To find only the NULL group:

```sql
SELECT dept_id, SUM(salary)
FROM employee
GROUP BY dept_id
HAVING dept_id IS NULL;
```

You can also filter before grouping:

```sql
SELECT dept_id, SUM(salary)
FROM employee
WHERE dept_id IS NULL
GROUP BY dept_id;
```

The second query filters the rows first, then groups the remaining rows.

### 2.8 GROUP BY without aggregate functions

You can use GROUP BY without an aggregate function:

```sql
SELECT dept_id
FROM employee
GROUP BY dept_id;
```

This returns one row per department group.

For this simple requirement, `DISTINCT` is usually clearer:

```sql
SELECT DISTINCT dept_id
FROM employee;
```

These are equivalent for this simple example, including the single NULL result if NULL is present.

### 2.9 GROUP BY does not sort the result

A common misconception is that GROUP BY automatically sorts rows.

```sql
SELECT dept_id, SUM(salary)
FROM employee
GROUP BY dept_id;
```

Do not rely on the result being returned in department order.

If sorting is required:

```sql
SELECT dept_id, SUM(salary) AS total_salary
FROM employee
GROUP BY dept_id
ORDER BY dept_id ASC;
```

Or sort by aggregate result:

```sql
SELECT dept_id, SUM(salary) AS total_salary
FROM employee
GROUP BY dept_id
ORDER BY total_salary DESC;
```

The second query displays the departments with the highest total salary first.

### 2.10 Advanced grouping: ROLLUP, CUBE and GROUPING SETS

HSQLDB also supports advanced grouping operations.

**ROLLUP** produces subtotals for progressively shorter grouping prefixes, plus a grand total.

```sql
SELECT dept_id, job_role, SUM(salary) AS total_salary
FROM employee
GROUP BY ROLLUP(dept_id, job_role);
```

This can produce:

- Department and role totals.
- Department subtotals.
- A grand total.

**CUBE** produces totals for all combinations of the grouping columns.

```sql
SELECT dept_id, job_role, SUM(salary) AS total_salary
FROM employee
GROUP BY CUBE(dept_id, job_role);
```

**GROUPING SETS** lets you specify exactly which grouping combinations you want:

```sql
SELECT dept_id, job_role, SUM(salary) AS total_salary
FROM employee
GROUP BY GROUPING SETS (
    (dept_id),
    (job_role),
    ()
);
```

Here:

- `(dept_id)` gives department totals.
- `(job_role)` gives role totals.
- `()` gives the grand total.

These are useful for reporting and analytical queries. A NULL displayed in a ROLLUP/CUBE result can represent a subtotal or grand-total placeholder, rather than an actual NULL in the source data. HSQLDB provides grouping-related functions to distinguish such cases.

## 3. HAVING - Filtering grouped results

### 3.1 Why do we need HAVING?

Suppose you want:

**Find departments whose total salary is greater than 100000.**

You cannot write:

```sql
SELECT dept_id, SUM(salary)
FROM employee
WHERE SUM(salary) > 100000
GROUP BY dept_id;
```

This is invalid because `WHERE` filters individual rows before grouping. At that stage, the grouped `SUM(salary)` has not been calculated.

Use `HAVING`:

```sql
SELECT dept_id, SUM(salary) AS total_salary
FROM employee
GROUP BY dept_id
HAVING SUM(salary) > 100000;
```

This query:

1. Groups employees by department.
2. Calculates each department's total salary.
3. Removes groups whose total salary is not greater than 100000.

### 3.2 HAVING syntax

```sql
SELECT grouping_column, AGGREGATE_FUNCTION(column)
FROM table_name
[WHERE row_condition]
GROUP BY grouping_column
HAVING group_condition
[ORDER BY expression];
```

Example:

```sql
SELECT dept_id, COUNT(*) AS employee_count
FROM employee
GROUP BY dept_id
HAVING COUNT(*) >= 5;
```

Only departments containing at least five employees are returned.

### 3.3 WHERE vs HAVING - The most important difference

| WHERE | HAVING |
| --- | --- |
| Filters individual rows | Filters groups |
| Applied before GROUP BY | Applied after grouping |
| Normally used for row-level conditions | Used for group-level conditions |
| Cannot directly use aggregate functions in its search condition | Can use aggregate functions |
| Reduces rows entering aggregation | Reduces groups after aggregation |

Example requirement:

Find departments where employees earn more than 30000, and then return departments whose total qualifying salary exceeds 100000.

```sql
SELECT
    dept_id,
    SUM(salary) AS total_salary
FROM employee
WHERE salary > 30000
GROUP BY dept_id
HAVING SUM(salary) > 100000;
```

Understand the order:

1. `WHERE salary > 30000`: Remove employees earning 30000 or less.
2. `GROUP BY dept_id`: Group the remaining employees by department.
3. `SUM(salary)`: Calculate each department's total qualifying salary.
4. `HAVING SUM(salary) > 100000`: Keep only groups meeting the condition.

This is a very common interview and exam pattern.

### 3.4 WHERE is generally more efficient than filtering with HAVING

If a condition can be applied before grouping, prefer `WHERE`.

For example:

```sql
SELECT dept_id, SUM(salary)
FROM employee
WHERE salary > 30000
GROUP BY dept_id;
```

This removes irrelevant employee rows before aggregation.

Do not unnecessarily write:

```sql
SELECT dept_id, SUM(salary)
FROM employee
GROUP BY dept_id
HAVING MIN(salary) > 30000;
```

These two queries are **not equivalent**:

- The WHERE query excludes employees earning 30000 or less, then calculates totals from the remaining employees.
- The HAVING query keeps only departments where every non-NULL salary is greater than 30000, but calculates totals using all rows in those departments.

The query optimizer may also transform queries internally, so do not treat WHERE as guaranteed to be faster in every possible execution plan. The important rule is to apply row-level filters before aggregation when that is the intended logic.

### 3.5 HAVING without GROUP BY

HAVING can also be used in an aggregate query without an explicit GROUP BY.

```sql
SELECT SUM(salary) AS total_salary
FROM employee
HAVING SUM(salary) > 500000;
```

The entire filtered input is treated as one aggregate group.

- If the condition is TRUE, the aggregate row is returned.
- If the condition is FALSE or UNKNOWN, no row is returned.

This is different from a query that groups by department.

### 3.6 HAVING with multiple conditions

You can combine conditions using AND and OR.

```sql
SELECT dept_id, SUM(salary) AS total_salary,
       COUNT(*) AS employee_count
FROM employee
GROUP BY dept_id
HAVING SUM(salary) > 100000
   AND COUNT(*) >= 3;
```

Only departments satisfying both conditions are returned.

Example using OR:

```sql
SELECT dept_id, AVG(salary) AS average_salary
FROM employee
GROUP BY dept_id
HAVING AVG(salary) > 50000
    OR COUNT(*) > 10;
```

### 3.7 HAVING with a non-aggregate grouping column

HAVING is not limited to aggregate expressions.

```sql
SELECT dept_id, SUM(salary) AS total_salary
FROM employee
GROUP BY dept_id
HAVING dept_id IN (10, 20);
```

This filters the groups based on the grouping column.

However, for a simple row-level filter such as department ID, it is usually better to use WHERE:

```sql
SELECT dept_id, SUM(salary) AS total_salary
FROM employee
WHERE dept_id IN (10, 20)
GROUP BY dept_id;
```

### 3.8 Can HAVING use SELECT aliases?

For maximum clarity and portability, write the aggregate expression in HAVING:

```sql
SELECT dept_id, SUM(salary) AS total_salary
FROM employee
GROUP BY dept_id
HAVING SUM(salary) > 100000;
```

Do not assume every SQL engine permits SELECT aliases in HAVING. Using the original expression avoids that compatibility issue.

### 3.9 Can we use aggregate functions in WHERE?

Not directly in the same query level.

**Invalid:**

```sql
SELECT dept_id, SUM(salary)
FROM employee
WHERE SUM(salary) > 100000
GROUP BY dept_id;
```

**Correct with HAVING:**

```sql
SELECT dept_id, SUM(salary)
FROM employee
GROUP BY dept_id
HAVING SUM(salary) > 100000;
```

**Alternative using a subquery:**

```sql
SELECT *
FROM (
    SELECT dept_id, SUM(salary) AS total_salary
    FROM employee
    GROUP BY dept_id
) AS department_totals
WHERE total_salary > 100000;
```

The outer WHERE works because the inner query has already calculated `total_salary`.

## 4. Aggregate-function edge cases you must know

These are especially important when using GROUP BY and HAVING.

### 4.1 COUNT(*) vs COUNT(column)

Consider:

| emp_id | dept_id | salary |
| --- | --- | --- |
| 1 | 10 | 30000 |
| 2 | 10 | NULL |
| 3 | 10 | 40000 |

```sql
SELECT
    COUNT(*) AS total_rows,
    COUNT(salary) AS salary_count
FROM employee
WHERE dept_id = 10;
```

Result:

| total_rows | salary_count |
| --- | --- |
| 3 | 2 |

- `COUNT(*)` counts rows, including rows containing NULL.
- `COUNT(salary)` counts only non-NULL salary values.

### 4.2 SUM and AVG ignore NULL values

For salaries `30000`, `NULL`, and `40000`:

```sql
SELECT SUM(salary), AVG(salary)
FROM employee;
```

- SUM = 70000
- AVG = 35000

NULL is excluded from the aggregate calculation.

### 4.3 What if every value is NULL?

```sql
SELECT
    COUNT(salary),
    SUM(salary),
    AVG(salary),
    MIN(salary),
    MAX(salary)
FROM employee
WHERE dept_id = 99;
```

If no rows match, the result is:

| COUNT(salary) | SUM(salary) | AVG(salary) | MIN(salary) | MAX(salary) |
| --- | --- | --- | --- | --- |
| 0 | NULL | NULL | NULL | NULL |

The same aggregate behavior applies when the input rows exist but every salary is NULL: COUNT(column) is zero, and the other listed aggregates return NULL.

`COUNT(*)` on an empty input also returns zero.

### 4.4 COUNT(DISTINCT column)

```sql
SELECT COUNT(DISTINCT dept_id)
FROM employee;
```

Counts the number of distinct non-NULL department IDs.

If department IDs are:

`10, 10, 20, 20, NULL`

The result is `2`.

### 4.5 SUM(DISTINCT column)

```sql
SELECT SUM(DISTINCT salary)
FROM employee;
```

This adds each distinct non-NULL salary value only once.

Suppose salaries are:

`30000, 30000, 40000, NULL`

Then:

- `SUM(salary)` = 100000
- `SUM(DISTINCT salary)` = 70000

This is not the same as summing all employee salaries. Be careful when using DISTINCT inside aggregate functions.

### 4.6 Aggregate functions with GROUP BY and HAVING

```sql
SELECT
    dept_id,
    COUNT(*) AS employee_count,
    COUNT(salary) AS employees_with_salary,
    SUM(salary) AS total_salary,
    AVG(salary) AS average_salary
FROM employee
GROUP BY dept_id
HAVING COUNT(*) >= 2
   AND SUM(salary) > 50000;
```

This demonstrates multiple aggregates in SELECT and multiple aggregate conditions in HAVING.

## 5. Logical query execution order

This order helps explain why WHERE cannot use an aggregate from the same query level.

A useful simplified logical order is:

| Order | Clause / operation | Purpose |
| --- | --- | --- |
| 1 | FROM | Identify source tables |
| 2 | JOIN / ON | Combine matching rows |
| 3 | WHERE | Filter individual rows |
| 4 | GROUP BY | Create groups |
| 5 | Aggregate calculations | Calculate SUM, COUNT, AVG, etc. |
| 6 | HAVING | Filter groups |
| 7 | SELECT | Produce selected expressions |
| 8 | DISTINCT | Remove duplicate result rows |
| 9 | ORDER BY | Sort the final result |
| 10 | OFFSET / FETCH | Limit or skip result rows |

This is a **logical explanation**, not a guarantee of the physical execution plan chosen by the optimizer.

### Complete example

Requirement:

- Consider employees earning more than 25000.
- Group them by department.
- Calculate employee count, total salary and average salary.
- Keep departments with at least two qualifying employees and total salary above 80000.
- Sort total salary from highest to lowest.

```sql
SELECT
    dept_id,
    COUNT(*) AS employee_count,
    SUM(salary) AS total_salary,
    AVG(salary) AS average_salary
FROM employee
WHERE salary > 25000
GROUP BY dept_id
HAVING COUNT(*) >= 2
   AND SUM(salary) > 80000
ORDER BY total_salary DESC;
```

This one query combines WHERE, GROUP BY, multiple aggregate functions, HAVING and ORDER BY.

## 6. Dos and don'ts - Exam revision

| Do | Don't |
| --- | --- |
| Use GROUP BY to calculate aggregates per group | Expect SUM without GROUP BY to calculate one total per department |
| Include every non-aggregated SELECT expression in GROUP BY | Select an arbitrary employee name from a department group |
| Use multiple grouping columns for unique combinations | Assume `GROUP BY a, b` independently groups a and b |
| Use WHERE for row-level filters | Put SUM, AVG or COUNT directly in WHERE |
| Use HAVING for aggregate-based filters | Use HAVING unnecessarily for simple row filters |
| Use ORDER BY for guaranteed result ordering | Assume GROUP BY sorts the result |
| Use explicit ASC/DESC when clarity matters | Assume all sort columns inherit the first column's direction |
| Use a tie-breaker for deterministic sorting | Assume equal sort keys have a guaranteed order |
| Handle NULL using `IS NULL` / `IS NOT NULL` | Compare NULL using `= NULL` |
| Remember COUNT(*) includes NULL-containing rows | Assume COUNT(*) and COUNT(column) are interchangeable |

**HSQLDB-specific notes:** HSQLDB's documented default ORDER BY direction is ASC, and its default NULL placement is NULLS FIRST. Specify NULLS FIRST or NULLS LAST explicitly when the ordering matters. It supports positional and expression-based ORDER BY, and supports ordering by a column not included in the SELECT list.

## 7. Advanced 15-question MCQ quiz

(2-year SQL developer level) (15 questions)

These questions test query output, execution order, NULL behaviour, sorting priorities, aggregation and common syntax traps.

**Your quiz** /15 answered

## 8. Official HSQLDB reference

For further practice, use the official HyperSQL 2.7 documentation:

- Data Access and Change - GROUP BY, HAVING, ORDER BY and aggregate functions
- HSQLDB JDBC metadata - ORDER BY and GROUP BY support

**Next important topic to master:** SQL JOINs with GROUP BY and HAVING. For example, calculating department-wise employee counts and salaries by joining `employee` and `department` tables.

### User

for 2 year sql developer hsql database level give concepts needed from required topics all tricky advanced topics from these explanation and 15 question quiz at end all edge cases union union all intersect except combine similar tables data rules for set operatin same number of columns correct order same datatype intersect except when to use each give

### ChatGPT

# HSQLDB: Set Operators - UNION, UNION ALL, INTERSECT and EXCEPT

Set operators combine the results of two or more `SELECT` queries into one result set.

For a SQL developer, these are essential when combining data from:

- Similar tables from different years.
- Current and archived employee records.
- Customers from different branches.
- Matching records between two datasets.
- Records that exist in one query result but not another.

The four operators you need to master are:

| Operator | Purpose |
| --- | --- |
| `UNION` | Combines results and removes duplicates |
| `UNION ALL` | Comb |

### User

for 2 year sql developer hsql database level give concepts needed from required topics all tricky advanced topics from these explanation and 15 question quiz at end all edge cases why joins, cross join when why syntax, inner join why when syntax examples inner join with cndition include condition in on since it is single step where is 2 step process self join why wen examples common syntax explain working of each join in algorithm full outer join left outer join right outer join when where syntax examples use cases outer joins with condition like is null not null condition also

### ChatGPT

# HSQLDB: SQL JOINs - Complete Advanced Guide for a 2-Year SQL Developer

A JOIN combines rows from two or more tables based on a relationship or matching condition.

JOINs are essential when data is stored in separate, related tables rather than duplicated in one large table.

For example, consider an employee management database:

**Department table**

| dept_id | dept_name |
| --- | --- |
| 10 | IT |
| 20 | HR |
| 30 | Finance |
| 40 | Marketing |

**Employee table**

| emp_id | emp_name | dept_id | salary |
| --- | --- | --- | --- |
| 1 | Arun | 10 | 50000 |
| 2 | Bala | 10 | 60000 |
| 3 | Charan | 20 | 45000 |
| 4 | Divya | 30 | 55000 |
| 5 | Ezhil | NULL | 40000 |
| 6 | Farah | 50 | 35000 |

Notice:

- Department 40 has no employees.
- Employee Ezhil has no department assigned.
- Employee Farah has department ID 50, which does not exist in the department table.

These examples will help us understand every JOIN, including unmatched rows and NULL behaviour.

## 1. Why do we need JOINs?

Suppose you need to display:

| Employee | Department name |
| --- | --- |
| Arun | IT |
| Bala | IT |
| Charan | HR |
| Divya | Finance |

The employee table contains `dept_id`, but it does not contain the department name.

The department table contains the department name.

We need to combine these two tables.

```sql
SELECT
    e.emp_name,
    d.dept_name
FROM employee e
INNER JOIN department d
    ON e.dept_id = d.dept_id;
```

Result:

| emp_name | dept_name |
| --- | --- |
| Arun | IT |
| Bala | IT |
| Charan | HR |
| Divya | Finance |

This is why JOINs are needed: they retrieve related information stored in different tables.

**Important terminology**

- Primary key: uniquely identifies a row in a table.
- Foreign key: references a key in another table.
- Join key: the column or expression used to match rows. It is often a PK/FK relationship, but does not have to be one.

A JOIN does not require a declared foreign key constraint. You can join tables using any compatible matching expressions.

## 2. CROSS JOIN - Cartesian product

### 2.1 What is CROSS JOIN?

A CROSS JOIN combines every row from the first table with every row from the second table.

Suppose:

**Employee**

| emp_name |
| --- |
| Arun |
| Bala |

**Project**

| project_name |
| --- |
| Banking |
| Retail |
| Healthcare |

Query:

```sql
SELECT
    e.emp_name,
    p.project_name
FROM employee e
CROSS JOIN project p;
```

Result:

| emp_name | project_name |
| --- | --- |
| Arun | Banking |
| Arun | Retail |
| Arun | Healthcare |
| Bala | Banking |
| Bala | Retail |
| Bala | Healthcare |

(Cartesian product)

### 2.2 How does CROSS JOIN work internally?

If the first table has `M` rows and the second table has `N` rows:

$$
\text{Result rows} = M \times N
$$

Example:

- Employee table: 2 rows.
- Project table: 3 rows.
- Result: 2 × 3 = 6 rows.

The database pairs each row of the first table with every row of the second table.

### 2.3 CROSS JOIN syntax

```sql
SELECT columns
FROM table1
CROSS JOIN table2;
```

You can join more than two tables:

```sql
SELECT *
FROM employee e
CROSS JOIN project p
CROSS JOIN location l;
```

If the tables contain 2, 3 and 4 rows, the result has 24 rows.

### 2.4 When do we use CROSS JOIN?

Common real-world use cases:

1. Generate all possible combinations of products and sizes.
2. Generate every employee and every available training course.
3. Create a calendar of dates and departments.
4. Generate combinations for test data.
5. Compare all possible pairs when that is genuinely required.

Example: Generate all product-size combinations.

```sql
SELECT
    p.product_name,
    s.size_name
FROM product p
CROSS JOIN product_size s;
```

If there are 10 products and 5 sizes, the result has 50 combinations.

### 2.5 CROSS JOIN vs INNER JOIN

```sql
SELECT *
FROM employee e
CROSS JOIN department d;
```

Produces every possible pair.

```sql
SELECT *
FROM employee e
INNER JOIN department d
    ON e.dept_id = d.dept_id;
```

Produces only matching pairs.

**Tricky point:** CROSS JOIN does not require an ON condition. INNER JOIN requires a join condition for the intended matching relationship.

You can technically filter a CROSS JOIN using WHERE:

```sql
SELECT *
FROM employee e
CROSS JOIN department d
WHERE e.dept_id = d.dept_id;
```

For an ordinary equality join, this produces the same matching rows as the INNER JOIN example, but writing INNER JOIN makes the intended relationship clearer.

## 3. INNER JOIN - Matching rows from both tables

### 3.1 What is INNER JOIN?

An INNER JOIN returns only rows that satisfy the join condition in both tables.

```sql
SELECT
    e.emp_name,
    d.dept_name
FROM employee e
INNER JOIN department d
    ON e.dept_id = d.dept_id;
```

The database compares the department ID from each employee with the department ID in the department table.

If a matching department exists, the combined row is returned.

If there is no match, the employee or department is excluded.

### 3.2 How does INNER JOIN work?

Conceptually, for every employee row:

1. Find department rows satisfying the ON condition.
2. If a matching department exists, return the combined row.
3. If no department matches, do not return that employee from an INNER JOIN.
4. Repeat for the remaining employee rows.

This is a conceptual explanation. The database optimizer can use different physical algorithms, such as nested-loop, hash or merge joins, depending on the query and available indexes.

### 3.3 INNER JOIN with additional conditions

Suppose you want employees belonging to IT and earning more than 50000.

```sql
SELECT
    e.emp_name,
    e.salary,
    d.dept_name
FROM employee e
INNER JOIN department d
    ON e.dept_id = d.dept_id
   AND d.dept_name = 'IT'
WHERE e.salary > 50000;
```

Here:

- `e.dept_id = d.dept_id` matches employee and department.
- `d.dept_name = 'IT'` is another join-side condition.
- `e.salary > 50000` filters the resulting matching rows.

For INNER JOIN, moving a suitable condition between ON and WHERE can produce the same result. However, the distinction becomes extremely important with OUTER JOINs.

### 3.4 ON condition vs WHERE condition

Consider:

```sql
SELECT e.emp_name, d.dept_name
FROM employee e
INNER JOIN department d
    ON e.dept_id = d.dept_id
WHERE d.dept_name = 'IT';
```

This is also valid.

For INNER JOIN, the following can be equivalent:

```sql
SELECT e.emp_name, d.dept_name
FROM employee e
INNER JOIN department d
    ON e.dept_id = d.dept_id
   AND d.dept_name = 'IT';
```

Why?

An INNER JOIN only retains rows where the join condition succeeds. Both versions ultimately restrict the result to matching IT employees.

**Important:** This equivalence does not generally hold for LEFT JOIN or RIGHT JOIN.

### 3.5 Multiple join conditions

You can match using more than one column:

```sql
SELECT *
FROM employee e
INNER JOIN employee_assignment a
    ON e.emp_id = a.emp_id
   AND e.dept_id = a.dept_id;
```

Both conditions must be true because they are connected using AND.

You can also use OR:

```sql
SELECT *
FROM employee e
INNER JOIN department d
    ON e.dept_id = d.dept_id
    OR e.alternate_dept_id = d.dept_id;
```

Be careful: OR can produce multiple matching rows for one employee if both department IDs match different rows.

### 3.6 What happens when NULL is used in an INNER JOIN?

Suppose:

```text
employee.dept_id = NULL
department.dept_id = NULL
```

The condition:

```sql
e.dept_id = d.dept_id
```

does not evaluate to TRUE when both values are NULL. It evaluates to UNKNOWN.

Therefore, these two rows do not match under ordinary equality.

If NULL-to-NULL matching is specifically required, use an explicit NULL-aware condition:

```sql
ON (
    e.dept_id = d.dept_id
    OR (e.dept_id IS NULL AND d.dept_id IS NULL)
)
```

Use this only when NULL represents the same meaningful category in both tables.

## 4. SELF JOIN - Joining a table with itself

### 4.1 What is a SELF JOIN?

A SELF JOIN means joining a table to itself.

It is useful when rows in the same table are related to other rows in that same table.

Example: An employee table contains manager IDs.

| emp_id | emp_name | manager_id |
| --- | --- | --- |
| 1 | Arun | NULL |
| 2 | Bala | 1 |
| 3 | Charan | 1 |
| 4 | Divya | 2 |
| 5 | Ezhil | 2 |

Here:

- Arun is a manager.
- Bala and Charan report to Arun.
- Divya and Ezhil report to Bala.

We want to display employee name and manager name.

### 4.2 SELF JOIN syntax

```sql
SELECT
    e.emp_name AS employee_name,
    m.emp_name AS manager_name
FROM employee e
LEFT JOIN employee m
    ON e.manager_id = m.emp_id;
```

Result:

| employee_name | manager_name |
| --- | --- |
| Arun | NULL |
| Bala | Arun |
| Charan | Arun |
| Divya | Bala |
| Ezhil | Bala |

### 4.3 How does SELF JOIN work?

We give the same table two aliases:

- `e` represents the employee.
- `m` represents the manager.

The condition:

```sql
e.manager_id = m.emp_id
```

matches the employee's manager ID with another row's employee ID.

The aliases are essential to distinguish the two logical roles of the same table.

### 4.4 Why use LEFT JOIN instead of INNER JOIN?

If we use INNER JOIN:

```sql
SELECT e.emp_name, m.emp_name AS manager_name
FROM employee e
INNER JOIN employee m
    ON e.manager_id = m.emp_id;
```

Arun will not appear because Arun has no manager.

If you need employees who do not have managers too, use LEFT JOIN.

### 4.5 Other SELF JOIN use cases

- Employee-manager hierarchy.
- Product comparison within the same product table.
- Find employees earning more than their managers.
- Find customers who share the same city.
- Find pairs of products with the same category.
- Compare a current row against a previous or related row.

Example: Employees earning more than their managers.

```sql
SELECT
    e.emp_name AS employee_name,
    e.salary AS employee_salary,
    m.emp_name AS manager_name,
    m.salary AS manager_salary
FROM employee e
INNER JOIN employee m
    ON e.manager_id = m.emp_id
WHERE e.salary > m.salary;
```

**Tricky point:** A SELF JOIN is not a separate JOIN type in terms of matching behaviour. It is a table joining itself, and it can use INNER JOIN, LEFT JOIN or other join forms.

## 5. LEFT OUTER JOIN - Keep all rows from the left table

### 5.1 What is LEFT JOIN?

A LEFT OUTER JOIN returns:

1. Every matching row from the left table and right table.
2. Every unmatched row from the left table.
3. NULL values for the right-table columns when no matching row exists.

`LEFT JOIN` and `LEFT OUTER JOIN` mean the same thing.

### 5.2 Syntax

```sql
SELECT columns
FROM table1
LEFT JOIN table2
    ON table1.common_column = table2.common_column;
```

### 5.3 Example

Remember our tables:

**Department**

| dept_id | dept_name |
| --- | --- |
| 10 | IT |
| 20 | HR |
| 30 | Finance |
| 40 | Marketing |

**Employee**

| emp_id | emp_name | dept_id |
| --- | --- | --- |
| 1 | Arun | 10 |
| 2 | Bala | 10 |
| 3 | Charan | 20 |
| 4 | Divya | 30 |
| 5 | Ezhil | NULL |
| 6 | Farah | 50 |

Query:

```sql
SELECT
    d.dept_id,
    d.dept_name,
    e.emp_name
FROM department d
LEFT JOIN employee e
    ON d.dept_id = e.dept_id;
```

Result:

| dept_id | dept_name | emp_name |
| --- | --- | --- |
| 10 | IT | Arun |
| 10 | IT | Bala |
| 20 | HR | Charan |
| 30 | Finance | Divya |
| 40 | Marketing | NULL |

Notice Marketing is returned even though it has no employee.

### 5.4 How does LEFT JOIN work? Algorithm

Conceptually:

1. Take a row from the left table.
2. Search the right table for all rows satisfying the ON condition.
3. If matches exist, produce one result row for each match.
4. If no matches exist, produce one row with NULLs for all right-table columns.
5. Repeat for every left-table row.

The unmatched left-side row is not discarded.

### 5.5 When do we use LEFT JOIN?

Common use cases:

- Find all departments, including departments without employees.
- Find all customers, including customers without orders.
- Find all products, including products never sold.
- Find all students, including students who have not registered for courses.
- Find all accounts, including accounts with no transactions.

### 5.6 LEFT JOIN with IS NULL - Find unmatched records

One of the most important patterns in SQL.

Requirement: Find departments that have no employees.

```sql
SELECT
    d.dept_id,
    d.dept_name
FROM department d
LEFT JOIN employee e
    ON d.dept_id = e.dept_id
WHERE e.emp_id IS NULL;
```

Result:

| dept_id | dept_name |
| --- | --- |
| 40 | Marketing |

Why does this work?

- Matching departments have an employee ID.
- Unmatched departments receive NULL for every right-table column.
- `WHERE e.emp_id IS NULL` retains only unmatched departments.

This pattern is commonly called an **anti-join**.

**Important:** Check a right-table column that cannot be NULL in a genuine matching row, preferably its primary key. Do not use a nullable column such as `e.salary` to identify unmatched rows, because a matching employee could genuinely have a NULL salary.

### 5.7 LEFT JOIN with IS NOT NULL

Requirement: Find departments that have at least one employee.

```sql
SELECT
    d.dept_id,
    d.dept_name,
    e.emp_name
FROM department d
LEFT JOIN employee e
    ON d.dept_id = e.dept_id
WHERE e.emp_id IS NOT NULL;
```

This removes the NULL-extended rows and retains matching records.

For this requirement, INNER JOIN would generally be simpler.

### 5.8 Critical edge case: ON vs WHERE with LEFT JOIN

This is a major interview topic.

Requirement: Display every department, but show only employees earning more than 50000.

**Query A - Condition in ON**

```sql
SELECT
    d.dept_name,
    e.emp_name,
    e.salary
FROM department d
LEFT JOIN employee e
    ON d.dept_id = e.dept_id
   AND e.salary > 50000;
```

Meaning:

- Keep every department.
- Match only employees whose salary exceeds 50000.
- If a department has no employee meeting that condition, return it with NULL employee columns.

**Query B - Condition in WHERE**

```sql
SELECT
    d.dept_name,
    e.emp_name,
    e.salary
FROM department d
LEFT JOIN employee e
    ON d.dept_id = e.dept_id
WHERE e.salary > 50000;
```

Meaning:

- First produce the LEFT JOIN result.
- Then remove rows where the salary condition is not TRUE.
- Unmatched departments have NULL salary, so they are removed.
- Departments with employees but no employee earning over 50000 are also removed.

(Important difference)

| Condition location | Effect |
| --- | --- |
| `ON ... AND e.salary > 50000` | Preserves every department |
| `WHERE e.salary > 50000` | Removes departments without a qualifying employee |

**Rule:** If you want to preserve unmatched rows from the left table, be careful when putting right-table conditions in WHERE.

### 5.9 A common mistake: WHERE right_column IS NULL

Suppose you want departments with no employees.

This is correct:

```sql
SELECT d.dept_name
FROM department d
LEFT JOIN employee e
    ON d.dept_id = e.dept_id
WHERE e.emp_id IS NULL;
```

But this is not equivalent:

```sql
SELECT d.dept_name
FROM department d
LEFT JOIN employee e
    ON d.dept_id = e.dept_id
WHERE e.salary IS NULL;
```

The second query can also return departments with employees whose salary is actually NULL. It is not a reliable unmatched-row test.

## 6. RIGHT OUTER JOIN - Keep all rows from the right table

### 6.1 What is RIGHT JOIN?

RIGHT OUTER JOIN returns:

1. All matching rows.
2. All unmatched rows from the right table.
3. NULL values for columns from the left table when no match exists.

### 6.2 Syntax

```sql
SELECT columns
FROM table1
RIGHT JOIN table2
    ON table1.common_column = table2.common_column;
```

### 6.3 Example

Requirement: Display all employees and all departments, preserving every employee, including those without a valid department.

```sql
SELECT
    d.dept_name,
    e.emp_name
FROM department d
RIGHT JOIN employee e
    ON d.dept_id = e.dept_id;
```

Result:

| dept_name | emp_name |
| --- | --- |
| IT | Arun |
| IT | Bala |
| HR | Charan |
| Finance | Divya |
| NULL | Ezhil |
| NULL | Farah |

Notice:

- Ezhil has no department ID.
- Farah has department ID 50, which does not exist in the department table.
- Both employees are preserved because employee is on the right side.

### 6.4 How does RIGHT JOIN work?

Conceptually:

1. Take each row from the right table.
2. Find all matching rows in the left table.
3. Return each matching combination.
4. If no left-table match exists, return the right row with NULLs in the left-table columns.
5. Repeat for every right-table row.

### 6.5 RIGHT JOIN with IS NULL

Requirement: Find employees who do not have a matching department.

```sql
SELECT
    e.emp_id,
    e.emp_name,
    e.dept_id
FROM department d
RIGHT JOIN employee e
    ON d.dept_id = e.dept_id
WHERE d.dept_id IS NULL;
```

Result:

| emp_id | emp_name | dept_id |
| --- | --- | --- |
| 5 | Ezhil | NULL |
| 6 | Farah | 50 |

You could use `d.dept_id IS NULL` here because a matched department's primary key cannot be NULL.

### 6.6 Can RIGHT JOIN be rewritten as LEFT JOIN?

Yes. Swap the table order.

This:

```sql
SELECT *
FROM department d
RIGHT JOIN employee e
    ON d.dept_id = e.dept_id;
```

Can be rewritten as:

```sql
SELECT *
FROM employee e
LEFT JOIN department d
    ON e.dept_id = d.dept_id;
```

Both preserve all employees.

Many developers prefer LEFT JOIN because keeping the preserved table on the left often makes complex queries easier to read.

## 7. FULL OUTER JOIN - Keep unmatched rows from both tables

### 7.1 What is FULL OUTER JOIN?

FULL OUTER JOIN combines the behaviour of LEFT JOIN and RIGHT JOIN.

It returns:

1. Matching rows.
2. Unmatched rows from the left table.
3. Unmatched rows from the right table.

### 7.2 Syntax

```sql
SELECT columns
FROM table1
FULL OUTER JOIN table2
    ON table1.common_column = table2.common_column;
```

`FULL JOIN` and `FULL OUTER JOIN` are equivalent.

### 7.3 Example

```sql
SELECT
    d.dept_id AS department_id,
    d.dept_name,
    e.emp_id,
    e.emp_name,
    e.dept_id AS employee_department_id
FROM department d
FULL OUTER JOIN employee e
    ON d.dept_id = e.dept_id;
```

Result:

| department_id | dept_name | emp_id | emp_name | employee_department_id |
| --- | --- | --- | --- | --- |
| 10 | IT | 1 | Arun | 10 |
| 10 | IT | 2 | Bala | 10 |
| 20 | HR | 3 | Charan | 20 |
| 30 | Finance | 4 | Divya | 30 |
| 40 | Marketing | NULL | NULL | NULL |
| NULL | NULL | 5 | Ezhil | NULL |
| NULL | NULL | 6 | Farah | 50 |

### 7.4 How does FULL OUTER JOIN work?

Conceptually:

1. Find all matching combinations.
2. Add every unmatched row from the left table, filling right-side columns with NULL.
3. Add every unmatched row from the right table, filling left-side columns with NULL.

This means neither table loses its unmatched records.

### 7.5 When do we use FULL OUTER JOIN?

Common use cases:

- Compare employee records between two systems.
- Reconcile customer records between old and new databases.
- Compare source and target tables after data migration.
- Find records missing from either dataset.
- Compare two lists where both unmatched sides matter.

### 7.6 FULL OUTER JOIN with IS NULL

Find rows that exist in only one table, not both.

```sql
SELECT
    d.dept_id,
    d.dept_name,
    e.emp_id,
    e.emp_name
FROM department d
FULL OUTER JOIN employee e
    ON d.dept_id = e.dept_id
WHERE d.dept_id IS NULL
   OR e.emp_id IS NULL;
```

This removes matching rows and keeps unmatched records from either side.

It is useful for reconciliation.

### 7.7 FULL OUTER JOIN with IS NOT NULL

If you write:

```sql
WHERE d.dept_id IS NOT NULL
  AND e.emp_id IS NOT NULL
```

you retain only rows where both sides are present. For a normal equality join on these keys, that is effectively the matched portion of the FULL JOIN.

If you only need matched records, INNER JOIN is clearer.

## 8. Compare all JOIN types

Using our employee and department examples:

**Which rows does each JOIN preserve?**

Matching rows

Unmatched rows preserved

---

Matching rows are returned by all four joins. Preservation refers to unmatched rows.

| JOIN | Matched rows | Unmatched left | Unmatched right |
| --- | --- | --- | --- |
| INNER | Yes | No | No |
| LEFT | Yes | Yes | No |
| RIGHT | Yes | No | Yes |
| FULL OUTER | Yes | Yes | Yes |
| CROSS | Every possible pair | Not applicable | Not applicable |

## 9. Advanced JOIN behaviour and edge cases

### 9.1 One-to-one, one-to-many and many-to-many joins

The number of rows produced by a JOIN depends on how many matches each row has.

**One-to-one:** One employee matches one employee profile.

```sql
SELECT e.emp_name, p.address
FROM employee e
INNER JOIN employee_profile p
    ON e.emp_id = p.emp_id;
```

**One-to-many:** One department can have multiple employees.

```sql
SELECT d.dept_name, e.emp_name
FROM department d
INNER JOIN employee e
    ON d.dept_id = e.dept_id;
```

One department row may appear multiple times, once for each matching employee.

**Many-to-many:** Students can enrol in multiple courses, and each course can have multiple students.

Typically, this is modelled using a junction table:

- `student(student_id, student_name)`
- `course(course_id, course_name)`
- `student_course(student_id, course_id)`

```sql
SELECT
    s.student_name,
    c.course_name
FROM student s
INNER JOIN student_course sc
    ON s.student_id = sc.student_id
INNER JOIN course c
    ON sc.course_id = c.course_id;
```

### 9.2 Why do duplicate rows appear after JOIN?

Suppose:

**Department**

| dept_id | dept_name |
| --- | --- |
| 10 | IT |

**Employee**

| emp_id | emp_name | dept_id |
| --- | --- | --- |
| 1 | Arun | 10 |
| 2 | Bala | 10 |
| 3 | Charan | 10 |

Query:

```sql
SELECT d.dept_name, e.emp_name
FROM department d
INNER JOIN employee e
    ON d.dept_id = e.dept_id;
```

Result:

| dept_name | emp_name |
| --- | --- |
| IT | Arun |
| IT | Bala |
| IT | Charan |

The department name repeats. This is not an accidental duplicate: it represents three different employee-department relationships.

**Important:** JOIN does not automatically remove duplicates. `DISTINCT` can remove duplicate selected rows, but do not use it to hide an incorrect join condition.

### 9.3 What if both tables contain duplicate join keys?

Suppose the left table has two rows with `id = 10` and the right table has three rows with `id = 10`.

The matching result contains:

$$
2 \times 3 = 6 \text{ rows}
$$

Every left-side row matches every right-side row with that key.

This is a common cause of unexpected row multiplication in data analysis and ETL pipelines.

### 9.4 Joining three or more tables

Example: Display employee name, department name and location name.

Tables:

- `employee(emp_id, emp_name, dept_id)`
- `department(dept_id, dept_name, location_id)`
- `location(location_id, location_name)`

```sql
SELECT
    e.emp_name,
    d.dept_name,
    l.location_name
FROM employee e
INNER JOIN department d
    ON e.dept_id = d.dept_id
INNER JOIN location l
    ON d.location_id = l.location_id;
```

Conceptually:

1. Join employee to department.
2. Join the resulting rows to location.
3. Return the selected columns.

HSQLDB evaluates joined-table operations left to right; parentheses can change grouping where needed.

### 9.5 Mixing INNER JOIN and LEFT JOIN

Suppose you want all employees, their department names if available, and their assigned project if available.

```sql
SELECT
    e.emp_name,
    d.dept_name,
    p.project_name
FROM employee e
LEFT JOIN department d
    ON e.dept_id = d.dept_id
LEFT JOIN project p
    ON e.emp_id = p.emp_id;
```

Both LEFT JOINs preserve the employee rows.

**Important:** If you replace the second LEFT JOIN with INNER JOIN, employees without a matching project disappear.

```sql
SELECT
    e.emp_name,
    d.dept_name,
    p.project_name
FROM employee e
LEFT JOIN department d
    ON e.dept_id = d.dept_id
INNER JOIN project p
    ON e.emp_id = p.emp_id;
```

This query requires a matching project. Employees without projects are removed, even though the first join is a LEFT JOIN.

### 9.6 The dangerous outer-join filter

Consider:

```sql
SELECT e.emp_name, d.dept_name
FROM employee e
LEFT JOIN department d
    ON e.dept_id = d.dept_id
WHERE d.dept_name = 'IT';
```

This removes employees with no matching department because `d.dept_name = 'IT'` is UNKNOWN for NULL-extended rows.

If you want all employees but only want IT to be matched:

```sql
SELECT e.emp_name, d.dept_name
FROM employee e
LEFT JOIN department d
    ON e.dept_id = d.dept_id
   AND d.dept_name = 'IT';
```

Employees from other departments remain, but their department columns become NULL in the result.

### 9.7 JOIN using USING

HSQLDB supports `USING` when the two tables have a common join-column name.

```sql
SELECT *
FROM employee
INNER JOIN department
USING (dept_id);
```

This is equivalent in matching behaviour to:

```sql
SELECT *
FROM employee e
INNER JOIN department d
    ON e.dept_id = d.dept_id;
```

The difference is in the result columns: `USING` presents the shared join column once rather than as two separate columns.

For multiple common columns:

```sql
SELECT *
FROM table_a
JOIN table_b
USING (id, dept_id);
```

Both columns must match.

### 9.8 NATURAL JOIN - Use with caution

A NATURAL JOIN automatically joins tables using all identically named columns.

```sql
SELECT *
FROM employee
NATURAL JOIN department;
```

If both tables contain `dept_id`, it joins using that column.

But suppose both tables also contain a column called `location_id`. The NATURAL JOIN may automatically use that column too.

This can change the results unexpectedly when someone adds a new same-named column to either table.

**Professional recommendation:** Prefer explicit `ON` conditions or carefully chosen `USING` columns in production queries. NATURAL JOIN can create fragile dependencies on table schemas.

### 9.9 Non-equi JOIN

A join does not have to use equality.

Example: Match employee salary against salary bands.

**Salary band**

| min_salary | max_salary | band |
| --- | --- | --- |
| 0 | 30000 | Low |
| 30001 | 60000 | Medium |
| 60001 | 100000 | High |

```sql
SELECT
    e.emp_name,
    e.salary,
    s.band
FROM employee e
INNER JOIN salary_band s
    ON e.salary BETWEEN s.min_salary AND s.max_salary;
```

Other non-equi conditions can use `<`, `>`, `<=`, `>=` or combinations of conditions.

Be careful that overlapping ranges can cause one employee to match multiple salary bands.

### 9.10 Self-join for comparing records

Find pairs of employees earning the same salary, without pairing an employee with themselves or returning both `(Arun, Bala)` and `(Bala, Arun)`:

```sql
SELECT
    e1.emp_name AS employee_one,
    e2.emp_name AS employee_two,
    e1.salary
FROM employee e1
INNER JOIN employee e2
    ON e1.salary = e2.salary
   AND e1.emp_id < e2.emp_id;
```

The condition `e1.emp_id < e2.emp_id`:

- Excludes an employee being matched with themselves.
- Returns each pair only once.

### 9.11 EXISTS vs JOIN

Sometimes you only need to check whether a matching row exists, not retrieve columns from the other table.

Using JOIN:

```sql
SELECT DISTINCT d.dept_id, d.dept_name
FROM department d
INNER JOIN employee e
    ON d.dept_id = e.dept_id;
```

Using EXISTS:

```sql
SELECT d.dept_id, d.dept_name
FROM department d
WHERE EXISTS (
    SELECT 1
    FROM employee e
    WHERE e.dept_id = d.dept_id
);
```

EXISTS is a semijoin-style pattern: it returns the left-side row if at least one matching row exists. It does not multiply the left-side row for multiple matches.

For finding departments with no employees:

```sql
SELECT d.dept_id, d.dept_name
FROM department d
WHERE NOT EXISTS (
    SELECT 1
    FROM employee e
    WHERE e.dept_id = d.dept_id
);
```

This is an alternative to LEFT JOIN ... IS NULL.

## 10. JOIN performance and professional best practices

1. Index frequently used join keys, particularly when joining large tables. A primary key or unique constraint normally provides an index for its key.
2. Make sure join columns have compatible data types. Avoid unnecessary conversions in join expressions.
3. Do not join tables using unrelated columns just because their data types match.
4. Check the cardinality of the join keys. Duplicate keys can multiply rows.
5. Avoid `SELECT *` in production queries. Select only the columns needed.
6. Use explicit JOIN syntax instead of comma-separated tables and WHERE conditions.
7. Filter rows appropriately, but preserve outer-join semantics.
8. Use `EXISTS` when checking for existence rather than retrieving matching rows.
9. Use a primary key or another guaranteed non-NULL column for unmatched-row detection.
10. Examine the execution plan when performance is important; do not assume every JOIN is implemented with the same algorithm.

### HSQLDB support summary

HSQLDB 2.7 supports the standard JOIN forms covered here:

| Join syntax | HSQLDB support |
| --- | --- |
| `CROSS JOIN` | Supported |
| `INNER JOIN ... ON` | Supported |
| `LEFT [OUTER] JOIN` | Supported |
| `RIGHT [OUTER] JOIN` | Supported |
| `FULL [OUTER] JOIN` | Supported |
| `JOIN ... USING` | Supported |
| `NATURAL JOIN` | Supported |
| Multi-table joins | Supported |

Reference: Official HyperSQL 2.7 - Data Access and Change.

## 11. Advanced 15-question JOIN quiz

(2-year SQL developer level) (15 questions)

The quiz covers JOIN execution, unmatched records, duplicate multiplication, NULL handling, ON vs WHERE, self-joins, anti-joins and multi-table joins.

## HSQLDB Advanced JOIN Assessment

### 1. Table A contains 4 rows and table B contains 6 rows. What is the result row count of `SELECT * FROM A CROSS JOIN B`?

- A. 10 rows  
Feedback: Adding the row counts does not describe a Cartesian product.
- B. 24 rows  
Feedback: A Cartesian product pairs every A row with every B row: 4 × 6 = 24.
- C. 6 rows  
Feedback: The result is not limited to the number of rows in the larger table.
- D. 4 rows  
Feedback: The result is not limited to the number of rows in the first table.

Correct answers: B

Hint: Think about how many partners each row in the first table receives.

### 2. Table A has two rows with key 10. Table B has three rows with key 10. Both tables are joined using `A.id = B.id`. How many matching rows are produced for key 10?

- A. 2  
Feedback: This ignores the multiple matching rows in B.
- B. 3  
Feedback: This counts B's rows but misses that each matches both A rows.
- C. 5  
Feedback: Adding the counts does not calculate matching combinations.
- D. 6  
Feedback: Each of the two A rows matches all three B rows, producing six combinations.

Correct answers: D

Hint: Count the combinations for each repeated key, not just the number of source rows.

### 3. An employee table has `emp_id`, `emp_name`, and `manager_id`. Which join condition retrieves each employee's manager from the same table?

- A. e.emp_id = m.manager_id  
Feedback: This reverses the relationship and matches a manager ID against another row's manager ID.
- B. e.manager_id = m.emp_id  
Feedback: The employee's manager_id references the manager row's emp_id.
- C. e.manager_id = m.manager_id  
Feedback: This matches employees who report to the same manager, not an employee to their manager.
- D. e.emp_name = m.emp_name  
Feedback: Matching names does not represent the manager relationship.

Correct answers: B

Hint: A manager ID points to the employee ID of another row.

### 4. Department D has IDs 10 and 20. Employee E has department IDs 10 and 30. For `D LEFT JOIN E ON D.id = E.dept_id`, how many rows are returned if each ID occurs once?

- A. 1  
Feedback: The unmatched department 20 is also preserved.
- B. 2  
Feedback: One matching row and one unmatched left-side row are returned.
- C. 3  
Feedback: The unmatched right-side employee with ID 30 is not preserved.
- D. 4  
Feedback: LEFT JOIN does not return every possible pair.

Correct answers: B

Hint: Count matching pairs and unmatched rows from the preserved side.

### 5. For `A LEFT JOIN B ON A.id = B.id WHERE B.id IS NULL`, assuming B.id cannot be NULL in a genuine matching row, what is returned?

- A. Only matching rows  
Feedback: Matching rows have a non-NULL B.id under the stated assumption.
- B. All rows from B  
Feedback: The preserved table is A, not B.
- C. Unmatched rows from A  
Feedback: The NULL-extended B.id identifies A rows without a match.
- D. All rows from A and B  
Feedback: The NULL condition removes matching rows and does not preserve unmatched B rows.

Correct answers: C

Hint: Consider what the right-side columns contain when a left-side row has no match.

### 6. You need every department, but only employees earning more than 50000 should match. Which condition placement preserves departments without qualifying employees?

- A. Put `e.salary > 50000` only in WHERE  
Feedback: WHERE removes NULL-extended rows and departments without qualifying employees.
- B. Put `e.salary > 50000` in ON  
Feedback: The matching condition restricts employee matches while preserving every left-side department.
- C. Replace LEFT JOIN with INNER JOIN  
Feedback: INNER JOIN removes departments without matching qualifying employees.
- D. Put `e.salary > 50000` in ORDER BY  
Feedback: ORDER BY sorts; it does not filter employee matches.

Correct answers: B

Hint: Separate the rule for matching employees from the rule for preserving departments.

### 7. A FULL OUTER JOIN is performed between A and B. Which rows does it preserve?

- A. Only matching rows  
Feedback: That is INNER JOIN behaviour.
- B. All rows from A only  
Feedback: That is LEFT JOIN behaviour.
- C. All rows from B only  
Feedback: That is RIGHT JOIN behaviour.
- D. Matching rows and unmatched rows from both tables  
Feedback: FULL OUTER JOIN preserves matched combinations and unmatched rows from both sides.

Correct answers: D

Hint: Think of the two outer-join preservation directions together.

### 8. Both tables contain a row where the join key is NULL. What happens with `A INNER JOIN B ON A.id = B.id` for those two rows?

- A. They match because both values are NULL  
Feedback: Ordinary equality involving NULL evaluates to UNKNOWN, not TRUE.
- B. They do not match  
Feedback: The equality condition is UNKNOWN, so it does not qualify as a match.
- C. They match only in HSQLDB  
Feedback: HSQLDB follows SQL NULL comparison semantics here.
- D. The query always fails  
Feedback: NULL join keys do not make the query syntactically invalid.

Correct answers: B

Hint: Recall the three-valued logic of SQL comparisons.

### 9. Which query returns each department once if it has at least one employee, without multiplying department rows when several employees match?

- A. A regular INNER JOIN without DISTINCT  
Feedback: A department with multiple employees appears multiple times.
- B. A CROSS JOIN with a WHERE condition  
Feedback: A matching condition can restrict pairs, but matching employees can still multiply departments.
- C. A WHERE EXISTS subquery  
Feedback: EXISTS tests whether at least one matching employee exists without returning one department row per match.
- D. A RIGHT JOIN without a filter  
Feedback: RIGHT JOIN does not guarantee one row per department.

Correct answers: C

Hint: Look for a predicate that tests existence rather than returning joined combinations.

### 10. In HSQLDB, what is the main risk of using NATURAL JOIN between two tables?

- A. It always produces a Cartesian product  
Feedback: NATURAL JOIN uses shared column names as matching columns.
- B. It can silently use additional same-named columns as join keys  
Feedback: Adding a common column name can change the automatic join condition and result.
- C. It can only join primary keys  
Feedback: NATURAL JOIN does not require primary-key columns.
- D. It always removes all NULL values before joining  
Feedback: NATURAL JOIN does not simply discard every NULL-containing row.

Correct answers: B

Hint: Think about what happens when a table schema changes and another common column name appears.

### 11. Which statement about `JOIN ... USING (dept_id)` in HSQLDB is correct?

- A. It joins using every column in both tables  
Feedback: That is the automatic behaviour associated with NATURAL JOIN.
- B. It joins only when dept_id is a primary key  
Feedback: USING does not require a primary key constraint.
- C. It explicitly joins on the named shared column and presents that shared column once  
Feedback: USING names the common join column and avoids presenting two copies of it in the joined result.
- D. It creates a Cartesian product  
Feedback: USING specifies a matching column rather than creating every possible pair.

Correct answers: C

Hint: Compare USING with ON and consider how the common join column appears in the output.

### 12. You need to find employees whose salary is greater than their own manager's salary. Which approach is appropriate?

- A. CROSS JOIN employee with itself without a condition  
Feedback: This creates all employee pairs without identifying manager relationships.
- B. SELF JOIN employee e to employee m on e.manager_id = m.emp_id, then filter e.salary > m.salary  
Feedback: The self-join connects each employee to their manager before comparing salaries.
- C. LEFT JOIN employee to department  
Feedback: That connects employees to departments, not managers.
- D. UNION employee with employee  
Feedback: UNION combines query results; it does not match employee-manager rows.

Correct answers: B

Hint: Both the employee and manager records live in the same table.

### 13. Which statements about HSQLDB JOINs are correct? Select every correct answer.

- A. A LEFT JOIN preserves unmatched rows from its left input  
Feedback: LEFT JOIN adds NULL-extended rows for left-side records without a match.
- B. A JOIN condition must always use equality  
Feedback: Non-equi joins can use inequalities and other valid Boolean conditions.
- C. A FULL OUTER JOIN preserves unmatched rows from both inputs  
Feedback: FULL OUTER JOIN preserves unmatched records on both sides.
- D. JOIN automatically removes duplicate result rows  
Feedback: JOIN returns matching combinations; duplicate removal requires an operation such as DISTINCT when appropriate.

Correct answers: A, C

Hint: Evaluate preservation behaviour and whether SQL join conditions are limited to equality.

### 14. In HSQLDB, `RIGHT JOIN` can be rewritten as a `LEFT JOIN` by swapping the order of the two tables and keeping the equivalent join condition.

- true. True  
Feedback: Swapping the table positions changes which input is preserved, so the equivalent LEFT JOIN can preserve the original right table.
- false. False  
Feedback: This rewrite is valid when the table order and corresponding join condition are adjusted correctly.

Correct answers: true

Hint: Compare which input is preserved before and after reversing the table order.

### 15. For a LEFT JOIN, adding a right-table filter in the WHERE clause can remove unmatched left-side rows.

- true. True  
Feedback: A WHERE comparison such as right_table.status = 'ACTIVE' is UNKNOWN for NULL-extended rows, so those rows are removed.
- false. False  
Feedback: The filter can reject NULL-extended rows, which means unmatched left-side records may disappear.

Correct answers: true

Hint: Consider what happens when the right-side column is NULL after an unmatched LEFT JOIN.

## 12. What you should be able to do in a real SQL developer role

Before moving to the next topic, practise writing these queries without referring to notes:

1. Display employees with their department names.
2. Display all departments, even if they have no employees.
3. Find departments with zero employees.
4. Find employees with no valid department.
5. Display all records from two systems, including unmatched records on both sides.
6. Display employee-manager relationships using SELF JOIN.
7. Find employees earning more than their managers.
8. Find departments with at least three employees using JOIN, GROUP BY and HAVING.
9. Join three tables and calculate department-wise salary totals.
10. Find records existing in one table but missing from another.

**Recommended next topic:** Subqueries, correlated subqueries, EXISTS, NOT EXISTS, IN, NOT IN, ANY, ALL and their differences from JOINs. These build directly on the JOIN concepts you've just studied.

### User

for 2 year sql developer hsql database level give concepts needed from required topics all tricky advanced topics from these explanation and 15 question quiz at end all edge cases indexing intro to indexing example why indexing working of index index tree search algo index for enforcing data integrity,index automatically created for constraint enforcement when u create primary and unique key,index types characterstics clustered index non clustered index clustered auto generated non clustered created manually max 249 per table max 1 clustered index per table clustererd sort table data non clustered do not sort table data, index of primarky key automatically created, consumes additional space, maintained automatically by databe once created we dont have to maintain,size oof index propertional to size of data, can be created on multiple attributes as well composite index , degratation of insert performance with addition of index numer of rows per unit time reduces as index increases, tabe scan examples give when large portion of rows in table must be accessed, index does not exist on column searched index exists cannot be used, index unique scan example give example working, index range scan  explain these 3 properly retieve one row index unique scan multiple row index range scan index, incorrect usage of index : no searching critera, no matching indexed using function on indexed column negative criteria no match on first column and express explain these crisply with single examples proeprly , index correct usage: search by primary key search on non unique column range search partial match like at end like at start multiple index match full match independent of order in where startement index advantages distdvantages index improve performance of select reduce performance of where , enforce integrity constraints how index can be located query for that

### ChatGPT

# HSQLDB: Indexing - Complete Advanced Guide for a 2-Year SQL Developer

Indexing is one of the most important concepts in SQL performance tuning. A developer must understand not only how to create an index, but also **when the database uses it, when it ignores it, how it affects INSERT/UPDATE/DELETE, and how to identify indexes during troubleshooting.**

We'll use HSQLDB syntax and examples throughout.

## 1. What is an index?

An index is a separate data structure maintained by the database to locate rows more efficiently.

Think of an index like the index at the back of a textbook:

- Without an index, you may have to scan every page to find a topic.
- With an index, you can locate the topic using its alphabetical entry and page number.

Similarly:

- Without a database index, the database may scan every row in a table.
- With an appropriate index, it can navigate the index to find matching row locations.

### Example: Searching without an index

Suppose an employee table contains 1,000,000 records.

```sql
SELECT *
FROM employee
WHERE emp_id = 50000;
```

If no usable index exists on `emp_id`, the database may perform a table scan:

1. Read the first row.
2. Check whether `emp_id = 50000`.
3. Read the next row.
4. Continue until the matching row is found or the table is exhausted.

In the worst case, it checks all one million rows.

### Example: Searching with an index

Suppose an index exists on `emp_id`.

```sql
CREATE INDEX idx_employee_emp_id
ON employee(emp_id);
```

Now the database can navigate the index to find the key `50000`, then locate the corresponding employee row.

It does not necessarily have to examine every row in the table.

**Conceptual comparison**

**Table scan**

Check rows one after another

Many rows may need to be examined.

**Index lookup**

Index root

Index branch

Index branch

Matching key / row location

Navigate through index levels to locate a matching key.

**Important:** An index does not guarantee that every query will be faster. The optimizer decides whether using an index is cheaper than scanning the table.

## 2. How does an index work internally?

A common index structure is a **B-tree** $or a B+ tree, depending on the implementation).

It keeps index keys in an ordered structure, with references to child nodes or row locations.

For example, an index on employee ID might conceptually contain\:

```text
                  [40 | 70]
                 /    |    \
          [10,20,30] [50,60] [80,90]
```

To search for employee ID 60\:

1. Start at the root.
2. Compare 60 with 40 and 70.
3. Follow the middle branch.
4. Find 60 in that branch.
5. Follow its row reference to retrieve the record.

The search does not need to inspect every key.

For a balanced tree, searching is approximately logarithmic in the number of indexed entries\:

\[
O(\log N)
\]

A table scan is approximately\:

\[
O(N)
\]

where \(N$ is the number of rows.

**Important distinction:** These are conceptual complexity comparisons, not guaranteed query execution times. Disk I/O, caching, row width, selectivity, index structure and the execution plan all matter.

### What does an index store?

Conceptually, an index stores:

- Indexed column values.
- References to the corresponding table rows.
- Additional structural information needed to navigate the index.

A composite index stores keys formed from multiple columns.

The index is maintained by the database when table data changes. You do not manually insert or remove index entries.

## 3. Why does the database automatically create indexes?

Indexes are also used to enforce data integrity constraints efficiently.

### 3.1 Primary key constraint

```sql
CREATE TABLE employee (
    emp_id INTEGER PRIMARY KEY,
    emp_name VARCHAR(100),
    salary DECIMAL(10,2)
);
```

A primary key enforces:

1. Uniqueness.
2. NOT NULL.

The database needs an efficient way to check whether an inserted primary key already exists.

An index is used for this uniqueness enforcement.

In HSQLDB, a primary key constraint creates an associated unique index automatically.

You should not create another ordinary index on the exact same primary-key column just for uniqueness enforcement.

### 3.2 UNIQUE constraint

```sql
CREATE TABLE employee (
    emp_id INTEGER PRIMARY KEY,
    email VARCHAR(150) UNIQUE
);
```

The UNIQUE constraint prevents duplicate non-NULL email values.

HSQLDB creates an associated unique index for a UNIQUE constraint as well.

### 3.3 FOREIGN KEY constraint

```sql
CREATE TABLE department (
    dept_id INTEGER PRIMARY KEY,
    dept_name VARCHAR(100)
);

CREATE TABLE employee (
    emp_id INTEGER PRIMARY KEY,
    emp_name VARCHAR(100),
    dept_id INTEGER,
    CONSTRAINT fk_employee_department
        FOREIGN KEY (dept_id)
        REFERENCES department(dept_id)
);
```

A foreign key enforces referential integrity.

For example, inserting an employee with `dept_id = 999` is rejected if department 999 does not exist.

**Important HSQLDB distinction:** Do not assume a foreign-key constraint automatically creates an index on the child-table foreign-key column. The referenced parent key is indexed through its primary-key or unique constraint, but you should consider creating an index on the child column when joins, parent deletes or updates need efficient child-row lookups.

```sql
CREATE INDEX idx_employee_dept
ON employee(dept_id);
```

This is particularly useful for:

```sql
SELECT *
FROM employee
WHERE dept_id = 10;
```

and:

```sql
SELECT d.dept_name, e.emp_name
FROM department d
JOIN employee e
    ON d.dept_id = e.dept_id;
```

**Correction to the earlier foreign-key explanation:** HSQLDB does automatically create a non-unique index for each FOREIGN KEY constraint. This differs from some other database engines. The HSQLDB documentation explicitly confirms that it creates indexes for PRIMARY KEY, UNIQUE and FOREIGN KEY constraints.

## 4. Types of indexes

There are several ways to classify indexes. Do not confuse general database terminology with features supported by a particular database engine.

### 4.1 Unique index

A unique index ensures that indexed key combinations cannot be duplicated.

Example:

```sql
CREATE TABLE employee (
    emp_id INTEGER PRIMARY KEY,
    email VARCHAR(100) UNIQUE
);
```

HSQLDB automatically creates unique indexes to support these constraints.

For example, the following two rows cannot both be inserted:

```sql
INSERT INTO employee VALUES (1, 'arun@gmail.com');
INSERT INTO employee VALUES (2, 'arun@gmail.com');
```

The second insert violates the UNIQUE constraint.

### 4.2 Non-unique index

A non-unique index permits duplicate indexed values.

```sql
CREATE INDEX idx_employee_dept
ON employee(dept_id);
```

Multiple employees can belong to department 10.

| emp_id | emp_name | dept_id |
| --- | --- | --- |
| 1 | Arun | 10 |
| 2 | Bala | 10 |
| 3 | Charan | 10 |
| 4 | Divya | 20 |

The index helps locate all employees belonging to department 10.

### 4.3 Single-column index

An index created on one column.

```sql
CREATE INDEX idx_employee_salary
ON employee(salary);
```

Useful for:

```sql
SELECT *
FROM employee
WHERE salary = 50000;
```

### 4.4 Composite index / Multiple-column index

An index created on multiple columns.

```sql
CREATE INDEX idx_employee_dept_salary
ON employee(dept_id, salary);
```

The index key is based on the combination:

```text
(dept_id, salary)
```

Useful queries:

```sql
SELECT *
FROM employee
WHERE dept_id = 10;
```

```sql
SELECT *
FROM employee
WHERE dept_id = 10
  AND salary = 50000;
```

```sql
SELECT *
FROM employee
WHERE dept_id = 10
  AND salary > 40000;
```

The order of columns in the index is important. We will examine this in detail in Section 8.

### 4.5 Clustered vs non-clustered indexes

These are common database concepts, particularly in SQL Server discussions.

**Clustered index - general database concept**

- The table's row storage is organized around the clustered key.
- The table data is stored in clustered-key order in systems that implement this model.
- A table can generally have only one clustered organization.
- Range access can be efficient.  
**Non-clustered index - general database concept**
- A separate index structure stores keys and row locators.
- The base table does not have to be stored in the index-key order.
- Multiple non-clustered indexes can exist on a table.
- Additional lookups may be needed to retrieve columns not present in the index.

(HSQLDB-specific distinction)

Do not apply SQL Server's clustered/non-clustered index rules directly to HSQLDB.

- HSQLDB does not expose the usual `CREATE CLUSTERED INDEX` / `CREATE NONCLUSTERED INDEX` syntax.
- Its documented `CREATE INDEX` syntax creates an index on one or more columns.
- Do not assume that creating a normal HSQLDB index physically sorts or reorganizes the table's rows.
- HSQLDB does not document a general limit of 249 indexes per table. That number should not be treated as an HSQLDB rule.
- Do not confuse the maximum number of indexes in another database with an HSQLDB restriction.

Also, HSQLDB accepts `ASC` and `DESC` in its index definition for compatibility, but documents that these options have no effect on how the index is created. Its ordinary indexes can be used for ascending or descending ordering.

## 5. Creating and dropping indexes in HSQLDB

### 5.1 CREATE INDEX

Syntax:

```sql
CREATE INDEX index_name
ON table_name (column_name);
```

Example:

```sql
CREATE INDEX idx_employee_salary
ON employee(salary);
```

### 5.2 Composite index

```sql
CREATE INDEX idx_employee_dept_salary
ON employee(dept_id, salary);
```

### 5.3 Index with multiple columns and explicit directions

```sql
CREATE INDEX idx_employee_dept_salary
ON employee(dept_id ASC, salary DESC);
```

HSQLDB accepts this syntax, but the ASC/DESC specifications do not change the actual index structure.

### 5.4 DROP INDEX

```sql
DROP INDEX idx_employee_salary;
```

Dropping an index removes that index structure, not the table data.

**Do not drop a constraint-generated index as if it were an ordinary user-created index.** To remove the index associated with a PRIMARY KEY, UNIQUE or FOREIGN KEY constraint, you normally change or drop the constraint itself.

### 5.5 Do we manually maintain indexes?

No. Once created, the database maintains index entries automatically.

For example:

```sql
INSERT INTO employee
VALUES (10, 'Kumar', 50000, 20);
```

The database adds the corresponding entry to applicable indexes.

When an indexed value changes:

```sql
UPDATE employee
SET salary = 60000
WHERE emp_id = 10;
```

The database updates the relevant index entries.

When a row is deleted, the corresponding entries are also removed.

You do not manually update index entries.

## 6. Advantages and disadvantages of indexing

### Advantages

1. Improves SELECT performance for suitable search conditions.
2. Speeds up primary-key and unique-key lookups.
3. Helps range queries such as BETWEEN, greater than and less than.
4. Helps JOIN operations on indexed columns.
5. Can help ORDER BY and GROUP BY queries.
6. Helps locate rows for UPDATE and DELETE.
7. Supports enforcement of uniqueness and referential integrity constraints.

### Disadvantages

1. **Extra storage:** Indexes consume additional disk or memory space.
2. **INSERT overhead:** Each insert may require new entries in several indexes.
3. **UPDATE overhead:** Changing an indexed column requires index maintenance.
4. **DELETE overhead:** Corresponding index entries must be removed.
5. **Maintenance overhead:** More indexes mean more work for the database.
6. **Poor index selection:** Unnecessary indexes can waste resources without improving queries.

Index size generally grows with the number of indexed rows and the width of the indexed keys, along with structural overhead. It is not an exact fixed proportion of table size.

### What happens to INSERT performance as indexes increase?

Suppose you insert 100,000 employee records.

- With no secondary indexes, the database has fewer index structures to maintain.
- With five secondary indexes, each insert may require maintaining those five indexes as well.
- With ten secondary indexes, the write operation may involve still more work.

**Conceptual write-cost comparison**

| Number of additional indexes | Index maintenance per insert |
| --- | --- |
| 0 | Minimal secondary-index work |
| 2 | More index entries to maintain |
| 5 | Higher maintenance work |
| 10 | Potentially substantial overhead |

Illustrative comparison, not measured HSQLDB benchmark results.

This means the number of rows inserted per second can decrease as the number of indexes increases.

However, the actual impact depends on index structure, data distribution, storage type, caching and workload.

**Professional rule:** Create indexes to support real query patterns, not simply because a table has many columns.

## 7. Three important data-access methods

You specifically need to understand:

1. Table scan.
2. Index unique scan.
3. Index range scan.

These are useful concepts for reading execution plans. The exact operation names vary between database engines; do not assume HSQLDB will print Oracle's exact labels.

### 7.1 Table scan

A table scan examines rows in the table to evaluate the query condition.

Example:

```sql
SELECT *
FROM employee
WHERE employee_name = 'Arun';
```

Suppose there is no index on `employee_name`.

The database may examine the table rows one by one to find Arun.

**When is a table scan used?**

- No usable index exists.
- The query returns a large portion of the table.
- The search condition is not suitable for an available index.
- The optimizer estimates that scanning the table is cheaper than using the index and retrieving many rows.

Example:

```sql
SELECT *
FROM employee;
```

Since all rows are requested, a table scan is often appropriate.

**Important:** A table scan is not necessarily bad. If you need 90% of a table, scanning the table may be more efficient than looking up 90% of its rows individually through an index.

### 7.2 Index unique scan

An index unique scan means using a unique index to locate a single row through a complete equality lookup of its unique key.

Example:

```sql
CREATE TABLE employee (
    emp_id INTEGER PRIMARY KEY,
    emp_name VARCHAR(100),
    salary DECIMAL(10,2)
);
```

Query:

```sql
SELECT *
FROM employee
WHERE emp_id = 101;
```

Since `emp_id` is a primary key, at most one row can match.

Conceptual execution:

1. Navigate the unique index.
2. Find key 101.
3. Retrieve the corresponding table row.
4. Stop because the unique key guarantees no second matching row.

(Single-row lookup)

Another example using a composite unique key:

```sql
CREATE TABLE employee_contact (
    emp_id INTEGER,
    contact_type VARCHAR(20),
    contact_value VARCHAR(100),
    CONSTRAINT uq_emp_contact
        UNIQUE (emp_id, contact_type)
);
```

This query specifies the complete unique key:

```sql
SELECT *
FROM employee_contact
WHERE emp_id = 101
  AND contact_type = 'OFFICE';
```

At most one row can match.

But if you search only:

```sql
SELECT *
FROM employee_contact
WHERE emp_id = 101;
```

Multiple rows may match because one employee can have different contact types. This is not a complete unique-key lookup.

### 7.3 Index range scan

An index range scan accesses a range of index entries. It can return one row or many rows.

Example:

```sql
CREATE INDEX idx_employee_salary
ON employee(salary);
```

Query:

```sql
SELECT *
FROM employee
WHERE salary BETWEEN 40000 AND 70000;
```

The database can navigate to the starting salary and examine relevant index entries up to the end of the range.

Other examples:

```sql
SELECT *
FROM employee
WHERE salary > 50000;
```

```sql
SELECT *
FROM employee
WHERE salary < 30000;
```

```sql
SELECT *
FROM employee
WHERE salary = 50000;
```

The equality condition on a non-unique index may return multiple rows, so it can use range-style index access.

### Difference between the three

| Access method | What it does | Typical example |
| --- | --- | --- |
| Table scan | Examines table rows | No suitable index or broad retrieval |
| Unique index lookup | Finds at most one matching row | Equality on complete primary key |
| Index range access | Examines matching index entries in a range | Non-unique equality or salary BETWEEN |

**Very important:** The words *index unique scan* and *index range scan* are often taught using Oracle execution-plan terminology. HSQLDB's own `EXPLAIN PLAN` reports its chosen indexes and plan details; learn to read the HSQLDB output rather than expecting identical operation labels.

## 8. Composite indexes - The most important advanced concept

A composite index is created using more than one column.

Example:

```sql
CREATE INDEX idx_employee_dept_salary
ON employee(dept_id, salary);
```

This index has a specific column order:

1. `dept_id` - first column.
2. `salary` - second column.

Think of it as an ordered key:

```text
(dept_id, salary)

(10, 30000)
(10, 40000)
(10, 50000)
(20, 35000)
(20, 45000)
(30, 60000)
```

### 8.1 Leftmost-prefix rule

An index on:

```sql
(dept_id, salary, join_date)
```

can efficiently support conditions using:

- `dept_id`
- `dept_id, salary`
- `dept_id, salary, join_date`

It generally cannot efficiently support a search using only `salary` or only `join_date` through that index.

Example:

**Index:** `(dept_id, salary, join_date)`

| Search condition | Index use |
| --- | --- |
| `dept_id = 10` | (Yes) |
| `dept_id = 10 AND salary = 50000` | (Yes) |
| `dept_id = 10 AND salary = 50000 AND join_date = ...` | (Yes) |
| `salary = 50000` | (No leading column) |
| `join_date = ...` | (No leading column) |

This is the leftmost-prefix principle.

HSQLDB specifically documents that a multicolumn index can be used for the first column or the first consecutive columns, but not for a search using only the second or third column.

### 8.2 Does the order of WHERE conditions matter?

Suppose your index is:

```sql
CREATE INDEX idx_employee_dept_salary
ON employee(dept_id, salary);
```

Both queries can use the same composite index:

```sql
SELECT *
FROM employee
WHERE dept_id = 10
  AND salary = 50000;
```

```sql
SELECT *
FROM employee
WHERE salary = 50000
  AND dept_id = 10;
```

(Same logical condition)

The textual order of conditions in WHERE does not determine the order of index columns.

The index definition determines the index-key order.

### 8.3 Full match vs partial match

**Full match:** All index columns are specified.

```sql
CREATE INDEX idx_emp
ON employee(dept_id, salary, join_date);
```

```sql
SELECT *
FROM employee
WHERE dept_id = 10
  AND salary = 50000
  AND join_date = DATE '2025-01-01';
```

All three indexed columns participate.

**Partial leading match:** Only the first one or two columns are specified.

```sql
SELECT *
FROM employee
WHERE dept_id = 10
  AND salary = 50000;
```

This can still use the composite index.

**Partial non-leading match:** Only the second column is specified.

```sql
SELECT *
FROM employee
WHERE salary = 50000;
```

The index is not a suitable leading-key lookup for this condition.

### 8.4 Composite index with a range condition

Consider:

```sql
CREATE INDEX idx_emp_dept_salary
ON employee(dept_id, salary);
```

Query:

```sql
SELECT *
FROM employee
WHERE dept_id = 10
  AND salary > 40000;
```

This is a good composite-index pattern:

- First, identify the department.
- Within that department, find salaries above 40000.

But consider:

```sql
SELECT *
FROM employee
WHERE dept_id > 10
  AND salary = 40000;
```

The first column is a range condition. The second column may be less useful for narrowing the lookup because the first key already spans multiple department values.

**Practical design tip:** Put commonly used equality-search columns before range-search columns when designing a composite index, after considering actual query patterns and selectivity.

### 8.5 Should we create separate indexes for every column?

Not necessarily.

If you have:

```sql
CREATE INDEX idx_emp_dept_salary
ON employee(dept_id, salary);
```

You generally do not need another index on `dept_id` just for queries that search by `dept_id`, because the composite index can support its leading column.

But if you frequently search only by salary:

```sql
SELECT *
FROM employee
WHERE salary = 50000;
```

An additional index may be useful:

```sql
CREATE INDEX idx_emp_salary
ON employee(salary);
```

HSQLDB explicitly recommends avoiding duplicate indexes where constraint-generated or existing indexes already cover the required column sets.

## 9. Incorrect and inefficient usage of indexes

These are common interview questions and real-world query-tuning problems.

### 9.1 No search condition

```sql
SELECT *
FROM employee;
```

You are requesting every row.

An index on `emp_id` does not help the database avoid retrieving the entire table.

A table scan may be the most efficient choice.

### 9.2 Searching a column without a suitable index

```sql
SELECT *
FROM employee
WHERE employee_name = 'Arun';
```

If there is no suitable index on `employee_name`, the database may scan the table.

Creating an index may help:

```sql
CREATE INDEX idx_employee_name
ON employee(employee_name);
```

Whether it is actually used depends on selectivity and the optimizer's cost estimate.

### 9.3 Applying a function to an indexed column

Suppose you have:

```sql
CREATE INDEX idx_employee_name
ON employee(employee_name);
```

This query may not be able to use the ordinary index efficiently:

```sql
SELECT *
FROM employee
WHERE UPPER(employee_name) = 'ARUN';
```

Why?

The condition applies a function to every candidate column value. The search expression is not a direct lookup on the indexed value.

A normal index on `employee_name` is not automatically an index on `UPPER(employee_name)`.

A better approach is to store or search normalized data consistently, or use an appropriate indexed normalized column if the application requires case-insensitive matching.

### 9.4 Applying calculations to an indexed numeric column

Suppose:

```sql
CREATE INDEX idx_employee_salary
ON employee(salary);
```

Potentially inefficient:

```sql
SELECT *
FROM employee
WHERE salary + 1000 > 50000;
```

Rewrite the condition algebraically:

```sql
SELECT *
FROM employee
WHERE salary > 49000;
```

Now the indexed column is directly compared to a constant.

### 9.5 Applying a function to a DATE column

Suppose you have an index on `join_date`.

Potentially inefficient:

```sql
SELECT *
FROM employee
WHERE YEAR(join_date) = 2025;
```

Prefer a date range:

```sql
SELECT *
FROM employee
WHERE join_date >= DATE '2025-01-01'
  AND join_date < DATE '2026-01-01';
```

This expresses the search directly against the indexed date column.

For TIMESTAMP columns, use timestamp boundaries of the appropriate type.

### 9.6 Leading wildcard in LIKE

Suppose:

```sql
CREATE INDEX idx_employee_name
ON employee(employee_name);
```

Potentially inefficient:

```sql
SELECT *
FROM employee
WHERE employee_name LIKE '%ar';
```

The search begins with a wildcard, so the beginning of the indexed string is not known.

Better index-friendly pattern:

```sql
SELECT *
FROM employee
WHERE employee_name LIKE 'Ar%';
```

The database can search for names beginning with `Ar`.

HSQLDB documents index use for LIKE conditions that search from the beginning of the string.

### 9.7 Negative conditions

Examples:

```sql
SELECT *
FROM employee
WHERE dept_id <> 10;
```

```sql
SELECT *
FROM employee
WHERE NOT (salary = 50000);
```

```sql
SELECT *
FROM employee
WHERE employee_name NOT LIKE 'A%';
```

These conditions can match a large percentage of the table. The optimizer may decide a table scan is cheaper.

**Important correction:** Negative conditions do not categorically prevent index use. HSQLDB documents index optimisation for `IS NOT NULL`, and the optimizer can use indexes for suitable conditions. The actual choice depends on the predicate, selectivity and execution plan.

### 9.8 Composite index without the first column

Index:

```sql
CREATE INDEX idx_emp_dept_salary
ON employee(dept_id, salary);
```

Inefficient for this index:

```sql
SELECT *
FROM employee
WHERE salary = 50000;
```

The first indexed column, `dept_id`, is missing.

If salary-only searches are common, consider a separate salary index.

### 9.9 Data type mismatch or implicit conversion

Suppose `emp_id` is INTEGER and has an index.

Prefer:

```sql
SELECT *
FROM employee
WHERE emp_id = 100;
```

Avoid unnecessary transformations or casts:

```sql
SELECT *
FROM employee
WHERE CAST(emp_id AS VARCHAR(20)) = '100';
```

The second expression may prevent an ordinary index lookup on the original integer key.

Use constants of compatible data types wherever possible.

## 10. Correct usage of indexes - Practical patterns

| Search requirement | Example | Index suitability |
| --- | --- | --- |
| Primary-key equality | `emp_id = 10` | Excellent |
| Unique-column equality | `email = 'a@x.com'` | Excellent |
| Non-unique-column equality | `dept_id = 10` | Good if selective enough |
| Range search | `salary BETWEEN 30000 AND 50000` | Good |
| Greater/less than | `salary > 50000` | Good |
| Prefix LIKE | `name LIKE 'Ar%'` | Can use index |
| Suffix LIKE | `name LIKE '%ar'` | Usually not suitable |
| Composite leading columns | `dept_id = 10 AND salary = 50000` | Good |
| Non-leading composite column only | `salary = 50000` | Not supported efficiently by that composite index |
| NULL test | `dept_id IS NULL` | HSQLDB can use indexes |
| IN predicate | `dept_id IN (10,20,30)` | HSQLDB can use indexes |

HSQLDB also documents that:

- It can use an index for suitable AND conditions.
- It can use multiple indexes when suitable OR conditions refer to indexed columns.
- It can use indexes for certain DISTINCT and GROUP BY queries.
- It can use indexes for ORDER BY, particularly with LIMIT/FETCH.

### Example: Multiple indexed columns in WHERE

Suppose:

```sql
CREATE INDEX idx_emp_dept
ON employee(dept_id);

CREATE INDEX idx_emp_salary
ON employee(salary);
```

Query:

```sql
SELECT *
FROM employee
WHERE dept_id = 10
  AND salary > 50000;
```

HSQLDB can choose the most useful indexed condition. Do not assume it must use both indexes or that it must use the index mentioned first in WHERE.

For OR:

```sql
SELECT *
FROM employee
WHERE dept_id = 10
   OR salary > 50000;
```

HSQLDB can use multiple suitable indexes for OR conditions when each branch can use an index.

## 11. How to check whether an index is being used in HSQLDB

This is the most important practical skill for a SQL developer.

### 11.1 EXPLAIN PLAN FOR

HSQLDB supports:

```sql
EXPLAIN PLAN FOR
SELECT *
FROM employee
WHERE emp_id = 101;
```

It reports the execution plan, including index information.

Test a query without an index:

```sql
EXPLAIN PLAN FOR
SELECT *
FROM employee
WHERE employee_name = 'Arun';
```

Then create the index:

```sql
CREATE INDEX idx_employee_name
ON employee(employee_name);
```

Run the same EXPLAIN statement again:

```sql
EXPLAIN PLAN FOR
SELECT *
FROM employee
WHERE employee_name = 'Arun';
```

Compare the plans to see whether the new index is selected.

**Remember:** Creating an index does not force the optimizer to use it. A table scan may still be cheaper.

### 11.2 Find index metadata using SYSTEM_INDEXINFO

HSQLDB provides the `INFORMATION_SCHEMA.SYSTEM_INDEXINFO` view for JDBC index metadata.

```sql
SELECT *
FROM INFORMATION_SCHEMA.SYSTEM_INDEXINFO;
```

To inspect a specific table:

```sql
SELECT *
FROM INFORMATION_SCHEMA.SYSTEM_INDEXINFO
WHERE TABLE_NAME = 'EMPLOYEE';
```

This is useful for identifying:

- Index names.
- Indexed columns.
- Whether the index is unique.
- Column order within an index.
- Other index metadata.

### 11.3 Find indexes created for constraints

HSQLDB provides:

```sql
SELECT *
FROM INFORMATION_SCHEMA.SYSTEM_KEY_INDEX_USAGE;
```

This view lists system-generated index names associated with PRIMARY KEY, UNIQUE and FOREIGN KEY constraints.

To see its available columns:

```sql
SELECT *
FROM INFORMATION_SCHEMA.SYSTEM_KEY_INDEX_USAGE
WHERE TABLE_NAME = 'EMPLOYEE';
```

You can also inspect the constraints themselves:

```sql
SELECT *
FROM INFORMATION_SCHEMA.TABLE_CONSTRAINTS
WHERE TABLE_NAME = 'EMPLOYEE';
```

The official documentation describes these metadata views and their purposes.

## 12. Final revision - Important interview points

| Concept | Remember |
| --- | --- |
| Primary key | HSQLDB automatically creates a unique index |
| UNIQUE constraint | HSQLDB automatically creates a unique index |
| FOREIGN KEY | HSQLDB automatically creates a non-unique index |
| Composite index | Column order matters |
| Leftmost prefix | First index column must be part of the search for efficient composite-index use |
| Index maintenance | Automatic during INSERT, UPDATE and DELETE |
| Index storage | Requires additional space |
| More indexes | Can increase write overhead |
| Table scan | Can be more efficient for broad result sets |
| Unique lookup | Equality lookup on a complete unique key |
| Range lookup | Can return one or multiple rows |
| LIKE 'Ar%' | Can use an appropriate index |
| LIKE '%ar' | Usually cannot use the ordinary index efficiently |
| Function on indexed column | Can prevent ordinary index use |
| EXPLAIN PLAN | Shows which indexes HSQLDB uses |
| SYSTEM_INDEXINFO | Shows index metadata |
| SYSTEM_KEY_INDEX_USAGE | Shows constraint-generated index names |

**One important HSQLDB feature:** Since version 2.6, you can extend the index associated with a FOREIGN KEY constraint to include extra columns, without changing the foreign-key relationship itself.

Example:

```sql
ALTER TABLE invoice
ALTER CONSTRAINT fk_invoice_customer
INDEX ADD (invoice_date);
```

This can help queries that search using both `customer_id` and `invoice_date`. The foreign-key constraint must have a user-defined name.

---

## 13. Advanced 15-question indexing quiz

(2-year SQL developer level) (15 questions)

## HSQLDB Advanced Indexing Assessment

### 1. In HSQLDB, which indexes are automatically created to support PRIMARY KEY, UNIQUE and FOREIGN KEY constraints, respectively?

- A. Non-unique, unique, no index  
Feedback: This does not match HSQLDB's documented constraint-index behaviour.
- B. Unique, unique, non-unique  
Feedback: HSQLDB creates a unique index for each primary-key and unique constraint, and a non-unique index for each foreign-key constraint.
- C. Unique, non-unique, unique  
Feedback: The unique and foreign-key index types are reversed here.
- D. No indexes for any constraint  
Feedback: HSQLDB creates system indexes to support these constraints.

Correct answers: B

Hint: Distinguish constraints that require uniqueness from a foreign key that permits repeated child values.

### 2. A table has an index on `(dept_id, salary, join_date)`. Which search condition has the most complete leading-key match?

- A. `salary = 50000`  
Feedback: This skips the first indexed column.
- B. `join_date = DATE '2025-01-01'`  
Feedback: This uses only the third indexed column.
- C. `dept_id = 10 AND salary = 50000`  
Feedback: This specifies the first two consecutive index columns, making it a valid leading-prefix lookup.
- D. `salary = 50000 AND join_date = DATE '2025-01-01'`  
Feedback: Both conditions omit the first indexed column.

Correct answers: C

Hint: The position of a column in a composite index matters more than the order of predicates in SQL.

### 3. An index is defined on `(dept_id, salary)`. Which statement about `WHERE salary = 50000 AND dept_id = 10` is correct?

- A. It cannot use the index because salary appears first in WHERE  
Feedback: The textual order of AND conditions does not determine the composite index's column order.
- B. It can use the composite index because both leading columns are constrained  
Feedback: Both indexed columns are specified; their textual order in WHERE does not change the index definition.
- C. It must use a table scan  
Feedback: The query supplies both leading index columns.
- D. It can use the index only if salary is the first indexed column  
Feedback: The WHERE predicate order does not need to match the index-key order.

Correct answers: B

Hint: Separate the index's defined key order from the written order of Boolean predicates.

### 4. A unique index exists on employee.emp_id. What is the expected logical lookup behaviour for `WHERE emp_id = 101`?

- A. A unique-key lookup returning at most one row  
Feedback: A unique key guarantees no more than one matching row.
- B. A range lookup that must return many rows  
Feedback: Uniqueness prevents multiple rows from sharing that key.
- C. A Cartesian product  
Feedback: No join or Cartesian product is involved.
- D. A full scan is mandatory  
Feedback: A suitable unique index can locate the key directly.

Correct answers: A

Hint: Use the uniqueness guarantee to reason about the maximum number of matching rows.

### 5. A non-unique index exists on salary. The query is `SELECT * FROM employee WHERE salary = 50000`. Which access pattern is appropriate?

- A. Unique index lookup guaranteed to return one row  
Feedback: A non-unique index allows several employees to have the same salary.
- B. Range-style index access that can return multiple matching rows  
Feedback: Duplicate salary values can occupy multiple index entries.
- C. A primary-key constraint lookup  
Feedback: Salary is not stated to be a primary key.
- D. A Cartesian product  
Feedback: The query reads one table and does not combine all row pairs.

Correct answers: B

Hint: A non-unique key can identify more than one row even when the comparison uses equality.

### 6. A query requests every row and every column from a large table. Why might the optimizer choose a table scan even if an index exists?

- A. Indexes are prohibited for SELECT *  
Feedback: SELECT * does not universally prohibit index use.
- B. The optimizer may estimate that reading most rows through an index and fetching table data costs more  
Feedback: A broad retrieval can make sequential table access cheaper than many index-driven row lookups.
- C. Indexes work only for primary keys  
Feedback: Indexes can support many search and ordering conditions.
- D. The table scan is always faster  
Feedback: The choice depends on the workload and estimated cost.

Correct answers: B

Hint: Consider how many table rows must ultimately be retrieved.

### 7. An ordinary index exists on employee_name. Which LIKE predicate is most suitable for using that index?

- A. `employee_name LIKE '%ar'`  
Feedback: The leading wildcard hides the beginning of the search value.
- B. `employee_name LIKE '%ar%'`  
Feedback: The pattern can begin anywhere, so an ordinary ordered index cannot directly seek its starting prefix.
- C. `employee_name LIKE 'Ar%'`  
Feedback: The fixed prefix allows the database to search from the beginning of the indexed string.
- D. `employee_name NOT LIKE 'Ar%'`  
Feedback: This negative predicate is generally less suitable for a selective prefix lookup.

Correct answers: C

Hint: An ordered string index is most helpful when the beginning of the value is known.

### 8. An ordinary index exists on join_date. Which rewrite is generally more index-friendly than `YEAR(join_date) = 2025`?

- A. `CAST(join_date AS VARCHAR(10)) LIKE '2025%'`  
Feedback: This applies a conversion to the indexed column rather than searching its original date value.
- B. `join_date >= DATE '2025-01-01' AND join_date < DATE '2026-01-01'`  
Feedback: The range compares the indexed date column directly against compatible boundary values.
- C. `MONTH(join_date) = 1`  
Feedback: This extracts a function from the indexed column and does not identify the entire year.
- D. `UPPER(CAST(join_date AS VARCHAR(10))) = '2025'`  
Feedback: The conversion and function do not provide a direct date-range lookup.

Correct answers: B

Hint: Convert the date-part requirement into lower and upper bounds on the original column.

### 9. What is the HSQLDB statement used to inspect the execution plan and see which indexes a query uses?

- A. `SHOW INDEX PLAN`  
Feedback: This is not the documented HSQLDB statement.
- B. `EXPLAIN PLAN FOR SELECT ...`  
Feedback: HSQLDB documents EXPLAIN PLAN FOR as the way to inspect query plans and index usage.
- C. `DESCRIBE PLAN SELECT ...`  
Feedback: This is not the documented HSQLDB syntax.
- D. `ANALYZE INDEX SELECT ...`  
Feedback: This is not the HSQLDB query-plan statement.

Correct answers: B

Hint: Recall the SQL command used to explain how the optimizer processes a statement.

### 10. Which HSQLDB INFORMATION_SCHEMA view provides JDBC index metadata?

- A. `SYSTEM_INDEXINFO`  
Feedback: This HSQLDB system view provides information used by JDBC DatabaseMetaData.getIndexInfo.
- B. `SYSTEM_PRIMARYKEYS`  
Feedback: This view is for primary-key metadata, not general index metadata.
- C. `SYSTEM_TABLESTATS`  
Feedback: This view provides table statistics, not index metadata.
- D. `SYSTEM_COLUMNS`  
Feedback: This view provides column metadata.

Correct answers: A

Hint: Look for the system view whose name explicitly refers to index information.

### 11. What is a likely consequence of adding many unnecessary secondary indexes to a table with frequent INSERT operations?

- A. Every insert becomes a read-only operation  
Feedback: Indexes do not make the table read-only.
- B. The database has more index entries to maintain, increasing write overhead  
Feedback: Each relevant insert may require changes to multiple index structures.
- C. The primary key stops enforcing uniqueness  
Feedback: Additional indexes do not disable primary-key enforcement.
- D. All SELECT queries must become table scans  
Feedback: Indexes can still improve suitable reads.

Correct answers: B

Hint: Consider the extra work required whenever a new row is inserted.

### 12. A table has a composite index on `(dept_id, salary)`. Which query is least likely to benefit from this index as a direct leading-key lookup?

- A. `WHERE dept_id = 10`  
Feedback: This uses the first indexed column.
- B. `WHERE dept_id = 10 AND salary = 50000`  
Feedback: This uses both leading indexed columns.
- C. `WHERE dept_id = 10 AND salary > 50000`  
Feedback: This uses the leading equality column followed by a range condition.
- D. `WHERE salary = 50000`  
Feedback: This skips the leading dept_id column, so the composite index is not a suitable direct lookup for salary alone.

Correct answers: D

Hint: Apply the leftmost-prefix rule to the index's first column.

### 13. Which statements about HSQLDB indexing are correct? Select every correct answer.

- A. HSQLDB automatically creates a non-unique index for a FOREIGN KEY constraint  
Feedback: HSQLDB's documentation explicitly describes an automatically created non-unique foreign-key index.
- B. A composite index on (a, b) is equally useful for a search on b alone  
Feedback: The documented leftmost-prefix behaviour requires the first indexed column for efficient use.
- C. HSQLDB can use suitable indexes for IS NULL and IS NOT NULL conditions  
Feedback: HSQLDB documents index optimisation for both NULL predicates.
- D. Creating an index automatically guarantees that every query will use it  
Feedback: The optimizer chooses an access plan based on estimated cost and suitability.

Correct answers: A, C

Hint: Check HSQLDB's documented constraint-index behaviour and the conditions supported by its optimizer.

### 14. In HSQLDB, an index on `(dept_id, salary)` can support an equality search on dept_id alone.

- true. True  
Feedback: The first column of a composite index can be used independently as a leading-prefix search.
- false. False  
Feedback: The first indexed column can be searched without specifying the later columns.

Correct answers: true

Hint: Consider whether the search starts at the first column of the index.

### 15. HSQLDB's documented CREATE INDEX syntax supports a clustered-index option that physically orders the table rows by the index key.

- true. True  
Feedback: The documented CREATE INDEX syntax does not expose a clustered-index option.
- false. False  
Feedback: HSQLDB's CREATE INDEX syntax creates an index on columns and does not expose the usual clustered-index option.

Correct answers: false

Hint: Distinguish general clustered-index terminology from the actual syntax supported by HSQLDB.

## 14. Official HSQLDB documentation

- HSQLDB - Indexes and Query Speed - index creation for constraints, composite indexes, joins and performance.
- HSQLDB - Index Conditions and Operations - AND, OR, IN, NULL, GROUP BY and ORDER BY index usage.
- HSQLDB - CREATE INDEX and DROP INDEX syntax.
- HSQLDB - System index metadata views.

**Recommended next topic:** Query optimization and execution plans - EXPLAIN PLAN, cost-based optimization, selectivity, cardinality, join algorithms, query rewriting, and how to diagnose slow SQL queries.

### User

for 2 year sql developer hsql database level give concepts needed from required topics all tricky advanced topics from these explanation and 15 question quiz at end all edge cases data control language why dcl,grant revoke syntax grant previlge object grantee previlage: select delete update all object tabe view routine sequence all example table particular column ny grant or revoke previlage be probided to both user and roles

### ChatGPT

# HSQLDB: Data Control Language (DCL) - Complete Advanced Guide for a 2-Year SQL Developer

DCL is used to control **who can access database objects and what operations they are allowed to perform**.

In a real SQL developer role, you may create tables, views, procedures and sequences, but not every database user should have permission to access or modify them.

For example:

- An HR user should be able to view employee records.
- An HR manager should be able to update employee records.
- A reporting user should have read-only access.
- A database administrator should have broader privileges.
- An application user should be allowed to execute a stored procedure without receiving direct access to the underlying tables.

This is where DCL is used.

## 1. What is DCL and why do we need it?

DCL stands for **Data Control Language**.

It controls database permissions and access rights.

The two main DCL commands are:

| Command | Purpose |
| --- | --- |
| `GRANT` | Give privileges to a user or role |
| `REVOKE` | Remove privileges from a user or role |

### Example scenario

Suppose you have a table:

```sql
CREATE TABLE employee (
    emp_id INTEGER PRIMARY KEY,
    emp_name VARCHAR(100),
    salary DECIMAL(10,2),
    dept_id INTEGER
);
```

You create three database users:

- `hr_user`
- `manager_user`
- `report_user`

You want different access levels:

| User | Permission |
| --- | --- |
| HR user | SELECT employee records |
| Manager user | SELECT and UPDATE employee records |
| Reporting user | SELECT employee records only |

Instead of allowing everyone to perform every operation, you grant only the necessary privileges.

**Important distinction:** DCL controls authorization. It does not create database objects or change their structure.

## 2. GRANT - Giving privileges

### 2.1 General syntax

```sql
GRANT privilege_name
ON object_name
TO user_or_role;
```

For example:

```sql
GRANT SELECT
ON employee
TO hr_user;
```

This gives `hr_user` permission to retrieve data from the employee table.

### 2.2 GRANT multiple privileges

```sql
GRANT SELECT, INSERT, UPDATE, DELETE
ON employee
TO manager_user;
```

The manager can:

- Read employee records.
- Insert employee records.
- Update employee records.
- Delete employee records.

### 2.3 GRANT ALL

```sql
GRANT ALL
ON employee
TO manager_user;
```

This grants all applicable privileges on that object that the grantor is authorized to grant.

**Important:** `ALL` does not mean unrestricted DBA or system-administrator privileges. It is limited to the applicable privileges on the specified object.

## 3. Understanding the components of GRANT

Consider:

```sql
GRANT SELECT, UPDATE
ON employee
TO hr_user;
```

| Component | Meaning |
| --- | --- |
| `GRANT` | Permission assignment command |
| `SELECT, UPDATE` | Privileges being granted |
| `ON employee` | Object receiving the privilege assignment |
| `TO hr_user` | Grantee receiving the privileges |

Three important terms:

- **Privilege:** What action is allowed.
- **Object:** Which database object the privilege applies to.
- **Grantee:** The user or role receiving the privilege.

## 4. Important object privileges in HSQLDB

Different database objects support different kinds of privileges.

| Object | Common privilege |
| --- | --- |
| Table | SELECT, INSERT, UPDATE, DELETE, REFERENCES |
| View | SELECT, INSERT, UPDATE, DELETE, REFERENCES, where applicable |
| Routine (procedure/function) | EXECUTE |
| Sequence | USAGE |
| Schema | Applicable schema privileges |

HSQLDB also supports object-specific privileges such as TRIGGER for tables and certain schema-related privileges.

Do not assume that every privilege applies to every object type.

## 5. GRANT on a table - All important privileges

Consider:

```sql
CREATE TABLE employee (
    emp_id INTEGER PRIMARY KEY,
    emp_name VARCHAR(100),
    salary DECIMAL(10,2),
    dept_id INTEGER
);
```

### 5.1 SELECT privilege

Allow a user to retrieve employee data:

```sql
GRANT SELECT
ON TABLE employee
TO hr_user;
```

Now `hr_user` can execute:

```sql
SELECT *
FROM employee;
```

Without SELECT permission, the user cannot retrieve the table's data.

### 5.2 INSERT privilege

```sql
GRANT INSERT
ON TABLE employee
TO hr_user;
```

Allows inserting rows, subject to the other required column privileges and constraints.

### 5.3 UPDATE privilege

```sql
GRANT UPDATE
ON TABLE employee
TO manager_user;
```

Allows the user to update employee columns, subject to applicable privileges and constraints.

### 5.4 DELETE privilege

```sql
GRANT DELETE
ON TABLE employee
TO manager_user;
```

Allows deleting employee rows.

**Important:** In HSQLDB, DELETE is a table-level privilege, not a column-level privilege.

### 5.5 REFERENCES privilege

```sql
GRANT REFERENCES
ON TABLE employee
TO developer_user;
```

Allows the grantee to define a foreign key in another table referencing the granted table.

You can also grant REFERENCES on particular columns:

```sql
GRANT REFERENCES(emp_id)
ON TABLE employee
TO developer_user;
```

### 5.6 TRIGGER privilege

```sql
GRANT TRIGGER
ON TABLE employee
TO developer_user;
```

Allows the grantee to create triggers on the table, subject to the relevant ownership and authorization rules.

### 5.7 Grant multiple privileges to multiple users

```sql
GRANT SELECT, INSERT, UPDATE
ON TABLE employee
TO hr_user, manager_user;
```

Both users receive the listed privileges.

You can also grant privileges to a role and a user in the same statement:

```sql
GRANT SELECT
ON TABLE employee
TO hr_user, reporting_role;
```

**Important:** The `TO` clause can contain multiple grantees. Each grantee can be a user or a role.

## 6. Column-level privileges - Very important

HSQLDB supports granting SELECT, INSERT and UPDATE privileges on particular columns.

This is useful when a user needs access to some columns but should not access confidential information.

Suppose the employee table contains:

| Column | Data |
| --- | --- |
| emp_id | Employee ID |
| emp_name | Employee name |
| salary | Confidential salary |
| dept_id | Department |

You want HR users to see employee IDs, names and departments, but not salaries.

### 6.1 Column-level SELECT

```sql
GRANT SELECT(emp_id, emp_name, dept_id)
ON TABLE employee
TO hr_user;
```

Now HR can execute:

```sql
SELECT emp_id, emp_name, dept_id
FROM employee;
```

But cannot directly retrieve the salary column:

```sql
SELECT salary
FROM employee;
```

This should fail due to insufficient SELECT privilege.

### 6.2 Column-level UPDATE

Suppose HR can update employee names but cannot update salaries.

```sql
GRANT UPDATE(emp_name)
ON TABLE employee
TO hr_user;
```

Allowed:

```sql
UPDATE employee
SET emp_name = 'Arun Kumar'
WHERE emp_id = 10;
```

Not allowed:

```sql
UPDATE employee
SET salary = 60000
WHERE emp_id = 10;
```

### 6.3 Column-level INSERT

```sql
GRANT INSERT(emp_name, dept_id)
ON TABLE employee
TO hr_user;
```

This permits explicit inserts into the specified columns, subject to the table's other requirements.

For example:

```sql
INSERT INTO employee(emp_name, dept_id)
VALUES ('Arun', 10);
```

This is possible only if the omitted columns can be supplied by defaults, generated values or NULLs as permitted by their constraints.

### 6.4 Can DELETE be granted for a particular column?

No.

This is invalid:

```sql
GRANT DELETE(emp_id)
ON TABLE employee
TO hr_user;
```

DELETE applies to the table as a whole.

Correct syntax:

```sql
GRANT DELETE
ON TABLE employee
TO hr_user;
```

### 6.5 Important: SELECT privilege and WHERE conditions

Suppose a user has:

```sql
GRANT SELECT(emp_name)
ON TABLE employee
TO hr_user;
```

Can the user execute:

```sql
SELECT emp_name
FROM employee
WHERE salary > 50000;
```

No. The SELECT privilege also applies to columns referenced in the search condition, not just columns displayed in the result.

The user needs the necessary SELECT privilege on `salary` too.

```sql
GRANT SELECT(emp_name, salary)
ON TABLE employee
TO hr_user;
```

This is an important edge case.

### 6.6 Column-level UPDATE also needs SELECT privileges for reading

Consider:

```sql
UPDATE employee
SET emp_name = 'Kumar'
WHERE emp_id = 10;
```

The user needs:

- UPDATE privilege on `emp_name`.
- SELECT privilege on `emp_id`, because it is referenced in the WHERE condition.

Similarly, if an UPDATE expression reads another column, the required SELECT privilege applies to that column.

**Remember:** Permission to modify a column does not automatically mean permission to read every other column used by the statement.

## 7. GRANT on a VIEW

A view can expose only selected columns or rows from an underlying table.

Example:

```sql
CREATE VIEW employee_public AS
SELECT emp_id, emp_name, dept_id
FROM employee;
```

Now grant access to the view:

```sql
GRANT SELECT
ON employee_public
TO reporting_user;
```

The reporting user can retrieve data through the view:

```sql
SELECT *
FROM employee_public;
```

But the view does not expose the salary column.

This is a useful way to implement controlled data access.

**Important:** A view is not automatically an authorization bypass. HSQLDB checks the relevant privileges and authorization rules for access through views. The view owner and the underlying objects' privileges matter.

### Column-level privilege on a view

```sql
GRANT SELECT(emp_id, emp_name)
ON employee_public
TO report_role;
```

This limits the columns the role can reference through that view.

### Updatable views

If a view is updatable, INSERT, UPDATE and DELETE operations through it can affect the underlying table.

Whether it is updatable depends on its query definition and any applicable triggers.

Granting a privilege on a view does not automatically grant the same direct privilege on its base table.

## 8. GRANT on ROUTINE - Procedures and functions

A routine is a stored procedure or stored function.

For routines, HSQLDB supports the `EXECUTE` privilege.

### 8.1 Create a procedure

```sql
CREATE PROCEDURE get_employee_count()
MODIFIES SQL DATA
BEGIN ATOMIC
    DECLARE employee_count INTEGER;

    SELECT COUNT(*)
    INTO employee_count
    FROM employee;
END;
```

For illustration, suppose this procedure exists in your schema.

Grant permission:

```sql
GRANT EXECUTE
ON PROCEDURE get_employee_count
TO app_user;
```

The user can execute the routine, subject to the routine's definition and other applicable permissions.

### 8.2 Grant EXECUTE to a role

```sql
GRANT EXECUTE
ON PROCEDURE get_employee_count
TO application_role;
```

Then grant the role to the user:

```sql
GRANT application_role
TO app_user;
```

The user receives the routine permission through the role.

### 8.3 Function privilege

```sql
GRANT EXECUTE
ON FUNCTION calculate_bonus
TO payroll_user;
```

### 8.4 Overloaded routines

HSQLDB supports granting EXECUTE on a generic routine name, covering its overloaded versions.

It also supports a specific routine designator when you want to grant permission to a particular signature.

For example, the documented form is:

```sql
GRANT EXECUTE
ON SPECIFIC ROUTINE routine_specific_name
TO app_user;
```

This is useful when a schema contains multiple routines with the same generic name but different parameter signatures.

## 9. GRANT on SEQUENCE

Sequences generate numeric values, often used for identifiers.

Example:

```sql
CREATE SEQUENCE employee_seq
START WITH 1
INCREMENT BY 1;
```

Grant USAGE:

```sql
GRANT USAGE
ON SEQUENCE employee_seq
TO app_user;
```

Now the user can reference the sequence where permitted:

```sql
SELECT NEXT VALUE FOR employee_seq
FROM (VALUES(0)) AS t(x);
```

HSQLDB uses the `NEXT VALUE FOR` expression to obtain the next sequence value.

Granting USAGE does not grant SELECT, UPDATE or DELETE on a table.

### Grant sequence privileges to a role

```sql
GRANT USAGE
ON SEQUENCE employee_seq
TO application_role;
```

Then:

```sql
GRANT application_role
TO app_user;
```

### Grant on all sequences in a schema

```sql
GRANT USAGE
ON ALL SEQUENCES IN SCHEMA company
TO application_role;
```

This is an HSQLDB schema-object-set extension.

## 10. GRANT on all objects in a schema

HSQLDB provides convenient syntax for granting privileges across all applicable objects of a type in a schema.

Examples:

```sql
GRANT SELECT
ON ALL TABLES IN SCHEMA company
TO reporting_role;
```

```sql
GRANT USAGE
ON ALL SEQUENCES IN SCHEMA company
TO application_role;
```

```sql
GRANT EXECUTE
ON ALL ROUTINES IN SCHEMA company
TO application_role;
```

**Important edge case:** These statements apply to the objects included when the grant is made. Do not assume that they automatically grant privileges on every table, sequence or routine created in that schema in the future.

For new objects, the owner or DBA must arrange the required grants.

## 11. CREATE USER and CREATE ROLE

### 11.1 CREATE USER

HSQLDB syntax:

```sql
CREATE USER username
PASSWORD 'password';
```

Example:

```sql
CREATE USER hr_user
PASSWORD 'Hr@12345';
```

This creates a database user.

Only a DBA-authorized user can create database users.

You can also create an administrator:

```sql
CREATE USER admin_user
PASSWORD 'Admin@123'
ADMIN;
```

The `ADMIN` keyword grants the DBA role to that user.

**Important:** Use a secure password in real deployments. These are demonstration passwords only.

### 11.2 CREATE ROLE

A role is a named collection of privileges.

```sql
CREATE ROLE hr_role;
```

Initially, the role has no explicitly granted privileges beyond those it inherits through PUBLIC.

### 11.3 Why use roles instead of granting everything directly to users?

Imagine a company has:

- 20 HR employees.
- 10 managers.
- 30 reporting users.

If you grant privileges individually to 60 users, managing access becomes difficult.

Instead:

```sql
CREATE ROLE hr_role;
CREATE ROLE manager_role;
CREATE ROLE reporting_role;
```

Grant permissions to the roles:

```sql
GRANT SELECT, INSERT, UPDATE
ON employee
TO hr_role;
```

```sql
GRANT SELECT, UPDATE
ON employee
TO manager_role;
```

```sql
GRANT SELECT
ON employee
TO reporting_role;
```

Assign roles to users:

```sql
GRANT hr_role
TO hr_user1, hr_user2, hr_user3;
```

```sql
GRANT manager_role
TO manager1, manager2;
```

```sql
GRANT reporting_role
TO report_user1, report_user2;
```

**How role-based access works**

**Privileges on database objects**

SELECT, INSERT, UPDATE, DELETE

**HR role**

SELECT, INSERT, UPDATE

**Manager role**

SELECT, UPDATE

**Report role**

SELECT

HR users

Managers

Report users

Privileges are maintained centrally through roles and inherited by their members.

### 11.4 Can a role be granted to another role?

Yes. HSQLDB supports role hierarchies.

```sql
CREATE ROLE employee_read_role;
CREATE ROLE hr_role;

GRANT employee_read_role
TO hr_role;
```

Now `hr_role` inherits the privileges assigned to `employee_read_role`.

You can grant `hr_role` to a user:

```sql
GRANT hr_role
TO hr_user;
```

The user receives privileges through the role hierarchy.

### 11.5 WITH ADMIN OPTION

This controls whether the recipient can grant the role to other users or roles.

```sql
GRANT hr_role
TO senior_hr_user
WITH ADMIN OPTION;
```

The senior HR user can now administer the assignment of that role to other grantees, subject to authorization rules.

**Do not confuse:**

| Option | Meaning |
| --- | --- |
| `WITH ADMIN OPTION` | Allows the recipient to grant the role to others |
| `WITH GRANT OPTION` | Allows the recipient to pass granted object privileges to others |

This difference is a frequent exam question.

## 12. WITH GRANT OPTION - Passing privileges to others

Suppose:

```sql
GRANT SELECT
ON employee
TO hr_manager
WITH GRANT OPTION;
```

The HR manager can now grant the SELECT privilege on the employee table to another user or role.

For example:

```sql
GRANT SELECT
ON employee
TO junior_hr;
```

Without `WITH GRANT OPTION`, a user who merely has SELECT permission cannot automatically pass that permission to another user.

### Example of privilege delegation

**Schema owner / DBA**

**HR manager**

(SELECT + GRANT OPTION)

**Junior HR user**

(SELECT)

**Important:** `WITH GRANT OPTION` applies to object privileges. `WITH ADMIN OPTION` applies to role assignment.

## 13. PUBLIC role - Permission for everyone

HSQLDB has a built-in role named `PUBLIC`.

Every authorization in the database automatically has the PUBLIC role.

When you grant a privilege to PUBLIC, it becomes available to all users and roles.

Example:

```sql
GRANT SELECT
ON employee
TO PUBLIC;
```

Now all database users receive SELECT permission on employee through PUBLIC.

### Why is PUBLIC risky?

Suppose the employee table contains confidential salaries.

```sql
GRANT SELECT
ON employee
TO PUBLIC;
```

This allows all database users to access the table, including its salary column.

A better design is to grant access to a restricted view or a specific role.

```sql
GRANT SELECT
ON employee_public
TO reporting_role;
```

**Important:** PUBLIC is a built-in role, not the same as the PUBLIC schema.

## 14. REVOKE - Removing privileges

REVOKE is the opposite of GRANT.

### 14.1 Basic syntax

```sql
REVOKE privilege_name
ON object_name
FROM user_or_role;
```

Example:

```sql
REVOKE SELECT
ON employee
FROM hr_user;
```

The user loses the directly granted SELECT privilege from that grantor.

### 14.2 Revoke multiple privileges

```sql
REVOKE INSERT, UPDATE
ON employee
FROM hr_user;
```

The HR user loses those privileges from the specified grants.

### 14.3 Revoke a particular column privilege

Suppose:

```sql
GRANT SELECT(emp_id, emp_name, salary)
ON employee
TO hr_user;
```

To revoke access to salary:

```sql
REVOKE SELECT(salary)
ON employee
FROM hr_user;
```

The intention is to remove the column-level salary privilege while retaining the other column grants.

Similarly:

```sql
REVOKE UPDATE(salary)
ON employee
FROM hr_user;
```

This removes the UPDATE privilege on the salary column from that grant.

### 14.4 Revoke DELETE

```sql
REVOKE DELETE
ON employee
FROM manager_user;
```

Remember, DELETE is a table-level privilege.

### 14.5 Revoke from a role

```sql
REVOKE UPDATE
ON employee
FROM manager_role;
```

All users who depend on that role for UPDATE access lose that inherited permission, unless they have another applicable grant.

### 14.6 Revoke from multiple grantees

```sql
REVOKE SELECT
ON employee
FROM hr_user, reporting_role;
```

HSQLDB supports multiple grantees in a REVOKE statement.

### 14.7 Revoke a role from a user

This is different from revoking an object privilege.

```sql
REVOKE hr_role
FROM hr_user;
```

This removes the role assignment.

The user may still have permissions granted directly or through another role.

## 15. REVOKE CASCADE vs RESTRICT

This is an advanced and important topic.

Suppose:

1. DBA grants SELECT to manager with GRANT OPTION.
2. Manager grants SELECT to junior user.
3. DBA now revokes SELECT from manager.

What happens to the junior user's grant?

### 15.1 REVOKE CASCADE

```sql
REVOKE SELECT
ON employee
FROM manager_user
CASCADE;
```

CASCADE removes dependent grants that rely on the revoked grant.

The junior user's dependent privilege can also be removed.

### 15.2 REVOKE RESTRICT

```sql
REVOKE SELECT
ON employee
FROM manager_user
RESTRICT;
```

RESTRICT prevents the revocation if dependent grants exist.

The database raises an error rather than automatically removing dependent grants.

### 15.3 GRANT OPTION FOR

Suppose a user has SELECT permission and the ability to grant it to others.

You want to remove only the ability to grant, while retaining the SELECT permission itself.

Use:

```sql
REVOKE GRANT OPTION FOR SELECT
ON employee
FROM manager_user
CASCADE;
```

The user's own SELECT permission can remain, but the ability to pass it to others is removed. Dependent grants are handled according to the chosen CASCADE or RESTRICT behaviour.

### 15.4 Revoke ADMIN OPTION for a role

Similarly, you can remove role-administration authority without necessarily removing role membership:

```sql
REVOKE ADMIN OPTION FOR hr_role
FROM senior_hr_user
CASCADE;
```

The role assignment itself and the authority to administer it are different things.

## 16. HSQLDB-specific advanced DCL: Row-level filtering

One of HSQLDB's useful access-control features is the `FILTER` clause in GRANT.

It allows a role to access only rows satisfying a condition.

Suppose:

```sql
CREATE TABLE employee (
    emp_id INTEGER PRIMARY KEY,
    emp_name VARCHAR(100),
    dept_id INTEGER,
    salary DECIMAL(10,2)
);
```

You want HR users to access only department 10.

```sql
CREATE ROLE dept10_role;

GRANT SELECT
FILTER (WHERE dept_id = 10)
ON TABLE employee
TO dept10_role;
```

Now users assigned this role can see only rows where department ID is 10 through that role's filtered permission.

For example:

```sql
GRANT dept10_role
TO hr_user;
```

This is a form of row-level access control.

### 16.1 Filtered UPDATE privilege

```sql
GRANT UPDATE
FILTER (WHERE dept_id = 10)
ON TABLE employee
TO dept10_role;
```

The role's UPDATE access is restricted to rows satisfying the filter.

### 16.2 Filtered DELETE privilege

```sql
GRANT DELETE
FILTER (WHERE dept_id = 10)
ON TABLE employee
TO dept10_role;
```

The role can delete only rows satisfying that filter through this permission.

### 16.3 Important restrictions

- HSQLDB's filtered grants are an extension beyond standard SQL.
- Fine-grained FILTER grants can be assigned to roles only, not directly to users.
- A user receives the filtered access through membership in the role.
- Filters affect the rows accessed by applicable SELECT, INSERT, UPDATE, DELETE and MERGE operations.
- If you want to change an existing filtered privilege, revoke it before granting the replacement filter.

This is useful for multi-tenant databases, branch-level access and department-level restrictions.

## 17. How to check granted privileges in HSQLDB

In a real SQL developer role, you must know how to inspect permissions rather than simply execute GRANT and REVOKE.

HSQLDB provides system metadata through `INFORMATION_SCHEMA`.

### 17.1 Check table privileges

```sql
SELECT *
FROM INFORMATION_SCHEMA.TABLE_PRIVILEGES;
```

This helps identify table-level privileges and their grantees.

### 17.2 Check column-level privileges

```sql
SELECT *
FROM INFORMATION_SCHEMA.COLUMN_PRIVILEGES;
```

Useful for finding which users or roles can access or modify particular columns.

### 17.3 Check role-based table privileges

```sql
SELECT *
FROM INFORMATION_SCHEMA.ROLE_TABLE_GRANTS;
```

### 17.4 Check routine privileges

```sql
SELECT *
FROM INFORMATION_SCHEMA.ROUTINE_PRIVILEGES;
```

### 17.5 Check sequence and USAGE privileges

```sql
SELECT *
FROM INFORMATION_SCHEMA.USAGE_PRIVILEGES;
```

### 17.6 Check available users and roles

```sql
SELECT *
FROM INFORMATION_SCHEMA.AUTHORIZATIONS;
```

```sql
SELECT *
FROM INFORMATION_SCHEMA.SYSTEM_USERS;
```

The full contents of some user and authorization metadata are restricted to administrators. Other privilege views show information according to the current authorization and active roles.

## 18. Complete practical example - HR access-control setup

Let's combine everything into one scenario.

**Requirement:**

- HR users can read employee names and departments.
- HR users can update employee names.
- HR users cannot access salaries.
- Managers can read and update employee data.
- Reporting users can only read the employee public view.
- Application users can execute a stored routine and use an employee sequence.

### Step 1: Create users and roles

```sql
CREATE USER hr_user
PASSWORD 'Hr@12345';

CREATE USER manager_user
PASSWORD 'Manager@123';

CREATE USER report_user
PASSWORD 'Report@123';

CREATE USER app_user
PASSWORD 'App@12345';

CREATE ROLE hr_role;
CREATE ROLE manager_role;
CREATE ROLE reporting_role;
CREATE ROLE application_role;
```

### Step 2: Grant HR permissions

```sql
GRANT SELECT(emp_id, emp_name, dept_id)
ON employee
TO hr_role;

GRANT UPDATE(emp_name)
ON employee
TO hr_role;
```

### Step 3: Grant manager permissions

```sql
GRANT SELECT, UPDATE
ON employee
TO manager_role;
```

### Step 4: Create a restricted view

```sql
CREATE VIEW employee_public AS
SELECT emp_id, emp_name, dept_id
FROM employee;
```

Grant read access:

```sql
GRANT SELECT
ON employee_public
TO reporting_role;
```

### Step 5: Grant sequence and routine access

```sql
GRANT USAGE
ON SEQUENCE employee_seq
TO application_role;

GRANT EXECUTE
ON PROCEDURE get_employee_count
TO application_role;
```

### Step 6: Assign roles to users

```sql
GRANT hr_role TO hr_user;

GRANT manager_role TO manager_user;

GRANT reporting_role TO report_user;

GRANT application_role TO app_user;
```

### Step 7: Verify permissions

```sql
SELECT *
FROM INFORMATION_SCHEMA.TABLE_PRIVILEGES;
```

```sql
SELECT *
FROM INFORMATION_SCHEMA.COLUMN_PRIVILEGES;
```

```sql
SELECT *
FROM INFORMATION_SCHEMA.ROUTINE_PRIVILEGES;
```

```sql
SELECT *
FROM INFORMATION_SCHEMA.USAGE_PRIVILEGES;
```

This demonstrates role-based access control and least-privilege design.

## 19. Advanced DCL exam traps - Final revision

| Question / trap | Correct understanding |
| --- | --- |
| Can GRANT be given to users and roles? | Yes |
| Can multiple users or roles be specified in one GRANT? | Yes |
| Does GRANT SELECT permit UPDATE? | No |
| Is DELETE a column-level privilege? | No, table-level |
| Can SELECT be granted for specific columns? | Yes |
| Can UPDATE be granted for specific columns? | Yes |
| Can INSERT be granted for specific columns? | Yes |
| Can REFERENCES be granted for specific columns? | Yes |
| Can EXECUTE be granted on procedures/functions? | Yes |
| Can USAGE be granted on sequences? | Yes |
| Does WITH GRANT OPTION allow passing object privileges? | Yes |
| Does WITH ADMIN OPTION allow passing role membership? | Yes |
| Does PUBLIC apply to all database authorizations? | Yes |
| Does revoking a role remove a direct grant? | No |
| Does REVOKE CASCADE remove dependent grants? | Yes |
| Does REVOKE RESTRICT allow dependent grants to remain? | No; it prevents the revoke when dependencies exist |
| Can a role have another role? | Yes |
| Does HSQLDB support column-level privileges? | Yes |
| Does HSQLDB support row-filtered grants? | Yes, for roles |
| Does GRANT SELECT on a view automatically grant SELECT on its base table? | No |

### DCL vs DDL vs DML vs TCL

| Category | Purpose | Examples |
| --- | --- | --- |
| DDL | Define database objects | CREATE, ALTER, DROP |
| DML | Modify data | INSERT, UPDATE, DELETE, MERGE |
| DQL | Retrieve data | SELECT |
| DCL | Manage authorization | GRANT, REVOKE |
| TCL | Manage transactions | COMMIT, ROLLBACK, SAVEPOINT |

**Remember these three especially:**

- `WITH GRANT OPTION` → pass object privileges.
- `WITH ADMIN OPTION` → pass role assignments.
- `CASCADE` → remove dependent grants when revoking.

## 20. Advanced 15-question DCL quiz

(2-year SQL developer level) (15 questions)

This quiz includes column-level permissions, role inheritance, GRANT OPTION, ADMIN OPTION, REVOKE CASCADE, sequences, routines, PUBLIC and HSQLDB-specific filtered privileges.

## HSQLDB Advanced DCL Assessment

### 1. In HSQLDB, which privilege is table-level and cannot be granted for an individual column?

- A. SELECT  
Feedback: SELECT can be granted for specified columns.
- B. UPDATE  
Feedback: UPDATE supports column-level grants.
- C. DELETE  
Feedback: DELETE applies to the table rather than individual columns.
- D. INSERT  
Feedback: INSERT supports column-level grants.

Correct answers: C

Hint: Consider which operation removes an entire row rather than reading or assigning a particular column.

### 2. A user has `GRANT UPDATE(emp_name) ON employee`. The user executes `UPDATE employee SET emp_name = 'Arun' WHERE emp_id = 10`. Which additional privilege is required for the referenced search column?

- A. SELECT(emp_id)  
Feedback: The WHERE condition reads emp_id, so SELECT access to that column is required.
- B. DELETE(emp_id)  
Feedback: DELETE is unrelated to reading the search condition.
- C. INSERT(emp_id)  
Feedback: INSERT permission does not authorize reading emp_id in the WHERE condition.
- D. EXECUTE(emp_id)  
Feedback: EXECUTE applies to routines, not table-column reads.

Correct answers: A

Hint: Separate the privilege needed to change a value from the privilege needed to read the filter column.

### 3. A DBA grants `SELECT ON employee TO hr_manager WITH GRANT OPTION`. What additional capability does hr_manager receive?

- A. Permission to create database users  
Feedback: User creation requires appropriate DBA authority.
- B. Permission to grant the SELECT privilege to other grantees  
Feedback: WITH GRANT OPTION allows passing the granted object privilege to other users or roles.
- C. Permission to grant any role with ADMIN OPTION  
Feedback: WITH GRANT OPTION is not the same as WITH ADMIN OPTION.
- D. Unrestricted access to every table  
Feedback: The grant is limited to the specified object privilege.

Correct answers: B

Hint: Distinguish delegating a table privilege from administering a role.

### 4. What does `GRANT hr_role TO hr_user WITH ADMIN OPTION` allow hr_user to do?

- A. Grant the role to other users or roles  
Feedback: WITH ADMIN OPTION gives authority to administer the assigned role.
- B. Grant every table privilege in the database  
Feedback: Role administration does not automatically provide every object privilege.
- C. Drop the employee table  
Feedback: Role administration does not grant schema ownership or DBA authority.
- D. Change another user's password  
Feedback: That is an administrative operation requiring appropriate authority.

Correct answers: A

Hint: Focus on what the option attached to a role assignment controls.

### 5. A user receives SELECT on employee through hr_role and also has a direct SELECT grant. The direct grant is revoked. What happens to the effective SELECT access if the role membership remains?

- A. SELECT is always removed  
Feedback: The remaining role-based grant can still provide SELECT access.
- B. SELECT remains through hr_role  
Feedback: A privilege can be available through a role even after a separate direct grant is revoked.
- C. The user becomes a DBA  
Feedback: Revoking a direct privilege does not confer administrative authority.
- D. The employee table is dropped  
Feedback: REVOKE changes authorization, not table existence.

Correct answers: B

Hint: Check whether there is another independent authorization path.

### 6. A manager granted SELECT to a junior user using a privilege received WITH GRANT OPTION. The original grant is revoked with CASCADE. What happens to the dependent grant?

- A. It must remain permanently  
Feedback: CASCADE removes dependent grants that rely on the revoked grant.
- B. The dependent grant can also be removed  
Feedback: CASCADE propagates the revocation through dependent privilege grants.
- C. The junior user automatically becomes the owner  
Feedback: Revocation does not transfer object ownership.
- D. The entire database is dropped  
Feedback: CASCADE here concerns dependent authorization grants, not database deletion.

Correct answers: B

Hint: Trace the chain of grants back to the original grantor.

### 7. What happens when REVOKE ... RESTRICT encounters dependent grants that rely on the grant being revoked?

- A. All dependent grants are silently deleted  
Feedback: That is the CASCADE behaviour.
- B. The privilege is always revoked without checks  
Feedback: RESTRICT checks whether dependent grants exist.
- C. The revocation is rejected due to the dependent grants  
Feedback: RESTRICT prevents revocation when dependent grant relationships would be affected.
- D. All roles are dropped  
Feedback: RESTRICT does not destroy roles.

Correct answers: C

Hint: Compare the meaning of restricting a change with propagating that change.

### 8. Which privilege does HSQLDB use for accessing a sequence directly?

- A. SELECT  
Feedback: SELECT is a table or view data privilege, not the sequence privilege.
- B. UPDATE  
Feedback: UPDATE is not the direct sequence access privilege.
- C. EXECUTE  
Feedback: EXECUTE applies to routines.
- D. USAGE  
Feedback: USAGE is the applicable privilege for sequences.

Correct answers: D

Hint: Remember the privilege category used for sequence and type objects.

### 9. Which privilege is required to invoke an SQL procedure or function directly?

- A. TRIGGER  
Feedback: TRIGGER authorizes creating triggers on tables.
- B. EXECUTE  
Feedback: Routines use the EXECUTE privilege.
- C. REFERENCES  
Feedback: REFERENCES allows defining foreign keys against designated keys.
- D. USAGE  
Feedback: USAGE is used for sequences and certain other object types.

Correct answers: B

Hint: Think of the permission associated with calling a stored routine.

### 10. A DBA executes `GRANT SELECT ON employee TO PUBLIC`. Who receives this permission?

- A. Only users created before the GRANT  
Feedback: PUBLIC is not limited to users who existed when the grant was issued.
- B. Only users in the employee schema  
Feedback: PUBLIC is a database role, not a schema membership.
- C. All database authorizations through the built-in PUBLIC role  
Feedback: Every authorization has PUBLIC, so a privilege granted to PUBLIC applies broadly.
- D. Only users with DBA authority  
Feedback: PUBLIC is not restricted to DBA users.

Correct answers: C

Hint: Think of the special role automatically assigned to every authorization.

### 11. Which HSQLDB syntax grants SELECT permission on only emp_id and emp_name to a role?

- A. `GRANT SELECT(emp_id, emp_name) ON TABLE employee TO hr_role`  
Feedback: This is the documented column-level SELECT privilege syntax.
- B. `GRANT SELECT ON COLUMN employee TO hr_role`  
Feedback: This does not specify the permitted column list in the required syntax.
- C. `GRANT SELECT(employee.emp_id, employee.emp_name) TO hr_role`  
Feedback: The ON object clause is missing.
- D. `GRANT COLUMN SELECT ON employee TO hr_role`  
Feedback: This is not HSQLDB's documented GRANT syntax.

Correct answers: A

Hint: The column list follows the privilege name, while the table follows ON.

### 12. HSQLDB's FILTER clause in GRANT statements has which restriction?

- A. It can only be used for PRIMARY KEY constraints  
Feedback: FILTER is an access-control feature, not a key constraint.
- B. Filtered privileges can be granted to roles only  
Feedback: HSQLDB restricts fine-grained FILTER grants to roles.
- C. It can only be used on sequences  
Feedback: FILTER is used for row-level access on tables.
- D. It is available only for DBA users  
Feedback: The filter grant is assigned to roles that can then be granted to users.

Correct answers: B

Hint: Consider the grantee type required for HSQLDB's row-filtered authorization feature.

### 13. Which statements about HSQLDB table privileges are correct? Select every correct answer.

- A. DELETE is a table-level privilege  
Feedback: HSQLDB does not support granting DELETE on an individual column.
- B. SELECT can be granted for specific columns  
Feedback: HSQLDB supports a column list for SELECT grants.
- C. INSERT can be granted for specified columns  
Feedback: HSQLDB supports column-level INSERT privileges.
- D. UPDATE can never be granted at column level  
Feedback: UPDATE supports column-level grants in HSQLDB.

Correct answers: A, B, C

Hint: Evaluate each privilege independently rather than assuming all table operations have identical granularity.

### 14. In HSQLDB, granting SELECT on a table to a role and then granting that role to a user allows the user to inherit the table access.

- true. True  
Feedback: A user receives privileges through roles assigned to that user, including applicable role hierarchies.
- false. False  
Feedback: Role membership is specifically designed to provide inherited access rights.

Correct answers: true

Hint: Think about how privileges assigned to a role become available to its members.

### 15. In HSQLDB, `GRANT SELECT ON ALL TABLES IN SCHEMA company TO reporting_role` automatically grants SELECT on every table that will be created in that schema in the future.

- true. True  
Feedback: The statement grants privileges on the applicable existing schema objects; it is not a general future-object default privilege declaration.
- false. False  
Feedback: The grant does not automatically cover future tables. New objects need their own appropriate grants.

Correct answers: false

Hint: Distinguish granting on a set of objects from defining a default privilege for future objects.

## 21. Official HSQLDB references

For version-specific syntax and edge cases:

- HSQLDB 2.7 - Access Control - GRANT, REVOKE, roles, column privileges and row filters.
- HSQLDB User Guide - Schemas and Database Objects - views, routines, sequences and schema objects.
- HSQLDB 2.7.4 Official User Guide PDF - complete SQL reference.

**Recommended next topic:** SQL transactions and TCL - COMMIT, ROLLBACK, SAVEPOINT, ACID properties, isolation levels, dirty reads, non-repeatable reads, phantom reads, locks and deadlocks. These are essential for a 2-year SQL developer role.

### User

for 2 year sql developer hsql database level give concepts needed from required topics all tricky advanced topics from these explanation and 15 question quiz at end all edge cases what is the need fr transactin handlling ensure data remains consistent user can access data concurrently transacrion done between2 users update 1 account reduce and that account add 2 update statement how do we ensure 2 complete successfully or none completes, what is transaction what it does for dbms,  how is transaction perfroms in database, transaction syntax set transaction mode: read only or read write query commit/rollback after end of each unit add commit or rollback ensure atomic consistent successfull, autocommit : if set autocommit true after every transaction commit is automatically issued default state of database, autocommit false: commit or rollback has to be manually added after set transactions show autocommit diplay status of autocommit property transaction states explain begin aactive partially commited commited failed aborted, transaction acid properties brief, transaction processisn systsem barch transaction processing ssystem explain real time transaction processing, online transaction processing system explain explaineach seperately , batch series of task to be executed in sequential order no user intervention automation of repeated tasks, real time processing system: handling expected to unexpected outputs application require user input stream of input at each stafes and have deadline for completion, online transaction: users to interact and provide input at stages in online and provide appropriate commands, requirements fr oltp system data inegrity scaabiity concurrency problems associated with cncurrent execution : lost update dirty read phantom record incrrect summary concurrecny techniqu: locking timestamp ordering, serializability, validation based crisply explain these locking explain shared mode exclusive mode shared lock higher transaction concurrency exclusive lock low transaction concurrency, when table locked in shared mode and read other transaction can also read it , exclusive lock : if t1 puts lock on resource no other transaction can put s or x lock on any resources lock matrix  explain 2 phase locking protocool for shared lock and exclusive lock read commited isolation + 2 phase locking used in hsql,

### ChatGPT

# HSQLDB Transactions - Advanced SQL Developer Study Guide

This guide covers transaction handling at a **2-year SQL developer level**, including HSQLDB syntax, concurrent account updates, transaction states, ACID, batch processing vs real-time processing vs OLTP, concurrency problems, locking, lock compatibility, two-phase locking (2PL), isolation levels and advanced edge cases.

## 1. What is a transaction?

A **transaction** is a logical unit of database work consisting of one or more SQL statements. The database treats the statements as one unit: either the transaction's changes are committed, or its uncommitted changes are rolled back.

For example, transferring ₹1,000 from Account A to Account B requires two updates:

1. Deduct ₹1,000 from Account A.
2. Add ₹1,000 to Account B.

Both updates must succeed together. If the first succeeds but the second fails, the database must not leave the money deducted from A without crediting B.

### Example: Bank transfer

Assume these rows:

| Account | Balance |
| --- | --- |
| A | 10,000 |
| B | 5,000 |

```sql
START TRANSACTION;

UPDATE accounts
SET balance = balance - 1000
WHERE account_id = 1;

UPDATE accounts
SET balance = balance + 1000
WHERE account_id = 2;

COMMIT;
```

If an error occurs after the first update but before the second, use:

```sql
ROLLBACK;
```

The rollback undoes the transaction's uncommitted changes.

**Important:** `COMMIT` is not simply a command to save the last SQL statement. It commits the entire current transaction. Similarly, `ROLLBACK` rolls back the current transaction, not just the immediately preceding statement.

## 2. Why is transaction handling needed?

Transactions solve two major problems:

- **All-or-nothing execution:** multiple related statements must succeed or fail as a unit.
- **Concurrent access:** multiple users may read or modify the same data at the same time. The DBMS must prevent conflicting operations from producing incorrect results.

Other reasons include:

- Maintaining referential integrity and business rules.
- Preventing partial updates when errors occur.
- Recovering from application failures.
- Coordinating changes across multiple tables.
- Ensuring that concurrent transactions do not corrupt data.

### Two users updating the same account

Suppose an account has ₹10,000. Two users simultaneously withdraw ₹2,000 and ₹3,000.

A problematic sequence without proper concurrency control could be:

| Step | Transaction T1 | Transaction T2 |
| --- | --- | --- |
| 1 | Reads balance = 10,000 |  |
| 2 |  | Reads balance = 10,000 |
| 3 | Calculates 8,000 |  |
| 4 |  | Calculates 7,000 |
| 5 | Writes 8,000 |  |
| 6 |  | Writes 7,000 |

The final balance becomes ₹7,000, even though ₹5,000 should have been withdrawn and the balance should be ₹5,000.

This is called a **lost update**.

Transactions alone are not enough to prevent this. The DBMS also needs concurrency-control mechanisms, such as locking or other isolation mechanisms.

A safer application pattern is to perform a conditional update:

```sql
UPDATE accounts
SET balance = balance - 2000
WHERE account_id = 1
  AND balance >= 2000;
```

Then check the affected-row count. If zero rows were updated, the withdrawal was not performed. This also helps prevent a negative balance.

## 3. How does a transaction work inside the DBMS?

A typical transaction follows this sequence:

1. A client connects to the database and obtains a database session.
2. The session starts a transaction when it executes a transactional statement (or explicitly starts one).
3. The DBMS checks permissions, constraints and data types.
4. The DBMS coordinates concurrent access using its transaction-control mechanism.
5. Changes are made within the transaction.
6. On `COMMIT`, the DBMS makes the transaction's changes committed.
7. On `ROLLBACK`, the DBMS undoes the transaction's uncommitted changes.

The DBMS also maintains recovery information so it can recover from failures. The exact implementation depends on the database engine and transaction-control mode.

### HSQLDB transaction syntax

HSQLDB supports explicit transaction start and transaction characteristics:

```sql
START TRANSACTION;

-- SQL statements
UPDATE accounts
SET balance = balance - 1000
WHERE account_id = 1;

COMMIT;
```

You can also set the next transaction's characteristics:

```sql
SET TRANSACTION READ WRITE;

START TRANSACTION;

UPDATE accounts
SET balance = balance + 500
WHERE account_id = 2;

COMMIT;
```

Or specify both access mode and isolation:

```sql
SET TRANSACTION
    READ WRITE,
    ISOLATION LEVEL READ COMMITTED;
```

Available transaction access modes:

| Mode | Meaning |
| --- | --- |
| `READ ONLY` | Transaction is intended for reading, not modifying database data. |
| `READ WRITE` | Transaction can read and modify data, subject to permissions and constraints. |

**Important HSQLDB detail:** `SET TRANSACTION` sets characteristics for the next transaction. It must be issued before that transaction starts (or after the preceding transaction ends). `START TRANSACTION` cannot be called in the middle of an active transaction. Also, HSQLDB starts transactions automatically when transactional statements are executed, so explicit `START TRANSACTION` is not always required.

## 4. COMMIT and ROLLBACK

### COMMIT

Makes the current transaction's changes permanent from the perspective of subsequent transactions.

```sql
START TRANSACTION;

INSERT INTO employees(employee_id, employee_name)
VALUES (101, 'Arun');

UPDATE departments
SET employee_count = employee_count + 1
WHERE department_id = 10;

COMMIT;
```

### ROLLBACK

Cancels the uncommitted changes made in the current transaction.

```sql
START TRANSACTION;

UPDATE accounts
SET balance = balance - 1000
WHERE account_id = 1;

ROLLBACK;
```

The balance returns to its pre-transaction value.

### Tricky cases

| Situation | Result |
| --- | --- |
| `COMMIT` after successful updates | Changes are committed. |
| `ROLLBACK` after successful but uncommitted updates | Changes are undone. |
| `ROLLBACK` after `COMMIT` | Cannot undo the already committed transaction. |
| `COMMIT` after `ROLLBACK` | Does not restore rolled-back changes. |
| An individual statement fails | HSQLDB normally raises an error; the whole transaction is not necessarily rolled back. |
| A concurrency conflict occurs | HSQLDB may implicitly roll back the transaction and raise an exception. |
| Connection closes with an active transaction | Do not rely on an application connection closing as a substitute for explicitly committing or rolling back. |

HSQLDB also performs automatic commits around schema definition/manipulation statements. Therefore, do not assume that a `CREATE TABLE` or `ALTER TABLE` can be undone using `ROLLBACK`.

## 5. AUTOCOMMIT

Autocommit determines whether the database connection automatically commits after each transactional SQL statement.

### AUTOCOMMIT TRUE

```sql
SET AUTOCOMMIT TRUE;

UPDATE accounts
SET balance = balance - 1000
WHERE account_id = 1;
```

The update is automatically committed after the statement succeeds.

If you then execute another statement and it fails, the earlier committed update is not automatically undone.

### AUTOCOMMIT FALSE

```sql
SET AUTOCOMMIT FALSE;

UPDATE accounts
SET balance = balance - 1000
WHERE account_id = 1;

UPDATE accounts
SET balance = balance + 1000
WHERE account_id = 2;

COMMIT;
```

Now the two updates belong to one transaction. If the second operation fails, the application can issue `ROLLBACK` to undo the first operation as well.

| Feature | Autocommit TRUE | Autocommit FALSE |
| --- | --- | --- |
| Commit after each transactional statement | Yes | No |
| Manual `COMMIT` needed for a multi-statement transaction | Yes, turn autocommit off first | Yes |
| Manual `ROLLBACK` available for uncommitted changes | No previous statement remains uncommitted | Yes |
| Suitable for | Independent statements | Related multi-statement operations |

### HSQLDB default

A new HSQLDB JDBC connection starts in autocommit mode by default. The SQL command is:

```sql
SET AUTOCOMMIT TRUE;
SET AUTOCOMMIT FALSE;
```

To inspect the current setting, use the JDBC connection property `Connection.getAutoCommit()` in Java. Do not assume a portable SQL `SHOW AUTOCOMMIT` command exists in HSQLDB. Autocommit is a connection/session property, not a database-wide setting.

**Java JDBC equivalent:**

```java
connection.setAutoCommit(false);

try {
    // Execute first update
    // Execute second update

    connection.commit();
} catch (Exception e) {
    connection.rollback();
}
```

A common mistake is switching autocommit to `TRUE` while a transaction is active: JDBC's `setAutoCommit(true)` commits the current transaction. Manage this setting deliberately.

## 6. Transaction states

A transaction can pass through several conceptual states during its lifecycle.

**ACTIVE**

Transaction is executing statements: SELECT, INSERT, UPDATE, DELETE.

**PARTIALLY COMMITTED**

The final statement has executed; the DBMS is completing the commit process.

**COMMITTED**

The transaction has successfully committed.

---

**FAILED**

An error or failure prevents the transaction from completing.

**ABORTED**

The transaction is rolled back; its uncommitted changes are undone.

### Meaning of each state

| State | Explanation |
| --- | --- |
| Active | Transaction is executing. |
| Partially committed | Last statement has executed, but the commit process is not yet complete. |
| Committed | Changes have been successfully committed. |
| Failed | Transaction cannot proceed because of an error or failure. |
| Aborted | DBMS has undone its uncommitted changes. |
| Terminated | Transaction has left the system after committing or aborting. |

**Tricky distinction:** A transaction that has executed its last SQL statement is not necessarily committed. It still needs a successful commit. These are conceptual DBMS transaction states, not commands you execute manually in HSQLDB.

## 7. ACID properties

ACID describes the four properties that make transactions reliable.

| Property | Meaning | Bank transfer example |
| --- | --- | --- |
| **Atomicity** | All operations succeed or none do. | Debit and credit both happen, or neither happens. |
| **Consistency** | A committed transaction preserves database rules and constraints. | Account balances must obey the application's rules. |
| **Isolation** | Concurrent transactions should not interfere in ways that produce invalid results. | Two withdrawals should not overwrite each other's changes. |
| **Durability** | Once committed, changes survive failures according to the database's durability guarantees. | A committed transfer must not disappear after a crash. |

### Important edge cases

- Atomicity does not mean every SQL statement in the database succeeds together. It means the statements in the current transaction are treated as one unit.
- Consistency depends on constraints, database rules and correct application logic. A DBMS cannot automatically enforce every business rule unless it is encoded.
- Isolation does not necessarily mean only one user can access the database at a time. Many users can work concurrently.
- Durability is about committed data surviving failures; it is not the same as isolation.

## 8. Types of transaction processing systems

These three terms are related, but they describe different processing patterns.

### A. Batch processing system

A batch processing system collects a group of tasks or records and processes them together, often automatically, without requiring user interaction for every record.

**Example: Monthly salary processing**

1. Read employee records.
2. Calculate salary, tax and deductions.
3. Generate salary records.
4. Update payroll tables.
5. Generate payslips or reports.

Other examples:

- Monthly bank interest calculation.
- Bulk invoice generation.
- Nightly data warehouse ETL.
- Processing thousands of uploaded records.

**Characteristics**

- Processes large volumes of data.
- Usually scheduled.
- Minimal interaction while the batch is running.
- Can be divided into smaller transactions or batches.
- Errors may be logged for individual records and retried.

**Tricky point:** A batch job is not automatically one giant transaction. It may commit after each record, each group of records, or only after the entire batch, depending on the design.

### B. Real-time processing system

A real-time processing system processes inputs and produces outputs within a required time constraint or deadline.

The important feature is **timeliness**: a result delivered too late may be useless even if it is correct.

Examples:

- Vehicle braking control.
- Aircraft control systems.
- Industrial machine monitoring.
- Medical device monitoring.

**Characteristics**

- Inputs may arrive continuously.
- The system processes events as they occur.
- Output must meet a timing requirement.
- Delays can have serious consequences in hard real-time systems.

Types:

| Type | Meaning | Example |
| --- | --- | --- |
| Hard real-time | Missing a deadline is considered system failure. | Airbag deployment. |
| Soft real-time | Missing a deadline reduces quality but may not cause total failure. | Video streaming. |

**Important:** Real-time processing does not necessarily require a user to provide input at every stage. It may process sensor events automatically.

### C. Online Transaction Processing (OLTP)

OLTP systems handle many short, interactive transactions from multiple users or applications.

Examples:

- Banking applications.
- Online shopping.
- Railway reservation systems.
- ATM transactions.
- Inventory management.

**Online shopping example:**

1. Customer places an order.
2. System checks product availability.
3. System creates an order.
4. System reduces available inventory.
5. System records payment status.

These operations must preserve data consistency even when many customers place orders simultaneously.

### OLTP requirements

| Requirement | Explanation |
| --- | --- |
| Data integrity | Data must obey constraints and business rules. |
| Concurrency | Many users should work simultaneously. |
| Scalability | System should handle increasing users and transactions. |
| Availability | System should remain accessible when needed. |
| Fast response | Short transactions should complete quickly. |
| Reliability | Failed operations must not leave partial business changes. |
| Recovery | Database should recover from failures. |

### Comparison

| Feature | Batch | Real-time | OLTP |
| --- | --- | --- | --- |
| Processing | Group of records | Event/input as it occurs | Individual transactions |
| User interaction | Usually low during processing | Not necessarily interactive | Usually interactive |
| Timing | Scheduled or periodic | Deadline-driven | Fast response expected |
| Typical workload | Large jobs | Continuous or event-driven | Many short transactions |
| Example | Payroll | Airbag control | Banking |

**Exam point:** OLTP is a type of online transaction-oriented workload. Real-time processing is defined by timing requirements. They are not interchangeable terms.

## 9. Concurrency problems

Concurrency occurs when multiple transactions execute during overlapping periods.

Concurrency is useful because it allows multiple users to access the database without waiting for every other user to finish. But without appropriate control, concurrent operations can produce anomalies.

### A. Lost update

Two transactions read the same original value and then update it. One transaction overwrites the other's update.

Initial balance = ₹10,000.

| Step | T1 | T2 |
| --- | --- | --- |
| 1 | Reads 10,000 |  |
| 2 |  | Reads 10,000 |
| 3 | Calculates 8,000 |  |
| 4 |  | Calculates 7,000 |
| 5 | Writes 8,000 |  |
| 6 |  | Writes 7,000 |

Final balance = ₹7,000 instead of ₹5,000.

**Prevention:** Appropriate write locks, optimistic conflict detection, or atomic updates.

### B. Dirty read

T1 updates a value but has not committed. T2 reads that uncommitted value.

| Step | T1 | T2 |
| --- | --- | --- |
| 1 | Updates balance to 5,000 |  |
| 2 |  | Reads balance = 5,000 |
| 3 | Rolls back |  |
| 4 |  | Has used an uncommitted value |

T2 read data that never became committed.

**Prevention:** Use at least READ COMMITTED isolation. HSQLDB does not allow dirty reads in its version 2 transaction models; a request for READ UNCOMMITTED is promoted to READ COMMITTED.

### C. Non-repeatable read / Fuzzy read

T1 reads the same row twice, but another transaction modifies and commits it between the reads.

| Step | T1 | T2 |
| --- | --- | --- |
| 1 | Reads salary = 40,000 |  |
| 2 |  | Updates salary to 45,000 |
| 3 |  | COMMIT |
| 4 | Reads salary = 45,000 |  |

The same query against the same row produces a different value within T1's transaction.

**Prevention:** REPEATABLE READ or SERIALIZABLE, depending on the DBMS implementation.

### D. Phantom read

T1 executes a query that returns a set of rows. T2 inserts a new row matching the same condition and commits. When T1 repeats its query, it sees an additional row.

T1:

```sql
SELECT *
FROM employees
WHERE salary > 50000;
```

T2:

```sql
INSERT INTO employees(employee_id, salary)
VALUES (101, 60000);

COMMIT;
```

T1 executes the same SELECT again and finds a new matching row.

That newly appearing row is called a **phantom row**.

**Prevention:** SERIALIZABLE isolation or suitable range/predicate locking, depending on the concurrency model.

### E. Incorrect summary / Inconsistent analysis

T1 calculates the total balance across multiple accounts while T2 transfers money between those accounts.

Suppose:

- Account A = ₹10,000
- Account B = ₹5,000
- Total = ₹15,000

T2 transfers ₹2,000 from A to B.

If T1 reads A before the transfer and B after the transfer, it might calculate:

- A = ₹10,000
- B = ₹7,000
- Total = ₹17,000

The summary is incorrect because it combines values from different points in time.

**Prevention:** Use an isolation level or concurrency strategy that provides a consistent view for the entire calculation.

### Summary of concurrency anomalies

| Problem | What happens? | Typical prevention |
| --- | --- | --- |
| Lost update | One update overwrites another | Write locks or conflict detection |
| Dirty read | Reads uncommitted data | READ COMMITTED or stronger |
| Non-repeatable read | Same row returns a different committed value | REPEATABLE READ or stronger |
| Phantom read | Repeated condition query returns additional/missing rows | SERIALIZABLE or predicate/range protection |
| Incorrect summary | Aggregate sees inconsistent values across rows | Consistent snapshot or SERIALIZABLE |

## 10. Concurrency control techniques

The major approaches are:

1. Lock-based concurrency control.
2. Timestamp ordering.
3. Optimistic / validation-based concurrency control.
4. Serializability as a correctness criterion.

### A. Lock-based concurrency control

A transaction must obtain a suitable lock before accessing a protected resource.

Two important lock modes:

- Shared lock (S): permits reading.
- Exclusive lock (X): permits writing.

A lock may protect a row, page, table or another resource, depending on the database implementation.

#### Shared lock (S lock)

Used for reading a resource.

- Multiple transactions can hold shared locks on the same resource simultaneously.
- A shared lock conflicts with an exclusive lock on the same resource.
- It permits concurrent reads.

Example:

| Transaction | Operation |
| --- | --- |
| T1 | Acquires S lock on table A |
| T2 | Acquires S lock on table A |
| T3 | Requests X lock on table A |

T1 and T2 can both read. T3 must wait until the conflicting shared locks are released.

#### Exclusive lock (X lock)

Used for writing a resource.

- Only one transaction can hold an exclusive lock on a given resource.
- No other transaction can obtain a shared or exclusive lock on that same resource while the X lock is held.
- It prevents conflicting reads/writes under a locking model.

Example:

| Transaction | Operation |
| --- | --- |
| T1 | Acquires X lock on table A |
| T2 | Requests S lock on table A |
| T3 | Requests X lock on table A |

T2 and T3 must wait until T1 releases its lock.

**Correction to remember:** An X lock does not block access to every resource in the database. It blocks incompatible locks on the *same protected resource*. A transaction can still access unrelated resources if no other constraint prevents it.

### Lock compatibility matrix

This is the standard compatibility matrix for shared and exclusive locks on the same resource.

| Existing lock ↓ / Requested lock → | Shared (S) | Exclusive (X) |
| --- | --- | --- |
| Shared (S) | (Compatible) | (Incompatible) |
| Exclusive (X) | (Incompatible) | (Incompatible) |

Remember:

- S + S = allowed.
- S + X = not allowed.
- X + S = not allowed.
- X + X = not allowed.

### B. Two-Phase Locking (2PL) protocol

2PL is a locking protocol that divides a transaction's locking activity into two phases.

**Phase 1: Growing phase**

(Acquire locks)

- Transaction can acquire new locks.
- It can upgrade a shared lock to an exclusive lock, if allowed.
- It cannot release locks.

---

**Lock point**

The point at which the transaction acquires its final lock.

---

**Phase 2: Shrinking phase**

(Release locks)

- Transaction releases locks.
- It cannot acquire any new locks after releasing its first lock.

**Key rule:** Once a transaction releases a lock, it cannot acquire another lock under basic 2PL.

#### Example of valid 2PL

```text
T1:
1. Acquire S lock on A
2. Acquire X lock on B
3. Read A
4. Update B
5. Release S lock on A
6. Release X lock on B
```

This is valid: it acquires all required locks before it starts releasing them.

#### Example of invalid 2PL

```text
T1:
1. Acquire S lock on A
2. Read A
3. Release S lock on A
4. Acquire X lock on B
```

This violates 2PL because T1 acquires a new lock after entering the shrinking phase.

### Variants of 2PL

| Variant | Rule | Main property |
| --- | --- | --- |
| Basic 2PL | Growing then shrinking | Ensures conflict serializability |
| Conservative / Static 2PL | Acquires all required locks before execution | Prevents deadlocks caused by lock acquisition |
| Strict 2PL | Holds exclusive locks until commit/rollback | Prevents other transactions from reading/writing uncommitted writes |
| Rigorous 2PL | Holds all locks, including shared locks, until commit/rollback | Stronger lock retention |

**Tricky distinction:** Basic 2PL does not necessarily prevent cascading rollbacks. Strict 2PL avoids this by retaining write locks until transaction completion.

### C. Timestamp ordering

Each transaction receives a unique timestamp when it begins.

The DBMS uses these timestamps to determine the allowed order of conflicting reads and writes.

Example:

- T1 starts at timestamp 10.
- T2 starts at timestamp 20.

T1 is older than T2.

Timestamp-ordering rules use the resource's read timestamp and write timestamp to determine whether an operation is valid. If an operation would violate the timestamp order, the DBMS may reject and restart the transaction.

**Advantages:**

- Does not require transactions to wait for locks in the same way as lock-based systems.
- Provides a serial ordering based on timestamps.

**Disadvantages:**

- Transactions may repeatedly abort and restart.
- Long-running transactions can suffer from repeated restarts.

### D. Validation-based / Optimistic concurrency control

This approach assumes conflicts are relatively rare.

A transaction proceeds in three phases:

1. **Read phase:** Reads data and performs calculations, recording what it has read and intends to write.
2. **Validation phase:** Checks whether concurrent transactions have created conflicts that make its changes unsafe.
3. **Write phase:** If validation succeeds, the changes are applied. Otherwise, the transaction is aborted and may be retried.

Example:

Two users read a product quantity of 10.

- T1 plans to reduce it by 2.
- T2 plans to reduce it by 3.
- Before either writes, validation checks whether their operations conflict.
- The system permits a safe serial outcome or aborts one transaction for retry.

**Best suited to:** Workloads with many reads and relatively few write conflicts.

## 11. Serializability

Serializability is a correctness property used to determine whether concurrent transactions produce a result equivalent to executing those transactions one after another in some serial order.

### Serial execution

T1 completes first, then T2:

```text
T1: Read A
T1: Update A
T1: Commit

T2: Read A
T2: Update A
T2: Commit
```

### Concurrent execution

Their operations are interleaved:

```text
T1: Read A
T2: Read B
T1: Update A
T2: Update B
T1: Commit
T2: Commit
```

If the concurrent schedule is equivalent to a valid serial schedule, it is serializable.

### Conflict serializability

Two operations conflict when:

1. They belong to different transactions.
2. They access the same data item.
3. At least one operation is a write.

| Operation 1 | Operation 2 | Conflict? |
| --- | --- | --- |
| Read A | Read A | No |
| Read A | Write A | Yes |
| Write A | Read A | Yes |
| Write A | Write A | Yes |
| Read A | Write B | No, assuming A and B are separate data items |

**Precedence graph rule:**

- Create one node for each transaction.
- Draw an edge T1 → T2 if a conflicting operation of T1 occurs before an operation of T2.
- If the graph has no cycle, the schedule is conflict-serializable.
- If the graph has a cycle, it is not conflict-serializable.

This is an important advanced interview and examination concept.

## 12. Isolation levels

Isolation levels determine how much one transaction is protected from changes made by other concurrent transactions.

| Isolation level | Dirty read | Non-repeatable read | Phantom read |
| --- | --- | --- | --- |
| READ UNCOMMITTED | Possible in the SQL standard | Possible | Possible |
| READ COMMITTED | Prevented | Possible | Possible |
| REPEATABLE READ | Prevented | Prevented | Possible in the SQL standard |
| SERIALIZABLE | Prevented | Prevented | Prevented |

### READ UNCOMMITTED

The weakest standard isolation level. It may permit reading uncommitted data.

### READ COMMITTED

A transaction reads only committed data. However, if another transaction commits a change between two reads, the first transaction may see a different value.

### REPEATABLE READ

If a transaction reads a row, another transaction cannot change that row in a way that makes the first transaction's repeated read return a different committed value.

The SQL standard does not require this level to prevent all phantom rows.

### SERIALIZABLE

The strongest standard isolation level. It requires concurrent transactions to behave as though they executed in a serial order.

### HSQLDB-specific isolation behaviour

This is an important distinction for your HSQLDB exam:

- HSQLDB's default isolation level for a new session is `READ COMMITTED`.
- HSQLDB's default concurrency-control model is `LOCKS`, which implements two-phase locking.
- In this default 2PL model, read locks are released after each operation at `READ COMMITTED`, while write locks are retained until commit or rollback.
- HSQLDB promotes `READ UNCOMMITTED` to `READ COMMITTED`.
- In the 2PL model, HSQLDB promotes `REPEATABLE READ` to `SERIALIZABLE`.

Therefore, the accurate statement is:

**HSQLDB's default configuration uses READ COMMITTED isolation with the 2PL locking model.** It is not accurate to say that all HSQLDB transactions always use 2PL: HSQLDB also supports MVCC and a hybrid MVLOCKS model.

## 13. HSQLDB concurrency-control modes

HSQLDB supports three database-wide concurrency-control models.

| Model | Full name | Main behaviour |
| --- | --- | --- |
| LOCKS | Two-phase locking | Uses shared and exclusive table locks. |
| MVLOCKS | 2PL + multiversion rows | Combines locking for updates with snapshot-based reads. |
| MVCC | Multiversion concurrency control | Uses multiple row versions; readers generally do not need shared read locks. |

The DBA can change the database's concurrency-control model:

```sql
SET DATABASE TRANSACTION CONTROL LOCKS;
```

Other supported values:

```sql
SET DATABASE TRANSACTION CONTROL MVLOCKS;

SET DATABASE TRANSACTION CONTROL MVCC;
```

### HSQLDB LOCKS model

This is the default model.

- Reading a table obtains a shared lock.
- Writing to a table obtains an exclusive lock.
- Multiple shared locks can coexist.
- An exclusive lock conflicts with shared and exclusive locks.
- A conflicting session waits until the other session commits or rolls back, or an error is raised if the operation would cause a deadlock.

**Very important:** HSQLDB's documented 2PL model uses table locks for this behaviour. Do not assume that its default 2PL implementation is the same as a row-level locking implementation in another database.

### HSQLDB READ COMMITTED with 2PL

This is the default combination.

| Lock type | When released |
| --- | --- |
| Shared/read lock | After each operation |
| Exclusive/write lock | At transaction commit or rollback |

Example:

```text
T1:
SELECT * FROM accounts WHERE account_id = 1;
-- Read lock is released after this operation.

T2:
UPDATE accounts
SET balance = balance + 100
WHERE account_id = 1;
COMMIT;

T1:
SELECT * FROM accounts WHERE account_id = 1;
-- May see T2's newly committed value.
```

This is why a repeated read under READ COMMITTED may return a different value.

### HSQLDB MVCC

MVCC means **Multiversion Concurrency Control**.

Instead of requiring readers and writers to block one another using shared locks, the database maintains multiple versions of rows.

Example:

- T1 reads the current version of a row.
- T2 updates that row and commits.
- T1 can continue reading its consistent version, depending on its isolation mode.
- Readers and writers can therefore operate with less blocking.

HSQLDB maps its isolation levels to MVCC-specific behaviours:

- READ COMMITTED corresponds to READ CONSISTENCY.
- REPEATABLE READ and SERIALIZABLE correspond to SNAPSHOT ISOLATION.
- READ UNCOMMITTED is promoted to READ COMMITTED.

This is one reason MVCC can improve concurrency in read-heavy or highly concurrent workloads.

## 14. Explicit table locking in HSQLDB

HSQLDB provides `LOCK TABLE` when a transaction needs to obtain locks before executing a group of statements.

```sql
SET AUTOCOMMIT FALSE;

START TRANSACTION;

LOCK TABLE accounts WRITE, customers READ;

-- Perform related operations

COMMIT;
```

Syntax:

```sql
LOCK TABLE table_name READ;
LOCK TABLE table_name WRITE;
```

You can lock multiple tables in one statement:

```sql
LOCK TABLE
    accounts WRITE,
    customers READ,
    departments READ;
```

- `READ` obtains a read/shared lock.
- `WRITE` obtains a write/exclusive lock.
- The statement waits until it can obtain the requested locks.
- The locks are released by `COMMIT` or `ROLLBACK`.

**HSQLDB edge cases:**

1. At READ COMMITTED, read locks are released after each operation. HSQLDB's guide recommends using WRITE locks in this mode when using `LOCK TABLE`.
2. In the MVCC transaction-control model, `LOCK TABLE` has no effect.
3. Acquire all necessary locks at the beginning of the transaction to reduce contention and deadlock risk.

## 15. Deadlock

A deadlock occurs when two or more transactions wait for each other indefinitely because each holds a resource needed by another.

Example:

| Step | T1 | T2 |
| --- | --- | --- |
| 1 | Locks A |  |
| 2 |  | Locks B |
| 3 | Requests B |  |
| 4 |  | Requests A |

- T1 holds A and waits for B.
- T2 holds B and waits for A.
- Neither can proceed.

This is a circular wait.

### How to reduce deadlocks

- Access tables/resources in a consistent order.
- Keep transactions short.
- Avoid waiting for user input while holding locks.
- Acquire required locks early where appropriate.
- Use indexes and efficient queries to reduce transaction duration.
- Handle deadlock exceptions and retry transactions safely.

HSQLDB detects deadlocks and may roll back the current transaction when a conflicting operation cannot proceed.

## 16. SAVEPOINT - partial rollback

A savepoint creates a checkpoint inside an active transaction. It lets you roll back part of a transaction without discarding all earlier work.

```sql
SET AUTOCOMMIT FALSE;

INSERT INTO orders(order_id, customer_id)
VALUES (101, 1);

SAVEPOINT order_created;

INSERT INTO order_items(order_id, product_id)
VALUES (101, 10);

-- Suppose the next operation fails.
ROLLBACK TO SAVEPOINT order_created;

COMMIT;
```

In this example:

- The order insert remains part of the transaction.
- The insert into `order_items` is undone.
- `COMMIT` commits the remaining work.

| Command | Purpose |
| --- | --- |
| `SAVEPOINT name` | Creates a savepoint. |
| `ROLLBACK TO SAVEPOINT name` | Rolls back changes after that savepoint. |
| `RELEASE SAVEPOINT name` | Removes the savepoint. |
| `ROLLBACK` | Rolls back the entire current transaction. |
| `COMMIT` | Commits the entire current transaction. |

A savepoint is not an independent transaction. It does not commit anything by itself.

## 17. Important HSQLDB transaction syntax - revision sheet

| Requirement | HSQLDB syntax |
| --- | --- |
| Start transaction | `START TRANSACTION;` |
| Commit | `COMMIT;` |
| Rollback | `ROLLBACK;` |
| Turn autocommit on | `SET AUTOCOMMIT TRUE;` |
| Turn autocommit off | `SET AUTOCOMMIT FALSE;` |
| Next transaction read-only | `SET TRANSACTION READ ONLY;` |
| Next transaction read-write | `SET TRANSACTION READ WRITE;` |
| Next transaction isolation | `SET TRANSACTION ISOLATION LEVEL SERIALIZABLE;` |
| Create savepoint | `SAVEPOINT sp1;` |
| Roll back to savepoint | `ROLLBACK TO SAVEPOINT sp1;` |
| Release savepoint | `RELEASE SAVEPOINT sp1;` |
| Lock table for reading | `LOCK TABLE accounts READ;` |
| Lock table for writing | `LOCK TABLE accounts WRITE;` |
| Set database concurrency model | `SET DATABASE TRANSACTION CONTROL LOCKS;` |

**Remember these HSQLDB defaults:**

- Autocommit: `TRUE` for a new JDBC connection.
- Default isolation: `READ COMMITTED`.
- Default concurrency-control model: `LOCKS` (2PL).
- `READ UNCOMMITTED` is promoted to `READ COMMITTED`.
- `REPEATABLE READ` is promoted to `SERIALIZABLE` in the 2PL model.

These are defaults and documented behaviours, not universal SQL rules.

## 18. Advanced 15-question quiz

Try answering these without looking at the answer key. Each question has one correct answer unless stated otherwise.

**HSQLDB Transaction Assessment** (/15 answered)

**Suggested next topic:** Database recovery and logging - undo/redo logs, checkpoints, crash recovery, write-ahead logging, and how a DBMS restores committed and uncommitted transactions after a failure.

### User

for 2 year sql developer hsql database level give concepts needed from required topics all tricky advanced topics from these explanation and 15 question quiz at end all edge cases big data characterstics briefly explain variery volume velocity veracity value, types of no sql databases proper examples for them each where it is used applications key value store column family store document oriented database graph database why each document oriented flexible schema rich querying language, rapid application development, suitable for storing data which requires no frequent updates but read many times, graph db charactersitcs data heavily interconnected relationship no need joins graph theory ensure acid properties only this ensure acid properties, sql vs no sql felxible vs rigid schema, small vs large storage, centralized vs distributed storage vertical vs horizontal scalbility, polyglot persistence ecommerce each category where will u store, cap therem database availabllity mre imprtant then cnsistency mre important then ap: cassandra cp mngdb neo4j ca sql database no sql databases have partition tolerance compulsory, eric brewer theorem eventual consistency strong consistency how no sql ensures consisency through eventual consistency,

### ChatGPT

# Big Data and NoSQL Databases - Advanced SQL Developer Study Guide

This guide covers Big Data fundamentals, the 4 Vs, NoSQL database types, SQL vs NoSQL, real-world applications, e-commerce database architecture, CAP theorem, strong vs eventual consistency, and how NoSQL databases handle consistency.

The focus is **2-year SQL developer level**, including practical examples, interview concepts, common misconceptions and tricky edge cases.

## 1. What is Big Data?

Big Data refers to datasets whose size, speed, diversity or complexity makes traditional data-processing approaches insufficient or inefficient for a particular workload.

It is not simply data that is large in size. A dataset can be considered Big Data because it arrives extremely quickly, has many different formats, or requires complex distributed processing.

Examples:

- Social media posts, images, videos and comments.
- Banking transactions generated every second.
- IoT sensor readings from industrial machines.
- E-commerce clicks, searches, orders and customer activity.
- GPS and location data from millions of devices.

## 2. Characteristics of Big Data - The 4 Vs

**1. Volume - How much data?**

Refers to the enormous quantity of data generated and stored.

Example: An e-commerce platform storing billions of customer clicks, orders and product records.

---

**2. Velocity - How fast does data arrive and get processed?**

Refers to the speed at which data is generated, transmitted and processed.

Example: Stock-market prices, payment events and IoT sensor streams arriving continuously.

---

**3. Variety - What types of data?**

Refers to different data formats and structures.

- Structured: relational tables.
- Semi-structured: JSON, XML.
- Unstructured: images, audio, video, documents.

---

**4. Veracity - How reliable is the data?**

Refers to data quality, accuracy, completeness, consistency and trustworthiness.

Example: Duplicate customer records, inaccurate GPS readings or fake product reviews.

### Additional V: Value

**Value** refers to the useful business insights or benefits extracted from data.

Example: An e-commerce company analyzes purchase history and browsing behaviour to recommend products and improve sales.

| Characteristic | Main question | Example |
| --- | --- | --- |
| Volume | How much? | Petabytes of data |
| Velocity | How fast? | Real-time payment events |
| Variety | What formats? | JSON, images, tables |
| Veracity | How reliable? | Duplicate or inaccurate records |
| Value | What benefit? | Better recommendations |

**Interview point:** Collecting huge amounts of data does not automatically create value. Data must be processed, analyzed and converted into useful decisions.

## 3. What is NoSQL?

NoSQL commonly means **Not Only SQL**.

NoSQL databases are databases designed for data models and workloads that may not fit traditional relational-table designs particularly well.

They are often used for:

- Large-scale distributed applications.
- Flexible or evolving data structures.
- High-throughput read/write workloads.
- Data that is naturally represented as documents, key-value pairs or relationships.
- Horizontal scaling across multiple servers.

NoSQL does not mean that SQL cannot be used. Some NoSQL databases support SQL-like query languages, while others use APIs or database-specific query languages.

### Four major types of NoSQL databases

**1. Key-value store**

Stores data as a key and its associated value.

Example:

```text
user:101 → "Arun"
cart:101 → [P1, P2, P3]
session:ABC → session data
```

Typical use: Caching, shopping carts, session management and fast lookups.

---

**2. Column-family / wide-column store**

Stores data using rows and column families. Different rows can contain different columns, and the data is designed for distributed, large-scale access patterns.

Example: A customer row might contain profile columns, while another row has additional activity columns.

Typical use: Large-scale event records, time-series workloads and distributed analytical-style access patterns.

---

**3. Document-oriented database**

Stores data as documents, commonly JSON-like or BSON structures.

Example:

```json
{
  "customerId": 101,
  "name": "Arun",
  "address": {
    "city": "Chennai"
  },
  "orders": [1001, 1002]
}
```

Typical use: Product catalogs, customer profiles, content management and applications with evolving data structures.

---

**4. Graph database**

Stores data as nodes, relationships (edges) and properties.

Example:

```text
Arun ──FRIEND_OF──> Bala
Arun ──PURCHASED──> Laptop
Bala ──WORKS_AT──> Company
```

Typical use: Social networks, fraud detection, recommendation engines and network analysis.

## 4. Types of NoSQL databases - detailed concepts

### A. Key-value database

The simplest NoSQL model: each key identifies a value.

**Example data**

| Key | Value |
| --- | --- |
| `user:101` | `Arun` |
| `cart:101` | `[P101, P102]` |
| `session:ABC` | `{"user":101}` |
| `otp:101` | `482931` |

**Examples:**

- Redis
- Amazon DynamoDB
- Riak KV

**How it works**

You provide a key and retrieve the corresponding value:

```text
GET user:101
SET user:101 "Arun"
DELETE user:101
```

These are illustrative Redis-style commands.

**Applications:**

- Session storage.
- Caching frequently accessed data.
- Shopping cart storage.
- User preferences.
- OTP and temporary token storage.
- Fast lookup by a known identifier.

**Advantages**

- Very fast key-based access.
- Simple data model.
- Easy to distribute and partition.
- Suitable for high-throughput workloads.

**Limitations**

- Complex queries across arbitrary fields are generally not its strength.
- Relationships and joins are not naturally represented.
- Access patterns often need to be designed around known keys.

**Tricky interview point:** Key-value stores are not necessarily in-memory only. Redis is commonly used as an in-memory data store, while DynamoDB is a managed distributed service with persistent storage.

### B. Column-family / wide-column database

A wide-column database organizes data into rows identified by a row key and groups columns into column families.

It is different from a traditional relational database table with a fixed set of columns shared by every row.

Example:

| Row key | Profile family | Activity family |
| --- | --- | --- |
| user101 | name=Arun, city=Chennai | login=10, purchase=5 |
| user102 | name=Bala | login=20 |
| user103 | city=Mysuru | purchase=8 |

The rows can have different sets of columns.

**Examples:**

- Apache Cassandra
- Apache HBase
- Google Bigtable

**Applications:**

- IoT sensor readings.
- Time-series data.
- Large-scale event logging.
- User activity tracking.
- High-volume distributed writes.
- Data distributed across multiple data centres.

**Why use it?**

Imagine 100 million IoT devices sending sensor readings every second. A wide-column database can distribute the workload across nodes and organize records around access patterns such as device ID and timestamp.

**Important Cassandra concept:** Cassandra is query-driven. You generally design tables around the queries you need to execute. It is not designed for arbitrary relational joins.

For example:

```sql
CREATE TABLE sensor_readings (
    device_id TEXT,
    reading_time TIMESTAMP,
    temperature DOUBLE,
    PRIMARY KEY (device_id, reading_time)
);
```

This is Cassandra CQL-style syntax, not an HSQLDB SQL example.

**Tricky distinction:** Column-family storage is not the same as columnar analytical storage. Cassandra is a wide-column NoSQL database; a columnar analytical database stores data in a column-oriented layout for analytical scans.

### C. Document-oriented database

A document database stores records as self-contained documents, usually using JSON-like structures.

Example:

```json
{
  "_id": 101,
  "name": "Arun",
  "age": 25,
  "address": {
    "city": "Chennai",
    "pincode": 600001
  },
  "skills": ["Java", "SQL", "Python"],
  "orders": [
    {"orderId": 501, "amount": 2500},
    {"orderId": 502, "amount": 1500}
  ]
}
```

**Examples:**

- MongoDB
- Couchbase
- Amazon DocumentDB

**Why use a document database?**

1. **Flexible schema:** Documents in the same collection need not contain exactly the same fields.
2. **Rich querying:** Query nested fields, arrays, values and combinations of conditions.
3. **Rapid application development:** Developers can store application objects in a structure close to JSON without mapping every field to a relational table.
4. **Natural representation:** Hierarchical objects such as product descriptions, profiles and order details fit naturally.
5. **Read efficiency:** Frequently accessed related data can be embedded in one document, reducing the need for multiple queries.

#### Flexible schema example

Document 1:

```json
{
  "_id": 1,
  "name": "Arun",
  "city": "Chennai"
}
```

Document 2:

```json
{
  "_id": 2,
  "name": "Bala",
  "city": "Mysuru",
  "skills": ["Java", "SQL"],
  "experience": 2
}
```

Both documents can exist in the same collection without requiring every document to contain every field.

**Rich querying example - MongoDB:**

```javascript
db.customers.find({
    "address.city": "Chennai",
    age: { $gt: 20 }
});
```

This queries a nested field and applies a comparison condition.

#### When is a document database suitable?

- Product catalogues with different product attributes.
- Customer profiles.
- Content management systems.
- Applications whose data structure evolves frequently.
- Data that is often retrieved as a complete aggregate/document.

**Important correction:** A document database is not inherently limited to read-heavy data or data that rarely changes. MongoDB supports frequent updates, indexes and transactions. The choice depends on the workload and data model.

#### Embedding vs referencing

Embedding:

```json
{
  "orderId": 501,
  "customer": {
    "customerId": 101,
    "name": "Arun"
  }
}
```

Referencing:

```json
{
  "orderId": 501,
  "customerId": 101
}
```

| Embedding | Referencing |
| --- | --- |
| Related data stored together | Related data stored separately |
| Convenient for reading together | Useful for independently managed entities |
| Can reduce extra queries | Avoids unnecessary duplication |
| Updates to duplicated data can be difficult | Requires additional lookup when related data is needed |

**Tricky edge case:** Embedding the same customer details in thousands of orders can create duplicated data. If the customer's address changes, multiple documents may need updating. Referencing avoids that duplication but may require additional queries.

### D. Graph database

A graph database represents information using:

- **Nodes:** Entities.
- **Relationships/edges:** Connections between entities.
- **Properties:** Attributes of nodes and relationships.

Example:

**Example graph**

- Arun - FRIEND_OF → Bala
- Arun - PURCHASED → Laptop
- Bala - WORKS_AT → Company
- Laptop - BELONGS_TO → Electronics

**Examples:**

- Neo4j
- Amazon Neptune
- JanusGraph

### Graph database characteristics

1. Relationships are stored as first-class elements.
2. Traversing interconnected data is a natural operation.
3. It is useful for complex, multi-level relationship queries.
4. It can avoid the repeated join operations often needed to traverse relationships in relational models.
5. Graph databases can store properties on both nodes and relationships.

Example: Find friends of friends who purchased a particular product.

A relational database might require several joins across customer, friendship and purchase tables. A graph database can traverse the corresponding relationships.

**Cypher example (Neo4j):**

```cypher
MATCH (a:Person {name: 'Arun'})
      -[:FRIEND_OF]->
      (friend:Person)
      -[:PURCHASED]->
      (product:Product)
RETURN friend, product;
```

### Where graph databases are used

| Application | Why graph database? |
| --- | --- |
| Social networks | People and friendships |
| Fraud detection | Connected accounts, devices and transactions |
| Recommendation engines | Users, interests and products |
| Network topology | Devices and connections |
| Knowledge graphs | Concepts and semantic relationships |
| Supply chain | Suppliers, products and dependencies |

### Does a graph database guarantee ACID?

Not automatically just because it is a graph database.

For example, **Neo4j supports ACID transactions**:

- Atomicity: all operations in a transaction succeed or fail together.
- Consistency: transactions preserve database constraints and rules.
- Isolation: concurrent transactions are isolated according to the database's isolation behaviour.
- Durability: committed changes can be recovered after failure.

Neo4j documents ACID transactions and write-ahead transaction logging. Its default isolation level is READ COMMITTED.

**Exam trap:** Graph database describes the data model, whereas ACID describes transaction guarantees. These are different concepts.

## 5. SQL vs NoSQL

| Feature | SQL databases | NoSQL databases |
| --- | --- | --- |
| Data model | Relational tables | Key-value, document, wide-column, graph |
| Schema | Usually predefined schema | Often flexible or model-specific |
| Relationships | Foreign keys and joins | Embedding, references, graph edges, or application-managed relationships |
| Query language | SQL | Database-specific query language/API; some support SQL-like queries |
| Scaling | Traditionally vertical, also distributed options exist | Commonly designed for horizontal distribution |
| Storage | Often relational and centrally managed in traditional deployments | Often distributed, depending on product |
| Data structure | Tables, rows, columns | Depends on NoSQL model |
| Transactions | ACID commonly supported | Varies by product; many support ACID transactions |
| Typical use | Banking, ERP, structured records | Large distributed applications, flexible data models, graph traversal, caching |

### Important clarifications

**1. Rigid schema vs flexible schema**

SQL example:

```sql
CREATE TABLE customers (
    customer_id INT PRIMARY KEY,
    name VARCHAR(100),
    city VARCHAR(50)
);
```

Every row follows the table's defined columns and types.

Document example:

```json
{"customerId": 1, "name": "Arun"}
```

```json
{"customerId": 2, "name": "Bala", "city": "Mysuru"}
```

A document database may allow the second document to contain an additional field without changing a table definition.

However, SQL databases can also support JSON columns and evolving data. NoSQL databases may enforce schemas through validation. So, rigid vs flexible is a general tendency, not an absolute rule.

**2. Small vs large storage**

It is incorrect to say SQL is only for small data and NoSQL is only for large data.

- SQL databases can handle very large datasets.
- NoSQL databases can handle small datasets too.
- Workload, data structure, query pattern, consistency requirements and architecture determine the choice.

**3. Centralized vs distributed storage**

Traditional relational deployments often use a central database server, but modern SQL databases can be distributed or replicated.

NoSQL systems commonly use distributed architectures, but not every NoSQL database must be distributed.

**4. Vertical vs horizontal scaling**

**Vertical scaling (scale up)**

Increase resources of one server:

- More CPU
- More RAM
- Faster storage

**Horizontal scaling (scale out)**

Add more servers/nodes:

- Distribute data
- Distribute requests
- Increase cluster capacity

| Vertical scaling | Horizontal scaling |
| --- | --- |
| Upgrade one machine | Add more machines |
| Simpler architecture | More distributed-system complexity |
| Hardware limits apply | Can grow by adding nodes |
| May have a single-machine bottleneck | Requires partitioning, replication and coordination |

**Important:** SQL does not mean vertical-only and NoSQL does not mean horizontal-only. Both models can scale in either direction depending on implementation.

## 6. Polyglot persistence

Polyglot persistence means using **different database technologies within the same application**, selecting each database according to the data and workload it handles best.

Instead of forcing all application data into one database, each component uses an appropriate storage model.

### Example: E-commerce application

Imagine an e-commerce platform with millions of users.

## E-commerce architecture

**E-commerce application**

Web, mobile app and backend services

**Relational DB**

Orders, payments, inventory, users

(PostgreSQL)

**Document DB**

Product catalogue, descriptions, specifications

(MongoDB)

**Key-value DB**

Sessions, carts, cache, OTPs

(Redis)

**Graph DB**

Recommendations, customer relationships, fraud connections

(Neo4j)

**Wide-column DB**

Large-scale clickstream, product views and event history

(Apache Cassandra)

### Which database should store each category?

| E-commerce data | Suitable database | Reason |
| --- | --- | --- |
| Customer account and address | SQL | Structured data, constraints and transactions |
| Orders and order items | SQL | ACID transactions and relationships |
| Payments and financial records | SQL | Strong consistency and transactional integrity |
| Product catalogue | Document | Different products have different attributes |
| Shopping cart | Key-value | Fast access using customer/session key |
| Login sessions | Key-value | Fast temporary lookups and expiration |
| Product recommendations | Graph | Relationships among users and products |
| Fraud detection relationships | Graph | Discover interconnected accounts and devices |
| Clickstream and activity logs | Wide-column | High-volume distributed writes |
| Product image/video files | Object storage | Large binary files are better stored outside the database |

**Tricky edge cases:**

- A shopping cart can also be stored in a relational database. Redis is a design choice, not a mandatory requirement.
- A product catalogue can be stored in SQL if product attributes are sufficiently structured.
- Payment data should not be made eventually consistent if the application requires reliable payment state transitions.
- Product images are usually stored in object storage, with their URLs and metadata in a database.
- Polyglot persistence introduces synchronization, duplicate data, monitoring and operational complexity.

### How do multiple databases remain consistent?

Suppose an order is created in SQL and a recommendation event is stored in Cassandra.

These are two different databases. A normal SQL `COMMIT` cannot automatically commit both databases atomically.

Common approaches include:

- **Outbox pattern:** Save the order and an event in the same SQL transaction; publish the event asynchronously.
- **Saga pattern:** Coordinate multiple service-level transactions using compensating actions if a later step fails.
- **Eventual consistency:** Allow downstream systems to catch up asynchronously.

This is a major real-world architecture consideration.

## 7. CAP theorem - Eric Brewer's theorem

The CAP theorem is one of the most important distributed database concepts.

CAP stands for:

- **C - Consistency**
- **A - Availability**
- **P - Partition tolerance**

The theorem explains a fundamental trade-off in a distributed data system when a network partition occurs.

It is commonly associated with Eric Brewer, who introduced the conjecture; Gilbert and Lynch later formalized the result.

### C - Consistency

In CAP, consistency means that every successful read receives the latest successful write, or the system returns an error.

This is closely related to linearizability.

Example:

1. Account balance = ₹10,000.
2. User updates it to ₹8,000.
3. Update succeeds.
4. A subsequent read must return ₹8,000, not the old ₹10,000.

**Important:** CAP consistency is not the same as the C in ACID.

- CAP consistency: agreement on the latest value across a distributed system.
- ACID consistency: transactions preserve database constraints and valid states.

### A - Availability

Every request received by a non-failing node must receive a response, even if the response may not contain the latest value.

Example:

A replica is disconnected from another replica but continues responding to customer requests using its available local data.

It may return stale information.

### P - Partition tolerance

The system continues operating despite communication failures between nodes.

Example:

A distributed database has two groups of nodes:

```text
Group A                 Group B

Node 1                  Node 3
Node 2       X          Node 4
             Network partition
```

The nodes in Group A cannot communicate with Group B.

Partition tolerance means the system has a defined behaviour despite that network separation.

### What does CAP actually say?

During a network partition, a distributed system cannot guarantee both:

- Strong consistency.
- Availability for every request.

It must choose which guarantee to relax.

## CAP trade-off during a partition

**CP system**

# C + P

Consistency + Partition tolerance

May reject or delay requests that cannot be served consistently.

**AP system**

# A + P

Availability + Partition tolerance

May respond with stale or temporarily divergent data.

**CA - Consistency + Availability**

Possible when there is no network partition to tolerate. A distributed system cannot guarantee CA through an arbitrary partition.

**The most important CAP exam point:** P is not an optional feature that distributed databases can simply switch off. Network partitions are possible in distributed systems. The practical choice is how the database behaves during a partition: favour consistency or availability.

### CP system example

Imagine a railway reservation system with one remaining seat.

Two users on different sides of a network partition try to reserve it.

If both sides accept the booking independently, the same seat may be sold twice.

A CP-style system may reject or delay one request until it can safely determine the correct state.

This sacrifices availability for that operation to preserve consistency.

### AP system example

Imagine a social media application.

A user changes their profile picture. During a network partition, one replica may still show the previous picture while another shows the new picture.

The system can continue serving requests, and the replicas may converge later.

This sacrifices immediate consistency for availability.

## 8. CP, AP and CA - database examples

These classifications are useful as teaching examples, but a database's actual guarantees depend on its configuration, operation, consistency level and failure conditions.

| Database | Common teaching classification | Explanation |
| --- | --- | --- |
| Apache Cassandra | AP-oriented | Designed for high availability and partition tolerance; offers tunable consistency and stronger operations through lightweight transactions. |
| MongoDB | Often CP-oriented | Replica-set writes are coordinated through a primary; during some partitions, writes may be unavailable on nodes that cannot act as the primary. |
| Neo4j | Often CP-oriented when clustered | Cluster coordination uses consensus to maintain consistent database state. |
| Traditional standalone SQL database | CA-like in simplified examples | There is no distributed network partition between database replicas in a standalone deployment. |
| Distributed SQL database | Often CP-oriented | Distributed consensus and replication are commonly used to preserve consistency during failures. |

**Important advanced caveats:**

- Cassandra is not simply an eventually consistent database for every operation. It has tunable consistency levels and lightweight transactions with linearizable consistency.
- MongoDB is not inherently an AP database. Its replica sets elect a primary and use read/write concerns to control consistency and durability.
- Neo4j is not classified as CP merely because it is a graph database. Its clustered deployment and consensus behaviour are what matter. Neo4j also supports ACID transactions.
- SQL vs NoSQL does not determine CAP classification. Architecture and replication behaviour matter.

## 9. Strong consistency vs eventual consistency

This is a very important topic for understanding distributed NoSQL systems.

### A. Strong consistency

Strong consistency means that after a successful write, subsequent reads are guaranteed to observe that write according to the specified consistency model.

Example:

Initial stock = 5.

T1 sells 2 products.

After the write succeeds:

```text
Stock = 3
```

A subsequent read that requires strong consistency must not return the old stock value of 5.

**Suitable for:**

- Banking balances.
- Payment processing.
- Inventory reservation.
- Ticket booking.
- Financial records.

### B. Eventual consistency

Eventual consistency means that replicas may temporarily contain different values, but if no new updates occur and communication is restored, the replicas will eventually converge.

Example:

A customer changes their profile city from Chennai to Mysuru.

**Immediately after the update**

**Replica 1**

(Updated)

Mysuru

**Replica 2**

(Stale)

Chennai

Replication catches up

**Eventually both replicas**

# Mysuru

(Converged)

**Suitable for:**

- Social media likes and views.
- Product reviews.
- User activity feeds.
- Analytics dashboards.
- Recommendation data.
- Distributed content delivery.

### Strong vs eventual consistency

| Feature | Strong consistency | Eventual consistency |
| --- | --- | --- |
| Read after successful write | Reflects the write under the specified guarantee | May return an older value |
| Replica synchronization | Stronger coordination required | May synchronize asynchronously |
| Availability during partition | Some operations may be rejected or delayed | Can continue serving some requests |
| Latency | May be higher | Often lower for suitable access patterns |
| Conflict handling | Strong coordination or serialization | May require reconciliation |
| Typical use | Payments, stock reservation | Feeds, views, analytics |

**Important:** Eventual consistency does not mean data is permanently inconsistent or that updates are randomly lost. It means temporary divergence is allowed, with a convergence mechanism.

### How do NoSQL databases ensure consistency?

NoSQL databases use different strategies depending on the database.

1. **Replication:** Maintain copies of data on multiple nodes.
2. **Quorum reads/writes:** Require a specified number of replicas to acknowledge operations.
3. **Consistency levels:** Allow applications to choose stronger or weaker guarantees.
4. **Conflict resolution:** Resolve concurrent updates using timestamps, version information or application logic.
5. **Consensus protocols:** Coordinate nodes to agree on the order of important operations.
6. **Transactions:** Apply atomic changes across one or more records, where supported.

### Example: Cassandra consistency levels

Cassandra provides tunable consistency levels.

For a replication factor of 3:

| Consistency level | Meaning |
| --- | --- |
| ONE | One replica must respond. |
| TWO | Two replicas must respond. |
| THREE | All three replicas must respond. |
| QUORUM | A majority of replicas must respond. |
| ALL | All replicas must respond. |
| LOCAL_QUORUM | A majority of replicas in the local data centre must respond. |
| EACH_QUORUM | A quorum in each data centre must respond for writes. |

Example:

```sql
CONSISTENCY QUORUM;

SELECT *
FROM customer_orders
WHERE customer_id = 101;
```

This is Cassandra CQL, not HSQLDB SQL.

For a replication factor $N=3$:

$$
QUORUM = \left\lfloor\frac{N}{2}\right\rfloor+1=2
$$

Two replicas must respond.

A useful quorum condition for overlapping read/write replica sets is:

$$
R+W>N
$$

Where:

- $R$ = number of replicas required for a read.
- $W$ = number of replicas required for a write.
- $N$ = replication factor.

If $R=2$, $W=2$, $N=3$, then:

$$
2+2>3
$$

The read and write replica sets must overlap.

**Tricky edge case:** Quorum intersection alone does not guarantee linearizability. Replica freshness, conflict resolution, timestamp ordering and the database's consistency protocol also matter. Cassandra's ordinary quorum reads/writes are not identical to its lightweight transactions.

### Cassandra lightweight transactions (LWT)

Cassandra supports lightweight transactions using the Paxos protocol.

They provide compare-and-set operations with linearizable consistency.

Example:

```sql
UPDATE inventory
SET quantity = 4
WHERE product_id = 101
IF quantity = 5;
```

The update happens only if the existing quantity is 5.

This is useful for preventing conflicting updates, such as two users attempting to reserve the last product.

LWT is more expensive than ordinary writes because it requires consensus coordination.

### MongoDB consistency

MongoDB provides read concern and write concern settings.

- `readConcern: "local"` - reads data available on the selected node; it may later be rolled back.
- `readConcern: "majority"` - reads data acknowledged by a majority of replica-set members.
- `readConcern: "linearizable"` - provides a stronger real-time consistency guarantee for supported primary reads.
- `writeConcern: { w: "majority" }` - requests acknowledgement from a majority of voting members.

MongoDB can therefore provide stronger or weaker consistency guarantees depending on how reads and writes are configured.

## 10. Advanced interview and examination edge cases

| Question | Correct understanding |
| --- | --- |
| Is NoSQL always schema-less? | No. Many NoSQL databases support schema validation. |
| Is NoSQL always faster than SQL? | No. Performance depends on workload, queries and architecture. |
| Does every NoSQL database support ACID? | No. Transaction guarantees differ by product. |
| Does every graph database support ACID? | No. Neo4j does, but graph model alone does not guarantee it. |
| Is MongoDB a key-value database? | Primarily a document database, although documents are identified by keys. |
| Is Cassandra a relational database? | No. It is a distributed wide-column database. |
| Is JSON always unstructured data? | No. JSON is generally considered semi-structured. |
| Is a document database suitable for frequent updates? | Yes, depending on the document model and workload. |
| Does eventual consistency mean permanent inconsistency? | No. Replicas are expected to converge under the required conditions. |
| Does CAP mean every database can only provide two properties under all circumstances? | No. The trade-off is specifically about guarantees during network partitions. |
| Does AP mean the database never provides strong consistency? | No. It may offer stronger guarantees for particular operations or configurations. |
| Is SQL always centralized? | No. Distributed SQL databases exist. |
| Is NoSQL always horizontally scalable? | No. Horizontal distribution is common, not mandatory. |
| Does quorum automatically guarantee linearizability? | No. Quorum overlap is not sufficient by itself. |
| Can an application use SQL and NoSQL together? | Yes. This is polyglot persistence. |

## 11. Quick revision sheet

**Big Data**

- Volume = quantity
- Velocity = speed
- Variety = formats
- Veracity = reliability
- Value = usefulness

---

**NoSQL types**

- Key-value = Redis
- Wide-column = Cassandra
- Document = MongoDB
- Graph = Neo4j

---

**CAP**

- C = Consistency
- A = Availability
- P = Partition tolerance
- During a partition, cannot guarantee both strong consistency and full availability.

---

**Consistency**

- Strong = latest successful write is visible according to the guarantee.
- Eventual = replicas may temporarily differ but converge eventually.

---

**Architecture**

- Vertical scaling = scale up.
- Horizontal scaling = scale out.
- Polyglot persistence = multiple database types in one application.

## 12. Advanced 15-question quiz

These questions test conceptual understanding, practical database selection and tricky CAP/consistency scenarios. Select one answer per question.

**Big Data & NoSQL Assessment** (/15 answered)

## Reference material

For further reading, these official and foundational sources are useful:

1. Apache Cassandra - Guarantees and CAP - replication, availability, eventual consistency and lightweight transactions.
2. MongoDB - Read Concern - read consistency levels.
3. MongoDB - Causal Consistency - read/write concerns.
4. Neo4j - Transactional Behaviour - ACID and transaction isolation.
5. Gilbert and Lynch - Perspectives on the CAP Theorem - theoretical foundation of CAP.

**Recommended next topic:** Distributed databases - sharding, partition keys, replication, leader/follower architecture, consistent hashing, quorum reads/writes, and distributed transactions.

### User

for 2 year sql developer hsql database level give concepts needed from required topics all tricky advanced topics from these explanation and 15 question quiz at end all edge cases mongodb : stre data in collections, unit of storage document have dynamic schema crud performed through insert find update remove primary key predefine name _id constraints nt supported except primary key join subquery not supported, query operators comparison operator: $eq, $gte like that $and $ or and $not give insert record statement example alll fieds mutipe recrds certai fies insert withut _ autmaticay generated by database, db find exampe or and and (a or b) and (c) a,b,c cndition row filter column filter give, return a dcuments db.find() filter fields suppres _id _id:0 using $in operator $or operator, mngo db update criteria update action multi:true why adding new fieds in that row update multipe cumn all document update, replacing document, db.emp.remove remve criteria give delete all delete a document delete multiple document do only using update remove find statement no One many nthing

### ChatGPT

# MongoDB - CRUD Operations and Query Operators

This guide covers MongoDB at a **2-year SQL developer level**, focusing on collections, documents, dynamic schemas, `_id`, insert operations, `find()`, filtering, projection, comparison operators, logical operators, `update()` and `remove()`.

As requested, the practical examples will primarily use:

- `insert()` for inserting records.
- `find()` for retrieving records.
- `update()` for modifying records.
- `remove()` for deleting records.

We will avoid `updateOne()`, `updateMany()`, `deleteOne()` and `deleteMany()` in the examples.

## 1. What is MongoDB?

MongoDB is a document-oriented NoSQL database.

Unlike a relational database, which stores data in tables containing rows and columns, MongoDB stores data in:

- **Database**
- **Collections**
- **Documents**
- **Fields**

**Database: company**

**Collection: employees**

Document collection

**Collection: departments**

Document collection

**Employee document**

```json
{
  "_id": 101,
  "name": "Arun",
  "age": 25,
  "department": "IT"
}
```

### SQL vs MongoDB terminology

| SQL database | MongoDB |
| --- | --- |
| Database | Database |
| Table | Collection |
| Row | Document |
| Column | Field |
| Primary key | `_id` field |
| INSERT | `insert()` |
| SELECT | `find()` |
| UPDATE | `update()` |
| DELETE | `remove()` |

## 2. Collection and document

### Collection

A collection is a group of MongoDB documents.

SQL equivalent: Table.

```javascript
db.createCollection("employees");
```

Insertions can also create a collection automatically if it does not already exist.

### Document

A document is the basic unit of storage in MongoDB.

Documents are stored in BSON (Binary JSON), which supports additional data types beyond JSON.

Example:

```javascript
{
    "_id": 101,
    "name": "Arun",
    "age": 25,
    "salary": 50000,
    "department": "IT"
}
```

Another document in the same collection can have different fields:

```javascript
{
    "_id": 102,
    "name": "Bala",
    "city": "Chennai",
    "skills": ["Java", "SQL"]
}
```

Both documents can belong to the same collection.

### Dynamic schema

MongoDB allows documents within a collection to have different fields and field types, unless validation rules restrict them.

Example:

```javascript
db.employees.insert({
    name: "Arun",
    age: 25
});

db.employees.insert({
    name: "Bala",
    age: 26,
    salary: 50000,
    city: "Mysuru"
});
```

Both insertions are valid without first altering the collection schema.

**Important edge cases:**

- Dynamic schema does not mean there are no data-quality rules.
- MongoDB supports schema validation using JSON Schema.
- Fields can be missing from some documents.
- A field can have different BSON types in different documents unless validation prevents it.
- A missing field is different from a field whose value is `null`.

## 3. `_id` - Primary identifier

Every MongoDB document must have a unique `_id` field within its collection.

Example:

```javascript
{
    "_id": 101,
    "name": "Arun"
}
```

If you do not provide `_id`, MongoDB automatically generates an ObjectId.

```javascript
db.employees.insert({
    name: "Arun",
    age: 25
});
```

Example generated value:

```javascript
{
    "_id": ObjectId("672a12345678901234567890"),
    "name": "Arun",
    "age": 25
}
```

### Important `_id` rules

1. `_id` is mandatory for every document.
2. If omitted during insertion, MongoDB generates it automatically.
3. `_id` must be unique within that collection.
4. `_id` is indexed by default.
5. `_id` cannot be changed after insertion.
6. The `_id` field can be a string, number, ObjectId or another supported BSON value, subject to restrictions.
7. The `_id` of two documents in different collections can be identical.

**Tricky example:**

```javascript
db.employees.insert({
    _id: 101,
    name: "Arun"
});

db.employees.insert({
    _id: 101,
    name: "Bala"
});
```

The second insertion fails because `_id: 101` already exists in the same collection.

MongoDB's `_id` is conceptually similar to a primary key, but MongoDB does not require you to declare it using SQL-style `PRIMARY KEY` syntax.

## 4. INSERT - inserting documents

The legacy shell method `db.collection.insert()` accepts one document or an array of documents.

### A. Insert a single document

```javascript
db.employees.insert({
    _id: 101,
    name: "Arun",
    age: 25,
    salary: 50000,
    department: "IT"
});
```

### B. Insert multiple documents

```javascript
db.employees.insert([
    {
        _id: 102,
        name: "Bala",
        age: 26,
        salary: 45000,
        department: "HR"
    },
    {
        _id: 103,
        name: "Charan",
        age: 28,
        salary: 60000,
        department: "IT"
    },
    {
        _id: 104,
        name: "Divya",
        age: 24,
        salary: 40000,
        department: "Finance"
    }
]);
```

### C. Insert without `_id`

```javascript
db.employees.insert({
    name: "Ezhil",
    age: 27,
    salary: 55000
});
```

MongoDB automatically generates `_id`.

### D. Insert documents with different fields

```javascript
db.employees.insert([
    {
        name: "Farah",
        age: 25,
        department: "IT"
    },
    {
        name: "Gokul",
        city: "Chennai",
        skills: ["Java", "MongoDB"]
    }
]);
```

Both are valid under a collection without restrictive validation.

### E. Important INSERT edge cases

| Case | Behaviour |
| --- | --- |
| `_id` omitted | Automatically generated |
| Duplicate `_id` | Duplicate-key error |
| Same field names in different documents | Allowed |
| Different fields in documents | Allowed unless validation restricts them |
| Empty document `{}` | Can be inserted; `_id` is generated |
| Explicit `_id: null` | Does not request automatic generation; it is an explicitly supplied value |
| Multiple inserts with one duplicate | Ordered inserts stop at the error; unordered inserts can continue with other documents |

**Version note:** `insert()` is deprecated in current `mongosh`. Modern MongoDB code generally uses `insertOne()` and `insertMany()`. We are using `insert()` here to match your requested syllabus.

## 5. FIND - retrieving documents

`find()` retrieves documents from a collection.

General syntax:

```javascript
db.collection.find(
    { condition },
    { projection }
);
```

- First argument: document filter - which records to retrieve.
- Second argument: projection - which fields to display.

### A. Retrieve all documents

```javascript
db.employees.find();
```

SQL equivalent:

```sql
SELECT * FROM employees;
```

### B. Retrieve documents using one condition

```javascript
db.employees.find({
    department: "IT"
});
```

SQL equivalent:

```sql
SELECT *
FROM employees
WHERE department = 'IT';
```

### C. Retrieve using multiple conditions - implicit AND

```javascript
db.employees.find({
    department: "IT",
    age: 25
});
```

Meaning:

```text
department = IT AND age = 25
```

Both conditions must match.

### D. Explicit `$and`

```javascript
db.employees.find({
    $and: [
        { department: "IT" },
        { age: { $gte: 25 } }
    ]
});
```

SQL equivalent:

```sql
SELECT *
FROM employees
WHERE department = 'IT'
  AND age >= 25;
```

### E. `$or` - any one condition

```javascript
db.employees.find({
    $or: [
        { department: "IT" },
        { department: "HR" }
    ]
});
```

Meaning:

```text
department = IT OR department = HR
```

### F. Combination: (A OR B) AND C

This is particularly important for advanced queries.

Suppose:

- A = department is IT.
- B = department is HR.
- C = salary is greater than 45,000.

Requirement:

```text
(A OR B) AND C
```

MongoDB:

```javascript
db.employees.find({
    $and: [
        {
            $or: [
                { department: "IT" },
                { department: "HR" }
            ]
        },
        {
            salary: { $gt: 45000 }
        }
    ]
});
```

SQL equivalent:

```sql
SELECT *
FROM employees
WHERE (department = 'IT' OR department = 'HR')
  AND salary > 45000;
```

### G. Combination: A AND (B OR C)

Suppose:

- A = age greater than 25.
- B = department is IT.
- C = department is HR.

```javascript
db.employees.find({
    age: { $gt: 25 },
    $or: [
        { department: "IT" },
        { department: "HR" }
    ]
});
```

This means:

```text
A AND (B OR C)
```

### H. `$not` - negation

```javascript
db.employees.find({
    age: {
        $not: { $gt: 25 }
    }
});
```

This matches documents where `age` does not satisfy the greater-than-25 predicate. It can also match documents where the field is missing.

**Tricky point:** `$not` is a field-level operator and should be used with another operator expression. It is not a general replacement for `$nor`.

Example:

```javascript
db.employees.find({
    age: { $not: { $gte: 25 } }
});
```

This does not mean simply "age less than 25" in every case because missing fields can also match.

### Logical operator revision

| Operator | Meaning |
| --- | --- |
| `$and` | All conditions must match |
| `$or` | At least one condition must match |
| `$not` | Negates a field predicate |
| `$nor` | None of the specified conditions should match |

Examples of `$nor`:

```javascript
db.employees.find({
    $nor: [
        { department: "IT" },
        { age: { $lt: 25 } }
    ]
});
```

This excludes documents matching either condition.

MongoDB supports implicit AND when multiple fields or predicates are placed in the same filter document.

## 6. Comparison operators

MongoDB comparison operators are used inside field conditions.

| Operator | Meaning | Example |
| --- | --- | --- |
| `$eq` | Equal | `{age: {$eq: 25}}` |
| `$ne` | Not equal | `{age: {$ne: 25}}` |
| `$gt` | Greater than | `{salary: {$gt: 50000}}` |
| `$gte` | Greater than or equal | `{salary: {$gte: 50000}}` |
| `$lt` | Less than | `{age: {$lt: 30}}` |
| `$lte` | Less than or equal | `{age: {$lte: 30}}` |
| `$in` | Matches any value in an array | `{department: {$in: ["IT","HR"]}}` |
| `$nin` | Does not match values in an array | `{department: {$nin: ["IT","HR"]}}` |

### A. `$eq`

```javascript
db.employees.find({
    age: { $eq: 25 }
});
```

Shorthand:

```javascript
db.employees.find({
    age: 25
});
```

### B. `$ne`

```javascript
db.employees.find({
    department: { $ne: "IT" }
});
```

Matches documents whose department is not IT, including documents where `department` is missing.

### C. `$gt` and `$gte`

```javascript
db.employees.find({
    salary: { $gt: 50000 }
});
```

```javascript
db.employees.find({
    salary: { $gte: 50000 }
});
```

Difference:

- `$gt`: strictly greater than.
- `$gte`: greater than or equal to.

### D. `$lt` and `$lte`

```javascript
db.employees.find({
    age: { $lt: 30 }
});
```

```javascript
db.employees.find({
    age: { $lte: 30 }
});
```

### E. `$in`

Suppose you need employees from IT, HR or Finance.

```javascript
db.employees.find({
    department: {
        $in: ["IT", "HR", "Finance"]
    }
});
```

SQL equivalent:

```sql
SELECT *
FROM employees
WHERE department IN ('IT', 'HR', 'Finance');
```

### F. `$nin`

```javascript
db.employees.find({
    department: {
        $nin: ["IT", "HR"]
    }
});
```

This matches documents whose department is not IT or HR, including documents where the field is missing.

**Important:** `$in` and `$nin` can also be used with array-valued fields. `$in` matches if at least one array element matches one of the specified values.

## 7. Combining comparison and logical operators

Suppose the requirement is:

```text
age >= 25
AND
salary > 40000
AND
(department = IT OR department = HR)
```

MongoDB:

```javascript
db.employees.find({
    age: { $gte: 25 },
    salary: { $gt: 40000 },
    $or: [
        { department: "IT" },
        { department: "HR" }
    ]
});
```

Another example:

```text
salary >= 50000
AND
department NOT IN (HR, Finance)
```

```javascript
db.employees.find({
    salary: { $gte: 50000 },
    department: {
        $nin: ["HR", "Finance"]
    }
});
```

### Edge cases - comparison operators

1. Comparison operators generally compare values using BSON comparison rules and type bracketing. Do not assume `"50000"` (string) is the same as `50000` (number).
2. `$ne` and `$nin` can match documents where the field is missing.
3. `$in` with an empty array matches no documents.
4. `$nin` with an empty array matches all documents, including those missing the field.
5. If a field is an array, comparison operators can match elements inside that array.
6. `$eq: null` can match both explicit null values and missing fields. Use `$exists` when you need to distinguish them.

## 8. FIND - filtering rows and projecting columns

This is one of the most important MongoDB concepts.

MongoDB `find()` has two separate operations:

1. **Filter documents:** Which documents should be returned?
2. **Projection:** Which fields should be displayed from those documents?

Think of the SQL equivalent:

```sql
SELECT name, salary
FROM employees
WHERE department = 'IT';
```

MongoDB separates these into two arguments.

### A. Return all fields for matching documents

```javascript
db.employees.find(
    { department: "IT" }
);
```

### B. Return only selected fields

```javascript
db.employees.find(
    { department: "IT" },
    { name: 1, salary: 1 }
);
```

The result contains:

- `name`
- `salary`
- `_id` (automatically included unless excluded)

### C. Suppress `_id`

```javascript
db.employees.find(
    { department: "IT" },
    {
        name: 1,
        salary: 1,
        _id: 0
    }
);
```

Now only `name` and `salary` are returned.

### D. Exclude a field

```javascript
db.employees.find(
    { department: "IT" },
    { salary: 0 }
);
```

Returns all fields except `salary`.

### E. Include vs exclude projection

| Projection | Meaning |
| --- | --- |
| `{name: 1}` | Include name and `_id` |
| `{name: 1, salary: 1}` | Include name, salary and `_id` |
| `{name: 1, _id: 0}` | Include name, suppress `_id` |
| `{salary: 0}` | Exclude salary, return other fields |
| `{salary: 0, age: 0}` | Exclude salary and age |

**Very important edge case:** You generally cannot mix inclusion and exclusion in the same projection, except for `_id`.

Invalid:

```javascript
db.employees.find(
    {},
    {
        name: 1,
        salary: 0
    }
);
```

This produces a projection error.

Valid:

```javascript
db.employees.find(
    {},
    {
        name: 1,
        salary: 1,
        _id: 0
    }
);
```

### F. Filter documents and project nested fields

Suppose a document looks like:

```javascript
{
    name: "Arun",
    address: {
        city: "Chennai",
        pincode: 600001
    }
}
```

Retrieve only the city:

```javascript
db.employees.find(
    { name: "Arun" },
    {
        "address.city": 1,
        _id: 0
    }
);
```

MongoDB uses dot notation to access nested fields.

**Remember:** Filter conditions select documents; projection controls fields in the returned documents. They are not the same operation.

## 9. UPDATE - modifying existing documents

The legacy `update()` method modifies one or more matching documents.

Syntax:

```javascript
db.collection.update(
    <criteria>,
    <update document>,
    <options>
);
```

The three parameters are:

| Parameter | Purpose |
| --- | --- |
| Criteria | Selects which documents to update |
| Update document | Specifies the modification |
| Options | Controls multi-update, upsert and other behaviour |

By default, `update()` modifies **only one matching document**.

To modify all matching documents, specify:

```javascript
{ multi: true }
```

### A. Update one matching document using `$set`

```javascript
db.employees.update(
    { _id: 101 },
    {
        $set: {
            salary: 60000
        }
    }
);
```

Only the `salary` field is changed. Other fields remain unchanged.

### B. Update multiple fields in the same document

```javascript
db.employees.update(
    { _id: 101 },
    {
        $set: {
            salary: 65000,
            department: "Finance",
            city: "Chennai"
        }
    }
);
```

All three fields are modified in the matching document.

### C. Add a new field to an existing document

Suppose the existing document is:

```javascript
{
    _id: 101,
    name: "Arun",
    age: 25
}
```

Execute:

```javascript
db.employees.update(
    { _id: 101 },
    {
        $set: {
            skills: ["Java", "SQL"],
            experience: 2
        }
    }
);
```

Result:

```javascript
{
    _id: 101,
    name: "Arun",
    age: 25,
    skills: ["Java", "SQL"],
    experience: 2
}
```

**Why does the new field get added?**

Because `$set` creates the field if it does not exist and changes its value if it already exists.

This is one of the advantages of a flexible document model.

### D. Update multiple documents using `multi: true`

Suppose you want to increase the salary of every IT employee.

```javascript
db.employees.update(
    { department: "IT" },
    {
        $set: {
            salary: 70000
        }
    },
    {
        multi: true
    }
);
```

All documents matching `department: "IT"` receive the new salary.

### E. Update multiple fields across multiple documents

```javascript
db.employees.update(
    { department: "IT" },
    {
        $set: {
            location: "Chennai",
            status: "Active",
            company: "ABC"
        }
    },
    {
        multi: true
    }
);
```

This operation:

1. Finds every document where department is IT.
2. Adds or updates `location`.
3. Adds or updates `status`.
4. Adds or updates `company`.
5. Preserves all other existing fields.

This is the correct way to understand `multi: true`: it controls **how many documents** are updated, not how many fields are updated.

### F. `$inc` - increment or decrement

Increase salary by 5,000:

```javascript
db.employees.update(
    { _id: 101 },
    {
        $inc: {
            salary: 5000
        }
    }
);
```

Decrease salary by 2,000:

```javascript
db.employees.update(
    { _id: 101 },
    {
        $inc: {
            salary: -2000
        }
    }
);
```

If the numeric field does not exist, `$inc` creates it with the specified value.

If the existing field is not numeric, the operation produces an error.

### G. `$unset` - remove a field from a document

```javascript
db.employees.update(
    { _id: 101 },
    {
        $unset: {
            city: ""
        }
    }
);
```

The `city` field is removed from the document. It is not merely assigned `null`.

### H. `$rename` - rename a field

```javascript
db.employees.update(
    { _id: 101 },
    {
        $rename: {
            department: "dept"
        }
    }
);
```

The field `department` becomes `dept`.

### I. `$push` - add an element to an array

```javascript
db.employees.update(
    { _id: 101 },
    {
        $push: {
            skills: "MongoDB"
        }
    }
);
```

Adds `"MongoDB"` to the `skills` array. It can add a duplicate value.

### J. `$addToSet` - add only if not already present

```javascript
db.employees.update(
    { _id: 101 },
    {
        $addToSet: {
            skills: "Java"
        }
    }
);
```

If `"Java"` already exists in the array, it is not added again.

### K. `$pull` - remove matching array elements

```javascript
db.employees.update(
    { _id: 101 },
    {
        $pull: {
            skills: "Java"
        }
    }
);
```

Removes all matching `"Java"` elements from the array.

### Update operator revision

| Operator | Purpose |
| --- | --- |
| `$set` | Add or modify fields |
| `$unset` | Remove fields |
| `$inc` | Increment/decrement numeric fields |
| `$mul` | Multiply numeric fields |
| `$rename` | Rename a field |
| `$min` | Set field only if the new value is smaller |
| `$max` | Set field only if the new value is larger |
| `$push` | Append to an array |
| `$addToSet` | Append only if value is not already present |
| `$pull` | Remove matching array elements |
| `$pop` | Remove first or last array element |

### L. Replacement update - very important

There are two different ways to update a MongoDB document:

1. Operator update using `$set`, `$inc`, etc.
2. Replacement update using a document containing ordinary field-value pairs.

Existing document:

```javascript
{
    _id: 101,
    name: "Arun",
    age: 25,
    salary: 50000,
    department: "IT"
}
```

Execute:

```javascript
db.employees.update(
    { _id: 101 },
    {
        name: "Arun Kumar",
        age: 26
    }
);
```

The result is:

```javascript
{
    _id: 101,
    name: "Arun Kumar",
    age: 26
}
```

Notice what happened:

- `salary` disappeared.
- `department` disappeared.
- `name` changed.
- `age` changed.
- `_id` was preserved.

**Why?** Because this is a replacement operation, not a partial field update.

To preserve other fields, use `$set`.

### M. `multi: true` vs replacement

This is a common advanced exam question.

```javascript
db.employees.update(
    { department: "IT" },
    {
        name: "Updated"
    },
    {
        multi: true
    }
);
```

This is not a valid multi-document replacement operation.

MongoDB does not allow `multi: true` with a replacement document. Multi-update requires update operators or an allowed update pipeline.

### N. `upsert: true`

Upsert means **update if found, insert if not found**.

```javascript
db.employees.update(
    { employee_code: 501 },
    {
        $set: {
            name: "Karthik",
            department: "IT"
        }
    },
    {
        upsert: true
    }
);
```

- If a matching document exists, it is updated.
- If no matching document exists, a new document is inserted.
- If the new document has no `_id`, MongoDB generates one.

### UPDATE edge cases to remember

| Situation | Result |
| --- | --- |
| No document matches | No change by default |
| No document matches with `upsert: true` | New document is inserted |
| Multiple documents match, no `multi: true` | Only one matching document is updated |
| Multiple documents match with `multi: true` | All matching documents are updated |
| `$set` on a missing field | Creates the field |
| `$unset` on missing field | No meaningful change |
| `$inc` on missing field | Creates numeric field |
| `$inc` on string field | Error |
| Replacement document | Removes fields not included in replacement |
| Attempt to change `_id` | Error |
| `$push` on missing array field | Creates array and appends |
| `$push` on non-array existing field | Error |
| `$addToSet` | Prevents adding an equal existing array value |

**Important:** Multi-update is not an all-or-nothing multi-document transaction. If an error occurs while updating multiple documents, some earlier documents may already have been updated. Also, MongoDB documents that `multi: true` should be used for idempotent operations.

## 10. REMOVE - deleting documents

`remove()` deletes documents matching a specified condition.

Syntax:

```javascript
db.collection.remove(
    <criteria>,
    <justOne>
);
```

The second argument controls whether to remove just one matching document.

### A. Delete a specific document

```javascript
db.employees.remove(
    { _id: 101 },
    true
);
```

Deletes one matching document.

### B. Delete multiple documents matching a condition

```javascript
db.employees.remove(
    { department: "IT" }
);
```

By default, `remove()` deletes **all matching documents**.

### C. Delete all documents in a collection

```javascript
db.employees.remove({});
```

An empty filter `{}` matches every document.

This deletes all documents but leaves the collection itself in place.

### D. Delete documents based on comparison operators

Delete employees whose salary is below 20,000:

```javascript
db.employees.remove({
    salary: { $lt: 20000 }
});
```

Delete employees whose department is IT or HR:

```javascript
db.employees.remove({
    department: {
        $in: ["IT", "HR"]
    }
});
```

### E. Delete one matching document

```javascript
db.employees.remove(
    { department: "IT" },
    true
);
```

If multiple documents match, only one is removed. Do not assume which matching document will be removed unless the operation specifies an appropriate selection order through a supported mechanism.

### F. Remove comparison

| Query | Behaviour |
| --- | --- |
| `remove({})` | Deletes all documents |
| `remove({age: 25})` | Deletes all matching documents |
| `remove({age: 25}, true)` | Deletes one matching document |
| `remove({salary: {$gt: 50000}})` | Deletes all documents with salary above 50,000 |
| `remove({department: "IT"})` | Deletes all IT department documents |

### G. Important REMOVE edge cases

- `remove({})` does not drop the collection.
- `remove({})` does not remove the collection's indexes.
- `remove()` without `justOne: true` removes all matching documents.
- `remove(criteria, true)` deletes only one matching document.
- If no document matches, nothing is deleted.
- Removing a document does not automatically delete related documents from another collection.
- If a document has an array field, the filter can match documents based on array elements.
- MongoDB does not automatically cascade deletes across collections like a relational foreign key with `ON DELETE CASCADE`.

**Difference between removing documents and dropping a collection:**

| Remove all documents | Drop collection |
| --- | --- |
| `db.employees.remove({})` | `db.employees.drop()` |
| Deletes documents | Deletes collection |
| Collection remains | Collection is removed |
| Indexes remain | Collection indexes are removed |

`remove()` is deprecated in current `mongosh`, but the legacy method supports the `justOne` argument as explained above.

## 11. Does MongoDB support JOINs and subqueries?

You mentioned that joins and subqueries are not supported. This needs an important correction.

MongoDB does not use traditional SQL `JOIN` syntax in its ordinary `find()` method. However, MongoDB **does support joins and correlated/uncorrelated subqueries** through aggregation, especially using `$lookup`.

Example collections:

`employees`:

```javascript
{
    _id: 101,
    name: "Arun",
    dept_id: 10
}
```

`departments`:

```javascript
{
    _id: 10,
    dept_name: "IT"
}
```

MongoDB join using `$lookup`:

```javascript
db.employees.aggregate([
    {
        $lookup: {
            from: "departments",
            localField: "dept_id",
            foreignField: "_id",
            as: "department_details"
        }
    }
]);
```

The result includes a `department_details` array containing matching department documents.

**For your CRUD syllabus:** You can focus on `insert()`, `find()`, `update()` and `remove()` without studying `$lookup` in depth yet. But do not write in an interview that MongoDB cannot perform joins or subqueries.

## 12. Complete MongoDB CRUD revision table

| Operation | Legacy syntax | Purpose |
| --- | --- | --- |
| Create | `db.emp.insert({...})` | Insert document |
| Read | `db.emp.find({...})` | Retrieve matching documents |
| Update one | `db.emp.update(filter, update)` | Modify one matching document |
| Update multiple | `db.emp.update(filter, update, {multi:true})` | Modify all matching documents |
| Delete one | `db.emp.remove(filter, true)` | Delete one matching document |
| Delete multiple | `db.emp.remove(filter)` | Delete all matching documents |
| Delete all | `db.emp.remove({})` | Delete every document |

**Version warning:** The four legacy methods you requested-`insert()`, `update()` and `remove()`-are deprecated in current `mongosh`; `find()` remains supported. They are useful to learn for legacy MongoDB shell questions, but for new application code use the current insert/update/delete methods.

## 13. Advanced edge cases - final revision

These are particularly important for output-prediction questions and practical assessments.

| Question | Correct answer |
| --- | --- |
| Can two documents in one collection have the same `_id`? | No. |
| Can two collections have the same `_id` value? | Yes. |
| What happens if `_id` is omitted? | MongoDB generates an ObjectId by default. |
| Does `$set` delete other fields? | No. |
| Does replacement update delete unspecified fields? | Yes. |
| Does `multi: true` update all matching documents? | Yes, when using a valid operator update. |
| What is the default `multi` value? | `false`. |
| Does `remove({})` remove the collection? | No, only its documents. |
| Does `remove({})` delete indexes? | No. |
| Does projection `{name: 1}` include `_id`? | Yes, by default. |
| Does `{name: 1, _id: 0}` suppress `_id`? | Yes. |
| Can inclusion and exclusion be mixed in projection? | Not generally, except for `_id`. |
| Does `$ne` match documents with a missing field? | Yes. |
| Does `$nin` match documents with a missing field? | Yes. |
| Does `$push` prevent duplicate values? | No. Use `$addToSet` for that. |
| Does `$unset` set a field to null? | No, it removes the field. |
| Does `update()` automatically insert if no record matches? | Only with `upsert: true`. |
| Can a replacement update use `multi: true`? | No. |
| Does MongoDB support joins? | Yes, using `$lookup` in aggregation. |
| Does MongoDB support schema validation? | Yes. |

## 14. Advanced 15-question MongoDB quiz

The questions cover CRUD syntax, logical operators, projections, updates, replacement, deletion and tricky edge cases.

**MongoDB CRUD - Advanced Assessment** (/15 answered)

**Recommended next topic:** MongoDB advanced querying - arrays, embedded documents, `$exists`, `$type`, `$regex`, `$elemMatch`, sorting, limiting, indexes and aggregation pipeline.
