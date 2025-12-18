## 引言
在连续介质力学中，精确描述物体的运动和形状变化是一切分析的出发点。变形运动学（Kinematics of Deformation）正是为此而生的数学语言，它为我们量化从参考状态到当前状态的几何变化提供了严谨的工具，是理解应力、应变以及材料本构关系的基础。然而，如何有效地区分引起[内力](@entry_id:167605)变化的真实“变形”与不产生应力的“刚体运动”？如何统一处理土木工程中的微小变形与生物软组织、高分子材料中的巨[大变形](@entry_id:167243)？这构成了[连续介质力学](@entry_id:155125)中的一个核心知识体系。

本教程旨在系统性地引导您深入掌握这一领域。在第一章“原理与机制”中，我们将从最基本的变形梯度概念出发，逐步构建起描述拉伸、旋转和应变的完整数学框架，并着重辨析有限应变与微小应变理论的本质区别与适用场景。随后，在第二章“应用与跨学科联系”中，我们将通过丰富的实例，展示这些抽象的运动学概念如何在高等固体力学、[计算模拟](@entry_id:146373)、材料科学乃至生物力学等前沿领域中扮演关键角色，将理论与工程和科学实践紧密相连。最后，第三章“动手实践”部分将提供若干精心设计的计算练习，旨在通过实际操作加深您对关键概念的理解和应用能力，确保您不仅知其然，更知其所以然。

## 原理与机制

本章旨在深入探讨描述物体变形的运动学原理与机制。继引言之后，我们将从变形的最基本度量——变形梯度（deformation gradient）出发，系统地构建描述变形、[拉伸与旋转](@entry_id:150197)的数学框架。我们将区分有限应变与微小应变理论，并阐述它们在不同物理情境下的适用性。最后，我们将讨论几个高级主题：确保物理定律在不同观测者下保持一致的[客观性原理](@entry_id:185412)，材料不可压缩性的运动学约束，以及保证连续变形场存在的[相容性条件](@entry_id:637057)。

### 变形梯度：变形的基本度量

连续介质力学的核心任务是描述一个物体（或称“构型”）如何从其初始（或“参考”）位置移动和变形到其当前位置。这一过程由一个光滑的**运动映射** $\boldsymbol{\varphi}$ 来描述，它将参考构型 $\Omega_0$ 中的每个物质点 $\boldsymbol{X}$ 映射到当前构型 $\Omega_t$ 中的空间位置 $\boldsymbol{x}$：

$$
\boldsymbol{x} = \boldsymbol{\varphi}(\boldsymbol{X}, t)
$$

为了量化物质点 $\boldsymbol{X}$ 邻域内的局部变形，我们引入了**变形梯度张量** $\boldsymbol{F}$。它被定义为运动映射 $\boldsymbol{\varphi}$ 对参考坐标 $\boldsymbol{X}$ 的梯度：

$$
\boldsymbol{F}(\boldsymbol{X}, t) = \nabla_{\boldsymbol{X}} \boldsymbol{\varphi}(\boldsymbol{X}, t)
$$

其分量形式为 $F_{iJ} = \partial x_i / \partial X_J$。变形梯度 $\boldsymbol{F}$ 是一个[二阶张量](@entry_id:199780)，它包含了关于局部变形的所有信息。它的几何意义在于，它将参考构型中一个无限小的物质[线元](@entry_id:196833) $d\boldsymbol{X}$ 映射到当前构型中对应的空间[线元](@entry_id:196833) $d\boldsymbol{x}$：

$$
d\boldsymbol{x} = \boldsymbol{F} \, d\boldsymbol{X}
$$

除了运动映射，我们还可以用**位移场** $\boldsymbol{u}$ 来描述变形，它表示物质点从[参考位](@entry_id:754187)置到当前位置的矢量差。在**拉格朗日描述**（Lagrangian description）中，位移是[参考位](@entry_id:754187)置 $\boldsymbol{X}$ 的函数：

$$
\boldsymbol{u}(\boldsymbol{X}, t) = \boldsymbol{\varphi}(\boldsymbol{X}, t) - \boldsymbol{X}
$$

