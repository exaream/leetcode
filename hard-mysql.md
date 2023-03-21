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

## 262. Trips and Users

- https://leetcode.com/problems/trips-and-users/
- Runtime 1140 ms
```sql
SELECT 
  t.request_at AS Day, 
  ROUND(
    SUM(CASE WHEN status IN ('cancelled_by_driver', 'cancelled_by_client') THEN 1 ELSE 0 END) / COUNT(t.id), 2
  ) AS `Cancellation Rate`
FROM 
  Trips t 
  JOIN Users u1 ON t.client_id = u1.users_id AND u1.banned = 'No'
  JOIN Users u2 ON t.driver_id = u2.users_id AND u2.banned = 'No'
WHERE 
  request_at BETWEEN '2013-10-01' AND '2013-10-03'
GROUP BY 
  request_at
```

- Runtime 917 ms
```sql
SELECT
    request_at AS DAY,
    ROUND(SUM(IF(status != 'completed', 1, 0)) / COUNT(id), 2) AS `Cancellation Rate`
FROM
    Trips
WHERE
    client_id IN (SELECT users_id FROM Users WHERE banned = 'No')
    AND driver_id IN (SELECT users_id FROM Users WHERE banned = 'No')
    AND request_at BETWEEN '2013-10-01' AND '2013-10-03'
GROUP BY
    request_at;
```

## 601. Human Traffic of Stadium

- https://leetcode.com/problems/human-traffic-of-stadium/
- 678 ms
```sql
WITH t1 AS (
    SELECT id, visit_date, people, id - ROW_NUMBER() OVER(ORDER BY id) AS diff
    FROM Stadium
    WHERE people > 99
)

SELECT id, visit_date, people
FROM t1
WHERE diff IN (SELECT diff FROM t1 GROUP BY diff HAVING COUNT(diff) > 2);
```


- 675 ms
```sql
SELECT id, visit_date, people
FROM (
    SELECT id, visit_date, people,
           LEAD(people, 1) OVER (ORDER BY id) next1,
           LEAD(people, 2) OVER (ORDER BY id) next2,
           LAG(people, 1) OVER (ORDER BY id) pre1,
           LAG(people, 2) OVER (ORDER BY id) pre2
    FROM Stadium
    ) t1 
WHERE (t1.people >= 100 AND t1.next1 >= 100 AND t1.next2 >= 100) 
    OR (t1.people >= 100 AND t1.next1 >= 100 AND t1.pre1 >= 100)  
    OR (t1.people >= 100 AND t1.pre1 >= 100 AND t1.pre2 >= 100); 
```

- 633 ms
```sql
SELECT id, visit_date, people
FROM (
        SELECT
            id, visit_date, people,
            LEAD(people, 1) OVER (ORDER BY id) next1,
            LEAD(people, 2) OVER (ORDER BY id) next2,
            LAG(people, 1) OVER (ORDER BY id) pre1,
            LAG(people, 2) OVER (ORDER BY id) pre2
        FROM Stadium
    ) t1 
WHERE
    (t1.people >= 100 AND t1.next1 >= 100 AND t1.next2 >= 100) 
    OR (t1.people >= 100 AND t1.next1 >= 100 AND t1.pre1 >= 100)  
    OR (t1.people >= 100 AND t1.pre1 >= 100 AND t1.pre2 >= 100)
```

- 620 ms
```sql
SELECT DISTINCT t2.id, t2.visit_date, t2.people
FROM (
    SELECT s1.id
    FROM Stadium s1
    JOIN Stadium s2 ON s2.id - s1.id BETWEEN 0 AND 2
    GROUP BY s1.id
    HAVING SUM(IF(s2.people >= 100, 1, 0)) = 3
    ) t1
JOIN Stadium t2 ON t2.id - t1.id BETWEEN 0 AND 2
ORDER BY id;
```

- 590 ms
```sql
WITH t1 AS (
    SELECT id, visit_date, people, id - DENSE_RANK() OVER (ORDER BY id) AS diff
    FROM Stadium
    WHERE people > 99
)

SELECT id, visit_date, people
FROM t1
WHERE diff IN (SELECT diff FROM t1 GROUP BY diff HAVING COUNT(diff) > 2)
```
