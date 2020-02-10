
----------------------------------------------------------------------------------------------------
# 4.other part:
----------------------------------------------------------------------------------------------------

<<如何高效利用GitHub>> 
http://www.yangzhiping.com/tech/github.html

<<图解Git>>
https://my.oschina.net/xdev/blog/114383

## 阮一峰git系列

- <<常用 Git 命令清单>>
http://www.ruanyifeng.com/blog/2015/12/git-cheat-sheet.html

- <<Git远程操作详解>>
http://www.ruanyifeng.com/blog/2014/06/git_remote.html
```
git branch --set-upstream master origin/next

上面命令指定master分支追踪origin/next分支。
```
```
git push --all origin
git push --force origin  //感觉这个比较实用，看描述能删远程仓库的commit
git push origin --tags
```
- <<Git 使用规范流程>>
http://www.ruanyifeng.com/blog/2015/08/git-use-process.html

## 伯乐在线git系列

http://blog.jobbole.com/75348/

<<趣文：那些会用 Git 的动物>>
http://blog.jobbole.com/20123/

## 其他高级技巧或知识

🥡 Git recipes in Chinese by Zhongyi Tong. 高质量的Git中文教程.  https://geeeeeeeeek.github.io/git-recipes/  https://github.com/geeeeeeeeek/git-recipes
- 第5篇 Git 实用贴士
  * 第3章 Git log 高级用法 https://github.com/geeeeeeeeek/git-recipes/wiki/5.3-Git-log-%E9%AB%98%E7%BA%A7%E7%94%A8%E6%B3%95
  * 第4章 Git 钩子：自定义你的工作流 https://github.com/geeeeeeeeek/git-recipes/wiki/5.4-Git-%E9%92%A9%E5%AD%90%EF%BC%9A%E8%87%AA%E5%AE%9A%E4%B9%89%E4%BD%A0%E7%9A%84%E5%B7%A5%E4%BD%9C%E6%B5%81

Git 常用命令速查表(图文+表格) https://www.jb51.net/article/55442.htm --> 一堆命令我连听都没听过。。。

git checkout 命令详解 https://www.cnblogs.com/hutaoer/archive/2013/05/07/git_checkout.html
```
(四）熟悉的checkout，陌生的用法，妈妈再也不用担心我的checkout啦！
1. git branch <branch> <start point>
2. git checkout --datch <branch>
3. git checkout -B <branch>
4. git checkout --orphan <branch>
6. git checkout -p <branch>
```

git寻根——^和~的区别 https://www.cnblogs.com/hutaoer/archive/2013/05/14/3078191.html
```
这时候HEAD悄然来到了”c2”的commit 1c73，因此，HEAD~2 相当于HEAD的第一个父提交的第一个父提交。
即HEAD~2 = HEAD^^ = HEAD^1^1, 符合预期！好开心的哟

五.总结

1. “^”代表父提交,当一个提交有多个父提交时，可以通过在”^”后面跟上一个数字，表示第几个父提交，”^”相当于”^1”.
2. ~<n>相当于连续的<n>个”^”.
3. checkout只会移动HEAD指针，reset会改变HEAD的引用值。
```
>> 个人再总结下吧：其实这个文章主要就是通过实验说明了，在有多个父节点的情况下：`HEAD^n`是多个父节点之间（横着）走的；`HEAD~n`是沿着第一个分支（纵向）走的。所以感觉还是`~`是更想达到的效果（一般用git reset回退几个commit的时候肯定是想纵向回退啊）。

###  git的refs
<<Git push与pull的默认行为>>
https://segmentfault.com/a/1190000002783245

<<Git远程分支和refs文件详解>>
http://blog.csdn.net/forever_wind/article/details/37506389

<<Git HEAD detached from XXX (git HEAD 游离) 解决办法>>
http://blog.csdn.net/u011240877/article/details/76273335

### git-symbolic-ref

git-symbolic-ref https://git-scm.com/docs/git-symbolic-ref
```
$ git branch
* master
$
$ git symbolic-ref HEAD
refs/heads/master
$
$ git checkout -b dev
Switched to a new branch 'dev'
$
$ git symbolic-ref HEAD
refs/heads/dev
$
$ git symbolic-ref HEAD --short
dev
```
>> 目前只知道这个命令最大的用途是脚本里面显示git当前分支的时候用。

Git 提效篇 http://hotoo.github.io/blog/post/git-branch

