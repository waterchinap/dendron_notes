---
id: sbbni7j3edb2n17bxy682er
title: Vs Code 离线安装插件的方式
desc: ''
updated: 1662565912898
created: 1662565912898
isDir: false
---
- 作为一个强大而又轻量级的编译器——VS code 深受各位程序猿&攻城狮的喜爱，尤其是其在线扩展插件的功能，简直不要太幸福
  collapsed:: true
  
  但是作为一只爱学习的程序猿，遇到这一点问题算什么，找度娘，找谷歌，找找解决方法，网上的方法很多，但是我测试了一下，治标不治本，所以，我再这里再写一个绝杀的方法——既然无法在线安装，那咱们就离线安装，也不是不行的
  
  下面咱们开启离线安装VScode插件学习之旅
  
  一、离线下载vscode插件
  1、进入[VScode插件市场](https://marketplace.visualstudio.com/search?term=ssh&target=VSCode&category=All%20categories&sortBy=Relevance)安装VScode插件，进入下载你所需要的插件，这里以远程连接的插件（ssh）为例。
  
  把下载下来的离线安装包拷贝到 VSCode 的安装目录下的 bin 目录下，比如我的 VSCode 安装在 D:\\Classes\\VScode translater\\Microsoft VS Code，因此这里我应该拷贝到 D:\\Classes\\VScode translater\\Microsoft VS Code\\bin 这个目录下
  
  在 bin 目录下，按下shift + 鼠标右键，会出现“在此处打开命令窗口”的字样，然后点击即可。
  输入命令 注意 code --install-extension 后面是插件的名称
  
  ```
  `code --install-extension ms-vscode-remote.remote-ssh-0.55.0.vsix` 
  
  - 1
  
  
  ```
  
  
  
  
  待看到如下提示即意味着安装成功，就可以打开 VSCode 进行查看了
  
  
  进入VS code进行查看
-
- #vscode