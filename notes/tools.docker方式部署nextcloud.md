---
id: yhosb6wcdviyeg7y5aqe5q4
title: Docker方式部署nextcloud
desc: ''
updated: 1662565912898
created: 1662565912898
isDir: false
---
- > 如果你想搭建个人或者团队私有网盘，那么 #NextCloud 可能是目前最好的选择了。
  
  搭建成功在：zealative.top:8010
## 网盘介绍

众所周知，国内很多网盘都关停了，现有的百度云还限速，甚至网盘里的文件还会被删除，网盘使用体验差、安全性堪忧。

团队内部分享文件，用微信传输有大小限制，且只能通过公网上传下载；用 QQ 传输虽然可以通过内网传输，但是有的文件是公司的机密，直接传输有泄露的风险，打包加密传输又太麻烦；并且不同部门对文档的操作权限也应该是不同的。

这个时候，如果有这么一套系统，既能够部署在局域网环境，又可以设置不同用户组对文档的访问权限，还可以实现内网 \+ 公网访问，岂不是完美解决了以上问题。

这就要说起今天的主角了--「[Nextcloud](https://nextcloud.com/)」，ownCloud 创始团队的新作，基于 ownCloud 开发，但是赋予了更多的特性，并且更加稳定，可以自定义部署，支持各种插件，甚至可以端到端加密等等。

（其实也可以考虑使用群辉等 NAS 设备，相对于非技术人员配置相对会更简单，不过不在本文讨论范围，以后有机会再写。）
## 安装
### 1、环境配置

首先，你需要有一台 Linux 环境的服务器，推荐使用 CentOS，本文及后续文章都会以 CentOS 为例。

其次，要在服务器上搭建 Docker 环境并启动 Docker，详细的操作参考我的上一篇文章「[Docker环境搭建（CentOS篇）](https://juemuren4449.com/archives/install-docker-ce-on-centos)」。

对于 #Docker 不了解也不要紧，只要按照下面的步骤进行操作即可。
### 2、拉取镜像

在终端执行以下命令，拉取 Nextcloud 镜像：

```
docker pull nextcloud 
```

拉取到的 Nextcloud 镜像的 tag 是 `latest`，显示以下信息即表示拉取成功：

```
Using default tag: latest
latest: Pulling from library/nextcloud
bc51dd8edc1b: Pull complete
a3224e2c3a89: Pull complete
be7a066df88f: Pull complete
bfdf741d72a9: Pull complete
a9e612a5f04c: Pull complete
c026d8d0e8cb: Pull complete
d94096c4941c: Pull complete
5a16031a7587: Pull complete
0cf1daf9efc0: Pull complete
b202acb13a6c: Pull complete
907001e30880: Pull complete
2e4b329c80b2: Pull complete
cd1ec92e7164: Pull complete
8cba435f5ca6: Pull complete
e15a177658f6: Pull complete
9b26736059ce: Pull complete
53dbece8c17a: Pull complete
07158f924c2a: Pull complete
5ea6266119b8: Pull complete
e377a8cc542f: Pull complete
5662efc30cde: Pull complete
Digest: sha256:fa863d16c10387f4bae140bdd38f5591aa4b88f1292593dcffa501b9e1a76e58
Status: Downloaded newer image for nextcloud:latest
docker.io/library/nextcloud:latest 
```
- ### 3、启动容器
  
  执行以下命令，启动 Nextcloud 容器：
  
  ```
  docker run -d --restart=always --name nextcloud -p 80:80 nextcloud 
  ```
  
  简单解释一下上述命令：
- `docker run` ：启动一个容器
- `-d`：后台运行容器
- `--restart=always`：Docker 重启的时候容器也会重启
- `--name nextcloud`：命名容器的 name 为 nextcloud，可以替代容器 id 使用
- `-p 80:80`：将容器的 80 端口映射到服务器的 80 端口
- `nextcloud`：要启动的镜像名称
  
  更多参数可以参考：https://hub.docker.com/_/nextcloud/
  
  执行之后会显示一个类似下面的长串字符，表示启动成功：
  
  ```
  526306c7a591205f6d2cd417384571b358e738e3c8b52c16c1fc6f1893c8535f 
  ```
  
  也可以使用下面命令查看容器是否正常运行：
  
  ```
  docker ps 
  ```
  
  如果显示以下内容，表明容器已经在运行中了：
  
  ```
  CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                               NAMES
  619d34210996        nextcloud           "/entrypoint.sh apac…"   1 hours ago        Up 1 hours         0.0.0.0:80->80/tcp                  nextcloud 
  ```
### 4、初始化安装

需要注意的是，如果使用的阿里云或腾讯云的服务器，要检查服务器的安全组是否开放了 80 端口，没有开放的需要开放一下。

如果使用的是本地虚拟机，需要执行以下命令开放 80 端口对外访问：

```
firewall-cmd --zone=public --add-port=80/tcp --permanent 
```

然后更新防火墙规则：

```
firewall-cmd --reload 
```

使用浏览器访问 [http://服务器ip](http://xn--ip-fr5c86lx7z/) 即可进入初始化设置页面。

直接输入管理员用户名和密码即可，数据库使用默认的 SQLite，后面有时间会写下怎么连 MySQL，安装推荐的应用勾不勾选无所谓，安装地址被墙了，即使勾选也不会安装。


初始化成功后弹出一个欢迎页面，关闭之后就进入到首页了，如下：


将域名解析到服务器，即可实现外网访问 Nextcloud。

## 总结

个人认为，部署 Nextcloud 最简单的方法就是使用 Docker 进行部署，其他方式多多少少都有些复杂，想了解更多部署方式请访问：「[Nextcloud 安装说明](https://nextcloud.com/install/#instructions-server)」。

本文介绍的只是最基础的环境部署，如果要在团队中的使用，还有很多需要优化和完善的地方，比如说数据库要改为 MySQL，插件的安装使用等等，后面有时间会再写一下相关的内容。

欢迎访问的个人博客：[掘墓人的小铲子](http://juemuren4449.com/)