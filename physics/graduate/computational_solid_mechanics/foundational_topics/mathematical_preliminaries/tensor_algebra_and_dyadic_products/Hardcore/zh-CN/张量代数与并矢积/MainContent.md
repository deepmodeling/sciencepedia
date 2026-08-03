## 引言
张量是描述物理定律的普适语言，它们以不依赖于特定坐标系的方式捕捉了方向性信息。从描述材料变形的连续介质力学，到描述时空弯曲的广义相对论，张量无处不在。其中，二阶张量及其代数是理解众多物理现象的基础，而并矢积作为构建二阶张量的基本单元，为我们提供了理解其几何与物理本质的强大工具。然而，许多工程师和科学家在实践中常常将张量仅仅视为一个分量矩阵，忽略了其作为线性映射的深刻内涵，这限制了他们对复杂物理现象的建模与分析能力。

本文旨在填补理论与应用之间的这一鸿沟。我们将系统地揭示张量作为多重线性映射的本质，并阐明并矢积在其中扮演的“基本构造块”角色。通过本文的学习，您将不再仅仅“计算”张量，而是能够“理解”张量。

本文将分为三个核心章节展开。在第一章“原理与机制”中，我们将奠定坚实的数学基础，详细探讨并矢积的定义、性质，以及它如何用于构建单位张量和实现关键的张量分解。随后，在第二章“应用与交叉学科联系”中，我们将展示这些抽象原理如何在连续介质力学、本构建模、多尺度分析和断裂力学等实际问题中发挥威力。最后，在第三章“动手实践”中，您将通过一系列精心设计的练习，将理论知识转化为解决实际问题的能力。让我们从深入张量代数的核心——其原理与机制——开始我们的探索之旅。

## 原理与机制

在深入研究计算固体力学的数值方法之前，我们必须首先建立一个坚实的数学基础。本章旨在系统地阐述张量代数的核心原理与机制，特别是并矢积（dyadic product）在构建和理解张量中的关键作用。张量不仅是描述物理量（如应力、应变）的数学工具，其内在的代数结构也深刻地反映了连续介质运动和变形的几何与物理本质。

### 张量作为线性映射与并矢积

在最根本的层面上，一个二阶张量 **A** 是一个作用于三维欧几里得向量空间 $\mathbb{R}^3$ 的线性映射。这意味着它将一个向量 **v** 转换为另一个向量 **u**，即 **u** = **A** · **v**，并且这种映射满足线性关系：$\boldsymbol{A} \cdot (\alpha\boldsymbol{v} + \beta\boldsymbol{w}) = \alpha(\boldsymbol{A} \cdot \boldsymbol{v}) + \beta(\boldsymbol{A} \cdot \boldsymbol{w})$。

尽管二阶张量可以被视为一个 $3 \times 3$ 的矩阵，但将其理解为由更基本的元素——向量——构建而成，会带来更深刻的洞察。这个基本的构造工具就是 **并矢积**（dyadic product）或称外积（outer product）。给定两个向量 **u** 和 **v**，它们的并矢积，记作 $\boldsymbol{u} \otimes \boldsymbol{v}$，本身就是一个二阶张量。其定义通过它对任意向量 **w** 的作用来给出 [@problem_id:3604549]：

$$ (\boldsymbol{u} \otimes \boldsymbol{v}) \boldsymbol{w} = \boldsymbol{u} (\boldsymbol{v} \cdot \boldsymbol{w}) $$

这里，$(\boldsymbol{v} \cdot \boldsymbol{w})$ 是一个标量（向量的内积），它缩放向量 **u**。因此，张量 $\boldsymbol{u} \otimes \boldsymbol{v}$ 将任何向量 **w** 映射到向量 **u** 的方向上。如果 **u** 和 **v** 都非零，那么这个映射的像（range）就是由 **u** 张成的一维子空间，因此 $\boldsymbol{u} \otimes \boldsymbol{v}$ 是一个 **秩为1**（rank-one）的张量。它的行列式在三维空间中恒为零 [@problem_id:3604549]。

