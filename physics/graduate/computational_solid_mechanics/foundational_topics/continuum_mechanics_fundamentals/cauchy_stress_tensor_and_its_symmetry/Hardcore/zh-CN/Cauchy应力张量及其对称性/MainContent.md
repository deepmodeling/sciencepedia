## 引言
柯西应力张量是连续介质力学中描述物体内部受力状态的核心概念。然而，对于初学者而言，其张量形式和内在属性，特别是其对称性，往往显得抽象且难以直观理解。本文旨在系统性地阐明柯西应力张量的理论基础及其在现代工程科学中的核心地位，填补理论概念与实际应用之间的知识鸿沟。读者将通过本文学习到，柯西应力张量不仅是一个数学工具，更是一个深刻物理原理的体现。在接下来的“原理与机制”章节中，我们将从第一性原理出发，推导应力张量的存在性及其对称性的物理根源。随后，“应用与交叉学科联系”章节将展示该理论在材料失效分析、计算力学和广义连续介质理论中的广泛应用。最后，通过“动手实践”部分的练习，读者将有机会将理论知识应用于具体问题，从而巩固学习成果。

## 原理与机制

本章旨在深入探讨柯西应力张量的基本原理与核心机制。我们将从应力的基本定义出发，通过第一性原理推导其存在性，并详细阐述其最为关键的性质——对称性。随后，我们将探讨该对称性带来的一系列重要推论，包括主应力、应力不变量以及静水/偏应力分解等概念。最后，我们将简要介绍这一经典理论在更广阔框架下的位置，例如大变形理论和微极连续介质理论，从而为后续章节的学习奠定坚实的理论基础。

### 应力的概念：面力与柯西应力张量

在连续介质力学中，我们设想将一个物体沿任意假想截面切开，其内部相互作用便会显露为分布在该截面上的接触力。为了将这种分布力进行局部化和数学化描述，我们引入**面力矢量**（traction vector）的概念。

考虑在当前构型中，位于点 $\mathbf{x}$ 处的一个微小有向表面元，其单位法向量为 $\mathbf{n}$，面积为 $\Delta A$。该表面一侧的物质对另一侧物质施加的接触力合力为 $\Delta \mathbf{F}$。面力矢量 $\mathbf{t}(\mathbf{n}; \mathbf{x}, t)$ 定义为该接触力与面积之比在面积趋于零时的极限 [@problem_id:3548562]：
$$
\mathbf{t}(\mathbf{n}; \mathbf{x}, t) = \lim_{\Delta A \to 0} \frac{\Delta \mathbf{F}}{\Delta A}
$$
这一定义表明，面力是一种面力密度，其值不仅取决于空间位置 $\mathbf{x}$ 和时间 $t$，还依赖于截面的方向 $\mathbf{n}$。根据牛顿第三定律（作用力与反作用力定律），作用在法向量为 $-\mathbf{n}$ 的截面上的面力，与作用在法向量为 $\mathbf{n}$ 的截面上的面力大小相等、方向相反。这被称为**柯西引理**（Cauchy's Lemma）：
$$
\mathbf{t}(-\mathbf{n}) = -\mathbf{t}(\mathbf{n})
$$

一个自然的问题是：在同一点，不同方向截面上的面力矢量之间是否存在某种内在联系？法国数学家 Augustin-Louis Cauchy 通过一个精妙的思维实验回答了这个问题。考虑一个以点 $\mathbf{x}$ 为顶点的无限小四面体，其三个正交表面分别垂直于坐标轴，法向量为 $-\mathbf{e}_1, -\mathbf{e}_2, -\mathbf{e}_3$，斜面法向量为 $\mathbf{n}$。对该四面体应用线动量守恒定律（牛顿第二定律），即所有外力之和等于质量乘以加速度。这些外力包括作用在四个面上的面力以及作用在整个体积上的体力。

