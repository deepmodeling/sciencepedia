## 引言
材料的[本构关系](@entry_id:186508)是描述其在外部载荷下如何变形和响应的数学方程，它是连接基础材料科学与工程[结构设计](@entry_id:196229)的核心桥梁。从航空发动机的涡轮盘到人体内的动脉血管，准确预测材料的力学行为对于确保安全性和功能性至关重要。然而，面对纷繁复杂的材料现象——弹性、塑性、[蠕变](@entry_id:150410)、损伤——学习者往往会迷失在各种独立的模型之中，难以把握其背后统一的物理和数学基础。本文旨在填补这一知识鸿沟，为读者构建一个关于材料本构建模的系统性认知框架。

在接下来的内容中，我们将分三步深入探索这一领域。第一章“原理与机制”将从[连续介质力学](@entry_id:155125)的基本概念出发，建立一套严谨的数学语言，并阐明所有模型都必须遵循的[热力学约束](@entry_id:755911)。第二章“应用与交叉学科联系”将展示这些理论如何在工程结构、生物力学和[多尺度模拟](@entry_id:752335)等前沿领域中发挥关键作用，揭示其广泛的学科交叉价值。最后，第三章“动手实践”将通过一系列精心设计的计算练习，帮助读者将理论知识转化为解决实际问题的能力。

让我们首先进入第一章，奠定[本构建模](@entry_id:183370)的基石：其基本原理与内在机制。

## 原理与机制

本章旨在系统性地阐述构建材料本构模型的基本原理以及支配材料行为的内在机制。我们将从连续介质力学的基本运动学和动力学概念出发，建立适用于有限变形的数学描述。随后，我们将引入两个普适的指导原则——材料框架无关性和[材料对称性](@entry_id:190289)，它们为所有[本构关系](@entry_id:186508)施加了严格的约束。本章的核心将是基于[热力学定律](@entry_id:202285)，特别是[Clausius-Duhem不等式](@entry_id:193424)，建立一个严谨的框架，以确保任何[本构模型](@entry_id:174726)都符合物理现实。利用这一框架，我们将探讨几种关键的材料行为机制——弹性、塑性、黏弹性和损伤——并介绍用于描述这些行为的经典模型。最后，我们将简要介绍多尺度建模中的均匀化方法，为从微观结构推导宏观本构关系提供一个初步的视角。

### [本构模型](@entry_id:174726)的基本原理

在深入研究具体的材料模型之前，我们必须首先建立一套用于描述材料变形和受力的通用语言，并明确所有[本构关系](@entry_id:186508)都必须遵守的基本公理。

#### 运动学基础：变形与应变的度量

当一个物体从其**初始构型**（或称参考构型）运动并变形到**当前构型**时，我们需要精确地量化其内部各点的局部变形。这一描述是通过**变形梯度**（deformation gradient）张量 $\mathbf{F}$ 来实现的。它将参考构型中的一个微元线段 $d\mathbf{X}$ 映射到当前构型中的对应线段 $d\mathbf{x}$，即 $d\mathbf{x} = \mathbf{F} d\mathbf{X}$。

虽然 $\mathbf{F}$ 完整地描述了变形，但它本身包含了[刚体转动](@entry_id:191086)，而材料的本构响应（即应力）通常仅由拉伸和剪切（即应变）引起。因此，我们需要定义一个纯粹度量应变的张量。在有限变形理论中，不存在唯一的[应变度量](@entry_id:755495)，选择哪种度量取决于所采用的数学框架（例如，是在参考构型上还是在当前构型上描述问题）。

考虑一个微元线段的长度平方的变化：在参考构型中为 $dS^2 = d\mathbf{X} \cdot d\mathbf{X}$，在当前构型中为 $ds^2 = d\mathbf{x} \cdot d\mathbf{x}$。两者之差可以用来定义应变。

- **[格林-拉格朗日应变张量](@entry_id:187745) (Green-Lagrange strain tensor)** $\mathbf{E}$ 是一个**物质[应变度量](@entry_id:755495)**（material strain measure），它在参考构型上定义。其定义源于将长度平方的变化与初始线段 $d\mathbf{X}$ 相关联：
  $ds^2 - dS^2 = d\mathbf{x}^{\mathsf{T}}d\mathbf{x} - d\mathbf{X}^{\mathsf{T}}d\mathbf{X} = (\mathbf{F}d\mathbf{X})^{\mathsf{T}}(\mathbf{F}d\mathbf{X}) - d\mathbf{X}^{\mathsf{T}}d\mathbf{X} = d\mathbf{X}^{\mathsf{T}}(\mathbf{F}^{\mathsf{T}}\mathbf{F} - \mathbf{I})d\mathbf{X}$。
  我们定义**右柯西-格林变形张量**（right Cauchy-Green deformation tensor）为 $\mathbf{C} = \mathbf{F}^{\mathsf{T}}\mathbf{F}$，则上述关系变为 $ds^2 - dS^2 = d\mathbf{X}^{\mathsf{T}}(\mathbf{C} - \mathbf{I})d\mathbf{X}$。[格林-拉格朗日应变张量](@entry_id:187745) $\mathbf{E}$ 定义为：
  $$ \mathbf{E} = \frac{1}{2}(\mathbf{C} - \mathbf{I}) = \frac{1}{2}(\mathbf{F}^{\mathsf{T}}\mathbf{F} - \mathbf{I}) $$
  由于 $\mathbf{E}$ 是在参考构型上定义的，它自然适用于那些将[本构关系](@entry_id:186508)（如[储能函数](@entry_id:197811)）表达为初始构型函数的**拉格朗日描述**（Lagrangian description）。

