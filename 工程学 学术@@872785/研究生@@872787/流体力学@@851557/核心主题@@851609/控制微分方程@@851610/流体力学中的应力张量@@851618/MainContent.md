## 引言
在[流体力学](@entry_id:136788)中，理解和量化流体内部的相互作用力是预测其运动、变形和输运性质的基石。[应力张量](@entry_id:148973)正是为实现这一目标而引入的核心数学工具，它将作用于流体微元表面上的复杂力系，统一到一个精确的张量框架中。然而，从静态液体中各向同性的压力，到复杂[湍流](@entry_id:151300)中由涡旋产生的表观“应力”，[应力张量](@entry_id:148973)的内涵和形式变化巨大，构成了[流体力学](@entry_id:136788)中的一个关键知识体系。本文旨在系统性地梳理这一概念，填补从基础理论到前沿应用之间的认知鸿沟。

本文将分为三个核心章节，引导读者深入理解应力张量的世界。在“原理与机制”部分，我们将建立[应力张量](@entry_id:148973)的基本定义，阐述其如何分解为压力和[粘性应力](@entry_id:261328)，并推导[牛顿流体](@entry_id:263796)的[本构方程](@entry_id:138559)，同时介绍非牛顿流体和[湍流](@entry_id:151300)中的应力概念。接下来，在“应用与[交叉](@entry_id:147634)学科联系”部分，我们将展示[应力张量](@entry_id:148973)在解决实际工程问题（如润滑和曳力计算）和推动其他科学领域（如[生物力学](@entry_id:153973)、[地球物理学](@entry_id:147342)和相对论）发展中的关键作用。最后，“动手实践”部分将提供具体的计算问题，帮助读者巩固理论知识。通过这一结构化的学习路径，读者将掌握应力张量这一强大工具，并能够运用它来分析和解决复杂的[流体动力学](@entry_id:136788)问题。

## 原理与机制

在流体连续介质的框架下，理解作用在流体内部的力是描述其运动和变形的基础。这些[内力](@entry_id:167605)通过[应力张量](@entry_id:148973)的概念被精确地数学化。本章旨在系统地阐述流体中应力张量的基本原理、其与[流体运动](@entry_id:182721)的关联，以及在不同流体模型（从[理想流体](@entry_id:161909)到复杂的[湍流](@entry_id:151300)）中应力所扮演的角色。

### 柯西应力张量与[静水压力](@entry_id:275365)

为了描述流体内部任意一点的受力状态，我们引入**柯西[应力张量](@entry_id:148973)**（Cauchy stress tensor），记为 $\sigma_{ij}$。这是一个二阶张量，其分量 $\sigma_{ij}$ 代表了作用在单位面积上的力。具体而言，如果一个微元面的法向指向 $j$ 轴，那么作用在该面上的力的第 $i$ 个分量就是 $\sigma_{ij}$。对角分量（$i=j$）如 $\sigma_{11}$、$\sigma_{22}$、$\sigma_{33}$ 被称为**法向应力**（normal stresses），它们描述了垂直于微元面的拉伸或压缩。非对角分量（$i \neq j$）如 $\sigma_{12}$、$\sigma_{23}$ 被称为**[剪切应力](@entry_id:137139)**（shear stresses），它们描述了平行于微元面的力。

理解[应力张量](@entry_id:148973)最简单的情形是考虑一种处于完全静止状态的**[理想流体](@entry_id:161909)**（ideal fluid），即一种粘性为零的流体。在这种**静水**（hydrostatic）条件下，流体内部不存在相对运动，因此无法承受任何[剪切应力](@entry_id:137139)。这意味着所有非对角应力分量都必须为零，即当 $i \neq j$ 时，$\sigma_{ij} = 0$。

