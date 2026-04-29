# Lab 8 — JOIN Queries

> **Database:** MariaDB | **Tables used:** `EMPLOYEE`, `DEPARTMENT`, `SALGRADE`

---

**1. Display all employees with their department name.**

```sql
SELECT E.ENAME, D.DNAME
FROM EMPLOYEE E
JOIN DEPARTMENT D
ON E.DEPTNO = D.DEPTNO;
```

**Output:**
```
+-------+------------+
| ENAME | DNAME      |
+-------+------------+
| SMITH | ACCOUNTING |
| JONES | ACCOUNTING |
| CLARK | ACCOUNTING |
| SCOTT | OPERATIONS |
| KING  | ACCOUNTING |
| ADAMS | ACCOUNTING |
| FORD  | ACCOUNTING |
+-------+------------+
```

---

**2. Display employees whose manager is JONES, along with manager name.**

```sql
SELECT E.ENAME AS EMPLOYEE, M.ENAME AS MANAGER
FROM EMPLOYEE E
JOIN EMPLOYEE M ON E.MGR = M.EMPNO
WHERE M.ENAME = 'JONES';
```

**Output:**
```
+----------+---------+
| EMPLOYEE | MANAGER |
+----------+---------+
| SCOTT    | JONES   |
| FORD     | JONES   |
+----------+---------+
```

---

**3. Display employee name, job, dept name, manager name, grade — ordered by department.**

```sql
SELECT E.ENAME, E.JOB, D.DNAME,
       M.ENAME AS MANAGER,
       S.GRADE
FROM EMPLOYEE E
JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
LEFT JOIN EMPLOYEE M ON E.MGR = M.EMPNO
JOIN SALGRADE S ON E.SAL BETWEEN S.LOSAL AND S.HISAL
ORDER BY D.DNAME;
```

**Output:**
```
+-------+-----------+------------+---------+-------+
| ENAME | JOB       | DNAME      | MANAGER | GRADE |
+-------+-----------+------------+---------+-------+
| ADAMS | CLERK     | ACCOUNTING | SCOTT   |     1 |
| JONES | MANAGER   | ACCOUNTING | KING    |     4 |
| FORD  | ANALYST   | ACCOUNTING | JONES   |     4 |
| CLARK | MANAGER   | ACCOUNTING | KING    |     4 |
| KING  | PRESIDENT | ACCOUNTING | NULL    |     5 |
| SMITH | CLERK     | ACCOUNTING | FORD    |     1 |
| SCOTT | ANALYST   | OPERATIONS | JONES   |     4 |
+-------+-----------+------------+---------+-------+
```

---

**4. List all employees (except clerks) with name, job, salary grade, dept name — sorted by salary descending.**

```sql
SELECT E.ENAME, E.JOB, E.SAL, D.DNAME, S.GRADE
FROM EMPLOYEE E
JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
JOIN SALGRADE S ON E.SAL BETWEEN S.LOSAL AND S.HISAL
WHERE E.JOB <> 'CLERK'
ORDER BY E.SAL DESC;
```

**Output:**
```
+-------+-----------+---------+------------+-------+
| ENAME | JOB       | SAL     | DNAME      | GRADE |
+-------+-----------+---------+------------+-------+
| KING  | PRESIDENT | 5000.00 | ACCOUNTING |     5 |
| FORD  | ANALYST   | 3000.00 | ACCOUNTING |     4 |
| SCOTT | ANALYST   | 3000.00 | OPERATIONS |     4 |
| JONES | MANAGER   | 2975.00 | ACCOUNTING |     4 |
| CLARK | MANAGER   | 2450.00 | ACCOUNTING |     4 |
+-------+-----------+---------+------------+-------+
```

---

**5. Display employee name, job and manager. Also include employees without a manager.**

```sql
SELECT E.ENAME, E.JOB,
       IFNULL(M.ENAME, 'NO MANAGER') AS MANAGER
FROM EMPLOYEE E
LEFT JOIN EMPLOYEE M ON E.MGR = M.EMPNO;
```

**Output:**
```
+-------+-----------+------------+
| ENAME | JOB       | MANAGER    |
+-------+-----------+------------+
| SMITH | CLERK     | FORD       |
| JONES | MANAGER   | KING       |
| CLARK | MANAGER   | KING       |
| SCOTT | ANALYST   | JONES      |
| KING  | PRESIDENT | NO MANAGER |
| ADAMS | CLERK     | SCOTT      |
| FORD  | ANALYST   | JONES      |
+-------+-----------+------------+
```

---

**6. List employee name, job, annual salary, deptno, dept name and grade — earning 36000/year OR not clerks.**

