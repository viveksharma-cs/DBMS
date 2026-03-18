# DBMS Lab - Practical 1 (DDL & DML Operations)

---

## Database & Table Setup

### Step 1: Create Database

```sql
CREATE DATABASE company;
```

**Output:**
```
MariaDB [(none)]> create database company;
Query OK, 1 row affected (0.005 sec)
```

---

### Step 2: Use Database & Create Department Table

```sql
USE company;

CREATE TABLE department(
    deptno INT(2) PRIMARY KEY,
    dname VARCHAR(15) NOT NULL
);
```

**Output:**
```
MariaDB [(none)]> use company;
Database changed

MariaDB [company]> create table department(
    -> deptno INT(2) PRIMARY KEY,
    -> dname varchar(15) not null);
Query OK, 0 rows affected (0.024 sec)

MariaDB [company]> desc department;
+--------+-------------+------+-----+---------+-------+
| Field  | Type        | Null | Key | Default | Extra |
+--------+-------------+------+-----+---------+-------+
| deptno | int(2)      | NO   | PRI | NULL    |       |
| dname  | varchar(15) | NO   |     | NULL    |       |
+--------+-------------+------+-----+---------+-------+
2 rows in set (0.008 sec)
```

---

### Step 3: Create Employee Table

```sql
CREATE TABLE employee(
    EMPNO INT(4) PRIMARY KEY,
    ENAME VARCHAR(20) NOT NULL,
    JOB VARCHAR(20),
    MGR INT(4),
    HIREDATE DATE,
    SAL INT(10),
    COMM INT(7),
    DEPTNO INT(2),
    FOREIGN KEY (DEPTNO) REFERENCES DEPARTMENT(DEPTNO)
);
```

**Output:**
```
MariaDB [company]> create table employee(
    -> EMPNO INT(4) primary key,
    -> ENAME VARCHAR(20) NOT NULL,
    -> JOB VARCHAR(20),
    -> MGR INT(4),
    -> HIREDATE DATE,
    -> SAL INT(10),
    -> COMM INT(7),
    -> DEPTNO INT(2),
    -> FOREIGN KEY (DEPTNO) REFERENCES DEPARTMENT(DEPTNO));
Query OK, 0 rows affected (0.071 sec)

MariaDB [company]> DESC EMPLOYEE;
+----------+-------------+------+-----+---------+-------+
| Field    | Type        | Null | Key | Default | Extra |
+----------+-------------+------+-----+---------+-------+
| EMPNO    | int(4)      | NO   | PRI | NULL    |       |
| ENAME    | varchar(20) | NO   |     | NULL    |       |
| JOB      | varchar(20) | YES  |     | NULL    |       |
| MGR      | int(4)      | YES  |     | NULL    |       |
| HIREDATE | date        | YES  |     | NULL    |       |
| SAL      | int(10)     | YES  |     | NULL    |       |
| COMM     | int(7)      | YES  | MUL | NULL    |       |
| DEPTNO   | int(2)      | YES  |     | NULL    |       |
+----------+-------------+------+-----+---------+-------+
8 rows in set (0.046 sec)
```

---

### Step 4: Insert Data into Department Table

```sql
INSERT INTO DEPARTMENT VALUES (10,'RESEARCH'),(20,'ACCOUNTING'),(30,'SALES'),(40,'OPERATIONS');
```

**Output:**
```
MariaDB [company]> INSERT INTO DEPARTMENT VALUES (10,"RESEARCH"),(20,"ACCOUNTING"),(30,"SALES"),(40,"OPERATIONS");
Query OK, 4 rows affected (0.004 sec)
Records: 4  Duplicates: 0  Warnings: 0

MariaDB [company]> SELECT * FROM DEPARTMENT;
+--------+------------+
| deptno | dname      |
+--------+------------+
|     10 | RESEARCH   |
|     20 | ACCOUNTING |
|     30 | SALES      |
|     40 | OPERATIONS |
+--------+------------+
4 rows in set (0.002 sec)
```

---

### Step 5: Insert Data into Employee Table

