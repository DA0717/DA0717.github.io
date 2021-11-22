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



> Process of learning mysql.

参考：[RUNOON](https://www.runoob.com/mysql/mysql-install.html)

## 0. Preparation

### 0.1 Installation in linux.

参考[MySQL 安装](https://www.runoob.com/mysql/mysql-install.html)

先尝试在`docker`的`centOS`中尝试下载，因为在`ubuntu:15.10`中下载失败，不知道是不是因为是在`docker`的原因。

`yum install wget` 遇到的问题：先后尝试使用 `centos6`和`centos7`，发现均无法安装`wget`，因为阿里云不更新了该版本的了，获取地址404，最后换成`centos8`成功安装`wget`。

>突然发现，可以直接 `docker pull mysql`，我上面的操作是在`docker`的 run 一个 centos，再在 centos 里面安装 sql。是不是有点多此一举？

学习完`linux`后点错了链接，进入了这个[教程](https://www.runoob.com/linux/mysql-install-setup.html)，出现了如下错误：

```bash
No match for argument: libmcrypt-devel2
No match for argument: libmhash-devel
```

先没解决这两个问题，虽然找到了疑似解决方案。

因此安装了其他编译工具后，返回了最初的教程，续。

```bash
sh-4.4$ mysqld --initialize
sh: /usr/sbin/mysqld: Operation not permitted
```

没有找到解决方案。

### 2. Installation in docker.

运用docker运行mysql虽然是套了一层docker位于os与mysql之间，但是还是运行在os之上。比如我应该在电脑的目录下运行查看mysql是否运行。

```bash
localhost:~ shenkot$ ps -ef | grep mysqld
  501 91601 76362   0  6:07下午 ttys001    0:00.01 grep mysqld
```

新建的container，mysql_test 其实是运行了一个 debian OS:

```bash
# cat /etc/issue 
Debian GNU/Linux 10 \n \l
```

所以实际上是image:mysql只是一个安装了mysql的debian OS而已，难怪pull的image大小:mysql>centos

## 1. Notes

### 1.1 Basic management

在docker激活container:mysql后，有两个shell，其中一个是macOS的terminal，另外一个是操作mysql的shell，在第一个shell里面查看mysql是否运行；第二个shell可以看做mysql的操作界面，可以关闭mysql:

```bash
$ ./mysqladmin -u root -p shutdown
Enter password: 
shenkotdeMacBook-Air:~ shenkot$ 
```

此时就会关闭container:mysql，退出到macOS terminal.

在第二个shell里面输入`mysql -u root -p`进入`mysql`操作界面。

```sh
$ mysql -u root -p
Enter password: 123456
Welcome to the MySQL monitor.
mysql>
```

进入后的界面：

```sql
#因为可能包含多个数据库，这一步是为了指定要操作的数据库
mysql> use mysql 
Database changed

#查看一共有哪些数据库
mysql> SHOW DATABASES;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
4 rows in set (0.01 sec)

#查看当前数据库的所有表
mysql> SHOW TABLES;
+------------------------------------------------------+
| Tables_in_mysql                                      |
+------------------------------------------------------+
| columns_priv                                         |
|...                                                   |
| user                                                 |
+------------------------------------------------------+
37 rows in set (0.00 sec)

#查看数据表属性（即表头）、属性类型、主键信息、是否为 NULL，默认值等其他信息。
mysql> SHOW COLUMNS FROM user
    -> ;
+--------------------------+-----------------------------------+------+-----+-----------------------+-------+
| Field                    | Type                              | Null | Key | Default               | Extra |
+--------------------------+-----------------------------------+------+-----+-----------------------+-------+
| Host                     | char(255)                         | NO   | PRI |                       |       |
| User                     | char(32)                          | NO   | PRI |                       |       |
| Select_priv              | enum('N','Y')                     | NO   |     | N                     |       |
| Insert_priv              | enum('N','Y')                     | NO   |     | N                     |       |
...
| User_attributes          | json                              | YES  |     | NULL                  |       |
+--------------------------+-----------------------------------+------+-----+-----------------------+-------+
51 rows in set (0.01 sec)

#显示数据表的详细索引信息，包括PRIMARY KEY（主键）。
mysql> SHOW INDEX FROM user;

#显示数据表状态，从数据库database中
mysql> show table status from mysql;
```

试了一下，SQL命令小写也是可以的。

由于mysql更新，用户设置已经不能用菜鸟教程的[在user表中添加一行](https://www.runoob.com/mysql/mysql-administration.html)来实现了，改为如下实现。

```sql
#创建新用户，用户名@访问IP indentified by 密码
mysql> create user 'guest'@'%' identified by 'guest123';

#赋予新用户所有数据库中所有表的增删查改和建表删表的权限
mysql> grant usage on *.* to 'guest'@'%' with grant option;
mysql> grant select,insert,update,delete,create,drop on *.* to 'guest'@'%' with grant option;

#释放内存
mysql> flush privileges;
```

### 1.2 SQL语法

基础语法没啥好讲的，直接看菜鸟的[SQL教程](https://www.runoob.com/sql/sql-tutorial.html)，怎么会有这样口语化的语法，哈哈。

大概记住，SQL无非就是对表进行操作的语言而已，只是不能可视化操作而已。

以及mysql就是一个软件而已，一些基本的操作语句也一看就懂，不会现查即可。

> 完结撒花！



