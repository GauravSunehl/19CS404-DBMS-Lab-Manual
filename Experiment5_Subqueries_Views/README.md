# Experiment 5: Subqueries and Views

## AIM
To study and implement subqueries and views.

## THEORY

### Subqueries
A subquery is a query inside another SQL query and is embedded in:
- WHERE clause
- HAVING clause
- FROM clause

**Types:**
- **Single-row subquery**:
  Sub queries can also return more than one value. Such results should be made use along with the operators in and any.
- **Multiple-row subquery**:
  Here more than one subquery is used. These multiple sub queries are combined by means of ‘and’ & ‘or’ keywords.
- **Correlated subquery**:
  A subquery is evaluated once for the entire parent statement whereas a correlated Sub query is evaluated once per row processed by the parent statement.

**Example:**
```sql
SELECT * FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees);
```
### Views
A view is a virtual table based on the result of an SQL SELECT query.
**Create View:**
```sql
CREATE VIEW view_name AS
SELECT column1, column2 FROM table_name WHERE condition;
```
**Drop View:**
```sql
DROP VIEW view_name;
```

**Question 1**
From the following tables, write a SQL query to determine the commission of the salespeople in Paris. Return commission.

salesman table

name             type
---------------  ---------------
salesman_id      numeric(5)
name                 varchar(30)
city                    varchar(15)
commission       decimal(5,2)

customer table

name         type
-----------  ----------
customer_id  int
cust_name    text
city         text
grade        int
salesman_id  int
For example:

Result
commission
----------
0.14



```sql
SELECT DISTINCT commission
FROM salesman
WHERE salesman_id IN (
    SELECT salesman_id
    FROM customer
    WHERE city = 'Paris'
);

```

**Output:**

<img width="438" height="421" alt="Screenshot 2025-11-05 101929" src="https://github.com/user-attachments/assets/f30f2fa3-c94c-4933-bc5c-4a0f6eb8be30" />


**Question 2**
Write a SQL query to Find employees who have an age less than the average age of employees with incomes over 2.5 Lakh

Employee Table

name             type

------------   ---------------

id                    INTEGER

name              TEXT

age                 INTEGER

city                 TEXT

income           INTEGER

For example:

Result
id     name             age              city             income
-----  ---------------  ---------------  ---------------  ----------
101    Peter            32               NewYork          200000
102    Mark             32               California       300000
103    Donald           25               Arizona          1000000
104    Obama            35               Florida          5000000
105    Linklon          32               Georgia          250000
107    Adam             35               California       5000000



```sql
SELECT id, name, age, city, income
FROM Employee
WHERE age < (
    SELECT AVG(age)
    FROM Employee
    WHERE income > 250000
);

```

**Output:**

<img width="1267" height="475" alt="Screenshot 2025-11-05 102024" src="https://github.com/user-attachments/assets/6c0f2f79-35c6-4bc6-8e56-8a7daa1a990f" />


**Question 3**
Write a SQL query to Retrieve the names of customers who have a phone number that is not shared with any other customer.

SAMPLE TABLE: customer

name             type
---------------  ---------------
id               INTEGER
name             TEXT
city             TEXT
email            TEXT
phone            INTEGER
For example:

Result
name
---------------
Aarti Desai
Vivek Sharma
Nisha Patel
Rajesh Singh
Radha Iyer

```sql
SELECT name
FROM customer
WHERE phone IN (
    SELECT phone
    FROM customer
    GROUP BY phone
    HAVING COUNT(phone) = 1
);

```

**Output:**

<img width="441" height="441" alt="image" src="https://github.com/user-attachments/assets/fb21d230-8b29-4387-a946-c9b2781e2ef2" />


**Question 4**
From the following tables write a SQL query to find salespeople who had more than one customer. Return salesman_id and name.

salesman table

name                 type
---------------   ---------------
salesman_id       numeric(5)
name                  varchar(30)
city                     varchar(15)
commission       decimal(5,2)

customer table

name              type
-----------       ----------
customer_id   int
cust_name     text
city                text
grade            int
salesman_id  int

For example:

Result
salesman_id  name
-----------  ----------
5001         James Hoog
5002         Nail Knite


```sql
SELECT salesman_id, name
FROM salesman
WHERE salesman_id IN (
    SELECT salesman_id
    FROM customer
    GROUP BY salesman_id
    HAVING COUNT(customer_id) > 1
);
```

**Output:**

<img width="488" height="438" alt="image" src="https://github.com/user-attachments/assets/96f8b18c-726d-45e1-a2f7-6273705c6ee6" />


**Question 5**
From the following tables write a SQL query to find the order values greater than the average order value of 10th October 2012. Return ord_no, purch_amt, ord_date, customer_id, salesman_id.

Note: date should be yyyy-mm-dd format

ORDERS TABLE

name            type
----------     ----------
ord_no          int
purch_amt    real
ord_date       text
customer_id  int
salesman_id  int

For example:

Result
ord_no      purch_amt   ord_date    customer_id  salesman_id
----------  ----------  ----------  -----------  -----------
70005       2400.6      2012-07-27  3007         5001
70008       5760.0      2012-09-10  3002         5001
70003       2480.4      2012-10-10  3009         5003
70013       3045.6      2012-04-25  3002         5001

```sql
SELECT ord_no, purch_amt, ord_date, customer_id, salesman_id
FROM orders
WHERE purch_amt > (
    SELECT AVG(purch_amt)
    FROM orders
    WHERE ord_date = '2012-10-10'
);

```

**Output:**

<img width="1084" height="432" alt="image" src="https://github.com/user-attachments/assets/9fe7baa2-20e4-4392-8a3c-9189991100b3" />


**Question 6**
Write a SQL query that retrieve all the columns from the table "Grades", where the grade is equal to the maximum grade achieved in each subject.

Sample table: GRADES (attributes: student_id, student_name, subject, grade)
<img width="602" height="233" alt="image" src="https://github.com/user-attachments/assets/422c8ae0-52ad-40c1-83b0-9500737546b2" />




For example:

Result
student_id       student_name     subject          grade
---------------  ---------------  ---------------  ---------------
3                Charlie          Math             95
5                Emma             Science          92
7                John             Social           85

```sql
SELECT *
FROM Grades g
WHERE grade = (
    SELECT MAX(grade)
    FROM Grades
    WHERE subject = g.subject
);
```

**Output:**
<img width="1164" height="419" alt="image" src="https://github.com/user-attachments/assets/b042a811-5e9d-4bee-907c-4f6a6004276f" />



**Question 7**
Write a SQL query to List departments with names longer than the average length

Departments Table (attributes: department_id, department_name)
<img width="866" height="134" alt="image" src="https://github.com/user-attachments/assets/0dfcd637-fd89-4807-ada7-0372742315ff" />




For example:

Result
depar  department_name
-----  ---------------
5      Anesthesiologis

```sql
SELECT department_id, department_name
FROM Departments
WHERE LENGTH(department_name) > (
    SELECT AVG(LENGTH(department_name))
    FROM Departments
);

```

**Output:**
<img width="523" height="381" alt="image" src="https://github.com/user-attachments/assets/15028320-dd5d-41cf-880a-8071e7e3b358" />




**Question 8**
Write a SQL query that retrieves the names of students and their corresponding grades, where the grade is equal to the minimum grade achieved in each subject.

Sample table: GRADES (attributes: student_id, student_name, subject, grade)
<img width="602" height="233" alt="image" src="https://github.com/user-attachments/assets/7d2186fb-6159-4448-a615-f3f2aec0213c" />




For example:

Result
student_name     grade
---------------  ---------------
Bob              85
Frank            85
John             85

```sql
SELECT student_name, grade
FROM Grades g
WHERE grade = (
    SELECT MIN(grade)
    FROM Grades
    WHERE subject = g.subject
);

```

**Output:**

<img width="646" height="424" alt="image" src="https://github.com/user-attachments/assets/51ebc13d-8c85-46c4-a0d4-3dbb07e1b00d" />


**Question 9**
From the following tables, write a SQL query to find all orders generated by the salespeople who may work for customers whose id is 3007. Return ord_no, purch_amt, ord_date, customer_id, salesman_id.

Table Name: orders

name             type
---------------  --------
order_no         int
purch_amt        real
order_date       text
customer_id      int
salesman_id      int
For example:

Result
ord_no      purch_amt   ord_date    customer_id  salesman_id
----------  ----------  ----------  -----------  -----------
70002       65.26       2012-10-05  3002         5001
70005       2400.6      2012-07-27  3007         5001
70008       5760.0      2012-09-10  3002         5001
70013       3045.6      2012-04-25  3002         5001


```sql
SELECT ord_no, purch_amt, ord_date, customer_id, salesman_id
FROM orders
WHERE salesman_id = (
    SELECT salesman_id
    FROM orders
    WHERE customer_id = 3007
);

```

**Output:**

<img width="1213" height="408" alt="image" src="https://github.com/user-attachments/assets/350ae59e-2ae2-45c5-998f-3a51495e5b7f" />


**Question 10**
Write a SQL query that retrieves the names of students and their corresponding grades, where the grade is equal to the maximum grade achieved in each subject.

Sample table: GRADES (attributes: student_id, student_name, subject, grade)
<img width="602" height="233" alt="image" src="https://github.com/user-attachments/assets/8c53fc15-daea-4d05-ac0c-d018067dafa4" />




For example:

Result
student_name     grade
---------------  ---------------
Charlie          95
Emma             92
John             85


```sql
SELECT student_name, grade
FROM Grades g
WHERE grade = (
    SELECT MAX(grade)
    FROM Grades
    WHERE subject = g.subject
);
```

**Output:**

<img width="716" height="419" alt="image" src="https://github.com/user-attachments/assets/cedd46ec-5f7b-44c4-b3de-9bf5a9bf194b" />



## RESULT
Thus, the SQL queries to implement subqueries and views have been executed successfully.
