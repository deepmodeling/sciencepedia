## 引言
在[微分几何](@entry_id:145818)领域，理解一个空间如何映射到另一个空间是研究的核心。光滑流形之间的[光滑映射](@entry_id:203730)通常是[非线性](@entry_id:637147)的复杂对象，直接分析它们颇具挑战。为了解决这一问题，我们需要一个工具，能够将映射在局部的复杂行为“线性化”，从而用强大而成熟的线性代数语言来研究它。这个关键工具就是[光滑映射](@entry_id:203730)的**[微分](@entry_id:158718)**（differential），也称**[前推](@entry_id:158718)**（pushforward）。

本文将系统地引导读者深入理解[微分](@entry_id:158718)这一基石性概念。在第一章**“原理与机制”**中，我们将从[微分](@entry_id:158718)的严格定义出发，探讨其作为[最佳线性逼近](@entry_id:164642)的本质，并揭示其在[局部坐标](@entry_id:181200)下的具体形式——[雅可比矩阵](@entry_id:264467)，同时阐明其基本性质如链式法则。随后的第二章**“应用与[交叉](@entry_id:147634)学科联系”**将展示[微分](@entry_id:158718)的强大威力，探索其如何定义[子流形](@entry_id:159439)、诱导度量、揭示曲率，以及在[李群论](@entry_id:204663)和几何分析等前沿领域中扮演核心角色。最后，在第三章**“动手实践”**中，我们将通过一系列精心设计的计算和分析问题，将理论知识转化为解决具体几何问题的实践能力。通过这三个章节的学习，读者将掌握[微分](@entry_id:158718)的理论精髓及其在现代几何学中的广泛应用。

## 原理与机制

继前一章介绍光滑流形上的基本概念之后，本章将深入探讨[流形](@entry_id:153038)之间[光滑映射](@entry_id:203730)的核心性质。其关键在于一个被称为**[微分](@entry_id:158718)**（differential）或**[前推](@entry_id:158718)**（pushforward）的[线性映射](@entry_id:185132)。[微分](@entry_id:158718)是联系不同[流形](@entry_id:153038)上[切空间](@entry_id:199137)的基本工具，它将[光滑映射](@entry_id:203730)在某一点的局部行为线性化，从而为我们分析映射如何改变几何结构提供了坚实的代数基础。本章将从其定义出发，展示其在[局部坐标](@entry_id:181200)下的矩阵表示，探讨其基本性质，并最终揭示其在黎曼几何与[李群](@entry_id:137659)理论中的深刻应用。

### [微分](@entry_id:158718)的定义：[最佳线性逼近](@entry_id:164642)

设 $M$ 和 $N$ 是光滑流形，并有[光滑映射](@entry_id:203730) $f: M \to N$。对于 $M$ 中的任意一点 $p$，我们希望找到一个[线性映射](@entry_id:185132)，以最佳方式逼近 $f$ 在 $p$ 点附近的行为。这个线性映射便是 $f$ 在 $p$ 点的[微分](@entry_id:158718)，记作 $d_p f$ 或 $f_{*,p}$，它是一个从 $p$ 点的[切空间](@entry_id:199137) $T_p M$ 到 $f(p)$ 点的切空间 $T_{f(p)} N$ 的线性映射。

$d_p f: T_p M \to T_{f(p)} N$

理解此映射作用的最佳方式有两种等价的视角：一种是通过它对[光滑函数](@entry_id:267124)的作用，另一种是通过它对曲线的作用。

#### 从函数作用的角度定义

我们记得，切向量可以被视为作用在[光滑函数](@entry_id:267124)上的[方向导数](@entry_id:189133)算子。据此，我们可以通过规定 $d_p f$ 的像 $d_p f(v) \in T_{f(p)}N$ 如何作用于 $N$ 上的光滑函数来唯一定义它。

