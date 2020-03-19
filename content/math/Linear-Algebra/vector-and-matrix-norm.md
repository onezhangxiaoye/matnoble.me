+++
title = "向量范数与矩阵范数"
description = "Vector Norm and Matrix Norm"
date = "2020-03-19T00:13:23+00:00"
categories = ["MATH","线代拾遗"]
tags = [""]
keywords = ["向量范数","矩阵范数","线性代数","matrix","linear algebra","vector norm","matrix norm","MatNoble"]
toc = true
mathjax = true
series = ["mla"]
+++

## 向量范数

{{< blockquote link="https://zh.wikipedia.org/wiki/%E8%8C%83%E6%95%B0" >}}
**范数(模)**(英语：norm), 是具有「长度」概念的函数. 在线性代数、泛函分析及相关的数学领域, 是一个函数, 其为..向量空间..内的所有向量赋予非零的正长度或大小. 
{{< /blockquote >}}

假设 $V$ 是数域 $F$ 上的向量空间, $V$ 的范数是一个函数 $p:V \to \mathbb{R}$, 对于 $\forall a \in F, \forall \\, \mathrm{u}, \mathrm{v} \in V$, 满足
> 1. **正定性**: $p(\mathrm{v}) \geq 0$, 当且仅当 $\mathrm{v}=0$ 时, $p(\mathrm{v})=0$ 
> 2. **齐次性**: $p(a\mathrm{v}) = |a|p(\mathrm{v})$
> 3. **三角不等式**: $p(\mathrm{u}+\mathrm{v}) \leq p(\mathrm{u}) + p(\mathrm{v})$

### $p-$范数

对于向量 <span>$\mathrm{x} = [x_1, x_2, \ldots, x_n]$</span>, 定义 <span>$p-$</span> 范数为

<div>
\begin{equation}
\lVert \mathrm{x} \rVert_p := \biggl( \sum_{i=1}^n |x_i|^p \biggr)^{1/p}
\label{eq:eqp}
\end{equation}
</div>

其中 $p \in [1, +\infty)$. 

范数在几何意义下, 可以看作是「距离」. 以 $2$ 维平面为例, 在式 (\ref{eq:eqp}) 定义的距离下, 分别取 $p = 0.25, 0.5, 1, 2, 4$, 画以原点为圆心的“单位圆” 

```python
# python3
import numpy as np
import matplotlib.pyplot as plt

fig = plt.figure(num=1, dpi=150)
r = 1
linestyle = ['b-','k-','m-','r-','y-']
p_values = (0.25, 0.5, 1, 2, 4)
for i,p in enumerate(p_values):
    x = np.arange(-r,r+1e-5,1/360.0)
    y = (r**p - (abs(x)**p))**(1.0/p)
    y = list(zip(y, -y))
    plt.plot(x, y, linestyle[i])
axs = plt.gca()
axs.set_aspect('equal', 'box')
plt.savefig('images/norm.svg', bbox_inches='tight')
plt.show()
```

{{< imgcap src="https://imgkr.cn-bj.ufileos.com/40ec9695-7444-48e1-b616-2b49771c4642.svg" title="p = 0.25, 0.5, 1, 2, 4" width="60%">}}


可见当 $p\geq 1$ 时, 图形都是凸集. 以式 (\ref{eq:eqp}) 为基础, 最常用的范数有三个

### 常用向量范数

{{< imgcap src="/images/norm.svg" title="Vector Norm" >}}

- $1-$范数<br>
取 $p = 1$
\begin{equation}
\lVert \mathrm{x} \rVert_1 = \sum_{i=1}^n |x_i|
\end{equation}
也叫绝对值范数.
- $2-$范数<br>
取 $p = 2$
\begin{equation}
\lVert \mathrm{x} \rVert_2 = \sqrt{\sum_{i=1}^n |x_i|^2}
\end{equation}
这是最常见的欧几里德范数, 也可以写成: $\lVert \mathrm{x} \rVert_2 = \sqrt{\mathrm{x}^{\mathsf T}\mathrm{x}}$
- $\infty-$范数<br>
令 $p = 2$ 并取极限
\begin{equation}
\lVert \mathrm{x} \rVert_{\infty} = \max |x_i|
\end{equation}

## 矩阵范数

那么矩阵 $\boldsymbol{A}$ 的大小应如何来度量呢?

### F 范数

