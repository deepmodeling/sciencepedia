## 引言
在现代科学与工程领域，对复杂非线性系统进行高效仿真是其核心追求之一。[降阶模型](@entry_id:754172)（ROMs）通过将高维动力学系统投影到低维[子空间](@entry_id:150286)，为此提供了一条充满希望的路径。然而，在处理非线性算子时，一个关键挑战随之出现：在标准的降阶框架中，计算这些[非线性](@entry_id:637147)项的成本往往仍然与原始高维系统相关，从而形成了一个严重的计算瓶颈，削弱了模型降阶的初衷。我们如何才能打破这种依赖关系，从而为[非线性](@entry_id:637147)问题完全释放[降阶模型](@entry_id:754172)的潜力？

答案在于一类被称为“超降阶”的技术，其中，[经验插值法](@entry_id:748957)（EIM）及其变体作为一种功能强大且用途广泛的方法脱颖而出。本文旨在全面探讨用于非[线性算子](@entry_id:149003)的EIM。**“原理与机制”**一章将深入剖析计算瓶颈的根源，并详细阐述EIM的基本原理，从基的构建到确保计算效率的插值机制。随后，**“应用与跨学科连接”**一章将展示这些原理如何在不同的科学领域和数值方法（如[谱方法](@entry_id:141737)和间断[伽辽金法](@entry_id:749698)）中进行调整和应用，突显该方法的灵活性与实际影响力。最后，**“动手实践”**部分提供了具体的练习，旨在巩固理论理解，并将理论与实践联系起来。这种结构将引导读者从基础理论走向实际应用，首先从深入探讨使超降阶成为可能的核心原理开始。

## 原理与机制

在降阶模型（Reduced-Order Models, ROMs）的构建中，一个核心挑战是如何高效地处理[非线性](@entry_id:637147)项。标准的[伽辽金投影](@entry_id:145611)方法虽然能够降低系统的维度，但在处理[非线性偏微分方程](@entry_id:169481)时，其计算成本仍然可能与原始[全阶模型](@entry_id:171001)（Full-Order Model, FOM）的规模相关，从而削弱了降阶的优势。本章将深入探讨这一计算瓶颈的来源，并系统地介绍用于克服该瓶颈的各类超降阶（hyper-reduction）方法，重点阐述[经验插值法](@entry_id:748957)（Empirical Interpolation Method, EIM）及其变体的原理、机制与应用。

### [非线性降阶模型](@entry_id:172252)中的计算瓶颈

考虑一个由[谱方法](@entry_id:141737)或间断伽辽金（Discontinuous Galerkin, DG）方法[半离散化](@entry_id:163562)后得到的[非线性常微分方程](@entry_id:142950)（ODE）系统：
$$
\frac{d\mathbf{u}}{dt} = \mathbf{f}(\mathbf{u})
$$
其中，$\mathbf{u}(t) \in \mathbb{R}^{N}$ 是包含 $N$ 个自由度的状态向量，$\mathbf{f}: \mathbb{R}^{N} \to \mathbb{R}^{N}$ 是一个非线性算子。在降阶模型中，我们寻求一个低维近似 $\mathbf{u}(t) \approx \mathbf{V}\mathbf{a}(t)$，其中 $\mathbf{V} \in \mathbb{R}^{N \times r}$ 是一个列向量标准正交的基矩阵（$r \ll N$），$\mathbf{a}(t) \in \mathbb{R}^{r}$ 是降阶坐标。通过将该近似代入原系统并进行[伽辽金投影](@entry_id:145611)（即左乘 $\mathbf{V}^{\top}$），我们得到降阶后的ODE系统：
$$
\frac{d\mathbf{a}}{dt} = \mathbf{V}^{\top}\mathbf{f}(\mathbf{V}\mathbf{a})
$$
为了在时间步进中求解 $\mathbf{a}(t)$，我们需要在每个时间步中计算右侧的[非线性](@entry_id:637147)项。直接（或称为“朴素”）的计算过程包括三个步骤：
1.  **重构（Lifting）**: 从降阶坐标 $\mathbf{a}$ 计算高维状态近似 $\mathbf{u}_{\text{approx}} = \mathbf{V}\mathbf{a}$。这是一个 $(N \times r)$ 矩阵与 $(r \times 1)$ 向量的乘法，计算成本为 $\mathcal{O}(Nr)$。
2.  **[非线性](@entry_id:637147)函数求值**: 在高维空间中计算非线性算子 $\mathbf{f}(\mathbf{u}_{\text{approx}})$。由于 $\mathbf{f}$ 是作用于 $\mathbb{R}^{N}$ 向量的通用[非线性](@entry_id:637147)函数，此步骤的成本不可避免地与输入向量的维度 $N$ 相关，通常至少为 $\mathcal{O}(N)$。
3.  **投影（Projection）**: 将计算结果投影回降阶空间，即计算 $\mathbf{V}^{\top}(\mathbf{f}(\mathbf{u}_{\text{approx}}))$。这是一个 $(r \times N)$ 矩阵与 $(N \times 1)$ 向量的乘法，成本为 $\mathcal{O}(Nr)$。