### git本地分支与远程分支关联关系查询
git 如何查看当前分支的upstream? - 知乎 https://www.zhihu.com/question/27324031
```
这个帖子，包括下面的stackoverflow里的帖子基本都没有特别好的办法，回头再研究下吧。
https://stackoverflow.com/questions/171550/find-out-which-remote-branch-a-local-branch-is-tracking

目前最好的办法就是上面stackoverflow帖子里的：
git for-each-ref --format='%(upstream:short)' $(git symbolic-ref -q HEAD)
```

### git如何查询当前某个文件是否已被添加到版本控制

Git git 如何列出已经跟踪的文件？ https://ruby-china.org/topics/1519
- > `git ls-files`
- > 谢楼上各位，我把pro git翻了好几遍也没找到。。。-_-#
- > 我是在 bundle 生成 gem 模板的时候，gemspec 里面偶然发现的
- > 我是当时尝试性的敲了一个 git files 结果git 提示我是不是用ls-files,提示还是挺贴心的。

**个人补充：可以结合`grep`快速过滤，从而确定某个文件是否已被git追踪，比如（更多grep的多关键词过滤参考linux命令的grep部分吧）下面这段列出了路径或者名称里`既包含cmd也包含operator`的文件**：
```
root@myopenshift:operator-sdk$ git ls-files | grep cmd | grep operator
cmd/operator-sdk/add/api.go
cmd/operator-sdk/add/cmd.go
cmd/operator-sdk/add/controller.go
cmd/operator-sdk/add/crd.go
cmd/operator-sdk/alpha/cmd.go
cmd/operator-sdk/alpha/olm/cmd.go
...
...
...
```

## git常用命令综合类

<<Git 常用命令速查表(图文+表格)>>
http://www.jb51.net/article/55442.htm

<<Git 常用命令整理>>
http://justcoding.iteye.com/blog/1830388

今年下半年，中日合拍的《Git游记》即将正式开机，我将...（上集） https://juejin.im/post/5c22056551882518fc5fe294 [`*`][:star:]


## git书籍和系列教程(易百教程git部分就不再重复贴了)

<Pro Git>
https://www.gitbook.com/book/bingohuang/progit2/details
>远程分支 https://bingohuang.gitbooks.io/progit2/content/03-git-branching/sections/remote-branches.html

《Git权威指南》GotGit 书稿开源
https://segmentfault.com/p/1210000008626219
>http://www.worldhello.net/gotgit/

猴子都能懂的GIT入门
https://backlog.com/git-tutorial/cn/contents/


## git push -u origin master 

```
上面命令将本地的master分支推送到origin主机，同时指定origin为默认主机，后面就可以不加任何参数使用git push了。

不带任何参数的git push，默认只推送当前分支，这叫做simple方式。此外，还有一种matching方式，会推送所有有对应的远程分支的本地分支。Git 2.0版本之前，默认采用matching方法，现在改为默认采用simple方式。如果要修改这个设置，可以采用git config命令。
```
http://www.yiibai.com/git/git_push.html