此外，[静止流体](@entry_id:187621)中任意一点的压力在所有方向上都是均等的，这一性质被称为压力的**各向同性**（isotropy）。作用在任何内部表面上的力都严格垂直于该表面，并且本质上是压缩性的。这个力的大小，即单位面积上的作用力，就是我们熟知的**[静水压力](@entry_id:275365)**（hydrostatic pressure）$p$。在连续介质力学中，通常约定压缩应力为负，拉伸应力为正。因此，在静水条件下，三个法向应力分量相等，且等于负的静水压力：$\sigma_{11} = \sigma_{22} = \sigma_{33} = -p$。

为了用一个统一的表达式来表示这种[对角形式](@entry_id:264850)的张量，我们使用**克罗内克符号**（Kronecker delta）$\delta_{ij}$，其定义为当 $i=j$ 时为 $1$，当 $i \neq j$ 时为 $0$。综合以上分析，静止理想流体的柯西[应力张量](@entry_id:148973)可以简洁地表示为 [@problem_id:1490177]：
$$
\sigma_{ij} = -p \delta_{ij}
$$
这个表达式精确地捕捉了静水状态的物理本质：应力是各向同性的（仅由一个标量 $p$ 描述）并且纯粹是压缩性的（由负号表示），没有任何剪切成分。

### 应力张量的一般分解

当流体开始运动时，情况变得复杂起来。流体内部的[相对运动](@entry_id:169798)会产生由粘性引起的[剪切应力](@entry_id:137139)，同时法向应力也可能不再各向同性。然而，即使在最一般的流动情况下，将总[应力分解](@entry_id:272862)为其各向同性[部分和](@entry_id:162077)偏斜部分的思想依然极其有用。

对于任何[二阶张量](@entry_id:199780) $\sigma_{ij}$，我们都可以将其唯一地分解为一个与单位张量 $\delta_{ij}$ 成比例的**[各向同性张量](@entry_id:195105)**（isotropic tensor）和一个**迹为零**的**[偏应力张量](@entry_id:267642)**（deviatoric stress tensor）。这个分解并非基于任何物理假设，而是一个纯粹的数学恒等式 [@problem_id:1794725]。

首先，我们定义**力学压力**（mechanical pressure）$p$ 为三个法向应力的算术平均值的[相反数](@entry_id:151709)。这个定义源自于总应力张量的迹（trace）：
$$
p \equiv -\frac{1}{3} (\sigma_{11} + \sigma_{22} + \sigma_{33}) = -\frac{1}{3} \operatorname{tr}(\boldsymbol{\sigma})
$$
值得注意的是，这个定义将压力与总[法向应力](@entry_id:260622)的平均值直接联系起来，这个平均值在[坐标旋转](@entry_id:164444)下是不变的，保证了 $p$ 是一个客观的标量。从一个给定的应力张量中计算力学压力时，只有对角线上的法向应力分量有贡献。例如，假设一个深海探测器在近乎静止的水中测得如下[应力张量](@entry_id:148973)（单位为MPa）[@problem_id:1560651]：
$$
\boldsymbol{\sigma} = \begin{pmatrix} -108.9  & 0.12  & -0.25 \\ 0.12  & -109.1  & 0.18 \\ -0.25  & 0.18  & -109.0 \end{pmatrix}
$$
尽管存在微小的剪切应力（可能是[测量噪声](@entry_id:275238)），我们可以计算出其迹为 $\operatorname{tr}(\boldsymbol{\sigma}) = -108.9 - 109.1 - 109.0 = -327.0$ MPa。因此，该点的力学压力为 $p = -(-327.0 / 3) = 109.0$ MPa。

