# Lab 9 — Subqueries (Single-row & Multi-row)

> **Database:** MariaDB | **Tables used:** `EMPLOYEE`, `DEPARTMENT`

---

**1. Display the employee who earns the highest salary.**

```sql
SELECT ENAME
FROM EMPLOYEE
WHERE SAL = (SELECT MAX(SAL) FROM EMPLOYEE);
```

**Output:**
```
+-------+
| ENAME |
+-------+
| KING  |
+-------+
```

---

**2. Display employee number and name of the clerk earning the highest salary among clerks.**

```sql
SELECT EMPNO, ENAME
FROM EMPLOYEE
WHERE JOB = 'CLERK'
  AND SAL = (SELECT MAX(SAL) FROM EMPLOYEE WHERE JOB = 'CLERK');
```

**Output:**
```
+-------+--------+
| EMPNO | ENAME  |
+-------+--------+
|  7934 | MILLER |
+-------+--------+
```

---

**3. Display names of salesmen who earn more than the highest salary of any clerk.**

```sql
SELECT ENAME
FROM EMPLOYEE
WHERE JOB = 'SALESMAN'
  AND SAL > (SELECT MAX(SAL) FROM EMPLOYEE WHERE JOB = 'CLERK');
```

**Output:**
```
+--------+
| ENAME  |
+--------+
| ALLEN  |
| TURNER |
+--------+
```

---

**4. Display names of clerks who earn more than JAMES but less than SCOTT.**

```sql
SELECT ENAME
FROM EMPLOYEE
WHERE JOB = 'CLERK'
  AND SAL > (SELECT SAL FROM EMPLOYEE WHERE ENAME = 'JAMES')
  AND SAL < (SELECT SAL FROM EMPLOYEE WHERE ENAME = 'SCOTT');
```

**Output:**
```
+--------+
| ENAME  |
+--------+
| ADAMS  |
| MILLER |
+--------+
```

---

**5. Display names of employees who earn more than JAMES OR more than SCOTT.**

```sql
SELECT ENAME
FROM EMPLOYEE
WHERE SAL > (SELECT SAL FROM EMPLOYEE WHERE ENAME = 'JAMES')
   OR SAL > (SELECT SAL FROM EMPLOYEE WHERE ENAME = 'SCOTT');
```

**Output:**
```
+--------+
| ENAME  |
+--------+
| ALLEN  |
| WARD   |
| JONES  |
| MARTIN |
| BLAKE  |
| CLARK  |
| SCOTT  |
| KING   |
| TURNER |
| ADAMS  |
| FORD   |
| MILLER |
+--------+
```

---

**6. Display names of employees who earn the highest salary in their respective departments.**

```sql
SELECT ENAME, DEPTNO, SAL
FROM EMPLOYEE E
WHERE SAL = (
    SELECT MAX(SAL)
    FROM EMPLOYEE
    WHERE DEPTNO = E.DEPTNO
);
```

**Output:**
```
+--------+--------+---------+
| ENAME  | DEPTNO | SAL     |
+--------+--------+---------+
| BLAKE  |     30 | 2850.00 |
| SCOTT  |     40 | 3000.00 |
| KING   |     20 | 5000.00 |
| MILLER |     10 | 1300.00 |
+--------+--------+---------+
```

---

**7. Display names of employees who earn the highest salary in their respective job groups.**

```sql
SELECT ENAME, JOB, SAL
FROM EMPLOYEE E
WHERE SAL = (
    SELECT MAX(SAL)
    FROM EMPLOYEE
    WHERE JOB = E.JOB
);
```

**Output:**
```
+--------+-----------+---------+
| ENAME  | JOB       | SAL     |
+--------+-----------+---------+
| ALLEN  | SALESMAN  | 1600.00 |
| JONES  | MANAGER   | 2975.00 |
| SCOTT  | ANALYST   | 3000.00 |
| KING   | PRESIDENT | 5000.00 |
| FORD   | ANALYST   | 3000.00 |
| MILLER | CLERK     | 1300.00 |
+--------+-----------+---------+
```

---

**8. Display employee names working in the Accounting department.**

```sql
SELECT ENAME
FROM EMPLOYEE
WHERE DEPTNO = (
    SELECT DEPTNO
    FROM DEPARTMENT
    WHERE DNAME = 'ACCOUNTING'
);
```

**Output:**
```
+-------+
| ENAME |
+-------+
| SMITH |
| JONES |
| CLARK |
| KING  |
| ADAMS |
| FORD  |
+-------+
```

---

**9. Display employee names working in Chicago.**

```sql
SELECT ENAME
FROM EMPLOYEE
WHERE DEPTNO = (
    SELECT DEPTNO
    FROM DEPARTMENT
    WHERE LOC = 'CHICAGO'
);
```

**Output:**
```
+--------+
| ENAME  |
+--------+
| ALLEN  |
| WARD   |
| MARTIN |
| BLAKE  |
| TURNER |
| JAMES  |
+--------+
```

---

**10. Display job groups whose total salary is greater than the maximum salary for managers.**

```sql
SELECT JOB, SUM(SAL) AS TOTAL_SAL
FROM EMPLOYEE
GROUP BY JOB
HAVING SUM(SAL) > (
    SELECT MAX(SAL)
    FROM EMPLOYEE
    WHERE JOB = 'MANAGER'
);
```

**Output:**
```
+-----------+-----------+
| JOB       | TOTAL_SAL |
+-----------+-----------+
| ANALYST   |   6000.00 |
| CLERK     |   4150.00 |
| MANAGER   |   8275.00 |
| PRESIDENT |   5000.00 |
| SALESMAN  |   5600.00 |
+-----------+-----------+
```
