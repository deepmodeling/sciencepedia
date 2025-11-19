## 引言
在理论物理学的广阔天地中，对称性是指导我们理解自然法则的基本原则。[共形场论](@entry_id:145449)（CFT）是描述那些在尺度变换下保持不变的物理系统的强大框架，它在[临界现象](@entry_id:144727)、弦论和[量子引力](@entry_id:145111)等领域扮演着核心角色。然而，一个根本性的问题摆在我们面前：大多数共形场论是在没有优选时间方向的[欧几里得空间](@entry_id:138052)中定义的，那么我们如何像在标准量子力学中那样，定义一个态空间（[希尔伯特空间](@entry_id:261193)）和时间演化呢？这个知识空白正是本文旨在填补的核心。

本文将深入探讨**径向量子化**——一个优雅而深刻的观念，它彻底改变了我们对[量子场论](@entry_id:138177)中“时间”和“演化”的看法，为欧几里得[共形场论](@entry_id:145449)提供了坚实的量子力学基础。通过学习本文，您将掌握这一强大工具的精髓，并理解其在不同物理分支中的广泛应用。

- 在“**原理和机制**”一章中，我们将建立径向量子化的基本思想，即以径向距离为“时间”，并由此引出革命性的状[态-算符对应](@entry_id:156407)。我们将看到扩张算符如何扮演[哈密顿量](@entry_id:172864)的角色，并深入探索[二维共形场论](@entry_id:148817)中由[Virasoro代数](@entry_id:143942)带来的丰富结构。

- 接着，在“**应用与跨学科联系**”一章中，我们将展示径向量子化远非一个抽象的形式体系。我们将探索它如何被用作计算工具，以及它如何成为连接统计物理中的热现象、[弦论](@entry_id:145688)中的[D-膜](@entry_id:147530)动力学以及量子引力中[全息原理](@entry_id:136306)的桥梁。

- 最后，在“**动手实践**”部分，您将通过具体的计算问题，将理论知识转化为实践技能，从而加深对[希尔伯特空间](@entry_id:261193)结构、关联函数和对称性约束的理解。

让我们一同开启这段旅程，揭示径向量子化如何将抽象的[代数结构](@entry_id:137052)与可观测的物理世界精妙地联系在一起。

## 原理和机制

在介绍性章节中，我们概述了共形场论（CFT）作为描述尺度不变系统在[临界点](@entry_id:144653)行为的通用框架。现在，我们深入探讨其核心原理和机制，重点关注使[共形场论](@entry_id:145449)成为一个可解的[量子场论](@entry_id:138177)框架的数学结构。本章的中心思想是**径向量子化（radial quantization）**，它为欧几里得时空中的共形场论提供了一个[希尔伯特空间](@entry_id:261193)（Hilbert space）和一个[哈密顿量](@entry_id:172864)（Hamiltonian），从而在根本上改变了我们对[量子场论](@entry_id:138177)中“时间”和“演化”的看法。

### 状态算符对应

在传统的[量子场论](@entry_id:138177)中，我们习惯于在一个具有时间方向的洛伦兹时空中进行量子化。理论由作用在希尔伯特空间上的局域算符代数和描述系统时间演化的[哈密顿量](@entry_id:172864)构成。然而，欧几里得共形场论是在一个没有优选时间方向的欧几里得空间中定义的。那么，我们如何定义一个量子力学系统所必需的[希尔伯特空间](@entry_id:261193)和[时间演化](@entry_id:153943)呢？

**径向量子化**提供了一个优雅的答案。其核心思想是将径向距离 $r = |x|$ 视为“时间”。这样，以原点为中心的同心球面（在二维情况下是同心圆）就扮演了等“时间”面的角色。算符的径向演化，即从一个小球面移动到一个大球面，就等价于时间演化。

这一观念引出了共形场论中最深刻和最有力的概念之一：**状[态-算符对应](@entry_id:156407)（state-operator correspondence）**。它断言，在径向量子化方案中，[希尔伯特空间](@entry_id:261193) $\mathcal{H}$ 中的态与插入在原点的局域算符之间存在一一对应关系。具体来说，任何局域算符 $\mathcal{O}(x)$，当其插入点 $x$ 趋于原点时，会从真空态 $|0\rangle$ 中创生一个相应的态 $|\mathcal{O}\rangle$：

