---
title: 基于crontab的mysql数据库备份
date: 2020-08-27 14:44:22
tags:
---
#### 创建目录
```
cd /home
mkdir backup
cd backup
```
#### 创建备份shell脚本
```
vim backup_demoDatabase.sh
```
#### 备份脚本（未压缩）
```bash
#!/bin/bash
mysqldump -uusername -ppassword > demoDatabase > /home/backup/demoDatabase_$(date + %Y%m%d_%H%M%S).sql
```
#### 备份脚本（压缩）
```base
mysqldump -uusername -ppaswword > demoDatabase > gzip > /home/backup/demoDatabase_$(date + %Y%m%d_%H%M%S).sql.gz
```
> `username` 为用户名
> `password` 为密码
> `demoDatabase` 为数据库名

#### 添加可执行权限
```bash 
chmod u+x backup_demoDatabase.sh
```
#### 添加计划任务
```bash
crontab -e
```
##### 编辑内容
```bash 
*/1 * * * * /home/backup/backup_demoDatabase
```
> 每一分钟执行一次shell脚本“/home/backup/bkDatabaseName.sh”


> 如果失，败可查看失败日志
```bash 
tail -f /var/log/cron
```