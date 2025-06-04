# Functional Dependency in Database Systems

## 📖 What is Functional Dependency?

**Functional Dependency** means that **the value of one column (or a set of columns) uniquely determines the value of another column** in a table.

In other words: If you know the value of column A, you can find exactly one value of column B.

## 🔍 Simple Explanation

- If **A → B** (read as "A determines B"), then for each value of A, there is only one corresponding value of B.
- So, no two rows with the same A value can have different B values.

## 📊 Basic Example

Consider a table of students:

| StudentID | StudentName | Department |
|-----------|-------------|------------|
| 101       | Alice       | CS         |
| 102       | Bob         | EE         |
| 103       | Carol       | ME         |

### Functional Dependencies in this table:
- `StudentID` **functionally determines** `StudentName` and `Department`
- Knowing `StudentID` tells you exactly which `StudentName` and `Department` correspond to it
- **StudentID → StudentName** and **StudentID → Department**

## 🎯 Why is Functional Dependency Important?

- **Primary Key Definition**: Helps define primary keys (unique identifiers)
- **Database Normalization**: Used to decide how to normalize tables by understanding which columns depend on others
- **Data Integrity**: Ensures consistency and prevents data anomalies

## ❌ Violation of Functional Dependency

### Example of Violation:

If we mistakenly add this row to our student table:

| StudentID | StudentName | Department |
|-----------|-------------|------------|
| 101       | Alicia      | CS         |

The complete table becomes:

| StudentID | StudentName | Department |
|-----------|-------------|------------|
| 101       | Alice       | CS         |
| 102       | Bob         | EE         |
| 103       | Carol       | ME         |
| 101       | Alicia      | CS         |

### 🚨 Problem Identified:
- **StudentID → StudentName** is **violated** because:
- StudentID `101` is mapping to **two different names**: `Alice` and `Alicia`

### 🛑 Why This is Bad:
- If `StudentID` is meant to uniquely identify students, this inconsistency can lead to:
  - Confusion in data interpretation
  - Application errors
  - Data integrity problems
  - Unreliable query results

## 🧩 Composite Key Functional Dependency

Sometimes a single column isn't enough to uniquely determine other values. In such cases, we use **composite keys** (combination of multiple columns).

### 🎓 Student-Course Enrollment Example

| StudentID | CourseCode | Grade |
|-----------|------------|-------|
| 101       | CS101      | A     |
| 101       | MA102      | B     |
| 102       | CS101      | B     |

### Key Points:
- **Primary key**: Combination of `(StudentID, CourseCode)`
- A student can take multiple courses
- A course can be taken by multiple students
- Each student-course combination should have exactly one grade

### 🔍 Functional Dependencies:
- **(StudentID, CourseCode) → Grade** ✅
- Each student-course pair determines exactly one grade

### ❌ Violation Example:

If we add this conflicting row:

| StudentID | CourseCode | Grade |
|-----------|------------|-------|
| 101       | CS101      | C     |

Now we have:

| StudentID | CourseCode | Grade |
|-----------|------------|-------|
| 101       | CS101      | A     |
| 101       | MA102      | B     |
| 102       | CS101      | B     |
| 101       | CS101      | C     |

### 🚨 Problem:
- The same `(StudentID, CourseCode)` pair `(101, CS101)` is giving **two different grades** (A and C)
- This violates the functional dependency: **(StudentID, CourseCode) → Grade**
---
