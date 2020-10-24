---
title: Docker简易教程
date: 2020-08-27 14:41:47
tags:
---
# Docker简介
## 为什么会有docker出现
&emsp;&emsp;一款产品从开发到上线, 从操作系统, 到运行环境,再到应用配置. 作为开发+ 运维之间的协作我们需要关心很多东西, 这也是很多互联网公司都不得不面对的问题, 特别是各种版本迭代之后, 不同版本环境的兼容, 对运维人员都是考验.
&emsp;&emsp;Docker之所以发展如此迅速, 也是因为它对此给出了一个标准化的解决方案.
&emsp;&emsp;环境配置如此麻烦, 换一台机器,就要重来一次, 费力费时. 很多人想到, 能不能从根本上解决问题, <font color=red>软件可以带环境安装?</font> 也就是说, <font color=red>安装的时候, 把原始环境一模一样地复制过来. 开发人员利用Docker可以消除写作编码时 " 在我的机器上可正常工作" 的问题</font>
&emsp;&emsp;之前在服务器配置了一个应用的运行环境, 要安装各种软件, 就拿电商项目来说, Java/Tomcat/MySQL/JDBC驱动包等. 安装和配置这些东西有多麻烦就不用说了, 它还不能夸平台. 加入我们是在Windows上安装的这些环境, 到了Linux又得重新装. 并且就算不跨操作系统, 换另一台同样操作系统的服务器, 要移植这些应用也是非常麻烦的.
&emsp;&emsp;传统上认为,软件编码开发/测试结束后, 所产出的成果即是程序或是能编译执行的二进制字节码等(java为例). 而为了让这些程序可以顺利执行, 开发团队也得准备完整的部署文件, 让运维团队得以部署应用程式, <font color=red>开发需要清楚的告诉运维部署团队,用的全部配置文件+所有软件环境. 不过, 即便如此, 仍然常常发生部署失败的状况.</font> Docker镜像的设计,<font color=red>使得Docker得以打破过去[程序即应用]的观念. 透过镜像(images)将作业系统核心除外, 运作应用程式所需要的系统环境, 由下而上打包, 达到应用程式跨平台间的无缝接轨运作.</font>

## 理念
&emsp;&emsp;Docker是基于Go语言实现的开源项目.
&emsp;&emsp;Docker的主要目标是"Build, Ship and Run Any App, Anywhere", 也就是通过对应用组件的封装, 分发, 部署, 运行 等生命周期的管理, 使用户的APP(可以是一个WEB应用或数据库应用等等) 及其运行环境能够做到<font color=red>"一次封装, 到处运行"</font>
&emsp;&emsp;Linux容器技术的出现就解决了这样一个问题, 而Docker就是在它基础上发展过来的. 将应用运行在Docker容器上面, 而Docker容器在任何操作系统上都是一致的, 这就实现了跨平台, 跨服务器. <font color=red>只需要一次配置好环境, 换到别的机子上就可以一键部署好, 大大简化了操作 </font>
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200716105825428.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mzc0NDA1OQ==,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200716105959254.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mzc0NDA1OQ==,size_16,color_FFFFFF,t_70)

## 是什么
> Docker是解决了运行环境和配置问题软件容器, 方便做持续集成并有助于整体发布的容器虚拟化技术
## 能干什么
### 之前的虚拟机技术
&emsp;&emsp;虚拟机(virtual machine) 就是带环境安装的一种解决方案.
&emsp;&emsp;它可以在一种操作系统里面运行另一种操作系统, 比如在Windows系统里面运行Linux系统. 应用程序对此毫无感知, 因为虚拟机看上去跟真实系统一模一样, 而对于底层系统来说, 虚拟机就是一个普通文件, 不需要了就删掉, 对其他部分毫无影响. 这类虚拟机完美的运行了另一套系统, 能够使应用程序, 操作系统和硬件三者之间的逻辑不变.

&emsp;&emsp; 虚拟机的缺点:
1. 资源占用多  &emsp;&emsp;   2. 冗余步骤多 &emsp;&emsp; 3. 启动慢
### 容器虚拟化技术(虚拟机与容器的区别)
&emsp;&emsp; 由于前面虚拟机存在这些缺点, Linux发展出了另一种虚拟化技术: Linux容器(Linux Containers, 缩写为LXC) .
&emsp;&emsp; <font color=red>Linux容器不是一个完整的操作系统, </font>而是对进程进行隔离. 有了容器,就可以将软件运行的所有资源打包到一个隔离的容器中, 容器与虚拟机不同, 不需要捆绑一整套操作系统, 只需要软件工作所需的库资源和设置. 系统因此而变得高效轻量并保证部署在任何环境中的软件都能始终如一地运行
&emsp;&emsp; 比较了Docker和传统虚拟化方式的不同之处:

* 传统虚拟机技术是虚拟出一套硬件后, 在其上运行一个完整操作系统, 在该系统上再运行所需应用进程;
* 而容器内的应用进程直接运行于宿主的内核, 容器内没有自己的内核, <font color=red>而且也没有进行硬件虚拟</font>. 因此容器要比传统虚拟机更为轻便. 
* 每个容器之间互相隔离,每个容器有自己的文件系统, 容器之间进程不会相互影响,能区分计算资源
## 去哪儿下
1. 官网
docker官网: [http://www.docker.com](http://www.docker.com)
docker中文网站: [https://www.docker-cn.com/](https://www.docker-cn.com/)
2. 仓库
Docker Hub 官网: [https://hub.docker.com/](https://hub.docker.com/)
## Docker架构与内部组件
&emsp;&emsp;Docker采用C/S架构, Docker daemon作为服务端接收来自客户端的请求, 并处理这些请求, 比如创建, 运行容器等. 客户端为用户提供一些列指令与Docker daemon交互
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200722090941727.png)

## Docker有什么优点
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200722091712736.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mzc0NDA1OQ==,size_16,color_FFFFFF,t_70)
## 应用场景
1. 应用打包与部署自动化
&emsp;&emsp;构建标准化的运行环境
&emsp;&emsp;现在大多方案是在物理机和虚拟机上部署运行环境,  面临问题是环境杂乱, 完整性迁移难度高等问题, 容器即开即用
2. 自动化测试和持续集成/部署
&emsp;&emsp;自动化构建镜像和良好的REST API, 能够很好的集成到持续集成/部署环境来
3. 部署与弹性扩展
&emsp;&emsp;由于容器是应用级的, 资源占用小, 弹性扩展部署速度更快.
4. 微服务
&emsp;&emsp;Docker这种容器化隔离技术, 正式应对了微服务理念, 将业务模块放到容器中运行, 容器的可复用性大大增加了业务模块扩展
# Docker安装
Docker支持一下的CentOS版本
CentOS7(64位)
CentOS6.5(64位)或更高的版本
## 前提说明
 <font color=blue>目前CentOS仅发行版本中的内核支持Docker</font>
&emsp;&emsp; Docker运行在CentOS 7 上, 要求系统为64位, 系统内核版本为3.10以上.
&emsp;&emsp; Docker运行在CentOS 6.5 或更高版本的CentOS上,要求系统为64位, <font color=red>系统内核版本为2.6.32-431或者更高版本</font>
<font color=blue>查看自己的内核</font>
&emsp;&emsp; uname命令用于打印当前系统相关信息(内核版本号, 硬件架构, 主机名称和操作系统类型等)
`# uname -r`
<font color=blue>查看已安装的CentOS版本信息</font>
`# lsb_release -a`
`# cat /etc/redhat-release`
## Docker的基本组成
### 镜像
&emsp;&emsp; Docker镜像(Image) 就是一个<font color=red>只读</font>的模板. 镜像可以用来创建Docker容器, <font color=red>一个镜像可以创建很多容器</font>.
![在这里插入图片描述](https://img-blog.csdnimg.cn/202007161152046.png)

### 容器
&emsp;&emsp; Docker利用容器(Container) 独立运行的一个或一组应用. <font color=red>容器是用镜像创建的运行实例</font>.
&emsp;&emsp; 它可以被启动, 开始, 停止, 删除. 每个容器都是相互隔离的, 保证安全的平台.
&emsp;&emsp;  <font color=red>可以把容器看做是一个简易版的Linux环境</font>(包括root用户权限, 进程空间, 用户空间和网络空间等) 和运行在其中的应用程序. 
&emsp;&emsp;容器的定义和镜像几乎一模一样, 也是一堆层的统一视角, 唯一区别在于容器的最上面那一层是可读可写的.

### 仓库
&emsp;&emsp;仓库(Repository) 是<font color=red>集中存放镜像文件</font>的场所.
&emsp;&emsp;仓库(Repository) 和仓库注册服务器(Registry) 是有区别的. 仓库注册服务器上往往存放着多个仓库, 每个仓库中又包含了多个镜像, 每个镜像有不同的标签(tag).
&emsp;&emsp;仓库分为公开仓库(Public) 和私有仓库(Private) 两种形式.
&emsp;&emsp;<font color=red>最大的公开仓库是Docker Hub(https://hub.docker.com/),</font>它存放了数量庞大的镜像供用户下载. 国内的公开仓库包括阿里云, 网易云等

### 小总结
&emsp;&emsp;需要正确的理解仓库/镜像/容器这几个概念:
&emsp;&emsp;Docker本身是一个容器运行载体或称之为管理引擎. 我们把应用程序和配置依赖打包好形成一个可交付的运行环境, 这个打包好的运行环境就是一个image镜像文件. 只有通过这个镜像文件才能生成Docker容器. image文件可以看作是容器的模板. Docker根据image文件生成容器的实例. 同一个image文件, 可以生成多个同时运行的容器实例.

* image文件生成的容器实例, 本身也是一个文件, 称为镜像文件.
* 一个容器运行一种服务, 当我们需要的时候, 就可以通过docker客户端创建一个对应的运行实例, 也就是我们的容器. 
* 至于仓库, 就是放了一堆镜像的地方,我们可以把镜像发布到仓储中, 需要的时候从仓库中拉下来就可以了
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200716131948233.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mzc0NDA1OQ==,size_16,color_FFFFFF,t_70)
## 安装步骤
### CentOS6.8 安装Docker
1. `yum install -y epel-release` Docker使用EPEL发布, RHEL系的OS首先要确保已经持有EPEL库,否则先检查OS版本, 然后安装响应的EPEL包
2. `yum install -y docker-io`
3. 安装后的配置文件: `/etc/sysconfig/docker`
4. 启动Docker后台服务: `service docker start`
5. docker version 验证
### CentOS7安装Docker[没网的情况下如何安装（源代码安装）]
[docker安装官方文档](https://docs.docker.com/install/linux/docker-ce/centos/)
1. 先装gcc`# yum -y install gcc` `# yum -y install gcc-c++`
再设置docker存储库 `# yum install -y yum-utils` 
下面的命令是一行linux命令
从官网设置存储库`# yum-config-manager   --add-repo  https://download.docker.com/linux/centos/docker-ce.repo`
从阿里云设置存储库(推荐)`# yum-config-manager   --add-repo  http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo`
2. 更新yum软件包索引`yum makecache fast`
3. 安装最新版本的Docker Engine和容器
`# yum install docker-ce docker-ce-cli containerd.io`
如果提示您接受GPG密钥，请验证指纹是否匹配 060A 61C5 1B55 8A7F 742B 77AA C52F EB6B 621E 9F35，如果是，则接受它。
4. 启动docker
`# systemctl start docker`
5. 查看docker版本
`# docker version`
6. 配置文件地址`# /etc/docker/daemon.json`可能还没有创建
7. 如果想要卸载 `yum remove docker-ce` `yum remove docker-ce-cli` `yum remove container.io` `rm -rf  /var/lib/docker`

## 永远的HelloWorld
### 阿里云镜像加速适用于CentOS7
1. 是什么?
[阿里云产品](https://dev.aliyun.com/search.html)
2. 注册一个属于自己的阿里云账户(可复用淘宝账号)
3. 在控制台中, 选择产品与服务, 选择容器镜像服务, 选择镜像加速器
4. 获得加速器地址链接
5. 配置本机Docker运行镜像加速器
```linux
# sudo mkdir -p /etc/docker
# vim /etc/docker/daemon.json
{
  "registry-mirrors": ["自己的地址"]
}
# systemctl daemon-reload
# systemctl restart docker
```
6. Linux系统下配置完加速器需要检查是否生效
```linux
# ps -ef|grep docker 
```
### 网易云加速
需要配置网易云的加速器地址
### 启动docker后台容器(测试运行 hello-world)
执行命令`# docker run hello-world`
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200716140006605.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mzc0NDA1OQ==,size_16,color_FFFFFF,t_70)
run的时候做了什么?
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200716140031229.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mzc0NDA1OQ==,size_16,color_FFFFFF,t_70)

## 底层原理
### Docker是怎么工作的
&emsp;&emsp;Docker是一个Client-Server结构的系统, Docker守护进程运行在主机上, 然后通过Socket连接从客户端访问, 守护进程从客户端接受命令并管理运行在主机上的容器. <font color=red>容器, 是一个运行时环境, 就是我们前面说的集装箱.</font>
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200716140500565.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mzc0NDA1OQ==,size_16,color_FFFFFF,t_70)

### 为什么Docker比VM快
1. docker有着比虚拟机更少的抽象层. 由于docker不需要Hypervisor实现硬件资源虚拟化, 运行在docker容器上的程序直接使用的都是实际物理机的硬件资源. 因此在CPU, 内存利用率上docker将会在效率上有明显优势.
2. docker利用的是宿主机的内核, 而不需要Guest OS. 因此, 当新建一个容器时, docker不需要和虚拟机一样重新加载一个操作系统内核. 因而避免引寻, 加载操作系统内返个比较费时费资源的过程, 当新建一个虚拟机时, 虚拟机软件需要加载Guest OS, 返个新建过程是分钟级别的, 而docker由于直接利用宿主机的操作系统, 则省略了返个过程, 因此新建一个docker容器只需要几秒钟
![](https://img-blog.csdnimg.cn/20200716140920200.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mzc0NDA1OQ==,size_16,color_FFFFFF,t_70)
# Docker 常用命令
## 帮助命令
1. `docker version` docker 版本
2. `docker info` docker 信息描述(信息全面)
3. `docker --help`
## 镜像命令
###  docker images  --列出本地主机上的镜像
下面各个标签说明:
REPOSITORY: 表示镜像的仓库源
TAG: 镜像的标签
IMAGE ID: 镜像ID
CREATED: 镜像创建时间
SIZE: 镜像大小
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200716143035413.png)
&emsp;&emsp;同一仓库可以有多个TAG, 代表这个仓库源的不同个版本, 我们使用REPOSITORY: TAG 来定义不同的镜像.
&emsp;&emsp;如果你不指定一个镜像的版本标签, 例如你只使用ubantu, docker将默认使用ubantu: latest

命令的OPTIONS说明: 
* -a: 列出本地所有的镜像(含中间镜像层 镜像就是千层饼,一层套一层 helloworld镜像相当于鸡蛋 里面还有鸡蛋清和鸡蛋黄)
* -q: 只显示镜像ID
* `--digests: 显示镜像的摘要信息`
* `--no-trunc: 显示完整的镜像信息`
### docker search 某个xxx镜像名字 --搜索镜像
&emsp;&emsp;网站: https://hub.docker.com 从这个网站查 然后去阿里云镜像中下载
&emsp;&emsp;命令: `docker search [OPTIONS] 镜像名字`
&emsp;&emsp;OPTIONS说明:
* ` --no-trunc: 显示完整的镜像描述`
* -s: 列出收藏数不小于指定值的镜像 `docker search -s 30 tomcat`   Flag --stars has been deprecated, use `--filter=stars=3` instead

* `--automated: 只列出automated build类型的镜像`
### docker pull 某个xxx镜像名字 --下载镜像
&emsp;&emsp;命令: `docker pull 镜像名字[:TAG]`
&emsp;&emsp;如果不加`:TAG` 等价于拉取`:latest`版本

### docker rmi 某个xxx镜像名字ID --删除镜像
如果不加版本号 默认`:latest`
&emsp;&emsp;删除单个`docker rmi -f 镜像ID(或者镜像名字) -f 强制删除` 
&emsp;&emsp;删除多个`docker rmi -f hello-world nginx 中间以空格分隔`
&emsp;&emsp;删除全部`docker rmi -f $(docker images -qa)`

### docker commit 提交容器副本使之成为一个新的镜像
`docker commit -m="提交的描述信息" -a="作者" 容器ID 要创建的目标镜像名:[标签名]`
### docker push 推送到远程仓库
`docker push  registry.cn-hangzhou.aliyuncs.com/命名空间/仓库名称:[镜像版本号]`
### docker tag把镜像重新打一个标签
`docker tag 镜像名:标签 镜像名:新标签`

### docker export 从(正在运行的)容器内导出所有文件夹(整个文件系统)并生成tar包
`docker export 容器名 > tar包名.tar`
### docker import 从tar包导入成一个镜像
`docker import tar包名.tar 镜像名:版本号`
### docker save把整个镜像都变成一个tar包(把分层的镜像整体打包)
`docker save 镜像名:标签 > 文件.tar`
### docker load把tar包导入成一个镜像
`docker load  -i  文件.tar`

## 容器命令
&emsp;&emsp;<font color=red size=5>有镜像才能创建容器,这是根本前提</font>
### 新建并启动容器
`docker run [OPTIONS] IMAGE(镜像名) [COMMAND] [ARG...]`
OPTIONS说明(常用): 有些是一个-有些是两个--

* `--name "容器新名字": 为容器指定一个名称`
* -d: 后台运行容器, 并返回容器ID, 也即启动守护式容器
* <font color=red>-i: 以交互模式运行容器, 通常与-t 同时使用</font>
* <font color=red>-t: 为容器重新分配一个伪输入终端, 通常与-i 同时使用</font>
* -P: 随机端口映射
* -p: 指定端口映射, 有以下四种格式
	ip:hostPort:containerPort
	ip::containerPort
	<font color=red>hostPort:containerPort</font>
	containerPort
* `--add-host dcsrv2.yuecloud.sy:192.168.xxx.xxx [还可以写其他的] ` 向镜像的/etc/hosts中追加host地址映射
* `-e 传入mysql密码` 将变量传入容器中, 常用于指定mysql的root登录初始密码
* `--link 要连接的容器name:起个别名` 把两个容器之间的网络访问打通
* `--restart=always` 容器挂了会自动重启
### 列出当前所有正在运行的容器
`docker ps`
OPTIONS说明(常用)
* -a: 列出当前所有<font color=red>正在运行的容器</font>+ <font color=red>历史上运行过的</font>
* -l: 显示最近创建的容器
* -n: 显示最近n个创建的容器`docker ps -n 3 上3次运行的`
* <font color=red>-q: 静默模式, 只显示容器编号</font>
* `--no-trunc: 不截断输出`
### 退出容器
1. `exit` 容器停止退出
2. `ctrl + P + Q`容器不停止退出
### 启动容器
`docker start 容器ID或容器名` 适用于停止容器后,启动容器

### 重启容器
`docker restart 容器ID或者容器名`
### 停止容器
`docker stop 容器ID或者容器名` 这个适用于在宿主机上(未进入容器)停止容器,想当于等电脑关机

### 强制停止容器
`docker kill 容器ID或者容器名` 相当于拔电脑插头

### 删除已停止的容器
`docker rm 容器ID`
一次性删除多个容器
`docker rm -f $(docker ps -a -q)`
或者使用
`docker ps -a -q | xargs docker rm`


### <font color=red>重要</font>
#### 启动守护式容器
&emsp;&emsp;使用`docker run -d centos`命令以后台方式启动一个centos容器
&emsp;&emsp;问题: 用`docker ps -a`进行查看会发现容器已经退出
很重要的要说明一点: <font color=red>Docker容器在后台运行, 就必须有一个前台进程</font>
容器运行的命令如果不是那些<font color=red>一直挂起的命令</font>(比如运行top, tail) ,就是会自动退出的.
&emsp;&emsp;这个是docker机制问题, 比如你的web容器,我们以nginx为例, 正常情况下,我们配置启动服务只需要启动响应的service即可. 例如service nginx start
但是, 这样做, nginx为后台进程模式运行, 就导致docker前台没有运行的应用,这样的容器后台启动后, 会立即自杀, 因为它觉得他没事可做了. 
&emsp;&emsp;所以, 最佳的解决方案是, 将你要运行的程序以前台进程的形式运行
那么`docker run -d centos /bin/sh -c "while true;do echo hello zzyy;sleep 2;done"`这个命令,给docker run -d 配置参数,参数是一组shell命令,功能是循环打印hello zzyy一直循环,这样后台运行的程序也有事可做所以不会自杀

#### 查看容器日志
`docker logs -f --tail 容器ID`
* `-t是加入时间戳`
* `-f跟随最新的日志打印`
* `--tail 数字 显示最后多少条`

#### 查看容器内运行的进程
`docker top 容器ID`
#### 查看容器内部细节
`docker inspect 容器ID` 查看容器嵌套容器的细节
#### 进入正在运行的容器并以命令行交互
通过`ctrl + P + Q`不停止退出后
可以用`docker exec -it 容器ID bashShell[shell命令对容器的操作]` 命令 把容器内执行命令后显示的内容返回到宿主机内(相当于隔山打牛)
`docker exec -it 容器ID /bin/bash`相当于重新进入容器的命令行界面
`docker exec -it 容器ID ls -l /tmp` 相当于把容器中/tmp目录下的文件列表输出到宿主机的命令行界面

或者使用
`docker attach 容器ID`
&emsp;&emsp;他们二者的区别
attach 直接进入容器启动命令的终端, 不会启动新的进程
exec实在容器中打开新的终端, 并且可以启动新的进程

#### 从容器内拷贝文件到主机上
`docker cp 容器ID:容器内路径 目的主机路径`
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200716171353791.png)

