## 引言
在计算科学与工程的众多前沿领域中，精确求解移动和变形域上的[偏微分方程](@entry_id:141332)是一个长期存在的挑战。无论是模拟飞行器颤振、[心脏瓣膜](@entry_id:154991)的开合，还是海岸线的演变，我们都需要能够同时处理复杂几何变化和流场动态的数值方法。任意拉格朗日-欧拉（Arbitrary Lagrangian-Eulerian, ALE）方法为此提供了一个优雅而强大的框架，它通过将[网格运动](@entry_id:163293)与物质运动[解耦](@entry_id:637294)，兼具了[拉格朗日方法](@entry_id:142825)的边界贴体性和欧拉方法的[网格质量](@entry_id:151343)可控性。然而，将ALE框架与以[高阶精度](@entry_id:750325)和局部守恒性著称的间断Galerkin（DG）方法相结合，带来了一系列独特的理论和实践难题，尤其是在如何保持格式的稳定性和基本守恒律方面。

本文旨在系统性地阐明构建一个稳健、高阶的ALE-[DG格式](@entry_id:178043)所需的核心构件。读者将通过三个循序渐进的章节，全面掌握这一先进的计算方法。在 **“原理与机制”** 一章中，我们将深入探讨ALE[运动学](@entry_id:173318)、守恒律在移动[坐标系](@entry_id:156346)下的变换，并着重阐述保证数值模拟保真度的基石——[几何守恒律](@entry_id:170384)（GCL）。接下来，在 **“应用与[交叉](@entry_id:147634)学科联系”** 一章中，我们将展示ALE-DG方法在计算流体动力学、流固耦合和地球物理学等领域的强大应用，揭示理论与实践的紧密联系。最后，在 **“动手实践”** 部分，我们通过具体的编程练习，将抽象的理论转化为可操作的技能，帮助读者巩固对关键概念的理解。

## 原理与机制

在移动和变形域上求解偏微分方程是计算科学与工程中的一个核心挑战。任意拉格朗日-欧拉（Arbitrary Lagrangian-Eulerian, ALE）方法为此提供了一个强大而灵活的框架，它将纯[拉格朗日方法](@entry_id:142825)（网格随材料移动）和纯欧拉方法（网格固定）的优点结合起来。本章旨在深入阐述[ALE方法](@entry_id:746347)应用于间断Galerkin（DG）格式时的基本原理和关键机制。我们将从移动域的运动学描述出发，推导在ALE框架下的守恒律，并详细探讨为保证[数值格式](@entry_id:752822)的稳定性和[高阶精度](@entry_id:750325)所必须满足的条件，特别是[几何守恒律](@entry_id:170384)（Geometric Conservation Law, GCL）。

### ALE框架：移动域的[运动学](@entry_id:173318)

[ALE方法](@entry_id:746347)的核心在于将物理域的运动与流体本身的运动解耦。这是通过引入一个独立的、任意规定的[网格运动](@entry_id:163293)来实现的。为了形式化地描述这一过程，我们考虑一个固定的、时间无关的**参考域**（或计算域） $\Omega_0 \subset \mathbb{R}^d$，其坐标用 $\boldsymbol{X}$ 表示。同时，我们有一个随时间 $t$ 变化的**物理域** $\Omega(t) \subset \mathbb{R}^d$，其坐标用 $\boldsymbol{x}$ 表示。

这两个域通过一个光滑、可逆的**ALE映射** $\boldsymbol{\chi}$ 联系起来：
$$
\boldsymbol{x} = \boldsymbol{\chi}(\boldsymbol{X}, t)
$$
在任意给定的时刻 $t$，该映射都是一个从 $\Omega_0$ 到 $\Omega(t)$ 的微分同胚。这个映射描述了参考域中的每一个点如何随时间移动到物理域中的相应位置。

为了分析守恒律在移动[坐标系](@entry_id:156346)下的变换，我们必须定义几个关键的[运动学](@entry_id:173318)量 。

