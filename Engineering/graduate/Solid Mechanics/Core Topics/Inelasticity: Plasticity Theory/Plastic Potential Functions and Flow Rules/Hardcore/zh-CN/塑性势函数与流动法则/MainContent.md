## 引言
在固体力学领域，理解材料在载荷作用下如何从弹性变形过渡到永久的塑性变形是工程设计与安全分析的基石。屈服准则，如von Mises或[Tresca准则](@entry_id:167002)，成功地界定了材料保持弹性的应力边界，回答了塑性“何时”开始的问题。然而，这仅仅是故事的一半。一个更为关键的问题是：一旦塑性变形发生，其演化的方向和模式是怎样的？仅凭[屈服函数](@entry_id:167970)，我们无法预测材料将如何流动，这构成了一个关键的知识缺口。

本文旨在系统性地填补这一缺口，深入探讨决定塑性流动方向的核心概念——塑性[势函数](@entry_id:176105)及与之相伴的[流动法则](@entry_id:177163)。我们将带领读者穿越[弹塑性](@entry_id:193198)理论的深层结构，揭示其背后深刻的物理原理与精妙的数学表述。

在“原理与机制”一章中，我们将从最基本的概念出发，厘清[屈服函数](@entry_id:167970)与塑性[势函数](@entry_id:176105)的不同角色，并基于[最大塑性耗散](@entry_id:184825)原理解释关联[流动法则](@entry_id:177163)的物理起源。随后，我们将探讨为何以及如何在[非关联流动法则](@entry_id:752544)中将强度与变形[解耦](@entry_id:637294)，以更精确地模拟土壤、岩石等复杂材料。

接着，在“应用与跨学科联系”一章中，我们会将这些理论应用于实际，展示它们如何用于解释和预测金属的各向异性、岩土的压力敏感性与[剪胀性](@entry_id:201001)，甚至连接到微观尺度上的晶体滑移与损伤机制。

最后，通过“动手实践”部分提供的计算练习，读者将有机会将理论知识转化为解决具体问题的能力，真正掌握这一强大的分析工具。本文将为您构建一个关于塑性流动的完整知识体系，从理论基础到前沿应用，助您在学术研究与工程实践中更进一步。

## 原理与机制

在[弹塑性力学](@entry_id:193198)中，仅通过[屈服函数](@entry_id:167970)来判断材料何时进入塑性状态是不足够的。我们还需要一个[本构关系](@entry_id:186508)来描述一旦发生塑性变形，其演化的方向和大小。本章将深入探讨决定塑性流动方向的核心概念——塑性[势函数](@entry_id:176105)，以及与之相关的[流动法则](@entry_id:177163)。我们将从最基本的原理出发，阐述关联流动与[非关联流动](@entry_id:199220)的物理意义、数学表述及其在工程实践中的应用。

### 塑性流动的方向：[屈服函数](@entry_id:167970)与塑性势

[屈服函数](@entry_id:167970) $f(\boldsymbol{\sigma}, \boldsymbol{\alpha}, \kappa)$ 界定了[应力空间](@entry_id:199156)中的弹性区域。当应力状态 $\boldsymbol{\sigma}$ 满足 $f \le 0$ 时，材料处于弹性状态或即将屈服。其中，$\boldsymbol{\alpha}$ 是代表[运动硬化](@entry_id:172077)的背应力张量，$\kappa$ 是代表[各向同性硬化](@entry_id:164486)的标量内禀变量。当应力路径触及[屈服面](@entry_id:175331)，即 $f=0$ 时，塑性变形便可能发生。然而，[屈服函数](@entry_id:167970)本身只提供了一个“开关”——它告诉我们塑性变形“何时”发生，但并未指明塑性应变增量 $\mathrm{d}\boldsymbol{\varepsilon}^{p}$ 的“方向”。

