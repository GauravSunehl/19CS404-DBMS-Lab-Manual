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
Insert all employees from Former_employees into Employee

Table attributes are EmployeeID, Name, Department, Salary

For example:

Test	Result
select * from Employee;
EmployeeID  Name        Department  Salary
----------  ----------  ----------  ----------
201         John Doe    HR          50000
202         Jane Smith  Engineerin  75000
203         Emily Davi  Marketing   60000

```
INSERT INTO Employee
SELECT * FROM Former_employees;

```

**Output:**

<img width="1233" height="352" alt="Screenshot 2025-10-06 091852" src="https://github.com/user-attachments/assets/0e80e24c-1dfd-4f5a-85d6-2283f6029f68" />


**Question 2**
---
-- Write an SQL query to add two new columns, first_name and last_name, to the table employee. Both columns should have a data type of varchar(50).

For example:

Test	Result
pragma table_info('employee');
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           id          integer     0                       0
1           salary      number      0                       0
2           first_name  varchar(50  0                       0
3           last_name   varchar(50  0                       0


```sql
ALTER TABLE employee ADD COLUMN first_name varchar(50);
ALTER TABLE employee ADD COLUMN last_name varchar(50);
```

**Output:**

<img width="1222" height="391" alt="Screenshot 2025-10-06 092148" src="https://github.com/user-attachments/assets/84d2cfaa-9c3b-4e31-9c7d-855d925c7075" />


**Question 3**
---
Create a table named Members with the following columns:

MemberID as INTEGER
MemberName as TEXT
JoinDate as DATE
For example:

Test	Result
pragma table_info('Members');
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           MemberID    INTEGER     0                       0
1           MemberName  TEXT        0                       0
2           JoinDate    DATE        0                       0

```sql
CREATE TABLE Members (
    MemberID INTEGER,
    MemberName TEXT,
    JoinDate DATE
);
```

**Output:**

<img width="1224" height="434" alt="Screenshot 2025-10-06 092253" src="https://github.com/user-attachments/assets/607cab03-e919-4d6d-a7e5-91cb127b1e5f" />


**Question 4**
---
Create a table named Invoices with the following constraints:

InvoiceID as INTEGER should be the primary key.
InvoiceDate as DATE.
DueDate as DATE should be greater than the InvoiceDate.
Amount as REAL should be greater than 0.
For example:

Test	Result
INSERT INTO Invoices (InvoiceID, InvoiceDate)
VALUES (1, '2024-08-08'),(1,'2024-09-08');
Error: UNIQUE constraint failed: Invoices.InvoiceID


```sql
CREATE TABLE Invoices (
    InvoiceID INTEGER PRIMARY KEY,
    InvoiceDate DATE,
    DueDate DATE,
    Amount REAL CHECK (Amount > 0),
    CHECK (DueDate > InvoiceDate)
);
```

**Output:**

<img width="1230" height="362" alt="Screenshot 2025-10-06 092412" src="https://github.com/user-attachments/assets/dff7f8d4-073f-4817-95b7-80afa3506d2d" />


**Question 5**
---
Insert the below data into the Books table, allowing the Publisher and Year columns to take their default values.

ISBN             Title                 Author
---------------  --------------------  ---------------
978-6655443321   Big Data Analytics    Karen Adams

Note: The Publisher and Year columns will use their default values.
 
 
For example:

Test	Result
SELECT ISBN, Title, Author
FROM Books 


ISBN             Title                 Author
---------------  --------------------  ---------------
978-6655443321   Big Data Analytics    Karen Adams


```sql
INSERT INTO Books (ISBN, Title, Author)
VALUES ('978-6655443321', 'Big Data Analytics', 'Karen Adams');
```

**Output:**

<img width="1227" height="410" alt="Screenshot 2025-10-06 092515" src="https://github.com/user-attachments/assets/d2bd0238-9171-4cd8-90b1-7d644a2f5155" />


**Question 6**
---
Write a SQL Query  to Rename attribute "name" to "first_name"  and add mobilenumber as number ,DOB as Date,State as varchar(30) in the table Companies. 

For example:

Test	Result
pragma table_info('Companies');
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           id          int         0                       0
1           first_name  varchar(50  0                       0
2           address     text        0                       0
3           email       varchar(50  0                       0
4           phone       varchar(10  0                       0
5           mobilenumb  number      0                       0
6           DOB         Date        0                       0
7           State       varchar(30  0                       0


```sql
ALTER TABLE Companies RENAME COLUMN name TO first_name;

ALTER TABLE Companies ADD COLUMN mobilenumb number;
ALTER TABLE Companies ADD COLUMN DOB Date;
ALTER TABLE Companies ADD COLUMN State varchar(30);
```

**Output:**

<img width="1222" height="486" alt="Screenshot 2025-10-06 092614" src="https://github.com/user-attachments/assets/3f35f0d9-a9ae-47af-a49c-9c31bd0815bd" />


**Question 7**
---
In the Books table, insert a record where some fields are NULL, another record where all fields are filled without any NULL values, and a third record where some fields are filled, and others are left as NULL.

ISBN             Title                      Author           Publisher   Year
---------------  -------------------------  ---------------  ----------  ----------
978-1234567890   Introduction to AI         John Doe
978-9876543210   Deep Learning              Jane Doe         TechPress   2022
978-1122334455   Cybersecurity Essentials   Alice Smith                  2021
For example:

Test	Result
SELECT * FROM Books;
ISBN             Title                      Author           Publisher   Year
---------------  -------------------------  ---------------  ----------  ----------
978-1234567890   Introduction to AI         John Doe
978-9876543210   Deep Learning              Jane Doe         TechPress   2022
978-1122334455   Cybersecurity Essentials   Alice Smith                  2021

```sql
INSERT INTO Books (ISBN, Title, Author)
VALUES ('978-1234567890', 'Introduction to AI', 'John Doe');

INSERT INTO Books (ISBN, Title, Author, Publisher, Year)
VALUES ('978-9876543210', 'Deep Learning', 'Jane Doe', 'TechPress', 2022);

INSERT INTO Books (ISBN, Title, Author, Publisher, Year)
VALUES ('978-1122334455', 'Cybersecurity Essentials', 'Alice Smith', NULL, 2021);
```

**Output:**

<img width="1227" height="364" alt="Screenshot 2025-10-06 092713" src="https://github.com/user-attachments/assets/f8c7f01c-c50c-492a-8328-ace38e7007e7" />



**Question 8**
---
Create a new table named item with the following specifications and constraints:
item_id as TEXT and as primary key.
item_desc as TEXT.
rate as INTEGER.
icom_id as TEXT with a length of 4.
icom_id is a foreign key referencing com_id in the company table.
The foreign key should set NULL on updates and deletes.
item_desc and rate should not accept NULL.
For example:

Test	Result
INSERT INTO item VALUES("ITM5","Charlie Gold",700,"COM4");
UPDATE company SET com_id='COM5' WHERE com_id='COM4';
SELECT * FROM item;
item_id     item_desc     rate        icom_id
----------  ------------  ----------  ----------
ITM5        Charlie Gold  700

```sql
CREATE TABLE item (
    item_id TEXT PRIMARY KEY,
    item_desc TEXT NOT NULL,
    rate INTEGER NOT NULL,
    icom_id TEXT CHECK(length(icom_id) = 4),
    FOREIGN KEY(icom_id) REFERENCES company(com_id) 
        ON UPDATE SET NULL 
        ON DELETE SET NULL
);
```

**Output:**

<img width="1227" height="428" alt="Screenshot 2025-10-06 092826" src="https://github.com/user-attachments/assets/d98bb24c-7c5e-4a99-a9a0-af0ced73357b" />


**Question 9**
---
Create a new table named products with the following specifications:
product_id as INTEGER and primary key.
product_name as TEXT and not NULL.
list_price as DECIMAL (10, 2) and not NULL.
discount as DECIMAL (10, 2) with a default value of 0 and not NULL.
A CHECK constraint at the table level to ensure:
list_price is greater than or equal to discount
discount is greater than or equal to 0
list_price is greater than or equal to 0
For example:

Test	Result
INSERT INTO products (product_id, product_name, list_price) VALUES (2, 'Product B', 50.00);
SELECT * FROM products;
product_id  product_name  list_price  discount
----------  ------------  ----------  ----------
2           Product B     50          0


```sql
CREATE TABLE products (
    product_id INTEGER PRIMARY KEY,
    product_name TEXT NOT NULL,
    list_price DECIMAL(10, 2) NOT NULL,
    discount DECIMAL(10, 2) NOT NULL DEFAULT 0,
    CHECK (list_price >= discount AND discount >= 0)
);
```

**Output:**

<img width="1233" height="361" alt="Screenshot 2025-10-06 092943" src="https://github.com/user-attachments/assets/6208895a-88d8-4fa7-8c55-c24b0489806d" />


**Question 10**
---
Create a new table named item with the following specifications and constraints:
item_id as TEXT and as primary key.
item_desc as TEXT.
rate as INTEGER.
icom_id as TEXT with a length of 4.
icom_id is a foreign key referencing com_id in the company table.
The foreign key should cascade updates and deletes.
item_desc and rate should not accept NULL.
For example:

Test	Result
INSERT INTO item VALUES("ITM5","Charlie Gold",700,"COM4");
UPDATE company SET com_id='COM5' WHERE com_id='COM4';
SELECT * FROM item;
item_id     item_desc     rate        icom_id
----------  ------------  ----------  ----------
ITM5        Charlie Gold  700         COM5


```sql
CREATE TABLE item (
    item_id TEXT PRIMARY KEY,
    item_desc TEXT NOT NULL,
    rate INTEGER NOT NULL,
    icom_id TEXT CHECK(length(icom_id) = 4),
    FOREIGN KEY(icom_id) REFERENCES company(com_id) 
        ON UPDATE CASCADE 
        ON DELETE CASCADE
);
```

**Output:**

<img width="1240" height="434" alt="Screenshot 2025-10-06 093047" src="https://github.com/user-attachments/assets/230166a8-71d1-4187-9860-be024f896049" />



## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
