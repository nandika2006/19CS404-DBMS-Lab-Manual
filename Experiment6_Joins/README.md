# Experiment 6: Joins

## AIM
To study and implement different types of joins.

## THEORY

SQL Joins are used to combine records from two or more tables based on a related column.

### 1. INNER JOIN
Returns records with matching values in both tables.

**Syntax:**
```sql
SELECT columns
FROM table1
INNER JOIN table2
ON table1.column = table2.column;
```

### 2. LEFT JOIN
Returns all records from the left table, and matched records from the right.

**Syntax:**

```sql
SELECT columns
FROM table1
LEFT JOIN table2
ON table1.column = table2.column;
```
### 3. RIGHT JOIN
Returns all records from the right table, and matched records from the left.

**Syntax:**

```sql
SELECT columns
FROM table1
RIGHT JOIN table2
ON table1.column = table2.column;
```
### 4. FULL OUTER JOIN
Returns all records when there is a match in either left or right table.

**Syntax:**

```sql
SELECT columns
FROM table1
FULL OUTER JOIN table2
ON table1.column = table2.column;
```

**Question 1**
--
    Write an SQL query that retrieves all columns from the 'customer' table (using the alias 'c'), performs a LEFT JOIN with the 'orders' table on the 'customer_id' column, and includes only those orders with an order date after '2012-08-17'.
    
    'customer' Table: (customer_id, cust_name, city, grade, salesman_id)
    
    'orders' Table: (ord_no, purch_amt, ord_date, customer_id, salesman_id)

```sql
SELECT c.*
FROM customer c
LEFT JOIN orders o
ON c.customer_id = o.customer_id
WHERE o.ord_date > '2012-08-17';
```

**Output:**

<img width="1315" height="756" alt="image" src="https://github.com/user-attachments/assets/0e5c0399-1535-4749-bb4a-b75b23c791cb" />


**Question 2**
---
    From the following tables write a SQL query to display the customer name, customer city, grade, salesman, salesman city. The results should be sorted by ascending customer_id.  
    
    Sample table: customer
    
     customer_id |   cust_name    |    city    | grade | salesman_id 
    -------------+----------------+------------+-------+-------------
            3002 | Nick Rimando   | New York   |   100 |        5001
            3007 | Brad Davis     | New York   |   200 |        5001
            3005 | Graham Zusi    | California |   200 |        5002
            3008 | Julian Green   | London     |   300 |        5002
            3004 | Fabian Johnson | Paris      |   300 |        5006
            3009 | Geoff Cameron  | Berlin     |   100 |        5003
            3003 | Jozy Altidor   | Moscow     |   200 |        5007
            3001 | Brad Guzan     | London     |       |        5005
    Sample table: salesman
    
     salesman_id |    name    |   city   | commission 
    -------------+------------+----------+------------
            5001 | James Hoog | New York |       0.15
            5002 | Nail Knite | Paris    |       0.13
            5005 | Pit Alex   | London   |       0.11
            5006 | Mc Lyon    | Paris    |       0.14
            5007 | Paul Adam  | Rome     |       0.13
            5003 | Lauson Hen | San Jose |       0.12

```sql
SELECT 
    c.cust_name,
    c.city,
    c.grade,
    s.name AS Salesman,
    s.city
FROM customer c
JOIN salesman s
ON c.salesman_id = s.salesman_id
ORDER BY c.customer_id ASC;
```

**Output:**

<img width="1316" height="807" alt="image" src="https://github.com/user-attachments/assets/274da9d7-c5ca-47ee-86c4-c1a8514a6c80" />


**Question 3**
---
    Write the SQL query that achieves the selection of the first name from the "patients" table (aliased as "patient_name") and all columns from the "test_results" table (aliased as "t"), with an inner join on the "patient_id" column and a condition filtering for patients admitted between '2024-01-01' and '2024-01-31'.

```sql
SELECT 
    p.first_name AS patient_name,
    t.*
FROM patients p
INNER JOIN test_results t
ON p.patient_id = t.patient_id
WHERE p.admission_date BETWEEN '2024-01-01' AND '2024-01-31';
```

