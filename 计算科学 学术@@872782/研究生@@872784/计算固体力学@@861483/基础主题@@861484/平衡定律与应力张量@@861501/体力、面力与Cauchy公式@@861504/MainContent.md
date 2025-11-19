## 引言
在工程与科学领域，理解固体材料如何响应外力是设计、分析和预测其行为的核心。无论是一座桥梁承受的风载与自重，还是人体组织在运动中受到的力，其力学响应都遵循着一套普适的物理定律。这些作用力以两种基本形式出现：穿透物体体积的“体力”和作用于其表面的“面力”。然而，我们如何从这些宏观的外部载荷，深入到物体内部，精确描述任意一点的受力状态呢？这正是[连续介质力学](@entry_id:155125)试图解决的核心问题。本文旨在填补这一知识鸿沟，系统性地建立外部载荷与内部应力之间的数学和物理联系。

本文将分为三个章节，引导您完成一次从基本原理到前沿应用的探索之旅。在“原理与机制”一章中，我们将从第一性原理出发，严格定义体力与面力，并推导出连续介质力学中最强大的工具之一——柯西公式，它揭示了内部应力张量的存在与意义。接着，我们将探讨动量守恒如何转化为控制应[力场](@entry_id:147325)[分布](@entry_id:182848)的平衡方程。在“应用与跨学科联系”一章中，我们将展示这些理论如何在[计算力学](@entry_id:174464)、[多物理场耦合](@entry_id:171389)、工程设计乃至生物力学等不同领域中发挥关键作用。最后，通过“动手实践”部分，您将有机会应用所学知识解决具体的力学问题，从而巩固和深化您的理解。

现在，让我们从最基本的概念开始，深入探索连续介质受力的两种基本模式。

## 原理与机制

在[连续介质力学](@entry_id:155125)中，理解物体如何响应外部载荷是核心任务。这些载荷通过两种基本方式作用于连续体：**体力**和**面力**。本章旨在从第一性原理出发，系统地阐述这些力的概念，并推导它们与物体内部应力状态之间的基本关系。我们将建立[连续介质力学](@entry_id:155125)中的核心方程，并探讨这些原理在计算力学中的深刻应用。

### 体力与面力：连续体受力的两种模式

作用于一个连续体上的力可以分为两类。第一类是**体力** (body forces)，它作用于物体的每一个质点，其大小与体积成正比。典型的例子是重力，它作用于物体内部的每一个质量微元。[体力](@entry_id:174230)通常用一个矢量场 $\boldsymbol{b}(\boldsymbol{x})$ 来描述，称为**体力密度** (body force density)，其单位是力每单位体积（[国际单位制](@entry_id:172547)中为 $\mathrm{N/m^3}$）。

第二类是**面力** (surface forces)，它通过直接接触作用于物体的表面。这些力[分布](@entry_id:182848)在表面上，其大小与作用面积成正比。例如，[静水压力](@entry_id:275365)或两个物体接触面上的[摩擦力](@entry_id:171772)。描述面力的物理量是**[面力矢量](@entry_id:189429)** (surface traction) 或简称**牵[引力](@entry_id:175476)** (traction)，记为 $\boldsymbol{t}$。它被定义为作用在某个表面微元上的力除以该微元的面积，因此其单位是力每单位面积（[国际单位制](@entry_id:172547)中为 $\mathrm{N/m^2}$，即帕斯卡，$\mathrm{Pa}$）。

一个关键的洞见是，牵[引力](@entry_id:175476)不仅依赖于其作用点 $\boldsymbol{x}$，还依赖于其作用表面的方位。一个通过点 $\boldsymbol{x}$ 的无限多个假想平面，每个平面都有不同的法向，其上作用的牵[引力](@entry_id:175476)也可能不同。因此，我们必须将牵[引力](@entry_id:175476)写成 $\boldsymbol{t}(\boldsymbol{x}, \boldsymbol{n})$，其中 $\boldsymbol{n}$ 是该点处表面的单位外法向矢量。根据牛顿第三定律（作用力与[反作用](@entry_id:203910)力定律），作用在同一表面但法向相反的两个牵[引力](@entry_id:175476)大小相等、方向相反，即 $\boldsymbol{t}(\boldsymbol{x}, -\boldsymbol{n}) = -\boldsymbol{t}(\boldsymbol{x}, \boldsymbol{n})$。

