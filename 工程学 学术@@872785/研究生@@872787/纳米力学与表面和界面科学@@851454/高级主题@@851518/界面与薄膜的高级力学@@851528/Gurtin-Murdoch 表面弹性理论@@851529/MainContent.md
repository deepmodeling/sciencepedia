## 引言
当材料的特征尺寸缩小到纳米级别时，其表面积与体积之比急剧增大，使得经典连续介质力学因忽略表面效应而不再适用。为了准确描述[纳米结构](@entry_id:148157)的力学行为，我们需要一个能够将表面本身作为力学承载实体的理论框架。Gurtin-Murdoch [表面弹性](@entry_id:185474)理论应运而生，它提供了一个简洁而强大的模型，将表面或界面视为一个具有自身应力、应变和[弹性常数](@entry_id:146207)的零厚度薄膜。该理论成功地填补了宏观力学与纳米世界之间的鸿沟，为解释长期困扰研究者的[尺寸依赖性](@entry_id:158413)现象提供了物理基础。

本文将系统地引导您深入 Gurtin-Murdoch 理论的精髓。在“原理与机制”一章中，我们将从第一性原理出发，建立描述表面运动学、动力学和本构关系的数学框架。随后的“应用与跨学科联系”一章将通过大量实例，展示该理论如何在[材料科学](@entry_id:152226)、[纳米技术](@entry_id:148237)和工程领域解释实验现象[并指](@entry_id:276731)导器件设计。最后，“动手实践”部分将提供一系列解析和计算问题，帮助您将理论知识转化为解决实际问题的能力。

## 原理与机制

本章深入探讨 Gurtin-Murdoch [表面弹性](@entry_id:185474)理论的核心原理与基本机制。我们将从描述可变形表面的几何与[运动学](@entry_id:173318)入手，建立描述表面变形的数学语言。随后，我们将引入表面应力的概念，并从[动量守恒](@entry_id:149964)第一原理出发，推导控制[界面力学](@entry_id:750731)行为的广义 Young-Laplace 方程。在此基础上，我们将构建表面的本构模型，阐明表面应力与表面应变之间的关系，这包括从[热力学势](@entry_id:140516)（[表面自由能](@entry_id:159200)）推导本构关系，以及区分各向同性与各向异性材料模型。最后，我们将通过具体应用展示该理论如何预测[纳米结构](@entry_id:148157)的[尺寸依赖性力学](@entry_id:180358)行为，并探讨其相较于经典理论的独到之处。

### 可变形表面的运动学

为了精确描述嵌入在三维欧几里得空间 $\mathbb{R}^3$ 中的二维[曲面](@entry_id:267450)上的物理过程，我们首先需要建立一套合适的数学框架。这个框架的核心在于如何将环境空间中的矢量和[张量场](@entry_id:190170)分解为[曲面](@entry_id:267450)的切向和法向分量。

**切向投影算子**

