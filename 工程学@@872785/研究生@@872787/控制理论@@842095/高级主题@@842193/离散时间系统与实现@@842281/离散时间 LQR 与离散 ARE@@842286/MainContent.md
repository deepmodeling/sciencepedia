## 引言
[离散时间线性二次调节器](@entry_id:174424)（LQR）问题是现代控制理论的基石，它为如何以最优方式控制动态系统提供了一个优雅而强大的数学框架。其核心在于，为线性系统找到一个控制策略，使得系统状态在趋于稳定的同时，相关的二次型性能指标（通常代表能量消耗和状态偏差）达到最小。这一看似简单的问题背后，隐藏着深刻的数学原理，其解——[离散代数Riccati方程](@entry_id:168652)（DARE）——不仅是控制领域的核心方程，其思想和工具更广泛地渗透到信号处理、经济学等多个学科。然而，对于初学者而言，从抽象的数学表述到直观的物理理解，再到实际应用，常常存在知识上的鸿沟。

本文旨在系统性地填补这一鸿沟，引领读者全面掌握[离散时间LQR](@entry_id:174424)与DARE。我们将分三步展开：
- **第一部分：原理与机制**，我们将从[LQR问题](@entry_id:267315)的构建出发，利用动态规划和[Richard Bellman](@entry_id:136980)的最优性原理，一步步推导出[离散代数Riccati方程](@entry_id:168652)（DARE）。您将学习到DARE镇定解的含义、其存在的充分必要条件（能镇性与能检性），以及稳健的数值求解方法。
- **第二部分：应用与交叉学科联系**，我们将视野从核心理论扩展到更广阔的应用领域。您将看到LQR原理如何自然地推广到处理随机噪声的LQG问题，如何为带约束的[模型预测控制](@entry_id:146965)（MPC）提供稳定性保证，以及在[数字控制](@entry_id:275588)实现中需要注意的关键问题。
- **第三部分：动手实践**，我们将理论付诸实践，通过一系列精心设计的编程练习，让您亲手计算DARE的解，并在仿真中验证[LQR控制器](@entry_id:267871)的性能。

通过这一系列的学习，您不仅将理解LQR的“是什么”和“为什么”，更将掌握如何将其作为强大工具，应用于解决更复杂、更现实的工程与科学问题。

## 原理与机制

本章旨在深入探讨[离散时间线性二次调节器](@entry_id:174424)（LQR）问题的基本原理，并阐明其核心机制。我们将从问题表述出发，通过动态规划方法推导出[离散代数Riccati方程](@entry_id:168652)（DARE），分析其解的存在性、唯一性与稳定性，并最终介绍其数值求解方法。

### [离散时间LQR](@entry_id:174424)问题的构建

[离散时间LQR](@entry_id:174424)问题旨在为线性时不变（LTI）系统找到一个[最优控制](@entry_id:138479)策略，以最小化一个二次型性能指标。考虑以下[离散时间LTI系统](@entry_id:188941)：
$$
x_{k+1} = A x_k + B u_k
$$
其中，$x_k \in \mathbb{R}^n$ 是系统在时刻 $k$ 的状态向量，$u_k \in \mathbb{R}^m$ 是控制输入向量。矩阵 $A$ 和 $B$ 分别是[状态转移矩阵](@entry_id:269075)和输入矩阵。

[LQR问题](@entry_id:267315)的目标是寻找一个控制序列 $\{u_k\}_{k=0}^\infty$，以最小化如下的无限时域二次性能指标（或称[代价泛函](@entry_id:268062)）：
$$
J(x_0, \{u_k\}) = \sum_{k=0}^{\infty} \left( x_k^{\top} Q x_k + 2 x_k^{\top} N u_k + u_k^{\top} R u_k \right)
$$
其中，$x_0$ 是给定的初始状态。权重矩阵 $Q \in \mathbb{R}^{n \times n}$、$R \in \mathbb{R}^{m \times m}$ 和 $N \in \mathbb{R}^{n \times m}$ 用于权衡状态误差和控制能量。通常，我们要求 $Q$ 为[对称半正定矩阵](@entry_id:163376)（$Q = Q^{\top} \succeq 0$），$R$ 为[对称正定矩阵](@entry_id:136714)（$R = R^{\top} \succ 0$）。交叉权重项 $2 x_k^{\top} N u_k$ 则描述了[状态和](@entry_id:193625)控制之间的耦合惩罚。

