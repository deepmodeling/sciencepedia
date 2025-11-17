## 引言
在连续介质力学的宏伟框架中，平衡方程扮演着基石的角色。它将施加于物体之上的外部作用（如重力和[表面力](@entry_id:188034)）与物体内部产生的应力状态直接联系起来，是理解和预测材料与结构力学行为的核心。任何处于静止或缓慢运动状态下的物体，从宏伟的行星到微小的工程部件，其内部的每一部分都必须满足这些由基本物理[守恒定律](@entry_id:269268)导出的严苛数学关系。然而，将这一普适原理应用于具有复杂几何形状的实际问题时，一个关键的挑战随之而来：如何选择并运用合适的数学语言（即[坐标系](@entry_id:156346)）来描述和求解这些方程？

本文旨在系统地解决这一挑战。我们不仅要展示平衡方程在不同[坐标系](@entry_id:156346)下的最终形式，更要揭示其从简单到复杂的演进脉络，以及其背后深刻的物理与几何内涵。文章将带领读者穿越三个核心章节，构建一个完整而深入的知识体系。

在“原理与机制”一章中，我们将回归本源，从线性动量与[角动量守恒](@entry_id:156798)出发，引入柯西应力张量的概念。我们将首先在最直观的直角[坐标系](@entry_id:156346)中推导出[平衡方程](@entry_id:172166)的微分形式，然后借助[张量分析](@entry_id:161423)的强大威力，引入[协变导数](@entry_id:152476)和[克里斯托费尔符号](@entry_id:159831)，将方程推广至具有普遍适用性的[曲线坐标系](@entry_id:172561)，并阐明其坐标[不变性](@entry_id:140168)的本质。

接着，在“应用与交叉学科联系”一章中，我们将展示这些理论的实际价值。通过分析诸如[厚壁圆筒](@entry_id:189222)的Lamé问题、带孔平板的[应力集中](@entry_id:160987)、行星的内部应力乃至[化学反应](@entry_id:146973)路径等一系列跨学科案例，读者将看到如何通过巧妙选择[坐标系](@entry_id:156346)来化繁为简，并理解平衡方程如何在工程、地球物理学、甚至理论化学等领域发挥关键作用。

最后，在“动手实践”部分，我们提供了一系列精心设计的练习题。这些练习将引导您亲手应用所学知识，从在[笛卡尔坐标系](@entry_id:169789)中检验应[力场](@entry_id:147325)，到在[柱坐标系](@entry_id:266798)下处理[轴对称](@entry_id:173333)问题，最终挑战在非标准[曲线坐标系](@entry_id:172561)下构建完整的[平衡方程](@entry_id:172166)，从而将理论知识转化为扎实的分析能力。

通过这一系列的学习，读者将不仅掌握平衡方程的数学表述，更能深刻理解其物理意义，并具备在不同[坐标系](@entry_id:156346)间灵活转换和应用这些基本方程解决复杂科学与工程问题的能力。

## 原理与机制

本章旨在深入阐述连续介质力学中静态[平衡方程](@entry_id:172166)的基本原理与数学表述。我们将从最基本的物理定律出发，首先在直角[坐标系](@entry_id:156346)（笛卡尔坐标系）中建立这些方程，然后利用[张量分析](@entry_id:161423)的强大工具，将其推广到更具普遍性的[曲线坐标系](@entry_id:172561)中。本章的目标是不仅展示这些方程的形式，更要揭示其背后深刻的物理和几何内涵。

### 静态平衡的基本原理

在[连续介质力学](@entry_id:155125)中，任何一个物体，无论其处于何种运动状态，都必须服从基本的物理[守恒定律](@entry_id:269268)。对于静态问题，我们关注的是[线性动量守恒](@entry_id:165717)（或称力平衡）和角动量守恒（或称[力矩平衡](@entry_id:752138)）。

#### 柯西应力原理与[力平衡](@entry_id:267186)

考虑一个处于静态平衡状态的连续体。根据[线性动量守恒](@entry_id:165717)原理，作用于该连续体内部任意一个子区域（我们称之为控制体）上的所有外力之和必须为零。这些力可分为两类：作用于整个体积的**体力（body forces）**，如重力、[电磁力](@entry_id:196024)等；以及作用于该控制体表面的**面力（surface forces）**，这是控制体外部的物质通过接触面对其施加的作用力。