$$
|\mathcal{O}\rangle = \lim_{x \to 0} \mathcal{O}(x)|0\rangle
$$

反之，希尔伯特空间中的每一个态都对应一个唯一的局域算符。在这个对应关系中，真空态 $|0\rangle$ 本身对应于单位算符 $\mathbb{I}$。

与时间演化由[哈密顿量](@entry_id:172864)生成类似，径向演化由标度[变换的生成元](@entry_id:172031)——**扩张算符（dilatation operator）** $D$ ——所生成。因此，在径向量子化中，$D$ 扮演了[哈密顿量](@entry_id:172864)的角色，$H_{\text{rad}} = D$。具有确定标度维度 $\Delta$ 的算符 $\mathcal{O}$ 所对应的态 $|\mathcal{O}\rangle$ 是[哈密顿量](@entry_id:172864)的本征态，其能量就是标度维度 $\Delta$：

$$
D |\mathcal{O}\rangle = \Delta |\mathcal{O}\rangle
$$

这个关系是连接算符的代数性质（标度维度）和态的物理性质（能量）的关键桥梁。

### 共形场论的希尔伯特空间

一个完整的量子理论不仅需要态空间，还需要一个定义了态之间范数和正交性的[内积](@entry_id:158127)。状[态-算符对应](@entry_id:156407)同样为我们提供了定义[内积](@entry_id:158127)的方法。两个态 $|\mathcal{O}_1\rangle$ 和 $|\mathcal{O}_2\rangle$ 的[内积](@entry_id:158127) $\langle \mathcal{O}_1 | \mathcal{O}_2 \rangle$ 与它们对应算符在欧几里得平面上的两点关联函数直接相关。

对于一个由算符 $\mathcal{O}(x)$ 创生的态 $|\mathcal{O}\rangle$，其共轭态 $\langle \mathcal{O}|$ 对应于伴随算符 $\mathcal{O}^\dagger(x)$ 在无穷远处的插入。在二维情况下，通过共形变换 $z \to 1/z^*$，可以将无穷远处的点[拉回](@entry_id:160816)到原点。这个变换将算符 $\mathcal{O}(z, \bar{z})$ 映射到其伴随算符，因此[内积](@entry_id:158127)可以被定义为：

$$
\langle \mathcal{O}_1 | \mathcal{O}_2 \rangle = \lim_{z,w \to 0} \langle 0 | \mathcal{O}_1^\dagger(z) \mathcal{O}_2(w) | 0 \rangle = \langle \mathcal{O}_1^\dagger(1) \mathcal{O}_2(0) \rangle
$$

对于满足 $\langle \phi_i | \phi_j \rangle = \delta_{ij}$ 的正交归一化的**主算符（primary operators）** $\phi_i$，它们创生的**主态（primary states）** $|\phi_i\rangle$ 构成了[希尔伯特空间](@entry_id:261193)的一组正交基。这意味着不同主算符的两点函数为零，而一个主算符与其自身的两点函数则被归一化。

这个构造的威力在于，我们可以计算由复杂算符（如[张量算符](@entry_id:203590)）创生的态的范数。考虑一个由[能量-动量张量](@entry_id:203902) $T_{\mu\nu}$ 创生的态，它是一个标度维度为 $\Delta_T = d$ 的主算符。在 $d$ 维CFT中，其[对应态](@entry_id:145033)的[内积](@entry_id:158127)由两点函数给出。例如，考虑一个由任意常数矢量 $a^\mu$ 和 $b^\mu$ 与能量-动量张量缩并而成的算符所创生的态 $|\Psi\rangle = a^\mu b^\nu |T_{\mu\nu}\rangle$ [@problem_id:362579]。其平方范数 $\langle \Psi | \Psi \rangle$ 的计算过程如下：

$$
\langle \Psi | \Psi \rangle = a^\mu b^\nu a^\rho b^\sigma \langle T_{\mu\nu} | T_{\rho\sigma} \rangle
$$

其中 $\langle T_{\mu\nu} | T_{\rho\sigma} \rangle$ 是[能量-动量张量](@entry_id:203902)的两点函数在算符-态对应下的形式，对于一个对称[无迹张量](@entry_id:274053)，它具有特定的张量结构：

