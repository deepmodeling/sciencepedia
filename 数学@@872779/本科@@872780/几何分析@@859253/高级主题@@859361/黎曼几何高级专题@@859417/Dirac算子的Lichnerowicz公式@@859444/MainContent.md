## 引言
[狄拉克算子](@entry_id:161631)的Lichnerowicz公式是现代[几何分析](@entry_id:157700)的基石之一，它以惊人的简洁形式，深刻揭示了[黎曼流形](@entry_id:261160)的曲率与定义在其上的旋量场的分析性质之间的内在联系。这一公式不仅是研究[旋量](@entry_id:158054)几何的强大工具，更在微分几何、拓扑学乃至理论物理等领域之间架起了坚实的桥梁。然而，对于初学者而言，理解这一公式的由来及其应用的广度常常构成一个知识上的鸿沟：我们如何从基本的几何概念出发，精确地量化曲率对一个核心[微分算子](@entry_id:140145)（[狄拉克算子](@entry_id:161631)）的影响？

本文旨在系统性地跨越这一鸿沟。我们将通过三个循序渐进的章节，为读者构建一个关于Lichnerowicz公式的完整知识图景。读者将学到：
- 在“原理与机制”一章中，我们将从[Clifford代数](@entry_id:137625)和[旋量](@entry_id:158054)结构等基础概念讲起，为定义[狄拉克算子](@entry_id:161631)铺平道路，并最终严谨地推导出Lichnerowicz公式本身，阐明其各个组成部分的几何意义。
- 接着，在“应用与跨学科联系”一章中，我们将展示该公式的强大威力，探索其在[谱几何](@entry_id:186460)中的消失性定理、在拓扑学中作为正数量曲率度量的障碍，以及在广义相对论中证明[正质量定理](@entry_id:158774)等前沿应用。
- 最后，通过“动手实践”环节，读者将有机会通过具体计算，将抽象的理论应用于平坦空间和球面等典型例子，从而巩固和深化对核心概念的理解。

现在，让我们从构建[旋量](@entry_id:158054)分析的代数与几何基础开始，踏上探索Lichnerowicz公式的旅程。

## 原理与机制

本章旨在阐明[狄拉克算子](@entry_id:161631)（Dirac operator）的Lichnerowicz公式背后的核心原理与机制。我们将从构建[旋量](@entry_id:158054)（spinor）所需的代数与几何基础出发，逐步推导出该公式，并探讨其在[几何分析](@entry_id:157700)中的深远影响。本章的论述将遵循从基本定义到核心定理，再到关键应用的逻辑顺序，旨在为读者提供一个系统而严谨的知识框架。

### 旋量分析的代数与几何基础

在黎曼流形上定义旋量与[狄拉克算子](@entry_id:161631)，需要一套特定的代数与几何工具。其核心在于[Clifford代数](@entry_id:137625)，它为“线性化”度量结构提供了代数框架；以及旋量结构，它为在[流形](@entry_id:153038)上整体地定义[旋量](@entry_id:158054)场提供了几何保障。

#### [Clifford代数](@entry_id:137625)：旋量的代数舞台

在处理[向量空间](@entry_id:151108)时，我们通常熟悉[外代数](@entry_id:201164)（exterior algebra） $\Lambda V$，其核心特征是反对称的楔积（wedge product），满足关系 $v \wedge v = 0$ 以及通过极化得到的 $v \wedge w = -w \wedge v$。这种结构在定义[微分形式](@entry_id:146747)时至关重要。然而，为了将[黎曼度量](@entry_id:754359) $g$ 的信息融入[代数结构](@entry_id:137052)中，我们需要一个不同的构造，即**[Clifford代数](@entry_id:137625)**。

给定一个配备了[对称双线性形式](@entry_id:148281) $g$（例如黎曼度量）的实[向量空间](@entry_id:151108) $V$，其[Clifford代数](@entry_id:137625) $\mathrm{Cl}(V, g)$ 的构造目标是将与 $g$ 相关的二次型 $Q(v) = g(v,v)$ “线性化”。这是通过要求向量自身的乘积等于其二次型的值来实现的。具体而言，与[外代数](@entry_id:201164)类似，[Clifford代数](@entry_id:137625)也是[张量代数](@entry_id:161671) $T(V) = \bigoplus_{k=0}^{\infty} V^{\otimes k}$ 的一个商代数。

