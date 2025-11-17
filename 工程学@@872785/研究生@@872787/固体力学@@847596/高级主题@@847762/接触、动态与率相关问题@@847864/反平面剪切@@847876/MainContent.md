## 引言
在探索复杂的三维[固体力学](@entry_id:164042)世界时，能够将问题简化为更易于处理的低维模型，是理论分析和工程实践中的一项核心技能。反平面剪切（Antiplane Shear）正是这样一种强大而优雅的二维简化理论。它通过一个看似严格的运动学假设——即所有物质点的位移都发生在垂直于观察平面的单一方向上——极大地简化了弹性力学的控制方程，将原本复杂的张量问题转化为一个标量问题。这种简化不仅没有牺牲物理本质，反而精确地捕捉了诸如长柱体扭转、[III型断裂](@entry_id:202725)等一系列重要工程现象的核心力学行为。本文旨在为读者构建一个关于反平面剪切理论的完整知识体系。

本文将分为三个核心部分。首先，在“原理与机制”章节中，我们将从第一性原理出发，系统推导反平面剪切的运动学、[本构关系](@entry_id:186508)和[平衡方程](@entry_id:172166)，最终得到其标志性的控制方程——拉普拉斯方程，并阐明相应的边界条件与能量原理。接着，在“应用与交叉学科联系”章节中，我们将展示该理论在[圣维南扭转](@entry_id:194475)、断裂力学、[材料科学](@entry_id:152226)及地球物理等领域的广泛应用，揭示其如何成为连接不同学科的桥梁。最后，“动手实践”部分将通过一系列精心设计的计算练习，帮助读者将理论知识转化为解决实际问题的能力。通过这一结构化的学习路径，读者将全面掌握反平面剪切的精髓及其在科学研究与工程设计中的强大威力。

## 原理与机制

在[连续介质力学](@entry_id:155125)中，为了分析复杂的三维问题，我们常常引入简化假设，将问题[降维](@entry_id:142982)到二维或一维。反平面剪切（antiplane shear）是弹性力学中一种经典且极为重要的二维简化模型。它描述了一种特殊的变形状态，即物体内所有点的位移都平行于某一固定方向（平面外方向），且位移大小仅取决于垂直于该方向的平面坐标。尽管这一运动学假设看似苛刻，但它精确地捕捉了多种工程问题的物理本质，例如长柱体的纵向剪切、[III型断裂](@entry_id:202725)以及[圣维南扭转](@entry_id:194475)问题的一部分。本章旨在从第一性原理出发，系统阐述反平面剪切的运动学、[本构关系](@entry_id:186508)、[平衡方程](@entry_id:172166)、边界条件及其能量原理，为后续应用奠定坚实的理论基础。

### 反平面剪切的运动学定义

我们考虑一个占据三维欧几里得空间区域的弹性体，并建立笛卡尔坐标系 $(x, y, z)$。反平面剪切状态的核心在于一个明确的 **运动学假设**（kinematic assumption）。我们假定物体的[位移场](@entry_id:141476) $\boldsymbol{u}=(u_x, u_y, u_z)$ 具有如下特定形式：
$$
u_x = 0, \quad u_y = 0, \quad u_z = w(x,y)
$$
这个表达式的物理意义是：物体内任意点的位移都严格沿着 $z$ 轴方向（平面外方向），而 $x$ 和 $y$ 方向（平面内方向）没有任何位移分量。此外，位移的大小 $w$ 仅是平面[内坐标](@entry_id:169764) $(x,y)$ 的函数，而与平面外坐标 $z$ 无关。这意味着沿着平行于 $z$ 轴的任意一条直线上，所有点的位移都是相同的。这种变形模式可以想象为一副扑克牌，每张牌相对于其下方的一张牌发生平移，但每张牌自身不发生弯曲或伸缩。

