## 引言
在固体力学中，精确描述和理解一个物体内部任意点的受力状态是进行强度分析、预测材料行为的基石。柯西[应力张量](@entry_id:148973)为此提供了完整的数学描述，但其分量数值会随着[坐标系](@entry_id:156346)的选取而改变，这为寻找一种客观、内在的度量方式带来了挑战。为了解决这一问题，连续介质力学引入了[主应力与主方向](@entry_id:193792)这一核心概念，它们是应力状态的内在属性，不随观察者改变，直接关联着材料可能承受的极端拉伸或压缩。

本文旨在为读者构建一个关于主应力理论的完整知识体系。我们将从第一性原理出发，系统地探索这一概念的物理与数学基础，并展示其在解决复杂工程问题中的强大威力。文章分为三个主要部分：第一章“原理与机制”，将深入剖析[主应力](@entry_id:176761)作为应力[张量[特征值问](@entry_id:198059)题](@entry_id:142153)的本质，探讨其存在性、唯一性以及与[应力不变量](@entry_id:170526)的深刻联系。第二章“应用与交叉学科联系”，将展示主应力理论如何在[材料失效准则](@entry_id:189510)、结构设计、实验力学和计算力学等多个领域中发挥关键作用。最后，“动手实践”部分将通过具体的计算问题，帮助读者将理论知识转化为解决实际问题的能力。

现在，让我们首先进入第一章，深入探讨[主应力与主方向](@entry_id:193792)的基本原理及其背后的数学机制。

## 原理与机制

在连续介质力学中，理解材料内部任意一点的受力状态是至关重要的。这种受力状态由柯西应力张量 $\boldsymbol{\sigma}$ 所描述。虽然应力张量在其分量表示上依赖于[坐标系](@entry_id:156346)的选择，但其物理本质是独立于[坐标系](@entry_id:156346)的。为了揭示这种内在的、不依赖于[坐标系](@entry_id:156346)的物理特性，我们引入了[主应力与主方向](@entry_id:193792)的概念。本章将从第一性原理出发，系统地阐述[主应力](@entry_id:176761)的物理起源、数学表述、基本性质及其在材料本构理论中的核心作用。

### [主应力](@entry_id:176761)的物理与数学起源

在受力连续体内的任意一点，我们可以想象一个通过该点的无限小[截面](@entry_id:154995)。这个[截面](@entry_id:154995)的方位由其[单位法向量](@entry_id:178851) $\boldsymbol{n}$ 定义。根据柯西应力原理，作用在该[截面](@entry_id:154995)上的力（即面力）可以用一个牵[引力](@entry_id:175476)矢量 $\boldsymbol{t}(\boldsymbol{n})$ 来描述。柯西公式（Cauchy's formula）建立了牵[引力](@entry_id:175476)矢量与应力张量之间的[线性关系](@entry_id:267880) [@problem_id:2674936]：

$$
\boldsymbol{t}(\boldsymbol{n}) = \boldsymbol{\sigma}\boldsymbol{n}
$$

这里，$\boldsymbol{\sigma}$ 是一个[二阶张量](@entry_id:199780)，它将描述[截面](@entry_id:154995)方位的[单位法向量](@entry_id:178851) $\boldsymbol{n}$ 映射为作用在该[截面](@entry_id:154995)上的牵[引力](@entry_id:175476)矢量 $\boldsymbol{t}$。在经典[连续介质力学](@entry_id:155125)中，若不考虑[体力](@entry_id:174230)矩（body couples），角动量守恒定律要求柯西应力张量必须是对称的，即 $\boldsymbol{\sigma} = \boldsymbol{\sigma}^{\mathsf{T}}$ [@problem_id:2621539] [@problem_id:2674911]。这一对称性是应力理论的基石，并带来了深刻的数学与物理后果。

