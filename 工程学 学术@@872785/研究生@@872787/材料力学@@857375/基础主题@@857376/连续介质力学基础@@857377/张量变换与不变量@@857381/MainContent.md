## 引言
在物理学和工程学中，张量是描述应力、应变和[电磁场](@entry_id:265881)等物理量的通用数学语言。然而，一个基本的科学原则要求，描述自然现象的物理定律其形式不应依赖于我们选择的观察[坐标系](@entry_id:156346)。这一“标架无关性”或“客观性”原理，引出了连续介质力学中的一个核心挑战：如何构建能够客观描述材料行为的[本构模型](@entry_id:174726)？答案的关键在于深入理解张量在不同[坐标系](@entry_id:156346)下的变换规律以及那些在变换中保持不变的量——即[张量不变量](@entry_id:203254)。

本文旨在系统地揭示[张量变换](@entry_id:183453)与[不变量](@entry_id:148850)的理论精髓及其在科学与工程中的深刻应用。在“**原理与机制**”一章中，我们将从[主动与被动变换](@entry_id:175638)的根本区别出发，阐明[标架无关性原理](@entry_id:200995)如何要求我们使用客观的[运动学](@entry_id:173318)量，并深入探讨[主不变量](@entry_id:193522)和[谱分解](@entry_id:173707)等核心数学工具。接下来，“**应用与跨学科联系**”一章将展示这些理论如何在连续介质力学、[材料科学](@entry_id:152226)、广义相对论乃至[量子化学](@entry_id:140193)等领域中，成为解决实际问题的强大武器。最后，“**动手实践**”部分提供了一系列精心设计的练习，帮助读者将理论知识转化为解决问题的实践能力。通过这趟旅程，您将掌握从复杂的、依赖于坐标的分量中提炼出普适物理规律的核心技能。

## 原理与机制

在[连续介质力学](@entry_id:155125)中，物理定律的表达形式不应依赖于观察者的参考标架。这一基本要求，即所谓的**标架无关性**或**[客观性原理](@entry_id:185412)**，是构建有效[本构模型](@entry_id:174726)的基石。张量是描述物理量（如应力、应变）的数学工具，其在不同[坐标系](@entry_id:156346)下的变换规律是理解客观性的核心。本章将系统阐述[张量变换](@entry_id:183453)的基本原理、[不变量](@entry_id:148850)的深刻内涵，以及它们在材料本构理论中的关键作用。

### [张量变换](@entry_id:183453)：主动观点与被动观点

理解[张量变换](@entry_id:183453)的第一步是区分两种互补的观点：**主动变换**和**被动变换**。这两种观点描述了不同的物理或几何情景，但它们在数学上紧密相关。考虑一个三维[欧几里得空间](@entry_id:138052)中的物理矢量 $\boldsymbol{v}^{\sharp}$，以及一个固定的标准正交基 $\mathcal{B} = \{ \boldsymbol{e}_1, \boldsymbol{e}_2, \boldsymbol{e}_3 \}$。该矢量可以表示为其分量列向量 $\boldsymbol{v} \in \mathbb{R}^3$ 与基的线性组合，即 $\boldsymbol{v}^{\sharp} = \sum_{i=1}^{3} v_i \boldsymbol{e}_i$。一个表示空间旋转的正交张量 $\boldsymbol{Q}$（满足 $\boldsymbol{Q}^{\mathsf{T}}\boldsymbol{Q}=\boldsymbol{I}$ 且 $\det \boldsymbol{Q}=+1$）可以作用于这个系统。

在**主动变换**中，我们保持[坐标基](@entry_id:270149) $\mathcal{B}$ 不变，而将物理矢量 $\boldsymbol{v}^{\sharp}$ 旋转到新的矢量 $\boldsymbol{v}^{\sharp\prime} = \mathcal{R}_{\boldsymbol{Q}}(\boldsymbol{v}^{\sharp})$，其中 $\mathcal{R}_{\boldsymbol{Q}}$ 是由 $\boldsymbol{Q}$ 代表的旋转算子。我们想知道新矢量 $\boldsymbol{v}^{\sharp\prime}$ 在*同一个*基 $\mathcal{B}$ 下的分量 $\boldsymbol{v}^{\mathrm{act}}$。根据线性代数的基本原理，算子 $\mathcal{R}_{\boldsymbol{Q}}$ 在基 $\mathcal{B}$ 下的[矩阵表示](@entry_id:146025)就是 $\boldsymbol{Q}$。因此，新分量列向量由矩阵-向量乘法直接给出：
$$
\boldsymbol{v}^{\mathrm{act}} = \boldsymbol{Q} \boldsymbol{v}
$$
这个过程可以想象为将一个物体在固定的实验室坐标系中进行旋转。

