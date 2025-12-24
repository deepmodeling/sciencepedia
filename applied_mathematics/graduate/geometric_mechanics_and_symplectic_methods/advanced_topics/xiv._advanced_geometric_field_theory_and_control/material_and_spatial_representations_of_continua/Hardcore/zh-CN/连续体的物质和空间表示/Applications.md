## 应用与交叉学科联系

在前几章中，我们建立了描述连续介质运动的物质（拉格朗日）和空间（欧拉）表示法的基础。这些看似抽象的数学框架并非仅仅是形式上的练习，它们是现代科学与工程中用以构建、分析和求解真实世界问题的基石。本章旨在揭示这些核心原理在不同学科背景下的应用，展示它们如何被用于解决从材料科学、[流体动力](@entry_id:750449)学到生物物理学和[地球物理学](@entry_id:147342)的各种前沿问题。我们将通过一系列具体的应用实例，探索物质和空间视角如何为理解复杂现象提供深刻的洞察力，并成为连接不同知识领域的桥梁。我们的目标不是重复介绍基本概念，而是演示这些概念的实用性、扩展性及其在交叉学科中的整合。

### [可变形体](@entry_id:1123496)与流体的运动学

连续介质的运动学本身就蕴含着丰富的几何内容，而物质和[空间表示](@entry_id:1132051)法的转换为我们分析这些内容提供了强大的工具。

#### 边界、面积微元与通量的变换

在许多物理问题中，我们关心的是跨越边界的[输运过程](@entry_id:177992)，例如热量、质量或动量的通量。这些过程通常通过在空间构型中的面积分来描述。然而，边界本身是随物质运动的。因此，建立物质边界与空间边界上积分量之间的关系至关重要。

考虑一个物质体 $\mathcal{B}$ 的边界 $\partial\mathcal{B}$，其单位外法向量为 $\boldsymbol{N}$。在运动 $\boldsymbol{\varphi}_t$ 下，它被映射为空间边界 $\partial\Omega_t = \boldsymbol{\varphi}_t(\partial\mathcal{B})$，其单位外法向量为 $\boldsymbol{n}$。物质坐标下的一个[有向面积](@entry_id:169588)微元 $\boldsymbol{N}\,dS_0$ 与其在空间坐标下的像 $\boldsymbol{n}\,dS$ 之间的关系由著名的 **[南森公式](@entry_id:195566)（Nanson's formula）** 给出：
$$
\boldsymbol{n}\,dS = J \boldsymbol{F}^{-\mathsf{T}} \boldsymbol{N}\,dS_0
$$
其中 $\boldsymbol{F}$ 是变形梯度，$J = \det \boldsymbol{F}$ 是其雅可比行列式。这个公式是联系两个构型中[面积分](@entry_id:275394)的关键。例如，对于任意一个空间矢量场 $\boldsymbol{w}(\boldsymbol{x},t)$，其通过空间边界 $\partial\Omega_t$ 的通量可以被转换到对固定物质边界 $\partial\mathcal{B}$ 的积分：
$$
\int_{\partial\Omega_t} \boldsymbol{w} \cdot \boldsymbol{n} \,dS = \int_{\partial\mathcal{B}} \boldsymbol{w}(\boldsymbol{\varphi}_t(\boldsymbol{X}),t) \cdot (J \boldsymbol{F}^{-\mathsf{T}} \boldsymbol{N}) \,dS_0 = \int_{\partial\mathcal{B}} (J \boldsymbol{F}^{-1} \boldsymbol{w}(\boldsymbol{\varphi}_t(\boldsymbol{X}),t)) \cdot \boldsymbol{N} \,dS_0
$$
这个变换在推导[守恒律的积分形式](@entry_id:174909)和在有限元方法中处理边界条件时至关重要。例如，它使得在[拉格朗日框架](@entry_id:751113)下施加空间构型中的[压力边界条件](@entry_id:753712)成为可能。此外，如果物质边界上的所有点的物质速度均为零，即 $\boldsymbol{V}(\boldsymbol{X},t) = \boldsymbol{0}$ 对于所有 $\boldsymbol{X} \in \partial\mathcal{B}$，那么空间边界的位置将不随时间改变，即 $\partial\Omega_t$ 是固定的。这为模拟具有固定边界的流体问题（如[管道流](@entry_id:189531)）提供了理论依据。

