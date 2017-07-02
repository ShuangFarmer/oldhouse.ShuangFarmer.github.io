---
layout: post
title:  "如何用 GitHub 和 jekyll 搭建博客"
subtitle: 
date:   2016-07-18 09:18 PM
categories: [Tech]
---
借助 GitHub 平台和 jekyll 静态网站主题模板，10分钟不到就能搭出一个博客。然，搭博客容易，个性定制博客却难上加难。若无 HTML, CSS 相关基础，只能连猜带蒙，小修小补，勉力拼凑。也罢也罢，博客嘛，积累优质博文才是正经事~   

## 搭建博客步骤  

- fork 心仪的博客仓库  
- clone 到本地  
- 本地修改 `_config.yml` 文件中的个人信息  
- 在 `CNAME` 中添加个性域名  
若 fork 的仓库中无 `CNAME` 文件，进入本地仓库目录，在 terminal 中输入如下代码。在新生成的 `CNAME` 中添加域名。  
  
```
touch CNAME
```     

- 在 `_posts` 中添加博文  
	- 博文文件名需依照格式 `date-title.md`，如 `2016-07-19-summer.md`，否则 Jekyll 无法正确识别读取文件，  
	- 博文头部需添加 `YAML 编码`  

``` 
---
layout: post  
title: 中文简要排版参考
categories: [blog]  
tags: [Chinese, Read, ]
description:
---
正文在这里开始~
``` 
- push 本地内容到 GitHub  
- 访问网址 `username.github.io` 或者 在 `CNAME` 文档中添加的个性域名，就可以看到自己的博客啦~  

## 本地预览 
发布博文的路径稍有繁琐：
  
> 本地修改 -> 同步到 GitHub 端 -> 访问博客网址 -> 查看修改效果

若持续检查修改博文，需要反复 commit 反复 push ，老辛苦了。有没有什么法子，能在本地预览博客网页效果了呢？有哒！  

- 安装 Jekyll 到本地 

```  
$ gem install jekyll   
```  
-  进入本地博客仓库    

```
$ cd Documents/.../username.github.io   
```

- 使用 jekyll 本地浏览服务   
 
```
$ jekyll serve     
```    

- 用浏览器访问 server address: <http://127.0.0.1:4000/> 查看网页

在 Mac 系统下安装 jekyll 可能因没有 permission 而失败。可以根据 jekyll 官方文档 [troubleshooting](https://jekyllrb.com/docs/troubleshooting/) ，尝试输入： 

```  
$ sudo gem update --system # update RubyGems  
$ xcode-select --install # if still have problems, download and install new Command Line Tools  
$ sudo gem install jekyll # install jekyll
```  

`sudo` 似乎是个需要慎用的命令？不懂啦……    

以及，遇到问题要先查阅 **官方文档** 呀！在 stackoverflow 上绕得一头雾水，糊里糊涂输了一些代码，安装了一些软件，依然没有解决问题……最后，发现人家官方文档早就给出最优解决方案了 T^T