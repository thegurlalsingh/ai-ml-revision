---
title: "DBMS Interview Preparation"
source: "https://chatgpt.com/c/6a44c279-dc90-83ee-8eb2-00e54a4f3f72?mweb_fallback=1"
---

**You:**

okay i am studying dbms and will tell you topics one by one, just explain me everything in brief regarding what will be asked in interviews and discussion can happen on them 
concept should be explain in detail and simple manner

* * *

**ChatGPT:**

Perfect. Given your interview goals (AI/ML + Software + Backend), we'll approach DBMS like an interviewer would, not like an exam.

For every topic you send, I'll explain it in this structure:

### 1. What is it?

* Simple intuition
* Real-world analogy
* Why it exists

### 2. How does it work?

* Step-by-step internally
* Small examples
* Visual imagination (without unnecessary complexity)

### 3. Why do we need it?

* What problem does it solve?
* What happens if it didn't exist?

### 4. Advantages & Disadvantages

* When to use
* When not to use

### 5. Interview Questions

I'll cover things like:

* Basic questions
* Follow-up questions
* Tricky questions
* "Why?" questions
* Comparison questions

Example:

> What is normalization?

↓

Then interviewer asks

> Why not fully normalize every database?

↓

Then

> What is denormalization?

↓

Then

> Which companies use denormalization?

↓

Then

> Why does Netflix use denormalization?

This is exactly how interviews flow.

* * *

### 6. Coding/System Design Connection

I'll explain where this concept appears in:

* Backend development
* APIs
* Microservices
* SQL queries
* Large-scale systems
* AI/ML data pipelines (where relevant)

* * *

### 7. Important SQL Queries (if applicable)

If the topic involves SQL, I'll show:

* Syntax
* Logic
* Common mistakes
* Optimized versions

* * *

### 8. Internal Working (the part interviewers love)

Instead of memorizing definitions, we'll understand what happens behind the scenes.

For example:

* Indexes → How B+ Trees actually work
* Transactions → What happens when two users update the same row
* Locks → Why deadlocks occur
* Joins → How the database executes them
* Buffer Pool → Why reading from RAM is faster
* Query Optimizer → How SQL gets converted into an execution plan

* * *

### 9. Frequently Confused Concepts

I'll compare concepts interviewers often ask together, for example:

* DELETE vs TRUNCATE vs DROP
* WHERE vs HAVING
* CHAR vs VARCHAR
* Primary Key vs Unique Key
* Clustered vs Non-clustered Index
* OLTP vs OLAP
* 2NF vs 3NF
* Shared Lock vs Exclusive Lock
* Serializable vs Repeatable Read
* Row Lock vs Table Lock

* * *

### 10. Interviewer's Thought Process

I'll also explain why interviewers ask a question and what kind of answer they're looking for.

For example:

> "Why is VARCHAR preferred over CHAR?"

A weak answer:

> "Because it saves space."

A strong answer:

> "VARCHAR stores variable-length strings, reducing storage overhead for varying data sizes. However, because row lengths become variable, updates may require row relocation, making CHAR preferable for fixed-length fields like country codes or gender."

That's the level expected in good product companies.

* * *

### 11. Common Follow-up Chains

We'll practice natural interview conversations.

Example:

> What is an Index?

↓

> Does index always improve performance?

↓

> Why does insertion become slower?

↓

> What data structure is used?

↓

> Why B+ Tree instead of Binary Search Tree?

↓

> Why not Hash Table?

↓

> Which databases use Hash Index?

↓

> When would you prefer one over the other?

This prepares you for real interviews rather than isolated questions.

* * *

### 12. Quick Revision

At the end of every topic, I'll provide:

* 5-line summary
* Key takeaways
* Interview checklist
* Most probable questions (high-frequency)

* * *

We'll keep the explanations simple, intuitive, and detailed enough that you can confidently answer both basic and deep follow-up questions.

Send me your **first DBMS topic**, and we'll start from there.

* * *

**You:**

1. what is data vs information. what is its types of data
2. what is database
3. what is dbms
4. how this data is stored in dbms 
5. what is file system and what is diff between file system vs dbms (data redundancy and inconsistency, diffifculty in accessing data, data isolation, integrity problems, atomicity problems, concurrent access anomalies, security problems) explain each of them, how they can be prevented and what is advantage of them in dbms over file system

* * *

**ChatGPT:**

Excellent. These are literally the first topics almost every DBMS interviewer starts with. Many students memorize definitions, but interviewers keep asking "why?" until they find whether you actually understand DBMS.

Let's study these exactly like an interview.

* * *

# 1. Data vs Information

## What is Data?

Data is **raw facts and figures** that by themselves have little or no meaning.

Think of data as **ingredients**.

Example:

```
John
21
Delhi
```

Looking at these three values separately tells us nothing.

These are just pieces of data.

Another example

```
98
87
92
```

Just numbers.

* * *

## What is Information?

Information is **processed and organized data that has meaning and can help in decision making.**

Now combine the previous data.

| Name | Age | City |
| --- | --- | --- |
| John | 21 | Delhi |

Now it tells something.

This is **information**.

Another example

```
Marks

Math = 98
Physics = 87
Chemistry = 92

Average = 92.3
Rank = 5
```

Now this becomes useful.

* * *

## Simple Analogy

Imagine cooking.

Raw vegetables

Rice

Salt

Spices

↓

These are **Data**

↓

Cook the food

↓

Delicious Biryani

↓

This is **Information**

* * *

## Interview Question

### Difference?

| Data | Information |
| --- | --- |
| Raw facts | Processed data |
| No meaning alone | Meaningful |
| Input | Output |
| Used for processing | Used for decisions |

* * *

## Follow-up

**Q:** Can information become data?

Yes.

Example

Today's sales report is information.

Tomorrow that report becomes historical data.

* * *

# Types of Data

There are multiple ways to classify data.

Interviewers usually ask these.

* * *

## 1. Structured Data

Stored in rows and columns.

Example

Employee table

| ID | Name | Salary |
| --- | --- | --- |
| 1 | John | 50000 |

Very easy to search.

Stored inside relational databases.

Examples

* MySQL
* PostgreSQL
* Oracle

* * *

## 2. Semi-Structured Data

Has some structure but not fixed tables.

Examples

```
JSON

{
"name":"John",
"age":22
}
```

or XML

Flexible.

* * *

## 3. Unstructured Data

No predefined format.

Examples

Images

Videos

Emails

Audio

PDFs

Social media posts

Huge companies mostly deal with this.

* * *

## Interview Question

**Which data type is most common today?**

Answer:

Unstructured data.

Around 80-90% of the world's data is unstructured.

* * *

# 2. What is Database?

## Definition

A **Database** is an organized collection of related data stored electronically so it can be easily accessed, managed, and updated.

Simply,

Database = Collection of related information.

* * *

Example

Instagram stores

```
Users

Followers

Posts

Comments

Likes

Messages
```

All together form one database.

* * *

Imagine a college.

It stores

Students

Faculty

Departments

Courses

Attendance

Marks

Everything together forms the college database.

* * *

## Real-life Analogy

Think of a library.

Books are arranged properly.

You can quickly search.

Borrow.

Return.

Update.

Library = Database

Librarian = DBMS

Books = Data

* * *

## Interview Question

**Can we have multiple databases?**

Yes.

One company may have

Employee Database

Payroll Database

Inventory Database

Customer Database

* * *

# 3. What is DBMS?

This is one of the most important definitions.

* * *

## Definition

A **Database Management System (DBMS)** is software that allows users to create, manage, retrieve, update, and delete data from a database.

Examples

* MySQL
* PostgreSQL
* Oracle Database
* SQLite
* Microsoft SQL Server

* * *

Think like this

```
User

↓

DBMS

↓

Database
```

User never directly accesses the database.

Everything goes through DBMS.

* * *

## Why do we need DBMS?

Suppose you have 50 million records.

How will you

Search?

Update?

Delete?

Maintain security?

Handle multiple users?

Recover after crashes?

Very difficult.

DBMS solves all these.

* * *

## Example

Suppose Facebook wants to find

```
User ID = 87454
```

You simply write

```SQL
SELECT * FROM Users
WHERE id=87454;
```

DBMS does all the hard work internally.

* * *

## Responsibilities of DBMS

* Store data
* Retrieve data
* Update data
* Delete data
* Security
* Backup
* Recovery
* Concurrency control
* Integrity checking
* Transaction management

* * *

## Interview Question

Difference between Database and DBMS?

Database = Stored data.

DBMS = Software that manages that data.

Think

```
Database = Books

DBMS = Librarian
```

* * *

# 4. How is Data Stored inside DBMS?

Many students think the database stores SQL statements. It doesn't.

It stores data on disk in an organized way.

Let's see the journey.

* * *

Imagine this SQL

```SQL
INSERT INTO Employee
VALUES(1,'John',50000);
```

What happens?

### Step 1

SQL reaches DBMS.

↓

### Step 2

Parser checks syntax.

Is SQL correct?

↓

### Step 3

Optimizer decides the best execution plan.

↓

### Step 4

Storage Manager stores data.

↓

### Step 5

Data is written into pages on disk.

* * *

## Internal Storage

Hard disks don't store tables.

They store **files**.

Inside files are **pages (blocks)**.

Inside pages are **records (rows)**.

```
Database

↓

Files

↓

Pages (4KB, 8KB, 16KB...)

↓

Rows (records)

↓

Columns
```

Example

```
Employee Table

↓

employee.dat

↓

Page 1

John

Alice

Bob

↓

Page 2

Sam

Tom
```

* * *

## Why Pages?

Reading one row directly from disk is slow.

Instead DBMS reads an entire page into memory.

Much faster.

* * *

## Buffer Pool

Frequently accessed pages are stored in RAM.

```
Disk

↓

Buffer Pool (RAM)

↓

CPU
```

This is why repeated queries become faster.

* * *

## Index

Suppose 1 crore employees.

Searching sequentially

```
John

Sam

Bob

Tom

....
```

Very slow.

DBMS creates an **Index**.

Usually using a **B+ Tree**.

Searching becomes much faster.

* * *

# Interview Question

Does DBMS store data in RAM?

No.

Permanent storage is on disk/SSD.

RAM is only for caching (Buffer Pool).

* * *

# 5. File System vs DBMS

This is one of the most frequently asked interview topics.

* * *

## What is File System?

A file system stores data in separate files.

Example

```
students.txt

teachers.txt

fees.txt

attendance.txt
```

Each application manages its own files.

No central management.

* * *

## Example

College stores

```
Student.txt

Faculty.txt

Course.txt
```

Every software reads these files independently.

Problems begin when the same data appears in multiple files.

* * *

# Problems of File System

* * *

# 1. Data Redundancy

Redundancy means **duplicate copies of the same data**.

Example

```
Student.txt

ID 101
John
Delhi
```

```
Fees.txt

ID 101
John
Delhi
```

John's city is stored twice.

Now imagine 20 files.

Huge duplication.

* * *

### Problems

Extra storage.

More updates.

Higher maintenance.

* * *

### How DBMS solves it?

Normalization stores data only once.

Student table

|ID|Name|City|

Fees table

|StudentID|Fees|

City is stored only in the Student table.

No unnecessary duplication.

* * *

# 2. Data Inconsistency

Suppose John shifts to Mumbai.

Update Student.txt

```
Mumbai
```

Forget to update Fees.txt

```
Delhi
```

Now the same student has two cities.

Which one is correct?

This is inconsistency.

* * *

### Prevention in DBMS

Single source of truth through normalization and constraints.

Update once.

Everywhere consistent.

* * *

# 3. Difficulty in Accessing Data

Suppose you want

```
Students with marks >90 and attendance >80%
```

In file system

Read file.

Write code.

Search manually.

Very slow.

* * *

DBMS

```SQL
SELECT *
FROM Student
WHERE Marks>90
AND Attendance>80;
```

Very easy.

* * *

# 4. Data Isolation

Files are stored separately.

Formats differ.

One file

CSV

Another

TXT

Another

Excel

Combining becomes difficult.

* * *

DBMS

Everything follows the same schema.

Easy joins.

* * *

# 5. Integrity Problems

Integrity means data should remain correct.

Example

Age = -5

Salary = -1000

Marks = 120

These are invalid values.

File system allows them unless your application checks every case.

* * *

DBMS prevents this using constraints like:

* **NOT NULL** – value cannot be empty.
* **CHECK** – value must satisfy a condition (e.g., marks between 0 and 100).
* **PRIMARY KEY** – uniquely identifies each row.
* **FOREIGN KEY** – ensures related data exists.
* **UNIQUE** – prevents duplicate values.

* * *

# 6. Atomicity Problems

Atomicity means

Either everything happens.

Or nothing happens.

Example

Transfer ₹1000.

```
A = 5000

B = 3000
```

Step 1

Deduct

```
A = 4000
```

Power failure.

B never gets money.

Money disappeared.

* * *

DBMS uses **transactions**.

```
BEGIN

Debit

Credit

COMMIT
```

If failure

```
ROLLBACK
```

Database returns to the previous consistent state.

* * *

# 7. Concurrent Access Anomalies

Two users edit the same data simultaneously.

Example

Account Balance

```
1000
```

User A withdraws 500.

User B withdraws 700.

If both read the balance before either writes back, they each think the balance is 1000. One update may overwrite the other, resulting in an incorrect final balance.

DBMS prevents such anomalies using:

* Locks
* Transactions
* Isolation levels
* Multi-Version Concurrency Control (MVCC) in many databases

We'll study these in depth later.

* * *

# 8. Security Problems

Suppose Employee Salary is stored in a text file.

Anyone with file access can read it.

No fine-grained control.

* * *

DBMS provides:

* User authentication
* Roles
* Permissions
* GRANT/REVOKE privileges
* Encryption (in many systems)
* Auditing

Only authorized users can access sensitive data.

* * *

# File System vs DBMS

| Feature | File System | DBMS |
| --- | --- | --- |
| Redundancy | High | Low (using normalization) |
| Inconsistency | Common | Rare |
| Querying | Manual programming | SQL |
| Security | Basic file permissions | Fine-grained access control |
| Concurrency | Poor | Built-in concurrency control |
| Atomicity | Not guaranteed | Transactions (ACID) |
| Integrity | Application-dependent | Constraints enforced by DBMS |
| Backup & Recovery | Limited/manual | Built-in mechanisms |
| Scalability | Limited | Designed for large datasets |

* * *

# High-Frequency Interview Questions

1. **What is the difference between data and information?**
2. **What are structured, semi-structured, and unstructured data? Give examples.**
3. **What is a database?**
4. **What is the role of a DBMS?**
5. **Explain the internal storage hierarchy of a DBMS (files → pages → records).**
6. **Why does a DBMS read pages instead of individual rows?**
7. **What is data redundancy? How does normalization reduce it?**
8. **What is data inconsistency? Give a real-life example.**
9. **What is data integrity? Which constraints enforce it?**
10. **What is atomicity? Explain with a bank transfer example.**
11. **What are concurrent access anomalies? Why are transactions necessary?**
12. **Compare a file system and a DBMS. Why is a DBMS preferred for modern applications?**

* * *

## Quick Revision (5 Minutes)

* **Data** = Raw facts; **Information** = Processed, meaningful data.
* **Database** = Organized collection of related data.
* **DBMS** = Software that manages databases, provides querying, security, transactions, recovery, and concurrency.
* **Storage**: Database → Files → Pages (blocks) → Records (rows), with a **buffer pool** caching frequently used pages in RAM.
* **DBMS advantages over file systems**: eliminates unnecessary redundancy through normalization, reduces inconsistency, supports powerful SQL queries, enforces integrity constraints, guarantees atomic transactions, safely handles concurrent users, and provides robust security.

These concepts form the foundation of DBMS. Understanding them well makes topics like normalization, keys, transactions, indexing, and concurrency much easier to learn later.

* * *

**You:**

1. abstraction in dbms
2, what is architectures in dbms and diff types of architechture
3. physical level, logical level, view level with examples
4. what is schema
5. instance of db
6. data models with examples
7. database languages (ddl, dml) what they do with examples and query language
8.  how sql and real world applications connect, like javascript and sql
9. database administrator ( functions including schema defination, storage structure and access methods, schema and physical organziation modifications, auth control, runtime maintenance such as periodic backups, security patches and any upgrades)
10. dbms application architecture (t1, t2, t3 arch) examples, advantgaes, disadvantasges

* * *

**ChatGPT:**

Perfect. These topics are interconnected. Once you understand them, you'll know **how a DBMS is designed internally** and **how applications communicate with databases**.

* * *

# 1. Abstraction in DBMS

## First understand why abstraction exists

Imagine you're driving a car.

Do you know:

* How the engine burns fuel?
* How the gearbox changes gears internally?
* How the brakes work?

No.

You simply use

* Steering
* Brake
* Accelerator

The complicated details are hidden.

This is called **abstraction**.

* * *

## Same happens in DBMS.

Suppose Facebook has a database containing

```
Users
Posts
Comments
Messages
Likes
```

When a user logs in, do they know

* where data is stored on disk?
* how pages are organized?
* which index is used?
* how memory management works?

No.

DBMS hides all these complexities.

This hiding is called **Data Abstraction**.

* * *

## Definition

> Data abstraction is the process of hiding unnecessary implementation details and showing only the required information to different users.

* * *

## Why is abstraction needed?

Without abstraction,

Every programmer would need to know

* disk management
* indexing
* page organization
* storage formats
* buffer pool

Writing one query would become impossible.

Abstraction makes databases easy to use.

* * *

## Interview Question

**Q: Why can't everyone directly access physical storage?**

Because

* it is complex
* insecure
* difficult to maintain
* changing storage shouldn't affect applications

* * *

# 2. Architecture in DBMS

There are **two different meanings** of architecture in DBMS.

Students often confuse them.

## Architecture Type 1

### Three-Level Architecture

This explains **how data is viewed**.

```
Users

↓

View Level

↓

Logical Level

↓

Physical Level
```

We'll study this in detail in the next topic.

* * *

## Architecture Type 2

Application Architecture

```
1-tier
2-tier
3-tier
```

This explains

How applications connect to databases.

We'll study it later.

* * *

# 3. Physical Level, Logical Level, View Level

This is probably the most frequently asked conceptual question.

* * *

Imagine Instagram database.

It stores

```
Users

Posts

Followers

Messages

Likes
```

Different people need different information.

* * *

# Level 1 : Physical Level

This is the **lowest level**.

It tells

**How data is actually stored.**

Examples

* Hard Disk
* SSD
* Pages
* Blocks
* B+ Trees
* Hash Index
* Compression

Example

Suppose

```
User

ID 101

John

Delhi
```

Internally DBMS stores

```
Disk

↓

Page 5

↓

Byte 230

↓

Binary data
```

Users never see this.

* * *

### Who works here?

Database Engineers

DBMS Developers

Storage Engine Developers

* * *

### Interview Question

Does an application know where data is stored physically?

No.

* * *

# Level 2 : Logical Level

This is the middle layer.

It tells

**What data is stored and how tables are related.**

Example

```
Student

StudentID

Name

Age
```

```
Course

CourseID

CourseName
```

Relationship

```
StudentID

↓

Enrollment

↓

CourseID
```

Here we define

Tables

Columns

Relationships

Constraints

Primary Keys

Foreign Keys

* * *

Notice

No discussion about

Disk

Blocks

Pages

Memory

* * *

### Who works here?

Database Designers

Backend Developers

* * *

# Level 3 : View Level

Highest level.

This is what users actually see.

Example

Employee Table

```
ID

Name

Salary

Address

Phone
```

HR should see

```
ID

Name

Salary
```

Receptionist should see

```
ID

Name

Phone
```

Customer

```
Only Name
```

Everyone sees different views.

Same database.

Different visibility.

* * *

## Why View Level?

Security

Simpler interface

Hide confidential information

* * *

## Complete Flow

```
User

↓

View Level

↓

Logical Level

↓

Physical Level

↓

Disk
```

* * *

## Interview Question

If the physical storage changes, should the application change?

No.

Because abstraction hides physical details.

* * *

# 4. What is Schema?

Students confuse schema with database.

They are different.

* * *

Imagine constructing a house.

Before construction

You first prepare

Blueprint.

```
Bedroom

Kitchen

Bathroom

Hall
```

Actual house comes later.

Blueprint = Schema

House = Database

* * *

## Definition

Schema is the **overall design or structure of the database.**

It tells

Which tables exist

Columns

Relationships

Constraints

Data Types

* * *

Example

```
Student

ID INT

Name VARCHAR

Age INT
```

This is schema.

No data yet.

* * *

## Interview Question

Can schema change frequently?

Usually No.

It changes very rarely.

Data changes daily.

* * *

# 5. Instance of Database

Instance means

Current data stored.

Suppose schema

```
Student

ID

Name

Age
```

Morning

```
1 John 20
```

Evening

```
1 John 20

2 Alice 19
```

Schema same.

Instance changed.

* * *

## Difference

Schema

Blueprint

Rarely changes

* * *

Instance

Current snapshot

Changes every second.

* * *

## Interview Question

Which changes more frequently?

Instance.

* * *

# 6. Data Models

Data model defines **how data is represented, organized, and related**.

Think of it as the "style" of organizing data.

* * *

## 1. Relational Model ⭐

Most popular.

Data stored as tables.

Example

Student

|ID|Name|

Course

|CID|Course|

Used by

MySQL

PostgreSQL

Oracle

SQL Server

* * *

## 2. Hierarchical Model

Tree structure.

```
Company

|

HR

|

Employee
```

Each child has one parent.

* * *

## 3. Network Model

One child

Multiple parents.

```
Student

↙      ↘

Course1 Course2
```

Many-to-many relationships are supported directly.

* * *

## 4. Object-Oriented Model

Stores objects instead of only rows.

Example

```
Employee

{

Name

Age

Functions()

}
```

Useful when databases need to store objects similar to object-oriented programming.

* * *

## 5. Entity Relationship (ER) Model

Used during database design.

Example

```
Student

↓

Enrolls

↓

Course
```

Drawn using ER diagrams before creating tables.

* * *

# 7. Database Languages

Database languages are commands used to interact with a database.

* * *

# DDL (Data Definition Language)

Used to define or modify the database structure.

Commands:

* CREATE
* ALTER
* DROP
* TRUNCATE
* RENAME

Example

```SQL
CREATE TABLE Student(
id INT,
name VARCHAR(50)
);
```

This creates the table structure.

* * *

## ALTER

```SQL
ALTER TABLE Student
ADD age INT;
```

Adds a new column.

* * *

## DROP

```SQL
DROP TABLE Student;
```

Deletes the table and its data.

* * *

## DML (Data Manipulation Language)

Used to manipulate the data inside tables.

Commands

INSERT

UPDATE

DELETE

Examples

```SQL
INSERT INTO Student
VALUES(1,'John',20);
```

* * *

```SQL
UPDATE Student
SET age=21
WHERE id=1;
```

* * *

```SQL
DELETE FROM Student
WHERE id=1;
```

* * *

## DQL (Data Query Language)

Used to retrieve data.

Main command

```
SELECT
```

Example

```SQL
SELECT *
FROM Student;
```

* * *

## TCL (Transaction Control Language)

Used to manage transactions.

Commands

```
COMMIT

ROLLBACK

SAVEPOINT
```

* * *

## DCL (Data Control Language)

Controls permissions.

Commands

```
GRANT

REVOKE
```

* * *

## Interview Question

Difference

DDL changes structure.

DML changes data.

DQL retrieves data.

TCL controls transactions.

DCL controls permissions.

* * *

# 8. How SQL Connects to Real Applications

This is one of the most practical interview questions.

Suppose you're building an e-commerce website using:

```
Frontend:
React

Backend:
Node.js

Database:
MySQL
```

Flow:

```
React

↓

HTTP Request

↓

Node.js

↓

SQL Query

↓

MySQL

↓

Node.js

↓

JSON Response

↓

React UI
```

### Example

A user logs in.

Frontend sends:

```JavaScript
POST /login
```

Backend receives:

```JavaScript
const user = await db.query(
  "SELECT * FROM users WHERE email = ?",
  [email]
);
```

The database returns the matching user, the backend verifies the password, then sends the response back to the frontend.

JavaScript **doesn't replace SQL**—it **uses SQL** to communicate with the database.

Another example:

* Instagram: Fetch posts → `SELECT`
* Amazon: Add order → `INSERT`
* Banking: Update balance → `UPDATE`
* Food delivery: Cancel order → `DELETE`

So, SQL is the language used by the backend to store and retrieve data from the database.

* * *

# 9. Database Administrator (DBA)

A **Database Administrator (DBA)** is responsible for managing, securing, maintaining, and optimizing databases.

Think of the DBA as the "manager" of the database.

* * *

## Functions of DBA

### 1. Schema Definition

Design tables, relationships, keys, constraints, and data types.

Example:

Creating `Student`, `Course`, and `Enrollment` tables.

* * *

### 2. Storage Structure and Access Methods

Decide:

* How data is stored.
* Which indexes to create.
* How files are organized.
* Partitioning strategies.

Goal: improve performance.

* * *

### 3. Schema and Physical Organization Modifications

As requirements change, the DBA may:

* Add new tables.
* Remove columns.
* Create indexes.
* Reorganize storage.
* Partition large tables.

Applications should continue working with minimal disruption.

* * *

### 4. Authorization Control

Manage who can access what.

Examples:

* HR can view salaries.
* Students cannot modify grades.
* Admin has full access.

This is done using users, roles, and permissions.

* * *

### 5. Runtime Maintenance

The DBA keeps the database healthy by:

* Taking periodic backups.
* Restoring data after failures.
* Applying security patches.
* Upgrading database software.
* Monitoring performance.
* Managing storage space.
* Tuning slow queries.

* * *

## Interview Question

Is a DBA responsible for writing application code?

Usually **No**.

A DBA focuses on the database itself, while application developers write business logic.

* * *

# 10. DBMS Application Architecture

This explains **how applications communicate with the database**.

* * *

# 1-Tier Architecture

Everything runs on the same machine.

```
User

↓

Application

↓

Database
```

Example

SQLite used by a desktop application.

### Advantages

* Very simple.
* Fast.
* Easy to develop.

### Disadvantages

* Poor security.
* Not suitable for multiple users.
* Limited scalability.

* * *

# 2-Tier Architecture

Client communicates directly with the database.

```
Client

↓

Database
```

Example

A Java desktop application directly connecting to MySQL.

### Advantages

* Faster than three-tier because there's no middle layer.
* Easy to build for small systems.

### Disadvantages

* Database credentials are often stored on the client.
* Harder to maintain.
* Limited scalability.
* Business logic is duplicated across clients.

* * *

# 3-Tier Architecture ⭐ (Most Common)

Used by almost every modern web application.

```
Frontend

↓

Backend Server

↓

Database
```

Example

```
React

↓

Node.js / Spring Boot / Django

↓

MySQL
```

### Advantages

* Better security (database is hidden behind the backend).
* Highly scalable.
* Easier maintenance.
* Centralized business logic.
* Easier authentication and authorization.

### Disadvantages

* More complex.
* Slightly higher latency due to the extra layer.
* Requires more infrastructure.

* * *

## Architecture Comparison

| Feature | 1-Tier | 2-Tier | 3-Tier |
| --- | --- | --- | --- |
| Complexity | Very Low | Low | High |
| Security | Poor | Moderate | Excellent |
| Scalability | Poor | Moderate | Excellent |
| Maintenance | Difficult as apps grow | Moderate | Easy |
| Typical Use | Personal desktop apps | Small business apps | Modern web/mobile applications |

* * *

# Most Asked Interview Questions

1. What is data abstraction, and why is it important?
2. Explain the three levels of DBMS architecture with examples.
3. Differentiate between the physical, logical, and view levels.
4. What is the difference between a schema and a database instance?
5. What is a data model? Name different types.
6. Differentiate DDL, DML, DQL, DCL, and TCL with examples.
7. How does a web application use SQL? Explain the complete request flow from frontend to database.
8. What are the responsibilities of a Database Administrator (DBA)?
9. Compare 1-tier, 2-tier, and 3-tier architectures. Which one is used by modern applications and why?
10. Why does three-tier architecture provide better security than two-tier architecture?

* * *

# Quick Revision (5 Minutes)

* **Abstraction** hides implementation details and presents only the required view.
* **Three-level architecture**: Physical (storage), Logical (tables and relationships), View (user-specific data).
* **Schema** is the database blueprint; an **instance** is the current data stored.
* **Data models** define how data is organized, with the **relational model** being the most widely used.
* **DDL** defines structure, **DML** changes data, **DQL** retrieves data, **TCL** manages transactions, and **DCL** manages permissions.
* In real applications, the **backend** executes SQL queries to communicate with the database on behalf of the frontend.
* A **DBA** designs, secures, optimizes, backs up, and maintains databases.
* **Three-tier architecture** (Frontend → Backend → Database) is the standard architecture for modern web and mobile applications because it offers better security, scalability, and maintainability.

* * *

**You:**

1. what is a data model
2. what is an er model and er diagram
3. what is an entity, its types, entity set, attributes, relationships 
4. types of attributes (simple, composite, single valued, multi valued, derived, null value) and how they are shown in er diagram with example
5. types of relationship (weak, strong, and other types) and how they are shown in er diagram with example
6. degree of relation (unary, binary, ternary)
7. relationship constraints (what is mapping cardinality and one to one one to many  mny to one many to many relationship, participation constraint or minimum cardinality constraint) explain all of them with examples
8. what is participation and types of participations (relationship between weak and strong entity with participation)
9. er notations

* * *

**ChatGPT:**

Excellent. These topics are the **heart of database design**. Almost every interview (especially for freshers) asks at least one ER model question, and many companies give an ER design problem such as:

> "Design a database for a library."
> 
> "Design an ER diagram for an online shopping system."
> 
> "Design a database for a college management system."

If you understand these concepts well, you'll be able to design almost any database.

* * *

# 1. What is a Data Model?

## Simple Definition

A **Data Model** is a blueprint or a set of rules that defines:

* How data is stored
* How data is organized
* How data is related
* How users can access the data

Think of it as **the language or style used to organize a database**.

* * *

## Real-life Analogy

Imagine you're constructing a house.

Before construction, you decide:

* How many rooms?
* Where is the kitchen?
* Where are the doors?
* Where are the windows?

This plan is like a **data model**.

Only after the plan is ready do you start building.

Similarly,

Data Model → Database Design → Actual Database

* * *

## Example

Suppose you're designing a college database.

A data model tells you:

```
Student

StudentID
Name
Age

↓

Enrolls

↓

Course

CourseID
CourseName
Credits
```

This is a model of how data should be organized.

* * *

## Why do we need Data Models?

Without a data model:

* No organization
* No relationships
* Duplicate data
* Difficult queries
* Hard maintenance

* * *

## Types of Data Models

Interviewers usually expect these:

### 1. Conceptual Data Model

High-level.

Only shows major entities and relationships.

Example:

```
Student ---- Enrolls ---- Course
```

No data types.

No keys.

Used while discussing requirements with clients.

* * *

### 2. Logical Data Model

Adds details.

Shows

* Attributes
* Primary Keys
* Foreign Keys
* Relationships

Still independent of a specific DBMS.

* * *

### 3. Physical Data Model

Shows actual implementation.

Includes

* Data types
* Indexes
* Storage details
* Constraints

Example

```SQL
CREATE TABLE Student(
ID INT PRIMARY KEY,
Name VARCHAR(50)
);
```

* * *

# Interview Question

**Difference between Conceptual, Logical, Physical?**

| Conceptual | Logical | Physical |
| --- | --- | --- |
| Business view | Database design | Actual implementation |
| Simple | Detailed | Most detailed |
| No datatypes | Keys & attributes | SQL tables |

* * *

# 2. ER Model and ER Diagram

This is one of the most important topics.

* * *

## What is ER Model?

ER stands for

**Entity Relationship Model**

It is a high-level model used to design databases before implementation.

Instead of writing SQL immediately,

we first understand

* What entities exist?
* How are they related?

