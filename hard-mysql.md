# Medium Level Problems

- https://leetcode.com/problemset/all/?page=1&sorting=W3sic29ydE9yZGVyIjoiREVTQ0VORElORyIsIm9yZGVyQnkiOiJBQ19SQVRFIn1d&difficulty=HARD&status=NOT_STARTED


## 185. Department Top Three Salaries

- https://leetcode.com/problems/department-top-three-salaries/
- Runtime 1838 ms
```sql
SELECT
    d.name AS 'Department',
    e1.name AS 'Employee',
    e1.salary
FROM
    Employee e1
    INNER JOIN Department d ON e1.departmentId = d.id
WHERE
    3 > (
        SELECT
            COUNT(DISTINCT e2.salary)
        FROM
            Employee e2
        WHERE
            e2.salary > e1.salary
            AND e1.departmentId = e2.departmentId
    );
```

- Runtime 1771 ms
```sql
SELECT
    d.name AS Department,
    e.name AS Employee,
    e.salary AS Salary
FROM
    (
        SELECT
            departmentId,
            name,
            salary,
            DENSE_RANK() OVER (
                PARTITION BY departmentId
                ORDER BY
                    salary DESC
            ) AS ranking
        FROM
            Employee
    ) AS e
    INNER JOIN Department d ON e.departmentId = d.id
WHERE
    ranking < 4;
```

- Runtime 1527 ms
```sql
WITH cte AS(
    SELECT
        name,
        salary,
        DENSE_RANK() OVER(
            PARTITION BY departmentId
            ORDER BY salary DESC
        ) ranking,
        departmentId
    FROM
        Employee
)

SELECT
    d.name AS Department,
    e.name AS Employee,
    e.salary AS Salary
FROM
    cte e
    JOIN Department d ON d.id = e.departmentId
WHERE
    e.ranking < 4;
```