**Output:**

<img width="1320" height="437" alt="image" src="https://github.com/user-attachments/assets/58dd9311-6b9f-45e6-9197-c2fc19aa515c" />


**Question 4**
---
    Write a SQL statement to make a report with customer name, city, order number, order date, and order amount in ascending order according to the order date to determine whether any of the existing customers have placed an order or not.
    
    Sample table: orders
    
    ord_no      purch_amt   ord_date    customer_id  salesman_id
    ----------  ----------  ----------  -----------  -----------
    70001       150.5       2012-10-05  3005         5002
    70009       270.65      2012-09-10  3001         5005
    70002       65.26       2012-10-05  3002         5001
    70004       110.5       2012-08-17  3009         5003
    70007       948.5       2012-09-10  3005         5002
    70005       2400.6      2012-07-27  3007         5001
    70008       5760        2012-09-10  3002         5001
    70010       1983.43     2012-10-10  3004         5006
    70003       2480.4      2012-10-10  3009         5003
    70012       250.45      2012-06-27  3008         5002
    70011       75.29       2012-08-17  3003         5007
    70013       3045.6      2012-04-25  3002         5001
    Sample table: customer
    
     customer_id |   cust_name    |    city    | grade | salesman_id 
    -------------+----------------+------------+-------+-------------
            3002 | Nick Rimando   | New York   |   100 |        5001
            3007 | Brad Davis     | New York   |   200 |        5001
            3005 | Graham Zusi    | California |   200 |        5002
            3008 | Julian Green   | London     |   300 |        5002
            3004 | Fabian Johnson | Paris      |   300 |        5006
            3009 | Geoff Cameron  | Berlin     |   100 |        5003
            3003 | Jozy Altidor   | Moscow     |   200 |        5007

```sql
SELECT 
    c.cust_name, 
    c.city, 
    o.ord_no, 
    o.ord_date, 
    o.purch_amt AS "Order Amount"
FROM customer c
LEFT JOIN orders o 
    ON c.customer_id = o.customer_id
ORDER BY o.ord_date ASC;
```

**Output:**

<img width="1078" height="700" alt="image" src="https://github.com/user-attachments/assets/f958c5ea-e8e2-441e-8c57-89341892e5e8" />


**Question 5**
---
    Write a SQL statement to join the tables salesman, customer and orders so that the same column of each table appears once and only the relational rows are returned. 
    
    Sample table: orders
    
    ord_no      purch_amt   ord_date    customer_id  salesman_id
    ----------  ----------  ----------  -----------  -----------
    70001       150.5       2012-10-05  3005         5002
    70009       270.65      2012-09-10  3001         5005
    70002       65.26       2012-10-05  3002         5001
    70004       110.5       2012-08-17  3009         5003
    70007       948.5       2012-09-10  3005         5002
    70005       2400.6      2012-07-27  3007         5001
    70008       5760        2012-09-10  3002         5001
    70010       1983.43     2012-10-10  3004         5006
    70003       2480.4      2012-10-10  3009         5003
    70012       250.45      2012-06-27  3008         5002
    70011       75.29       2012-08-17  3003         5007
    70013       3045.6      2012-04-25  3002         5001
    Sample table: customer
    
     customer_id |   cust_name    |    city    | grade | salesman_id 
    -------------+----------------+------------+-------+-------------
            3002 | Nick Rimando   | New York   |   100 |        5001
            3007 | Brad Davis     | New York   |   200 |        5001
            3005 | Graham Zusi    | California |   200 |        5002
            3008 | Julian Green   | London     |   300 |        5002
            3004 | Fabian Johnson | Paris      |   300 |        5006
            3009 | Geoff Cameron  | Berlin     |   100 |        5003
            3003 | Jozy Altidor   | Moscow     |   200 |        5007
            3001 | Brad Guzan     | London     |       |        5005
    Sample table : salesman
    
     salesman_id |    name    |   city   | commission 
    -------------+------------+----------+------------
            5001 | James Hoog | New York |       0.15
            5002 | Nail Knite | Paris    |       0.13
            5005 | Pit Alex   | London   |       0.11
            5006 | Mc Lyon    | Paris    |       0.14
            5007 | Paul Adam  | Rome     |       0.13
            5003 | Lauson Hen | San Jose |       0.12

