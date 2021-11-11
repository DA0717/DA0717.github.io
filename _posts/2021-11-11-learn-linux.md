---
layout: post
title: "Learn Linux"
category: Code
tags:
  - CentOS
  - Linux
  - SQL
last_modified_at: 2021-11-11T21:37:48-05:00
---



> First step into Linux. Device: docker run centos.

reference: [Linux 教程](https://www.runoob.com/linux/linux-system-contents.html)

#### 遇到的问题

##### 1. cannot find the `/boot`

根目录里面并没有 `/boot` ，猜测原因是 `docker`?

##### 2. ` man: command not found`

```shell
sh-4.4# man cp
sh: man: command not found
```

先尝试安装 `yum install man`

```bash
sh-4.4# man cp
No manual entry for cp
```

再尝试 `yum install -y man-pages` DONE!

##### 3. What is shell

`shell` includes: `sh`, `bash`, `zsh`, `csh`, `tcsh`

虽然是 `sh`，但是可以按到是指向 `bash`的。

```bash
sh-4.4# ls -l /bin/sh 
lrwxrwxrwx 1 root root 4 May 27 15:11 /bin/sh -> bash
sh-4.4# echo $SHELL
/bin/bash
# look up shells installed
sh-4.4# cat /etc/shells
/bin/sh
/bin/bash
/usr/bin/sh
/usr/bin/bash
```