当四面体的尺寸趋近于零时，可以证明，体力、惯性力等体量（与体积 $h^3$ 成正比）相比于面力（与面积 $h^2$ 成正比）将成为高阶小量而可以忽略。最终，线动量守恒的要求简化为一个纯粹的代数关系，即斜面上的面力矢量可以由三个坐标面上的面力矢量线性表示。这一结论被称为**柯西应力定理**（Cauchy's Stress Theorem），它揭示了面力 $\mathbf{t}(\mathbf{n})$ 与法向量 $\mathbf{n}$ 之间存在线性关系。

这种线性关系可以通过一个二阶张量来描述，我们称之为**柯西应力张量**（Cauchy stress tensor），记作 $\boldsymbol{\sigma}$。该关系式为：
$$
\mathbf{t}(\mathbf{n}) = \boldsymbol{\sigma} \mathbf{n}
$$
在分量形式下，可写作 $t_i = \sum_{j=1}^3 \sigma_{ij} n_j$。柯西应力张量 $\boldsymbol{\sigma}(\mathbf{x}, t)$ 是描述材料内部某一点应力状态的根本物理量。它在给定点是一个不依赖于截面方向 $\mathbf{n}$ 的线性映射算子，而面力矢量 $\mathbf{t}$ 则是该算子作用于特定方向 $\mathbf{n}$ 的结果。$\boldsymbol{\sigma}$ 的第 $j$ 列向量正是作用在法向量为 $\mathbf{e}_j$ 的坐标面上的面力矢量 $\mathbf{t}(\mathbf{e}_j)$。

### 柯西应力张量的对称性

柯西应力张量最重要、最基本的性质之一是其**对称性**，即 $\boldsymbol{\sigma} = \boldsymbol{\sigma}^{\mathsf{T}}$，或写作 $\sigma_{ij} = \sigma_{ji}$。这一性质并非源于材料的本构关系（如各向同性），而是一个更为根本的、由物理学基本定律——**角动量守恒**——所决定的普适原理 [@problem_id:2616464]。

为了理解这一点，我们考虑一个围绕点 $\mathbf{x}$ 的微小立方体单元。根据角动量守恒定律，作用在该单元上的所有外力矩之和必须等于其角动量的变化率。在**经典柯西连续介质**的框架下，我们做出一个关键假设：不存在分布式的**体力矩**（body couples）和**力偶应力**（couple stresses），即物质微元之间只通过力来传递相互作用，而不直接传递力偶或力矩 [@problem_id:3548580]。

在此假设下，作用在微小立方体上的总力矩仅来源于表面面力和体积力的力矩。通过对立方体各表面上的面力（由应力张量分量表示）进行力矩分析，可以发现，由应力张量的反对称部分（例如 $\sigma_{12} - \sigma_{21}$）产生的力矩是最低阶的主导项（量级为 $\epsilon^3$，其中 $\epsilon$ 是立方体边长）。而体力矩和惯性力矩等项则是更高阶的小量（例如 $\epsilon^4$ 或 $\epsilon^5$）。为了在 $\epsilon \to 0$ 的极限下依然满足角动量守恒，唯一的可能性就是应力张量反对称部分产生的净力矩必须为零。这直接要求：
$$
\sigma_{ij} = \sigma_{ji}
$$
因此，柯西应力张量的对称性是角动量守恒定律在无内部力偶作用的经典连续介质中的直接体现 [@problem_id:3548562]。

必须强调，这一结论不依赖于线动量守恒方程 $\nabla \cdot \boldsymbol{\sigma} + \mathbf{b} = \rho \mathbf{a}$，该方程本身并未对 $\boldsymbol{\sigma}$ 的对称性施加任何约束。同时，对称性也与材料是否为各向同性无关，它对各向异性材料同样成立。

### 对称性的推论与表示

应力张量的对称性极大地简化了应力分析，并引出了一系列重要的概念和工具。

#### 分量简化与Voigt记法