考虑一个光滑、有向的[曲面](@entry_id:267450) $S$，其上每一点都有一个[单位法向量](@entry_id:178851) $\boldsymbol{n}$。空间中任意一个矢量 $\boldsymbol{v}$ 都可以唯一地分解为平行于 $\boldsymbol{n}$ 的法向分量 $\boldsymbol{v}_n$ 和正交于 $\boldsymbol{n}$ 的切向分量 $\boldsymbol{v}_s$。法向分量是 $\boldsymbol{v}$ 在 $\boldsymbol{n}$ 方向上的投影，即 $\boldsymbol{v}_n = (\boldsymbol{v} \cdot \boldsymbol{n})\boldsymbol{n}$。切向分量则是从原矢量中减去法向分量得到：
$$
\boldsymbol{v}_s = \boldsymbol{v} - \boldsymbol{v}_n = \boldsymbol{v} - (\boldsymbol{v} \cdot \boldsymbol{n})\boldsymbol{n}
$$
我们可以定义一个二阶张量，称为**切向[投影算子](@entry_id:154142) (tangential projector)** $\boldsymbol{P}$，它作用于任意矢量 $\boldsymbol{v}$ 时，能够直接得到其切向分量 $\boldsymbol{v}_s = \boldsymbol{P}\boldsymbol{v}$。利用二阶单位张量 $\boldsymbol{I}$ 和[并矢积](@entry_id:748716) (dyadic product) $\otimes$，上述表达式可以写为：
$$
\boldsymbol{P}\boldsymbol{v} = \boldsymbol{I}\boldsymbol{v} - \boldsymbol{n}(\boldsymbol{n}\cdot\boldsymbol{v}) = (\boldsymbol{I} - \boldsymbol{n}\otimes\boldsymbol{n})\boldsymbol{v}
$$
由此，我们得到切向[投影算子](@entry_id:154142)的表达式：
$$
\boldsymbol{P} = \boldsymbol{I} - \boldsymbol{n}\otimes\boldsymbol{n}
$$
这个算子具有两个至关重要的代数性质。首先是**[幂等性](@entry_id:190768) (idempotence)**，即 $\boldsymbol{P}^2 = \boldsymbol{P}$。这意味着对一个矢量连续进行两次切向投影，结果与一次投影相同，因为第一次投影后的矢量已经完全处于[切平面](@entry_id:136914)内。其次是**对[法向量](@entry_id:264185)的湮灭性 (annihilation of the normal)**，即 $\boldsymbol{P}\boldsymbol{n} = \boldsymbol{0}$。这表明法向量本身没有切向分量。这两个性质可以通过代数运算[直接证明](@entry_id:141172) [@problem_id:2772859]。

**[表面梯度](@entry_id:261146)与表面应变**

定义了投影算子后，我们便可以定义作用于[曲面](@entry_id:267450)上的场的微分算子。**[表面梯度](@entry_id:261146) (surface gradient)** 算子 $\nabla_s$ 捕捉了场沿着[曲面](@entry_id:267450)的变化率。对于一个定义在三维[环境空间](@entry_id:184743)中的矢量场 $\boldsymbol{u}(\boldsymbol{x})$，其在[曲面](@entry_id:267450) $S$ 上的[表面梯度](@entry_id:261146)是一个二阶张量，定义为：
$$
\nabla_s \boldsymbol{u} := \boldsymbol{P}(\nabla \boldsymbol{u})\boldsymbol{P}
$$
其中 $\nabla \boldsymbol{u}$ 是标准的三维梯度张量，其分量为 $(\nabla \boldsymbol{u})_{ij} = \partial u_i / \partial x_j$。这个定义的直观意义是：首先计算场在三维空间中的梯度，然后通过左右两边乘以投影算子 $\boldsymbol{P}$，将其限制在[曲面](@entry_id:267450)的[切空间](@entry_id:199137)内。这么做既保证了梯度的输入（作用方向）是切向的，也保证了其输出（场的变化量）是切向的。

例如，考虑一个平面 $S=\{\boldsymbol{x}\in\mathbb{R}^3: \boldsymbol{n}\cdot\boldsymbol{x}=1\}$，其中法向量为常数。对于一个给定的[位移场](@entry_id:141476) $\boldsymbol{u}(\boldsymbol{x})$，我们可以在[曲面](@entry_id:267450)上任意一点计算其三维梯度 $\nabla \boldsymbol{u}$，然后利用该点的 $\boldsymbol{P}$ 计算出 $\nabla_s \boldsymbol{u}$。这个[张量的迹](@entry_id:190669) $\operatorname{tr}(\nabla_s \boldsymbol{u})$ 被称为**表面散度 (surface divergence)**，它描述了[曲面](@entry_id:267450)上矢量场的面积通量密度 [@problem_id:2772859]。

