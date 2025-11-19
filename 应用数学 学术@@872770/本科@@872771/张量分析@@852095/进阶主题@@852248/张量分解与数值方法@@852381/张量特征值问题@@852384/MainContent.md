## 引言
在物理学和工程学中，张量是描述多向性物理量的强大数学工具，从材料的[应力应变](@entry_id:204183)状态到刚体的转动惯性，其应用无处不在。然而，一个张量的分量会随着[坐标系](@entry_id:156346)的改变而变化，这使得直接从分量中提取其内在物理意义变得困难。为了解决这一问题，我们需要找到一种方法来揭示张量固有的、不依赖于观察者[坐标系](@entry_id:156346)选择的本质属性。[张量特征值问题](@entry_id:198059)正是解决这一核心问题的关键。

本文旨在系统地引导读者深入理解[张量特征值问题](@entry_id:198059)的理论与实践。通过学习，你将能够从一个给定的张量中，提炼出其最根本的特性——[主值](@entry_id:189577)（[特征值](@entry_id:154894)）和[主方向](@entry_id:276187)（[特征向量](@entry_id:151813)）。我们将在第一章“原理与机制”中，从基本定义出发，建立求解[特征值问题](@entry_id:142153)的数学框架，包括特征方程、[主不变量](@entry_id:193522)以及对称张量的谱定理。随后，在第二章“应用与交叉学科联系”中，我们将展示这些理论如何在[连续介质力学](@entry_id:155125)、[刚体动力学](@entry_id:142040)、几何学乃至数据科学等多个领域中发挥作用，将抽象的数学概念与具体的物理现象和工程应用紧密相连。最后，通过第三章“动手实践”中的一系列精选问题，你将有机会亲手计算和应用所学知识，从而巩固和深化对这一重要课题的理解。

## 原理与机制

在对物理系统进行张量描述时，我们常常关心那些在张量作用下其方向保持不变的特殊方向。这些方向，被称为张量的主方向或[特征向量](@entry_id:151813)，揭示了系统固有的、不依赖于[坐标系](@entry_id:156346)选择的内在属性。与之对应的标量缩放因子，即主值或[特征值](@entry_id:154894)，量化了在这些[主方向](@entry_id:276187)上张量作用的强度。本章将深入探讨[张量特征值问题](@entry_id:198059)的核心原理与基本机制，这些是理解连续介质力学、[材料科学](@entry_id:152226)和[刚体动力学](@entry_id:142040)等领域中诸多现象的基础。

### [张量特征值问题](@entry_id:198059)的定义

对于一个给定的二阶张量 $\mathbf{T}$ 和一个非[零向量](@entry_id:156189) $\mathbf{v}$，如果 $\mathbf{T}$ 对 $\mathbf{v}$ 的作用仅仅是将其长度进行缩放，而其方向保持不变，那么我们就称 $\mathbf{v}$ 是 $\mathbf{T}$ 的一个**[特征向量](@entry_id:151813)**（eigenvector），相应的缩放因子 $\lambda$ 称为**[特征值](@entry_id:154894)**（eigenvalue）。这个关系可以用以下方程来表示：

$$
\mathbf{T}\mathbf{v} = \lambda\mathbf{v}
$$

这个方程是[张量分析](@entry_id:161423)的核心方程之一，被称为**[特征值方程](@entry_id:192306)**。在不同的物理背景下，[特征向量](@entry_id:151813)和[特征值](@entry_id:154894)具有不同的名称和意义。例如，在连续介质力学中，[应力张量](@entry_id:148973) $\mathbf{T}$ 的[特征向量](@entry_id:151813)被称为**[主应力方向](@entry_id:753737)**，而其[特征值](@entry_id:154894)则被称为**[主应力](@entry_id:176761)**，它们代表了作用在某些特定平面上且只有正应力而无剪应力的应力值。

为了具体理解这一概念，我们可以通过一个简单的验证来入门。考虑在某材料点处的应力状态由一个二阶[对称张量](@entry_id:148092) $\mathbf{T}$ 描述，其在标准笛卡尔基下的分量矩阵为：
$$
[T] = \begin{pmatrix} 2 & 3 & 4 \\ 3 & 3 & 1 \\ 4 & 1 & 10 \end{pmatrix}
$$
现在，我们想考察方向由向量 $\mathbf{v}$（其分量为 $[1, 2, -1]^T$）表示的平面。为了判断 $\mathbf{v}$ 是否为一个[主应力方向](@entry_id:753737)，我们只需计算 $\mathbf{T}\mathbf{v}$ 并检查结果是否与 $\mathbf{v}$ 共线 [@problem_id:1543026]。

