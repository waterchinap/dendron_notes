---
id: qad108vk8jzuardd2fpja7p
title: '2021_12_05'
desc: ''
updated: 1662566166174
created: 1662566166174
isDir: false
---
- [[sqlite]] tips
	- 列出数据库中所有表：客户端或者litecli，使用点命令`.tables`
	- 列出一个表中的所有列：
		- 在客户端可以：`pragma table_info(table_name)`或者`.schema table_name`
		- SQL: `select name from pragma_table_info(table_name)`
	- select 语句
	  collapsed:: true
		- Use ORDER BY clause to sort the result set
		  id:: 61ac35c6-f8ce-4578-a7f2-4516c117999e
			- 默认null为最小。可以用nulls last 改变。
			- 默认升序，可以用desc改变。
		- Use DISTINCT clause to query unique rows in a table
		- Use WHERE clause to filter rows in the result set
			- in 后面的列表是用小括号括起来的：`select * from basic where id in (1, 2, 3)`
			- like 使用的模式有两个通配符
				- `%表示0个或多个字符`
				- `_表示任意单个字符`
		- Use LIMIT OFFSET clauses to constrain the number of rows returned
		- Use INNER JOIN or LEFT JOIN to query data from multiple tables using join.
			- 一般情况`select a, b from left l INNER JOIN right r ON l.id=r.id `
			- 如果两个表的连接列名相同，可以简化`select a, b from basic INNER JOIN daily USING (id)`
		- Use GROUP BY to get the group rows into groups and apply aggregate function for each group.
			- group by 语句应该在where语句之后。
			- 聚合函数后面紧跟括号包起来的列名。`select id SUM(sales) from books GROUP BY id`
		- Use HAVING clause to filter groups
	- 集合操作
		- 两个类似表的交并合等。
		- Union – combine result sets of multiple queries into a single result set. We also discuss the differences between UNION and UNION ALL clauses.
		- Except – compare the result sets of two queries and returns distinct rows from the left query that are not output by the right query.
		- Intersect – compare the result sets of two queries and returns distinct rows that are output by both queries.
	- 子查询
	- 数据增删查改
	- 交易
	- 表操作：增删改
	- 表限制 constraints
	- 视图 views
	-
-