整个过程的总计算成本由 $\mathcal{O}(Nr) + \text{Cost}(\mathbf{f})$ 主导，其[线性依赖](@entry_id:185830)于[全阶模型](@entry_id:171001)的维度 $N$。这种依赖性构成了计算瓶颈，使得即使 $r$ 很小，ROM的在线（online）计算效率也无法显著优于FOM。超降阶技术的目标正是为了打破这种对 $N$ 的依赖。[@problem_id:3383563]

### 一种精确方案：针对多项式[非线性](@entry_id:637147)的张量预计算

在特定情况下，如果非[线性算子](@entry_id:149003) $\mathbf{f}$ 具有特殊的多项式结构，我们可以通过一种“离线-在线”分解策略，完全消除在线计算对 $N$ 的依赖。

考虑一个二次[非线性](@entry_id:637147)问题，其算子可以表示为 $f_k(\mathbf{u}) = \sum_{i,j=1}^{N} \mathcal{T}_{ijk} u_i u_j$。将降阶近似 $u_i = \sum_{q=1}^{r} V_{iq} a_q$ 代入降阶系统的第 $m$ 个分量，我们得到：
$$
\dot{a}_m = \sum_{k=1}^{N} V_{mk} f_k(\mathbf{V}\mathbf{a}) = \sum_{k=1}^{N} V_{mk} \left( \sum_{i,j=1}^{N} \mathcal{T}_{ijk} \left(\sum_{q=1}^{r} V_{iq} a_q\right) \left(\sum_{s=1}^{r} V_{js} a_s\right) \right)
$$
通过重新[排列](@entry_id:136432)求和顺序，我们可以将所有涉及大维度 $N$ 的计算部分分离出来：
$$
\dot{a}_m = \sum_{q,s=1}^{r} \left( \sum_{k,i,j=1}^{N} V_{mk} \mathcal{T}_{ijk} V_{iq} V_{js} \right) a_q a_s
$$
括号内的部分构成一个三阶张量 $\mathcal{C}_{mqs} \in \mathbb{R}^{r \times r \times r}$，它仅依赖于固定的基矩阵 $\mathbf{V}$ 和算子定义 $\mathcal{T}$。因此，我们可以在“离线”阶段预先计算并存储这个降阶张量 $\mathcal{C}$。在“在线”阶段，对任意给定的降阶状态 $\mathbf{a}$，计算 $\dot{a}_m$ 变成了一个与 $N$ 无关的[张量缩并](@entry_id:193373)：
$$
\dot{a}_m = \sum_{q,s=1}^{r} \mathcal{C}_{mqs} a_q a_s
$$
计算所有 $r$ 个分量的成本为 $\mathcal{O}(r^3)$。这一思想可以推广到任意 $p$ 次多项式[非线性](@entry_id:637147)，其在线成本为 $\mathcal{O}(r^{p+1})$。[@problem_id:3383571]

