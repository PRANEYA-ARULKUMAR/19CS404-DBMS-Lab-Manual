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
--  Create a table named Employees with the following columns:

EmployeeID as INTEGER FirstName as TEXT LastName as TEXT HireDate as DATE

```
create table Employees(
EmployeeID INTEGER,
FirstName TEXT,
LastName TEXT,
HireDate DATE
);
```

**Output:**

<img width="1233" height="407" alt="image" src="https://github.com/user-attachments/assets/90f622f4-9c23-44fb-96e8-1a741c7e34fc" />


**Question 2**
---
-- Create a table named Orders with the following constraints: OrderID as INTEGER should be the primary key. OrderDate as DATE should be not NULL. CustomerID as INTEGER should be a foreign key referencing Customers(CustomerID).

```
create table Orders(
OrderID INTEGER PRIMARY KEY,
OrderDate DATE NOT NULL,
CustomerID INTEGER,
foreign key (CustomerID) references Customers(CustomerID)
);
```

**Output:**

<img width="1228" height="372" alt="image" src="https://github.com/user-attachments/assets/ca0313b5-93ea-44d9-a431-841e9958c8fd" />


**Question 3**
---
-- Insert all books from Out_of_print_books into Books

Table attributes are ISBN, Title, Author, Publisher, YearPublished

```
insert into Books(ISBN, Title, Author, Publisher, YearPublished) select 
ISBN, Title, Author, Publisher, YearPublished from out_of_print_books;
```

**Output:**

<img width="1229" height="374" alt="image" src="https://github.com/user-attachments/assets/18c9d19c-4186-47de-8dc8-18e532eba8f6" />


**Question 4**
---
-- Write an SQL query to add a new column email of type TEXT to the Student_details table, and ensure that this column cannot contain NULL values and make default value as 'Invalid'

```
alter table Student_details add column email TEXT NOT NULL DEFAULT 'Invalid';
```

**Output:**
<img width="1248" height="334" alt="image" src="https://github.com/user-attachments/assets/69e8584a-3d6c-43bc-b128-e3650f6ebdb3" />


**Question 5**
---
-- Create a table named Locations with the following columns:

LocationID as INTEGER LocationName as TEXT Address as TEXT

```
create table Locations(
LocationID INTEGER,
LocationName TEXT,
Address TEXT
);
```

**Output:**

<img width="1236" height="465" alt="image" src="https://github.com/user-attachments/assets/7f426140-8d1f-453c-9e75-c0991f6f4cfb" />


**Question 6**
---
--Insert the following customers into the Customers table:

CustomerID Name Address City ZipCode

```
insert into Customers(CustomerID,Name, Address, City, ZipCode)
values
(302, 'Laura Croft', '456 Elm St', 'Seattle',98101),
(303,'Bruce Wayne','789 Oak St','Gotham',10001);
```

**Output:**

<img width="1231" height="466" alt="image" src="https://github.com/user-attachments/assets/58ec86d1-e78b-4848-8265-5c3c0cb3c47a" />


**Question 7**
---
-- Create a table named Department with the following constraints: DepartmentID as INTEGER should be the primary key. DepartmentName as TEXT should be unique and not NULL. Location as TEXT.

```
create table Department (
DepartmentID INTEGER primary key,
DepartmentName TEXT NOT NULL UNIQUE,
Location TEXT
);
```

**Output:**

<img width="1235" height="367" alt="image" src="https://github.com/user-attachments/assets/1aeea865-558b-4409-a368-d15e2418dbe7" />


**Question 8**
---
-- Insert the below data into the Customers table, allowing the City and ZipCode columns to take their default values.

CustomerID Name Address

```
insert into Customers
(CustomerID,Name,Address)values
(304,'Peter Parker','Spider St');
```

**Output:**

<img width="1229" height="398" alt="image" src="https://github.com/user-attachments/assets/e8cfd3af-85bb-4b05-a990-44481a1b7dbf" />


**Question 9**
---
-- Create a new table named item with the following specifications and constraints: item_id as TEXT and as primary key. item_desc as TEXT. rate as INTEGER. icom_id as TEXT with a length of 4. icom_id is a foreign key referencing com_id in the company table. The foreign key should set NULL on updates and deletes. item_desc and rate should not accept NULL.

```
create table item(
item_id TEXT primary key,
item_desc TEXT NOT NULL,
rate INTEGER NOT NULL,
icom_id TEXT(4),
foreign key (icom_id) references company(com_id)
ON UPDATE SET NULL
ON DELETE SET NULL
);
```

**Output:**

<img width="1227" height="437" alt="image" src="https://github.com/user-attachments/assets/9b485128-7743-47c6-afbc-c34e5eea18af" />

**Question 10**
---
-- Write a SQL Query to add an attribute designation in the employee table with the data type VARCHAR(50).

```
--alter table employee add column designation varchar(50);
```

**Output:**

<img width="1229" height="376" alt="image" src="https://github.com/user-attachments/assets/d408fb54-0705-44d4-9353-67bf4a77b6ca" />

**RESULT:**
---

Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.


## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
