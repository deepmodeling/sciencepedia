## 引言
理解材料在外力作用下的响应方式，是所有工程设计与科学研究的基石。无论是设计一座宏伟的桥梁，开发下一代高性能电池，还是揭示生命过程的奥秘，我们都必须面对一个核心问题：物质如何变形，以及如何量化其内部的力？应力、应变与弹性变形的概念为回答这些问题提供了统一而强大的语言。然而，从直观的拉伸与压缩到描述复杂三维状态的严谨数学框架之间，存在着一条需要系统学习才能跨越的鸿沟。

本文旨在为读者构建一个关于应力、应变和弹性变形的完整知识体系。我们将超越简单的标量定义，深入探讨其作为张量的本质，并展示这一理论框架如何应用于从宏观到微观的广阔领域。通过本文的学习，你将能够：

- 在第一章“原理与机制”中，建立对柯西[应力张量](@entry_id:148973)、微小及有限应变张量、以及基于[热力学](@entry_id:141121)的各向同性与[各向异性弹性](@entry_id:186771)[本构关系](@entry_id:186508)的深刻理解。
- 在第二章“应用与交叉学科联系”中，见证这些基本原理如何解决土木工程、[材料科学](@entry_id:152226)、实验力学乃至生物化学等领域的实际问题。
- 在第三章“动手实践”中，通过具体计算练习，将抽象的理论转化为解决问题的实用技能。

现在，让我们从最基本的原理出发，踏上探索[材料力学](@entry_id:201885)行为核心奥秘的旅程。

## 原理与机制

在对材料行为进行力学分析时，理解在外力作用下材料内部如何响应以及如何描述其形状变化是至关重要的。本章旨在系统地阐述应力、应变和弹性变形的“原理与机制”。我们将从最基本的概念出发，建立一个严谨的张量框架，用以描述从微小变形到有限变形的力学行为，并探讨材料[本构关系](@entry_id:186508)的[热力学](@entry_id:141121)基础及其在各向同性与各向异性材料中的具体形式。

### 应力的概念：柯西[应力张量](@entry_id:148973)

当一个连续体受到外部载荷或[体力](@entry_id:174230)时，其内部会产生相互作用力以维持平衡。为了量化这些内力，我们想象用一个虚拟的平面将物体在某一点切开。在该点周围，平面一侧的材料会对另一侧的材料施加一个[分布](@entry_id:182848)力。在极限情况下，当[截面](@entry_id:154995)面积趋于零时，单位面积上的力被定义为**牵[引力](@entry_id:175476)矢量** (traction vector)，记为 $\mathbf{t}$。这个牵[引力](@entry_id:175476)矢量的大小和方向不仅取决于物体内部考察点的位置，还依赖于[截面](@entry_id:154995)的方向，该方向由[截面](@entry_id:154995)的[单位法向量](@entry_id:178851) $\mathbf{n}$ 描述。

一个核心的问题是：我们是否需要知道在每一个可能的[截面](@entry_id:154995)方向上的牵[引力](@entry_id:175476)来完全描述一个点的应力状态？Augustin-Louis Cauchy 的一个杰出贡献在于证明了这一点是不必要的。通过对一个无限小的四面体进行力平衡分析，可以证明，任意方向 $\mathbf{n}$ 上的牵[引力](@entry_id:175476)矢量 $\mathbf{t}^{(\mathbf{n})}$ 与[法向量](@entry_id:264185) $\mathbf{n}$ 之间存在线性关系。这个[线性映射](@entry_id:185132)关系本身就完整地定义了该点的应力状态。这个[线性映射](@entry_id:185132)算子就是**柯西[应力张量](@entry_id:148973)** (Cauchy stress tensor)，记为[二阶张量](@entry_id:199780) $\boldsymbol{\sigma}$。[@problem_id:2525690] 它们的关系式为：

$$
\mathbf{t}^{(\mathbf{n})} = \boldsymbol{\sigma}\mathbf{n}
$$

或者用分量形式写为 $t_i = \sigma_{ij}n_j$，这里我们采用了爱因斯坦求和约定。

