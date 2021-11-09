---
layout: post
title: "Learn Docker"
category: Code
tags:
  - Docker
  - Linux
last_modified_at: 2021-11-09T10:47:48-05:00
---

参考：[Docker 教程](https://www.runoob.com/docker/docker-tutorial.html)，因此本文主要写一些学习过程中遇到的问题及其结局方案。

#### 1. Introduction

如果看不懂上述教程对 `docker` 的专业性介绍，以这篇[入门](https://zhuanlan.zhihu.com/p/187505981)更好——对于 `image` 和 `container` 的解释十分通俗，对初学者十分友好。

#### 2. Installation

[官网](https://docs.docker.com/desktop/mac/install/)下载速度很慢，包括 `homebrew` 下载也很慢，采用[阿里云源](https://mirrors.aliyun.com/docker-toolbox/)。注意查看所支持的系统版本，比如我就下载到 MacOS 11.0 以上的版本了。

#### 3. Example

##### 3.1 example 1: basic

```bash
localhost:~ shenkot$ docker run -d ubuntu:15.10 /bin/sh -c "while true; do echo hello world; sleep 1; done"
0d1942140b2bb671f950abcb4eef15de419ea20edd79bfb56b73e17e3dea0de1
# list all containers
localhost:~ shenkot$ docker ps
CONTAINER ID   IMAGE          COMMAND                  CREATED         STATUS         PORTS     NAMES
0d1942140b2b   ubuntu:15.10   "/bin/sh -c 'while t…"   2 seconds ago   Up 6 seconds             unruffled_ishizaka
# show the container
localhost:~ shenkot$ docker logs 0d1942140b2b
hello world
hello world
# stop the container
localhost:~ shenkot$ docker stop 0d1942140b2b
0d1942140b2b
# start the container
localhost:~ shenkot$ docker start 0d1942140b2b
0d1942140b2b
```



