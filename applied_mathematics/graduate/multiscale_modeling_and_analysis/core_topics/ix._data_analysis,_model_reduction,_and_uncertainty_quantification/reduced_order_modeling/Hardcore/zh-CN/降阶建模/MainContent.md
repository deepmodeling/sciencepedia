## 引言
在现代科学与工程领域，高保真数值仿真已成为理解、预测和设计复杂物理系统的基石。然而，这些通常基于有限元或有限体积等方法的[全阶模型](@entry_id:171001)（Full-Order Models, FOMs），往往具有数百万甚至更多的自由度，导致其计算成本极其高昂。这一瓶颈严重限制了它们在需要大量重复求解的应用场景中的使用，例如多学科设计优化、[不确定性量化](@entry_id:138597)、[实时控制](@entry_id:754131)和数字孪生。[降阶模型](@entry_id:754172)（Reduced-Order Models, ROMs）应运而生，旨在解决这一根本矛盾，它提供了一套强大的数学框架，能够从高维FOM中提取关键动态特性，构建出计算量极小但预测精度依然很高的低维代理模型。

本文将带领读者深入探索降阶建模的理论精髓与实践应用。在“**原理与机制**”一章中，我们将揭示降阶模型的核心——投影方法，并探讨如何通过[本征正交分解](@entry_id:165074)（POD）等技术从数据中提取[最优基](@entry_id:752971)底，以及如何利用超降阶等高级策略攻克非线性系统的计算瓶颈。接着，在“**应用与跨学科关联**”一章中，我们将通过[结构力学](@entry_id:276699)、流体力学、控制论乃至数据科学等领域的丰富案例，展示降阶模型作为一种赋能技术，如何解决各学科中的实际挑战。最后，“**动手实践**”部分将提供具体的编程练习，帮助读者将理论知识转化为实践技能。通过本文的学习，读者将全面掌握降阶建模的核心思想，并具备将其应用于解决实际问题的能力。

## 原理与机制

本章旨在阐述降阶模型（Reduced-Order Models, ROMs）背后的核心原理与关键机制。我们将从一个高维[全阶模型](@entry_id:171001)（Full-Order Model, FOM）出发，系统地探讨如何通过投影方法构建一个计算高效且能保持高保真度的低维代理。我们的讨论将涵盖降阶的核心思想——投影，基底的生成方法，[参数化](@entry_id:265163)系统的有效计算策略，以及处理[非线性](@entry_id:637147)问题的先进技术。

### 投影：降阶模型的核心机制

几乎所有侵入式降阶模型（intrusive reduced-order models）的构建都基于一个共同的核心思想：**投影（projection）**。其基本假设是，尽管一个物理系统在离散化后可能具有极高的自由度（例如，数百万），但其动态[行为的演化](@entry_id:183748)实际上被约束在一个维度远低于原始[状态空间](@entry_id:160914)的低维子空间内。我们的目标就是找到这个子空间，并将原始的控制方程投影到其上，从而得到一个规模小且易于求解的[降阶模型](@entry_id:754172)。

#### 状态近似与残差

考虑一个由有限元方法（FEM）等空间离散化技术得到的常微分方程（Ordinary Differential Equation, ODE）系统，它描述了一个动态系统的演化：
$$
\boldsymbol{M} \ddot{\boldsymbol{u}}(t) + \boldsymbol{C} \dot{\boldsymbol{u}}(t) + \boldsymbol{f}_{\mathrm{int}}(\boldsymbol{u}(t)) = \boldsymbol{f}_{\mathrm{ext}}(t)
$$
其中，$\boldsymbol{u}(t) \in \mathbb{R}^{n}$ 是系统的[状态向量](@entry_id:154607)（例如，节点位移），$n$ 是系统的自由度，通常非常大。$\boldsymbol{M}$, $\boldsymbol{C}$ 分别是质量矩阵和阻尼矩阵，$\boldsymbol{f}_{\mathrm{int}}$ 是（可能为[非线性](@entry_id:637147)的）[内力向量](@entry_id:750751)，$\boldsymbol{f}_{\mathrm{ext}}$ 是外力向量。

