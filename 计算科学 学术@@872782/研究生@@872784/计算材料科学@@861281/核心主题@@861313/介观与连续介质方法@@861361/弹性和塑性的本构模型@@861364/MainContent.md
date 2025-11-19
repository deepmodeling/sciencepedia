## 引言
材料的力学行为是其在工程应用中性能表现的基础。准确预测材料在复杂载荷下的变形、应力响应乃至失效，是确保结构安全、优化产品设计和推动技术创新的核心。[弹塑性](@entry_id:193198)[本构模型](@entry_id:174726)正是实现这一目标的关键理论工具，它通过数学方程系统地描述了材料从可逆的弹性变形到不可逆的塑性流动的全过程。然而，从抽象的数学框架到解决实际工程问题的应用之间，往往存在着一条知识鸿沟。本篇文章旨在填补这一鸿沟，为读者提供一个关于[弹塑性](@entry_id:193198)[本构模型](@entry_id:174726)从基础理论到前沿应用的全面视角。

为实现这一目标，本文将分为三个核心章节。首先，在“原理与机制”一章中，我们将深入连续介质力学的核心，系统阐述描述变形的[运动学](@entry_id:173318)、不同的[应力与应变](@entry_id:137374)度量、弹性的[热力学](@entry_id:141121)基础以及塑性流动的基本法则，为理解本构模型奠定坚实的理论基础。接着，在“应用与交叉学科联系”一章中，我们将展示这些理论如何在结构工程、[材料科学](@entry_id:152226)和[多物理场耦合](@entry_id:171389)等不同领域中发挥作用，通过具体实例揭示模型的强大预测能力和跨学科的重要性。最后，“动手实践”部分将提供一系列精心设计的问题，引导读者将理论知识应用于具体的计算与分析中，从而深化理解并巩固所学。通过这一结构化的学习路径，读者将能够系统地掌握[弹塑性](@entry_id:193198)本构模型，并具备将其应用于学术研究和工程实践的能力。

## 原理与机制

本章旨在系统性地阐述弹性和塑性本构模型的基本原理与核心机制。继引言之后，我们将深入探讨描述[材料变形](@entry_id:169356)的运动学框架、应力与平衡的概念、弹性响应的[热力学](@entry_id:141121)基础，并进一步建立线性和[非线性弹性](@entry_id:185743)模型。随后，我们将转向不可[逆变](@entry_id:192290)形，介绍[经典塑性理论](@entry_id:167389)的框架，最后讨论与[材料不稳定性](@entry_id:172649)相关的模型失效及其[正则化方法](@entry_id:150559)等前沿论题。

### 变形[运动学](@entry_id:173318)：描述材料的运动

任何[本构模型](@entry_id:174726)的首要任务是精确描述材料的变形。在[连续介质力学](@entry_id:155125)中，这是通过运动学变量来完成的。

#### 变形梯度与[应变度量](@entry_id:755495)

考虑一个连续体，其在未变形的 **参考构型** 中占据区域 $\Omega_0$，物[质点](@entry_id:186768)的坐标用 $\mathbf{X}$ 表示。在变形后，该连续体占据 **当前构型** 中的区域 $\Omega$，物[质点](@entry_id:186768)的新坐标为 $\mathbf{x}$。描述这一过程的映射函数为 $\mathbf{x} = \boldsymbol{\chi}(\mathbf{X})$。

描述局部变形的核心物理量是 **变形梯度（deformation gradient）** $\mathbf{F}$，其定义为当前构型坐标对参考构型坐标的梯度：
$$
\mathbf{F} = \frac{\partial \mathbf{x}}{\partial \mathbf{X}}
$$
变形梯度 $\mathbf{F}$ 将参考构型中的一个无穷小线元 $d\mathbf{X}$ 映射到当前构型中的对应[线元](@entry_id:196833) $d\mathbf{x}$，即 $d\mathbf{x} = \mathbf{F} d\mathbf{X}$。它包含了关于局部拉伸、剪切和旋转的全部信息。变形梯度的[行列式](@entry_id:142978) $J = \det(\mathbf{F})$ 代表了局部体积的变化，即 $dV = J dV_0$，其中 $dV$ 和 $dV_0$ 分别是当前构型和参考构型中的无穷小体积元。

#### [小应变张量](@entry_id:754968)

