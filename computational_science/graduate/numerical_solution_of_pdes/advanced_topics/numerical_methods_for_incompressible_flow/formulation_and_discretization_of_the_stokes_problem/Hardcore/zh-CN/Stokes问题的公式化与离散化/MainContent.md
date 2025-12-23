## 引言
[斯托克斯方程](@entry_id:196346)是[流体力学](@entry_id:136788)领域的基石，它精确描述了在[低雷诺数](@entry_id:204816)下（即[粘性力](@entry_id:263294)远大于[惯性力](@entry_id:169104)时）的[流体运动](@entry_id:182721)，这在从[地幔对流](@entry_id:203493)到微流控设备和[生物医学工程](@entry_id:268134)等众多科学与工程领域中都至关重要。然而，将这一优雅的物理模型转化为可靠的[数值模拟](@entry_id:137087)却面临着独特的挑战。其核心难点在于[不可压缩性约束](@entry_id:750592)，该约束将问题转化为一个数学上称为“[鞍点问题](@entry_id:174221)”的耦合系统，其数值解的稳定性不再是理所当然的。

本文旨在系统性地解决这一知识鸿沟：如何对[斯托克斯问题](@entry_id:755479)进行稳健且高效的[数值离散化](@entry_id:752782)。我们将深入探讨有限元方法框架下的核心理论与实践，揭示从数学原理到实际应用的完整图景。读者将学习到：[斯托克斯问题](@entry_id:755479)的弱形式是如何建立的；保证离散系统稳定性的关键——[LBB条件](@entry_id:746626)——是什么，以及它为何如此重要；当[LBB条件](@entry_id:746626)不满足时，如何通过先进的稳定化方法来“拯救”数值解。

为了构建一个全面的理解，本文分为三个循序渐进的章节。在“**原理与机制**”中，我们将奠定理论基础，深入剖析[斯托克斯问题](@entry_id:755479)的[变分形式](@entry_id:166033)、压力唯一性问题、[LBB条件](@entry_id:746626)以及各种稳定化方法的内在机理。接着，在“**应用与[交叉](@entry_id:147634)学科联系**”中，我们将拓宽视野，探索替代性的数学表述、丰富的有限元格式“动物园”、处理复杂几何与代数系统的实际挑战，并通过[生物流体动力学](@entry_id:152896)的案例展示其跨学科应用。最后，“**动手实践**”部分将提供一系列精心设计的练习，帮助读者将理论知识转化为可操作的计算技能。

## 原理与机制

本章旨在深入探讨[稳态](@entry_id:182458)不可压缩[斯托克斯问题](@entry_id:755479)的数学原理和[数值离散化](@entry_id:752782)机制。在前一章介绍其物理背景和重要性的基础上，我们将从[变分形式](@entry_id:166033)（或称[弱形式](@entry_id:142897)）出发，系统地分析其连续形式的[适定性](@entry_id:148590)，特别是压[力场](@entry_id:147325)的唯一性问题。随后，我们将过渡到[有限元离散化](@entry_id:193156)，并聚焦于离散[系统稳定性](@entry_id:273248)的核心——Ladyzhenskaya-Babuška-Brezzi (LBB) 条件。我们将通过具体的例子揭示不满足此条件所导致的数值不稳定性。最后，我们将介绍并阐释多种现代稳定化方法，这些方法旨在克服 LBB 条件的限制，从而能够使用更广泛的有限元空间对。

### [斯托克斯问题](@entry_id:755479)的[弱形式](@entry_id:142897)

[斯托克斯方程](@entry_id:196346)的强形式由线[动量守恒](@entry_id:149964)和质量守恒（不可压缩性）构成，分别表示为：
$$
-\nu \Delta \boldsymbol{u} + \nabla p = \boldsymbol{f} \quad \text{in } \Omega,
$$
$$
\nabla \cdot \boldsymbol{u} = 0 \quad \text{in } \Omega,
$$
其中 $\boldsymbol{u}$ 是流体速度矢量， $p$ 是压力（运动学压力），$\nu$ 是运动粘度，$\boldsymbol{f}$ 是单位质量的[体力](@entry_id:174230)。这些方程必须辅以适当的边界条件才能构成一个完整的边值问题。

