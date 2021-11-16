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

#### 一、遇到的问题

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

#### 二、Shell

##### 1. 传递参数示例

```shell
#!/bin/bash
:<<!
this is note
note ending
!
echo "1st parameter is filename itself: $0"
echo "2nd parameter is what i input: $1"
echo "3rd parameter is what i input too: $2"
echo "total parameters: $#"
echo "They are: $*"
for i in "$*"; do
	echo $i
done
# 是否缩进并没有影响运行
for j in "$@"; do 
	echo $j
done
```

x it in bash：

```bash
sh-4.4# ./test.sh "Shenko.T" "Hello!"
1st parameter is filename itself: ./test.sh
2nd parameter is what i input: Shenko.T
3rd parameter is what i input too: Hello!
total parameters: 2
They are: Shenko.T Hello!
Shenko.T Hello!
Shenko.T
Hello!
```

##### 2. 运算符示例

[运算符](https://www.runoob.com/linux/linux-shell-basic-operators.html)包括：算数运算符、关系运算符、布尔运算符、逻辑运算符、字符串运算符、文件测试运算符。

```shell
#!/bin/bash
a=10
b=20
add=`expr $a + $b`
times=`expr $a \* $b`
divide=`expr $a / $b`
int_div=`expr $a % $b`
echo "a + b = $add"
echo "a * b = $times"
echo "a / n = $divide"
echo "a % b = ${int_div}"
if [ $a == $b ]
then
echo "a == b"
fi
if [ $a != $b ]
then
echo "a != b"
fi
```

x result:

```bash
sh-4.4# ./expression.sh
a + b = 30
a * b = 200
a / n = 0
a % b = 10
a != b
```