#### 运动学场：涡度与环量

流体动力学中的关键概念，如涡度（vorticity）和环量（circulation），在物质和[空间表示](@entry_id:1132051)下有着不同的但内在联系的形式。空间涡度场定义为[空间速度](@entry_id:190294)场 $\boldsymbol{v}$ 的旋度，$\boldsymbol{\omega} = \nabla \times \boldsymbol{v}$。它描述了流体微元的瞬时转动。另一方面，环量是沿一个闭合回路的速度[线积分](@entry_id:141417)，$\Gamma(t) = \oint_{\gamma_t} \boldsymbol{v} \cdot d\boldsymbol{x}$，其中 $\gamma_t$ 是一条随流体运动的物质回路（advected loop）。

[开尔文环量定理](@entry_id:139984)（Kelvin's circulation theorem）指出，在理想正压流体中，物质回路的环量是守恒的。该定理的证明和理解深刻地依赖于物质和空间描述之间的转换。利用微分形式的语言，速度场可以表示为一个[1-形式](@entry_id:270392) $\alpha = \boldsymbol{v} \cdot d\boldsymbol{x}$。环量就是 $\oint_{\gamma_t} \alpha$。根据[斯托克斯定理](@entry_id:264534)和[微分形式](@entry_id:146747)的回拉（pullback）运算性质，这个积分等价于在初始构型中对固定的回路 $\gamma_0$ 的积分：
$$
\oint_{\gamma_t} \alpha = \oint_{\boldsymbol{\varphi}_t(\gamma_0)} \alpha = \oint_{\gamma_0} \boldsymbol{\varphi}_t^*(\alpha)
$$
其中 $\boldsymbol{\varphi}_t^*(\alpha)$ 是将[空间速度](@entry_id:190294)[1-形式](@entry_id:270392) $\alpha$ 拉回到物质构型的结果。在笛卡尔坐标下，这可以具体写为 $\oint_{\gamma_0} (\boldsymbol{F}^\mathsf{T} \boldsymbol{v}(\boldsymbol{\varphi}_t(\boldsymbol{X}),t)) \cdot d\boldsymbol{X}$。这个表达式定义了物质环量。

同样，空间涡度[2-形式](@entry_id:188008) $\varpi = d\alpha$ (在三维空间中对应于矢量场 $\boldsymbol{\omega}$)可以通过回拉操作转换成物质涡度[2-形式](@entry_id:188008) $\varpi_0 = \boldsymbol{\varphi}_t^*(\varpi)$。由于[外微分](@entry_id:161900)与回拉运算可交换 ($d\boldsymbol{\varphi}_t^* = \boldsymbol{\varphi}_t^*d$)，我们有 $\varpi_0 = d(\boldsymbol{\varphi}_t^*\alpha)$。物质涡度矢量场 $\boldsymbol{\Omega}$ 与空间涡度矢量场 $\boldsymbol{\omega}$ 的关系由[皮奥拉变换](@entry_id:163790)（Piola transform）给出：$\boldsymbol{\Omega} = J \boldsymbol{F}^{-1} \boldsymbol{\omega}$。这一关系保证了物质曲面的涡通量守恒，即 $\int_{S_t} \boldsymbol{\omega} \cdot \boldsymbol{n}\,dS = \int_{S_0} \boldsymbol{\Omega} \cdot \boldsymbol{N}\,dS_0$。这些变换是[流体动力](@entry_id:750449)学中[涡动力学](@entry_id:145644)研究的基础。

### 材料的[本构模型](@entry_id:174726)

[本构关系](@entry_id:186508)描述了材料如何响应变形，是连接运动学与动力学的桥梁。物质和[空间表示](@entry_id:1132051)法在本构理论中扮演着核心角色，特别是在处理[大变形](@entry_id:167243)问题时。

#### 变形的分解与[位移梯度](@entry_id:165352)

