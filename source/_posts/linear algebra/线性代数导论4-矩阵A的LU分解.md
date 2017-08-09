---
title: 线性代数导论4-矩阵A的LU分解
tags: 线性代数
categories: 线性代数
abbrlink: 2283559014
date: 2017-08-08 19:40:11
---

<!-- toc -->
<!-- more -->
# 1. 逆矩阵

对一个 $n$ 阶方阵 $A$,，如果存在一个 $n$阶方阵 $B$使 {% math %}AB=BA=I_{n}{% endmath %},（{% math %}I_{n}{% endmath %}是单位矩阵），则称 $A$是可逆的，也称 $A$为非奇异矩阵。 $B$是$A$的逆阵。

$AB$的逆矩阵：
{% math %}
\begin{aligned}
A \cdot A^{-1} = I & = A^{-1} \cdot A\\
(AB) \cdot (B^{-1}A^{-1}) & = I\\
\textrm{则} AB \textrm{的逆矩阵为} & B^{-1}A^{-1}
\end{aligned}
{% endmath %}

{% math %}A^{T}{% endmath %}的逆矩阵：
{% math %}
\begin{aligned}
(A \cdot A^{-1})^{T} & = I^{T}\\
(A^{-1})^{T} \cdot A^{T} & = I\\
\textrm{则} A^{T} \textrm{的逆矩阵为} & (A^{-1})^{T}
\end{aligned}
{% endmath %}

# 2. LU分解

LU分解是矩阵分解的一种，可以将一个矩阵分解为一个**下三角矩阵**和一个**上三角矩阵**的乘积（有时是它们和一个置换矩阵的乘积）。LU分解主要应用在数值分析中，用来解线性方程、求逆矩阵或计算行列式。

例子

{% math %}
{\begin{bmatrix}a_{{11}}&a_{{12}}&a_{{13}}\\a_{{21}}&a_{{22}}&a_{{23}}\\a_{{31}}&a_{{32}}&a_{{33}}\\\end{bmatrix}}={\begin{bmatrix}l_{{11}}&0&0\\l_{{21}}&l_{{22}}&0\\l_{{31}}&l_{{32}}&l_{{33}}\\\end{bmatrix}}{\begin{bmatrix}u_{{11}}&u_{{12}}&u_{{13}}\\0&u_{{22}}&u_{{23}}\\0&0&u_{{33}}\\\end{bmatrix}}
{% endmath %}

将一个简单的3×3矩阵A进行LU分解：
{% math %}
A={\begin{bmatrix}1&2&3\\2&5&7\\3&5&3\\\end{bmatrix}}
{% endmath %}
先将矩阵第一列元素中a11以下的所有元素变为0，即
{% math %}
L_{{1}}A={\begin{bmatrix}1&0&0\\-2&1&0\\-3&0&1\\\end{bmatrix}}\times {\begin{bmatrix}1&2&3\\2&5&7\\3&5&3\\\end{bmatrix}}={\begin{bmatrix}1&2&3\\0&1&1\\0&-1&-6\\\end{bmatrix}}
{% endmath %}

再将矩阵第二列元素中a22以下的所有元素变为0，即
{% math %}
L_{{2}}(L_{{1}}A)={\begin{bmatrix}1&0&0\\0&1&0\\0&1&1\\\end{bmatrix}}\times {\begin{bmatrix}1&2&3\\0&1&1\\0&-1&-6\\\end{bmatrix}}={\begin{bmatrix}1&2&3\\0&1&1\\0&0&-5\\\end{bmatrix}}=U
{% endmath %}

{% math %}
L=L_{{1}}^{{-1}}L_{{2}}^{{-1}}={\begin{bmatrix}1&0&0\\2&1&0\\3&0&1\\\end{bmatrix}}\times {\begin{bmatrix}1&0&0\\0&1&0\\0&-1&1\\\end{bmatrix}}={\begin{bmatrix}1&0&0\\2&1&0\\3&-1&1\\\end{bmatrix}}
{% endmath %}

A=LU，如果不存在行互换，消元乘数（即消元步骤中的需要乘以并减去的那个倍数），消元乘数可以直接写入L中。即只要步骤正确，可以在得到LU过程中把A抛开

有时我们将U中的主元提取出来，其余的位置设为0，即diagonal对角阵D，可分解得到LDU，两边各一个三角矩阵，中间一个对角阵。

# 3. 将一个 $n$ 阶方阵 $A$ 变换为 $LU$ 需要的计算量估计：

1. 第一步，将{% math %}a_{11}{% endmath %}作为主元，需要的运算量约为{% math %}n^2{% endmath %}
{% math %}
\begin{bmatrix}
a_{11} & a_{12} & \cdots & a_{1n} \\
a_{21} & a_{22} & \cdots & a_{2n} \\
\vdots & \vdots & \ddots & \vdots \\
a_{n1} & a_{n2} & \cdots & a_{nn} \\
\end{bmatrix}
\underrightarrow{消元}
\begin{bmatrix}
a_{11} & a_{12} & \cdots & a_{1n} \\
0      & a_{22} & \cdots & a_{2n} \\
0      & \vdots & \ddots & \vdots \\
0      & a_{n2} & \cdots & a_{nn} \\
\end{bmatrix}
{% endmath %}

2. 以此类推，接下来每一步计算量约为$(n-1)^2、(n-2)^2、\cdots、2^2、1^2$。

3. 则将 $A$ 变换为 $LU$ 的总运算量应为{% math %}O(n^2+(n-1)^2+\cdots+2^2+1^2){% endmath %}，即{% math %}O(\frac{n^3}{3}){% endmath %}。

# 4. 置换矩阵(Permutation Matrix)

方阵是行数及列数皆相同的矩阵
3阶方阵的置换矩阵有6个：
{% math %}
\begin{bmatrix}
1 & 0 & 0 \\
0 & 1 & 0 \\
0 & 0 & 1 \\
\end{bmatrix}
\begin{bmatrix}
0 & 1 & 0 \\
1 & 0 & 0 \\
0 & 0 & 1 \\
\end{bmatrix}
\begin{bmatrix}
0 & 0 & 1 \\
0 & 1 & 0 \\
1 & 0 & 0 \\
\end{bmatrix}
\begin{bmatrix}
1 & 0 & 0 \\
0 & 0 & 1 \\
0 & 1 & 0 \\
\end{bmatrix}
\begin{bmatrix}
0 & 1 & 0 \\
0 & 0 & 1 \\
1 & 0 & 0 \\
\end{bmatrix}
\begin{bmatrix}
0 & 0 & 1 \\
1 & 0 & 0 \\
0 & 1 & 0 \\
\end{bmatrix}
{% endmath %}

$n$阶方阵的置换矩阵有{% math %}\binom{n}{1}=n!{% endmath %}个。