# Docker镜像
## 是什么
&emsp;&emsp;镜像是一种轻量级的, 可执行的独立软件包, <font color = red>用来打包软件运行环境和基于运行环境开发的软件, </font> 它包含运行某个软件所需的所有内容, 包含代码, 库, 环境变量和配置文件.
### UnionFS(联合文件系统)
&emsp;&emsp;UnionFS(联合文件系统): Union文件系统(UnionFS)是一种分层, 轻量级并且高性能的==文件系统==, 它支持<font color=red>对文件系统的修改作为一次提交来一层层的得加</font>, 同时可以将不同目录挂载到同一个虚拟文件系统下. Union文件系统是Docker镜像的基础. 镜像可以通过分层来进行继承, 基于基础镜像(没有副镜像), 可以制作各种具体的应用镜像
&emsp;&emsp;特性: 一次同时加载多个文件系统, 但从外面看起来, 只能看到一个文件系统, 联合加载会把各层文件系统叠加起来, 这样最终的文件系统会包含所有底层的文件和目录

### Docker镜像加载原理
&emsp;&emsp;docker的镜像实际上由一层一层的文件系统组成, 这种层级的文件系统UnionFS.
&emsp;&emsp;bootfs(boot file system)<font color=red>(实质上就是Linux内核)</font>主要包含bootloader和kernel, bootloader主要是引导加载kernel, Linux刚启动时会加载bootfs文件系统, <font color=red>在Docker镜像的最底层是bootfs</font>. 这一层与我们典型的Linux/Unix系统是一样的, 包含boot加载器和内核. 当boot加载完成之后整个内核就都在内存中了, 此时内存的使用权已由bootfs转交给内核, 此时系统也会卸载bootfs.
&emsp;&emsp;rootfs(root file system), 在bootfs之上. 包含的就是典型Linux系统中的 /dev, /proc, /bin, /etc等标准目录和文件. rootfs就是各种不同的操作系统发行版, 比如Ubantu, Centos等
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200720132118208.png)
<font color=blue>平时我们安装进虚拟机的CentOS都是好几个G, 为什么docker这里才200M?</font>
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200720132205289.png)
&emsp;&emsp;对于一个精简的OS, rootfs可以很小, 只需要包括最基本的命令, 工具和程序库就可以了, 因为底层直接用Host(宿主机)的kernel(内核), 自己只需要提供rootfs就行了. 由此可见对于不同的Linux发行版, bootfs基本是一致的, rootfs会有差别, 因此不同的发行版可以共用bootfs

