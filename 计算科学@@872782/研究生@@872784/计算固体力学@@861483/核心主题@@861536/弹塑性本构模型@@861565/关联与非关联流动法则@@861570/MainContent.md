## 引言
在[固体力学](@entry_id:164042)领域，理解材料如何从弹性变形过渡到永久的塑性变形是[结构设计](@entry_id:196229)与安全评估的基石。[塑性流动法则](@entry_id:189597)正是描述这一过程的核心演化规律，它规定了塑性应变产生的方向和速率。然而，一个关键的理论分岔点摆在了研究者面前：是应该采用与屈服条件内在关联的[流动法则](@entry_id:177163)，还是选择一个独立的、非关联的法则？

虽然关联[流动法则](@entry_id:177163)因其数学上的简洁性和坚实的[热力学](@entry_id:141121)基础而备受青睐，但它在描述土壤、岩石等重要工程材料的真实行为时却屡屡碰壁，暴露出理论与实验之间的知识鸿沟。解决这一矛盾，并理解在不同场景下选择何种法则及其带来的深远影响，是高级[计算固体力学](@entry_id:169583)研究的关键一环。

本文旨在系统性地剖析关联与[非关联流动法则](@entry_id:752544)。在“原理与机制”一章中，我们将深入其数学表述与[热力学](@entry_id:141121)根基。随后的“应用与[交叉](@entry_id:147634)学科联系”将展示这些法则如何在岩土工程、[金属成形](@entry_id:188560)及[失效分析](@entry_id:266723)等领域发挥作用。最后，“动手实践”部分将通过具体的计算问题，巩固理论知识。

我们将从最基本的原理出发，首先在下一章中揭示这两种流动法则背后的数学与物理机制。

## 原理与机制

在率无关塑性力学的框架内，塑性流动的大小和方向由一组称为[流动法则](@entry_id:177163)的[演化方程](@entry_id:268137)确定。本章旨在深入阐释这些法则背后的核心原理和机制，重点区分两种关键的[范式](@entry_id:161181)：**关联[流动法则](@entry_id:177163) (associative flow rule)** 和 **[非关联流动法则](@entry_id:752544) (non-associative flow rule)**。我们将从最广义的数学表述出发，探讨其[热力学](@entry_id:141121)基础、物理动机，最终分析其在计算力学中的深刻影响。

### 广义流动法则与关联性

在小应变、等温条件下，一个标准的[弹塑性](@entry_id:193198)[本构模型](@entry_id:174726)包含以下核心要素：一个定义了弹性域边界的**[屈服函数](@entry_id:167970) (yield function)** $f(\boldsymbol{\sigma}, \boldsymbol{\alpha})$，以及一个决定[塑性流动](@entry_id:201346)方向的**塑性势函数 (plastic potential)** $g(\boldsymbol{\sigma}, \boldsymbol{\alpha})$。其中，$\boldsymbol{\sigma}$ 是柯西应力张量，$\boldsymbol{\alpha}$ 是一组描述材料历史状态的内变量（例如硬化变量）。

塑性应变率 $\dot{\boldsymbol{\varepsilon}}^{p}$ 的演化由一个广义[流动法则](@entry_id:177163)给出：

$$
\dot{\boldsymbol{\varepsilon}}^{p} = \dot{\lambda} \frac{\partial g}{\partial \boldsymbol{\sigma}}
$$

在此方程中，$\dot{\lambda} \ge 0$ 是一个非负标量，称为**塑性乘子 (plastic multiplier)**。它是一个率类型的量，决定了塑性变形的“量值”或速率。当 $\dot{\lambda} > 0$ 时，材料发生塑性加载；当 $\dot{\lambda} = 0$ 时，材料处于弹性加载、卸载或中性加载状态。而张量 $\frac{\partial g}{\partial \boldsymbol{\sigma}}$ 是塑性势函数 $g$ 对应力 $\boldsymbol{\sigma}$ 的梯度，它定义了塑性应变率张量的“方向”。

[流动法则](@entry_id:177163)的**关联性 (associativity)** 是一个核心分类标准：

-   如果塑性[势函数](@entry_id:176105)与[屈服函数](@entry_id:167970)相同（或至多相差一个无关紧要的常数），即 $g = f$，则该[流动法则](@entry_id:177163)被称为 **关联流动法则**。
-   如果塑性势函数与[屈服函数](@entry_id:167970)不同，即 $g \neq f$，则该[流动法则](@entry_id:177163)被称为 **[非关联流动法则](@entry_id:752544)**。

