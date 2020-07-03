---
title: centos7.4上mysql服务端安装与使用
date: 2020-07-04 00:43:51
tags: env
---
#### MySQL简介
- 性能高、成本低、可靠性好
- 较为流行
- 适合中小型网站
- ...
<!--more-->
### 安装
##### 目前MySQL 8已为稳定版，推荐安装，当然你也可以安装其他版本，[下载链接](https://dev.mysql.com/downloads/mysql/)
##### 在弹出页面中选择`Linux - Generic`如图所示
![选择操作系统](/blog/env/imgs/select.png)
##### 然后在页面下方选择适合的版本例如[https://dev.mysql.com/get/Downloads/MySQL-8.0/mysql-8.0.20-linux-glibc2.12-x86_64.tar.xz](https://dev.mysql.com/get/Downloads/MySQL-8.0/mysql-8.0.20-linux-glibc2.12-x86_64.tar.xz)如图所示
![选择版本](/blog/env/imgs/version.png)
##### 然后下载所选版本 wget -O `URL`
##### 然后根据官方的描述，下载所需依赖
``` shell
yum install numactl
yum install libaio-dev
yum install openssl
```
##### 解压安装包
``` shell
tar -xvf PATH
```
##### _`PATH`为下载的文件夹的路径_
##### 移动解压后的文件夹到/usr/local/mysql或其他位置
``` shell
mv mysql-8.0.20-linux-glibc2.12-x86_64 /usr/local/mysql
```
##### 添加用户，赋予权限
``` shell
groupadd mysql
useradd -r -g mysql -s /bin/false mysql
cd /usr/local
cd mysql
mkdir mysql-files
chown mysql:mysql mysql-files
chmod 750 mysql-files
```
##### 创建MySQL数据存储目录例如`/usr/local/mysql/data/`
```shell
mkdir /usr/local/mysql/data
```
##### MySQL配置，创建`/etc/my.conf`输入，详细内容可以百度
```
[mysql]

# 设置mysql客户端默认字符集

default-character-set=utf8


[mysqld]

#设置3306端口

port = 3306

# 设置mysql的安装目录

basedir=/usr/local/mysql

# 设置mysql数据库的数据的存放目录

datadir=/usr/local/mysql/data

# 允许最大连接数

max_connections=200

# 服务端使用的字符集默认为8比特编码的latin1字符集

character-set-server=utf8
# 创建新表时将使用的默认存储引擎

default-storage-engine=INNODB
```
##### 初始化数据库，切勿不可重复初始化
```shell
cd /usr/local/mysql/bin
mysqld --initialize --user=mysql
```
##### 此步会生成一个随机的密码，请先复制到本地
![初始化生成密码](/blog/env/imgs/init.webp)

##### 复制服务文件
```shell
cp /usr/local/mysql/support-files/mysql.server /etc/init.d/mysql.server
```
##### 开启MySQL服务
```shell
/usr/local/bin/mysqld_safe --user=mysql &
```
##### 连接MySQL数据库
```shell
mysql -u root -p
```
###### 接着输入之前复制的密码并回车
#### 更改密码及允许远程访问，在mysql客户端中输入:
```sql
ALTER USER 'root'@'localhost' IDENTIFIED BY `PASSWORD` PASSWORD EXPIRE NEVER;
use mysql;
update user set host='%' where user = 'root';
flush privileges;
ALTER USER 'root'@'%' IDENTIFIED WITH mysql_native_password BY `PASSWORD`;
flush privileges;
```
###### _`PASSWORD`_为新的密码
#### now you can enjoy it!
##### MySQL`启停
```shell
/etc/init.d/mysql.server start #启动
/etc/init.d/mysql.server stop #停止
