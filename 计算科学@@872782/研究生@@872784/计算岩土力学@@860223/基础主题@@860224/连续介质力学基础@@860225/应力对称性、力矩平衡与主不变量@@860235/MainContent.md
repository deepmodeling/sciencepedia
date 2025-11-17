## 引言
在计算岩土力学和连续介质力学的研究中，准确描述和分析材料内部的力学状态是理解其变形与破坏行为的先决条件。核心概念是应力张量，它完整地刻画了某一点的受力情况。然而，应力张量作为一个数学实体，其背后的物理意义，特别是其对称性与基本物理定律的联系，以及如何用不依赖于[坐标系](@entry_id:156346)的方式来表征其“大小”与“形状”，是初学者和研究人员需要深入掌握的关键知识。本文旨在系统性地填补理论推导与工程应用之间的认知鸿沟。

本文将引导读者踏上一段从基本原理到前沿应用的探索之旅。在第一章“原理与机制”中，我们将回归本源，从动量与[角动量平衡](@entry_id:181848)定律出发，揭示柯西[应力张量对称性](@entry_id:201218)的深刻物理根源，并详细介绍[主应力](@entry_id:176761)与[应力不变量](@entry_id:170526)这些用于描述应力状态内在特性的强大数学工具。接下来的第二章“应用与跨学科联系”将视野拓宽至实际工程领域，展示这些理论如何在各向同性与[各向异性材料](@entry_id:184874)的本构模型构建、复杂数值模拟的实现与验证，乃至与[广义连续介质理论](@entry_id:193621)的交叉中发挥关键作用。最后，在第三章“动手实践”部分，读者将通过具体的计算练习，将理论知识转化为解决实际问题的能力。通过这一结构化的学习路径，本文旨在帮助读者建立一个关于[应力分析](@entry_id:168804)的坚实而全面的知识体系。

## 原理与机制

在[连续介质力学](@entry_id:155125)中，应力状态的描述是分析材料响应的基础。本章旨在深入阐述[应力张量](@entry_id:148973)的基本原理，从柯西[应力张量](@entry_id:148973)的定义出发，探讨其对称性的物理根源，并介绍描述应力状态大小和形状的坐标无关量——主[应力[不变](@entry_id:170526)量](@entry_id:148850)。这些概念不仅是理论力学的基石，也在计算岩[土力学](@entry_id:180264)中具有至关重要的实际应用。

### 柯西[应力张量](@entry_id:148973)与[动量平衡](@entry_id:193575)

我们对材料内部相互作用的探索始于**牵[引力](@entry_id:175476)（traction）**的概念。想象在连续体内部任意取一点$P$，并构造一个经过该点的微小虚拟切割面。该切割面的方位可由其[单位法向量](@entry_id:178851) $\boldsymbol{n}$ 唯一确定。根据[牛顿第三定律](@entry_id:166652)，切割面两侧的物质会相互作用。我们将一侧物质对另一侧物质施加的[分布](@entry_id:182848)力，在$P$点处单位面积上的极限，定义为该点的牵[引力](@entry_id:175476)矢量 $\boldsymbol{t}(\boldsymbol{n})$。

一个核心问题是，牵[引力](@entry_id:175476) $\boldsymbol{t}$ 如何依赖于平面的方位 $\boldsymbol{n}$？法国数学家 Augustin-Louis Cauchy 提出了一个基本假设，即**柯西假设（Cauchy's postulate）**：在某一点的牵[引力](@entry_id:175476)仅取决于该点的空间位置和该平面的法向量，而与平面的曲率无关。基于此假设，并应用[线性动量守恒](@entry_id:165717)定律，我们可以推导出牵[引力](@entry_id:175476)与法向量之间存在一个线性关系。

考虑一个以$P$点为顶点的无限小四面体，其三个面分别垂直于笛卡尔坐标系的[基向量](@entry_id:199546) $\boldsymbol{e}_1, \boldsymbol{e}_2, \boldsymbol{e}_3$，第四个斜面的[单位法向量](@entry_id:178851)为 $\boldsymbol{n}$。通过对该四面体应用[线性动量平衡](@entry_id:193575)方程（即[牛顿第二定律](@entry_id:274217)的积分形式），并在[四面体体积](@entry_id:176424)趋于零时取极限，可以证明牵[引力](@entry_id:175476)矢量 $\boldsymbol{t}(\boldsymbol{n})$ 是法向量 $\boldsymbol{n}$ 的线性函数。这个[线性关系](@entry_id:267880)可以通过一个二阶张量来表示，这个张量就是**柯西[应力张量](@entry_id:148973)（Cauchy stress tensor）**，记为 $\boldsymbol{\sigma}$。它们之间的关系，即**柯西公式（Cauchy's formula）**，表达为：