为了确保该[优化问题](@entry_id:266749)是良构的（well-posed），即存在唯一的最小化解（如果有限代价的解存在），[代价泛函](@entry_id:268062) $J$ 作为控制序列 $\{u_k\}$ 的函数必须是**严格凸 (strictly convex)** 的。要确定保证[严格凸性](@entry_id:193965)的最小条件，我们可以考察代价的二阶变分。对于任意非零的控制变分序列 $\{\delta u_k\}$，其引起的二阶代价变分 $\delta^2 J$ 必须为正。可以证明，这等价于要求每个时刻的阶段代价 $L_k(x_k, u_k) = x_k^{\top} Q x_k + 2 x_k^{\top} N u_k + u_k^{\top} R u_k$ 是一个[凸函数](@entry_id:143075)，并且在某些时刻是严格凸的。

保证阶段代价非负的条件是其二次型对应的[分块矩阵](@entry_id:148435)为半正定：
$$
\begin{bmatrix} Q  N \\ N^{\top}  R \end{bmatrix} \succeq 0
$$
这个条件利用舒尔补引理（Schur complement lemma），在 $R \succ 0$ 的情况下等价于 $Q - N R^{-1} N^{\top} \succeq 0$。为了保证[严格凸性](@entry_id:193965)，我们考虑任意一个非零的控制变分序列 $\{\delta u_k\}$。设 $k_0$ 是第一个使得 $\delta u_{k_0} \neq 0$ 的时刻。由于 $\delta x_0=0$ 且在 $k \le k_0$ 时 $\delta x_k$ 仅依赖于之前的零变分输入，我们有 $\delta x_{k_0} = 0$。因此，二阶代价变分 $\delta^2 J$ 的第一项非零贡献来自时刻 $k_0$，其值为 $\delta u_{k_0}^{\top} R \delta u_{k_0}$。为了使 $\delta^2 J  0$，我们需要这一项严格为正，即 $\delta u_{k_0}^{\top} R \delta u_{k_0}  0$。这正是要求 $R$ 为正定矩阵（$R \succ 0$）的根本原因。因此，保证[代价泛函](@entry_id:268062)对任何系统 $(A, B)$ 都是严格凸的最小假设是 $R \succ 0$ 且 $\begin{bmatrix} Q  N \\ N^{\top}  R \end{bmatrix} \succeq 0$ [@problem_id:2700972]。

### [贝尔曼方程](@entry_id:138644)与最优性原理

解决[LQR问题](@entry_id:267315)的核心工具是[Richard Bellman](@entry_id:136980)的**最优性原理 (Principle of Optimality)**。该原理指出，一个最优策略的任何子策略也必须是最优的。对于无限时域、时不变问题，这导出了一个[稳态](@entry_id:182458)的**[贝尔曼方程](@entry_id:138644) (Bellman equation)**。

我们假设最优代价（从状态 $x$ 出发）是一个关于 $x$ 的二次函数，称为**[价值函数](@entry_id:144750) (value function)**，形式为 $V(x) = x^{\top} P x$，其中 $P$ 是一个[对称半正定矩阵](@entry_id:163376)。根据最优性原理，最优[价值函数](@entry_id:144750)必须满足：
$$
V(x_k) = \min_{u_k} \left\{ x_k^{\top} Q x_k + 2 x_k^{\top} N u_k + u_k^{\top} R u_k + V(x_{k+1}) \right\}
$$
将 $V(x) = x^{\top} P x$ 和[系统动力学](@entry_id:136288) $x_{k+1} = A x_k + B u_k$ 代入上式，我们得到：
$$
x_k^{\top} P x_k = \min_{u_k} \left\{ x_k^{\top} Q x_k + 2 x_k^{\top} N u_k + u_k^{\top} R u_k + (A x_k + B u_k)^{\top} P (A x_k + B u_k) \right\}
$$
这个方程是推导LQR[最优控制](@entry_id:138479)器和相关[Riccati方程](@entry_id:184132)的出发点。

### DARE的推导与[最优控制](@entry_id:138479)律

