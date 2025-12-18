## 引言
在生物力学领域，理解组织和器官如何响应力学载荷、如何生长和[适应环境](@entry_id:156246)，是探索生命奥秘和攻克疾病的关键。生物组织——从坚硬的骨骼到柔软的大脑——在微观尺度上都拥有极其复杂的[异质结构](@entry_id:136451)。然而，我们关注的往往是它们在器官层面的宏观功能。那么，我们如何才能跨越从微观离散到宏观连续的鸿沟，建立一个既能精确描述变形又能进行有效计算的力学框架呢？这正是连续介质力学所要解决的核心问题，而其运动学部分，则是整个理论体系的基石。

本文旨在系统性地介绍连续介质力学的运动学理论及其在生物力学中的应用。我们将从最基本的连续介质假设出发，阐明为何可以将由细胞和纤维构成的复杂组织视为一个连续的物质体。随后，在**“原理与机制”**部分，我们将建立描述变形的数学语言，深入探讨变形梯度、有限应变张量、变形率等核心概念，并介绍客观性、生长分解等生物力学特有的高级理论。接下来，在**“应用与跨学科联系”**部分，我们将展示这些看似抽象的理论如何被应用于解决真实的生物学问题，从分析细胞尺度的变形到模拟心脏的电-力耦合，再到揭示大脑皮层褶皱的形成机理。最后，在**“动手实践”**部分，您将通过一系列精心设计的问题，将理论知识转化为解决实际问题的能力。

现在，让我们从最根本的假设开始，一同走进[连续介质力学](@entry_id:155125)的世界，学习如何用精确的数学语言来描述生命的运动与形态变化。

## 原理与机制

本章旨在为读者奠定连续介质力学的运动学基础。我们将从最根本的假设出发，建立一套描述生物组织变形的数学框架，并逐步引入更高级的概念，例如有限应变、变形率以及生物力学中至关重要的客观性、生长和[多相流](@entry_id:146480)动等理论。本章内容是后续章节中讨论本构关系和力学平衡的基础。

### 连续介质假设：从微观结构到场变量

生物组织，例如肌肉、骨骼或血管壁，在微观尺度上具有极其复杂的结构，由细胞、胶原纤维、[细胞外基质](@entry_id:136546)等离散单元构成。直接对每个微观组分进行建模在计算上是不现实的，也无法有效地揭示器官层面的力学行为。为了克服这一挑战，生物力学采用**连续介质假设** (continuum hypothesis)，将组织理想化为一个连续、无间隙的物质体。

这一假设的有效性，依赖于一个关键的**[尺度分离](@entry_id:270204)** (separation of scales) 原则。我们必须能够定义一个**代表性体积元** (Representative Volume Element, RVE)，其尺寸 $L_{\mathrm{RVE}}$ 远大于微观结构的特征尺度 $\ell_{\mathrm{micro}}$（如细胞直径或纤维间距），同时又远小于宏观物理场发生显著变化的特征尺度 $\ell_{\mathrm{macro}}$（如器官的厚度或变形的波长）。这一关系可以表示为：

$$
\ell_{\mathrm{micro}} \ll L_{\mathrm{RVE}} \ll \ell_{\mathrm{macro}}
$$

$L_{\mathrm{RVE}} \gg \ell_{\mathrm{micro}}$ 保证了 RVE 内部包含了足够多的微观组分，从而其平均性质（如密度、刚度）具有统计意义且相对稳定。$L_{\mathrm{RVE}} \ll \ell_{\mathrm{macro}}$ 则保证了我们可以将 RVE 视为一个数学上的“点”，从而能够描述宏观物理场（如应力、应变）在空间中的梯度变化，而不会因平均过程而抹去这些重要的细节。

在连续介质模型中，像**质量密度** $\rho$、**位移** $\boldsymbol{u}$ 或**应力** $\boldsymbol{\sigma}$ 这样的**场变量** (field variables)，实际上是在 RVE 尺度上对微观量进行局部平均后得到的[光滑函数](@entry_id:267124)。例如，某一点的密度 $\rho(\boldsymbol{x}, t)$ 并非指该空间点上某个原子的质量，而是指以 $\boldsymbol{x}$ 为中心的 RVE 内总质量与该 RVE 体积之比。

