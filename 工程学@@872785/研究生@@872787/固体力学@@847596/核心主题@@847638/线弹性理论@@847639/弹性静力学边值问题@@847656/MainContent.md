## 引言
[弹性静力学](@entry_id:198298)边值问题是[固体力学](@entry_id:164042)领域的基石，它提供了一个强大的数学框架，用于预测弹性体在外部载荷作用下的内部应力、应变和位移。无论是设计一座桥梁、一架飞机，还是理解[复合材料](@entry_id:139856)的微观行为，其核心都离不开对这些[边值问题](@entry_id:193901)的精确求解。然而，学习者常常面临将零散的力学概念（如应力、应变、[胡克定律](@entry_id:149682)）整合成一个完整、自洽的分析框架的挑战。如何系统地建立一个适定的[边值问题](@entry_id:193901)，理解不同提法（强形式与[弱形式](@entry_id:142897)）的内涵，并将其应用于解决横跨不同学科的实际问题，是本文章旨在解决的核心知识缺口。

为了系统性地构建这一知识体系，本文将分为三个核心部分。我们首先在“**原理与机制**”一章中，从[应力与应变](@entry_id:137374)的基本定义出发，建立[本构关系](@entry_id:186508)，完整地表述边值问题，并探讨[解的唯一性](@entry_id:143619)及[圣维南原理](@entry_id:165302)等高级概念。随后，在“**应用与[交叉](@entry_id:147634)学科联系**”一章中，我们将展示该理论在工程、[材料科学](@entry_id:152226)及[断裂力学](@entry_id:141480)中的实际应用，并连接到[有限元法](@entry_id:749389)等现代计算方法。最后，“**动手实践**”部分将提供具体的计算问题，让读者在实践中巩固理论知识。通过这一结构化的学习路径，本文旨在帮助读者不仅掌握理论，更能融会贯通，将之应用于解决复杂的科学与工程挑战。

## 原理与机制

本章旨在系统性地阐述[弹性静力学](@entry_id:198298)[边值问题](@entry_id:193901)的核心原理与基本机制。我们将从[应力与应变](@entry_id:137374)的基本定义出发，构建线弹性[本构关系](@entry_id:186508)，进而完整地表述一个边值问题。在此基础上，我们将探讨弱形式、[解的唯一性](@entry_id:143619)、[圣维南原理](@entry_id:165302)以及二维简化等高级主题，为理解和求解[弹性静力学](@entry_id:198298)问题奠定坚实的理论基础。

### 应力状态与平衡

在[连续介质力学](@entry_id:155125)中，物体内部的相互作用力通过**应力 (stress)** 的概念来描述。考虑物体内部一个假想的微小[截面](@entry_id:154995)，其法向为[单位向量](@entry_id:165907) $\boldsymbol{n}$，该[截面](@entry_id:154995)上单位面积所受到的力定义为**[面力矢量](@entry_id:189429) (traction vector)** $\boldsymbol{t}(\boldsymbol{n})$。

#### 柯西应力原理

