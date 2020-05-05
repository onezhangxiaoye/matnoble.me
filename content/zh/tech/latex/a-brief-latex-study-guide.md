+++
title = "一份不太简短的 LaTeX 写作指北"
categories = ["TECH","LaTeX 科技排版"]
date = "2020-03-26T00:08:00+00:00"
keywords = ["在 LaTeX 里更改字体大小","Changing the font size in LaTeX","font size","经验分享","技术总结","LaTeX","matnoble","数系家园","数学小兵儿"]
tags = [""]
katex = true
series = ["latex"]
toc = true
+++


## 前言

### 软科普 

本小节主要介绍 $\TeX$、$\LaTeX$ 以及 TeX Live 分别是什么？以及他们的区别是什么？不读也不影响使用，不敢兴趣者可以直接跳到[下一小节]()。

$\TeX$ 是 Donald Knuth 在 1978 年首先发布的，用于排版出高质量书籍的开源软件系统。

{{< blockquote link="https://en.wikipedia.org/wiki/TeX" >}}
$\TeX$ is a *typesetting system* which was designed and mostly written by *Donald Knuth* and released in 1978.<br>
$\TeX$ was designed with two main goals in mind: 
  - To allow anybody to produce high-quality books with minimal effort
  - To provide a system that would give exactly the same results on all computers, at any point in time.<br>
  
$\TeX$ is *free software*, which made it accessible to a wide range of users.
{{< /blockquote >}}

$\LaTeX$ 是带有宏(macros) 的 $\TeX$

"What You See Is What You Get" 

TeX Live is a cross-platform, free software distribution for the TeX typesetting system

### 本文写什么

### 写作目的

纯文本

严格来说，$\TeX$ 是一套「编码式的排版系统」。只要有文档模板，然后以「$\TeX$ 语法」填入文档内容，通过编译，就可以精准地按照模板定义的格式呈现一篇 PDF 文档了。

对于文档模板，初学者或者对自定义格式无感者，「拿来主义」就好。GitHub，[LaTeX Templates](http://www.latextemplates.com/)，[Overleaf](https://www.overleaf.com/latex/templates)等网站都提供了大量的开源模板。

所谓「$\TeX$ 语法」就是能让 $\TeX$ 能读懂的语言。

## 文档结构

类似 C 语言的头文件，每一个 .tex 文件都有一个最基本的框架

```tex
\documentclass{article}
% 导言区 
\begin{document}
% 正文部分
Hello world
\end{document}
```

第一行 `\documentclass{article}` 中的 `article` 可以被替换为 `book` `letter` 或者 `beamer` 等文件类名。

### 摘要

### 章节

## 环境

### 图片



### 表格

### 浮动体

## 数学公式

## 参考文献
