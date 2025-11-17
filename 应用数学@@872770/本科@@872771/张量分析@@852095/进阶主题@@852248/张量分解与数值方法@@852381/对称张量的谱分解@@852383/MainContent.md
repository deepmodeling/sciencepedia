## 引言
对称张量，如[应力张量和应变张量](@entry_id:755512)，是描述物理世界中各种现象的核心数学工具。然而，它们在特定[坐标系](@entry_id:156346)下的分量表示形式往往十分复杂，掩盖了其内在的物理本质。如何超越[坐标系](@entry_id:156346)的束缚，直接洞察张量所代表的物理状态（例如，一个受力点最主要的拉伸方向和大小）？这便是对称张量[谱分解](@entry_id:173707)理论所要解决的核心问题。它提供了一种强大的方法，将复杂的[张量分解](@entry_id:173366)为一组简单且具有明确物理意义的“谱”分量——主值和主方向。

本文将系统性地引导读者深入探索对称张量的谱分解。在第一部分“原理与机制”中，我们将奠定该理论的数学基石，从本征值问题出发，详细阐述[谱定理](@entry_id:136620)及其推论。接下来，在“应用与跨学科联系”部分，我们将展示该理论如何在连续介质力学、[材料科学](@entry_id:152226)和[几何分析](@entry_id:157700)等领域大放异彩，成为连接抽象数学与工程实践的关键桥梁。最后，“动手实践”部分将通过一系列精心设计的计算问题，帮助读者将理论知识转化为解决实际问题的能力。通过这三个章节的学习，读者将能够全面掌握谱分解的理论精髓与实用技巧。

## 原理与机制

本章深入探讨[对称张量](@entry_id:148092)[谱分解](@entry_id:173707)的核心原理与机制。在上一章的引言之后，我们将直接进入该主题的数学和物理基础。[谱分解](@entry_id:173707)不仅是线性代数中的一个优美结果，更是在连续介质力学等领域中分析应力、应变等物理量不可或缺的工具。我们将从对称张量的本征值问题出发，系统地建立[谱定理](@entry_id:136620)，并阐述其在不同情况下的具体形式和应用。

### [对称张量](@entry_id:148092)的[本征值问题](@entry_id:142153)

在物理学和工程学中，许多重要的物理量，如[应力张量和应变张量](@entry_id:755512)，都由二阶[对称张量](@entry_id:148092)来描述。[对称张量](@entry_id:148092)的一个关键特性是它们存在一组特殊的“方向”，在这些方向上，张量的作用效果变得异常简单。具体来说，当张量作用于沿这些方向的矢量时，其效果等同于对该矢量进行简单的缩放，而不会改变其方向。这一现象的数学描述构成了 **本征值问题** (eigenvalue problem)。

对于一个给定的二阶对称张量 $\mathbf{A}$，其[本征值问题](@entry_id:142153)是寻找一个标量 $\lambda$ 和一个非[零矢量](@entry_id:155273) $\mathbf{n}$，使得它们满足以下方程：
$$ \mathbf{A}\mathbf{n} = \lambda\mathbf{n} $$
在这里，$\lambda$ 被称为张量 $\mathbf{A}$ 的一个 **[本征值](@entry_id:154894)** (eigenvalue)，而 $\mathbf{n}$ 则被称为对应于该[本征值](@entry_id:154894)的 **本征矢量** (eigenvector)。在力学背景下，这些量通常有更具物理意义的名称：[本征值](@entry_id:154894)被称为 **主值** (principal values)，而单位化的本征矢量被称为 **[主方向](@entry_id:276187)** (principal directions)。

这个抽象的数学定义在物理世界中有非常直观的对应。以连续介质力学中的柯西应力张量 $\boldsymbol{\sigma}$ 为例，它是一个[对称张量](@entry_id:148092)，描述了物体内部某一点的应力状态。根据柯西公式，作用在以[单位法向量](@entry_id:178851) $\mathbf{n}$ 为特征的微小表面上的牵[引力](@entry_id:175476)矢量 $\mathbf{t}$ 由下式给出：$\mathbf{t}(\mathbf{n}) = \boldsymbol{\sigma}\mathbf{n}$。通常情况下，牵[引力](@entry_id:175476)矢量 $\mathbf{t}$ 与法向量 $\mathbf{n}$ 并不平行，这意味着作用在该表面上的力既有垂直于表面的分量（[正应力](@entry_id:260622)），也有平行于表面的分量（剪应力）。

