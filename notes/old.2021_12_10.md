---
id: plkxlcfdcf7nr079cv8nx96
title: '2021_12_10'
desc: ''
updated: 1662566166174
created: 1662566166174
isDir: false
---
- [[archlinux]]安装
	- 刻录镜像时，注意可以选择gpt, uefi模式，这样可以统一管理多系统启动。
	- 查看启动模式：`ls /sys/firmware/efi/efivars`
	- 联网：直接用lan不需要操作。
		- wifi：使用`iwctl`
	- 更新系统时钟：`timedatectl set-ntp true`
	- 准备磁盘：
		- 使用uefi模式，只需要准备一个磁盘用于安装root分区。`fdisk /dev/sda`
		- 如果已经有uefi分区，只需要挂上去就可以，不需要再准备。如果没有，则需要准备。
		- 没有必要准备交换分区，安装完以后用交换文件。
	- 格式化：
		- `mkfs.ext4 /dev/sdb2` for root
		- `mkfs.fat -F 32 /efi_system_partition`: for efi 使用已有的efi分区时不需要格式化了。
	- 挂载系统
		- `mount /dev/sdb1 /mnt`
		- `mkdir /mnt/boot`
		- `mount /dev/efi_system_partition /mnt/boot`
	- 安装
		- 选择镜象：`reflect -c China --rank rate --save /etc/pacman.d/mirrorlist`
		- 安装基础包：`pacstrap /mnt base linux linux-firmware base-devel dhcpcd`最重要是把联网的相关包安装上去。
	- 配置
		- `genfstab -U /mnt >> /mnt/etc/fstab`
		- `arch-chroot /mnt`
		- `ln -sf /usr/share/zoneinfo/Region/City /etc/localtime`
		- `hwclock --systohc`
		- 本地化
			- 编辑`/etc/locale.gen`把中文和英文取消注释
			- 运行`locale-gen`
			- ```
			  /etc/locale.conf
			  LANG=en_US.UTF-8
			  ```
		- `/etc/hostname`设置计算机名
		- 设置root密码：passwd
	- 安装boot loader
		- `pacman -S grub efibootmgr os-prob intel-ucode`
		- `grub-install --target=x86_64-efi --efi-directory=esp --bootloader-id=GRUB`
		- `grub-mkconfig -o /boot/grub/grub.cfg`
		- 参考os-prob的说明，把其他系统的启动器扫出来。
	- 退出重启
	- 安装后的必要操作
		- 输入法：fcitx5，fcitx5-configtool, fcitx5-material-color
		- 中文字体：sarasa gothic
		- 添加清华源：在`/etc/pacman.conf`添加两行
		  ```
		  [archlinuxcn]
		  Server = https://mirrors.tuna.tsinghua.edu.cn/archlinuxcn/$arch
		  ```
			- 运行`archlinuxcn-keyring`
			-
		- [[python]] :
			- 安装python, python-pip, python-pipx(用于全局使用的python程序，不会因为滚动升级导致程序无法运行)
			- 添加清华源：
			  ```
			  pip install pip -U
			  pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple
			  ```
-
-