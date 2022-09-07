---
id: udnsuev9kvocbixu526e21n
title: GitHub使用ssh秘钥的好处以及设置
desc: ''
updated: 1662565912900
created: 1662565912900
isDir: false
---
- git使用https协议，每次pull,push都要输入密码，使用git协议，使用ssh秘钥，可以省去每次输密码
  
  大概需要三个步骤：
  一、本地生成密钥对；
  二、设置github上的公钥；
  三、修改git的remote url为git协议。
- 一、生成密钥对。
  
  大多数 Git 服务器都会选择使用 SSH 公钥来进行授权。系统中的每个用户都必须提供一个公钥用于授权，没有的话就要生成一个。生成公钥的过程在所有操作系统上都差不多。首先先确认一下是否已经有一个公钥了。SSH 公钥默认储存在账户的主目录下的 ~/.ssh 目录。进去看看：
  ````
  $ cd ~/.ssh 
  $ ls
  authorized\_keys2  id\_dsa       known\_hosts config            id\_dsa.pub
  ````
  关键是看有没有用 something 和 something.pub 来命名的一对文件，这个 something 通常就是 id\_dsa 或 id\_rsa。有 .pub 后缀的文件就是公钥，另一个文件则是密钥。假如没有这些文件，或者干脆连 .ssh 目录都没有，可以用 ssh-keygen 来创建。该程序在 Linux/Mac 系统上由 SSH 包提供，而在 Windows 上则包含在 MSysGit 包里：
  ````
  $ ssh-keygen -t rsa -C "your_email@youremail.com"
  
  \# Creates a new ssh key using the provided email # Generating public/private rsa key pair. 
  
  \# Enter file in which to save the key (/home/you/.ssh/id_rsa):
  ````
  直接Enter就行。然后，会提示你输入密码，如下(建议输一个，安全一点，当然不输也行)：
  
  ````
  Enter passphrase (empty for no passphrase): \[Type a passphrase\] 
  \# Enter same passphrase again: \[Type passphrase again\]
  ````
  完了之后，大概是这样。
  ````
  Your identification has been saved in /home/you/.ssh/id_rsa. 
  \# Your public key has been saved in /home/you/.ssh/id_rsa.pub. 
  \# The key fingerprint is: # 01:0f:f4:3b:ca:85:d6:17:a1:7d:f0:68:9d:f0:a2:db your_email@youremail.com
  ````
  这样。你本地生成密钥对的工作就做好了。
- 二、添加公钥到你的github帐户
  
  1、查看你生成的公钥：大概如下：
  ````
  $ cat ~/.ssh/id_rsa.pub  
  ssh-rsa AAAAB3NzaC1yc2EAAAABIwAAAQEAklOUpkDHrfHY17SbrmTIpNLTGK9Tjom/BWDSU GPl+nafzlHDTYW7hdI4yZ5ew18JH4JW9jbhUFrviQzM7xlE
  LEVf4h9lFX5QVkbPppSwg0cda3 Pbv7kOdJ/MTyBlWXFCR+HAo3FXRitBqxiX1nKhXpHAZsMciLq8V6RjsNAQwdsdMFvSlVK/7XA t3FaoJoAsncM1Q9x5+3V
  0Ww68/eIFmb1zuUFljQJKprrX88XypNDvjYNby6vw/Pb0rwert/En mZ+AW4OZPnTPI89ZPmVMLuayrD2cE86Z/il8b+gw3r3+1nKatmIkjn2so1d01QraTlMqVSsbx NrRFi9wrf+M7Q== schacon@agadorlaptop.local
  ````
  2、登陆你的github帐户。然后 Account Settings -> 左栏点击 SSH Keys -> 点击 Add SSH key
  3、然后你复制上面的公钥内容，粘贴进“Key”文本域内。 title域，你随便填一个都行。
  4、完了，点击 Add key。
  
  这样，就OK了。然后，验证下这个key是不是正常工作。
  ````
  $ ssh -T git@github.com
  \# Attempts to ssh to github
  ````
  如果，看到：
  Hi username! You've successfully authenticated, but GitHub does not # provide shell access.
  就表示你的设置已经成功了。
-
- 三、修改你本地的ssh remote url. 不用https协议，改用git 协议
  
  可以用git remote -v 查看你当前的remote url
  ````
  $ git remote -v
  origin https://github.com/someaccount/someproject.git (fetch)
  origin https://github.com/someaccount/someproject.git (push)
  ````
  可以看到是使用https协议进行访问的。
  
  你可以使用浏览器登陆你的github，在上面可以看到你的ssh协议相应的url。类似如下：
  
  git@github.com:someaccount/someproject.git
  
  这时，你可以使用 git remote set-url 来调整你的url。
  
  git remote set-url origin git@github.com:someaccount/someproject.git
  
  完了之后，你便可以再用 git remote -v 查看一下。
  
  OK。
  
  以上操作表明我们本地到github上可以实现无需输入用户名密码就可以提交文件。但是实际我们再来提交代码时仍然提示需要输入用户名密码，这是怎么回事？
  ````
  1.  \[root@client css\] \# git push origin master  
  2.  Username for 'https://github.com': yangfei2013  
  3.  Password for 'https://yangfei2013@github.com':   
  4.  remote: Invalid username or password.  
  5.  fatal: Authentication failed for 'https://github.com/yangfei2013/ghblog.git/'  
  ````
  原来git提交有两个地址一个是https://github.com/yourname/repo.git,还有一个地址是git@github.com:yourname/repo.git,如果我们配置了公钥，那么再提交代码时需要使用git@github.com:yourname/repo.git的url来提交。这样就需要我们配置这个提交的URL地址,没有修改配置之前我们通过 git config --list可以看到相关配置。
  ````
  1.  \[root@client css\]# git config --list  
  2.  user.name=yangfei2013  
  3.  user.email=yangfei5459@126.com  
  4.  core.repositoryformatversion=0  
  5.  core.filemode=true  
  6.  core.bare=false  
  7.  core.logallrefupdates=true  
  8.  remote.origin.url=https://github.com/yangfei2013/ghblog.git  
  9.  remote.origin.fetch=+refs/heads/*:refs/remotes/origin/*  
  10. branch.master.remote=origin  
  11. branch.master.merge=refs/heads/master  
  ````
  第三步、配置提交的URL，更改项目路径下.git/config文件，修改remote.origin.url
  
  
  更改之后，我们再通过git config --list查看remote.origin.url确实发生了变化
  
  
  更改之后再次提交代码，就不出现提示输入用户名和密码了。
  ````
  1.  \[root@client css\]# vi ../.git/config   
  2.  \[root@client css\]# git push origin master  
  3.  Warning: Permanently added the RSA host key for IP address '192.30.255.112' to the list of known hosts.  
  4.  Counting objects: 7, done.  
  5.  Compressing objects: 100% (3/3), done.  
  6.  Writing objects: 100% (4/4), 358 bytes | 0 bytes/s, done.  
  7.  Total 4 (delta 2), reused 0 (delta 0)  
  8.  remote: Resolving deltas: 100% (2/2), completed with 2 local objects.  
  9.  To git@github.com:yangfei2013/ghblog.git  
  10.    8dd24e8..3fb9ab9  master -> master
  ````
-