$$
\langle T_{\mu\nu} | T_{\rho\sigma} \rangle = C_T \left[ \frac{1}{2}(\delta_{\mu\rho}\delta_{\nu\sigma} + \delta_{\mu\sigma}\delta_{\nu\rho}) - \frac{1}{d}\delta_{\mu\nu}\delta_{\rho\sigma} \right]
$$

这里的 $C_T$ 是一个正常数，其大小与理论的“[中心荷](@entry_id:155921)”有关，表征了理论中自由度的数量。通过代入并利用克罗内克符号 $\delta$ 进行[指标缩并](@entry_id:180403)，我们可以得到态 $|\Psi\rangle$ 的范数：

$$
\langle \Psi | \Psi \rangle = a^\mu b^\nu a^\rho b^\sigma C_T \left[ \frac{1}{2}(\delta_{\mu\rho}\delta_{\nu\sigma} + \delta_{\mu\sigma}\delta_{\nu\rho}) - \frac{1}{d}\delta_{\mu\nu}\delta_{\rho\sigma} \right] \\
= C_T \left[ \frac{1}{2}(a^\mu a_\mu)(b^\nu b_\nu) + \frac{1}{2}(a^\mu b_\mu)(a^\nu b_\nu) - \frac{1}{d}(a^\mu b_\mu)(a^\rho b_\rho) \right] \\
= C_T \left[ \frac{1}{2} (a \cdot a) (b \cdot b) + \left(\frac{1}{2} - \frac{1}{d}\right) (a \cdot b)^2 \right] = C_T \left[ \frac{1}{2} (a \cdot a) (b \cdot b) + \frac{d-2}{2d} (a \cdot b)^2 \right]
$$

这个计算明确地展示了希尔伯特空间的[内积](@entry_id:158127)结构是如何由算符的关联函数所决定的。

### 一般维度下的径向量子化

在任意维度 $d$ 的欧几里得CFT中，[守恒流](@entry_id:148966)的存在意味着有相应的[守恒荷](@entry_id:145660)。对于[共形对称性](@entry_id:142366)，相关的[守恒流](@entry_id:148966)是对称、无迹的[能量-动量张量](@entry_id:203902) $T^{\mu\nu}$。扩张算符 $D$ 作为与[标度变换](@entry_id:166413)相关的荷，可以表示为 $T^{\mu\nu}$ 在一个等“时间”面上的积分：

$$
D = \int_{S_R} dS_\mu \, x_\nu T^{\mu\nu}(x)
$$

其中积分是在一个半径为 $R$ 的 $(d-1)$ 维球面 $S_R$ 上进行的，$dS_\mu = n_\mu dS$ 是矢量面积元，$n_\mu = x_\mu/R$ 是向外的[单位法向量](@entry_id:178851)。

这个积分形式的美妙之处在于，由于 $T^{\mu\nu}$ 的守恒性（$\partial_\mu T^{\mu\nu} = 0$），积分的值不依赖于球面半径 $R$。这使我们能够通过形变积分围道来计算算符的对易子。例如，要计算 $[D, \phi(y)]$，我们可以将 $D$ 的积分围道从一个大球面收缩到一个包围点 $y$ 的无穷小球面上。

这个计算过程揭示了扩张算符作用的本质 [@problem_id:362682]。当我们将积分围道收缩到 $y$ 附近时，积分只对 $T^{\mu\nu}(x)$ 和 $\phi(y)$ 在 $x \to y$ 时的**[算符乘积展开](@entry_id:141941)（Operator Product Expansion, OPE）**的奇异项敏感。对于一个标量主算符 $\phi(y)$，其OPE具有如下形式：

$$
T^{\mu\nu}(x)\phi(y) \sim C \left( d \frac{(x-y)^\mu (x-y)^\nu}{|x-y|^2} - \delta^{\mu\nu} \right) \frac{\phi(y)}{|x-y|^d} + \dots \quad \text{for } x \to y
$$

通过在 $y$ 周围的一个无穷小球面上计算 $D$ 的积分，我们可以直接评估对易子 $[D, \phi(y)]$。其结果恰好是标度变换作用在场 $\phi(y)$ 上的形式：