然而，对于特定的[主方向](@entry_id:276187) $\mathbf{n}_i$，情况就不同了。如果 $\mathbf{n}_i$ 是一个[主方向](@entry_id:276187)，那么根据[本征值方程](@entry_id:192306)，我们有 $\boldsymbol{\sigma}\mathbf{n}_i = \lambda_i\mathbf{n}_i$。这意味着作用在以 $\mathbf{n}_i$ 为[法向量](@entry_id:264185)的平面（称为 **[主平面](@entry_id:164488)**）上的牵[引力](@entry_id:175476)矢量 $\mathbf{t}(\mathbf{n}_i)$ 完全平行于法向量本身。换言之，在[主平面](@entry_id:164488)上，剪应力分量为零，物体内部的力完全表现为纯粹的拉伸或压缩。对应的[主值](@entry_id:189577) $\lambda_i$ 就是这个平面上的[正应力](@entry_id:260622)大小，被称为 **[主应力](@entry_id:176761)** (principal stress) [@problem_id:2686483] [@problem_id:2686484]。因此，寻找一个张量的[主值](@entry_id:189577)和主方向，等价于在复杂的应力状态中找到那些“最纯粹”的受力方向和大小，这对于材料的强度分析和失效预测至关重要。

### [谱定理](@entry_id:136620)：分解的基石

[对称张量](@entry_id:148092)的美妙之处在于，其本征值问题总是有着非常良好和确定的解。这一结论由所谓的 **谱定理** (Spectral Theorem) 保证。对于作用在三维实[欧几里得空间](@entry_id:138052) $\mathbb{R}^3$ 上的任意一个实对称二阶张量 $\mathbf{A}$，谱定理断言：

1.  张量 $\mathbf{A}$ 的所有[本征值](@entry_id:154894)都是实数。
2.  存在一组由 $\mathbf{A}$ 的本征矢量构成的标准正交基，该基能够张成整个空间 $\mathbb{R}^3$。

这个定理是谱分解理论的基石。第一个论断保证了[主值](@entry_id:189577)是真实的物理量，而非数学上的复数。第二个论断则更为深刻，它意味着任何矢量都可以被唯一地表示为这些相互正交的[主方向](@entry_id:276187)的[线性组合](@entry_id:154743)。

[谱定理](@entry_id:136620)的两个关键性质可以通过基本定义推导出来。首先，对于一个实[对称张量](@entry_id:148092)，其[本征值](@entry_id:154894)必为实数。其次，对应于 *不同* [本征值](@entry_id:154894)的本征矢量必然相互正交 [@problem_id:2686484]。我们可以简单证明后一点：假设 $(\lambda_1, \mathbf{n}_1)$ 和 $(\lambda_2, \mathbf{n}_2)$ 是张量 $\mathbf{A}$ 的两个本征对，且 $\lambda_1 \neq \lambda_2$。我们考察[标量积](@entry_id:138996) $\mathbf{n}_2 \cdot (\mathbf{A}\mathbf{n}_1)$。一方面，$\mathbf{n}_2 \cdot (\mathbf{A}\mathbf{n}_1) = \mathbf{n}_2 \cdot (\lambda_1 \mathbf{n}_1) = \lambda_1 (\mathbf{n}_2 \cdot \mathbf{n}_1)$。另一方面，由于 $\mathbf{A}$ 是对称的（$\mathbf{A} = \mathbf{A}^\mathsf{T}$），我们有 $\mathbf{n}_2 \cdot (\mathbf{A}\mathbf{n}_1) = (\mathbf{A}\mathbf{n}_2) \cdot \mathbf{n}_1 = (\lambda_2 \mathbf{n}_2) \cdot \mathbf{n}_1 = \lambda_2 (\mathbf{n}_2 \cdot \mathbf{n}_1)$。因此，我们得到 $(\lambda_1 - \lambda_2)(\mathbf{n}_1 \cdot \mathbf{n}_2) = 0$。因为 $\lambda_1 \neq \lambda_2$，所以必然有 $\mathbf{n}_1 \cdot \mathbf{n}_2 = 0$，即这两个本征矢量是正交的。

