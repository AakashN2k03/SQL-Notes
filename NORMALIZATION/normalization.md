# Database Normalization Overview

---

## 📋 What is Normalization?

Normalization is a process used in designing a database to organize data to:

- 🔄 **Reduce redundancy** (duplicate data)
- ⚠️ **Avoid inconsistency** (conflicting data)
- ✔️ **Improve data integrity** (accuracy and consistency)
- ⚙️ **Make the database efficient and easier to maintain**

It involves dividing a large table into smaller, related tables and defining relationships between them.

---

## ❓ Why is Normalization Important?

- 💾 **Reduces Redundancy**  
  Storing the same data multiple times wastes space and increases the risk of inconsistencies.

- 🚫 **Prevents Data Anomalies:**  
  - **Insertion Anomalies:** Inability to add data because of missing related data  
    _(e.g., unable to add a new student without a course if both are in the same table)_  
  - **Update Anomalies:** Changing data in one place but not in others, leading to inconsistencies  
    _(e.g., updating a teacher's name in one record but not others)_  
  - **Deletion Anomalies:** Losing unrelated data when deleting a record  
    _(e.g., deleting a student’s record also deletes course information)_

- ⚡ **Improves Query Efficiency**  
  Well-structured tables make queries faster and easier to write.

- 📈 **Ensures Scalability**  
  Normalized databases are easier to maintain and scale as data grows.

---

## 🔑 Key Concepts in Normalization

Before diving into normal forms, here are some fundamental concepts:

| Concept                | Description                                                                                  |
|------------------------|----------------------------------------------------------------------------------------------|
| 🆔 **Primary Key**      | A unique identifier for each record in a table (e.g., `StudentID` in a Students table).      |
| 🔗 **Foreign Key**      | A field in one table that references the primary key of another table, establishing relation. |
| 📊 **Functional Dependency** | A relationship where one attribute uniquely determines another (e.g., `StudentID` determines `StudentName`). |
| ⚠️ **Partial Dependency**    | When a non-key attribute depends on only part of a composite primary key.                   |
| ↪️ **Transitive Dependency** | When a non-key attribute depends on another non-key attribute.                              |

---

## 📚 Summary

Normalization is essential for:

- Reducing data duplication  
- Preventing data anomalies  
- Improving database performance and integrity  
- Designing scalable and maintainable databases

---

If you'd like me to help with examples of normalization or SQL queries, just ask! 😊
