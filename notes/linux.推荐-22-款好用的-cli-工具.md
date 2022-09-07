---
id: lgspdx4sby9vhfpbn92uk1f
title: 推荐 22 款好用的 CLI 工具
desc: ''
updated: 1662565912905
created: 1662565912905
isDir: false
---
- 作者根据多年的终端使用经验，详细介绍了一些实用的 CLI 工具，希望它们能帮读者提高生产力。
  
  我大部分的时间都花费在终端的使用上，我觉得有必要给大家推荐一下比较好用的终端工具。先给大家列个推荐清单，如下图。
  
  
  #linux **高频 CLI 工具推荐**
### 1、fish shell

Shell- 毋庸置疑，在终端中，Shell 是使用最频繁也最重要的工具。过去，我曾经使用过 Bash 和 Z Shell，而如今，我正在使用的是 Fish Shell。这是一个非常优秀的终端 Shell 工具，拥有许多开箱即用的功能，例如语法自动推荐补全、语法高亮显示或使用快捷键在最近访问的文件夹之间来回切换。

一方面，它非常适合初学者使用，因为使用者无需进行任何设置。另一方面，由于它使用的脚本语法与其他 Shell 有所差异，因此通常用户不能把拷贝自网上的脚本直接粘贴使用。你必须将不兼容的命令更改为合法的 Fish 脚本，或者启动一个 Bash 会话以运行 Bash 脚本。

