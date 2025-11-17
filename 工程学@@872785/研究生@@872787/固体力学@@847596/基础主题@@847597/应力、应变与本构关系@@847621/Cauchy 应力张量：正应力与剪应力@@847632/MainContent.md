## 引言
在探索物质世界如何响应外力的过程中，一个核心问题是：力如何在物体内部传递和[分布](@entry_id:182848)？无论是桥梁的横梁、飞机的机翼，还是地壳深处的岩石，其内部都存在一个复杂的力的网络。为了从模糊的直觉过渡到精确的科学描述，我们需要一个强大的数学工具。柯西应力张量正是为解决这一问题而生，它为我们提供了一种描述和量化物体内任何一点“应力状态”的通用语言。它的重要性不仅在于其理论的优美，更在于它在整个工程与科学领域的广泛应用。

本文旨在系统性地解决从“力”的概念到“应[力场](@entry_id:147325)”的量化描述这一知识跨越。我们将引导您深入理解柯西应力张量的本质，并掌握其分析方法。文章分为三个核心章节：

在第一章“原理与机制”中，我们将从第一性原理出发，通过动量守恒定律推导出柯西[应力张量](@entry_id:148973)的存在性，并详细阐释其分量（包括[正应力](@entry_id:260622)和剪应力）的物理意义、基本性质（如对称性），以及主应力和[应力分解](@entry_id:272862)等关键概念。

接下来的第二章“应用与交叉学科联系”将理论与实践相连接，展示柯西应力张量如何在结构工程、[材料科学](@entry_id:152226)、[流体力学](@entry_id:136788)等不同领域解决实际问题，例如分析[应力集中](@entry_id:160987)、预测[材料失效](@entry_id:160997)、建立[固液界面](@entry_id:201674)条件等。

最后，在“动手实践”部分，我们提供了一系列精心设计的计算与编程练习，旨在帮助您将理论知识转化为解决具体问题的实践技能，从而真正内化所学内容。

## 原理与机制

在连续介质力学中，理解物体内部的力如何[分布](@entry_id:182848)与传递是核心任务之一。与作用于整个物体体积的**[体力](@entry_id:174230)**（**body force**）（如重力）不同，我们更关注于物体内部因相互作用而产生的**面力**（**surface force**）。这些力通过物体内部的任意假想[截面](@entry_id:154995)进行传递。本章旨在深入阐述描述这种内部力状态的核心数学工具——柯西应力张量，并揭示其基本原理和力学机制。

### 牵[引力](@entry_id:175476)矢量与柯西基本假设

想象在连续体内部取一个点 $\boldsymbol{x}$，并过此点作一个具有特定方向的微小平面。这个平面的方向可以用其[单位法向量](@entry_id:178851) $\boldsymbol{n}$ 来定义。平面一侧的物质会对另一侧的物质施加一个[分布](@entry_id:182848)力。当我们让这个微小平面的面积 $\Delta A$ 趋近于零时，作用在该面上的[合力](@entry_id:163825) $\Delta \boldsymbol{F}$ 与面积之比会趋于一个确定的极限。这个极限被定义为在点 $\boldsymbol{x}$ 处作用于法向为 $\boldsymbol{n}$ 的平面上的**牵[引力](@entry_id:175476)矢量**（**traction vector**），记为 $\boldsymbol{t}(\boldsymbol{n})$。

$$
\boldsymbol{t}(\boldsymbol{n}) = \lim_{\Delta A \to 0} \frac{\Delta \boldsymbol{F}}{\Delta A}
$$

牵[引力](@entry_id:175476)矢量 $\boldsymbol{t}(\boldsymbol{n})$ 的物理意义是单位面积上的[接触力](@entry_id:165079)密度，其量纲为力除以面积。值得注意的是，体力（例如单位质量的体力 $\boldsymbol{b}$，其量纲为加速度）是作用于体积元素的，其对一个区域 $\mathcal{P}$ 的总贡献需要通过对该区域的体积进行积分得到，即 $\int_{\mathcal{P}} \rho \boldsymbol{b} \, \mathrm{d}V$，其中 $\rho$ 是质量密度 [@problem_id:2694331]。

