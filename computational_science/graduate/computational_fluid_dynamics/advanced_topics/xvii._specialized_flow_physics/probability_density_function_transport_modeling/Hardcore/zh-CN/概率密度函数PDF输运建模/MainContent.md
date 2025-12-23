## 引言
在[湍流](@entry_id:151300)的复杂世界中，仅用平均值来描述流动现象往往是不够的，尤其是在涉及[化学反应](@entry_id:146973)或[多相流](@entry_id:146480)等[非线性](@entry_id:637147)过程时。[概率密度函数](@entry_id:140610)（PDF）输运建模提供了一个强大而全面的框架，它超越了传统的[雷诺平均](@entry_id:754341)方法，旨在捕捉流场中速度、标量浓度或温度等物理量的完整[统计分布](@entry_id:182030)。这种方法的核心优势在于能够精确处理平均[化学反应速率](@entry_id:147315)等难以封闭的项，从而为模拟[湍流燃烧](@entry_id:756233)等复杂现象提供了坚实的理论基础。

本文旨在系统性地介绍PDF输运建模的理论与实践。我们将深入探讨这一高级[计算流体动力学](@entry_id:147500)（CFD）工具，以弥合理论推导与工程应用之间的鸿沟。通过本文的学习，读者将全面了解PDF方法的核心思想、其在解决关键物理问题中的应用，以及相关的数值挑战。

文章结构如下：第一章“原理与机制”将奠定理论基础，详细阐述PDF的定义、其[输运方程](@entry_id:756133)的推导，并聚焦于[湍流输运](@entry_id:150198)和分子混合这两个核心闭合问题。第二章“应用与跨学科连接”将展示PDF方法在[湍流燃烧](@entry_id:756233)、涡量动力学和[数据同化](@entry_id:153547)等多个领域的实际应用，凸显其强大的问题解决能力和跨学科特性。最后，在第三章“动手实践”中，我们提供了一系列精心设计的问题，旨在帮助读者将理论知识转化为解决实际建模问题的能力。让我们从PDF方法的基本原理开始，踏上这段探索[湍流统计](@entry_id:200093)世界的旅程。

## 原理与机制

在对[湍流](@entry_id:151300)流动的统计描述中，我们不仅关心平均量，如平均速度或平均标量浓度，还关心这些量的波动和完整[分布](@entry_id:182848)。概率密度函数 (PDF) 方法为此提供了一个强大而全面的框架。通过直接对感兴趣的量（如速度和标量）的单点或多点联合 PDF 建模，我们可以绕过传统[矩方法](@entry_id:752140)中出现的许多闭合问题，同时获得更丰富的统计信息。本章旨在阐述 PDF 输运建[模的基](@entry_id:156416)本原理和核心机制，从 PDF 的基本定义开始，推导其[输运方程](@entry_id:756133)，并探讨为使该方程封闭而必须引入的关键建模概念。

### 基本定义：PDF方法的语言

掌握 PDF 方法的第一步是熟悉其基本词汇——各种形式的概率密度函数及其属性。这些定义是构建更复杂理论的基石。

#### 单点标量 PDF

考虑一个[湍流](@entry_id:151300)流场中的[被动标量](@entry_id:191726)场 $\phi(\mathbf{x}, t)$，例如[混合分数](@entry_id:752032)或污染物浓度。在任何给定的欧拉空间点 $\mathbf{x}$ 和时间 $t$，$\phi(\mathbf{x}, t)$ 的值由于[湍流](@entry_id:151300)的随机性而波动。为了描述这种波动，我们将 $\phi(\mathbf{x}, t)$ 视为一个[随机变量](@entry_id:195330)。其统计特性可以通过其 **单点标量概率密度函数 (one-point scalar PDF)** $f_\phi(\xi; \mathbf{x}, t)$ 来完全表征。