[https://fishshell.com/docs/cu...](https://link.zhihu.com/?target=https%3A//fishshell.com/docs/current/index.html%23syntax-overview)

我能理解这种更改背后的原因（毕竟 Bash 脚本不是易于用户使用的语言），但这种不兼容丝毫没有给我带来任何好处。我平时很少编写 Bash / Fish 脚本，所以经常遗忘这些语法，因此每次要使用这些脚本时我总是必须从头开始重新学习它。与 Bash 脚本相比，Fish 脚本的资源相对更少。我通常不会去阅读文档，重复造轮子，而是从 StackOverflow 复制粘贴现成的脚本拿来即用。

虽然前面我提到了 Fish Shell 的几个缺点，但是我还是会推荐你去用一下，因为切换 Shell 工具十分简单，所以很值得你去尝试一下。特别是当你懒得自己去配置 Shell，并希望通过最少的配置就能获得很好的使用效果的时候，那就更不要错过它了。

**Fish插件**

你可以自己添加相关插件来扩展 Fish Shell 的功能。最简单的安装插件的方法就是使用插件管理工具，比如 Fisher、Oh My Fish 或者 fundle。现在，我使用的插件管理工具是 Fisher，我用它安装管理了三个插件：

1.  franciscolourenco/done ——在长时间运行的脚本完成后发送通知。
2.  evanlucas/fish-kubectl-completions——1个自动补全 kubectl(Kubernetes command line tool) 命令的插件。
3.  fzf——将 fzf 工具与 Fish 集成在一起的插件。

过去，我有使用很多的插件（比如 rbenv、pyenv、nodenv、fzf、z），但是我改用其他工具以避免影响我的 Shell 的运行速度（这是我过去使用 Z shell 所得到的一个教训）。

下载地址：[https://fishshell.com/](https://link.zhihu.com/?target=https%3A//fishshell.com/)
- ### 2、Starship
  
  如果必须要从本篇文章中选择一个我最喜欢的终端工具——那非 Starship 莫属。Starship 可以适用于任何 Shell。你只需要安装它，然后在相应的配置文件`.bashrc`/`.zshrc`/`config.fish`添加一行配置，剩下的工作交给它来完成就好了。
	- 它可以做到：
		- 根据你是否在代码仓库中添加了新文件、是否修改了文件、是否暂存了文件等情况，用相应的符号表示 git 仓库的状态。
		- 根据你所在的 Python 项目目录，展示 Python 的版本号，这也适用于 Go/Node/Rust/Elm 等其他编程语言环境。
		- 展示上一个命令执行所用的时间，指令运行时间必须在毫秒级别。
		- 如果上一个命令执行失败，会展示相应的错误提示符。
		- 还有不计其数的其他信息可以展示。但是，它能以更加友好的形式智能地给你呈现！比如，如果你不在 git 存储库中，它将隐藏 git 信息。如果您不在 Python 项目中，则不会有 Python 版本信息，因为显示它没有什么意义。它永远不会给你展示多余信息，始终保持终端的美观，优雅和简约。
		  
		  Starship 的运行速度怎么样呢？它是用 Rust 编写的，尽管功能如此之多，但仍然比我以前使用的所有提示工具都要快！我对提示信息非常洁癖，因此我经常破解自己的版本。我会根据现有的提示找到对应的功能代码，然后将其粘组合在一起，以确保 Starship 只有我需要的功能以保持其快速运行。“外部工具永远无法比我精心制作的提示工具更快！” 这就是我对 Starship 持怀疑态度的原因。
		  
		  下载地址：[https://starship.rs/](https://link.zhihu.com/?target=https%3A//starship.rs/)
### 3、z

“z”可以让你快速地在文件目录之间跳转。它会记住你访问的历史文件夹，经过短暂的学习后，你就可以使用`z path_of_the_folder_name`命令在目录之间跳转了。


比如，如果我经常访问 `~/work/src/projects`，我只需要运行 `z pro` ，就可以立马跳转到那里。z 的原理参考了 frecency 算法——一个基于统计 frequency 和 recency 进行分析的算法。如果它存储了你不想使用的路径文件夹，你随时可以手动将其删除。它提高了我在常用的不同文件路径之间频繁切换的效率，帮我节省了键盘击键次数以及大量的路径记忆。

下载地址：[https://github.com/rupa/z](https://link.zhihu.com/?target=https%3A//github.com/rupa/z)
### 4、fzf

fzf— fuzzy finder，即模糊查找器。它是一种通用工具，可让你使用模糊搜索来查找文件、历史命令、进程、git 提交等。你键入一些字母，它会尝试匹配结果列表中任何位置的字母。输入的字母越多，结果也就越准确。你可能在其他的代码编辑器中有过这种类型的搜索使用体验——当你想打开某个文件时，只键入文件名的一部分而不用输入完整路径就能进行查找——这就是模糊搜索。

我通过 fish fzf 插件插件使用它，因此我可以搜索命令历史记录或快速打开文件。这是可以每天为我节省不少时间的一个非常棒的工具。

[https://github.com/jethrokuan...](https://link.zhihu.com/?target=https%3A//github.com/jethrokuan/fzf)

下载地址：[https://github.com/junegunn/fzf](https://link.zhihu.com/?target=https%3A//github.com/junegunn/fzf)
### 5、fd

类似于系统自带的 `find` 命令，但使用起来更简单，查找速度更快，并且具有良好的默认设置。

不管你想找到一个名为“invoice”的文件，但是不确定文件的扩展名，还是查找一个存放所有 invoice 的目录，而不单是一个文件。你可以撸起袖子，开始为 find 命令编写那些复杂的正则表达式，也可以直接命令行运行 `fd invoice`。反正对我来说，我只选择最简单的那个。

默认情况下，fd 会忽略隐藏的以及在`.gitignore`列出的文件和目录。大多数时候，这也是我们想要的，但是在极少数特殊情况下，如果需要禁用此功能时，我会给该命令设置一个别名：`fda='fd -IH'`。

你会发现，fd 命令输出的颜色配置很漂亮，而且根据基准测试（上述 GIF），它的执行速度甚至比`find 命令`的还要快。

下载地址：[https://github.com/sharkdp/fd](https://link.zhihu.com/?target=https%3A//github.com/sharkdp/fd)
### 6、ripgrep

上图为 grep（左）与 rg（右）命令执行时的对比。

与上述`fd`指令类似，`ripgrep`是`grep`命令的替代方法， 不过`ripgrep`的执行速度更快，而且具有健全的默认配置以及丰富的彩色输出。

它同样会跳过被`.gitignore`忽略以及隐藏的文件，因此如果有特殊需要，我们可以设置指令别名：`rga ='rg -uuu'`。它会禁用所有智能筛选，并使`ripgrep`的表现与标准的 grep 指令一致。

下载地址：[https://github.com/BurntSushi...](https://link.zhihu.com/?target=https%3A//github.com/BurntSushi/ripgrep)
### 7、htop 和 glances

在 Linux 或 Mac 上显示进程运行状态信息最常用工具是我们熟悉的`top`，它是每位系统管理员的好帮手。而且，即使是像我一样主要从事网络开发，查看计算机的运行状况也很有用。你知道，只是看一下当前到底是 Docker 进程还是 Chrome 进程吃掉了你所有的 RAM，应该如何做吗？

`htop`工具是`top`工具的绝佳替代品。

`top`工具是非常基础的监控工具，提供的功能有限，因此很多人转去使用 htop。`htop`比起`top`，优势很明显——除了功能更加完善以外，它的色彩搭配也很丰富，整体上使用起来更加友好。


借助 glances，还可以让你一目了然地快速了解系统当前状态。

glances 是`htop`的补充工具。除了列出所有进程及其 CPU 和内存使用情况之外，它还可以显示有关系统的其他信息，比如：
	- 网络及磁盘使用情况
	- 文件系统已使用的空间和总空间
	- 来自不同传感器（例如电池）的数据
	- 以及最近消耗过多资源的进程列表
	- 我选择使用`htop`来筛选和终止进程，因为对我来讲，效率提高了不少，我也使用 `glances`可以快速浏览一下计算机的运行状况。它提供 API 接口、Web UI 以及支持各种导出格式，因此你可以将系统监视提高到一个新 Level。因此我在这里强烈推荐一波！
	  
	  htop 下载地址：[https://hisham.hm/htop/](https://link.zhihu.com/?target=https%3A//hisham.hm/htop/)
	  
	  glances 下载地址：
	  
	  [https://nicolargo.github.io/g...](https://link.zhihu.com/?target=https%3A//nicolargo.github.io/glances/)
### 8、virtualenv 和 virtualfish

Virtualenv 是用于在 Python 中创建虚拟环境的工具（比起内置的`venv`模块，我更喜欢 Virtualenv）。


VirtualFish 是 Fish Shell 的虚拟环境管理器（如果你不使用 Fish Shell，请查看 virtualenvwrapper）。它提供了许多命令来执行快速创建、列出或删除虚拟环境等操作。

virtualenv 下载地址：

[https://pypi.org/project/virt...](https://link.zhihu.com/?target=https%3A//pypi.org/project/virtualenv/)

virtualfish 下载地址：

[https://github.com/justinmaye...](https://link.zhihu.com/?target=https%3A//github.com/justinmayer/virtualfish)
### 9、pyenv、nodenv 和 rbenv

pyenv 可以轻松实现 Python 版本的切换。


Pyenv、nodenv 和 rubyenv 是用于管理计算机上不同版本的 Python、Node 和 Ruby 的工具。

假设你要在计算机上安装两个版本的 Python。比如，你正在从事两个不同的 Python 项目，或者因为特殊情况仍然需要使用 Python2。不同 Python 版本在电脑上管理很复杂。你需要确保不同的项目具有正确版本的软件依赖包。如果你不小心的话，很容易弄乱这种脆弱的配置并被其他软件包使用的二进制文件所覆盖。

该工具为版本管理提供了很多帮助，并将这一噩梦变得易于管理。它可以全局或“按文件夹”切换 Python 版本，而且每个版本都是相互隔离的。

我最近找到了一种名为 asdf 的工具，该工具可以将 pyenv、nodenv、rbenv 及其他 env 进行统一管理。它提供了几乎所有编程语言的版本管理，下次我需要为编程语言设置版本管理器时，一定会尝试使用一下。

pyenv 下载地址：[https://github.com/pyenv/pyenv](https://link.zhihu.com/?target=https%3A//github.com/pyenv/pyenv)

nodenv 下载地址：[https://github.com/nodenv/nodenv](https://link.zhihu.com/?target=https%3A//github.com/nodenv/nodenv)

rbenv 下载地址：[https://github.com/rbenv/rbenv](https://link.zhihu.com/?target=https%3A//github.com/rbenv/rbenv)
### 10、pipx

Virtualenv 解决了 Python 程序包管理中的许多问题，但是还有一个方案可以解决。如果我想在全局环境下安装 Python 软件包（比如它是一个独立的工具，正如前面提到的`glances` 工具），那么我会遇到全局安装带来的问题。在虚拟环境之外安装软件包不是一个好主意，将来可能会导致意想不到的问题。另一方面，如果我决定使用虚拟环境，那么每次我要运行程序时都需要激活该虚拟环境。这也不是最方便的解决方案。


事实证明，`pipx`工具可以解决上面提到的问题。它将 Python 软件依赖包安装到单独的环境中（因此不会存在依赖项冲突的问题）。与此同时，这些工具提供的 CLI 命令在全局环境内也可用。因此，我无需激活任何环境——`pipx`会帮我完成这个操作！

如果你想了解有关 Python 工具的更多信息并想了解如何使用它们，我为 PyCon 2020 会议制作了一个名为“现代 Python 开发人员工具包”的视频。


这是一个长达两个小时的视频教程，内容涉及如何设置 Python 开发环境，要使用的工具以及如何从头开始制作 TODO 应用程序（包括测试和文档）。你可以在 YouTube 上进行观看。

[https://www.youtube.com/watch...](https://link.zhihu.com/?target=https%3A//www.youtube.com/watch%3Fv%3DWkUBx3g2QfQ)

pipx 下载地址：

[https://github.com/pipxprojec...](https://link.zhihu.com/?target=https%3A//github.com/pipxproject/pipx)
### 11、ctop 和 lazydocker


ctop 的实时监控示例

当你使用 Docker 并对其监控时，这两个工具会很有帮助。`ctop`是 Docker 容器的顶级接口。它可以为你：
- 展示正在运行和已停止的容器列表。
- 展示统计信息，例如内存、CPU 使用率以及针对每个容器的其他详细信息窗口（例如绑定的端口等其他信息）。
- 提供快捷菜单，方便快速停止、杀掉指定容器进程或显示给定容器的日志。
  
  这比你尝试从`docker ps`命令中找出所有这些信息要方便多了。
  
  
  `lazydocker`是我最喜欢的 Docker 工具
  
  如果你认为`ctop`很酷，请你尝试使用 lazydocker 后再做决定！它是一个非常成熟的拥有终端 UI 界面的工具，提供了非常丰富的功能用于管理 Docker。这是我最喜欢的 Docker 管理工具！
  
  ctop 下载地址：[https://github.com/bcicen/ctop](https://link.zhihu.com/?target=https%3A//github.com/bcicen/ctop)
  
  lazydocker 下载地址：
  
  [https://github.com/jesseduffi...](https://link.zhihu.com/?target=https%3A//github.com/jesseduffield/lazydocker)
  
  **低频 CLI 工具推荐**
  
  除了几乎每天都在使用的工具以外，我多年来还收集了一些给力的工具，这些工具对于一些特定需求非常好用。比如有的终端工具可以用来将终端操作记录成 GIF（并且可以让你在 GIF 中暂停和复制文本！），还有的终端工具可以用于列出目录结构、连接数据库等，下面我会一一介绍。
### 12、Homebrew


如果你使用的是 Mac，那我就无需再介绍 Homebrew 了。它是 macOS 上被业界普遍认可的软件包管理器。对了，它还有一个称为 Cakebrew 的 GUI 版本软件，如果感兴趣你可以尝试一下。

下载地址：[https://brew.sh/](https://link.zhihu.com/?target=https%3A//brew.sh/)
### 13、asciinema


`asciinema`是可用于记录终端会话的工具。但是，与录制 GIF 不同，它可以让用户选择并复制这些录制中的代码！

这对于录制编码教程来说十分好用。你应该遇到那种尴尬的情况——当你准备跟着视频教程在终端中敲巨长的命令，但是讲师并为你提供这个代码段，你不得不花费很长的时间去整理这些冗长的命令。`asciinema`录制的内容，支持直接复制，十分给力。

下载地址：[https://asciinema.org/](https://link.zhihu.com/?target=https%3A//asciinema.org/)
### 14、colordiff 和 diff-so-fancy


我很少在终端中使用`diff`操作（比较两个文件之间的差异），但是如果你需要执行这个操作，可以放弃使用`diff`命令，而是使用 `colordiff`。`colordiff`输出可以高亮显示，因此在查看文件差异内容时要方便得多，而不是在`diff`命令输出内容下，费力地查看所有的“ &lt;”和“&gt;”符号来对比文件差异。

如果你觉得还不够，那么我推荐给你 diff-so-fancy。它是比`colordiff`更友好的一个差异对比工具。


它通过以下方式进一步改善了文件内容差异展示的外观：
- 突出显示每一行中差异的单词，而不是整行
- 简化变更文件的标题
- 去除 \+ 和 \- 符号（颜色差异展示就够了）
- 清楚地指出新行和删除的空行
  
  colordiff 下载地址：[https://www.colordiff.org/](https://link.zhihu.com/?target=https%3A//www.colordiff.org/)
  
  diff-so-fancy 下载地址：[https://github.com/so-fancy/d...](https://link.zhihu.com/?target=https%3A//github.com/so-fancy/diff-so-fancy)
### 15、tree

你可以通过`brew install tree`安装该工具。如果要查看给定目录的内容，那么 tree 是执行此操作的必备工具。它能以漂亮的树状结构显示所有子目录及文件：

```
$ tree .
.
├── recovery.md
├── README.md
├── archive
├── automator
│   ├── Open Iterm2.workflow
│   │   └── Contents
│   │       ├── Info.plist
│   │       ├── QuickLook
│   │       │   └── Thumbnail.png
│   │       └── document.wflow
│   └── Start Screen Saver.workflow
├── brew-cask.sh
```
### 16、bat


类似于在终端中常用的用于显示文件内容的`cat`命令，但是`bat`效果更佳。

它增加了语法高亮显示，git gutter 标记（如果适用），自动分页（如果文件很大）等功能，并且使得输出的内容阅读起来更加友好。

bat 下载地址：[https://github.com/sharkdp/bat](https://link.zhihu.com/?target=https%3A//github.com/sharkdp/bat)
### 17、httpie


如果你需要发送一些 HTTP 请求，但发现使用`curl`不够直观，那么请尝试一下`httpie`。这是一款非常好用的`curl`替代工具。合理的默认配置以及简洁的语法使它更易于使用，命令返回也是彩色输出，甚至支持为不同类型的身份验证安装相应的插件。

httpie 下载地址：[https://httpie.org/](https://link.zhihu.com/?target=https%3A//httpie.org/)
### 18、tldr

简化版的命令帮助手册。“man pages” 包含了 Linux 软件的手册，这些手册解释了如何使用给定的命令。你可以尝试运行`man cat`或`man grep`来查看相关命令的帮助手册。它们描述的非常详细，有时可能难以掌握。因此，`tldr`社区的目的，就是将每个命令的帮助手册进行简化，方便用户查阅。

`tldr`适用于几乎所有的受欢迎的软件。正如我提到的，这是社区的努力和功劳，虽然不太可能包含所有的软件的简化帮助手册。但是当某个帮助手册被纳入管理并起作用时，它提供的信息通常就是你要查找的内容。

比如，如果你要创建一些文件的 gzip 压缩存档，`man tar`可以为你提供可能的参数选择。而`tldr tar`会列出一些我们常见的示例——如图所示，第二个示例正是你要执行的操作：


“man pages”展示的信息太全面了，但是很多时候使用`tldr`可以更快地帮你找到特定信息，这才是用户真正想要的。

tldr 下载地址：[https://tldr.sh/](https://link.zhihu.com/?target=https%3A//tldr.sh/)
### 19、exa


`exa`是`ls`命令的一个可替代方案。

它色彩艳丽，还可以显示 git 状态等其他信息，自动将文件大小转换为方便人们阅读的单位，并且所有这些都保持与`ls`几乎相同的执行速度。虽然我很喜欢这个工具并推荐给你们，但由于某种原因，我仍然坚持使用 ls。

exa 下载地址：[https://the.exa.website/](https://link.zhihu.com/?target=https%3A//the.exa.website/)
### 20、litecli 和 pgcli


这是我首选的 SQLite 和 PostgreSQL CLI 的解决方案。借助自动提示和语法突出显示，它们比默认的`sqlite3`和`psql`工具要好用很多。

litecli 下载地址：[https://litecli.com/](https://link.zhihu.com/?target=https%3A//litecli.com/)

pgcli 下载地址：[https://www.pgcli.com/](https://link.zhihu.com/?target=https%3A//www.pgcli.com/)
### 21、mas


`mas`是一个用于从 App Store 安装软件的 CLI 工具。我目前为止，我仅仅使用过它一次——设置我的 Macbook 电脑软件。将来，我也将使用它来设置我的下一台 Macbook。`mas`可让你自动在 macOS 中安装软件。它解放了你大量的点击操作。而且，鉴于你正在阅读这篇有关 CLI 工具的文章，所以我大胆地认为，大家都和我一样，不喜欢无聊的单击操作。

我在“灾难修复”脚本中保留了从 App Store 安装的应用程序列表。如果我的电脑真的发生了什么意外情况，我希望能够以最小的代价重新安装所有内容。

mas 下载地址：[https://github.com/mas-cli/mas](https://link.zhihu.com/?target=https%3A//github.com/mas-cli/mas)
### 22、ncdu


这是在终端进行磁盘分析时使用的工具，它使用起来简单快捷。当我需要释放一些硬盘空间时，会默认使用这款工具。

ncdu 下载地址：[https://dev.yorhel.nl/ncdu](https://link.zhihu.com/?target=https%3A//dev.yorhel.nl/ncdu)
### 23、总结

以上推荐工具清单确实很长，但是我希望有一些工具真的能够带给你方便，提高你的生产力。`fd`、`ripgrep`或`httpie`等工具可能是你以前熟悉的工具的改进版本。这些工具的改进版本除了更易于使用之外，它们还提供更友好的输出，执行速度甚至更快。所以，我们要多多尝试并接受新的事物，不要仅仅因为大家都在使用旧工具而只局限在旧工具的使用上。事物都是在向前发展的，穷则变，变则通，通则久。大家一起共勉。