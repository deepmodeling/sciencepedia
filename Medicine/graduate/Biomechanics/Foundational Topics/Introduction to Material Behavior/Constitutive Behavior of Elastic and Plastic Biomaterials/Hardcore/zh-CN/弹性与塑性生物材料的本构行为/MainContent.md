## 引言
[生物材料](@entry_id:161584)的力学行为对其在生理环境中的功能至关重要。无论是支撑身体的骨骼、泵送血液的[心肌](@entry_id:924326)，还是用于修复组织的工程支架，它们如何在外力作用下变形、流动和响应，都决定了其成败。精确描述这种复杂的力学行为，正是[生物材料](@entry_id:161584)[本构关系](@entry_id:186508)研究的核心任务。然而，[生物材料](@entry_id:161584)往往表现出高度[非线性](@entry_id:637147)、各向异性、时间依赖性以及不可恢复的变形特性，这为建立准确的数学模型带来了巨大挑战。本文旨在系统性地填补这一知识鸿沟，为读者提供一个从基本原理到前沿应用的全面视角。

在接下来的内容中，我们将踏上一段结构化的学习之旅。首先，在“原理与机制”一章中，我们将深入[连续介质力学](@entry_id:155125)的核心，建立描述弹性、粘弹性、[孔隙弹性](@entry_id:174851)及塑性行为的数学与物理基础。随后，在“应用与交叉学科联系”一章，我们将展示这些理论如何应用于[组织工程](@entry_id:142974)、[失效分析](@entry_id:266723)和生长重塑等实际问题中，揭示理论与实践的紧密联系。最后，通过“动手实践”部分，您将有机会亲手实现和探索这些模型，将抽象的理论转化为具体的计算能力。本章将从本构理论的基石——变形运动学和[客观性原理](@entry_id:185412)讲起，为您后续的学习奠定坚实的基础。

## 原理与机制

本章旨在系统性地阐述描述[生物材料](@entry_id:161584)力学行为的[本构关系](@entry_id:186508)背后的核心原理与关键机制。与绪论章节的宏观介绍不同，本章将深入到连续介质力学的数学框架中，从变形的运动学描述出发，逐步建立弹性、粘弹性、孔隙弹性及塑性行为的理论模型。我们将重点关注这些理论的物理基础、数学表述的严谨性，以及它们在模拟真实生物组织（如软组织、骨骼和凝胶）行为时的适用性与局限性。

### 本构关系的基本原理

任何严谨的本构理论都必须建立在普适的物理原理之上。在进入具体的材料模型之前，我们首先讨论两个最为基础的支柱：变形运动学和材料坐标系无关性原理。

#### 变形运动学：应变的度量

描述一个物体如何从其初始状态（**参考构型**）运动到当前状态（**当前构型**）是连续介质力学的第一步。我们将参考构型中的一个物[质点](@entry_id:186768)的位置向量记为 $\mathbf{X}$，当前构型中的位置记为 $\mathbf{x}$。描述这一过程的映射函数为 $\mathbf{x} = \boldsymbol{\chi}(\mathbf{X}, t)$。

所有关于局部变形的信息都蕴含在一个称为**变形梯度** (deformation gradient) 的[二阶张量](@entry_id:199780) $\mathbf{F}$ 中：
$$ \mathbf{F} = \frac{\partial \mathbf{x}}{\partial \mathbf{X}} $$
变形梯度 $\mathbf{F}$ 度量了物[质点](@entry_id:186768)邻域的局部变形（拉伸、剪切和旋转）。然而，$\mathbf{F}$ 本身包含[刚体转动](@entry_id:191086)，这对于描述材料的内在变形（即引起应力的变形）来说是不便的。为了只描述拉伸和剪切，我们需要引入不包含[刚体转动](@entry_id:191086)的[应变度量](@entry_id:755495)。

