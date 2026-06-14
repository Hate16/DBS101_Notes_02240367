Unit VII: Transactions, Concurrency Control and Recovery Systems – Complete Notes
7.1 Simple Transaction Models
What is a Transaction?

A transaction is a sequence of database operations treated as a single logical unit of work.

A transaction must either:

Complete successfully (Commit)
Fail completely (Rollback)
Example

Bank Transfer:

Account A = A - 1000
Account B = B + 1000

Both operations must be completed together.

Transaction States
1. Active

Transaction is executing.

START → ACTIVE
2. Partially Committed

Last statement executed.

ACTIVE → PARTIALLY COMMITTED
3. Committed

Changes permanently saved.

PARTIALLY COMMITTED → COMMITTED
4. Failed

An error occurs.

ACTIVE → FAILED
5. Aborted

All changes are undone.

FAILED → ABORTED
Transaction State Diagram
Start
  ↓
Active
  ↓
Partially Committed
  ↓
Committed

If Error:
Active → Failed → Aborted
7.2 Transaction Atomicity, Isolation and Durability

These are three important ACID properties.

Atomicity
Definition

A transaction executes completely or not at all.

Example

Transfer Nu.1000:

Withdraw from A
Deposit into B

If deposit fails:

Rollback

No money should be lost.

Isolation
Definition

Transactions execute independently.

Example

Two users withdrawing money simultaneously should not interfere.

Durability
Definition

Once committed, data remains permanent.

Example

After:

COMMIT;

Data remains even if:

System crashes
Power fails
7.3 Transaction Isolation Levels

Isolation levels determine how much one transaction can see changes made by another transaction.

Problems Caused by Concurrent Transactions
Dirty Read

Reading uncommitted data.

Non-Repeatable Read

Reading different values during the same transaction.

Phantom Read

New rows appear unexpectedly.

Isolation Levels
1. Read Uncommitted

Lowest isolation level.

Features
Allows dirty reads.
Fastest performance.
Transaction A
reads data modified
by Transaction B
before commit.
2. Read Committed

Only committed data can be read.

Prevents

✔ Dirty Reads

Allows

✘ Non-repeatable Reads

3. Repeatable Read

Data read once remains unchanged.

Prevents

✔ Dirty Reads

✔ Non-repeatable Reads

Allows

✘ Phantom Reads

4. Serializable

Highest isolation level.

Prevents

✔ Dirty Reads

✔ Non-repeatable Reads

✔ Phantom Reads

Drawback

Slower performance.

Comparison
Isolation Level	Dirty Read	Non-Repeatable Read	Phantom Read
Read Uncommitted	Yes	Yes	Yes
Read Committed	No	Yes	Yes
Repeatable Read	No	No	Yes
Serializable	No	No	No
7.4 Serializability
Definition

Serializability ensures concurrent transactions produce the same result as serial execution.

Serial Schedule

Transactions execute one after another.

Example:

T1 completes
T2 starts
Concurrent Schedule

Transactions execute simultaneously.

Example:

T1
T2
T1
T2
Types of Serializability
1. Conflict Serializability

Based on conflicting operations.

Conflicts occur when:

Read-Write
Write-Read
Write-Write

occur on the same data item.

2. View Serializability

Schedules produce the same final result as a serial schedule.

More general than conflict serializability.

Importance
Maintains consistency
Prevents incorrect results
7.5 Lock-Based Protocols

Locks control access to data.

Why Locks?

Prevent multiple transactions from modifying the same data simultaneously.

Types of Locks
Shared Lock (S)

Used for reading.

Multiple transactions may hold shared locks.

Read Allowed
Write Not Allowed
Exclusive Lock (X)

Used for writing.

Only one transaction may hold it.

Read Not Allowed
Write Allowed
Lock Compatibility
Lock	Shared	Exclusive
Shared	Yes	No
Exclusive	No	No
Two-Phase Locking (2PL)

Most common locking protocol.

Growing Phase

Acquire locks.

Lock A
Lock B
Shrinking Phase

Release locks.

Unlock B
Unlock A
Benefits
Ensures serializability
Prevents inconsistencies
7.6 Deadlock Handling
What is Deadlock?

A deadlock occurs when transactions wait forever for each other.

Example

Transaction T1:

Locks Account A
Needs Account B

Transaction T2:

Locks Account B
Needs Account A

Result:

T1 waits for T2
T2 waits for T1

Deadlock occurs.

Deadlock Prevention

Prevent deadlocks before they occur.

Methods:

Resource ordering
Timestamp ordering
Deadlock Detection

System periodically checks for deadlocks.

Uses:

Wait-For Graph
Deadlock Recovery

After detection:

Option 1

Abort one transaction.

Option 2

Rollback one transaction.

7.7 Concurrency Control Mechanisms

Concurrency control ensures correct execution of simultaneous transactions.

Objectives
Maintain consistency
Prevent conflicts
Improve performance
Methods
1. Lock-Based Protocols

Use shared and exclusive locks.

2. Timestamp-Based Protocols

Assign timestamps to transactions.

Example:

T1 = 10
T2 = 20

Older transactions get priority.

3. Validation-Based Protocols

Also called optimistic concurrency control.

Steps:

Read Phase
Validation Phase
Write Phase
4. Multiversion Concurrency Control (MVCC)

Stores multiple versions of data.

Readers do not block writers.

Used in:

PostgreSQL
Oracle Database
7.8 Recovery Algorithms

Recovery algorithms restore the database after failures.

Types of Failures
Transaction Failure

Transaction cannot complete.

System Crash

Power outage or operating system failure.

Media Failure

Disk damage or corruption.

Recovery Techniques
Log-Based Recovery

DBMS maintains a log file.

Example:

<T1 START>
<T1 WRITE A>
<T1 COMMIT>
Undo Operation

Removes effects of incomplete transactions.

UNDO(T1)
Redo Operation

Reapplies committed transactions.

REDO(T1)
Checkpointing

Periodically saves database state.

Example:

Checkpoint at 2:00 PM

Recovery starts from the checkpoint rather than the beginning.

Immediate Update

Changes written before commit.

Requires:

UNDO + REDO
Deferred Update

Changes written after commit.

Requires:

REDO only
7.10 Remote Backup Systems

Remote backup systems maintain copies of data at remote locations.

Purpose

Protect data from:

Hardware failures
Natural disasters
Cyber attacks
Human errors
Architecture
Primary Database
        ↓
Network
        ↓
Backup Database
Types of Remote Backup
1. Synchronous Backup

Primary and backup databases updated simultaneously.

Advantages
No data loss
Disadvantages
Slower performance
2. Asynchronous Backup

Updates sent later.

Advantages
Faster performance
Disadvantages
Possible data loss
Benefits
Disaster recovery
High availability
Business continuity
Data protection
Example

A bank stores:

Main database in Thimphu
Backup database in another city

If the main system fails, the backup system continues operation.

Quick Revision
Transaction States
Active
↓
Partially Committed
↓
Committed

OR

Active
↓
Failed
↓
Aborted
ACID Properties
Atomicity → All or Nothing
Consistency → Valid State
Isolation → Independent Transactions
Durability → Permanent Changes
Isolation Levels
Read Uncommitted
Read Committed
Repeatable Read
Serializable
Types of Locks
Shared Lock (Read)
Exclusive Lock (Write)
Deadlock Solutions
Prevention
Detection
Recovery
Concurrency Control Methods
Lock-Based
Timestamp-Based
Validation-Based
MVCC
Recovery Operations
UNDO
REDO
Checkpointing
Remote Backup Types
Synchronous Backup
Asynchronous Backup