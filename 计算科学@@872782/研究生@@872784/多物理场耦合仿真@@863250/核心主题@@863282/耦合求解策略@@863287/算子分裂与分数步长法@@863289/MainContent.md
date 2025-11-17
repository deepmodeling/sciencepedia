## 引言
在科学与工程的广阔天地中，从天气预报到[反应堆设计](@entry_id:190145)，从[生物系统](@entry_id:272986)到金融市场，许多复杂系统的演化行为都可以通过[微分方程](@entry_id:264184)来描述。然而，当这些系统涉及多个相互作用的物理过程（即[多物理场耦合](@entry_id:171389)）时，描述其整体动力学的算子会变得异常复杂，导致直接进行数值求解的成本高昂甚至不可行。这一挑战催生了一种强大而优雅的计算[范式](@entry_id:161181)：[算子分裂法](@entry_id:752962)（Operator Splitting Methods），或称分数步法（Fractional Step Methods）。其核心思想是一种“分而治之”的策略：与其一次性解决整个耦合问题，不如将其分解为一系列由更简单的物理子[过程控制](@entry_id:271184)的子问题，然后顺序求解它们来逼近整体演化。

本文旨在系统地介绍[算子分裂法](@entry_id:752962)的理论与实践。我们将深入探讨这一方法为何在处理刚性、[非线性](@entry_id:637147)以及多尺度问题时如此有效，并揭示其背后深刻的数学原理。通过接下来的内容，读者将能够全面理解[算子分裂法](@entry_id:752962)的精髓，并掌握将其应用于解决实际问题的能力。

- 在第一章**“原理与机制”**中，我们将奠定理论基础，从基本的Lie-Trotter和[Strang分裂](@entry_id:755497)格式出发，借助算子[交换子](@entry_id:158878)和[BCH公式](@entry_id:197600)分析其精度，并引入[半群理论](@entry_id:273332)来严格证明其[收敛性与稳定性](@entry_id:636533)。
- 随后，在第二章**“应用与[交叉](@entry_id:147634)学科联系”**中，我们将踏上一段跨学科之旅，探索[算子分裂法](@entry_id:752962)如何在计算流体力学、[化学反应](@entry_id:146973)、[材料科学](@entry_id:152226)和计算机图形学等领域大放异彩，展示其作为[IMEX方法](@entry_id:170079)、[投影法](@entry_id:144836)和维度分裂等具体技术的应用实例。
- 最后，在第三章**“动手实践”**中，我们将通过一系列精心设计的问题，引导读者将理论知识转化为实践技能，解决边界条件处理、[耦合稳定性](@entry_id:747984)以及不同方法选择等真实世界中的挑战。

通过这三个章节的层层深入，我们将共同揭开[算子分裂法](@entry_id:752962)的面纱，领略其作为现代计算科学基石的强大威力。

## 原理与机制

在多物理场耦合仿真的领域，许多复杂的演化问题可以抽象为以下形式的[初值问题](@entry_id:144620)：

$$
\frac{d}{dt}u(t) = \mathcal{A}u(t), \quad u(0) = u_0
$$

其中 $u(t)$ 是在[巴拿赫空间](@entry_id:143833) $X$ 中取值的[状态向量](@entry_id:154607)，而 $\mathcal{A}$ 是一个（可能无界的）线性或非线性算子，它描述了系统的完整动力学。通常，算子 $\mathcal{A}$ 可以自然地分解为两个或多个部分的总和，例如 $\mathcal{A} = A + B$，其中每个子算子 $A$ 和 $B$ 代表一个独立的物理过程（如[扩散](@entry_id:141445)、[平流](@entry_id:270026)或反应）或一个在数值上更易于处理的部分。

[算子分裂法](@entry_id:752962)（Operator Splitting Methods）或分数步法（Fractional Step Methods）的核心思想是基于这种分解。它没有直接解决由复杂算子 $\mathcal{A}$ 控制的完整问题，而是将问题分解为一系列由更简单的子算子 $A$ 和 $B$ 控制的子问题，并通过顺序求解这些子问题来逼近完整系统的演化。这种“[分而治之](@entry_id:273215)”的策略是计算科学中一个极其强大和广泛应用的技术，因为它允许我们为每个物理过程选择最优的数值方法，从而有效地处理刚性、[非线性](@entry_id:637147)以及[多物理场](@entry_id:164478)之间的复杂耦合。

### 基本分裂格式：Lie-Trotter 与 Strang 分裂

