+++
title = "逼近函数 IV"
mathjax = true
categories = ["简述有限元"]
tags = ["有限元"]
keywords = ["有限元","FEM"]
date = "2019-12-30T00:00:00+00:00"
toc = true
katex = true
+++

<img src="https://imgkr.cn-bj.ufileos.com/64498351-25f9-435e-8951-704f5883d9e0.png" title="简述有限元: 逼近函数 IV"  alt="简述有限元逼近函数" />

<!--more-->

# 有限元基函数 IV

## 上期回顾

### 程序

> 例题 1  
> 利用拉格朗日多项式做基函数编程实现: 设函数 $f(x)=10(x-1)^2-1$, 在线性函数空间中找到最佳逼近函数 $u(x)$, 求解域 $\Omega = [1, 2]$, 两个真解点为: $x\_0 = 1+1/3, x\_1 = 1+2/3$.

<img src="https://imgkr.cn-bj.ufileos.com/08a52fa9-b8f3-46c5-b6ff-1d7a9703bbfc.png" title="简述有限元: 例题 1"  alt="简述有限元逼近函数" width="500"/>

<img src="https://imgkr.cn-bj.ufileos.com/c8dfa667-6a58-48d2-9ec7-7123dae6c7bc.png" title="简述有限元: 例题 1 结果展示"  alt="简述有限元逼近函数" width="300"/>

> 主程序

```matlab
f = @(x)(10*(x-1).^2 - 1);
syms x
psi = [1, x];
points = [1+1/3, 2-1/3];

[ A, b ] = interpolation( f, psi, points );
c = A\b;
u = psi*c;

% 可视化
omega = [1, 2];
X = omega(1) : 0.01 : omega(2);
U = inline(vectorize(u), 'x');
Plot(X, f, U)

% 结果展示
result(A, b, c, u)
```

> 例题 2  
> 假设 $f(x)=\sin(2\pi x), \Omega=[0, 1]$, 利用拉格朗日多项式做基函数, 分别用`最小二乘法`和`插值法`寻找最佳逼近函数 $u(x)$.  
>  _注: 可假设基函数个数为 4 个, 拉格朗日点为等距节点_

- 最小二乘法

