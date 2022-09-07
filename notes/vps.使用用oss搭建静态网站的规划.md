---
id: vhdjarifproc485wshrpe2d
title: 使用用oss搭建静态网站的规划
desc: ''
updated: 1662565912904
created: 1662565912904
isDir: false
---
## 域名
必需。
申请后可以备案也可以不备案。
不备案只能使用香港的bucket.
## 空间
为了免备案，在香港的空间开启一个buket。

~~为了mkdocs生成的site文件夹同步，在空间建立一个目录，设为blog.
设置一个blog的子域名。
更新后重新生产站点，可以用sync重新部署。~~


~~为ppt应用建立另一个目录，设为ppt，同时设置另一个子域名。
添加新的内容后用sync更新。~~

以上不行，一个子域名只能对应一个bucket，所以不能用新建目录来解决，只能新建一个bucket

在成都的空间另开一个buket，用来做为图床。
设置typora, picgo使得在插入图片时，同时上传图片到图床。 #OSS