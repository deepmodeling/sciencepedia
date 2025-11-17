## 引言
在黎曼几何的宏伟画卷中，[子流形理论](@entry_id:190701)是探索几何对象如何嵌入更高维空间的核心篇章。而在这其中，形状算子（Shape Operator）扮演着无可替代的角色。它是一个精妙的数学工具，如同一座桥梁，牢固地连接着[子流形](@entry_id:159439)的“内蕴”几何（仅依赖于[子流形](@entry_id:159439)自身度量的性质，如[测地线](@entry_id:269969)和内蕴曲率）与“外蕴”几何（依赖于其在背景空间中嵌入方式的性质，如弯曲程度）。尽管其定义抽象，但[形状算子](@entry_id:264703)为我们量化和理解“弯曲”这一直观概念提供了最精确的语言。本文旨在系统性地揭开形状算子的神秘面纱，引领读者从基本定义走向深刻应用，填补从抽象理论到具体计算与几何直觉之间的鸿沟。

为了实现这一目标，我们将分三个章节展开探索之旅。首先，在“原理与机制”一章中，我们将从最简单的[超曲面](@entry_id:159491)出发，严谨地构建[形状算子](@entry_id:264703)的定义，阐明其与第二基本形式的深刻联系，并揭示其如何决定[主曲率](@entry_id:270598)等关键几何量。我们还将探讨其在高[余维](@entry_id:273141)情形下的推广，并展示其在子流形基本[方程组](@entry_id:193238)中的核心地位。接下来，“应用与跨学科联系”一章将展示[形状算子](@entry_id:264703)的强大威力，通过分析经典[曲面](@entry_id:267450)、[极小曲面](@entry_id:157732)以及它在[几何分析](@entry_id:157700)和广义相对论等前沿领域的应用，使其从抽象理论走向生动的几何实例。最后，“动手实践”部分将提供精选的计算问题，帮助读者将理论知识转化为解决实际问题的能力。

现在，让我们启程，首先深入其根本，探索形状算子的核心原理与机制。

## 原理与机制

本章旨在深入探讨[形状算子](@entry_id:264703)（shape operator）的根本原理与核心机制。作为从属于黎曼几何中[子流形理论](@entry_id:190701)的一个关键概念，[形状算子](@entry_id:264703)是连接子[流形](@entry_id:153038)的内蕴几何（intrinsic geometry）与外蕴几何（extrinsic geometry）的中心桥梁。我们将从最直观的[超曲面](@entry_id:159491)情形出发，逐步建立形状算子的严谨定义，揭示其与第二基本形式的深刻联系，并阐明其在决定[主曲率](@entry_id:270598)、[法曲率](@entry_id:270966)等几何量中的核心作用。随后，我们会将此概念推广至任意[余维数](@entry_id:273141)的[子流形](@entry_id:159439)，并展示如何通过坐标或[活动标架法](@entry_id:175562)进行具体计算。最后，我们将把形状算子置于高斯-科达齐-里奇（Gauss-Codazzi-Ricci）[方程组](@entry_id:193238)这一宏大框架之下，揭示其作为外蕴曲率[核心张量](@entry_id:747891)的根本地位。

### [超曲面](@entry_id:159491)的形状算子

我们从最简单且最直观的情形开始：一个 $n$ 维可定向超曲面 $M^n$ 浸入一个 $(n+1)$ 维的黎曼流形 $(\bar{M}^{n+1}, \bar{g})$ 中。由于 $M$ 是可定向的，我们可以选取一个光滑的、全局定义的[单位法向量](@entry_id:178851)场 $\nu$，它在 $M$ 的每一点 $p$ 都与切空间 $T_pM$ 正交，即 $\bar{g}(\nu, X) = 0$ 对所有 $X \in T_pM$ 成立，且其长度为1，即 $\bar{g}(\nu, \nu) = 1$。