在任意一个标准正交基 $\{\boldsymbol{e}_1, \boldsymbol{e}_2, \boldsymbol{e}_3\}$ 中，向量 **u** 和 **v** 可以表示为 $\boldsymbol{u} = u_i \boldsymbol{e}_i$ 和 $\boldsymbol{v} = v_j \boldsymbol{e}_j$ (此处及后续将默认使用爱因斯坦求和约定，即重复指标表示求和)。并矢积 $\boldsymbol{u} \otimes \boldsymbol{v}$ 的分量形式为：

$$ (\boldsymbol{u} \otimes \boldsymbol{v})_{ij} = u_i v_j $$

这与向量内积 $\boldsymbol{u} \cdot \boldsymbol{v} = u_i v_i$ 形成了鲜明的对比。内积将两个向量映射为一个标量，而并矢积则生成一个二阶张量。

并矢积的一些基本性质对于后续的推导至关重要：
- **非交换性**：通常情况下，$\boldsymbol{u} \otimes \boldsymbol{v} \neq \boldsymbol{v} \otimes \boldsymbol{u}$。
- **转置**：并矢积的转置是交换两个向量的顺序：$(\boldsymbol{u} \otimes \boldsymbol{v})^{\mathsf{T}} = \boldsymbol{v} \otimes \boldsymbol{u}$。因此，一个并矢积是**对称**的，当且仅当两个向量是共线的 [@problem_id:3604549]。
- **迹**：并矢积的迹等于其构成向量的内积：$\operatorname{tr}(\boldsymbol{u} \otimes \boldsymbol{v}) = u_i v_i = \boldsymbol{u} \cdot \boldsymbol{v}$ [@problem_id:3604549]。
- **复合**：两个秩为1的张量的复合（或矩阵乘法）遵循一个简单的法则：$(\boldsymbol{u} \otimes \boldsymbol{v})(\boldsymbol{a} \otimes \boldsymbol{b}) = (\boldsymbol{v} \cdot \boldsymbol{a}) \boldsymbol{u} \otimes \boldsymbol{b}$ [@problem_id:3604549]。

### 单位张量与指标符号

在张量代数中，**单位张量** **I** 扮演着如同标量代数中“1”的角色。它是一个特殊的二阶张量，其作用于任何向量都保持该向量不变：$\boldsymbol{I} \boldsymbol{v} = \boldsymbol{v}$。

在标准正交基 $\{\boldsymbol{e}_i\}$ 中，单位张量的分量由 **克罗内克δ**（Kronecker delta）符号 $\delta_{ij}$ 给出 [@problem_id:3604616]：
$$ I_{ij} = \delta_{ij} $$
其中，$\delta_{ij} = 1$ 当 $i = j$ 时，$\delta_{ij} = 0$ 当 $i \neq j$ 时。这个定义源于基向量的正交性 $\boldsymbol{e}_i \cdot \boldsymbol{e}_j = \delta_{ij}$。

利用并矢积，单位张量有一个非常优雅和强大的表示形式：
$$ \boldsymbol{I} = \sum_{i=1}^3 \boldsymbol{e}_i \otimes \boldsymbol{e}_i = \boldsymbol{e}_i \otimes \boldsymbol{e}_i $$
我们可以通过它对任意向量 $\boldsymbol{v} = v_j \boldsymbol{e}_j$ 的作用来验证这一点：
$$ (\boldsymbol{e}_i \otimes \boldsymbol{e}_i) \boldsymbol{v} = (\boldsymbol{e}_i \otimes \boldsymbol{e}_i) (v_j \boldsymbol{e}_j) = v_j (\boldsymbol{e}_i (\boldsymbol{e}_i \cdot \boldsymbol{e}_j)) = v_j (\boldsymbol{e}_i \delta_{ij}) = v_i \boldsymbol{e}_i = \boldsymbol{v} $$
这个并矢表示不仅揭示了单位张量的内在结构，也是进行复杂张量运算的有力工具。例如，任何二阶张量 **A** 都可以用其分量 $A_{ij}$ 和基并矢积表示为 $\boldsymbol{A} = A_{ij} \boldsymbol{e}_i \otimes \boldsymbol{e}_j$。

