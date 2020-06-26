---
title: centos上命令行安装Node与pm2
date: 2020-03-15 10:24:26
tags: env
---
#### Node简介
- 是js在服务器端的运行时
- 事件驱动,易处理高并发场景
- 拥有众多开发者及模块
- ...
<!--more-->
#### 安装Node
#### 1.挑选合适版本(例如v12.16.1)并获取下载链接例如:([https://nodejs.org/dist/v12.16.1/node-v12.16.1-linux-x64.tar.gz](https://nodejs.org/dist/v12.16.1/node-v12.16.1-linux-x64.tar.gz))下载
```shell
wget https://nodejs.org/dist/v12.16.1/node-v12.16.1-linux-x64.tar.gz
```
2.解压包
```shell
tar -xvf node-v12.16.1-linux-x64.tar.gz
```
##### `node-v12.16.1-linux-x64.tar.gz` 为压缩文件位置
3.在profile(/etc/profile)中末尾加入
```
export NODE_HOME=/root/node-v12.16.1-linux-x64
export NODE_HOME
export PATH=${PATH}:${NODE_HOME}/bin
```
##### `/root/node-v12.16.1-linux-x64`为解压后文件位置
#### 刷新配置
```shell
source /etc/profile
```
4.安装pm2
```shell
npm install pm2
```
5.建立软链接
```shell
ln -s /root/node-v12.16.1-linux-x64/bin/pm2 /usr/local/bin/
```
##### `/root/node-v12.16.1-linux-x64`可以替换成你的安装路径