降阶的第一步是建立一个**状态近似（state approximation）**或** ansatz**。我们假设高维状态 $\boldsymbol{u}(t)$ 可以由一组精心挑选的[基向量](@entry_id:199546)的线性组合来精确近似。这组[基向量](@entry_id:199546)构成了我们所说的**降阶基底（reduced basis）**。令此基底由矩阵 $\boldsymbol{V} \in \mathbb{R}^{n \times r}$ 的列向量构成，其中 $r \ll n$ 是降阶模型的维度。于是，状态近似可以写作：
$$
\boldsymbol{u}(t) \approx \boldsymbol{V} \boldsymbol{q}(t)
$$
其中, $\boldsymbol{q}(t) \in \mathbb{R}^{r}$ 是**降阶坐标（reduced coordinates）**或[广义坐标](@entry_id:156576)的向量，它描述了系统在低维子空间中的状态。

将此近似代入原始控制方程，等式通常不再成立。这导致了一个**残差（residual）**向量 $\boldsymbol{r}(t) \in \mathbb{R}^{n}$：
$$
\boldsymbol{r}(t) = \boldsymbol{M}(\boldsymbol{V}\ddot{\boldsymbol{q}}) + \boldsymbol{C}(\boldsymbol{V}\dot{\boldsymbol{q}}) + \boldsymbol{f}_{\mathrm{int}}(\boldsymbol{V}\boldsymbol{q}) - \boldsymbol{f}_{\mathrm{ext}}(t) \neq \boldsymbol{0}
$$
降阶模型的任务就是寻找一个最优的降阶坐标演化路径 $\boldsymbol{q}(t)$，使得这个残差在某种意义上“最小”。投影方法正是通过强制残差与某个**测试子空间（test subspace）**正交来实现这一点的。

#### Galerkin 投影

最常用和最直观的投影方法是 **Galerkin 投影（Galerkin projection）**。在该方法中，我们选择测试子空间与**试验子空间（trial subspace）**相同，即由基底 $\boldsymbol{V}$ 的列[向量张成](@entry_id:152883)的子空间 $\mathrm{span}(\boldsymbol{V})$。 [正交性条件](@entry_id:168905)可以简洁地表示为：
$$
\boldsymbol{V}^{\top} \boldsymbol{r}(t) = \boldsymbol{0}
$$
这意味着[残差向量](@entry_id:165091)的每个分量在试验子空间的每个基向量方向上的投影均为零。将残差表达式代入，我们得到：
$$
\boldsymbol{V}^{\top} \left( \boldsymbol{M}\boldsymbol{V}\ddot{\boldsymbol{q}} + \boldsymbol{C}\boldsymbol{V}\dot{\boldsymbol{q}} + \boldsymbol{f}_{\mathrm{int}}(\boldsymbol{V}\boldsymbol{q}) - \boldsymbol{f}_{\mathrm{ext}} \right) = \boldsymbol{0}
$$
整理后，我们得到一个关于降阶坐标 $\boldsymbol{q}(t)$ 的 $r$ 维常微分方程系统：
$$
\boldsymbol{M}_r \ddot{\boldsymbol{q}}(t) + \boldsymbol{C}_r \dot{\boldsymbol{q}}(t) + \boldsymbol{f}_{r, \mathrm{int}}(\boldsymbol{q}(t)) = \boldsymbol{f}_{r, \mathrm{ext}}(t)
$$
其中，降阶算子定义如下：
- **降阶质量矩阵**: $\boldsymbol{M}_r = \boldsymbol{V}^{\top} \boldsymbol{M} \boldsymbol{V} \in \mathbb{R}^{r \times r}$
- **降阶阻尼矩阵**: $\boldsymbol{C}_r = \boldsymbol{V}^{\top} \boldsymbol{C} \boldsymbol{V} \in \mathbb{R}^{r \times r}$
- **降阶[内力向量](@entry_id:750751)**: $\boldsymbol{f}_{r, \mathrm{int}}(\boldsymbol{q}) = \boldsymbol{V}^{\top} \boldsymbol{f}_{\mathrm{int}}(\boldsymbol{V}\boldsymbol{q}) \in \mathbb{R}^{r}$
- **降阶外力向量**: $\boldsymbol{f}_{r, \mathrm{ext}}(t) = \boldsymbol{V}^{\top} \boldsymbol{f}_{\mathrm{ext}}(t) \in \mathbb{R}^{r}$