因为矩阵是由列(行)向量组成, 所以仿照向量范数, 首先可以定义度量「矩阵长度」的 Frobenius 范数, 简称 F 范数, 记为 $\lVert \boldsymbol{A} \rVert_F$. 假设 $\boldsymbol{A}$ 是 $m\times n$ 阶矩阵, 则 Frobenius 范数定义为:

<div>
$$
\begin{aligned}
\lVert \boldsymbol{A} \rVert_F &= \sqrt{\lVert \mathrm{\alpha_1} \rVert^2 + \cdots + \lVert \mathrm{\alpha_n} \rVert^2} \\[3pt]
& = \sqrt{\sum_{i=1}^m |a_{i1}|^2 + \cdots + \sum_{i=1}^m |a_{in}|^2} \\[3pt]
& = \sqrt{\sum_{j=1}^n\sum_{i=1}^m |a_{ij}|^2} = \sqrt{\mathrm{trace}(\boldsymbol{A}^{\mathsf T}\boldsymbol{A})}
\end{aligned}
$$
<div>

另外, F 范数还和奇异值有关系. 如果已知秩为 $r$ 的矩阵 $\boldsymbol{A}$ 及其奇异值, <span>$\sigma_1 \geq \cdots \geq \sigma_r > 0$, $\sigma_{r+1} = \cdots = \sigma_p = 0, p = \min\\{m, n\\}$</span>, 那么

\begin{equation}
\lVert \boldsymbol{A} \rVert_F = \sqrt{\sum_{i=1}^r \sigma_i^2}
\end{equation}

**证明:**

首先假设 $\boldsymbol{Q}$ 是正交矩阵, 那么成立

<div>
$$
\begin{cases}
\lVert \boldsymbol{Q} \boldsymbol{A} \rVert_F^2 = \mathrm{trace}\bigl((\boldsymbol{Q} \boldsymbol{A})^\mathsf{T}\boldsymbol{Q} \boldsymbol{A}\bigr) = \mathrm{trace}\bigl(\boldsymbol{A}^\mathsf{T} \boldsymbol{Q}^\mathsf{T} \boldsymbol{Q} \boldsymbol{A}\bigr) = \mathrm{trace}(\boldsymbol{A}^{\mathsf T}\boldsymbol{A}) = \lVert \boldsymbol{A} \rVert_F^2
\\[3pt]
\lVert \boldsymbol{A} \boldsymbol{Q} \rVert_F^2 = \mathrm{trace}\bigl(\boldsymbol{A} \boldsymbol{Q} (\boldsymbol{A} \boldsymbol{Q})^\mathsf{T}\bigr) = \mathrm{trace}\bigl(\boldsymbol{A} \boldsymbol{Q} \boldsymbol{Q}^\mathsf{T}\boldsymbol{A}^\mathsf{T} \bigr) = \mathrm{trace}(\boldsymbol{A}\boldsymbol{A}^\mathsf{T}) = \lVert \boldsymbol{A} \rVert_F^2
\end{cases}
$$
<div>

即矩阵范数有「正交不变性」

所以针对矩阵的奇异值分解 $\boldsymbol{A} = \boldsymbol{U}\boldsymbol{\Sigma}\boldsymbol{V}^{\mathsf T}$, 成立

$$
\lVert \boldsymbol{A} \rVert_F = \lVert \boldsymbol{\Sigma} \rVert_F = \sqrt{\sum_{i=1}^r \sigma_i^2}
$$

<p style="text-align: right">
$\blacksquare$
</p>

### 矩阵范数性质

首先, 矩阵是多维向量, 所以容易验证, 矩阵范数同样满足: **正定性, 齐次性, 三角不等式**; 

正因为矩阵是增加了维度的向量, 所以还有向量所没有的性质 --- 矩阵可以表示「线性变换」在维度适合时(可乘), 矩阵可以乘向量 $\boldsymbol{A}\mathrm{x}$, 得到的..像.. $\boldsymbol{A}\mathrm{x}$ 与..原像.. $\mathrm{x}$ 有如下关系

<div>
$$
\begin{aligned}
\lVert \boldsymbol{A}\mathrm{x} \rVert^2 & = \lVert x_1 \alpha_1 + \cdots + x_n \alpha_n \rVert^2
\\[3pt]
& \leq \bigl( \lVert x_1 \alpha_1 \rVert + \cdots + \lVert x_n \alpha_n \bigr)^2
\\[3pt]
& = \bigl(|x_1| \cdot \lVert \alpha_1 \rVert + \cdots + |x_n| \cdot \lVert \alpha_n\bigr)^2
\end{aligned}
$$
</div>

