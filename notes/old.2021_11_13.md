---
id: xrymsgob529lhvq7u7wcko7
title: '2021_11_13'
desc: ''
updated: 1662566166172
created: 1662566166172
isDir: false
---
- 安装 #manjaro-i3wm
	- 原因：在原来xfce的基本上安装的i3大部分没问题，就是有些应用的阴影效果好象是因为主题的问题，出现残影，看了半天，也不知道在哪里调整。
	- manjaro-i3wm预装了一些适用的软件，看起来好象不错。
	- 下载镜象：下载到家底服务器上
		- 通过rsync命令同步到本机上。
		  `rsync somefile.iso eric@10.0.0.111 `
	- 制作liveusb
		- 使用imagewriter
	- 安装使用默认设置
		- 两难选择，还是先设置本地化吧
		- 家目录中的中文目录后面再设法改回来
	- 安装后配置
		- 设置中国源
			- `sudo pacman-mirrors -i -c China -m rank`
		- 设置输入法
			- `sudo pacman -S fcitxsudo pacman -S fcitx-configtoolsudo pacman -S fcitx-gtk3 fcitx-qt4 fcitx-qt5`
			- 字体
				- `sudo pacman -S ttf-dejavu adobe-source-han-sans-otc-fonts `
				- `pacman -S adobe-source-code-pro-fonts wqy-bitmapfont wqy-microhei wqy-zenhei wjy-microhei-lite`
				- 在i3的配置文件中设置开机启动fcitx5
			- 修改配置文件
				- ```
				  export GTK_IM_MODULE=fcitx
				  export QT_IM_MODULE=fcitx
				  export XMODIFIERS="@im=fcitx"
				  ```
		- 设置声音
			- 还没有搞定，莫名其妙搞定了。
			- 安装pulseaudio, pavucontrol，重启了一下，就好了。不知道后面有没有问题。
			-
		- appimagelaucher无法正常找到APP
		- 设置自动打开数字键盘
		- 设置时间
			- 重装了win10之后，现在正常了。
		- 设置多屏幕
			- 是否有基于xorg的图形端
			- 还是使用xrandr命令：`xrandr --output HDMI-3 --rotate left`，将其放入i3的配置文件的自动启动项目中
		- 桌面上conky不显示汉字
			- 找到相应的插件的位置`/usr/share/conky/`，用fc-list找到能用的中文字体，在相应的位置把原来的字体替换成中文字体就可以了。
-
-