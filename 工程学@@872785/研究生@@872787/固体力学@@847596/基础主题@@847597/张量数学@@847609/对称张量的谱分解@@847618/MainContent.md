## 引言
在[固体力学](@entry_id:164042)中，对称二阶张量，如[应力张量和应变张量](@entry_id:755512)，是描述[材料力学](@entry_id:201885)行为的核心数学工具。然而，一个张量以其分量形式表示时，往往难以直观地揭示其内在的物理本质。[谱分解](@entry_id:173707)理论正是解决这一问题的关键，它提供了一个强大的框架，能够将复杂的[张量分解](@entry_id:173366)为更易于理解的[主值](@entry_id:189577)和[主方向](@entry_id:276187)。本文旨在系统性地阐述对称张量[谱分解](@entry_id:173707)的理论与应用，弥合抽象数学与具体物理现象之间的鸿沟。在接下来的内容中，我们将首先在“原理与机制”一章中深入探讨谱定理的数学基础、谱分解的构成及其唯一性，并介绍[张量不变量](@entry_id:203254)与[体积-偏量分解](@entry_id:183756)等重要概念。随后，在“应用与跨学科联系”一章中，我们将展示该理论如何在[应力应变](@entry_id:204183)分析、有限变形理论、[材料塑性](@entry_id:186852)模型及计算力学中发挥关键作用。最后，通过“动手实践”部分提供的一系列计算练习，读者将有机会将理论知识应用于具体问题，从而加深理解。

## 原理与机制

在对固体材料的力学行为进行数学描述时，对称[二阶张量](@entry_id:199780)扮演着核心角色。[应力张量和应变张量](@entry_id:755512)等基本物理量都由此[类数](@entry_id:156164)学对象表示。本章将深入探讨对称张量的一个基本且极为重要的性质——谱分解。我们将阐明其背后的数学原理，揭示其在[连续介质力学](@entry_id:155125)中的深刻物理意义，并探索与之相关的重要概念，如[张量不变量](@entry_id:203254)和[体积-偏量分解](@entry_id:183756)。

### 对称张量的[谱定理](@entry_id:136620)

[对称张量](@entry_id:148092)最引人注目的性质由**[谱定理](@entry_id:136620) (Spectral Theorem)** 概括。该定理是线性代数和[张量分析](@entry_id:161423)的基石，它指出，在有限维实欧几里得空间中，任何一个实的对称二阶张量 $\mathbf{A}$ 都存在一组由其[特征向量](@entry_id:151813)构成的标准正交基。此外，所有对应的[特征值](@entry_id:154894)都是实数。

为了完整理解这一定理，我们首先需要明确其核心概念。一个[二阶张量](@entry_id:199780) $\mathbf{A}$，作为从三维[欧几里得向量空间](@entry_id:192574) $\mathbb{R}^3$ 到其自身的线性映射，如果其在任一[标准正交基](@entry_id:147779)下的矩阵表示 $[A]$ 等于其转置 $[A]^T$，即 $A_{ij} = A_{ji}$，则称其为**对称的 (symmetric)** [@2918191]。这一定义等价于对于任意向量 $\mathbf{u}$ 和 $\mathbf{v}$，[内积](@entry_id:158127)关系 $(\mathbf{A}\mathbf{u}) \cdot \mathbf{v} = \mathbf{u} \cdot (\mathbf{A}\mathbf{v})$ 恒成立。

谱定理的结论是一个“当且仅当”的陈述：一个实的二阶张量是可[正交对角化](@entry_id:149411)的，当且仅当它是对称的 [@2686506]。

**必要性 (Necessity)** 的证明相对直接。如果一个张量 $\mathbf{A}$ 可被[正交对角化](@entry_id:149411)，意味着存在一个正交矩阵 $\mathbf{Q}$ (满足 $\mathbf{Q}^T\mathbf{Q} = \mathbf{I}$) 和一个对角矩阵 $\mathbf{D}$，使得 $\mathbf{D} = \mathbf{Q}^T\mathbf{A}\mathbf{Q}$。由此可得 $\mathbf{A} = \mathbf{Q}\mathbf{D}\mathbf{Q}^T$。对其进行[转置](@entry_id:142115)，我们得到 $\mathbf{A}^T = (\mathbf{Q}\mathbf{D}\mathbf{Q}^T)^T = (\mathbf{Q}^T)^T\mathbf{D}^T\mathbf{Q}^T = \mathbf{Q}\mathbf{D}\mathbf{Q}^T$，因为对角矩阵自身是对称的 ($\mathbf{D}^T=\mathbf{D}$)。因此，我们证明了 $\mathbf{A} = \mathbf{A}^T$，即张量必须是对称的 [@2686506]。