现在，我们提出一个关键问题：是否存在某些特殊的[截面](@entry_id:154995)，其上的牵[引力](@entry_id:175476)矢量 $\boldsymbol{t}(\boldsymbol{n})$ 与该[截面](@entry_id:154995)的[法向量](@entry_id:264185) $\boldsymbol{n}$ 方向相同（或相反）？换言之，在这些[截面](@entry_id:154995)上，应力完全是法向的，没有任何剪切分量。这样的[截面](@entry_id:154995)被称为**[主平面](@entry_id:164488)**（principal plane），其法向量 $\boldsymbol{n}$ 被称为**[主应力方向](@entry_id:753737)**（principal stress direction）或简称**主方向**（principal direction）。

从物理定义上，如果 $\boldsymbol{n}$ 是一个主方向，那么牵[引力](@entry_id:175476)矢量 $\boldsymbol{t}(\boldsymbol{n})$ 必然与 $\boldsymbol{n}$ 共线。这可以表示为 [@problem_id:2621539]：

$$
\boldsymbol{t}(\boldsymbol{n}) = \lambda\boldsymbol{n}
$$

其中，标量 $\lambda$ 是一个比例系数，它度量了在[主平面](@entry_id:164488)上法向应力的大小。这个标量 $\lambda$ 被定义为与主方向 $\boldsymbol{n}$ 相关联的**主应力**（principal stress）。当 $\lambda$ 为正时，表示拉伸；为负时，表示压缩。

将上述两个关于 $\boldsymbol{t}(\boldsymbol{n})$ 的表达式联立，我们便得到了确定[主应力](@entry_id:176761)和[主方向](@entry_id:276187)的基本数学方程 [@problem_id:2674911]：

$$
\boldsymbol{\sigma}\boldsymbol{n} = \lambda\boldsymbol{n}
$$