### 分层的镜像
以pull 拉取mongo为例, 在下载的过程中可以看到docker镜像好像是一层一层的在下载
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200720132438586.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mzc0NDA1OQ==,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200720132700563.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mzc0NDA1OQ==,size_16,color_FFFFFF,t_70)

### 为什么Docker镜像要采用这种分层结构?
&emsp;&emsp;最大的一个好处就是 - 共享资源
&emsp;&emsp;比如: 有多个镜像都从相同的base镜像构建而来, 那么宿主机只需要在磁盘上保存一份base镜像, 同时内存中也只需加载一份base镜像, 就可以为所有容器服务了. 而且镜像的每一层都可以被共享.

## 特点
&emsp;&emsp;Docker镜像都是只读的
&emsp;&emsp;当容器启动时, 一个新的可写层被加载到镜像的顶部.
&emsp;&emsp;这一层通常被称作"容器层", "容器层"之下的都叫"镜像层".
&emsp;&emsp;例如tomcat镜像, 可以操作的部分只是tomcat, 其余的下层都是不可直接操作的. 例如不可以修改tomcat底层的jdk

## Docker镜像commit操作补充
`docker commit `提交容器副本使之成为一个新的镜像
`docker commit -m="提交的描述信息" -a="作者" 容器ID 要创建的目标镜像名:[标签名]`