Galerkin 投影的一个优美特性是它能保持原始算子的数学性质。例如，如果[全阶模型](@entry_id:171001)中的质量矩阵 $\boldsymbol{M}$ 和刚度矩阵 $\boldsymbol{K}$ 是[对称正定](@entry_id:145886)的（Symmetric Positive Definite, SPD），并且降阶基底 $\boldsymbol{V}$ 是列满秩的，那么相应的降阶矩阵 $\boldsymbol{M}_r = \boldsymbol{V}^{\top} \boldsymbol{M} \boldsymbol{V}$ 和 $\boldsymbol{K}_r = \boldsymbol{V}^{\top} \boldsymbol{K} \boldsymbol{V}$ 也将是对称正定的。这保证了降阶模型在能量意义上是良态的。

值得注意的是，这种[基于投影的降阶模型](@entry_id:1130226)与简单的网格粗化有本质区别。网格粗化是重新离散化原始[偏微分](@entry_id:194612)方程，它使用通用的、具有局部支撑的基函数（如有限元形函数）。而降阶模型则是将一个已有的高保真离散模型投影到由**全局的**、**问题相关的**基[向量张成](@entry_id:152883)的子空间上。这些[基向量](@entry_id:199546)通常是从高保真模型的解中提取的，因此能高效地捕捉系统的主要动态特征。

#### Petrov-Galerkin 投影

在某些情况下，选择与试验子空间不同的测试子空间会带来好处。这种方法被称为 **Petrov-Galerkin 投影**。假设测试子空间由矩阵 $\boldsymbol{W} \in \mathbb{R}^{n \times r}$ 的列[向量张成](@entry_id:152883)，[正交性条件](@entry_id:168905)变为：
$$
\boldsymbol{W}^{\top} \boldsymbol{r}(t) = \boldsymbol{0}
$$
这会导出降阶方程 $\boldsymbol{W}^{\top}\boldsymbol{M}\boldsymbol{V}\ddot{\boldsymbol{q}} + \dots = \boldsymbol{W}^{\top}\boldsymbol{f}_{\mathrm{ext}}$。

Petrov-Galerkin 方法的一个重要应用是**[模型稳定性](@entry_id:636221)**的提升。例如，在求解以平流为主导的流体动力学问题时（例如[高雷诺数CFD](@entry_id:750318)），标准的 Galerkin 投影可能会产生非物理性的[数值振荡](@entry_id:163720)。这是因为离散算子违反了**[离散最大值原理](@entry_id:748510)**。具体而言，对于一维[平流扩散](@entry_id:268279)问题，当单元[佩克莱数](@entry_id:141791) $\mathrm{Pe} \equiv \frac{U h}{2 \nu} > 1$（其中 $U$ 为速度，$h$ 为单元尺寸，$\nu$ 为粘性系数）时，Galerkin 方法得到的离散格式中，顺风节点的系数会变为正值，从而导致不稳定。

为了解决这个问题，可以构造特殊的[测试函数](@entry_id:166589)，如**流线[迎风](@entry_id:756372)/[Petrov-Galerkin](@entry_id:174072) (Streamline-Upwind [Petrov-Galerkin](@entry_id:174072), SUPG)** 方法。SUPG通过在测试函数中引入一个沿流线方向的扰动项（$\psi_{i} = \phi_{i} + \tau U \frac{\partial \phi_{i}}{\partial x}$）来修改测试空间。这种修正等效于在原始方程中引入了[数值耗散](@entry_id:168584)项，也称为**[人工粘性](@entry_id:142854)（artificial viscosity）**，其大小与稳定化参数 $\tau$ 和速度的平方 $U^2$ 成正比。通过精心选择 $\tau$，可以确保离散算子的良好性质，从而抑制振荡并恢复模型的稳定性。

### 降阶基底的构建：[本征正交分解](@entry_id:165074) (POD)

投影方法框架的关键在于如何选择一个“好”的降阶基底 $\boldsymbol{V}$。一个理想的基底应该能够用尽可能少的[基向量](@entry_id:199546)来尽可能精确地表示系统的所有可能状态。**[本征正交分解](@entry_id:165074) (Proper Orthogonal Decomposition, POD)**，在流体力学中也称为 Karhunen-Loève 分解，正是为此目的而设计的黄金标准方法。