更进一步，对称性不仅是能够进行[正交对角化](@entry_id:149411)的充分条件，也是必要条件。也就是说，一个实二阶张量能够被[正交对角化](@entry_id:149411)（即存在一个正交矩阵 $\mathbf{Q}$ 使得 $\mathbf{Q}^{\mathsf{T}}\mathbf{A}\mathbf{Q}$ 为对角阵）的充要条件是该张量是对称的 [@problem_id:2686506]。这一深刻的联系凸显了对称性在[张量分析](@entry_id:161423)中的核心地位。

### 谱分解公式

[谱定理](@entry_id:136620)保证了存在一个由标准正交本征矢量 $\{\mathbf{n}_1, \mathbf{n}_2, \mathbf{n}_3\}$ 构成的基。基于这个基，我们可以将对称张量 $\mathbf{A}$ 本身进行分解。为此，我们首先引入 **并矢** (dyadic product) 的概念。两个矢量 $\mathbf{u}$ 和 $\mathbf{v}$ 的并矢记作 $\mathbf{u} \otimes \mathbf{v}$，它是一个[二阶张量](@entry_id:199780)，其作用于任意矢量 $\mathbf{w}$ 的结果是 $(\mathbf{u} \otimes \mathbf{v})\mathbf{w} = \mathbf{u}(\mathbf{v} \cdot \mathbf{w})$。

特别地，当 $\mathbf{u}=\mathbf{v}=\mathbf{n}$ 且 $\mathbf{n}$ 是单位矢量时，张量 $\mathbf{P} = \mathbf{n} \otimes \mathbf{n}$ 具有特殊的几何意义：它是一个 **[正交投影](@entry_id:144168)算子** (orthogonal projection operator)。它将任意矢量 $\mathbf{w}$ 投影到由 $\mathbf{n}$ 所张成的方向上，即 $\mathbf{P}\mathbf{w} = (\mathbf{n} \cdot \mathbf{w})\mathbf{n}$。

利用这些[投影算子](@entry_id:154142)，[对称张量](@entry_id:148092) $\mathbf{A}$ 可以被表示为其[本征值](@entry_id:154894)和对应[主方向](@entry_id:276187)[投影算子](@entry_id:154142)的加权和。这便是 **谱分解** (spectral decomposition) 公式：
$$ \mathbf{A} = \sum_{i=1}^3 \lambda_i (\mathbf{n}_i \otimes \mathbf{n}_i) = \lambda_1 (\mathbf{n}_1 \otimes \mathbf{n}_1) + \lambda_2 (\mathbf{n}_2 \otimes \mathbf{n}_2) + \lambda_3 (\mathbf{n}_3 \otimes \mathbf{n}_3) $$
这个公式优雅地揭示了[对称张量](@entry_id:148092)的内在结构。它告诉我们，一个[对称张量](@entry_id:148092) $\mathbf{A}$ 对任意矢量 $\mathbf{v}$ 的作用，可以分解为三个独立的步骤：首先将 $\mathbf{v}$ 分别投影到三个相互正交的主方向 $\mathbf{n}_i$ 上，然后将每个投影分量乘以对应的[主值](@entry_id:189577) $\lambda_i$ 进行缩放，最后将这三个缩放后的矢量分量重新组合起来 [@problem_id:2686483]。数学上，这表现为：
$$ \mathbf{A}\mathbf{v} = \left(\sum_{i=1}^3 \lambda_i \mathbf{n}_i \otimes \mathbf{n}_i\right) \mathbf{v} = \sum_{i=1}^3 \lambda_i (\mathbf{n}_i \cdot \mathbf{v}) \mathbf{n}_i $$
这与我们从本征矢量[基展开](@entry_id:746689) $\mathbf{v}$ 再应用 $\mathbf{A}$ 所得的结果完全一致。