### 案例演示
1. 从Hub上下载tomcat镜像到本地并成功运行
`docker run -it -p 8080:8080 tomcat`
-p: 主机端口:docker容器端口
-P: 随机分配端口
-i: 交互
-t: 终端
可能会出现网络问题参考[docker 出现网络问题解决方案](https://blog.csdn.net/weixin_43744059/article/details/107462168)
可能会出现404,这是由于tomcat的webapp目录中没有东西
2. 故意删除上一步镜像生产tomcat容器的文档
进入docker容器中的shell命令行`docker exec -it [docker进程号] /bin/bash`
3. 也即当前的tomcat运行实例是一个没有文档内容的容器, 以它为模板commit一个没有doc的tomcat新镜像yang/tomcat02
`docker commit -a="yang" -m="del tomcat docs" tomcat容器ID yang/tomcat:1.2`
4. 启动新镜像并和原来的对比
# Docker容器数据卷(数据持久化, 数据共享)
## 是什么
先看看Docker的理念:
* 将运用与运行的环境打包形成容器运行, 运行可以伴随着容器, 但是我们对数据的要求希望是持久化的
* 容器之间希望有可能共享数据
&emsp;&emsp;Docker容器产生的数据, 如果不通过docker commit生成新的镜像, 使得数据做为镜像的一部分保存下来, 那么当容器删除后, 数据自然也就没有了
&emsp;&emsp;为了能保存数据在docker中我们使用卷
>一句话, 有点类似我们的Redis里面的rdb 和aof文件
## 能干什么
&emsp;&emsp;卷就是目录或文件, 存在于一个或多个容器中, 由docker挂载到容器, 但不属于联合文件系统, 因此能够绕过Union File System提供一些用于持续存储或数据共享的特性
&emsp;&emsp;卷的设计目的就是数据的持久化, 完全独立于容器的生存周期, 因此Docker不会在容器删除时删除其挂载的数据卷
特点:

1. 数据卷可在容器之间共享或重用数据
2. 卷中的更改可以直接生效
3. 数据卷中的更改不会包含在镜像的更新中
4. 数据卷的生命周期一直持续到没有容器使用它为止

>* 容器的持久化
>* 荣期间继承 + 共享数据
## 数据卷实操
### 直接命令添加
`docker run -it -v /宿主机绝对路径目录:/容器内目录 镜像名`  没有目录的话, 会新建出来

#### 查看数据卷是否挂载成功
`docker inspect 容器ID` 在返回的json串中查看是否有Volumes并且是否挂载到一起
 容器停止退出后, 主机修改后数据也是同步的
 #### 命令(带权限)
 `docker run -it -v/宿主机绝对路径目录:/容器内目录:ro 镜像名` ro代表read-only(容器只读)只读

### DockerFile添加
1. 根目录下新建mydocker文件夹并进入
2. 可在Dockerfile中使用<font color=red>VOLUME指令</font>来给镜像添加一个或多个数据卷
`VOLUME["/dataVolumeContainer","/dataVolumeContainer2","/dataVolumeContainer3"]`这里的目录都是容器内目录
&emsp;&emsp;说明:
&emsp;&emsp;处于可移植和分享的考虑, <font color=blue>用`-v 主机目录:容器目录`这种方法不能够直接在Dockerfile中实现.</font>
&emsp;&emsp;由于宿主机目录是依赖于特定宿主机的, 并不能够保证在所有的宿主机上都存在这样的特定目录
3. File构建 vim dockerfile
```Linux
# volume test
FROM centos
VOLUME["/dataVolumeContainer1", "/dataVolumeContainer2"]
CMD echo "finished, -----success1"
CMD /bin/bash
```
4. build后生成镜像
`docker build -f /mydocker/dockerfile -t zzyy/centos .`
5. run容器
`docker run -it zzyy/centos`
6. 通过上述步骤, 容器内的卷目录地址已经知道对应的主机目录地址哪??
`docker ps` 查看当前运行的容器的ID
`docker inspect 容器ID` 查看容器的详细信息, 这里面就有docker宿主机与docker容器挂载的数据卷映射(查看Volumes)
7. <font color=blue>主机对应默认地址</font>
### 备注
&emsp;&emsp;Docker挂载主机目录Docker访问出现cannot open directory: Permission denied
&emsp;&emsp;解决办法: 在挂载目录后多加一个--privileged=true参数即可

## 数据卷容器
### 是什么
&emsp;&emsp;命名的容器挂载数据卷, 其他容器通过挂载这个(父容器)实现数据共享, 挂载数据卷的容器, 称之为数据卷容器
>活动硬盘上面挂活动硬盘实现数据的传递依赖
### 总体介绍
1. 以上一步新建的镜像zzyy/centos为模板并运行容器dc01/dc02/dc03
2. 他们已经具有容器卷/dataVolumeContainer1与/dataVolumeContainer2
### 容器间传递共享
1. 先启动一个父容器dc01 并在dataVolumeContainer2新增内容
`docker run -it --name dc01 zzyy/centos`
2. dc02/dc03继承自dc01
`--volumes-from 父容器名` 继承容器,父容器有什么, 就全都继承过来
命令:`docker run -it --name dc02 --volumes-from dc01 zzyy/centos` dc02/dc03分别在dataVolumeContainer2各自新增内容
3. 回到dc01可以看到02/03各自添加的都能共享了
4. 删除dc01, dc02修改后dc03可否访问? 可以
`docker rm -f dc01` 是可以访问的
5. 删除dc02后dc03可否访问? 可以
6. 新建dc04继承dc03后再删除dc03? 可以
7. <font color=red>结论: 容器之间配置信息的传递, 数据卷的生命周期一直持续到没有容器使用它为止</font>
# DockerFile解析
## 是什么
&emsp;&emsp;DockerFile是用来构建Docker镜像的构建文件, 是由一系列命令和参数构成的脚本. 
### 构建三步骤
1. 编写Dockerfile文件
2. docker build
3. docker run
### 文件什么样
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200721124417846.png)