```sql
INSERT INTO EMPLOYEE VALUES
(7369,'SMITH','CLERK',7902,'1980-12-17',800,NULL,20),
(7499,'ALLEN','SALESMAN',7698,'1981-02-20',1600,300,30),
(7521,'WARD','SALESMAN',7698,'1981-02-22',1250,300,30),
(7566,'JONES','MANAGER',7839,'1981-04-02',2975,NULL,20),
(7654,'MARTIN','SALESMAN',7698,'1981-09-28',1250,1400,30),
(7698,'BLAKE','MANAGER',7839,'1981-05-01',2850,NULL,30),
(7782,'CLARK','MANAGER',7839,'1981-06-09',2450,NULL,20),
(7788,'SCOTT','ANALYST',7566,'1982-12-09',3000,NULL,40),
(7839,'KING','PRESIDENT',NULL,'1981-11-17',5000,NULL,20),
(7844,'TURNER','SALESMAN',7698,'1981-09-08',1500,0,30),
(7876,'ADAMS','CLERK',7788,'1983-01-12',1100,NULL,20),
(7900,'JAMES','CLERK',7698,'1981-12-03',950,NULL,30),
(7902,'FORD','ANALYST',7566,'1981-12-03',3000,NULL,20);
```

**Output:**
```
MariaDB [company]> INSERT INTO EMPLOYEE VALUES
    -> (7369,'SMITH','CLERK',7902,'1980-12-17',800,NULL,20),
    -> (7499,'ALLEN','SALESMAN',7698,'1981-02-20',1600,300,30),
    -> (7521,'WARD','SALESMAN',7698,'1981-02-22',1250,300,30),
    -> (7566,'JONES','MANAGER',7839,'1981-04-02',2975,NULL,20),
    -> (7654,'MARTIN','SALESMAN',7698,'1981-09-28',1250,1400,30),
    -> (7698,'BLAKE','MANAGER',7839,'1981-05-01',2850,NULL,30),
    -> (7782,'CLARK','MANAGER',7839,'1981-06-09',2450,NULL,20),
    -> (7788,'SCOTT','ANALYST',7566,'1982-12-09',3000,NULL,40),
    -> (7839,'KING','PRESIDENT',NULL,'1981-11-17',5000,NULL,20),
    -> (7844,'TURNER','SALESMAN',7698,'1981-09-08',1500,0,30),
    -> (7876,'ADAMS','CLERK',7788,'1983-01-12',1100,NULL,20),
    -> (7900,'JAMES','CLERK',7698,'1981-12-03',950,NULL,30),
    -> (7902,'FORD','ANALYST',7566,'1981-12-03',3000,NULL,20);
Query OK, 13 rows affected (0.008 sec)
Records: 13  Duplicates: 0  Warnings: 0
```

---

### Step 6: Insert Last Record (MILLER) & View Full Employee Table

```sql
INSERT INTO EMPLOYEE VALUES (7934,'MILLER','CLERK',7782,'1982-01-23',1300,NULL,10);
```

**Output:**
```
MariaDB [company]> INSERT INTO EMPLOYEE VALUES (7934,'MILLER','CLERK',7782,'1982-01-23',1300,NULL,10);
Query OK, 1 row affected (0.005 sec)

MariaDB [company]> SELECT * FROM EMPLOYEE;
+-------+--------+-----------+------+------------+------+------+--------+
| EMPNO | ENAME  | JOB       | MGR  | HIREDATE   | SAL  | COMM | DEPTNO |
+-------+--------+-----------+------+------------+------+------+--------+
|  7369 | SMITH  | CLERK     | 7902 | 1980-12-17 |  800 | NULL |     20 |
|  7499 | ALLEN  | SALESMAN  | 7698 | 1981-02-20 | 1600 |  300 |     30 |
|  7521 | WARD   | SALESMAN  | 7698 | 1981-02-22 | 1250 |  300 |     30 |
|  7566 | JONES  | MANAGER   | 7839 | 1981-04-02 | 2975 | NULL |     20 |
|  7654 | MARTIN | SALESMAN  | 7698 | 1981-09-28 | 1250 | 1400 |     30 |
|  7698 | BLAKE  | MANAGER   | 7839 | 1981-05-01 | 2850 | NULL |     30 |
|  7782 | CLARK  | MANAGER   | 7839 | 1981-06-09 | 2450 | NULL |     20 |
|  7788 | SCOTT  | ANALYST   | 7566 | 1982-12-09 | 3000 | NULL |     40 |
|  7839 | KING   | PRESIDENT | NULL | 1981-11-17 | 5000 | NULL |     20 |
|  7844 | TURNER | SALESMAN  | 7698 | 1981-09-08 | 1500 |    0 |     30 |
|  7876 | ADAMS  | CLERK     | 7788 | 1983-01-12 | 1100 | NULL |     20 |
|  7900 | JAMES  | CLERK     | 7698 | 1981-12-03 |  950 | NULL |     30 |
|  7902 | FORD   | ANALYST   | 7566 | 1981-12-03 | 3000 | NULL |     20 |
|  7934 | MILLER | CLERK     | 7782 | 1982-01-23 | 1300 | NULL |     10 |
+-------+--------+-----------+------+------------+------+------+--------+
14 rows in set (0.001 sec)
```

