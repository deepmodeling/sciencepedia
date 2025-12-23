## 引言
黏塑性是描述材料在加载下表现出时间相关和率相关行为的力学分支，对于理解和预测材料在高温或高[应变率](@entry_id:154778)等极端工况下的性能至关重要。传统的率无关塑性理论虽然成功描述了材料的永久变形，但无法捕捉到如蠕变（恒定应力下的持续变形）和[应力松弛](@entry_id:159905)（恒定应变下的应力衰减）等关键现象。这一知识鸿沟催生了更为普适的理论框架，其中Perzyna和Duvaut-Lions提出的模型堪称两大基石。

本文旨在深入剖析这两种开创性的黏塑性模型。我们将从第一章“原理与机制”开始，系统阐述其核心思想：[Perzyna模型](@entry_id:753365)基于“过应力”概念，将黏塑性流动直接与应力超出[屈服面](@entry_id:175331)的程度联系起来；而[Duvaut-Lions模型](@entry_id:748713)则从几何角度出发，将其视为应力向弹性许可域的“松弛投影”。随后的“应用与跨学科联系”章节将展示这些理论如何应用于解释材料的宏观行为、解决复杂的工程问题，并与其他学科（如地球力学和[热力学](@entry_id:141121)）[交叉](@entry_id:147634)融合。最后，在“动手实践”部分，我们将引导读者完成从理论到实践的关键一步，学习如何通过[数值算法](@entry_id:752770)将这些模型付诸于[计算模拟](@entry_id:146373)。通过这一结构化的学习路径，读者将能够全面掌握黏塑性理论的精髓及其在现代[计算固体力学](@entry_id:169583)中的强大应用。

## 原理与机制

黏塑性理论将率无关塑性理论的框架进行了扩展，以考虑许多材料中观察到的时间相关和率相关行为，尤其是在高温或高应变率条件下。本章旨在阐明两类开创性黏塑性模型的指导性基本原理：由Perzyna首创的过应力模型和由Duvaut与Lions发展的松弛模型。我们将探讨过应力的核心概念、[流动法则](@entry_id:177163)的数学公式、塑性势的关键作用，以及这些选择对[热力学一致性](@entry_id:138886)和计算实现所产生的深远影响。

### 过应力的概念

在率无关塑性理论中，材料的应力状态被严格限制在[应力空间](@entry_id:199156)中一个凸弹性域的内部或其边界上。该域由一个**[屈服函数](@entry_id:167970)** $f(\boldsymbol{\sigma}, \boldsymbol{\alpha}) \le 0$ 定义，其中 $\boldsymbol{\sigma}$ 是柯西应力张量，$\boldsymbol{\alpha}$ 代表一组描述材料状态（例如[硬化](@entry_id:177483)）的内变量。该域的边界 $f(\boldsymbol{\sigma}, \boldsymbol{\alpha}) = 0$ 被称为**屈服面**。任何满足 $f(\boldsymbol{\sigma}, \boldsymbol{\alpha}) > 0$ 的应力状态都是不被允许的。

率相关塑性理论，或称黏塑性理论，放宽了这一约束。它允许应力状态暂时存在于[屈服面](@entry_id:175331)之外。应力超出此边界的程度由**过应力**来量化。对于给定的[屈服函数](@entry_id:167970) $f$，当其值为正时，函数值本身可作为过应力的一个自然标量度量。也就是说，过应力标量 $s$ 可以定义为 $s = f(\boldsymbol{\sigma}, \boldsymbol{\alpha})$。当应力状态位于弹性域内或其边界上时，$s \le 0$，表示没有过应力。当应力状态移动到[屈服面](@entry_id:175331)之外时，$s > 0$，这个正值就量化了过应力的大小 。