1.  **变形梯度张量 (Deformation Gradient)**：变形梯度张量 $\boldsymbol{F}$ 描述了映射引起的局部变形，定义为物理坐标 $\boldsymbol{x}$ 对参考坐标 $\boldsymbol{X}$ 的梯度：
    $$
    \boldsymbol{F}(\boldsymbol{X}, t) = \nabla_{\boldsymbol{X}} \boldsymbol{\chi}(\boldsymbol{X}, t)
    $$
    在其分量形式中，$F_{ij} = \frac{\partial x_i}{\partial X_j}$。这个二阶张量将参考域中的一个微小矢量映射到物理域中的对应矢量。

2.  **雅可比行列式 (Jacobian)**：[雅可比行列式](@entry_id:137120) $J$ 是变形梯度张量的[行列式](@entry_id:142978)，它量化了体积的局部变化：
    $$
    J(\boldsymbol{X}, t) = \det(\boldsymbol{F}(\boldsymbol{X}, t))
    $$
    一个参考域中的无穷小体积元 $dV_{\boldsymbol{X}}$ 经过映射后，在物理域中变为 $dV_{\boldsymbol{x}} = J \, dV_{\boldsymbol{X}}$。由于映射是保持方向的微分同胚，我们要求 $J > 0$。

3.  **网格速度 (Grid Velocity)**：网格速度 $\boldsymbol{w}$ 是ALE框架中的一个核心概念，它描述了计算网格上点的运动速度。在ALE的描述中，网格点对应于固定的参考坐标 $\boldsymbol{X}$。因此，网格速度被定义为在保持 $\boldsymbol{X}$ 不变的情况下，物理位置 $\boldsymbol{x}$ 对时间的导数：
    $$
    \boldsymbol{w}(\boldsymbol{X}, t) = \frac{\partial \boldsymbol{\chi}(\boldsymbol{X}, t)}{\partial t} \bigg|_{\boldsymbol{X}}
    $$
    这个定义给出了在参考域上定义的网格速度。为了在物理域中场 $(\boldsymbol{x}, t)$ 上表示它，我们需要进行坐标替换 $\boldsymbol{X} = \boldsymbol{\chi}^{-1}(\boldsymbol{x}, t)$：
    $$
    \boldsymbol{w}(\boldsymbol{x}, t) = \left( \frac{\partial \boldsymbol{\chi}(\boldsymbol{X}, t)}{\partial t} \bigg|_{\boldsymbol{X}} \right) \bigg|_{\boldsymbol{X} = \boldsymbol{\chi}^{-1}(\boldsymbol{x}, t)}
    $$

这些运动学量之间存在一个至关重要的关系，它构成了[几何守恒律](@entry_id:170384)的基础。通过对[雅可比行列式](@entry_id:137120)求时间导数，并使用[雅可比公式](@entry_id:142453)（Jacobi's formula），可以推导出以下恒等式，也称为**欧拉展开公式** (Euler's expansion formula) ：
$$
\frac{\partial J(\boldsymbol{X}, t)}{\partial t} \bigg|_{\boldsymbol{X}} = J(\boldsymbol{X}, t) \left( \nabla_{\boldsymbol{x}} \cdot \boldsymbol{w}(\boldsymbol{x}, t) \right)
$$
这个恒等式表明，一个随[网格运动](@entry_id:163293)的微元体积的变化率，等于该体积乘以物理空间中网格[速度场](@entry_id:271461)的散度。这一关系是确保[数值格式](@entry_id:752822)在[移动网格](@entry_id:752196)上保持守恒性的关键。

### ALE框架下的守恒律

现在我们考虑一个在物理域 $\Omega(t)$ 上定义的守恒律：
$$
\frac{\partial q}{\partial t} + \nabla_{\boldsymbol{x}} \cdot \boldsymbol{f}(q) = 0
$$
其中 $q$ 是[守恒变量](@entry_id:747720)，$\boldsymbol{f}(q)$ 是物理通量。为了在[移动网格](@entry_id:752196)上构建保守的数值格式，我们需要从积分形式出发，并考虑[控制体积](@entry_id:143882)本身的运动。

