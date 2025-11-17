## 引言
当材料经历塑性变形时，其抵抗后续变形的能力会发生改变——这一现象被称为“硬化”。简单地假设[材料屈服](@entry_id:751736)后强度保持不变（[理想塑性](@entry_id:753335)）远不能满足现代工程分析的精度要求。实际材料在[循环加载](@entry_id:181502)下会表现出复杂的行为，如鲍辛格效应（反向加载时[屈服强度](@entry_id:162154)降低）和棘轮效应（塑性应变的逐周期累积），这些现象对结构的完整性和寿命有决定性影响。本文旨在系统性地解决如何用数学模型精确描述这些复杂的[硬化](@entry_id:177483)行为这一核心问题。

为实现这一目标，本文将分为三个核心部分。首先，在“原理与机制”一章中，我们将深入探讨两种基本的硬化理论：**[各向同性硬化](@entry_id:164486)**（屈服面的均匀膨胀）和**[随动硬化](@entry_id:172077)**（屈服面的平移），并介绍将二者结合的先进**Chaboche[组合硬化模型](@entry_id:199179)**。接着，在“应用与跨学科联系”一章中，我们将展示这些模型如何在[结构力学](@entry_id:276699)、[疲劳分析](@entry_id:191624)、材料加工等领域发挥关键作用，并揭示其与[晶体塑性](@entry_id:141273)学、[热力学](@entry_id:141121)等学科的深刻联系。最后，通过“动手实践”部分，读者将有机会通过具体的计算练习，将理论知识转化为解决实际问题的能力。

## 原理与机制

在前一章中，我们介绍了塑性力学的基本概念，并将材料响应划分为弹性阶段和塑性阶段。我们假定在达到初始[屈服应力](@entry_id:274513)后，材料要么以恒定的应力流动（[理想塑性](@entry_id:753335)），要么其屈服强度会发生变化。这种屈服强度的演化被称为**[硬化](@entry_id:177483)**。本章深入探讨描述材料在塑性变形过程中如何“变硬”或“变软”的本构模型。具体而言，我们将系统地阐述**[各向同性硬化](@entry_id:164486) (isotropic hardening)** 和**[随动硬化](@entry_id:172077) (kinematic hardening)** 的原理与机制，它们是现代[计算塑性力学](@entry_id:171377)中不可或缺的基石。我们将从它们的物理现象和几何解释出发，建立数学框架，并最终将它们组合成能够预测复杂循环加载行为的先进模型。

### [各向同性硬化](@entry_id:164486)：屈服面的均匀膨胀

最直观的硬化现象是材料在塑性变形后，其抵抗进一步变形的能力在所有方向上都得到增强。例如，对一根金属棒进行拉伸，使其进入塑性区域，我们会观察到不仅其后续的拉伸屈服应力提高了，其压缩、扭转等其他加载方向上的屈服应力也相应提高。这种现象被称为**[各向同性硬化](@entry_id:164486)**。

#### 几何与数学表述

在应力空间中，[各向同性硬化](@entry_id:164486)被理想化为[屈服面](@entry_id:175331)的均匀膨胀。对于遵循 von Mises [屈服准则](@entry_id:193897)的材料，其初始屈服面在偏[应力空间](@entry_id:199156)中是一个以原点为中心的超球面。在[各向同性硬化](@entry_id:164486)过程中，该球面的中心保持在原点不动，而其半径随塑性变形的累积而增大 [@problem_id:2895956]。

数学上，这通过一个演化的标量屈服强度 $\sigma_y$ 来描述。[屈服函数](@entry_id:167970)写为：
$$
f(\boldsymbol{\sigma}, \kappa) = \sigma_{eq} - \sigma_y(\kappa) = \sqrt{\frac{3}{2}\mathbf{s}:\mathbf{s}} - \sigma_y(\kappa) \le 0
$$
其中，$\boldsymbol{\sigma}$ 是柯西应力张量，$\mathbf{s}$ 是其[偏应力](@entry_id:163323)部分。$\sigma_{eq}$ 是 von Mises [等效应力](@entry_id:749064)。关键在于，当前的屈服应力 $\sigma_y$ 是一个标量内部变量 $\kappa$ 的函数。这个内部变量 $\kappa$ 通常被定义为**累积等效塑性应变**，用于度量材料所经历的塑性变形总量，其率形式为 $\dot{\kappa} = \sqrt{\frac{2}{3}\dot{\boldsymbol{\varepsilon}}^p:\dot{\boldsymbol{\varepsilon}}^p}$，其中 $\dot{\boldsymbol{\varepsilon}}^p$ 是塑性应变率张量 [@problem_id:2570568]。