## DockerFile构建过程解析
### Dockerfile内容基础知识
1. 每条保留字指令都必须为大写字母且后面要跟随至少一个参数
2. 指令按照从上到下, 顺序执行
3. #表示注释
4. <font color=red>每条指令都会创建一个新的镜像层, 并对镜像进行提交</font>
### Docker执行Dockerfile的大致流程
1. docker从基础镜像运行一个容器
2. 执行一条指令并对容器做出修改
3. 执行类似dockercommit的操作提交一个新的镜像层
4. docker再基于刚提交的镜像运行一个新容器
5. 执行dockerfile中的下一条指令知道所有指令都执行完成
### 小总结
&emsp;&emsp;从应用软件的角度来看, Dockerfile, Docker镜像与Docker容器分别代表软件的三个不同阶段
* Dockerfile是软件的原材料
* Docker镜像是软件的交付品
* Docker容器则可以认为是软件的运行态

&emsp;&emsp;Dockerfile面向开发, Docker镜像成为交付标准, Docker容器则设计部署与运维, 三者缺一不可, 合理充当Docker体系的基石
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200721125257336.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mzc0NDA1OQ==,size_16,color_FFFFFF,t_70)
1. Dockerfile, 需要定义一个Dockerfile, Dockerfile定义了进程需要的一切东西. Dockerfile涉及到的内容包括执行代码或者是文件, 环境变量, 依赖包, 运行时环境, 动态链接库, 操作系统的发行版, 服务进程和内核进程(当应用进程需要和系统服务和内核进程打交道, 这时需要考虑如何设计namespace的权限控制)等等
2. Docker镜像, 在用Dockerfile定义一个文件之后, docker build时会产生一个Docker镜像, 当运行Docker镜像时, 会真正开始提供服务;
3. Docker容器, 容器是直接提供服务的
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200721141048735.png)