在许多工程应用中，位移 $\mathbf{u} = \mathbf{x} - \mathbf{X}$ 及其梯度 $\nabla_{\mathbf{X}}\mathbf{u}$ 都非常小。在这种情况下，我们可以将变形运动学线性化，从而定义 **[无穷小应变张量](@entry_id:167211)（infinitesimal strain tensor）** 或称 **[小应变张量](@entry_id:754968)（small-strain tensor）** $\boldsymbol{\varepsilon}$：
$$
\boldsymbol{\varepsilon} = \frac{1}{2} \left( \nabla_{\mathbf{X}}\mathbf{u} + (\nabla_{\mathbf{X}}\mathbf{u})^{\mathrm{T}} \right) = \frac{1}{2} \left( \mathbf{F} + \mathbf{F}^{\mathrm{T}} - 2\mathbf{I} \right)
$$
其中 $\mathbf{I}$ 是二阶单位张量。[小应变张量](@entry_id:754968)因其简单性和线性而得到广泛应用。然而，它的一个根本性缺陷在于它并非 **客观的（objective）**，即它无法区分[刚体转动](@entry_id:191086)和真实变形。例如，考虑一个纯[刚体转动](@entry_id:191086) $\mathbf{x} = \mathbf{Q}\mathbf{X}$，其中 $\mathbf{Q}$ 是一个[旋转张量](@entry_id:191990)。此时的变形梯度为 $\mathbf{F} = \mathbf{Q}$。对应的[小应变张量](@entry_id:754968)为 $\boldsymbol{\varepsilon} = \frac{1}{2}(\mathbf{Q} + \mathbf{Q}^{\mathrm{T}} - 2\mathbf{I})$。除非 $\mathbf{Q} = \mathbf{I}$（即没有转动），否则 $\boldsymbol{\varepsilon}$ 不为零。这错误地将[刚体转动](@entry_id:191086)诠释为应变，因此[小应变张量](@entry_id:754968)仅适用于转动和应变均微小的情形 [@problem_id:3439444]。

#### [有限应变度量](@entry_id:185716)：[格林-拉格朗日应变](@entry_id:170427)

当变形（尤其是转动）较大时，我们需要一个客观的[应变度量](@entry_id:755495)。一种物理上直观的方法是比较变形前后无穷小[线元](@entry_id:196833)长度的平方变化。参考构型中线元 $d\mathbf{X}$ 的长度平方为 $ds_0^2 = d\mathbf{X} \cdot d\mathbf{X}$。变形后，其对应线元 $d\mathbf{x}$ 的长度平方为：
$$
ds^2 = d\mathbf{x} \cdot d\mathbf{x} = (\mathbf{F}d\mathbf{X}) \cdot (\mathbf{F}d\mathbf{X}) = d\mathbf{X}^{\mathrm{T}}\mathbf{F}^{\mathrm{T}}\mathbf{F}d\mathbf{X}
$$
我们定义 **右柯西-格林变形张量（right Cauchy-Green deformation tensor）** $\mathbf{C} = \mathbf{F}^{\mathrm{T}}\mathbf{F}$。于是，$ds^2 = d\mathbf{X}^{\mathrm{T}}\mathbf{C}d\mathbf{X}$。长度平方的改变为：
$$
ds^2 - ds_0^2 = d\mathbf{X}^{\mathrm{T}}(\mathbf{C} - \mathbf{I})d\mathbf{X}
$$
这启发我们定义 **[格林-拉格朗日应变张量](@entry_id:187745)（Green-Lagrange strain tensor）** $\mathbf{E}$：
$$
\mathbf{E} = \frac{1}{2}(\mathbf{C} - \mathbf{I}) = \frac{1}{2}(\mathbf{F}^{\mathrm{T}}\mathbf{F} - \mathbf{I})
$$
$\mathbf{E}$ 是一个完全定义在参考构型上的[拉格朗日量](@entry_id:174593)。至关重要的是，$\mathbf{E}$ 是客观的。如果在当前构型上叠加一个任意的刚体运动（旋转 $\mathbf{Q}$ 和平移 $\mathbf{c}$），即 $\mathbf{x}^+ = \mathbf{Q}\mathbf{x} + \mathbf{c}$，新的变形梯度为 $\mathbf{F}^+ = \mathbf{Q}\mathbf{F}$。然而，新的[右柯西-格林张量](@entry_id:174156) $\mathbf{C}^+ = (\mathbf{F}^+)^{\mathrm{T}}\mathbf{F}^+ = \mathbf{F}^{\mathrm{T}}\mathbf{Q}^{\mathrm{T}}\mathbf{Q}\mathbf{F} = \mathbf{F}^{\mathrm{T}}\mathbf{F} = \mathbf{C}$ 保持不变。因此，$\mathbf{E}$ 也不变，它正确地滤除了刚体运动的影响，只度量纯粹的变形 [@problem_id:3439444]。对于任何纯[刚体转动](@entry_id:191086) $\mathbf{F}=\mathbf{Q}$，我们有 $\mathbf{C} = \mathbf{Q}^{\mathrm{T}}\mathbf{Q} = \mathbf{I}$，从而 $\mathbf{E}=\mathbf{0}$，这符合物理直觉。

