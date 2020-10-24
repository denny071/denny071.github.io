---
title: MacOS文件夹名称实现本地化方法
date: 2020-08-27 14:44:12
tags:
---
### 方法步骤

#### 1、关闭SIP
> 打开终端，输入csrutil status命令，查看SIP是否打开。如果显示：
`System Integrity Protection status: disabled.`
证明SIP已经关闭，可以跳过这一步。

> 如果SIP没有关闭，执行以下操作关闭：重启系统，按住Command (⌘)-R进入苹果的恢复系统
进入系统后，在顶部菜单栏选怎“实用工具”，打开“终端”程序，输入`csrutil disable`，完成后重启系统
如果是Catalina系统，需要再多执行一个命令`sudo mount -uw /`，重新挂载一下硬盘执行命令

#### 2、如果关闭SIP的时候就重新挂载了硬盘，应该就不用再执行了
```sh
sudo mount -uw /

cd /System/Library/CoreServices/SystemFolderLocalizations/zh_CN.lproj

# 如果没有权限的话就执行
sudo chmod -R 777 *
sudo /usr/libexec/PlistBuddy -c "Add 'Projects' string '项目'" SystemFolderLocalizations.strings


cd /System/Library/CoreServices/SystemFolderLocalizations/en.lproj
# 如果没有权限的话就执行
sudo chmod -R 777 *
sudo /usr/libexec/PlistBuddy -c "Add 'Projects' string 'Projects'" SystemFolderLocalizations.strings 

cd ~/Projects
touch .localized
pkill Finder
```

> 执行完上述命令后，就能看到效果，如果还不行就重启下系统试试。
关键点应该是对en.lproj目录下的SystemFolderLocalizations.strings文件操作，网上很多教程都是缺少了这一步。