![](https://imgkr.cn-bj.ufileos.com/ad0d5094-04f7-412e-a46f-b05819c0218f.png)

![结果展示](https://imgkr.cn-bj.ufileos.com/2be6ad26-cf1e-41e7-9c57-c5941b2e9dbe.png)

- 插值法

![](https://imgkr.cn-bj.ufileos.com/2ac593aa-fe3c-4ee3-93c7-fe0cac07f874.png)

![结果展示](https://imgkr.cn-bj.ufileos.com/fe705f59-213e-4579-b5cb-628dde96dd9a.png)

程序过长, 源代码见原文链接. 肉眼可见, 最小二乘法逼近效果更好, 但其系数矩阵更复杂一些.

### 小结

上次推送了重要的`拉格朗日多项式`作基函数, 结合上述例题, 知用于`插值法`中, 可使得系数矩阵 $A=I$ 为单位矩阵, 但是, 应用到`最小二乘法`中, 系数矩阵却不是[稀疏矩阵](https://en.wikipedia.org/wiki/Sparse_matrix "稀疏矩阵")的, 因为

$$
A\_{i, j} =\left(\psi\_{i}, \psi_{j}\right) \neq 0.
$$

![N=1](https://imgkr.cn-bj.ufileos.com/083a9174-aa6e-47cf-b4f5-f1b2126b9572.png "两个节点")

![N=2](https://imgkr.cn-bj.ufileos.com/924d5fa6-9124-44f9-939f-c72221b5d5d6.png "三个节点")

![N=3](https://imgkr.cn-bj.ufileos.com/c8ef646c-730a-44e7-8554-ca6befead4c0.png "四个节点")

因此, 本次继续讨论逼近函数问题, 考虑 ..有限元基函数.. .

---

## 有限元基函数

### 引子

在之前 3 期推送(逼近函数)中, 基函数 $\psi_i(x), i \in {\mathcal{I}_s}$ 在整个区域 $\Omega$ 上一般都是非零的, 如下图所示.

![$u(x)=4\psi_0(x)-\frac{1}{2}\psi_1(x)$](https://imgkr.cn-bj.ufileos.com/856a7f13-620b-426b-909a-31f57f18c3f7.png)

而有限元法要求基函数有[紧支撑](http://mathworld.wolfram.com/CompactSupport.html "紧支撑"), 即它们只有在一小部分区域内是非零的, 在大部分区域都是零. 另外, 一般要求基函数是分段多项式函数, 如下图所示

![](https://imgkr.cn-bj.ufileos.com/355f0ce0-2714-44ed-8c01-7939ff089172.png)

### 单元和节点

$\color{gray}{\textit{Elements and nodes}}$

将区域 $\Omega$ 剖分为有限个`互补重叠`的子区域 $\Omega^{(e)}, e=0,\dots, N_e$:

$$
\Omega=\Omega^{(0)} \cup \cdots \cup \Omega^{\left(N_{e}\right)}
$$

称这样的子区域为`单元`, 每个单元有一个区分其他单元的上标 $^{(e)}$. 然后, 在每个单元 $\Omega^{(e)}$ 上定义`点`的集合, 命名为`节点`. 为区分不同节点, 我们还需要一套节点的`全局编号`, 并且在每个小单元上定义`局部编号`.

![有 5 个单元 6 个节点的有限元网格](https://imgkr.cn-bj.ufileos.com/da8653b4-fd8f-4f76-958c-746ab875e1c3.png)

单元和节点完全定义了`有限元网格`, 即完成了对空间的离散. 上图为常见的均匀剖分网格, 即单元的规格相同, 节点间的距离也相同.

> **一个例子**  
> $\Omega=[0, 1]$ 内剖分为两个单元:
>
> ![2 个单元 5 个节点的单位有限元网格](https://imgkr.cn-bj.ufileos.com/f8f1b018-16d8-455c-99ea-ebc117f6c033.png)
>
> \begin{aligned}
> \Omega^{(0)}=[0, 0.4]\\\\
> \Omega^{(1)}=[0.4, 1]
> \end{aligned}
>
> 每个单元内有 3 个节点. 则有全局编号
>
> | 全局编号 |  0  |  1  |  2  |  3  |  4  |
> | :------: | :-: | :-: | :-: | :-: | :-: |
> |   坐标   |  0  | 0.2 | 0.4 | 0.7 |  1  |
>
> 因此, `节点信息`用向量表示
>
> ```matlab
> nodes = [0, 0.2, 0.4, 0.7, 1];
> ```
>
> 每个单元由三个节点组成
>
> | 局部编号 | 0 | 1 | 2 |
> | :---: | :---: | :---: | :---: |
> | $\Omega^{(0)}$ | 0 | 1 | 2 |
> | $\Omega^{(1)}$ | 2 | 3 | 4 |
>
> 因此, `单元信息`用矩阵信息
>
> ```matlab
> elements= [0, 1, 2;
>            2, 3, 4];
> ```

### 基函数

有限元基函数用 $\varphi_i(x)$ 表示, 索引 $i$ 为节点的全局编码, 即基函数的个数等于节点的个数. 在逼近函数问题时, 我们另 $\psi_i(x) = \varphi_i(x)$.

#### 构造原理

为方便, 在单元 $e$ 中, 令 $i$ 为全局编号, $r$ 为局部编号, 有限元基函数构造遵循以下规则:

- $r$ 为单元 $e$ 内部编号:  
  选取 $\varphi_i$ 在 单元 $e$ 内 $r$ 处为 1, 其他节点为 0; 在其他单元上 $\varphi_i(x) \equiv 0$.
- $r$ 为单元 $e$ 边界编号:  
  选取 $\varphi_i$ 在单元 $e$ 和单元 $e+1$ 上不恒为 0 ($ \varphi_i \not\equiv0$), 具体的, 在 $r$ 处等于 1, 其他节点处等于 0. 而在其他单元上, $\varphi_i(x) \equiv 0$.

下图展示对这两条规则直观的理解

![$\Omega^{(1)}$ 内的三个基函数](https://imgkr.cn-bj.ufileos.com/b1fd8d22-ae6f-4dc7-834d-a06911bec573.png)

#### $\varphi_i$ 的性质

- $$
\varphi\_{i}\left(x\_{j}\right)=\delta\_{i j}, \quad \delta_{i j}=
\left\\{\begin{array}{ll}
{1,} & {i=j} \\\\
{0,} & {i \neq j}
\end{array}\right.
$$

从而

$$
u\left(x\_{i}\right)=\sum\_{j \in \mathcal{I}\_{s}} c\_{j} \psi\_{j}\left(x\_{i}\right)=\sum\_{j \in \mathcal{I}\_{s}} c\_{j} \varphi\_{j}\left(x\_{i}\right)=c\_{i} \varphi\_{i}\left(x\_{i}\right)=c\_{i}
$$

即 `..系数..` $c_i$ 的值等于 $u$ 在 $i$ 处的函数值(数值解).

- $\varphi_i(x)$ 在区域 $\Omega$ 的大部分区域等于 0.

   - $\varphi_i(x)\neq 0$ 仅在有全局节点 $i$ 的单元中成立.
   - $\varphi_i(x)\varphi_j(x)\neq 0$ 仅在同时有全局节点 $i$ 和全局节点 $j$ 的单元中成立.

因此, $A\_{ij} = \int\_{\Omega^{(e)}} \varphi \_i(x) \varphi\_j(x) {\rm d} x $ 在系数矩阵中大多等于 0.

假设每个单元有 $d+1$ 个节点, 那么局部拉格朗日多项式的次数是 $d$.

#### 分段线性有限元基函数

$$
\varphi\_{i}(x)=
\begin{cases}
0, \quad & x < x\_{i-1} \\\\
(x-x\_{i-1})/h,  & x\_{i-1} \leq x < x\_i \\\\
1-(x-x\_{i-1})/h,  & x\_{i}  \leq x < x\_{i+1} \\\\
0, & x \geq x\_{i+1}
\end{cases}
$$

![P1 元](https://imgkr.cn-bj.ufileos.com/5b252f1d-7d4a-4367-a7ae-dd95be8b85ec.png)

#### 分段二次有限元基函数

![P2 元](https://imgkr.cn-bj.ufileos.com/8c2784e1-11de-4f02-95f0-36ba5303b9af.png)

**在每一个单元上, 都是拉格朗日多项式作基函数**

### 建立线性方程组

#### 组装系数矩阵

$$
[A\_{i,j}] = \big(\varphi\_j(x), \varphi\_i(x)\big).
$$

![系数矩阵](https://imgkr.cn-bj.ufileos.com/af886738-a916-4c3a-82fb-d191a368ffd3.png)

由基函数的性质, 可知只有 $A\_{i, i}$ 或者 $A\_{i,i-1}=A_{i.i+1}$ 不为 0, 即 $A$ 为三对角阵.

当 $0<i<N$

\begin{aligned}
A\_{i,i} & = \int\_{\Omega} \varphi\_i^2 {\rm d} x \\\\
& = \int\_{i-1}^{i} \varphi\_i^2 {\rm d} x + \int\_{i}^{i-1} \varphi\_i^2 {\rm d} x \\\\
&=\int\_{i-1}^{i} \left(\frac{x-x\_{i-1}}{h}\right)^2 {\rm d} x + \int\_{i}^{i-1} \left(1-\frac{x-x_{i}}{h}\right)^2 {\rm d} x \\\\
& = \frac{2h}{3}.
\end{aligned}

以及 $0 < i \leq N$

<img src="https://imgkr.cn-bj.ufileos.com/92813566-6697-4c2f-8205-e71f1cf3531a.png" width="500" alt="有限元公式"/>

$A\_{i,i+1}=A_{i,i-1}$.最后显然,

$$
A\_{0,0}=\int\_{\Omega} \varphi\_{0}^{2} \mathrm{d} x=\int\_{x\_{0}}^{x\_{1}}\left(1-\frac{x-x\_{0}}{h}\right)^{2} \mathrm{d} x=\frac{h}{3}.
$$

$
A\_{N, N}=A\_{0, 0}.
$

#### 载入右端项

\begin{aligned}
b\_{i}&=\int\_{\Omega} \varphi\_{i}(x) f(x) \mathrm{d} x \\\\
& = \int\_{x\_{i-1}}^{x\_{i}} \frac{x-x\_{i-1}}{h} f(x) \mathrm{d} x+\int\_{x\_{i}}^{x\_{i+1}}\left(1-\frac{x-x_{i}}{h}\right) f(x) \mathrm{d} x
\end{aligned}

![右端项](https://imgkr.cn-bj.ufileos.com/91613bcd-7a64-48ac-9f13-4d75f2a6216a.png)

### 例题

> 将 $\Omega = [0, 1]$ 划分为两个相同的的子区域, 设 $f(x)=x(1-x)$, 利用一阶有限元基函数(P1)计算最佳逼近 $u(x)$.

利用上述公式, 得到

$$
A=\frac{h}{6}\left[\begin{array}{lll}
{2} & {1} & {0} \\\\
{1} & {4} & {1} \\\\
{0} & {1} & {2}
\end{array}\right], \quad b=\frac{h^{2}}{12}\left[\begin{array}{c}
{2-3 h} \\\\
{12-14 h} \\\\
{10-17 h}
\end{array}\right].
$$

进而得到

$$
c\_{0}=\frac{h^{2}}{6}, \quad c\_{1}=h-\frac{5}{6} h^{2}, \quad c_{2}=2 h-\frac{23}{6} h^{2}.
$$

所以,

$$
u(x)=c\_{0} \varphi\_{0}(x)+c\_{1} \varphi\_{1}(x)+c\_{2} \varphi\_{2}(x).
$$

利用计算机绘图得到

![左: 2 个节点  右: 4 个节点](https://imgkr.cn-bj.ufileos.com/82d4dc49-5731-4afa-a036-e5da8b2e9bb2.png)

### 小结

有限元基函数可以保证最小二乘法的系数矩阵是稀疏的, 而且基函数是简单的多项式.

!["帽子"函数](https://imgkr.cn-bj.ufileos.com/64498351-25f9-435e-8951-704f5883d9e0.png)

---

## 下节预告

有限元计算在实际中不可能是手算的, 所以下次介绍一下编程技巧.