在旋量几何中，我们采用的惯例是 $\mathrm{Cl}(T_x M, g_x)$，其中 $(M,g)$ 是[黎曼流形](@entry_id:261160)，$T_x M$ 是其在点 $x$ 的切空间。该代数由[张量代数](@entry_id:161671) $T(T_x M)$ 模掉由所有形如 $v \otimes v + g_x(v,v) \cdot 1$ 的元素生成的[双边理想](@entry_id:272452) $I_{\mathrm{Cl}}$ 而得到。其中 $v \in T_x M$，$1$ 是 $\mathbb{R}$ 中的单位元。在这个商代数中，诱导的乘积（称为**Clifford乘积**，通常并列写出）满足基本关系：
$$
v^2 = -g_x(v,v) \cdot 1
$$
这个关系式捕捉了度量的核心信息。通过在 $v+w$ 上应用此关系，我们可以推导出任意两个向量 $v, w \in T_x M$ 的乘积满足的[极化恒等式](@entry_id:271819)：
$$
(v+w)^2 = -g_x(v+w, v+w) \cdot 1
$$
展开两侧，我们得到：
$$
v^2 + vw + wv + w^2 = -(g_x(v,v) + 2g_x(v,w) + g_x(w,w)) \cdot 1
$$
利用 $v^2 = -g_x(v,v) \cdot 1$ 和 $w^2 = -g_x(w,w) \cdot 1$ 进行代换，简化后便得到至关重要的**Clifford关系**:
$$
vw + wv = -2g_x(v,w) \cdot 1
$$
这个关系表明，两个向量的Clifford乘积的对称部分由度量确定。这与[外代数](@entry_id:201164)中 $v \wedge w + w \wedge v = 0$ 的纯反对称性形成了鲜明对比 [@problem_id:3072049]。[Clifford代数](@entry_id:137625)因此成为一个更丰富的结构，它既包含了向量的[反对易](@entry_id:186708)性质，也编码了底层的[度量几何](@entry_id:185748)。

#### 旋量群与旋量结构：几何提升

要在整个[流形](@entry_id:153038)上一致地定义旋量，我们需要一个整体的几何结构，这便是**旋量结构（spin structure）**。对于一个 $n$ 维定向黎曼流形 $(M,g)$，其所有定向[标准正交标架](@entry_id:189702)构成一个[主丛](@entry_id:160029)，称为定向[标准正交标架](@entry_id:189702)丛 $P_{\mathrm{SO}(n)}$，其结构群为[特殊正交群](@entry_id:146418) $\mathrm{SO}(n)$。

我们知道，对于 $n \ge 3$，$\mathrm{SO}(n)$ 的[基本群](@entry_id:146111)是 $\pi_1(\mathrm{SO}(n)) \cong \mathbb{Z}_2$，这意味着它不是单连通的。$\mathrm{SO}(n)$ 有一个[二重覆盖](@entry_id:183816)群，称为**[旋量](@entry_id:158054)群（spin group）** $\mathrm{Spin}(n)$，它是单连通的。存在一个典范的 $2:1$ 覆盖同态 $\lambda: \mathrm{Spin}(n) \to \mathrm{SO}(n)$。（注意，当 $n=2$ 时，$\mathrm{SO}(2) \cong S^1$，其[万有覆盖](@entry_id:151142)是 $\mathbb{R}$，而 $\mathrm{Spin}(2) \cong S^1$ 自身，因此此时 $\lambda$ 不是[万有覆盖](@entry_id:151142)。）

