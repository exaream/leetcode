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