这种张量预计算方法同样适用于参数依赖问题，前提是参数依赖性是**仿射（affine）**的。例如，如果算子具有形式 $B(\boldsymbol{\mu}) = \sum_{q=1}^{Q} \theta_q(\boldsymbol{\mu}) B_q$，其中 $\theta_q$ 是标量函数，$B_q$ 是常数算子，那么我们可以为每个 $B_q$ 预计算一个降阶张量 $\mathcal{C}_q$。在线阶段，只需计算 $Q$ 个标量 $\theta_q(\boldsymbol{\mu})$，然后对预计算的张量进行[线性组合](@entry_id:154743)即可，总成本为 $\mathcal{O}(Qr^{p+1})$，这仍然是独立于 $N$ 的。[@problem_id:3383571]

然而，张量预计算方法的适用范围有限：
1.  **非多项式结构**: 对于一般的非多项式[非线性](@entry_id:637147)，如 $\sin(\mathbf{u})$ 或涉及平方根、条件判断的复杂函数（例如，[气体动力学](@entry_id:147692)中的[黎曼求解器](@entry_id:754362)），无法进行上述的代数重排。此时，$\sin(\mathbf{V}\mathbf{a})$ 的计算必须首先构造 $N$ 维向量 $\mathbf{V}\mathbf{a}$。[@problem_id:3383563]
2.  **非[仿射参数](@entry_id:260625)依赖**: 如果参数 $\boldsymbol{\mu}$ 以一种复杂的非仿射方式影响算子，那么无法将其分解为少数几个可分离项的和，也就无法通过预计算有限个张量来覆盖整个[参数空间](@entry_id:178581)。[@problem_id:3383571]
3.  **高阶多项式的成本**: 即使对于多项式[非线性](@entry_id:637147)，$\mathcal{O}(r^{p+1})$ 的计算成本会随着降阶维度 $r$ 或多项式次数 $p$ 的增加而急剧增长。当 $r$ 或 $p$ 稍大时，这种所谓的“维度之咒”可能使得在线计算依然非常昂贵。[@problem_id:3383563]

在这些情况下，我们需要一种更通用的、基于近似的超降阶方法。

### 通用近似方法：[经验插值法](@entry_id:748957) (EIM)

[经验插值法](@entry_id:748957)（EIM）及其离散变体（DEIM）为处理一般非线性算子提供了一个强大的框架。其核心思想是，尽管[非线性](@entry_id:637147)项 $\mathbf{f}(\mathbf{u})$ 所在的空间维度 $N$ 很高，但在模拟过程中，所有可能出现的 $\mathbf{f}(\mathbf{u}(t))$ 构成的集合（即[非线性](@entry_id:637147)[流形](@entry_id:153038) $\mathcal{F} = \{\mathbf{f}(\mathbf{u}(t)) | t \in [0, T]\}$）通常具有一个低维结构。

**1. 基的构建**

EIM的第一步是为这个[非线性](@entry_id:637147)[流形](@entry_id:153038) $\mathcal{F}$ 构建一个低维的近似基。这通常通过以下方式实现：
-   在离线阶段，运行一次或多次[全阶模型](@entry_id:171001)模拟，并对不同时刻 $t_k$ 和/或不同参数 $\boldsymbol{\mu}_k$ 下的[非线性](@entry_id:637147)项 $\mathbf{f}(\mathbf{u}^{(k)}; \boldsymbol{\mu}^{(k)})$ 进行采样，形成一个“快照”矩阵 $\mathbf{S} = [\mathbf{f}^{(1)}, \mathbf{f}^{(2)}, \dots, \mathbf{f}^{(K)}]$。
-   对快照矩阵 $\mathbf{S}$ 进行奇异值分解（SVD）或主成分分析（POD），提取其前 $m$ 个能量最大的[左奇异向量](@entry_id:751233)，构成一个[标准正交基](@entry_id:147779)矩阵 $\mathbf{U} \in \mathbb{R}^{N \times m}$。这个基 $\mathbf{U}$ 张成了一个能够很好地近似[非线性](@entry_id:637147)[流形](@entry_id:153038) $\mathcal{F}$ 的低维[子空间](@entry_id:150286)，我们称之为**旁系空间（collateral space）**。

