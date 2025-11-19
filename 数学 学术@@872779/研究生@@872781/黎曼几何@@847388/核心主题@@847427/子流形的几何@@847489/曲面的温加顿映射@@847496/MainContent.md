## 引言
温加滕映射，或称[形状算子](@entry_id:264703)，是微分几何中研究[曲面](@entry_id:267450)几何的基石。它精确地量化了[曲面](@entry_id:267450)如何嵌入周围的三维欧氏空间并发生弯曲，从而在[曲面](@entry_id:267450)的内在属性（如长度和角度）与外在形态之间建立了关键的联系。理解这一算子是深入掌握[曲面论](@entry_id:273972)，乃至现代几何学、物理学和工程学中相关应用的前提。本文旨在系统性地剖析温加滕映射，解决“如何数学化地描述和计算[曲面](@entry_id:267450)弯曲”这一基本问题。

通过本文，读者将踏上一段从基础理论到前沿应用的探索之旅。在第一章“原理和机制”中，我们将建立温加滕映射的形式化定义，揭示其与[第二基本形式](@entry_id:161454)的深刻对偶关系，并推导出[高斯曲率](@entry_id:149725)和[平均曲率](@entry_id:162147)等核心[不变量](@entry_id:148850)。第二章“应用与[交叉](@entry_id:147634)学科联系”将展示该算子的强大威力，从刻画局部几何形状到解决物理学中的[极小曲面](@entry_id:157732)问题，再到分析计算机图形学中的[曲面](@entry_id:267450)演化。最后，在第三章“动手实践”中，我们将通过计算球面、圆柱面等经典实例的温加滕映射，将抽象的理论转化为具体的计算和几何直觉。

## 原理和机制

在前一章中，我们介绍了研究嵌入[欧氏空间](@entry_id:138052)中[曲面](@entry_id:267450)的基本工具。现在，我们将深入探讨连接[曲面](@entry_id:267450)内在几何与外在几何的核心算子——**Weingarten 映射**（或称**形状算子**）。这个算子精确地量化了[曲面](@entry_id:267450)在周围空间中的弯曲方式，其谱属性（[特征值](@entry_id:154894)和[特征向量](@entry_id:151813)）定义了[曲面](@entry_id:267450)的主曲率和[主方向](@entry_id:276187)，从而引出了高斯曲率和平均曲率这两个中心概念。本章将系统地阐述 Weingarten 映射的定义、基本性质、几何解释，及其在坐标和[活动标架](@entry_id:175562)下的表示。最终，我们将展示它如何作为[高斯-科达齐方程](@entry_id:159376)（Gauss-Codazzi equations）这一[曲面论基本定理](@entry_id:267703)的核心组成部分。

### Weingarten 映射的定义

从几何直观上看，一个[曲面](@entry_id:267450)在空间中的弯曲程度可以通过其[法向量](@entry_id:264185)的变化率来衡量。例如，一个平面，其[法向量](@entry_id:264185)处处恒定，因此变化率为零。而对于一个球面，当你沿着球面移动时，[法向量](@entry_id:264185)会持续“转向”。Weingarten 映射正是对这一思想的数学精确化。

#### 形式化定义

令 $M \subset \mathbb{R}^3$ 是一个光滑的定向[曲面](@entry_id:267450)，其上有光滑的[单位法向量](@entry_id:178851)场 $n: M \to \mathbb{S}^2$。对于[曲面](@entry_id:267450)上任意一点 $p \in M$ 和一个切向量 $v \in T_p M$，我们可以考察[法向量场](@entry_id:268853) $n$ 沿着由 $v$ 定义的方向的变化率。这由协变导数 $\nabla_v n$ 给出，其中 $\nabla$ 是 $\mathbb{R}^3$ 中的标准 Levi-Civita 联络（即通常的方向导数）。