变形梯度 $\boldsymbol{F}$ 捕捉了从物质构型到空间构型的所有局部变形信息。对于有限变形分析，理解 $\boldsymbol{F}$ 与位移场 $\boldsymbol{u}(\boldsymbol{X}) = \boldsymbol{x}(\boldsymbol{X}) - \boldsymbol{X}$ 的关系至关重要。这是一个精确的运动学关系：
$$
\boldsymbol{F} = \nabla_{\boldsymbol{X}} \boldsymbol{x} = \nabla_{\boldsymbol{X}} (\boldsymbol{X} + \boldsymbol{u}) = \boldsymbol{I} + \nabla_{\boldsymbol{X}} \boldsymbol{u}
$$
这个关系是精确的，对任意大小的变形和转动都成立，并非小变形近似。它构成了[计算力学](@entry_id:174464)中“全拉格朗日（Total Lagrangian）”有限元法的理论基础，在这种方法中，[位移场](@entry_id:141476)是基本未知量，而所有运动学量（包括 $\boldsymbol{F}$）都由[位移梯度](@entry_id:165352)导出。

为了更深入地理解变形，极分解（polar decomposition）定理提供了一个强大的工具。它将变形梯度唯一地分解为一个纯拉伸和一个[刚体转动](@entry_id:191086)：
$$
\boldsymbol{F} = \boldsymbol{R}\boldsymbol{U}
$$
这里，$\boldsymbol{U}$ 是[对称正定](@entry_id:145886)的右[拉伸张量](@entry_id:193200)，它作用于物质构型，描述了材料微元的纯变形（拉伸或压缩）；$\boldsymbol{R}$ 是一个[旋转张量](@entry_id:191990)（$\boldsymbol{R} \in \mathrm{SO}(3)$），描述了变形后的材料微元发生的[刚体转动](@entry_id:191086)。$\boldsymbol{U}$ 完全由右柯西-格林变形张量 $\boldsymbol{C} = \boldsymbol{F}^\mathsf{T}\boldsymbol{F}$ 决定，即 $\boldsymbol{U} = \sqrt{\boldsymbol{C}}$。由于 $\boldsymbol{C}$ 是在物质构型上定义的，$\boldsymbol{U}$ 也是一个物质张量。这种分解清晰地揭示了变形的物理内涵，即将复杂的变形过程概念性地分为两步：先在物质构型中进行拉伸，然后再进[行空间](@entry_id:148831)中的[刚体](@entry_id:1131033)旋转。

#### [客观性原理](@entry_id:185412)与[材料对称性](@entry_id:190289)

[本构定律](@entry_id:178936)必须满足**标架无关性（material frame indifference）**或称**客观性（objectivity）**原理。该原理指出，本构关系不能依赖于观察者。一个观察者的变换等价于在当前的空间构型上叠加一个[刚体运动](@entry_id:144691)。这意味着，在变换 $\boldsymbol{x} \to \boldsymbol{Q}\boldsymbol{x} + \boldsymbol{c}$（其中 $\boldsymbol{Q}$ 是旋转矩阵）下，变形梯度变为 $\boldsymbol{F} \to \boldsymbol{Q}\boldsymbol{F}$。[应变能密度函数](@entry_id:755490) $W$ 必须在该变换下不变，即 $W(\boldsymbol{Q}\boldsymbol{F}) = W(\boldsymbol{F})$。

满足这一要求的唯一途径是让 $W$ 仅通过[右柯西-格林张量](@entry_id:174156) $\boldsymbol{C} = \boldsymbol{F}^\mathsf{T}\boldsymbol{F}$ 依赖于 $\boldsymbol{F}$，因为 $\boldsymbol{C}$ 在这种变换下是不变的：$(\boldsymbol{Q}\boldsymbol{F})^\mathsf{T}(\boldsymbol{Q}\boldsymbol{F}) = \boldsymbol{F}^\mathsf{T}\boldsymbol{Q}^\mathsf{T}\boldsymbol{Q}\boldsymbol{F} = \boldsymbol{F}^\mathsf{T}\boldsymbol{F} = \boldsymbol{C}$。因此，[客观性原理](@entry_id:185412)强制要求[应变能函数](@entry_id:178435)具有简约形式 $W = \hat{W}(\boldsymbol{C})$。这是现代[连续介质力学](@entry_id:155125)的基石之一，而物质表示法（通过张量 $\boldsymbol{C}$）是系统地满足该原理的自然途径。由此，[第二皮奥拉-基尔霍夫应力](@entry_id:173163)张量 $\boldsymbol{S}$ 可由 $W$ 对 $\boldsymbol{C}$ 求导得出：$\boldsymbol{S} = 2 \frac{\partial \hat{W}}{\partial \boldsymbol{C}}$。