黏塑性模型的一个基石是，黏塑性流动——材料不可逆的、时间相关的变形——是由这种过应力驱动的。因此，黏塑性变形只应在过应力为正时发生。为了在数学上强制执行这一条件，我们采用**麦考利括号**（或正部算子），对于任何标量 $x$，其定义为 $\langle x \rangle = \max(x, 0)$。通过将此算子应用于过应力标量，即 $\langle s \rangle = \langle f(\boldsymbol{\sigma}, \boldsymbol{\alpha}) \rangle$，我们得到一个量，对于任何弹性许可的应力状态（$f \le 0$），该量为零；对于任何不许可的状态（$f > 0$），该量等于过应力本身。因此，麦考利括号作为一个优雅而有效的数学“开关”，仅在应力超过屈服面时才激活黏[塑性流动](@entry_id:201346) 。值得注意的是，麦考利括号函数在零点是[连续但不可微](@entry_id:261860)的，这在塑性流动开始时引入了一个“扭折”，这一特性对材料响应的[光滑性](@entry_id:634843)有影响。

### [Perzyna过应力模型](@entry_id:165503)

[Perzyna模型](@entry_id:753365)提供了一种黏[塑性流动](@entry_id:201346)速率与过应力之间的直接唯象关系。黏塑性[应变张量](@entry_id:193332)的演化，$\dot{\boldsymbol{\varepsilon}}^{vp}$，由以下形式的[流动法则](@entry_id:177163)给出：

$$
\dot{\boldsymbol{\varepsilon}}^{vp} = \gamma \, \frac{\partial g}{\partial \boldsymbol{\sigma}}
$$

这里，$g(\boldsymbol{\sigma}, \boldsymbol{\alpha})$ 是一个称为**塑性势**的标量函数，其对应力的梯度 $\partial g / \partial \boldsymbol{\sigma}$ 定义了应变空间中黏塑性流动的方向。标量 $\gamma \ge 0$ 是**黏塑性乘子**，它决定了流动速率的大小。在Perzyna框架中，$\gamma$ 被假定为过应力的函数：

$$
\gamma = \phi(\langle f(\boldsymbol{\sigma}, \boldsymbol{\alpha}) \rangle)
$$

函数 $\phi(\cdot)$ 通常被称为**黏度函数**或流动函数，它是一个单调递增的本构函数，且满足 $\phi(0)=0$。它决定了材料的率敏感性——黏塑性[应变率](@entry_id:154778)随过应力增加的快慢。该函数的两种常见形式是[幂律](@entry_id:143404)和指数律 。

**[幂律](@entry_id:143404)**公式被广泛使用：
$$
\phi(s) = \frac{1}{\eta} s^{n}
$$
其中 $s = \langle f \rangle$ 是过应力。参数 $\eta$ 是一个**黏度系数**，$n \ge 1$ 是**率敏感性指数**。为了[量纲一致性](@entry_id:271193)，如果过应力 $s$ 的单位是应力（例如帕斯卡），[应变率](@entry_id:154778)的单位是时间的倒数（$\mathrm{s}^{-1}$），那么 $\eta$ 的单位必须是 $\text{应力}^n \times \text{时间}$（例如 $\mathrm{Pa}^n \cdot \mathrm{s}$）。

另一种选择是**指数律**：
$$
\phi(s) = \gamma_{0} \left( \exp\left(\frac{s}{s_0}\right) - 1 \right)
$$
这里，$\gamma_{0}$ 是一个参考[应变率](@entry_id:154778)（单位为 $\mathrm{s}^{-1}$），$s_0$ 是一个归一化过应力的特征应力。与纯[幂律](@entry_id:143404)不同，这种形式引入了一个**内在应力尺度** $s_0$，这使得材料响应的标定更具灵活性，特别是对于较小的过应力值 。

黏度函数的选择具有重要意义。对于小过应力（$s \to 0^+$），指数律呈线性行为（$\phi(s) \propto s$），与 $n=1$ 时的[幂律](@entry_id:143404)相同。对于 $n>1$，[幂律](@entry_id:143404)表现出较慢的[非线性激活](@entry_id:635291)。对于大过应力（$s \to \infty$），指数律预测的流动速率增长远快于任何[幂律](@entry_id:143404)，反映了其快于多项式的增长特性 。