**Weingarten 映射**（或**形状算子**）$S_p: T_p M \to T_p M$ 是一个线性算子，定义为：
$$
S_p(v) := -\nabla_v n
$$
其中负号是一个重要的惯例，它使得对于标[准球](@entry_id:169696)面（以向外的法向量定向），其[主曲率](@entry_id:270598)为正。

要使这个定义有意义，我们必须证明 $S_p$ 确实是一个从切空间到自身的、定义良好的[线性算子](@entry_id:149003) [@problem_id:3004751]。

1.  **$S_p$ 的像空间是[切空间](@entry_id:199137) $T_p M$**：由于 $n$ 是一个[单位法向量](@entry_id:178851)场，我们有 $\langle n, n \rangle = 1$ 在 $M$ 上恒成立。沿着任意一个由切向量 $v \in T_p M$ 确定的方向对这个等式求导，我们得到：
    $$
    d_v \langle n, n \rangle = 2 \langle \nabla_v n, n(p) \rangle = 0
    $$
    这表明向量 $\nabla_v n$ 与法向量 $n(p)$ 正交。在三维空间中，与法向量正交的向量必然位于切空间 $T_p M$ 中。因此，$S_p(v) = -\nabla_v n$ 是 $T_p M$ 中的一个向量。

2.  **$S_p$ 的良定义性（Well-definedness）**：定义中的 $\nabla_v n$ 通常需要将点 $p$ 处的向量 $v$ 延拓为一个光滑的[切向量](@entry_id:265494)场 $X$ 来计算 $\nabla_X n |_p$。我们必须证明其结果不依赖于延拓方式。设 $\gamma(t)$ 是 $M$ 上的一条光滑曲线，满足 $\gamma(0) = p$ 和 $\gamma'(0) = v$。那么，根据协变导数的定义，$\nabla_v n$ 可以通过对复合映射 $n(\gamma(t))$ 求导来计算：
    $$
    \nabla_v n = \frac{d}{dt}\bigg|_{t=0} n(\gamma(t))
    $$
    这个表达式只依赖于曲线在 $t=0$ 处的速度向量 $v$，而与 $v$ 如何延拓成一个向量场无关。因此，$S_p(v)$ 的定义是明确的，只依赖于点 $p$ 和向量 $v$。

3.  **$S_p$ 的线性性**：对于任意 $v, w \in T_p M$ 和标量 $a, b \in \mathbb{R}$，$\nabla$ 算子在其下标参数上是线性的。因此：
    $$
    S_p(av + bw) = -\nabla_{av+bw} n = -(a\nabla_v n + b\nabla_w n) = aS_p(v) + bS_p(w)
    $$
    这证明了 $S_p$ 是一个线性算子。

综上所述，$S_p$ 是一个从 $T_p M$ 到自身的[线性变换](@entry_id:149133)，它内在地捕捉了[曲面](@entry_id:267450)在点 $p$ 的弯曲信息。

### 与[第二基本形式](@entry_id:161454)的对偶关系

虽然 Weingarten 映射是一个算子，但它与一个称为**第二基本形式**的[双线性形式](@entry_id:746794)密切相关。这种对偶关系是[曲面](@entry_id:267450)外在几何的核心。

#### 第二基本形式

直观上，当你在[曲面](@entry_id:267450)上沿着一条曲线运动时，你的加速度向量通常会有一个指向[曲面](@entry_id:267450)外部或内部的分量。这个法向分量衡量了曲线在空间中的弯曲程度如何不被[曲面](@entry_id:267450)所“容纳”。第二基本形式就是对这一现象的量化。

设 $M$ 是一个浸入[黎曼流形](@entry_id:261160) $(N, \bar{g})$ 的[曲面](@entry_id:267450)，$\bar{\nabla}$ 是 $N$ 上的 Levi-Civita 联络，$n$ 是 $M$ 上的[单位法向量](@entry_id:178851)场。对于 $M$ 上的任意[切向量](@entry_id:265494)场 $X, Y$，**第二基本形式** $II$ 定义为：
$$
II(X, Y) := \langle \bar{\nabla}_X Y, n \rangle
$$
这里 $\bar{\nabla}_X Y$ 是 $Y$ 沿着 $X$ 的协变导数，它通常既有切向分量又有法向分量。$II(X,Y)$ 正是其法向分量的大小。特别地，如果 $\gamma(t)$ 是一条单位速度曲线，其切向量为 $X=\dot{\gamma}$，那么 $II(X,X) = \langle \bar{\nabla}_X X, n \rangle$ 就等于曲线的[法曲率](@entry_id:270966) $\kappa_n$ [@problem_id:3004748]。