$$
\boldsymbol{t}(\boldsymbol{n}) = \boldsymbol{\sigma}\boldsymbol{n}
$$

这个公式是[连续介质力学](@entry_id:155125)的基石之一 [@problem_id:3565135]。它表明，一旦我们知道了在某一点的[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$（一个包含九个分量的量），我们就可以确定作用于经过该点的任意方向平面的牵[引力](@entry_id:175476)。应力张量 $\boldsymbol{\sigma}$ 和牵[引力](@entry_id:175476) $\boldsymbol{t}$ 的物理单位都是力每单位面积，在[国际单位制](@entry_id:172547)中是帕斯卡（$\mathrm{Pa}$）或 $\mathrm{N/m^2}$。

### 应力[张量的对称性](@entry_id:202126)：[角动量平衡](@entry_id:181848)的推论

柯西[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ 的一个至关重要的性质是其**对称性**。在**经典（非极性）连续介质**理论中，这一性质是[角动量平衡](@entry_id:181848)的直接推论。经典连续介质理论假设物质点只具有[平动自由度](@entry_id:140257)，不考虑其自身的旋转。

对于任意一个物质体积，其角动量的变化率等于作用于其上的所有外力的力矩之和。当我们考虑一个无限小的立方体单元，并假设不存在**体力矩（body couples）**或内禀的**[力偶应力](@entry_id:747952)（couple stresses）**时，[角动量平衡](@entry_id:181848)方程最终会简化为一个纯代数约束 [@problem_id:3565135] [@problem_id:3565145]。在分量形式中，这个约束写作 $\epsilon_{ijk}\sigma_{jk} = 0$，其中 $\epsilon_{ijk}$ 是列维-奇维塔（Levi-Civita）[置换符号](@entry_id:153173)。这个方程直接导出：

$$
\sigma_{ij} = \sigma_{ji}
$$

或者用[张量表示](@entry_id:180492)为 $\boldsymbol{\sigma} = \boldsymbol{\sigma}^{\mathsf{T}}$。这意味着在经典连续介质中，柯西[应力张量](@entry_id:148973)是一个[对称张量](@entry_id:148092)，其九个分量中只有六个是独立的。

在计算岩土力学中，由于[数值误差](@entry_id:635587)（例如，欠积分的单元更新或非收敛的迭代），有限元程序有时可能会输出非对称的应力张量 [@problem_id:3565164]。面对这种情况，我们必须认识到，任何非对称部分都违反了[角动量平衡](@entry_id:181848)这一基本物理定律。因此，物理上可接受的[应力张量](@entry_id:148973)应该是数值结果的**对称部分**。给定一个“原始”的非[对称张量](@entry_id:148092) $\boldsymbol{\sigma}^{\text{raw}}$，其物理上对应的应力张量 $\boldsymbol{\sigma}$ 应通过以下方式获得：

$$
\boldsymbol{\sigma} = \frac{1}{2}(\boldsymbol{\sigma}^{\text{raw}} + (\boldsymbol{\sigma}^{\text{raw}})^{\mathsf{T}})
$$

例如，如果一个数值模拟报告的应力为 $\boldsymbol{\sigma}^{\text{raw}}=\begin{pmatrix} 80  30  -10 \\ 25  50  20 \\ -15  5  40 \end{pmatrix}\,\mathrm{MPa}$，我们可以观察到 $\sigma_{12} \neq \sigma_{21}$。物理上真实的应力应为其对称部分，即 $\boldsymbol{\sigma} = \begin{pmatrix} 80  27.5  -12.5 \\ 27.5  50  12.5 \\ -12.5  12.5  40 \end{pmatrix}\,\mathrm{MPa}$ [@problem_id:3565195]。忽略这种修正将导致错误的分析，因为[张量的反对称部分](@entry_id:193562)虽然不影响[法向应力](@entry_id:260622)或一阶[不变量](@entry_id:148850)，但会污染高阶[不变量](@entry_id:148850)（如 $J_2$）的计算，并导致[主应力](@entry_id:176761)计算的错误 [@problem_id:3565164]。

### [谱分解](@entry_id:173707)与[主应力](@entry_id:176761)

由于柯西应力张量 $\boldsymbol{\sigma}$ 是对称的，线性代数中的**谱定理（Spectral Theorem）**保证了它具有优良的数学性质。该定理指出，任何实对称[二阶张量](@entry_id:199780)都存在一组三个实数[特征值](@entry_id:154894)和三个相互正交的[特征向量](@entry_id:151813)。在[应力分析](@entry_id:168804)中，这些量具有深刻的物理意义：

-   [特征值](@entry_id:154894)被称为**主应力（principal stresses）**，记为 $\sigma_1, \sigma_2, \sigma_3$。
-   对应的[特征向量](@entry_id:151813)被称为**主方向（principal directions）**，记为 $\boldsymbol{n}_1, \boldsymbol{n}_2, \boldsymbol{n}_3$。

这意味着对于任何应力状态，总能找到一个[正交坐标](@entry_id:166074)系（由[主方向](@entry_id:276187)构成），在该[坐标系](@entry_id:156346)下应力张量的矩阵表示是对角的，对角线上的元素即为[主应力](@entry_id:176761)。这种表示方式揭示了应力状态的纯拉伸/压缩性质，不受剪切分量的复杂化。

应力[张量的对称性](@entry_id:202126)保证了其可以进行**[谱分解](@entry_id:173707)（spectral decomposition）** [@problem_id:3565145]：

$$
\boldsymbol{\sigma} = \sum_{i=1}^3 \sigma_i \boldsymbol{n}_i \otimes \boldsymbol{n}_i
$$

其中 $\otimes$ 表示张量积。这个表达式清晰地表明，任何应力状态都可以看作是沿三个相互正交的主方向上的单向拉伸或压缩状态的叠加。

主应力和主方向的一个关键几何解释是：在**[主平面](@entry_id:164488)**（即法向量为某一主方向的平面）上，牵[引力](@entry_id:175476)矢量是纯法向的，即牵[引力](@entry_id:175476)矢量平行于该平面的法向量。根据柯西公式，作用于[法向量](@entry_id:264185)为 $\boldsymbol{n}_i$ 的[主平面](@entry_id:164488)上的牵[引力](@entry_id:175476)为：

$$
\boldsymbol{t}(\boldsymbol{n}_i) = \boldsymbol{\sigma}\boldsymbol{n}_i = \sigma_i \boldsymbol{n}_i
$$

由于 $\boldsymbol{t}(\boldsymbol{n}_i)$ 与 $\boldsymbol{n}_i$ 平行，该平面上的**[剪切应力](@entry_id:137139)分量为零** [@problem_id:3565145]。[主平面](@entry_id:164488)是纯[法向应力](@entry_id:260622)作用的平面。

#### 重复[主应力](@entry_id:176761)的情形

在某些特殊的应力状态下，可能会出现两个或三个[主应力](@entry_id:176761)相等的情况，即**[特征值重数](@entry_id:156360)（eigenvalue multiplicity）**大于1。

-   **二重主应力**：如果两个[主应力](@entry_id:176761)相等（例如，$\sigma_2 = \sigma_3$），则与不重复的主应力 $\sigma_1$ 对应的的[主方向](@entry_id:276187) $\boldsymbol{n}_1$ 是唯一的（不计符号）。而与重复主应力 $\sigma_2$ 对应的特征空间是一个二维平面，该平面垂直于 $\boldsymbol{n}_1$。在这个平面内的任何单位向量都是一个有效的主方向。因此，存在无穷多个主方向的选择 [@problem_id:3565182]。这种情况对应于绕 $\boldsymbol{n}_1$ 轴旋转对称的应力状态。

-   **三重[主应力](@entry_id:176761)**：如果所有三个[主应力](@entry_id:176761)都相等（$\sigma_1 = \sigma_2 = \sigma_3 = p$），则应力状态是**静水的（hydrostatic）**或**各向同性的（isotropic）**，$\boldsymbol{\sigma} = p\boldsymbol{I}$，其中 $\boldsymbol{I}$ 是单位张量。在这种情况下，任何方向都是[主方向](@entry_id:276187)。空间中的任意一组正交基都可以作为主方向基。

主应力的[重数](@entry_id:136466)对[数值算法](@entry_id:752770)有重要影响。在主应力发生重合的点，从应力张量到其单个[特征向量](@entry_id:151813)的映射是不连续的，这会导致依赖于[特征向量](@entry_id:151813)导数的算法（如某些[弹塑性](@entry_id:193198)模型中的一致性[切线](@entry_id:268870)算子）变得不稳定或病态。一个稳健的解决方法是转而使用[谱投影算子](@entry_id:755184)，该算子即使在[特征值](@entry_id:154894)重合点也是光滑可微的 [@problem_id:3565182]。

### [应力不变量](@entry_id:170526)：坐标无关的描述

为了以不依赖于特定[坐标系](@entry_id:156346)选择的方式来表征应力状态的“大小”和“形状”，我们引入了**[应力不变量](@entry_id:170526)（stress invariants）**。这些是从[应力张量](@entry_id:148973)的分量构造出来的标量，其数值在[坐标系](@entry_id:156346)旋转下保持不变。

对于一个三维应力张量 $\boldsymbol{\sigma}$，其三个**[主不变量](@entry_id:193522)（principal invariants）**是其[特征多项式](@entry_id:150909) $\det(\boldsymbol{\sigma} - \lambda \boldsymbol{I}) = 0$ 的系数：

$$
\lambda^3 - I_1 \lambda^2 + I_2 \lambda - I_3 = 0
$$

这些[不变量](@entry_id:148850)可以用张量分量表示，也可以用主应力表示 [@problem_id:3565135]：

-   **第一[不变量](@entry_id:148850) $I_1$**：
    $I_1 = \mathrm{tr}(\boldsymbol{\sigma}) = \sigma_{kk} = \sigma_1 + \sigma_2 + \sigma_3$
    其单位是 $\mathrm{Pa}$。

-   **第二[不变量](@entry_id:148850) $I_2$**：
    $I_2 = \frac{1}{2} \left[ (\mathrm{tr}(\boldsymbol{\sigma}))^2 - \mathrm{tr}(\boldsymbol{\sigma}^2) \right] = \sigma_1\sigma_2 + \sigma_2\sigma_3 + \sigma_3\sigma_1$
    其单位是 $\mathrm{Pa}^2$。

-   **第三[不变量](@entry_id:148850) $I_3$**：
    $I_3 = \det(\boldsymbol{\sigma}) = \sigma_1\sigma_2\sigma_3$
    其单位是 $\mathrm{Pa}^3$。

[不变量](@entry_id:148850)的价值在于它们捕捉了应力状态的内在几何特性。例如，两个应力状态如果具有相同的[主应力](@entry_id:176761)集合，那么它们必然具有相同的 $(I_1, I_2, I_3)$ 值，也对应着完全相同的[莫尔圆](@entry_id:168131)（Mohr's circles）。然而，它们的空间方位（即[主方向](@entry_id:276187)）可能完全不同 [@problem_id:3565162]。一个应力状态由其内在的大小和形状（由[不变量](@entry_id:148850)描述）以及其在空间中的方位（由主方向描述）共同定义。

### 岩[土力学](@entry_id:180264)中的[不变量](@entry_id:148850)与[应力分解](@entry_id:272862)

在岩土力学和塑性力学中，将应力张量分解为两部分尤其有用：引起体积变化的**静水压力（hydrostatic）**[部分和](@entry_id:162077)引起形状变化的**偏应力（deviatoric）**部分。

$$
\boldsymbol{\sigma} = \boldsymbol{s} + p\boldsymbol{I}
$$

-   **平均应力（Mean Stress）** $p$：
    $p = \frac{1}{3} I_1 = \frac{1}{3}(\sigma_{11} + \sigma_{22} + \sigma_{33})$
    它代表了应力的静水压力分量。在岩土工程中，通常规定**压应力为正**。因此，一个纯静水压缩状态对应于 $p > 0$。

-   **[偏应力张量](@entry_id:267642)（Deviatoric Stress Tensor）** $\boldsymbol{s}$：
    $\boldsymbol{s} = \boldsymbol{\sigma} - p\boldsymbol{I}$
    [偏应力张量](@entry_id:267642)的迹恒为零，$\mathrm{tr}(\boldsymbol{s}) = 0$。它代表了应力状态中导致材料剪切变形或畸变的部分。

由于 $\boldsymbol{\sigma}$ 和 $p\boldsymbol{I}$ 都是对称的，[偏应力张量](@entry_id:267642) $\boldsymbol{s}$ 也是对称的。我们可以研究[偏应力张量](@entry_id:267642)的[不变量](@entry_id:148850)，它们在描述剪切行为和屈服准则时极为重要。其中最常用的是偏应力的第二和第三[不变量](@entry_id:148850)，记为 $J_2$ 和 $J_3$。

-   **[偏应力](@entry_id:163323)第二[不变量](@entry_id:148850) $J_2$**：
    $J_2 = \frac{1}{2} \boldsymbol{s}:\boldsymbol{s} = \frac{1}{2} s_{ij}s_{ji}$
    $J_2$ 是一个恒为非负的标量，它度量了应力状态的[剪切强度](@entry_id:754762)。其与[弗罗贝尼乌斯范数](@entry_id:143384)（Frobenius norm）的关系为 $\|\boldsymbol{s}\| = \sqrt{2J_2}$。用[主应力](@entry_id:176761)表示为：
    $$
    J_2 = \frac{1}{6} \left[ (\sigma_1-\sigma_2)^2 + (\sigma_2-\sigma_3)^2 + (\sigma_3-\sigma_1)^2 \right]
    $$
    从这个表达式可以看出，$J_2=0$ 当且仅当 $\sigma_1=\sigma_2=\sigma_3$，即应力状态为纯静水压力，没有任何剪切分量 [@problem_id:3565149]。

-   **[偏应力](@entry_id:163323)第三[不变量](@entry_id:148850) $J_3$**：
    $J_3 = \det(\boldsymbol{s}) = s_1 s_2 s_3$，其中 $s_i = \sigma_i - p$ 是[偏应力](@entry_id:163323)的[主值](@entry_id:189577)。

这些[不变量](@entry_id:148850)是许多岩土材料[本构模型](@entry_id:174726)的核心。例如：
-   **$J_2$ 塑性模型（如 von Mises 屈服准则）**：这类模型假设材料的屈服仅由 $J_2$ 的大小决定，与静水压力 $p$ 无关。这适用于描述金属等材料，但通常不适用于土体或岩石。
-   **压力相关模型（如 Drucker-Prager 准则）**：这类模型更适合岩土材料，其[屈服函数](@entry_id:167970)同时依赖于[剪切强度](@entry_id:754762)（通过 $J_2$）和静水压力（通过 $I_1$）。一个常见的形式是 $f(\boldsymbol{\sigma}) = \alpha I_1 + \sqrt{J_2} - k = 0$，其中 $\alpha$ 和 $k$ 是材料参数，反映了摩擦和粘聚特性 [@problem_id:3565149]。

#### 洛德角（Lode Angle）

除了剪切的“强度”（由 $J_2$ 度量），剪切的“类型”或“模式”也对岩土材料的响应有显著影响。**洛德角（Lode angle）** $\theta$ 就是为了表征这种模式而引入的[不变量](@entry_id:148850)。它通常通过 $J_2$ 和 $J_3$ 定义：

$$
\cos(3\theta) = \frac{3\sqrt{3}}{2} \frac{J_3}{J_2^{3/2}} \quad (\text{for } J_2 > 0)
$$

洛德角描述了在[主应力空间](@entry_id:184388)中，给定应力状态在所谓的**偏平面（deviatoric plane）**上的位置。它能够区分两种重要的轴对称应力状态 [@problem_id:3565146]：
-   **三轴压缩（Triaxial Compression, TC）**：$\sigma_1 > \sigma_2 = \sigma_3$。在这种状态下，$\theta = 0^\circ$（或 $0$ 弧度）。
-   **三轴拉伸（Triaxial Extension, TE）**：$\sigma_1 = \sigma_2 > \sigma_3$。在这种状态下，$\theta = 30^\circ$（或 $\pi/6$ 弧度，对于不同的定义可能是 $60^\circ$ 或 $-\pi/6$）。

一般的三维应力状态（$\sigma_1 \ge \sigma_2 \ge \sigma_3$）介于这两种极端情况之间。洛德角的符号和大小反映了中间主应力 $\sigma_2$ 相对于最大和最小[主应力](@entry_id:176761) $\sigma_1, \sigma_3$ 的位置。例如，一个计算表明，对于某对称[应力张量](@entry_id:148973)，其平均应力 $p=\frac{170}{3}\,\mathrm{MPa}$，$J_2=\frac{18025}{12}\,\mathrm{MPa}^2$，$J_3>0$，计算得到的洛德角约为 $\theta \approx 26.6^\circ$，这表明该应力状态接近三轴拉伸 [@problem_id:3565195] [@problem_id:3565146]。

### 超越经典连续介质：[非对称应力](@entry_id:191550)

我们之前关于[应力对称性](@entry_id:181689)的讨论，其前提是材料被建模为**经典（非极性）连续介质**。然而，对于具有显著微观结构的材料，如[颗粒材料](@entry_id:750005)、[复合材料](@entry_id:139856)或[多孔介质](@entry_id:154591)，这种假设可能不成立。这些材料的微观单元不仅会平移，还可能发生独立的旋转。

为了描述这种行为，发展了**微极连续介质（micropolar continuum）**或**科塞拉（Cosserat）介质**理论。在这种理论中，除了位移场 $\boldsymbol{u}$，还引入了一个独立的**[微旋转](@entry_id:184355)场 $\boldsymbol{\varphi}$**。材料内部不仅能传递力（通过力应力 $\boldsymbol{\sigma}$），还能传递力矩（通过**[力偶应力](@entry_id:747952)张量 $\boldsymbol{\mu}$**）。

在这种更广义的框架下，[角动量平衡](@entry_id:181848)方程必须包含[力偶应力](@entry_id:747952)的贡献 [@problem_id:3565187]。其局部形式变为：

$$
\mu_{ij,j} + \epsilon_{ijk}\sigma_{jk} + c_i = J\ddot{\varphi}_i
$$

其中 $c_i$ 是体力矩密度，$J$ 是微惯量。这个方程揭示了一个根本性的变化：$\epsilon_{ijk}\sigma_{jk}$ 项（即 $\boldsymbol{\sigma}$ 的反对称部分的[轴矢量](@entry_id:196296)）不再必须为零。这意味着**力[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ 通常是非对称的**。其反对称部分直接与力偶[应力的散度](@entry_id:185633)、体力矩以及[微旋转](@entry_id:184355)的惯性相关。

一个简单的离散[晶格模型](@entry_id:184345)可以直观地展示这种效应。想象一系列由偏心弹簧连接的刚性块体，这种结构在宏观上可以等效为一个能够支持[力偶应力](@entry_id:747952)的连续介质。当这个介质发生弯曲时，会产生一个与[微旋转](@entry_id:184355)梯度（曲率）成正比的[力偶应力](@entry_id:747952) $m_z$ [@problem_id:3565144]。

应力[张量的对称性](@entry_id:202126)在[微极理论](@entry_id:202574)中被恢复为一个特例。当[力偶应力](@entry_id:747952)场为常数（$\mu_{ij,j}=0$）、[体力](@entry_id:174230)矩为零（$c_i=0$）且[微旋转](@entry_id:184355)惯性效应可忽略时（$J\ddot{\varphi}_i=0$），[角动量平衡](@entry_id:181848)方程才退化为经典的 $\epsilon_{ijk}\sigma_{jk} = 0$，从而保证了 $\boldsymbol{\sigma}$ 的对称性 [@problem_id:3565187]。

值得注意的是，即使[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ 是非对称的，其[主不变量](@entry_id:193522) $I_1, I_2, I_3$ 仍然是客观且良定义的。特别地，由于任何[反对称张量](@entry_id:199349)的迹都为零，第一[不变量](@entry_id:148850) $I_1 = \mathrm{tr}(\boldsymbol{\sigma})$ 始终等于其对称部分的迹。这意味着静水压力 $p = \frac{1}{3}I_1$ 始终不受应力张量反对称部分的影响 [@problem_id:3565144]。