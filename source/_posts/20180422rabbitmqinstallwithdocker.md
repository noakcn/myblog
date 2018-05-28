---
title: Docker安装部署Rabbitmq
date: 2018-4-22 16:37:22
tags:
- docker
- rabbitmq
- 消息中间件
categories:
- 实践
- 
---

最近突然想玩下消息中间件，根据搜索结果rabbitmq是比较流行的消息中间件。那么我们通过docker部署来试用下。

### 搜索

网上有很多教程，不过都是利用镜像`macintoshplus/rabbitmq-management`来构建，我试用了下，他的rabbitmq版本是16年发布的3.6.2。如果我想用新的怎么办呢。

我们可以利用 [docker hub](https://hub.docker.com/)来搜索(需要翻墙才能稳定打开)利用官方镜像创建最新的。
搜索结果如下:
![](http://om8bq99t5.bkt.clouddn.com/18-5-28/33063754.jpg)

![](http://om8bq99t5.bkt.clouddn.com/18-5-28/30085426.jpg)

运行拉取最新的镜像
```
docker pull rabbitmq 
```

如果直接运行这个rabbitmq镜像，是没有管理界面的。我们需要执行如下命令
```

docker run -d --name officialrabbitmq -p 5672:5672 -p 15672:15672 rabbitmq:3-management

```
`3-management`表示使用带管理功能的镜像

### 访问

启动后访问 http://ip:15672 端口即可 默认用户guest，密码guest