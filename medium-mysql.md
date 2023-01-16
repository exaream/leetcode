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


## 1158. Market Analysis I

- https://leetcode.com/problems/market-analysis-i/
- Runtime 1411 ms
```sql
SELECT
    u.user_id AS buyer_id,
    u.join_date,
    COUNT(o.order_id) AS orders_in_2019
FROM
    Users u
    LEFT JOIN Orders o ON u.user_id = o.buyer_id
    AND order_date LIKE '2019%'
GROUP BY
    u.user_id;
```


## 626. Exchange Seats

- https://leetcode.com/problems/exchange-seats/
- Runtime 331 ms
```sql
-- References:
-- https://leetcode.com/problems/exchange-seats/solutions/127561/exchange-seats/
SELECT
    s1.id,
    -- Set s1.student if s2.student is NULL
    COALESCE(s2.student, s1.student) AS student
FROM
    seat s1
    -- Bit manipulation expression (id+1)^1-1 can calculate the next id.
    LEFT JOIN seat s2 ON ((s1.id + 1) ^ 1) - 1 = s2.id
ORDER BY
    s1.id;
```
- Runtime 314 ms
```sql
SELECT
    ROW_NUMBER() OVER() id,
    student
FROM
    seat
ORDER BY
    IF(id % 2 = 0, id - 1, id + 1);
```
- Runtime 311 ms
```sql
SELECT
    (
        CASE
            -- even
            WHEN id % 2 = 0 THEN id - 1
            -- odd
            WHEN max_num != id THEN id + 1
            WHEN max_num = id THEN id
        END
    ) AS id,
    student
FROM
    seat,
    (SELECT COUNT(id) AS max_num FROM seat) AS tmp
ORDER BY
    id ASC;
```


## 178. Rank Scores

- https://leetcode.com/problems/rank-scores/
- Runtime 592 ms
```sql
-- SEE: https://leetcode.com/problems/rank-scores/solutions/456610/mysql-two-simple-solutions-and-explanations-for-beginners/
SELECT
    a.score,
    COUNT(b.score) AS `rank`
FROM
    Scores a,
    (SELECT DISTINCT(score) FROM Scores) b
WHERE
    a.score <= b.score
GROUP BY
    a.id
ORDER BY
    a.score DESC;
```
- Runtime 591 ms
```sql
WITH a AS (
    SELECT
        score,
        ROW_NUMBER() OVER(ORDER BY score DESC) AS `rank`
    FROM
        Scores
    GROUP BY
        score
)

SELECT
    a.score,
    a.rank
FROM
    a
    INNER JOIN Scores AS b USING (score)
ORDER BY
    score DESC;
```
- Runtime 389 ms
```sql
-- Using variables.
SELECT
    score,
    CONVERT(`rank`, SIGNED) AS `rank`
FROM
    (
        SELECT
            score,
            @num := (CASE WHEN score = @prev THEN @num ELSE @num + 1 END) AS `rank`,
            @prev := score
        FROM
            Scores,
            (
                SELECT
                    @prev := -1,
                    @num := 0
            ) init
        ORDER BY
            Score DESC
    ) tmp;
```
- Runtime 289 ms
```sql
-- Using Window function, DENSE_RANK().
SELECT
    score,
    DENSE_RANK() OVER (ORDER BY score DESC) AS `rank`
FROM
    Scores;
```


## 184. Department Highest Salary

- https://leetcode.com/problems/department-highest-salary/
- Runtime 622 ms
```sql
SELECT
    d.name AS Department,
    e.name AS Employee,
    e.salary AS Salary
FROM
    Department d
    INNER JOIN Employee e ON d.id = e.departmentId
    INNER JOIN (
        SELECT
            departmentId,
            MAX(salary) AS max_salary
        FROM
            Employee
        GROUP BY
            departmentId
    ) tmp ON d.id = tmp.departmentId
WHERE
    e.salary = tmp.max_salary;
```
- Runtime 607 ms
```sql
-- Using WITH (Common Table Expressions)
WITH cte AS (
    SELECT
        departmentId,
        name,
        salary,
        RANK() OVER (PARTITION BY departmentId ORDER BY salary DESC) AS ranking
    FROM
        Employee
)

SELECT
    d.name AS Department,
    c.name AS Employee,
    c.salary AS Salary
FROM
    cte c
    INNER JOIN Department d ON c.departmentId = d.id
WHERE
    c.ranking = 1;
```