**Command line instructions** (https://gitlab.com/BIAOXYZ/testproject)
- Git global setup
```
git config --global user.name "liuliang 00384038"
git config --global user.email "liuliang21@huawei.com"
```
- Create a new repository
```
git clone http://code.huawei.com/l00384038/DBATG_Work_Progress.git
cd DBATG_Work_Progress
touch README.md
git add README.md
git commit -m "add README"
git push -u origin master
```
- Existing folder
```
cd existing_folder
git init
git remote add origin http://code.huawei.com/l00384038/DBATG_Work_Progress.git
git add .
git commit
git push -u origin master
```
- Existing Git repository
```
cd existing_repo
git remote add origin http://code.huawei.com/l00384038/DBATG_Work_Progress.git
git push -u origin --all
git push -u origin --tags
```

## Github相关

<<为什么我pull request后全部放在一个未关闭的pull request里面了>>
https://segmentfault.com/q/1010000005178786

### Github Gist

如何看待 Github Gist 这个服务，怎样更好的利用？ - 知乎用户的回答 - 知乎
https://www.zhihu.com/question/21343711/answer/32023379
>GistBox http://www.gistboxapp.com/ (后改名cacher https://www.cacher.io/)

学习编程用什么做笔记比较好？ - pezy的回答 - 知乎
https://www.zhihu.com/question/21438053/answer/18790164

### https://raw.githubusercontent.com

What do raw.githubusercontent.com URLs represent? https://stackoverflow.com/questions/39065921/what-do-raw-githubusercontent-com-urls-represent
> The `raw.githubusercontent.com` domain is used to serve unprocessed versions of files stored in GitHub repositories. If you browse to a file on GitHub and then click the Raw link, that's where you'll go.

### Github相关第三方工具

#### gitbook

>http://blog.csdn.net/hk2291976/article/details/51173850
>https://www.jianshu.com/p/5d0b25cd9495

#### Travis CI

https://travis-ci.org/getting_started
>https://docs.travis-ci.com/user/language-specific/
>>https://docs.travis-ci.com/user/getting-started/
>>>https://docs.travis-ci.com/user/deployment/heroku/
>>>>https://www.heroku.com/

<持续集成服务 Travis CI 教程> http://www.ruanyifeng.com/blog/2017/12/travis_ci_tutorial.html
- https://gist.github.com/domenic/ec8b0fc8ab45f39403dd
- https://oncletom.io/2016/travis-ssh-deploy/

使用Travis进行持续集成 https://www.liaoxuefeng.com/article/1083103562955136  -->  廖雪峰这个Travis教程跟阮一峰那个还是没法比，比较基本。

如何简单入门持续集成( Travis-CI ) https://github.com/nukc/how-to-use-travis-ci

<类似Travis CI 这种持续集成「自动编译测试」的网站有哪些？>
https://www.zhihu.com/question/42991087
https://github.com/blog/2463-github-welcomes-all-ci-tools

#### Codecov

Github装逼指南——Travis CI 和 Codecov
https://segmentfault.com/a/1190000004415437

#### ZenHub

ZenHub - Agile Project Management for GitHub -- A better way to manage your GitHub Issues https://www.zenhub.com/
> https://app.zenhub.com/dashboard/o/biaoxyz/integrations

如何使用 Issue 管理软件项目？ http://www.ruanyifeng.com/blog/2017/08/issue.html
> 许多第三方工具可以增强 Github 的看板功能，最著名的是 Zenhub，这里就不详细介绍了。

#### Coveralls

如果你用Github，可以这样提高效率 https://www.jianshu.com/p/f0f65f15d295
- > 代码覆盖率 — Coveralls
  >> COVERALLS https://coveralls.io/
- > 持续集成工具再加上 flow.ci 吧 https://flow.ci :relaxed: // 进去看了下，国产的。姑且mark支持一下吧，有空可以考虑研究下。  

#### Heroku

<<国内有没有类似heroku的云服务平台？>>
https://www.zhihu.com/question/19902966

#### 

https://david-dm.org/

#### gitter (https://gitter.im/)

<GitLab收购公共聊天软件Gitter>
http://www.infoq.com/cn/news/2017/03/gitlab-gitter-acquisition

#### Gerrit

易百教程 -- Gerrit概述
https://www.yiibai.com/gerrit/gerrit_overview.html

[原创]CI持续集成系统环境---部署gerrit环境完整记录
https://www.cnblogs.com/kevingrace/p/5624122.html

Gerrit代码Review入门实战
http://geek.csdn.net/news/detail/85681

#### [GitHub开发者](https://githuber.cn/)

- https://githuber.cn/stat
- https://githuber.cn/rank
- https://githuber.cn/search
- http://blog.githuber.cn/

### GitLab相关

GitLab安装、使用教程（Docker版） - 慕课网的文章 - 知乎
https://zhuanlan.zhihu.com/p/33592623

Git使用教程,最详细，最傻瓜，最浅显，真正手把手教 - 慕课网的文章 - 知乎
https://zhuanlan.zhihu.com/p/30044692

GitLab发布Web IDE 在Web端为你提供集成开发体验 - Open Source 开源 - cnBeta.COM https://www.cnbeta.com/articles/soft/737313.htm
- https://about.gitlab.com/2018/06/15/introducing-gitlab-s-integrated-development-environment/
- https://docs.gitlab.com/ee/user/project/web_ide/
```
试了一下，可以在线同时commit多个change，并且可以先stage然后选择性commit部分change。无敌，就是这么寂寞！
这么一比的话，Github你的心不会痛嘛？！
```

https://gitlab.com/help/ci/quick_start/README

### 自建git服务相关

#### gitea

 Git with a cup of tea, painless self-hosted git service https://github.com/go-gitea/gitea
 > Gitea - Git with a cup of tea -- A painless self-hosted Git service. https://gitea.io