$\boldsymbol{\sigma}$ 的分量 $\sigma_{ij}$ 具有明确的物理意义。分量 $\sigma_{ij}$ 代表作用在法向量指向 $j$ 坐标轴方向的微小平面上，沿 $i$ 坐标轴方向的力分量。[@problem_id:2525690] 例如，$\sigma_{11}$ 是作用在垂直于 $x_1$ 轴的平面上的正向力分量（[正应力](@entry_id:260622)），而 $\sigma_{12}$ 是作用在垂直于 $x_2$ 轴的平面上，沿 $x_1$ 轴方向的剪切力分量（切应力）。

在没有[体力](@entry_id:174230)矩或微观结构力偶矩的情况下，对一个无限小的立方体单元应用[角动量守恒](@entry_id:156798)定律，可以证明柯西应力张量必须是对称的，即 $\sigma_{ij} = \sigma_{ji}$。[@problem_id:2525690] 这意味着在描述一般三维应力状态时，$\boldsymbol{\sigma}$ 的九个分量中只有六个是独立的。

应力张量可以分解为一个球形[部分和](@entry_id:162077)一个偏量部分。球形部分描述了体积的变化趋势，而偏量部分描述了形状的变化趋势。在[流体力学](@entry_id:136788)中，压力通常被定义为压应力。在固体力学中，我们通常将拉伸应力定义为正。为了与压为正的压力概念兼容，**力学压力** (mechanical pressure) $p$ 通常定义为平均正应力的相反数：

$$
p = -\frac{1}{3}(\sigma_{11} + \sigma_{22} + \sigma_{33}) = -\frac{1}{3}\text{tr}(\boldsymbol{\sigma})
$$

其中 $\text{tr}(\boldsymbol{\sigma})$ 是[应力张量](@entry_id:148973)的迹。在这种约定下，正压力 $p>0$ 意味着压缩状态。一个纯静水压力状态对应于 $\boldsymbol{\sigma} = -p\mathbf{I}$，其中 $\mathbf{I}$ 是单位张量。[@problem_id:2525690]

### 变形的描述：[应变张量](@entry_id:193332)

为了描述材料的变形，我们需要一个能够量化其形状和尺寸变化的数学工具。

#### 微[小变形理论](@entry_id:174991)

在许多工程应用中，材料的变形非常小，位移的梯度远小于1。在这种情况下，我们可以使用微[小变形理论](@entry_id:174991)。一个点 $\mathbf{x}$ 的**位移场** (displacement field) $\mathbf{u}(\mathbf{x})$ 描述了它从参考构型到当前构型的移动。变形的局部信息包含在**[位移梯度张量](@entry_id:748571)** $\nabla\mathbf{u}$ 中，其分量为 $(\nabla\mathbf{u})_{ij} = u_{i,j} = \partial u_i / \partial x_j$。

[位移梯度张量](@entry_id:748571)可以唯一地分解为一个对称部分和一个反对称部分：

$$
\nabla\mathbf{u} = \frac{1}{2}(\nabla\mathbf{u} + (\nabla\mathbf{u})^T) + \frac{1}{2}(\nabla\mathbf{u} - (\nabla\mathbf{u})^T)
$$

对称部分被称为**无限[小应变张量](@entry_id:754968)** (infinitesimal strain tensor) $\boldsymbol{\epsilon}$，它描述了材料的真实变形（形状和尺寸的改变）。反对称部分被称为**无限小转动张量** (infinitesimal rotation tensor) $\boldsymbol{\omega}$，它描述了材料的局部[刚体转动](@entry_id:191086)。[@problem_id:2525695]

$$
\boldsymbol{\epsilon} = \frac{1}{2}(\nabla\mathbf{u} + (\nabla\mathbf{u})^T) \quad \text{;} \quad \boldsymbol{\omega} = \frac{1}{2}(\nabla\mathbf{u} - (\nabla\mathbf{u})^T)
$$