在小变形假设下，**表面应变张量 (surface strain tensor)** $\boldsymbol{\varepsilon}_s$ 被定义为位移[表面梯度](@entry_id:261146)的对称部分：
$$
\boldsymbol{\varepsilon}_s = \frac{1}{2} ( \nabla_s \boldsymbol{u} + (\nabla_s \boldsymbol{u})^T ) = \mathrm{sym}(\nabla_s \boldsymbol{u})
$$
$\boldsymbol{\varepsilon}_s$ 是一个对称的二阶切向张量，它描述了[曲面](@entry_id:267450)单元的拉伸和剪切变形。它的迹 $\operatorname{tr}(\boldsymbol{\varepsilon}_s)$ 表示[曲面](@entry_id:267450)单元的微小面积变化率。

### 表面应力与[界面力](@entry_id:184024)平衡

Gurtin-Murdoch 理论的核心思想是，材料的表面或界面本身可以被视为一个具有自身力学特性的二维薄膜，这个薄膜能够承受面[内力](@entry_id:167605)。这种面[内力](@entry_id:167605)通过**[表面应力](@entry_id:191241)张量 (surface stress tensor)** $\boldsymbol{\sigma}_s$ 来描述。$\boldsymbol{\sigma}_s$ 是一个二阶切向张量（即 $\boldsymbol{\sigma}_s \boldsymbol{n} = \boldsymbol{0}$ 且 $\boldsymbol{n} \boldsymbol{\sigma}_s = \boldsymbol{0}$），它类似于三维连续体中的 Cauchy [应力张量](@entry_id:148973)。其物理意义是，在[曲面](@entry_id:267450)上切开一条线，$\boldsymbol{\sigma}_s \boldsymbol{\nu}$ 就代表了线一侧对另一侧单位长度上施加的力，其中 $\boldsymbol{\nu}$ 是垂直于该线的切向量。

当一个带有表面应力的界面处于静态平衡时，作用在其上的所有力必须相互抵消。考虑一个分隔两个体块（$\Omega^+$ 和 $\Omega^-$）的界面 $\Gamma$ 上的任意一个小面元 $S$。作用在该面元上的力有三部分：
1.  来自体块 $\Omega^+$ 的力，通过体块应力 $\boldsymbol{\sigma}^+$ 作用在界面上，其[合力](@entry_id:163825)为 $\int_S \boldsymbol{\sigma}^+\boldsymbol{n}^+ dA$。这里 $\boldsymbol{n}^+$ 是指向 $\Omega^+$ 外部的[法向量](@entry_id:264185)。
2.  来自体块 $\Omega^-$ 的力，通过体块应力 $\boldsymbol{\sigma}^-$ 作用在界面上，其合力为 $\int_S \boldsymbol{\sigma}^-\boldsymbol{n}^- dA$。这里 $\boldsymbol{n}^-$ 是指向 $\Omega^-$ 外部的[法向量](@entry_id:264185)，满足 $\boldsymbol{n}^- = -\boldsymbol{n}^+$。
3.  来自面元 $S$ 周围界面部分通过其边界 $\partial S$ 施加的线力，其[合力](@entry_id:163825)为 $\int_{\partial S} \boldsymbol{\sigma}_s \boldsymbol{\nu} ds$。