* * *

## Why use ER Model?

Suppose a company says:

"We need a Hospital Management System."

Don't start creating tables immediately.

First identify:

* Doctor
* Patient
* Appointment
* Medicine

Then connect them.

That's ER Modeling.

* * *

## ER Diagram

ER Diagram is the **graphical representation** of the ER Model.

It uses symbols.

Example

```
Student -------- Enrolls -------- Course
```

Later we'll draw using ER notation.

* * *

# Interview Question

Difference?

ER Model = Concept

ER Diagram = Picture representing the concept

* * *

# 3. Entity, Entity Types, Entity Set, Attributes, Relationships

These terms confuse many students.

Let's separate them.

* * *

# Entity

An entity is a **real-world object** that can be identified independently.

Examples

Student

Teacher

Employee

Car

Hospital

Bank Account

Book

* * *

### Example

```
Student

ID = 101

Name = John

Age = 20
```

John is an entity.

* * *

# Entity Set

Collection of similar entities.

Example

```
Student Table

101 John

102 Alice

103 Bob
```

Entire collection = Entity Set.

Think

Entity → One object

Entity Set → Collection of objects

* * *

# Types of Entities

## Strong Entity

Can exist independently.

Example

```
Student

Employee

Department
```

Each has its own Primary Key.

Example

StudentID

* * *

## Weak Entity

Cannot exist independently.

Depends on another entity.

Example

```
Employee

↓

Dependent
```

Dependent

* Name
* Age

No unique identity without Employee.

* * *

Interview Question

Can a weak entity exist without a strong entity?

No.

* * *

# Attributes

Attributes describe an entity.

Example

Student

```
ID

Name

Age

Phone
```

Each is an attribute.

* * *

# Relationship

A relationship shows association between entities.

Example

```
Student

↓

Enrolls

↓

Course
```

Student and Course are related through "Enrolls".

* * *

# 4. Types of Attributes

This is a favorite interview question.

* * *

## 1. Simple Attribute

Cannot be divided further.

Examples

Age

Salary

Gender

ER Symbol

⭕ Oval

```
(Student)

   |

 (Age)
```

* * *

## 2. Composite Attribute

Can be divided.

Example

Name

↓

First Name

↓

Middle Name

↓

Last Name

Address

↓

House

↓

Street

↓

City

↓

State

↓

PIN

ER Representation

```
          Name

      /     |      \

 First  Middle  Last
```

Parent attribute connected to child attributes.

* * *

## 3. Single-Valued Attribute

Only one value.

Example

Date of Birth

Gender

Roll Number

One student has one DOB.

* * *

## 4. Multi-Valued Attribute

Multiple values.

Example

Phone Numbers

```
98765

99999

88888
```

One student can have multiple phone numbers.

ER Symbol

⭕ Double Oval

```
((Phone))
```

* * *

## 5. Derived Attribute

Can be calculated.

Example

DOB

↓

Age

Age need not be stored.

Can be calculated.

ER Symbol

Dashed Oval

```
- - Age - -
```

* * *

## 6. Null Attribute

Value is unknown or unavailable.

Example

Middle Name

Many people don't have one.

Passport Number

Not everyone owns a passport.

* * *

Interview Question

Difference between NULL and 0?

NULL = Unknown / Not Available

0 = Actual value

* * *

# Attribute Summary

| Attribute | Example | ER Symbol |
| --- | --- | --- |
| Simple | Age | Single oval |
| Composite | Address | Oval with sub-ovals |
| Single-valued | DOB | Single oval |
| Multi-valued | Phone | Double oval |
| Derived | Age from DOB | Dashed oval |
| Null | Passport Number | Normal oval (NULL is a value state, not a different symbol) |

* * *

# 5. Types of Relationships

Many students mistakenly think "weak" and "strong" are relationship types. **They are actually entity types.** A relationship itself can be identifying or non-identifying, and relationships are also classified by cardinality and degree.

## 1. Identifying Relationship

Used between a **weak entity** and its **strong entity**.

Example:

```
Employee

      |

   Has

      |

Dependent
```

The dependent cannot exist without the employee.

ER notation: **Double diamond**.

* * *

## 2. Non-Identifying Relationship

Used between independent (strong) entities.

Example

```
Student

↓

Enrolls

↓

Course
```

Both exist independently.

ER notation: **Single diamond**.

* * *

## 3. Recursive (Unary) Relationship

Entity related to itself.

Example

```
Employee

↓

Manages

↓

Employee
```

One employee manages another employee.

* * *

## 4. Relationship with Attributes

Sometimes a relationship has its own attributes.

Example

```
Student

↓

Enrollment

↓

Course
```

Enrollment has

```
Enrollment Date

Grade
```

Those attributes belong to the **relationship**, not to either entity.

* * *

# 6. Degree of Relationship

Degree means

**How many entity types participate in a relationship?**

* * *

## Unary Relationship

One entity.

Example

Employee manages Employee.

```
Employee

↓

Manages

↓

Employee
```

* * *

## Binary Relationship

Two entities.

Most common.

```
Student

↓

Enrolls

↓

Course
```

* * *

## Ternary Relationship

Three entities.

Example

```
Doctor

Patient

Medicine
```

Doctor prescribes Medicine to Patient.

All three participate together.

* * *

Interview Question

Which relationship degree is most common?

Binary.

* * *

# 7. Relationship Constraints

Constraints tell us **how entities are allowed to participate in relationships**.

There are two major constraints:

1. Mapping Cardinality (Maximum participation)
2. Participation Constraint (Minimum participation)

* * *

# Mapping Cardinality

Maximum number of entities that can participate.

* * *

## One-to-One (1:1)

One employee gets one locker.

One locker belongs to one employee.

```
Employee ---- Locker
```

* * *

## One-to-Many (1:M)

One department has many employees.

One employee belongs to one department.

```
Department

↓

Employee

Employee

Employee
```

* * *

## Many-to-One (M:1)

Many students belong to one college.

Reverse of one-to-many.

```
Student

Student

Student

↓

College
```

* * *

## Many-to-Many (M:N)

Students enroll in many courses.

Courses have many students.

```
Student

↘     ↙

 Course

↗     ↖

Student
```

This is the most common relationship in real applications and is usually implemented using a junction (bridge) table.

* * *

# Participation Constraint (Minimum Cardinality)

It tells whether participation is **mandatory or optional**.

* * *

## Total Participation (Mandatory)

Every entity **must** participate.

Example

Every Employee must belong to a Department.

No employee exists without a department.

ER notation

**Double Line**

```
Employee
||

Works In

◇

Department
```

* * *

## Partial Participation (Optional)

Some entities may not participate.

Example

Some employees may not manage anyone.

ER notation

**Single Line**

```
Employee

|

Manages

◇

Employee
```

* * *

# 8. Participation and Weak Entity

This is a very common interview question.

Weak entities always have **total participation** in their identifying relationship.

Example

```
Employee

||

Has

◇◇

Dependent
```

Meaning

Every dependent **must** belong to an employee.

But an employee may or may not have dependents.

So:

* Weak Entity → Total Participation
* Strong Entity → Usually Partial Participation (depends on business rules)

* * *

# 9. ER Notations

These are standard symbols you should know.

| Symbol | Meaning |
| --- | --- |
| Rectangle | Strong Entity |
| Double Rectangle | Weak Entity |
| Oval | Attribute |
| Double Oval | Multi-valued Attribute |
| Dashed Oval | Derived Attribute |
| Composite Oval | Composite Attribute (parent oval connected to sub-ovals) |
| Diamond | Relationship |
| Double Diamond | Identifying relationship (for weak entities) |
| Underlined Attribute | Primary Key |
| Dashed Underline | Partial Key (Discriminator of weak entity) |
| Single Line | Partial (Optional) Participation |
| Double Line | Total (Mandatory) Participation |

* * *

# Complete Example

Let's model a simple college system.

```
                (Name)
                   |
              (StudentID)  ← Underlined (Primary Key)
                   |
              +-----------+
              | Student   |
              +-----------+
                    ||
                 Enrolls
                  ◇
                    |
                    |
              +-----------+
              | Course    |
              +-----------+
                   |
              (CourseID)
```

Here:

* **Student** and **Course** are strong entities.
* **Enrolls** is a relationship.
* **StudentID** and **CourseID** are primary keys.
* The **double line** indicates total participation of Student in this example (if every student must enroll in at least one course).

* * *

# High-Frequency Interview Questions

1. What is a data model? Why is it required?
2. Differentiate between conceptual, logical, and physical data models.
3. What is an ER model? Why is it used before creating database tables?
4. Differentiate between an ER model and an ER diagram.
5. What is an entity? How is it different from an entity set?
6. Explain strong and weak entities with examples.
7. Explain all types of attributes and their ER diagram symbols.
8. What is the difference between a simple and composite attribute? Between a single-valued and multi-valued attribute?
9. What is a derived attribute? Why might we avoid storing it?
10. Explain one-to-one, one-to-many, many-to-one, and many-to-many relationships with real-world examples.
11. What is the difference between mapping cardinality and participation constraints?
12. Why does a weak entity require total participation in its identifying relationship?
13. Draw an ER diagram for a Library, College, Hospital, or E-commerce system (a very common practical interview question).

* * *

# Quick Revision (5 Minutes)

* A **data model** defines how data is structured, related, and managed.
* An **ER model** is a conceptual design approach; an **ER diagram** is its graphical representation.
* An **entity** is a real-world object; an **entity set** is a collection of similar entities.
* **Strong entities** have their own primary key; **weak entities** depend on a strong entity and are connected through an **identifying relationship**.
* Attributes can be **simple, composite, single-valued, multi-valued, derived**, or **NULL** (missing/unknown value).
* Relationships are classified by **degree** (unary, binary, ternary) and **cardinality** (1:1, 1:M, M:1, M:N).
* **Participation** tells whether taking part in a relationship is **mandatory (total)** or **optional (partial)**.
* Learn the ER symbols: rectangle, double rectangle, oval, double oval, dashed oval, diamond, double diamond, single line, double line, and underlined primary key—they are frequently tested in interviews.

* * *

**You:**

extended er features
1. what is specialization, where it is used and  how it is used with example
2. what is generalization, where it is used and  how it is used with example
3. attribute inheritance
4. participation inheritance
5. aggregation, where and why it is used and how with example

* * *

**ChatGPT:**

Excellent. **Extended ER (EER) Model** is an extension of the basic ER Model. It adds concepts from **Object-Oriented Programming (OOP)**, such as inheritance and hierarchy, making database design more expressive.

Many interviewers ask these topics because they test whether you understand **real-world database design**, not just tables.

> **Important Interview Tip**
> 
> Students often memorize:
> 
> * Specialization = Top-down
> * Generalization = Bottom-up
> 
> But interviewers usually ask:
> 
> **"Why do we need specialization if we can simply create separate tables?"**
> 
> or
> 
> **"When would you choose generalization over specialization?"**
> 
> So we'll focus on the reasoning as well.

* * *

# What is Extended ER (EER) Model?

Normal ER Model can represent

* Entities
* Attributes
* Relationships

But in real life, objects have

* Different categories
* Common properties
* Parent-child relationships
* Inheritance

Normal ER cannot express these elegantly.

So EER introduces

* Specialization
* Generalization
* Inheritance
* Aggregation

Think of it as

```
ER Model
      +
Object Oriented Concepts
      =
Extended ER (EER)
```

* * *

# 1. Specialization

## Simple Definition

Specialization is the process of dividing **one general entity into multiple specialized entities** based on their characteristics.

It is a **Top-Down approach**.

```
General Entity
      ↓
Specific Entities
```

* * *

## Real-life Example

Suppose we have

```
Employee
```

Every employee has

* Employee ID
* Name
* Salary

But employees can be

* Professor
* Accountant
* Security Guard

Each has additional information.

Professor

* Subject

Accountant

* Tax Department

Security Guard

* Shift Timing

Instead of putting every possible attribute into one table,

we divide Employee.

```
                 Employee
          ----------------------
          EmployeeID
          Name
          Salary
                 |
      -----------------------
      |          |          |
 Professor  Accountant  Security
```

* * *

## Why not keep everything in one table?

Imagine one table

|ID|Name|Salary|Subject|Shift|TaxDept|

Professor rows

```
Subject = DBMS

Shift = NULL

TaxDept = NULL
```

Security rows

```
Subject = NULL

Shift = Night

TaxDept = NULL
```

Lots of NULL values.

Very poor design.

Specialization avoids this.

* * *

## Where is it used?

Hospital

```
Employee

↓

Doctor

Nurse

Receptionist
```

University

```
Person

↓

Student

Teacher

Staff
```

Bank

```
Account

↓

Savings

Current

Loan
```

* * *

## Interview Question

### Why do we use specialization?

Answer:

* Reduce NULL values
* Better organization
* Easier maintenance
* Separate entity-specific attributes
* Closer representation of the real world

* * *

# How is it represented?

```
           Employee

               |

               O

      -----------------

      |               |

 Professor        Accountant
```

Circle represents specialization.

* * *

# Types of Specialization

Interviewers sometimes ask this.

## Disjoint Specialization

One entity belongs to only one subclass.

Example

Employee

↓

Professor

OR

Security

Not both.

* * *

## Overlapping Specialization

One entity can belong to multiple subclasses.

Example

Teacher

↓

Professor

↓

Researcher

A person can be both.

* * *

## Total Specialization

Every parent entity must belong to some subclass.

Every employee is either

Professor

or

Security

or

Accountant.

* * *

## Partial Specialization

Some employees may remain just "Employee."

* * *

# 2. Generalization

Exactly opposite.

* * *

## Definition

Generalization combines multiple similar entities into one generalized entity.

Bottom-Up approach.

```
Specific Entities

↓

General Entity
```

* * *

## Example

Suppose database has

```
Car

Bike

Truck
```

All have

* Registration Number
* Color
* Manufacturer

Instead of repeating these attributes,

Create

```
Vehicle

↓

Car

Bike

Truck
```

Vehicle stores common attributes.

Subclasses store only unique attributes.

* * *

Another Example

```
Dog

Cat

Cow
```

↓

Animal

* * *

## Why use Generalization?

Avoid repeated attributes.

Better organization.

Less redundancy.

Easy maintenance.

* * *

## Interview Question

Difference?

| Specialization | Generalization |
| --- | --- |
| Top Down | Bottom Up |
| Divide entity | Combine entities |
| Parent → Child | Child → Parent |
| Used when subclasses differ | Used when entities share common features |

* * *

# 3. Attribute Inheritance

This concept comes from OOP.

* * *

Suppose

```
Vehicle

↓

Car
```

Vehicle has

```
VehicleID

Color

Manufacturer
```

Car has

```
Seats
```

Does Car have Color?

Yes.

Even if we don't write it again.

Why?

Inheritance.

* * *

Car automatically inherits

```
VehicleID

Manufacturer

Color
```

and additionally has

```
Seats
```

* * *

Example

```
Person

↓

Student
```

Person

```
Name

DOB

Gender
```

Student

```
Roll Number
```

Student automatically gets

```
Name

DOB

Gender
```

* * *

## Interview Question

Do we duplicate inherited attributes?

No.

They are inherited logically.

* * *

# 4. Participation Inheritance

This is a topic students often find confusing.

Let's understand it carefully.

* * *

Suppose

```
Employee

↓

Works In

↓

Department
```

Every employee works in one department.

Now specialize Employee.

```
Employee

↓

Professor

↓

Assistant Professor
```

Does Professor also work in Department?

Yes.

Because participation is inherited.

* * *

Meaning

If parent entity participates in a relationship,

child entities automatically participate.

* * *

Example

```
Vehicle

↓

Owner
```

Relationship

```
Vehicle

Owned By

Person
```

Now

Vehicle specialized into

```
Car

Bike
```

Do Car and Bike have owners?

Yes.

Relationship inherited.

* * *

Interview Question

Can subclasses participate in additional relationships?

Absolutely.

Example

Professor

↓

Teaches

↓

Course

Employee doesn't teach.

Only Professor.

* * *

# 5. Aggregation

This is one of the trickiest EER concepts.

Most students memorize it without understanding.

Let's simplify it.

* * *

## Problem

Normal ER allows

Entity ↔ Relationship

But sometimes we need

Relationship ↔ Relationship

ER Model doesn't allow this directly.

Aggregation solves it.

* * *

## Definition

Aggregation is a technique where a **relationship is treated as a higher-level entity** so that it can participate in another relationship.

Think of it as:

> **"Treat a relationship as if it were an entity."**

* * *

## Real-life Example

Suppose

```
Employee

↓

Works On

↓

Project
```

Now Manager supervises this work.

Question

Manager supervises whom?

Employee?

No.

Project?

No.

Manager supervises

**Employee working on Project.**

Meaning

Manager supervises the relationship

```
Employee

Works On

Project
```

* * *

Without aggregation

Impossible.

* * *

Using aggregation

```
Employee

↓

Works On

↓

Project

     |

 (Treat as Entity)

     |

Supervised By

     |

Manager
```

* * *

## Another Example

University

```
Student

↓

Enrolls

↓

Course
```

Now

Instructor evaluates this enrollment.

Instructor is not evaluating Student alone.

Not Course alone.

Instructor evaluates

Student enrolled in Course.

Again,

Relationship becomes an entity.

* * *

## Why Aggregation?

Because sometimes

Relationship itself has meaning.

We want another entity to interact with that relationship.

* * *

## Where is it used?

Project Management

```
Employee

Works On

Project

↓

Manager supervises
```

University

```
Student

Enrolls

Course

↓

Professor evaluates
```

Hospital

```
Doctor

Treats

Patient

↓

Insurance approves treatment
```

Insurance approves

Treatment

Not doctor alone.

Not patient alone.

* * *

## ER Representation

Normally

```
Employee

◇ Works On

Project
```

Aggregation

Draw a **box around the relationship and the participating entities**.

```
+----------------------------+
| Employee ◇ WorksOn Project |
+----------------------------+
              |
        Supervises
              |
           Manager
```

The boxed portion behaves like a single higher-level entity in another relationship.

* * *

# Complete Comparison

| Feature | Specialization | Generalization | Aggregation |
| --- | --- | --- | --- |
| Approach | Top-down | Bottom-up | Relationship abstraction |
| Purpose | Create subclasses | Create superclass | Treat relationship as entity |
| Uses Inheritance | Yes | Yes | No |
| Main Goal | Divide entities | Combine entities | Model relationship between relationships |
| Example | Employee → Professor | Car + Bike → Vehicle | Manager supervises Employee working on Project |

* * *

# Interview Flow

Interviewer:

> What is specialization?

↓

Why not simply create separate tables?

↓

Difference between specialization and generalization?

↓

Can subclasses inherit attributes?

↓

Can subclasses inherit relationships?

↓

What is aggregation?

↓

Why can't we solve aggregation using ordinary relationships?

↓

Give a real-world example.

* * *

# High-Frequency Interview Questions

### Basic

1. What is an Extended ER Model?
2. Why do we need EER when ER already exists?
3. Explain specialization with an example.
4. Explain generalization with an example.
5. What is attribute inheritance?
6. What is participation inheritance?
7. What is aggregation?

* * *

### Intermediate

8. Difference between specialization and generalization.
9. What is total specialization?
10. What is partial specialization?
11. What is disjoint specialization?
12. What is overlapping specialization?

* * *

### Advanced

13. Why does specialization reduce NULL values?
14. Can subclasses have additional relationships not present in the superclass?
15. Why can't ordinary ER diagrams model relationship-to-relationship interactions?
16. Explain aggregation with a real-world system like a hospital, university, or project management.

* * *

# Quick Revision (5 Minutes)

* **Specialization** is a **top-down** process that splits a general entity into more specific entities to avoid NULL values and better model real-world differences.
* **Generalization** is a **bottom-up** process that combines similar entities into a common superclass to reduce redundancy.
* **Attribute inheritance** means subclasses automatically inherit the attributes of their superclass.
* **Participation inheritance** means subclasses also inherit the relationships in which the superclass participates, though they may have additional relationships of their own.
* **Aggregation** treats a **relationship as a higher-level entity** so that another relationship can involve it. It's used when you need to model interactions with the relationship itself, such as a manager supervising an employee's work on a project.

* * *

## One Interview Correction to Remember

Many textbooks and students say:

> "Relationship types are **strong** and **weak**."

This is **not technically correct**.

* **Strong** and **weak** describe **entities**, not relationships.
* Relationships are better classified as **identifying vs non-identifying**, by **cardinality (1:1, 1:M, M:N)**, by **degree (unary, binary, ternary)**, and by **participation (total/partial)**.

Knowing this distinction can help you stand out in interviews because it shows conceptual clarity rather than rote memorization.

* * *

**You:**

steps to make er diagram
1. identify empty sets
2. identify attributes and their types
3. identify relation and constraints, mapping, participation

* * *

**ChatGPT:**

This is one of the most important practical topics because interviewers often don't ask theory directly. Instead, they'll say:

> **"Design an ER diagram for a Library Management System."**
> 
> or
> 
> **"Draw an ER diagram for an E-commerce Website."**

If you know the **step-by-step process**, you can design **any ER diagram**, even if you've never seen that problem before.

* * *

# Steps to Make an ER Diagram

Think of it like building a house.

You don't start by painting walls.

You first identify:

* What objects exist?
* What information about them is needed?
* How are they connected?

Exactly the same process is followed in ER modeling.

* * *

# Step 1: Read the Problem Carefully

Never start drawing immediately.

Read the problem 2–3 times.

Example

> "A college has many students. Students enroll in courses. Teachers teach courses."

Don't think about rectangles and diamonds yet.

First understand the business.

* * *

# Step 2: Identify the Entities (Entity Sets)

## What is an Entity?

Ask yourself:

> **What are the main objects or nouns in the problem?**

Usually nouns become entities.

Example

> "Students borrow books from the library."

Nouns are

* Student
* Book
* Library

But should every noun become an entity?

No.

Some nouns are relationships.

For example,

"Borrow"

is an action.

Not an entity.

* * *

### Example

Problem

> Customers place orders.

Entities

```
Customer
Order
```

Relationship

```
Places
```

* * *

## Interview Trick

Sometimes interviewers purposely include unnecessary nouns.

Example

"A student writes an exam using a pen."

Entities?

Student

Exam

Pen?

Usually **Pen is not an entity** because the system is not storing information about pens.

Always ask:

> Does the system need to store information about this object?

If **Yes → Entity**

If **No → Ignore**

* * *

# Step 3: Identify Attributes and Their Types

Once entities are identified,

find information describing each entity.

Ask:

> What information should I store about this object?

* * *

## Example

Student

```
StudentID
Name
Age
Email
Phone
DOB
```

Book

```
BookID
Title
Author
Price
Publisher
```

* * *

## Now classify attributes

Interviewers love this.

* * *

### Primary Key

Unique identifier.

Student

```
StudentID
```

Underline it.

* * *

### Composite Attribute

Can be divided.

Example

Name

↓

First Name

Middle Name

Last Name

Address

↓

House

Street

City

PIN

* * *

### Multi-valued Attribute

Student

↓

Phone Numbers

A student may have

98765

99887

77889

Double Oval

* * *

### Derived Attribute

DOB

↓

Age

Age is calculated.

Dashed Oval

* * *

### Nullable Attribute

Passport Number

Middle Name

These may not exist.

* * *

## Interview Tip

If Age is stored,

Interviewer may ask

> Why not store DOB instead?

Answer

Because

Age changes every year.

DOB never changes.

Age can always be calculated.

* * *

# Step 4: Identify Relationships

Ask

How are entities connected?

Usually verbs indicate relationships.

Example

Student

**Enrolls**

Course

Teacher

**Teaches**

Course

Customer

**Places**

Order

Doctor

**Treats**

Patient

* * *

Example

```
Student

↓

Enrolls

↓

Course
```

* * *

# Step 5: Determine Relationship Constraints

This is where most students lose marks.

After finding relationships,

ask two questions.

* * *

## Question 1

How many?

(Mapping Cardinality)

* * *

## One-to-One

One person

One passport

```
Person

↓

Has

↓

Passport
```

* * *

## One-to-Many

One department

Many employees

```
Department

↓

Employee

Employee

Employee
```

* * *

## Many-to-One

Many employees

↓

Department

Reverse of previous.

* * *

## Many-to-Many

Students

↓

Enroll

↓

Courses

Many students

Many courses

* * *

## Interview Tip

Whenever you see words like

> "many"

or

> "multiple"

Think

Many-to-Many.

* * *

# Step 6: Determine Participation

Now ask

Is participation compulsory?

* * *

## Total Participation

Every entity must participate.

Example

Every employee must belong to a department.

Double Line

* * *

## Partial Participation

Some entities may participate.

Others may not.

Example

Some professors supervise projects.

Some don't.

Single Line.

* * *

# Step 7: Check Weak Entities

Ask

Can this entity exist independently?

Example

Employee

↓

Dependent

Dependent cannot exist alone.

Weak Entity.

Double Rectangle.

Relationship

Double Diamond.

* * *

# Step 8: Check for Specialization / Generalization

Ask

Can an entity be divided?

Example

Employee

↓

Professor

↓

Security

↓

Accountant

Use specialization.

* * *

Or

Car

Bike

Truck

↓

Vehicle

Generalization.

* * *

# Step 9: Check Relationship Attributes

Sometimes attributes belong to relationships.

Example

Student

↓

Enrolls

↓

Course

Enrollment has

Enrollment Date

Grade

These belong to the relationship "Enrolls", not to Student or Course.

* * *

# Step 10: Draw Using Correct ER Notations

Now finally draw.

Use

Rectangle

↓

Entities

Oval

↓

Attributes

Diamond

↓

Relationships

Double Rectangle

↓

Weak Entity

Double Diamond

↓

Identifying Relationship

Underlined Attribute

↓

Primary Key

Double Oval

↓

Multi-valued

Dashed Oval

↓

Derived

Single/Double Lines

↓

Participation

* * *

# Complete Example

Let's solve one from scratch.

## Problem

> A student enrolls in courses.
> 
> Every course is taught by one teacher.
> 
> Students have ID, Name, Phone Numbers.
> 
> Phone numbers can be multiple.
> 
> Age is calculated from DOB.

* * *

## Step 1

Entities

```
Student

Course

Teacher
```

* * *

## Step 2

Attributes

Student

```
StudentID (PK)

Name

DOB

Age (Derived)

Phone (Multi-valued)
```

Course

```
CourseID

CourseName
```

Teacher

```
TeacherID

TeacherName
```

* * *

## Step 3

Relationships

```
Student

↓

Enrolls

↓

Course
```

```
Teacher

↓

Teaches

↓

Course
```

* * *

## Step 4

Mapping

Student ↔ Course

Many-to-Many

Teacher ↔ Course

One-to-Many

One teacher teaches many courses.

One course has one teacher.

* * *

## Step 5

Participation

Every course must have a teacher.

Total Participation.

Students may not enroll immediately.

Partial Participation.

* * *

## Final ER Diagram (Text Representation)

```
                  (Phone)
                ((     ))
                     |
                 (Name)
                     |
          --------Student--------
         |      StudentID       |
         |         DOB          |
         |   - - Age - -        |
          ----------------------
                  ||
                  ||
              ◇ Enrolls ◇
               /        \
              /          \
             /            \
     --------Course---------
    | CourseID            |
    | CourseName          |
     ----------------------
             ||
             ||
          ◇ Teaches ◇
             ||
             ||
     -------Teacher--------
    | TeacherID           |
    | TeacherName         |
     ----------------------
```

* **StudentID, CourseID, TeacherID** → Primary Keys (underlined in a real ER diagram).
* **Phone** → Multi-valued attribute (double oval).
* **Age** → Derived attribute (dashed oval).
* **Enrolls** → Many-to-Many relationship.
* **Teaches** → One-to-Many relationship (Teacher → Course).
* **Double lines** indicate total participation where required.

* * *

# How Interviewers Think

Suppose they ask:

> Design an ER Diagram for Amazon.

They expect this thought process:

### Step 1

Find Entities

```
Customer

Product

Order

Payment

Seller
```

* * *

### Step 2

Attributes

Customer

```
CustomerID

Name

Phone
```

* * *

### Step 3

Relationships

```
Customer

Places

Order

Order

Contains

Product

Seller

Sells

Product
```

* * *

### Step 4

Mapping

Customer → Order

One-to-Many

Order → Product

Many-to-Many

Seller → Product

One-to-Many

* * *

### Step 5

Participation

Can Product exist without Seller?

Can Order exist without Customer?

Think about business rules.

* * *

# Common Mistakes Students Make

### ❌ Mistake 1

Making every noun an entity.

Wrong.

Only create entities for objects whose data the system must store.

* * *

### ❌ Mistake 2

Treating actions as entities.

Wrong

Borrow

Purchase

Enroll

These are usually relationships.

* * *

### ❌ Mistake 3

Not identifying Primary Keys.

Every strong entity should have one.

* * *

### ❌ Mistake 4

Ignoring cardinality.

Interviewers almost always ask:

> Is it One-to-Many or Many-to-Many?

* * *

### ❌ Mistake 5

Ignoring participation.

Can an entity exist without the relationship?

Always think about mandatory vs optional participation.

* * *

# Universal Algorithm for Any ER Diagram

Whenever you see an ER design question, remember this checklist:

1. **Read the problem** carefully.
2. **Identify entities** (important nouns whose data must be stored).
3. **Identify attributes** for each entity.
4. **Classify attributes** (primary key, composite, multi-valued, derived, nullable).
5. **Identify relationships** (usually verbs connecting entities).
6. **Determine mapping cardinality** (1:1, 1:M, M:1, M:N).
7. **Determine participation** (total or partial).
8. **Check for weak entities** and identifying relationships.
9. **Look for specialization/generalization** if entities naturally form a hierarchy.
10. **Check for relationship attributes** and **aggregation** if needed.
11. **Draw the diagram using standard ER notations**.

If you follow these steps consistently, you can design ER diagrams for **Library Management**, **Hospital**, **Bank**, **College**, **Railway Reservation**, **Food Delivery**, **E-commerce**, or almost any other domain, even if you haven't practiced that exact example before.

* * *

**You:**

1. what is relational model, degree of attributes, cardinality, relational schema, relational key
2. relational keys (super key, candidate key, primary key, alternate key, foreign key, composite key, compound key, surrogate key) explain them what thry are, their functions, with examples, where they are used, rules for them
3. integrity constraints (crud operation must be done with some integrity policy so that db is always consistent, introduced so that we dont corrupt the db, domain constraints, entitty constraints)
4. referential constraints (insert constraint, delete constraint, and other constraints)
5. referencing table and referenced table
6. on delete cascade, on delete null
7. key constraints (not null, unique constraint, default constraint,  check constraint, primary key constraint, foreign key constraint)

* * *

**ChatGPT:**

Excellent. This is **the most important DBMS topic for interviews**.

If I had to rank DBMS topics by interview frequency, it would be:

1. **Keys (Most Asked ⭐⭐⭐⭐⭐)**
2. **Normalization**
3. **Transactions (ACID)**
4. **Indexing**
5. **Joins**
6. **Constraints**

Companies from TCS to Google ask about keys because **everything in a relational database revolves around them**.

Let's learn this like an interview.

* * *

# 1. What is the Relational Model?

Before understanding keys, understand why the relational model exists.

* * *

## History

Before relational databases, data was stored using:

* Hierarchical Model
* Network Model

Problems:

* Complex relationships
* Difficult querying
* Hard maintenance

In 1970, Edgar F. Codd proposed the **Relational Model**, which became the foundation of modern relational databases.

Today databases like

* MySQL
* PostgreSQL
* Oracle Database
* Microsoft SQL Server

are based on it.

* * *

# Definition

The Relational Model stores data in the form of **relations (tables).**

Each table contains

Rows

↓

Records

Columns

↓

Attributes

Example

Student

| StudentID | Name | Age |
| --- | --- | --- |
| 101 | John | 20 |
| 102 | Alice | 19 |

This table itself is called a **Relation**.