考虑线性[演化方程](@entry_id:268137) $u'(t) = (A+B)u(t)$。其形式解可以写为 $u(t) = \exp(t(A+B))u(0)$，其中 $\exp(t\mathcal{A})$ 表示由算子 $\mathcal{A}$ 生成的演化[半群](@entry_id:153860)。[算子分裂法](@entry_id:752962)的目标是利用子问题的演化算子 $\exp(tA)$ 和 $\exp(tB)$ 的组合来逼近完整的演化算子 $\exp(t(A+B))$。

最基础的分裂格式是 **[Lie-Trotter 分裂](@entry_id:751267)**（或称 Godunov 分裂）。在一个时间步长 $\Delta t$ 内，它通过顺序应用两个子演化来近似解：

$$
u^{n+1} = \exp(\Delta t A) \exp(\Delta t B) u^n
$$

或者采用相反的顺序 $u^{n+1} = \exp(\Delta t B) \exp(\Delta t A) u^n$。这种方法将一个复杂的时间步分解为两个（或多个）更简单的子步骤。

一个更精确的格式是 **Strang 分裂**（或称对称 [Lie-Trotter 分裂](@entry_id:751267)），它采用对称的组合方式：

$$
u^{n+1} = \exp\left(\frac{\Delta t}{2} A\right) \exp(\Delta t B) \exp\left(\frac{\Delta t}{2} A\right) u^n
$$

这种对称结构通常能带来更高的精度。

这些格式的精度根源于[算子指数](@entry_id:198199)的性质，尤其是当算子 $A$ 和 $B$ 不对易（non-commuting）时，即它们的 **[交换子](@entry_id:158878)** (commutator) $[A,B] = AB - BA \neq 0$。如果 $A$ 和 $B$ 对易，则 $\exp(t(A+B)) = \exp(tA)\exp(tB)$，此时 [Lie-Trotter 分裂](@entry_id:751267)是精确的。然而，[算子分裂法](@entry_id:752962)的主要价值恰恰在于处理不对易的情况。

通过 **Baker-Campbell-Hausdorff (BCH) 公式**，我们可以对[有界算子](@entry_id:264879)的[分裂误差](@entry_id:755244)进行分析。对于 Lie-Trotter 格式，其单步传播算子与精确传播算子之差（即 **[局部截断误差](@entry_id:147703)**）为：

$$
\exp(\Delta t A)\exp(\Delta t B) - \exp(\Delta t (A+B)) = \frac{\Delta t^2}{2}[A,B] + \mathcal{O}(\Delta t^3)
$$

这个 $\mathcal{O}(\Delta t^2)$ 的局部误差意味着，在有限时间区间上累积后，**全局误差** 为 $\mathcal{O}(\Delta t)$，因此 Lie-Trotter 是一种 **一阶** 精确方法。

对于 Strang 分裂，其对称结构巧妙地消除了 $\Delta t^2$ 阶的误差项：

$$
\exp\left(\frac{\Delta t}{2}A\right)\exp(\Delta t B)\exp\left(\frac{\Delta t}{2}A\right) - \exp(\Delta t(A+B)) = \mathcal{O}(\Delta t^3)
$$

其局部误差为 $\mathcal{O}(\Delta t^3)$，这使得 Strang 分裂在全局上是 **二阶** 精确的。[@problem_id:3519196]

### 理论基础：[半群](@entry_id:153860)与收敛性

为了在更严格的数学框架内理解[算子分裂](@entry_id:634210)，尤其是在处理由[偏微分方程](@entry_id:141332)（PDE）导出的[无界算子](@entry_id:144655)时，我们需要引入 $C_0$ **[半群](@entry_id:153860)**（[强连续半群](@entry_id:272133)）的理论。

一个定义在巴拿赫空间 $X$ 上的[有界线性算子](@entry_id:180446)族 $\{T(t)\}_{t\ge 0}$ 被称为 $C_0$ **[半群](@entry_id:153860)**，如果它满足以下三个条件：
1.  $T(0) = I$ （$I$ 是[恒等算子](@entry_id:204623)）。
2.  $T(t+s) = T(t)T(s)$ 对所有 $t, s \ge 0$ 成立（[半群性质](@entry_id:271012)）。
3.  对每个 $x \in X$，映射 $t \mapsto T(t)x$ 在 $t=0$ 处是强连续的，即 $\lim_{t\downarrow 0}\lVert T(t)x - x\rVert = 0$。