一个关键的客观度量是**右柯西-格林变形张量** (right Cauchy-Green deformation tensor) $\mathbf{C}$，定义为：
$$ \mathbf{C} = \mathbf{F}^{\top}\mathbf{F} $$
$\mathbf{C}$ 是一个对称正定张量，它完全描述了从参考构型到当前构型的局部拉伸和剪切，但剔除了叠加在变形之上的[刚体转动](@entry_id:191086)信息。基于 $\mathbf{C}$，我们可以定义**[格林-拉格朗日应变张量](@entry_id:187745)** (Green-Lagrange strain tensor) $\mathbf{E}$：
$$ \mathbf{E} = \frac{1}{2}(\mathbf{C} - \mathbf{I}) = \frac{1}{2}(\mathbf{F}^{\top}\mathbf{F} - \mathbf{I}) $$
其中 $\mathbf{I}$ 是单位张量。$\mathbf{E}$ 是一个在参考构型上定义的张量，对于有限变形（large deformations）是完全通用的。

在许多生物力学问题中，变形非常小。若[位移场](@entry_id:141476)为 $\mathbf{u}(\mathbf{X}) = \mathbf{x} - \mathbf{X}$，则变形梯度为 $\mathbf{F} = \mathbf{I} + \nabla \mathbf{u}$。当[位移梯度](@entry_id:165352) $\nabla \mathbf{u}$ 的范数远小于1时（$\lVert \nabla \mathbf{u} \rVert \ll 1$），我们可以对 $\mathbf{E}$ 进行线性化。代入 $\mathbf{F}$ 的表达式：
$$ \mathbf{E} = \frac{1}{2}((\mathbf{I} + \nabla \mathbf{u})^{\top}(\mathbf{I} + \nabla \mathbf{u}) - \mathbf{I}) = \frac{1}{2}(\nabla \mathbf{u} + (\nabla \mathbf{u})^{\top} + (\nabla \mathbf{u})^{\top}\nabla \mathbf{u}) $$
忽略高阶项 $(\nabla \mathbf{u})^{\top}\nabla \mathbf{u}$，我们得到**[无穷小应变张量](@entry_id:167211)** (infinitesimal strain tensor) $\boldsymbol{\varepsilon}$ ：
$$ \boldsymbol{\varepsilon} = \frac{1}{2}(\nabla \mathbf{u} + (\nabla \mathbf{u})^{\top}) $$
这个[对称张量](@entry_id:148092)是[线性弹性](@entry_id:166983)理论的基础。选择合适的[应变度量](@entry_id:755495)（$\mathbf{E}$ 用于有限应变，$\boldsymbol{\varepsilon}$ 用于小应变）是建立任何本构关系的第一步 。

#### 材料坐标系无关性原理 (客观性)

**材料坐标系无关性原理** (principle of material frame indifference)，或称**[客观性原理](@entry_id:185412)** (objectivity)，是[连续介质力学](@entry_id:155125)的一条基本公理。它要求本构关系（即应力与应变之间的关系）不能依赖于观察者。换句话说，如果在一个已发生变形的物体上再叠加一个刚体运动（平移和旋转），材料内部的应力状态不应改变。

数学上，这意味着[本构关系](@entry_id:186508)的形式在不同的坐标系下必须保持不变。对于柯西应力 $\boldsymbol{\sigma}$，如果其本构关系是变形梯度 $\mathbf{F}$ 的函数 $\boldsymbol{\sigma} = \mathcal{G}(\mathbf{F})$，那么对于任意的[刚体](@entry_id:1131033)旋转 $\mathbf{Q}$（一个正交张量），该函数必须满足：
$$ \mathcal{G}(\mathbf{Q}\mathbf{F}) = \mathbf{Q}\mathcal{G}(\mathbf{F})\mathbf{Q}^{\top} $$
这一要求极大地限制了本构函数的可能形式。一个不满足[客观性原理](@entry_id:185412)的本构模型是无物理意义的，因为它会预测在纯[刚体](@entry_id:1131033)旋转下产生虚假的应力。