这两个力学量在[计算力学](@entry_id:174464)的[变分形式](@entry_id:166033)中扮演着核心角色。例如，在[虚功原理](@entry_id:138749)或[虚功](@entry_id:176403)率原理中，体力 $\boldsymbol{b}$ 和面力 $\boldsymbol{t}$ 对一个虚速度场 $\boldsymbol{v}$ 所做的功率分别为[体积分](@entry_id:171119)和[面积分](@entry_id:275394)的形式：
$$ P_{body} = \int_{\Omega} \boldsymbol{b} \cdot \boldsymbol{v} \, d\Omega $$
$$ P_{surface} = \int_{\partial\Omega} \boldsymbol{t} \cdot \boldsymbol{v} \, dS $$
其中 $\Omega$ 是物体占据的区域，$\partial\Omega$ 是其边界。这两个积分项都具有功率的量纲，它们构成了有限元方法中[载荷向量](@entry_id:635284)的基础 [@problem_id:3547598]。

### 柯西应力原理与柯西公式

虽然面力的概念直观，但它描述的是物体表面（真实的或假想的）上的力。我们如何描述物体内部的受力状态呢？这引出了连续介质力学中最核心的概念之一：**应力** (stress)。

法国数学家奥古斯丁-路易·柯西 (Augustin-Louis Cauchy) 提出了一个革命性的思想：在连续体内部的任意一点 $\boldsymbol{x}$，通过该点的任意一个假想平面，该平面一侧的物质会对另一侧的物质施加一个[分布](@entry_id:182848)力。这个[分布](@entry_id:182848)力的密度就是该平面上的牵[引力](@entry_id:175476) $\boldsymbol{t}(\boldsymbol{x}, \boldsymbol{n})$。这便是**柯西应力原理** (Cauchy's Stress Principle)。

然而，一个点可以有无限多个通过它的平面，难道我们需要无限多的信息才能描述该点的受力状态吗？柯西的下一个伟大贡献——**柯西应力定理** (Cauchy's Stress Theorem)——给出了一个否定的答案。该定理指出，在任意一点 $\boldsymbol{x}$，牵[引力](@entry_id:175476)矢量 $\boldsymbol{t}$ 与该平面的单位法向矢量 $\boldsymbol{n}$ 之间存在一个**线性关系**。

这个线性关系可以通过一个著名的思想实验——“柯西四面体”——来推导。考虑一个以点 $\boldsymbol{x}$ 为顶点的无限小的四面体，其三个面与坐标平面平行，另一个斜面具有单位法向 $\boldsymbol{n}$。对这个四面体应用线[动量平衡原理](@entry_id:196256)（牛顿第二定律），即所有作用力之和等于质量乘以加速度。作用在四面体上的力包括四个面上的牵[引力](@entry_id:175476)（面力）和体内的体力。当我们将四面体的尺寸缩减至零时，体积相关的项（如体力和[惯性力](@entry_id:169104)）比面积相关的项（面力）更快地趋于零。在极限情况下，只有面力保留下来并相互平衡。这个平衡关系最终导出一个纯粹的代数关系，表明斜面上的牵[引力](@entry_id:175476) $\boldsymbol{t}(\boldsymbol{x}, \boldsymbol{n})$ 可以表示为作用在坐标面上的三个牵[引力](@entry_id:175476) $\boldsymbol{t}(\boldsymbol{x}, \boldsymbol{e}_1)$、$\boldsymbol{t}(\boldsymbol{x}, \boldsymbol{e}_2)$ 和 $\boldsymbol{t}(\boldsymbol{x}, \boldsymbol{e}_3)$ 的线性组合，其中系数就是 $\boldsymbol{n}$ 的分量 $n_1, n_2, n_3$。

这个线性映射的存在意味着，在点 $\boldsymbol{x}$ 的内部受力状态可以由一个二阶张量完全描述。这个张量被称为**柯西应力张量** (Cauchy stress tensor)，记为 $\boldsymbol{\sigma}$。牵[引力](@entry_id:175476)与法向的关系可以简洁地写成：
$$ \boldsymbol{t}(\boldsymbol{x}, \boldsymbol{n}) = \boldsymbol{\sigma}(\boldsymbol{x}) \boldsymbol{n} $$
这个方程被称为**柯西公式** (Cauchy's formula)。它是一个极其强大的工具，它告诉我们，只要知道了在某一点的应力张量 $\boldsymbol{\sigma}$（一个包含9个分量的矩阵），我们就可以计算出通过该点的**任意**方向平面上的牵[引力](@entry_id:175476) [@problem_id:3547598]。[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ 的第 $j$ 列，正是作用在法向为 $\boldsymbol{e}_j$ 的平面上的牵[引力](@entry_id:175476)矢量。

柯西公式的线性性质也为从实验或数值上重构[应力张量](@entry_id:148973)提供了途径。例如，在二维情况下，我们只需要测量作用在两个线性无关方向（如 $\boldsymbol{e}_x = [1,0]^T$ 和 $\boldsymbol{e}_y = [0,1]^T$）平面上的牵[引力](@entry_id:175476)，就可以完全确定该点的应力张量。测得的两个牵[引力](@entry_id:175476)矢量 $\boldsymbol{t}(\boldsymbol{e}_x)$ 和 $\boldsymbol{t}(\boldsymbol{e}_y)$ 直接构成了[应力张量](@entry_id:148973)矩阵的两列 [@problem_id:3547583]。如果在三维空间中，我们对三个线性无关的法向 $\boldsymbol{n}_1, \boldsymbol{n}_2, \boldsymbol{n}_3$ 进行“测量”，得到对应的牵[引力](@entry_id:175476) $\boldsymbol{t}_1, \boldsymbol{t}_2, \boldsymbol{t}_3$。我们可以将这些关系写成一个矩阵方程 $\mathbf{T} = \boldsymbol{\sigma} \mathbf{N}$，其中 $\mathbf{T}$ 和 $\mathbf{N}$ 分别是以牵[引力](@entry_id:175476)矢量和法向矢量为列的矩阵。只要 $\mathbf{N}$ 是可逆的（即法向是线性无关的），我们就可以通过求解 $\boldsymbol{\sigma} = \mathbf{T} \mathbf{N}^{-1}$ 来唯一地重构[应力张量](@entry_id:148973) [@problem_id:3547603]。

让我们通过一个具体的例子来应用柯西公式 [@problem_id:3547535]。假设一个物体内部某一点 $\boldsymbol{x}_0 = (1,1,1)$ 的应力张量为：
$$ \boldsymbol{\sigma}(1,1,1) = \begin{pmatrix} 3  & 2  & 1 \\ 2  & 4  & 1 \\ 1  & 1  & 5 \end{pmatrix} $$
我们想要求出作用在通过该点的一个[曲面](@entry_id:267450)上的牵[引力](@entry_id:175476)。该[曲面](@entry_id:267450)由方程 $f(x,y,z) = x^2 + 2y^2 + 3z^2 - 6 = 0$ 定义。首先，我们需要找到在点 $\boldsymbol{x}_0$ 处[曲面](@entry_id:267450)的单位外法向矢量 $\boldsymbol{n}$。这个法向平行于函数 $f$ 的梯度：
$$ \nabla f = \begin{pmatrix} \frac{\partial f}{\partial x} \\ \frac{\partial f}{\partial y} \\ \frac{\partial f}{\partial z} \end{pmatrix} = \begin{pmatrix} 2x \\ 4y \\ 6z \end{pmatrix} $$
在点 $(1,1,1)$，梯度为 $\nabla f(1,1,1) = [2, 4, 6]^T$。将其归一化，得到单位法向：
$$ \boldsymbol{n} = \frac{[2, 4, 6]^T}{\sqrt{2^2 + 4^2 + 6^2}} = \frac{1}{\sqrt{56}} \begin{pmatrix} 2 \\ 4 \\ 6 \end{pmatrix} = \frac{1}{\sqrt{14}} \begin{pmatrix} 1 \\ 2 \\ 3 \end{pmatrix} $$
现在，我们可以使用柯西公式计算牵[引力](@entry_id:175476)矢量 $\boldsymbol{t} = \boldsymbol{\sigma}\boldsymbol{n}$：
$$ \boldsymbol{t} = \begin{pmatrix} 3  & 2  & 1 \\ 2  & 4  & 1 \\ 1  & 1  & 5 \end{pmatrix} \frac{1}{\sqrt{14}} \begin{pmatrix} 1 \\ 2 \\ 3 \end{pmatrix} = \frac{1}{\sqrt{14}} \begin{pmatrix} 3(1) + 2(2) + 1(3) \\ 2(1) + 4(2) + 1(3) \\ 1(1) + 1(2) + 5(3) \end{pmatrix} = \frac{1}{\sqrt{14}} \begin{pmatrix} 10 \\ 13 \\ 18 \end{pmatrix} $$
这表明，尽管应力状态是由一个张量描述的抽象概念，但它通过柯西公式与可测量的物理量——牵[引力](@entry_id:175476)——直接相关。牵[引力](@entry_id:175476)绝非仅仅是边界上的属性，而是内部应力状态在特定界面上的直接体现 [@problem_id:3547598]。

### 平衡方程与应力[张量的对称性](@entry_id:202126)

有了应力张量的概念，我们现在可以重新表述连续介质的运动定律。

#### 线[动量平衡](@entry_id:193575)与柯西第一运动定律

我们从线[动量平衡](@entry_id:193575)的积分形式出发，它适用于物体内任何一个有限的子区域 $P$：
$$ \frac{d}{dt} \int_P \rho \boldsymbol{v} \, dV = \int_P \boldsymbol{b} \, dV + \int_{\partial P} \boldsymbol{t}(\boldsymbol{x}, \boldsymbol{n}) \, dS $$
左边是子区域内总动量的变化率，可以通过[雷诺输运定理](@entry_id:191217)转化为 $\int_P \rho \boldsymbol{a} \, dV$，其中 $\boldsymbol{a}$ 是[物质加速度](@entry_id:270992)。右边是作用在该子区域上的总体力和总面力。

利用柯西公式 $\boldsymbol{t} = \boldsymbol{\sigma}\boldsymbol{n}$ 和[高斯散度定理](@entry_id:188065)，我们可以将边界上的面积分转化为[体积分](@entry_id:171119)：
$$ \int_{\partial P} \boldsymbol{t} \, dS = \int_{\partial P} \boldsymbol{\sigma}\boldsymbol{n} \, dS = \int_P (\nabla \cdot \boldsymbol{\sigma}) \, dV $$
这里，$\nabla \cdot \boldsymbol{\sigma}$ 是应力[张量的散度](@entry_id:191736)，它是一个矢量，其第 $i$ 个分量是 $(\nabla \cdot \boldsymbol{\sigma})_i = \sum_j \partial \sigma_{ji} / \partial x_j$（注意索引顺序，这与 $\boldsymbol{t}=\boldsymbol{\sigma}^T\boldsymbol{n}$ 的定义约定有关；若使用 $\boldsymbol{t}=\boldsymbol{\sigma}\boldsymbol{n}$ 且 $\boldsymbol{\sigma}$ 对称，则为 $\sum_j \partial \sigma_{ij} / \partial x_j$）。将所有项都表示为在体积 $P$ 上的积分，我们得到：
$$ \int_P \left( \nabla \cdot \boldsymbol{\sigma} + \boldsymbol{b} - \rho \boldsymbol{a} \right) \, dV = \boldsymbol{0} $$
由于这个方程必须对**任意**子区域 $P$ 都成立，所以被积函数（假设连续）必须处处为零。这导出了线[动量平衡](@entry_id:193575)的**局部**（[微分](@entry_id:158718)）形式，即**柯西第一运动定律**：
$$ \nabla \cdot \boldsymbol{\sigma} + \boldsymbol{b} = \rho \boldsymbol{a} $$
在静力学问题中，加速度 $\boldsymbol{a} = \boldsymbol{0}$，方程简化为**[平衡方程](@entry_id:172166)**：
$$ \nabla \cdot \boldsymbol{\sigma} + \boldsymbol{b} = \boldsymbol{0} $$
这个[偏微分方程组](@entry_id:172573)将[应力张量](@entry_id:148973)的空间变化率与[体力](@entry_id:174230)联系起来。它意味着，一个给定的应[力场](@entry_id:147325)要能成为一个[平衡解](@entry_id:174651)，它必须满足这个方程。例如，在一个受有均匀[体力](@entry_id:174230) $\boldsymbol{b} = b_0(\boldsymbol{e}_1+\boldsymbol{e}_2+\boldsymbol{e}_3)$ 的物体中，如果应[力场](@entry_id:147325)具有 $\sigma_{ii} = a + c x_i$ 的形式，通过代入平衡方程，我们可以立即确定常数 $c$ 必须等于 $-b_0$ [@problem_id:3547551]。

#### [角动量平衡](@entry_id:181848)与柯西第二运动定律

除了[线动量](@entry_id:174467)，角动量也必须守恒。对于一个非极性介质（即不存在[体力](@entry_id:174230)偶或面力偶），[角动量平衡](@entry_id:181848)的局部形式要求柯西应力张量必须是**对称的**，即 $\boldsymbol{\sigma} = \boldsymbol{\sigma}^T$。这被称为**柯西第二运动定律**。

这个深刻的结论可以通过考虑作用在一个无限小立方体上的[力矩平衡](@entry_id:752138)来推导。也可以通过更普适的积分形式推导。对于一个由常数应力 $\boldsymbol{\sigma}$ 作用的体积为 $V$ 的封闭体，由[表面牵引力](@entry_id:169207)产生的总力矩 $\mathbf{M}_S$ 可以通过[散度定理](@entry_id:143110)被证明为 [@problem_id:3547544]：
$$ \mathbf{M}_S = \int_{\partial V} \mathbf{r} \times \mathbf{t} \, dS = V \begin{pmatrix} \sigma_{32} - \sigma_{23} \\ \sigma_{13} - \sigma_{31} \\ \sigma_{21} - \sigma_{12} \end{pmatrix} = 2V\boldsymbol{\omega} $$
其中 $\boldsymbol{\omega}$ 是[应力张量](@entry_id:148973)反对称部分 $\frac{1}{2}(\boldsymbol{\sigma} - \boldsymbol{\sigma}^T)$ 的[轴矢量](@entry_id:196296)。在没有[体力](@entry_id:174230)偶且处于平衡状态时，总力矩必须为零。因此，$\boldsymbol{\omega}$ 必须为零，这意味着 $\boldsymbol{\sigma} - \boldsymbol{\sigma}^T = \mathbf{0}$，即 $\boldsymbol{\sigma}$ 是对称的。

应力[张量的对称性](@entry_id:202126)是一个极其重要的性质。它将描述三维应力状态所需的独立分量从9个减少到6个。这是经典[连续介质力学](@entry_id:155125)的一个基本假设，并且在绝大多数工程应用中都成立。

### 在[计算力学](@entry_id:174464)中的应用与推论

上述原理构成了[计算固体力学](@entry_id:169583)的理论基石。它们不仅定义了要求解的方程，还塑造了求解方法的结构。

#### 虚功原理与弱形式

直接求解[平衡方程](@entry_id:172166)这个[偏微分方程组](@entry_id:172573)（即强形式）在复杂几何和材料下通常很困难。[计算力学](@entry_id:174464)，特别是有限元方法（FEM），通常基于其等价的积分形式，即**虚功原理**（或[虚功](@entry_id:176403)率原理）。

通过将平衡方程 $\nabla \cdot \boldsymbol{\sigma} + \boldsymbol{b} = \mathbf{0}$ 与一个任意的、满足[运动学](@entry_id:173318)约束的[虚位移](@entry_id:168781)（或虚速度）场 $\boldsymbol{w}$ 做[内积](@entry_id:158127)，并在整个区域 $\Omega$ 上积分，我们得到：
$$ \int_\Omega (\nabla \cdot \boldsymbol{\sigma} + \boldsymbol{b}) \cdot \boldsymbol{w} \, dV = 0 $$
利用[散度定理](@entry_id:143110)（即分部积分）处理第一项，并利用柯西公式，我们得到：
$$ - \int_\Omega \boldsymbol{\sigma} : \nabla \boldsymbol{w} \, dV + \int_{\partial \Omega} \boldsymbol{t} \cdot \boldsymbol{w} \, dS + \int_\Omega \boldsymbol{b} \cdot \boldsymbol{w} \, dV = 0 $$
重新整理后，我们得到[虚功](@entry_id:176403)方程：
$$ \int_\Omega \boldsymbol{\sigma} : \boldsymbol{\varepsilon}(\boldsymbol{w}) \, dV = \int_\Omega \boldsymbol{b} \cdot \boldsymbol{w} \, dV + \int_{\Gamma_t} \overline{\boldsymbol{t}} \cdot \boldsymbol{w} \, dS $$
这里，我们使用了应力[张量的对称性](@entry_id:202126)，使得 $\boldsymbol{\sigma} : \nabla \boldsymbol{w} = \boldsymbol{\sigma} : \boldsymbol{\varepsilon}(\boldsymbol{w})$，其中 $\boldsymbol{\varepsilon}(\boldsymbol{w})$ 是虚应变。边界积分仅在施加了已知牵[引力](@entry_id:175476) $\overline{\boldsymbol{t}}$ 的边界部分 $\Gamma_t$ 上进行，因为在位移边界 $\Gamma_u$ 上，[虚位移](@entry_id:168781) $\boldsymbol{w}$ 为零。

这个方程被称为**[弱形式](@entry_id:142897)**。它将[求解微分方程](@entry_id:137471)的问题转化为了求解一个[积分方程](@entry_id:138643)。有限元法的本质就是将求解域离散化，并在这个弱形式的基础上构建一个大型[代数方程](@entry_id:272665)组。值得注意的是，弱形式的推导过程完美地展示了体力如何贡献于[体积分](@entry_id:171119)项，而规定的面力（牵[引力](@entry_id:175476)）如何贡献于边界积分项 [@problem_id:3547598]。对这个积分等式的[数值验证](@entry_id:156090)，是验证有限元代码正确性的一个基本步骤 [@problem_id:3547582]。

#### 边界值问题与[适定性](@entry_id:148590)

在实际问题中，物体的全部边界 $\partial\Omega$ 会被划分为施加位移约束的**狄利克雷 (Dirichlet) 边界** $\Gamma_u$ 和施加力约束的**诺伊曼 (Neumann) 边界** $\Gamma_t$。问题的**[适定性](@entry_id:148590)**（解的存在性、唯一性和稳定性）与这种划分密切相关 [@problem_id:3547542]。

- **[混合边值问题](@entry_id:187682)**：如果 $\Gamma_u$ 的面积不为零，即至少有一小部分边界的位移是固定的，那么刚体运动（平移和旋转）就被有效抑制了。在这种情况下，对于任意（足够光滑的）[体力](@entry_id:174230) $\boldsymbol{b}$ 和面力 $\overline{\boldsymbol{t}}$，弹性力学问题都存在唯一的解。施加的载荷不需要满足任何特殊的全局平衡条件，因为任何不平衡的力或力矩都会由 $\Gamma_u$ 上的**反作用力**来平衡。

- **纯牵[引力](@entry_id:175476)问题**：如果 $\Gamma_u$ 为空，即整个边界上都施加的是力（牵[引力](@entry_id:175476)），那么刚体运动是不受约束的。此时，为了使问题有解，所有施加的外力（包括[体力](@entry_id:174230)和面力）必须自身处于平衡状态。也就是说，总[合力](@entry_id:163825)和总[合力矩](@entry_id:166772)必须为零：
$$ \int_\Omega \boldsymbol{b} \, dV + \int_{\partial \Omega} \overline{\boldsymbol{t}} \, dS = \mathbf{0} $$
$$ \int_\Omega \boldsymbol{x} \times \boldsymbol{b} \, dV + \int_{\partial \Omega} \boldsymbol{x} \times \overline{\boldsymbol{t}} \, dS = \mathbf{0} $$
即使满足了这些条件，解也只能在相差一个任意刚体位移的意义下是唯一的。

#### 全局平衡检验与坐标[不变性](@entry_id:140168)

在计算模拟中，即使一个问题理论上是平衡的，由于离散化和数值误差，计算出的解可能不会精确满足平衡条件。因此，一个重要的验证步骤是检查**全局平衡残差** $\mathbf{R}$：
$$ \mathbf{R} = \int_\Omega \boldsymbol{b} \, dV + \int_{\partial \Omega} \boldsymbol{t} \, dS $$
其中边界牵[引力](@entry_id:175476) $\boldsymbol{t}$ 是根据计算出的应[力场](@entry_id:147325) $\boldsymbol{\sigma}$ 通过柯西公式 $\boldsymbol{t} = \boldsymbol{\sigma}\boldsymbol{n}$ 得到的。对于一个精确的[平衡解](@entry_id:174651)，$\mathbf{R}$ 应为零。在数值解中，其范数 $\|\mathbf{R}\|$ 的大小可以作为衡量解的质量和[网格质量](@entry_id:151343)的一个指标 [@problem_id:3547515]。

最后，我们必须强调应力张量和牵[引力](@entry_id:175476)矢量都是物理实体，它们的定义和它们之间的关系 $\boldsymbol{t} = \boldsymbol{\sigma}\boldsymbol{n}$ 是客观的，不依赖于观察者选择的[坐标系](@entry_id:156346)。这是一个深刻的物理原理，称为**物质坐标[不变性](@entry_id:140168)**。这意味着，无论我们是在笛卡尔坐标系中，还是在复杂的[曲线坐标系](@entry_id:172561)（如极坐标、球坐标或任意自定义[坐标系](@entry_id:156346)）中进行计算，只要正确地应用[张量变换法则](@entry_id:185176)，最终得到的物理矢量（如牵[引力](@entry_id:175476)）在物理空间中必须是相同的。通过在不同[坐标系](@entry_id:156346)下进行计算并验证结果的一致性，我们可以深刻理解这些物理量的张量本质，并对处理复杂几何形状的计算方法建立信心 [@problem_id:3547607]。

综上所述，从体力和面力的基本概念出发，通过柯西的应力原理和[动量平衡](@entry_id:193575)定律，我们构建了描述连续介质内部力学行为的数学框架。柯西[应力张量](@entry_id:148973)、柯西公式以及[平衡方程](@entry_id:172166)构成了这一框架的核心，它们不仅为理论分析提供了基础，也直接指导了现代计算力学方法的建立与应用。