为了完整描述塑性行为，我们需要引入第二个关键函数，即**塑性势函数** $g(\boldsymbol{\sigma}, \boldsymbol{\alpha}, \kappa)$。塑性理论假设塑性应变增量的方向由塑性势函数 $g$ 在[应力空间](@entry_id:199156)的梯度确定。这一假设被称为**[流动法则](@entry_id:177163)** (flow rule)，其数学表达式为：
$$
\mathrm{d}\boldsymbol{\varepsilon}^{p} = \mathrm{d}\lambda \, \frac{\partial g}{\partial \boldsymbol{\sigma}}
$$
其中，$\mathrm{d}\lambda \ge 0$ 是一个非负的标量，称为**塑性乘子**，它表示塑性变形的量值。当 $\mathrm{d}\lambda > 0$ 时，发生塑性加载；当 $\mathrm{d}\lambda = 0$ 时，则为弹性加载或卸载。

这个法则具有清晰的几何意义：塑性应变增量 $\mathrm{d}\boldsymbol{\varepsilon}^{p}$ 的方向与塑性[势函数](@entry_id:176105) $g$ 的[等值面](@entry_id:196027)在当前应力点 $\boldsymbol{\sigma}$ 的外[法线](@entry_id:167651)方向相同。因此，流动法则是决定塑性变形模式的核心。

综上所述，[屈服函数](@entry_id:167970) $f$ 和塑性[势函数](@entry_id:176105) $g$ 扮演着截然不同的角色 ：
1.  **[屈服函数](@entry_id:167970) $f$**：定义了[弹性极限](@entry_id:186242)。其核心作用是通过 **[Karush-Kuhn-Tucker](@entry_id:634966) (KKT) 加载/卸载条件** ($f \le 0$, $\mathrm{d}\lambda \ge 0$, $\mathrm{d}\lambda f = 0$) 来判断[塑性流动](@entry_id:201346)是否被激活。
2.  **塑性势函数 $g$**：定义了[塑性流动](@entry_id:201346)的方向。一旦[塑性流动](@entry_id:201346)被激活（即 $\mathrm{d}\lambda > 0$），塑性应变增量的方向就由 $g$ 的梯度 $\frac{\partial g}{\partial \boldsymbol{\sigma}}$ 唯一确定。

### 关联流动法则与[最大塑性耗散](@entry_id:184825)原理

一个自然的问题是：塑性[势函数](@entry_id:176105) $g$ 和[屈服函数](@entry_id:167970) $f$ 之间是否存在某种关系？在[经典塑性理论](@entry_id:167389)中，这一关系由一个重要的物理原理——**[最大塑性耗散](@entry_id:184825)原理** (principle of maximum plastic dissipation) 所确立。该原理由 Drucker 提出，因此也称为 Drucker 公设。其基本内容是：在一个塑性变形过程中，对于给定的塑性应变增量，真实的应力状态在所有可能的许应力状态中，使得[塑性耗散](@entry_id:201273)功率达到最大值。

对于一个处于屈服状态的应力点 $\boldsymbol{\sigma}$ (即 $f(\boldsymbol{\sigma})=0$)，以及弹性域内的任意其他许应力点 $\boldsymbol{\sigma}^{*}$ (即 $f(\boldsymbol{\sigma}^{*}) \le 0$)，该原理可以表述为：
$$
(\boldsymbol{\sigma} - \boldsymbol{\sigma}^{*}) : \mathrm{d}\boldsymbol{\varepsilon}^{p} \ge 0
$$
将流动法则 $\mathrm{d}\boldsymbol{\varepsilon}^{p} = \mathrm{d}\lambda \, \frac{\partial g}{\partial \boldsymbol{\sigma}}$ 代入上式，并考虑到 $\mathrm{d}\lambda > 0$，我们得到：
$$
(\boldsymbol{\sigma} - \boldsymbol{\sigma}^{*}) : \frac{\partial g}{\partial \boldsymbol{\sigma}} \ge 0
$$
这一不等式在[凸分析](@entry_id:273238)中具有明确的几何意义。如果弹性域 $\lbrace \boldsymbol{\tau} \mid f(\boldsymbol{\tau}) \le 0 \rbrace$ 是一个凸集，那么上述不等式意味着向量 $\frac{\partial g}{\partial \boldsymbol{\sigma}}$ 必须指向屈服面 $f=0$ 在 $\boldsymbol{\sigma}$ 点的外[法线](@entry_id:167651)方向。[屈服面](@entry_id:175331)的外法线方向由 $\frac{\partial f}{\partial \boldsymbol{\sigma}}$ 给出。因此，为了满足[最大塑性耗散](@entry_id:184825)原理，$\frac{\partial g}{\partial \boldsymbol{\sigma}}$ 的方向必须与 $\frac{\partial f}{\partial \boldsymbol{\sigma}}$ 的方向相同。

