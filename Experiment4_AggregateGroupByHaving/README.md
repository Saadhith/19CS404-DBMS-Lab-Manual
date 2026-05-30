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
```
Write a SQL query to find the average salary of all employees?

Table: employee

name        type
----------  ----------
id          INTEGER
name        TEXT
age         INTEGER
city        TEXT
income      INTEGER
``` 

```
SELECT AVG(income) AS Average_Salary
FROM employee;
```

**Output:**

<img width="1296" height="354" alt="image" src="https://github.com/user-attachments/assets/4cd0a2b9-10b7-486b-b9a2-a1b5980d4d7b" />


**Question 2**
```
Write a SQL query to calculate the total number of working hours of all employees
```
<img width="1181" height="292" alt="image" src="https://github.com/user-attachments/assets/dca9c23d-57e1-46d7-92fe-38c3dac98432" />



```
SELECT SUM(workhour) AS 'Total working hours'
FROM  employee1;
```

**Output:**

<img width="1262" height="364" alt="image" src="https://github.com/user-attachments/assets/dd2b796d-1cb6-4d0f-b670-3749a5fe0cfa" />


**Question 3**
```
Write a SQL query to determine the number of customers who received at least one grade for their activity.

Sample table: customer

customer_id |   cust_name    |    city    | grade | salesman_id 

-------------+----------------+------------+-------+-------------

        3002 | Nick Rimando   | New York   |   100 |        5001

        3007 | Brad Davis     | New York   |   200 |        5001

        3005 | Graham Zusi    | California |   200 |        5002
```

```
SELECT COUNT(customer_id) AS COUNT
FROM customer
WHERE grade IS NOT NULL;
```

**Output:**

<img width="1284" height="358" alt="image" src="https://github.com/user-attachments/assets/c5463b79-ce6e-4ad1-bcc8-15362214b70e" />


**Question 4**
```
Write the SQL query that accomplishes the grouping of data by joining date (jdate), calculates the minimum work hours for each date, and excludes dates where the minimum work hour is not less than 10. Sample table: employee1
```

```
SELECT jdate,MIN(workhour) AS  'MIN(workhour)'
FROM employee1
GROUP BY jdate
HAVING MIN(workhour) < 10;
```

**Output:**

<img width="868" height="492" alt="image" src="https://github.com/user-attachments/assets/11450f6c-541f-4744-b7d5-9d7a4baca9bc" />


**Question 5**
```
Write the SQL query that accomplishes the grouping of data by age, calculates the maximum income for each age group, and includes only those age groups where the maximum income is greater than 2,000,000.
```
<img width="1077" height="271" alt="image" src="https://github.com/user-attachments/assets/35e96c89-df0f-4362-a906-89619373f5bf" />



```
SELECT age, MAX(income) AS 'MAX(income)'
FROM employee
GROUP BY age
HAVING MAX(income) > 2000000;
```

**Output:**

<img width="1271" height="427" alt="image" src="https://github.com/user-attachments/assets/8f457922-a3ca-4dfd-a918-e8f9758bda05" />


**Question 6**
```
Write the SQL query that accomplishes the selection of number of products for each category from products table which includes only those products where the category ID is greater than 2.
```
<img width="1071" height="315" alt="image" src="https://github.com/user-attachments/assets/014abe1c-c0b7-4b04-aa3f-6aae187a7820" />



```
SELECT category_id, COUNT(*) AS COUNT
FROM products
WHERE category_id > 2
GROUP BY category_id;
```

**Output:**

<img width="967" height="387" alt="image" src="https://github.com/user-attachments/assets/d2202bdb-1a21-4434-88a6-01364355fe28" />


**Question 7**
```
Write a SQL Query to find how many medications are prescribed for each patient?

Sample table:MedicalRecords Table
````

<img width="1323" height="179" alt="image" src="https://github.com/user-attachments/assets/02ff9315-2c58-40a4-9bf1-943ecc189507" />



```
SELECT PatientID,COUNT(medications) AS AvgMedications
FROM MedicalRecords
GROUP BY PatientID;
```

**Output:**

<img width="990" height="626" alt="image" src="https://github.com/user-attachments/assets/ce60f4ad-df38-416c-8b8f-9c9d088811e1" />


**Question 8**
```
How many prescriptions were written in each frequency category (e.g., once daily, twice daily)? Sample tablePrescriptions Table
```
<img width="1275" height="172" alt="image" src="https://github.com/user-attachments/assets/cae8010c-eff3-445f-a2cb-108149b399b7" />



```
SELECT Frequency,COUNT(Frequency) AS  TotalPrescriptions
FROM Prescriptions 
GROUP BY Frequency;
```

**Output:**

<img width="886" height="596" alt="image" src="https://github.com/user-attachments/assets/215c6c3d-49ec-4b75-aada-60181dd260ed" />


**Question 9**
```
What is the total number of appointments scheduled by each doctor?

Sample table:Appointments Table
```
<img width="1303" height="214" alt="image" src="https://github.com/user-attachments/assets/030327c3-24b1-452b-a1da-b9487f64580a" />


```
SELECT DoctorID,COUNT(*) AS TotalAppointments
FROM Appointments 
GROUP BY DoctorID;
```

**Output:**
<img width="1054" height="711" alt="image" src="https://github.com/user-attachments/assets/0e1fff76-978a-4b6e-b93a-09d35c5fb534" />


**Question 10**
```
 Write a SQL query to return the total number of rows in the 'customer' table where the city is Noida. Sample table:
```
<img width="1125" height="220" alt="image" src="https://github.com/user-attachments/assets/0f415664-9fc9-44e0-b716-9985993b72b3" />


```
select count(city)as COUNT
from customer
where city='Noida';
```

**Output:**

<img width="884" height="361" alt="image" src="https://github.com/user-attachments/assets/a00adb73-2c1e-4c46-97c6-886aa177df0b" />



## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
