## 引言
为了精确描述和预测一个物体在受力后的运动、变形乃至失效，连续介质力学建立了一套严谨的数学框架。这个框架的核心挑战在于：我们既需要追踪物体内部每一个“物质点”的独特经历，又需要在固定的空间中描述温度、应力等物理场的分布。解决这一挑战的关键，便是清晰地区分并关联两种基本坐标系：用于标记物质点身份的**物质坐标**（拉格朗日坐标）和用于描述其瞬时位置的**空间坐标**（欧拉坐标）。掌握这两种坐标系及其转换法则是理解所有后续高级概念（如应变、应力、本构关系）的先决条件。

本文旨在系统性地构建这一运动学基础。我们将从第一章**“原理与机制”**开始，详细阐述物质与空间坐标的定义，引入连接两者的核心工具——变形梯度张量，并由此推导出各种应变和应力度量，以及它们在不同坐标系下的转换法则。随后，在第二章**“应用与交叉学科联系”**中，我们将展示这些抽象的理论如何在计算固体力学、有限元分析、断裂力学、生物力学乃至宇宙学等前沿领域中发挥关键作用，将数学概念与实际工程和科学问题联系起来。最后，通过第三章**“动手实践”**提供的一系列计算和编程问题，读者将有机会亲手应用所学知识，将理论理解转化为解决问题的实践能力。

## 原理与机制

在连续介质力学中，为了描述一个物体从初始状态到变形后状态的运动，我们必须建立一个严谨的运动学框架。该框架的核心在于区分和关联两种不同的坐标系：一种用于标记物质微团本身，不随时间改变；另一种用于描述这些微团在空间中的瞬时位置。本章将系统地阐述这些基本原理与机制，它们是后续学习应力、应变和本构关系的基础。

### 运动学描述：物质与空间坐标

为了精确描述一个变形体，我们首先引入**物质体** $\mathcal{B}$ 的概念，它是一个由物质点（或粒子）组成的抽象集合。在任意时刻 $t$，这些物质点在三维欧几里得空间 $\mathbb{R}^3$ 中占据一个特定的区域。

我们选择一个特定的时刻（通常是 $t=0$）作为参考，此时物体所占据的空间区域被称为**参考构型**，记作 $\mathcal{B}_0$。参考构型中的任意一点的位置矢量，我们用 $\boldsymbol{X}$ 表示，它被称为**物质坐标**或**拉格朗日坐标 (Lagrangian coordinate)**。至关重要的是，物质坐标 $\boldsymbol{X}$ 是一个物质点的永久“标签”，它不随时间变化。一旦一个物质点被赋予了坐标 $\boldsymbol{X}$，这个 $\boldsymbol{X}$ 就始终标识着这同一个物质点。

随着时间的推移，物体发生运动和变形。在任意时刻 $t$，物体占据的空间区域被称为**当前构型**，记作 $\mathcal{B}_t$。最初位于 $\boldsymbol{X}$ 的物质点，在时刻 $t$ 会移动到一个新的空间位置，其位置矢量我们用 $\boldsymbol{x}$ 表示，它被称为**空间坐标**或**欧拉坐标 (Eulerian coordinate)**。显然，$\boldsymbol{x}$ 是时间和该物质点标签 $\boldsymbol{X}$ 的函数。

连接这两种坐标描述的是**运动映射** $\boldsymbol{\varphi}$。它将每个物质点的标签 $\boldsymbol{X}$ 映射到其在时刻 $t$ 的空间位置 $\boldsymbol{x}$：
$$ \boldsymbol{x} = \boldsymbol{\varphi}(\boldsymbol{X}, t) $$
为了保证物理上的合理性，运动映射 $\boldsymbol{\varphi}$ 必须满足几个关键条件。首先，它必须是**连续可微**的，以确保速度、加速度等物理量有良好定义。其次，在任意固定时刻 $t$，映射 $\boldsymbol{\varphi}(\cdot, t): \mathcal{B}_0 \to \mathcal{B}_t$ 必须是**双射**的，即一一对应。这意味着每个物质点在当前构型中都有一个唯一的位置，同时空间中的每个被占据的点都只对应一个物质点。这体现了**物质不可入性**的基本公设：两个不同的物质点不能同时占据同一个空间位置。最后，映射必须**保持定向**，即其雅可比行列式（我们将在下文定义）必须为正，这防止了物质体积被压缩至零或负值（即物质“翻转”）。[@problem_id:3579898]

