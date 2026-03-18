# DBMS Lab - Advanced SQL Queries

---

## 1. Compute the no. of days remaining in this year.

```sql
SELECT DATEDIFF(DATE('2026-12-31'), CURDATE()) AS days_remaining;
```

**Output:**
```
MariaDB [company]> select datediff(date('2026-12-31'), curdate()) as days_remaining;
+----------------+
| days_remaining |
+----------------+
|            287 |
+----------------+
1 row in set (0.001 sec)
```

---

## 2. Find the highest and lowest salaries and the difference between of them.

```sql
SELECT MAX(sal) AS max_salary, MIN(sal) AS min_salary, MAX(sal) - MIN(sal) AS difference FROM employee;
```

**Output:**
```
MariaDB [company]> select max(sal) as max_salary, min(sal) as min_salary, max(sal)-min(sal) as difference from employee;
+------------+------------+------------+
| max_salary | min_salary | difference |
+------------+------------+------------+
|       5000 |        800 |       4200 |
+------------+------------+------------+
1 row in set (0.001 sec)
```

---

## 3. List employee whose commission is greater than 25% of their salaries.

```sql
SELECT ename, sal, comm FROM employee WHERE comm > sal * 0.25;
```

**Output:**
```
MariaDB [company]> select ename, sal, comm from employee where comm > sal * 0.25;
+--------+------+------+
| ename  | sal  | comm |
+--------+------+------+
| MARTIN | 1250 | 1400 |
+--------+------+------+
1 row in set (0.001 sec)
```

---

## 4. Make a query that displays salary in dollar format.

```sql
SELECT ename, CONCAT('$', FORMAT(sal, 2)) AS salary_in_dollar FROM employee;
```

**Output:**
```
MariaDB [company]> select ename, concat('$', format(sal, 2)) as salary_in_dollar from employee;
+--------+------------------+
| ename  | salary_in_dollar |
+--------+------------------+
| SMITH  | $800.00          |
| ALLEN  | $1,600.00        |
| WARD   | $1,250.00        |
| JONES  | $2,975.00        |
| MARTIN | $1,250.00        |
| BLAKE  | $2,850.00        |
| CLARK  | $2,450.00        |
| SCOTT  | $3,000.00        |
| KING   | $5,000.00        |
| TURNER | $1,500.00        |
| ADAMS  | $1,100.00        |
| JAMES  | $950.00          |
| FORD   | $3,000.00        |
| MILLER | $1,300.00        |
+--------+------------------+
14 rows in set (0.001 sec)
```

---

## 5. Create a matrix query to display the job, the salary for that job based on department number, and the total salary for that job for all departments, giving each column an appropriate heading.

```sql
SELECT job,
    SUM(CASE WHEN deptno = 10 THEN sal ELSE 0 END) AS dept_10,
    SUM(CASE WHEN deptno = 20 THEN sal ELSE 0 END) AS dept_20,
    SUM(CASE WHEN deptno = 30 THEN sal ELSE 0 END) AS dept_30,
    SUM(CASE WHEN deptno = 40 THEN sal ELSE 0 END) AS dept_40,
    SUM(sal) AS total
FROM employee
GROUP BY job;
```

**Output:**
```
MariaDB [company]> select job,
    -> sum(case when deptno=10 then sal else 0 end) as dept_10,
    -> sum(case when deptno=20 then sal else 0 end) as dept_20,
    -> sum(case when deptno=30 then sal else 0 end) as dept_30,
    -> sum(case when deptno=40 then sal else 0 end) as dept_40,
    -> sum(sal) as total
    -> from employee group by job;
+-----------+---------+---------+---------+---------+-------+
| job       | dept_10 | dept_20 | dept_30 | dept_40 | total |
+-----------+---------+---------+---------+---------+-------+
| CLERK     |    1300 |    1900 |     950 |       0 |  4150 |
| SALESMAN  |       0 |       0 |    6600 |       0 |  6600 |
| MANAGER   |    2450 |    2975 |    2850 |       0 |  8275 |
| ANALYST   |       0 |    3000 |       0 |    3000 |  6000 |
| PRESIDENT |       0 |    5000 |       0 |       0 |  5000 |
+-----------+---------+---------+---------+---------+-------+
5 rows in set (0.001 sec)
```

