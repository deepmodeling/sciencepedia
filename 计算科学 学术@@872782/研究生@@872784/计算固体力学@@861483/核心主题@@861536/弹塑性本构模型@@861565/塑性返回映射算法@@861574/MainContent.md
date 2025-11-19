## 引言
在[计算固体力学](@entry_id:169583)领域，精确模拟材料从弹性到塑性的复杂行为是[结构完整性](@entry_id:165319)分析的核心。当[材料屈服](@entry_id:751736)并进入塑性阶段，其响应变得不可逆且依赖于加载历史，这对[有限元分析](@entry_id:138109)中的本构关系积分提出了严峻挑战。传统的显式积分方法往往需要极小的时间步长以保证稳定性，而[返回映射算法](@entry_id:168456)（Return Mapping Algorithms, RMA）作为一种隐式积分方案，为高效、稳健地解决这一问题提供了标准[范式](@entry_id:161181)。它的重要性不仅在于其在数值计算中的核心地位，更在于其思想的普适性，使其成为连接多个工程与科学领域的桥梁。

本文旨在系统性地剖析[返回映射算法](@entry_id:168456)的理论精髓与实践应用。读者将通过三个层层递进的章节，全面掌握这一关键技术。

首先，在“原理与机制”一章中，我们将深入探讨算法的“弹性预测-塑性校正”核心思想，建立起[塑性流动](@entry_id:201346)的基本法则，并以经典的J2塑性模型为例，详细推导[径向返回算法](@entry_id:169742)及其关键的“一致性[切线刚度](@entry_id:166213)”，为理解算法的数值性能奠定基础。接着，在“应用与跨学科关联”一章中，我们将展示该算法框架的强大通用性，探讨其如何应用于复杂的硬化模型、[各向异性材料](@entry_id:184874)以及岩[土力学](@entry_id:180264)等领域，并揭示其与接触力学、[优化理论](@entry_id:144639)等学科的深刻联系。最后，通过“动手实践”环节，读者将有机会通过解决具体问题，将理论知识转化为实际的编程与分析能力。

通过本文的学习，您将不仅理解[返回映射算法](@entry_id:168456)的“如何做”，更能深刻领会其背后的“为什么”，从而在科研和工程实践中更加灵活、自信地应用这一强大的计算工具。

## 原理与机制

在[弹塑性](@entry_id:193198)材料的数值模拟中，一个核心挑战是在离散的时间步内准确地积分本构关系。当材料进入塑性状态时，其响应变得不可逆且依赖于加载历史。[返回映射算法](@entry_id:168456)（Return Mapping Algorithms, RMA）为解决这一问题提供了一个强大而通用的框架。本章将深入探讨这些算法背后的基本原理与核心机制，从最基础的 predictor-corrector（预测-校正）思想出发，系统地建立起适用于经典 $J_2$ 塑性理论的算法，并进一步探讨其在更高级材料模型和计算实现中的应用。

### 核心思想：弹性预测与塑性校正

[返回映射算法](@entry_id:168456)的根本思想可分解为一个两步过程：**弹性预测**和**塑性校正**。在一个增量步中，我们首先假设整个变形增量完全由弹性产生，这构成了“预测”阶段。然后，我们检查这个纯弹性假设下的应力状态是否在材料的容许范围内。如果超出了范围，就必须进行“校正”，将应力状态“[拉回](@entry_id:160816)”到容许的塑性边界上。

这个“容许范围”在[应力空间](@entry_id:199156)中由一个**屈服面 (yield surface)** 来定义。[屈服面](@entry_id:175331)由一个标量**[屈服函数](@entry_id:167970)** $f$ 描述，其形式通常为 $f(\boldsymbol{\sigma}, \boldsymbol{q}) \le 0$，其中 $\boldsymbol{\sigma}$ 是柯西应力张量，$\boldsymbol{q}$ 代表一组描述材料内部状态的[硬化](@entry_id:177483)变量（例如，等效塑性应变）。$f  0$ 的区域代表纯弹性状态， $f = 0$ 代表材料正处于屈服状态（即塑性状态），而 $f > 0$ 的状态在物理上是不允许的。