#### 硬化法则

$\sigma_y$ 如何随 $\kappa$ 演化，即**硬化法则**，决定了模型的具体形式。以下是两种常见的模型 [@problem_id:2895938]：

1.  **线性[各向同性硬化](@entry_id:164486)**：这是最简单的模型，假设屈服应力随累积塑性应变线性增加：
    $$
    \sigma_y(\kappa) = \sigma_{y0} + H\kappa
    $$
    其中 $\sigma_{y0}$ 是初始[屈服应力](@entry_id:274513)，$H$ 是一个正常数，被称为**线性[硬化](@entry_id:177483)模量**或塑性模量。该模型的切向硬化模量 $d\sigma_y/d\kappa = H$ 是一个常数。虽然简单，但它预测屈服应力可以无限增长，这对于大多数金属在经历大变形时并不符合物理实际。

2.  **[非线性](@entry_id:637147) (Voce) [各向同性硬化](@entry_id:164486)**：为了更真实地描述许多金属中观察到的硬化饱和现象，Voce [硬化](@entry_id:177483)法则被引入：
    $$
    \sigma_y(\kappa) = \sigma_s - (\sigma_s - \sigma_{y0})\exp(-b\kappa)
    $$
    这里引入了两个新参数：$\sigma_s$ 是**饱和应力**，表示当塑性变形非常大 (即 $\kappa \to \infty$) 时[屈服应力](@entry_id:274513)所能达到的极限值；$b$ 是一个正常数，控制着[屈服应力](@entry_id:274513)趋近饱和应力的速率。该模型的切向[硬化](@entry_id:177483)模量 $d\sigma_y/d\kappa = b(\sigma_s - \sigma_{y0})\exp(-b\kappa)$，它从初始值 $b(\sigma_s - \sigma_{y0})$ 开始，随着 $\kappa$ 的增加而逐渐衰减至零。这种[非线性模型](@entry_id:276864)能够更准确地捕捉材料从初始屈服到[硬化](@entry_id:177483)饱和的整个过程。

#### 局限性：鲍辛格效应

尽管[各向同性硬化](@entry_id:164486)模型直观且易于实现，但它有一个显著的局限性：无法描述**鲍辛格效应 (Bauschinger effect)**。鲍辛格效应是指材料在某个方向上发生塑性变形后，其在反向加载时的[屈服应力](@entry_id:274513)会显著降低的现象。例如，将金属棒拉伸至塑性状态后卸载，再对其进行压缩，会发现其开始塑性流动的压缩应力大小，远低于其在拉伸方向上达到的应力水平。

在[各向同性硬化](@entry_id:164486)模型中，[屈服面](@entry_id:175331)只是均匀膨胀。因此，拉伸后的材料在压缩方向上的屈服强度与拉伸方向上的屈服强度大小相等。这与实验观察到的鲍辛格效应相悖 [@problem_id:2895956]。为了捕捉这一关键的物理现象，我们需要引入另一种硬化机制。

### [随动硬化](@entry_id:172077)：屈服面的平移

**[随动硬化](@entry_id:172077)**，又称[运动硬化](@entry_id:172077)，是为解释鲍辛格效应而提出的。其核心思想是，在塑性变形过程中，屈服面在应力空间中并不膨胀，而是作为一个刚体发生平移。

#### 几何与数学表述

