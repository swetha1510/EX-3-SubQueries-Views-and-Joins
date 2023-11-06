# EX 3 SubQueries, Views and Joins 
## DATE:
## Create employee Table
```sql
CREATE TABLE EMPY (EMPNO NUMBER(4) PRIMARY KEY,ENAME VARCHAR2(10),JOB VARCHAR2(9),MGR NUMBER(4),HIREDATE DATE,SAL NUMBER(7,2),COMM NUMBER(7,2),DEPTNO NUMBER(2));
```
## Insert the values
```sql
INSERT INTO EMPY (EMPNO, ENAME, JOB, MGR, HIREDATE, SAL, COMM, DEPTNO)
VALUES (7369, 'SMITH', 'CLERK', 7902, '17-DEC-80', 800, NULL, 20);

INSERT INTO EMPY (EMPNO, ENAME, JOB, MGR, HIREDATE, SAL, COMM, DEPTNO)
VALUES (7499, 'ALLEN', 'SALESMAN', 7698, '20-FEB-81', 1600, 300, 30);

INSERT INTO EMPY (EMPNO, ENAME, JOB, MGR, HIREDATE, SAL, COMM, DEPTNO)
VALUES (7521, 'WARD', 'SALESMAN', 7698, '22-FEB-81', 1250, 500, 30);

INSERT INTO EMPY (EMPNO, ENAME, JOB, MGR, HIREDATE, SAL, COMM, DEPTNO)
VALUES (7566, 'JONES', 'MANAGER', 7839, '02-APR-81', 2975, NULL, 20);

INSERT INTO EMPY (EMPNO, ENAME, JOB, MGR, HIREDATE, SAL, COMM, DEPTNO)
VALUES (7654, 'MARTIN', 'SALESMAN', 7698, '28-SEP-81', 1250, 1400, 30);

INSERT INTO EMPY (EMPNO, ENAME, JOB, MGR, HIREDATE, SAL, COMM, DEPTNO)
VALUES (7698, 'BLAKE', 'MANAGER', 7839, '01-MAY-81', 2850, NULL, 30);

INSERT INTO EMPY (EMPNO, ENAME, JOB, MGR, HIREDATE, SAL, COMM, DEPTNO)
VALUES (7782, 'CLARK', 'MANAGER', 7839, '09-JUN-81', 2450, NULL, 10);

INSERT INTO EMPY (EMPNO, ENAME, JOB, MGR, HIREDATE, SAL, COMM, DEPTNO)
VALUES (7788, 'SCOTT', 'ANALYST', 7566, '19-APR-87', 3000, NULL, 20);

INSERT INTO EMPY (EMPNO, ENAME, JOB, MGR, HIREDATE, SAL, COMM, DEPTNO)
VALUES (7839, 'KING', 'PRESIDENT', NULL, '17-NOV-81', 5000, NULL, 10);

INSERT INTO EMP (EMPNO, ENAME, JOB, MGR, HIREDATE, SAL, COMM, DEPTNO)
VALUES (7844, 'TURNER', 'SALESMAN', 7698, '08-SEP-81', 1500, 0, 30);

INSERT INTO EMPY (EMPNO, ENAME, JOB, MGR, HIREDATE, SAL, COMM, DEPTNO)
VALUES (7876, 'ADAMS', 'CLERK', 7788, '23-MAY-87', 1100, NULL, 20);

INSERT INTO EMPY (EMPNO, ENAME, JOB, MGR, HIREDATE, SAL, COMM, DEPTNO)
VALUES (7900, 'JAMES', 'CLERK', 7698, '03-DEC-81', 950, NULL, 30);

INSERT INTO EMPY (EMPNO, ENAME, JOB, MGR, HIREDATE, SAL, COMM, DEPTNO)
VALUES (7902, 'FORD', 'ANALYST', 7566, TO_DATE('03-DEC-81', 'DD-MON-RR'), 3000, 20, 20);

INSERT INTO EMPY (EMPNO, ENAME, JOB, MGR, HIREDATE, SAL, COMM, DEPTNO)
VALUES (7934, 'MILLER', 'CLERK', 7782, TO_DATE('23-JAN-82', 'DD-MON-RR'), 1300, 10, 10);
```

