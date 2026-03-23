# Experiment 2: DDL Commands

## AIM
To study and implement DDL commands and different types of constraints.

## THEORY

### 1. CREATE
Used to create a new relation (table).

**Syntax:**
```sql
CREATE TABLE (
  field_1 data_type(size),
  field_2 data_type(size),
  ...
);
```
### 2. ALTER
Used to add, modify, drop, or rename fields in an existing relation.
(a) ADD
```sql
ALTER TABLE std ADD (Address CHAR(10));
```
(b) MODIFY
```sql
ALTER TABLE relation_name MODIFY (field_1 new_data_type(size));
```
(c) DROP
```sql
ALTER TABLE relation_name DROP COLUMN field_name;
```
(d) RENAME
```sql
ALTER TABLE relation_name RENAME COLUMN old_field_name TO new_field_name;
```
### 3. DROP TABLE
Used to permanently delete the structure and data of a table.
```sql
DROP TABLE relation_name;
```
### 4. RENAME
Used to rename an existing database object.
```sql
RENAME TABLE old_relation_name TO new_relation_name;
```
### CONSTRAINTS
Constraints are used to specify rules for the data in a table. If there is any violation between the constraint and the data action, the action is aborted by the constraint. It can be specified when the table is created (using CREATE TABLE) or after it is created (using ALTER TABLE).
### 1. NOT NULL
When a column is defined as NOT NULL, it becomes mandatory to enter a value in that column.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) NOT NULL
);
```
### 2. UNIQUE
Ensures that values in a column are unique.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) UNIQUE
);
```
### 3. CHECK
Specifies a condition that each row must satisfy.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) CHECK (logical_expression)
);
```
### 4. PRIMARY KEY
Used to uniquely identify each record in a table.
Properties:
Must contain unique values.
Cannot be null.
Should contain minimal fields.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) PRIMARY KEY
);
```
### 5. FOREIGN KEY
Used to reference the primary key of another table.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size),
  FOREIGN KEY (column_name) REFERENCES other_table(column)
);
```
### 6. DEFAULT
Used to insert a default value into a column if no value is specified.

Syntax:
```sql
CREATE TABLE Table_Name (
  col_name1 data_type,
  col_name2 data_type,
  col_name3 data_type DEFAULT 'default_value'
);
```

**Question 1**
--
    Insert all students from Archived_students table into the Student_details table.
    
    cid         name        type        notnull     dflt_value  pk
    ----------  ----------  ----------  ----------  ----------  ----------
    0           RollNo      INT           0                       1
    1           Name        VARCHAR(100)  0                       0
    2           Gender      VARCHAR(10)   0                       0
    3           Subject     VARCHAR(50)   0                       0
    4           MARKS       INT           0                       0

```sql
insert into
Student_details(RollNo,Name,Gender,Subject,MARKS)
select RollNo,Name,Gender,Subject,MARKS 
from Archived_students;
```

**Output:**

<img width="1224" height="407" alt="image" src="https://github.com/user-attachments/assets/39fa1a23-9e75-4ed6-9f0e-12717798a508" />


**Question 2**
---
    Create a table named Employees with the following constraints:
    
    EmployeeID should be the primary key.
    FirstName and LastName should be NOT NULL.
    Email should be unique.
    Salary should be greater than 0.
    DepartmentID should be a foreign key referencing the Departments table.

```sql
create table Employees(
EmployeeID int primary key,
FirstName varchar(50) not null,
LastName varchar(50) not null,
Email varchar(100) UNIQUE,
Salary decimal(10,2) CHECK (Salary>0),
DepartmentID int,
foreign key (DepartmentID) references Departments(DepartmentID));
```

**Output:**

<img width="1228" height="549" alt="image" src="https://github.com/user-attachments/assets/0752ae84-4cd5-4ea6-a77f-c555535625d4" />


**Question 3**
---
    Write a SQL query to Add a new column State as text in the Student_details table.
    
    Sample table: Student_details
    
     cid              name             type   notnull     dflt_value  pk
    ---------------  ---------------  -----  ----------  ----------  ----------
    0                RollNo           int    0                       1
    1                Name             VARCH  1                       0
    2                Gender           TEXT   1                       0
    3                Subject          VARCH  0                       0
    4                MARKS            INT (  0                       0

```sql
alter table Student_details
add column State TEXT;
```

**Output:**

<img width="1214" height="481" alt="image" src="https://github.com/user-attachments/assets/8ceb3398-717c-4c8e-aecb-800471f30983" />


**Question 4**
---
    Create a table named Department with the following constraints:
    DepartmentID as INTEGER should be the primary key.
    DepartmentName as TEXT should be unique and not NULL.
    Location as TEXT.

```sql
CREATE TABLE Department(
DepartmentID int primary key,
DepartmentName text unique not null,
Location text
);
```

**Output:**

<img width="1218" height="393" alt="image" src="https://github.com/user-attachments/assets/0f266d5c-f25b-4788-a0a8-26e6cc4cdc6b" />


**Question 5**
---
    Insert a product with ProductID 104, Name Tablet, and Category Electronics into the Products table, where Price and Stock should use default values.

```sql
insert into products(ProductID, Name, Category)
VALUES (104,'Tablet','Electronics');
```

**Output:**

<img width="1210" height="348" alt="image" src="https://github.com/user-attachments/assets/d174ed5c-1ad4-48ba-ab16-e4c6b0b8daa3" />


**Question 6**
---
    Insert the following products into the Products table:
    
    Name        Category     Price       Stock
    ----------  -----------  ----------  ----------
    Smartphone  Electronics  800         150
    Headphones  Accessories  200         300

```sql
INSERT INTO Products(Name, Category, Price, Stock)
VALUES ('Smartphone','Electronics',800,150),('Headphones','Accessories',200,300);
```

**Output:**

<img width="1220" height="392" alt="image" src="https://github.com/user-attachments/assets/ccedce2b-e14a-4415-bea0-30f13580773c" />


**Question 7**
---
    Write an SQL command can to add a column named email of type TEXT to the customers table

```sql
ALTER TABLE customers
add column email TEXT;
```

**Output:**

<img width="1216" height="405" alt="image" src="https://github.com/user-attachments/assets/599b8afb-bd38-44e5-b0c7-828901f44586" />


**Question 8**
---
    Create a table named Locations with the following columns:
    
    LocationID as INTEGER
    LocationName as TEXT
    Address as TEXT

```sql
CREATE TABLE Locations(
LocationID INTEGER,
LocationName TEXT,
Address TEXT
);
```

**Output:**

<img width="1221" height="493" alt="image" src="https://github.com/user-attachments/assets/efc972f9-ed38-46f6-95a8-0b7fb7a1ac48" />


**Question 9**
---
    Create a table named ProjectAssignments with the following constraints:
    AssignmentID as INTEGER should be the primary key.
    EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
    ProjectID as INTEGER should be a foreign key referencing Projects(ProjectID).
    AssignmentDate as DATE should be NOT NULL.

```sql
PRAGMA foreign_keys = ON;
CREATE TABLE ProjectAssignments(
AssignmentID INTEGER PRIMARY KEY,
EmployeeID INTEGER,
FOREIGN KEY(EmployeeID) REFERENCES Employees(EmployeeID),
ProjectID INTEGER,
FOREIGN KEY(ProjectID) REFERENCES Projects(ProjectsID), 
AssignmentDate DATE NOT NULL
);
INSERT INTO ProjectAssignments (AssignmentID, EmployeeID, ProjectID, AssignmentDate) VALUES (1, 1, 1, '2024-01-02');
select * from ProjectAssignments; 
```

**Output:**

<img width="1207" height="547" alt="image" src="https://github.com/user-attachments/assets/805ba8e0-e956-44de-b9ee-feb72025f859" />


**Question 10**
---
    Create a table named Products with the following constraints:
    ProductID as INTEGER should be the primary key.
    ProductName as TEXT should be unique and not NULL.
    Price as REAL should be greater than 0.
    StockQuantity as INTEGER should be non-negative.

```sql

```

**Output:**

<img width="1166" height="577" alt="image" src="https://github.com/user-attachments/assets/a89b2d56-476b-4bab-aba5-1101932b73b7" />



## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
