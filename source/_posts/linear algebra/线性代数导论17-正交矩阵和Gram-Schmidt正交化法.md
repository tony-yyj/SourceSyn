---
title: 线性代数导论(17)-正交矩阵和Gram-Schmidt正交化法(最新讲义)
tags: 线性代数
categories: 线性代数
abbrlink: 2077705030
date: 2017-08-14 10:20:20
---

<!-- toc -->
<!-- more -->

# 1. 标准正交矩阵

## 1.1. 标准正交基

一组基里的向量，任意$q$ 都和其他$q$ 正交，两两垂直，内积为零，且$q_i$不和自己正交，$q_i$的长度为1，这样的向量组叫标准正交基（orthonormal vectors）：
 {% math %}q_i^Tq_j=\begin{cases}0\quad i\neq j\\1\quad i=j\end{cases}{% endmath %}

## 1.2. 标准正交矩阵$Q$

将标准正交向量放入矩阵中，有
$Q=\Bigg[q_1 q_2 \cdots q_n\Bigg]$。

$Q^TQ=\begin{bmatrix} & q_1^T & \\ & q_2^T & \\ & \vdots & \\ & q_n^T & \end{bmatrix}\Bigg[q_1 q_2 \cdots q_n\Bigg]$

根据标准正交向量的定义，计算
{% math %}Q^TQ=\begin{bmatrix}1&0&\cdots&0\\0&1&\cdots&0\\\vdots&\vdots&\ddots&\vdots\\0&0&\cdots&1\end{bmatrix}=I{% endmath %}
我们也把$Q$称为标准正交矩阵（orthonormal matrix）。

## 1.3. $Q$恰好是方阵时

特别的，当$Q$恰好是方阵时，由于正交性，易得$Q$是可逆的，又$Q^TQ=I$，所以$Q^T=Q^{-1}$。

举个置换矩阵的例子：
{% math %}Q=\begin{bmatrix}0&1&0\\1&0&0\\0&0&1\end{bmatrix}$，则$Q^T=\begin{bmatrix}0&1&0\\0&0&1\\1&0&0\end{bmatrix}{% endmath %}，易得$Q^TQ=I$。

## 1.4. 举几个正交矩阵的例子

 * 使用上一讲的例子
 $Q=\begin{bmatrix}\cos\theta&-\sin\theta\\\sin\theta&\cos\theta\end{bmatrix}$
 列向量长度为$1$，且列向量相互正交。

* 其他例子{% math %}Q=\frac{1}{\sqrt 2}\begin{bmatrix}1&1\\1&-1\end{bmatrix}{% endmath %}列向量长度为$1$，且列向量相互正交。

## 1.5. 阿德玛矩阵
是一种只有 1 和-1 的正交矩阵
* 使用上一个例子的矩阵，令{% math %}Q'=c\begin{bmatrix}Q&Q\\Q&-Q\end{bmatrix}{% endmath %}，取合适的$c$另列向量长度为$1$也可以构造标准正交矩阵：
{% math %}Q=\frac{1}{2}\begin{bmatrix}1&1&1&1\\1&-1&1&-1\\1&1&-1&-1\\1&-1&-1&1\end{bmatrix}{% endmath %}
这种构造方法以阿德玛（Adhemar）命名，对$2, 4, 16, 64, \cdots$阶矩阵有效(2 维，4 维，16 维，64 维)

* 再来看一个例子，
{% math %}Q=\frac{1}{3}\begin{bmatrix}1&-2&2\\2&-1&-2\\2&2&1\end{bmatrix}{% endmath %}
列向量长度为$1$，且列向量相互正交。格拉姆-施密特正交化法的缺点在于，由于要求得单位向量，所以我们总是除以向量的长度，这导致标准正交矩阵中总是带有根号，而上面几个例子很少有根号。

## 1.6. 再来看标准正交化有什么好处

假设要做投影，将向量$b$投影在标准正交矩阵$Q$的列空间中，根据上一讲的公式得$P=Q(Q^TQ)^{-1}Q^T$，易得$P=QQ^T$。我们断言，当列向量为标准正交基时，$QQ^T$是投影矩阵。
极端情况，假设矩阵是方阵，而其列向量是标准正交的，则其列空间就是整个向量空间，而投影整个空间的投影矩阵就是单位矩阵，此时$QQ^T=I$。

可以验证一下投影矩阵的两个性质：
$(QQ^T)^T=(Q^T)^TQ^T=QQ^T$，得证；
$(QQ^T)^2=QQ^TQQ^T=Q(Q^TQ)Q^T=QQ^T$，得证。

