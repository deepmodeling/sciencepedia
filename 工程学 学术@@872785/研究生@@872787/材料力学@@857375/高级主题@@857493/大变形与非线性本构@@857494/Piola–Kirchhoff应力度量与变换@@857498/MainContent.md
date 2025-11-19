## 引言
在处理材料的[大变形](@entry_id:167243)问题时，例如橡胶的拉伸或金属的塑性成型，仅依赖于经典[线性弹性](@entry_id:166983)理论中的柯西（Cauchy）应力是远远不够的。柯西应力，即“真实应力”，定义在不断变化的当前物体构型上，这给在固定参考[坐标系](@entry_id:156346)下进行的理论分析和数值计算（如[有限元法](@entry_id:749389)）带来了巨大挑战。为了解决这一根本性难题，连续介质力学引入了一套更为强大的工具——皮奥拉-基尔霍夫（Piola-Kirchhoff）应力度量，它们能够在固定的、未变形的参考构型上一致地描述应力状态。

本文旨在系统地阐明这些关键的应力度量。我们将从“原理与机制”出发，深入探讨第一和[第二皮奥拉-基尔霍夫应力](@entry_id:173163)张量的定义、物理意义及其与柯西应力之间的数学变换关系。随后，在“应用与跨学科联系”一章中，我们将展示这些理论概念如何应用于实际工程与科学问题，例如表征[超弹性材料](@entry_id:190241)的本构行为、处理各向异性[复合材料](@entry_id:139856)，以及它们在[计算力学](@entry_id:174464)中的核心作用。最后，通过“动手实践”部分，您将有机会运用所学知识解决具体问题，从而加深理解。让我们首先进入第一章，揭示这些应力度量背后的基本原理。

## 原理与机制

在[连续介质力学](@entry_id:155125)中，当物体经历大变形时，描述其内部应力状态需要超越在线弹性理论中常见的柯西（Cauchy）应力张量。这是因为在[大变形](@entry_id:167243)背景下，物体的几何构型——包括其体积、面积和方向——都在不断变化。为了在固定不变的参考构型上建立运动方程和[本构关系](@entry_id:186508)，必须引入新的应力度量。本章将系统地阐述这些应力度量，即第一和第二皮奥拉-基尔霍夫（Piola-Kirchhoff）[应力张量](@entry_id:148973)，并阐明它们之间的转换关系、物理意义，以及在能量原理和本构理论中的核心作用。

### 应力度量的必要性：参考构型与当前构型