---
---

## Questions

---

## 1. Create Employee_master table with data using Employee table.

```sql
CREATE TABLE EMPLOYEE_MASTER AS SELECT * FROM EMPLOYEE;
```

**Output:**
```
MariaDB [company]> CREATE TABLE EMPLOYEE_MASTER AS SELECT * FROM EMPLOYEE;
Query OK, 14 rows affected (0.035 sec)
Records: 14  Duplicates: 0  Warnings: 0

MariaDB [company]> DESC EMPLOYEE_MASTER;
+----------+-------------+------+-----+---------+-------+
| Field    | Type        | Null | Key | Default | Extra |
+----------+-------------+------+-----+---------+-------+
| EMPNO    | int(4)      | NO   |     | NULL    |       |
| ENAME    | varchar(20) | NO   |     | NULL    |       |
| JOB      | varchar(20) | YES  |     | NULL    |       |
| MGR      | int(4)      | YES  |     | NULL    |       |
| HIREDATE | date        | YES  |     | NULL    |       |
| SAL      | int(10)     | YES  |     | NULL    |       |
| COMM     | int(7)      | YES  |     | NULL    |       |
| DEPTNO   | int(2)      | YES  |     | NULL    |       |
+----------+-------------+------+-----+---------+-------+
8 rows in set (0.005 sec)

MariaDB [company]> SELECT * FROM EMPLOYEE_MASTER;
+-------+--------+-----------+------+------------+---------+------+--------+
| EMPNO | ENAME  | JOB       | MGR  | HIREDATE   | SAL     | COMM | DEPTNO |
+-------+--------+-----------+------+------------+---------+------+--------+
|  7369 | SMITH  | CLERK     | 7902 | 1980-12-17 |  880.00 | NULL |     20 |
|  7499 | ALLEN  | SALESMAN  | 7698 | 1981-02-20 | 1600.00 |  300 |     30 |
|  7521 | WARD   | SALESMAN  | 7698 | 1981-02-22 | 1250.00 |  300 |     30 |
|  7566 | JONES  | MANAGER   | 7839 | 1981-04-02 | 3273.00 | NULL |     20 |
|  7654 | MARTIN | SALESMAN  | 7698 | 1981-09-28 | 1250.00 | 1400 |     30 |
|  7698 | BLAKE  | MANAGER   | 7839 | 1981-05-01 | 2850.00 | NULL |     30 |
|  7782 | CLARK  | MANAGER   | 7839 | 1981-06-09 | 2695.00 | NULL |     20 |
|  7788 | SCOTT  | ANALYST   | 7566 | 1982-12-09 | 3000.00 | NULL |     40 |
|  7839 | KING   | PRESIDENT | NULL | 1981-11-17 | 5500.00 | NULL |     20 |
|  7844 | TURNER | SALESMAN  | 7698 | 1981-09-08 | 1500.00 |    0 |     30 |
|  7876 | ADAMS  | CLERK     | 7788 | 1983-01-12 | 1210.00 | NULL |     20 |
|  7900 | JAMES  | CLERK     | 7698 | 1981-12-03 |  950.00 | NULL |     30 |
|  7902 | FORD   | ANALYST   | 7566 | 1981-12-03 | 3300.00 | NULL |     20 |
+-------+--------+-----------+------+------------+---------+------+--------+
13 rows in set (0.001 sec)
```

---

## 2. Delete all record into Employee_master whose DeptNo is 10.

```sql
DELETE FROM EMPLOYEE_MASTER WHERE DEPTNO = 10;
```

**Output:**
```
MariaDB [company]> DELETE FROM EMPLOYEE_MASTER WHERE DEPTNO = 10;
Query OK, 1 row affected (0.007 sec)
```

---

## 3. Update 10% in his salary of DEPTNO 20 into Employee_Master.

```sql
UPDATE EMPLOYEE_MASTER SET SAL = SAL * 1.10 WHERE DEPTNO = 20;
```