- **[阿尔曼西应变](@entry_id:191140)张量 (Almansi strain tensor)** $\mathbf{e}$ 是一个**空间[应变度量](@entry_id:755495)**（spatial strain measure），它在当前构型上定义。其定义源于将同一长度平方变化与当前线段 $d\mathbf{x}$ 相关联：
  $ds^2 - dS^2 = d\mathbf{x}^{\mathsf{T}}\mathbf{I}d\mathbf{x} - (\mathbf{F}^{-1}d\mathbf{x})^{\mathsf{T}}(\mathbf{F}^{-1}d\mathbf{x}) = d\mathbf{x}^{\mathsf{T}}(\mathbf{I} - \mathbf{F}^{-\mathsf{T}}\mathbf{F}^{-1})d\mathbf{x}$。
  我们定义**左柯西-格林变形张量**（left Cauchy-Green deformation tensor）为 $\mathbf{b} = \mathbf{F}\mathbf{F}^{\mathsf{T}}$，其逆为 $\mathbf{b}^{-1} = \mathbf{F}^{-\mathsf{T}}\mathbf{F}^{-1}$。于是，[阿尔曼西应变](@entry_id:191140)张量 $\mathbf{e}$ 定义为：
  $$ \mathbf{e} = \frac{1}{2}(\mathbf{I} - \mathbf{b}^{-1}) $$
  由于 $\mathbf{e}$ 是在当前构型上定义的，它自然适用于那些在空间框架中表述本构关系的**[欧拉描述](@entry_id:264722)**（Eulerian description），例如在流[体力](@entry_id:174230)学或某些[固体力学](@entry_id:164042)数值方法中。

这两种应变张量都是**客观的**（objective），即它们的值在叠加一个[刚体转动](@entry_id:191086)后保持不变（对于物质张量 $\mathbf{E}$）或以客观的方式进行变换（对于[空间张量](@entry_id:185799) $\mathbf{e}$）。在构建[本构模型](@entry_id:174726)时，选择合适的[应变度量](@entry_id:755495)至关重要，因为它直接关系到与之[功共轭](@entry_id:194957)的应力度量以及整个本构框架的数学一致性 。

#### 动力学基础：应力的度量

与[应变度量](@entry_id:755495)类似，应力的定义也取决于我们是测量单位参考面积上的力还是单位当前面积上的力。在有限变形理论中，有多种应力度量，它们之间可以通过变形梯度 $\mathbf{F}$ 及其雅可比行列式 $J = \det(\mathbf{F})$ 进行转换。

- **柯西应力张量 (Cauchy stress tensor)** $\boldsymbol{\sigma}$ 是物理上最直观的应力度量，代表当前构型中单位变形后面积上的真实作用力。根据柯西定理，作用在[法向量](@entry_id:264185)为 $\mathbf{n}$ 的面上的牵[引力](@entry_id:189550)矢量 $\mathbf{t}$ 由 $\mathbf{t} = \boldsymbol{\sigma}\mathbf{n}$ 给出。在没有体力矩的情况下，动量矩守恒要求 $\boldsymbol{\sigma}$ 是对称的（$\boldsymbol{\sigma} = \boldsymbol{\sigma}^{\mathsf{T}}$）。

- **[第一皮奥拉-基尔霍夫应力](@entry_id:163971)张量 (First Piola-Kirchhoff stress tensor)** $\mathbf{P}$ 是一个名义应力，它将作用在当前构型上的力与参考构型中的[面积元](@entry_id:263205)相关联。它将参考法向量 $\mathbf{N}$ 映射到名义牵[引力](@entry_id:189550)（单位参考面积上的力） $\mathbf{T}$，即 $\mathbf{T} = \mathbf{P}\mathbf{N}$。$\mathbf{P}$ 是一个“两点”张量，因为它将参考构型中的一个矢量（$\mathbf{N}$）映射到当前构型中的一个矢量（$\mathbf{T}$）。通常情况下，$\mathbf{P}$ 是非对称的。

