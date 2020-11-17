---
title: Docker安装elasticsearch
date: 2020-08-27 14:43:37
Tags: docker
---

### 执行命令

```ssh 
docker run -d --name elasticsearch  --privileged -p 9200:9200 -p 9300:9300   elasticsearch:6.8.6
```


### 安装中文解析插件
```ssh 
elasticsearch-plugin install https://github.com/medcl/elasticsearch-analysis-ik/releases/download/v6.8.5/elasticsearch-analysis-ik-6.8.6.zip

docker cp /Users/denny/Downloads/elasticsearch-analysis-ik-6.8.6.zip elasticsearch:/usr/share/elasticsearch/plugins
elasticsearch-plugin list
```

> 如报错，需要手动创建一个文件（位置与名称看错误信息）


