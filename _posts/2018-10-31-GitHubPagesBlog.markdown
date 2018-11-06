---
layout: post
title: "GitHub Pages + jekyll + gulp 搭建个人博客网站"
date: 2018-10-31 15:30:08 +0800
description: GitHub Pages + jekyll + gulp 搭建个人博客网站
tags: [技术,前端]
img: import/GitHubPages.jpg
---

    关于GitHub+jekyll搭建博客的文章网上已经很多了，但是我发现大部分文章思路不是很清晰，而且总是贴一些概念，不便于理解。所以我就以我搭建博客的经历重写了一篇文章，希望能对大家有帮助。

## 首先，我们为什么要搭建博客网站？

这个问题我们换个问法是——为什么写博客？这个问题应该是我们首先需要明确的，当然，看这篇文章的人肯定已经对写博客抱有兴趣了，但我还是想让大家清楚的知道自己的目的以及这样做带来的好处，我这里推荐阅读前端教育启蒙界三驾马车之一阮大神的文章——<a href="http://www.ruanyifeng.com/blog/2006/12/why_i_keep_blogging.html" target="_blank">为什么要写Blog？ - 阮一峰的网络日志</a>

好了，清楚了我们即将要做的事情的意义之后，我们就进入正题。

## 如何搭建？

我得说声抱歉，因为这篇文章的起点是你需要懂一些前端知识例如git与html，如果你是小白的话，这篇文章可能对你并不太友好，但是，如果你有耐心，愿意按照我的步骤一步步来的话，我相信这问题不大。我尽量写的通俗易懂，细化每一步流程。

**整个过程其实是三件事**

1. 首先是利用GitHub Pages提供的服务托管我们的页面

2. 然后是本地搭建jekyll环境

3. 最后是美化和工程化管理我们的项目

在这里，我会把这三步分开做，最后再组合，这样做我觉得会有助于我们学习理解。

### 一、玩转GitHub Pages

GitHub Pages是一个静态站点托管服务，功能是我们可以把写好的网页放到这里，概念介绍我就不贴了，具体请见<a href="https://help.github.com/articles/what-is-github-pages/" target="_blank">What is GitHub Pages?</a>

#### 1.拥有你的GitHub账号

<a href="https://github.com/join?return_to=%2Fjoin&source=login" target="_blank">GitHub注册地址</a>

![注册GitHub](/assets/img/import/注册GitHub.jpg "注册GitHub")

强调一点，名字很重要，与你之后博客的地址息息相关，如果你不设置自己的域名， `username` + .github.io就是你的博客地址。

#### 2.创建仓库

两个入口都可以进入创建仓库的页面

![开始项目](/assets/img/import/开始项目.jpg "开始项目")

仓库名字的话我建议你按照这个格式username.github.io，当然，这不是必要的，如果你取了其他的仓库名字，那么，访问地址就会变为https://username.github.io/仓库名字/

![创建仓库](/assets/img/import/创建仓库.jpg "创建仓库")

获取git地址

![获取git地址](/assets/img/import/获取git地址.jpg "获取git地址")

#### 3.添加文件

创建好仓库之后，我们就能在本地做修改了，接下来的操作我习惯用命令行实现，你也可以用其他工具。（小白的话可以尝试GitHub的官方工具<a href="https://desktop.github.com/" target="_blank">GitHub Desktop</a>图形化操作，很方便，网上的教程很多，在此我就不赘述了。如果你是连git是什么都不知道的白又白，那也没关系，知识咱们是可以慢慢学的嘛，推荐你阅读<a href="https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000" target="_blank">Git教程 - 廖雪峰的官方网站</a>）

* 切换到你想存放的目录

{% highlight ruby %}
~ $ cd Documents/project/demo/
{% endhighlight %}

* 克隆你的仓库

{% highlight ruby %}
~ $ git clone https://github.com/username/username.github.io
{% endhighlight %}

* 进入克隆出的目录并添加一个index.html文件

{% highlight ruby %}
~ $ cd chen-ba-dou.github.io
~ $ echo "Hello World" > index.html
{% endhighlight %}

* 添加、提交和推送你的更改

{% highlight ruby %}
~ $ git add --all
~ $ git commit -m "first commit"
~ $ git push -u origin master
{% endhighlight %}

附上操作记录

![操作记录](/assets/img/import/操作记录.jpg "操作记录")

好了，这会儿你已经可以看到你新添加的页面了，地址是username.github.io。

![GitHubPages部署成功](/assets/img/import/GitHubPages部署成功.jpg "GitHubPages部署成功")

至此，我们已经完成了第一部分的工作，其实你已经可以提前享受成功的喜悦了，因为通向读者的路已经修通，接下来只是页面编写方式与是否美观的问题了。

### 二、搭建jekyll环境

首先，我们需要知道，我们为什么要用jekyll以及它能帮我们做什么？

上面我们创建了一个托管我们代码的仓库，但是我们最终的目的是专注的写blog，仅仅有一个发布环境这还不够，我们还需要一个博客的模板并启动一个可以让我们边写边看的本地服务，我们来让jekyll帮我们做这个工作。

#### 1.安装jekyll

**确保你在系统里有下面这些配置**