从数学上讲，$f_\phi(\xi; \mathbf{x}, t)$ 定义为在特定时空点 $(\mathbf{x}, t)$ [标量场](@entry_id:151443)取值为 $\xi$ 的概率密度。一个严谨且在理论上极其实用的定义是使用狄拉克 delta [分布](@entry_id:182848) $\delta(\cdot)$ 和系综平均 $\langle \cdot \rangle$ ：
$$
f_\phi(\xi; \mathbf{x}, t) = \langle \delta(\xi - \phi(\mathbf{x}, t)) \rangle
$$
这里，$\xi$ 是[样本空间](@entry_id:275301)中的一个确[定性变量](@entry_id:637195)，而 $\phi(\mathbf{x}, t)$ 是[随机变量](@entry_id:195330)。该定义的直观含义是，通过在大量独立的流动实现（系综）中进行平均，我们可以构建出在每个 $\xi$ 值附近的[概率密度](@entry_id:175496)。

根据概率的基本公理，$f_\phi$ 必须满足 **[归一化条件](@entry_id:156486)**，即其在整个样本空间上的积分必须为 1：
$$
\int_{-\infty}^{\infty} f_\phi(\xi; \mathbf{x}, t) \, \mathrm{d}\xi = \left\langle \int_{-\infty}^{\infty} \delta(\xi - \phi(\mathbf{x}, t)) \, \mathrm{d}\xi \right\rangle = \langle 1 \rangle = 1
$$
$f_\phi$ 的 **支撑集** (support) 是指标量 $\phi$ 可能取值的范围。例如，对于一个被归一化为 0 到 1 之间的[混合分数](@entry_id:752032)，$f_\phi(\xi; \mathbf{x}, t)$ 仅在 $\xi \in [0, 1]$ 上为非零。

