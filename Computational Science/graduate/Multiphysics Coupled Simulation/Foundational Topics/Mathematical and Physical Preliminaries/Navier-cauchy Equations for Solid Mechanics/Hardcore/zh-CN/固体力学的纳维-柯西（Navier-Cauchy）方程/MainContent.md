## 引言
[纳维-柯西方程](@entry_id:189211)是[固体力学](@entry_id:164042)的基石，是描述弹性材料在外力作用下如何变形和响应的数学语言。尽管其形式优雅，但从其基本原理的深刻理解到在复杂多物理场耦合问题中的灵活应用，往往存在着知识上的鸿沟。本文旨在弥合这一差距，为读者构建一个从理论到实践的完整知识体系。

在接下来的内容中，您将踏上一段系统性的学习之旅。在“原理与机制”一章中，我们将深入其核心，从变形运动学和本构关系出发，推导出这一关键的控制方程，并探讨其在[弹性波](@entry_id:196203)、边值问题等方面的理论内涵。随后，在“应用与跨学科联系”一章中，我们将视野扩展到更广阔的工程与科学领域，展示该方程如何与热、流体、电磁等物理场耦合，解决从土木工程到[材料科学](@entry_id:152226)的实际问题。最后，通过“动手实践”部分，您将有机会直面并解决数值模拟中遇到的关键挑战，将理论知识转化为实践能力。

## 原理与机制

本章深入探讨线弹性[固体力学](@entry_id:164042)的核心控制方程——[纳维-柯西方程](@entry_id:189211) (Navier-Cauchy equations) 的基本原理和机制。我们将从变形的[运动学](@entry_id:173318)描述出发，建立位移与应变的联系；接着，通过[动量守恒](@entry_id:149964)和本构关系，推导出静态与动态的[纳维-柯西方程](@entry_id:189211)；最后，我们将探讨该方程在波传播、边值问题、数值计算以及高等理论中的应用，从而系统地构建对弹性固体行为的深刻理解。

### 变形运动学：位移与应变

在[连续介质力学](@entry_id:155125)中，固体的变形是通过一个[光滑映射](@entry_id:203730) $\boldsymbol{\varphi}$ 来描述的。该映射将物体在未变形的**参考构型** $\mathcal{B}_0$ 中的任一物质点 $\boldsymbol{X}$，映射到其在变形后的**当前构型**中的空间位置 $\boldsymbol{x} = \boldsymbol{\varphi}(\boldsymbol{X}, t)$。

#### [位移场](@entry_id:141476)与应变张量

为了量化变形，我们首先引入**[位移场](@entry_id:141476) (displacement field)** $\boldsymbol{u}$，它定义为物[质点](@entry_id:186768)当前位置与[参考位](@entry_id:754187)置之间的矢量差。在**[拉格朗日描述](@entry_id:264498)**（或称物质描述）中，位移是物质坐标 $\boldsymbol{X}$ 和时间 $t$ 的函数：
$$
\boldsymbol{u}(\boldsymbol{X}, t) = \boldsymbol{\varphi}(\boldsymbol{X}, t) - \boldsymbol{X}
$$
变形的局部特性由**变形梯度 (deformation gradient)** $\boldsymbol{F}$ 描述，它定义为映射 $\boldsymbol{\varphi}$ 对物质坐标 $\boldsymbol{X}$ 的梯度：
$$
\boldsymbol{F} = \nabla_{\boldsymbol{X}}\boldsymbol{\varphi} = \frac{\partial \boldsymbol{x}}{\partial \boldsymbol{X}} = \boldsymbol{I} + \nabla_{\boldsymbol{X}}\boldsymbol{u}
$$
其中 $\boldsymbol{I}$ 是二阶单位张量。变形梯度 $\boldsymbol{F}$ 包含了关于局部拉伸、剪切和旋转的全部信息。

