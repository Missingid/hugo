+++
categories = ["搬家日记"]
date = 2022-01-27T16:00:00Z
description = "在Hugo+Vercel+Waline搭建博客过程中，我遇到的问题和解决方法。"
draft = true
image = "/uploads/jesse.jpg"
tags = ["Hugo", ""]
title = "Hugo | 那些我踩过的坑"

+++
# Waline

* Hugo博客的config.yaml文件中需要填写waline的ServerURL，这里最好填Vercel DOMAINS最简单最原始的那个，这样无论Redeploy多少次config.yaml都不需要反复修改。我最开始在ServerURL后面填的网址超级复杂，且经过Redeploy后这个网址失效了，并没有跟随Redeploy自动更新。