牵[引力](@entry_id:175476)矢量 $\boldsymbol{t}(\boldsymbol{n})$ 自身是一个矢量，它可以被分解为两个相互正交的分量：一个平行于法向量 $\boldsymbol{n}$ 的分量，称为**正向牵[引力](@entry_id:175476)**（**normal traction**）；另一个垂直于[法向量](@entry_id:264185) $\boldsymbol{n}$（即位于平面内）的分量，称为**剪切牵[引力](@entry_id:175476)**（**shear traction**）[@problem_id:2694331]。这一分解对于理解材料的拉伸/压缩和[剪切变形](@entry_id:170920)至关重要。

在建立应力理论时，一个基本出发点是**柯西假设**（**Cauchy's Postulate**）：在给定点，牵[引力](@entry_id:175476)矢量 $\boldsymbol{t}$ 仅依赖于平面的[法向量](@entry_id:264185) $\boldsymbol{n}$，而与该平面的曲率或其他几何形状无关。这一假设极大地简化了问题的数学描述。接下来的核心问题是：牵[引力](@entry_id:175476)矢量 $\boldsymbol{t}(\boldsymbol{n})$ 与[法向量](@entry_id:264185) $\boldsymbol{n}$ 之间究竟存在何种数学关系？

### 柯西应力张量的引入：[动量守恒](@entry_id:149964)的推论

为了揭示 $\boldsymbol{t}(\boldsymbol{n})$ 与 $\boldsymbol{n}$ 之间的关系，我们运用物理学的基本定律——[线性动量守恒](@entry_id:165717)。考虑在点 $\boldsymbol{x}_0$ 附近构建一个极小的四面体，其三个面与[笛卡尔坐标系](@entry_id:169789)的坐标平面平行，第四个斜面的单位外法线为 $\boldsymbol{n}$。这个思想实验被称为**柯西四面体论证**（**Cauchy's tetrahedron argument**）。

对这个微小四面体应用[线性动量守恒](@entry_id:165717)定律的积分形式：
$$
\int_{\partial V} \boldsymbol{t}(\boldsymbol{n},\boldsymbol{x}) \, \mathrm{d}A + \int_V \boldsymbol{b}(\boldsymbol{x}) \, \mathrm{d}V = \int_V \rho(\boldsymbol{x}) \boldsymbol{a}(\boldsymbol{x}) \, \mathrm{d}V
$$
其中左侧第一项是作用在四面体边界上的总面力，第二项是总体积力，右侧是质量与加速度的乘积（[惯性力](@entry_id:169104)）的体积积分。

设四面体的特征尺寸为 $\varepsilon$（例如，从顶点 $\boldsymbol{x}_0$ 到斜面的高）。那么，四面体各个面的面积 $\Delta A$ 与 $\varepsilon^2$ 成正比，而其体积 $V$ 与 $\varepsilon^3$ 成正比。因此，上述方程中的面力积分项的量级为 $O(\varepsilon^2)$，而[体力](@entry_id:174230)积分和[惯性力](@entry_id:169104)积分项的量级均为 $O(\varepsilon^3)$。

当我们让四面体收缩到点 $\boldsymbol{x}_0$（即 $\varepsilon \to 0$）时，体积相关的项（$O(\varepsilon^3)$）将比面积相关的项（$O(\varepsilon^2)$）更快地趋近于零。因此，在极限情况下，方程的平衡由面力项主导。这一尺度分析的结论是，在一点上，所有通过该点的不同方向平面上的牵[引力](@entry_id:175476)必须自身[达到平衡](@entry_id:170346)，而体力与惯性力则成为高阶小量，可以忽略不计 [@problem_id:2694307] [@problem_id:2694365]。

经过推导，这个平衡关系最终表明，牵[引力](@entry_id:175476)矢量 $\boldsymbol{t}(\boldsymbol{n})$ 必须是[法向量](@entry_id:264185) $\boldsymbol{n}$ 的**线性函数**。任何关于 $\boldsymbol{n}$ 的[非线性](@entry_id:637147)项在极限过程中都将消失。既然 $\boldsymbol{t}(\boldsymbol{n})$ 与 $\boldsymbol{n}$ 之间是[线性映射](@entry_id:185132)关系，根据线性代数理论，这个映射可以由一个[二阶张量](@entry_id:199780)来表示。这个张量就是**柯西应力张量**（**Cauchy stress tensor**），记为 $\boldsymbol{\sigma}$。它们之间的关系是[连续介质力学](@entry_id:155125)的基石之一：

$$
\boldsymbol{t}(\boldsymbol{n}) = \boldsymbol{\sigma}\boldsymbol{n}
$$

