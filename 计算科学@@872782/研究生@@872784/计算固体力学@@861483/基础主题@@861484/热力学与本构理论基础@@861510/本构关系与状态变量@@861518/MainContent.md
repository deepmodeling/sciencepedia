## 引言
在[计算固体力学](@entry_id:169583)领域，准确预测材料在各种载荷和环境条件下的行为是工程设计与科学研究的基石。[本构关系](@entry_id:186508)，即描述材料[应力与应变](@entry_id:137374)之间关系的数学方程，是实现这一目标的核心。然而，随着对高性能材料和复杂物理现象（如大变形、塑性、损伤和多场耦合）研究的深入，如何构建既具有物理真实性又在计算上稳健的[本构模型](@entry_id:174726)，成为了一项巨大的挑战。这其中的关键在于理解并正确运用“[状态变量](@entry_id:138790)”这一概念，它为描述材料的内部[状态和](@entry_id:193625)历史依赖性提供了有力的工具。

本文旨在系统性地阐述基于[热力学](@entry_id:141121)和内部状态变量的现代理论框架，为构建复杂的材料本构模型提供一个统一而严谨的视角。通过学习本文，您将能够弥合纯理论概念与计算实践之间的鸿沟。

在**原理和机制**章节中，我们将从连续介质力学的基础出发，建立描述材料变形的[运动学](@entry_id:173318)框架，并强调材料框架无关性原理的重要性。随后，我们将深入探讨如何利用[热力学第二定律](@entry_id:142732)（克劳修斯-杜亨不等式）和亥姆霍兹自由能，为弹性和非弹性材料（如塑性、[粘弹性](@entry_id:148045)）系统地推导[本构方程](@entry_id:138559)和演化规律。

在**应用与跨学科联系**章节中，我们将展示该理论框架的强大适用性，探讨其如何被扩展应用于解决高级非弹性行为（如[循环塑性](@entry_id:176411)、[损伤演化](@entry_id:184965)）、[多物理场耦合](@entry_id:171389)问题（如热-力、流-固耦合）以及生物力学和多尺度建模等前沿领域中的实际问题。

最后，在**动手实践**部分，您将通过一系列精心设计的计算练习，将所学的理论知识付诸实践，加深对[超弹性](@entry_id:159356)、[亚弹性](@entry_id:204371)和耗散机制计算实现的理解。

让我们一同开启这段探索之旅，掌握构建先进材料模型的关键理论与方法。

## 原理和机制

本章旨在为本构关系和状态变量的现代理论奠定基础。在“引言”部分对连续介质力学的基本概念进行概述之后，我们将深入探讨描述材料行为的数学和物理框架。我们的目标是建立一套系统性的方法，用于构建能够准确预测材料在各种载荷和环境条件下响应的本构模型。我们将从变形[运动学](@entry_id:173318)的基本原理出发，引入[客观性原理](@entry_id:185412)，然后构建一个严格的[热力学](@entry_id:141121)框架，该框架不仅适用于弹性材料，也适用于存在能量耗散的复杂材料。最后，我们将探讨各项异性、[材料稳定性](@entry_id:183933)以及不同本构表述形式之间的微妙差别，为后续章节中具体的材料模型和计算实现打下坚实的基础。

### 运动学基础与材料框架无关性原理

任何本构理论的出发点都是对物体变形的精确数学描述。我们考虑一个连续体，其在某个选定的**参考构型** $\mathcal{B}_0$ 中占据空间区域。该构型中的物[质点](@entry_id:186768)由物质[坐标向量](@entry_id:153319) $\boldsymbol{X}$ 标记。物体的运动由一个映射 $\boldsymbol{\varphi}$ 描述，该映射将每个物[质点](@entry_id:186768) $\boldsymbol{X}$ 映射到其在当前时刻 $t$ 的空间位置 $\boldsymbol{x}$，即 $\boldsymbol{x} = \boldsymbol{\varphi}(\boldsymbol{X}, t)$。

