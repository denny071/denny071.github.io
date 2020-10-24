---
title: Docker安装gitlab
date: 2020-08-27 14:42:02
tags:
---
 
```
  sudo apt install docker.io 
 ```
#### 添加加速器
```
curl -sSL https://get.daocloud.io/daotools/set_mirror.sh | sh -s http://f1361db2.m.daocloud.io
```
#### 创建初始目录
```
sudo mkdir -m 755 -p /srv/gitlab60/config /srv/gitlab60/logs /srv/gitlab60/data
```

#### 创建并运行容器
```
sudo docker run -d -h 10.0.0.252  -p 6080:80 -p 60443:443 -p 6022:22 --name gitlab60 --restart always -v /srv/gitlab60/config:/etc/gitlab -v /srv/gitlab60/logs:/var/log/gitlab -v /srv/gitlab60/data:/var/opt/gitlab gitlab/gitlab-ce:latest
```
#### 命令详解
| 参数 | 说明 |
| --- | --- |
| run | 启动容器 |
|  -d| 后台启动 |
| -h 10.0.0.252 |  设置容器主机地址|
| -p 6080:80 -p 60443:443 -p 6022:22 | 端口映射 宿主端口：容器端口 |
| --name gitlab60 |  容器名称|
|restart always  | 停止重启 |
| -v /srv/gitlab60/config:/etc/gitlab -v /srv/gitlab60/logs:/var/log/gitlab -v /srv/gitlab60/data:/var/opt/gitlab |目录挂载 宿主目录：容器目录|
|gitlab/gitlab-ce:latest| 容器名称：版本号 |

> 需要等待几分钟进行初始化，此时可以查看gitlab日志

#### 修改gitlab配置文件
```
sudo docker exec -it gitlab60 vi /etc/gitlab/gitlab.rb
```

|  参数| 说明 |
| --- | --- |
| exec | 进入容器|
| -it |  显示容器信息|
|  gitlab60| 容器名称 |

#### 编辑文件
```
vi /etc/gitlab/gitlab.rb
```
#### 查看gitlab日志
```
sudo docker logs -f gitlab60
```

| 参数 | 说明 |
| --- | --- |
| logs |  容器日志|
|  -f|  动态显示 |
| gitlab60 | 容器名称 |


#### 进入gitlab容器
```
sudo docker exec -it gitlab60 /bin/bash
```

|  参数|  说明|
| --- | --- |
| exec |  进入容器|
|  -it| 显示容器信息 |
| gitlab60 | 容器名称 |
| /bin/bash | 进入bash |

#### 进入容器后可以执行一下命令

**启动容器**
```
sudo gitlab-ctl start
```
**停止容器**
```
sudo gitlab-ctl stop
```
**重启容器**
```
sudo gitlab-ctl restart
```