**示例：计算谱分解**

让我们通过一个具体的例子来演示如何计算谱分解。考虑一个应力张量，其在某个笛卡尔坐标系下的矩阵表示为 [@problem_id:1539547] [@problem_id:1539529]：
$$ [\boldsymbol{\sigma}] = \begin{pmatrix} 7  & -2  & 0 \\ -2  & 6  & -2 \\ 0  & -2  & 5 \end{pmatrix} $$
1.  **计算[本征值](@entry_id:154894) ([主应力](@entry_id:176761))**: 我们求解特征方程 $\det([\boldsymbol{\sigma}] - \lambda \mathbf{I}) = 0$。
    $$ \det \begin{pmatrix} 7-\lambda  & -2  & 0 \\ -2  & 6-\lambda  & -2 \\ 0  & -2  & 5-\lambda \end{pmatrix} = (7-\lambda)((6-\lambda)(5-\lambda)-4) - (-2)(-2(5-\lambda)) = 0 $$
    展开并化简后得到[特征多项式](@entry_id:150909)：$\lambda^3 - 18\lambda^2 + 99\lambda - 162 = 0$。通过试根或[因式分解](@entry_id:150389)，我们发现其根为 $\lambda_1 = 3$, $\lambda_2 = 6$, $\lambda_3 = 9$。这些就是该应力状态下的三个主应力。

2.  **计算本征矢量 ([主方向](@entry_id:276187))**: 对每一个[本征值](@entry_id:154894) $\lambda_i$，我们求解线性方程组 $([\boldsymbol{\sigma}] - \lambda_i \mathbf{I})\mathbf{n}_i = \mathbf{0}$。
    *   对于 $\lambda_1 = 3$，解得本征矢量正比于 $(1, 2, 2)^\mathsf{T}$。单位化后得到 $\mathbf{n}_1 = \frac{1}{3}(1, 2, 2)^\mathsf{T}$。
    *   对于 $\lambda_2 = 6$，解得本征矢量正比于 $(2, 1, -2)^\mathsf{T}$。单位化后得到 $\mathbf{n}_2 = \frac{1}{3}(2, 1, -2)^\mathsf{T}$。
    *   对于 $\lambda_3 = 9$，解得本征矢量正比于 $(2, -2, 1)^\mathsf{T}$。单位化后得到 $\mathbf{n}_3 = \frac{1}{3}(2, -2, 1)^\mathsf{T}$。
    读者可以自行验证，这三个[主方向](@entry_id:276187)两两正交。

3.  **构造[谱分解](@entry_id:173707)**: 现在我们可以写出该张量的谱分解形式。例如，投影算子 $\mathbf{P}_1 = \mathbf{n}_1 \otimes \mathbf{n}_1$ 的矩阵表示为：
    $$ [\mathbf{P}_1] = \frac{1}{9} \begin{pmatrix} 1 \\ 2 \\ 2 \end{pmatrix} \begin{pmatrix} 1  & 2  & 2 \end{pmatrix} = \frac{1}{9} \begin{pmatrix} 1  & 2  & 2 \\ 2  & 4  & 4 \\ 2  & 4  & 4 \end{pmatrix} $$
    最终，应力张量可以表示为 $[\boldsymbol{\sigma}] = 3[\mathbf{P}_1] + 6[\mathbf{P}_2] + 9[\mathbf{P}_3]$。

### 唯一性与简并性

谱分[解的唯一性](@entry_id:143619)取决于[本征值](@entry_id:154894)的[分布](@entry_id:182848)情况。

*   **非简并情况 (Non-degenerate case)**: 如果三个[本征值](@entry_id:154894) $\lambda_1, \lambda_2, \lambda_3$ 互不相同，那么对应的三个一维[本征空间](@entry_id:147356)（[主方向](@entry_id:276187)）也是唯一确定的（除了可以选择相反的方向，即 $\mathbf{n}_i \mapsto -\mathbf{n}_i$，但这不影响[投影算子](@entry_id:154142) $\mathbf{n}_i \otimes \mathbf{n}_i$）。因此，在这种情况下，[谱分解](@entry_id:173707)是（在不计各项顺序和主方向符号的情况下）唯一的 [@problem_id:2686483]。