有了这个基，任何[非线性](@entry_id:637147)项的实例都可以近似地表示为其列向量的线性组合：
$$
\mathbf{f}(\mathbf{u}) \approx \mathbf{U} \mathbf{c}(\mathbf{u})
$$
其中 $\mathbf{c}(\mathbf{u}) \in \mathbb{R}^{m}$ 是待定的系数向量。

**2. 系数的确定：插值**

接下来的关键问题是如何高效地确定系数 $\mathbf{c}(\mathbf{u})$。通过[伽辽金投影](@entry_id:145611) $\mathbf{c} = \mathbf{U}^{\top}\mathbf{f}(\mathbf{u})$ 来求解是不可行的，因为它仍然需要计算完整的 $N$ 维向量 $\mathbf{f}(\mathbf{u})$。

DEIM巧妙地采用了**插值**的思想。它选择 $m$ 个“插值点”（即向量 $\mathbf{f}(\mathbf{u})$ 的 $m$ 个分量索引），并要求近似解在这些点上与真实值完全相等。令 $\mathbf{P} \in \mathbb{R}^{N \times m}$ 为一个选择矩阵，其每一列是 $\mathbb{R}^N$ 的一个[标准基向量](@entry_id:152417)，用于从一个向量中提取出 $m$ 个指定索引处的分量。插值条件可以写作：
$$
\mathbf{P}^{\top}\mathbf{f}(\mathbf{u}) = \mathbf{P}^{\top}(\mathbf{U}\mathbf{c}) = (\mathbf{P}^{\top}\mathbf{U})\mathbf{c}
$$
这是一个 $m \times m$ 的[线性方程组](@entry_id:148943)。如果插值点选择得当，矩阵 $\mathbf{P}^{\top}\mathbf{U}$ 是非奇异的，我们便可以解出系数：
$$
\mathbf{c}(\mathbf{u}) = (\mathbf{P}^{\top}\mathbf{U})^{-1} \mathbf{P}^{\top}\mathbf{f}(\mathbf{u})
$$
插值点的选择至关重要，通常采用一种贪心算法（如基于 $\mathbf{U}$ 的主元[LU分解](@entry_id:144767)）来选取，以确保 $\mathbf{P}^{\top}\mathbf{U}$ 的条件数尽可能小。

**3. 超降阶系统**

将系数表达式代回，我们得到[非线性](@entry_id:637147)项的DEIM近似：
$$
\mathbf{f}(\mathbf{u}) \approx \mathbf{U} (\mathbf{P}^{\top}\mathbf{U})^{-1} \mathbf{P}^{\top}\mathbf{f}(\mathbf{u})
$$
将此近似代入原始的降阶ODE系统，得到最终的超降阶系统：
$$
\frac{d\mathbf{a}}{dt} \approx \mathbf{V}^{\top}\left( \mathbf{U} (\mathbf{P}^{\top}\mathbf{U})^{-1} \mathbf{P}^{\top}\mathbf{f}(\mathbf{V}\mathbf{a}) \right)
$$
为了实现在线高效计算，我们可以进行[离线-在线分解](@entry_id:177117)。在离线阶段，预先计算并存储矩阵 $\tilde{\mathbf{V}} = \mathbf{V}^{\top}\mathbf{U} \in \mathbb{R}^{r \times m}$ 和 $\mathbf{M} = (\mathbf{P}^{\top}\mathbf{U})^{-1} \in \mathbb{R}^{m \times m}$。在线计算流程变为：
1.  计算高维状态在 $m$ 个插值点处的值：$(\mathbf{P}^{\top}\mathbf{V})\mathbf{a}$。
2.  仅在这 $m$ 个点上计算[非线性](@entry_id:637147)函数 $\mathbf{f}$ 的值，得到向量 $\mathbf{f}_{\mathcal{P}} = \mathbf{P}^{\top}\mathbf{f}(\mathbf{V}\mathbf{a}) \in \mathbb{R}^m$。
3.  通过一系列小规模矩阵乘法计算最终结果：$\dot{\mathbf{a}} \approx \tilde{\mathbf{V}} \mathbf{M} \mathbf{f}_{\mathcal{P}}$。

