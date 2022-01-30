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

# 左侧栏

## 社交账号icon居中

在assets-scss-partials-menu.scss中修改

## 修改菜单栏上方距离

在assets-scss-partials-menu.scss中修改

    .menu {
    	······
        @include respond(xl) {
            margin-top: 10px; //原来是30px
        }