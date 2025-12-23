## 引言
在固体力学领域，能量原理提供了一种超越传统力平衡分析的深刻而优雅的视角。它将系统的行为归结为一个标量泛函——总势能——的最小化问题，从而将复杂的矢量和张量方程转化为更为直观的[变分问题](@entry_id:756445)。然而，从抽象的[变分原理](@entry_id:198028)到解决实际工程问题的计算工具，其间存在着理论与实践的鸿沟。本文旨在系统性地架起这座桥梁，为读者提供一个关于保守系统能量原理的完整知识体系。

在接下来的内容中，我们将分三个章节展开探讨。首先，在 **“原理与机制”** 一章中，我们将深入剖析能量原理的理论核心，从总[势能](@entry_id:748988)泛函的构建，到[势能](@entry_id:748988)驻值原理的数学表述，再到其与[有限元法](@entry_id:749389)中[切线刚度矩阵](@entry_id:170852)和[稳定性分析](@entry_id:144077)的内在联系。接着，在 **“应用与跨学科连接”** 一章中，我们将展示这些原理如何作为通用工具，应用于结构静力学、[断裂力学](@entry_id:141480)、[材料科学](@entry_id:152226)和前沿的机器人设计等多个领域。最后，通过 **“动手实践”** 部分，读者将有机会将理论知识应用于具体的计算问题，从而巩固对核心概念的理解。通过这一结构化的学习路径，本文将引导您掌握[计算固体力学](@entry_id:169583)中这一基石性的理论。

## 原理与机制

在保守系统中，能量原理为分析和求解固体力学问题提供了强大而优雅的框架。其核心思想是，一个保守力学系统的平衡状态对应于其总[势能](@entry_id:748988)的驻值点。这一看似简单的陈述蕴含着深刻的物理内涵，并构成了现代[计算力学](@entry_id:174464)，特别是[有限元法](@entry_id:749389)（FEM）的理论基石。本章将系统地阐述[保守系统](@entry_id:167760)的能量原理、其在计算中的应用机制，以及其更深层次的理论基础。

### 总[势能](@entry_id:748988)泛函的构建

对于一个保守系统，其全部信息可以被编码在一个称为**总势能泛函**（total potential energy functional）的标量函数 $\Pi$ 中。这个泛函是系统位形（由[位移场](@entry_id:141476) $\mathbf{u}$ 描述）的函数，其结构可分解为两个主要部分：系统的**内部储存能**（internal stored energy）$U$ 和**外加载荷[势能](@entry_id:748988)**（potential energy of external loads）$V_{\text{ext}}$。

$$
\Pi(\mathbf{u}) = U(\mathbf{u}) + V_{\text{ext}}(\mathbf{u})
$$

#### 内部储存能

内部储存能代表了系统因变形而储存的能量。对于弹性体，这主要是应变能。

- **弹性应变能**：对于一个占据区域 $\Omega$ 的超弹性体，其应变能通过对**[应变能密度](@entry_id:200085)**（strain energy density）$W$ 在整个体积上积分得到。在小应变理论中，[应变能密度](@entry_id:200085)是[应变张量](@entry_id:193332) $\boldsymbol{\varepsilon}$ 的函数，$\boldsymbol{\varepsilon}(\mathbf{u}) = \frac{1}{2}(\nabla \mathbf{u} + \nabla \mathbf{u}^{\top})$。对于[线性弹性](@entry_id:166983)材料，该密度函数是一个二次型：

  $$
  W(\boldsymbol{\varepsilon}) = \frac{1}{2} \boldsymbol{\varepsilon} : \mathbb{C} : \boldsymbol{\varepsilon}
  $$

  其中 $\mathbb{C}$ 是[四阶弹性张量](@entry_id:188318)。因此，物体的总[应变能](@entry_id:162699)为：

  $$
  U_{\text{body}}(\mathbf{u}) = \int_{\Omega} W(\boldsymbol{\varepsilon}(\mathbf{u})) \, \mathrm{d}\Omega = \int_{\Omega} \frac{1}{2} \boldsymbol{\varepsilon}(\mathbf{u}) : \mathbb{C} : \boldsymbol{\varepsilon}(\mathbf{u}) \, \mathrm{d}\Omega
  $$

  在有限变形理论中，[应变能密度](@entry_id:200085)是变形梯度 $\mathbf{F} = \mathbf{I} + \nabla \mathbf{u}$ 的函数，即 $W(\mathbf{F})$ 。储存能总是对总势能做出正贡献，因为它代表了变形所“消耗”并储存在材料内部的能量。