整个在线计算过程的成本主要由 $\mathcal{O}(mr)$ 和 $\mathcal{O}(m^2)$ 决定，完全独立于全阶维度 $N$。[@problem_id:3383618]

### 应用与高级专题

EIM框架的成功应用依赖于一系列理论和实践考量。以下我们将探讨几个关键方面。

#### 快照收集策略

旁系基 $\mathbf{U}$ 的质量直接决定了DEIM近似的精度，而基的质量又取决于离线阶段收集的快照集。一个好的快照集应该能够充分“探索”[非线性](@entry_id:637147)[流形](@entry_id:153038) $\mathcal{F}$。以下是一些有效的策略：[@problem_id:3383595]
-   **[参数扫描](@entry_id:142676)**: 对于含参问题，应在参数空间 $\mathcal{P}$ 中进行系统性采样（例如，通过实验设计），尤其是在参数空间的边界和高敏感度区域，以确保生成的基对整个参[数域](@entry_id:155558)都具有良好的代表性。
-   **随机扰动**: 在从轨迹上采集的快照 $\mathbf{f}(\mathbf{u}^{(k)})$ 基础上，可以增加一些在状态 $\mathbf{u}^{(k)}$ 附近施加小随机扰动后生成的快照，如 $\mathbf{f}(\mathbf{u}^{(k)} + \epsilon \boldsymbol{\eta}^{(j)})$。从[泰勒展开](@entry_id:145057)的角度看，这相当于向快照集中添加了雅可比矩阵作用于随机方向的向量 $\mathbf{J}_{\mathbf{f}} \boldsymbol{\eta}$，有助于更好地捕捉[非线性](@entry_id:637147)[流形](@entry_id:153038)的局部几何特性（切空间），从而提高基的鲁棒性。
-   **残差驱动的自适应方法**: 这是一种[贪心算法](@entry_id:260925)。从一个初始基开始，在一个预先准备的[训练集](@entry_id:636396)上评估DEIM近似误差（通常使用[后验误差估计](@entry_id:167288)器）。然后，找到误差最大的那个状态-参数对 $(\mathbf{u}_{\star}, \boldsymbol{\mu}_{\star})$，并将对应的[非线性](@entry_id:637147)项 $\mathbf{f}(\mathbf{u}_{\star}; \boldsymbol{\mu}_{\star})$（或其误差分量）添加到快照集中以扩充基。这个过程迭代进行，直到误差满足要求。这种方法可以确保在每次迭代中，[训练集](@entry_id:636396)上的最大误差是单调不减的。
-   **一个重要的警示**: 必须强调，快照必须是针对非[线性算子](@entry_id:149003)输出 $\mathbf{f}(\mathbf{u})$ 进行的，而不是状态向量 $\mathbf{u}$ 本身。$\mathbf{f}(\mathbf{u})$ 和 $\mathbf{u}$ 所在的[向量空间](@entry_id:151108)和[流形](@entry_id:153038)结构完全不同，混淆两者是一个根本性的错误。

#### 在间断伽辽金（DG）方法中的应用

[DG方法](@entry_id:748369)因其在处理[双曲守恒律](@entry_id:147752)方面的优势而备受关注。其半离散算子通常包含单元内部的**体积积分项**和单元边界上的**[面积分](@entry_id:275394)（或数值通量）项**。[@problem_id:3383619]
$$
M_{e}\dot{\mathbf{u}}_{e} = \mathbf{f}_{e}(\mathbf{u}) = \underbrace{-B_{e} \mathbf{F}_{e}(\mathbf{u})}_{\text{体积项}} + \underbrace{\mathbf{t}_{e}^{L} \hat{F}_{e}^{L} - \mathbf{t}_{e}^{R} \hat{F}_{e}^{R}}_{\text{面积项}}
$$
其中，体积项涉及在单元内部大量求积点上计算[非线性](@entry_id:637147)物理通量 $\mathbf{F}(\mathbf{u})$，是计算成本的主要来源。面积项则包含在单元界面上计算的数值通量 $\hat{F}$，它耦合了相邻单元。