* * *

## Why "Relational"?

Because tables are related.

Example

Student

| StudentID | Name |
| --- | --- |
| 101 | John |

Course

| CourseID | Course |
| --- | --- |
| 1 | DBMS |

Enrollment

| StudentID | CourseID |
| --- | --- |
| 101 | 1 |

Enrollment creates the relationship.

* * *

# Important Terminologies

## Relation

A table.

Example

Student table.

* * *

## Tuple

One row.

```
101 John 20
```

One tuple.

* * *

## Attribute

One column.

```
StudentID

Name

Age
```

Each column is an attribute.

* * *

# Degree

Interviewers ask this often.

Degree = Number of attributes (columns).

Example

|ID|Name|Age|Phone|

Number of columns = 4

Degree = 4

* * *

# Cardinality

Cardinality = Number of tuples (rows).

Example

| ID | Name |
| --- | --- |
| 1 | John |
| 2 | Alice |
| 3 | Bob |

Rows = 3

Cardinality = 3

* * *

## Interview Trick

Students confuse these.

| Degree | Cardinality |
| --- | --- |
| Columns | Rows |

Easy trick

**Degree grows horizontally.**

**Cardinality grows vertically.**

* * *

# Relational Schema

Schema = Structure of a relation.

Example

```
Student(
StudentID,
Name,
Age
)
```

This defines

* table name
* attributes
* data types (in implementation)
* constraints

No actual data.

* * *

# Relation Instance

Current data.

Morning

|ID|Name|

1 John

Evening

|ID|Name|

1 John

2 Alice

Schema same.

Instance changed.

* * *

# Relational Keys

Keys uniquely identify records and establish relationships between tables.

Without keys,

The database cannot guarantee correctness.

* * *

# 2. Relational Keys

Think of keys as identity cards.

Every person may have

Name

Age

City

But

Aadhaar Number uniquely identifies them.

Database keys serve the same purpose.

* * *

# Super Key

## Definition

A Super Key is **any set of one or more attributes that can uniquely identify a row.**

Example

Student

|ID|Email|Phone|Name|

Possible Super Keys

```
ID

Email

Phone

ID + Name

Email + Name

ID + Email

ID + Phone

ID + Email + Phone
```

All uniquely identify a student.

* * *

## Why?

Because uniqueness is preserved even if extra unnecessary attributes are added.

* * *

## Interview Question

Can Super Key contain unnecessary attributes?

Yes.

Example

```
ID + Name
```

Name unnecessary.

Still Super Key.

* * *

# Candidate Key

Definition

A Candidate Key is a **minimal Super Key**.

Minimal means

Remove any attribute

↓

Uniqueness disappears.

* * *

Example

Student

|ID|Email|Phone|

Each is unique.

Candidate Keys

```
ID

Email

Phone
```

Not

```
ID + Email
```

because ID alone is enough.

* * *

## Function

Possible choices for the Primary Key.

* * *

# Primary Key ⭐⭐⭐⭐⭐

Most important key.

Definition

One Candidate Key selected to uniquely identify every row.

Example

```SQL
Student(
StudentID PRIMARY KEY,
Name,
Age
)
```

* * *

## Rules

Must be unique.

Cannot be NULL.

One table has only one Primary Key (though it can consist of multiple columns).

Should rarely change.

* * *

## Function

* Unique identification
* Prevent duplicates
* Used by foreign keys
* Speeds indexing (in many DBMSs)

* * *

Interview Question

Can Primary Key be NULL?

Never.

* * *

# Alternate Key

Remaining Candidate Keys.

Example

Candidate Keys

```
ID

Email

Phone
```

Choose

ID

↓

Primary Key

Remaining

Email

Phone

↓

Alternate Keys

* * *

## Function

Alternative unique identifiers.

* * *

# Foreign Key ⭐⭐⭐⭐⭐

One of the most important concepts.

Definition

A Foreign Key is an attribute in one table that refers to the Primary Key of another table.

* * *

Example

Student

|ID|Name|

101 John

Course

|CourseID|

1 DBMS

Enrollment

|StudentID|CourseID|

101 1

StudentID

↓

Foreign Key

CourseID

↓

Foreign Key

* * *

## Why?

Connect tables.

Prevent invalid references.

* * *

## Interview Question

Can Foreign Key contain duplicates?

Yes.

Many students can belong to the same department, so duplicate foreign key values are allowed.

* * *

Can Foreign Key be NULL?

Yes, unless constrained with `NOT NULL`.

* * *

# Composite Key

A key made using multiple attributes because **no single attribute is sufficient**.

Example

Enrollment

|StudentID|CourseID|

Neither alone is unique.

Together

```
StudentID + CourseID
```

becomes the Primary Key.

* * *

# Compound Key

Many interviewers use **Composite Key** and **Compound Key** interchangeably.

Technically, a **compound key** is a composite key formed from **two or more attributes**, often where each attribute could be a foreign key from different tables.

Example

Enrollment

StudentID

CourseID

Compound Key.

For interviews, if asked, you can mention:

> "In most DBMS discussions, compound key and composite key are used interchangeably."

* * *

# Surrogate Key

Artificial key.

No business meaning.

Usually Auto Increment.

Example

```
CustomerID

1

2

3

4
```

Generated by DBMS.

* * *

## Why?

Suppose

Email

used as Primary Key.

Customer changes email.

Now every related table needs updating.

Bad.

Instead

```
CustomerID
```

Never changes.

* * *

## Real-world Examples

Instagram

UserID

Amazon

OrderID

Uber

RideID

All are surrogate keys.

* * *

# Key Summary

| Key | Unique | NULL Allowed | Purpose |
| --- | --- | --- | --- |
| Super Key | Yes | Depends | Uniquely identify rows (may contain extra attributes) |
| Candidate Key | Yes | No | Minimal unique key |
| Primary Key | Yes | No | Main identifier |
| Alternate Key | Yes | No | Candidate key not chosen as primary |
| Foreign Key | Usually No | Yes (unless restricted) | Relates tables |
| Composite/Compound Key | Yes | Depends on role | Multiple attributes together form a key |
| Surrogate Key | Yes | No | Artificial identifier |

* * *

# 3. Integrity Constraints

## Why are constraints needed?

Imagine a bank.

Without constraints,

Someone inserts

```
Balance = -100000
```

or

```
Age = -5
```

Database becomes invalid.

Constraints protect consistency.

* * *

## Definition

Integrity Constraints are rules that ensure the database remains **accurate, valid, and consistent** during **CRUD operations**.

CRUD

Create

Read

Update

Delete

Constraints mainly affect Create, Update, and Delete.

* * *

# Domain Constraint

Each attribute has a valid domain.

Example

Age

Allowed

0–120

Reject

```
Age = -10
```

Salary

Must be positive.

Gender

Only

Male

Female

Other

* * *

## Implemented using

* Data types
* CHECK
* ENUM (database-dependent)

* * *

# Entity Integrity Constraint

Primary Key

Must

Be Unique

Never NULL

Example

Wrong

|ID|Name|

NULL John

Invalid.

* * *

# 4. Referential Integrity Constraint

The most important constraint after the primary key.

Definition

A Foreign Key value must either:

* Match an existing Primary Key value in the referenced table, or
* Be NULL (if allowed).

* * *

Example

Student

|ID|

101

102

Enrollment

|StudentID|

101

103 ❌

103 doesn't exist.

Insertion rejected.

* * *

## Insert Constraint

Cannot insert a child record if the parent doesn't exist.

Wrong

Enrollment

StudentID = 999

Student table has no 999.

Rejected.

* * *

## Update Constraint

Suppose

StudentID

101

↓

Updated to

105

Enrollment still contains

101

Broken reference.

DBMS prevents this or updates child rows depending on the configured action (`ON UPDATE CASCADE`, etc.).

* * *

## Delete Constraint

Parent deleted.

Student

101

Enrollment still has

101

Invalid.

DBMS prevents or handles this according to the configured delete rule.

* * *

# 5. Referencing Table vs Referenced Table

This is asked surprisingly often.

Example

Student

|StudentID|

101

Enrollment

|StudentID|

101

Student

↓

Has Primary Key

Referenced Table

Enrollment

↓

Contains Foreign Key

Referencing Table

Easy trick:

**Referenced Table → Owns the Primary Key**

**Referencing Table → Stores the Foreign Key**

* * *

# 6. ON DELETE CASCADE and ON DELETE SET NULL

Suppose

Student

|ID|

101

Enrollment

|StudentID|

101

* * *

# ON DELETE CASCADE

Delete Student

↓

Automatically delete all related Enrollment rows.

Example

Before

Student

101

Enrollment

101

After

Student

(empty)

Enrollment

(empty)

* * *

## Used when

Child data has no meaning without the parent.

Examples

* Order → Order Items
* Blog → Comments
* Customer → Customer Addresses (depending on design)

* * *

# ON DELETE SET NULL

Delete Student

↓

Enrollment remains.

Foreign Key becomes NULL.

Before

Enrollment

StudentID

101

After

Enrollment

StudentID

NULL

* * *

## Used when

Child data can exist without the parent.

Example

Employee leaves the company.

Tasks remain.

EmployeeID becomes NULL until reassigned.

* * *

## Other Common Delete Behaviors

### RESTRICT / NO ACTION (Default in many databases)

Parent cannot be deleted if child records exist.

Example

Cannot delete a customer while orders still reference that customer.

* * *

# 7. Key Constraints

These are SQL constraints.

* * *

# NOT NULL

Column cannot store NULL.

Example

```SQL
Name VARCHAR(100) NOT NULL
```

* * *

# UNIQUE

No duplicate values.

Example

Email.

Two users cannot share the same email.

Unlike a primary key, many databases allow multiple `NULL` values in a `UNIQUE` column (database-specific behavior).

* * *

# DEFAULT

Provides a value if none is supplied.

Example

```SQL
Status VARCHAR(20) DEFAULT 'Pending'
```

Insert

```SQL
INSERT INTO Orders(id)
VALUES(1);
```

Status automatically becomes

Pending.

* * *

# CHECK

Validates values.

Example

```SQL
CHECK (Age>=18)
```

Age

16

Rejected.

* * *

# PRIMARY KEY

Combination of

UNIQUE

NOT NULL

Example

```SQL
StudentID INT PRIMARY KEY
```

* * *

# FOREIGN KEY

Maintains relationships.

Example

```SQL
StudentID INT,
FOREIGN KEY(StudentID)
REFERENCES Student(StudentID)
```

Ensures every `StudentID` in the child table exists in the parent table (unless NULL is allowed).

* * *

# Constraint Summary

| Constraint | Purpose | Example |
| --- | --- | --- |
| NOT NULL | Prevent missing values | Name |
| UNIQUE | Prevent duplicates | Email |
| DEFAULT | Provide default value | Status = 'Pending' |
| CHECK | Restrict valid values | Age ≥ 18 |
| PRIMARY KEY | Unique row identifier | StudentID |
| FOREIGN KEY | Maintain relationships | StudentID referencing Student |

* * *

# Most Asked Interview Questions

### Keys

1. Difference between Super Key and Candidate Key.
2. Difference between Candidate Key and Primary Key.
3. Difference between Primary Key and Unique Constraint.
4. Can a table have multiple Candidate Keys?
5. Can a table have multiple Primary Keys?
6. Can a Foreign Key be NULL?
7. Can a Foreign Key contain duplicate values?
8. Why do modern databases prefer surrogate keys over natural keys?

### Constraints

9. What are integrity constraints?
10. Difference between entity integrity and referential integrity.
11. What happens if you insert a foreign key value that doesn't exist?
12. Explain `ON DELETE CASCADE` vs `ON DELETE SET NULL`.
13. Difference between the referencing table and the referenced table.
14. Difference between `UNIQUE` and `PRIMARY KEY`.
15. Why are `CHECK` constraints better than validating everything in application code?

* * *

# Quick Revision (5 Minutes)

* The **Relational Model** stores data in **tables (relations)** made up of **rows (tuples)** and **columns (attributes)**.
* **Degree** = number of columns; **Cardinality** = number of rows.
* A **schema** defines the table structure, while an **instance** is the current data.
* **Super Keys** uniquely identify rows; **Candidate Keys** are minimal super keys; one candidate key is chosen as the **Primary Key**; the remaining candidate keys become **Alternate Keys**.
* A **Foreign Key** connects tables and enforces **referential integrity**.
* **Composite (compound) keys** use multiple columns together, while **surrogate keys** are artificial identifiers (such as auto-increment IDs).
* **Integrity constraints** ensure the database remains valid during insert, update, and delete operations.
* The **referenced table** contains the primary key, while the **referencing table** contains the foreign key.
* `ON DELETE CASCADE` removes related child rows automatically, whereas `ON DELETE SET NULL` preserves child rows but clears the foreign key.
* Common SQL constraints are `NOT NULL`, `UNIQUE`, `DEFAULT`, `CHECK`, `PRIMARY KEY`, and `FOREIGN KEY`, each enforcing a different rule to keep the database consistent.

* * *

**You:**

1. what is sql and diff between sql and mysql
2. what is rdbms
3. sql data types (why varchar over char, advanced dt like json)
4. type of sql commands -> ddl (create, alter table, drop, truncate, rename), dql (select), dml (insert, update, delete), dcl (grant, revoke), tcl(start transaction, commit, rollback, savepoint)
5. common sql commands (MANAGING DB (DDL)
1. Creation of DB
1. CREATE DATABASE IF NOT EXISTS db-name;
2. USE db-name; //need to execute to choose on which DB CREATE TABLE etc commands will be executed.
//make switching between DBs possible.
3. DROP DATABASE IF EXISTS db-name; //dropping database.
4. SHOW DATABASES; //list all the DBs in the server.
5. SHOW TABLES; //list tables in the selected DB.
DECIMAL Double stored as string
DATE YYYY-MM-DD
DATETIME YYYY-MM-DD HH:MM:SS
TIMESTAMP YYYYMMDDHHMMSS
TIME HH:MM:SS
ENUM One of the preset values
SET One or many of the preset values
BOOLEAN 0/1
BIT e.g., BIT(n), n upto 64, store values in bits.
DATATYPE Description

DATA RETRIEVAL LANGUAGE (DRL)
1. Syntax: SELECT <set of column names> FROM <table_name>;
2. Order of execution from RIGHT to LEFT.
3. Q. Can we use SELECT keyword without using FROM clause?
1. Yes, using DUAL Tables.
2. Dual tables are dummy tables created by MySQL, help users to do certain obvious actions without referring to user
defined tables.
3. e.g., SELECT 55 + 11;
SELECT now();
SELECT ucase(); etc.
4. WHERE
1. Reduce rows based on given conditions.
2. E.g., SELECT * FROM customer WHERE age > 18;
5. BETWEEN
1. SELECT * FROM customer WHERE age between 0 AND 100;
2. In the above e.g., 0 and 100 are inclusive.
6. IN
1. Reduces OR conditions;
2. e.g., SELECT * FROM officers WHERE officer_name IN ('Lakshay', ‘Maharana Pratap', ‘Deepika’);
7. AND/OR/NOT
1. AND: WHERE cond1 AND cond2
2. OR: WHERE cond1 OR cond2
3. NOT: WHERE col_name NOT IN (1,2,3,4);
8. IS NULL
1. e.g., SELECT * FROM customer WHERE prime_status is NULL;
9. Pattern Searching / Wildcard (‘%’, ‘_’)
1. ‘%’, any number of character from 0 to n. Similar to ‘*’ asterisk in regex.
2. ‘_’, only one character.
3. SELECT * FROM customer WHERE name LIKE ‘%p_’;
10. ORDER BY
1. Sorting the data retrieved using WHERE clause.
2. ORDER BY <column-name> DESC;
3. DESC = Descending and ASC = Ascending
4. e.g., SELECT * FROM customer ORDER BY name DESC;
11. GROUP BY
1. GROUP BY Clause is used to collect data from multiple records and group the result by one or more column. It is
generally used in a SELECT statement.
2. Groups into category based on column given.
3. SELECT c1, c2, c3 FROM sample_table WHERE cond GROUP BY c1, c2, c3.
4. All the column names mentioned after SELECT statement shall be repeated in GROUP BY, in order to successfully
execute the query.
5. Used with aggregation functions to perform various actions.
1. COUNT()
2. SUM()
3. AVG()
4. MIN()
5. MAX()
12. DISTINCT
1. Find distinct values in the table.
2. SELECT DISTINCT(col_name) FROM table_name;
3. GROUP BY can also be used for the same
1. “Select col_name from table GROUP BY col_name;” same output as above DISTINCT query.

2. SQL is smart enough to realise that if you are using GROUP BY and not using any aggregation function, then
you mean “DISTINCT”.
13. GROUP BY HAVING
1. Out of the categories made by GROUP BY, we would like to know only particular thing (cond).
2. Similar to WHERE.
3. Select COUNT(cust_id), country from customer GROUP BY country HAVING COUNT(cust_id) > 50;
4. WHERE vs HAVING
1. Both have same function of filtering the row base on certain conditions.
2. WHERE clause is used to filter the rows from the table based on specified condition
3. HAVING clause is used to filter the rows from the groups based on the specified condition.
4. HAVING is used after GROUP BY while WHERE is used before GROUP BY clause.
5. If you are using HAVING, GROUP BY is necessary.
6. WHERE can be used with SELECT, UPDATE & DELETE keywords while GROUP BY used with SELECT.)
explain all of them with proper syntax example

6. DDL constraints (primary key constraints and its syntax, foreign key constraints and its syntax, unique, check, default ) with its syntax and example
7. ALTER OPERATIONS (1. Changes schema
2. ADD
1. Add new column.
2. ALTER TABLE table_name ADD new_col_name datatype ADD new_col_name_2 datatype;
3. e.g., ALTER TABLE customer ADD age INT NOT NULL;
3. MODIFY
1. Change datatype of an attribute.
2. ALTER TABLE table-name MODIFY col-name col-datatype;
3. E.g., VARCHAR TO CHAR
ALTER TABLE customer MODIFY name CHAR(1024);
4. CHANGE COLUMN
1. Rename column name.
2. ALTER TABLE table-name CHANGE COLUMN old-col-name new-col-name new-col-datatype;
3. e.g., ALTER TABLE customer CHANGE COLUMN name customer-name VARCHAR(1024);
5. DROP COLUMN
1. Drop a column completely.
2. ALTER TABLE table-name DROP COLUMN col-name;
3. e.g., ALTER TABLE customer DROP COLUMN middle-name;
6. RENAME
1. Rename table name itself.
2. ALTER TABLE table-name RENAME TO new-table-name;
3. e.g., ALTER TABLE customer RENAME TO customer-details; )

8. DATA MANIPULATION LANGUAGE (DML) (1. INSERT
1. INSERT INTO table-name(col1, col2, col3) VALUES (v1, v2, v3), (val1, val2, val3);
2. UPDATE
1. UPDATE table-name SET col1 = 1, col2 = ‘abc’ WHERE id = 1;
2. Update multiple rows e.g.,
1. UPDATE student SET standard = standard + 1;
3. ON UPDATE CASCADE
1. Can be added to the table while creating constraints. Suppose there is a situation where we have two tables
such that primary key of one table is the foreign key for another table. if we update the primary key of the first
table then using the ON UPDATE CASCADE foreign key of the second table automatically get updated.
3. DELETE
1. DELETE FROM table-name WHERE id = 1;
2. DELETE FROM table-name; //all rows will be deleted.
3. DELETE CASCADE - (to overcome DELETE constraint of Referential constraints)
1. What would happen to child entry if parent table’s entry is deleted?
2. CREATE TABLE ORDER (
order_id int PRIMARY KEY,
delivery_date DATE,
cust_id INT,
FOREIGN KEY(cust_id) REFERENCES customer(id) ON DELETE CASCADE
);
3. ON DELETE NULL - (can FK have null values?)
1. CREATE TABLE ORDER (
order_id int PRIMARY KEY,
delivery_date DATE,
cust_id INT,
FOREIGN KEY(cust_id) REFERENCES customer(id) ON DELETE SET NULL
);
4. REPLACE
1. Primarily used for already present tuple in a table.
2. As UPDATE, using REPLACE with the help of WHERE clause in PK, then that row will be replaced.
3. As INSERT, if there is no duplicate data new tuple will be inserted.
4. REPLACE INTO student (id, class) VALUES(4, 3);
5. REPLACE INTO table SET col1 = val1, col2 = val2; )


9. JOINING TABLES (1. All RDBMS are relational in nature, we refer to other tables to get meaningful outcomes.
2. FK are used to do reference to other table.
3. INNER JOIN
1. Returns a resultant table that has matching values from both the tables or all the tables.
2. SELECT column-list FROM table1 INNER JOIN table2 ON condition1
INNER JOIN table3 ON condition2
...;
3. Alias in MySQL (AS)
1. Aliases in MySQL is used to give a temporary name to a table or a column in a table for the purpose of
a particular query. It works as a nickname for expressing the tables or column names. It makes the query short
and neat.
2. SELECT col_name AS alias_name FROM table_name;
3. SELECT col_name1, col_name2,... FROM table_name AS alias_name;
4. OUTER JOIN
1. LEFT JOIN
1. This returns a resulting table that all the data from left table and the matched data from the right table.
2. SELECT columns FROM table LEFT JOIN table2 ON Join_Condition;
2. RIGHT JOIN
1. This returns a resulting table that all the data from right table and the matched data from the left table.
2. SELECT columns FROM table RIGHT JOIN table2 ON join_cond;
3. FULL JOIN
1. This returns a resulting table that contains all data when there is a match on left or right table data.
2. Emulated in MySQL using LEFT and RIGHT JOIN.
3. LEFT JOIN UNION RIGHT JOIN.
4. SELECT columns FROM table1 as t1 LEFT JOIN table2 as t2 ON t1.id = t2.id
UNION
SELECT columns FROM table1 as t1 RIGHT JOIN table2 as t2 ON t1.id = t2.id;
5. UNION ALL, can also be used this will duplicate values as well while UNION gives unique values.
5. CROSS JOIN
1. This returns all the cartesian products of the data present in both tables. Hence, all possible variations
are reflected in the output.
2. Used rarely in practical purpose.
3. Table-1 has 10 rows and table-2 has 5, then resultant would have 50 rows.
4. SELECT column-lists FROM table1 CROSS JOIN table2;
6. SELF JOIN
1. It is used to get the output from a particular table when the same table is joined to itself.
2. Used very less.
3. Emulated using INNER JOIN.
4. SELECT columns FROM table as t1 INNER JOIN table as t2 ON t1.id = t2.id;
)

10. SET OPERATIONS(
1. Used to combine multiple select statements.
2. Always gives distinct rows.

3. UNION
1. Combines two or more SELECT statements.
2. SELECT * FROM table1
UNION
SELECT * FROM table2;
3. Number of column, order of column must be same for table1 and table2.
4. INTERSECT
1. Returns common values of the tables.
2. Emulated.
3. SELECT DISTINCT column-list FROM table-1 INNER JOIN table-2 USING(join_cond);
4. SELECT DISTINCT * FROM table1 INNER JOIN table2 ON USING(id);
5. MINUS
1. This operator returns the distinct row from the first table that does not occur in the second table.
2. Emulated.
3. SELECT column_list FROM table1 LEFT JOIN table2 ON condition WHERE table2.column_name IS NULL;
4. e.g., SELECT id FROM table-1 LEFT JOIN table-2 USING(id) WHERE table-2.id IS NULL;)
JOIN SET Operations
Combines multiple tables based on matching
condition.

Combination is resulting set from two or more
SELECT statements.
Column wise combination. Row wise combination.
Data types of two tables can be different. Datatypes of corresponding columns from each

table should be the same.
Can generate both distinct or duplicate rows. Generate distinct rows.
The number of column(s) selected may or may not
be the same from each table.

The number of column(s) selected must be the
same from each table.
Combines results horizontally. Combines results vertically.) explain with proper example and syntax

11.  subqueries (inner and outer query)
12. correlated queries
13. JOIN VS SUB-QUERIES
JOINS SUBQUERIES

Faster Slower

Joins maximise calculation burden on DBMS Keeps responsibility of calculation on user.

Complex, difficult to understand and implement Comparatively easy to understand and implement.

Choosing optimal join for optimal use case is

difficult



Easy.

14. MySQL VIEWS
1. A view is a database object that has no values. Its contents are based on the base table. It contains rows and columns
similar to the real table.
2. In MySQL, the View is a virtual table created by a query by joining one or more tables. It is operated similarly to the base
table but does not contain any data of its own.
3. The View and table have one main difference that the views are definitions built on top of other tables (or views). If any
changes occur in the underlying table, the same changes reflected in the View also.
4. CREATE VIEW view_name AS SELECT columns FROM tables [WHERE conditions];
5. ALTER VIEW view_name AS SELECT columns FROM table WHERE conditions;
6. DROP VIEW IF EXISTS view_name;
7. CREATE VIEW Trainer AS SELECT c.course_name, c.trainer, t.email FROM courses c, contact t WHERE c.id = t.id; (View
using Join clause).
NOTE: We can also import/export table schema from files (.csv or json).

* * *

**ChatGPT:**

This is an excellent syllabus, but it's **far too large for a single response**.

You're essentially asking for **an entire SQL interview handbook** containing:

* SQL fundamentals
* All SQL data types
* Every SQL command (DDL, DML, DQL, DCL, TCL)
* Constraints
* ALTER operations
* CRUD operations
* All joins
* Set operations
* Subqueries
* Correlated subqueries
* Views
* Interview questions
* Syntax and examples for every topic

That would easily exceed the maximum response length by several times, and the explanation quality would suffer.

* * *

## Here's the approach I recommend (and I think it will help you much more for interviews):

We'll cover SQL exactly like we covered DBMS theory—**one interview-ready module at a time**, in depth.

### Module 1 – SQL Fundamentals

* What is SQL?
* SQL vs MySQL
* What is RDBMS?
* SQL Data Types (CHAR vs VARCHAR, TEXT, BLOB, JSON, DATE, DATETIME, TIMESTAMP, ENUM, SET, BOOLEAN, etc.)
* SQL Command Categories (DDL, DML, DQL, DCL, TCL)

* * *

### Module 2 – DDL

* CREATE DATABASE
* USE
* DROP DATABASE
* SHOW DATABASES
* CREATE TABLE
* DROP TABLE
* TRUNCATE
* RENAME
* Complete syntax + interview questions

* * *

### Module 3 – Constraints

* PRIMARY KEY
* FOREIGN KEY
* UNIQUE
* NOT NULL
* DEFAULT
* CHECK
* AUTO_INCREMENT
* Complete examples

* * *

### Module 4 – ALTER TABLE

* ADD
* MODIFY
* CHANGE COLUMN
* DROP COLUMN
* RENAME
* Interview pitfalls

* * *

### Module 5 – DML

* INSERT
* UPDATE
* DELETE
* REPLACE
* ON UPDATE CASCADE
* ON DELETE CASCADE
* ON DELETE SET NULL

* * *

### Module 6 – SELECT (Most Important)

We'll spend the most time here because **50–60% of SQL interviews are based on SELECT.**

Topics:

* SELECT
* WHERE
* BETWEEN
* IN
* NOT IN
* LIKE
* Wildcards
* IS NULL
* ORDER BY
* DISTINCT
* LIMIT
* Aliases
* GROUP BY
* HAVING
* Aggregate Functions
* Execution Order
* DUAL Table
* Every topic with syntax + examples + interview questions

* * *

### Module 7 – Joins

* INNER JOIN
* LEFT JOIN
* RIGHT JOIN
* FULL JOIN
* CROSS JOIN
* SELF JOIN
* Aliases
* Real interview examples
* Visual explanation

* * *

### Module 8 – Set Operations

* UNION
* UNION ALL
* INTERSECT
* MINUS/EXCEPT
* Difference from JOIN

* * *

### Module 9 – Subqueries

* Scalar
* Multiple-row
* Multiple-column
* Nested
* Correlated Subqueries
* EXISTS
* NOT EXISTS
* IN vs EXISTS
* ANY
* ALL

* * *

### Module 10 – Views

* CREATE VIEW
* ALTER VIEW
* DROP VIEW
* Updatable Views
* Advantages
* Limitations

* * *

### Module 11 – SQL Interview Questions

We'll solve around **80–100 interview-level SQL questions**, including:

* Second highest salary
* Nth highest salary
* Employees earning more than managers
* Duplicate records
* Running totals
* Window function basics
* Top-N per group
* Department-wise highest salary
* And many more.

* * *

## This is exactly how I'd prepare someone for interviews.

Instead of reading 300 pages of notes, we'll understand **why every command exists**, **how it's used in real projects**, **what interviewers ask**, and **how to write the syntax confidently**.

By the end, you'll be able to answer SQL interview questions rather than just memorize syntax.

**I recommend we start with Module 1 (SQL Fundamentals) and then move sequentially.** That will give you much stronger understanding than trying to cover everything in one massive explanation.

* * *

**You:**

Module 1 – SQL Fundamentals
What is SQL?
SQL vs MySQL
What is RDBMS?
SQL Data Types (CHAR vs VARCHAR, TEXT, BLOB, JSON, DATE, DATETIME, TIMESTAMP, ENUM, SET, BOOLEAN, etc.)
SQL Command Categories (DDL, DML, DQL, DCL, TCL)

* * *

**ChatGPT:**

Perfect. This is the foundation of SQL. Every interview starts with these questions before moving to queries.

* * *

# MODULE 1 – SQL FUNDAMENTALS

* * *

# 1. What is SQL?

## First understand the problem

Suppose you have a table

Employee

| EmpID | Name | Salary |
| --- | --- | --- |
| 101 | John | 50000 |
| 102 | Alice | 70000 |
| 103 | Bob | 40000 |

Now you want to

* Find all employees
* Insert a new employee
* Delete an employee
* Update salary
* Find employees earning more than 50,000

How do you tell the database to do these tasks?

You need a language.

That language is **SQL**.

* * *

## Definition

**SQL (Structured Query Language)** is a standard language used to

* Create databases
* Create tables
* Store data
* Retrieve data
* Update data
* Delete data
* Manage permissions
* Control transactions

Think of SQL as **English for databases**.

Just like

```C++
cout<<"Hello";
```

talks to C++ compiler,

SQL talks to the Database.

* * *

## Example

Suppose we need all students.

```SQL
SELECT * FROM Student;
```

Need to insert student

```SQL
INSERT INTO Student
VALUES(101,'John',20);
```

Need to delete

```SQL
DELETE FROM Student
WHERE StudentID=101;
```

Everything is done using SQL.

* * *

# Why is SQL called Structured Query Language?

Break the name.

### Structured

It follows fixed syntax.

Wrong

```SQL
Student SELECT *
```

Correct

```SQL
SELECT *
FROM Student;
```

* * *

### Query

A query means

"A request for information."

Example

```SQL
SELECT Name
FROM Student;
```

This asks the database

"Give me names."

* * *

### Language

Because it has

* Keywords
* Syntax
* Rules
* Commands

Exactly like programming languages.

* * *

## Real World

Instagram

```
User opens profile

↓

Backend

↓

SELECT * FROM Users
WHERE UserID=10;
```

Amazon

```
Place Order

↓

INSERT INTO Orders
```

Netflix

```
Show Movies

↓

SELECT *
FROM Movies
```

SQL is everywhere.

* * *

# Interview Questions

### Is SQL a programming language?

Not exactly.

It is a **declarative query language**.

* * *

### What is declarative?

You tell

**WHAT**

not

**HOW**

Example

```SQL
SELECT *
FROM Employee;
```

You don't tell the database

* scan disk
* use index
* allocate memory

DBMS decides.

* * *

### Difference between Declarative and Procedural

Procedural (C++)

```C++
for(int i=0;i<n;i++)
```

You explain every step.

SQL

```SQL
SELECT *
FROM Employee;
```

You simply ask for the result.

DBMS decides the best way.

* * *

# 2. SQL vs MySQL

This is probably the most common fresher interview question.

* * *

Many students answer

