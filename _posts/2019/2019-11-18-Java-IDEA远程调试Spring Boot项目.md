---
layout: post
title: "IDEA远程调试Spring Boot项目"
date: 2019-11-18 17:58:34 +0800
categories: [Java]
---

## IDEA远程调试Spring Boot项目

> java -Xdebug -Xrunjdwp:server=y,transport=dt_socket,address=8080,suspend=n -jar debug.jar

- 其中``debug.jar``为程序jar名称 
- 8080为远程调试监听端口, 非程序运行端口
- 可--server.port=8081指定程序运行端口
- 远程调试不需要启动本地项目，两边代码一定要**保持一致**
- 本人使用JDK版本为8
- centos查询端口指令netstat -tunlp \|grep 8000



### 配置远程调试

1. 项目启动配置添加**Remote**

![1574068154208](/assets/img/remote01.png)

2. 添加监听地址，主机位目标主机IP地址，端口为之前项目启动时配置的调试监听端口。注意JDK版本，

![1574068292417](/assets/img/remote02.png)
