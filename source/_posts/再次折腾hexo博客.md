title: 再次折腾hexo博客
date: 2014-08-27 00:40:18
categories: 折腾
tags: [hexo, 有意思, tips]
---

上次重装系统之后遇到`hexo generate`有问题，没有解决，干脆就重新搞一个，重新熟悉一下hexo建站流程。（PS：不过意外看到[hexo deploy命令报错](http://heamon7.com/2014/08/02/hexo-deploy-error/)这篇文章，有可能可以解决我的问题）

<!--more-->

重装过程中主要参考了

1. [不如-hexo你的博客](http://ibruce.info/2013/11/22/hexo-your-blog/)
2. [Zippera's blog-hexo系列教程](http://zipperary.com/categories/hexo/)
3. [Alimon's Blog-使用hexo搭建博客](http://yangjian.me/workspace/building-blog-with-hexo/)
4. [heamon7's Utopia-hexo分类](http://heamon7.com/categories/Hexo/)
5. [Jark's blog-hexo分类](http://wuchong.me/categories/Hexo/)


以下重装过程中的Tips

## 环境 ##

1. 新建`blog`目录，需要顺序执行`hexo init`和`npm install`两个命令
2. 部署时（`hexo deploy`）遇到“`blog`文件夹不包含`.git`目录”的问题，只要在`blog`文件夹和`.deploy`文件夹内都新建git工程即可。
3. 无法在github上生成静态网页：github上的工程名必须是`username.github.com`或者`username.github.io`，否则新建的博客页面必须push到`gh-pages`分支下，且网址会变成`username.gihub.io/project_name`

## 配置 ##

1. 生成post时默认生成categories配置项：在`scaffolds/post.md`中，添加一行`categories:`。同理可应用在`page.md`和`photo.md`。
2. 导航栏添加“关于”：
  1. `hexo new page "about"`
  2. 到`source/about/index.md`编辑内容
  3. 在`themes/light/_config.yml`中，添加
     menu:
     关于: /about

3. 主页文章显示摘要：在要作为摘要的文字后面添加`<!--more-->`即可。
4. 在`TAG CLOUD`中存在已经删除的标签：需要重新生成博客文章：`hexo clean` -> `hexo g` -> `hexo d`