#### 体积与形状改变的分解

在许多材料中，抵[抗体](@entry_id:146805)积改变和抵抗形状改变的物理机制是不同的。因此，将变形分解为体积[部分和](@entry_id:162077)形状保持（等容）部分在数学上和物理上都极具价值。这可以通过对变形梯度 $\mathbf{F}$ 进行 **[乘法分解](@entry_id:199514)（multiplicative decomposition）** 实现 [@problem_id:3439461]：
$$
\mathbf{F} = J^{1/3} \bar{\mathbf{F}}
$$
这里，$J = \det(\mathbf{F})$ 是体积变化率。$J^{1/3}$ 代表一个均匀的、各向同性的体积膨胀或收缩。$\bar{\mathbf{F}} = J^{-1/3}\mathbf{F}$ 是 **[等容变形](@entry_id:196451)梯度（isochoric part of the deformation gradient）**，它描述了保持体积不变的形状改变，因为 $\det(\bar{\mathbf{F}}) = \det(J^{-1/3}\mathbf{F}) = (J^{-1/3})^3 \det(\mathbf{F}) = J^{-1}J = 1$。这种分解是构建现代[超弹性](@entry_id:159356)模型和[有限应变塑性](@entry_id:185352)模型的基础。

### 应力度量与平衡

力是引起变形的驱动因素，而 **应力（stress）** 则是描述材料内部相互作用力的集肤化度量。

#### 柯西[应力张量](@entry_id:148973)

最直观的应力度量是 **柯西应力张量（Cauchy stress tensor）** $\boldsymbol{\sigma}$，它定义在当前构型上。对于当前构型中的一个假想切割面，其[单位法向量](@entry_id:178851)为 $\mathbf{n}$，作用在该面上的力（称为 **面力 traction**） $\mathbf{t}$ 与 $\boldsymbol{\sigma}$ 的关系为：
$$
\mathbf{t} = \boldsymbol{\sigma}\mathbf{n}
$$
柯西应力描述的是单位变形后面积上的力，因此被称为“真实应力”。根据动量矩守恒，柯西[应力张量](@entry_id:148973)必须是对称的，即 $\boldsymbol{\sigma} = \boldsymbol{\sigma}^{\mathrm{T}}$。

#### 有限应变下的其他应力度量

在[有限应变理论](@entry_id:176941)中，将定义在当前构型上的柯西应力与定义在参考构型上的[应变度量](@entry_id:755495)（如 $\mathbf{E}$）直接关[联会](@entry_id:139072)遇到困难。为此，我们引入定义在参考构型上的应力度量。

**[第一皮奥拉-基尔霍夫应力](@entry_id:163971)（First Piola-Kirchhoff stress, PK1）** $\mathbf{P}$ 定义了单位参考面积上的名义面力 $\mathbf{T}_{\mathrm{R}}$，即 $\mathbf{T}_{\mathrm{R}} = \mathbf{P}\mathbf{N}$，其中 $\mathbf{N}$ 是参考构型中对应面的[单位法向量](@entry_id:178851)。通过力等效原则 $\mathbf{t} da = \mathbf{T}_{\mathrm{R}} dA$ 和Nanson关系式 $ \mathbf{n} da = J \mathbf{F}^{-\mathrm{T}} \mathbf{N} dA $，可以推导出 $\mathbf{P}$ 与 $\boldsymbol{\sigma}$ 的关系 [@problem_id:3439465]：
$$
\mathbf{P} = J \boldsymbol{\sigma} \mathbf{F}^{-\mathrm{T}}
$$
注意，$\mathbf{P}$ 通常是非对称的。它将参考构型中的法向量映射到当前构型中的力矢量，因此是一个“两点”张量。

