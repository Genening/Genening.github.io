---
title: Electron
author: Genening
thumbnail: /gallery/thumbnail/electron.jpg
date: 2019-11-08 09:03:25
updated: 2019-11-08 09:03:25
categories: web
tags: electron开发
---
## 简介
<!--more-->
>Electron是由Github开发，用**HTML，CSS和JavaScript**来构建跨平台桌面应用程序的一个开源库。 Electron通过将Chromium和Node.js合并到同一个运行时环境中，并将其打包为**Mac，Windows和Linux**系统下的应用来实现这一目的。<br>简单来说，这是一个强大的工具，可以用于搭建跨平台桌面应用，而且有方便强大的API库提供，所以，开始一场新的探索吧，**如果你永远只做你能做到的事情，那么你永远也只能停在当前的高度。**
![companies](electron/company.jpg)

## 目录：暂略

### 1. 环境准备
>* 安装**Node.js** [Node.js下载页面](https://nodejs.org/en/download/)
>* npm 安装Node.js的时候已经安装了 
>>检查npm node是否安装成功，在命令行工具中输入*node -v* *npm -v*，显示版本号则便是环境准备完成。就是这么简单，赶紧尝试一下吧！

**快速开始一个项目**
```
# 克隆示例项目的仓库
$ git clone https://github.com/electron/electron-quick-start

# 进入这个仓库
$ cd electron-quick-start

# 安装依赖并运行
$ npm install && npm start
```
效果如下：
![quick-start](electron/quick-start.jpg)

>这个quick-start项目提供了一个非常简约的模板，可以在这个基础上搭建自己的应用。看起来还是不错的，很期待打包成桌面应用的效果。

**quick-start目录解析**
![content](electron/content.jpg)

* node_modules：模块依赖
* package.json：描述包的文件，这里默认已经将主进程入口文件配置为main.js
* main.js：主进程
* renderer.js：渲染进程，它的操作跟web中的js操作大同小异，所以最好有node.js、js以及es6的语法的功底，这样开发起来，才能得心应手。