根据表面[散度定理](@entry_id:143110)，[线积分](@entry_id:141417)可以转化为面积分 $\int_S (\nabla_s \cdot \boldsymbol{\sigma}_s) dA$。在静态、无[体力](@entry_id:174230)矩的情况下，力平衡要求这些力的总和为零。由于面元 $S$ 的任意性，被积函数必须处处为零，这便得到了[界面力](@entry_id:184024)平衡的点式方程 [@problem_id:2772814]：
$$
\nabla_s \cdot \boldsymbol{\sigma}_s + \boldsymbol{\sigma}^+\boldsymbol{n}^+ + \boldsymbol{\sigma}^-\boldsymbol{n}^- = \boldsymbol{0}
$$
这个方程是 Gurtin-Murdoch 理论的基石之一。其中，$\nabla_s \cdot \boldsymbol{\sigma}_s$ 项代表了由表面应力在[曲面](@entry_id:267450)上[分布](@entry_id:182848)不均所产生的单位面积力。$\boldsymbol{\sigma}^+\boldsymbol{n}^+ + \boldsymbol{\sigma}^-\boldsymbol{n}^-$ 项是两侧体块施加在界面上的**净牵[引力](@entry_id:175476) (net traction)**。若定义一个统一的法向量 $\boldsymbol{n}$ (例如从 $\Omega^-$ 指向 $\Omega^+$)，则 $\boldsymbol{n}^+=\boldsymbol{n}$ 且 $\boldsymbol{n}^-=-\boldsymbol{n}$。此时，净牵[引力](@entry_id:175476)可以写作**牵[引力](@entry_id:175476)跳跃 (traction jump)** 的形式：$[[\boldsymbol{\sigma}\boldsymbol{n}]] := \boldsymbol{\sigma}^+\boldsymbol{n} - \boldsymbol{\sigma}^-\boldsymbol{n}$。于是，[平衡方程](@entry_id:172166)通常写为：
$$
\nabla_s \cdot \boldsymbol{\sigma}_s + [[\boldsymbol{\sigma}\boldsymbol{n}]] = \boldsymbol{0}
$$
这个方程也被称为**广义 Young-Laplace 方程**。它表明，界面两侧的牵[引力](@entry_id:175476)不再需要连续（即 $[[\boldsymbol{\sigma}\boldsymbol{n}]] \neq \boldsymbol{0}$），其[不连续性](@entry_id:144108)（跳跃）可以由表面[应力的散度](@entry_id:185633)来平衡。只有当表面没有力学效应（$\boldsymbol{\sigma}_s = \boldsymbol{0}$）时，该方程才退化为经典的牵[引力](@entry_id:175476)连续条件 $[[\boldsymbol{\sigma}\boldsymbol{n}]] = \boldsymbol{0}$。

### 表面的[本构模型](@entry_id:174726)

上述力[平衡方程](@entry_id:172166)联系了[表面应力](@entry_id:191241)与体应力，但它本身并不完整，因为我们还需要一个描述[表面应力](@entry_id:191241)如何产生的**[本构关系](@entry_id:186508) (constitutive relation)**。

#### [热力学](@entry_id:141121)基础：[表面能](@entry_id:161228)与 Shuttleworth 方程

对于固体表面，**[表面自由能](@entry_id:159200) (surface free energy)** $\gamma$（单位面积的 Helmholtz 自由能）和[表面应力](@entry_id:191241) $\boldsymbol{\sigma}_s$ 是两个不同但相关的物理量。[表面自由能](@entry_id:159200) $\gamma$ 是指等温等体积下可逆地创造单位面积表面所需要做的功；而[表面应力](@entry_id:191241) $\boldsymbol{\sigma}_s$ 是指等温下可逆[地弹](@entry_id:173166)性拉伸一块已存在的单位面积表面所需要做的功。

通过对一个表面单元进行[虚功](@entry_id:176403)分析，可以推导出联系这两个量的[基本热力学关系](@entry_id:144320)，即 **Shuttleworth 方程** [@problem_id:2772816]。对于一个依赖于表面应变 $\boldsymbol{\varepsilon}_s$ 的[表面能](@entry_id:161228)密度 $\gamma(\boldsymbol{\varepsilon}_s)$，[表面应力](@entry_id:191241)张量 $\boldsymbol{\sigma}_s$ (这里用 $\boldsymbol{\Upsilon}$ 表示以区分) 由下式给出：
$$
\boldsymbol{\Upsilon} = \gamma \boldsymbol{P} + \frac{\partial \gamma}{\partial \boldsymbol{\varepsilon}_s}
$$
其中 $\boldsymbol{P}$ 是切向投影算子（在此作为面内单位张量）。这个方程表明，表面应力由两部分贡献：一部分与表面能密度 $\gamma$ 本身的大小有关，表现为各向同性的张力；另一部分与表面能随应变的变化率有关，代表了表面的弹性响应。