为了得到一个完全定义在参考构型上且对称的应力度量，我们引入 **[第二皮奥拉-基尔霍夫应力](@entry_id:173163)（Second Piola-Kirchhoff stress, PK2）** $\mathbf{S}$。$\mathbf{S}$ 可以看作是将 $\mathbf{P}$ 通过 $\mathbf{F}^{-1}$ 从当前构型“[拉回](@entry_id:160816)”（pull back）到参考构型：
$$
\mathbf{S} = \mathbf{F}^{-1}\mathbf{P} = J \mathbf{F}^{-1} \boldsymbol{\sigma} \mathbf{F}^{-\mathrm{T}}
$$
$\mathbf{S}$ 的一个重要特性是，如果 $\boldsymbol{\sigma}$ 是对称的，那么 $\mathbf{S}$ 也是对称的。更重要的是，$\mathbf{S}$ 与[格林-拉格朗日应变张量](@entry_id:187745) $\mathbf{E}$ 构成一个 **[功共轭](@entry_id:194957)（work-conjugate）** 对。这意味着[应力功率](@entry_id:182907)（单位参考体积的内功率）可以简洁地表示为 $\dot{W}_{\text{int}} = \mathbf{S} : \dot{\mathbf{E}}$。这使得 $\mathbf{S}$ 和 $\mathbf{E}$ 成为构建有限应变超[弹性理论](@entry_id:184142)的理想选择。

### 弹性的[热力学](@entry_id:141121)基础

弹性材料的特性是其变形是可逆的，并且存在一个势函数（[应变能](@entry_id:162699)）来描述其状态。这与[热力学定律](@entry_id:202285)密切相关。

#### [热力学势](@entry_id:140516)

对于一个可逆的[热弹性](@entry_id:158447)过程，第一和第二热力学定律结合可以写出单位参考体积的内能密度 $\mathcal{U}$ 的[微分](@entry_id:158718)为 [@problem_id:3439481]：
$$
d\mathcal{U} = T dS + \boldsymbol{\sigma} : d\boldsymbol{\varepsilon}
$$
此式适用于小应变情况。其中 $T$ 是绝对温度，$S$ 是单位参考体积的熵密度。这个表达式揭示了[功共轭](@entry_id:194957)对的存在：$(T, S)$ 是[热力学](@entry_id:141121)对，$(\boldsymbol{\sigma}, \boldsymbol{\varepsilon})$ 是力学对。当以内能 $\mathcal{U}(S, \boldsymbol{\varepsilon})$ 为基本势函数时，其自然变量是 $S$ 和 $\boldsymbol{\varepsilon}$，[本构关系](@entry_id:186508)（constitutive equations）可通过求偏导得到：
$$
T = \frac{\partial \mathcal{U}}{\partial S}, \quad \boldsymbol{\sigma} = \frac{\partial \mathcal{U}}{\partial \boldsymbol{\varepsilon}}
$$

#### 勒让德变换与[本构关系](@entry_id:186508)

在实验中，我们通常控制温度 $T$ 和应变 $\boldsymbol{\varepsilon}$，或者温度 $T$ 和应力 $\boldsymbol{\sigma}$，而不是熵。为了将基本势函数转换为以这些更方便的变量为自然变量的形式，我们使用 **[勒让德变换](@entry_id:146727)（Legendre transform）**。

通过对 $(T,S)$ 对进行变换，我们得到 **亥姆霍兹自由能密度（Helmholtz free energy density）** $\psi(T, \boldsymbol{\varepsilon})$：
$$
\psi(T, \boldsymbol{\varepsilon}) = \mathcal{U} - TS
$$
其[全微分](@entry_id:171747)为 $d\psi = -S dT + \boldsymbol{\sigma} : d\boldsymbol{\varepsilon}$。因此，当以 $\psi(T, \boldsymbol{\varepsilon})$ 为势函数时，[本构关系](@entry_id:186508)变为：
$$
S = -\frac{\partial \psi}{\partial T}, \quad \boldsymbol{\sigma} = \frac{\partial \psi}{\partial \boldsymbol{\varepsilon}}
$$
这表明，在恒温条件下，应力是亥姆霍兹自由能对应变的导数。这正是弹性[本构模型](@entry_id:174726)的核心思想。

类似地，若同时对 $(T,S)$ 和 $(\boldsymbol{\sigma}, \boldsymbol{\varepsilon})$ 进行变换，则得到 **吉布斯自由能密度（Gibbs free energy density）** $G(T, \boldsymbol{\sigma})$ [@problem_id:3439481]：
$$
G(T, \boldsymbol{\sigma}) = \mathcal{U} - TS - \boldsymbol{\sigma}:\boldsymbol{\varepsilon}
$$
其[全微分](@entry_id:171747)为 $dG = -S dT - \boldsymbol{\varepsilon} : d\boldsymbol{\sigma}$。此时，应变可以通过对[吉布斯自由能](@entry_id:146774)求导得到：
$$
\boldsymbol{\varepsilon} = -\frac{\partial G}{\partial \boldsymbol{\sigma}}
$$
这种从一个标量势函数导出张量[本构关系](@entry_id:186508)的方法，保证了模型的[能量守恒](@entry_id:140514)和[路径无关性](@entry_id:163750)，是构建物理上自洽的弹性模型的基石。

