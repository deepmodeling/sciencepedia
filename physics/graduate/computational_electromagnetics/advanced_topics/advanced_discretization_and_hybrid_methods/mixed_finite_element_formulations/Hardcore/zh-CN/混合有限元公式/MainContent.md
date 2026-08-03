## 引言
在计算科学与工程领域，混合有限元方法 (Mixed Finite Element Method) 是一种功能强大且数学上严谨的数值技术，尤其在计算电磁学中扮演着至关重要的角色。当直接求解基于麦克斯韦方程组的二阶矢量波动方程时，传统的有限元方法常常会产生被称为“伪模式”的非物理数值解，严重污染计算结果并影响其可靠性。混合有限元方法正是为了解决这一核心难题而生，它通过引入辅助变量来显式地施加系统中隐含的物理约束，不仅极大地提高了数值解的准确性和稳定性，也为我们洞察物理定律背后的深刻数学结构提供了窗口。

本文将引导读者全面掌握混合有限元公式。在第一章“原理与机制”中，我们将深入探讨伪模式产生的根源，并引入de Rham复形这一数学工具来揭示其拓扑本质。随后，我们将详细阐述如何利用拉格朗日乘子构建混合弱形式，并介绍用于精确离散化的Nédélec边元等适配有限元，以及保证方法稳定性的关键理论——LBB条件。接着，在第二章“应用与交叉学科联系”中，我们将展示这些理论在解决复杂电磁问题（如高级边界条件、多连通区域和多物理场耦合）时的威力，并探索其与流体力学、固体力学等其他学科的深刻联系。最后，“动手实践”部分提供了一系列精心设计的问题，旨在通过具体计算加深读者对离散空间构建、系统性质分析和潜在数值陷阱的理解。通过这三个章节的学习，读者将建立起从理论基础到实际应用的完整知识体系。

## 原理与机制

在计算电磁学中，混合有限元方法提供了一个强大而严谨的框架，用于求解麦克斯韦方程组。与直接求解场的二阶矢量波动方程的标准方法不同，混合方法通过引入辅助变量（通常是拉格朗日乘子）来明确地施加物理定律中隐含的约束。这种方法不仅提高了数值解的稳定性和准确性，还为我们提供了对电磁现象背后深刻数学结构的洞察。本章将系统地阐述混合有限元公式的原理和机制，从它们解决的根本问题出发，逐步揭示其理论基础和实际应用。

### 离散化麦克斯韦方程组的挑战：伪模式

求解时谐麦克斯韦方程组的一个常用策略是消去磁场 $\mathbf{H}$，从而得到关于电场 $\mathbf{E}$ 的二阶矢量波动方程。在无源、均匀、各向同性的介质中，这一过程始于法拉第定律和安培-麦克斯韦定律：
$$ \nabla \times \mathbf{E} = -i \omega \mu \mathbf{H} $$
$$ \nabla \times \mathbf{H} = i \omega \epsilon \mathbf{E} $$
将第一个方程中的 $\mathbf{H}$ 代入第二个方程的旋度，我们得到所谓的“旋度-旋度”方程：
$$ \nabla \times (\mu^{-1} \nabla \times \mathbf{E}) - \omega^2 \epsilon \mathbf{E} = \mathbf{0} $$
这个方程，连同适当的边界条件（例如，在理想电导体（PEC）边界上 $\mathbf{n} \times \mathbf{E} = \mathbf{0}$），构成了腔体本征值问题的基础。然而，当使用标准有限元方法直接离散化这个二阶方程时，经常会遇到一个严重的问题：**伪模式** (spurious modes) 的出现 [@problem_id:3331083]。

伪模式是数值计算产生的非物理本征解，它们污染了真实的物理谱，使得计算结果难以解释。在旋度-旋度方程的离散化中，最常见的伪模式是**梯度模式** (gradient modes)。这些模式是无旋场的离散表示，即 $\mathbf{E}_h = \nabla p_h$，其中 $p_h$ 是某个标量势的离散近似。由于 $\nabla \times (\nabla p_h) = \mathbf{0}$，这些场使得旋度-旋度算子的离散版本的核空间变得过大，导致在非零频率 $\omega_h \neq 0$ 处出现虚假的、类似于静电场的解。