拥有了 $f_\phi$，我们便可以计算任何关于 $\phi$ 的单点[统计矩](@entry_id:268545)。例如，[雷诺平均](@entry_id:754341)值（一阶矩）和[方差](@entry_id:200758)（[二阶中心矩](@entry_id:200758)）分别为：
$$
\langle \phi(\mathbf{x}, t) \rangle = \int_{-\infty}^{\infty} \xi \, f_\phi(\xi; \mathbf{x}, t) \, \mathrm{d}\xi
$$
$$
\langle (\phi'(\mathbf{x}, t))^2 \rangle = \int_{-\infty}^{\infty} (\xi - \langle \phi \rangle)^2 \, f_\phi(\xi; \mathbf{x}, t) \, \mathrm{d}\xi
$$
其中 $\phi' = \phi - \langle \phi \rangle$ 是标量脉动。

值得强调的是，理论上的 PDF $f_\phi$ 与实验或数值模拟中获得的有限样本近似值有所区别 。例如，一个由 $N$ 个独立实现构建的 **[直方图](@entry_id:178776)**，在样本数 $N \to \infty$ 和箱宽 $\Delta\xi \to 0$ 的极限下，并经过箱宽的适当归一化后，才能收敛到 $f_\phi$。同样，对于一个统计定常的流动，在单个实现中进行[时间平均](@entry_id:267915)得到的频率计数，只有在满足 **[遍历性假设](@entry_id:147104)** (ergodic hypothesis) 的情况下，才能在时间趋于无穷时收敛到系综平均的 PDF。对于非定常或非遍历的系统，这两种平均是不等价的。

#### 多点和联合 PDF

单点 PDF 提供了在单一位置的完整统计信息，但它无法描述不同空间点之间的关联，也无法描述不同物理量（如速度和标量）之间的耦合。为此，我们需要引入多点和联合 PDF。

**两点联合 PDF** $f_{\phi_1, \phi_2}(\xi_1, \xi_2; \mathbf{x}_1, \mathbf{x}_2, t)$ 描述了在同一时间 $t$，在两个不同空间点 $\mathbf{x}_1$ 和 $\mathbf{x}_2$ 的标量值分别为 $\xi_1$ 和 $\xi_2$ 的[联合概率](@entry_id:266356)密度 。其定义为：
$$
f_{\phi_1, \phi_2}(\xi_1, \xi_2; \mathbf{x}_1, \mathbf{x}_2, t) = \langle \delta(\xi_1 - \phi(\mathbf{x}_1, t)) \, \delta(\xi_2 - \phi(\mathbf{x}_2, t)) \rangle
$$
两点 PDF 包含了关于流场空间结构的重要信息。例如，**[两点相关函数](@entry_id:185074)** $R_{\phi\phi}(\mathbf{x}_1, \mathbf{x}_2, t) = \langle \phi(\mathbf{x}_1, t) \phi(\mathbf{x}_2, t) \rangle$ 就可以通过对两点 PDF积分得到：
$$
R_{\phi\phi}(\mathbf{x}_1, \mathbf{x}_2, t) = \int_{-\infty}^{\infty} \int_{-\infty}^{\infty} \xi_1 \xi_2 \, f_{\phi_1, \phi_2}(\xi_1, \xi_2; \mathbf{x}_1, \mathbf{x}_2, t) \, \mathrm{d}\xi_1 \mathrm{d}\xi_2
$$
只有当两个点的标量在统计上是独立的，两点 PDF 才能分解为两个单点 PDF 的乘积：$f_{\phi_1, \phi_2} = f_\phi(\xi_1; \mathbf{x}_1, t) f_\phi(\xi_2; \mathbf{x}_2, t)$。在[湍流](@entry_id:151300)中，当两点间距 $|\mathbf{x}_1 - \mathbf{x}_2|$ 远大于[湍流](@entry_id:151300)积分尺度时，这种独立性才近似成立。

类似地，为了描述[湍流输运](@entry_id:150198)（即速度场与标量场的耦合），我们定义 **速度-标量联合 PDF** $f_{\mathbf{u}, \phi}(\mathbf{v}, \xi; \mathbf{x}, t)$，它表示在 $(\mathbf{x}, t)$ 处，速度为 $\mathbf{v}$ 且标量为 $\xi$ 的[联合概率](@entry_id:266356)密度 ：
$$
f_{\mathbf{u}, \phi}(\mathbf{v}, \xi; \mathbf{x}, t) = \langle \delta(\mathbf{v} - \mathbf{u}(\mathbf{x}, t)) \, \delta(\xi - \phi(\mathbf{x}, t)) \rangle
$$
这里 $\delta(\mathbf{v} - \mathbf{u})$ 是三维狄拉克 delta 函数。通过对联合 PDF 在一个变量的[样本空间](@entry_id:275301)上进行积分，我们可以得到另一个变量的 **边缘 PDF** (marginal PDF)。例如，对所有可能的速度值积分，可以恢复单点标量 PDF：
$$
f_\phi(\xi; \mathbf{x}, t) = \int_{\mathbb{R}^3} f_{\mathbf{u}, \phi}(\mathbf{v}, \xi; \mathbf{x}, t) \, \mathrm{d}\mathbf{v}
$$

#### [可压缩流](@entry_id:747589)中的 Favre 平均 PDF

在密度 $\rho$ 显著变化的 **可压缩流** 或 **[变密度流](@entry_id:756427)**（如燃烧）中，直接使用上述基于体积的[雷诺平均](@entry_id:754341)会使控制方程变得异常复杂。为了简化方程形式，引入 **Favre 平均** (或质量加权平均) 是非常有用的。一个量 $\psi$ 的 Favre 平均定义为 $\tilde{\psi} = \langle \rho \psi \rangle / \langle \rho \rangle$。

与此对应，我们定义 **密度加权 PDF** (或 Favre PDF) $\tilde{f}_\phi(\xi; \mathbf{x}, t)$ ：
$$
\tilde{f}_\phi(\xi; \mathbf{x}, t) = \frac{\langle \rho(\mathbf{x}, t) \delta(\xi - \phi(\mathbf{x}, t)) \rangle}{\langle \rho(\mathbf{x}, t) \rangle}
$$
Favre PDF 同样满足[归一化条件](@entry_id:156486) $\int \tilde{f}_\phi \, \mathrm{d}\xi = 1$ 。使用 Favre PDF，我们可以方便地计算任何标量函数 $g(\phi)$ 的 Favre 平均值 ：
$$
\tilde{g(\phi)} = \int_{-\infty}^{\infty} g(\xi) \, \tilde{f}_\phi(\xi; \mathbf{x}, t) \, \mathrm{d}\xi
$$
Favre 平均值 $\tilde{\phi}$ 和[雷诺平均](@entry_id:754341)值 $\langle \phi \rangle$ 之间的差异由密度和标量的协[方差](@entry_id:200758)决定 ：
$$
\tilde{\phi} - \langle \phi \rangle = \frac{\langle \rho \phi \rangle - \langle \rho \rangle \langle \phi \rangle}{\langle \rho \rangle} = \frac{\langle \rho' \phi' \rangle}{\langle \rho \rangle}
$$
其中 $\rho' = \rho - \langle \rho \rangle$ 是密度脉动。类似地，**Favre 脉动** 定义为 $\phi'' = \phi - \tilde{\phi}$。一个重要的性质是，其质量加权平均为零，即 $\langle \rho \phi'' \rangle = 0$，但其常规的[雷诺平均](@entry_id:754341) $\langle \phi'' \rangle$ 通常不为零 。这些区别在推导和解释可压缩[湍流](@entry_id:151300)的模型方程时至关重要。

### PDF 输运方程：一个统计[守恒定律](@entry_id:269268)

PDF 方法的核心优势在于，我们可以为 PDF 本身推导出精确的输运方程。这个方程描述了 PDF 在相空间（由物理空间坐标和样本空间坐标组成）中的演化。然而，正如我们将看到的，这个“精确”的方程包含一些无法仅从 PDF 本身求解的项，这便是 **闭合问题** (closure problem) 的根源。

#### 推导与未闭合项

让我们考虑一个由不可压缩[速度场](@entry_id:271461) $\mathbf{u}$ [平流](@entry_id:270026)并以[分子扩散](@entry_id:154595)率 $D$ [扩散](@entry_id:141445)的[被动标量](@entry_id:191726) $\phi$。其守恒方程为：
$$
\frac{\partial \phi}{\partial t} + \mathbf{u} \cdot \nabla \phi = D \nabla^2 \phi + S(\phi)
$$
其中 $S(\phi)$ 是[源项](@entry_id:269111)。通过对 $f_\phi(\xi; \mathbf{x}, t) = \langle \delta(\xi - \phi) \rangle$ 的定义应用时间导数和链式法则，可以推导出 $f_\phi$ 的[输运方程](@entry_id:756133)。最终得到的精确形式为：
$$
\frac{\partial f_\phi}{\partial t} + \nabla \cdot (\langle \mathbf{u} \rangle f_\phi) = -\nabla \cdot \langle \mathbf{u}' \delta(\xi - \phi) \rangle - \frac{\partial}{\partial \xi} [S(\xi) f_\phi] - \frac{\partial}{\partial \xi} \langle (D \nabla^2 \phi) \delta(\xi - \phi) \rangle
$$
为了更清晰地理解未闭合项，我们可以引入 **条件平均** (conditional average) 的概念。对于任意量 $A$，其在 $\phi = \xi$ 条件下的平均值记为 $\langle A | \phi=\xi \rangle$。利用关系式 $\langle A \delta(\xi - \phi) \rangle = \langle A | \phi=\xi \rangle f_\phi(\xi)$，上述方程可以重写为：
$$
\frac{\partial f_\phi}{\partial t} + \underbrace{\nabla \cdot (\langle \mathbf{u} | \phi=\xi \rangle f_\phi)}_{\text{物理空间输运}} = \underbrace{-\frac{\partial}{\partial \xi} [S(\xi) f_\phi]}_{\text{反应源项}} \underbrace{- \frac{\partial}{\partial \xi} [D \langle \nabla^2 \phi | \phi=\xi \rangle f_\phi]}_{\text{组分空间输运 (分子混合)}}
$$
这个方程形式优美，清晰地展示了 PDF 在相空间中的守恒。左侧是 PDF 在物理空间中的[对流](@entry_id:141806)项，而右侧则表示 PDF 在组分空间 $\xi$ 中的“流动”。源项 $S(\xi)f_\phi$ 是一个闭合项，因为它只依赖于 $\xi$ 和 $f_\phi$。然而，方程中还有两个关键的未闭合项，它们代表了[湍流输运](@entry_id:150198)和分子混合的平均效应。

**物理空间输运**：第一项 $\nabla \cdot (\langle \mathbf{u} | \phi=\xi \rangle f_\phi)$ 描述了 PDF 在物理空间中的输运。其中，**条件速度** $\langle \mathbf{u} | \phi=\xi \rangle$ 是未知的 。它表示携带标量值为 $\xi$ 的流体微团的平均速度。我们可以将其分解为平均速度和脉动速度的贡献：$\langle \mathbf{u} | \phi=\xi \rangle = \langle \mathbf{u} \rangle + \langle \mathbf{u}' | \phi=\xi \rangle$。输运项因此变为 $\nabla \cdot (\langle \mathbf{u} \rangle f_\phi) + \nabla \cdot (\langle \mathbf{u}' | \phi=\xi \rangle f_\phi)$。第一部分是已知的[平均速度](@entry_id:267649)平流，而第二部分则代表由[湍流](@entry_id:151300)脉动引起的 **[湍流](@entry_id:151300)[扩散](@entry_id:141445)**，其核心是未知的条件速度脉动 $\langle \mathbf{u}' | \phi=\xi \rangle$。