### 弹性本构模型

基于[热力学](@entry_id:141121)框架，我们可以构建具体的弹性本构模型。

#### [线性弹性](@entry_id:166983)（胡克定律）

对于小应变情况，最简单也最常用的模型是[线性弹性](@entry_id:166983)，即应力与应变成[线性关系](@entry_id:267880)：$\boldsymbol{\sigma} = \mathbb{C} : \boldsymbol{\varepsilon}$，其中 $\mathbb{C}$ 是四阶 **[弹性张量](@entry_id:170728)（elasticity tensor）**。对于 **各向同性（isotropic）** 材料，其性质不随方向改变。基于[材料对称性](@entry_id:190289)和[张量对称性](@entry_id:191651)要求，可以证明[各向同性弹性](@entry_id:203237)张量 $\mathbb{C}$ 最多只能包含两个独立的材料常数 [@problem_id:3439484]。其[本构关系](@entry_id:186508)（**胡克定律 Hooke's law**）可以写成：
$$
\boldsymbol{\sigma} = \lambda \operatorname{tr}(\boldsymbol{\varepsilon}) \mathbf{I} + 2\mu \boldsymbol{\varepsilon}
$$
其中，$\lambda$ 和 $\mu$ 是 **拉梅常数（Lamé parameters）**。$\mu$ 也被称为 **剪切模量（shear modulus）** $G$。这些常数与工程中更常见的 **杨氏模量（Young's modulus）** $E$ 和 **泊松比（Poisson's ratio）** $\nu$ 有确定的关系：
$$
\lambda = \frac{E\nu}{(1+\nu)(1-2\nu)}, \quad \mu = \frac{E}{2(1+\nu)}
$$
这个关系可以通过分析简单的[单轴拉伸试验](@entry_id:195375)来建立 [@problem_id:3439484]。

#### 超弹性

对于有限应变，我们采用 **[超弹性](@entry_id:159356)（hyperelasticity）** 框架，即假设存在一个 **[应变能密度函数](@entry_id:755490)（strain-energy density function）** $W$，使得应力可以从其导出。为保证客观性，对于[各向同性材料](@entry_id:170678)，$W$ 必须是变形[张量不变量](@entry_id:203254)的函数。通常，我们将其写成[右柯西-格林张量](@entry_id:174156) $\mathbf{C}$ 的函数，即 $W(\mathbf{C})$。由于 $\mathbf{C}$ 本身是客观的，那么任何基于 $\mathbf{C}$ 及其[不变量](@entry_id:148850)（$I_1 = \operatorname{tr}(\mathbf{C})$, $I_2 = \frac{1}{2}((\operatorname{tr}(\mathbf{C}))^2 - \operatorname{tr}(\mathbf{C}^2))$, $I_3 = \det(\mathbf{C})$）的[应变能函数](@entry_id:178435)都将自动满足客观性要求 [@problem_id:3439518]。

从[应变能函数](@entry_id:178435) $W$ 出发，[功共轭](@entry_id:194957)的第二PK应力 $\mathbf{S}$ 可由下式得到：
$$
\mathbf{S} = 2 \frac{\partial W}{\partial \mathbf{C}}
$$
随后，柯西应力 $\boldsymbol{\sigma}$ 可通过“[前推](@entry_id:158718)”（push-forward）操作获得：
$$
\boldsymbol{\sigma} = \frac{1}{J} \mathbf{F} \mathbf{S} \mathbf{F}^{\mathrm{T}}
$$
我们可以利用体积-等容分解的思想来构建[应变能函数](@entry_id:178435)，例如，将其分解为体积部分 $U(J)$ 和等容部分 $\bar{W}(\bar{\mathbf{C}})$，其中 $\bar{\mathbf{C}} = J^{-2/3}\mathbf{C}$ 是等容[右柯西-格林张量](@entry_id:174156)。一个典型的例子是 **可压缩[新胡克模型](@entry_id:165881)（compressible neo-Hookean model）** [@problem_id:3439508]：
$$
\psi(\mathbf{F}) = \frac{\mu}{2}(\bar{I}_1 - 3) + \frac{\kappa}{2}(J - 1)^2
$$
其中 $\bar{I}_1 = \operatorname{tr}(\bar{\mathbf{C}})$, $\mu$ 是剪切模量，$\kappa$ 是 **[体积模量](@entry_id:160069)（bulk modulus）**。通过[链式法则](@entry_id:190743)对该函数求导，我们可以得到其柯西应力表达式：
$$
\boldsymbol{\sigma} = \frac{\mu}{J^{5/3}} \left( \mathbf{B} - \frac{1}{3} I_1 \mathbf{I} \right) + \kappa (J - 1) \mathbf{I}
$$
其中 $\mathbf{B} = \mathbf{F}\mathbf{F}^{\mathrm{T}}$ 是[左柯西-格林张量](@entry_id:186163)，而 $I_1 = \operatorname{tr}(\mathbf{B})$。第一项是[偏应力](@entry_id:163323)（迹为零），代表形状改变的贡献；第二项是球应力，代表体积改变的贡献 [@problem_id:3439461]。

