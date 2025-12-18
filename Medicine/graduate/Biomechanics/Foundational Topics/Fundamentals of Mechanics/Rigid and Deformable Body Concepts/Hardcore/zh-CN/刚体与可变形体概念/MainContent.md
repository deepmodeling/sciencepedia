## 引言
在生物力学领域，如何对生物结构（从骨骼到肌肉再到细胞）进行力学建模，是一个根本性的问题。我们面临着一个关键的选择：是将其简化为在运动中保持形状不变的**[刚体](@entry_id:1131033)**，还是将其视为能够响应载荷而变形的**[可变形体](@entry_id:1123496)**？尽管[刚体模型](@entry_id:1131036)在分析宏观运动（如人体步态）时是一种强大而高效的工具，但生物组织的功能、损伤、生长和适应过程本质上都与变形紧密相连。特别是对于肌肉、血管和肌腱等软组织，其力学行为表现出复杂的[非线性](@entry_id:637147)、各向异性和时间依赖性，远非传统[线性模型](@entry_id:178302)所能描述。

本文旨在填补从理想化[刚体](@entry_id:1131033)概念到复杂[可变形体](@entry_id:1123496)理论之间的知识鸿沟，为读者构建一个连贯的理解框架。我们将系统地阐明描述这两种力学行为背后的数学语言和物理原理，并展示如何在具体的生物力学问题中做出恰当的[模型选择](@entry_id:155601)。通过学习本文，您将能够理解和运用从基础运动学到高级[本构关系](@entry_id:186508)的核心概念。

文章的结构安排如下：首先，在“**原理与机制**”一章中，我们将深入连续介质力学的核心，定义变形、应变和应力，并建立[超弹性](@entry_id:159356)和黏弹性等先进材料模型的理论基础。接着，在“**应用与跨学科联系**”一章中，我们将通过丰富的案例，展示这些理论如何在人体运动分析、手术导航、组织工程和医学成像等领域发挥作用，凸显理论与实践的结合。最后，在“**动手实践**”部分，您将有机会通过解决具体问题来巩固所学知识，将抽象的数学公式转化为解决实际生物力学挑战的能力。

## 原理与机制

在对生物组织的力学行为进行建模时，我们面临一个根本性的选择：是将其视为一个不会变形的**[刚体](@entry_id:1131033)（rigid body）**，还是一个能够改变形状和体积的**[可变形体](@entry_id:1123496)（deformable body）**。虽然[刚体模型](@entry_id:1131036)在许多生物力学分析中（例如，在宏观尺度上研究骨骼的运动学）是一个有效且方便的简化，但对于软组织如肌肉、韧带、皮肤和血管而言，变形是其功能的内在组成部分。本章旨在深入探讨描述这两种力学行为的核心原理和数学框架，为后续章节中更复杂的[本构模型](@entry_id:174726)和应用奠定基础。

我们将从[连续介质运动学](@entry_id:747813)的基本概念出发，区分描述运动的不同方式，并定义量化局部变形的关键物理量。随后，我们将探讨几种核心的变形度量方式，并阐明理想化模型（如[刚体](@entry_id:1131033)和[线性弹性](@entry_id:166983)体）的适用性与局限性。最后，我们将介绍适用于[可变形体](@entry_id:1123496)的基本平衡定律，并构建描述[超弹性](@entry_id:159356)与黏弹性等复杂材料行为的本构关系框架。

### [连续介质运动学](@entry_id:747813)描述

#### 运动的描述：参考构型与当前构型

为了精确描述一个物体的变形，我们首先需要建立一个坐标系。在[连续介质力学](@entry_id:155125)中，我们区分两种构型（configuration）：**参考构型（reference configuration）** $\mathcal{B}_0$ 和**当前构型（current configuration）** $\mathcal{B}_t$。参考构型是物体在某个初始时刻（通常是 $t=0$）的形状，我们用物质坐标（material coordinates）$\mathbf{X}$ 来标记该构型中的每一个物质点。当前构型则是物体在任意时刻 $t$ 的形状，我们用空间坐标（spatial coordinates）$\mathbf{x}$ 来描述物[质点](@entry_id:186768)在物理空间中的位置。

