---
title: node-install-on-linux
date: 2016-06-20 15:12:30
tags: node
---
## 写在开始

去年按照小老大的博客教程 step by step 的在 linux 上装过 node，然而今年要在新申请的虚拟机上安装时还是手忙脚乱，所以还是认真记录下吧。

由于是 clean 的虚拟机所以简单的配置下方便以后的工作：

创建新的账户：

	useradd jingjing
	
为新创建的账户设置密码：

	password jingjing
	
切换到新创建的账户下面：

	su - jingjing
	
创建软件存放目录和软件安装目录：

	mkdir softwares && mkdir local
	
简单配置过后就可以安装了，在 linux 安装 node 有三种方式。
	
## 二进制文件安装

**step 1：在浏览器打开 node [download](https://nodejs.org/en/download/current/) 的页面并复制二进制文件地址。** 地址如下：

[https://nodejs.org/dist/v6.2.1/node-v6.2.1-linux-x64.tar.xz](https://nodejs.org/dist/v6.2.1/node-v6.2.1-linux-x64.tar.xz)


{% asset_img 2016-06-20-15.32.50.png %}

**step 2：进入 softwares 目录下并下载二进制文件**

	cd softwears && wget https://nodejs.org/dist/v6.2.1/node-v6.2.1-linux-x64.tar.xz
	
**step 3：解压文件**

	tar Jxf node-v6.2.1-linux-x64.tar.xz
	
**step 4：将解压后的文件移到 local 目录下**

	mv node-v6.2.1-linux-x64 ~/local
	
**step 5：验证 node 是否安装成功**

解压后的目录下有个 bin 目录，里面有我们需要的两个可执行文件 node 和 npm。我们可以可以在这个 bin 目录下执行 node 和 npm 命令。

	cd ~/local/node-v6.2.1-linux-x64/bin && ./node -v
	
**step 6：设置环境变量**

我们可以进到这个 bin 目录执行 node 和 npm 命令，但是出了这个目录就不行了，为了在外面也可以执行，需要把它设置进 PATH 环境变量。

	vim ~/.bashrc
	
然后插入：

	HOME="/home/jingjing"
	PATH="$PATH:$HOME/bin:$HOME/local/node-v6.2.1-linux-x64/bin"
	
## 源码安装

**step 1：去官网下载 source code**

	wget https://nodejs.org/dist/v6.2.2/node-v6.2.2.tar.gz
	
**step 2：解压**

	tar xvf node-v6.2.2.tar.gz
	
**step 3: 编译**

	cd node-v6.2.2/
	./configure
	make
	
**step 4: 安装**

	make install
	
**step 5：设置环境变量**

同上

## 使用 apt-get

别人说不好用，自己没有试~~~~