为了阐明这一点，我们来构造一个违反[客观性原理](@entry_id:185412)的反例 。考虑一个假设的二维弹性定律：
$$ \boldsymbol{\sigma} = \lambda\,\mathrm{tr}(\mathbf{F}-\mathbf{I})\,\mathbf{I} + 2\mu\,\mathrm{sym}(\mathbf{F}-\mathbf{I}) $$
其中 $\mathrm{sym}(\cdot)$ 表示取对称部分。现在，我们考虑一个纯[刚体](@entry_id:1131033)旋转，其变形梯度就是[旋转矩阵](@entry_id:140302)本身 $\mathbf{F} = \mathbf{R}(\theta)$：
$$ \mathbf{R}(\theta) = \begin{pmatrix} \cos\theta & -\sin\theta \\ \sin\theta & \cos\theta \end{pmatrix} $$
由于这是一个纯旋转，没有任何实际的[材料变形](@entry_id:169356)，我们期望应力为零。然而，将 $\mathbf{F} = \mathbf{R}(\theta)$ 代入上述本构律，经过计算可得：
$$ \boldsymbol{\sigma} = 2(\lambda + \mu)(\cos\theta - 1)\mathbf{I} $$
显然，只要旋转角 $\theta$ 不是 $2\pi$ 的整数倍，$\cos\theta \neq 1$，就会产生一个非零的应力 $\boldsymbol{\sigma}$。例如，当旋转 $90$ 度（$\theta = \pi/2$）时，$\cos\theta = 0$，应力为 $\boldsymbol{\sigma} = -2(\lambda + \mu)\mathbf{I}$，这是一个显著的[静水压力](@entry_id:275365)。这清楚地表明该本构律是错误的，因为它错误地将[刚体](@entry_id:1131033)旋转“感知”为变形。

为了满足[客观性原理](@entry_id:185412)，[本构关系](@entry_id:186508)必须通过客观的张量来建立，例如[右柯西-格林张量](@entry_id:174156) $\mathbf{C}$。$\mathbf{C}$ 在[刚体](@entry_id:1131033)旋转下保持不变，因此任何以 $\mathbf{C}$ 为变量的函数都自动满足客观性要求 。

### [生物材料](@entry_id:161584)的弹性行为

弹性是指材料在移除外力后能完全恢复其原始形状的特性。这是对[生物材料](@entry_id:161584)在生理载荷范围内行为进行建模的起点。

#### [线性弹性](@entry_id:166983) (小应变理论)

当材料的变形和转动都足够小时，我们可以使用线性化的运动学和[本构关系](@entry_id:186508)。如前所述，此时的[应变度量](@entry_id:755495)是[无穷小应变张量](@entry_id:167211) $\boldsymbol{\varepsilon}$。

