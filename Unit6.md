Unit VI: Indexing and Query Processing – Complete Notes
6.1 Basic Concepts of Indexing
What is Indexing?

Indexing is a technique used to speed up data retrieval in a database.

Just like a book index helps find a topic quickly without reading the whole book, a database index helps locate records without scanning the entire table.

Why is Indexing Needed?

Without an index:

Database → Scan every row

With an index:

Database → Directly locate rows

This improves query performance significantly.

Example

Student Table

StudentID	Name
101	Sonam
102	Karma
103	Pema

Query:

SELECT *
FROM Student
WHERE StudentID = 102;

If StudentID is indexed, the database finds the record directly.

Advantages of Indexing
Faster data retrieval
Faster searching
Faster sorting
Improves query performance
Disadvantages of Indexing
Requires additional storage
Slower INSERT operations
Slower UPDATE operations
Slower DELETE operations
6.2 Indexing Structures

An index structure is the method used to organize index entries.

Types of Index Structures
1. Single-Level Index

One index file points directly to records.

Index
 ↓
Records

Simple but inefficient for large databases.

2. Multi-Level Index

Indexes are built on top of other indexes.

Root Index
     ↓
Sub Index
     ↓
Data Blocks

Faster than single-level indexing.

B-Tree Index

Most common indexing structure.

Characteristics
Balanced tree
Sorted data
Efficient insertion and deletion

Example:

         50
       /    \
     20      80
    /  \    /  \
  10  30 60 100
B+ Tree Index

Most widely used in modern DBMS.

Features
Internal nodes store keys only.
Leaf nodes store actual pointers to records.
Leaf nodes are linked.
Root
 ↓
Internal Nodes
 ↓
Leaf Nodes (Data Pointers)
Advantages
Fast search
Efficient range queries
Better disk access
Hash Index

Uses a hash function to locate records.

Example:

Hash(101) → Bucket 1
Hash(102) → Bucket 2
Advantages
Extremely fast exact-match searches
Disadvantages
Poor for range queries
6.3 Ordered and Unordered Indices

Indexes can be classified based on the arrangement of entries.

Ordered Index

Index entries are stored in sorted order.

Example:

Key	Pointer
101	P1
102	P2
103	P3
Advantages
Efficient range searches
Supports sorting

Example:

SELECT *
FROM Student
WHERE StudentID
BETWEEN 100 AND 200;
Unordered Index (Hash Index)

Entries are stored according to hash values.

Example:

Hash(101) = Bucket 3
Hash(102) = Bucket 1
Hash(103) = Bucket 7
Advantages
Fast exact searches

Example:

SELECT *
FROM Student
WHERE StudentID = 102;
Comparison
Feature	Ordered	Unordered
Exact Search	Fast	Very Fast
Range Search	Excellent	Poor
Sorting	Supported	Not Supported
6.4 Indexing of Temporal and Spatial Data
Temporal Data Indexing

Temporal data changes over time.

Examples:

Salary history
Product prices
Student addresses
Temporal Table
EmployeeID	Salary	StartDate	EndDate
E1	30000	2024-01-01	2024-12-31
E1	35000	2025-01-01	NULL
Why Temporal Indexing?

To answer questions like:

What was Sonam's salary in 2024?

Special temporal indexes speed up time-based searches.

Spatial Data Indexing

Spatial data represents locations and geometric objects.

Examples:

Maps
GPS locations
Buildings
Roads
Spatial Objects
Point
(5,3)
Line
A -------- B
Polygon
Rectangle
Triangle
R-Tree

Most common spatial indexing structure.

Features
Stores geometric objects
Efficient for map searches
Supports nearest-neighbor queries

Applications:

Google Maps
GIS systems
Navigation systems
6.5 Indexing for Search

Indexes improve search efficiency.

Exact Match Search

Example:

SELECT *
FROM Student
WHERE StudentID = 101;

Best Index:

Hash Index
Range Search

Example:

SELECT *
FROM Student
WHERE Age BETWEEN 18 AND 25;

Best Index:

B+ Tree
Prefix Search

Example:

SELECT *
FROM Student
WHERE Name LIKE 'S%';

Best Index:

B+ Tree
Full-Text Search

Searches text content.

Example:

Find all documents containing
"database"

Used in:

Search engines
Libraries
E-commerce websites
Search Performance Factors
Number of records
Type of index
Disk access speed
Query complexity
6.6 Query Processing and Optimization

Query processing converts SQL statements into efficient operations.

Steps in Query Processing
Step 1: Parsing

Checks SQL syntax.

Example:

SELECT *
FROM Student;
Step 2: Translation

Converts SQL into an internal representation.

Step 3: Optimization

Finds the most efficient execution plan.

Step 4: Evaluation

Executes the query.

SQL Query
     ↓
Parser
     ↓
Optimizer
     ↓
Execution Engine
     ↓
Result
6.6.1 Measures of Query Cost

The DBMS evaluates query plans using cost measures.

1. Disk Access Cost

Most important factor.

Reading data from disk is expensive.

Example:

100 Disk Reads

is more costly than:

10 Disk Reads
2. CPU Cost

Time spent processing data.

Includes:

Comparisons
Sorting
Calculations
3. Memory Cost

Amount of RAM required.

Large queries need more memory.

4. Communication Cost

Important in distributed databases.

Data transferred over a network increases cost.

Goal

Choose the plan with the lowest total cost.

6.6.2 Evaluation of Expression

The DBMS executes relational operations to evaluate queries.

Selection Operation

Filters rows.

Example:

SELECT *
FROM Student
WHERE Age > 20;
Projection Operation

Selects columns.

Example:

SELECT Name
FROM Student;
Join Operation

Combines tables.

Example:

SELECT Name, DeptName
FROM Student
JOIN Department
ON Student.DeptID=
Department.DeptID;
Sorting

Orders records.

Example:

SELECT *
FROM Student
ORDER BY Name;
Aggregation

Computes summaries.

Example:

SELECT AVG(Marks)
FROM Student;
6.6.3 Choice of Evaluation Plans

A query can be executed in different ways.

The optimizer selects the best plan.

Example

Query:

SELECT *
FROM Student
WHERE StudentID = 101;

Possible Plans:

Plan A
Full Table Scan

Read every record.

Plan B
Use Index

Directly locate record.

Comparison
Plan	Cost
Full Scan	High
Index Search	Low

Optimizer chooses:

Plan B
Factors Affecting Plan Selection
Available Indexes

More useful indexes often mean lower cost.

Table Size

Large tables benefit more from indexes.

Selectivity

Selectivity = Fraction of rows returned.

Example:

1 row out of 1,000,000

Very selective query.

Index is beneficial.

Memory Availability

More memory allows faster operations.