+++
aliases = []
author = ""
categories = []
date = 2022-01-28T16:00:00Z
description = "在Hugo+Vercel+Waline搭建博客过程中，我遇到的问题和解决方法。"
draft = true
image = "/uploads/tsn5.jpg"
series = []
slug = "hugoblog_1"
tags = ["Hugo"]
title = "Hugo | 那些我踩过的坑"

+++
## Github Desktop

* Files-Options-Accounts中登录Github账号时，Chrome浏览器一直无法跳转，最后的解决方法是在Windows系统设置里把默认浏览器调成了Edge，秒跳转······

## Walinee

_多写一个e是因为直接写waline会在这一块出现评论区，怪事，怪事！_

* Hugo博客的config.yaml文件中需要填写waline的ServerURL，这里最好填Vercel DOMAINS最简单最原始的那个，这样无论Redeploy多少次config.yaml都不需要反复修改。我最开始在ServerURL后面填的网址超级复杂，且经过Redeploy后这个网址失效了，并没有跟随Redeploy自动更新。
* [设置邮箱提醒](https://gregueria.vercel.app/posts/decoration/)时注意：很多邮箱都要先开启SMTP服务（至少QQ邮箱、Gmail需要），我设置QQ邮箱自动提醒失败了······也不知道是哪步出了错。不过我按照前面朋友的教程，设置Gmail邮箱自动提醒成功了！

## Hugo

* 在根目录中创建的东西，只要跟theme文件夹中的同路径同名，Hugo都会以根目录中的优先级为先，所以装修的正确操作是在根目录下新建同名文件，这样在theme原作者更新后直接换掉theme文件夹不影响已做出的改动。
* 修改头像：config.yaml文件中对应的是sidebar-avatar-src，图片存放位置为assets/img。