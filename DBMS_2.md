# DBMS Lab - Retrieving Data using Employee Table

---

## 1. List all distinct job in Employee.

```sql
SELECT DISTINCT job FROM employee;
```

**Output:**
```
MariaDB [company]> select distinct job  from employee ;
+-----------+
| job       |
+-----------+
| CLERK     |
| SALESMAN  |
| MANAGER   |
| ANALYST   |
| PRESIDENT |
+-----------+
5 rows in set (0.002 sec)
```

---

## 2. List all information about employee in Department Number 30.

```sql
SELECT * FROM employee WHERE deptno = 30;
```

**Output:**
```
MariaDB [company]> select * from employee where deptno = 30 ;
+-------+--------+----------+------+------------+------+------+--------+
| EMPNO | ENAME  | JOB      | MGR  | HIREDATE   | SAL  | COMM | DEPTNO |
+-------+--------+----------+------+------------+------+------+--------+
|  7499 | ALLEN  | SALESMAN | 7698 | 1981-02-20 | 1600 |  300 |     30 |
|  7521 | WARD   | SALESMAN | 7698 | 1981-02-22 | 1250 |  300 |     30 |
|  7654 | MARTIN | SALESMAN | 7698 | 1981-09-28 | 1250 | 1400 |     30 |
|  7698 | BLAKE  | MANAGER  | 7839 | 1981-05-01 | 2850 | NULL |     30 |
|  7844 | TURNER | SALESMAN | 7698 | 1981-09-08 | 1500 |    0 |     30 |
|  7900 | JAMES  | CLERK    | 7698 | 1981-12-03 |  950 | NULL |     30 |
+-------+--------+----------+------+------------+------+------+--------+
6 rows in set (0.041 sec)
```

---

## 3. Find all department number with department names greater than 20.

```sql
SELECT deptno, dname FROM department WHERE deptno > 20;
```

**Output:**
```
MariaDB [company]> select deptno ,dname from department where deptno >20;
+--------+------------+
| deptno | dname      |
+--------+------------+
|     30 | SALES      |
|     40 | OPERATIONS |
+--------+------------+
2 rows in set (0.001 sec)
```

---

## 4. Find all information about all the managers as well as the clerks in department 30.

```sql
SELECT * FROM employee WHERE deptno = 30 AND job IN ('manager', 'clerk');
```

**Output:**
```
MariaDB [company]> select * from employee where deptno = 30 and  job in ('manager','clerk');
+-------+-------+---------+------+------------+------+------+--------+
| EMPNO | ENAME | JOB     | MGR  | HIREDATE   | SAL  | COMM | DEPTNO |
+-------+-------+---------+------+------------+------+------+--------+
|  7698 | BLAKE | MANAGER | 7839 | 1981-05-01 | 2850 | NULL |     30 |
|  7900 | JAMES | CLERK   | 7698 | 1981-12-03 |  950 | NULL |     30 |
+-------+-------+---------+------+------------+------+------+--------+
2 rows in set (0.001 sec)
```

---

## 5. List the Employee name, Employee numbers and department of all clerks.

```sql
SELECT ename, empno, deptno, job FROM employee WHERE job = 'clerk';
```

**Output:**
```
MariaDB [company]> select ename,empno,deptno,job from employee where job = 'clerk';
+--------+-------+--------+-------+
| ename  | empno | deptno | job   |
+--------+-------+--------+-------+
| SMITH  |  7369 |     20 | CLERK |
| ADAMS  |  7876 |     20 | CLERK |
| JAMES  |  7900 |     30 | CLERK |
| MILLER |  7934 |     10 | CLERK |
+--------+-------+--------+-------+
4 rows in set (0.001 sec)
```

---

## 6. Find all managers not in department 30.

```sql
SELECT * FROM employee WHERE job = "manager" AND deptno <> 30;
```

**Output:**
```
MariaDB [company]> select * from employee where  job ="manager" and  deptno< > 30;
+-------+-------+---------+------+------------+------+------+--------+
| EMPNO | ENAME | JOB     | MGR  | HIREDATE   | SAL  | COMM | DEPTNO |
+-------+-------+---------+------+------------+------+------+--------+
|  7566 | JONES | MANAGER | 7839 | 1981-04-02 | 2975 | NULL |     20 |
|  7782 | CLARK | MANAGER | 7839 | 1981-06-09 | 2450 | NULL |     20 |
+-------+-------+---------+------+------------+------+------+--------+
2 rows in set (0.001 sec)
```

---

## 7. List information about all Employees in department 10 who are not manager or clerks.

```sql
SELECT * FROM employee WHERE deptno = 10 AND job NOT IN ("manager", "clerk");
```

**Output:**
```
MariaDB [company]> select * from employee where deptno = 10 and job not in (
"manager","clerk");
Empty set (0.001 sec)
```

---

## 8. Find Employees and jobs earning between 1200 and 1400.

```sql
SELECT ename, job FROM employee WHERE sal > 1200 AND sal < 1400;
```

**Output:**
```
MariaDB [company]> select ename , job from employee where sal >1200 and sal<1400 ;
+--------+----------+
| ename  | job      |
+--------+----------+
| WARD   | SALESMAN |
| MARTIN | SALESMAN |
| MILLER | CLERK    |
+--------+----------+
3 rows in set (0.001 sec)
```

---

## 9. List Name and Department Number of employee who are clerks, analyst or salesman.

```sql
SELECT ename, deptno, job FROM employee WHERE job IN ('clerk', 'analyst', 'salesman');
```

**Output:**
```
MariaDB [company]> select ename,deptno ,job from employee where job in ('clerk','analyst','salesman');
+--------+--------+----------+
| ename  | deptno | job      |
+--------+--------+----------+
| SMITH  |     20 | CLERK    |
| ALLEN  |     30 | SALESMAN |
| WARD   |     30 | SALESMAN |
| MARTIN |     30 | SALESMAN |
| SCOTT  |     40 | ANALYST  |
| TURNER |     30 | SALESMAN |
| ADAMS  |     20 | CLERK    |
| JAMES  |     30 | CLERK    |
| FORD   |     20 | ANALYST  |
| MILLER |     10 | CLERK    |
+--------+--------+----------+
10 rows in set (0.000 sec)
```

---

## 10. List Name and Department Number of employee whose names began with M.

```sql
SELECT ename, deptno FROM employee WHERE ename LIKE 'm%';
```

**Output:**
```
MariaDB [company]> select ename ,deptno from employee where ename like 'm%';
+--------+--------+
| ename  | deptno |
+--------+--------+
| MARTIN |     30 |
| MILLER |     10 |
+--------+--------+
2 rows in set (0.001 sec)
```