- **[第二皮奥拉-基尔霍夫应力](@entry_id:173163)张量 (Second Piola-Kirchhoff stress tensor)** $\mathbf{S}$ 是一个完全在参考构型中定义的应力度量。它通过关系式 $\mathbf{P} = \mathbf{F}\mathbf{S}$ 与[第一皮奥拉-基尔霍夫应力](@entry_id:163971)联系起来。$\mathbf{S}$ 的主要优点在于它与[格林-拉格朗日应变](@entry_id:170427)率 $\dot{\mathbf{E}}$ 在能量上是[功共轭](@entry_id:194957)的，即单位参考体积的[应力功率](@entry_id:182907)为 $\dot{W} = \mathbf{S}:\dot{\mathbf{E}}$。与柯西应力一样，$\mathbf{S}$ 也是对称的。

- **[基尔霍夫应力](@entry_id:751039)张量 (Kirchhoff stress tensor)** $\boldsymbol{\tau}$ 是柯西应力 $\boldsymbol{\sigma}$ 的一个加权版本，定义为 $\boldsymbol{\tau} = J\boldsymbol{\sigma}$。引入它的主要目的是简化某些有限变形理论中的数学表达式。$\boldsymbol{\tau}$ 也是对称的。

这些[应力张量](@entry_id:148973)之间的转换关系对于在不同描述框架（[拉格朗日与欧拉](@entry_id:270774)）之间转换本构模型至关重要。关键的转换公式包括 ：
$$ \mathbf{P} = \mathbf{F}\mathbf{S} $$
$$ \boldsymbol{\sigma} = \frac{1}{J}\mathbf{P}\mathbf{F}^{\mathsf{T}} = \frac{1}{J}\mathbf{F}\mathbf{S}\mathbf{F}^{\mathsf{T}} $$
$$ \boldsymbol{\tau} = J\boldsymbol{\sigma} = \mathbf{F}\mathbf{S}\mathbf{F}^{\mathsf{T}} $$

#### 指导原则：框架无关性与[材料对称性](@entry_id:190289)

除了运动学和动力学的基本描述外，任何有效的本构模型都必须遵守两个高级别的原理：材料框架无关性和[材料对称性](@entry_id:190289)。这两个概念虽然都涉及转动，但其物理意义和数学表述截然不同，理解它们的区别至关重要。

**材料框架无关性**（Material frame indifference），或称**客观性**（objectivity），是一个普适的物理公理。它要求物理定律（包括[本构关系](@entry_id:186508)）的形式不应依赖于观察者。在连续介质力学中，这意味着[本构关系](@entry_id:186508)在叠加一个任意的[刚体运动](@entry_id:144691)（转动和平移）到当前构型后必须保持形式不变。考虑一个变形，其变形梯度为 $\mathbf{F}$，一个改变了观察者参考系的刚体运动可以用一个正交张量 $\mathbf{Q}$ ($\mathbf{Q}^{\mathsf{T}}\mathbf{Q}=\mathbf{I}, \det(\mathbf{Q})=1$) 来表示，使得新的变形梯度变为 $\mathbf{F}^+ = \mathbf{Q}\mathbf{F}$。框架无关性要求材料的响应（例如，[储能函数](@entry_id:197811) $\Psi$）对于这种变换是不变的：
$$ \Psi(\mathbf{Q}\mathbf{F}, \boldsymbol{\alpha}) = \Psi(\mathbf{F}, \boldsymbol{\alpha}) \quad \text{对于所有 } \mathbf{Q} \in \mathrm{SO}(3) $$
这里 $\boldsymbol{\alpha}$ 代表一组在参考构型中定义的内部变量（如[晶格](@entry_id:148274)取向、纤维方向等），它们本身是客观的，因为它们描述的是材料的内在结构，与空间观察者无关。为了满足这一要求，[储能函数](@entry_id:197811) $\Psi$ 只能通过那些在空间[刚体转动](@entry_id:191086)下不变的量来依赖于 $\mathbf{F}$。[右柯西-格林张量](@entry_id:174156) $\mathbf{C} = \mathbf{F}^{\mathsf{T}}\mathbf{F}$ 正是这样一个量，因为它在变换 $\mathbf{F} \to \mathbf{Q}\mathbf{F}$ 下保持不变。因此，框架无关性原理将[储能函数](@entry_id:197811)的一般形式 $\Psi(\mathbf{F}, \boldsymbol{\alpha})$ 简化为**简约形式**（reduced form）$\hat{\Psi}(\mathbf{C}, \boldsymbol{\alpha})$。本构关系 $\mathbf{S}=\mathcal{S}(\mathbf{C},\boldsymbol{\alpha})$ 的形式本身就已经蕴含了框架无关性原理的应用 。

