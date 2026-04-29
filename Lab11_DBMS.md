# Lab 11 — Correlated Subqueries & DELETE

> **Database:** MariaDB | **Tables used:** `EMPLOYEE`, `DEPARTMENT`, `SALGRADE`

---

**1. Display employees whose salary is less than their manager's but more than any other manager's salary.**

```sql
SELECT E.ENAME
FROM EMPLOYEE E
JOIN EMPLOYEE M ON E.MGR = M.EMPNO
WHERE E.SAL < M.SAL
  AND E.SAL > ANY (
      SELECT SAL FROM EMPLOYEE WHERE JOB = 'MANAGER'
  );
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

**2. Find the number of employees whose salary is greater than their manager's salary.**

```sql
SELECT COUNT(*)
FROM EMPLOYEE E
JOIN EMPLOYEE M ON E.MGR = M.EMPNO
WHERE E.SAL > M.SAL;
```

**Output:**
```
+----------+
| COUNT(*) |
+----------+
|        2 |
+----------+
```

---

**3. Display managers who are not working under the president.**

```sql
SELECT ENAME
FROM EMPLOYEE
WHERE JOB = 'MANAGER'
  AND MGR <> (
      SELECT EMPNO FROM EMPLOYEE WHERE JOB = 'PRESIDENT'
  );
```

**Output:** `Empty set`

---

**4. Delete departments where no employee is working.**

```sql
DELETE FROM DEPARTMENT
WHERE DEPTNO NOT IN (
    SELECT DISTINCT DEPTNO FROM EMPLOYEE
);
```

**Output:** `Query OK, 2 rows affected`

---

**5. Delete records from EMPLOYEE table whose deptno is not in DEPARTMENT table.**

```sql
DELETE FROM EMPLOYEE
WHERE DEPTNO NOT IN (
    SELECT DEPTNO FROM DEPARTMENT
);
```

**Output:** `Query OK, 0 rows affected`

---

**6. Display employees whose salary is out of the grade range in SALGRADE table.**

```sql
SELECT ENAME, SAL
FROM EMPLOYEE
WHERE SAL NOT BETWEEN 700 AND 9999;
```

**Output:** `Empty set`

---

**7. Display employee name, salary, commission and net pay for those whose net pay is greater than any other employee.**

```sql
SELECT ENAME, SAL, COMM, (SAL + IFNULL(COMM,0)) AS NET_PAY
FROM EMPLOYEE
WHERE (SAL + IFNULL(COMM,0)) > ALL (
    SELECT (SAL + IFNULL(COMM,0)) FROM EMPLOYEE
);
```

**Output:** `Empty set`

---

**8. Display employees working in Sales or Research department.**

```sql
SELECT E.ENAME
FROM EMPLOYEE E
JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
WHERE D.DNAME IN ('SALES', 'RESEARCH');
```

**Output:** `Empty set`

---

**9. Display the grade of JONES.**

```sql
SELECT S.GRADE
FROM EMPLOYEE E
JOIN SALGRADE S ON E.SAL BETWEEN S.LOSAL AND S.HISAL
WHERE E.ENAME = 'JONES';
```

**Output:**
```
+-------+
| GRADE |
+-------+
|     4 |
+-------+
```

---

**10. Display department names whose character count equals the number of employees in any department.**

```sql
SELECT D.DNAME
FROM DEPARTMENT D
WHERE LENGTH(D.DNAME) IN (
    SELECT COUNT(*)
    FROM EMPLOYEE
    GROUP BY DEPTNO
);
```

**Output:** `Empty set`
