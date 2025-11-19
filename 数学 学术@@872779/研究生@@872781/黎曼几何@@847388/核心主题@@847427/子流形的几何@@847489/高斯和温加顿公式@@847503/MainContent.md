## 引言
在研究嵌入黎曼流形 $(\bar{M}, \bar{g})$ 中的[子流形](@entry_id:159439) $(M, g)$ 时，一个核心挑战在于如何利用环境空间的结构来理解[子流形](@entry_id:159439)自身的几何特性。当我们在环境空间中对子流形上的[切向量](@entry_id:265494)场进行[微分](@entry_id:158718)时，结果向量通常会包含一个“[逸出](@entry_id:141194)”[切空间](@entry_id:199137)的分量。这个法向分量并非麻烦，而是精确地编码了[子流形](@entry_id:159439)的外在弯曲信息。高斯公式与魏因加滕公式正是为了系统地分析这一现象而发展出的基本工具，它们构成了连接子[流形](@entry_id:153038)“内蕴”几何（如曲率）与“外在”几何（其在空间中的形状）之间的关键桥梁。

本文将系统地引导读者掌握这两个公式及其深远影响。我们将从“原理与机制”出发，阐明如何通过分解[协变导数](@entry_id:152476)来建立高斯与魏因加滕公式，并定义第二基本形式和形状算子等核心概念。随后，在“应用与跨学科联系”中，我们将见证这些公式的威力，不仅用它们推导出[高斯绝妙定理](@entry_id:159067)等基石性结论，还将探索它们在[固体力学](@entry_id:164042)、几何分析等前沿领域的应用。最后，“动手实践”部分将提供具体的计算练习，以巩固理论知识。

现在，让我们开始这场几何探索之旅，首先进入“原理与机制”部分，揭示这些公式的构造基础。

## 原理与机制

在研究嵌入黎曼流形 $(M, g)$ 的几何性质时，一个核心的策略是利用其所在的环境[流形](@entry_id:153038) $(\bar{M}, \bar{g})$ 的结构。环境[流形](@entry_id:153038)通常具有更简单的几何性质（例如，[欧几里得空间](@entry_id:138052)是平坦的），其列维-奇维塔联络 $\bar{\nabla}$ 也更易于处理。然而，一个主要的挑战在于，当我们将 $\bar{\nabla}$ 应用于 $M$ 上的切向量场时，其结果通常不会停留在 $M$ 的切丛 $TM$ 中。向量的这种“[逸出](@entry_id:141194)”恰恰编码了 $M$ 如何弯曲地嵌入在 $\bar{M}$ 中。本章的目的是系统地阐述分解环境联络的基本工具——高斯公式与魏因加滕公式，并展示它们如何成为[连接子](@entry_id:177005)[流形](@entry_id:153038)内外蕴几何的桥梁。

### 协变导数的基本分解

考虑一个[切向量](@entry_id:265494)场 $X, Y \in \Gamma(TM)$。在 $M$ 上的任意点 $p$，$\bar{\nabla}_X Y$ 是[环境空间](@entry_id:184743) $T_p\bar{M}$ 中的一个向量。由于 $T_p\bar{M}$ 可以[正交分解](@entry_id:148020)为[切空间](@entry_id:199137) $T_pM$ 和法空间 $N_pM$ 的[直和](@entry_id:156782)，即 $T_p\bar{M} = T_pM \oplus N_pM$，我们可以将向量 $\bar{\nabla}_X Y$ 唯一地分解为其切向分量和法向分量。这个简单的分解思想引出了[子流形理论](@entry_id:190701)中两个最基本的对象。

#### 高斯公式：对[切向量](@entry_id:265494)场的[微分](@entry_id:158718)

对于 $M$ 上的任意切向量场 $X, Y \in \Gamma(TM)$，我们将它们在环境[流形](@entry_id:153038)中的[协变导数](@entry_id:152476) $\bar{\nabla}_X Y$ 分解如下：
$$
\bar{\nabla}_X Y = (\bar{\nabla}_X Y)^\top + (\bar{\nabla}_X Y)^\perp
$$
其中 $(\bar{\nabla}_X Y)^\top$ 表示在切丛 $TM$ 上的正交投影，而 $(\bar{\nabla}_X Y)^\perp$ 表示在[法丛](@entry_id:272447) $NM$ 上的正交投影。

这个分解引出了两个核心定义：