与[半群](@entry_id:153860)紧密相关的是它的 **无穷小生成元** (infinitesimal generator) $G$，定义为：

$$
Gx = \lim_{t\downarrow 0} \frac{T(t)x - x}{t}
$$

其定义域 $D(G)$ 包含所有使上述极限存在的 $x \in X$。生成元 $G$ 唯一确定了[半群](@entry_id:153860) $T(t)$，我们通常记为 $T(t) = \exp(tG)$。Hille-Yosida 定理和 Lumer-Phillips 定理建立了生成元性质与半群存在性之间的深刻联系。[@problem_id:3519252]

在[算子分裂](@entry_id:634210)的背景下，最关键的理论保证来自于 **Lie-Trotter-Kato [乘积公式](@entry_id:137076)**。该公式指出，如果 $A$ 和 $B$ 分别是 $C_0$ 半[群的生成元](@entry_id:137215)，并且它们的和（在某种意义下）$A+B$ 也生成一个 $C_0$ [半群](@entry_id:153860) $\exp(t(A+B))$，那么对于任意 $u_0 \in X$ 和固定的 $t \ge 0$，当 $n \to \infty$ 时，Lie-Trotter 逼近在强拓扑意义下收敛到真解：

$$
\lim_{n\to\infty} \left( \exp\left(\frac{t}{n} A\right) \exp\left(\frac{t}{n} B\right) \right)^n u_0 = \exp(t(A+B))u_0
$$

这个定理为[算子分裂法](@entry_id:752962)提供了坚实的理论基础，证明了它不仅仅是一个启发式的近似，而是一个在极限情况下严格收敛到真解的[数值积分器](@entry_id:752799)。[@problem_id:3519196] [@problem_id:3519252]

要将[算子分裂](@entry_id:634210)与经典的数值分析理论联系起来，我们必须正确理解 **相容性 (consistency)**、**稳定性 (stability)** 和 **收敛性 (convergence)** 的概念。**Lax-Richtmyer 等价性定理** 指出，对于一个适定的线性初值问题，一个相容的线性[数值格式](@entry_id:752822)是收敛的当且仅当它是稳定的。在分析[算子[分裂](@entry_id:752962)法](@entry_id:755245)时，我们将整个分裂步骤，例如 $\Phi_{\Delta t} = \exp(\Delta t B)\exp(\Delta t A)$，视为一个 **单一的复合单步算子**。因此：
-   **相容性** 必须是针对完整耦合算子 $(A+B)$ 来评估的。也就是说，我们需要检验 $\Phi_{\Delta t}$ 与精确演化算子 $\exp(\Delta t(A+B))$ 的近似程度。仅仅检验子步骤的相容性是无意义的，因为[分裂误差](@entry_id:755244)恰恰来自于算子的不对易性。
-   **稳定性** 要求复合算子 $\Phi_{\Delta t}$ 的幂次是一致有界的，即对任意 $n$ 使得 $n\Delta t \le T$（某个有限时间 $T$），存在一个常数 $M_T$ 使得 $\|\Phi_{\Delta t}^n\| \le M_T$。
-   对于线性的[算子分裂](@entry_id:634210)格式，Lax-Richtmyer 定理可以直接应用于复合算子 $\Phi_{\Delta t}$，从而将收敛性问题转化为验证其相容性和稳定性。[@problem_id:3519259]

### 稳定性与收缩半群

稳定性是任何[数值格式](@entry_id:752822)的生命线。[算子分裂法](@entry_id:752962)在处理[耗散系统](@entry_id:151564)时表现出的优异稳定性是其广受欢迎的关键原因之一。这与 **收缩[半群](@entry_id:153860)** (contraction semigroup) 的概念密切相关。

一个 $C_0$ 半群 $\{S(t)\}_{t \ge 0}$ 被称为 **收缩[半群](@entry_id:153860)**，如果它的算子范数满足 $\|S(t)\| \le 1$ 对所有 $t \ge 0$ 成立。这对应于一般 $C_0$ [半群](@entry_id:153860)范数界 $\|S(t)\| \le M e^{\omega t}$ 中 $M=1$ 和 $\omega=0$ 的特殊情况。物理上，收缩[半群](@entry_id:153860)描述的是能量不增的系统，例如纯[扩散过程](@entry_id:170696)。[@problem_id:3519232]