**[材料对称性](@entry_id:190289)**（Material symmetry）则不是一个普适公理，而是描述特定材料内在对称性的属性。它指的是在参考构型中，存在一组转动（或更一般的变换），使得材料的本构响应在这些变换前后保持不变。这些变换构成了材料的**[对称群](@entry_id:146083)** $\mathcal{G}_{m}$。例如，对于[各向同性材料](@entry_id:170678)，其性质不随方向改变，因此[对称群](@entry_id:146083)是整个[特殊正交群](@entry_id:146418) $\mathrm{SO}(3)$。而对于具有特定纤维方向的复合材料（横观各向同性），其对称群只包括绕纤维轴的任意转动和绕垂直于纤维轴的 $180^\circ$ 转动。

数学上，一个对称性变换 $\mathbf{Q}_m \in \mathcal{G}_m$ 作用于参考构型上，使得变形梯度变为 $\mathbf{F}' = \mathbf{F}\mathbf{Q}_m$。这会相应地改变变形张量和内部变量：$\mathbf{C} \to \mathbf{Q}_m^{\mathsf{T}}\mathbf{C}\mathbf{Q}_m$，$\boldsymbol{\alpha} \to \mathbf{Q}_m^{\diamond}\boldsymbol{\alpha}$ (其中 $\mathbf{Q}_m^{\diamond}$ 代表对 $\boldsymbol{\alpha}$ 的恰当变换)。[材料对称性](@entry_id:190289)要求：
$$ \hat{\Psi}(\mathbf{Q}_m^{\mathsf{T}}\mathbf{C}\mathbf{Q}_m, \mathbf{Q}_m^{\diamond}\boldsymbol{\alpha}) = \hat{\Psi}(\mathbf{C}, \boldsymbol{\alpha}) \quad \text{对于所有 } \mathbf{Q}_m \in \mathcal{G}_m $$
这条约束极大地限制了[储能函数](@entry_id:197811) $\hat{\Psi}$ 的具体形式。根据[不变量理论](@entry_id:145135)，$\hat{\Psi}$ 必须是其张量变量 $(\mathbf{C}, \boldsymbol{\alpha})$ 在对称群 $\mathcal{G}_m$ 作用下的一组[标量不变量](@entry_id:193787)的函数。例如，对于一个由纤维方向 $\mathbf{a}_0$ 表征的横观[各向同性材料](@entry_id:170678)，$\hat{\Psi}$ 必须是诸如 $\mathrm{tr}(\mathbf{C})$, $\mathrm{tr}(\mathbf{C}^2)$, $\det(\mathbf{C})$, $\mathbf{a}_0 \cdot \mathbf{C}\mathbf{a}_0$, $\mathbf{a}_0 \cdot \mathbf{C}^2\mathbf{a}_0$ 等不变量的函数 。

### [热力学](@entry_id:172368)框架

为了确保[本构模型](@entry_id:174726)在物理上是合理的，它必须遵守热力学定律。这为[本构关系](@entry_id:186508)的推导提供了最坚实的理论基础。

#### [热力学](@entry_id:172368)第一和第二定律

对于一个连续介质，热力学定律可以写成局部（[微分](@entry_id:158422)）形式。在拉格朗日描述下，单位参考体积的**热力学第一定律**（能量守恒）可以表述为：
$$ \rho_0 \dot{e} = \mathbf{P}:\dot{\mathbf{F}} - \nabla_0 \cdot \mathbf{Q} + \rho_0 r $$
其中，$\rho_0$ 是参考密度，$\dot{e}$ 是单位质量内能的时间变化率，$\mathbf{P}:\dot{\mathbf{F}}$ 是[应力功率](@entry_id:182907)密度（[内力](@entry_id:167605)做功的速率），$\mathbf{Q}$ 是参考构型下的热流矢量，$\rho_0 r$ 是单位体积的内热源。等式左边是内能的增加率，右边是[内力](@entry_id:167605)做功减去热量流出再加上内部热源产生的热量。

**[热力学](@entry_id:172368)第二定律**以熵的形式陈述了过程的不可逆性。其局部形式，即**[Clausius-Duhem不等式](@entry_id:193424)**，规定了熵的产生必须是非负的。在[拉格朗日描述](@entry_id:1127015)下，它写作：
$$ \rho_0 \dot{\eta} \ge - \nabla_0 \cdot \left(\frac{\mathbf{Q}}{\Theta}\right) + \frac{\rho_0 r}{\Theta} $$
其中 $\eta$ 是单位质量的熵，$\Theta$ 是绝对温度。不等式表明，熵的增加率（左侧）至少等于通过边界流入的熵流和由热源产生的熵（右侧）。

通过引入**[亥姆霍兹自由能](@entry_id:136442)**（Helmholtz free energy）$\psi = e - \Theta\eta$，我们可以将这两个定律合并成一个更实用的不等式。经过推导，我们得到自由能形式的[Clausius-Duhem不等式](@entry_id:193424) ：
$$ \rho_0 \dot{\psi} + \rho_0 \eta \dot{\Theta} \le \mathbf{P}:\dot{\mathbf{F}} - \frac{\mathbf{Q}\cdot \nabla_0 \Theta}{\Theta} $$
这个不等式是所有本构关系推导的出发点。它表明，提供给系统的机械功率（$\mathbf{P}:\dot{\mathbf{F}}$）必须大于或等于储存为自由能和可逆热的部分（$\rho_0 \dot{\psi} + \rho_0 \eta \dot{\Theta}$）加上由[热传导](@entry_id:143509)耗散的部分。