对于橡胶等近乎不可压缩的材料，我们通常施加 **不可压缩约束（incompressibility constraint）** $J=1$。这可以通过引入一个 **拉格朗日乘子（Lagrange multiplier）** $p$（其物理意义是静水压力）来实现。例如，对于 **不可压缩[穆尼-里夫林模型](@entry_id:177592)（incompressible Mooney-Rivlin model）**，其[应变能](@entry_id:162699)为 $W = C_{10}(I_1-3) + C_{01}(I_2-3)$。其柯西应力表达式为 [@problem_id:3439518]：
$$
\boldsymbol{\sigma} = -p\mathbf{I} + 2(C_{10} + I_1 C_{01}) \mathbf{B} - 2C_{01}\mathbf{B}^2
$$
其中压力 $p$ 是一个待定场，需要通过求解[平衡方程](@entry_id:172166)和边界条件来确定。

#### [亚弹性模型](@entry_id:184632)的病态行为

在超弹性框架出现之前，人们曾尝试通过直接定义[客观应力率](@entry_id:199282)和[应变率](@entry_id:154778)之间的关系来构建[大变形](@entry_id:167243)弹性模型，这类模型被称为 **[亚弹性](@entry_id:204371)（hypoelasticity）**。一个典型的例子是使用 **Jaumann率** $\dot{\boldsymbol{\sigma}}^{\mathrm{J}}$：
$$
\dot{\boldsymbol{\sigma}}^{\mathrm{J}} = \dot{\boldsymbol{\sigma}} + \boldsymbol{\sigma}\mathbf{W} - \mathbf{W}\boldsymbol{\sigma} = \mathbb{C}:\mathbf{D}
$$
其中 $\mathbf{D}$ 是变形率张量，$\mathbf{W}$ 是[自旋张量](@entry_id:187346)。尽管Jaumann率是客观的，但这种增量式的定义通常是不可积的，即它不对应于一个[储能](@entry_id:264866)势函数。这会导致一些非物理的行为。一个著名的例子是，在纯[刚体转动](@entry_id:191086)下（$\mathbf{D}=\mathbf{0}$），通过对[亚弹性](@entry_id:204371)方程进行[数值积分](@entry_id:136578)会产生虚假的剪切应力 [@problem_id:3439479]。而正确的物理响应应该是[应力张量](@entry_id:148973)随物体刚性转动，不产生新的应力分量。这个病态行为凸显了超弹性模型作为描述弹性行为的优越性，因为它从一个势函数出发，天然地保证了[能量守恒](@entry_id:140514)和[路径无关性](@entry_id:163750)。

### 塑性：不可逆变形的建模

当应力超过某一阈值后，许多材料（尤其是金属）会发生不可逆的永久变形，这就是 **塑性（plasticity）**。

#### 基本概念