[形状算子](@entry_id:264703)，又称温加滕映射（Weingarten map），描述了当我们沿着[超曲面](@entry_id:159491)上的一个切方向移动时，[法向量场](@entry_id:268853) $\nu$ 是如何变化的。令 $\bar{\nabla}$ 为背景[流形](@entry_id:153038) $\bar{M}$ 上的[列维-奇维塔联络](@entry_id:161107)。对于 $M$ 上的任意切向量场 $X$，我们可以计算 $\nu$ 沿着 $X$ 的协变导数 $\bar{\nabla}_X \nu$。一个关键的观察是，这个导数向量实际上是 $M$ 的一个切向量。为了证明这一点，我们对恒等式 $\bar{g}(\nu, \nu) = 1$ 求导：
$$
0 = X(\bar{g}(\nu, \nu)) = \bar{g}(\bar{\nabla}_X \nu, \nu) + \bar{g}(\nu, \bar{\nabla}_X \nu) = 2\bar{g}(\bar{\nabla}_X \nu, \nu)
$$
这表明 $\bar{\nabla}_X \nu$ 与 $\nu$ 正交。在一个[超曲面](@entry_id:159491)中，与法向量 $\nu$ 正交的向量必然位于[切空间](@entry_id:199137) $T_pM$ 内。因此，$\bar{\nabla}_X \nu$ 是一个[切向量](@entry_id:265494)场。

这个观察使我们能够定义一个从[切丛](@entry_id:161294) $TM$ 到自身的[线性映射](@entry_id:185132)。**形状算子** $S: \Gamma(TM) \to \Gamma(TM)$ 通常按以下约定定义：
$$
S(X) = -\bar{\nabla}_X \nu
$$
这个算子在点 $p$ 的取值 $S_p: T_pM \to T_pM$ 捕捉了在 $p$ 点沿不同切方向 $X$ [法向量](@entry_id:264185)的变化率的“切向部分”（在此超曲面情况下，即为其全部）。负号是一个惯例，但其选择会影响其他几何量的符号。

**符号约定与定向**

在[微分几何](@entry_id:145818)文献中，对于[形状算子](@entry_id:264703)的定义存在两种主流约定。除了我们采纳的 $S^-(X) = -\bar{\nabla}_X \nu$ 之外，另一个常见的定义是 $S^+(X) = \bar{\nabla}_X \nu$。显然，这两个算子互为[相反数](@entry_id:151709)，$S^+ = -S^-$。这个符号上的差异会系统性地影响一系列外蕴几何量的定义。例如，平均曲率 $H = \frac{1}{n} \mathrm{tr}(S)$ 会因此相差一个负号，即 $H^+ = -H^-$。主曲率（$S$ 的[特征值](@entry_id:154894)）也会变为其相反数。然而，某些量在此符号变换下保持不变。例如，对于一个二维[曲面](@entry_id:267450)（$n=2$），其[高斯曲率](@entry_id:149725) $K$ 是两个[主曲率](@entry_id:270598)的乘积，因此 $K^+ = (-\kappa_1^-)(-\kappa_2^-) = \kappa_1^-\kappa_2^- = K^-$，[高斯曲率](@entry_id:149725)不受此约定影响。更一般地，高斯-克罗内克曲率 $\det S$ 的变换规则是 $\det S^+ = (-1)^n \det S^-$。[@problem_id:3003618]

另一个与符号相关的微妙之处在于[法向量](@entry_id:264185) $\nu$ 的选择。对于一个可定向超曲面，我们总是有两种选择：$\nu$ 或 $-\nu$。如果我们保持 $S(X) = -\bar{\nabla}_X \nu$ 的定义不变，但将[法向量](@entry_id:264185)替换为 $\nu' = -\nu$，那么新的[形状算子](@entry_id:264703) $S'$ 将是：
$$
S'(X) = -\bar{\nabla}_X (\nu') = -\bar{\nabla}_X (-\nu) = \bar{\nabla}_X \nu = -S(X)
$$
这意味着改变定向（即反转[法向量](@entry_id:264185)）会使[形状算子](@entry_id:264703)变为其相反数。这一性质与前述的定义约定选择的效果类似。相应地，第二基本形式和平均曲率也会变号。然而，值得注意的是，**[平均曲率向量](@entry_id:199617)** $H\nu$ 在此变换下保持不变，因为 $H' = -H$ 且 $\nu' = -\nu$，故 $H'\nu' = (-H)(-\nu) = H\nu$。这个向量是一个[几何不变量](@entry_id:178611)，它不依赖于定向的选择。[@problem_id:3003606]

### 第二基本形式及其与形状算子的关系

