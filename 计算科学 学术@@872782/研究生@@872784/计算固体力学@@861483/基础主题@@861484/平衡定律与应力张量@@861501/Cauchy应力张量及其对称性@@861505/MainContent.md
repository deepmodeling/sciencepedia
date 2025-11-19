## 引言
柯西[应力张量](@entry_id:148973)是[连续介质力学](@entry_id:155125)中描述物体内部受力状态的核心概念。然而，对于初学者而言，其张量形式和内在属性，特别是其对称性，往往显得抽象且难以直观理解。本文旨在系统性地阐明柯西[应力张量](@entry_id:148973)的理论基础及其在现代工程科学中的核心地位，填补理论概念与实际应用之间的知识鸿沟。读者将通过本文学习到，柯西[应力张量](@entry_id:148973)不仅是一个数学工具，更是一个深刻物理原理的体现。在接下来的“原理与机制”章节中，我们将从第一性原理出发，推导[应力张量](@entry_id:148973)的存在性及其对称性的物理根源。随后，“应用与交叉学科联系”章节将展示该理论在[材料失效分析](@entry_id:160408)、计算力学和[广义连续介质理论](@entry_id:193621)中的广泛应用。最后，通过“动手实践”部分的练习，读者将有机会将理论知识应用于具体问题，从而巩固学习成果。

## 原理与机制

本章旨在深入探讨柯西[应力张量](@entry_id:148973)的基本原理与核心机制。我们将从应力的基本定义出发，通过第一性原理推导其存在性，并详细阐述其最为关键的性质——对称性。随后，我们将探讨该对称性带来的一系列重要推论，包括[主应力](@entry_id:176761)、[应力不变量](@entry_id:170526)以及静水/偏[应力分解](@entry_id:272862)等概念。最后，我们将简要介绍这一经典理论在更广阔框架下的位置，例如[大变形理论](@entry_id:188422)和微极连续介质理论，从而为后续章节的学习奠定坚实的理论基础。

### 应力的概念：面力与柯西[应力张量](@entry_id:148973)

在[连续介质力学](@entry_id:155125)中，我们设想将一个物体沿任意假想[截面](@entry_id:154995)切开，其内部相互作用便会显露为[分布](@entry_id:182848)在该[截面](@entry_id:154995)上的接触力。为了将这种[分布](@entry_id:182848)力进行局部化和数学化描述，我们引入**[面力矢量](@entry_id:189429)**（traction vector）的概念。

考虑在当前构型中，位于点 $\mathbf{x}$ 处的一个微小有向表面元，其[单位法向量](@entry_id:178851)为 $\mathbf{n}$，面积为 $\Delta A$。该表面一侧的物质对另一侧物质施加的接触力合力为 $\Delta \mathbf{F}$。[面力矢量](@entry_id:189429) $\mathbf{t}(\mathbf{n}; \mathbf{x}, t)$ 定义为该[接触力](@entry_id:165079)与面积之比在面积趋于零时的极限 [@problem_id:3548562]：
$$
\mathbf{t}(\mathbf{n}; \mathbf{x}, t) = \lim_{\Delta A \to 0} \frac{\Delta \mathbf{F}}{\Delta A}
$$
这一定义表明，面力是一种面力密度，其值不仅取决于空间位置 $\mathbf{x}$ 和时间 $t$，还依赖于[截面](@entry_id:154995)的方向 $\mathbf{n}$。根据牛顿第三定律（作用力与[反作用](@entry_id:203910)力定律），作用在法向量为 $-\mathbf{n}$ 的[截面](@entry_id:154995)上的面力，与作用在[法向量](@entry_id:264185)为 $\mathbf{n}$ 的[截面](@entry_id:154995)上的面力大小相等、方向相反。这被称为**柯西引理**（Cauchy's Lemma）：
$$
\mathbf{t}(-\mathbf{n}) = -\mathbf{t}(\mathbf{n})
$$

一个自然的问题是：在同一点，不同方向[截面](@entry_id:154995)上的[面力矢量](@entry_id:189429)之间是否存在某种内在联系？法国数学家 Augustin-Louis Cauchy 通过一个精妙的思维实验回答了这个问题。考虑一个以点 $\mathbf{x}$ 为顶点的无限小四面体，其三个正交表面分别垂直于坐标轴，法向量为 $-\mathbf{e}_1, -\mathbf{e}_2, -\mathbf{e}_3$，斜[面法向量](@entry_id:749211)为 $\mathbf{n}$。对该四面体应用线动量[守恒定律](@entry_id:269268)（[牛顿第二定律](@entry_id:274217)），即所有外力之和等于质量乘以加速度。这些外力包括作用在四个面上的面力以及作用在整个体积上的体力。