[Perzyna模型](@entry_id:753365)优雅地弥合了纯弹性行为和率无关塑性行为之间的差距。在黏度无限大（$\eta \to \infty$）的极限情况下，黏塑性乘子 $\gamma$ 趋近于零，材料表现为弹性。相反，在黏度为零（$\eta \to 0$）的极限情况下，对于任何非零过应力，黏塑性流动速率变得无限大。为了保持有限的应变率，过应力必须被驱动至零，这意味着应力状态被强制返回到[屈服面](@entry_id:175331)上。这就恢复了率无关塑性理论的[一致性条件](@entry_id:637057) $f(\boldsymbol{\sigma}, \boldsymbol{\alpha})=0$ 。

### Duvaut-Lions松弛模型

[Duvaut-Lions模型](@entry_id:748713)提供了一个不同但相关的黏塑性视角。它不是基于过应力值来假定一个[流动法则](@entry_id:177163)，而是将黏塑性构建为一个[应力松弛](@entry_id:159905)过程。其中心思想是，当应力状态 $\boldsymbol{\sigma}$ 位于容许的弹性域 $K(\boldsymbol{\alpha})$ 之外时，它会在一个[特征时间](@entry_id:173472)内松弛回该域。

这种松弛的驱动力是当前应力 $\boldsymbol{\sigma}$ 与其在凸弹性集 $K$ 上的**度量投影** $\bar{\boldsymbol{\sigma}} = \Pi_{K}(\boldsymbol{\sigma})$ 之间的差值。投影点 $\bar{\boldsymbol{\sigma}}$ 是集合 $K$ 中在特定度量下距离 $\boldsymbol{\sigma}$ 最近的唯一一点。对于具有[刚度张量](@entry_id:176588) $\mathbb{C}$ 的[线性弹性](@entry_id:166983)材料，该度量由[弹性势能](@entry_id:168893)自然定义，对应于由柔度张量 $\mathbb{C}^{-1}$ 导出的范数。

由黏塑性流动引起的应力变化率被视为与“应力误差”向量 $(\boldsymbol{\sigma} - \bar{\boldsymbol{\sigma}})$ 成正比：
$$
\dot{\boldsymbol{\sigma}}_{vp} = -\mathbb{C} : \dot{\boldsymbol{\varepsilon}}^{vp} = -\frac{1}{\eta} (\boldsymbol{\sigma} - \bar{\boldsymbol{\sigma}})
$$
其中 $\eta$ 是一个特征松弛时间（单位为时间）。这直接导出了Duvaut-Lions流动法则：
$$
\dot{\boldsymbol{\varepsilon}}^{vp} = \frac{1}{\eta} \mathbb{C}^{-1} : (\boldsymbol{\sigma} - \bar{\boldsymbol{\sigma}})
$$
[投影算子](@entry_id:154142)的一个关键特性是，如果应力已在容许集内（$\boldsymbol{\sigma} \in K$），那么它就是自身的投影（$\bar{\boldsymbol{\sigma}} = \boldsymbol{\sigma}$）。在这种情况下，应力差为零，不发生黏[塑性流动](@entry_id:201346)。这提供了一种隐式的开关机制，功能上等同于[Perzyna模型](@entry_id:753365)中使用的显式麦考利括号 。