让我们通过一个具体的例子来理解**弹性预测**步骤。假设一个材料点在上一个收敛步结束时的应力状态为 $\boldsymbol{\sigma}_n$，在当前增量步中，它承受了应变增量 $\Delta\boldsymbol{\varepsilon}$。在弹性预测阶段，我们计算一个“试探应力” $\boldsymbol{\sigma}^{\text{tr}}$，它等于[初始应力](@entry_id:750652)加上完全由 $\Delta\boldsymbol{\varepsilon}$ 产生的弹性应力增量：
$$
\boldsymbol{\sigma}^{\text{tr}} = \boldsymbol{\sigma}_n + \mathbb{C}^e : \Delta\boldsymbol{\varepsilon}
$$
其中 $\mathbb{C}^e$ 是四阶[弹性刚度张量](@entry_id:170728)。对于[各向同性线弹性](@entry_id:185899)材料，这个关系可以用拉梅参数 $\lambda$ 和[剪切模量](@entry_id:167228) $G$ 来表示。例如，如果我们已知一个[初始应力](@entry_id:750652)[状态和](@entry_id:193625)材料的弹性常数（如[杨氏模量](@entry_id:140430) $E$ 和[泊松比](@entry_id:158876) $\nu$），我们可以直接计算出任何给定应变增量所对应的试探应力 $\boldsymbol{\sigma}^{\text{tr}}$ [@problem_id:3596265]。

得到试探应力后，下一步是评估[屈服函数](@entry_id:167970) $f^{\text{tr}} = f(\boldsymbol{\sigma}^{\text{tr}}, \boldsymbol{q}_n)$ 的值。
- 如果 $f^{\text{tr}} \le 0$，说明试探应力位于弹性域内部或恰好在[屈服面](@entry_id:175331)上。这意味着弹性假设是成立的（或处于[临界状态](@entry_id:160700)），该增量步是纯弹性的（或中性加载）。我们接受试探状态作为最终状态，即 $\boldsymbol{\sigma}_{n+1} = \boldsymbol{\sigma}^{\text{tr}}$，并且没有塑性变形发生。
- 如果 $f^{\text{tr}} > 0$，说明试探应力已经超出了屈服面，进入了“不允许”的区域。这意味着材料在此增量步中发生了塑性变形。此时，必须启动**塑性校正**步骤，将应力从 $\boldsymbol{\sigma}^{\text{tr}}$ “返回”到更新后的屈服面上，得到最终的应力状态 $\boldsymbol{\sigma}_{n+1}$，并确保 $\boldsymbol{\sigma}_{n+1}$ 满足 $f(\boldsymbol{\sigma}_{n+1}, \boldsymbol{q}_{n+1}) = 0$。这个校正过程就是[返回映射算法](@entry_id:168456)的核心。

### 塑性流动的基本法则：屈服条件与[流动法则](@entry_id:177163)

为了精确执行塑性校正，我们需要一套明确的规则来指导这一过程。这套规则主要包括屈服条件、硬化规律、流动方向以及加载/卸载的判断准则。

#### [屈服函数](@entry_id:167970)与[硬化](@entry_id:177483)

对于许多金属材料，其塑性屈服行为与[静水压力](@entry_id:275365)无关，主要由偏应力决定。经典的 **von Mises 屈服准则** 正是基于这一假设。它定义了一个**[等效应力](@entry_id:749064)** $\sigma_{\text{eq}}$，当该值达到材料当前的[屈服强度](@entry_id:162154) $\sigma_y$ 时，材料开始屈服。[等效应力](@entry_id:749064)是[偏应力](@entry_id:163323)第二[不变量](@entry_id:148850) $J_2 = \frac{1}{2} \mathbf{s}:\mathbf{s}$ 的函数，其中 $\mathbf{s} = \boldsymbol{\sigma} - \frac{1}{3}\text{tr}(\boldsymbol{\sigma})\mathbf{I}$ 是[偏应力张量](@entry_id:267642)。通过与[单轴拉伸试验](@entry_id:195375)结果进行标定，可以推导出[等效应力](@entry_id:749064)的标准形式 [@problem_id:3596247]：
$$
\sigma_{\text{eq}} = \sqrt{3 J_2} = \sqrt{\frac{3}{2}\mathbf{s}:\mathbf{s}}
$$
于是，von Mises [屈服函数](@entry_id:167970)可以写为：
$$
f(\boldsymbol{\sigma}, \kappa) = \sigma_{\text{eq}}(\boldsymbol{\sigma}) - \sigma_y(\kappa) \le 0
$$
这里的 $\kappa$ 是一个标量内部变量，代表累积等效塑性应变，用于描述材料的硬化状态。

