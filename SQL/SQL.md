---
sort: 1
---


# SQL小结

## Creating, Dropping, and Altering a Table

## Inserting, Deleting, and Updating a Row

## `CASE WHEN`

Examples:

```sql
SELECT OrderID, Quantity,
CASE
    WHEN Quantity > 30 THEN 'The quantity is greater than 30'
    WHEN Quantity = 30 THEN 'The quantity is 30'
    ELSE 'The quantity is under 30'
END AS QuantityText
FROM OrderDetails;
```

```sql
SELECT CustomerName, City, Country
FROM Customers
ORDER BY
(CASE
    WHEN City IS NULL THEN Country
    ELSE City
END);
```

Treat the whole `CASE WHEN` part as a column. It can even be combined with aggregate functions. E.g.

```sql
SELECT AVG(
	CASE WHEN is_low_fat_flg=1 AND is_recyclable_flg=1 THEN 1
	ELSE 0 
	END) * 100 AS pct_low_fat_and_recyclable
FROM products
```

## 日期函数

## 字符串函数

* 字符串截取

 `LEFT(str, n)`: 返回字符串最左边的x个字符

 `RIGHT(str, n)`: 返回字符串最左边的x个字符

 `SUBSTIRING(str, n)`: 返回字符串最左边的x个字符

[//]: # (```sql SELECT * FROM```)

## `COALESCE` Function

```sql
COALESCE(x,y,z) = x if x is not NULL
COALESCE(x,y,z) = y if x is NULL and y is not NULL
COALESCE(x,y,z) = z if x and y are NULL but z is not NULL
COALESCE(x,y,z) = NULL if x and y and z are all NULL 
```
E.g. Use the COALESCE function and a LEFT JOIN to print the teacher name and department name. Use the string 'None' where there is no department.

```sql
SELECT teacher.name, COALESCE(dept.name, 'None')
FROM teacher LEFT JOIN dept ON teacher.dept=dept.id
```

## ` ROW_NUMBER()`, `RANK()`, `DENSE_RANK`
### Using ROW_NUMBER() for finding nth highest value per group

The following example shows you how to find the employees whose have the highest salary in their departments:

```sql
-- find the highest salary per department
SELECT 
    department_name,
    first_name,
    last_name,
    salary
FROM 
    (
        SELECT 
            department_name,
            `ROW_NUMBER()` OVER (
                PARTITION BY department_name
                ORDER BY salary DESC) row_num, 
            first_name, 
            last_name, 
            salary
        FROM 
            employees e
            INNER JOIN departments d 
                ON d.department_id = e.department_id
    ) t
WHERE 
    row_num = 1;
```

### Leetcode Database Problems No. 178 Rank Scores

- Problem:

```
Input: 
Scores table:
+----+-------+
| id | score |
+----+-------+
| 1  | 3.50  |
| 2  | 3.65  |
| 3  | 4.00  |
| 4  | 3.85  |
| 5  | 4.00  |
| 6  | 3.65  |
+----+-------+
Output: 
+-------+------+
| score | rank |
+-------+------+
| 4.00  | 1    |
| 4.00  | 1    |
| 3.85  | 2    |
| 3.65  | 3    |
| 3.65  | 3    |
| 3.50  | 4    |
+-------+------+
```

- Solution 1: An easy solution using `DENSE_RANK()` is shown below. It gives the exact output. We can see that 'the tie' get the same ranking and rankings are consecutive numbers.

```sql
SELECT score, DENSE_RANK() OVER (ORDER BY score DESC) AS rank
FROM Scores
```

- Compared with `RANK()`

```sql
SELECT score, RANK() OVER (ORDER BY score DESC) AS rank
FROM Scores
```
The output is shown below. Notice that the rankings are not consecutive. 

```
Output: 
+-------+------+
| score | rank |
+-------+------+
| 4.00  | 1    |
| 4.00  | 1    |
| 3.85  | 3    |
| 3.65  | 4    |
| 3.65  | 4    |
| 3.50  | 6    |
+-------+------+
```

- Solution 2

```sql
SELECT s.score, l.rank 
from Scores s
LEFT JOIN (
    SELECT score, ROW_NUMBER() OVER (ORDER BY score DESC) AS rank
    FROM Scores 
    GROUP BY score
) l on l.score=s.score
ORDER BY s.score DESC
```

## `Lag()`, `Lead()` Functions
### Leetcode Database Problems No. 180 Consecutive Numbers

Problem:

Write an SQL query to find all numbers that appear at least three times consecutively.

```
Input: 
Logs table:
+----+-----+
| id | num |
+----+-----+
| 1  | 1   |
| 2  | 1   |
| 3  | 1   |
| 4  | 2   |
| 5  | 1   |
| 6  | 2   |
| 7  | 2   |
+----+-----+

Output: 
+-----------------+
| ConsecutiveNums |
+-----------------+
| 1               |
+-----------------+
Explanation: 1 is the only number that appears consecutively for at least three times.
```

- Solution 1: Self Join

```sql
SELECT DISTINCT
    l1.Num AS ConsecutiveNums
FROM
    Logs l1,
    Logs l2,
    Logs l3
WHERE
    l1.id = l2.id - 1
    AND l2.id = l3.id - 1
    AND l1.num = l2.num
    AND l2.num = l3.num
;
```

OR we write in a more clear way using `JOIN()`

```sql
SELECT DISTINCT l1.num AS ConsecutiveNums
FROM Logs l1
INNER JOIN Logs l2 ON l1.id=l2.id+1
INNER JOIN Logs l3 ON l2.id=l3.id+1
WHERE l1.num=l2.num AND l2.num=l3.num
```

- Solution 2: Using `LAG()` and `LEAD()`

```sql
-- CTE
WITH newlog AS (
SELECT id, num,
LAG(num) OVER (ORDER BY id) AS lag_num,
LEAD(num) OVER (ORDER BY id) AS lead_num
from logs
)
SELECT DISTINCT num AS ConsecutiveNums FROM newlog
WHERE lag_num=num AND lead_num=num
```
OR we can write as

```sql
SELECT DISTINCT num ConsecutiveNums
FROM (
	SELECT *,
	CASE WHEN num = LAG(num) OVER(ORDER BY id ASC) AND num = LEAD(num) OVER(ORDER BY id ASC)
	THEN "Y"
	ELSE "N"
	END CNs
	FROM Logs
	) ConsNums
WHERE ConsNums.CNs = "Y";
```

## `JOIN` Without Using `ON` Keyword

https://tableplus.com/blog/2019/09/sql-join-without-on.html



## 参考资料

[1] [Leetcode: https://leetcode.com/problemset/database/](https://leetcode.com/problemset/database/)

