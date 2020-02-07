+++
title = "Matlab 实用总结"
categories = ["编程"]
tags = ["Matlab"]
keywords = ["Matlab","经验分享"]
date = "2019-10-16T00:00:00+00:00"
toc = true
katex = true
+++

<img src="https://imgkr.cn-bj.ufileos.com/8c6ec84a-6d25-4c12-85a8-91647c9bb6e1.jpeg" title="Matlab 绘图" alt="Matlab 绘图" width="600" />

<center> 好记忆不如烂笔头 </center>

<!--more-->

## 基础
### 向量
1. 生成等间距的向量
> y = linspace(a,b,n) 
*(之前, 我总是写成`linespace`)*

``` matlab
x = linspace(1,5,5)
输出:
x = [1, 2, 3, 4, 5]
```
2. 网格坐标
> [X, Y] = meshgrid(x, y)

``` matlab
x = [0, 1, 2]
y = [3, 4, 5]
[X, Y] = meshgrid(x, y)
输出:
X = 
     0     1     2
     0     1     2
     0     1     2
Y = 
     3     3     3
     4     4     4
     5     5     5
```

## 绘图

```matlab
axis square tight 
set(gca,'looseInset',[0 0.01 0 0.01])
```