为了更深入地理解形状算子的几何意义，我们需要引入**[第二基本形式](@entry_id:161454)**（second fundamental form）。它衡量了子流形相对于背景[流形](@entry_id:153038)的弯曲程度。其标准定义源于**高斯公式**（Gauss formula）。对于 $M$ 上的任意两个切向量场 $X, Y$，它们在背景[流形](@entry_id:153038)中的协变导数 $\bar{\nabla}_X Y$ 可以被唯一地分解为一个切向分量和一个法向分量：
$$
\bar{\nabla}_X Y = (\bar{\nabla}_X Y)^\top + (\bar{\nabla}_X Y)^\perp
$$
其中 $(\cdot)^\top$ 表示到 $T_pM$ 的正交投影，$(\cdot)^\perp$ 表示到法空间 $N_pM$ 的[正交投影](@entry_id:144168)。切向分量定义了 $M$ 上的[诱导联络](@entry_id:635081)（也是一个[列维-奇维塔联络](@entry_id:161107)），记为 $\nabla_X Y = (\bar{\nabla}_X Y)^\top$。法向分量则定义了[第二基本形式](@entry_id:161454)，它是一个取值于[法丛](@entry_id:272447)的[对称双线性形式](@entry_id:148281) $h: \Gamma(TM) \times \Gamma(TM) \to \Gamma(NM)$：
$$
h(X, Y) = (\bar{\nabla}_X Y)^\perp
$$

在[超曲面](@entry_id:159491)的情况下，法空间 $N_pM$ 是一维的，由 $\nu(p)$ 张成。因此，$h(X,Y)$ 必然是 $\nu$ 的一个标量倍。我们可以写成 $h(X,Y) = II(X,Y)\nu$，其中 $II$ 是一个标量值的[对称双线性形式](@entry_id:148281)，被称为**标量第二基本形式**。

现在，我们可以揭示第二基本形式与[形状算子](@entry_id:264703)之间的核心关系。我们从恒等式 $\bar{g}(Y, \nu) = 0$ 出发，并沿 $X$ 方向求导：
$$
0 = X(\bar{g}(Y, \nu)) = \bar{g}(\bar{\nabla}_X Y, \nu) + \bar{g}(Y, \bar{\nabla}_X \nu)
$$
利用高斯公式和[形状算子](@entry_id:264703)的定义，上式可以改写为：
$$
0 = \bar{g}(\nabla_X Y + II(X,Y)\nu, \nu) + \bar{g}(Y, -S(X))
$$
由于 $\nabla_X Y$ 是[切向量](@entry_id:265494)，它与 $\nu$ 正交。同时，$\bar{g}(\nu, \nu) = 1$。因此，方程简化为：
$$
0 = II(X,Y) - g(Y, S(X))
$$
其中 $g$ 是 $M$ 上的诱导度量。由此，我们得到关键关系式：
$$
II(X,Y) = g(S(X), Y)
$$
这个公式表明，第二基本形式 $II$（一个(0,2)型张量）和形状算子 $S$（一个(1,1)型张量）本质上是同一几何信息的不同[代数表示](@entry_id:143783)。它们之间的转换由度量张量 $g$ 及其逆 $g^{-1}$ 来实现，这在坐标中表现为“[升降指标](@entry_id:161292)”的操作。例如，若在[局部坐标系](@entry_id:751394)中 $II$ 的分量为 $II_{ij}$，$S$ 的分量为 $S^k_j$，$g$ 的分量为 $g_{ik}$，则 $II_{ij} = g_{ik} S^k_j$。反之，$S^l_j = g^{li} II_{ij}$。因此，从 $II$ 到 $S$ 的过程离不开度量 $g$ 的参与。[@problem_id:3004776]

### 基本性质与几何解释

#### 自伴性
形状算子最重要的代数性质之一是其**自伴性**（self-adjointness）。这意味着对于任意[切向量](@entry_id:265494) $X, Y \in T_pM$，都有 $g(S(X), Y) = g(X, S(Y))$。该性质是[第二基本形式](@entry_id:161454)对称性的直接推论。$II$ 的对称性，即 $II(X,Y)=II(Y,X)$，又源于背景联络 $\bar{\nabla}$ 的无挠性。证明如下：
$$
II(X,Y) - II(Y,X) = \bar{g}(\bar{\nabla}_X Y, \nu) - \bar{g}(\bar{\nabla}_Y X, \nu) = \bar{g}(\bar{\nabla}_X Y - \bar{\nabla}_Y X, \nu) = \bar{g}([X,Y], \nu)
$$
由于 $X, Y$ 是 $M$ 的切向量场，它们的[李括号](@entry_id:636461) $[X,Y]$ 仍然是 $M$ 的切向量场，因此与[法向量](@entry_id:264185) $\nu$ 正交，即 $\bar{g}([X,Y], \nu) = 0$。故 $II$ 是对称的。于是：
$$
g(S(X),Y) = II(X,Y) = II(Y,X) = g(S(Y),X) = g(X,S(Y))
$$
这就证明了 $S$ 的自伴性。此性质与[形状算子](@entry_id:264703)的定义约定或[定向选择](@entry_id:136267)无关。[@problem_id:3003618] [@problem_id:3003617]