随着塑性变形的累积，材料的[屈服强度](@entry_id:162154)通常会发生变化，这种现象称为**硬化**。在**[各向同性硬化](@entry_id:164486) (isotropic hardening)** 模型中，屈服面在应力空间中均匀地扩张，其中心保持不变。一个简单的模型是**线性[各向同性硬化](@entry_id:164486)**，其屈服强度与累积塑性应变成线性关系：
$$
\sigma_y(\kappa) = \sigma_{y0} + H\kappa
$$
其中 $\sigma_{y0}$ 是初始屈服强度，$H$ 是常数硬化模量。在这种情况下，[屈服面](@entry_id:175331) $f=0$ 在[主应力空间](@entry_id:184388)中表示一个圆柱体（von Mises 圆柱），其半径 $\sigma_y(\kappa)$ 随着 $\kappa$ 的增加而线性增大 [@problem_id:3596254]。

#### 加载/卸载条件：[Kuhn-Tucker 条件](@entry_id:185881)

如何判断一个增量步是否会产生塑性变形？这由一组被称为 **Kuhn-Tucker (KKT) 条件**的互补关系严格定义。这些条件源于[塑性流动](@entry_id:201346)的不[可逆性](@entry_id:143146)和[约束优化理论](@entry_id:635923)，它们将[屈服函数](@entry_id:167970) $f$ 和塑性流动的大小（由塑性乘子增量 $\Delta\lambda$ 表示）联系在一起 [@problem_id:3596307]：
1.  **容许性条件**: $f \le 0$。应力状态必须始终位于弹性域内或其边界上。
2.  **不可逆性条件**: $\Delta\lambda \ge 0$。塑性变形是耗散过程，不能逆转。塑性乘子增量必须非负。
3.  **互补或[一致性条件](@entry_id:637057)**: $\Delta\lambda \cdot f = 0$。这个条件是关键的“开关”。

这三个条件共同构成了加载/卸载的判断准则：
- **弹性加载/卸载**: 当 $f  0$ 时，为了满足[互补条件](@entry_id:747558)，必须有 $\Delta\lambda = 0$。这意味着没有[塑性流动](@entry_id:201346)。
- **塑性加载**: 当发生塑性流动时，$\Delta\lambda > 0$。为了满足[互补条件](@entry_id:747558)，必须有 $f = 0$。这意味着应力状态必须维持在[屈服面](@entry_id:175331)上。
- **中性加载**: 当 $f = 0$ 且 $\Delta\lambda = 0$ 时，应力状态在[屈服面](@entry_id:175331)上，但当前增量步并未引起新的塑性变形。

在[返回映射算法](@entry_id:168456)中，如果弹性预测导致 $f^{\text{tr}} > 0$，KKT 条件就要求最终状态必须满足 $f=0$ 和 $\Delta\lambda > 0$。

#### 流动方向：关联与[非关联流动法则](@entry_id:752544)

当[塑性流动](@entry_id:201346)发生时（$\Delta\lambda > 0$），塑性应变增量 $\Delta\boldsymbol{\varepsilon}^p$ 的方向由**流动法则 (flow rule)** 决定。一个广义的流动法则引入了**塑性势函数** $g(\boldsymbol{\sigma}, \boldsymbol{q})$ 的概念，并假定塑性[应变率](@entry_id:154778)的方向垂直于塑性[势函数](@entry_id:176105)的[等值面](@entry_id:196027)：
$$
\Delta\boldsymbol{\varepsilon}^p = \Delta\lambda \frac{\partial g}{\partial \boldsymbol{\sigma}}
$$
这里引出了一个至关重要的区别 [@problem_id:3596285]：
- **关联流动法则 (Associated Flow Rule)**: 当塑性[势函数](@entry_id:176105)与[屈服函数](@entry_id:167970)相同时，即 $g = f$。此时，塑性应变增量的方向垂直于[屈服面](@entry_id:175331)。这被称为**法向法则 (normality rule)**。对于[凸屈服面](@entry_id:203690)，该法则与 Drucker 稳定性公设（或[最大塑性耗散](@entry_id:184825)原理）相一致，具有坚实的物理基础。
- **[非关联流动法则](@entry_id:752544) (Non-Associated Flow Rule)**: 当塑性[势函数](@entry_id:176105)与[屈服函数](@entry_id:167970)不同时，即 $g \neq f$。此时，塑性流动的方向不再垂直于屈服面。