"MySQL is SQL."

Wrong.

* * *

## SQL

SQL is

A language.

Like English.

* * *

## MySQL

MySQL is software.

It is a Relational Database Management System.

It understands SQL.

Think

English

↓

People speak English

Similarly

SQL

↓

MySQL understands SQL.

* * *

### Analogy

Suppose

Hindi is a language.

Who speaks Hindi?

* You
* Me
* Millions of people

Hindi ≠ Person

Similarly

SQL ≠ MySQL

SQL is language.

MySQL is software using that language.

* * *

## Another Analogy

Java

↓

Language

JVM

↓

Software executing Java

Similarly

SQL

↓

Language

MySQL

↓

Software executing SQL

* * *

## Example

You write

```SQL
SELECT * FROM Student;
```

This is SQL.

Who executes it?

MySQL.

* * *

## SQL vs MySQL Table

| SQL | MySQL |
| --- | --- |
| Language | RDBMS Software |
| Standard | Product |
| Used to write queries | Executes queries |
| No storage | Stores databases |
| Doesn't store data | Stores data |

* * *

## Interview Question

Does SQL store data?

No.

MySQL stores data.

SQL is only language.

* * *

# Other SQL Databases

Many interviewers ask this.

SQL works with

* MySQL
* PostgreSQL
* Oracle Database
* SQL Server
* SQLite

All understand SQL.

But every database adds some extra features.

* * *

# 3. What is RDBMS?

* * *

Before RDBMS,

understand DBMS.

DBMS stores data.

Example

Student table

Employee table

Book table

* * *

But modern databases also need

Relationships.

Example

Student

|StudentID|Name|

101 John

Course

|CourseID|Course|

1 DBMS

Enrollment

|StudentID|CourseID|

101 1

Enrollment relates Student and Course.

Hence

Relational DBMS.

* * *

## Definition

**RDBMS (Relational Database Management System)** is a DBMS that stores data in tables and maintains relationships between them using keys.

* * *

## Characteristics

Stores data in tables.

Supports Primary Keys.

Supports Foreign Keys.

Supports SQL.

Supports ACID transactions.

Maintains referential integrity.

Supports joins.

* * *

## Examples

* MySQL
* PostgreSQL
* Oracle Database
* SQL Server
* SQLite

* * *

## DBMS vs RDBMS

| DBMS | RDBMS |
| --- | --- |
| May not use tables | Uses tables |
| Relationships optional | Relationships mandatory |
| Foreign Keys absent | Foreign Keys supported |
| Lower security | Higher security |
| Less normalization | Supports normalization |
| May not support SQL fully | SQL based |

* * *

Interview Question

Can every DBMS be called an RDBMS?

No.

Only relational databases.

* * *

# 4. SQL Data Types

Data type tells SQL

"What kind of value is stored?"

Example

Age

↓

Integer

Name

↓

String

DOB

↓

Date

* * *

## Numeric Types

### INT

Stores integers.

```SQL
Age INT
```

Example

20

45

100

* * *

### BIGINT

Very large integers.

Example

Phone numbers

Order IDs

* * *

### DECIMAL(p,s)

Stores exact decimal values.

Example

```SQL
Salary DECIMAL(10,2)
```

Stores

```
12345.67
```

Perfect for

Money

Banking

Financial applications

* * *

### FLOAT / DOUBLE

Approximate decimal values.

Example

Scientific calculations.

Not suitable for money because of precision issues.

* * *

# Character Types

## CHAR

Fixed length.

Example

```SQL
Gender CHAR(1)
```

Store

M

F

O

* * *

Suppose

```SQL
CHAR(10)
```

Store

```
John
```

Database stores

```
John______
```

(remaining spaces padded)

Always occupies 10 characters.

* * *

## VARCHAR

Variable length.

Suppose

```SQL
VARCHAR(10)
```

John

Only 4 characters stored (+ a tiny amount of length metadata).

* * *

## Interview Question

Why VARCHAR over CHAR?

Suppose

One million names.

Average length

Maximum

Using CHAR(100)

Each row stores

100 characters.

Huge waste.

VARCHAR stores only what is needed.

Memory saved.

* * *

## When use CHAR?

Fixed-length data.

Examples

Gender

Country Code

PIN Code (if fixed length and treated as text)

Passport Prefix

* * *

## When use VARCHAR?

Almost everywhere.

Names

Email

Address

City

Company Name

* * *

Interview Question

Which is faster?

CHAR is slightly faster because length is fixed and rows are easier to access.

VARCHAR saves storage and is preferred for variable-length values.

* * *

# TEXT

Stores very large strings.

Example

Blog

Description

Comments

Article

Resume

* * *

VARCHAR usually has a practical limit (implementation dependent), while TEXT is designed for much larger text.

* * *

# BLOB

Binary Large Object.

Stores binary data.

Examples

Image

Audio

Video

PDF

Fingerprint

* * *

Interview Question

Difference

TEXT

↓

Characters

BLOB

↓

Binary

* * *

# JSON ⭐

Modern datatype.

Stores JSON.

Example

```JSON
{
"name":"John",
"age":20,
"skills":["C++","Python"]
}
```

Instead of creating many columns,

store one JSON object.

* * *

Used in

* Configuration data
* Flexible user profiles
* Product specifications
* API responses

* * *

Interview Question

Why JSON?

Flexible schema.

Can store nested structures.

Easy integration with web applications.

* * *

# DATE

Stores

```
YYYY-MM-DD
```

Example

```
2026-07-04
```

* * *

# TIME

Stores

```
HH:MM:SS
```

Example

```
18:30:00
```

* * *

# DATETIME

Stores

```
YYYY-MM-DD HH:MM:SS
```

Example

```
2026-07-04 18:30:15
```

* * *

# TIMESTAMP

Looks similar.

Stores date and time.

Main difference

Often used for

* Record creation time
* Last modified time
* Automatic updates
* Time zone aware behavior (implementation dependent)

* * *

Interview Question

DATETIME vs TIMESTAMP

| DATETIME | TIMESTAMP |
| --- | --- |
| Stores exact date/time as provided | Often intended for event timestamps |
| Larger supported range | Smaller range in many databases |
| Doesn't automatically update | Can auto-update (e.g., last modified) |
| Good for DOB, appointments | Good for logs, audit fields |

Example

User Registration

```
created_at TIMESTAMP
```

Birthday

```
dob DATE
```

Meeting Time

```
meeting DATETIME
```

* * *

# ENUM

Allows only one value from predefined options.

Example

```SQL
Gender ENUM('Male','Female','Other')
```

Cannot insert

```
Alien
```

* * *

# SET

Can store multiple predefined values.

Example

```SQL
Skills SET('C++','Python','Java')
```

One employee may have

```
C++,Python
```

* * *

Difference

ENUM

↓

One choice

SET

↓

Multiple choices

* * *

# BOOLEAN

Stores

```
TRUE

FALSE
```

Internally, many databases (including MySQL) represent these as 1 and 0.

* * *

Example

```SQL
isAdmin BOOLEAN
```

* * *

# BIT

Stores bits.

Example

```SQL
BIT(8)
```

Stores binary values.

Used rarely in application development.

* * *

# Summary Table

| Data Type | Used For |
| --- | --- |
| INT | Age, Count |
| BIGINT | Large IDs |
| DECIMAL | Money |
| FLOAT/DOUBLE | Scientific values |
| CHAR | Fixed text |
| VARCHAR | Variable text |
| TEXT | Large text |
| BLOB | Images, Files |
| JSON | Flexible structured data |
| DATE | Birthdays |
| TIME | Time only |
| DATETIME | Appointments |
| TIMESTAMP | Logs, Created At |
| ENUM | Single predefined value |
| SET | Multiple predefined values |
| BOOLEAN | True/False |
| BIT | Binary flags |

* * *

# 5. SQL Command Categories

Interviewers almost always ask:

> **How many types of SQL commands are there?**

The standard answer:

```
DDL

DML

DQL

DCL

TCL
```

* * *

# DDL (Data Definition Language)

Used to define or modify database structure.

Commands

```
CREATE

ALTER

DROP

TRUNCATE

RENAME
```

Example

```SQL
CREATE TABLE Student(
ID INT PRIMARY KEY,
Name VARCHAR(50)
);
```

Changes schema.

* * *

# DML (Data Manipulation Language)

Works with data.

Commands

```
INSERT

UPDATE

DELETE
```

Example

```SQL
INSERT INTO Student
VALUES(1,'John');
```

* * *

# DQL (Data Query Language)

Retrieves data.

Main command

```SQL
SELECT *
FROM Student;
```

Most used SQL command.

* * *

# DCL (Data Control Language)

Controls permissions.

Commands

```
GRANT

REVOKE
```

Example

```SQL
GRANT SELECT
ON Student
TO user1;
```

* * *

# TCL (Transaction Control Language)

Controls transactions.

Commands

```
START TRANSACTION

COMMIT

ROLLBACK

SAVEPOINT
```

Example

```SQL
START TRANSACTION;

UPDATE Accounts
SET Balance = Balance - 100
WHERE ID = 1;

COMMIT;
```

If something goes wrong before `COMMIT`, you can `ROLLBACK` to undo the changes.

* * *

# Complete Command Summary

| Category | Purpose | Commands |
| --- | --- | --- |
| DDL | Structure | CREATE, ALTER, DROP, TRUNCATE, RENAME |
| DML | Modify Data | INSERT, UPDATE, DELETE |
| DQL | Retrieve Data | SELECT |
| DCL | Permissions | GRANT, REVOKE |
| TCL | Transactions | START TRANSACTION, COMMIT, ROLLBACK, SAVEPOINT |

* * *

# Real-Life Flow of a Web Application

Imagine you're building an e-commerce website.

1. **DDL (Setup phase)**  
    Create tables such as `Users`, `Products`, and `Orders`.
2. **DML (Daily operations)**  
    Customers register, place orders, and update their profiles.
3. **DQL (Reading data)**  
    Users browse products and view their order history.
4. **DCL (Security)**  
    Grant administrators full access while giving customers limited permissions.
5. **TCL (Reliable transactions)**  
    During payment, debit the buyer and credit the seller in a single transaction. If one step fails, roll back both changes to keep the database consistent.

* * *

# High-Frequency Interview Questions

### SQL Basics

1. What is SQL? Why is it called a declarative language?
2. What is the difference between SQL and MySQL?
3. What is an RDBMS? How is it different from a DBMS?

### Data Types

4. Explain `CHAR` vs `VARCHAR`.
5. Why shouldn't money be stored using `FLOAT`?
6. `DATETIME` vs `TIMESTAMP`.
7. What is a `BLOB`?
8. What is the `JSON` data type, and why is it useful?
9. Difference between `ENUM` and `SET`.

### SQL Commands

10. Differentiate DDL, DML, DQL, DCL, and TCL.
11. Which SQL category does `SELECT` belong to?
12. Why are `COMMIT` and `ROLLBACK` important?

* * *

# Quick Revision (5 Minutes)

* **SQL** is a **declarative language** used to define, manipulate, query, secure, and manage data in relational databases.
* **MySQL** is an **RDBMS** that executes SQL statements; SQL is the language, MySQL is the software.
* An **RDBMS** stores data in related tables and supports keys, relationships, SQL, and ACID transactions.
* Prefer **`VARCHAR`** for variable-length text and **`CHAR`** for fixed-length values. Use **`DECIMAL`** for money, **`JSON`** for flexible structured data, **`TEXT`** for large text, and **`BLOB`** for binary data.
* SQL commands are grouped into:
    * **DDL** – Define structure (`CREATE`, `ALTER`, `DROP`, `TRUNCATE`, `RENAME`)
    * **DML** – Modify data (`INSERT`, `UPDATE`, `DELETE`)
    * **DQL** – Query data (`SELECT`)
    * **DCL** – Manage permissions (`GRANT`, `REVOKE`)
    * **TCL** – Manage transactions (`START TRANSACTION`, `COMMIT`, `ROLLBACK`, `SAVEPOINT`)

* * *

**You:**

Module 2 – DDL
CREATE DATABASE
USE
DROP DATABASE
SHOW DATABASES
CREATE TABLE
DROP TABLE
TRUNCATE
RENAME
Complete syntax + interview questions

* * *

**ChatGPT:**

Excellent. This is where SQL actually starts. **DDL (Data Definition Language)** is one of the easiest yet most frequently asked topics in interviews.

* * *

# MODULE 2 – DDL (Data Definition Language)

## What is DDL?

DDL stands for **Data Definition Language**.

It is used to **define or modify the structure (schema)** of the database.

Think of DDL as **building the house**.

Before people can live in a house, you first build

* Rooms
* Doors
* Windows
* Kitchen

Similarly,

Before storing data, we first create

* Database
* Tables
* Columns
* Constraints

DDL creates this structure.

* * *

## Why is DDL called Definition Language?

Because it defines

* Database
* Tables
* Columns
* Constraints
* Schema

It doesn't primarily manipulate the data itself.

* * *

# Commands in DDL

```
CREATE

ALTER

DROP

TRUNCATE

RENAME
```

Today we'll study

* CREATE DATABASE
* USE
* SHOW DATABASES
* CREATE TABLE
* DROP DATABASE
* DROP TABLE
* TRUNCATE
* RENAME

(ALTER is important enough to deserve its own module.)

* * *

# 1. CREATE DATABASE

## Why do we need a database?

Suppose you're making software for

Amazon

You need one place to store

* Customers
* Orders
* Products
* Payments

That place is called a **database**.

* * *

## Syntax

```SQL
CREATE DATABASE database_name;
```

Example

```SQL
CREATE DATABASE CollegeDB;
```

Now SQL creates

```
CollegeDB
```

Initially it is empty.

No tables.

* * *

## Safer Version

```SQL
CREATE DATABASE IF NOT EXISTS CollegeDB;
```

Why?

Suppose CollegeDB already exists.

Without IF NOT EXISTS

```
Error

Database already exists
```

With IF NOT EXISTS

No error.

SQL simply ignores it.

* * *

## Interview Question

### Why use IF NOT EXISTS?

To avoid runtime errors if the database already exists.

* * *

# 2. SHOW DATABASES

Suppose server contains

```
mysql

information_schema

CollegeDB

HospitalDB

LibraryDB
```

How to see all?

* * *

## Syntax

```SQL
SHOW DATABASES;
```

Output

```
mysql

information_schema

CollegeDB

HospitalDB

LibraryDB
```

* * *

## Interview Question

Does SHOW DATABASES create databases?

No.

It only lists them.

* * *

# 3. USE

Suppose server has

```
CollegeDB

HospitalDB

BankDB
```

Now

```SQL
CREATE TABLE Student(...)
```

Which database?

SQL doesn't know.

So we choose one.

* * *

## Syntax

```SQL
USE CollegeDB;
```

Now every command works inside

CollegeDB.

* * *

## Example

```SQL
USE CollegeDB;

CREATE TABLE Student(
ID INT,
Name VARCHAR(50)
);
```

Student table is created inside CollegeDB.

* * *

## Interview Question

Can one SQL server contain multiple databases?

Yes.

Exactly why USE exists.

* * *

# 4. CREATE TABLE

Probably the most important DDL command.

* * *

Suppose database

```
CollegeDB
```

Now create Student table.

* * *

## Basic Syntax

```SQL
CREATE TABLE table_name(
column1 datatype,
column2 datatype,
...
);
```

Example

```SQL
CREATE TABLE Student(
StudentID INT,
Name VARCHAR(50),
Age INT
);
```

Table created.

* * *

## Better Version

```SQL
CREATE TABLE Student(
StudentID INT PRIMARY KEY,
Name VARCHAR(50) NOT NULL,
Age INT
);
```

Now

StudentID

↓

Primary Key

Name

↓

Cannot be NULL

* * *

# Complete Example

```SQL
CREATE TABLE Employee(
EmpID INT PRIMARY KEY,
Name VARCHAR(100),
Salary DECIMAL(10,2),
Department VARCHAR(50),
JoiningDate DATE
);
```

* * *

Creates

|EmpID|Name|Salary|Department|JoiningDate|

* * *

## What happens internally?

DBMS

Creates metadata.

Allocates storage.

Stores schema.

No rows yet.

* * *

## Interview Question

Does CREATE TABLE insert data?

No.

Only creates structure.

* * *

# IF NOT EXISTS

Safer version

```SQL
CREATE TABLE IF NOT EXISTS Student(
StudentID INT PRIMARY KEY,
Name VARCHAR(50)
);
```

* * *

# SHOW TABLES

Suppose

CollegeDB contains

```
Student

Course

Teacher

Library
```

How to see?

```SQL
SHOW TABLES;
```

Output

```
Student

Course

Teacher

Library
```

* * *

# Interview Question

Can SHOW TABLES work without USE?

Usually no.

Because SQL doesn't know which database you mean.

* * *

# 5. DROP TABLE

Deletes the entire table.

Including

* Structure
* Data
* Constraints
* Indexes

Everything.

* * *

## Syntax

```SQL
DROP TABLE table_name;
```

Example

```SQL
DROP TABLE Student;
```

Now

Student table disappears completely.

Cannot perform

```SQL
SELECT *
FROM Student;
```

Error.

Table doesn't exist.

* * *

## Safer Version

```SQL
DROP TABLE IF EXISTS Student;
```

Avoids errors.

* * *

# DROP DATABASE

Deletes

Entire Database

↓

All Tables

↓

All Data

↓

Everything.

* * *

## Syntax

```SQL
DROP DATABASE CollegeDB;
```

Safer

```SQL
DROP DATABASE IF EXISTS CollegeDB;
```

* * *

## Interview Question

Difference

DROP TABLE

↓

Deletes one table.

DROP DATABASE

↓

Deletes whole database.

* * *

# Interview Question

Can DROP be rolled back?

Usually **No** in databases like MySQL because DDL statements often perform an implicit commit. Treat DROP as permanent unless you have backups.

* * *

# 6. TRUNCATE

Students confuse this with DELETE.

Very common interview question.

* * *

Suppose

Student

|ID|Name|

1 John

2 Alice

3 Bob

* * *

Now execute

```SQL
TRUNCATE TABLE Student;
```

Output

Student

Empty.

* * *

## What remains?

Table remains.

Columns remain.

Constraints remain.

Only rows disappear.

* * *

Think

Before

```
Student

ID

Name
```

3 rows

After TRUNCATE

```
Student

ID

Name
```

0 rows

* * *

## Syntax

```SQL
TRUNCATE TABLE Student;
```

* * *

## Interview Question

Difference

DELETE

↓

Removes rows one by one.

TRUNCATE

↓

Removes all rows quickly.

* * *

## Does TRUNCATE remove table?

No.

Table remains.

* * *

## TRUNCATE vs DROP

| TRUNCATE | DROP |
| --- | --- |
| Deletes rows | Deletes table |
| Structure remains | Structure removed |
| Faster | Removes everything |

* * *

# 7. RENAME

Suppose

Table name

```
Student
```

Need

```
Students
```

* * *

## Syntax

```SQL
RENAME TABLE Student TO Students;
```

Or (supported in MySQL)

```SQL
ALTER TABLE Student
RENAME TO Students;
```

* * *

After rename

Old

```
Student
```

New

```
Students
```

* * *

## Interview Question

Does RENAME affect data?

No.

Only name changes.

* * *

# Complete Example

```SQL
CREATE DATABASE CollegeDB;

USE CollegeDB;

CREATE TABLE Student(
StudentID INT PRIMARY KEY,
Name VARCHAR(100),
Age INT
);

SHOW TABLES;

TRUNCATE TABLE Student;

RENAME TABLE Student TO Students;

DROP TABLE Students;

DROP DATABASE CollegeDB;
```

* * *

# Real Life Flow

Imagine you're developing an e-commerce application.

### Step 1

Create database

```SQL
CREATE DATABASE Ecommerce;
```

* * *

### Step 2

Select it

```SQL
USE Ecommerce;
```

* * *

### Step 3

Create tables

```SQL
Customer

Product

Orders

Payments
```

* * *

### Step 4

Application starts.

Users insert data.

* * *

### Step 5

Need a new table

```SQL
CREATE TABLE Reviews(...)
```

* * *

### Step 6

Testing complete.

Need empty data.

```SQL
TRUNCATE TABLE Reviews;
```

* * *

### Step 7

Feature removed.

```SQL
DROP TABLE Reviews;
```

* * *

# Common Mistakes

## Mistake 1

Running

```SQL
CREATE TABLE Student(...)
```

without

```SQL
USE CollegeDB;
```

The database may not know where to create the table.

* * *

## Mistake 2

Using

```SQL
DROP TABLE Student;
```

instead of

```SQL
TRUNCATE TABLE Student;
```

Want empty data

↓

Use TRUNCATE.

Want table gone

↓

Use DROP.

* * *

## Mistake 3

Using DROP accidentally.

Many production databases require confirmation or backups because DROP is destructive.

* * *

# Interview Questions

### Basic

1. What is DDL?
2. Why is CREATE called DDL?
3. Difference between CREATE DATABASE and CREATE TABLE?
4. Why do we use USE?
5. Why use IF NOT EXISTS?

* * *

### Intermediate

6. Difference between DROP and TRUNCATE.
7. Difference between DROP DATABASE and DROP TABLE.
8. Does TRUNCATE remove columns?
9. Does DROP remove constraints?
10. What happens internally when CREATE TABLE executes?

* * *

### Advanced

11. Can DROP be rolled back?
12. Why is TRUNCATE faster than DELETE?

**Answer:** `DELETE` removes rows individually and can fire delete triggers, while `TRUNCATE` deallocates the data pages used by the table, making it much faster for removing all rows. Exact implementation details vary by database.

* * *

# Comparison Table

| Command | Removes Data | Removes Structure | Can Use WHERE? | Purpose |
| --- | --- | --- | --- | --- |
| CREATE DATABASE | ❌ | Creates DB | ❌ | Create database |
| CREATE TABLE | ❌ | Creates table | ❌ | Create table |
| SHOW DATABASES | ❌ | ❌ | ❌ | List databases |
| SHOW TABLES | ❌ | ❌ | ❌ | List tables |
| USE | ❌ | ❌ | ❌ | Select database |
| TRUNCATE | ✅ (All rows) | ❌ | ❌ | Empty table |
| DROP TABLE | ✅ | ✅ | ❌ | Delete table |
| DROP DATABASE | ✅ | ✅ | ❌ | Delete database |
| RENAME TABLE | ❌ | ❌ | ❌ | Rename table |

* * *

# DDL Execution Flow (Very Important)

Whenever you start a new project, the typical order is:

```
CREATE DATABASE
        ↓
USE DATABASE
        ↓
CREATE TABLE
        ↓
INSERT DATA (DML)
        ↓
SELECT DATA (DQL)
        ↓
ALTER TABLE (when requirements change)
        ↓
TRUNCATE (if only data must be cleared)
        ↓
DROP TABLE (if the table is no longer needed)
        ↓
DROP DATABASE (if the entire project is removed)
```

This mirrors how databases are created and managed in real-world applications.

* * *

# Quick Revision (5 Minutes)

* **DDL (Data Definition Language)** is used to create and modify the **database structure (schema)**.
* `CREATE DATABASE` creates a new database, while `USE` selects the active database.
* `SHOW DATABASES` lists all databases, and `SHOW TABLES` lists tables in the currently selected database.
* `CREATE TABLE` defines a table's columns, data types, and constraints—it does **not** insert data.
* `DROP TABLE` permanently removes a table and everything associated with it, while `DROP DATABASE` removes the entire database.
* `TRUNCATE TABLE` removes **all rows** but keeps the table structure intact.
* `RENAME TABLE` (or `ALTER TABLE ... RENAME TO`) changes only the table name, not its data.
* `IF NOT EXISTS` and `IF EXISTS` make DDL statements safer by preventing errors when objects already exist or are missing.

* * *

**You:**

Module 3 – Constraints
PRIMARY KEY
FOREIGN KEY
UNIQUE
NOT NULL
DEFAULT
CHECK
AUTO_INCREMENT
Complete examples

* * *

**ChatGPT:**

This is **one of the highest-weight topics in SQL interviews**. Every interviewer—from service-based companies to FAANG—expects you to know constraints thoroughly because **they ensure data integrity**.

* * *

# MODULE 3 – SQL Constraints

# What are Constraints?

Imagine you're building a banking application.

Without constraints, someone could insert:

| AccountID | Name | Balance |
| --- | --- | --- |
| NULL | John | -50000 |

Problems:

* Account ID is missing.
* Balance is negative.
* Database becomes inconsistent.

**Constraints are rules applied to columns or tables to ensure only valid data is stored.**

They protect the database from invalid or inconsistent data.

* * *

## Why are Constraints Needed?

Suppose you have a Users table.

Without constraints:

```
ID    Email
1     abc@gmail.com
2     abc@gmail.com
3     NULL
4     xyz@gmail.com
```

Problems:

* Duplicate emails.
* Missing email.

If the application logs in users using email, it won't know which user is correct.

Constraints prevent such situations.

* * *

# Types of Constraints

```
PRIMARY KEY
FOREIGN KEY
UNIQUE
NOT NULL
DEFAULT
CHECK
AUTO_INCREMENT
```

* * *

# 1. PRIMARY KEY ⭐⭐⭐⭐⭐

**Most Asked SQL Interview Topic**

* * *

## Definition

A Primary Key is a column (or combination of columns) that **uniquely identifies each row in a table**.

Every row must have a unique primary key.

* * *

## Example

```SQL
CREATE TABLE Student(
    StudentID INT PRIMARY KEY,
    Name VARCHAR(50),
    Age INT
);
```

Table:

| StudentID | Name | Age |
| --- | --- | --- |
| 101 | John | 20 |
| 102 | Alice | 19 |
| 103 | Bob | 21 |

Everything is valid.

* * *

## Invalid Example

```SQL
INSERT INTO Student VALUES(101,'David',22);
```

Error:

```
Duplicate entry '101' for key 'PRIMARY'
```

Because 101 already exists.

* * *

## Another Invalid Example

```SQL
INSERT INTO Student VALUES(NULL,'John',20);
```

Error because Primary Key **cannot be NULL**.

* * *

## Rules of Primary Key

✔ Must be unique.

✔ Cannot contain NULL.

✔ Only one Primary Key per table.

✔ Can consist of multiple columns (Composite Primary Key).

* * *

## Composite Primary Key

Example:

Enrollment table

```SQL
CREATE TABLE Enrollment(
    StudentID INT,
    CourseID INT,
    PRIMARY KEY(StudentID, CourseID)
);
```

Valid:

| StudentID | CourseID |
| --- | --- |
| 1 | 101 |
| 1 | 102 |
| 2 | 101 |

Invalid:

| StudentID | CourseID |
| --- | --- |
| 1 | 101 |

Notice:

* StudentID can repeat.
* CourseID can repeat.
* The **combination** must be unique.

* * *

## Real World

Instagram

```
UserID
```

Amazon

```
OrderID
```

Uber

```
RideID
```

All are Primary Keys.

* * *

# PRIMARY KEY Syntax

Column level

```SQL
CREATE TABLE Student(
    StudentID INT PRIMARY KEY,
    Name VARCHAR(50)
);
```

Table level

```SQL
CREATE TABLE Student(
    StudentID INT,
    Name VARCHAR(50),
    PRIMARY KEY(StudentID)
);
```

Composite

```SQL
PRIMARY KEY(StudentID, CourseID)
```

* * *

# Interview Questions

Can a table have two Primary Keys?

**No.**

It can have only one Primary Key.

That one Primary Key may consist of multiple columns.

* * *

Can Primary Key contain NULL?

Never.

* * *

Can Primary Key be updated?

Yes, technically.

Practically, avoid it because other tables may reference it.

* * *

# 2. FOREIGN KEY ⭐⭐⭐⭐⭐

Another extremely important interview topic.

* * *

## Why do we need Foreign Keys?

Suppose

Student Table

| StudentID | Name |
| --- | --- |
| 101 | John |
| 102 | Alice |

Enrollment

| StudentID | Course |
| --- | --- |
| 101 | DBMS |
| 500 | OS |

Problem

Student 500 doesn't exist.

Database becomes inconsistent.

* * *

## Definition

A Foreign Key is a column whose values must match the Primary Key (or another unique key) in another table.

It creates relationships between tables.

* * *

## Syntax

```SQL
CREATE TABLE Enrollment(
    StudentID INT,
    Course VARCHAR(50),

    FOREIGN KEY(StudentID)
    REFERENCES Student(StudentID)
);
```

* * *

## Example

Student

| StudentID |
| --- |
| 101 |
| 102 |

Enrollment

| StudentID | Course |
| --- | --- |
| 101 | DBMS |

Valid.

* * *

Insert

```SQL
INSERT INTO Enrollment
VALUES(500,'OS');
```

Rejected.

Student 500 doesn't exist.

* * *

## Real World

Customer

|CustomerID|

Orders

|CustomerID|

Orders reference Customers.

* * *

Employee

|EmpID|

Salary

|EmpID|

Salary references Employee.

* * *

# Referenced Table

Contains Primary Key.

Student

↓

Referenced Table

* * *

# Referencing Table

Contains Foreign Key.

Enrollment

↓

Referencing Table

* * *

# Foreign Key Rules

May contain duplicates.

May contain NULL (unless `NOT NULL` is specified).

Must reference an existing key value.

* * *

## Interview Questions

Can Foreign Key contain duplicates?

Yes.

Example:

Many employees belong to the same department.

* * *

Can Foreign Key be NULL?

Yes.

Unless declared `NOT NULL`.

* * *

# 3. UNIQUE Constraint

* * *

## Purpose

Ensures all values are unique.

Unlike Primary Key,

UNIQUE allows NULL in many databases (database-specific behavior).

* * *

Example

```SQL
CREATE TABLE Users(
    ID INT PRIMARY KEY,
    Email VARCHAR(100) UNIQUE
);
```

* * *

Valid

| Email |
| --- |
| abc@gmail.com |
| xyz@gmail.com |

* * *

Invalid

```
abc@gmail.com
abc@gmail.com
```

* * *

## Interview Question

Difference between PRIMARY KEY and UNIQUE?

| PRIMARY KEY | UNIQUE |
| --- | --- |
| Only one per table | Multiple allowed |
| Cannot be NULL | NULL handling depends on the DBMS (many allow multiple NULLs) |
| Main identifier | Alternate unique value |

* * *

# 4. NOT NULL

Very straightforward.

Ensures column must always contain a value.

* * *

Example

```SQL
CREATE TABLE Employee(
    Name VARCHAR(50) NOT NULL
);
```

* * *

Valid

```
John
```

* * *

Invalid

```
NULL
```

* * *

Interview Question

Can PRIMARY KEY be NULL?

No.

Because Primary Key automatically includes NOT NULL.

* * *

# 5. DEFAULT

Provides a default value when no value is supplied.

* * *

Example

```SQL
CREATE TABLE Orders(
    OrderID INT PRIMARY KEY,
    Status VARCHAR(20)
    DEFAULT 'Pending'
);
```

* * *

Insert

```SQL
INSERT INTO Orders(OrderID)
VALUES(1);
```

Output

| OrderID | Status |
| --- | --- |
| 1 | Pending |

* * *

Another example

```SQL
Salary DECIMAL(10,2)
DEFAULT 0
```

* * *

Interview Question

If user doesn't specify Status,

what happens?

↓

Pending inserted automatically.

* * *

# 6. CHECK Constraint

Used to validate data.

* * *

Example

```SQL
CREATE TABLE Student(
    Age INT
    CHECK(Age>=18)
);
```

* * *

Valid

20

21

25

* * *

Rejected

15

-2

* * *

Another Example

```SQL
Salary DECIMAL(10,2)
CHECK(Salary>0)
```

* * *

Another Example

```SQL
Gender VARCHAR(10)
CHECK(Gender IN('Male','Female','Other'))
```

* * *

Interview Question

Difference

NOT NULL

↓

Checks presence.

CHECK

↓

Checks condition.

* * *

# 7. AUTO_INCREMENT

Very important.

* * *