#### [主曲率](@entry_id:270598)与主方向
形状算子 $S_p$ 是一个定义在 $n$ 维实[内积空间](@entry_id:271570) $(T_pM, g_p)$ 上的自伴[线性算子](@entry_id:149003)。根据线性代数中的**谱定理**（spectral theorem），任何这样的算子都具有以下优良性质：
1.  $S_p$ 的所有[特征值](@entry_id:154894)都是实数。
2.  存在一个由 $S_p$ 的[特征向量](@entry_id:151813)组成的 $T_pM$ 的 $g_p$-标准正交基。

这两个性质在几何上具有非凡的意义。$S_p$ 的[特征值](@entry_id:154894)被称为 $M$ 在 $p$ 点的**主曲率**（principal curvatures），记为 $\kappa_1, \dots, \kappa_n$。对应的[特征向量](@entry_id:151813)则定义了**[主方向](@entry_id:276187)**（principal directions）。[谱定理](@entry_id:136620)保证了在每一点，我们总能找到 $n$ 个相互正交的主方向，以及与之对应的 $n$ 个实的[主曲率](@entry_id:270598)（计入重数）。这构成了[子流形](@entry_id:159439)外蕴几何的“骨架”。[@problem_id:3003654]

#### [法曲率](@entry_id:270966)与[欧拉定理](@entry_id:138104)
[形状算子](@entry_id:264703)的几何意义可以通过**[法曲率](@entry_id:270966)**（normal curvature）的概念来直观理解。给定 $p \in M$ 和一个[单位切向量](@entry_id:262985) $v \in T_pM$，我们可以考虑一条参数为[弧长](@entry_id:191173)的曲线 $\gamma(s) \subset M$，使得 $\gamma(0) = p$ 且 $\gamma'(0) = v$。这条曲线在背景[流形](@entry_id:153038) $\bar{M}$ 中的加速度向量为 $\bar{\nabla}_{\gamma'(s)}\gamma'(s)$。在点 $p$，该加速度向量在法方向 $\nu(p)$ 上的投影（带符号）就被定义为 $M$ 在 $v$ 方向的[法曲率](@entry_id:270966) $k_n(v)$。
$$
k_n(v) = \bar{g}(\bar{\nabla}_v v, \nu(p))
$$
这正是[第二基本形式](@entry_id:161454)的二次型 $II(v,v)$。结合我们之前导出的关系，我们得到：
$$
k_n(v) = II(v,v) = g(S(v),v)
$$
这个等式优美地揭示了形状算子的作用：它将一个[方向向量](@entry_id:169562) $v$ 映射为 $S(v)$，而 $S(v)$ 与 $v$ 的[内积](@entry_id:158127)恰好就是该方向的[法曲率](@entry_id:270966)。换言之，[形状算子](@entry_id:264703)通过其关联的二次型 $v \mapsto g(S(v),v)$，完全编码了所有方向的[法曲率](@entry_id:270966)信息。[@problem_id:3003642]

**[欧拉定理](@entry_id:138104)**（Euler's Theorem）是这一思想在二维[曲面](@entry_id:267450)上的经典体现。设 $e_1, e_2$ 为 $p$ 点的两个主方向，对应主曲率 $\kappa_1, \kappa_2$。任何一个[单位切向量](@entry_id:262985) $v$ 都可以表示为 $v = \cos\theta e_1 + \sin\theta e_2$。利用 $S$ 的线性性和自伴性，以及 $S(e_i) = \kappa_i e_i$ 和 $g(e_i, e_j)=\delta_{ij}$，我们计算[法曲率](@entry_id:270966)：
$$
k_n(v) = g(S(v),v) = g(\kappa_1\cos\theta e_1 + \kappa_2\sin\theta e_2, \cos\theta e_1 + \sin\theta e_2) = \kappa_1\cos^2\theta + \kappa_2\sin^2\theta
$$
这正是[欧拉定理](@entry_id:138104)的表达式，它表明任意方向的[法曲率](@entry_id:270966)可以由两个主曲率插值得到。