1.  **[诱导联络](@entry_id:635081) (Induced Connection)**：我们将切向分量定义为 $M$ 上的一个新联络 $\nabla$：
    $$
    \nabla_X Y := (\bar{\nabla}_X Y)^\top
    $$

2.  **[第二基本形式](@entry_id:161454) (Second Fundamental Form)**：我们将法向分量定义为一个映射 $B$：
    $$
    B(X,Y) := (\bar{\nabla}_X Y)^\perp
    $$

将这两个定义代入分解式，我们便得到了**高斯公式 (Gauss formula)**：
$$
\bar{\nabla}_X Y = \nabla_X Y + B(X,Y)
$$

一个自然而深刻的问题是：这个通过投影定义的联络 $\nabla$ 究竟是什么？答案是，它正是[子流形](@entry_id:159439) $(M, g)$ 上的**列维-奇维塔联络**。我们可以通过验证它满足列维-奇维塔联络的唯一性条件——无挠性和[度量兼容性](@entry_id:265910)——来证明这一点 [@problem_id:2997189] [@problem_id:2997218]。

**无挠性**：联络 $\nabla$ 的[挠率张量](@entry_id:204137)定义为 $T(X,Y) = \nabla_X Y - \nabla_Y X - [X,Y]$。利用 $\nabla$ 的定义和 $\bar{\nabla}$ 的无挠性 ($\bar{\nabla}_X Y - \bar{\nabla}_Y X = [X,Y]$)，我们有：
$$
\nabla_X Y - \nabla_Y X = (\bar{\nabla}_X Y)^\top - (\bar{\nabla}_Y X)^\top = (\bar{\nabla}_X Y - \bar{\nabla}_Y X)^\top = ([X,Y])^\top
$$
由于 $X$ 和 $Y$ 是 $M$ 的切向量场，它们的[李括号](@entry_id:636461) $[X,Y]$ 仍然是 $M$ 的切向量场。因此，$([X,Y])^\top = [X,Y]$。于是，$T(X,Y) = [X,Y] - [X,Y] = 0$，证明了 $\nabla$ 是[无挠的](@entry_id:161664)。

**[度量兼容性](@entry_id:265910)**：我们需要证明 $Z(g(X,Y)) = g(\nabla_Z X, Y) + g(X, \nabla_Z Y)$。由于 $g$ 是诱导度量，我们有 $g(X,Y) = \bar{g}(X,Y)$。利用 $\bar{\nabla}$ 的[度量兼容性](@entry_id:265910)：
$$
Z(g(X,Y)) = Z(\bar{g}(X,Y)) = \bar{g}(\bar{\nabla}_Z X, Y) + \bar{g}(X, \bar{\nabla}_Z Y)
$$
应用高斯公式 $\bar{\nabla}_V W = \nabla_V W + B(V,W)$：
$$
Z(g(X,Y)) = \bar{g}(\nabla_Z X + B(Z,X), Y) + \bar{g}(X, \nabla_Z Y + B(Z,Y))
$$
由于 $\nabla_V W$ 是[切向量](@entry_id:265494)，而 $B(V,W)$ 是法向量，根据[正交分解](@entry_id:148020)，切向量与法向量的[内积](@entry_id:158127)为零。因此，$\bar{g}(B(Z,X), Y) = 0$ 且 $\bar{g}(X, B(Z,Y)) = 0$。上式简化为：
$$
Z(g(X,Y)) = \bar{g}(\nabla_Z X, Y) + \bar{g}(X, \nabla_Z Y) = g(\nabla_Z X, Y) + g(X, \nabla_Z Y)
$$
这证明了 $\nabla$ 与度量 $g$ 兼容。根据[黎曼几何基本定理](@entry_id:189185)，$\nabla$ 确实是 $(M,g)$ 上唯一的[列维-奇维塔联络](@entry_id:161107)。

