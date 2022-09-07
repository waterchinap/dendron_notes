---
id: cfh42od762mrd63nsnebowg
title: Git( branch ) 的基本使用
desc: ''
updated: 1662565912899
created: 1662565912899
isDir: false
---
- [[git]] 分支( branches ) 是指在开发主线中分离出来，做进一步开发而不影响到原来主线。
  
  Git 存储的不是一系列的更改集( changeset )，而是一系列快照。当你执行一次 commit 时， Git 存储一个 commit 对象，它包含一个指针指向你当前需要提交的内容的快照。
  
  Git 中的 master 分支的功能，和其他分支一样。master 在 git 项目中常见到，是因为 git init 命令运行时默认创建一个分支，并命名为 master。
  
  创建一个新的分支，就是创建一个新的指针，用来在快照间移动。Git 通过 HEAD 指针，指向当前工作的本地分支。
  
  使用 git checkcout 命令，可以切换分支。
  
  修改文件并 commit 代码后，会移动分支的指针
  
  $ vim test.rb
  $ git commit -a -m 'update test.rb'
  
  通过 checkout 可以切换回去 master 分支。下面的命令做了两件事，一是把 HEAD 指针指向了 master 分支，二是当前工作目录的文件恢复到了 master 所指向的快照版本。也就是说 87ab2 提交的变动，在切换到 master 分支时被移除。
  
  再做一些变更和 commit 。注意，此时历史记录开始出现分叉。
  
  $ vim test.rb
  $ git commit -a -m 'make other changes'
  
  Git 中的分支，实际上是一个简单的包含 40 个字符的文件，这 40 个字符是一次提交所产生的 SHA-1 checksum。所以，在 Git 中创建和销毁一个分支的成本非常低。这个和其他大多数版本管理系统比起来，Git 无需拷贝整个项目的文件，是一个巨大的不同点。
  
  基本的分支与合并
  
  下面的例子是一个比较常见的场景，应用了分支与合并的功能。
  
  1.  在开发一个网站
  2.  创建一个分支 ( iss53 )，用于处理新的项目需求( user story )
  3.  在这个分支上，做了一些工作
  
  这时，接收到另一个紧急的问题，需要立刻修复( hotfix )
  
  　　4\. 切换到生产环境分支
  
  　　5\. 创建一个新的分支 ( hotfix )，用于修复线上问题
  
  　　6\. 测试过后，把修复分支合并到主分支上，并推送到生产环境 
  
  　　7\. 切换到原来的需求分支，继续工作
  
  最开始的状态如下
  
  
  通过 branch / checkout / commit 等操作，做到上面的第 5 步， 状态如下
  
  
  接下来，先合并 hotfix 分支，然后部署到线上环境。
  
  $ git checkout master
  $ git merge hotfix
  Updating f42c576..3a0874c
  Fast-forward
   index.html | 2 ++
   1 file changed, 2 insertions(+)
  
  上面的提示中，有 Fast-forward 字眼，表明 hotfix 分支指向的 c4 提交，是 master 分支指向的 c3 提交的祖先，因此，直接把 master 移动到 c4 即可。合并后效果关系如下
  
  
  由于 hotfix 已经合并到 master 分支，此时 master 和 hotfix 指向同一个地方，后续不在需要用到 hotfix 分支，所以可以删除。
  
  下来了可以切换到 iss53 分支继续工作，继续修改，然后提交。当修改完毕后，关系大致如下
  
  $ git checkout iss53
  Switched to branch "iss53" $ vim index.html
  $ git commit -a -m 'finished the new footer \[issue 53\]' \[iss53 ad82d7a\] finished the new footer \[issue 53\] 1 file changed, 1 insertion(+)
  
  
  接下来开始合并。
  
  $ git checkout master
  Switched to branch 'master' $ git merge iss53
  Merge made by the 'recursive' strategy.
  index.html |    1 +
  1 file changed, 1 insertion(+)
  
  这里合并没有了 Fast-forward 字眼，因为不是简单的移动分支指针。Git 采用三路合并( three-way merge ) 方式进行合并，创建了一个 commit ( c6 )，用于包含合并后的结果。三路合并方式，是指通过两个分支的最新提交( c4 和 c5 )，以及他们的共同祖先 c2，来进行分支合并。c6 是一个合并提交记录，特别之处是有两个祖先。 
  
  
  此时，你已不在需要 iss53 分支，可以删除它.
  
  基本合并冲突处理
  
  如果两个分支修改同一个文件的同一个部分，例如同一行代码，Git 不知道如何合并，认为这是一个冲突。例如你在 iss53 和 hotfix 分支都修改了 index.html 文件的同一个部分，合并 iss53 到已包含 hotfix 的 master 分支时，效果如下
  
  $ git merge iss53
  Auto-merging index.html
  CONFLICT (content): Merge conflict in index.html
  Automatic merge failed; fix conflicts and then commit the result.
  
  此时，自动合并暂停，需要手动合并。 git status 显示冲突了的文件
  
  
  $ git status
  On branch master
  You have unmerged paths.
    (fix conflicts and run "git commit")
  
  Unmerged paths:
    (use "git add &lt;file&gt;..." to mark resolution)
  
      both modified:      index.html
  
  no changes added to commit (use "git add" and/or "git commit -a")
  
  
  Git 在冲突的文件中添加标准的冲突解决标识。
  
  这个表明，HEAD 版本的代码是 ======= 以上部分，iss53 的版本是 ======= 以下部分。
  
  开打 index.html 文件，修改成自己想要的版本，并剔除 &lt;<<<<<< ======= &gt;>>>>>> 标识，然后用 git add 标识冲突已接近，然后git commit 提交解决冲突后的版本。