对于任意[切向量](@entry_id:265494) $v \in T_p M$ 和在 $f(p)$ 附近定义的任意光滑实值函数 $\psi: N \to \mathbb{R}$，映射 $d_p f(v)$ 是 $T_{f(p)}N$ 中的一个切向量，其定义为：
$$
(d_p f(v))(\psi) = v(\psi \circ f)
$$
这里，$\psi \circ f$ 是一个从 $M$ 到 $\mathbb{R}$ 的复合光滑函数。这个定义直观地表明，$f$ 将 $v$ 这个[方向导数](@entry_id:189133)算子“[前推](@entry_id:158718)”为一个新的[方向导数](@entry_id:189133)算子，该算子在 $f(p)$ 点作用于函数 $\psi$ 的效果，等同于原始算子 $v$ 在 $p$ 点作用于通过 $f$ “[拉回](@entry_id:160816)”的函数 $\psi \circ f$ 的效果。从这个定义可以验证，$d_p f$ 确实是一个线性映射，即对于任意标量 $a, b \in \mathbb{R}$ 和任意向量 $v_p, w_p \in T_p M$，均满足 $d_p f(a v_p + b w_p) = a d_p f(v_p) + b d_p f(w_p)$。 [@problem_id:1671517]

#### 从曲线作用的角度定义

另一个同样深刻的视角，是将切向量视为通过 $p$ 点的光滑曲线的等价类。一条光滑曲线 $\gamma: (-\epsilon, \epsilon) \to M$ 且满足 $\gamma(0) = p$，其在 $t=0$ 处的速度向量定义了 $T_p M$ 中的一个切向量 $v = [\gamma] = \gamma'(0)$。

[光滑映射](@entry_id:203730) $f$ 可以作用于整条曲线 $\gamma$，生成一条位于 $N$ 中且通过 $f(p)$ 的新曲线 $f \circ \gamma$。这条新曲线在 $t=0$ 处的速度向量，自然地定义了 $T_{f(p)}N$ 中的一个[切向量](@entry_id:265494)。我们就将这个向量定义为 $v$ 在 $d_p f$ 下的像：
$$
d_p f(v) = d_p f([\gamma]) = [f \circ \gamma] = (f \circ \gamma)'(0)
$$
这个定义提供了一种[运动学](@entry_id:173318)上的直观理解：[微分](@entry_id:158718)将一条穿过 $p$ 点的路径的速度向量，映射为该路径在 $f$ 下的像路径在对应点 $f(p)$ 的速度向量。这两种定义是完全等价的，为我们在不同情境下使用[微分](@entry_id:158718)提供了灵活性。

### [局部坐标](@entry_id:181200)下的[微分](@entry_id:158718)：雅可比矩阵

虽然[微分](@entry_id:158718)的抽象定义优雅且强大，但在具体计算中，我们通常需要在[局部坐标](@entry_id:181200)下工作。此时，[微分](@entry_id:158718) $d_p f$ 就表现为一个我们非常熟悉的对象——[雅可比矩阵](@entry_id:264467)。

假设 $(U, x)$ 是 $M$ 在 $p$ 点的一个[坐标卡](@entry_id:262338)，坐标为 $x=(x^1, \dots, x^m)$，它给出了 $T_p M$ 的一组基底 $\left\{\frac{\partial}{\partial x^i}\big|_p\right\}_{i=1}^m$。同样，设 $(V, y)$ 是 $N$ 在 $f(p)$ 点的一个坐标卡，坐标为 $y=(y^1, \dots, y^n)$，它给出了 $T_{f(p)} N$ 的一组基底 $\left\{\frac{\partial}{\partial y^\alpha}\big|_{f(p)}\right\}_{\alpha=1}^n$。