以[心肌](@entry_id:924326)组织为例，其微观结构包括直径约为 $10-25\,\mu\mathrm{m}$ 的心肌细胞、厚度为 $50-300\,\mu\mathrm{m}$ 的细胞片层等。而其宏观力学行为则体现在心室壁的整体变形上，其厚度约为 $10-30\,\mathrm{mm}$。根据尺度分离原则，一个边长约为 $1\,\mathrm{mm}$ 的立方体（即体积为 $1\,\mathrm{mm}^3$）可以作为一个合理的 RVE。这个尺寸远大于单个细胞或细胞片层，足以包含它们的代表性统计分布（例如纤维方向），同时又远小于心室壁的厚度，足以解析[跨壁](@entry_id:150135)的应力梯度 。

### 运动学：描述运动与变形

运动学是研究物体如何运动和变形的几何学，而不涉及引起运动的力。

#### 运动映射

我们通过**运动** (motion) 函数 $\boldsymbol{\chi}$ 来描述一个连续体的变形。该函数将物体在某个初始时刻 $t=0$ 的形态，即**参考构型** (reference configuration) $\mathcal{B}_0$，中的每一个**物[质点](@entry_id:186768)** (material point) $\boldsymbol{X}$，映射到当前时刻 $t$ 在物理空间中的位置 $\boldsymbol{x}$。数学上表示为：

$$
\boldsymbol{x} = \boldsymbol{\chi}(\boldsymbol{X}, t)
$$

$\boldsymbol{X}$ 被称为**物质坐标** (material coordinates) 或**拉格朗日坐标** (Lagrangian coordinates)，它如同一个贴在物质点上的永久标签，不随时间改变。而 $\boldsymbol{x}$ 被称为**空间坐标** (spatial coordinates) 或**欧拉坐标** (Eulerian coordinates)，它描述了物[质点](@entry_id:186768)在某一时刻的瞬时空间位置。物体在时刻 $t$ 所占据的空间区域被称为**当前构型** (current configuration) $\mathcal{B}_t$，即 $\mathcal{B}_t = \boldsymbol{\chi}(\mathcal{B}_0, t)$ 。

从物理角度出发，运动映射 $\boldsymbol{\chi}$ 必须满足几个基本条件：
1.  **光滑性**：$\boldsymbol{\chi}$ 必须足够光滑，以保证其导数存在，这是进行后续运动学和力学分析的前提。
2.  **[单射性](@entry_id:147722) (Injectivity)**：不同的物[质点](@entry_id:186768)在同一时刻不能占据相同的空间位置，这体现了“物质不可穿透”的物理公理。
3.  **方向保持性**：物质微元在变形后不能被“翻转”（例如，从[右手坐标系](@entry_id:166669)变为左手坐标系）。

#### 变形梯度

为了量化局部的变形，我们引入一个核心的运动学量——**变形梯度张量** (deformation gradient tensor) $\boldsymbol{F}$。它被定义为运动映射 $\boldsymbol{\chi}$ 对物质坐标 $\boldsymbol{X}$ 的梯度：

$$
\boldsymbol{F} = \frac{\partial \boldsymbol{x}}{\partial \boldsymbol{X}} = \nabla_{\boldsymbol{X}} \boldsymbol{\chi}
$$

$\boldsymbol{F}$ 是一个[二阶张量](@entry_id:199780)，其分量形式为 $F_{iJ} = \partial x_i / \partial X_J$。变形梯度描述了参考构型中的一个无限小矢量 $d\boldsymbol{X}$ 如何被映射为当前构型中的矢量 $d\boldsymbol{x}$：

$$
d\boldsymbol{x} = \boldsymbol{F} d\boldsymbol{X}
$$

变形梯度的行列式，即**[雅可比行列式](@entry_id:137120)** (Jacobian determinant) $J = \det \boldsymbol{F}$，具有明确的物理意义。它代表了局部的体积变化率，即当前构型中的一个无限小体积元 $dv$ 与其对应的参考构型中的[体积元](@entry_id:267802) $dV$ 之间的关系为 $dv = J dV$。根据前述的方向保持性要求，[雅可比行列式](@entry_id:137120)必须恒为正，即 $J > 0$ 。

