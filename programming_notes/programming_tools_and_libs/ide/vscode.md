
# vscode官方

Visual Studio Code https://github.com/Microsoft/vscode || https://code.visualstudio.com/

# vscode较系统攻略

中文版 Awesome VS Code https://github.com/formulahendry/awesome-vscode-cn

Collection of helpful tips and tricks for VS Code. https://github.com/Microsoft/vscode-tips-and-tricks

# vscode新闻

Visual Studio Code 1.26 发布，大量新特性来袭 - Microsoft Visual Studio - cnBeta.COM https://www.cnbeta.com/articles/soft/756969.htm

# vscode快捷键

# vscode已验证技巧

## 预览markdown

VS Code 使用小技巧 - 赵吉彤的文章 - 知乎 http://zhuanlan.zhihu.com/p/22880087
```
- 预览markdown Ctrl+Shift+V  //所以Typora彻底没用了
- 自动保存：File -> AutoSave ，或者Ctrl+Shift+P，输入 auto
```

## 注释/取消注释

vs code 的常用快捷键 https://segmentfault.com/a/1190000012047237
```
1、注释：
　　a) 单行注释：[ctrl+k,ctrl+c] 或 ctrl+/
　　b) 取消单行注释：[ctrl+k,ctrl+u] (按下ctrl不放，再按k + u)
　　c) 多行注释：[alt+shift+A]
```

## 关闭已开启的文件夹（其实可以通过新开另一个文件夹来达到关闭的效果）

How to close an opened folder in Visual Studio Code https://stackoverflow.com/questions/30028469/how-to-close-an-opened-folder-in-visual-studio-code/37549173
> The command to close the currently opened folder can be found from `File` -> `Close Folder`. You can also use the shortcut: Ctrl+K F

## 自动换行

如何让 Visual Studio Code 自动换行？ - wansho的回答 - 知乎 https://www.zhihu.com/question/35042902/answer/400070742
```
English环境下
点击菜单栏 View--> Toggle Word Wrap 选项.
或者直接 快捷键 : alt + Z
```

## 代码块整体左移右移

```
多行代码同时左移一个tab键（等于 shift + tab）
ctrl+[

多行代码同时右移一个tab键（等于 tab）
ctrl+]
```

## vscode护眼色修改

- VSCode修改编辑器(代码窗口)背景色 https://blog.csdn.net/u013506207/article/details/80529858   【1】
  > "如果你的VSCode使用的是自带的主题，可以直接到VSCode的安装目录下找到：\resources\app\extensions这个目录，该目录下以theme-开头的文件夹表示其是主题文件夹，按照自己当前使用的主题名称去找到对应的文件夹进去修改即可，在上面给出的参考链接中已有比较详细的说明。本文主要针对在这个目录下找不到的当前所使用主题的文件夹如何修改背景色。"
  >
  > "在你的用户目录下：通常是C:\Users[你的用户名].vscode\extensions存放你从vscode的插件库中下载的第三方插件，当然，主题也会在这里啦，所以找到你这个目录下包含有你当前主题名称的文件夹就是等下要修改的主题文件夹了。"
- Visual Studio Code护眼绿豆沙主题修改 https://blog.csdn.net/Lean_on_Me/article/details/84552487   【2】
  ```
  这款主题是在亮色Atom One Light 的基础上修改的，首先下载并设置Atom One Light
  
  "workbench.colorCustomizations": {
        "[Atom One Light]": {
          "editor.background": "#C7EDCC",   
	      "sideBar.background": "#C7EDCC",
          "activityBar.background": "#C7EDCC",       
        },
    },
  ```
```
总结一下：现在vscode改个背景色比过去麻烦多了。。。

目前粗看是不能直接改vscode的背景色，只能是vscode当前在用某个主题（theme），然后改这个主题的背景色。于是【1】的主要目的
是找到对应主题的json配置文件所在的目录；【2】的主要目的是把两个需要的选项替换成相应的护眼色。

我最终的文件目录是：C:\Users\LiangLiu\.vscode\extensions\akamud.vscode-theme-onelight-2.1.0\themes\OneLight.json
然后里面其实只改了两项"editor.background"和"sideBar.background"似乎就够了。
```

## vscode连接远程服务器开发

VS Code Remote Development https://code.visualstudio.com/docs/remote/remote-overview
- Remote Development using SSH https://code.visualstudio.com/docs/remote/ssh

VSCode使用Remote插件编辑远程服务器文件 https://www.bilibili.com/video/av52490747/
```
一些个人补充：
1.已经是正式版的功能，不需要insider版本。
2.插件一装好，在vscode的最左下角（Mac上是这个位置）就有个很明显的标记去连接。
3.实际上那个记录远程主机和用户列表的config文件不是必需的，只是为了方便。我认为是没必要记，手输一下就完了。会提示：
> Select configured SSH host or enter user@host
>> 所以接着输入一下 user@host（比如我是：root@myopenshift，注意本机hosts要能识别myopenshift噢，不然就用ip）就可以了。

总结一下过程：
1.配好本地主机（window，mac之类的）和远程主机的单向互信，保证在本地主机执行：ssh user@remotehost 时没问题。
2.下载好对应的vscode插件。
3.连接。
```

9102 年的 Windows + Linux 混合开发环境方案 - 王磊的文章 - 知乎 https://zhuanlan.zhihu.com/p/68309055
> 这个里面给了一些可能的问题的解决方案，不过我目前还没有碰到。

***--------------------------------------------------分割线--------------------------------------------------***

# vscode for C/C++

Visual Studio Code 如何编写运行 C、C++ 程序？ - 知乎 https://www.zhihu.com/question/30315894

万字长文把 VSCode 打造成 C++ 开发利器 - 腾讯技术工程的文章 - 知乎 https://zhuanlan.zhihu.com/p/96819625

# vscode for go

vscode golang配置说明 https://www.cnblogs.com/nickchou/p/9038114.html
```
vscode也可以通过ctrl+shift+p运行命令一次性安装所有这些工具
Go: Install/Update Tools
```

VS code golang 开发环境搭建 - CSDN博客 https://blog.csdn.net/hil2000/article/details/51714607
> https://github.com/golang/tools

在Visual Studio Code配置GoLang开发环境 - CSDN博客 https://blog.csdn.net/chszs/article/details/50076641
> "要注意，GoLang的安装要确保两个环境变量，一个是GOROOT环境变量；二是PATH环境变量要包含$GOROOT\bin值。"

使用Visual Studio Code调试Golang工程 - 徐波的文章 - 知乎 https://zhuanlan.zhihu.com/p/26473355
>> notes：感觉主要就是调试配置那里模式改成————`"mode": "debug"`（有的时候值是`"auto"`）就差不多了。不过我是因为机器之前已经下过delve了。

vscode 的 go 插件怎么正确安装？ https://www.v2ex.com/t/615962
- > export GOPROXY=https://goproxy.cn
- > idea 社区版 可以装 go 的插件，使用体验和 goland 是一样的

***--------------------------------------------------分割线--------------------------------------------------***

# vscode for python

VSCode基础使用+VSCode调试python程序入门 https://blog.csdn.net/u013600225/article/details/52971528

***--------------------------------------------------分割线--------------------------------------------------***

# vscode for latex

VS Code 与 LaTeX 真乃天作之合 https://www.jianshu.com/p/57f8d1e026f5