POD的核心思想是从系统的**快照（snapshots）**中提取[最优基](@entry_id:752971)底。快照是指在不同时间点或不同参数下，通过求解高保真[全阶模型](@entry_id:171001)得到的一系列状态向量 $\{\boldsymbol{u}_1, \boldsymbol{u}_2, \ldots, \boldsymbol{u}_m\}$。我们将这些快照向量作为列向量排列，构成**[快照矩阵](@entry_id:1131792)** $\boldsymbol{X} = [\boldsymbol{u}_1, \boldsymbol{u}_2, \ldots, \boldsymbol{u}_m] \in \mathbb{R}^{n \times m}$。

POD的目标是寻找一个 $r$ 维的[正交基](@entry_id:264024)底 $\{\boldsymbol{\phi}_i\}_{i=1}^r$，使得所有快照在其上的投影误差的平均和最小。即最小化：
$$
\min_{\{\boldsymbol{\phi}_i\}_{i=1}^r} \sum_{k=1}^{m} \left\| \boldsymbol{u}_k - \sum_{i=1}^{r} (\boldsymbol{u}_k^{\top}\boldsymbol{\phi}_i)\boldsymbol{\phi}_i \right\|_2^2
$$
这个问题等价于最大化投影分量的能量。可以证明，这个优化问题的解由[快照矩阵](@entry_id:1131792) $\boldsymbol{X}$ 的**奇异值分解 (Singular Value Decomposition, SVD)** 给出。

令 $\boldsymbol{X} = \boldsymbol{U}\boldsymbol{\Sigma}\boldsymbol{W}^{\top}$ 为[快照矩阵](@entry_id:1131792)的SVD，其中 $\boldsymbol{U} \in \mathbb{R}^{n \times n}$ 的列向量是[左奇异向量](@entry_id:751233)，$\boldsymbol{\Sigma} \in \mathbb{R}^{n \times m}$ 是对角矩阵，其对角线元素为[奇异值](@entry_id:152907) $\sigma_i$（按降序排列），$\boldsymbol{W} \in \mathbb{R}^{m \times m}$ 的列向量是[右奇异向量](@entry_id:754365)。POD的[最优基](@entry_id:752971)底正是由 $\boldsymbol{U}$ 的前 $r$ 个列向量构成，即 $\boldsymbol{V} = \boldsymbol{U}(:, 1:r)$。

[奇异值](@entry_id:152907) $\sigma_i$ 具有深刻的物理意义：$\sigma_i^2$ 代表了第 $i$ 个POD模态（即[基向量](@entry_id:199546) $\boldsymbol{\phi}_i$）所捕获的快照集合的“能量”（在[欧几里得范数](@entry_id:172687)意义下）。总能量为所有[奇异值](@entry_id:152907)平方和。因此，通过观察奇异值的衰减速度，我们可以决定截断维数 $r$。例如，可以选择 $r$ 使得捕获的能量达到总能量的99.99%：
$$
\frac{\sum_{i=1}^{r} \sigma_i^2}{\sum_{i=1}^{\text{rank}(\boldsymbol{X})} \sigma_i^2} \ge 0.9999
$$


标准的POD对于[欧几里得范数](@entry_id:172687)（$L^2$ 范数）是最优的。如果我们需要最优地表示其他物理量，例如动能（由质量矩阵 $\boldsymbol{M}$ 定义的[能量范数](@entry_id:274966) $\boldsymbol{u}^{\top}\boldsymbol{M}\boldsymbol{u}$）或应变能（由刚度矩阵 $\boldsymbol{K}$ 定义的[能量范数](@entry_id:274966) $\boldsymbol{u}^{\top}\boldsymbol{K}\boldsymbol{u}$），则需要使用**加权POD**。这可以通过对快照数据进行加权变换（例如，使用 $\boldsymbol{M}^{1/2}\boldsymbol{X}$）来求解一个[广义特征值问题](@entry_id:151614)。

### 模型的“可降阶性”：理论边界

[线性子空间](@entry_id:151815)逼近的有效性并非理所當然。一个系统是否能够被低维[线性子空间](@entry_id:151815)有效近似，取决于其**解流形（solution manifold）**的几何特性。解流形是指在[参数空间](@entry_id:178581) $\mathcal{P}$ 内所有可能解的集合 $\mathcal{M} = \{u(\boldsymbol{\mu}) | \boldsymbol{\mu} \in \mathcal{P}\}$。

