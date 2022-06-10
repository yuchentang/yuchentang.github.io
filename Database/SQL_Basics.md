---
sort: 2
---


# SQL Basics

## `UPDATE`

```sql
UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE condition;
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

**LIMIT & DISTINCT clauses: unique rows**


## Modulo Operation: `MOD` or `%`

Return the remainder of x/y:

- `MOD(x, y)`
- `x MOD y`
- `x % y`

## 日期函数

## 字符串函数

- concatenate strings

	`CONCAT(...,...,...)`

- 字符串截取

	`LEFT(str, n)`
	
	`RIGHT(str, n)`
	
	`SUBSTRING(string, start, length)`: length is optional. The number of characters to extract. If omitted, the whole string will be returned (from the start position)
 
## Wildcard

A wildcard character is used to substitute one or more characters in a string.

Wildcard characters are used with the `LIKE` operator. The `LIKE` operator is used in a `WHERE` clause to search for a specified pattern in a column.

For example, in MySQL:

|Symbol |Description |Example|
|:------|:-----------|:------|
|%     |Represents zero or more characters |bl% finds bl, black, blue, and blob|
|_     |Represents a single character |h_t finds hot, hat, and hit|