**充分性 (Sufficiency)** 的证明则更为精妙，它揭示了对称性所带来的深刻后果。其关键步骤包括 [@2686506]：
1.  **存在性**：对于任意[对称张量](@entry_id:148092) $\mathbf{A}$，至少存在一个实[特征值](@entry_id:154894)及对应的实[特征向量](@entry_id:151813)。这可以通过变分原理来证明，即考虑在[单位球](@entry_id:142558)面 $\lVert \mathbf{n} \rVert = 1$ 上寻找二次型 $\mathbf{n} \cdot (\mathbf{A}\mathbf{n})$ 的极值。由于单位球是[紧集](@entry_id:147575)且二次型是[连续函数](@entry_id:137361)，极值必然存在。通过[拉格朗日乘子法](@entry_id:176596)可以证明，达到极值的方向 $\mathbf{n}$ 恰好是 $\mathbf{A}$ 的一个[特征向量](@entry_id:151813)，而极值本身就是对应的[特征值](@entry_id:154894) $\lambda$ [@2686484] [@2686506]。
2.  **正交性**：对于对称张量 $\mathbf{A}$，分属于不同[特征值](@entry_id:154894) $\lambda_1 \neq \lambda_2$ 的[特征向量](@entry_id:151813) $\mathbf{v}_1$ 和 $\mathbf{v}_2$ 必定是正交的。这是因为 $\lambda_1(\mathbf{v}_1 \cdot \mathbf{v}_2) = (\lambda_1\mathbf{v}_1) \cdot \mathbf{v}_2 = (\mathbf{A}\mathbf{v}_1) \cdot \mathbf{v}_2 = \mathbf{v}_1 \cdot (\mathbf{A}\mathbf{v}_2) = \mathbf{v}_1 \cdot (\lambda_2\mathbf{v}_2) = \lambda_2(\mathbf{v}_1 \cdot \mathbf{v}_2)$。由于 $\lambda_1 \neq \lambda_2$，必然有 $\mathbf{v}_1 \cdot \mathbf{v}_2 = 0$ [@2686484] [@2686506]。
3.  **归纳构造**：找到一个特征对 $(\lambda_1, \mathbf{n}_1)$ 后，可以证明由所有与 $\mathbf{n}_1$ 正交的向量构成的[子空间](@entry_id:150286)（即 $\mathbf{n}_1$ 的正交补）在 $\mathbf{A}$ 的作用下是**不变的 (invariant)**。并且，$\mathbf{A}$ 在这个[子空间](@entry_id:150286)上的限制仍然是一个[对称算子](@entry_id:272489)。因此，我们可以在这个维度减一的[子空间](@entry_id:150286)上重复此过程，通过[数学归纳法](@entry_id:138544)，最终构建出覆盖整个空间的一组标准[正交特征向量](@entry_id:155522) [@2686506]。

对称性这一条件是至关重要的。若张量非对称，谱定理的结论便不再成立。考虑以下几个反例 [@2686469]：
-   **无实[特征值](@entry_id:154894)**：纯[旋转张量](@entry_id:191990) $\boldsymbol{W}=\begin{pmatrix} 0  -1 \\ 1  0 \end{pmatrix}$ 是反对称的。其[特征值](@entry_id:154894)为 $\pm i$，在实数域内没有[特征向量](@entry_id:151813)，因此无法在实空间中找到[特征基](@entry_id:151409)。
-   **不可[对角化](@entry_id:147016)**：[剪切变换](@entry_id:151272)张量 $\boldsymbol{J}=\begin{pmatrix} 1  1 \\ 0  1 \end{pmatrix}$ 是非对称的。它只有一个实[特征值](@entry_id:154894) $\lambda=1$，但其对应的特征空间仅为一维。这意味着我们无法找到足够多的[线性无关](@entry_id:148207)的[特征向量](@entry_id:151813)来张成整个二维空间，故其不可[对角化](@entry_id:147016)。
-   **可对角化但非正交**：张量 $\boldsymbol{A}=\begin{pmatrix} 3  1 \\ 0  2 \end{pmatrix}$ 是非对称的，但它有两个不同的实[特征值](@entry_id:154894) $\lambda_1=3$ 和 $\lambda_2=2$。对应的[特征向量](@entry_id:151813)为 $\mathbf{v}_1 = (1,0)^T$ 和 $\mathbf{v}_2 = (1,-1)^T$。这两个向量线性无关，可以构成一个[特征基](@entry_id:151409)，但它们之间并不正交 ($\mathbf{v}_1 \cdot \mathbf{v}_2 = 1 \neq 0$)。由于特征空间均为一维，我们无法选择其他的[特征向量](@entry_id:151813)来使它们正交。