为了确定 $d_p f$ 在这两组基底下的矩阵表示，我们只需计算 $d_p f$ 对 $T_p M$ 的每个[基向量](@entry_id:199546)的作用。根据[微分](@entry_id:158718)从函数作用角度的定义，对于[基向量](@entry_id:199546) $\frac{\partial}{\partial x^i}\big|_p$ 和任意[光滑函数](@entry_id:267124) $\psi: N \to \mathbb{R}$，我们有：
$$
\left(d_p f\left(\frac{\partial}{\partial x^i}\bigg|_p\right)\right)(\psi) = \frac{\partial}{\partial x^i}\bigg|_p (\psi \circ f)
$$
利用多元微积分的[链式法则](@entry_id:190743)，我们可以展开右侧的表达式。在[局部坐标](@entry_id:181200)中，$f$ 被表示为一组函数 $y^\alpha = f^\alpha(x^1, \dots, x^m)$，而 $\psi$ 是 $y$ 坐标的函数。因此，$\psi \circ f = \psi(f^1(x), \dots, f^n(x))$。于是：
$$
\frac{\partial}{\partial x^i}(\psi \circ f)\bigg|_p = \sum_{\alpha=1}^n \frac{\partial \psi}{\partial y^\alpha}\bigg|_{f(p)} \frac{\partial (y^\alpha \circ f)}{\partial x^i}\bigg|_p
$$
另一方面， $d_p f\left(\frac{\partial}{\partial x^i}\big|_p\right)$ 是 $T_{f(p)} N$ 中的一个向量，可以写成[基向量](@entry_id:199546)的[线性组合](@entry_id:154743)，形式为 $\sum_{\alpha=1}^n C_i^\alpha \frac{\partial}{\partial y^\alpha}\big|_{f(p)}$。它作用于 $\psi$ 的结果是：
$$
\left(\sum_{\alpha=1}^n C_i^\alpha \frac{\partial}{\partial y^\alpha}\bigg|_{f(p)}\right)(\psi) = \sum_{\alpha=1}^n C_i^\alpha \frac{\partial \psi}{\partial y^\alpha}\bigg|_{f(p)}
$$
比较两个表达式，由于 $\psi$ 是任意的，我们可以通过选取 $\psi$ 为坐标函数 $y^\beta$ 来分离出系数。此时 $\frac{\partial y^\beta}{\partial y^\alpha} = \delta^\beta_\alpha$ (克罗内克 delta)，我们立即得到系数 $C_i^\beta = \frac{\partial (y^\beta \circ f)}{\partial x^i}\big|_p$。

因此，我们得到了[微分](@entry_id:158718)在[局部坐标](@entry_id:181200)基下的完整表达式 [@problem_id:2994964]：
$$
d_{p}f\left(\frac{\partial}{\partial x^{i}}\bigg|_{p}\right) = \sum_{\alpha=1}^{n}\frac{\partial (y^{\alpha}\circ f)}{\partial x^{i}}(p)\frac{\partial}{\partial y^{\alpha}}\bigg|_{f(p)}
$$
这表明，线性映射 $d_p f$ 的[矩阵表示](@entry_id:146025)，其第 $\alpha$ 行第 $i$ 列的元素正是[偏导数](@entry_id:146280) $\frac{\partial (y^\alpha \circ f)}{\partial x^i}$ 在点 $p$ 的值。这个 $n \times m$ 矩阵正是[光滑映射](@entry_id:203730) $f$ 在[局部坐标](@entry_id:181200)下的**雅可比矩阵**（Jacobian matrix），记作 $J_f(p)$。

例如，对于映射 $F: \mathbb{R}^2 \to \mathbb{R}^2$，$F(x, y) = (x^2y, x - y^2)$，在点 $p=(1, 2)$，其[雅可比矩阵](@entry_id:264467)为：
$$
J_F(1, 2) = \begin{pmatrix} \frac{\partial(x^2y)}{\partial x} & \frac{\partial(x^2y)}{\partial y} \\ \frac{\partial(x-y^2)}{\partial x} & \frac{\partial(x-y^2)}{\partial y} \end{pmatrix}\bigg|_{(1,2)} = \begin{pmatrix} 2xy & x^2 \\ 1 & -2y \end{pmatrix}\bigg|_{(1,2)} = \begin{pmatrix} 4 & 1 \\ 1 & -4 \end{pmatrix}
$$
这个矩阵完全描述了 $dF_p$ 的作用。例如，它可以作用于[切向量](@entry_id:265494) $u_p \in T_p \mathbb{R}^2$ 的分量上，计算出其像 $dF_p(u_p)$ 在 $T_{F(p)}\mathbb{R}^2$ 中的分量 [@problem_id:1671517]。

### [微分](@entry_id:158718)的基本性质

[微分](@entry_id:158718)作为一个基本的构造，遵循一些重要的代数性质，这些性质是其在[几何分析](@entry_id:157700)中如此有用的原因。

#### 恒等[映射的[微](@entry_id:269524)分](@entry_id:158718)

