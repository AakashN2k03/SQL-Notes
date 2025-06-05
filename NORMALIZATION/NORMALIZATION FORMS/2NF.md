# 🧾 Second Normal Form (2NF) in DBMS

## 🔹 Definition:
A table is in **Second Normal Form (2NF)** if:
1. ✅ It is **already in First Normal Form (1NF)**.
2. ❌ It has **no partial dependencies** — meaning **non-prime attributes** depend on the **entire candidate key**, not just part of it.

## 🔁 Partial Dependency Reminder:
If a non-prime attribute depends on **part of a composite key**, it's a **partial dependency**, which violates 2NF.

## 🚫 2NF Violation Example (Assume 1NF is already satisfied):

| StudentID | CourseID | StudentName | CourseName |
|-----------|----------|-------------|------------|
| 101       | C1       | Alice       | Math       |
| 101       | C2       | Alice       | English    |
| 102       | C1       | Bob         | Math       |

* **Composite key**: `(StudentID, CourseID)`
* `StudentName` depends **only on** `StudentID`
* `CourseName` depends **only on** `CourseID`

👉 So: `StudentName` and `CourseName` are **partially dependent**, violating 2NF.

## ✅ Correct 2NF (Decomposed Tables):
Split into 3 tables:

### 1. Student Table
| StudentID | StudentName |
|-----------|-------------|
| 101       | Alice       |
| 102       | Bob         |

### 2. Course Table
| CourseID | CourseName |
|----------|------------|
| C1       | Math       |
| C2       | English    |

### 3. Enrollment Table
| StudentID | CourseID |
|-----------|----------|
| 101       | C1       |
| 101       | C2       |
| 102       | C1       |

Now:
* Every non-prime attribute depends **only on full candidate key**.
* ✅ No partial dependencies → Table is in **2NF**.

## 💡 Summary Table:

| Rule | Description |
|------|-------------|
| Must be in 1NF | Atomic values, unique rows, same data type |
| Remove partial dependencies | Non-prime attributes must depend on full key |
| When needed | Only if table has a **composite primary key** |