#### 几何解释：正交流动法则

关联流动法则具有一个至关重要的几何解释。[屈服函数](@entry_id:167970) $f(\boldsymbol{\sigma}, \boldsymbol{\alpha}) = 0$ 在应力空间中定义了一个[曲面](@entry_id:267450)，即**屈服面 (yield surface)**。根据多元微[积分学](@entry_id:146293)的基本原理，函数 $f$ 的梯度 $\frac{\partial f}{\partial \boldsymbol{\sigma}}$ 在屈服面上的任意一点都与该点的[切平面](@entry_id:136914)正交，即指向屈服面的**外法线方向**。

因此，在关联塑性中 ($g=f$)，流动法则 $\dot{\boldsymbol{\varepsilon}}^{p} = \dot{\lambda} \frac{\partial f}{\partial \boldsymbol{\sigma}}$ 表明，塑性[应变率张量](@entry_id:266108) $\dot{\boldsymbol{\varepsilon}}^{p}$ 的方向始终与[屈服面](@entry_id:175331)正交。这便是著名的**正交[流动法则](@entry_id:177163) (normality rule)**。[@problem_id:3545021]

一个经典的例子是用于描述[金属塑性](@entry_id:176585)的 **von Mises [屈服准则](@entry_id:193897)**。其[屈服函数](@entry_id:167970)可以写为 $f = J_2 - k^2$，其中 $J_2 = \frac{1}{2}\boldsymbol{s}:\boldsymbol{s}$ 是应力偏量 $\boldsymbol{s}$ 的第二[不变量](@entry_id:148850)，$k$ 是与材料当前[屈服强度](@entry_id:162154)相关的参数。对应力 $\boldsymbol{\sigma}$ 求导可得 $\frac{\partial f}{\partial \boldsymbol{\sigma}} = \boldsymbol{s}$。因此，关联流动法则预测 $\dot{\boldsymbol{\varepsilon}}^{p} = \dot{\lambda} \boldsymbol{s}$。由于应力偏量的迹恒为零（$\text{tr}(\boldsymbol{s}) = 0$），这意味着塑性[体积应变率](@entry_id:272471)也为零：

$$
\text{tr}(\dot{\boldsymbol{\varepsilon}}^{p}) = \text{tr}(\dot{\lambda} \boldsymbol{s}) = \dot{\lambda} \, \text{tr}(\boldsymbol{s}) = 0
$$

这个结果表明，基于 von Mises 准则的关联塑性流动是**体积不可压缩的 (isochoric)**，即塑性变形不引起体积变化。这与大多数金属材料在塑性变形中的实验观察高度吻合。[@problem_id:3545015]

#### 推广至非光滑[屈服面](@entry_id:175331)：[凸分析](@entry_id:273238)视角

当[屈服面](@entry_id:175331)存在角点或棱线（例如 Tresca 或 Mohr-Coulomb [屈服面](@entry_id:175331)）时，其在这些点上是不可导的，经典的梯度定义失效。此时，需要借助**[凸分析](@entry_id:273238) (convex analysis)** 的工具来更严谨地定义正交性。

关联流动法则可以被更广义地表述为 $\dot{\boldsymbol{\varepsilon}}^{p}$ 属于[屈服点](@entry_id:188474) $\boldsymbol{\sigma}$ 处弹性域 $K$ 的**法向锥 (normal cone)** $N_K(\boldsymbol{\sigma})$。对于由凸函数 $f(\boldsymbol{\sigma}) \le 0$ 定义的凸弹性域 $K$，法向锥由 $f$ 在 $\boldsymbol{\sigma}$ 处的**[次微分](@entry_id:175641) (subdifferential)** $\partial f(\boldsymbol{\sigma})$ 的正[锥包](@entry_id:634790)生成。