[流形](@entry_id:153038) $(M,g)$ 上的一个[旋量](@entry_id:158054)结构，本质上是将[标架丛](@entry_id:187852)的结构群从 $\mathrm{SO}(n)$ “提升”到 $\mathrm{Spin}(n)$。形式上，一个[旋量](@entry_id:158054)结构由一个主 $\mathrm{Spin}(n)$-丛 $P_{\mathrm{Spin}(n)} \to M$ 和一个丛映射 $\Theta: P_{\mathrm{Spin}(n)} \to P_{\mathrm{SO}(n)}$ 组成，该映射覆盖了 $M$ 上的[恒等映射](@entry_id:634191)，并且是等变（equivariant）的。等变条件指的是，对于任意 $u \in P_{\mathrm{Spin}(n)}$ 和 $g' \in \mathrm{Spin}(n)$，满足：
$$
\Theta(u \cdot g') = \Theta(u) \cdot \lambda(g')
$$
这里，$u \cdot g'$ 表示 $\mathrm{Spin}(n)$ 在 $P_{\mathrm{Spin}(n)}$ 上的右作用，而 $\Theta(u) \cdot \lambda(g')$ 表示 $\mathrm{SO}(n)$ 在 $P_{\mathrm{SO}(n)}$ 上的右作用。这个定义确保了两个[主丛](@entry_id:160029)的结构能够以与群覆盖相容的方式联系起来。

一个[流形](@entry_id:153038)是否允许存在旋量结构，是一个拓扑问题。一个定向[黎曼流形](@entry_id:261160) $(M,g)$ 存在旋量结构的充分必要条件是其第二个**Stiefel-Whitney类** $w_2(TM) \in H^2(M; \mathbb{Z}_2)$ 为零 [@problem_id:3072060]。这是一个深刻的拓扑不变量，它衡量了将 $\mathrm{SO}(n)$ 结构提升到 $\mathrm{Spin}(n)$ 结构的拓扑障碍。

#### [旋量丛](@entry_id:181093)与[旋量](@entry_id:158054)联络

一旦[流形](@entry_id:153038)具备了旋量结构 $P_{\mathrm{Spin}(n)}$，我们就可以通过伴随丛（associated bundle）的构造来定义**[旋量丛](@entry_id:181093)（spinor bundle）**。这需要一个 $\mathrm{Spin}(n)$ 群的表示。所使用的表示是**[旋量表示](@entry_id:141362)（spin representation）** $\rho: \mathrm{Spin}(n) \to \mathrm{GL}(\Delta_n)$，其中 $\Delta_n$ 是复[Clifford代数](@entry_id:137625) $\mathrm{Cl}_n^{\mathbb{C}}$ 的一个不可约模，称为旋量模。

[旋量丛](@entry_id:181093) $\mathbb{S}$ 定义为伴随于[主丛](@entry_id:160029) $P_{\mathrm{Spin}(n)}$ 和[旋量表示](@entry_id:141362) $\rho$ 的向量丛：
$$
\mathbb{S} = P_{\mathrm{Spin}(n)} \times_\rho \Delta_n
$$
根据伴随丛的构造，$\mathbb{S}$ 在点 $p \in M$ 的纤维 $\mathbb{S}_p$ 同构于表示空间 $\Delta_n$。$\Delta_n$ 的复维度为 $2^{\lfloor n/2 \rfloor}$。当维数 $n$ 是偶数时，[Clifford代数](@entry_id:137625)中存在一个“手性元”（chirality element），它在 $\Delta_n$ 上的作用将 $\Delta_n$ 分解为两个[特征值](@entry_id:154894)为 $\pm 1$ 的[子空间](@entry_id:150286) $\Delta_n = \Delta_n^+ \oplus \Delta_n^-$。这个分解也诱导出[旋量丛](@entry_id:181093)的典范分裂 $\mathbb{S} = \mathbb{S}^+ \oplus \mathbb{S}^-$，其中 $\mathbb{S}^{\pm}$ 的纤维维度为 $2^{n/2 - 1}$ [@problem_id:3072051]。$\mathbb{S}^+$ 和 $\mathbb{S}^-$ 的[截面](@entry_id:154995)分别称为正手性和负手性[旋量](@entry_id:158054)场。

