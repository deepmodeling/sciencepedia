## 引言
在固体力学和[材料科学](@entry_id:152226)领域，精确描述物体的变形是理解其力学行为的基石。当一个物体受力时，它内部的物[质点](@entry_id:186768)会发生移动，导致整体形状和尺寸的改变。然而，如何从复杂的[位移场](@entry_id:141476)中，严格地、定量地分离出真正引起[内力](@entry_id:167605)变化的“形状改变”（即应变）与不产生[内力](@entry_id:167605)的“刚体运动”？这正是[小应变运动学](@entry_id:192140)理论所要解决的核心知识缺口。该理论为分析工程结构和材料在小变形下的行为提供了一个简洁而强大的数学框架。

本文将带领您系统地掌握[小应变运动学](@entry_id:192140)的精髓。在第一章“原理和机制”中，我们将从位移场出发，严格定义[无穷小应变张量](@entry_id:167211)与转动张量，并阐明其物理意义及协调性条件。随后，在第二章“应用与跨学科联系”中，我们将探索这些基本原理如何在结构力学、实验力学、先进[材料建模](@entry_id:751724)乃至断裂力学中发挥关键作用，揭示理论与实践的紧密联系。最后，在第三章“动手实践”中，您将通过解决具体问题，将所学知识付诸实践，从而深化理解。学完本文，您将能够自信地运用[运动学](@entry_id:173318)原理来分析和诠释各种变形问题。

## 原理和机制

本章旨在系统地阐述[小应变运动学](@entry_id:192140)的基本原理和核心机制。我们将从[位移场](@entry_id:141476)出发，严格定义应变和转动，深入探讨其物理意义，并最终建立起确保[运动学](@entry_id:173318)协调性的数学框架。本章内容是后续章节中本构关系和[平衡方程](@entry_id:172166)的基础。

### [形变运动学](@entry_id:189142)：从位移到应变

连续介质力学的核心任务是描述物质点在空间和时间中的运动。我们首先考虑一个物体在其初始的、未变形的**参考构型 (reference configuration)** 中占据的空间区域 $\Omega$。该构型中的任意物[质点](@entry_id:186768)可以通过其位置向量 $\mathbf{X}$（称为**物质坐标**）来唯一标识。在力的作用下，物体发生形变，运动到一个新的**当前构型 (current configuration)**，该构型中的同一点的位置由向量 $\mathbf{x}$（称为**空间坐标**）描述。

将每个物[质点](@entry_id:186768)从其[参考位](@entry_id:754187)置映射到当前位置的函数，被称为**形变映射 (deformation mapping)** $\varphi$：
$$ \mathbf{x} = \varphi(\mathbf{X}) $$
为了保证物质的连续性和唯一性，$\varphi$ 必须是连续、可微且[几乎处处](@entry_id:146631)可逆的。

描述物质点位置变化的更直接的物理量是**位移场 (displacement field)** $\mathbf{u}$，它定义为当前位置与[参考位](@entry_id:754187)置之差：
$$ \mathbf{u}(\mathbf{X}) = \varphi(\mathbf{X}) - \mathbf{X} $$
位移场是描述形变的核心变量，因为它直接量化了每个点相对于其“起点”的移动。

为了从位移场中提取关于局部形变（即拉伸、压缩和剪切）的信息，我们需要考察位移在空间中的变化率。这由**[位移梯度张量](@entry_id:748571) (displacement gradient tensor)** $\mathbf{H}$ 来描述，其定义为位移场对物质坐标的梯度：
$$ \mathbf{H} = \nabla_{\mathbf{X}} \mathbf{u} $$
在[笛卡尔坐标系](@entry_id:169789)中，其分量形式为 $H_{ij} = \frac{\partial u_i}{\partial X_j}$。[位移梯度张量](@entry_id:748571)是连接位移与应变的关键。它与描述总形变的**[形变梯度张量](@entry_id:150370) (deformation gradient tensor)** $\mathbf{F} = \nabla_{\mathbf{X}} \varphi$ 之间存在简单的关系：
$$ \mathbf{F} = \nabla_{\mathbf{X}}(\mathbf{X} + \mathbf{u}) = \mathbf{I} + \nabla_{\mathbf{X}}\mathbf{u} = \mathbf{I} + \mathbf{H} $$
其中 $\mathbf{I}$ 是二阶单位张量。