描述局部变形的核心[运动学](@entry_id:173318)量是**变形梯度 (deformation gradient)** 张量 $\boldsymbol{F}$。它定义为空间位置 $\boldsymbol{x}$ 对物质坐标 $\boldsymbol{X}$ 的梯度：
$$
\boldsymbol{F} = \frac{\partial \boldsymbol{\varphi}(\boldsymbol{X}, t)}{\partial \boldsymbol{X}} \quad \text{或以分量形式写作} \quad F_{ij} = \frac{\partial x_i}{\partial X_j}
$$
变形梯度 $\boldsymbol{F}$ 是一个[二阶张量](@entry_id:199780)，它将参考构型中的一个无穷小物质线元 $d\boldsymbol{X}$ 映射到当前构型中的对应[线元](@entry_id:196833) $d\boldsymbol{x}$，即 $d\boldsymbol{x} = \boldsymbol{F} d\boldsymbol{X}$。因此，$\boldsymbol{F}$ 包含了关于局部拉伸、剪切和旋转的全部信息。

然而，$\boldsymbol{F}$ 本身并非描述材料应变的理想选择。为了构建一个只测量变形而不包含[刚体转动](@entry_id:191086)的[应变度量](@entry_id:755495)，我们考察线元长度的平方如何变化。在参考构型中，其长度平方为 $ds_0^2 = d\boldsymbol{X} \cdot d\boldsymbol{X}$。在当前构型中，其长度平方为 $ds^2 = d\boldsymbol{x} \cdot d\boldsymbol{x} = (\boldsymbol{F} d\boldsymbol{X}) \cdot (\boldsymbol{F} d\boldsymbol{X}) = d\boldsymbol{X} \cdot (\boldsymbol{F}^{\mathsf{T}} \boldsymbol{F}) d\boldsymbol{X}$。

这个推导引出了一个至关重要的张量——**[右柯西-格林张量](@entry_id:174156) (right Cauchy-Green tensor)** $\boldsymbol{C}$：
$$
\boldsymbol{C} = \boldsymbol{F}^{\mathsf{T}} \boldsymbol{F}
$$
张量 $\boldsymbol{C}$ 是一个对称正定张量，它完全在参考构型上定义。它度量了物质邻域内长度的平方如何变化，从而量化了纯变形。另一个与之密切相关的[应变度量](@entry_id:755495)是**[格林-拉格朗日应变张量](@entry_id:187745) (Green-Lagrange strain tensor)** $\boldsymbol{E}$，它直接度量了长度平方的变化量：
$$
\boldsymbol{E} = \frac{1}{2}(\boldsymbol{C} - \boldsymbol{I})
$$
其中 $\boldsymbol{I}$ 是单位张量。当变形为[刚体运动](@entry_id:193355)时，$\boldsymbol{F}$ 是一个[旋转张量](@entry_id:191990)，此时 $\boldsymbol{C} = \boldsymbol{F}^{\mathsf{T}} \boldsymbol{F} = \boldsymbol{I}$，因此 $\boldsymbol{E} = \boldsymbol{0}$。这证实了 $\boldsymbol{C}$ 和 $\boldsymbol{E}$ 确实是纯粹的[应变度量](@entry_id:755495)。

选择 $\boldsymbol{C}$ 和 $\boldsymbol{E}$ 而不是 $\boldsymbol{F}$ 作为[本构关系](@entry_id:186508)中的[应变度量](@entry_id:755495)，其更深层次的原因在于**材料框架无关性原理 (principle of material frame indifference)**，也称为**[客观性原理](@entry_id:185412) (principle of objectivity)**。该原理是一个基本物理公设，它要求材料的本构响应（如应力或储存的能量）不能依赖于观察者。一个观察者的变换可以通过在当前构型上叠加一个[刚体运动](@entry_id:193355)来数学地表示。考虑一个与原运动相关的、经过刚体旋转的新运动 $\boldsymbol{x}^*(\boldsymbol{X}, t) = \boldsymbol{Q}(t) \boldsymbol{x}(\boldsymbol{X}, t)$，其中 $\boldsymbol{Q}(t)$ 是一个不依赖于空间位置的正交[旋转张量](@entry_id:191990)（即 $\boldsymbol{Q}^{\mathsf{T}}\boldsymbol{Q}=\boldsymbol{I}$ 且 $\det\boldsymbol{Q}=1$）。

在这种观察者变换下，变形梯度变换为 $\boldsymbol{F}^* = \boldsymbol{Q}\boldsymbol{F}$。由于 $\boldsymbol{F}$ 的值依赖于观察者（通过 $\boldsymbol{Q}$），它不是一个客观的量。如果一个材料的能量储存函数 $\psi$ 直接依赖于 $\boldsymbol{F}$，即 $\psi = \hat{\psi}(\boldsymbol{F})$，那么 $\hat{\psi}(\boldsymbol{Q}\boldsymbol{F})$ 通常不等于 $\hat{\psi}(\boldsymbol{F})$，这意味着材料在旋转的[坐标系](@entry_id:156346)中看起来会有不同的行为，这在物理上是不可接受的。

