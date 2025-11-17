## 引言
在[黎曼几何](@entry_id:160508)的广阔图景中，子流形的研究占据着核心地位。我们身边的世界充满了各种几何形状——从肥皂膜的优美[曲面](@entry_id:267450)到行星运行的[轨道](@entry_id:137151)——它们都可以被数学地描述为嵌入在更高维空间中的子流形。一个根本性的问题随之产生：一个[子流形](@entry_id:159439)的[内蕴几何](@entry_id:158788)属性（如其自身的距离和曲率）如何与其在外围空间中的嵌入方式（其外在的弯曲形态）相互关联？高斯公式与[魏恩加滕公式](@entry_id:635565)正是解答这一问题的关键钥匙，它们构成了连接[内蕴几何与外在几何](@entry_id:161677)的数学桥梁。

本文旨在系统地阐释这两个基本公式。读者将通过本文的学习，掌握子流形微分几何的基石。
- 在“原理与机制”一章中，我们将从外围空间协变导数的分解出发，严格推导出高斯公式和[魏恩加滕公式](@entry_id:635565)，并阐明[第二基本形式](@entry_id:161454)与[形状算子](@entry_id:264703)的几何意义。
- 接着，在“应用与跨学科联系”一章中，我们将展示这些公式如何应用于计算[曲面](@entry_id:267450)的[高斯曲率](@entry_id:149725)与平均曲率、定义和理解物理世界中的[极小曲面](@entry_id:157732)，并为现代几何分析中的演化方程提供理论基础。
- 最后，通过“动手实践”部分的引导，您将有机会亲手计算具体案例，将抽象的理论转化为坚实的几何直觉和计算能力。

让我们首先深入这些公式的“原理与机制”，揭示它们如何将一个复杂的几何问题分解为可分析的内蕴与外在两个部分。

## 原理与机制

本章旨在深入探讨浸入黎曼[子流形几何](@entry_id:189265)学的基本[结构方程](@entry_id:274644)：高斯公式（Gauss formula）和[魏恩加滕公式](@entry_id:635565)（Weingarten formula）。这些公式是连接子[流形](@entry_id:153038)（submanifold）的[内蕴几何](@entry_id:158788)（intrinsic geometry）与其在外围空间（ambient space）中弯曲方式（外在曲率, extrinsic curvature）的关键桥梁。我们将从第一性原理出发，通过分解外围空间的[协变导数](@entry_id:152476)，系统地定义并推导这些公式的核心组成部分，阐明它们的几何意义和相互关系。

### [协变导数](@entry_id:152476)的基本分解

一切理论的出发点是一个简单而深刻的观察。设 $(\overline{M}, \overline{g})$ 是一个黎曼流形，其[列维-奇维塔联络](@entry_id:161107)（Levi-Civita connection）为 $\overline{\nabla}$。再设 $M$ 是 $\overline{M}$ 的一个[浸入子流形](@entry_id:264923)，其上赋有由 $\overline{g}$ 诱导的度量 $g$。对于 $M$ 上的任意一点 $p$，$\overline{M}$ 在该点的[切空间](@entry_id:199137) $T_p\overline{M}$ 可以[正交分解](@entry_id:148020)为 $M$ 的[切空间](@entry_id:199137) $T_pM$ 和法空间 $N_pM$ 的直和：
$$
T_p\overline{M} = T_pM \oplus N_pM
$$
这个分解是核心。它意味着任何沿 $M$ 定义的、存在于外围空间切丛中的向量场，在每一点都可以唯一地分解为其切向分量（tangential component）和法向分量（normal component）。我们将分别用上标 $(\cdot)^\top$ 和 $(\cdot)^\perp$ 表示到 $T_pM$ 和 $N_pM$ 的正交投影。

现在，考虑[子流形](@entry_id:159439) $M$ 上的两个切向量场 $X, Y \in \Gamma(TM)$。外围联络 $\overline{\nabla}$ 作用于它们所产生的[协变导数](@entry_id:152476) $\overline{\nabla}_X Y$ 是一个沿 $M$ 定义的向量场，但其在每一点 $p$ 的值 $\overline{\nabla}_X Y|_p$ 通常并不位于 $T_pM$ 中。然而，我们可以利用上述的[正交分解](@entry_id:148020)来剖析它：
$$
\overline{\nabla}_X Y = (\overline{\nabla}_X Y)^\top + (\overline{\nabla}_X Y)^\perp
$$
这个简单的分解将一个外围几何对象分解成两个与子流形 $M$ 直接相关的部分。正是这两个分量，定义了[子流形几何](@entry_id:189265)中最重要的两个外在几何量，并引出了高斯公式。