然而，在固体力学中，我们通常更关心能引起内力（应力）的纯变形，而非不产生应力的刚体运动。**应变 (strain)** 的度量正是为此目的而设计的。一个精确且通用的[应变度量](@entry_id:755495)是**[格林-拉格朗日应变张量](@entry_id:187745) (Green-Lagrange strain tensor)** $\boldsymbol{E}$，其定义为：
$$
\boldsymbol{E} = \frac{1}{2} (\boldsymbol{F}^T \boldsymbol{F} - \boldsymbol{I})
$$
这个定义的一个关键性质是其对**刚体运动的客观性 (objectivity)**。考虑一个纯[刚体运动](@entry_id:193355) $\boldsymbol{x} = \boldsymbol{R}\boldsymbol{X} + \boldsymbol{c}$，其中 $\boldsymbol{R}$ 是一个旋转矩阵 ($\boldsymbol{R}^T\boldsymbol{R} = \boldsymbol{I}$)，$\boldsymbol{c}$ 是一个平移向量。在此情况下，变形梯度 $\boldsymbol{F} = \boldsymbol{R}$，代入 $\boldsymbol{E}$ 的定义可得 $\boldsymbol{E} = \frac{1}{2} (\boldsymbol{R}^T \boldsymbol{R} - \boldsymbol{I}) = \boldsymbol{0}$。这表明[格林-拉格朗日应变张量](@entry_id:187745)能够正确地识别出[刚体运动](@entry_id:193355)中不存在任何变形 。

将 $\boldsymbol{F} = \boldsymbol{I} + \nabla_{\boldsymbol{X}}\boldsymbol{u}$ 代入 $\boldsymbol{E}$ 的表达式，我们得到：
$$
\boldsymbol{E} = \frac{1}{2} \left( (\boldsymbol{I} + \nabla_{\boldsymbol{X}}\boldsymbol{u})^T (\boldsymbol{I} + \nabla_{\boldsymbol{X}}\boldsymbol{u}) - \boldsymbol{I} \right) = \frac{1}{2} \left( \nabla_{\boldsymbol{X}}\boldsymbol{u} + (\nabla_{\boldsymbol{X}}\boldsymbol{u})^T + (\nabla_{\boldsymbol{X}}\boldsymbol{u})^T \nabla_{\boldsymbol{X}}\boldsymbol{u} \right)
$$
这个表达式是[非线性](@entry_id:637147)的，包含了[位移梯度](@entry_id:165352)的二次项，适用于**有限应变 (finite strain)** 理论。

#### 小应变线性化

在许多工程应用中，材料的变形非常微小。在这种情况下，[位移梯度张量](@entry_id:748571) $\nabla_{\boldsymbol{X}}\boldsymbol{u}$ 的所有分量都远小于1，即 $\|\nabla_{\boldsymbol{X}}\boldsymbol{u}\| \ll 1$。这就是**小应变假设 (small-strain assumption)**。在此假设下，我们可以忽略[格林-拉格朗日应变张量](@entry_id:187745)中的高阶项 $(\nabla_{\boldsymbol{X}}\boldsymbol{u})^T \nabla_{\boldsymbol{X}}\boldsymbol{u}$，从而得到一个线性化的[应变度量](@entry_id:755495)，即**[无穷小应变张量](@entry_id:167211) (infinitesimal strain tensor)** 或柯西[应变张量](@entry_id:193332) $\boldsymbol{\varepsilon}$：
$$
\boldsymbol{\varepsilon} \approx \frac{1}{2} \left( \nabla_{\boldsymbol{X}}\boldsymbol{u} + (\nabla_{\boldsymbol{X}}\boldsymbol{u})^T \right)
$$
由于小变形时参考构型与当前构型几乎重合，我们可以不严格区分物质坐标 $\boldsymbol{X}$ 和空间坐标 $\boldsymbol{x}$，因此通常写作：
$$
\boldsymbol{\varepsilon}(\boldsymbol{u}) = \frac{1}{2} \left( \nabla\boldsymbol{u} + (\nabla\boldsymbol{u})^T \right)
$$
这个张量是[位移梯度](@entry_id:165352)的对称部分。[小应变张量](@entry_id:754968) $\boldsymbol{\varepsilon}$ 构成了[线性弹性](@entry_id:166983)理论的基础。然而，需要强调的是，这种线性化牺牲了对大转动的客观性。对于一个有限转动（非无穷小转动），$\boldsymbol{R} \neq \boldsymbol{I}$，相应的[无穷小应变张量](@entry_id:167211) $\boldsymbol{\varepsilon} = \frac{1}{2}(\boldsymbol{R}+\boldsymbol{R}^T) - \boldsymbol{I}$ 通常不为零，这表明它错误地将纯转动识别为应变。因此，小应变理论仅在位移、应变和转动都足够小的情况下成立 。

