---
layout: post
title: "Learn mysql"
category: Code
tags:
  - Docker
  - Linux
  - SQL
last_modified_at: 2021-11-11T17:31:48-05:00
---



> Process of learning mySQL.

参考：[RUNOON](https://www.runoob.com/mysql/mysql-install.html)

#### 1. Installation

参考[MySQL 安装](https://www.runoob.com/mysql/mysql-install.html)

先尝试在`docker`的`centOS`中尝试下载，因为在`ubuntu:15.10`中下载失败，不知道是不是因为是在`docker`的原因。

`yum install wget` 遇到的问题：先后尝试使用 `centos6`和`centos7`，发现均无法安装`wget`，因为阿里云不更新了该版本的了，获取地址404，最后换成`centos8`成功安装`wget`。

>突然发现，可以直接 `docker pull mysql`，我上面的操作是在`docker`的 run 一个 centos，再在 centos 里面安装 sql。是不是有点多此一举？

额，先去学习一下 `linux` 操作吧，不然每一步都看太不懂。