[收缩性](@entry_id:162795)质对[算子分裂](@entry_id:634210)的稳定性有着深远的影响。考虑 [Lie-Trotter 分裂](@entry_id:751267)，其单步算子为 $\Phi_{\Delta t} = \exp(\Delta t A) \exp(\Delta t B)$。如果子演化 $\exp(\Delta t A)$ 和 $\exp(\Delta t B)$ 都是收缩的，那么由于[算子范数](@entry_id:752960)的[次乘性](@entry_id:276284) (submultiplicativity)，我们有：

$$
\|\Phi_{\Delta t}\| = \|\exp(\Delta t A) \exp(\Delta t B)\| \le \|\exp(\Delta t A)\| \|\exp(\Delta t B)\| \le 1 \cdot 1 = 1
$$

同样，对于 Strang 分裂，其单步[算子范数](@entry_id:752960)也满足 $\|\Phi_{\Delta t}\| \le 1$。这意味着，如果系统的每个物理子过程都是耗散的，那么通过[算子分裂](@entry_id:634210)构造的[数值格式](@entry_id:752822)的每一步都是非扩张的（norm non-increasing）。这直接保证了数值解的范数不会随时间增长，从而实现了对任意时间步长 $\Delta t$ 都成立的 **[无条件稳定性](@entry_id:145631)**。这种强大的稳定性是[算子分裂](@entry_id:634210)方法在求解[抛物型方程](@entry_id:144670)和耗散型多物理场问题时的一个核心优势。[@problem_id:3519196] [@problem_id:3519232]

### 应用与变体

[算子分裂](@entry_id:634210)的思想在各种数值方法中都有体现。以下是一些经典的应用。

#### 交替方向隐式（ADI）方法

对于[多维偏微分方程](@entry_id:752273)，全[隐式格式](@entry_id:166484)虽然稳定，但需要求解巨大的耦合[线性系统](@entry_id:147850)，计算成本高昂。ADI 方法通过[算子分裂](@entry_id:634210)将多维[问题分解](@entry_id:272624)为一系列一维问题来解决这一困难。

以[二维热方程](@entry_id:746155) $u_t = \nu(u_{xx} + u_{yy})$ 为例，我们可以定义算子 $A = \nu \partial_{xx}$ 和 $B = \nu \partial_{yy}$。由于偏导数可以交换次序，这两个算子是对易的 ($[A,B]=0$)。**Peaceman-Rachford ADI** 格式是基于 Crank-Nicolson 方法的一种分裂，它近似于一个二阶精度的对称分裂：

$$
\left(I - \frac{\Delta t}{2} A\right)u^{(1)} = \left(I + \frac{\Delta t}{2} B\right)u^n
$$
$$
\left(I - \frac{\Delta t}{2} B\right)u^{n+1} = \left(I + \frac{\Delta t}{2} A\right)u^{(1)}
$$

该格式将一个二维隐式求解过程（涉及一个大的[带状矩阵](@entry_id:746657)）替换为两个一维隐式求解过程（每个只涉及一个简单的三对角矩阵），大大降低了计算复杂度。另一种相关的格式是 **Douglas ADI** 方法，它提供了不同的分裂方式，有时在处理更复杂问题时具有更好的稳定性。[@problem_id:3519217]

#### [不可压缩流](@entry_id:140301)的分数步法

在计算流体力学中，**Chorin-Temam [投影法](@entry_id:144836)** 是求解不可压缩 [Navier-Stokes](@entry_id:276387) 方程的经典分数步法。[Navier-Stokes](@entry_id:276387) 方程包含[动量方程](@entry_id:197225)和[不可压缩性约束](@entry_id:750592) $\nabla \cdot \boldsymbol{u} = 0$。[投影法](@entry_id:144836)将这两个部分解耦：

1.  **预测步（[动量输运](@entry_id:139628)）**: 首先，求解一个忽略[压力梯度](@entry_id:274112)的中间速度场 $\boldsymbol{u}^\star$。这一步通常包含[对流](@entry_id:141806)和[扩散](@entry_id:141445)项，例如：
    $$
    \frac{\boldsymbol{u}^\star - \boldsymbol{u}^n}{\Delta t} = -(\boldsymbol{u}^n \cdot \nabla_h)\boldsymbol{u}^n + \nu \nabla_h^2 \boldsymbol{u}^\star + \boldsymbol{f}^n
    $$
    这里，我们对黏性项（[扩散](@entry_id:141445)）采用了隐式处理，对[对流](@entry_id:141806)项采用了显式处理。得到的中间[速度场](@entry_id:271461) $\boldsymbol{u}^\star$ 通常不满足[不可压缩性约束](@entry_id:750592)，即 $\nabla_h \cdot \boldsymbol{u}^\star \neq 0$。

