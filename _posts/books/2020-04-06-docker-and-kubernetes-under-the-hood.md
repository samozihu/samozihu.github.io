---
layout:     post
title:      "Docker 容器与容器云"
subtitle:   "浙江大学SEL实验室"
date:       2020-04-06 08:46:00
author:     "aguozhang"
header-img: "img/post-bg-2015.jpg"
tags:
    - Docker 
    - Kubernetes
    - 云原生
---

## 前言
这本书买了很久，一直没有看，最近想学习一下Kubernetes，就翻了一下，发现其实写得不错。

## Docker深入解读
* Iaas层为基础设施运维人员服务，提供计算、存储、网络及其他基础资源，云平台使用者可以在上面部署和运行包括操作系统和应用程序在内的任意软件，无需再为基础设施的管理分心
* Paas层为应用开发人员服务，提供支撑应用运行所需的软件运行时环境、相关工具与服务，如数据库服务、日志服务、监控服务等，让应用开发者可以专注于核心业务的开发。
* Saas层为一般用户服务，提供了一套完整可用的软件系统，让一般用户无需关注技术细节，只需通过浏览器、应用客户端等方式就能使用部署在云上的应用服务。
* 云时代应用生命周期管理机制  十二要素应用规范
* Docker是以Docker容器为资源分割和调度的基本单位，封装整个软件运行时环境，为开发者和系统管理员设计的，用于构建、发布和运行分布式应用的平台
* GCE 
* 持续部署与测试
* 跨云平台支持
* 环境标准化和版本控制
* 高资源利用率与隔离
* 容器跨平台性与镜像
* 易于理解且易用
* 应用镜像仓库
* cgroups namespace
* Docker daemon
* Docker app stack
* Docker容器本质上是宿主机上的进程。Docker通过namespace实现资源隔离，通过cgroups实现了资源限制,通过写时复制机制(copy-on-write)实现了高效的文件操作
* libcontainer
* UTS IPC PID NETwork Mount User
* 可以通过创建veth pair(虚拟网络设备对：有两端，类似管道，如果数据从一端传入另一端也能接收到，反之亦然）在不同的network namespace间创建通道，以达到通信目的
* cgroups最初名为process container, 由google工程师Paul Menage和Rohit Seth于2006年提出，后来由于container有多重含义容易引起误解，就在2007年更名为control groups,并整合进linux内核，顾名思义就是把任务放到一个组里面统一加以控制
* cgroups四大功能: 资源限制  优先级分配 资源统计 任务控制
* cgroups术语表：task任务 cgroup控制组 subsystem子系统 hierarchy层级
* execdriver volumedriver graphdriver
* network
* client 
* daemon
* libcontainer 说到底，容器是一个与宿主机系统共享内核但与系统中的其他进程资源相隔离的执行环境。docker通过对namespace, cgroups, capabilities以及文件系统的管理和分配来隔离出一个上述执行环境，这就是docker容器
* docker镜像的主要特点：分层 写时复制 内容寻址 联合挂载
* Docker的volume的本质是容器中一个特殊的目录
* 这里使用的挂载方法是绑定挂载（bind mount), 故挂载完成后的宿主机目录和容器内的目标目录表现一致
* docker network子命令和跨主机网络支持
* CNM主要有沙盒(sandbox)、端点(endpoint)、网络(network)这3种组件
* libcontainer网络配置原理
* --net --dns
* 命令行参数阶段
* docker与容器安全
* docker daemon安全
* 镜像安全
* 内核安全
* 容器之间的网络安全
* docker容器能力限制
* Docker安全的解决方案
* SELinux
* 磁盘限制
* 宿主机内容器流量限制
* 容器化思维
* 彼此独立
* 原子化
* 组合和重构
* ip netns
* 不要在dockerfile中做端口映射
* 常用的容器监控工具
* google的cAdvisor
* Datadog
* SoundCloud的Prometheus
* etcd
* 

## Docker云平台解读
* 当第一个daemon开始工作时，终于可以当仁不让地宣布自己已经是个高级玩家
* 将军开发者
* 而容器云就是在无数这样的Docker大神的努力中产生的
* 所谓容器云，就是以容器为资源分割和调度的基本单位，封装整个软件运行时环境，为开发者和系统管理员提供用于构建、发布和运行分布式应用的平台
* Docker compose
* 编排 orchestration
* 部署 deployment
* Docker machine
* Machine处于辅助docker客户端的定位，它能提供对宿主机的管理都是轻量级操作
* Docker swarm
* 编排之秀：Fleet
* systemd
* 专注应用支撑和运行时：Flynn和Deis
* Flynn，一个小而美的两层架构
* 一切皆容器：Kubernetes
* 代表了Google过去十余年设计、构建和管理大规模容器集群的经验
* Kubernetes还是一个管理跨主机容器化应用的系统，实现了包括应用部署、高可用管理和弹性伸缩在内的一系列基础功能并封装成为一套完整、简单易用的RESTful API对外提供服务。
* Kubernetes工作的层次比Pass更低，但比Fleet要高的原因
* label
* 能够被创建、调度和管理的最小单元是pod，而非单个容器
* pod意为豆荚，里面容纳了多个豆子，很形象
* Horizontal Pod Autoscaler
* kebelet组件是Kubernetes集群工作节点上最重要的组件进程




