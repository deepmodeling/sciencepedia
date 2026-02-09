## 引言
在连续介质力学中，精确描述物体的运动是理解其变形、应力和失效行为的出发点。与刚体仅涉及平移和旋转不同，可变形体（如受载的桥梁、流动的河水或生长的生物组织）内部各点会经历复杂的相对位移，导致其形状和尺寸的改变。为了量化这些变化，我们需要一个比日常直觉更严谨的数学框架，而这正是本文将要探讨的核心问题：如何建立一个能够描述任意连续体运动的普适性语言。

本文旨在系统地介绍并区分两种描述运动的基本方法：物质描述（拉格朗日法）和空间描述（欧拉法）。我们将揭示这两种看似不同的视角如何通过变形梯度等核心概念紧密联系在一起，并共同构成分析变形的基础。读者将通过本文学习到：

在“原理与机制”一章中，我们将定义物质坐标与空间坐标，引入变形梯度、有限应变张量以及速度梯度等关键运动学量，并阐明质量守恒等基本物理原理在这一框架下的数学表达。

接着，在“应用与交叉学科联系”一章中，我们将展示这些理论概念如何在固体力学、流体力学、计算方法乃至生物力学等领域中发挥作用，探讨如何根据问题特性选择合适的描述方法，并解决诸如客观性和各向异性等高级问题。

最后，在“动手实践”部分，读者将有机会通过具体问题，亲手计算和应用前述概念，从而巩固和深化对连续介质运动学的理解。

现在，让我们从最基本的概念开始，进入“原理与机制”的世界，学习如何为连续体中的每一个点建立运动的数学描述。

## 原理与机制

在连续介质力学中，对物体运动的描述是分析其变形和受力的基础。与刚体运动不同，可变形体的不同部分会经历不同的位移，导致其形状和体积发生改变。为了精确地量化这些变化，我们需要建立一个严谨的运动学框架。本章将系统地阐述描述连续体运动的两种基本视角——物质描述和空间描述，并在此基础上引入变形、应变和运动速率的关键度量。

### 运动的描述：物质坐标与空间坐标

为了追踪一个可变形体中每一个点的运动，我们首先需要一种方法来唯一地标记这些点。为此，我们选取一个特定的时刻（通常是 $t=0$）下物体所占据的构型作为**参考构型**，记作 $\Omega_0$。物体中的任意一个物质点可以通过其在参考构型中的位置向量 $\mathbf{X}$ 来进行永久性的标记。这个向量 $\mathbf{X}$ 被称为该物质点的**物质坐标**或**拉格朗日坐标 (Lagrangian coordinate)**。它就像是分配给每个物质点的“身份证号码”，在整个运动过程中保持不变。

随着时间的推移，物体运动并变形，在时刻 $t$ 占据了**当前构型** $\Omega_t$。同一个物质点 $\mathbf{X}$ 在时刻 $t$ 的空间位置由另一个位置向量 $\mathbf{x}$ 给出，该向量被称为**空间坐标**或**欧拉坐标 (Eulerian coordinate)**。

因此，物体的运动可以被描述为一个映射关系 $\boldsymbol{\chi}$，它将每个物质点的标签 $\mathbf{X}$ 和时间 $t$ 映射到其当前的空间位置 $\mathbf{x}$：
$$
\mathbf{x} = \boldsymbol{\chi}(\mathbf{X}, t)
$$
这个函数 $\boldsymbol{\chi}$ 被称为**运动函数**。对于一个物理上可行的运动，我们要求在任意时刻 $t$，映射 $\boldsymbol{\chi}(\cdot, t)$ 都是一个从 $\Omega_0$ 到 $\Omega_t$ 的一一对应（双射），并且保持了物质的朝向。这意味着：
1.  **物质不可入性**：不同的物质点在同一时刻不能占据相同的空间位置（映射是单射的）。
2.  **连续性与可逆性**：物质点不能凭空出现或消失，并且可以从当前位置追溯其初始位置（映射是连续且可逆的）。
3.  **保向性**：物质微元的局部朝向不会被翻转（例如，一个右手坐标系微元不会变成左手坐标系）。[@problem_id:2657166]

基于这两种坐标系，任何与物体相关的物理场（如温度、密度或位移）都可以用两种方式来描述 [@problem_id:2657169]：