当四面体的尺寸趋近于零时，可以证明，体力、惯性力等体量（与体积 $h^3$ 成正比）相比于面力（与面积 $h^2$ 成正比）将成为高阶小量而可以忽略。最终，线[动量守恒](@entry_id:149964)的要求简化为一个纯粹的代数关系，即斜面上的[面力矢量](@entry_id:189429)可以由三个坐标面上的[面力矢量](@entry_id:189429)[线性表示](@entry_id:139970)。这一结论被称为**柯西应力定理**（Cauchy's Stress Theorem），它揭示了面力 $\mathbf{t}(\mathbf{n})$ 与[法向量](@entry_id:264185) $\mathbf{n}$ 之间存在[线性关系](@entry_id:267880)。

这种[线性关系](@entry_id:267880)可以通过一个二阶张量来描述，我们称之为**柯西[应力张量](@entry_id:148973)**（Cauchy stress tensor），记作 $\boldsymbol{\sigma}$。该关系式为：
$$
\mathbf{t}(\mathbf{n}) = \boldsymbol{\sigma} \mathbf{n}
$$
在分量形式下，可写作 $t_i = \sum_{j=1}^3 \sigma_{ij} n_j$。柯西[应力张量](@entry_id:148973) $\boldsymbol{\sigma}(\mathbf{x}, t)$ 是描述材料内部某一点应力状态的根本物理量。它在给定点是一个不依赖于[截面](@entry_id:154995)方向 $\mathbf{n}$ 的线性映射算子，而[面力矢量](@entry_id:189429) $\mathbf{t}$ 则是该算子作用于特定方向 $\mathbf{n}$ 的结果。$\boldsymbol{\sigma}$ 的第 $j$ 列向量正是作用在[法向量](@entry_id:264185)为 $\mathbf{e}_j$ 的坐标面上的[面力矢量](@entry_id:189429) $\mathbf{t}(\mathbf{e}_j)$。

### 柯西应力[张量的对称性](@entry_id:202126)

柯西应力张量最重要、最基本的性质之一是其**对称性**，即 $\boldsymbol{\sigma} = \boldsymbol{\sigma}^{\mathsf{T}}$，或写作 $\sigma_{ij} = \sigma_{ji}$。这一性质并非源于材料的[本构关系](@entry_id:186508)（如各向同性），而是一个更为根本的、由物理学基本定律——**[角动量守恒](@entry_id:156798)**——所决定的普适原理 [@problem_id:2616464]。

为了理解这一点，我们考虑一个围绕点 $\mathbf{x}$ 的微小立方体单元。根据[角动量守恒](@entry_id:156798)定律，作用在该单元上的所有外力矩之和必须等于其角动量的变化率。在**经典柯西连续介质**的框架下，我们做出一个关键假设：不存在[分布](@entry_id:182848)式的**[体力](@entry_id:174230)矩**（body couples）和**[力偶应力](@entry_id:747952)**（couple stresses），即物质微元之间只通过力来传递相互作用，而不直接传递力偶或力矩 [@problem_id:3548580]。

在此假设下，作用在微小立方体上的总力矩仅来源于表面面力和体积力的力矩。通过对立方体各表面上的面力（由[应力张量](@entry_id:148973)分量表示）进行力矩分析，可以发现，由应力[张量的反对称部分](@entry_id:193562)（例如 $\sigma_{12} - \sigma_{21}$）产生的力矩是最低阶的[主导项](@entry_id:167418)（量级为 $\epsilon^3$，其中 $\epsilon$ 是立方体边长）。而体力矩和[惯性力](@entry_id:169104)矩等项则是更高阶的小量（例如 $\epsilon^4$ 或 $\epsilon^5$）。为了在 $\epsilon \to 0$ 的极限下依然满足[角动量守恒](@entry_id:156798)，唯一的可能性就是[应力张量](@entry_id:148973)反对称部分产生的[净力矩](@entry_id:166772)必须为零。这直接要求：
$$
\sigma_{ij} = \sigma_{ji}
$$
因此，柯西应力[张量的对称性](@entry_id:202126)是[角动量守恒](@entry_id:156798)定律在无内部力偶作用的经典连续介质中的直接体现 [@problem_id:3548562]。

必须强调，这一结论不依赖于线动量守恒方程 $\nabla \cdot \boldsymbol{\sigma} + \mathbf{b} = \rho \mathbf{a}$，该方程本身并未对 $\boldsymbol{\sigma}$ 的对称性施加任何约束。同时，对称性也与材料是否为各向同性无关，它对[各向异性材料](@entry_id:184874)同样成立。