[经典塑性理论](@entry_id:167389)建立在几个核心概念之上：
1.  **屈服面（Yield Surface）**: 在应力空间中定义了一个弹性区域的边界，由[屈服函数](@entry_id:167970) $f(\boldsymbol{\sigma}, \boldsymbol{\alpha}) \le 0$ 描述。其中 $\boldsymbol{\alpha}$ 是一组描述材料内部状态的 **内变量（internal variables）**，如硬化参数。当 $f  0$ 时，材料处于弹性状态；当 $f=0$ 时，材料达到屈服，可能发生[塑性流动](@entry_id:201346)。$f > 0$ 的状态在物理上是不允许的。
2.  **[应变分解](@entry_id:186005)（Strain Decomposition）**: 假设总应变（或应变率）可以加和分解为弹性部分和塑性部分：$\dot{\boldsymbol{\varepsilon}} = \dot{\boldsymbol{\varepsilon}}^{e} + \dot{\boldsymbol{\varepsilon}}^{p}$。
3.  **[流动法则](@entry_id:177163)（Flow Rule）**: 规定了塑性应变率 $\dot{\boldsymbol{\varepsilon}}^{p}$ 的方向。对于 **关联塑性（associative plasticity）**，[塑性流动](@entry_id:201346)方向垂直于[屈服面](@entry_id:175331)：
    $$
    \dot{\boldsymbol{\varepsilon}}^{p} = \dot{\lambda} \frac{\partial f}{\partial \boldsymbol{\sigma}}
    $$
    其中 $\dot{\lambda} \ge 0$ 是一个标量，称为 **塑性乘子率（plastic multiplier rate）**，它的大小决定了塑性流动的速率。
4.  **硬化法则（Hardening Rule）**: 描述了[屈服面](@entry_id:175331)如何随着塑性变形而演化（例如，通过内变量 $\boldsymbol{\alpha}$ 的演化）。

#### [J2流动理论](@entry_id:190689)与[一致性条件](@entry_id:637057)

对于金属材料，一个广泛应用的理论是基于 **von Mises** [屈服准则](@entry_id:193897)的 **[J2流动理论](@entry_id:190689)**。该理论假设屈服仅取决于应力偏量 $\mathbf{s} = \boldsymbol{\sigma} - \frac{1}{3}\operatorname{tr}(\boldsymbol{\sigma})\mathbf{I}$ 的第二[不变量](@entry_id:148850) $J_2 = \frac{1}{2}\mathbf{s}:\mathbf{s}$。[屈服函数](@entry_id:167970)通常写成：
$$
f = \sigma_{\mathrm{eq}} - \sigma_y(p) = 0
$$
其中 $\sigma_{\mathrm{eq}} = \sqrt{3J_2} = \sqrt{\frac{3}{2}\mathbf{s}:\mathbf{s}}$ 是[von Mises等效应力](@entry_id:756574)，$\sigma_y$ 是当前屈服强度，它依赖于累积等效塑性应变 $p$。对于线性[各向同性硬化](@entry_id:164486)，$\sigma_y = \sigma_{y0} + H p$，其中 $H$ 是 **[硬化](@entry_id:177483)模量（hardening modulus）**。

在塑性加载过程中，应力点必须始终停留在[屈服面](@entry_id:175331)上，这意味着[屈服函数](@entry_id:167970)的时间导数必须为零，即 **[一致性条件](@entry_id:637057)（consistency condition）** $\dot{f}=0$。利用链式法则展开此条件，并结合流动法则和[硬化](@entry_id:177483)法则，我们可以推导出塑性乘子率 $\dot{\lambda}$ 的表达式 [@problem_id:3439475]：
$$
\dot{\lambda} = \frac{\boldsymbol{N} : \dot{\boldsymbol{s}}_{\mathrm{tr}}}{3G + H}
$$
其中 $\boldsymbol{N} = \frac{\partial f}{\partial \boldsymbol{\sigma}} = \sqrt{\frac{3}{2}} \frac{\mathbf{s}}{\|\mathbf{s}\|}$ 是屈服面的单位法向，$\dot{\boldsymbol{s}}_{\mathrm{tr}} = 2G \operatorname{dev}(\dot{\boldsymbol{\varepsilon}})$ 是 **弹性试探偏应力率（elastic trial deviatoric stress rate）**。这个方程是率无关塑性[数值算法](@entry_id:752770)的核心，它将未知的[塑性流动](@entry_id:201346)大小 $\dot{\lambda}$ 与已知的总应变率 $\dot{\boldsymbol{\varepsilon}}$ 联系起来。

在[有限应变塑性](@entry_id:185352)中，通常采用[乘法分解](@entry_id:199514) $\mathbf{F} = \mathbf{F}_e \mathbf{F}_p$，其中 $\mathbf{F}_e$ 和 $\mathbf{F}_p$ 分别代表弹性和塑性变形梯度。一个常见的假设是[塑性流动](@entry_id:201346)是等容的，即 $\det(\mathbf{F}_p)=1$。这意味着所有体积变化都是弹性的，即 $J = \det(\mathbf{F}) = \det(\mathbf{F}_e)$。因此，弹性响应可以由一个依赖于 $\mathbf{F}_e$ 的[超弹性](@entry_id:159356)模型来描述，这自然地将之前讨论的超弹性和塑性理论结合起来 [@problem_id:3439461]。