#### 基本关系式与对称性

Weingarten 映射 $S$ 和[第二基本形式](@entry_id:161454) $II$ 通过一个优美的关系式联系在一起。对于任意[切向量](@entry_id:265494)场 $X, Y$，我们有 $\langle Y, n \rangle = 0$。利用 $\bar{\nabla}$ 的[度量兼容性](@entry_id:265910)对此式求导：
$$
0 = X \langle Y, n \rangle = \langle \bar{\nabla}_X Y, n \rangle + \langle Y, \bar{\nabla}_X n \rangle
$$
根据定义，$II(X,Y) = \langle \bar{\nabla}_X Y, n \rangle$ 和 $S(X) = -\bar{\nabla}_X n$。代入上式得到：
$$
0 = II(X,Y) + \langle Y, -S(X) \rangle = II(X,Y) - \langle Y, S(X) \rangle
$$
因此，我们得到了核心的对偶关系 [@problem_id:3004748] [@problem_id:3004776]：
$$
II(X,Y) = \langle S(X), Y \rangle
$$
这个等式表明，在给定诱导度量（[内积](@entry_id:158127)）$\langle \cdot, \cdot \rangle$ 的情况下，Weingarten 映射 $S$ 是第二基本形式 $II$ 所对应的 $(1,1)$-张量。

此外，[第二基本形式](@entry_id:161454)是**对称的**，即 $II(X,Y) = II(Y,X)$。这可以利用 $\bar{\nabla}$ 的无挠性（torsion-free）来证明：
$$
II(X,Y) - II(Y,X) = \langle \bar{\nabla}_X Y, n \rangle - \langle \bar{\nabla}_Y X, n \rangle = \langle \bar{\nabla}_X Y - \bar{\nabla}_Y X, n \rangle = \langle [X,Y], n \rangle
$$
由于 $X, Y$ 是 $M$ 的[切向量](@entry_id:265494)场，它们的李括号 $[X,Y]$ 也是 $M$ 的切向量场，因此与[法向量](@entry_id:264185) $n$ 正交，即 $\langle [X,Y], n \rangle = 0$。故 $II(X,Y) = II(Y,X)$ [@problem_id:3004748]。

第二基本形式的对称性直接导致了 Weingarten 映射的一个关键性质：$S$ 是**自伴的**（或称对称的）。
$$
\langle S(X), Y \rangle = II(X,Y) = II(Y,X) = \langle S(Y), X \rangle = \langle X, S(Y) \rangle
$$
这个自伴性是[谱理论](@entry_id:275351)得以应用的基础，从而引出了一系列重要的[几何不变量](@entry_id:178611)。

### [几何不变量](@entry_id:178611)与定向

由于 $S_p: T_p M \to T_p M$ 是一个在二维[内积空间](@entry_id:271570)上的自伴[线性算子](@entry_id:149003)，根据[谱定理](@entry_id:136620)，它保证存在一组实[特征值](@entry_id:154894)和相应的[正交特征向量](@entry_id:155522)。这些谱数据具有深刻的几何意义。

**[主曲率](@entry_id:270598)与[主方向](@entry_id:276187)**
Weingarten 映射 $S_p$ 的两个实[特征值](@entry_id:154894)，记为 $\kappa_1$ 和 $\kappa_2$，被称为[曲面](@entry_id:267450)在点 $p$ 的**[主曲率](@entry_id:270598)**。它们是该点最大和最小的[法曲率](@entry_id:270966)。对应的[特征向量](@entry_id:151813)定义了两个相互正交的方向，称为**[主方向](@entry_id:276187)**。这些方向指明了[曲面](@entry_id:267450)在局部弯曲得最剧烈和最平缓的方向 [@problem_id:3004776]。