#### 外蕴曲率[不变量](@entry_id:148850)
[主曲率](@entry_id:270598)是研究外蕴几何的基本构件。通过它们，我们可以构造出许多重要的[几何不变量](@entry_id:178611)。这些[不变量](@entry_id:148850)是主曲率的[对称多项式](@entry_id:153581)，其中最著名的是：
- **平均曲率**（Mean Curvature）: $H = \frac{1}{n} \sum_{i=1}^n \kappa_i = \frac{1}{n} \mathrm{tr}(S)$
- **高斯-克罗内克曲率**（Gauss-Kronecker Curvature）: $K_G = \prod_{i=1}^n \kappa_i = \det(S)$

对于二维[曲面](@entry_id:267450)，高斯-克罗内克曲率就是著名的[高斯曲率](@entry_id:149725) $K$。如前所述，改变定向 $\nu \to -\nu$ 会使所有[主曲率](@entry_id:270598)变号 $\kappa_i \to -\kappa_i$。因此，任何奇数阶的主曲率[对称多项式](@entry_id:153581)（如[平均曲率](@entry_id:162147)）都会变号，而任何偶数阶的[对称多项式](@entry_id:153581)（如 $|S|^2 = \sum_i \kappa_i^2$，以及偶数维时的高斯-克罗内克曲率）则保持不变。[@problem_id:3003606]

### 向高[余维](@entry_id:273141)推广

现在我们将形状算子的概念从超曲面推广到嵌入在 $(n+k)$ 维[黎曼流形](@entry_id:261160) $(\bar{M}^{n+k}, \bar{g})$ 中的任意 $n$ 维子流形 $M^n$ ([余维](@entry_id:273141) $k \ge 1$)。

此时，在每一点 $p \in M$，法空间 $N_pM$ 是一个 $k$ 维[向量空间](@entry_id:151108)。高斯公式 $\bar{\nabla}_X Y = \nabla_X Y + h(X, Y)$ 依然成立，但第二基本形式 $h(X,Y)$ 是一个取值于 $k$ 维法空间的向量。我们无法再像[超曲面](@entry_id:159491)那样定义一个单一的形状算子。取而代之的是，我们为法空间中的**每一个**法向量方向 $\xi \in N_pM$ 定义一个形状算子。

对于任意[法向量场](@entry_id:268853) $\xi \in \Gamma(NM)$，我们定义与之关联的**形状算子** $A_\xi: \Gamma(TM) \to \Gamma(TM)$，它通过以下关系式与第二基本形式 $h$ 挂钩：
$$
g(A_\xi X, Y) = \bar{g}(h(X, Y), \xi)
$$
对所有[切向量](@entry_id:265494)场 $X, Y$ 成立。这个定义表明，$A_\xi X$ 是通过度量 $g$ 与“将 $h(X, \cdot)$ 投影到 $\xi$ 方向上”这一线性泛函对偶的切向量。由于 $h$ 对其两个[切向量](@entry_id:265494)参数是对称的，易证每个 $A_\xi$ 都是 $g$-自伴的。

此外，从定义可以看出，映射 $\xi \mapsto A_\xi$ 是线性的，即 $A_{a\xi_1 + b\xi_2} = a A_{\xi_1} + b A_{\xi_2}$。因此，我们得到的是一个从[法丛](@entry_id:272447)到 $TM$ 上[自伴算子](@entry_id:152188)丛的线性映射。[@problem_id:3003617]