- **其他弹性元件的储存能**：系统中任何其他能够储存和释放能量的保守元件也会对总储存能有贡献。一个典型的例子是[弹性地基](@entry_id:186539)。如果物体在边界 $\Gamma_s$ 上附着于一个线[弹性地基](@entry_id:186539)（可视为一个[分布](@entry_id:182848)式的弹簧场，称为[Winkler地基](@entry_id:184939)），其反作用力密度为 $\mathbf{t}_s = -k_s \mathbf{u}$，其中 $k_s$ 是地基刚度密度。该地基储存的[势能](@entry_id:748988)为：

  $$
  U_{\text{foundation}}(\mathbf{u}) = \int_{\Gamma_s} \frac{1}{2} k_s (\mathbf{u} \cdot \mathbf{u}) \, \mathrm{d}\Gamma
  $$

  这个能量项同样是正的，因为它在变形时储存能量 。

#### 外加载荷势能

外加载荷势能来源于外力在物体变形过程中所做的功。对于**保守载荷**（conservative loading），外力所做的功与变形路径无关，仅取决于初始和最终位形。这使得我们可以定义一个势能函数。在变分力学中，这一定义更为精确：如果外力[虚功](@entry_id:176403) $\delta W_{\text{ext}}$ 可以表示为某个[标量势](@entry_id:276177) $\Pi_{\text{ext}}$ 的负[一次变分](@entry_id:174697)，即 $\delta W_{\text{ext}} = -\delta \Pi_{\text{ext}}$，则该载荷是保守的 。

最常见的一类保守载荷是**死载荷**（dead loads），其大小和方向在变形过程中保持不变。对于死载荷，其[势能](@entry_id:748988)就是它所做功的负值，$V_{\text{ext}} = -W_{\text{ext}}$。

- **体力势能**：作用于体积 $\Omega$ 内的[体力](@entry_id:174230)密度 $\mathbf{f}$ 所做的功为 $\int_{\Omega} \mathbf{f} \cdot \mathbf{u} \, \mathrm{d}\Omega$。其[势能](@entry_id:748988)为：

  $$
  V_f(\mathbf{u}) = - \int_{\Omega} \mathbf{f} \cdot \mathbf{u} \, \mathrm{d}\Omega
  $$

- **面力[势能](@entry_id:748988)**：作用于边界 $\Gamma_t$ 上的给定面力密度 $\bar{\mathbf{t}}$ 所做的功为 $\int_{\Gamma_t} \bar{\mathbf{t}} \cdot \mathbf{u} \, \mathrm{d}\Gamma$。其[势能](@entry_id:748988)为：

  $$
  V_t(\mathbf{u}) = - \int_{\Gamma_t} \bar{\mathbf{t}} \cdot \mathbf{u} \, \mathrm{d}\Gamma
  $$

- **集中力[势能](@entry_id:748988)**：作用于某一点 $\mathbf{x}_P$ 的集中力 $\mathbf{P}$ 所做的功为 $\mathbf{P} \cdot \mathbf{u}(\mathbf{x}_P)$。其势能为：

  $$
  V_P(\mathbf{u}) = - \mathbf{P} \cdot \mathbf{u}(\mathbf{x}_P)
  $$