为了推导其弱形式，我们引入一组适当的函数空间。[速度场](@entry_id:271461) $\boldsymbol{u}$ 通常属于索博列夫空间 $H^1(\Omega)^d$ 的一个[子空间](@entry_id:150286)，该[子空间](@entry_id:150286)包含了边界条件的信息。压[力场](@entry_id:147325) $p$ 通常被假定属于[平方可积函数](@entry_id:200316)空间 $L^2(\Omega)$。我们选取速度检验函数 $\boldsymbol{v}$ 和压力[检验函数](@entry_id:166589) $q$，它们分别与解函数 $\boldsymbol{u}$ 和 $p$ 位于相同的函数空间。

动量方程的[弱形式](@entry_id:142897)通过将其与任意[检验函数](@entry_id:166589) $\boldsymbol{v}$ 做 $L^2$ [内积](@entry_id:158127)并进行分部积分得到。将[动量方程](@entry_id:197225)乘以 $\boldsymbol{v}$ 并在定义域 $\Omega$ 上积分：
$$
\int_{\Omega} (-\nu \Delta \boldsymbol{u}) \cdot \boldsymbol{v} \, \mathrm{d}x + \int_{\Omega} (\nabla p) \cdot \boldsymbol{v} \, \mathrm{d}x = \int_{\Omega} \boldsymbol{f} \cdot \boldsymbol{v} \, \mathrm{d}x.
$$
利用格林第一公式（[分部积分](@entry_id:136350)的推广），我们得到：
$$
\nu \int_{\Omega} \nabla \boldsymbol{u} : \nabla \boldsymbol{v} \, \mathrm{d}x - \int_{\partial \Omega} \nu \frac{\partial \boldsymbol{u}}{\partial \boldsymbol{n}} \cdot \boldsymbol{v} \, \mathrm{d}s - \int_{\Omega} p (\nabla \cdot \boldsymbol{v}) \, \mathrm{d}x + \int_{\partial \Omega} p (\boldsymbol{v} \cdot \boldsymbol{n}) \, \mathrm{d}s = \int_{\Omega} \boldsymbol{f} \cdot \boldsymbol{v} \, \mathrm{d}x.
$$
此处的边界积分项的具体处理方式取决于边界条件。同理，不可压缩约束 $\nabla \cdot \boldsymbol{u} = 0$ 通过与任意压力检验函数 $q$ 相乘并积分得到其弱形式：
$$
\int_{\Omega} q (\nabla \cdot \boldsymbol{u}) \, \mathrm{d}x = 0.
$$
为了数学上的对称性和便利性，我们定义如下的双线性形式：
- 粘性项： $a(\boldsymbol{u}, \boldsymbol{v}) = \nu \int_{\Omega} \nabla \boldsymbol{u} : \nabla \boldsymbol{v} \, \mathrm{d}x$
- 耦合项（或称[压力-速度耦合](@entry_id:155962)项）： $b(\boldsymbol{v}, p) = -\int_{\Omega} p (\nabla \cdot \boldsymbol{v}) \, \mathrm{d}x$

综合起来，[斯托克斯问题](@entry_id:755479)的[弱形式](@entry_id:142897)（或称混合[变分形式](@entry_id:166033)）是一个典型的**[鞍点问题](@entry_id:174221)**：寻找一对解 $(\boldsymbol{u}, p) \in V \times Q$（其中 $V$ 和 $Q$ 是合适的速度和压力函数空间），使得对于所有的[检验函数](@entry_id:166589) $(\boldsymbol{v}, q) \in V \times Q$ 均满足：
$$
\begin{aligned}
a(\boldsymbol{u}, \boldsymbol{v}) + b(\boldsymbol{v}, p) = (\boldsymbol{f}, \boldsymbol{v}) \\
b(\boldsymbol{u}, q) = 0
\end{aligned}
$$
其中 $(\boldsymbol{f}, \boldsymbol{v})$ 代表体力项和边界条件贡献的[线性泛函](@entry_id:276136)。

### 连续问题的[适定性](@entry_id:148590)与压力唯一性

一个数学模型的[适定性](@entry_id:148590)（existence, uniqueness, and stability of the solution）是其理论分析和数值求解的基础。对于[斯托克斯问题](@entry_id:755479)，压力的唯一性是一个微妙且关键的问题，它与边界条件的类型密切相关。