### 张量积与内积

为了量化张量的大小和它们之间的“角度”，我们需要定义一个内积。对于二阶张量空间，最常用的内积是 **弗罗贝尼乌斯内积**（Frobenius inner product），也称为双点积（double dot product）或双重缩并（double contraction），记作 $\boldsymbol{A}:\boldsymbol{B}$。其定义为 [@problem_id:3604590]：

$$ \boldsymbol{A}:\boldsymbol{B} = \operatorname{tr}(\boldsymbol{A}^{\mathsf{T}} \boldsymbol{B}) = A_{ij} B_{ij} $$

这个内积赋予了二阶张量空间以欧几里得结构。它满足内积的所有性质：双线性、对称性（$\boldsymbol{A}:\boldsymbol{B} = \boldsymbol{B}:\boldsymbol{A}$）和正定性（$\boldsymbol{A}:\boldsymbol{A} \ge 0$，且等号成立当且仅当 $\boldsymbol{A}=\boldsymbol{0}$）。由这个内积可以诱导出弗罗贝尼乌斯范数 $\|\boldsymbol{A}\| = \sqrt{\boldsymbol{A}:\boldsymbol{A}}$，它衡量了张量“大小”。

对于由并矢积构成的张量，这个内积有一个简单的结果 [@problem_id:3604590]：
$$ (\boldsymbol{a} \otimes \boldsymbol{b}) : (\boldsymbol{c} \otimes \boldsymbol{d}) = (a_i c_i)(b_j d_j) = (\boldsymbol{a} \cdot \boldsymbol{c})(\boldsymbol{b} \cdot \boldsymbol{d}) $$
这个性质在构建和分析四阶张量时尤其有用。

在固体力学中，我们经常遇到四阶张量，例如弹性张量，它将一个二阶张量（应变）映射到另一个二阶张量（应力）。我们可以通过二阶张量的并矢积来构建四阶张量。例如，给定二阶张量 **A** 和 **B**，可以定义一个四阶张量 $\mathbb{C} = \boldsymbol{A} \otimes \boldsymbol{B}$，其分量为 $C_{ijkl} = A_{ij} B_{kl}$。它对任意二阶张量 **X** 的作用（通过双重缩并）为 [@problem_id:3604559]：

$$ \mathbb{C}:\boldsymbol{X} = (\boldsymbol{A} \otimes \boldsymbol{B}):\boldsymbol{X} = (B_{kl} X_{kl}) \boldsymbol{A} = (\boldsymbol{B}:\boldsymbol{X}) \boldsymbol{A} $$

这个运算是构建本构关系（constitutive relations）的基础。例如，各向同性投影算子就是基于这种构造。

### 张量的分解

复杂的问题往往可以通过将其分解为更简单、更易于理解的部分来解决。张量代数提供了一套强大的分解工具，每一种分解都对应着一种深刻的物理或几何解释。

#### 对称与反对称分解

任何二阶张量 **A** 都可以唯一地分解为一个 **对称** 部分和一个 **反对称**（或称斜对称、skew-symmetric）部分的和 [@problem_id:3604614]：

$$ \boldsymbol{A} = \operatorname{sym}(\boldsymbol{A}) + \operatorname{skw}(\boldsymbol{A}) $$

其中，
$$ \operatorname{sym}(\boldsymbol{A}) = \frac{1}{2}(\boldsymbol{A} + \boldsymbol{A}^{\mathsf{T}}) $$
$$ \operatorname{skw}(\boldsymbol{A}) = \frac{1}{2}(\boldsymbol{A} - \boldsymbol{A}^{\mathsf{T}}) $$