若用 $\mathbf{b}$ 表示单位质量的体力，$\rho$ 表示密度，则作用于体积 $V$ 上的总[体力](@entry_id:174230)为 $\int_V \rho \mathbf{b} \, dV$。对于面力，法国数学家和工程师 Augustin-Louis Cauchy 提出了一个革命性的概念。他假设，在物体内部某一点，通过该点的一个微小面元上的面力，仅取决于该点的[状态和](@entry_id:193625)面元的方向。他进一步证明，存在一个[二阶张量](@entry_id:199780)场 $\boldsymbol{\sigma}$，称为**柯西[应力张量](@entry_id:148973)（Cauchy stress tensor）**，它完全描述了该点的应力状态。通过这个张量，作用在任意一个法向量为 $\mathbf{n}$ 的面上的**[面力矢量](@entry_id:189429)（traction vector）** $\mathbf{t}$ 可以被[线性表示](@entry_id:139970)为：

$$
\mathbf{t} = \boldsymbol{\sigma} \cdot \mathbf{n} \quad \text{或} \quad \mathbf{t} = \mathbf{n} \cdot \boldsymbol{\sigma}
$$

[指标记法](@entry_id:191923)存在不同约定，例如 $t_j = \sigma_{ij}n_i$ 或 $t_i = \sigma_{ji}n_j$。这两种约定在文献中均很常见，但由于[应力张量](@entry_id:148973)最终被证明是对称的，因此在实际应用中并无差异。这个关系式被称为**柯西公式（Cauchy's formula）**[@problem_id:2636626]。应力张量的分量 $\sigma_{ij}$ 的物理意义是作用在法向量为第 $i$ 个[基向量](@entry_id:199546)方向的平面上，沿第 $j$ 个[基向量](@entry_id:199546)方向的单位面积力。

有了这些定义，作用于任意控制体 $V$ 上的静态[力平衡](@entry_id:267186)原理可以用积分形式表示为：

$$
\int_S \mathbf{t} \, dS + \int_V \rho \mathbf{b} \, dV = \mathbf{0}
$$

其中 $S$ 是[控制体](@entry_id:143882) $V$ 的封闭边界面。这是一个矢量方程，它表明所有[表面力](@entry_id:188034)的合力与所有体力的合力必须相互抵消。这个积分形式的方程是所有平衡方程推导的出发点，它是一个不依赖于任何特定[坐标系](@entry_id:156346)的物理定律。

#### [角动量平衡](@entry_id:181848)与应力[张量的对称性](@entry_id:202126)

除了力平衡，物体还必须满足[力矩平衡](@entry_id:752138)，即角动量守恒。对于一个没有内禀自旋和体力矩的经典（非极性）连续体，角动量守恒定律要求，作用于任意[控制体](@entry_id:143882)上的总力矩为零。从这个基本物理定律出发，经过一系列推导可以证明，柯西应力张量必须是对称的 [@problem_id:2636648]。

$$
\boldsymbol{\sigma} = \boldsymbol{\sigma}^{\mathsf{T}} \quad \text{或以分量形式写作} \quad \sigma_{ij} = \sigma_{ji}
$$

这个结论极其重要。它意味着描述三维空间中任意一点的应力状态，我们只需要 6 个独立的分量（3 个正应力和 3 个剪应力），而不是 9 个。应力[张量的对称性](@entry_id:202126)是一个源于物理基本定律的普遍结论，它不依赖于材料的本构关系（即无论材料是弹性的、塑性的还是流体），并且在任何[坐标系](@entry_id:156346)下都成立。

### 直角[坐标系](@entry_id:156346)下的[平衡方程](@entry_id:172166)

虽然积分形式的[平衡方程](@entry_id:172166)具有普遍性，但在求解具体问题时，我们通常需要其局部（[微分](@entry_id:158718)）形式。为了从积分形式过渡到微分形式，我们首先考虑最简单的[坐标系](@entry_id:156346)——固定的三维直角[坐标系](@entry_id:156346)（笛卡尔坐标系），其坐标为 $(x_1, x_2, x_3)$。

我们将柯西公式 $\mathbf{t} = \boldsymbol{\sigma} \cdot \mathbf{n}$（或分量形式 $t_j = \sigma_{ij} n_i$）代入到[力平衡](@entry_id:267186)[积分方程](@entry_id:138643)中：

$$
\int_S \sigma_{ij} n_i \, dS + \int_V \rho b_j \, dV = 0
$$

