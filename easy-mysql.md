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


## 1148. Article Views I

- https://leetcode.com/problems/article-views-i/
- `Database`
- Runtime 527 ms
```sql
SELECT
    author_id AS id
FROM
    Views
WHERE
    author_id = viewer_id
GROUP BY
    author_id
ORDER BY
    author_id
```

- Runtime 471 ms
- Maybe, one line SQL is a bit faster than formatted SQL.
```sql
SELECT DISTINCT(author_id) AS id FROM Views WHERE author_id = viewer_id ORDER BY author_id
```


## 1407. Top Travellers

- https://leetcode.com/problems/top-travellers/
- `Database`
- Runtime 1030 ms
```sql
SELECT
    u.name,
    SUM(IFNULL(r.distance, 0)) AS travelled_distance
FROM
    Users u
    LEFT JOIN Rides r ON r.user_id = u.id
GROUP BY
    u.id
ORDER BY
    travelled_distance DESC,
    name ASC
```

- Runtime 811 ms
```sql
SELECT
    u.name,
    IFNULL(tmp.travelled_distance, 0) AS travelled_distance
FROM
    Users u
    LEFT JOIN (
        SELECT
            r.user_id,
            SUM(r.distance) AS travelled_distance
        FROM
            Rides r
        GROUP BY
            r.user_id
    ) tmp ON u.id = tmp.user_id
ORDER BY
    tmp.travelled_distance DESC, u.name ASC
```


## 1484. Group Sold Products By The Date

- https://leetcode.com/problems/group-sold-products-by-the-date/
- `Database`
- Runtime 498 ms
```sql
SELECT
    sell_date,
    COUNT(DISTINCT product) AS num_sold,
    GROUP_CONCAT(
        DISTINCT product
        ORDER BY product
    ) AS products
FROM
    Activities
GROUP BY
    sell_date
ORDER BY
    sell_date
```


## 175. Combine Two Tables

- https://leetcode.com/problems/combine-two-tables/
- `Database`
- Runtime 422 ms
```sql
SELECT
    p.firstName,
    p.lastName,
    a.city,
    a.state
FROM
    Person p
    LEFT JOIN Address a ON p.personId = a.personId
```


## 595. Big Countries

- https://leetcode.com/problems/big-countries/
- `Database`
- Runtime 432 ms
```sql
SELECT
    name,
    population,
    area
FROM
    World
WHERE
    area >= 3000000
    OR population >= 25000000;
```
- Runtime 320 ms
```sql
SELECT name, population, area FROM World WHERE area >= 3000000 OR population >= 25000000;
```


## 1757. Recyclable and Low Fat Products

- https://leetcode.com/problems/recyclable-and-low-fat-products/
- `Database`
- Runtime 555 ms
```sql
SELECT
    product_id
FROM
    Products
WHERE
    low_fats = 'Y'
    AND recyclable = 'Y';
```


## 584. Find Customer Referee

- https://leetcode.com/problems/find-customer-referee/
- `Database`
- Runtime 699 ms
```sql
SELECT
    name
FROM
    Customer
WHERE
    referee_id IS NULL
    OR referee_id != 2;
```


## 183. Customers Who Never Order

- https://leetcode.com/problems/customers-who-never-order/
- `Database`
- Runtime 1983 ms
```sql
SELECT
    c.name AS Customers
FROM
    Customers c
    LEFT JOIN Orders o ON c.id = o.customerID
WHERE
    o.id IS NULL;
```
- Runtime 463 ms
```sql
SELECT
    name AS Customers
FROM
    Customers
WHERE
    id NOT IN(
        SELECT
            customerId
        FROM
            Orders
    );
```


## 1873. Calculate Special Bonus

- https://leetcode.com/problems/calculate-special-bonus/
- `Database`
- Runtime 609 ms
```sql
SELECT
    employee_id,
    CASE
        WHEN employee_id % 2 <> 0
        AND name NOT LIKE 'M%' THEN salary
        ELSE 0
    END AS bonus
FROM
    employees
ORDER BY
    employee_id;
```
- Runtime 576 ms
```sql
SELECT
    employee_id,
    IF(
        employee_id % 2 <> 0
        AND name NOT LIKE 'M%',
        salary,
        0
    ) AS bonus
FROM
    Employees
ORDER BY
    employee_id;
```


## 627. Swap Salary

- https://leetcode.com/problems/swap-salary/
- `Database`
- Runtime 259 ms
```sql
UPDATE
    Salary
SET
    sex = CASE
        WHEN sex = 'f' THEN 'm'
        WHEN sex = 'm' THEN 'f'
    END;
```

- Runtime 245 ms
```sql
UPDATE
    Salary
SET
    sex = IF(sex = 'f', 'm', 'f');
```