对上式求关于 $\boldsymbol{X}$ 的梯度，我们可以得到变形梯度 $\boldsymbol{F}$ 与**[位移梯度](@entry_id:165352)** $\nabla_{\boldsymbol{X}} \boldsymbol{u}$ 之间的直接关系 ：

$$
\boldsymbol{F} = \nabla_{\boldsymbol{X}} (\boldsymbol{u} + \boldsymbol{X}) = \nabla_{\boldsymbol{X}} \boldsymbol{u} + \nabla_{\boldsymbol{X}} \boldsymbol{X} = \boldsymbol{I} + \nabla_{\boldsymbol{X}} \boldsymbol{u}
$$

其中 $\boldsymbol{I}$ 是二阶单位张量。这个关系是线性的，它表明变形梯度可以分解为一个单位张量（代表未变形状态）和一个[位移梯度张量](@entry_id:748571)（代表由位移引起的所有局部变化，包括拉伸和旋转）之和。

变形梯度一个至关重要的属性是它的行列式，记为 $J = \det \boldsymbol{F}$，通常称为**[雅可比行列式](@entry_id:137120)**。$J$ 描述了局部的体积变化。一个位于 $\boldsymbol{X}$ 处的参考体积微元 $dV$ 在变形后，其当前体积 $dv$ 由下式给出 ：

$$
dv = J \, dV
$$

因此，$J$ 是当前体积与参考体积之比。基于物质不可穿透的物理原理，物质点不能相互重叠，并且[局部坐标系](@entry_id:751394)的“手性”（例如，从[右手系](@entry_id:166669)变为左手系）不能翻转。这要求 $J > 0$。$J=1$ 的情况对应于**[等容变形](@entry_id:196451)**或**不可压缩变形**，即变形过程中局部[体积保持](@entry_id:141001)不变。$0 \lt J \lt 1$ 表示体积压缩，而 $J > 1$ 表示[体积膨胀](@entry_id:144241)。

体积变化与质量密度直接相关。根据质量守恒定律，一个物质微元的质量 $dm$ 在变形前后保持不变，即 $dm = \rho_0 dV = \rho dv$，其中 $\rho_0$ 和 $\rho$ 分别是参考构型和当前构型的质量密度。结合 $dv = J dV$，我们立即得到它们之间的关系：

$$
\rho = \frac{\rho_0}{J}
$$

这个关系在模拟不可压缩或近乎不可压缩的材料（如橡胶、许多生物软组织和流体）时至关重要 。

### 应变张量：变形的纯粹度量

变形梯度 $\boldsymbol{F}$ 包含了拉伸、剪切和[刚体](@entry_id:1131033)旋转的全部信息。然而，在材料的本构关系中（即应力与变形的关系），我们通常只关心引起内力变化的“纯”变形部分，而希望排除不产生应力的[刚体运动](@entry_id:144691)。**[应变张量](@entry_id:1132487)**（strain tensors）正是为此而生。

#### 有限应变

对于任意大小的变形，我们需要一个在刚体运动下保持不变（即客观）的应变量。考虑一个[线元](@entry_id:196833) $d\boldsymbol{X}$，其变形后的长度平方为：

$$
\|d\boldsymbol{x}\|^2 = d\boldsymbol{x} \cdot d\boldsymbol{x} = (\boldsymbol{F} d\boldsymbol{X}) \cdot (\boldsymbol{F} d\boldsymbol{X}) = d\boldsymbol{X} \cdot (\boldsymbol{F}^T \boldsymbol{F} \, d\boldsymbol{X})
$$

我们定义**右柯西-格林变形张量**（right Cauchy-Green deformation tensor）为 $\boldsymbol{C} = \boldsymbol{F}^T \boldsymbol{F}$。于是，$\|d\boldsymbol{x}\|^2 = d\boldsymbol{X} \cdot (\boldsymbol{C} d\boldsymbol{X})$。张量 $\boldsymbol{C}$ 完全描述了物[质点](@entry_id:186768)邻域内的长度和角度如何变化。考虑一个[刚体运动](@entry_id:144691)，其运动形式为 $\boldsymbol{x} = \boldsymbol{Q}\boldsymbol{X} + \boldsymbol{c}$，其中 $\boldsymbol{Q}$ 是一个[旋转张量](@entry_id:191990)（$\boldsymbol{Q}^T\boldsymbol{Q}=\boldsymbol{I}$），$\boldsymbol{c}$ 是一个平移向量。此时变形梯度 $\boldsymbol{F} = \boldsymbol{Q}$，于是 $\boldsymbol{C} = \boldsymbol{Q}^T\boldsymbol{Q} = \boldsymbol{I}$。这表明 $\boldsymbol{C}$ 在[刚体](@entry_id:1131033)平移和旋转下等于单位张量，因此它“看”不到刚体运动。

