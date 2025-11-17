## 引言
连续介质力学为描述和预测固体与流体等可变形物质的力学行为提供了严谨的数学框架。该框架的基石是“连续体”这一核心概念，以及用于追踪其随[时间演化](@entry_id:153943)的“位形”与“运动”的运动学描述。理解这些基本概念是掌握从材料本构理论到高级计算仿真的所有后续内容的前提。

然而，从适用于小变形的线性理论过渡到能够精确捕捉真实世界中普遍存在的大变形、大转动现象的[非线性](@entry_id:637147)理论，常常构成一个重大的概念挑战。许多学习者难以清晰地将在不同[坐标系](@entry_id:156346)下定义的多种应力、[应变度量](@entry_id:755495)（如柯西应力、PK应力、格林应变）与变形梯度这一中心运动学量联系起来。本文旨在系统性地梳理这一知识体系，填补理论与应用之间的鸿沟。

读者将通过本文学习到：第一章“原理和机制”将奠定理论基础，深入剖析从连续介质假设到变形梯度、[应力张量](@entry_id:148973)和[客观性原理](@entry_id:185412)的核心概念。第二章“应用与跨学科关联”将展示这些理论如何在[有限元分析](@entry_id:138109)、[多尺度建模](@entry_id:154964)和[生物医学工程](@entry_id:268134)等前沿领域中发挥关键作用。最后，第三章“动手实践”将通过具体的计算问题，帮助读者将抽象的理论转化为可操作的技能。

## 原理和机制

### 连续介质假设

在宏观尺度上，固体和流体等物质通常表现为连续的、可变形的实体，而不是离散的原子或分[子集](@entry_id:261956)合。尽管我们知道所有物质在根本上都是由原子构成的，但在大多数工程和物理应用中，我们关心的长度尺度远大于原子间距。这使得我们可以采用一种被称为**连续介质假设** (continuum hypothesis) 的强大抽象。该假设将物体理想化为一个**连续介质体** (continuum body)，即一个由无穷多个**物[质点](@entry_id:186768)** (material points) 组成的集合，这些点连续地填充着物体所占据的空间区域。

每个物质点本身并不是一个原子或分子，而是一个抽象的数学点。然而，它被认为代表了一个足够大的微小体积，这个体积包含着数量巨大的原子，使得我们可以有意义地定义其平均物理属性，如密度、温度和速度。这个微小的体积被称为**[代表性体积元](@entry_id:164290)** (Representative Volume Element, RVE)。RVE的尺度 $\ell$ 必须满足一个关键的**尺度分离** (separation of scales) 原则。一方面，$\ell$ 必须远大于底层的微观结构尺度，例如晶格间距 $a$ 或微观结构相关长度 $\xi$ (即 $a, \xi \ll \ell$)。这保证了在RVE尺度上进行的物理量平均具有统计意义，能够有效地消除原子尺度的涨落。另一方面，$\ell$ 必须远小于我们感兴趣的宏观现象的[特征长度](@entry_id:265857)，例如物体的整体尺寸 $L$ 或在动态问题中波的波长 $\lambda$ (即 $\ell \ll L, \lambda$)。这保证了RVE可以被视为一个数学上的“点”，从而能够定义连续的物理场并对其进行[微分](@entry_id:158718)运算。

综合起来，对于一个动态问题，连续介质模型在尺度 $\ell$ 上有效的充分条件是存在清晰的尺度分离：
$$ a, \xi \ll \ell \ll \min\{L, \lambda\} $$
同时，在尺度 $\ell$ 上，[空间平均](@entry_id:203499)的材料属性必须具有统计[代表性](@entry_id:204613)，即其在整个物体内的相对波动低于某个预设的容差 $\varepsilon$ [@problem_id:3554291]。例如，考虑一个晶体，其[晶格间距](@entry_id:180328) $a = 5 \times 10^{-10} \text{ m}$，宏观[特征长度](@entry_id:265857) $L = 10^{-2} \text{ m}$。若其受到频率为 $5 \times 10^6 \text{ Hz}$ 的波激励，[波速](@entry_id:186208)为 $5000 \text{ m/s}$，则波长 $\lambda = 10^{-3} \text{ m}$。如果在一个 $\ell = 10^{-6} \text{ m}$ 的尺度上测得的密度波动小于 $1\%$ 的容差，并且该尺度满足 $5 \times 10^{-10} \text{ m} \ll 10^{-6} \text{ m} \ll 10^{-3} \text{ m}$，那么在这个尺度上使用连续介质模型来描述该动态问题是完全合理的 [@problem_id:3554291]。

