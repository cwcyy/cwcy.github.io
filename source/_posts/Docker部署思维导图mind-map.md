---
title: Docker部署思维导图mind-map
date: 2023-11-24 09:04:27
tags:
  - 思维导图
categories: 服务器
---
## 拉取并部署镜像
拉取命令：
``` bash
docker pull shuiche/mind-map:latest
```
部署命令：
```
docker run -d --restart=always -p 9090:8080 --name mind-map shuiche/mind-map:latest
```