**组分空间输运 (分子混合)**：最后一项 $- \frac{\partial}{\partial \xi} [D \langle \nabla^2 \phi | \phi=\xi \rangle f_\phi]$ 描述了[分子扩散](@entry_id:154595)如何改变标量值的[分布](@entry_id:182848)，即 **分子混合** 或 **[微观混合](@entry_id:751971)** (micromixing)。这一项在组分空间 $\xi$ 中具有通量的形式，其驱动力是 **条件拉普拉斯** $\langle \nabla^2 \phi | \phi=\xi \rangle$ 。这个量代表了在标量[等值面](@entry_id:196027) $\phi=\xi$ 上的[平均曲率](@entry_id:162147)。直观上，[局部极大值](@entry_id:137813)点（曲率为负）的标量会因[扩散](@entry_id:141445)而降低，而局部极小值点（曲率为正）的标量会升高，从而导致 PDF 向中间值收缩。条件拉普拉斯包含了关于[标量场](@entry_id:151443)空间梯度的信息，而这些信息无法从单点 PDF $f_\phi$ 中获得，因此该项是未闭合的。这是 PDF 方法中最核心的闭合挑战 。

### 闭合模型：弥合差距

为了使 PDF 输运方程成为一个可解的系统，我们必须为未闭合的[湍流输运](@entry_id:150198)项和分子混合项引入模型，即 **闭合模型** (closure models)。