最简单也最基本的情形是恒等映射 $\text{id}_M: M \to M$。对于任意点 $p \in M$，其[微分](@entry_id:158718) $d_p(\text{id}_M)$ 是什么？从定义出发，$d_p(\text{id}_M)(v)(\psi) = v(\psi \circ \text{id}_M) = v(\psi)$。这意味着 $d_p(\text{id}_M)(v)$ 和 $v$ 对任意函数的作用都相同，因此它们是同一个向量。所以，恒等[映射的[微](@entry_id:269524)分](@entry_id:158718)是切空间上的[恒等变换](@entry_id:264671)：
$$
d_p(\text{id}_M) = \text{id}_{T_p M}
$$
在[局部坐标](@entry_id:181200)中，恒等映射 $y^\alpha = x^\alpha$，因此雅可比矩阵的元素为 $\frac{\partial x^\alpha}{\partial x^i} = \delta^\alpha_i$，这正是单位矩阵，与上述结论一致 [@problem_id:1671532]。

#### [链式法则](@entry_id:190743)

[微分](@entry_id:158718)最重要的性质之一是它在映射复合下的表现，即**链式法则** (Chain Rule)。设有两个[光滑映射](@entry_id:203730) $f: M \to N$ 和 $g: N \to P$，它们的复合映射为 $g \circ f: M \to P$。[链式法则](@entry_id:190743)指出，复合[映射的微分](@entry_id:269524)等于各个映射[微分](@entry_id:158718)的复合：
$$
d_p(g \circ f) = d_{f(p)}g \circ d_p f
$$
这个法则在代数上意味着，在[局部坐标](@entry_id:181200)中，复合映射的雅可比矩阵是各个映射雅可比矩阵的乘积：
$$
J_{g \circ f}(p) = J_g(f(p)) \cdot J_f(p)
$$
我们可以通过曲线的视角直观地理解[链式法则](@entry_id:190743) [@problem_id:2994957]。令 $v \in T_p M$ 由曲线 $\gamma$ 代表，即 $v = [\gamma]$。那么 $d_p f(v)$ 由曲线 $f \circ \gamma$ 代表。接着，$d_{f(p)}g$ 作用于 $d_p f(v)$，就是将曲线 $f \circ \gamma$ 再通过 $g$ [前推](@entry_id:158718)，得到的新曲线是 $g \circ (f \circ \gamma) = (g \circ f) \circ \gamma$。这个新曲线所代表的切向量正是 $d_p(g \circ f)(v)$。这个过程清晰地展示了 $d_p(g \circ f)$ 将 $v$ 一步映射的结果，等同于先经 $d_p f$ 再经 $d_{f(p)}g$ 两步映射的结果。

### [微分](@entry_id:158718)的几何应用

[微分](@entry_id:158718)不仅仅是一个抽象的代数工具，它在描述和分析映射如何与[流形](@entry_id:153038)的几何结构相互作用方面扮演着核心角色。

#### [微分](@entry_id:158718)与对偶性：[拉回](@entry_id:160816)

[微分](@entry_id:158718)将[切向量](@entry_id:265494)从一个[流形](@entry_id:153038)“[前推](@entry_id:158718)”到另一个[流形](@entry_id:153038)。与此对偶地，它也允许我们将余切向量（covectors，也即1-形式）从目标[流形](@entry_id:153038)“[拉回](@entry_id:160816)”（pull back）到源[流形](@entry_id:153038)。

设 $\omega$ 是 $N$ 上的一个1-形式，对于每个点 $q \in N$，$\omega_q$ 是 $T_q N$ 上的一个[线性泛函](@entry_id:276136)。$f$ 的**[拉回](@entry_id:160816)1-形式** $f^*\omega$ 是 $M$ 上的一个[1-形式](@entry_id:270392)，其在点 $p \in M$ 对向量 $v \in T_p M$ 的作用定义为：
$$
(f^*\omega)_p(v) = \omega_{f(p)}(d_p f(v))
$$
这个定义完美地体现了[前推与拉回](@entry_id:181877)的对偶关系：为了计算[拉回](@entry_id:160816)的1-形式对向量 $v$ 的值，我们先将向量 $v$ [前推](@entry_id:158718)到目标[流形](@entry_id:153038)的切空间，然后再让原始的[1-形式](@entry_id:270392)作用于这个[前推](@entry_id:158718)后的向量。这个关系是计算[流形](@entry_id:153038)上积分和理解[辛几何](@entry_id:160783)、[德拉姆上同调](@entry_id:158673)等高级概念的基础 [@problem_id:1671477]。

