## 引言
[Bochner恒等式](@entry_id:193184)是现代几何分析的基石之一，它以一个看似简单的[微分](@entry_id:158718)公式，深刻地揭示了黎曼流形的局部几何（曲率）与其上的分析学（微分算子与函数性质）之间的内在联系。然而，一个核心问题是：这样一个点态的计算恒等式，是如何转化为强大的工具，用以推断[流形](@entry_id:153038)的[全局几何](@entry_id:197506)、拓扑结构乃至谱性质的？理解这一转化过程，是掌握[Bochner技巧](@entry_id:196927)并将其应用于研究的关键所在。

本文旨在系统性地回答这一问题。在**第一章“原理与机制”**中，我们将从[黎曼几何](@entry_id:160508)的基本算子出发，详细推导函数上的经典[Bochner恒等式](@entry_id:193184)，并将其推广至[微分形式](@entry_id:146747)的Weitzenböck恒等式以及[Bakry-Émery理论](@entry_id:635411)的框架。随后的**第二章“应用与交叉学科联系”**将展示这些恒等式的威力，探讨其在证明[Lichnerowicz特征值估计](@entry_id:192504)、Bochner消失定理、Cheeger-Gromoll[分裂定理](@entry_id:197795)以及在[里奇流](@entry_id:145202)理论中的关键作用。最后，在**第三章“动手实践”**中，您将通过具体的计算练习，亲手运用[Bochner技巧](@entry_id:196927)解决问题，从而将理论知识内化为分析能力。通过这三章的学习，读者将能够全面掌握[Bochner恒等式](@entry_id:193184)的理论精髓与应用[范式](@entry_id:161181)。

## 原理与机制

本章旨在深入探讨[Bochner恒等式](@entry_id:193184)及其相关推广的核心原理与机制。我们将从黎曼几何中最基本的微分算子出发，逐步建立起函数上的经典[Bochner恒等式](@entry_id:193184)，并阐释其在[几何分析](@entry_id:157700)中的深刻应用。随后，我们将这一思想推广至更广阔的领域，包括[Bakry-Émery理论](@entry_id:635411)中的[加权拉普拉斯算子](@entry_id:634510)以及微分形式上的Weitzenböck恒等式，最终揭示这些恒等式如何将[流形](@entry_id:153038)的曲率与分析性质紧密联系起来。

### [黎曼几何](@entry_id:160508)中的基本算子

在进入[Bochner恒等式](@entry_id:193184)的核心内容之前，我们必须首先精确定义在其上构建的几个基本微分算子。设 $(M^n, g)$ 是一个光滑的 $n$ 维[黎曼流形](@entry_id:261160)，其Levi-Civita联络为 $\nabla$。

**梯度 (Gradient)**：对于一个[光滑函数](@entry_id:267124) $u \in C^\infty(M)$，其梯度 $\nabla u$ 是一个向量场。它由 $u$ 的[外微分](@entry_id:161900) $du$ 通过[黎曼度量](@entry_id:754359) $g$ 唯一确定。具体而言，$\nabla u$ 是满足下述条件的唯一向量场：对于任意向量场 $X$，恒有 $g(\nabla u, X) = du(X) = X(u)$。在[局部坐标](@entry_id:181200) $(x^1, \dots, x^n)$ 中，梯度的分量表示为 $(\nabla u)^i = g^{ij} \partial_j u$，其中 $g^{ij}$ 是度量张量 $g_{ij}$ 的[逆矩阵](@entry_id:140380)分量。

**散度 (Divergence)**：一个光滑向量场 $X$ 的散度 $\operatorname{div}X$ 是一个光滑函数。它可以从几何上通过向量场 $X$ 对黎曼[体积元](@entry_id:267802) $d\mu_g$ 的[李导数](@entry_id:171745)来定义：$\mathcal{L}_X d\mu_g = (\operatorname{div}X) d\mu_g$。等价地，散度是 $X$ 的[协变导数](@entry_id:152476) $\nabla X$ 的迹。在[局部坐标](@entry_id:181200)中，这两种定义分别给出以下表达式：
$$ \operatorname{div}X = \frac{1}{\sqrt{\det g}} \partial_i \left( \sqrt{\det g} \, X^i \right) = \nabla_i X^i = \partial_i X^i + \Gamma^i_{ki} X^k $$
其中 $\Gamma^i_{jk}$ 是[Levi-Civita联络](@entry_id:161107)的[Christoffel符号](@entry_id:159831)。

