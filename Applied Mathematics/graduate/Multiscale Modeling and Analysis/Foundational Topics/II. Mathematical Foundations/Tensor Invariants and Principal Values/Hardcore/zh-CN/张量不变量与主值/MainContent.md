## 引言
在[多尺度建模](@entry_id:154964)与分析领域，构建能够精确描述物理系统行为的数学模型至关重要。这些模型的一个根本要求是其**客观性 (objectivity)**，即模型的预测不应随观察者坐标系的变化而改变。然而，描述系统状态的张量（如应力或应变）其分量本身却是依赖于坐标系的。这就带来了一个核心的知识鸿沟：我们如何从这些依赖于坐标系的分量中，提取出能够客观描述材料内在物理状态的标量信息？[张量不变量](@entry_id:203254)和[主值](@entry_id:189577)正是解决这一问题的关键。

本文旨在系统性地介绍[张量不变量](@entry_id:203254)和[主值](@entry_id:189577)的理论及其应用。通过学习本文，您将深入理解这些概念如何为构建不依赖于坐标系的宏观描述符提供坚实的数学基础。
- 在“**原理与机制**”一章中，我们将深入探讨不变量和[主值](@entry_id:189577)的定义、它们与[谱分解](@entry_id:173707)和极分解的深刻联系，以及如何利用它们来构建满足[客观性原理](@entry_id:185412)的[本构关系](@entry_id:186508)。
- 随后，在“**应用与跨学科联系**”一章中，我们将展示这些理论概念如何在材料科学、生物医学工程、流体动力学乃至天体物理学等多个领域中发挥关键作用，解决实际的科学与工程问题。
- 最后，在“**动手实践**”部分，您将通过一系列精心设计的练习，巩固对核心概念的计算和理论推导能力。

让我们首先进入第一章，深入探索[张量不变量](@entry_id:203254)与[主值](@entry_id:189577)的基本原理与力学机制，揭示它们在现代科学与工程中的核心地位。

## 原理与机制

在[多尺度建模](@entry_id:154964)与分析中，我们致力于建立能够描述物理系统在不同尺度下行为的数学模型。一个核心挑战是确保这些模型是**客观的 (objective)**，即模型的预测不应依赖于观察者（或用于描述系统的坐标系）。[张量不变量](@entry_id:203254)和[主值](@entry_id:189577)是确保这种客观性的基石。本章将深入探讨这些基本概念的原理和机制，阐明它们在构建不依赖于坐标系的宏观描述符中的核心作用。

### 不变量的概念：为何至关重要

物理定律必须独立于观察者的参考系而存在。例如，一个材料样本的断裂强度是一个内在属性，其数值不应因为我们选择将坐标系的 x 轴指向东或指向北而改变。然而，描述该材料内部状态的张量（如[应力张量](@entry_id:148973)或应变张量）的**分量 (components)** 却确实依赖于坐标系的选择。

考虑一个由[二阶张量](@entry_id:199780) $\mathcal{A}$ 描述的物理状态。在某个[标准正交基](@entry_id:147779)下，这个张量由一个 $3 \times 3$ 的矩阵 $\boldsymbol{A}$ 表示。如果我们选择另一个[正交基](@entry_id:264024)，通过一个[正交矩阵](@entry_id:169220) $\boldsymbol{Q}$（满足 $\boldsymbol{Q}^{\top}\boldsymbol{Q}=\boldsymbol{I}$，其中 $\boldsymbol{I}$ 是单位矩阵）与原基底联系起来，那么在新的基底下，同一个张量 $\mathcal{A}$ 的[矩阵表示](@entry_id:146025)会变为 $\boldsymbol{A}'=\boldsymbol{Q}\boldsymbol{A}\boldsymbol{Q}^{\top}$。这个变换法则描述了张量分量如何随着坐标系的旋转或反射而改变。

显然，矩阵 $\boldsymbol{A}$ 的单个分量（例如 $A_{12}$）通常在变换后会发生改变（即 $A'_{12} \neq A_{12}$）。因此，单个分量不能作为物理状态的客观描述符。为了构建客观的标量描述符，我们需要寻找那些在任意[正交坐标](@entry_id:166074)变换下其值保持不变的函数。

