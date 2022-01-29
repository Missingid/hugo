+++
aliases = []
author = ""
categories = ["搬家日记"]
date = 2022-01-27T16:00:00Z
description = "在Hugo+Vercel+Waline搭建博客过程中，我遇到的问题和解决方法。"
draft = true
image = "/uploads/tsn5.jpg"
series = []
slug = "hugoblog_1"
tags = ["Hugo", ""]
title = "Hugo | 那些我踩过的坑"

+++
## Github Desktop

* Files-Options-Accounts中登录Github账号时，Chrome浏览器一直无法跳转，最后的解决方法是在Windows系统设置里把默认浏览器调成了Edge，秒跳转······

## Walinee

_多写一个e是因为直接写waline会在这一块出现评论区，怪事，怪事！_

* Hugo博客的config.yaml文件中需要填写waline的ServerURL，这里最好填Vercel DOMAINS最简单最原始的那个，这样无论Redeploy多少次config.yaml都不需要反复修改。我最开始在ServerURL后面填的网址超级复杂，且经过Redeploy后这个网址失效了，并没有跟随Redeploy自动更新。
* [设置邮箱提醒]()时注意：很多邮箱都要先开启SMTP服务（至少QQ邮箱、Gmail需要），我设置QQ邮箱自动提醒失败了······也不知道是哪步出了错。不过我按照前面朋友的教程，设置Gmail邮箱自动提醒成功了！