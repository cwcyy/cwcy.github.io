---
title: Hexo更换主题
date: 2023-11-08 09:48:12
tags:
  - Hexo
---
## 一、下载主题
主题可以在[Themes | Hexo](https://hexo.io/themes/)中寻找，点击主题的标题可以进入对应的`Github`地址。
![](../img/Pasted%20image%2020231108095013.png)
然后在`themes`目录下，右键打开`Git Bash Here`，也可以使用`cmd`。
![](../img/Pasted%20image%2020231108094850.png)
将刚刚打开的仓库`clone`下来：
```shell
git clone https://github.com/blinkfox/hexo-theme-matery.git
```
如果不想用`git clone`的方式，也可以直接下载下来后打开。

## 二、更换主题
### 1、修改配置文件
在`_config,yml`中修改`theme`
```yml
# 修改中文
language: zh-CN
# 设置为6的倍数，这样文章列表在各个屏幕下都能较好的显示。
index_generator:
  path: ''
  per_page: 12
  order_by: -date
# 设置为6的倍数，这样文章列表在各个屏幕下都能较好的显示。
per_page: 12
# 修改为自己下载后对应的文件夹名即可
theme: hexo-theme-matery
```
### 2、新建分类 categories 页
```
hexo new page 'categories'
```
编辑 `/source/categories/index.md` 页面，其中必须有以下内容
```md
---
title: categories
date: 2023-11-08 10:09:21
type: "categories"
layout: "categories"
---
```

### 3、新建标签 tags 页
```Shell
hexo new page 'tags'
```
编辑 `/source/tags/index.md` 页面，其中必须有以下内容
```md
---
title: tags
date: 2023-11-08 10:14:30
type: "tags"
layout: "tags"
---
```
### 4、新建关于我 about 页
```Shell
hexo new page 'about'
```
编辑 `/source/about/index.md` 页面，其中必须有以下内容
```md
---
title: about
date: 2023-11-08 10:09:10
type: "about"
layout: "about"
---
```
### 4、新建 404 页
```Shell
hexo new page '404'
```
编辑 `/source/404.md` 页面，其中必须有以下内容
```
---
title: '404'
date: 2023-11-08 10:11:32
type: "404"
layout: "404"
description: "Oops～，我崩溃了！找不到你想要的页面 :("
---
```
### 5、留言板和友情链接(可选)
创建页面
```text
# 留言板
hexo new page "contact"
# 内容
---
title: contact
date: 2018-09-30 17:25:30
type: "contact"
layout: "contact"
---
# 友情链接
hexo new page "friends"
#内容
---
title: friends
date: 2018-12-12 21:25:30
type: "friends"
layout: "friends"
---
```
不需要的话可以关闭掉，在`themes\hexo-theme-matery\_config.yml`中配置。
![](../img/Pasted%20image%2020231108102716.png)
## 三、运行查看
```Shell
hexo clean
hexo s
```
![](../img/Pasted%20image%2020231108102825.png)
## 四、主题功能自定义（可选）
### 1、代码高亮
修改`_config.yml`中的`highlight.enable`和`prismjs.enable`
```yml
highlight:
  enable: false
  line_number: true
  auto_detect: false
  tab_replace: ''
  wrap: true
  hljs: false
prismjs:
  enable: true
  preprocess: true
  line_number: true
  tab_replace: ''
```
### 2、搜索
主题中使用了[hexo-generator-search](https://github.com/wzpan/hexo-generator-search)做内容搜索，要使用搜索需要安装该插件：
```shell
npm install hexo-generator-search --save
```
配置Hexo的`_config.yml`
```yml
search:
  path: search.xml
  field: post
```
### 3、中文链接转拼音
如果文章名称是中文的，那么 `Hexo` 默认的生成的永久链接也会有中文，这样不利于 `SEO`。可以用[hexo-permalink-pinyin](https://github.com/viko16/hexo-permalink-pinyin)该插件将名称生成为中文拼音的永久链接。 
```shell
npm i hexo-permalink-pinyin --save
```
配置Hexo的`_config.yml`
```yml
permalink_pinyin:
  enable: true
  separator: '-' # default: '-'
```
### 4、文章字数统计
如果你想要在文章中显示文章字数、阅读时长信息，可以安装 [hexo-wordcount](https://github.com/willin/hexo-wordcount)插件。
```shell
npm i --save hexo-wordcount
```
配置主题的`/themes//_config.yml`
```
postInfo:
  date: true
  update: true
  wordCount: true # 设置文章字数统计为 true.
  totalCount: true # 设置站点文章总字数统计为 true.
  min2read: true # 阅读时长.
  readCount: true # 阅读次数.
```
### 5、重新配色
渐变色网站参考[ WebGradients](https://webgradients.com/)
在主题文件夹中`\themes\hexo-theme-matery\source\css\matery.css`，全局替换`#4cbf30`和`#0f9d58`
为自己喜欢的颜色即可。
### 6、使用相对路径引用本地图片
hexo默认的资源文件夹是`source`，在`source`中创建一个文件夹`img`。
`typora`的配置如下，使用相对路径，然后设置默认存放的路径：
![](../img/Pasted%20image%2020231108090606.png)
`obsidian`的配置如下，使用相对路径，然后设置默认存放的路径。
![](../img/Pasted%20image%2020231108092415.png)