那么，为什么连续的物理问题没有这些伪模式呢？答案在于一个被忽略的约束：高斯电场定律。在无源区域中，高斯定律要求 $\nabla \cdot (\epsilon \mathbf{E}) = 0$。这个散度为零的条件确保了真实的电场解与所有梯度场（在适当的边界条件下）是正交的。然而，标准的矢量波动方程弱形式并不能在离散层面自动强制执行这个散度约束。因此，离散解空间被不满足该约束的梯度模式所污染 [@problem_id:3331083]。

### de Rham 复形：电磁学的结构蓝图

伪模式问题的根源可以通过一个深刻的数学结构——**de Rham 复形** (de Rham complex) 来理解。这个复形揭示了微积分中基本微分算子（梯度、旋度和散度）之间的内在联系，并为电磁场论提供了数学上的“蓝图” [@problem_id:3331100]。在函数分析的框架下，对于一个有界、单连通的区域 $\Omega \subset \mathbb{R}^3$，相关的 de Rham 序列可以写作：
$$ H^1(\Omega) \xrightarrow{\nabla} H(\mathrm{curl}; \Omega) \xrightarrow{\nabla \times} H(\mathrm{div}; \Omega) \xrightarrow{\nabla \cdot} L^2(\Omega) \rightarrow 0 $$
这里，$H^1(\Omega)$、$H(\mathrm{curl}; \Omega)$、$H(\mathrm{div}; \Omega)$ 和 $L^2(\Omega)$ 是描述标量场和矢量场及其导数可积性的索博列夫空间（我们将在后续章节详细定义）。

这个序列被称为是**正合的** (exact)。正合性意味着在序列的每一步，前一个算子的**像** (image) 都恰好等于后一个算子的**核** (kernel)。这包含了两个关键的矢量恒等式及其逆命题：
1.  $\mathrm{im}(\nabla) = \ker(\nabla \times)$：这意味着在 $H(\mathrm{curl}; \Omega)$ 空间中，一个矢量场的旋度为零（即它是一个无旋场）的充要条件是，它是一个标量场的梯度。这正式地将旋度算子的核空间与梯度场等同起来。
2.  $\mathrm{im}(\nabla \times) = \ker(\nabla \cdot)$：这意味着在 $H(\mathrm{div}; \Omega)$ 空间中，一个矢量场的散度为零（即它是一个无散场或螺线场）的充要条件是，它是另一个矢量场的旋度。
3.  $\mathrm{im}(\nabla \cdot) = L^2(\Omega)$：这意味着任何 $L^2$ 标量场都可以是某个 $H(\mathrm{div}; \Omega)$ 矢量场的散度。

de Rham 复形的正合性精确地指出了伪模式的来源：旋度-旋度算子的核空间正是梯度场构成的空间 $\mathrm{im}(\nabla)$。物理上，高斯定律 $\nabla \cdot (\epsilon \mathbf{E}) = 0$ 将解限制在无散场的一个子空间中，从而排除了这些梯度模式。因此，一个成功的数值方法必须在离散层面有效地模拟或强制执行这个散度约束。

### 混合公式：用拉格朗日乘子施加约束

解决伪模式问题的最直接和最严谨的方法就是**混合有限元方法**。其核心思想是，不依赖于离散化过程能“自动”满足散度约束，而是通过引入一个**拉格朗日乘子** (Lagrange multiplier) 来明确地、以弱形式强制该约束 [@problem_id:3331081]。