只有当[表面能](@entry_id:161228) $\gamma$ 不随应变 $\boldsymbol{\varepsilon}_s$ 变化时（$\partial \gamma / \partial \boldsymbol{\varepsilon}_s = \boldsymbol{0}$），[表面应力](@entry_id:191241)才简化为 $\boldsymbol{\Upsilon} = \gamma \boldsymbol{P}$。这种情况是理想液体表面的特征，其表面张力数值上等于[表面能](@entry_id:161228)。对于固体，尤其是晶体，原子键的拉伸会改变表面能，因此 $\gamma$ 总是应变的函数，导致表面应力不等于[表面能](@entry_id:161228)。

#### 线性[各向同性弹性](@entry_id:203237)表面

对于一个各向同性的弹性表面，在小应变下，我们可以将[表面自由能](@entry_id:159200) $\gamma$ 展开为应变 $\boldsymbol{\varepsilon}_s$ 的二次函数：
$$
\gamma(\boldsymbol{\varepsilon}_s) = \gamma_0 + \tau_0 \operatorname{tr}(\boldsymbol{\varepsilon}_s) + \frac{1}{2}\lambda_s (\operatorname{tr}(\boldsymbol{\varepsilon}_s))^2 + \mu_s \boldsymbol{\varepsilon}_s : \boldsymbol{\varepsilon}_s
$$
其中，$\gamma_0$ 是未变形时的[表面能](@entry_id:161228)，$\tau_0$ 是未变形时的**[残余表面应力](@entry_id:191384) (residual surface stress)**，$\lambda_s$ 和 $\mu_s$ 是表面的**拉梅常数 (Lamé constants)**，其单位是力/长度（例如 N/m）。$\mu_s$ 称为**表面剪切模量**，抵抗面内形状改变；$\lambda_s$ 和 $\mu_s$ 共同决定了抵抗面内面积改变的能力。

将此能量表达式代入 Shuttleworth 方程，或者基于一般线性[各向同性张量函数的表示定理](@entry_id:754252)，我们可以直接写出线性化的 Gurtin-Murdoch [本构关系](@entry_id:186508) [@problem_id:2772918] [@problem_id:2772895]：
$$
\boldsymbol{\sigma}_s = \tau_0 \boldsymbol{P} + 2\mu_s \boldsymbol{\varepsilon}_s + \lambda_s \operatorname{tr}(\boldsymbol{\varepsilon}_s) \boldsymbol{P}
$$
这个关系式是 Gurtin-Murdoch 理论在各向同性情况下的核心。它表明表面应力由三部分构成：
1.  **[残余应力](@entry_id:138788)** $\tau_0 \boldsymbol{P}$：即使在没有任何宏观应变（$\boldsymbol{\varepsilon}_s = \boldsymbol{0}$）的情况下，表面由于其原子结构与体内的不同，本身就存在一个各向同性的张力或压力。
2.  **剪切响应** $2\mu_s \boldsymbol{\varepsilon}_s$：这部分与应变张量的偏量部分成正比，抵抗表面的形状变化。
3.  **面积膨胀响应** $\lambda_s \operatorname{tr}(\boldsymbol{\varepsilon}_s) \boldsymbol{P}$：这部分与应变的迹（即面积变化）成正比，抵抗表面的面积变化。