### 对称性的推论与表示

应力[张量的对称性](@entry_id:202126)极大地简化了[应力分析](@entry_id:168804)，并引出了一系列重要的概念和工具。

#### 分量简化与Voigt记法

一个普适的二阶三维张量有 $3 \times 3 = 9$ 个独立分量。对称性条件 $\sigma_{ij} = \sigma_{ji}$ 提供了三个独立的约束方程（$\sigma_{12}=\sigma_{21}, \sigma_{13}=\sigma_{31}, \sigma_{23}=\sigma_{32}$），从而将柯西应力张量的独立分量数量从9个减少到6个。这6个独立分量是3个正应力（$\sigma_{11}, \sigma_{22}, \sigma_{33}$）和3个剪应力（$\sigma_{12}, \sigma_{13}, \sigma_{23}$）。

在[计算固体力学](@entry_id:169583)中，为了方便存储和进行矩阵运算，通常将这6个独立分量[排列](@entry_id:136432)成一个6维列向量，这种表示方法称为**Voigt记法**（Voigt notation）。一个标准的Voigt应力向量形式为 [@problem_id:3548563]：
$$
\boldsymbol{\sigma}_{\text{Voigt}} = \begin{pmatrix} \sigma_{11}  \sigma_{22}  \sigma_{33}  \sigma_{23}  \sigma_{13}  \sigma_{12} \end{pmatrix}^{\mathsf{T}}
$$
这种记法广泛应用于有限元软件的[本构关系](@entry_id:186508)计算中。

#### [主应力与主方向](@entry_id:193792)