### 高斯公式：内蕴联络与[外在曲率](@entry_id:160405)

我们基于上述分解来定义两个核心对象。

首先，我们将 $\overline{\nabla}_X Y$ 的 **切向分量** 定义为 $M$ 上的一个新联络，称为 **[诱导联络](@entry_id:635081)（induced connection）**，记作 $\nabla$：
$$
\nabla_X Y := (\overline{\nabla}_X Y)^\top
$$
其次，我们将 $\overline{\nabla}_X Y$ 的 **法向分量** 定义为一个[法丛](@entry_id:272447)值的映射，称为 **第二基本形式（second fundamental form）**，记作 $B(X,Y)$ 或 $\mathrm{II}(X,Y)$：
$$
B(X,Y) := (\overline{\nabla}_X Y)^\perp
$$
将这两个定义代回分解式，我们便得到了著名的 **高斯公式** [@problem_id:3042719] [@problem_id:2997218]：
$$
\overline{\nabla}_X Y = \nabla_X Y + B(X,Y)
$$
这个公式优雅地表明，外围空间中沿[子流形](@entry_id:159439)切[向量的[协变导](@entry_id:191566)数](@entry_id:152476)，可以分解为[子流形](@entry_id:159439)自身的（内蕴的）协变导数和一个纯粹的法向量。

#### [诱导联络](@entry_id:635081)的内蕴本质

一个自然的问题是：这个[诱导联络](@entry_id:635081) $\nabla$ 究竟是什么？惊人的结论是，它正是[子流形](@entry_id:159439) $(M,g)$ 自身的[列维-奇维塔联络](@entry_id:161107) [@problem_id:3071118] [@problem_id:2997574]。根据[黎曼几何基本定理](@entry_id:189185)，一个度量[流形](@entry_id:153038)上的列维-奇维塔联络是唯一满足“无挠（torsion-free）”和“度量兼容（metric-compatible）”这两个条件的联络。我们可以证明 $\nabla$ 恰好满足这两个条件。

1.  **无挠性**：联络 $\nabla$ 的[挠率张量](@entry_id:204137)定义为 $T(X,Y) = \nabla_X Y - \nabla_Y X - [X,Y]$。利用 $\nabla$ 的定义以及外围联络 $\overline{\nabla}$ 的无挠性（即 $\overline{\nabla}_X Y - \overline{\nabla}_Y X = [X,Y]$），我们有：
    $$
    \nabla_X Y - \nabla_Y X = (\overline{\nabla}_X Y)^\top - (\overline{\nabla}_Y X)^\top = (\overline{\nabla}_X Y - \overline{\nabla}_Y X)^\top = ([X,Y])^\top
    $$
    由于 $X$ 和 $Y$ 是 $M$ 的切向量场，它们的[李括号](@entry_id:636461) $[X,Y]$ 同样是 $M$ 的[切向量](@entry_id:265494)场。因此，其切向投影就是它自身，即 $([X,Y])^\top = [X,Y]$。于是我们得到 $\nabla_X Y - \nabla_Y X = [X,Y]$，这表明 $\nabla$ 是[无挠的](@entry_id:161664)。

