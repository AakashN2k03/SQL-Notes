# 🔑 Super Key in Database Management Systems

## 🔑 What is a **Super Key**?

A **Super Key** is any **set of one or more columns** that can **uniquely identify** a row in a table.

### Key Points:
- ✅ **All Candidate Keys are Super Keys**
- ❌ **Not all Super Keys are Candidate Keys** (because they might have extra columns)

## 🧠 Real-Life Analogy

Imagine a student record with the following attributes:
- `RollNumber` = 101
- `Email` = student101@abc.edu
- `Name` = Aakash

### Examples of Super Keys:
- `RollNumber` ✅
- (`RollNumber`, `Email`) ✅ (still uniquely identifies)
- (`RollNumber`, `Email`, `Name`) ✅ (still unique)

> **Note:** Only the **minimal** one is called a **Candidate Key**, others are just **Super Keys**.

## 🧾 Table Example

| RollNumber | Email | Name |
|------------|-------|------|
| 101 | aakash@gmail.com | Aakash |
| 102 | anu@gmail.com | Anu |

### ✅ Super Keys (unique identifiers):
- `RollNumber`
- `Email`
- (`RollNumber`, `Email`)
- (`RollNumber`, `Email`, `Name`)
- And more combinations...

### 🎯 Candidate Keys:
- `RollNumber`
- `Email`

Only those that are **minimal** and **still uniquely identify** a row qualify as Candidate Keys.

## 🔁 Key Types Summary

| Term | Definition |
|------|------------|
| **Super Key** | Any set of column(s) that uniquely identifies a row |
| **Candidate Key** | Minimal super key (no extra columns) |
| **Primary Key** | One of the candidate keys chosen to uniquely identify rows |
| **Alternate Key** | Other candidate keys not selected as primary |

## 🔍 SQL Schema Example

```sql
-- Example table structure
CREATE TABLE Students (
    RollNumber INT,
    Email VARCHAR(100),
    Name VARCHAR(100)
);
```

### Possible **Super Keys**:
- `RollNumber`
- `Email`
- (`RollNumber`, `Email`)
- (`Email`, `Name`)
- (`RollNumber`, `Name`, `Email`)

✅ All of these can uniquely identify a student.

> **Important:** Only `RollNumber` and `Email` are **Candidate Keys** if they alone can uniquely identify a row.

## 🔍 **Difference Between Candidate Key and Super Key**

| Feature | **Candidate Key** | **Super Key** |
|---------|-------------------|---------------|
| **Definition** | A **minimal** set of columns that uniquely identify a row | **Any** set of columns that uniquely identify a row |
| **Uniqueness** | ✅ Must be unique | ✅ Must be unique |
| **Minimality** | ✅ Must be minimal (no extra columns) | ❌ Can include extra columns |
| **Subset of** | Super Key | Superset (includes candidate keys and more) |
| **Primary Key?** | One candidate key becomes the Primary Key | A primary key is also a super key |
| **Number of Keys** | Usually fewer | Usually more |

## 🔑 Conclusion

### Key Takeaways:
- **Super Key** = Any key that uniquely identifies rows
- **Candidate Key** = Minimal version of a super key
- All **Primary & Alternate Keys** are **Super Keys**, but not vice versa

### Hierarchy:
```
Super Keys (Broad Category)
    ├── Candidate Keys (Minimal Super Keys)
    │   ├── Primary Key (Chosen Candidate Key)
    │   └── Alternate Keys (Other Candidate Keys)
    └── Non-minimal Super Keys (Extra columns included)
```
