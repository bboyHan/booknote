## 文章目录（Table of Contents）

- [二、Linux环境安装Mysql](#二Linux环境安装Mysql)
  - [1、下载解压](#1下载解压)
  - [2、安装](#2安装)
  - [3、使用](#3使用)
  
# 二、Linux环境安装Mysql

## 1、下载解压

官方下载链接：[https://dev.mysql.com/downloads/mysql/5.7.html#downloads](https://dev.mysql.com/downloads/mysql/5.7.html#downloads)

将下载的文件上传至服务器上某一路径下(/usr/src/software/)，进行解压。

```shell
tar -zxvf mysql-5.6.44-linux-glibc2.12-i686.tar.gz

# 重命名
mv mysql-5.6.44-linux-glibc2.12-i686 mysql
```

## 2、安装

### 2.1 添加用户和用户组mysql

```shell
# 添加用户组 mysql
groupadd mysql

# 添加用户 mysql
useradd -g mysql mysql
```

### 2.2 创建data文件夹，并赋予mysql用户权限

```shell
# 路径自己定义(/usr/src/data)
mkdir data

# 赋权限
chown -R mysql:mysql data
```

### 2.3 初始化

```shell
# 去往路径，你的mysql路径(/usr/src/mysql)
./scripts/mysql_install_db --user=mysql \ 
--datadir=/usr/src/data \
--basedir=/usr/src/mysql

# 复制脚本(/usr/src/mysql)
cp support-files/mysql.server /etc/init.d/mysqld

# 权限设置
chmod 755 /etc/init.d/mysqld
# 复制my.cnf
cp support-files/my-default.cnf /etc/my.cnf
```

### 2.4 修改配置

```shell
# 将之前设置的datadir、basedir路径写入

# my.cnf
vim /etc/my.cnf

[mysqld]

# Remove leading # and set to the amount of RAM for the most important data
# cache in MySQL. Start at 70% of total RAM for dedicated server, else 10%.
# innodb_buffer_pool_size = 128M

# Remove leading # to turn on a very important data integrity option: logging
# changes to the binary log between backups.
# log_bin

# These are commonly set, remove the # and set as required.
# basedir = .....
basedir = /usr/src/mysql
# datadir = .....
datadir = /usr/src/data
# port = .....
# server_id = .....
# socket = .....

:wq
```

```shell
vim /etc/init.d/mysqld

# If you install MySQL on some other places than /usr/local/mysql, then you
# have to do one of the following things for this script to work:
#
# - Run this script from within the MySQL installation directory
# - Create a /etc/my.cnf file with the following information:
#   [mysqld]
#   basedir=<path-to-mysql-installation-directory>
# - Add the above to any other configuration file (for example ~/.my.ini)
#   and copy my_print_defaults to /usr/bin
# - Add the path to the mysql-installation-directory to the basedir variable
#   below.
#
# If you want to affect other MySQL variables, you should make your changes
# in the /etc/my.cnf, ~/.my.cnf or other MySQL configuration files.

# If you change base dir, you must also change datadir. These may get
# overwritten by settings in the MySQL configuration files.

basedir=/usr/src/mysql
datadir=/home/mysql/data

# Default value, in seconds, afterwhich the script should timeout waiting
# for server start. 
# Value here is overriden by value in my.cnf. 
# 0 means don't wait at all
# Negative numbers mean to wait indefinitely

:wq
```

### 2.5 启动服务

```shell
# 启动
service mysqld start

# 查看状态
service mysqld status

# 停止
service mysqld stop
```

### 2.6 配置全局使用

```shell
# 添加
export PATH=$PATH:/usr/src/mysql/bin

# 编译
souce /etc/profile
```

## 3、使用

## 3.1 进入数据库

```shell
# mysql/bin
mysql

# 查看数据库
show databases;

# 选择mysql
use mysql
```

## 3.2 创建用户，设置密码

```shell
# CREATE USER 'username'@'host' IDENTIFIED BY 'password';

CREATE USER 'bboyhan'@'localhost' IDENTIFIED BY '123456';
```

## 3.3 授权

```shell
# 授权查询、新增权限
GRANT SELECT, INSERT ON test.user TO 'bboyhan'@'%';

# 授权所有权限
GRANT ALL ON *.* TO 'pig'@'%';

# 使授权的用户能给其它用户授权:
GRANT ALL ON test.tablename TO \
'bboyhan'@'host' WITH GRANT OPTION;

# 更新上述设置
flush privileges;
```

**注：**
%表示允许外网访问。可能有些朋友设置了%之后，发现外网或者第三方工具在连接时被拒绝访问，可能出现的问题是防火墙未开放。

```shell
# 开放防火墙端口
vim /etc/sysconfig/iptables

# 授权开放端口(3306)
-A INPUT -m state --state NEW -m \ 
tcp -p tcp –dport 3306 -j ACCEPT

# 重启防火墙
service iptables restart
```