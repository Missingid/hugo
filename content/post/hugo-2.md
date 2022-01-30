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
## 修改菜单栏上方距离

在assets-scss-partials-menu.scss中修改

    .menu {
    	······
        @include respond(xl) {
            margin-top: 10px; //原来是30px
        }