### 局部变形的度量：变形梯度

运动映射 $\boldsymbol{\varphi}$ 描述了物体的全局运动，但为了分析物体内部的变形，我们需要一个能够描述局部变形的量。这个量就是**变形梯度 (deformation gradient)**，记作 $\boldsymbol{F}$。它被定义为运动映射 $\boldsymbol{\varphi}$ 对物质坐标 $\boldsymbol{X}$ 的梯度：
$$ \boldsymbol{F}(\boldsymbol{X}, t) = \frac{\partial \boldsymbol{\varphi}(\boldsymbol{X}, t)}{\partial \boldsymbol{X}} = \nabla_{\boldsymbol{X}} \boldsymbol{\varphi} $$
在分量形式下，其表达式为 $F_{iA} = \frac{\partial x_i}{\partial X_A}$，其中 $i$ 和 $A$ 分别代表空间坐标和物质坐标的分量索引。

变形梯度 $\boldsymbol{F}$ 的几何意义是它将一个位于物质点 $\boldsymbol{X}$ 的无限小物质线元 $d\boldsymbol{X}$ 线性映射到相应的空间线元 $d\boldsymbol{x}$：
$$ d\boldsymbol{x} = \boldsymbol{F} \, d\boldsymbol{X} $$
这意味着 $\boldsymbol{F}$ 包含了关于物质点 $\boldsymbol{X}$ 邻域内所有方向上的拉伸和旋转的全部信息。例如，考虑一个由运动 $\boldsymbol{\varphi}(\boldsymbol{X},t) = \begin{pmatrix} X_1 + \alpha t X_2 \\ e^{\beta t} X_2 \\ X_3 + \gamma t X_1 X_2 \end{pmatrix}$ 描述的变形。其变形梯度为 $\boldsymbol{F}(\boldsymbol{X},t) = \begin{pmatrix} 1  \alpha t  0 \\ 0  e^{\beta t}  0 \\ \gamma t X_2  \gamma t X_1  1 \end{pmatrix}$。在特定点和时刻，这个矩阵可以将任何给定的物质线元 $d\boldsymbol{X}$ 转换为其在当前构型中的对应线元 $d\boldsymbol{x}$。[@problem_id:3579860]

从变形梯度中可以导出一个至关重要的标量——**雅可比行列式 (Jacobian determinant)** $J$：
$$ J(\boldsymbol{X}, t) = \det \boldsymbol{F}(\boldsymbol{X}, t) $$
$J$ 代表了局部体积的变化率。一个在参考构型中体积为 $dV$ 的无限小物质微元，在当前构型中其体积将变为 $dv = J \, dV$。物理上要求 $J > 0$，以保证物质不会被压缩到零体积或发生局部反转。[@problem_id:3579860]

这个体积变换关系是进行积分变量替换的基础。当我们需要对当前构型 $\mathcal{B}_t$ 上的某个函数 $f(\boldsymbol{x})$ 进行积分时，可以通过变形梯度将其转换到对参考构型 $\mathcal{B}_0$ 的积分。这是通过**积分变量变换公式**实现的：
$$ \int_{\mathcal{B}_t} f(\boldsymbol{x}) \, d\boldsymbol{x} = \int_{\mathcal{B}_0} f(\boldsymbol{\varphi}(\boldsymbol{X},t)) \, J(\boldsymbol{X},t) \, d\boldsymbol{X} $$
这个公式在推导连续介质力学的积分形式守恒律时至关重要，例如，它确保了总质量或总能量在不同构型下的积分结果是等效的。[@problem_id:3579915]

### 有限应变度量