**[拉普拉斯-贝尔特拉米算子](@entry_id:267002) (Laplace–Beltrami Operator)**：函数 $u$ 上的[拉普拉斯-贝尔特拉米算子](@entry_id:267002)（或称[拉普拉斯算子](@entry_id:146319)）定义为其[梯度的散度](@entry_id:270716)，即 $\Delta u = \operatorname{div}(\nabla u)$。这是一个二阶微分算子，在几何分析中扮演着核心角色。在[局部坐标](@entry_id:181200)中，其表达式为：
$$ \Delta u = \frac{1}{\sqrt{\det g}} \partial_i \left( \sqrt{\det g} \, g^{ij} \partial_j u \right) = g^{ij} \left( \partial_i \partial_j u - \Gamma^k_{ij} \partial_k u \right) $$
值得注意的是，算子的符号约定在不同文献中可能存在差异。在本章中，我们采用上述定义，这通常被称为“几何学家的拉普拉斯算子”。在此约定下，对于紧致无边[流形](@entry_id:153038)上的非平凡函数，$\Delta$ 是一个负半定算子。另一种常见的约定是“分析学家的拉普拉斯算子” $\tilde{\Delta} = -\Delta$，它是一个正半定算子。理解这种符号差异至关重要，因为它会影响[Bochner恒等式](@entry_id:193184)的具体形式。若将 $\Delta$ 替换为 $\tilde{\Delta}$，恒等式中的每一项都会相应地改变符号 [@problem_id:3034276]。我们将始终明确我们所使用的约定。

**Hessian**：函数 $u$ 的Hessian张量 $\nabla^2 u$ 是一个对称的(0,2)-型张量场，定义为 $u$ 的[外微分](@entry_id:161900) $du$ 的协变导数，即 $\nabla^2 u = \nabla(du)$。对于任意向量场 $X, Y$，其作用为：
$$ \nabla^2 u(X, Y) = (\nabla_X(du))(Y) = X(du(Y)) - du(\nabla_X Y) = X(Y(u)) - (\nabla_X Y)(u) $$
它也可以通过梯度的协变导数来理解：$\nabla^2 u(X,Y) = g(\nabla_X(\nabla u), Y)$。在[局部坐标](@entry_id:181200)中，其分量为 $(\nabla^2 u)_{ij} = \partial_i \partial_j u - \Gamma^k_{ij} \partial_k u$。拉普拉斯算子可以简洁地表示为Hessian的迹，$\Delta u = g^{ij}(\nabla^2 u)_{ij} = \operatorname{tr}_g(\nabla^2 u)$。

这些算子虽然在一般坐标下表达式复杂，但在任何一点 $p \in M$，我们总可以选取一个[法坐标](@entry_id:143194)系，使得在该点 $p$ 处 $g_{ij}(p) = \delta_{ij}$ 且所有Christoffel符号均为零，即 $\Gamma^k_{ij}(p) = 0$。在这样的[坐标系](@entry_id:156346)中心，上述算子的表达式骤然简化，恢复为其在[欧氏空间](@entry_id:138052)中的[标准形式](@entry_id:153058)：$(\nabla u)^i = \partial_i u$, $\operatorname{div}X = \sum_i \partial_i X^i$, $\Delta u = \sum_i \partial_i^2 u$, 以及 $(\nabla^2 u)_{ij} = \partial_i \partial_j u$。这表明，[黎曼几何](@entry_id:160508)中的这些定义是[欧氏空间](@entry_id:138052)中相应概念的内在、自然的推广 [@problem_id:3034266]。

### 函数的经典[Bochner恒等式](@entry_id:193184)

[Bochner恒等式](@entry_id:193184)是联系上述基本算子与[流形曲率](@entry_id:187680)的核心工具。它本质上是一个关于协变导数交换次序的计算结果，但其形式揭示了深刻的几何信息。对于一个[光滑函数](@entry_id:267124) $u \in C^\infty(M)$，其梯度的模长平方 $|\nabla u|^2 = g(\nabla u, \nabla u)$ 本身也是一个[光滑函数](@entry_id:267124)。[Bochner恒等式](@entry_id:193184)描述了该函数的拉普拉斯。