这一选择具有深刻的物理和计算意义。例如，在模拟土壤、岩石等[压敏材料](@entry_id:753710)时，关联流动法则往往会高估材料在剪切作用下的[体积膨胀](@entry_id:144241)（[剪胀性](@entry_id:201001)）。而采用[非关联流动法则](@entry_id:752544)，可以选择一个与[屈服函数](@entry_id:167970)（描述强度）不同的塑性[势函数](@entry_id:176105)（描述流动和剪胀），从而更真实地模拟材料行为。然而，这种灵活性是有代价的：在有限元计算中，关联[流动法则](@entry_id:177163)（对于[各向同性硬化](@entry_id:164486)）通常会产生对称的**算法一致性[切线刚度矩阵](@entry_id:170852)**，而这对于保持[牛顿-拉弗森法](@entry_id:140620)（[Newton-Raphson](@entry_id:177436) method）的二次[收敛速度](@entry_id:636873)至关重要。[非关联流动](@entry_id:199220)则通常导致非对称的[切线](@entry_id:268870)矩阵，增加了计算的复杂性和成本。

对于经典的金属 $J_2$ 塑性理论，通常采用关联[流动法则](@entry_id:177163)，因为它既符合物理观测，又具有计算上的优势。

### 经典的 J2 [径向返回算法](@entry_id:169742)详解

现在，我们将上述原理应用于 $J_2$ 塑性模型，并推导其[返回映射算法](@entry_id:168456)。我们假设采用关联流动法则和线性[各向同性硬化](@entry_id:164486)模型。

塑性校正的核心方程是应力更新公式，它将最终应力 $\boldsymbol{\sigma}_{n+1}$ 与试探应力 $\boldsymbol{\sigma}^{\text{tr}}$ 联系起来：
$$
\boldsymbol{\sigma}_{n+1} = \boldsymbol{\sigma}^{\text{tr}} - \mathbb{C}^e : \Delta\boldsymbol{\varepsilon}^p
$$
对于 $J_2$ 塑性，[塑性流动](@entry_id:201346)是等体积的（$\text{tr}(\Delta\boldsymbol{\varepsilon}^p) = 0$），因此校正过程不影响[静水压力](@entry_id:275365)，即 $\text{tr}(\boldsymbol{\sigma}_{n+1}) = \text{tr}(\boldsymbol{\sigma}^{\text{tr}})$。我们只需关注[偏应力](@entry_id:163323)部分：
$$
\mathbf{s}_{n+1} = \mathbf{s}^{\text{tr}} - 2G \Delta\boldsymbol{\varepsilon}^p_{\text{dev}}
$$
根据关联[流动法则](@entry_id:177163)，$\Delta\boldsymbol{\varepsilon}^p = \Delta\lambda \frac{\partial f}{\partial \boldsymbol{\sigma}}\Big|_{\boldsymbol{\sigma}_{n+1}}$。对于 von Mises [屈服函数](@entry_id:167970)，其梯度为 $\frac{\partial f}{\partial \boldsymbol{\sigma}} = \frac{\partial \sigma_{\text{eq}}}{\partial \boldsymbol{\sigma}} = \frac{3}{2\sigma_{\text{eq}}}\mathbf{s}$。因此，
$$
\mathbf{s}_{n+1} = \mathbf{s}^{\text{tr}} - 2G \Delta\lambda \left( \frac{3}{2\sigma_{\text{eq}, n+1}} \mathbf{s}_{n+1} \right) = \mathbf{s}^{\text{tr}} - 3G \Delta\lambda \frac{\mathbf{s}_{n+1}}{\sigma_{\text{eq}, n+1}}
$$
整理上式可得：
$$
\mathbf{s}^{\text{tr}} = \mathbf{s}_{n+1} \left( 1 + \frac{3G \Delta\lambda}{\sigma_{\text{eq}, n+1}} \right)
$$
这个简单的关系揭示了一个深刻的几何事实：最终的[偏应力张量](@entry_id:267642) $\mathbf{s}_{n+1}$ 与试探[偏应力张量](@entry_id:267642) $\mathbf{s}^{\text{tr}}$ 是共线的。这意味着塑性校正的过程是在偏应力空间中，沿着从 $\mathbf{s}^{\text{tr}}$ 指向原点的直线进行的。这正是 **“[径向返回](@entry_id:754007)” (Radial Return)** 这一名称的由来。这种简洁的返回路径是材料各向同性假设的直接结果。通过**谱分解 (spectral decomposition)** 可以更严格地证明，对于[各向同性材料](@entry_id:170678)，[返回映射](@entry_id:754324)过程保持了[主应力方向](@entry_id:753737)，仅对[主应力](@entry_id:176761)值进行缩放 [@problem_id:3596289]。

