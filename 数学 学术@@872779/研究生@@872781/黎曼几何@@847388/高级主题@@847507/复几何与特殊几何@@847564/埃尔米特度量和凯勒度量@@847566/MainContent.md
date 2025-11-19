## 引言

在复微分几何的宏伟蓝图中，[埃尔米特度量](@entry_id:202337)与凯勒度量扮演着基石性的角色。它们为复流形——那些局部看起来像复欧几里得空间的空间——赋予了丰富的几何结构，使得我们能够运用微积分、拓扑和代数工具进行深入研究。然而，仅仅在复流形上定义一个黎曼度量是不够的；关键的挑战在于如何确保度量结构与固有的复结构和谐共存，从而揭示更深层次的内在联系。本文旨在系统性地解决这一问题，带领读者穿越从基本定义到前沿应用的完整知识体系。

本文将分为三个核心章节，旨在为读者构建一个关于埃尔米特与[凯勒几何](@entry_id:160314)的坚实理论框架。在第一章“原理与机制”中，我们将从[殆复结构](@entry_id:159849)和[可积性](@entry_id:142415)的概念出发，精确定义[埃尔米特度量](@entry_id:202337)，并最终引出核心的[凯勒条件](@entry_id:637291)。我们将探讨该条件的多种等价表述——从联络的平行性到[和乐群](@entry_id:191471)的限制——并揭示其对[霍奇理论](@entry_id:161814)的深远影响。随后的“应用与跨学科联系”一章将理论付诸实践，通过研究[复射影空间](@entry_id:268402)、Calabi-Yau流形等关键范例，展示[凯勒几何](@entry_id:160314)如何与[辛几何](@entry_id:160783)、[代数几何](@entry_id:156300)、理论物理（特别是[弦理论](@entry_id:145688)）和数论等领域交织在一起。最后，在“动手实践”部分，读者将通过具体的计算练习，亲手验证和推导核心概念，从而巩固所学知识。现在，让我们从构建[复流形](@entry_id:159076)上相容几何结构的第一步开始，深入探索其“原理与机制”。

## 原理与机制

在介绍性章节之后，我们现在深入探讨[埃尔米特度量](@entry_id:202337)和凯勒度量的核心原理与机制。本章将从复流形上最基本的几何结构出发，逐步建立一整套丰富的理论，最终揭示[凯勒几何](@entry_id:160314)中代数、分析与拓扑的深刻联系。

### 从实到复：[殆复结构](@entry_id:159849)

在[微分](@entry_id:158718)[流形](@entry_id:153038)上引入[复分析](@entry_id:167282)工具的第一步是赋予其[切空间](@entry_id:199137)一种“[复结构](@entry_id:269128)”。这正是**[殆复结构](@entry_id:159849)（almost complex structure）**的角色。在一个光滑偶数维[流形](@entry_id:153038) $M$（维度为 $2n$）上，一个[殆复结构](@entry_id:159849)是一个光滑的丛同态 $J: TM \to TM$，满足 $J^2 = -\mathrm{Id}_{TM}$，其中 $\mathrm{Id}_{TM}$ 是切丛上的[恒等映射](@entry_id:634191)。这个条件 $J^2 = -\mathrm{Id}$ 模仿了复数 $i$ 的性质 $i^2 = -1$，使得每个切空间 $T_pM$ 都成为一个[复向量空间](@entry_id:264355)，其中 $J$ 充当了与向量相乘的 $i$。

然而，一个[殆复结构](@entry_id:159849)的存在本身并不足以保证[流形](@entry_id:153038)是一个复流形。一个真正的**[复流形](@entry_id:159076)（complex manifold）**要求存在一个图册，其坐标转移映射是全纯的。这引出了一个关键问题：一个给定的[殆复结构](@entry_id:159849) $J$ 是否由这样的一个复[坐标图](@entry_id:156506)册所诱导？如果答案是肯定的，我们称该殆"复结构是**可积的（integrable）**。