在对[DG方法](@entry_id:748369)应用超降阶时，一个常见的策略是仅对计算密集的体积项使用EIM近似，而精确计算面积项。这样做有两个好处：1) 大幅降低了计算成本；2) 精确处理单元间的耦合有助于保持原始[DG格式](@entry_id:178043)的稳定性和守恒性。经过EIM近似后，局部算子变为：
$$
f_{e}^{(m)}(\mathbf{u}) = - B_{e} U (P^{\top}U)^{-1} P^{\top} \mathbf{F}_{e}(\mathbf{u}) + \mathbf{t}_{e}^{L} \hat{F}_{e}^{L} - \mathbf{t}_{e}^{R} \hat{F}_{e}^{R}
$$
全局算子则通过对所有单元的局部算子进行组装得到：$f^{(m)}(\mathbf{u}) = \sum_{e=1}^{E} R_{e} f_{e}^{(m)}(\mathbf{u})$。[@problem_id:3383619]

#### 经验求积法 (EQM)

对于形如 $\int_{\Omega} \phi(x) g(u(x)) dx$ 的[非线性](@entry_id:637147)积分项，除了直接对被积函数 $g(u)$ 进行插值外，还有一种更直接的方法，称为经验求积法（Empirical Quadrature Method, EQM）。其核心思想是构建一个定制的[求积法则](@entry_id:753909)：
$$
\int_{\Omega} \phi(x) g(u(x)) dx \approx \sum_{i=1}^{m} w_{i} \phi(x_{i}) g(u(x_{i}))
$$
这里的求积点 $\{x_i\}$ 可以通过DEIM类型的贪心算法选择，而[求积权重](@entry_id:753910) $\{w_i\}$ 则不是像高斯求积那样来自某个固定的规则，而是“经验地”通过求解一个[线性系统](@entry_id:147850)来确定。具体来说，我们要求这个[求积法则](@entry_id:753909)对所有训练快照 $\{u^{(k)}(x)\}$ 都精确成立，这会导出一个关于 $\{w_i\}$ 的[线性方程组](@entry_id:148943)。离线求解得到固定的权重后，在线计算就变成了一个简单的加权求和。[@problem_id:3383569]

#### [谱方法](@entry_id:141737)中的去混淆处理

在[傅里叶谱方法](@entry_id:749538)中，[非线性](@entry_id:637147)项（如 $u^2$）通常通过在物理空间的[配置点](@entry_id:169000)上进行逐点相乘来计算，这在谱空间中等价于[循环卷积](@entry_id:147898)。由于计算是在有限个点上进行的，这会引入**混淆误差（aliasing error）**，即高波数的能量会“折叠”回来污染低波数的模式。如果使用被混淆误差污染的快照来构建旁系基 $\mathbf{U}$，会导致基的效率降低，因为基的一部分“容量”被用来表示这些非物理的、虚假的频率成分。

为了生成“干净”的快照，必须进行去混淆处理。对于二次[非线性](@entry_id:637147)，标准的**$3/2$规则**可以完美地消除混淆。其过程是：
1.  将原始的 $N$ 个傅里叶系数通过[补零](@entry_id:269987)扩展到一个长度为 $M = 3N/2$ 的数组中。
2.  对这个长数组进行[逆傅里叶变换](@entry_id:178300)，得到在一个更精细的 $M$ 点网格上的物理值。
3.  在这个精细网格上进行逐点相乘。
4.  将结果变换回谱空间，得到长度为 $M$ 的谱系数。由于网格足够精细，此时的卷积是线性的，不会发生折叠。
5.  截断这些谱系数，只保留原始波数范围（$|k| \le N/2$）内的模式。
6.  将截断后的“干净”谱系数逆变换回原始的 $N$ 点物理网格，作为快照。

