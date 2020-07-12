---
title: centos7.4-ssh配置与使用
date: 2020-07-12 19:25:23
tags: env
---
#### ssh简介
- Secure Shell（安全外壳协议，简称SSH）是一种加密的网络传输协议
- 可在不安全的网络中为网络服务提供安全的传输环境
- SSH最常见的用途是远程登录系统，人们通常利用SSH来传输命令行界面和远程执行命令。
- ...
<!--more-->
### 使用
#### 安装
```shell
yum install ssh
```
#### 启停
```shell
service sshd start | stop | restart
```
### 配置密钥对方式登录
1. ##### 生成密钥
```shell
ssh-keygen
```
###### 执行此命令会默认生成两个文件: id_rsa(私钥),id_rsa.pub(公钥),你可以选择使用命令参数改变
```shell
ssh-keygen -f [文件名]
```
###### 若没有指定会询问位置
```shell
[root@desktop ~]# ssh-keygen
Generating public/private rsa key pair.
Enter file in which to save the key (/root/.ssh/id_rsa):输入文件保存位置/名称
```
2. ##### 将公钥添加到~/.ssh/authorized_keys
```shell
cat [公钥位置] > ~/.ssh/anthorized_keys
```
3. ##### 修改权限
```shell
[root@desktop ~]# chmod 700 ~
[root@desktop ~]# chmod 700 ~/.ssh
[root@desktop ~]# chmod 400 ~/.ssh/authorized_keys
```
4. ##### 更改sshd配置
```shell
vim /etc/ssh/sshd_config
```
##### 修改或添加以下部分
```
PubkeyAuthentication yes  # 启用基于密匙的安全验证
PasswordAuthentication no  # 关闭基于口令的安全验证
```
##### 重启sshd
```shell
service sshd restart
```
###### 若是新手或者不确定，请不要立刻关闭会话，再打开一个会话进行测试，防止连不上服务器
#### 连接服务器(先将之前的id_rsa（私钥内容）复制到本地的.ssh/id_rsa)
```shell
ssh [用户名]@[ip/域名]
```
###### enjoy it!