基于[小变形理论](@entry_id:174991)，我们可以从该位移场出发，推导[应变张量](@entry_id:193332) $\boldsymbol{\varepsilon}$ 的各个分量。根据[应变-位移关系](@entry_id:173321) $\varepsilon_{ij} = \frac{1}{2}(u_{i,j} + u_{j,i})$（其中 $u_{i,j}$ 表示 $\partial u_i / \partial x_j$），我们逐一计算：

- **[正应变](@entry_id:204633)**（Normal Strains）：
  $$
  \varepsilon_{xx} = \frac{\partial u_x}{\partial x} = 0
  $$
  $$
  \varepsilon_{yy} = \frac{\partial u_y}{\partial y} = 0
  $$
  $$
  \varepsilon_{zz} = \frac{\partial u_z}{\partial z} = \frac{\partial w(x,y)}{\partial z} = 0
  $$
  所有[正应变](@entry_id:204633)分量均为零，表明在线性近似下，物体在任何方向上都没有伸长或缩短。

- **[剪应变](@entry_id:175241)**（Shear Strains）：
  $$
  \varepsilon_{xy} = \frac{1}{2}\left(\frac{\partial u_x}{\partial y} + \frac{\partial u_y}{\partial x}\right) = 0
  $$
  $$
  \varepsilon_{xz} = \frac{1}{2}\left(\frac{\partial u_x}{\partial z} + \frac{\partial u_z}{\partial x}\right) = \frac{1}{2}\left(0 + \frac{\partial w}{\partial x}\right) = \frac{1}{2}\frac{\partial w}{\partial x}
  $$
  $$
  \varepsilon_{yz} = \frac{1}{2}\left(\frac{\partial u_y}{\partial z} + \frac{\partial u_z}{\partial y}\right) = \frac{1}{2}\left(0 + \frac{\partial w}{\partial y}\right) = \frac{1}{2}\frac{\partial w}{\partial y}
  $$
  可见，在反平面剪切状态下，只有平面外[剪应变](@entry_id:175241)分量 $\varepsilon_{xz}$ 和 $\varepsilon_{yz}$ 可能非零 [@problem_id:2615407]。这两种[剪应变](@entry_id:175241)描述了垂直于 $z$ 轴的平面（即 $xy$ 平面）相对于彼此的错动。值得注意的是，工程[剪应变](@entry_id:175241) $\gamma_{ij}$ 与张量[剪应变](@entry_id:175241) $\varepsilon_{ij}$ 的关系为 $\gamma_{ij} = 2\varepsilon_{ij}$（当 $i \neq j$ 时）。因此，非零的工程[剪应变](@entry_id:175241)为 $\gamma_{xz} = \partial w/\partial x$ 和 $\gamma_{yz} = \partial w/\partial y$。

一个重要的问题是，这样的应变场是否满足 **[运动学](@entry_id:173318)协调性**（kinematic compatibility）？协调性条件确保应变场可以积分得到一个单值的、连续的位移场。然而，在我们的推导中，我们是从一个已经给定的、单值的[位移场](@entry_id:141476) $w(x,y)$ 出发来计算应变的。因此，只要函数 $w(x,y)$ 具有足够的连续性和[可微性](@entry_id:140863)（例如，至少是连续可微的），其派生出的应变场必然是协调的。换言之，反平面剪切的[运动学](@entry_id:173318)假设本身就保证了协调性的满足，无需施加额外的约束条件 [@problem_id:2615438]。

### 应力、平衡与控制方程

确定了物体的变形模式（[运动学](@entry_id:173318)）后，下一步是分析其内部的力学状态（动力学）。这需要引入材料的 **本构关系**（constitutive relation）和 **平衡方程**（equilibrium equations）。

