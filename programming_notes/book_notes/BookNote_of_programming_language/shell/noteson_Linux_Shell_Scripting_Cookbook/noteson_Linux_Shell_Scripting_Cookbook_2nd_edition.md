
- 《Linux Shell Scripting Cookbook》 2nd edition 2013
- 《LINUX SHELL脚本攻略》2011年翻译，所以应该是第一版————确定是第一版，因为翻译版第一章开头部分只有14个任务，英文版第一章开头有16个。

# 1 Shell Something Out 小试牛刀 (即使意译，也不能这么过分。。。这是我选择用英文版记笔记的原因之一。)

```
In this chapter, we will cover:
   Printing in the terminal
   Playing with variables and environment variables
   Function to prepend to environment variables
   Math with the shell
   Playing with file descriptors and redirection
   Arrays and associative array
   Visiting aliases
   Grabbing information about the terminal
   Getting and setting dates and delays
   Debugging the script
   Functions and arguments
   Reading output of a sequence of commands in a variable
   Reading n characters without pressing the return key
   Running a command until it succeeds
   Field separators and iterators
   Comparisons and tests
```

## Introduction 简介

#### page 8

> "$ represents regular users and # represents the administrative user root."

```
A shell script is a text file that typically begins with a shebang, as follows:
    #!/bin/bash
Shebang is a line on which #! is prefixed to the interpreter path. /bin/bash is the
interpreter command path for Bash.
```

#### page 9

> "Execution of a script can be done in two ways. Either we can run the script as a command-line argument to bash or we can grant execution permission to the script so it becomes executable."

> "When a shell is started, it initially executes a set of commands to define various settings such as prompt text, colors, and much more. This set of commands are read from a shell script at ~/.bashrc (or ~/.bash_profile for login shells) located in the home directory of the user. The Bash shell also maintains a history of commands run by the user. It is available in the ~/.bash_history file."

> [Tips] "A login shell is the shell which you get just after logging in to a machine. However, if you open up a shell while logged in to a graphical environment (such as GNOME, KDE, and so on), then it is not a login shell."

## Printing in the terminal 终端打印

#### page 10-11 

总结(上)：书中原文内容主要在11页上，大致是叙述了echo命令打印时`加无引号字符串`，`加单引号字符串`，`加双引号字符串`情况下的局限性。说实话，我在两个系统里（`Windows 10 上的 WSL Ubuntu 18.04.1 LTS \n \l` 以及 `VitualBox 5.2.20 r125813 上的 CentOS 7.5.2`）实战了下之后发现不论哪个系统`echo+双引号字符串`的打印方式都和原文的叙述并不完全相符（其他两种是符合的），先列出原文然后是实战：

> 原文："Hence, if you want to print special characters such as !, either do not use them within double
quotes or escape them with a special escape character (\) prefixed with it"
>> 这段的意思是说想打印诸如叹号之类的特殊字符的话，或者别用双引号，或者在双引号里加斜杠转义该字符。

```
原文：
The side effects of each of the methods are as follows:
    ● When using echo without quotes, we cannot use a semicolon, as it acts as a
    delimiter between commands in the Bash shell
    ● `echo hello; hello` takes echo hello as one command and the second hello
    the second command
    ● Variable substitution, which is discussed in the next recipe, will not work within
    single quotes
```
>> 这段的意思是说`echo+不带引号字符串`的打印方式**无法处理中间有分号的情形**。`echo+单引号字符串`的打印方式**无法做变量替换**。


**(1)**`echo+不带引号字符串`的打印方式**无法处理中间有分号的情形**：
```shell
两个系统的实战结果均和书上的叙述是一致的。

1.WSL Ubuntu 18.04.1

wsl@DESKTOP-5LVLGG9:~$ echo hello; hello
hello

Command 'hello' not found, but can be installed with:

sudo apt install hello
sudo apt install hello-traditional

2. VitualBox CentOS 7.5.2

test2@localhost:~\> echo hello; hello
hello
-bash: hello: 未找到命令
```

**(2)**`echo+单引号字符串`的打印方式**无法做变量替换**。
```shell
两个系统的实战结果均和书上的叙述是一致的。

1.WSL Ubuntu 18.04.1

wsl@DESKTOP-5LVLGG9:~$ echo $PWD
/home/wsl
wsl@DESKTOP-5LVLGG9:~$ echo '$PWD'
$PWD
wsl@DESKTOP-5LVLGG9:~$ echo "$PWD"
/home/wsl

2. VitualBox CentOS 7.5.2

test2@localhost:~\> echo $PWD
/home/test2
test2@localhost:~\> echo '$PWD'
$PWD
test2@localhost:~\> echo "$PWD"
/home/test2
```

