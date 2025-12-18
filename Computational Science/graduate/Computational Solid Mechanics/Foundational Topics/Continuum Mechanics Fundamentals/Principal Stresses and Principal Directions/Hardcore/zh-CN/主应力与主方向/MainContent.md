## 引言
在[固体力学](@entry_id:164042)中，理解材料内部的应力状态是预测其行为和失效的关键。然而，完整的应力张量表示方法依赖于所选的[坐标系](@entry_id:156346)，这为直观理解和比较带来了挑战。为了解决这一问题，力学引入了[主应力与主方向](@entry_id:193792)这一核心概念，它们提供了对受力状态的一种客观且物理意义明确的描述。本文旨在系统性地阐述主应力理论及其应用。在第一章“原理与机制”中，我们将从柯西[应力张量](@entry_id:148973)出发，揭示主应力作为[特征值问题](@entry_id:142153)的数学本质及其基本性质。随后的第二章“应用与跨学科联系”将展示这一概念如何在[材料失效准则](@entry_id:189510)、[计算固体力学](@entry_id:169583)以及多物理场耦合问题中发挥关键作用。最后，在第三章“动手实践”中，读者将通过具体的编程练习，将理论知识转化为解决实际问题的能力。通过这三部分的学习，您将对[主应力与主方向](@entry_id:193792)建立起从理论到实践的全面认识。

## 原理与机制

在[连续介质力学](@entry_id:155125)中，应力状态的分析是理解材料如何响应外部载荷的核心。虽然应力张量以九个分量完整地描述了一个点的应力状态，但这种表示方式依赖于[坐标系](@entry_id:156346)的选择。为了获得一种不依赖于[坐标系](@entry_id:156346)的、更具物理洞察力的描述，我们引入了[主应力与主方向](@entry_id:193792)的概念。本章将从第一性原理出发，系统地阐述主应力的定义、物理意义及其数学基础，并探讨其在一些特殊和高级情况下的表现。

### 从面力到应力：柯西应力张量

想象在连续体内部取一个点，并通过这个点切割一个无限小的虚拟平面。该平面的方位由其[单位法向量](@entry_id:178851) $\boldsymbol{n}$ 定义。根据柯西应力原理，平面一侧的材料对另一侧施加的力，在单位面积上的[分布](@entry_id:182848)极限，定义为 **[面力矢量](@entry_id:189429)** (traction vector) $\boldsymbol{t}(\boldsymbol{n})$。这个矢量既依赖于点的位置，也依赖于平面的方位 $\boldsymbol{n}$。

一个关键的洞见，即柯西应力定理，指出[面力矢量](@entry_id:189429) $\boldsymbol{t}(\boldsymbol{n})$ 与法向量 $\boldsymbol{n}$ 之间存在[线性关系](@entry_id:267880)。这意味着存在一个二阶张量 $\boldsymbol{\sigma}$，它完全描述了该点的应力状态，并通过以下关系将任意方向 $\boldsymbol{n}$ 映射到对应的[面力矢量](@entry_id:189429) $\boldsymbol{t}(\boldsymbol{n})$：

$$
\boldsymbol{t}(\boldsymbol{n}) = \boldsymbol{\sigma}\boldsymbol{n}
$$

在分量形式下，我们有 $t_i = \sigma_{ij}n_j$。这个张量 $\boldsymbol{\sigma}$ 被称为 **柯西应力张量**。必须明确区分这两个概念：$\boldsymbol{\sigma}$ 是一个[二阶张量](@entry_id:199780)，代表一个点的完整应力状态，不依赖于任何特定平面；而 $\boldsymbol{t}(\boldsymbol{n})$ 是一个矢量，表示在特定方位平面 $\boldsymbol{n}$ 上作用的力 。

### 应力[张量的对称性](@entry_id:202126)

在经典[连续介质力学](@entry_id:155125)中，一个至关重要的性质是柯西应力[张量的对称性](@entry_id:202126)，即 $\boldsymbol{\sigma} = \boldsymbol{\sigma}^T$ 或 $\sigma_{ij} = \sigma_{ji}$。这一性质并非公理，而是可以从动量矩平衡定律（[角动量守恒](@entry_id:156798)）推导出来的。

