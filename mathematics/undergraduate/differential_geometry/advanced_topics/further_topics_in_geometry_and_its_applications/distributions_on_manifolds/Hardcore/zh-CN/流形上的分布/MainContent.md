## 引言
在微分几何与物理学的广阔天地中，我们常常需要描述那些在每一点都受到方向限制的系统，例如力学中的非完整约束或几何中的特定曲面族。流形上的**分布**理论为这一类问题提供了严谨而强大的数学语言。它允许我们系统地研究流形上“平面场”的性质，但一个核心问题随之而来：这些在各点局部定义的平面，能否光滑地“缝合”成一个完整的子流形族？这便是**可积性**问题，也是理解许多几何与物理现象的关键。

本文将深入探讨分布理论的核心。在第一章**“原理与机制”**中，我们将从基本定义出发，建立分布的数学框架，并引入解决可积性问题的核心武器——**Frobenius定理**，揭示代数结构（李括号）与几何结构（积分流形）之间的深刻联系。接下来的第二章**“应用与跨学科联系”**将展示这一理论的广泛影响力，从描述控制系统的运动可能性，到解释哈密顿力学的可积性，再到为偏微分方程提供几何视角。最后，在第三章**“动手实践”**中，你将通过具体的计算练习，亲手检验分布的可积性，将抽象的理论转化为切实的技能。通过这三章的学习，你将掌握分析流形上局部几何结构的基本工具，并领会其在多个科学领域中的应用价值。

## 原理与机制

在对光滑流形的研究中，我们常常不仅关心整个流形，也对其上特定方向的结构感兴趣。例如，一个力学系统的运动轨迹可能被限制在相空间的某个子集上，或者一个偏微分方程的解可能定义了流形中的一系列曲面。**分布（Distribution）** 的概念为这些几何结构提供了统一而严谨的数学框架。它允许我们在流形的每一点上指定一个切空间的子空间，从而定义一个“方向场”或“平面场”。本章将深入探讨分布的定义、其核心性质——**可积性（integrability）**，以及判断可积性的关键工具——**Frobenius 定理**。

### 分布的定义与表示

一个光滑流形 $M$ 上的**$k$ 维分布** $\mathcal{D}$ 是对 $M$ 上每一点 $p$ 指定其切空间 $T_pM$ 的一个 $k$ 维线性子空间 $\mathcal{D}_p$ 的规则，并且这种指定是光滑的。换言之，分布是切丛 $TM$ 的一个 $k$ 维**子丛**。分布的维数 $k$ 也被称为其**秩（rank）**。

在实践中，我们通常通过以下两种方式来具体描述一个分布：

1.  **由向量场张成（Spanned by Vector Fields）**：
    一个 $k$ 维分布 $\mathcal{D}$ 可以由 $k$ 个在每点都线性无关的光滑向量场 $X_1, X_2, \dots, X_k$ 张成。在任意点 $p \in M$，分布的子空间 $\mathcal{D}_p$ 就是由这些向量场在该点的值 $\{X_1(p), X_2(p), \dots, X_k(p)\}$ 所张成的向量空间：
    $$ \mathcal{D}_p = \text{span}\{X_1(p), X_2(p), \dots, X_k(p)\} $$
    例如，在 $\mathbb{R}^3$ 上，我们可以考虑由向量场 $V_1 = \frac{\partial}{\partial x}$ 和 $V_2 = \frac{\partial}{\partial y} + x^2 \frac{\partial}{\partial z}$ 张成的二维分布 [@problem_id:1635903]。在每一点 $p=(x,y,z)$，这个分布 $\mathcal{D}_p$ 就是 $T_p\mathbb{R}^3$ 中由向量 $(1,0,0)$ 和 $(0,1,x^2)$ 张成的平面。