[可积性](@entry_id:142415)并非无条件成立。一个[殆复结构](@entry_id:159849)的“[可积性](@entry_id:142415)障碍”可以通过**奈恩胡伊斯张量（Nijenhuis tensor）** $N_J$ 来度量 [@problem_id:2979192]。对于任意向量场 $X, Y$，该张量定义为：
$$
N_{J}(X,Y) = [JX,JY] - J[JX,Y] - J[X,JY] - [X,Y]
$$
利用 $J^2 = -\mathrm{Id}$，这可以写作等价形式：
$$
N_{J}(X,Y) = [JX,JY] - J[JX,Y] - J[X,JY] + J^2[X,Y]
$$
奈恩胡伊斯张量是一个 $(1,2)$-型张量，它衡量了[李括号](@entry_id:636461)运算与 $J$ 运算的可交换性。一个深刻的结果，即**[纽兰德-尼伦伯格定理](@entry_id:158862)（Newlander-Nirenberg theorem）**，断言：一个[殆复结构](@entry_id:159849) $J$ 是可积的（即 $M$ 是一个[复流形](@entry_id:159076)）当且仅当其奈恩胡伊斯张量恒为零，即 $N_J \equiv 0$。因此，并非所有[殆复结构](@entry_id:159849)都是可积的；例如，球面 $S^6$ 就存在不可积的[殆复结构](@entry_id:159849) [@problem_id:2979128]。

无论 $J$ 是否可积，它都允许我们将[切丛](@entry_id:161294)[复化](@entry_id:260775)。[复化](@entry_id:260775)的[切丛](@entry_id:161294) $T_\mathbb{C}M = TM \otimes_\mathbb{R} \mathbb{C}$ 可以根据 $J$ 的作用分解为两个子丛：
$$
T_\mathbb{C}M = T^{1,0}M \oplus T^{0,1}M
$$
其中 $T^{1,0}M$ 和 $T^{0,1}M$ 分别是 $J$ 的[特征值](@entry_id:154894)为 $i$ 和 $-i$ 的特征[子空间](@entry_id:150286)。相应地，[微分形式](@entry_id:146747)的代数也分解为**$(p,q)$-型形式** $\Omega^{p,q}(M)$。外微分算子 $d$ 作用在这些形式上。仅当 $J$ 可积时，$d$ 才能完美地分解为两个算子 $d = \partial + \bar{\partial}$，其中 $\partial: \Omega^{p,q} \to \Omega^{p+1,q}$ 且 $\bar{\partial}: \Omega^{p,q} \to \Omega^{p,q+1}$，并满足 $\partial^2 = 0$, $\bar{\partial}^2 = 0$ 以及 $\partial\bar{\partial} + \bar{\partial}\partial = 0$。在一般的殆复流形上，$\bar{\partial}^2$ 的非零性与奈恩胡伊斯张量的非零性直接相关，因此[算子分解](@entry_id:154443) $d = \partial + \bar{\partial}$ 和相关的[上同调理论](@entry_id:270863)（如[Dolbeault上同调](@entry_id:203257)）是复流形特有的性质 [@problem_id:2979128]。

### 引入度量：埃尔米特[流形](@entry_id:153038)

现在我们在[复流形](@entry_id:159076)上引入黎曼度量的概念。一个与复结构相容的[黎曼度量](@entry_id:754359)被称为**[埃尔米特度量](@entry_id:202337)（Hermitian metric）**。具体而言，在一个复流形 $(M,J)$ 上，一个[黎曼度量](@entry_id:754359) $g$ 如果满足对任意向量场 $X, Y$ 都有 $g(JX,JY) = g(X,Y)$，则称 $g$ 是[埃尔米特度量](@entry_id:202337)。这个条件意味着 $J$ 在每个切空间上都是一个关于度量 $g$ 的[等距同构](@entry_id:273188)。一个[复流形](@entry_id:159076)配上一个[埃尔米特度量](@entry_id:202337) $(M, J, g)$ 称为一个**埃尔米特[流形](@entry_id:153038)（Hermitian manifold）**。

从一个[埃尔米特度量](@entry_id:202337)出发，我们可以定义一个重要的[2-形式](@entry_id:188008)，称为**[基本2-形式](@entry_id:183276)（fundamental 2-form）**或**凯勒形式（Kähler form）**，其定义为：
$$
\omega(X,Y) = g(JX,Y)
$$
这个形式捕捉了度量 $g$ 和复结构 $J$ 之间的相互作用。由于 $g(JX,Y) = g(J(JX),JY) = g(-X,JY) = -g(JY,X) = -\omega(Y,X)$，$\omega$ 是一个反对称的2-形式。一个更为关键的性质是，$\omega$ 总是一个**$(1,1)$-型[实形式](@entry_id:193866)**。这意味着 $\omega$ 在 $T^{1,0}M$ 和 $T^{0,1}M$ 的向量上取值为零，只在混合类型向量对上非零。这个性质甚至在 $J$ 不可积的殆埃尔米特[流形](@entry_id:153038)（almost Hermitian manifold）上也成立，因为验证 $\omega(JX,JY)=\omega(X,Y)$ 仅需使用 $g$ 的[埃尔米特性](@entry_id:141899)质 [@problem_id:2979128]。