**[高斯曲率](@entry_id:149725)与平均曲率**
从[主曲率](@entry_id:270598)可以构造出两个基本的外在曲率[不变量](@entry_id:148850)：
*   **[高斯曲率](@entry_id:149725) (Gaussian Curvature)** $K$，定义为 $S_p$ 的[行列式](@entry_id:142978)：
    $$
    K(p) = \det(S_p) = \kappa_1 \kappa_2
    $$
*   **[平均曲率](@entry_id:162147) (Mean Curvature)** $H$，定义为 $S_p$ 的迹的一半：
    $$
    H(p) = \frac{1}{2} \operatorname{tr}(S_p) = \frac{1}{2}(\kappa_1 + \kappa_2)
    $$
高斯曲率衡量了[曲面](@entry_id:267450)在一点附近是“碗状”（$K>0$，如球面）、“鞍状”（$K<0$，如[双曲抛物面](@entry_id:275753)）还是“柱状”（$K=0$，如柱面）的弯曲。平均曲率则衡量了[曲面](@entry_id:267450)在局部“鼓起”的平均程度，它在[极小曲面](@entry_id:157732)理论和[几何分析](@entry_id:157700)中扮演着核心角色。

#### 定向的影响

Weingarten 映射的定义依赖于[法向量场](@entry_id:268853) $n$ 的选取。一个定向[曲面](@entry_id:267450)允许两种相反的[法向量场](@entry_id:268853)选择，$n$ 和 $-n$。考察当 $n$ 变为 $\tilde{n} = -n$ 时，相关几何量如何变化是至关重要的 [@problem_id:3004750]。
设 $\tilde{S}$ 是对应于 $\tilde{n}$ 的 Weingarten 映射，则：
$$
\tilde{S}(v) = -\nabla_v \tilde{n} = -\nabla_v(-n) = \nabla_v n = -S(v)
$$
因此，$\tilde{S} = -S$。这意味着：
*   **[第二基本形式](@entry_id:161454)**改变符号：$\tilde{II}(X,Y) = \langle \tilde{S}(X), Y \rangle = \langle -S(X), Y \rangle = -II(X,Y)$。
*   **主曲率**改变符号：$\tilde{\kappa}_i = -\kappa_i$。
*   **平均曲率**改变符号：$\tilde{H} = -\frac{1}{2}(\kappa_1 + \kappa_2) = -H$。
*   **[高斯曲率](@entry_id:149725)**保持不变：$\tilde{K} = (-\kappa_1)(-\kappa_2) = \kappa_1 \kappa_2 = K$。

这一分析揭示了一个深刻的事实：[高斯曲率](@entry_id:149725) $K$ 是一个比 $S$ 或 $H$ 更“内在”的量。虽然我们的定义依赖于外在的法向量，但 $K$ 的值（在二维情况下）不依赖于[法向量](@entry_id:264185)的朝向。[高斯绝妙定理](@entry_id:159067)（Theorema Egregium）将进一步揭示，$K$ 实际上是一个**内蕴**量，完全由[曲面](@entry_id:267450)的[第一基本形式](@entry_id:274022)决定，无需参考其在三维空间中的嵌入方式。

### 坐标表示

为了进行具体计算，我们需要将 Weingarten 映射及其相关量用[局部坐标](@entry_id:181200)表达出来。

#### [矩阵表示](@entry_id:146025)：从 $II$ 到 $S$