*   **物质描述（拉格朗日描述）**：将物理量的值与物质点 $\mathbf{X}$ 相关联。例如，温度场可以表示为一个函数 $A(\mathbf{X}, t)$。这种描述就像是给每个物质点配备一个传感器，追踪该特定点上的物理量随时间的变化。其定义域是参考构型与时间区间的笛卡尔积 $\Omega_0 \times I$。

*   **空间描述（欧拉描述）**：将物理量的值与空间点 $\mathbf{x}$ 相关联。例如，温度场可以表示为 $a(\mathbf{x}, t)$。这种描述就像是在空间中设置固定的监测站，记录流经该站点的不同物质点在不同时刻所展现的物理量。其定义域是随时间变化的当前构型 $\Omega_t$。

这两种描述描述的是同一个物理现实，因此它们必然是等价的。它们之间的转换通过运动函数 $\boldsymbol{\chi}$ 实现。在时刻 $t$，位于空间点 $\mathbf{x}$ 的物质点是 $\mathbf{X} = \boldsymbol{\chi}^{-1}(\mathbf{x}, t)$。因此，空间场在该点的值必须等于物质场在该物质点的值：
$$
a(\mathbf{x}, t) = A(\boldsymbol{\chi}^{-1}(\mathbf{x}, t), t)
$$
反之，物质点 $\mathbf{X}$ 在时刻 $t$ 的温度也可以通过查询其当前位置 $\mathbf{x} = \boldsymbol{\chi}(\mathbf{X}, t)$ 处的空间温度场来获得：
$$
A(\mathbf{X}, t) = a(\boldsymbol{\chi}(\mathbf{X}, t), t)
$$

### 变形梯度：局部变形的线性度量

为了量化物体局部的变形情况，我们引入一个核心的运动学量——**变形梯度 (deformation gradient)**。考虑参考构型中一个点 $\mathbf{X}$ 及其一个无限接近的邻点 $\mathbf{X} + d\mathbf{X}$。在当前构型中，它们分别被映射到 $\mathbf{x} = \boldsymbol{\chi}(\mathbf{X}, t)$ 和 $\mathbf{x} + d\mathbf{x} = \boldsymbol{\chi}(\mathbf{X} + d\mathbf{X}, t)$。对运动函数在 $\mathbf{X}$ 处进行泰勒展开，我们得到：
$$
\boldsymbol{\chi}(\mathbf{X} + d\mathbf{X}, t) \approx \boldsymbol{\chi}(\mathbf{X}, t) + \frac{\partial \boldsymbol{\chi}}{\partial \mathbf{X}}(\mathbf{X}, t) d\mathbf{X}
$$
这揭示了微小的物质线元 $d\mathbf{X}$ 与其变形后的空间线元 $d\mathbf{x}$ 之间的线性关系：
$$
d\mathbf{x} = \mathbf{F}(\mathbf{X}, t) d\mathbf{X}
$$
其中，二阶张量 $\mathbf{F}(\mathbf{X}, t) = \nabla_{\mathbf{X}} \boldsymbol{\chi}(\mathbf{X}, t)$ 被定义为变形梯度。它的分量形式为 $F_{iA} = \partial x_i / \partial X_A$。变形梯度 $\mathbf{F}$ 是一个两点张量 (two-point tensor)，它将参考构型中的矢量映射到当前构型中。它完整地描述了一个物质点邻域内的局部变形，包括拉伸、剪切和旋转。[@problem_id:2657139]

变形梯度的行列式，即**雅可比行列式 (Jacobian)** $J = \det \mathbf{F}$，具有明确的几何意义。它描述了体积的局部变化率。一个在参考构型中体积为 $dV_0$ 的微元，在变形后其体积 $dv$ 变为：
$$
dv = J \, dV_0
$$
物理上，物质不能被压缩至零体积或被“翻转”成负体积。因此，对于任何物理上可行的运动，必须始终满足 $J > 0$。这个条件保证了运动的局部可逆性和保向性。[@problem_id:2657166]

