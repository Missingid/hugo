+++
aliases = []
categories = []
date = 2022-01-29T16:00:00Z
description = "将施工过程中的Tips分享与你！"
draft = true
image = ""
series = []
slug = "decorating_2"
tags = ["Hugo"]
title = "Hugo | 装修小技巧"

+++
我会持续按照总体Tips、左侧栏、右侧栏等的顺序更新装修技巧！

# Tips

* Chrome浏览器打开博客后，点击最右侧纵向排列的三个点，找到更多工具中的开发者工具

![](/uploads/hugo1.png)

# 正文

## 正文图片缩小

在assets\\scss\\partials\\layout\\articles.scss中修改max-width：

    .article-content {
    	margin: var(--card-padding) 0;
    	color: var(--card-text-color-main);
        img {
          max-width: 90%; //原来是100%
          height: auto;
        }
    }

# 左侧栏

## 社交账号icon居中

在assets\\scss\\partials\\menu.scss中新加一行：

    .social-menu {
        list-style: none; 
        padding: 0%;
        display: flex;
        flex-direction: row;
        gap: 10px;
        justify-content:center; //新加的
    }

## 修改菜单栏上方距离

在assets-scss-partials-menu.scss中修改margin-top：

    .menu {
    	······
        @include respond(xl) {
            margin-top: 10px; //原来是30px
        }