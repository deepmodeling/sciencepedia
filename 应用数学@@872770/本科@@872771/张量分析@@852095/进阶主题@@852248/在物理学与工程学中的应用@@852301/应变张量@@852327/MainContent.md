## 引言
在连续介质力学中，理解和量化物体的变形是分析其力学行为的基础。应变张量正是为此而生的核心数学工具，它提供了一种严谨的方式来描述材料内部各点之间相对位置的变化。然而，一个物体的运动可能既包含使其形状和大小改变的真实变形，也包含不产生内应力的整体平移和旋转。核心的挑战在于如何从总位移中精确地分离出纯粹的变形部分。[应变张量](@entry_id:193332)的建立正是为了解决这一关键问题。

本文将系统地引导您深入理解[应变张量](@entry_id:193332)。在“原理与机制”一章中，我们将从[位移场](@entry_id:141476)出发，详细推导无限[小应变张量](@entry_id:754968)的定义，阐释其各个分量的物理意义，并探讨其分解、不变性及物理真实性条件。随后的“应用与跨学科联系”一章将展示应变张量如何在固体力学、[流体动力学](@entry_id:136788)、[材料科学](@entry_id:152226)及计算力学等多个领域中发挥关键作用。最后，“动手实践”部分将通过具体问题，帮助您巩固理论知识并将其应用于实际计算中。

## 原理与机制

在上一章中，我们介绍了连续介质力学的基本框架，并确立了描述物体运动与变形的必要性。本章将深入探讨变形的定量描述，引入一个核心的数学工具——**应变张量**（Strain Tensor）。我们将从其定义出发，系统地揭示其各个分量的物理意义，并探讨其在描述体积改变与形状扭曲中的作用。此外，我们还将区分真正的变形与不产生应变的[刚体运动](@entry_id:193355)，并讨论一个应变场要成为物理上可能存在的场所必须满足的内在约束。

### 从位移到应变：无限[小应变张量](@entry_id:754968)的定义

当一个连续介质物体受力变形时，其内部的每个点都会从初始位置 $\vec{X}$ 移动到一个新的空间位置 $\vec{x}$。这个过程可以用**[位移矢量场](@entry_id:196067)** $\vec{u}(\vec{X}) = \vec{x} - \vec{X}$ 来描述。然而，位移本身并不能完全刻画变形，因为它也包含了物体的整体平移和旋转。真正的变形，指的是物体内部各点之间的相对位置变化，即材料纤维的拉伸、收缩或彼此间角度的改变。

描述这种相对位置变化的关键在于**[位移梯度张量](@entry_id:748571)**（Displacement Gradient Tensor），记作 $\nabla \vec{u}$，其分量形式为 $\frac{\partial u_i}{\partial x_j}$。这个二阶张量包含了关于局部变形（拉伸与剪切）和局部刚体旋转的全部信息。为了分离出纯粹的变形部分，我们可以利用[张量分解](@entry_id:173366)的数学技巧。任何一个张量都可以分解为一个[对称张量](@entry_id:148092)和一个[反对称张量](@entry_id:199349)之和：

$$
\frac{\partial u_i}{\partial x_j} = \frac{1}{2} \left( \frac{\partial u_i}{\partial x_j} + \frac{\partial u_j}{\partial x_i} \right) + \frac{1}{2} \left( \frac{\partial u_i}{\partial x_j} - \frac{\partial u_j}{\partial x_i} \right)
$$

其中，对称部分描述了介质的变形，而反对称部分则与介质的刚性转动相关。

在**[小变形理论](@entry_id:174991)**（Small Deformation Theory）的框架下——即位移和[位移梯度](@entry_id:165352)都足够小——我们可以定义**无限[小应变张量](@entry_id:754968)**（Infinitesimal Strain Tensor），记作 $\boldsymbol{\epsilon}$，它正是位移梯度[张量的对称部分](@entry_id:182434)：

$$
\epsilon_{ij} = \frac{1}{2} \left( \frac{\partial u_i}{\partial x_j} + \frac{\partial u_j}{\partial x_i} \right)
$$