考虑一个[骨骼肌](@entry_id:147955)微元的变形，其映射关系为 $x_1=\lambda_f X_1$, $x_2=s X_1+\lambda_t X_2$, $x_3=\lambda_t X_3$，其中 $\lambda_f$ 和 $\lambda_t$ 分别是纤维方向和横向的拉伸比。其变形梯度为：
$$
\boldsymbol{F} = \begin{pmatrix} \lambda_f & 0 & 0 \\ s & \lambda_t & 0 \\ 0 & 0 & \lambda_t \end{pmatrix}
$$
其雅可比行列式为 $J = \det(\boldsymbol{F}) = \lambda_f \lambda_t^2$。如果[肌肉收缩](@entry_id:153054)是**不可压缩的** (incompressible)，意味着局部[体积保持](@entry_id:141001)不变，即 $J=1$。例如，当 $\lambda_f=1.2$ 且 $\lambda_t=1/\sqrt{1.2}$ 时，我们得到 $J=1.2 \times (1/\sqrt{1.2})^2 = 1$，这代表了一次[等容变形](@entry_id:196451)，即使其中包含了剪切 ($s \neq 0$) 。

[质量守恒定律](@entry_id:147377)要求一个物质微元的质量 $dm$ 保持不变，即 $dm = \rho_0 dV = \rho dv$。结合 $dv=J dV$，我们得到当前密度 $\rho$ 与参考密度 $\rho_0$ 的关系：

$$
\rho = \frac{\rho_0}{J}
$$

对于[不可压缩材料](@entry_id:159741)，$J=1$，因此密度始终保持为 $\rho_0$。

#### 变形的相容性

并非任何一个 $J>0$ 的[二阶张量](@entry_id:199780)场 $\boldsymbol{F}(\boldsymbol{X})$ 都能成为一个有效的变形梯度。为了使 $\boldsymbol{F}$ 能够由一个单值的、连续的运动场 $\boldsymbol{\chi}$ 导出（即 $\boldsymbol{F}=\nabla_{\boldsymbol{X}}\boldsymbol{\chi}$），它必须满足**[相容性条件](@entry_id:637057)** (compatibility condition)。对于一个**单连通** (simply connected) 的物体（即内部无孔洞），该条件可以表示为 $\boldsymbol{F}$ 的旋度为零：

$$
\text{Curl} \, \boldsymbol{F} = \boldsymbol{0}
$$

这里，[旋度算子](@entry_id:184984)作用于张量 $\boldsymbol{F}$ 的每一行。这个条件保证了沿任何闭合路径 $\mathcal{C}$ 的[线积分](@entry_id:141417) $\oint_{\mathcal{C}} \boldsymbol{F} \, d\boldsymbol{X}$ 均为零，从而确保了由积分定义的位移场 $\boldsymbol{u}(\boldsymbol{X}) = \int \boldsymbol{F} \, d\boldsymbol{X} - \boldsymbol{X}$ 的[单值性](@entry_id:174849)。如果一个给定的$\boldsymbol{F}$场不满足此条件，则说明它不可能来自一个连续光滑的物体变形，或者该物体内部存在着像位错那样的缺陷 。

### [有限应变度量](@entry_id:185716)

变形梯度 $\boldsymbol{F}$ 本身包含了拉伸和旋转两种信息，不是一个纯粹的[应变度量](@entry_id:755495)。为了只量化变形（拉伸和剪切），我们需要引入不随[刚体转动](@entry_id:191086)变化的张量。

#### 拉伸与应变张量

通过**极分解** (polar decomposition)，我们可以将 $\boldsymbol{F}$ 分解为一个[旋转张量](@entry_id:191990) $\boldsymbol{R}$ 和一个[对称正定](@entry_id:145886)的[拉伸张量](@entry_id:193200) $\boldsymbol{U}$ 或 $\boldsymbol{V}$：$\boldsymbol{F}=\boldsymbol{R}\boldsymbol{U}=\boldsymbol{V}\boldsymbol{R}$。其中，$\boldsymbol{U}$ 是**右[拉伸张量](@entry_id:193200)**，$\boldsymbol{V}$ 是**左[拉伸张量](@entry_id:193200)**。

