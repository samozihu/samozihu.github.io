---
layout:     post
title:      "laravel 总体架构与设计思想"
subtitle:   ""
date:       2020-02-25 11:21:00
author:     "aguozhang"
header-img: "img/post-bg-2015.jpg"
tags:
    - code
    - php
    - laravel
    - arch
    - design 
---
结构、风格、可读性
为什么写、写什么、为谁写

## 1. laravel概述
laravel是一个php语言的web框架，但除了支持web请求，也支持命令行的运行。

最近几年很火，用的人很多，许多公司选其作为主开发框架。网上的评论有好有坏，且分化很严重。以知乎为例，说好的人极端维护，觉得设计优雅，使用简单，开
发效率高。批判的人则说的一无是处，觉得炒冷饭，设计的太复杂让人无法理解。

我现公司也选其为主开发框架，为了更好的进行开发，也为了学习一下php和框架思想，最近一段时间研究了一下laravel的源码，个人收获还是不少的。

##  2. 设计思想

web框架，简单理解，就是负责 获取请求 => 路由请求 => 处理请求 => 返回结果。在这个基础上进行一些封装和约束，就可以称为一个web框架了。其余
功能如model, controller, cache等都是可选的，或者说是提供的额外福利。

在框架的基本功能都提供的情况下，剩下的东西是决定一个框架是否取胜的关键：
* 附加功能。非必要，但提供了能大大加速rd的开发速度，如cache, model, queue等
* 可扩展性。好的框架必须容易扩展，可以基于实际业务进行定制开发和替换等
* 代码封装的艺术性。框架除了服务于开发之外，还必须要易于人阅读的，没有可阅读性的代码是没有人敢用的，不然出了问题没法debug
* 文档。 好的文档能让人迅速了解框架的设计思想和基本用法，降低学习曲线。
* 社区。 好的社区是框架能持续改进的基础。

### 2.1 附加功能
laravel作为一个框架，提供的功能很多，包括以下：
 * Auth。 包含认证和授权
 * Broadcasting。 广播功能
 * Bus。 command的队列化运行与调度
 * Cache。 缓存
 * Config。 配置
 * Console。 命令行命令的封装
 * Container。 容器
 * Contracts。 接口集合，为了`带着镣铐跳舞`。也为了方便Container绑定与注入
 * Cookie。 cookie
 * Database。数据库
 * Encryption。 加密 与 hash
 * Events。 事件，为了更好的代码解耦
 * Filesystem。文件系统
 * Foudation。 框架的核心代码实现
 * Hashing。哈希
 * Http。 request请求处理
 * Log。 log实现
 * Mail. 发送邮件功能
 * Notification。通知功能
 * Pagination。 分页功能
 * Pipeline。 pipeline模式实现，request请求处理标准化
 * Queue。 队列功能
 * Redis。 Redis功能
 * Routing。 路由功能，相当强大
 * Session。 session
 * Support。 utils的代码
 * Translation。 国际化支持
 * Validation。 表单验证
 * View。 view
 
 以上所有功能都提供了开箱即用的实现，且都有默认配置。所以从开发角度，laravel对程序员很友好，不用去关心各种细节配置。
 
 ### 2.2 可扩展性
 laravel是面向接口编程的典范，框架提供的所有功能都是基于接口的，接口对应的真正实现，是在运行启动的过程中通过配置动态决定。这也是说对于一套接口可以
 有多个实现，真正使用的实现是依赖于配置，想要换个实现，更改一下配置就可。 因为有了接口的约束，开发者也可有自己的实现，这也是可扩展性的精髓所在。
 
 



## 总体架构图


## 优美之处


## 不足之处


## 总体感受
总体来说，laravel是一个很重的框架，提供的功能很丰富，有点像python的django框架。