## DockerFile体系结构(保留字指令)
1. FROM: 基础镜像, 当前新镜像是基于哪个镜像的
2. MAINTAINER: 镜像维护者的姓名和邮箱地址
3. RUN: 容器构建时候需要运行的命令,例如可以 `RUN yum install vim`
4. EXPOSE: 当前容器对外暴露出的端口
5. WORKDIR: 指定在创建容器后, 终端默认登陆的进来工作目录, 一个落脚点
6. ENV: 在构建镜像过程中设置环境变量
`ENV MY_PATH /usr/mytest`
&emsp;&emsp;这个环境变量可以在后续的任何RUN指令中使用, 这就如同在命令前面指定了环境变量前缀一样
&emsp;&emsp;比如: WORKDIR $MY_PATH
7. ADD: 将宿主机目录下的文件拷贝进镜像且ADD命令会自动处理URL和解压缩`ADD jdkxxxx /usr/local`
8. COPY: 类似ADD, 拷贝文件和目录到镜像中. 将从构建上下文目录中<源路径>的文件/目录复制到新的一层的镜像内的<目标路径>位置`COPY c.txt /usr/local/cincontainer.txt`
`COPY src dest` 或 `COPY ["src", "dest"]`
9. VOLUME: 容器数据卷,用于数据保存和持久化工作
10. CMD: 制定一个容器启动时要运行的命令
`CMD`指令的格式和`RUN`相似, 也是两种格式
* `shell`格式: `CMD <命令>`
* `exec`格式: `CMD ["可执行文件", "参数1", "参数2"...]`
* 参数列表格式: `CMD ["参数1", "参数2"...]`, 在指定了`ENTRYPOINT`指令后, 用`CMD`指定具体的参数
&emsp;&emsp;Dockerfile中可以有多个CMD指令, 但只有最后一个生效, CMD会被docker run之后的参数替换
11. ENTRYPOINT: 指定一个容器启动时要运行的命令, ENTRYPOINT的目的和CMD一样, 都是在指定容器启动程序及参数, 不会被docker run之后的参数替换而是会追加进来
12. ONBUILD: 当构建一个被继承的Dockerfile时运行命令, 父镜像在被子继承后父镜像的onbuild被触发`ONBUILD RUN echo "father image onbuild ----- 886"`
### 小总结
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200721143835945.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mzc0NDA1OQ==,size_16,color_FFFFFF,t_70)

## 案例
### Base镜像(scratch)
&emsp;&emsp;Docker Hub中 99% 的镜像都是通过在base镜像中安装和配置需要的软件构建出来的
### 自定义镜像mycentos
1. 编写
&emsp;Hub默认CentOS镜像什么情况?
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200721144559424.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mzc0NDA1OQ==,size_16,color_FFFFFF,t_70)

&emsp;准备编写Dockerfile文件
&emsp;myCentOS内容Dockerfile

```dockerfile
FROM centos
MAINTAINER zzyy<zzyy167@126.com>

ENV MYPATH /usr/local
WORKDIR $MYPATH

RUN yum -y install vim
RUN yum -y install net-tools

EXPOSE 80

CMD echo $MYPATH
CMD echo "success-------------------ok"
CMD /bin/bash
```
2. 构建
`docker build -f dockerfile的绝对路径 -t 新镜像名字:TAG .` 别忘了最后的点代表在当前路径下
3. 运行
`docker run -it mycentos:1.3`
4. 列出镜像的变更历史
`docker history 镜像名`
### CMD/ENTRYPOINT镜像案例
&emsp;&emsp;都是指定一个容器启动时要运行的命令
&emsp;&emsp;CMD
&emsp;&emsp;&emsp;Dockerfile中可以有多个CMD指令, 但只有最后一个生效, CMD会被docker run 之后的参数替换
&emsp;&emsp;ENTRYPOINT
&emsp;&emsp;&emsp;docker run之后的参数会被当做参数传递给ENTRYPOINT, 之后形成新的