这个方程表明，在任意一点，只要我们知道了应力张量 $\boldsymbol{\sigma}$，就可以求出作用在任意方向平面上的牵[引力](@entry_id:175476)。$\boldsymbol{\sigma}$ 完全描述了该点的应力状态，它是一个场量，即在物体每个点上都有定义，$\boldsymbol{\sigma} = \boldsymbol{\sigma}(\boldsymbol{x}, t)$。这个张量的存在性和唯一性是[动量守恒](@entry_id:149964)定律的直接推论，它不依赖于我们为推导它而选择的[坐标系](@entry_id:156346)或微元体的具体方向 [@problem_id:2694365]。

### 应力张量的分量、性质与物理诠释

在一个正交[右手坐标系](@entry_id:166669) $\{\boldsymbol{e}_1, \boldsymbol{e}_2, \boldsymbol{e}_3\}$ 中，二阶张量 $\boldsymbol{\sigma}$ 可以表示为一个 $3 \times 3$ 的矩阵，其分量为 $\sigma_{ij}$。这些分量的物理意义可以通过考察作用在坐标平面上的牵[引力](@entry_id:175476)来理解。例如，作用在法向量为 $\boldsymbol{e}_j$ 的平面上的牵[引力](@entry_id:175476)为 $\boldsymbol{t}(\boldsymbol{e}_j) = \boldsymbol{\sigma}\boldsymbol{e}_j$。在分量形式下，这个矢量是 $\sum_i \sigma_{ij} \boldsymbol{e}_i$。

因此，分量 $\sigma_{ij}$ 的物理意义是：**作用在 $j$-平面（[法向量](@entry_id:264185)为 $\boldsymbol{e}_j$ 的平面）上的牵[引力](@entry_id:175476)在 $i$ 方向上的分量** [@problem_id:2616500]。

- **正应力 (Normal Stress)**：当指标 $i$ 和 $j$ 相同时，如 $\sigma_{11}, \sigma_{22}, \sigma_{33}$，它们表示作用在各自坐标平面上的正向牵[引力](@entry_id:175476)分量。习惯上，拉伸为正，压缩为负。
- **剪应力 (Shear Stress)**：当指标 $i$ 和 $j$ 不同时，如 $\sigma_{12}, \sigma_{23}$，它们表示作用在各自坐标平面上的剪切牵[引力](@entry_id:175476)分量。例如，$\sigma_{12}$ 是作用在 2-平面（法向为 $\boldsymbol{e}_2$）上的牵[引力](@entry_id:175476)在 1-方向（$\boldsymbol{e}_1$）上的分量。

**基本性质**