这是一个标准的**特征值问题**（eigenvalue problem）。主应力 $\lambda$ 正是[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ 的**[特征值](@entry_id:154894)**（eigenvalues），而主方向 $\boldsymbol{n}$ 则是其对应的**[特征向量](@entry_id:151813)**（eigenvectors）。由于 $\boldsymbol{n}$ 代表一个[单位法向量](@entry_id:178851)，我们通常对其进行归一化，即 $\|\boldsymbol{n}\| = 1$。值得注意的是，如果 $\boldsymbol{n}$ 是一个主方向，那么 $-\boldsymbol{n}$ 也是，它们代表同一个[主平面](@entry_id:164488)，只是[法向量](@entry_id:264185)指向相反。

在[主平面](@entry_id:164488)上，[剪切应力](@entry_id:137139)为零。这一点可以明确地验证。牵[引力](@entry_id:175476)矢量 $\boldsymbol{t}$ 可以分解为法向分量 $\boldsymbol{t}_{\mathrm{n}}$ 和切向（剪切）分量 $\boldsymbol{t}_{\mathrm{s}}$。法向分量是 $\boldsymbol{t}$ 在 $\boldsymbol{n}$ 方向上的投影，即 $\boldsymbol{t}_{\mathrm{n}} = (\boldsymbol{t} \cdot \boldsymbol{n})\boldsymbol{n}$。剪切分量则是 $\boldsymbol{t}_{\mathrm{s}} = \boldsymbol{t} - \boldsymbol{t}_{\mathrm{n}}$。如果 $\boldsymbol{n}$ 是一个主方向，则 $\boldsymbol{t} = \lambda\boldsymbol{n}$。代入分解式可得：

$$
\boldsymbol{t}_{\mathrm{n}} = ((\lambda\boldsymbol{n}) \cdot \boldsymbol{n})\boldsymbol{n} = \lambda(\|\boldsymbol{n}\|^2)\boldsymbol{n} = \lambda\boldsymbol{n} = \boldsymbol{t}
$$

因此，剪切分量为：

$$
\boldsymbol{t}_{\mathrm{s}} = \boldsymbol{t} - \boldsymbol{t}_{\mathrm{n}} = \lambda\boldsymbol{n} - \lambda\boldsymbol{n} = \boldsymbol{0}
$$

这从数学上证实了[主平面](@entry_id:164488)的物理意义：它们是承受纯法向应力、没有任何[剪切应力](@entry_id:137139)的平面 [@problem_id:2694312]。

### [特征方程](@entry_id:265849)与[应力不变量](@entry_id:170526)

为了求解[特征值问题](@entry_id:142153) $\boldsymbol{\sigma}\boldsymbol{n} = \lambda\boldsymbol{n}$，我们将其改写为一个[齐次线性方程组](@entry_id:153432)：

$$
(\boldsymbol{\sigma} - \lambda\boldsymbol{I})\boldsymbol{n} = \boldsymbol{0}
$$

其中 $\boldsymbol{I}$ 是二阶单位张量。这个[方程组](@entry_id:193238)要有非零解（即 $\boldsymbol{n} \neq \boldsymbol{0}$），其系数矩阵 $(\boldsymbol{\sigma} - \lambda\boldsymbol{I})$ 的[行列式](@entry_id:142978)必须为零 [@problem_id:2674911]：

$$
\det(\boldsymbol{\sigma} - \lambda\boldsymbol{I}) = 0
$$

这就是应力张量 $\boldsymbol{\sigma}$ 的**[特征方程](@entry_id:265849)**（characteristic equation）。对于三维空间中的应力状态，这是一个关于 $\lambda$ 的三次多项式方程。展开这个[行列式](@entry_id:142978)，我们可以得到如下形式 [@problem_id:2674855]：

$$
-\lambda^3 + I_1 \lambda^2 - I_2 \lambda + I_3 = 0
$$

或者，更常见的形式是：

$$
\lambda^3 - I_1 \lambda^2 + I_2 \lambda - I_3 = 0
$$

这个方程的三个根 $\sigma_1, \sigma_2, \sigma_3$ 就是三个[主应力](@entry_id:176761)。方程的系数 $I_1, I_2, I_3$ 被称为**主[应力[不变](@entry_id:170526)量](@entry_id:148850)**（principal invariants of stress），因为它们的值不随[坐标系](@entry_id:156346)的旋转而改变。这一点我们将在后续小节中进行严格证明。这些[不变量](@entry_id:148850)可以由应力张量的分量直接计算得出 [@problem_id:2674855] [@problem_id:2674887]：

$$
I_1 = \operatorname{tr}(\boldsymbol{\sigma}) = \sigma_{ii}
$$

$$
I_2 = \frac{1}{2} \left[ (\operatorname{tr}(\boldsymbol{\sigma}))^2 - \operatorname{tr}(\boldsymbol{\sigma}^2) \right] = \frac{1}{2} (\sigma_{ii}\sigma_{jj} - \sigma_{ij}\sigma_{ji})
$$

$$
I_3 = \det(\boldsymbol{\sigma}) = \det(\sigma_{ij})
$$

根据[韦达定理](@entry_id:150627)（Vieta's formulas），这些[不变量](@entry_id:148850)也是主应力的[基本对称多项式](@entry_id:152224)：

$$
I_1 = \sigma_1 + \sigma_2 + \sigma_3
$$

$$
I_2 = \sigma_1\sigma_2 + \sigma_2\sigma_3 + \sigma_3\sigma_1
$$

$$
I_3 = \sigma_1\sigma_2\sigma_3
$$

这组关系表明，三个主[应力[不变](@entry_id:170526)量](@entry_id:148850)唯一地确定了三个[主应力](@entry_id:176761)的大小（作为一个无序集合），反之亦然。

### 存在性、实数性与正交性：谱定理的应用

我们已经知道，柯西应力张量 $\boldsymbol{\sigma}$ 是一个**实对称**张量。这一性质在数学上具有极其重要的意义。线性代数中的**[谱定理](@entry_id:136620)**（Spectral Theorem）为[实对称矩阵](@entry_id:192806)（或张量）的[特征值问题](@entry_id:142153)提供了强有力的保证 [@problem_id:2621539]：

1.  **实数性**：一个实对称张量的所有[特征值](@entry_id:154894)均为实数。这意味着三个主应力 $\sigma_1, \sigma_2, \sigma_3$ 都是实数，这与它们作为物理量的身份相符。

2.  **正交性**：对于一个实[对称张量](@entry_id:148092)，对应于不同[特征值](@entry_id:154894)的[特征向量](@entry_id:151813)是相互正交的。

3.  **存在性**：一个 $n$ 维实[对称张量](@entry_id:148092)总能找到一组 $n$ 个[线性无关](@entry_id:148207)的[特征向量](@entry_id:151813)，构成一个完整的**正交基**。在三维情况下，这意味着总能找到三个相互正交的主方向 $\boldsymbol{n}_1, \boldsymbol{n}_2, \boldsymbol{n}_3$，它们构成一个标准正交基。

这些性质是经典[应力分析](@entry_id:168804)的理论基石。它们保证了对于任何应力状态，我们总能找到一个由三个相互垂直的[主平面](@entry_id:164488)构成的[坐标系](@entry_id:156346)（称为**主[坐标系](@entry_id:156346)**），在该[坐标系](@entry_id:156346)下，[应力张量](@entry_id:148973)的[矩阵表示](@entry_id:146025)是对角化的，对角线上的元素就是三个[主应力](@entry_id:176761)。

为了凸显[应力张量对称性](@entry_id:201218)的重要性，我们可以考察一个非对称的[二阶张量](@entry_id:199780) $\boldsymbol{\tau}$ 的情况。这种张量可能出现在[微极连续体](@entry_id:751972)（Cosserat continuum）等更复杂的理论中，或者作为计算中的误差产物 [@problem_id:2674917]。其代数上的主值问题同样是 $\boldsymbol{\tau}\boldsymbol{v} = \lambda\boldsymbol{v}$。然而，由于 $\boldsymbol{\tau}$ 不再是对称的，[谱定理](@entry_id:136620)的结论不再成立：
*   其[特征值](@entry_id:154894) $\lambda$ 不再保证是实数，它们可以以[共轭复数对](@entry_id:150139)的形式出现。
*   其[特征向量](@entry_id:151813)通常不是相互正交的。

例如，考虑一个非对称张量 $\boldsymbol{\tau} = \begin{pmatrix} 1  -2  0 \\ 3  4  0 \\ 0  0  2 \end{pmatrix}$。它的一个[特征值](@entry_id:154894)是 $\lambda_3=2$，而另外两个[特征值](@entry_id:154894)由其左上角 $2 \times 2$ 子块决定，求解可得 $\lambda_{1,2} = \frac{5 \pm i\sqrt{15}}{2}$。复数[特征值](@entry_id:154894)的出现，意味着在经典物理框架下，它们无法被解释为真实的应力。这清晰地表明，[角动量守恒](@entry_id:156798)所导致的[应力张量对称性](@entry_id:201218)，对于确保主[应力分析](@entry_id:168804)的物理意义是不可或缺的 [@problem_id:2674917]。

在实际工程应用中，如果通过实验测量或数值模拟得到的[应力张量](@entry_id:148973)包含微小的非对称部分，通常将其视为非物理的误差。标准的处理方法是取其对称部分 $\boldsymbol{\sigma}_{\text{sym}} = \frac{1}{2}(\boldsymbol{\sigma}_{\text{meas}} + \boldsymbol{\sigma}_{\text{meas}}^{\mathsf{T}})$ 进行后续的物理分析，例如[主应力](@entry_id:176761)计算 [@problem_id:2674911]。

### [主应力与主方向](@entry_id:193792)的求解：示例与特殊情况

求解[主应力](@entry_id:176761)和主方向的过程分为两步：首先解特征方程得到三个[主应力](@entry_id:176761)，然后对每一个[主应力](@entry_id:176761)，求解相应的[齐次线性方程组](@entry_id:153432)得到[主方向](@entry_id:276187)。

让我们考虑一个具体的应力状态，其[张量表示](@entry_id:180492)为 [@problem_id:2694312]：
$$
\boldsymbol{\sigma}=\begin{pmatrix}
60  20  0\\
20  30  0\\
0  0  10
\end{pmatrix}
\text{ MPa}
$$
其特征方程为 $\det(\boldsymbol{\sigma} - \lambda\boldsymbol{I}) = 0$，即：
$$
\det \begin{pmatrix}
60-\lambda  20  0\\
20  30-\lambda  0\\
0  0  10-\lambda
\end{pmatrix} = (10-\lambda)[(60-\lambda)(30-\lambda) - 400] = 0
$$
这立即给出一个[主应力](@entry_id:176761) $\sigma_3 = 10$ MPa。另外两个主应力是二次方程 $\lambda^2 - 90\lambda + 1400 = 0$ 的根。解得 $\sigma_1 = 70$ MPa 和 $\sigma_2 = 20$ MPa。

接下来，我们求解对应的主方向。
对于 $\sigma_1 = 70$ MPa，我们求解 $(\boldsymbol{\sigma} - 70\boldsymbol{I})\boldsymbol{n}_1 = \boldsymbol{0}$：
$$
\begin{pmatrix} -10  20  0\\ 20  -40  0\\ 0  0  -60 \end{pmatrix}
\begin{pmatrix} n_x \\ n_y \\ n_z \end{pmatrix} = \boldsymbol{0}
$$
这得到 $n_z=0$ 和 $-10n_x + 20n_y=0$，即 $n_x = 2n_y$。归一化后的主方向是 $\boldsymbol{n}_1 = \frac{1}{\sqrt{5}}(2, 1, 0)^{\mathsf{T}}$。
类似地，对于 $\sigma_2 = 20$ MPa，可解得 $\boldsymbol{n}_2 = \frac{1}{\sqrt{5}}(1, -2, 0)^{\mathsf{T}}$。
对于 $\sigma_3 = 10$ MPa，可解得 $\boldsymbol{n}_3 = (0, 0, 1)^{\mathsf{T}}$。
可以验证，这三个[主方向](@entry_id:276187) $\boldsymbol{n}_1, \boldsymbol{n}_2, \boldsymbol{n}_3$ 构成了一个[标准正交基](@entry_id:147779)。

**特殊情况：重根[主应力](@entry_id:176761)**

当特征方程有[重根](@entry_id:151486)时，即出现两个或三个相等的[主应力](@entry_id:176761)，我们称之为**简并**（degenerate）情况。此时，[主方向](@entry_id:276187)的唯一性会发生改变 [@problem_id:2674876]。
*   如果两个主应力相等（例如 $\sigma_1 = \sigma_2 \neq \sigma_3$），则对应于这个[重复特征值](@entry_id:154579)的[特征空间](@entry_id:638014)是一个二维平面。任何位于这个平面内的[单位向量](@entry_id:165907)都是一个有效的主方向。这种情况被称为**[平面应力](@entry_id:172193)主态**或[轴对称](@entry_id:173333)应力状态。
*   如果三个[主应力](@entry_id:176761)都相等（$\sigma_1 = \sigma_2 = \sigma_3 = \sigma_0$），则应力状态为**静水压**（hydrostatic）状态，$\boldsymbol{\sigma} = \sigma_0 \boldsymbol{I}$。此时，特征空间是整个三维空间，**任何方向都是主方向**。

考虑一个具有重根[主应力](@entry_id:176761)的例子 [@problem_id:2674876]：
$$
\boldsymbol{\sigma} = \begin{pmatrix} 5  1  1 \\ 1  5  1 \\ 1  1  5 \end{pmatrix}
$$
其特征方程为 $-(\lambda-4)^2(\lambda-7) = 0$。主应力为 $\sigma_1 = 7$（单根）和 $\sigma_2 = \sigma_3 = 4$（二重根）。
*   对于单根 $\sigma_1=7$，可以解得唯一的主方向（除去符号）为 $\boldsymbol{n}_1 = \frac{1}{\sqrt{3}}(1, 1, 1)^{\mathsf{T}}$。
*   对于二[重根](@entry_id:151486) $\sigma_2=4$，我们求解 $(\boldsymbol{\sigma} - 4\boldsymbol{I})\boldsymbol{n} = \boldsymbol{0}$，得到方程 $n_x+n_y+n_z=0$。这是一个通过原点的平面的方程。任何满足该方程且长度为1的向量都是与[主应力](@entry_id:176761)4 MPa相关联的有效主方向。这个平面就是与[特征值](@entry_id:154894)4对应的特征[子空间](@entry_id:150286)。我们可以在这个平面内任意选择两个相互正交的[单位向量](@entry_id:165907)（例如，通过[格拉姆-施密特正交化](@entry_id:143035)方法），与 $\boldsymbol{n}_1$ 一起，构成一个完整的主方向[标准正交基](@entry_id:147779)。

### 应力的张量性质与[主应力](@entry_id:176761)的不变性

我们之前提到[应力不变量](@entry_id:170526)和[主应力](@entry_id:176761)本身不随[坐标系](@entry_id:156346)改变，现在我们从更根本的张量理论角度来阐明这一点。

一个物理量被称为[二阶张量](@entry_id:199780)，并不仅仅因为它有9个分量，而是因为它的分量在[坐标系](@entry_id:156346)变换下遵循特定的法则。考虑一个从旧[坐标基](@entry_id:270149) $\lbrace\boldsymbol{e}_i\rbrace$ 到新[坐标基](@entry_id:270149) $\lbrace\boldsymbol{e}'_j\rbrace$ 的刚性旋转，该变换由一个正交张量 $\boldsymbol{Q}$ 描述。在此变换下，向量的分量变换规律为 $\boldsymbol{v}' = \boldsymbol{Q}\boldsymbol{v}$。牵[引力](@entry_id:175476)矢量 $\boldsymbol{t}$ 和法向量 $\boldsymbol{n}$ 都是客观的物理向量，因此它们的表示也遵循此规律。

物理定律本身必须是客观的，即在任何[坐标系](@entry_id:156346)下形式不变。因此，柯西关系在新旧[坐标系](@entry_id:156346)下都成立：$\boldsymbol{t} = \boldsymbol{\sigma}\boldsymbol{n}$ 和 $\boldsymbol{t}' = \boldsymbol{\sigma}'\boldsymbol{n}'$。结合向量的变换规律，可以推导出应力张量分量的变换法则 [@problem_id:2674936]：

$$
\boldsymbol{\sigma}' = \boldsymbol{Q}\boldsymbol{\sigma}\boldsymbol{Q}^{\mathsf{T}}
$$

这正是二阶张量的定义性变换法则。由于 $\boldsymbol{Q}$ 是正交张量，$\boldsymbol{Q}^{\mathsf{T}} = \boldsymbol{Q}^{-1}$，所以这个变换是一个**相似变换**。线性代数的一个基本定理是，[相似变换](@entry_id:152935)不改变矩阵的[特征值](@entry_id:154894)。我们可以显式地证明这一点：

令 $\lambda$ 是 $\boldsymbol{\sigma}$ 的一个[特征值](@entry_id:154894)，$\boldsymbol{n}$ 是对应的[特征向量](@entry_id:151813)，即 $\boldsymbol{\sigma}\boldsymbol{n} = \lambda\boldsymbol{n}$。在新[坐标系](@entry_id:156346)下，我们考察变换后的张量 $\boldsymbol{\sigma}'$ 对变换后的向量 $\boldsymbol{n}' = \boldsymbol{Q}\boldsymbol{n}$ 的作用：

$$
\boldsymbol{\sigma}'\boldsymbol{n}' = (\boldsymbol{Q}\boldsymbol{\sigma}\boldsymbol{Q}^{\mathsf{T}})(\boldsymbol{Q}\boldsymbol{n}) = \boldsymbol{Q}\boldsymbol{\sigma}(\boldsymbol{Q}^{\mathsf{T}}\boldsymbol{Q})\boldsymbol{n} = \boldsymbol{Q}(\boldsymbol{\sigma}\boldsymbol{n})
$$

将 $\boldsymbol{\sigma}\boldsymbol{n} = \lambda\boldsymbol{n}$ 代入，得到：

$$
\boldsymbol{\sigma}'\boldsymbol{n}' = \boldsymbol{Q}(\lambda\boldsymbol{n}) = \lambda(\boldsymbol{Q}\boldsymbol{n}) = \lambda\boldsymbol{n}'
$$

这个结果 $\boldsymbol{\sigma}'\boldsymbol{n}' = \lambda\boldsymbol{n}'$ 表明，$\boldsymbol{n}'$ 是 $\boldsymbol{\sigma}'$ 的[特征向量](@entry_id:151813)，并且其[特征值](@entry_id:154894)**仍然是** $\lambda$。这雄辩地证明了：

*   **主应力是客观标量**：它们的值不依赖于观察者（[坐标系](@entry_id:156346)），是应力状态的内在属性。
*   **[主方向](@entry_id:276187)是客观向量**：它们是真实的物理方向，其在不同[坐标系](@entry_id:156346)下的分量表示会随[坐标系](@entry_id:156346)的旋转而相应改变。

这个结论同样适用于随时间变化的[旋转坐标系](@entry_id:170324) $\boldsymbol{Q}(t)$。在任意时刻 $t$，上述变换关系和不变性都瞬时成立。尽管[坐标系](@entry_id:156346)的旋转速率 $\dot{\boldsymbol{Q}}(t)$ 会在应力率的变换中引入额外项，但它不影响任何时刻 $t$ 的应力张量本身及其[主值](@entry_id:189577) [@problem_id:2674937]。这就是应力[客观性原理](@entry_id:185412)（principle of objectivity）的体现。

### 在材料本构中的意义

主应力与[应力不变量](@entry_id:170526)不仅是数学上的便利工具，它们在描述[材料力学](@entry_id:201885)行为的[本构关系](@entry_id:186508)中扮演着核心角色。

首先，主应力代表了一点处[法向应力](@entry_id:260622)的极值。最大[主应力](@entry_id:176761) $\sigma_{\max} = \max(\sigma_1, \sigma_2, \sigma_3)$ 和最小主应力 $\sigma_{\min} = \min(\sigma_1, \sigma_2, \sigma_3)$ 是许多[材料强度](@entry_id:158701)和失效理论（如最大[正应力](@entry_id:260622)理论）的关键判据。

其次，在构建材料本构模型时，尤其是对于**各向同性**（isotropic）材料，[应力不变量](@entry_id:170526)是不可或缺的。[各向同性材料](@entry_id:170678)的力学响应与方向无关。这意味着，任何描述其材料属性的标量函数（例如，[应变能密度函数](@entry_id:755490) $W$）如果依赖于应力状态，那么它只能通过那些不随[坐标系](@entry_id:156346)旋转而改变的量来依赖于[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$。这些量正是[应力不变量](@entry_id:170526) $I_1, I_2, I_3$ [@problem_id:2920806]。

因此，[各向同性材料](@entry_id:170678)的本构关系可以普遍地表达为[应力不变量](@entry_id:170526)的函数，例如 $W = W(I_1, I_2, I_3)$。这种表达方式自动满足了材料的客观性和各向同性要求。它完美地体现了物理本质：$I_1, I_2, I_3$ 这三个标量唯一地决定了三个主应力的大小，但完全不包含任何关于主方向（即应力状态在空间中方位）的信息。对于一个没有内部优选方向的[各向同性材料](@entry_id:170678)而言，其响应正应该只取决于应力状态的“大小”而非“方位”。这就是[应力不变量](@entry_id:170526)在现代[连续介质力学](@entry_id:155125)中的深刻意义 [@problem_id:2920806]。