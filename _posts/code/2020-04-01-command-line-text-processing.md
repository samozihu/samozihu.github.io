---
layout:     post
title:      "Command line text processing"
subtitle:   "命令行文本处理"
date:       2020-04-01 11:42:00
author:     "aguozhang"
header-img: "img/post-bg-2015.jpg"
tags:
    - Command line
    - text
    - sed 
    - awk

    - 
---


## 前言
作为一个程序开发人员，熟悉使用命令行，尤其中文本处理方面的，是一个基本的要求, 它可以帮助你大大提高效率。

就像你有一个工具箱，里面有各种各样的工具了，遇到问题使用合适的工具。

没有这个工具箱，就会出现，你只有一把锤子, 就不可避免的出现把所有问题都看成钉子。

github有一个库，把文本命令行的方面讲得很详细，[链接](https://github.com/learnbyexample/Command-line-text-processing)


## 摘录

### cat
* cat marks_201*
* cat - marks_2015.txt
* printf 'hello\n\nworld\n\nhave a nice day\n'
* cat -n marks_201* 
* cat -sb mark_201*
* nl
* cat -E marks_2015.txt
* cat -T marks_2015.txt
* printf 'foo\0bar\0baz\n' | cat -v
* -A is equivalent to -vET
* -e is equivalent to -vE
* cat > abc.txt

### tac
* tac report.log | sed -n '/Error:/,/Warning:/p' | tac
* line reverse use rev
* grep -E 'Warning|Error' report.log
* tr 'A-Z' 'a-z' < marks_2015.txt
* grep -c 'foo' marks_201*
* cat marks_201* | grep -c 'foo'
* Use input redirection if a command doesn't accept file input

### less
* g go to start of file
* G go to end of file
* q quit
* /pattern search for the given pattern in forward direction
* ?pattern search for the given pattern in backword direction
* n go to next pattern
* N go to previous pattern

### tail
* Use -n option to control number of lines to filter
* when number is prefixed with + sign, all lines are fetched from that particular line number to end of file
* tail -c3
* tail -c +2
* tail -n2 report.log sample.txt
* tail -q -n2 report.log sample.txt
* tail -f

### head
* head sample.txt
* head -n3 sample.txt
* when number is prefixed with - sign, all lines are fetched except those many lines to end of file
* head -c2
* head -c -4

### grep
* echo 