有两种等价的视角来理解[埃尔米特度量](@entry_id:202337)，这对于后续的计算至关重要。

一种是从[复向量丛](@entry_id:276223)的观点出发。我们可以将[埃尔米特度量](@entry_id:202337) $h$ 直接定义在 $(1,0)$-型[切丛](@entry_id:161294) $T^{1,0}M$ 上，它是一个光滑变化的正定埃尔米特形式（即满足[共轭对称性](@entry_id:144131) $h(Z,W) = \overline{h(W,Z)}$ 和正定性 $h(Z,Z) > 0$ 的[半双线性形式](@entry_id:154766)）。给定这样的 $h$，我们可以通过取实部的方式恢复出底[流形](@entry_id:153038) $TM$ 上的[黎曼度量](@entry_id:754359) $g$ [@problem_id:2979186]。对于实切向量 $X,Y \in TM$，它们的 $(1,0)$-分量为 $X^{1,0} = \frac{1}{2}(X - iJX)$ 和 $Y^{1,0} = \frac{1}{2}(Y - iJY)$。相关的[黎曼度量](@entry_id:754359) $g$ 和基本形式 $\omega$ 可以通过 $h$ 表示为：
$$
g(X,Y) = 2 \operatorname{Re} h(X^{1,0}, Y^{1,0})
$$
$$
\omega(X,Y) = 2 \operatorname{Im} h(X^{1,0}, Y^{1,0})
$$
这些关系清晰地揭示了 $g$ 和 $\omega$ 分别扮演了埃尔米特形式 $h$ 的“实部”和“虚部”的角色。

另一种视角是[局部坐标](@entry_id:181200)表示。在局部全纯[坐标系](@entry_id:156346) $\{z^1, \dots, z^n\}$ 下，[埃尔米特度量](@entry_id:202337) $h$ 通常被写成作用在 $(1,0)$-型余切向量上的形式：
$$
h = \sum_{i,j=1}^{n} h_{i\bar{j}} dz^i \otimes d\bar{z}^j
$$
其中 $(h_{i\bar{j}})$ 是一个正定[埃尔米特矩阵](@entry_id:155147)，即 $h_{i\bar{j}} = \overline{h_{j\bar{i}}}$。基于上述关系，相关的黎曼度量 $g$ 和基本形式 $\omega$ 在这个[坐标系](@entry_id:156346)下的表达式可以被推导出来 [@problem_id:2979095]：
$$
g = \frac{1}{2} \sum_{i,j=1}^{n} \left( h_{i\bar{j}} dz^i \otimes d\bar{z}^j + h_{j\bar{i}} d\bar{z}^i \otimes dz^j \right)
$$
$$
\omega = \frac{i}{2} \sum_{i,j=1}^{n} h_{i\bar{j}} dz^i \wedge d\bar{z}^j
$$
这些公式是进行具体计算和理论推导的基石。

### [凯勒条件](@entry_id:637291)：几何结构的完美融合

虽然[埃尔米特度量](@entry_id:202337)已经融合了黎曼结构和复结构，但最深刻、性质最丰富的几何出现在一个附加条件满足时。当一个[埃尔米特度量](@entry_id:202337)的[基本2-形式](@entry_id:183276) $\omega$ 是一个**闭形式（closed form）**，即 $d\omega = 0$ 时，我们称该度量为**凯勒度量（Kähler metric）**。一个配有凯勒度量的[复流形](@entry_id:159076)称为**凯勒流形（Kähler manifold）**。

[凯勒条件](@entry_id:637291) $d\omega = 0$ 看似简单，却蕴含着极其丰富的几何内容。它将[流形](@entry_id:153038)的黎曼结构、[复结构](@entry_id:269128)和辛结构（因为 $\omega$ 是一个闭的非退化2-形式）完美地统一起来。这一条件的深刻性体现在它有众多等价的表述，这些表述从不同侧面揭示了[凯勒几何](@entry_id:160314)的内在和谐。

以下是凯勒度量的一些核心等价刻画 [@problem_id:2979199]：

**1. [复结构](@entry_id:269128)与列维-奇维塔联络的相容性**