从数学上讲，连续介质体 $\mathcal{B}$ 可以被建模为一个[可微流形](@entry_id:183068)，其上的每个物[质点](@entry_id:186768) $\mathbf{X}$ 都拥有邻域。这使得我们可以在 $\mathcal{B}$ 上定义连续的运动学场，如速度 $\mathbf{v}(\mathbf{X},t)$，并以场方程的形式表达质量、动量和能量等物理[守恒定律](@entry_id:269268) [@problem_id:3554291]。

### 位形与运动：描述变形

为了描述连续体的变形，我们需要追踪其所有物[质点](@entry_id:186768)随时间的位置变化。这是通过引入**位形** (configuration) 和**运动** (motion) 的概念来实现的。

一个**位形**是连续体 $\mathcal{B}$ 在某一时刻在三维[欧几里得空间](@entry_id:138052) $\mathbb{R}^3$ 中的一个具体“快照”或[几何实现](@entry_id:265700)。我们通常选择一个特定的、方便的位形作为参考，称为**[参考位](@entry_id:754187)形** (reference configuration) $\mathcal{B}_0$。物体中一个物[质点](@entry_id:186768)在此位形中的位置向量 $\mathbf{X}$ 被称为**物质坐标** (material coordinate) 或**参考坐标** (referential coordinate)。$\mathbf{X}$ 的关键作用是作为该物[质点](@entry_id:186768)的永久“标签”，在整个运动过程中唯一地标识它。

物体在任意时刻 $t$ 所占据的空间区域被称为**当前位形** (current configuration) $\mathcal{B}_t$。同一个物[质点](@entry_id:186768)在当前位形中的位置向量 $\mathbf{x}$ 被称为**空间坐标** (spatial coordinate) 或**当前坐标** (current coordinate)。

**运动**是一个光滑的、依赖于时间的映射 $\boldsymbol{\chi}$，它将每个物质点从其在[参考位](@entry_id:754187)形中的位置 $\mathbf{X}$ 映射到其在 $t$ 时刻在当前位形中的位置 $\mathbf{x}$：
$$ \mathbf{x} = \boldsymbol{\chi}(\mathbf{X}, t) $$
因此，$\boldsymbol{\chi}$ 描述了从[参考位](@entry_id:754187)形 $\mathcal{B}_0$ 到当前位形 $\mathcal{B}_t$ 的完整变形历史 [@problem_id:3554361]。

为了使运动在物理上是可接受的，映射 $\boldsymbol{\chi}(\cdot, t)$ 在每个时刻 $t$ 都必须是一个**嵌入** (embedding)。这意味着它必须满足两个核心条件：

1.  **[单射性](@entry_id:147722) (Injectivity)**：映射必须是**一对一**的。这意味着两个不同的物[质点](@entry_id:186768) $\mathbf{X}_1 \neq \mathbf{X}_2$ 在任何时刻都不能占据同一个空间位置，即 $\boldsymbol{\chi}(\mathbf{X}_1, t) \neq \boldsymbol{\chi}(\mathbf{X}_2, t)$。这是物质**不可入性** (impenetrability) 公理的数学表达。如果[单射性](@entry_id:147722)失效，就意味着物质发生了自相交或相互穿透，这在经典连续介质力学中通常是不允许的 [@problem_id:3554361]。

2.  **保[向性](@entry_id:144651) (Orientation-Preservation)**：映射必须保持物质微元的[局部定向](@entry_id:264384)。一个[右手坐标系](@entry_id:166669)定义的微元在变形后仍应为[右手坐标系](@entry_id:166669)。这防止了物质被“由内向外”翻转。我们将在下一节看到，这个条件与变形梯度的雅可比行列式直接相关。

值得注意的是，一个映射的[局部可逆性](@entry_id:143266)并不保证其全局[单射性](@entry_id:147722)。即使一个变形在每一点都是局部一对一的，它仍然可能在全局上发生自相交（例如，将一张平坦的薄片卷成圆筒并使其部分重叠）。因此，全局[单射性](@entry_id:147722)是一个独立的、更强的条件，它对于防止物质穿透至关重要 [@problem_id:3554361] [@problem_id:3554293]。