设 $\{u^1, u^2\}$ 是 $M$ 上的一个局部坐标系，对应的切基底为 $\{\partial_1, \partial_2\}$。[第一基本形式](@entry_id:274022)的系数矩阵为 $g = (g_{ij})$，其中 $g_{ij} = \langle \partial_i, \partial_j \rangle$。[第二基本形式](@entry_id:161454)的[系数矩阵](@entry_id:151473)为 $h = (h_{ij})$，其中 $h_{ij} = II(\partial_i, \partial_j)$。Weingarten 映射 $S$ 是一个 $(1,1)$-张量，其分量记为 $S^i{}_j$。

关系式 $II(X,Y) = g(SX,Y)$ 在基底上展开为：
$$
h_{ij} = II(\partial_i, \partial_j) = \langle S(\partial_i), \partial_j \rangle = \langle S^k{}_i \partial_k, \partial_j \rangle = S^k{}_i \langle \partial_k, \partial_j \rangle = S^k{}_i g_{kj}
$$
在矩阵形式下，这可以写成 $h = gS^T$ 或者 $h^T = S g^T$。由于 $g$ 和 $h$ 都是对称矩阵，这等价于 $h=Sg$。为了解出算子 $S$ 的矩阵，我们需要左乘 $g$ 的[逆矩阵](@entry_id:140380) $g^{-1}$：
$$
[S] = g^{-1} h
$$
其中 $[S]$ 表示 $S$ 在基底 $\{\partial_i\}$ 下的[矩阵表示](@entry_id:146025)。用张量指标写出来，就是所谓的“[升指标](@entry_id:265340)”操作 [@problem_id:3004776] [@problem_id:3004763]：
$$
S^i{}_j = g^{ik}h_{kj}
$$
这里 $g^{ik}$ 是逆度量张量 $g^{-1}$ 的分量。这明确地显示了从第二基本形式 $h$（一个(0,2)-张量）到 Weingarten 映射 $S$（一个(1,1)-张量）的转换必须通过度量张量 $g$ 来实现。

#### 曲率的坐标公式

利用 $S=g^{-1}h$，我们可以推导出高斯曲率和平均曲率的经典坐标公式 [@problem_id:3004755]。在经典微分几何中，通常使用记号 $E=g_{11}, F=g_{12}, G=g_{22}$ 和 $e=h_{11}, f=h_{12}, g=h_{22}$（注意这里的 $g$ 是[第二基本形式](@entry_id:161454)的系数，不要与度量矩阵混淆）。
$$
g = \begin{pmatrix} E  F \\ F  G \end{pmatrix}, \quad h = \begin{pmatrix} e  f \\ f  g \end{pmatrix}
$$
于是：
$$
K = \det(S) = \det(g^{-1}h) = \det(g^{-1})\det(h) = \frac{\det(h)}{\det(g)} = \frac{eg - f^2}{EG - F^2}
$$
$$
H = \frac{1}{2}\operatorname{tr}(S) = \frac{1}{2}\operatorname{tr}(g^{-1}h) = \frac{1}{2}\operatorname{tr}\left( \frac{1}{EG-F^2}\begin{pmatrix} G  -F \\ -F  E \end{pmatrix} \begin{pmatrix} e  f \\ f  g \end{pmatrix} \right) = \frac{Eg - 2Ff + Ge}{2(EG-F^2)}
$$
这些公式是计算[曲面](@entry_id:267450)曲率的有力工具。

#### 示例：Monge 参数片

考虑由 Monge 参数片给出的[曲面](@entry_id:267450) $x(u,v) = (u, v, f(u,v))$。在原点 $(0,0)$ 处，如果 $f(0,0)=0$ 且 $f_u(0,0)=f_v(0,0)=0$，则[切平面](@entry_id:136914)是 $xy$-平面。此时，[第一基本形式](@entry_id:274022)矩阵在原点是单位阵 $g(0,0) = I$。第二基本形式矩阵的系数恰好是 $f$ 的[二阶偏导数](@entry_id:635213)：$e=f_{uu}, f=f_{uv}, g=f_{vv}$（在原点处）。因此，Weingarten 映射的矩阵为：
$$
[S](0,0) = g(0,0)^{-1}h(0,0) = I \cdot \begin{pmatrix} f_{uu}  f_{uv} \\ f_{uv}  f_{vv} \end{pmatrix} = \operatorname{Hess}(f)
$$
即 $S$ 的矩阵就是 $f$ 的 Hessian 矩阵。高斯曲率就是 Hessian [矩阵的行列式](@entry_id:148198) $K(0,0) = \det(\operatorname{Hess}(f)) = f_{uu}f_{vv} - f_{uv}^2$ [@problem_id:3004774]。例如，对于二次曲面 $z = \frac{1}{2}(au^2 + 2buv + cv^2)$，在原点的高斯曲率为 $K=ac-b^2$。