相反，在**被动变换**中，物理矢量 $\boldsymbol{v}^{\sharp}$ 保持固定，但我们改变观察它的[坐标基](@entry_id:270149)。我们将基从 $\mathcal{B}$ 变换到一个新的旋转后的基 $\mathcal{B}' = \{ \boldsymbol{e}'_1, \boldsymbol{e}'_2, \boldsymbol{e}'_3 \}$。一个自然的约定是，新[基矢](@entry_id:199546)量是旧[基矢](@entry_id:199546)量在旋转算子 $\mathcal{R}_{\boldsymbol{Q}}$ 作用下的像，即 $\boldsymbol{e}'_j = \mathcal{R}_{\boldsymbol{Q}}(\boldsymbol{e}_j) = \sum_{i=1}^{3} Q_{ij} \boldsymbol{e}_i$。同一个物理矢量 $\boldsymbol{v}^{\sharp}$ 在新旧两个基下的表示必须相等：
$$
\boldsymbol{v}^{\sharp} = \sum_{i=1}^{3} v_i \boldsymbol{e}_i = \sum_{j=1}^{3} v^{\mathrm{pas}}_j \boldsymbol{e}'_j
$$
将 $\boldsymbol{e}'_j$ 的表达式代入并重新组合，我们得到 $\sum_{i=1}^{3} v_i \boldsymbol{e}_i = \sum_{i=1}^{3} (\sum_{j=1}^{3} Q_{ij} v^{\mathrm{pas}}_j) \boldsymbol{e}_i$。通过比较[基矢](@entry_id:199546)量 $\boldsymbol{e}_i$ 的系数，我们发现旧分量 $\boldsymbol{v}$ 与新分量 $\boldsymbol{v}^{\mathrm{pas}}$ 之间的关系是 $\boldsymbol{v} = \boldsymbol{Q} \boldsymbol{v}^{\mathrm{pas}}$。为了求解新分量，我们利用 $\boldsymbol{Q}$ 的正交性，左乘其转置 $\boldsymbol{Q}^{\mathsf{T}}$：
$$
\boldsymbol{v}^{\mathrm{pas}} = \boldsymbol{Q}^{\mathsf{T}} \boldsymbol{v}
$$
这个过程可以想象为同一个物体，但我们从一个旋转过的角度（例如，旋转我们的头）去观察它。

主动变换和被动变换的公式——$\boldsymbol{Q}\boldsymbol{v}$ 与 $\boldsymbol{Q}^{\mathsf{T}}\boldsymbol{v}$——是不同的，这揭示了两者在概念和数学上的明确区别。变换矩阵是 $\boldsymbol{Q}$ 还是其转置 $\boldsymbol{Q}^{\mathsf{T}}$，取决于我们是旋转物体还是[旋转坐标系](@entry_id:170324)。然而，一个重要的共性是，两种变换都保持了矢量的几何属性。由于 $\boldsymbol{Q}$ 和 $\boldsymbol{Q}^{\mathsf{T}}$ 都是正交张量，它们都保持了矢量的欧几里得范数（长度）和两个矢量之间的[内积](@entry_id:158127)（夹角），例如 $(\boldsymbol{Q}\boldsymbol{v})^{\mathsf{T}}(\boldsymbol{Q}\boldsymbol{w}) = \boldsymbol{v}^{\mathsf{T}}\boldsymbol{Q}^{\mathsf{T}}\boldsymbol{Q}\boldsymbol{w} = \boldsymbol{v}^{\mathsf{T}}\boldsymbol{w}$。