一个重要的特例是，当表面不存在弹性（$\lambda_s = \mu_s = 0$）时，本构关系退化为 $\boldsymbol{\sigma}_s = \tau_0 \boldsymbol{P}$。这是一个恒定的、各向同性的表面张力模型，类似于液体表面。此时，广义 Young-Laplace 方程 $\nabla_s \cdot \boldsymbol{\sigma}_s + [[\boldsymbol{\sigma}\boldsymbol{n}]] = \boldsymbol{0}$ 可以被推导为经典形式。对于一个曲率处处相同的表面，$\nabla_s \cdot (\tau_0 \boldsymbol{P}) = -2H \tau_0 \boldsymbol{n}$，其中 $H$ 是平均曲率。若界面两侧为流体，$[[\boldsymbol{\sigma}\boldsymbol{n}]] = \Delta p \boldsymbol{n}$。代入力[平衡方程](@entry_id:172166)得到 $\Delta p = 2H \tau_0$。对于球体，$H=1/R$，于是我们得到了经典的 Young-Laplace 方程 $\Delta p = 2\tau_0/R$ [@problem_id:2772812]。

#### [各向异性弹性](@entry_id:186771)表面

对于晶体材料，其表面性质通常是各向异性的。此时，[表面自由能](@entry_id:159200)中的二次项需要用一个四阶的**[表面弹性](@entry_id:185474)张量** $\boldsymbol{\mathcal{A}}$ 来描述 [@problem_id:2772862]：
$$
\gamma(\boldsymbol{\varepsilon}_s) = \gamma_0 + \frac{1}{2} \boldsymbol{\varepsilon}_s : \boldsymbol{\mathcal{A}} : \boldsymbol{\varepsilon}_s
$$
应用 Shuttleworth 方程，我们得到各向异性情况下的[表面应力](@entry_id:191241)为：
$$
\boldsymbol{\sigma}_s = \left(\gamma_0 + \frac{1}{2} \boldsymbol{\varepsilon}_s : \boldsymbol{\mathcal{A}} : \boldsymbol{\varepsilon}_s\right) \boldsymbol{P} + \boldsymbol{\mathcal{A}} : \boldsymbol{\varepsilon}_s
$$
注意这里我们假设了零应变下不存在[残余应力](@entry_id:138788)，但可以轻易将其加入。[四阶张量](@entry_id:181350) $\boldsymbol{\mathcal{A}}$ 必须满足特定的对称性要求。首先，由于能量的存在性和[应力应变](@entry_id:204183)关系，它必须具备**主对称性** ($\mathcal{A}_{ijkl} = \mathcal{A}_{klij}$) 和**次对称性** ($\mathcal{A}_{ijkl} = \mathcal{A}_{jikl} = \mathcal{A}_{ijlk}$)。其次，为了反映[晶格](@entry_id:196752)的对称性，$\boldsymbol{\mathcal{A}}$ 在该[晶体表面](@entry_id:195760)的[点群](@entry_id:142456)操作下必须保持不变（Neumann 原理）。这些对称性约束大大减少了 $\boldsymbol{\mathcal{A}}$ 的独立分量数目。

### 应用与启示

Gurtin-Murdoch 理论最重要的应用之一是解释和预测纳米尺度物体的[尺寸依赖性力学](@entry_id:180358)行为。

#### 广义 Young-Laplace 方程

让我们考虑一个半径为 $R$ 的球形界面，它从一个无应力的参考半径 $R_0$ 膨胀而来。表面的应变是均匀的、双轴的，$\varepsilon_s = (R-R_0)/R_0$。将各向同性本构关系 $\boldsymbol{\sigma}_s = (\tau_0 + (2\lambda_s+2\mu_s)\varepsilon_s) \boldsymbol{P}$ 代入[界面力](@entry_id:184024)[平衡方程](@entry_id:172166)，可以推导出广义 Young-Laplace 方程 [@problem_id:2772908]：
$$
\Delta p = \frac{2}{R} \left( \tau_0 + (2\lambda_s + 2\mu_s) \frac{R - R_0}{R_0} \right)
$$
这个方程表明，维持一个半径为 $R$ 的球形界面所需的压力差 $\Delta p$ 不仅取决于当前的曲率 $1/R$ 和[残余表面应力](@entry_id:191384) $\tau_0$，还取决于表面的弹性响应（由 $\lambda_s, \mu_s$ 描述）以及它的“变形历史”（由应变 $(R-R_0)/R_0$ 体现）。

