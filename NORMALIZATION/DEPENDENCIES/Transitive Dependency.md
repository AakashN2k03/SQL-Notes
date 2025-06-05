# 🔄 Transitive Dependency in DBMS

## 🔹 Definition:
A **transitive dependency** occurs in a relation **when a non-prime attribute depends on another non-prime attribute**, **not directly on the candidate key**.
It **violates Third Normal Form (3NF)**.

## 🧠 Simple Explanation:
If:
* **A → B**
* **B → C**

Then, **A → C** is a **transitive dependency** (C depends on A through B).

## 🔍 Real Example (Violation of 3NF):

| EmpID | EmpName | DeptID | DeptName |
|-------|---------|--------|----------|
| 1     | Alice   | D1     | HR       |
| 2     | Bob     | D2     | Finance  |
| 3     | Carol   | D1     | HR       |

* **Candidate key**: `EmpID`
* **EmpName**, **DeptID**, and **DeptName** are non-prime attributes

## 🔎 Functional Dependencies:
* `EmpID → DeptID` ✅ (good)
* `DeptID → DeptName` ✅
* So: `EmpID → DeptName` ❌ (this is **transitive dependency**)

Here, **DeptName** is **not directly dependent** on the candidate key `EmpID`, but through another non-prime attribute `DeptID`.

## 🚨 Problems with Transitive Dependency:
* **Redundancy**: "HR" repeated multiple times.
* **Update Anomaly**: If "HR" changes to "Human Resources", you have to update every row.
* **Inconsistent data** may occur.

## ✅ Fix: Normalize to **3NF**
Split into two tables:

### 1. Employee Table
| EmpID | EmpName | DeptID |
|-------|---------|--------|
| 1     | Alice   | D1     |
| 2     | Bob     | D2     |
| 3     | Carol   | D1     |

### 2. Department Table
| DeptID | DeptName |
|--------|----------|
| D1     | HR       |
| D2     | Finance  |

Now, all non-prime attributes depend **only on the candidate key** and **not on other non-prime attributes**.