**(3)**`echo+双引号字符串`的打印方式**对特殊符号（如叹号）必须转义**。
```shell
全部都用书上的例子，首先实验不加转义的情况下打印叹号。书上认为最后两个例子都不可能打印成功，
但是实际上Ubuntu全部打印成功；CentOS一个成功一个失败（这点我也觉得很怪，本以为都该失败的）。。。

1.WSL Ubuntu 18.04.1

wsl@DESKTOP-5LVLGG9:~$ echo hello world!
hello world!
wsl@DESKTOP-5LVLGG9:~$ echo 'hello world!'
hello world!
wsl@DESKTOP-5LVLGG9:~$ echo "hello world!"
hello world!
wsl@DESKTOP-5LVLGG9:~$ echo "cannot include exclamation - ! within double quotes"
cannot include exclamation - ! within double quotes

2. VitualBox CentOS 7.5.2

test2@localhost:~\> echo hello world!
hello world!
test2@localhost:~\> echo 'hello world!'
hello world!
test2@localhost:~\> echo "hello world!"
-bash: !": event not found
test2@localhost:~\> echo "cannot include exclamation - ! within double quotes"
cannot include exclamation - ! within double quotes

再实验一下有转义字符的情况。结果全都和书上叙述不符：都把转义字符原封不动打印出来了。

1.WSL Ubuntu 18.04.1

wsl@DESKTOP-5LVLGG9:~$ echo "Hello world \!"
Hello world \!

2. VitualBox CentOS 7.5.2

test2@localhost:~\> echo "Hello world \!"
Hello world \!
```

总结(下)：浪费了不少时间（主要是记录，实验的时间其实用的不多），实际还有不少点没有覆盖到，比如：`其他特殊符号是什么情况？单引号双引号混合是什么情况？反引号是什么情况？`等等。网上也能查到不少，但是不在这里记了，因为一旦展开就没完没了了，所以这里只记录和书上直接相关的吧。最后的结论就是要用的时候根据系统和脚本多查查多试试吧。。。

#### page 12-13
```shell
%-5s can be described as a string substitution with left alignment (- represents left
alignment) with width equal to 5. If - was not specified, the string would have been aligned to
the right. The width specifies the number of characters reserved for that variable.
```
```shell
By default, echo has a newline appended at the end of its output text. This can be avoided
by using the -n flag. echo can also accept escape sequences in double-quoted strings as an
argument. When using escape sequences, use echo as echo -e "string containing
escape sequences".
```
```shell
Colors are represented by color codes, some examples being, reset = 0, black = 30, red = 31,
green = 32, yellow = 33, blue = 34, magenta = 35, cyan = 36, and white = 37.

For a colored background, reset = 0, black = 40, red = 41, green = 42, yellow = 43, blue = 44,
magenta = 45, cyan = 46, and white=47, are the color codes that are commonly used.
```
```shell
echo命令和其flag在 WSL Ubuntu 18.04.1 上的实战：

(1)echo -e 将 \t 转义序列转义为tab：
wsl@DESKTOP-5LVLGG9:~$ echo -e "1\t2\t3"
1       2       3
wsl@DESKTOP-5LVLGG9:~$ echo "1\t2\t3"
1\t2\t3

(2)echo打印默认带换行符，用 -n 标志忽略结尾的换行符：
wsl@DESKTOP-5LVLGG9:~$ echo 123
123
wsl@DESKTOP-5LVLGG9:~$ echo -n 123
123wsl@DESKTOP-5LVLGG9:~$

(3)echo的flag必须在字符串之前，不然会被当成字符串的一部分：
wsl@DESKTOP-5LVLGG9:~$ echo "1\t2\t3" -n
1\t2\t3 -n
wsl@DESKTOP-5LVLGG9:~$ echo "1\t2\t3" -e
1\t2\t3 -e

(4)echo打印彩色字体和彩色背景——不过这边应该显示不出来吧：
wsl@DESKTOP-5LVLGG9:~$ echo -e "\e[1;31m This is red text \e[0m"
 This is red text
wsl@DESKTOP-5LVLGG9:~$ echo -e "\e[1;42m Green Background \e[0m"
 Green Background
```

