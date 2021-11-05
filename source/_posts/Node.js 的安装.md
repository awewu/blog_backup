---
title: Node.js 的安装
cover: /my_pic/Node.js_install/0.png
date: 2021-11-04 10:39:32
tags: ['Node.js']
categories: ['前端']
toc: true
---

# `Node.js` 的安装

## 安装包下载

`Node.js` 的官网是 <https://nodejs.org/en/download/>。根据个人电脑系统对不同的安装包进行选择。本文以 `Windows` 为例。

在通常情况下，`Node.js` 的版本要求不是那么高。所以可以选中网页下方的 <u>**All download options**</u> 。

![1](/my_pic/Node.js_install/1.png)

选择相应的文件目录下载适合个人的 `Node.js` 版本。本文以 `node-v13.8.0-x64.msi` 为例。

## 程序安装

双击打开下载好的安装程序，然后选择 `Next`。

![image-20211102213313685](/my_pic/Node.js_install/2.png)

勾选 <u>**I accept the terms in the License Agreement**</u>，然后点击 `Next`。

![image-20211102213642900](/my_pic/Node.js_install/3.png)

设置安装路径，点击 `Next`。

![image-20211102213812091](/my_pic/Node.js_install/4.png)

直接选择 `Next`。

![image-20211102213933978](/my_pic/Node.js_install/5.png)

同样直接选择 `Next`。

![image-20211102214009755](/my_pic/Node.js_install/6.png)

选择 `Install`。

![image-20211102214042360](/my_pic/Node.js_install/7.png)

等待安装完成。

![image-20211102214104610](/my_pic/Node.js_install/8.png)

点击 `Finish`。

![image-20211102214140385](/my_pic/Node.js_install/9.png)

## 验证安装情况

使用 `win + R` 快捷键唤出 `运行` 窗口，在窗口中键入 `cmd`。

![image-20211102214817206](/my_pic/Node.js_install/10.png)

在命令行窗口中分别键入 `node -v` 和 `npm -v` 查看安装程序版本。如图，即为安装成功。

![image-20211102214956085](/my_pic/Node.js_install/11.png)

## 修改 `npm` 与 `npm_cache` 路径

在安装目录下分别创建好 `npm` 与 `npm_cache` 文件夹，同时在新建的 `npm` 文件夹下创建 `node_modules` 文件夹。

再次使用 `win + R` 快捷键打开 `运行` 窗口，键入 `cmd` 打开命令行窗口。输入以下命令：

```shell
npm config set prefix "D:/opensource/Node.js/npm"
npm config set cache "D:/opensource/Node.js/npm_cache"
```

然后在 `环境变量` 中新建 `NODE_PATH`，设置值为 `D:/opensource/Node.js/npm/node_modules`

![image-20211102220723615](/my_pic/Node.js_install/12.png)

同时修改 `Path`，将 `C:/Users/E360/AppData/Roaming/npm` 修改为 `D:/opensource/Node.js/npm`。

（*文中各路径皆需与个人安装位置和用户名匹配*）