#### [湍流输运](@entry_id:150198)的闭合：梯度[扩散](@entry_id:141445)假设

对于物理空间中的[湍流输运](@entry_id:150198)项 $\nabla \cdot (\langle \mathbf{u}' | \phi=\xi \rangle f_\phi)$，最常用的闭合方法是 **广义梯度[扩散](@entry_id:141445)假设** (Generalized Gradient Diffusion Hypothesis, GGDH)。该模型假设[湍流](@entry_id:151300)通量与被输运量（此处为 $f_\phi$）的梯度成正比 ：
$$
\langle \mathbf{u}' | \phi=\xi \rangle f_\phi \approx - \mathbf{D}_t \cdot \nabla f_\phi(\xi; \mathbf{x}, t)
$$
其中 $\mathbf{D}_t$ 是[湍流扩散系数](@entry_id:196515)张量，通常通过涡粘模型（如 $k-\varepsilon$ 模型）来确定。这个模型将[湍流](@entry_id:151300)对 PDF 的输运效应模拟为一种类似于[分子扩散](@entry_id:154595)的 Fickian 扩散过程。代入此模型后，完整的物理空间输运项变为：
$$
\nabla \cdot (\langle \mathbf{u} \rangle f_\phi - \mathbf{D}_t \cdot \nabla f_\phi)
$$
这一项现在只依赖于[平均速度](@entry_id:267649)场、[湍流扩散系数](@entry_id:196515)和 PDF 本身，因此是闭合的。

#### 分子混合的闭合：[微观混合](@entry_id:751971)模型

分子混合项的闭合是 PDF 建模中最具挑战性也最丰富多彩的领域。这些 **[微观混合](@entry_id:751971)模型** 旨在描述在一个拉格朗日流体微团上，标量值因[分子扩散](@entry_id:154595)而如何随时间变化。

一个基础且广泛应用的[微观混合](@entry_id:751971)模型是 **与平均值相互作用交换模型** (Interaction by Exchange with the Mean, IEM)。该模型假设一个流体微团上的标量 $\phi$ 会以一定的速率向其周围的平均标量值 $\tilde{\phi}$ 松弛 ：
$$
\frac{d\phi}{dt} = -\chi (\phi - \tilde{\phi})
$$
这里的 $\tilde{\phi}$ 在常密度流中是[雷诺平均](@entry_id:754341) $\langle \phi \rangle$，而在[变密度流](@entry_id:756427)中必须是 Favre 平均 $\tilde{\phi}$ 以保证质量守恒 。参数 $\chi$ 是 **混合频率**，单位为 $\mathrm{s}^{-1}$，其倒数 $\tau_\phi = 1/\chi$ 代表了[微观混合](@entry_id:751971)的时间尺度。混合频率通常与[湍流](@entry_id:151300)宏观时间尺度关联，一个常见的模型是 $\chi = C_\phi \frac{\varepsilon}{k}$，其中 $k$ 和 $\varepsilon$ 分别是[湍流](@entry_id:151300)能和[湍流耗散率](@entry_id:756234)，$C_\phi$ 是一个模型常数 。

IEM 模型的一个重要特性是 **[可实现性](@entry_id:193701)** (realizability)。对于一个有界标量（如 $0 \le \phi \le 1$），该模型保证标量值永远不会超出其物理边界，因为其解是初始值和平均值之间的一个[凸组合](@entry_id:635830) 。将 IEM 模型代入 PDF 方程的分子混合项，会得到一个在组分空间中的[对流-扩散](@entry_id:148742)形式的闭合项，驱动 PDF 向平均值收缩。

#### 对 LES 的扩展：过滤密度函数 (FDF)

PDF 方法的概念可以从[雷诺平均](@entry_id:754341)模拟 (RANS) 框架自然地扩展到[大涡模拟 (LES)](@entry_id:751142) 框架。在 LES 中，我们使用[空间滤波](@entry_id:202429)器而不是系综平均。相应的统计工具是 **过滤密度函数** (Filtered Density Function, FDF)，定义为 $\tilde{P}_\phi(\xi; \mathbf{x}, t) = \langle \delta(\xi - \phi(\mathbf{x}, t)) \rangle_\Delta$，其中 $\langle \cdot \rangle_\Delta$ 表示[空间滤波](@entry_id:202429)操作 。

FDF 的[输运方程](@entry_id:756133)与 PDF 方程非常相似，但其中的未闭合项代表了 **亚格子尺度 (SFS)** 的效应。具体来说，存在未闭合的 SFS [对流输运](@entry_id:149512)项和 SFS 分子混合项。SFS 分子混合项同样需要一个[微观混合](@entry_id:751971)模型来闭合，例如 IEM 模型。在这种情况下，[混合时间](@entry_id:262374)尺度 $T_m$ 应该与亚格子尺度相关，一个基于物理的尺度分析表明 $T_m \propto \Delta^{2/3}\varepsilon^{-1/3}$，其中 $\Delta$ 是滤波器宽度 。

### 速度-组分 PDF 建模中的高等课题

当我们的目标是模拟速度和组分的联合 PDF 时，模型的复杂性和微妙之处进一步增加。这需要[对流](@entry_id:141806)体微团的速度演化本身进行建模，并确保模型满足基本的物理原理。

#### 速度的[朗之万模型](@entry_id:195161)

在速度-组分联合 PDF 的拉格朗日蒙特卡洛方法中，流体微团的速度演化通常由一个 **广义[朗之万模型](@entry_id:195161)** (generalized Langevin model) 描述。这是一个[随机微分方程](@entry_id:146618) (SDE)，其一般形式为：
$$
d\mathbf{u} = \mathbf{a}(\mathbf{u}, \phi, \langle \mathbf{u} \rangle, \dots) \, dt + \mathbf{B}(\mathbf{u}, \phi, \langle \mathbf{u} \rangle, \dots) \, d\mathbf{W}
$$
其中 $\mathbf{a}$ 是 **漂移向量**，代表确定性效应（如平均压力梯度、粘性阻力），$\mathbf{B}$ 是 **[扩散张量](@entry_id:748421)**，代表由[湍流](@entry_id:151300)脉动压力和[粘性应力](@entry_id:261328)引起的随机加速，而 $d\mathbf{W}$ 是一个维纳过程的增量。

#### 伽利略不变性

一个基本的物理原理是 **伽利略不变性** (Galilean invariance)，即物理定律在所有匀速运动的惯性参考系中都应具有相同的形式。这意味着[朗之万模型](@entry_id:195161)必须被精心构建以满足这一约束 。具体而言，对于一个从速度为 $\mathbf{u}$、[平均速度](@entry_id:267649)为 $\langle \mathbf{u} \rangle$ 的[参考系](@entry_id:169232)，转到一个以恒定速度 $\mathbf{V}$ 运动的新[参考系](@entry_id:169232)（其中速度为 $\mathbf{u}' = \mathbf{u} - \mathbf{V}$，[平均速度](@entry_id:267649)为 $\langle \mathbf{u} \rangle' = \langle \mathbf{u} \rangle - \mathbf{V}$），[朗之万模型](@entry_id:195161)的漂移项 $\mathbf{a}$ 和[扩散](@entry_id:141445)项 $\mathbf{B}$ 的函数形式必须保持不变。

这一要求意味着 $\mathbf{a}$ 和 $\mathbf{B}$ 必须仅仅是 **[相对速度](@entry_id:178060)** $\mathbf{u} - \langle \mathbf{u} \rangle$ 的函数，而不是 $\mathbf{u}$ 和 $\langle \mathbf{u} \rangle$ 的独立函数 。例如，一个漂移模型形如 $\mathbf{a} = -G(\mathbf{u} - \langle \mathbf{u} \rangle)$ 是伽利略不变的，而形如 $\mathbf{a} = -G\mathbf{u} + \alpha \langle \mathbf{u} \rangle$ 的模型（除非 $\alpha$ 和 $G$ 有特殊关系）则不是。同样，如果[扩散](@entry_id:141445)项依赖于速度大小，它必须依赖于[相对速度](@entry_id:178060)的大小 $\|\mathbf{u} - \langle \mathbf{u} \rangle\|$ 而不是绝对速度的大小 $\|\mathbf{u}\|$。不满足伽利略[不变性](@entry_id:140168)的模型是物理上不自洽的。

#### [随机微积分](@entry_id:143864)：Itô 与 Stratonovich

当[朗之万模型](@entry_id:195161)中的[扩散](@entry_id:141445)项 $\mathbf{B}$ 依赖于[状态变量](@entry_id:138790)（如速度 $\mathbf{u}$）本身时，这种情况称为 **[乘性噪声](@entry_id:261463)** (multiplicative noise)。此时，[随机微分方程](@entry_id:146618)的数学解释变得至关重要，主要有两种解释：**Itô 积分** 和 **Stratonovich 积分** 。

- **Stratonovich 解释** 通常与物理推导更相符，因为它遵循经典的[链式法则](@entry_id:190743)，并且在数值上对应于中点差分格式。
- **Itô 解释** 在数学上更便于处理，因为它与[鞅](@entry_id:267779)理论有直接联系，并且其对应的福克-普朗克方程（即 PDF [输运方程](@entry_id:756133)）形式更简单。

一个 Stratonovich 形式的 SDE 可以被精确地转换为一个等价的 Itô 形式的 SDE。在这个转换过程中，Itô 形式的漂移项会比 Stratonovich 形式多出一个额外的项，这个项被称为 **“伪漂移”** (spurious drift) 或 Itô 修正项。对于[朗之万模型](@entry_id:195161)，这个修正项的形式为 $\Delta A_i = \frac{1}{2} \sum_{j,k} B_{kj} \frac{\partial B_{ij}}{\partial u_k}$ 。

忽略这个修正在建模中是一个常见的错误。它会导致模型在数学上不自洽。例如，在推导[雷诺应力输运方程](@entry_id:754345)时，这个伪漂移项对压力-应变相关项和耗散项有直接的贡献。如果忽略它，所得到的[雷诺应力](@entry_id:263788)收支方程将是不正确的，可能导致模型预测出现非物理行为或数值不稳定性 。因此，正确处理 Itô-Stratonovich 转换是构建和实现可靠的速度-组分联合 PDF 模型的关键一步。