为了求解[贝尔曼方程](@entry_id:138644)中的最小化问题，我们考察右侧括号内的表达式，它是一个关于 $u_k$ 的二次函数。将其对 $u_k$ 求导并令其为零，可以找到最优控制输入 $u_k^*$。[展开表](@entry_id:756360)达式并对 $u_k$ 求导：
$$
\frac{\partial}{\partial u_k} \left( \dots \right) = 2 N^{\top} x_k + 2 R u_k + 2 B^{\top} P A x_k + 2 B^{\top} P B u_k = 0
$$
整理后得到：
$$
(R + B^{\top} P B) u_k = -(B^{\top} P A + N^{\top}) x_k
$$
由于 $R \succ 0$ 且 $P \succeq 0$，矩阵 $(R + B^{\top} P B)$ 是正定的，因此可逆。由此，我们得到最优控制律是一个线性的**[状态反馈](@entry_id:151441) (state-feedback)**：
$$
u_k^* = - (R + B^{\top} P B)^{-1} (B^{\top} P A + N^{\top}) x_k
$$
这可以写成 $u_k = -K x_k$ 的形式，其中最优[反馈增益](@entry_id:271155)矩阵 $K$ 为：
$$
K = (R + B^{\top} P B)^{-1} (B^{\top} P A + N^{\top}) \quad [@problem_id:2700990]
$$
将[最优控制](@entry_id:138479) $u_k^*$ 代回[贝尔曼方程](@entry_id:138644)，并要求该等式对所有 $x_k$ 成立，我们就能得到一个关于未知矩阵 $P$ 的[代数方程](@entry_id:272665)。经过化简，该方程为：
$$
P = A^{\top} P A + Q - (A^{\top} P B + N) (R + B^{\top} P B)^{-1} (B^{\top} P A + N^{\top})
$$
这个非[线性[矩阵方](@entry_id:203443)程](@entry_id:203695)被称为**[离散代数Riccati方程](@entry_id:168652) (Discrete Algebraic Riccati Equation, DARE)** [@problem_id:2701002]。它是[离散时间LQR](@entry_id:174424)理论的核心。

### 镇定解及其存在性

DARE通常有多个解，但我们关心的是其中能够使[闭环系统](@entry_id:270770)稳定的解。闭环[系统动力学](@entry_id:136288)为 $x_{k+1} = (A - BK)x_k$。一个DARE的解 $P = P^{\top} \succeq 0$ 如果其对应的[反馈增益](@entry_id:271155) $K$ 使得闭环矩阵 $A-BK$ 是**舒尔稳定 (Schur stable)**的（即所有[特征值](@entry_id:154894)的模都严格小于1），则该解被称为**镇定解 (stabilizing solution)** [@problem_id:2701002]。只有镇定解才能保证状态收敛到零，从而使无限时域代价 $J$ 为有限值。

一个核心问题是：在什么条件下，DARE存在唯一的半正定镇定解？答案由LQR理论中的一个基本定理给出，该定理涉及两个重要的系统性质：能镇性和能检性 [@problem_id:2701017]。

1.  **能镇性 (Stabilizability)**：如果系统 $(A,B)$ 是能镇定的，意味着所有不稳定的模式（即 $A$ 的[特征值](@entry_id:154894) $|\lambda| \ge 1$ 对应的模式）都是可控的。这是存在一个镇定[反馈增益](@entry_id:271155) $K$ 的充要条件。从物理直觉上看，如果系统存在一个自身不稳定且无法通过控制输入影响的模式，那么无论如何设计控制器，该模式都将导致状态发散，代价无穷大。因此，**能镇性是存在镇定解的必要条件**。

2.  **能检性 (Detectability)**：如果系统 $(A, C)$ 是能检测的（在[LQR问题](@entry_id:267315)中，通常取 $C=Q^{1/2}$），意味着所有不稳定的模式都是可观测的。在代价函数的语境下，这意味着任何不稳定的状态轨迹都会被 $x_k^{\top}Qx_k$ 项“察觉”到，从而产生非零代价。如果一个不稳定的模式是不可检测的，例如存在一个特征对 $(\lambda, v)$ 使得 $Av = \lambda v$（$|\lambda| \ge 1$）且 $Qv = 0$，那么当初始状态为 $x_0=v$ 时，即使系统状态 $x_k = \lambda^k v$ 发散，[代价函数](@entry_id:138681)中的状态惩罚项 $x_k^{\top}Qx_k$ 始终为零。此时，[最优控制](@entry_id:138479)器为了最小化代价，将不会花费任何控制能量去抑制这个不稳定的模式（即令 $u_k=0$），导致闭环系统不稳定。这说明[优化问题](@entry_id:266749)本身无法提供稳定该模式的“动机” [@problem_id:2700949]。因此，**能检性也是存在镇定解的必要条件**。

事实上，LQR理论的基石之一就是如下定理：对于 $R \succ 0$ 和 $Q \succeq 0$ 的[LQR问题](@entry_id:267315)，**当且仅当系统对 $(A,B)$ 是能镇定的，且系统对 $(A,Q^{1/2})$ 是能检的时**，DARE存在唯一的半正定镇定解 $P$ [@problem_id:2701017]。