一个[埃尔米特度量](@entry_id:202337) $g$ 是凯勒度量，当且仅当其[列维-奇维塔联络](@entry_id:161107) $\nabla$ (即唯一无挠且与 $g$ 相容的联络) 也与复结构 $J$ 相容，即 $\nabla J = 0$ [@problem_id:2979128]。这意味着沿着[流形](@entry_id:153038)上任意曲线的平行移动不仅保持向量的长度和夹角（因为 $\nabla g = 0$），也保持其[复结构](@entry_id:269128)（即将 $(1,0)$-向量映为 $(1,0)$-向量）。这个等价性源于一个基本恒等式，它将 $d\omega$ 与 $\nabla J$ 联系起来。对于任意埃尔米特[流形](@entry_id:153038)，我们有：
$$
d\omega(X,Y,Z) = \mathfrak{S} g((\nabla_X J)Y, Z)
$$
其中 $\mathfrak{S}$ 表示对 $X,Y,Z$ 的循环求和。如果 $\nabla J=0$，显然 $d\omega=0$。反过来，若 $d\omega=0$ 且 $J$ 可积（即 $N_J=0$），可以证明 $\nabla J$ 必定为零。值得强调的是，**可积性是关键**：在一般的殆埃尔米特[流形](@entry_id:153038)上，$d\omega=0$ 并不足以推出 $\nabla J=0$ [@problem_id:2979176]。反之，条件 $\nabla J = 0$ 则非常强，它同时蕴含了 $d\omega=0$ 和 $J$ 的可积性 $N_J=0$ [@problem_id:2979176]。

**2. [列维-奇维塔联络](@entry_id:161107)与陈联络的重合**

在埃尔米特[流形](@entry_id:153038)上，除了[列维-奇维塔联络](@entry_id:161107) $\nabla$ 外，还有另一个重要的联络，即**陈联络（Chern connection）**。陈联络是唯一满足以下条件的联络：(1) 与度量 $g$ 相容；(2) 与[复结构](@entry_id:269128) $J$ 相容；(3) 其[挠率张量](@entry_id:204137)的 $(1,1)$-部分为零。在一般的埃尔米特[流形](@entry_id:153038)上，陈联络有挠，而[列维-奇维塔联络](@entry_id:161107)无挠，因此它们通常不相等。

然而，在[凯勒流形](@entry_id:161192)上，情况发生了变化。如上所述，[凯勒条件](@entry_id:637291)等价于 $\nabla J=0$。这意味着列维-奇维塔联络 $\nabla$ 本身已经满足了陈联络的前两个定义属性。此外，$\nabla$ 是[无挠的](@entry_id:161664)，其[挠率张量](@entry_id:204137)为零，自然也满足第三个条件。根据陈联络的唯一性，我们必然得出结论：在[凯勒流形](@entry_id:161192)上，[列维-奇维塔联络](@entry_id:161107)与陈联络完全重合 [@problem_id:2979128] [@problem_id:2979176] [@problem_id:2982200]。反之，如果陈[联络的挠率](@entry_id:192913)张量为零，那么它就同时满足无挠和度量相容性，从而必定是[列维-奇维塔联络](@entry_id:161107)。而陈联络又与 $J$ 相容，故 $\nabla J=0$，这意味着度量是凯勒的 [@problem_id:2979199]。

这一重合在[局部坐标](@entry_id:181200)下表现为克氏符号的对称性。[凯勒条件](@entry_id:637291) $d\omega=0$ 在局部全纯坐标下等价于对称性条件 $\partial_i g_{j\bar{k}} = \partial_j g_{i\bar{k}}$。这个条件恰好能保证陈[联络的挠率](@entry_id:192913)分量 $T^k_{ij} = g^{k\bar{\ell}}(\partial_i g_{j\bar{\ell}} - \partial_j g_{i\bar{\ell}})$ 为零，并使得[列维-奇维塔联络](@entry_id:161107)和陈联络的[联络系数](@entry_id:157618) $(\Gamma)^k_{ij}$ 相等 [@problem_id:2982200]。

**3. [凯勒势](@entry_id:154750)的存在性**