为了定义一个在未变形状态下为零的应变量，我们引入**[格林-拉格朗日应变张量](@entry_id:187745)**（Green-Lagrange strain tensor）$\boldsymbol{E}$ ：

$$
\boldsymbol{E} = \frac{1}{2}(\boldsymbol{C} - \boldsymbol{I}) = \frac{1}{2}(\boldsymbol{F}^T \boldsymbol{F} - \boldsymbol{I})
$$

$\boldsymbol{E}$ 是一个真正意义上的应变量：对于任何刚体运动，$\boldsymbol{F}=\boldsymbol{Q}$，$\boldsymbol{E}=\frac{1}{2}(\boldsymbol{Q}^T\boldsymbol{Q} - \boldsymbol{I}) = \boldsymbol{0}$；而在未变形状态下（$\boldsymbol{F}=\boldsymbol{I}$），$\boldsymbol{E}$ 也为零。将 $\boldsymbol{F} = \boldsymbol{I} + \nabla_{\boldsymbol{X}}\boldsymbol{u}$ 代入，我们得到 $\boldsymbol{E}$ 与[位移梯度](@entry_id:165352)的关系：

$$
\boldsymbol{E} = \frac{1}{2} \left( (\boldsymbol{I} + \nabla_{\boldsymbol{X}}\boldsymbol{u})^T (\boldsymbol{I} + \nabla_{\boldsymbol{X}}\boldsymbol{u}) - \boldsymbol{I} \right) = \frac{1}{2} \left( \nabla_{\boldsymbol{X}}\boldsymbol{u} + (\nabla_{\boldsymbol{X}}\boldsymbol{u})^T + (\nabla_{\boldsymbol{X}}\boldsymbol{u})^T \nabla_{\boldsymbol{X}}\boldsymbol{u} \right)
$$

这个表达式清楚地显示了 $\boldsymbol{E}$ 与[位移梯度](@entry_id:165352)之间的**[非线性](@entry_id:637147)**关系，其中 $(\nabla_{\boldsymbol{X}}\boldsymbol{u})^T \nabla_{\boldsymbol{X}}\boldsymbol{u}$ 是二次项。这种[非线性](@entry_id:637147)是有限变形理论的标志。

#### 微小应变

在许多工程应用中，变形非常小，即[位移梯度](@entry_id:165352)及其所有分量的绝对值都远小于1（$\|\nabla_{\boldsymbol{X}}\boldsymbol{u}\| \ll 1$）。在这种情况下，我们可以忽略 $\boldsymbol{E}$表达式中的二次项，从而得到一个线性化的应变量，即**[无穷小应变张量](@entry_id:167211)**（infinitesimal strain tensor）或**柯西[应变张量](@entry_id:1132487)**（Cauchy strain tensor）$\boldsymbol{\varepsilon}$ ：

$$
\boldsymbol{\varepsilon} = \frac{1}{2} \left( \nabla_{\boldsymbol{X}}\boldsymbol{u} + (\nabla_{\boldsymbol{X}}\boldsymbol{u})^T \right)
$$

$\boldsymbol{\varepsilon}$ 就是[位移梯度](@entry_id:165352)的对称部分。线性化的一个重要后果是，$\boldsymbol{\varepsilon}$ 对于有限大小的[刚体](@entry_id:1131033)旋转**不是**客观的。对于一个纯旋转 $\boldsymbol{F}=\boldsymbol{Q}$，[位移梯度](@entry_id:165352)为 $\nabla_{\boldsymbol{X}}\boldsymbol{u} = \boldsymbol{Q}-\boldsymbol{I}$，对应的微小应变为 $\boldsymbol{\varepsilon} = \frac{1}{2}(\boldsymbol{Q}+\boldsymbol{Q}^T) - \boldsymbol{I}$。除非 $\boldsymbol{Q}=\boldsymbol{I}$（无旋转）或旋转是无穷小量，否则 $\boldsymbol{\varepsilon}$ 不为零。这意味着微小应变理论无法区分小应变和大转动。

