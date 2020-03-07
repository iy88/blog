---
title: hexo的基本使用方法
date: 2020-03-05 20:06:19
tags: hexo
---
## 简介

- hexo是一个高效的基于nodejs的博客框架
- 拥有众多主题和插件
- 支持markdown语法,不懂的自觉[`baidu`](https://www.baidu.com)|[`google`](https://www.google.com)|[`bing`](https://cn.bing.com)
- 易上手
<!--more-->
## 快速上手
###### _本教程适用于windows系统用户,使用前请确保你有以下的环境_

- [git](https://git-scm.com/)
- [Node](https://nodejs.org): ^8.10

### 1.按win+R在文本框中输入cmd,然后点击确认
>![](/blog/hexo/imgs/run.png)
### 2.cmd下输入以下内容,并回车
```shell
    npm install -g hexo-cli
```
#### 等待安装hexo完成
>![](/blog/hexo/imgs/cmd.png)
### 3.cd进入桌面
```shell
    cd desktop
```
### 4.创建博客
```shell
    hexo init name
```
#### `name`指你博客(注意:此处博客指博客系统的根目录,包括博客静态文件以及配置文件、主题等)存放的文件夹名称(如果不存在，则会自动创建)。创建完成后,打开这个文件夹你看到的会和下图中类似
>![](/blog/hexo/imgs/dir.png)
#### 文件说明
- node_modules:
##### 存放node的模块(依赖)
- scaffolds:
##### 模板
- source:
##### 存放文章的文件夹(注意,此处是md文件,要在网上访问需要生成html文件,后面会说)
- themes:
##### 存放博客主题的文件夹
- _config.yml:
##### 博客配置文件,添加插件、更换主题，需要更改此文件
- .gitignore:
##### 不上传git的文件说明,不懂自觉[`baidu`](https://www.baidu.com)|[`google`](https://www.google.com)|[`bing`](https://cn.bing.com)
- package.json
##### npm包说明(依赖说明,用于快速安装模块),不懂自觉[`baidu`](https://www.baidu.com)|[`google`](https://www.google.com)|[`bing`](https://cn.bing.com)
- package-lock.json:
##### npm依赖详细说明(npm install后自动生成),不懂自觉[`baidu`](https://www.baidu.com)|[`google`](https://www.google.com)|[`bing`](https://cn.bing.com)
### 5.初次体验
#### cmd中进入之前生成的文件夹
```shell
    cd name
```
##### 此处`name`同上
#### 运行hexo内置服务器(开启预览,会根据文章的变动,自动更新内容,不创键html文件,生成一个临时文件)
```shell
    hexo s
```
#### 执行上述命令后,cmd会出现如下图类似的内容
>![](/blog/hexo/imgs/hexo-s.png)
#### 这时，不要关cmd!在浏览器中访问[`http://localhost:4000/`](http://localhost:4000/)会出现如下内容
>![](/blog/hexo/imgs/webpage.png)
### 5.生成静态文件
```shell
    hexo g
```
#### 进入cmd,进入上面生成的文件夹,输入上述命令,会在文件夹中生成public文件夹,此文件夹便是静态页面,(注意:由于使用路径的缘故，无法通过本地打开html的方式预览,需要放进静态服务器,才可查看)
### 6.如何使用
1. #### 用下方的命令，可以快速创建一篇博客(仅仅是创建这个文件,如果你喜欢,手动创建也可以,文件位置后面会说)
```shell
    hexo new title
```
##### `title`指文章标题,执行此命令后,会在source/_posts文件夹中创建一个title.md(title中如有空格,需用""将title包起来,创建的文件名会是你输入的标题将空格替换成'-',类如输入"hello world",则创建hello-world.md)
2. #### 用下方的命令可以快速创建一个标签(文章种类)
```shell
    hexo new page "name"
```
##### `name`指标签名称，执行此命令会在source文件夹下创建一个叫上述名称的文件夹,其中包含index.md默认配置