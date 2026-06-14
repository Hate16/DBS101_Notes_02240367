Unit IV: Intermediate and Advanced SQL – Complete Notes
4.1 Join Expressions

A JOIN combines rows from two or more tables based on a related column.

Example Tables

Student

StudentID	Name	DeptID
101	Sonam	D1
102	Karma	D2

Department

DeptID	DeptName
D1	IT
D2	CSE
1. Inner Join

Returns only matching records.

SELECT Student.Name, Department.DeptName
FROM Student
INNER JOIN Department
ON Student.DeptID = Department.DeptID;

Result:

Name	DeptName
Sonam	IT
Karma	CSE
2. Left Join

Returns all records from the left table and matching records from the right table.

SELECT *
FROM Student
LEFT JOIN Department
ON Student.DeptID = Department.DeptID;
3. Right Join

Returns all records from the right table and matching records from the left table.

SELECT *
FROM Student
RIGHT JOIN Department
ON Student.DeptID = Department.DeptID;
4. Full Outer Join

Returns all records from both tables.

SELECT *
FROM Student
FULL OUTER JOIN Department
ON Student.DeptID = Department.DeptID;
5. Self Join

A table joins itself.

SELECT E1.Name, E2.Name
FROM Employee E1, Employee E2
WHERE E1.ManagerID = E2.EmployeeID;
4.2 Views

A view is a virtual table created from a query.

Advantages
Improves security
Simplifies complex queries
Hides unnecessary data
Creating a View
CREATE VIEW Student_View AS
SELECT StudentID, Name
FROM Student;
Using a View
SELECT * FROM Student_View;
Dropping a View
DROP VIEW Student_View;
4.3 Transactions

A transaction is a sequence of operations performed as a single logical unit.

Example

Money Transfer:

Withdraw 1000 from A
Deposit 1000 into B

Both operations must succeed together.

Transaction Commands
BEGIN TRANSACTION
BEGIN TRANSACTION;
COMMIT

Permanently saves changes.

COMMIT;
ROLLBACK

Cancels changes.

ROLLBACK;
ACID Properties
Atomicity

All operations succeed or none succeed.

Consistency

Database remains valid.

Isolation

Transactions do not interfere.

Durability

Committed data remains permanent.

4.4 Integrity Constraints

Constraints enforce correctness of data.

NOT NULL

Column cannot contain NULL values.

Name VARCHAR(50) NOT NULL
UNIQUE

Prevents duplicate values.

Email VARCHAR(100) UNIQUE
PRIMARY KEY

Uniquely identifies records.

StudentID INT PRIMARY KEY
FOREIGN KEY

References another table's primary key.

FOREIGN KEY(DeptID)
REFERENCES Department(DeptID)
CHECK

Limits acceptable values.

CHECK (Age >= 18)
DEFAULT

Provides a default value.

Status VARCHAR(10)
DEFAULT 'Active'
4.5 SQL Data Types and Schemas
SQL Data Types
Numeric Types
Type	Description
INT	Integer
SMALLINT	Small Integer
DECIMAL	Fixed Decimal
FLOAT	Floating Point
Character Types
Type	Description
CHAR(n)	Fixed Length
VARCHAR(n)	Variable Length

Example:

Name VARCHAR(50)
Date and Time Types
Type	Description
DATE	Date
TIME	Time
TIMESTAMP	Date and Time

Example:

DOB DATE
Schema

A schema is a collection of database objects.

Create Schema
CREATE SCHEMA University;
4.6 Index Definition in SQL

An index improves data retrieval speed.

Without Index

Database scans entire table.

With Index

Database directly finds records.

Create Index
CREATE INDEX idx_name
ON Student(Name);
Create Unique Index
CREATE UNIQUE INDEX idx_email
ON Student(Email);
Drop Index
DROP INDEX idx_name;
Advantages
Faster searching
Faster sorting
Disadvantages
Requires extra storage
Slower insert/update operations
4.7 Authorization

Authorization controls user access to database resources.

GRANT

Gives privileges.