我们从待求解的强形式方程组出发，该方程组同时包含矢量波动方程和高斯定律约束：
$$ \nabla \times (\mu^{-1} \nabla \times \mathbf{E}) - \omega^2 \epsilon \mathbf{E} + \nabla p = \mathbf{0} $$
$$ \nabla \cdot (\epsilon \mathbf{E}) = 0 $$
在这里，$p$ 是一个辅助的标量场，即拉格朗日乘子。它的梯度 $\nabla p$ 加入到第一个方程中，以强制执行第二个方程所代表的约束。

为了推导其弱形式，我们首先需要严格定义在函数空间中的散度算子。对于一个通常不具备足够光滑性的电通量密度场 $\mathbf{D} = \epsilon \mathbf{E} \in L^2(\Omega)^3$，其**弱散度** (weak divergence) 被定义为一个作用于检验函数空间上的泛函。为了避免处理在 $L^2$ 场上没有良定义的边界项，我们选择检验函数来自 $H_0^1(\Omega)$（在边界上为零的 $H^1$ 函数）。通过分部积分（即格林公式），我们定义弱散度 $\mathrm{div}_w(\mathbf{D})$ 对任意检验函数 $q \in H_0^1(\Omega)$ 的作用为 [@problem_id:3331109]：
$$ \langle \mathrm{div}_w(\mathbf{D}), q \rangle := - \int_{\Omega} \mathbf{D} \cdot \nabla q \, dx $$
这个定义构成了混合公式的基础。

现在，我们寻找解 $(\mathbf{E}, p)$ 所在的函数空间分别为 $H_0(\mathrm{curl}; \Omega)$ 和 $H_0^1(\Omega)$。我们将第一个强形式方程与检验函数 $\mathbf{F} \in H_0(\mathrm{curl}; \Omega)$ 做内积，第二个方程与检验函数 $q \in H_0^1(\Omega)$ 做内积，并在整个区域 $\Omega$ 上积分。通过分部积分，我们得到如下的混合弱形式：寻找 $(\mathbf{E}, p) \in H_0(\mathrm{curl}; \Omega) \times H_0^1(\Omega)$，使得对于所有的 $(\mathbf{F}, q) \in H_0(\mathrm{curl}; \Omega) \times H_0^1(\Omega)$，满足：
$$ (\mu^{-1} \nabla \times \mathbf{E}, \nabla \times \mathbf{F}) - \omega^2 (\epsilon \mathbf{E}, \mathbf{F}) + (\epsilon \mathbf{F}, \nabla p) = 0 $$
$$ (\epsilon \mathbf{E}, \nabla q) = 0 $$
这里，$(\cdot, \cdot)$ 表示标准的 $L^2$ 内积。注意第二个方程正是基于我们对弱散度的定义，它以弱形式强制了 $\nabla \cdot (\epsilon \mathbf{E}) = 0$ [@problem_id:3331081]。

这个鞍点问题可以写成如下的算子块矩阵形式 [@problem_id:3331074]：
$$
\begin{pmatrix}
A  & B^{T} \\
B  & 0
\end{pmatrix}
\begin{pmatrix}
\mathbf{E} \\
p
\end{pmatrix}
=
\begin{pmatrix}
\mathbf{0} \\
0
\end{pmatrix}
$$
其中，算子 $A$ 代表旋度-旋度项和质量项，算子 $B$ 代表散度约束，而 $B^T$ 是其伴随算子。这种结构在代数上非常重要，例如，我们可以通过**舒尔补** (Schur complement) 算子 $S = -B A^{-1} B^T$ 来形式上消去场 $\mathbf{E}$，得到一个只关于乘子 $p$ 的方程，这在理论分析和求解器设计中都扮演着核心角色。

### 精准的工具：矢量函数空间与有限元

为了将上述连续的混合弱形式转化为可计算的离散系统，我们需要为电磁场选择合适的有限元。这要求我们首先理解场本身所在的函数空间。