考虑一个无限小的立方体单元，在没有体力偶或面力偶（即非极性介质）的假设下，为了防止该单元产生无限大的[角加速度](@entry_id:177192)，作用在其表面上的剪切应力所产生的力矩必须相互平衡。这一平衡条件直接导致了剪切应力互等定理，即 $\sigma_{ij} = \sigma_{ji}$。因此，应力[张量的对称性](@entry_id:202126)是角动量守恒在连续介质中的直接体现，而非来自线动量守恒  。这个对称性是后续所有讨论的基石，因为它极大地简化了应力张量的数学结构。

### [主应力与主方向](@entry_id:193792)：一个[特征值问题](@entry_id:142153)

现在我们提出一个关键问题：是否存在某些特殊的平面，其上的作用力完全是法向的？换言之，在这些平面上，剪切应力为零。这样的平面被称为 **[主平面](@entry_id:164488)** (principal planes)，其法线方向被称为 **主方向** (principal directions)。

从物理定义上看，如果一个平面是[主平面](@entry_id:164488)，其法向量为 $\boldsymbol{n}$，那么作用其上的[面力矢量](@entry_id:189429) $\boldsymbol{t}(\boldsymbol{n})$ 必须与 $\boldsymbol{n}$ 共线。这可以用数学语言表达为：

$$
\boldsymbol{t}(\boldsymbol{n}) = \lambda \boldsymbol{n}
$$

其中 $\lambda$ 是一个标量，它表示该[主平面](@entry_id:164488)上的[法向应力](@entry_id:260622)大小。将柯西公式 $\boldsymbol{t}(\boldsymbol{n}) = \boldsymbol{\sigma}\boldsymbol{n}$ 代入上式，我们得到：

$$
\boldsymbol{\sigma}\boldsymbol{n} = \lambda \boldsymbol{n}
$$

