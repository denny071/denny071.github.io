---
title: 安装_windows10_store
date: 2020-11-14 14:42:47
tags: win10
categories: os
---


#### 1.运行管理员模式的powershell
```
cd  C:\Program Files\WindowsApps\
```
#### 2.查看当前路径
```
ls
```
#### 3.查看 Microsoft.WindowsStore 开头的目录 

```
例如 Microsoft.WindowsStore_11706.1002.9.0_x64__8wekyb3d8bbwe
```

#### 4.然后执行如下命令
```
add-appxpackage -register "C:\Program Files\WindowsApps\Microsoft.WindowsStore_11706.1002.9.0_x64__8wekyb3d8bbwe\appxmanifest.xml" -disabledevelopmentmode
```
修复成功