2.  **[度量兼容性](@entry_id:265910)**：我们需要验证 $Z(g(X,Y)) = g(\nabla_Z X, Y) + g(X, \nabla_Z Y)$。由于 $g$ 是诱导度量，我们有 $g(X,Y) = \overline{g}(X,Y)$。利用 $\overline{\nabla}$ 与 $\overline{g}$ 的兼容性以及高斯公式：
    $$
    \begin{align*}
    Z(g(X,Y)) = Z(\overline{g}(X,Y)) \\
    = \overline{g}(\overline{\nabla}_Z X, Y) + \overline{g}(X, \overline{\nabla}_Z Y) \\
    = \overline{g}(\nabla_Z X + B(Z,X), Y) + \overline{g}(X, \nabla_Z Y + B(Z,Y))
    \end{align*}
    $$
    由于 $\nabla_Z X$ 和 $Y$ 是[切向量](@entry_id:265494)，而 $B(Z,X)$ 是[法向量](@entry_id:264185)，它们是正交的，即 $\overline{g}(B(Z,X), Y) = 0$。同理 $\overline{g}(X, B(Z,Y)) = 0$。因此，上式简化为：
    $$
    Z(g(X,Y)) = \overline{g}(\nabla_Z X, Y) + \overline{g}(X, \nabla_Z Y) = g(\nabla_Z X, Y) + g(X, \nabla_Z Y)
    $$
    这证明了 $\nabla$ 与 $g$ 兼容。

因此，由外围联络的切向投影定义的 $\nabla$ 就是 $(M,g)$ 内蕴的列维-奇维塔联络。这意味着子流形的内蕴几何（如[测地线](@entry_id:269969)、平行移动）完全由其诱导度量 $g$ 决定，而与它如何被嵌入到 $\overline{M}$ 中无关 [@problem_id:2997574]。这是一个深刻的结论，高斯本人称之为他的“[绝妙定理](@entry_id:159067)”（Theorema Egregium）的推广。

#### [第二基本形式](@entry_id:161454)的几何意义

如果说 $\nabla_X Y$ 描述了子流形内部的几何，那么 $B(X,Y)$ 则描述了[子流形](@entry_id:159439)如何在外围空间中弯曲，是 **[外在曲率](@entry_id:160405)** 的基本度量。$B(X,Y)$ 衡量了当沿着 $X$ 方向移动时，$Y$ 这个[切向量](@entry_id:265494)的变化率“偏离”子流形切空间的程度。如果一个[子流形](@entry_id:159439)是“平直”地嵌入的（例如 $\mathbb{R}^2$ 在 $\mathbb{R}^3$ 中作为一个平面），那么任何[切向量](@entry_id:265494)场对另一个[切向量](@entry_id:265494)场的[协变导数](@entry_id:152476)仍然是[切向量](@entry_id:265494)场，此时 $B(X,Y)$ 恒为零。这样的子流形被称为 **[全测地子流形](@entry_id:637049)（totally geodesic submanifold）** [@problem_id:2997574]。

第二基本形式 $B$ 具有两个至关重要的代数性质 [@problem_id:2997223] [@problem_id:3071118]：
1.  **张量性**：$B(X,Y)$ 对于 $X$ 和 $Y$ 是 $C^\infty(M)$-[双线性](@entry_id:146819)的。这意味着在某一点 $p$， $B(X,Y)|_p$ 的值只依赖于 $X(p)$ 和 $Y(p)$，而与向量场在 $p$ 点邻域内的变化无关。这一点源于联络算子 $\overline{\nabla}$ 在第一个变量上的线性和在第二个变量上的莱布尼茨律。特别是对于第二个变量 $Y$，例如 $B(X, fY) = (\overline{\nabla}_X(fY))^\perp = ((Xf)Y + f\overline{\nabla}_X Y)^\perp = (Xf)Y^\perp + f(\overline{\nabla}_X Y)^\perp$。由于 $Y$ 是切向量，$Y^\perp = 0$，故 $B(X, fY) = f B(X,Y)$。
2.  **对称性**：$B(X,Y) = B(Y,X)$。这个性质是外围联络 $\overline{\nabla}$ 无挠性的直接推论：
    $$
    B(X,Y) - B(Y,X) = (\overline{\nabla}_X Y)^\perp - (\overline{\nabla}_Y X)^\perp = (\overline{\nabla}_X Y - \overline{\nabla}_Y X)^\perp = ([X,Y])^\perp
    $$
    由于 $[X,Y]$ 仍是 $M$ 的切向量场，它的法向分量为零。因此 $B(X,Y) = B(Y,X)$。

