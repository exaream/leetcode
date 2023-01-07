# Medium Level Problems

- https://leetcode.com/problemset/all/?page=1&sorting=W3sic29ydE9yZGVyIjoiREVTQ0VORElORyIsIm9yZGVyQnkiOiJGUk9OVEVORF9JRCJ9XQ%3D%3D&difficulty=MEDIUM&listId=5htp6xyg&status=NOT_STARTED


## 1393. Capital Gain/Loss

- https://leetcode.com/problems/capital-gainloss/
- `Database`
- Runtime 741 ms
```sql
SELECT
    stock_name,
    SUM(
        CASE
            operation
            WHEN 'Buy' THEN price * -1
            ELSE price
        END
    ) AS capital_gain_loss
FROM
    Stocks
GROUP BY
    stock_name
```

- Runtime 689 ms
```sql
-- WITH (Common Table Expressions)
-- MySQL 8.0+ https://dev.mysql.com/doc/refman/8.0/en/with.html
-- MariaDB 10.2.1+ https://mariadb.com/kb/en/with/
WITH cte AS (
    SELECT
        stock_name,
        operation,
        operation_day,
        CASE
            WHEN operation = 'Buy' THEN price * -1
            ELSE price
        END AS calculated_price
    FROM
        Stocks
)

SELECT
    stock_name,
    SUM(calculated_price) AS capital_gain_loss
FROM
    cte
GROUP BY
    stock_name;
```


## 608. Tree Node

- https://leetcode.com/problems/tree-node/
- `Database`
- Runtime 711 ms
```sql
SELECT
    t1.id,
    IF(
        ISNULL(t1.p_id),
        'Root',
        IF(
            t1.id IN (
                SELECT
                    t2.p_id
                FROM
                    tree t2
            ),
            'Inner',
            'Leaf'
        )
    ) type
FROM
    tree t1
ORDER BY
    t1.id
```

- Runtime 434 ms
```sql
SELECT
    id,
    CASE
        WHEN t1.p_id IS NULL
          THEN 'Root'
        WHEN t1.id IN (SELECT t2.p_id FROM tree t2)
          THEN 'Inner'
        ELSE 'Leaf'
    END AS type
FROM
    tree t1
ORDER BY id
```


## 176. Second Highest Salary

- https://leetcode.com/problems/second-highest-salary/
- Runtime 450 ms
```sql
-- CROSS JOIN
SELECT
    MAX(e2.salary) AS SecondHighestSalary
FROM
    Employee e1,
    Employee e2
WHERE
    e1.salary > e2.salary;
```
- Runtime 369 ms
```sql
-- LIMIT and OFFSET
SELECT
(
    SELECT DISTINCT salary
    FROM Employee
    ORDER BY salary DESC
    LIMIT 1
    OFFSET 1
) AS SecondHighestSalary;
```
- Runtime 314 ms
```sql
-- MAX() of multiple SELECT clauses
SELECT
    MAX(salary) AS SecondHighestSalary
FROM
    Employee
WHERE
    salary < (SELECT MAX(Salary) FROM Employee);
```
- Runtime 229 ms
```sql
-- LIMIT, OFFSET and IFFNULL()
SELECT
    IFNULL(
        NULL,
        (
            SELECT DISTINCT salary
            FROM Employee
            ORDER BY salary DESC
            LIMIT 1
            OFFSET 1
        )
    ) AS SecondHighestSalary;
```
