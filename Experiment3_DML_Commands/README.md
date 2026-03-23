# Experiment 3: DML Commands

## AIM
To study and implement DML (Data Manipulation Language) commands.

## THEORY

### 1. INSERT INTO
Used to add records into a relation.
These are three type of INSERT INTO queries which are as
A)Inserting a single record
**Syntax (Single Row):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES (value_1, value_2, ...);
```
**Syntax (Multiple Rows):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES
(value_1, value_2, ...),
(value_3, value_4, ...);
```
**Syntax (Insert from another table):**
```sql
INSERT INTO table_name SELECT * FROM other_table WHERE condition;
```
### 2. UPDATE
Used to modify records in a relation.
Syntax:
```sql
UPDATE table_name SET column1 = value1, column2 = value2 WHERE condition;
```
### 3. DELETE
Used to delete records from a relation.
**Syntax (All rows):**
```sql
DELETE FROM table_name;
```
**Syntax (Specific condition):**
```sql
DELETE FROM table_name WHERE condition;
```
### 4. SELECT
Used to retrieve records from a table.
**Syntax:**
```sql
SELECT column1, column2 FROM table_name WHERE condition;
```
**Question 1**
--
    Write a SQL statement to Increase the selling price by 10% for all products in the 'Bakery' category in the products table.
    
    Products table
    
    ---------------
    product_id
    product_name
    category
    cost_price
    sell_price
    reorder_lvl
    quantity
    supplier_id

```sql
UPDATE products 
SET sell_price=sell_price*1.1 
WHERE category='Bakery';
```

**Output:**

<img width="1337" height="319" alt="image" src="https://github.com/user-attachments/assets/ab0d8751-0636-4c70-9e07-deed858e4bf4" />


**Question 2**
---
    Write a SQL statement to Increase quantity of all products by 10% to adjust for surplus stock counted
    
    Products table
    
    ---------------
    product_id
    product_name
    category
    cost_price
    sell_price
    reorder_lvl
    quantity
    supplier_id

```sql
UPDATE Products
SET quantity = quantity*1.1;
```

**Output:**

<img width="1202" height="373" alt="image" src="https://github.com/user-attachments/assets/fd4c9526-1bb0-4b2d-87b0-a237fba864b6" />


**Question 3**
---
    For  Increase the selling price per unit by 3 for all products supplied by supplier ID 4 in the sales table.
    
    PRODUCTS TABLE
    
    name               type
    -----------------  ---------------
    product_id         INT
    product_name       VARCHAR(100)
    category           VARCHAR(50)
    cost_price         DECIMAL(10,2)
    sell_price         DECIMAL(10,2)
    reorder_lvl        INT
    quantity           INT
    supplier_id        INT
    
    SALES TABLE
    name               type
    -----------------  ---------------
    sale_id            INT
    sale_date          DATE
    product_id         INT
    quantity           INT
    sell_price         DECIMAL(10,2)
    total_sell_price   DECIMAL(10,2)

```sql
UPDATE SALES 
SET sell_price = sell_price+3
WHERE product_id IN(SELECT product_id FROM Products
WHERE supplier_id=4);
```

**Output:**

<img width="1118" height="239" alt="image" src="https://github.com/user-attachments/assets/e740cee9-1c47-436c-8936-37e5cd57159b" />


**Question 4**
---
    Change the supplier name to upper case where contact person contains ' Singh' in suppliers table.
    
    name               type
    -----------------  ---------------
    supplier_id        INT
    supplier_name      VARCHAR(100)
    contact_person     VARCHAR(100)
    phone_number       VARCHAR(20)
    email              VARCHAR(100)
    address            VARCHAR(250)

```sql
UPDATE suppliers 
SET supplier_name=UPPER(supplier_name)
WHERE contact_person
LIKE '%Singh%';
```

**Output:**

<img width="1365" height="255" alt="image" src="https://github.com/user-attachments/assets/7853567f-1fdb-4fcf-b8e6-23e163c8d909" />


**Question 5**
---
     Paste Question 5 hereWrite a SQL query to reduce the reorder level by 30% where cost price is more than 50 and quantity in stock is less than 100 in the products table.
    
    Products Table 
    
    name          type       
    ----------    ---------- 
    product_id     INT PRIMARY KEY        
    product_name   VARCHAR(10) 
    category       VARCHAR(50) 
    cost_price     DECIMAL(10) 
    sell_price     DECIMAL(10) 
    reorder_lvl    INT        
    quantity       INT        
    supplier_id    INT  
```sql
UPDATE products
SET reorder_lvl=reorder_lvl*0.7
WHERE cost_price>50 AND quantity<100;
```

**Output:**

<img width="1369" height="304" alt="image" src="https://github.com/user-attachments/assets/dbd3fc63-9bbf-4ef8-8721-eeebf016fe10" />


**Question 6**
---
    Write a SQL query to Delete a Specific Surgery whose ID is 3
    
    Sample table: Surgeries
    
    attributes: surgery_id, patient_id, surgeon_id, surgery_date

```sql
DELETE FROM Surgeries 
WHERE surgery_id=3;
```

**Output:**

<img width="789" height="242" alt="image" src="https://github.com/user-attachments/assets/bf3ae08c-af5e-4f7e-9141-06264a219554" />


**Question 7**
---
    Write a SQL query to Delete customers from 'customer' table where 'CUST_CITY' is not 'New York' and 'OUTSTANDING_AMT' is greater than 5000.
    
    Sample table: Customer
    
```sql
DELETE FROM customer 
WHERE CUST_CITY!='New York' AND OUTSTANDING_AMT>50
```

**Output:**

<img width="1365" height="378" alt="image" src="https://github.com/user-attachments/assets/f93655c0-a733-4b06-a840-3d816379df08" />


**Question 8**
---
    Write a SQL query to Delete All Doctors with a NULL Last Name
    
    Sample table: Doctors
    
    attributes : doctor_id, first_name, last_name, specialization

```sql
DELETE FROM Doctors 
WHERE last_name is NULL;
```

**Output:**

<img width="818" height="420" alt="image" src="https://github.com/user-attachments/assets/17a13ec5-62b0-4bf1-b9f5-3383089778ba" />


**Question 9**
---
Write a SQL query to Delete customers from 'customer' table where 'WORKING_AREA' is 'New York'.

Sample table: Customer

```sql
DELETE FROM customer
WHERE WORKING_AREA='New York';
```

**Output:**

<img width="1372" height="482" alt="image" src="https://github.com/user-attachments/assets/d352495b-9aa4-478e-b142-6e55b0f2bb0d" />


**Question 10**
---
    Write a SQL query to Delete All Doctors whose ID ranges from 2 to 4.
    
    Sample table: Doctors
    
    attributes : doctor_id, first_name, last_name, specialization

```sql
DELETE FROM Doctors 
WHERE doctor_id BETWEEN 2 AND 4;
```

**Output:**

<img width="1214" height="911" alt="image" src="https://github.com/user-attachments/assets/d3d4c2f5-911a-43e4-8f5d-685cb29a502d" />


## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.