*   **简并情况 (Degenerate case)**: 如果出现 **[重根](@entry_id:151486)**，即某些[本征值](@entry_id:154894)相等，情况则有所不同。例如，假设 $\lambda_1 = \lambda_2 \neq \lambda_3$。此时，对应于重复[本征值](@entry_id:154894) $\lambda_1$ 的[本征空间](@entry_id:147356)不再是一条直线，而是一个二维平面。任何位于这个平面内的非[零矢量](@entry_id:155273)都是对应于 $\lambda_1$ 的本征矢量。因此，单个的主方向不再是唯一的。我们可以为这个二维[本征空间](@entry_id:147356)选取任意一组[标准正交基](@entry_id:147779) $\{\mathbf{m}_1, \mathbf{m}_2\}$，它们都是合法的主方向。

    尽管单个主方向不唯一，但[本征空间](@entry_id:147356)本身是唯一确定的。更重要的是，投影到这个简并[本征空间](@entry_id:147356)上的 **[投影算子](@entry_id:154142)** $\mathbf{P}_{\lambda_1}$ 也是唯一的，它不依赖于我们如何选择基。这个[投影算子](@entry_id:154142)可以表示为 $\mathbf{P}_{\lambda_1} = \mathbf{m}_1 \otimes \mathbf{m}_1 + \mathbf{m}_2 \otimes \mathbf{m}_2$。无论我们选择哪一组标准正交基，这个和都是不变的 [@problem_id:2686483] [@problem_id:2686484]。在这种情况下，谱分解写为不同[本征值](@entry_id:154894)对应的投影算子的和：
    $$ \mathbf{A} = \lambda_1 \mathbf{P}_{\lambda_1} + \lambda_3 \mathbf{P}_{\lambda_3} $$
    其中 $\mathbf{P}_{\lambda_1}$ 是秩为2的投影算子，$\mathbf{P}_{\lambda_3}$ 是秩为1的投影算子。

一个巧妙的技巧是，我们可以在不求解本征矢量的情况下，直接构造这些投影算子。假设一个张量 $\mathbf{A}$ 只有两个不同的[本征值](@entry_id:154894) $\lambda_a$ 和 $\lambda_b$。其[谱分解](@entry_id:173707)和单位分解分别为：
$$ \mathbf{A} = \lambda_a \mathbf{P}_a + \lambda_b \mathbf{P}_b $$
$$ \mathbf{I} = \mathbf{P}_a + \mathbf{P}_b $$
这是一个关于未知算子 $\mathbf{P}_a$ 和 $\mathbf{P}_b$ 的线性方程组。通过求解这个[方程组](@entry_id:193238)，我们可以得到每个投影算子关于 $\mathbf{A}$ 和 $\mathbf{I}$ 的多项式表达式。例如，我们可以得到 $\mathbf{P}_a = \frac{\mathbf{A} - \lambda_b \mathbf{I}}{\lambda_a - \lambda_b}$。

以张量 $[\mathbf{A}] = \begin{pmatrix} 3  & 1  & 1 \\ 1  & 3  & 1 \\ 1  & 1  & 3 \end{pmatrix}$ 为例 [@problem_id:2686478]，我们之前计算出其[本征值](@entry_id:154894)为 $\lambda_1=5$ (非简并) 和 $\lambda_2=2$ (二重简并)。我们想要求解对应于简并[本征值](@entry_id:154894) $\lambda=2$ 的[投影算子](@entry_id:154142) $\mathbf{P}_2$。根据上述方法，我们有：
$$ \mathbf{P}_2 = \frac{\mathbf{A} - 5\mathbf{I}}{2 - 5} = \frac{\mathbf{A} - 5\mathbf{I}}{-3} = \frac{5\mathbf{I} - \mathbf{A}}{3} $$
这个简洁的表达式完全由张量本身及其[本征值](@entry_id:154894)谱确定，无需知道任何一个具体的本征矢量。

### [张量不变量](@entry_id:203254)及其意义