在许多工程应用中，例如金属、[陶瓷](@entry_id:148626)和[复合材料](@entry_id:139856)在[弹性极限](@entry_id:186242)内的行为，位移及其梯度都非常小。这引出了**小应变假设 (small-strain assumption)**，其数学核心是假定**[位移梯度](@entry_id:165352)的范数远小于1**：
$$ \|\nabla_{\mathbf{X}}\mathbf{u}\| \ll 1 $$
这意味着[位移梯度](@entry_id:165352)的所有分量 $\partial u_i / \partial X_j$ 都是无量纲的小量。这个看似简单的假设带来了极大的简化。首先，它允许我们在计算中忽略[位移梯度](@entry_id:165352)的高阶项（例如二次项）。其次，由于 $\mathbf{u}$ 相对于物体的尺寸很小，当前坐标 $\mathbf{x}$ 和参考坐标 $\mathbf{X}$ 非常接近，即 $\mathbf{x} \approx \mathbf{X}$。这使得我们可以不严格区分对物质坐标的梯度 ($\nabla_{\mathbf{X}}$) 和对空间坐标的梯度 ($\nabla_{\mathbf{x}}$)，即 $\nabla_{\mathbf{X}} \approx \nabla_{\mathbf{x}}$。这个近似在小应变理论中被广泛采用，它极大地简化了控制方程的建立和求解 [@problem_id:2917823]。

### [无穷小应变张量](@entry_id:167211)和转动张量

[位移梯度张量](@entry_id:748571) $\mathbf{H}$ 包含了物体局部运动的全部信息，但这其中既包括了能引起[内力](@entry_id:167605)的真实形变（拉伸和剪切），也包括了不产生[内力](@entry_id:167605)的[刚体转动](@entry_id:191086)。为了将这两者分离开，我们可以利用任何一个[二阶张量](@entry_id:199780)都可以唯一地分解为一个对称[部分和](@entry_id:162077)一个反对称部分的数学性质 [@problem_id:2917798]。

我们将[位移梯度张量](@entry_id:748571) $\mathbf{H} = \nabla\mathbf{u}$（在小应变假设下，我们不再区分 $\nabla_{\mathbf{X}}$ 和 $\nabla_{\mathbf{x}}$）分解为：
$$ \nabla\mathbf{u} = \boldsymbol{\varepsilon} + \boldsymbol{\omega} $$
其中，
$$ \boldsymbol{\varepsilon} = \frac{1}{2}\left(\nabla\mathbf{u} + (\nabla\mathbf{u})^T\right) $$
是 $\nabla\mathbf{u}$ 的**对称部分**，定义为**[无穷小应变张量](@entry_id:167211) (infinitesimal strain tensor)**。
$$ \boldsymbol{\omega} = \frac{1}{2}\left(\nabla\mathbf{u} - (\nabla\mathbf{u})^T\right) $$
是 $\nabla\mathbf{u}$ 的**反对称部分**（或称斜对称部分），定义为**无穷小转动张量 (infinitesimal rotation tensor)**。

这个分解的意义是深刻的。**应变张量 $\boldsymbol{\varepsilon}$ 完全描述了物体的局部形状和尺寸的变化**，而**转动张量 $\boldsymbol{\omega}$ 则描述了物体的局部[刚体转动](@entry_id:191086)**。一个关键的物理原则是，纯刚体运动（平移和转动）不应产生应变，因为物体的内力状态不会因此改变。将应变定义为[位移梯度](@entry_id:165352)的对称部分恰好满足了这一要求。对于一个纯[刚体转动](@entry_id:191086)，其[位移梯度](@entry_id:165352)是一个[反对称张量](@entry_id:199349)，因此其对称部分 $\boldsymbol{\varepsilon}$ 恒为零 [@problem_id:2917861] [@problem_id:2917809]。

