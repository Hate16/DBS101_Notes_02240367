Unit II: Database Design – Complete Notes
2.1 Overview of the Design Process

Database design is the process of creating a database structure that accurately stores and manages data.

Objectives of Database Design
Minimize data redundancy
Ensure data consistency
Improve efficiency
Maintain data integrity
Support future growth
Steps in Database Design
1. Requirements Collection and Analysis
Gather information about user needs.
Identify data to be stored.
2. Conceptual Design
Create an Entity-Relationship (ER) model.
Identify entities, attributes, and relationships.
3. Logical Design
Convert ER model into relational tables.
Define primary and foreign keys.
4. Physical Design
Decide storage structures and indexes.
5. Implementation
Create database using SQL.
6. Testing and Maintenance
Verify correctness and update when necessary.
2.2 Relational Modeling

Relational modeling organizes data into tables (relations).

Basic Components
Relation (Table)

Example:

StudentID	Name	Department
101	Sonam	IT
102	Karma	CSE
Tuple (Row)

A single record in a table.

Attribute (Column)

A property of an entity.

Domain

Set of valid values for an attribute.

Example:

Age → 0–120
Gender → Male, Female
Advantages
Simple structure
Easy querying
Data independence
2.3 The Entity-Relationship (ER) Model

The ER model is a conceptual design tool used to represent data and relationships.

Components
Entity

An object that exists independently.

Examples:

Student
Employee
Course
Entity Set

Collection of similar entities.

Example:
All students in a university.

Attribute

Describes an entity.

Example:

Student:

StudentID
Name
Age
Relationship

Association between entities.

Example:

Student ----- Enrolls ----- Course
2.4 Complex Attributes

Attributes can be simple or complex.

1. Simple Attribute

Cannot be divided further.

Example:

Age
Salary
2. Composite Attribute

Can be divided into subparts.

Example:

Name
 ├─ First Name
 ├─ Middle Name
 └─ Last Name
3. Single-Valued Attribute

Contains only one value.

Example:

Date of Birth
4. Multi-Valued Attribute

Contains multiple values.

Example:

Phone Numbers
Phone Number:
98765432
17654321
5. Derived Attribute

Calculated from another attribute.

Example:

Age = Current Date – Date of Birth
2.5 Mapping Cardinalities

Cardinality specifies the number of entities participating in a relationship.

1. One-to-One (1:1)

One entity relates to one entity.

Example:

Person ↔ Passport

One person has one passport.

2. One-to-Many (1:N)

One entity relates to many entities.

Example:

Department → Employees

One department has many employees.

3. Many-to-One (N:1)

Many entities relate to one entity.

Example:

Employees → Department

Many employees belong to one department.

4. Many-to-Many (M:N)

Many entities relate to many entities.

Example:

Students ↔ Courses

A student takes many courses and a course has many students.

2.6 Primary Key

A primary key uniquely identifies each record in a table.

Characteristics
Unique
Cannot be NULL
Stable
One primary key per table

Example:

StudentID	Name
101	Sonam
102	Karma

StudentID is the primary key.

Candidate Key

A key that can become a primary key.

Alternate Key

Candidate key not selected as primary key.

Foreign Key

Attribute that references the primary key of another table.

Example:

Student Table

StudentID	Name
101	Sonam

Enrollment Table

EnrollID	StudentID
E1	101

StudentID in Enrollment is a foreign key.

2.7 Removing Redundant Attributes in Entity Sets
Redundancy

Occurs when the same information is stored multiple times.

Example

Student Table

ID	DOB	Age

Age can be calculated from DOB.

Thus Age is redundant.

Problems of Redundancy
Wasted storage
Update anomalies
Inconsistent data
Solution

Store only necessary attributes.

Store:

ID	DOB

Calculate Age when needed.

2.8 Reducing E-R Diagrams to Relational Schemas

Converting ER diagrams into relational tables.

Entity Set to Table

Entity:

Student
StudentID
Name
Age

Becomes:

Student(
StudentID PRIMARY KEY,
Name,
Age
)
Relationship to Table

Many-to-Many Relationship:

Student ↔ Course

Create:

Enrollment(
StudentID,
CourseID
)

Both become foreign keys.

Multi-Valued Attribute
Student
PhoneNumber

Convert into separate table:

StudentPhone(
StudentID,
PhoneNumber
)
2.9 Extended E-R Features

Extended ER (EER) adds advanced modeling concepts.

Specialization

Top-down approach.

Example:

Employee
 ├─ Manager
 └─ Engineer

Manager and Engineer inherit Employee attributes.

Generalization

Bottom-up approach.

Example:

Car
Truck
  ↓
Vehicle

Common attributes combined into Vehicle.

Inheritance

Subclasses inherit properties from superclass.

Example:

Manager inherits:

EmployeeID
Name
Salary
2.10 Entity-Relationship Design Issues
1. Choosing Entity Sets

Example:

Student should be an entity because it has independent existence.

2. Choosing Attributes

Example:

Age may be derived from DOB.

Store DOB instead of Age.

3. Choosing Relationships

Example:

Student Enrolls Course

This should be modeled as a relationship.

4. Binary vs Ternary Relationships
Binary Relationship
Student → Course
Ternary Relationship
Supplier → Part → Project

Three entities involved.

2.11 Alternative Notations for Modeling Data

Different notations are used to represent database models.

Chen Notation

Uses:

Rectangle = Entity
Oval = Attribute
Diamond = Relationship

Example:

[Student]
   |
(Name)
   |
<Enrolls>
   |
[Course]
Crow's Foot Notation

Widely used in industry.

Example:

Student |-----< Enrollment >-----| Course

Crow's foot symbol represents "many".

UML (Unified Modeling Language)

Used in software engineering.

Example:

+ Student
------------
StudentID
Name
Age
2.12 Other Aspects of Database Design
Data Integrity

Ensures correctness of data.

Types
Entity Integrity

Primary key cannot be NULL.

Referential Integrity

Foreign key must reference existing record.

Security

Protects data from unauthorized access.

Methods:

Passwords
Encryption
Access control
Performance

Improved through:

Indexing
Query optimization
Normalization
Scalability

Database should support future growth.

Backup and Recovery

Protects against data loss.

Examples:

Full backup
Incremental backup
2.13 Atomicity, Consistency, Isolation and Durability (ACID)

ACID properties ensure reliable transaction processing.

1. Atomicity

"All or Nothing"

Either all operations occur or none occur.

Example

Transfer Nu.1000 from Account A to B:

A = A - 1000
B = B + 1000

If one step fails, both operations are cancelled.

2. Consistency

Database moves from one valid state to another.

Example

Total money before and after transfer remains unchanged.

3. Isolation

Transactions execute independently.

Example

Two users withdrawing money simultaneously should not interfere with each other.

4. Durability

Once a transaction is committed, it remains permanent.

Example

Even after power failure, committed transactions remain saved.