现在，我们考察[右柯西-格林张量](@entry_id:174156) $\boldsymbol{C}$ 的变换规律：
$$
\boldsymbol{C}^* = (\boldsymbol{F}^*)^{\mathsf{T}} \boldsymbol{F}^* = (\boldsymbol{Q}\boldsymbol{F})^{\mathsf{T}} (\boldsymbol{Q}\boldsymbol{F}) = \boldsymbol{F}^{\mathsf{T}} \boldsymbol{Q}^{\mathsf{T}} \boldsymbol{Q} \boldsymbol{F} = \boldsymbol{F}^{\mathsf{T}} \boldsymbol{I} \boldsymbol{F} = \boldsymbol{C}
$$
张量 $\boldsymbol{C}$ 在观察者变换下保持不变。因此，$\boldsymbol{C}$ 是一个**客观**的张量。由于 $\boldsymbol{E}$ 只是 $\boldsymbol{C}$ 的线性函数，它同样是客观的。对于一个在拉格朗日（参考构型）框架下描述的**超弹性 (hyperelastic)** 材料，其[应变能函数](@entry_id:178435) $\psi$ 必须是一个客观的标量函数，因此它只能通过客观的[应变度量](@entry_id:755495)来依赖于变形。这意味着一个有效的本构律必须具有 $\psi = \hat{\psi}(\boldsymbol{C})$ 或等效地 $\psi = \bar{\psi}(\boldsymbol{E})$ 的形式。[@problem_id:3552867] [@problem_id:3552818]

### [本构建模](@entry_id:183370)的[热力学](@entry_id:141121)框架

物理上合理的本构关系必须遵守[热力学定律](@entry_id:202285)。对于连续介质，这些定律的局部形式——结合了[能量守恒](@entry_id:140514)（第一定律）和[熵增原理](@entry_id:142282)（第二定律）——可以被浓缩为**克劳修斯-杜亨不等式 (Clausius-Duhem inequality)**。这个不等式为所有可能的材料行为设置了严格的约束。

为了系统地应用这些约束，我们引入**[热力学状态](@entry_id:755916) (thermodynamic state)** 的概念。一个物质点的状态由一组**状态变量 (state variables)** 完全描述，这些变量的当前值足以唯一确定该点的所有[热力学性质](@entry_id:146047)（如应力、熵、能量）并预测其未来的演化。选择一组完备且最小的状态变量是[本构建模](@entry_id:183370)的核心任务。

我们首先引入**[亥姆霍兹自由能](@entry_id:136442) (Helmholtz free energy)** $\psi$（单位质量或单位参考体积的自由能）作为一个关键的**[热力学势](@entry_id:140516) (thermodynamic potential)**。假设 $\psi$ 是状态变量的函数。对于一个可逆的纯弹性材料，其状态完全由变形和温度决定。因此，其[状态向量](@entry_id:154607)可以取为 $(\boldsymbol{C}, T)$，其中 $T$ 是绝对温度，自由能为 $\psi = \hat{\psi}(\boldsymbol{C}, T)$。

应用**科尔曼-诺尔程序 (Coleman-Noll procedure)**，我们将 $\dot{\psi}$ 的链式法则表达式代入克劳修斯-杜亨不等式。由于该不等式必须对任意允许的[热力学过程](@entry_id:141636)（即任意的 $\dot{\boldsymbol{C}}$ 和 $\dot{T}$ 速率）都成立，这要求那些与非受限速率相乘的项必须为零。这立即导出了关于应力和熵的[本构关系](@entry_id:186508)：
$$
\boldsymbol{S} = 2\rho_0 \frac{\partial \hat{\psi}(\boldsymbol{C}, T)}{\partial \boldsymbol{C}} \quad \text{和} \quad \eta = -\frac{\partial \hat{\psi}(\boldsymbol{C}, T)}{\partial T}
$$
这里，$\boldsymbol{S}$ 是与 $\dot{\boldsymbol{E}}$（或 $\frac{1}{2}\dot{\boldsymbol{C}}$）[功共轭](@entry_id:194957)的**[第二皮奥拉-基尔霍夫应力](@entry_id:173163) (second Piola-Kirchhoff stress)**，$\rho_0$ 是参考构型密度，$\eta$ 是单位质量熵。这些关系被称为**[状态方程](@entry_id:274378)**，它们表明应力和熵不是独立的量，而是由[自由能函数](@entry_id:749582)对状态变量的导数唯一确定。[@problem_id:3552831]

