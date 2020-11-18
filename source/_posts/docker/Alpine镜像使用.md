---
title: Alpine镜像使用
categories: docker
date: 2020-11-01 09:46:22
tags: apline
---

## Alpine镜像使用

alpine镜像在构建镜像过程中作为基础镜像占比越来越高，下面是alpine镜像中包管理工具apk使用相关示例：

1. apk --help命令查看完整的包管理命令。
2. apk update：从远程镜像源中更新本地镜像源索引
3. apk add：安装PACKAGES并自动解决依赖关系，也可以从第三方仓库添加软件包
```bash
apk add  nmap vim

apk add --no-cache mysql-client

apk add docker --update-cache --repository http://mirrors.ustc.edu.cn/alpine/v3.4/main/ --allow-untrusted
```
安装指定版本软件包:
```bash 
apk add  nmap=7.70-r3
```
4. apkupgrade 升级软件包
```bash 
 apk upgrade （升级所有软件报）
 apk add --upgrade nmap（指定软件升级）
```
5. apk del 卸载并删除PACKAGES
```bash
apk del nmap
```
6. apk search 命令搜索可用软件包，-v 参数输出描述内容，支出通配符，-d 或 –description 参数指定通过软件包描述查询。
```bash
  apk search #查找所有可用软件包
  apk search -v #查找所有可用软件包及其描述内容
  apk search -v 'acf*' #通过软件包名称查找软件包
  apk search -v -d 'docker' #通过描述文件查找特定的软件包
```
7. apk info：列出PACKAGES或镜像源的详细信息
```bash
  apk info #列出所有已安装的软件包
  apk info -a zlib #显示完整的软件包信息
  apk info --who-owns /sbin/lbu #显示指定文件属于的包
```
8. 清理akp缓存:rm -rf /var/cache/apk/*
9. apk使用阿里云的源
```bash
sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories
```
10. 添加用户
```bash
addgroup -g 1000 -S demo
adduser demo -D -G demo -u 1000
```
11. alpine内编译安装lrzsz
```bash
apk update
apk add wget gcc g++ make
wget https://ohse.de/uwe/releases/lrzsz-0.12.20.tar.gz
tar -xf lrzsz-0.12.20.tar.gz
cd lrzsz-0.12.20/
./configure
make; make install
ln -s /usr/local/bin/lrz /usr/local/bin/rz
ln -s /usr/local/bin/lsz /usr/local/bin/sz
```



