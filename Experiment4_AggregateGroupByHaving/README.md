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
What is the total number of appointments scheduled by each doctor?

Sample table:Appointments Table
<img width="998" height="163" alt="image" src="https://github.com/user-attachments/assets/b7c529f3-0ad8-4140-a0c8-de918de3c29c" />




For example:

Result
DoctorID    TotalAppointments
----------  -----------------
1           1
2           3
5           3
9           2
10          1

```sql
SELECT
    DoctorID,
    COUNT(*) AS TotalAppointments
FROM
    Appointments
GROUP BY
    DoctorID
ORDER BY
    DoctorID;
```

**Output:**
<img width="632" height="542" alt="Screenshot 2025-10-29 101544" src="https://github.com/user-attachments/assets/028c9b68-589b-4a54-ada5-b16926e9f6b6" />



**Question 2**
What is the average duration of insurance coverage for patients covered by each insurance company?

Sample table:Insurance Table

name               type
-----------------  ----------
InsuranceID        INTEGER
PatientID          INTEGER
InsuranceCompany   TEXT
PolicyNumber       TEXT
PolicyHolder       TEXT
StartDate          DATE
EndDate            DATE
For example:

Result
InsuranceCompany  AvgCoverageDurationDays
----------------  -----------------------
ABC Insurance     7.0
DEF Insurance     3.0
JKL Insurance     3.0
STU Insurance     3.0
VWX Insurance     3.0
XYZ Insurance     3.0
YZA Insurance     3.0

```sql
SELECT
    InsuranceCompany,
    ROUND(AVG((JULIANDAY(EndDate) - JULIANDAY(StartDate)) / 365.0), 1) AS AvgCoverageDurationDays
FROM
    Insurance
GROUP BY
    InsuranceCompany
ORDER BY
    InsuranceCompany;
```

**Output:**

<img width="727" height="567" alt="Screenshot 2025-10-29 101654" src="https://github.com/user-attachments/assets/533630f0-3cf2-4536-a079-cc12f09b055c" />


**Question 3**
What is the most common diagnosis among patients?

Sample table:MedicalRecords Table
<img width="1089" height="164" alt="image" src="https://github.com/user-attachments/assets/4ec7f7d1-77da-4d55-994d-ff8816645913" />

For example:

Result
Diagnosis              DiagnosisCount
---------------------  --------------
Childhood vaccination  3

```sql
SELECT
    Diagnosis,
    COUNT(*) AS DiagnosisCount
FROM
    MedicalRecords
GROUP BY
    Diagnosis
ORDER BY
    DiagnosisCount DESC
LIMIT 1;
```

**Output:**

<img width="686" height="279" alt="Screenshot 2025-10-29 101834" src="https://github.com/user-attachments/assets/c98adbe5-17e8-4ab6-881c-515b9f294355" />


**Question 4**
Write a SQL query to determine the number of customers who received at least one grade for their activity.

Sample table: customer

customer_id |   cust_name    |    city    | grade | salesman_id 

-------------+----------------+------------+-------+-------------

        3002 | Nick Rimando   | New York   |   100 |        5001

        3007 | Brad Davis     | New York   |   200 |        5001

        3005 | Graham Zusi    | California |   200 |        5002

 

For example:

Result
COUNT
----------
8


```sql
select count (grade) as COUNT
from customer;
```

**Output:**

<img width="326" height="295" alt="Screenshot 2025-10-29 101936" src="https://github.com/user-attachments/assets/4401889e-7eb9-48c8-a1f6-8116902c134a" />


**Question 5**
Write a SQL query to calculate the average purchase amount of all orders. Return average purchase amount.

Sample table: orders

ord_no      purch_amt   ord_date    customer_id  salesman_id

----------  ----------  ----------  -----------  -----------

70001       150.5       2012-10-05  3005         5002

70009       270.65      2012-09-10  3001         5005

70002       65.26       2012-10-05  3002         5001

 

For example:

Result
AVERAGE
----------
1461.765