为了在[旋量](@entry_id:158054)场上进行[微分](@entry_id:158718)，我们需要一个联络。旋量结构的一个关键几何后果是，[黎曼几何](@entry_id:160508)中的Levi-Civita联络（定义在 $P_{\mathrm{SO}(n)}$ 上的一个 $\mathfrak{so}(n)$-值[联络形式](@entry_id:263247)）可以唯一地提升为 $P_{\mathrm{Spin}(n)}$ 上的一个 $\mathfrak{spin}(n)$-值[联络形式](@entry_id:263247) [@problem_id:3072060]。这个提升的联络继而诱导了在[旋量丛](@entry_id:181093) $\mathbb{S}$ 上的一个协变导数，称为**旋量联络（spin connection）** $\nabla^{\mathbb{S}}$。

在局部[标准正交标架](@entry_id:189702) $\{e_1, \dots, e_n\}$ 下，Levi-Civita联络由[联络1-形式](@entry_id:275839) $\omega_{ij}$ 描述，满足 $\nabla e_i = \sum_j \omega_{ij} e_j$。[旋量](@entry_id:158054)联络 $\nabla^{\mathbb{S}}$ 作用在一个局部[旋量](@entry_id:158054)场 $\psi$ 上的表达式可以通过Clifford乘法 $c(e_i)$ 给出 [@problem_id:2995205]：
$$
\nabla^{\mathbb{S}}_X \psi = X(\psi) + \frac{1}{4} \sum_{i,j=1}^n \omega_{ij}(X) c(e_i)c(e_j) \psi
$$
其中 $X(\psi)$ 是[方向导数](@entry_id:189133)，第二项是与曲率相关的修正项。这个公式明确地将底[流形](@entry_id:153038)的几何（通过 $\omega_{ij}$）与[旋量](@entry_id:158054)纤维的[代数结构](@entry_id:137052)（通过 $c(e_i)c(e_j)$）联系起来。

### [狄拉克算子](@entry_id:161631)与Lichnerowicz公式

有了[旋量丛](@entry_id:181093) $\mathbb{S}$ 和[旋量](@entry_id:158054)联络 $\nabla^{\mathbb{S}}$，我们就拥有了定义[狄拉克算子](@entry_id:161631)的所有要素。

#### [狄拉克算子](@entry_id:161631)：一阶几何算子

**[狄拉克算子](@entry_id:161631)（Dirac operator）** $D$ 是一个作用在[旋量丛](@entry_id:181093)[截面](@entry_id:154995)（[旋量](@entry_id:158054)场）上的一阶微分算子。它通过将[旋量](@entry_id:158054)联络与Clifford乘法复合而定义。给定一个[局部定向](@entry_id:264384)[标准正交标架](@entry_id:189702) $\{e_i\}_{i=1}^n$，[狄拉克算子](@entry_id:161631)定义为：
$$
D\psi = \sum_{i=1}^n c(e_i) \nabla^{\mathbb{S}}_{e_i} \psi
$$
这里的 $c(e_i)$ 是切向量 $e_i$ 通过Clifford乘法作用在[旋量](@entry_id:158054)上的[线性变换](@entry_id:149133)。这个定义是与标架选取无关的，因此 $D$ 是一个在整个[流形](@entry_id:153038)上良定义的算子。[狄拉克算子](@entry_id:161631)是[椭圆算子](@entry_id:181616)，并且在[紧流形](@entry_id:158804)上是（本质）自伴的。它在几何、拓扑和物理中都扮演着核心角色，其性质深刻地反映了[流形](@entry_id:153038)的几何与拓扑。

从概念上讲，[狄拉克算子](@entry_id:161631)可以被视为某种意义上的“[拉普拉斯算子](@entry_id:146319)的平方根”。为了揭示这种关系，我们来计算它的平方 $D^2$。

#### Bochner-Weitzenböck分解：推导Lichnerowicz公式

在几何分析中，有一个普遍的指导思想，称为**Bochner-Weitzenböck哲学**：许多几何中自然出现的二阶[微分算子](@entry_id:140145)（“拉普拉斯型”算子）可以被分解为一个“粗拉普拉斯算子”（rough Laplacian）和一个零阶的曲率项。前者捕捉了算子的[微分](@entry_id:158718)部分，类似于动能；后者是一个代数项，依赖于[流形](@entry_id:153038)的曲率，类似于势能 [@problem_id:3072042]。Lichnerowicz公式正是[狄拉克算子](@entry_id:161631)平方的Bochner-Weitzenböck分解。

