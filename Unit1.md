Unit I: Introduction to Database Systems – Complete Notes
1.1 View of Data

A database is an organized collection of related data stored electronically for easy access, management, and updating.

Levels of Data Abstraction

Database systems hide complex details from users through three levels:

1. Physical Level
Lowest level of abstraction.
Describes how data is stored on storage devices.
Includes files, indexes, and storage structures.

Example: Customer records stored in disk blocks.

2. Logical Level
Describes what data is stored and relationships among data.
Used by database administrators.

Example: Student(ID, Name, Department).

3. View Level
Highest level of abstraction.
Shows only relevant data to specific users.

Example: A student sees only his/her own grades.

Data Independence

The ability to modify the schema without affecting application programs.

Physical Data Independence: Changes in storage do not affect logical schema.
Logical Data Independence: Changes in logical schema do not affect user views.
1.2 Purpose of Database Systems

Database systems were developed to overcome problems of traditional file-processing systems.

Problems with File Systems
Data Redundancy
Same data stored multiple times.
Wastes storage space.
Data Inconsistency
Different copies of the same data may contain different values.
Difficulty in Accessing Data
New programs required for new queries.
Data Isolation
Data scattered in different files.
Integrity Problems
Difficult to enforce constraints.
Security Problems
Difficult to restrict access.
Concurrent Access Problems
Multiple users may update data simultaneously.
Advantages of DBMS
Reduced redundancy
Improved consistency
Better security
Data sharing
Backup and recovery
Efficient data access
1.3 History of Database Systems
1. Early File Systems (1950s–1960s)
Data stored in separate files.
No centralized management.
2. Hierarchical Databases (1960s)
Data organized in a tree structure.
Parent-child relationship.

Example:

Company
 ├── Department
      ├── Employee
3. Network Databases (1970s)
Data organized as a graph.
Supports many-to-many relationships.
4. Relational Databases (1970s–Present)

Introduced by:
Edgar F. Codd

Data stored in tables.
Uses SQL.
Most widely used model.
5. Object-Oriented Databases (1980s)
Store objects directly.
Integrates database and object-oriented programming.
6. NoSQL Databases (2000s–Present)
Designed for big data and scalability.
Types:
Document databases
Key-value stores
Graph databases
Column-family databases
1.4 Database-System Applications

Databases are used in many areas.

Banking
Customer accounts
Transactions
Loans
Education
Student records
Attendance
Examination results
Healthcare
Patient records
Appointments
Medical history
E-Commerce
Products
Orders
Payments
Telecommunications
Call records
Billing systems
Social Media
User profiles
Posts
Messages
Government
Census data
Tax systems
Citizen records
1.5 Database Languages

Database languages are used to define, manipulate, and control data.

1. Data Definition Language (DDL)

Used to define database structure.

Commands:

CREATE
ALTER
DROP
TRUNCATE

Example:

CREATE TABLE Student(
ID INT,
Name VARCHAR(50)
);
2. Data Manipulation Language (DML)

Used to manipulate data.

Commands:

INSERT
UPDATE
DELETE

Example:

INSERT INTO Student VALUES(1,'Sonam');
3. Data Query Language (DQL)

Used to retrieve data.

Command:

SELECT * FROM Student;
4. Data Control Language (DCL)

Used to control access permissions.

Commands:

GRANT
REVOKE

Example:

GRANT SELECT ON Student TO User1;
5. Transaction Control Language (TCL)

Used to manage transactions.

Commands:

COMMIT
ROLLBACK
SAVEPOINT

Example:

COMMIT;
1.6 Database Design

Database design is the process of creating a database structure that stores data efficiently.

Steps in Database Design
1. Requirement Analysis
Identify user requirements.
Determine data needs.
2. Conceptual Design
Create Entity Relationship (ER) model.

Example:

Student ---- Enrolls ---- Course
3. Logical Design
Convert ER model into relational tables.
4. Physical Design
Decide storage methods and indexes.
5. Implementation
Create tables and constraints.
Goals of Good Database Design
Minimize redundancy
Improve consistency
Ensure integrity
Improve performance
1.7 Database Engine

A database engine is the core software component that stores, retrieves, and manages data.

Functions
Data Storage
Data Retrieval
Transaction Management
Concurrency Control
Security Enforcement
Backup and Recovery
Components
Storage Manager
Handles storage operations.
Query Processor
Processes SQL queries.
Transaction Manager
Maintains ACID properties.
Examples
MySQL
PostgreSQL
Oracle Database
Microsoft SQL Server
1.8 Database and Application Architecture

Architecture describes how database components interact.

1-Tier Architecture
Database and application on the same system.
Used for local applications.
User
  ↓
Database
Advantages
Simple
Fast
Disadvantages
Limited scalability
2-Tier Architecture

Client communicates directly with database server.

Client ↔ Database Server
Example

Desktop application connected to MySQL.

Advantages
Better than 1-tier.
Disadvantages
Security concerns.
3-Tier Architecture

Most common architecture.

Client
   ↓
Application Server
   ↓
Database Server
Advantages
Better security
Scalability
Easier maintenance
Example

Web applications

1.9 Database Users and Administrators

Different people interact with databases in different ways.

1. Database Administrator (DBA)

Responsible for overall database management.

Responsibilities
Database installation
User management
Security
Backup and recovery
Performance tuning
2. Database Designers
Design database schema.
Define relationships and constraints.
3. Application Programmers
Develop applications that interact with databases.
Write SQL queries and programs.
4. End Users

People who use the database system.

Types of End Users
a) Naive Users
Use predefined applications.
Example: ATM users.
b) Casual Users
Access occasionally.
Example: Managers.
c) Sophisticated Users
Use advanced queries.
Example: Analysts.
d) Specialized Users
Develop special database applications.