$$
[D, \phi(y)] = -\left(y^\mu \frac{\partial}{\partial y^\mu} + \Delta\right) \phi(y)
$$

其中，标度维度 $\Delta$ 与OPE系数 $C$、时空维度 $d$ 以及单位 $(d-1)$ 维球面的面积 $S_d = \frac{2\pi^{d/2}}{\Gamma(d/2)}$ 直接相关，具体为 $\Delta = -C(d-1)S_d$。这个结果完美地体现了CFT的[自洽性](@entry_id:160889)：算符的代数性质（OPE）决定了它在对称性下的变换规律（标度维度）。特别地，当算符位于原点 $y=0$ 时，我们有 $[D, \phi(0)] = -\Delta\phi(0)$。将此作用于真空态，并利用状[态-算符对应](@entry_id:156407)，我们便得到 $D|\phi\rangle = \Delta|\phi\rangle$，这正是我们之前断言的[哈密顿量](@entry_id:172864)本征方程。

### 二维的丰富性：[Virasoro代数](@entry_id:143942)

当维度 $d=2$ 时，共形[对称群](@entry_id:146083)从有限维的 $SO(3,1)$（或欧几里得的 $SO(2,2)$）变为无穷维的。这导致了极为丰富的[代数结构](@entry_id:137052)。在复坐标 $z=x_1+ix_2$ 和 $\bar{z}=x_1-ix_2$下，任意的[全纯函数](@entry_id:158563) $z \to f(z)$ 都是一个[共形变换](@entry_id:159863)。这些无穷多的对称性由[能量-动量张量](@entry_id:203902)的全纯部分 $T(z)$ 和反全纯部分 $\bar{T}(\bar{z})$ 的模（modes）生成。

全纯部分的生成元被称为**[Virasoro生成元](@entry_id:190266)** $L_n$，定义为 $T(z)$ 在原点周围的洛朗展开的系数：

$$
L_n = \oint_C \frac{dz}{2\pi i} z^{n+1} T(z)
$$

其中围道 $C$ 包围原点。这些生成元构成**[Virasoro代数](@entry_id:143942)**：

$$
[L_m, L_n] = (m-n)L_{m+n} + \frac{c}{12}(m^3-m)\delta_{m+n,0}
$$

这里的常数 $c$ 是一个至关重要的参数，称为**[中心荷](@entry_id:155921)（central charge）**。它是理论的一个基本特征，衡量了[量子涨落](@entry_id:154889)对[共形对称性](@entry_id:142366)产生的反常（anomaly）。

在二维径向量子化中，$L_0$ 和 $\bar{L}_0$ 的角色尤为重要。扩张算符（[哈密顿量](@entry_id:172864)）是 $D = L_0 + \bar{L}_0$，而[旋转生成元](@entry_id:154292)是 $M = L_0 - \bar{L}_0$。因此，$L_0$ 衡量了态的全纯**[共形权重](@entry_id:182513)（conformal weight）** $h$，而 $\bar{L}_0$ 衡量反全纯[共形权重](@entry_id:182513) $\bar{h}$。标度维度 $\Delta = h+\bar{h}$，自旋 $s = h-\bar{h}$。

一个[共形权重](@entry_id:182513)为 $h$ 的全纯[主场](@entry_id:153633) $\phi(w)$，在状[态-算符对应](@entry_id:156407)下，创生一个**主态** $|h\rangle = \phi(0)|0\rangle$。这个态是[Virasoro代数](@entry_id:143942)的**最高权重态（highest-weight state）**，它满足：
1. $L_0|h\rangle = h|h\rangle$ （能量本征态）
2. $L_n|h\rangle = 0$ for $n > 0$ （被所有“上升”算符湮灭）

[Virasoro生成元](@entry_id:190266)在关联函数上的作用可以通过[围道积分](@entry_id:169446)和OPE来计算。对任意关联函数的作用 $L_k \langle \dots \rangle$ 定义为包含所有算符插入点的围道积分。通过形变围道，这个作用可以分解为围绕每个算符的局部贡献之和 [@problem_id:362591]。对单个[主场](@entry_id:153633) $\phi(w)$ 的作用等价于计算对易子 $[L_k, \phi(w)]$，这又是由 $T(z)$ 和 $\phi(w)$ 的OPE决定的：

