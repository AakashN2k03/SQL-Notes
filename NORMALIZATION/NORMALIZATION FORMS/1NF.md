# 🧾 First Normal Form (1NF) in DBMS

## 🔹 Definition:
A relation is in **First Normal Form (1NF)** if:
1. **All attributes (columns) contain only atomic (indivisible) values**.
2. **Each column contains values of the same data type**.
3. **Each record is unique (there is a primary key)**.

## 🚫 Violates 1NF Example:

| StudentID | Name  | Courses       |
|-----------|-------|---------------|
| 101       | Alice | Math, Science |
| 102       | Bob   | English       |

Here, the `Courses` column contains **multiple values**. This violates **1NF**.

## ✅ 1NF-Compliant Table:

| StudentID | Name  | Course  |
|-----------|-------|---------|
| 101       | Alice | Math    |
| 101       | Alice | Science |
| 102       | Bob   | English |

* Now, each field holds **atomic values only**.
* The table satisfies **1NF**.

## 🎯 Why 1NF is important:
* Ensures data consistency.
* Removes multi-valued attributes.
* It's the **foundation** for higher normal forms (2NF, 3NF, etc.)
