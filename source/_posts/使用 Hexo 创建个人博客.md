---
title: 使用Hexo创建个人博客
cover: /my_pic/使用Hexo创建个人博客/0.png
date: 2021-11-06 23:36:32
tags: ['Hexo']
categories: ['前端']
toc: true
---

# 使用 `Hexo` 创建个人博客

`Hexo` 是一个简单高效的博客框架工具，通过解析 `markdown` 文件快速生成网页。

> `Hexo` 官网：<https://hexo.io/>

在安装 `Hexo` 前需要先安装好 `Node.js` 和 `Git`，安装方法参考一下链接。

> [`Node.js` 的安装](https://awewu.github.io/2021/11/04/Node.js%20%E7%9A%84%E5%AE%89%E8%A3%85/)
>
> [`Git` 的安装](https://awewu.github.io/2021/11/04/Git%20%E7%9A%84%E5%AE%89%E8%A3%85/)

## `Hexo` 的安装

安装好 `Node.js` 和 `Git` 后，在命令行里输入以下命令安装 `Hexo`。

```shell
npm install hexo-cli -g
```

等待其安装。

![1](/my_pic/使用Hexo创建个人博客/1.png)

## 创建项目

安装好 `Hexo` 后，进入个人项目文件夹，通过命令行输入以下命令创建项目。

```shell
# 初始化项目，项目名自选
hexo init project-name

# 进入到项目目录
cd project-name

# 安装所需依赖
npm install

# 安装插件
npm install hexo-deployer-git --save
```

![2](/my_pic/使用Hexo创建个人博客/2.png)

## 生成项目

继续输入下列命令在本地生成博客项目。

```shell
# 生成项目
hexo g

# 启动服务（设置端口为80）
hexo s -p 8080
```

在浏览器地址栏中输入 `http://localhost:8080`，可以见到效果。

![3](/my_pic/使用Hexo创建个人博客/3.png)

## 新建博客

在命令行中输入 `hexo new article-name` 可以新建一篇文章，文章名自选。

![4](/my_pic/使用Hexo创建个人博客/4.png)

文章是 `markdown` 文件，存放在 `source/_post` 目录下。

![5](/my_pic/使用Hexo创建个人博客/5.png)

打开文件可以看到文章结构。

![6](/my_pic/使用Hexo创建个人博客/6.png)

上方区块里写的是该文章的一些基本信息。区块下方可以写正文。

![7](/my_pic/使用Hexo创建个人博客/7.png)

写好之后重新生成项目，并打开网站，效果如下。

![8](/my_pic/使用Hexo创建个人博客/8.png)

## 使用 `GitHub` 创建网站

`GitHub` 提供了一个 `GitHub Page` 服务，可以帮助我们自动生成静态网站，我们使用的就是该服务。

首先，先新建一个仓库，仓库名格式有要求，必须要用你的 `GitHub` 用户名，比如我的 `GitHub` 用户名是 **<u>awewu</u>**，所以我的仓库名必须叫 `awewu.github.io`。

![9](/my_pic/使用Hexo创建个人博客/9.png)

创建好后，找到项目根目录下的 `_config.xml` 文件，修改末尾的 `deploy`。示例如下。

```yml
deploy:
	type: git
	repo: https://github.com/awewu/awe_wu.github.io.git
	branch: master
```

其中，`repo` 是指你博客的 `GitHub` 仓库地址。

修改好后，在命令行中键入 `hexo d` 将项目提交到 `GitHub`。

然后打开<https://awewu.github.io/>，可以看到已经创建好了。

