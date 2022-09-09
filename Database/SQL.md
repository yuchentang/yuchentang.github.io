---
sort: 3
---

# SQL小结

## `ROW_NUMBER()`, `RANK()`, `DENSE_RANK()`
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
            ROW_NUMBER() OVER (
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

## 'Consecutive' Problems

E.g.

创作者回答情况表answer\_tb如下（其中answer\_date表示创作日期、author\_id指创作者编号、issue\_id指回答问题编号）：

|answer\_date |author\_id |issue\_id|
|:----------|:------|:--------|
|2021-11-01 |101 |E001 |
|2021-11-01 |101 |E002 |
|2021-11-01 |102 |C003 |
|2021-11-01 |103 |P001 |
|2021-11-02 |101 |P001 |
|2021-11-02 |110 |C001 |
|2021-11-03 |101 |C002|
|...              |      |        |
请你统计最大连续回答问题的天数大于等于3天的用户及其等级（若有多条符合条件的数据，按author\_id升序排序），以上例子的输出结果如下：

|author_id |days_cnt |
|:-------|:-------|
|101         |3            |
|...           |              |

Solution:

```sql
SELECT t3.author_id, author_tb.author_level, t3.days_cnt
FROM (
    SELECT author_id, start_date, COUNT(*) AS days_cnt
    FROM (
        SELECT DISTINCT answer_date, author_id, DATE_SUB(answer_date, INTERVAL num DAY) AS start_date
        FROM (
            SELECT answer_date, author_id, DENSE_RANK() OVER(PARTITION BY author_id ORDER BY answer_date) AS num
            FROM answer_tb
        ) AS t1
    ) AS t2
    GROUP BY author_id, start_date
    HAVING days_cnt >= 3
) AS t3
LEFT JOIN author_tb ON t3.author_id=author_tb.author_id
ORDER BY t3.author_id
```


## `JOIN` Without Using `ON` Keyword

Cartesian product will be returned.

https://tableplus.com/blog/2019/09/sql-join-without-on.html

## `IN` With Multiple Lines V.S. Window Function

Problem:

An table called **dept_emp** is like:

|emp_no |dept_no |from_date  |to_date    |
|:------|:-------|:----------|:----------|
|10001  |d001    |1986-06-26 |9999-01-01 |
|10002  |d001    |1996-08-03 |9999-01-01 |
|10003  |d002.   |1996-08-03 |9999-01-01 |

**salaries** table is like:

|emp_no |salary |from_date  |to_date    |
|:------|:------|:----------|:----------|
|10001  |88958  |2002-06-22 |9999-01-01 |
|10002  |72527  |2001-08-02 |9999-01-01 |
|10003  |92527  |2001-08-02 |9999-01-01 |

Find out the employees with the highest salaries withn each department, and order by dept_no, which is like:

|dept_no |emp_no |maxSalary |
|:-------|:------|:---------|
|d001    |10001  |88958     |
|d002    |10003  |92527     |

My answers (2 Methods)
The first is to find out the max salary for each department and then use `IN` for multiple columns.

```sql
WITH cte AS(
    SELECT dept_emp.emp_no, dept_emp.dept_no, salaries.salary
    FROM dept_emp INNER JOIN salaries ON dept_emp.emp_no=salaries.emp_no
)

SELECT dept_no, emp_no, salary AS maxSalary
FROM cte
WHERE (dept_no, salary) IN
(
    SELECT dept_no, MAX(salary) AS salary
    FROM cte
    GROUP BY dept_no
)
ORDER BY dept_no
```

THe second method is to use the window function `RANK() OVER()`

```sql
WITH cte AS(
    SELECT dept_emp.emp_no, dept_emp.dept_no, salaries.salary
    FROM dept_emp INNER JOIN salaries ON dept_emp.emp_no=salaries.emp_no
)

SELECT dept_no, emp_no, salary AS maxSalary
FROM
(
    SELECT *, RANK() OVER(PARTITION BY dept_no 
                          ORDER BY salary DESC) AS rank_within_dept
    FROM cte
) AS t
WHERE rank_within_dept = 1
ORDER BY dept_no
```
Don't forget the alias of the subquery.

## Find the number of occurence of one character

```sql
SELECT id, LENGTH(string) - LENGTH(REPLACE(string, ",", "")) AS cnt
FROM strings;
```

## Cumulative Total

Solution: self join by condition like `s1.xxx >= s2.xxx`

E.g.

Output:

|emp_no |salary |running_total |
|:------|:------|:-------------|
|10001 |88958 |88958|
|10002 |72527 |161485|
|10003 |43311 |204796|
|......|

```sql
SELECT s1.emp_no, s1.salary, SUM(s2.salary)
FROM salaries s1 JOIN salaries s2 ON s1.emp_no >= s2.emp_no
WHERE s1.to_date = '9999-01-01' AND s2.to_date = '9999-01-01'
GROUP BY s1.emp_no, s1.salary
```

OR using window function

SUM() OVER()

## 中位数 Median

首先我们需要知道:当某一数的正序和逆序累计均大于整个序列的数字个数的一半即为中位数

比如:

A A B B C C D D 

1 2 3  4  5 6  7 8

8 7 6  5  4  3 2 1

那么上面的4，5以及5，4就是中位数，如果是奇数的话，就只有1个

再比如

A2个，B3个，C5个，D2个，

正序2，5，10，12

倒序12，10，7，2

正序和12，大于等于6的，为C,D，

逆序和为12，大于等于6的为ABC，所以最后中位数为C

## 各科目同时在线人数

上课情况表attend\_tb如下（其中user\_id表示用户编号、course\_id代表课程编号、in\_datetime表示进入直播间的时间、out\_datetime表示离开直播间的时间）：

|user_id |course_id |in_datetime             |out_datetime              |
|:-----|:--------|:----------------|:-----------------|
|100     |1              |2021-12-01 19:00:00 |2021-12-01 19:28:00  |
|100     |1              |2021-12-01 19:30:00 |2021-12-01 19:53:00  |
|101      |1              |2021-12-01 19:00:00 |2021-12-01 20:55:00 |
|102     |1              |2021-12-01 19:00:00 |2021-12-01 19:05:00  |
|104     |1              |2021-12-01 19:00:00 |2021-12-01 20:59:00 |
|101     |2              |2021-12-02 19:05:00 |2021-12-02 20:58:00 |
|102    |2              |2021-12-02 18:55:00 |2021-12-02 21:00:00 |
|104    |2              |2021-12-02 18:57:00 |2021-12-02 20:56:00 |
|107    |2              |2021-12-02 19:10:00 |2021-12-02 19:18:00  |
|...      |                |                              |                               |

请你统计每个科目最大同时在线人数（按course\_id排序），以上数据的输出结果如下：

|course_id |max_num|
|:-------|:-------|
|1             |4           |
|2            |4           |
|3            |3           |

Solution:

```sql
WITH act AS (
    SELECT user_id, course_id, in_datetime AS dt, 1 AS act
    FROM attend_tb
    UNION
    SELECT user_id, course_id, out_datetime AS dt, -1 AS act
    FROM attend_tb
)

SELECT c.course_id, c.course_name, MAX(t.max_num) AS max_num
FROM (
    SELECT course_id, SUM(act) OVER(PARTITION BY course_id ORDER BY dt) AS max_num
    FROM act
) AS t
LEFT JOIN course_tb AS c
ON t.course_id = c.course_id
GROUP BY c.course_id, c.course_name
```

## 近一周总点赞量和一周内最大单天转发量

Problem Link: [Nowcoder SQL160 国庆期间每类视频点赞量和转发量](https://www.nowcoder.com/practice/f90ce4ee521f400db741486209914a11?tpId=268&tqId=2285070&ru=/exam/oj&qru=/ta/sql-factory-interview/question-ranking&sourceUrl=%2Fexam%2Foj%3Fpage%3D1%26tab%3DSQL%25E7%25AF%2587%26topicId%3D268)

Hints: GROUP BY, **Self Join** by date

Problem：统计2021年国庆头3天每类视频每天的近一周总点赞量和一周内最大单天转发量，结果按视频类别降序、日期升序排序。假设数据库中数据足够多，至少每个类别下国庆头3天及之前一周的每天都有播放记录。

```sql
WITH combined AS (
    SELECT u.*, v.tag
    FROM tb_user_video_log u
    JOIN tb_video_info v on u.video_id = v.video_id
),
grouped AS (
    SELECT tag, DATE_FORMAT(start_time, '%Y-%m-%d') AS dt, 
           SUM(if_like) AS like_cnt, SUM(if_retweet) AS retweet_cnt
    FROM combined
    GROUP BY tag, DATE_FORMAT(start_time, '%Y-%m-%d')
)
SELECT g1.tag, 
       g1.dt, 
       SUM(g2.like_cnt) sum_like_cnt_7d, 
       MAX(g2.retweet_cnt) max_retweet_cnt_7d
FROM grouped g1
JOIN grouped g2 
ON g1.tag = g2.tag
   AND g1.dt <= DATE_ADD(g2.dt, INTERVAL 6 DAY) 
   AND g1.dt >= g2.dt
WHERE g1.dt >= '2021-10-01' AND g1.dt <= '2021-10-03'
GROUP BY g1.tag, g1.dt
```

## 参考资料

[1] [Leetcode Database Problemset](https://leetcode.com/problemset/database/)