### DARE的诠释与等价形式

#### DARE作为[不动点方程](@entry_id:203270)

DARE可以从动态规划的迭代角度来理解。对于有限时域[LQR问题](@entry_id:267315)，价值函数矩阵通过一个向后的差分方程（Riccati[差分方程](@entry_id:262177)）$P_k = \mathcal{R}(P_{k+1})$ 进行迭代。其中，$\mathcal{R}$ 是一个映射，称为**Riccati算子 (Riccati operator)**。无限时域问题可以看作是时域趋于无穷的极限。当迭代收敛时，我们得到一个[稳态解](@entry_id:200351) $P^{\star}$，它满足 $P^{\star} = \mathcal{R}(P^{\star})$。这表明，DARE的解正是Riccati算子的**[不动点](@entry_id:156394) (fixed point)**。从更根本的层面说，这是因为无限时域的[贝尔曼方程](@entry_id:138644) $V^{\star} = T(V^{\star})$ 本身就是一个[不动点方程](@entry_id:203270)，而DARE正是这个方程在二次[价值函数](@entry_id:144750)假设下的代数体现 [@problem_id:2700973]。

#### 交叉项的处理：[配方法](@entry_id:265480)

当代价函数中存在交叉项 $2x_k^{\top}Nu_k$ 时，除了直接求解包含 $N$ 的DARE之外，还有一种等价的变换方法，即**[配方法](@entry_id:265480) (completing the square)** [@problem_id:2700971]。通过引入一个新的[控制变量](@entry_id:137239) $\tilde{u}_k = u_k + R^{-1}N^{\top}x_k$，可以将原[代价函数](@entry_id:138681)变换为一个不含[交叉](@entry_id:147634)项的[标准形式](@entry_id:153058)：
$$
x_k^{\top} Q x_k + 2 x_k^{\top} N u_k + u_k^{\top} R u_k = x_k^{\top} (Q - N R^{-1} N^{\top}) x_k + \tilde{u}_k^{\top} R \tilde{u}_k
$$
同时，[系统动力学](@entry_id:136288)也相应改变：
$$
x_{k+1} = (A - B R^{-1} N^{\top}) x_k + B \tilde{u}_k
$$
这样，原问题就转化为了一个具有新状态矩阵 $\tilde{A} = A - B R^{-1} N^{\top}$ 和新状态权重 $\tilde{Q} = Q - N R^{-1} N^{\top}$ 的标准[LQR问题](@entry_id:267315)。求解这个标准问题得到最优反馈 $\tilde{u}_k = -\tilde{K}x_k$，再变换回原始[控制变量](@entry_id:137239)，即可得到原问题的[最优控制](@entry_id:138479)律 $u_k = -(\tilde{K} + R^{-1}N^{\top})x_k$。这个方法不仅在求解上提供了便利，也深刻揭示了交叉项的本质——它等价于对系统动力学和状态代价进行了一次反馈式的修正。

#### 与连续时间LQR的对比

[离散时间LQR](@entry_id:174424)的结构与连续时间LQR有显著区别，理解这些区别至关重要 [@problem_id:2701023]。
*   **[最优性条件](@entry_id:634091)**：[离散时间LQR](@entry_id:174424)基于[贝尔曼方程](@entry_id:138644)（差分方程），而连续时间LQR基于Hamilton-Jacobi-Bellman（HJB）方程（[偏微分方程](@entry_id:141332)）。这两种原理在本质上都是动态规划，但前者处理离散时间步，后者处理连续时间流 [@problem_id:2701023]。
*   **[Riccati方程](@entry_id:184132)**：连续代数[Riccati方程](@entry_id:184132)（CARE）的形式为 $A^{\top}P + PA - PBR^{-1}B^{\top}P + Q = 0$，而DARE的形式如前所述。DARE包含 $A^{\top}PA$ 项，反映了状态在一个时间步内的演化，而CARE包含 $A^{\top}P+PA$ 项，反映了状态的[瞬时变化率](@entry_id:141382)。
*   **最优增益**：连续时间LQR的最优增益为 $K_c = R^{-1}B^{\top}P$，而离散时间的最优增益为 $K_d = (R+B^{\top}PB)^{-1}(B^{\top}PA+N^{\top})$（以 $N=0$ 为例）。$K_d$ 中的 $B^{\top}PB$ 项体现了离散[时间控制](@entry_id:263806)的“一步预测”效应：当前的控制 $u_k$ 会影响下一时刻的状态 $x_{k+1}$，从而影响未来的代价 $x_{k+1}^{\top}Px_{k+1}$。这个二次项 $u_k^{\top}B^{\top}PBu_k$ 在最小化时与 $u_k^{\top}Ru_k$ 合并，导致了 $R+B^{\top}PB$ 这一项的出现。而在连续时间中，这种效应是无穷小量，因此不改变增益的结构 [@problem_id:2701023]。