这意味着，在不失一般性的情况下，我们可以选择塑性[势函数](@entry_id:176105)与[屈服函数](@entry_id:167970)完全相同，即 $g=f$。这种特殊情况被称为**关联流动法则** (associated flow rule) 。

$$
\mathrm{d}\boldsymbol{\varepsilon}^{p} = \mathrm{d}\lambda \, \frac{\partial f}{\partial \boldsymbol{\sigma}} \quad (\text{关联流动法则})
$$

这个结论揭示了屈服面**[凸性](@entry_id:138568)** (convexity) 的重要性。对于采用关联流动法则的材料模型，屈服面的[凸性](@entry_id:138568)是保证 Drucker 稳定性和增量问题[解的唯一性](@entry_id:143619)的前提条件 。一个非凸的屈服面与关联流动法则结合，可能导致材料在某些加载路径下出现不稳定行为，这在物理上是不合理的。

### [非关联流动法则](@entry_id:752544)及其应用

尽管关联流动法则在理论上具有优雅性和简单性，但大量实验表明，许多材料（尤其是压力相关的摩擦性材料，如土壤、岩石和混凝土）的塑性行为并不遵循此法则。最典型的偏差在于**[剪胀性](@entry_id:201001)** (dilatancy)，即材料在剪切作用下发生体积膨胀的现象。

对于一个压力相关的[屈服函数](@entry_id:167970) $f$（例如，Drucker-Prager 或 Mohr-Coulomb 模型），其对压力的导数 $\frac{\partial f}{\partial p}$ (其中 $p = \frac{1}{3}\mathrm{tr}(\boldsymbol{\sigma})$) 不为零。如果采用关联[流动法则](@entry_id:177163)，塑性[体积应变率](@entry_id:272471) $\dot{\varepsilon}_{v}^{p} = \mathrm{tr}(\dot{\boldsymbol{\varepsilon}}^{p}) = \dot{\lambda} \, \mathrm{tr}(\frac{\partial f}{\partial \boldsymbol{\sigma}})$ 也将不为零，这预测了剪胀的发生。然而，实验测得的剪胀值往往远小于由关联流动法则预测的值。

为了更准确地描述这类材料的行为，人们引入了**[非关联流动法则](@entry_id:752544)** (non-associated flow rule)，即选择一个与[屈服函数](@entry_id:167970)不同的塑性[势函数](@entry_id:176105) $g \neq f$ 。通过这种方式，材料的强度特性（由 $f$ 控制）和变形特性（由 $g$ 控制）可以被[解耦](@entry_id:637294)。

一个经典的例子是岩[土力学](@entry_id:180264)中的应用 。我们可以使用更精确地描述强度的 **Mohr-Coulomb 屈服准则**作为 $f$，它与材料的**[内摩擦角](@entry_id:197521)** $\varphi$ 相关。同时，选用一个形式上更简单的 **Drucker-Prager 函数**作为塑性势 $g$，并引入一个独立的**[剪胀角](@entry_id:748435)** $\psi$。塑性[势函数](@entry_id:176105)可以写成 $g(p, J_2) = \sqrt{J_2} + \beta p$，其中 $J_2$ 是[偏应力张量](@entry_id:267642)的第二[不变量](@entry_id:148850)。参数 $\beta$ 与[剪胀角](@entry_id:748435) $\psi$ 相关，例如 $\beta = \frac{2}{\sqrt{3}}\sin\psi$。通过流动法则，可以推导出塑性[体积应变率](@entry_id:272471)与等效塑性[剪切应变率](@entry_id:276945)之比为：
$$
\frac{\dot{\varepsilon}_{v}^{p}}{\dot{\varepsilon}_{q}^{p}} = 2\sin\psi
$$
在关联流动中，$\psi=\varphi$。而在[非关联流动](@entry_id:199220)中，通过实验数据选择一个较小的[剪胀角](@entry_id:748435) $\psi  \varphi$，就可以显著降低模型预测的剪胀效应，从而与实际观测吻合。当 $\psi = 0$ 时，$\dot{\varepsilon}_{v}^{p}=0$，表示[塑性流动](@entry_id:201346)是体积不可压缩的。