现在我们来考察**[第二基本形式](@entry_id:161454)** $B(X,Y)$ 的性质。它是一个从 $\Gamma(TM) \times \Gamma(TM)$ 到 $\Gamma(NM)$ 的映射。利用与证明 $\nabla$ 无挠性时相同的逻辑，我们可以发现 $B$ 是一个对称的张量 [@problem_id:2997223]。
$$
B(X,Y) - B(Y,X) = (\bar{\nabla}_X Y)^\perp - (\bar{\nabla}_Y X)^\perp = (\bar{\nabla}_X Y - \bar{\nabla}_Y X)^\perp = ([X,Y])^\perp
$$
因为 $[X,Y]$ 是 $M$ 的[切向量](@entry_id:265494)场，其法向分量为零。因此，$B(X,Y) = B(Y,X)$。此外，可以证明 $B$ 对于 $C^\infty(M)$ 函数是[双线性](@entry_id:146819)的，这意味着它是一个**张量**，其在一点 $p$ 的取值 $B_p(X_p, Y_p)$ 仅依赖于该点的向量 $X_p$ 和 $Y_p$ [@problem_id:2997223]。这个[法向量](@entry_id:264185)值的对称张量 $B$ 描述了 $M$ 的**外在弯曲**。如果 $B \equiv 0$，则高斯公式变为 $\bar{\nabla}_X Y = \nabla_X Y$，这意味着 $M$ 的[测地线](@entry_id:269969)与 $\bar{M}$ 的[测地线](@entry_id:269969)一致（在一定意义下），这样的[子流形](@entry_id:159439)称为**[全测地子流形](@entry_id:637049)**。

#### 魏因加滕公式：对[法向量场](@entry_id:268853)的[微分](@entry_id:158718)

我们已经分析了对[切向量](@entry_id:265494)场求导的情形，现在转向另一个基本问题：当沿着 $M$ 上的[切向量](@entry_id:265494)场 $X$ 对一个[法向量场](@entry_id:268853) $\xi \in \Gamma(NM)$ 求导时，会发生什么？同样，向量 $\bar{\nabla}_X \xi$ 也可以分解为切向和法向分量：
$$
\bar{\nabla}_X \xi = (\bar{\nabla}_X \xi)^\top + (\bar{\nabla}_X \xi)^\perp
$$
这个分解同样定义了两个重要的几何对象：

1.  **[形状算子](@entry_id:264703) (Shape Operator)** 或称 **魏因加滕映射 (Weingarten map)**：这是一个与[法向量](@entry_id:264185) $\xi$ 相关的映射 $S_\xi: \Gamma(TM) \to \Gamma(TM)$，定义为：
    $$
    S_\xi(X) := -(\bar{\nabla}_X \xi)^\top
    $$
    这里的负号是一个重要的惯例，它将使形状算子成为一个[自伴算子](@entry_id:152188)。

2.  **法联络 (Normal Connection)**：这是一个在法[丛上的联络](@entry_id:191877) $\nabla^\perp$，定义为：
    $$
    \nabla^\perp_X \xi := (\bar{\nabla}_X \xi)^\perp
    $$

将这些定义代入，我们得到**魏因加滕公式 (Weingarten formula)** [@problem_id:2997225]：
$$
\bar{\nabla}_X \xi = -S_\xi(X) + \nabla^\perp_X \xi
$$

形状算子 $S_\xi$ 和[第二基本形式](@entry_id:161454) $B$ 之间存在着深刻的联系。考虑任意[切向量](@entry_id:265494)场 $X, Y$ 和[法向量场](@entry_id:268853) $\xi$。由于 $Y$ 和 $\xi$ 正交，我们有 $\bar{g}(Y, \xi) = 0$。利用 $\bar{\nabla}$ 的[度量兼容性](@entry_id:265910)对此求导：
$$
0 = X(\bar{g}(Y, \xi)) = \bar{g}(\bar{\nabla}_X Y, \xi) + \bar{g}(Y, \bar{\nabla}_X \xi)
$$
移项并代入高斯公式和魏因加滕公式：
$$
\bar{g}(\nabla_X Y + B(X,Y), \xi) = -\bar{g}(Y, -S_\xi(X) + \nabla^\perp_X \xi)
$$
利用切、法[向量的正交性](@entry_id:274719)，上式简化为：
$$
\bar{g}(B(X,Y), \xi) = \bar{g}(Y, S_\xi(X))
$$
由于 $S_\xi(X)$ 和 $Y$ 都是[切向量](@entry_id:265494)，我们可以用内蕴度量 $g$ 代替 $\bar{g}$：
$$
\bar{g}(B(X,Y), \xi) = g(S_\xi(X), Y)
$$
这个关键关系式表明，给定一个[法向量](@entry_id:264185) $\xi$，形状算子 $S_\xi$ 是第二基本形式 $B$ 在 $\xi$ 方向上的“[标量化](@entry_id:634761)”版本的[伴随算子](@entry_id:140236)。由于 $B(X,Y)$ 对 $X, Y$ 是对称的，这也立即推导出 $S_\xi$ 是一个关于度量 $g$ 的**[自伴算子](@entry_id:152188)**，即 $g(S_\xi(X), Y) = g(X, S_\xi(Y))$ [@problem_id:2997223]。$S_\xi$ 的[特征值](@entry_id:154894)被称为 $M$ 在 $\xi$ 方向上的**主曲率**，相应的[特征向量](@entry_id:151813)被称为**[主方向](@entry_id:276187)**。

