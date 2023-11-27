---
title: Hexo使用相对路径插入图片
date: 2023-11-08 08:56:20
tags:
---
# 一、安装插件
在文件目录中使用`nodejs`安装`hexo-asset-image`
```Shell
npm install hexo-asset-image --save
```
因为项目是很久之前的了，所以需要修改其中的一点参数。
依次打开`node_modules`->`hexo-asset-image`->`index.js`。
修改第58行，删除原本的其他参数即可，只留下`src`。
![](../img/Pasted%20image%2020231108090016.png)
# 二、修改设置
hexo默认的资源文件夹是`source`，在`source`中创建一个文件夹`img`。
`typora`的配置如下，使用相对路径，然后设置默认存放的路径：
![](../img/Pasted%20image%2020231108090606.png)
`obsidian`的配置如下，使用相对路径，然后设置默认存放的路径。
![](../img/Pasted%20image%2020231108092415.png)
