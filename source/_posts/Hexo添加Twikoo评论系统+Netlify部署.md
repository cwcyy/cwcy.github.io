---
title: Hexo添加Twikoo评论系统
date: 2023-11-24 17:22:48
tags:
  - Hexo
categories: 博客
---
## MongoDB注册
### 1.申请 MongoDB 账号

注册MongoDB账号[MongoDB Atlas | MongoDB](https://www.mongodb.com/cloud/atlas/register)，可以直接使用Google登录。
### 2.创建MongoDb数据库
选择免费的，区域要选择`AWS / N. Virginia (us-east-1)`。

![](../img/Pasted%20image%2020231124173104.png)
### 3.创建用户
输入用户名和密码后点击创建。
![](../img/Pasted%20image%2020231124173421.png)
### 4.设置网络允许所有ip连接
在 Network Access 页面点击 Add IP Address，Access List Entry 输入 `0.0.0.0/0`（允许所有 IP 地址的连接），点击 Confirm。
![](../img/Pasted%20image%2020231124173635.png)
### 5.复制连接字符串
在 Database 页面点击 Connect，连接方式选择 Drivers，并记录数据库连接字符串，请将连接字符串中的 `<username>:<password>` 修改为刚刚创建的数据库 `用户名:密码`。
![](../img/Pasted%20image%2020231124174841.png)
## Vercel部署
### 1.申请Vercel账号
申请并登录 [Vercel](https://vercel.com/) 账号
点击以下一键部署进行部署。
[一键部署][https://vercel.com/import/project?template=https://github.com/twikoojs/twikoo/tree/main/src/server/vercel-min]
![](../img/Pasted%20image%2020231127100211.png)
### 2.添加环境变量
打开`Setting -> Environment Variables`，添加环境变量 `MONGODB_URI`，输入前面保存的字符串。
![](../img/Pasted%20image%2020231127100617.png)
然后重新部署
![](../img/Pasted%20image%2020231127100838.png)
成功运行
![](../img/Pasted%20image%2020231127100942.png)
### 3.博客配置
将部署的网址配置到博客主题对应的配置中。
![](../img/Pasted%20image%2020231127105851.png)
