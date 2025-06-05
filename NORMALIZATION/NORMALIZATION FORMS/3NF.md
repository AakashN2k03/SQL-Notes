# 🧾 Third Normal Form (3NF)

## 🔹 Definition:
A table is in **Third Normal Form (3NF)** if:
1. ✅ It is in **Second Normal Form (2NF)**
2. ❌ It has **no transitive dependencies** — i.e., **non-prime attributes** must depend **only on the candidate key**, not on other non-prime attributes.

## 🔁 Recap: What is Transitive Dependency?
If:
* `A → B` and `B → C` Then: `A → C` is a **transitive dependency**.

In DBMS, it means a **non-prime attribute** depends **on another non-prime attribute**, not directly on the key.

## 🚫 3NF Violation Example:

| EmpID | EmpName | DeptID | DeptName |
|-------|---------|--------|----------|
| 101   | Alice   | D1     | HR       |
| 102   | Bob     | D2     | Finance  |
| 103   | Carol   | D1     | HR       |

* **Candidate key**: `EmpID`
* `EmpName`, `DeptID`, `DeptName` are **non-prime attributes**
* `EmpID → DeptID`
* `DeptID → DeptName` ⛔ So: `EmpID → DeptName` (transitive dependency — violation of 3NF)

## ✅ How to Normalize (Achieve 3NF):
Split into two tables:

### 1. Employee Table
| EmpID | EmpName | DeptID |
|-------|---------|--------|
| 101   | Alice   | D1     |
| 102   | Bob     | D2     |
| 103   | Carol   | D1     |

### 2. Department Table
| DeptID | DeptName |
|--------|----------|
| D1     | HR       |
| D2     | Finance  |

Now:
* `EmpID` → `EmpName`, `DeptID`
* `DeptID` → `DeptName`
* No transitive dependency ✅
* Satisfies 3NF ✅

## 💡 Summary Table:

| Rule | Description |
|------|-------------|
| Already in 2NF | No partial dependency |
| No transitive dependency | Non-prime attributes should depend **only on the candidate key** |
| Why needed | To reduce redundancy, avoid anomalies |
