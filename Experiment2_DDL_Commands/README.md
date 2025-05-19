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
Create a new table named item with the following specifications and constraints:
item_id as TEXT and as primary key.
item_desc as TEXT.
rate as INTEGER.
icom_id as TEXT with a length of 4.
icom_id is a foreign key referencing com_id in the company table.
The foreign key should cascade updates and deletes.
item_desc and rate should not accept NULL.
-- 

```sql
CREATE TABLE item (
    item_id TEXT PRIMARY KEY,
    item_desc TEXT NOT NULL,
    rate INTEGER NOT NULL,
    icom_id TEXT(4) CHECK (LENGTH(icom_id)=4),
    FOREIGN KEY (icom_id) REFERENCES company(com_id)
        ON UPDATE CASCADE
        ON DELETE CASCADE
    
);
```

**Output:**
![image](https://github.com/user-attachments/assets/1eebe62f-ecf1-4528-a32a-a5b17223a978)


**Question 2**
--
Create a table named Attendance with the following constraints:
AttendanceID as INTEGER should be the primary key.
EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
AttendanceDate as DATE.
Status as TEXT should be one of 'Present', 'Absent', 'Leave'.
-- 

```sql
CREATE TABLE Attendance(
    AttendanceID INTEGER PRIMARY KEY,
    EmployeeID INTEGER,
    AttendanceDate date,
    Status TEXT CHECK (Status IN ('Present','Absent','Leave')),
    FOREIGN KEY(EmployeeID) REFERENCES Employees(EmployeeID)
    
);
```

**Output:**

![image-1](https://github.com/user-attachments/assets/d3599df2-3b55-4029-9c3c-6e33b9da5279)


**Question 3**
--
Create a table named Bonuses with the following constraints:
BonusID as INTEGER should be the primary key.
EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
BonusAmount as REAL should be greater than 0.
BonusDate as DATE.
Reason as TEXT should not be NULL.
-- 

```sql
CREATE TABLE Bonuses(
    BonusID INTEGER PRIMARY KEY,
    EmployeeID INTEGER,
    BonusAmount REAL check(BonusAmount>0),
    BonusDate DATE,
    Reason TEXT NOT NULL,
    FOREIGN KEY (EmployeeID) REFERENCES  Employees(EmployeeID) 
);
```

**Output:**
![image-2](https://github.com/user-attachments/assets/0ee99bfa-47f2-462f-9f24-9ebcf8182835)


**Question 4**
--
Create a new table named item with the following specifications and constraints:
item_id as TEXT and as primary key.
item_desc as TEXT.
rate as INTEGER.
icom_id as TEXT with a length of 4.
icom_id is a foreign key referencing com_id in the company table.
The foreign key should set NULL on updates and deletes.
item_desc and rate should not accept NULL.
-- 

```sql
CREATE TABLE item (
    item_id TEXT PRIMARY KEY,
    item_desc TEXT NOT NULL,
    rate INTEGER NOT NULL,
    icom_id TEXT(4) CHECK (LENGTH(icom_id)=4),
    FOREIGN KEY (icom_id) REFERENCES company(com_id)
        ON UPDATE SET NULL
        ON DELETE SET NULL
        
);
```

**Output:**
![image-3](https://github.com/user-attachments/assets/32b027c7-33e4-4a75-8edb-3e8345bd2843)


**Question 5**
--
Create a table named Employees with the following columns:

EmployeeID as INTEGER
FirstName as TEXT
LastName as TEXT
HireDate as DATE
-- 

```sql
CREATE TABLE Employees (
    EmployeeID INTEGER,
    FirstName TEXT, 
    LastName TEXT,
    HireDate DATE
);
```

**Output:**

![image-4](https://github.com/user-attachments/assets/b982c15f-7cee-4b1a-a850-bd651473b56a)


**Question 6**
--
Insert all customers from Old_customers into Customers

Table attributes are CustomerID, Name, Address, Email
-- 

```sql
INSERT into Customers(CustomerID, Name, Address, Email) SELECT CustomerID, Name, Address, Email FROM Old_customers;
```

**Output:**
![image-5](https://github.com/user-attachments/assets/661313cb-0b82-4c18-8ff0-b9a00af5768e)


**Question 7**
--
Write a SQL Query  to change the name of attribute "name" to "first_name"  and add mobilenumber as number ,DOB as Date in the table Companies. 
-- 

```sql
ALTER table Companies rename column name TO first_name;
ALTER table Companies add column mobilenumber number;
ALTER table Companies add column DOB Date;

 
 
```

**Output:**

![image-6](https://github.com/user-attachments/assets/0ee51a67-9f6f-42ba-8a64-44b5c62c42f1)


**Question 8**
--
Create a table named Bonuses with the following constraints:
BonusID as INTEGER should be the primary key.
EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
BonusAmount as REAL should be greater than 0.
BonusDate as DATE.
Reason as TEXT should not be NULL.
-- 

```sql
CREATE TABLE Bonuses(
    BonusID INTEGER PRIMARY KEY,
    EmployeeID INTEGER,
    BonusAmount REAL check(BonusAmount>0),
    BonusDate DATE,
    Reason TEXT NOT NULL,
    FOREIGN KEY (EmployeeID) REFERENCES  Employees(EmployeeID) 
);
```

**Output:**
![image-7](https://github.com/user-attachments/assets/a33d1304-be44-4d45-bf98-839b26d64fe1)



**Question 9**
--
In the Student_details table, insert a student record where some fields are NULL, another record where all fields are filled without any NULL values, and a third record where some fields are filled, and others are left as NULL.
-- 

```sql
INSERT INTO student_details (RollNo,Name,Gender,Subject,MARKS) VALUES (205, 'Olivia Green','F',NULL,NULL);
INSERT INTO student_details (RollNo,Name,Gender,Subject,MARKS) VALUES (207 ,'Liam Smith','M','Mathematics',85); 
INSERT INTO student_details (RollNo,Name,Gender,Subject,MARKS) VALUES (208 ,'Sophia Johnson','F','Science',NULL);
 

```

**Output:**
![image-8](https://github.com/user-attachments/assets/da8cbcfc-edc6-4ca6-9bb6-23b31e177767)



**Question 10**
--
Insert a new product with ProductID 101, Name Laptop, Category Electronics, Price 1500, and Stock 50 into the Products table.
-- 

```sql
INSERT INTO Products (ProductID,Name,Category,Price,Stock) VALUES (101,'Laptop','Electronics',1500,50);
```

**Output:**
![image-9](https://github.com/user-attachments/assets/13e520bb-e454-4acf-8fb6-f230cf5d334d)



## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