需要注意的是，外力势能项通常在总势能泛函中带有负号，因为外力做正功会降低系统的总[势能](@entry_id:748988)。

综合以上各项，一个承受体力、面力、集中力并由[弹性地基](@entry_id:186539)支撑的[线性弹性](@entry_id:166983)体的总势能泛函可以写为 ：

$$
\Pi(\mathbf{u}) = \underbrace{\int_{\Omega} \frac{1}{2} \boldsymbol{\varepsilon}(\mathbf{u}):\mathbb{C}:\boldsymbol{\varepsilon}(\mathbf{u}) \, \mathrm{d}\Omega + \int_{\Gamma_s} \frac{1}{2} k_s \mathbf{u} \cdot \mathbf{u} \, \mathrm{d}\Gamma}_{U(\mathbf{u})} \underbrace{- \int_{\Omega} \mathbf{f} \cdot \mathbf{u} \, \mathrm{d}\Omega - \int_{\Gamma_t} \bar{\mathbf{t}} \cdot \mathbf{u} \, \mathrm{d}\Gamma - \mathbf{P} \cdot \mathbf{u}(\mathbf{x}_P)}_{V_{\text{ext}}(\mathbf{u})}
$$

### 势能驻值原理

构建了总[势能](@entry_id:748988)泛函后，下一步是利用它来寻找平衡。**[最小势能原理](@entry_id:173340)**（Principle of Minimum Potential Energy）或更广义的**势能驻值原理**（Principle of Stationary Potential Energy）指出：

> 在所有满足给定运动学约束的位形中，使保守系统处于平衡的位形是那些使其总势能泛函 $\Pi(\mathbf{u})$ 取驻值（stationary value）的位形。

#### 变分、[函数空间](@entry_id:143478)与边界条件

“驻值”是一个微积分概念，意味着泛函的一阶变分为零。为了严谨地定义变分，我们需要引入合适的函数空间。[位移场](@entry_id:141476) $\mathbf{u}$ 必须足够光滑，以确保应变能积分有意义。这通常要求[位移场](@entry_id:141476)属于**[索博列夫空间](@entry_id:141995)**（Sobolev space），如 $H^1(\Omega)$，该空间包含平方可积及其一阶[弱导数](@entry_id:189356)也平方可积的函数。

- **容许位移空间**（Admissible Displacement Space）$\mathcal{U}_g$：包含所有满足给定**本质边界条件**（essential boundary conditions）的、[运动学](@entry_id:173318)上可能的位移场。[本质边界条件](@entry_id:173524)通常是位移约束，例如在边界 $\Gamma_u$ 上规定了位移 $\mathbf{u} = \bar{\mathbf{u}}$。因此，

  $$
  \mathcal{U}_g = \left\{ \mathbf{u} \in [H^1(\Omega)]^d \,\middle|\, \gamma(\mathbf{u}) = \bar{\mathbf{u}} \text{ on } \Gamma_u \right\}
  $$
  其中 $\gamma$ 是将体内函数映射到边界值的[迹算子](@entry_id:183665) 。

- **容许变分空间**（Admissible Variation Space）$\mathcal{V}_0$：也称为[检验函数](@entry_id:166589)空间。如果 $\mathbf{u}$ 是一个容许位移，那么 $\mathbf{u} + \epsilon \mathbf{w}$（其中 $\epsilon$ 是一个小参数，$\mathbf{w}$ 是一个[虚位移](@entry_id:168781)）也必须是容许的。这意味着变分 $\mathbf{w}$ 必须满足对应的齐次本质边界条件，即 $\mathbf{w} = \mathbf{0}$ on $\Gamma_u$。

  $$
  \mathcal{V}_0 = \left\{ \mathbf{w} \in [H^1(\Omega)]^d \,\middle|\, \gamma(\mathbf{w}) = \mathbf{0} \text{ on } \Gamma_u \right\}
  $$