对于[二阶张量](@entry_id:199780)，如柯西[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$，其变换法则旨在确保物理关系（如柯西公式 $\boldsymbol{t} = \boldsymbol{\sigma}\boldsymbol{n}$）在所有[坐标系](@entry_id:156346)中都保持形式不变。在被动变换下，法向量分量 $\boldsymbol{n}$ 和牵[引力](@entry_id:175476)矢量分量 $\boldsymbol{t}$ 都遵循 $\boldsymbol{v}' = \boldsymbol{Q}^{\mathsf{T}}\boldsymbol{v}$ 的规则。为了使 $\boldsymbol{t}' = \boldsymbol{\sigma}'\boldsymbol{n}'$ 成立，即 $\boldsymbol{Q}^{\mathsf{T}}\boldsymbol{t} = \boldsymbol{\sigma}'(\boldsymbol{Q}^{\mathsf{T}}\boldsymbol{n})$，可以推导出应力张量的分量必须遵循以下变换法则：
$$
\boldsymbol{\sigma}' = \boldsymbol{Q}^{\mathsf{T}} \boldsymbol{\sigma} \boldsymbol{Q}
$$
在[连续介质力学](@entry_id:155125)中，通常将 $\boldsymbol{Q}$ 定义为从固定空间基到旋转后的新基的[变换矩阵](@entry_id:151616)，这时矢量分量的变换是 $\boldsymbol{v}' = \boldsymbol{Q}\boldsymbol{v}$，而[二阶张量](@entry_id:199780)的变换是 $\boldsymbol{\sigma}' = \boldsymbol{Q}\boldsymbol{\sigma}\boldsymbol{Q}^{\mathsf{T}}$。我们将遵循后一种约定。

### [标架无关性原理](@entry_id:200995)与客观张量

物理定律的客观性要求本构关系不能依赖于观察者。一个观察者（或标架）由其在空间中的位置和定向决定。两个空间观察者通过一个时间相关的刚体运动相关联，其位置关系为 $\boldsymbol{x}^{\star} = \boldsymbol{c}(t) + \boldsymbol{Q}(t)\boldsymbol{x}$，其中 $\boldsymbol{c}(t)$ 是平移，$\boldsymbol{Q}(t)$ 是一个正常正交张量（旋转）。

考虑一个从参考构型 $\mathcal{B}_0$ 到当前构型 $\mathcal{B}$ 的变形，由变形梯度 $\boldsymbol{F}$ 描述。对于一个叠加了刚体运动的观察者，其测量的变形梯度 $\boldsymbol{F}^{\star}$ 会发生变化：
$$
\boldsymbol{F}^{\star} = \frac{\partial \boldsymbol{x}^{\star}}{\partial \boldsymbol{X}} = \boldsymbol{Q} \frac{\partial \boldsymbol{x}}{\partial \boldsymbol{X}} = \boldsymbol{Q}\boldsymbol{F}
$$
由于 $\boldsymbol{F}$ 的值会随着观察者的旋转 $\boldsymbol{Q}$ 而改变，任何直接依赖于 $\boldsymbol{F}$ 的本构关系（例如，[应变能函数](@entry_id:178435) $\Psi(\boldsymbol{F})$）都会因观察者而异，这违反了[客观性原理](@entry_id:185412)。因此，$\boldsymbol{F}$ 本身不是一个**客观**的运动学量度。

为了构建客观的本构模型，我们需要寻找那些在叠加刚体运动下具有特定不变性或协变性的运动学量度。**右柯西-格林变形张量** $\boldsymbol{C}$ 和**左柯西-格林变形张量** $\boldsymbol{B}$ 正是为此而生：
$$
\boldsymbol{C} = \boldsymbol{F}^{\mathsf{T}}\boldsymbol{F}
$$
$$
\boldsymbol{B} = \boldsymbol{F}\boldsymbol{F}^{\mathsf{T}}
$$
让我们考察它们在观察者变换下的行为。对于 $\boldsymbol{C}$：
$$
\boldsymbol{C}^{\star} = (\boldsymbol{F}^{\star})^{\mathsf{T}}\boldsymbol{F}^{\star} = (\boldsymbol{Q}\boldsymbol{F})^{\mathsf{T}}(\boldsymbol{Q}\boldsymbol{F}) = \boldsymbol{F}^{\mathsf{T}}\boldsymbol{Q}^{\mathsf{T}}\boldsymbol{Q}\boldsymbol{F} = \boldsymbol{F}^{\mathsf{T}}\boldsymbol{I}\boldsymbol{F} = \boldsymbol{C}
$$
$\boldsymbol{C}$ 在叠加刚体运动下保持不变。它是一个与参考构型相关的**物质张量**，其测量结果不随空间观察者的旋转而改变。

对于 $\boldsymbol{B}$：
$$
\boldsymbol{B}^{\star} = \boldsymbol{F}^{\star}(\boldsymbol{F}^{\star})^{\mathsf{T}} = (\boldsymbol{Q}\boldsymbol{F})(\boldsymbol{Q}\boldsymbol{F})^{\mathsf{T}} = \boldsymbol{Q}\boldsymbol{F}\boldsymbol{F}^{\mathsf{T}}\boldsymbol{Q}^{\mathsf{T}} = \boldsymbol{Q}\boldsymbol{B}\boldsymbol{Q}^{\mathsf{T}}
$$
$\boldsymbol{B}$ 并不保持不变，但它的变换方式 $\boldsymbol{B}^{\star} = \boldsymbol{Q}\boldsymbol{B}\boldsymbol{Q}^{\mathsf{T}}$ 与一个空间[二阶张量](@entry_id:199780)（如柯西应力）的变换方式完全相同。因此，$\boldsymbol{B}$ 是一个客观的**[空间张量](@entry_id:185799)**。

基于这些变换性质，我们可以定义客观的[应变度量](@entry_id:755495)。**[格林-拉格朗日应变张量](@entry_id:187745)** $E = \frac{1}{2}(\boldsymbol{C} - \boldsymbol{I})$，由于 $\boldsymbol{C}$ 是客观的，$\boldsymbol{E}$ 也是一个客观的物质张量（$\boldsymbol{E}^{\star} = \boldsymbol{E}$）。另一方面，**[欧拉-阿尔曼西应变张量](@entry_id:194948)** $\boldsymbol{e} = \frac{1}{2}(\boldsymbol{I} - \boldsymbol{B}^{-1})$ 是一个客观的[空间张量](@entry_id:185799)（$\boldsymbol{e}^{\star} = \boldsymbol{Q}\boldsymbol{e}\boldsymbol{Q}^{\mathsf{T}}$）。如果一个运动本身就是纯刚体运动（无变形），那么 $\boldsymbol{F}=\boldsymbol{Q}$，可以轻易证明 $\boldsymbol{C}=\boldsymbol{I}$ 和 $\boldsymbol{B}=\boldsymbol{I}$，从而 $\boldsymbol{E}=\boldsymbol{0}$ 和 $\boldsymbol{e}=\boldsymbol{0}$，这与物理直觉相符。

因此，一个客观的弹性体本构律必须通过客观的[运动学](@entry_id:173318)量（如 $\boldsymbol{C}$ 或 $\boldsymbol{B}$）来表达，而不是直接使用非客观的 $\boldsymbol{F}$。这背后的物理意义可以通过**极分解** $\boldsymbol{F}=\boldsymbol{R}\boldsymbol{U}$ 来理解，其中 $\boldsymbol{R}$ 是旋转，$\boldsymbol{U}$ 是[右伸长张量](@entry_id:193756)。客观性要求本构响应不应受材料局部刚体旋转 $\boldsymbol{R}$ 的影响，而只应依赖于拉伸 $\boldsymbol{U}$。由于 $\boldsymbol{C}=\boldsymbol{U}^2$，使用 $\boldsymbol{C}$ 作为变量自然地过滤掉了非客观的旋转信息。

### [张量不变量](@entry_id:203254)：客观性的精髓

尽管 $\boldsymbol{\sigma}$ 和 $\boldsymbol{B}$ 等[空间张量](@entry_id:185799)的分量会随观察者而变，但我们可以构造一些纯量组合，其值在所有[坐标系](@entry_id:156346)下都保持不变。这些量被称为**[张量不变量](@entry_id:203254)**。它们构成了建立客观且具有[材料对称性](@entry_id:190289)的本构模型的数学基础。

对于任何一个[二阶张量](@entry_id:199780) $\boldsymbol{A}$，其三个**[主不变量](@entry_id:193522)** $I_1, I_2, I_3$ 是其[特征多项式](@entry_id:150909) $\det(\boldsymbol{A}-\lambda\boldsymbol{I}) = -\lambda^3 + I_1\lambda^2 - I_2\lambda + I_3 = 0$ 的系数。这些[不变量](@entry_id:148850)也可以直接通过张量分量计算：
$$
I_1(\boldsymbol{A}) = \mathrm{tr}\,\boldsymbol{A}
$$
$$
I_2(\boldsymbol{A}) = \frac{1}{2}\big[(\mathrm{tr}\,\boldsymbol{A})^2 - \mathrm{tr}(\boldsymbol{A}^2)\big]
$$
$$
I_3(\boldsymbol{A}) = \det \boldsymbol{A}
$$
我们可以证明，在[坐标旋转](@entry_id:164444) $\boldsymbol{A}' = \boldsymbol{Q}\boldsymbol{A}\boldsymbol{Q}^{\mathsf{T}}$下，这三个量确实保持不变。例如，利用[迹的循环性质](@entry_id:153103) $\mathrm{tr}(\boldsymbol{XYZ}) = \mathrm{tr}(\boldsymbol{ZXY})$，我们有 $I_1' = \mathrm{tr}(\boldsymbol{Q}\boldsymbol{A}\boldsymbol{Q}^{\mathsf{T}}) = \mathrm{tr}(\boldsymbol{Q}^{\mathsf{T}}\boldsymbol{Q}\boldsymbol{A}) = \mathrm{tr}(\boldsymbol{A}) = I_1$。类似地，利用[行列式的乘法性质](@entry_id:148055)和 $\det \boldsymbol{Q} = 1$，可以证明 $I_3' = I_3$。由于 $\mathrm{tr}(\boldsymbol{A}'^2) = \mathrm{tr}(\boldsymbol{Q}\boldsymbol{A}^2\boldsymbol{Q}^{\mathsf{T}}) = \mathrm{tr}(\boldsymbol{A}^2)$，所以 $I_2$ 也是[不变量](@entry_id:148850)。