一个标量函数 $f(\boldsymbol{A})$ 被称为在[正交基](@entry_id:264024)变换下的**不变量 (invariant)**，如果对于所有属于[正交群](@entry_id:152531) $\mathrm{O}(3)$ 的矩阵 $\boldsymbol{Q}$，该函数都满足：
$$ f(\boldsymbol{Q}\boldsymbol{A}\boldsymbol{Q}^{\top}) = f(\boldsymbol{A}) $$
这个条件确保了 $f$ 的值是张量 $\mathcal{A}$ 的内在属性，不依赖于我们选择的用于观察它的“镜头”或坐标系。在连续介质力学中，满足此条件的标量也被称为**客观的 (objective)** 或**标架无关的 (frame-indifferent)** 。

一个经典的非客观量的反例是柯西应力张量 $\boldsymbol{T}$ 的某个特定分量，比如 $T_{12}$。在坐标系旋转后，新的分量 $T'_{12}$ 通常会是所有原始分量的[线性组合](@entry_id:154743)，其值会发生变化。因此，$T_{12}$ 本身不能作为一个鲁棒的材料属性指标，例如用于定义材料的屈服或失效。相反，能够描述材料真实状态的量必须是客观的标量 。这就引出了张量的[主值](@entry_id:189577)和不变量的概念，它们是构建此类客观描述符的系统性方法。

### [对称张量](@entry_id:148092)的[主值](@entry_id:189577)与[主方向](@entry_id:276187)

在物理学和工程中遇到的许多重要张量，如柯西[应力张量](@entry_id:148973)、[小应变张量](@entry_id:754968)和[热导](@entry_id:189019)率张量（对于某些晶体类别），都是对称的。对称[二阶张量](@entry_id:199780)具有一些优美的数学性质，这些性质由**[谱定理](@entry_id:136620) (spectral theorem)** 保证。

[谱定理](@entry_id:136620)指出，对于任何一个实对称[二阶张量](@entry_id:199780) $\boldsymbol{T}$（在 $\mathbb{R}^{3 \times 3}$ 中由对称矩阵表示），必然存在：
1.  三个实数**特征值 (eigenvalues)** $\lambda_1, \lambda_2, \lambda_3$，它们被称为张量的**[主值](@entry_id:189577) (principal values)**。
2.  一组对应的**[特征向量](@entry_id:151813) (eigenvectors)** $\boldsymbol{n}_1, \boldsymbol{n}_2, \boldsymbol{n}_3$，它们构成一个[标准正交基](@entry_id:147779)（即彼此正交且长度为1）。这些向量定义了张量的**[主方向](@entry_id:276187) (principal directions)**。

特征值和[特征向量](@entry_id:151813)由[特征方程](@entry_id:265849) $\boldsymbol{T}\boldsymbol{n} = \lambda\boldsymbol{n}$ 定义。在物理上，[主方向](@entry_id:276187)是这样一些特殊的方向：当张量 $\boldsymbol{T}$ 作用于沿着这些方向的向量时，其效果仅仅是对该向量进行一次简单的缩放，而不会改变其方向。[主值](@entry_id:189577) $\lambda_i$ 就是对应[主方向](@entry_id:276187) $\boldsymbol{n}_i$ 上的缩放因子。

利用[主值](@entry_id:189577)和[主方向](@entry_id:276187)，任何[对称张量](@entry_id:148092) $\boldsymbol{T}$ 都可以被唯一地表示为其**[谱分解](@entry_id:173707) (spectral decomposition)** 形式：
$$ \boldsymbol{T} = \sum_{i=1}^{3} \lambda_i \boldsymbol{n}_i \otimes \boldsymbol{n}_i $$
其中 $\otimes$ 表示[张量积](@entry_id:140694)（或[外积](@entry_id:147029)），$\boldsymbol{n}_i \otimes \boldsymbol{n}_i$ 是一个[投影算子](@entry_id:154142)，它将任意[向量投影](@entry_id:147046)到[主方向](@entry_id:276187) $\boldsymbol{n}_i$ 上。这个表达式优雅地揭示了张量的内在结构：它在三个相互正交的[主方向](@entry_id:276187)上的作用被完全[解耦](@entry_id:160890)，每个方向的行为由其对应的[主值](@entry_id:189577)独立决定  。