张量的某些属性不随[坐标系](@entry_id:156346)的选取而改变，这些属性被称为 **[张量不变量](@entry_id:203254)** (tensor invariants)。对于一个[二阶张量](@entry_id:199780)，其最重要的[不变量](@entry_id:148850)是其[本征值](@entry_id:154894)。因为[本征值方程](@entry_id:192306) $\mathbf{A}\mathbf{n} = \lambda\mathbf{n}$ 是一个与[坐标系](@entry_id:156346)无关的固有属性，所以[本征值](@entry_id:154894)本身就是[不变量](@entry_id:148850) [@problem_id:1539522]。这意味着，即使我们将张量在一个旋转后的新[坐标系](@entry_id:156346)中表示，其计算出的主值集合依然保持不变。

除了[本征值](@entry_id:154894)本身，由[本征值](@entry_id:154894)构成的[对称多项式](@entry_id:153581)也是[不变量](@entry_id:148850)。对于三维空间中的二阶张量 $\mathbf{A}$，有三个 **[主不变量](@entry_id:193522)** (principal invariants)，它们是特征多项式 $\det(\mathbf{A} - \lambda\mathbf{I}) = 0$ 的系数（稍加整理后）：
$$ \lambda^3 - I_1(\mathbf{A})\lambda^2 + I_2(\mathbf{A})\lambda - I_3(\mathbf{A}) = 0 $$
这些[不变量](@entry_id:148850)可以由[本征值](@entry_id:154894)表示为 [@problem_id:2686496]：
$$ I_1 = \lambda_1 + \lambda_2 + \lambda_3 $$
$$ I_2 = \lambda_1\lambda_2 + \lambda_2\lambda_3 + \lambda_3\lambda_1 $$
$$ I_3 = \lambda_1\lambda_2\lambda_3 $$
更实用的是，这些[不变量](@entry_id:148850)可以直接通过张量在任意[坐标系](@entry_id:156346)下的分量计算出来，而无需先求解[本征值](@entry_id:154894)：
*   **第一[不变量](@entry_id:148850)** $I_1$ 是张量的 **迹** (trace)：$I_1 = \operatorname{tr}(\mathbf{A}) = A_{kk}$
*   **第三[不变量](@entry_id:148850)** $I_3$ 是张量的 **[行列式](@entry_id:142978)** (determinant)：$I_3 = \det(\mathbf{A})$
*   **第二[不变量](@entry_id:148850)** $I_2$ 可以通过迹运算组合得到：$I_2 = \frac{1}{2} [(\operatorname{tr}\mathbf{A})^2 - \operatorname{tr}(\mathbf{A}^2)]$

这些[不变量](@entry_id:148850)在构建不依赖于观察者[坐标系](@entry_id:156346)的物理[本构关系](@entry_id:186508)时至关重要。

### 高级分解与应用

**瑞利商与极值原理**

[本征值问题](@entry_id:142153)还有一个等价的变分提法。定义 **[瑞利商](@entry_id:137794)** (Rayleigh quotient) 如下：
$$ R(\mathbf{x}) = \frac{\mathbf{x} \cdot (\mathbf{A}\mathbf{x})}{\mathbf{x} \cdot \mathbf{x}} $$
对于一个[对称张量](@entry_id:148092) $\mathbf{A}$，[瑞利商](@entry_id:137794)在其所有非[零矢量](@entry_id:155273) $\mathbf{x}$ 上取得的 **极值** (最大值和最小值) 正是张量的最大和最小[本征值](@entry_id:154894)。而使得瑞利商取到极值的矢量，恰好就是对应的本征矢量 [@problem_id:2686484]。

这个原理在物理上有直接应用。例如，一个点处沿不同方向的法向应力 $\sigma_n$ 由 $\sigma_n = \mathbf{n} \cdot (\boldsymbol{\sigma}\mathbf{n})$ 给出，其中 $\mathbf{n}$ 是[单位法向量](@entry_id:178851)。这正是应力张量 $\boldsymbol{\sigma}$ 在[单位球](@entry_id:142558)面上的瑞利商。因此，要寻找一个受力构件中可能出现的最大拉应力（这通常是材料破坏的决定性因素），我们实际上是在寻找[应力张量](@entry_id:148973)的最大[本征值](@entry_id:154894) [@problem_id:1539537]。