$$
T(z)\phi(w) \sim \frac{h}{(z-w)^2}\phi(w) + \frac{1}{z-w}\partial_w \phi(w) + O(1)
$$

利用留数定理，可以发现 $[L_k, \phi(w)]$ 等价于一个作用在 $\phi(w)$ 上的[微分](@entry_id:158718)算符。例如，计算 $L_k$ 对两点函数 $\langle \phi(w)\phi(0) \rangle$ 的作用时，来自 $w$ 点的贡献 $\mathcal{A}_k(w)$ 可以通过计算 $z$ 在 $w$ 附近的[围道积分](@entry_id:169446)得到，结果为 $\mathcal{A}_k(w) = (w^{k+1}\partial_w + h(k+1)w^k) \langle \phi(w) \phi(0) \rangle$。代入两点函数 $\langle \phi(w)\phi(0) \rangle = w^{-2h}$，我们得到一个具体的表达式 $h(k-1)w^{k-2h}$。这展示了OPE如何将抽象的代数作用转化为具体的[微分](@entry_id:158718)运算。

### 构建谱：[Verma模](@entry_id:201926)和[后代态](@entry_id:153392)

一旦我们有了主态，整个希尔伯特空间就可以通过作用[Virasoro代数](@entry_id:143942)的“下降”算符 $L_{-n}$（$n>0$）来构建。由一个主态 $|h\rangle$ 和所有 $L_{-n_1}\dots L_{-n_k}$ 作用生成的态的集合，构成了一个称为**[Verma模](@entry_id:201926)（Verma module）** $V(c,h)$ 的表示空间。

$$
V(c,h) = \text{span} \{ L_{-n_1} \dots L_{-n_k} |h\rangle \mid n_i > 0, k \ge 0 \}
$$

这些被称为**[后代态](@entry_id:153392)（descendant states）**的态也是 $L_0$ 的本征态，其[共形权重](@entry_id:182513)为 $h+N$，其中 $N = \sum n_i$ 称为**能级（level）**。

[希尔伯特空间](@entry_id:261193)的[内积](@entry_id:158127)结构由[厄米共轭](@entry_id:191215)性质 $L_n^\dagger = L_{-n}$ 和主态的正交归一性 $\langle h | h \rangle = 1$ 所确定。这使得我们可以计算任意[后代态](@entry_id:153392)之间的[内积](@entry_id:158127)。在任意能级 $N$，我们可以选择一组基（例如，按 $n_i$ 排序的 $L_{-n_1}\dots L_{-n_k}$ ），然后计算它们之间的[内积](@entry_id:158127)矩阵，即**[Gram矩阵](@entry_id:148915)** $M_N(c,h)$。

例如，在能级2，[基态](@entry_id:150928)可以选为 $|v_1\rangle = L_{-2}|h\rangle$ 和 $|v_2\rangle = L_{-1}^2|h\rangle$。它们之间的[内积](@entry_id:158127)可以通过反复使用[Virasoro代数](@entry_id:143942)对易关系和主态条件来计算 [@problem_id:362729]：
*   $\langle v_1 | v_1 \rangle = \langle h | L_2 L_{-2} | h \rangle = \langle h | [L_2, L_{-2}] | h \rangle = \langle h | (4L_0 + \frac{c}{2}) | h \rangle = 4h + \frac{c}{2}$
*   $\langle v_1 | v_2 \rangle = \langle h | L_2 L_{-1}^2 | h \rangle = 6h$
*   $\langle v_2 | v_2 \rangle = \langle h | L_1^2 L_{-1}^2 | h \rangle = 8h^2 + 4h$