### [活动标架法](@entry_id:175562)下的 Weingarten 映射

另一种描述 Weingarten 映射的强大工具是嘉当（Cartan）的[活动标架法](@entry_id:175562)。考虑[曲面](@entry_id:267450)上的一个局部正交[标架场](@entry_id:160577) $\{e_1, e_2\}$，并补充[法向量](@entry_id:264185) $e_3=n$ 构成 $\mathbb{R}^3$ 的一个正交[标架场](@entry_id:160577) $\{e_1, e_2, e_3\}$。

这些标架向量的无穷小变化由联络 [1-形式](@entry_id:270392) $\omega_{ij}$ 描述：
$$
de_i = \sum_{j=1}^3 \omega_{ij} e_j, \quad \text{其中 } \omega_{ij} + \omega_{ji} = 0
$$
Weingarten 映射的定义 $S(X) = -\nabla_X e_3$ 在这个框架下可以被重新解释。$\nabla_X e_3$ 正是 $de_3$ 在 $X$ 方向上的值。因此：
$$
S(X) = -(de_3)(X) = -(\omega_{31}(X)e_1 + \omega_{32}(X)e_2 + \omega_{33}(X)e_3)
$$
由于 $\omega_{33}=0$，并且利用反对称性 $\omega_{3j} = -\omega_{j3}$，我们得到：
$$
S(X) = \omega_{13}(X)e_1 + \omega_{23}(X)e_2
$$
这表明 $S$ 确实映到切空间。$S$ 在基底 $\{e_1, e_2\}$ 下的矩阵分量 $S_{ab}$ 可以通过将[基向量](@entry_id:199546)代入上式得到：
$$
S(e_b) = \sum_{a=1}^2 S_{ab} e_a \quad \implies \quad S_{ab} = \omega_{a3}(e_b)
$$
另一方面，通过对 $de_a$ 进行分解，我们发现 $\omega_{a3}$ 正是 $de_a$ 的法向分量。同时，这些[联络形式](@entry_id:263247)与[第二基本形式](@entry_id:161454)的系数 $h_{ab}=II(e_a, e_b)$ 相关，即 $\omega_{a3} = \sum_b h_{ab}\theta^b$，其中 $\theta^b$ 是对偶[余标架](@entry_id:637284)。因此 $h_{ab} = \omega_{a3}(e_b) = S_{ab}$。这说明在正交标架下，Weingarten 映射的矩阵与第二基本形式的矩阵是相同的 [@problem_id:3004745]。

### [可积性](@entry_id:142415)条件：Gauss-Codazzi 方程

一个自然的问题是：任意给定的一对[第一和第二基本形式](@entry_id:192112)（即 $g_{ij}$ 和 $h_{ij}$），是否总能对应一个实际的嵌入[曲面](@entry_id:267450)？答案是否定的。它们必须满足一组称为**[高斯-科达齐方程](@entry_id:159376)（Gauss-Codazzi equations）**的[可积性](@entry_id:142415)条件。这些方程源于对位置向量 $X$ 的三阶[混合偏导数相等](@entry_id:138898)的要求（Clairaut 定理），如 $X_{uuv} = X_{uvu}$。

经过推导，这些相等关系分解为切向分量和法向分量上的两个方程 [@problem_id:3004743] [@problem_id:3004736]。