当坐标系发生旋转时（由正交张量 $\boldsymbol{Q}$ 描述），张量 $\boldsymbol{T}$ 的表示变为 $\boldsymbol{T}' = \boldsymbol{Q}\boldsymbol{T}\boldsymbol{Q}^{\top}$。可以证明，新张量 $\boldsymbol{T}'$ 的[主值](@entry_id:189577)与原张量 $\boldsymbol{T}$ 完全相同（$\lambda'_i = \lambda_i$），而其[主方向](@entry_id:276187)则是原[主方向](@entry_id:276187)经过相同[旋转变换](@entry_id:200017)后的方向（$\boldsymbol{n}'_i = \boldsymbol{Q}\boldsymbol{n}_i$）。这意味着[主值](@entry_id:189577)本身就是不变量，因此它们是描述张量状态的理想候选者 。例如，柯西[应力张量](@entry_id:148973)的最大[主值](@entry_id:189577)（最大[主应力](@entry_id:176761)）是一个客观的标量，常被用作材料科学中的失效判据 。

### [主不变量](@entry_id:193522)

虽然[主值](@entry_id:189577)是客观的，但它们是三个独立的数。在许多应用中，我们希望用单个标量来表征张量的某些特定方面，例如它的大小或形状。这可以通过构造[主值](@entry_id:189577)的[对称函数](@entry_id:177113)来实现。一组特别重要且基础的函数被称为**[主不变量](@entry_id:193522) (principal invariants)**。

[主不变量](@entry_id:193522) $I_1, I_2, I_3$ 可以通过张量的**[特征多项式](@entry_id:150909) (characteristic polynomial)** 来定义。[特征多项式](@entry_id:150909)为 $p(\lambda) = \det(\boldsymbol{T} - \lambda\boldsymbol{I})$，其根正是张量的[主值](@entry_id:189577) $\lambda_1, \lambda_2, \lambda_3$。因此，该多项式可以写作：
$$ p(\lambda) = (\lambda_1 - \lambda)(\lambda_2 - \lambda)(\lambda_3 - \lambda) = -\lambda^3 + (\lambda_1+\lambda_2+\lambda_3)\lambda^2 - (\lambda_1\lambda_2+\lambda_2\lambda_3+\lambda_3\lambda_1)\lambda + \lambda_1\lambda_2\lambda_3 $$
通过将这个展开式与用张量分量表示的形式 $p(\lambda) = -\lambda^3 + I_1\lambda^2 - I_2\lambda + I_3$ 进行比较，我们立即得到了[主不变量](@entry_id:193522)与[主值](@entry_id:189577)之间的关系  ：
- **第一不变量 ($I_1$)**: $I_1 = \lambda_1 + \lambda_2 + \lambda_3$
- **第二不变量 ($I_2$)**: $I_2 = \lambda_1\lambda_2 + \lambda_2\lambda_3 + \lambda_3\lambda_1$
- **第三不变量 ($I_3$)**: $I_3 = \lambda_1\lambda_2\lambda_3$

这些不变量是[主值](@entry_id:189577)的**初等[对称多项式](@entry_id:153581)**。由于[主值](@entry_id:189577)本身是客观的，这些不变量自然也是客观的。它们的强大之处在于，它们也可以直接通过张量 $\boldsymbol{T}$ 的分量计算，而无需预先求解[特征值问题](@entry_id:142153)：
- $I_1(\boldsymbol{T}) = \mathrm{tr}(\boldsymbol{T})$
- $I_2(\boldsymbol{T}) = \frac{1}{2} \left[ (\mathrm{tr}(\boldsymbol{T}))^2 - \mathrm{tr}(\boldsymbol{T}^2) \right]$
- $I_3(\boldsymbol{T}) = \det(\boldsymbol{T})$

这里，$\mathrm{tr}(\boldsymbol{T})$ 是张量的**迹 (trace)**，即其对角线元素之和，而 $\det(\boldsymbol{T})$ 是其**行列式 (determinant)**。[迹和行列式](@entry_id:149685)是矩阵理论中最基本的不变量，在任何[相似变换](@entry_id:152935)（包括[正交变换](@entry_id:155650)）下都保持不变。这些公式为计算不变量提供了非常实用的方法 。