这些[不变量](@entry_id:148850)具有明确的物理意义。如果张量 $\boldsymbol{A}$ 是对称的，它可以被[对角化](@entry_id:147016)，其对角元是它的三个[主值](@entry_id:189577)（[特征值](@entry_id:154894)）$\lambda_1, \lambda_2, \lambda_3$。[不变量](@entry_id:148850)可以表示为这些[主值](@entry_id:189577)的[对称函数](@entry_id:177113)：
$$
I_1 = \lambda_1 + \lambda_2 + \lambda_3
$$
$$
I_2 = \lambda_1\lambda_2 + \lambda_2\lambda_3 + \lambda_3\lambda_1
$$
$$
I_3 = \lambda_1\lambda_2\lambda_3
$$
由于主值是张量固有的属性，不受[坐标系](@entry_id:156346)影响，所以任何只依赖于[主值](@entry_id:189577)的函数都是[不变量](@entry_id:148850)。对于柯西应力张量 $\boldsymbol{\sigma}$，其[主值](@entry_id:189577)被称为**主应力**。第一[不变量](@entry_id:148850) $I_1$ 与[静水压力](@entry_id:275365)直接相关（$p = -I_1/3$），因此静水压力是一个客观的物理量。

对于**各向同性**材料，其本构响应在所有方向上都是相同的。这在数学上意味着本构函数必须是一个**[各向同性张量](@entry_id:195105)函数**。根据[表示定理](@entry_id:637872)，任何应力张量的标量值[各向同性函数](@entry_id:750877)（如[应变能](@entry_id:162699)）都可以表示为其三个[主不变量](@entry_id:193522)的函数，即 $\Psi = \Psi(I_1, I_2, I_3)$。这种形式自动满足了客观性要求，因为它不依赖于张量的分量，只依赖于[不变量](@entry_id:148850)。