2.  **由微分形式的核定义（Defined by the Kernel of 1-forms）**：
    一个**余维（codimension）**为 $m$ 的分布（即秩为 $n-m$，其中 $n$ 是流形的维数）可以被定义为 $m$ 个在每点都线性无关的光滑1-形式 $\omega^1, \dots, \omega^m$ 的公共核。即，在每一点 $p \in M$，一个切向量 $v \in T_pM$ 属于 $\mathcal{D}_p$ 当且仅当所有这些1-形式作用于它都为零：
    $$ \mathcal{D}_p = \{v \in T_pM \mid \omega^1_p(v) = 0, \dots, \omega^m_p(v) = 0\} = \bigcap_{i=1}^{m} \ker(\omega^i_p) $$
    一个特别重要的情形是余维为1的分布。在 $n$ 维流形上，一个秩为 $n-1$ 的分布可以（至少在局部上）由一个处处非零的1-形式 $\omega$ 的核来定义，即 $\mathcal{D} = \ker \omega$。例如，在 $\mathbb{R}^3$ 的开集 $U = \{(x,y,z) \mid x>0, y>0, z>0\}$ 上，1-形式 $\omega = yz \, dx + xz \, dy + xy \, dz$ 定义了一个二维分布 $\mathcal{D}$，其中 $\mathcal{D}_p = \{v \in T_pU \mid \omega_p(v) = 0\}$ [@problem_id:1635879]。

### 核心问题：可积性

一旦我们定义了一个分布，一个自然的几何问题随之产生：我们能否将这些在各点指定的 $k$ 维切子空间“缝合”起来，形成一系列 $k$ 维的子流形？

这引出了**积分流形（integral submanifold）**的概念。流形 $M$ 的一个 $k$ 维子流形 $S$ 被称为分布 $\mathcal{D}$ 的一个积分流形，如果对于 $S$ 上的任意一点 $p$，其切空间 $T_pS$ 恰好是分布在该点指定的子空间，即 $T_pS = \mathcal{D}_p$。

如果一个分布在每一点附近都存在一个通过该点的积分流形，我们就称这个分布是**可积的（integrable）**。一个可积分布将整个流形剖分成一族互不相交的、连通的、极大的积分流形。这个剖分被称为**叶状结构（foliation）**，而这些极大的积分流形则被称为**叶（leaves）**。

例如，在 $\mathbb{R}^2 \setminus \{(0,0)\}$ 上，由向量场 $X = -y \frac{\partial}{\partial x} + x \frac{\partial}{\partial y}$ 张成的1维分布是可积的 [@problem_id:1635911]。这个向量场在每一点都与从原点出发的位置向量正交，因此它总是切于以原点为中心的圆。积分曲线满足 $\dot{x}=-y, \dot{y}=x$，其解是 $x(t) = R\cos(t+t_0), y(t) = R\sin(t+t_0)$。这些积分曲线描绘了以原点为中心的圆。因此，这个分布的叶就是所有以原点为中心的同心圆。

### Frobenius 定理：从代数到几何的桥梁

如何判断一个分布是否可积？直接去寻找积分流形通常需要解复杂的偏微分方程组，这非常困难。幸运的是，Frobenius 定理提供了一个等价的、纯代数的判别方法。这个方法的关键在于**李括号（Lie bracket）**。

对于两个向量场 $X$ 和 $Y$，它们的李括号 $[X, Y] = XY - YX$ 衡量了沿着这两个向量场的流（flow）交换的非对易性。从几何上看，从一点 $p$ 出发，先沿 $X$ 的流走一小段时间，再沿 $Y$ 的流走同样长的时间，与先沿 $Y$ 再沿 $X$ 的路径终点并不相同。李括号 $[X, Y]$ 的方向正是这两个终点之间的偏差方向。

如果一个分布 $\mathcal{D}$ 是可积的，其积分流形 $S$ 的切空间在每一点都由 $\mathcal{D}$ 给出。由于 $S$ 是一个子流形，任何属于 $S$ 切丛的向量场 $X, Y$ 的李括号 $[X, Y]$ 也必须仍然是 $S$ 的切向量场。这意味着 $[X,Y]$ 必须仍在分布 $\mathcal{D}$ 中。这个观察启发了**对合分布（involutive distribution）**的定义：