## Create department table
```sql
CREATE TABLE DEPT (DEPTNO NUMBER(2) PRIMARY KEY,DNAME VARCHAR2(14),LOC VARCHAR2(13));
```
## Insert the values in the department table
```sql
INSERT INTO DEPT (DEPTNO, DNAME, LOC) VALUES (10, 'ACCOUNTING', 'NEW YORK');

INSERT INTO DEPT (DEPTNO, DNAME, LOC) VALUES (20, 'RESEARCH', 'DALLAS');

INSERT INTO DEPT (DEPTNO, DNAME, LOC) VALUES (30, 'SALES', 'CHICAGO');

INSERT INTO DEPT (DEPTNO, DNAME, LOC) VALUES (40, 'OPERATIONS', 'BOSTON');
```

### Q1) List the name of the employees whose salary is greater than that of employee with empno 7566.
### QUERY:
```
select ENAME from EMPY where SAL>(select SAL from EMPY where EMPNO=7566);
```
### OUTPUT:
![Screenshot 2023-10-03 234148](https://github.com/swetha1510/EX-3-SubQueries-Views-and-Joins/assets/120623583/4f30abf0-0ebc-427a-b7d5-580fb2af8181)

### Q2) List the ename,job,sal of the employee who get minimum salary in the company.

### QUERY:
```
SELECT ename, job, sal FROM empy WHERE sal = (SELECT MIN(sal) FROM emp);
```
### OUTPUT:
![Screenshot 2023-10-03 234250](https://github.com/swetha1510/EX-3-SubQueries-Views-and-Joins/assets/120623583/ef285470-33ad-47c8-9846-44e302834385)

### Q3) List ename, job of the employees who work in deptno 10 and his/her job is any one of the job in the department ‘SALES’.

### QUERY:
```
SELECT e.ename, e.job FROM emp e, dept d WHERE e.deptno = 10 AND e.job IN (SELECT job FROM empy WHERE deptno = (SELECT deptno FROM dept WHERE dname = 'SALES'));
```
### OUTPUT:
![Screenshot 2023-10-03 234401](https://github.com/swetha1510/EX-3-SubQueries-Views-and-Joins/assets/120623583/93540217-c58c-4285-a5ae-7c3d4787331b)

### Q4) Create a view empv5 (for the table emp) that contains empno, ename, job of the employees who work in dept 10.

### QUERY:
```
CREATE VIEW empv5 AS SELECT empno, ename, job FROM empy WHERE deptno = 10;
```

### OUTPUT:
![Screenshot 2023-10-03 234432](https://github.com/swetha1510/EX-3-SubQueries-Views-and-Joins/assets/120623583/8995fc83-6106-4184-a7c0-b47f639a6018)

### Q5) Create a view with column aliases empv30 that contains empno, ename, sal of the employees who work in dept 30. Also display the contents of the view.

### QUERY:
```
CREATE VIEW empv30 AS SELECT empno, ename, sal FROM empy WHERE deptno = 30; SELECT * FROM empv30;
```

### OUTPUT:
![Screenshot 2023-10-03 234726](https://github.com/swetha1510/EX-3-SubQueries-Views-and-Joins/assets/120623583/1e9c6a5b-66d6-42ae-9bd0-ae7d56c97cbb)

### Q6) Update the view empv5 by increasing 10% salary of the employees who work as ‘CLERK’. Also confirm the modifications in emp table

### QUERY:
```
UPDATE empy SET sal = sal * 1.10 WHERE empno IN (SELECT empno FROM empv5 WHERE job = 'CLERK');
SELECT * FROM empy;
```
### OUTPUT:
![Screenshot 2023-10-03 234907](https://github.com/swetha1510/EX-3-SubQueries-Views-and-Joins/assets/120623583/4459b875-a4fc-4e2c-8e66-9eac01dd182f)
![Screenshot 2023-10-03 235101](https://github.com/swetha1510/EX-3-SubQueries-Views-and-Joins/assets/120623583/5d9c3a56-42e8-42ba-a756-42efd1ed6d14)


## Create a Customer1 Table
```sql
CREATE TABLE Customer1 (customer_id INT,cust_name VARCHAR(20),city VARCHAR(20),grade INT,salesman_id INT);
```
## Inserting Values to the Table
```sql
INSERT INTO Customer1 (customer_id, cust_name, city, grade, salesman_id) VALUES(3002, 'Nick Rimando', 'New York', 100, 5001);
INSERT INTO Customer1 (customer_id, cust_name, city, grade, salesman_id) VALUES(3007, 'Brad Davis', 'New York', 200, 5001);
INSERT INTO Customer1 (customer_id, cust_name, city, grade, salesman_id) VALUES(3005, 'Graham Zusi', 'California', 200, 5002);
INSERT INTO Customer1 (customer_id, cust_name, city, grade, salesman_id) VALUES(3008, 'Julian Green', 'London', 300, 5002);
INSERT INTO Customer1 (customer_id, cust_name, city, grade, salesman_id) VALUES(3004, 'Fabian Johnson', 'Paris', 300, 5006);
INSERT INTO Customer1 (customer_id, cust_name, city, grade, salesman_id) VALUES(3009, 'Geoff Cameron', 'Berlin', 100, 5003);
INSERT INTO Customer1 (customer_id, cust_name, city, grade, salesman_id) VALUES(3003, 'Jozy Altidor', 'Moscow', 200, 5007);
INSERT INTO Customer1 (customer_id, cust_name, city, grade, salesman_id) VALUES(3001, 'Brad Guzan', 'London', NULL, 5005);
```
## Create a Salesperson1 table
```sql
CREATE TABLE Salesman1 (salesman_id INT,name VARCHAR(20),city VARCHAR(20),commission DECIMAL(4,2));
```
## Inserting Values to the Table
```sql
INSERT INTO Salesman1 (salesman_id, name, city, commission) VALUES(5001, 'James Hoog', 'New York', 0.15);
INSERT INTO Salesman1 (salesman_id, name, city, commission) VALUES(5002, 'Nail Knite', 'Paris', 0.13);
INSERT INTO Salesman1 (salesman_id, name, city, commission) VALUES(5005, 'Pit Alex', 'London', 0.11);
INSERT INTO Salesman1 (salesman_id, name, city, commission) VALUES(5006, 'Mc Lyon', 'Paris', 0.14);
INSERT INTO Salesman1 (salesman_id, name, city, commission) VALUES(5007, 'Paul Adam', 'Rome', 0.13);
INSERT INTO Salesman1 (salesman_id, name, city, commission) VALUES(5003, 'Lauson Hen', 'San Jose', 0.12);
```
### Q7) Write a SQL query to find the salesperson and customer who reside in the same city. Return Salesman, cust_name and city.

### QUERY:
```
SELECT S.name AS Salesman, C.cust_name, C.city FROM Salesman1 S ,Customer1 C where S.city = C.city;
```
### OUTPUT:
![Screenshot 2023-10-03 235300](https://github.com/swetha1510/EX-3-SubQueries-Views-and-Joins/assets/120623583/f7974df2-5108-4de0-9bee-46edd59a9ed8)

### Q8) Write a SQL query to find salespeople who received commissions of more than 13 percent from the company. Return Customer Name, customer city, Salesman, commission.
### QUERY:
```
SELECT c.cust_name AS CustomerName, c.city AS CustomerCity, s.name AS Salesman, s.commission FROM Salesman1 s JOIN Customer1 c ON s.salesman_id = c.salesman_id WHERE s.commission > 0.13;
```
### OUTPUT:
![Screenshot 2023-10-03 235355](https://github.com/swetha1510/EX-3-SubQueries-Views-and-Joins/assets/120623583/56a276da-1164-4b1b-ade2-c89048e36f4e)

### Q9) Perform Natural join on both tables

### QUERY:
```
SELECT * FROM Salesman1 NATURAL JOIN Customer1;
```
### OUTPUT:
![Screenshot 2023-10-03 235432](https://github.com/swetha1510/EX-3-SubQueries-Views-and-Joins/assets/120623583/88943f74-1162-46e8-a2e9-b0ee32bc12d9)

### Q10) Perform Left and right join on both tables

### QUERY:
```
-- Left Join SELECT * FROM Customer1 LEFT JOIN Salesman1 ON Customer1.salesman_id = Salesman1.salesman_id;
```
### OUTPUT:
![Screenshot 2023-10-03 235553](https://github.com/swetha1510/EX-3-SubQueries-Views-and-Joins/assets/120623583/69ee9215-c031-427a-b445-8260a8997515)

### RESULT:
Thus the SubQueries, Views and Joins programs are used.