对于更复杂的材料，如那些表现出[粘弹性](@entry_id:148045)或塑性的材料，当前状态不仅取决于当前的变形和温度，还取决于其加载历史。为了在[状态函数](@entry_id:137683)的框架内描述这种历史依赖性，我们引入了一组**内部[状态变量](@entry_id:138790) (internal state variables)**，记为 $\boldsymbol{\alpha}$。这些变量旨在捕捉[材料微观结构](@entry_id:198422)中不可见的、与耗散过程相关的变化，例如聚合物链的构象、晶体缺陷的密度或损伤的累积。[@problem_id:3552866]

对于这类材料，[热力学状态](@entry_id:755916)向量被扩展为 $z = (\boldsymbol{F}, T, \boldsymbol{\alpha})$（或使用客观度量，$(\boldsymbol{C}, T, \boldsymbol{\alpha})$）。[亥姆霍兹自由能](@entry_id:136442)现在是 $\psi = \hat{\psi}(\boldsymbol{C}, T, \boldsymbol{\alpha})$。再次应用科尔曼-诺尔程序，我们发现应力和熵的表达式形式上保持不变：
$$
\boldsymbol{S} = 2\rho_0 \frac{\partial \hat{\psi}(\boldsymbol{C}, T, \boldsymbol{\alpha})}{\partial \boldsymbol{C}} \quad \text{和} \quad \eta = -\frac{\partial \hat{\psi}(\boldsymbol{C}, T, \boldsymbol{\alpha})}{\partial T}
$$
然而，克劳修斯-杜亨不等式现在留下了一个**残余[耗散不等式](@entry_id:188634) (residual dissipation inequality)**：
$$
\mathcal{D} = \boldsymbol{A} \cdot \dot{\boldsymbol{\alpha}} \ge 0
$$
其中 $\boldsymbol{A} = -\rho_0 \frac{\partial \hat{\psi}}{\partial \boldsymbol{\alpha}}$ 被定义为与内部变量速率 $\dot{\boldsymbol{\alpha}}$ 共轭的**[热力学](@entry_id:141121)驱动力 (thermodynamic driving force)**。这个不等式表明，内部变量的演化必须以一种总是耗散能量（或至少不产生能量）的方式进行。

[状态向量](@entry_id:154607) $z = (\boldsymbol{C}, T, \boldsymbol{\alpha})$ 的选择是**最小的**，因为移除其中任何一个变量都将导致无法描述材料的完整行为。例如，对于一个热[粘弹性材料](@entry_id:194223)：
- 缺少 $\boldsymbol{C}$ 意味着无法描述对机械变形的响应。
- 缺少 $T$ 意味着无法描述[热膨胀](@entry_id:137427)或与温度相关的材料属性。
- 缺少 $\boldsymbol{\alpha}$ 则将模型简化为纯[热弹性](@entry_id:158447)材料，无法捕捉[粘性流](@entry_id:136330)动、[应力松弛](@entry_id:159905)或塑性变形等耗散效应。
因此，该状态向量为描述这类材料提供了一个完备且非冗余的基础。[@problem_id:3552866] [@problem_id:3552829]

### 耗散机制的建模

残余[耗散不等式](@entry_id:188634) $\mathcal{D} = \boldsymbol{A} \cdot \dot{\boldsymbol{\alpha}} \ge 0$ 是构建耗散材料演化方程的基石。为了确保这个不等式恒成立，**广义标准材料 (Generalized Standard Materials, GSM)** 框架被发展出来。该框架假定存在一个**耗散势 (dissipation potential)** $\phi$，它是一个关于内部变量速率 $\dot{\boldsymbol{\alpha}}$ 的凸函数，且在 $\dot{\boldsymbol{\alpha}}=\boldsymbol{0}$ 时取最小值为零。

