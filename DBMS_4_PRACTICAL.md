# DBMS Lab - Practical 4

---

## 1. Display the list of employees who have joined the company before 30th June 80 or after 31st Dec 81.

```sql
SELECT ENAME FROM employee WHERE hiredate < '1980-06-30' OR hiredate > '1981-12-30';
```

**Output:**
```
MariaDB [2cse16g21552]> SELECT ENAME from employee where hiredate < '1980-06-30' or hiredate >'1981-12-30';
+---------+
| ENAME   |
+---------+
| SCOTT   |
| ADAMS   |
| MILLER  |
+---------+
3 rows in set (0.041 sec)
```

---

## 2. Display the names of employees whose names have second alphabet A in their names.

```sql
SELECT ename FROM employee WHERE ename LIKE '_A%';
```

**Output:**
```
MariaDB [2cse16g21552]> select ename from employee where ename like '_A%';
+--------+
| ename  |
+--------+
| WARD   |
| MARTIN |
| JAMES  |
+--------+
3 rows in set (0.042 sec)
```

---

## 3. Display the names of employees whose name is exactly five characters in length.

```sql
SELECT ename FROM employee WHERE LENGTH(ename) = 5;
```

**Output:**
```
MariaDB [2cse16g21552]> select ename from employee where length(ename)=5;
+-------+
| ename |
+-------+
| SMITH |
| ALLEN |
| JONES |
| BLAKE |
| CLARK |
| SCOTT |
| ADAMS |
| JAMES |
+-------+
8 rows in set (0.041 sec)
```

---

## 4. Display the names of employees whose names have second alphabet A in their names.

```sql
SELECT ename FROM employee WHERE SUBSTR(ename, 2, 1) = 'a';
```

**Output:**
```
MariaDB [2cse16g21552]> select ename from employee where substr(ename,2,1)="a";
+--------+
| ename  |
+--------+
| WARD   |
| MARTIN |
| JAMES  |
+--------+
3 rows in set (0.001 sec)
```

---

## 5. Display the names of employees who are not working as salesman or clerk or analyst.

```sql
SELECT ename FROM employee WHERE job NOT IN ('clerk', 'salesman', 'analyst');
```

**Output:**
```
MariaDB [2cse16g21552]> select ename from employee where job not in ('clerk','salesman','analyst');
+-------+
| ename |
+-------+
| JONES |
| BLAKE |
| CLARK |
| KING  |
+-------+
4 rows in set (0.001 sec)
```

---

## 6. Display the name of the employee along with their annual salary (sal*12). The name of the employee earning highest salary should appear first.

```sql
SELECT ename, (sal * 12) AS annual_sal FROM employee ORDER BY sal DESC;
```

**Output:**
```
MariaDB [2cse16g21552]> select ename ,(sal *12)as annual_sal  from employee order by sal desc;
+--------+------------+
| ename  | annual_sal |
+--------+------------+
| KING   |      66000 |
| SCOTT  |      39600 |
| FORD   |      39600 |
| JONES  |      39276 |
| BLAKE  |      37620 |
| CLARK  |      32340 |
| ALLEN  |      19200 |
| TURNER |      18000 |
| MILLER |      17160 |
| MARTIN |      15000 |
| WARD   |      15000 |
| ADAMS  |      14520 |
| JAMES  |      12540 |
| SMITH  |      10560 |
+--------+------------+
14 rows in set (0.017 sec)
```

---

## 7. Display name, sal, hra, pf, da, totalsal for each employee. The output should be in the order of total sal, hra 15% of sal, da 10% of sal, pf 5% of sal. Total salary will be (sal+hra+da)-pf.

```sql
SELECT ename, sal,
    (sal + sal*0.15 + sal*0.10) - sal*0.05 AS total_sal,
    sal*0.15 AS hra,
    sal*0.10 AS da,
    sal*0.05 AS pf
FROM employee;
```