$$
[T][v] = \begin{pmatrix} 2 & 3 & 4 \\ 3 & 3 & 1 \\ 4 & 1 & 10 \end{pmatrix} \begin{pmatrix} 1 \\ 2 \\ -1 \end{pmatrix} = \begin{pmatrix} 2(1) + 3(2) + 4(-1) \\ 3(1) + 3(2) + 1(-1) \\ 4(1) + 1(2) + 10(-1) \end{pmatrix} = \begin{pmatrix} 4 \\ 8 \\ -4 \end{pmatrix}
$$

观察计算结果，我们发现：
$$
\begin{pmatrix} 4 \\ 8 \\ -4 \end{pmatrix} = 4 \begin{pmatrix} 1 \\ 2 \\ -1 \end{pmatrix} = 4[v]
$$

由于 $\mathbf{T}\mathbf{v} = 4\mathbf{v}$，计算结果满足[特征值方程](@entry_id:192306)的形式。因此，向量 $\mathbf{v}$ 确实是一个主方向，其对应的[主应力](@entry_id:176761)（[特征值](@entry_id:154894)）为 $\lambda=4$。这表明，沿着 $\mathbf{v}$ 方向的法平面上，材料受到的牵[引力](@entry_id:175476)方向与法向完全一致，其大小是法向单位长度的4倍。

### 特征方程与[主不变量](@entry_id:193522)

验证一个给定的向量是否为[特征向量](@entry_id:151813)是直接的，但我们如何系统地找出所有未知的[特征值](@entry_id:154894)和[特征向量](@entry_id:151813)呢？为此，我们需要求解[特征值方程](@entry_id:192306)。将方程 $\mathbf{T}\mathbf{v} = \lambda\mathbf{v}$ 稍作变形，可以写作：

$$
(\mathbf{T} - \lambda\mathbf{I})\mathbf{v} = \mathbf{0}
$$

其中 $\mathbf{I}$ 是二阶单位张量。这个方程是一个[齐次线性方程组](@entry_id:153432)。根据线性代数的知识，要使该方程存在非零解（即 $\mathbf{v} \neq \mathbf{0}$），系数矩阵（或张量） $\mathbf{T} - \lambda\mathbf{I}$ 必须是奇异的，这意味着它的[行列式](@entry_id:142978)必须为零：

$$
\det(\mathbf{T} - \lambda\mathbf{I}) = 0
$$

这个方程被称为**特征方程**（characteristic equation）。它是一个关于 $\lambda$ 的多项式方程，其根就是张量 $\mathbf{T}$ 的所有[特征值](@entry_id:154894)。对于一个在 $n$ 维空间中的二阶张量，特征方程是一个 $n$ 次多项式，因此它有 $n$ 个（可能重复的）复数根。

以一个二维平面应力问题为例 [@problem_id:1542996]，假设应力张量 $\boldsymbol{\sigma}$ 的矩阵表示为：
$$
\boldsymbol{\sigma} = \begin{pmatrix} 80.0 & 30.0 \\ 30.0 & 20.0 \end{pmatrix}
$$
其特征方程为：
$$
\det(\boldsymbol{\sigma} - \lambda\mathbf{I}) = \det\begin{pmatrix} 80.0 - \lambda & 30.0 \\ 30.0 & 20.0 - \lambda \end{pmatrix} = 0
$$
展开[行列式](@entry_id:142978)得到一个关于 $\lambda$ 的二次多项式：
$$
(80.0 - \lambda)(20.0 - \lambda) - (30.0)^2 = \lambda^2 - 100\lambda + 1600 - 900 = \lambda^2 - 100\lambda + 700 = 0
$$
解这个[二次方程](@entry_id:163234)可以得到两个[主应力](@entry_id:176761)（[特征值](@entry_id:154894)） $\lambda_1 \approx 92.4$ MPa 和 $\lambda_2 \approx 7.57$ MPa。一旦求出[特征值](@entry_id:154894)，例如 $\lambda_1$，就可以将其代回方程 $(\boldsymbol{\sigma} - \lambda_1\mathbf{I})\mathbf{v}_1 = \mathbf{0}$ 来求解对应的[特征向量](@entry_id:151813) $\mathbf{v}_1$。