```sql
select AVG (purch_amt) as AVERAGE
from orders
```

**Output:**
<img width="671" height="297" alt="Screenshot 2025-10-29 102139" src="https://github.com/user-attachments/assets/1a8fb81b-03fc-4896-908a-5dc5c6b836cf" />



**Question 6**
Write a SQL query to find the maximum purchase amount.

Sample table: orders

ord_no      purch_amt   ord_date    customer_id  salesman_id

----------  ----------  ----------  -----------  -----------

70001       150.5       2012-10-05  3005         5002

70009       270.65      2012-09-10  3001         5005

70002       65.26       2012-10-05  3002         5001

 

For example:

Result
MAXIMUM
----------
5760.0


```sql
select max(purch_amt)as MAXIMUM
from orders
```

**Output:**
<img width="715" height="297" alt="Screenshot 2025-10-29 102234" src="https://github.com/user-attachments/assets/2d469b71-07d2-43f1-b8b0-791bebcf5f51" />



**Question 7**
Write a SQL query to Calculate the average email length (in characters) for people who lives in Mumbai city

Table: customer

name        type
----------  ----------
id          INTEGER
name        TEXT   
city        TEXT
email       TEXT
phone       INTEGER
For example:

Result
avg_email_length_below_30
-------------------------
14.0

```sql
select avg(length(email))as avg_email_length_below_30
from customer
where city='Mumbai'
```

**Output:**
<img width="856" height="291" alt="Screenshot 2025-10-29 102320" src="https://github.com/user-attachments/assets/2afbef5f-ed59-4613-991c-00155d69780a" />



**Question 8**
Write the SQL query that accomplishes the grouping of data by joining date (jdate), calculates the minimum work hours for each date, and excludes dates where the minimum work hour is not less than 10.

Sample table: employee1
<img width="1031" height="203" alt="image" src="https://github.com/user-attachments/assets/107eb059-85f2-4b51-a43b-4c6ff092a0b3" />




For example:

Result
jdate       MIN(workhour)
----------  -------------
2002.0      9
2004.0      9
2006.0      9


```sql
SELECT
    jdate,
    MIN(workhour)
FROM
    employee1
GROUP BY
    jdate
HAVING
    MIN(workhour) < 10;
```

**Output:**

<img width="941" height="391" alt="image" src="https://github.com/user-attachments/assets/4361b331-a454-41a9-8d5d-e011179794a7" />


**Question 9**
Write the SQL query that accomplishes the grouping of data by age, calculates the total income for each age group, and includes only those age groups where the total income sum is greater than 1,000,000.

Sample table: employee
<img width="1011" height="215" alt="image" src="https://github.com/user-attachments/assets/06a4134b-0f41-46be-8d2b-790971081295" />




For example:

Result
age         SUM(income)
----------  -----------
35          10000000
40          1350000

```sql
select age,
SUM(income)
from employee
group by age
having SUM(income)>1000000
```

**Output:**
<img width="661" height="351" alt="Screenshot 2025-10-29 102643" src="https://github.com/user-attachments/assets/e8b14037-8842-40ff-9c3c-e192803548f1" />



**Question 10**
Write the SQL query that accomplishes the grouping of data by addresses, calculates the sum of salaries for each address, and excludes addresses where the total salary sum is not greater than 2000.

Sample table: customer1
<img width="992" height="173" alt="image" src="https://github.com/user-attachments/assets/9f5410dd-01d5-41ba-b151-562f39b42af3" />




For example:

Result
address     SUM(salary)
----------  -----------
Bhopal      8500
Hyderabad   4500
Indore      10000
Mumbai      6500

```sql
select address,
SUM(salary)
from customer1
group by address
having not SUM(salary)<=2000;
```

**Output:**
<img width="594" height="426" alt="Screenshot 2025-10-29 102806" src="https://github.com/user-attachments/assets/ef5fa699-fd8c-4604-bee2-cd724c4cb923" />





## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