我们的目标是计算 $D^2$。为此，我们选择在任意一点 $p \in M$ 使用一个[法坐标](@entry_id:143194)系下的[标准正交标架](@entry_id:189702) $\{e_i\}$，使得在该点 $\nabla_{e_i} e_j|_p = 0$。这大大简化了计算。我们有：
$$
D^2\psi = D(D\psi) = \sum_{j=1}^n c(e_j) \nabla^{\mathbb{S}}_{e_j} \left( \sum_{i=1}^n c(e_i) \nabla^{\mathbb{S}}_{e_i} \psi \right)
$$
由于旋量联络与Clifford乘法的相容性（在[法坐标](@entry_id:143194)系下 $\nabla^{\mathbb{S}}_{e_j}(c(e_i))|_p = c(\nabla_{e_j} e_i)|_p = 0$），在 $p$ 点，我们可以将 $c(e_i)$ 移到 $\nabla^{\mathbb{S}}_{e_j}$ 的左边：
$$
D^2\psi|_p = \sum_{i,j=1}^n c(e_j) c(e_i) \nabla^{\mathbb{S}}_{e_j} \nabla^{\mathbb{S}}_{e_i} \psi
$$
为了分离出拉普拉斯项和曲率项，我们将Clifford乘积 $c(e_j)c(e_i)$ 分解为其对称和反对称部分：
$$
c(e_j)c(e_i) = \frac{1}{2}(c(e_j)c(e_i) + c(e_i)c(e_j)) + \frac{1}{2}(c(e_j)c(e_i) - c(e_i)c(e_j)) = -\delta_{ji} \cdot \mathrm{Id}_{\mathbb{S}} + \frac{1}{2}[c(e_j), c(e_i)]
$$
代入 $D^2$ 的表达式，得到：
$$
D^2\psi|_p = -\sum_{i=1}^n \nabla^{\mathbb{S}}_{e_i} \nabla^{\mathbb{S}}_{e_i} \psi + \frac{1}{2} \sum_{i,j=1}^n [c(e_j), c(e_i)] \nabla^{\mathbb{S}}_{e_j} \nabla^{\mathbb{S}}_{e_i} \psi
$$
第一项正是（负的）**[联络拉普拉斯算子](@entry_id:197120)**（或称[Bochner拉普拉斯算子](@entry_id:204681)），记为 $\nabla^{\mathbb{S}*}\nabla^{\mathbb{S}}$。第二项是我们要研究的曲率项。由于 $[c(e_j), c(e_i)]$ 关于指标 $i,j$ 是反对称的，它只拾取了 $\nabla^{\mathbb{S}}_{e_j} \nabla^{\mathbb{S}}_{e_i}$ 的反对称部分，也就是[联络的曲率](@entry_id:159154)：
$$
\frac{1}{2} \sum_{i,j} [c(e_j), c(e_i)] \left( \frac{1}{2} [\nabla^{\mathbb{S}}_{e_j}, \nabla^{\mathbb{S}}_{e_i}] \right) \psi = \frac{1}{4} \sum_{i,j} [c(e_j), c(e_i)] R^{\mathbb{S}}(e_j, e_i) \psi
$$
其中 $R^{\mathbb{S}}(X,Y) = [\nabla^{\mathbb{S}}_X, \nabla^{\mathbb{S}}_Y] - \nabla^{\mathbb{S}}_{[X,Y]}$ 是[旋量](@entry_id:158054)[联络的曲率](@entry_id:159154)算子。一个关键的恒等式将旋量曲率与[黎曼曲率张量](@entry_id:160189) $R^g$ 联系起来 [@problem_id:3072055]：
$$
R^{\mathbb{S}}(e_j, e_i) = -\frac{1}{4} \sum_{a,b=1}^n \langle R^g(e_j, e_i)e_a, e_b \rangle c(e_a)c(e_b) = -\frac{1}{4} \sum_{a,b=1}^n R_{jiab} c(e_a)c(e_b)
$$
将此代入曲率项，得到一个涉及[黎曼张量分量](@entry_id:188469)和四个Clifford乘积的复杂表达式。然而，通过一个精妙的代数计算，利用[黎曼张量的对称性](@entry_id:190547)和[Clifford代数](@entry_id:137625)迹的性质，可以证明这个复杂的算子最终坍缩为一个非常简单的形式 [@problem_id:3072055] [@problem_id:3072028]。这个零阶的[曲率算子](@entry_id:198006)恰好是与[流形](@entry_id:153038)**数量曲率（scalar curvature）** $R$ 成正比的标量乘法算子。