作为一个具体的例子 [@problem_id:2997189]，考虑 $\mathbb{R}^3$ 中的一个[曲面](@entry_id:267450)，由 $r(u,v) = (u, v, u^2+v^3)$ 参数化。在原点 $(0,0,0)$，[切向量](@entry_id:265494) $X = \partial_u$ 对应的向量是 $r_u(0,0)=(1,0,0)$，[单位法向量](@entry_id:178851)是 $\nu=(0,0,1)$。在 $\mathbb{R}^3$ 中，$\overline{\nabla}$ 就是通常的[方向导数](@entry_id:189133)。我们计算 $\overline{\nabla}_X X$ 在原点的值：
$$
\overline{\nabla}_{\partial_u} r_u = \frac{\partial}{\partial u} r_u(u,v) = \frac{\partial}{\partial u}(1,0,2u) = (0,0,2)
$$
这个向量 $(0,0,2)$ 就是 $\overline{\nabla}_X X$ 在原点的值。它的切向分量 $(\nabla_X X)_p$ 是其在 $xy$ 平面（即 $T_pM$）上的投影，为 $(0,0,0)$。它的法向分量 $B(X,X)_p$ 则是 $(0,0,2)$。我们看到，正是因为[曲面](@entry_id:267450)是弯曲的，才导致了非零的法向分量。与[单位法向量](@entry_id:178851) $\nu$ 的[内积](@entry_id:158127) $\langle B(X,X), \nu \rangle = \langle (0,0,2), (0,0,1) \rangle = 2$，这个数值度量了[曲面](@entry_id:267450)在 $\partial_u$ 方向的加速度偏离切平面的程度。

### [魏恩加滕公式](@entry_id:635565)：形状算子与法联络

高斯公式分析了[切向量](@entry_id:265494)场对切向量场的导数。现在我们转向分析切向量场对 **[法向量场](@entry_id:268853)** 的导数。设 $X \in \Gamma(TM)$ 是一个切向量场，$\nu \in \Gamma(NM)$ 是一个沿 $M$ 的[法向量场](@entry_id:268853)。同样，外围导数 $\overline{\nabla}_X \nu$ 也可以分解为切向和法向分量：
$$
\overline{\nabla}_X \nu = (\overline{\nabla}_X \nu)^\top + (\overline{\nabla}_X \nu)^\perp
$$
这个分解同样定义了两个重要的几何对象。

我们定义 **[形状算子](@entry_id:264703)（shape operator）**（或[魏恩加滕映射](@entry_id:271773)）$A_\nu$ 是一个从 $TM$ 到 $TM$ 的线性算子，它由 $\overline{\nabla}_X \nu$ 的切向分量给出，但带有一个关键的负号（这是一个重要的惯例）：
$$
A_\nu(X) := -(\overline{\nabla}_X \nu)^\top
$$
同时，我们将法向分量定义为 **法联络（normal connection）** $\nabla^\perp$：
$$
\nabla^\perp_X \nu := (\overline{\nabla}_X \nu)^\perp
$$
将这些定义代入，便得到 **[魏恩加滕公式](@entry_id:635565)** [@problem_id:2997225]：
$$
\overline{\nabla}_X \nu = -A_\nu(X) + \nabla^\perp_X \nu
$$
形状算子 $A_\nu(X)$ 描述了[法向量](@entry_id:264185) $\nu$ 沿着切方向 $X$ 变化时，其变化率“掉入”[切空间](@entry_id:199137)的部分。它直接反映了子流形的弯曲如何影响法向量的变化。

#### 形状算子与第二基本形式的对偶关系

[形状算子](@entry_id:264703)和[第二基本形式](@entry_id:161454)并非孤立，而是通过一个优美的对偶关系紧密联系在一起。这个关系是[子流形几何](@entry_id:189265)学的基石之一。我们考虑两个[切向量](@entry_id:265494)场 $X, Y$ 和一个[法向量场](@entry_id:268853) $\nu$。由于 $Y$ 和 $\nu$ 处处正交，$\overline{g}(Y, \nu) = 0$。利用 $\overline{\nabla}$ 的[度量兼容性](@entry_id:265910)对此式求导：
$$
0 = X(\overline{g}(Y, \nu)) = \overline{g}(\overline{\nabla}_X Y, \nu) + \overline{g}(Y, \overline{\nabla}_X \nu)
$$
现在，我们将高斯公式和[魏恩加滕公式](@entry_id:635565)代入并利用正交性。
-   $\overline{g}(\overline{\nabla}_X Y, \nu) = \overline{g}(\nabla_X Y + B(X,Y), \nu) = \overline{g}(B(X,Y), \nu)$。
-   $\overline{g}(Y, \overline{\nabla}_X \nu) = \overline{g}(Y, -A_\nu(X) + \nabla^\perp_X \nu) = -\overline{g}(Y, A_\nu(X))$。