一个分布 $\mathcal{D}$ 被称为**对合的**，如果对于任意两个属于 $\mathcal{D}$ 的向量场（即 $\mathcal{D}$ 的任意两个截面） $X$ 和 $Y$，它们的李括号 $[X, Y]$ 仍然是 $\mathcal{D}$ 的一个截面。

**Frobenius 定理（李括号形式）**
一个光滑分布是可积的，当且仅当它是对合的。

这个定理是微分几何的基石之一，它将一个解析问题（寻找积分流形）转化为了一个代数问题（检验李括号的封闭性）。

#### 应用对合性检验

要检验一个由向量场 $\{X_1, \dots, X_k\}$ 张成的分布 $\mathcal{D}$ 是否是对合的，我们只需计算所有基向量场两两之间的李括号 $[X_i, X_j]$，并检查结果是否能表示为基向量场的线性组合。也就是说，是否存在光滑函数 $c_{ij}^l$ 使得：
$$ [X_i, X_j](p) = \sum_{l=1}^k c_{ij}^l(p) X_l(p) \quad \text{对所有 } i,j \text{ 和所有 } p \in M $$

**平凡的可积情形：一维分布**
任何一维分布 $\mathcal{D} = \text{span}\{X\}$ 都是可积的。这是因为任何属于该分布的两个向量场都可以写成 $Y_1 = fX$ 和 $Y_2 = gX$ 的形式，其中 $f, g$ 是光滑函数。利用李括号的性质 $[X, fY] = f[X,Y] + (Xf)Y$，我们有：
$$ [Y_1, Y_2] = [fX, gX] = f[X, gX] - (gXf)X = f(g[X,X] + (Xg)X) - (gXf)X $$
由于 $[X,X]=0$，上式简化为：
$$ [Y_1, Y_2] = (f(Xg) - g(Xf))X $$
这个结果显然仍在 $\text{span}\{X\}$ 中，因此分布是对合的，从而也是可积的 [@problem_id:1635889]。

**不可积分布的例子**
现在我们来看一个不可积的例子。考虑 $\mathbb{R}^3$ 上由 $V_1 = \frac{\partial}{\partial x}$ 和 $V_2 = \frac{\partial}{\partial y} + x^2 \frac{\partial}{\partial z}$ 张成的二维分布 $\mathcal{D}$ [@problem_id:1635903]。我们计算李括号：
$$ [V_1, V_2] = \left[\frac{\partial}{\partial x}, \frac{\partial}{\partial y} + x^2 \frac{\partial}{\partial z}\right] = \left[\frac{\partial}{\partial x}, \frac{\partial}{\partial y}\right] + \left[\frac{\partial}{\partial x}, x^2 \frac{\partial}{\partial z}\right] $$
由于坐标向量场对易，第一项为零。对于第二项，我们使用性质 $[X, fY] = (Xf)Y + f[X,Y]$：
$$ \left[\frac{\partial}{\partial x}, x^2 \frac{\partial}{\partial z}\right] = \left(\frac{\partial}{\partial x}(x^2)\right)\frac{\partial}{\partial z} + x^2\left[\frac{\partial}{\partial x}, \frac{\partial}{\partial z}\right] = 2x \frac{\partial}{\partial z} $$
因此，$[V_1, V_2] = 2x \frac{\partial}{\partial z}$。现在的问题是，这个新的向量场是否位于分布 $\mathcal{D}$ 中？即，是否存在函数 $a(x,y,z)$ 和 $b(x,y,z)$ 使得 $2x \frac{\partial}{\partial z} = aV_1 + bV_2$？
$$ 2x \frac{\partial}{\partial z} = a(x,y,z) \frac{\partial}{\partial x} + b(x,y,z) \left(\frac{\partial}{\partial y} + x^2 \frac{\partial}{\partial z}\right) $$
比较 $\frac{\partial}{\partial x}, \frac{\partial}{\partial y}, \frac{\partial}{\partial z}$ 的系数，我们得到一个方程组：
$$ a=0, \quad b=0, \quad bx^2=2x $$
当 $x \neq 0$ 时，这个系统是矛盾的。因此，李括号 $[V_1, V_2]$ “跳出”了由 $V_1, V_2$ 张成的平面。分布不是对合的，故不可积。另一个类似的例子见 [@problem_id:1635913]。