### 高等论题：稳定性与正则化

一个有效的[本构模型](@entry_id:174726)不仅要能描述材料行为，还必须保证其在数学上是适定的（well-posed），并能反映物理上的稳定性。

#### [热力学稳定性](@entry_id:142877)（[德鲁克公设](@entry_id:180546)）

为了保证[本构模型](@entry_id:174726)的物理合理性，它应满足一定的稳定性准则。**[德鲁克公设](@entry_id:180546)（Drucker's postulates）** 为此提供了充分条件。对于率无关塑性，这些条件可以简化为对[屈服函数](@entry_id:167970)和硬化法则的要求 [@problem_id:3439464]：
1.  **[屈服面](@entry_id:175331)在应力空间中是凸的（convex）**。这保证了对于任何允许的应力状态，塑性[应变率](@entry_id:154778)的方向是唯一的，并且满足 $(\boldsymbol{\sigma} - \boldsymbol{\sigma}^*) : \dot{\boldsymbol{\varepsilon}}^p \ge 0$，其中 $\boldsymbol{\sigma}^*$ 是[屈服面](@entry_id:175331)内的任意应力点。
2.  **硬化法则是非软化的**。这意味着在塑性加载过程中，外力所做的塑性功增量必须是非负的，即 $\dot{\boldsymbol{\sigma}} : \dot{\boldsymbol{\varepsilon}}^p \ge 0$。对于[各向同性硬化](@entry_id:164486)，这通常意味着硬化模量 $H \ge 0$。

如果屈服面是非凸的，增量问题的解可能不再唯一，这预示着潜在的[材料不稳定性](@entry_id:172649) [@problem_id:3439464]。

#### [应变软化](@entry_id:755491)与椭圆性丧失

当材料表现出 **[应变软化](@entry_id:755491)（strain softening）** 行为时（即[硬化](@entry_id:177483)模量 $H  0$），情况会变得更加复杂。尽管在一定程度的软化下模型仍能保持稳定，但当软化达到某个临界值时，描述增量问题的[偏微分方程组](@entry_id:172573)会丧失 **椭圆性（ellipticity）**。

椭圆性的丧失是一个数学上的灾难，它意味着边界值问题变得 **不适定（ill-posed）**。其物理表现是变形会倾向于集中在宽度为零的无限窄带中，即 **[应变局部化](@entry_id:176973)（strain localization）** 或[剪切带](@entry_id:183352)。在数值计算中，这表现为解对网格的病态依赖性：网格越细，[剪切带](@entry_id:183352)越窄，[应力应变](@entry_id:204183)响应越软，无法得到收敛的物理解。

临界软化模量 $h_{cr}$ 的值取决于材料的弹性常数和应力状态。例如，在平面应变纯剪切下，对于一个与坐标轴成45度角的剪切带，当软化模量达到临界值 $h_{cr} = -\frac{3\mu(\lambda+\mu)}{\lambda+2\mu}$ 时，控制方程的[声学张量](@entry_id:200089)将出现零[特征值](@entry_id:154894)，标志着椭圆性的丧失 [@problem_id:3439462]。

#### [正则化方法](@entry_id:150559)

为了解决由软化引起的[模型不适定性](@entry_id:170436)问题，需要引入 **正则化（regularization）** 技术。这些方法通过在经典（局部）[本构模型](@entry_id:174726)中引入一个 **[内禀长度尺度](@entry_id:750789)（internal length scale）** 来实现。

一种有效的[正则化方法](@entry_id:150559)是 **[梯度增强模型](@entry_id:162584)（gradient-enhanced models）**。例如，在[梯度塑性](@entry_id:749995)中，我们假设自由能不仅依赖于局部内变量（如 $\kappa$），还依赖于其空间梯度（如 $|\nabla\kappa|$）。一个典型的增广自由能形式可以包含一个梯度项 $\frac{1}{2} \eta \ell^2 |\nabla\kappa|^2$，其中 $\eta$ 是一个梯度模量，$\ell$ 是材料的[内禀长度尺度](@entry_id:750789) [@problem_id:3439462]。

这个梯度项起到了惩罚应变剧烈变化的作用，从而阻止了[应变集中](@entry_id:187026)到零宽度区域。它在数学上保证了即使在软化区，控制方程依然保持椭圆性，从而使边界值问题始终适定。在物理上，它使得预测的[剪切带](@entry_id:183352)具有与[内禀长度尺度](@entry_id:750789) $\ell$ 相当的有限宽度，从而能够得到网格无关的、具有物理意义的模拟结果。