这里我们写出了方程的第 $j$ 个分量，并使用了爱因斯坦求和约定（即重复的指标表示求和）。接下来，我们应用**[散度定理](@entry_id:143110)（Divergence Theorem）**，它将一个矢量场在闭合[曲面](@entry_id:267450)上的通量与其在体积内的散度联系起来。对于一个固定的分量 $j$，我们可以将 $\sigma_{ij}$ (其中 $i=1, 2, 3$) 视为一个矢量场的分量。应用散度定理，可将面积分转化为[体积分](@entry_id:171119)：

$$
\int_S \sigma_{ij} n_i \, dS = \int_V \frac{\partial \sigma_{ij}}{\partial x_i} \, dV = \int_V \sigma_{ij,i} \, dV
$$

在这里，我们引入了**逗号记法**，即下标中的逗号后跟一个指标表示对相应坐标的[偏微分](@entry_id:194612)，例如 $\sigma_{ij,i} = \partial \sigma_{ij} / \partial x_i$。

将此结果代回力[平衡方程](@entry_id:172166)，我们得到：

$$
\int_V (\sigma_{ij,i} + \rho b_j) \, dV = 0
$$

由于这个积分等式必须对任意选择的控制体 $V$ 都成立，且被积函数是连续的，那么被积函数本身必须处处为零。这被称为**局部化原理（localization principle）**。因此，我们得到了静态平衡的局部[微分方程](@entry_id:264184) [@problem_id:2636667]：

$$
\sigma_{ij,i} + \rho b_j = 0 \quad (\text{for } j=1, 2, 3)
$$

由于应力[张量的对称性](@entry_id:202126)（$\sigma_{ij} = \sigma_{ji}$），这个方程也可以等价地写成更常见的形式：

$$
\sigma_{ji,i} + \rho b_j = 0 \quad \text{或} \quad \nabla \cdot \boldsymbol{\sigma} + \rho\boldsymbol{b} = \mathbf{0}
$$

在直角[坐标系](@entry_id:156346)中，这三个标量方程展开后为：
$$
\begin{cases}
\dfrac{\partial \sigma_{xx}}{\partial x} + \dfrac{\partial \sigma_{yx}}{\partial y} + \dfrac{\partial \sigma_{zx}}{\partial z} + \rho b_x = 0 \\
\dfrac{\partial \sigma_{xy}}{\partial x} + \dfrac{\partial \sigma_{yy}}{\partial y} + \dfrac{\partial \sigma_{zy}}{\partial z} + \rho b_y = 0 \\
\dfrac{\partial \sigma_{xz}}{\partial x} + \dfrac{\partial \sigma_{yz}}{\partial y} + \dfrac{\partial \sigma_{zz}}{\partial z} + \rho b_z = 0
\end{cases}
$$
其中，为了直观，我们使用了 $(x, y, z)$ 和相应的下标来表示坐标和分量。这些方程是连续介质力学中最基本的方程之一。

### 向[曲线坐标系](@entry_id:172561)的推广

直角[坐标系](@entry_id:156346)虽然简单，但在处理具有[曲面](@entry_id:267450)边界（如圆柱、球体）或特定对称性的问题时却显得非常不便。因此，我们必须将[平衡方程](@entry_id:172166)推广到一般[曲线坐标系](@entry_id:172561)中，如[圆柱坐标系](@entry_id:266798)和球坐标系。

#### 坐标不变性与[张量分析](@entry_id:161423)

首先需要明确一个核心概念：力平衡定律是一个物理定律，它的正确性不应依赖于我们选择用什么[坐标系](@entry_id:156346)去描述它。方程 $\nabla \cdot \boldsymbol{\sigma} + \rho\boldsymbol{b} = \mathbf{0}$ 是一个**张量方程**，它表示不同张量场之间的关系。张量方程的显著特点是其**形式的坐标不变性（coordinate invariance）** [@problem_id:2636613]。这意味着，尽管在不同的[坐标系](@entry_id:156346)下，张量的*分量*和微分算子的*表达式*会改变，但方程的整体结构保持不变。

