---
layout: post
title:  "git学习笔记1"
subtitle: 
date:   2015-12-30 11:16 AM
categories: [Tech]
---
研究报告、论文、代码，都是需要长线发展，一点点更新、修改、打磨的项目，无法一夜之间大笔一挥，一蹴而就。为求稳妥，每做一点修改，都会把文件另存为，取名为ver1、ver2、ver3、ver4..., 把它跟旧版本区分开来。这样一来，一篇报告，一个程序，往往有N个不同的版本。时间长了，根本不知道每个版本都有哪些改动。而某个版本出现了bug，想要回看历史版本，也不知该从何看起。版本管理系统就是为了应对这样的需求而设计。版本管理，顾名思义，管理的是文件的各个历史版本。有了它，可以很方便地回看、储存和编辑同一个文件的历史版本。甚至，论文、程序写坏了都不要紧，还原到之前的稳妥版本就行。下面提到的git就是这样一个版本管理系统。

###git系统简介  
git是一个分布式版本管理系统。**分布式**是相对**集中式**而言的。一个集中式的管理系统，文件的历史版本全部存在中央服务器中。需要从中央服务器下载先需要修改的文件，进行修改。而每做一次修改，又需要将修改的文件上传到中央服务器。集中式管理系统使用起来并不方便也不安全，因为它必须联网才能工作，而要是中央服务器坏了，所有的历史记录都没了。而分布式系统的优势在于，它没有中央服务器，每个用户的电脑里都保存着完整的文件历史版本的记录，完全可以离线操作。用户之间可以相互分享文件的历史记录。如果某个人的电脑坏了，历史记录没了，从其他人的电脑上把历史记录拷贝过来就行。 

###git工作方式  
想保存某一版本的文件，用git给这个版本拍张‘快照’，生成一个commit。git会储存这些快照，想回到过去的文件版本，访问该版本的commit ID即可。而何时拍张快照、建立commit完全取决于使用者本人。一般来说，每个logical change对应一个commit。

如何建立commit，给当前的文件‘咔嚓’拍张快照呢？这需要了解git的三个区域:   

* 工作区（working directory）  
存放正在编辑修改的文件

* 暂存间（stage/index）  
类似于缓存空间，修改好的文件，一开始需要提交至暂存区  

* HEAD   
最终，commit（快照）将保存在这里  

因此，建立commit分两步走： 
 
1. 将工作间里需要commit的文件，添加到暂存区  

2. 将暂存区的文件提交至HEAD

 
###git入门操作

####安装  
登陆[git下载页面](http://git-scm.com/downloads), 下载安装。安装好后，在terminal中输入：  
 
    $ git --version  
   
如果terminal给出git的版本号，如：  

    git version 2.6.3  

则安装成功. 

####建立git仓库  
存放文件的文件夹，在git里叫做仓库（repositary）。仓库可以是已经建立好的文件夹，也可以新建。版本管理的第一步，是初始化仓库。将工作路径设置为需要版本管理的某文件夹的路径，在terminal输入：  

    $ git init  
    
terminal会显示：  

    Initialized empty Git repository in /Users/shuang/introgit/.git/
    
一个仓库就建好了 ：）
  
####添加文件到暂存区  
将文件添加至暂存区，使用指令`git add`加上需要添加的文件名，如：

    $ git add readme.txt
 
`git add`一次只能添加一个文件。想要一次性添加文件夹内（仓库内）的所有文件，可以输入：  

    $ git add .
    
这时，可以使用指令`git status`，查看当前git状态：

    $ git status  

将得到如下信息：  

    On branch master

    Initial commit

    Changes to be committed:
      (use "git rm --cached <file>..." to unstage)

	new file:   readme.txt

on branch master，意思为在master分支 （目前可先不理会分支）。initial commit，表明这是初次提交的commit。changes to be commited表示新文件readme.txt已经放到了暂存区，可以commit到HEAD了。

####提交文件至HEAD  
使用`git commit -m "commit message"`，将暂存区中的文件，提交至HEAD。在`-m`后面，添加该次commit的备注，说明此次commit做了何种改动。`git commit`可以一次性将暂存区中的多个文件，一并提交。  

    $ git commit -m "Add readme.txt file"
    [master (root-commit) 78122e2] Add readme file
     1 file changed, 1 insertion(+)
     create mode 100644 readme.txt
 
命令执行成功后，会告知一个文件有改动，有1行添加的内容。

这时输入`git status`查看git状态，会得到：

    $ git status
    On branch master
    nothing to commit, working directory clean
    
这时，工作区的文件没有改动。暂存区的文件，在上一次commit之后已经清空。因此，当前的状态是没啥可commit（nothing to commit）。   

####查看commit历史记录  
可以使用`git log`查看commit的记录。

    $ git log
    commit b8b0082e51f2afdf1c1f8b9ba44023d68a9fd6a8
    Author: 
    Date:   Wed Dec 30 18:01:14 2015 +0100

    Add game file

    commit 78122e28a7dd941711d8c34b57ca8c9de1b128dd
    Author: 
    Date:   Wed Dec 30 17:46:29 2015 +0100

    Add readme file

历史记录是按照时间顺序由新到旧排列。commit后面的一系列字符串，即是每个commit的ID，可以根据ID，回访文件的历史版本。Author一栏会给出每次commit的作者信息，这在多人协作的项目中比较有用。该指令也会显示每个commit的备注信息，每个commit到底做了什么改动，一目了然（前提是最初设置的备注信息要清晰明白）。

####比较不同版本的文件  
版本多了，我们可能需要了解两个版本之间到底有哪些差异，这时需要用到`git diff commit_id1 commit_id2`。`git diff`会比较commit_id2比commit_id1增加了或减少了哪些内容。如果想要比较新版本较之于旧版本做了哪些改动，commit_id1写较旧那个版本的commit id。

    $ git diff b8b0082e51f2afdf1c1f8b9ba44023d68a9fd6a8  6e088c0c257b1322f89c2f17af789b2a960bd961
    diff --git a/game.py b/game.py
    index 7f5651b..83c850b 100644
    --- a/game.py
    +++ b/game.py
    @@ -1,2 +1,6 @@
     #print hello world
    -#this is an introductional file
    \ No newline at end of file
    +#this is an introduction file
    +
    +i = 0
    +for i in range(4):
    + print i + 1
    \ No newline at end of file

**+**表示新版本较旧版本增加的内容  
**-** 表示新版本较旧版本删除的内容

####回到历史版本
输入指令`git checkout`加上commit id，就能回到该版本：

    $ git checkout 78122e28a7dd941711d8c34b57ca8c9de1b128dd
    Note: checking out '78122e28a7dd941711d8c34b57ca8c9de1b128dd'.

    You are in 'detached HEAD' state. You can look around, make experimental
    changes and commit them, and you can discard any commits you make in this
    state without impacting any branches by performing another checkout.
    
    If you want to create a new branch to retain commits you create, you may
    do so (now or later) by using -b with the checkout command again. Example:
    
      git checkout -b <new-branch-name>
    
    HEAD is now at 78122e2... Add readme file
 
这时回到仓库，打开文件，会发现它已经回到了历史版本 ：）   
git会吐出一堆内容，涉及到分支的知识，先暂时不管它啦。

拥有这些知识，就已经可以着手管理自己的文件啦！

###参考资料：  
Udacity课程: [How to use Git and Github](https://www.udacity.com/course/how-to-use-git-and-github--ud775)  

廖雪峰的[git教程](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)