对于一个**各向同性** (isotropic) 的线弹性材料，其[应力-应变关系](@entry_id:274093)，即**胡克定律** (Hooke's law)，可以由两个独立的材料常数完全确定。最常见的形式是使用拉梅参数 (Lamé parameters) $\lambda$ 和 $\mu$：
$$ \boldsymbol{\sigma} = \lambda\,\mathrm{tr}(\boldsymbol{\varepsilon})\,\mathbf{I} + 2\mu\,\boldsymbol{\varepsilon} $$
这个关系式保证了对于对称的[应变张量](@entry_id:1132487) $\boldsymbol{\varepsilon}$，产生的柯西[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ 也是对称的，这与角动量守恒的要求一致。参数 $\mu$ 通常被称为**剪切模量** (shear modulus)，它反映了材料抵抗形状改变的能力。参数 $\lambda$ 与材料的体积响应有关，它和 $\mu$ 共同决定了**体积模量** (bulk modulus) $K = \lambda + \frac{2}{3}\mu$，后者反映了材料抵抗体积改变的能力 。尽管许多生物软组织近乎不可压缩，但[线性弹性](@entry_id:166983)模型仍是分析骨骼等硬组织或在极小变形下分析软组织行为的有效工具。

#### [超弹性](@entry_id:159356) ([有限应变理论](@entry_id:176941))

许多生物软组织（如皮肤、肌肉、血管）在生理功能中会经历巨大的变形，此时[线性弹性](@entry_id:166983)理论不再适用。对于这类材料，我们通常采用**[超弹性](@entry_id:159356)** (hyperelasticity) 理论。其核心思想是假设存在一个**[应变能密度函数](@entry_id:755490)** (strain-energy density function) $\psi$，它表示单位参考体积内储存的弹性能。材料的应力状态完全由该函数对变形的导数确定。

这种方法的一个主要优点是，只要应变能函数基于客观的[应变度量](@entry_id:755495)（如 $\mathbf{C}$）构建，所导出的[本构关系](@entry_id:186508)就自动满足[客观性原理](@entry_id:185412)和[热力学](@entry_id:172368)第二定律（对于弹性过程）。对于[超弹性材料](@entry_id:190241)，**[第二皮奥拉-基尔霍夫应力](@entry_id:173163)** (second Piola-Kirchhoff stress) $\mathbf{S}$ 与[格林-拉格朗日应变](@entry_id:170427) $\mathbf{E}$ 是[功共轭](@entry_id:194957)的，其关系为 ：
$$ \mathbf{S} = \frac{\partial \psi}{\partial \mathbf{E}} = 2\frac{\partial \psi}{\partial \mathbf{C}} $$
而我们更熟悉的柯西应力 $\boldsymbol{\sigma}$ 可以通过 $\mathbf{S}$ 转换得到：$\boldsymbol{\sigma} = \frac{1}{J}\mathbf{F}\mathbf{S}\mathbf{F}^{\top}$，其中 $J = \det(\mathbf{F})$ 是体积变化率。

**各向同性[超弹性](@entry_id:159356)：以可压缩 Neo-Hookean 模型为例**

一个广泛用于模拟橡胶和软组织的模型是 Neo-Hookean 模型。考虑一个可压缩的 Neo-Hookean 材料，其[应变能函数](@entry_id:178435)可以写成 ：
$$ \psi(I_{1},J) = \frac{\mu}{2}(I_{1} - 3) - \mu \ln J + \frac{\kappa}{2}(\ln J)^{2} $$
其中 $I_1 = \mathrm{tr}(\mathbf{C})$ 是 $\mathbf{C}$ 的第一不变量，$\mu$ 和 $\kappa$ 是材料参数。这里的 $\psi$ 分为两部分：一部分与形状改变有关（由 $I_1$ 项主导），另一部分与体积改变有关（由 $J$ 项主导）。

通过[链式法则](@entry_id:190743)和张量恒等式，我们可以从这个 $\psi$ 导出柯西应力 $\boldsymbol{\sigma}$ 的表达式：
1.  首先计算[第一皮奥拉-基尔霍夫应力](@entry_id:163971) $\mathbf{P} = \frac{\partial \psi}{\partial \mathbf{F}}$：
    $$ \mathbf{P} = \mu \mathbf{F} + (\kappa \ln J - \mu) \mathbf{F}^{-\top} $$
2.  然后通过坐标转换得到柯西应力 $\boldsymbol{\sigma} = \frac{1}{J}\mathbf{P}\mathbf{F}^{\top}$：
    $$ \boldsymbol{\sigma} = \frac{\mu}{J}\mathbf{B} + \frac{1}{J}(\kappa \ln J - \mu)\mathbf{I} $$
    其中 $\mathbf{B} = \mathbf{F}\mathbf{F}^{\top}$ 是**左柯西-格林变形张量**。

在这个模型中，参数 $\mu$ 和 $\kappa$ 具有明确的物理意义。$\mu$ 是材料的**剪切模量**，主导了材料在保持体积不变的情况下的形状改变响应（剪切响应）。$\kappa$ 则主导了材料的**体积响应**，与体积模量密切相关，量化了材料抵抗压缩或膨胀的能力。对于含水量高的软组织，其抗体积变化能力远强于抗形状变化能力，因此通常有 $\kappa \gg \mu$ 。

**[各向异性超弹性](@entry_id:191276)：横观各向同性模型**

许多[生物材料](@entry_id:161584)，如肌腱、韧带和肌肉，由于其内部的纤维结构而表现出显著的**各向异性** (anisotropy)。为了对此进行建模，我们需要在应变能函数中引入描述材料结构方向的信息。

对于由单一族[纤维增强](@entry_id:194439)的材料（例如肌腱），我们可以将其模型化为**横观各向同性** (transversely isotropic) 材料。设纤维在参考构型中的方向由[单位向量](@entry_id:165907) $\mathbf{a}$ 表示。我们可以构造一个**结构张量** $\mathbf{M} = \mathbf{a} \otimes \mathbf{a}$。[应变能函数](@entry_id:178435) $\psi$ 不仅依赖于通常的[应变不变量](@entry_id:190518)（如 $I_1 = \mathrm{tr}(\mathbf{C})$），还必须依赖于描述纤维拉伸的混合不变量。最重要的一个混合不变量是 $I_4$：
$$ I_4 = \mathbf{a} \cdot \mathbf{C} \mathbf{a} = \lambda_f^2 $$
其中 $\lambda_f$ 是纤维方向的拉伸比。一个典型的横观各向同性应变能函数可以写成 $\psi = \psi(I_1, I_4)$  。

在这种框架下，[第二皮奥拉-基尔霍夫应力](@entry_id:173163) $\mathbf{S}$ 可以通过链式法则导出：
$$ \mathbf{S} = 2\frac{\partial \psi}{\partial \mathbf{C}} = 2\left(\frac{\partial \psi}{\partial I_1}\frac{\partial I_1}{\partial \mathbf{C}} + \frac{\partial \psi}{\partial I_4}\frac{\partial I_4}{\partial \mathbf{C}}\right) = 2(\psi_1 \mathbf{I} + \psi_4 \mathbf{M}) $$
其中 $\psi_1 = \frac{\partial \psi}{\partial I_1}$ 和 $\psi_4 = \frac{\partial \psi}{\partial I_4}$。这个表达式清晰地显示了应力如何分解为来自基质的各向同性部分（与 $\mathbf{I}$ 相关）和来自纤维的各向异性部分（与 $\mathbf{M}$ 相关）。此外，还可以进一步求导得到四阶的**[材料弹性](@entry_id:751729)张量** $\mathbb{A} = \frac{\partial \mathbf{S}}{\partial \mathbf{C}}$，这在[有限元分析](@entry_id:138109)的数值实现中至关重要 。

### 时间依赖性行为：粘弹性

[生物材料](@entry_id:161584)的响应通常是时间依赖的。当施加一个恒定的应变时，应力会随时间逐渐减小（**[应力松弛](@entry_id:159905)**）；当施加一个恒定的应力时，应变会随时间逐渐增大（**蠕变**）。这种行为被称为**粘弹性** (viscoelasticity)。

#### [线性粘弹性](@entry_id:181219)

在小应变范围内，我们可以使用[线性粘弹性](@entry_id:181219)理论。该理论的基石是**Boltzmann [叠加原理](@entry_id:144649)**，它指出在任意时刻的应力是所有过去应变增量所引起响应的线性总和。这可以通过一个**[遗传积分](@entry_id:186265)** (hereditary integral) 来数学化地表达 。如果应变历史为 $\varepsilon(t)$，那么 $t$ 时刻的应力 $\sigma(t)$ 可以表示为[应变率](@entry_id:154778) $\dot{\varepsilon}(t)$ 与一个材料核[函数的卷积](@entry_id:186055)：
$$ \sigma(t) = \int_{0}^{t} G(t-\tau)\,\dot{\varepsilon}(\tau)\,d\tau $$
这里的材料核函数 $G(t)$ 被称为**松弛模量** (relaxation modulus)。它的物理意义可以通过一个思想实验来理解：在 $t=0$ 时刻对材料施加一个单位阶跃应变 $\varepsilon(t) = H(t)$。在这种情况下，应力响应就是松弛模量本身：$\sigma(t) = G(t)$。

因此，$G(t)$ 描述了材料在保持恒定应变下的应力衰减历史。对于典型的生物软组织，松弛模量 $G(t)$ 具有以下特征：
-   它是一个正的、非增函数，反映了[能量耗散](@entry_id:147406)过程。
-   初始值 $G(0^+)$ 是**瞬时模量**，代表材料最硬的、瞬间的响应。
-   最终值 $G(\infty)$ 是**平衡模量**，代表[应力松弛](@entry_id:159905)完毕后，仅由固体骨架承担的长期弹性响应。对于固体， $G(\infty) > 0$ 。

### [多物理场](@entry_id:164478)行为：[孔隙弹性](@entry_id:174851)

许多生物软组织是多孔的固体基质（如胶原蛋白和弹性蛋白网络），其孔隙中充满了间质流体（主要是水）。这些材料的力学行为受到固体基质变形与流体在孔隙中流动之间复杂的相互作用的强烈影响。**[双相混合物理论](@entry_id:1121663)** (biphasic mixture theory)，或称**[孔隙弹性理论](@entry_id:195706)** (poroelasticity)，为描述这种行为提供了框架。

该理论将组织视为两种连续介质的叠加：一个弹性固体相和一个流体相。其核心方程源于质量和动量守恒，并遵循特定的本构假设 。
1.  **[有效应力原理](@entry_id:171867)** (Principle of Effective Stress): 总的宏观应力（柯西应力 $\boldsymbol{\sigma}$）是固体基质承担的**[有效应力](@entry_id:198048)** $\boldsymbol{\sigma}^s$ 和流体承担的孔隙压力 $p$ 的总和。采用工程中常用的“拉为正”的应力约定和“压为正”的压力约定，[流体压力](@entry_id:142203) $p$ 产生的应力为 $-p\mathbf{I}$。因此，总应力为：
    $$ \boldsymbol{\sigma} = \boldsymbol{\sigma}^{s} - p \mathbf{I} $$
    这个原理至关重要，因为它表明是有效应力而非总应力导致固体基质的变形。
2.  **[达西定律](@entry_id:153223)** (Darcy's Law): 描述了流体相对于固体骨架的流动通量 $\mathbf{q}$。流动的驱动力是压力梯度 $\nabla p$。根据[热力学](@entry_id:172368)第二定律，耗散（由流体与固体之间的摩擦引起）必须是非负的。这要求流动必须从高压区流向低压区，从而确定了达西定律的形式：
    $$ \mathbf{q} = - \mathbf{k} \nabla p $$
    其中 $\mathbf{k}$ 是**渗透率张量** (permeability tensor)，它是一个[正定张量](@entry_id:204409)。负号确保了流动方向与压力梯度方向相反，满足物理直觉和[热力学约束](@entry_id:755911) 。

### 非弹性行为：塑性

当载荷超过某个阈值时，材料会发生不可恢复的变形，这种现象称为**塑性** (plasticity)。在[生物材料](@entry_id:161584)中，这可能对应于微观结构的重组、损伤或[生长与重塑](@entry_id:1125833)等过程。

#### 塑性理论基础

塑性理论的核心是**[屈服面](@entry_id:175331)** (yield surface) 的概念，它在[应力空间](@entry_id:199156)中定义了一个纯弹性行为的区域。当应力状态位于[屈服面](@entry_id:175331)内部时，材料响应是弹性的；当应力状态达到[屈服面](@entry_id:175331)时，塑性变形开始发生。

在描述[弹塑性](@entry_id:193198)变形时，如何分解总变形是关键。
-   **小应变塑性**：在小应变理论中，总应变张量 $\boldsymbol{\varepsilon}$ 通常被**加法分解** (additive decomposition) 为弹性部分 $\boldsymbol{\varepsilon}^e$ 和塑性部分 $\boldsymbol{\varepsilon}^p$：
    $$ \boldsymbol{\varepsilon} = \boldsymbol{\varepsilon}^e + \boldsymbol{\varepsilon}^p $$
-   **[有限应变塑性](@entry_id:185352)**：当变形和转动很大时，简单的加法分解不再成立，因为它不满足[客观性原理](@entry_id:185412)。正确的做法是采用**[乘法分解](@entry_id:199514)** (multiplicative decomposition) 的运动学框架，将变形梯度 $\mathbf{F}$ 分解为弹性部分 $\mathbf{F}^e$ 和塑性部分 $\mathbf{F}^p$ ：
    $$ \mathbf{F} = \mathbf{F}^e \mathbf{F}^p $$
    这个框架引入了一个概念上的、无应力的**[中间构型](@entry_id:193000)**。$\mathbf{F}^p$ 代表从参考构型到[中间构型](@entry_id:193000)的塑性变形，而 $\mathbf{F}^e$ 代表从[中间构型](@entry_id:193000)到当前构型的弹性变形。在小应变极限下，[乘法分解](@entry_id:199514)可以近似还原为加法分解，保证了理论的[自洽性](@entry_id:160889) 。

#### [有限应变塑性](@entry_id:185352)框架

在[乘法分解](@entry_id:199514)框架下，弹性能量 $\psi$ 的构建必须遵循严格的原则，以确保理论的物理意义和数学严谨性 。
1.  **能量仅依赖于弹性变形**: 储存的弹性能应该只与弹性变形 $\mathbf{F}^e$ 有关。
2.  **客观性**: 如前所述，能量函数必须满足客观性。这要求 $\psi$ 必须是 $\mathbf{F}^e$ 的客观函数。
3.  **[中间构型](@entry_id:193000)无关性**: [中间构型](@entry_id:193000)不是唯一的，它可以任意旋转而不改变物理状态。这意味着弹性能量不能依赖于[中间构型](@entry_id:193000)的取向。

同时满足这些要求的结论是，弹性能量 $\psi$ 必须是**弹性[右柯西-格林张量](@entry_id:174156)** $\mathbf{C}^e = \mathbf{F}^{e\top}\mathbf{F}^e$ 的[各向同性函数](@entry_id:750877)。换言之，$\psi$ 只能通过 $\mathbf{C}^e$ 的不变量来表达，例如 $\psi = \hat{\psi}(I_1(\mathbf{C}^e), I_2(\mathbf{C}^e), I_3(\mathbf{C}^e))$ 。这一框架也得到了[热力学一致性](@entry_id:138886)的支持，通过将[耗散不等式](@entry_id:188634)分解为弹性能量变化和[塑性耗散](@entry_id:201273)，可以为[塑性流动](@entry_id:201346)的[演化方程](@entry_id:268137)提供坚实的基础 。如果[塑性流动](@entry_id:201346)是保体积的（这在许多情况下是合理的假设），则有 $\det(\mathbf{F}^p) = 1$，这意味着所有的体积变化都归因于弹性变形，即 $J = \det(\mathbf{F}) = \det(\mathbf{F}^e)$ 。

#### [屈服准则](@entry_id:193897)

[屈服准则](@entry_id:193897)定义了[塑性流动](@entry_id:201346)的起始条件。一个被广泛应用的准则是 **von Mises [屈服准则](@entry_id:193897)**，它适用于许多金属材料，并可作为模拟某些[生物材料](@entry_id:161584)（如蛋白质凝胶）塑性行为的起点。

该准则假设材料的屈服只依赖于**[偏应力张量](@entry_id:267642)** (deviatoric stress tensor) $\mathbf{s} = \boldsymbol{\sigma} - \frac{1}{3}\mathrm{tr}(\boldsymbol{\sigma})\mathbf{I}$，而与静水压力无关。这对于近似不可压缩的材料是合理的。[屈服函数](@entry_id:167970) $f$ 通常基于[偏应力](@entry_id:163323)的第二不变量 $J_2 = \frac{1}{2}\mathbf{s}:\mathbf{s}$ 来定义：
$$ f(\boldsymbol{\sigma}) = \sqrt{3J_2} - \sigma_y = 0 $$
其中 $\sigma_y$ 是材料在[单轴拉伸](@entry_id:188287)下的[屈服应力](@entry_id:274513)，是一个材料参数。当 $\sqrt{3J_2}  \sigma_y$ 时，材料处于弹性状态；当 $\sqrt{3J_2} = \sigma_y$ 时，材料发生屈服。

例如，在简单剪切实验中，如果测得的应力状态不仅包含剪切应力 $\tau$，还包含第一[法向应力差](@entry_id:199507) $N_1 = \sigma_{xx} - \sigma_{yy}$（这是软材料中的常见现象），则在计算 $J_2$ 时必须考虑所有[偏应力](@entry_id:163323)分量。对于一个特定的应力状态，计算出的 $J_2 = \tau^2 + \sigma_n^2$（其中 $N_1 = 2\sigma_n$），von Mises [等效应力](@entry_id:749064)为 $\sigma_{eq} = \sqrt{3(\tau^2+\sigma_n^2)}$。当 $\sigma_{eq}$ 达到 $\sigma_y$ 时，[材料屈服](@entry_id:751736)。虽然这个简单的准则无法捕捉触[变性](@entry_id:165583)、老化或强烈的应变率依赖性等复杂现象，但它为理解和模拟[生物材料](@entry_id:161584)的压力不敏感[塑性流动](@entry_id:201346)提供了一个基本框架 。