现在我们求解塑性乘子 $\Delta\lambda$。对上述共线关系两边取[等效应力](@entry_id:749064)（范数）：
$$
\sigma_{\text{eq}}^{\text{tr}} = \sigma_{\text{eq}, n+1} \left( 1 + \frac{3G \Delta\lambda}{\sigma_{\text{eq}, n+1}} \right) = \sigma_{\text{eq}, n+1} + 3G \Delta\lambda
$$
根据一致性条件，最终状态必须在更新后的屈服面上，即 $\sigma_{\text{eq}, n+1} = \sigma_y(\kappa_{n+1})$。对于[线性硬化模型](@entry_id:180941)，$\sigma_y(\kappa_{n+1}) = \sigma_y(\kappa_n) + H\Delta\kappa$。对于 $J_2$ 塑性，累积塑性应变增量 $\Delta\kappa$ 与塑性乘子 $\Delta\lambda$ 相等，即 $\Delta\kappa = \Delta\lambda$。于是：
$$
\sigma_{\text{eq}, n+1} = \sigma_y(\kappa_n) + H\Delta\lambda
$$
将此式代入 $\sigma_{\text{eq}}^{\text{tr}}$ 的表达式中：
$$
\sigma_{\text{eq}}^{\text{tr}} = (\sigma_y(\kappa_n) + H\Delta\lambda) + 3G \Delta\lambda
$$
解出 $\Delta\lambda$：
$$
\Delta\lambda = \frac{\sigma_{\text{eq}}^{\text{tr}} - \sigma_y(\kappa_n)}{3G + H} = \frac{f^{\text{tr}}}{3G + H}
$$
这是一个非常简洁的[闭式](@entry_id:271343)解，仅在 $f^{\text{tr}} > 0$ 时有效。一旦求得 $\Delta\lambda$，就可以计算出最终的应力 $\mathbf{s}_{n+1}$ 和更新后的[硬化](@entry_id:177483)变量 $\kappa_{n+1}$，从而完成整个增量步的计算 [@problem_id:3596247]。

### 数学基础与模型拓展

一个鲁棒的数值算法不仅需要能够执行计算，还需要建立在坚实的数学基础之上，并能够适应更复杂的材料行为。

#### [返回映射](@entry_id:754324)的[适定性](@entry_id:148590)

[返回映射算法](@entry_id:168456)在几何上可以被看作是将一个点（试探应力）投影到应力空间中的一个集合（弹性域）上。为了保证这个投影是唯一的、稳定的，[屈服函数](@entry_id:167970) $f$ 和它所定义的弹性域需要满足一定的数学条件 [@problem_id:3596308]。
- **凸性 (Convexity)**: 弹性域 $\mathcal{E} = \{\boldsymbol{\sigma} | f(\boldsymbol{\sigma}, \boldsymbol{q}) \le 0\}$ 必须是一个[凸集](@entry_id:155617)。这是[经典塑性理论](@entry_id:167389)的基石，它保证了对于任何在域外的点 $\boldsymbol{\sigma}^{\text{tr}}$，存在一个唯一的“最近点”投影。[屈服函数](@entry_id:167970) $f$ 本身是 $\boldsymbol{\sigma}$ 的凸函数是保证弹性域凸性的一个充分条件。
- **[光滑性](@entry_id:634843) (Smoothness)**: [流动法则](@entry_id:177163) $\Delta\boldsymbol{\varepsilon}^p = \Delta\lambda \frac{\partial f}{\partial \boldsymbol{\sigma}}$ 要求[屈服函数](@entry_id:167970) $f$ 的梯度存在，以便定义唯一的[塑性流动](@entry_id:201346)方向。因此，$f$ 至少需要是[几乎处处](@entry_id:146631)连续可微的 ($C^1$)。对于像 von Mises 准则的范数形式 $f = \sqrt{3J_2} - \sigma_y$，在 $\mathbf{s}=\mathbf{0}$ 处是不可微的。为了便于数值处理，常采用其等价的光滑形式，如 $f = 3J_2 - \sigma_y^2 \le 0$。而对于 Drucker-Prager 这类在屈服面锥顶处存在[奇异点](@entry_id:199525)的模型，算法需要特殊的处理逻辑（例如使用[次梯度](@entry_id:142710)理论）。

#### [非线性](@entry_id:637147)硬化与非[各向同性弹性](@entry_id:203237)