一个普适的二阶三维张量有 $3 \times 3 = 9$ 个独立分量。对称性条件 $\sigma_{ij} = \sigma_{ji}$ 提供了三个独立的约束方程（$\sigma_{12}=\sigma_{21}, \sigma_{13}=\sigma_{31}, \sigma_{23}=\sigma_{32}$），从而将柯西应力张量的独立分量数量从9个减少到6个。这6个独立分量是3个正应力（$\sigma_{11}, \sigma_{22}, \sigma_{33}$）和3个剪应力（$\sigma_{12}, \sigma_{13}, \sigma_{23}$）。

在计算固体力学中，为了方便存储和进行矩阵运算，通常将这6个独立分量排列成一个6维列向量，这种表示方法称为**Voigt记法**（Voigt notation）。一个标准的Voigt应力向量形式为 [@problem_id:3548563]：
$$
\boldsymbol{\sigma}_{\text{Voigt}} = \begin{pmatrix} \sigma_{11}  \sigma_{22}  \sigma_{33}  \sigma_{23}  \sigma_{13}  \sigma_{12} \end{pmatrix}^{\mathsf{T}}
$$
这种记法广泛应用于有限元软件的本构关系计算中。

#### 主应力与主方向

由于柯西应力张量 $\boldsymbol{\sigma}$ 是对称的，根据线性代数理论，它保证具有三个实数特征值和一组相互正交的特征向量。在力学中，这些特征值和特征向量具有明确的物理意义。

*   **主应力**（Principal stresses）是应力张量 $\boldsymbol{\sigma}$ 的三个特征值，通常记为 $\sigma_1, \sigma_2, \sigma_3$。
*   **主方向**（Principal directions）是与主应力对应的特征向量，记为 $\mathbf{n}_1, \mathbf{n}_2, \mathbf{n}_3$。

特征值问题可写为 $\boldsymbol{\sigma} \mathbf{n}_i = \sigma_i \mathbf{n}_i$。结合面力定义 $\mathbf{t}(\mathbf{n}) = \boldsymbol{\sigma} \mathbf{n}$，我们得到 $\mathbf{t}(\mathbf{n}_i) = \sigma_i \mathbf{n}_i$。这表明，在以主方向为法线的平面（称为**主平面**）上，面力矢量与法向量共线，即该平面上的**剪切应力为零**，只有法向应力，其大小就是对应的主应力 [@problem_id:3548600]。

主应力代表了某一点应力状态的极值特性。通过求解一个约束优化问题，可以证明，作用在所有可能方向截面上的**法向应力** $p(\mathbf{n}) = \mathbf{n} \cdot \mathbf{t}(\mathbf{n}) = \mathbf{n}^{\mathsf{T}} \boldsymbol{\sigma} \mathbf{n}$ 的所有驻值（极大值、极小值和鞍点值）恰好就是三个主应力 [@problem_id:3548600]。最大和最小主应力分别代表了该点所能承受的最大和最小法向拉伸（或压缩）应力。

例如，对于一个给定的应力状态 [@problem_id:3548600]：
$$
\boldsymbol{\sigma} = \begin{pmatrix} 120  30  0 \\ 30  80  0 \\ 0  0  50 \end{pmatrix} \text{ MPa}
$$
通过求解其特征值问题，可得三个主应力约为 $\sigma_1 \approx 136.06 \text{ MPa}$，$\sigma_2 \approx 63.94 \text{ MPa}$，以及 $\sigma_3 = 50 \text{ MPa}$。这意味着通过该点的所有平面中，最大的法向拉应力是 $136.06 \text{ MPa}$，最小的法向应力是 $50 \text{ MPa}$。

### 应力张量的客观性与不变量

#### 坐标变换与客观性