这种分解在连续介质运动学中至关重要。考虑一个点的邻域内的速度场，其梯度 $\boldsymbol{L} = \nabla\boldsymbol{v}$ 是一个二阶张量。**L** 的对称部分 $\boldsymbol{D} = \operatorname{sym}(\boldsymbol{L})$ 被称为 **变形率张量**（rate-of-deformation tensor），它描述了材料微元的拉伸和剪切变形速率。反对称部分 $\boldsymbol{W} = \operatorname{skw}(\boldsymbol{L})$ 被称为 **自旋张量**（spin tensor），它描述了材料微元的刚性转动速率。

这种物理解释的数学基础是：只有对称部分 **D** 会导致材料线元长度的改变。考虑一个随材料运动的线元 **r**，其长度平方的变化率为：
$$ \frac{\mathrm{d}}{\mathrm{d}t}\|\boldsymbol{r}\|^2 = 2 \boldsymbol{r} \cdot \dot{\boldsymbol{r}} = 2 \boldsymbol{r} \cdot (\boldsymbol{L}\boldsymbol{r}) = 2 \boldsymbol{r} \cdot ((\boldsymbol{D}+\boldsymbol{W})\boldsymbol{r}) = 2 \boldsymbol{r} \cdot (\boldsymbol{D}\boldsymbol{r}) $$
由于一个反对称张量 **W** 的二次型恒为零（即 $\boldsymbol{r} \cdot (\boldsymbol{W}\boldsymbol{r}) = 0$），长度变化率完全由对称部分 **D** 决定。在三维空间中，任何反对称张量 **W** 的作用都可以表示为一个向量叉乘，即存在一个 **轴矢** $\boldsymbol{\omega}$ 使得 $\boldsymbol{W}\boldsymbol{x} = \boldsymbol{\omega} \times \boldsymbol{x}$，其中 $\boldsymbol{\omega}$ 就是该点的刚体角速度矢量 [@problem_id:3604614]。

此外，对称张量空间和反对称张量空间在弗罗贝尼乌斯内积下是**正交**的。也就是说，对于任何对称张量 **S** 和反对称张量 **W**，它们的内积 $\boldsymbol{S}:\boldsymbol{W} = 0$。这一性质有着重要的物理后果。例如，对于一个具有对称柯西应力张量 $\boldsymbol{\sigma}$ 的材料，应力功率（单位体积的内力功）仅取决于变形率张量，而与自旋无关：
$$ \dot{w} = \boldsymbol{\sigma}:\boldsymbol{L} = \boldsymbol{\sigma}:(\boldsymbol{D} + \boldsymbol{W}) = \boldsymbol{\sigma}:\boldsymbol{D} $$

#### 球形与偏斜分解

另一种极其有用的分解是将张量 **A** 分解为 **球形**（spherical）部分和 **偏斜**（deviatoric）部分 [@problem_id:3604613]：

$$ \boldsymbol{A} = \boldsymbol{A}^{\text{sph}} + \boldsymbol{A}' $$

其中，
$$ \boldsymbol{A}^{\text{sph}} = \frac{1}{3}(\operatorname{tr}\boldsymbol{A})\boldsymbol{I} $$
$$ \boldsymbol{A}' = \boldsymbol{A} - \boldsymbol{A}^{\text{sph}} = \boldsymbol{A} - \frac{1}{3}(\operatorname{tr}\boldsymbol{A})\boldsymbol{I} $$