* Ruby
* RubyGems
* Linux, Unix, or Mac OS X

>### 在 Windows 下使用 jekyll
你可以使用 jekyll running on Windows, 但是官方文档并不建议你在 Windows 平台上安装 jekyll。

如果你有以上配置，那jekyll的安装就非常简单了，你只需使用RubyGems在命令行输入以下命令就完成了jekyll的安装

{% highlight ruby %}
~ $ gem install jekyll
{% endhighlight %}

#### 2.创建最简单的jekyll模板

我们假定项目名字为jekyll_demo，你也可以取你想取的名字

{% highlight ruby %}
~ $ jekyll new jekyll_demo
~ $ cd jekyll_demo
~ $ jekyll serve
{% endhighlight %}

ok，现在你就可以去<a href="http://localhost:4000" target="_blank">http://localhost:4000</a>上查看效果了。

![jekyll简单首页](/assets/img/import/jekyll简单首页.jpg "jekyll简单首页")
![jekyll简单正文](/assets/img/import/jekyll简单正文.jpg "jekyll简单正文")

怎么样，是不是很简单？

#### 3.修改jekyll配置

上面创建了一个最简单的jekyll实例，但是这并不是我们想要的，我们想要一个携带有个人信息的博客网站。这时候我们需要了解一下jekyll的结构以及配置文件了。

一个基本的 Jekyll 网站的目录结构一般是像这样的：

{% highlight ruby %}
.
├── _config.yml
├── _posts
|   └── 2018-10-31-welcome-to-jekyll.markdown
├── _site
└── index.html
{% endhighlight %}

我们需要修改_config.yml文件，这里是jekyll的基本配置，以下是我修改的示意图，供大家参考。

![jekyll基本配置修改_首页](/assets/img/import/jekyll基本配置修改_首页.jpg "jekyll基本配置修改_首页")

_posts文件夹下面是你的文章，文件格式很重要，必须要符合：YEAR-MONTH-DAY-title.markdown。文章需要用markdown语法书写，如果你不熟悉，不用担心，这很简单，你只需记住常用写法就ok了，剩下的可以等用到的时候再查markdown的文档。

![jekyll基本配置修改_正文](/assets/img/import/jekyll基本配置修改_正文.jpg "jekyll基本配置修改_正文")

这样，一个最简单的博客就完成了。

![jekyll搭建成功_首页](/assets/img/import/jekyll搭建成功_首页.jpg "jekyll搭建成功_首页")
![jekyll搭建成功_正文](/assets/img/import/jekyll搭建成功_正文.jpg "jekyll搭建成功_正文")

jekyll详细文档请见jekyll官网<a href="https://www.jekyll.com.cn" target="_blank">Jekyll • 简单的博客、静态网站工具</a>

### 三、美化博客模板和工程化项目

#### 1.美化博客模板

现在，我们已经把博客发布地址和本地博客的配置搞定了，现在只需把这两步组合到一起，然后推送到远端，你就完成了一个最基本的博客了。

但是，这可能还没有满足我们的需求，我们一定希望我们的博客页面美观优雅，这样会使我们的读者赏心悦目。美化的话，你可以直接选择别人写好的博客模板，这样省时省力，如果你想自己设计你的博客网站，你也可以自己写样式，因人而异。我提供我的博客模板引入方法，如果你觉得我的模板不符合你的心意，你可以在<a href="http://jekyllthemes.org" target="_blank">jekyll主题</a>选择其他主题。

引入方法很简单，你只需在我的仓库<a href="https://github.com/ChenBaDou/ChenBaDou.github.io" target="_blank">https://github.com/ChenBaDou/ChenBaDou.github.io</a>点击右上角fork按钮

![fork项目](/assets/img/import/fork项目.jpg "fork项目")

接下来在导航条最右侧settings里修改项目名称 `username` + .github.io。

![修改项目名称](/assets/img/import/修改项目名称.jpg "修改项目名称")

好了，现在你已经可以访问 `username` + .github.io了。当然，现在博客的信息和内容还都是我的，接下来你需要重复第一步，把这个库clone到本地，再重复第二步，修改项目的_config.yml文件和_posts文件下面的博客文章，写好博文之后你只需要推送到远端就可以看到自己发表的博文了。


#### 2.工程化项目

我的项目使用gulp作为自动化工具，你也可以选择其他的自动化工具，比如grunt，看个人喜好。

在你上一步fork我的项目时，gulp的配置都已经clone过去了，这里你可以不做改动，直接用我写好的配置，gulp会帮你做sass转换、压缩css与图片、浏览器同步等工作。因为本文主体是搭建博客，工程化我就不多说了，有关gulp的详细配置，我准备之后写一篇博客单独介绍。

因为我们已经配置好了gulp的配置文件，我们这里直接用gulp启动项目。

* 切换到你的项目目录

{% highlight ruby %}
~ $ cd username.github.io
{% endhighlight %}

* 安装必要的包

{% highlight ruby %}
~ $ npm install
{% endhighlight %}

* 启动项目

{% highlight ruby %}
~ $ gulp server
{% endhighlight %}

    以上，我们就成功搭建了一个免费的博客网站，尽情享受写博客的乐趣吧。

