通过这种方式生成的快照不含混淆误差，由此构建的基 $\mathbf{U}$ 能够更有效地表示真实的[非线性](@entry_id:637147)[流形](@entry_id:153038)，其奇异值衰减通常更快，从而可以用更小的 $m$ 达到相同的近似精度。[@problem_id:3383601]

#### 边界条件的处理

在许多物理问题中，边界条件的处理至关重要。为了让超降阶模型天然地尊重边界条件，一种有效的方法是**约束插值**。具体操作如下：
1.  在定义全阶算子 $\mathbf{f}(\mathbf{u})$ 时，将与边界条件相关的自由度（例如，[DG方法](@entry_id:748369)中的“[鬼点](@entry_id:177889)”）包含在内。
2.  采集快照时，这些边界自由度的值也被一并记录。
3.  在执行DEIM的插值点选择时，强制要求所有 $n_b$ 个边界自由度对应的索引必须被选为插值点。
4.  剩余的 $m - n_b$ 个插值点则通过标准的贪心算法从内部自由度中选择。

通过这种方式构建的选择矩阵 $\mathbf{P}$，可以确保DEIM近似在边界点上是完全精确的，从而将边界条件的影响无缝地整合到超降阶算子中，避免了任何需要后处理的步骤。[@problem_id:3383591]

#### 误差与[稳定性分析](@entry_id:144077)

虽然超降阶方法在[计算效率](@entry_id:270255)上带来了巨大提升，但它引入了新的近似误差源，可能对模型的稳定性和[长期行为](@entry_id:192358)产生影响。一个关键的概念是**[交换子误差](@entry_id:747515)（commutator error）**：
$$
E(u) = \mathcal{P}(\mathcal{N}(u)) - \tilde{\mathcal{N}}(\mathcal{P}(u))
$$
其中 $\mathcal{P}$ 是到低维[多项式空间](@entry_id:144410)的投影算子，$\mathcal{N}$ 是非线性算子，$\tilde{\mathcal{N}}$ 是EIM近似算子。这个误差度量了“先投影后近似”与“先计算后投影”之间的差异。

这个误差的存在意味着，即使原始的伽辽金方法（对应 $\mathcal{P}(\mathcal{N}(\mathcal{P}(u)))$）能够保持某些离散[不变量](@entry_id:148850)（如[能量守恒](@entry_id:140514)），经过EIM近似后，由于 $\tilde{\mathcal{N}}(\mathcal{P}(u)) \neq \mathcal{P}(\mathcal{N}(\mathcal{P}(u)))$，这些守恒性质可能会被破坏。[交换子误差](@entry_id:747515)在离散系统的[能量平衡](@entry_id:150831)中表现为一个非零的[源项](@entry_id:269111)或汇项，可能导致数值解的[能量不守恒](@entry_id:276143)，从而引发长期不稳定性或漂移。因此，理解并控制[交换子误差](@entry_id:747515)是发展稳定可靠的超降阶方法的关键研究方向。[@problem_id:3383607]

#### 关于计算成本的进一步思考

最后，我们回到计算成本的比较。对于 $p$ 次多项式[非线性](@entry_id:637147)，张量预计算的在线成本为 $\mathcal{O}(r^{p+1})$，而DEIM的成本为 $\mathcal{O}(mr + m^2)$。以三次[非线性](@entry_id:637147)为例，张量法的成本为 $\mathcal{O}(r^4)$，而DEIM的成本主要由 $\mathcal{O}(mr)$ 主导。要使DEIM的计算成本与张量法具有可比性，DEIM的采样点数 $m$ 需要如何随 $r$ 变化？一项分析表明，为了达到收支平衡，$m^{\star}(r) \propto r^2$。[@problem_id:3383627]

这揭示了一个重要的事实：虽然DEIM成功地消除了对全阶维度 $N$ 的依赖，但其自身的计算成本并非微不足道。采样点数 $m$ 的选择是在近似精度（需要较大的 $m$）和计算速度（需要较小的 $m$）之间的一个权衡。