球形部分是一个各向同性的张量（与单位张量成比例），它代表了张量的“平均”或“静水”效应。偏斜部分则捕获了张量的所有非各向同性（即“剪切”或“畸变”）效应。一个关键性质是偏斜张量的迹恒为零：$\operatorname{tr}(\boldsymbol{A}') = 0$。

在物理上，这种分解用于分离体积变化和形状变化。对于小应变张量 $\boldsymbol{\varepsilon}$，其迹 $\operatorname{tr}(\boldsymbol{\varepsilon})$ 代表了体积应变。因此，球形应变张量 $\boldsymbol{\varepsilon}^{\text{sph}}$ 描述了纯粹的体积变化（膨胀或收缩），而偏斜应变张量 $\boldsymbol{\varepsilon}'$ 描述了保持体积不变的形状畸变。

与对称/反对称分解类似，球形张量空间和偏斜张量空间在弗罗贝尼乌斯内积下也是**正交**的，即 $\boldsymbol{A}^{\text{sph}}:\boldsymbol{A}' = 0$ [@problem_id:3604613]。这使得能量或功率可以被干净地分解为体积部分和偏斜部分。例如，在线性弹性中，应变能密度可以分解为体积应变能和畸变能之和。对于纯静水应力状态 $\boldsymbol{\sigma} = -p\boldsymbol{I}$（其中 $p$ 是压力），应力是纯球形的（其偏斜部分为零），因此它只对变形的体积部分做功，而不对形状畸变做功 [@problem_id:3604613]。

这种分解也可以通过四阶 **投影张量** 来实现。球形投影算子可定义为 $\boldsymbol{P}_{\text{sph}} = \frac{1}{3} \boldsymbol{I} \otimes \boldsymbol{I}$，其作用于 **A** 得到 $\boldsymbol{P}_{\text{sph}}:\boldsymbol{A} = \boldsymbol{A}^{\text{sph}}$。相应的，偏斜投影算子为 $\boldsymbol{P}_{\text{dev}} = \boldsymbol{I}_4 - \boldsymbol{P}_{\text{sph}}$，其中 $\boldsymbol{I}_4$ 是四阶单位张量 [@problem_id:3604613]。

#### 谱分解

对于 **对称** 的二阶张量 **A**，**谱定理**（Spectral Theorem）保证了其存在一种极为重要的分解形式，称为 **谱分解**（spectral decomposition）[@problem_id:3604622]：

$$ \boldsymbol{A} = \sum_{i=1}^{3} \lambda_{i} \boldsymbol{n}_{i} \otimes \boldsymbol{n}_{i} $$

这里，$\{\lambda_1, \lambda_2, \lambda_3\}$ 是 **A** 的三个实数 **特征值**（eigenvalues），而 $\{ \boldsymbol{n}_1, \boldsymbol{n}_2, \boldsymbol{n}_3\}$ 是一组与之对应的相互正交的单位 **特征向量**（eigenvectors）。这些特征向量构成了空间的一个标准正交基，被称为 **主方向**（principal directions）。

谱分解的几何意义是，任何对称张量的作用都可以被看作是在其三个主方向上进行独立的拉伸或压缩（由特征值 $\lambda_i$ 决定）。

- **存在性与唯一性**：对于任何实对称二阶张量，谱分解总是存在的。特征值的多重集是唯一的。
  - 如果三个特征值互不相同，那么对应的三个主方向（特征向量）除了符号（$\pm \boldsymbol{n}_i$）和排列顺序外是唯一的。因此，每个投影算子 $\boldsymbol{n}_i \otimes \boldsymbol{n}_i$ 都是唯一的。
  - 如果有两个或三个特征值相同（特征值退化），对应的特征向量就不唯一了。例如，如果 $\lambda_1 = \lambda_2 \neq \lambda_3$，那么任何在由 $\boldsymbol{n}_1$ 和 $\boldsymbol{n}_2$ 张成的平面内的单位向量都是特征值为 $\lambda_1$ 的特征向量。尽管单个的特征向量不唯一，但**投向该特征空间的投影算子**是唯一的。在此例中，投影算子 $\boldsymbol{P}^{(1)} = \boldsymbol{n}_1 \otimes \boldsymbol{n}_1 + \boldsymbol{n}_2 \otimes \boldsymbol{n}_2$ 是唯一的。因此，更严谨的唯一分解形式是 $\boldsymbol{A} = \sum_k \lambda^{(k)} \boldsymbol{P}^{(k)}$，其中 $\lambda^{(k)}$ 是互不相同的特征值，$\boldsymbol{P}^{(k)}$ 是投向对应特征空间的投影算子 [@problem_id:3604622]。

一个简单的例子是秩为1的投影张量 $\boldsymbol{P} = \boldsymbol{n} \otimes \boldsymbol{n}$，其中 **n** 是单位向量。它本身就是其谱分解的形式，其特征值为1（对应特征向量 **n**）和0（对应所有与 **n** 正交的向量）。这个张量满足 $\boldsymbol{P}^2 = \boldsymbol{P}$ 和 $\boldsymbol{P}^{\mathsf{T}} = \boldsymbol{P}$，是正交投影算子的典型代表 [@problem_id:3604566]。

### 在连续介质力学中的应用

张量代数的这些原理是描述和求解连续介质力学问题的基石。

#### 柯西应力张量

在连续体内部的任何一点，作用在穿过该点的一个假想微小平面上的力（称为 **面力** traction, **t**）取决于该平面的法向 **n**。**柯西应力定理**（Cauchy's Stress Theorem）指出，这种依赖关系是线性的。这意味着存在一个二阶张量 $\boldsymbol{\sigma}$，称为 **柯西应力张量**，使得 [@problem_id:3604591]：

$$ \boldsymbol{t}(\boldsymbol{n}) = \boldsymbol{\sigma} \boldsymbol{n} $$

这个基本关系可以通过对一个无限小的四面体进行动量平衡分析而导出。这个推导过程本身就揭示了 $\boldsymbol{\sigma}$ 的并矢表示：$\boldsymbol{\sigma} = \sum_{i=1}^3 \boldsymbol{t}(\boldsymbol{e}_i) \otimes \boldsymbol{e}_i$，其中 $\boldsymbol{t}(\boldsymbol{e}_i)$ 是作用在法向为 $\boldsymbol{e}_i$ 的面上的面力向量。值得注意的是，$\boldsymbol{\sigma}$ 的存在性仅依赖于线性动量守恒，而其**对称性** ($\boldsymbol{\sigma} = \boldsymbol{\sigma}^{\mathsf{T}}$) 则是由角动量守恒导出的（在无体力矩和体偶应力的情况下）[@problem_id:3604591]。

#### 极分解

对于大变形问题，**变形梯度张量** **F** 描述了从参考构形到当前构形的局部变形。**F** 本身通常不是对称的，因为它既包含拉伸也包含转动。**极分解定理**（Polar Decomposition Theorem）提供了一种精确分离这两种效应的方法 [@problem_id:3604598]：

$$ \boldsymbol{F} = \boldsymbol{R}\boldsymbol{U} = \boldsymbol{V}\boldsymbol{R} $$

这里，**F** 被唯一地分解为一个**转动张量** **R**（一个满足 $\boldsymbol{R}^{\mathsf{T}}\boldsymbol{R}=\boldsymbol{I}$ 和 $\det\boldsymbol{R}=1$ 的正常正交张量）和一个**对称正定**的**拉伸张量**。

- **U** 是 **右拉伸张量**，它作用于参考构形，描述纯粹的材料拉伸。它可以通过 $ \boldsymbol{U} = \sqrt{\boldsymbol{F}^{\mathsf{T}}\boldsymbol{F}} $ 计算得到。$\boldsymbol{F}=\boldsymbol{R}\boldsymbol{U}$ 的物理解释是：变形首先在参考构形中进行纯拉伸（**U**），然后再进行刚体转动（**R**）。
- **V** 是 **左拉伸张量**，它作用于当前构形，描述纯粹的空间拉伸。它可以通过 $ \boldsymbol{V} = \sqrt{\boldsymbol{F}\boldsymbol{F}^{\mathsf{T}}} $ 计算得到。$\boldsymbol{F}=\boldsymbol{V}\boldsymbol{R}$ 的物理解释是：变形首先进行刚体转动（**R**），然后在当前构形中进行纯拉伸（**V**）。
- 两个拉伸张量通过转动相关联：$\boldsymbol{V} = \boldsymbol{R}\boldsymbol{U}\boldsymbol{R}^{\mathsf{T}}$。它们的特征值相同（称为**主伸长**），但主方向（特征向量）不同，主方向之间也通过 **R** 相互关联。

#### 张量在不同构形间的转换

在构建本构关系时，通常在材料本身性质不变的参考构形中进行会更方便。这就需要将在当前构形中定义的物理量（如柯西应力 $\boldsymbol{\sigma}$）转换到参考构形中。

这种转换通过 **推前**（push-forward）和 **拉回**（pull-back）操作实现，这些操作由变形梯度 **F** 定义。例如，一个参考构形中的切向量 **V** 被推前到当前构形，得到 $\boldsymbol{v} = \boldsymbol{F}\boldsymbol{V}$。对于作为线性映射的二阶张量 **T**，从参考构形到当前构形的推前操作为 $ \boldsymbol{t} = \boldsymbol{F}\boldsymbol{T}\boldsymbol{F}^{-\mathsf{T}} $ [@problem_id:3604582]。

对于应力张量，其转换关系稍微复杂，因为它还涉及到面积元素的变化（由南森公式 $\boldsymbol{n}\mathrm{d}a = J\boldsymbol{F}^{-\mathsf{T}}\boldsymbol{N}\mathrm{d}A$ 描述，其中 $J = \det\boldsymbol{F}$）。通过力平衡 $\boldsymbol{t}\mathrm{d}a = \boldsymbol{t}_0\mathrm{d}A$，我们可以建立不同应力张量之间的关系。其中，**第二皮奥拉-基尔霍夫应力张量**（Second Piola-Kirchhoff stress tensor, **S**）是一个在参考构形中定义的对称张量，它与柯西应力 $\boldsymbol{\sigma}$ 的关系为 [@problem_id:3604582]：

$$ \boldsymbol{S} = J \boldsymbol{F}^{-1} \boldsymbol{\sigma} \boldsymbol{F}^{-\mathsf{T}} $$

其逆关系为：

$$ \boldsymbol{\sigma} = J^{-1} \boldsymbol{F} \boldsymbol{S} \boldsymbol{F}^{\mathsf{T}} $$

这个转换至关重要，因为它允许我们将物理上在当前构形中测量的应力（$\boldsymbol{\sigma}$）与在参考构形中定义的应变度量（如格林-拉格朗日应变张量）联系起来，从而建立客观的本构模型。

#### 张量分量的坐标变换

最后，张量是一个几何对象，其本身独立于坐标系的选择。然而，它的分量会随着坐标系的改变而改变。如果我们将坐标系从基 $\{\boldsymbol{e}_i\}$ 旋转到基 $\{\boldsymbol{e}'_i\}$，旋转由正交矩阵 **Q** 描述，即 $\boldsymbol{e}'_i = Q_{ij} \boldsymbol{e}_j$，那么一个二阶张量 **A** 在新旧坐标系下的分量 $A'_{ij}$ 和 $A_{kl}$ 满足以下转换法则 [@problem_id:3604604]：

$$ A'_{ij} = Q_{ik} Q_{jl} A_{kl} $$

在矩阵表示中，这等价于：

$$ \boldsymbol{A}' = \boldsymbol{Q} \boldsymbol{A} \boldsymbol{Q}^{\mathsf{T}} $$

理解这个变换法则是区分一个真正的张量和一个普通 $3 \times 3$ 矩阵的关键。张量的物理意义不随观察者（坐标系）的改变而改变，其分量必须遵循特定的变换法则来保持这种不变性。

本章所介绍的原理和机制构成了研究和模拟固体力学行为的通用语言。掌握这些概念，是从简单的一维问题迈向复杂三维、大变形、非线性材料分析的关键一步。