变形梯度 $\boldsymbol{F}$ 本身并非一个“纯粹”的应变度量，因为它包含了刚体转动的信息。为了只量化变形（即拉伸和剪切），我们需要构造一些不受刚体转动影响的张量。

我们从比较物质线元变形前后的长度平方入手。在参考构型中，线元 $d\boldsymbol{X}$ 的长度平方为 $dS^2 = d\boldsymbol{X} \cdot d\boldsymbol{X}$。在当前构型中，其对应线元 $d\boldsymbol{x}$ 的长度平方为：
$$ ds^2 = d\boldsymbol{x} \cdot d\boldsymbol{x} = (\boldsymbol{F} d\boldsymbol{X}) \cdot (\boldsymbol{F} d\boldsymbol{X}) = d\boldsymbol{X}^T \boldsymbol{F}^T \boldsymbol{F} d\boldsymbol{X} $$
这启发我们定义一个物质张量，即**右柯西-格林变形张量 (right Cauchy-Green deformation tensor)**：
$$ \boldsymbol{C}(\boldsymbol{X}, t) = \boldsymbol{F}^T \boldsymbol{F} $$
$\boldsymbol{C}$ 是一个对称的二阶张量，它完全定义在物质构型上。它度量了物质点邻域的变形，并且是**客观的 (objective)**，意味着它在叠加的刚体运动下保持不变。基于 $\boldsymbol{C}$，我们可以定义**格林-拉格朗日应变张量 (Green-Lagrange strain tensor)**：
$$ \boldsymbol{E}(\boldsymbol{X}, t) = \frac{1}{2} (\boldsymbol{C} - \boldsymbol{I}) $$
其中 $\boldsymbol{I}$ 是单位张量。当变形为无穷小时，$\boldsymbol{E}$ 趋近于经典的线性应变张量。

类似地，我们也可以从空间构型出发，比较 $dS^2$ 和 $ds^2$。利用 $d\boldsymbol{X} = \boldsymbol{F}^{-1} d\boldsymbol{x}$，我们有 $dS^2 = d\boldsymbol{x}^T \boldsymbol{F}^{-T} \boldsymbol{F}^{-1} d\boldsymbol{x}$。这引出了**左柯西-格林变形张量 (left Cauchy-Green deformation tensor)** 或 **芬格张量 (Finger tensor)**：
$$ \boldsymbol{b}(\boldsymbol{x}, t) = \boldsymbol{F} \boldsymbol{F}^T $$
$\boldsymbol{b}$ 是一个定义在空间构型上的对称二阶张量。相应地，**欧拉-阿尔曼西应变张量 (Euler-Almansi strain tensor)** 定义为：
$$ \boldsymbol{e}(\boldsymbol{x}, t) = \frac{1}{2} (\boldsymbol{I} - \boldsymbol{b}^{-1}) $$
$\boldsymbol{b}$ 和 $\boldsymbol{e}$ 都是空间度量，它们在叠加的刚体转动 $\boldsymbol{Q}$ 下会随之转动（例如，$\boldsymbol{b}^* = \boldsymbol{Q}\boldsymbol{b}\boldsymbol{Q}^T$）。[@problem_id:3579857]

### 物理场的描述：物质与空间视角

连续介质中的物理量，如温度、密度或应力，可以表示为场函数。根据其定义域的不同，我们有两种描述方式。

**物质描述 (Material description)** 或 **拉格朗日描述 (Lagrangian description)** 将物理量视为物质坐标 $\boldsymbol{X}$ 和时间 $t$ 的函数，记作 $\phi_0(\boldsymbol{X}, t)$。这种描述方式跟踪特定的物质点，并报告该点上的物理量随时间的变化。

**空间描述 (Spatial description)** 或 **欧拉描述 (Eulerian description)** 将物理量视为空间坐标 $\boldsymbol{x}$ 和时间 $t$ 的函数，记作 $\phi(\boldsymbol{x}, t)$。这种描述方式关注空间中的固定点，并报告流经该点的不同物质点所携带的物理量。

