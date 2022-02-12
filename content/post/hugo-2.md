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