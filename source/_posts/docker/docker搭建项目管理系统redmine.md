---
title: docker搭建项目管理系统redmine
categories: docker
date: 2020-10-27 10:14:50
tags: redmine
---

Redmine是一个跨平台的项目管理系统，它通过项目的形式把成员、任务、文档、讨论及各种形式的资源组织在一起。这篇文章记录使用Docker搭建Redmine系统的工程。

使用sameersbn/redmine镜像搭建Redmine服务，项目地址为：

```bash
https://github.com/sameersbn/docker-redmine
```

安装指令如下：

（1）启动postgresql

```bash
docker run --name=postgresql-redmine -d --env='DB_NAME=redmine_production' --env='DB_USER=redmine' --env='DB_PASS=password' sameersbn/postgresql:9.4-12
```

结果如下：![B401FDDC-A680-45D3-81D0-B790A3A49216](docker%E6%90%AD%E5%BB%BA%E9%A1%B9%E7%9B%AE%E7%AE%A1%E7%90%86%E7%B3%BB%E7%BB%9Fredmine/B401FDDC-A680-45D3-81D0-B790A3A49216.png)

（2）启动redmine

```bash
docker run --name=redmine -d --link=postgresql-redmine:postgresql --publish=10083:80 --env='REDMINE_PORT=10083' sameersbn/redmine:3.2.0-4
```

结果如下：

![09FC17E6-BA0D-46D9-8A57-BC3386D4DE45](docker%E6%90%AD%E5%BB%BA%E9%A1%B9%E7%9B%AE%E7%AE%A1%E7%90%86%E7%B3%BB%E7%BB%9Fredmine/09FC17E6-BA0D-46D9-8A57-BC3386D4DE45.png)

（3）测试Redmine

在Docker指令中，把对外服务的端口映射到了10083，可以通过IP+端口进行访问。

获取IP地址：

```bash
docker-machine ip
```

可以获得我的IP地址是：192.168.99.100

所以可以通过地址：`http://192.168.99.100:10083`， 进行访问，界面如下：

![1F45C6CF-FC4A-4463-87D4-D26771CDD182-5665839](docker%E6%90%AD%E5%BB%BA%E9%A1%B9%E7%9B%AE%E7%AE%A1%E7%90%86%E7%B3%BB%E7%BB%9Fredmine/1F45C6CF-FC4A-4463-87D4-D26771CDD182-5665839.png)