[Gram矩阵](@entry_id:148915)为：
$$
M_2 = 
\begin{pmatrix}
4h + \frac{c}{2} & 6h \\
6h & 8h^2 + 4h
\end{pmatrix}
$$
这个[矩阵的行列式](@entry_id:148198)，即**Kac[行列式](@entry_id:142978)**，$\det(M_2) = 2h(16h^2 + (2c-10)h + c)$，在决定表示是否包含**[零态](@entry_id:154996)（null states）**——即范数为零的非[零态](@entry_id:154996)——方面起着核心作用。如果对于某些 $(c,h)$ 值，Kac[行列式](@entry_id:142978)为零，那么[Verma模](@entry_id:201926)是可约的，存在[零态](@entry_id:154996)。这些[零态](@entry_id:154996)及其后代必须从[希尔伯特空间](@entry_id:261193)中被移除，从而得到一个更小的不可约表示。[零态](@entry_id:154996)的存在对关联函数施加了强大的约束，通常表现为[微分方程](@entry_id:264184)。例如，从 $M_2$ 的[逆矩阵](@entry_id:140380)元素 $(M_2^{-1})_{11} = \frac{2(2h + 1)}{16h^2 + (2c - 10)h + c}$ 可以看出，当分母（即Kac[行列式](@entry_id:142978)）为零时，[逆矩阵](@entry_id:140380)发散，预示着结构的退化。

OPE不仅编码了主算符之间的融合，还包含了后代算符的信息。例如，在OPE $\phi_a \times \phi_b$ 中出现的 $L_{-1}\phi_p$ 项，对应于一个能级1的[后代态](@entry_id:153392)。我们可以计算这些由算符融合产生的[后代态](@entry_id:153392)之间的[内积](@entry_id:158127) [@problem_id:362592]。例如，两个分别由 $\phi_a \times \phi_b$ 和 $\phi_c \times \phi_d$ 融合产生的、处于同一[主场](@entry_id:153633) $\phi_p$ 的能级1[后代态](@entry_id:153392)的[内积](@entry_id:158127)，可以直接通过[Virasoro代数](@entry_id:143942)计算得出，结果依赖于相关场的[共形权重](@entry_id:182513)。这再次表明了OPE、[Virasoro代数](@entry_id:143942)和[希尔伯特空间](@entry_id:261193)结构之间的深刻联系。

我们甚至可以推导 $T(z)$ 与后代场的OPE，从而计算后代场与[Virasoro生成元](@entry_id:190266)的对易子。例如，通过对 $T(z)\phi(w)$ 的OPE对 $w$ 求导，我们可以得到 $T(z)\partial\phi(w)$ 的OPE，并用它来计算 $[L_1, \partial\phi(0)]$，结果为 $2h\phi(0)$ [@problem_id:362721]。这表明后代场在共形变换下的行为比主场更复杂，它们会混合到其他场中。

### 共形变换和物理后果

径向量子化将欧几里得平面与一个时空为 $\mathbb{R} \times S^1$ 的圆柱体联系起来。[共形变换](@entry_id:159863) $z = \exp(2\pi w/L)$ 将复平面（除去原点）映射到一个周长为 $L$ 的无限长圆柱体上，其中 $w = \tau + ix$ 是圆柱坐标。平面上的同心圆（等径向时间面）被映射到圆柱体上的等时间[截面](@entry_id:154995)（$x$ 坐标构成的圆）。因此，平面上的径向演化（由 $D = L_0+\bar{L}_0$ 生成）与圆柱体上的[时间演化](@entry_id:153943)（由[哈密顿量](@entry_id:172864) $H$ 生成）是等价的。

然而，能量-动量张量在从平坦的复平面到弯曲的圆柱体的[坐标变换](@entry_id:172727)下，其变换不是协变的，而是出现一个反常项，该项由**[施瓦茨导数](@entry_id:161840)（Schwarzian derivative）** $\{z, w\}$ 描述：

$$
T_{\text{cyl}}(w) = \left(\frac{\partial z}{\partial w}\right)^2 T_{\text{plane}}(z(w)) + \frac{c}{12} \{z,w\}
$$

由于平面上的[真空期望值](@entry_id:146340) $\langle T_{\text{plane}}(z) \rangle_{\text{plane}} = 0$，圆柱体上的能量-动量张量将获得一个非零的[真空期望值](@entry_id:146340)：

$$
\langle T_{\text{cyl}}(w) \rangle_{\text{cyl}} = \frac{c}{12} \{z,w\}
$$

