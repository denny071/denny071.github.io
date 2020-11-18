---
title: update与upgrade的作用及区别
categories: os
date: 2020-10-25 10:21:02
tags: linux
---

个LINUX的发行版，比如UBUNTU，都会维护一个自己的软件仓库，我们常用的几乎所有软件都在这里面。这里面的软件绝对安全，而且绝对的能正常安装。

在UBUNTU下，我们维护一个源列表，源列表里面都是一些网址信息，这每一条网址就是一个源，这个地址指向的数据标识着这台源服务器上有哪些软件可以安装使用。

编辑源命令：
```bash
sudo gedit /etc/apt/sources.list
```
在这个文件里加入或者注释（加#）掉一些源后，保存。这时候，我们的源列表里指向的软件就会增加或减少一部分。

获得最近的软件包的列表:(列表中包含一些包的信息，比如这个包是否更新过)
```bash
sudo apt-get update
```
这个命令，会访问源列表里的每个网址，并读取软件列表，然后保存在本地电脑。软件包管理器里看到的软件列表，都是通过update命令更新的。

update后，可能需要upgrade一下。
```bash
sudo apt-get upgrade
```
这个命令，会把本地已安装的软件，与刚下载的软件列表里对应软件进行对比，如果发现已安装的软件版本太低，就会提示你更新。如果你的软件都是最新版本，会提示：

升级了 0 个软件包，新安装了 0 个软件包，要卸载 0 个软件包，有 0 个软件包未被升级。

总而言之，update是更新软件列表，upgrade是更新软件。



注解：一般在执行 sudo apt-get upgrade 命令之前需要先执行一下 `sudo apt-get update `----其实和windows下的软件检测更新是一样的，需要更新的会帮你自动更新并安装好

在线直接安装的命令
```bash
sudo apt-get install 软件名称
```
`apt-get update` 指令会同步使用者端和APT 伺服器的RPM 索引清单（package list），APT 伺服器的RPM 索引清单置于base 资料夹内，使用者端电脑取得base 资料夹内的bz2 RPM 索引清单压缩档后，会将其解压置放于`/var/state/apt/lists/`，而使用者使用`apt-get install` 或`apt-get dist-upgrade` 指令的时候，就会将这个资料夹内的资料和使用者端电脑内的RPM 资料库比对，如此一来就可以知道那些RPM 已安装、未安装、或是可以升级的。