然后，我们假定[热力学](@entry_id:141121)驱动力 $\boldsymbol{A}$ 和内部变量速率 $\dot{\boldsymbol{\alpha}}$ 之间存在一个**关联演化法则 (associative evolution law)**，即 $\boldsymbol{A}$ 可由 $\phi$ 对 $\dot{\boldsymbol{\alpha}}$ 的导数（或[次梯度](@entry_id:142710)）给出：
$$
\boldsymbol{A} = \frac{\partial \phi(\dot{\boldsymbol{\alpha}})}{\partial \dot{\boldsymbol{\alpha}}}
$$
由于 $\phi$ 的凸性，这个关联法则自动保证了耗散非负。这个框架为[粘弹性](@entry_id:148045)、塑性和损伤等多种不可逆过程的建模提供了一个统一而强大的工具。[@problem_id:3552843] [@problem_id:3552829]

#### 应用实例：粘弹性和塑性

让我们通过几个具体的例子来说明内部变量和耗散势的应用。

在**[线性粘弹性](@entry_id:181219) (linear viscoelasticity)** 中，例如一个[广义麦克斯韦模型](@entry_id:169862)，内部变量可以被选为代表模型中各个麦克斯韦单元的粘性应变 $\boldsymbol{\varepsilon}_v^i$。自由能可以构造成弹性部分和粘性部分的能量之和，例如：
$$
\psi(\boldsymbol{\varepsilon}, \{\boldsymbol{\varepsilon}_v^i\}) = \frac{1}{2}(\boldsymbol{\varepsilon} - \sum_i \boldsymbol{\varepsilon}_v^i) : \mathbb{C}_0 : (\boldsymbol{\varepsilon} - \sum_i \boldsymbol{\varepsilon}_v^i) + \sum_i \frac{1}{2} \boldsymbol{\varepsilon}_v^i : \mathbb{C}_i : \boldsymbol{\varepsilon}_v^i
$$
这里，$\mathbb{C}_0$ 和 $\mathbb{C}_i$ 是[弹性模量](@entry_id:198862)张量。[热力学力](@entry_id:161907)被证明是 $\boldsymbol{A}_i = \boldsymbol{\sigma} - \mathbb{C}_i:\boldsymbol{\varepsilon}_v^i$。选择一个关于速率 $\dot{\boldsymbol{\varepsilon}}_v^i$ 的二次耗散势 $\phi = \sum_i \frac{1}{2} (\dot{\boldsymbol{\varepsilon}}_v^i : \mathbb{L}_i^{-1} : \dot{\boldsymbol{\varepsilon}}_v^i)$，其中 $\mathbb{L}_i$ 是正定的流动性张量，即可得到一个线[性的演化](@entry_id:163338)法则 $\dot{\boldsymbol{\varepsilon}}_v^i = \mathbb{L}_i : \boldsymbol{A}_i$，这与经典的[流变模型](@entry_id:193749)相符。[@problem_id:3552819]

在**小应变塑性 (small-strain plasticity)** 中，典型的内部变量是**塑性[应变张量](@entry_id:193332) (plastic strain tensor)** $\boldsymbol{\varepsilon}^p$ 和一个或多个**[硬化](@entry_id:177483)变量 (hardening variables)**（例如，用于[各向同性硬化](@entry_id:164486)的标量 $r$）。应变被加法分解为弹性部分和塑性部分：$\boldsymbol{\varepsilon} = \boldsymbol{\varepsilon}^e + \boldsymbol{\varepsilon}^p$。自由能通常也相应地分解为弹性能和硬化能：
$$
\psi(\boldsymbol{\varepsilon}, \boldsymbol{\varepsilon}^p, r) = \psi_e(\boldsymbol{\varepsilon} - \boldsymbol{\varepsilon}^p) + \psi_h(r)
$$
[热力学力](@entry_id:161907)被证明是应力 $\boldsymbol{\sigma}$（与 $\boldsymbol{\varepsilon}^p$ 共轭）和硬化应力 $R$（与 $r$ 共轭）。[塑性流动](@entry_id:201346)由一个**[屈服函数](@entry_id:167970) (yield function)** $f(\boldsymbol{\sigma}, R) \le 0$ 控制，该函数定义了弹性区域的边界。关联塑性理论假定塑性[应变率](@entry_id:154778)的方向垂直于屈服面，这等价于将[屈服函数](@entry_id:167970)本身作为耗散势（对于率无关塑性）。[@problem_id:3552819]

