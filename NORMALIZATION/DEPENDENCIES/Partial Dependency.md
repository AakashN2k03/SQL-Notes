# 📘 Partial Dependency in Database Management Systems (DBMS)

## Table of Contents
- [Overview](#overview)
- [Definition](#definition)
- [Prerequisites](#prerequisites)
- [When Partial Dependencies Occur](#when-partial-dependencies-occur)
- [Example Demonstration](#example-demonstration)
- [Problems Caused](#problems-caused)
- [Solution](#solution)
- [Implementation Guide](#implementation-guide)
- [Best Practices](#best-practices)
- [Related Concepts](#related-concepts)

## Overview

This documentation provides a comprehensive guide to understanding **Partial Dependency** in Database Management Systems, a crucial concept in database normalization that helps identify and resolve data redundancy issues.

## Definition

**Partial Dependency** occurs when a **non-prime attribute** (an attribute that is not part of any candidate key) is **functionally dependent on only part of a candidate key**, rather than the entire candidate key.

### Key Terms:
- **Non-prime attribute**: An attribute that is not part of any candidate key
- **Candidate key**: A minimal set of attributes that can uniquely identify a tuple
- **Functional dependency**: A relationship where one attribute determines another

## Prerequisites

To understand partial dependencies, you should be familiar with:
- Database fundamentals
- Primary keys and composite keys
- Functional dependencies
- Database normalization concepts

## When Partial Dependencies Occur

Partial dependencies **only occur in tables that have a composite primary key** (a primary key consisting of more than one column). In tables with single-column primary keys, partial dependencies cannot exist.

### Conditions for Partial Dependency:
1. Table must have a composite candidate key
2. Non-prime attribute depends on only part of the composite key
3. The dependency is not on the complete candidate key

## Example Demonstration

Consider the following **Student Enrollment** table:

| StudentID | CourseID | StudentName | CourseName | Credits |
|-----------|----------|-------------|------------|---------|
| 101       | CS101    | Alice       | Computer Science | 3 |
| 101       | MA101    | Alice       | Mathematics | 4 |
| 102       | CS101    | Bob         | Computer Science | 3 |
| 102       | PH101    | Bob         | Physics | 3 |

### Key Analysis:
- **Composite Primary Key**: (`StudentID`, `CourseID`)
- **Non-prime attributes**: `StudentName`, `CourseName`, `Credits`

### Functional Dependencies:
```
StudentID → StudentName                    ✅ (Partial Dependency)
CourseID → CourseName                      ✅ (Partial Dependency)  
CourseID → Credits                         ✅ (Partial Dependency)
(StudentID, CourseID) → All attributes     ✅ (Full Dependency)
```

### Partial Dependencies Identified:
1. `StudentName` depends only on `StudentID` (not the full composite key)
2. `CourseName` depends only on `CourseID` (not the full composite key)
3. `Credits` depends only on `CourseID` (not the full composite key)

## Problems Caused

Partial dependencies lead to several database anomalies:

### 1. Data Redundancy
- Student names are repeated for each course enrollment
- Course information is duplicated across multiple enrollments

### 2. Update Anomalies
- If a student changes their name, multiple rows must be updated
- Risk of inconsistent data if some updates fail

### 3. Insert Anomalies
- Cannot add a new course without having at least one student enrolled
- Cannot add a new student without course enrollment

### 4. Delete Anomalies
- Deleting the last enrollment for a course removes all course information
- Loss of course data when no students are enrolled

### 5. Storage Inefficiency
- Unnecessary duplication increases storage requirements
- Impacts database performance

## Solution

To eliminate partial dependencies, decompose the table to achieve **Second Normal Form (2NF)**:

### Decomposed Tables:

#### Students Table
| StudentID | StudentName |
|-----------|-------------|
| 101       | Alice       |
| 102       | Bob         |

#### Courses Table
| CourseID | CourseName | Credits |
|----------|------------|---------|
| CS101    | Computer Science | 3 |
| MA101    | Mathematics | 4 |
| PH101    | Physics | 3 |

#### Enrollments Table
| StudentID | CourseID |
|-----------|----------|
| 101       | CS101    |
| 101       | MA101    |
| 102       | CS101    |
| 102       | PH101    |

### Benefits of Decomposition:
- ✅ Eliminates data redundancy
- ✅ Prevents update anomalies
- ✅ Reduces storage requirements
- ✅ Achieves 2NF compliance
- ✅ Maintains data integrity
