# DBMS Lab - Date & String Functions

---

## 1. Display empno, ename, deptno from employee table. Instead of displaying department numbers display the related department name (Use decode function).

```sql
SELECT empno, ename,
    CASE deptno
        WHEN 10 THEN 'research'
        WHEN 20 THEN 'accounting'
        WHEN 30 THEN 'sales'
        WHEN 40 THEN 'operation'
    END AS dname
FROM employee;
```

**Output:**
```
MariaDB [2cse16g21552]> select empno, ename,
    -> case deptno
    -> when 10 then 'research'
    -> when 20 then 'accounting'
    -> when 30 then 'sales'
    -> when 40 then 'operation'
    -> end as dname from employee;
+-------+--------+------------+
| empno | ename  | dname      |
+-------+--------+------------+
|  7369 | SMITH  | accounting |
|  7499 | ALLEN  | sales      |
|  7521 | WARD   | sales      |
|  7566 | JONES  | accounting |
|  7654 | MARTIN | sales      |
|  7698 | BLAKE  | sales      |
|  7782 | CLARK  | accounting |
|  7788 | SCOTT  | operation  |
|  7839 | KING   | accounting |
|  7844 | TURNER | sales      |
|  7876 | ADAMS  | accounting |
|  7900 | JAMES  | sales      |
|  7902 | FORD   | accounting |
|  7934 | MILLER | research   |
+-------+--------+------------+
14 rows in set (0.021 sec)
```

---

## 2. Display your age in days.

```sql
SELECT DATEDIFF(CURDATE(), '2005-08-31') AS days;
```

**Output:**
```
MariaDB [2cse16g21552]> select datediff(curdate(),'2005-08-31') as days;
+------+
| days |
+------+
| 7473 |
+------+
1 row in set (0.003 sec)
```

---

## 3. Display your age in months.

```sql
SELECT TIMESTAMPDIFF(MONTH, '2005-08-31', CURDATE()) AS months;
```

**Output:**
```
MariaDB [2cse16g21552]> select timestampdiff(month,'2005-08-31',curdate()) as months;
+---------+
| months  |
+---------+
|     245 |
+---------+
1 row in set (0.001 sec)
```

---

## 4. Display the current date as 15th August Friday Nineteen Ninety-Seven.

```sql
SELECT DATE_FORMAT('1997-08-15', '%D %M %W %Y') AS format_day;
```

**Output:**
```
MariaDB [2cse16g21552]> select date_format('1997-08-15','%D %M %W %Y') as format_day;
+--------------------------+
| format_day               |
+--------------------------+
| 15th August Friday 1997  |
+--------------------------+
1 row in set (0.002 sec)
```

---

## 7. Find the date for nearest Saturday after current date.

```sql
SELECT DATE_ADD(CURDATE(), INTERVAL (7 - DAYOFWEEK(CURDATE())) DAY) AS next_saturday;
```

**Output:**
```
MariaDB [2cse16g21552]> select date_add(curdate(),interval(7-dayofweek(curdate()))day) as next_saturday;
+---------------+
| next_saturday |
+---------------+
| 2026-02-21    |
+---------------+
1 row in set (0.002 sec)
```

---

## 8. Display current time.

```sql
SELECT CURTIME();
```

**Output:**
```
MariaDB [2cse16g21552]> select curtime();
+-----------+
| curtime() |
+-----------+
| 22:39:50  |
+-----------+
1 row in set (0.002 sec)
```

---

## 9. Display the date three months before the current date.

```sql
SELECT DATE_SUB(CURDATE(), INTERVAL 3 MONTH);
```

**Output:**
```
MariaDB [2cse16g21552]> select date_sub(curdate(), interval 3 month);
+---------------------------------------+
| date_sub(curdate(), interval 3 month) |
+---------------------------------------+
| 2025-11-15                            |
+---------------------------------------+
1 row in set (0.000 sec)
```

---

## 10. Display those employees who joined in the company in the month of Dec.

```sql
SELECT ename FROM employee WHERE MONTH(hiredate) = 12;
```

**Output:**
```
MariaDB [2cse16g21552]> select ename from employee where month(hiredate)=12;
+-------+
| ename |
+-------+
| SMITH |
| SCOTT |
| JAMES |
| FORD  |
+-------+
4 rows in set (0.003 sec)
```

---

## 13. Display those employees who joined the company before 15 of the months.

```sql
SELECT ename, hiredate FROM employee WHERE DAY(hiredate) < 15;
```

**Output:**
```
MariaDB [2cse16g21552]> select ename, hiredate from employee where day(hiredate)<15;
+--------+------------+
| ename  | hiredate   |
+--------+------------+
| JONES  | 1981-04-02 |
| BLAKE  | 1981-05-01 |
| CLARK  | 1981-06-09 |
| SCOTT  | 1982-12-09 |
| TURNER | 1981-09-08 |
| ADAMS  | 1983-01-12 |
| JAMES  | 1981-12-03 |
| FORD   | 1981-12-03 |
+--------+------------+
8 rows in set (0.001 sec)
```
