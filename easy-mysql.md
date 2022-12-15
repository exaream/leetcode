# Easy Level Problems

- https://leetcode.com/problemset/all/?page=1&sorting=W3t9XQ%3D%3D&status=NOT_STARTED&difficulty=EASY&listId=5htp6xyg


## 511. Game Play Analysis I

- https://leetcode.com/problems/game-play-analysis-i/
- Runtime 791 ms
- `Database`
```sql
SELECT
    player_id,
    MIN(event_date) AS first_login
FROM
    Activity
GROUP BY
    player_id
```


## 586. Customer Placing the Largest Number of Orders

- https://leetcode.com/problems/customer-placing-the-largest-number-of-orders/
- `Database`
- Runtime 513 ms
```sql
SELECT
    customer_number
FROM
    (
        SELECT
            customer_number,
            COUNT(order_number) AS order_count
        FROM
            Orders
        GROUP BY
            customer_number
        ORDER BY
            order_count DESC
        LIMIT
            1
    ) AS tmp
```

- Runtime 488 ms
```sql
SELECT
    customer_number
FROM
    Orders
GROUP BY
    customer_number
ORDER BY
    COUNT(order_number) DESC
LIMIT
    1
```


## 607. Sales Person

- https://leetcode.com/problems/sales-person/
- `Database`
- Runtime 1007 ms
```sql
SELECT
    name
FROM
    SalesPerson
WHERE
    sales_id NOT IN(
        SELECT
            o.sales_id
        FROM
            Company c
            INNER JOIN Orders o ON c.com_id = o.com_id
        WHERE
            c.name = 'RED'
    )
```

## 1050. Actors and Directors Who Cooperated At Least Three Times

- https://leetcode.com/problems/actors-and-directors-who-cooperated-at-least-three-times/
- `Database`
- Runtime 393 ms
```sql
SELECT
    actor_id,
    director_id
FROM
    ActorDirector
GROUP BY
    actor_id,
    director_id
HAVING
    COUNT(timestamp) > 2
```


## 1084. Sales Analysis III

- https://leetcode.com/problems/sales-analysis-iii/
- `Database`
- Runtime 1532 ms
```sql
SELECT
    p.product_id,
    p.product_name
FROM
    Product p
    INNER JOIN Sales s ON p.product_id = s.product_id
WHERE
    s.sale_date BETWEEN '2019-01-01' AND '2019-03-31'
    AND s.product_id NOT IN (
        SELECT
            product_id
        FROM
            Sales
        WHERE
            sale_date NOT BETWEEN '2019-01-01' AND '2019-03-31'
    )
GROUP BY
    p.product_id
```

- Runtime 1386 ms
```sql
SELECT
    p.product_id,
    p.product_name
FROM
    Product p
    JOIN Sales s ON p.product_id = s.product_id
GROUP BY
    s.product_id
HAVING
    MIN(s.sale_date) >= '2019-01-01'
    AND MAX(s.sale_date) <= '2019-03-31'
```


## 1141. User Activity for the Past 30 Days I

- https://leetcode.com/problems/user-activity-for-the-past-30-days-i/
- `Database`
- Runtime 599 ms
```sql
SELECT
    activity_date AS day,
    COUNT(DISTINCT(user_id)) AS active_users
FROM
    Activity
WHERE
    activity_date > '2019-06-27' -- DATE_FORMAT(('2019-07-27' - INTERVAL 30 DAY), '%Y-%m-%d')
    AND activity_date < '2019-07-28'
GROUP BY
    activity_date
```