在分析层面，[凯勒条件](@entry_id:637291)等价于度量在局部可以由一个单一的实值函数——**[凯勒势](@entry_id:154750)（Kähler potential）** $\phi$ ——完全决定。具体来说，$d\omega=0$ 且 $\omega$ 是一个 $(1,1)$-型[实形式](@entry_id:193866)，根据代数几何中的 **$\partial\bar{\partial}$-引理**，这意味着在任意点的某个邻域内，存在一个光滑实值函数 $\phi$，使得 $\omega$ 可以表示为 [@problem_id:2979115]：
$$
\omega = i\partial\bar{\partial}\phi
$$
将此表达式与 $\omega = i \sum_{i,j} g_{i\bar{j}} dz^i \wedge d\bar{z}^j$ (这里使用了不同的标准化常数) 进行比较，我们得到度量张量的分量为：
$$
g_{i\bar{j}} = \frac{\partial^2 \phi}{\partial z^i \partial \bar{z}^j}
$$
[凯勒势](@entry_id:154750)并非唯一。如果 $\phi$ 是一个[凯勒势](@entry_id:154750)，那么 $\phi + f + \bar{f}$ 也是一个[凯勒势](@entry_id:154750)，其中 $f$ 是任意一个局部全纯函数。这意味着两个[凯勒势](@entry_id:154750)之差是一个**多重调和函数（pluriharmonic function）**，即满足 $\partial\bar{\partial}(\phi_1-\phi_2)=0$ 的函数 [@problem_id:2979115]。反过来，如果一个实值函数 $\phi$ 的复Hessian矩阵 $(\partial_i\partial_{\bar{j}}\phi)$ 处处正定，那么它就定义了一个局部的凯勒度量。这类函数被称为**严格多重[次调和函数](@entry_id:191036)（strictly plurisubharmonic function）** [@problem_id:2979115]。

**4. [和乐群](@entry_id:191471)的限制**

从几何的角度看，[凯勒条件](@entry_id:637291)最深刻的体现是在[流形](@entry_id:153038)的**[和乐群](@entry_id:191471)（holonomy group）**上。[黎曼度量](@entry_id:754359) $g$ 的[和乐群](@entry_id:191471) $\mathrm{Hol}(g)$ 刻画了沿[流形](@entry_id:153038)中闭环平行移动如何旋转[切空间](@entry_id:199137)。由于[列维-奇维塔联络](@entry_id:161107)总是与度量相容，和乐群总是包含在[正交群](@entry_id:152531) $\mathrm{SO}(2n)$ 中。

当度量是凯勒时，$\nabla J = 0$，这意味着平行移动也保持[复结构](@entry_id:269128) $J$。因此，[和乐群](@entry_id:191471)中的每个元素都必须是与 $J$ 可交换的等距变换。在 $\mathrm{GL}(n,\mathbb{C})$ 中，保持标准[埃尔米特内积](@entry_id:141742)的[线性变换](@entry_id:149133)构成了**[酉群](@entry_id:138602)（unitary group）** $\mathrm{U}(n)$。因此，[凯勒条件](@entry_id:637291)等价于和乐群被限制在[酉群](@entry_id:138602)中，即 $\mathrm{Hol}(g) \subseteq \mathrm{U}(n)$ [@problem_id:2979199] [@problem_id:2979124]。反之，如果 $\mathrm{Hol}(g) \subseteq \mathrm{U}(n)$，则 $J$ 必然是平行场，即 $\nabla J=0$，从而度量是凯勒的。

### [凯勒条件](@entry_id:637291)的深刻推论

[凯勒条件](@entry_id:637291)的严格约束导致了[流形](@entry_id:153038)几何和拓扑的许多强[大性](@entry_id:268856)质。

**凯勒流形上的[霍奇理论](@entry_id:161814)**

在紧致凯勒流形上，[霍奇理论](@entry_id:161814)变得异常优美和强大。一系列被称为**凯勒恒等式（Kähler identities）**的算子[交换关系](@entry_id:136780)成立，它们联系了外[微分算子](@entry_id:140145) $(\partial, \bar{\partial})$ 及其共轭 $(\partial^*, \bar{\partial}^*)$，以及与凯勒形式 $\omega$ 相关的**勒夫谢茨算子（Lefschetz operator）** $L(\alpha) = \omega \wedge \alpha$ 及其共轭 $\Lambda$ [@problem_id:2979181]。这些恒等式中最基本的是：
$$
[\Lambda, \partial] = i\bar{\partial}^*, \quad [\Lambda, \bar{\partial}] = -i\partial^*
$$
这些恒等式的一个直接推论是不同拉普拉斯算子之间的关系。我们有三个主要的拉普拉斯算子：$\Delta_d = dd^*+d^*d$, $\Delta_\partial = \partial\partial^*+\partial^*\partial$ 和 $\Delta_{\bar{\partial}} = \bar{\partial}\bar{\partial}^*+\bar{\partial}^*\bar{\partial}$。在[凯勒流形](@entry_id:161192)上，它们满足惊人的关系 [@problem_id:2979181]：
$$
\Delta_d = 2\Delta_\partial = 2\Delta_{\bar{\partial}}
$$
这意味着一个形式是 $d$-调和的（即 $\Delta_d\alpha=0$），当且仅当它是 $\partial$-调和的和 $\bar{\partial}$-调和的。在紧致流形上，这进一步意味着[调和形式](@entry_id:193378)被所有的算子 $\partial, \bar{\partial}, \partial^*, \bar{\partial}^*$ 所湮灭 [@problem_id:2979181]。这个结果是[霍奇分解定理](@entry_id:199343)在凯勒流形上的精致化，它直接导致了[上同调群](@entry_id:142450) $H^k(M,\mathbb{C})$ 的[霍奇分解](@entry_id:160332)。此外，凯勒恒等式还保证了[霍奇拉普拉斯算子](@entry_id:183923) $\Delta_d$ 保持形式的 $(p,q)$-双次数 [@problem_id:2979181]，这在一般埃尔米特[流形](@entry_id:153038)上是不成立的。