在这个方程中，$\rho$ 是一个标量场（零阶张量），$\boldsymbol{b}$ 是一个矢量场（一阶张量），$\boldsymbol{\sigma}$ 是一个[二阶张量](@entry_id:199780)场。[微分算子](@entry_id:140145)“散度”作用于一个二阶张量会得到一个一阶张量（矢量）。因此，方程中的每一项 ($\nabla \cdot \boldsymbol{\sigma}$ 和 $\rho\boldsymbol{b}$) 都是矢量场，它们相加得到[零矢量](@entry_id:155273)场。这种张量阶数的匹配是方程能够保持坐标[不变性](@entry_id:140168)的一个必要条件 [@problem_id:2636613]。

#### [协变导数](@entry_id:152476)与克里斯托费尔符号

当从直角[坐标系转换](@entry_id:263003)到[曲线坐标系](@entry_id:172561)（例如，从 $(x,y,z)$ 到 $(q^1, q^2, q^3)$）时，[基向量](@entry_id:199546)（如 $\mathbf{g}_i = \partial \mathbf{x} / \partial q^i$）不再是常数，它们会随着空间位置的改变而改变方向和/或长度。因此，对一个张量分量进行普通的[偏微分](@entry_id:194612)不再能得到一个具有正确变换性质的张量。

为了解决这个问题，数学上引入了**协变导数（covariant derivative）**，记为 $\nabla$ 或用分号 `;` 表示。协变导数在普通[偏导数](@entry_id:146280)的基础上增加了一些修正项，这些修正项正好抵消了[基向量](@entry_id:199546)变化带来的影响，从而保证了求导结果仍然是一个张量。这些修正项由**[克里斯托费尔符号](@entry_id:159831)（Christoffel symbols）** $\Gamma^k_{ij}$ 构成。克里斯托费尔符号精确地量化了[基向量](@entry_id:199546)随坐标的变化率 [@problem_id:2636606]：

$$
\frac{\partial \mathbf{g}_j}{\partial q^k} = \Gamma^i_{jk} \mathbf{g}_i
$$

对于一个源于[坐标基](@entry_id:270149)的无挠率联络，[克里斯托费尔符号](@entry_id:159831)的下标记是对称的（$\Gamma^k_{ij} = \Gamma^k_{ji}$）。更重要的是，在一个具有度规张量 $g_{ij} = \mathbf{g}_i \cdot \mathbf{g}_j$ 的空间中，要求联络是**度规相容的**（即[度规张量的协变导数](@entry_id:198162)为零），就可以唯一地确定[克里斯托费尔符号](@entry_id:159831)，它们完全由[度规张量](@entry_id:160222)及其[一阶导数](@entry_id:749425)决定 [@problem_id:2636606] [@problem_id:2636629]。这就是黎曼几何的基本定理，它为在任意[坐标系](@entry_id:156346)中进行微积分提供了坚实的几何基础。

利用[协变导数](@entry_id:152476)，应力张量 $\sigma^{ij}$ 的散度（一个矢量）的第 $i$ 个分量可以写为 $\sigma^{ij}{}_{;j}$。其展开式明确地包含了[克里斯托费尔符号](@entry_id:159831) [@problem_id:2636661] [@problem_id:2636650]：

$$
(\nabla \cdot \boldsymbol{\sigma})^i = \sigma^{ij}{}_{;j} = \frac{\partial \sigma^{ij}}{\partial q^j} + \Gamma^i_{kj} \sigma^{kj} + \Gamma^j_{kj} \sigma^{ik}
$$

这个表达式中的附加项（$\Gamma$ 项）正是从直角[坐标系](@entry_id:156346)推广到[曲线坐标系](@entry_id:172561)的关键，它们确保了散度作为一个物理量被正确计算。

因此，在一般[曲线坐标系](@entry_id:172561)中，静态平衡方程的分量形式为 [@problem_id:2636650]：

$$
\sigma^{ij}{}_{;j} + b^i = 0
$$

其中 $b^i$ 是体力矢量的[逆变分量](@entry_id:185440)。

### 应用：[圆柱坐标系](@entry_id:266798)下的[平衡方程](@entry_id:172166)

为了将上述抽象理论具体化，我们来看一个重要的应用实例：[圆柱坐标系](@entry_id:266798) $(r, \theta, z)$。其单位[正交基](@entry_id:264024)向量为 $\{\mathbf{e}_r, \mathbf{e}_\theta, \mathbf{e}_z\}$。在这个[坐标系](@entry_id:156346)中，[基向量](@entry_id:199546) $\mathbf{e}_r$ 和 $\mathbf{e}_\theta$ 的方向会随着角度 $\theta$ 的变化而改变，这导致了非零的克里斯托费尔符号，从而在[平衡方程](@entry_id:172166)中产生额外的“几何”项。

