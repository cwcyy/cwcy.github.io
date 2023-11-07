---
title: Hexo+Github Pages + Github Actions 部署个人博客
date: 2023-11-07 17:38:25
tags:
---
# 一、部署Hexo
## 1、安装Hexo
在安装nodejs、和git的情况下，打开cmd，输入命令安装Hexo。
```
npm install -g hexo-cli
```
## 2、初始化项目
在想要初始化项目的地方打开cmd，然后输入`hexo init xxx-blog` 以下命令，会自动生成一个新的文件夹。
初始化后`cd xxx-blog`进入目录文件夹，`npm install`安装需要的依赖文件
```
hexo init xxx-blog
cd xxx-blog
npm install
```
## 3、运行项目
输入`hexo s`，然后打开`http://localhost:4000/`即可访问
![](img/Pasted%20image%2020231106161324.png)
![](img/Pasted%20image%2020231106161254.png)
# 二、配置Github Pages
# 1、新建仓库
打开[github.com](https://github.com/)登录自己的账号后新建一个仓库，仓库名称**必须为`用户名.github.io`**
![](img/Pasted%20image%2020231106161842.png)![](img/Pasted%20image%2020231107162634.png)
输入`repository name`后直接创建即可。
# 三、部署到Github Pages
## 方式一、使用Github Actions
### 1、设置部署方式
设置Source 为 GitHub Actions
![](img/Pasted%20image%2020231107172939.png)
### 2、创建工作流文件
在hexo目录下创建`.github/workflows/pages.yml`文件。
- 其中的`branches`如果自己的分支不是`master`的需要修改为自己的分支名。
- `node-version`需要修改为自己的版本，可以使用命令`node --version`查看自己的版本。
```
name: Pages

on:
  push:
    branches:
      - master # default branch

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
        with:
          token: ${{ secrets.GITHUB_TOKEN }}
          # If your repository depends on submodule, please see: https://github.com/actions/checkout
          submodules: recursive
      - name: Use Node.js 16.x
        uses: actions/setup-node@v2
        with:
          node-version: '16.14.2'
      - name: Cache NPM dependencies
        uses: actions/cache@v2
        with:
          path: node_modules
          key: ${{ runner.OS }}-npm-cache
          restore-keys: |
            ${{ runner.OS }}-npm-cache
      - name: Install Dependencies
        run: npm install
      - name: Build
        run: npm run build
      - name: Upload Pages artifact
        uses: actions/upload-pages-artifact@v2
        with:
          path: ./public
  deploy:
    needs: build
    permissions:
      pages: write
      id-token: write
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v2
```
### 3、添加文件然后部署
使用`git` 将文件推送到服务端即可。
若文件中没有.gitignore，需要先创建一下
```
node_modules/
package-lock.json
yarn.lock
public/
```
然后将文件推送到`github`仓库
```
# 添加修改文件到暂存区
git add .
# 提交
git commit -m 'init commit'
# 推送
git push origin
```
### 4、查看部署情况
打开`Github` 仓库可以看到工作流已经完成，此时打开`https://用户名.github.io`即可看到自己的博客。
![](img/Pasted%20image%2020231107173632.png)
## 方式二、使用`hexo-deployer-git`插件
### 1、安装部署插件
```
npm install hexo-deployer-git --save
```
### 2、配置上传路径
在`_config.yml`中配置：
将其中的`<username>`替换成自己的即可

```
deploy:  
  type: git  
  repo: https://github.com/<username>/<username>.github.io  
  # example, https://github.com/hexojs/hexojs.github.io  
  branch: gh-pages
```
### 3、部署
在目录中输入以下命令：
```
hexo clean && hexo d
```
如果部署失败可能是因为git的ssh没有配置好，需要配置一下。
### 4、GithubPages设置
打开刚刚创建的仓库，然后设置要显示的分支
![](img/Pasted%20image%2020231107163852.png)
### 5、打开网页查看效果
浏览器输入`https://用户名.github.io`，将用户名换成自己的进行访问。
![](img/Pasted%20image%2020231107171041.png)