尽管有此局限，线性化带来了巨大的简化。例如，在[热弹性](@entry_id:158447)或塑性理论中，小应变框架允许应变的**加法分解**，如总应变等于弹性应变、塑性应变和[热应变](@entry_id:187744)之和 ($\boldsymbol{\varepsilon} = \boldsymbol{\varepsilon}_e + \boldsymbol{\varepsilon}_p + \boldsymbol{\varepsilon}_{th}$)。相比之下，在[有限应变理论](@entry_id:176941)中，这种分解通常以**乘法形式**作用于变形梯度上（例如 $\boldsymbol{F} = \boldsymbol{F}_e \boldsymbol{F}_p$），这在数学上更为复杂 。

### 变形的分解：[拉伸与旋转](@entry_id:150197)

变形梯度 $\boldsymbol{F}$ 将拉伸和旋转两种效应耦合在一起。**极分解定理**（polar decomposition theorem）提供了一种数学上严谨的方法，将这两种效应[解耦](@entry_id:160890)。任何一个可逆的[二阶张量](@entry_id:199780) $\boldsymbol{F}$ (满足 $\det\boldsymbol{F} > 0$) 都可以唯一地分解为两种形式：

1.  **右极分解**: $\boldsymbol{F} = \boldsymbol{R}\boldsymbol{U}$
2.  **左极分解**: $\boldsymbol{F} = \boldsymbol{V}\boldsymbol{R}$

其中：
-   $\boldsymbol{R}$ 是一个**[旋转张量](@entry_id:191990)**（即纯正交张量，$\boldsymbol{R}^T\boldsymbol{R} = \boldsymbol{I}$ 且 $\det\boldsymbol{R}=1$）。它描述了物质邻域的[刚体](@entry_id:1131033)旋转。
-   $\boldsymbol{U}$ 是**右[拉伸张量](@entry_id:193200)**（right stretch tensor），它是一个[对称正定](@entry_id:145886)张量（$\boldsymbol{U}^T=\boldsymbol{U}$ 且其特征值均为正）。
-   $\boldsymbol{V}$ 是**左[拉伸张量](@entry_id:193200)**（left stretch tensor），它也是一个对称正定张量（$\boldsymbol{V}^T=\boldsymbol{V}$）。

右极分解 $\boldsymbol{F} = \boldsymbol{R}\boldsymbol{U}$ 的物理解释是：变形过程可以看作是先对物质进行纯拉伸（由 $\boldsymbol{U}$ 描述），然后再进行[刚体](@entry_id:1131033)旋转（由 $\boldsymbol{R}$ 描述） 。左极分解 $\boldsymbol{F} = \boldsymbol{V}\boldsymbol{R}$ 则解释为：先进行[刚体](@entry_id:1131033)旋转，然后再进行纯拉伸。

[拉伸张量](@entry_id:193200) $\boldsymbol{U}$ 和 $\boldsymbol{V}$与前面定义的柯西-格林张量密切相关。我们可以证明：

$$
\boldsymbol{U} = \sqrt{\boldsymbol{C}} = \sqrt{\boldsymbol{F}^T \boldsymbol{F}}
$$
$$
\boldsymbol{V} = \sqrt{\boldsymbol{B}} = \sqrt{\boldsymbol{F} \boldsymbol{F}^T}
$$

其中 $\boldsymbol{B} = \boldsymbol{F}\boldsymbol{F}^T$ 被称为**左柯西-格林变形张量**或**[芬格张量](@entry_id:1124965)**（Finger tensor）。$\boldsymbol{U}$ 和 $\boldsymbol{V}$ 通过[旋转张量](@entry_id:191990) $\boldsymbol{R}$ 联系在一起：$\boldsymbol{V} = \boldsymbol{R}\boldsymbol{U}\boldsymbol{R}^T$。