#### Lichnerowicz公式与约定的作用

经过上述计算，我们最终得到**Lichnerowicz公式**:
$$
D^2 = \nabla^{\mathbb{S}*}\nabla^{\mathbb{S}} + \frac{1}{4} R \cdot \mathrm{Id}_{\mathbb{S}}
$$
这个公式优雅地将[狄拉克算子](@entry_id:161631)的平方分解为一个非负的动能项 $\nabla^{\mathbb{S}*}\nabla^{\mathbb{S}}$ 和一个由数量曲率决定的势能项 $\frac{1}{4}R$ [@problem_id:3072042]。

值得强调的是，公式中曲率项的符号依赖于[黎曼曲率张量](@entry_id:160189)的定义约定。我们采用的约定是 $R(X,Y)Z = \nabla_X\nabla_Y Z - \nabla_Y\nabla_X Z - \nabla_{[X,Y]}Z$，在此约定下，标准单位球面 $S^n$ 的数量曲率为正值 $n(n-1)$。Lichnerowicz公式中的曲率项符号为正。如果采用相反的曲率约定 $R' = -R$，那么数量曲率也会变号 $R' = -R$，并且公式中的曲率项会相应地变为 $-\frac{1}{4}R'$ [@problem_id:3072038]。因此，在使用此公式时，必须明确所采用的曲率约定。

### 应用与诠释

Lichnerowicz公式的强大之处在于它将一个分析对象（[狄拉克算子](@entry_id:161631)的谱）与一个纯粹的[几何不变量](@entry_id:178611)（数量曲率）直接联系起来。

#### 谱的推论与消失性定理

我们可以将Lichnerowicz公式类比于量子力学中的薛定谔方程。算子 $D^2$ 的谱（[特征值](@entry_id:154894)集合）受到“势能”项 $\frac{1}{4}R$ 的显著影响。

考虑一个紧致（closed）[旋量](@entry_id:158054)[流形](@entry_id:153038)。由于 $D$ 是自伴的，其平方 $D^2$ 是一个非负算子，即其所有[特征值](@entry_id:154894) $\lambda \ge 0$。Lichnerowicz公式的积分形式为：
$$
\int_M \langle D^2\psi, \psi \rangle dV_g = \int_M |\nabla^{\mathbb{S}}\psi|^2 dV_g + \frac{1}{4} \int_M R |\psi|^2 dV_g
$$
左侧是 $\|D\psi\|_{L^2}^2$。如果[流形](@entry_id:153038)的数量曲率处处为正，即 $R \ge R_0 > 0$，那么对于任意非零[旋量](@entry_id:158054)场 $\psi$：
$$
\|D\psi\|_{L^2}^2 = \|\nabla^{\mathbb{S}}\psi\|_{L^2}^2 + \frac{1}{4} \int_M R |\psi|^2 dV_g \ge \frac{R_0}{4} \int_M |\psi|^2 dV_g = \frac{R_0}{4} \|\psi\|_{L^2}^2
$$
这意味着 $D^2$ 的任何[特征值](@entry_id:154894) $\lambda$ 都必须满足 $\lambda \ge \frac{R_0}{4} > 0$。特别地，零不能是 $D^2$ 的[特征值](@entry_id:154894)。这意味着不存在非零的[旋量](@entry_id:158054)场 $\psi$ 使得 $D^2\psi=0$，也即不存在非零的 $\psi$ 使得 $D\psi=0$。因此，[狄拉克算子](@entry_id:161631)的核（kernel）是平凡的，$\ker D = \{0\}$ [@problem_id:3072031]。