这里的 $u_i$ 是[位移矢量](@entry_id:262782) $\vec{u}$ 的第 $i$ 个分量，$x_j$ 是坐标的第 $j$ 个分量。这个定义是线性应变理论的基石。

举例来说，假设一个弹性介质的[位移场](@entry_id:141476)由 $u_1 = \alpha x_2^2$, $u_2 = \beta x_1 x_3$, $u_3 = \gamma x_2$ 给出，其中 $\alpha, \beta, \gamma$ 为小常数。我们可以通过计算偏导数来确定应变张量的各个分量。例如，$\epsilon_{11} = \frac{\partial u_1}{\partial x_1} = 0$，而 $\epsilon_{12}$ 的计算如下：
$$
\epsilon_{12} = \frac{1}{2} \left( \frac{\partial u_1}{\partial x_2} + \frac{\partial u_2}{\partial x_1} \right) = \frac{1}{2} (2\alpha x_2 + \beta x_3) = \alpha x_2 + \frac{\beta}{2} x_3
$$
通过系统地计算所有分量，我们可以得到完整的应变张量矩阵，它描述了介质中每一点的局部变形状态。[@problem_id:1557362]

从定义可以看出，无限[小应变张量](@entry_id:754968)具有一个至关重要的 intrinsic property：**对称性**。即 $\epsilon_{ij} = \epsilon_{ji}$。这一点是显而易见的，因为交换定义式中的下标 $i$ 和 $j$ 不会改变其值。例如，对于位移场 $u_x = a y^{2} + b z$, $u_y = a x^{2} + c z$, $u_z = b x + c y$，我们可以直接计算：
$$
\epsilon_{xy} = \frac{1}{2}\left(\frac{\partial u_{x}}{\partial y}+\frac{\partial u_{y}}{\partial x}\right) = \frac{1}{2}\left(2 a y+2 a x\right)=a(x+y)
$$
$$
\epsilon_{yx} = \frac{1}{2}\left(\frac{\partial u_{y}}{\partial x}+\frac{\partial u_{x}}{\partial y}\right) = \frac{1}{2}\left(2 a x+2 a y\right)=a(x+y)
$$
显然 $\epsilon_{xy} = \epsilon_{yx}$。这个对称性意味着一个 $3 \times 3$ 的应变张量只有6个独立分量（3个对角元和3个独立非对角元），而不是9个。[@problem_id:1557368]

### 应变分量的物理意义

[应变张量](@entry_id:193332)的数学形式固然简洁，但其真正的威力在于每个分量都具有明确的物理意义。

**[正应变](@entry_id:204633) (Normal Strain)**

张量的对角分量 $\epsilon_{11}, \epsilon_{22}, \epsilon_{33}$ 被称为**[正应变](@entry_id:204633)**。$\epsilon_{ii}$ （此处不使用爱因斯坦求和约定）代表了沿 $x_i$ 轴方向的材料微元线段的单位长度伸长率。如果 $\epsilon_{ii} > 0$，表示该方向上发生了拉伸；如果 $\epsilon_{ii}  0$，表示发生了压缩。

考虑一个简单的[位移场](@entry_id:141476) $\vec{u} = (\alpha x_1, \beta x_2, \gamma x_3)$。根据定义，我们可以轻易求得其应变张量为：
$$
\boldsymbol{\epsilon} = \begin{pmatrix} \alpha  0  0 \\ 0  \beta  0 \\ 0  0  \gamma \end{pmatrix}
$$
在这个例子中，$\epsilon_{11} = \alpha$ 直接量度了物体在 $x_1$ 方向的拉伸或压缩程度，其他两个对角分量同理。所有非对角分量均为零，表明没有发生角度变化，这是一种纯粹的伸缩变形。[@problem_id:1557316]

**[剪应变](@entry_id:175241) (Shear Strain)**