当目标[流形](@entry_id:153038)是 $\mathbb{R}$ 时，即 $f$ 是一个光滑实值函数 $f: M \to \mathbb{R}$，它的[微分](@entry_id:158718) $df$ 本身就是一个1-形式。在这种情况下，$d_p f: T_p M \to T_{f(p)}\mathbb{R} \cong \mathbb{R}$，这意味着 $d_p f$ 是一个从 $T_p M$ 到实数的线性映射，这正是 $T_p^* M$ 中余切向量的定义。在[欧氏空间](@entry_id:138052) $\mathbb{R}^n$ 中，这个1-形式 $df_p$ 的作用可以通过[梯度向量](@entry_id:141180) $\nabla f(p)$ 的[点积](@entry_id:149019)来实现：$df_p(v) = \nabla f(p) \cdot v$ [@problem_id:1671472]。

#### [拉回度量](@entry_id:161465)与等距

这个[拉回](@entry_id:160816)的概念可以从1-形式推广到更复杂的张量。对于[黎曼几何](@entry_id:160508)而言，最重要的应用是[拉回](@entry_id:160816)[黎曼度量](@entry_id:754359)。设 $(N, h)$ 是一个黎曼流形，其中 $h$ 是 $N$ 上的[黎曼度量张量](@entry_id:198086)。我们可以通过[光滑映射](@entry_id:203730) $f: M \to N$ 将度量 $h$ [拉回](@entry_id:160816)到 $M$ 上，定义一个称为**[拉回度量](@entry_id:161465)** (pullback metric) 的 $(0,2)$-张量 $f^*h$：
$$
(f^*h)_p(u, v) = h_{f(p)}(d_p f(u), d_p f(v))
$$
对于任意 $p \in M$ 和 $u, v \in T_p M$。这个公式的含义是，要测量 $M$ 上 $p$ 点的两个[切向量](@entry_id:265494) $u$ 和 $v$ 之间的[内积](@entry_id:158127)，我们首先用[微分](@entry_id:158718) $d_p f$ 将它们[前推](@entry_id:158718)到 $N$ 上的 $f(p)$ 点，然后在那里使用 $N$ 的度量 $h$ 来测量它们的[内积](@entry_id:158127)。如果对于所有 $p$， $d_p f$ 都是单射的（即 $f$ 是一个浸入），那么 $f^*h$ 就成为 $M$ 上的一个[黎曼度量](@entry_id:754359)，称为**诱导度量**（induced metric）。

一个经典的例子是球面 $S^2_R \subset \mathbb{R}^3$ 的度量。通过包含映射 $i: S^2_R \hookrightarrow \mathbb{R}^3$，我们可以将 $\mathbb{R}^3$ 的标准欧氏度量[拉回](@entry_id:160816)到球面上，从而得到球面上的标[准圆](@entry_id:175119)度量。在球坐标 $(\theta, \phi)$ 下，计算表明诱导度量的矩阵是对角的，其[行列式](@entry_id:142978)为 $R^4 \sin^2\theta$，这正是球面上我们熟悉面积元的核心部分 [@problem_id:2994945]。

如果一个映射 $f: (M, g) \to (N, h)$ 不仅是微分同胚，而且其[拉回度量](@entry_id:161465)恰好等于源[流形](@entry_id:153038)上的原始度量，即 $f^*h = g$，那么这个映射就被称为**等距** (isometry)。根据定义，这等价于说，在每一点 $p \in M$，[微分](@entry_id:158718) $d_p f$ 都保持了向量的[内积](@entry_id:158127)：
$$
h_{f(p)}(d_p f(u), d_p f(v)) = g_p(u, v) \quad \forall u, v \in T_p M
$$
等距是[黎曼几何](@entry_id:160508)中的“[刚性运动](@entry_id:170523)”，它保持了所有与度量相关的几何量，如长度、角度和体积 [@problem_id:1671498]。

#### [临界点](@entry_id:144653)与秩

