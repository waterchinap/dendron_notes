---
id: ax93mxz1i6dy0zgtosvieo3
title: Gitee
desc: ''
updated: 1662565912900
created: 1662565912900
isDir: false
---
gitee配置ssh不成功，后来才发现官方有公布原因。

原因

我们使用golang.org/x/crypto/ssh来从public key中提取出指纹，以此从Gitee主应用兑换用户信息

而这个库目前（2021-10-12）还没有支持RSA-SHA2算法，因此会获取不到指纹，导致用户校验失败
临时解决

配置OpenSSH服务允许使用RSA-SHA1key

    在 ~/.ssh/config 加上如下配置
```
    Host gitee.com 
    HostkeyAlgorithms +ssh-rsa 
    PubkeyAcceptedAlgorithms +ssh-rsa
```
    PS：这种方式不需要更换ssh key，推荐Linux和windows git bash用户使用