与普适的[客观性原理](@entry_id:185412)不同，**[材料对称性](@entry_id:190289)（material symmetry）**是材料的内在属性。它描述了在参考构型中，何种[旋转操作](@entry_id:140575)不会改变材料的响应。例如，如果材料是**各向同性（isotropic）**的，那么它在所有方向上都具有相同的性质，其响应在参考构型的任意旋转 $\boldsymbol{Q}_m \in \mathrm{SO}(3)$ 下都不变。这要求 $W(\boldsymbol{F}\boldsymbol{Q}_m) = W(\boldsymbol{F})$。对于已经满足客观性的 $W=\hat{W}(\boldsymbol{C})$，这进一步要求 $\hat{W}(\boldsymbol{Q}_m^\mathsf{T} \boldsymbol{C} \boldsymbol{Q}_m) = \hat{W}(\boldsymbol{C})$。对于[各向同性材料](@entry_id:170678)，这意味着 $\hat{W}$ 只能是 $\boldsymbol{C}$ 的[主不变量](@entry_id:193522)的函数，即 $W = W(I_1, I_2, I_3)$。

然而，许多真实材料，尤其是生物组织，是**各向异性（anisotropic）**的。例如，软组织中的胶原纤维赋予了材料一个或多个优先方向。对于一个具有单一优先方向 $\boldsymbol{a}_0$（在参考构型中定义）的横观[各向同性材料](@entry_id:170678)，其对称性群只是绕 $\boldsymbol{a}_0$ 轴的[旋转群](@entry_id:204412)，是 $\mathrm{SO}(3)$ 的一个子群。为了描述这种方向依赖性，应变能函数必须显式地依赖于 $\boldsymbol{a}_0$。这通过引入额外的混合不变量来实现，例如 $I_4 = \boldsymbol{a}_0 \cdot \boldsymbol{C} \boldsymbol{a}_0$ 和 $I_5 = \boldsymbol{a}_0 \cdot \boldsymbol{C}^2 \boldsymbol{a}_0$。$I_4$ 直接度量了沿纤维方向的拉伸的平方。仅依赖于 $I_1, I_2, I_3$ 的模型无法区分沿纤维方向和垂直于纤维方向的拉伸，因此无法正确描述各向异性行为。因此，物质表示法对于精确建模复杂材料（如复合材料和生物组织）的各向异性响应至关重要。 

各向同性假设有一个重要的力学推论：在这种材料中，柯西应力张量 $\boldsymbol{\sigma}$ 与[左柯西-格林张量](@entry_id:186163) $\boldsymbol{B} = \boldsymbol{F}\boldsymbol{F}^\mathsf{T}$ 是**共轴的（coaxial）**，即它们拥有相同的[主方向](@entry_id:276187)。这是因为对于各向同性[超弹性材料](@entry_id:190241)，柯西应力可以表示为 $\boldsymbol{B}$ 的张量多项式（$\boldsymbol{\sigma} = \alpha_0 \boldsymbol{I} + \alpha_1 \boldsymbol{B} + \alpha_2 \boldsymbol{B}^{-1}$）。一个张量与其自身的任何多项式函数都可交换，而两个可交换的[对称张量](@entry_id:148092)必然共轴。这意味着在[各向同性材料](@entry_id:170678)中，[主应力方向](@entry_id:753737)总是与主拉伸方向对齐。

### 守恒律与[变分原理](@entry_id:198028)

物质和[空间表示](@entry_id:1132051)法是表述基本物理守恒律的两种互补语言。

#### 质量守恒：连续性方程

质量守恒是所有连续介质模型的基础。在物质（拉格朗日）描述中，其表述极为简单：一个物质体（control mass），即一组固定的物质粒子，其总质量不随时间改变。
$$
\frac{d}{dt} \int_{\mathcal{B}_t} \rho(\boldsymbol{x}, t) \,dV = 0
$$
其中 $\mathcal{B}_t$ 是随流体运动和变形的物质体积。