$\boldsymbol{U}$ 和 $\boldsymbol{V}$ 共享相同的特征值，这些特征值被称为**主拉伸**（principal stretches），记为 $\lambda_1, \lambda_2, \lambda_3$。它们量化了变形在三个相互正交方向上的伸长或缩短程度。然而，它们的[特征向量](@entry_id:151813)不同：
-   $\boldsymbol{U}$ 的[特征向量](@entry_id:151813) $\{\boldsymbol{e}_i\}$ 定义了参考构型中的**主拉伸方向**。
-   $\boldsymbol{V}$ 的[特征向量](@entry_id:151813) $\{\boldsymbol{n}_i\}$ 定义了当前构型中的**主拉伸方向**。

这两个[主方向](@entry_id:276187)集通过旋转 $\boldsymbol{R}$ 相关联，即 $\boldsymbol{n}_i = \boldsymbol{R}\boldsymbol{e}_i$ 。这一分解对于理解[各向异性材料](@entry_id:184874)（如复合材料或生物组织）的力学行为至关重要，因为材料的响应通常取决于拉伸相对于其内部微观结构（如纤维方向）的方向。

### 变形率：[欧拉描述](@entry_id:264722)

到目前为止，我们的讨论主要基于参考构型（[拉格朗日描述](@entry_id:1127015)）。在流体力学或涉及[大变形](@entry_id:167243)的固体力学中，采用**[欧拉描述](@entry_id:264722)**（Eulerian description）通常更为方便，即所有物理量都表示为当前空间位置 $\boldsymbol{x}$ 和时间 $t$ 的函数。

在[欧拉框架](@entry_id:749109)中，我们关注的是**速度场** $\boldsymbol{v}(\boldsymbol{x}, t)$。**[空间速度梯度](@entry_id:187198)** $\boldsymbol{L}$ 定义为速度场 $\boldsymbol{v}$ 对当前坐标 $\boldsymbol{x}$ 的梯度：

$$
\boldsymbol{L}(\boldsymbol{x}, t) = \nabla_{\boldsymbol{x}} \boldsymbol{v}(\boldsymbol{x}, t)
$$

其分量为 $L_{ij} = \partial v_i / \partial x_j$。速度梯度 $\boldsymbol{L}$ 与变形梯度 $\boldsymbol{F}$ 的时间导数之间存在一个关键关系：$\dot{\boldsymbol{F}} = \boldsymbol{L}\boldsymbol{F}$。

与变形梯度 $\boldsymbol{F}$ 类似，$\boldsymbol{L}$ 也包含了变形速率和旋转速率的信息。我们可以将其分解为一个对称[部分和](@entry_id:162077)一个反对称部分：

$$
\boldsymbol{L} = \boldsymbol{D} + \boldsymbol{W}
$$

其中：
-   $\boldsymbol{D} = \frac{1}{2}(\boldsymbol{L} + \boldsymbol{L}^T)$ 是**变形率张量**（rate of deformation tensor）。
-   $\boldsymbol{W} = \frac{1}{2}(\boldsymbol{L} - \boldsymbol{L}^T)$ 是**[自旋张量](@entry_id:187346)**（spin tensor）。

$\boldsymbol{D}$ 描述了物质微元的瞬时拉伸和[剪切变形](@entry_id:170920)速率，而 $\boldsymbol{W}$ 描述了其瞬时[刚体](@entry_id:1131033)旋转速率。一个物质纤维的长度 $\ell$ 的变化率完全由 $\boldsymbol{D}$ 决定。如果 $\boldsymbol{n}$ 是该纤维在当前构型中的单位[方向向量](@entry_id:169562)，那么其**轴向拉伸率**为 ：

$$
\frac{1}{\ell}\frac{d\ell}{dt} = \boldsymbol{n} \cdot \boldsymbol{D} \boldsymbol{n}
$$

反对称的[自旋张量](@entry_id:187346) $\boldsymbol{W}$ 对长度变化率没有贡献，因为对于任何向量 $\boldsymbol{n}$，$\boldsymbol{n} \cdot \boldsymbol{W} \boldsymbol{n} = 0$。同样，两个物质纤维之间夹角的变化率也仅取决于 $\boldsymbol{D}$。