这个结论是一个深刻的**消失性定理**，通常称为**Bochner-Lichnerowicz消失性定理**：
**定理**：在一个数量曲率为正的紧致旋量[流形](@entry_id:153038)上，不存在非平凡的**调和旋量（harmonic spinors）**（即 $\ker D$ 中的元素）。
这个定理为[流形](@entry_id:153038)是否能支持正数量曲率度量提供了一个重要的拓扑障碍。

#### 一个具体例子：[Killing旋量](@entry_id:190525)方程

Lichnerowicz公式的威力还可以通过分析满足特定[微分方程](@entry_id:264184)的[旋量](@entry_id:158054)场来体现。一个重要的例子是**[Killing旋量](@entry_id:190525)方程**：
$$
\nabla^{\mathbb{S}}_X \psi = \mu c(X) \psi
$$
其中 $\mu$ 是一个实常数。满足此方程的非零旋量场 $\psi$ 称为**[Killing旋量](@entry_id:190525)**。

首先，我们可以计算[狄拉克算子](@entry_id:161631)作用在[Killing旋量](@entry_id:190525)上的结果。将[Killing旋量](@entry_id:190525)方程代入 $D$ 的定义：
$$
D\psi = \sum_{i=1}^n c(e_i) (\mu c(e_i) \psi) = \mu \sum_{i=1}^n c(e_i)^2 \psi = \mu \sum_{i=1}^n (-1) \psi = -n\mu \psi
$$
这表明[Killing旋量](@entry_id:190525)是[狄拉克算子](@entry_id:161631)的特征旋量，[特征值](@entry_id:154894)为 $-n\mu$。因此，$D^2\psi = (-n\mu)^2\psi = n^2\mu^2\psi$。

另一方面，我们可以使用Lichnerowicz公式来计算 $D^2\psi$。为此，需要计算 $\nabla^{\mathbb{S}*}\nabla^{\mathbb{S}}\psi$。在[法坐标](@entry_id:143194)系下，它等于 $-\sum_i \nabla^{\mathbb{S}}_{e_i} \nabla^{\mathbb{S}}_{e_i} \psi$。我们计算[二阶导数](@entry_id:144508)：
$$
\nabla^{\mathbb{S}}_{e_i}(\nabla^{\mathbb{S}}_{e_i}\psi) = \nabla^{\mathbb{S}}_{e_i}(\mu c(e_i)\psi) = \mu c(e_i) \nabla^{\mathbb{S}}_{e_i}\psi = \mu c(e_i) (\mu c(e_i)\psi) = \mu^2 c(e_i)^2 \psi = -\mu^2\psi
$$
因此，$\nabla^{\mathbb{S}*}\nabla^{\mathbb{S}}\psi = -\sum_i (-\mu^2\psi) = n\mu^2\psi$。
将此结果代入Lichnerowicz公式，得到：
$$
D^2\psi = (n\mu^2 + \frac{1}{4}R)\psi
$$
比较我们得到的两个 $D^2\psi$ 的表达式：
$$
n^2\mu^2 \psi = (n\mu^2 + \frac{1}{4}R)\psi
$$
由于 $\psi$ 是非零的，我们可以得到数量曲率必须满足的刚性条件 [@problem_id:2995171]：
$$
R = 4(n^2\mu^2 - n\mu^2) = 4n(n-1)\mu^2
$$
这个结果表明，一个[流形](@entry_id:153038)如果存在实[Killing旋量](@entry_id:190525)，其数量曲率必须为正常数（除非 $\mu=0$ 或 $n=1$）。这揭示了[特殊几何](@entry_id:194564)结构（如[Killing旋量](@entry_id:190525)场）的存在如何[对流](@entry_id:141806)形的全局曲率施加极强的限制，这是几何分析中的一个反复出现的主题，也展示了Lichnerowicz公式作为连接分析与几何的桥梁所具有的强大力量。