重要的是要区分张量分量的变换与材料的对称性。在一个[各向同性材料](@entry_id:170678)中，一个非球形的应力张量（例如由[单轴拉伸](@entry_id:188287)引起）其分量在[坐标系](@entry_id:156346)旋转下仍然会改变。观察到张量分量变化，仅仅说明了张量本身的非球形性质，并不能得出材料是各向异性的结论。

考虑一个二维[平面应力](@entry_id:172193)问题可以具体地说明[不变量](@entry_id:148850)的威力。一个应力张量 $\boldsymbol{\sigma}$ 在 $(x,y)$ 基下的分量为 $\sigma_{xx}, \sigma_{yy}, \tau_{xy}$。其[主应力](@entry_id:176761) $\sigma_1, \sigma_2$ 是特征方程 $\lambda^2 - I_1\lambda + I_2 = 0$ 的解，其中 $I_1 = \sigma_{xx}+\sigma_{yy}$，$I_2 = \sigma_{xx}\sigma_{yy}-\tau_{xy}^2$。解为：
$$
\sigma_{1,2} = \frac{I_1 \pm \sqrt{I_1^2 - 4I_2}}{2}
$$
这个公式表明，无论我们选择哪个旋转的[坐标系](@entry_id:156346)来测量应力分量，只要我们将这些分量代入并计算[不变量](@entry_id:148850) $I_1$ 和 $I_2$，我们总能得到相同的、物理上唯一的两个主应力。主应力本身就是[不变量](@entry_id:148850)。