在我们的符号约定（$\Delta = \operatorname{div}(\nabla)$）下，函数 $u$ 的经典[Bochner恒等式](@entry_id:193184)为：
$$ \frac{1}{2} \Delta |\nabla u|^2 = |\nabla^2 u|^2 + \langle \nabla u, \nabla(\Delta u) \rangle + \operatorname{Ric}(\nabla u, \nabla u) $$
[@problem_id:3034257]

这个恒等式可以通过在一点的[法坐标](@entry_id:143194)系中直接计算 $\Delta(|\nabla u|^2)$ 并利用[协变导数](@entry_id:152476)的[可交换性](@entry_id:263314)公式（即Ricci恒等式）来推导。恒等式中的每一项都有明确的几何或分析意义 [@problem_id:3034278]：

1.  **$|\nabla^2 u|^2$**：这是函数 $u$ 的Hessian张量的范数平方，在[局部坐标](@entry_id:181200)中为 $\sum_{i,j} ((\nabla^2 u)_{ij})^2$。由于它是一个平方和，该项总是非负的 ($|\nabla^2 u|^2 \ge 0$)。它衡量了函数 $u$ 的[二阶导数](@entry_id:144508)偏离“[协变](@entry_id:634097)常数”的程度。在与热流等[演化方程](@entry_id:268137)相关的场景中，这一项通常被解释为一个**耗散项 (dissipation term)**，因为它总是试图使[梯度场](@entry_id:264143)变得更加平滑。

2.  **$\langle \nabla u, \nabla(\Delta u) \rangle$**：这是 $u$ 的梯度与 $u$ 的拉普拉斯的梯度之间的[内积](@entry_id:158127)。这一项的符号不确定。在[演化方程](@entry_id:268137)的语境中，它被视为一个**漂移项 (drift term)**，因为它描述了 $|\nabla u|^2$ 沿着 $\nabla u$ 方向的变化与 $\Delta u$ 变化之间的关系。当 $u$ 是一个调和函数（即 $\Delta u = 0$）时，这一项自然消失，使得恒等式大大简化。

3.  **$\operatorname{Ric}(\nabla u, \nabla u)$**：这是[流形](@entry_id:153038)的[Ricci曲率张量](@entry_id:271424)作用在梯度向量场 $\nabla u$ 上的结果，局部表示为 $\operatorname{Ric}_{ij}(\nabla u)^i (\nabla u)^j$。这是[Bochner恒等式](@entry_id:193184)中纯粹的**几何项**，直接将[流形](@entry_id:153038)的曲率与函数 $u$ 的分析性质联系起来。如果[流形](@entry_id:153038)具有正的Ricci曲率，该项就倾向于为正，对 $\Delta |\nabla u|^2$ 贡献一个正值，起到一个“源”的作用；反之，如果Ricci曲率为负，它就起到“汇”的作用。

若采用分析学家的拉普拉斯算子 $\tilde{\Delta} = -\Delta$，则整个恒等式两边乘以 $-1$。注意到 $\nabla(\Delta u) = \nabla(-\tilde{\Delta} u) = -\nabla(\tilde{\Delta} u)$，我们得到另一个常见的形式：
$$ \frac{1}{2} \tilde{\Delta} |\nabla u|^2 = -|\nabla^2 u|^2 + \langle \nabla u, \nabla(\tilde{\Delta} u) \rangle - \operatorname{Ric}(\nabla u, \nabla u) $$
[@problem_id:3034276]

### [Bochner恒等式](@entry_id:193184)的应用与诠释

[Bochner恒等式](@entry_id:193184)的威力在于它为我们提供了一个强大的工具，通过应用最大值原理来从[流形](@entry_id:153038)的曲率信息中推导出关于函数及其梯度的深刻结论。

#### [调和函数](@entry_id:746864)与曲率

