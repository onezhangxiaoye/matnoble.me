+++
title = "「手撕」奇异值分解"
description = "矩阵"
date = "2020-03-16T00:14:37+00:00"
categories = ["MATH","线代拾遗"]
tags = ["奇异值分解"]
keywords = ["线性方程组","奇异值分解","system of linear equations","SVD","线性代数","最小二乘法","matrix","linear algebra","leastsquares","MatNoble"]
toc = true
mathjax = true
series = ["mla"]
+++

设 ${\boldsymbol{A}}=\Biggl[ \begin{smallmatrix} 1 & 0 \\\\ 0 & 1 \\\\ 1 & 1 \end{smallmatrix} \Biggr]$, $x \in \mathbb{R}$, 计算 $\boldsymbol{A}$ 的奇异值分解.

<br>

以下分两步计算:

- 计算右奇异矩阵 $\boldsymbol{V}$<br>
因为 $\boldsymbol{A} = \boldsymbol{U}\boldsymbol{\Sigma}\boldsymbol{V}^\mathsf{T}$, 所以 $\boldsymbol{A}^\mathsf{T}\boldsymbol{A} = \boldsymbol{V}(\boldsymbol{\Sigma}^\mathsf{T}\boldsymbol{\Sigma})\boldsymbol{V}^\mathsf{T}$<br>
$$\boldsymbol{A}^\mathsf{T}\boldsymbol{A} = \begin{bmatrix} 
1 & 0 & 1
\\\\ 
0 & 1 & 1
\end{bmatrix} 
\begin{bmatrix} 
1 & 0 \\\\ 0 & 1 \\\\ 1 & 1 
\end{bmatrix} = \begin{bmatrix}
2 & 1 \\\\\\
1 & 2
\end{bmatrix}
$$
利用 $\det(\boldsymbol{A}^\mathsf{T}\boldsymbol{A}-\lambda\boldsymbol{I})=0$ 计算特征值
$$
\begin{aligned}
\begin{vmatrix}
2-\lambda & 1 \\\\\\
1 & 2-\lambda
\end{vmatrix} & = (2-\lambda)^2 - 1 
\\\\\[3pt]
& = \lambda^2 - 4\lambda + 3
\\\\\[3pt]
& = (\lambda - 3) (\lambda-1)
\end{aligned}
$$
则特征值 $\lambda\_1 = 3, \lambda\_2=1$. 代入 $\Bigl[\begin{smallmatrix}
2-\lambda & 1 \\\\\\
1 & 2-\lambda
\end{smallmatrix}\Bigr]\mathbf{x} = \mathbf{b}$ 计算特征向量
  - $\lambda\_1 = 3$
  $$
  \begin{bmatrix}
  -1 & 1 \\\\\\
  1 & -1
  \end{bmatrix}
  $$
  
  - $\lambda\_1 = 1$


- 

$$\boldsymbol{A}^\mathsf{T}\boldsymbol{A} = \begin{bmatrix} 
1 & 0 & x
\\\\ 
0 & 1 & x
\end{bmatrix} 
\begin{bmatrix} 
1 & 0 \\\\ 0 & 1 \\\\ x & x 
\end{bmatrix} = \begin{bmatrix}
1+x^2 & x^2 \\\\\\
x^2 & 1+x^2
\end{bmatrix}
$$<br>
利用 $\det(\boldsymbol{A}^\mathsf{T}\boldsymbol{A}-\lambda\boldsymbol{I})=0$ 计算特征值<br>
$$
\begin{aligned}
\begin{vmatrix}
1+x^2-\lambda & x^2 \\\\\\
x^2 & 1+x^2-\lambda
\end{vmatrix} & = [(1+x^2)-\lambda]^2 - x^4 
\\\\\[3pt]
& = \lambda^2 - 2(1+x^2)\lambda +(1+2x^2)
\\\\\[3pt]
& = [\lambda - (1+2x^2)] \\, (\lambda-1)
\end{aligned}
$$<br>
则特征值 $\lambda\_1 = 1+2x^2, \lambda\_2=1$.