对于任意一个随网格以速度 $\boldsymbol{w}$ 移动的控制体积 $K(t) \subset \Omega(t)$，**[雷诺输运定理](@entry_id:191217)** (Reynolds Transport Theorem) 给出了其内部 $q$ 总量的变化率 ：
$$
\frac{d}{dt} \int_{K(t)} q \, dV = \int_{K(t)} \frac{\partial q}{\partial t} \, dV + \int_{\partial K(t)} q (\boldsymbol{w} \cdot \boldsymbol{n}) \, dS
$$
其中 $\boldsymbol{n}$ 是[控制体积](@entry_id:143882)边界 $\partial K(t)$ 的单位外法向向量。

将原始守恒律在 $K(t)$ 上积分，并应用散度定理，我们得到：
$$
\int_{K(t)} \frac{\partial q}{\partial t} \, dV = - \int_{K(t)} \nabla_{\boldsymbol{x}} \cdot \boldsymbol{f}(q) \, dV = - \int_{\partial K(t)} \boldsymbol{f}(q) \cdot \boldsymbol{n} \, dS
$$
将此式代入[雷诺输运定理](@entry_id:191217)，我们得到ALE框架下的守恒律积分形式：
$$
\frac{d}{dt} \int_{K(t)} q \, dV = - \int_{\partial K(t)} \boldsymbol{f}(q) \cdot \boldsymbol{n} \, dS + \int_{\partial K(t)} q (\boldsymbol{w} \cdot \boldsymbol{n}) \, dS
$$
整理后得到：
$$
\frac{d}{dt} \int_{K(t)} q \, dV + \int_{\partial K(t)} (\boldsymbol{f}(q) - q\boldsymbol{w}) \cdot \boldsymbol{n} \, dS = 0
$$
这个方程明确地表明，在随网格移动的[控制体积](@entry_id:143882)中，守恒量的总变化由跨越其边界的净通量决定。这个有效的通量被称为**ALE相对通量** ，其张量形式为：
$$
\boldsymbol{F}_{\text{ALE}}(q) = \boldsymbol{f}(q) - q\boldsymbol{w}^T
$$
相对通量的物理意义是物质通量相对于移动边界的通量。这是构建ALE[数值格式](@entry_id:752822)时所有界面通量计算的基础。

作为一个具体的例子，考虑一维[可压缩欧拉方程](@entry_id:747588)，其[守恒变量](@entry_id:747720)向量为 $U = (\rho, \rho u, E)^T$。其在静止[坐标系](@entry_id:156346)下的物理通量为 $F(U) = (\rho u, \rho u^2 + p, (E+p)u)^T$。在ALE框架下，网格以速度 $w$ 移动，相应的ALE通量 $F_{\text{ALE}}(U) = F(U) - wU$ 的分量为 ：
$$
F_{\text{ALE}}(U) = \begin{pmatrix} \rho(u-w) \\ \rho u(u-w) + p \\ E(u-w) + pu \end{pmatrix}
$$
可以看到，每一项都包含了流体相对于网格的运动速度 $(u-w)$。

当我们将守恒律从物理域变换到参考域时，方程的形式会变得更加复杂，并引入几何度量项。通过引入**[协变基](@entry_id:198968)矢** $\boldsymbol{a}_i = \partial \boldsymbol{x} / \partial X_i$ 和**[逆变基](@entry_id:197906)矢** $\boldsymbol{a}^i$（满足 $\boldsymbol{a}^i \cdot \boldsymbol{a}_j = \delta^i_j$），可以将物理通量 $\boldsymbol{f}$ 转换为参考域中的**[逆变](@entry_id:192290)通量** $\tilde{F}^i = J \boldsymbol{f} \cdot \boldsymbol{a}^i$。这些量在基于[参考单元](@entry_id:168425)的DG方法实现中至关重要 。