需要强调的是，即使在[非关联塑性](@entry_id:186531)中，[热力学第二定律](@entry_id:142732)仍然必须满足，即[塑性耗散](@entry_id:201273) $\mathcal{D} = \boldsymbol{\sigma}:\dot{\boldsymbol{\varepsilon}}^{p} \ge 0$。只要塑性势函数 $g$ 是应力的[凸函数](@entry_id:143075)，并且满足一些温和的条件，这个[耗散不等式](@entry_id:188634)通常都能得到保证。然而，[非关联流动](@entry_id:199220)通常会违反 Drucker 公设，这会导致在数值计算中[算法切线模量](@entry_id:199979)失去主对称性，并对[边值问题](@entry_id:193901)[解的唯一性](@entry_id:143619)分析带来挑战 。

### 非光滑[屈服面](@entry_id:175331)上的[流动法则](@entry_id:177163)

许多经典的[屈服准则](@entry_id:193897)，如 Tresca 和 Mohr-Coulomb，其屈服面在[主应力空间](@entry_id:184388)中是[多面体](@entry_id:637910)，包含尖锐的**角点** (corners) 和**棱边** (edges)。在这些非光滑点上，函数的梯度没有唯一定义，因此经典的[流动法则](@entry_id:177163) $\mathrm{d}\boldsymbol{\varepsilon}^{p} = \mathrm{d}\lambda \, \nabla g$ 失效。

为了处理这种情况，我们需要借助[凸分析](@entry_id:273238)中的**[次微分](@entry_id:175641)** (subdifferential) 概念 。对于一个[凸函数](@entry_id:143075) $g$，其在点 $\boldsymbol{\sigma}$ 的[次微分](@entry_id:175641) $\partial g(\boldsymbol{\sigma})$ 是一个向量集合，其中每个向量 $\mathbf{n}$ (称为[次梯度](@entry_id:142710)) 都满足以下不等式：
$$
g(\boldsymbol{\tau}) \ge g(\boldsymbol{\sigma}) + \mathbf{n}:(\boldsymbol{\tau}-\boldsymbol{\sigma}), \quad \forall \boldsymbol{\tau}
$$
几何上，[次微分](@entry_id:175641) $\partial g(\boldsymbol{\sigma})$ 对应于屈服域在 $\boldsymbol{\sigma}$ 点的**法向锥** (normal cone)。
*   在光滑点，法向锥只包含一个向量，即标准意义下的梯度 $\nabla g$。
*   在棱边或角点，法向锥则包含无穷多个向量，它们是由相邻光滑面的法[向量张成](@entry_id:152883)的[凸集](@entry_id:155617)。例如，在一个角点处，法向锥是所有与该角点相邻的光滑[面法向量](@entry_id:749211)的非负线性组合。

利用[次微分](@entry_id:175641)，流动法则被推广为一个包含关系，称为**广义流动法则**：
$$
\mathrm{d}\boldsymbol{\varepsilon}^{p} \in \mathrm{d}\lambda \, \partial g(\boldsymbol{\sigma})
$$
这意味着塑性应变增量的方向可以是法向锥内的任意一个方向。例如，对于 Tresca [屈服准则](@entry_id:193897)（在偏平面上为正六边形），其关联流动法则在六边形的顶点处，允许[塑性流动](@entry_id:201346)方向介于相邻两个面法线之间的任何方向 。这为处理多轴加载下复杂的塑性流动提供了理论基础。在数值计算中，这种情况对应于应力点返回到[屈服面](@entry_id:175331)的一个顶点，此时多个屈服面被同时激活  。