一个核心的物理原理是**物质框架无关性** (material frame-indifference)，它要求材料的[本构关系](@entry_id:186508)（如[应力-应变关系](@entry_id:274093)）不应依赖于[刚体运动](@entry_id:193355)。这意味着应力只能由应变 $\boldsymbol{\epsilon}$ 决定，而不能由转动 $\boldsymbol{\omega}$ 决定。纯[刚体转动](@entry_id:191086)不应产生应力。[@problem_id:2525695]

[应变张量](@entry_id:193332)的分量同样具有清晰的物理意义。对角分量 $\epsilon_{ii}$ (例如 $\epsilon_{11}$) 描述了沿 $x_i$ 轴方向的**正向应变** (normal strain)，即材料[线元](@entry_id:196833)的伸长或缩短。非对角分量 $\epsilon_{ij}$ ($i \neq j$) 描述了**张量剪切应变** (tensorial shear strain)。它与**工程剪切应变** (engineering shear strain) $\gamma_{ij}$ 有关。$\gamma_{ij}$ 被定义为最初沿 $x_i$ 和 $x_j$ 轴的两个[线元](@entry_id:196833)之间直角的变化量。通过[几何分析](@entry_id:157700)可以严格证明，在小变形假设下，两者关系为 $\gamma_{ij} = 2\epsilon_{ij}$。[@problem_id:2525692] 此外，应变张量的迹 $\text{tr}(\boldsymbol{\epsilon}) = \epsilon_{11} + \epsilon_{22} + \epsilon_{33}$ 代表了材料的**体应变** (volumetric strain)，即单位体积的变化率。[@problem_id:2525695]

#### 有限变形理论

当变形较大时，微小应变理论不再适用。我们需要更通用的变形度量。变形的基本描述是**变形梯度张量** (deformation gradient) $\mathbf{F}$，它将参考构型中的一个无限小[线元](@entry_id:196833) $d\mathbf{X}$ 映射到当前构型中的对应[线元](@entry_id:196833) $d\mathbf{x}$：$d\mathbf{x} = \mathbf{F} d\mathbf{X}$。

通过比较变形前后[线元](@entry_id:196833)长度的平方，$ds^2 = d\mathbf{x} \cdot d\mathbf{x}$ 和 $dS^2 = d\mathbf{X} \cdot d\mathbf{X}$，我们可以定义有限应变张量。

**[格林-拉格朗日应变张量](@entry_id:187745)** (Green-Lagrange strain tensor) $\mathbf{E}$ 是一个定义在参考构型（材料[坐标系](@entry_id:156346)）下的[应变度量](@entry_id:755495)：

$$
\mathbf{E} = \frac{1}{2}(\mathbf{F}^T\mathbf{F} - \mathbf{I}) = \frac{1}{2}(\mathbf{C} - \mathbf{I})
$$

其中 $\mathbf{C} = \mathbf{F}^T\mathbf{F}$ 是**右柯西-格林变形张量** (right Cauchy-Green deformation tensor)。$\mathbf{E}$ 的一个重要特性是它是“客观的”，即在[刚体转动](@entry_id:191086)下保持不变，因此它真实地度量了变形。[@problem_id:2525669]

**[欧拉-阿尔曼西应变张量](@entry_id:194948)** (Euler-Almansi strain tensor) $\mathbf{e}$ 是一个定义在当前构型（空间[坐标系](@entry_id:156346)）下的[应变度量](@entry_id:755495)：

$$
\mathbf{e} = \frac{1}{2}(\mathbf{I} - (\mathbf{F}^{-1})^T\mathbf{F}^{-1}) = \frac{1}{2}(\mathbf{I} - \mathbf{b}^{-1})
$$

其中 $\mathbf{b} = \mathbf{F}\mathbf{F}^T$ 是**左柯西-格林变形张量** (left Cauchy-Green deformation tensor)。在小变形极限下，即 $\mathbf{F} = \mathbf{I} + \nabla\mathbf{u}$ 且 $\|\nabla\mathbf{u}\| \ll 1$，可以证明 $\mathbf{E}$ 和 $\mathbf{e}$ 都将退化为无限[小应变张量](@entry_id:754968) $\boldsymbol{\epsilon}$。[@problem_id:2525669]