这两种描述的是同一个物理实在，因此它们之间必然存在联系。在任意时刻 $t$，位于空间点 $\boldsymbol{x} = \boldsymbol{\varphi}(\boldsymbol{X}, t)$ 的物质点就是标签为 $\boldsymbol{X}$ 的那个点。因此，它们的值必须相等：
$$ \phi_0(\boldsymbol{X}, t) = \phi(\boldsymbol{\varphi}(\boldsymbol{X}, t), t) $$
反之，亦有 $\phi(\boldsymbol{x}, t) = \phi_0(\boldsymbol{\chi}(\boldsymbol{x}, t), t)$，其中 $\boldsymbol{\chi}$ 是运动映射 $\boldsymbol{\varphi}$ 的逆映射。

这个关系也决定了它们梯度之间的变换法则。通过对上述关系应用链式法则，可以推导出物质梯度 $\nabla_{\boldsymbol{X}}$ 和空间梯度 $\nabla_{\boldsymbol{x}}$ 之间的关系。对于一个标量场，我们有：
$$ \nabla_{\boldsymbol{X}} \phi_0(\boldsymbol{X}, t) = \boldsymbol{F}^T (\boldsymbol{X}, t) \, \nabla_{\boldsymbol{x}} \phi(\boldsymbol{x}, t) $$
这个关系对于在不同坐标系下转换偏微分方程至关重要。[@problem_id:3579846]

### 坐标变换的普适工具：推前与拉回

上述不同物理量在物质构型和空间构型之间的转换，可以用一套更普适和几何化的语言来描述，即**推前 (push-forward)** 和**拉回 (pull-back)** 运算。这些运算由运动映射 $\boldsymbol{\varphi}$ 诱导。

- **标量场**：对于一个物质标量场 $f_0(\boldsymbol{X})$，其**推前**是定义在空间构型上的场 $f = f_0 \circ \boldsymbol{\varphi}^{-1}$。对于一个空间标量场 $g(\boldsymbol{x})$，其**拉回**是定义在物质构型上的场 $g^\flat = g \circ \boldsymbol{\varphi}$。这正是我们之前看到的 $\phi_0$ 和 $\phi$ 的关系。

- **矢量场** (切矢量)：一个物质矢量 $\boldsymbol{V}$（例如 $d\boldsymbol{X}$）的**推前**是通过变形梯度 $\boldsymbol{F}$ 实现的线性变换：$\boldsymbol{v} = \boldsymbol{\varphi}_*(\boldsymbol{V}) = \boldsymbol{F}\boldsymbol{V}$。反之，一个空间矢量 $\boldsymbol{w}$ 的**拉回**则是 $\boldsymbol{W} = \boldsymbol{\varphi}^*(\boldsymbol{w}) = \boldsymbol{F}^{-1}\boldsymbol{w}$。

- **二阶张量场**：张量的变换规则取决于其类型。
    - 对于**线性算子**类型（(1,1)型张量）的物质张量 $\boldsymbol{A}$，其推前是一个相似变换 $\boldsymbol{a} = \boldsymbol{F}\boldsymbol{A}\boldsymbol{F}^{-1}$。
    - 对于**双线性形式**类型（(0,2)型协变张量）的物质张量 $\boldsymbol{M}$（例如度量张量），其推前为 $\boldsymbol{m} = \boldsymbol{F}^{-T}\boldsymbol{M}\boldsymbol{F}^{-1}$。

这些变换规则是保持物理定律在不同坐标系下协变性的核心。例如，它们保证了功率共轭关系在物质和空间描述下的一致性。内功率密度在空间构型中表示为柯西应力 $\boldsymbol{\sigma}$ 和速度梯度 $\boldsymbol{l}$ 的双点积，即 $\boldsymbol{\sigma} : \boldsymbol{l}$。通过拉回运算，可以得到其在物质构型中的对应表达，即第一皮奥拉-基尔霍夫应力 $\boldsymbol{P}$ 和变形梯度率 $\dot{\boldsymbol{F}}$ 的双点积，即 $\boldsymbol{P} : \dot{\boldsymbol{F}}$。这两个表达式的等价性，通过积分变量变换，导出了 $\boldsymbol{\sigma}$ 和 $\boldsymbol{P}$ 之间的重要关系。[@problem_id:3579905]