```sql
SELECT 
    o.ord_no,
    o.purch_amt,
    o.ord_date,
    c.cust_name,
    c.city AS customer_city,
    c.grade,
    s.name AS salesman_name,
    s.city AS salesman_city,
    s.commission
FROM orders o
JOIN customer c
ON o.customer_id = c.customer_id
JOIN salesman s
ON o.salesman_id = s.salesman_id;
```

**Output:**

<img width="1389" height="713" alt="image" src="https://github.com/user-attachments/assets/744c6e91-58db-4d0e-94b5-c07fbd8d8148" />


**Question 6**
---
    Write an SQL query to retrieve all columns from the 'customer' table (aliased as 'c') using a LEFT JOIN with the 'orders' table on the 'customer_id' column, and filter the results to include only those orders placed between '2012-07-01' and '2012-07-30'.
    
    'customer' Table: (customer_id, cust_name, city, grade, salesman_id)
    
    'orders' Table: (ord_no, purch_amt, ord_date, customer_id, salesman_id)

```sql
SELECT c.*
FROM customer c
LEFT JOIN orders o
ON c.customer_id = o.customer_id
WHERE o.ord_date BETWEEN '2012-07-01' AND '2012-07-30';
```

**Output:**

<img width="1145" height="266" alt="image" src="https://github.com/user-attachments/assets/1097cb68-213c-4bdb-8bd4-6be1fe9258fe" />


**Question 7**
---
    Write the SQL query that achieves the selection of all columns from the "patients" table (aliased as "p"), with an inner join on the "patient_id" column and conditions filtering for test results with the test name 'X-Ray' and a result of 'Normal'.
    
    PATIENTS TABLE:
    
    ATTRIBUTES - patient_id, first_name, last_name, date_of_birth, admission_date, discharge_date, doctor_id

```sql
SELECT p.*
FROM patients p
INNER JOIN test_results t
ON p.patient_id = t.patient_id
WHERE t.test_name = 'X-Ray'
AND t.result = 'Normal';
```

**Output:**

<img width="1196" height="259" alt="image" src="https://github.com/user-attachments/assets/d1f883c8-2211-4d66-82c6-5535419cd109" />


**Question 8**
---
     From the following tables write a SQL query to find salespeople who received commissions of more than 12 percent from the company. Return Customer Name, customer city, Salesman, commission.  
    
    Sample table: customer
    
     customer_id |   cust_name    |    city    | grade | salesman_id 
    -------------+----------------+------------+-------+-------------
            3002 | Nick Rimando   | New York   |   100 |        5001
            3007 | Brad Davis     | New York   |   200 |        5001
            3005 | Graham Zusi    | California |   200 |        5002
            3008 | Julian Green   | London     |   300 |        5002
            3004 | Fabian Johnson | Paris      |   300 |        5006
            3009 | Geoff Cameron  | Berlin     |   100 |        5003
            3003 | Jozy Altidor   | Moscow     |   200 |        5007
            3001 | Brad Guzan     | London     |       |        5005
    Sample table: salesman
    
     salesman_id |    name    |   city   | commission 
    -------------+------------+----------+------------
            5001 | James Hoog | New York |       0.15
            5002 | Nail Knite | Paris    |       0.13
            5005 | Pit Alex   | London   |       0.11
            5006 | Mc Lyon    | Paris    |       0.14
            5007 | Paul Adam  | Rome     |       0.13
            5003 | Lauson Hen | San Jose |       0.12

```sql
SELECT 
    c.cust_name AS "Customer Name",
    c.city,
    s.name AS "Salesman",
    s.commission
FROM customer c
INNER JOIN salesman s
ON c.salesman_id = s.salesman_id
WHERE s.commission > 0.12;
```