我们从一个基本问题开始：为什么柯西应力不足以处理大变形问题？柯西[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$，也被称为**真实应力**，其定义为作用在**当前（或变形后）构型**中一个微元面上的单位面积力。这一定义在物理上非常直观，因为它描述了材料在当前瞬间实际承受的应力。然而，在分析中，尤其是[数值模拟](@entry_id:137087)（如[有限元法](@entry_id:749389)）中，我们通常在一个固定的、未变形的**参考构型**上进行计算。随着物体的变形，柯西应力作用的微元面积本身的大小和方向都在改变，这使得在固定参考域上的积分和[微分](@entry_id:158718)运算变得异常复杂。

为了克服这一困难，我们需要定义一种新的应力，它能够将当前构型中的力与参考构型中固定的、未变形的面积联系起来。这正是[皮奥拉-基尔霍夫应力](@entry_id:173629)张量的基本思想。

### [第一皮奥拉-基尔霍夫应力](@entry_id:163971)：连接两个构型的桥梁

第一皮奥拉-基尔霍夫（First Piola-Kirchhoff, PK1）[应力张量](@entry_id:148973)，记为 $\mathbf{P}$，通常也被称为**名义应力（nominal stress）**。它的物理意义是：作用在当前构型中物体上的力，除以其在**参考构型**中对应的未变形面积。

为了精确定义 $\mathbf{P}$，我们考虑力在两个构型中的平衡。设一个微元面在参考构型中的面积为 $dA$，其[单位法向量](@entry_id:178851)为 $\mathbf{N}$。经过变形后，该微元面在当前构型中的面积变为 $da$，[单位法向量](@entry_id:178851)为 $\mathbf{n}$。作用在该微元面上的真实力微元 $d\mathbf{f}$ 是一个客观存在的物理量，不因我们选择的描述方式而改变。根据柯西应力 $\boldsymbol{\sigma}$ 和 PK1应力 $\mathbf{P}$ 的定义，我们有：

$d\mathbf{f} = \boldsymbol{\sigma} \mathbf{n} \, da$ (在当前构型中)

$d\mathbf{f} = \mathbf{P} \mathbf{N} \, dA$ (在参考构型中)

其中，$\mathbf{P} \mathbf{N}$ 被称为**名义面力**或参考面力 $\mathbf{T}_0$ [@problem_id:2908141]。要建立 $\mathbf{P}$ 与 $\boldsymbol{\sigma}$ 之间的关系，我们需要连接两个构型中面积微元 $(\mathbf{n}, da)$ 和 $(\mathbf{N}, dA)$ 的几何关系。这一关系由著名的**[南森公式](@entry_id:195566)（Nanson's formula）**给出 [@problem_id:2908101]：

$\mathbf{n} \, da = J \mathbf{F}^{-T} \mathbf{N} \, dA$

这里，$\mathbf{F} = \nabla_0 \boldsymbol{\varphi}$ 是**变形梯度**，它将参考构型中的[线元](@entry_id:196833) $d\mathbf{X}$ 映射到当前构型中的线元 $d\mathbf{x}$，即 $d\mathbf{x} = \mathbf{F} d\mathbf{X}$。$J = \det(\mathbf{F})$ 是 $\mathbf{F}$ 的雅可比行列式，代表了局部体积变化的比例，即 $dv = J dV$。$\mathbf{F}^{-T}$ 表示 $\mathbf{F}$ 的逆的[转置](@entry_id:142115)。物理上合理的变形要求 $J > 0$。

现在，我们将[南森公式](@entry_id:195566)代入力平衡方程：

$\mathbf{P} \mathbf{N} \, dA = \boldsymbol{\sigma} (J \mathbf{F}^{-T} \mathbf{N} \, dA)$

由于这个关系对任意选择的参考[法向量](@entry_id:264185) $\mathbf{N}$ 都成立，我们必然得到 $\mathbf{P}$ 和 $\boldsymbol{\sigma}$ 之间的转换关系：

$\mathbf{P} = J \boldsymbol{\sigma} \mathbf{F}^{-T}$

这个公式是有限变形力学的基石之一 [@problem_id:2657141] [@problem_id:2908101] [@problem_id:2908071]。它清晰地表明，PK1应力 $\mathbf{P}$ 是如何通过变形的几何信息（$J$ 和 $\mathbf{F}$）与真实应力 $\boldsymbol{\sigma}$ 联系起来的。

$\mathbf{P}$ 张量的一个显著特点是，它是一个**两点张量（two-point tensor）**。它的定义将一个属于参考构型的向量（[法向量](@entry_id:264185) $\mathbf{N}$）映射到一个属于当前构型的向量（力 $\mathbf{T}_0 dA$）。这种混合特性使得 $\mathbf{P}$ 在数学上和物理上都具有独特的性质。

一个直观的例子是[单轴拉伸试验](@entry_id:195375)。假设一个杆件沿 $X_1$ 方向拉伸，拉伸比为 $\lambda$。在不可压缩的情况下，横向收缩使得当前[截面](@entry_id:154995)积 $A = A_0 / \lambda$。试验机测得的力为 $F_m$。工程应力定义为 $\sigma_{\text{eng}} = F_m / A_0$，而真实应力为 $\sigma_{11} = F_m / A = \lambda (F_m / A_0) = \lambda \sigma_{\text{eng}}$。通过计算可以证明，PK1应力的分量 $P_{11}$ 正好等于工程应力 $\sigma_{\text{eng}}$ [@problem_id:2908071]。

### [第二皮奥拉-基尔霍夫应力](@entry_id:173163)：纯粹的参考构型度量

尽管 PK1应力 $\mathbf{P}$ 解决了在参考构型上描述应力的问题，但它仍然存在两个不便之处。首先，它将参考构型的量与当前构型的量联系起来，使其成为一个两点张量。其次，也是更重要的一点，即使柯西应力 $\boldsymbol{\sigma}$ 是对称的（由动量矩平衡保证），$\mathbf{P}$ 通常也**不是对称的**。这给[本构模型](@entry_id:174726)的建立带来了困难，因为本构关系通常基于对称的应变和应力度量。

为了解决这些问题，我们引入**第二皮奥拉-基尔霍夫（Second Piola-Kirchhoff, PK2）[应力张量](@entry_id:148973)**，记为 $\mathbf{S}$。$\mathbf{S}$ 的引入纯粹是出于数学和物理建模的便利，它通过将 PK1应力 $\mathbf{P}$ 中的力向量也“[拉回](@entry_id:160816)”到参考构型来定义。定义关系为：

$\mathbf{P} = \mathbf{F} \mathbf{S}$  或  $\mathbf{S} = \mathbf{F}^{-1} \mathbf{P}$

这个定义将两点张量 $\mathbf{P}$ 分解为一个纯粹描述变形的张量 $\mathbf{F}$ 和一个新的、纯粹定义在参考构型上的张量 $\mathbf{S}$。现在，$\mathbf{S}$ 将参考构型的法向量 $\mathbf{N}$ 映射到一个“伪力向量” $\mathbf{F}^{-1}\mathbf{T}_0$，该向量也位于参考构型中。

结合 $\mathbf{P}$ 和 $\boldsymbol{\sigma}$ 的关系，我们可以推导出 $\mathbf{S}$ 和 $\boldsymbol{\sigma}$ 之间的关系：

$\mathbf{S} = \mathbf{F}^{-1} (J \boldsymbol{\sigma} \mathbf{F}^{-T}) = J \mathbf{F}^{-1} \boldsymbol{\sigma} \mathbf{F}^{-T}$

反过来，将真实应力 $\boldsymbol{\sigma}$ 用 $\mathbf{S}$ 表示的 push-forward 操作为：

$\boldsymbol{\sigma} = \frac{1}{J} \mathbf{F} \mathbf{S} \mathbf{F}^{T}$

PK2应力 $\mathbf{S}$ 具有两个至关重要的性质 [@problem_id:2908168]：
1.  **对称性**：如果柯西应力 $\boldsymbol{\sigma}$ 是对称的，那么 $\mathbf{S}$ 也必然是对称的。这可以通过其与 $\boldsymbol{\sigma}$ 的转换关系[直接证明](@entry_id:141172)：$\mathbf{S}^T = (J \mathbf{F}^{-1} \boldsymbol{\sigma} \mathbf{F}^{-T})^T = J (\mathbf{F}^{-T})^T \boldsymbol{\sigma}^T (\mathbf{F}^{-1})^T = J \mathbf{F}^{-1} \boldsymbol{\sigma} \mathbf{F}^{-T} = \mathbf{S}$。
2.  **客观性（Objectivity）**：在变形之上叠加一个[刚体转动](@entry_id:191086)时，$\mathbf{S}$ 的值保持不变。这使得 $\mathbf{S}$ 成为建立不依赖于观察者[刚体运动](@entry_id:193355)的[本构关系](@entry_id:186508)的理想选择。

### 应力与平衡定律

物质的运动必须遵守动量和动量矩守恒。这些物理定律在不同的构型中有不同的数学表达形式。

#### [线性动量平衡](@entry_id:193575)

在[线性动量平衡](@entry_id:193575)（即牛顿第二定律）的局部形式中，空间（当前）构型的方程为：

$\operatorname{div}_{\mathbf{x}} \boldsymbol{\sigma} + \rho \mathbf{b} = \rho \mathbf{a}$

其中 $\operatorname{div}_{\mathbf{x}}$ 是对当前坐标 $\mathbf{x}$ 的[散度算子](@entry_id:265975)，$\rho$ 是当前密度，$\mathbf{b}$ 是单位质量的体力，$\mathbf{a}$ 是加速度。要将其转换为参考构型，我们需要将对 $\boldsymbol{\sigma}$ 的散度转换为对 $\mathbf{P}$ 的散度。这可以通过**皮奥拉恒等式（Piola's identity）**实现 [@problem_id:2908139]：

$\operatorname{Div}_{\mathbf{X}} \mathbf{P} = J (\operatorname{div}_{\mathbf{x}} \boldsymbol{\sigma}) \circ \boldsymbol{\varphi}$

其中 $\operatorname{Div}_{\mathbf{X}}$ 是对参考坐标 $\mathbf{X}$ 的[散度算子](@entry_id:265975)。利用此恒等式以及质量守恒关系 $\rho_0 = J \rho$，我们可以得到[动量平衡](@entry_id:193575)的物质（参考）形式：

$\operatorname{Div}_{\mathbf{X}} \mathbf{P} + \rho_0 \mathbf{b}_0 = \rho_0 \mathbf{a}$

其中 $\rho_0$ 是参考密度，$\mathbf{b}_0$ 和 $\mathbf{a}$ 是在参考构型上描述的[体力](@entry_id:174230)与加速度。这个方程只包含在固定参考域上定义的场，因此特别适用于全拉格朗日（Total Lagrangian）有限元方法。

#### [角动量平衡](@entry_id:181848)与[应力的对称性](@entry_id:181684)

在没有[体力](@entry_id:174230)偶的情况下，[角动量平衡](@entry_id:181848)定律在局部形式下要求柯西[应力张量](@entry_id:148973)必须是对称的，即 $\boldsymbol{\sigma} = \boldsymbol{\sigma}^T$。如前所述，这直接导致了 PK2应力 $\mathbf{S}$ 的对称性。

然而，PK1应力 $\mathbf{P}$ 通常不是对称的。[角动量平衡](@entry_id:181848)在参考构型中的体现是张量 $\mathbf{P}\mathbf{F}^T$ 的对称性 [@problem_id:2908091]：

$\mathbf{P}\mathbf{F}^T = (\mathbf{P}\mathbf{F}^T)^T = \mathbf{F}\mathbf{P}^T$

这个条件通常不意味着 $\mathbf{P} = \mathbf{P}^T$。$\mathbf{P}$ 的非对称性源于其两点张量的本质：它的两个索引分别与不同构型（和不同[坐标系](@entry_id:156346)）的[基向量](@entry_id:199546)相关联，因此“对称”这一概念本身就失去了其在单一场所张量（如 $\boldsymbol{\sigma}$ 或 $\mathbf{S}$）中的明确几何意义 [@problem_id:2908091]。

例如，考虑一个简单的剪切变形，其变形梯度为 $\mathbf{F} = \begin{pmatrix} 1  \gamma  0 \\ 0  1  0 \\ 0  0  1 \end{pmatrix}$，并假设材料处于静水压力状态 $\boldsymbol{\sigma} = p\mathbf{I}$。通过计算可得 $\mathbf{P} = p\mathbf{F}^{-T} = p\begin{pmatrix} 1  0  0 \\ -\gamma  1  0 \\ 0  0  1 \end{pmatrix}$。当 $\gamma \neq 0$ 时，$\mathbf{P}$ 显然是非对称的，尽管它满足所有平衡定律 [@problem_id:2908091] [@problem_id:2908141]。

### 能量共轭与功率表达式

理解不同应力度量的最深刻方式之一是通过**能量共轭（energetic conjugacy）**的概念。材料变形时，[内力](@entry_id:167605)所做的[功率密度](@entry_id:194407)（单位体积的功率）可以用[应力与应变率](@entry_id:263123)的缩并来表示。

1.  在**当前构型**中，[应变率](@entry_id:154778)由变形率张量 $\mathbf{d}$（[空间速度梯度](@entry_id:187198) $\mathbf{l}=\nabla_x \mathbf{v}$ 的对称部分）描述。内[功率密度](@entry_id:194407)为：
    $\dot{w} = \boldsymbol{\sigma} : \mathbf{d}$
    其单位是功率/当前体积 [@problem_id:2908170]。

2.  在**参考构型**中，我们需要考虑单位参考体积的[功率密度](@entry_id:194407) $\dot{w}_0 = J \dot{w}$。通过[运动学](@entry_id:173318)和[张量代数](@entry_id:161671)变换，可以证明这个[功率密度](@entry_id:194407)可以表达为另外两种等价形式：
    $\dot{w}_0 = \mathbf{P} : \dot{\mathbf{F}}$
    $\dot{w}_0 = \mathbf{S} : \dot{\mathbf{E}}$

    这里，$\dot{\mathbf{F}}$ 是变形梯度的[物质时间导数](@entry_id:190892)，$\mathbf{E} = \frac{1}{2}(\mathbf{F}^T\mathbf{F} - \mathbf{I})$ 是格林-拉格朗日（Green-Lagrange）应变张量，$\dot{\mathbf{E}}$ 是其[物质时间导数](@entry_id:190892)。

这些关系揭示了深刻的共轭配对 [@problem_id:2908170] [@problem_id:2908141]：
-   柯西应力 $\boldsymbol{\sigma}$ 与变形率 $\mathbf{d}$ 共轭。
-   第一PK应力 $\mathbf{P}$ 与变形梯度 $\mathbf{F}$ 的率 $\dot{\mathbf{F}}$ 共轭。
-   第二PK应力 $\mathbf{S}$ 与[格林-拉格朗日应变](@entry_id:170427) $\mathbf{E}$ 的率 $\dot{\mathbf{E}}$ 共轭。

这种共轭关系是选择何种应力/应变组合来描述材料本构行为和建立力学方程的基础。

### 在本构模型和数值方法中的应用

理论上的优雅最终要服务于实际应用。[皮奥拉-基尔霍夫应力](@entry_id:173629)在[超弹性](@entry_id:159356)和[弹塑性](@entry_id:193198)[本构模型](@entry_id:174726)以及有限元方法中扮演着不可或缺的角色。

#### 超弹性与第二PK应力 $\mathbf{S}$

[超弹性材料](@entry_id:190241)的本构行为由一个[应变能密度函数](@entry_id:755490) $\Psi$ 定义。根据**[材料客观性原理](@entry_id:177427)**，$\Psi$ 不能依赖于观察者的刚体运动。这意味着 $\Psi$ 只能是[客观应变度量](@entry_id:752864)的函数，例如[右柯西-格林张量](@entry_id:174156) $\mathbf{C} = \mathbf{F}^T\mathbf{F}$ 或[格林-拉格朗日应变](@entry_id:170427) $\mathbf{E}$，因为它们在[刚体转动](@entry_id:191086)下保持不变。因此，我们可以写出 $\Psi = \hat{\Psi}(\mathbf{E})$。

根据能量共轭原理，应力可以由[应变能函数](@entry_id:178435)对共轭[应变度量](@entry_id:755495)的导数得到。由于 $\mathbf{S}$ 与 $\mathbf{E}$ 共轭，我们自然得到：

$\mathbf{S} = \frac{\partial \hat{\Psi}}{\partial \mathbf{E}}$

这个简洁而优雅的关系使得 $\mathbf{S}$ 成为描述[超弹性材料](@entry_id:190241)本构行为的首选应力度量。它既对称又客观，完美地契合了基于能量的本构理论框架 [@problem_id:2908168] [@problem_id:2908151]。

#### 全[拉格朗日有限元](@entry_id:751107)与第一PK应力 $\mathbf{P}$

在全拉格朗日（Total Lagrangian）有限元公式中，所有的计算都在固定的初始参考构型 $\mathcal{B}_0$ 上进行。其核心是[虚功原理](@entry_id:138749)的[弱形式](@entry_id:142897)。[内虚功](@entry_id:172278) $\delta W_{int}$ 是应力与虚应变的积分。将空间构型中的[虚功](@entry_id:176403)表达式 $\int_{\mathcal{B}_t} \boldsymbol{\sigma} : \delta\mathbf{d} \, dv$ [拉回](@entry_id:160816)到参考构型，利用能量共轭关系，我们得到：

$\delta W_{int} = \int_{\mathcal{B}_0} \mathbf{P} : \delta\mathbf{F} \, dV_0$

因此，在全拉格朗日[弱形式](@entry_id:142897)中自然出现的应力度量是第一PK应力 $\mathbf{P}$，因为它与变形梯度的变分 $\delta\mathbf{F}$ 直接共轭。这就是为什么在有限元软件的底层实现中，单元的[内力向量](@entry_id:750751)是通过对 $\mathbf{P}$ 在单元上积分得到的 [@problem_id:2908151]。

#### 率形式[本构模型](@entry_id:174726)与柯西应力 $\boldsymbol{\sigma}$

对于率相关的材料，如[弹塑性](@entry_id:193198)材料，其[本构关系](@entry_id:186508)通常以率形式给出，即应力率与变形率之间的关系。为了保证客观性，必须使用**[客观应力率](@entry_id:199282)**，如 Zaremba-[Jaumann 率](@entry_id:185572)或 Green-Naghdi 率。这些[客观率](@entry_id:198692)通常是为[空间张量](@entry_id:185799)（如 $\boldsymbol{\sigma}$ 或[基尔霍夫应力](@entry_id:751039) $\boldsymbol{\tau} = J\boldsymbol{\sigma}$）定义的，因为它们能自然地利用空间[自旋张量](@entry_id:187346) $\mathbf{W}$ 来消除[刚体转动](@entry_id:191086)的影响。此外，塑性理论中的屈服和流动通常由变形率 $\mathbf{d}$ 驱动，而与 $\mathbf{d}$ 直接能量共轭的应力是 $\boldsymbol{\sigma}$ 或 $\boldsymbol{\tau}$。最后，大多数塑性算法（如[返回映射](@entry_id:754324)）利用了应力[张量的对称性](@entry_id:202126)进行[谱分解](@entry_id:173707)（[主应力](@entry_id:176761)计算），这是 $\boldsymbol{\sigma}$ 和 $\boldsymbol{\tau}$ 的天然优势，而对于非对称的 $\mathbf{P}$ 则非常复杂。综上所述，尽管计算在[拉格朗日框架](@entry_id:751113)下进行，但率形式的本构更新步骤几乎总是在空间构型中，使用柯西或[基尔霍夫应力](@entry_id:751039)来完成 [@problem_id:2908088]。

通过理解这三种应力度量——$\boldsymbol{\sigma}$ 的物理直观性、$\mathbf{P}$ 在连接构型和动量方程中的桥梁作用，以及 $\mathbf{S}$ 在客观本构理论中的核心地位——我们才能全面掌握大变形固体力学的分析框架。