### 动力学度量：应力张量及其转换

与应变度量类似，力学中的应力也有不同的描述方式，它们分别与不同的构型和面积元相关联。

- **柯西应力张量 (Cauchy stress tensor)** $\boldsymbol{\sigma}$：这是最符合物理直觉的应力，定义在**当前构型** $\mathcal{B}_t$ 上。它是一个对称的二阶空间张量，通过柯西公式 $\boldsymbol{t} = \boldsymbol{\sigma}\boldsymbol{n}$，将作用在当前构型中单位法向为 $\boldsymbol{n}$ 的面上的真实面力（单位当前面积上的力）$\boldsymbol{t}$ 联系起来。

- **第一皮奥拉-基尔霍夫应力张量 (First Piola-Kirchhoff stress tensor)** $\boldsymbol{P}$：也称为**名义应力 (nominal stress)**，定义在**参考构型** $\mathcal{B}_0$ 上。它将作用在参考构型中单位法向为 $\boldsymbol{N}$ 的面上的名义面力（单位参考面积上的力）$\boldsymbol{T}_R$ 联系起来，即 $\boldsymbol{T}_R = \boldsymbol{P}\boldsymbol{N}$。由于 $\boldsymbol{N}$ 是物质矢量而 $\boldsymbol{T}_R$ 是空间矢量，$\boldsymbol{P}$ 是一个**两点张量 (two-point tensor)**，且通常是**非对称**的。

- **第二皮奥拉-基尔霍夫应力张量 (Second Piola-Kirchhoff stress tensor)** $\boldsymbol{S}$：这是一个完全定义在**参考构型** $\mathcal{B}_0$ 上的**对称**二阶物质张量。它在能量上与格林-拉格朗日应变 $\boldsymbol{E}$ 共轭，是本构关系（材料如何响应变形的规律）中常用的应力度量。

