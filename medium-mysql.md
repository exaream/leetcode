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