对于三维空间中的张量，特征方程是一个三次多项式，通常写作：
$$
\lambda^3 - I_1\lambda^2 + I_2\lambda - I_3 = 0
$$
这里的系数 $I_1, I_2, I_3$ 是张量 $\mathbf{T}$ 的**[主不变量](@entry_id:193522)**（principal invariants）。它们之所以被称为“[不变量](@entry_id:148850)”，是因为它们的值不随[坐标系](@entry_id:156346)的旋转而改变，是张量内在的属性。这些[不变量](@entry_id:148850)可以由张量的分量计算得出：

- **第一[不变量](@entry_id:148850) $I_1$**: 张量的**迹**（trace），即主对角线元素之和。
  $$ I_1 = \operatorname{tr}(\mathbf{T}) = T_{ii} $$
- **第二[不变量](@entry_id:148850) $I_2$**: 张量矩阵所有主对角 $2 \times 2$ 子式之和。
  $$ I_2 = \frac{1}{2}[(\operatorname{tr}(\mathbf{T}))^2 - \operatorname{tr}(\mathbf{T}^2)] $$
- **第三[不变量](@entry_id:148850) $I_3$**: 张量的**[行列式](@entry_id:142978)**（determinant）。
  $$ I_3 = \det(\mathbf{T}) $$

例如，对于[应力张量](@entry_id:148973) [@problem_id:1542994]
$$
\mathbf{S} = \begin{pmatrix} 3 & 1 & 1 \\ 1 & 0 & 2 \\ 1 & 2 & 0 \end{pmatrix}
$$
我们可以计算其[主不变量](@entry_id:193522)：
$$
I_1 = \operatorname{tr}(\mathbf{S}) = 3 + 0 + 0 = 3
$$
$$
I_2 = \det\begin{pmatrix} 0 & 2 \\ 2 & 0 \end{pmatrix} + \det\begin{pmatrix} 3 & 1 \\ 1 & 0 \end{pmatrix} + \det\begin{pmatrix} 3 & 1 \\ 1 & 0 \end{pmatrix} = -4 - 1 - 1 = -6
$$
$$
I_3 = \det(\mathbf{S}) = 3(0-4) - 1(0-2) + 1(2-0) = -12 + 2 + 2 = -8
$$
因此，该[应力张量](@entry_id:148973)的特征方程为 $\lambda^3 - 3\lambda^2 - 6\lambda + 8 = 0$。

[主不变量](@entry_id:193522)与[特征值](@entry_id:154894)之间也存在直接的代数关系（[韦达定理](@entry_id:150627)）：
$$
I_1 = \lambda_1 + \lambda_2 + \lambda_3
$$
$$
I_2 = \lambda_1\lambda_2 + \lambda_2\lambda_3 + \lambda_3\lambda_1
$$
$$
I_3 = \lambda_1\lambda_2\lambda_3
$$
这些关系非常有用。例如，如果我们知道一个三阶张量的三个[特征值](@entry_id:154894)分别为 $4$, $3$, 和 $-5$，我们就可以立即确定它的[迹和行列式](@entry_id:149685) [@problem_id:1543025]：
$$
\operatorname{tr}(\mathbf{A}) = 4 + 3 + (-5) = 2
$$
$$
\det(\mathbf{A}) = 4 \times 3 \times (-5) = -60
$$
特别地，[行列式](@entry_id:142978) $I_3$ 的值直接关系到张量是否可逆。一个张量是可逆的，当且仅当其[行列式](@entry_id:142978)不为零，这等价于它没有任何一个[特征值](@entry_id:154894)为零 [@problem_id:1542997]。如果一个张量的[行列式](@entry_id:142978)为零，那么它至少有一个零[特征值](@entry_id:154894)，此时该张量是奇异的或不可逆的。

### [对称张量](@entry_id:148092)的谱性质

在物理和工程学中遇到的大多数二阶张量，如[应力张量](@entry_id:148973)、应变张量和[惯性张量](@entry_id:148659)，都是**对称张量**（即 $\mathbf{T} = \mathbf{T}^T$，或 $T_{ij} = T_{ji}$）。对称性赋予了[张量特征值问题](@entry_id:198059)两个至关重要的性质，这构成了所谓的**[谱定理](@entry_id:136620)**（Spectral Theorem）的基础：

1.  **对称张量的[特征值](@entry_id:154894)总是实数。** 这在物理上是合乎情理的，因为像[主应力](@entry_id:176761)、[主应变](@entry_id:197797)或[主转动惯量](@entry_id:150889)这样的物理量都应该是实数。