通过将[协变散度](@entry_id:275039)算子应用于物理应力分量（$\sigma_{rr}, \sigma_{\theta\theta}, \sigma_{zz}, \sigma_{r\theta}, \dots$），可以推导出[平衡方程](@entry_id:172166)在[圆柱坐标系](@entry_id:266798)下的三个标量形式 [@problem_id:2636643] [@problem_id:2636626]：

**r-方向 (径向):**
$$
\frac{\partial \sigma_{rr}}{\partial r} + \frac{1}{r}\frac{\partial \sigma_{r\theta}}{\partial\theta} + \frac{\partial \sigma_{rz}}{\partial z} + \frac{\sigma_{rr}-\sigma_{\theta\theta}}{r} + b_r = 0
$$

**θ-方向 (环向):**
$$
\frac{\partial \sigma_{r\theta}}{\partial r} + \frac{1}{r}\frac{\partial \sigma_{\theta\theta}}{\partial\theta} + \frac{\partial \sigma_{\theta z}}{\partial z} + \frac{2\sigma_{r\theta}}{r} + b_{\theta} = 0
$$

**z-方向 (轴向):**
$$
\frac{\partial \sigma_{rz}}{\partial r} + \frac{1}{r}\frac{\partial \sigma_{z\theta}}{\partial\theta} + \frac{\partial \sigma_{zz}}{\partial z} + \frac{\sigma_{rz}}{r} + b_z = 0
$$

请注意这些方程中出现的 $1/r$ 因子项，例如[径向方程](@entry_id:191687)中的 $(\sigma_{rr}-\sigma_{\theta\theta})/r$ 和环向方程中的 $2\sigma_{r\theta}/r$。这些并非新的物理效应，而是由于在[曲线坐标系](@entry_id:172561)下进行[微分](@entry_id:158718)运算，为保持坐标[不变性](@entry_id:140168)而必须引入的几何修正项。它们直接源于[克里斯托费尔符号](@entry_id:159831)。例如，对于轴对称问题（所有场量不随 $\theta$ 变化，即 $\partial/\partial\theta = 0$），这些方程会得到简化，但几何项依然存在 [@problem_id:2636641]。

### 静态与动态问题的关联

最后，值得一提的是，本章所讨论的静态平衡方程是更普适的[动量守恒](@entry_id:149964)定律的一个特例。完整的**柯西第一运动定律（Cauchy's first law of motion）**的局部形式为：

$$
\nabla \cdot \boldsymbol{\sigma} + \rho\boldsymbol{b} = \rho\boldsymbol{a}
$$

其中 $\boldsymbol{a}$ 是材料点的加速度，$\rho\boldsymbol{a}$ 这一项被称为**惯性项（inertia term）**。

静态[平衡方程](@entry_id:172166)本质上是假设加速度 $\boldsymbol{a} = \mathbf{0}$ 的情况。在许多工程问题中，如果加载过程非常缓慢，使得加速度足够小，[惯性力](@entry_id:169104) $\rho\boldsymbol{a}$ 与应力梯度项 $\nabla \cdot \boldsymbol{\sigma}$ 或[体力](@entry_id:174230)项 $\rho\boldsymbol{b}$ 相比可以忽略不计，此时就可以采用静态或**准静态（quasi-static）**近似。一个常用的判断准则是，加载的[特征时间](@entry_id:173472) $T_c$ 远大于[弹性波](@entry_id:196203)在结构中传播所需的特征时间 $L/c$（其中 $L$ 是特征长度，c 是[波速](@entry_id:186208)），即 $T_c \gg L/c$ [@problem_id:2636641]。

此外，当在[非惯性参考系](@entry_id:169712)（如一个匀速转动的框架）中分析问题时，方程的形式可以保持不变。此时，由[坐标系](@entry_id:156346)变换产生的惯性力（如离心力、[科里奥利力](@entry_id:160096)）可以被移到方程左边，并被吸收到一个“有效”的[体力](@entry_id:174230)项中。在这种情况下，“静态”指的是相对于该[非惯性参考系](@entry_id:169712)的加速度为零 [@problem_id:2636641]。

通过本章的学习，我们从基本物理原理出发，系统地建立了在不同[坐标系](@entry_id:156346)下描述连续介质静态平衡的数学框架，为后续的力学分析和求解奠定了坚实的基础。