### 变形梯度：变形的局部度量

运动映射 $\boldsymbol{\chi}$ 描述了全局的变形，但为了进行力学分析，我们需要一个能够量化**局部**变形的量。这个量就是**变形梯度** (deformation gradient)。

变形梯度张量 $\mathbf{F}$ 定义为运动 $\boldsymbol{\chi}$ 对物质坐标 $\mathbf{X}$ 的梯度：
$$ \mathbf{F}(\mathbf{X}, t) = \nabla_{\mathbf{X}} \boldsymbol{\chi}(\mathbf{X}, t) \equiv \frac{\partial \boldsymbol{\chi}(\mathbf{X}, t)}{\partial \mathbf{X}} $$
其分量形式为 $F_{ij} = \partial x_i / \partial X_j$。$\mathbf{F}$ 在几何上是运动映射在点 $\mathbf{X}$ 处的**切映射** (tangent map)。它的核心作用是将一个位于[参考位](@entry_id:754187)形中点 $\mathbf{X}$ 处的无穷小物质线元向量 $d\mathbf{X}$，线性地映射到当前位形中相应点 $\mathbf{x}$ 处的无穷小空间[线元](@entry_id:196833)向量 $d\mathbf{x}$：
$$ d\mathbf{x} = \mathbf{F} \, d\mathbf{X} $$
因此，$\mathbf{F}$ 包含了关于点 $\mathbf{X}$ 邻域内物质[线元](@entry_id:196833)被拉伸、剪切和旋转的全部信息 [@problem_id:3554307]。

例如，考虑一个运动由 $\boldsymbol{\chi}(\mathbf{X},t) = [(1+t)X_1 + 2tX_2, (1+t^2)X_2, (1+t)X_3 + 3tX_1 X_2]^{\top}$ 给出。在 $t=1$ 时刻，变形梯度为：
$$ \mathbf{F} = \begin{bmatrix} 1+t & 2t & 0 \\ 0 & 1+t^2 & 0 \\ 3tX_2 & 3tX_1 & 1+t \end{bmatrix}_{t=1} = \begin{bmatrix} 2 & 2 & 0 \\ 0 & 2 & 0 \\ 3X_2 & 3X_1 & 2 \end{bmatrix} $$
在物质点 $\mathbf{X}=(1,2,0)^{\top}$ 处，$\mathbf{F}$ 的值为 $\begin{pmatrix} 2 & 2 & 0 \\ 0 & 2 & 0 \\ 6 & 3 & 2 \end{pmatrix}$。一个物质线元 $d\mathbf{X} = (1,-1,2)^{\top}$ 在变形后将变为空间[线元](@entry_id:196833) $d\mathbf{x} = \mathbf{F} d\mathbf{X} = (0,-2,7)^{\top}$ [@problem_id:3554307]。

变形梯度的[行列式](@entry_id:142978)，即**[雅可比行列式](@entry_id:137120)** (Jacobian determinant) $J$，具有特殊的物理意义：
$$ J(\mathbf{X}, t) = \det \mathbf{F}(\mathbf{X}, t) $$
$J$ 度量了局部的体积变化率。一个在[参考位](@entry_id:754187)形中体积为 $dV$ 的无穷小物质微元，在变形后其体积 $dv$ 为：
$$ dv = J \, dV $$
这就是 $J$ 作为局部体积比的解释 [@problem_id:3554356]。前述的**保[向性](@entry_id:144651)**条件在数学上即要求 $J > 0$。如果 $J  0$，则意味着物质微元发生了定向翻转；如果 $J = 0$，则意味着一个有限体积被压缩成了零体积，这对于真实物质来说是不可能的。

基于 $J$ 的体积变化关系，质量守恒定律可以被方便地表达出来。由于物质微元的质量 $dm$ 在变形前后保持不变（$dm = \rho_0 dV = \rho dv$），其中 $\rho_0$ 和 $\rho$ 分别是参考密度和当前密度，我们立即得到物质描述下的连续性方程：
$$ \rho_0(\mathbf{X}) = \rho(\boldsymbol{\chi}(\mathbf{X}, t), t) J(\mathbf{X}, t) \quad \text{或} \quad \rho = \frac{\rho_0}{J} $$
这表明，当材料膨胀（$J > 1$）时，其密度下降；当材料压缩（$J  1$）时，其密度增加 [@problem_id:3554356]。