一个重要的应用场景是研究调和函数，即满足 $\Delta u = 0$ 的函数。对于[调和函数](@entry_id:746864)，[Bochner恒等式](@entry_id:193184)简化为：
$$ \frac{1}{2} \Delta |\nabla u|^2 = |\nabla^2 u|^2 + \operatorname{Ric}(\nabla u, \nabla u) $$
现在，假设[流形](@entry_id:153038) $(M,g)$ 具有**非负[Ricci曲率](@entry_id:162038)**，即对任意向量场 $X$，$\operatorname{Ric}(X, X) \ge 0$。在此条件下，$\operatorname{Ric}(\nabla u, \nabla u) \ge 0$。由于 $|\nabla^2 u|^2$ 也总是非负的，我们立即得到一个关键的不等式：
$$ \Delta |\nabla u|^2 \ge 0 $$
这意味着函数 $|\nabla u|^2$ 是一个**[次调和函数](@entry_id:191036) (subharmonic function)**。根据弱[最大值原理](@entry_id:138611)，在一个[紧致流形](@entry_id:158804)上，[次调和函数](@entry_id:191036)的最大值必在边界上达到。如果[流形](@entry_id:153038)无边界，则该函数必为常数。这意味着在具有非负[Ricci曲率](@entry_id:162038)的紧致无边[流形](@entry_id:153038)上，任意[调和函数](@entry_id:746864)的梯度模长 $|\nabla u|$ 必须为常数。进一步的分析可以证明，这要求 $\nabla^2 u = 0$ 且 $\operatorname{Ric}(\nabla u, \nabla u) = 0$。如果Ricci曲率在某点严格为正，则必然有 $\nabla u = 0$，即 $u$ 是常数。这就是著名的Bochner消失定理的一个版本：具有正Ricci曲率的紧致流形上不存在非常数的[调和函数](@entry_id:746864)。[@problem_id:3034278]

#### 热流与[梯度估计](@entry_id:164549)

[Bochner恒等式](@entry_id:193184)在研究[热方程](@entry_id:144435) $\partial_t u = \Delta u$ 的解时也同样有效。我们可以推导一个“抛物型”的[Bochner公式](@entry_id:187951)，来描述 $|\nabla u|^2$ 如何随[时间演化](@entry_id:153943)。计算 $|\nabla u|^2$ 对时间 $t$ 的导数：
$$ \partial_t |\nabla u|^2 = 2 \langle \nabla_{\partial_t} \nabla u, \nabla u \rangle = 2 \langle \nabla(\partial_t u), \nabla u \rangle = 2 \langle \nabla(\Delta u), \nabla u \rangle $$
将此与经典[Bochner恒等式](@entry_id:193184)联立，我们可以消去 $\langle \nabla(\Delta u), \nabla u \rangle$ 项，得到关于 $(\partial_t - \Delta)$ 算子的表达式：
$$ (\partial_t - \Delta) |\nabla u|^2 = -2 |\nabla^2 u|^2 - 2 \operatorname{Ric}(\nabla u, \nabla u) $$
[@problem_id:3034278]
这个公式非常强大。如果[流形](@entry_id:153038)具有非负[Ricci曲率](@entry_id:162038) ($\operatorname{Ric} \ge 0$)，那么右端两项均为非正，我们得到不等式：
$$ (\partial_t - \Delta) |\nabla u|^2 \le 0 $$
根据抛物型最大值原理，对于定义在 $M \times [0, T)$ 上的函数 $|\nabla u|^2$，其在空间中的最大值 $\sup_{x \in M} |\nabla u(x,t)|^2$ 是关于时间 $t$ 非增的。这意味着，在非负[Ricci曲率](@entry_id:162038)的几何背景下，热流具有梯度耗散的性质：梯度的最大值不会随时间增长。这就是著名的[Li-Yau梯度估计](@entry_id:200503)的基础。[@problem_id:3034280]

值得一提的是，上述所有 pointwise 的推导仅依赖于Ricci恒等式（即[协变导数](@entry_id:152476)[交换子](@entry_id:158878)），而**不直接需要二阶Bianchi恒等式**。二阶[Bianchi恒等式](@entry_id:261685)的收缩形式，即 $\nabla^i \operatorname{Ric}_{ij} = \frac{1}{2} \nabla_j R$（其中 $R$ 是数量曲率），在对[Bochner公式](@entry_id:187951)进行积分或取散度，或者在处理如Einstein[流形](@entry_id:153038)（$\operatorname{Ric} = \lambda g$）这样的[特殊几何](@entry_id:194564)结构时，才显示其重要性。例如，在Einstein[流形](@entry_id:153038)上，该恒等式可以证明数量曲率 $R$ 必须是常数（对于 $n \ge 3$）。[@problem_id:3034256]

### [Bakry-Émery理论](@entry_id:635411)的推广