**[Kolmogorov n-宽度](@entry_id:751055)（Kolmogorov n-width）** $d_n(\mathcal{M})$ 为我们提供了衡量解流形“可降阶性”的理论工具。它定义为用一个 $n$ 维[线性子空间](@entry_id:151815)去逼近流形 $\mathcal{M}$ 时，可能达到的最小[最坏情况误差](@entry_id:169595)。$d_n(\mathcal{M})$ 的快速衰减意味着存在高效的低维[线性逼近](@entry_id:142309)。

系统的可降阶性与解对参数的**光滑度**密切相关。
- **快速衰减（高可降阶性）**: 如果解映射 $\boldsymbol{\mu} \mapsto u(\boldsymbol{\mu})$ 是解析的（analytic），那么 [Kolmogorov n-宽度](@entry_id:751055)会呈指数级衰减。这通常发生在控制方程的算子对参数是解析依赖且问题保持稳定（例如，一致强制性）的情况下。在动力学问题中，如果外部激励的频率被限制在某个截止频率之下，系统的响应主要由少数低频模态主导，高频模态的贡献很小，此时系统也表现出良好的可降阶性。
- **缓慢衰减（低可降阶性）**: 如果问题中存在随参数移动的局部特征，如冲击波、锋面或移动的波包，那么解流形将具有高度的[非线性](@entry_id:637147)。任何固定的线性基底都难以有效表示这种平移特征，导致 [Kolmogorov n-宽度](@entry_id:751055)衰减缓慢（通常是代数级衰减）。此外，如果问题在某些参数点附近失去稳定性（例如，在[近不可压缩](@entry_id:752387)弹性问题中，泊松比趋近0.5时出现的[体积锁定](@entry_id:172606)），解[算子范数](@entry_id:752960)会“爆炸”，解流形的几何性质变差，线性降阶方法也会失效。

### [计算效率](@entry_id:270255)：离线-在线策略与[非线性](@entry_id:637147)瓶颈

降阶模型的最终目标是在所谓的**在线（online）**阶段实现快速计算，即为新的参数快速提供预测。为了达到这一目标，所有依赖于高维自由度 $n$ 的计算都必须在**离线（offline）**阶段完成。

#### [参数化](@entry_id:265163)问题的仿射分解

对于参数依赖的线性问题 $A(\boldsymbol{\mu})u(\boldsymbol{\mu}) = f(\boldsymbol{\mu})$，即使构建了[降阶模型](@entry_id:754172) $A_r(\boldsymbol{\mu})q(\boldsymbol{\mu}) = f_r(\boldsymbol{\mu})$，其中 $A_r(\boldsymbol{\mu}) = \boldsymbol{V}^{\top}A(\boldsymbol{\mu})\boldsymbol{V}$，在线阶段为每个新参数 $\boldsymbol{\mu}$ 组装高维矩阵 $A(\boldsymbol{\mu})$ 并进行投影的计算成本依然与 $n$ 相关，这违背了降阶的初衷。

解决方法是要求或构造算子的**[仿射参数](@entry_id:260625)依赖（affine parameter dependence）**。即，算子可以分解为参数相关标量函数与参数无关矩阵的乘[积之和](@entry_id:266697)：
$$
A(\boldsymbol{\mu}) = \sum_{q=1}^{Q_a} \Theta_q^a(\boldsymbol{\mu}) A_q, \quad f(\boldsymbol{\mu}) = \sum_{q=1}^{Q_f} \Theta_q^f(\boldsymbol{\mu}) f_q
$$
如果满足此结构，我们便可以实施高效的[离线-在线分解](@entry_id:177117)：
- **离线阶段**：计算并存储所有参数无关的降阶小矩阵和向量，如 $\boldsymbol{V}^{\top}A_q\boldsymbol{V}$ 和 $\boldsymbol{V}^{\top}f_q$。这部分计算昂贵，但只需执行一次。
- **在线阶段**：对于给定的新参数 $\boldsymbol{\mu}$，只需计算标量系数 $\Theta_q(\boldsymbol{\mu})$，然后对预计算好的小矩阵和向量进行线性组合，以极小的计算成本（仅与 $r$ 和 $Q$ 相关，与 $n$ 无关）组装并求解 $r \times r$ 的降阶系统。

这种仿射结构对于在线高效地计算**[后验误差估计](@entry_id:167288)（a posteriori error estimators）**也至关重要，从而为降阶模型的预测提供严格的置信界。

#### [非线性](@entry_id:637147)瓶颈与超降阶