驻值条件于是被 formal 地写为：寻找 $\mathbf{u} \in \mathcal{U}_g$，使得对于所有 $\mathbf{w} \in \mathcal{V}_0$：

$$
\delta \Pi(\mathbf{u}; \mathbf{w}) = \left. \frac{\mathrm{d}}{\mathrm{d}\epsilon} \Pi(\mathbf{u} + \epsilon \mathbf{w}) \right|_{\epsilon=0} = 0
$$

这个方程被称为系统的**[弱形式](@entry_id:142897)**（weak form）或**虚功原理**（Principle of Virtual Work）。

#### [本质边界条件与自然边界条件](@entry_id:146051)

能量原理巧妙地区分了两类边界条件。如上所述，**[本质边界条件](@entry_id:173524)**（essential boundary conditions）是那些必须预先施加于函数空间（即[试探函数](@entry_id:756165)空间）上的约束，以确保[变分问题](@entry_id:756445)的[适定性](@entry_id:148590)。在位移法中，[位移边界条件](@entry_id:203261)是本质的。

相反，**自然边界条件**（natural boundary conditions）是那些作为变分过程的 *结果* 而自动满足的条件。在位移法中，力边界条件是自然的。我们可以通过对弱形式进行分部积分（即应用[格林公式](@entry_id:173118)或散度定理）来揭示这一点 。以线性弹性体为例，$\delta\Pi=0$ 给出：

$$
\int_{\Omega} \boldsymbol{\sigma}(\mathbf{u}) : \boldsymbol{\varepsilon}(\mathbf{w}) \, \mathrm{d}\Omega - \int_{\Omega} \mathbf{b} \cdot \mathbf{w} \, \mathrm{d}\Omega - \int_{\Gamma_t} \bar{\mathbf{t}} \cdot \mathbf{w} \, \mathrm{d}\Gamma = 0
$$

利用散度定理和应力[张量的对称性](@entry_id:202126)，第一项可以变换为：

$$
\int_{\Omega} \boldsymbol{\sigma} : \nabla\mathbf{w} \, \mathrm{d}\Omega = \int_{\partial\Omega} (\boldsymbol{\sigma}\mathbf{n}) \cdot \mathbf{w} \, \mathrm{d}\Gamma - \int_{\Omega} (\nabla \cdot \boldsymbol{\sigma}) \cdot \mathbf{w} \, \mathrm{d}\Omega
$$

代入弱形式并整理，得到：

$$
-\int_{\Omega} (\nabla \cdot \boldsymbol{\sigma} + \mathbf{b}) \cdot \mathbf{w} \, \mathrm{d}\Omega + \int_{\Gamma_t} (\boldsymbol{\sigma}\mathbf{n} - \bar{\mathbf{t}}) \cdot \mathbf{w} \, \mathrm{d}\Gamma + \int_{\Gamma_u} (\boldsymbol{\sigma}\mathbf{n}) \cdot \mathbf{w} \, \mathrm{d}\Gamma = 0
$$

由于 $\mathbf{w} \in \mathcal{V}_0$，它在 $\Gamma_u$ 上为零，所以第三个积分自动消失。根据[变分法](@entry_id:163656)基本引理，既然剩下的方程对任意在 $\Omega$ 内部和 $\Gamma_t$ 上不为零的 $\mathbf{w}$ 都成立，那么两个被积函数必须为零：
1.  $\nabla \cdot \boldsymbol{\sigma} + \mathbf{b} = \mathbf{0}$ 在 $\Omega$ 内（平衡方程）。
2.  $\boldsymbol{\sigma}\mathbf{n} = \bar{\mathbf{t}}$ 在 $\Gamma_t$ 上（力边界条件）。

由此可见，力边界条件是从[变分原理](@entry_id:198028)中“自然”产生的，而[位移边界条件](@entry_id:203261)则必须预先作为对[解空间](@entry_id:200470)的“本质”约束来施加。