对于一个线性、各向同性的弹性材料，其[应力-应变关系](@entry_id:274093)遵循[胡克定律](@entry_id:149682)。在反平面剪切中，由于所有[正应变](@entry_id:204633)和面内[剪应变](@entry_id:175241)均为零，[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ 的形式也大大简化。应力分量与应变分量之间的关系为：
$$
\sigma_{ij} = \lambda \varepsilon_{kk} \delta_{ij} + 2\mu \varepsilon_{ij}
$$
其中 $\lambda$ 和 $\mu$ 是拉梅参数（Lamé parameters），$\mu$ 也被称为 **[剪切模量](@entry_id:167228)**（shear modulus），$\delta_{ij}$ 是克罗内克符号。由于体积应变 $\varepsilon_{kk} = \varepsilon_{xx} + \varepsilon_{yy} + \varepsilon_{zz} = 0$，上式简化为 $\sigma_{ij} = 2\mu \varepsilon_{ij}$。代入我们求得的应变分量，得到非零的应力分量为：
$$
\sigma_{xz} = 2\mu \varepsilon_{xz} = \mu \frac{\partial w}{\partial x}
$$
$$
\sigma_{yz} = 2\mu \varepsilon_{yz} = \mu \frac{\partial w}{\partial y}
$$
所有其他应力分量（$\sigma_{xx}, \sigma_{yy}, \sigma_{zz}, \sigma_{xy}$）均为零。这表明，反平面剪切状态下，物体内部只存在平面外剪应力。[剪切模量](@entry_id:167228) $\mu$ 在此扮演了关键角色：它是一个正的材料常数，量化了材料抵抗剪切变形的能力，是连接[位移梯度](@entry_id:165352)（几何量）与剪应力（力学量）的桥梁 [@problem_id:2615448]。

在静态（或准静态）情况下，且存在[体力](@entry_id:174230) $b_z(x,y)$ 时，应[力场](@entry_id:147325)必须满足[平衡方程](@entry_id:172166) $\nabla \cdot \boldsymbol{\sigma} + \boldsymbol{b} = \mathbf{0}$。由于所有场量都与 $z$ 无关，且只有 $\sigma_{xz}$ 和 $\sigma_{yz}$ 非零，平衡方程的三个分量简化为：
- $x$ 方向: $\frac{\partial \sigma_{xx}}{\partial x} + \frac{\partial \sigma_{xy}}{\partial y} + \frac{\partial \sigma_{xz}}{\partial z} + b_x = 0 \implies 0 + 0 + 0 + 0 = 0$
- $y$ 方向: $\frac{\partial \sigma_{yx}}{\partial x} + \frac{\partial \sigma_{yy}}{\partial y} + \frac{\partial \sigma_{yz}}{\partial z} + b_y = 0 \implies 0 + 0 + 0 + 0 = 0$
- $z$ 方向: $\frac{\partial \sigma_{zx}}{\partial x} + \frac{\partial \sigma_{zy}}{\partial y} + \frac{\partial \sigma_{zz}}{\partial z} + b_z = 0 \implies \frac{\partial \sigma_{xz}}{\partial x} + \frac{\partial \sigma_{yz}}{\partial y} + b_z = 0$

$x$ 和 $y$ 方向的平衡被自动满足。唯一有意义的方程是 $z$ 方向的[平衡方程](@entry_id:172166)。将应力表达式代入，我们得到关于位移函数 $w(x,y)$ 的 **控制[偏微分方程](@entry_id:141332)**：
$$
\frac{\partial}{\partial x}\left(\mu \frac{\partial w}{\partial x}\right) + \frac{\partial}{\partial y}\left(\mu \frac{\partial w}{\partial y}\right) + b_z = 0
$$
这可以写成更紧凑的形式 $\nabla \cdot (\mu \nabla w) + b_z = 0$，其中 $\nabla$ 是二维[梯度算子](@entry_id:275922)。

这个方程的形式取决于材料的性质。
- 对于 **均匀材料**（homogeneous material），剪切模量 $\mu$ 是一个常数。若同时没有[体力](@entry_id:174230)（$b_z=0$），控制方程就简化为一个非常著名的方程—— **[拉普拉斯方程](@entry_id:143689)**（Laplace equation）:
  $$
  \nabla^2 w = \frac{\partial^2 w}{\partial x^2} + \frac{\partial^2 w}{\partial y^2} = 0
  $$
  需要强调的是，[拉普拉斯方程](@entry_id:143689)是[运动学](@entry_id:173318)、[本构关系](@entry_id:186508)和平衡三大要素共同作用的结果，而不仅仅是[运动学](@entry_id:173318)协调性的要求 [@problem_id:2615438]。

- 对于 **非均匀材料**（heterogeneous material），剪切模量 $\mu = \mu(x,y)$ 是空间位置的函数。此时，$\mu$ 不能从[微分算子](@entry_id:140145)中提出，必须保留 $\nabla \cdot (\mu \nabla w) + b_z = 0$ 的完整形式。在这种情况下，即使没有[体力](@entry_id:174230)，[位移场](@entry_id:141476) $w$ 通常也不满足[拉普拉斯方程](@entry_id:143689) [@problem_id:2615448]。

### 边界条件与问题提法

为了从控制方程中求解唯一的[位移场](@entry_id:141476) $w(x,y)$，我们必须在求解域 $\Omega$ 的边界 $\partial\Omega$ 上指定 **边界条件**（boundary conditions）。在反平面剪切问题中，边界条件主要有两种类型。

#### [位移边界条件](@entry_id:203261)（Dirichlet 条件）

[第一类边界条件](@entry_id:142800)是直接规定边界上位移的大小，称为 **[位移边界条件](@entry_id:203261)** 或 **[本质边界条件](@entry_id:173524)**（essential boundary condition）。在反平面剪切中，这表现为在边界的一部分 $\Gamma_w$ 上给定 $w$ 的值：
$$
w(x,y) = \bar{w}(x,y) \quad \text{在 } \Gamma_w \text{ 上}
$$
其中 $\bar{w}$ 是一个已知的函数。

这种条件的物理意义是边界的运动学受到了强制约束 [@problem_id:2615447]。例如，这可以模拟边界与一个刚性驱动器牢固地粘接在一起，该驱动器按照预设的剖面 $\bar{w}$ 运动。当边界位移被指定后，维持该位移所需的力，即边界上的 **剪切反力** $t_z$，就成为一个未知的待求量。它不能被同时指定，而是在解出整个位移场 $w$ 之后，通过应[力场](@entry_id:147325)计算得到。在[变分原理](@entry_id:198028)（如[虚功原理](@entry_id:138749)）中，指定位移的边界要求相应的[虚位移](@entry_id:168781) $\delta w$ 在该边界上为零（$\delta w = 0$ on $\Gamma_w$），这使得反力所做的[虚功](@entry_id:176403)自动消失 [@problem_id:2615447]。

#### 应力边界条件（Neumann 条件）

第二类边界条件是规定边界上的力，称为 **应力边界条件** 或 **自然边界条件**（natural boundary condition）。对于反平面剪切问题，这对应于在边界的一部分 $\Gamma_t$ 上规定平面外剪切曳引（traction）$t_z$ 的大小：
$$
t_z = \bar{t}_z(x,y) \quad \text{在 } \Gamma_t \text{ 上}
$$
为了理解 $t_z$ 的表达式，我们使用 **柯西应力定理**（Cauchy's traction theorem），$\boldsymbol{T} = \boldsymbol{\sigma}\boldsymbol{n}$。在一个侧表面上，单位外[法向量](@entry_id:264185)为 $\boldsymbol{n} = (n_x, n_y, 0)$。曳引向量 $\boldsymbol{T}$ 为：
$$
\boldsymbol{T} = \begin{pmatrix} 0  & 0 & \sigma_{xz} \\ 0 & 0 & \sigma_{yz} \\ \sigma_{xz} & \sigma_{yz} & 0 \end{pmatrix} \begin{pmatrix} n_x \\ n_y \\ 0 \end{pmatrix} = \begin{pmatrix} 0 \\ 0 \\ \sigma_{xz}n_x + \sigma_{yz}n_y \end{pmatrix}
$$
曳引向量只有一个 $z$ 分量，这正是我们所说的平面外剪切曳引 $t_z$。因此，边界条件可以写作：
$$
t_z = \sigma_{xz}n_x + \sigma_{yz}n_y = \bar{t}_z \quad \text{在 } \Gamma_t \text{ 上}
$$
物理上，$\bar{t}_z$ 代表了施加在单位边界面积上的、沿着 $z$ 方向的剪切力 [@problem_id:2615423]。将[本构关系](@entry_id:186508)代入，我们得到以位移 $w$ 表示的 Neumann 边界条件：
$$
\mu\left(\frac{\partial w}{\partial x}n_x + \frac{\partial w}{\partial y}n_y\right) = \mu \frac{\partial w}{\partial n} = \bar{t}_z \quad \text{在 } \Gamma_t \text{ 上}
$$
其中 $\partial w/\partial n$ 是 $w$ 沿边界外[法线](@entry_id:167651)方向的方向导数。

#### [界面条件](@entry_id:750725)

当材料由不同性质的子区域组成时（例如[复合材料](@entry_id:139856)），在这些子区域之间的内部界面 $\Gamma$ 上，场量必须满足特定的 **[界面条件](@entry_id:750725)**（interface conditions）或 **传递条件**（transmission conditions）。假设界面两侧的[剪切模量](@entry_id:167228)分别为 $\mu_1$ 和 $\mu_2$，且界面是完美粘合的，则：
1.  **位移连续性**：由于完美粘合，界面两侧的材料点不能分离或相对滑移。这要求[位移场](@entry_id:141476) $w$ 跨界面是连续的。使用跳跃算子 $[f] = f_2 - f_1$ 表示跨界面的值的变化，我们有：
    $$
    [w] = 0
    $$
2.  **曳引连续性**：根据[牛顿第三定律](@entry_id:166652)，界面两侧相互作用的力（曳引）必须大小相等、方向相反。在没有界面奇异源的情况下，这要求曳引向量连续，即 $[t_z] = 0$。这转化为：
    $$
    [\mu \frac{\partial w}{\partial n}] = 0 \quad \text{或} \quad \mu_2 \left.\frac{\partial w}{\partial n}\right|_2 = \mu_1 \left.\frac{\partial w}{\partial n}\right|_1
    $$
这两条是反平面剪切问题在两种不同[材料界面](@entry_id:751731)上的基本条件 [@problem_id:2615425]。值得注意的是，如果 $\mu_1 \neq \mu_2$，那么位移的[法向导数](@entry_id:169511) $\partial w/\partial n$ 在界面上必然是不连续的。

### 能量方法与[变分原理](@entry_id:198028)

除了通过[求解偏微分方程](@entry_id:138485)（强形式）来解决问题，我们还可以采用基于能量的 **变分方法**（variational methods），即所谓的[弱形式](@entry_id:142897)。这种方法在理论分析和数值计算（如有限元法）中都至关重要。其核心是构造一个代表系统总势能的 **泛函**（functional），并找到使该泛函取极小值的位移场。

对于反平面剪切问题，系统的 **总势能** $\Pi[w]$ 由两部分组成：内部的 **应变能** $U$ 和外部载荷的势能 $V$。
$$
\Pi[w] = U - W_{\text{ext}}
$$
其中 $W_{\text{ext}}$ 是外力所做的功。

- **[应变能](@entry_id:162699)**：[应变能密度](@entry_id:200085)（单位体积的[应变能](@entry_id:162699)）$W$ 为 $W = \frac{1}{2}\sigma_{ij}\varepsilon_{ij}$。代入反平面剪切的[应力应变](@entry_id:204183)，我们得到：
  $$
  W = \frac{1}{2}(\sigma_{xz}\gamma_{xz} + \sigma_{yz}\gamma_{yz}) = \frac{1}{2}\mu\left[\left(\frac{\partial w}{\partial x}\right)^2 + \left(\frac{\partial w}{\partial y}\right)^2\right] = \frac{1}{2}\mu |\nabla w|^2
  $$
  总的内部应变能 $U$ 是将[应变能密度](@entry_id:200085)在整个求解域 $\Omega$ 上积分：
  $$
  U[w] = \int_{\Omega} \frac{1}{2}\mu |\nabla w|^2 \, dA
  $$
  可见，应变能与剪切模量成正比，与[位移梯度](@entry_id:165352)的平方成正比 [@problem_id:2615448]。

- **外力功**：外力功由体力 $b_z$ 和边界曳引 $\bar{t}_z$ 产生：
  $$
  W_{\text{ext}}[w] = \int_{\Omega} b_z w \, dA + \int_{\Gamma_t} \bar{t}_z w \, ds
  $$

将以上各项组合，我们得到总势能泛函 [@problem_id:2615437]：
$$
\Pi[w] = \int_{\Omega} \frac{1}{2}\mu |\nabla w|^2 \, dA - \int_{\Omega} b_z w \, dA - \int_{\Gamma_t} \bar{t}_z w \, ds
$$
根据[最小势能原理](@entry_id:173340)，真实的[位移场](@entry_id:141476) $w$ 是在所有满足[位移边界条件](@entry_id:203261)的 **容许位移场**（admissible displacement field）中，使 $\Pi[w]$ 达到最小值的那个场。

从数学角度看，为了保证泛函中的各项积分有意义，位移函数 $w$ 及其[一阶导数](@entry_id:749425)必须是平方可积的。满足这一条件的函数构成了 **索伯列夫空间** $H^1(\Omega)$。因此，求解问题就转化为在 $H^1(\Omega)$ 的一个满足本质边界条件的[子集](@entry_id:261956)（一个[仿射空间](@entry_id:152906)）上寻找泛函 $\Pi[w]$ 的最小值点。这一框架为问题的[适定性](@entry_id:148590)分析和有限元方法的构建提供了严格的数学基础 [@problem_id:2615437]。

### 模型适用性与相关问题

#### 与其他二维模型的比较

反平面剪切是弹性力学中三种主要的二维简化模型之一。将其与 **[平面应变](@entry_id:167046)** 和 **平面应力** 进行比较，有助于我们理解各自的[适用范围](@entry_id:636189) [@problem_id:2615403]。

- **反平面剪切** (Antiplane Shear):
  - **[运动学](@entry_id:173318)假设**: $u_x = 0, u_y = 0, u_z = w(x,y)$。
  - **应变状态**: $\varepsilon_{xx}=\varepsilon_{yy}=\varepsilon_{zz}=\varepsilon_{xy}=0$。只有 $\varepsilon_{xz}, \varepsilon_{yz}$ 非零。
  - **应力状态**: $\sigma_{xx}=\sigma_{yy}=\sigma_{zz}=\sigma_{xy}=0$。只有 $\sigma_{xz}, \sigma_{yz}$ 非零。
  - **适用场景**: 长柱体受到平行于轴线的剪切载荷。

- **[平面应变](@entry_id:167046)** (Plane Strain):
  - **[运动学](@entry_id:173318)假设**: $u_z = 0$，且 $u_x = u_x(x,y), u_y = u_y(x,y)$。
  - **应变状态**: $\varepsilon_{zz}=\varepsilon_{xz}=\varepsilon_{yz}=0$。平面内应变 $\varepsilon_{xx}, \varepsilon_{yy}, \varepsilon_{xy}$ 非零。
  - **应力状态**: 由于[泊松效应](@entry_id:158876)，为维持 $\varepsilon_{zz}=0$ 需要产生非零的 $\sigma_{zz} = \lambda(\varepsilon_{xx}+\varepsilon_{yy})$。$\sigma_{xz}, \sigma_{yz}$ 为零。
  - **适用场景**: 几何和载荷在 $z$ 方向不变的长条形物体（如大坝、隧道、挡土墙）。

- **[平面应力](@entry_id:172193)** (Plane Stress):
  - **应力假设**: $\sigma_{zz}=\sigma_{xz}=\sigma_{yz}=0$。
  - **应变状态**: 由于[泊松效应](@entry_id:158876)，非零的[平面应力](@entry_id:172193)会导致平面外应变 $\varepsilon_{zz} = -\frac{\lambda}{\lambda+2\mu}(\varepsilon_{xx}+\varepsilon_{yy}) \neq 0$。$\varepsilon_{xz}, \varepsilon_{yz}$ 为零。
  - **适用场景**: 厚度方向尺寸远小于平面尺寸的薄板，且载荷作用在板的平面内。

#### 模型的有效性与[圣维南原理](@entry_id:165302)

反平面剪切解在何种条件下是精确的？对于一个无限长的、[横截面](@entry_id:154995)均匀的柱体，如果其材料是各向同性或[横向各向同性](@entry_id:756140)的（[对称轴](@entry_id:177299)沿 $z$ 轴），且所受的体力和侧面力也仅有 $z$ 分量且沿 $z$ 轴不变，那么反平面剪切场就是一个精确的弹性力学解。

对于有限长度的柱体，端部的边界条件通常会破坏沿 $z$ 轴的不变性。例如，端部可能是自由的，这意味着所有应力分量（包括 $\sigma_{xz}, \sigma_{yz}$）都应为零。而一个典型的反平面剪切解在内部通常具有非零的 $\sigma_{xz}, \sigma_{yz}$。根据 **[圣维南原理](@entry_id:165302)**（Saint-Venant's principle），这种端部边界条件与内部解之间的不匹配所产生的影响是局部的。其效应会随着远离端部而迅速衰减。因此，对于一个足够长的柱体，在远离两端的“内部”区域，反平面剪切解仍然是一个非常好的近似 [@problem_id:2615451]。

#### 与[圣维南扭转](@entry_id:194475)的类比

反平面剪切的数学结构与另一个经典的弹性力学问题——**[圣维南扭转](@entry_id:194475)**（Saint-Venant's torsion）——有着深刻的类比关系 [@problem_id:2615416]。考虑一个[横截面](@entry_id:154995)为 $\Omega$ 的柱体绕 $z$ 轴扭转。其位移场可以分解为一个绕轴的刚性转动和一个与[截面](@entry_id:154995)形状相关的轴向 **翘曲**（warping）位移 $u_z = \alpha \psi(x,y)$，其中 $\alpha$ 是单位长度扭转角，$\psi(x,y)$ 是[翘曲函数](@entry_id:187475)。

可以证明，对于均匀各向同性材料，在没有体力的情况下，[翘曲函数](@entry_id:187475) $\psi$ 同样满足 **[拉普拉斯方程](@entry_id:143689)**：
$$
\nabla^2 \psi = 0 \quad \text{在 } \Omega \text{ 中}
$$
此外，若柱体侧面是自由的（无曳引），则[翘曲函数](@entry_id:187475)必须满足一个Neumann型边界条件：
$$
\frac{\partial \psi}{\partial n} = y n_x - x n_y \quad \text{在 } \partial\Omega \text{ 上}
$$
对比反平面剪切问题，我们发现：[圣维南扭转](@entry_id:194475)的翘曲问题在数学上完全等价于一个特定的反平面剪切问题。在这个问题中，位移函数 $w$ 满足拉普拉斯方程，且在边界上施加了特定的剪切曳引 $\bar{t}_z = G(y n_x - x n_y)$。这种数学上的类比关系不仅揭示了弹性理论内在的统一性，也使得我们可以借用一个问题的解来理解另一个问题。

总之，反平面剪切模型虽然简单，但其背后蕴含了丰富的物理原理和深刻的数学结构，是通向更高级[弹性理论](@entry_id:184142)和应用的重要阶梯。