然而，在大多数应用（特别是流体力学和地球物理学）中，我们更关心在一个固定的空间区域或控制体积（control volume）$\mathcal{V}$ 内物理量的变化。为了从拉格朗日描述得到[欧拉描述](@entry_id:264722)，我们需要应用雷诺输运定理（Reynolds Transport Theorem）。该定理将[随体导数](@entry_id:204621)与[局部时](@entry_id:194383)间导数和通过边界的对流通量联系起来。将[质量守恒定律](@entry_id:147377)应用于一个固定的控制体积 $\mathcal{V}$，可以得到其积分形式：
$$
\frac{d}{dt} \int_{\mathcal{V}} \rho \,dV + \oint_{\partial\mathcal{V}} \rho \boldsymbol{v} \cdot \boldsymbol{n} \,dA = 0
$$
这个方程的物理意义是：固定体积内质量的增加率等于通过边界的净[质量流](@entry_id:143424)入率。再利用[高斯散度定理](@entry_id:188065)，我们可以得到其局部（[微分](@entry_id:158422)）形式，即著名的**[连续性方程](@entry_id:195013)（continuity equation）**：
$$
\frac{\partial \rho}{\partial t} + \nabla \cdot (\rho \boldsymbol{v}) = 0
$$
这个方程也可以写成物质导数的形式：$\frac{D\rho}{Dt} + \rho (\nabla \cdot \boldsymbol{v}) = 0$，它描述了跟随一个流体质点，其密度的变化率等于体积的相对膨胀率（由速度场的散度度量）的负值。从一个简单的拉格朗日陈述到一个功能强大的欧拉[偏微分](@entry_id:194612)方程的推导，是物质-空间变换思想威力的完美体现。

#### 变分原理与不可压缩性

许多物理系统，特别是弹性力学，可以通过[变分原理](@entry_id:198028)来描述，即系统的运动路径使某个作用量（action）泛函取极值。对于[超弹性](@entry_id:159356)体，作用量通常由动能和应变能之差的积分给出。在物质构型中，其[拉格朗日量](@entry_id:174593)泛函可以写为：
$$
S[\boldsymbol{\varphi}] = \int_{t_0}^{t_1} \int_{\mathcal{B}} \left( \frac{1}{2} \rho_0 |\partial_t \boldsymbol{\varphi}|^2 - W(\boldsymbol{F}) \right) \,dX \,dt
$$
许多流体和类橡胶材料在很大程度上是**不可压缩的（incompressible）**，这一约束在运动学上表现为体积不变，即 $J = \det \boldsymbol{F} = 1$。为了在变分原理中引入这个约束，我们使用[拉格朗日乘子法](@entry_id:176596)。我们将约束项 $\Lambda(J-1)$ 添加到[拉格朗日量密度](@entry_id:156695)中，其中 $\Lambda(\boldsymbol{X}, t)$ 是一个[拉格朗日乘子](@entry_id:142696)场。

通过对修正后的作用量进行变分，我们发现这个约束项对[第一皮奥拉-基尔霍夫应力](@entry_id:163971)张量 $\boldsymbol{P}$ 产生了一个额外的贡献：$\boldsymbol{P}^{\mathrm{inc}} = - \Lambda \, \mathrm{Cof}(\boldsymbol{F})$。更有趣的是，当我们把这个应力项推回到空间构型中以获得柯西应力时，它变成了一个纯各向同性的压力项：
$$
\boldsymbol{\sigma}^{\mathrm{inc}} = J^{-1} \boldsymbol{P}^{\mathrm{inc}} \boldsymbol{F}^\mathsf{T} = - \Lambda \boldsymbol{I} = -p \boldsymbol{I}
$$
这表明，拉格朗日乘子场 $\Lambda$ 在物理上可以被解释为维持不可压缩性所需的[热力学压力](@entry_id:1133073) $p$。更准确地说，空间压[力场](@entry_id:147325) $p(\boldsymbol{x},t)$ 就是拉格朗日乘子场 $\Lambda(\boldsymbol{X},t)$ 在空间构型中的表示，即 $p = \Lambda \circ \boldsymbol{\varphi}^{-1}$。这种方法优雅地将一个纯运动学约束转化为一个动力学量（压力），是[约束力学](@entry_id:1122939)系统建模的典范。

### 交叉学科中的高等建模应用