与[超曲面](@entry_id:159491)情形类似，高[余维](@entry_id:273141)的[形状算子](@entry_id:264703)也与[法向量场](@entry_id:268853)的[协变导数](@entry_id:152476)有关，这体现在**温加滕公式**（Weingarten formula）中。对于任意[法向量场](@entry_id:268853) $\xi$ 和[切向量](@entry_id:265494)场 $X$，协变导数 $\bar{\nabla}_X \xi$ 同样可以分解为切向和法向分量：
$$
\bar{\nabla}_X \xi = (\bar{\nabla}_X \xi)^\top + (\bar{\nabla}_X \xi)^\perp
$$
可以证明，其切向分量恰好由形状算子 $A_\xi$ 给出：
$$
(\bar{\nabla}_X \xi)^\top = -A_\xi X
$$
其法向分量则定义了[法丛](@entry_id:272447)上的一个联络，称为**法联络**（normal connection） $\nabla^\perp_X \xi = (\bar{\nabla}_X \xi)^\perp$。于是温加滕公式的完整形式为：
$$
\bar{\nabla}_X \xi = -A_\xi X + \nabla^\perp_X \xi
$$
这个公式解释了为何在高[余维](@entry_id:273141)情况下，我们获得的是一个算子族而非单个算子。$\bar{\nabla}_X \xi$ 的变化不仅包含了一个切向的“形状”部分（由 $A_\xi$ 描述），还包含了一个法向的“扭转”部分（由 $\nabla^\perp$ 描述）。只有在[超曲面](@entry_id:159491)（$k=1$）情况下，$\bar{\nabla}_X \nu$ 没有法向分量（因为它必须与 $\nu$ 正交），因此它完全由一个到[切空间](@entry_id:199137)的映射所决定。这正是术语“温加滕映射”通常保留给超曲面情形的原因。[@problem_id:3003648]

### 计算方法

理论的生命力在于其[可计算性](@entry_id:276011)。下面我们通过两个范例，展示如何具体计算[形状算子](@entry_id:264703)。

#### 基于坐标的方法
此方法适用于当背景度量和子[流形嵌入](@entry_id:159781)均有显式坐标表达式时。我们将以一个具体问题为例 [@problem_id:3003646]。

考虑一个三维[黎曼流形](@entry_id:261160) $(\bar{M}, \bar{g})$，其度量为 $\bar{g} = \lambda(z)^2(dx^2 + dy^2) + dz^2$。浸入的[曲面](@entry_id:267450) $M$ 由图 $z = f(x,y) = \frac{\kappa}{2}(x^2+y^2)$ 给出。我们希望计算在原点 $p=(0,0,0)$ 的[形状算子](@entry_id:264703)。

计算步骤如下：
1.  **计算背景联络**：根据度量 $\bar{g}_{\alpha\beta}$ 的表达式，利用公式 $\bar{\Gamma}^{\alpha}_{\beta\gamma} = \frac{1}{2}\bar{g}^{\alpha\delta}(\partial_\beta \bar{g}_{\delta\gamma} + \partial_\gamma \bar{g}_{\delta\beta} - \partial_\delta \bar{g}_{\beta\gamma})$ 计算背景[流形](@entry_id:153038)的克氏符（Christoffel symbols）。在我们的例子中，在点 $p$ 处，非零的克氏符为 $\bar{\Gamma}^1_{13}|_p = \bar{\Gamma}^1_{31}|_p = \mu$, $\bar{\Gamma}^2_{23}|_p = \bar{\Gamma}^2_{32}|_p = \mu$, $\bar{\Gamma}^3_{11}|_p = -\mu$, $\bar{\Gamma}^3_{22}|_p = -\mu$，其中 $\mu = \lambda'(0)$。

2.  **计算[第二基本形式](@entry_id:161454)**：利用高斯公式的法向部分 $h(X,Y) = (\bar{\nabla}_X Y)^\perp$。在[局部坐标](@entry_id:181200) $(x^1, x^2)$ 中，[基向量](@entry_id:199546)为 $\partial_i = \partial\Phi/\partial x^i$。$\bar{\nabla}_{\partial_i} \partial_j$ 的分量形式为 $(\bar{\nabla}_{\partial_i} \partial_j)^\alpha = \frac{\partial^2 y^\alpha}{\partial x^i \partial x^j} + \sum_{\beta, \gamma} \bar{\Gamma}^\alpha_{\beta\gamma} \frac{\partial y^\beta}{\partial x^i} \frac{\partial y^\gamma}{\partial x^j}$。在点 $p$，[切向量](@entry_id:265494)为 $\partial_1|_p = (1,0,0)$ 和 $\partial_2|_p = (0,1,0)$，[单位法向量](@entry_id:178851)为 $N|_p = (0,0,1)$。计算可得 $\bar{\nabla}_{\partial_1}\partial_1|_p = (\kappa-\mu)\partial_3$, $\bar{\nabla}_{\partial_2}\partial_2|_p = (\kappa-\mu)\partial_3$, $\bar{\nabla}_{\partial_1}\partial_2|_p = 0$。因此第二基本形式 $II(\partial_i, \partial_j) = \bar{g}(\bar{\nabla}_{\partial_i}\partial_j, N)$ 的矩阵为：
    $$
    [II_{ij}]_p = \begin{pmatrix} \kappa-\mu  & 0 \\ 0 & \kappa-\mu \end{pmatrix}
    $$