基于[拉伸张量](@entry_id:193200)，我们定义两个重要的变形张量：
- **右柯西-格林变形张量** (Right Cauchy-Green deformation tensor): $\boldsymbol{C} = \boldsymbol{F}^\mathsf{T} \boldsymbol{F} = \boldsymbol{U}^2$。这是一个定义在参考构型上的**物质张量** (material tensor)。
- **左柯西-格林变形张量** (Left Cauchy-Green deformation tensor): $\boldsymbol{B} = \boldsymbol{F}\boldsymbol{F}^\mathsf{T} = \boldsymbol{V}^2$。这是一个定义在当前构型上的**[空间张量](@entry_id:185799)** (spatial tensor)。

从 $\boldsymbol{C}$ 和 $\boldsymbol{B}$ 出发，可以定义两种常用的[有限应变度量](@entry_id:185716)：
1.  **[格林-拉格朗日应变张量](@entry_id:187745)** (Green-Lagrange strain tensor) $\boldsymbol{E}$，定义为：
    $$
    \boldsymbol{E} = \frac{1}{2}(\boldsymbol{C} - \boldsymbol{I})
    $$
    $\boldsymbol{E}$ 是一个物质张量，它量化了物质[线元](@entry_id:196833)平方长度的变化。具体来说，$ds^2 - dS^2 = 2 d\boldsymbol{X} \cdot (\boldsymbol{E} d\boldsymbol{X})$，其中 $dS$ 和 $ds$ 分别是[线元](@entry_id:196833)在参考构型和当前构型中的长度。当没有变形时（$\boldsymbol{F}=\boldsymbol{I}$），$\boldsymbol{C}=\boldsymbol{I}$ 且 $\boldsymbol{E}=\boldsymbol{0}$。

2.  **[欧拉-阿尔曼西应变张量](@entry_id:194948)** (Euler-Almansi strain tensor) $\boldsymbol{e}$，定义为：
    $$
    \boldsymbol{e} = \frac{1}{2}(\boldsymbol{I} - \boldsymbol{B}^{-1})
    $$
    $\boldsymbol{e}$ 是一个[空间张量](@entry_id:185799)，它同样量化了平方长度的变化，但从空间构型角度描述：$ds^2 - dS^2 = 2 d\boldsymbol{x} \cdot (\boldsymbol{e} d\boldsymbol{x})$。

$\boldsymbol{E}$ 和 $\boldsymbol{e}$ 描述的是同一个物理应变状态，但分别是在参考构型和当前构型中的表示。它们之间可以通过变形梯度进行转换（**推前** (push-forward) 和**拉回** (pull-back) 操作）：
$$
\boldsymbol{e} = \boldsymbol{F}^{-\mathsf{T}} \boldsymbol{E} \boldsymbol{F}^{-1}, \quad \boldsymbol{E} = \boldsymbol{F}^{\mathsf{T}} \boldsymbol{e} \boldsymbol{F}
$$
在微小应变情况下，当[位移梯度](@entry_id:165352)$\nabla \boldsymbol{u}$很小时，$\boldsymbol{F} \approx \boldsymbol{I} + \nabla \boldsymbol{u}$，$\boldsymbol{E}$ 和 $\boldsymbol{e}$ 都会退化为经典的**[无穷小应变张量](@entry_id:167211)** $\boldsymbol{\varepsilon} = \frac{1}{2}(\nabla\boldsymbol{u} + (\nabla\boldsymbol{u})^\mathsf{T})$ 。

#### [应变不变量](@entry_id:190518)与主拉伸

为了构建不依赖于坐标系选择的[本构模型](@entry_id:174726)（特别是对于[各向同性材料](@entry_id:170678)），我们通常使用应变张量的不变量。[对称张量](@entry_id:148092) $\boldsymbol{C}$ 有三个**[主不变量](@entry_id:193522)** (principal invariants)：
- $I_1 = \text{tr}(\boldsymbol{C})$
- $I_2 = \frac{1}{2}[(\text{tr}(\boldsymbol{C}))^2 - \text{tr}(\boldsymbol{C}^2)]$
- $I_3 = \det(\boldsymbol{C})$