2.  **投影步（[压力修正](@entry_id:753714)）**: 接着，通过引入压力 $p^{n+1}$ 将 $\boldsymbol{u}^\star$ 投影到[无散度](@entry_id:190991)空间上，得到最终的[速度场](@entry_id:271461) $\boldsymbol{u}^{n+1}$。这一步可以看作是：
    $$
    \frac{\boldsymbol{u}^{n+1} - \boldsymbol{u}^\star}{\Delta t} = -\frac{1}{\rho}\nabla_h p^{n+1}
    $$
    为了确定压力，我们对上式两边取散度，并强制要求 $\nabla_h \cdot \boldsymbol{u}^{n+1} = 0$，从而得到一个关于压力的 **[泊松方程](@entry_id:143763)**：
    $$
    \nabla_h^2 p^{n+1} = \frac{\rho}{\Delta t} \nabla_h \cdot \boldsymbol{u}^\star
    $$
    求解这个泊松方程得到压力 $p^{n+1}$ 后，再通过 $\boldsymbol{u}^{n+1} = \boldsymbol{u}^\star - \frac{\Delta t}{\rho} \nabla_h p^{n+1}$ 更新速度。压力在此扮演了[拉格朗日乘子](@entry_id:142696)的角色，其梯度场恰好将中间速度场中不满足约束的部分“修正”掉。[@problem_id:3519260]

#### 隐式-显式（IMEX）方法

对于形如 $u' = F(u) + G(u)$ 的方程，其中 $F$ 是刚性项（如[扩散](@entry_id:141445)），$G$ 是非刚性项（如[平流](@entry_id:270026)或反应），除了[算子分裂](@entry_id:634210)，还可以使用 **IMEX** 方法。与[算子分裂](@entry_id:634210)将演化分解为多个子流的复合不同，IMEX 方法在单个时间步内对不同项采用不同的离散格式。例如，一阶 IMEX-Euler 格式为：

$$
\frac{u^{n+1} - u^n}{\Delta t} = G(u^n) + F(u^{n+1})
$$

这里，非刚性项 $G$ 被显式处理（在 $t^n$ 时刻取值），而刚性项 $F$ 被隐式处理（在 $t^{n+1}$ 时刻取值）。这构成了一个关于 $u^{n+1}$ 的[非线性方程](@entry_id:145852)：$u^{n+1} - \Delta t F(u^{n+1}) = u^n + \Delta t G(u^n)$。这个方程的求解只涉及刚性算子 $F$。与[算子分裂](@entry_id:634210)相比，IMEX 方法不是子流的复合，而是在单步格式内部混合了显式和隐式评估。[@problem_id:3519225]

### 高级主题与实践挑战

在实际应用中，[算子分裂](@entry_id:634210)的实施会遇到一系列更深层次的挑战。

#### 耦合系统的[分区方法](@entry_id:170629)

对于多场耦合问题，例如：
$$
\frac{\partial u}{\partial t} = A(u) + C(u,v), \qquad \frac{\partial v}{\partial t} = B(v) + D(u,v)
$$
其中 $A, B$ 是自算子，$C, D$ 是耦合项，**[分区方法](@entry_id:170629) (Partitioned Methods)** 是一种特殊形式的[算子分裂](@entry_id:634210)。最直接的分区策略是使用 **滞后耦合 (lagged coupling)**，即在一个时间步内，每个场的求解都使用来自前一时刻的其它场的数据。这种类似 Jacobi 迭代的格式允许并行求解各个物理场：
-   求解 $\dfrac{\partial u}{\partial t} = A(u) + C(u, v^n)$ 得到 $u^{n+1}$。
-   求解 $\dfrac{\partial v}{\partial t} = B(v) + D(u^n, v)$ 得到 $v^{n+1}$。
这种显式处理耦合项的方式虽然简单且易于实现，但它在耦合项中引入了一个 $\mathcal{O}(\Delta t)$ 的误差，因此通常只会得到[一阶精度](@entry_id:749410)。另一种策略是类似 Gauss-Seidel 迭代的顺序更新，例如在求解 $v$ 时使用刚刚计算出的 $u^{n+1}$，这可能会改善稳定性和收敛性，但牺牲了并行性。[@problem_id:3519237]