在处理大变形问题时，选择合适的应力度量和[应变度量](@entry_id:755495)至关重要。除了柯西应力（真实应力），还有**第一类[皮奥拉-基尔霍夫应力](@entry_id:173629)张量** (First Piola-Kirchhoff stress) $\mathbf{P}$（名义应力）和**第二类[皮奥拉-基尔霍夫应力](@entry_id:173629)张量** (Second Piola-Kirchhoff stress) $\mathbf{S}$。它们与柯西应力 $\boldsymbol{\sigma}$ 的关系为 $\mathbf{P} = J\boldsymbol{\sigma}\mathbf{F}^{-T}$ 和 $\mathbf{S} = \mathbf{F}^{-1}\mathbf{P} = J\mathbf{F}^{-1}\boldsymbol{\sigma}\mathbf{F}^{-T}$，其中 $J=\det\mathbf{F}$。这些不同的应力张量在功率平衡原理中与不同的[应变率](@entry_id:154778)度量是**[功共轭](@entry_id:194957)** (work-conjugate) 的。具体来说，单位体积的[功率密度](@entry_id:194407)可以表示为：
-   在当前构型中：$\mathcal{W} = \boldsymbol{\sigma} : \mathbf{d}$，其中 $\mathbf{d}$ 是变形率张量（速度梯度的对称部分）。
-   在参考构型中：$\mathcal{W}_0 = \mathbf{P} : \dot{\mathbf{F}}$，其中 $\dot{\mathbf{F}}$ 是变形梯度的[物质时间导数](@entry_id:190892)。
-   在参考构型中：$\mathcal{W}_0 = \mathbf{S} : \dot{\mathbf{E}}$，其中 $\dot{\mathbf{E}}$ 是[格林-拉格朗日应变张量](@entry_id:187745)的[物质时间导数](@entry_id:190892)。

这些[功共轭](@entry_id:194957)关系是建立[大变形](@entry_id:167243)本构模型的理论基础。[@problem_id:2525704]

### 线性弹性：本构关系