一个重要的运动学约束是**[不可压缩性](@entry_id:274914)** (incompressibility)，即物质在变形过程中[体积保持](@entry_id:141001)不变。这等价于要求 $J=1$ 在所有物[质点](@entry_id:186768)和所有时刻都成立。例如，一个变形梯度为 $\mathbf{F}=\operatorname{diag}(2, 1/2, 1)$ 的变形，其雅可比行列式 $J = 2 \times 1/2 \times 1 = 1$。尽管主方向上存在拉伸和压缩，但总[体积保持](@entry_id:141001)不变，因此该变形是**等容的** (isochoric)，并且在该点的密度保持不变 $\rho=\rho_0$ [@problem_id:3554356]。

### 运动的率：速度、拉伸与自旋

为了描述变形发生的速度，我们需要引入运动的率量。

**物质速度** $\mathbf{V}$ 是固定物[质点](@entry_id:186768) $\mathbf{X}$ 的位置随时间的变化率，而**[空间速度](@entry_id:190294)** $\mathbf{v}$ 是在 $t$ 时刻占据空间点 $\mathbf{x}$ 的物[质点](@entry_id:186768)的速度：
$$ \mathbf{V}(\mathbf{X}, t) = \frac{\partial \boldsymbol{\chi}(\mathbf{X}, t)}{\partial t} \qquad \mathbf{v}(\mathbf{x}, t) = \mathbf{V}(\boldsymbol{\chi}^{-1}(\mathbf{x}, t), t) $$
在力学分析中，我们更常使用**[空间速度梯度](@entry_id:187198)** $\mathbf{L}$，它被定义为[空间速度](@entry_id:190294)场 $\mathbf{v}$ 对空间坐标 $\mathbf{x}$ 的梯度：
$$ \mathbf{L}(\mathbf{x}, t) = \nabla_{\mathbf{x}} \mathbf{v}(\mathbf{x}, t) $$
$\mathbf{L}$ 描述了速度场在空间中的变化，从而反映了邻近物[质点](@entry_id:186768)之间的相对运动速率。通过[链式法则](@entry_id:190743)，可以建立 $\mathbf{L}$ 与变形梯度 $\mathbf{F}$ 及其时间导数 $\dot{\mathbf{F}}$ 之间的重要关系：
$$ \mathbf{L} = \dot{\mathbf{F}} \mathbf{F}^{-1} $$
这表明[空间速度梯度](@entry_id:187198)包含了关于变形速率的全部信息 [@problem_id:3554297]。

$\mathbf{L}$ 本身可以被分解为其对称[部分和](@entry_id:162077)反对称部分，这两部分具有截然不同的物理意义：
$$ \mathbf{L} = \mathbf{D} + \mathbf{W} $$
其中，
-   **变形率张量** (rate-of-deformation tensor) $\mathbf{D} = \frac{1}{2}(\mathbf{L} + \mathbf{L}^{\top})$ 是对称的。
-   **[自旋张量](@entry_id:187346)** (spin tensor) $\mathbf{W} = \frac{1}{2}(\mathbf{L} - \mathbf{L}^{\top})$ 是反对称的。

$\mathbf{D}$ 描述了物质线元的**拉伸率**和**剪切率**。事实上，一个空间物质[线元](@entry_id:196833) $d\mathbf{x}$ 的长度平方的变化率完全由 $\mathbf{D}$ 决定：
$$ \frac{d}{dt} \left( \|d\mathbf{x}\|^2 \right) = 2 \, d\mathbf{x} \cdot (\mathbf{D} \, d\mathbf{x}) $$
反对称的[自旋张量](@entry_id:187346) $\mathbf{W}$ 在这个二次型中不起作用（$d\mathbf{x} \cdot (\mathbf{W} \, d\mathbf{x}) = 0$）[@problem_id:3554297]。

$\mathbf{W}$ 则描述了物质微元的**刚性转动速率**，也称为**涡度** (vorticity)。

