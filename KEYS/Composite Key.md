# Composite Key Guide

## 🔑 What is a Composite Key?

A **composite key** is a **primary key made up of two or more columns** that together uniquely identify a row in a table.

❗ A single column **is not enough** to uniquely identify the row, so we **combine** two or more columns to create uniqueness.

## ✅ Properties of a Composite Key

1. **Combines multiple columns** to act as one primary key
2. Each combination of values must be **unique**
3. All columns in the composite key must be **NOT NULL**
4. You can use it when **no single column is unique by itself**

## 🛠️ Syntax of Composite Key

### While Creating a Table:

```sql
CREATE TABLE CourseRegistration (
    StudentID INT,
    CourseID INT,
    RegistrationDate DATE,
    PRIMARY KEY (StudentID, CourseID)
);
```

📌 Here, `StudentID` **and** `CourseID` together form the **composite key**.

### Adding Composite Key to Existing Table:

```sql
ALTER TABLE CourseRegistration 
ADD PRIMARY KEY (StudentID, CourseID);
```

## 🧾 Example Table

| StudentID | CourseID | RegistrationDate |
|-----------|----------|------------------|
| 101       | C001     | 2024-01-10       |
| 101       | C002     | 2024-01-12       |
| 102       | C001     | 2024-01-15       |

✅ No two rows have the **same combination** of `StudentID` and `CourseID`.

## ❌ What Causes Errors?

### Duplicate Composite Key:
```sql
-- This would cause an error
INSERT INTO CourseRegistration 
VALUES (101, 'C001', '2024-02-01');
-- Error: Duplicate composite key (101, C001)
```

### NULL Values:
```sql
-- This would cause an error
INSERT INTO CourseRegistration 
VALUES (NULL, 'C003', '2024-02-01');
-- Error: Primary key column cannot be NULL
```

## 🔗 When to Use Composite Keys?

Use composite keys when:
- A single column **cannot uniquely identify** a row
- You need to ensure **uniqueness based on a combination** of values
- You want to enforce business rules at the database level

### Common Use Cases:

| Scenario | Composite Key Columns | Description |
|----------|----------------------|-------------|
| **Order Details** | OrderID + ProductID | Each product can appear once per order |
| **Course Enrollments** | StudentID + CourseID | Each student can enroll once per course |
| **Attendance Records** | StudentID + Date | One attendance record per student per day |
| **Employee Projects** | EmployeeID + ProjectID | Each employee assigned once per project |
| **Product Reviews** | CustomerID + ProductID | One review per customer per product |

## 📊 Real-World Examples

### 1. Order Details Table:
```sql
CREATE TABLE OrderDetails (
    OrderID INT,
    ProductID INT,
    Quantity INT,
    Price DECIMAL(10,2),
    PRIMARY KEY (OrderID, ProductID)
);
```

### 2. Employee Schedule Table:
```sql
CREATE TABLE EmployeeSchedule (
    EmployeeID INT,
    ShiftDate DATE,
    ShiftTime VARCHAR(20),
    PRIMARY KEY (EmployeeID, ShiftDate, ShiftTime)
);
```

### 3. Student Grades Table:
```sql
CREATE TABLE StudentGrades (
    StudentID INT,
    SubjectID INT,
    Semester VARCHAR(10),
    Grade CHAR(2),
    PRIMARY KEY (StudentID, SubjectID, Semester)
);
```

## 📌 Comparison: Primary Key vs Composite Key

| Feature | Primary Key | Composite Key |
|---------|-------------|---------------|
| **Columns involved** | One (usually) | Two or more |
| **Uniqueness basis** | Single column | Combination of columns |
| **Example** | StudentID | (StudentID, CourseID) |
| **Complexity** | Simple | More complex |
| **Storage** | Less index space | More index space |
| **Query performance** | Faster for single column | Slower for multi-column searches |


## ⚠️ Important Considerations

- **Index size**: Composite keys create larger indexes
- **Foreign key references**: Other tables must reference all columns
- **Query complexity**: Joins become more complex
- **Application code**: More parameters needed for lookups

---
*Composite keys are essential for maintaining data integrity in many-to-many relationships and ensuring business rule enforcement at the database level.*