### 谱分解与[不变子空间](@entry_id:152829)

理解[张量不变量](@entry_id:203254)和主值的更深层次方法是通过**谱分解**。对称[二阶张量](@entry_id:199780)的**[谱定理](@entry_id:136620)**保证了任何一个实对称二阶张量 $\boldsymbol{T}$（如应力或[小应变张量](@entry_id:754968)）都存在一组实数[特征值](@entry_id:154894)（主值）$\{\lambda_i\}$ 和一个对应的标准[正交特征向量](@entry_id:155522)基（[主方向](@entry_id:276187)）$\{\boldsymbol{n}_i\}$。这使得张量可以被“分解”为：
$$
\boldsymbol{T} = \sum_{i=1}^{3} \lambda_i \boldsymbol{n}_i \otimes \boldsymbol{n}_i = \sum_{i=1}^{3} \lambda_i \boldsymbol{P}_i
$$
其中 $\boldsymbol{P}_i = \boldsymbol{n}_i \otimes \boldsymbol{n}_i$ 是沿着[主方向](@entry_id:276187) $\boldsymbol{n}_i$ 的**正交投影算子**。这些算子满足 $\boldsymbol{P}_i \boldsymbol{P}_j = \delta_{ij} \boldsymbol{P}_i$ 和 $\sum_i \boldsymbol{P}_i = \boldsymbol{I}$。

[谱分解](@entry_id:173707)揭示了张量的内在结构：它将其作用分解为沿着三个相互正交的主方向的独立拉伸（或压缩）。例如，一个纯剪切应力状态 $\boldsymbol{\sigma} = \tau(\boldsymbol{e}_1 \otimes \boldsymbol{e}_2 + \boldsymbol{e}_2 \otimes \boldsymbol{e}_1)$，其矩阵表示为 $\begin{pmatrix} 0  \tau  0 \\ \tau  0  0 \\ 0  0  0 \end{pmatrix}$。通过求解特征值问题，我们发现其主应力为 $\lambda_1=\tau, \lambda_2=-\tau, \lambda_3=0$，对应的主方向为 $\boldsymbol{n}_1 = \frac{1}{\sqrt{2}}(\boldsymbol{e}_1+\boldsymbol{e}_2)$, $\boldsymbol{n}_2 = \frac{1}{\sqrt{2}}(\boldsymbol{e}_1-\boldsymbol{e}_2)$, $\boldsymbol{n}_3 = \boldsymbol{e}_3$。这表明，一个在 $(x,y)$ 方向上的纯剪切状态，等效于在旋转45度的方向上的拉伸和在与之垂直方向上的压缩。

谱分解在计算张量函数时非常有用。例如，张量的任意整数次幂可以简单地表示为：
$$
\boldsymbol{T}^k = \sum_{i=1}^{3} \lambda_i^k \boldsymbol{P}_i
$$
因此，任何基于迹的更高阶[不变量](@entry_id:148850)都可以轻松计算。例如，$\mathrm{tr}(\boldsymbol{T}^4) = \mathrm{tr}(\sum_i \lambda_i^4 \boldsymbol{P}_i) = \sum_i \lambda_i^4 \mathrm{tr}(\boldsymbol{P}_i) = \sum_i \lambda_i^4$，因为 $\mathrm{tr}(\boldsymbol{P}_i)=1$。对于上述纯剪切例子，$\mathrm{tr}(\boldsymbol{\sigma}^4) = \tau^4 + (-\tau)^4 + 0^4 = 2\tau^4$。

**[不变子空间](@entry_id:152829)**是谱理论中的一个重要概念。一个[子空间](@entry_id:150286) $W \subseteq \mathbb{R}^3$ 被称为在 $\boldsymbol{T}$ 作用下是**不变的**，如果对于任何向量 $\boldsymbol{w} \in W$，其像 $\boldsymbol{T}(\boldsymbol{w})$ 仍然在 $W$ 中。[特征向量](@entry_id:151813)张成的空间（一维的特征空间）是最简单的[不变子空间](@entry_id:152829)。