2.  **对应于不同[特征值](@entry_id:154894)的[特征向量](@entry_id:151813)是相互正交的。** 也就是说，如果 $\lambda_1 \neq \lambda_2$，则它们对应的[特征向量](@entry_id:151813) $\mathbf{v}_1$ 和 $\mathbf{v}_2$ 满足 $\mathbf{v}_1 \cdot \mathbf{v}_2 = 0$。

我们可以通过一个具体的例子来验证第二条性质 [@problem_id:1543001]。考虑对称张量：
$$
[T] = \begin{pmatrix} 5 & 2 \\ 2 & 8 \end{pmatrix}
$$
其[特征方程](@entry_id:265849)为 $(\lambda-4)(\lambda-9)=0$，得到两个不同的[特征值](@entry_id:154894) $\lambda_1 = 9$ 和 $\lambda_2 = 4$。
对于 $\lambda_1=9$，[特征向量](@entry_id:151813)满足 $([T]-9\mathbf{I})\mathbf{v}_1=\mathbf{0}$，即 $\begin{pmatrix} -4 & 2 \\ 2 & -1 \end{pmatrix}\mathbf{v}_1=\mathbf{0}$，可得一个[特征向量](@entry_id:151813) $\mathbf{v}_1 = \begin{pmatrix} 1 \\ 2 \end{pmatrix}$。
对于 $\lambda_2=4$，[特征向量](@entry_id:151813)满足 $([T]-4\mathbf{I})\mathbf{v}_2=\mathbf{0}$，即 $\begin{pmatrix} 1 & 2 \\ 2 & 4 \end{pmatrix}\mathbf{v}_2=\mathbf{0}$，可得一个[特征向量](@entry_id:151813) $\mathbf{v}_2 = \begin{pmatrix} 2 \\ -1 \end{pmatrix}$。
计算这两个[特征向量](@entry_id:151813)的[点积](@entry_id:149019)：
$$
\mathbf{v}_1 \cdot \mathbf{v}_2 = (1)(2) + (2)(-1) = 2 - 2 = 0
$$
结果为零，证实了它们是正交的。

如果一个[特征值](@entry_id:154894)有多个[线性无关](@entry_id:148207)的[特征向量](@entry_id:151813)（即[特征值](@entry_id:154894)是[重根](@entry_id:151486)），我们总可以在该[特征值](@entry_id:154894)的特征[子空间](@entry_id:150286)中选出一组正交的[基向量](@entry_id:199546)。因此，对于任何一个 $n$ 维空间中的对称二阶张量，我们总能找到一组 $n$ 个相互正交的、归一化的[特征向量](@entry_id:151813)。这组向量 $\{\mathbf{e}_1, \mathbf{e}_2, \dots, \mathbf{e}_n\}$ 构成了一个标准正交基，被称为张量的**主基**或**[特征基](@entry_id:151409)**。

### 谱分解定理

能够找到一个由[特征向量](@entry_id:151813)构成的标准正交基，这一事实引出了一个极为优美的表示方法，称为**[谱分解](@entry_id:173707)**（spectral decomposition）或**[谱表示](@entry_id:153219)**。任何对称的二阶张量 $\mathbf{S}$ 都可以表示为其[特征值](@entry_id:154894)和对应[特征向量](@entry_id:151813)的外积的[线性组合](@entry_id:154743)：

$$
\mathbf{S} = \sum_{i=1}^{n} \lambda_i (\mathbf{e}_i \otimes \mathbf{e}_i)
$$

在这里，$\lambda_i$ 是[特征值](@entry_id:154894)，$\mathbf{e}_i$ 是对应的归一化[特征向量](@entry_id:151813)。$\mathbf{P}_i = \mathbf{e}_i \otimes \mathbf{e}_i$ 是一个**投影张量**，它将任意[向量投影](@entry_id:147046)到由 $\mathbf{e}_i$ 张成的方向上。在矩阵形式中，$\mathbf{e}_i \otimes \mathbf{e}_i$ 对应于矩阵 $\mathbf{e}_i \mathbf{e}_i^T$。

[谱分解](@entry_id:173707)的几何意义是：任何[对称张量](@entry_id:148092)所代表的[线性变换](@entry_id:149133)，都可以分解为沿着一组正交的[主方向](@entry_id:276187)的一系列独立拉伸（或压缩），拉伸的比例就是相应的[特征值](@entry_id:154894)。