在三维[笛卡尔坐标系](@entry_id:169789) $(x, y, z)$ 中，位移场为 $\mathbf{u} = (u_x, u_y, u_z)$，[应变张量](@entry_id:193332) $\boldsymbol{\varepsilon}$ 的九个分量由下式给出 [@problem_id:2917861]：
- **[正应变](@entry_id:204633) (Normal Strains)**，描述沿坐标轴方向的伸长或缩短：
$$ \varepsilon_{xx} = \frac{\partial u_x}{\partial x}, \quad \varepsilon_{yy} = \frac{\partial u_y}{\partial y}, \quad \varepsilon_{zz} = \frac{\partial u_z}{\partial z} $$

- **[剪应变](@entry_id:175241) (Shear Strains)**，描述坐标轴之间夹角的变化：
$$ \varepsilon_{xy} = \varepsilon_{yx} = \frac{1}{2}\left(\frac{\partial u_x}{\partial y} + \frac{\partial u_y}{\partial x}\right) $$
$$ \varepsilon_{xz} = \varepsilon_{zx} = \frac{1}{2}\left(\frac{\partial u_x}{\partial z} + \frac{\partial u_z}{\partial x}\right) $$
$$ \varepsilon_{yz} = \varepsilon_{zy} = \frac{1}{2}\left(\frac{\partial u_y}{\partial z} + \frac{\partial u_z}{\partial y}\right) $$
由于其对称性 $\varepsilon_{ij} = \varepsilon_{ji}$，在三维空间中，[应变张量](@entry_id:193332)只有6个独立分量。

**示例**：考虑位移场 $\mathbf{u} = (0.02y + 0.01z, -0.02x + 0.03z, -0.01x + 0.02y)$。首先计算[位移梯度张量](@entry_id:748571)：
$$ \nabla\mathbf{u} = \begin{pmatrix} 0 & 0.02 & 0.01 \\ -0.02 & 0 & 0.03 \\ -0.01 & 0.02 & 0 \end{pmatrix} $$
其对称部分（[应变张量](@entry_id:193332)）为：
$$ \boldsymbol{\varepsilon} = \frac{1}{2}(\nabla\mathbf{u} + (\nabla\mathbf{u})^T) = \begin{pmatrix} 0 & 0 & 0 \\ 0 & 0 & 0.025 \\ 0 & 0.025 & 0 \end{pmatrix} $$
其反对称部分（转动张量）为：
$$ \boldsymbol{\omega} = \frac{1}{2}(\nabla\mathbf{u} - (\nabla\mathbf{u})^T) = \begin{pmatrix} 0 & 0.02 & 0.01 \\ -0.02 & 0 & 0.005 \\ -0.01 & -0.005 & 0 \end{pmatrix} $$
这个例子清楚地展示了如何从一个复杂的[位移场](@entry_id:141476)中分离出纯形变（由 $\boldsymbol{\varepsilon}$ 描述）和纯[刚体转动](@entry_id:191086)（由 $\boldsymbol{\omega}$ 描述） [@problem_id:2917798]。

### 应变分量的物理解释

为了更深入地理解[应变张量](@entry_id:193332)的含义，我们来探究其各个分量的具体物理意义。

**[正应变](@entry_id:204633)** $\varepsilon_{ii}$（无求和）代表沿 $i$ 轴方向的单位长度变化。例如，$\varepsilon_{xx}$ 表示一根最初沿 $x$ 轴的微小线段的相对伸长率。如果 $\varepsilon_{xx} > 0$，则线段被拉伸；如果 $\varepsilon_{xx}  0$，则线段被压缩。一个经典的例子是**[单轴拉伸](@entry_id:188287)**，其位移场为 $\mathbf{u} = (\epsilon_0 x_1, 0, 0)$。在这种情况下，应变张量只有一个非零分量 $\varepsilon_{11} = \epsilon_0$，清晰地对应于沿 $x_1$ 轴的拉伸 [@problem_id:2917847]。