利用 [Cauchy 不等式](https://matnoble.me/math/fem/inequality/#cauchy-inequality-for-scalar-product), 可得

<div>
$$
\begin{aligned}
\bigl(|x_1| \cdot \lVert \alpha_1 \rVert + \cdots + |x_n| \cdot \lVert \alpha_n\bigr)^2 & \leq (\lVert \alpha_1 \rVert^2 + \cdots +  \lVert \alpha_n \rVert^2)(|x_1|^2 + \cdots + |x_n|^2)
\\[3pt]
& = \lVert \boldsymbol{A} \rVert_F^2 \lVert \mathrm{x} \rVert^2
\end{aligned}
$$
</div>

即 $\lVert \boldsymbol{A}\mathrm{x} \rVert\leq \lVert \boldsymbol{A} \rVert_F \lVert \mathrm{x} \rVert$. 若将向量 $\mathrm{x}$ 换作 $n\times p$ 阶矩阵 $\boldsymbol{B}$，情况又如何呢? 

<div>
$$
\begin{aligned}
\lVert \boldsymbol{A}\boldsymbol{B} \rVert_F^2 & = \bigl\lVert \bigl[ \boldsymbol{A} \beta_1  \cdots  \boldsymbol{A} \beta_p \bigr] \bigr\rVert_F^2
\\[3pt]
& = \lVert \boldsymbol{A} \beta_1 \rVert_F^2 + \cdots + \lVert \boldsymbol{A} \beta_p \rVert_F^2
\\[3pt]
& \leq \lVert \boldsymbol{A} \rVert_F^2 \lVert \beta_1 \rVert^2 + \cdots + \lVert \boldsymbol{A} \rVert_F^2 \lVert \beta_p \rVert^2
\\[3pt]
& = \lVert \boldsymbol{A} \rVert_F^2 ( \lVert \beta_1 \rVert^2 + \cdots + \lVert \beta_p \rVert^2)
\\[3pt]
& = \lVert \boldsymbol{A} \rVert_F^2\lVert \boldsymbol{B} \rVert_F^2
\end{aligned}
$$
</div>

即 $\lVert \boldsymbol{A}\boldsymbol{B} \rVert_F \leq  \lVert \boldsymbol{A} \rVert_F \lVert \boldsymbol{B} \rVert_F$. 综合之前的 3 条性质, 可总结为

> **矩阵范数的性质**<br>
> - $\lVert \boldsymbol{A} \rVert \geq 0$, 当且仅当 $A=0$ 等号成立.<br>
> - $\lVert c\boldsymbol{A} \rVert = |c|\lVert \boldsymbol{A} \rVert $
> - $\lVert \boldsymbol{A} + \boldsymbol{B} \rVert \leq \lVert \boldsymbol{A} \rVert + \lVert \boldsymbol{B} \rVert $
> - $\lVert \boldsymbol{A}\boldsymbol{B} \rVert \leq  \lVert \boldsymbol{A} \rVert \lVert \boldsymbol{B} \rVert$

与向量范数相同, 矩阵范数也不唯一. 甚至利用性质 4, 可以导出更重要的范数.

### 矩阵 $2-$范数

当矩阵 $\boldsymbol{B}$ 退化为向量 $\mathrm{x}$ 时, $\lVert \boldsymbol{A}\mathrm{x} \rVert\leq \lVert \boldsymbol{A} \rVert \lVert \mathrm{x} \rVert$
, 如果 $\mathrm{x} \neq 0$, 就有

\begin{equation}
 \lVert \boldsymbol{A} \rVert \geq \frac{\lVert \boldsymbol{A}\mathrm{x} \rVert}{\lVert \mathrm{x} \rVert}
\label{eq:eq20} 
\end{equation}

当向量右端取向量 $2-$范数时, 可以定义矩阵 $2-$范数

\begin{equation}
 \lVert \boldsymbol{A} \rVert_2 = \max_{x\neq 0} \frac{\lVert \boldsymbol{A}\mathrm{x} \rVert_2}{\lVert \mathrm{x} \rVert_2}
\label{eq:eqm2} 
\end{equation}

因为是由向量的欧氏距离所决定, 所以对应地称为矩阵的 $2-$范数. 其几何意义就是: 限制了原像的「伸缩」

### 其他矩阵范数