法联络 $\nabla^\perp$ 也具有良好的性质。可以证明，它是一个与[法丛](@entry_id:272447)上的度量（由 $\bar{g}$ 诱导）兼容的联络 [@problem_id:2997225]。然而，与列维-奇维塔联络不同，它通常不是[无挠的](@entry_id:161664)。

对于**[余维](@entry_id:273141)为1**的[超曲面](@entry_id:159491)，情况大大简化。此时[法丛](@entry_id:272447)是一维的，可以由一个[单位法向量](@entry_id:178851)场 $\nu$ 张成。因为 $\bar{g}(\nu, \nu) = 1$，对其求导可得 $\bar{g}(\bar{\nabla}_X \nu, \nu) = 0$。这意味着 $\bar{\nabla}_X \nu$ 总是与 $\nu$ 正交，因此它是一个纯切向量。根据法联络的定义 $\nabla^\perp_X \nu = (\bar{\nabla}_X \nu)^\perp$，我们立即得到 $\nabla^\perp_X \nu = 0$ [@problem_id:2997203]。这意味着对于[超曲面](@entry_id:159491)，法联络总是平凡的（只要[单位法向量](@entry_id:178851)场是全局定义的），魏因加滕公式简化为：
$$
\bar{\nabla}_X \nu = -S_\nu(X)
$$

### 坐标表示与经典公式

虽然上述定义在坐标无关的抽象形式下最为清晰，但在具体计算中，我们通常需要借助[局部坐标](@entry_id:181200)。对于嵌入在 $\mathbb{R}^3$ 中的[曲面](@entry_id:267450) $M^2$，这些公式与经典[曲面](@entry_id:267450)理论中的一、二基本形式系数 $(E, F, G)$ 和 $(e, f, g)$ 紧密相连。

假设[曲面](@entry_id:267450)由一个参数化映射 $r(u,v)$ 给出。切空间由[基向量](@entry_id:199546) $\{r_u, r_v\}$ 张成。

**[第一基本形式](@entry_id:274022)**的系数定义为 $E = \langle r_u, r_u \rangle$, $F = \langle r_u, r_v \rangle$, $G = \langle r_v, r_v \rangle$。它们构成了度量张量 $g$ 在该基底下的矩阵 $I = \begin{pmatrix} E  F \\ F  G \end{pmatrix}$。

**[第二基本形式](@entry_id:161454)**的系数定义为 $e = \langle r_{uu}, n \rangle$, $f = \langle r_{uv}, n \rangle$, $g = \langle r_{vv}, n \rangle$，其中 $n$ 是[单位法向量](@entry_id:178851)。在欧几里得空间中，$\bar{\nabla}_{r_u} r_v = \frac{\partial}{\partial u} r_v = r_{uv}$。因此，标量第二基本形式 $h(X,Y) = \langle B(X,Y), n \rangle$ 在基底 $\{r_u, r_v\}$ 下的矩阵就是 $II = \begin{pmatrix} e  f \\ f  g \end{pmatrix}$。

例如，对于由 $r(u,v) = (u, v, u^2 + v^3)$ [参数化](@entry_id:272587)的[曲面](@entry_id:267450)，在点 $p=r(0,0)$，我们有 $r_u=(1,0,0)$，$n=(0,0,1)$。环境导数 $\bar{\nabla}_{\partial_u} \partial_u = r_{uu} = (0,0,2)$。这个向量本身就是法向的，所以 $B(\partial_u, \partial_u) = (0,0,2)$，而 $\nabla_{\partial_u}\partial_u = 0$。我们计算 $\langle B(\partial_u, \partial_u), n \rangle = \langle (0,0,2), (0,0,1) \rangle = 2$，这正是系数 $e$ 在该点的值 [@problem_id:2997189]。