**最大不可积分布：切触结构**
在某些情况下，李括号不仅跳出原分布，而且会生成所有“缺失”的方向。这类分布被称为“最大不可积”的。一个典型的例子是 $\mathbb{R}^3$ 上的**Heisenberg 分布**，它可以由 $X = \frac{\partial}{\partial x} - \frac{y}{2} \frac{\partial}{\partial z}$ 和 $Y = \frac{\partial}{\partial y} + \frac{x}{2} \frac{\partial}{\partial z}$ 张成 [@problem_id:1635925]。它们的李括号是：
$$ [X, Y] = \frac{\partial}{\partial z} $$
在任何一点，$X, Y, [X,Y]$ 三个向量在坐标基下的分量矩阵为：
$$ \begin{pmatrix} 1  & 0 & 0 \\ 0  & 1 & 0 \\ -y/2 & x/2 & 1 \end{pmatrix} $$
该矩阵的行列式恒为1，说明这三个向量在每一点都是线性无关的。这意味着由 $X, Y$ 张成的二维分布 $\mathcal{D}$ 与它们的李括号一起，张成了整个三维切空间。由 $\mathcal{D}$ 及其李括号张成的新分布 $\mathcal{D}^{(1)} = \text{span}\{X, Y, [X,Y]\}$ 被称为 $\mathcal{D}$ 的**导分布（derived distribution）**。在此例中，$\mathcal{D}^{(1)}$ 的秩为3。
这种在 $(2n+1)$ 维流形上的、秩为 $2n$ 的、最大不可积的分布被称为**切触结构（contact structure）**，在几何光学和力学中有重要应用 [@problem_id:1635901]。

### Frobenius 定理的其他表述

除了李括号，Frobenius 定理还有两种非常有用的等价表述。

**1. 局部坐标形式（法形式）**
这可以说是 Frobenius 定理最深刻的几何结论。它断言，任何可积的 $k$ 维分布在局部看起来都像标准的坐标平面。

**Frobenius 定理（局部坐标形式）**
一个秩为 $k$ 的分布 $\mathcal{D}$ 是可积的，当且仅当在每一点 $p$ 的邻域内，都存在一个局部坐标系 $(u_1, \dots, u_k, w_1, \dots, w_{n-k})$，使得分布 $\mathcal{D}$ 在该坐标系下由前 $k$ 个坐标向量场张成：
$$ \mathcal{D} = \text{span}\left\{\frac{\partial}{\partial u_1}, \dots, \frac{\partial}{\partial u_k}\right\} $$
在这个“平坦”坐标系中，积分流形的叶就是由 $w_j = \text{constant}$ 给出的 $k$ 维平面 [@problem_id:1635892]。这表明，尽管一个可积分布的叶在整体上可能是弯曲的复杂曲面（例如球面），但在足够小的尺度下，它总是可以被“拉直”的。

**2. 微分形式形式（针对余维1）**
对于余维为1的分布 $\mathcal{D} = \ker \omega$，其中 $\omega$ 是一个处处非零的1-形式，Frobenius 定理有一个特别简洁的表述。

**Frobenius 定理（微分形式形式）**
由 $\mathcal{D} = \ker \omega$ 定义的分布是可积的，当且仅当：
$$ \omega \wedge d\omega = 0 $$
这里的 $d\omega$ 是 $\omega$ 的外微分。这个条件的直观解释是：如果 $X, Y$ 是分布中的任意两个向量场，即 $\omega(X)=0, \omega(Y)=0$，那么我们需要 $\omega([X,Y])=0$。根据 Cartan 公式 $d\omega(X,Y) = X(\omega(Y)) - Y(\omega(X)) - \omega([X,Y])$，这等价于要求 $d\omega(X,Y)=0$。条件 $\omega \wedge d\omega = 0$ 正是保证了对于所有属于分布的向量场对， $d\omega$ 的作用为零。