这些不变量可以通过**主拉伸比** (principal stretches) $\lambda_1, \lambda_2, \lambda_3$（即右[拉伸张量](@entry_id:193200) $\boldsymbol{U}$ 的特征值）来表达。$\boldsymbol{C}$ 的特征值是 $\lambda_i^2$，因此：
- $I_1 = \lambda_1^2 + \lambda_2^2 + \lambda_3^2$
- $I_2 = \lambda_1^2 \lambda_2^2 + \lambda_2^2 \lambda_3^2 + \lambda_3^2 \lambda_1^2$
- $I_3 = \lambda_1^2 \lambda_2^2 \lambda_3^2 = (\lambda_1 \lambda_2 \lambda_3)^2$

注意到 $\det(\boldsymbol{F}) = \det(\boldsymbol{R}\boldsymbol{U}) = \det(\boldsymbol{R})\det(\boldsymbol{U}) = 1 \cdot (\lambda_1\lambda_2\lambda_3)$，所以 $J = \lambda_1\lambda_2\lambda_3$。因此，第三不变量与[雅可比行列式](@entry_id:137120)直接相关：$I_3 = J^2$。对于[不可压缩材料](@entry_id:159741)，$J=1$，所以 $I_3=1$ 。

### 运动与变形的率

在许多生物力学问题中，如血流动力学或[组织粘弹性](@entry_id:923952)，变形的速率至关重要。

#### 速度与速度梯度

物[质点](@entry_id:186768) $\boldsymbol{X}$ 的**速度**可以从两个角度描述：
- **物质速度** (Material velocity)：$\boldsymbol{V}(\boldsymbol{X}, t) = \frac{\partial \boldsymbol{\chi}(\boldsymbol{X}, t)}{\partial t}$，描述了固定物质点 $\boldsymbol{X}$ 的速度。
- **[空间速度](@entry_id:190294)** (Spatial velocity)：$\boldsymbol{v}(\boldsymbol{x}, t)$，描述了当前时刻占据空间点 $\boldsymbol{x}$ 的那个物[质点](@entry_id:186768)的速度。

两者之间的关系为 $\boldsymbol{v}(\boldsymbol{\chi}(\boldsymbol{X}, t), t) = \boldsymbol{V}(\boldsymbol{X}, t)$ 。

描述速度场在空间中的变化的量是**[空间速度梯度](@entry_id:187198)** (spatial velocity gradient) $\boldsymbol{L}$：
$$
\boldsymbol{L} = \nabla_{\boldsymbol{x}} \boldsymbol{v}
$$

#### 变形率与自旋

[空间速度梯度](@entry_id:187198) $\boldsymbol{L}$ 可以分解为其对称部分和反对称部分，分别描述了物质的变形速率和刚性转动速率。
- **变形率张量** (Rate-of-deformation tensor) $\boldsymbol{D}$：
  $$
  \boldsymbol{D} = \frac{1}{2}(\boldsymbol{L} + \boldsymbol{L}^\mathsf{T})
  $$
  $\boldsymbol{D}$ 的对角分量表示沿坐标轴方向的拉伸或压缩速率，非对角分量表示剪切角的变化率。

- **[自旋张量](@entry_id:187346)** (Spin tensor) $\boldsymbol{W}$：
  $$
  \boldsymbol{W} = \frac{1}{2}(\boldsymbol{L} - \boldsymbol{L}^\mathsf{T})
  $$
  $\boldsymbol{W}$ 描述了物质微元的瞬时[刚体](@entry_id:1131033)旋转角速度。

考虑一个由剪切率为 $\dot{\gamma}_0$ 的简单剪切和角速度为 $\omega_0$ 的[刚体](@entry_id:1131033)旋转叠加而成的速度场 $\boldsymbol{v} = ((\dot{\gamma}_0 - \omega_0)y, \omega_0 x, 0)$。其[速度梯度](@entry_id:261686)为 $\boldsymbol{L} = \begin{pmatrix} 0 & \dot{\gamma}_0 - \omega_0 & 0 \\ \omega_0 & 0 & 0 \\ 0 & 0 & 0 \end{pmatrix}$。通过分解可以发现，变形率张量 $\boldsymbol{D}$ 只与剪切率 $\dot{\gamma}_0$ 有关，而与刚性转动 $\omega_0$ 无关。$\boldsymbol{D}$ 的[主值](@entry_id:189577)（特征值）为 $\pm \dot{\gamma}_0/2$ 和 $0$，对应于与坐标轴成 $\pm 45^{\circ}$ 的拉伸和压缩方向。这表明纯[剪切流](@entry_id:266817)动可以被看作是两个正交方向上的等量拉伸和压缩。而[自旋张量](@entry_id:187346) $\boldsymbol{W}$ 则同时包含了剪切流动内在的旋转和外加的[刚体](@entry_id:1131033)旋转 。