3.  **计算[形状算子](@entry_id:264703)**：首先计算诱导度量 $g_{ij} = \bar{g}(\partial_i, \partial_j)$。在点 $p$，$[g_{ij}]_p$ 是[单位矩阵](@entry_id:156724)。[形状算子](@entry_id:264703)的矩阵 $[S^i_j]$ 由关系 $[S] = [g]^{-1}[II]$ 给出。因此：
    $$
    [S^i_j]_p = \begin{pmatrix} 1 & 0 \\ 0 & 1 \end{pmatrix}^{-1} \begin{pmatrix} \kappa-\mu & 0 \\ 0 & \kappa-\mu \end{pmatrix} = \begin{pmatrix} \kappa-\mu & 0 \\ 0 & \kappa-\mu \end{pmatrix}
    $$
    此例中，高斯曲率 $K(p) = \det S(p) = (\kappa-\mu)^2$。

#### [活动标架法](@entry_id:175562)
此方法在处理具有对称性的几何对象时尤为强大。我们将以一个在[欧氏空间](@entry_id:138052) $\mathbb{R}^3$ 中的[曲面](@entry_id:267450)为例 [@problem_id:3003613]。

考虑[曲面](@entry_id:267450) $M$ 由 $z = f(u,v) = \frac{1}{2}(\alpha u^2 + 2\beta uv + \gamma v^2)$ 给出，我们希望计算原点 $p$ 的[高斯曲率](@entry_id:149725)。

1.  **选取[活动标架](@entry_id:175562)**：在 $p$ 点附近选取一个[标准正交标架](@entry_id:189702)场 $\{e_1, e_2, e_3\}$，使得 $e_1, e_2$ 是 $M$ 的[切向量](@entry_id:265494)，而 $e_3$ 是[法向量](@entry_id:264185)。在点 $p=(0,0,0)$，我们可以取 $e_1(p)=(1,0,0)$, $e_2(p)=(0,1,0)$, $e_3(p)=(0,0,1)$。

2.  **利用[联络形式](@entry_id:263247)**：形状算子 $S$ 的定义 $S(X) = -\bar{\nabla}_X e_3$ 在标架基下可表示为 $S(e_j) = \sum_i S_{ij} e_i$。另一方面，背景联络的定义 $\bar{\nabla}e_b = \sum_a \omega^a_b e_a$ 给出 $\bar{\nabla}_{e_j}e_3 = \sum_a \omega^a_3(e_j)e_a$。由于 $S(e_j)$ 是切向量，我们有：
    $$
    S(e_j) = -\omega^1_3(e_j)e_1 - \omega^2_3(e_j)e_2
    $$
    因此，$S_{ij} = -\omega^i_3(e_j)$。利用[联络形式](@entry_id:263247)的反对称性 $\omega^i_3 = -\omega^3_i$，得到：
    $$
    S_{ij} = \omega^3_i(e_j)
    $$

3.  **计算[联络形式](@entry_id:263247)**：在[欧氏空间](@entry_id:138052)中，[联络形式](@entry_id:263247)由标架向量场的外微分给出：$\omega^a_b(X) = \langle de_b(X), e_a \rangle = \langle \bar{\nabla}_X e_b, e_a \rangle$。因此，$S_{ij} = \langle \bar{\nabla}_{e_j}e_i, e_3 \rangle|_p$。这等价于计算切[标架场](@entry_id:160577) $e_i, e_j$ 在 $p$ 点的法向[二阶导数](@entry_id:144508)。通过对切向量场 $F_u, F_v$ 进行 Gram-Schmidt [正交化](@entry_id:149208)得到[标架场](@entry_id:160577) $e_1, e_2$ 的[一阶近似](@entry_id:147559)，并求其在 $p$ 点的导数，我们得到：
    $$
    S_{11} = \alpha, \quad S_{12} = \beta, \quad S_{21} = \beta, \quad S_{22} = \gamma
    $$
    所以[形状算子](@entry_id:264703)的矩阵为：
    $$
    S_p = \begin{pmatrix} \alpha & \beta \\ \beta & \gamma \end{pmatrix}
    $$
    高斯曲率 $K(p) = \det(S_p) = \alpha\gamma - \beta^2$。

### 形状算子在[子流形](@entry_id:159439)基本方程中的作用