在偏应力空间中，[随动硬化](@entry_id:172077)模型假设 von Mises [屈服面](@entry_id:175331)的尺寸（半径）保持不变，但其中心位置会移动。这个中心的偏移量由一个[二阶张量](@entry_id:199780)——**[背应力](@entry_id:198105) (backstress)** 张量 $\boldsymbol{\alpha}$ 来描述。由于 von Mises 塑性对[静水压力](@entry_id:275365)不敏感，[背应力](@entry_id:198105) $\boldsymbol{\alpha}$ 也被假定为偏量张量 (即 $\mathrm{tr}(\boldsymbol{\alpha}) = 0$) [@problem_id:2895956]。

引入背应力后，[屈服函数](@entry_id:167970)变为：
$$
f(\boldsymbol{\sigma}, \boldsymbol{\alpha}) = \sigma_{eq}(\mathbf{s} - \boldsymbol{\alpha}) - \sigma_{y0} = \sqrt{\frac{3}{2}(\mathbf{s} - \boldsymbol{\alpha}):(\mathbf{s} - \boldsymbol{\alpha})} - \sigma_{y0} \le 0
$$
这里的 $\mathbf{s} - \boldsymbol{\alpha}$ 被称为**有效[偏应力](@entry_id:163323)**。屈服现在取决于有效[偏应力](@entry_id:163323)的大小，而不是[偏应力](@entry_id:163323)本身。[屈服面](@entry_id:175331)在偏应力空间中是一个半径固定（由初始[屈服应力](@entry_id:274513) $\sigma_{y0}$ 决定）、中心位于 $\boldsymbol{\alpha}$ 的超球面 [@problem_id:2621864]。

当材料沿某一方向加载时，例如拉伸，背应力 $\boldsymbol{\alpha}$ 会朝着加载方向发展。这导致整个屈服面向拉伸方向平移。结果，[屈服面](@entry_id:175331)的“背面”（压缩侧）会更接近应力原点。因此，当卸载并反向加载至压缩状态时，应力路径会更快地接触到移动后的[屈服面](@entry_id:175331)边界，从而在较小的[应力幅](@entry_id:191678)值下发生屈服。这便是对鲍辛格效应的几何解释 [@problem_id:2895942]。

#### [硬化](@entry_id:177483)法则：背应力的演化

[随动硬化](@entry_id:172077)的关键在于如何定义[背应力](@entry_id:198105) $\boldsymbol{\alpha}$ 的演化法则。

1.  **Prager 线性[随动硬化](@entry_id:172077)**：最简单的模型由 Prager 提出，假设[背应力](@entry_id:198105)的增长率与塑性[应变率](@entry_id:154778)成正比 [@problem_id:2895971]：
    $$
    \dot{\boldsymbol{\alpha}} = C \dot{\boldsymbol{\varepsilon}}^p
    $$
    其中 $C$ 是一个常数，称为[随动硬化](@entry_id:172077)模量。在关联[流动法则](@entry_id:177163)下，塑性应变率 $\dot{\boldsymbol{\varepsilon}}^p$ 的方向垂直于[屈服面](@entry_id:175331)。因此，该法则意味着[背应力](@entry_id:198105)的演化方向（即屈服面中心的移动方向）总是沿着当前应力点处屈服面的外[法线](@entry_id:167651)方向。对于[单轴拉伸](@entry_id:188287)，该模型预测应力-塑性应变曲线为线性，因此被称为线性[随动硬化](@entry_id:172077)。

2.  **Armstrong-Frederick (AF) [非线性](@entry_id:637147)[随动硬化](@entry_id:172077)**：[线性模型](@entry_id:178302)预测背应力会无限增长，这同样不符合物理实际。为了引入饱和效应，Armstrong 和 Frederick 增加了一个“动态恢复项”：
    $$
    \dot{\boldsymbol{\alpha}} = C \dot{\boldsymbol{\varepsilon}}^p - \gamma \boldsymbol{\alpha} |\dot{\boldsymbol{\varepsilon}}^p|
    $$
    其中 $\gamma$ 是一个控制恢复速率的材料参数，而 $|\dot{\boldsymbol{\varepsilon}}^p| = \sqrt{\dot{\boldsymbol{\varepsilon}}^p:\dot{\boldsymbol{\varepsilon}}^p}$ 是塑性[应变率](@entry_id:154778)的大小。第一项 $C \dot{\boldsymbol{\varepsilon}}^p$ 是一个产生项，使[背应力](@entry_id:198105)向加载方向发展。第二项 $-\gamma \boldsymbol{\alpha} |\dot{\boldsymbol{\varepsilon}}^p|$ 是一个恢复项或遗忘项，其作用是使[背应力](@entry_id:198105)的增长随着自身大小的增加而减慢。当达到平衡时，$\dot{\boldsymbol{\alpha}} = \mathbf{0}$，背应力将饱和于一个与加载方向和 $C/\gamma$ 有关的极限值。

