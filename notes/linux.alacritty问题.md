---
id: ebmyzl90822k0nzqb2nvqtl
title: Alacritty问题
desc: ''
updated: 1662565912898
created: 1662565912898
isDir: false
---
alacritty通过ssh远程登录到阿里云的shell时，后退和方向键不起作用。

一个解决方案时这样使用ssh

`TERM=xterm-256color ssh root@47.101.129.XX`