我们计算的$A^TA\hat x=A^Tb$，现在变为$Q^TQ\hat x=Q^Tb$，也就是$\hat x=Q^Tb$，分解开来看就是 $\underline{\hat x_i=q_i^Tb}$，这个式子在很多数学领域都有重要作用。当我们知道标准正交基，则解向量第$i$个分量为基的第$i$个分量乘以$b$，在第$i$个基方向上的投影就等于$q_i^Tb$。

# 2. Gram-Schmidt正交化法

格拉姆-施密特正交化的目标是让列向量线性无关的矩阵正交化（向量垂直且长度为1）。（就像消元法的目标是将矩阵变成三角矩阵）

## 2.1. 格拉姆-施密特公式
我们有两个线性无关的向量$a, b$，先把它们化为正交向量$A, B$，再将它们单位化，变为单位正交向量$q_1=\frac{A}{\left\|A\right\|}, q_2=\frac{B}{\left\|B\right\|}$：

* 我们取定$a$向量的方向，$a=A$；
* 接下来将$b$投影在$A$的法方向上得到$B$，也就是求子空间投影一讲中，我们提到的误差向量$e=b-p$，即$B=b-\frac{A^Tb}{A^TA}A$(格拉姆-施密特公式)。
* 检验一下$A\bot B$，$A^TB=A^Tb-A^T\frac{A^Tb}{A^TA}A=A^Tb-\frac{A^TA}{A^TA}A^Tb=0$。（$\frac{A^Tb}{A^TA}A$就是$A\hat x=p$。）

## 2.2. 得到正交与A,B的C

如果我们有三个线性无关的向量$a, b, c$，则我们现需要求它们的正交向量$A, B, C$，再将它们单位化，变为单位正交向量$q_1=\frac{A}{\left\|A\right\|}, q_2=\frac{B}{\left\|B\right\|}, q_3=\frac{C}{\left\|C\right\|}$：

* 前两个向量我们已经得到了，我们现在需要求第三个向量同时正交于$A, B$；
* 我们依然沿用上面的方法，从$c$中减去其在$A, B$上的分量，得到正交与$A, B$的$C$：$C=c-\frac{A^Tc}{A^TA}A-\frac{B^Tc}{B^TB}B$。

## 2.3. 现在我们试验一下推导出来的公式

一个例子，已知两个向量a,b，求格拉姆-施密特标准正交基Q，Q 的列空间和原来的矩阵列空间是一样的。
{% math %}a=\begin{bmatrix}1\\1\\1\end{bmatrix}, b=\begin{bmatrix}1\\0\\2\end{bmatrix}{% endmath %}
 则
 {% math %}A=a=\begin{bmatrix}1\\1\\1\end{bmatrix}{% endmath %}
 
根据公式有$B=a-hA$，$h$是比值{% math %}\frac{A^Tb}{A^TA}=\frac{3}{3}{% endmath %}，则
{% math %}B=\begin{bmatrix}1\\1\\1\end{bmatrix}-\frac{3}{3}\begin{bmatrix}1\\0\\2\end{bmatrix}=\begin{bmatrix}0\\-1\\1\end{bmatrix}{% endmath %}

验证一下正交性有$A\cdot B=0$。

单位化
{% math %}q_1=\frac{1}{\sqrt 3}\begin{bmatrix}1\\1\\1\end{bmatrix},\quad q_2=\frac{1}{\sqrt 2}\begin{bmatrix}1\\0\\2\end{bmatrix}{% endmath %}
则标准正交矩阵为
{% math %}Q=\begin{bmatrix}\frac{1}{\sqrt 3}&0\\\frac{1}{\sqrt 3}&-\frac{1}{\sqrt 2}\\\frac{1}{\sqrt 3}&\frac{1}{\sqrt 2}\end{bmatrix}{% endmath %}
对比原来的矩阵
{% math %}D=\begin{bmatrix}1&1\\1&0\\1&2\end{bmatrix}{% endmath %}
有$D, Q$的列空间是相同的，我们只是将原来的基标准正交化了。

我们曾经用矩阵的眼光审视消元法，有$A=LU$。同样的，我们也用矩阵表达标准正交化，$A=QR$。也就是说一个由线性无关的向量组成的矩阵A，与格拉姆-施密特标准正交化矩阵Q 的关系是一个上三角
矩阵R。

设矩阵$A$有两个列向量$\Bigg[a_1 a_2\Bigg]$;
则标准正交化后有
{% math %}\Bigg[a_1 a_2\Bigg]=\Bigg[q_1 q_2\Bigg]\begin{bmatrix}a_1^Tq_1&a_2^Tq_1\\a_1^Tq_2&a_2^Tq_2\end{bmatrix}{% endmath %}
而左下角的$a_1^Tq_2$始终为$0$:因为Gram-Schmidt正交化总是使得$a_1\bot q_2$，后来构造的向量总是正交于先前的向量。所以这个$R$矩阵是一个上三角矩阵。