对于[非线性](@entry_id:637147)问题，即使采用了 Galerkin 投影，我们仍然面临一个计算瓶颈。回顾降阶[内力](@entry_id:167605)项 $\boldsymbol{f}_{r, \mathrm{int}}(\boldsymbol{q}) = \boldsymbol{V}^{\top} \boldsymbol{f}_{\mathrm{int}}(\boldsymbol{V}\boldsymbol{q})$。在线评估此项需要以下步骤：
1.  **提升 (Lifting)**: 将降阶坐标 $\boldsymbol{q}$ 映射回高维空间：$\boldsymbol{u} = \boldsymbol{V}\boldsymbol{q}$。此步骤的计算成本为 $\mathcal{O}(nr)$。
2.  **评估 (Evaluation)**: 在高维空间中计算[非线性](@entry_id:637147)力 $\boldsymbol{f}_{\mathrm{int}}(\boldsymbol{u})$。成本至少为 $\mathcal{O}(n)$。
3.  **投影 (Projection)**: 将高维力[向量投影](@entry_id:147046)回降阶空间：$\boldsymbol{V}^{\top}\boldsymbol{f}_{\mathrm{int}}(\boldsymbol{u})$。成本为 $\mathcal O(nr)$。

总成本为 $\mathcal{O}(nr)$，它依然依赖于高维系统的规模 $n$。这个**[非线性](@entry_id:637147)瓶颈**使得标准的 Galerkin 投影在[非线性](@entry_id:637147)问题中无法实现真正的在线高效计算。

**超降阶 (Hyper-reduction)** 技术正是为了打破这一瓶颈而生。其核心思想是，不再精确计算[非线性](@entry_id:637147)项，而是用一个计算成本与 $n$ 无关的廉价代理来近似它。**[离散经验插值法](@entry_id:748503) (Discrete Empirical Interpolation Method, DEIM)** 是一种主流的超降阶方法。

DEIM 的工作原理如下：
1.  首先，假设[非线性](@entry_id:637147)力向量 $\boldsymbol{f}_{\mathrm{int}}(\boldsymbol{u})$ 本身也存在于一个低维子空间中，该子空间由一个“旁系”基底 $\boldsymbol{U} \in \mathbb{R}^{n \times m}$（其中 $m \ll n$）张成。这个基底可以通过对[非线性](@entry_id:637147)力的快照进行 POD 来获得。
2.  我们可以近似 $\boldsymbol{f}_{\mathrm{int}}(\boldsymbol{u}) \approx \boldsymbol{U}\boldsymbol{c}(t)$，其中 $\boldsymbol{c}(t) \in \mathbb{R}^{m}$ 是待定系数。
3.  DEIM 不通过投影来求解系数 $\boldsymbol{c}$，而是通过**插值**。它预先选择 $m$ 个“魔法”插值点（即状态向量的分量索引），并强制近似值在这些点上与真实值完全相等。
4.  这个插值条件导出一个 $m \times m$ 的小系统，求解得到系数 $\boldsymbol{c}$，从而得到[非线性](@entry_id:637147)项的近似。整个过程的在线计算成本仅依赖于 $m$ 和插值点的数量，与 $n$ 完全无关。

DEIM 的近似公式可以写作 $\boldsymbol{f}(\boldsymbol{u}) \approx \boldsymbol{U} (\boldsymbol{P}^{\top} \boldsymbol{U})^{-1} \boldsymbol{P}^{\top} \boldsymbol{f}(\boldsymbol{u})$，其中 $\boldsymbol{P}$ 是一个选择插值点的采样矩阵。这个公式的巧妙之处在于，在线计算时，我们只需要计算高维向量 $\boldsymbol{f}(\boldsymbol{u})$ 的 $m$ 个分量（由 $\boldsymbol{P}^{\top}$ 选择），而非整个向量。DEIM 是一个插值投影，当真实向量 $\boldsymbol{f}(\boldsymbol{u})$ 恰好位于基底 $\boldsymbol{U}$ 张成的子空间中时，DEIM 近似是精确的。

综上所述，通过组合使用投影（如Galerkin）、基底生成（如POD）以及针对[非线性](@entry_id:637147)和[参数化](@entry_id:265163)问题的先进策略（如仿射分解和DEIM），我们可以构建出既高效又可靠的[降阶模型](@entry_id:754172)。这些模型构成了连接第一性原理仿真与实时多查询应用（如设计、优化和控制）的重要桥梁。