物体的运动（motion）可以通过一个映射函数 $\boldsymbol{\varphi}$ 来描述，它将每个物质点从其[参考位](@entry_id:754187)置 $\mathbf{X}$ 映射到其在时刻 $t$ 的空间位置 $\mathbf{x}$：
$$ \mathbf{x} = \boldsymbol{\varphi}(\mathbf{X}, t) $$
这个映射是[连续介质运动学](@entry_id:747813)的基础。描述附加在物[质点](@entry_id:186768)上的物理量（如位移）的场，称为**物质场（material field）**，因为它以物质坐标 $\mathbf{X}$ 为变量。而描述在空间某点上的物理量（如速度）的场，则称为**空间场（spatial field）**，因为它以空间坐标 $\mathbf{x}$ 为变量。

例如，**[位移场](@entry_id:141476)（displacement field）** $\mathbf{u}$ 被定义为一个物[质点](@entry_id:186768)从[参考位](@entry_id:754187)置到当前位置的向量。它自然地是一个物质场：
$$ \mathbf{u}(\mathbf{X}, t) = \boldsymbol{\varphi}(\mathbf{X}, t) - \mathbf{X} $$
而**速度场（velocity field）** $\mathbf{v}$ 通常被定义为在空间点 $\mathbf{x}$ 的物质[瞬时速度](@entry_id:167797)，因此它是一个空间场。它与运动映射的关系通过[复合函数](@entry_id:147347)给出，其中速度是固定物[质点](@entry_id:186768) $\mathbf{X}$ 的位置随时间的变化率：
$$ \mathbf{v}(\boldsymbol{\varphi}(\mathbf{X}, t), t) = \frac{\partial \boldsymbol{\varphi}(\mathbf{X}, t)}{\partial t} \bigg|_{\mathbf{X}} $$

在处理生物组织时，我们隐式地采用了**连续介质假设（continuum hypothesis）**。生物组织由离散的细胞、纤维和[细胞外基质](@entry_id:136546)构成，但在宏观尺度上，我们可以忽略其微观结构，并假设质量、应力、应变等物理量在空间中是连续且光滑分布的。这一假设的有效性取决于[尺度分离](@entry_id:270204)：微观结构的特征长度 $\ell_m$（如细胞直径或纤维间距）必须远小于我们关心的宏观几何特征长度 $L$（如器官尺寸），即 $\ell_m/L \ll 1$。在这种情况下，我们可以定义一个**代表性体积元（Representative Volume Element, RVE）**，它足够小以至于在宏观上可被视为一个点，但又足够大以至于包含了具有统计代表性的微观结构信息。

#### 变形梯度：局部变形的度量

虽然位移场 $\mathbf{u}$ 描述了物体的整体位置变化，但它本身并不能直接揭示材料局部的拉伸、剪切或旋转。例如，一个物体可以经历巨大的位移（如平移），但其内部完全没有变形。 为了量化局部变形，我们需要考察相邻物质点的相对位移，这自然引出了对运动映射求梯度的思想。

**变形梯度张量（deformation gradient tensor）** $\mathbf{F}$ 被定义为运动映射 $\boldsymbol{\varphi}$ 对物质坐标 $\mathbf{X}$ 的梯度：
$$ \mathbf{F}(\mathbf{X}, t) = \frac{\partial \mathbf{x}}{\partial \mathbf{X}} = \nabla_{\mathbf{X}} \boldsymbol{\varphi}(\mathbf{X}, t) $$
变形梯度是一个[二阶张量](@entry_id:199780)，它包含了关于一个物质点邻域内局部变形的全部信息。它的基本作用是将参考构型中的一个无限小[线元](@entry_id:196833) $d\mathbf{X}$ 映射到当前构型中的对应线元 $d\mathbf{x}$：
$$ d\mathbf{x} = \mathbf{F} \, d\mathbf{X} $$
由此可见，$\mathbf{F}$ 描述了[线元](@entry_id:196833)如何被拉伸、剪切和旋转。例如，在纯[平移运动](@entry_id:911899) $\mathbf{x} = \mathbf{X} + \mathbf{c}(t)$ 中，$\mathbf{F} = \mathbf{I}$（单位张量），表明没有局部变形。而在纯[刚体](@entry_id:1131033)旋转 $\mathbf{x} = \mathbf{R}(t)\mathbf{X}$ 中，$\mathbf{F} = \mathbf{R}(t)$，其中 $\mathbf{R}(t)$ 是一个[旋转张量](@entry_id:191990)。这表明，要从[位移场](@entry_id:141476)中提取局部变形信息，必须计算其梯度，即**[位移梯度张量](@entry_id:748571)** $\nabla_{\mathbf{X}}\mathbf{u} = \mathbf{F} - \mathbf{I}$。

