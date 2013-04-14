---
layout: post
title: "Build a Blog With Octopress on Github"
date: 2013-04-13 13:31
comments: true
categories: blog github octopress
---

_在开始前，请确认机器上已安装github, ruby, rvm._

##安装Octopress

#####从Github克隆Octopress

```
git clone git://github.com/imathis/octopress.git your_dir
cd your_dir
```
#####安装依赖的gems

```
gem install bundler
bundle install
```

#####安装默认主题

```
rake install
```

没有自定义主题么？稍后播出~

#####部署到Github

我自己的博客就使用了 [Github Pages](http://pages.github.com/), 使用git中的pull和push命令就可以提交自己的博客，Octopress的一键部署让整个过程更加方便。像程序员使用Github合作写代码一样，只要添加合作者，就可以多人合作维护一个博客。

在Github建立一个名为```username.github.io```的版本库，切记前面的名字要和你的Github用户名完全一样，因为Github Pages就靠这个生成静态页面，最终才可以通过```http://username.github.io```访问你的博客。

```
rake setup_github_pages
```
上面的命令做了这些事情：
1. 需要你提供Github Pages需要的版本库链接
2. 将指向imathis/octopress的分支从"origin"重命名并且重定向到“octopress”
3. 将你的Github Pages的版本库设置为默认的origin remote.
4. 将活跃分支从master切换到source
5. 根据版本库URL配置你的博客链接
6. 为部署建立一个master分支

**Note**: 在进行第一步时，我偷懒直接从Github拷贝了版本库URL——这个URL是有 ".git"后缀的.而该命令真正需要的是没有“.git”后缀的URL。我使用带.git后缀的URL，命令仍然看起来是成功了，但是没办法成功提交本地修改，折腾了俩小时。所以，切记要输入正确的链接，它看起来应该像这样， "git@github.com:username/username.github.io".

接下来运行：

```
rake gen_deploy
```

你的博客就被成功生成和部署啦！访问 http://username.github.io 就可以看到~

#####修改Octopress的配置

```
vi _config.yml
```

该文件中可以修改站点名称，作者等信息，还可以添加第三方插件的配置信息。

官方支持的第三方插件设置：

* Github - List your github repositories in the sidebar
* Twitter - Setup a sidebar twitter feed, follow button, and tweet button (for sharing posts and pages).
* Google Plus One - Setup sharing for posts and pages on Google’s plus one network.
* Pinboard - Share your recent Pinboard bookmarks in the sidebar.
* Delicious - Share your recent Delicious bookmarks in the sidebar.
* Disqus Comments - Add your disqus short name to enable disqus comments on your site.（这个是添加评论功能的，非常好用）
* Google Analytics - Add your tracking id to enable Google Analytics tracking for your site.
* Facebook - Add a Facebook like button

#####安装第三方主题

谷歌上搜索“octopress theme”，会有很多可选项。我使用了相对简约的主题 [slash](http://zespia.tw/Octopress-Theme-Slash/index_tw.html)，安装过程如下：

```
cd octopress
git clone git://github.com/tommy351/Octopress-Theme-Slash.git .themes/slash
rake install['slash']
rake generate
```

其他的主题安装方法类似，一般情况下他们的github页面上就会有安装指南。

#####修改主题

完全做出一个好用的主题模板比较复杂，日后可以分析下文件结构。在octopress中，使用者可以通过修改目录"sass/custom"下的 *.scss 文件来重写样式，比如颜色，字体及大小等其他的样式定义。如此，当使用者重新安装主题的时候，自定义的样式不会覆盖。

#####发表文章

发表文章之前，首先要安装markdown文件的编辑器。Mac用户推荐安装mou，Windows上没用过，google之后排位靠前的是MarkdownPad。

```
rake new_post[title]
```

生成新的文章，路径看起来是这样的```source/_posts/2013-04-13-build-a-blog-with-octopress-on-github.markdown```，用markdown编辑器打开，就可以写文章啦。

```
rake preview 预览文章
rake gen_depoly 生成并部署新的文章
```

#####添加评论

因为github上的页面都是静态的，评论的功能就得动用外部工具[Disqus](https://disqus.com/)，注册自己的域名和用户信息后，将注册时填写的“Site Shortname”复制到_config.yml文件中对应“disqus_short_name:”的位置就可以啦。

这里推荐一个小工具[Gravatar](https://en.gravatar.com/)，在这里上传自己的头像，会同步到很多其他的网站，省得以后一个个设置太麻烦。
我了解到的，它支持github，disqus，stachoverflow，别的没试过~