**Output:**

<img width="850" height="458" alt="image" src="https://github.com/user-attachments/assets/c2c56f39-a316-4084-8887-90d7b0983598" />


**Question 9**
---
    Write the SQL query that achieves the selection of all columns from the "patients" table, with an inner join on the "doctor_id" column, and includes a condition filtering for patients whose doctors have the first name 'John' and last name 'Smith'.
    
    PATIENTS TABLE:
    name             type
    ---------------  ---------------
    patient_id       INT
    first_name       VARCHAR(50)
    last_name        VARCHAR(50)
    date_of_birth    DATE
    admission_date   DATE
    discharge_date   DATE
    doctor_id        INT
    
    DOCTORS TABLE:
    
    name             type
    ---------------  ---------------
    doctor_id        INT
    first_name       VARCHAR(50)
    last_name        VARCHAR(50)
    specialization   VARCHAR(100)

```sql
SELECT p.*
FROM patients p
INNER JOIN doctors d
ON p.doctor_id = d.doctor_id
WHERE d.first_name = 'John'
AND d.last_name = 'Smith';
```

**Output:**

<img width="1308" height="267" alt="image" src="https://github.com/user-attachments/assets/d70da572-9873-4b56-a2a7-2b03d1f8188d" />


**Question 10**
---
    SQL statement to generate a report with customer name, city, order number, order date, order amount, salesperson name, and commission to determine if any of the existing customers have not placed orders or if they have placed orders through their salesman or by themselves.
    
    Sample table: customer
    
     customer_id |   cust_name    |    city    | grade | salesman_id 
    -------------+----------------+------------+-------+-------------
            3002 | Nick Rimando   | New York   |   100 |        5001
            3007 | Brad Davis     | New York   |   200 |        5001
            3005 | Graham Zusi    | California |   200 |        5002
            3008 | Julian Green   | London     |   300 |        5002
            3004 | Fabian Johnson | Paris      |   300 |        5006
            3009 | Geoff Cameron  | Berlin     |   100 |        5003
            3003 | Jozy Altidor   | Moscow     |   200 |        5007
            3001 | Brad Guzan     | London     |       |        5005
    Sample table: orders
    
    ord_no      purch_amt   ord_date    customer_id  salesman_id
    ----------  ----------  ----------  -----------  -----------
    70001       150.5       2012-10-05  3005         5002
    70009       270.65      2012-09-10  3001         5005
    70002       65.26       2012-10-05  3002         5001
    70004       110.5       2012-08-17  3009         5003
    70007       948.5       2012-09-10  3005         5002
    70005       2400.6      2012-07-27  3007         5001
    70008       5760        2012-09-10  3002         5001
    70010       1983.43     2012-10-10  3004         5006
    70003       2480.4      2012-10-10  3009         5003
    70012       250.45      2012-06-27  3008         5002
    70011       75.29       2012-08-17  3003         5007
    70013       3045.6      2012-04-25  3002         5001
    Sample table: salesman
    
     salesman_id |    name    |   city   | commission 
    -------------+------------+----------+------------
            5001 | James Hoog | New York |       0.15
            5002 | Nail Knite | Paris    |       0.13
            5005 | Pit Alex   | London   |       0.11
            5006 | Mc Lyon    | Paris    |       0.14
            5007 | Paul Adam  | Rome     |       0.13
            5003 | Lauson Hen | San Jose |       0.12

```sql
SELECT 
c.cust_name,
c.city,
o.ord_no,
o.ord_date,
o.purch_amt AS "Order Amount",
s.name,
s.commission
FROM customer c
LEFT JOIN orders o
ON c.customer_id = o.customer_id
LEFT JOIN salesman s
ON c.salesman_id = s.salesman_id;
```

**Output:**

<img width="1199" height="695" alt="image" src="https://github.com/user-attachments/assets/f265df58-943e-4451-aca0-0b416624a88f" />



## RESULT
Thus, the SQL queries to implement different types of joins have been executed successfully.