利用变形梯度，我们还可以推导其他重要的几何关系，例如面积微元的变化规律，这由著名的**南森公式 (Nanson's formula)** 给出：
$$
d a \, \mathbf{n} = J \, \mathbf{F}^{-\mathsf{T}} (d A \, \mathbf{N})
$$
这里 $(dA, \mathbf{N})$ 和 $(da, \mathbf{n})$ 分别是参考构型和当前构型中面积微元的面积和单位法向量。此外，通过链式法则可以证明，逆运动的梯度等于变形梯度的逆，即 $\nabla_{\mathbf{x}} \mathbf{X} = \mathbf{F}^{-1}$。[@problem_id:2657139]

### 运动学：速度、加速度与物质时间导数

描述运动不仅需要知道位置的变化，还需要知道变化的速率。物质点 $\mathbf{X}$ 的**物质速度 (material velocity)** 定义为：
$$
\mathbf{V}(\mathbf{X}, t) = \frac{\partial \boldsymbol{\chi}}{\partial t}(\mathbf{X}, t)
$$
这是在拉格朗日框架下，固定物质点 $\mathbf{X}$ 对时间求导。而在欧拉框架下，我们更关心在空间点 $\mathbf{x}$ 的速度，即**空间速度 (spatial velocity)** $\mathbf{v}(\mathbf{x}, t)$。它是指在时刻 $t$ 占据空间点 $\mathbf{x}$ 的那个物质点的速度。因此，两者关系为：
$$
\mathbf{v}(\boldsymbol{\chi}(\mathbf{X}, t), t) = \mathbf{V}(\mathbf{X}, t)
$$

一个核心问题是如何计算一个随物质点运动的物理量的变化率。例如，一个随波逐流的木块所感受到的水温变化率是多少？这个变化率由两部分组成：一是水温本身可能随时间变化（例如太阳升起）；二是因为木块漂到了一个水温不同的新位置。为了形式化这个概念，我们定义**物质时间导数 (material time derivative)**，通常记为 $\dot{\phi}$ 或 $D\phi/Dt$。它表示跟随着一个特定物质点所观察到的物理场 $\phi$ 的变化率。

对于一个空间场 $\phi(\mathbf{x}, t)$，其物质时间导数的定义是：
$$
\dot{\phi} = \frac{d}{dt} \phi(\boldsymbol{\chi}(\mathbf{X}, t), t)
$$
利用多元函数的链式法则，我们可以将其展开为纯粹用空间量表达的形式 [@problem_id:2657177]：
$$
\dot{\phi} = \frac{\partial \phi}{\partial t} + (\nabla_{\mathbf{x}}\phi) \cdot \mathbf{v}
$$
这个重要的公式被称为**雷诺输运定理 (Reynolds transport theorem)** 的基础，它将拉格朗日视角的变化率（左侧）与欧拉视角下的量（右侧）联系起来。右侧的两项有明确的物理意义：
*   $\dfrac{\partial \phi}{\partial t}$ 是**局部变化率 (local rate of change)**，表示在空间固定点 $\mathbf{x}$ 处观察到的场的变化。
*   $(\nabla_{\mathbf{x}}\phi) \cdot \mathbf{v}$ 是**对流变化率 (convective rate of change)**，表示由于物质点运动到场值不同的新位置所引起的变化。

物质点的加速度 $\mathbf{a}$ 就是其速度的物质时间导数。将上述公式应用于空间速度场 $\mathbf{v}(\mathbf{x},t)$，我们得到物质加速度的欧拉表达式 [@problem_id:2657199]：
$$
\mathbf{a}(\mathbf{x}, t) = \frac{D\mathbf{v}}{Dt} = \frac{\partial \mathbf{v}}{\partial t} + (\nabla_{\mathbf{x}}\mathbf{v})\mathbf{v}
$$
其中，$\nabla_{\mathbf{x}}\mathbf{v}$ 是空间速度梯度，我们将在下一节详细讨论。

### 应变率与应变度量

变形的速率由空间速度场 $\mathbf{v}(\mathbf{x}, t)$ 的空间分布决定。**空间速度梯度 (spatial velocity gradient)** $\mathbf{L} = \nabla_{\mathbf{x}}\mathbf{v}$ 是描述这一分布的核心张量。它与变形梯度的物质时间导数 $\dot{\mathbf{F}}$ 之间存在一个基本关系 [@problem_id:2657199]：
$$
\dot{\mathbf{F}} = \mathbf{L} \mathbf{F}
$$
这个关系表明，变形梯度的变化率可以由当前的速度梯度和当前的变形状态共同确定。

速度梯度 $\mathbf{L}$ 可以唯一地分解为其对称部分和反对称部分：
$$
\mathbf{L} = \mathbf{D} + \mathbf{W}
$$
其中，
*   $\mathbf{D} = \frac{1}{2}(\mathbf{L} + \mathbf{L}^{\mathsf{T}})$ 被称为**变形率张量 (rate of deformation tensor)** 或伸长率张量。
*   $\mathbf{W} = \frac{1}{2}(\mathbf{L} - \mathbf{L}^{\mathsf{T}})$ 被称为**自旋张量 (spin tensor)** 或涡量张量。

这个分解具有深刻的物理意义 [@problem_id:2657230]。变形率张量 $\mathbf{D}$ 描述了物质线元的伸长率和物质微元夹角的变化率，即纯粹的变形速率。而自旋张量 $\mathbf{W}$ 描述了物质微元的刚性转动速率，它与变形无关。可以证明，物质线元长度平方的变化率仅由 $\mathbf{D}$ 决定：
$$
\frac{d}{dt}(d\mathbf{x} \cdot d\mathbf{x}) = 2 \, d\mathbf{x} \cdot \mathbf{D} \, d\mathbf{x}
$$
这表明，在非极性介质中，只有引起变形的变形率张量 $\mathbf{D}$ 才与应力做功有关，而刚性转动（由 $\mathbf{W}$ 描述）不产生内力功，即应力功率密度为 $\boldsymbol{\sigma}:\mathbf{D}$。

以上描述的是变形的“率”，而要度量从参考构型到当前构型的总变形量，我们需要引入**有限应变张量 (finite strain tensors)**。任何一个合理的应变度量都必须满足一个基本要求：对于纯刚体运动（只有平移和旋转，没有形状改变），应变必须为零。

我们可以从线元长度的平方变化出发来定义应变。长度平方的变化量为 $d\mathbf{x} \cdot d\mathbf{x} - d\mathbf{X} \cdot d\mathbf{X}$。

*   用物质坐标表达该变化量 [@problem_id:2657136]：
    $$
    d\mathbf{x} \cdot d\mathbf{x} - d\mathbf{X} \cdot d\mathbf{X} = d\mathbf{X} \cdot (\mathbf{F}^{\mathsf{T}}\mathbf{F} - \mathbf{I}) d\mathbf{X}
    $$
    我们定义**格林-拉格朗日应变张量 (Green-Lagrange strain tensor)** $\mathbf{E}$ 为：
    $$
    \mathbf{E} = \frac{1}{2}(\mathbf{F}^{\mathsf{T}}\mathbf{F} - \mathbf{I}) = \frac{1}{2}(\mathbf{C} - \mathbf{I})
    $$
    其中 $\mathbf{C} = \mathbf{F}^{\mathsf{T}}\mathbf{F}$ 是**右柯西-格林变形张量 (Right Cauchy-Green deformation tensor)**。$\mathbf{E}$ 是一个物质张量，它在参考构型上度量应变。

*   用空间坐标表达该变化量 [@problem_id:2657136]：
    $$
    d\mathbf{x} \cdot d\mathbf{x} - d\mathbf{X} \cdot d\mathbf{X} = d\mathbf{x} \cdot (\mathbf{I} - \mathbf{F}^{-\mathsf{T}}\mathbf{F}^{-1}) d\mathbf{x}
    $$
    我们定义**欧拉-阿尔曼西应变张量 (Euler-Almansi strain tensor)** $\mathbf{e}$ 为：
    $$
    \mathbf{e} = \frac{1}{2}(\mathbf{I} - \mathbf{F}^{-\mathsf{T}}\mathbf{F}^{-1}) = \frac{1}{2}(\mathbf{I} - \mathbf{b}^{-1})
    $$
    其中 $\mathbf{b} = \mathbf{F}\mathbf{F}^{\mathsf{T}}$ 是**左柯西-格林变形张量 (Left Cauchy-Green deformation tensor)**（也称 Finger 张量）。$\mathbf{e}$ 是一个空间张量，它在当前构型上度量应变。

这两个应变张量都是客观的（在刚体运动叠加下有正确的张量变换规律），并且在小位移梯度下，它们都退化为经典的**无穷小应变张量 (infinitesimal strain tensor)** $\boldsymbol{\varepsilon} = \frac{1}{2}(\nabla \mathbf{u} + (\nabla \mathbf{u})^{\mathsf{T}})$。[@problem_id:2657136]

### 运动的分解与主伸长

变形梯度 $\mathbf{F}$ 包含了物质微元从参考构型到当前构型的全部几何信息，包括拉伸和旋转。**极分解定理 (Polar Decomposition Theorem)** 提供了一种将这两种效应分离开来的有力工具。该定理指出，任何可逆的变形梯度 $\mathbf{F}$ (即 $\det \mathbf{F} \neq 0$) 都可以唯一地分解为：
$$
\mathbf{F} = \mathbf{R}\mathbf{U} = \mathbf{V}\mathbf{R}
$$
其中：
*   $\mathbf{R}$ 是一个正交张量 ($\mathbf{R}^{\mathsf{T}}\mathbf{R}=\mathbf{I}$)，代表局部刚体旋转。若 $\det \mathbf{F} > 0$，则 $\det \mathbf{R} = +1$，$\mathbf{R}$ 是一个纯旋转。
*   $\mathbf{U}$ 和 $\mathbf{V}$ 是对称正定张量，分别称为**右伸长张量 (right stretch tensor)** 和**左伸长张量 (left stretch tensor)**。它们描述了纯粹的拉伸变形。

$\mathbf{U}$ 和 $\mathbf{V}$ 与柯西-格林张量密切相关：$\mathbf{U} = \sqrt{\mathbf{C}} = \sqrt{\mathbf{F}^{\mathsf{T}}\mathbf{F}}$，而 $\mathbf{V} = \sqrt{\mathbf{b}} = \sqrt{\mathbf{F}\mathbf{F}^{\mathsf{T}}}$。$\mathbf{U}$ 作用于参考构型，而 $\mathbf{V}$ 作用于当前构型。

伸长张量 $\mathbf{U}$ 和 $\mathbf{V}$ 是共轭的（$\mathbf{V} = \mathbf{R}\mathbf{U}\mathbf{R}^{\mathsf{T}}$），因此它们具有相同的特征值。这些特征值，记为 $\lambda_1, \lambda_2, \lambda_3$，被称为**主伸长 (principal stretches)**。它们代表了三个相互正交的方向上物质线元长度的伸长比。由于 $\mathbf{U}^2 = \mathbf{C}$，主伸长 $\lambda_i$ 等于右柯西-格林张量 $\mathbf{C}$ 特征值的平方根。

例如，给定一个变形梯度 [@problem_id:2657223]：
$$
\mathbf{F}=\begin{pmatrix}
1.2  0.6  0 \\
0  1.5  0 \\
0  0  1.1
\end{pmatrix}
$$
我们可以计算出 $\mathbf{C} = \mathbf{F}^{\mathsf{T}}\mathbf{F}$ 的特征值为 $\{2.953, 1.097, 1.21\}$。对这些值取平方根，就得到三个主伸长，它们组成的无序集合为 $\{1.718, 1.048, 1.100\}$。这组数值完全刻画了该点变形的拉伸程度，而不受刚体转动的影响。

### 质量守恒原理

质量守恒是所有物理理论的基本公理之一。在连续介质力学中，它断言任何一个物质体（由同一群物质点构成）的总质量在运动过程中保持不变。

从这个基本公理出发，可以推导出两种等价的局部数学表达式：

1.  **物质形式（拉格朗日形式）**：考虑一个质量为 $dm$ 的物质微元。在参考构型中，其体积为 $dV_0$，密度为 $\rho_0(\mathbf{X})$，因此 $dm = \rho_0 dV_0$。在当前构型中，该微元的体积变为 $dv = J dV_0$，密度为 $\rho(\mathbf{x}, t)$，因此 $dm = \rho dv = \rho J dV_0$。由于质量守恒，我们得到一个简单的代数关系 [@problem_id:2657137] [@problem_id:2657139]：
    $$
    \rho_0(\mathbf{X}) = \rho(\boldsymbol{\chi}(\mathbf{X}, t), t) J(\mathbf{X}, t)
    $$
    或简记为 $\rho_0 = \rho J$。这个关系表明，当前密度与参考密度的比值等于体积变化的倒数。

2.  **空间形式（欧拉形式）**：通过对任意物质体积应用雷诺输运定理，可以得到一个偏微分方程，即**连续性方程 (continuity equation)**：
    $$
    \frac{\partial \rho}{\partial t} + \nabla_{\mathbf{x}} \cdot (\rho \mathbf{v}) = 0
    $$
    利用物质时间导数的定义，上式可以写为：
    $$
    \frac{D\rho}{Dt} + \rho (\nabla_{\mathbf{x}} \cdot \mathbf{v}) = 0 \quad \text{或} \quad \dot{\rho} + \rho \operatorname{div}(\mathbf{v}) = 0
    $$

这两种形式是完全等价的。我们可以通过对物质形式 $\rho_0 = \rho J$ 求物质时间导数来证明这一点。由于 $\rho_0(\mathbf{X})$ 对一个给定的物质点来说是常数，其物质时间导数为零：
$$
\frac{d}{dt}(\rho J) = \dot{\rho} J + \rho \dot{J} = 0
$$
这里需要用到雅可比行列式 $J$ 的物质时间导数与速度散度之间的关键运动学恒等式：$\dot{J} = J \operatorname{div}(\mathbf{v})$。代入上式并除以 $J$（因为 $J>0$），我们便得到了空间形式的连续性方程。这一推导优美地展示了物质描述和空间描述之间的内在联系。[@problem_id:2657137]

对于**不可压缩 (incompressible)** 材料，其定义是任何物质点的密度在运动中保持不变，即 $\dot{\rho}=0$。根据连续性方程，这等价于空间速度场是无散的：
$$
\operatorname{div}(\mathbf{v}) = \operatorname{tr}(\mathbf{L}) = \operatorname{tr}(\mathbf{D}) = 0
$$
这也意味着对于不可压缩运动，雅可比行列式 $J$ 保持为 1，即运动是保体积的。[@problem_id:2657199]

### 变形的相容性

到目前为止，我们都从一个给定的运动 $\boldsymbol{\chi}(\mathbf{X})$ 出发，推导出变形梯度 $\mathbf{F} = \nabla \boldsymbol{\chi}$ 及其他运动学量。现在我们考虑一个逆问题：给定一个在物体上定义的二阶张量场 $\mathbf{F}(\mathbf{X})$，它是否能代表一个真实的、连续的单值运动？

换言之，是否存在一个单值的位移场 $\mathbf{u}(\mathbf{X})$，使得 $\mathbf{F} = \mathbf{I} + \nabla \mathbf{u}$？如果存在，我们称 $\mathbf{F}$ 是**相容的 (compatible)**。

这个问题的答案源于向量分析中的一个基本事实：一个向量场的旋度为零，是该向量场可以表示为某个标量场的梯度的必要条件。将此思想逐行应用于变形梯度 $\mathbf{F}$，如果 $\mathbf{F}$ 是某个向量场 $\boldsymbol{\chi}$ 的梯度，那么其混合偏导数必须相等，即 $\partial F_{iA}/\partial X_B = \partial^2 \chi_i / \partial X_B \partial X_A = \partial F_{iB}/\partial X_A$。这等价于 $\mathbf{F}$ 的物质**旋度 (Curl)** 为零 [@problem_id:2657157]：
$$
\operatorname{Curl}_{\mathbf{X}} \mathbf{F} = \mathbf{0}
$$
其中，旋度算子作用于张量的每一行。

这个条件是相容性的**必要**条件。根据斯托克斯定理的推广，如果物体占据的区域是**单连通 (simply connected)** 的（即内部没有“洞”），那么 $\operatorname{Curl}_{\mathbf{X}} \mathbf{F} = \mathbf{0}$ 也是**充分**条件。它保证了通过对 $\mathbf{F}$ 进行路径积分来定义的运动 $\boldsymbol{\chi}$ 是单值的，与积分路径无关。
$$
\boldsymbol{\chi}(\mathbf{X}) = \boldsymbol{\chi}(\mathbf{X}_0) + \int_{\mathbf{X}_0}^{\mathbf{X}} \mathbf{F}(\mathbf{X}') d\mathbf{X}'
$$
因此，在单连通域中，$\operatorname{Curl}_{\mathbf{X}} \mathbf{F} = \mathbf{0}$ 确保了一个给定的变形梯度场可以被“积分”成一个连续的、物理上可能的位移场。如果这个条件不满足，就意味着所描述的“变形”会在材料内部产生裂缝或重叠，这在经典连续介质力学中是不允许的。[@problem_id:2657157]