这些例子清晰地表明，只有对称性才能保证一个实张量同时拥有完备的、正交的实[特征向量](@entry_id:151813)集。

### 谱分解及其组成部分

[谱定理](@entry_id:136620)保证了任何对称二阶张量 $\mathbf{A}$ 都可以表示为其[特征值](@entry_id:154894)和特征方向的组合。这种表示称为**谱分解 (spectral decomposition)**：
$$
\mathbf{A} = \sum_{i=1}^3 \lambda_i (\mathbf{n}_i \otimes \mathbf{n}_i)
$$
这里，$\{\lambda_1, \lambda_2, \lambda_3\}$ 是 $\mathbf{A}$ 的三个实[特征值](@entry_id:154894)，$\{\mathbf{n}_1, \mathbf{n}_2, \mathbf{n}_3\}$ 是对应的标准[正交特征向量](@entry_id:155522)基。符号 $\otimes$ 表示**[并矢积](@entry_id:748716) (dyadic product)**，$(\mathbf{a} \otimes \mathbf{b})\mathbf{v} = \mathbf{a}(\mathbf{b} \cdot \mathbf{v})$。

每一项 $\mathbf{P}_i = \mathbf{n}_i \otimes \mathbf{n}_i$ 都是一个**[谱投影算子](@entry_id:755184) (spectral projector)** [@2686477]。它将任意[向量投影](@entry_id:147046)到由[特征向量](@entry_id:151813) $\mathbf{n}_i$ 张成的一维[子空间](@entry_id:150286)上。这些[投影算子](@entry_id:154142)构成了一个完备且正交的集合，满足以下性质：
-   **正交性 (Orthogonality)**：$\mathbf{P}_i \mathbf{P}_j = \delta_{ij} \mathbf{P}_i$ (其中 $\delta_{ij}$ 是克罗内克符号)
-   **完备性 (Completeness)**：$\sum_{i=1}^3 \mathbf{P}_i = \mathbf{I}$ (其中 $\mathbf{I}$ 是二阶单位张量)

利用这些性质，我们可以清晰地看到[谱分解](@entry_id:173707)如何作用于一个任意向量 $\mathbf{v}$ [@2686483]：
$$
\mathbf{A}\mathbf{v} = \left(\sum_{i=1}^3 \lambda_i \mathbf{P}_i\right)\mathbf{v} = \sum_{i=1}^3 \lambda_i (\mathbf{n}_i \otimes \mathbf{n}_i)\mathbf{v} = \sum_{i=1}^3 \lambda_i (\mathbf{n}_i \cdot \mathbf{v})\mathbf{n}_i
$$
这个表达式的几何意义是：$\mathbf{A}$ 对 $\mathbf{v}$ 的作用，等价于先将 $\mathbf{v}$ 分别向三个相互正交的特征方向 $\mathbf{n}_i$ 进行投影，得到分量 $(\mathbf{n}_i \cdot \mathbf{v})$，然后将每个投影分量沿其对应的特征方向拉伸或压缩 $\lambda_i$ 倍，最后将这三个结果向量相加。