1.  **[高斯方程](@entry_id:192573) (Gauss Equation)**：它来源于三阶导数切向分量的相等，并给出了[曲面](@entry_id:267450)的内蕴曲率（由[第一基本形式](@entry_id:274022)确定）和[外在曲率](@entry_id:160405)（由第二基本形式确定）之间的关系。对于在欧氏空间 $\mathbb{R}^3$ 中的[曲面](@entry_id:267450)，它有一个简洁的形式：
    $$
    K = \det(S)
    $$
    这正是我们之前定义的 $K$。这个方程的更深层版本（[高斯绝妙定理](@entry_id:159067)）表明左边的 $K$ 完全可以由 $g_{ij}$ 及其导数计算，而右边由 $h_{ij}$ 和 $g_{ij}$ 确定。

2.  **科达齐-迈纳尔迪方程 (Codazzi-Mainardi Equations)**：它来源于三阶导数法向分量的相等，描述了[第二基本形式](@entry_id:161454)的变化规律。在坐标形式下，它们可以写成（以 $\mathcal{C}_1=0, \mathcal{C}_2=0$ 的形式给出）：
    $$
    e_v - f_u = e\Gamma_{12}^1 + f(\Gamma_{12}^2 - \Gamma_{11}^1) - g\Gamma_{11}^2
    $$
    $$
    f_v - g_u = e\Gamma_{22}^1 + f(\Gamma_{22}^2 - \Gamma_{12}^1) - g\Gamma_{12}^2
    $$
    其中 $\Gamma_{ij}^k$ 是由[第一基本形式](@entry_id:274022)确定的 Christoffel 符号。这些方程可以用 Weingarten 映射的[协变导数](@entry_id:152476) $(\nabla_X S)$ 来更紧凑地表达，即 $(\nabla_X S)Y = (\nabla_Y S)X$。

#### 推广到弯曲[环境空间](@entry_id:184743)

当背景空间本身就是一个弯曲的[黎曼流形](@entry_id:261160) $(M^3, g)$ 时，上述方程会包含额外的项，以反映背景空间的曲率。设 $R^M$ 是背景[流形](@entry_id:153038)的黎曼曲率张量，$\bar{K}(T_p\Sigma)$ 是背景[流形](@entry_id:153038)在 $T_p\Sigma$ 平面上的[截面曲率](@entry_id:159738)。

*   **[高斯方程](@entry_id:192573)**变为：
    $$
    K(p) = \det(S_p) + \bar{K}(T_p\Sigma)
    $$
    这表明[曲面](@entry_id:267450)的[内蕴曲率](@entry_id:161701)是其外在弯曲（由 $\det S$ 度量）和背景空间自身弯曲的叠加。

*   **[科达齐方程](@entry_id:635135)**的向量形式变为：
    $$
    (\nabla_X S)Y - (\nabla_Y S)X = -(R^M(X,Y)\nu)^T
    $$
    其中 $(\cdot)^T$ 表示到[切空间](@entry_id:199137)的正交投影。右端项 $R^M(X,Y)\nu$ 捕获了沿 $X, Y$ 构成的无穷小平行四边形移动法向量 $\nu$ 时，由于背景空间弯曲而产生的“不闭合”效应。

[曲面论基本定理](@entry_id:267703)指出，只要[第一和第二基本形式](@entry_id:192112)满足[高斯-科达齐方程](@entry_id:159376)，那么在局部上就存在一个（在[刚性运动](@entry_id:170523)意义下唯一的）[曲面](@entry_id:267450)与之对应。Weingarten 映射作为连接这两个基本形式的桥梁，是理解这一基本定理和整个[曲面](@entry_id:267450)几何的关键。例如，对于 $\mathbb{R}^3$ 中的球面，我们可以直接计算其 $E,F,G,e,f,g$ 和 Christoffel 符号，并验证其确实满足科达齐-迈纳尔迪方程，即 $\mathcal{C}_1=0, \mathcal{C}_2=0$ [@problem_id:3004743]。这为理论的正确性提供了一个坚实的例证。