让我们看一个例子 [@problem_id:1543017]。给定一个对称张量：
$$
[S] = \begin{pmatrix} 4 & 2 \\ 2 & 1 \end{pmatrix}
$$
其[特征值](@entry_id:154894)为 $\lambda_1=5$ 和 $\lambda_2=0$。非零[特征值](@entry_id:154894)是 $\lambda_1=5$。对应的归一化[特征向量](@entry_id:151813)为 $\mathbf{e}_1 = \frac{1}{\sqrt{5}}\begin{pmatrix} 2 \\ 1 \end{pmatrix}$。与零[特征值](@entry_id:154894) $\lambda_2=0$ 对应的[特征向量](@entry_id:151813)为 $\mathbf{e}_2 = \frac{1}{\sqrt{5}}\begin{pmatrix} -1 \\ 2 \end{pmatrix}$。
与非零[特征值](@entry_id:154894) $\lambda_1=5$ 相关联的投影张量 $\mathbf{P}_1 = \mathbf{e}_1 \otimes \mathbf{e}_1$ 的分量为 $(P_1)_{ij} = (\mathbf{e}_1)_i (\mathbf{e}_1)_j$。例如，其 (1, 2) 分量为：
$$
(P_1)_{12} = \left(\frac{2}{\sqrt{5}}\right) \left(\frac{1}{\sqrt{5}}\right) = \frac{2}{5} = 0.4
$$
根据谱分解，我们有：
$$
\mathbf{S} = \lambda_1 (\mathbf{e}_1 \otimes \mathbf{e}_1) + \lambda_2 (\mathbf{e}_2 \otimes \mathbf{e}_2) = 5 (\mathbf{e}_1 \otimes \mathbf{e}_1) + 0 (\mathbf{e}_2 \otimes \mathbf{e}_2) = 5(\mathbf{e}_1 \otimes \mathbf{e}_1)
$$
这表明张量 $\mathbf{S}$ 的作用等效于将一个[向量投影](@entry_id:147046)到 $\mathbf{e}_1$ 方向，然后将其长度拉伸5倍。

### [特征值](@entry_id:154894)的[不变性](@entry_id:140168)与物理意义

张量的一个最根本的特性是，它的物理意义独立于我们用来描述它的[坐标系](@entry_id:156346)。[特征值](@entry_id:154894)和[特征向量](@entry_id:151813)正是这种不依赖性的数学体现。张量的分量会随着[坐标系](@entry_id:156346)的旋转而改变，但它的[特征值保持](@entry_id:636565)不变。