[面力矢量](@entry_id:189429)的性质由经典的**柯西应力原理 (Cauchy's Stress Principle)** 所刻画。该原理的核心思想是，在给定点 $\boldsymbol{x}$，[面力矢量](@entry_id:189429) $\boldsymbol{t}$ 仅依赖于该点的空间位置和[截面](@entry_id:154995)的法向 $\boldsymbol{n}$，而与[截面](@entry_id:154995)的具体形状和大小无关。通过对一个无限小的四面体进行力平衡分析（即柯西四面体论证），可以证明[面力矢量](@entry_id:189429) $\boldsymbol{t}(\boldsymbol{n})$ 与法向量 $\boldsymbol{n}$ 之间存在线性关系。这一线性关系确保了在每一点都存在一个[二阶张量](@entry_id:199780)，即**柯西应力张量 (Cauchy stress tensor)** $\boldsymbol{\sigma}(\boldsymbol{x})$，使得：

$$
\boldsymbol{t}(\boldsymbol{n}) = \boldsymbol{\sigma}(\boldsymbol{x})\boldsymbol{n}
$$

这便是柯西公式，它将描述某点应力状态的张量 $\boldsymbol{\sigma}$ 与作用在任意方向[截面](@entry_id:154995)上的力 $\boldsymbol{t}$ 联系起来。根据牛顿第三定律（作用力与[反作用](@entry_id:203910)力定律），作用在法向为 $-\boldsymbol{n}$ 的[截面](@entry_id:154995)上的[面力矢量](@entry_id:189429)与作用在法向为 $\boldsymbol{n}$ [截面](@entry_id:154995)上的[面力矢量](@entry_id:189429)大小相等、方向相反，即 $\boldsymbol{t}(-\boldsymbol{n}) = -\boldsymbol{t}(\boldsymbol{n})$ [@problem_id:2620357]。值得强调的是，应力是基于[力平衡](@entry_id:267186)公理建立的基本动力学概念，其定义不依赖于[位移场](@entry_id:141476)或变形的存在 [@problem_id:2620357]。

#### 应力[张量的对称性](@entry_id:202126)

在经典（非极性）连续介质理论中，若不考虑体力偶和面力偶的[分布](@entry_id:182848)，角动量守恒定律要求柯西应力张量必须是对称的，即：

$$
\boldsymbol{\sigma} = \boldsymbol{\sigma}^{\top} \quad \text{或} \quad \sigma_{ij} = \sigma_{ji}
$$

这一性质极大地简化了[应力分析](@entry_id:168804)，因为它将一个[二阶张量](@entry_id:199780)中独立的未知分量从9个减少到6个。应力[张量的对称性](@entry_id:202126)是弹性理论的基石之一，在推导本构关系和[虚功原理](@entry_id:138749)时起着至关重要的作用 [@problem_id:2620357] [@problem_id:2620334]。

#### [局部平衡](@entry_id:156295)方程

除了[角动量守恒](@entry_id:156798)，线动量守恒（或在静力学中，[力平衡](@entry_id:267186)）必须在物体的每一部分都得到满足。将力平衡条件应用于一个无限小的控制体，可以得到描述应[力场](@entry_id:147325)在空间中变化的[偏微分方程](@entry_id:141332)，即**[局部平衡](@entry_id:156295)方程 (local equilibrium equations)**：

$$
\nabla \cdot \boldsymbol{\sigma} + \boldsymbol{b} = \boldsymbol{0} \quad \text{或} \quad \frac{\partial \sigma_{ij}}{\partial x_j} + b_i = 0
$$

其中 $\boldsymbol{b}$ 是单位体积所受的**[体力](@entry_id:174230) (body force)**，例如重力。这个方程也被称为柯西第一运动定律的静态形式。

### 变形与应变

为了描述物体的变形，我们引入**位移场 (displacement field)** $\boldsymbol{u}(\boldsymbol{x})$，它表示物体中物[质点](@entry_id:186768)从参考构型到当前构型的位移。

#### [位移梯度](@entry_id:165352)及其分解

[位移场](@entry_id:141476)的梯度 $\nabla \boldsymbol{u}$ 是一个二阶张量，它包含了关于局部变形和转动的全部信息。根据极分解定理，任何可逆的变形梯度都可以分解为一个[拉伸张量](@entry_id:193200)和一个[旋转张量](@entry_id:191990)的乘积。在线性理论（小变形假设）中，这种分解简化为加法分解。[位移梯度](@entry_id:165352)可以唯一地分解为其对称部分和反对称部分 [@problem_id:2620352]：

$$
\nabla \boldsymbol{u} = \frac{1}{2}(\nabla \boldsymbol{u} + (\nabla \boldsymbol{u})^{\top}) + \frac{1}{2}(\nabla \boldsymbol{u} - (\nabla \boldsymbol{u})^{\top})
$$

#### [无穷小应变张量](@entry_id:167211)

[位移梯度](@entry_id:165352)的对称部分定义为**[无穷小应变张量](@entry_id:167211) (infinitesimal strain tensor)** $\boldsymbol{\varepsilon}$：

$$
\boldsymbol{\varepsilon}(\boldsymbol{u}) = \frac{1}{2}(\nabla \boldsymbol{u} + (\nabla \boldsymbol{u})^{\top})
$$

[应变张量](@entry_id:193332)是一个描述物体局部变形（形状和尺寸变化）的纯运动学量。其对角分量 $\varepsilon_{ii}$ 代表沿坐标轴方向的线应变（伸长或缩短），非对角分量 $\varepsilon_{ij}$ ($i \neq j$) 代表剪切应变（初始正交线段夹角的变化）[@problem_id:2620352]。需要注意的是，应变和应力是两个截然不同的物理量；将两者混淆是一个根本性的错误。它们之间的关系由材料的本构行为决定。

#### 无穷小转动张量

[位移梯度](@entry_id:165352)的反对称部分定义为**无穷小转动张量 (infinitesimal rotation tensor)** $\boldsymbol{W}$：

$$
\boldsymbol{W}(\boldsymbol{u}) = \frac{1}{2}(\nabla \boldsymbol{u} - (\nabla \boldsymbol{u})^{\top})
$$

该张量描述了物质微元的**[刚体转动](@entry_id:191086) (rigid-body rotation)**。由于它不引起物质点之间相对距离的一阶变化，因此在经典[弹性理论](@entry_id:184142)中，它既不产生应力，也不储存弹性能量。因此，[应力张量](@entry_id:148973)和[应变能密度函数](@entry_id:755490)仅依赖于[位移梯度](@entry_id:165352)的对称部分，即应变张量 [@problem_id:2620352]。

### 本构关系：线弹性

**本构关系 (constitutive relation)** 描述了材料的力学响应，即[应力与应变](@entry_id:137374)之间的关系。对于弹性材料，这种关系是可逆的。

#### [广义胡克定律](@entry_id:203555)与[弹性张量](@entry_id:170728)

对于线弹性材料，在小变形假设下，[应力与应变](@entry_id:137374)之间呈[线性关系](@entry_id:267880)，这被称为**[广义胡克定律](@entry_id:203555) (Generalized Hooke's Law)**：

$$
\sigma_{ij} = C_{ijkl} \varepsilon_{kl}
$$

其中 $C_{ijkl}$ 是四阶**[弹性张量](@entry_id:170728) (elasticity tensor)** 的分量。由于 $\sigma_{ij}$ 和 $\varepsilon_{kl}$ 分别有6个独立分量，[弹性张量](@entry_id:170728)在最一般的情况下（各向异性）最多可以有 $36$ 个独立常数。

[弹性张量](@entry_id:170728)具有特定的对称性，这些对称性源于物理原理 [@problem_id:2620334]：
1.  **次对称性 (Minor Symmetries)**：由于[应力张量和应变张量](@entry_id:755512)都是对称的（$\sigma_{ij}=\sigma_{ji}$, $\varepsilon_{kl}=\varepsilon_{lk}$），可以证明[弹性张量](@entry_id:170728)必须满足 $C_{ijkl} = C_{jikl}$ 和 $C_{ijkl} = C_{ijlk}$。
2.  **主对称性 (Major Symmetry)**：如果材料是**[超弹性](@entry_id:159356)的 (hyperelastic)**，即存在一个[应变能密度函数](@entry_id:755490) $W(\boldsymbol{\varepsilon})$，使得 $\boldsymbol{\sigma} = \frac{\partial W}{\partial \boldsymbol{\varepsilon}}$，则[弹性张量](@entry_id:170728)还必须满足主对称性 $C_{ijkl} = C_{klij}$。对于线弹性材料，$W$ 是应变的二次函数，即 $W = \frac{1}{2} C_{ijkl} \varepsilon_{ij} \varepsilon_{kl}$，主对称性自然成立。

这些对称性将各向异性线弹性材料的独立常数从36个减少到21个。

#### [各向同性线弹性](@entry_id:185899)

对于**各向同性 (isotropic)** 材料，其力学性质不随方向改变。这意味着[弹性张量](@entry_id:170728) $C_{ijkl}$ 在任意[坐标旋转](@entry_id:164444)下必须保持不变。满足此条件的[四阶张量](@entry_id:181350)的一般形式只有两个独立的材料常数。这使得[本构关系](@entry_id:186508)可以被写成一个更简洁的形式，通常用**拉梅参数 (Lamé parameters)** $\lambda$ 和 $\mu$ 来表示 [@problem_id:2620334] [@problem_id:2620352]：

$$
\boldsymbol{\sigma} = \lambda (\text{tr}(\boldsymbol{\varepsilon})) \boldsymbol{I} + 2\mu \boldsymbol{\varepsilon}
$$

其中 $\boldsymbol{I}$ 是二阶单位张量，$\text{tr}(\boldsymbol{\varepsilon}) = \varepsilon_{kk}$ 是[体积应变](@entry_id:267252)。参数 $\mu$ 也被称为**剪切模量 (shear modulus)**。这两个常数与其他常见的弹性常数如[杨氏模量](@entry_id:140430) $E$ 和泊松比 $\nu$ 密切相关。

### [边值问题](@entry_id:193901)的提法

一个完整的[弹性静力学](@entry_id:198298)边值问题 (BVP) 由三组基本方程构成：[平衡方程](@entry_id:172166)、[几何方程](@entry_id:173321)（[应变-位移关系](@entry_id:173321)）和[本构方程](@entry_id:138559)。这组方程定义了物体内部的物理行为。为了得到唯一解，还必须指定物体边界上的条件。

#### 边界条件

边界条件描述了物体与其周围环境的相互作用。最基本的两种边界条件是 [@problem_id:2620390]：
1.  **[位移边界条件](@entry_id:203261) (Displacement Boundary Conditions)**：在边界的一部分 $\Gamma_u$ 上，位移被指定为已知函数 $\bar{\boldsymbol{u}}$。这被称为**[本质边界条件](@entry_id:173524) (essential boundary condition)** 或狄利克雷 (Dirichlet) 型条件。
    $$
    \boldsymbol{u}(\boldsymbol{x}) = \bar{\boldsymbol{u}}(\boldsymbol{x}) \quad \text{for } \boldsymbol{x} \in \Gamma_u
    $$

2.  **[面力边界条件](@entry_id:167112) (Traction Boundary Conditions)**：在边界的另一部分 $\Gamma_t$ 上，面力被指定为已知函数 $\bar{\boldsymbol{t}}$。这被称为**自然边界条件 (natural boundary condition)** 或诺伊曼 (Neumann) 型条件。利用柯西公式，该条件可写为：
    $$
    \boldsymbol{\sigma}(\boldsymbol{x})\boldsymbol{n}(\boldsymbol{x}) = \bar{\boldsymbol{t}}(\boldsymbol{x}) \quad \text{for } \boldsymbol{x} \in \Gamma_t
    $$
    其中 $\boldsymbol{n}$ 是边界上的外法向单位向量。

在实际问题中，也常遇到**[混合边界条件](@entry_id:176456) (mixed boundary conditions)**，例如在无[摩擦接触](@entry_id:749595)面上，法向位移为零，而切向面力为零。

#### 强形式提法

综上所述，[弹性静力学](@entry_id:198298)[边值问题](@entry_id:193901)的**强形式 (strong form)** 或经典提法是：求解一个位移场 $\boldsymbol{u}(\boldsymbol{x})$，使其满足：
- 在区域 $\Omega$ 内部的平衡方程：$\nabla \cdot \boldsymbol{\sigma}(\boldsymbol{u}) + \boldsymbol{b} = \boldsymbol{0}$
- 在边界 $\Gamma_u$ 上的位移条件：$\boldsymbol{u} = \bar{\boldsymbol{u}}$
- 在边界 $\Gamma_t$ 上的面力条件：$\boldsymbol{\sigma}(\boldsymbol{u})\boldsymbol{n} = \bar{\boldsymbol{t}}$

其中应力 $\boldsymbol{\sigma}$ 和应变 $\boldsymbol{\varepsilon}$ 通过本构和几何关系与 $\boldsymbol{u}$ 联系。

### [弱形式](@entry_id:142897)与虚功原理

强形式提法要求解具有足够的连续性和可微性，这在许多物理情境（如含尖角或集中力的物体）中过于严苛。**弱形式 (weak formulation)** 或变分提法放宽了对解的[光滑性](@entry_id:634843)要求，并为有限元等数值方法的建立提供了理论基础。

弱形式可以通过**虚功原理 (Principle of Virtual Work)** 导出。其基本思想是，如果一个物体处于平衡状态，那么对于任何满足[运动学](@entry_id:173318)约束的、无限小的**[虚位移](@entry_id:168781) (virtual displacement)** $\delta\boldsymbol{u}$，外力所做的总[虚功](@entry_id:176403)等于[内力](@entry_id:167605)所做的总[虚功](@entry_id:176403)。

从[平衡方程](@entry_id:172166)的强形式出发，将其与一个任意的[虚位移](@entry_id:168781)场 $\delta\boldsymbol{u}$ 做[内积](@entry_id:158127)，并在整个区域 $\Omega$ 上积分。通过应用散度定理和边界条件，可以得到如下积分恒等式 [@problem_id:2620331]：

$$
\int_{\Omega} \boldsymbol{\sigma}(\boldsymbol{u}) : \boldsymbol{\varepsilon}(\delta\boldsymbol{u})\, dx = \int_{\Omega} \boldsymbol{b} \cdot \delta\boldsymbol{u}\, dx + \int_{\Gamma_t} \bar{\boldsymbol{t}} \cdot \delta\boldsymbol{u}\, ds
$$

该方程必须对所有满足齐次本质边界条件（即在 $\Gamma_u$ 上为零）的[虚位移](@entry_id:168781) $\delta\boldsymbol{u}$ 成立。左边是**[内虚功](@entry_id:172278) (internal virtual work)**，右边是**外[虚功](@entry_id:176403) (external virtual work)**。

在现代数学框架下，求解[弱形式](@entry_id:142897)问题需要引入合适的**[函数空间](@entry_id:143478) (function spaces)**。通常，我们寻找的解 $\boldsymbol{u}$ 和[虚位移](@entry_id:168781) $\delta\boldsymbol{u}$ 都属于索博列夫空间 $H^1(\Omega)^d$。具体地，解 $\boldsymbol{u}$ 属于满足非齐次[位移边界条件](@entry_id:203261)的**容许位移空间 (kinematically admissible space)** $V$，而[虚位移](@entry_id:168781) $\delta\boldsymbol{u}$ 属于满足相应齐次[位移边界条件](@entry_id:203261)的**[检验函数](@entry_id:166589)空间 (test function space)** $V_0$ [@problem_id:2620331]：
- **[试探空间](@entry_id:756166) (Trial Space)**: $V = \{ \boldsymbol{v} \in H^1(\Omega)^d : \boldsymbol{v} = \bar{\boldsymbol{u}} \text{ on } \Gamma_u \}$
- **检验空间 (Test Space)**: $V_0 = \{ \boldsymbol{v} \in H^1(\Omega)^d : \boldsymbol{v} = \boldsymbol{0} \text{ on } \Gamma_u \}$

[弱形式](@entry_id:142897)的提法变为：寻找 $\boldsymbol{u} \in V$，使得上述积分恒等式对所有 $\delta\boldsymbol{u} \in V_0$ 成立。

### [解的唯一性](@entry_id:143619)、存在性与[适定性](@entry_id:148590)

一个边值问题的**[适定性](@entry_id:148590) (well-posedness)** 通常指解的存在性、唯一性以及对数据的稳定性。在线性[弹性静力学](@entry_id:198298)中，唯一性问题与**刚体位移 (rigid-body motions)** 密切相关。

一个刚体位移是指不产生任何应变的位移场，其一般形式为 $\boldsymbol{r}(\boldsymbol{x}) = \boldsymbol{a} + \boldsymbol{W}\boldsymbol{x}$，其中 $\boldsymbol{a}$ 是一个常数平移向量，$\boldsymbol{W}$ 是一个常数[反对称张量](@entry_id:199349)（代表无穷小转动）。由于 $\boldsymbol{\varepsilon}(\boldsymbol{r}) = \boldsymbol{0}$，刚体位移不会产生应力，因此也不会改变平衡方程或[面力边界条件](@entry_id:167112)。

#### 唯一性分析

假设存在两个不同的解 $\boldsymbol{u}_1$ 和 $\boldsymbol{u}_2$。它们的差 $\boldsymbol{w} = \boldsymbol{u}_1 - \boldsymbol{u}_2$ 必然满足齐次的控制方程和边界条件。通过能量方法可以证明，$\boldsymbol{w}$ 对应的[应变能](@entry_id:162699)必须为零，这意味着 $\boldsymbol{\varepsilon}(\boldsymbol{w})=\boldsymbol{0}$。因此，两个解的差必定是一个刚体位移 [@problem_id:2620386]。

解是否唯一，取决于边界条件能否排除所有非零的刚体位移：
- 如果位移边界 $\Gamma_u$ 的面积（或在二维中的长度）大于零，即 $\mathcal{H}^{d-1}(\Gamma_u) > 0$，那么任何满足 $\boldsymbol{r}(\boldsymbol{x}) = \boldsymbol{0}$ on $\Gamma_u$ 的刚体位移 $\boldsymbol{r}$ 都必须是零位移。在这种情况下，刚体运动被完全约束，解是唯一的 [@problem_id:2620386]。
- 如果是**纯面力问题 (pure traction problem)**，即 $\Gamma_u = \emptyset$，边界条件无法约束任何刚体位移。因此，解只能在相差一个任意刚体位移的意义下是唯一的。换句话说，解在商空间 $H^1(\Omega)^d / \mathcal{R}$ 中是唯一的，其中 $\mathcal{R}$ 是刚体位移空间 [@problem_id:2620386] [@problem_id:2620335]。

#### 纯面力问题的约束

对于纯面力问题，首先，为了保证**存在性 (existence)**，施加的外部载荷（体力 $\boldsymbol{b}$ 和面力 $\bar{\boldsymbol{t}}$）必须处于**全局平衡 (global equilibrium)** 状态，即总合力和总[合力矩](@entry_id:166772)必须为零 [@problem_id:2620390]：
$$
\int_{\Omega} \boldsymbol{b}\, dV + \int_{\partial \Omega} \bar{\boldsymbol{t}}\, dS = \boldsymbol{0}, \quad \int_{\Omega} \boldsymbol{x}\times \boldsymbol{b}\, dV + \int_{\partial \Omega} \boldsymbol{x}\times \bar{\boldsymbol{t}}\, dS = \boldsymbol{0}
$$
其次，为了得到一个**唯一 (unique)** 的位移解，必须施加额外的约束来消除刚体位移的任意性。这些约束不应改变问题的物理本质（即应[力场](@entry_id:147325)）。常见的约[束方法](@entry_id:636307)包括 [@problem_id:2620386] [@problem_id:2620335]：
- **[固定点](@entry_id:156394)位移**: 在某些点上指定位移。例如，固定一个点的位移可以消除三个平移自由度，但不能消除绕该点的转动。需要更多的约束来完全消除刚体位移。
- **积分约束**: 施加关于位移场和转动场的积分约束。例如，以下两组约束都足以确保唯一性：
  1.  令全域的平均位移和平均转动为零：
      $$
      \int_{\Omega} \boldsymbol{u}\, dV = \boldsymbol{0} \quad \text{和} \quad \int_{\Omega} \text{skw}(\nabla \boldsymbol{u})\, dV = \boldsymbol{0}
      $$
  2.  或者，如果坐标原点位于[形心](@entry_id:265015)，可以要求平均位移和平均角动量为零：
      $$
      \int_{\Omega} \boldsymbol{u}\, dV = \boldsymbol{0} \quad \text{和} \quad \int_{\Omega} \boldsymbol{x} \times \boldsymbol{u}\, dV = \boldsymbol{0}
      $$

### 高级原理与简化模型

除了上述基本框架，一些高级原理和简化模型在弹性力学分析中也扮演着重要角色。

#### Beltrami-Michell 相容性方程

通常，弹性问题是通过求解[位移场](@entry_id:141476)来解决的（位移法）。然而，也存在一种直接求解应[力场](@entry_id:147325)的方法（应力法）。为此，需要一组只包含应力分量的控制方程。这可以通过将[平衡方程](@entry_id:172166)、本构关系与**[应变相容性](@entry_id:199659)方程 (strain compatibility equations)** 相结合来实现。

对于无体力的[各向同性线弹性](@entry_id:185899)体，最终得到的方程被称为 **Beltrami-Michell 相容性方程** [@problem_id:2620369]：
$$
\nabla^2 \boldsymbol{\sigma} + \frac{1}{1+\nu} \nabla \nabla (\text{tr}(\boldsymbol{\sigma})) = \boldsymbol{0}
$$
在推导此方程的过程中，可以证明应力张量的迹 $\text{tr}(\boldsymbol{\sigma})$ 是一个调和函数，即 $\nabla^2(\text{tr}(\boldsymbol{\sigma})) = 0$。因此，上述方程可简化为：
$$
\sigma_{ij,kk} + \frac{1}{1+\nu} \sigma_{mm,ij} = 0
$$
这组方程确保了从它们求解出的应[力场](@entry_id:147325)所对应的应变场是协调的，即可以积分得到一个单值的连续[位移场](@entry_id:141476)。

#### [圣维南原理](@entry_id:165302)

**[圣维南原理](@entry_id:165302) (Saint-Venant's Principle)** 是一个在工程应用中极其重要的近似原理。它指出，如果将作用在物体一小块区域上的载荷替换为另一组静态等效（即具有相同的[合力](@entry_id:163825)和[合力矩](@entry_id:166772)）的载荷，那么这种替换对远离载荷作用区的应力[分布](@entry_id:182848)影响很小 [@problem_id:2620378]。

- **定性表述**: 载荷[分布](@entry_id:182848)的局部细节只会影响其附近区域的应[力场](@entry_id:147325)。在远离载荷作用区的地方，应[力场](@entry_id:147325)主要由载荷的[合力](@entry_id:163825)和[合力矩](@entry_id:166772)决定。
- **定量表述**: 对于一个半无限长的棱柱体，如果其端部作用着一组自平衡（即合力与[合力矩](@entry_id:166772)均为零）的载荷，那么由这组载荷引起的应[力场](@entry_id:147325)和[应变能](@entry_id:162699)将随着离端部距离的增加而**指数衰减 (exponentially decay)**。衰减率由棱柱体[横截面](@entry_id:154995)的几何形状和材料性质决定，并与一个相关[算子的谱](@entry_id:272027)隙（第一个正[特征值](@entry_id:154894)）有关 [@problem_id:2620378]。

#### 二维简化模型

对于具有特定几何形状和载荷条件的三维弹性问题，可以合理地简化为二维问题进行分析，从而大大降低求解的复杂性。最常见的两种二维模型是平面应力和平面应变 [@problem_id:2620365]。

- **[平面应力](@entry_id:172193) (Plane Stress)**: 适用于薄板类结构，其厚度远小于平面尺寸，且在垂直于板面的方向上没有载荷。其基本假设是垂直于板面的应力分量可以忽略不计：
  $$
  \sigma_{zz} = \sigma_{xz} = \sigma_{yz} = 0
  $$
  尽管应力为零，但由于[泊松效应](@entry_id:158876)，垂直于板面的应变 $\varepsilon_{zz}$ 通常不为零。一个典型的例子是受到面[内载荷](@entry_id:195654)的薄板，其上下表面是自由的 [@problem_id:2620365]。

- **平面应变 (Plane Strain)**: 适用于沿某一方向很长的棱柱体结构（如大坝、隧道），且载荷和几何形状在该方向上保持不变。其基本假设是垂直于分析平面的应变分量为零：
  $$
  \varepsilon_{zz} = \varepsilon_{xz} = \varepsilon_{yz} = 0
  $$
  为了维持 $\varepsilon_{zz}=0$ 的约束，通常需要产生一个不为零的法向应力 $\sigma_{zz} = \nu(\sigma_{xx} + \sigma_{yy})$ 来抵抗泊松效应。一个典型的例子是一个在厚度方向上被刚性夹板约束的薄板 [@problem_id:2620365]。

选择哪种模型取决于结构的几何特征以及在厚度方向上的边界约束条件，而非仅仅是厚度本身。