### 变形的运动学度量

#### 极分解定理：旋转与拉伸的分离

变形梯度 $\mathbf{F}$ 将旋转和拉伸两种运动学效应耦合在一起。**极分解定理（Polar Decomposition Theorem）**提供了一种将这两种效应[解耦](@entry_id:160890)的严谨方法。该定理指出，任何可逆的变形梯度 $\mathbf{F}$ 都可以唯一地分解为：
$$ \mathbf{F} = \mathbf{R}\mathbf{U} = \mathbf{V}\mathbf{R} $$
其中：
- $\mathbf{R}$ 是一个**正常正交张量**（proper orthogonal tensor），属于[特殊正交群](@entry_id:146418) $SO(3)$，即满足 $\mathbf{R}^T\mathbf{R}=\mathbf{I}$ 且 $\det(\mathbf{R})=1$。它代表了物质的**局部[刚体](@entry_id:1131033)旋转（local rigid-body rotation）**。
- $\mathbf{U}$ 和 $\mathbf{V}$ 分别是**右[拉伸张量](@entry_id:193200)（right stretch tensor）**和**左[拉伸张量](@entry_id:193200)（left stretch tensor）**。它们都是对称正定张量，代表了纯粹的拉伸变形。

这种分解具有清晰的物理意义：$F=RU$ 可以理解为先在参考构型中沿主拉伸方向进行纯拉伸（由 $\mathbf{U}$ 描述），然后再进行一次[刚体](@entry_id:1131033)旋转（由 $\mathbf{R}$ 描述）到达最终构型。而 $F=VR$ 则可理解为先进行[刚体](@entry_id:1131033)旋转，再在旋转后的空间构型中进行纯拉伸（由 $\mathbf{V}$ 描述）。

右[拉伸张量](@entry_id:193200) $\mathbf{U}$ 与左[拉伸张量](@entry_id:193200) $\mathbf{V}$ 的特征值相同，它们被称为**主拉伸（principal stretches）**，记为 $\lambda_1, \lambda_2, \lambda_3$。它们量化了材料在三个相互正交的[主方向](@entry_id:276187)上的拉伸程度。

#### [应变张量](@entry_id:1132487)：变形的真实度量

为了构建一个只度量变形（拉伸和剪切）而不受[刚体](@entry_id:1131033)旋转影响的量，我们考察[线元](@entry_id:196833)长度的平方的变化。参考构型中线元 $d\mathbf{X}$ 的长度平方为 $ds_0^2 = d\mathbf{X} \cdot d\mathbf{X}$。变形后，其长度平方变为：
$$ ds^2 = d\mathbf{x} \cdot d\mathbf{x} = (\mathbf{F}d\mathbf{X}) \cdot (\mathbf{F}d\mathbf{X}) = d\mathbf{X} \cdot (\mathbf{F}^T\mathbf{F} \, d\mathbf{X}) $$
我们定义**右柯西-格林变形张量（right Cauchy-Green deformation tensor）** $\mathbf{C} = \mathbf{F}^T\mathbf{F}$。这个张量完全在参考构型中定义，并且与极分解中的右[拉伸张量](@entry_id:193200)有直接关系：$\mathbf{C} = \mathbf{U}^2$。长度平方的变化可以写为：
$$ ds^2 - ds_0^2 = d\mathbf{X} \cdot (\mathbf{C} - \mathbf{I}) d\mathbf{X} $$
由此，我们定义**[格林-拉格朗日应变张量](@entry_id:187745)（Green-Lagrange strain tensor）** $\mathbf{E}$：
$$ \mathbf{E} = \frac{1}{2}(\mathbf{C} - \mathbf{I}) = \frac{1}{2}(\mathbf{F}^T\mathbf{F} - \mathbf{I}) $$
$\mathbf{E}$ 是一个**物质[应变度量](@entry_id:755495)（material measure of strain）**，它完全不受[刚体](@entry_id:1131033)旋转的影响（因为 $\mathbf{C}$ 不受旋转影响），并且当且仅当没有变形时（即运动为纯[刚体运动](@entry_id:144691)）为零。