#### 核心函数空间
在电磁学中，最重要的两个矢量索博列夫空间是 $H(\mathrm{curl}; \Omega)$ 和 $H(\mathrm{div}; \Omega)$ [@problem_id:3331137]。
*   **$H(\mathrm{curl}; \Omega)$**：这个空间包含所有平方可积的矢量场 $\mathbf{u}$，其旋度 $\nabla \times \mathbf{u}$ 也是平方可积的。形式上，
    $$ H(\mathrm{curl}; \Omega) = \{ \mathbf{u} \in (L^2(\Omega))^3 : \nabla \times \mathbf{u} \in (L^2(\Omega))^3 \} $$
    这个空间是电场 $\mathbf{E}$ 和磁场 $\mathbf{H}$ 的自然归宿，因为法拉第定律和安培-麦克斯韦定律都涉及旋度。
*   **$H(\mathrm{div}; \Omega)$**：这个空间包含所有平方可积的矢量场 $\mathbf{u}$，其散度 $\nabla \cdot \mathbf{u}$ 是平方可积的。形式上，
    $$ H(\mathrm{div}; \Omega) = \{ \mathbf{u} \in (L^2(\Omega))^3 : \nabla \cdot \mathbf{u} \in L^2(\Omega) \} $$
    这个空间是电通量密度 $\mathbf{D}$ 和磁通量密度 $\mathbf{B}$ 的自然归宿，因为高斯定律涉及散度。

#### 迹与边界条件
这些空间的一个关键特性是它们具有良定义的**迹** (trace)，即场在边界 $\partial \Omega$ 上的值。
*   对于 $H(\mathrm{curl}; \Omega)$ 中的场 $\mathbf{u}$，其**切向迹** (tangential trace) $\gamma_t(\mathbf{u}) = \mathbf{n} \times \mathbf{u}|_{\partial \Omega}$ 是良定义的。这使得我们可以自然地施加像理想电导体 (PEC) 边界条件 $\mathbf{n} \times \mathbf{E} = \mathbf{0}$ 或理想磁导体 (PMC) 边界条件 $\mathbf{n} \times \mathbf{H} = \mathbf{0}$。
*   对于 $H(\mathrm{div}; \Omega)$ 中的场 $\mathbf{u}$，其**法向迹** (normal trace) $\gamma_n(\mathbf{u}) = \mathbf{n} \cdot \mathbf{u}|_{\partial \Omega}$ 是良定义的。这使得我们可以自然地施加像 PEC 边界上的 $\mathbf{n} \cdot \mathbf{B} = 0$ 或 PMC 边界上的 $\mathbf{n} \cdot \mathbf{D} = 0$。

#### 适配的有限元
为了使离散解能够忠实地逼近连续解，有限元基函数必须在单元之间保持与连续空间相匹配的连续性。这就催生了**适配有限元** (conforming finite elements) 家族。
*   **Nédélec 边单元 (Edge Elements)**：为了构造 $H(\mathrm{curl})$ 适配的有限元空间，我们需要保证矢量场在单元间切向连续。Nédélec 边单元通过将自由度与网格的**边**关联起来实现了这一点。最低阶的第一类 Nédélec 单元定义在一个四面体 $T$ 上的局部空间为 [@problem_id:3331124]：
    $$ V(T) = \{ \mathbf{v}(\mathbf{x}) = \mathbf{a} + \mathbf{b} \times \mathbf{x} \mid \mathbf{a}, \mathbf{b} \in \mathbb{R}^3 \} $$
    其自由度是矢量场沿六条边的切向分量的线积分，即 $\int_{e_\ell} \mathbf{v} \cdot \mathbf{t}_\ell \, ds$。通过在相邻单元间共享边的自由度，我们确保了场的切向分量是连续的。

*   **Raviart-Thomas 面单元 (Face Elements)**：为了构造 $H(\mathrm{div})$ 适配的有限元空间，我们需要保证矢量场在单元间法向连续。Raviart-Thomas 面单元通过将自由度与网格的**面**关联起来实现了这一点。最低阶的 RT 单元定义在一个四面体 $K$ 上的局部空间为 [@problem_id:3331135]：
    $$ RT_0(K) = \{ \mathbf{v}(\mathbf{x}) = \mathbf{a} + b\mathbf{x} \mid \mathbf{a} \in \mathbb{R}^3, b \in \mathbb{R} \} $$
    其自由度是矢量场穿过四个面的法向通量，即 $\int_{F} \mathbf{v} \cdot \mathbf{n}_F \, dS$。通过在相邻单元间共享面的自由度，我们确保了场的法向分量是连续的。