### 高级主题

#### 客观性与标架无关性

物理定律和材料[本构关系](@entry_id:186508)不应依赖于观测者。这一基本原理被称为**[标架无关性原理](@entry_id:200995)**（principle of frame-indifference）或**[物质客观性原理](@entry_id:191727)**（principle of material objectivity）。一个“观测者”的改变可以通过一个时间依赖的刚体运动来描述，即 $\boldsymbol{x}^* = \boldsymbol{c}(t) + \boldsymbol{Q}(t)\boldsymbol{x}$，其中 $\boldsymbol{Q}(t)$ 是一个旋转。

一个张量（如应力 $\boldsymbol{\sigma}$ 或变形率 $\boldsymbol{D}$）被称为**客观的**，如果它在观测者变换下遵循标准的[张量变换法则](@entry_id:185176)，例如对于[二阶张量](@entry_id:199780) $\boldsymbol{A}$，其变换为 $\boldsymbol{A}^* = \boldsymbol{Q}\boldsymbol{A}\boldsymbol{Q}^T$。

通过推导，可以证明变形率张量 $\boldsymbol{D}$ 是客观的，即 $\boldsymbol{D}^* = \boldsymbol{Q}\boldsymbol{D}\boldsymbol{Q}^T$。然而，[空间速度梯度](@entry_id:187198) $\boldsymbol{L}$ 和[自旋张量](@entry_id:187346) $\boldsymbol{W}$ 都不是客观的 。它们的变换规律包含一个额外的项，该项与观测者自身的旋转角速度有关：

$$
\boldsymbol{L}^* = \boldsymbol{Q}\boldsymbol{L}\boldsymbol{Q}^T + \dot{\boldsymbol{Q}}\boldsymbol{Q}^T
$$
$$
\boldsymbol{W}^* = \boldsymbol{Q}\boldsymbol{W}\boldsymbol{Q}^T + \dot{\boldsymbol{Q}}\boldsymbol{Q}^T
$$

$\boldsymbol{D}$ 的客观性是其在建立本构关系中作为变形度量的核心作用的基础。材料如何响应变形（由 $\boldsymbol{D}$ 描述）不应取决于我们如何旋转我们的坐标系。这也引出了在率形式本构模型（hypoelasticity）中需要使用**[客观应力率](@entry_id:199282)**的问题。Cauchy应力的简单[物质时间导数](@entry_id:190892) $\dot{\boldsymbol{\sigma}}$ 并不是客观的，在纯[刚体](@entry_id:1131033)旋转下（此时 $\boldsymbol{D}=\boldsymbol{0}$），$\dot{\boldsymbol{\sigma}}$ 仍不为零。为了修正这一点，需要引入包含[自旋张量](@entry_id:187346) $\boldsymbol{W}$ 的**协同旋转导数**，如 [Jaumann 率](@entry_id:185572) $\boldsymbol{\sigma}^{\nabla J} = \dot{\boldsymbol{\sigma}} - \boldsymbol{W}\boldsymbol{\sigma} + \boldsymbol{\sigma}\boldsymbol{W}$，它是一个客观的应力率 。

#### [不可压缩性](@entry_id:274914)

如前所述，[不可压缩材料](@entry_id:159741)的特征是其体积在变形过程中保持不变，即 $J = \det\boldsymbol{F} \equiv 1$ （或等于初始值 $J_0$）。为了理解这对[应变率](@entry_id:154778)施加了何种约束，我们考察 $J$ 的时间导数。可以证明一个关键关系 ：

$$
\dot{J} = J \operatorname{tr}(\boldsymbol{L})
$$

其中 $\operatorname{tr}(\boldsymbol{L})$ 是[空间速度梯度](@entry_id:187198)的迹。如果体积守恒，则 $\dot{J}=0$，这意味着 $\operatorname{tr}(\boldsymbol{L})=0$。反之，如果 $\operatorname{tr}(\boldsymbol{L})=0$，则 $\dot{J}=0$，[体积保持](@entry_id:141001)恒定。因此，**不可压缩运动的运动学约束是[空间速度梯度](@entry_id:187198)为无迹的**。