- 在屈服面的光滑点，[次微分](@entry_id:175641) $\partial f(\boldsymbol{\sigma})$ 退化为包含唯一梯度向量 $\nabla f(\boldsymbol{\sigma})$ 的单点集，从而恢复经典的正交[流动法则](@entry_id:177163) $\dot{\boldsymbol{\varepsilon}}^p = \dot{\lambda} \nabla f(\boldsymbol{\sigma})$。[@problem_id:3545034]
- 在屈服面的角点，[次微分](@entry_id:175641)是所有活动[屈服函数](@entry_id:167970)分支梯度的凸包。例如，对于二维[应力空间](@entry_id:199156)中的[屈服函数](@entry_id:167970) $f(\boldsymbol{\sigma}) = \max\{\sigma_1 - \sigma_y, \sigma_2 - \sigma_y\}$，在角点 $\boldsymbol{\sigma}^\star = (\sigma_y, \sigma_y)$ 处，两个分支均处于活动状态，其梯度分别为 $(1,0)$ 和 $(0,1)$。因此，[次微分](@entry_id:175641)是这两个向量的凸包，即连接它们的线段 $\partial f(\boldsymbol{\sigma}^\star) = \text{co}\{(1,0), (0,1)\}$。关联[流动法则](@entry_id:177163)此时预测，塑性应变率 $\dot{\boldsymbol{\varepsilon}}^{p}$ 的方向可以是这两个法向的任意[凸组合](@entry_id:635830)，即 $\dot{\boldsymbol{\varepsilon}}^{p} \in \dot{\lambda} \, \text{co}\{(1,0), (0,1)\}$。几何上，这意味着塑性流动方向被限制在由两个活动[屈服面](@entry_id:175331)法向所张成的锥内。[@problem_id:3545034]

这种基于[凸分析](@entry_id:273238)的观点为正交流动法则提供了更深刻和普适的数学基础。

### 热力学原理

关联与[非关联流动法则](@entry_id:752544)的选择与热力学原理密切相关，特别是关于[塑性耗散](@entry_id:201273)的假设。

#### [最大塑性耗散](@entry_id:184825)原理