物质和[空间表示](@entry_id:1132051)法的思想也渗透到了许多特定领域的先进[计算模型](@entry_id:637456)中。

#### [移动界面](@entry_id:141467)的计算方法

在地球物理学、材料科学和多相流中，模拟[移动界面](@entry_id:141467)（如熔体/固[相界面](@entry_id:172947)、不同流体间的界面）的演化是一个巨大的挑战，特别是当界面拓扑结构发生复杂变化（如合并和断裂）时。对此，存在两种主要的计算策略。

**前缘追踪（Front-tracking）**方法是一种[拉格朗日方法](@entry_id:142825)，它通过一组离散的标记点或网格来显式地表示界面，并根据当地的速度场来移动这些点。这种方法的优点是界面位置精确，但其致命弱点在于处理[拓扑变化](@entry_id:136654)。当界面需要合并或断裂时，必须执行复杂且脆弱的网格重构或“外科手术”算法。

相比之下，**前缘捕捉（Front-capturing）**方法是一种欧拉方法，它在固定的网格上求解一个辅助标量场的演化方程，界面的位置被“捕捉”为该场的某个特征。例如，**水平集方法（Level Set Method）**将界面定义为[水平集](@entry_id:751248)函数 $\phi(\boldsymbol{x},t)$ 的零等值面。通过求解一个简单的对流方程 $\partial_t \phi + \boldsymbol{v} \cdot \nabla \phi = 0$，整个标量场得以演化，而其零[等值面](@entry_id:196027)的拓扑结构可以自然地发生合并或断裂，无需任何特殊处理。**相场方法（Phase Field Method）**是另一种欧拉方法，它用一个在空间上平滑过渡的“序参数”来表示一个具有有限厚度的弥散界面，其演化由一个[能量泛函](@entry_id:170311)（如Cahn-Hilliard或Allen-Cahn能量）驱动。这些欧拉方法在处理复杂[拓扑变化](@entry_id:136654)方面的鲁棒性使其在模拟晶体生长、[多相流](@entry_id:146480)和地球[地幔对流](@entry_id:203493)等问题中极具优势。

#### 生物组织中的各向异性输运

生物组织通常具有高度有序的微观结构，这导致了其宏观物理性质的显著各向异性。[心肌](@entry_id:924326)组织就是一个典型的例子。心肌细胞排列成纤维束，定义了一个[局部坐标系](@entry_id:751394) $\{\boldsymbol{f}, \boldsymbol{s}, \boldsymbol{n}\}$（分别代表纤维方向、板层方向和板层法线方向）。这种结构使得电信号在沿纤维方向的传导速度远快于横向传导速度。

在**双畴模型（bidomain model）**这一描述心脏电生理的标准模型中，细胞内和细胞外空间的电导率被分别建模为两个[二阶张量](@entry_id:199780) $\boldsymbol{\sigma}_i$ 和 $\boldsymbol{\sigma}_e$。由于材料的微观结构，这两个张量都是**[正交各向异性](@entry_id:196967)（orthotropic）**的，它们的主轴与局部的物质坐标系 $\{\boldsymbol{f}, \boldsymbol{s}, \boldsymbol{n}\}$ 对齐。因此，它们可以在这个物质基底下被对角化：
$$
\boldsymbol{\sigma}_k = \sigma_{k,f}\,\boldsymbol{f}\boldsymbol{f}^\mathsf{T} + \sigma_{k,s}\,\boldsymbol{s}\boldsymbol{s}^\mathsf{T} + \sigma_{k,n}\,\boldsymbol{n}\boldsymbol{n}^\mathsf{T} \quad (k \in \{i,e\})
$$
其中 $\sigma_{k,f}, \sigma_{k,s}, \sigma_{k,n}$ 是沿三个[主方向](@entry_id:276187)的电导率标量。这些物质张量描述了组织固有的、与方向相关的属性。在求解电势的[偏微分](@entry_id:194612)方程时，这些在物质框架下定义的张量被用于空间框架下的奥姆定律 $\boldsymbol{J}_k = -\boldsymbol{\sigma}_k \nabla \phi_k$ 中。这完美地展示了如何利用物质坐标系来定义各向异性本构关系，并将其应用于空间描述的物理模型中。此外，当细胞内和细胞外[电导率张量](@entry_id:155827)成比例，即 $\boldsymbol{\sigma}_i(\boldsymbol{x}) = \lambda \boldsymbol{\sigma}_e(\boldsymbol{x})$（其中 $\lambda$ 是一个[空间常数](@entry_id:193491)）时，复杂的双畴模型可以精确地简化为一个更易于求解的**单畴模型（monodomain model）**。