代入求导的等式，得到：
$$
\overline{g}(B(X,Y), \nu) - \overline{g}(Y, A_\nu(X)) = 0
$$
由于 $A_\nu(X)$ 和 $Y$ 都是切向量，它们的[内积](@entry_id:158127)可以用 $M$ 上的度量 $g$ 表示，即 $\overline{g}(Y, A_\nu(X)) = g(Y, A_\nu(X)) = g(A_\nu(X), Y)$。于是我们得到了这个核心关系式 [@problem_id:3071118] [@problem_id:2997225] [@problem_id:2997183]：
$$
\overline{g}(B(X,Y), \nu) = g(A_\nu(X), Y)
$$
这个等式表明，[第二基本形式](@entry_id:161454)在法方向 $\nu$ 上的分量，可以通过形状算子 $A_\nu$ 在切空间中的作用来度量。

这个关系的一个直接推论是，形状算子 $A_\nu$ 是一个 **自伴算子（self-adjoint operator）** [@problem_id:3071118] [@problem_id:2997574]。这意味着 $g(A_\nu X, Y) = g(X, A_\nu Y)$。证明如下：
$$
g(A_\nu X, Y) = \overline{g}(B(X,Y), \nu)
$$
利用 $B$ 的对称性 $B(X,Y)=B(Y,X)$ 和度量 $g$ 的对称性：
$$
g(X, A_\nu Y) = g(A_\nu Y, X) = \overline{g}(B(Y,X), \nu) = \overline{g}(B(X,Y), \nu)
$$
因此，$g(A_\nu X, Y) = g(X, A_\nu Y)$。因为 $A_\nu$ 是自伴的，所以在每一点它都有一组正交的[特征向量](@entry_id:151813)和实数的[特征值](@entry_id:154894)。这些[特征值](@entry_id:154894)被称为 **[主曲率](@entry_id:270598)（principal curvatures）**，它们描述了子流形在不同方向上最剧烈和最平缓的弯曲程度。

#### 法联络

[魏恩加滕公式](@entry_id:635565)中的另一项，法联络 $\nabla^\perp_X \nu = (\overline{\nabla}_X \nu)^\perp$，描述了法向量 $\nu$ 沿切方向 $X$ 变化时，其变化率中保持在法空间内的部分。可以证明，这个法联络是在[法丛](@entry_id:272447) $NM$ 上的一个与度量兼容的联络 [@problem_id:2997225]。也就是说，对于任意两个[法向量场](@entry_id:268853) $\xi, \eta$：
$$
X(\overline{g}(\xi, \eta)) = \overline{g}(\nabla^\perp_X \xi, \eta) + \overline{g}(\xi, \nabla^\perp_X \eta)
$$
在 **[余维](@entry_id:273141)为1（codimension-one）** 的[超曲面](@entry_id:159491)情形下，[法丛](@entry_id:272447)是一维的。如果我们选取一个[单位法向量](@entry_id:178851)场 $\nu$，那么在任何一点，法空间都由 $\nu$ 张成。此时法联络的行为变得非常简单。因为 $\overline{g}(\nu, \nu) = 1$，对其求导得到 $2\overline{g}(\overline{\nabla}_X \nu, \nu) = 0$。这意味着 $\overline{\nabla}_X \nu$ 总是与 $\nu$ 正交，即它是一个切向量。因此，它的法向分量必定为零 [@problem_id:3071118] [@problem_id:2997203]：
$$
\nabla^\perp_X \nu = (\overline{\nabla}_X \nu)^\perp = \overline{g}(\overline{\nabla}_X \nu, \nu)\nu = 0
$$
所以在超曲面的情况下，[魏恩加滕公式](@entry_id:635565)简化为 $\overline{\nabla}_X \nu = -A_\nu(X)$。