经典[Bochner恒等式](@entry_id:193184)的结构是如此普适，以至于它可以被推广到一个更抽象的框架，即所谓的[Bakry-Émery理论](@entry_id:635411)，或称$\Gamma$-calculus。这个理论考虑的是一个带有加权测度 $e^{-f} d\mu_g$ 的[流形](@entry_id:153038)，其中 $f$ 是一个光滑的“势”函数。

与此加权测度相伴的是一个自伴的二阶[扩散算子](@entry_id:136699)，即**[加权拉普拉斯算子](@entry_id:634510)**（或Bakry-Émery[拉普拉斯算子](@entry_id:146319)），定义为：
$$ L_f u = \Delta u - \langle \nabla f, \nabla u \rangle $$
这个算子可以看作是 $L_f = e^f \operatorname{div}(e^{-f} \nabla \cdot)$ 的展开形式，其构造保证了它在加权 $L^2$ 空间 $L^2(M, e^{-f}d\mu_g)$ 中是自伴的。

[Bakry-Émery理论](@entry_id:635411)的核心是引入**“平方场”算子 (carré du champ operator)** $\Gamma_f$：
$$ \Gamma_f(u,v) = \frac{1}{2} \left( L_f(uv) - u L_f v - v L_f u \right) $$
通过直接计算可以发现，对于上面定义的 $L_f$，这个抽象的 $\Gamma_f$ 算子恰好就是我们熟悉的梯度[内积](@entry_id:158127)：
$$ \Gamma_f(u,v) = \langle \nabla u, \nabla v \rangle $$
这表明梯度结构可以从算子 $L_f$ 的代数性质中恢复出来。接下来，定义**迭代平方场算子 (iterated carré du champ)** $\Gamma_{2,f}$：
$$ \Gamma_{2,f}(u) = \Gamma_{2,f}(u,u) = \frac{1}{2} \left( L_f(\Gamma_f(u,u)) - 2\Gamma_f(u, L_f u) \right) $$
通过与经典[Bochner恒等式](@entry_id:193184)完全平行的计算，可以推导出**Bochner-Bakry-Émery恒等式**：
$$ \Gamma_{2,f}(u) = |\nabla^2 u|^2 + \operatorname{Ric}_f(\nabla u, \nabla u) $$
其中 $\operatorname{Ric}_f$ 被称为**Bakry-Émery Ricci张量**，其定义为：
$$ \operatorname{Ric}_f = \operatorname{Ric} + \nabla^2 f $$
这个恒等式揭示了一个深刻的事实：从分析的角度看，[势函数](@entry_id:176105) $f$ 的Hessian $\nabla^2 f$ 起到了与[流形](@entry_id:153038)的[Ricci曲率](@entry_id:162038)完全相同的作用。许多依赖于[Ricci曲率](@entry_id:162038)下界的经典几何结果，都可以被推广到满足 $\operatorname{Ric}_f \ge K g$（即 $\operatorname{Ric} + \nabla^2 f \ge K g$）的加权[流形](@entry_id:153038)上。这套理论在概率论、最优传输和Ricci流等领域有着广泛而深刻的应用。[@problem_id:3034275]

### [微分形式](@entry_id:146747)的Weitzenböck恒等式

[Bochner恒等式](@entry_id:193184)的思想可以从函数（0-形式）推广到任意阶的微分形式上。这种推广通常被称为**Weitzenböck恒等式**或Weitzenböck-[Bochner公式](@entry_id:187951)。

为了表述这个恒等式，我们需要引入作用在[微分形式](@entry_id:146747)上的两种不同的拉普拉斯算子。设 $\omega$ 是一个 $k$-形式。

1.  **[霍奇-拉普拉斯算子](@entry_id:261049) (Hodge Laplacian)** $\Delta_H$：它由外微分算子 $d$ 和其[余微分算子](@entry_id:191334) $\delta$ (在一些文献中记为 $d^*$) 组合而成，定义为 $\Delta_H = d\delta + \delta d$。[霍奇-拉普拉斯算子](@entry_id:261049)与[流形的拓扑](@entry_id:267834)性质（通过[de Rham上同调](@entry_id:158673)）密切相关，其核由调和形式构成。