对于**[有限应变塑性](@entry_id:185352) (finite strain plasticity)**，通常采用**变形梯度的[乘法分解](@entry_id:199514) (multiplicative decomposition of the deformation gradient)**：$\boldsymbol{F} = \boldsymbol{F}_e \boldsymbol{F}_p$。这里，$\boldsymbol{F}_p$ 代表一个导致塑性变形的局部、无应力构型重排，而 $\boldsymbol{F}_e$ 代表从这个虚拟的[中间构型](@entry_id:193000)到当前构型的后续弹性变形。亥姆霍兹自由能自然地被假定为弹性变形的函数，$\psi = \hat{\psi}(\boldsymbol{C}_e)$，其中 $\boldsymbol{C}_e = \boldsymbol{F}_e^{\mathsf{T}}\boldsymbol{F}_e$ 是弹性[右柯西-格林张量](@entry_id:174156)。通过[热力学分析](@entry_id:142723)，可以推导出驱动[塑性流动](@entry_id:201346)的有效应力，即**[曼德尔应力](@entry_id:191786) (Mandel stress)** $\boldsymbol{M} = \boldsymbol{C}_e \boldsymbol{S}_e$，其中 $\boldsymbol{S}_e = 2\rho_0 \partial\hat{\psi}/\partial\boldsymbol{C}_e$ 是[中间构型](@entry_id:193000)中的[第二皮奥拉-基尔霍夫应力](@entry_id:173163)。如果塑性流动是不可压缩的（即 $\det\boldsymbol{F}_p = 1$），则可以进一步证明只有[曼德尔应力](@entry_id:191786)的偏量部分 $\text{dev}(\boldsymbol{M})$ 才做塑性功，因此它才是驱动塑性变形的真正[热力学力](@entry_id:161907)。[@problem_id:3552874]

### 高阶主题与替代表述

#### 各向异性与结构张量

材料框架无关性（客观性）和**[材料对称性](@entry_id:190289) (material symmetry)**（如各向同性）是两个必须严格区分的独立概念。客观性是所有材料都必须满足的普适运动学约束，而[材料对称性](@entry_id:190289)是特定材料的内在属性。**各向同性 (Isotropic)** 材料在所有方向上具有相同的性质，而**各向异性 (anisotropic)** 材料则具有一个或多个优势方向（例如，[复合材料](@entry_id:139856)中的纤维方向，或轧制金属中的晶粒织构）。

为了在客观的框架下描述各向异性，我们引入**结构张量 (structural tensors)** $\mathcal{A}$。这些张量在参考构型中定义，用于量化材料的内部结构。例如，一个纤维方向可以用一个[单位向量](@entry_id:165907) $\boldsymbol{a}_0$ 表示，相应的结构张量可以是 $\mathcal{A} = \boldsymbol{a}_0 \otimes \boldsymbol{a}_0$。一个客观且各向异性的[亥姆霍兹自由能](@entry_id:136442)函数可以写成 $\psi = \hat{\psi}(\boldsymbol{C}, \mathcal{A})$。为了保证这个函数是标量，它必须表示为张量 $\boldsymbol{C}$ 和 $\mathcal{A}$ 的联合[不变量](@entry_id:148850)的函数。例如，除了 $\boldsymbol{C}$ 的[主不变量](@entry_id:193522)（如 $\text{tr}(\boldsymbol{C})$）之外，还会出现混合[不变量](@entry_id:148850)，如 $\boldsymbol{a}_0 \cdot \boldsymbol{C}\boldsymbol{a}_0$（表示沿纤维方向的拉伸平方）。这种方法能够构建出既满足客观性要求又能反映材料方向依赖性的复杂本构模型。[@problem_id:3552818]

#### [亚弹性](@entry_id:204371)与超弹性

在超弹性（hyperelasticity）理论（即基于[势能](@entry_id:748988) $\psi$ 的理论）出现之前，人们曾尝试使用率形式的本构关系，称为**[亚弹性](@entry_id:204371) (hypoelasticity)**，其一般形式为 $\stackrel{\circ}{\boldsymbol{\sigma}} = \mathbb{C}:\boldsymbol{d}$。这里，$\stackrel{\circ}{\boldsymbol{\sigma}}$ 是柯西应力 $\boldsymbol{\sigma}$ 的一个**[客观应力率](@entry_id:199282) (objective stress rate)**，例如**耀曼率 (Jaumann rate)** 或**[特鲁斯德尔率](@entry_id:181014) (Truesdell rate)**，$\boldsymbol{d}$ 是变形率张量。使用[客观应力率](@entry_id:199282)确保了该本构关系满足框架无关性原理。然而，一个关键的缺陷是，这类方程通常是**不可积的 (non-integrable)**。这意味着对于一个给定的最终变形状态，计算出的应力取决于所经历的加载路径。其直接后果是，在经历一个闭合的变形循环（即最终回到初始构型）后，[亚弹性模型](@entry_id:184632)会预测出非零的净功，这违反了弹性材料的[能量守恒](@entry_id:140514)特性。因此，[亚弹性模型](@entry_id:184632)通常不被认为是描述纯弹性行为的物理上合适的模型，而基于势能的超弹性模型由于其内在的能量一致性而成为首选。[@problem_id:3552803]

