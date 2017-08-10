---
abbrlink: 2
---

# 第十一讲：矩阵空间、秩1矩阵和小世界图

## 矩阵空间

接上一讲，使用{% math %}3 \times 3{% endmath %}矩阵举例，其矩阵空间记为$M$。

则$M$的一组基为：
$
\begin{bmatrix}
1 & 0 & 0 \\
0 & 0 & 0 \\
0 & 0 & 0 \\
\end{bmatrix}
\begin{bmatrix}
0 & 1 & 0 \\
0 & 0 & 0 \\
0 & 0 & 0 \\
\end{bmatrix}
\begin{bmatrix}
0 & 0 & 1 \\
0 & 0 & 0 \\
0 & 0 & 0 \\
\end{bmatrix} \\
\begin{bmatrix}
0 & 0 & 0 \\
1 & 0 & 0 \\
0 & 0 & 0 \\
\end{bmatrix}
\begin{bmatrix}
0 & 0 & 0 \\
0 & 1 & 0 \\
0 & 0 & 0 \\
\end{bmatrix}
\begin{bmatrix}
0 & 0 & 0 \\
0 & 0 & 1 \\
0 & 0 & 0 \\
\end{bmatrix} \\
\begin{bmatrix}
0 & 0 & 0 \\
0 & 0 & 0 \\
1 & 0 & 0 \\
\end{bmatrix}
\begin{bmatrix}
0 & 0 & 0 \\
0 & 0 & 0 \\
0 & 1 & 0 \\
\end{bmatrix}
\begin{bmatrix}
0 & 0 & 0 \\
0 & 0 & 0 \\
0 & 0 & 1 \\
\end{bmatrix} \\
$

易得，{% math %}dim M=9{% endmath %}。

所以可以得出，对上讲中的三阶对称矩阵空间有{% math %}dim S=6{% endmath %}、上三角矩阵空间有{% math %}dim U=6{% endmath %}、对角矩阵空间有{% math %}dim D=3{% endmath %}

求并（intersect）：{% math %}S \cup U=D, dim(S \cup U)=9{% endmath %}；

求交（sum）：{% math %}S \cap U=M, dim(S \cap U)=3{% endmath %}；

可以看出：{% math %}dim S + dim U=12=dim(S \cup U) + dim(S \cap U){% endmath %}。

另一个例子来自微分方程：

{% math %}\frac{d^2y}{dx^2}+y=0{% endmath %}，即{% math %}y''+y=0{% endmath %}

方程的解有：{% math %}y=\cos{x}, \quad y=\sin{x}, \quad y=e^{ix}, \quad y=e^{-ix}{% endmath %}等等（{% math %}e^{ix}=\cos{x}+i\sin{x}, \quad e^{-ix}=\cos{x}-i\sin{x}{% endmath %}）

而该方程的所有解：{% math %}y=c_1 \cos{x} + c_2 \sin{x}{% endmath %}。

所以，该方程的零空间的一组基为{% math %}\cos{x}, \sin{x}{% endmath %}，零空间的维数为$2$。同理{% math %}e^{ix}, e^{-ix}{% endmath %}可以作为另一组基。

## 秩一矩阵

{% math %}2 \times 3{% endmath %}矩阵{% math %}A=\begin{bmatrix}1&4&5\\2&8&10\end{bmatrix}=\begin{bmatrix}1\\2\end{bmatrix}\begin{bmatrix}1&4&5\end{bmatrix}{% endmath %}。

且{% math %}dimC(A)=1=dimC(A^T){% endmath %}，所有的秩一矩阵都可以划为{% math %}A=UV^T{% endmath %}的形式，这里的{% math %}U, V{% endmath %}均为列向量。

秩一矩阵类似“积木”，可以搭建任何矩阵，如对于一个{% math %}5 \times 17{% endmath %}秩为$4$的矩阵，只需要$4$个秩一矩阵就可以组合出来。

令$M$代表所有{% math %}5 \times 17{% endmath %}，$M$中所有秩$4$矩阵组成的集合并不是一个子空间，通常两个秩四矩阵相加，其结果并不是秩四矩阵。

现在，在{% math %}\mathbb{R}^4{% endmath %}空间中有向量{% math %}v=\begin{bmatrix}v_1\\v_2\\v_3\\v_4\end{bmatrix}{% endmath %}，取{% math %}\mathbb{R}^4{% endmath %}中满足{% math %}v_1+v_2+v_3+v_4=0{% endmath %}的所有向量组成一个向量空间$S$，则$S$是一个向量子空间。

易看出，不论是使用系数乘以该向量，或是用两个满足条件的向量相加，其结果仍然落在分量和为零的向量空间中。

求$S$的维数：

从另一个角度看，{% math %}v_1+v_2+v_3+v_4=0{% endmath %}等价于{% math %}\begin{bmatrix}1&1&1&1\end{bmatrix}\begin{bmatrix}v_1\\v_2\\v_3\\v_4\end{bmatrix}=0{% endmath %}，则$S$就是{% math %}A=\begin{bmatrix}1&1&1&1\end{bmatrix}{% endmath %}的零空间。

{% math %}rank(A)=1{% endmath %}，则对其零空间有{% math %}rank(N(A))=n-r=3=dim N(A){% endmath %}，则$S$的维数是$3$。

顺便看一下{% math %}1 \times 4{% endmath %}矩阵$A$的四个基本子空间：

行空间：{% math %}dim C(A^T)=1{% endmath %}，其中的一组基是{% math %}\begin{bmatrix}1\\1\\1\\1\end{bmatrix}{% endmath %}；

零空间：{% math %}dim N(A)=3{% endmath %}，其中的一组基是{% math %}\begin{bmatrix}-1\\1\\0\\0\end{bmatrix}\begin{bmatrix}-1\\0\\1\\0\end{bmatrix}\begin{bmatrix}-1\\0\\0\\1\end{bmatrix}{% endmath %}

列空间：{% math %}dim C(A)=1{% endmath %}，其中一组基是{% math %}\begin{bmatrix}1\end{bmatrix}{% endmath %}，可以看出列空间就是整个{% math %}\mathbb{R}^1{% endmath %}空间。

左零空间：{% math %}dim N(A^T)=0{% endmath %}，因为$A$转置后没有非零的$v$可以使{% math %}Av=0{% endmath %}成立，就是{% math %}\begin{bmatrix}0\end{bmatrix}{% endmath %}。

综上，{% math %}dim C(A^T)+dim N(A)=4=n, dim C(A)+dim N(A^T)=1=m{% endmath %}

## 小世界图

图（graph）由节点（node）与边（edge）组成。

假设，每个人是图中的一个节点，如果两个人为朋友关系，则在这两个人的节点间添加一条边，通常来说，从一个节点到另一个节点只需要不超过$6$步（即六条边）即可到达。