凯勒形式 $\omega$ 本身也具有重要的[上同调](@entry_id:160558)性质。在紧致[凯勒流形](@entry_id:161192)上，由于其[体积形式](@entry_id:203000) $\omega^n$ 的积分必须为正，可以证明 $[\omega]^k \in H^{2k}(M,\mathbb{R})$ 对所有 $1 \le k \le n$ 都是非平凡的上同调类 [@problem_id:2979181]。

**[特殊和乐群](@entry_id:158889)与[卡拉比-丘流形](@entry_id:159253)**

[和乐群](@entry_id:191471)的进一步限制会引出更为特殊的几何。如果一个凯勒流形的里奇曲率形式为零，则其和乐群可以被进一步限制在**[特殊酉群](@entry_id:138145)（special unitary group）** $\mathrm{SU}(n)$ 中，即[行列式](@entry_id:142978)为1的[酉矩阵](@entry_id:138978)构成的群。在单连通的情形下，$\mathrm{Hol}(g) \subseteq \mathrm{SU}(n)$ 是[里奇平坦](@entry_id:159097)的充要条件 [@problem_id:2979124]。这类[里奇平坦](@entry_id:159097)的凯勒流形被称为**[卡拉比-丘流形](@entry_id:159253)（Calabi-Yau manifolds）**。$\mathrm{SU}(n)$ [和乐群](@entry_id:191471)的一个重要几何后果是存在一个处处非零、平行的全纯 $(n,0)$-形式 $\Omega$ (即 $\nabla \Omega = 0$)，它在弦理论中扮演着核心角色 [@problem_id:2979124]。

### 超越凯勒：非[凯勒几何](@entry_id:160314)一瞥

尽管[凯勒几何](@entry_id:160314)非常优美，但许多[复流形](@entry_id:159076)（如霍普夫[曲面](@entry_id:267450)）根本不允许存在凯勒度量。这催生了对更弱几何条件的研究，形成了广阔的**非[凯勒几何](@entry_id:160314)（non-Kähler geometry）**领域。其中一些重要的度量类型包括 [@problem_id:2979101]：

- **平衡度量（Balanced metric）**：满足 $d(\omega^{n-1})=0$。当 $n=2$ 时，这等价于[凯勒条件](@entry_id:637291)，但当 $n \ge 3$ 时，这是一个更弱的条件。
- **SKT度量（Strong Kähler with torsion / pluriclosed metric）**：满足 $\partial\bar{\partial}\omega=0$。这个条件意味着 $d\omega$ 是一个 $\partial$-闭也 $\bar{\partial}$-闭的 $(2,1)+(1,2)$ 型3-形式。
- **戈杜雄度量（Gauduchon metric）**：满足 $\partial\bar{\partial}(\omega^{n-1})=0$。**戈杜雄定理**保证在任意一个[埃尔米特度量](@entry_id:202337)的共形类中，总存在一个唯一的（直到常数缩放）戈杜雄度量。

这些度量类别之间的关系是错综复杂的。例如，当 $n=2$ 时，SKT条件与戈杜雄条件等价 [@problem_id:2979101]。然而，一般情况下，这些条件互不包含，为[复流形](@entry_id:159076)的几何分类提供了更精细的层次。例如，存在紧致[复流形](@entry_id:159076)，其上的度量是SKT的但不是平衡的 [@problem_id:2979101]。对这些非凯勒度量的研究是现代[微分几何](@entry_id:145818)的一个活跃前沿。