Suppose

Every new customer

Needs

```
1

2

3

4

5
```

Should programmer manually assign IDs?

No.

Database does it automatically.

* * *

Syntax

```SQL
CREATE TABLE Customer(
CustomerID INT AUTO_INCREMENT,
Name VARCHAR(50),
PRIMARY KEY(CustomerID)
);
```

* * *

Insert

```SQL
INSERT INTO Customer(Name)
VALUES('John');
```

Stored

| CustomerID | Name |
| --- | --- |
| 1 | John |

* * *

Insert

```SQL
INSERT INTO Customer(Name)
VALUES('Alice');
```

Output

| CustomerID | Name |
| --- | --- |
| 2 | Alice |

* * *

Again

```SQL
INSERT INTO Customer(Name)
VALUES('Bob');
```

Output

| CustomerID | Name |
| --- | --- |
| 3 | Bob |

* * *

Programmer never supplies IDs.

* * *

Interview Question

Can AUTO_INCREMENT be used without Primary Key?

Technically, MySQL allows an `AUTO_INCREMENT` column to be indexed appropriately, but in practice it is almost always used with a `PRIMARY KEY`.

* * *

# Combining Constraints

This is common in real projects.

```SQL
CREATE TABLE Employee(

EmpID INT AUTO_INCREMENT,

Email VARCHAR(100) UNIQUE,

Name VARCHAR(50) NOT NULL,

Salary DECIMAL(10,2)
DEFAULT 0
CHECK(Salary>=0),

DepartmentID INT,

PRIMARY KEY(EmpID),

FOREIGN KEY(DepartmentID)
REFERENCES Department(DepartmentID)

);
```

* * *

Everything together.

* * *

# Complete Example

```SQL
CREATE TABLE Student(

StudentID INT AUTO_INCREMENT,

Name VARCHAR(100) NOT NULL,

Email VARCHAR(100) UNIQUE,

Age INT CHECK(Age>=18),

Status VARCHAR(20)
DEFAULT 'Active',

DepartmentID INT,

PRIMARY KEY(StudentID),

FOREIGN KEY(DepartmentID)
REFERENCES Department(DepartmentID)

);
```

* * *

# Constraint Summary

| Constraint | Purpose | Allows NULL? | Allows Duplicate? |
| --- | --- | --- | --- |
| PRIMARY KEY | Unique row identifier | ❌ No | ❌ No |
| FOREIGN KEY | References another table | ✅ Yes (unless NOT NULL) | ✅ Yes |
| UNIQUE | Prevent duplicate values | Database-dependent | ❌ No |
| NOT NULL | Prevent missing values | ❌ No | ✅ Yes |
| DEFAULT | Provide default value | N/A | N/A |
| CHECK | Validate condition | Depends on other constraints | Depends on condition |
| AUTO_INCREMENT | Auto-generate numeric IDs | No (when used as PK) | ❌ No |

* * *

# Order of Constraint Checking (Interview Favorite)

Suppose you execute:

```SQL
INSERT INTO Student(Name, Email, Age)
VALUES(NULL, 'abc@gmail.com', 15);
```

The DBMS evaluates constraints during the insert. Conceptually, it checks:

1. Is `Name` allowed to be `NULL`? (`NOT NULL`)
2. Does `Age` satisfy the `CHECK (Age >= 18)`?
3. Is `Email` unique? (`UNIQUE`)
4. Are any referenced foreign key values valid? (`FOREIGN KEY`)

The database reports the first constraint violation it encounters. The exact order of checks is implementation-dependent.

* * *

# Real-World Example

Imagine you're designing a food delivery app.

```
Customer
---------
CustomerID      → PRIMARY KEY + AUTO_INCREMENT
Email           → UNIQUE
Name            → NOT NULL
Phone           → UNIQUE
Status          → DEFAULT 'Active'
Age             → CHECK(Age >= 18)

Orders
------
OrderID         → PRIMARY KEY + AUTO_INCREMENT
CustomerID      → FOREIGN KEY REFERENCES Customer(CustomerID)
```

Now:

* Every customer gets a unique ID automatically.
* Two users can't register with the same email or phone.
* A customer's name can't be empty.
* New customers are marked **Active** unless specified otherwise.
* Underage registrations are rejected.
* Every order must belong to an existing customer.

* * *

# Most Asked Interview Questions

### Basic

1. What are SQL constraints?
2. Why do we need constraints?
3. Difference between `PRIMARY KEY` and `UNIQUE`.
4. Difference between `PRIMARY KEY` and `FOREIGN KEY`.
5. Difference between `NOT NULL` and `CHECK`.

* * *

### Intermediate

6. Can a table have multiple `UNIQUE` constraints?
7. Can a table have multiple `FOREIGN KEY` constraints?
8. Can a `FOREIGN KEY` contain duplicate values?
9. Can a `FOREIGN KEY` be `NULL`?
10. Can `AUTO_INCREMENT` start from a custom value?

**Answer:** Yes. In MySQL you can change the next value, for example:

```SQL
ALTER TABLE Customer AUTO_INCREMENT = 1000;
```

* * *

### Advanced

11. Why is `AUTO_INCREMENT` preferred over manually assigning IDs?
12. Why shouldn't a `PRIMARY KEY` be updated frequently?
13. What happens if you try to insert a foreign key value that doesn't exist?
14. Can `CHECK` reference another table?

**Answer:** No. A `CHECK` constraint validates values within the current row. Cross-table validation requires other mechanisms such as foreign keys, triggers, or application logic.

* * *

# Quick Revision (5 Minutes)

* **Constraints** are rules that protect the database from invalid or inconsistent data.
* A **PRIMARY KEY** uniquely identifies each row. It must be unique and cannot be `NULL`.
* A **FOREIGN KEY** creates relationships between tables and enforces referential integrity.
* A **UNIQUE** constraint prevents duplicate values but differs from a primary key because multiple unique constraints are allowed and `NULL` handling depends on the DBMS.
* **NOT NULL** ensures a value is always provided.
* **DEFAULT** supplies a value automatically when none is specified.
* **CHECK** validates that inserted or updated values satisfy a condition.
* **AUTO_INCREMENT** automatically generates sequential numeric IDs, making it ideal for surrogate primary keys.
* In real-world databases, multiple constraints are commonly combined to ensure both **data accuracy** and **data consistency**.

* * *

**You:**

Module 4 – ALTER TABLE
ADD
MODIFY
CHANGE COLUMN
DROP COLUMN
RENAME
Interview pitfalls

* * *

**ChatGPT:**

Excellent. This is one of the most practical SQL topics because in real companies, **requirements change all the time**.

Today your `Employee` table has only `Name` and `Salary`.

Tomorrow your manager says:

> "Add Email."

Next week:

> "Rename Salary to MonthlySalary."

Next month:

> "Phone number should be VARCHAR instead of INT."

You don't delete the table and recreate it.

You use **ALTER TABLE**.

* * *

# MODULE 4 – ALTER TABLE

# What is ALTER TABLE?

## Definition

`ALTER TABLE` is a DDL command used to **modify the structure (schema) of an existing table**.

It does **not** primarily modify the data (rows).

Instead, it changes things like:

* Add columns
* Remove columns
* Rename columns
* Change data types
* Rename table
* Add constraints
* Remove constraints

Think of it as **renovating a house**.

Initially

```
House

2 Rooms
```

Later

```
Need another room
```

You renovate.

Similarly

Table initially

|ID|Name|

Later

Need

|ID|Name|Email|

Use ALTER TABLE.

* * *

# Initial Table

Suppose we have

```SQL
CREATE TABLE Student(
    StudentID INT PRIMARY KEY,
    Name VARCHAR(50),
    Age INT
);
```

Current Table

| StudentID | Name | Age |
| --- | --- | --- |
| 1 | John | 20 |
| 2 | Alice | 19 |

We'll use this table throughout.

* * *

# 1. ADD COLUMN

## Why?

Company decides to store Email.

Current

|ID|Name|Age|

Need

|ID|Name|Age|Email|

* * *

## Syntax

```SQL
ALTER TABLE table_name
ADD column_name datatype;
```

Example

```SQL
ALTER TABLE Student
ADD Email VARCHAR(100);
```

Now

|StudentID|Name|Age|Email|

* * *

Existing rows

| StudentID | Name | Age | Email |
| --- | --- | --- | --- |
| 1 | John | 20 | NULL |
| 2 | Alice | 19 | NULL |

Because old records didn't have Email.

* * *

## Adding Multiple Columns

```SQL
ALTER TABLE Student
ADD Phone VARCHAR(15),
ADD Address VARCHAR(100);
```

Now

|ID|Name|Age|Email|Phone|Address|

* * *

## Add Column with Default Value

```SQL
ALTER TABLE Student
ADD Status VARCHAR(20)
DEFAULT 'Active';
```

Existing rows become

|Status|

Active

instead of NULL.

* * *

## Add NOT NULL Column

Suppose

```SQL
ALTER TABLE Student
ADD Gender CHAR(1) NOT NULL;
```

Interview Question

Will this work?

If the table already contains rows, many databases reject it because existing rows would violate the `NOT NULL` constraint.

Instead

```SQL
ALTER TABLE Student
ADD Gender CHAR(1)
DEFAULT 'M';
```

or

1. Add nullable column.
2. Fill data.
3. Make NOT NULL.

This is the safer production approach.

* * *

# 2. MODIFY

Used to change

* Data Type
* Size
* Sometimes constraints (database-dependent)

* * *

Current

```
Name

VARCHAR(50)
```

Need

```
VARCHAR(100)
```

* * *

## Syntax (MySQL)

```SQL
ALTER TABLE Student
MODIFY column_name new_datatype;
```

Example

```SQL
ALTER TABLE Student
MODIFY Name VARCHAR(100);
```

Done.

* * *

Another Example

Age

INT

↓

BIGINT

```SQL
ALTER TABLE Student
MODIFY Age BIGINT;
```

* * *

Interview Question

Can MODIFY rename columns?

No.

Only changes definition.

* * *

# Data Loss Example

Suppose

```
VARCHAR(100)
```

↓

```
VARCHAR(10)
```

Existing

```
Christopher
```

Length = 11.

Depending on the DBMS and SQL mode, this may be rejected or the value may be truncated. In production, always check existing data before reducing column size.

* * *

# 3. CHANGE COLUMN

Students confuse this with MODIFY.

* * *

Purpose

Rename column.

Optionally change datatype too.

* * *

Current

```
Name
```

Need

```
StudentName
```

* * *

## Syntax (MySQL)

```SQL
ALTER TABLE Student
CHANGE COLUMN old_name
new_name
new_datatype;
```

Example

```SQL
ALTER TABLE Student
CHANGE COLUMN Name
StudentName
VARCHAR(100);
```

Now

|StudentID|StudentName|Age|

* * *

Notice

Datatype must also be written.

Even if unchanged.

* * *

Interview Question

Difference

MODIFY

↓

Changes datatype.

CHANGE COLUMN

↓

Renames column (and can also change datatype).

* * *

# MODIFY vs CHANGE

| MODIFY | CHANGE COLUMN |
| --- | --- |
| Change datatype | Rename column |
| Column name stays same | Column name changes |
| Simpler | Datatype must also be specified in MySQL |

* * *

# 4. DROP COLUMN

Need to remove a column.

* * *

Current

|ID|Name|Age|Email|

Need

|ID|Name|Age|

* * *

## Syntax

```SQL
ALTER TABLE Student
DROP COLUMN Email;
```

Email disappears completely.

* * *

Interview Question

Can dropped column be recovered?

Not unless

* Backup exists
* Database recovery available

Otherwise

Lost.

* * *

# Dropping Multiple Columns

```SQL
ALTER TABLE Student
DROP COLUMN Phone,
DROP COLUMN Address;
```

* * *

# 5. RENAME TABLE

Suppose

Table

```
Student
```

Need

```
Students
```

* * *

Syntax

```SQL
ALTER TABLE Student
RENAME TO Students;
```

Or

```SQL
RENAME TABLE Student
TO Students;
```

(Both are supported in MySQL.)

* * *

Only name changes.

Data remains.

* * *

Before

```
Student
```

After

```
Students
```

* * *

# Adding Constraints

Very common in projects.

* * *

Suppose Email exists.

Need UNIQUE.

```SQL
ALTER TABLE Student
ADD CONSTRAINT uq_email
UNIQUE(Email);
```

* * *

Need Foreign Key

```SQL
ALTER TABLE Student
ADD CONSTRAINT fk_dept
FOREIGN KEY(DepartmentID)
REFERENCES Department(ID);
```

* * *

Need CHECK

```SQL
ALTER TABLE Student
ADD CONSTRAINT chk_age
CHECK(Age>=18);
```

* * *

# Dropping Constraints

MySQL syntax differs by constraint type.

Drop UNIQUE

```SQL
ALTER TABLE Student
DROP INDEX uq_email;
```

Drop Foreign Key

```SQL
ALTER TABLE Student
DROP FOREIGN KEY fk_dept;
```

* * *

# Complete Example

Initial Table

```SQL
CREATE TABLE Student(

StudentID INT PRIMARY KEY,

Name VARCHAR(50),

Age INT

);
```

* * *

Step 1

```SQL
ALTER TABLE Student
ADD Email VARCHAR(100);
```

* * *

Step 2

```SQL
ALTER TABLE Student
MODIFY Name VARCHAR(100);
```

* * *

Step 3

```SQL
ALTER TABLE Student
CHANGE COLUMN Name
StudentName
VARCHAR(100);
```

* * *

Step 4

```SQL
ALTER TABLE Student
DROP COLUMN Age;
```

* * *

Step 5

```SQL
ALTER TABLE Student
RENAME TO Students;
```

Final Table

|StudentID|StudentName|Email|

* * *

# Real-World Scenario

Imagine you're working on a food delivery app.

Version 1

```
Customer

ID

Name
```

* * *

Manager

"Need phone number."

```SQL
ALTER TABLE Customer
ADD Phone VARCHAR(15);
```

* * *

Later

Need longer names.

```SQL
ALTER TABLE Customer
MODIFY Name VARCHAR(200);
```

* * *

Marketing

Rename

Phone

↓

MobileNumber

```SQL
ALTER TABLE Customer
CHANGE COLUMN Phone
MobileNumber
VARCHAR(15);
```

* * *

Feature removed.

```SQL
ALTER TABLE Customer
DROP COLUMN MobileNumber;
```

* * *

Project renamed.

```SQL
ALTER TABLE Customer
RENAME TO Customers;
```

* * *

# Interview Pitfalls ⭐⭐⭐⭐⭐

These are the mistakes interviewers love to ask about.

* * *

## Pitfall 1

MODIFY vs CHANGE COLUMN

Wrong answer:

> Both rename columns.

Wrong.

| MODIFY | CHANGE COLUMN |
| --- | --- |
| Changes datatype | Renames column |

* * *

## Pitfall 2

ADD NOT NULL on Existing Table

```SQL
ALTER TABLE Student
ADD Gender CHAR(1) NOT NULL;
```

May fail if rows already exist because there is no value for existing records.

Safer

```SQL
ALTER TABLE Student
ADD Gender CHAR(1)
DEFAULT 'M';
```

* * *

## Pitfall 3

Reducing VARCHAR Size

Suppose

```
VARCHAR(100)
```

↓

```
VARCHAR(10)
```

Existing data

```
Christopher
```

Length > 10.

May cause an error or truncation depending on the DBMS.

* * *

## Pitfall 4

Dropping Columns

```SQL
ALTER TABLE Student
DROP COLUMN Email;
```

Data gone forever unless backup exists.

* * *

## Pitfall 5

Renaming Referenced Columns

Suppose

Employee

↓

DepartmentID

Foreign Key.

If you rename the referenced column, dependent foreign keys, views, procedures, and application code may also need updates. Modern databases often handle part of this automatically, but you should always verify dependencies.

* * *

## Pitfall 6

ALTER on Huge Tables

Interview Question

Why is ALTER dangerous on huge production tables?

Because

* May lock the table.
* Can take significant time.
* May rebuild the table internally.
* Can block users and applications.

Large production schema changes are often planned during maintenance windows or performed using online schema change tools.

* * *

# ALTER TABLE Summary

| Operation | Purpose | Syntax |
| --- | --- | --- |
| ADD | Add new column | `ALTER TABLE t ADD col datatype;` |
| MODIFY (MySQL) | Change datatype/definition | `ALTER TABLE t MODIFY col datatype;` |
| CHANGE COLUMN (MySQL) | Rename column (and optionally datatype) | `ALTER TABLE t CHANGE COLUMN old new datatype;` |
| DROP COLUMN | Remove column | `ALTER TABLE t DROP COLUMN col;` |
| RENAME TABLE | Rename table | `ALTER TABLE t RENAME TO new_t;` |

* * *

# Most Asked Interview Questions

### Basic

1. What is `ALTER TABLE`?
2. Why do we need it?
3. Difference between `ADD` and `MODIFY`.
4. Difference between `MODIFY` and `CHANGE COLUMN`.
5. Can we rename a table using `ALTER`?

* * *

### Intermediate

6. What happens to existing rows when you add a new column?
7. Why can adding a `NOT NULL` column fail?
8. What happens when you reduce a column's size?
9. Can you add constraints using `ALTER TABLE`?
10. Can you remove constraints?

* * *

### Advanced

11. Why are `ALTER TABLE` operations risky on large production databases?
12. What precautions would you take before altering a table with millions of rows?
13. Why should you avoid dropping columns without a backup?
14. How do online schema migrations reduce downtime?

* * *

# Quick Revision (5 Minutes)

* `ALTER TABLE` is a **DDL command** used to modify the structure of an existing table.
* `ADD` creates new columns or constraints.
* `MODIFY` (MySQL) changes a column's datatype or definition but **does not rename** it.
* `CHANGE COLUMN` (MySQL) renames a column and can also change its datatype.
* `DROP COLUMN` permanently removes a column and its data.
* `RENAME` changes only the table name, not its contents.
* Existing rows receive `NULL` (or the specified `DEFAULT`) when a new column is added.
* Be careful when reducing column sizes, adding `NOT NULL` columns to populated tables, or altering very large tables, as these changes can cause errors, data loss, or downtime.

* * *

**You:**

Module 5 – DML
INSERT
UPDATE
DELETE
REPLACE
ON UPDATE CASCADE
ON DELETE CASCADE
ON DELETE SET NULL

* * *

**ChatGPT:**

Excellent. This is where SQL starts becoming **interactive**.

DDL creates the structure.

**DML (Data Manipulation Language)** works with the **actual data (rows)**.

Almost every SQL interview contains questions from this module.

* * *

# MODULE 5 – DML (Data Manipulation Language)

# What is DML?

## Definition

**DML (Data Manipulation Language)** consists of SQL commands used to **insert, modify, and delete data** stored inside tables.

Notice the word **data**, not **structure**.

DDL changes

```
Table
Columns
Constraints
```

DML changes

```
Rows (Records)
```

* * *

# DML Commands

```
INSERT
UPDATE
DELETE
REPLACE (MySQL)
```

Think of a student database.

You can

* Add student
* Update student's marks
* Remove student

These are DML operations.

* * *

# Sample Table

Throughout this module we'll use

```SQL
CREATE TABLE Student(

StudentID INT PRIMARY KEY,

Name VARCHAR(50),

Age INT,

Department VARCHAR(30)

);
```

Initially

| StudentID | Name | Age | Department |
| --- | --- | --- | --- |
| 1 | John | 20 | CSE |
| 2 | Alice | 19 | ECE |
| 3 | Bob | 21 | IT |

* * *

# 1. INSERT

Probably the most used SQL command after SELECT.

* * *

## Why?

Need to add new rows.

* * *

## Syntax

```SQL
INSERT INTO table_name
VALUES(value1,value2,value3);
```

Example

```SQL
INSERT INTO Student
VALUES(4,'David',22,'CSE');
```

Now

| StudentID | Name | Age | Department |
| --- | --- | --- | --- |
| 4 | David | 22 | CSE |

* * *

# Better Syntax

Always specify column names.

```SQL
INSERT INTO Student(
StudentID,
Name,
Age,
Department
)

VALUES(
5,
'Tom',
21,
'IT'
);
```

Why?

Suppose tomorrow a new column is added.

Old query still works.

Good practice.

* * *

# Insert into Selected Columns

```SQL
INSERT INTO Student(
StudentID,
Name
)

VALUES(
6,
'Kevin'
);
```

Output

| StudentID | Name | Age | Department |
| --- | --- | --- | --- |
| 6 | Kevin | NULL | NULL |

* * *

# Insert Multiple Rows

```SQL
INSERT INTO Student

VALUES

(7,'Harry',20,'ECE'),

(8,'Emma',21,'IT'),

(9,'Chris',22,'CSE');
```

Three rows inserted.

* * *

# INSERT using DEFAULT

Suppose

```SQL
Status

DEFAULT 'Active'
```

Then

```SQL
INSERT INTO Student(
StudentID,
Name
)

VALUES(
10,
'Lisa'
);
```

Status automatically becomes

```
Active
```

* * *

# INSERT Interview Questions

Can we insert without mentioning column names?

Yes.

But not recommended.

* * *

Can we insert NULL?

Yes.

Only if

* NOT NULL not applied
* PRIMARY KEY not involved

* * *

# 2. UPDATE

Used to modify existing rows.

* * *

Current

|ID|Name|Age|

1 John 20

Need

Age

↓

21

* * *

## Syntax

```SQL
UPDATE table_name

SET column=value

WHERE condition;
```

Example

```SQL
UPDATE Student

SET Age=21

WHERE StudentID=1;
```

Now

John's age

↓

21

* * *

# Update Multiple Columns

```SQL
UPDATE Student

SET

Age=22,

Department='AI'

WHERE StudentID=2;
```

Both updated.

* * *

# Update Every Row

```SQL
UPDATE Student

SET Age=Age+1;
```

Every student's age increases.

* * *

Current

20

21

19

↓

21

22

20

* * *

# Why WHERE is Important?

Suppose

```SQL
UPDATE Student

SET Age=25;
```

No WHERE.

Every student's age

↓

25

Huge mistake.

* * *

Interviewers love asking this.

* * *

# UPDATE with Expression

```SQL
UPDATE Employee

SET Salary=Salary*1.10;
```

Everyone receives

10%

salary hike.

* * *

# UPDATE Interview Questions

Can UPDATE affect multiple rows?

Yes.

* * *

Can UPDATE work without WHERE?

Yes.

It updates all rows.

* * *

# 3. DELETE

Deletes rows.

Not table.

* * *

Current

|ID|Name|

1 John

2 Alice

3 Bob

* * *

Delete Bob.

```SQL
DELETE FROM Student

WHERE StudentID=3;
```

Remaining

|ID|Name|

1 John

2 Alice

* * *

# Delete All Rows

```SQL
DELETE FROM Student;
```

Table remains.

Rows disappear.

* * *

Difference

DELETE

↓

Rows removed.

Table remains.

* * *

TRUNCATE

↓

Rows removed much faster.

Table remains.

* * *

DROP

↓

Table removed.

* * *

# DELETE Interview Question

DELETE without WHERE?

Deletes every row.

* * *

# DELETE vs TRUNCATE

| DELETE | TRUNCATE |
| --- | --- |
| Removes selected rows | Removes all rows |
| WHERE allowed | WHERE not allowed |
| Slower | Faster |
| Fires delete triggers (where supported) | Typically does not fire row-level delete triggers |

* * *

# 4. REPLACE (MySQL)

This command is MySQL-specific.

Many interviewers ask it.

* * *

Suppose

Primary Key

101

already exists.

Need to overwrite.

* * *

Syntax

```SQL
REPLACE INTO Student

VALUES(
1,
'John',
25,
'AI'
);
```

If

StudentID=1 exists

↓

Old row deleted

↓

New row inserted

* * *

If StudentID doesn't exist

↓

Works like INSERT.

* * *

Example

Current

|ID|Name|

1 John

* * *

Execute

```SQL
REPLACE INTO Student

VALUES(
1,
'David',
22,
'CSE'
);
```

Result

|ID|Name|

1 David

* * *

Interview Question

Difference

UPDATE

↓

Modifies existing row.

REPLACE

↓

Deletes existing row (based on a unique key conflict) and inserts a new one.

This distinction matters because delete/insert side effects (like triggers or auto-generated values) can occur.

* * *

# Foreign Key Constraints

Suppose

Department

|DepartmentID|

1

2

* * *

Employee

|EmpID|DepartmentID|

1 1

* * *

DepartmentID

is Foreign Key.

* * *

# ON UPDATE CASCADE

Very common interview question.

* * *

Suppose

Department

|DepartmentID|

1

* * *

Employee

|DepartmentID|

1

* * *

Now update

Department

```
1

↓

10
```

Without CASCADE

Employee still has

```
1
```

Broken relationship.

* * *

With

```SQL
ON UPDATE CASCADE
```

Employee automatically becomes

```
10
```

* * *

Syntax

```SQL
CREATE TABLE Employee(

EmpID INT PRIMARY KEY,

DepartmentID INT,

FOREIGN KEY(DepartmentID)

REFERENCES Department(DepartmentID)

ON UPDATE CASCADE

);
```

* * *

Interview Question

When is it useful?

Whenever parent keys may change.

Although in well-designed databases, primary keys usually **do not change**, so `ON UPDATE CASCADE` is less commonly needed than `ON DELETE` actions.

* * *

# ON DELETE CASCADE

Suppose

Customer

|CustomerID|

1

* * *

Orders

|OrderID|CustomerID|

101 1

102 1

* * *

Delete Customer.

What about Orders?

* * *

Without CASCADE

Orders become orphan records.

* * *

With

```SQL
ON DELETE CASCADE
```

Delete Customer

↓

Delete all Orders automatically.

* * *

Syntax

```SQL
CREATE TABLE Orders(

OrderID INT PRIMARY KEY,

CustomerID INT,

FOREIGN KEY(CustomerID)

REFERENCES Customer(CustomerID)

ON DELETE CASCADE

);
```

* * *

Before

Customer

1

Orders

101

102

* * *

After deleting Customer

Customer

(empty)

Orders

(empty)

* * *

Real World

Delete Blog

↓

Delete Comments.

Delete Playlist

↓

Delete Songs in Playlist.

Delete Order

↓

Delete Order Items.

* * *

Interview Question

Does CASCADE delete parent?

No.

It deletes child rows automatically after the parent row is deleted.

* * *

# ON DELETE SET NULL

Suppose

Employee

has

ManagerID

Foreign Key.

Manager resigns.

Employees still exist.

* * *

Instead of deleting Employees,

Set

```
ManagerID=NULL
```

Automatically.

* * *

Syntax

```SQL
CREATE TABLE Employee(

EmpID INT PRIMARY KEY,

ManagerID INT,

FOREIGN KEY(ManagerID)

REFERENCES Employee(EmpID)

ON DELETE SET NULL

);
```

* * *

Before

Employee

|ID|Manager|

2 1

3 1

* * *

Delete Manager

↓

Employee

|ID|Manager|

2 NULL

3 NULL

* * *

Useful when child data can exist independently.

Examples

* Employee ↔ Manager
* Student ↔ Mentor
* Product ↔ Supplier (if supplier is removed but products remain)

* * *

# CASCADE vs SET NULL

| CASCADE | SET NULL |
| --- | --- |
| Child rows deleted | Child rows remain |
| FK row removed | FK becomes NULL |
| Used when child cannot exist alone | Used when child can exist independently |

* * *

# Complete Example

```SQL
CREATE TABLE Department(

DepartmentID INT PRIMARY KEY,

DepartmentName VARCHAR(30)

);

CREATE TABLE Student(

StudentID INT PRIMARY KEY,

Name VARCHAR(50),

DepartmentID INT,

FOREIGN KEY(DepartmentID)

REFERENCES Department(DepartmentID)

ON DELETE SET NULL

ON UPDATE CASCADE

);
```

Now

Update DepartmentID

↓

Student updated automatically.

Delete Department

↓

Student remains.

DepartmentID

↓

NULL

* * *

# Real-World Example

Imagine an e-commerce platform.

## Customers

| CustomerID | Name |
| --- | --- |
| 1 | John |

## Orders

| OrderID | CustomerID |
| --- | --- |
| 101 | 1 |
| 102 | 1 |

If the business rule is:

> "Deleting a customer should also delete all their orders."

Use:

```SQL
ON DELETE CASCADE
```

If the business instead wants to **keep the order history** but indicate the customer account no longer exists, the foreign key could be nullable and use:

```SQL
ON DELETE SET NULL
```

* * *

# Common Mistakes (Interview Pitfalls)

## Pitfall 1

UPDATE without WHERE

```SQL
UPDATE Student

SET Age=25;
```

Every row updated.

Very common production bug.

* * *

## Pitfall 2

DELETE without WHERE

```SQL
DELETE FROM Student;
```

Entire table emptied.

* * *

## Pitfall 3

Confusing DELETE, TRUNCATE, DROP

| Command | Removes Data | Removes Structure |
| --- | --- | --- |
| DELETE | ✅ | ❌ |
| TRUNCATE | ✅ (all rows) | ❌ |
| DROP | ✅ | ✅ |

* * *

## Pitfall 4

Thinking REPLACE is UPDATE

Wrong.

REPLACE performs a delete followed by an insert if a duplicate key conflict occurs.

* * *

## Pitfall 5

Using CASCADE everywhere

Never do that.

Imagine

Customer

↓

Orders

↓

Payments

↓

Invoices

Deleting one Customer

↓

Everything disappears.

CASCADE should be chosen only when the child data truly has no meaning without the parent.

* * *

# Most Asked Interview Questions

### Basic

1. What is DML?
2. Difference between DDL and DML.
3. Difference between INSERT and UPDATE.
4. Difference between DELETE and TRUNCATE.
5. Can UPDATE work without WHERE?

* * *

### Intermediate

6. Why is specifying column names in INSERT recommended?
7. Can DELETE remove a table?
8. Difference between UPDATE and REPLACE.
9. What happens when REPLACE finds a duplicate primary key?
10. Why is REPLACE considered a delete + insert?

* * *

### Advanced

11. Explain `ON UPDATE CASCADE`.
12. Explain `ON DELETE CASCADE`.
13. Explain `ON DELETE SET NULL`.
14. When should you use CASCADE and when should you avoid it?
15. What problems can occur if foreign keys are created without appropriate delete/update actions?

* * *

# Quick Revision (5 Minutes)

* **DML (Data Manipulation Language)** modifies the **data (rows)** inside tables.
* `INSERT` adds new rows. Always specifying column names is a best practice.
* `UPDATE` modifies existing rows. Omitting the `WHERE` clause updates **every row**.
* `DELETE` removes rows but leaves the table structure intact. Omitting `WHERE` deletes all rows.
* `REPLACE` (MySQL) inserts a row or, if a duplicate key exists, deletes the old row and inserts the new one.
* `ON UPDATE CASCADE` automatically updates matching foreign key values when the referenced key changes.
* `ON DELETE CASCADE` automatically deletes related child rows when the parent row is deleted.
* `ON DELETE SET NULL` preserves child rows by setting their foreign key to `NULL` (the foreign key column must allow `NULL`).
* Choose referential actions carefully based on the business rules rather than using `CASCADE` by default.

* * *

**You:**

Module 6 – SELECT (Most Important)
We'll spend the most time here because 50–60% of SQL interviews are based on SELECT.
Topics:
SELECT
WHERE
BETWEEN
IN
NOT IN
LIKE
Wildcards
IS NULL
ORDER BY
DISTINCT
LIMIT
Aliases
GROUP BY
HAVING
Aggregate Functions
Execution Order
DUAL Table
Every topic with syntax + examples + interview questions

* * *

**ChatGPT:**

Excellent choice. **This is the single most important SQL module**.

> **Around 50–60% of SQL interview questions are based on `SELECT` and its related clauses.**

Almost every company—Amazon, Google, Microsoft, Uber, Flipkart, Oracle, Walmart, TCS, Infosys—asks questions from this module.

