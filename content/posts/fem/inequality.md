+++
title = "Inequality"
description = "Sometimes 「inequality」 is more important than 「equation」"
categories = ["MATH","数学基础"]
tags = [""]
keywords = ["不等式","inequality","Cauchy inequality","Young's inequality","Cauchy inequality for scalar product","Holder inequality","FEM"]
date = "2020-03-17T00:21:47+00:00"
toc = true
mathjax = true
+++

## Cauchy inequality

Let $a, b$ are any real numbers, then

\begin{equation}
\label{eq:eqc}
    ab \leq \frac{1}{2}(a^{2} + b^{2}),\quad (Cauchy\ inequality)
\end{equation}

\begin{equation}
\label{eq:eqce}
    ab \leq \epsilon a^{2} + \frac{b^{2}}{4\epsilon},\,\forall \epsilon > 0,\quad (Cauchy\ inequality\ with\ epsilon)
\end{equation}

**Proof.**

$$
(a-b)^{2} \geq 0 \Rightarrow ab \leq\frac{1}{2}(a^{2} + b^{2}).
$$

Constant deformation with $\epsilon$

$$
\begin{aligned}
      ab &= ((2\epsilon)^{\frac{1}{2}}a)(\frac{b}{(2\epsilon)^{\frac{1}{2}}}) \\\\[3pt]
         &\leq \frac{1}{2} [((2\epsilon)^{\frac{1}{2}}a)^2 + (\frac{b}{(2\epsilon)^{\frac{1}{2}}})^2] \\\\[3pt]
         &= \frac{1}{2} (2\epsilon a^{2} + \frac{b^{2}}{2\epsilon}) \\\\[3pt]
         &= \epsilon a^{2} + \frac{b^{2}}{4\epsilon}.
\end{aligned}
$$
<p style="text-align: right">
$\blacksquare$
</p>

### Cauchy inequality for scalar product

Let $\lVert \mathbf{x} \rVert^2 = \sum\_{k=1}^n \lvert x \rvert^2$, $\langle \mathbf{x}, \mathbf{y} \rangle = \sum\_{k=1}^n x_k \bar{y}\_k$, which $\mathbf{x} = \\{ x\_k \\}\_{k=1,\ldots,n}, \mathbf{y} = \\{ y\_k \\}\_{k=1,\ldots,n}$ then

\begin{equation}
\langle \mathbf{x}, \mathbf{y} \rangle \leq \lVert \mathbf{x} \rVert \lVert \mathbf{y} \rVert 
\end{equation}

**Proof.** We have
$$
f(\lambda) = \lVert \mathbf{x} + \lambda\mathbf{y}\rVert^2 \geq 0, \quad \forall \lambda \in \mathbb{R}
$$
Thus the quadratic function
$$
f(\lambda) = \lVert \mathbf{y} \rVert^2 \lambda^2 +  2\langle \mathbf{x}, \mathbf{y} \rangle \lambda + \lVert \mathbf{x} \rVert^2 \geq 0
$$
According to *the discriminant of the quadratic polynomial*
$$
\langle \mathbf{x}, \mathbf{y} \rangle ^2 \leq \lVert \mathbf{x} \rVert^2 \lVert \mathbf{y} \rVert^2
$$
<p style="text-align: right">
$\blacksquare$
</p>

## Young's inequality

For $a, b \geq 0$ and $p,q \geq 1$ such that $ \frac{1}{p} + \frac{1}{q} = 1$, then

\begin{equation}
\label{eq:eqy}
    ab \leq \frac{a^{p}}{p} + \frac{b^{q}}{q}. \quad (Young\ inequality)
\end{equation}

**Proof.** The function $x \mapsto e^x$ is convex. This means that for $x, y\in \mathbb{R}$ and $0\leq \theta \leq 1$

$$
\mbox{exp}(\theta x + (1-\theta)y) \leq \theta\mbox{exp}(x) + (1-\theta)\mbox{exp}(y)
$$

When $a$ or $b$ are zero the inequality is trivial. Otherwise, the theorem is just this inequality with

$$
x:=  p \ln a \quad y:= q \ln b \quad \theta = \frac{1}{p}
$$
<p style="text-align: right">
$\blacksquare$
</p>

There is a more general theorem[^1]

## Holder inequality

Let $p, q$ are real numbers $1\leq p, q\leq \infty$ connected by the relationship $\frac{1}{p} + \frac{1}{q} = 1$ and $u \in L^p, v \in L^q$. then

\begin{equation}
    \int \lvert uv \rvert \\,\mathrm{d}x \leq \sqrt[p]{\int \lvert u \rvert \\,\mathrm{d}x} \sqrt[q]{\int \lvert v \rvert \\,\mathrm{d}x}
\label{eq:eqh}
\end{equation}

**Proof.** The formula Young inequality (\ref{eq:eqy}) implies
$$
\int \lvert ab \rvert \\,\mathrm{d}x \leq \frac{1}{p} \int \lvert a \rvert^p \\,\mathrm{d}x + \frac{1}{q} \int \lvert b \rvert^q \\,\mathrm{d}x
$$

set $a=\frac{|u|}{c\_1}, a=\frac{|v|}{c\_2}$, where $c\_1=\sqrt[p]{\int \lvert u \rvert \\,\mathrm{d}x}$ and $\sqrt[q]{\int \lvert v \rvert \\,\mathrm{d}x}$, then

$$
\begin{aligned}
\frac{1}{c\_1c\_2} \int \lvert uv \rvert \\,\mathrm{d}x & \leq \frac{1}{p} \int \Biggl| \frac{|u|}{c\_1} \Biggr| ^p \\,\mathrm{d}x + \frac{1}{q} \int \Biggl| \frac{|v|}{c\_2} \Biggr| ^q \\,\mathrm{d}x \\\\[3pt]
& = \frac{1}{p} + \frac{1}{q} \\\\[3pt]
& = 1
\end{aligned}
$$
Hence
$$
\int \lvert uv \rvert \\,\mathrm{d}x \leq c\_1 c\_2 = \sqrt[p]{\int \lvert u \rvert \\,\mathrm{d}x} \sqrt[q]{\int \lvert v \rvert \\,\mathrm{d}x}
$$
<p style="text-align: right">
$\blacksquare$
</p>

[^1]: General Young’s inequality https://canizo.org/tex/young.pdf