一旦定义了力学压力，总[应力张量](@entry_id:148973) $\sigma_{ij}$ 就可以写作：
$$
\sigma_{ij} = -p \delta_{ij} + \tau_{ij}
$$
其中，$\tau_{ij}$ 被定义为**[偏应力张量](@entry_id:267642)**，有时也称为**[粘性应力](@entry_id:261328)张量**或**额外[应力张量](@entry_id:148973)**（extra stress tensor）。它代表了总应力中偏离[各向同性压力](@entry_id:269937)状态的部分：
$$
\tau_{ij} = \sigma_{ij} + p \delta_{ij}
$$
根据力学压力的定义，[偏应力张量](@entry_id:267642)的迹恒为零：
$$
\operatorname{tr}(\boldsymbol{\tau}) = \tau_{kk} = \sigma_{kk} + p \delta_{kk} = \sigma_{kk} + 3p = \sigma_{kk} + 3 \left(-\frac{1}{3}\sigma_{ll}\right) = \sigma_{kk} - \sigma_{kk} = 0
$$
这个分解至关重要。$-p\delta_{ij}$ 部分与流体微元的体积变化相关联，而[偏应力张量](@entry_id:267642) $\tau_{ij}$ 则与流体微元的形状变化（即变形或剪切）相关联 [@problem_id:1767802]。

### [本构方程](@entry_id:138559)：连接应力与运动

上述的[应力分解](@entry_id:272862)是一个数学恒等式，它适用于任何连续介质。[流体力学](@entry_id:136788)的核心任务之一，便是建立描述特定流体行为的**[本构方程](@entry_id:138559)**（constitutive equation），即建立[偏应力张量](@entry_id:267642) $\tau_{ij}$ 与[流体运动学](@entry_id:202835)特征之间的关系。

流体微元在空间中的局部运动可以由其**[速度梯度张量](@entry_id:270928)** $\frac{\partial u_i}{\partial x_j}$ 完全描述。这个张量也可以被分解为一个对称部分和一个反对称部分：
$$
\frac{\partial u_i}{\partial x_j} = \frac{1}{2} \left( \frac{\partial u_i}{\partial x_j} + \frac{\partial u_j}{\partial x_i} \right) + \frac{1}{2} \left( \frac{\partial u_i}{\partial x_j} - \frac{\partial u_j}{\partial x_i} \right)
$$
对称部分被称为**应变率张量**（rate-of-strain tensor）$S_{ij} = \frac{1}{2} (\frac{\partial u_i}{\partial x_j} + \frac{\partial u_j}{\partial x_i})$，它描述了流体微元的拉伸和剪切变形速率。反对称部分被称为**[涡量张量](@entry_id:189621)**（vorticity tensor）$\Omega_{ij} = \frac{1}{2} (\frac{\partial u_i}{\partial x_j} - \frac{\partial u_j}{\partial x_i})$，它描述了流体微元的刚性旋转速率。

