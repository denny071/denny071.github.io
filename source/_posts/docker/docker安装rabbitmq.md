---
title: docker安装rabbitmq
categories: docker
date: 2020-10-26 10:00:36
tags: rabbitmq
---



### 获取镜像

```bash
#指定版本，该版本包含了web控制页面
docker pull rabbitmq:management
```

### 运行镜像

```bash
#方式一：默认guest 用户，密码也是 guest
docker run -d --hostname my-rabbit --name rabbit -p 15672:15672 -p 5672:5672 rabbitmq:management

#方式二：设置用户名和密码
docker run -d --hostname my-rabbit --name rabbit -e RABBITMQ_DEFAULT_USER=user -e RABBITMQ_DEFAULT_PASS=password -p 15672:15672 -p 5672:5672 rabbitmq:management
```

### 访问UI页面

```bash
http://localhost:15672/
```

![1449147-20190720164053275-1039971470](docker%E5%AE%89%E8%A3%85rabbitmq/1449147-20190720164053275-1039971470.png)