[不可压缩性](@entry_id:274914)条件 $J=1$ 的**率形式**也与这些量相关。$J$ 的[物质时间导数](@entry_id:190892)与 $\mathbf{L}$ 的迹（即 $\mathbf{v}$ 的散度）有关：$\dot{J} = J \operatorname{tr}(\mathbf{L})$。因此，对于[不可压缩材料](@entry_id:159741)（$J=1, \dot{J}=0$），我们必须有 $\operatorname{tr}(\mathbf{L}) = 0$。由于 $\operatorname{tr}(\mathbf{L}) = \operatorname{tr}(\mathbf{D}) + \operatorname{tr}(\mathbf{W})$，并且任何[反对称张量](@entry_id:199349)的迹都恒为零（$\operatorname{tr}(\mathbf{W})=0$），不可压缩性条件最终简化为：
$$ \operatorname{tr}(\mathbf{D}) = 0 \quad (\text{等价于 } \nabla \cdot \mathbf{v} = 0) $$
这表明[不可压缩材料](@entry_id:159741)的变形率是无迹的，即体积变化率为零 [@problem_id:3554297]。

### 客观性与标架无关性

材料的本构关系（例如应力与应变的关系）是物质的内在属性，它不应依赖于观察者。例如，无论观察者是静止的，还是在做匀速或旋转运动，测得的[材料弹性](@entry_id:751729)模量都应该是相同的。这个基本物理原理被称为**物质[标架无关性原理](@entry_id:200995)** (principle of material frame-indifference)，或**[客观性原理](@entry_id:185412)** (principle of objectivity)。

在数学上，一个从[静止参考系](@entry_id:262703)到另一个做[刚体运动](@entry_id:193355)的[参考系](@entry_id:169232)的变换，可以用一个**叠加刚体运动**来表示。在 $t$ 时刻，原空间坐标 $\mathbf{x}$ 变换为新坐标 $\hat{\mathbf{x}}$：
$$ \hat{\mathbf{x}}(t) = \mathbf{c}(t) + \mathbf{Q}(t) \mathbf{x}(t) $$
其中 $\mathbf{c}(t)$ 是一个时变的平移向量，$\mathbf{Q}(t)$ 是一个时变的正交旋转矩阵（$\mathbf{Q}^{\top}\mathbf{Q}=\mathbf{I}$, $\det\mathbf{Q}=1$）[@problem_id:3554333]。

一个标量本身就是客观的。一个空间向量 $\mathbf{u}$ 在此变换下变为 $\hat{\mathbf{u}} = \mathbf{Q} \mathbf{u}$。一个二阶[空间张量](@entry_id:185799) $\mathbf{T}$ 如果被称为**客观的** (objective)，则它必须按如下方式变换：
$$ \hat{\mathbf{T}} = \mathbf{Q} \mathbf{T} \mathbf{Q}^{\top} $$
我们可以检验各个[运动学](@entry_id:173318)量是否客观。通过对叠加[刚体运动](@entry_id:193355)的定义进行[微分](@entry_id:158718)，可以推导出各量的变换规律 [@problem_id:3554333] [@problem_id:3554297]：
-   变形梯度：$\hat{\mathbf{F}} = \mathbf{Q} \mathbf{F}$ (非客观)
-   [右柯西-格林张量](@entry_id:174156) $\mathbf{C} = \mathbf{F}^{\top}\mathbf{F}$：$\hat{\mathbf{C}} = \hat{\mathbf{F}}^{\top}\hat{\mathbf{F}} = (\mathbf{Q}\mathbf{F})^{\top}(\mathbf{Q}\mathbf{F}) = \mathbf{F}^{\top}\mathbf{Q}^{\top}\mathbf{Q}\mathbf{F} = \mathbf{F}^{\top}\mathbf{F} = \mathbf{C}$ (客观，或者更准确地说是**物质客观的**，因为它在变换下不变)
-   [左柯西-格林张量](@entry_id:186163) $\mathbf{B} = \mathbf{F}\mathbf{F}^{\top}$：$\hat{\mathbf{B}} = \hat{\mathbf{F}}\hat{\mathbf{F}}^{\top} = (\mathbf{Q}\mathbf{F})(\mathbf{Q}\mathbf{F})^{\top} = \mathbf{Q}(\mathbf{F}\mathbf{F}^{\top})\mathbf{Q}^{\top} = \mathbf{Q}\mathbf{B}\mathbf{Q}^{\top}$ (客观)
-   [空间速度梯度](@entry_id:187198)：$\hat{\mathbf{L}} = \mathbf{Q} \mathbf{L} \mathbf{Q}^{\top} + \dot{\mathbf{Q}}\mathbf{Q}^{\top}$ (非客观，因为存在额外的仿射项 $\dot{\mathbf{Q}}\mathbf{Q}^{\top}$)
-   变形率张量：$\hat{\mathbf{D}} = \mathbf{Q} \mathbf{D} \mathbf{Q}^{\top}$ (客观)
-   [自旋张量](@entry_id:187346)：$\hat{\mathbf{W}} = \mathbf{Q} \mathbf{W} \mathbf{Q}^{\top} + \dot{\mathbf{Q}}\mathbf{Q}^{\top}$ (非客观)