当张量出现**[重根](@entry_id:151486)**（或称为**[简并特征值](@entry_id:187316)**）时，不变子空间的结构变得更加丰富。假设一个张量在一个主基下的形式为 $\mathrm{diag}(\lambda, \lambda, \mu)$，其中 $\lambda \neq \mu$。此时，对应于 $\lambda$ 的特征空间 $E_\lambda$ 是一个二维平面，而对应于 $\mu$ 的特征空间 $E_\mu$ 是一条直线。可以证明，任何在 $\boldsymbol{T}$ 下的不变子空间 $W$ 必须是 $E_\lambda$ 的一个[子空间](@entry_id:150286)与 $E_\mu$ 的一个[子空间](@entry_id:150286)的直和，即 $W = W_\lambda \oplus W_\mu$，其中 $W_\lambda \subseteq E_\lambda$ 且 $W_\mu \subseteq E_\mu$。

这一结论有几个重要推论：
1.  特征空间 $E_\lambda$ 和 $E_\mu$ 本身都是[不变子空间](@entry_id:152829)。
2.  任何 $E_\lambda$ 的[子空间](@entry_id:150286)（即特征平面中的任何直线或原点）都是不变的。这是因为对于 $E_\lambda$ 中的任何向量 $\boldsymbol{w}$，$\boldsymbol{T}(\boldsymbol{w}) = \lambda\boldsymbol{w}$，结果只是对原向量的缩放。
3.  如果一个张量是球形的，即 $\boldsymbol{T} = \lambda\boldsymbol{I}$（所有[特征值](@entry_id:154894)都相等），那么 $\mathbb{R}^3$ 的**每一个**[子空间](@entry_id:150286)都是不变的。

### 高等应用：分解与特殊变换

[张量变换](@entry_id:183453)和[不变量](@entry_id:148850)的理论在[连续介质力学](@entry_id:155125)的多个领域都有着关键应用，尤其是在本构模型的构建中。

#### [静水-偏应力分解](@entry_id:196441)