#### 纯狄利克雷边界条件下的压力不唯一性

考虑最常见的情况：在整个边界 $\partial\Omega$ 上施加齐次狄利克雷（Dirichlet）边界条件，即[无滑移边界条件](@entry_id:186229) $\boldsymbol{u} = \boldsymbol{0}$ on $\partial\Omega$。在这种情况下，速度的[试探空间](@entry_id:756166)和检验空间均为 $V = H_0^1(\Omega)^d$（在边界上迹为零的 $H^1$ [函数空间](@entry_id:143478)），压力空间暂定为 $Q = L^2(\Omega)$。

问题的核心在于，压力 $p$ 在[动量方程](@entry_id:197225)中仅以其梯度 $\nabla p$ 的形式出现。这意味着，如果 $(\boldsymbol{u}, p)$ 是一个解，那么对于任意常数 $c \in \mathbb{R}$，[速度场](@entry_id:271461) $\boldsymbol{u}$ 和新的压[力场](@entry_id:147325) $\tilde{p} = p + c$ 构成的对 $(\boldsymbol{u}, \tilde{p})$ 是否也是一个解？显然，$\nabla \tilde{p} = \nabla (p+c) = \nabla p$，因此强形式的动量方程保持不变。

在弱形式中，这种不确定性表现为耦合项 $b(\boldsymbol{v}, p)$ 对常数的“不敏感性”。对于任意[检验函数](@entry_id:166589) $\boldsymbol{v} \in H_0^1(\Omega)^d$，我们考察 $b(\boldsymbol{v}, p+c)$：
$$
b(\boldsymbol{v}, p+c) = -\int_{\Omega} (p+c)(\nabla \cdot \boldsymbol{v}) \, \mathrm{d}x = -\int_{\Omega} p(\nabla \cdot \boldsymbol{v}) \, \mathrm{d}x - c \int_{\Omega} \nabla \cdot \boldsymbol{v} \, \mathrm{d}x.
$$
根据[散度定理](@entry_id:143110)，$\int_{\Omega} \nabla \cdot \boldsymbol{v} \, \mathrm{d}x = \int_{\partial\Omega} \boldsymbol{v} \cdot \boldsymbol{n} \, \mathrm{d}s$。由于 $\boldsymbol{v} \in H_0^1(\Omega)^d$，其在边界 $\partial\Omega$ 上的迹为零，因此边界积分为零。这意味着 $c \int_{\Omega} \nabla \cdot \boldsymbol{v} \, \mathrm{d}x = 0$。于是，我们得到 $b(\boldsymbol{v}, p+c) = b(\boldsymbol{v}, p)$。

这表明，对于纯狄利克雷边界问题，弱形式的[方程组](@entry_id:193238)无法确定压力的一个任意常数。压力解在 $L^2(\Omega)$ 空间中是不唯一的，它只在一个相差常数的[等价类](@entry_id:156032)中唯一。从[泛函分析](@entry_id:146220)的角度看，这是因为算子 $B: \boldsymbol{v} \mapsto -\nabla \cdot \boldsymbol{v}$ 的[伴随算子](@entry_id:140236) $B^*$ 的核空间（nullspace）非平凡，恰好由常数函数构成。

为了获得唯一的压力解，我们必须施加一个额外的约束来固定这个常数。标准做法是要求压力的全域积分为零，即 $\int_{\Omega} p \, \mathrm{d}x = 0$。这等价于将压力空间限制在 $Q = L_0^2(\Omega) = \{ q \in L^2(\Omega) : \int_{\Omega} q \, \mathrm{d}x = 0 \}$。这个约束从每个压力等价类中挑选出了唯一一个均值为零的代表元，从而保证了[解的唯一性](@entry_id:143619)。

值得强调的是，压力 $p$ 并非仅仅是确保[不可压缩性](@entry_id:274914)的[拉格朗日乘子](@entry_id:142696)。在某些物理情景下，即使[速度场](@entry_id:271461)为零，压[力场](@entry_id:147325)也可以是非零的。一个典型的例子是流体在势场力作用下的静[水平衡](@entry_id:140465)。假设[体力](@entry_id:174230) $\boldsymbol{f}$ 是一个标量势 $\phi$ 的梯度，即 $\boldsymbol{f} = \nabla \phi$。在这种情况下，[斯托克斯方程](@entry_id:196346)的一个解是 $\boldsymbol{u} \equiv \boldsymbol{0}$ 和 $\nabla p = \nabla \phi$。这表明 $p = \phi + C$，其中 $C$ 是一个常数。只要 $\phi$ 不是常数，压力 $p$ 就是一个非平凡的空间函数，它精确地平衡了外加的体力。

