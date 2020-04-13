---
title: Mac 终端命令学习
date: 2017-02-10 20:42:51
categories: 学习总结
tags: Mac
---

大学C语言第一堂上机课，老师说：上世纪计算机大牛都不用鼠标的，Windows下可以Dos命令控制电脑上的一切，瞬间觉得逼格不是一般的高。所以刚开始自学iOS的时候，我就最先学习macOS(原来叫OSX)环境的终端命令。

虽然现在也一直在用，但是很多不经常用的命令就忘记了，忽然再用的时候就比较费劲，这就再复习总结一下。

如果有意愿，可以在终端下使用下面的命令进行学习：

``` terminal
man 命令名称 
man cd
```
使用后会显示当前命令的释义、用法以及参数等，可以自己学习。

<!-- more -->
# 文件操作

对于文件的操作是最经常用的操作。

## 目录操作

| 命令名 | 功能描述 | 例子 |
| :------: | :------ | :------ |
| mkdir | 创建一个目录 | mkdir dirname |
| rmdir | 删除一个目录 | rmdir dirname |
| mv | 修改或移动目录或文件 | mv dirname1 dirname2 |
| rm | 删除目录或文件 | rm (-rf 慎用) dirname filename |
| cd | 跳转当前目录路径 | cd path |
| pwd | 显示当前路径 | pwd |
| ls | 显示当前目录内容 | ls |

## 文件操作

| 命令名 | 功能描述 | 例子 |
| :------: | :------ | :------ |
| cat | 连接和输入文件 | cat filename1 filename2 .. |
| cp | 拷贝文件(并可以修改文件名称) | cp file1 path/file2 |
| file | 查找文件的类型 | file file1 |
| open | 默认程序打开文件 | open file1 |
| head | 显示文件头几行 | head -number file1 |
| tail | 显示文件头后行 | tail -number file1 |
| diff | 比较两个文件| diff file1 file2 | 
| wc | 查找文件的字、行、字符、比特数 | wc [-w、-l、-m、-c] file1|


## cd path 拼接符号
cd 搭配以下符号跳转目录路径

| 符号 | 功能描述 | 例子 |
| :------: | :------ | :------ |
| / | 连接路径 搭配 '.'或dirname 使用 | cd ./test/ |
| . | 当前目录 | cd ./ 还是当前目录|
| .. | 上级目录 | cd ../.. 上上级目录 |
| / | 根目录 | cd /User/username/Desktop |
| ~ | 用户目录  等于/User/username | cd ~/Desktop |

# 安全操作

| 命令名 | 功能描述 | 例子 |
| :------ | :------ | :------ |
| passwd | 修改用户密码 | |
| chmod | 修改目录或文件权限| chmod ug+x filename |
| umask | 定义创建文件的权限掩码 | umask 027 （027要转换2进制）|
| chown | 改变文件或目录的属主和组 | chown newowner file |
| chgrp | 改变文件或目录的属组 | chown newowner file |

# 时间操作

| 命令名 | 功能描述 | 例子 |
| :------ | :------ | :------ |
| date | 显示或者设置日期和时间| date |
| cal | 显示当前日历 | cal |
| time | 命令执行时间 | time |

# 其他操作
一些可能会用的操作

| 命令名 | 功能描述 | 例子 |
| :------ | :------ | :------ |
| history | 最近执行的命令历史及其编号 | history |
| clear | 清除屏幕或窗口内容 | (command+L也能实现) |
| env | 显示当前所有设置过的环境变量 | env |
| who | 列出当前登录的所有用户 | who |
| whoami | 显示当前正进行操作的用户名 | whoami |