#### Coleman-Noll程序与内部状态变量

**Coleman-Noll程序**是一种系统性地利用[Clausius-Duhem不等式](@entry_id:193424)来推导本构关系并确保其热力学一致性的方法。该程序的核心思想是：本构关系描述的是材料在任何可能的物理过程中的响应，因此[热力学不等式](@entry_id:161368)必须对所有这些过程都成立。

考虑一个材料，其状态由一组**[状态变量](@entry_id:138790)**描述，例如[格林-拉格朗日应变](@entry_id:170427) $\mathbf{E}$、温度 $\Theta$ 以及一组**内部状态变量** $\boldsymbol{\alpha}$。内部状态变量 $\boldsymbol{\alpha}$ 可以是标量、矢量或张量，用于描述材料内部的微观结构状态，如塑性应变、损伤程度或高分子链的取向。亥姆霍兹自由能被假定为这些[状态变量](@entry_id:138790)的函数：$\psi = \psi(\mathbf{E}, \Theta, \boldsymbol{\alpha})$。

我们将 $\dot{\psi}$ 的链式法则表达式代入[Clausius-Duhem不等式](@entry_id:193424)（使用[功共轭](@entry_id:194957)对 $\mathbf{S}$ 和 $\mathbf{E}$ 更为方便）：
$$ (\mathbf{S} - \rho_0\frac{\partial\psi}{\partial\mathbf{E}}):\dot{\mathbf{E}} - \rho_0(\eta + \frac{\partial\psi}{\partial\Theta})\dot{\Theta} - \rho_0\frac{\partial\psi}{\partial\boldsymbol{\alpha}}:\dot{\boldsymbol{\alpha}} - \frac{\mathbf{Q}\cdot\nabla_0\Theta}{\Theta} \ge 0 $$
由于我们可以任意控制[应变率](@entry_id:154778) $\dot{\mathbf{E}}$ 和温度变化率 $\dot{\Theta}$，为了使不等式对任意过程都成立，乘以这些任意速率的系数必须为零。这立即给出了**非耗散**（non-dissipative）的本构关系：
$$ \mathbf{S} = \rho_0\frac{\partial\psi}{\partial\mathbf{E}} \quad \text{和} \quad \eta = -\frac{\partial\psi}{\partial\Theta} $$
这些关系表明，应力和熵可以直接从[自由能函数](@entry_id:749582)对相应的状态变量求导得到。不等式随之简化为**剩余[耗散不等式](@entry_id:188634)**（residual dissipation inequality）：
$$ \mathcal{D}_{\mathrm{int}} = -\rho_0\frac{\partial\psi}{\partial\boldsymbol{\alpha}}:\dot{\boldsymbol{\alpha}} - \frac{\mathbf{Q}\cdot\nabla_0\Theta}{\Theta} \ge 0 $$
该不等式将总耗散分为了两部分：由内部变量演化引起的**内禀耗散**（intrinsic dissipation）和由[热传导](@entry_id:143509)引起的热耗散。定义[热力学力](@entry_id:161907) $\mathbf{A} = -\rho_0\frac{\partial\psi}{\partial\boldsymbol{\alpha}}$，内禀耗散可以写为 $\mathbf{A}:\dot{\boldsymbol{\alpha}} \ge 0$ (假设热耗散独立非负)。这表明，内部变量的演化方向必须使其与共轭的[热力学力](@entry_id:161907)做正功。

为了[封闭模型](@entry_id:1122505)，我们还需要一个描述内部变量如何演化的**演化方程**，即 $\dot{\boldsymbol{\alpha}}$ 的表达式。一个常见且强大的方法是引入一个**耗散势**（dissipation potential） $\Phi^*$，它是[热力学力](@entry_id:161907) $\mathbf{A}$ 的函数。如果演化方程取缔合于该势的形式：
$$ \dot{\boldsymbol{\alpha}} = \frac{\partial\Phi^*}{\partial\mathbf{A}} $$
并且 $\Phi^*$ 是一个关于 $\mathbf{A}$ 的凸函数且在 $\mathbf{A}=0$ 时取最小值0，那么[耗散不等式](@entry_id:188634) $\mathbf{A}:\dot{\boldsymbol{\alpha}} \ge 0$ 将自动得到满足。这种方法为构建[热力学一致的](@entry_id:755906)黏塑性、损伤等复杂模型提供了系统性的途径 。

### 典型材料行为的[本构模型](@entry_id:174726)