这种线性化在多物理场耦合建模中也具有重要意义。在线性理论框架下，总应变可以方便地进行**加法分解 (additive decomposition)**。例如，在[热弹性](@entry_id:158447)问题中，总应变 $\boldsymbol{\varepsilon}$ 可以分解为机械应变 $\boldsymbol{\varepsilon}^{\text{mech}}$ 和[热应变](@entry_id:187744) $\boldsymbol{\varepsilon}^{\text{th}}$ 之和，即 $\boldsymbol{\varepsilon} = \boldsymbol{\varepsilon}^{\text{mech}} + \boldsymbol{\varepsilon}^{\text{th}}$。相反，在[有限应变理论](@entry_id:176941)中，处理非弹性效应（如塑性）通常采用基于变形梯度的**[乘法分解](@entry_id:199514) (multiplicative decomposition)**，例如 $\boldsymbol{F} = \boldsymbol{F}_{\mathrm{e}}\boldsymbol{F}_{\mathrm{p}}$，这反映了变形过程的先后次序 。

### 控制方程的建立

弹性体的行为由一系列基本物理定律决定，包括动量守恒、[本构关系](@entry_id:186508)和[运动学](@entry_id:173318)关系。将它们结合起来，便可得到[纳维-柯西方程](@entry_id:189211)。

#### 应力、平衡与[本构关系](@entry_id:186508)

