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
    activity
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
            orders
        GROUP BY
            customer_number
        ORDER BY
            order_count DESC
        LIMIT
            1
    ) AS t1
```

- Runtime 488 ms
```sql
SELECT
    customer_number
FROM
    orders
GROUP BY
    customer_number
ORDER BY
    COUNT(order_number) DESC
LIMIT
    1
```