类似地，我们也可以从当前构型出发定义应变。定义**左柯西-格林变形张量（left Cauchy-Green deformation tensor）** $\mathbf{b} = \mathbf{F}\mathbf{F}^T$，它与左[拉伸张量](@entry_id:193200)相关：$\mathbf{b} = \mathbf{V}^2$。通过相似的推导，可以得到**[阿尔曼西应变](@entry_id:191140)张量（Almansi strain tensor）** $\mathbf{e}$：
$$ \mathbf{e} = \frac{1}{2}(\mathbf{I} - \mathbf{b}^{-1}) $$
$\mathbf{e}$ 是一个**空间[应变度量](@entry_id:755495)（spatial measure of strain）**，因为它与当前构型中的线元 $d\mathbf{x}$ 相关。它同样不受刚体运动影响，是有限变形理论中另一个常用的[应变度量](@entry_id:755495)。

### 理想化模型及其局限性

#### [刚体模型](@entry_id:1131036)

**[刚体](@entry_id:1131033)（rigid body）**是一个理想化的模型，其内部任意两点间的距离在运动过程中保持不变。从运动学的角度看，这意味着变形梯度 $\mathbf{F}$ 在物体中处处为一个[旋转张量](@entry_id:191990) $\mathbf{Q}(t) \in SO(3)$。此时，$\mathbf{C} = \mathbf{Q}^T\mathbf{Q} = \mathbf{I}$，因此[格林-拉格朗日应变](@entry_id:170427) $\mathbf{E}$ 恒为零。刚体运动可以表示为平移和旋转的叠加：$\mathbf{x}(\mathbf{X}, t) = \mathbf{c}(t) + \mathbf{Q}(t)\mathbf{X}$。

在实际应用中，没有任何物体是绝对刚性的。[刚体模型](@entry_id:1131036)是一种近似，当材料的变形非常小，以至于应变引起的形状和尺寸变化远小于实验测量的精度时，这种近似就是合理的。数学上，这可以表示为范数 $\|\mathbf{F}^T\mathbf{F} - \mathbf{I}\| \le \delta$，其中 $\delta$ 是一个与实验不确定度相关的小量。

#### 小应变[线性弹性](@entry_id:166983)模型

当[位移梯度](@entry_id:165352)很小（$\|\nabla\mathbf{u}\| \ll 1$）时，我们可以对[格林-拉格朗日应变张量](@entry_id:187745)进行线性化。在这种情况下，$\mathbf{E} \approx \frac{1}{2}(\nabla\mathbf{u} + (\nabla\mathbf{u})^T)$。我们定义**[无穷小应变张量](@entry_id:167211)（infinitesimal strain tensor）**为：
$$ \boldsymbol{\varepsilon} = \frac{1}{2}(\nabla\mathbf{u} + (\nabla\mathbf{u})^T) $$
对于**各向同性[线性弹性](@entry_id:166983)材料（isotropic linear elastic material）**，其[本构关系](@entry_id:186508)（[应力-应变关系](@entry_id:274093)）由**[胡克定律](@entry_id:149682)（Hooke's Law）**给出：
$$ \boldsymbol{\sigma} = \lambda \, \text{tr}(\boldsymbol{\varepsilon})\mathbf{I} + 2\mu \, \boldsymbol{\varepsilon} $$
其中 $\boldsymbol{\sigma}$ 是柯西应力张量，$\lambda$ 和 $\mu$ 是材料的**拉梅参数（Lamé parameters）**。该模型预测应力与应变成线性关系，且材料的刚度在所有方向上都相同。