#### 混合与纯[诺伊曼边界条件](@entry_id:142124)

当边界条件改变时，压力的唯一性也可能随之改变。

考虑边界 $\partial\Omega$ 分为狄利克雷部分 $\Gamma_D$ 和诺伊曼（Neumann）部分 $\Gamma_N$ 的情况，其中 $\Gamma_N$ 具有正测度。在 $\Gamma_N$ 上，我们施加一个应力（traction）边界条件 $\boldsymbol{\sigma}(\boldsymbol{u}, p)\boldsymbol{n} = \boldsymbol{g}$，其中 $\boldsymbol{\sigma} = 2\nu\boldsymbol{\varepsilon}(\boldsymbol{u}) - p\boldsymbol{I}$ 是[应力张量](@entry_id:148973)。此时，速度检验空间变为 $V = \{ \boldsymbol{v} \in H^1(\Omega)^d : \boldsymbol{v}|_{\Gamma_D} = \boldsymbol{0} \}$。我们再次考察积分 $\int_{\Omega} \nabla \cdot \boldsymbol{v} \, \mathrm{d}x = \int_{\partial\Omega} \boldsymbol{v} \cdot \boldsymbol{n} \, \mathrm{d}s$。由于 $\boldsymbol{v}$ 只在 $\Gamma_D$ 上为零，该积分变为 $\int_{\Gamma_N} \boldsymbol{v} \cdot \boldsymbol{n} \, \mathrm{d}s$。因为我们可以在 $\Gamma_N$ 上构造一个法向分量不为零的[检验函数](@entry_id:166589) $\boldsymbol{v} \in V$，所以这个积分通常不为零。因此，$b(\boldsymbol{v}, c)$ 不再对所有 $\boldsymbol{v} \in V$ 都为零。这意味着常数[压力模](@entry_id:159654)式在[弱形式](@entry_id:142897)中是“可见的”，压力不再具有任意常数的不确定性。物理上，应力边界条件隐式地在边界 $\Gamma_N$ 上固定了压力的“水平”，从而使得全域压力在 $L^2(\Omega)$ 中唯一。在这种情况下，我们无需施加零均值约束，可以直接取 $Q = L^2(\Omega)$。

在另一种极端情况，即纯[诺伊曼问题](@entry_id:176713)（或称纯应力问题），边界完全由 $\Gamma_N$ 构成。此时，速度检验空间是整个 $H^1(\Omega)^d$。分析表明，问题的算子核（kernel）变得更加复杂。不仅压力解具有任意常数的不确定性（因为没有任何狄利克雷边界来约束 $\int \nabla \cdot \boldsymbol{v}$），速度解本身也存在不唯一性，即可以任意添加一个**[刚体运动](@entry_id:193355)**（rigid body motion）。刚体运动 $\boldsymbol{r}(\boldsymbol{x}) = \boldsymbol{a} + \boldsymbol{S}\boldsymbol{x}$（其中 $\boldsymbol{a}$ 是平移向量，$\boldsymbol{S}$ 是反对称矩阵代表的[无穷小旋转](@entry_id:166635)）是那些使得[应变率张量](@entry_id:266108) $\boldsymbol{\varepsilon}(\boldsymbol{r})$ 为零的运动。对于这类问题，解的存在性要求外加载荷（体力 $\boldsymbol{f}$ 和边界应力 $\boldsymbol{t}$）必须与所有[刚体运动](@entry_id:193355)正交，这在物理上对应于总受力和总力矩的平衡。

### [有限元离散化](@entry_id:193156)