### [移动网格](@entry_id:752196)上的[间断Galerkin格式](@entry_id:178043)

在ALE框架下构建[DG格式](@entry_id:178043)时，我们直接在每个随时间变化的单元 $K(t)$ 上书写弱形式。将ALE守恒律[微分形式](@entry_id:146747)乘以一个检验函数 $v_h$ 并在 $K(t)$ 上积分，经过[分部积分](@entry_id:136350)后，得到：
$$
\frac{d}{dt} \int_{K(t)} v_h q_h \, dV - \int_{K(t)} \nabla v_h \cdot (\boldsymbol{f}(q_h) - q_h \boldsymbol{w}) \, dV + \int_{\partial K(t)} v_h \mathcal{H}(q_h^-, q_h^+, \boldsymbol{n}, w_n) \, dS = 0
$$
这里，$q_h$ 是数值解，$q_h^-$ 和 $q_h^+$ 分别是单元内部和相邻单元在界面上的值，$w_n = \boldsymbol{w} \cdot \boldsymbol{n}$ 是法向网格速度。$\mathcal{H}$ 是**数值通量**，它必须仔细设计以保证格式的稳定性和守恒性。

为了使ALE-[DG格式](@entry_id:178043)是守恒的，[数值通量](@entry_id:752791) $\mathcal{H}$ 必须满足以下关键属性 ：

1.  **相容性 (Consistency)**：当界面两侧的状态相同时（$q^- = q^+$），数值通量必须退化为真实的ALE相对通量：
    $$
    \mathcal{H}(q, q, \boldsymbol{n}, w_n) = (\boldsymbol{f}(q) - q\boldsymbol{w}) \cdot \boldsymbol{n}
    $$
    这意味着[数值通量](@entry_id:752791)必须同时考虑物理通量和由[网格运动](@entry_id:163293)引起的附加通量。

2.  **守恒性 (Conservatism)**：对于任意内部界面，一个单元的流出通量必须等于相邻单元的流入通量。这要求[数值通量](@entry_id:752791)是**单值**的，即 $\mathcal{H}(q^-, q^+, \boldsymbol{n}, w_n) = -\mathcal{H}(q^+, q^-, -\boldsymbol{n}, -w_n)$。为了实现这一点，两个相邻单元在共享界面上必须使用相同的法向网格速度 $w_n$。

数值通量的设计直接影响着[迎风](@entry_id:756372)性质。在ALE框架下，信息的传播方向取决于[特征速度](@entry_id:165394)相对于网格的速度。以一维线性平流方程 $\partial_t q + \partial_x (aq) = 0$ 为例，其特征速度为 $a$。在[移动网格](@entry_id:752196)上，相对特征速度为 $a-w$ 。因此，[迎风](@entry_id:756372)方向由 $a-w$ 的符号决定，而不是 $a$ 的符号。
-   **[欧拉框架](@entry_id:749109)** ($w=0$)：[相对速度](@entry_id:178060)为 $a$，是标准的迎风格式。
-   **[拉格朗日框架](@entry_id:751113)** ($w=a$)：相对速度为 $0$。流体质点与网格单元保持相对静止，因此跨越内部界面的[对流通量](@entry_id:158187)为零。
-   **一般ALE框架**：迎风方向取决于 $a$ 和 $w$ 的相对大小。例如，即使物理流速 $a>0$（向右），如果网格以更快的速度向右移动（$w>a$），那么[相对速度](@entry_id:178060) $a-w0$，信息实际上是从右向左相对于网格传播的。

这种相对速度的概念也直接影响了显式时间格式的稳定性。**Courant–Friedrichs–Lewy (CFL) 条件**要求时间步长 $\Delta t$ 必须受限于信息[传播速度](@entry_id:189384)。在ALE框架下，这个速度是相对速度，因此[CFL条件](@entry_id:178032)的形式为 $\Delta t \lesssim h / |\lambda - w|$，其中 $h$ 是网格尺寸，$\lambda$ 是特征速度 。

