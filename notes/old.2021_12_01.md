---
id: tjvez6jiqvaqz4sptdujby3
title: '2021_12_01'
desc: ''
updated: 1662566166174
created: 1662566166174
isDir: false
---
- [[wsl]]挂载其他硬盘
	- `wmic diskdrive list brief` 查看硬盘。
	- `wsl --mount \\.\PHYSICALDRIVE0 --partition 1` 将查到的硬盘挂上去。
	- 这个好象在重启(休眠)之后会失效，需要重新挂，不然wsl启动不了
-
- 打印注册会计师专业阶段合格证
-
- [[python]]虚拟环境`venv`
	- 需要python的版本大于3.3
	- 创建：`python -m venv /path/to/new/virtual/env` 一般就在项目文件夹中创建
	- 激活：`source env/bin/activate` 如果是fish shell `source env/bin/activate.fish`
	- 离开：`deactivate`
	- 安装包：在虚拟环境下正常使用pip
	- 安装批量：`pip install -r requirements.txt`
	- 冻结：`pip freeze`
-
- [[python]]替换中国源
	- 创建配置文件`~/.pip/pip.conf`
	- 在pip.conf配置镜像源
	  ```
	  [global]
	  timeout = 6000
	  index-url = https://mirrors.aliyun.com/pypi/simple/
	  trusted-host = mirrors.aliyun.com
	  ```
-
- [[tmux]] #cheatsheet
	- session
		- start a new session `tmux`
		- kill session: exit all shell
		- detach from session `ctrl+b d`
		- show all sessions `tmux ls`
		- attach to last session: `tmux a`
		- session and window preview: `ctrl+b w`
	- windows
		- create window `ctrl+b c`
		- close current window: exit all panel or `ctrl+b &`
		- switch next window `ctrl+b n`
		- switch last wiindow `ctrl+b l`
	- panes
		- 水平分割：`ctrl+b %`
		- 垂直分割：`ctrl+b "`
		- 左右移动：`ctrl+b {}`
		- 前行各个pane：`ctrl+b`后上下左右方向
		- panel最大化：`ctrl+b z`
		- 将panel转为window: `ctrl+b !`
	- others
		- help: `ctrl+b ?`
-
- [[wsl]]启动和停止
	- `wsl -t Arch` or `wsl --shutdown` 停止
	- `wsl -d Arch`
	-
- 乐歌电动桌控制失灵怎么办？
	- 同时按住上下键，过几秒就能恢复。
-
- [[linux]]切换用户
	- `su - eric`使用这个命令加了一个减号，可以在切换后进入用户的家目录。
	- 在fish shell中设置PATH：`fish_add_path /mnt/c/WINDOWS/system32`
	-