# Easy Level Problems

- https://leetcode.com/problemset/all/?page=1&sorting=W3t9XQ%3D%3D&status=NOT_STARTED&difficulty=EASY&listId=5htp6xyg


## 511. Game Play Analysis I

- https://leetcode.com/problems/game-play-analysis-i/
- Runtime 791 ms
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


## 196. Delete Duplicate Emails

- https://leetcode.com/problems/delete-duplicate-emails/
- Runtime 1031 ms
```sql
# Please write a DELETE statement and DO NOT write a SELECT statement.
DELETE a
FROM
    Person a
    INNER JOIN Person b
WHERE
    a.email = b.email
    AND a.id > b.id
```
- Runtime 811 ms
```sql
# Please write a DELETE statement and DO NOT write a SELECT statement.
# In case that you can use a SELECT statement to improve performance:
# WITH (Common Table Expressions)
WITH cte AS (
    SELECT
        MIN(id) AS id
    FROM
        Person
    GROUP BY
        email
)

DELETE FROM
    Person
WHERE
    ID NOT IN (
        SELECT
            id
        FROM
            cte
    )
```
- Runtime 546 ms
```sql
# Please write a DELETE statement and DO NOT write a SELECT statement.
# In case that you can use a SELECT statement to improve performance:
DELETE FROM
    Person
WHERE
    id NOT IN (
        SELECT
            id
        FROM
            (
                SELECT
                    MIN(id) AS id
                FROM
                    Person
                GROUP BY
                    email
            ) AS FirstIds
    );
```


## 1667. Fix Names in a Table

- https://leetcode.com/problems/fix-names-in-a-table/
- Runtime 688 ms
```sql
SELECT
    user_id,
    CONCAT (
        UPPER(SUBSTRING(name, 1, 1)),
        LOWER(SUBSTRING(name, 2))
    ) AS name
FROM
    Users
ORDER BY
    user_id;
```


## 1527. Patients With a Condition

- https://leetcode.com/problems/patients-with-a-condition/description/
- Runtime 352 ms
```sql
-- \b matches either a non-word character (a space etc) or the position before the first character in the string.
SELECT
    patient_id,
    patient_name,
    conditions
FROM
    Patients
WHERE
    conditions REGEXP '\\bDIAB1';
```
- Runtime 312 ms
```sql
SELECT
    patient_id,
    patient_name,
    conditions
FROM
    Patients
WHERE
    conditions LIKE 'DIAB1%'
    OR conditions LIKE '% DIAB1%';
```


## 1965. Employees With Missing Information

- https://leetcode.com/problems/employees-with-missing-information/
- Runtime 553 ms
```sql
SELECT employee_id
FROM Employees
WHERE employee_id NOT IN (SELECT employee_id FROM Salaries)
UNION
SELECT employee_id
FROM Salaries
WHERE employee_id NOT IN (SELECT employee_id FROM Employees)
ORDER BY employee_id;
```
- Runtime 492 ms
```sql
SELECT e.employee_id
FROM Employees e LEFT JOIN Salaries s ON e.employee_id = s.employee_id
WHERE e.name IS NULL OR s.salary IS NULL
UNION ALL
SELECT s.employee_id
FROM Salaries s LEFT JOIN Employees e ON s.employee_id = e.employee_id
WHERE e.name IS NULL OR s.salary IS NULL
ORDER BY employee_id;
```
- Runtime 454 ms
```sql
SELECT tmp.employee_id
FROM
    (
        -- Can use USING() to join 2 tables if they have the same key.
        SELECT * FROM Employees LEFT JOIN Salaries USING(employee_id)
        UNION
        SELECT * FROM Employees RIGHT JOIN Salaries USING(employee_id)
    ) AS tmp
WHERE tmp.salary IS NULL OR tmp.name IS NULL
ORDER BY tmp.employee_id;
```


## 1795. Rearrange Products Table

- https://leetcode.com/problems/rearrange-products-table/
- Runtime 569 ms
```sql
SELECT * FROM (
    SELECT product_id, 'store1' AS store, store1 AS price FROM Products
    UNION
    SELECT  product_id, 'store2' AS store, store2 AS price FROM Products
    UNION
    SELECT  product_id, 'store3' AS store, store3 AS price FROM Products
) AS tmp
WHERE price IS NOT NULL;
```
- Runtime 472 ms
```sql
SELECT product_id, 'store1' AS store, store1 AS price FROM Products WHERE store1 IS NOT NULL
UNION
SELECT  product_id, 'store2' AS store, store2 AS price FROM Products WHERE store2 IS NOT NULL
UNION
SELECT  product_id, 'store3' AS store, store3 AS price FROM Products WHERE store3 IS NOT NULL;
```


## 1581. Customer Who Visited but Did Not Make Any Transactions