**体积部分与偏量部分的分解**

在[连续介质力学](@entry_id:155125)中，将张量（如应变或应力）分解为其引起体积变化的部分和引起形状变化的部分是非常有用的。这引出了 **[体积-偏量分解](@entry_id:183756)** (volumetric-deviatoric decomposition)。对于任何一个二阶张量 $\mathbf{A}$，它可以唯一地分解为一个 **球张量** (spherical tensor) 和一个 **[偏张量](@entry_id:185837)** (deviatoric tensor) 的和：
$$ \mathbf{A} = \mathbf{A}_{\text{vol}} + \mathbf{A}' $$
其中：
*   **体积部分** (volumetric part) $\mathbf{A}_{\text{vol}}$ 是一个球张量，定义为 $\mathbf{A}_{\text{vol}} = \frac{1}{3}(\operatorname{tr}\mathbf{A})\mathbf{I}$。它与张量的[平均法](@entry_id:264400)向分量有关，在[应变张量](@entry_id:193332)中代表体积的均匀膨胀或收缩。
*   **偏量部分** (deviatoric part) $\mathbf{A}'$ 是张量中引起形状畸变的部分，定义为 $\mathbf{A}' = \mathbf{A} - \mathbf{A}_{\text{vol}}$。

这个分解具有一系列重要的性质 [@problem_id:2686477]：
1.  **偏[张量的迹](@entry_id:190669)为零**: $\operatorname{tr}(\mathbf{A}') = \operatorname{tr}(\mathbf{A} - \frac{1}{3}(\operatorname{tr}\mathbf{A})\mathbf{I}) = \operatorname{tr}(\mathbf{A}) - \frac{1}{3}(\operatorname{tr}\mathbf{A})\operatorname{tr}(\mathbf{I}) = \operatorname{tr}(\mathbf{A}) - \operatorname{tr}(\mathbf{A}) = 0$。这是[偏张量](@entry_id:185837)的定义性特征。

2.  **共享本征矢量**: 张量 $\mathbf{A}$ 和其偏量部分 $\mathbf{A}'$ 拥有完全相同的[主方向](@entry_id:276187)（本征矢量）。这是因为向一个张量加上一个球张量（$\alpha\mathbf{I}$）只会将其[本征值](@entry_id:154894)移动一个常数 $\alpha$，而不会改变其本征矢量。具体来说，如果 $\lambda_i$ 是 $\mathbf{A}$ 的[本征值](@entry_id:154894)，那么 $\mathbf{A}'$ 对应的[本征值](@entry_id:154894)是 $\lambda'_i = \lambda_i - \frac{1}{3}(\operatorname{tr}\mathbf{A})$。这个性质也解释了为何向张量添加一个各向同性部分不会改变其[主方向](@entry_id:276187) [@problem_id:2686484]。

3.  **正交性**: 体积部分和偏量部分在[弗罗贝尼乌斯内积](@entry_id:153693)（Frobenius inner product, $\mathbf{X}:\mathbf{Y} = \operatorname{tr}(\mathbf{X}^\mathsf{T}\mathbf{Y})$）的意义下是正交的，即 $\mathbf{A}_{\text{vol}} : \mathbf{A}' = 0$。这个正交性对于任意二阶张量（不一定是对称的）都成立。

4.  **范数的分解**: 基于上述正交性，张量的[弗罗贝尼乌斯范数](@entry_id:143384)的平方可以像[勾股定理](@entry_id:264352)一样分解为两部分范数的平方和：$\|\mathbf{A}\|_F^2 = \|\mathbf{A}_{\text{vol}}\|_F^2 + \|\mathbf{A}'\|_F^2$。

这种分解在[弹塑性力学](@entry_id:193198)中尤为重要，因为材料的体积变形（弹性）和形状改变（塑性）往往遵循不同的物理规律。通过[谱分解](@entry_id:173707)和[体积-偏量分解](@entry_id:183756)，我们可以将复杂的张量量分解为一系列在物理和几何上具有清晰含义的基本组成部分，从而极大地简化了分析和建模的过程。