2.  **[联络拉普拉斯算子](@entry_id:197120) (Connection Laplacian)** 或**糙拉普拉斯算子 (Rough Laplacian)** $\nabla^*\nabla$：这是一个作用于任意[张量场](@entry_id:190170)的算子。对于 $k$-形式，它定义为[协变导数](@entry_id:152476) $\nabla$ 与其形式伴随 $\nabla^*$ 的复合。在任意一点的[法坐标](@entry_id:143194)系 $\{e_i\}$ 中，其作用为 $\nabla^*\nabla \omega = - \sum_i \nabla_{e_i}\nabla_{e_i}\omega$。这个算子只依赖于[流形](@entry_id:153038)的联络结构。

Weitzenböck恒等式精确地描述了这两个拉普拉斯算子之间的差异。这个差异完全由[流形](@entry_id:153038)的曲率决定。恒等式的一般形式为：
$$ \Delta_H \omega = \nabla^*\nabla \omega + \mathscr{R}_k(\omega) $$
[@problem_id:3034262]
其中 $\mathscr{R}_k$ 是一个零阶算子，即一个作用在 $\Lambda^k T^*M$ 上的代数（逐点）**曲率端omorphism (curvature endomorphism)**，它由[黎曼曲率张量](@entry_id:160189) $R$ 构建。

曲率项 $\mathscr{R}_k$ 的具体形式取决于形式的阶数 $k$：

*   对于**0-形式**（函数 $f$）：$\mathscr{R}_0 = 0$。[霍奇理论](@entry_id:161814)表明 $\Delta_H f = \delta d f = -\operatorname{div}(\nabla f) = -\Delta f$。因此，$\nabla^*\nabla f = -\Delta f$，两个[拉普拉斯算子](@entry_id:146319)（在符号意义上）是相同的。

*   对于**[1-形式](@entry_id:270392)** $\omega$：曲率项由[Ricci曲率](@entry_id:162038)决定。具体来说，$\mathscr{R}_1$ 是由Ricci张量通过度量提[升指标](@entry_id:265340)得到的 $(1,1)$-型张量 $\operatorname{Ric}^\sharp$。即，$\mathscr{R}_1(\omega) = \operatorname{Ric}^\sharp(\omega)$。若将 $\omega$ 视作其[对偶向量](@entry_id:161217)场 $X = \omega^\sharp$，则 $\langle \mathscr{R}_1(\omega), \omega \rangle = \operatorname{Ric}(X, X)$。

*   对于**一般的 $k$-形式** ($k \ge 2$)：曲率项 $\mathscr{R}_k$ 的结构更为复杂，它不仅依赖于[Ricci曲率](@entry_id:162038)，还依赖于黎曼曲率张量的完整信息（包括[Weyl曲率](@entry_id:188172)部分）。其作用可以表示为黎曼曲率张量在 $\Lambda^k T^*M$ 上的[诱导表示](@entry_id:136842)。一个明确的表达（在[法坐标](@entry_id:143194)系中）是 $\mathscr{R}_k(\omega) = \sum_{i,j} e^j \wedge \iota_{e_i} (R(e_i, e_j) \cdot \omega)$，其中 $R(e_i, e_j)$ 作为导子作用在形式上 [@problem_id:3034272]。

一个特别重要且可计算的例子是**[常截面曲率](@entry_id:272200)**为 $\kappa$ 的[流形](@entry_id:153038)。在这种情况下，黎曼曲率张量有非常简单的形式，可以算出曲率项 $\mathscr{R}_k$ 是一个标量乘以单位算子：
$$ \mathscr{R}_k = \kappa k(n-k) \operatorname{Id} $$
因此，在[常截面曲率流形](@entry_id:634470)上，Weitzenböck恒等式变为 $\Delta_H \omega = \nabla^*\nabla \omega + \kappa k(n-k)\omega$。[@problem_id:3034272]

### Weitzenböck恒等式的应用

与经典[Bochner公式](@entry_id:187951)类似，Weitzenböck恒等式是研究微分形式和[流形](@entry_id:153038)拓扑之间关系的核心工具。一个主要应用是研究**霍奇热流 (Hodge heat flow)** $\partial_t \omega = -\Delta_H \omega$。

考虑 $k$-形式 $\omega(t)$ 的 $L^2$-能量 $E(t) = \frac{1}{2} \int_M |\omega(t)|^2 dV_g$。其随时间的演化由下式给出：
$$ \frac{dE}{dt} = \int_M \langle \partial_t \omega, \omega \rangle dV_g = - \int_M \langle \Delta_H \omega, \omega \rangle dV_g $$
利用Weitzenböck恒等式，并对 $\nabla^*\nabla$ 项进行[分部积分](@entry_id:136350)，我们得到：
$$ \frac{dE}{dt} = - \int_M \langle \nabla^*\nabla \omega + \mathscr{R}_k(\omega), \omega \rangle dV_g = - \left( \|\nabla \omega\|_{L^2}^2 + \int_M \langle \mathscr{R}_k(\omega), \omega \rangle dV_g \right) $$
[@problem_id:3034280]