- https://leetcode.com/problems/customer-who-visited-but-did-not-make-any-transactions/
- Runtime 2067 ms
```sql
SELECT
    v.customer_id,
    COUNT(v.visit_id) AS count_no_trans
FROM
    Visits v
WHERE
    NOT EXISTS (
        SELECT
            visit_id 
        FROM
            Transactions t 
        WHERE
            v.visit_id = t.visit_id
    )
GROUP BY
    v.customer_id
```
- Runtime 1338 ms
```sql
SELECT
    v.customer_id,
    COUNT(v.visit_id) AS count_no_trans
FROM
    Visits v
    LEFT JOIN Transactions t ON v.visit_id = t.visit_id
WHERE
    t.transaction_id IS NULL
GROUP BY
    v.customer_id
```
- Runtime 1333 ms
```sql
SELECT
    customer_id,
    COUNT(visit_id) AS count_no_trans
FROM
    Visits
WHERE
    visit_id NOT IN (SELECT DISTINCT(visit_id) FROM Transactions)
GROUP BY
    customer_id;
```


## 197. Rising Temperature

- https://leetcode.com/problems/rising-temperature/
- Runtime 933 ms
```sql
SELECT
    w1.id
FROM
    Weather w1
    INNER JOIN Weather w2 ON w1.recordDate = w2.recordDate + INTERVAL 1 DAY
WHERE
    w1.temperature > w2.temperature;
```
- Runtime 441 ms
```sql
-- "DATE_ADD(fooDate, INTERVAL 1 DAY)" is faster than "+ INTERVAL 1 DAY"
SELECT
    w1.id
FROM
    Weather w1
    INNER JOIN Weather w2 ON w1.recordDate = DATE_ADD(w2.recordDate, INTERVAL 1 DAY)
WHERE
    w1.temperature > w2.temperature;
```
- Runtime 396 ms
```sql
-- CROSS JOIN
SELECT
    w1.id
FROM
    Weather w1,
    Weather w2
WHERE
    w1.recordDate = DATE_ADD(w2.recordDate, INTERVAL 1 DAY)
    AND w1.temperature > w2.temperature;
```


## 1693. Daily Leads and Partners

- https://leetcode.com/problems/daily-leads-and-partners/
- Runtime 530 ms
```sql
SELECT
    date_id,
    make_name,
    COUNT(DISTINCT(lead_id)) AS unique_leads,
    COUNT(DISTINCT(partner_id)) AS unique_partners
FROM
    DailySales
GROUP BY
    date_id,
    make_name;
```


## 1729. Find Followers Count

- https://leetcode.com/problems/find-followers-count/
- Runtime 628 ms
```sql
SELECT
    user_id,
    COUNT(follower_id) AS followers_count
FROM
    Followers
GROUP BY
    user_id
ORDER BY
    user_id;
```

## 1890. The Latest Login in 2020

- https://leetcode.com/problems/the-latest-login-in-2020/
- Runtime 1121 ms
```sql
SELECT
    user_id,
    MAX(time_stamp) AS last_stamp
FROM
    Logins
WHERE
    time_stamp BETWEEN '2020-01-01 00:00:00'
    AND '2020-12-31 23:59:59'
GROUP BY
    user_id;
```
- Runtime 817 ms
```sql
-- Note that INDEX will not work if you use a function on the left-hand side of the WHERE clause.
SELECT
    user_id,
    MAX(time_stamp) AS last_stamp
FROM
    Logins
WHERE
    YEAR(time_stamp) = 2020
GROUP BY
    user_id;
```
- Runtime 710 ms
```sql
SELECT
    user_id,
    MAX(time_stamp) AS last_stamp
FROM
    Logins
WHERE
    time_stamp LIKE '2020%'
GROUP BY
    user_id;
```


## 181. Employees Earning More Than Their Managers

- https://leetcode.com/problems/employees-earning-more-than-their-managers/
- Runtime 370 ms
```sql
SELECT
    e.name AS Employee
FROM
    Employee e
    INNER JOIN Employee m ON e.managerId = m.id
WHERE
    e.salary > m.salary;
```


## 182. Duplicate Emails

- https://leetcode.com/problems/duplicate-emails/
- Runtime 442 ms
```sql
SELECT
    email AS Email
FROM
    Person
GROUP BY
    email
HAVING
    COUNT(id) > 1;
```


## 1741. Find Total Time Spent by Each Employee

- https://leetcode.com/problems/find-total-time-spent-by-each-employee/
- Runtime 474 ms
```sql
SELECT
    event_day AS day,
    emp_id,
    SUM(out_time - in_time) AS total_time
FROM
    Employees
GROUP BY
    event_day,
    emp_id;
```


## 1587. Bank Account Summary II

- https://leetcode.com/problems/bank-account-summary-ii/
- Runtime 644 ms
```sql
SELECT
    name,
    SUM(amount) AS balance
FROM
    Users u
    JOIN Transactions t ON u.account = t.account
GROUP BY
    u.account
HAVING
    balance > 10000;
```