在更高[余维](@entry_id:273141)的情况下，我们需要一个[法丛](@entry_id:272447)的局部[标准正交标架](@entry_id:189702) $\{e_\alpha\}_{\alpha=1}^k$。向量值的[第二基本形式](@entry_id:161454) $B(X,Y)$ 可以在这个标架下分解：
$$
B(X,Y) = \sum_{\alpha=1}^k \bar{g}(B(X,Y), e_\alpha) e_\alpha
$$
每一项的系数 $h^\alpha(X,Y) := \bar{g}(B(X,Y), e_\alpha)$ 都定义了一个**标量第二基本形式**。因此，向量值的 $B$ 可以看作是一组标量[第二基本形式](@entry_id:161454)的集合 $B = \sum_{\alpha=1}^k h^\alpha \otimes e_\alpha$ [@problem_id:2997217]。当法标架发生旋转时，这些标量形式 $h^\alpha$ 会相应地线性组合。

魏因加滕公式在坐标下也有具体的体现。对于超曲面，魏因加滕方程 $-n_u = a r_u + b r_v$ 和 $-n_v = c r_u + d r_v$ 给出了[法向量](@entry_id:264185)导数在切基底下的分量。通过一系列[内积](@entry_id:158127)运算，可以证明形状算子（魏因加滕映射） $S$ 在基底 $\{r_u, r_v\}$ 下的矩阵 $L = \begin{pmatrix} a  c \\ b  d \end{pmatrix}$（注意转置）满足关系 $I \cdot L = II$，即 $L = I^{-1} II$ [@problem_id:2997213]。这提供了一个从一、二基本形式系数直接计算[形状算子](@entry_id:264703)矩阵的有效方法。例如，对于[抛物面](@entry_id:264713) $X(u,v)=(u, v, \frac{1}{2}(u^2+v^2))$，我们可以计算出 $E,F,G$ 和 $e,f,g$，然后代入公式 $L = I^{-1} II$ 得到形状算子的具体表达式，从而得到[法向量](@entry_id:264185)的导数 $n_u, n_v$ [@problem_id:2997194]。

### [子流形理论](@entry_id:190701)的基本方程

[高斯和](@entry_id:196588)魏因加滕公式的真正威力在于它们能够推导出联系子[流形曲率](@entry_id:187680)、环境曲率和[第二基本形式](@entry_id:161454)的一组基本方程。这些方程，即[高斯方程](@entry_id:192573)、科达齐-迈纳尔迪方程和里奇方程，构成了[子流形几何](@entry_id:189265)的基石。

#### [高斯方程](@entry_id:192573)：[内蕴曲率](@entry_id:161701)

**[高斯方程](@entry_id:192573) (Gauss equation)** 揭示了子流形的[内蕴曲率](@entry_id:161701)（[黎曼曲率张量](@entry_id:160189) $R$）是如何由环境[流形](@entry_id:153038)的曲率 $\bar{R}$ 和[子流形](@entry_id:159439)自身的外在弯曲（[第二基本形式](@entry_id:161454) $B$）共同决定的。其推导始于对环境曲率张量 $\bar{R}(X,Y)Z = \bar{\nabla}_X \bar{\nabla}_Y Z - \bar{\nabla}_Y \bar{\nabla}_X Z - \bar{\nabla}_{[X,Y]} Z$ 的考察。通过反复应用[高斯和](@entry_id:196588)魏因加滕公式展开各项，并分离出最终结果的切向分量，我们得到一个只涉及 $M$ 上张量的方程。对于任意[切向量](@entry_id:265494) $X,Y,Z,W$，有：
$$
\bar{g}(R(X,Y)Z, W) = \bar{g}(\bar{R}(X,Y)Z, W) + \bar{g}(B(X,W), B(Y,Z)) - \bar{g}(B(X,Z), B(Y,W))
$$
在坐标下，这个方程可以更简洁地写作 $R_{ijkl} = \bar{R}_{ijkl} + h_{ik}h_{jl} - h_{il}h_{jk}$（对于[超曲面](@entry_id:159491)）。

这个方程最著名的应用是当环境空间为[常截面曲率](@entry_id:272200) $\kappa$ 的[空间形式](@entry_id:186145)时。对于一个二维[曲面](@entry_id:267450)，[高斯方程](@entry_id:192573)可以简化为关于高斯曲率 $K$ 的优美公式 [@problem_id:2997216]：
$$
K = \kappa + \det(S)
$$
其中 $\det(S)$ 是形状算子的[行列式](@entry_id:142978)（即[主曲率](@entry_id:270598)的乘积）。