这些特殊的有限元，以及拉格朗日节点元（用于 $H^1$）和分片不连续单元（用于 $L^2$），共同构成了所谓的**有限元外微分** (Finite Element Exterior Calculus, FEEC) 的基础，它们为离散 de Rham 复形提供了稳定且精确的构建模块。从参考单元到物理单元的映射是通过保持相应连续性的**皮奥拉变换** (Piola transformations) 完成的 [@problem_id:3331135]。

### 稳定性与收敛性：混合方法的理论保证

我们已经有了弱形式和合适的有限元，但如何保证数值方法是有效的呢？一个混合方法必须是**稳定**的，这样才能保证解的存在性、唯一性，并且误差是可控的。

#### LBB (inf-sup) 条件
混合鞍点问题的稳定性由**Ladyzhenskaya–Babuška–Brezzi (LBB) 条件**（或称 **inf-sup 条件**）来保证 [@problem_id:3331102]。这个条件确保了拉格朗日乘子空间和原始场空间之间的耦合是“健康的”。对于我们之前讨论的混合问题，如果乘子空间选择为 $L_0^2(\Omega)$（零均值的 $L^2$ 函数），LBB 条件要求存在一个与网格尺寸无关的常数 $\beta > 0$，使得：
$$ \inf_{q \in L_0^2(\Omega)} \sup_{\mathbf{v} \in H_0(\mathrm{curl}, \Omega)} \frac{\int_\Omega \nabla \cdot (\epsilon \mathbf{v}) q \, d\mathbf{x}}{\|\mathbf{v}\|_{H(\mathrm{curl}, \Omega)} \|q\|_{L^2(\Omega)}} \ge \beta $$
这个条件可以这样理解：对于乘子空间中**任何**一个非零的“约束模式” $q$，我们总能找到一个场 $\mathbf{v}$，其散度与该模式有显著的耦合。这防止了某些约束模式变得“不可见”，从而导致离散系统奇异或近似病态。LBB 条件的满足是选择适配有限元对（例如 Nédélec 单元与分片不连续多项式）的关键，它保证了混合方法的鲁棒性。

#### 离散紧致性与谱收敛
对于本征值问题，我们不仅关心解的收敛，更关心整个**谱**的收敛，即计算出的本征值是否能准确逼近真实的物理本征值，并且没有伪模式。这需要一个比标准误差分析更强的理论工具，即**离散紧致性** (discrete compactness) [@problem_id:3331090]。

连续的麦克斯韦算子具有一个重要的**紧嵌入性质**：一个在能量范数下有界的弱无散场序列，必定包含一个在 $L^2$ 范数下收敛的子序列。离散紧致性是这一性质在离散有限元空间中的直接模拟。它断言，对于一个构造良好的有限元空间族（如 Nédélec 单元），一个在离散弱无散子空间中且旋度范数一致有界的序列，同样包含一个 $L^2$ 收敛的子序列。

离散紧致性的重要性在于，它是证明离散本征谱无污染收敛到连续谱的核心要素。现代有限元理论证明，对于 Nédélec 单元等适配元，可以通过构造满足特定**交换性质** (commuting property) 的投影算子来证明离散紧致性。这些交换算子构成了离散 de Rham 复形理论的基石，它保证了离散空间能够正确地模仿连续空间的拓扑结构 [@problem_id:3331090], [@problem_id:3331100]。最终，离散紧致性与谱近似理论相结合，为混合有限元方法在腔体谐振等问题中的可靠性提供了坚实的数学保证，确保了我们计算得到的是物理真实的模式，而非数值幻象。