## 引言
[张量分析](@entry_id:161423)是[连续介质力学](@entry_id:155125)的数学基石，它提供了一个严谨且普适的框架来描述材料的变形、流动和应力。无论是在工程设计、[地球科学](@entry_id:749876)还是生物力学中，精确描述物质行为的能力都至关重要。然而，许多学习者常常在抽象的张量数学与具体的物理应用之间感到脱节。本文旨在弥合这一鸿沟，系统性地展示[张量分析](@entry_id:161423)如何成为理解和解决复杂力学问题的强大工具。

在接下来的内容中，我们将分三个章节展开探讨。首先，在“原理与机制”一章中，我们将建立[张量分析](@entry_id:161423)的核心理论，从其不依赖[坐标系](@entry_id:156346)的本质出发，系统介绍描述变形运动的运动学、关联力与应力的动力学，并深入到客观性和[材料对称性](@entry_id:190289)等高级概念。接着，在“应用与跨学科联系”一章中，我们将展示这些理论如何在[固体力学](@entry_id:164042)、波的传播、[材料稳定性](@entry_id:183933)和生物学等多个领域中发挥关键作用，将抽象概念与实际问题紧密相连。最后，通过“动手实践”部分，您将有机会通过解决具体问题来巩固所学知识，将理论真正内化为解决问题的能力。

## 原理与机制

本章旨在深入探讨连续介质力学中[张量分析](@entry_id:161423)的核心原理与机制。我们将从张量的基本定义出发，系统地建立描述物体变形与运动的运动学框架，进而关联到力与应力的[动力学平衡](@entry_id:187220)，最后探讨[本构关系](@entry_id:186508)建模中至关重要的高级概念，如客观性和[材料对称性](@entry_id:190289)。

### 张量的基本概念：超越矩阵的视角

在工程应用中，我们习惯于将向量和张量看作是分量的数组或矩阵。然而，从根本上讲，一个**张量 (tensor)** 是一个独立于任何特定[坐标系](@entry_id:156346)的几何或物理对象。这种抽象的定义是理解其在物理定律中扮演角色的关键。

以一个[二阶张量](@entry_id:199780)为例，它可以被严谨地定义为一个作用于两个矢量并返回一个标量的**[双线性映射](@entry_id:186502) (bilinear map)**。例如，一个 (0,2) 型张量 $\mathbf{T}$ 是一个函数 $\mathbf{T}: V \times V \to \mathbb{R}$，其中 $V$ 是一个三维欧几里得矢量空间。这个定义并未提及任何[基矢](@entry_id:199546)或坐标，因此 $\mathbf{T}$ 本身是一个**基无关 (basis-independent)** 的几何实体 [@problem_id:2922083]。

然而，为了进行计算，我们必须引入一个[坐标系](@entry_id:156346)。一旦我们选定一组[基矢](@entry_id:199546) $\{\mathbf{e}_i\}$，就可以通过张量在[基矢](@entry_id:199546)上的作用来定义其**分量 (components)**，即 $T_{ij} := \mathbf{T}(\mathbf{e}_i, \mathbf{e}_j)$。这些分量可以被[排列](@entry_id:136432)成一个 $3 \times 3$ 的矩阵。此时，一个关键的认知误区必须被澄清：张量不等于其分量矩阵。矩阵仅仅是张量在特定基下的“快照”或表示。