```sql
SELECT E.ENAME, E.JOB, (E.SAL*12) AS ANNUAL_SAL,
       E.DEPTNO, D.DNAME, S.GRADE
FROM EMPLOYEE E
JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
JOIN SALGRADE S ON E.SAL BETWEEN S.LOSAL AND S.HISAL
WHERE (E.SAL*12) = 36000
   OR E.JOB <> 'CLERK';
```

**Output:**
```
+-------+-----------+------------+--------+------------+-------+
| ENAME | JOB       | ANNUAL_SAL | DEPTNO | DNAME      | GRADE |
+-------+-----------+------------+--------+------------+-------+
| JONES | MANAGER   |   35700.00 |     20 | ACCOUNTING |     4 |
| CLARK | MANAGER   |   29400.00 |     20 | ACCOUNTING |     4 |
| SCOTT | ANALYST   |   36000.00 |     40 | OPERATIONS |     4 |
| KING  | PRESIDENT |   60000.00 |     20 | ACCOUNTING |     5 |
| FORD  | ANALYST   |   36000.00 |     20 | ACCOUNTING |     4 |
+-------+-----------+------------+--------+------------+-------+
```

---

**7. List ename, job, annual sal, deptno, dname and grade — earning 30000/year AND not clerks.**

```sql
SELECT E.ENAME, E.JOB, (E.SAL*12) AS ANNUAL_SAL,
       E.DEPTNO, D.DNAME, S.GRADE
FROM EMPLOYEE E
JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
JOIN SALGRADE S ON E.SAL BETWEEN S.LOSAL AND S.HISAL
WHERE (E.SAL*12) = 30000
  AND E.JOB <> 'CLERK';
```

**Output:** `Empty set`

---

**8. List all employees by name and number along with manager's name and number; show 'NO MANAGER' if none.**

```sql
SELECT E.ENAME, E.EMPNO,
       IFNULL(M.ENAME, 'NO MANAGER') AS MANAGER_NAME,
       M.EMPNO AS MANAGER_NO
FROM EMPLOYEE E
LEFT JOIN EMPLOYEE M ON E.MGR = M.EMPNO;
```

**Output:**
```
+-------+-------+--------------+------------+
| ENAME | EMPNO | MANAGER_NAME | MANAGER_NO |
+-------+-------+--------------+------------+
| SMITH |  7369 | FORD         |       7902 |
| JONES |  7566 | KING         |       7839 |
| CLARK |  7782 | KING         |       7839 |
| SCOTT |  7788 | JONES        |       7566 |
| KING  |  7839 | NO MANAGER   |       NULL |
| ADAMS |  7876 | SCOTT        |       7788 |
| FORD  |  7902 | JONES        |       7566 |
+-------+-------+--------------+------------+
```

---

**9. Select dept name, dept no and sum of salary.**

```sql
SELECT D.DNAME, D.DEPTNO, SUM(E.SAL) AS TOTAL_SALARY
FROM EMPLOYEE E
JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
GROUP BY D.DNAME, D.DEPTNO;
```

**Output:**
```
+------------+--------+--------------+
| DNAME      | DEPTNO | TOTAL_SALARY |
+------------+--------+--------------+
| ACCOUNTING |     20 |     15325.00 |
| OPERATIONS |     40 |      3000.00 |
+------------+--------+--------------+
```

---

**10. Display employee number, name and location of the department they work in.**

```sql
SELECT E.EMPNO, E.ENAME, D.LOC
FROM EMPLOYEE E
JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO;
```

**Output:**
```
+-------+-------+--------+
| EMPNO | ENAME | LOC    |
+-------+-------+--------+
|  7369 | SMITH | DALLAS |
|  7566 | JONES | DALLAS |
|  7782 | CLARK | DALLAS |
|  7788 | SCOTT | BOSTON |
|  7839 | KING  | DALLAS |
|  7876 | ADAMS | DALLAS |
|  7902 | FORD  | DALLAS |
+-------+-------+--------+
```

---

**11. Display employee name and department name for each employee.**

```sql
SELECT E.ENAME, D.DNAME
FROM EMPLOYEE E
JOIN DEPARTMENT D
ON E.DEPTNO = D.DEPTNO;
```

**Output:**
```
+-------+------------+
| ENAME | DNAME      |
+-------+------------+
| SMITH | ACCOUNTING |
| JONES | ACCOUNTING |
| CLARK | ACCOUNTING |
| SCOTT | OPERATIONS |
| KING  | ACCOUNTING |
| ADAMS | ACCOUNTING |
| FORD  | ACCOUNTING |
+-------+------------+
```