### DARE的数值求解

DARE是一个[非线性方程组](@entry_id:178110)，直接迭代求解可能不稳定或不收敛。一种可靠且广泛使用的数值方法是基于**[辛矩阵](@entry_id:142706)束 (symplectic pencil)** 的几何特性 [@problem_id:2700976]。

首先，通过[LQR问题](@entry_id:267315)的[哈密顿系统](@entry_id:143533)必要条件，可以构建一个 $2n \times 2n$ 的[矩阵束](@entry_id:751760) $\mathcal{N} - z\mathcal{M}$，其中：
$$
\mathcal{N} = \begin{bmatrix} A  0 \\ -Q  I \end{bmatrix}, \quad \mathcal{M} = \begin{bmatrix} I  BR^{-1}B^{\top} \\ 0  A^{\top} \end{bmatrix}
$$
这个[矩阵束](@entry_id:751760)的广义[特征值](@entry_id:154894)对应于[哈密顿系统](@entry_id:143533)的动力学模式。DARE的镇定解 $P$ 与这个[矩阵束](@entry_id:751760)的一个特定**不变子空间 (invariant subspace)** 密切相关。具体来说，$P$ 定义了一个 $n$ 维[子空间](@entry_id:150286)，其上的向量满足 costate-state 关系 $p_k = Px_k$。可以证明，这个[子空间](@entry_id:150286)恰好是与[矩阵束](@entry_id:751760)在单位圆内的 $n$ 个广义[特征值](@entry_id:154894)相对应的[稳定不变子空间](@entry_id:755318) [@problem_id:2700976]。

基于这一理论，一个数值稳定的求解算法是使用**[广义舒尔分解](@entry_id:749792) (generalized Schur decomposition)**，也称为[QZ算法](@entry_id:753987) [@problem_id:2700997]。算法步骤如下：
1.  **构建[矩阵束](@entry_id:751760)**：根据给定的 $A, B, Q, R$ 构建上述 $2n \times 2n$ 矩阵 $\mathcal{N}$ 和 $\mathcal{M}$。
2.  **QZ分解与排序**：计算矩阵对 $(\mathcal{N}, \mathcal{M})$ 的[广义舒尔分解](@entry_id:749792)，得到正交矩阵 $U, V$ 和上三角（或准上三角）矩阵 $S, T$，使得 $U^{\top}\mathcal{N}V=S$ 和 $U^{\top}\mathcal{M}V=T$。然后，对分解进行重排，使得与稳定广义[特征值](@entry_id:154894)（模小于1）对应的对角块位于 $S$ 和 $T$ 的左上角。
3.  **提取[不变子空间](@entry_id:152829)基**：重排后，[正交矩阵](@entry_id:169220) $V$ 的前 $n$ 列构成了[稳定不变子空间](@entry_id:755318)的一组[标准正交基](@entry_id:147779)。我们将 $V$ 分块为 $$V = \begin{bmatrix} V_{11}  V_{12} \\ V_{21}  V_{22} \end{bmatrix}$$，其中 $V_{11}, V_{21} \in \mathbb{R}^{n \times n}$。那么 $\begin{bmatrix} V_{11} \\ V_{21} \end{bmatrix}$ 就是这个[子空间的基](@entry_id:160685)。
4.  **恢复解P**：由于这个基张成的空间与 $\begin{bmatrix} I \\ P \end{bmatrix}$ 张成的空间相同，必然存在一个[可逆矩阵](@entry_id:171829) $Z$ 使得 $\begin{bmatrix} V_{11} \\ V_{21} \end{bmatrix} = \begin{bmatrix} I \\ P \end{bmatrix} Z$。由此可得 $Z=V_{11}$ 和 $V_{21}=PV_{11}$。在能镇性和能检性的保证下，$V_{11}$ 是可逆的，因此可以解出 $P$：
    $$
    P = V_{21}V_{11}^{-1}
    $$
这个基于QZ分解的方法避免了直接迭代DARE可能带来的数值问题，是现代控制软件库中求解DARE的标准算法。