一个非凡的见解是，在某些重要情况下，[Duvaut-Lions模型](@entry_id:748713)在数学上等价于线性的[Perzyna模型](@entry_id:753365)。考虑一个基于[von Mises屈服准则](@entry_id:174339) $f(\boldsymbol{\sigma}) = \|\mathbf{s}\| - \sigma_y$ 的关联模型，其中 $\mathbf{s}$ 是[偏应力](@entry_id:163323)，$\sigma_y$ 是[屈服应力](@entry_id:274513)。如果应力在[屈服面](@entry_id:175331)之外（$\|\mathbf{s}\| > \sigma_y$），投影点 $\bar{\boldsymbol{\sigma}}$ 的静水压力部分与 $\boldsymbol{\sigma}$ 相同，但其偏应力部分被径向缩回以落在屈服柱面上。应力差变为纯偏量：
$$
\boldsymbol{\sigma} - \bar{\boldsymbol{\sigma}} = \left( \|\mathbf{s}\| - \sigma_y \right) \frac{\mathbf{s}}{\|\mathbf{s}\|} = \langle f(\boldsymbol{\sigma}) \rangle \frac{\partial f}{\partial \boldsymbol{\sigma}}
$$
将此代入Duvaut-Lions[流动法则](@entry_id:177163)，并注意到对于各向同性材料，柔度张量作用于[偏应力张量](@entry_id:267642)的形式为 $\mathbb{C}^{-1}:\mathbf{s} = \frac{1}{2G}\mathbf{s}$（其中 $G$ 是[剪切模量](@entry_id:167228)），我们得到：
$$
\dot{\boldsymbol{\varepsilon}}^{vp} = \frac{1}{\eta} \frac{1}{2G} \langle f(\boldsymbol{\sigma}) \rangle \frac{\partial f}{\partial \boldsymbol{\sigma}}
$$
这正是一个线性的[Perzyna模型](@entry_id:753365)（$\phi(s)=s/\mu_{\text{eff}}$），其有效黏度为 $\mu_{\text{eff}} = 2G\eta$ 。这种等价性展示了唯象的Perzyna公式与几何上直观的Duvaut-Lions松弛概念之间的深刻联系 。

### 流动方向：关联性及其后果

黏塑性应变率张量 $\dot{\boldsymbol{\varepsilon}}^{vp}$ 的方向由塑性[势的梯度](@entry_id:268447) $\boldsymbol{m} = \partial g / \partial \boldsymbol{\sigma}$ 决定。塑性[势函数](@entry_id:176105) $g$ 相对于[屈服函数](@entry_id:167970) $f$ 的选择至关重要。

如果塑性势选择为与[屈服函数](@entry_id:167970)相同（$g=f$），则流动被称为**关联**流动。在这种情况下，黏塑性流动发生在屈服面外法线的方向上。这是最常见的假设，因为它可以从适用于广泛材料的热力学稳定性原理推导出来。

然而，对于某些材料，特别是如土壤和岩石等[地质材料](@entry_id:749838)，或在某些复杂载荷下的金属，实验证据表明塑性流动的方向不垂直于[屈服面](@entry_id:175331)。为了模拟这种行为，可以选择一个不同于[屈服函数](@entry_id:167970) $f$ 的塑性势 $g$（$g \neq f$）。这被称为**非关联**流动 。虽然非关联性为拟合实验数据提供了更大的灵活性，但它也带来了深刻而具挑战性的后果。

#### 热力学稳定性

在等温力学过程中，[热力学第二定律](@entry_id:142732)要求[机械耗散](@entry_id:169843)率 $\mathcal{D} = \boldsymbol{\sigma} : \dot{\boldsymbol{\varepsilon}}^{vp}$ 必须为非负。对于Perzyna型模型，这意味着：
$$
\mathcal{D} = \boldsymbol{\sigma} : \left( \phi(\langle f \rangle) \frac{\partial g}{\partial \boldsymbol{\sigma}} \right) = \phi(\langle f \rangle) \left( \boldsymbol{\sigma} : \frac{\partial g}{\partial \boldsymbol{\sigma}} \right) \ge 0
$$
对于关联流动（$g=f$），如果 $f$ 是一个[凸函数](@entry_id:143075)且原点 $\boldsymbol{\sigma}=\mathbf{0}$ 在弹性域内，可以证明对于任何在[屈服面](@entry_id:175331)上或之外的应力，$\boldsymbol{\sigma} : (\partial f / \partial \boldsymbol{\sigma}) \ge 0$。由于 $\phi(\cdot)$ 也是非负的，因此耗散必定为正。