特别地，当[曲面](@entry_id:267450)位于[欧几里得空间](@entry_id:138052) $\mathbb{R}^3$ 中时，环境曲率 $\kappa=0$。此时[高斯曲率](@entry_id:149725)完全由形状算子决定：$K = \det(S)$。利用 $L = I^{-1} II$，我们有 $\det(S) = \det(L) = \det(I^{-1}II) = \frac{\det(II)}{\det(I)}$。这便得到了高斯著名的 **Theorema Egregium** 的一个表达式 [@problem_id:2997238]：
$$
K = \frac{eg-f^2}{EG-F^2}
$$
这个公式表明，尽管 $e,f,g$ 的定义依赖于[曲面](@entry_id:267450)在空间中的嵌入方式（法向量），但它们的特定组合 $(eg-f^2)/(EG-F^2)$ 竟然只依赖于[第一基本形式](@entry_id:274022)及其导数，因此是一个内蕴量。

我们可以通过两个经典例子来直观理解 $K = \det(S)$：
1.  **球面**：半径为 $R$ 的球面，其向外的[形状算子](@entry_id:264703)为 $S = -\frac{1}{R} \mathrm{Id}$。任意方向的主曲率都是 $-\frac{1}{R}$。因此，$\det(S) = (-\frac{1}{R})(-\frac{1}{R}) = \frac{1}{R^2}$，所以其高斯曲率为 $K = \frac{1}{R^2}$。
2.  **圆柱面**：半径为 $R$ 的圆柱面。沿轴线方向是直线，该方向的主曲率为 $0$。沿圆周方向，其弯曲类似于半径为 $R$ 的圆，[主曲率](@entry_id:270598)为 $-\frac{1}{R}$（取决于法向量指向）。因此，$\det(S) = 0 \cdot (-\frac{1}{R}) = 0$，所以圆柱面的高斯曲率为 $K=0$。这与圆柱面可以无拉伸地展开成一个平面（平坦的）的直观经验相符 [@problem_id:2997216]。

#### 科达齐-迈纳尔迪方程与里奇方程

**科达齐-迈纳尔迪方程 (Codazzi-Mainardi equation)** 来自于对环境曲率张量 $\bar{R}(X,Y)Z$ 表达式的法向分量的分析。它给出了第二基本形式的[协变导数](@entry_id:152476)必须满足的对称性条件，本质上是[第二基本形式](@entry_id:161454)与[诱导联络](@entry_id:635081)之间的[可积性](@entry_id:142415)条件。

**里奇方程 (Ricci equation)** 则描述了[法丛](@entry_id:272447)自身的曲率。法联络 $\nabla^\perp$ 也有一个[曲率张量](@entry_id:181383) $R^\perp$，定义为 $R^\perp(X,Y)\xi = \nabla^\perp_X \nabla^\perp_Y \xi - \nabla^\perp_Y \nabla^\perp_X \xi - \nabla^\perp_{[X,Y]} \xi$。通过与推导[高斯方程](@entry_id:192573)类似的方法，但这次分离出法向分量，可以得到**里奇方程** [@problem_id:2997187]：
$$
\bar{g}(R^\perp(X,Y)\xi, \eta) = \bar{g}(\bar{R}(X,Y)\xi, \eta) + g([S_\xi, S_\eta]X, Y)
$$
其中 $[S_\xi, S_\eta] = S_\xi S_\eta - S_\eta S_\xi$ 是形状[算子的交换子](@entry_id:261812)。这个方程表明，[法丛](@entry_id:272447)的曲率由两部分贡献：一部分来自环境空间的曲率在[法丛](@entry_id:272447)上的投影，另一部分则完全由形状算子[代数结构](@entry_id:137052)的非交换性决定。如果所有[形状算子](@entry_id:264703)相互交换，且环境空间是平坦的，则[法丛](@entry_id:272447)也是平坦的。

总之，[高斯和](@entry_id:196588)魏因加滕公式不仅提供了在子流形上进行微积分的基本工具，而且还催生了联系内外蕴几何的三个基本方程，构成了现代黎曼[子流形几何](@entry_id:189265)的理论核心。