---

## 6. Query that will display the total no of employees, and of that total the number who were hired in 1980, 1981, 1982 and 1983. Give appropriate column heading.

```sql
SELECT
    COUNT(*) AS total_employees,
    SUM(CASE WHEN YEAR(hiredate) = 1980 THEN 1 ELSE 0 END) AS hired_1980,
    SUM(CASE WHEN YEAR(hiredate) = 1981 THEN 1 ELSE 0 END) AS hired_1981,
    SUM(CASE WHEN YEAR(hiredate) = 1982 THEN 1 ELSE 0 END) AS hired_1982,
    SUM(CASE WHEN YEAR(hiredate) = 1983 THEN 1 ELSE 0 END) AS hired_1983
FROM employee;
```

**Output:**
```
MariaDB [company]> select
    -> count(*) as total_employees,
    -> sum(case when year(hiredate)=1980 then 1 else 0 end) as hired_1980,
    -> sum(case when year(hiredate)=1981 then 1 else 0 end) as hired_1981,
    -> sum(case when year(hiredate)=1982 then 1 else 0 end) as hired_1982,
    -> sum(case when year(hiredate)=1983 then 1 else 0 end) as hired_1983
    -> from employee;
+-----------------+------------+------------+------------+------------+
| total_employees | hired_1980 | hired_1981 | hired_1982 | hired_1983 |
+-----------------+------------+------------+------------+------------+
|              14 |          1 |          9 |          2 |          2 |
+-----------------+------------+------------+------------+------------+
1 row in set (0.001 sec)
```

---

## 7. Query to get the last Sunday of Any Month.

```sql
SELECT DATE_SUB(LAST_DAY(CURDATE()), INTERVAL (WEEKDAY(LAST_DAY(CURDATE())) + 1) % 7 DAY) AS last_sunday;
```

**Output:**
```
MariaDB [company]> select date_sub(last_day(curdate()), interval (weekday(last_day(curdate()))+1)%7 day) as last_sunday;
+-------------+
| last_sunday |
+-------------+
| 2026-03-29  |
+-------------+
1 row in set (0.001 sec)
```

---

## 8. Display department numbers and total number of employees working in each department.

```sql
SELECT deptno, COUNT(*) AS total_employees FROM employee GROUP BY deptno;
```

**Output:**
```
MariaDB [company]> select deptno, count(*) as total_employees from employee group by deptno;
+--------+-----------------+
| deptno | total_employees |
+--------+-----------------+
|     20 |               6 |
|     30 |               6 |
|     40 |               1 |
|     10 |               1 |
+--------+-----------------+
4 rows in set (0.001 sec)
```

---

## 9. Display the various jobs and total number of employees within each job group.

```sql
SELECT job, COUNT(*) AS total_employees FROM employee GROUP BY job;
```

**Output:**
```
MariaDB [company]> select job, count(*) as total_employees from employee group by job;
+-----------+-----------------+
| job       | total_employees |
+-----------+-----------------+
| CLERK     |               4 |
| SALESMAN  |               4 |
| MANAGER   |               3 |
| ANALYST   |               2 |
| PRESIDENT |               1 |
+-----------+-----------------+
5 rows in set (0.001 sec)
```

---

## 10. Display the department numbers and total salary for each department.

```sql
SELECT deptno, SUM(sal) AS total_salary FROM employee GROUP BY deptno;
```

**Output:**
```
MariaDB [company]> select deptno, sum(sal) as total_salary from employee group by deptno;
+--------+--------------+
| deptno | total_salary |
+--------+--------------+
|     20 |        10875 |
|     30 |        10050 |
|     40 |         3000 |
|     10 |         1300 |
+--------+--------------+
4 rows in set (0.001 sec)
```