当[坐标基](@entry_id:270149)发生变化时，例如从 $\{\mathbf{e}_i\}$ 变为 $\{\mathbf{e}'_k\}$，其中 $\mathbf{e}'_k = P^i{}_k \mathbf{e}_i$ (这里 $\mathbf{P}$ 是[基变换矩阵](@entry_id:184480))，张量的分量也会相应地改变。对于 (0,2) 型张量 $\mathbf{T}$，其分量的变换规律是**协变 (covariant)** 的：
$$
T'_{kl} = P^i{}_k P^j{}_l T_{ij}
$$
这个变换规律确保了无论在哪种[坐标系](@entry_id:156346)下，由分量和[基矢](@entry_id:199546)重构出的物理实体始终是同一个张量 $\mathbf{T}$。不同类型的张量（例如 (1,1) 型或 (2,0) 型）遵循不同的变换规律。因此，即使两个不同类型的张量在某个特定基下的分量矩阵恰好相同，它们在基变换下的行为也会暴露其本质上的不同 [@problem_id:2922083]。

此外，矢量空间 $V$ 上的**[内积](@entry_id:158127) (inner product)** 或**[度规张量](@entry_id:160222) (metric tensor)** $\mathbf{g}$ 扮演着至关重要的角色。它不仅定义了矢量的长度和角度，还建立了一个在矢量空间 $V$ 与其[对偶空间](@entry_id:146945) $V^*$ 之间的规范同构。如果没有[内积](@entry_id:158127)，一个双线性形式 $\mathbf{T}$ (类型 (0,2)) 和一个[线性映射](@entry_id:185132) $\mathbf{A}: V \to V$ (类型 (1,1)) 是完全不同的对象。但在[内积](@entry_id:158127) $\mathbf{g}$ 存在且非退化的情况下，根据[里斯表示定理](@entry_id:140012)，我们可以唯一地将两者关联起来，使得 $\mathbf{T}(\mathbf{u},\mathbf{v}) = \mathbf{g}(\mathbf{A}\mathbf{u},\mathbf{v})$ 对所有 $\mathbf{u},\mathbf{v} \in V$ 成立。[度规张量](@entry_id:160222)的分量 $g_{ij}$ 及其逆 $g^{ij}$ 也被用来**[升降指标](@entry_id:161292) (raising and lowering indices)**，从而在张量的不同分量表示（[协变](@entry_id:634097)、逆变、混合）之间进行转换 [@problem_id:2922083]。

最后，对于**对称 (symmetric)** 的双线性形式 $\mathbf{T}$，即满足 $\mathbf{T}(\mathbf{u},\mathbf{v}) = \mathbf{T}(\mathbf{v},\mathbf{u})$，一个重要的代数定理保证了总能找到一个基，使得 $\mathbf{T}$ 在该基下的分量矩阵是对角的。这个过程本身并不需要[内积](@entry_id:158127)结构，尽管在引入[内积](@entry_id:158127)后，我们会得到更强的谱定理，即存在一个正交归一的基使自伴[算子对角化](@entry_id:141515) [@problem_id:2922083]。

### 变形[运动学](@entry_id:173318)：从参考构型到当前构型

连续介质力学的核心任务是描述物质点的运动和变形。我们引入一个**参考构型 (reference configuration)** $\mathcal{B}_0$，代表物体在某个初始时刻（通常是 $t=0$）的形状，其中的物[质点](@entry_id:186768)用物质坐标 $\mathbf{X}$ 标记。在 $t$ 时刻，物体运动到**当前构型 (current configuration)** $\mathcal{B}_t$，物质点 $\mathbf{X}$ 的空间位置由空间坐标 $\mathbf{x}$ 描述。

描述这一过程的数学工具是**变形映射 (deformation mapping)** $\mathbf{x} = \boldsymbol{\varphi}(\mathbf{X}, t)$。为保证物理上的合理性（物质不重叠或撕裂），该映射必须是光滑且可逆的 [@problem_id:2922110]。

#### 变形梯度张量

变形的核心度量是**变形梯度张量 (deformation gradient tensor)**，定义为变形映射对物质坐标的梯度：
$$
\mathbf{F}(\mathbf{X}, t) = \frac{\partial \boldsymbol{\varphi}}{\partial \mathbf{X}}
$$
$\mathbf{F}$ 是一个[二阶张量](@entry_id:199780)，它包含了关于局部变形的全部信息。其最直接的物理意义是：它将参考构型中一个无限小的物质线元 $\mathrm{d}\mathbf{X}$ [线性映射](@entry_id:185132)到当前构型中对应的空间线元 $\mathrm{d}\mathbf{x}$ [@problem_id:2922110]：
$$
\mathrm{d}\mathbf{x} = \mathbf{F} \, \mathrm{d}\mathbf{X}
$$
变形梯度还决定了面积和体积的变化。其[行列式](@entry_id:142978) $J = \det \mathbf{F}$，被称为**[雅可比行列式](@entry_id:137120) (Jacobian determinant)**，代表了局部的体积变化率：$\mathrm{d}v = J \, \mathrm{d}V$。物理上要求 $J > 0$，以确保物质的局部朝向不被翻转。参考构型中的面元 $\mathbf{N}\mathrm{d}A$ 通过**[南森公式](@entry_id:195566) (Nanson's formula)** 变换到当前构型的面元 $\mathbf{n}\mathrm{d}a$：
$$
\mathbf{n}\,\mathrm{d}a = J\,\mathbf{F}^{-\mathsf{T}}\,\mathbf{N}\,\mathrm{d}A
$$
其中 $\mathbf{F}^{-\mathsf{T}} = (\mathbf{F}^{-1})^{\mathsf{T}}$ 是 $\mathbf{F}$ 的逆转置 [@problem_id:2922110]。

#### 极分解与[应变张量](@entry_id:193332)

变形梯度 $\mathbf{F}$ 可以通过**极分解 (polar decomposition)** 分解为一个纯拉伸和一个纯[刚体转动](@entry_id:191086)的组合。这有两种形式：
$$
\mathbf{F} = \mathbf{R}\mathbf{U} = \mathbf{V}\mathbf{R}
$$
这里，$\mathbf{R}$ 是一个**转动张量 (rotation tensor)**（即 proper orthogonal tensor, $\mathbf{R}^{\mathsf{T}}\mathbf{R}=\mathbf{I}, \det\mathbf{R}=1$）。$\mathbf{U}$ 和 $\mathbf{V}$ 分别是**右[拉伸张量](@entry_id:193200) (right stretch tensor)** 和**左[拉伸张量](@entry_id:193200) (left stretch tensor)**，它们都是[对称正定](@entry_id:145886)张量。这种分解的物理图像非常清晰：$\mathbf{F} = \mathbf{R}\mathbf{U}$ 意味着变形过程可以看作是先在参考构型中进行纯拉伸 $\mathbf{U}$，然后再进行[刚体转动](@entry_id:191086) $\mathbf{R}$ 将其转到当前位置 [@problem_id:2922110]。

从 $\mathbf{F}$ 出发，我们可以定义纯粹度量应变的张量。其中最重要的是**右柯西-格林变形张量 (right Cauchy-Green deformation tensor)** $\mathbf{C}$ 和**左柯西-格林变形张量 (left Cauchy-Green deformation tensor)** $\mathbf{B}$：
$$
\mathbf{C} = \mathbf{F}^{\mathsf{T}}\mathbf{F} \quad \text{and} \quad \mathbf{B} = \mathbf{F}\mathbf{F}^{\mathsf{T}}
$$
$\mathbf{C}$ 和 $\mathbf{B}$ 都是对称正定张量，它们只包含变形的拉伸信息，而不含转动信息。可以证明，[拉伸张量](@entry_id:193200)是它们唯一的正定平方根：$\mathbf{U} = \sqrt{\mathbf{C}}$ 和 $\mathbf{V} = \sqrt{\mathbf{B}}$。对于纯刚体运动，$\mathbf{F}=\mathbf{R}$，此时 $\mathbf{C} = \mathbf{R}^{\mathsf{T}}\mathbf{R} = \mathbf{I}$，表明没有发生应变 [@problem_id:2922110]。

**示例：** 考虑一个齐次运动 $\mathbf{x} = \mathbf{F}\mathbf{X}$，其变形梯度为 [@problem_id:2922054]：
$$
\mathbf{F} = \begin{pmatrix} \sqrt{3}  & -3/4  & 0 \\ 1  & 3\sqrt{3}/4  & 0 \\ 0  & 0  & 1 \end{pmatrix}
$$
我们可以计算出[右柯西-格林张量](@entry_id:174156)：
$$
\mathbf{C} = \mathbf{F}^{\mathsf{T}}\mathbf{F} = \begin{pmatrix} 4  & 0  & 0 \\ 0  & 9/4  & 0 \\ 0  & 0  & 1 \end{pmatrix}
$$
由于 $\mathbf{C}$ 是对角阵，其正定平方根（右[拉伸张量](@entry_id:193200) $\mathbf{U}$）可以直接求得：
$$
\mathbf{U} = \sqrt{\mathbf{C}} = \begin{pmatrix} 2  & 0  & 0 \\ 0  & 3/2  & 0 \\ 0  & 0  & 1 \end{pmatrix}
$$
有了 $\mathbf{F}$ 和 $\mathbf{U}$，就可以通过 $\mathbf{R} = \mathbf{F}\mathbf{U}^{-1}$ 计算出转动张量：
$$
\mathbf{R} = \begin{pmatrix} \sqrt{3}/2  & -1/2  & 0 \\ 1/2  & \sqrt{3}/2  & 0 \\ 0  & 0  & 1 \end{pmatrix}
$$
这个矩阵代表绕 $X_3$ 轴逆时针旋转 $\theta = \pi/6$ [弧度](@entry_id:171693)。这个例子清晰地展示了如何将一个复杂的变形分解为纯拉伸和纯转动。

### [流动运动](@entry_id:184094)学：速率与流动

为了描述变形如何随[时间演化](@entry_id:153943)，我们需要引入速率的概念。

**欧拉[速度场](@entry_id:271461) (Eulerian velocity field)** $\mathbf{v}(\mathbf{x}, t)$ 描述了在时刻 $t$ 占据空间点 $\mathbf{x}$ 的物质点的速度。

一个物理量（如温度 $\theta$）跟随着一个特定物[质点](@entry_id:186768)变化的时间变化率由**[物质时间导数](@entry_id:190892) (material time derivative)** 给出，其公式为：
$$
\frac{D\theta}{Dt} = \frac{\partial \theta}{\partial t} + \mathbf{v} \cdot \nabla \theta
$$
第一项 $\frac{\partial \theta}{\partial t}$ 是在固定空间点上的[局部变化率](@entry_id:264961)，第二项 $\mathbf{v} \cdot \nabla \theta$ 是由物质点运动到具有不同 $\theta$ 值的位置而引起的**迁移 (advective)** 变化率 [@problem_id:2922107]。

[速度场](@entry_id:271461)在空间上的变化由**[速度梯度张量](@entry_id:270928) (velocity gradient tensor)** $\mathbf{L}$ 描述：
$$
\mathbf{L}(\mathbf{x}, t) = \nabla \mathbf{v} = \frac{\partial \mathbf{v}}{\partial \mathbf{x}}
$$
其分量为 $L_{ij} = \partial v_i / \partial x_j$。[速度梯度张量](@entry_id:270928)的物理意义在于，它线性地将两个邻近空间点之间的位置差矢量 $\mathrm{d}\mathbf{x}$ 映射为它们之间的相对速度矢量 $\mathrm{d}\mathbf{v}$：$\mathrm{d}\mathbf{v} \approx \mathbf{L}\,\mathrm{d}\mathbf{x}$ [@problem_id:2922111]。

[速度梯度张量](@entry_id:270928) $\mathbf{L}$ 可以唯一地分解为其对称[部分和](@entry_id:162077)反对称部分：
$$
\mathbf{L} = \mathbf{D} + \mathbf{W}
$$
其中，**应变率张量 (rate-of-deformation tensor)** $\mathbf{D} = \frac{1}{2}(\mathbf{L} + \mathbf{L}^{\mathsf{T}})$ 是对称的，它描述了物质微元的拉伸和[剪切变形](@entry_id:170920)速率。其迹 $\mathrm{tr}(\mathbf{D}) = \nabla \cdot \mathbf{v}$ 代表了[体积膨胀](@entry_id:144241)率。**[自旋张量](@entry_id:187346) (spin tensor)** $\mathbf{W} = \frac{1}{2}(\mathbf{L} - \mathbf{L}^{\mathsf{T}})$ 是反对称的，它描述了物质微元的[刚体转动](@entry_id:191086)[角速度](@entry_id:192539) [@problem_id:2922111]。对于一个纯[刚体运动](@entry_id:193355)，应变率为零 ($\mathbf{D}=\mathbf{0}$)，但[自旋张量](@entry_id:187346)非零 [@problem_id:2922111]。

这些概念可以通过一个具体的运动学例子来加深理解 [@problem_id:2922107]，例如一个叠加了拉伸、旋转和平移的齐次运动。通过计算可以发现，速度梯度 $\mathbf{L}$ 是由一个对称部分（来自拉伸 $\mathbf{S}(t)$）和一个反对称部分（来自旋转 $\mathbf{R}(t)$）相加而成，这正好对应了应变率张量 $\mathbf{D}$ 和[自旋张量](@entry_id:187346) $\mathbf{W}$。

### 动力学：力、应力与平衡定律

动力学研究力和运动之间的关系。在连续介质中，力分为两类：作用于整个体积的**体力 (body forces)**（如重力）和作用于物体表面的**面力 (surface forces)** 或**[接触力](@entry_id:165079) (contact forces)**。

#### 柯西[应力张量](@entry_id:148973)与[平衡方程](@entry_id:172166)

面力的概念通过**柯西应力张量 (Cauchy stress tensor)** $\boldsymbol{\sigma}$ 得以精确化。对于物体内任何一个假想的[截面](@entry_id:154995)，其法向为 $\mathbf{n}$，作用在该[截面](@entry_id:154995)单位面积上的力，即**牵[引力](@entry_id:175476)矢量 (traction vector)** $\mathbf{t}$，由**柯西公式 (Cauchy's formula)** 给出：
$$
\mathbf{t} = \boldsymbol{\sigma}\mathbf{n}
$$
$\boldsymbol{\sigma}$ 是一个[二阶张量](@entry_id:199780)，它完整地描述了物体内某一点的应力状态。

通过对任意一个物质子体应用[牛顿第二定律](@entry_id:274217)（[线性动量守恒](@entry_id:165717)），并结合柯西公式和[高斯散度定理](@entry_id:188065)，可以推导出其局部形式，即**柯西第一运动定律 (Cauchy's first law of motion)** 或[线性动量平衡](@entry_id:193575)方程 [@problem_id:2922066]：
$$
\rho\dot{\mathbf{v}} = \nabla \cdot \boldsymbol{\sigma} + \rho\mathbf{b}
$$
这里，$\rho$ 是密度，$\dot{\mathbf{v}}$ 是[物质加速度](@entry_id:270992)，$\mathbf{b}$ 是单位质量的体力。$\nabla \cdot \boldsymbol{\sigma}$ 是应力张量的**散度 (divergence)**，其物理意义是由于应力在空间上的不[均匀分布](@entry_id:194597)而产生的单位体积的净[内力](@entry_id:167605) [@problem_id:2922111]。对于静态平衡且无体力的情况，该方程简化为 $\nabla \cdot \boldsymbol{\sigma} = \mathbf{0}$ [@problem_id:2922111]。

类似地，对物质子体应用角动量守恒定律，可以推导出**柯西第二运动定律 (Cauchy's second law of motion)**。在经典（非极性）连续介质理论中，我们假设不存在体力矩和面力矩。在此假设下，[角动量守恒](@entry_id:156798)的局部形式要求柯西应力张量必须是**对称的 (symmetric)** [@problem_id:2922066]：
$$
\boldsymbol{\sigma} = \boldsymbol{\sigma}^{\mathsf{T}}
$$
这个对称性是力学中的一个基本结论，它将一个[二阶张量](@entry_id:199780)的9个独立分量减少到了6个。

### 深入专题：[张量分析](@entry_id:161423)在力学中的高级应用

#### 谱分解与[不变量](@entry_id:148850)

由于应力张量 $\boldsymbol{\sigma}$ 和柯西-格林[应变张量](@entry_id:193332) $\mathbf{C}$、$\mathbf{B}$ 都是对称的，它们具有重要的谱特性。对于任何一个实对称[二阶张量](@entry_id:199780) $\mathbf{A}$，总存在三个相互正交的**主方向 (principal directions)**（单位[特征向量](@entry_id:151813) $\mathbf{e}_i$）和对应的三个**[主值](@entry_id:189577) (principal values)**（实[特征值](@entry_id:154894) $\lambda_i$）。这意味着在以[主方向](@entry_id:276187)为基的[坐标系](@entry_id:156346)中，该张量的分量矩阵是对角阵：
$$
\mathbf{A} = \sum_{i=1}^3 \lambda_i \mathbf{e}_i \otimes \mathbf{e}_i
$$
在物理上，[主应力](@entry_id:176761)是作用在某一点上无剪应力的三个相互垂直平面上的[正应力](@entry_id:260622)，代表了该点的最大和最小[正应力](@entry_id:260622)。

与[特征值](@entry_id:154894)相关的是**[主不变量](@entry_id:193522) (principal invariants)**，它们是在[坐标旋转](@entry_id:164444)下保持不变的标量。对于一个[二阶张量](@entry_id:199780) $\mathbf{A}$，三个[主不变量](@entry_id:193522)是：
$$
\begin{align*}
I_1(\mathbf{A}) &= \mathrm{tr}(\mathbf{A}) = \lambda_1 + \lambda_2 + \lambda_3 \\
I_2(\mathbf{A}) &= \frac{1}{2}[(\mathrm{tr}(\mathbf{A}))^2 - \mathrm{tr}(\mathbf{A}^2)] = \lambda_1\lambda_2 + \lambda_2\lambda_3 + \lambda_3\lambda_1 \\
I_3(\mathbf{A}) &= \det(\mathbf{A}) = \lambda_1\lambda_2\lambda_3
\end{align*}
$$
这些[不变量](@entry_id:148850)既可以通过张量在任意[坐标系](@entry_id:156346)下的分量计算，也可以通过其[主值](@entry_id:189577)计算，结果必然相同 [@problem_id:2922091]。它们在建立不依赖于[坐标系](@entry_id:156346)的[本构关系](@entry_id:186508)中扮演着核心角色。

#### 客观性、标架无关性与[张量变换](@entry_id:183453)

物理定律和材料[本构关系](@entry_id:186508)应该独立于观察者的选择。这一原理被称为**客观性 (objectivity)** 或**标架无关性 (frame-indifference)**。数学上，它要求在叠加一个任意的刚体运动（由转动 $\mathbf{Q}(t)$ 和平移 $\mathbf{c}(t)$ 描述）后，物理量和方程的形式应保持不变。

为了精确地在不同构型或标架之间转换张量，我们引入**推前 (push-forward)** 和**[拉回](@entry_id:160816) (pull-back)** 运算。例如，一个参考构型中的矢量 $\mathbf{V}$ 被变形梯度 $\mathbf{F}$ **推前**到当前构型，成为 $\mathbf{v} = \mathbf{F}\mathbf{V}$。反之，一个当前构型中的矢量 $\mathbf{v}$ 被 $\mathbf{F}^{-1}$ **[拉回](@entry_id:160816)**到参考构型，成为 $\mathbf{V} = \mathbf{F}^{-1}\mathbf{v}$。不同类型的张量有不同的推前/[拉回](@entry_id:160816)法则，这些法则可以通过保持张量与矢量/[余矢量](@entry_id:157727)的缩并运算不变来推导 [@problem_id:2922144]。例如，一个协变二阶张量（如度规）$\mathbf{M}$ 的推前是 $\mathbf{m} = \mathbf{F}^{-\mathsf{T}} \mathbf{M} \mathbf{F}^{-1}$，而一个 (1,1) 型张量（如[线性映射](@entry_id:185132)）$\mathbf{A}$ 的推前是 $\mathbf{a} = \mathbf{F} \mathbf{A} \mathbf{F}^{-1}$。

在客观性分析中，我们发现并非所有运动学和动力学量都是客观的。例如，变形梯度 $\mathbf{F}$ 在叠加一个[刚体转动](@entry_id:191086) $\mathbf{Q}$ 后会变为 $\mathbf{F}^* = \mathbf{Q}\mathbf{F}$，因此它不是客观的。然而，[右柯西-格林张量](@entry_id:174156) $\mathbf{C} = \mathbf{F}^{\mathsf{T}}\mathbf{F}$ 在此变换下保持不变（$\mathbf{C}^* = (\mathbf{Q}\mathbf{F})^{\mathsf{T}}(\mathbf{Q}\mathbf{F}) = \mathbf{F}^{\mathsf{T}}\mathbf{Q}^{\mathsf{T}}\mathbf{Q}\mathbf{F} = \mathbf{F}^{\mathsf{T}}\mathbf{F} = \mathbf{C}$），所以它是客观的[应变度量](@entry_id:755495) [@problem_id:2922110]。

一个更微妙的问题出现在时间导数上。柯西应力张量 $\boldsymbol{\sigma}$ 是客观的（变换为 $\boldsymbol{\sigma}^* = \mathbf{Q}\boldsymbol{\sigma}\mathbf{Q}^{\mathsf{T}}$），但它的简单[物质时间导数](@entry_id:190892) $\dot{\boldsymbol{\sigma}}$ 却不是客观的。一个简单的思想实验可以证明这一点：考虑一个处于恒定应力状态的物体，如果观察者自身在旋转，即使物体本身没有任何变化，该旋转观察者也会测量到一个非零的应力变化率 $\dot{\boldsymbol{\sigma}}^* \neq \mathbf{0}$ [@problem_id:2922125]。

为了在率型本构关系（即应力率与应变率的关系）中保持客观性，必须使用**[客观时间导数](@entry_id:189677) (objective time rates)** 或**同旋率 (corotational rates)**。这些导数通过减去由[刚体转动](@entry_id:191086)引起的虚假变化率来修正简单的时间导数。一个常见的例子是**Jaumann率 (Jaumann rate)**：
$$
\overset{\triangle}{\boldsymbol{\sigma}} = \dot{\boldsymbol{\sigma}} - \mathbf{W}\boldsymbol{\sigma} + \boldsymbol{\sigma}\mathbf{W}
$$
其中 $\mathbf{W}$ 是[自旋张量](@entry_id:187346)。可以证明，Jaumann率是客观的，因此可以用于构建符合物理原理的[本构方程](@entry_id:138559) [@problem_id:2922125]。

#### [各向同性张量](@entry_id:195105)函数

材料的**各向同性 (isotropy)** 是指其物理性质不随方向改变。对于一个将[对称张量](@entry_id:148092) $\mathbf{A}$（如应变张量）映射到对称张量 $\mathbf{B}$（如应力张量）的本构函数 $\mathbf{B} = f(\mathbf{A})$，各向同性的数学定义是，对于任意正交变换 $\mathbf{Q}$，该函数满足**等价性 (equivariance)** 条件 [@problem_id:2922127]：
$$
\mathbf{Q}f(\mathbf{A})\mathbf{Q}^{\mathsf{T}} = f(\mathbf{Q}\mathbf{A}\mathbf{Q}^{\mathsf{T}})
$$
这个条件的一个直接推论是，张量 $\mathbf{A}$ 和其函数值 $f(\mathbf{A})$ 必须是**共轴 (coaxial)** 的，即它们拥有相同的主方向。这也意味着它们必然**交换 (commute)**：$f(\mathbf{A})\mathbf{A} = \mathbf{A}f(\mathbf{A})$ [@problem_id:2922127]。

关于[各向同性张量](@entry_id:195105)函数，一个极为强大的结果是**里夫林-埃里克森[表示定理](@entry_id:637872) (Rivlin-Ericksen representation theorem)**。该定理指出，任何光滑的、各向同性的[对称张量](@entry_id:148092)函数 $f(\mathbf{A})$ 都可以表示为 $\mathbf{I}$, $\mathbf{A}$, 和 $\mathbf{A}^2$ 的[线性组合](@entry_id:154743) [@problem_id:2922127]：
$$
f(\mathbf{A}) = \alpha_0 \mathbf{I} + \alpha_1 \mathbf{A} + \alpha_2 \mathbf{A}^2
$$
其中的标量系数 $\alpha_0, \alpha_1, \alpha_2$ 仅仅是 $\mathbf{A}$ 的三个[主不变量](@entry_id:193522) $I_1, I_2, I_3$ 的函数。这个定理是建立弹性、塑性和流体本构模型的基础，它极大地简化了描述各向同性材料行为所需的函数形式。