### [组合硬化模型](@entry_id:199179)与 Chaboche 模型

在现实中，材料的[硬化](@entry_id:177483)行为通常既包含各向同性部分（例如，[循环加载](@entry_id:181502)过程中幅值的变化，即**循环硬化**或**循环软化**），也包含随动部分（鲍辛格效应）。因此，需要将两种硬化机制结合起来，形成**[组合硬化](@entry_id:186067) (combined hardening)** 模型。

#### 通用[屈服函数](@entry_id:167970)

[组合硬化模型](@entry_id:199179)的一般[屈服函数](@entry_id:167970)形式为 [@problem_id:2570556] [@problem_id:2621864]：
$$
f(\boldsymbol{\sigma}, \boldsymbol{\alpha}, \kappa) = \sqrt{\frac{3}{2}(\mathbf{s} - \boldsymbol{\alpha}):(\mathbf{s} - \boldsymbol{\alpha})} - (\sigma_{y0} + R(\kappa)) \le 0
$$
在这个形式中，[屈服面](@entry_id:175331)既可以平移（通过演化的 $\boldsymbol{\alpha}$），也可以膨胀或收缩（通过演化的半径 $\sigma_y(\kappa) = \sigma_{y0} + R(\kappa)$）。$R(\kappa)$ 是[各向同性硬化](@entry_id:164486)变量，可以是线性或[非线性](@entry_id:637147)的，如前所述。

#### Chaboche 模型

为了更精确地模拟复杂的材料行为，特别是循环加载下的响应（如棘轮效应、[应力松弛](@entry_id:159905)等），Chaboche 提出了一个强大的[非线性](@entry_id:637147)[随动硬化](@entry_id:172077)模型。其核心思想是将总[背应力](@entry_id:198105) $\boldsymbol{\alpha}$ 分解为多个（例如 $m$ 个）Armstrong-Frederick 型分量的叠加：
$$
\boldsymbol{\alpha} = \sum_{i=1}^{m} \boldsymbol{\alpha}_i
$$
每一个背应力分量 $\boldsymbol{\alpha}_i$ 都遵循自己的 AF 型演化法则 [@problem_id:2570611]：
$$
\dot{\boldsymbol{\alpha}}_i = C_i \dot{\boldsymbol{\varepsilon}}^p - \gamma_i \boldsymbol{\alpha}_i |\dot{\boldsymbol{\varepsilon}}^p|
$$
其中，$C_i$ 和 $\gamma_i$ 是第 $i$ 个分量对应的材料参数。

使用多个背应力分量的根本原因在于，它们能够以不同的速率饱和。一个分量可以有较大的 $C_i$ 和 $\gamma_i$ 值，用于描述应力-应变曲线初始阶段的急剧变化（曲线的“膝部”）。另一个分量可以有较小的 $C_j$ 和 $\gamma_j$ 值，用于描述在[大应变](@entry_id:751152)下缓慢接近饱和的长期行为。通过组合多个具有不同[特征时间尺度](@entry_id:276738)（由 $1/\gamma_i$ 决定）的演化过程，Chaboche 模型可以像 Prony 级数一样，以高精度拟合整个应力-应变[滞回环](@entry_id:160173)的形状 [@problem_id:2570611]。这种灵活性对于准确预测诸如**棘轮效应 (ratcheting)**（在非对称循环应力下塑性应变的持续累积）等[路径依赖性](@entry_id:186326)极强的现象至关重要 [@problem_id:2570611] [@problem_id:2570556]。

