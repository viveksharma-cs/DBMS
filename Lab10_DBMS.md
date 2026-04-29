# Lab 10 — ANY / ALL & Advanced Subqueries

> **Database:** MariaDB | **Tables used:** `EMPLOYEE`, `DEPARTMENT`, `SALGRADE`

---

**1. Display employees from dept 10 with salary greater than ANY employee in other departments.**

```sql
SELECT ENAME
FROM EMPLOYEE
WHERE DEPTNO = 10
  AND SAL > ANY (
      SELECT SAL FROM EMPLOYEE WHERE DEPTNO <> 10
  );
```

**Output:**
```
+--------+
| ENAME  |
+--------+
| MILLER |
+--------+
```

---

**2. Display employees from dept 10 with salary greater than ALL employees in other departments.**

```sql
SELECT ENAME
FROM EMPLOYEE
WHERE DEPTNO = 10
  AND SAL > ALL (
      SELECT SAL FROM EMPLOYEE WHERE DEPTNO <> 10
  );
```

**Output:** `Empty set`

---

**3. Display details of employees in Sales dept with grade 3.**

```sql
SELECT E.*
FROM EMPLOYEE E
JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
JOIN SALGRADE S ON E.SAL BETWEEN S.LOSAL AND S.HISAL
WHERE D.DNAME = 'SALES'
  AND S.GRADE = 3;
```

**Output:**
```
+------+--------+----------+------+------------+---------+--------+--------+
| empno| ename  | job      | mgr  | hiredate   | sal     | comm   | deptno |
+------+--------+----------+------+------------+---------+--------+--------+
| 7499 | ALLEN  | SALESMAN | 7698 | 1981-02-20 | 1600.00 | 300.00 |     30 |
| 7844 | TURNER | SALESMAN | 7698 | 1981-09-08 | 1500.00 |   0.00 |     30 |
+------+--------+----------+------+------------+---------+--------+--------+
```

---

**4. Display those who are not managers (and who are managers of anyone).**

```sql
SELECT *
FROM EMPLOYEE
WHERE JOB <> 'MANAGER';
```

**Output:** 11 rows — all non-manager employees (SMITH, ALLEN, WARD, MARTIN, SCOTT, KING, TURNER, ADAMS, JAMES, FORD, MILLER)

---

**5. Display employees whose manager name is JONES.**

```sql
SELECT E.ENAME
FROM EMPLOYEE E
JOIN EMPLOYEE M ON E.MGR = M.EMPNO
WHERE M.ENAME = 'JONES';
```

**Output:**
```
+-------+
| ENAME |
+-------+
| SCOTT |
| FORD  |
+-------+
```

---

**6. Display employees working in the Sales department.**

```sql
SELECT E.ENAME
FROM EMPLOYEE E
JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
WHERE D.DNAME = 'SALES';
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

**7. Display employee name, dept name, salary and commission for salary between 2000–5000 in Chicago.**

```sql
SELECT E.ENAME, D.DNAME, E.SAL, E.COMM
FROM EMPLOYEE E
JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
WHERE E.SAL BETWEEN 2000 AND 5000
  AND D.LOC = 'CHICAGO';
```

**Output:**
```
+-------+-------+---------+------+
| ENAME | DNAME | SAL     | COMM |
+-------+-------+---------+------+
| BLAKE | SALES | 2850.00 | NULL |
+-------+-------+---------+------+
```

---

**8. Display employees whose salary is greater than their manager's salary.**

```sql
SELECT E.ENAME
FROM EMPLOYEE E
JOIN EMPLOYEE M ON E.MGR = M.EMPNO
WHERE E.SAL > M.SAL;
```

**Output:**
```
+-------+
| ENAME |
+-------+
| SCOTT |
| FORD  |
+-------+
```

---

**9. Display employees working in the same department as their manager.**

```sql
SELECT E.ENAME
FROM EMPLOYEE E
JOIN EMPLOYEE M ON E.MGR = M.EMPNO
WHERE E.DEPTNO = M.DEPTNO;
```

**Output:**
```
+--------+
| ENAME  |
+--------+
| SMITH  |
| ALLEN  |
| WARD   |
| JONES  |
| MARTIN |
| CLARK  |
| TURNER |
| JAMES  |
| FORD   |
+--------+
```

---

**10. Display grade and employee name for dept 10 or 30 where grade is not 4 and hired before 31-Dec-82.**

```sql
SELECT E.ENAME, S.GRADE
FROM EMPLOYEE E
JOIN SALGRADE S ON E.SAL BETWEEN S.LOSAL AND S.HISAL
WHERE E.DEPTNO IN (10, 30)
  AND S.GRADE <> 4
  AND E.HIREDATE < '1982-12-31';
```

**Output:**
```
+--------+-------+
| ENAME  | GRADE |
+--------+-------+
| ALLEN  |     3 |
| WARD   |     2 |
| MARTIN |     2 |
| TURNER |     3 |
| JAMES  |     1 |
| MILLER |     2 |
+--------+-------+
```
