# Candidate Key in Database Design

## 🔑 What is a Candidate Key?

A **Candidate Key** is a column (or a set of columns) in a table that can **uniquely identify every row** in that table.

✅ **Every table can have multiple candidate keys**, but **only one of them** is chosen as the **Primary Key**.

The others become **Alternate Keys**.

## 📌 Key Properties (Simple)

A candidate key must be:

1. **Unique** (no duplicates allowed)
2. **Not null** (cannot contain empty values)
3. **Minimal** (no extra/unnecessary columns)

## 🧠 Real-Life Analogy

Imagine a student who has:
- 🎓 **Roll Number**
- 🆔 **Aadhaar Number** 
- 📧 **University Email**

All three can uniquely identify that student — these are **candidate keys**.

But we might choose **Roll Number** as the **Primary Key**.

✅ The rest (Aadhaar and Email) become **Alternate Keys**

## 🛠️ SQL Example

```sql
CREATE TABLE Students (
    RollNumber INT,
    AadharNumber CHAR(12),
    Email VARCHAR(100),
    Name VARCHAR(100),
    PRIMARY KEY (RollNumber),
    UNIQUE (AadharNumber),
    UNIQUE (Email)
);
```

### 👇 Candidate Keys Analysis:
- `RollNumber`
- `AadharNumber` 
- `Email`

✅ All three can **uniquely identify** a student → So they are **candidate keys**.

🛠 But we chose `RollNumber` as **Primary Key**, so:
- `AadharNumber` & `Email` become **Alternate Keys**

## 🧾 Table Example

| RollNumber | AadharNumber | Email | Name |
|------------|--------------|-------|------|
| 101 | 123456789012 | john@gmail.com | John |
| 102 | 987654321098 | asha@gmail.com | Asha |

All columns (`RollNumber`, `AadharNumber`, `Email`) are **unique & not null** → all are **valid candidate keys**

## ✅ Properties of Candidate Keys

1. ✅ Must **uniquely identify** rows
2. ❌ No duplicates allowed
3. ❌ Cannot contain null values
4. ✅ One of them becomes the **Primary Key**
5. ✅ Others become **Alternate Keys**

> **📝 NOTE:** Every Primary Key is a Candidate Key, and all other Candidate Keys that are **not chosen** as Primary Key are called **Alternate Keys**.

## 🔍 Types of Candidate Keys

### Simple Candidate Key
A single column that can uniquely identify rows:
```sql
Email VARCHAR(100) UNIQUE  -- Single column candidate key
```

### Composite Candidate Key
Multiple columns together forming a unique identifier:
```sql
CREATE TABLE OrderDetails (
    OrderID INT,
    ProductID INT,
    Quantity INT,
    Price DECIMAL(10,2),
    UNIQUE(OrderID, ProductID)  -- Composite candidate key
);
```

## 📊 Candidate Key vs Other Keys

| Key Type | Definition | Quantity | Selection |
|----------|------------|----------|-----------|
| **Candidate Key** | Can uniquely identify rows | Multiple possible | All potential unique identifiers |
| **Primary Key** | Chosen main identifier | One per table | Selected from candidate keys |
| **Alternate Key** | Non-selected candidate keys | Multiple possible | Remaining candidate keys |

## 🎯 How to Identify Candidate Keys

### Step-by-Step Process:

1. **List all columns** in the table
2. **Check uniqueness** - does this column have unique values?
3. **Check for nulls** - can this column be null?
4. **Test minimality** - for composite keys, are all columns necessary?
5. **Verify** - does it uniquely identify every row?

### Example Analysis:
```sql
CREATE TABLE Employees (
    EmployeeID INT,
    SSN CHAR(11),
    Email VARCHAR(100),
    Phone VARCHAR(15),
    Name VARCHAR(100)
);
```

**Potential Candidate Keys:**
- ✅ `EmployeeID` - Unique, not null
- ✅ `SSN` - Unique, not null  
- ✅ `Email` - Unique, not null
- ❌ `Phone` - Might not be unique (shared phones)
- ❌ `Name` - Definitely not unique

## 🚀 Best Practices

### Choosing the Right Primary Key:
1. **Stability** - Choose keys that won't change frequently
2. **Simplicity** - Prefer single column over composite when possible
3. **Performance** - Consider indexing and join performance
4. **Business Logic** - Align with how data is accessed

### Example Decision Process:
```sql
-- Options for Primary Key:
-- EmployeeID (Auto-increment, stable, simple)
-- SSN (Natural key, but sensitive data)
-- Email (Natural key, but might change)

-- Best choice: EmployeeID
CREATE TABLE Employees (
    EmployeeID INT AUTO_INCREMENT PRIMARY KEY,  -- Chosen
    SSN CHAR(11) UNIQUE,                        -- Alternate Key
    Email VARCHAR(100) UNIQUE,                  -- Alternate Key
    Name VARCHAR(100)
);
```

## ⚠️ Common Mistakes

1. **Ignoring Minimality** - Including unnecessary columns in composite keys
2. **Allowing Nulls** - Candidate keys must be NOT NULL
3. **Poor Primary Key Choice** - Choosing unstable or complex keys as primary
4. **Missing Constraints** - Not enforcing uniqueness on alternate keys

## 🔧 Implementation Tips

### Enforce Candidate Keys:
```sql
-- Method 1: During table creation
CREATE TABLE Students (
    RollNumber INT PRIMARY KEY,
    Email VARCHAR(100) UNIQUE NOT NULL,
    AadharNumber CHAR(12) UNIQUE NOT NULL
);

-- Method 2: Adding constraints later
ALTER TABLE Students 
ADD CONSTRAINT uk_email UNIQUE (Email);

ALTER TABLE Students 
ADD CONSTRAINT uk_aadhar UNIQUE (AadharNumber);
```

### Check for Candidate Keys:
```sql
-- Find columns with unique values
SELECT column_name, COUNT(DISTINCT column_name) as unique_count, 
       COUNT(*) as total_count
FROM table_name 
GROUP BY column_name
HAVING COUNT(DISTINCT column_name) = COUNT(*);
```

## 📚 Summary

Candidate keys are the foundation of database design, ensuring data integrity and providing multiple options for uniquely identifying records. Understanding candidate keys helps you:

- **Design better databases** with proper constraints
- **Choose appropriate primary keys** based on business needs  
- **Maintain data quality** through unique constraints
- **Optimize query performance** with proper indexing

Remember: **Every table should have at least one candidate key**, and **one candidate key must be chosen as the primary key** to ensure proper database design.
