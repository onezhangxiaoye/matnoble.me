+++
title = "在 LaTeX 添加图片"
categories = ["TECH","LaTeX 科技排版"]
date = "2020-04-07T00:18:32+00:00"
keywords = ["在 LaTeX 里更改字体大小","Changing the font size in LaTeX","font size","经验分享","技术总结","LaTeX","matnoble","数系家园","数学小兵儿"]
tags = [""]
katex = true
series = ["latex"]
toc = true
+++

<img src="https://imgkr.cn-bj.ufileos.com/4e7ca500-bdca-42dc-9444-bffa8af84fc5.png" width="95%" />
<div align="center"><a href="/series/latex">◎ 你过来啊 🤞</a></div>

## 最基础

在 $\LaTeX$ 里添加图片使用 `graphicx` 宏包，在导言区导入

```tex
\usepackage{graphicx}
```

然后，在需要插入图片的地方，使用如下命令

```tex
\includegraphics[选项]{图形文件名}
```

其中，图形文件名支持包含路径，常用的选项包括:

- width, height $\to$ 指定图形的宽度和高度[^2]
- scale $\to$ 缩放因子，如 scale = 0.6
- angle $\to$ 制定旋转角度，逆时针，以`度`为单位

```tex
% 插入 MatNoble logo
\includegraphics[width = .3\textwidth]{images/logo.pdf}

% 居中 logo
{ \centering \includegraphics[width = .3\textwidth]{images/logo.pdf}
  % 下方必须有一行空格才能居中
  
}

% 居中 logo 并逆时针旋转 37 度
{ \centering \includegraphics[width = .3\textwidth,angle=37]{images/logo.pdf}
  % 下方必须有一行空格才能居中
  
}
```

<img src="https://imgkr.cn-bj.ufileos.com/0e40f4dd-e865-4017-958c-e4404f50214c.png" width="85%" />

{{< notice tip >}}
`graphicx` 宏包支持多种常见的图片格式，但推荐使用 `.eps` 和 `.pdf` 格式，以得到更清晰的显示效果。
{{< /notice >}}

## 自动搜寻路径

以上 `图形文件名` 处，加上了 `.tex` 文件目录下的用来存储图片文件夹的目录 `images`，为了更方便使用，我们可以不加目录，甚至是图片后缀名。只需在导言区加入以下代码

```tex
 % 如果图片没有指定后缀, 依次按下列顺序搜索
\DeclareGraphicsExtensions{.eps,.pdf,.jpg,.png}

 % 设置图表搜索路径, 可以给图表文件夹取如下名字
\graphicspath{{figures/}{figure/}{pictures/}
  {picture/}{pic/}{pics/}{image/}{images/}}
```

之后，就可以省去目录和后缀名[^1]

```tex
\includegraphics[width = .3\textwidth]{logo}
```

## 浮动图环境

如果想为图片自动添加编号，则需要使用..浮动图环境..[^3]。**浮动**的意义在于：自动调整图表位置, 避免出现大片的空白

```tex
\begin{figure}[位置]
    ··· ···
\end{figure}
```

**位置** 选项的取值: h $\to$ here, t $\to$ top, b $\to$ bottom, p $\to$ page

推荐顺序：h $\to$ t $\to$ b $\to$ p

一般情况，还要求图片居中，则可以在环境中首先加上 `\centering`

```te
\begin{figure}[htbp]
    \centering
    ··· ···
\end{figure}
```

接着填入开始说的 `\includegraphics[选项]{图形文件名}` 命令。添加图片名称使用 `\caption` 命令。最后，使用 `\label` 标签及 `\ref` 命令实现..交叉引用..

```tex
\begin{figure}[htbp]
    \centering
    \includegraphics[width = .3\textwidth]{logo}
    \caption{\em logo}
    \label{fig:logo}
\end{figure}

figure \ref{fig:logo} is my logo
```

<img src="https://imgkr.cn-bj.ufileos.com/9255d2bb-ca05-4726-a390-77a107dc3e94.png" width="85%" />

## 图片并排

**TO DO**

[^1]: 仔细观察下代码就可以发现，诸如`{figures/}{figure/}{pictures/}{picture/}{pic/}{pics/}{image/}{images/}` 这些目录都会被支持
[^2]: 只保留其中一个参数，另一个则会等比例放大或缩小
[^3]: 对应的还有浮动..表..环境
