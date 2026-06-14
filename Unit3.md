Unit III: Introduction to SQL – Complete Notes
3.1 Overview of SQL Query Language
What is SQL?

SQL (Structured Query Language) is the standard language used to communicate with relational databases. It is used to create, manage, retrieve, and manipulate data.

Why SQL is Important
Easy to learn
Standard database language
Works with most DBMSs
Efficient data retrieval
Supports security and transactions
SQL Categories
Category	Purpose
DDL	Define database structure
DML	Manipulate data
DQL	Retrieve data
DCL	Control permissions
TCL	Manage transactions
3.2 SQL Data Definition

Data Definition Language (DDL) is used to define database structures.

CREATE

Used to create databases and tables.

Create Table
CREATE TABLE Student (
    StudentID INT,
    Name VARCHAR(50),
    Age INT
);
ALTER

Used to modify an existing table.

Add Column
ALTER TABLE Student
ADD Department VARCHAR(20);
Modify Column
ALTER TABLE Student
MODIFY Age SMALLINT;
DROP

Used to permanently remove a table.

DROP TABLE Student;
TRUNCATE

Removes all rows but keeps the table structure.

TRUNCATE TABLE Student;
3.3 Basic Structure of SQL Queries

The most common SQL command is SELECT.

General Structure
SELECT column_name
FROM table_name
WHERE condition;
Example
SELECT Name
FROM Student;
SELECT *

Retrieves all columns.

SELECT *
FROM Student;
WHERE Clause

Filters records.

SELECT *
FROM Student
WHERE Age > 20;
Comparison Operators
Operator	Meaning
=	Equal
!= or <>	Not Equal
>	Greater Than
<	Less Than
>=	Greater Than or Equal
<=	Less Than or Equal

Example:

SELECT *
FROM Student
WHERE Age >= 18;
3.4 Additional Basic Operations
DISTINCT

Removes duplicate values.

Example
SELECT DISTINCT Department
FROM Student;
ORDER BY

Sorts data.

Ascending Order
SELECT *
FROM Student
ORDER BY Name ASC;
Descending Order
SELECT *
FROM Student
ORDER BY Name DESC;
AND Operator

All conditions must be true.

SELECT *
FROM Student
WHERE Age > 18
AND Department = 'IT';
OR Operator

At least one condition must be true.

SELECT *
FROM Student
WHERE Department='IT'
OR Department='CSE';
BETWEEN

Checks a range of values.

SELECT *
FROM Student
WHERE Age BETWEEN 18 AND 25;
LIKE

Pattern matching.

Starts with S
SELECT *
FROM Student
WHERE Name LIKE 'S%';
Ends with a
SELECT *
FROM Student
WHERE Name LIKE '%a';
3.5 Set Operations

Set operations combine results from multiple queries.

UNION

Combines results and removes duplicates.

SELECT Name FROM Student
UNION
SELECT Name FROM Teacher;
Example

Student:

Sonam
Karma

Teacher:

Karma
Pema

Result:

Sonam
Karma
Pema
UNION ALL

Combines results including duplicates.

SELECT Name FROM Student
UNION ALL
SELECT Name FROM Teacher;
INTERSECT

Returns common records.

SELECT Name FROM Student
INTERSECT
SELECT Name FROM Teacher;

Result:

Karma
EXCEPT (MINUS)

Returns records from first query not found in second query.

SELECT Name FROM Student
EXCEPT
SELECT Name FROM Teacher;

Result:

Sonam
3.6 Null Values
What is NULL?

NULL means:

Unknown value
Missing value
Not applicable value

NULL is not:

Zero (0)
Empty string (' ')
Checking NULL
IS NULL
SELECT *
FROM Student
WHERE Phone IS NULL;
IS NOT NULL
SELECT *
FROM Student
WHERE Phone IS NOT NULL;
Problems with NULL

Suppose:

Age = NULL

Then:

Age = 20

is neither TRUE nor FALSE.

Result = UNKNOWN

3.7 Aggregate Functions

Aggregate functions perform calculations on multiple rows.

COUNT()

Counts records.

SELECT COUNT(*)
FROM Student;
SUM()

Calculates total.

SELECT SUM(Salary)
FROM Employee;
AVG()

Calculates average.

SELECT AVG(Marks)
FROM Student;
MAX()

Returns largest value.

SELECT MAX(Salary)
FROM Employee;
MIN()

Returns smallest value.

SELECT MIN(Salary)
FROM Employee;
GROUP BY

Groups rows with similar values.

Example
SELECT Department,
COUNT(*)
FROM Student
GROUP BY Department;

Result:

Department	Count
IT	20
CSE	15
HAVING

Filters grouped data.

SELECT Department,
COUNT(*)
FROM Student
GROUP BY Department
HAVING COUNT(*) > 10;
3.8 Nested Subqueries

A query inside another query is called a subquery.

Single-Row Subquery
Example

Find students whose marks are above average.

SELECT Name
FROM Student
WHERE Marks >
(
SELECT AVG(Marks)
FROM Student
);
Multi-Row Subquery
Example
SELECT Name
FROM Student
WHERE DepartmentID IN
(
SELECT DepartmentID
FROM Department
WHERE Location='Thimphu'
);
EXISTS

Checks whether subquery returns rows.

SELECT Name
FROM Student S
WHERE EXISTS
(
SELECT *
FROM Enrollment E
WHERE S.StudentID=E.StudentID
);
NOT EXISTS

Returns records when no match exists.

SELECT Name
FROM Student S
WHERE NOT EXISTS
(
SELECT *
FROM Enrollment E
WHERE S.StudentID=E.StudentID
);
3.9 Modification of the Database

Modification means changing database contents.

INSERT

Adds new records.

Example
INSERT INTO Student
VALUES (101,'Sonam',20);
Insert Specific Columns
INSERT INTO Student
(StudentID,Name)
VALUES
(102,'Karma');
UPDATE

Modifies existing records.

Example
UPDATE Student
SET Age=21
WHERE StudentID=101;
Update Multiple Columns
UPDATE Student
SET Age=21,
Department='IT'
WHERE StudentID=101;
DELETE

Removes records.

Example
DELETE FROM Student
WHERE StudentID=101;
Delete All Records
DELETE FROM Student;

(Table remains but rows are removed.)