GRANT SELECT
ON Student
TO User1;
REVOKE

Removes privileges.

REVOKE SELECT
ON Student
FROM User1;
Common Privileges
Privilege	Description
SELECT	Read data
INSERT	Add data
UPDATE	Modify data
DELETE	Remove data
ALL	All permissions
4.8 Accessing SQL from a Programming Language

Applications often communicate with databases using programming languages.

Why?
Execute SQL commands
Retrieve data
Update records
General Process
Program
   ↓
SQL Driver
   ↓
Database
Example (Python)
import sqlite3

conn = sqlite3.connect("student.db")

cursor = conn.cursor()

cursor.execute(
"SELECT * FROM Student"
)

rows = cursor.fetchall()
Example (Java JDBC)
Connection con =
DriverManager.getConnection(
"url","user","password");
4.9 Functions and Stored Procedures
Functions

A function returns a value.

Example
CREATE FUNCTION GetBonus
(@salary INT)
RETURNS INT
AS
BEGIN
RETURN @salary * 10/100
END
Call Function
SELECT GetBonus(50000);
Stored Procedures

A stored procedure is a saved SQL program.

Advantages
Reusable
Faster execution
Better security
Example
CREATE PROCEDURE ShowStudents
AS
BEGIN
SELECT * FROM Student
END
Execute Procedure
EXEC ShowStudents;
4.10 Triggers

A trigger is a procedure that automatically executes when an event occurs.

Events
INSERT
UPDATE
DELETE
Example
CREATE TRIGGER Student_Audit
AFTER INSERT
ON Student
FOR EACH ROW
BEGIN
INSERT INTO AuditLog
VALUES ('Record Added');
END;
Uses
Logging changes
Security monitoring
Enforcing business rules
4.11 Recursive Queries

A recursive query refers to itself and is useful for hierarchical data.

Example

Employee Table

EmployeeID	ManagerID
1	NULL
2	1
3	2
Recursive SQL
WITH RECURSIVE EmployeeTree AS
(
SELECT EmployeeID, ManagerID
FROM Employee
WHERE ManagerID IS NULL

UNION ALL

SELECT E.EmployeeID,
       E.ManagerID
FROM Employee E
JOIN EmployeeTree ET
ON E.ManagerID =
ET.EmployeeID
)

SELECT *
FROM EmployeeTree;
Uses
Organizational charts
Family trees
Folder structures
Network paths
4.12 Advanced Aggregation Features

Advanced aggregation performs complex summary operations.

GROUP BY

Groups similar rows.

SELECT Department,
COUNT(*)
FROM Student
GROUP BY Department;
HAVING

Filters grouped records.

SELECT Department,
COUNT(*)
FROM Student
GROUP BY Department
HAVING COUNT(*) > 5;
ROLLUP

Produces subtotals and grand totals.

SELECT Department,
SUM(Salary)
FROM Employee
GROUP BY ROLLUP(Department);

Example Output:

Department	Salary
IT	50000
CSE	40000
NULL	90000

(NULL represents grand total.)

CUBE

Generates all possible subtotal combinations.

SELECT Department,
Gender,
COUNT(*)
FROM Employee
GROUP BY CUBE(
Department,
Gender
);
GROUPING SETS

Allows multiple GROUP BY operations in one query.

SELECT Department,
Gender,
COUNT(*)
FROM Employee
GROUP BY GROUPING SETS
(
(Department),
(Gender),
()
);
Quick Revision
Types of Joins
INNER JOIN
LEFT JOIN
RIGHT JOIN
FULL OUTER JOIN
SELF JOIN
Transaction Commands
BEGIN TRANSACTION
COMMIT
ROLLBACK
Integrity Constraints
NOT NULL
UNIQUE
PRIMARY KEY
FOREIGN KEY
CHECK
DEFAULT
Authorization Commands
GRANT
REVOKE
Database Objects
View
Index
Function
Stored Procedure
Trigger
Advanced Aggregation
GROUP BY
HAVING
ROLLUP
CUBE
GROUPING SETS