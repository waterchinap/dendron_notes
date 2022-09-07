---
id: rnj29vfgo1r3kawjyd3h3pw
title: '2021_12_11'
desc: ''
updated: 1662566166175
created: 1662566166175
isDir: false
---
- [[archlinux]]终端的美化
	- 启动以后默认的字体很小，不利于操作。
	- 使用`setfont sun12x22`可以设置稍大一点的字体，但重新启动后失效。
	- 修改`/etc/consolefont.conf`文件，可以持久化修改
- [[archlinux]]实现在终端自动登录
	- 按照wiki里，对getty进行配置，即可以实现自动登录到某一个终端
		- `/etc/systemd/system/`创建一个tty1的配置文件夹：`getty@tty1.service.d`
		- 在文件夹下创建一个配置文件`override.conf`，按wiki里的内容，填写需要自动登录的用户名。
		- 重启后就可以自动登录到设置的用户名下了。然后可以启动i3或者sway
	- 还可以通过greetd来实现，目前还没有试。
- [[sway]]的使用要点
	- 输入法：关键是要使用waybar，原来默认的bar无法显示输入法。
	- code, logseq等使用electron的程序，需要根据wiki进行设置。
	- 注意要安装qt5-wayland, qt6-wayland,不然很多应用有问题。
	- 参考：https://wiki.archlinux.org/title/Wayland#XWayland
	- 参考：https://www.fosskers.ca/en/blog/wayland
	-
-