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
Insert all products from Discontinued_products into Products.

Table attributes are ProductID, ProductName, Price, Stock

```sql
insert into Products(ProductID, ProductName, Price, Stock)
SELECT  ProductID, ProductName, Price, Stock
from Discontinued_products
```

**Output:**

![image](https://github.com/user-attachments/assets/077f5368-6206-4b83-bb13-8cb417b54582)


**Question 2**
---
Insert the following products into the Products table:

Name        Category     Price       Stock
----------  -----------  ----------  ----------
Smartphone  Electronics  800         150
Headphones  Accessories  200         300

```sql
insert into Products(Name,Category,Price,Stock)values('Smartphone','Electronics',800,150),('Headphones','Accessories',200,300);
```

**Output:**

![image](https://github.com/user-attachments/assets/aaa68917-d460-46ed-b9f4-bfe5f1c7db54)


**Question 3**
---
Insert a product with ProductID 104, Name Tablet, and Category Electronics into the Products table, where Price and Stock should use default values.

```sql
insert into products(ProductID,Name,Category,Price,Stock)values(104,'Tablet','Electronics',100,50);
```

**Output:**

![image](https://github.com/user-attachments/assets/3f7626d3-00e9-45c3-a3ea-48c3e458796e)


**Question 4**
---
Create a new table named item with the following specifications and constraints:
item_id as TEXT and as primary key.
item_desc as TEXT.
rate as INTEGER.
icom_id as TEXT with a length of 4.
icom_id is a foreign key referencing com_id in the company table.
The foreign key should set NULL on updates and deletes.
item_desc and rate should not accept NULL.
```sql
create table item(
item_id TEXT primary key,
item_desc TEXT not null,
rate INTEGER not null,
icom_id TEXT(4),
foreign key(icom_id) references company(com_id)
on update set null
on delete set null
);
```

**Output:**

![image](https://github.com/user-attachments/assets/1cfa7ffc-bdab-431f-b3be-a2865aedc939)

**Question 5**
---
Create a table named Orders with the following columns:

OrderID as INTEGER
OrderDate as TEXT
CustomerID as INTEGER

```sql
create table Orders(
OrderID  INTEGER,
OrderDate  TEXT,
CustomerID  INTEGER
);
```

**Output:**

![image](https://github.com/user-attachments/assets/02dc5864-b408-4418-8b64-88573c9ce50a)


**Question 6**
---
Write a SQL query to Add a new column Mobilenumber as number in the Student_details table.

Sample table: Student_details

 cid              name             type             notnu  dflt_value  pk
---------------  ---------------  ---------------  -----  ----------  ----------
0                RollNo           int              0                  1
1                Name             VARCHAR(100)     1                  0
2                Gender           TEXT             1                  0
3                Subject          VARCHAR(30)      0                  0
4                MARKS            INT (3)          0                  0

```sql

ALTER TABLE Student_details
Add column Mobilenumber number;
```

**Output:**
![image](https://github.com/user-attachments/assets/9f305d8e-d92d-4179-a023-2cbb74ef4176)


**Question 7**
---
Create a table named Shipments with the following constraints:
ShipmentID as INTEGER should be the primary key.
ShipmentDate as DATE.
SupplierID as INTEGER should be a foreign key referencing Suppliers(SupplierID).
OrderID as INTEGER should be a foreign key referencing Orders(OrderID).

```sql
create table Shipments(
ShipmentID INTEGER  primary key,
ShipmentDate  DATE NOT NULL,
SupplierID  INTEGER NOT NULL,
OrderID  INTEGER NOT NULL,
foreign key(SupplierID) references Suppliers(SupplierID),
foreign key(OrderID) references Orders(OrderID)
);
```

**Output:**
![image](https://github.com/user-attachments/assets/e10172ad-a601-4ef0-b2ce-c0c0369b9c70)



**Question 8**
---
Create a table named Attendance with the following constraints:
AttendanceID as INTEGER should be the primary key.
EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
AttendanceDate as DATE.
Status as TEXT should be one of 'Present', 'Absent', 'Leave'.

```sql
create table Attendance(
AttendanceID INTEGER primary key,
EmployeeID  INTEGER NOT NULL ,
AttendanceDate  DATE,
Status  TEXT  CHECK (STATUS IN('Present', 'Absent', 'Leave')),
foreign key(EmployeeID) references Employees(EmployeeID)
);
```

**Output:**

![image](https://github.com/user-attachments/assets/55293e23-7a43-4038-812e-a7962a73dba0)


**Question 9**
---
Create a table named Tasks with the following columns:

TaskID as INTEGER
TaskName as TEXT
DueDate as DATE

```sql
create table tasks(
TaskID  INTEGER,
TaskName TEXT,
DueDate  DATE
);
```

**Output:**

![image](https://github.com/user-attachments/assets/191ef1cb-fb64-4897-b49c-12a4f359bb89)


**Question 10**
---
Insert the following customers into the Customers table:

CustomerID  Name         Address     City        ZipCode
----------  -----------  ----------  ----------  ----------
302         Laura Croft  456 Elm St  Seattle     98101
303         Bruce Wayne  789 Oak St  Gotham      10001

```sql
insert into Customers(CustomerID,Name,Address,City,ZipCode)values(302,'Laura Croft','456 Elm St','Seattle',98101),(303,'Bruce Wayne','789 Oak St','Gotham',10001);
```

**Output:**

![image](https://github.com/user-attachments/assets/5d86e342-50b1-42d8-894c-4c411ce19e20)


## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