这个公式清楚地表明，能量的演化受到两项的控制：一项是总与[能量耗散](@entry_id:147406)方向一致的 $\|\nabla \omega\|_{L^2}^2$，另一项是完全由曲率决定的 $\int_M \langle \mathscr{R}_k(\omega), \omega \rangle dV_g$。因此，[曲率算子](@entry_id:198006) $\mathscr{R}_k$ 的符号性质至关重要。

如果[曲率算子](@entry_id:198006) $\mathscr{R}_k$ 是**非负定**的（即对任意 $\omega$，$\langle \mathscr{R}_k(\omega), \omega \rangle \ge 0$），则 $\frac{dE}{dt} \le -\|\nabla \omega\|_{L^2}^2 \le 0$。这意味着能量是单调不减的。如果 $\mathscr{R}_k$ 是**正定**的，我们甚至可以得到能量指数衰减的估计。

确定 $\mathscr{R}_k$ 的符号是一个微妙的几何问题：
*   一个深刻的定理指出，如果[流形](@entry_id:153038)上的**[曲率算子](@entry_id:198006)** $\mathcal{R}: \Lambda^2 TM \to \Lambda^2 TM$ 是非负定的（这是一个比[非负截面曲率](@entry_id:636727)更强的条件），那么 $\mathscr{R}_k$ 对所有 $k$ 都是非负定的。[@problem_id:3034280]
*   对于 $k=1$，$\mathscr{R}_1$ 的非负性等价于Ricci曲率的非负性。
*   然而，对于 $k \ge 2$，[Ricci曲率](@entry_id:162038)非负**不足以**保证 $\mathscr{R}_k$ 非负。例如，[复射影空间](@entry_id:268402) $\mathbb{CP}^m$ ($m \ge 2$) 具有正[Ricci曲率](@entry_id:162038)，但其上的 $\mathscr{R}_2$ 却不是正定的。

在[常截面曲率](@entry_id:272200) $\kappa$ 的情形下，$\langle \mathscr{R}_k(\omega), \omega \rangle = \kappa k(n-k) |\omega|^2$。如果 $\kappa \ge 0$，则 $\mathscr{R}_k$ 非负。此时能量演化满足 $\frac{dE}{dt} \le -\kappa k(n-k) \|\omega\|_{L^2}^2$，这直接导出了能量的指数衰减界。[@problem_id:3034280]

### 到向量丛值形式的推广

Weitzenböck原理可以进一步推广到作用在**向量丛值微分形式**上的拉普拉斯算子。设 $(E, h, \nabla^E)$ 是一个带度量和相容联络的Hermitian向量丛。我们可以定义 $E$-值的 $p$-形式，以及相应的[协变](@entry_id:634097)[外微分](@entry_id:161900) $d^E$ 和[霍奇-拉普拉斯算子](@entry_id:261049) $\Delta_H^E$。

在这种更一般的情形下，Weitzenböck恒等式依然成立：
$$ \Delta_H^E = (\nabla^E)^* \nabla^E + \mathscr{R}^E $$
这里的曲率项 $\mathscr{R}^E$ 现在包含了来自两个源头的曲率贡献：一是来自底[流形](@entry_id:153038) $M$ 的[黎曼曲率](@entry_id:635343) $R^{TM}$，二是来自向量丛 $E$ 的联络曲率 $F^E$。其结构可以抽象地写作：
$$ \mathscr{R}^E \sim R^{TM} \otimes \operatorname{Id}_E + \operatorname{Id}_{\Lambda^p T^*M} \otimes F^E $$
更精确的表达式表明，$\mathscr{R}^E$ 是作用在张量积丛 $\Lambda^p T^*M \otimes E$ 上的[曲率算子](@entry_id:198006)。这个普适的公式统一了函数、微分形式以及更一般的几何场论中的[拉普拉斯算子](@entry_id:146319)理论，是现代[几何分析](@entry_id:157700)中不可或缺的工具。[@problem_id:3034273]