一个核心问题是谱分[解的唯一性](@entry_id:143619)。对于一个给定的对称张量 $\mathbf{A}$ [@2686509] [@2686483]：
-   **[特征值](@entry_id:154894)**：由张量的[特征多项式](@entry_id:150909)唯一确定。因此，[特征值](@entry_id:154894)的多重集 $\{\lambda_1, \lambda_2, \lambda_3\}$ 是唯一的 [@2686509]。
-   **[特征空间](@entry_id:638014)与[谱投影算子](@entry_id:755184)**：每个不同的[特征值](@entry_id:154894)所对应的[特征空间](@entry_id:638014)是唯一的。因此，投影到这些特征空间上的[谱投影算子](@entry_id:755184) $\mathbf{P}_i$ 也是唯一的 [@2686509]。
-   **[特征向量](@entry_id:151813)**：
    -   如果一个[特征值](@entry_id:154894)是**非简并的 (non-degenerate)** (即其[代数重数](@entry_id:154240)为1)，那么其对应的特征方向（一维[特征空间](@entry_id:638014)）是唯一的，相应的单位[特征向量](@entry_id:151813)仅在符号上不唯一 ($\mathbf{n}_i \mapsto -\mathbf{n}_i$) [@2686483] [@2686509]。
    -   如果一个[特征值](@entry_id:154894)是**简并的 (degenerate)** (即其[代数重数](@entry_id:154240)大于1)，例如 $\lambda_1 = \lambda_2 \neq \lambda_3$，那么对应的[特征空间](@entry_id:638014)将是一个二维平面。在这个平面内，任何一个非零向量都是[特征向量](@entry_id:151813)。因此，单个的[特征向量](@entry_id:151813)不是唯一的。我们可以选择该平面内的任意一组标准正交基（例如 $\{\mathbf{n}_1, \mathbf{n}_2\}$）作为[谱分解](@entry_id:173707)的[基向量](@entry_id:199546)。尽管[基向量](@entry_id:199546)的选择不唯一，但它们张成的[特征空间](@entry_id:638014)以及投影到该空间上的算子 $\mathbf{P}_\lambda = \mathbf{n}_1 \otimes \mathbf{n}_1 + \mathbf{n}_2 \otimes \mathbf{n}_2$ 是唯一的 [@2686509] [@2686483]。

### 在[连续介质力学](@entry_id:155125)中的物理解释

