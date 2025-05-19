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
<pre>
What is the total number of appointments scheduled for each day?

Table: Appointments

name                 type
-------------------  ----------
AppointmentID        INTEGER
PatientID            INTEGER
DoctorID             INTEGER
AppointmentDateTime  DATETIME
Purpose              TEXT
Status               TEXT
</pre>
-- 

```sql
SELECT
    DATE(AppointmentDateTime) AS
AppointmentDate,
    COUNT(*) AS TotalAppointments
FROM 
    Appointments
GROUP BY
    DATE(AppointmentDateTime)
ORDER BY
    AppointmentDate;
```

**Output:**

![image](https://github.com/user-attachments/assets/d5d2b1e1-8ae3-468c-94d9-a401da49f68d)


**Question 2**
--
<pre>
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
</pre>
-- 

```sql
SELECT
    PatientID,
    COUNT(*) AS TotalAppointments
FROM
    Appointments
GROUP BY
    PatientID
ORDER BY
    PatientID;
```

**Output:**

![image-1](https://github.com/user-attachments/assets/7ce7f910-694b-40a8-b5e1-65d65b1df33f)


**Question 3**
--
<pre>
Write a SQL query to Calculate the average email length (in characters) for people who lives in Mumbai city

Table: customer

name        type
----------  ----------
id          INTEGER
name        TEXT   
city        TEXT
email       TEXT
phone       INTEGER
</pre>
-- 

```sql
SELECT
    AVG(LENGTH(email)) AS
avg_email_length_below_30
FROM
    customer
WHERE
    city='Mumbai';
```

**Output:**

![image-2](https://github.com/user-attachments/assets/26ba26f3-d325-4612-92ff-3395d4507dbf)


**Question 4**
--

Write a SQL query to find What is the age difference between the youngest and oldest employee in the company.

Table: __employee__
<pre>
name        type
----------  ----------
id          INTEGER
name        TEXT
age         INTEGER
city        TEXT
income      INTEGER
</pre>
-- 

```sql
SELECT
    MAX(age) - MIN(age) AS age_difference
FROM employee;
```

**Output:**

![image-3](https://github.com/user-attachments/assets/494be162-38d8-44a2-83e2-c171f4c9f6ca)


**Question 5**
--
Write a SQL query to find the maximum purchase amount.

Sample table: orders
<pre>
ord_no      purch_amt   ord_date    customer_id  salesman_id

----------  ----------  ----------  -----------  -----------

70001       150.5       2012-10-05  3005         5002

70009       270.65      2012-09-10  3001         5005

70002       65.26       2012-10-05  3002         5001
</pre>
-- 

```sql
 SELECT 
    MAX(purch_amt) AS MAXIMUM
FROM orders;
```

**Output:**

![image-5](https://github.com/user-attachments/assets/74324e9a-82c4-41cb-95dc-1077e9463792)


**Question 6**
--
Write a SQL query to calculate total purchase amount of all orders. Return total purchase amount.

Sample table: orders
<pre>
ord_no      purch_amt   ord_date    customer_id  salesman_id

----------  ----------  ----------  -----------  -----------

70001       150.5       2012-10-05  3005         5002

70009       270.65      2012-09-10  3001         5005

70002       65.26       2012-10-05  3002         5001
</pre>
-- 

```sql
SELECT SUM(purch_amt) AS TOTAL
FROM orders;
```

**Output:**

![image-6](https://github.com/user-attachments/assets/bda83c8e-4bdc-411d-98e6-52342253a583)


**Question 7**
--
Write the SQL query that achieves the grouping of data by occupation, calculates the minimum work hours for each occupation, and excludes occupations where the minimum work hour is not greater than 8.

Sample table: employee1
![image-7](https://github.com/user-attachments/assets/c755deb3-7d85-4bec-a46f-86baa7f19ca5)


-- 

```sql
SELECT occupation,MIN(workhour) AS
"MIN(workhour)"
FROM employee1
GROUP BY occupation
HAVING MIN(workhour) > 8;
```

**Output:**
![image-8](https://github.com/user-attachments/assets/fd7c000a-cad6-4c9b-9352-9ee4fe9838e2)


**Question 8**
--
Write the SQL query that accomplishes the grouping of data by age intervals using the expression (age/5)5, calculates the minimum age for each group, and excludes groups where the minimum age is not less than 25.

Sample table: customer1
![image-9](https://github.com/user-attachments/assets/8da2afa0-1b42-482a-a214-56e8b45f4fe5)

-- 

```sql
SELECT (age/5)*5 AS age_group, MIN(age) AS "MIN(age)" FROM customer1 GROUP BY (age/5)*5 HAVING MIN(age) < 25 ORDER BY age_group;
```

**Output:**
![image-10](https://github.com/user-attachments/assets/1b674bfd-bef1-48a6-aea4-71f9272b6f17)



**Question 9**
--
Write the SQL query that accomplishes the grouping of data by addresses, calculates the sum of salaries for each address, and excludes addresses where the total salary sum is not greater than 2000.

Sample table: customer1
![image-11](https://github.com/user-attachments/assets/9f255494-e4a0-44ed-8881-fc171780ff6b)


-- 

```sql
SELECT address, SUM(salary) AS
"SUM(salary)"
FROM customer1
GROUP BY address
HAVING SUM(salary)>2000;
```

**Output:**
![image-12](https://github.com/user-attachments/assets/36531ae2-153c-4240-a1bb-7c608be2913c)



**Question 10**
--
How many patients have insurance coverage valid in each year?

Sample table:Insurance Table

<pre>
name               type
-----------------  ----------
InsuranceID        INTEGER
PatientID          INTEGER
InsuranceCompany   TEXT
PolicyNumber       TEXT
PolicyHolder       TEXT
ValidityPeriod     TEXT
-- 
</pre>

```sql
SELECT CAST(ValidityPeriod AS INTEGER) AS ValidityYear,
COUNT(DISTINCT PatientID) AS TotalPatients
FROM Insurance
GROUP BY ValidityYear
ORDER BY ValidityYear;
```

**Output:**

![image-13](https://github.com/user-attachments/assets/7294999c-7e7b-42db-b6d4-0b5a711abc44)


## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