### [硬化](@entry_id:177483)模型与流动法则的耦合

塑性模型通常需要包含[硬化](@entry_id:177483)效应，即材料在塑性变形后屈服强度发生变化的现象。这通过演化的内禀变量来实现，主要分为[各向同性硬化](@entry_id:164486)和[运动硬化](@entry_id:172077)。

*   **[各向同性硬化](@entry_id:164486)** (Isotropic Hardening) 由标量内禀变量 $\kappa$ 描述，它导致屈服面在保持形状和中心位置不变的情况下均匀地扩大或缩小。在[屈服函数](@entry_id:167970) $f(\boldsymbol{\sigma}-\boldsymbol{\alpha}, \kappa) = \Phi(\boldsymbol{\sigma}-\boldsymbol{\alpha}) - R(\kappa) - \sigma_{y}$ 中，它通过 $R(\kappa)$ 项体现。
*   **[运动硬化](@entry_id:172077)** (Kinematic Hardening) 由背[应力张量](@entry_id:148973) $\boldsymbol{\alpha}$ 描述，它导致屈服面在[应力空间](@entry_id:199156)中平移，而不改变其形状和大小。这在[屈服函数](@entry_id:167970)中通过有效应力 $\boldsymbol{\sigma}-\boldsymbol{\alpha}$ 体现。

在一个通用的非关联框架中，如果塑性势函数 $g$ 被假设为仅与应力 $\boldsymbol{\sigma}$ 相关，即 $g = g(\boldsymbol{\sigma})$，那么流动方向 $\frac{\partial g}{\partial \boldsymbol{\sigma}}$ 将不依赖于任何硬化变量（无论是 $\kappa$ 还是 $\boldsymbol{\alpha}$）。这意味着，屈服面的扩大或平移本身并不直接改变[塑性流动](@entry_id:201346)的方向 。

然而，硬化状态深刻地影响着[塑性流动](@entry_id:201346)的**量值**，即塑性乘子 $\mathrm{d}\lambda$ 的大小。这通过下一节将要讨论的一致性条件来实现。

### [塑性流动](@entry_id:201346)的量值：[一致性条件](@entry_id:637057)

我们已经确定了塑性流动的方向，现在需要确定其大小 $\mathrm{d}\lambda$。在率无关塑性中，如果发生塑性加载，应力点必须停留在不断演化的屈服面上。这一条件被称为**塑性[一致性条件](@entry_id:637057)** (plastic consistency condition)，数学上表示为 $\mathrm{d}f=0$。

我们可以利用[链式法则](@entry_id:190743)将 $\mathrm{d}f=0$ 展开：
$$
\mathrm{d}f = \frac{\partial f}{\partial \boldsymbol{\sigma}} : \mathrm{d}\boldsymbol{\sigma} + \frac{\partial f}{\partial \boldsymbol{\alpha}} : \mathrm{d}\boldsymbol{\alpha} + \frac{\partial f}{\partial \kappa} \mathrm{d}\kappa = 0
$$
这是一个求解 $\mathrm{d}\lambda$ 的核心方程。我们将所有相关的[本构关系](@entry_id:186508)代入此方程：
1.  弹性定律：$\mathrm{d}\boldsymbol{\sigma} = \mathbb{C}_{\mathrm{e}} : (\mathrm{d}\boldsymbol{\varepsilon} - \mathrm{d}\boldsymbol{\varepsilon}^{p})$
2.  流动法则：$\mathrm{d}\boldsymbol{\varepsilon}^{p} = \mathrm{d}\lambda \, \frac{\partial g}{\partial \boldsymbol{\sigma}}$
3.  [硬化](@entry_id:177483)法则：例如，$\mathrm{d}\kappa = h \, \mathrm{d}\lambda$