在建立了连续[弱形式](@entry_id:142897)之后，数值求解的第一步是将其离散化。伽辽金有限元法（Galerkin FEM）通过在连续函数空间 $V$ 和 $Q$ 的有限维[子空间](@entry_id:150286) $V_h \subset V$ 和 $Q_h \subset Q$ 中寻找近似解 $(\boldsymbol{u}_h, p_h)$ 来实现这一点。这些[子空间](@entry_id:150286)通常由定义在计算网格 $\mathcal{T}_h$ 上的分片多项式函数构成。

离散问题可以表述为：寻找 $(\boldsymbol{u}_h, p_h) \in V_h \times Q_h$，使得对于所有的 $(\boldsymbol{v}_h, q_h) \in V_h \times Q_h$ 均满足：
$$
\begin{aligned}
a(\boldsymbol{u}_h, \boldsymbol{v}_h) + b(\boldsymbol{v}_h, p_h) = (\boldsymbol{f}, \boldsymbol{v}_h) \\
b(\boldsymbol{u}_h, q_h) = 0
\end{aligned}
$$
如果我们选择 $V_h$ 和 $Q_h$ 的一组[基函数](@entry_id:170178)，$\{\boldsymbol{\phi}_i\}_{i=1}^{N_u}$ 和 $\{\psi_j\}_{j=1}^{N_p}$，并将解展开为 $\boldsymbol{u}_h = \sum_{i=1}^{N_u} U_i \boldsymbol{\phi}_i$ 和 $p_h = \sum_{j=1}^{N_p} P_j \psi_j$，上述[变分问题](@entry_id:756445)就转化为一个大型的线性[代数方程](@entry_id:272665)组。该[方程组](@entry_id:193238)通常写成如下的[分块矩阵](@entry_id:148435)形式：
$$
\begin{pmatrix} A & B^T \\ B & 0 \end{pmatrix} \begin{pmatrix} \mathbf{U} \\ \mathbf{P} \end{pmatrix} = \begin{pmatrix} \mathbf{F} \\ \mathbf{0} \end{pmatrix}
$$
其中矩阵的元素分别为 $A_{ij} = a(\boldsymbol{\phi}_j, \boldsymbol{\phi}_i)$，$B_{ji} = b(\boldsymbol{\phi}_i, \psi_j)$，$\mathbf{U}$ 和 $\mathbf{P}$ 是未知系数向量，$\mathbf{F}$ 是[载荷向量](@entry_id:635284)。这个系统是典型的[鞍点系统](@entry_id:754480)，其[系数矩阵](@entry_id:151473)是对称不定的。

### 离散稳定性的核心：[LBB条件](@entry_id:746626)

一个自然的问题是：是否任何速度和压力有限元空间 $V_h$ 和 $Q_h$ 的组合都能产生稳定且收敛的解？答案是否定的。离散[鞍点系统](@entry_id:754480)的稳定性和[适定性](@entry_id:148590)依赖于一个关键的[相容性条件](@entry_id:637057)，即**离散 [inf-sup 条件](@entry_id:174538)**，也称为 Ladyzhenskaya-Babuška-Brezzi (LBB) 条件。

LBB 条件要求存在一个与网格尺寸 $h$ 无关的正常数 $\beta > 0$，使得：
$$
\inf_{q_h \in Q_h \setminus \{0\}} \sup_{\boldsymbol{v}_h \in V_h \setminus \{\boldsymbol{0}\}} \frac{b(\boldsymbol{v}_h, q_h)}{\|\boldsymbol{v}_h\|_{V} \|q_h\|_{Q}} \ge \beta
$$
其中 $\|\cdot\|_{V}$ 和 $\|\cdot\|_{Q}$ 分别是速度空间 $V$ (通常是 $H^1$ 范数) 和压力空间 $Q$ (通常是 $L^2$ 范数) 上的范数。

直观地，LBB 条件保证了离散速度空间 $V_h$ 足够“丰富”，能够表示出足以“看见”任何离散[压力模](@entry_id:159654)式 $q_h$ 的散度场。换句话说，对于 $Q_h$ 中任何非零的压力函数，我们总能在 $V_h$ 中找到一个速度场，其散度与该压力函数有显著的（非零）耦合，并且这个[速度场](@entry_id:271461)的范数是受控的。

如果 LBB 条件不被满足（例如 $\beta$ 依赖于 $h$ 并在 $h \to 0$ 时趋于零），[分块矩阵](@entry_id:148435)系统会变得病态或奇异。这在计算上的后果是，压力解会变得极不稳定，常常出现非物理的、剧烈的空间[振荡](@entry_id:267781)，例如“棋盘格”（checkerboard）模式。