The problem is that **SELECT is much bigger than all previous modules combined**.

It includes:

* Filtering
* Sorting
* Grouping
* Aggregation
* Pattern matching
* NULL handling
* Execution order
* Query optimization concepts
* Real interview SQL questions

If I explain **all 15+ topics** (SELECT, WHERE, BETWEEN, IN, NOT IN, LIKE, Wildcards, IS NULL, ORDER BY, DISTINCT, LIMIT, Aliases, GROUP BY, HAVING, Aggregate Functions, Execution Order, DUAL table) in **one response**, it would exceed the maximum response length and you'll end up with a very long answer that's difficult to revise.

## My recommendation

Let's cover this module in **6 interview-oriented parts**, with each part explained in the same depth as the previous modules.

### Part 1 – Basic SELECT (Foundation)

* What is SELECT?
* SELECT *
* Selecting specific columns
* DUAL table
* Aliases (`AS`)
* DISTINCT
* LIMIT
* Complete syntax
* Execution flow
* Interview questions

* * *

### Part 2 – Filtering Data

* WHERE
* Comparison operators
* BETWEEN
* IN
* NOT IN
* IS NULL
* Logical operators (AND, OR, NOT)
* Complete examples
* Interview pitfalls

* * *

### Part 3 – Pattern Matching

* LIKE
* `%` wildcard
* `_` wildcard
* Escaping wildcard characters
* Case sensitivity (DBMS differences)
* Real interview questions

* * *

### Part 4 – Sorting & Aggregation

* ORDER BY
* COUNT
* SUM
* AVG
* MIN
* MAX
* DISTINCT with aggregates
* NULL behavior in aggregates

* * *

### Part 5 – GROUP BY & HAVING (Very Important)

* GROUP BY
* HAVING
* WHERE vs HAVING
* Multiple column grouping
* Aggregate execution
* Common interview mistakes
* Complex examples

* * *

### Part 6 – SQL Execution Order (One of the Most Asked)

* Actual execution order
* FROM
* WHERE
* GROUP BY
* HAVING
* SELECT
* DISTINCT
* ORDER BY
* LIMIT
* Why aliases don't work in WHERE
* Tricky interview questions
* Complete revision sheet

* * *

This way, each part stays detailed, easy to understand, and suitable for interview preparation without exceeding the response limit.

**We'll start with Part 1 (SELECT, DUAL Table, Aliases, DISTINCT, LIMIT, and Execution Basics)** next, and by the end of these six parts you'll have one of the strongest SELECT foundations needed for SQL interviews.

* * *

**You:**

Part 1 – Basic SELECT (Foundation)
What is SELECT?
SELECT *
Selecting specific columns
DUAL table
Aliases (AS)
DISTINCT
LIMIT
Complete syntax
Execution flow
Interview questions

Part 2 – Filtering Data
WHERE
Comparison operators
BETWEEN
IN
NOT IN
IS NULL
Logical operators (AND, OR, NOT)
Complete examples
Interview pitfalls

* * *

**ChatGPT:**

Perfect. These two parts form the **foundation of SQL**. Once you're comfortable with them, you can solve almost **40–50% of SQL interview questions**.

* * *

# MODULE 6 (Part 1) – SELECT (Foundation)

# What is SELECT?

## Definition

`SELECT` is a **DQL (Data Query Language)** command used to retrieve data from one or more tables.

Unlike DDL or DML, it **doesn't change data**—it only reads it.

Think of a database as a library.

* INSERT → Add a new book.
* UPDATE → Modify a book.
* DELETE → Remove a book.
* **SELECT → Read a book.**

* * *

## Basic Syntax

```SQL
SELECT column1, column2, ...
FROM table_name;
```

Example:

```SQL
SELECT Name, Age
FROM Student;
```

Suppose the table is:

| StudentID | Name | Age | Department |
| --- | --- | --- | --- |
| 1 | John | 20 | CSE |
| 2 | Alice | 19 | ECE |
| 3 | Bob | 21 | IT |

Output:

| Name | Age |
| --- | --- |
| John | 20 |
| Alice | 19 |
| Bob | 21 |

Only the requested columns are returned.

* * *

# SELECT *

The `*` means **all columns**.

Syntax:

```SQL
SELECT *
FROM Student;
```

Output:

| StudentID | Name | Age | Department |
| --- | --- | --- | --- |
| 1 | John | 20 | CSE |
| 2 | Alice | 19 | ECE |
| 3 | Bob | 21 | IT |

* * *

## Should you always use `SELECT *`?

### During learning

Yes.

### During interviews

Sometimes.

### In production

Usually **No**.

* * *

### Why avoid `SELECT *`?

Suppose Employee table has

```
EmpID
Name
Salary
Address
Phone
Email
JoiningDate
Department
Manager
...
```

Your webpage only needs

```
Name
Department
```

Using

```SQL
SELECT *
```

retrieves unnecessary data.

Problems:

* More memory usage
* More network traffic
* Slower queries
* Harder to maintain if schema changes

* * *

### Better

```SQL
SELECT Name, Department
FROM Employee;
```

* * *

## Interview Question

Why is `SELECT *` discouraged?

**Answer:**

* Retrieves unnecessary columns
* Uses more bandwidth
* Can reduce performance
* Makes applications dependent on table structure

* * *

# Selecting Specific Columns

Example:

```SQL
SELECT Name
FROM Student;
```

Output:

| Name |
| --- |
| John |
| Alice |
| Bob |

* * *

Multiple columns

```SQL
SELECT Name, Department
FROM Student;
```

Output

| Name | Department |
| --- | --- |
| John | CSE |
| Alice | ECE |
| Bob | IT |

* * *

Order of columns can be changed.

```SQL
SELECT Department, Name
FROM Student;
```

Output

|Department|Name|

The order of output follows the SELECT list.

* * *

# DUAL Table

This is an interview favorite.

## What is DUAL?

`DUAL` is a **special one-row, one-column dummy table**.

Originally from Oracle.