#### 计算中的热力学势选择

[亥姆霍兹自由能](@entry_id:136442) $\psi(\boldsymbol{\varepsilon}, \theta)$ 和**吉布斯自由能 (Gibbs free energy)** $G(\boldsymbol{\sigma}, \theta)$ 通过[勒让德变换](@entry_id:146727)相互关联。在计算力学中，选择哪一个[势函数](@entry_id:176105)作为基础并非无关紧要。最佳选择取决于[有限元列式](@entry_id:164720)中使用的主要未知场。
- 在标准的**位移-温度**列式中，节点未知量是位移 $\boldsymbol{u}$ 和温度 $\theta$。在积分点处，应变 $\boldsymbol{\varepsilon}$ 和温度 $\theta$ 是直接可得的量。因此，使用以 $(\boldsymbol{\varepsilon}, \theta)$ 为自然变量的亥姆霍兹自由能 $\psi$ 是最直接和高效的。
- 在**应力-温度**混合列式中，应力 $\boldsymbol{\sigma}$ 和温度 $\theta$ 被作为独立场。此时，使用以 $(\boldsymbol{\sigma}, \theta)$ 为自然变量的吉布斯自由能 $G$ 则是最自然的选择。
通过将势函数的自变量与[有限元列式](@entry_id:164720)的主要变量相匹配，可以简化本构更新算法并提高[计算效率](@entry_id:270255)。[@problem_id:3552831]

#### [材料稳定性](@entry_id:183933)与凸性条件

最后，一个[本构模型](@entry_id:174726)的数学属性对其物理真实性和数值行为有着深远的影响。对于[超弹性材料](@entry_id:190241)，[应变能函数](@entry_id:178435) $\psi$ 的**[凸性](@entry_id:138568) (convexity)** 条件至关重要。
- **$\psi$ 关于 $\boldsymbol{C}$ 的[凸性](@entry_id:138568)**：对于某些模型（如圣维南-基尔霍夫模型），$\psi$ 是关于其参数 $\boldsymbol{C}$ 的[凸函数](@entry_id:143075)。然而，这并不足以保证材料在所有变形下都是稳定的。
- **[秩一凸性](@entry_id:191019) (Rank-one convexity)**：这是一个比 $\boldsymbol{C}$-[凸性](@entry_id:138568)更弱的条件，它直接作用于变形梯度 $\boldsymbol{F}$。物理上，它与**勒让德-[阿达玛条件](@entry_id:168914) (Legendre-Hadamard condition)** 等价，后者要求在任何方向上的平面波波速都是实数。如果一个材料在某个变形状态下丧失了[秩一凸性](@entry_id:191019)，它就会发生材料失稳（如[剪切带](@entry_id:183352)的形成），并且控制方程会从椭圆型变为双曲型，导致数值解出现病态的[网格依赖性](@entry_id:198563)。
- **[多凸性](@entry_id:185154) (Polyconvexity)**：这是一个比[秩一凸性](@entry_id:191019)更强的条件。[多凸性](@entry_id:185154)是保证[变分问题](@entry_id:756445)（如能量[泛函最小化](@entry_id:184561)）存在解的一个充分条件。在计算中，基于多凸能量函数的模型通常表现出更好的稳定性和收敛性。

一个著名的例子是**圣维南-基尔霍夫 (St. Venant-Kirchhoff)** 模型，其能量函数 $\psi(C)$ 是 $\boldsymbol{C}$ 的[凸函数](@entry_id:143075)，但它在压缩下会丧失[秩一凸性](@entry_id:191019)，这说明了不同凸性概念之间的微妙区别和深刻含义。理解这些数学条件对于开发稳定可靠的[非线性材料模型](@entry_id:193383)至关重要。[@problem_id:3552885]