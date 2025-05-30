# Primary Key Guide

## 🔑 What is a Primary Key?

A **Primary Key** is a column (or a set of columns) in a table that **uniquely identifies each row** in that table. It serves as a unique identifier for database records and ensures data integrity.

## ✅ Properties of a Primary Key

1. **Uniqueness** – No two rows can have the same value in the primary key column
2. **Not NULL** – It must have a value. You cannot leave it empty
3. **One per table** – A table can have **only one** primary key
4. **Can be composite** – A primary key can include more than one column (called a **composite key**)

## 🔧 Syntax of Primary Key

### Creating a table with a primary key:

```sql
CREATE TABLE Students (
    StudentID INT PRIMARY KEY,
    Name VARCHAR(100),
    Age INT
);
```

**Output:** `StudentID` is now the primary key. Each student must have a unique and non-null `StudentID`.

### Alternative syntax:

```sql
CREATE TABLE Students (
    StudentID INT,
    Name VARCHAR(100),
    Age INT,
    PRIMARY KEY (StudentID)
);
```

### Composite Primary Key:

```sql
CREATE TABLE Enrollment (
    StudentID INT,
    CourseID INT,
    EnrollmentDate DATE,
    PRIMARY KEY (StudentID, CourseID)
);
```

## 🛑 What Happens If You Violate Primary Key Rules?

### 1. Inserting duplicate values:

```sql
-- First insertion (successful)
INSERT INTO Students (StudentID, Name, Age) 
VALUES (101, 'John', 20);

-- Second insertion with same ID (will fail)
INSERT INTO Students (StudentID, Name, Age) 
VALUES (101, 'Mike', 22);
```

**🛑 Error:** Duplicate entry for primary key.

### 2. Inserting NULL:

```sql
INSERT INTO Students (StudentID, Name, Age) 
VALUES (NULL, 'Asha', 21);
```

**🛑 Error:** Primary key column cannot be NULL.

## 📝 Best Practices

- Choose a column that will never change (like ID numbers)
- Use simple data types (integers are preferred)
- Keep primary keys as short as possible
- Consider using auto-incrementing integers for surrogate keys
- Avoid using business data as primary keys when possible

## 🔄 Adding/Removing Primary Keys

### Adding a primary key to an existing table:

```sql
ALTER TABLE Students 
ADD PRIMARY KEY (StudentID);
```

### Removing a primary key:

```sql
ALTER TABLE Students 
DROP PRIMARY KEY;
```

## 💡 Common Use Cases

- **Student Management System:** StudentID as primary key
- **Product Catalog:** ProductID as primary key
- **User Authentication:** UserID as primary key
- **Order Processing:** OrderID as primary key

## ⚠️ Important Notes

- Every table should have a primary key for optimal database performance
- Primary keys automatically create a unique index
- Foreign keys in other tables often reference primary keys
- Primary key constraints are enforced at the database level

---

*This guide covers the fundamental concepts of primary keys in relational databases. Understanding primary keys is essential for proper database design and data integrity.*
