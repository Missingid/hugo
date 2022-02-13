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

* VS Code全文件夹搜索，非常好用，可以快速定位关联代码

## 正文

### 正文图片缩小

在assets\\scss\\partials\\layout\\articles.scss中修改max-width：

    .article-content {
    	margin: var(--card-padding) 0;
    	color: var(--card-text-color-main);
        img {
          max-width: 90%; //原来是100%
          height: auto;
        }
    }

### 代码块颜色修改

我在Issues随意乱逛的时候看到有网友将light模式下代码块颜色调浅，非常好看！火速抄个作业->在custom.scss文件中加入：

    [data-scheme="light"] {
        .article-content pre{
            --pre-background-color: #fafafa;
            --pre-text-color: #272822;
        }
    }

## 左侧栏

### 社交账号icon居中

在assets\\scss\\partials\\menu.scss中新加一行：

    .social-menu {
        list-style: none; 
        padding: 0%;
        display: flex;
        flex-direction: row;
        gap: 10px;
        justify-content:center; //新加的
    }

### 修改菜单栏上方距离

在assets-scss-partials-menu.scss中修改margin-top：

    .menu {
    	······
        @include respond(xl) {
            margin-top: 10px; //原来是30px
        }

### Related Content

根据[Hugo的官方说明文档](https://gohugo.io/content-management/related/)，文章之间可以按照tags/categories/date等因素计算出加权的Related值，如果该值大于阈值，该文章会被加入到下方的Related Content。我们可以在config.yaml中找到下面这段代码，修改每个因素对应的权重以及阈值：

    related:
        includeNewer: true
        threshold: 50 #原来是60
        toLower: false
        indices:
            - name: tags
              weight: 200 #原来是100
            - name: categories
              weight: 100 #原来是200

比如我之后不打算保留categories，可以将tags权重调高，将categories权重降低。

### 去掉About

本人真的很不会自我介绍···对着About界面发呆半小时也不知该说些什么，索性删掉。根据[Jimmy的自定义菜单指南](https://docs.stack.jimmycai.com/zh/configuration/custom-menu)，About、Archive以及Links页面都是由/content/page下的md文件控制。这里说一句题外话，config.yaml中的menu部分只显示了Home一栏，About等都在各自的md文件中······我一直以为是我眼神不好没找到，大哭 : (

弄明白这个后，自定义菜单栏就很简单啦！比如我这里不想要About，只需在About文件夹中的index.md把menu注释掉。

    title: About
    description: Hugo, the world's fastest framework for building websites
    date: '2019-02-28'
    aliases:
      - about-us
      - about-hugo
      - contact
    license: CC BY-NC-ND
    lastmod: '2020-10-09'
    #menu:
    #    main: 
    #        weight: -90
    #        params:
    #            icon: user

## 右侧栏

### Search字号/边框大小调整

在assets\\scss\\partials\\layout中找到search文件，修改以下部分：

    .search-form {
        &.widget {
            label {
                font-size: 1.8rem; //改字号
                top: 10px;
            }
    
            input {
                font-size: 1.4rem; //改字号
                padding: 40px 20px 30px 20px; //改边框大小
            }
        }
    
        label {
            position: absolute;
            top: 25px; //改
            left: 20px;
            font-size: 1.8rem; //改Search字号
            color: var(--card-text-color-tertiary);
        }
    
        input {
            padding: 60px 20px 20px; //改
            font-size: 1.6rem; //改Search下方字号
        }

## Icon

### 从Tabler Icons上获取美丽图标

根据[Jimmy的指南](https://docs.stack.jimmycai.com/zh/configuration/custom-menu.html#%E9%85%8D%E7%BD%AE%E5%9B%BE%E6%A0%87)，Stack主题使用的Icon来自于[Tabler Icons](https://tablericons.com/)。如果想自行修改，可以点击Tabler Icons网页上的图标，此时图标下方会出现“copied”字样，说明该图标的信息我们已拷贝完全。然后回到assets/icons中新建html文件（注意后缀是.svg），将上述信息复制上去，保存，即可获得美丽图标。

### Icon的暗色模式

其实我一直没发现这个问题，小鱼提醒之后我才意识到——噢！怎么自己添加的icon不会随着暗色模式变化啊！

还是在Issues里抄到了答案（真的意想不到！)，美美附上一个[作业链接](https://github.com/CaiJimmy/hugo-theme-stack/issues/218)，在此为这位热心网友送上赛博感谢！

只需要修改svg文件代码，无需改动博客的任何代码：在svg文件中将stroke设置为stroke="currentColor"，这样icon color可以自动匹配随着环境模式（暗色模式 or 亮色模式）。

## 修改Archives

### 将Archives中的Categories改为Tags

成功删除About后，我似乎逐渐开窍。Archives的md文件显示，layouts对应的是archives.html，点开后看到第一块中赫然立着“categories”，这就是我们要找的东西！

    {{- $taxonomy := $.Site.GetPage "taxonomyTerm" "tags" -}} //这里将categories改成tags
    {{- $terms := $taxonomy.Pages -}}
    {{ if $terms }}
    <h2 class="section-title">{{ $taxonomy.Title }}</h2>
    <div class="subsection-list">
    	<div class="article-list--tile">
    		{{ range $terms }}
    			{{ partial "article-list/tile" (dict "context" . "size" "250x150" "Type" "taxonomy") }}
    		{{ end }}
    	</div>
    </div>
    {{ end }}

将categories改成tags，一试，大功告成！archives界面的第一块成功按照tags进行排序。

后续我根据[Jimmy的指南](https://docs.stack.jimmycai.com/zh/taxonomy/)，给tags加上图片。注意slug不要随意写，不然网址对不上，tag会以article的形式展开。建议只写title、description和image。

## 友情链接

### 给友情链接底部加上评论区

作业我抄的[Bore的这篇](https://bore.vip/archives/3bf3725e/#%E6%B7%BB%E5%8A%A0%E5%8F%8B%E6%83%85%E9%93%BE%E6%8E%A5-shortcodes)，注意到layouts\\page\\links.html里有这样一段：

        {{ if or (not (isset .Params "comments")) (eq .Params.comments "true")}} 
            {{ partial "comments/include" . }}
        {{ end }}

我：肯定是和友链评论有关！

火速在content\\page\\links文件夹里找到对应的md文件，修改如下：

    ---
    title: 友情链接
    description: 快来和我做互联网邻居！
    date: '2022-02-12'
    slug: links
    layout: links
    license: false
    toc: true #目录显示
    comments: true #评论显示
    enabled: #想保持右侧栏不动，但目前尚未搞定
        - search
        - toc
        - archives
        - tag-cloud
    menu:
        main: 
            weight: -70
            name: Friends
            url: /
            params:
                icon: friends
    ---

最后将links.html的comments段落改为：

    {{ partial "comments/include" . }}

这样就可以在评论区直接交换友链啦，是不是很方便。

### 友链右侧边栏来啦

闲逛的时候逛到[这位朋友的博客](https://blog.mysto.cyou/posts/211102-blogsearch/)，看到“问题不大”那块，我突然灵光一闪。这个{{ define XXX }}感觉好眼熟！我肯定在哪见过。于是速速打开links.html，果然有。昨天我捯饬很久，右侧边栏却一直在评论区下方，原来是我把right-sidebar的生成代码放在了main里。

让我来一步步讲解原理！

Stack原有的主题在打开文章后，右侧边栏只会显示目录，也就是toc，widget都会消失。之前我已经通过抄塔塔的教程[《调整文章页面的显示样式》](https://mantyke.icu/2021/f9f0ec87/#%E8%B0%83%E6%95%B4%E6%96%87%E7%AB%A0%E9%A1%B5%E9%9D%A2%E7%9A%84%E6%98%BE%E7%A4%BA%E6%A0%B7%E5%BC%8F)，在文章页面搞出了widget，那么，要在友情链接页面搞出widget，只需要依葫芦画瓢，将生成widget的代码复制粘贴到links.html就可以了！

一一对比后，我发现文章界面的widget生成代码在single.html中：

    {{ define "right-sidebar" }}
        <!-- {{ if (.Scratch.Get "hasTOC") }}
            <aside class="sidebar right-sidebar sticky">
                <section class="widget archives">
                    <div class="widget-icon">
                        {{ partial "helper/icon" "hash" }}
                    </div>
                    <h2 class="widget-title section-title">{{ T "article.tableOfContents" }}</h2>
                    
                    <div class="widget--toc">
                        {{ .TableOfContents }}
                    </div>
                </section>
            </aside>
        {{ else }}
            {{ partial "sidebar/right.html" . }}
        {{ end }} -->
        {{ partial "sidebar/right.html" . }}
    {{ end }}

将这段代码复制到links.html中，右侧边栏就出现啦！

**_注意不要复制到{{ define "main" }}里，这俩是平行关系。_**

## 引用

跟着[塔塔的教程](https://mantyke.icu/2021/a08f1963/)改变了引用格式，但用<br>换行一直不对，在此留下一个大疑点！

最后我使用的替代方法非常奇怪，在塔塔写的quote的scss中加入这一段：

    blockquote.quote {
        position: relative;
        margin: 1.5em -10em 0 -10 ;
        padding-left: 18%;
        padding-right: 18%;
        border: none;
        background-color: transparent;;
        //p块为新加，主要起作用的是margin:0 auto
        p{
            text-align: left;
            margin-top: 1.5em;
            margin-bottom: 1.5em;
            margin: 0 auto;
        }

然后直接空行，如：（实际使用时quote左右都是两个花括号）

    {< quote >}
    名称：Missing不想睡
    
    网址：https://hugo-missingid.vercel.app/
    
    简介：和我一起做赛博宵夜吧!
    
    头像：https://github.com/Missingid/hugo/issues/1
    
    {< /quote >}

最后的效果和换行一样！

今晚（2月13日）还学到一个基础技巧，**markdown里自带的引用语法是>**，好简单！