基于上述原理，我们可以为不同类型的材料行为构建具体的[本构模型](@entry_id:174726)。

#### [超弹性](@entry_id:159356)

[超弹性材料](@entry_id:190241)是一种理想弹性体，其[应力-应变关系](@entry_id:274093)可以从一个[标量势](@entry_id:276177)函数——**[应变能密度函数](@entry_id:755490)**（strain energy density function）$\Psi$——导出。对于各向同性[超弹性材料](@entry_id:190241)，$\Psi$ 是应变[张量不变量](@entry_id:203254)的函数。

**体积-等容分解 (Volumetric-Isochoric Split)**
对于可压缩材料，特别是橡胶类材料，其体积变化（压缩性）和形状变化（剪切）的响应机制差异很大。因此，在建模时将这两种行为[解耦](@entry_id:160890)是一种非常有效的方法。这通过对变形梯度 $\mathbf{F}$进行**[乘法分解](@entry_id:199514)**实现 ：
$$ \mathbf{F} = J^{1/3}\bar{\mathbf{F}} $$
其中 $J = \det(\mathbf{F})$ 是体积变化比，$J^{1/3}$ 代表了平均的线弹性伸长。$\bar{\mathbf{F}}$ 是变形的**等容部分**（isochoric part），其行列式 $\det(\bar{\mathbf{F}})=1$。相应地，我们可以定义等容[右柯西-格林张量](@entry_id:174156) $\bar{\mathbf{C}} = J^{-2/3}\mathbf{C}$。

基于此分解，[应变能函数](@entry_id:178435)可以写成体积部分 $U(J)$ 和等容部分 $\Psi_{\mathrm{iso}}(\bar{\mathbf{C}})$ 的叠加形式：
$$ \Psi(\mathbf{C}) = U(J) + \Psi_{\mathrm{iso}}(\bar{\mathbf{C}}) $$
这种分解的优点在于，体积响应（通常是抵抗压缩的惩罚项）完全由 $U(J)$ 控制，其贡献于柯西应力是一个静水压力项 $U'(J)\mathbf{I}$。而形状变化的响应则由 $\Psi_{\mathrm{iso}}$ 控制，其贡献于柯西应力是一个[偏应力](@entry_id:163323)项（迹为零）。

**经典模型：Neo-Hookean与Mooney-Rivlin**
对于[各向同性材料](@entry_id:170678)，$\Psi_{\mathrm{iso}}$ 是 $\bar{\mathbf{C}}$ 的不变量 $\bar{I}_1 = \mathrm{tr}(\bar{\mathbf{C}})$ 和 $\bar{I}_2$ 的函数。

- **Neo-Hookean模型**是最简单的[超弹性](@entry_id:159356)模型之一，它假设[应变能](@entry_id:162699)仅与第一不变量[线性相关](@entry_id:185830)。其不可压缩形式为 $\Psi = C_{10}(I_1 - 3)$，其中 $I_1 = \mathrm{tr}(\mathbf{C})$。其可压缩形式采用体积-等容分解，$\Psi = U(J) + C_{10}(\bar{I}_1 - 3)$ 。

- **[Mooney-Rivlin模型](@entry_id:177592)**是Neo-Hookean模型的扩展，它同时包含了第一和第二不变量的线性项。其不可压缩形式为 $\Psi = C_{10}(I_1 - 3) + C_{01}(I_2 - 3)$。同样，其可压缩形式可以写为 $\Psi = U(J) + C_{10}(\bar{I}_1 - 3) + C_{01}(\bar{I}_2 - 3)$ 。该模型能更好地拟合[大应变](@entry_id:751152)下橡胶材料的实验数据。

#### 塑性

塑性描述了材料在加载超过某一阈值后发生的不可恢复变形。

**[屈服函数](@entry_id:167970)与[流动法则](@entry_id:177163)**
塑性理论的核心是**[屈服面](@entry_id:175331)**（yield surface）的概念，它在[应力空间](@entry_id:199156)中定义了弹性行为和塑性行为的边界。[屈服面](@entry_id:175331)由一个**[屈服函数](@entry_id:167970)** $f(\boldsymbol{\sigma}, \kappa) = 0$ 描述，其中 $\boldsymbol{\sigma}$ 是应力，$\kappa$ 是一组描述[材料硬化](@entry_id:175896)状态的内部变量。当应力状态在[屈服面](@entry_id:175331)内部时（$f  0$），材料行为是弹性的；当应力状态达到[屈服面](@entry_id:175331)时（$f=0$），塑性变形开始。