一个特别简单的情况是当 $d\omega=0$ 时（即 $\omega$ 是一个**闭形式**）。此时，$\omega \wedge d\omega = \omega \wedge 0 = 0$ 显然成立，因此分布必定可积。更进一步，如果流形是单连通的，由 Poincaré 引理可知，闭形式必为**恰当形式**，即存在一个函数 $f$ 使得 $\omega = df$。在这种情况下，分布 $\mathcal{D} = \ker(df)$ 的积分流形就是函数 $f$ 的水平集 $\{p \in M \mid f(p) = \text{constant}\}$。

例如，在 $\mathbb{R}^3$ 的正卦限中，考虑由 $\omega = yz \, dx + xz \, dy + xy \, dz$ 定义的分布 [@problem_id:1635879]。直接计算可得 $d\omega = 0$。因此，$\omega \wedge d\omega = 0$，分布是可积的。事实上，我们不难发现 $\omega = d(xyz)$。所以，这个分布的叶就是由方程 $xyz = c$（$c$ 为正常数）定义的一族曲面。

### 特例：李群上的分布

分布理论在李群的研究中扮演着特殊而重要的角色。在一个李群 $G$ 上，我们可以通过其在单位元 $e$ 处的切空间——即李代数 $\mathfrak{g} = T_eG$ ——来定义一种特殊的分布。

任取李代数 $\mathfrak{g}$ 的一个子空间 $\mathfrak{h}$，我们可以通过左平移将其扩展为 $G$ 上的一个分布 $\mathcal{D}$，定义为 $\mathcal{D}_g = L_{g*}(\mathfrak{h})$，其中 $L_{g*}$ 是由左平移 $L_g: x \mapsto gx$ 诱导的切映射。这样的分布被称为**左不变分布**。

关于这类分布的可积性，有一个非常优美的结论：一个左不变分布 $\mathcal{D}$ 是可积的，当且仅当其在单位元处的子空间 $\mathfrak{h}$ 是 $\mathfrak{g}$ 的一个**子代数**（即 $\mathfrak{h}$ 在李代数的括号运算下是封闭的）。

考虑李群 $GL(2, \mathbb{R})$，其李代数是所有 $2 \times 2$ 实矩阵构成的空间 $M_2(\mathbb{R})$，其李括号就是矩阵的对易子 $[A,B] = AB-BA$。设 $\mathcal{D}$ 是由对应于矩阵 $A = \begin{pmatrix} 0  & 1 \\ 0  & 0 \end{pmatrix}$ 和 $B = \begin{pmatrix} 0  & 0 \\ 1  & 0 \end{pmatrix}$ 的左不变向量场张成的分布 [@problem_id:1635922]。要判断其可积性，我们只需检查子空间 $\mathfrak{h} = \text{span}\{A, B\}$ 是否为子代数。计算它们的对易子：
$$ [A,B] = AB - BA = \begin{pmatrix} 1  & 0 \\ 0  & 0 \end{pmatrix} - \begin{pmatrix} 0  & 0 \\ 0  & 1 \end{pmatrix} = \begin{pmatrix} 1  & 0 \\ 0  & -1 \end{pmatrix} =: H $$
由于 $H$ 无法表示为 $A$ 和 $B$ 的线性组合，$\mathfrak{h}$ 不是一个子代数，因此分布 $\mathcal{D}$ 不是可积的。

我们可以继续计算括号，直到获得一个封闭的子代数。这个过程生成的子代数对应于原分布的**对合闭包（involutive closure）**，即包含原分布的最小可积分布。在此例中，进一步计算可知 $[H,A]=2A$ 和 $[H,B]=-2B$。因此，由 $A,B$ 生成的李代数是 $\text{span}\{A, B, H\}$，它同构于 $\mathfrak{sl}(2, \mathbb{R})$。这个三维子代数对应于一个秩为3的可积分布，即 $\mathcal{D}$ 的对合闭包。

总结而言，分布理论为研究流形上的局部几何结构提供了强有力的工具。Frobenius 定理以其多种形式，建立了切空间上的代数条件（对合性）与流形中子流形的存在性（可积性）之间的深刻联系，是现代微分几何不可或缺的一部分。