一个经典的例子是 $\mathbb{R}^{m+1}$ 中的[单位球](@entry_id:142558)面 $S^m$ [@problem_id:3071118]。取向外的[单位法向量](@entry_id:178851)场 $\mathbf{n}(p) = p$ (其中 $p$ 是球面上的点，也看作是 $\mathbb{R}^{m+1}$ 中的位置向量)。对于球面上任意[切向量](@entry_id:265494)场 $X$，在 $\mathbb{R}^{m+1}$ 中的导数 $\overline{\nabla}_X \mathbf{n}$ 就是 $X$ 本身。由于 $X$ 是[切向量](@entry_id:265494)，我们有 $\overline{\nabla}_X \mathbf{n} = X$。根据[魏恩加滕公式](@entry_id:635565)的简化版，我们得到 $-A_\mathbf{n}(X) = X$，即 $A_\mathbf{n} = -\mathrm{Id}$。球面的[形状算子](@entry_id:264703)是负单位阵，这意味着在任何方向上，它的主曲率都是 $-1$（根据符号和法向量方向的约定，也可能是 $1$）。

### 第二基本形式的结构

#### [超曲面](@entry_id:159491)的标量[第二基本形式](@entry_id:161454)

对于[余维](@entry_id:273141)为1的超曲面 $M^n \subset \overline{M}^{n+1}$，我们可以选取一个局部[单位法向量](@entry_id:178851)场 $N$。此时，任何[法向量](@entry_id:264185)都可以写成 $N$ 的倍数。因此，[第二基本形式](@entry_id:161454) $B(X,Y)$ 必然可以表示为：
$$
B(X,Y) = h(X,Y) N
$$
其中 $h(X,Y)$ 是一个标量值的函数。这个 $h$ 被称为 **标量[第二基本形式](@entry_id:161454)（scalar second fundamental form）**。从 $B$ 的性质可知，$h$ 也是一个对称的[双线性形式](@entry_id:746794)。

此时，连接[第二基本形式](@entry_id:161454)和形状算子的基本关系 $\overline{g}(B(X,Y), N) = g(A_N(X), Y)$ 变得更加直接 [@problem_id:2997183]：
$$
\overline{g}(h(X,Y)N, N) = h(X,Y) \overline{g}(N,N) = h(X,Y)
$$
于是我们得到：
$$
h(X,Y) = g(A_N(X), Y)
$$
这表明，标量[第二基本形式](@entry_id:161454) $h$ 就是形状算子 $A_N$ 作为[双线性形式的矩阵表示](@entry_id:149415)。如果我们选取一个局部正交标架 $\{e_i\}$，那么 $h$ 的分量 $h_{ij} = h(e_i, e_j)$ 就等于 $g(A_N(e_i), e_j)$，这正是形状算子矩阵的 $(j,i)$ 元（或在自伴情况下为 $(i,j)$ 元）。例如，如果在一个正交标架下 $S$ 的矩阵为 $S_{mat}$，那么对于向量 $X_p$ 和 $Y_p$，其[坐标向量](@entry_id:153319)分别为 $[X_p]$ 和 $[Y_p]$，我们有 $h(X_p, Y_p) = ([Y_p])^T S_{mat} [X_p]$。

#### 高[余维](@entry_id:273141)情形

当子流形 $M^n$ 的[余维](@entry_id:273141) $k > 1$ 时，情况更为复杂 [@problem_id:2997217]。[法丛](@entry_id:272447) $NM$ 是一个 $k$ 维向量丛。我们可以选取一个局部的正交法标架 $\{e_\alpha\}_{\alpha=1}^k$。在每一点，$B(X,Y)$ 作为法空间中的一个向量，可以被这个标架[唯一分解](@entry_id:152313)：
$$
B(X,Y) = \sum_{\alpha=1}^k \overline{g}(B(X,Y), e_\alpha) e_\alpha
$$
我们可以定义 $k$ 个标量[第二基本形式](@entry_id:161454) $h^\alpha(X,Y) := \overline{g}(B(X,Y), e_\alpha)$。于是，向量值的[第二基本形式](@entry_id:161454) $B$ 可以写成：
$$
B = \sum_{\alpha=1}^k h^\alpha \otimes e_\alpha
$$
每个 $h^\alpha$ 都是一个对称的 $(0,2)$-张量。然而，这组 $\{h^\alpha\}$ 依赖于法标架的选择。如果更换另一组正交法标架 $\{\tilde{e}_\alpha\}$，它与原标架通过一个[正交矩阵](@entry_id:169220) $R(x)=(R_{\alpha\beta}(x))$ 相关联，即 $\tilde{e}_\alpha = \sum_\beta R_{\alpha\beta} e_\beta$，那么新的标量形式 $\tilde{h}^\alpha$ 与旧的标量形式 $h^\beta$ 的关系是：
$$
\tilde{h}^\alpha_{ij} = \sum_{\beta=1}^k R_{\alpha\beta} h^\beta_{ij}
$$
这意味着，在高[余维](@entry_id:273141)情形下，并没有一个唯一的标量[第二基本形式](@entry_id:161454)，而是一个在法标架旋转下[线性变换](@entry_id:149133)的集合。几何上不变的量是这些形式所张成的[线性空间](@entry_id:151108)。

