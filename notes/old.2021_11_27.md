---
id: ecqcsid0bewog16zrmbss7q
title: '2021_11_27'
desc: ''
updated: 1662566166173
created: 1662566166173
isDir: false
---
- #manjaro 自带的urvxt美化
	- 修改的是家目录下的.Xresourse目录
	- 修改完之后，需要运行：`xrdb ~/.Xresources`
- #manjaro 使用百度网盘
	- baidupcs-go：终端应用，目前版本在登录时会崩溃。可以放弃使用了。
	- bypy：python命令行应用，目前可以使用。
	- 通过`yay -S baidunetdisk-electron`安装百度网盘，感觉象是官方支持版本的打包。目前使用正常。
- #pdf 工具
	- pdf合并分割工具：`pdfmixtool`
	- 切边工具`krop`
	- 阅读工具`okular`
	-
- #manjaro-i3wm 设置锁屏
	- 默认是使用xautolock配置不方便，在视频时也会锁屏
	- 根据wiki提示，安装`xidlehook`和`betterscreenlock`
	- 在i3的配置文件中使用
	- ```xidlehook --not-when-audio --not-when-fullscreen --timer 360 "betterlockscreen -l dim" ""  
	  ```
	-
-