一个经典的 LBB 不稳定配对是使用**同阶连续分片[双线性](@entry_id:146819)元**（在四边形网格上记为 $\mathbb{Q}_1/\mathbb{Q}_1$）来近似速度和压力。在一个均匀的四边形网格上，可以构造一个特殊的离散[压力模](@entry_id:159654)式，其在网格节点上的值为 $p_h(x_i, y_j) = (-1)^{i+j}$。这个模式具有高频[振荡](@entry_id:267781)的棋盘格形状。通过直接计算可以证明，对于任意离散速度函数 $\boldsymbol{v}_h \in V_h$，耦合项 $b(\boldsymbol{v}_h, p_h) = -\int_{\Omega} p_h (\nabla \cdot \boldsymbol{v}_h) \, \mathrm{d}x$ 恒等于零。这意味着这个非零的[压力模](@entry_id:159654)式对于离散[散度算子](@entry_id:265975)来说是“不可见的”，它位于离散耦合算子伴随的核空间中。这直接违反了 LBB 条件，导致压力解中出现无法控制的伪影。

与此相反，有一些经典的有限元配对被证明是 LBB 稳定的。最著名的例子之一是**泰勒-胡德（Taylor-Hood）单元**，它通常使用比压力高一阶的多项式来近似速度（例如，$\mathbb{P}_2/\mathbb{P}_1$ 元，即速度为连续分片二次，压力为连续分片线性）。其稳定性证明通常比较复杂，一种经典的方法是**宏元技术**（macroelement technique）。该技术通过在由共享顶点的单元构成的局部“宏元”上证明一个局部的 [inf-sup 条件](@entry_id:174538)，然后利用单位分解等工具将局部结果“粘贴”成一个全局的稳定下界。[泰勒-胡德单元](@entry_id:165658)的稳定性源于其更丰富的[速度空间](@entry_id:181216)，它拥有额外的自由度（如边中点节点），足以控制低阶压力空间中的所有模式。

### 稳定化方法：克服[LBB条件](@entry_id:746626)的限制

尽管泰勒-胡德等单元是稳定的，但它们在实现上比同阶单元更为复杂。在许多应用中，出于[计算效率](@entry_id:270255)和简便性的考虑，人们仍然希望使用同阶单元（如 $\mathbb{P}_1/\mathbb{P}_1$ 或 $\mathbb{Q}_1/\mathbb{Q}_1$）。为了弥补这些单元在 LBB 条件上的缺陷，研究者们开发了多种**稳定化方法**。这些方法通过向原始的[弱形式](@entry_id:142897)中添加额外的、经过精心设计的项来修正离散系统。

这些稳定化项通常具有两个关键特征：
1.  **一致性 (Consistency)**：对于连续问题的精确解，这些附加项为零。这保证了稳定化方法不会改变原始问题的解，只是改变了其离散近似的性质。
2.  **稳定性 (Stability)**：附加项能有效抑制不稳定的[压力模](@entry_id:159654)式，从而恢复整个离散系统的[适定性](@entry_id:148590)。

以下是几种主流的稳定化策略：

#### 压力稳定化/[彼得罗夫-伽辽金方法](@entry_id:753372) (PSPG)

PSPG 方法是一种基于残差的稳定化技术。其核心思想是在离散的[连续性方程](@entry_id:195013)（即 $b(\boldsymbol{u}_h, q_h)=0$）中添加一个与动量方程[残差相关](@entry_id:754268)的项。例如，一个常见的 PSPG 形式是添加如下稳定化项：
$$
S_{PSPG}(\boldsymbol{u}_h, p_h; q_h) = \sum_{K \in \mathcal{T}_h} \tau_K \int_K (-\nu \Delta \boldsymbol{u}_h + \nabla p_h - \boldsymbol{f}) \cdot \nabla q_h \, \mathrm{d}x
$$
其中 $\tau_K$ 是一个依赖于局部网格尺寸和物理参数的稳定化参数。该方法是一致的，因为当 $(\boldsymbol{u}_h, p_h)$ 是精确解时，动量方程残差为零。从稳定性的角度看，该项中的 $\int_K (\nabla p_h) \cdot (\nabla q_h)$ 部分提供了一个对压力梯度的控制，有效抑制了棋盘格等高频[振荡](@entry_id:267781)模式。