柯西应力张量描述的是一个物理状态，它不应随观察者坐标系的选择而改变。若两个坐标系通过一个正交变换矩阵 $\mathbf{Q}$ 相关联，即新坐标系中的矢量 $\mathbf{x}' = \mathbf{Q} \mathbf{x}$，则应力张量在新坐标系下的分量 $\boldsymbol{\sigma}'$ 与旧坐标系下的分量 $\boldsymbol{\sigma}$ 满足以下变换关系 [@problem_id:3548543]：
$$
\boldsymbol{\sigma}' = \mathbf{Q} \boldsymbol{\sigma} \mathbf{Q}^{\mathsf{T}}
$$
这一关系确保了物理定律（如 $\mathbf{t} = \boldsymbol{\sigma} \mathbf{n}$）在不同坐标系下形式不变，是张量**客观性**（objectivity）或物质标架无关性（material frame indifference）的体现 [@problem_id:3548610]。

一个重要的推论是，对称性是客观属性。如果 $\boldsymbol{\sigma}$ 是对称的（$\boldsymbol{\sigma} = \boldsymbol{\sigma}^{\mathsf{T}}$），那么其变换后的形式 $\boldsymbol{\sigma}'$ 也必然是对称的：
$$
(\boldsymbol{\sigma}')^{\mathsf{T}} = (\mathbf{Q} \boldsymbol{\sigma} \mathbf{Q}^{\mathsf{T}})^{\mathsf{T}} = (\mathbf{Q}^{\mathsf{T}})^{\mathsf{T}} \boldsymbol{\sigma}^{\mathsf{T}} \mathbf{Q}^{\mathsf{T}} = \mathbf{Q} \boldsymbol{\sigma} \mathbf{Q}^{\mathsf{T}} = \boldsymbol{\sigma}'
$$
这意味着，一个对称的应力状态在任何旋转坐标系下观察，都将是还对称的 [@problem_id:3548543]。

#### 应力不变量与静水/偏应力分解

尽管应力张量的分量会随坐标系的旋转而改变，但某些由分量组合而成的标量值却保持不变，这些量被称为**应力不变量**（stress invariants）。对于一个三维对称应力张量，存在三个独立的主不变量，它们可以通过主应力 $\sigma_1, \sigma_2, \sigma_3$ 表示：
$$
\begin{align*}
I_1 = \sigma_1 + \sigma_2 + \sigma_3 \\
I_2 = \sigma_1\sigma_2 + \sigma_2\sigma_3 + \sigma_3\sigma_1 \\
I_3 = \sigma_1\sigma_2\sigma_3
\end{align*}
$$
这些不变量也可以直接通过任意坐标系下的应力分量计算得到 [@problem_id:3548594]：
$$
\begin{align*}
I_1 = \operatorname{tr}(\boldsymbol{\sigma}) \\
I_2 = \frac{1}{2} \left[ (\operatorname{tr}\boldsymbol{\sigma})^2 - \operatorname{tr}(\boldsymbol{\sigma}^2) \right] \\
I_3 = \det(\boldsymbol{\sigma})
\end{align*}
$$
其中 $\operatorname{tr}(\cdot)$ 表示迹，$\det(\cdot)$ 表示行列式。

为了更好地理解应力的物理效应，通常将其分解为两部分：引起体积变化的**静水应力**（hydrostatic stress）部分和引起形状变化的**偏应力**（deviatoric stress）部分。

**静水压力**（hydrostatic pressure）定义为三个正应力平均值的相反数：
$$
p = -\frac{1}{3}(\sigma_{11} + \sigma_{22} + \sigma_{33}) = -\frac{1}{3} I_1
$$
静水应力张量（或球量张量）是一个对所有方向都施加相同法向应力的纯球形张量，即 $\boldsymbol{\sigma}_{\text{hydro}} = -p \mathbf{I}$，其中 $\mathbf{I}$ 是单位张量。

**偏应力张量** $\mathbf{s}$ 则定义为总应力减去静水应力部分：
$$
\mathbf{s} = \boldsymbol{\sigma} - \boldsymbol{\sigma}_{\text{hydro}} = \boldsymbol{\sigma} + p\mathbf{I}
$$
根据其定义，偏应力张量是**无迹的**（$\operatorname{tr}(\mathbf{s}) = 0$）。由于 $\boldsymbol{\sigma}$ 和 $\mathbf{I}$ 都是对称的，$\mathbf{s}$ 也是一个对称张量。偏应力张量描述了应力状态中导致材料剪切变形或扭曲的部分。它的不变量，特别是第二偏应力[不变量](@entry_id:148850) $J_2 = \frac{1}{2} \operatorname{tr}(\mathbf{s}^2)$，在塑性力学（如von Mises屈服准则）中扮演着核心角色 [@problem_id:3548594]。

值得注意的是，由于偏应力张量只是在柯西应力张量的基础上减去一个单位张量的标量倍，两者是**共轴的**，即它们共享相同的主方向 [@problem_id:3548594]。

### 经典连续介质理论的拓展

本章所讨论的柯西应力及其对称性构成了经典连续介质力学的基石。然而，在处理更复杂问题时，这些概念也需要被审视和拓展。

#### 大变形中的应力测度

当物体经历大变形时，区分**参考构型**（变形前）和**当前构型**（变形后）变得至关重要。柯西应力是定义在当前构型上的“真实”应力。在理论和计算中，还引入了其他应力测度，它们将力与参考构型联系起来。最重要的两种是：

1.  **第一Piola-Kirchhoff (PK1) 应力张量** ($\mathbf{P}$): 将当前构型中的力与参考构型中的面积元联系起来。
2.  **第二Piola-Kirchhoff (PK2) 应力张量** ($\mathbf{S}$): 将一个虚拟的、映射回参考构型的力与参考构型中的面积元联系起来。

这些应力张量通过变形梯度 $\mathbf{F}$ 与柯西应力 $\boldsymbol{\sigma}$ 相关联。重要的对称性结论是：如果柯西应力 $\boldsymbol{\sigma}$ 是对称的，那么第二PK应力 $\mathbf{S}$ 也是对称的。然而，第一PK应力 $\mathbf{P}$ 在一般情况下**不是对称的** [@problem_id:3548619]。这一特性对建立大变形问题的控制方程和数值算法具有深远影响。

#### 超越经典：微极连续介质

柯西应力张量的对称性源于一个关键假设：物质微元间不存在直接的力矩传递。然而，对于某些具有显著微观结构的材料，如颗粒材料、复合材料或泡沫材料，这种假设可能不成立。

**微极（或Cosserat）连续介质理论**通过引入独立的**微转动**自由度 $\boldsymbol{\varphi}$ 和与之共轭的**力偶应力张量** $\boldsymbol{\mu}$ 来描述这类材料的行为 [@problem_id:3548581]。在此推广的理论框架下，角动量守恒定律的形式变为 [@problem_id:3548580]：
$$
\boldsymbol{\varepsilon}:\boldsymbol{\sigma} + \operatorname{div}\boldsymbol{\mu} + \mathbf{c} = \rho \mathbf{J} \ddot{\boldsymbol{\varphi}}
$$
其中 $\boldsymbol{\varepsilon}:\boldsymbol{\sigma}$ 是与 $\boldsymbol{\sigma}$ 的反对称部分相关的轴矢量，$\mathbf{c}$ 是体力偶密度，$\rho \mathbf{J} \ddot{\boldsymbol{\varphi}}$ 是微转动惯性项。

这个方程的意义非凡：它表明柯西应力张量 $\boldsymbol{\sigma}$ 的反对称部分不再必须为零，而是与力偶应力的散度、体力偶以及微惯性力矩相平衡 [@problem_id:2616464] [@problem_id:3548610]。这不仅为描述更复杂的材料行为提供了理论工具，也从反面深刻地揭示了经典理论中应力对称性所依赖的物理前提。