# SELECT

## 기본
### 전체 조회
```sql
SELECT *
FROM employees;
```

### 원하는 열만 조회하고 순서를 내림차순
```sql
SELECT employee_id, first_name, last_name
FROM employees
ORDER BY employee_id DESC;
```

### 중복 값 제거
```sql
SELECT DISTINCT employee_id
FROM employees;
```

### 별칭
```sql
SELECT employee_id AS 사원번호, first_name AS 이름, last_name AS 성
FROM employees;
```

### 값 연결
```sql
SELECT employee_id, first_name||' '||last_name
FROM employees;
```

### 산술
```sql
SELECT employee_id AS 사원번호, salary AS 급여, salary+500 AS 추가급여, salary-100 AS 인하급여, (salary*1.1)/2 AS 조정급여
FROM employees;
```

## WHERE
### 비교연산자 `=, <>(!=), >, >=, <, <=`

```sql
SELECT *
FROM employees
WHERE first_name = 'David';

SELECT *
FROM employees
WHERE employee_id >= 105;
```

### 추가연산자 `BETWEEN a AND b, IN (), LIKE '', IS NULL`

```sql
SELECT *
FROM employees
WHERE salary BETWEEN 10000 AND 20000;

SELECT *
FROM employees
WHERE salary IN (10000, 17000, 24000);

SELECT *
FROM employees
WHERE job_id LIKE 'AD%';

SELECT *
FROM employees
WHERE job_id LIKE 'AD___';

SELECT *
FROM employees
WHERE manager_id IS NULL;
```

### 논리연산자 `AND, OR, NOT`

```sql
SELECT *
FROM employees
WHERE salary > 4000
AND job_id = 'IT_PROG';
OR job_id = 'FI_ACCOUNT';

SELECT *
FROM employees
WHERE manager_id IS NOT NULL;
```