**[最大塑性耗散](@entry_id:184825)原理 (Principle of Maximum Plastic Dissipation)**，也称为 **Drucker 稳定性公设 (Drucker's stability postulate)**，为关联流动法则提供了坚实的理论基础。该原理断言，对于一个给定的塑性[应变率](@entry_id:154778) $\dot{\boldsymbol{\varepsilon}}^p$，材料真实的应力状态 $\boldsymbol{\sigma}$（位于[屈服面](@entry_id:175331)上）会使得[塑性耗散](@entry_id:201273)率 $\mathcal{D}_p = \boldsymbol{\sigma} : \dot{\boldsymbol{\varepsilon}}^p$ 达到最大值，即对于弹性域内的任何其他应力状态 $\boldsymbol{\sigma}^*$（$f(\boldsymbol{\sigma}^*) \le 0$），都满足以下不等式：

$$
(\boldsymbol{\sigma} - \boldsymbol{\sigma}^*) : \dot{\boldsymbol{\varepsilon}}^p \ge 0
$$

这个不等式在几何上意味着 $\dot{\boldsymbol{\varepsilon}}^p$ 必须位于弹性域在 $\boldsymbol{\sigma}$ 点的法向锥内。对于光滑的[凸屈服面](@entry_id:203690)，这直接导出了关联[流动法则](@entry_id:177163) $\dot{\boldsymbol{\varepsilon}}^p = \dot{\lambda} \frac{\partial f}{\partial \boldsymbol{\sigma}}$。因此，关联流动法则是满足[最大塑性耗散](@entry_id:184825)原理的必然结果。反之，任何[非关联流动法则](@entry_id:752544)（$g \neq f$）都必然违背此原理。[@problem_id:3545021]

#### 热力学第二定律与耗散非负性

[最大塑性耗散](@entry_id:184825)原理是一个比[热力学第二定律](@entry_id:142732)更强的假设。热力学第二定律（在等温条件下）仅要求**[塑性耗散](@entry_id:201273) (plastic dissipation)** 是非负的。在最简单的模型中（不考虑硬化能存储），这表现为 $\mathcal{D}_p = \boldsymbol{\sigma} : \dot{\boldsymbol{\varepsilon}}^p \ge 0$。

对于关联流动，如果屈服面是凸的且包含原点，这个条件通常是自动满足的。但对于[非关联流动](@entry_id:199220)，情况则更为微妙。耗散率为：

$$
\mathcal{D}_p = \boldsymbol{\sigma} : \dot{\boldsymbol{\varepsilon}}^p = \dot{\lambda} \left( \boldsymbol{\sigma} : \frac{\partial g}{\partial \boldsymbol{\sigma}} \right)
$$

由于 $\dot{\lambda} \ge 0$，耗散非负的要求转化为 $\boldsymbol{\sigma} : \frac{\partial g}{\partial \boldsymbol{\sigma}} \ge 0$。仅仅假设 $g$ 是[凸函数](@entry_id:143075)并不足以保证此条件对所有可能的应力状态都成立。[@problem_id:3545021]

考虑一个 Drucker-Prager 模型，其[屈服函数](@entry_id:167970)为 $f = \sqrt{J_2} + \alpha_f p - k=0$，塑性势为 $g = \sqrt{J_2} + \alpha_g p$（这里取压力 $p$ 为正）。可以证明，在[屈服面](@entry_id:175331)上，[耗散率](@entry_id:748577)可以表示为 $\mathcal{D}_p = \dot{\lambda} (k + (\alpha_g - \alpha_f)p)$。[@problem_id:3545065] 如果选择了一个不恰当的塑性势，例如 $\alpha_g$ 为负值，那么在高围压（大的正值 $p$）下，耗散 $\mathcal{D}_p$ 可能会变为负值。这将违反热力学第二定律，导致模型在物理上不可接受。[@problem_id:3545016] 因此，[非关联塑性](@entry_id:186531)势的选择必须受到[热力学一致性](@entry_id:138886)的严格约束，以确保在所有可行的塑性过程中耗散都是非负的。

### [非关联流动](@entry_id:199220)的物理动机：以摩擦材料为例

既然关联[流动法则](@entry_id:177163)具有坚实的理论基础，为何还需要引入更为复杂且可能存在理论隐患的非关联法则呢？答案在于，对于某些材料，特别是土壤、岩石、混凝土等**摩擦材料 (frictional materials)**，关联流动的预测与实验现象存在显著偏差。

这些材料的强度主要来源于颗粒间的摩擦，其屈服行为通常用 **Mohr-Coulomb** 或 **Drucker-Prager** 等压敏性准则来描述。在这类模型中，材料的[剪切强度](@entry_id:754762)与作用在其上的静水压力正相关，这一特性由**[内摩擦角](@entry_id:197521) (friction angle)** $\phi$ 来量化。

如果采用关联流动法则 ($g=f$)，那么[塑性流动](@entry_id:201346)方向将由[屈服函数](@entry_id:167970)梯度决定。对于摩擦材料，这意味着塑性变形过程中的体积变化——即**剪胀 (dilatancy)**——将直接由摩擦角 $\phi$ 控制。具体来说，$\phi$ 越大，模型预测的剪切过程中的体积膨胀就越大。然而，对密砂等材料的实验表明，尽管其[内摩擦角](@entry_id:197521) $\phi$ 可能很高（例如 $35^\circ$ 到 $45^\circ$），但其实际的剪胀要小得多。若强行使用关联法则，将会极大地高估材料的体积膨胀。[@problem_id:3545059]

为了解决这一矛盾，人们引入了[非关联流动法则](@entry_id:752544)。通过构造一个独立的塑性势函数 $g$，并引入一个**[剪胀角](@entry_id:748435) (dilation angle)** $\psi$ 来描述塑性[体积应变](@entry_id:267252)，使得 $g$ 的形式与 $f$ 相似但参数不同。选择一个远小于摩擦角的[剪胀角](@entry_id:748435)（$\psi  \phi$），便可以将材料的强度（由 $\phi$ 控制）与塑性流动行为（由 $\psi$ 控制）解耦。[@problem_id:3545059]

例如，在三轴[压缩试验](@entry_id:198777)下，对于一个摩擦角为 $\phi=30^\circ$ 的材料，关联模型（取 $\psi=\phi=30^\circ$）预测的塑性[体积应变率](@entry_id:272471)可能是等效塑性[剪切应变率](@entry_id:276945)的 $1.2$ 倍（方向为膨胀）。而如果采用一个更符合实际的[剪胀角](@entry_id:748435)，如 $\psi=10^\circ$ 的非关联模型，这一比值将大幅下降至约 $0.37$。这清晰地展示了非关联法则在定量描述真实材料行为方面的优势。[@problem_id:3545052]

此外，非关联性对于模拟摩擦材料更复杂的行为至关重要：
- **[压实](@entry_id:161543)行为**：对于松散的砂土，剪切过程可能伴随着体积减小（塑性压实）。这可以通过选取一个负的[剪胀角](@entry_id:748435) ($\psi  0$) 来模拟。[@problem_id:3545059]
- **临界状态**：大量实验表明，摩擦材料在经历大剪切变形后会趋向于一个**[临界状态](@entry_id:160700) (critical state)**，在该状态下，材料可以在体积不变的情况下持续剪切。这意味着塑性[体积应变率](@entry_id:272471)为零，对应于 $\psi=0$。然而，此时材料依然具有不可忽略的[剪切强度](@entry_id:754762)，即临界状态摩擦角 $\phi_{cs} > 0$。关联模型（$\psi=\phi$）无法描述这种状态（除非强度为零），而非关联模型则可以自然地通过让[剪胀角](@entry_id:748435) $\psi$ 随塑性应变累积而演化至零，同时保持摩擦角 $\phi$ 为一正值，从而完美捕捉到这一关键现象。[@problem_id:3545059]

### 在[计算塑性力学](@entry_id:171377)中的影响

关联性与非关联性的选择，对[弹塑性](@entry_id:193198)模型的数值实现和[计算效率](@entry_id:270255)有着决定性的影响。其核心在于对**[弹塑性](@entry_id:193198)[切线](@entry_id:268870)算子 (elasto-plastic tangent operator)** $\mathbb{C}^{ep}$ 的影响，该算子描述了应力率与总应变率之间的关系 $\text{d}\boldsymbol{\sigma} = \mathbb{C}^{ep} : \text{d}\boldsymbol{\varepsilon}$。

在塑性加载过程中，塑性乘子 $\dot{\lambda}$ 的值由**一致性条件 (consistency condition)** $\dot{f}=0$ 确定，即在塑性流动期间应力点必须保持在[屈服面](@entry_id:175331)上。通过求解一致性条件，可以推导出 $\dot{\lambda}$ 的表达式：

$$
\dot{\lambda} = \frac{\frac{\partial f}{\partial \boldsymbol{\sigma}} : \mathbb{C} : \dot{\boldsymbol{\varepsilon}}}{\frac{\partial f}{\partial \boldsymbol{\sigma}} : \mathbb{C} : \frac{\partial g}{\partial \boldsymbol{\sigma}} + H'}
$$

其中 $\mathbb{C}$ 是[弹性刚度张量](@entry_id:170728)，$H'$ 是广义硬化模量。[@problem_id:3545011] 将此表达式代回，可以得到[切线](@entry_id:268870)算子的通用形式：

$$
\mathbb{C}^{ep} = \mathbb{C} - \frac{(\mathbb{C} : \frac{\partial g}{\partial \boldsymbol{\sigma}}) \otimes (\frac{\partial f}{\partial \boldsymbol{\sigma}} : \mathbb{C})}{H' + \frac{\partial f}{\partial \boldsymbol{\sigma}} : \mathbb{C} : \frac{\partial g}{\partial \boldsymbol{\sigma}}}
$$

其中 $\otimes$ 表示张量积。[@problem_id:3545025]

#### 对称性及其后果

[切线](@entry_id:268870)算子的一个关键性质是其**主对称性 (major symmetry)**，即 $C^{ep}_{ijkl} = C^{ep}_{klij}$。

- **关联流动 ($g=f$)**：此时，$\frac{\partial g}{\partial \boldsymbol{\sigma}} = \frac{\partial f}{\partial \boldsymbol{\sigma}}$。由于[弹性张量](@entry_id:170728) $\mathbb{C}$ 具有主对称性，上述表达式中的分子变为 $(\mathbb{C} : \frac{\partial f}{\partial \boldsymbol{\sigma}}) \otimes (\frac{\partial f}{\partial \boldsymbol{\sigma}} : \mathbb{C})$，这是一个对称的张量积。因此，整个 $\mathbb{C}^{ep}$ 算子保持了**主对称性**。[@problem_id:3545021]

- **[非关联流动](@entry_id:199220) ($g \neq f$)**：此时，流动方向 $\frac{\partial g}{\partial \boldsymbol{\sigma}}$ 与屈服面法向 $\frac{\partial f}{\partial \boldsymbol{\sigma}}$ 不一致。这导致分子中的张量积 $(\mathbb{C} : \frac{\partial g}{\partial \boldsymbol{\sigma}}) \otimes (\frac{\partial f}{\partial \boldsymbol{\sigma}} : \mathbb{C})$ 失去了对称性。因此，$\mathbb{C}^{ep}$ 算子变为**非对称**的。[@problem_id:3545025]

这一对称性的丧失是采用非关联模型最主要的计算代价。在有限元分析中，[全局刚度矩阵](@entry_id:138630)是由[单元刚度矩阵](@entry_id:139369)组装而成，而后者是通过对 $\mathbb{C}^{ep}$（或其离散化的形式——**一致性[切线](@entry_id:268870)算子**）进行积分得到的。因此，一个非对称的本构[切线](@entry_id:268870)算子将导致一个**非对称的[全局刚度矩阵](@entry_id:138630)**。

这对求解[非线性有限元](@entry_id:173184)[方程组](@entry_id:193238)的[迭代算法](@entry_id:160288)选择有直接影响：
- 对于对称、正定的系统，可以采用高效的**共轭梯度法 (Conjugate Gradient, CG)**。
- 对于非对称系统，则必须使用更通用但通常计算成本更高、内存消耗更大的求解器，例如**[广义最小残差法](@entry_id:139566) (GMRES)** 或**[稳定双共轭梯度法](@entry_id:634145) (BiCGSTAB)**。[@problem_id:3545025]

此外，非对称性还与更深层次的稳定性问题相关。关联塑性模型通常能保证[材料稳定性](@entry_id:183933)（满足[Drucker公设](@entry_id:180546)）和边值问题[解的唯一性](@entry_id:143619)。而非关联模型则可能在加载的早期就失去[材料稳定性](@entry_id:183933)或导致解的非唯一性，给数值模拟带来更大挑战。[@problem_id:3545045]

### 硬化变量的影响

在更复杂的模型中，[屈服函数](@entry_id:167970)和塑性势函数还可能依赖于硬化内变量。区分两种主要的[硬化](@entry_id:177483)类型非常重要：

- **[各向同性硬化](@entry_id:164486) (Isotropic Hardening)**：通常由一个标量内变量（如等效塑性应变 $\kappa$）描述，它控制屈服面的均匀放大或缩小。例如，$f(\boldsymbol{\sigma}, \kappa) = \phi(\boldsymbol{\sigma}) - R(\kappa)$。由于硬化项 $R(\kappa)$ 不直接依赖于应力 $\boldsymbol{\sigma}$，它在对 $\boldsymbol{\sigma}$ 求导时会消失。因此，[各向同性硬化](@entry_id:164486)改变了[屈服面](@entry_id:175331)的大小，但**不改变**流动方向的梯度 $\frac{\partial g}{\partial \boldsymbol{\sigma}}$。[@problem_id:3545072]

- **[随动硬化](@entry_id:172077) (Kinematic Hardening)**：通常由一个[二阶张量](@entry_id:199780)内变量——**背应力 (back-stress)** $\boldsymbol{\alpha}$——来描述，它控制屈服面在[应力空间](@entry_id:199156)中的平移。屈服条件通常表示为[有效应力](@entry_id:198048) $\boldsymbol{\sigma}' = \boldsymbol{\sigma} - \boldsymbol{\alpha}$ 的函数，例如 $f(\boldsymbol{\sigma}, \boldsymbol{\alpha}) = \phi(\boldsymbol{\sigma} - \boldsymbol{\alpha}) - \sigma_y$。在这种情况下，[背应力](@entry_id:198105) $\boldsymbol{\alpha}$ 会出现在对 $\boldsymbol{\sigma}$ 的导数中。因此，[随动硬化](@entry_id:172077)**会改变**[塑性流动](@entry_id:201346)的方向，无论是在关联模型还是非关联模型中。[@problem_id:3545072]

综上所述，关联与[非关联流动法则](@entry_id:752544)的选择，是在深刻的理论原理、确凿的实验证据和严峻的计算现实之间进行权衡的结果。关联[流动法则](@entry_id:177163)以其优雅的理论结构和良好的数值特性而备受青睐，而[非关联流动法则](@entry_id:752544)则为精确模拟特定材料（尤其是摩擦材料）的复杂物理行为提供了不可或缺的工具，尽管其代价是增加了模型的复杂性和计算的挑战性。