作为数值通量的一个具体例子，我们可以推导**ALE-[Roe通量](@entry_id:754409)**。标准[Roe通量](@entry_id:754409)的核心是近似Riemann问题的解。在ALE框架下，我们本质上是在一个以速度 $w_n$ 移动的[参考系](@entry_id:169232)中求解Riemann问题。这导致了一个简洁而深刻的结果：ALE-[Roe通量](@entry_id:754409)的形式与标准[Roe通量](@entry_id:754409)非常相似，但其[特征值](@entry_id:154894)被平移了 。如果标准法向通量雅可比矩阵 $A(\tilde{U})$ 的[特征值](@entry_id:154894)为 $\lambda_k$，那么ALE框架下对应的[特征值](@entry_id:154894)为 $\lambda_k - w_n$。而定义特征波结构的[特征向量](@entry_id:151813)保持不变。最终的ALE-[Roe通量](@entry_id:754409)可以写为：
$$
\boldsymbol{F}^*_{\text{ALE}} = \frac{1}{2}(\boldsymbol{F}_{n}(U_{L}) + \boldsymbol{F}_{n}(U_{R})) - \frac{1}{2}w_{n}(U_{L} + U_{R}) - \frac{1}{2}R|\Lambda - w_{n}I|R^{-1}(U_{R} - U_{L})
$$
其中 $F_n$ 是法向物理通量，$U_L, U_R$ 是界面左右状态，$\Lambda$ 是[特征值](@entry_id:154894)对角矩阵，$R$ 是右[特征向量](@entry_id:151813)矩阵。

### [几何守恒律](@entry_id:170384)与[高阶精度](@entry_id:750325)

ALE-[DG格式](@entry_id:178043)中最微妙也最关键的方面之一是**[几何守恒律 (GCL)](@entry_id:749845)**。一个设计不当的[移动网格](@entry_id:752196)格式可能无法保持最简单的解，例如一个均匀流场（即**[自由流](@entry_id:159506)保持**，free-stream preservation）。这意味着即使物理上解应该保持常数，数值解也可能因为网格的纯粹几何运动而产生非物理的[振荡](@entry_id:267781)或误差 。

GCL的本质要求是，数值格式必须精确地再现体积随时间变化的几何事实。我们在前面已经看到其连续形式：$\partial_t J = J (\nabla_{\boldsymbol{x}} \cdot \boldsymbol{w})$，或者在参考域中等价地写为 $\partial_t J = \nabla_{\boldsymbol{X}} \cdot (J \boldsymbol{F}^{-1} \boldsymbol{w})$。当我们将这些导数用离散算子（例如DG中的[微分矩阵](@entry_id:149870) $D$）代替时，必须保证离散模拟的几何关系是自洽的。

对于一个节点[DG格式](@entry_id:178043)，其空间导数由[微分矩阵](@entry_id:149870) $D$ 近似，离散GCL通常要求在每个节点上满足：
$$
\frac{\partial J_i}{\partial t} = (D \boldsymbol{w})_i
$$
这里的挑战在于，$\partial J / \partial t$ 和 $D\boldsymbol{w}$ 的计算方式必须相容。如果 $\boldsymbol{w}$ 的函数形式不是多项式（例如，在正弦[网格运动](@entry_id:163293) $\boldsymbol{x}(X,t) = X + \varepsilon \sin(\pi X) \sin(\omega t)$ 的情况下），那么用多项式[微分矩阵](@entry_id:149870) $D$ 计算的 $(D \boldsymbol{w})_i$ 通常不等于 $\partial \boldsymbol{w} / \partial X$ 的精确解析值。如果我们独立地计算左侧的 $\partial J_i / \partial t$（例如，通过对 $J$ 的解析表达式求导）和右侧的 $(D\boldsymbol{w})_i$，两者之间会存在差异，这个差异就构成了对常数解的虚假源项，从而违反了GCL 。保证GCL的一种可靠方法是，将离散的雅可比时间导数 *定义* 为网格速度的[离散空间](@entry_id:155685)导数，即 $J_t^{\text{disc}} := D \boldsymbol{w}$。