张量的非对角分量 $\epsilon_{ij}$ ($i \neq j$) 被称为**[剪应变](@entry_id:175241)**。它描述了初始时刻分别沿着 $x_i$ 和 $x_j$ 轴方向的两个材料微元线段之间夹角的变化。具体来说，[剪应变](@entry_id:175241)分量 $\epsilon_{ij}$ 等于这两个线段夹角（初始为 $90^\circ$ 或 $\pi/2$[弧度](@entry_id:171693)）减小量的一半。因此，两个正交方向间的夹角变化量 $\delta\theta$ 近似为 $2\epsilon_{ij}$。

一个典型的例子是**纯剪切**状态，例如，在一个平面上，只有 $\epsilon_{12} = \epsilon_{21} = \gamma_0$ 不为零，其余分量均为零。在这种变形下，原本位于 $x_1-x_2$ 平面内、分别沿 $x_1$ 和 $x_2$ 轴的线段，其夹角将不再是 $90^\circ$。变形后两个方向之间的夹角 $\theta'$ 满足 $\cos(\theta') \approx 2\epsilon_{12}$。由于初始夹角为 $\pi/2$，变形后的夹角为 $\theta' = \pi/2 - \delta\theta$，其中 $\delta\theta$ 是角度的减小量。利用[小角度近似](@entry_id:145423) $\cos(\pi/2 - \delta\theta) = \sin(\delta\theta) \approx \delta\theta$，我们得到角度的减小量为 $\delta\theta \approx 2\epsilon_{12} = 2\gamma_0$。这个关系清晰地揭示了[剪应变](@entry_id:175241)分量与材料形状扭曲之间的直接联系。[@problem_id:1557328]

### 作为张量的应变：性质与诠释

应变张量之所以被称为“张量”，是因为它不仅仅是一个分量的集合，更重要的是，它蕴含了某一点所有方向上的变形信息，并且其分量在[坐标系](@entry_id:156346)旋转时遵循特定的变换法则。

**任意方向的[正应变](@entry_id:204633)**

一旦我们知道了在某个[坐标系](@entry_id:156346)下应变张量 $\boldsymbol{\epsilon}$ 的全部分量，我们就可以计算出该点任意方向的[正应变](@entry_id:204633)。给定一个方向，由单位矢量 $\vec{n}$ 表示，该方向上的[正应变](@entry_id:204633) $\epsilon_n$ 可以通过二次型运算得到：
$$
\epsilon_n = \vec{n}^T \boldsymbol{\epsilon} \vec{n} \quad \text{或指标记法} \quad \epsilon_n = n_i \epsilon_{ij} n_j
$$
这个公式体现了张量的强大之处：它是一个统一的数学对象，封装了空间中所有方向的应变信息。例如，如果我们知道某点的应变张量 $\boldsymbol{\epsilon}$ 和一个特定方向的矢量 $\vec{v}$，我们首先需要将 $\vec{v}$ 单位化为 $\vec{n} = \vec{v} / |\vec{v}|$，然后便可代入公式计算该方向的伸长率。[@problem_id:1557349]

**应变张量的分解：球张量与[偏张量](@entry_id:185837)**

任何应变状态都可以被唯一地分解为两部分的叠加：一部分引起体积变化而不改变形状，另一部分引起形状扭曲而保持体积不变。

1.  **[体积应变](@entry_id:267252)与球张量**：材料微元的相对体积变化，称为**体积应变**或**胀量**（Dilatation），由应变张量的迹（trace）给出，即其对角元素之和：
    $$
    \theta = \mathrm{tr}(\boldsymbol{\epsilon}) = \epsilon_{11} + \epsilon_{22} + \epsilon_{33} = \epsilon_{kk} = \nabla \cdot \vec{u}
    $$
    这是[应变张量](@entry_id:193332)的**第一[不变量](@entry_id:148850)**，意味着它的值不随[坐标系](@entry_id:156346)的旋转而改变。它直接反映了材料的膨胀或收缩程度。[@problem_id:1557316] 我们可以构造一个只引起体积变化的[应变张量](@entry_id:193332)，称为**球形应变张量**（Spherical Strain Tensor），$\boldsymbol{\epsilon}^{\text{sph}}$:
    $$
    \boldsymbol{\epsilon}^{\text{sph}} = \frac{1}{3} \mathrm{tr}(\boldsymbol{\epsilon}) \mathbf{I} \quad \text{或以指标形式} \quad (\epsilon^{\text{sph}})_{ij} = \frac{1}{3} \epsilon_{kk} \delta_{ij}
    $$
    其中 $\mathbf{I}$ 是单位张量。这个张量在所有方向上都引起相同的[正应变](@entry_id:204633)，对应于均匀的膨胀或压缩。