对于[非关联流动](@entry_id:199220)，这一保证便不复存在。项 $\boldsymbol{\sigma} : (\partial g / \partial \boldsymbol{\sigma})$ 可能变为负值。例如，考虑一个J2材料，其中流动方向 $\mathbf{n}_g$ 与法向 $\mathbf{n}_f = \mathbf{s}/\|\mathbf{s}\|$ 成一个角度 $\theta$。耗散率变得与 $\boldsymbol{\sigma} : \mathbf{n}_g = \mathbf{s} : \mathbf{n}_g = \|\mathbf{s}\| \cos(\theta)$ 成正比。如果角度 $\theta$ 大于 $\pi/2$，耗散就会变为负值（$\mathcal{D}  0$）。这意味着材料在塑性变形过程中会产生能量，这违反了热力学第二定律。这样的[本构模型](@entry_id:174726)是物理上不稳定的 。

#### 算法上的后果

关联与[非关联流动](@entry_id:199220)之间的区别也对求解边界值问题的[数值算法](@entry_id:752770)（例如在有限元方法中）有关键影响。在一个时间步内求解[非线性](@entry_id:637147)[本构方程](@entry_id:138559)需要迭代过程（如[牛顿法](@entry_id:140116)），这又需要对应力更新进行线性化。这种线性化产生了**一致算法切向模量** $\mathbb{C}_{\text{alg}} = \partial \boldsymbol{\sigma}_{n+1} / \partial \boldsymbol{\varepsilon}_{n+1}$。

对于关联模型，其底层数学结构是一个约束优化问题。这种结构确保了最终的算法切向模量 $\mathbb{C}_{\text{alg}}$ 具有**主对称性**。对称的切向模量使得有限元模拟中的[全局刚度矩阵](@entry_id:138630)也是对称的，从而可以使用[共轭梯度法](@entry_id:143436)等鲁棒的求解器高效求解 。

对于非关联模型，这种对称结构被破坏了。[流动法则](@entry_id:177163)不再能从定义约束的同一个势函数中导出，算法切向模量 $\mathbb{C}_{\text{alg}}$ 变为**非对称**的。这对实现有两个主要后果 ：
1.  使用精确的非对称切向模量会导致非对称的[全局刚度矩阵](@entry_id:138630)。虽然这保持了[牛顿法](@entry_id:140116)理想的二次[收敛率](@entry_id:146534)，但它需要使用计算成本更高、内存消耗更大的非对称[线性求解器](@entry_id:751329)（例如GMRES）。
2.  可以选择只使用切向模量的对称部分 $\frac{1}{2}(\mathbb{C}_{\text{alg}} + \mathbb{C}_{\text{alg}}^{\mathsf{T}_{\text{maj}}})$，以保留对称的全局矩阵并使用更简单的求解器。然而，这意味着该算法不再是真正的[牛顿法](@entry_id:140116)。雅可比矩阵不精确，[收敛率](@entry_id:146534)通常会从二次下降到线性或超线性，往往需要更多迭代才能达到解。

### 与物理机制和现象的联系

虽然Perzyna和[Duvaut-Lions模型](@entry_id:748713)是唯象的，但它们的数学形式可以由底层的物理过程和宏观观察所启发和关联。

#### [幂律](@entry_id:143404)黏塑性的微观结构起源

应变率和过应力之间普遍存在的[幂律](@entry_id:143404)关系不仅仅是一种方便的数学选择；它可以从位错运动模型中推导出来。宏观黏塑性[剪切应变率](@entry_id:276945) $\dot{\gamma}$ 由**Orowan关系**给出，$\dot{\gamma} = \rho b v$，其中 $\rho$ 是可动[位错](@entry_id:157482)的密度，$b$ 是柏氏矢量的大小，$v$ 是平均[位错](@entry_id:157482)速度。

