# DBMS Lab - Retrieving Data using Employee Table

---

## 1. List all employees and jobs in Department 30 in descending order by salary.

```sql
SELECT ename, job, sal, deptno FROM employee WHERE deptno = 30 ORDER BY sal DESC;
```

**Output:**
```
MariaDB [company]> select ename,job,sal,deptno from employee where deptno =30 order by sal desc;
+--------+----------+------+--------+
| ename  | job      | sal  | deptno |
+--------+----------+------+--------+
| BLAKE  | MANAGER  | 2850 |     30 |
| ALLEN  | SALESMAN | 1600 |     30 |
| TURNER | SALESMAN | 1500 |     30 |
| WARD   | SALESMAN | 1250 |     30 |
| MARTIN | SALESMAN | 1250 |     30 |
| JAMES  | CLERK    |  950 |     30 |
+--------+----------+------+--------+
6 rows in set (0.001 sec)
```

---

## 2. List job and Department Number of employees whose name are five letters long begin with "A" and end with "N".

```sql
SELECT job, deptno FROM employee WHERE ename LIKE 'A___N';
```

**Output:**
```
MariaDB [company]> select job,deptno from employee where ename like  'A___N';
+----------+--------+
| job      | deptno |
+----------+--------+
| SALESMAN |     30 |
+----------+--------+
1 row in set (0.001 sec)
```

---

## 3. Display the name of employees whose name start with alphabet S.

```sql
SELECT ename, deptno FROM employee WHERE ename LIKE 's%';
```

**Output:**
```
MariaDB [company]> select ename ,deptno from employee where ename like 's%';
+-------+--------+
| ename | deptno |
+-------+--------+
| SMITH |     20 |
| SCOTT |     40 |
+-------+--------+
2 rows in set (0.001 sec)
```

---

## 4. Display the names of employees whose name ends with alphabet S.

```sql
SELECT ename, deptno FROM employee WHERE ename LIKE '%s';
```

**Output:**
```
MariaDB [company]> select ename ,deptno from employee where ename like '%s';
+-------+--------+
| ename | deptno |
+-------+--------+
| JONES |     20 |
| ADAMS |     20 |
| JAMES |     30 |
+-------+--------+
3 rows in set (0.001 sec)
```

---

## 5. Display the names of employees working in department number 10 or 20 or 40 or employees working as clerks, salesman or analyst.

```sql
SELECT ename, deptno, job FROM employee 
WHERE deptno = 10 OR deptno = 20 OR deptno = 40 
OR job IN ('clerk', 'salesman', 'analyst');
```

**Output:**
```
MariaDB [company]> select ename,deptno,job from employee where deptno =10 or deptno=20 or deptno=40 or job in ('clerk','salesman','analyst');
+--------+--------+-----------+
| ename  | deptno | job       |
+--------+--------+-----------+
| SMITH  |     20 | CLERK     |
| ALLEN  |     30 | SALESMAN  |
| WARD   |     30 | SALESMAN  |
| JONES  |     20 | MANAGER   |
| MARTIN |     30 | SALESMAN  |
| CLARK  |     20 | MANAGER   |
| SCOTT  |     40 | ANALYST   |
| KING   |     20 | PRESIDENT |
| TURNER |     30 | SALESMAN  |
| ADAMS  |     20 | CLERK     |
| JAMES  |     30 | CLERK     |
| FORD   |     20 | ANALYST   |
| MILLER |     10 | CLERK     |
+--------+--------+-----------+
13 rows in set (0.001 sec)
```

---

## 6. Display employee number and names for employees who earn commission.

```sql
SELECT empno, ename, comm FROM employee WHERE comm <> 0;
```

**Output:**
```
MariaDB [company]> select empno,ename,comm from employee where comm <> 0;
+-------+--------+------+
| empno | ename  | comm |
+-------+--------+------+
|  7499 | ALLEN  |  300 |
|  7521 | WARD   |  300 |
|  7654 | MARTIN | 1400 |
+-------+--------+------+
3 rows in set (0.000 sec)
```

---

## 7. Display employee number and total salary for each employee.

```sql
SELECT empno, (sal + IFNULL(comm, 0)) AS total_sal FROM employee;
```

**Output:**
```
MariaDB [company]> select empno ,(sal +nvl(comm,0)) as total_sal from employee ;
+-------+-----------+
| empno | total_sal |
+-------+-----------+
|  7369 |       800 |
|  7499 |      1900 |
|  7521 |      1550 |
|  7566 |      2975 |
|  7654 |      2650 |
|  7698 |      2850 |
|  7782 |      2450 |
|  7788 |      3000 |
|  7839 |      5000 |
|  7844 |      1500 |
|  7876 |      1100 |
|  7900 |       950 |
|  7902 |      3000 |
|  7934 |      1300 |
+-------+-----------+
14 rows in set (0.001 sec)
```

---

## 8. Display employee number and annual salary for each employee.

```sql
SELECT empno, (sal * 12) AS annual_salery FROM employee;
```

**Output:**
```
MariaDB [company]> select empno ,(sal * 12) as annual_salery from employee ;
+-------+---------------+
| empno | annual_salery |
+-------+---------------+
|  7369 |          9600 |
|  7499 |         19200 |
|  7521 |         15000 |
|  7566 |         35700 |
|  7654 |         15000 |
|  7698 |         34200 |
|  7782 |         29400 |
|  7788 |         36000 |
|  7839 |         60000 |
|  7844 |         18000 |
|  7876 |         13200 |
|  7900 |         11400 |
|  7902 |         36000 |
|  7934 |         15600 |
+-------+---------------+
14 rows in set (0.001 sec)
```

---

## 9. Display the names of all employees working as clerks and drawing a salary more than 3,000.

```sql
SELECT ename FROM employee WHERE job = 'clerk' AND sal > 3000;
```

**Output:**
```
MariaDB [company]> select ename from employee where job = 'clerk' and sal > 3000;
Empty set (0.001 sec)
```

---

## 10. Display the names of employees who are working as clerk, salesman or analyst and drawing a salary more than 3,000.

```sql
SELECT ename FROM employee WHERE job IN ('clerk', 'salesman', 'analyst') AND sal > 3000;
```

**Output:**
```
MariaDB [company]> select ename from employee where job in ('clerk','salesman','analyst') and sal > 3000;
Empty set (0.000 sec)
```