GCL的满足与[DG弱形式](@entry_id:748377)中积分的计算精度密切相关。考虑ALE-[DG方法](@entry_id:748369)中典型的[质量矩阵](@entry_id:177093)项 $\int_{\hat{K}} J u v \, d\boldsymbol{X}$。这个积分以及其他包含[雅可比](@entry_id:264467) $J$ 或其导数 $\partial_t J$ 的项必须被精确计算，否则就会引入破坏守恒性的求积误差。例如，离散格式必须精确地满足[乘积法则](@entry_id:158393)的弱形式 $\frac{d}{dt} \int Ju v \, d\boldsymbol{X} = \int (\partial_t J) u v \, d\boldsymbol{X} + \int J (\partial_t u) v \, d\boldsymbol{X}$ 。

对于使用[张量积](@entry_id:140694)单元（例如四边形或六面体）的高阶DG方法，这就对数值求积提出了明确的要求。如果[雅可比](@entry_id:264467) $J$、[试探函数](@entry_id:756165) $u$ 和[检验函数](@entry_id:166589) $v$ 在每个坐标方向 $\ell$ 上的多项式次数分别为 $r_\ell, p_\ell, q_\ell$，并且我们使用每维 $n$ 个求积点的张量积高斯求积，那么为了精确计算该积分，必须在**每个坐标方向**上满足以下条件 ：
-   对于**高斯-勒让德 (Gauss-Legendre)** 求积：$r_\ell + p_\ell + q_\ell \le 2n - 1$
-   对于**[高斯-洛巴托-勒让德](@entry_id:749736) ([Gauss-Lobatto-Legendre](@entry_id:749736))** 求积：$r_\ell + p_\ell + q_\ell \le 2n - 3$

未能满足这些条件将导致质量矩阵和几何项的计算不精确，从而可能违反GCL。

最后，GCL的要求也延伸到了[时间离散化](@entry_id:169380)。ALE-DG的[半离散系统](@entry_id:754680)可以写成：
$$
M(t) \frac{d\boldsymbol{u}}{dt} = \boldsymbol{r}(\boldsymbol{u}, t)
$$
其中[质量矩阵](@entry_id:177093) $M(t)$ 是时变的。为了求解这个系统，我们不能简单地将标准显式龙格-库塔（RK）方法应用于 $\dot{\boldsymbol{u}} = M(t)^{-1} \boldsymbol{r}$，因为这既昂贵又不稳定。一个更好的方法是对方程 $\frac{d}{dt}(M\boldsymbol{u}) = \dot{M}\boldsymbol{u} + \boldsymbol{r}$ 进行时间积分 。为了在这种[显式时间积分](@entry_id:165797)方案中精确满足GCL（即保持常数解），RK方法的求积规则必须能够精确地积分质量矩阵的时间导数。这引出了对[时间积分格式](@entry_id:165373)的GCL条件：
$$
\Delta t \sum_{i=1}^{s} b_i \dot{M}(t^{(i)}) = M(t^{n+1}) - M(t^n)
$$
其中 $b_i$ 和 $t^{(i)}$ 是RK方法的权和阶段时间。这个条件确保了在一个时间步内，由RK求积计算出的总几何变化（[质量矩阵](@entry_id:177093)的变化）与真实的几何变化相匹配。如果[网格运动](@entry_id:163293)在时间上是 $p$ 次多项式，那么 $\dot{M}(t)$ 是 $p-1$ 次多项式，这就要求RK方法的精度至少为 $p-1$。

综上所述，构建一个保守且高阶的ALE-[DG格式](@entry_id:178043)，需要在一个统一的框架内仔细处理从连续运动学到空间和[时间离散化](@entry_id:169380)的每一个环节。正确定义和使用相对通量是基础，而严格满足离散[几何守恒律](@entry_id:170384)则是实现高保真模拟的关键。