这个方程是线性代数中标准的 **特征值问题** (eigenvalue problem) 。这意味着：
- **[主应力](@entry_id:176761)** (principal stresses) $\lambda$ 是应力张量 $\boldsymbol{\sigma}$ 的[特征值](@entry_id:154894)。
- **主方向** (principal directions) $\boldsymbol{n}$ 是[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ 的[特征向量](@entry_id:151813)。

为了找到主应力，我们需要求解上述方程。将方程改写为[齐次线性方程组](@entry_id:153432)：

$$
(\boldsymbol{\sigma} - \lambda\boldsymbol{I})\boldsymbol{n} = \boldsymbol{0}
$$

其中 $\boldsymbol{I}$ 是二阶单位张量。为了使该方程有非零解（即存在主方向 $\boldsymbol{n} \neq \boldsymbol{0}$），[系数矩阵](@entry_id:151473) $(\boldsymbol{\sigma} - \lambda\boldsymbol{I})$ 必须是奇异的，即其[行列式](@entry_id:142978)为零：

$$
\det(\boldsymbol{\sigma} - \lambda\boldsymbol{I}) = 0
$$

这就是应力张量的 **特征方程** (characteristic equation)。对于三维问题，这是一个关于 $\lambda$ 的三次多项式，求解它可以得到三个主应力，记为 $\sigma_1, \sigma_2, \sigma_3$。

对于每个求出的[主应力](@entry_id:176761) $\sigma_i$，将其代回[特征值方程](@entry_id:192306) $(\boldsymbol{\sigma} - \sigma_i\boldsymbol{I})\boldsymbol{n}_i = \boldsymbol{0}$，即可解出对应的主方向 $\boldsymbol{n}_i$。按照惯例，[主方向](@entry_id:276187)被归一化为单位矢量，即 $\|\boldsymbol{n}\|=1$，因为它代表一个方向 。

### 主应力的存在性与性质

应力[张量的对称性](@entry_id:202126)保证了[主应力与主方向](@entry_id:193792)具有极其优良的性质。根据线性代数中的 **[谱定理](@entry_id:136620)** (Spectral Theorem)，对于任意[实对称矩阵](@entry_id:192806)（或张量），其所有[特征值](@entry_id:154894)均为实数，并且存在一组相互正交的[特征向量](@entry_id:151813)构成该空间的一组[标准正交基](@entry_id:147779)。

将此定理应用于对称的柯西应力张量 $\boldsymbol{\sigma}$，我们得到以下重要结论  ：
1.  **实数[主应力](@entry_id:176761)**：任意应力状态下，三个[主应力](@entry_id:176761) $\sigma_1, \sigma_2, \sigma_3$ 总是实数。这符合其作为物理可测量应力的直观。
2.  **正交[主方向](@entry_id:276187)**：总能找到三个相互正交的[主方向](@entry_id:276187) $\boldsymbol{n}_1, \boldsymbol{n}_2, \boldsymbol{n}_3$。这些方向构成了一个笛卡尔坐标系，称为 **主[坐标系](@entry_id:156346)**。在这个[坐标系](@entry_id:156346)中，[应力张量](@entry_id:148973)的[矩阵表示](@entry_id:146025)是对角的，对角线元素即为主应力值。

#### 示例：[主应力](@entry_id:176761)计算

为了具体说明，我们来计算一个给定应力张量的[主应力](@entry_id:176761)。考虑一个点的应力状态由以下张量描述 ：

$$
\boldsymbol{\sigma}=\begin{pmatrix}
150  -40  0 \\
-40  90  0 \\
0  0  60
\end{pmatrix}\ \text{MPa}
$$

其[特征方程](@entry_id:265849)为 $\det(\boldsymbol{\sigma} - \lambda\boldsymbol{I}) = 0$：
$$
\det\begin{pmatrix}
150-\lambda  -40  0 \\
-40  90-\lambda  0 \\
0  0  60-\lambda
\end{pmatrix} = (60-\lambda) \left[ (150-\lambda)(90-\lambda) - (-40)^2 \right] = 0
$$

这个方程给出一个解 $\lambda_3 = 60$ MPa。另外两个解来自方括号内的二次方程：
$$
\lambda^2 - 240\lambda + 13500 - 1600 = 0 \implies \lambda^2 - 240\lambda + 11900 = 0
$$

使用求根公式，我们得到：
$$
\lambda = \frac{240 \pm \sqrt{240^2 - 4(11900)}}{2} = \frac{240 \pm \sqrt{57600 - 47600}}{2} = \frac{240 \pm 100}{2}
$$

因此，另外两个主应力为 $\lambda_1 = (240+100)/2 = 170$ MPa 和 $\lambda_2 = (240-100)/2 = 70$ MPa。所以，该应力状态的三个主应力为 $\{170, 70, 60\}$ MPa。在与这些[主应力](@entry_id:176761)对应的[主平面](@entry_id:164488)上，面力的大小恰好是这些[主应力](@entry_id:176761)的[绝对值](@entry_id:147688) 。

### 物理意义与不依赖基的性质

主应力和主方向不仅仅是数学上的构造，它们是具有深刻物理意义且不依赖于观测者[坐标系](@entry_id:156346)的客观存在。

考虑一个[坐标系](@entry_id:156346)变换，由正交张量 $\boldsymbol{Q}$ 表示。在新的[坐标系](@entry_id:156346)中，应力张量的分量矩阵变为 $\boldsymbol{\sigma}' = \boldsymbol{Q}\boldsymbol{\sigma}\boldsymbol{Q}^T$。如果 $\boldsymbol{n}$ 是 $\boldsymbol{\sigma}$ 的一个[特征向量](@entry_id:151813)（主方向），其[特征值](@entry_id:154894)为 $\lambda$，即 $\boldsymbol{\sigma}\boldsymbol{n} = \lambda\boldsymbol{n}$，那么在新的[坐标系](@entry_id:156346)中，该方向的矢量表示为 $\boldsymbol{n}' = \boldsymbol{Q}\boldsymbol{n}$。我们来考察 $\boldsymbol{n}'$ 是否是 $\boldsymbol{\sigma}'$ 的[特征向量](@entry_id:151813)：

$$
\boldsymbol{\sigma}'\boldsymbol{n}' = (\boldsymbol{Q}\boldsymbol{\sigma}\boldsymbol{Q}^T)(\boldsymbol{Q}\boldsymbol{n}) = \boldsymbol{Q}\boldsymbol{\sigma}(\boldsymbol{Q}^T\boldsymbol{Q})\boldsymbol{n} = \boldsymbol{Q}(\boldsymbol{\sigma}\boldsymbol{n}) = \boldsymbol{Q}(\lambda\boldsymbol{n}) = \lambda(\boldsymbol{Q}\boldsymbol{n}) = \lambda\boldsymbol{n}'
$$

这个推导表明，$\boldsymbol{n}'$ 确实是 $\boldsymbol{\sigma}'$ 的[特征向量](@entry_id:151813)，并且其 **[特征值](@entry_id:154894) $\lambda$ 保持不变** 。这意味着[主应力](@entry_id:176761)是[标量不变量](@entry_id:193787)，其值不随[坐标系](@entry_id:156346)的旋转而改变。[主方向](@entry_id:276187)作为空间中的一个特定方向，其物理存在也是客观的，只是它在不同[坐标系](@entry_id:156346)下的分量表示会不同。这证实了[主应力与主方向](@entry_id:193792)是应力状态的内在属性，是真正的[物理可观测量](@entry_id:154692)。

#### [应力不变量](@entry_id:170526)

由于主应力是内在属性，任何由主应力组合而成的[对称函数](@entry_id:177113)也必然是坐标[不变量](@entry_id:148850)。[特征方程](@entry_id:265849) $\det(\boldsymbol{\sigma} - \lambda\boldsymbol{I}) = 0$ 可以展开为：
$$
-\lambda^3 + I_1\lambda^2 - I_2\lambda + I_3 = 0
$$
其中系数 $I_1, I_2, I_3$ 被称为 **主[应力[不变](@entry_id:170526)量](@entry_id:148850)** (principal stress invariants)，它们可以表示为主应力的函数：
$$
I_1 = \sigma_1 + \sigma_2 + \sigma_3 = \mathrm{tr}(\boldsymbol{\sigma})
$$
$$
I_2 = \sigma_1\sigma_2 + \sigma_2\sigma_3 + \sigma_3\sigma_1 = \frac{1}{2}[(\mathrm{tr}(\boldsymbol{\sigma}))^2 - \mathrm{tr}(\boldsymbol{\sigma}^2)]
$$
$$
I_3 = \sigma_1\sigma_2\sigma_3 = \det(\boldsymbol{\sigma})
$$
给定一组[不变量](@entry_id:148850) $\{I_1, I_2, I_3\}$，它们唯一地确定了主应力的大小集合 $\{\sigma_1, \sigma_2, \sigma_3\}$（作为特征方程的三个根）。然而，这些[不变量](@entry_id:148850)不包含任何关于[主方向](@entry_id:276187)（即应力张量在空间中方位）的信息。两个具有相同[主应力](@entry_id:176761)但空间方位不同的应力张量，将拥有完全相同的[应力不变量](@entry_id:170526)。这个特性在建立 **各向同性** 材料[本构关系](@entry_id:186508)时至关重要，因为[各向同性材料](@entry_id:170678)的响应不应依赖于载荷方向，因此其能量或[屈服函数](@entry_id:167970)通常仅表示为[应力不变量](@entry_id:170526)的函数 。

### 谱分解与[应力张量](@entry_id:148973)的重构

[主应力与主方向](@entry_id:193792)的几何图像，可以通过 **谱分解** (spectral decomposition) 精确地表达。任何对称的应力张量 $\boldsymbol{\sigma}$ 都可以表示为其[主应力与主方向](@entry_id:193792)投影张量的线性组合：

$$
\boldsymbol{\sigma} = \sum_{i=1}^{3} \sigma_i (\boldsymbol{n}_i \otimes \boldsymbol{n}_i)
$$

其中 $\boldsymbol{n}_i \otimes \boldsymbol{n}_i$ 是主方向 $\boldsymbol{n}_i$ 的[外积](@entry_id:147029)，它是一个投影算子，将任意矢量投影到 $\boldsymbol{n}_i$ 方向上。

在矩阵表示中，这等价于相似对角化。令 $\boldsymbol{\Sigma}$ 为[主应力](@entry_id:176761)构成的[对角矩阵](@entry_id:637782)，$\boldsymbol{N}$ 为主方向（作为列向量）构成的[正交矩阵](@entry_id:169220)：

$$
\boldsymbol{\Sigma} = \begin{pmatrix} \sigma_1  0  0 \\ 0  \sigma_2  0 \\ 0  0  \sigma_3 \end{pmatrix}, \quad \boldsymbol{N} = \begin{pmatrix} \boldsymbol{n}_1  \boldsymbol{n}_2  \boldsymbol{n}_3 \end{pmatrix}
$$

由于 $\boldsymbol{N}$ 是[正交矩阵](@entry_id:169220)，$\boldsymbol{N}^{-1} = \boldsymbol{N}^T$。应力张量 $\boldsymbol{\sigma}$ 在任意[坐标系](@entry_id:156346)下的分量矩阵可以通过下式从其主系统重构：

$$
\boldsymbol{\sigma} = \boldsymbol{N}\boldsymbol{\Sigma}\boldsymbol{N}^T
$$

这个公式清楚地揭示了[应力张量](@entry_id:148973)的内在结构：它由三个内在的大小（主应力）和一组内在的方向（主方向）完全确定 。知道这六个独立的量（三个[主应力](@entry_id:176761)和定义三个正交方向的三个参数，如[欧拉角](@entry_id:171794)），就可以确定[应力张量](@entry_id:148973)的九个分量。

### 特殊情况：[特征值](@entry_id:154894)[重根](@entry_id:151486)

当主应力不完全互异时，[主方向](@entry_id:276187)的唯一性会发生改变。

#### 轴对称应力状态 ($\sigma_1 = \sigma_2 \neq \sigma_3$)

如果两个[主应力](@entry_id:176761)相等，例如 $\sigma_1 = \sigma_2$，则对应于该[重复特征值](@entry_id:154579)的特征空间是一个二维[子空间](@entry_id:150286)，即一个平面。这个平面垂直于与第三个[主应力](@entry_id:176761) $\sigma_3$ 对应的唯一[主方向](@entry_id:276187) $\boldsymbol{n}_3$ 。

在这种情况下，位于该平面内的 **任何** 单位矢量都是一个有效的主方向。因此，[主方向](@entry_id:276187)的选择具有无穷多种可能性，不再唯一（即使不考虑符号）。我们可以选择该平面内的任意一组[正交基](@entry_id:264024) $\{\boldsymbol{n}_1, \boldsymbol{n}_2\}$，它们与 $\boldsymbol{n}_3$ 一起构成一组标准正交的主方向基。无论如何选择这组基，应力张量在该基下的表示都是对角阵 $\mathrm{diag}(\sigma_1, \sigma_1, \sigma_3)$ 。

这种情况的[谱分解](@entry_id:173707)可以更优雅地用投影算子表达。令 $\mathbf{P}$ 为到该二维[特征空间](@entry_id:638014)（[主平面](@entry_id:164488)）的[正交投影](@entry_id:144168)算子，则 $(\mathbf{I}-\mathbf{P})$ 是到其正交补空间（即 $\boldsymbol{n}_3$ 方向）的投影算子。应力张量可以写作：

$$
\boldsymbol{\sigma} = \sigma_1\mathbf{P} + \sigma_3(\mathbf{I}-\mathbf{P})
$$

这清晰地表明，[应力张量](@entry_id:148973)的作用是将矢量分解到[主平面](@entry_id:164488)和其[法线](@entry_id:167651)方向上，并在这两个正交的[子空间](@entry_id:150286)上分别按 $\sigma_1$ 和 $\sigma_3$ 进行缩放 。

#### [静水应力](@entry_id:186327)状态 ($\sigma_1 = \sigma_2 = \sigma_3 = p$)

这是[特征值](@entry_id:154894)[重根](@entry_id:151486)的极致情况，称为 **[静水应力](@entry_id:186327)** (hydrostatic stress) 或球应力状态。此时，[应力张量](@entry_id:148973)可以写成 $\boldsymbol{\sigma} = p\boldsymbol{I}$。

[特征值方程](@entry_id:192306)变为 $p\boldsymbol{I}\boldsymbol{v} = \lambda\boldsymbol{v}$，即 $p\boldsymbol{v} = \lambda\boldsymbol{v}$。唯一的[特征值](@entry_id:154894)是 $\lambda=p$，而这个方程对 **任意** 非[零矢量](@entry_id:155273) $\boldsymbol{v}$ 都成立。这意味着 **空间中的每一个方向都是[主方向](@entry_id:276187)** 。[主方向](@entry_id:276187)的概念在这种情况下失去了其独特性。

由于 $\boldsymbol{\sigma}$ 在任何标准正交基下都表示为对角矩阵 $p\boldsymbol{I}$，可以说它在任何[坐标系](@entry_id:156346)下都已是对角化的。这种应力状态下，所有平面都是[主平面](@entry_id:164488)，任何平面上都没有剪切应力，只有大小为 $p$ 的法向应力。这也意味着最大[剪切应力](@entry_id:137139)为零。其[偏应力张量](@entry_id:267642) $\boldsymbol{s} = \boldsymbol{\sigma} - \frac{1}{3}\mathrm{tr}(\boldsymbol{\sigma})\boldsymbol{I} = p\boldsymbol{I} - \frac{1}{3}(3p)\boldsymbol{I} = \boldsymbol{0}$，因此与形状改变相关的应力分量完全消失 。

### 高级应用：跨界面的主方向不连续性

一个常见但可能产生误解的物理情景是两种不同材料通过一个完美黏合的界面接触。根据[牛顿第三定律](@entry_id:166652)，在没有界面源（如表面张力）的情况下，跨越界面的[面力矢量](@entry_id:189429)必须是连续的。如果界面的法向量为 $\boldsymbol{n}$，则有：

$$
\boldsymbol{t}^-(\boldsymbol{n}) = \boldsymbol{t}^+(\boldsymbol{n}) \quad \implies \quad \boldsymbol{\sigma}^-\boldsymbol{n} = \boldsymbol{\sigma}^+\boldsymbol{n}
$$

其中上标 “-” 和 “+” 分别代表界面两侧的材料。这个条件保证了界面上的[力平衡](@entry_id:267186)。然而，一个重要且微妙的结论是：**面力连续性并不意味着应力张量本身连续，更不意味着[主方向](@entry_id:276187)连续**。

上述连续性条件仅约束了两个[应力张量](@entry_id:148973) $\boldsymbol{\sigma}^-$ 和 $\boldsymbol{\sigma}^+$ 在作用于 **单个** 矢量 $\boldsymbol{n}$ 时产生相同的结果。它没有对这些张量作用于其他任何方向的矢量施加任何约束。而主方向是由整个张量的性质（即其完整的特征结构）决定的。因此，两个完全不同的[应力张量](@entry_id:148973)可以恰好在作用于特定矢量 $\boldsymbol{n}$ 时给出相同的结果，但它们各自的[特征向量](@entry_id:151813)（主方向）却可以完全不同 。

例如，考虑界面法向为 $\boldsymbol{n} = (1, 0)^T$ 的二维情况。假设界面两侧的应力张量分别为：
$$
\boldsymbol{\sigma}^{-} = \begin{pmatrix} 5  2 \\ 2  3 \end{pmatrix} \quad \text{和} \quad \boldsymbol{\sigma}^{+} = \begin{pmatrix} 5  2 \\ 2  10 \end{pmatrix}
$$
两者在界面上的面力均为 $\boldsymbol{t} = (5, 2)^T$，满足连续性条件。然而，计算表明，$\boldsymbol{\sigma}^-$ 的最大[主应力方向](@entry_id:753737)与x轴夹角约为 $31.7^\circ$，而 $\boldsymbol{\sigma}^+$ 的最大[主应力方向](@entry_id:753737)与x轴夹角约为 $70.6^\circ$。这意味着，尽管界面上的力是平滑过渡的，但应[力场](@entry_id:147325)的主要作用方向却在界面上发生了约 $38.9^\circ$ 的突变 。这个例子深刻地揭示了主方向作为[应力张量](@entry_id:148973)“全局”属性与面力作为其在特定平面上“局部”表现之间的区别，对于理解[复合材料](@entry_id:139856)和[异质结构](@entry_id:136451)中的[应力传递](@entry_id:182468)至关重要。