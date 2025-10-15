Experiment 3: DML Commands

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
Write a SQL statement to Update the hire_date of employees in department 50 to 2024-01-24.

Employees table

---------------
employee_id
first_name
last_name
email
phone_number
hire_date
job_id
salary
commission_pct
manager_id
department_id
For example:

Test	Result
SELECT EMPLOYEE_ID, FIRST_NAME, HIRE_DATE FROM EMPLOYEES 
WHERE DEPARTMENT_ID=50 LIMIT 3;
EMPLOYEE_ID  FIRST_NAME  HIRE_DATE
-----------  ----------  ----------
120          Matthew     2024-01-24
121          Adam        2024-01-24
122          Payam       2024-01-24



```sql
UPDATE Employees
SET hire_date = '2024-01-24'
WHERE department_id = 50;
```

**Output:**
<img width="1198" height="412" alt="Screenshot 2025-10-15 104812" src="https://github.com/user-attachments/assets/03d6039b-f2dc-4ab4-a3b9-22ba0c14d8b3" />


**Question 2**
Increase the reorder level by 30% for products from 'Food' category having quantity in stock less than 50% of existing reorder level in the products table
name               type
--------------  ----------
product_id         INT
product_name       VARCHAR(10)
category           VARCHAR(50)
cost_price         DECIMAL(10)
sell_price         DECIMAL(10)
reorder_lvl        INT
quantity              INT
supplier_id           INT
For example:

Test	Result
select changes();
changes()
----------


```sql
UPDATE products
SET reorder_lvl = reorder_lvl * 1.3
WHERE category = 'Food'
  AND quantity < (reorder_lvl * 0.5);
```

**Output:**
<img width="1206" height="522" alt="Screenshot 2025-10-15 104948" src="https://github.com/user-attachments/assets/a2bfdca8-44f3-4797-aeec-ad9ce4c1cee0" />



**Question 3**
Write a SQL statement to Update the reorder level to 20 where the quantity in stock is less than 10 and product category is 'Snacks' in the products table.

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
SET reorder_lvl = 20
WHERE quantity < 10 AND category = 'Snacks';
```

**Output:**

<img width="1203" height="618" alt="Screenshot 2025-10-15 105052" src="https://github.com/user-attachments/assets/dddfe3c0-be69-4313-97b6-a79a7077f851" />



**Question 4**
Write a SQL statement to Update the product_name to 'Premium Bread' whose product ID is 5 in the products table.

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
SET product_name = 'Premium Bread'
WHERE product_id = 5;
```

**Output:**
<img width="1215" height="535" alt="Screenshot 2025-10-15 105155" src="https://github.com/user-attachments/assets/3eb581b2-16a3-4520-b8d9-e5d043920d53" />



**Question 5**
Write a SQL statement to update the product_name as 'Grapefruit' whose product_id is 4 in the products table.

products table

---------------
product_id
product_name
category_id
availability

```sql
UPDATE products
SET product_name = 'Grapefruit'
WHERE product_id = 4;
```

**Output:**
<img width="1200" height="349" alt="Screenshot 2025-10-15 105323" src="https://github.com/user-attachments/assets/e1957cd0-fc2c-4400-886c-8228627ba17f" />



**Question 6**
Write a SQL query to Delete customers from 'customer' table where 'GRADE' is less than 2.

 
Sample table: Customer

+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+  
|CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
| C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |
| C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |
| C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000.00 | BBBBSBB      | A008       |
For example:

Test	Result
select distinct(grade)from customer;
GRADE
----------
2
3
1
0
GRADE
----------
2
3


```sql
DELETE FROM customer
WHERE GRADE < 2;
```

**Output:**
<img width="1211" height="698" alt="Screenshot 2025-10-15 105428" src="https://github.com/user-attachments/assets/31a23652-4765-4ecb-8d37-17095bb540f2" />



**Question 7**
Write a SQL query to Delete All Doctors whose ID ranges from 2 to 4.

Sample table: Doctors

attributes : doctor_id, first_name, last_name, specialization
For example:

Test	Result
SELECT * FROM doctors;
doctor_id   first_name  last_name   specialization
----------  ----------  ----------  --------------
1           John        Smith       Cardiology
2           Emily       Johnson     Orthopedics
3           Michael     Brown       Pediatrics
doctor_id   first_name  last_name   specialization
----------  ----------  ----------  --------------
1           John        Smith       Cardiology


```sql
DELETE FROM Doctors
WHERE doctor_id BETWEEN 2 AND 4;
```

**Output:**
<img width="1252" height="805" alt="Screenshot 2025-10-15 105538" src="https://github.com/user-attachments/assets/17a1f094-9ee4-4d29-aafd-99ba05cda7e8" />



**Question 8**
Write a SQL query to Delete customers from 'customer' table where 'CUST_CITY' is not 'New York' and 'OUTSTANDING_AMT' is greater than 5000.

Sample table: Customer

+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+  
|CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
| C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |
| C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |
| C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000.00 | BBBBSBB      | A008       |
For example:

Test	Result
select changes();
changes()
----------
16

```sql
DELETE FROM customer
WHERE CUST_CITY <> 'New York' AND OUTSTANDING_AMT > 5000;
```

**Output:**
<img width="1306" height="483" alt="Screenshot 2025-10-15 105645" src="https://github.com/user-attachments/assets/606c516e-5009-4070-b11f-f20dc946e5e8" />

**Question 9**
Write a SQL query to Delete All Doctors with a NULL Specialization

Sample table: Doctors

attributes : doctor_id, first_name, last_name, specialization
For example:

Test	Result
SELECT * FROM doctors;
doctor_id   first_name  last_name   specialization
----------  ----------  ----------  --------------
1           John        Smith       Cardiology
2           Emily       Johnson     Orthopedics
3           Michael     Brown       Pediatrics
4           Febin       Jones
doctor_id   first_name  last_name   specialization
----------  ----------  ----------  --------------
1           John        Smith       Cardiology
2           Emily       Johnson     Orthopedics
3           Michael     Brown       Pediatrics


```sql
DELETE FROM Doctors
WHERE specialization IS NULL;
```

**Output:**
<img width="1295" height="803" alt="Screenshot 2025-10-15 105744" src="https://github.com/user-attachments/assets/bca6ed4d-2f32-4780-b891-5c84759e6e88" />



**Question 10**
Write a SQL query to Delete All Doctors with a NULL Last Name

Sample table: Doctors

attributes : doctor_id, first_name, last_name, specialization
For example:

Test	Result
SELECT * FROM doctors;
doctor_id   first_name  last_name   specialization
----------  ----------  ----------  --------------
1           John        Smith       Cardiology
2           Emily       Johnson     Orthopedics
3           Michael     Brown       Pediatrics
4           Febin                   Cardiology
doctor_id   first_name  last_name   specialization
----------  ----------  ----------  --------------
1           John        Smith       Cardiology
2           Emily       Johnson     Orthopedics
3           Michael     Brown       Pediatrics

```sql
DELETE FROM Doctors
WHERE last_name IS NULL;
```

**Output:**
<img width="1294" height="584" alt="Screenshot 2025-10-15 105835" src="https://github.com/user-attachments/assets/80d4ec0e-5e4e-41be-95c3-7c8dcb7a6111" />


## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.
