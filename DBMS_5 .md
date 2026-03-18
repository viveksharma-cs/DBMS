# DBMS Lab - Aggregate & String Functions

---

## 1. Display the total number of employee working in the company.

```sql
SELECT COUNT(*) AS total_employee FROM employee;
```

**Output:**
```
MariaDB [2cse16g21552]> select count(*) as total_employee from employee;
+----------------+
| total_employee |
+----------------+
|             14 |
+----------------+
1 row in set (0.010 sec)
```

---

## 2. Display the total salary being paid to all employees.

```sql
SELECT SUM(sal) AS total_salary FROM employee;
```

**Output:**
```
MariaDB [2cse16g21552]> select sum(sal) as total_salary from employee;
+--------------+
| total_salary |
+--------------+
|        33946 |
+--------------+
1 row in set (0.001 sec)
```

---

## 3. Display the maximum salary from employee table.

```sql
SELECT MAX(sal) AS max_salary FROM employee;
```

**Output:**
```
MariaDB [2cse16g21552]> select max(sal) as max_salary from employee;
+------------+
| max_salary |
+------------+
|       6050 |
+------------+
1 row in set (0.001 sec)
```

---

## 4. Display the minimum salary from employee table.

```sql
SELECT MIN(sal) AS min_salary FROM employee;
```

**Output:**
```
MariaDB [2cse16g21552]> select min(sal) as min_salary from employee;
+------------+
| min_salary |
+------------+
|        968 |
+------------+
1 row in set (0.001 sec)
```

---

## 5. Display the average salary from employee table.

```sql
SELECT AVG(sal) AS avg_salary FROM employee;
```

**Output:**
```
MariaDB [2cse16g21552]> select avg(sal) as avg_salary from employee;
+------------+
| avg_salary |
+------------+
|  2424.7143 |
+------------+
1 row in set (0.001 sec)
```

---

## 6. Display the maximum salary being paid to clerk.

```sql
SELECT MAX(sal) AS max_salary FROM employee WHERE job = "clerk";
```

**Output:**
```
MariaDB [2cse16g21552]> select max(sal) as max_salary from employee where job ="clerk";
+------------+
| max_salary |
+------------+
|       1573 |
+------------+
1 row in set (0.001 sec)
```

---

## 7. Display the maximum salary being paid in dept no 20.

```sql
SELECT MAX(sal) AS max_salary FROM employee WHERE deptno = 20;
```

**Output:**
```
MariaDB [2cse16g21552]> select max(sal) as max_salary from employee where deptno = 20;
+------------+
| max_salary |
+------------+
|       6050 |
+------------+
1 row in set (0.002 sec)
```

---

## 8. Display the minimum salary paid to any salesman.

```sql
SELECT MIN(sal) AS min_salary FROM employee WHERE job = "salesman";
```

**Output:**
```
MariaDB [2cse16g21552]> select min(sal) as min_salary from employee where job ="salesman";
+------------+
| min_salary |
+------------+
|       1250 |
+------------+
1 row in set (0.000 sec)
```

---

## 9. Display the average salary drawn by managers.

```sql
SELECT AVG(sal) AS average_salary FROM employee WHERE job = "manager";
```

**Output:**
```
MariaDB [2cse16g21552]> select avg(sal) as average_salary from employee where job ="manager";
+----------------+
| average_salary |
+----------------+
|      3338.0000 |
+----------------+
1 row in set (0.000 sec)
```

---

## 10. Display the total salary drawn by analyst working in dept no 40.

```sql
SELECT SUM(sal) AS total_salary FROM employee WHERE job = "analyst" AND deptno = 40;
```

**Output:**
```
MariaDB [2cse16g21552]> select sum(sal) as total_salary from employee where job ="analyst" and deptno = 40;
+--------------+
| total_salary |
+--------------+
|         3630 |
+--------------+
1 row in set (0.021 sec)
```

---

## 11. Display the names of the employee in Uppercase.

```sql
SELECT UPPER(ename) FROM employee;
```

**Output:**
```
MariaDB [2cse16g21552]> select upper(ename) from employee;
+--------------+
| upper(ename) |
+--------------+
| SMITH        |
| ALLEN        |
| WARD         |
| JONES        |
| MARTIN       |
| BLAKE        |
| CLARK        |
| SCOTT        |
| KING         |
| TURNER       |
| ADAMS        |
| JAMES        |
| FORD         |
| MILLER       |
+--------------+
14 rows in set (0.001 sec)
```

---

## 12. Display the names of the employee in Lowercase.

```sql
SELECT LOWER(ename) FROM employee;
```

**Output:**
```
MariaDB [2cse16g21552]> select lower(ename) from employee;
+--------------+
| lower(ename) |
+--------------+
| smith        |
| allen        |
| ward         |
| jones        |
| martin       |
| blake        |
| clark        |
| scott        |
| king         |
| turner       |
| adams        |
| james        |
| ford         |
| miller       |
+--------------+
14 rows in set (0.001 sec)
```

---

## 13. Display the names of the employee in Proper case.

```sql
SELECT CONCAT(
    UPPER(SUBSTRING(ename, 1, 1)),
    LOWER(SUBSTRING(ename, 2))) AS proper_name
FROM employee;
```

**Output:**
```
MariaDB [2cse16g21552]> select concat(
    -> upper(substring(ename,1,1)),
    -> lower(substring(ename,2))) as proper_name from employee;
+-------------+
| proper_name |
+-------------+
| Smith       |
| Allen       |
| Ward        |
| Jones       |
| Martin      |
| Blake       |
| Clark       |
| Scott       |
| King        |
| Turner      |
| Adams       |
| James       |
| Ford        |
| Miller      |
+-------------+
14 rows in set (0.001 sec)
```

---

## 14. Display the length of Your name using appropriate function.

```sql
SELECT LENGTH("vivek") AS name_length;
```

**Output:**
```
MariaDB [2cse16g21552]> select length("vivek") as name_length;
+-------------+
| name_length |
+-------------+
|           5 |
+-------------+
1 row in set (0.001 sec)
```

---

## 15. Display the length of all the employee names.

```sql
SELECT LENGTH(ename) AS name_length FROM employee;
```

**Output:**
```
MariaDB [2cse16g21552]> select length(ename) as name_length from employee;
+-------------+
| name_length |
+-------------+
|           5 |
|           5 |
|           4 |
|           5 |
|           6 |
|           5 |
|           5 |
|           5 |
|           4 |
|           6 |
|           5 |
|           5 |
|           4 |
|           6 |
+-------------+
14 rows in set (0.001 sec)
```
