# Foreign Key Guide

## 🔗 What is a Foreign Key?

A **foreign key** is a column (or a group of columns) in one table that **links to the primary key of another table**.

It is used to **maintain relationships between tables** and ensures **referential integrity** – meaning, data must be valid and consistent between related tables.

## ✅ Properties of a Foreign Key

1. It **references** a column (usually a primary key) in another table
2. It ensures that the value in the foreign key column **must exist** in the referenced table
3. It can be **NULL**, unless specified otherwise
4. It can have **duplicate values** (not unique like primary key)

## 🧠 Why Use a Foreign Key?

- To **link tables** logically
- To **prevent invalid data** entry
- To **model real-world relationships**, e.g., customers placing orders
- To maintain **data consistency** across related tables
- To enable **efficient joins** between tables

## 🛠️ Syntax of Foreign Key

### Example 1: Creating a foreign key while creating the table

```sql
CREATE TABLE Customers (
    CustomerID INT PRIMARY KEY,
    Name VARCHAR(100)
);

CREATE TABLE Orders (
    OrderID INT PRIMARY KEY,
    CustomerID INT,
    OrderDate DATE,
    FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID)
);
```

✅ Here:
- `CustomerID` in `Orders` table is a **foreign key**
- It points to `CustomerID` in `Customers` table (the **parent table**)

### Example 2: Adding a foreign key using `ALTER TABLE`

```sql
ALTER TABLE Orders 
ADD CONSTRAINT fk_customer 
FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID);
```

### Example 3: Multiple Foreign Keys

```sql
CREATE TABLE OrderDetails (
    OrderDetailID INT PRIMARY KEY,
    OrderID INT,
    ProductID INT,
    Quantity INT,
    FOREIGN KEY (OrderID) REFERENCES Orders(OrderID),
    FOREIGN KEY (ProductID) REFERENCES Products(ProductID)
);
```

## 🧾 Sample Data Example

### Customers Table:
| CustomerID | Name |
|------------|------|
| 101        | John |
| 102        | Asha |

### Orders Table:
| OrderID | CustomerID | OrderDate  |
|---------|------------|------------|
| 1       | 101        | 2024-05-01 |
| 2       | 102        | 2024-05-02 |

✅ This is valid because both `CustomerID`s exist in the `Customers` table.

## ❌ Invalid Insertion Example

```sql
INSERT INTO Orders (OrderID, CustomerID, OrderDate) 
VALUES (3, 999, '2024-05-03');
```

🛑 **Error:** Foreign key constraint fails — CustomerID `999` does not exist in `Customers` table.

## 🔐 What is Referential Integrity?

It means that the **foreign key must match a valid primary key value** from the other table – this ensures your database is consistent and accurate.

## 🔄 Foreign Key Actions (Cascade Options)

### 1. `ON DELETE CASCADE`

👉 If a row in the **parent table** is **deleted**, then **automatically delete all matching rows** in the **child table**.

```sql
CREATE TABLE Orders (
    OrderID INT PRIMARY KEY,
    CustomerID INT,
    OrderDate DATE,
    FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID) 
    ON DELETE CASCADE
);
```

**Scenario:**
```sql
DELETE FROM Customers WHERE CustomerID = 101;
```
✅ All orders with `CustomerID = 101` in the `Orders` table will also be **automatically deleted**.

### 2. `ON DELETE SET NULL`

👉 If a row in the **parent table** is deleted, the matching foreign key in the **child table is set to NULL**.

```sql
CREATE TABLE Orders (
    OrderID INT PRIMARY KEY,
    CustomerID INT, -- Must allow NULL
    OrderDate DATE,
    FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID) 
    ON DELETE SET NULL
);
```

📝 You must allow `CustomerID` to be NULL in the `Orders` table.

**Example:**
```sql
DELETE FROM Customers WHERE CustomerID = 101;
```
✅ The matching `CustomerID` in `Orders` becomes `NULL`.

### 3. `ON DELETE RESTRICT` (default behavior)

👉 Prevent the deletion of the parent row **if there is a matching child row**.

```sql
-- This will cause an error if orders exist:
DELETE FROM Customers WHERE CustomerID = 101;
```
🛑 **Error:** Cannot delete or update because of foreign key constraint.

### 4. `ON DELETE NO ACTION`

👉 **Do nothing** – deny deletion if child records exist (same as RESTRICT in most databases).

### 5. `ON UPDATE CASCADE`

👉 If the **primary key in the parent table is updated**, the **foreign key in the child table is also updated** automatically.

```sql
CREATE TABLE Orders (
    OrderID INT PRIMARY KEY,
    CustomerID INT,
    OrderDate DATE,
    FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID) 
    ON UPDATE CASCADE
);
```

**Example:**
```sql
UPDATE Customers SET CustomerID = 999 WHERE CustomerID = 101;
```
✅ Now, all orders where `CustomerID = 101` will be updated to `999`.


## 🔍 Managing Foreign Keys

### View Foreign Key Constraints
```sql
-- MySQL
SELECT 
    CONSTRAINT_NAME,
    TABLE_NAME,
    COLUMN_NAME,
    REFERENCED_TABLE_NAME,
    REFERENCED_COLUMN_NAME
FROM INFORMATION_SCHEMA.KEY_COLUMN_USAGE
WHERE REFERENCED_TABLE_NAME IS NOT NULL;
```

### Drop Foreign Key Constraint
```sql
ALTER TABLE Orders 
DROP FOREIGN KEY fk_customer;
```

### Check Foreign Key Violations
```sql
-- Find orders with invalid customer IDs
SELECT o.* 
FROM Orders o 
LEFT JOIN Customers c ON o.CustomerID = c.CustomerID 
WHERE c.CustomerID IS NULL AND o.CustomerID IS NOT NULL;
```

## 💡 Best Practices

1. **Name constraints clearly** - Use descriptive names like `fk_orders_customer`
2. **Choose appropriate cascade options** - Consider business requirements
3. **Index foreign key columns** - Improves join performance
4. **Validate data before insertion** - Prevent constraint violations
5. **Document relationships** - Maintain clear ER diagrams
6. **Consider performance impact** - Foreign keys add overhead to DML operations

## ⚠️ Important Notes

- A foreign key can reference a **composite key**
- Foreign keys can be **self-referencing** (point to same table)
- **Multiple foreign keys** can exist in a single table
- Foreign key constraints are **checked during INSERT, UPDATE, and DELETE** operations
- **Circular references** should be avoided or handled carefully
- Foreign keys help the query optimizer create better execution plans

## 🚀 Advanced Examples

### Self-Referencing Foreign Key (Employee-Manager Relationship)
```sql
CREATE TABLE Employees (
    EmployeeID INT PRIMARY KEY,
    Name VARCHAR(100),
    ManagerID INT,
    FOREIGN KEY (ManagerID) REFERENCES Employees(EmployeeID)
);
```

### Multiple Cascade Options
```sql
CREATE TABLE Orders (
    OrderID INT PRIMARY KEY,
    CustomerID INT,
    OrderDate DATE,
    FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID) 
    ON DELETE CASCADE 
    ON UPDATE CASCADE
);
```

---

*Foreign keys are fundamental to relational database design, ensuring data integrity and enabling complex relationships between tables while maintaining consistency across your database.*