**Output:**
```
MariaDB [2cse16g21552]> select ename ,sal,
    -> (sal+sal*0.15+sal*0.10)-sal*0.05 as total_sal,
    -> sal*0.15 as hra,
    -> sal*0.10 as da,
    -> sal*0.05 as pf from employee;
+--------+------+-----------+--------+--------+--------+
| ename  | sal  | total_sal | hra    | da     | pf     |
+--------+------+-----------+--------+--------+--------+
| SMITH  |  880 |   1056.00 | 132.00 |  88.00 |  44.00 |
| ALLEN  | 1600 |   1920.00 | 240.00 | 160.00 |  80.00 |
| WARD   | 1250 |   1500.00 | 187.50 | 125.00 |  62.50 |
| JONES  | 3273 |   3927.60 | 490.95 | 327.30 | 163.65 |
| MARTIN | 1250 |   1500.00 | 187.50 | 125.00 |  62.50 |
| BLAKE  | 3135 |   3762.00 | 470.25 | 313.50 | 156.75 |
| CLARK  | 2695 |   3234.00 | 404.25 | 269.50 | 134.75 |
| SCOTT  | 3300 |   3960.00 | 495.00 | 330.00 | 165.00 |
| KING   | 5500 |   6600.00 | 825.00 | 550.00 | 275.00 |
| TURNER | 1500 |   1800.00 | 225.00 | 150.00 |  75.00 |
| ADAMS  | 1210 |   1452.00 | 181.50 | 121.00 |  60.50 |
| JAMES  | 1045 |   1254.00 | 156.75 | 104.50 |  52.25 |
| FORD   | 3300 |   3960.00 | 495.00 | 330.00 | 165.00 |
| MILLER | 1430 |   1716.00 | 214.50 | 143.00 |  71.50 |
+--------+------+-----------+--------+--------+--------+
14 rows in set (0.010 sec)
```

---

## 8. Update the salary of each employee by 10% increment who are not eligible for commission.

```sql
UPDATE employee SET sal = sal * 1.10 WHERE comm IS NULL;
```

**Output:**
```
MariaDB [2cse16g21552]> update employee set sal = sal*1.10 where comm is null;
Query OK, 10 rows affected (0.047 sec)
Rows matched: 10  Changed: 10  Warnings: 0

MariaDB [2cse16g21552]> select ename, sal from employee ;
+--------+------+
| ename  | sal  |
+--------+------+
| SMITH  |  968 |
| ALLEN  | 1600 |
| WARD   | 1250 |
| JONES  | 3600 |
| MARTIN | 1250 |
| BLAKE  | 3449 |
| CLARK  | 2965 |
| SCOTT  | 3630 |
| KING   | 6050 |
| TURNER | 1500 |
| ADAMS  | 1331 |
| JAMES  | 1150 |
| FORD   | 3630 |
| MILLER | 1573 |
+--------+------+
14 rows in set (0.001 sec)
```

---

## 9. Display those employees whose salary is more than 3000 after giving 20% increment.

```sql
SELECT ename, sal FROM employee WHERE sal * 1.20 > 3000;
```

**Output:**
```
MariaDB [2cse16g21552]> select ename ,sal from employee where sal*1.20 >3000;
+-------+------+
| ename | sal  |
+-------+------+
| JONES | 3600 |
| BLAKE | 3449 |
| CLARK | 2965 |
| SCOTT | 3630 |
| KING  | 6050 |
| FORD  | 3630 |
+-------+------+
6 rows in set (0.001 sec)
```

---

## 10. Display those employees whose salary contains atleast 3 digits.

```sql
SELECT ename FROM employee WHERE LENGTH(sal) = 3;
```

**Output:**
```
MariaDB [2cse16g21552]> select ename from employee where length(sal)=3;
+-------+
| ename |
+-------+
| SMITH |
+-------+
1 row in set (0.001 sec)
```