设想我们将[坐标系](@entry_id:156346)从基 $\{\mathbf{e}_i\}$ 旋转到新的基 $\{\mathbf{e}'_j\}$，旋转由一个正交矩阵 $R$ 描述。旧[坐标系](@entry_id:156346)下的张量分量矩阵 $S$ 和新[坐标系](@entry_id:156346)下的分量矩阵 $S'$ 之间的关系为相似变换：
$$
S' = R S R^T
$$
我们可以证明，经过这种变换后，特征方程的形式是不变的 [@problem_id:1543029]：
$$
\det(S' - \lambda I) = \det(R S R^T - \lambda R I R^T) = \det(R(S - \lambda I)R^T) = \det(R)\det(S - \lambda I)\det(R^T)
$$
因为对于旋转矩阵 $R$，$\det(R)=1$，所以 $\det(S' - \lambda I) = \det(S - \lambda I)$。由于两个[张量表示](@entry_id:180492)具有相同的[特征方程](@entry_id:265849)，它们必然拥有相同的[特征值](@entry_id:154894)。这证实了[特征值](@entry_id:154894)是张量的内在属性，是[标量不变量](@entry_id:193787)。无论观察者如何选择他们的坐标轴，他们计算出的主应力或[主转动惯量](@entry_id:150889)都是相同的。

这种不变性使得[特征值分析](@entry_id:273168)成为一个强大的工具。通过切换到以[特征向量](@entry_id:151813)为[主轴](@entry_id:172691)的[坐标系](@entry_id:156346)（主基），张量的矩阵表示会变成一个[对角矩阵](@entry_id:637782)，对角线上的元素就是[特征值](@entry_id:154894)。
$$
[S]_{\text{principal}} = \begin{pmatrix} \lambda_1 & 0 & 0 \\ 0 & \lambda_2 & 0 \\ 0 & 0 & \lambda_3 \end{pmatrix}
$$
在这个“自然”[坐标系](@entry_id:156346)中，张量的作用变得异常简单：它只是沿着坐标轴方向的独立缩放。

### [瑞利商](@entry_id:137794)与[变分原理](@entry_id:198028)

[特征值](@entry_id:154894)还可以通过一种完全不同的方式来理解，即作为某个函数的极值。对于一个对称张量 $\mathbf{S}$，我们定义**瑞利商**（Rayleigh quotient）为：
$$
R(\mathbf{x}) = \frac{\mathbf{x} \cdot (\mathbf{S}\mathbf{x})}{\mathbf{x} \cdot \mathbf{x}}
$$
瑞利商是一个标量函数，它依赖于向量 $\mathbf{x}$ 的方向。**瑞利原理**指出，[瑞利商](@entry_id:137794) $R(\mathbf{x})$ 的驻值（最大值、最小值或[鞍点](@entry_id:142576)值）恰好就是张量 $\mathbf{S}$ 的[特征值](@entry_id:154894)。而使得 $R(\mathbf{x})$ 取驻值的向量 $\mathbf{x}$，就是对应的[特征向量](@entry_id:151813)。

这个原理在物理学中有广泛的应用。例如，一个刚体的转动惯量 $I_{\hat{\mathbf{n}}}$ 是关于转轴方向（由单位向量 $\hat{\mathbf{n}}$ 表示）的函数，可以由惯性张量 $\mathbf{I}$ 计算得出：
$$
I_{\hat{\mathbf{n}}} = \hat{\mathbf{n}} \cdot (\mathbf{I}\hat{\mathbf{n}})
$$
这正是分母为1（因为 $\hat{\mathbf{n}} \cdot \hat{\mathbf{n}} = 1$）的[瑞利商](@entry_id:137794)。因此，要找到一个刚体的最大和最小[转动惯量](@entry_id:174608)，我们只需要找到其[惯性张量](@entry_id:148659) $\mathbf{I}$ 的最大和最小特征值即可 [@problem_id:1543004]。这些[特征值](@entry_id:154894)就是**[主转动惯量](@entry_id:150889)**，它们是[刚体转动](@entry_id:191086)性质的基本参数。

### 可交换张量与共同主方向

最后，一个有趣的问题是：在什么条件下，两个不同的[对称张量](@entry_id:148092)会共享同一组[主方向](@entry_id:276187)（[特征向量](@entry_id:151813)）？这在研究[复合材料](@entry_id:139856)或叠加应[力场](@entry_id:147325)时可能遇到。答案是，两个对称张量 $\mathbf{S}_1$ 和 $\mathbf{S}_2$ 具有共同的[特征向量基](@entry_id:163721)，当且仅当它们**可交换**（commute），即它们的乘积与顺序无关：
$$
\mathbf{S}_1 \mathbf{S}_2 = \mathbf{S}_2 \mathbf{S}_1
$$
或者说，它们的**交换子**（commutator）为零：$[\mathbf{S}_1, \mathbf{S}_2] = \mathbf{S}_1 \mathbf{S}_2 - \mathbf{S}_2 \mathbf{S}_1 = \mathbf{0}$。

我们可以用一个简单的计算来验证这一点 [@problem_id:1542987]。给定两个共享主方向的张量：
$$
\mathbf{S}_1 = \begin{pmatrix} 3 & 2 \\ 2 & 3 \end{pmatrix} \quad \text{和} \quad \mathbf{S}_2 = \begin{pmatrix} 1 & 2 \\ 2 & 1 \end{pmatrix}
$$
计算它们的乘积：
$$
\mathbf{S}_1 \mathbf{S}_2 = \begin{pmatrix} 3 & 2 \\ 2 & 3 \end{pmatrix} \begin{pmatrix} 1 & 2 \\ 2 & 1 \end{pmatrix} = \begin{pmatrix} 7 & 8 \\ 8 & 7 \end{pmatrix}
$$
$$
\mathbf{S}_2 \mathbf{S}_1 = \begin{pmatrix} 1 & 2 \\ 2 & 1 \end{pmatrix} \begin{pmatrix} 3 & 2 \\ 2 & 3 \end{pmatrix} = \begin{pmatrix} 7 & 8 \\ 8 & 7 \end{pmatrix}
$$
由于 $\mathbf{S}_1 \mathbf{S}_2 = \mathbf{S}_2 \mathbf{S}_1$，它们的[交换子](@entry_id:158878)为零矩阵，这与它们共享主方向的性质是一致的。这个性质意味着，如果系统由两个可交换的[对称张量](@entry_id:148092)描述，那么存在一个共同的主[坐标系](@entry_id:156346)，在这个[坐标系](@entry_id:156346)下，两个张量都可以同时被对角化，从而极大地简化分析。