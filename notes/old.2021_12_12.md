---
id: u2fcvr6zxffo5oy80mlbqlr
title: '2021_12_12'
desc: ''
updated: 1662566166175
created: 1662566166175
isDir: false
---
- [[sqlite]]查询一个表中的行数
	- 方法一：`select count(rowid) from daily` 0.4 seconds
	- 方法二：`select count(1) from daily` 0.2 seconds。这应该是最常用的方法
	- 方法三：`select rowid form daily order by rowid desc limit 1` o.oo4 seconds
		- 这个方法快了100倍，但前提是sqlite3要保证rowid连续。目前不确定是否可靠。
		- 查了资料，不可靠。使用了VACUUM之后，数据库会压缩空间释放删除记录空间，这时才是可靠的。