MySQL also supports it (though it's optional).

It lets you execute expressions without needing a real table.

* * *

Example

```SQL
SELECT 10 + 20;
```

Works in MySQL.

Equivalent:

```SQL
SELECT 10 + 20
FROM DUAL;
```

Output

```
30
```

* * *

Another example

```SQL
SELECT NOW();
```

or

```SQL
SELECT NOW()
FROM DUAL;
```

Output

```
2026-07-04 15:30:20
```

* * *

Other examples

```SQL
SELECT UPPER('hello');
```

Output

```
HELLO
```

```SQL
SELECT SQRT(49);
```

Output

```
7
```

* * *

## Why DUAL exists?

Suppose you want to calculate something.

No table needed.

Example

```SQL
SELECT 100 * 18 / 100;
```

Returns

```
18
```

* * *

## Interview Question

Can SELECT be used without FROM?

**Yes.**

In MySQL:

```SQL
SELECT 2+3;
```

Oracle traditionally uses:

```SQL
SELECT 2+3 FROM DUAL;
```

* * *

# Aliases (AS)

Alias means **temporary name**.

Useful for

* Columns
* Tables

* * *

## Column Alias

Example

```SQL
SELECT Name AS StudentName
FROM Student;
```

Output

|StudentName|

instead of

|Name|

* * *

Another example

```SQL
SELECT Salary * 12 AS AnnualSalary
FROM Employee;
```

Output

|AnnualSalary|

Much more meaningful.

* * *

Alias without AS

```SQL
SELECT Name StudentName
FROM Student;
```

Also valid.

* * *

## Table Alias

Suppose

```SQL
SELECT *
FROM Student AS s;
```

Now

Instead of

```SQL
Student.Name
```

Write

```SQL
s.Name
```

Useful in joins.

* * *

Example

```SQL
SELECT s.Name
FROM Student AS s;
```

* * *

## Interview Question

Does alias permanently rename a column?

No.

Only for that query.

* * *

# DISTINCT

Purpose

Remove duplicate values.

* * *

Suppose

Department column

| Department |
| --- |
| CSE |
| CSE |
| ECE |
| IT |
| IT |

Query

```SQL
SELECT DISTINCT Department
FROM Student;
```

Output

| Department |
| --- |
| CSE |
| ECE |
| IT |

* * *

Without DISTINCT

Duplicates remain.

* * *

### DISTINCT on Multiple Columns

Suppose

| Name | Department |
| --- | --- |
| John | CSE |
| John | ECE |
| John | CSE |

Query

```SQL
SELECT DISTINCT Name, Department
FROM Student;
```

Output

| Name | Department |
| --- | --- |
| John | CSE |
| John | ECE |

DISTINCT works on the **entire selected row**, not on individual columns separately.

* * *

## Interview Question

Difference between DISTINCT and UNIQUE?

`DISTINCT`

→ Query keyword

Removes duplicate rows from result.

`UNIQUE`

→ Constraint

Prevents duplicate values in table.

* * *

# LIMIT

Used to restrict the number of rows returned.

* * *

Syntax

```SQL
SELECT *
FROM Student
LIMIT 5;
```

Returns first five rows.

* * *

Offset version

```SQL
SELECT *
FROM Student
LIMIT 5 OFFSET 10;
```

Skip first 10 rows.

Return next 5.

* * *

MySQL shortcut

```SQL
LIMIT 10,5;
```

Means

Skip 10.

Return 5.

* * *

Example

Table

| ID |
| --- |
| 1 |
| 2 |
| 3 |
| 4 |
| 5 |
| 6 |
| 7 |

Query

```SQL
SELECT *
FROM Student
LIMIT 3;
```

Output

```
1
2
3
```

* * *

## Top N Highest Salary

```SQL
SELECT *
FROM Employee
ORDER BY Salary DESC
LIMIT 5;
```

Returns top 5 highest-paid employees.

Very common interview question.

* * *

## Interview Question

Does LIMIT guarantee order?

No.

Without `ORDER BY`, the database can return rows in any order.

* * *

# Complete SELECT Syntax

The logical order of clauses in a query is:

```SQL
SELECT column_list
FROM table_name
WHERE condition
GROUP BY columns
HAVING condition
ORDER BY columns
LIMIT n;
```

Not every clause is required.

* * *

# Basic Execution Flow (Concept)

Although we write

```SQL
SELECT Name
FROM Student;
```

The DBMS conceptually:

1. Finds the table.
2. Reads rows.
3. Returns requested columns.

A more detailed execution order will be covered in **Part 6**.

* * *

# Real-World Example

Customer Table

| ID | Name | City |
| --- | --- | --- |
| 1 | John | Delhi |
| 2 | Alice | Mumbai |

Need only names.

```SQL
SELECT Name
FROM Customer;
```

Need all details.

```SQL
SELECT *
FROM Customer;
```

Need unique cities.

```SQL
SELECT DISTINCT City
FROM Customer;
```

Need first 10 customers.

```SQL
SELECT *
FROM Customer
LIMIT 10;
```

* * *

# Interview Questions (Part 1)

### Basic

1. What is SELECT?
2. Difference between SELECT and INSERT.
3. Difference between SELECT * and selecting columns.
4. What is DUAL?
5. Can SELECT work without FROM?

* * *

### Intermediate

6. Why avoid SELECT *?
7. What is alias?
8. Difference between alias and rename.
9. Difference between DISTINCT and UNIQUE.
10. Does LIMIT guarantee order?

* * *

### Advanced

11. Why is `SELECT *` discouraged in production?
12. Why are table aliases important in joins?
13. How does DISTINCT work on multiple columns?
14. Why should LIMIT almost always be paired with ORDER BY?

* * *

# MODULE 6 (Part 2) – Filtering Data

Filtering means retrieving **only the rows that satisfy certain conditions**.

Without filtering:

```SQL
SELECT *
FROM Student;
```

All rows are returned.

With filtering:

```SQL
SELECT *
FROM Student
WHERE Age > 20;
```

Only matching rows are returned.

* * *

# WHERE

The `WHERE` clause filters rows.

Syntax

```SQL
SELECT columns
FROM table
WHERE condition;
```

Example

```SQL
SELECT *
FROM Student
WHERE Age > 20;
```

Output

| StudentID | Name | Age |
| --- | --- | --- |
| 3 | Bob | 21 |

* * *

# Comparison Operators

| Operator | Meaning |
| --- | --- |
| = | Equal |
| != or <> | Not equal |
| > | Greater than |
| < | Less than |
| >= | Greater than or equal |
| <= | Less than or equal |

Examples

```SQL
SELECT *
FROM Student
WHERE Age = 20;
```

```SQL
SELECT *
FROM Student
WHERE Age >= 18;
```

```SQL
SELECT *
FROM Student
WHERE Department <> 'CSE';
```

* * *

# BETWEEN

Used for ranges.

Inclusive.

Syntax

```SQL
SELECT *
FROM Student
WHERE Age BETWEEN 18 AND 22;
```

Equivalent to

```SQL
WHERE Age >= 18
AND Age <= 22
```

* * *

Example

Age

18

19

20

21

22

All returned.

17 and 23 are excluded.

* * *

Interview Question

Is BETWEEN inclusive?

Yes.

Both endpoints are included.

* * *

# IN

Used instead of multiple OR conditions.

Without IN

```SQL
SELECT *
FROM Student
WHERE Department='CSE'
OR Department='IT'
OR Department='ECE';
```

Using IN

```SQL
SELECT *
FROM Student
WHERE Department IN ('CSE','IT','ECE');
```

Cleaner and easier to read.

* * *

# NOT IN

Returns rows whose values are **not** in the given list.

```SQL
SELECT *
FROM Student
WHERE Department NOT IN ('CSE','ECE');
```

Returns students from all other departments.

* * *

# IS NULL

Never compare NULL using `=`.

Wrong

```SQL
WHERE ManagerID = NULL
```

Correct

```SQL
WHERE ManagerID IS NULL
```

Find employees without managers.

```SQL
SELECT *
FROM Employee
WHERE ManagerID IS NULL;
```

* * *

Similarly

```SQL
WHERE ManagerID IS NOT NULL
```

Finds employees that do have a manager.

* * *

## Interview Question

Why doesn't `= NULL` work?

Because `NULL` means **unknown**, not a value. SQL uses `IS NULL` and `IS NOT NULL` to test for nulls.

* * *

# Logical Operators

## AND

Both conditions must be true.

```SQL
SELECT *
FROM Student
WHERE Age > 18
AND Department='CSE';
```

* * *

## OR

Either condition can be true.

```SQL
SELECT *
FROM Student
WHERE Department='CSE'
OR Department='IT';
```

* * *

## NOT

Negates a condition.

```SQL
SELECT *
FROM Student
WHERE NOT Department='CSE';
```

Equivalent to

```SQL
WHERE Department <> 'CSE';
```

* * *

# Combining Conditions

Example

```SQL
SELECT *
FROM Student
WHERE Age BETWEEN 18 AND 22
AND Department IN ('CSE','IT')
AND Name IS NOT NULL;
```

This is very common in interviews.

* * *

# Real-World Example

Employee Table

| Name | Department | Salary |
| --- | --- | --- |
| John | IT | 60000 |
| Alice | HR | 50000 |
| Bob | IT | 70000 |

Employees in IT

```SQL
SELECT *
FROM Employee
WHERE Department='IT';
```

Employees with salary between 50000 and 70000

```SQL
SELECT *
FROM Employee
WHERE Salary BETWEEN 50000 AND 70000;
```

Employees not in HR

```SQL
SELECT *
FROM Employee
WHERE Department NOT IN ('HR');
```

* * *

# Interview Pitfalls

### Pitfall 1

Using

```SQL
WHERE Salary = NULL;
```

Wrong.

Use

```SQL
WHERE Salary IS NULL;
```

* * *

### Pitfall 2

Forgetting that BETWEEN is inclusive.

* * *

### Pitfall 3

Using many OR conditions instead of IN.

Poor readability.

* * *

### Pitfall 4

Writing

```SQL
WHERE Age > 18
OR Department='IT'
AND Salary > 50000;
```

Because `AND` has higher precedence than `OR`, this is interpreted as:

```SQL
WHERE Age > 18
OR (Department='IT' AND Salary > 50000);
```

If you mean something else, use parentheses.

* * *

### Pitfall 5

Using `NOT IN` with a list that contains `NULL`.

Example:

```SQL
WHERE DepartmentID NOT IN (1, 2, NULL);
```

This can produce unexpected results because comparisons with `NULL` evaluate to unknown. Be careful when `NULL` values may be present.

* * *

# Most Asked Interview Questions

1. Difference between WHERE and HAVING (covered in Part 5).
2. Why is `IS NULL` used instead of `= NULL`?
3. Is `BETWEEN` inclusive?
4. Difference between `IN` and multiple `OR`s.
5. Difference between `NOT IN` and `NOT EXISTS` (covered with subqueries).
6. Which operator has higher precedence: `AND` or `OR`?
7. Can WHERE use aggregate functions?

**Answer:** No. Aggregate functions are evaluated after WHERE. Use `HAVING` for filtering aggregated results.

* * *

# Quick Revision

### Part 1

* `SELECT` retrieves data.
* `SELECT *` returns all columns but is usually avoided in production.
* Use column names to fetch only required data.
* `DUAL` allows expressions without a user table.
* Aliases (`AS`) provide temporary names.
* `DISTINCT` removes duplicate rows from the result.
* `LIMIT` restricts the number of returned rows and should generally be used with `ORDER BY`.

### Part 2

* `WHERE` filters rows before they are returned.
* Comparison operators (`=`, `>`, `<`, `>=`, `<=`, `<>`) define filter conditions.
* `BETWEEN` checks an inclusive range.
* `IN` and `NOT IN` simplify multiple comparisons.
* Use `IS NULL` and `IS NOT NULL` for null checks.
* `AND`, `OR`, and `NOT` combine conditions; remember that `AND` has higher precedence than `OR`.

* * *

**You:**

Part 3 – Pattern Matching
LIKE
% wildcard
_ wildcard
Escaping wildcard characters
Case sensitivity (DBMS differences)
Real interview questions

Part 4 – Sorting & Aggregation
ORDER BY
COUNT
SUM
AVG
MIN
MAX
DISTINCT with aggregates
NULL behavior in aggregates

* * *

**ChatGPT:**

Excellent. These two topics are **asked in almost every SQL interview**. Especially **`LIKE`, `ORDER BY`, `COUNT`, `SUM`, `AVG`** are among the most frequently tested concepts.

* * *

# MODULE 6 – Part 3 : Pattern Matching

Pattern matching is used when you **don't know the exact value**.

Suppose your database contains

| Name |
| --- |
| John |
| Johnny |
| Johnson |
| Alice |
| Bob |

Now you want

> Find every student whose name starts with **John**

You don't know the complete name.

This is where **LIKE** comes in.

* * *

# LIKE Operator

## What is LIKE?

LIKE is used to search for a pattern in a string.

Instead of exact matching

```SQL
WHERE Name='John'
```

we write

```SQL
WHERE Name LIKE 'John%'
```

* * *

## Syntax

```SQL
SELECT columns
FROM table
WHERE column LIKE pattern;
```

* * *

Suppose

| Name |
| --- |
| John |
| Johnny |
| Johnson |
| Alice |

Query

```SQL
SELECT *
FROM Student
WHERE Name LIKE 'John%';
```

Output

| Name |
| --- |
| John |
| Johnny |

Notice

Johnson is NOT returned because it starts with

```
Johns
```

not

```
John
```

* * *

# Wildcards

Wildcards are special symbols used with LIKE.

There are mainly two:

```
%

_
```

* * *

# % Wildcard

Most important wildcard.

Means

> Zero or more characters.

Think of it as

```
*
```

in regular expressions.

* * *

## Starts With

Find names starting with J

```SQL
SELECT *
FROM Student
WHERE Name LIKE 'J%';
```

Matches

```
John

Johnny

James

Jack
```

* * *

## Ends With

Find names ending with n

```SQL
SELECT *
FROM Student
WHERE Name LIKE '%n';
```

Matches

```
John

Mohan

Karan
```

* * *

## Contains

Find names containing "oh"

```SQL
SELECT *
FROM Student
WHERE Name LIKE '%oh%';
```

Matches

```
John

Johnson

Mohan
```

* * *

## Everything

```SQL
LIKE '%'
```

Matches every non-NULL string.

Equivalent to selecting all rows (for non-null values).

* * *

# Interview Trick

Difference

```SQL
LIKE 'John%'
```

vs

```SQL
LIKE '%John%'
```

First

↓

Starts with John.

Second

↓

Contains John anywhere.

* * *

# _ Wildcard

Means

Exactly one character.

This is where students get confused.

* * *

Suppose

Names

```
Ram

Ramy

Ravi

Raj

Rohan
```

Query

```SQL
WHERE Name LIKE 'Ra_'
```

Matches

```
Ram

Raj
```

Only

Three-letter names.

* * *

Another example

```SQL
LIKE 'J___'
```

Matches exactly

4-letter names beginning with J.

```
John

Jack
```

Not

```
Johnny
```

because Johnny has six letters.

* * *

## Difference

```
%
```

↓

Any number of characters.

```
_
```

↓

Exactly one character.

* * *

Example

```
LIKE 'A%'
```

Matches

```
A

AB

ABC

ABCDE
```

* * *

```
LIKE 'A_'
```

Matches

```
AB
```

Only.

* * *

# Combining % and _

Suppose

```SQL
LIKE 'A_%'
```

Meaning

Starts with

```
A
```

Then exactly one character.

Then anything.

Matches

```
AB

ABC

APPLE

AXYZ
```

* * *

Another

```SQL
LIKE '__a%'
```

Means

First two characters

↓

Anything

Third character

↓

a

Remaining

↓

Anything.

* * *

# Escaping Wildcards

Suppose your data actually contains

```
100%

50%

90%
```

Now you want

```
100%
```

not

everything beginning with

* * *

Normally

```SQL
LIKE '100%'
```

means

```
100 followed by anything.
```

Not literal %.

* * *

Use ESCAPE.

Example

```SQL
SELECT *
FROM Products
WHERE Discount LIKE '100\%'
ESCAPE '\';
```

Now

```
%
```

is treated as a normal character.

* * *

Similarly

Suppose

Name

```
A_B
```

Need underscore literally.

```SQL
LIKE 'A\_B'
ESCAPE '\'
```

* * *

Interview Question

Why ESCAPE?

Because

```
%
```

and

```
_
```

normally behave as wildcards.

* * *

# Case Sensitivity

Very important.

Students think SQL is always case-sensitive.

Wrong.

It depends on DBMS.

* * *

## MySQL

Usually

```
LIKE
```

is **case-insensitive** under common collations.

Example

```SQL
LIKE 'john%'
```

matches

```
John

JOHN

john
```

* * *

## PostgreSQL

LIKE is usually case-sensitive.

Need

```
ILIKE
```

for case-insensitive matching.

Example

```SQL
WHERE Name ILIKE 'john%'
```

* * *

## SQL Server

Depends on database collation.

* * *

Interview Answer

Is LIKE case-sensitive?

Answer:

> It depends on the DBMS and collation.

* * *

# NOT LIKE

Opposite.

Example

```SQL
SELECT *
FROM Student
WHERE Name NOT LIKE 'J%';
```

Returns

Everyone

Except names beginning with J.

* * *

# Real World Examples

Find Gmail users

```SQL
SELECT *
FROM Users
WHERE Email LIKE '%@gmail.com';
```

* * *

Find PDF files

```SQL
WHERE FileName LIKE '%.pdf';
```

* * *

Find Indian phone numbers

```SQL
WHERE Phone LIKE '98%';
```

* * *

Find employees whose second letter is A

```SQL
WHERE Name LIKE '_a%';
```

* * *

# Common Interview Questions (LIKE)

### Basic

Difference between

```
=
```

and

```
LIKE
```

Answer

```
=
```

Exact match.

LIKE

Pattern match.

* * *

Difference

```
%
```

vs

```
_
```

* * *

Does LIKE work on numbers?

Usually it's intended for character data, though many databases implicitly convert values to strings.

* * *

Can LIKE use indexes?

Sometimes.

```
LIKE 'John%'
```

Often can use an index.

```
LIKE '%John%'
```

Usually cannot efficiently use a normal B-tree index because the pattern starts with a wildcard.

Very common optimization question.

* * *

# MODULE 6 – Part 4 : Sorting & Aggregation

* * *

# ORDER BY

Without ORDER BY

Database can return rows in any order.

Never assume insertion order.

* * *

Example

```SQL
SELECT *
FROM Employee;
```

Output could be

```
John

Alice

Bob
```

Tomorrow

```
Bob

John

Alice
```

No guarantee.

* * *

Need sorting.

* * *

## Syntax

```SQL
SELECT columns
FROM table
ORDER BY column;
```

* * *

Ascending

(Default)

```SQL
ORDER BY Salary ASC;
```

Descending

```SQL
ORDER BY Salary DESC;
```

* * *

Example

Salary

```
50000

30000

70000
```

Query

```SQL
ORDER BY Salary ASC;
```

Output

```
30000

50000

70000
```

* * *

Descending

```
70000

50000

30000
```

* * *

# Sorting on Multiple Columns

Example

```SQL
ORDER BY Department,
Salary DESC;
```

Meaning

First

Sort departments alphabetically.

Inside each department

Sort salary descending.

* * *

# ORDER BY Alias

```SQL
SELECT Salary*12 AS AnnualSalary

FROM Employee

ORDER BY AnnualSalary DESC;
```

Allowed.

* * *

# Aggregate Functions

Aggregate

↓

Works on multiple rows.

Returns

One value.

* * *

Main functions

```
COUNT

SUM

AVG

MIN

MAX
```

* * *

# COUNT()

Returns

Number of rows.

* * *

Example

```SQL
SELECT COUNT(*)

FROM Student;
```

Suppose

5 students.

Output

```
5
```

* * *

COUNT(column)

Counts only non-NULL values.

Example

ManagerID

```
1

2

NULL

4
```

```SQL
SELECT COUNT(ManagerID)
FROM Employee;
```

Output

```
3
```

NULL ignored.

* * *

Difference

```
COUNT(*)
```

Counts rows.

```
COUNT(column)
```

Counts non-NULL values.

Very common interview question.

* * *

# SUM()

Adds numbers.

Example

Salary

```
20000

30000

50000
```

Query

```SQL
SELECT SUM(Salary)

FROM Employee;
```

Output

```
100000
```

* * *

# AVG()

Returns average.

```SQL
SELECT AVG(Salary)

FROM Employee;
```

Output

```
33333.33
```

* * *

Important

NULL ignored.

* * *

# MIN()

Returns smallest value.

Example

```SQL
SELECT MIN(Salary)

FROM Employee;
```

Output

```
20000
```

* * *

# MAX()

Largest value.

```SQL
SELECT MAX(Salary)

FROM Employee;
```

Output

```
50000
```

* * *

# DISTINCT with Aggregates

Suppose

Salary

```
100

100

200

300
```

* * *

Without DISTINCT

```SQL
SELECT SUM(Salary)
```

Output

```
700
```

* * *

With DISTINCT

```SQL
SELECT SUM(DISTINCT Salary)
```

Output

```
600
```

Because duplicate

100

counted once.

* * *

Another

```SQL
COUNT(DISTINCT Department)
```

Suppose

```
CSE

CSE

ECE

IT
```

Output

```
3
```

Very common interview question.

* * *

# NULL Behavior

Extremely important.

Suppose

Salary

```
100

200

NULL

300
```

* * *

COUNT(*)

↓

4

* * *

COUNT(Salary)

↓

3

* * *

SUM(Salary)

↓

600

NULL ignored.

* * *

AVG(Salary)

↓

200

NULL ignored.

* * *

MIN()

Ignores NULL.

* * *

MAX()

Ignores NULL.

* * *

Interview Question

Do aggregate functions consider NULL?

Except

```
COUNT(*)
```

Most aggregate functions ignore NULL values.

* * *

# Real World Example

Employee

| Salary |
| --- |
| 40000 |
| 50000 |
| 60000 |

Highest Salary

```SQL
SELECT MAX(Salary)
FROM Employee;
```

* * *

Average Salary

```SQL
SELECT AVG(Salary)
FROM Employee;
```

* * *

Number of Employees

```SQL
SELECT COUNT(*)
FROM Employee;
```

* * *

Total Salary

```SQL
SELECT SUM(Salary)
FROM Employee;
```

* * *

# ORDER BY + LIMIT

Very common interview question.

Top 5 salaries

```SQL
SELECT *
FROM Employee
ORDER BY Salary DESC
LIMIT 5;
```

* * *

Lowest salary

```SQL
SELECT *
FROM Employee
ORDER BY Salary ASC
LIMIT 1;
```

* * *

Second highest salary (basic approach)

```SQL
SELECT DISTINCT Salary
FROM Employee
ORDER BY Salary DESC
LIMIT 1 OFFSET 1;
```

(There are several ways to solve this; you'll learn better approaches later using subqueries and window functions.)

* * *

# Common Interview Pitfalls

## Pitfall 1

Thinking COUNT(column)

Counts NULL.

Wrong.

It ignores NULL.

* * *

## Pitfall 2

Forgetting

ORDER BY

default

↓

ASC.

* * *

## Pitfall 3

Using aggregate function in WHERE

Wrong

```SQL
SELECT *
FROM Employee
WHERE AVG(Salary)>50000;
```

Correct

```SQL
SELECT AVG(Salary)
FROM Employee
HAVING AVG(Salary)>50000;
```

Or use a subquery, depending on the requirement.

* * *

## Pitfall 4

Using LIKE

instead of

=

for exact matches.

Use

```SQL
WHERE Name='John'
```

if exact matching is needed.

* * *

## Pitfall 5

Believing database returns sorted rows automatically.

Never assume this.

Always use

ORDER BY.

* * *

# Most Asked Interview Questions

### Pattern Matching

1. Difference between `=` and `LIKE`.
2. Difference between `%` and `_`.
3. What is `ESCAPE`?
4. Is `LIKE` case-sensitive?
5. Can `LIKE '%abc%'` use an index efficiently?

* * *

### Sorting & Aggregation

6. Difference between `COUNT(*)` and `COUNT(column)`.
7. Does `AVG()` include NULL?
8. Difference between `COUNT(DISTINCT column)` and `DISTINCT`.
9. Can you use aggregate functions in `WHERE`?
10. Why should `ORDER BY` be used with `LIMIT`?

* * *

# Quick Revision (5 Minutes)

## Pattern Matching

* `LIKE` performs pattern matching on strings.
* `%` matches **zero or more characters**.
* `_` matches **exactly one character**.
* `NOT LIKE` returns rows that do not match the pattern.
* Use `ESCAPE` when you need `%` or `_` to be treated as normal characters.
* Case sensitivity depends on the **DBMS and its collation**.
* Prefix searches like `LIKE 'abc%'` can often use indexes, while leading wildcard searches like `LIKE '%abc%'` usually cannot.

* * *

## Sorting & Aggregation

* `ORDER BY` sorts the result set (`ASC` by default, `DESC` for descending).
* Multiple columns can be used in `ORDER BY`.
* `COUNT(*)` counts all rows.
* `COUNT(column)` counts only non-`NULL` values.
* `SUM`, `AVG`, `MIN`, and `MAX` ignore `NULL` values.
* `DISTINCT` can be combined with aggregate functions, e.g., `COUNT(DISTINCT Department)` or `SUM(DISTINCT Salary)`.
* Always pair `LIMIT` with `ORDER BY` when you need the "top N" or "bottom N" rows.

* * *

**You:**

Part 5 – GROUP BY & HAVING (Very Important)
GROUP BY
HAVING
WHERE vs HAVING
Multiple column grouping
Aggregate execution
Common interview mistakes
Complex examples

Part 6 – SQL Execution Order (One of the Most Asked)
Actual execution order
FROM
WHERE
GROUP BY
HAVING
SELECT
DISTINCT
ORDER BY
LIMIT
Why aliases don't work in WHERE
Tricky interview questions
Complete revision sheet

* * *

**ChatGPT:**

This is the **most important topic of SQL**.

If I had to choose only **one SQL topic** for interviews, it would be:

> **GROUP BY + HAVING + SQL Execution Order**

Almost every company asks at least one question from this.

* * *

# MODULE 6 – Part 5 : GROUP BY & HAVING

* * *

# Why do we need GROUP BY?

Suppose Employee table

| EmpID | Name | Department | Salary |
| --- | --- | --- | --- |
| 1 | John | IT | 50000 |
| 2 | Alice | HR | 40000 |
| 3 | Bob | IT | 70000 |
| 4 | David | HR | 45000 |
| 5 | Emma | Sales | 60000 |

Manager asks

> "What is the average salary of each department?"

Without GROUP BY,

you only get

```SQL
SELECT AVG(Salary)
FROM Employee;
```

Output

```
53000
```

Average of entire company.

But manager wants

```
IT

↓

60000

HR

↓

42500

Sales

↓

60000
```

Need grouping.

* * *

# What is GROUP BY?

Definition

GROUP BY groups rows having the same value into one group.

Then aggregate functions are applied **group-wise**, not on the entire table.

Think of it like sorting students into classrooms before calculating averages.

Without GROUP BY

```
Whole class

↓

Average
```

With GROUP BY

```
Each classroom

↓

Average
```

* * *

# Basic Syntax

```SQL
SELECT column_name,
aggregate_function(column)

FROM table

GROUP BY column_name;
```

* * *

Example

```SQL
SELECT Department,
COUNT(*)

FROM Employee

GROUP BY Department;
```

Output

| Department | Employees |
| --- | --- |
| IT | 2 |
| HR | 2 |
| Sales | 1 |

* * *

# Another Example

Average Salary

```SQL
SELECT Department,

AVG(Salary)

FROM Employee

GROUP BY Department;
```

Output

| Department | Average Salary |
| --- | --- |
| IT | 60000 |
| HR | 42500 |
| Sales | 60000 |

* * *

# GROUP BY using SUM

```SQL
SELECT Department,

SUM(Salary)

FROM Employee

GROUP BY Department;
```

Output

| Department | Total Salary |
| --- | --- |
| IT | 120000 |
| HR | 85000 |
| Sales | 60000 |

* * *

# GROUP BY using MAX

Highest salary per department

```SQL
SELECT Department,

MAX(Salary)

FROM Employee

GROUP BY Department;
```

Output

| Department | Highest Salary |
| --- | --- |
| IT | 70000 |
| HR | 45000 |
| Sales | 60000 |

* * *

# GROUP BY Rules

Very important interview question.

Suppose

```SQL
SELECT Department,

AVG(Salary)

FROM Employee

GROUP BY Department;
```

Correct.

* * *

Now

```SQL
SELECT Name,

Department,

AVG(Salary)

FROM Employee

GROUP BY Department;
```

Wrong.

Why?

Because

```
Department

↓

IT
```

contains

```
John

Bob
```

Which Name should SQL show?

John?

Bob?

Impossible.

Hence error (in standards-compliant SQL).

* * *

Rule

Every selected column must be

* inside GROUP BY

OR

* inside an aggregate function.

* * *

Correct

```SQL
SELECT Department,

AVG(Salary)

FROM Employee

GROUP BY Department;
```

Correct

```SQL
SELECT Department,

COUNT(*)

FROM Employee

GROUP BY Department;
```

Wrong

```SQL
SELECT Name,

Department

FROM Employee

GROUP BY Department;
```

* * *

# Multiple Column GROUP BY

Suppose

| Department | Gender | Salary |
| --- | --- | --- |
| IT | Male | 50000 |
| IT | Female | 70000 |
| HR | Female | 40000 |
| HR | Male | 45000 |

Need

Average salary

for

Department + Gender.

* * *

```SQL
SELECT Department,

Gender,

AVG(Salary)

FROM Employee

GROUP BY Department,

Gender;
```

Output

| Department | Gender | Average |
| --- | --- | --- |
| IT | Male | 50000 |
| IT | Female | 70000 |
| HR | Male | 45000 |
| HR | Female | 40000 |

* * *

Grouping becomes

```
(IT,Male)

(IT,Female)

(HR,Male)

(HR,Female)
```

* * *

# HAVING

Most asked interview topic.

* * *

Suppose

Need

Departments

having

more than

5 employees.

* * *

Can we write

```SQL
SELECT Department,

COUNT(*)

FROM Employee

WHERE COUNT(*)>5

GROUP BY Department;
```

No.

Wrong.

COUNT()

doesn't exist yet.

* * *

Need

HAVING.

* * *

Syntax

```SQL
SELECT Department,

COUNT(*)

FROM Employee

GROUP BY Department

HAVING COUNT(*)>5;
```

* * *

Execution

First

Make groups.

↓

Calculate COUNT.

↓

Apply HAVING.

* * *

Example

Employee

| Department |
| --- |
| IT |
| IT |
| HR |
| HR |
| HR |
| Sales |

GROUP BY

↓

IT

↓

2

HR

↓

3

Sales

↓

1

HAVING

```SQL
COUNT(*)>=2
```

Output

| Department |
| --- |
| IT |
| HR |

* * *

# WHERE vs HAVING

Most important interview question.

| WHERE | HAVING |
| --- | --- |
| Filters rows | Filters groups |
| Before GROUP BY | After GROUP BY |
| Aggregate functions not allowed | Aggregate functions allowed |

* * *

Example

Find

Employees

earning

more than

```SQL
SELECT *

FROM Employee

WHERE Salary>50000;
```

WHERE filters rows.

* * *

Now

Need

Departments

whose

average salary

```SQL
SELECT Department,

AVG(Salary)

FROM Employee

GROUP BY Department

HAVING AVG(Salary)>60000;
```

HAVING filters groups.

* * *

Memory Trick

WHERE

↓

Individual rows

HAVING

↓

Groups

* * *

# WHERE + GROUP BY + HAVING Together

Suppose

Need

Average salary

of

IT and HR

departments

only

whose average salary

```SQL
SELECT Department,

AVG(Salary)

FROM Employee

WHERE Department IN ('IT','HR')

GROUP BY Department

HAVING AVG(Salary)>45000;
```

Execution

WHERE

↓

Keep IT HR rows

↓

GROUP

↓

AVG

↓

HAVING

↓

Final result

* * *

# Aggregate Execution

Suppose

Table

| Salary |
| --- |
| 100 |
| 200 |
| 300 |

```SQL
SELECT AVG(Salary)
```

Execution

```
100

200

300

↓

AVG

↓

200
```

With GROUP BY

```
IT

↓

50000

70000

↓

AVG

↓

60000
```

* * *

# Complex Example

Orders

| Customer | Amount |
| --- | --- |
| A | 100 |
| A | 300 |
| A | 200 |
| B | 50 |
| B | 60 |
| C | 900 |

Need

Customers

whose total purchase

300

```SQL
SELECT Customer,

SUM(Amount)

FROM Orders

GROUP BY Customer

HAVING SUM(Amount)>300;
```

Output

| Customer | Total |
| --- | --- |
| A | 600 |
| C | 900 |

* * *

Need

Customers

with

more than

3 orders

```SQL
SELECT Customer,

COUNT(*)

FROM Orders

GROUP BY Customer

HAVING COUNT(*)>3;
```

* * *

Need

Highest salary

of each department

whose highest salary

100000

```SQL
SELECT Department,

MAX(Salary)

FROM Employee

GROUP BY Department

HAVING MAX(Salary)>100000;
```

* * *

# Common Interview Mistakes

* * *

## Mistake 1

Using aggregate in WHERE

Wrong

```SQL
WHERE AVG(Salary)>50000;
```

Correct

```SQL
HAVING AVG(Salary)>50000;
```

* * *

## Mistake 2

Selecting columns

not in GROUP BY

Wrong

```SQL
SELECT Name,

AVG(Salary)

GROUP BY Department;
```

* * *

## Mistake 3

Thinking HAVING replaces WHERE.

Wrong.

Use WHERE whenever possible because it filters earlier and is generally more efficient.

* * *

## Mistake 4

Using HAVING without GROUP BY

It is allowed in many SQL databases.

Entire table becomes one group.

Example

```SQL
SELECT COUNT(*)

FROM Employee

HAVING COUNT(*)>5;
```

* * *

# Interview Questions

Difference between GROUP BY and ORDER BY?

GROUP BY

Creates groups.

ORDER BY

Sorts rows.

* * *

Can HAVING exist without GROUP BY?

Yes.

Entire result becomes one group.

* * *

Can WHERE use aggregate functions?

No.

* * *

Can HAVING use non-aggregate columns?

Yes, but usually those columns should also appear in the GROUP BY (or be functionally dependent on it, depending on the DBMS).

* * *

# MODULE 6 – Part 6 : SQL Execution Order

This is probably the **most misunderstood topic** in SQL.

Every interview asks it.

* * *

# Biggest Confusion

We write

```SQL
SELECT Name

FROM Employee

WHERE Salary>50000;
```

Students think

Execution

↓

SELECT

↓

FROM

↓

WHERE

Wrong.

SQL does NOT execute

top to bottom.

* * *

# Actual SQL Execution Order

```
1 FROM

↓

2 WHERE

↓

3 GROUP BY

↓

4 HAVING

↓

5 SELECT

↓

6 DISTINCT

↓

7 ORDER BY

↓

8 LIMIT
```

Memorize this.

* * *

# Step 1 : FROM

Load table.

```SQL
FROM Employee
```

Database first finds the table.

* * *

# Step 2 : WHERE

Filter rows.

```SQL
WHERE Salary>50000
```

Rows removed.

* * *

# Step 3 : GROUP BY

Remaining rows

↓

Groups created.

* * *

# Step 4 : HAVING

Groups filtered.

* * *

# Step 5 : SELECT

Columns selected.

Expressions calculated.

Aliases created.

* * *

# Step 6 : DISTINCT

Duplicate rows removed.

* * *

# Step 7 : ORDER BY

Rows sorted.

* * *

# Step 8 : LIMIT

Return first N rows.

* * *

# Visual Flow

```
Employee Table

↓

FROM

↓

WHERE

↓

GROUP BY

↓

HAVING

↓

SELECT

↓

DISTINCT

↓

ORDER BY

↓

LIMIT

↓

Output
```

* * *

# Why Alias Doesn't Work in WHERE

Interview favorite.

Query

```SQL
SELECT Salary*12 AS AnnualSalary

FROM Employee

WHERE AnnualSalary>500000;
```

Error.

Why?

Because

WHERE

executes

before

SELECT.

Alias

doesn't exist yet.

* * *

Correct

```SQL
SELECT Salary*12 AS AnnualSalary

FROM Employee

WHERE Salary*12>500000;
```

Or use a subquery/CTE if you want to reuse the alias.

* * *

But

ORDER BY

works.

```SQL
SELECT Salary*12 AS AnnualSalary

FROM Employee

ORDER BY AnnualSalary;
```

Because

ORDER BY

comes after

SELECT.

* * *

# Execution Example

Employee

| Name | Dept | Salary |
| --- | --- | --- |
| John | IT | 50000 |
| Bob | IT | 70000 |
| Alice | HR | 40000 |

Query

```SQL
SELECT Department,

AVG(Salary)

FROM Employee

WHERE Salary>45000

GROUP BY Department

HAVING AVG(Salary)>55000

ORDER BY AVG(Salary);
```

Execution

FROM

↓

All rows

↓

WHERE

↓

John

Bob

↓

GROUP

↓

IT

↓

AVG

↓

60000

↓

HAVING

↓

60000>55000

↓

SELECT

↓

Department

Average

↓

ORDER BY

↓

Final answer

* * *

# Tricky Interview Questions

* * *

## Question 1

Why doesn't alias work in WHERE?

Answer

WHERE executes before SELECT.

* * *

## Question 2

Why can't WHERE use aggregate functions?

Because

Aggregation happens after WHERE.

* * *

## Question 3

Why can ORDER BY use alias?

Because ORDER BY executes after SELECT.

* * *

## Question 4

Can HAVING use aliases?

It depends on the DBMS.

* MySQL often allows it.
* Standard SQL generally does not.
* PostgreSQL and SQL Server are stricter.

In interviews, avoid relying on aliases in HAVING unless you know the specific database behavior.

* * *

## Question 5

Difference

DISTINCT

vs

GROUP BY

DISTINCT

↓

Remove duplicates.

GROUP BY

↓

Create groups for aggregation.

* * *

# Complete Revision Sheet

## GROUP BY

* Creates groups based on one or more columns.
* Every non-aggregated selected column should appear in the GROUP BY (standard SQL).
* Aggregate functions operate on each group.

* * *

## HAVING

* Filters groups after aggregation.
* Used with aggregate functions.
* Executes after GROUP BY.

* * *

## WHERE

* Filters rows before grouping.
* Cannot use aggregate functions.

* * *

## WHERE vs HAVING

| WHERE | HAVING |
| --- | --- |
| Filters rows | Filters groups |
| Before GROUP BY | After GROUP BY |
| No aggregates | Aggregates allowed |

* * *

## SQL Execution Order (Memorize)

```
FROM
↓
WHERE
↓
GROUP BY
↓
HAVING
↓
SELECT
↓
DISTINCT
↓
ORDER BY
↓
LIMIT
```

* * *

# Top 20 Interview Questions from These Two Parts

1. What is GROUP BY?
2. Why do we use GROUP BY?
3. Difference between GROUP BY and ORDER BY?
4. Difference between WHERE and HAVING?
5. Can HAVING be used without GROUP BY?
6. Can WHERE use aggregate functions?
7. Can HAVING use aggregate functions?
8. Explain SQL execution order.
9. Why doesn't an alias work in WHERE?
10. Why does an alias work in ORDER BY?
11. Why is WHERE usually faster than HAVING?
12. What happens if a selected column is not in GROUP BY?
13. Can GROUP BY have multiple columns?
14. What does `COUNT(*)` return after GROUP BY?
15. How do you find departments with more than 10 employees?
16. How do you find the average salary of each department?
17. How do you find departments with an average salary greater than ₹50,000?
18. What is the difference between `DISTINCT` and `GROUP BY`?
19. At which stage is `LIMIT` applied?
20. In what order are `WHERE`, `GROUP BY`, `HAVING`, and `ORDER BY` executed?

* * *

## Interview Tip

If you remember **only one thing** from SQL, remember this execution order:

```
FROM
→ WHERE
→ GROUP BY
→ HAVING
→ SELECT
→ DISTINCT
→ ORDER BY
→ LIMIT
```

Understanding this single sequence explains:

* Why aliases don't work in `WHERE`
* Why aggregate functions can't be used in `WHERE`
* Why `HAVING` exists
* Why `ORDER BY` can use aliases

Many seemingly confusing SQL behaviors become straightforward once you know this execution order.

* * *

**You:**

Module 7 – Joins
INNER JOIN
LEFT JOIN
RIGHT JOIN
FULL JOIN
CROSS JOIN
SELF JOIN
Aliases
Real interview examples
Visual explanation

* * *

**ChatGPT:**

This is **the second most important SQL topic after SELECT**.

If you master **Joins**, you can solve **70–80% of SQL interview questions**.

Companies like Amazon, Google, Microsoft, Oracle, Walmart, Adobe, Atlassian, etc., ask joins in almost every SQL round.

* * *

# MODULE 7 – SQL JOINS

# What is a JOIN?

## Definition

A JOIN is used to **combine rows from two or more tables** based on a related column.

Think about a real college database.

### Student Table

| StudentID | Name | DeptID |
| --- | --- | --- |
| 1 | John | 101 |
| 2 | Alice | 102 |
| 3 | Bob | 101 |
| 4 | David | 103 |

* * *

### Department Table

| DeptID | Department |
| --- | --- |
| 101 | CSE |
| 102 | ECE |
| 104 | MBA |

Notice

Student table

knows

```
DeptID
```

Department table

knows

```
Department Name
```

Need

```
John → CSE
Alice → ECE
Bob → CSE
```

No single table has complete information.

Need JOIN.

* * *

# Why are JOINs needed?

Without JOIN

You would first fetch

```
DeptID = 101
```

Then run another query

```
Department = CSE
```

Very inefficient.

JOIN lets SQL combine related data in one query.

* * *

# Foreign Key Review

Student Table

```
DeptID
```

↓

Foreign Key

↓

References

Department Table

```
DeptID
```

This relationship is what JOIN uses.

* * *

# Types of JOIN

There are six major joins.

```
1. INNER JOIN

2. LEFT JOIN

3. RIGHT JOIN

4. FULL OUTER JOIN

5. CROSS JOIN

6. SELF JOIN
```

* * *

# Sample Tables

We'll use these throughout.

## Student

| StudentID | Name | DeptID |
| --- | --- | --- |
| 1 | John | 101 |
| 2 | Alice | 102 |
| 3 | Bob | 101 |
| 4 | David | 103 |

* * *

## Department

| DeptID | Department |
| --- | --- |
| 101 | CSE |
| 102 | ECE |
| 104 | MBA |

Notice

Student

DeptID

103

does NOT exist

in Department.

Department

104

has

no student.

These unmatched rows help explain joins.

* * *

# 1. INNER JOIN

Most common join.

* * *

## Definition

Returns only matching rows from both tables.

If no match exists,

row is discarded.

* * *

## Syntax

```SQL
SELECT columns
FROM Student
INNER JOIN Department
ON Student.DeptID = Department.DeptID;
```

* * *

### Visual

```
Student            Department

    ◯──────────◯

Only overlap
```

Think of two circles.

Only the overlapping region is returned.

* * *

## Execution

Student

| Name | DeptID |
| --- | --- |
| John | 101 |
| Alice | 102 |
| Bob | 101 |
| David | 103 |

Department

| DeptID | Department |
| --- | --- |
| 101 | CSE |
| 102 | ECE |
| 104 | MBA |

* * *

Matching

101

↓

CSE

102

↓

ECE

103

↓

No Match

104

↓

No Student

Output

| Name | Department |
| --- | --- |
| John | CSE |
| Alice | ECE |
| Bob | CSE |

David removed.

MBA removed.

* * *

## Interview Question

What does INNER JOIN return?

Answer

Only matching records.

* * *

# 2. LEFT JOIN

Definition

Return

ALL rows

from left table.

Matching rows

from right table.

If no match,

NULL.

* * *

Syntax

```SQL
SELECT *

FROM Student

LEFT JOIN Department

ON Student.DeptID=Department.DeptID;
```

* * *

Visual

```
Student            Department

██████◯──────────◯

Entire left circle
+
Intersection
```

* * *

Output

| Name | Dept |
| --- | --- |
| John | CSE |
| Alice | ECE |
| Bob | CSE |
| David | NULL |

David remains.

Because LEFT JOIN

keeps

every row

from Student.

* * *

Interview Question

What happens if no match exists?

NULL.

* * *

# 3. RIGHT JOIN

Exactly opposite.

Keep

every row

from right table.

* * *

Syntax

```SQL
SELECT *

FROM Student

RIGHT JOIN Department

ON Student.DeptID=Department.DeptID;
```

* * *

Visual

```
Student            Department

◯──────────◯██████

Entire right circle
```

* * *

Output

| Department | Student |
| --- | --- |
| CSE | John |
| CSE | Bob |
| ECE | Alice |
| MBA | NULL |

MBA retained.

Student absent.

* * *

Interview Question

Difference

LEFT

vs

RIGHT

Just opposite sides.

Many developers prefer LEFT JOIN for readability and rewrite queries instead of using RIGHT JOIN.

* * *

# 4. FULL OUTER JOIN

Return

everything.

Matching

Unmatched

Left

Unmatched

Right.

* * *

Visual

```
██████◯──────────◯██████
```

Entire diagram.

* * *

Output

| Student | Department |
| --- | --- |
| John | CSE |
| Alice | ECE |
| Bob | CSE |
| David | NULL |
| NULL | MBA |

* * *

Syntax (standard SQL)

```SQL
SELECT *

FROM Student

FULL OUTER JOIN Department

ON Student.DeptID=Department.DeptID;
```

* * *

## MySQL Problem

MySQL

does NOT support

FULL JOIN.

* * *

Emulate using

```SQL
SELECT *
FROM Student
LEFT JOIN Department
ON Student.DeptID = Department.DeptID

UNION

SELECT *
FROM Student
RIGHT JOIN Department
ON Student.DeptID = Department.DeptID;
```

* * *

Interview Question

Does MySQL support FULL JOIN?

No.

Need UNION of LEFT and RIGHT JOIN.

* * *

# 5. CROSS JOIN

Most dangerous join.

Produces Cartesian Product.

Every row

joins

with every row.

* * *

Suppose

Student

4 rows

Department

3 rows

Result

```
4 × 3 = 12 rows
```

* * *

Syntax

```SQL
SELECT *

FROM Student

CROSS JOIN Department;
```

* * *

Visual

```
John

↓

CSE

ECE

MBA

Alice

↓

CSE

ECE

MBA

...
```

Every combination.

* * *

Uses

Rare.

Examples

Generate

All

```
Color × Size

Black Small

Black Medium

Black Large

Blue Small

Blue Medium
```

Useful in reporting or combinatorial generation.

* * *

Interview Question

Rows produced?

Answer

```
m × n
```

* * *

# 6. SELF JOIN

A table joins itself.

Used when

one row

references another row

in same table.

* * *

Example

Employee

| ID | Name | ManagerID |
| --- | --- | --- |
| 1 | John | NULL |
| 2 | Alice | 1 |
| 3 | Bob | 1 |
| 4 | David | 2 |

Need

Employee

Manager Name

No manager table.

Same table.

* * *

Syntax

```SQL
SELECT

e.Name,

m.Name AS Manager

FROM Employee e

LEFT JOIN Employee m

ON e.ManagerID=m.ID;
```

Output

| Employee | Manager |
| --- | --- |
| John | NULL |
| Alice | John |
| Bob | John |
| David | Alice |

* * *

Interview Question

Where is SELF JOIN used?

Employee-manager hierarchy

Category-parent category

Folder-parent folder

Comments-replies

Organizational structures

* * *

# Aliases

Almost always used with joins.

Instead of

```SQL
SELECT Student.Name

FROM Student;
```

Use

```SQL
SELECT s.Name

FROM Student s;
```

* * *

Join

```SQL
SELECT

s.Name,

d.Department

FROM Student s

INNER JOIN Department d

ON s.DeptID=d.DeptID;
```

Cleaner.

* * *

Without Alias

```SQL
Student.Name

Department.Department
```

Too lengthy.

* * *

# Multiple Joins

Example

Student

↓

Department

↓

College

```SQL
SELECT

s.Name,

d.Department,

c.CollegeName

FROM Student s

JOIN Department d

ON s.DeptID=d.DeptID

JOIN College c

ON d.CollegeID=c.CollegeID;
```

Very common in interviews.

* * *

# Real Interview Examples

## Question 1

Find every student with department name.

```SQL
SELECT

s.Name,

d.Department

FROM Student s

JOIN Department d

ON s.DeptID=d.DeptID;
```

* * *

## Question 2

Find students without department.

Need LEFT JOIN.

```SQL
SELECT

s.Name

FROM Student s

LEFT JOIN Department d

ON s.DeptID=d.DeptID

WHERE d.DeptID IS NULL;
```

Output

David.

* * *

## Question 3

Find departments with no students.

```SQL
SELECT

d.Department

FROM Department d

LEFT JOIN Student s

ON d.DeptID=s.DeptID

WHERE s.StudentID IS NULL;
```

Output

MBA.

* * *

## Question 4

Find employee and manager.

Need SELF JOIN.

* * *

## Question 5

Generate every product-size combination.

Need CROSS JOIN.

* * *

# Visual Summary

## INNER JOIN

```
      Student
     (   ●   )
      \     /
       \ ● /
        \ /
   Department

Only intersection
```

* * *

## LEFT JOIN

```
████████●●

Entire left

+
intersection
```

* * *

## RIGHT JOIN

```
●●████████

Entire right

+
intersection
```

* * *

## FULL JOIN

```
██████████████

Everything
```

* * *

## CROSS JOIN

```
Every row

×

Every row
```

* * *

## SELF JOIN

```
Employee

↓

Employee
```

* * *

# JOIN Comparison Table

| JOIN | Returns |
| --- | --- |
| INNER JOIN | Only matching rows |
| LEFT JOIN | All left rows + matching right rows |
| RIGHT JOIN | All right rows + matching left rows |
| FULL OUTER JOIN | All rows from both tables |
| CROSS JOIN | Cartesian product (every combination) |
| SELF JOIN | A table joined with itself |

* * *

# Common Interview Mistakes

### Mistake 1

Forgetting ON condition

```SQL
SELECT *

FROM Student

JOIN Department;
```

This becomes invalid (or behaves like a cross join in some DBMS with different syntax).

* * *

### Mistake 2

Using INNER JOIN

when LEFT JOIN is required.

Missing rows disappear.

* * *

### Mistake 3

Using RIGHT JOIN unnecessarily.

Prefer LEFT JOIN.

Most companies do.

* * *

### Mistake 4

Using CROSS JOIN accidentally.

Millions of rows generated.

Can crash queries.

* * *

### Mistake 5

Confusing FULL JOIN with CROSS JOIN.

FULL JOIN

↓

Union of matched and unmatched rows.

CROSS JOIN

↓

Every possible combination.

* * *

# Top Interview Questions

### Basic

1. What is JOIN?
2. Why do we need JOIN?
3. Difference between INNER and LEFT JOIN?
4. Difference between LEFT and RIGHT JOIN?
5. Difference between FULL JOIN and CROSS JOIN?

* * *

### Intermediate

6. Does MySQL support FULL OUTER JOIN?
7. What is a Cartesian Product?
8. Why are aliases used in joins?
9. What is SELF JOIN?
10. Can we join more than two tables?

* * *

### Advanced

11. Find employees without departments.
12. Find departments without employees.
13. Find employee-manager pairs using SELF JOIN.
14. Why is LEFT JOIN generally preferred over RIGHT JOIN?
15. Which join is the fastest?

**Answer:** There isn't a single "fastest" join type. Performance depends on factors like indexes, table sizes, query conditions, and the execution plan chosen by the database optimizer. An `INNER JOIN` often processes fewer rows because unmatched rows are discarded, but the optimizer ultimately determines the most efficient strategy.

* * *

# Complete Revision Sheet

## INNER JOIN

* Returns only matching rows.

## LEFT JOIN

* Returns all rows from the left table and matching rows from the right.
* Unmatched right-side values become `NULL`.

## RIGHT JOIN

* Returns all rows from the right table and matching rows from the left.

## FULL OUTER JOIN

* Returns all matched and unmatched rows from both tables.
* Not supported directly in MySQL.

## CROSS JOIN

* Produces the Cartesian product (`m × n` rows).

## SELF JOIN

* Joins a table with itself.
* Commonly used for hierarchical relationships such as employee-manager.

## Aliases

* Improve readability, especially in joins.
* Essential for self joins because the same table is referenced twice.

* * *

## Memory Trick

```
INNER
→ Only common records

LEFT
→ Keep everything on the left

RIGHT
→ Keep everything on the right

FULL
→ Keep everything

CROSS
→ Everything × Everything

SELF
→ Table joins itself
```

This simple mental model is enough to identify the correct join type in most interview problems.

* * *

**You:**

Module 8 – Set Operations
UNION
UNION ALL
INTERSECT
MINUS/EXCEPT
Difference from JOIN

* * *

**ChatGPT:**

This module is **moderately important** in interviews. It is not asked as frequently as **JOINs** or **GROUP BY**, but almost every SQL interview has at least one question like:

* What is the difference between **UNION and UNION ALL**?
* Difference between **UNION and JOIN**?
* How can you implement **INTERSECT** in MySQL?
* Difference between **EXCEPT and NOT EXISTS**?

These questions are very common.

* * *

# MODULE 8 – SET OPERATIONS

* * *

# What are Set Operations?

Set Operations are used to **combine the results of two or more SELECT queries**.

Unlike JOINs:

* JOIN combines **columns** (Horizontal Combination)
* Set Operations combine **rows** (Vertical Combination)

Think of two Excel sheets.

## JOIN

```
Student Table

ID  Name

↓

Department Table

Dept

↓

Result

ID Name Dept
```

Tables become wider.

* * *

## UNION

```
Table 1

John

Alice

Bob

+

Table 2

David

Emma

↓

Result

John

Alice

Bob

David

Emma
```

Rows become longer.

* * *

# Important Rule

Every SELECT statement must have:

* Same number of columns
* Same order of columns
* Compatible data types

* * *

Correct

```SQL
SELECT Name, Age
FROM Student

UNION

SELECT Name, Age
FROM Employee;
```

* * *

Wrong

```SQL
SELECT Name

UNION

SELECT Name, Age;
```

Different number of columns.

* * *

Wrong

```SQL
SELECT Name

UNION

SELECT Salary;
```

Different data types may cause an error depending on the DBMS.

* * *

# Types of Set Operations

```
1 UNION

2 UNION ALL

3 INTERSECT

4 EXCEPT (MINUS in Oracle)
```

* * *

# Sample Tables

## Student_A

| Name |
| --- |
| John |
| Alice |
| Bob |

* * *

## Student_B

| Name |
| --- |
| Bob |
| David |
| Emma |

* * *

# 1. UNION

Most commonly used.

* * *

## Definition

Combines rows from two queries and **removes duplicates**.

* * *

Syntax

```SQL
SELECT column
FROM table1

UNION

SELECT column
FROM table2;
```

* * *

Example

```SQL
SELECT Name
FROM Student_A

UNION

SELECT Name
FROM Student_B;
```

Output

| Name |
| --- |
| John |
| Alice |
| Bob |
| David |
| Emma |

Notice

Bob appeared once.

Duplicate removed.

* * *

How UNION works internally

```
Query1

↓

Query2

↓

Combine

↓

Remove duplicates

↓

Output
```

Removing duplicates requires additional work (sorting or hashing), which can affect performance.

* * *

# UNION ALL

Very common interview question.

* * *

Definition

Combines rows

**Keeps duplicates.**

* * *

Syntax

```SQL
SELECT column
FROM table1

UNION ALL

SELECT column
FROM table2;
```

* * *

Example

```SQL
SELECT Name
FROM Student_A

UNION ALL

SELECT Name
FROM Student_B;
```

Output

| Name |
| --- |
| John |
| Alice |
| Bob |
| Bob |
| David |
| Emma |

Bob appears twice.

* * *

# Difference

UNION

↓

Distinct

UNION ALL

↓

Duplicates allowed

* * *

Interview Question

Which is faster?

UNION ALL

Why?

Because it does not remove duplicates.

* * *

Memory Trick

```
UNION

↓

Unique

UNION ALL

↓

All rows
```

* * *

# INTERSECT

Definition

Returns only common rows.

* * *

Example

Student_A

```
John

Alice

Bob
```

Student_B

```
Bob

David

Emma
```

Output

```
Bob
```

Only common value.

* * *

Syntax (DBMS that support it)

```SQL
SELECT Name
FROM Student_A

INTERSECT

SELECT Name
FROM Student_B;
```

* * *

## MySQL Problem

MySQL (before version 8.0.31) did not support `INTERSECT` directly.

It can be emulated.

```SQL
SELECT DISTINCT a.Name
FROM Student_A a
INNER JOIN Student_B b
ON a.Name = b.Name;
```

Output

```
Bob
```

* * *

# EXCEPT (MINUS)

Different databases use different names.

| DBMS | Keyword |
| --- | --- |
| SQL Server | EXCEPT |
| PostgreSQL | EXCEPT |
| Oracle | MINUS |
| MySQL | No direct support (can emulate) |

* * *

Definition

Return rows

present in first query

but NOT in second.

* * *

Student_A

```
John

Alice

Bob
```

Student_B

```
Bob

David
```

Output

```
John

Alice
```

* * *

Syntax

```SQL
SELECT Name
FROM Student_A

EXCEPT

SELECT Name
FROM Student_B;
```

* * *

MySQL Equivalent

```SQL
SELECT a.Name
FROM Student_A a

LEFT JOIN Student_B b
ON a.Name=b.Name

WHERE b.Name IS NULL;
```

or

```SQL
SELECT Name
FROM Student_A
WHERE Name NOT IN (
    SELECT Name
    FROM Student_B
);
```

* * *

# Visual Understanding

Imagine

```
A

John

Alice

Bob
```

```
B

Bob

David
```

* * *

UNION

```
John

Alice

Bob

David
```

* * *

UNION ALL

```
John

Alice

Bob

Bob

David
```

* * *

INTERSECT

```
Bob
```

* * *

EXCEPT

```
John

Alice
```

* * *

# UNION vs UNION ALL

| UNION | UNION ALL |
| --- | --- |
| Removes duplicates | Keeps duplicates |
| Slower | Faster |
| Uses DISTINCT internally | No duplicate removal |
| Most commonly used when unique results are required | Used when duplicates are meaningful or acceptable |

* * *

# Difference Between JOIN and UNION

One of the most asked interview questions.

* * *

Suppose

Student

| ID | Name |
| --- | --- |
| 1 | John |
| 2 | Alice |

Department

| ID | Dept |
| --- | --- |
| 1 | CSE |
| 2 | ECE |

* * *

JOIN

```SQL
SELECT Name,Dept

FROM Student

JOIN Department

ON Student.ID=Department.ID;
```

Output

| Name | Dept |
| --- | --- |
| John | CSE |
| Alice | ECE |

Columns increased.

* * *

UNION

Table1

```
John

Alice
```

Table2

```
Bob

David
```

Output

```
John

Alice

Bob

David
```

Rows increased.

* * *

Memory Trick

JOIN

↓

Horizontal

UNION

↓

Vertical

* * *

# JOIN vs UNION Table

| JOIN | UNION |
| --- | --- |
| Combines columns | Combines rows |
| Needs matching condition (`ON`) | No join condition |
| Can use different numbers of columns? No | Must have same number of selected columns |
| Works on related tables | Works on query results with compatible structure |
| Returns wider tables | Returns taller tables |

* * *

# Real Interview Examples

* * *

## Question 1

Show every employee from two branches.

Branch1

```
John

Alice
```

Branch2

```
Bob

Emma
```

```SQL
SELECT Name
FROM Branch1

UNION

SELECT Name
FROM Branch2;
```

* * *

## Question 2

Keep duplicates

```SQL
SELECT Name

FROM Branch1

UNION ALL

SELECT Name

FROM Branch2;
```

* * *

## Question 3

Find students studying in both courses.

```SQL
SELECT StudentID

FROM CourseA

INTERSECT

SELECT StudentID

FROM CourseB;
```

* * *

## Question 4

Students enrolled in CourseA but not CourseB.

```SQL
SELECT StudentID

FROM CourseA

EXCEPT

SELECT StudentID

FROM CourseB;
```

* * *

## Question 5

MySQL implementation

```SQL
SELECT a.StudentID

FROM CourseA a

LEFT JOIN CourseB b

ON a.StudentID=b.StudentID

WHERE b.StudentID IS NULL;
```

* * *

# Common Interview Mistakes

* * *

## Mistake 1

Using different numbers of columns.

Wrong

```SQL
SELECT Name

UNION

SELECT Name,Age;
```

* * *

## Mistake 2

Confusing UNION with JOIN.

Remember

UNION

↓

Rows

JOIN

↓

Columns

* * *

## Mistake 3

Thinking UNION keeps duplicates.

Wrong.

UNION

removes duplicates.

* * *

## Mistake 4

Thinking MySQL supports every set operation.

Historically, MySQL supported `UNION`/`UNION ALL`, but `INTERSECT` and `EXCEPT` were added only in newer versions. In many interviews, it's still useful to know how to emulate them using joins or subqueries.

* * *

## Mistake 5

Ignoring performance.

Need duplicates?

Use

```SQL
UNION ALL
```

instead of

```SQL
UNION
```

* * *

# Advanced Interview Discussion

## Q1. Why is UNION slower than UNION ALL?

Because UNION has to identify and remove duplicate rows, which usually involves sorting or hashing.

* * *

## Q2. Can UNION combine different data types?

Only if the DBMS can convert them to compatible types. Otherwise, it throws an error.

* * *

## Q3. Can ORDER BY be used?

Yes.

But only once,

at the end.

Correct

```SQL
SELECT Name
FROM A

UNION

SELECT Name
FROM B

ORDER BY Name;
```

Wrong

```SQL
SELECT Name
FROM A
ORDER BY Name

UNION

SELECT Name
FROM B;
```

* * *

## Q4. Can LIMIT be used?

Yes.

Usually after the complete UNION result.

```SQL
SELECT Name
FROM A

UNION

SELECT Name
FROM B

LIMIT 5;
```

* * *

## Q5. Can GROUP BY be used?

Yes.

Inside each SELECT query or after combining (often by wrapping the UNION in a subquery).

Example

```SQL
SELECT Department, COUNT(*)
FROM (
    SELECT Department FROM Table1
    UNION ALL
    SELECT Department FROM Table2
) AS Combined
GROUP BY Department;
```

* * *

# Complete Revision Sheet

## UNION

* Combines multiple SELECT results.
* Removes duplicate rows.
* Requires the same number of columns and compatible data types.

* * *

## UNION ALL

* Combines multiple SELECT results.
* Keeps duplicates.
* Faster than UNION.

* * *

## INTERSECT

* Returns only common rows.
* Not available in older MySQL versions; can be emulated using INNER JOIN or EXISTS.

* * *

## EXCEPT / MINUS

* Returns rows in the first query but not in the second.
* `EXCEPT` is used in SQL Server/PostgreSQL.
* `MINUS` is used in Oracle.
* Older MySQL versions emulate it using LEFT JOIN, `NOT EXISTS`, or `NOT IN`.

* * *

## JOIN vs UNION

| JOIN | UNION |
| --- | --- |
| Combines columns | Combines rows |
| Horizontal combination | Vertical combination |
| Requires a join condition | No join condition |
| Used on related tables | Used to combine compatible query results |

* * *

# Top Interview Questions

1. Difference between `UNION` and `UNION ALL`.
2. Why is `UNION ALL` faster?
3. Difference between `JOIN` and `UNION`.
4. Can `UNION` combine different numbers of columns?
5. Can `ORDER BY` be used with `UNION`?
6. What does `INTERSECT` do?
7. What is `EXCEPT` (or `MINUS`)?
8. How would you implement `INTERSECT` in older MySQL versions?
9. How would you implement `EXCEPT` in older MySQL versions?
10. When would you choose `UNION ALL` over `UNION`?

* * *

## Memory Trick

```
UNION
→ Combine rows
→ Remove duplicates

UNION ALL
→ Combine rows
→ Keep duplicates

INTERSECT
→ Common rows only

EXCEPT / MINUS
→ First query − Second query

JOIN
→ Combine columns (Horizontal)

SET OPERATIONS
→ Combine rows (Vertical)
```

This mental model is enough to distinguish set operations from joins in almost every SQL interview.

* * *

**You:**

Module 9 – Subqueries
Scalar
Multiple-row
Multiple-column
Nested
Correlated Subqueries
EXISTS
NOT EXISTS
IN vs EXISTS
ANY
ALL

* * *

**ChatGPT:**

This is one of the **most important SQL modules** for interviews.

Almost every company asks questions involving subqueries because they test whether you understand **how SQL thinks**, not just syntax.

Companies like Amazon, Microsoft, Oracle, Google, Walmart, Adobe, Flipkart, Atlassian, etc., ask questions like:

* Find the second highest salary.
* Find employees earning more than the average salary.
* Difference between `IN` and `EXISTS`.
* What is a correlated subquery?
* Difference between `ANY` and `ALL`.

* * *

# MODULE 9 – SUBQUERIES

* * *

# What is a Subquery?

## Definition

A **subquery** is a query written inside another SQL query.

It is also called an **Inner Query** or **Nested Query**.

The outer query uses the result produced by the inner query.

* * *

Example

Suppose Employee table

| EmpID | Name | Salary |
| --- | --- | --- |
| 1 | John | 50000 |
| 2 | Alice | 70000 |
| 3 | Bob | 60000 |

Manager asks

> Find employees earning more than the average salary.

Can we directly write

```SQL
SELECT *
FROM Employee
WHERE Salary > AVG(Salary);
```

❌ Wrong.

`AVG()` is calculated after filtering.

Instead

```SQL
SELECT *
FROM Employee
WHERE Salary >
(
    SELECT AVG(Salary)
    FROM Employee
);
```

Execution

```
Inner Query

↓

AVG = 60000

↓

Outer Query

↓

Salary > 60000

↓

Alice
```

* * *

# General Syntax

```SQL
SELECT columns

FROM table

WHERE column operator

(
    SELECT ...
);
```

* * *

# Types of Subqueries

There are mainly five important types.

```
1 Scalar Subquery

2 Multiple-row Subquery

3 Multiple-column Subquery

4 Nested Subquery

5 Correlated Subquery
```

* * *

# 1. Scalar Subquery

Most common.

* * *

## Definition

Returns exactly **one value**.

One row

One column.

* * *

Example

Average salary.

```SQL
SELECT AVG(Salary)

FROM Employee;
```

Output

```
60000
```

Now

```SQL
SELECT *

FROM Employee

WHERE Salary>

(
SELECT AVG(Salary)

FROM Employee
);
```

Output

| Name |
| --- |
| Alice |

* * *

Interview Question

Why is it called scalar?

Because it returns a single value.

* * *

Another Example

Highest Salary

```SQL
SELECT *

FROM Employee

WHERE Salary=

(
SELECT MAX(Salary)

FROM Employee
);
```

* * *

# 2. Multiple-row Subquery

Returns multiple rows.

* * *

Example

Customer table

| CustomerID | City |
| --- | --- |
| 1 | Delhi |
| 2 | Mumbai |
| 3 | Delhi |

Need

Orders

belonging to customers

living in Delhi.

* * *

Customer

```SQL
SELECT CustomerID

FROM Customer

WHERE City='Delhi';
```

Output

```
1

3
```

Multiple values.

Outer Query

```SQL
SELECT *

FROM Orders

WHERE CustomerID IN

(
SELECT CustomerID

FROM Customer

WHERE City='Delhi'
);
```

Output

Orders

of customers

1

and

* * *

Important

Need

```SQL
IN
```

not

```SQL
=
```

because multiple values.

* * *

Interview Mistake

Wrong

```SQL
WHERE CustomerID=

(
SELECT CustomerID...
)
```

Error

More than one row returned.

* * *

# 3. Multiple-column Subquery

Returns multiple columns.

Less common but asked.

* * *

Example

Employee

| Name | Dept | Salary |
| --- | --- | --- |
| John | IT | 50000 |
| Alice | HR | 60000 |

Need

Employee

having

same

Dept

and

Salary

as another table.

```SQL
SELECT *

FROM Employee

WHERE

(Department,Salary)

IN

(
SELECT Department,Salary

FROM NewEmployee
);
```

Both columns are compared together.

* * *

# 4. Nested Subquery

A subquery inside another subquery.

* * *

Example

```
Outer Query

↓

Inner Query

↓

Another Inner Query
```

* * *

Example

```SQL
SELECT *

FROM Employee

WHERE DepartmentID=

(
SELECT DepartmentID

FROM Department

WHERE ManagerID=

(
SELECT EmployeeID

FROM Employee

WHERE Name='John'
)
);
```

Three levels.

* * *

Execution

Find John's EmployeeID

↓

Find John's department

↓

Find employees

in that department

* * *

# 5. Correlated Subquery

Most important interview topic.

* * *

Normal subquery

Runs once.

Correlated subquery

Runs once

for every row

of outer query.

* * *

Suppose

Employee

| Name | Dept | Salary |
| --- | --- | --- |
| John | IT | 50000 |
| Bob | IT | 70000 |
| Alice | HR | 60000 |
| David | HR | 40000 |

Need

Highest salary

within each department.

* * *

Query

```SQL
SELECT *

FROM Employee e1

WHERE Salary=

(
SELECT MAX(Salary)

FROM Employee e2

WHERE e1.Department=e2.Department
);
```

* * *

Execution

John

↓

Compare IT

↓

70000

↓

John rejected.

* * *

Bob

↓

Compare IT

↓

70000

↓

Bob selected.

* * *

Alice

↓

Compare HR

↓

60000

↓

Selected.

* * *

David

↓

Compare HR

↓

60000

↓

Rejected.

* * *

Output

| Name |
| --- |
| Bob |
| Alice |

* * *

Why correlated?

Because inner query depends on outer query.

```SQL
WHERE e1.Department=e2.Department
```

Without outer query,

inner query cannot execute.

* * *

Interview Question

Difference

Normal

vs

Correlated

| Normal | Correlated |
| --- | --- |
| Runs once | Runs for every outer row |
| Independent | Depends on outer query |
| Usually faster | Can be slower |

* * *

# EXISTS

Extremely important.

* * *

Definition

Checks

whether subquery returns

at least one row.

Returns

TRUE

or

FALSE.

* * *

Syntax

```SQL
SELECT *

FROM Customer c

WHERE EXISTS

(
SELECT *

FROM Orders o

WHERE o.CustomerID=c.CustomerID
);
```

Meaning

Return

customer

if

at least one order exists.

* * *

Execution

Customer

John

↓

Any order?

↓

Yes

↓

Return John

* * *

Customer

Alice

↓

No orders

↓

Ignore

* * *

Interview Point

EXISTS

stops searching

after finding first match.

Very efficient.

* * *

# NOT EXISTS

Opposite.

Return

rows

for which

subquery returns nothing.

* * *

Example

Customers

who never ordered.

```SQL
SELECT *

FROM Customer c

WHERE NOT EXISTS

(
SELECT *

FROM Orders o

WHERE o.CustomerID=c.CustomerID
);
```

* * *

Output

Customers

without orders.

* * *

# IN vs EXISTS

Most asked interview question.

* * *

Example

```SQL
WHERE CustomerID IN

(
SELECT CustomerID

FROM Orders
)
```

* * *

EXISTS

```SQL
WHERE EXISTS

(
SELECT *

FROM Orders

WHERE Orders.CustomerID=Customer.CustomerID
)
```

* * *

Difference

| IN | EXISTS |
| --- | --- |
| Compares values | Checks existence |
| Works well for small result sets | Often better for large datasets, especially correlated checks |
| Evaluates the returned values | Stops after first matching row |

* * *

Interview Answer

When data is huge

↓

Prefer

EXISTS

because it can stop early once a match is found, depending on the optimizer and indexes.

* * *

# ANY

Less common but important.

* * *

Definition

Compare

with

any value

returned.

* * *

Suppose

Salaries

```
30000

40000

50000
```

Query

```SQL
SELECT *

FROM Employee

WHERE Salary>

ANY

(
SELECT Salary

FROM Employee

WHERE Department='HR'
);
```

Meaning

Salary

greater than

at least one

HR salary.

* * *

Suppose

HR

```
30000

40000
```

Condition

```
Salary > 30000
```

Enough.

* * *

# ALL

Opposite.

Must satisfy

every value.

* * *

Example

```SQL
SELECT *

FROM Employee

WHERE Salary>

ALL

(
SELECT Salary

FROM HR
);
```

Suppose

HR

```
30000

40000
```

Need

Salary

30000

AND

40000

Effectively

Salary

40000

* * *

Difference

| ANY | ALL |
| --- | --- |
| One value enough | Every value required |
| Similar to OR logic | Similar to AND logic |

* * *

# Real Interview Examples

* * *

## Find second highest salary

Classic interview question.

```SQL
SELECT MAX(Salary)

FROM Employee

WHERE Salary<

(
SELECT MAX(Salary)

FROM Employee
);
```

* * *

## Employees earning above average salary

```SQL
SELECT *

FROM Employee

WHERE Salary>

(
SELECT AVG(Salary)

FROM Employee
);
```

* * *

## Customers with no orders

```SQL
SELECT *

FROM Customer c

WHERE NOT EXISTS

(
SELECT *

FROM Orders o

WHERE o.CustomerID=c.CustomerID
);
```

* * *

## Employees working in departments located in Delhi

```SQL
SELECT *

FROM Employee

WHERE DepartmentID IN

(
SELECT DepartmentID

FROM Department

WHERE City='Delhi'
);
```

* * *

## Highest salary in each department

```SQL
SELECT *

FROM Employee e1

WHERE Salary=

(
SELECT MAX(Salary)

FROM Employee e2

WHERE e1.Department=e2.Department
);
```

* * *

# Common Interview Mistakes

### Mistake 1

Using `=` with multiple rows.

Wrong

```SQL
WHERE ID=

(
SELECT ID

FROM Student
);
```

If multiple rows are returned, use `IN`.

* * *

### Mistake 2

Thinking `EXISTS` returns values.

Wrong.

Returns only TRUE or FALSE.

* * *

### Mistake 3

Confusing `IN` with `EXISTS`.

`IN`

↓

Value comparison

`EXISTS`

↓

Existence check

* * *

### Mistake 4

Thinking correlated subquery runs once.

Wrong.

Runs for every row of outer query.

* * *

### Mistake 5

Using `ALL`

instead of

`ANY`.

Remember

```
ANY

↓

One match enough

ALL

↓

Every value
```

* * *

# Performance Discussion

Interviewers often ask:

**Which is faster: JOIN or Subquery?**

Answer:

There is **no universal answer**.

* Modern query optimizers often transform subqueries into joins internally.
* A well-written JOIN may be faster in many cases.
* `EXISTS` is often efficient for existence checks.
* Performance depends on indexes, table sizes, and the execution plan.

* * *

# Complete Revision Sheet

## Scalar Subquery

* Returns one row and one column.
* Used with `=`, `>`, `<`, etc.

* * *

## Multiple-row Subquery

* Returns multiple rows.
* Typically used with `IN`, `ANY`, or `ALL`.

* * *

## Multiple-column Subquery

* Returns multiple columns.
* Compared using tuple syntax like `(col1, col2)`.

* * *

## Nested Subquery

* A subquery inside another subquery.

* * *

## Correlated Subquery

* Depends on the outer query.
* Executes once for each row of the outer query.

* * *

## EXISTS

* Returns TRUE if the subquery returns at least one row.
* Often efficient for existence checks.

* * *

## NOT EXISTS

* Returns TRUE if the subquery returns no rows.

* * *

## IN vs EXISTS

| IN | EXISTS |
| --- | --- |
| Compares values | Checks whether matching rows exist |
| Good for smaller result sets | Often efficient for large, indexed tables |
| Uses returned values | Stops after first match |

* * *

## ANY

* Condition must be true for at least one value returned.

Example:

```SQL
Salary > ANY (...)
```

* * *

## ALL

* Condition must be true for every value returned.

Example:

```SQL
Salary > ALL (...)
```

* * *

# Top 20 Interview Questions

1. What is a subquery?
2. What is a scalar subquery?
3. Difference between scalar and multiple-row subqueries?
4. What is a correlated subquery?
5. Why is a correlated subquery slower?
6. Difference between `IN` and `EXISTS`?
7. Difference between `EXISTS` and `NOT EXISTS`?
8. What is `ANY`?
9. What is `ALL`?
10. Difference between `ANY` and `ALL`?
11. How do you find the second highest salary?
12. How do you find employees earning above the average salary?
13. How do you find customers without orders?
14. Can a subquery return multiple columns?
15. Can a subquery appear in the `SELECT` clause? (Yes, if it returns a scalar value.)
16. Can a subquery appear in the `FROM` clause? (Yes, as a derived table.)
17. Can a subquery appear in the `WHERE` clause? (Yes.)
18. Which is generally better for existence checks: `IN` or `EXISTS`?
19. Can modern SQL optimizers rewrite subqueries as joins? (Often, yes.)
20. When would you choose a correlated subquery over a JOIN?

* * *

# Memory Trick

```
Scalar
→ One value

Multiple-row
→ Many values

Nested
→ Query inside query

Correlated
→ Depends on outer row

EXISTS
→ Is there at least one match?

NOT EXISTS
→ No matching rows exist

IN
→ Compare values

ANY
→ One match is enough

ALL
→ Must satisfy every value
```

Understanding these concepts is enough to solve a large portion of SQL interview problems, especially when combined with `JOIN`, `GROUP BY`, and aggregate functions.

* * *

**You:**

Module 10 – Views
CREATE VIEW
ALTER VIEW
DROP VIEW
Updatable Views
Advantages
Limitations

* * *

**ChatGPT:**

This is a **medium-priority interview topic**.

It is not asked as frequently as **JOINs, GROUP BY, or Subqueries**, but almost every interviewer expects you to know:

* What is a View?
* Why do we use Views?
* Difference between View and Table?
* Can we update a View?
* What are Materialized Views?

These are very common discussion questions.

* * *

# MODULE 10 – VIEWS

* * *

# What is a View?

## Definition

A **View** is a **virtual table** created from one or more existing tables using a SQL query.

It **does not store the actual data** (in a standard view).

Instead,

it stores

```
The SQL Query
```

Whenever you access the view,

SQL executes that query

and returns fresh data.

* * *

## Example

Employee Table

| ID | Name | Department | Salary |
| --- | --- | --- | --- |
| 1 | John | IT | 60000 |
| 2 | Alice | HR | 50000 |
| 3 | Bob | IT | 70000 |

Suppose HR employees should **not** see salaries.

Instead of giving them access to Employee table,

create a View.

```SQL
CREATE VIEW Employee_Public AS
SELECT ID, Name, Department
FROM Employee;
```

Now

```SQL
SELECT *
FROM Employee_Public;
```

Output

| ID | Name | Department |
| --- | --- | --- |
| 1 | John | IT |
| 2 | Alice | HR |
| 3 | Bob | IT |

Salary is hidden.

* * *

# Why do we need Views?

Think about a banking system.

Customer table

| ID | Name | Balance | Password | PIN |
| --- | --- | --- | --- | --- |

Should every employee see

```
PIN

Password
```

No.

Create a View.

```SQL
CREATE VIEW CustomerInfo AS
SELECT ID, Name, Balance
FROM Customer;
```

Employees access only the View.

Sensitive data stays protected.

* * *

# Syntax

## CREATE VIEW

```SQL
CREATE VIEW view_name AS
SELECT column1, column2
FROM table
WHERE condition;
```

* * *

Example

```SQL
CREATE VIEW IT_Employees AS
SELECT Name, Salary
FROM Employee
WHERE Department = 'IT';
```

Now

```SQL
SELECT *
FROM IT_Employees;
```

Output

| Name | Salary |
| --- | --- |
| John | 60000 |
| Bob | 70000 |

* * *

# Can a View use JOINs?

Yes.

Very common.

Suppose

Employee

| EmpID | Name | DeptID |
| --- | --- | --- |
| 1 | John | 101 |
| 2 | Alice | 102 |

Department

| DeptID | Department |
| --- | --- |
| 101 | IT |
| 102 | HR |

Create View

```SQL
CREATE VIEW EmployeeDetails AS
SELECT e.Name,
       d.Department
FROM Employee e
JOIN Department d
ON e.DeptID = d.DeptID;
```

Now

```SQL
SELECT *
FROM EmployeeDetails;
```

Output

| Name | Department |
| --- | --- |
| John | IT |
| Alice | HR |

* * *

# ALTER VIEW

Modify an existing View.

Syntax

```SQL
ALTER VIEW view_name AS
SELECT ...
```

Example

Earlier

```SQL
CREATE VIEW Employee_Public AS
SELECT Name
FROM Employee;
```

Need Department too.

```SQL
ALTER VIEW Employee_Public AS
SELECT Name,
       Department
FROM Employee;
```

View updated.

* * *

# DROP VIEW

Delete the View.

Only the View disappears.

Original table remains.

Syntax

```SQL
DROP VIEW view_name;
```

Example

```SQL
DROP VIEW Employee_Public;
```

Employee table still exists.

* * *

# How Views Work Internally

Suppose

```SQL
CREATE VIEW ITEmployees AS
SELECT *
FROM Employee
WHERE Department='IT';
```

When you execute

```SQL
SELECT *
FROM ITEmployees;
```

SQL internally executes

```SQL
SELECT *
FROM Employee
WHERE Department='IT';
```

The View stores the query definition, not a separate copy of the data.

* * *

# View vs Table

Very common interview question.

| Table | View |
| --- | --- |
| Stores actual data | Stores only query definition (standard view) |
| Occupies storage for rows | Very little storage (mainly metadata) |
| Can exist independently | Depends on underlying table(s) |
| Data inserted directly | Usually retrieves data from base tables |
| Can have indexes | Standard views cannot have their own indexes (materialized/indexed views are DBMS-specific) |

* * *

# Updatable Views

Most asked interview question.

Can we update a View?

Answer

**Yes, but only under certain conditions.**

* * *

## Example

Employee

| ID | Name | Salary |
| --- | --- | --- |
| 1 | John | 60000 |

View

```SQL
CREATE VIEW EmployeeView AS
SELECT ID,
       Name,
       Salary
FROM Employee;
```

Now

```SQL
UPDATE EmployeeView
SET Salary = 70000
WHERE ID = 1;
```

Employee table becomes

| ID | Name | Salary |
| --- | --- | --- |
| 1 | John | 70000 |

The underlying table is updated.

* * *

# When is a View Updatable?

Generally, a view is updatable if it is based on a **single table** and avoids constructs that make updates ambiguous.

Typically, avoid:

* Aggregate functions (`SUM`, `AVG`, `COUNT`, ...)
* `GROUP BY`
* `DISTINCT`
* `UNION`
* Many complex joins
* Calculated columns that cannot be mapped back to a base column

Example

```SQL
CREATE VIEW AvgSalary AS
SELECT Department,
       AVG(Salary)
FROM Employee
GROUP BY Department;
```

Cannot update.

There is no single employee row

to update.

* * *

# Advantages of Views

* * *

## 1. Security

Hide confidential columns.

Instead of

```
Name

Salary

Password

PIN
```

Show only

```
Name

Salary
```

* * *

## 2. Simplicity

Complex query

```SQL
SELECT ...
FROM A
JOIN B
JOIN C
JOIN D
WHERE ...
GROUP BY ...
```

Create View

```SQL
CREATE VIEW Report AS
...
```

Now

```SQL
SELECT *
FROM Report;
```

Much simpler.

* * *

## 3. Code Reusability

Instead of writing

100-line SQL

every time,

create one View.

Everyone uses it.

* * *

## 4. Logical Data Independence

Suppose

Employee table changes internally.

You can sometimes modify the View definition so applications continue using the same View interface.

* * *

## 5. Consistency

Everyone uses

same business logic.

No repeated SQL.

Less chance of mistakes.

* * *

# Limitations of Views

* * *

## 1. Performance

Every time

View executes,

underlying query runs.

Complex Views

can be slower.

* * *

## 2. Cannot Always Update

Complex Views

are usually

read-only.

* * *

## 3. Dependency

Delete underlying table

↓

View becomes invalid.

* * *

## 4. Large Nested Views

View

↓

View

↓

View

↓

View

Can become difficult to maintain and debug.

* * *

# Materialized View

Very common interview discussion.

Standard View

```
Stores SQL Query
```

Materialized View

```
Stores Result Data
```

Difference

Normal View

```
Every SELECT

↓

Run query
```

Materialized View

```
Query runs once

↓

Result stored

↓

Future SELECT reads stored data
```

Much faster

for reporting,

analytics,

dashboards.

* * *

Example

Sales table

10 crore rows.

Average sales report

Very slow.

Create Materialized View.

Now report

loads instantly.

* * *

Interview Question

Difference

View

vs

Materialized View

| View | Materialized View |
| --- | --- |
| Stores query | Stores query result |
| Always latest data | May need refresh depending on DBMS |
| Less storage | Uses storage for cached results |
| Can be slower for complex queries | Faster for repeated reads |

> **Note:** MySQL does **not** have native materialized views. They are available in databases like Oracle and PostgreSQL (through different mechanisms).

* * *

# Real Interview Examples

## Example 1

Create View

showing

only IT employees.

```SQL
CREATE VIEW ITEmployees AS
SELECT *
FROM Employee
WHERE Department='IT';
```

* * *

## Example 2

Hide salary.

```SQL
CREATE VIEW EmployeePublic AS
SELECT ID,
       Name
FROM Employee;
```

* * *

## Example 3

View using JOIN.

```SQL
CREATE VIEW EmployeeDept AS
SELECT e.Name,
       d.Department
FROM Employee e
JOIN Department d
ON e.DeptID=d.DeptID;
```

* * *

## Example 4

Delete View.

```SQL
DROP VIEW EmployeeDept;
```

* * *

## Example 5

Modify View.

```SQL
ALTER VIEW EmployeeDept AS
SELECT Name,
       Salary
FROM Employee;
```

* * *

# Common Interview Mistakes

### Mistake 1

Thinking a View stores data.

Wrong.

Standard Views

store

the query definition.

* * *

### Mistake 2

Thinking every View can be updated.

Wrong.

Only certain Views

are updatable.

* * *

### Mistake 3

Deleting View

deletes table.

Wrong.

Only View disappears.

* * *

### Mistake 4

Thinking Views improve performance.

Not necessarily.

Standard Views simply encapsulate queries.

* * *

### Mistake 5

Confusing View

with

Materialized View.

One stores

query.

Other stores

query result.

* * *

# Performance Discussion

**Q. Are Views faster than Tables?**

Not necessarily.

A View is simply a saved SQL query.

The database optimizer expands it into the underlying query.

* * *

**Q. Then why use Views?**

Main reasons:

* Security
* Simplicity
* Reusability
* Consistent business logic

Not primarily for speed.

* * *

# Complete Revision Sheet

## CREATE VIEW

```SQL
CREATE VIEW view_name AS
SELECT ...
```

Creates a virtual table.

* * *

## ALTER VIEW

```SQL
ALTER VIEW view_name AS
SELECT ...
```

Changes the view definition.

* * *

## DROP VIEW

```SQL
DROP VIEW view_name;
```

Removes only the View.

* * *

## Updatable View

Usually possible when:

* Based on one table
* No aggregates
* No `GROUP BY`
* No `DISTINCT`
* No `UNION`
* No ambiguous mappings

* * *

## Advantages

* Security
* Simpler queries
* Reusable SQL
* Consistent business logic
* Logical abstraction

* * *

## Limitations

* Standard views don't inherently improve performance
* Complex views may be read-only
* Depend on underlying tables
* Can become difficult to maintain if overused

* * *

## View vs Table

| Table | View |
| --- | --- |
| Stores data | Stores query definition |
| Independent | Depends on base tables |
| Can be indexed | Standard views cannot have independent indexes |
| Direct data storage | Virtual representation |

* * *

## View vs Materialized View

| View | Materialized View |
| --- | --- |
| Stores query | Stores query result |
| Always reflects current data | May require refresh |
| Minimal storage | Uses storage |
| Query executed on each access | Reads precomputed data |

* * *

# Top Interview Questions

1. What is a View?
2. Why do we use Views?
3. Difference between a View and a Table?
4. Can Views be updated?
5. What is an updatable View?
6. Can a View contain a JOIN?
7. Can a View contain `GROUP BY`?
8. Does a View store data?
9. Difference between a View and a Materialized View?
10. Why are Views useful for security?
11. What happens if the base table is dropped?
12. Can you create a View from another View? (Yes.)
13. Can a View have indexes? (Standard views cannot; indexed/materialized views depend on the DBMS.)
14. Are Views faster than tables?
15. When would you choose a View over writing the SQL query repeatedly?

* * *

# Memory Trick

```
VIEW
→ Virtual Table
→ Stores SQL Query
→ Security
→ Simplicity
→ Reusability

UPDATABLE VIEW
→ Usually one table
→ No GROUP BY
→ No DISTINCT
→ No Aggregate
→ No UNION

MATERIALIZED VIEW
→ Stores Result
→ Faster Reads
→ Uses Storage
→ May Need Refresh
```

If you can confidently answer **"What is a View?", "Can it be updated?", "View vs Table", and "View vs Materialized View"**, you'll be well prepared for almost every SQL interview question on this topic.