当硬化行为不再是线性的，即[硬化](@entry_id:177483)模量 $H$ 不再是常数，而是依赖于累积塑性应变 $H(\kappa)$ 时，求解塑性乘子 $\Delta\lambda$ 的方程将变为一个[非线性](@entry_id:637147)标量方程 [@problem_id:3596268]：
$$
\sigma_{\text{eq}}^{\text{tr}} - 3G\Delta\lambda - \sigma_y(\kappa_n + \Delta\lambda) = 0
$$
这个方程通常需要使用数值方法（如 [Newton-Raphson](@entry_id:177436) 法）来求解。同样，如果材料的弹性响应不是各向同性的，例如，[弹性模量](@entry_id:198862)依赖于[主应力方向](@entry_id:753737)，那么返回路径也可能不再是严格的“径向”，其主应力分量的缩放比例会不同，导致返回路径偏离直线 [@problem_id:3596289]。

#### 向有限变形的推广

[返回映射](@entry_id:754324)的思想可以优雅地推广到有限变形框架下。在小应变理论中，我们使用应变的加法分解 $\boldsymbol{\varepsilon} = \boldsymbol{\varepsilon}^e + \boldsymbol{\varepsilon}^p$。而在有限变形理论中，[运动学](@entry_id:173318)假设被**变形梯度的[乘法分解](@entry_id:199514)**所取代：$\mathbf{F} = \mathbf{F}^e \mathbf{F}^p$。这里 $\mathbf{F}^p$ 将未变形的参考构型映射到一个假想的、卸除应力的[中间构型](@entry_id:193000)，而 $\mathbf{F}^e$ 则将[中间构型](@entry_id:193000)映射到当前的变形构型 [@problem_id:3596275]。

在这种框架下，[返回映射算法](@entry_id:168456)可以在[对数应变](@entry_id:751438)空间中重新构建。采用基于弹性[对数应变](@entry_id:751438) $\mathbf{E}^e = \frac{1}{2}\ln(\mathbf{F}^e{\mathbf{F}^e}^T)$ 的 Hencky-type [超弹性](@entry_id:159356)模型，其共轭的应力度量是 Kirchhoff 应力 $\boldsymbol{\tau}$。令人惊讶的是，在这种[变量选择](@entry_id:177971)下，[返回映射算法](@entry_id:168456)的结构与小应变情况惊人地相似。例如，对于 $J_2$ 塑性，算法仍然表现为在偏 Kirchhoff [应力空间](@entry_id:199156)中的[径向返回](@entry_id:754007) [@problem_id:3596275]。这种框架因其理论上的优雅性和数值上的鲁棒性而备受青睐。

### 在计算实现中的作用：一致性[切线刚度](@entry_id:166213)

[返回映射算法](@entry_id:168456)是作为有限元等全局求解器中的一个“局部”本构驱动程序来运行的。在每个高斯积分点，它根据给定的总应变增量来更新应力。为了使全局的[非线性](@entry_id:637147)求解过程（通常是 [Newton-Raphson](@entry_id:177436) 法）高效收敛，我们需要提供一个准确的[切线刚度矩阵](@entry_id:170852)。

理想的[切线刚度矩阵](@entry_id:170852)是全局残差向量关于全局自由度（位移）的精确导数，即雅可比矩阵。为了构造这个精确的雅可比矩阵，我们需要在积分点层面提供应力关于应变的精确线性化，即 $\text{d}\boldsymbol{\sigma} = \mathbb{C}^{\text{alg}} : \text{d}\boldsymbol{\varepsilon}$。这里的 $\mathbb{C}^{\text{alg}}$ 就是**算法一致性[切线刚度](@entry_id:166213) (algorithmic consistent tangent)**，它被定义为[返回映射算法](@entry_id:168456)本身的精确线性化。

使用这个近似刚度通常会导致[线性收敛](@entry_id:163614)。为了确保 [Newton-Raphson](@entry_id:177436) 迭代在解的邻域内具有**二次收敛**速度，必须使用通过对[返回映射算法](@entry_id:168456)本身进行精确线性化而得到的**算法一致性[切线刚度](@entry_id:166213)** $\mathbb{C}^{\text{alg}}$ [@problem_id:3596276]。它的推导更为复杂，但能极大地提高计算效率。因此，推导和实现正确的一致性[切线刚度](@entry_id:166213)是现代[计算塑性力学](@entry_id:171377)中一个不可或缺的环节。