这三种应力张量描述的是同一个物体内部的应力状态，因此它们之间可以通过变形梯度 $\boldsymbol{F}$ 相互转换。其转换关系可以通过考虑作用在同一个物质面上的力在不同构型下的表达等价性来推导。推导的关键是**南森公式 (Nanson's formula)**，它关联了参考构型和当前构型中的有向面积元 $d\boldsymbol{A} = \boldsymbol{N} dA$ 和 $d\boldsymbol{a} = \boldsymbol{n} da$：
$$ \boldsymbol{n} \, da = J \boldsymbol{F}^{-T} \boldsymbol{N} \, dA $$
值得注意的是，这里的变换矩阵是 $\boldsymbol{F}^{-T}$ 而非 $\boldsymbol{F}^{-1}$ 或其他形式，这源于叉乘的变换法则。使用错误的变换矩阵会导致对力平衡的错误计算。[@problem_id:3579903]

利用南森公式和力的等价性，可以推导出应力张量之间的转换关系：
$$ \boldsymbol{P} = J \boldsymbol{\sigma} \boldsymbol{F}^{-T} $$
$$ \boldsymbol{S} = \boldsymbol{F}^{-1} \boldsymbol{P} = J \boldsymbol{F}^{-1} \boldsymbol{\sigma} \boldsymbol{F}^{-T} $$
反过来，柯西应力也可以通过推前第二皮奥拉-基尔霍夫应力得到：
$$ \boldsymbol{\sigma} = \frac{1}{J} \boldsymbol{F} \boldsymbol{S} \boldsymbol{F}^T $$
这些关系是在不同力学框架（例如，拉格朗日有限元法和欧拉流体动力学）之间转换结果的基础。[@problem_id:3579871]

### 基本原理与约束条件

最后，我们讨论两个保证运动学框架自洽性的基本原理。

#### 材料客观性原理

**材料客观性原理 (Principle of material frame-indifference)**，或称**观察者无关性原理**，要求本构关系（即材料属性）独立于观察者的刚体运动。换言之，无论观察者如何平移或旋转，材料的响应行为都应相同。

这一原理对应变和应力度量施加了严格的约束。在一个已有的运动 $\boldsymbol{\varphi}$ 之上叠加一个刚体旋转 $\boldsymbol{Q}(t)$，新的变形梯度为 $\boldsymbol{F}^* = \boldsymbol{Q}\boldsymbol{F}$。
- **物质度量**如右柯西-格林张量 $\boldsymbol{C} = \boldsymbol{F}^T\boldsymbol{F}$ 和第二皮奥拉-基尔霍夫应力 $\boldsymbol{S}$ 必须是客观的。事实上，$\boldsymbol{C}^* = (\boldsymbol{Q}\boldsymbol{F})^T(\boldsymbol{Q}\boldsymbol{F}) = \boldsymbol{F}^T\boldsymbol{Q}^T\boldsymbol{Q}\boldsymbol{F} = \boldsymbol{F}^T\boldsymbol{F} = \boldsymbol{C}$，即 $\boldsymbol{C}$ 在叠加的刚体转动下不变，因此任何只依赖于 $\boldsymbol{C}$ 的本构关系（如 $\Psi(\boldsymbol{C})$）都是自动满足客观性的。
- **空间度量**如左柯西-格林张量 $\boldsymbol{b}$ 和柯西应力 $\boldsymbol{\sigma}$ 则必须以特定的方式随观察者一同旋转。例如，正确的柯西应力变换关系是 $\boldsymbol{\sigma}^* = \boldsymbol{Q}\boldsymbol{\sigma}\boldsymbol{Q}^T$。

在计算力学中，忽略这一原理会导致严重的错误。例如，一个简单的刚体旋转不应产生任何应变或应力变化，但一个非客观的数值算法可能会错误地预测出虚假的应力。一个常见的错误来源是对应力率使用了朴素的时间导数，而正确的客观应力率（如Jaumann率或Green-Naghdi率）必须包含与材料自旋相关的项，以消除刚体旋转的影响。[@problem_id:3579918]

#### 相容性条件

我们已经知道，变形梯度场 $\boldsymbol{F}(\boldsymbol{X})$ 是由一个运动场 $\boldsymbol{\chi}(\boldsymbol{X})$ 的梯度定义的。一个自然的问题是：任意给定的二阶张量场 $\boldsymbol{F}(\boldsymbol{X})$ 都能成为一个有效的变形梯度场吗？答案是否定的。

为了使一个张量场 $\boldsymbol{F}$ 能够对应于一个连续、单值的位移场，它必须满足**相容性条件 (compatibility condition)**。这个条件源于数学中混合偏导数次序无关的性质（施瓦茨定理）。既然 $F_{iA} = \partial \chi_i / \partial X_A$，那么对 $\boldsymbol{F}$ 的分量再次求导，我们必须有：
$$ \frac{\partial F_{iA}}{\partial X_B} = \frac{\partial^2 \chi_i}{\partial X_B \partial X_A} = \frac{\partial^2 \chi_i}{\partial X_A \partial X_B} = \frac{\partial F_{iB}}{\partial X_A} $$
这个条件可以更紧凑地用旋度算子来表示。将 $\boldsymbol{F}$ 的每一行视为一个物质矢量场，该条件等价于要求 $\boldsymbol{F}$ 的**行旋度 (row-wise curl)** 为零：
$$ \nabla_{\boldsymbol{X}} \times \boldsymbol{F} = \boldsymbol{0} $$
在单连通的物质域 $\mathcal{B}_0$ 上，根据庞加莱引理，这个条件不仅是**必要**的，也是**充分**的。这意味着，只要一个连续可微的张量场 $\boldsymbol{F}$ 满足行旋度为零的条件，就必然存在一个（在相差一个刚体位移的意义上）唯一的运动场 $\boldsymbol{\chi}$，使得 $\boldsymbol{F} = \nabla_{\boldsymbol{X}} \boldsymbol{\chi}$。这个条件保证了物质在变形过程中不会产生不合理的“缝隙”或“重叠”。[@problem_id:3579879]