然而，这个广泛用于传统工程材料的模型在应用于软生物组织时有其根本性的局限性：
1.  **无法处理大转动**：[无穷小应变张量](@entry_id:167211) $\boldsymbol{\varepsilon}$ 并非在客观性上是精确的。例如，对于一个有限的[刚体](@entry_id:1131033)旋转，$\boldsymbol{\varepsilon}$ 并不为零，这意味着模型会错误地预测在纯旋转下会产生应力。这违反了**物质[标架无关性原理](@entry_id:200995)（principle of material frame-indifference）**。
2.  **无法描述[非线性](@entry_id:637147)行为**：许多软组织（如肌腱）表现出**[应变硬化](@entry_id:1132472)（strain-stiffening）**行为，即材料在拉伸时会变得越来越硬。线性模型无法捕捉这种[非线性响应](@entry_id:188175)。
3.  **无法描述各向异性**：由于胶原纤维等结构的存在，软组织的力学特性通常是方向依赖的（**各向异性 anisotropy**）。各向同性模型无法描述这种行为。

这些局限性促使我们必须采用基于有限变形理论的更高级本构模型来准确描述软组织的力学行为。

### 连续介质的基本[平衡定律](@entry_id:171298)

对于[可变形体](@entry_id:1123496)，其运动不仅受运动学约束，还必须遵循物理学的基本平衡定律。这些定律的局部（[微分](@entry_id:158422)）形式构成了控制方程。

- **质量守恒（Conservation of Mass）**：局部[质量守恒定律](@entry_id:147377)，也称为**[连续性方程](@entry_id:195013)（continuity equation）**，其[欧拉形式](@entry_id:637896)为：
  $$ \frac{\partial\rho}{\partial t} + \nabla \cdot (\rho\mathbf{v}) = 0 $$
  其中 $\rho$ 是当前质量密度，$\mathbf{v}$ 是速度场。对于密度恒定的[不可压缩材料](@entry_id:159741)，该方程简化为 $\nabla \cdot \mathbf{v} = 0$。

- **[线性动量守恒](@entry_id:165717)（Conservation of Linear Momentum）**：这是牛顿第二定律在连续介质中的推广，也称为**柯西第一运动定律（Cauchy's first law of motion）**：
  $$ \nabla \cdot \boldsymbol{\sigma} + \rho\mathbf{b} = \rho\mathbf{a} $$
  其中 $\boldsymbol{\sigma}$ 是柯西[应力张量](@entry_id:148973)，$\mathbf{b}$ 是单位质量的体力（如重力），$\mathbf{a}$ 是[物质加速度](@entry_id:270992)。该方程表明，应力的空间梯度（内力）和体力（外力）共同驱动物质的加速。即使在[刚体](@entry_id:1131033)旋转运动中，也需要非均匀的应[力场](@entry_id:147325)来提供[向心加速度](@entry_id:190458)。

- **[角动量守恒](@entry_id:156798)（Conservation of Angular Momentum）**：在没有体力矩和耦合应力的情况下，[角动量守恒](@entry_id:156798)定律（柯西第二运动定律）要求柯西[应力张量](@entry_id:148973)必须是对称的：
  $$ \boldsymbol{\sigma} = \boldsymbol{\sigma}^T $$
  这是经典连续介质力学的一个基本结论。

- **能量守恒（Conservation of Energy）**：能量守恒的第一定律引入了内能和热量。在力学分析中，我们特别关注机械功。**[应力功率](@entry_id:182907)密度（stress power density）**，即单位体积内应力做功的速率，由[应力张量](@entry_id:148973)和**应变率张量（rate of deformation tensor）** $\mathbf{d} = \text{sym}(\nabla\mathbf{v})$ 的缩并给出：$w = \boldsymbol{\sigma}:\mathbf{d}$。对于任何[刚体运动](@entry_id:144691)，$\mathbf{d}=0$，因此[应力功率](@entry_id:182907)为零。只有在发生变形时，[内力](@entry_id:167605)才会做功并改变系统的内能。

### [超弹性](@entry_id:159356)组织的[本构模型](@entry_id:174726)