**J2（von Mises）塑性模型**是描述金属[材料塑性](@entry_id:186852)的经典模型。它假设屈服取决于[应力张量](@entry_id:148973)的偏量部分 $\mathbf{s} = \boldsymbol{\sigma} - \frac{1}{3}\mathrm{tr}(\boldsymbol{\sigma})\mathbf{I}$ 的第二不变量 $J_2 = \frac{1}{2}\mathbf{s}:\mathbf{s}$。[屈服函数](@entry_id:167970)通常写为：
$$ f(\boldsymbol{\sigma}, \kappa) = \sigma_{eq} - \sigma_y(\kappa) = \sqrt{3J_2} - \sigma_y(\kappa) = 0 $$
其中 $\sigma_{eq} = \sqrt{3J_2}$ 被称为[von Mises等效应力](@entry_id:756574)，$\sigma_y(\kappa)$ 是材料当前的单轴屈服强度，它会随着硬化变量 $\kappa$ （如等效塑性应变）的增加而演化。$\sqrt{3}$ 这个系数是通过将[等效应力](@entry_id:749064)与[单轴拉伸](@entry_id:188287)状态下的应力进行校准得出的 。

塑性应变增量 $d\boldsymbol{\varepsilon}^p$ 的方向由**[流动法则](@entry_id:177163)**（flow rule）确定，它通常假设源于一个**塑性势** $g(\boldsymbol{\sigma}, \kappa)$：
$$ d\boldsymbol{\varepsilon}^p = d\lambda \frac{\partial g}{\partial \boldsymbol{\sigma}} $$
其中 $d\lambda$ 是一个非负的塑性乘子。

- 当塑性[势函数](@entry_id:176105)与[屈服函数](@entry_id:167970)相同时（$g=f$），[流动法则](@entry_id:177163)是**关联的**（associative）。这被称为**正交[流动法则](@entry_id:177163)**（normality rule），因为它意味着塑性应变增量的方向垂直于[屈服面](@entry_id:175331)。对于von Mises模型，由于 $f$ 只依赖于 $J_2$，其对应力梯度与应力偏量 $\mathbf{s}$ 成正比。因此，塑性应变增量也是偏量的，即 $\mathrm{tr}(d\boldsymbol{\varepsilon}^p) = 0$，这表明von Mises关联塑性理论预测了塑性体积[不可压缩性](@entry_id:274914)，这与大多数金属的行为非常吻合 。
- 当塑性[势函数](@entry_id:176105)与[屈服函数](@entry_id:167970)不同时（$g \neq f$），[流动法则](@entry_id:177163)是**非关联的**（non-associative）。这在模拟土壤、岩石和混凝土等压力敏感材料时非常重要，因为关联[流动法则](@entry_id:177163)往往会过高地预测这些材料的[剪胀性](@entry_id:201001)。

#### 黏弹性

黏弹性材料同时表现出弹性固体的储能特性和黏性流体的耗能特性，其响应具有时间依赖性。

在线性小应变范围内，黏弹性行为可以通过**[Boltzmann叠加原理](@entry_id:185170)**（Boltzmann superposition principle）来描述。该原理指出，材料在任意时刻的响应是其整个加载历史中所有微小增量响应的线性叠加。

这导致了本构关系表现为**[遗传积分](@entry_id:186265)**（hereditary integral）的形式。具体来说，应力 $\sigma(t)$ 可以通过对整个应变率历史 $\dot{\varepsilon}(\tau)$ 进行卷积来计算，反之亦然 ：
$$ \sigma(t) = \int_0^t G(t-\tau)\dot{\varepsilon}(\tau)d\tau $$
$$ \varepsilon(t) = \int_0^t J(t-\tau)\dot{\sigma}(\tau)d\tau $$
这里假设材料在 $t  0$ 时处于静止状态。

- **松弛模量 (Relaxation modulus)** $G(t)$ 描述了材料在施加一个单位阶跃应变 $\varepsilon(t) = H(t)$ 后的应力响应。应力会从一个初始值开始随时间衰减或“松弛”。
- **[蠕变柔量](@entry_id:182488) (Creep compliance)** $J(t)$ 描述了材料在施加一个单位阶跃应力 $\sigma(t) = H(t)$ 后的应变响应。应变会随时间逐渐增长或“[蠕变](@entry_id:150410)”。

$G(t)$ 和 $J(t)$ 并非相互独立，它们通过[拉普拉斯变换](@entry_id:159339)域中的一个简单关系联系在一起：$s^2 \hat{G}(s) \hat{J}(s) = 1$，其中 $\hat{G}(s)$ 和 $\hat{J}(s)$ 分别是 $G(t)$ 和 $J(t)$ 的[拉普拉斯变换](@entry_id:159339)。这两种材料函数提供了表征线性黏弹性材料行为的等效方式。

#### [连续介质损伤力学](@entry_id:177438)

[连续介质损伤力学](@entry_id:177438)（CDM）旨在通过引入连续的内部变量来描述材料因微裂纹、微孔洞的萌生和扩展而导致的刚度和强度退化。

最简单的模型引入一个标量**[损伤变量](@entry_id:197066)** $D$，其值域为 $[0, 1]$，其中 $D=0$ 代表无损材料，$D=1$ 代表完全破坏。

