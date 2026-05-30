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
```
Write a SQL query to List departments with names longer than the average length Departments Table (attributes: department_id, department_name)
```
<img width="1222" height="205" alt="image" src="https://github.com/user-attachments/assets/dbcb2c7d-725f-4292-9dc7-be3d613acb5a" />


```
SELECT department_id, department_name
FROM Departments
WHERE LENGTH(department_name) > (
    SELECT AVG(LENGTH(department_name)) FROM Departments
);
```

**Output:**
<img width="961" height="533" alt="image" src="https://github.com/user-attachments/assets/a00bf2e3-de7c-41f4-9649-052ae0d1c978" />


**Question 2**
```
Write a SQL query to Retrieve the medications with dosages equal to the lowest dosage Table Name: Medications (attributes: medication_id, medication_name, dosage)
```
<img width="1202" height="314" alt="image" src="https://github.com/user-attachments/assets/1878581c-8f1a-4426-9d81-0cbe5ab7d6df" />


```
SELECT medication_id, medication_name, dosage
FROM Medications
WHERE dosage = (
    SELECT MIN(dosage)
    FROM Medications
);
```

**Output:**

<img width="1302" height="515" alt="image" src="https://github.com/user-attachments/assets/8eec2fb6-576d-4732-81a7-a39e33c42152" />


**Question 3**
```
Write a SQL query to Identify customers whose city is different from the city of the customer with the highest ID SAMPLE TABLE: customer
name             type
---------------  ---------------
id               INTEGER
name             TEXT
city             TEXT
email            TEXT
phone            INTEGER
```

```
SELECT *
FROM customer
WHERE city <> (
    SELECT city
    FROM customer
    WHERE id = (SELECT MAX(id) FROM customer)
);
```

**Output:**

<img width="1356" height="565" alt="image" src="https://github.com/user-attachments/assets/4bde6f9e-f0d4-4f5e-afc3-9ae1f636cf71" />


**Question 4**
```
 Write a SQL query to Retrieve the names of customers who have a phone number that is not shared with any other customer. SAMPLE TABLE: customer
name             type
---------------  ---------------
id               INTEGER
name             TEXT
city             TEXT
email            TEXT
phone            INTEGER
```

```
SELECT name
FROM customer
WHERE phone IN (
    SELECT phone
    FROM customer
    GROUP BY phone
    HAVING COUNT(*) = 1
);
```

**Output:**

<img width="826" height="629" alt="image" src="https://github.com/user-attachments/assets/ba5638fc-2af6-4cc6-9bfb-f12b7ff608bf" />


**Question 5**
```
Write a SQL query that retrieve all the columns from the table "Grades", where the grade is equal to the maximum grade achieved in each subject.

Sample table: GRADES (attributes: student_id, student_name, subject, grade)
```
<img width="963" height="383" alt="image" src="https://github.com/user-attachments/assets/e0642a85-0039-4683-93f0-12d70f097673" />



```
SELECT *
FROM Grades g
WHERE grade = (
    SELECT MAX(grade)
    FROM Grades
    WHERE subject = g.subject
);
```

**Output:**

<img width="1307" height="454" alt="image" src="https://github.com/user-attachments/assets/234ee222-25c3-4322-806a-9c87e1a56b68" />


**Question 6**
```
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose Address as Delhi

Sample table: CUSTOMERS

ID          NAME        AGE         ADDRESS     SALARY
----------  ----------  ----------  ----------  ----------

1          Ramesh     32              Ahmedabad     2000
2          Khilan        25              Delhi                 1500
3          Kaushik      23              Kota                  2000
4          Chaitali       25             Mumbai            6500
5          Hardik        27              Bhopal              8500
6          Komal         22              Hyderabad       4500

7           Muffy          24              Indore            10000
```

```
SELECT *
FROM CUSTOMERS
WHERE ADDRESS = 'Delhi';
```

**Output:**

<img width="1329" height="391" alt="image" src="https://github.com/user-attachments/assets/bd9fad96-e4f4-49d1-b944-dd7c48c98b58" />


**Question 7**
```
 Write a SQL query to Retrieve the names and cities of customers who have the same city as customers with IDs 3 and 7

SAMPLE TABLE: customer

name             type
---------------  ---------------
id               INTEGER
name             TEXT
city             TEXT
email            TEXT
phone            INTEGER
```

```
SELECT name, city
FROM customer
WHERE city IN (
    SELECT city
    FROM customer
    WHERE id IN (3, 7)
);
```

**Output:**

<img width="896" height="604" alt="image" src="https://github.com/user-attachments/assets/dd23e709-6806-42b5-8c83-391a78d5f970" />


**Question 8**
```
  Write a SQL query that retrieves the names of students and their corresponding grades, where the grade is equal to the maximum grade achieved in each subject. Sample table: GRADES
```
<img width="984" height="393" alt="image" src="https://github.com/user-attachments/assets/a5742804-89fb-40f5-816b-12cffedbe614" />


```
select student_name   ,  grade
from GRADES g
where grade =
(
     select max(grade)
     from GRADES
     where subject = g.subject
);
```

**Output:**

<img width="1125" height="556" alt="image" src="https://github.com/user-attachments/assets/bf82971b-b65e-44cb-be03-44b9f397e9e1" />


**Question 9**
```
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose salary is LESS than $2500.

Sample table: CUSTOMERS

ID          NAME        AGE         ADDRESS     SALARY
----------  ----------  ----------  ----------  ----------

1          Ramesh     32              Ahmedabad     2000
2          Khilan        25           Delhi         1500
3          Kaushik      23            Kota                  2000
4          Chaitali       25             Mumbai            6500
5          Hardik        27              Bhopal              8500
6          Komal         22              Hyderabad       4500

7           Muffy          24              Indore            10000
```

```
select *
from CUSTOMERS
where SALARY < 2500;
```

**Output:**

<img width="1315" height="464" alt="image" src="https://github.com/user-attachments/assets/691e8377-6649-46a3-8768-e3e294947de2" />


**Question 10**
```
From the following tables write a SQL query to find the order values greater than the average order value of 10th October 2012. Return ord_no, purch_amt, ord_date, customer_id, salesman_id.

Note: date should be yyyy-mm-dd format ORDERS TABLE

name            type
----------     ----------
ord_no          int
purch_amt    real
ord_date       text
customer_id  int
salesman_id  int
```

```
select * 
from ORDERS
where purch_amt >
(
     select purch_amt
     from ORDERS
     where ord_date = '2012-10-10'
);
```

**Output:**

<img width="1320" height="466" alt="image" src="https://github.com/user-attachments/assets/aca4cf25-f653-4bcd-850f-c472411d3f69" />



## RESULT
Thus, the SQL queries to implement subqueries and views have been executed successfully.