任何[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ 都可以唯一地分解为一个**球形（静水）部分**和一个**偏（剪切）部分**：
$$
\boldsymbol{\sigma} = p\boldsymbol{I} + \boldsymbol{s}
$$
其中 $p = \frac{1}{3}\mathrm{tr}(\boldsymbol{\sigma}) = \frac{1}{3}I_1$ 是**[静水压力](@entry_id:275365)**，而 $\boldsymbol{s} = \boldsymbol{\sigma} - p\boldsymbol{I}$ 是**[偏应力张量](@entry_id:267642)**，其迹为零 $\mathrm{tr}(\boldsymbol{s})=0$。

这个分解在物理上和数学上都极为重要。静水部分与材料的体积变化相关，而偏应力部分与形状变化（畸变）相关。由于 $p$ 直接由第一[不变量](@entry_id:148850) $I_1$ 决定，它是一个客观标量。在[坐标旋转](@entry_id:164444)下，静水部分 $p\boldsymbol{I}$ 保持不变，而[偏应力](@entry_id:163323)部分则和应力张量一样变换：$\boldsymbol{s}' = \boldsymbol{Q}\boldsymbol{s}\boldsymbol{Q}^{\mathsf{T}}$。[偏应力张量](@entry_id:267642)的[不变量](@entry_id:148850)，特别是第二[不变量](@entry_id:148850) $J_2 = \frac{1}{2}\mathrm{tr}(\boldsymbol{s}^2)$，在塑性力学中扮演核心角色，例如，著名的 **von Mises 屈服准则**就是假定当 $J_2$ 达到一个临界值时材料开始屈服。

#### 等容-[体积分](@entry_id:171119)解

在有限变形理论中，特别是对于橡胶等近乎不可压缩的材料，将变形能分解为体积变化部分和形状变化（等容）部分是标准做法。这可以通过对变形梯度 $\boldsymbol{F}$ 进行[乘法分解](@entry_id:199514)来实现：$\boldsymbol{F} = F_{\mathrm{vol}} \overline{\boldsymbol{F}}$。一种常见的方法是定义一个仅描述体积变化的球形张量和一个描述[等容变形](@entry_id:196451)的 unimodular 张量 $\overline{\boldsymbol{F}}$，其中 $J = \det \boldsymbol{F}$。
$$
\overline{\boldsymbol{F}} = J^{-1/3}\boldsymbol{F}, \quad \text{使得 } \det \overline{\boldsymbol{F}} = 1
$$
相应的，修正的（或等容的）[右柯西-格林张量](@entry_id:174156)为 $\overline{\boldsymbol{C}} = \overline{\boldsymbol{F}}^{\mathsf{T}}\overline{\boldsymbol{F}} = J^{-2/3}\boldsymbol{C}$。$\overline{\boldsymbol{C}}$ 的[不变量](@entry_id:148850)被称为**等容[不变量](@entry_id:148850)**：
$$
\overline{I}_1 = \mathrm{tr}(\overline{\boldsymbol{C}}) = J^{-2/3}I_1
$$
$$
\overline{I}_2 = \frac{1}{2}[(\mathrm{tr}\overline{\boldsymbol{C}})^2 - \mathrm{tr}(\overline{\boldsymbol{C}}^2)] = J^{-4/3}I_2
$$
这些等容[不变量](@entry_id:148850)对纯[体积缩放](@entry_id:197908)是不敏感的。基于此，[超弹性材料](@entry_id:190241)的[应变能函数](@entry_id:178435) $W$ 可以分解为等容部分和体积部分之和：$W(\boldsymbol{F}) = W_{\text{iso}}(\overline{I}_1, \overline{I}_2) + U(J)$。这种分解形式极大地简化了对[近不可压缩材料](@entry_id:752388)的建模。

#### 极分解与[反射变换](@entry_id:175518)

极分解 $\boldsymbol{F} = \boldsymbol{R}\boldsymbol{U}$ 是有限变形理论的基石，其中 $\boldsymbol{R}$ 是正常正交的（$\det \boldsymbol{R}=1$）。考虑一个更一般的情景，变形与一个**反射**（或称为[非正常旋转](@entry_id:151532)）复合，即 $\hat{\boldsymbol{F}} = \boldsymbol{Q}\boldsymbol{F}$，其中 $\boldsymbol{Q}$ 是一个正交张量且 $\det\boldsymbol{Q}=-1$。

我们可以分析 $\hat{\boldsymbol{F}}$ 的极分解 $\hat{\boldsymbol{F}} = \hat{\boldsymbol{R}}\hat{\boldsymbol{U}}$。新的[右柯西-格林张量](@entry_id:174156) $\hat{\boldsymbol{C}} = \hat{\boldsymbol{F}}^{\mathsf{T}}\hat{\boldsymbol{F}} = \boldsymbol{F}^{\mathsf{T}}\boldsymbol{Q}^{\mathsf{T}}\boldsymbol{Q}\boldsymbol{F} = \boldsymbol{F}^{\mathsf{T}}\boldsymbol{F} = \boldsymbol{C}$。由于[右伸长张量](@entry_id:193756)是其柯西-格林张量的唯一对称正定平方根（$\boldsymbol{U} = \boldsymbol{C}^{1/2}$），我们立即得到 $\hat{\boldsymbol{U}} = \boldsymbol{U}$。这意味着[右伸长张量](@entry_id:193756)不受左乘[反射变换](@entry_id:175518)的影响。

新的[旋转因子](@entry_id:201226)则为 $\hat{\boldsymbol{R}} = \hat{\boldsymbol{F}}\hat{\boldsymbol{U}}^{-1} = (\boldsymbol{Q}\boldsymbol{F})\boldsymbol{U}^{-1} = \boldsymbol{Q}(\boldsymbol{F}\boldsymbol{U}^{-1}) = \boldsymbol{Q}\boldsymbol{R}$。由于 $\det(\hat{\boldsymbol{R}}) = \det(\boldsymbol{Q})\det(\boldsymbol{R}) = (-1)(1) = -1$，新的正交因子 $\hat{\boldsymbol{R}}$ 本身也成了一个反射。这表明，虽然对于任何[可逆矩阵](@entry_id:171829)，其分解为一个[正交矩阵](@entry_id:169220)和一个对称正定矩阵是唯一的，但其正交部分是否为[正常旋转](@entry_id:141831)取决于原[矩阵行列式](@entry_id:194066)的符号。同时，[左伸长张量](@entry_id:197330)会发生变化 $\hat{\boldsymbol{V}} = \boldsymbol{Q}\boldsymbol{V}\boldsymbol{Q}^{\mathsf{T}}$，但其[主不变量](@entry_id:193522)保持不变。这一分析加深了我们对极分解唯一性和几何内涵的理解。