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

## 1. laravel概述

laravel是一个php语言的web框架，除了支持web请求，也支持命令行的运行。

应该是当前最火的php框架，用的人很多，许多公司选其作为主开发框架。网上对其的评价参差不一且分化严重。以知乎为例，说好的人极端维护，觉得设计优雅，使用简单，开
发效率高。批判的人则说的一无是处，觉得炒冷饭，设计复杂让人无法理解。

laravel是我现公司的主开发框架，为了更好的进行开发，也为了学习一下php和框架思想，最近研究了laravel的源码，我收获还是不少的。

##  2. 什么是web框架

什么是web框架？简单理解，就是负责 获取请求 => 路由请求 => 处理请求 => 返回结果。在此基础上进行一些封装和并加入约束，就可以称为一个web框架了。其余
功能如model, controller, cache等都不是必需的，或者说是额外福利。

决定一个框架是否受欢迎，除了基本的功能，我觉得还有以下：
* 附加功能。非必要，但提供了能大大加速开发，如cache, model, queue等
* 可扩展性。好的框架必须容易扩展，可以基于实际业务进行定制开发和替换等
* 代码封装的艺术性。框架除了服务于开发之外，还必须要易于阅读的，没有可阅读性的代码是没有人敢用的，尤其是遇到bug的时候。
* 文档。 好的文档能让人迅速了解其设计思想和基本用法，降低学习曲线。
* 社区。 社区是持续改进的基础。


## 3. laravel特色

### 3.1 附加功能
laravel提供了如下功能：
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
 
以上所有都能开箱即用，且都有默认配置。所以从开发角度，laravel对程序员很友好。

### 3.2 可扩展性
 
 laravel是面向接口编程的典范，框架提供的所有功能都是基于接口的，不和具体实现耦合。
 接口对应的真正实现，是通过配置实现的。一个接口可以有多套实现，换一个实现，改一下配置就行。
 因为有了接口的约束，开发者可以有自己的实现，这也是可扩展性的精髓所在。
 
### 3.3 代码实现
 * 代码拆分：laravel按照功能切分代码，不同功能放入不同的文件夹。不同文件夹实现解耦，同一个文件夹实现内聚。如有关cache的功能都放在Cache文件夹中。有关文件的都放在Filesystem中。各个功能基本相互独立，各个文件夹
 也是一个单独的lib库，可以在非laravel框架项目中安装使用。
 * 代码引用：功能代码之间不跨文件夹直接引用，引用只依赖接口。例如Cache文件夹中的代码不会直接引用Redis文件夹中的代码。如果有依赖，依赖的是接口。接口的生成实例由框架
 负责注入。所有功能对外提供的接口都定义在Contracts。例如Cache的redis实现中要用到redis实例，这个redis实例不会直接引用Redis中的代码。而且引用
 Contracts/Redis中的接口。
 * 功能注入： laravel提供了一个标准流程。多个底层功能实现 ==> 对外提供功能的Repository ==> 生成repository对象的Factory|Manager
 ==> ServiceProvider将其注入到app容器中 ==> 通过app按需取用
 
### 3.4 文档
 官方文档写得很好，从浅到深，浅显易懂。
 
### 3.5 社区
 现在社区很庞大也很活跃，遇到的问题网上基本都能搜到解决方案。
 

## 4. 总体架构图
![总体架构图](/img/laravel/total_arch.jpg)

从图中可以看出，container容器居于核心地位，框架把所有附加功能都注入到容器中

## 5. 优美之处
个人最喜欢laravel有以下几处：
1. 接口。 基于所有功能都是先定义接口再开发。
2. 易用性。如Facade, app()等都是为了提高开发者效率的。
3. 绑定注入及别名。 容器中提供了大量的将实现注入到容器中的方法，如bind, singleton, instance等。
4. type hint自动注入。Controller, Job等构造函数或方法的参数只要加上类型声明，laravel会自动为其生成对应的实例。
5. artisan提供了make功能，可以帮助开发者生成代码模板，提高效率且减少bug.


## 6. 不足之处
1. 从底层实现到最终注入到容器中的链路过长，容易把开发者绕晕。
2. 命名不一致。同样差不多的功能，有时叫Manager,有时叫Factory。接口名称和实现名称经常一致，只能从文件夹路径来区分。


## 7. 总体感受
总体来说，laravel是一个很重的框架，提供的功能很丰富，有点像python的django框架。 
提供的功能开箱即用，对于要求不高的开发者完全够用。