本构关系描述了材料的力学响应，即应力与应变之间的关系。对于在小变形范围内表现出线性、可逆行为的弹性材料，其[本构关系](@entry_id:186508)是线性的，被称为**[广义胡克定律](@entry_id:203555)** (generalized Hooke's Law)。

#### [热力学](@entry_id:141121)基础与[刚度张量](@entry_id:176588)

对于弹性材料，其变形过程是可逆的，我们可以定义一个**[应变能密度函数](@entry_id:755490)** (strain energy density) $W$，它是一个仅与应变状态有关的标量函数。对于一个**[超弹性材料](@entry_id:190241)** (hyperelastic material)，[应力张量](@entry_id:148973)可以由[应变能密度](@entry_id:200085)对[应变张量](@entry_id:193332)的导数得到：

$$
\sigma_{ij} = \frac{\partial W}{\partial \varepsilon_{ij}}
$$

对于[线性弹性](@entry_id:166983)材料，[应变能密度](@entry_id:200085)是应变的二次型：

$$
W = \frac{1}{2} C_{ijkl} \varepsilon_{ij} \varepsilon_{kl}
$$

其中 $C_{ijkl}$ 是四阶**[刚度张量](@entry_id:176588)** (stiffness tensor)，也称为[弹性张量](@entry_id:170728)。[@problem_id:2525682] 将这个能量函数代入应力定义，我们得到线性的[应力-应变关系](@entry_id:274093)：$\sigma_{ij} = C_{ijkl}\varepsilon_{kl}$。

[刚度张量](@entry_id:176588) $C_{ijkl}$ 具有重要的对称性。由于[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ 和应变张量 $\boldsymbol{\epsilon}$ 都是对称的，[刚度张量](@entry_id:176588)具有**次对称性** (minor symmetries)：$C_{ijkl} = C_{jikl} = C_{ijlk}$。更重要的是，由于应力可以从一个标量势函数 $W$ 导出，根据[克莱罗定理](@entry_id:139814)（[混合偏导数的对称性](@entry_id:146941)），[刚度张量](@entry_id:176588)还必须具有**主对称性** (major symmetry)：$C_{ijkl} = C_{klij}$。[@problem_id:2525665] [@problem_id:2525682] 这些对称性将一个[四阶张量](@entry_id:181350) $3^4=81$ 个独立分量减少到最多 $21$ 个。

材料的力学稳定性要求，在无应力参考状态下，[应变能密度](@entry_id:200085)必须是一个严格的极小值。这意味着对于任何非零的应变状态 $\boldsymbol{\epsilon}$，[应变能](@entry_id:162699) $W$ 必须为正。这要求[刚度张量](@entry_id:176588) $\mathbf{C}$ 必须是**正定**的。[@problem_id:2525682] [@problem_id:2525665]

#### [各向同性弹性](@entry_id:203237)

对于[各向同性材料](@entry_id:170678)，其力学性质在所有方向上都是相同的。这意味着其[刚度张量](@entry_id:176588)在任何[坐标旋转](@entry_id:164444)下都保持不变。这种高度的对称性使得 $21$ 个[独立弹性常数](@entry_id:203649)减少到只有 $2$ 个。其[本构关系](@entry_id:186508)通常用**拉梅参数** (Lamé parameters) $\lambda$ 和 $\mu$ 表示：

$$
\boldsymbol{\sigma} = \lambda \text{tr}(\boldsymbol{\epsilon})\mathbf{I} + 2\mu\boldsymbol{\epsilon}
$$

参数 $\mu$ 就是**[剪切模量](@entry_id:167228)** (shear modulus) $G$。在工程中，更常用的弹性常数组合是**杨氏模量** (Young's modulus) $E$ 和**泊松比** (Poisson's ratio) $\nu$。另一组常用的是**体积模量** (bulk modulus) $K$ 和剪切模量 $G$。这三组参数 ($(\lambda, \mu)$，$(E, \nu)$，$(K, G)$) 都是等价的，并且可以相互转换。例如，一些重要的转换关系如下：[@problem_id:2525718]

$$
K = \lambda + \frac{2}{3}\mu \quad ; \quad E = \frac{\mu(3\lambda + 2\mu)}{\lambda + \mu} \quad ; \quad \nu = \frac{\lambda}{2(\lambda + \mu)}
$$

$$
E = \frac{9KG}{3K+G} \quad ; \quad \nu = \frac{3K-2G}{2(3K+G)}
$$

这些关系式可以通过考虑[单轴拉伸](@entry_id:188287)、纯剪切和[静水压力](@entry_id:275365)等简单载荷情况下的材料响应来推导。

#### [各向异性弹性](@entry_id:186771)与[晶体对称性](@entry_id:198772)

对于晶体材料，其原子[排列](@entry_id:136432)具有特定的周期性和对称性，导致其力学性质通常是各向异性的。为了方便表示，我们通常使用**[Voigt表示法](@entry_id:166691)** (Voigt notation)，将对称的[应力张量和应变张量](@entry_id:755512)写成 $6 \times 1$ 的矢量形式，而四阶[刚度张量](@entry_id:176588) $C_{ijkl}$ 则被写成一个 $6 \times 6$ 的[对称矩阵](@entry_id:143130) $C_{\alpha\beta}$。[@problem_id:2525665]

根据**[诺伊曼原理](@entry_id:136408)** (Neumann's Principle)，材料任何物理性质的对称性必须包含其晶体点[群的对称性](@entry_id:136707)元素。[@problem_id:2525731] 这意味着[弹性刚度张量](@entry_id:170728)必须在晶体所属[点群](@entry_id:142456)的所有对称操作（如旋转、反映）下保持不变。这个原理极大地减少了[独立弹性常数](@entry_id:203649)的数量。例如：
-   **正交晶系** (Orthorhombic)：具有三个相互垂直的二重旋转轴，[独立弹性常数](@entry_id:203649)为 $9$ 个。
-   **六方晶系** (Hexagonal)：具有一个六重或三重旋转轴，在垂直于该轴的基面内是各向同性的，[独立弹性常数](@entry_id:203649)为 $5$ 个。
-   **立方[晶系](@entry_id:137271)** (Cubic)：具有比正交晶系更高的对称性，如$\langle 111 \rangle$方向的三重轴，[独立弹性常数](@entry_id:203649)减少到 $3$ 个 ($C_{11}, C_{12}, C_{44}$)。

[各向同性材料](@entry_id:170678)可以看作是立方晶系的一个特例，它满足额外的关系 $C_{11}-C_{12}=2C_{44}$，从而将独立常数从 $3$ 个减少到 $2$ 个。

### 高级议题与扩展

#### [应变协调性](@entry_id:199659)

我们已经知道如何从[位移场](@entry_id:141476)计算应变场。但反过来的问题是：给定一个应变场 $\boldsymbol{\epsilon}(\mathbf{x})$，它是否总是对应于一个真实、连续、单值的位移场？答案是否定的。

一个给定的应变场要想成为一个有效的（即“相容的”）应变场，它的六个分量不能是完全独立的函数，它们必须满足一定的[微分](@entry_id:158718)约束条件。这些条件被称为**[圣维南协调方程](@entry_id:754487)** (Saint-Venant compatibility equations)。其张量形式为：[@problem_id:2525699]

$$
\varepsilon_{ij,kl} + \varepsilon_{kl,ij} - \varepsilon_{ik,jl} - \varepsilon_{jl,ik} = 0
$$

该[方程组](@entry_id:193238)对于所有 $i,j,k,l$ 都成立。可以证明，在一个单连通的区域内，这组方程是应变场能够积分得到一个单值[位移场](@entry_id:141476)的充要条件。从物理上看，协调方程保证了当我们将应变场在整个物体上积分时，不会出现几何上的不自洽，如材料的撕裂或重叠。当材料中存在[位错](@entry_id:157482)等[晶体缺陷](@entry_id:267016)时，它们会产生一个不满足协调方程的应变场。

#### [本征应变](@entry_id:198120)

除了力学加载，其他物理过程也能引起材料的变形。这些非力学因素导致的应力自由变形被称为**[本征应变](@entry_id:198120)** (eigenstrain) 或固有应变。在这种情况下，总应变 $\boldsymbol{\epsilon}$ 可以分解为产生应力的**[弹性应变](@entry_id:189634)** $\boldsymbol{\epsilon}^{\text{el}}$ 和不产生应力的[本征应变](@entry_id:198120) $\boldsymbol{\epsilon}^{\text{eigen}}$：

$$
\boldsymbol{\epsilon} = \boldsymbol{\epsilon}^{\text{el}} + \boldsymbol{\epsilon}^{\text{eigen}}
$$

应力只由弹性应变产生，因此[本构关系](@entry_id:186508)被修正为：

$$
\boldsymbol{\sigma} = \mathbf{C} : \boldsymbol{\epsilon}^{\text{el}} = \mathbf{C} : (\boldsymbol{\epsilon} - \boldsymbol{\epsilon}^{\text{eigen}})
$$

常见的[本征应变](@entry_id:198120)包括：
-   **[热应变](@entry_id:187744)** ($\boldsymbol{\epsilon}^{\text{th}}$)：由温度变化 $\Delta T$ 引起，$\epsilon^{\text{th}}_{ij} = \alpha_{ij} \Delta T$，其中 $\alpha_{ij}$ 是热膨胀系数张量。
-   **[相变](@entry_id:147324)应变**：由材料的[晶体结构](@entry_id:140373)变化引起。
-   **化学应变或成分应变** ($\boldsymbol{\epsilon}^{*}$)：在[固态电化学](@entry_id:194456)（如电池电极）中，离子的嵌入或脱出会引起[晶格](@entry_id:196752)的膨胀或收缩。

这个框架的理论基础是，[亥姆霍兹自由能](@entry_id:136442)是弹性应变的函数，而非总应变。因此，应力作为自由能对应变的导数，自然地与[弹性应变](@entry_id:189634)联系在一起。[@problem_id:2525674]

通过本章的学习，我们建立了一个从基本原理出发，能够描述和预测材料在各种条件下力学行为的综合框架。这个框架不仅是[材料科学](@entry_id:152226)和固体力学研究的基石，也是设计和分析先进材料与器件不可或缺的工具。