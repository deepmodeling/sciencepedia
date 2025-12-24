## 引言
在[固体力学](@entry_id:164042)，特别是塑性力学领域，理解材料在超过[弹性极限](@entry_id:186242)后的行为至关重要。对于[金属成形](@entry_id:188560)等经历大规模塑性变形的工程问题，复杂的[弹塑性](@entry_id:193198)[本构关系](@entry_id:186508)往往导致分析异常困难。为了解决这一挑战，[刚塑性流动](@entry_id:197608)理论提供了一个精炼而强大的简化模型，其核心正是**Lévy-Mises方程**。该理论通过忽略[弹性应变](@entry_id:189634)，将问题转化为一个更易于处理的流动问题，为分析材料流动、预测成形力以及评估结构极限承载能力提供了深刻的洞见。

本文旨在系统性地构建[刚塑性流动](@entry_id:197608)理论的完整框架，填补基础概念与高级应用之间的知识鸿沟。读者将通过本文学习到：

- **第一章：原理与机制**，将从刚-[理想塑性](@entry_id:753335)材料的基本假设出发，详细推导基于[von Mises屈服准则](@entry_id:174339)和相联流动法则的Lévy-Mises方程，并阐明其物理内涵，如[塑性不可压缩性](@entry_id:183440)和[主轴](@entry_id:172691)共轴性。

- **第二章：应用与跨学科联系**，将展示该理论如何在[金属成形](@entry_id:188560)、[极限分析](@entry_id:188743)等工程实践中发挥作用，并揭示其与[流体力学](@entry_id:136788)、计算科学和[材料科学](@entry_id:152226)等领域的深刻类比与联系。

- **第三章：动手实践**，将通过一系列精心设计的问题，引导读者将理论知识应用于具体的计算和推导，从而巩固对核心概念的掌握。

本章将首先从理论的基石——[刚塑性流动](@entry_id:197608)模型的基本框架开始，逐步深入其核心机制。

## 原理与机制

本章在前一章介绍塑性力学基本概念的基础上，深入探讨一种在[金属成形](@entry_id:188560)和[极限分析](@entry_id:188743)等领域具有重要理论和应用价值的模型：[刚塑性流动](@entry_id:197608)理论，并重点阐述其核心[本构关系](@entry_id:186508)——**Lévy-Mises方程**。我们将从基本假设出发，系统构建该理论的数学框架，阐明其背后的物理原理和力学机制，并讨论其[适用范围](@entry_id:636189)与局限性。

### [刚塑性流动](@entry_id:197608)模型的基本框架

在许多大规模塑性变形问题中，如金属锻造或挤压，塑性应变远大于弹性应变。在这种情况下，为了简化分析，可以引入**刚-[理想塑性](@entry_id:753335)**（rigid-perfectly plastic）材料的理想化模型。该模型的核心假设是：材料在应力达到屈服极限之前是完全刚性的（即不产生任何变形），一旦达到屈服极限，便开始[塑性流动](@entry_id:201346)，且流动过程中不发生[硬化](@entry_id:177483)（即[屈服应力](@entry_id:274513)保持不变）。

这一理想化极大地简化了问题的数学描述。由于[弹性应变](@entry_id:189634)被忽略，总应变率张量 $\dot{\boldsymbol{\varepsilon}}$ 等同于塑性[应变率张量](@entry_id:266108) $\dot{\boldsymbol{\varepsilon}}^p$。对于一个小变形问题，控制[方程组](@entry_id:193238)主要由以下几个部分构成 ：

