Unit V: Relational Database Design – Complete Notes
5.1 Features of Good Relational Designs

A good relational database design stores data efficiently while minimizing redundancy and maintaining consistency.

Objectives of Good Design
1. Minimize Data Redundancy

Avoid storing the same data repeatedly.

Bad Example

StudentID	StudentName	DeptName
101	Sonam	IT
102	Karma	IT

Department name "IT" is repeated.

2. Avoid Update Anomalies
Insertion Anomaly

Cannot insert data without other information.

Deletion Anomaly

Deleting one record may remove important information.

Update Anomaly

Updating one value requires multiple changes.

3. Ensure Data Integrity

Data should remain:

Accurate
Consistent
Reliable
4. Improve Query Performance

Well-designed tables make searching faster.

5.2 Decomposition Using Functional Dependencies
What is Decomposition?

Breaking a large relation into smaller relations without losing information.

Example

Student Table

SID	Name	Dept	HOD

Functional Dependency:

Dept → HOD

Since HOD depends on Dept, separate tables can be created:

Student
SID	Name	Dept
Department
Dept	HOD

This reduces redundancy.

Goals of Decomposition
Lossless Join

Original table can be reconstructed.

Dependency Preservation

Functional dependencies remain valid.

5.3 Normal Forms

Normalization is the process of organizing data to reduce redundancy.

Types of Normal Forms
1NF

First Normal Form

2NF

Second Normal Form

3NF

Third Normal Form

BCNF

Boyce-Codd Normal Form

4NF

Fourth Normal Form

5NF

Fifth Normal Form

5.4 Functional-Dependency Theory
Functional Dependency (FD)

A relationship between attributes.

Notation:

X → Y

Meaning:
If two rows have the same X value, they must have the same Y value.

Example

Student Table

StudentID	Name
101	Sonam
102	Karma

Dependency:

StudentID → Name

StudentID uniquely determines Name.

Types of Functional Dependencies
1. Trivial FD
A,B → A

Right side already appears on left side.

2. Non-Trivial FD
StudentID → Name

Name not part of left side.

3. Completely Non-Trivial FD

No attribute common on both sides.

StudentID → Department
Armstrong's Axioms

Rules for finding dependencies.

Reflexivity

If Y ⊆ X

X → Y

Example:

(A,B) → A
Augmentation

If:

X → Y

Then:

XZ → YZ
Transitivity

If:

X → Y
Y → Z

Then:

X → Z
5.5 Algorithms for Decomposition Using Functional Dependencies

Decomposition algorithms divide relations into smaller tables.

3NF Decomposition Algorithm

Steps:

Find minimal cover.
Create relation for each FD.
Ensure a candidate key exists.
Remove redundant relations.
BCNF Decomposition Algorithm

Steps:

Identify BCNF violations.
Split relation into smaller relations.
Repeat until all relations satisfy BCNF.
Advantages
Removes redundancy
Prevents anomalies
Maintains consistency
5.6 Decomposition Using Multivalued Dependencies
Multivalued Dependency (MVD)

Occurs when one attribute determines multiple independent values.

Notation:

A ↠ B

(Read as A multivalued determines B)

Example
Student	Hobby	Language
Sonam	Football	English
Sonam	Football	Dzongkha
Sonam	Music	English
Sonam	Music	Dzongkha

Dependencies:

Student ↠ Hobby
Student ↠ Language
Solution

Separate tables:

Student_Hobby

Student	Hobby

Student_Language

Student	Language

This removes redundancy.

5.7 More Normal Forms
BCNF (Boyce-Codd Normal Form)

A relation is in BCNF if:

For every FD X → Y,
X must be a super key.
Example

Not BCNF:

Course → Instructor

If Course is not a super key.

Fourth Normal Form (4NF)

Removes multivalued dependencies.

Condition:

A ↠ B

must have A as a super key.

Fifth Normal Form (5NF)

Removes join dependencies.

Used when information can be reconstructed from smaller tables without redundancy.

5.8 Atomic Domains and First Normal Form
Atomic Domain

An attribute contains indivisible values.

Atomic Value
Phone = 17123456

Single value.

Non-Atomic Value
Phone =
17123456,77223344

Contains multiple values.

First Normal Form (1NF)

A relation is in 1NF if:

All attributes contain atomic values.
No repeating groups.
No multivalued attributes.
Not in 1NF
Student	Phones
Sonam	17123456,77223344
In 1NF
Student	Phone
Sonam	17123456
Sonam	77223344
5.9 Database-Design Process

Database design follows a structured approach.

Step 1: Requirement Collection

Gather user requirements.

Questions:

What data is needed?
Who will use it?
Step 2: Conceptual Design

Create ER Diagram.

Example:

Student ---- Enrolls ---- Course
Step 3: Logical Design

Convert ER model into relational schema.

Example:

Student(StudentID, Name)
Course(CourseID, Title)
Enrollment(StudentID, CourseID)
Step 4: Normalization

Apply:

1NF
2NF
3NF
BCNF
Step 5: Physical Design

Choose:

Storage structures
Indexes
File organization
Step 6: Implementation

Create database tables using SQL.

Step 7: Testing and Maintenance

Monitor:

Performance
Security
Backup and recovery
5.10 Modelling Temporal Data

Temporal data stores information related to time.

Why Temporal Data?

Some data changes over time.

Examples:

Employee salary
Student address
Product price
Types of Time
Valid Time

Time when a fact is true in the real world.

Example:

Salary = Nu.30,000
From Jan 2024 to Dec 2024
Transaction Time

Time when data is stored in database.

Example:

Salary updated on:
15 March 2025
Temporal Table Example
EmployeeID	Salary	StartDate	EndDate
E01	30000	2024-01-01	2024-12-31
E01	35000	2025-01-01	NULL

NULL means current salary.

Applications of Temporal Data
Banking

Track account history.

Healthcare

Track patient records over time.

Human Resources

Track salary changes.

E-Commerce

Track product price history.

Quick Revision
Features of Good Design
Minimal redundancy
No anomalies
Data integrity
Better performance
Functional Dependency
X → Y

X determines Y.

Example:

StudentID → Name
Multivalued Dependency
X ↠ Y

X determines multiple values of Y.

Normal Forms
Normal Form	Purpose
1NF	Atomic values
2NF	Remove partial dependency
3NF	Remove transitive dependency
BCNF	Every determinant is a super key
4NF	Remove multivalued dependency
5NF	Remove join dependency
Armstrong's Axioms
Reflexivity
Augmentation
Transitivity
Decomposition Goals
Lossless Join
Dependency Preservation
Types of Time
Valid Time
Transaction Time