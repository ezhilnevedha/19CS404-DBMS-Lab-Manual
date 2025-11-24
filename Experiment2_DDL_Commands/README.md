# Experiment 2: DDL Commands
## NAME: EZHIL NEVEDHA K
## REG.NO: 212223230055
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
---
Create a table named Department with the following constraints: DepartmentID as INTEGER should be the primary key. DepartmentName as TEXT should be unique and not NULL. Location as TEXT.e

```sql
CREATE TABLE Department(
    DepartmentID INTEGER PRIMARY KEY,
    DepartmentName TEXT UNIQUE NOT NULL,
    Location TEXT
);
```

**Output:**

<img width="1197" height="353" alt="439246983-2e79062b-18c6-4eb1-b131-3ba4b0b8d6ad" src="https://github.com/user-attachments/assets/97287403-df81-46db-ad25-8cbfce81ba1b" />

<img width="1207" height="342" alt="439247121-39f61a82-5223-488c-b29e-736ad6e9d842" src="https://github.com/user-attachments/assets/1be7e1c9-1f9b-4a7a-80e7-382b52876557" />

**Question 2**
---
Create a table named Bonuses with the following constraints: BonusID as INTEGER should be the primary key. EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID). BonusAmount as REAL should be greater than 0. BonusDate as DATE. Reason as TEXT should not be NULL.

```sql
CREATE TABLE Bonuses(
BonusID INTEGER PRIMARY KEY,
EmployeeID INTEGER,
BonusAmount REAL CHECK(BonusAmount > 0),
BonusDate DATE,
Reason TEXT NOT NULL,
FOREIGN KEY (EmployeeID) REFERENCES Employees(EmployeeID)
);
```

**Output:**
<img width="1191" height="340" alt="439248381-b0bc3b60-cfcd-4251-b70a-cd06ac8d6025" src="https://github.com/user-attachments/assets/132ace2e-2f09-4706-b80a-045ec7d57281" />

<img width="1232" height="317" alt="439248737-98412e76-0695-4140-a23e-832e13cc2b78" src="https://github.com/user-attachments/assets/13b3aa67-6036-40a3-a0d0-dd54103fb3b4" />


**Question 3**
---
Create a table named Shipments with the following constraints: ShipmentID as INTEGER should be the primary key. ShipmentDate as DATE. SupplierID as INTEGER should be a foreign key referencing Suppliers(SupplierID). OrderID as INTEGER should be a foreign key referencing Orders(OrderID).

```sql
CREATE TABLE Shipments(
    ShipmentID INTEGER primary key,
    ShipmentDate DATE,
    SupplierID INTEGER,
    OrderID INTEGER,
    FOREIGN KEY (SupplierID) REFERENCES Suppliers(SupplierID),
    FOREIGN KEY (OrderID) REFERENCES Orders(OrderID)
);
```

**Output:**
<img width="996" height="300" alt="439249199-93844c33-4a75-42e1-9d47-1487e1a6cb34" src="https://github.com/user-attachments/assets/5d9ef9e6-4634-4752-9352-1520bd47c4ae" />

<img width="1127" height="378" alt="439249396-2ca9ac3f-c295-4d66-a41c-8e5f5b78d2ed" src="https://github.com/user-attachments/assets/72e19761-01f5-4a9a-b6c3-3f30ff69b2e0" />


**Question 4**
---
Write a SQL query to add a column named Date_of_birth as Date in the Student_details table.

```sql
ALTER TABLE Student_details
ADD COLUMN Date_of_birth Date;
```

**Output:**

<img width="1312" height="277" alt="439249875-127f7e23-23ca-4fdd-a568-8eed74f2777c" src="https://github.com/user-attachments/assets/ed8393f4-fec3-492d-a6e9-48141756f836" />


**Question 5**
--
Insert the following customers into the Customers table:

----------------------------------------
|CustomerID| Name| Address| City| ZipCode|
------------------------------------------
|302| Laura Croft| 456 Elm St| Seattle| 98101|                                     
|303| Bruce Wayne| 789 Oak St| Gotham |10001|
---------------------------------------------

```sql
INSERT INTO Customers(CustomerID,Name,Address,City,ZipCode)
VALUES(302,'Laura Croft','456 Elm St','Seattle',98101);
INSERT INTO Customers(CustomerID,Name,Address,City,ZipCode)
VALUES(303,'Bruce Wayne','789 Oak St','Gotham',10001);
```

**Output:**

<img width="1312" height="290" alt="439251084-a6c4dd6d-72c1-4473-9c81-3f451cd35ca8" src="https://github.com/user-attachments/assets/01f2a66f-d60a-44bb-9209-00a152787b2a" />


**Question 6**
---
Create a table named Employees with the following constraints:

EmployeeID should be the primary key. FirstName and LastName should be NOT NULL. Email should be unique. Salary should be greater than 0. DepartmentID should be a foreign key referencing the Departments table.

```sql
CREATE TABLE Employees(
EmployeeID INTEGER PRIMARY KEY,
FirstName NOT NULL,
LastName NOT NULL,
Email UNIQUE,
Salary CHECK (Salary > 0),
DepartmentID INTEGER,
FOREIGN KEY (DepartmentID) REFERENCES Departments(DepartmentID)
);
```

**Output:**

<img width="1316" height="316" alt="439251444-e2870930-a58f-4b65-86ec-9a3fd17f0da3" src="https://github.com/user-attachments/assets/0e971738-e9c7-430d-bbb8-84678df6b74f" />


**Question 7**
---
Create a table named Departments with the following columns:

DepartmentID as INTEGER DepartmentName as TEXT

```sql
CREATE TABLE Departments(
DepartmentID INTEGER,
DepartmentName TEXT
);
```

**Output:**
<img width="1316" height="272" alt="439251808-2528931c-9443-449d-8d64-ec183c65a23c" src="https://github.com/user-attachments/assets/82aa36a4-e971-44b0-9a04-058c0422a7f0" />



**Question 8**
---
Insert all customers from Old_customers into Customers

Table attributes are CustomerID, Name, Address, Email

```sql
INSERT INTO Customers(CustomerID, Name, Address, Email)
SELECT CustomerID, Name, Address, Email FROM Old_customers
```

**Output:**

<img width="1316" height="232" alt="439252428-b54c265c-03b1-4ebd-ba0d-c8e14a9a32f1" src="https://github.com/user-attachments/assets/c42d625a-42e4-4c64-8f75-438e57c2cf47" />


**Question 9**
---
Insert the below data into the Books table, allowing the Publisher and Year columns to take their default values.

ISBN Title Author

978-6655443321 Big Data Analytics Karen Adams

Note: The Publisher and Year columns will use their default values

```sql
INSERT INTO Books(ISBN, Title, Author) VALUES('978-6655443321','Big Data Analytics','Karen Adams');
```

**Output:**

<img width="1317" height="263" alt="439252754-9a5f18e9-45a3-42e5-a0d5-88523ede6c17" src="https://github.com/user-attachments/assets/045561be-6f0c-415c-9041-d259975a1a00" />


**Question 10**
---
Write a SQL query to Rename the "city" column to "location" in the "customer" table.

Sample table: customer

customer_id | cust_name | city | grade | salesman_id -------------+----------------+------------+-------+------------- 3002 | Nick Rimando | New York | 100 | 5001 3007 | Brad Davis | New York | 200 | 5001 3005 | Graham Zusi | California | 200 | 5002

```sql
ALTER TABLE customer
RENAME COLUMN city to location;
```

**Output:**

<img width="1368" height="196" alt="439253093-126ce3d8-d58a-45ca-a5db-e6ffb59bb108" src="https://github.com/user-attachments/assets/700143d6-0ae8-48ef-b294-aae68a0099cf" />



## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