## Playing with variables and environment variables 玩转变量和环境变量

#### page 13

> "In Bash, the value for every variable is string, regardless of whether we assign variables with quotes or without quotes."

#### page 13-14

> "To view all the environment variables related to a terminal, issue the env command."
>> 命令`env`可以查看所有的环境变量。

> "For every process, environment variables in its runtime can be viewed by: cat /proc/$PID/environ"
>> 命令`cat /proc/$PID/environ`可以查看进程相关的环境变量。

```shell
然后书上用gedit做了示范：

$ pgrep gedit
12501
$ cat /proc/12501/environ
GDM_KEYBOARD_LAYOUT=usGNOME_KEYRING_PID=1560USER=slynuxHOME=/home/slynux
$ cat /proc/12501/environ | tr '\0' '\n'
...
...   //使用tr命令，把结果中的'\0'用'\n'代替，从而做到每一个var=value独占一行。


我自己实战的话用vi试了下：
test2@localhost:~\> pgrep vi
1692
test2@localhost:~\> cat /proc/1692/environ
...
...      //结果太多，不复制了。
test2@localhost:~\> cat /proc/1692/environ | tr '\0' '\n'
...
...      //结果太多，不复制了。用tr过滤后一个键值对独占一行。

notes:
1.在讲这段的时候涉及了两个新命令，pgrep和tr。
2.pgrep结合反引号有时能更省事，比如：
test2@localhost:~\> cat /proc/`pgrep vi`/environ | tr '\0' '\n'
...
...      //结果太多，不复制了。用tr过滤后一个键值对独占一行。
```

#### page 14

> "If value does not contain any space character (such as space), it need not be enclosed in quotes, Otherwise it is to be enclosed in single or double quotes."

> "Note that var = value and var=value are different. It is a usual mistake to write var = value instead of var=value. The later one is the assignment operation, whereas the earlier one is an equality operation."
>> 给shell变量赋值不能有空格，再记一次~

#### page 15

> "Environment variables are variables that are not defined in the current process, but are received from the parent processes."

> 『When given a command for execution, the shell automatically searches for the executable in the list of directories in the PATH environment variable (directory paths are delimited by the ":" character).』

#### page 16

> "Get the length of a variable value using the following command: `length=${#var}`"
```shell
wsl@DESKTOP-5LVLGG9:~$ var=12345678901234567890
wsl@DESKTOP-5LVLGG9:~$ echo ${#var}
20
```

> "To identify the shell which is currently being used, we can use the `SHELL` variable"
```shell
wsl@DESKTOP-5LVLGG9:~$ echo $SHELL
/bin/bash
wsl@DESKTOP-5LVLGG9:~$ echo $0
-bash

test2@localhost:~\> echo $SHELL
/bin/bash
test2@localhost:~\> echo $0
-bash

所以也就是说 $SHELL 等于 $0，但是我这边两个系统下echo $0显示的都和书上的不太一样啊。
```

#### page 17

> "The `UID` value for the root user is 0."
```shell
if [ $UID -ne 0 ]; then
echo Non root user. Please run as root.
else
echo Root user
fi
```

> "We can customize the prompt text using the `PS1` environment variable. The default prompt text for the shell is set using a line in the `~/.bashrc` file."
```shell
1.WSL Ubuntu 18.04.1

wsl@DESKTOP-5LVLGG9:~$ cat ~/.bashrc | grep PS1
    PS1='${debian_chroot:+($debian_chroot)}\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\$ '
    PS1='${debian_chroot:+($debian_chroot)}\u@\h:\w\$ '
    PS1="\[\e]0;${debian_chroot:+($debian_chroot)}\u@\h: \w\a\]$PS1"

2. VitualBox CentOS 7.5.2

test2@localhost:~\> cat ~/.bashrc | grep PS1
PS1="\u@\h:\033[1;33m\]\W\[\033[1;32m\]\$(parse_git_branch_and_add_brackets)\[\033[0m\]\> "
```
>> 不知道为啥 WSL Ubuntu 18.04.1 里会有三个。。。然后修改命令提示符样式回头再研究，这里就不展开了。

```
"There are also certain special characters that expand to system parameters. For example,
\u expands to username, \h expands to hostname, and \w expands to the current
working directory."
```

## Function to prepend to environment variables (中文版无该部分，应该是英文第二版新加的所以中文版第一版没有)

