---
title: "DBMS Interview Preparation"
source: "https://chatgpt.com/c/6a44c279-dc90-83ee-8eb2-00e54a4f3f72?mweb_fallback=1"
---

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