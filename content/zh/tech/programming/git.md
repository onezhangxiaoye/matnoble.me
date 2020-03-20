+++
title = "Git 实用命令汇总(长期更新)"
categories = ["TECH","好工具高效率"]
tags = ["Git"]
keywords = ["Git 基础教程","Git 实用命令","单个文件的“增删改查”","多设备间管理代码库","在 Github 上删除已提交的文件夹"]
date = "2019-03-14T00:00:00+00:00"
toc = true
+++

<img src="https://imgkr.cn-bj.ufileos.com/e13f1349-c714-4eee-ba1d-a0f12bce7661.png" title="Git && GitHub" alt="Git 实用命令汇总" />

<!--more-->

## 1 安装及配置

安装:

```shell
sudo apt-get install git
```

配置:

```shell
git config --global user.name "Your Name"
git config --global user.email "email@example.com"
```

------------

## 2 单个文件的“增删改查”

### 2.1 创建版本库

```shell
git init
```

### 2.2 提交

```shell
git add filename
git commit -m "description"
```

### 2.3 显示工作树状态

```shell
git -status	
```

### 2.4 显示版本库和工作树之间的不同

```shell
git diff
```

------------

## 3 多设备间管理代码库 🖖

> 我有两台笔记本: 
- Lenovo Y430p 作为主力机, 性能还不错, 装有 Win10 和 Ubuntu 18.04 双系统, 缺点就是太重了. 
- Surface Go 作为二奶机, 性能不及主力机, 但携带方便.  

> 因此, 两个设备三个系统间协作编程, Github 私有仓库(现已免费) :fa-github: 再适合不过了 

### 3.1 电脑 1 初始化仓库, 初始提交
在 GitHub 中创立私有库`Share_Code`, 在本地

```shell
% 初始化仓库
git init
% 提交到本地仓库
git add filename
git commit -m "description1"
% 初始提交到远程仓库
git remote add origin git@github.com:MatNoble/Share_Code.git
git push -u origin master
```
### 3.2 电脑 2 克隆, 修改, 提交

```shell
% 克隆
git clone git@github.com:MatNoble/Share_Code.git
% 修改本地代码后, 修改本地仓库
git add filename
git commit -m "description2"
% 提交到远程仓库
git push
```

### 3.3 电脑 1 远程同步

```shell
% 将远程仓库同步到本地仓库
git fetch origin master
% 合并本地代码
git merge origin/master
```

<hr />

## 4 在 Github 上删除已提交的文件夹

之前在一次项目的Github提交中不小心把一个不需要的文件夹提交了上去,而此时在写.gitignored已经为时已晚,为了解决这一问题,经查阅多方资料后得出以下解决办法:

Github在提交了之后无法在线删除文件夹,但是在本地Git库中却可以,只要在Git库中删除了仓库对应缓存,再push到Github服务器,文件夹的删除目的就达成了,

以下是具体操作:

```shell
git rm -r --cached 目录名
git commit -m '描述'
git push -u origin master
```