根据**柯西应力定理 (Cauchy's Stress Theorem)**，作用在物体内部一个假想面上的力（面力）可以通过**柯西应力张量 (Cauchy stress tensor)** $\boldsymbol{\sigma}$ 来描述。作用在法向量为 $\boldsymbol{n}$ 的单位面积上的**[面力矢量](@entry_id:189429) (traction vector)** $\boldsymbol{t}$ 由下式给出：
$$
\boldsymbol{t} = \boldsymbol{\sigma}\boldsymbol{n}
$$
此外，动量矩[守恒定律](@entry_id:269268)在经典连续介质理论中要求柯西应力张量必须是对称的，即 $\boldsymbol{\sigma} = \boldsymbol{\sigma}^T$ 。

在没有惯性效应的静态或准静态情况下，[线性动量守恒](@entry_id:165717)（或称[力平衡](@entry_id:267186)）要求应力[张量的散度](@entry_id:191736)与单位体积所受的体力 $\boldsymbol{b}$ 相平衡：
$$
\nabla \cdot \boldsymbol{\sigma} + \boldsymbol{b} = \boldsymbol{0}
$$
对于动态问题，[平衡方程](@entry_id:172166)则包含惯性项：
$$
\nabla \cdot \boldsymbol{\sigma} + \boldsymbol{b} = \rho \frac{\partial^2 \boldsymbol{u}}{\partial t^2}
$$
其中 $\rho$ 是材料的密度。

为了封闭上述方程，我们需要一个描述[材料力学](@entry_id:201885)行为的**[本构关系](@entry_id:186508) (constitutive relation)**。对于**线弹性材料 (linear elastic material)**，[应力与应变](@entry_id:137374)成线性关系，即 $\boldsymbol{\sigma} = \mathbb{C} : \boldsymbol{\varepsilon}$，其中 $\mathbb{C}$ 是一个四阶**[刚度张量](@entry_id:176588) (stiffness tensor)**。

对于**各向同性 (isotropic)** 的线弹性材料，其本构关系（也称**胡克定律 (Hooke's law)**）可以由两个独立的材料常数来表征。最常见的形式是使用**拉梅参数 (Lamé parameters)** $\lambda$ 和 $\mu$：
$$
\boldsymbol{\sigma} = \lambda \operatorname{tr}(\boldsymbol{\varepsilon})\boldsymbol{I} + 2\mu\boldsymbol{\varepsilon}
$$
这里，$\mu$ 被称为**剪切模量 (shear modulus)**，它关联了[剪切应力](@entry_id:137139)与剪切应变。$\lambda$ 则与材料的体积变形响应有关。

为了更好地理解这些参数的物理意义，我们可以将它们与工程中更直观的**[杨氏模量](@entry_id:140430) (Young's modulus)** $E$ 和**[泊松比](@entry_id:158876) (Poisson's ratio)** $\nu$ 联系起来。考虑一个单轴应力实验，沿 $x_1$ 方向施加应力 $\sigma_{11} = \sigma_0$，其他应力分量为零。根据定义，$E = \sigma_0 / \varepsilon_{11}$，$\nu = - \varepsilon_{22} / \varepsilon_{11}$。通过将该[应力应变](@entry_id:204183)状态代入各向同性[胡克定律](@entry_id:149682)，经过一系列代数推导，我们可以得到它们之间的转换关系 ：
$$
\mu = \frac{E}{2(1+\nu)}
$$
$$
\lambda = \frac{E\nu}{(1+\nu)(1-2\nu)}
$$
这些关系式是线[弹性理论](@entry_id:184142)中的基本公式，使得我们可以在不同材料参数体系之间灵活转换。

#### [纳维-柯西方程](@entry_id:189211)

将[运动学](@entry_id:173318)关系 $\boldsymbol{\varepsilon}(\boldsymbol{u}) = \frac{1}{2} (\nabla\boldsymbol{u} + (\nabla\boldsymbol{u})^T)$ 和各向同性[本构关系](@entry_id:186508) $\boldsymbol{\sigma} = \lambda \operatorname{tr}(\boldsymbol{\varepsilon})\boldsymbol{I} + 2\mu\boldsymbol{\varepsilon}$ 代入动态[动量守恒](@entry_id:149964)方程 $\nabla \cdot \boldsymbol{\sigma} + \boldsymbol{b} = \rho \ddot{\boldsymbol{u}}$ 中，即可得到完全用[位移场](@entry_id:141476) $\boldsymbol{u}$ 表示的控制方程，即**[纳维-柯西方程](@entry_id:189211) (Navier-Cauchy equations)**：
$$
(\lambda + \mu) \nabla(\nabla \cdot \boldsymbol{u}) + \mu \nabla^2\boldsymbol{u} + \boldsymbol{b} = \rho \frac{\partial^2 \boldsymbol{u}}{\partial t^2}
$$
其中 $\nabla^2\boldsymbol{u}$ 是矢量拉普拉斯算子。该方程是描述均匀、各向同性、线弹性[固体力学](@entry_id:164042)行为的[偏微分方程](@entry_id:141332)。对于静态问题，等式右边的惯性项为零。

### 方程的求解与分析

[纳维-柯西方程](@entry_id:189211)是一个复杂的[偏微分方程组](@entry_id:172573)。它的解不仅取决于方程本身，还强烈依赖于所施加的边界条件和初始条件。

#### 弹性[波的传播](@entry_id:144063)

[纳维-柯西方程](@entry_id:189211)描述了机械扰动如何在弹性介质中以波的形式传播。为了研究这种传播特性，我们考虑一个无体力项 ($\boldsymbol{b}=\boldsymbol{0}$) 的无限大均匀介质。

一种有效的方法是采用**[亥姆霍兹分解](@entry_id:181767) (Helmholtz decomposition)**，将位移场 $\boldsymbol{u}$ 分解为一个标量势 $\phi$ 的梯度和一个矢量势 $\boldsymbol{\psi}$ 的旋度之和：
$$
\boldsymbol{u} = \nabla\phi + \nabla \times \boldsymbol{\psi}
$$
其中矢量势满足[库仑规范](@entry_id:273044) $\nabla \cdot \boldsymbol{\psi} = 0$。将此分解代入动态[纳维-柯西方程](@entry_id:189211)，利用矢量恒等式，可以惊人地发现方程被解耦为两个独立的波动方程 ：
$$
(\lambda + 2\mu) \nabla^2\phi = \rho \frac{\partial^2 \phi}{\partial t^2} \quad \implies \quad \nabla^2\phi = \frac{1}{c_L^2} \frac{\partial^2 \phi}{\partial t^2}
$$
$$
\mu \nabla^2\boldsymbol{\psi} = \rho \frac{\partial^2 \boldsymbol{\psi}}{\partial t^2} \quad \implies \quad \nabla^2\boldsymbol{\psi} = \frac{1}{c_T^2} \frac{\partial^2 \boldsymbol{\psi}}{\partial t^2}
$$
第一个方程描述了**[纵波](@entry_id:172335) (longitudinal wave)** 或**[压缩波](@entry_id:747596) (P-wave)** 的传播，其质点[振动](@entry_id:267781)方向平行于波的传播方向。第二个方程描述了**[横波](@entry_id:269527) (transverse wave)** 或**剪切波 (S-wave)** 的传播，其[质点](@entry_id:186768)[振动](@entry_id:267781)方向垂直于[波的传播](@entry_id:144063)方向。

这两种波的相速度可以直接从方程中确定：
*   **纵波波速** $c_L$ (或 $c_p$)：$c_L = \sqrt{\frac{\lambda + 2\mu}{\rho}}$
*   **[横波](@entry_id:269527)[波速](@entry_id:186208)** $c_T$ (或 $c_s$)：$c_T = \sqrt{\frac{\mu}{\rho}}$

这个结果也可以通过假设一个平面谐波解 $\mathbf{u}(\mathbf{x},t)=\Re\{\mathbf{U}\exp(i(\mathbf{k}\cdot\mathbf{x}-\omega t))\}$ 并将其代入[纳维-柯西方程](@entry_id:189211)来获得。这会导出一个关于极化向量 $\mathbf{U}$ 的[代数特征值问题](@entry_id:169099)，其解同样揭示了两种截然不同的传播模式及其对应的波速 。

对于更一般的**各向异性 (anisotropic)** 材料，其[刚度张量](@entry_id:176588) $C_{ijkl}$ 不再具有简单的各向同性形式。此时，[波速](@entry_id:186208)将依赖于传播方向 $\boldsymbol{n}$。通过平面波分析，可以得到**[克里斯托费尔声学张量](@entry_id:186595) (Christoffel acoustic tensor)** $\boldsymbol{\Gamma}(\boldsymbol{n})$，其定义为 $\Gamma_{ik} = C_{ijkl}n_j n_l$。特征值问题 $\boldsymbol{\Gamma}\boldsymbol{p} = \rho c^2 \boldsymbol{p}$ 的解给出了在 $\boldsymbol{n}$ 方向上传播的三个波的[波速](@entry_id:186208) $c$ 和极化方向 $\boldsymbol{p}$。波速是真实的物理量，要求 $\rho c^2 > 0$，这意味着克里斯托费尔张量 $\boldsymbol{\Gamma}$ 必须是正定的。这个条件被称为**强椭圆性 (strong ellipticity)**，它是保证[弹性动力学](@entry_id:175818)方程[适定性](@entry_id:148590)的关键数学条件。对于[各向同性材料](@entry_id:170678)，强椭圆性条件简化为 $\mu > 0$ 和 $\lambda + 2\mu > 0$，这确保了剪切波和纵波的波速都是实数 。

值得注意的是，当材料性质并非均匀（例如 $\lambda(\boldsymbol{x}), \mu(\boldsymbol{x})$ 随空间变化）时，[亥姆霍兹分解](@entry_id:181767)将不再能完全[解耦](@entry_id:637294) P 波和 S 波。材料属性的梯度会引入耦合项，导致在一个地方产生的纯 P 波在传播到另一个地方时可能会激发出 S 波，反之亦然。这种现象被称为**波形转换 (mode conversion)** 。

#### 边值问题与[弱形式](@entry_id:142897)

在实际工程问题中，我们求解的是在特定几何域 $\Omega$ 内满足[纳维-柯西方程](@entry_id:189211)，并在其边界 $\partial\Omega$ 上满足给定条件的[位移场](@entry_id:141476)。这些边界条件通常分为两类：
1.  **[狄利克雷边界条件](@entry_id:173524) (Dirichlet boundary condition)**：在边界的一部分 $\Gamma_D$ 上规定位移，例如 $\boldsymbol{u} = \bar{\boldsymbol{u}}$。这也被称为**[本质边界条件](@entry_id:173524) (essential boundary condition)**。
2.  **[诺伊曼边界条件](@entry_id:142124) (Neumann boundary condition)**：在边界的另一部分 $\Gamma_N$ 上规定面力，例如 $\boldsymbol{t} = \boldsymbol{\sigma}\boldsymbol{n} = \bar{\boldsymbol{t}}$。这也被称为**自然边界条件 (natural boundary condition)**。

在同一边界部分同时规定位移和面力通常会使问题**超定 (over-determined)**，除非规定的面力恰好是满足位移条件所产生的反力 。

对于复杂的几何形状和边界条件，直接求解偏微分方程（即**强形式 (strong form)**）非常困难。现代计算力学，尤其是有限元方法，依赖于其等价的**[弱形式](@entry_id:142897) (weak form)** 或**[变分形式](@entry_id:166033) (variational form)**。

弱形式的推导始于将静态平衡方程乘以一个任意的**测试函数 (test function)** $\boldsymbol{v}$，并在整个求解域 $\Omega$ 上积分。然后利用[高斯散度定理](@entry_id:188065)（分部积分）来降低位移的求导阶数。对于静态问题 $-\nabla \cdot \boldsymbol{\sigma}(\boldsymbol{u}) = \boldsymbol{f}$，这个过程得到如下的[积分方程](@entry_id:138643)：
$$
\int_{\Omega} \boldsymbol{\sigma}(\boldsymbol{u}) : \boldsymbol{\varepsilon}(\boldsymbol{v}) \, d\Omega = \int_{\Omega} \boldsymbol{f} \cdot \boldsymbol{v} \, d\Omega + \int_{\Gamma_N} \bar{\boldsymbol{t}} \cdot \boldsymbol{v} \, d\Gamma
$$
该方程需要对所有满足特定条件的测试函数 $\boldsymbol{v}$ 成立。这里的冒号“$:$”表示张量的[双点积](@entry_id:748648)。

在[弱形式](@entry_id:142897)的构建中，边界条件的处理方式有所不同。[诺伊曼边界条件](@entry_id:142124)（面力）自然地出现在分部积分产生的边界积分项中，因此被称为“自然”边界条件。而狄利克雷边界条件（位移）则需要通过限制求解空间和测试[函数空间](@entry_id:143478)来强制施加。具体来说：
*   **[试探函数](@entry_id:756165) (trial function)** $\boldsymbol{u}$（即我们要求解的位移）必须属于一个[函数空间](@entry_id:143478)，该空间中的函数满足本质边界条件 $\boldsymbol{u} = \bar{\boldsymbol{u}}$ on $\Gamma_D$。
*   **测试函数 (test function)** $\boldsymbol{v}$ 必须属于一个相应的[线性空间](@entry_id:151108)，且在本质边界上为零，即 $\boldsymbol{v} = \boldsymbol{0}$ on $\Gamma_D$，以消除该边界上未知的反力项。

从数学上讲，这些函数空间通常是**索伯列夫空间 (Sobolev space)** $H^1(\Omega)$ 的[子集](@entry_id:261956)。因此，完整的弱形式问题陈述为：寻找 $\boldsymbol{u} \in V$ 使得上述[积分方程](@entry_id:138643)对所有 $\boldsymbol{v} \in V_0$ 成立，其中 $V=\{\boldsymbol{u}\in [H^1(\Omega)]^d \,|\, \boldsymbol{u}=\bar{\boldsymbol{u}} \text{ on } \Gamma_D\}$ 是[试探空间](@entry_id:756166)，而 $V_0=\{\boldsymbol{v}\in [H^1(\Omega)]^d \,|\, \boldsymbol{v}=\boldsymbol{0} \text{ on } \Gamma_D\}$ 是测试空间 。

#### 解的[适定性](@entry_id:148590)与唯一性

一个有意义的物理问题，其数学模型应具有**[适定性](@entry_id:148590) (well-posedness)**，即解存在、唯一且稳定地依赖于输入数据。对于弹性力学边值问题：
*   当狄利克雷边界 $\Gamma_D$ 的面积（或长度）大于零时，**[科恩不等式](@entry_id:174794) (Korn's inequality)** 保证了问题的解是唯一的。
*   当整个边界都是诺伊曼边界（即**纯[诺伊曼问题](@entry_id:176713)**，$\Gamma_D = \varnothing$）时，情况变得复杂。此时，任何刚体位移 $\boldsymbol{u}_{\text{RBM}}$（平移和无穷小转动）都会产生零应变和零应力，因此如果 $\boldsymbol{u}$ 是一个解，那么 $\boldsymbol{u} + \boldsymbol{u}_{\text{RBM}}$ 也是一个解。这意味着解不是唯一的，仅在相差一个刚体位移的意义下唯一 。

为了在纯[诺伊曼问题](@entry_id:176713)中获得唯一解，必须施加额外的约束来排除[刚体运动](@entry_id:193355)。首先，为了保证解的存在性，外载荷（[体力](@entry_id:174230) $\boldsymbol{f}$ 和面力 $\bar{\boldsymbol{t}}$）必须自身处于平衡状态，即总主矢和总主矩为零：
$$
\int_{\Omega} \boldsymbol{f}\, d\Omega + \int_{\Gamma_N} \bar{\boldsymbol{t}}\, d\Gamma = \boldsymbol{0}, \quad
\int_{\Omega} \boldsymbol{x} \times \boldsymbol{f}\, d\Omega + \int_{\Gamma_N} \boldsymbol{x} \times \bar{\boldsymbol{t}}\, d\Gamma = \boldsymbol{0}
$$
其次，必须通过附加约束来固定物体。例如，可以[固定域](@entry_id:155430)内某一点的位移和某另外一点的部分位移以防止转动，或者施加积分形式的约束，如要求解的平均位移和平均转动为零 ：
$$
\int_{\Omega} \boldsymbol{u}\, d\Omega = \boldsymbol{0}, \quad \int_{\Omega} \boldsymbol{x} \times \boldsymbol{u}\, d\Omega = \boldsymbol{0}
$$

### 高等原理与计算问题

除了基本的方程求解，弹性理论还包含一些深刻的原理，并引出重要的计算挑战。

#### [互易定理](@entry_id:267731)与[格林函数](@entry_id:147802)

**[贝蒂互易定理](@entry_id:200996) (Betti's reciprocal theorem)** 是线弹性理论中一个优雅而强大的原理。它指出，对于一个弹性体，由第一组载荷（[体力](@entry_id:174230) $\boldsymbol{b}^{(1)}$ 和面力 $\boldsymbol{t}^{(1)}$）在第二组载荷引起的[位移场](@entry_id:141476) $\boldsymbol{u}^{(2)}$ 上所做的功，等于由第二组载荷（体力 $\boldsymbol{b}^{(2)}$ 和面力 $\boldsymbol{t}^{(2)}$）在第一组载荷引起的位移场 $\boldsymbol{u}^{(1)}$ 上所做的功。其积分形式为：
$$
\int_{\Omega} \boldsymbol{b}^{(1)} \cdot \boldsymbol{u}^{(2)} dV + \int_{\partial\Omega} \boldsymbol{t}^{(1)} \cdot \boldsymbol{u}^{(2)} dS = \int_{\Omega} \boldsymbol{b}^{(2)} \cdot \boldsymbol{u}^{(1)} dV + \int_{\partial\Omega} \boldsymbol{t}^{(2)} \cdot \boldsymbol{u}^{(1)} dS
$$
这个定理源于[弹性刚度张量](@entry_id:170728) $\mathbb{C}$ 的主对称性 ($C_{ijkl}=C_{klij}$)。

[互易定理](@entry_id:267731)的一个重要应用是利用**基本解 (fundamental solution)** 或**[格林函数](@entry_id:147802) (Green's function)** 来求解问题。例如，考虑状态 (2) 是由在原点处沿 $x_1$ 方向施加的单位点力 $\boldsymbol{b}^{(2)}(\boldsymbol{x}) = \delta(\boldsymbol{x})\boldsymbol{e}_1$ 引起的位移场（即**[开尔文解](@entry_id:187869) (Kelvin solution)**）。利用狄拉克 $\delta$ 函数的性质，[互易定理](@entry_id:267731)可以转化为一个积分表达式，直接给出由任意[体力](@entry_id:174230)[分布](@entry_id:182848) $\boldsymbol{b}^{(1)}$ 在原点处引起的位移分量 $u_1^{(1)}(\boldsymbol{0})$。这不仅为复杂载荷问题提供了半解析解的途径，也为验证数值解（如有限元计算结果）的准确性提供了一个强有力的工具 。

#### 不可压缩极限与体积自锁

当材料的[泊松比](@entry_id:158876) $\nu$ 趋近于 $0.5$ 时，我们称之为**不可压缩极限 (incompressible limit)**。从关系式 $\lambda = E\nu/((1+\nu)(1-2\nu))$ 可以看出，此时拉梅参数 $\lambda \to \infty$。在物理上，这意味着材料抵[抗体](@entry_id:146805)积变化的能力变得无穷大。

从[变分原理](@entry_id:198028)的角度看，总势能 $\Pi_\lambda(\boldsymbol{u}) = \int_\Omega (\mu\,\|\boldsymbol{\varepsilon}(\boldsymbol{u})\|^2 + \frac{\lambda}{2}\,(\nabla\cdot \boldsymbol{u})^2)\,dx - \int_\Omega \boldsymbol{f}\cdot \boldsymbol{u}\,dx$ 要保持有限，当 $\lambda \to \infty$ 时，必须有 $(\nabla\cdot \boldsymbol{u})^2 \to 0$。这表明，在不可压缩极限下，[位移场](@entry_id:141476)必须满足[运动学](@entry_id:173318)约束 $\nabla\cdot \boldsymbol{u} = 0$，即体积应变为零。

这种极限行为给基于纯位移的[纳维-柯西方程](@entry_id:189211)带来了严重的数学和计算难题 ：
1.  **病态条件 (Ill-conditioning)**：随着 $\lambda$ 的增大，控制方程的刚度[矩阵的[条件](@entry_id:150947)数](@entry_id:145150)会以 $\mathcal{O}(\lambda)$ 的速度增长，导致数值求解变得极其不稳定和不准确。
2.  **体积自锁 (Volumetric locking)**：在[有限元离散化](@entry_id:193156)中，特别是使用低阶单元（如线性三角形或四面体）时，离散函数空间中能够满足 $\nabla\cdot \boldsymbol{u}_h \approx 0$ 的自由度非常有限。这导致任何微小的体积变形都会产生巨大的、非物理的惩罚能量项 $\frac{\lambda}{2}\int(\nabla\cdot \boldsymbol{u}_h)^2 dx$。其后果是，数值解被人为地“锁定”在几乎为零的状态，表现为系统刚度被严重高估，无法得到有意义的变形结果。

为了解决这个问题，需要放弃纯位移公式。一种标准方法是引入一个独立的**压[力场](@entry_id:147325) (pressure field)** $p$作为拉格朗日乘子来施加不可压缩约束 $\nabla\cdot \boldsymbol{u} = 0$。这导致了一个**混合公式 (mixed formulation)**，需求解 $(\boldsymbol{u}, p)$ 场。这种方法的稳定性由**LBB (Ladyzhenskaya–Babuška–Brezzi) 条件**保证，它要求位移和压力的有限元插值空间必须满足一定的相容性。在实践中，诸如“[减缩积分](@entry_id:167949)”或“选择性积分”等技术也是缓解体积自锁的有效策略 。