[微分](@entry_id:158718)的代数性质，如其秩（rank），直接反映了映射的局部几何行为。映射 $f$ 在点 $p$ 的**秩**定义为其[微分](@entry_id:158718) $d_p f$ 的秩，即其像空间 $\text{Im}(d_p f) \subseteq T_{f(p)}N$ 的维数。

*   如果 $d_p f$ 是满射的，则称 $p$ 是 $f$ 的一个**正则点**（regular point）。
*   如果 $d_p f$ 不是满射的，则称 $p$ 是 $f$ 的一个**[临界点](@entry_id:144653)**（critical point）。

根据线性代数中的秩-零度定理，当[流形](@entry_id:153038) $M$ 和 $N$ 维数相同时（$\dim M = \dim N = m$），$d_p f$ 是满射的当且仅当它是单射的，当且仅当它是同构。因此，在这种情况下，$p$ 是[临界点](@entry_id:144653)等价于 $d_p f$ 不是单射的，即其核（kernel） $\ker(d_p f) = \{v \in T_p M \mid d_p f(v) = 0\}$ 是非平凡的。

这意味着，在[临界点](@entry_id:144653) $p$ 处，存在一个非零的[切向量](@entry_id:265494) $v \in T_p M$，其在[前推](@entry_id:158718)作用下被“压扁”为[零向量](@entry_id:156189)。从曲线的角度看，这意味着我们可以找到一条通过 $p$ 的曲线 $\gamma(t)$，其在 $p$ 点的速度向量非零 ($\gamma'(0) = v \neq 0$)，但是其像曲线 $f \circ \gamma(t)$ 在 $f(p)$ 点的速度向量却为零 ($(f \circ \gamma)'(0) = 0$)。这刻画了函数在[临界点](@entry_id:144653)附近发生的“折叠”或“投影”等行为 [@problem_id:2994965]。

### [李群论](@entry_id:204663)中的[微分](@entry_id:158718)

[微分](@entry_id:158718)的概念在[李群](@entry_id:137659)理论中也扮演着至关重要的角色。李群是同时具有群结构和[光滑流形](@entry_id:160799)结构的数学对象，且群运算是光滑的。[李群](@entry_id:137659) $G$ 在其单位元 $e$ 处的[切空间](@entry_id:199137) $T_e G$ 被赋予了一个额外的结构，即李括号 $[\cdot, \cdot]$，使其成为一个**李代数**，记作 $\mathfrak{g}$。

一个基本而深刻的结果是，李群之间的任何光滑同态（homomorphism）$\Phi: G \to H$ 都会诱导其对应[李代数](@entry_id:137954)之间的一个同态。具体来说，$\Phi$ 在单位元处的[微分](@entry_id:158718) $d\Phi_e: \mathfrak{g} \to \mathfrak{h}$ 不仅是一个[线性映射](@entry_id:185132)，它还保持李括号结构：
$$
d\Phi_e([X, Y]) = [d\Phi_e(X), d\Phi_e(Y)] \quad \forall X, Y \in \mathfrak{g}
$$
这说明[微分](@entry_id:158718)完美地联系了李群的全局结构（[群同态](@entry_id:140603)）和[李代数](@entry_id:137954)的局部、线性化结构（代数同态）。对于[矩阵李群](@entry_id:145968)，这个关系尤为具体。例如，考虑由矩阵 $P$ 定义的共轭同态 $\Phi(A) = PAP^{-1}$。其在单位矩阵 $I$ 处的[微分](@entry_id:158718)作用于李代数中的一个元素 $X$ (也是一个矩阵)，结果就是通过 $P$ 进行的共轭变换：$d\Phi_I(X) = PXP^{-1}$。这个性质直接导出了它保持李括号（矩阵交换子）的结论，为研究李[群的[表](@entry_id:140711)示论](@entry_id:137998)和结构理论提供了强大的计算工具 [@problem_id:1671534]。

综上所述，[光滑映射的微分](@entry_id:268823)是微分几何的基石。它将[非线性](@entry_id:637147)的几何问题转化为[切空间](@entry_id:199137)上的线性代数问题，并作为一座桥梁，连接了[流形的拓扑](@entry_id:267834)、几何和[代数结构](@entry_id:137052)。无论是定义诱导度量、刻画等距变换，还是理解李群与[李代数](@entry_id:137954)的关系，[微分](@entry_id:158718)都提供了统一而深刻的视角。