**[剪应变](@entry_id:175241)** $\varepsilon_{ij}$ ($i \neq j$) 则与角度变化有关。它量化了两条最初分别平行于 $i$ 轴和 $j$ 轴的线段之间夹角的变化。在工程实践中，更常用的是**工程[剪应变](@entry_id:175241) (engineering shear strain)** $\gamma_{ij}$，其定义为 $\gamma_{ij} = 2\varepsilon_{ij}$。$\gamma_{ij}$ 的物理意义是两条材料线之间直角的减少量（以弧度计）。

例如，考虑一个最初位于 $x$ 轴和 $y$ 轴上的直角。变形后，这个直角变为 $\alpha$。那么，工程[剪应变](@entry_id:175241) $\gamma_{xy}$ 与角度变化 $\Delta\alpha = \alpha - \pi/2$ 的关系为 $\gamma_{xy} = -\Delta\alpha$。也就是说，正的工程[剪应变](@entry_id:175241)对应于直角的减小。我们可以通过一个**纯剪切**[位移场](@entry_id:141476) $u_x = \kappa y, u_y=0$ 来严格证明这一点。计算表明，两条坐标轴之间的角度变化恰好为 $\Delta\alpha = -\kappa$，而从位移场计算得到的工程[剪应变](@entry_id:175241)为 $\gamma_{xy} = \frac{\partial u_x}{\partial y} + \frac{\partial u_y}{\partial x} = \kappa$。这完美地验证了[剪应变](@entry_id:175241)的几何解释 [@problem_id:2917865]。

### 高级应变概念

#### [主应变](@entry_id:197797)和[主方向](@entry_id:276187)

应变张量 $\boldsymbol{\varepsilon}$ 是一个对称的[二阶张量](@entry_id:199780)，因此它总可以通过[坐标系](@entry_id:156346)的旋转[对角化](@entry_id:147016)。对角化后的[应变张量](@entry_id:193332)的对角元被称为**[主应变](@entry_id:197797) (principal strains)**，记为 $\varepsilon_1, \varepsilon_2, \varepsilon_3$。它们是[应变张量](@entry_id:193332) $\boldsymbol{\varepsilon}$ 的[特征值](@entry_id:154894)。对应的坐标轴方向被称为**主方向 (principal directions)**，它们是 $\boldsymbol{\varepsilon}$ 的[特征向量](@entry_id:151813)。

物理上，[主方向](@entry_id:276187)是指在某一点处，材料线段只发生伸缩而没有[剪切变形](@entry_id:170920)的方向。[主应变](@entry_id:197797)则代表了这些方向上的最大、最小和中间的[正应变](@entry_id:204633)值。在主方向构成的[坐标系](@entry_id:156346)中，[应变张量](@entry_id:193332)表示为：
$$ \boldsymbol{\varepsilon} = \begin{pmatrix} \varepsilon_1  0  0 \\ 0  \varepsilon_2  0 \\ 0  0  \varepsilon_3 \end{pmatrix} $$
这表明，任何复杂的应变状态在局部都可以被看作是三个相互垂直方向上的拉伸或压缩的叠加。在之前提到的[单轴拉伸](@entry_id:188287)例子中，坐标轴方向本身就是[主方向](@entry_id:276187)，[主应变](@entry_id:197797)分别为 $(\epsilon_0, 0, 0)$ [@problem_id:2917847]。

#### [体积应变和偏应变](@entry_id:197710)

为了更好地将应变与材料的两种基本响应——体积改变和形状改变——联系起来，我们可以将[应变张量](@entry_id:193332)进一步分解。

**体积应变 (volumetric strain)** $\varepsilon_v$ 定义为[应变张量](@entry_id:193332)的迹 (trace)，它等于三个[正应变](@entry_id:204633)之和：
$$ \varepsilon_v = \mathrm{tr}(\boldsymbol{\varepsilon}) = \varepsilon_{xx} + \varepsilon_{yy} + \varepsilon_{zz} $$
体积应变代表了材料微元的单位体积变化率。在小应变理论中，它近似等于[形变梯度](@entry_id:163749)的雅可比行列式 $J$ 减1，即 $\varepsilon_v \approx J - 1$。体积应变是应变张量的第一[不变量](@entry_id:148850)，这意味着它的大小不随[坐标系](@entry_id:156346)的旋转而改变 [@problem_id:2917866]。