2.  **形状改变与偏斜应变张量**：从总应变张量中减去球形部分，剩下的就是**偏斜应变张量**（Deviatoric Strain Tensor），$\boldsymbol{\epsilon}'$:
    $$
    \boldsymbol{\epsilon}' = \boldsymbol{\epsilon} - \boldsymbol{\epsilon}^{\text{sph}}
    $$
    偏斜[应变张量](@entry_id:193332)的一个关键特性是其迹为零，$\mathrm{tr}(\boldsymbol{\epsilon}') = 0$，这意味着它所代表的变形不引起任何体积变化，是纯粹的形状扭曲（畸变）。这种分解在材料的塑性理论和[流体力学](@entry_id:136788)中至关重要，因为它将导致体积变化的压力效应和导致流动的剪切效应分离开来。例如，给定一个应变张量，我们可以先计算其迹，然后构造球张量，最后通过减法得到[偏张量](@entry_id:185837)，从而清晰地分析体积变化和形状变化。[@problem_id:1557335]

### 应变与刚体运动

[应变张量](@entry_id:193332)的一个核心作用是区分变形与[刚体运动](@entry_id:193355)。**[刚体运动](@entry_id:193355)**（Rigid Body Motion）包括平移和旋转，在这种运动中，物体内部任意两点间的距离保持不变。因此，一个有效的变形度量，如[应变张量](@entry_id:193332)，对于纯粹的[刚体运动](@entry_id:193355)应该为零。

-   **刚体平移**：当物体经历一个均匀的平移时，位移场是常数矢量，$\vec{u}(\vec{r}) = \vec{c}$。由于位移分量 $u_i = c_i$ 不依赖于坐标 $x_j$，所有的位移[偏导数](@entry_id:146280) $\frac{\partial u_i}{\partial x_j}$ 都等于零。因此，应变张量的所有分量 $\epsilon_{ij}$ 也都为零。这证实了均匀平移不产生任何应变。[@problem_id:1557359]

-   **刚体旋转**：考虑一个绕 $x_3$ 轴的微小刚体旋转，其[位移场](@entry_id:141476)可以近似表示为 $u_1 = -\alpha x_2$, $u_2 = \alpha x_1$, $u_3 = 0$，其中 $\alpha$ 是一个小转角。计算[位移梯度张量](@entry_id:748571)会发现，其反对称部分非零，但对称部分的所有分量都恰好抵消为零。例如，
    $$
    \epsilon_{12} = \frac{1}{2} \left( \frac{\partial u_1}{\partial x_2} + \frac{\partial u_2}{\partial x_1} \right) = \frac{1}{2} (-\alpha + \alpha) = 0
    $$
    所有其他 $\epsilon_{ij}$ 分量也均为零。因此，整个无限[小应变张量](@entry_id:754968) $\boldsymbol{\epsilon}$ 是一个零张量。这明确地说明了无限[小应变张量](@entry_id:754968)的定义成功地滤除了刚体旋转的影响，只保留了纯粹的变形。[@problem_id:1557361]

### 物理真实性条件：[应变协调性](@entry_id:199659)

我们已经知道，一个位移场唯一地决定了一个应变场。但反过来的问题是：任意给定的一个对称二阶张量场 $\boldsymbol{\epsilon}(\vec{x})$，是否都能对应于某个连续、单值的[位移场](@entry_id:141476) $\vec{u}(\vec{x})$ 呢？

答案是否定的。因为6个独立的应变分量 $\epsilon_{ij}$ 是由仅仅3个独立的位移分量 $u_i$ 通过[微分](@entry_id:158718)运算得到的，所以这6个应变分量之间必须满足特定的约束关系。这些关系被称为**[应变协调方程](@entry_id:195003)**（Strain Compatibility Equations），由伟大的法国力学家 Adhémar Jean Claude Barré de Saint-Venant 首次导出。它们保证了从应变场积分到[位移场](@entry_id:141476)时，能够得到一个连续且单值的解，避免在物体内部出现不物理的“裂缝”或“重叠”。

在二维情况下，主要的协调方程可以简化为一个不协调性度量 $I$：
$$
I = \frac{\partial^2 \epsilon_{11}}{\partial x_2^2} + \frac{\partial^2 \epsilon_{22}}{\partial x_1^2} - 2 \frac{\partial^2 \epsilon_{12}}{\partial x_1 \partial x_2}
$$
对于一个物理上可能的应变场，必须有 $I=0$。例如，如果一个理论模型预测的应变场为 $\epsilon_{11} = \alpha x_2^2$, $\epsilon_{22} = 0$, $\epsilon_{12} = 0$，计算其不协调性度量会得到 $I = 2\alpha$。只要 $\alpha \neq 0$，这个应变场就是不协调的，即它不可能由任何一个连续的位移场产生，因此在物理上是不可能实现的。[@problem_id:1557354]

### 超越无限小应变：有限应变简介

本章主要关注无限[小应变张量](@entry_id:754968)，它是线[弹性理论](@entry_id:184142)和许多[流体动力学](@entry_id:136788)模型的基础。然而，认识到它的局限性至关重要。“小变形”假设意味着它仅在位移及其梯度都很小的情况下才准确。

当变形较大时（例如，在[橡胶弹性](@entry_id:164297)、[金属成形](@entry_id:188560)或[软组织力学](@entry_id:199866)中），我们必须使用**有限应变张量**。其中最常见的一种是**[格林-拉格朗日应变张量](@entry_id:187745)**（Green-Lagrange strain tensor）$\mathbf{E}$，它是根据物质坐标 $\vec{X}$ 定义的：
$$
\mathbf{E} = \frac{1}{2}(\mathbf{F}^T \mathbf{F} - \mathbf{I})
$$
此处，$\mathbf{F}$ 是**变形梯度张量**，其分量为 $F_{ij} = \frac{\partial x_i}{\partial X_j}$，而 $\mathbf{I}$ 是单位张量。

与无限[小应变张量](@entry_id:754968)不同，[格林-拉格朗日应变张量](@entry_id:187745)本质上是[非线性](@entry_id:637147)的。例如，在杆的[纯弯曲](@entry_id:202969)问题中（该问题涉及大转动），可以计算出[轴向应变](@entry_id:160811)分量 $E_{11}$。对于一个初始距离中性轴为 $X_2$、被弯曲成半径为 $R$ 的点，其结果为：
$$
E_{11} = \frac{X_2}{R} + \frac{X_2^2}{2R^2}
$$
这个表达式非常富有启发性。第一项 $\frac{X_2}{R}$ 是我们在初等[梁理论](@entry_id:176426)中熟悉的线性应变[分布](@entry_id:182848)。第二项 $\frac{X_2^2}{2R^2}$ 是一个[非线性](@entry_id:637147)修正项，它正是[有限应变理论](@entry_id:176941)捕捉到的[几何非线性](@entry_id:169896)效应。这个例子清晰地展示了，当变形不再“无限小”时，需要更高级的工具来精确描述物体的应变状态。[@problem_id:1557315]

总之，应变张量是描述[材料变形](@entry_id:169356)的核心工具。从其基于[位移梯度](@entry_id:165352)的定义，到其分量的物理意义，再到其[不变性](@entry_id:140168)、分解以及满足的协调性条件，这一概念为我们定量分析固体与流体的力学行为提供了坚实的数学基础。