这些变换规律至关重要，因为它们告诉我们，任何描述物质内在响应的[本构方程](@entry_id:138559)（例如，应力作为变形的函数）必须只通过客观的量来表达。这就是为什么基于 $\mathbf{C}$ 或 $\mathbf{B}$ 的[应变度量](@entry_id:755495)以及变形率 $\mathbf{D}$ 在本构理论中扮演核心角色的原因。

### 应力与[功共轭](@entry_id:194957)

力学分析的另一半是动力学，其核心概念是**应力** (stress)。应力是描述物体内部相互作用力的量度。

最直观的应力张量是**柯西[应力张量](@entry_id:148973)** $\boldsymbol{\sigma}$ (Cauchy stress tensor)。它是一个定义在**当前位形**上的对称张量，通过柯西关系式将作用在当前表面微元上的面力 $\mathbf{t}$ 与该微元的法向 $\mathbf{n}$ 联系起来：$\mathbf{t} = \boldsymbol{\sigma} \mathbf{n}$。

然而，在处理大变形问题时，[本构关系](@entry_id:186508)通常是在[参考位](@entry_id:754187)形中定义的。因此，需要将柯西应力“[拉回](@entry_id:160816)”到[参考位](@entry_id:754187)形。这催生了另外两种[应力张量](@entry_id:148973)：

1.  **[第一皮奥拉-基尔霍夫应力](@entry_id:163971)张量** $\mathbf{P}$ (First Piola-Kirchhoff stress tensor)，也称名义应力 (nominal stress)。它将当前构型中的力与参考构型中的面积联系起来。$\mathbf{P}$ 与 $\boldsymbol{\sigma}$ 的关系为：
    $$ \mathbf{P} = J \boldsymbol{\sigma} \mathbf{F}^{-\top} $$
    $\mathbf{P}$ 的一个特点是它通常是**非对称**的。

2.  **[第二皮奥拉-基尔霍夫应力](@entry_id:173163)张量** $\mathbf{S}$ (Second Piola-Kirchhoff stress tensor)。这是一个完全定义在**[参考位](@entry_id:754187)形**上的对称张量，可以看作是对 $\boldsymbol{\sigma}$ 的完全[拉回](@entry_id:160816)操作的结果：
    $$ \mathbf{S} = \mathbf{F}^{-1} \mathbf{P} = J \mathbf{F}^{-1} \boldsymbol{\sigma} \mathbf{F}^{-\top} $$

这三种[应力张量](@entry_id:148973)并非各自独立，而是同一物理实在的不同数学描述。选择哪一种取决于分析的便利性。一个选择的关键判据是它们与哪些[运动学](@entry_id:173318)率量**[功共轭](@entry_id:194957)** (work-conjugate)。内力在单位时间内所做的功，即[应力功率](@entry_id:182907)，可以有多种等价的表达形式。每种形式都将一个应力张量与一个特定的变形率张量配对 [@problem_id:3554373]。

-   单位**当前体积**的[应力功率](@entry_id:182907) $p$：
    $$ p = \boldsymbol{\sigma} : \mathbf{L} = \boldsymbol{\sigma} : \mathbf{D} $$
    由于 $\boldsymbol{\sigma}$ 是对称的，而 $\mathbf{W}$ 是反对称的，它们的[双点积](@entry_id:748648) $\boldsymbol{\sigma} : \mathbf{W}$ 恒为零。这表明，[应力功率](@entry_id:182907)仅由变形率 $\mathbf{D}$ 产生，而与刚性转动率 $\mathbf{W}$ 无关。因此，$\boldsymbol{\sigma}$ 和 $\mathbf{D}$ 是[功共轭](@entry_id:194957)对 [@problem_id:3554297]。

-   单位**参考体积**的[应力功率](@entry_id:182907) $p_0$：
    $$ p_0 = \mathbf{P} : \dot{\mathbf{F}} $$
    这表明，$\mathbf{P}$ 与变形梯度的[物质时间导数](@entry_id:190892) $\dot{\mathbf{F}}$ 是[功共轭](@entry_id:194957)的。