将应变张量中引起体积变化的部分分离出去后，剩下的部分描述了纯粹的形状改变（畸变）。这通过将 $\boldsymbol{\varepsilon}$ 分解为一个**球形部分 (spherical part)** 和一个**偏斜部分 (deviatoric part)** 来实现：
$$ \boldsymbol{\varepsilon} = \boldsymbol{\varepsilon}_{\text{sph}} + \boldsymbol{\varepsilon}' $$
其中，球形部分 $\boldsymbol{\varepsilon}_{\text{sph}} = \frac{1}{3}\varepsilon_v \mathbf{I}$ 是一个各向同性的张量，它只引起体积变化。而**偏应变张量 (deviatoric strain tensor)** $\boldsymbol{\varepsilon}'$ 定义为：
$$ \boldsymbol{\varepsilon}' = \boldsymbol{\varepsilon} - \frac{1}{3}\varepsilon_v \mathbf{I} $$
偏[应变[张](@entry_id:193332)量的迹](@entry_id:190669)恒为零 ($\mathrm{tr}(\boldsymbol{\varepsilon}') = 0$)，这意味着它所描述的形变不伴随任何体积变化，完全是形状的扭曲。

这个分解在[材料科学](@entry_id:152226)中至关重要，因为许多材料（如金属）的塑性变形主要是由[偏应力](@entry_id:163323)驱动的形状改变，而体积变化则主要是弹性的。像[体积应变](@entry_id:267252)一样，偏应变张量的[标量不变量](@entry_id:193787)（如其第二和第三[不变量](@entry_id:148850)）在[坐标变换](@entry_id:172727)下也是不变的 [@problem_id:2917866]。

### 动力学和协调性

#### [应变率张量](@entry_id:266108)

当变形随时间变化时，我们需要引入率量来描述运动。**[应变率张量](@entry_id:266108) (strain rate tensor)**，也称为**变形率张量 (rate of deformation tensor)** $\mathbf{d}$，被定义为速度场 $\mathbf{v}$ 梯度的对称部分：
$$ \mathbf{d} = \frac{1}{2}\left(\nabla\mathbf{v} + (\nabla\mathbf{v})^T\right) $$
在小应变假设下，可以证明[应变率张量](@entry_id:266108)等于[无穷小应变张量](@entry_id:167211)对时间的物质导数，即 $\mathbf{d} = \dot{\boldsymbol{\varepsilon}}$。这个关系是建立[粘弹性](@entry_id:148045)或塑性等率相关本构模型的基础，它将当前的运动速率（通过 $\mathbf{d}$）与应变的历史演化（通过 $\dot{\boldsymbol{\varepsilon}}$）联系起来。与应变张量一样，应变率张量对于[刚体运动](@entry_id:193355)也为零，这意味着[刚体运动](@entry_id:193355)不会产生变形率 [@problem_id:2917882]。工程[剪应变率](@entry_id:189459) $\dot{\gamma}_{ij}$ 也与[应变率张量](@entry_id:266108)的分量相关，即 $\dot{\gamma}_{ij} = 2d_{ij}$ [@problem_id:2917882]。

#### 协调性条件

我们已经知道，一个给定的位移场 $\mathbf{u}$ 可以唯一地确定一个应变场 $\boldsymbol{\varepsilon}$。现在我们提出一个反向的问题：任意给定一个对称的[二阶张量](@entry_id:199780)场 $\boldsymbol{\varepsilon}(\mathbf{x})$，它是否总能对应于某个单值的、连续的位移场？

答案是否定的。因为[应变张量](@entry_id:193332)的6个独立分量是通过对[位移场](@entry_id:141476)的3个分量求导得来的，这6个分量之间必须满足一定的约束关系。这些约束关系被称为**圣维南协调性条件 (Saint-Venant compatibility conditions)**。

这些条件本质上要求应变场的[二阶导数](@entry_id:144508)之间存在特定的组合关系，从而保证通[过积分](@entry_id:753033)能够得到一个没有“裂缝”或“重叠”的单值位移场。在三维情况下，用[指标形式](@entry_id:183467)表示，协调性方程为：
$$ \varepsilon_{ij,kl} + \varepsilon_{kl,ij} - \varepsilon_{ik,jl} - \varepsilon_{jl,ik} = 0 $$
其中逗号表示对相应坐标的偏导数。这个[方程组](@entry_id:193238)包含了81个方程，但其中只有6个是独立的。

对于一个**单连通 (simply connected)** 的物体（即没有孔洞的物体），圣维南协调性条件是应变场能够积分得到一个单值[位移场](@entry_id:141476)的充分必要条件 [@problem_id:2917863]。如果物体是多连通的（例如一个环），则还需要满足额外的积分条件。协调性条件在[断裂力学](@entry_id:141480)、[位错理论](@entry_id:160051)以及从实验测量的应变数据重构[位移场](@entry_id:141476)等领域具有重要意义。

### 小应变框架的有效性和局限性

小应变理论的基石是[位移梯度](@entry_id:165352)足够小，即 $\|\nabla\mathbf{u}\| \ll 1$。理解这一假设的后果和局限性至关重要。

当不采用小应变假设时，应变的精确度量由**[格林-拉格朗日应变张量](@entry_id:187745) (Green-Lagrange strain tensor)** $\mathbf{E}$ 给出：
$$ \mathbf{E} = \frac{1}{2}(\mathbf{F}^T\mathbf{F} - \mathbf{I}) = \frac{1}{2}(\nabla\mathbf{u} + (\nabla\mathbf{u})^T + (\nabla\mathbf{u})^T\nabla\mathbf{u}) $$
比较 $\mathbf{E}$ 和[无穷小应变张量](@entry_id:167211) $\boldsymbol{\varepsilon}$，我们发现它们之间的误差项为：
$$ \mathbf{E} - \boldsymbol{\varepsilon} = \frac{1}{2}(\nabla\mathbf{u})^T\nabla\mathbf{u} $$
这是一个关于[位移梯度](@entry_id:165352)的二次项。小应变理论的本质就是忽略这个二次项。因此，该理论的有效性直接取决于这个二次项是否可以忽略不计。

我们可以更严格地分析这个误差。使用矩阵的[2-范数](@entry_id:636114)（[谱范数](@entry_id:143091)），误差的大小可以被界定为：
$$ \|\mathbf{E} - \boldsymbol{\varepsilon}\|_2 = \frac{1}{2}\|(\nabla\mathbf{u})^T\nabla\mathbf{u}\|_2 = \frac{1}{2}\|\nabla\mathbf{u}\|_2^2 $$
这个关系明确地表明，要保证线性化带来的误差在一个可接受的范围内，就必须保证[位移梯度](@entry_id:165352)的范数足够小 [@problem_id:2917870]。

值得强调的是，$\|\nabla\mathbf{u}\| \ll 1$ 不仅要求应变 $\boldsymbol{\varepsilon}$ 很小，还要求转动 $\boldsymbol{\omega}$ 也很小。如果存在大转动，即使应变为零，小应变理论也会产生谬误。考虑一个绕 $z$ 轴的[刚体转动](@entry_id:191086)，角度为 $\theta$。这是一个零应变的运动。然而，如果我们用精确的[位移场](@entry_id:141476)代入[无穷小应变](@entry_id:197162)的公式，会得到一个虚假的、非零的[应变张量](@entry_id:193332)，其分量约为 $-\theta^2/2$ [@problem_id:2917809]。这个例子生动地说明了，当转动不可忽略时（即使角度 $\theta$ 只是中等大小），小应变理论就会失效。

因此，[小应变运动学](@entry_id:192140)框架的[适用范围](@entry_id:636189)被严格限定在**小应变**和**小转动**同时满足的场合。在遇到大转动问题（如柔性梁的弯曲）或[大应变](@entry_id:751152)问题（如[金属塑性](@entry_id:176585)成型）时，必须采用更精确的[有限应变理论](@entry_id:176941)。