在连续介质力学中，[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ 通常被分解为一个**球形 (spherical)** 部分和一个**偏（离）(deviatoric)** 部分。球形部分与体积变化相关，而偏离部分与形状改变（剪切）相关。[偏应力张量](@entry_id:267642)定义为 $\boldsymbol{s} = \boldsymbol{\sigma} - \frac{1}{3}I_1(\boldsymbol{\sigma})\boldsymbol{I}$。这个张量的一个重要不变量是它的第二不变量 $J_2$，定义为 $J_2 = \frac{1}{2}\boldsymbol{s}:\boldsymbol{s} = \frac{1}{2}\mathrm{tr}(\boldsymbol{s}^2)$。可以证明，[偏应力张量](@entry_id:267642) $\boldsymbol{s}$ 与原[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ 具有相同的[主方向](@entry_id:276187)，其[主值](@entry_id:189577)为 $s_i = \sigma_i - \frac{1}{3}I_1$。利用这一点，$J_2$ 可以用[主应力](@entry_id:176761)表示为一个与[剪切变形](@entry_id:170920)密切相关的量：
$$ J_2 = \frac{1}{6}\left[(\sigma_1-\sigma_2)^2+(\sigma_2-\sigma_3)^2+(\sigma_3-\sigma_1)^2\right] $$
这个形式清晰地表明，$J_2$ 衡量了[主应力](@entry_id:176761)之间的差异，因此它成为了[金属塑性](@entry_id:176585)理论（如 von Mises [屈服准则](@entry_id:193897)）中的核心度量 。

### 非[对称张量](@entry_id:148092)的情况：变形、拉伸与奇异值

并非所有重要的物理张量都是对称的。一个典型的例子是**变形梯度张量 (deformation gradient tensor)** $\boldsymbol{F}$，它描述了材料微元的局部变形，将未变形构型中的向量映射到变形后构型中的向量。通常情况下，$\boldsymbol{F}$ 是非对称的。

对于非[对称张量](@entry_id:148092)，特征值可能是复数，[特征向量](@entry_id:151813)也未必正交，这使得基于[主值](@entry_id:189577)和[主方向](@entry_id:276187)的分析变得复杂。为了处理这种情况，我们引入了**极分解 (polar decomposition)** 定理。该定理指出，任何可逆的张量 $\boldsymbol{F}$（在物理上对应于不会将体积压缩至零的变形）都可以唯一地分解为：
$$ \boldsymbol{F} = \boldsymbol{R}\boldsymbol{U} = \boldsymbol{V}\boldsymbol{R} $$
其中：
- $\boldsymbol{R}$ 是一个正交张量，代表了变形过程中的**[刚体](@entry_id:1131033)旋转 (rigid body rotation)**。如果变形是保向的（即 $\det(\boldsymbol{F}) > 0$），那么 $\boldsymbol{R}$ 是一个纯旋转（$\det(\boldsymbol{R})=+1$）。
- $\boldsymbol{U}$ 和 $\boldsymbol{V}$ 是对称且正定的张量，分别称为**右[拉伸张量](@entry_id:193200) (right stretch tensor)** 和**左[拉伸张量](@entry_id:193200) (left stretch tensor)**。它们描述了变形中的纯拉伸或压缩，即形状的改变。

极分解的物理意义在于它将复杂的变形过程[解耦](@entry_id:160890)为一个纯粹的拉伸（由 $\boldsymbol{U}$ 或 $\boldsymbol{V}$ 描述）和一个纯粹的[刚体](@entry_id:1131033)旋转（由 $\boldsymbol{R}$ 描述）。

由于 $\boldsymbol{U}$ 和 $\boldsymbol{V}$ 是对称的，我们可以分析它们的[谱分解](@entry_id:173707)。$\boldsymbol{U}$ 和 $\boldsymbol{V}$ 的特征值（始终为正实数）被称为**主拉伸 (principal stretches)**，记为 $\lambda_i$。它们量化了材料在三个相互正交的主拉伸方向上的伸长或缩短程度。

现在，我们可以将非[对称张量](@entry_id:148092) $\boldsymbol{F}$ 与其他[对称张量](@entry_id:148092)联系起来。两个重要的[对称张量](@entry_id:148092)是**[右柯西-格林张量](@entry_id:174156) (right Cauchy-Green tensor)** $\boldsymbol{C} = \boldsymbol{F}^{\top}\boldsymbol{F}$ 和**[左柯西-格林张量](@entry_id:186163) (left Cauchy-Green tensor)** $\boldsymbol{B} = \boldsymbol{F}\boldsymbol{F}^{\top}$。利用极分解，我们发现：
$$ \boldsymbol{C} = \boldsymbol{F}^{\top}\boldsymbol{F} = (\boldsymbol{R}\boldsymbol{U})^{\top}(\boldsymbol{R}\boldsymbol{U}) = \boldsymbol{U}^{\top}\boldsymbol{R}^{\top}\boldsymbol{R}\boldsymbol{U} = \boldsymbol{U}^2 $$
$$ \boldsymbol{B} = \boldsymbol{F}\boldsymbol{F}^{\top} = (\boldsymbol{V}\boldsymbol{R})(\boldsymbol{V}\boldsymbol{R})^{\top} = \boldsymbol{V}\boldsymbol{R}\boldsymbol{R}^{\top}\boldsymbol{V}^{\top} = \boldsymbol{V}^2 $$
这些关系至关重要。它们表明，$\boldsymbol{C}$ 和 $\boldsymbol{B}$ 的特征值分别是主拉伸的平方，即 $\lambda_i^2$。

这就引出了**[奇异值](@entry_id:152907) (singular values)** 的概念。对于任意矩阵（或[二阶张量](@entry_id:199780)）$\boldsymbol{F}$，其[奇异值](@entry_id:152907) $\sigma_i$ 定义为[对称正定矩阵](@entry_id:136714) $\boldsymbol{F}^{\top}\boldsymbol{F}$ 的特征值的非负平方根。根据我们刚刚的推导，$\boldsymbol{F}^{\top}\boldsymbol{F} = \boldsymbol{C}$，而 $\boldsymbol{C}$ 的特征值是 $\lambda_i^2$。因此，变形梯度 $\boldsymbol{F}$ 的奇异值正是主拉伸 $\lambda_i$。
$$ \sigma_i(\boldsymbol{F}) = \sqrt{\text{eig}(\boldsymbol{F}^{\top}\boldsymbol{F})_i} = \sqrt{\lambda_i^2} = \lambda_i $$
这一结论将非[对称张量](@entry_id:148092) $\boldsymbol{F}$ 的[奇异值](@entry_id:152907)与描述其纯变形部分的[对称张量](@entry_id:148092) $\boldsymbol{U}$ 的[主值](@entry_id:189577)（即主拉伸）直接等同起来，为分析非[对称张量](@entry_id:148092)的“大小”提供了一个坚实的基础 。

### 更深层次的不变性：特征值与[奇异值](@entry_id:152907)

我们已经看到，对于不同的变换，不同的量会保持不变。这值得我们做更深入的区分 。
1.  **[相似变换](@entry_id:152935)下的不变量（特征值）**：当一个张量 $\boldsymbol{A}$ 经历**[相似变换](@entry_id:152935) (similarity transformation)** $\boldsymbol{A}' = \boldsymbol{Q}^{-1}\boldsymbol{A}\boldsymbol{Q}$（对于[正交变换](@entry_id:155650)，这与 $\boldsymbol{Q}^{\top}\boldsymbol{A}\boldsymbol{Q}$ 相同）时，其**特征值 (eigenvalues)** 保持不变。这种变换在物理上对应于对张量作用的“空间”的基底进行改变（即观察者坐标系的改变）。因此，特征值是张量在单一坐标系下的内在谱属性。

2.  **左右[正交变换](@entry_id:155650)下的不变量（[奇异值](@entry_id:152907)）**：当一个张量 $\boldsymbol{A}$ 经历更广义的**左右正交作用 (left-right orthogonal action)** $\boldsymbol{A}' = \boldsymbol{U}^{\top}\boldsymbol{A}\boldsymbol{V}$ 时（其中 $\boldsymbol{U}$ 和 $\boldsymbol{V}$ 是两个独立的[正交矩阵](@entry_id:169220)），其**奇异值 (singular values)** 保持不变，但特征值通常会改变。这种变换可以被看作是张量所关联的两个空间（[定义域和陪域](@entry_id:159300)）各自独立地改变了基底。

一个具体的例子可以很好地说明这一点。考虑一个[对称张量](@entry_id:148092) $\boldsymbol{A} = \begin{pmatrix} 1  0 \\ 0  -1 \end{pmatrix}$，其特征值为 $\{1, -1\}$，[奇异值](@entry_id:152907)为 $\{1, 1\}$。现在让它经历一个左右变换，其中 $\boldsymbol{U} = \begin{pmatrix} 0  1 \\ 1  0 \end{pmatrix}$（一个反射/[置换矩阵](@entry_id:136841)），$\boldsymbol{V} = \boldsymbol{I}$。变换后的张量为 $\boldsymbol{B} = \boldsymbol{U}^{\top}\boldsymbol{A}\boldsymbol{V} = \begin{pmatrix} 0  -1 \\ 1  0 \end{pmatrix}$。这是一个[斜对称张量](@entry_id:199349)，代表一个纯旋转。它的特征值是复数 $\{i, -i\}$，与原始特征值完全不同。然而，通过计算 $\boldsymbol{B}^{\top}\boldsymbol{B} = \boldsymbol{I}$，我们发现其奇异值仍然是 $\{1, 1\}$，保持不变。

这个例子揭示了一个深刻的道理：特征值描述了一个变换（张量）作用于某个空间并回到**相同**空间时的拉伸和旋转特性，而奇异值则描述了一个变换从**一个**空间到**另一个**空间时的纯粹“拉伸”或“放大”效应，完全剥离了旋转的影响。在连续介质力学中，变形梯度 $\boldsymbol{F}$ 将未变形构型映射到变形构型，这正是[奇异值](@entry_id:152907)（即主拉伸）成为描述纯变形的[正确度](@entry_id:197374)量的根本原因。

### 在[本构模型](@entry_id:174726)中的应用

[张量不变量](@entry_id:203254)和[主值](@entry_id:189577)的理论在建立材料的**[本构关系](@entry_id:186508) (constitutive relations)**（即[应力与应变](@entry_id:137374)之间的关系）时发挥着核心作用，尤其是在描述[超弹性材料](@entry_id:190241)时。

对于一个[超弹性材料](@entry_id:190241)，其力学行为由一个**[应变能密度函数](@entry_id:755490) (stored-energy function)** $W(\boldsymbol{F})$ 完全决定。这个函数必须满足两个基本物理原理 ：
1.  **[客观性原理](@entry_id:185412) (Principle of Objectivity)**：能量不应随观察者的[刚体运动](@entry_id:144691)而改变。这意味着对于任意旋转 $\boldsymbol{Q}$，必须有 $W(\boldsymbol{F}) = W(\boldsymbol{Q}\boldsymbol{F})$。由于极分解 $\boldsymbol{F}=\boldsymbol{R}\boldsymbol{U}$，这个条件意味着能量函数实际上不能依赖于旋转部分 $\boldsymbol{R}$，而只能依赖于拉伸部分 $\boldsymbol{U}$，即 $W(\boldsymbol{F}) = \widehat{W}(\boldsymbol{U})$。因为 $\boldsymbol{U} = \sqrt{\boldsymbol{C}}$，这等价于能量可以表示为[右柯西-格林张量](@entry_id:174156) $\boldsymbol{C}$ 的函数，即 $\widetilde{W}(\boldsymbol{C})$。

2.  **[材料对称性](@entry_id:190289)原理 (Principle of Material Symmetry)**：材料的响应可能在某些方向上是相同的。对于**各向同性 (isotropic)** 材料，其响应在所有方向上都是相同的。这意味着[应变能函数](@entry_id:178435)对于施加在参考构型上的任意旋转 $\boldsymbol{Q}$ 都应保持不变，即 $\widetilde{W}(\boldsymbol{C}) = \widetilde{W}(\boldsymbol{Q}^{\top}\boldsymbol{C}\boldsymbol{Q})$。根据[各向同性张量函数的表示定理](@entry_id:754252)，任何满足此条件的标量函数都必须可以表示为其张量宗量的[主不变量](@entry_id:193522)的函数。

综合这两个原理，我们得出一个强大的结论：对于一个各向同性的[超弹性材料](@entry_id:190241)，其[应变能密度函数](@entry_id:755490)必然可以表示为柯西-格林张量 $\boldsymbol{C}$ 的三个[主不变量](@entry_id:193522)的函数：
$$ W = W(I_1(\boldsymbol{C}), I_2(\boldsymbol{C}), I_3(\boldsymbol{C})) $$
这个结论极大地简化了本构模型的构建，将一个复杂的张量函数简化为了一个仅有三个标量变量的函数。例如，一种常见的可压缩 Neo-Hookean 模型就具有这种形式：$W = \frac{\mu}{2}(I_1(\boldsymbol{C}) - 3) - \mu \ln J + \frac{\kappa}{2}(\ln J)^2$，其中 $J = \det(\boldsymbol{F}) = \sqrt{I_3(\boldsymbol{C})}$ 是体积变化率，$\mu$ 和 $\kappa$ 是材料参数 。

### 高级主题：[重根](@entry_id:151486)与[可微性](@entry_id:140863)

在理论和应用的深入探讨中，我们会遇到一些更微妙的情况。

#### [重根](@entry_id:151486)与[材料对称性](@entry_id:190289)

当一个[对称张量](@entry_id:148092)的两个或三个[主值](@entry_id:189577)相等时（即特征值出现**[重根](@entry_id:151486) (repeated eigenvalues)**），其[主方向](@entry_id:276187)将不再是唯一的。例如，如果 $\lambda_1 = \lambda_2 \neq \lambda_3$，那么任何在由 $\boldsymbol{n}_1$ 和 $\boldsymbol{n}_2$ 张成的平面内的[单位向量](@entry_id:165907)都是对应于特征值 $\lambda_1$ 的有效[主方向](@entry_id:276187)。这个平面被称为一个二维的**[特征空间](@entry_id:638014) (eigenspace)**。

这种情况在物理上对应于更高层次的[材料对称性](@entry_id:190289)。例如，$\lambda_1=\lambda_2 \neq \lambda_3$ 的情况对应于**横观各向同性 (transverse isotropy)**，即材料在一个特定方向（由 $\boldsymbol{n}_3$ 定义的轴）上具有独特的性质，但在垂直于该轴的平面内是各向同性的。如果所有三个[主值](@entry_id:189577)都相等（$\lambda_1=\lambda_2=\lambda_3$），则张量是球形的（$\boldsymbol{T} = \lambda\boldsymbol{I}$），材料在所有方向上都表现出相同的行为，即完全各向同性 。

尽管[主方向](@entry_id:276187)在这种情况下变得不唯一，但[主不变量](@entry_id:193522)作为[主值](@entry_id:189577)的[对称函数](@entry_id:177113)，其定义和值完全不受影响。这再次凸显了不变量作为鲁棒描述符的优势。

#### [谱函数](@entry_id:147628)的[可微性](@entry_id:140863)

在进行[灵敏度分析](@entry_id:147555)或基于梯度的优化时，我们需要考虑不变量和[主值](@entry_id:189577)对张量变化的**[可微性](@entry_id:140863) (differentiability)**。这是一个精细的数学问题，尤其是在存在[重根](@entry_id:151486)的情况下 。

- **不变量的[可微性](@entry_id:140863)**：[主不变量](@entry_id:193522) $I_1, I_2, I_3$ 是张量分量的多项式函数。因此，它们在任何地方都是无限次光滑可微的，即使在[主值](@entry_id:189577)发生重合的点也是如此。更广泛地说，任何作为[主值](@entry_id:189577)的对称**多项式**的[谱函数](@entry_id:147628)都具有良好的[可微性](@entry_id:140863)。这是基于不变量的本构模型在数值计算中表现稳健的一个关键原因。

- **[主值](@entry_id:189577)的[可微性](@entry_id:140863)**：与此相反，**单个的**、经过排序的[主值](@entry_id:189577)（例如，最大[主值](@entry_id:189577) $\lambda_{\max}$ 或最小[主值](@entry_id:189577) $\lambda_{\min}$）在[主值](@entry_id:189577)重合的点通常是**不可微的**（在严格的 Fréchet 意义上）。它们在这些点上会形成“尖点”或“棱”，就像函数 $|x|$ 在 $x=0$ 处不可微一样。然而，对于许多重要的[谱函数](@entry_id:147628)（如 $\lambda_{\max}$），即使它们不是 Fréchet 可微的，它们仍然是凸函数，并且在所有方向上都存在[方向导数](@entry_id:189133)。这一特性在变分原理和[凸优化](@entry_id:137441)中至关重要。

总之，[张量不变量](@entry_id:203254)和[主值](@entry_id:189577)不仅为我们提供了独立于坐标系的、描述物理状态的客观工具，而且还构成了理解[材料对称性](@entry_id:190289)、构建本构关系以及分析复杂多尺度[模型稳定性](@entry_id:636221)和灵敏度的数学基础。