### 稳定性、极小化与[凸性](@entry_id:138568)

驻值原理找到了所有可能的[平衡点](@entry_id:272705)，但这并未区分它们是稳定的、不稳定的还是临界的。

- **[驻点](@entry_id:136617) vs. 极小点**：一个[平衡点](@entry_id:272705)是**稳定**的，如果它对应于总[势能](@entry_id:748988)的[局部极小值](@entry_id:143537)。[驻点](@entry_id:136617)可以是极小值点、极大值点或[鞍点](@entry_id:142576) 。
- **二阶变分**：要判断一个[驻点](@entry_id:136617) $\mathbf{u}$是否为[局部极小值](@entry_id:143537)，我们需要考察总势能的**二阶变分**（second variation）。对于稳定的平衡，二阶变分必须是非负的：
  $$
  \delta^2 \Pi(\mathbf{u}; \mathbf{w}, \mathbf{w}) = \left. \frac{\mathrm{d}^2}{\mathrm{d}\epsilon^2} \Pi(\mathbf{u} + \epsilon \mathbf{w}) \right|_{\epsilon=0} \ge 0 \quad \forall \mathbf{w} \in \mathcal{V}_0
  $$
- **[凸性](@entry_id:138568)**：如果总势能泛函 $\Pi(\mathbf{u})$ 是**凸**（convex）的，那么任何驻点都是[全局最小值](@entry_id:165977)点。对于线性弹性问题，如果[弹性张量](@entry_id:170728) $\mathbb{C}$ 是正定的，那么[应变能](@entry_id:162699)是严格凸的。由于外力势能是线性的，总[势能](@entry_id:748988)泛函 $\Pi(\mathbf{u})$ 也是严格凸的。在这种情况下，[平衡解](@entry_id:174651)是唯一的，并且是稳定的。然而，在有限变形的[非线性](@entry_id:637147)[超弹性](@entry_id:159356)问题中，$W(\mathbf{F})$ 可能不是凸函数，这可能导致多个[平衡解](@entry_id:174651)和失稳现象（如[屈曲](@entry_id:162815)）。

### [计算力学](@entry_id:174464)中的实现：有限元法

能量原理为[有限元法](@entry_id:749389)提供了坚实的理论基础。其核心思想是将连续的[位移场](@entry_id:141476)用离散的节点位移向量 $\mathbf{d}$ 和形函数 $\mathbf{N}$ 来近似：$\mathbf{u}(\mathbf{X}) \approx \mathbf{N}(\mathbf{X})\mathbf{d}$。

代入总势能泛函 $\Pi(\mathbf{u})$，它就变成了一个关于节点位移向量 $\mathbf{d}$ 的普通[多元函数](@entry_id:145643) $\Pi(\mathbf{d})$。

- **离散平衡方程**：驻值条件 $\delta\Pi=0$ 转化为对 $\mathbf{d}$ 的梯度为零：
  $$
  \frac{\partial \Pi(\mathbf{d})}{\partial \mathbf{d}} = \mathbf{R}(\mathbf{d}) = \mathbf{0}
  $$
  这里的向量 $\mathbf{R}(\mathbf{d})$ 被称为**[残差向量](@entry_id:165091)**（residual vector），它表示在当前位形 $\mathbf{d}$ 下的节点[不平衡力](@entry_id:753019)。$\mathbf{R}(\mathbf{d}) = \mathbf{F}_{\text{int}}(\mathbf{d}) - \mathbf{F}_{\text{ext}}$，其中 $\mathbf{F}_{\text{int}}$ 是[内力向量](@entry_id:750751)，$\mathbf{F}_{\text{ext}}$ 是外力向量。