### [高斯-科达齐方程](@entry_id:159376)一瞥

高斯公式和[魏恩加滕公式](@entry_id:635565)是子流形微分几何的“运动学”方程。它们还必须满足一组“动力学”的约束，即所谓的 **高斯-科达齐（Gauss-Codazzi）方程**，这些方程是[可积性](@entry_id:142415)条件。它们本质上来源于外围空间曲率张量 $\overline{R}$ 在切向和法向的分解。

其中，**科达齐-迈纳尔迪（Codazzi-Mainardi）方程** 来自于对 $\overline{R}(X,Y)Z$ 取法向分量。它建立了第二基本形式的[协变导数](@entry_id:152476) $(\nabla B)$ 与外围曲率之间的关系。一个简化的说法是 [@problem_id:2997574]：
$$
(\tilde{\nabla}_X B)(Y,Z) - (\tilde{\nabla}_Y B)(X,Z) = (\overline{R}(X,Y)Z)^\perp
$$
其中 $\tilde{\nabla}$ 是在[张量丛](@entry_id:203012)上诱导的联络。

这个方程的右边，$(\overline{R}(X,Y)Z)^\perp$，是外围[曲率张量](@entry_id:181383)的法向分量。如果外围空间是一个[常曲率空间](@entry_id:161841)（如欧氏空间 $\mathbb{R}^n$、球面 $S^n$ 或[双曲空间](@entry_id:268092) $\mathbb{H}^n$），那么对于任何切向量 $X,Y,Z$，$\overline{R}(X,Y)Z$ 总是位于由 $X,Y,Z$ 张成的[切空间](@entry_id:199137)内，因此它的法向分量为零。在这种特殊且重要的情况下，[科达齐方程](@entry_id:635135)简化为 $(\tilde{\nabla}_X B)(Y,Z) = (\tilde{\nabla}_Y B)(X,Z)$，表明第二基本形式的[协变导数](@entry_id:152476)是对称的。

然而，在一般弯曲的外围空间中，$(\overline{R}(X,Y)Z)^\perp$ 不一定为零 [@problem_id:2997199]。例如，在[积流形](@entry_id:270208) $S^2(\kappa_1) \times S^2(\kappa_2)$ 中，由于两个因子的曲率不同，[流形](@entry_id:153038)本身不是[常曲率空间](@entry_id:161841)。对于嵌入其中的对角[子流形](@entry_id:159439) $\Sigma = \{(p,p)\}$, 我们可以计算出 $(\overline{R}(X,Y)Z)^\perp$ 是非零的。这个非零项是理解[子流形几何](@entry_id:189265)如何受外围空间曲率变化影响的关键，它为[科达齐方程](@entry_id:635135)提供了一个非平凡的[源项](@entry_id:269111)，从而对第二基本形式的性质施加了更强的约束。

总而言之，[高斯和](@entry_id:196588)[魏恩加滕公式](@entry_id:635565)通过引入第二基本形式和[形状算子](@entry_id:264703)，为我们提供了一套强大的工具，用以[降维](@entry_id:142982)和分析[子流形](@entry_id:159439)的几何。它们不仅揭示了[内蕴几何与外在几何](@entry_id:161677)的深刻联系，也为更高层次的曲率关系，如[高斯-科达齐方程](@entry_id:159376)，奠定了基础。