### [热力学](@entry_id:141121)与计算框架

所有塑性[本构模型](@entry_id:174726)都必须满足[热力学第二定律](@entry_id:142732)，以确保其物理上的合理性。此外，在有限元 (FEM) 等数值方法中实现这些模型时，也需要考虑特定的算法和框架。

#### [热力学一致性](@entry_id:138886)

对于[等温过程](@entry_id:143096)，[热力学第二定律](@entry_id:142732)（以 Clausius-Duhem 不等式形式表达）要求材料的内耗散率必须非负。对于包含各向同性和[随动硬化](@entry_id:172077)的[弹塑性](@entry_id:193198)材料，可以推导出[耗散不等式](@entry_id:188634) [@problem_id:2570590]：
$$
D = \boldsymbol{\sigma} : \dot{\boldsymbol{\varepsilon}}^p + \mathbf{X} : \dot{\boldsymbol{\alpha}} + R_H \dot{\kappa} \ge 0
$$
这里，我们定义了与内部变量 $\boldsymbol{\alpha}$ 和 $\kappa$ 共轭的[热力学力](@entry_id:161907)，即[背应力](@entry_id:198105) $\mathbf{X}$ 和[各向同性硬化](@entry_id:164486)应力 $R_H$。它们通常通过亥姆霍兹自由能 $\psi$ 对内部变量的导数来定义，例如 $\mathbf{X} = -\partial\psi/\partial\boldsymbol{\alpha}$。这个不等式表明，总耗散由三部分组成：[塑性流动](@entry_id:201346)产生的耗散 ($\boldsymbol{\sigma} : \dot{\boldsymbol{\varepsilon}}^p$)、与[背应力](@entry_id:198105)演化相关的耗散 ($\mathbf{X} : \dot{\boldsymbol{\alpha}}$)，以及与[各向同性硬化](@entry_id:164486)演化相关的耗散 ($R_H \dot{\kappa}$)。本构理论的构建必须确保这一不等式恒成立。

#### 计算实现考量

在有限元分析中，这些率形式的[本构方程](@entry_id:138559)需要在离散的时间步内进行积分。这通常通过**[返回映射算法](@entry_id:168456) (return-mapping algorithm)** 来实现。对于[组合硬化模型](@entry_id:199179)，算法的核心是在一个“试探”弹性步之后，将超出[屈服面](@entry_id:175331)的应力状态“投影”回演化后的屈服面上。这个投影是在以 $\boldsymbol{\alpha}$ 为中心的[有效应力](@entry_id:198048)空间中沿径向进行的 [@problem_id:2570556]。

此外，当处理[大变形](@entry_id:167243)问题时，必须考虑物体[刚体转动](@entry_id:191086)对[本构关系](@entry_id:186508)的影响。张量的时间导数（如 $\dot{\boldsymbol{\sigma}}$ 和 $\dot{\boldsymbol{\alpha}}$）在默认情况下不是**客观的 (objective)**，即它们的值会随观察者[坐标系](@entry_id:156346)的旋转而改变。为了保证**物质框架无关性 (material frame indifference)**，必须使用[客观应力率](@entry_id:199282)，例如 **[Jaumann 率](@entry_id:185572)** 或 Green-Naghdi 率。在更新拉格朗日列式的有限元程序中，这意味着本构更新需要在与材料一同旋转的**协同转动[坐标系](@entry_id:156346) (corotational frame)** 中进行，以消除[刚体转动](@entry_id:191086)带来的伪应力/背应力增量 [@problem_id:2570585]。这对于保证大转动下数值解的准确性和稳定性至关重要。

综上所述，从简单的[各向同性硬化](@entry_id:164486)到复杂的 Chaboche [组合硬化模型](@entry_id:199179)，塑性力学提供了一套不断丰富的工具，用于描述材料在塑性变形过程中的复杂演化行为。这些模型不仅具有清晰的物理和几何解释，也建立在严格的[热力学](@entry_id:141121)和计算框架之上，使其成为现代工程模拟中不可或缺的一部分。