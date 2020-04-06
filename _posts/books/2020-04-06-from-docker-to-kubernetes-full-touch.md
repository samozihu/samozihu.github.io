---
layout:     post
title:      "Kubernetes权威指南"
subtitle:   "从docker到Kubernetes实践全接触"
date:       2020-04-06 10:07:00
author:     "aguozhang"
header-img: "img/post-bg-2015.jpg"
tags:
    - Docker
    - Kubernetes
    - 权威指南
---

## 前言
同样是之前买的书，最近拿来翻了一下，感觉不错

## 摘录
* 太公兵法
* Kubernetes这个名字起源于古希腊，是舵手的意思
* Kubernetes是第一个将 一切以服务为中心，一切围绕服务运转 作为指导思想的创新型产品，它的功能和架构设计自始至终都遵循了这一指导思想，构建在Kubernetes上的系统不仅可以独立运行在物理机、虚拟机集群或者企业私有云上，也可以被托管在公有云中
* Kubernetes是什么？
* it从来都是一个由新技术驱动的行业
* 轻装上阵
* 全面拥抱微服务架构
* Master
* Node (Minion)
* Pod
* Label
* Label selector
* Label和Label selector共同构成了Kubernetes系统中最核心的应用模型
* Replication Controller(RC)
* Deployment
* Horizontal Pod Autoscaler (HPA)
* Service
* NodePort
* Volume(存储卷）
* Persistent Volume
* Namespace
* Annotation
* Kubernetes集群网络配置方案
* flannel
* Open vswitch
* 直接路由
* kubectl
* skydns
* 深入掌握pod
* 而一旦创建出新pod,就将在执行完启动命令后，陷入无限循环和过程中。这就是kubernetes需要我们自己创建的docker镜像以一个前台命令作为启动命令的原因
* pod生命周期和重启策略
* pod健康检查
* Rest本身只是为分布式超媒体系统设计的一种架构风格，而不是标准
* Jersey
* Fabric8
* 服务质量等级(QoS Classes)
* Guaranteed(完全可靠的）
* Best-Effort(尽力而为，不太可靠的）
* Burstable(弹性波动、较可靠的）
* etcd数据存储的高可用性
* Kubernetes Master组件的高可用性
* Heapster InfluxDB  Grafana
* Kubelet的垃圾回收(GC)机制