形状算子不仅是计算工具，它更是[子流形理论](@entry_id:190701)的理论核心。它作为外蕴曲率的主要载体，出现在描述内外蕴几何关系的一组基本方程中，即**高斯-科达齐-里奇（Gauss-Codazzi-Ricci）[方程组](@entry_id:193238)**。[@problem_id:3003644]

1.  **[高斯方程](@entry_id:192573)**：此方程将[子流形](@entry_id:159439) $M$ 的内蕴曲率（由其黎曼曲率张量 $R$ 描述）与背景[流形](@entry_id:153038) $\bar{M}$ 的曲率（由 $\bar{R}$ 描述）联系起来。其表达式为：
    $$
    \langle R(X,Y)Z,W \rangle = \langle \bar{R}(X,Y)Z,W \rangle + \langle h(X,W), h(Y,Z) \rangle - \langle h(X,Z), h(Y,W) \rangle
    $$
    右边最后两项是第二基本形式的二次项，完全由[形状算子](@entry_id:264703)族 $\{A_\xi\}$ 决定。这个方程揭示了[子流形](@entry_id:159439)的[内蕴曲率](@entry_id:161701)部分地由其所处的空间弯曲决定，部分地由其自身的嵌入方式（外蕴弯曲）决定。[高斯绝妙定理](@entry_id:159067)（Theorema Egregium）正是此方程在二维[曲面](@entry_id:267450)嵌入 $\mathbb{R}^3$ 时的特例，它表明高斯曲率完全由内蕴度量决定。

2.  **科达齐-迈纳尔迪方程**（Codazzi-Mainardi Equation）：此方程给出了第二基本形式（或形状算子）的导数所必须满足的约束。它将 $h$ 的[协变导数](@entry_id:152476)的反对称部分与背景[曲率张量](@entry_id:181383)的法向分量联系起来：
    $$
    (\bar{R}(X,Y)Z)^\perp = (\nabla_X h)(Y,Z) - (\nabla_Y h)(X,Z)
    $$
    其中 $(\nabla h)$ 是 $h$ 的[协变导数](@entry_id:152476)。这个方程可以看作是子[流形嵌入](@entry_id:159781)的“可积性条件”之一。

3.  **里奇方程**（Ricci Equation）：此方程描述了[法丛](@entry_id:272447)自身的曲率（由法联络 $\nabla^\perp$ 的[曲率张量](@entry_id:181383) $R^\perp$ 描述）。它将[法曲率](@entry_id:270966)与背景曲率以及[形状算子](@entry_id:264703)对的交换子联系起来：
    $$
    \langle R^\perp(X,Y)\xi, \eta \rangle = \langle \bar{R}(X,Y)\xi, \eta \rangle + \langle [A_\xi, A_\eta]X, Y \rangle
    $$
    其中 $[A_\xi, A_\eta] = A_\xi A_\eta - A_\eta A_\xi$ 是两个[形状算子](@entry_id:264703)的李括号（交换子）。

里奇方程提供了一个理解高[余维](@entry_id:273141)几何的有力工具。例如，考虑一个[余维](@entry_id:273141)为2的子流形 [@problem_id:3003629]。此时[法丛](@entry_id:272447)是二维的，其曲率由一个标量函数完全决定。里奇方程揭示了[法丛](@entry_id:272447)的曲率（即[法丛](@entry_id:272447)是否“平坦”）、背景空间的曲率以及形状算子是否交换这三者之间的深刻联系。特别地，如果背景空间是[常曲率空间](@entry_id:161841)（如[欧氏空间](@entry_id:138052)、球面或[双曲空间](@entry_id:268092)），则 $\langle \bar{R}(X,Y)\xi, \eta \rangle = 0$。此时里奇方程简化为：
$$
\langle R^\perp(X,Y)\xi, \eta \rangle = \langle [A_\xi, A_\eta]X, Y \rangle
$$
这表明，在[常曲率](@entry_id:162122)背景空间中，**法联络是平坦的（$R^\perp=0$）当且仅当任意两个正交法方向对应的形状算子相互交换（$[A_{\xi_1}, A_{\xi_2}]=0$）**。这一结论是现代[子流形几何](@entry_id:189265)中的一个基本结果，它将一个代数条件（算子[交换性](@entry_id:140240)）与一个几何条件（[法丛](@entry_id:272447)平坦性）等同起来，充分展示了[形状算子](@entry_id:264703)作为理论核心的强大威力。