1.  **[平衡方程](@entry_id:172166)**：在忽略惯性效应的[准静态过程](@entry_id:136273)中，物体内任意部分的力都必须保持平衡。这由柯西（Cauchy）[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ 的散度来表达：
    $$ \nabla \cdot \boldsymbol{\sigma} + \mathbf{b} = \mathbf{0} $$
    其中 $\mathbf{b}$ 是单位体积的体力。此外，动量矩平衡要求柯西应力张量是对称的，即 $\boldsymbol{\sigma} = \boldsymbol{\sigma}^T$。

2.  **[运动学方程](@entry_id:173032)**：[应变率张量](@entry_id:266108) $\dot{\boldsymbol{\varepsilon}}$ 描述了材料点的变形速率，它与速度场 $\mathbf{v}$ 之间的关系由下式给出：
    $$ \dot{\boldsymbol{\varepsilon}} = \frac{1}{2}\left(\nabla \mathbf{v} + (\nabla \mathbf{v})^T\right) $$
    在刚塑性模型中，由于[弹性应变](@entry_id:189634)的贡献为零，上式给出的总[应变率](@entry_id:154778)即为塑性应变率 $\dot{\boldsymbol{\varepsilon}}^p$。

3.  **[本构关系](@entry_id:186508)**：这部分描述材料的特定响应，包括[屈服准则](@entry_id:193897)和流动法则，是理论的核心。对于[刚塑性流动](@entry_id:197608)，[本构关系](@entry_id:186508)将应力状态与塑性流动速率联系起来。

这个框架将一个复杂的[弹塑性](@entry_id:193198)问题简化为一个关于[速度场](@entry_id:271461) $\mathbf{v}$ 和应[力场](@entry_id:147325) $\boldsymbol{\sigma}$ 的流动问题。

### [von Mises屈服准则](@entry_id:174339)：压力无关性与[光滑性](@entry_id:634843)

[本构关系](@entry_id:186508)的核心是屈服准则，它定义了材料从刚性状态转变为塑性流动状态的应力边界。对于大多数金属材料，实验表明[静水压力](@entry_id:275365)对其屈服行为影响甚微。为了在数学上描述这种**压力无关性**（pressure-insensitivity），通常将应力张量 $\boldsymbol{\sigma}$ 分解为两部分：

-   **[静水压力](@entry_id:275365)**（hydrostatic pressure）$p$，它引起体积变化：$p = -\frac{1}{3}\text{tr}(\boldsymbol{\sigma}) = -\frac{1}{3}\sigma_{kk}$。
-   **[偏应力张量](@entry_id:267642)**（deviatoric stress tensor）$\mathbf{s}$，它引起形状变化（畸变）：$\mathbf{s} = \boldsymbol{\sigma} + p\mathbf{I}$。[偏应力张量](@entry_id:267642)的迹为零，即 $\text{tr}(\mathbf{s}) = 0$。

**[von Mises屈服准则](@entry_id:174339)**正是基于这一物理观察建立的。它假设材料的屈服仅由[偏应力张量](@entry_id:267642)决定。具体而言，[屈服函数](@entry_id:167970) $f$ 定义为：
$$ f(\boldsymbol{\sigma}) = \sigma_{eq} - \sigma_y = 0 $$
其中 $\sigma_y$ 是材料在[单轴拉伸](@entry_id:188287)下的屈服应力，而 $\sigma_{eq}$ 是 **[von Mises等效应力](@entry_id:756574)**，其定义为：
$$ \sigma_{eq} = \sqrt{\frac{3}{2}\mathbf{s}:\mathbf{s}} = \sqrt{\frac{3}{2}s_{ij}s_{ij}} $$
这里的 $\mathbf{s}:\mathbf{s}$ 是[偏应力张量](@entry_id:267642)的[双点积](@entry_id:748648)。$f  0$ 的应力状态位于屈服面内部，对应刚性行为；$f=0$ 的应力状态位于[屈服面](@entry_id:175331)上，材料可以发生塑性流动；而 $f > 0$ 的状态在[理想塑性](@entry_id:753335)理论中是不允许出现的 。

由于 $\sigma_{eq}$ 仅依赖于偏应力 $\mathbf{s}$，[von Mises屈服准则](@entry_id:174339)完美地体现了压力无关性。施加纯[静水压力](@entry_id:275365)（$\boldsymbol{\sigma} = -p\mathbf{I}$）时，[偏应力张量](@entry_id:267642) $\mathbf{s}$ 为零，故 $\sigma_{eq}=0$，永远不会导致屈服 。

在三维[主应力空间](@entry_id:184388) $(\sigma_1, \sigma_2, \sigma_3)$ 中，方程 $\sigma_{eq} = \sigma_y$ 描述了一个几何[曲面](@entry_id:267450)——[屈服面](@entry_id:175331)。由于其不依赖于[静水压力](@entry_id:275365) $p = -(\sigma_1+\sigma_2+\sigma_3)/3$，该[曲面](@entry_id:267450)是一个以静水压力轴（即直线 $\sigma_1=\sigma_2=\sigma_3$）为中心轴的无限长圆柱体 。这个圆柱面的一个至关重要的特性是其**[光滑性](@entry_id:634843)**——它没有任何[尖点](@entry_id:636792)或棱线。这与另一个经典的**[Tresca屈服准则](@entry_id:190718)**（[最大剪应力](@entry_id:181794)准则）形成鲜明对比，后者在[主应力空间](@entry_id:184388)中表现为一个正六角棱柱，其表面存在棱线和顶点。von Mises屈服面的光滑性保证了在屈服面上任意一点的法向都是唯一确定的，这对[流动法则](@entry_id:177163)具有深远的影响 。

### 相联[流动法则](@entry_id:177163)与Lévy-Mises方程

[流动法则](@entry_id:177163)（flow rule）建立了塑性[应变率](@entry_id:154778) $\dot{\boldsymbol{\varepsilon}}^p$ 与应力状态 $\boldsymbol{\sigma}$ 之间的关系。在塑性力学中，一个被广泛接受且具有深刻物理背景的法则是**相联流动法则**（associative flow rule），也称为**法向法则**（normality rule）。它假定塑性应变率的方向与屈服面在该应力点的外法线方向一致。数学上，这表示为：
$$ \dot{\boldsymbol{\varepsilon}}^p = \dot{\lambda} \frac{\partial f}{\partial \boldsymbol{\sigma}} $$
其中 $\dot{\lambda}$ 是一个非负的标量，称为塑性乘子率，它的大小决定了塑性流动的速率。

法向法则并非一个随意的假设。它可以从更基本的**[最大塑性耗散](@entry_id:184825)原理**（principle of maximum plastic dissipation）导出 [@problem_id:2654620, @problem_id:2654579]。该原理指出，对于一个给定的塑性[应变率](@entry_id:154778) $\dot{\boldsymbol{\varepsilon}}^p$，在所有满足屈服条件 $f(\boldsymbol{\sigma}^*) \le 0$ 的可能应力状态 $\boldsymbol{\sigma}^*$ 中，材料实际所处的应力状态 $\boldsymbol{\sigma}$ 使得塑性[功率耗散](@entry_id:264815) $\mathcal{D}^p = \boldsymbol{\sigma}:\dot{\boldsymbol{\varepsilon}}^p$ 达到最大值。将此表述为一个约束优化问题，并利用[Karush-Kuhn-Tucker](@entry_id:634966)（KKT）条件求解，可以直接得到相联[流动法则](@entry_id:177163)。这一原理为法向法则提供了坚实的[热力学](@entry_id:141121)和变分力学基础。从更现代的[凸分析](@entry_id:273238)角度看，这一关系可以被优雅地描述为塑性[应变率](@entry_id:154778)属于[屈服面](@entry_id:175331)在当前应力点处的法向锥，这等价于说耗散势是弹性域指示函数的[支撑函数](@entry_id:755667) 。

现在，我们将相联[流动法则](@entry_id:177163)应用于[von Mises屈服准则](@entry_id:174339)。首先计算[屈服函数](@entry_id:167970) $f = \sqrt{\frac{3}{2}\mathbf{s}:\mathbf{s}} - \sigma_y$ 对应力 $\boldsymbol{\sigma}$ 的梯度：
$$ \frac{\partial f}{\partial \boldsymbol{\sigma}} = \frac{\partial f}{\partial \mathbf{s}} : \frac{\partial \mathbf{s}}{\partial \boldsymbol{\sigma}} $$
通过链式法则可以证明 $\frac{\partial f}{\partial \boldsymbol{\sigma}} = \frac{3}{2\sigma_{eq}}\mathbf{s}$ 。代入相联流动法则，我们便得到了**Lévy-Mises方程**：
$$ \dot{\boldsymbol{\varepsilon}}^p = \dot{\lambda} \frac{3}{2\sigma_{eq}}\mathbf{s} $$
这是一个简洁而深刻的关系，它构成了[刚塑性流动](@entry_id:197608)理论的核心。该方程揭示了两个重要推论：

1.  **[塑性不可压缩性](@entry_id:183440)**（Plastic Incompressibility）：由于塑性应变率张量 $\dot{\boldsymbol{\varepsilon}}^p$ 与[偏应力张量](@entry_id:267642) $\mathbf{s}$ 成正比，而[偏应力张量](@entry_id:267642)的迹为零（$\text{tr}(\mathbf{s})=0$），因此塑性[应变率](@entry_id:154778)的迹也必然为零：
    $$ \text{tr}(\dot{\boldsymbol{\varepsilon}}^p) = \dot{\varepsilon}^p_{kk} = 0 $$
    这意味着在[von Mises塑性](@entry_id:185870)流动中，材料的体积是保持不变的。这与[金属塑性](@entry_id:176585)变形主要由晶体滑移（一种剪切过程）主导的物理机制相吻合 [@problem_id:2654568, @problem_id:2654555]。

2.  **[主轴](@entry_id:172691)共轴性**（Coaxiality）：Lévy-Mises方程表明，塑性应变率张量 $\dot{\boldsymbol{\varepsilon}}^p$ 与[偏应力张量](@entry_id:267642) $\mathbf{s}$ 的主轴方向是重合的。这意味着，材料在哪个方向上受到的偏应力最大，它也将在该方向上产生最大的塑性拉伸率。这一特性具有重要的实际意义。例如，如果我们通过实验测量了一个点处的应变率张量 $\dot{\boldsymbol{\varepsilon}}^p$ (在刚塑性模型中即为 $\mathbf{D}$)，我们就可以立即确定该点[偏应力张量](@entry_id:267642) $\mathbf{s}$ 的[主方向](@entry_id:276187)和主值之比，因为 $\mathbf{s}$ 与 $\dot{\boldsymbol{\varepsilon}}^p$ 成正比 。

### 能量耗散与等效量

为了量化塑性变形过程，我们引入了两个重要的标量：[等效应力](@entry_id:749064)和等效塑性应变率。它们之间的关系与能量耗散密切相关。单位体积的塑性功率耗散 $\mathcal{D}$ 定义为应力与塑性应变率的[内积](@entry_id:158127)：
$$ \mathcal{D} = \boldsymbol{\sigma}:\dot{\boldsymbol{\varepsilon}}^p $$
利用[应力分解](@entry_id:272862) $\boldsymbol{\sigma} = \mathbf{s} - p\mathbf{I}$ 和[塑性不可压缩性](@entry_id:183440) $\text{tr}(\dot{\boldsymbol{\varepsilon}}^p)=0$，上式可以简化为：
$$ \mathcal{D} = (\mathbf{s} - p\mathbf{I}):\dot{\boldsymbol{\varepsilon}}^p = \mathbf{s}:\dot{\boldsymbol{\varepsilon}}^p - p\,\text{tr}(\dot{\boldsymbol{\varepsilon}}^p) = \mathbf{s}:\dot{\boldsymbol{\varepsilon}}^p $$
这表明，[塑性耗散](@entry_id:201273)完全由[偏应力](@entry_id:163323)做功产生，[静水压力](@entry_id:275365)不做塑性功，这与[von Mises准则](@entry_id:164472)的压力无关性是一致的 。

为了使标量度量具有一致性，我们定义**等效塑性应变率** $\dot{\bar{\varepsilon}}^p$ 如下：
$$ \dot{\bar{\varepsilon}}^p = \sqrt{\frac{2}{3}\dot{\boldsymbol{\varepsilon}}^p:\dot{\boldsymbol{\varepsilon}}^p} $$
这个定义中的系数 $\sqrt{2/3}$ 经过精心选择，以确保在[单轴拉伸](@entry_id:188287)情况下，$\dot{\bar{\varepsilon}}^p$ 就等于轴向塑性[应变率](@entry_id:154778) $\dot{\varepsilon}_{11}^p$。

将Lévy-Mises方程代入 $\mathcal{D} = \mathbf{s}:\dot{\boldsymbol{\varepsilon}}^p$ 并结合 $\sigma_{eq}$ 和 $\dot{\bar{\varepsilon}}^p$ 的定义，可以推导出一个非常重要的关系 ：
$$ \mathcal{D} = \sigma_{eq}\dot{\bar{\varepsilon}}^p $$
这表明[等效应力](@entry_id:749064) $\sigma_{eq}$ 和等效塑性[应变率](@entry_id:154778) $\dot{\bar{\varepsilon}}^p$ 在能量上是**[功共轭](@entry_id:194957)**（work-conjugate）的。它们如同单轴情况下的应力和应变率，其乘积等于单位体积的[功率耗散](@entry_id:264815)。这个关系是建立更复杂的[硬化](@entry_id:177483)模型的基础。此外，通过这些定义还可以证明，对于 $f = \sigma_{eq} - \sigma_y$ 形式的[屈服函数](@entry_id:167970)，塑性乘子率 $\dot{\lambda}$ 恰好等于等效塑性应变率 $\dot{\bar{\varepsilon}}^p$ 。这使得Lévy-Mises方程可以被写成一种更常用的形式：
$$ \dot{\boldsymbol{\varepsilon}}^p = \frac{3}{2}\frac{\dot{\bar{\varepsilon}}^p}{\sigma_{eq}}\mathbf{s} $$

### 塑性流动的逻辑：加载与卸载

率无关塑性理论必须能够区分加载、卸载和中性加载。这一逻辑由一组被称为**[Karush-Kuhn-Tucker (KKT) 条件](@entry_id:176491)**的互补关系来描述 ：

1.  **屈服条件 (Primal Feasibility)**：$f(\boldsymbol{\sigma}) \le 0$。应力状态必须位于弹性域或其边界上。
2.  **流动速率非负 (Dual Feasibility)**：$\dot{\lambda} \ge 0$。塑性流动不可逆。
3.  **互补松弛条件 (Complementary Slackness)**：$\dot{\lambda} f(\boldsymbol{\sigma}) = 0$。

这三个条件完美地编码了塑性流动的开关机制。如果应力状态在[屈服面](@entry_id:175331)内部（$f  0$），则为了满足[互补条件](@entry_id:747558)，必须有 $\dot{\lambda} = 0$，即没有塑性流动。反之，如果发生[塑性流动](@entry_id:201346)（$\dot{\lambda} > 0$），则应力状态必须位于[屈服面](@entry_id:175331)上（$f = 0$）。

对于[理想塑性](@entry_id:753335)材料，当塑性流动发生时，应力点必须停留在屈服面上。这意味着[屈服函数](@entry_id:167970)的时间变化率必须为零，这被称为**[一致性条件](@entry_id:637057)**（consistency condition）：
$$ \dot{f} = \frac{\partial f}{\partial \boldsymbol{\sigma}} : \dot{\boldsymbol{\sigma}} = 0 \quad (\text{当 } \dot{\lambda} > 0) $$
该条件对应力率 $\dot{\boldsymbol{\sigma}}$ 施加了约束，确保在塑性加载过程中应力点不会“穿出”[屈服面](@entry_id:175331)。

### 完整模型及其适用性

综上所述，描述刚-[理想塑性](@entry_id:753335)材料在准静态、小变形下的流动的完整[方程组](@entry_id:193238)包括 ：
-   **平衡方程**: $\nabla \cdot \boldsymbol{\sigma} + \mathbf{b} = \mathbf{0}$
-   **[运动学](@entry_id:173318)关系**: $\dot{\boldsymbol{\varepsilon}} = \frac{1}{2}(\nabla \mathbf{v} + (\nabla \mathbf{v})^T)$
-   **[本构关系](@entry_id:186508) (Lévy-Mises)**: $\dot{\boldsymbol{\varepsilon}} = \dot{\lambda}\frac{3}{2\sigma_{eq}}\mathbf{s}$
-   **[不可压缩性](@entry_id:274914)**: $\nabla \cdot \mathbf{v} = 0$
-   **加载/卸载条件**: $f(\boldsymbol{\sigma}) \le 0, \dot{\lambda} \ge 0, \dot{\lambda}f(\boldsymbol{\sigma}) = 0$
-   **[一致性条件](@entry_id:637057)**: $\dot{\lambda}\dot{f}=0$

在这个体系中，静水压力 $p$ 的角色变得非常特殊。它不出现在[屈服准则](@entry_id:193897)或[流动法则](@entry_id:177163)中，其值由本构关系无法确定。实际上，$p$ 的作用类似于一个**拉格朗日乘子**，其值由平衡方程和[不可压缩性约束](@entry_id:750592) $\nabla \cdot \mathbf{v} = 0$ 共同决定 。

最后，我们必须清醒地认识到刚塑性模型是一种高度理想化的理论，其应用有明确的边界。在以下情况中，该模型会失效或变得不准确，需要采用更复杂的理论 ：

-   **[回弹](@entry_id:275734)（Springback）分析**：[回弹](@entry_id:275734)是卸载后弹性应变恢复导致的形状变化。刚塑性模型忽略了弹性应变，因此完全无法预测[回弹](@entry_id:275734)现象。此时必须使用[弹塑性](@entry_id:193198)模型。
-   **高[应变率](@entry_id:154778)动力学**：在冲击等问题中，应力波的传播至关重要。[波速](@entry_id:186208)由材料的[弹性模量](@entry_id:198862)和密度决定。刚塑性模型相当于假设弹性模量无穷大，导致[波速](@entry_id:186208)无穷大，无法描述波的传播和应力瞬态。
-   **大变形问题**：当应变或转动较大时（例如，[剪应变](@entry_id:175241)达到1），小应变理论不再适用。必须采用[有限应变运动学](@entry_id:168563)，并使用客观的应力率（如Jaumann率）来确保本构关系的物理客观性。
-   **体积变化分析**：刚塑性von Mises模型预测[体积守恒](@entry_id:276587)。如果需要分析由[静水压力](@entry_id:275365)引起的弹性体积变化（例如，高压下的密度变化），则必须考虑弹性应变。

然而，在许多[金属成形](@entry_id:188560)问题中，载荷是单调的，塑性应变远大于弹性应变（即 $\varepsilon^p \gg \sigma_y/E$）。在这些情况下，[刚塑性流动](@entry_id:197608)模型不仅能极大地简化计算，而且能够为力-位移响应和材料流动模式提供足够精确的预测，是[极限分析](@entry_id:188743)和[滑移线理论](@entry_id:184792)等经典方法的基石。