由于任何[反对称张量](@entry_id:199349)（如 $\boldsymbol{W}$）的迹都为零，我们有 $\operatorname{tr}(\boldsymbol{L}) = \operatorname{tr}(\boldsymbol{D} + \boldsymbol{W}) = \operatorname{tr}(\boldsymbol{D})$。因此，[不可压缩性](@entry_id:274914)条件等价于要求变形率张量 $\boldsymbol{D}$ 是无迹的，即 $\operatorname{tr}(\boldsymbol{D})=0$。

在[数值模拟](@entry_id:146043)中，精确地保持[不可压缩性约束](@entry_id:750592)是一个挑战。简单的[数值积分](@entry_id:136578)格式，如[显式欧拉法](@entry_id:1124769) $\boldsymbol{F}_{n+1} = (\boldsymbol{I} + \Delta t \boldsymbol{L}_n)\boldsymbol{F}_n$，即使在 $\operatorname{tr}(\boldsymbol{L}_n)=0$ 的条件下，也无法精确保持[体积守恒](@entry_id:276587)（即 $\det \boldsymbol{F}_{n+1} \neq \det \boldsymbol{F}_n$）。而基于矩阵指数的更新格式 $\boldsymbol{F}_{n+1} = \exp(\Delta t \boldsymbol{L}_n)\boldsymbol{F}_n$ 则可以精确地满足这一条件，因为 $\det(\exp(\boldsymbol{A})) = \exp(\operatorname{tr}(\boldsymbol{A}))$，当 $\operatorname{tr}(\boldsymbol{L}_n)=0$ 时，该更新的行列式为1 。

#### 相容性

我们已经将变形梯度 $\boldsymbol{F}$ 定义为运动 $\boldsymbol{\varphi}$ 的梯度。现在我们反过来问一个问题：给定一个[二阶张量](@entry_id:199780)场 $\boldsymbol{F}(\boldsymbol{X})$，它是否总是对应某个光滑的、单值的运动场 $\boldsymbol{\varphi}(\boldsymbol{X})$？答案是否定的。

为了使 $\boldsymbol{F}$ 成为一个梯度的场，即 $\boldsymbol{F} = \nabla_X \boldsymbol{\varphi}$，它必须满足一定的**[相容性条件](@entry_id:637057)**（compatibility condition）。在数学上，一个向量场是某个标量[势的梯度](@entry_id:268447)的充要条件是该向量场的旋度为零（在单连通域上）。将此思想逐行应用于张量 $\boldsymbol{F}$，我们要求 $\boldsymbol{F}$ 的每一行都必须是无旋的 。这个条件可以简洁地写成：

$$
\operatorname{Curl} \boldsymbol{F} = \boldsymbol{0}
$$

其中 $\operatorname{Curl}$ 是逐行作用的[旋度算子](@entry_id:184984)。

这个条件的几何意义是，沿着参考构型中的任何一条闭合回路 $C$ 对 $\boldsymbol{F}$ 进行[线积分](@entry_id:141417)，结果必须为[零向量](@entry_id:156189)：

$$
\oint_C \boldsymbol{F} \, d\boldsymbol{X} = \boldsymbol{0}
$$

如果这个条件不满足，那么当我们将物[质点](@entry_id:186768)沿着回路 $C$ 积分变形后，它们将无法回到起始点，从而在材料中产生一个“缝隙”或“重叠”。这个积分得到的非[零向量](@entry_id:156189) $\boldsymbol{b} = \oint_C \boldsymbol{F} \, d\boldsymbol{X}$ 被称为**[伯格斯矢量](@entry_id:160637)**（Burgers vector），它量化了这种不相容性。在晶体材料中，$\operatorname{Curl} \boldsymbol{F} \neq \boldsymbol{0}$ 的物理根源是**位错**（dislocations）的存在，而[伯格斯矢量](@entry_id:160637)正是表征位错强度的经典工具 。因此，[相容性条件](@entry_id:637057)将宏观连续介质的运动学与[材料微观结构](@entry_id:198422)中的缺陷理论联系起来。