**Output:**
```
MariaDB [company]> update employee_master set sal =sal * 1.10 where deptno =20;
Query OK, 6 rows affected (0.007 sec)
Rows matched: 6  Changed: 6  Warnings: 0

MariaDB [company]> SELECT * FROM EMPLOYEE_MASTER;
+-------+--------+-----------+------+------------+------+------+--------+
| EMPNO | ENAME  | JOB       | MGR  | HIREDATE   | SAL  | COMM | DEPTNO |
+-------+--------+-----------+------+------------+------+------+--------+
|  7369 | SMITH  | CLERK     | 7902 | 1980-12-17 |  880 | NULL |     20 |
|  7499 | ALLEN  | SALESMAN  | 7698 | 1981-02-20 | 1600 |  300 |     30 |
|  7521 | WARD   | SALESMAN  | 7698 | 1981-02-22 | 1250 |  300 |     30 |
|  7566 | JONES  | MANAGER   | 7839 | 1981-04-02 | 3273 | NULL |     20 |
|  7654 | MARTIN | SALESMAN  | 7698 | 1981-09-28 | 1250 | 1400 |     30 |
|  7698 | BLAKE  | MANAGER   | 7839 | 1981-05-01 | 2850 | NULL |     30 |
|  7782 | CLARK  | MANAGER   | 7839 | 1981-06-09 | 2695 | NULL |     20 |
|  7788 | SCOTT  | ANALYST   | 7566 | 1982-12-09 | 3000 | NULL |     40 |
|  7839 | KING   | PRESIDENT | NULL | 1981-11-17 | 5500 | NULL |     20 |
|  7844 | TURNER | SALESMAN  | 7698 | 1981-09-08 | 1500 |    0 |     30 |
|  7876 | ADAMS  | CLERK     | 7788 | 1983-01-12 | 1210 | NULL |     20 |
|  7900 | JAMES  | CLERK     | 7698 | 1981-12-03 |  950 | NULL |     30 |
|  7902 | FORD   | ANALYST   | 7566 | 1981-12-03 | 3300 | NULL |     20 |
+-------+--------+-----------+------+------------+------+------+--------+
13 rows in set (0.001 sec)
```

---

## 4. Alter SAL with size 10,2 in Employee_Master.

```sql
ALTER TABLE EMPLOYEE_MASTER MODIFY SAL DECIMAL(10, 2);
```

**Output:**
```
MariaDB [company]> ALTER TABLE EMPLOYEE_MASTER MODIFY SAL DECIMAL(10,2);
Query OK, 13 rows affected (0.089 sec)
Records: 13  Duplicates: 0  Warnings: 0

MariaDB [company]> SELECT * FROM EMPLOYEE_MASTER;
+-------+--------+-----------+------+------------+---------+------+--------+
| EMPNO | ENAME  | JOB       | MGR  | HIREDATE   | SAL     | COMM | DEPTNO |
+-------+--------+-----------+------+------------+---------+------+--------+
|  7369 | SMITH  | CLERK     | 7902 | 1980-12-17 |  880.00 | NULL |     20 |
|  7499 | ALLEN  | SALESMAN  | 7698 | 1981-02-20 | 1600.00 |  300 |     30 |
|  7521 | WARD   | SALESMAN  | 7698 | 1981-02-22 | 1250.00 |  300 |     30 |
|  7566 | JONES  | MANAGER   | 7839 | 1981-04-02 | 3273.00 | NULL |     20 |
|  7654 | MARTIN | SALESMAN  | 7698 | 1981-09-28 | 1250.00 | 1400 |     30 |
|  7698 | BLAKE  | MANAGER   | 7839 | 1981-05-01 | 2850.00 | NULL |     30 |
|  7782 | CLARK  | MANAGER   | 7839 | 1981-06-09 | 2695.00 | NULL |     20 |
|  7788 | SCOTT  | ANALYST   | 7566 | 1982-12-09 | 3000.00 | NULL |     40 |
|  7839 | KING   | PRESIDENT | NULL | 1981-11-17 | 5500.00 | NULL |     20 |
|  7844 | TURNER | SALESMAN  | 7698 | 1981-09-08 | 1500.00 |    0 |     30 |
|  7876 | ADAMS  | CLERK     | 7788 | 1983-01-12 | 1210.00 | NULL |     20 |
|  7900 | JAMES  | CLERK     | 7698 | 1981-12-03 |  950.00 | NULL |     30 |
|  7902 | FORD   | ANALYST   | 7566 | 1981-12-03 | 3300.00 | NULL |     20 |
+-------+--------+-----------+------+------------+---------+------+--------+
13 rows in set (0.001 sec)
```

---

## 5. Drop Employee_master Table.

```sql
DROP TABLE EMPLOYEE_MASTER;
```

**Output:**
```
MariaDB [company]> DROP TABLE EMPLOYEE_MASTER;
Query OK, 0 rows affected (0.015 sec)

MariaDB [company]> SELECT * FROM EMPLOYEE_MASTER;
ERROR 1146 (42S02): Table 'company.employee_master' doesn't exist

MariaDB [company]>
```