一个基本的物理原理是，对于简单的各向同性流体（如水或空气，它们不具有内在的微观结构方向性），[粘性应力](@entry_id:261328)是由流体微元的变形引起的，而不是由其整体的刚性旋转引起的。换言之，$\tau_{ij}$ 应该只依赖于 $S_{ij}$ 而不依赖于 $\Omega_{ij}$。我们可以通过一个更形式化的论证来证明这一点。假设[粘性应力](@entry_id:261328)是[速度梯度](@entry_id:261686)的线性函数，并且可以写成应变率和涡量贡献之和。基于[各向同性原理](@entry_id:200394)，任何由[涡量张量](@entry_id:189621) $\boldsymbol{\Omega}$ 产生的应力贡献 $\boldsymbol{\tau}_\Omega$ 必须与 $\boldsymbol{\Omega}$ 本身成正比。然而，柯西[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ 对于非极性流体（分子不携带[内禀角动量](@entry_id:189727)）必须是对称的。由于 $-p\boldsymbol{I}$ 是对称的，这意味着 $\boldsymbol{\tau}$ 也必须是对称的。如果 $\boldsymbol{\tau}_\Omega$ 是由反对称的 $\boldsymbol{\Omega}$ 线性生成的，并且自身需要是对称的，那么唯一的可能性就是 $\boldsymbol{\tau}_\Omega$ 必须为零张量。因此，[粘性应力](@entry_id:261328)不依赖于[涡量](@entry_id:142747) [@problem_id:657123]。

### 牛顿流体

最简单也是最常见的流体模型是**[牛顿流体](@entry_id:263796)**（Newtonian fluid），其定义是[偏应力张量](@entry_id:267642) $\tau_{ij}$ 与[应变率张量](@entry_id:266108) $S_{ij}$ 之间存在线性关系。

#### 不可压缩情况
对于**[不可压缩流体](@entry_id:181066)**，流体微元的体积在运动中保持不变。这在数学上表现为[速度场](@entry_id:271461)的散度为零，即 $\nabla \cdot \mathbf{u} = \frac{\partial u_k}{\partial x_k} = 0$。由于 $\operatorname{tr}(\mathbf{S}) = S_{kk} = \frac{\partial u_k}{\partial x_k}$，这意味着[不可压缩流](@entry_id:140301)动的[应变率张量](@entry_id:266108)是无迹的。

在这种情况下，$\tau_{ij}$ 和 $S_{ij}$ 之间最简单的线性各向同性关系是：
$$
\tau_{ij} = 2\mu S_{ij}
$$
其中，比例常数 $\mu$ 被称为**[动力粘度](@entry_id:268228)**（dynamic viscosity），它是一个衡量流体抵抗剪切变形能力的材料属性。因子 $2$ 是历史约定俗成的。将此代入总应力张量的分解中，我们得到不可压缩[牛顿流体](@entry_id:263796)的完整[本构方程](@entry_id:138559) [@problem_id:1746674]：
$$
\sigma_{ij} = -p \delta_{ij} + 2\mu S_{ij} = -p \delta_{ij} + \mu \left( \frac{\partial u_i}{\partial x_j} + \frac{\partial u_j}{\partial x_i} \right)
$$
这个方程是著名的**[纳维-斯托克斯方程](@entry_id:142275)**（[Navier-Stokes](@entry_id:276387) equations）的基石。

#### 可压缩情况
对于**[可压缩流体](@entry_id:164617)**，其密度可以变化，因此[速度散度](@entry_id:264117) $\nabla \cdot \mathbf{u}$ 通常不为零。这意味着流体微元可以经历体积膨胀或收缩。在这种情况下，最一般的线性各向同性[本构关系](@entry_id:186508)包含一个额外的项，该项与体积变化率（即 $\operatorname{tr}(\mathbf{S})$ 或 $\nabla \cdot \mathbf{u}$）相关：
$$
\tau_{ij} = 2\mu S_{ij} + \lambda (\nabla \cdot \mathbf{u}) \delta_{ij}
$$
这里的 $\lambda$ 是**[第二粘度](@entry_id:189253)系数**（second coefficient of viscosity）。这个新项是一个[各向同性张量](@entry_id:195105)，它描述了由体积变化引起的附加法向应力。

通常，将 $\lambda$ 和 $\mu$ 组合成一个更有物理解释的系数，即**[体积粘度](@entry_id:187773)**（bulk viscosity）$\kappa$，定义为：
$$
\kappa \equiv \lambda + \frac{2}{3}\mu
$$
利用这个定义，我们可以发现[偏应力](@entry_id:163323)的迹（即平均法向[粘性应力](@entry_id:261328)）与体积变化率成正比：
$$
\frac{1}{3}\operatorname{tr}(\boldsymbol{\tau}) = \frac{1}{3} \tau_{kk} = \frac{1}{3} [2\mu S_{kk} + \lambda (\nabla \cdot \mathbf{u}) \delta_{kk}] = \frac{1}{3} [2\mu (\nabla \cdot \mathbf{u}) + 3\lambda (\nabla \cdot \mathbf{u})] = \left(\lambda + \frac{2}{3}\mu\right) (\nabla \cdot \mathbf{u}) = \kappa (\nabla \cdot \mathbf{u})
$$
因此，[体积粘度](@entry_id:187773) $\kappa$ 是抵[抗体](@entry_id:146805)积快速变化的量度。对于许多常见流体，如[单原子气体](@entry_id:140562)，可以从理论上证明 $\kappa=0$。这个假设，即 $\lambda = -2/3 \mu$，被称为**斯托克斯假说**（Stokes' hypothesis）。虽然它对许多应用来说是一个很好的近似，但对于多原子气体和液体，尤其是在声波吸收和激波结构等现象中，$\kappa$ 的值可能非零且相当重要 [@problem_id:657101]。

### 粘性耗散

[粘性应力](@entry_id:261328)的存在意味着当[流体变形](@entry_id:271538)时，[机械能](@entry_id:162989)会因内摩擦而不可逆地转化为内能（热量）。这个能量转化的速率，单位体积称为**[粘性耗散](@entry_id:143708)函数**（viscous dissipation function），记为 $\Phi$。它被定义为[粘性应力](@entry_id:261328)张量与[速度梯度张量](@entry_id:270928)的完全收缩：
$$
\Phi = \tau_{ij} \frac{\partial u_i}{\partial x_j}
$$
由于 $\tau_{ij}$ 是对称的，而[速度梯度](@entry_id:261686)可以分解为对称的 $S_{ij}$ 和反对称的 $\Omega_{ij}$，我们可以证明 $\tau_{ij} \Omega_{ij} = 0$。因此，耗散函数可以简化为粘性[应力与[应变](@entry_id:263123)率张量](@entry_id:266108)的收缩：
$$
\Phi = \tau_{ij} S_{ij}
$$
对于不可压缩[牛顿流体](@entry_id:263796)，我们有 $\tau_{ij} = 2\mu S_{ij}$，代入上式得到：
$$
\Phi = 2\mu S_{ij} S_{ij}
$$
由于 $S_{ij} S_{ij}$ 是一个张量所有分量的平方和（乘以一个常数），它总是一个非负值。物理上，[动力粘度](@entry_id:268228) $\mu$ 也必须是非负的，这确保了 $\Phi \ge 0$。这符合热力学第二定律，即粘性总是耗散能量，而不是产生能量。这个耗散函数也可以用应变率张量的**第二[不变量](@entry_id:148850)** $II_S$ 来表示，对于不可压缩流体，有 $\Phi = -4\mu II_S$，这突显了耗散是一个不依赖于[坐标系](@entry_id:156346)选择的内在物理过程 [@problem_id:657151]。

### 超越牛顿模型的应力

虽然[牛顿流体](@entry_id:263796)模型应用广泛，但许多工业和生物流体（如聚合物熔体、血液、涂料）表现出更复杂的行为，不能用简单的线性[本构方程](@entry_id:138559)描述。

#### 非牛顿流体与[法向应力差](@entry_id:191914)
这些**[非牛顿流体](@entry_id:145598)**的一个显著特征是在简单的[剪切流](@entry_id:266817)中会产生**[法向应力差](@entry_id:191914)**（normal stress differences）。考虑一个简单的剪切流，其[速度场](@entry_id:271461)为 $\mathbf{v} = (\dot{\gamma}y, 0, 0)$，其中 $\dot{\gamma}$ 是恒定的剪切速率，$x$ 是流动方向，$y$ 是[速度梯度](@entry_id:261686)方向。对于牛顿流体，在这种流动中，除了[剪切应力](@entry_id:137139) $\sigma_{xy}$ 外，所有法向应力都是相等的（都等于 $-p$）。

然而，对于[聚合物溶液](@entry_id:145399)或熔体，实验观察到[法向应力](@entry_id:260622)并不相等。我们定义**第一[法向应力差](@entry_id:191914)** $N_1$ 和**第二[法向应力差](@entry_id:191914)** $N_2$ 为 [@problem_id:2925775]：
$$
N_1 = \sigma_{xx} - \sigma_{yy}
$$
$$
N_2 = \sigma_{yy} - \sigma_{zz}
$$
对于大多数聚合物液体，$N_1$ 是正的且远大于 $|N_2|$，而 $N_2$ 通常是负的。这种现象的微观起源在于[剪切流](@entry_id:266817)场会拉伸和[排列](@entry_id:136432)长链聚合物分子。分子链倾向于沿着流动方向（$x$ 方向）对齐和伸展，产生一种类似橡皮筋的弹性张力。这种沿流动方向的张力导致 $\sigma_{xx}$ 显著大于其他方向的[法向应力](@entry_id:260622)，从而产生一个正的 $N_1$。

这种弹性效应会导致一些惊人的宏观现象。一个典型的例子是**[魏森贝格效应](@entry_id:276292)**（Weissenberg effect），或称**爬杆效应**。当一根旋转的杆插入到聚合物液体中时，液体会沿着杆向上爬升，形成一个凸起的液面。这是因为在圆周运动中，正的 $N_1$ 表现为沿流线方向的“[环向应力](@entry_id:190931)”，这种应力像拉紧的绳索一样向内收缩，将流体推向旋转中心（杆），从而迫使液面升高。

#### [湍流](@entry_id:151300)与雷诺应力
另一种应力概念出现在**[湍流](@entry_id:151300)**（turbulent flow）的研究中。[湍流](@entry_id:151300)的特点是[速度场](@entry_id:271461)在时间和空间上都表现出混沌和无序的脉动。直接模拟这种脉动通常计算成本极高。因此，一种常见的处理方法是使用**[雷诺平均](@entry_id:754341)**（Reynolds averaging），将瞬时速度 $\mathbf{u}$ 分解为[时间平均](@entry_id:267915)部分 $\langle \mathbf{u} \rangle$ 和脉动部分 $\mathbf{u}'$。

将这个分解代入动量方程并进行时间平均，[非线性](@entry_id:637147)的[对流](@entry_id:141806)项 $\rho (\mathbf{u} \cdot \nabla)\mathbf{u}$ 会产生一个形如 $-\rho \langle u'_i u'_j \rangle$ 的附加项。这个张量被称为**[雷诺应力张量](@entry_id:270803)**（Reynolds stress tensor）。它虽然被称为“应力”，但其物理来源与分子间的[粘性力](@entry_id:263294)完全不同。它代表了由速度脉动引起的动量在空间中的输运。本质上，它是[湍流涡](@entry_id:266898)旋携带动量从一个地方移动到另一个地方的宏观效应。

在许多工程问题中，比如管道或环形通道中的流动，我们关心的是**总应力**（total stress），即分子[粘性应力](@entry_id:261328)与[雷诺应力](@entry_id:263788)之和。例如，在一个由恒定压力梯度驱动的稳定、充分发展的环形通道[湍流](@entry_id:151300)中，[动量方程](@entry_id:197225)的积分可以精确地揭示总[剪切应力](@entry_id:137139) $\tau_{total}$ 的[分布](@entry_id:182848) [@problem_id:657084]：
$$
\tau_{total}(r) = \tau_{viscous}(r) + \tau_{turbulent}(r) = \left(\mu \frac{d\langle u_z \rangle}{dr}\right) + \left(-\rho \langle u'_z u'_r \rangle\right)
$$
通过对整个流体域进行[动量平衡](@entry_id:193575)分析，可以得到总应力 $\tau_{total}(r)$ 的精确解析表达式，即使我们对[粘性应力](@entry_id:261328)和[雷诺应力](@entry_id:263788)如何单独分配一无所知。这表明，总应力的概念在连接宏观驱动力（如压力梯度）和流动的内部力学状态方面起着核心作用，为[湍流建模](@entry_id:151192)提供了坚实的基础。