1.  **柯西互易原理 (Cauchy's Reciprocity Principle)**：基于 $\boldsymbol{t}(\boldsymbol{n}) = \boldsymbol{\sigma}\boldsymbol{n}$ 的线性关系，我们可以立即得到 $\boldsymbol{t}(-\boldsymbol{n}) = \boldsymbol{\sigma}(-\boldsymbol{n}) = -(\boldsymbol{\sigma}\boldsymbol{n}) = -\boldsymbol{t}(\boldsymbol{n})$。这表明，在同一位置，作用于一个平面的两个相对侧面上的牵[引力](@entry_id:175476)大小相等、方向相反。这本质上是[牛顿第三定律](@entry_id:166652)在连续体内部[接触力](@entry_id:165079)上的体现 [@problem_id:2694331] [@problem_id:2694318]。

2.  **对称性 (Symmetry)**：在经典（非极性）连续介质理论中，我们假设不存在[体力](@entry_id:174230)矩和面力偶。在此前提下，对一个微元体应用**角动量守恒**定律，可以推导出[应力张量](@entry_id:148973)必须是对称的，即 $\boldsymbol{\sigma} = \boldsymbol{\sigma}^T$，或用分量表示为 $\sigma_{ij} = \sigma_{ji}$。例如，$\sigma_{12} = \sigma_{21}$。这个性质将独立分量的数量从9个减少到6个，极大地简化了理论和计算 [@problem_id:2616500]。值得注意的是，在包含内部旋转自由度的更广义的连续体模型（如[Cosserat介质](@entry_id:747932)）中，应力张量可以是非对称的。

### 任意平面上的[正应力与剪应力](@entry_id:201088)

我们已经知道，在任意平面 $\boldsymbol{n}$ 上的牵[引力](@entry_id:175476)为 $\boldsymbol{t} = \boldsymbol{\sigma}\boldsymbol{n}$。这个牵[引力](@entry_id:175476)可以分解为[正应力](@entry_id:260622)分量和剪应力分量。

作用在该平面上的**[正应力](@entry_id:260622)**（标量），记为 $\sigma_n$，是牵[引力](@entry_id:175476)矢量 $\boldsymbol{t}$ 在法向 $\boldsymbol{n}$ 上的投影：
$$
\sigma_n = \boldsymbol{t} \cdot \boldsymbol{n} = (\boldsymbol{\sigma}\boldsymbol{n}) \cdot \boldsymbol{n}
$$
根据[张量表示法](@entry_id:272140)，这通常写作 $\sigma_n = \boldsymbol{n} \cdot \boldsymbol{\sigma} \cdot \boldsymbol{n}$。如果 $\sigma_n > 0$，表示该平面处于拉伸状态；如果 $\sigma_n  0$，表示处于压缩状态 [@problem_id:2690964]。

牵[引力](@entry_id:175476)矢量 $\boldsymbol{t}$ 中不平行于 $\boldsymbol{n}$ 的部分就是**剪应力矢量** $\boldsymbol{t}_s$：
$$
\boldsymbol{t}_s = \boldsymbol{t} - \sigma_n \boldsymbol{n} = \boldsymbol{\sigma}\boldsymbol{n} - (\boldsymbol{n} \cdot \boldsymbol{\sigma} \cdot \boldsymbol{n})\boldsymbol{n}
$$
由于 $\boldsymbol{t}_s$ 和 $\sigma_n \boldsymbol{n}$ 相互正交，根据勾股定理，它们的模长满足 $|\boldsymbol{t}|^2 = |\sigma_n \boldsymbol{n}|^2 + |\boldsymbol{t}_s|^2 = \sigma_n^2 + \tau_s^2$，其中 $\tau_s = |\boldsymbol{t}_s|$ 是**剪应力的大小**。

我们可以推导出一个不依赖于特定[坐标系](@entry_id:156346)的、计算剪应力大小的优美公式。首先计算 $|\boldsymbol{t}|^2$：
$$
|\boldsymbol{t}|^2 = \boldsymbol{t} \cdot \boldsymbol{t} = (\boldsymbol{\sigma}\boldsymbol{n}) \cdot (\boldsymbol{\sigma}\boldsymbol{n}) = \boldsymbol{n} \cdot \boldsymbol{\sigma}^T \boldsymbol{\sigma} \boldsymbol{n}
$$
利用应力[张量的对称性](@entry_id:202126) $\boldsymbol{\sigma}^T = \boldsymbol{\sigma}$，上式变为 $|\boldsymbol{t}|^2 = \boldsymbol{n} \cdot \boldsymbol{\sigma}^2 \boldsymbol{n}$。因此，剪应力大小的平方为：
$$
\tau_s^2 = |\boldsymbol{t}|^2 - \sigma_n^2 = (\boldsymbol{n} \cdot \boldsymbol{\sigma}^2 \cdot \boldsymbol{n}) - (\boldsymbol{n} \cdot \boldsymbol{\sigma} \cdot \boldsymbol{n})^2
$$
于是，剪应力的大小为 [@problem_id:2694346]：
$$
\tau_s = \sqrt{(\boldsymbol{n} \cdot \boldsymbol{\sigma}^2 \cdot \boldsymbol{n}) - (\boldsymbol{n} \cdot \boldsymbol{\sigma} \cdot \boldsymbol{n})^2}
$$

**计算示例**
考虑某地壳深处的应力状态由以下张量描述（单位：MPa）[@problem_id:2229888]：
$$
\boldsymbol{\sigma} = \begin{pmatrix} -10  4  0 \\ 4  -20  2 \\ 0  2  -15 \end{pmatrix}
$$
我们想要求解作用在法向量方向为 $\vec{v} = \hat{i} + 2\hat{j} + 2\hat{k}$ 的平面上的[正应力](@entry_id:260622)和剪应力大小。首先，将 $\vec{v}$ 单位化得到 $\boldsymbol{n} = \frac{1}{3}(1, 2, 2)^T$。
牵[引力](@entry_id:175476)矢量为：
$$
\boldsymbol{t} = \boldsymbol{\sigma}\boldsymbol{n} = \begin{pmatrix} -10  4  0 \\ 4  -20  2 \\ 0  2  -15 \end{pmatrix} \begin{pmatrix} 1/3 \\ 2/3 \\ 2/3 \end{pmatrix} = \begin{pmatrix} -2/3 \\ -32/3 \\ -26/3 \end{pmatrix} \, \text{MPa}
$$
该平面上的[正应力](@entry_id:260622)为：
$$
\sigma_n = \boldsymbol{t} \cdot \boldsymbol{n} = (-2/3, -32/3, -26/3) \cdot (1/3, 2/3, 2/3) = \frac{-2 - 64 - 52}{9} = -\frac{118}{9} \approx -13.1 \, \text{MPa}
$$
负号表示该平面承受压缩。
剪应力的大小可以通过 $\tau_s^2 = |\boldsymbol{t}|^2 - \sigma_n^2$ 计算：
$$
|\boldsymbol{t}|^2 = (-2/3)^2 + (-32/3)^2 + (-26/3)^2 = \frac{4+1024+676}{9} = \frac{1704}{9}
$$
$$
\tau_s^2 = \frac{1704}{9} - \left(-\frac{118}{9}\right)^2 = \frac{15336 - 13924}{81} = \frac{1412}{81}
$$
$$
\tau_s = \sqrt{\frac{1412}{81}} \approx 4.18 \, \text{MPa}
$$

### [主应力与主方向](@entry_id:193792)

在一点的无数个可能的[截面](@entry_id:154995)中，是否存在一些特殊的[截面](@entry_id:154995)，其上的力完全是法向的，即剪应力为零？答案是肯定的。这些特殊的平面称为**[主平面](@entry_id:164488)**（**principal planes**），其[法线](@entry_id:167651)方向称为**[主方向](@entry_id:276187)**（**principal directions**），作用在[主平面](@entry_id:164488)上的正应力称为**[主应力](@entry_id:176761)**（**principal stresses**）。

在[主平面](@entry_id:164488)上，牵[引力](@entry_id:175476)矢量 $\boldsymbol{t}$ 平行于[法向量](@entry_id:264185) $\boldsymbol{n}$，即 $\boldsymbol{t} = \sigma_p \boldsymbol{n}$，其中 $\sigma_p$ 是一个标量（主应力）。结合柯西公式 $\boldsymbol{t} = \boldsymbol{\sigma}\boldsymbol{n}$，我们得到：
$$
\boldsymbol{\sigma}\boldsymbol{n} = \sigma_p \boldsymbol{n} \quad \text{或} \quad (\boldsymbol{\sigma} - \sigma_p \boldsymbol{I})\boldsymbol{n} = \boldsymbol{0}
$$
这正是一个标准的**[特征值问题](@entry_id:142153)**。主应力是应力张量 $\boldsymbol{\sigma}$ 的[特征值](@entry_id:154894)，[主方向](@entry_id:276187)是对应的[特征向量](@entry_id:151813)。

由于柯西应力张量 $\boldsymbol{\sigma}$ 是一个实对称张量，线性代数理论保证了：
1.  它有三个实数[特征值](@entry_id:154894)（三个[主应力](@entry_id:176761)），记为 $\sigma_1, \sigma_2, \sigma_3$。
2.  它有三组对应的相互正交的[特征向量](@entry_id:151813)（三个[主方向](@entry_id:276187)），记为 $\boldsymbol{n}_1, \boldsymbol{n}_2, \boldsymbol{n}_3$。

在以三个[主方向](@entry_id:276187)为基准的[坐标系](@entry_id:156346)中，应力张量矩阵呈现[对角形式](@entry_id:264850)，对角[线元](@entry_id:196833)素即为三个[主应力](@entry_id:176761)：
$$
\boldsymbol{\sigma}' = \begin{pmatrix} \sigma_1  0  0 \\ 0  \sigma_2  0 \\ 0  0  \sigma_3 \end{pmatrix}
$$
这表明，任何复杂的应力状态都可以通过[坐标旋转](@entry_id:164444)，看作是三个互相垂直方向上的纯拉伸或压缩状[态的叠加](@entry_id:273993)。找到[主应力](@entry_id:176761)对于评估材料强度和预测失效至关重要，因为材料的破坏往往与最大[主应力](@entry_id:176761)或[最大剪应力](@entry_id:181794)有关。

例如，对于应力张量 [@problem_id:2694312]：
$$
\boldsymbol{\sigma}=\begin{pmatrix} 60  20  0\\ 20  30  0\\ 0  0  10 \end{pmatrix} \text{ MPa}
$$
通过求解其[特征值方程](@entry_id:192306) $\det(\boldsymbol{\sigma} - \lambda\boldsymbol{I}) = 0$，我们可以得到三个[主应力](@entry_id:176761)为 $\sigma_1 = 70$ MPa, $\sigma_2 = 20$ MPa, 和 $\sigma_3 = 10$ MPa。求解对应的[特征向量](@entry_id:151813)，我们便能找到三个主方向。在这些[主平面](@entry_id:164488)上，根据定义，剪应力为零。

### [应力张量](@entry_id:148973)的分解：球量与偏量

为了更深刻地理解应力如何引起材料的变形，通常将应力张量分解为两个具有明确物理意义的部分：**球量部分**（**spherical part**）和**偏量部分**（**deviatoric part**）。

$$
\boldsymbol{\sigma} = \boldsymbol{\sigma}_{hyd} + \boldsymbol{s}
$$

**球量[应力张量](@entry_id:148973)** $\boldsymbol{\sigma}_{hyd}$，也称静水压力张量，定义为：
$$
\boldsymbol{\sigma}_{hyd} = p \boldsymbol{I}
$$
其中 $p$ 是**平均正应力**（**mean normal stress**），定义为 $p = \frac{1}{3}\operatorname{tr}(\boldsymbol{\sigma}) = \frac{1}{3}(\sigma_{11} + \sigma_{22} + \sigma_{33})$，$\boldsymbol{I}$ 是单位张量。球量应力在所有方向上都产生大小相等、方向沿法向的牵[引力](@entry_id:175476) ($p\boldsymbol{n}$)，不产生任何剪切作用。它在物理上与物体的**体积改变**（膨胀或收缩）相关联。

**[偏应力张量](@entry_id:267642)** $\boldsymbol{s}$ 定义为总应力减去球量部分：
$$
\boldsymbol{s} = \boldsymbol{\sigma} - p \boldsymbol{I}
$$
[偏应力张量](@entry_id:267642)的一个重要数学特性是其迹为零 ($\operatorname{tr}(\boldsymbol{s}) = 0$)。它代表了总应力中引起物体**形状改变**（畸变或剪切变形）的部分，而不改变其体积。

这种分解的意义重大 [@problem_id:2630210]：
- **[应力功率](@entry_id:182907)的解耦**：单位体积内的[应力功率](@entry_id:182907)（[应力与应变率](@entry_id:263123)张量的[双点积](@entry_id:748648)）可以完美地分解为两部分：$\mathcal{P} = \boldsymbol{\sigma} : \boldsymbol{d} = p \, \operatorname{tr}(\boldsymbol{d}) + \boldsymbol{s} : \operatorname{dev}(\boldsymbol{d})$。第一项是球量应力在[体积应变率](@entry_id:272471)上做的功（体积改变功率），第二项是[偏应力](@entry_id:163323)在形状改变[应变率](@entry_id:154778)上做的功（畸变功率）。两者之间没有交叉项。

- **材料本构关系**：对于[各向同性线弹性](@entry_id:185899)材料，体积响应和形状响应由不同的材料常数控制。体积模量 $K$ 描述了对体积改变的抵抗 ($p = K \epsilon_{vol}$)，而[剪切模量](@entry_id:167228) $G$ 描述了对形状改变的抵抗 ($\boldsymbol{s} = 2G \boldsymbol{\epsilon}_{dev}$)。

- **塑性力学**：对于许多工程材料（如金属），塑性屈服主要由形状改变驱动，而对[静水压力](@entry_id:275365)不敏感。例如，在经典的 von Mises ($J_2$) 塑性理论中，[屈服函数](@entry_id:167970)仅依赖于[偏应力张量](@entry_id:267642) $\boldsymbol{s}$。这意味着，施加一个纯[静水压力](@entry_id:275365)（$\boldsymbol{\sigma} = p\boldsymbol{I}$，此时 $\boldsymbol{s} = \boldsymbol{0}$）并不会使这类材料发生塑性流动。

通过这些原理和机制，柯西[应力张量](@entry_id:148973)不仅提供了一种描述物体内部力的数学语言，更通过其性质和分解，深刻揭示了力与材料变形（体积改变与形状改变）之间的内在联系。