**[超弹性](@entry_id:159356)（Hyperelasticity）**是一种理想的弹性行为，其中应力完全由当前变形状态决定，并且[应力-应变关系](@entry_id:274093)可以从一个[标量势](@entry_id:276177)函数——**[应变能密度函数](@entry_id:755490)（strain energy density function）** $W$ ——导出。

#### [客观性原理](@entry_id:185412)

如前所述，[本构定律](@entry_id:178936)必须独立于观察者的参考系。这一**[客观性原理](@entry_id:185412)（principle of objectivity）**或物质[标架无关性原理](@entry_id:200995)，对 $W$ 的形式施加了严格的约束。它要求对于任何叠加的[刚体](@entry_id:1131033)旋转 $\mathbf{Q}$，应变能必须保持不变：$W(\mathbf{Q}\mathbf{F}) = W(\mathbf{F})$。这一要求的结果是，应变能函数 $W$ 不能直接依赖于包含旋转信息的 $\mathbf{F}$，而只能依赖于纯[拉伸张量](@entry_id:193200) $\mathbf{U}$，或等价地，依赖于[右柯西-格林张量](@entry_id:174156) $\mathbf{C} = \mathbf{F}^T\mathbf{F}$。因此，任何客观的[超弹性](@entry_id:159356)模型都可以写成 $W = \hat{W}(\mathbf{C})$。

#### 各向同性[超弹性](@entry_id:159356)

如果材料是**各向同性的（isotropic）**，那么其本构关系还必须在参考构型中具有旋转不变性。这意味着 $\hat{W}(\mathbf{C})$ 必须是一个[各向同性张量](@entry_id:195105)函数，根据[张量表示](@entry_id:180492)理论，这样的函数只能通过其宗量的**[主不变量](@entry_id:193522)（principal invariants）**来表达。对于 $3 \times 3$ 的张量 $\mathbf{C}$，其三个[主不变量](@entry_id:193522)为：
- $I_1 = \text{tr}(\mathbf{C}) = \lambda_1^2 + \lambda_2^2 + \lambda_3^2$
- $I_2 = \frac{1}{2}[(\text{tr}\mathbf{C})^2 - \text{tr}(\mathbf{C}^2)] = \lambda_1^2\lambda_2^2 + \lambda_2^2\lambda_3^2 + \lambda_3^2\lambda_1^2$
- $I_3 = \det(\mathbf{C}) = (\lambda_1\lambda_2\lambda_3)^2 = J^2$

其中 $\lambda_i$ 是主拉伸，$J=\det(\mathbf{F})$ 是体积变化率。因此，各向同性[超弹性材料](@entry_id:190241)的应变能函数可以写成 $W = \tilde{W}(I_1, I_2, I_3)$。这些不变量是描述纯变形大小的自然变量。 

#### [各向异性超弹性](@entry_id:191276)

对于像肌腱和韧带这样具有优先方向（如胶原纤维方向）的各向异性组织，应变能函数还必须依赖于这些方向。对于具有单一纤维方向的**横观各向同性（transversely isotropic）**材料，我们可以定义一个参考构型中的[单位向量](@entry_id:165907) $\mathbf{a}_0$ 来表示纤维方向。为了构建客观的[本构模型](@entry_id:174726)，我们引入额外的**伪不变量（pseudo-invariants）**，它们将纤维方向与变形耦合起来。最常用的两个是：
- $I_4 = \mathbf{a}_0 \cdot \mathbf{C} \mathbf{a}_0 = \text{tr}(\mathbf{C}\mathbf{M})$，其中 $\mathbf{M} = \mathbf{a}_0 \otimes \mathbf{a}_0$ 是**结构张量（structural tensor）**。$I_4 = \lambda_f^2$，即纤维方向拉伸的平方。
- $I_5 = \mathbf{a}_0 \cdot \mathbf{C}^2 \mathbf{a}_0 = \text{tr}(\mathbf{C}^2\mathbf{M})$