将这些关系代入[一致性条件](@entry_id:637057)，经过一系列代数运算，我们可以解出塑性乘子 $\mathrm{d}\lambda$ ：
$$
\mathrm{d}\lambda = \frac{\frac{\partial f}{\partial \boldsymbol{\sigma}} : \mathbb{C}_{\mathrm{e}} : \mathrm{d}\boldsymbol{\varepsilon}}{H}
$$
其中，分母 $H$ 被称为广义塑性模量，其一般形式为：
$$
H = \frac{\partial f}{\partial \boldsymbol{\sigma}} : \mathbb{C}_{\mathrm{e}} : \frac{\partial g}{\partial \boldsymbol{\sigma}} - \frac{\partial f}{\partial \boldsymbol{\alpha}} : (\text{运动硬化项}) - \frac{\partial f}{\partial \kappa} (\text{各向同性硬化项})
$$
对于一个简单的[各向同性硬化](@entry_id:164486)模型 $\dot{\kappa} = h \dot{\lambda}$，其表达式为：
$$
H = \frac{\partial f}{\partial \boldsymbol{\sigma}} : \mathbb{C}_{\mathrm{e}} : \frac{\partial g}{\partial \boldsymbol{\sigma}} - h \frac{\partial f}{\partial \kappa}
$$
这个结果清晰地表明，塑性乘子 $\mathrm{d}\lambda$ 的大小取决于当前的应力状态、材料的弹性、屈服准则、流动法则以及硬化行为。[硬化](@entry_id:177483)（$H>0$）会使得分母增大，从而在相同的应变驱动下产生较小的塑性变形；而软化（$H0$）则会产生相反的效果 。

### 高等议题：稳定性与数值实现

最后，我们讨论与塑性势和流动法则相关的一些高级主题，这些主题在理论研究和计算实践中至关重要。

#### 稳定性与唯一性

如前所述，[非关联流动法则](@entry_id:752544) ($g \neq f$) 通常会违反 Drucker 公设。这导致了所谓的“非对称性”，即在数值计算中推导出的算法[切线刚度矩阵](@entry_id:170852) $\mathbb{C}_{ep}$ 失去了主对称性。这对[边值问题](@entry_id:193901)[解的唯一性](@entry_id:143619)证明构成了挑战。在材料出现**软化** ($H0$) 的情况下，问题尤为严重。此时，[声学张量](@entry_id:200089)可能失去正定性，导致控制方程失去椭圆性，从而引发[应变局部化](@entry_id:176973)（如[剪切带](@entry_id:183352)）等物理不稳定性，并使得数值解依赖于网格尺寸，出现非唯一解 。

#### 数值实现中的权衡

在非光滑屈服面（如 Tresca）的数值实现中，工程师面临一个重要的权衡 。
*   **方法一：光滑势近似**。一个常见的做法是采用非关联模型，即使用非光滑的 Tresca 函数作为[屈服函数](@entry_id:167970) $f$（以保证强度预测的准确性），但选择一个光滑的函数（如 von Mises 型函数）作为塑性势 $g$。这样做的主要优点是，流动方向 $\frac{\partial g}{\partial \boldsymbol{\sigma}}$ 始终是唯一且可微的。这保证了算法[切线[刚度矩](@entry_id:170852)阵](@entry_id:178659)的良好性质，使得基于[牛顿法](@entry_id:140116)的[返回映射算法](@entry_id:168456)能够保持二次收敛，从而提高计算的鲁棒性和效率。其代价是牺牲了物理上的精确性，特别是在屈服面角点附近的流动方向预测会与关联理论存在偏差。

*   **方法二：非光滑算法**。另一种更严谨的途径是坚持使用关联流动法则 ($g=f$)，并开发能够直接处理非光滑问题的先进[数值算法](@entry_id:752770)。这些算法包括基于[变分不等式](@entry_id:172788)的框架、主动集策略或[半光滑牛顿法](@entry_id:754689)。这些方法能够精确地模拟关联流动在角点和棱边的行为，保持了模型的物理保真度。然而，它们的实现复杂度远高于标准算法，且在角点处的[收敛速度](@entry_id:636873)可能从二次退化为超线性。

总之，塑性[势函数](@entry_id:176105)和流动法则的选择不仅是理论建模的核心，也深刻影响着计算力学方法的选择和最终结果的可靠性。理解其背后的原理、物理动机和数学工具，对于进行高水平的[固体力学](@entry_id:164042)研究和工程分析至关重要。