#### [局部投影](@entry_id:139486)稳定化 (LPS)

LPS 是一种更精细的压力稳定化方法。它只针对压[力场](@entry_id:147325)中无法被更低阶多项式空间所表示的“小尺度”或“[子网](@entry_id:156282)格”部分进行惩罚。其稳定化项通常具有如下形式：
$$
S_{LPS}(p_h; q_h) = \sum_{K \in \mathcal{T}_h} \tau_K \int_K (\nabla p_h - \Pi_h^{k-1} \nabla p_h) \cdot (\nabla q_h - \Pi_h^{k-1} \nabla q_h) \, \mathrm{d}x
$$
其中 $\Pi_h^{k-1}$ 是到一个断裂的、低一阶（$k-1$ 阶）多项式空间的局部 $L^2$ 投影。这种方法通过仅作用于“未解出的”压力波动，避免了对解的大尺度部分的过度阻尼，从而在恢复稳定性的同时能更好地保持高阶[收敛率](@entry_id:146534)。

#### Grad-div 稳定化

Grad-div 稳定化方法在动量方程的[弱形式](@entry_id:142897)中添加了一个惩罚[速度散度](@entry_id:264117)的项：
$$
S_{GD}(\boldsymbol{u}_h; \boldsymbol{v}_h) = \gamma \int_{\Omega} (\nabla \cdot \boldsymbol{u}_h) (\nabla \cdot \boldsymbol{v}_h) \, \mathrm{d}x
$$
其中 $\gamma > 0$ 是一个用户定义的惩罚系数。需要明确的是，Grad-div 稳定化本身**并不**修复压力空间的 LBB 条件缺陷，因此它不能单独用来抑制压力[振荡](@entry_id:267781)。它的主要作用是改善速度近似的质量，特别是增强其**[压力鲁棒性](@entry_id:167963)**（pressure robustness）。

[压力鲁棒性](@entry_id:167963)指的是速度误差对压力大小不敏感的特性。在许多标准有限元方法中，当体力是无旋的（irrotational），即 $\boldsymbol{f} = \nabla \phi$ 时，速度的精确解为零，而压力则很大（$p \approx \phi$）。然而，由于离散误差，计算出的速度 $\boldsymbol{u}_h$ 往往不为零，并且其[误差范数](@entry_id:176398)可能与压力的大小（以及粘度 $\nu$ 的倒数）成正比，即 $\lVert \boldsymbol{u}_h \rVert_{L^2} \propto 1/\nu$。这是一种非物理的耦合。Grad-div 稳定化通过在 $L^2$ 意义上更强地强制执行 $\nabla \cdot \boldsymbol{u}_h \approx 0$，显著减弱了这种依赖性，使得速度误差对压力不敏感。

我们可以通过一个数值思想实验来清晰地看到这一点。考虑一个具有无旋[体力](@entry_id:174230) $\boldsymbol{f} = \nabla \phi$ 的问题，其精确速度解 $\boldsymbol{u}=\boldsymbol{0}$。
- 使用不含稳定化的标准同阶单元离散，当粘度 $\nu$ 减小时，计算出的速度范数 $\lVert \boldsymbol{u}_h \rVert_{L^2}$ 会显著增大，表现出 $\mathcal{O}(1/\nu)$ 的行为。
- 在此基础上添加 Grad-div 稳定化项（例如，取 $\gamma=1$），这种范数的增长趋势会得到有效抑制，即使 $\nu$ 很小，速度解也能保持接近于零。

因此，现代高性能的斯托克斯求解器通常会结合使用这些稳定化技术。例如，将 PSPG 或 LPS 与 Grad-div 稳定化相结合，前者负责控制压力[振荡](@entry_id:267781)，保证压[力场](@entry_id:147325)的稳定性和准确性；后者则负责解耦速度与压力的误差，提供压力鲁棒的[速度场](@entry_id:271461)近似。这种协同作用使得即使在[对流](@entry_id:141806)占优或压力梯度剧烈变化等挑战性问题中，也能获得可靠的数值解。