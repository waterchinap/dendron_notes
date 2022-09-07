---
id: 39q6pgkdbldyjwcfv0b3fae
title: Linux 常用命令
desc: ''
updated: 1662565912901
created: 1662565912901
isDir: false
---
- 用来记录 #linux 常用的命令
## 查看某个目录中的磁盘占用：
	- https://www.mankier.com/
	  
	  ```
	  du -h -s *
	  
	  du -sh path/to/directory
	  ```
## linux cp 隐藏文件

`cp -r /etc/somedir ~/`
-
## 递归查找某种类型的文件，并全部拷贝出来
	- `find ./ -iname "*.md" -exec cp {} ./temp \;`
	- 注意：{}表示对找到的结果全部执行，；是结束符号是必须的。\反是用来脱字分号的，因为不同系统分号可能有不同意义。