-   同样是单位**参考体积**的[应力功率](@entry_id:182907) $p_0$，也可以表示为：
    $$ p_0 = \mathbf{S} : \dot{\mathbf{E}} $$
    其中 $\mathbf{E} = \frac{1}{2}(\mathbf{C} - \mathbf{I})$ 是**[格林-拉格朗日应变张量](@entry_id:187745)** (Green-Lagrange strain tensor)。这表明，$\mathbf{S}$ 与 $\mathbf{E}$ 的[物质时间导数](@entry_id:190892) $\dot{\mathbf{E}}$ 是[功共轭](@entry_id:194957)的。

这些[功共轭](@entry_id:194957)关系是超[弹性理论](@entry_id:184142)的基石，它允许我们通过对一个[势能函数](@entry_id:200753)（[应变能密度函数](@entry_id:755490)）对[应变度量](@entry_id:755495)求导来获得应力。例如，$\mathbf{S} = \frac{\partial \Psi(\mathbf{E})}{\partial \mathbf{E}}$。

### 高级主题：再论[参考位](@entry_id:754187)形

到目前为止，我们都默认存在一个物理上可实现的、无应力的[参考位](@entry_id:754187)形。然而，对于许多现实材料，这并非理所当然。经历过塑性变形、非均匀生长（如生物组织）或非均匀[相变](@entry_id:147324)的材料，其内部可能存在即使在没有外部载荷时也无法消除的**残余应力** (residual stress)。

为了模拟这些现象，通常采用**变形梯度的[乘法分解](@entry_id:199514)** (multiplicative decomposition of the deformation gradient)：
$$ \mathbf{F} = \mathbf{F}_e \mathbf{F}_g $$
其中，$\mathbf{F}_g$ 代表局部的、非弹性的“物质重排”，例如生长或塑性应变；$\mathbf{F}_e$ 则代表后续的弹性变形，它是产生应力的部分 [@problem_id:3554299]。

关键在于，$\mathbf{F}_g$ 场在宏观上可能是**不相容的** (incompatible)。这意味着 $\mathbf{F}_g$ 不能作为一个全局变形映射的梯度存在。在数学上，如果 $\mathcal{B}_0$ 是单连通的，这等价于 $\operatorname{Curl} \mathbf{F}_g \neq 0$。从[微分几何](@entry_id:145818)的角度看，这等价于由物质度规 $\bar{g} = \mathbf{F}_g^{\top}\mathbf{F}_g$ 定义的虚拟物质[流形](@entry_id:153038)具有非零的[黎曼曲率](@entry_id:635343) [@problem_id:3554299]。

这种不相容性的物理后果是深刻的：物体无法在三维欧氏空间中找到一个位形，使得其处处无应力。换言之，不存在一个全局的变形 $\boldsymbol{\varphi}$，使得弹性变形 $\mathbf{F}_e = (\nabla \boldsymbol{\varphi}) \mathbf{F}_g^{-1}$ 处处都是纯旋转。为了“拼合”这些局部不相容的变形，材料内部必须产生应力，即残余应力。

这对[计算建模](@entry_id:144775)具有重要启示。当一个无应力的[参考位](@entry_id:754187)形不存在时，我们必须选择一个方便的构型作为计算的**参考**，通常就是物体在载荷作用下的当前已知形状。然后，必须在这个初始状态中明确地引入[残余应力](@entry_id:138788)。这可以通过两种等效的方式实现 [@problem_id:3554299]：
1.  定义一个满足平衡方程（$\operatorname{Div} \mathbf{P}_0 = 0$）的**[初始应力](@entry_id:750652)场** $\mathbf{P}_0$。
2.  定义一个不相容的非弹性场 $\mathbf{F}_g$。在初始构型中，总变形为单位张量 $\mathbf{F}=\mathbf{I}$，这意味着初始弹性变形为 $\mathbf{F}_e = \mathbf{F}_g^{-1}$。[初始应力](@entry_id:750652)则由本构律从 $\mathbf{F}_e$ 计算得出。

这两种方法都为模拟具有复杂[内应力](@entry_id:193721)的材料提供了严谨且实用的出发点。它提醒我们，连续介质力学中的“[参考位](@entry_id:754187)形”可能只是一个数学上的辅助工具，而非一个物理上必须存在的状态。