#### 不可压缩性再探

一个重要的运动学关系将有限变形的度量 $J$ 与瞬时变形率的度量 $\boldsymbol{D}$ 联系起来。可以证明，$J$ 的[物质时间导数](@entry_id:190892) $\dot{J}$ 与 $\boldsymbol{L}$ 的迹（即 $\boldsymbol{D}$ 的迹）满足以下关系，即**欧拉展开公式** (Euler's expansion formula)：
$$
\dot{J} = J \, \text{tr}(\boldsymbol{L}) = J \, \text{tr}(\boldsymbol{D})
$$
$\text{tr}(\boldsymbol{D}) = \nabla \cdot \boldsymbol{v}$ 表示速度场的散度，即局部体积的膨胀率。

这个公式清晰地表明，瞬时不可压缩（或称**等容流动**）的条件是 $\text{tr}(\boldsymbol{D})=0$。如果一个材料在初始时刻是不可压缩的（即 $J(\boldsymbol{X}, 0)=1$），并且在随后的整个运动过程中始终满足 $\text{tr}(\boldsymbol{D})=0$，那么对上述[微分](@entry_id:158422)方程积分可知，$J(\boldsymbol{X}, t)$ 将恒等于1。因此，有限变形的不可压缩条件 $J=1$ 和瞬时流动的不可压缩条件 $\text{tr}(\boldsymbol{D})=0$ 是等价的，后者并非只适用于小应变情况 。

### 生物力学中的高级运动学概念

#### [客观性原理](@entry_id:185412)

物理定律和材料的本构关系不应依赖于观察者。这一基本原则被称为**[客观性原理](@entry_id:185412)** (principle of objectivity) 或**标架无关性** (frame indifference)。考虑两个观察者，他们的坐标系通过一个随时间变化的[刚体运动](@entry_id:144691)相关联：$\boldsymbol{x}^{*} = \boldsymbol{Q}(t)\boldsymbol{x} + \boldsymbol{c}(t)$，其中 $\boldsymbol{Q}(t)$ 是一个[旋转张量](@entry_id:191990)。

一个物理量被称为是**客观的** (objective)，如果它在不同观察者坐标系下的表示遵循特定的转换规则。对于空间场，这些规则是：
- **客观标量** (Objective scalar) $s$：$s^{*}(\boldsymbol{x}^{*},t) = s(\boldsymbol{x},t)$
- **客观向量** (Objective vector) $\boldsymbol{a}$：$\boldsymbol{a}^{*}(\boldsymbol{x}^{*},t) = \boldsymbol{Q}(t)\boldsymbol{a}(\boldsymbol{x},t)$
- **客观[二阶张量](@entry_id:199780)** (Objective second-order tensor) $\boldsymbol{A}$：$\boldsymbol{A}^{*}(\boldsymbol{x}^{*},t) = \boldsymbol{Q}(t)\boldsymbol{A}(\boldsymbol{x},t)\boldsymbol{Q}^{\mathsf{T}}(t)$

可以证明，[格林-拉格朗日应变](@entry_id:170427) $\boldsymbol{E}$ 和[欧拉-阿尔曼西应变](@entry_id:187104) $\boldsymbol{e}$ 都是客观的[应变度量](@entry_id:755495)。同样，变形率张量 $\boldsymbol{D}$ 也是客观的。然而，变形梯度 $\boldsymbol{F}$、[空间速度梯度](@entry_id:187198) $\boldsymbol{L}$ 和[自旋张量](@entry_id:187346) $\boldsymbol{W}$ 都不是客观的，因为它们的转换规则中包含了与观察者相对转动相关的附加项。因此，在构建描述材料真实物理响应的本构方程时，必须使用客观的张量   。

#### 生长运动学：[乘法分解](@entry_id:199514)

生物生长是一个复杂的过程，它导致组织质量和体积的永久性变化，并常常伴随着**[残余应力](@entry_id:138788)** (residual stress) 的产生。为了在[连续介质力学](@entry_id:155125)框架下描述这一现象，**变形梯度的[乘法分解](@entry_id:199514)** (multiplicative decomposition of the deformation gradient) 被广泛采用：

$$
\boldsymbol{F} = \boldsymbol{F}_e \boldsymbol{F}_g
$$

这个分解提出一个概念上的“三步”过程：
1.  **生长**：参考构型 $\mathcal{B}_0$ 中的物质微元 $d\boldsymbol{X}$ 经历一个由**[生长张量](@entry_id:1125835)** $\boldsymbol{F}_g$ 描述的局部变形，变为一个假想的、无应力的**生长构型** $\mathcal{B}_g$ 中的微元 $d\boldsymbol{X}_g = \boldsymbol{F}_g d\boldsymbol{X}$。这个过程是不可逆的，不储存弹性能。
2.  **弹性变形**：由于生长在不同位置和方向上可能不均匀，各个独立的 $d\boldsymbol{X}_g$ 拼凑在一起可能无法形成一个连续的物体（即 $\text{Curl}\,\boldsymbol{F}_g \neq \boldsymbol{0}$，称 $\boldsymbol{F}_g$ 是**不相容的**）。为了保持物体的连续和完整，必须施加一个**弹性变形张量** $\boldsymbol{F}_e$，将 $d\boldsymbol{X}_g$ 映射到最终的、真实的当前构型中的 $d\boldsymbol{x} = \boldsymbol{F}_e d\boldsymbol{X}_g$。
3.  **总变形**：最终的总变形 $\boldsymbol{F} = \boldsymbol{F}_e \boldsymbol{F}_g$ 必须是相容的（$\text{Curl}\,\boldsymbol{F} = \boldsymbol{0}$）。

正是这个为了维持连续性而不得不产生的弹性变形 $\boldsymbol{F}_e$，导致了[残余应力](@entry_id:138788)的出现。即使在没有任何外力的情况下，只要生长是不相容的，组织内部也会存在自平衡的应[力场](@entry_id:147325)。材料的弹性能和应力响应由弹性变形决定，因此本构关系是基于由 $\boldsymbol{F}_e$ 导出的[应变度量](@entry_id:755495)（如 $\boldsymbol{C}_e = \boldsymbol{F}_e^\mathsf{T} \boldsymbol{F}_e$）来建立的 。

#### 多孔介质运动学

许多生物组织，如软骨、骨骼和肿瘤，可以被建模为**多孔介质** (porous media)，即一个可变形的固体骨架，其孔隙中充满了流体。在 mixture theory（[混合物理论](@entry_id:908766)）的框架下，我们为每个组分（固体和流体）分别定义速度场。

设固体骨架的速度为 $\boldsymbol{v}_s(\boldsymbol{x}, t)$，间质流体的速度为 $\boldsymbol{v}_f(\boldsymbol{x}, t)$。对组织的力学功能和物质输运起决定性作用的是两者之间的[相对运动](@entry_id:169798)，这通过**渗流速度** (seepage velocity) 或相对速度来量化：

$$
\boldsymbol{v}_{rel} = \boldsymbol{v}_f - \boldsymbol{v}_s
$$

这种相对流动是[关节软骨](@entry_id:922365)润滑和营养物质输送的关键机制。在分析溶质（如营养物或药物）在组织中的输运时，必须正确处理这种相对运动。例如，考虑一个随固体骨架运动的控制体 $V_s(t)$，溶质仅存在于孔隙流体中，其输运是纯对流的。穿过该控制体边界的溶质通量，取决于溶质相对于运动边界的速度，即 $\boldsymbol{v}_f - \boldsymbol{v}_s$。基于此，并应用适用于随动控制体的**雷诺输运定理** (Reynolds Transport Theorem)，可以推导出溶质浓度变化的局部守恒方程。这个过程突显了在多相系统中，选择合适的参考坐标系并精确描述相对运动的重要性 。