---
layout:     post
title:      "laravel request 和 command 处理流程"
subtitle:   "laravel源码入口"
date:       2020-02-24 17:45:00
author:     "aguozhang"
header-img: "img/post-bg-2015.jpg"
tags:
    - code
    - php
    - laravel
    - source code
---



## Http requests处理流程

入口是 `public\index.php` ， 执行步骤如下：

1. 载入`bootstrap\autoload.php`， 这个文件只负责载入`vendor\autload.php`，后一个`autoload.php`是composer在安装完composer.json后自动生成的。laravel framework是项目的依赖，载入后laravel framework的所有功能准备就绪了。
2. 生成一个容器实例`app` 并返回。执行代码在`bootstrap\app.php` 中。这个app实例是整个框架的核心，框架的所有功能都通过依赖注入到这个app中，之后在使用中可随时按需获取。在返回app之前，还完成了以下功能：
   * 注入一个`App\Http\Kernel`单例
   * 注入一个`App\Console\Kernel` 单例
   * 注入一个`App\Exceptions\Handler`单例
3. 通过`app` 获取上一步生成的`App\Http\Kernel`单例。
4. 捕获请求并生成一个request实例，kernel处理请求并返回response，处理流程如下：
   * 把request绑定到app中
   * 启动基本设施：环境变量， 配置，注册异常处理， Facades, 注册Providers， 启动Proivders
   * pipeline->send->through->then, 生成一个pipeline, 把request send给pipeline, 通过pipeline把request给每个middleware处理，处理完后then给Router处理
   * Router接收到请求后dispatch给相应的route处理
   * 在route中，也有一个 pipeline->send->through->then, 生成一个pipeline, 把request send给pipeline, 在pipeline中把request给每一个middleware处理(注：这里的middleware跟上上一步的middleware是不一样的），middleware都处理完后，then给到具体的controller action处理或者closure进行处理。
5. 发送response给client
6. kernel通用terminate函数。通常response发送完后，可能会些一些后续的处理，如session保存，销毁连接等。



## command处理流程

laravel中command的运行都是通过artisan来运行的，如 `php artisan list` 就是列出所有可以运行的command。 `artisan`是一个php的可执行文件，位于项目根目录下。命令行的处理流程基本与request一致，上步骤如下：

1. 载入 `bootstrap/autload.php`文件

2. 载入`bootstrap/app.php`文件并返回一个app实例

3. 通过app获取一个 `Illuminate\Contracts\Console\Kernel`class实例，这个Kernel实例其实是上一步返回app之前注入的

4. kernel实例的handle函数运行真正的命令行功能

5. kernel调用terminate函数进行后处理

   

## 总结

从之上的处理流程看出，request和command的处理流程基本一致，差别只是调用不用的kernel进行处理。而kernel处理各自的功能逻辑，这样就是把变和不变分开了，kernel是变的地方，而总的处理流程步骤是不变的地方。