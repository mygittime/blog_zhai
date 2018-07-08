# LessOrMore

博客访问地址:https://mygittime.github.io/blog_zhai/


致谢
====================================
+ 感谢[Less官网](http://lesscss.cn/)的样式，本Jekyll框架的样式都是基于Less官网的样式直接拷贝过来的。只是重构了JS，并且加入了Jekyll语法而已。
+ 感谢[Github](https://github.com/)提供的代码维护和发布平台
+ 感谢[Jekyll](https://jekyllrb.com/)团队做出如此优秀的产品
+ 感谢[Solar](https://github.com/mattvh/solar-theme-jekyll)的原作者[康志华](https://github.com/luoyan35714)，在我开始编写博客时为我提供这么好的模板


使用
====================================

下载
------------------------------------

使用git从[LessOrMore](https://github.com/luoyan35714/LessOrMore.git)主页下载项目

``` bash
git clone https://github.com/luoyan35714/LessOrMore.git
```

配置
------------------------------------

`LessOrMore`项目需要配置的只有一个文件`_config.yml`，打开之后按照如下进行配置。

> 特别注意`baseurl`的配置。如果是`***.github.io`项目，不修改为空''的话，会导致JS,CSS等静态资源无法找到的错误

``` bash
name: 博客名称
email: 邮箱地址
author: 作者名
url: 个人网站
### baseurl修改为项目名，如果项目是'***.github.io'，则设置为空''
baseurl: "/LessOrMore"
resume_site: 个人简历网站
github: github地址
github_username: github用户名称
FB:
  comments :
    provider : duoshuo
    duoshuo:
        short_name : 多说账户
    disqus :
        short_name : Disqus账户
```

如何写文章
------------------------------------

在`LessOrMore/_posts`目录下新建一个文件，可以创建文件夹并在文件夹中添加文件，方便维护。在新建文件中粘贴如下信息，并修改以下的`titile`,`date`,`categories`,`tag`的相关信息，添加`* content {:toc}`为目录相关信息，在进行正文书写前需要在目录和正文之间输入至少2行空行。然后按照正常的Markdown语法书写正文。

``` bash
---
layout: post
#标题配置
title:  标题
#时间配置
date:   2016-08-27 01:08:00 +0800
#大类配置
categories: document
#小类配置
tag: 教程
---

* content
{:toc}


我是正文。我是正文。我是正文。我是正文。我是正文。我是正文。
```

执行
------------------------------------

``` bash
jekyll server
```

效果
------------------------------------
打开浏览器并输入URL`http://localhost:4000/`,回车。


为什么要写博客
====================================

人到中年不得已，保温杯里泡枸杞！最近明显感觉记忆力大不如前，平时用过的技术点，过一段时间不用就忘记怎么用了。博客就当是自己的技术仓库，随用随取。在这里不得不吐槽一下百度，搜索问题90%的答案都是一个模板，然而还是不适用的，剩下的10%能不能搜到完全依据玄学，google是个不错的东西，可惜需要翻墙。和大多数人一样，我也喜欢免费的东西，但翻墙软件这个东西免费的真的是不太好用，在这里给大家推荐一种翻墙方式，`shadowsocks`。当然，这个不是免费的，需要的小伙伴可以在github上搜索一下，各种系统的都有。
关于作者
====================================

一个逐渐走上健身道路的前端工程师 

关于打赏
====================================

如果你也像我一样在寻觅一个简洁的博客主题。不妨试下LessOrMore。

当然你也可以为了我的工作打赏！以激励我写出更好的东西。

支付宝
----------------

<img src="/styles/images/zhifubao.PNG" alt="支付宝二维码付款给Freud" width="310" />

微信
----------------
![微信二维码付款给我](/styles/images/weixin.png)
