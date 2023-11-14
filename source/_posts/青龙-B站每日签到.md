---
title: 青龙-B站每日签到
date: 2023-11-14 16:41:56
tags:
- 青龙面板
categories: 服务器
---
## 一、参数配置

打开青龙面板->配置文件->修改RepoFileExtensions为`js py sh ts`。  

![](../img/Pasted%20image%2020231113154531.png)

## 二、添加订阅

打开青龙面板->订阅管理->创建订阅->粘贴下面命令到名称后输入名称->设置定时任务`2 2 28 * *`(每天0点更新仓库)->确定->运行。

```bash
ql repo https://github.com/RayWangQvQ/BiliBiliToolPro.git "bili_task_"
#如果无法拉取到的可以在前面加Github加速网址例如：https://hub.gitmirror.com/
ql repo https://hub.gitmirror.com/https://github.com/RayWangQvQ/BiliBiliToolPro.git "bili_task_"
```
![](../img/Pasted%20image%2020231114164540.png)
## 三、登录

打开青龙面板->定时任务->找到`bili扫码登录`->运行（第一次运行会自动安装`dotnet`环境，会比较慢）->查看日志->使用手机扫码登录。
登录后，会自动将cookie保存到青龙的环境变量中。
![](../img/Pasted%20image%2020231114170419.png)