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


## 🔧 Implementation Tips

- ✅ PRIMARY KEY constraint → for the selected candidate key
- ✅ UNIQUE constraint → for the remaining candidate keys (i.e., alternate keys)
- 
### Enforce Candidate Keys:
```sql
-- Method 1: During table creation
CREATE TABLE Students (
    RollNumber INT PRIMARY KEY,           -- Enforces 1st candidate key
    Email VARCHAR(100) UNIQUE,            -- Enforces 2nd candidate key (alternate key)
    AadharNumber CHAR(12) UNIQUE,         -- Enforces 3rd candidate key (alternate key)
    Name VARCHAR(100)
);


-- Method 2: Adding constraints later

ALTER TABLE Students 
ADD CONSTRAINT uk_email UNIQUE (Email);
```
### 📚 Remember: **Every table should have at least one candidate key**, and **one candidate key must be chosen as the primary key** to ensure proper database design.