#### 离散化引发的误差

一个非常微妙但重要的问题是，[空间离散化](@entry_id:172158)过程可能会破坏[连续算子](@entry_id:143297)的代数性质，从而对[算子分裂](@entry_id:634210)的精度产生意想不到的影响。一个典型的例子是[平流-扩散方程](@entry_id:746317) $u_t = a u_{xx} + b u_x$。在连续层面，[微分算子](@entry_id:140145) $A = a \partial_{xx}$ 和 $B = b \partial_x$ 是对易的，即 $[A, B] = 0$。然而，当我们使用标准的[有限差分](@entry_id:167874)方法对它们进行离散时，得到的离散[矩阵算子](@entry_id:269557) $A_h$ 和 $B_h$ 通常是 **不对易** 的，即 $[A_h, B_h] \neq 0$。

这种离散化引入的非对易性意味着，即使在连续层面分裂是精确的，在离散层面也会产生[分裂误差](@entry_id:755244)。更糟糕的是，这个离散交换子 $[A_h, B_h]$ 的范数可能随着[网格加密](@entry_id:168565)（$h \to 0$）而急剧增长。例如，对于标准的[中心差分](@entry_id:173198)和一阶[迎风差分](@entry_id:173570)，可以证明 $\|[A_h, B_h]\| = \mathcal{O}(h^{-3})$。这导致 [Lie-Trotter 分裂](@entry_id:751267)的局部误差项 $\frac{\Delta t^2}{2}[A_h, B_h]$ 的范数行为像 $\mathcal{O}(\Delta t^2 h^{-3})$。为了保证该误差项在 $h \to 0$ 时收敛到零，时间步长 $\Delta t$ 必须与空间步长 $h$ 满足特定的约束关系，例如 $\Delta t = o(h^{1.5})$。如果 $\Delta t$ 和 $h$ 的关系不满足此要求（例如，在双曲 CFL 条件下 $\Delta t \sim \mathcal{O}(h)$），[分裂误差](@entry_id:755244)会发散，导致[数值格式](@entry_id:752822)不相容。这种现象被称为 **依赖于网格的相容性** (grid-dependent consistency)，是设计高保真[多物理场模拟](@entry_id:145294)时必须考虑的一个关键问题。[@problem_id:3519229]

#### 边界条件的处理

在分裂方法中，如何处理边界条件是另一个充满挑战的难题，尤其当边界条件本身耦合了不同的物理过程时。考虑一个带有 Robin 边界条件 $\nu \partial_x u(0,t) + \kappa u(0,t) = s(t)$ 的[平流-扩散](@entry_id:151021)问题。这里，Neumann 迹 $\partial_x u$ 自然地与[扩散算子](@entry_id:136699) $A$ 相关，而 Dirichlet 迹 $u$ 自然地与平流算子 $B$ 的流入边界相关。

简单地将边界条件的一部分分配给一个子步骤，另一部分分配给另一个子步骤，通常会导致不一致和精度损失。例如，在[扩散](@entry_id:141445)步中施加 $\nu \partial_x u = s(t)$ 而在平流步中施加 $u=0$ 是不正确的。一种更精确且物理上一致的方法是采用 **“通信”边界条件** (communicating boundary conditions)。在这种策略中：
-   在求解 **平流子问题** 时，需要一个 Dirichlet 入流条件。这个值可以通过完整的 Robin 边界条件 $u = (s - \nu \partial_x u)/\kappa$ 来确定。其中缺失的 Neumann 迹 $\partial_x u$ 必须由 **[扩散](@entry_id:141445)子问题** 提供一个足够精确的近似，并且为了保持[高阶精度](@entry_id:750325)，该值需要在时间步的[中心点](@entry_id:636820)进行评估。
-   同样，在求解 **[扩散](@entry_id:141445)子问题** 时，可以施加一个 Robin 条件。但其中的 Dirichlet 迹 $u$ 必须由 **平流子问题** 提供相应的近似值。

这种跨子步骤的信息交换确保了在每个子步骤中，施加的边界条件都是对完整物理边界条件的[高阶近似](@entry_id:262792)。如果简单地使用来自上一个时间步的滞后信息，通常会导致边界处的局部误差降低为一阶，进而污染整个计算域，使得像 Strang 分裂这样的二阶格式降阶为一阶。因此，对边界条件的精细处理对于[算子分裂](@entry_id:634210)方法的精度和稳定性至关重要。[@problem_id:3519201]