[谱分解](@entry_id:173707)在[连续介质力学](@entry_id:155125)中具有直接而深刻的物理解释，尤其是在[应力分析](@entry_id:168804)中。柯西[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ 是一个对称二阶张量，其谱分解揭示了材料内部的应力主态。

在这种情况下：
-   [特征值](@entry_id:154894) $\sigma_i$ 称为**主应力 (principal stresses)**。它们代表了作用在特定平面上且没有剪切分量的法向应力。
-   [特征向量](@entry_id:151813) $\mathbf{n}_i$ 称为**主方向 (principal directions)**。由这些方向定义的平面称为**[主平面](@entry_id:164488) (principal planes)**。

[谱分解](@entry_id:173707)最重要的物理推论是：在[主平面](@entry_id:164488)上，牵[引力](@entry_id:175476)矢量 $\mathbf{t}$ 与该平面的法向矢量 $\mathbf{n}$ 共线 [@2686484] [@2686483]。根据柯西公式 $\mathbf{t} = \boldsymbol{\sigma}\mathbf{n}$，如果 $\mathbf{n}$ 是一个[主方向](@entry_id:276187) $\mathbf{n}_i$，则：
$$
\mathbf{t}(\mathbf{n}_i) = \boldsymbol{\sigma}\mathbf{n}_i = \sigma_i\mathbf{n}_i
$$
这意味着作用在[主平面](@entry_id:164488)上的牵[引力](@entry_id:175476)完全是法向的，其大小为主应力 $\sigma_i$，而**剪应力 (shear stress)** 分量为零。寻找[主应力](@entry_id:176761)和[主方向](@entry_id:276187)，就是寻找一个特殊的[坐标系](@entry_id:156346)，在这个[坐标系](@entry_id:156346)下，复杂的应力状态可以被最简洁地描述为三个独立的法向拉伸或压缩。

**示例：** 考虑一个由以下[矩阵表示](@entry_id:146025)的[应力张量](@entry_id:148973) $\boldsymbol{\Sigma}$ [@1539547]：
$$
\boldsymbol{\Sigma} = \begin{pmatrix} 7  -2  0 \\ -2  6  -2 \\ 0  -2  5 \end{pmatrix}
$$
通过求解其特征问题 $\det(\boldsymbol{\Sigma} - \lambda\mathbf{I}) = 0$，我们可以找到[主应力](@entry_id:176761)（[特征值](@entry_id:154894)）为 $\lambda_1 = 3$, $\lambda_2 = 6$, $\lambda_3 = 9$。随后，通过求解线性方程组 $(\boldsymbol{\Sigma} - \lambda_i\mathbf{I})\mathbf{v}_i = \mathbf{0}$，可以找到对应的归一化主方向（[特征向量](@entry_id:151813)），例如：
-   $\lambda_1=3$ 对应 $\mathbf{n}_1 = \frac{1}{3}(1, 2, 2)^T$
-   $\lambda_2=6$ 对应 $\mathbf{n}_2 = \frac{1}{3}(2, 1, -2)^T$
-   $\lambda_3=9$ 对应 $\mathbf{n}_3 = \frac{1}{3}(2, -2, 1)^T$
这组正交的向量 $\{\mathbf{n}_1, \mathbf{n}_2, \mathbf{n}_3\}$ 构成了主[坐标系](@entry_id:156346)。在该[坐标系](@entry_id:156346)下，应力张量是一个[对角矩阵](@entry_id:637782) $\mathrm{diag}(3, 6, 9)$，表示材料在该点承受着三个方向上大小分别为3、6和9的纯[法向应力](@entry_id:260622)。

### [不变量](@entry_id:148850)与分解

通过谱分解，我们可以定义一些不随[坐标系](@entry_id:156346)选择而改变的张量属性，即**[不变量](@entry_id:148850) (invariants)**，并可以将[张量分解](@entry_id:173366)为具有不同物理意义的部分。

#### [主不变量](@entry_id:193522)

对称张量 $\mathbf{A}$ 的特征多项式 $\det(\mathbf{A} - \lambda\mathbf{I}) = 0$ 可以写作：
$$
\lambda^3 - I_1(\mathbf{A})\lambda^2 + I_2(\mathbf{A})\lambda - I_3(\mathbf{A}) = 0
$$
其中的系数 $I_1, I_2, I_3$ 被称为 $\mathbf{A}$ 的**[主不变量](@entry_id:193522) (principal invariants)**。它们不依赖于[坐标系](@entry_id:156346)的选择，并且可以完全由[特征值](@entry_id:154894)确定 [@2686496]：
-   **第一[不变量](@entry_id:148850) (First Invariant)**: $I_1 = \lambda_1 + \lambda_2 + \lambda_3$
-   **第二[不变量](@entry_id:148850) (Second Invariant)**: $I_2 = \lambda_1\lambda_2 + \lambda_2\lambda_3 + \lambda_3\lambda_1$
-   **第三[不变量](@entry_id:148850) (Third Invariant)**: $I_3 = \lambda_1\lambda_2\lambda_3$

这些[不变量](@entry_id:148850)也可以直接通过张量运算计算，而无需先求解[特征值](@entry_id:154894) [@2686496]：
-   $I_1(\mathbf{A}) = \mathrm{tr}(\mathbf{A})$
-   $I_2(\mathbf{A}) = \frac{1}{2} \left[ (\mathrm{tr}\mathbf{A})^2 - \mathrm{tr}(\mathbf{A}^2) \right]$
-   $I_3(\mathbf{A}) = \det(\mathbf{A})$

在连续介质力学中，对于**各向同性 (isotropic)** 材料，其[本构关系](@entry_id:186508)（如[应力-应变关系](@entry_id:274093)）必须通过这些[不变量](@entry_id:148850)来表达，以保证材料响应与观察[坐标系](@entry_id:156346)无关。

#### [体积-偏量分解](@entry_id:183756)

任何二阶张量 $\mathbf{A}$ 都可以唯一地分解为一个**球张量 (spherical tensor)** 和一个**[偏张量](@entry_id:185837) (deviatoric tensor)** 的和。这在描述材料的体积变化和形状变化时尤其有用。
-   **体积部分 (Volumetric Part)** 或 **球部** 定义为 $\mathbf{A}_{\text{vol}} = \frac{1}{3}(\mathrm{tr}\mathbf{A})\mathbf{I}$。它是一个各向同性的张量，代表了张量的[平均法](@entry_id:264400)向分量（例如，[应力张量](@entry_id:148973)的静水压力）。
-   **偏量部分 (Deviatoric Part)** 或 **偏部** 定义为 $\mathbf{A}' = \mathbf{A} - \mathbf{A}_{\text{vol}}$。

[偏张量](@entry_id:185837) $\mathbf{A}'$ 的一个关键特性是它的迹为零：$\mathrm{tr}(\mathbf{A}') = 0$ [@2686477]。对于对称张量，这种分解对其谱有着直接的影响 [@2686477] [@2686499]：
-   **[主方向](@entry_id:276187)不变**：$\mathbf{A}'$ 和 $\mathbf{A}$ 共享相同的[主方向](@entry_id:276187)（[特征向量](@entry_id:151813)）。
-   **[主值](@entry_id:189577)的平移**：如果 $\mathbf{A}$ 的主值为 $\lambda_i$，那么 $\mathbf{A}'$ 的主值为 $\lambda'_i = \lambda_i - \frac{1}{3}(\mathrm{tr}\mathbf{A})$。
-   **偏[主值](@entry_id:189577)之和为零**：由于 $\mathrm{tr}(\mathbf{A}') = 0$，其主值之和也必须为零：$\lambda'_1 + \lambda'_2 + \lambda'_3 = 0$ [@2686499]。

此外，体积部分和偏量部分在以**[弗罗贝尼乌斯内积](@entry_id:153693) (Frobenius inner product)** $\mathbf{X}:\mathbf{Y} = \mathrm{tr}(\mathbf{X}^T\mathbf{Y})$ 定义的张量空间中是正交的，即 $\mathbf{A}_{\text{vol}}:\mathbf{A}' = 0$ [@2686477]。这导致了张量范数的毕达哥拉斯式分解：
$$
\lVert \mathbf{A} \rVert^2 = \lVert \mathbf{A}_{\text{vol}} \rVert^2 + \lVert \mathbf{A}' \rVert^2
$$
这个[正交分解](@entry_id:148020)对于任意[二阶张量](@entry_id:199780)（不一定对称）都成立，它将张量的大小分解为与其体积变化相关的[部分和](@entry_id:162077)与形状变化相关的部分 [@2686477]。

### 在主空间中的几何解释

为了更直观地理解应力状态，我们可以引入一个三维的**[主应力空间](@entry_id:184388) (principal-stress space)**，其坐标轴分别为三个[主应力](@entry_id:176761) $(\sigma_1, \sigma_2, \sigma_3)$ [@2686499]。

在这个空间中：
-   所有**[静水应力](@entry_id:186327)状态 (hydrostatic stress states)**，即 $\sigma_1 = \sigma_2 = \sigma_3 = p$，都位于一条穿过原点、[方向向量](@entry_id:169562)为 $(1, 1, 1)$ 的直线上。这条直线被称为**静水轴线 (hydrostatic axis)** [@2686499]。
-   偏应力主值 $(\sigma'_1, \sigma'_2, \sigma'_3)$ 的向量和总是为零，这意味着所有[偏应力](@entry_id:163323)状态都位于一个通过原点且[法向量](@entry_id:264185)为 $(1, 1, 1)$ 的平面上。这个平面被称为**偏平面 (deviatoric plane)** 或 $\pi$-平面。

从几何上看，将一个应力状态 $\boldsymbol{\sigma}$ 分解为其静水[部分和](@entry_id:162077)偏量部分，等价于在[主应力空间](@entry_id:184388)中，将点 $(\sigma_1, \sigma_2, \sigma_3)$ [正交投影](@entry_id:144168)到静水轴线和偏平面上 [@2686499]。[偏应力](@entry_id:163323)状态 $(\sigma'_1, \sigma'_2, \sigma'_3)$ 正是原应力点在偏平面上的投影。

偏应力的大小在[材料塑性](@entry_id:186852)理论中至关重要。[偏应力张量](@entry_id:267642)的第二[不变量](@entry_id:148850)，通常记为 $J_2$，定义为 $J_2 = \frac{1}{2}\boldsymbol{\sigma}':\boldsymbol{\sigma}' = \frac{1}{2}\mathrm{tr}((\boldsymbol{\sigma}')^2)$。在[主应力](@entry_id:176761)[坐标系](@entry_id:156346)下，这等于 $\frac{1}{2}(\sigma_1'^2 + \sigma_2'^2 + \sigma_3'^2)$。

在[主应力空间](@entry_id:184388)中，一个偏应力点到原点的[欧几里得距离](@entry_id:143990)的平方为 $\sigma_1'^2 + \sigma_2'^2 + \sigma_3'^2 = 2J_2$。这个距离 $\sqrt{2J_2}$ 是一个度量偏应力“大小”或“强度”的标量，它在许多屈服准则（如[von Mises屈服准则](@entry_id:174339)）中扮演着核心角色，因为它直接关联于引起材料形状改变（而非体积改变）的应力分量 [@2686499]。

综上所述，[对称张量](@entry_id:148092)的谱分解不仅是一个优美的数学工具，它还为我们理解和简化复杂的物理状态（如应力）提供了基础框架，并引出了一系列在[材料建模](@entry_id:751724)和[失效分析](@entry_id:266723)中不可或缺的核心概念。