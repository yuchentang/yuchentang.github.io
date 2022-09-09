---
sort: 2
---


# SQL Basics

## `CREATE` A Table

An example:

```sql
create table tutorials_tbl(
   tutorial_id INT NOT NULL AUTO_INCREMENT,
   tutorial_title VARCHAR(100) NOT NULL,
   tutorial_author VARCHAR(40) NOT NULL,
   submission_date DATE,
   PRIMARY KEY ( tutorial_id )
);
```

## `INSERT`

Let's insert multiple rows in MySQL. The column names of actor can be dropped if all columns are included.

```sql
INSERT INTO 
	actor(actor_id, first_name, last_name, last_update)
VALUES
    (1, 'PENELOPE', 'GUINESS', '2006-02-15 12:34:33'),
    (2, 'NICK', 'WAHLBERG', '2006-02-15 12:34:33');
```

In MySQL, When using `INSERT IGNORE INTO table VALUES...`: 如果存在数据,则忽略。

```sql
insert ignore into actor 
values("3","ED","CHASE","2006-02-15 12:34:33");
```

## `UPDATE`

```sql
UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE condition;
```

Using `REPLACE` when it is associated to the primary key

```sql
UPDATE titles_test
SET emp_no = REPLACE(emp_no, 10001, 10005)
WHERE id=5 AND emp_no=10001;
```

## ADD A Column

```sql
ALTER TABLE actor
ADD (create_date datetime NOT NULL DEFAULT '2020-10-01 00:00:00');
```

## `LIMIT`

The `LIMIT` in MySQL is like

```sql
SELECT 
	select_list
FROM
	table_name
WHERE 
	condition
LIMIT [offset,] row_count;
```

Also the LIMIT part can also be written as

```sql
LIMIT row_count OFFSET offset
```

**LIMIT + DISTINCT clauses: unique rows**

## `[NOT] EXISTS`

```sql
select * from employees e
where not exists
(select emp_no from dept_emp d where d.emp_no = e.emp_no);
```

## Modulo Operation: `MOD` or `%`

Return the remainder of x/y:

- `MOD(x, y)`
- `x MOD y`
- `x % y`

## 日期函数 Functions About Dates AND Time

- `YEAR()`, `MONTH()`, `DAY()`
- `DATE_FORMAT(date, '%Y-%m') `

```sql
SELECT job, DATE_FORMAT(date, '%Y-%m') mon, SUM(num) cnt
FROM resume_info
WHERE YEAR(date) = 2025
GROUP BY job, DATE_FORMAT(date, '%Y-%m')
ORDER BY mon DESC, cnt DESC
```
- `TIME()`: Extract the time from a date

```sql
SELECT TIME("2017-08-15 19:30:10");
/*
It outputs 19:30:10
*/
```

- `TIMESTAMPDIFF(unit,datetime_expr1,datetime_expr2)`

	To get the time difference. E.g.

```sql
SELECT TIMESTAMPDIFF(MINUTE, '2021-12-01 19:00:00', '2021-12-01 19:28:00')
/*
It outputs 28.
*/
```


- `CURDATE()`: current date

## 字符串函数 Functions About Strings

- concatenate strings

	`CONCAT(...,...,...)`
	
	`GROUP_CONCAT()`
	
	E.g.
		
	```sql
	mysql> 
	SELECT student_name,
	GROUP_CONCAT(DISTINCT test_score
	             ORDER BY test_score DESC SEPARATOR ' ')
	FROM student
	GROUP BY student_name;
	```

- 字符串截取

	`LEFT(str, n)`
	
	`RIGHT(str, n)`
	
	`SUBSTRING(string, start, length)`: length is optional. The number of characters to extract. If omitted, the whole string will be returned (from the start position)

- `REPLACE()` Function

	MySQL REPLACE() replaces all the occurrences of a substring within a string.

	Syntax:

	`REPLACE(str, find_string, replace_with)`

 
## Wildcard

A wildcard character is used to substitute one or more characters in a string.

Wildcard characters are used with the `LIKE` operator. The `LIKE` operator is used in a `WHERE` clause to search for a specified pattern in a column.

For example, in MySQL:

|Symbol |Description |Example|
|:------|:-----------|:------|
|%     |Represents zero or more characters |bl% finds bl, black, blue, and blob|
|_     |Represents a single character |h_t finds hot, hat, and hit|


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

Treat the whole `CASE WHEN` part as a column. It can even be combined with aggregation functions. 

E.g.

```sql
SELECT AVG(
	CASE WHEN is_low_fat_flg=1 AND is_recyclable_flg=1 THEN 1
	ELSE 0 
	END) * 100 AS pct_low_fat_and_recyclable
FROM products
```

## `COALESCE` Function

`COALESCE(x,y,z)` = x if x is not NULL

`COALESCE(x,y,z)` = y if x is NULL and y is not NULL

`COALESCE(x,y,z)` = z if x and y are NULL but z is not NULL

`COALESCE(x,y,z)` = NULL if x and y and z are all NULL 

E.g. Use the `COALESCE()` function and a `LEFT JOIN` to print the teacher name and department name. Use the string 'None' where there is no department.

```sql
SELECT teacher.name, COALESCE(dept.name, 'None')
FROM teacher LEFT JOIN dept ON teacher.dept=dept.id
```