如果我们考虑一种材料，其中[位错](@entry_id:157482)被微观结构障碍物（例如，[位错](@entry_id:157482)林、析出物）的随机[分布](@entry_id:182848)所钉扎，一个给定的[位错](@entry_id:157482)段只有在施加的应力 $\tau$ 超过其局部脱钉应力 $\tau_c$ 时才能移动。因此，可动[位错](@entry_id:157482)的总体是所有满足 $\tau_c  \tau$ 的[位错](@entry_id:157482)段。如果脱钉后的速度遵循像 $v \propto (\tau - \tau_c)^p$ 这样的规律，并且宏观屈服阈值 $\tau_0$ 附近的障碍物强度[统计分布](@entry_id:182030)遵循[形状参数](@entry_id:270600)为 $k$ 的[威布尔分布](@entry_id:270143)，那么通过对所有可动[位错](@entry_id:157482)的贡献进行积分，可以得到一个形式为 $\dot{\gamma} \propto \langle \tau - \tau_0 \rangle^{m}$ 的宏观[流动法则](@entry_id:177163)。最终的宏观指数被发现是微观指数之和：$m = p+k$ 。这个有力的结果表明，唯象的率敏感性指数 $m$ 如何包含了关于微观结构障碍物[分布](@entry_id:182848)（$k$）和[位错](@entry_id:157482)-障碍[物相](@entry_id:196677)互作用物理（$p$）的信息。

#### 模拟[蠕变行为](@entry_id:199994)

黏塑性模型特别适用于描述**蠕变**，即材料在恒定载荷下的时间相关变形。典型的[蠕变](@entry_id:150410)曲线表现出三个阶段：
1.  **[初始蠕变](@entry_id:204710)**：[应变率](@entry_id:154778)最初很高，但随时间减速。
2.  **[稳态蠕变](@entry_id:161740)**：应变率稳定在一个近似恒定的值。
3.  **三级蠕变**：[应变率](@entry_id:154778)开始加速，最终导致断裂。

包含[硬化](@entry_id:177483)和动态恢复的标准黏塑性模型可以自然地捕捉前两个阶段 。当首次施加恒定应力时，过应力很高，导致初始[应变率](@entry_id:154778)很高。这种塑性流动引起应变硬化，增加了[屈服强度](@entry_id:162154)，从而减小了过应力并导致[应变率](@entry_id:154778)减速（[初始蠕变](@entry_id:204710)）。随着时间的推移，[热激活](@entry_id:201301)的恢复机制（例如，[位错攀移](@entry_id:199426)和湮灭）抵消了硬化。最终达到一个动态平衡，其中硬化速率与恢复速率相平衡。此时，材料的内部状态变得恒定，过应力变得恒定，材料以稳定的速率变形（[稳态蠕变](@entry_id:161740)）。

然而，这些模型在其基本形式下无法捕捉三级蠕变。在恒定施加应力下，应变率的加速需要一种能够持续*降低*材料强度或有效承载面积的机制。这需要引入额外的物理过程，例如**损伤**的演化（如孔洞[形核](@entry_id:140577)与长大、微裂纹）或几何不稳定性（如颈缩），而这些并非标准黏塑性框架的一部分 。

最后，对于许多涉及[稳态蠕变](@entry_id:161740)的工程应用，通常使用更简单的经验定律，如**诺顿[蠕变](@entry_id:150410)[幂律](@entry_id:143404)** $\dot{\varepsilon}^c = A \sigma^n$。重要的是要认识到，这些定律可以被视为更全面的基于阈值的模型（如[Perzyna模型](@entry_id:753365)）的近似。通过在特定工作应力 $\sigma_0$ 处匹配[Perzyna模型](@entry_id:753365)的值和应力敏感性，可以为诺顿型定律推导出等效的参数 $A$ 和 $n$。这提供了一个在工作点附近有效的有用近似，但它在远离 $\sigma_0$ 的应力下必然不准确，尤其是在真实[屈服应力](@entry_id:274513)附近，[Perzyna模型](@entry_id:753365)预测流动为零，而诺顿模型预测非零流动速率 。