#### [表面弹性](@entry_id:185474)的历史依赖性

经典表面张力模型与 Gurtin-Murdoch [表面弹性](@entry_id:185474)模型之间的一个根本区别在于**历史依赖性 (history dependence)**。我们可以通过一个思想实验来揭示这一点 [@problem_id:2772815]。

考虑一个半径为 $R=10$ nm 的纳米球。
*   **路径 A**: 球体在制造时其无应力参考半径就是 $R_0^{(A)} = 10$ nm。
*   **路径 B**: 球体在制造时其无应力参考半径是一个较小的值，例如 $R_0^{(B)} = 9.5$ nm，然后被弹性拉伸到 $10$ nm。

对于一个**恒定表面张力模型**（如液体），表面应力只与当前状态有关。因此，无论通过路径 A 还是 B，只要最终半径是 $10$ nm，所需的压力差都是一样的，即 $\Delta p = 2\gamma/R$。

然而，对于一个 Gurtin-Murdoch **弹性表面模型**，情况则大不相同。
*   在路径 A 中，应变为零（$R=R_0^{(A)}$），所以压力差仅由[残余应力](@entry_id:138788)决定：$\Delta p_A = 2\tau_0/R$。
*   在路径 B 中，表面被拉伸，产生了正的应变 $\varepsilon_s = (10-9.5)/9.5 > 0$。这个应变会通过弹性项 $(2\lambda_s+2\mu_s)\varepsilon_s$ 产生额外的[表面应力](@entry_id:191241)。因此，所需的压力差为 $\Delta p_B = (2/R)(\tau_0 + \text{弹性贡献})$，这会显著大于 $\Delta p_A$。

这个例子清晰地表明，固体的表面像一个弹性薄膜，它“记住”了它的初始无应力状态。两个具有相同当前形状的物体，如果它们的制造或加载历史不同，其内部的表面应力[状态和](@entry_id:193625)外在的力学响应可以是截然不同的。这是理解和设计纳米器件时必须考虑的关键因素。

### 展望：超越线性理论

本章所讨论的 Gurtin-Murdoch 理论是线性化的，即它假设了微小的表面应变和转动。这在许多情况下是有效的近似，但它有其局限性 [@problem_id:2772881]。例如，它无法描述由大拉伸引起的[几何非线性](@entry_id:169896)或[材料各向异性](@entry_id:204117)的演化，也无法严格满足大转动下的[客观性原理](@entry_id:185412)。

为了将该理论推广到**有限应变**领域，需要遵循[非线性](@entry_id:637147)连续介质力学的标准框架：
1.  定义一个**表面变形梯度** $\boldsymbol{F}_s$，它描述了参考构型中表面[切向量](@entry_id:265494)到当前构型中表面切向量的映射。
2.  引入一个客观的[应变度量](@entry_id:755495)，通常是**表面右 Cauchy-Green 张量** $\boldsymbol{C}_s = \boldsymbol{F}_s^T \boldsymbol{F}_s$。
3.  假设一个依赖于 $\boldsymbol{C}_s$ 的客观的**表面能函数** $\hat{\gamma}(\boldsymbol{C}_s)$。
4.  通过对能量函数求导，获得与应变共轭的表面应力张量（例如，第二 Piola-Kirchhoff 表面应力 $\boldsymbol{S}_s = 2 \partial\hat{\gamma}/\partial\boldsymbol{C}_s$）。
5.  [残余表面应力](@entry_id:191384)可以通过恰当地选择能量函数形式来引入，使得在未变形状态（$\boldsymbol{C}_s=\boldsymbol{P}$）下，应力不为零。

这个有限应变框架为处理涉及大变形的[纳米力学](@entry_id:185346)问题（如纳米薄膜的[屈曲](@entry_id:162815)、[纳米线](@entry_id:195506)的拉伸断裂等）提供了必要的理论工具。