- **[切线刚度矩阵](@entry_id:170852)**：二阶变分则对应于 $\Pi(\mathbf{d})$ 的**Hessian矩阵**，这正是**[切线刚度矩阵](@entry_id:170852)**（tangent stiffness matrix）$\mathbf{K}_t$：
  $$
  \mathbf{K}_t(\mathbf{d}) = \frac{\partial^2 \Pi(\mathbf{d})}{\partial \mathbf{d}^2} = \frac{\partial \mathbf{R}(\mathbf{d})}{\partial \mathbf{d}}
  $$
  [切线刚度矩阵](@entry_id:170852)的对称性源于能量泛函的Hessian矩阵的对称性，这是保守系统的固有特性。其[正定性](@entry_id:149643)则直接关系到[平衡解的稳定性](@entry_id:171720) 。

#### 牛顿-拉夫逊法与稳定性

非线性方程组 $\mathbf{R}(\mathbf{d}) = \mathbf{0}$ 通常采用**牛顿-拉夫逊法**（[Newton-Raphson](@entry_id:177436) method）求解。在第 $k$ 次迭代中，求解线性方程组来获得位移增量 $\Delta\mathbf{d}_{k+1}$：
$$
\mathbf{K}_t(\mathbf{d}_k) \Delta\mathbf{d}_{k+1} = - \mathbf{R}(\mathbf{d}_k)
$$
然后更新位移：$\mathbf{d}_{k+1} = \mathbf{d}_k + \alpha_k \Delta\mathbf{d}_{k+1}$。

- **下降方向**：如果[切线刚度矩阵](@entry_id:170852) $\mathbf{K}_t$ 是**对称正定**（Symmetric Positive Definite, SPD）的，那么牛顿法计算出的搜索方向 $\Delta\mathbf{d}$ 就是一个**下降方向**（descent direction），即它保证了在当前点附近，沿着该方向移动会减小总势能 $\Pi$ 。
- **载荷的贡献**：死载荷的势能是位移的线性函数。因此，它们对残差（[一阶导数](@entry_id:749425)）有贡献，但对[切线刚度矩阵](@entry_id:170852)（[二阶导数](@entry_id:144508)）的贡献为零 。这解释了为什么在标准的[牛顿法](@entry_id:140116)中，只有材料和[几何非线性](@entry_id:169896)才贡献于[切线刚度矩阵](@entry_id:170852)的变化。
- **线搜索**：为了保证[全局收敛](@entry_id:635436)，通常会引入**线搜索**（line search）来确定步长 $\alpha_k$。[Armijo条件](@entry_id:169106)等准则确保每一步都实现势能的充分下降。当迭代接近一个势能的局部极小点（即稳定[平衡点](@entry_id:272705)）时，$\mathbf{K}_t$ 是正定的，牛顿法会表现出二次收敛性，并且通常会接受完整的步长 $\alpha_k=1$ 。

### [对偶原理](@entry_id:276615)：[余能](@entry_id:192009)

除了基于位移和应变的势能原理，还存在一系列**[对偶原理](@entry_id:276615)**（dual principles），它们使用力或应力作为基本变量。其中最重要的是**[最小余能原理](@entry_id:200382)**（Principle of Minimum Complementary Energy）。

- **余能密度**：对于[应变能密度](@entry_id:200085)为 $W(\boldsymbol{\varepsilon})$ 的材料，其**[余能](@entry_id:192009)密度**（complementary energy density）$W^*(\boldsymbol{\sigma})$ 通过**[勒让德变换](@entry_id:146727)**（Legendre transform）定义：
  $$
  W^*(\boldsymbol{\sigma}) = \sup_{\boldsymbol{\varepsilon}} (\boldsymbol{\sigma}:\boldsymbol{\varepsilon} - W(\boldsymbol{\varepsilon}))
  $$
  这个变换将能量函数的[自变量](@entry_id:267118)从应变 $\boldsymbol{\varepsilon}$ 转换为了应力 $\boldsymbol{\sigma}$。为了使这个变换是良定义且可逆的，[应变能密度](@entry_id:200085) $W(\boldsymbol{\varepsilon})$ 必须是**严格凸**的。在这种情况下，[本构关系](@entry_id:186508) $\boldsymbol{\sigma} = \partial W / \partial \boldsymbol{\varepsilon}$ 是可逆的，其[逆关系](@entry_id:274206)由[余能](@entry_id:192009)密度给出：$\boldsymbol{\varepsilon} = \partial W^* / \partial \boldsymbol{\sigma}$ 。