横观[各向同性材料](@entry_id:170678)的[应变能函数](@entry_id:178435)通常写成 $W = W(I_1, I_2, I_3, I_4, I_5)$。一个简单的例子是 $W = W_{iso}(I_1, I_2) + W_{aniso}(I_4)$，例如 $W(I_1, I_4) = \frac{\mu}{2}(I_1 - 3) + \frac{k}{2}(I_4 - 1)^2$，其中后一项专门惩罚纤维方向的拉伸。

#### [不可压缩性](@entry_id:274914)

许多软组织在生理变形范围内近似**不可压缩的（incompressible）**。这在运动学上表示为一个约束：体积变化率 $J = \det(\mathbf{F}) = 1$。在[变分原理](@entry_id:198028)中，这个约束通过引入一个**[拉格朗日乘子](@entry_id:142696)（Lagrange multiplier）** $p$ 来强制执行，该乘子在物理上可以解释为**[静水压力](@entry_id:275365)（hydrostatic pressure）**。

其结果是，[不可压缩材料](@entry_id:159741)的柯西应力张量总是可以分解为一个由变形决定的“弹性”部分 $\boldsymbol{\sigma}_{el}$ 和一个不定的静水压力部分：
$$ \boldsymbol{\sigma} = -p\mathbf{I} + \boldsymbol{\sigma}_{el} $$
压[力场](@entry_id:147325) $p$ 本身不是由[本构定律](@entry_id:178936)决定的，而是作为一个未知场，与[位移场](@entry_id:141476)一起通过求解[平衡方程](@entry_id:172166)和边界条件来确定。它确保了在任何变形下 $J=1$ 的约束都得到满足。在数值上，这种方法等价于使用一个体积[罚函数](@entry_id:638029) $U(J) = \frac{1}{2}K(J-1)^2$ 并在罚参数（体积模量 $K$）趋于无穷大的极限情况。

### 时间依赖行为：黏弹性

生物软组织不仅表现出弹性，还表现出**黏弹性（viscoelasticity）**，即它们的力学响应依赖于时间或加载速率。黏弹性行为可以概念化为纯弹性元件（弹簧）和纯黏性元件（阻尼器）的组合。

- **线性弹簧**: $\sigma_s = 2\mu\varepsilon_s$
- **牛顿阻尼器**: $\sigma_d = 2\eta\dot{\varepsilon}_d$

两种最简单的组合模型是[Maxwell模型](@entry_id:157958)和[Kelvin-Voigt模型](@entry_id:195229)。

- **Maxwell模型（串联）**：弹簧和阻尼器串联，应力相等，应变相加。其本构方程为：
  $$ \dot{\varepsilon} = \frac{1}{2\mu}\dot{\sigma} + \frac{1}{2\eta}\sigma $$
  在应变阶跃（$\varepsilon(t) = \varepsilon_0 H(t)$）下，Maxwell模型表现出**[应力松弛](@entry_id:159905)（stress relaxation）**，应力随时间指数衰减。在应力阶跃（$\sigma(t) = \sigma_0 H(t)$）下，它表现出瞬时[弹性应变](@entry_id:189634)，然后是无限的线性**[蠕变](@entry_id:150410)（creep）**。

- **[Kelvin-Voigt模型](@entry_id:195229)（并联）**：弹簧和阻尼器并联，应变相等，应力相加。其本构方程为：
  $$ \sigma = 2\mu\varepsilon + 2\eta\dot{\varepsilon} $$
  在应变阶跃下，该模型预测一个瞬时的无限应力（由于阻尼器），然后应力保持恒定，不发生松弛。在应力阶跃下，它表现出有界的渐进蠕变，应变最终趋于一个稳定值。

肌腱和韧带等真实组织既表现出明显的[应力松弛](@entry_id:159905)，也表现出可测量的蠕变。Maxwell模型能描述松弛但不能描述有界[蠕变](@entry_id:150410)，而[Kelvin-Voigt模型](@entry_id:195229)能描述有界蠕变但不能描述松弛。因此，这两种简单的模型都不能单独完整地描述软组织的黏弹性行为。为了更准确地建模，需要更复杂的模型，如**[标准线性固体模型](@entry_id:204500)（Standard Linear Solid, SLS）**或由多个Maxwell元件组成的**[广义Maxwell模型](@entry_id:169862)（[Prony级数](@entry_id:204348)）**。