### 自定义镜像Tomcat9
前提是在dockerfile 文件的同级目录中有jdk和tomcat的tar.gz压缩包和c.txt文件
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200721153401898.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mzc0NDA1OQ==,size_16,color_FFFFFF,t_70)
run命令
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200721154232196.png)


## 小总结
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200721155400591.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mzc0NDA1OQ==,size_16,color_FFFFFF,t_70)

# Docker常用安装
## 总体步骤
1. 搜索镜像
2. 拉取镜像
3. 查看镜像
4. 启动镜像
5. 停止容器
6. 移除容器
## 安装tomcat
1. 查找tomcat镜像 `docker search tomcat`
2. 拉取到本地`docker pull tomcat`
3. 查看是否拉取到`docker images`
4. 运行镜像`docker run -it -p8080:8080 tomcat`
## 安装mysql
1. `docker pull mysql:5.6`
2. 使用mysql镜像
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200721160636550.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mzc0NDA1OQ==,size_16,color_FFFFFF,t_70)


3. 外部win10也来连接运行在docker上的mysql服务
## 安装redis
1. `docker pull redis:3.2`
2. ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200721161510126.png)

# 本地镜像发布到阿里云
## 镜像的生成方法
1. Dockerfile的build
2. 从容器创建一个新的镜像`docker commit [OPTIONS] 容器ID [REPOSITORY[:TAG]]`
`-a`: 提交的镜像作者
`-m`: 提交时的说明文字	

## 将本地镜像推送到阿里云
1. 阿里云开发者平台[阿里云开发者平台](https://cr.console.aliyun.com/cn-hangzhou/instances/images)
2. 创建仓库镜像
&emsp;&emsp;命名空间
&emsp;&emsp;仓库名称
3. 将镜像推送到阿里云
`docker login --username=registry.cn-hangzhou.aliyuncs.com`
`输入账号`
`docker tag xxxxx registry.cn-hangzhou.aliyuncs.com/命名空间/mycentos:[镜像版本号]`
`docker push  registry.cn-hangzhou.aliyuncs.com/命名空间/仓库名称:[镜像版本号]`
# 搭建私有镜像仓库
&emsp;&emsp;docker已经提供一个镜像来支持本地搭建私有镜像仓库了
`docker pull registry` 拉取镜像仓库镜像
`docker run -d -v /opt/registry:/var/lib/registry -p 5000:5000 --restart=always --name registry registry`
`curl http://本机ip地址:5000/v2/_catalog` 列出已经上传了的镜像列表

## 私有仓库管理
### 配置私有仓库可信任（设置非对称私钥 使用https访问）
`# vi /etc/docker/daemon.json`添加
`{"insecure-registries":["本机ip:5000"]}`
`# systemctl start docker`重启docker

### 重新打标签
`docker tag centos:6 本地仓库IP:5000/centos:6.1`

### 上传
`docker push 本地ip:5000/centos:6.1`

### 下载
`docker pull 本地ip:5000/centos:6.1`

### 列出镜像标签
`curl http://本机ip地址:5000/v2/centos/tags/list`

# 图形界面管理DockerUI
&emsp;&emsp;DockerUI是一个基于Docker API提供图形化页面简单的容器管理系统, 支持容器管理, 镜像管理
`docker pull uifd/ui-for-docker`
`docker run -it -d --name docker-web -p 9000:9000 -v /var/run/docker.sock:/var/run/docker.sock --restart=always docker.io/uifd/ui-for-docker `
访问IP地址:9000进入dockerui管理界面

# Shipyard管理系统
&emsp;&emsp;Shipyard也算是基于Docker API实现的容器图形管理系统, 支持container, images, engine, cluster等功能, 可满足我们的基本的容器部署需求
&emsp;&emsp;Shipyard分为手动部署和自动部署
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200722115816845.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mzc0NDA1OQ==,size_16,color_FFFFFF,t_70)
[shipyard官方文档](https://www.shipyard-project.com/docs/deploy/)

# cAdvisor+ InfluxDB+ Grafana监控docker
&emsp;&emsp;cAdvisor: Google开源的工具, 用于监控Docker主机和容器系统资源, 通过图形界面实时显示数据, 但不存储: 它通过宿主机/proc, /sys, /var/lib/docker等目录下文件获取宿主机和容器运行信息
&emsp;&emsp;InfluxDB: 是一个分布式的时间序列数据库, 用来存储cAdvisor收集的系统资源数据
&emsp;&emsp;Grafana: 可视化展示平台, 可做仪表盘, 并图表页面操作很方便, 数据源支持zabbix, Graphite, InfluxDB, OpenTSDB, Elasticsearch等
&emsp;&emsp;他们之间的关系: cAdvisor容器数据采集 -> InfluxDB容器数据存储 -> Grafana可视化展示

# Docker结合Jenkins构建持续集成环境
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200722150039612.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mzc0NDA1OQ==,size_16,color_FFFFFF,t_70)
## 持续集成相关工具
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200722151941748.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mzc0NDA1OQ==,size_16,color_FFFFFF,t_70)
## Docker+Jenkins+Maven+Git搭建持续集成环境
## 流程图
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200804091223259.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mzc0NDA1OQ==,size_16,color_FFFFFF,t_70)



