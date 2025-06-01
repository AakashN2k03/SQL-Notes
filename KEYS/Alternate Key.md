# Alternate Key in Database Design

## 🔑 What is an Alternate Key?

An **Alternate Key** is a column (or combination of columns) that can **uniquely identify a row** in a table **but is not chosen as the Primary Key**.

It's essentially a **"backup" candidate key** - meaning it was a strong candidate to become the Primary Key but wasn't selected for that role.

## ✅ Key Properties

1. **Uniquely identifies** each row (just like a primary key)
2. **NOT NULL** and **must be unique** across all rows
3. There can be **multiple alternate keys** in a single table
4. Only **one key is chosen as the Primary Key**, all others become **alternate keys**

## 🛠️ SQL Example

```sql
CREATE TABLE Students (
    RollNumber INT PRIMARY KEY,
    Email VARCHAR(100) UNIQUE,
    AadharNumber CHAR(12) UNIQUE,
    Name VARCHAR(100)
);
```

### Breakdown:
- `RollNumber` is the **Primary Key** (chosen as main identifier)
- `Email` and `AadharNumber` are **Alternate Keys**
- Both `Email` and `AadharNumber` could have served as primary keys
- Since `RollNumber` was chosen as primary, the others become alternate keys

## 🧠 Real-Life Analogy

Think of identifying a student:
- 🎓 **Roll Number**: Chosen as the main identifier (Primary Key)
- 📧 **Email**: Can also uniquely identify a student (Alternate Key)
- 🆔 **Aadhaar Number**: Another unique identifier (Alternate Key)

All three can uniquely identify a student, but we pick one as the "main" identifier.

## 🔍 Implementation Details

### How Alternate Keys are Enforced
Alternate keys are implemented using the `UNIQUE` constraint:

```sql
Email VARCHAR(100) UNIQUE,
AadharNumber CHAR(12) UNIQUE
```

This ensures:
- **Uniqueness** across all rows
- **No duplicate values** allowed
- **NULL values** are typically not allowed (depending on database system)

### Multiple Column Alternate Keys
You can also have composite alternate keys:

```sql
CREATE TABLE Orders (
    OrderID INT PRIMARY KEY,
    CustomerID INT,
    OrderDate DATE,
    UNIQUE(CustomerID, OrderDate)  -- Composite alternate key
);
```

## 📊 Comparison Table

| Aspect | Primary Key | Alternate Key |
|--------|-------------|---------------|
| **Uniqueness** | ✅ Required | ✅ Required |
| **NULL Values** | ❌ Not allowed | ❌ Not allowed |
| **Quantity per Table** | 1 only | Multiple allowed |
| **Purpose** | Main identifier | Backup identifier |
| **Indexing** | Auto-indexed | Should be indexed |

## 🎯 When to Use Alternate Keys

1. **Natural Identifiers**: When you have multiple natural ways to identify records
2. **Data Integrity**: To prevent duplicate entries on important fields
3. **Query Performance**: Frequently searched columns benefit from unique constraints

## ⚠️ Important Considerations

- **Performance**: Each unique constraint creates an index, which can impact insert/update performance
- **Flexibility**: Choose your primary key carefully - alternate keys provide flexibility for future changes
- **Referential Integrity**: Foreign keys typically reference primary keys, not alternate keys
- **Database Design**: Good practice to identify all candidate keys during design phase
