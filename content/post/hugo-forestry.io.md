+++
aliases = []
categories = []
date = 2022-04-27T04:00:00Z
description = "为降低博客使用门槛，欢迎使用forestry.io进行博客写作！"
draft = true
image = ""
series = []
slug = "forestry"
tags = ["Hugo"]
title = "Hugo | 利用forestry.io进行博客写作"

+++
> 本文基于[小鱼](https://gregueria.icu/)和我的聊天记录生成！

## 关于forestry.io

forestry.io是一种后端网站，我们把github上的代码仓库托管给它后，任何时候我们在forestry.io网页上写作，它都会自动帮我们将文章push至github博客项目里的.content文件夹。

相比起本地写作完成、利用github desktop将文章push至代码仓库，基于forestry.io的写作有以下几个优点：

* 本地写作必须依赖电脑，而forestry.io可以在任何能打开网页的地方进行写作，对手机、ipad用户友好
* 利用forestry的Preview功能可以一边写博客一边预览，方便调整文章排版
* forestry可以保存文章开头的front-matter模板，一劳永逸
* 使用forestry基本不需要markdown语法，直接点点点，操作简单
* 有自动保存功能，避免内容丢失

![本文写作时的forestry界面](/uploads/forestry.png)

## 具体步骤

### 进入forestry.io界面，注册账号

forestry.io网址为[https://forestry.io/](https://forestry.io/ "https://forestry.io/")，第一次点进去时需要注册账号（也可以直接点击[https://forestry.io/login]()，推荐直接使用Github账号登陆。

![forestry.io登陆界面](/uploads/forestry2.png)

### Add site

登陆成功后会显示如下界面（应该是空的，我这里的hugo文件是因为我之前已经添加过），点击右上角的Add site。

![](/uploads/forestry3.png)

选择Hugo，然后再选择你的代码仓库，如我的代码仓库存放在github，这里便选择github，会出现以下界面。

![](/uploads/forestry4.png)

在Repository处选择你的博客项目，我自己的博客项目命名就是hugo，branches选择main就好。点击next，导入完成。

### Finish setup process

点击第四个Set up preview commands打开实时浏览。

### 设置Front matter

点击左边黑框的Front matter，接着点add template，设置Front matter模板。这里可以选择添加一个新的模板，或者直接导入已有文章的模板。一般博客主题如果提供了示例文章，建议选择第二个，更加方便，如果没有提供示例文章，需要根据博客主题中Front matter相关的使用说明进行设置。一般而言，基本的Front matter都大同小异，包含文章标题、写作日期、间接、标签等。

![](/uploads/forestry5.png)

### 开始写作吧！

以上全部完成后，就可以点击左侧的Post，再点击create new，就可以新建一个新的post文件开始写作了，界面基本和我的第一张图一样，左侧是Front matter，右侧是正文。

是不是很简单很方便！

不明白的地方也可以参考下这篇：[https://blog.arcto.me/others/forestry.io/](https://blog.arcto.me/others/forestry.io/ "使用forestry.io管理你的博客")