一个核心概念是**有效应力**（effective stress） $\tilde{\boldsymbol{\sigma}}$，它代表在材料未损伤的承载部分上所承受的应力。**[应变等效](@entry_id:186173)性原理**（principle of strain equivalence）假设，损伤材料在应力 $\boldsymbol{\sigma}$ 下的应变响应与无损材料在有效应力 $\tilde{\boldsymbol{\sigma}}$ 下的应变响应相同。基于一个形式为 $\psi = (1-D)\psi_0(\boldsymbol{\varepsilon})$ 的自由能（其中 $\psi_0$ 是无损材料的应变能），可以推导出柯西应力 $\boldsymbol{\sigma} = (1-D)\mathbb{C}_0:\boldsymbol{\varepsilon}$ 和有效应力 $\tilde{\boldsymbol{\sigma}} = \mathbb{C}_0:\boldsymbol{\varepsilon}$。这两者之间的关系为 ：
$$ \tilde{\boldsymbol{\sigma}} = \frac{\boldsymbol{\sigma}}{1-D} $$
这表明，有效应力总是大于名义上的柯西应力，物理上对应于由于损伤导致承载面积减小而引起的[应力集中](@entry_id:160987)。

理解**[刚度退化](@entry_id:202277)**（stiffness degradation）和**[应变软化](@entry_id:755491)**（strain softening）之间的区别至关重要：

- **[刚度退化](@entry_id:202277)** 是指由于损伤的存在（$D>0$），材料的弹性刚度降低。在固定的损伤水平下进行卸载/再加载，测得的弹性模量为 $(1-D)\mathbb{C}_0$，它小于初始模量 $\mathbb{C}_0$。这是一个状态属性 。

- **[应变软化](@entry_id:755491)** 是指在单调加载过程中，应力随应变的增加而减小的现象，即[应力-应变曲线](@entry_id:159459)的[切线](@entry_id:268870)模量 $\mathrm{d}\sigma/\mathrm{d}\varepsilon$ 变为负值。这不仅取决于损伤的存在，更取决于损伤的**[演化速率](@entry_id:202008)**。只有当损伤的增长速率 $\mathrm{d}D/\mathrm{d}\varepsilon$ 足够快，其导致的应力下降效应超过了弹性变形引起的应力增加效应时，才会发生宏观上的软化现象 。

### 连接尺度：均匀化简介

许多工程材料（如复合材料、多晶金属）在微观尺度上是高度非均匀的。**均匀化**（Homogenization）理论旨在从非均匀的微观结构出发，通过数学方法推导出等效的宏观均匀材料的[本构关系](@entry_id:186508)。

该理论的基石是**[尺度分离假设](@entry_id:1131494)**（scale separation assumption），即微观结构特征尺度 $\ell$ 远小于宏观问题特征尺度 $L$（例如，载荷或几何尺寸的变化尺度），即 $\varepsilon = \ell/L \ll 1$ 。

基于此假设，可以通过求解一个定义在**代表性体积元**（Representative Volume Element, RVE）上的边界值问题来计算宏观有效性能。

- **一阶均匀化**（First-order homogenization）是最常见的方法。它假设宏观应变场 $\mathbf{E}(\mathbf{X})$ 在RVE尺度上是均匀的。通过对RVE施加与宏观应变 $\mathbf{E}$ 一致的边界条件（如线性[位移边界条件](@entry_id:203261)或周期性边界条件），求解RVE内部的微观应[力场](@entry_id:147325)，然后通过体积平均得到宏观应力 $\mathbf{\Sigma}$。最终得到一个经典的（局部的）宏观[本构关系](@entry_id:186508) $\mathbf{\Sigma} = \mathbb{C}^{\text{eff}}:\mathbf{E}$，其中 $\mathbb{C}^{\text{eff}}$ 是有效[刚度张量](@entry_id:176588)。这种方法得到的宏观模型是一个标准的柯西连续体，不包含任何[尺度效应](@entry_id:153734) 。

- **二阶均匀化**（Second-order homogenization）或**[应变梯度理论](@entry_id:1132470)**（strain gradient theory）是更高阶的理论，它考虑了宏观应变场**梯度** $\nabla\mathbf{E}(\mathbf{X})$ 的影响。当宏观尺度 $L$ 与微观尺度 $\ell$ 不再相差悬殊，或者在[应力集中](@entry_id:160987)区域，[应变梯度](@entry_id:204192)变得显著时，就需要这种理论。二阶均匀化方法需要更复杂的RVE边界条件（如二次[位移边界条件](@entry_id:203261)）来包含[应变梯度](@entry_id:204192)的信息。其结果是一个更高阶的宏观连续体模型，其本构关系不仅依赖于应变，还依赖于[应变梯度](@entry_id:204192)，并引入了与[尺寸效应](@entry_id:153734)相关的新的有效材料参数 。