由于柯西[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ 是对称的，根据线性代数理论，它保证具有三个实数[特征值](@entry_id:154894)和一组相互正交的[特征向量](@entry_id:151813)。在力学中，这些[特征值](@entry_id:154894)和[特征向量](@entry_id:151813)具有明确的物理意义。

*   **主应力**（Principal stresses）是[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ 的三个[特征值](@entry_id:154894)，通常记为 $\sigma_1, \sigma_2, \sigma_3$。
*   **主方向**（Principal directions）是与[主应力](@entry_id:176761)对应的[特征向量](@entry_id:151813)，记为 $\mathbf{n}_1, \mathbf{n}_2, \mathbf{n}_3$。

[特征值问题](@entry_id:142153)可写为 $\boldsymbol{\sigma} \mathbf{n}_i = \sigma_i \mathbf{n}_i$。结合面力定义 $\mathbf{t}(\mathbf{n}) = \boldsymbol{\sigma} \mathbf{n}$，我们得到 $\mathbf{t}(\mathbf{n}_i) = \sigma_i \mathbf{n}_i$。这表明，在以主方向为法线的平面（称为**[主平面](@entry_id:164488)**）上，[面力矢量](@entry_id:189429)与[法向量](@entry_id:264185)共线，即该平面上的**[剪切应力](@entry_id:137139)为零**，只有[法向应力](@entry_id:260622)，其大小就是对应的主应力 [@problem_id:3548600]。

[主应力](@entry_id:176761)代表了某一点应力状态的[极值](@entry_id:145933)特性。通过求解一个[约束优化](@entry_id:635027)问题，可以证明，作用在所有可能方向[截面](@entry_id:154995)上的**[法向应力](@entry_id:260622)** $p(\mathbf{n}) = \mathbf{n} \cdot \mathbf{t}(\mathbf{n}) = \mathbf{n}^{\mathsf{T}} \boldsymbol{\sigma} \mathbf{n}$ 的所有驻值（极大值、极小值和[鞍点](@entry_id:142576)值）恰好就是三个[主应力](@entry_id:176761) [@problem_id:3548600]。最大和最小[主应力](@entry_id:176761)分别代表了该点所能承受的最大和最小法向拉伸（或压缩）应力。

例如，对于一个给定的应力状态 [@problem_id:3548600]：
$$
\boldsymbol{\sigma} = \begin{pmatrix} 120  30  0 \\ 30  80  0 \\ 0  0  50 \end{pmatrix} \text{ MPa}
$$
通过求解其[特征值问题](@entry_id:142153)，可得三个[主应力](@entry_id:176761)约为 $\sigma_1 \approx 136.06 \text{ MPa}$，$\sigma_2 \approx 63.94 \text{ MPa}$，以及 $\sigma_3 = 50 \text{ MPa}$。这意味着通过该点的所有平面中，最大的法向拉应力是 $136.06 \text{ MPa}$，最小的法向应力是 $50 \text{ MPa}$。

### [应力张量](@entry_id:148973)的客观性与[不变量](@entry_id:148850)

#### 坐标变换与客观性

柯西应力张量描述的是一个物理状态，它不应随观察者[坐标系](@entry_id:156346)的选择而改变。若两个[坐标系](@entry_id:156346)通过一个正交变换矩阵 $\mathbf{Q}$ 相关联，即新[坐标系](@entry_id:156346)中的矢量 $\mathbf{x}' = \mathbf{Q} \mathbf{x}$，则应力张量在新[坐标系](@entry_id:156346)下的分量 $\boldsymbol{\sigma}'$ 与旧[坐标系](@entry_id:156346)下的分量 $\boldsymbol{\sigma}$ 满足以下变换关系 [@problem_id:3548543]：
$$
\boldsymbol{\sigma}' = \mathbf{Q} \boldsymbol{\sigma} \mathbf{Q}^{\mathsf{T}}
$$
这一关系确保了物理定律（如 $\mathbf{t} = \boldsymbol{\sigma} \mathbf{n}$）在不同[坐标系](@entry_id:156346)下形式不变，是张量**客观性**（objectivity）或物质标架无关性（material frame indifference）的体现 [@problem_id:3548610]。

一个重要的推论是，对称性是客观属性。如果 $\boldsymbol{\sigma}$ 是对称的（$\boldsymbol{\sigma} = \boldsymbol{\sigma}^{\mathsf{T}}$），那么其变换后的形式 $\boldsymbol{\sigma}'$ 也必然是对称的：
$$
(\boldsymbol{\sigma}')^{\mathsf{T}} = (\mathbf{Q} \boldsymbol{\sigma} \mathbf{Q}^{\mathsf{T}})^{\mathsf{T}} = (\mathbf{Q}^{\mathsf{T}})^{\mathsf{T}} \boldsymbol{\sigma}^{\mathsf{T}} \mathbf{Q}^{\mathsf{T}} = \mathbf{Q} \boldsymbol{\sigma} \mathbf{Q}^{\mathsf{T}} = \boldsymbol{\sigma}'
$$
这意味着，一个对称的应力状态在任何[旋转坐标系](@entry_id:170324)下观察，都将是还对称的 [@problem_id:3548543]。

#### [应力不变量](@entry_id:170526)与静水/偏[应力分解](@entry_id:272862)

尽管[应力张量](@entry_id:148973)的分量会随[坐标系](@entry_id:156346)的旋转而改变，但某些由分量组合而成的标量值却保持不变，这些量被称为**[应力不变量](@entry_id:170526)**（stress invariants）。对于一个三维对称应力张量，存在三个独立的[主不变量](@entry_id:193522)，它们可以通过[主应力](@entry_id:176761) $\sigma_1, \sigma_2, \sigma_3$ 表示：
$$
\begin{align*}
I_1 = \sigma_1 + \sigma_2 + \sigma_3 \\
I_2 = \sigma_1\sigma_2 + \sigma_2\sigma_3 + \sigma_3\sigma_1 \\
I_3 = \sigma_1\sigma_2\sigma_3
\end{align*}
$$
这些[不变量](@entry_id:148850)也可以直接通过任意[坐标系](@entry_id:156346)下的应力分量计算得到 [@problem_id:3548594]：
$$
\begin{align*}
I_1 = \operatorname{tr}(\boldsymbol{\sigma}) \\
I_2 = \frac{1}{2} \left[ (\operatorname{tr}\boldsymbol{\sigma})^2 - \operatorname{tr}(\boldsymbol{\sigma}^2) \right] \\
I_3 = \det(\boldsymbol{\sigma})
\end{align*}
$$
其中 $\operatorname{tr}(\cdot)$ 表示迹，$\det(\cdot)$ 表示[行列式](@entry_id:142978)。

为了更好地理解应力的物理效应，通常将其分解为两部分：引起体积变化的**[静水应力](@entry_id:186327)**（hydrostatic stress）[部分和](@entry_id:162077)引起形状变化的**[偏应力](@entry_id:163323)**（deviatoric stress）部分。

**静水压力**（hydrostatic pressure）定义为三个[正应力](@entry_id:260622)平均值的相反数：
$$
p = -\frac{1}{3}(\sigma_{11} + \sigma_{22} + \sigma_{33}) = -\frac{1}{3} I_1
$$
[静水应力](@entry_id:186327)张量（或球量张量）是一个对所有方向都施加相同法向应力的纯球形张量，即 $\boldsymbol{\sigma}_{\text{hydro}} = -p \mathbf{I}$，其中 $\mathbf{I}$ 是单位张量。

**[偏应力张量](@entry_id:267642)** $\mathbf{s}$ 则定义为总应力减去[静水应力](@entry_id:186327)部分：
$$
\mathbf{s} = \boldsymbol{\sigma} - \boldsymbol{\sigma}_{\text{hydro}} = \boldsymbol{\sigma} + p\mathbf{I}
$$
根据其定义，[偏应力张量](@entry_id:267642)是**无迹的**（$\operatorname{tr}(\mathbf{s}) = 0$）。由于 $\boldsymbol{\sigma}$ 和 $\mathbf{I}$ 都是对称的，$\mathbf{s}$ 也是一个对称张量。[偏应力张量](@entry_id:267642)描述了应力状态中导致材料[剪切变形](@entry_id:170920)或扭曲的部分。它的[不变量](@entry_id:148850)，特别是第二偏[应力[不变](@entry_id:170526)量](@entry_id:148850) $J_2 = \frac{1}{2} \operatorname{tr}(\mathbf{s}^2)$，在塑性力学（如[von Mises屈服准则](@entry_id:174339)）中扮演着核心角色 [@problem_id:3548594]。

值得注意的是，由于[偏应力张量](@entry_id:267642)只是在柯西应力张量的基础上减去一个单位张量的标量倍，两者是**共轴的**，即它们共享相同的[主方向](@entry_id:276187) [@problem_id:3548594]。

### 经典连续介质理论的拓展

本章所讨论的柯西应力及其对称性构成了经典连续介质力学的基石。然而，在处理更复杂问题时，这些概念也需要被审视和拓展。

#### 大变形中的应力测度

当物体经历[大变形](@entry_id:167243)时，区分**参考构型**（变形前）和**当前构型**（变形后）变得至关重要。柯西应力是定义在当前构型上的“真实”应力。在理论和计算中，还引入了其他应力测度，它们将力与参考构型联系起来。最重要的两种是：

1.  **第一Piola-Kirchhoff (PK1) 应力张量** ($\mathbf{P}$): 将当前构型中的力与参考构型中的[面积元](@entry_id:263205)联系起来。
2.  **第二Piola-Kirchhoff (PK2) [应力张量](@entry_id:148973)** ($\mathbf{S}$): 将一个虚拟的、映射回参考构型的力与参考构型中的[面积元](@entry_id:263205)联系起来。

这些应力张量通过变形梯度 $\mathbf{F}$ 与柯西应力 $\boldsymbol{\sigma}$ 相关联。重要的对称性结论是：如果柯西应力 $\boldsymbol{\sigma}$ 是对称的，那么第二PK应力 $\mathbf{S}$ 也是对称的。然而，第一PK应力 $\mathbf{P}$ 在一般情况下**不是对称的** [@problem_id:3548619]。这一特性对建立大变形问题的控制方程和[数值算法](@entry_id:752770)具有深远影响。

#### 超越经典：微极连续介质

柯西应力[张量的对称性](@entry_id:202126)源于一个关键假设：物质微元间不存在直接的力矩传递。然而，对于某些具有显著微观结构的材料，如[颗粒材料](@entry_id:750005)、[复合材料](@entry_id:139856)或泡沫材料，这种假设可能不成立。

**微极（或Cosserat）连续介质理论**通过引入独立的**微转动**自由度 $\boldsymbol{\varphi}$ 和与之共轭的**[力偶应力](@entry_id:747952)张量** $\boldsymbol{\mu}$ 来描述这类材料的行为 [@problem_id:3548581]。在此推广的理论框架下，[角动量守恒](@entry_id:156798)定律的形式变为 [@problem_id:3548580]：
$$
\boldsymbol{\varepsilon}:\boldsymbol{\sigma} + \operatorname{div}\boldsymbol{\mu} + \mathbf{c} = \rho \mathbf{J} \ddot{\boldsymbol{\varphi}}
$$
其中 $\boldsymbol{\varepsilon}:\boldsymbol{\sigma}$ 是与 $\boldsymbol{\sigma}$ 的反对称部分相关的[轴矢量](@entry_id:196296)，$\mathbf{c}$ 是体力偶密度，$\rho \mathbf{J} \ddot{\boldsymbol{\varphi}}$ 是微转动惯性项。

这个方程的意义非凡：它表明柯西[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ 的反对称部分不再必须为零，而是与力偶[应力的散度](@entry_id:185633)、[体力](@entry_id:174230)偶以及微[惯性力](@entry_id:169104)矩[相平衡](@entry_id:136822) [@problem_id:2616464] [@problem_id:3548610]。这不仅为描述更复杂的材料行为提供了理论工具，也从反面深刻地揭示了经典理论中[应力对称性](@entry_id:181689)所依赖的物理前提。