对于映射 $z = \exp(2\pi w/L)$，[施瓦茨导数](@entry_id:161840)为一个常数 $\{z,w\} = -2\pi^2/L^2$。这导致了一个非零的[真空能](@entry_id:155067)量密度 [@problem_id:362704]。圆柱体上的[哈密顿量](@entry_id:172864) $H$ 与[Virasoro生成元](@entry_id:190266) $L_0^{(\text{cyl})}$ 和 $\bar{L}_0^{(\text{cyl})}$ 相关。$L_0^{(\text{cyl})}$ 的[真空期望值](@entry_id:146340) $\langle L_0^{(\text{cyl})} \rangle$ 可以通[过积分](@entry_id:753033) $\langle T_{\text{cyl}} \rangle$ 得到，结果为 $-c/24$。因此，圆柱体上的真空能量，即**[卡西米尔能量](@entry_id:149660)（Casimir energy）**，为：

$$
E_{\text{Casimir}} = \langle H \rangle = \frac{2\pi}{L} (\langle L_0^{(\text{cyl})} \rangle + \langle \bar{L}_0^{(\text{cyl})} \rangle) = \frac{2\pi}{L} \left(-\frac{c}{24} - \frac{c}{24}\right) = -\frac{\pi c}{6L}
$$

这个著名的结果表明，在一个有限尺寸的空间中，[量子真空](@entry_id:155581)本身具有负能量，这是一种纯粹的量子效应，其大小由[中心荷](@entry_id:155921) $c$ 和系统尺寸 $L$ 决定。这个反常项也影响了关联函数，例如，[能量-动量张量](@entry_id:203902)在圆柱体上的两点函数会包含一个由[施瓦茨导数](@entry_id:161840)产生的常数项，以及一个与[双曲函数](@entry_id:165175)相关的项 [@problem_id:362622]。

### [算符乘积展开](@entry_id:141941)：理论的基因密码

在整个讨论中，OPE反复出现，成为连接不同概念的纽带。事实上，OPE可以被视为一个CFT的“基因密码”。它不仅编码了算符在短距离下的行为，还通过其**[结构常数](@entry_id:157960)（structure constants）** $C_{ijk}$（也称为OPE系数）编码了理论的[融合规则](@entry_id:142240)：

$$
\phi_i(z) \phi_j(0) = \sum_k C_{ij}^k |z|^{h_k - h_i - h_j} (\phi_k(0) + \text{descendants})
$$

理论的全部动力学信息——谱（哪些主场存在）和相互作用（$C_{ijk}$）——都包含在OPE中。关联函数的一致性，特别是四点函数的[交叉对称性](@entry_id:145431)，对这些OPE系数施加了强大的自洽约束，这构成了现代**[共形自举](@entry_id:153253)（conformal bootstrap）**方法的基础。

反过来，如果我们知道一个理论的关联函数，我们就可以通过分析其在特定极限下的行为来提取OPE数据。一个经典的例子是[二维临界伊辛模型](@entry_id:152466)，其主场包括自旋场 $\sigma$（权重 $h=1/16$）和能量场 $\epsilon$（权重 $h=1/2$）。其四点[自旋关联](@entry_id:201234)函数是已知的。通过考察 $z_1 \to z_2$ 的极限，我们可以将四点函数展开为 $z_{12}=z_1-z_2$ 的[幂级数](@entry_id:146836)。这个展开的每一项都对应于OPE中某个算符及其后代的贡献。例如，$\sigma \times \sigma$ 的OPE包含单位算符 $\mathbb{I}$ 和能量算符 $\epsilon$。通过将四点函数的展开式与OPE的预测形式进行比较，我们可以精确地提取出OPE系数，如 $C_{\sigma\sigma\epsilon}^2 = 1/4$ [@problem_id:362724]。这个过程展示了如何从可观测的量（关联函数）中解码出理论的基本[代数结构](@entry_id:137052)（OPE系数）。

总结而言，径向量子化为欧几里得CFT提供了一个坚实的量子力学诠释。它将算符代数、希尔伯特空间谱和关联函数紧密地联系在一起，形成一个高度自洽和强大的理论框架。尤其是在二维情况下，[Virasoro代数](@entry_id:143942)的无穷对称性使得许多模型可以被精确求解，为我们理解[相变](@entry_id:147324)和[量子引力](@entry_id:145111)等广泛的物理现象提供了宝贵的见解。