### 几何力学观点：连续统的辛结构

对于追求更深层次理论理解的读者，物质表示法为将[连续介质力学](@entry_id:155125)置于哈密顿力学的优雅框架中提供了自然的舞台。这导致了**几何力学**这一[数学物理](@entry_id:265403)分支的诞生。

在这个观点中，系统的[构型空间](@entry_id:149531)是所有可能的物质到空间嵌入的无限维流形 $Q = \mathrm{Emb}(\mathcal{B}, \mathcal{S})$。相空间则是其**余切丛（cotangent bundle）** $T^*Q$，其上的点由一个构型 $\boldsymbol{\varphi}$ 和一个与之对应的**[动量密度](@entry_id:271360)场** $\boldsymbol{\pi}$ 组成。对于一个具有[拉格朗日量密度](@entry_id:156695) $\mathcal{L}(\boldsymbol{\varphi}, \dot{\boldsymbol{\varphi}})$ 的系统，正则动量密度通过对速度场 $\dot{\boldsymbol{\varphi}}$ 的泛函变分来定义，$\boldsymbol{\pi} = \frac{\partial \mathcal{L}}{\partial \dot{\boldsymbol{\varphi}}}$。例如，对于标准的[超弹性](@entry_id:159356)体，[动量密度](@entry_id:271360)就是物质质量密度与物质速度的乘积，$\boldsymbol{\pi}(\boldsymbol{X},t) = \rho_0(\boldsymbol{X})\dot{\boldsymbol{\varphi}}(\boldsymbol{X},t)$。

在这个无限维相空间上，可以定义一个**正则辛[2-形式](@entry_id:188008)（canonical symplectic 2-form）**，它赋予了相空间一种几何结构，并决定了[哈密顿动力学](@entry_id:156273)。该辛形式可以形式上写为：
$$
\Omega = \int_{\mathcal{B}} d\boldsymbol{\varphi} \wedge d\boldsymbol{\pi} \,dX
$$
这个表达式的严格含义是，对于相空间中 $(\boldsymbol{\varphi}, \boldsymbol{\pi})$ 点的两个切矢量 $(\delta_1\boldsymbol{\varphi}, \delta_1\boldsymbol{\pi})$ 和 $(\delta_2\boldsymbol{\varphi}, \delta_2\boldsymbol{\pi})$，$\Omega$ 的作用为：
$$
\Omega((\delta_1\boldsymbol{\varphi}, \delta_1\boldsymbol{\pi}), (\delta_2\boldsymbol{\varphi}, \delta_2\boldsymbol{\pi})) = \int_{\mathcal{B}} \left( \langle \delta_2\boldsymbol{\pi}, \delta_1\boldsymbol{\varphi} \rangle - \langle \delta_1\boldsymbol{\pi}, \delta_2\boldsymbol{\varphi} \rangle \right) dX
$$
其中 $\langle \cdot, \cdot \rangle$ 表示矢量和[余矢量](@entry_id:157727)之间的自然配对。这个辛结构是守恒的，并且控制着系统的哈密顿演化，完全类似于有限维经典力学中的情况。

对于在时空中定义的场论（如[弹性动力学](@entry_id:175818)），这个思想可以进一步推广到**多[辛形式](@entry_id:165896)（multisymplectic formulation）**。通过**[庞加莱-嘉当形式](@entry_id:1129851)（Poincaré-Cartan form）**，可以定义一个在时空和场的多重喷射丛上的多辛 $(n+2)$-形式 $\Omega_{\mathcal{L}}$。这个形式是闭的（$d\Omega_{\mathcal{L}}=0$），并且它编码了场方程（[欧拉-拉格朗日方程](@entry_id:137827)）。更重要的是，它引出了一个广义的守恒律，即多辛守恒律，$\partial_\mu \omega^\mu = 0$。这为研究[场论](@entry_id:155241)的守恒律和对称性（通过诺特定理的推广）提供了一个强大的几何框架。