- **[最小余能原理](@entry_id:200382)**：该原理陈述如下：

  > 在所有满足[平衡方程](@entry_id:172166)和力边界条件的**静力容许应[力场](@entry_id:147325)**（statically admissible stress fields）中，真实的应[力场](@entry_id:147325)使总余能泛函 $\Pi^*$ 取最小值。

  对于[线性弹性](@entry_id:166983)体，总[余能](@entry_id:192009)泛函为：
  $$
  \Pi^*[\boldsymbol{\sigma}] = \int_{\Omega} W^*(\boldsymbol{\sigma}) \, \mathrm{d}\Omega - \int_{\Gamma_u} (\boldsymbol{\sigma}\mathbf{n}) \cdot \bar{\mathbf{u}} \, \mathrm{d}S
  $$
  该原理为发展基于应力的有限元法和应力杂交元法提供了理论基础。一个经典的应用是利用**[艾里应力函数](@entry_id:191331)**（Airy stress function）$\phi$ 来求解平面问题。[艾里应力函数](@entry_id:191331)自动满足[平衡方程](@entry_id:172166)，通过选择合适的[试探函数](@entry_id:756165)并最小化总余能，可以得到问题的近似解 。

### 深层基础：[对称性与守恒律](@entry_id:160300)

能量原理的背后是更深刻的物理定律，这些定律可以通过**诺特定理**（Noether's Theorem）与物理空间的对称性联系起来。在动力学框架下，系统的行为由作用量 $S = \int \mathcal{L} \, dt$ 的平稳性决定，其中拉格朗日量 $\mathcal{L} = T - U$ 是动能与[势能](@entry_id:748988)之差。

- **空间平移不变性**：如果系统的[拉格朗日量](@entry_id:174593)在空间平移变换（$\boldsymbol{\varphi} \to \boldsymbol{\varphi} + \mathbf{c}$）下保持不变，那么诺特定理保证系统的**总线动量**守恒。其局域形式正是我们熟悉的[动量平衡](@entry_id:193575)方程（即牛顿第二定律的连续介质形式）：$\rho_0 \ddot{\boldsymbol{\varphi}} = \text{Div}_X \mathbf{P}$ 。

- **空间[旋转不变性](@entry_id:137644)**：如果系统的拉格朗日量在空间[旋转变换](@entry_id:200017)（$\boldsymbol{\varphi} \to \mathbf{Q}\boldsymbol{\varphi}$）下保持不变（这与材料的**客观性**（objectivity）原理紧密相关），那么诺特定理保证系统的**[总角动量](@entry_id:155748)**守恒。这一守恒律的局域形式要求**柯西[应力张量](@entry_id:148973)**（Cauchy stress tensor）$\boldsymbol{\sigma}$ 是对称的，即 $\boldsymbol{\sigma} = \boldsymbol{\sigma}^T$ 。

这些联系揭示了能量原理不仅仅是求解问题的便捷工具，更是根本物理对称性在[连续介质力学](@entry_id:155125)中的具体体现。

综上所述，能量原理为我们理解和模拟保守力学系统提供了一个完整而自洽的理论体系。从构建[势能](@entry_id:748988)泛函，到通过[变分原理](@entry_id:198028)导出平衡方程和边界条件，再到通过二阶变分判断稳定性，以及最终将其离散化为可计算的有限元模型，每一步都植根于清晰的物理和数学原理。对这些原理的深刻理解，是进行高级[计算力学](@entry_id:174464)分析与研究的关键。