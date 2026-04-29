# Lab 12 — Complex Subqueries & Manager Analysis

> **Database:** MariaDB | **Tables used:** `EMPLOYEE`, `DEPARTMENT`, `SALGRADE`

---

**1. Delete employees who joined before 31-Dec-82 from departments in New York or Chicago.**

```sql
DELETE FROM EMPLOYEE
WHERE HIREDATE < '1982-12-31'
  AND DEPTNO IN (
      SELECT DEPTNO
      FROM DEPARTMENT
      WHERE LOC IN ('NEW YORK', 'CHICAGO')
  );
```

**Output:** `Query OK, 7 rows affected`

---

**2. Display employee name, job, dept name, location for all managers.**

```sql
SELECT E.ENAME, E.JOB, D.DNAME, D.LOC
FROM EMPLOYEE E
JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
WHERE E.JOB = 'MANAGER';
```

**Output:**
```
+-------+---------+------------+--------+
| ENAME | JOB     | DNAME      | LOC    |
+-------+---------+------------+--------+
| JONES | MANAGER | ACCOUNTING | DALLAS |
| CLARK | MANAGER | ACCOUNTING | DALLAS |
+-------+---------+------------+--------+
```

---

**3. Display name and salary of FORD if his salary equals the highest salary in his grade.**

```sql
SELECT E.ENAME, E.SAL
FROM EMPLOYEE E
JOIN SALGRADE S ON E.SAL BETWEEN S.LOSAL AND S.HISAL
WHERE E.ENAME = 'FORD'
  AND E.SAL = (
      SELECT MAX(E2.SAL)
      FROM EMPLOYEE E2
      JOIN SALGRADE S2 ON E2.SAL BETWEEN S2.LOSAL AND S2.HISAL
      WHERE S2.GRADE = S.GRADE
  );
```

**Output:**
```
+-------+---------+
| ENAME | SAL     |
+-------+---------+
| FORD  | 3000.00 |
+-------+---------+
```

---

**4. Find the top 5 earners of the company.**

```sql
SELECT *
FROM EMPLOYEE
ORDER BY SAL DESC
LIMIT 5;
```

**Output:**
```
+------+-------+-----------+------+------------+---------+------+--------+
| empno| ename | job       | mgr  | hiredate   | sal     | comm | deptno |
+------+-------+-----------+------+------------+---------+------+--------+
| 7839 | KING  | PRESIDENT | NULL | 1981-11-17 | 5000.00 | NULL |     20 |
| 7902 | FORD  | ANALYST   | 7566 | 1981-12-03 | 3000.00 | NULL |     20 |
| 7788 | SCOTT | ANALYST   | 7566 | 1982-12-09 | 3000.00 | NULL |     40 |
| 7566 | JONES | MANAGER   | 7839 | 1981-04-02 | 2975.00 | NULL |     20 |
| 7782 | CLARK | MANAGER   | 7839 | 1981-06-09 | 2450.00 | NULL |     20 |
+------+-------+-----------+------+------------+---------+------+--------+
```

---

**5. Display the name of employees getting the highest salary.**

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

**6. Display employees whose salary equals the average of maximum and minimum salary.**

```sql
SELECT ENAME, SAL
FROM EMPLOYEE
WHERE SAL = (
    (SELECT MAX(SAL) FROM EMPLOYEE) +
    (SELECT MIN(SAL) FROM EMPLOYEE)
) / 2;
```

**Output:** `Empty set`

---

**7. Display department names where at least 3 employees are working.**

```sql
SELECT D.DNAME
FROM EMPLOYEE E
JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
GROUP BY D.DNAME
HAVING COUNT(E.EMPNO) >= 3;
```

**Output:**
```
+------------+
| DNAME      |
+------------+
| ACCOUNTING |
+------------+
```

---

**8. Display manager names whose salary is more than the average salary of the company.**

```sql
SELECT ENAME
FROM EMPLOYEE
WHERE JOB = 'MANAGER'
  AND SAL > (SELECT AVG(SAL) FROM EMPLOYEE);
```

**Output:**
```
+-------+
| ENAME |
+-------+
| JONES |
+-------+
```

---

**9. Display managers whose salary is more than the average salary of their own employees.**

```sql
SELECT M.ENAME
FROM EMPLOYEE M
WHERE M.JOB = 'MANAGER'
  AND M.SAL > (
      SELECT AVG(E.SAL)
      FROM EMPLOYEE E
      WHERE E.MGR = M.EMPNO
  );
```

**Output:** `Empty set`

---

**10. Display employee name, salary, commission and net pay for those whose net pay >= any other employee's salary.**

```sql
SELECT ENAME, SAL, COMM, (SAL + IFNULL(COMM,0)) AS NET_PAY
FROM EMPLOYEE
WHERE (SAL + IFNULL(COMM,0)) >= ANY (
    SELECT SAL FROM EMPLOYEE
);
```

**Output:**
```
+-------+---------+------+---------+
| ENAME | SAL     | COMM | NET_PAY |
+-------+---------+------+---------+
| SMITH |  800.00 | NULL |  800.00 |
| JONES | 2975.00 | NULL | 2975.00 |
| CLARK | 2450.00 | NULL | 2450.00 |
| SCOTT | 3000.00 | NULL | 3000.00 |
| KING  | 5000.00 | NULL | 5000.00 |
| ADAMS | 1100.00 | NULL | 1100.00 |
| FORD  | 3000.00 | NULL | 3000.00 |
+-------+---------+------+---------+
```
