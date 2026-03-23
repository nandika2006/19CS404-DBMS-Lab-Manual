# Experiment 4: Aggregate Functions, Group By and Having Clause

## AIM
To study and implement aggregate functions, GROUP BY, and HAVING clause with suitable examples.

## THEORY

### Aggregate Functions
These perform calculations on a set of values and return a single value.

- **MIN()** – Smallest value  
- **MAX()** – Largest value  
- **COUNT()** – Number of rows  
- **SUM()** – Total of values  
- **AVG()** – Average of values

**Syntax:**
```sql
SELECT AGG_FUNC(column_name) FROM table_name WHERE condition;
```
### GROUP BY
Groups records with the same values in specified columns.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name;
```
### HAVING
Filters the grouped records based on aggregate conditions.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name
HAVING condition;
```

**Question 1**
--
    How many appointments are scheduled for each patient?
    
    Sample table: Appointments Table
    
    name                  type
    --------------------  ----------
    AppointmentID         INTEGER
    PatientID             INTEGER
    DoctorID              INTEGER
    AppointmentDateTime   DATETIME
    Purpose               TEXT
    Status                TEXT

```sql
SELECT 
PatientID, 
COUNT(*) AS TotalAppointments
FROM Appointments
WHERE Status = 'Rescheduled'
GROUP BY PatientID;
```

**Output:**

<img width="705" height="612" alt="image" src="https://github.com/user-attachments/assets/140aee70-5c6a-4201-af03-10e6e2d16e8e" />


**Question 2**
---
    Write a SQL Query to find how many medications are prescribed for each patient?
    Sample table:MedicalRecords Table

```sql
SELECT 
PatientID,
COUNT(Medications) AS AvgMedications
FROM MedicalRecords
GROUP BY PatientID;
```

**Output:**

<img width="763" height="594" alt="image" src="https://github.com/user-attachments/assets/abcdb5b8-4a41-46d4-a622-d1bb5525d752" />


**Question 3**
---
How many medical records are there for each patient?

Sample table:MedicalRecords Table

```sql
SELECT PatientID,
COUNT(*) AS TotalRecords
FROM MedicalRecords
GROUP BY PatientID;
```

**Output:**

<img width="765" height="633" alt="image" src="https://github.com/user-attachments/assets/bef03e91-9cd3-46e6-b92f-d0981dc3c142" />


**Question 4**
---
Write a SQL query to find the shortest email address in the customer table?

Table: customer

name        type
----------  ----------
id          INTEGER
name        TEXT   
city        TEXT
email       TEXT
phone       INTEGER

```sql
SELECT name, email, LENGTH(email) AS min_email_length
FROM customer
ORDER BY min_email_length ASC
LIMIT 1;
```

**Output:**

<img width="930" height="345" alt="image" src="https://github.com/user-attachments/assets/d102b00e-83a8-4aa8-8ca1-e366920b8a48" />

**Question 5**
---
    Write a SQL query to find the total number of unique cities in the customer table?
    
    Table: customer
    
    name        type
    ----------  ----------
    id          INTEGER
    name        TEXT
    city        TEXT
    email       TEXT
    phone       INTEGER

```sql
SELECT COUNT(DISTINCT city) AS unique_cities
FROM customer;
```

**Output:**

<img width="526" height="347" alt="image" src="https://github.com/user-attachments/assets/0d5f1d90-37de-4482-9377-82e311c7d810" />


**Question 6**
---
    Write a SQL query to find the difference between the maximum and minimum price of fruits?
    
    Table: fruits
    
    name        type
    ----------  ----------
    id          INTEGER
    name        TEXT
    unit        TEXT
    inventory   INTEGER
    price       REAL

```sql
SELECT MAX(price) - MIN(price) AS price_diff
FROM fruits;
```

**Output:**

<img width="506" height="340" alt="image" src="https://github.com/user-attachments/assets/bc49284a-9947-4023-85bc-409bcf9d8f9e" />


**Question 7**
---
    Write a SQL query to find the minimum purchase amount.
    
    Sample table: orders
    
    ord_no      purch_amt   ord_date    customer_id  salesman_id
    
    ----------  ----------  ----------  -----------  -----------
    
    70001       150.5       2012-10-05  3005         5002
    
    70009       270.65      2012-09-10  3001         5005
    
    70002       65.26       2012-10-05  3002         5001

```sql
SELECT MIN(purch_amt) AS MINIMUM
FROM orders;
```

**Output:**

<img width="570" height="338" alt="image" src="https://github.com/user-attachments/assets/445090df-1a51-4695-83b6-9598a56bcb80" />


**Question 8**
---
    Write the SQL query to find how many patients have more than 3 medical records?.
    
    Sample table: MedicalRecords
    
    name        type
    ----------  ----------
    RecordID    INTEGER
    PatientID   INTEGER
    DoctorID    INTEGER
    Date        DATE
    Diagnosis   TEXT
    Treatment   TEXT
    Medication  TEXT

```sql
SELECT 
PatientID,
COUNT(*) AS TotalRecords
FROM MedicalRecords
GROUP BY PatientID
HAVING COUNT(*)>3;
```

**Output:**

<img width="739" height="371" alt="image" src="https://github.com/user-attachments/assets/dc2f4517-88f3-4c77-a258-39acae3e8a6a" />


**Question 9**
---
    Write the SQL query that achieves the grouping of data by occupation, calculates the total work hours for each occupation, and excludes occupations where the total work hour sum is not greater than 20.
    
    Sample table: employee1
    
```sql
-SELECT occupation, SUM(workhour) AS total_workhour
FROM employee1
GROUP BY occupation
HAVING SUM(workhour) > 20;
```

**Output:**

<img width="824" height="536" alt="image" src="https://github.com/user-attachments/assets/67510a8f-3039-4483-a3b1-b2d33700cbee" />


**Question 10**
---
    Write the SQL query that achieves the grouping of data by city, calculates the average income for each city, and includes only those cities where the average income is greater than 500,000.
    
    Sample table: employee

```sql
SELECT city, AVG(income)
FROM employee
GROUP BY city
HAVING AVG(income) > 500000;
```

**Output:**

<img width="633" height="449" alt="image" src="https://github.com/user-attachments/assets/ebe1effa-df9e-40c1-ba4b-2ceaa647d334" />



## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
