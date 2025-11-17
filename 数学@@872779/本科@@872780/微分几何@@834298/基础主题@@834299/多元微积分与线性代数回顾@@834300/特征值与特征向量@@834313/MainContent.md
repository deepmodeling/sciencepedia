## 引言
在线性代数的世界中，[矩阵变换](@entry_id:156789)无处不在，它们描述了从简单的几何旋转到复杂的系统演化等各种过程。然而，一个变换的作用通常是复杂的，它会同时改变向量的大小和方向。我们不禁要问：是否存在一些特殊的、不变的方向，在变换的作用下，这些方向上的向量只发生简单的拉伸或压缩？这个看似简单的问题引出了线性代数中最深刻、应用最广泛的概念之一——[特征值与特征向量](@entry_id:748836)。它们是理解线性变换、动力系统乃至[曲面](@entry_id:267450)几何的“钥匙”，能够揭示复杂系统背后的内在结构和[不变量](@entry_id:148850)。

本文旨在系统地引导您深入理解[特征值与特征向量](@entry_id:748836)的理论精髓及其跨学科的应用威力。我们将分三个章节展开：

- **第一章：原理与机制** 将从基本定义出发，详细阐述[特征值](@entry_id:154894)和[特征向量](@entry_id:151813)的数学原理，包括如何通过特征方程计算它们，如何理解特征空间，以及对角化、对称矩阵等重要性质。我们还将特别探讨其在微分几何中作为形算子[特征值](@entry_id:154894)的核心作用。
- **第二章：应用与交叉学科联系** 将展示这些抽象概念如何在现实世界中“大显身手”。您将看到[特征值](@entry_id:154894)如何刻画[曲面](@entry_id:267450)的几何形状，如何决定物理系统的稳定性和[振动](@entry_id:267781)模式，以及如何在现代数据科学和[网络分析](@entry_id:139553)中揭示隐藏的结构。
- **第三章：动手实践** 提供了一系列精心挑选的练习题，旨在通过具体计算和概念辨析，巩固您对[主曲率](@entry_id:270598)、[主方向](@entry_id:276187)等核心概念的理解，将理论知识转化为解决问题的实际能力。

通过本文的学习，您将不仅掌握[特征值与特征向量](@entry_id:748836)的计算方法，更重要的是，能够建立起从抽象数学到具体应用的桥梁，理解它们为何是现代科学与工程中不可或缺的分析工具。让我们首先从其最基本的原理与机制开始探索。

## 原理与机制

在本章中，我们将深入探讨[特征值](@entry_id:154894)和[特征向量](@entry_id:151813)的数学原理及其在不同科学与工程领域中的核心机制。我们将从基本定义出发，逐步建立计算方法，并最终揭示这些概念在描述[线性变换](@entry_id:149133)、动力系统以及[曲面](@entry_id:267450)几何中的深刻意义。

### [特征值与特征向量](@entry_id:748836)的定义

在许多物理和数学模型中，核心问题是理解一个[线性变换](@entry_id:149133)如何作用于一个[向量空间](@entry_id:151108)。一个线性变换，由矩阵 $A$ 表示，通常会同时改变输入向量的大小和方向。然而，对于任何给定的变换，几乎总存在一些特殊的非零向量，当它们被变换作用时，其方向保持不变（或恰好反向）。这些向量仅被拉伸或压缩。这些特殊的向量被称为**[特征向量](@entry_id:151813) (eigenvectors)**，而对应的缩放因子则被称为**[特征值](@entry_id:154894) (eigenvalues)**。

这一概念可以用一个简洁的方程来精确表述。对于一个 $n \times n$ 的方阵 $A$，如果存在一个非零向量 $\mathbf{v} \in \mathbb{R}^n$ 和一个标量 $\lambda$，使得：

$A\mathbf{v} = \lambda\mathbf{v}$

那么，我们称 $\lambda$ 为矩阵 $A$ 的一个**[特征值](@entry_id:154894)**，$\mathbf{v}$ 为对应于[特征值](@entry_id:154894) $\lambda$ 的一个**[特征向量](@entry_id:151813)**。

这个方程的几何意义是，向量 $A\mathbf{v}$ 与向量 $\mathbf{v}$ 是共线的。[特征向量](@entry_id:151813)定义了这样一个[子空间](@entry_id:150286)，其中矩阵 $A$ 的作用简化为纯粹的标量乘法。

为了具体理解这一点，我们可以考虑一个生态系统模型。假设有两种相互作用的物种，其在某年初的种群数量可以用一个向量 $\mathbf{p} = \begin{pmatrix} p_1 \\ p_2 \end{pmatrix}$ 表示。一年后，新的种群向量 $\mathbf{p}_{\text{next}}$ 由一个[转移矩阵](@entry_id:145510) $A$ 决定，即 $\mathbf{p}_{\text{next}} = A\mathbf{p}$。如果系统存在一种“[平衡分布](@entry_id:263943)”，即两个物种的相对比例年复一年保持不变，这意味着后一年的种群向量 $\mathbf{p}_{\text{next}}$与前一年的向量 $\mathbf{p}$ 方向相同，仅仅是在大小上有一个缩放。这正是[特征向量](@entry_id:151813)的定义：$A\mathbf{p} = \lambda\mathbf{p}$。这里的[特征值](@entry_id:154894) $\lambda$ 代表了整个种群的年增长率。

我们可以直接使用定义来验证一个给定的向量是否是某个矩阵的[特征向量](@entry_id:151813)。例如，考虑转移矩阵 $A = \begin{pmatrix} 3  -1 \\ 2  0 \end{pmatrix}$。我们想知道向量 $\mathbf{v}_B = \begin{pmatrix} 1 \\ 1 \end{pmatrix}$ 是否代表一个[平衡分布](@entry_id:263943)。我们只需计算 $A\mathbf{v}_B$：
$$
A\mathbf{v}_B = \begin{pmatrix} 3  -1 \\ 2  0 \end{pmatrix} \begin{pmatrix} 1 \\ 1 \end{pmatrix} = \begin{pmatrix} 3 \cdot 1 - 1 \cdot 1 \\ 2 \cdot 1 + 0 \cdot 1 \end{pmatrix} = \begin{pmatrix} 2 \\ 2 \end{pmatrix}
$$
我们可以观察到，结果向量 $\begin{pmatrix} 2 \\ 2 \end{pmatrix}$ 正好是原始向量 $\begin{pmatrix} 1 \\ 1 \end{pmatrix}$ 的两倍。因此，我们可以写出：
$$
A\mathbf{v}_B = 2\mathbf{v}_B
$$
这完全符合 $A\mathbf{v} = \lambda\mathbf{v}$ 的形式。因此，$\mathbf{v}_B = \begin{pmatrix} 1 \\ 1 \end{pmatrix}$ 是矩阵 $A$ 的一个[特征向量](@entry_id:151813)，其对应的[特征值](@entry_id:154894)为 $\lambda = 2$ [@problem_id:1360110]。

### [特征值](@entry_id:154894)的计算：[特征方程](@entry_id:265849)

虽然我们可以逐一验证向量，但这并非系统性的方法。为了系统地找出矩阵的所有[特征值](@entry_id:154894)，我们需要一种更通用的策略。我们可以将[特征方程](@entry_id:265849) $A\mathbf{v} = \lambda\mathbf{v}$ 进行改写。令 $I$ 为单位矩阵，则 $\lambda\mathbf{v} = \lambda I \mathbf{v}$。于是，方程变为：
$A\mathbf{v} - \lambda I \mathbf{v} = \mathbf{0}$
$(A - \lambda I)\mathbf{v} = \mathbf{0}$

这个方程表明，一个非零的[特征向量](@entry_id:151813) $\mathbf{v}$ 存在于矩阵 $(A - \lambda I)$ 的[零空间](@entry_id:171336) (null space) 中。根据线性代数的基本定理，一个[齐次线性方程组](@entry_id:153432)要有非零解，当且仅当其系数矩阵是奇异的（singular），也就是说，该[矩阵的行列式](@entry_id:148198)为零。

因此，寻找[特征值](@entry_id:154894) $\lambda$ 的问题就转化为求解以下方程：
$$
\det(A - \lambda I) = 0
$$
这个方程被称为**特征方程 (characteristic equation)**。方程的左边，$\det(A - \lambda I)$，是一个关于 $\lambda$ 的多项式，称为**特征多项式 (characteristic polynomial)**。对于一个 $n \times n$ 矩阵，$p(\lambda) = \det(A - \lambda I)$ 是一个 $n$ 次多项式，它的根就是矩阵 $A$ 的所有[特征值](@entry_id:154894)。

例如，在数字图形学中，一个线性变换 $A = \begin{pmatrix} 7  -2 \\ 4  1 \end{pmatrix}$ 被用来变换平面上的点。那些在变换下方向不变的向量所对应的缩放因子，就是该矩阵的[特征值](@entry_id:154894)。为了找到这些因子，我们建立并求解特征方程 [@problem_id:2168104]：
$$
A - \lambda I = \begin{pmatrix} 7 - \lambda  -2 \\ 4  1 - \lambda \end{pmatrix}
$$
其[行列式](@entry_id:142978)为：
$$
\det(A - \lambda I) = (7 - \lambda)(1 - \lambda) - (-2)(4) = \lambda^2 - 8\lambda + 7 + 8 = \lambda^2 - 8\lambda + 15
$$
令特征多项式为零，$\lambda^2 - 8\lambda + 15 = 0$，我们可以分解为 $(\lambda - 3)(\lambda - 5) = 0$。因此，该变换的[特征值](@entry_id:154894)为 $\lambda_1 = 3$ 和 $\lambda_2 = 5$。这意味着存在两个方向，在变换 $A$ 的作用下，一个方向上的向量长度变为原来的3倍，另一个方向上的[向量长度](@entry_id:156432)变为原来的5倍。

对于某些特殊结构的矩阵，[特征值](@entry_id:154894)的计算会变得非常简单。一个重要的例子是**三角矩阵**（上三角或下[三角矩阵](@entry_id:636278)）。对于一个[三角矩阵](@entry_id:636278)，其[行列式](@entry_id:142978)就是对角线上元素的乘积。因此，对于矩阵 $A - \lambda I$（如果 $A$ 是三角矩阵，它也是三角矩阵），其[行列式](@entry_id:142978)就是 $(a_{11} - \lambda)(a_{22} - \lambda)\cdots(a_{nn} - \lambda)$。这意味着[三角矩阵的特征值](@entry_id:196522)就是其对角线上的元素。例如，对于矩阵 $A = \begin{pmatrix} 5  2  -1 \\ 0  -2  4 \\ 0  0  3 \end{pmatrix}$，我们无需计算复杂的[行列式](@entry_id:142978)，通过观察即可得知其[特征值](@entry_id:154894)为 $\lambda_1 = 5$, $\lambda_2 = -2$, 和 $\lambda_3 = 3$ [@problem_id:2168109]。

### [特征空间](@entry_id:638014)

一旦我们求出了一个[特征值](@entry_id:154894) $\lambda$，所有与之对应的[特征向量](@entry_id:151813)（以及[零向量](@entry_id:156189)）构成一个[向量子空间](@entry_id:151815)，称为**[特征空间](@entry_id:638014) (eigenspace)**，记作 $E_\lambda$。根据定义，这个空间就是矩阵 $(A - \lambda I)$ 的[零空间](@entry_id:171336)，即 $E_\lambda = \ker(A - \lambda I)$。寻找一个特征空间的基，就是求解[齐次线性方程组](@entry_id:153432) $(A - \lambda I)\mathbf{v} = \mathbf{0}$。

让我们以一个[振动](@entry_id:267781)系统模型为例，其动力学由矩阵 $A = \begin{pmatrix} 5  2  0 \\ 2  4  -1 \\ 0  -1  2 \end{pmatrix}$ 描述。已知 $\lambda = 3$ 是一个[特征值](@entry_id:154894)，我们来寻找对应的[特征空间](@entry_id:638014) $E_3$ [@problem_id:1360138]。
首先，构建矩阵 $A - 3I$:
$$
A - 3I = \begin{pmatrix} 5-3  2  0 \\ 2  4-3  -1 \\ 0  -1  2-3 \end{pmatrix} = \begin{pmatrix} 2  2  0 \\ 2  1  -1 \\ 0  -1  -1 \end{pmatrix}
$$
现在我们求解方程 $(A - 3I)\mathbf{v} = \mathbf{0}$，其中 $\mathbf{v} = \begin{pmatrix} x \\ y \\ z \end{pmatrix}$。这等价于[方程组](@entry_id:193238)：
$$
\begin{cases}
2x+2y=0 \\
2x+y-z=0 \\
-y-z=0
\end{cases}
$$
从第一个方程得到 $x = -y$。从第三个方程得到 $z = -y$。将这两个关系代入第二个方程，我们得到 $2(-y) + y - (-y) = -2y + y + y = 0$，这是一个恒等式，说明[方程组](@entry_id:193238)是相容的。因此，所有解向量的形式为：
$$
\mathbf{v} = \begin{pmatrix} -y \\ y \\ -y \end{pmatrix} = y \begin{pmatrix} -1 \\ 1 \\ -1 \end{pmatrix}
$$
其中 $y$ 是任意实数。这意味着[特征空间](@entry_id:638014) $E_3$ 是由向量 $\begin{pmatrix} 1 \\ -1 \\ 1 \end{pmatrix}$ (或其任意非零标量倍) 生成的一维[子空间](@entry_id:150286)。因此，集合 $\left\{ \begin{pmatrix} 1 \\ -1 \\ 1 \end{pmatrix} \right\}$ 构成了 $E_3$ 的一组基。

### [特征值与特征向量](@entry_id:748836)的重要性质

#### [对称矩阵](@entry_id:143130)

**[实对称矩阵](@entry_id:192806)**（即 $A^T = A$）在线性代数和物理学中扮演着至关重要的角色。它们的[特征值](@entry_id:154894)和[特征向量](@entry_id:151813)具有非凡的性质，这些性质由谱定理 (Spectral Theorem) 概括：
1.  一个[实对称矩阵](@entry_id:192806)的所有[特征值](@entry_id:154894)都是实数。
2.  对应于不同[特征值](@entry_id:154894)的[特征向量](@entry_id:151813)是相互**正交**的。

正交性是一个非常强大的属性。如果 $\mathbf{v}_1$ 和 $\mathbf{v}_2$ 是[对称矩阵](@entry_id:143130) $A$ 分别对应于不同[特征值](@entry_id:154894) $\lambda_1$ 和 $\lambda_2$ 的[特征向量](@entry_id:151813)，那么它们的[点积](@entry_id:149019)为零，即 $\mathbf{v}_1 \cdot \mathbf{v}_2 = \mathbf{v}_1^T \mathbf{v}_2 = 0$。

例如，如果我们知道一个 $2 \times 2$ [实对称矩阵](@entry_id:192806) $A$ 有两个不同的[特征值](@entry_id:154894)，并且对应的[特征向量](@entry_id:151813)分别是 $\mathbf{v}_1 = \begin{pmatrix} 3 \\ 1 \end{pmatrix}$ 和 $\mathbf{v}_2 = \begin{pmatrix} x \\ 3 \end{pmatrix}$，那么我们可以利用正交性来确定 $x$ 的值。
$$
\mathbf{v}_1^T \mathbf{v}_2 = \begin{pmatrix} 3  1 \end{pmatrix} \begin{pmatrix} x \\ 3 \end{pmatrix} = 3x + 1 \cdot 3 = 0
$$
解得 $x=-1$。这个性质在很多应用中都极为有用，例如，它保证了在量子力学中可观测量（由厄米算子，即[复数域](@entry_id:153768)的对称矩阵推广，表示）的[本征态](@entry_id:149904)构成一个正交基 [@problem_id:1360132]。

#### 复数[特征值](@entry_id:154894)

即使一个矩阵的所有元素都是实数，它的[特征值](@entry_id:154894)也可能是复数。当这种情况发生时，它们总是以**共轭对**的形式出现。也就是说，如果 $\lambda = a + b\mathrm{i}$ ($b \neq 0$) 是一个[特征值](@entry_id:154894)，那么它的共轭 $\bar{\lambda} = a - b\mathrm{i}$也必定是矩阵的一个[特征值](@entry_id:154894)。此外，如果 $\mathbf{v}$ 是对应于 $\lambda$ 的[特征向量](@entry_id:151813)，那么它的共轭向量 $\bar{\mathbf{v}}$ 就是对应于 $\bar{\lambda}$ 的[特征向量](@entry_id:151813)。

在动力系统中，实数[特征值](@entry_id:154894)通常对应于指数增长或衰减的模式，而复数[特征值](@entry_id:154894)则与系统的**[振荡](@entry_id:267781)或旋转行为**相关。例如，考虑一个由矩阵 $A = \begin{pmatrix} 1  -5 \\ 1  -1 \end{pmatrix}$ 控制的[离散时间系统](@entry_id:263935) [@problem_id:2168082]。其[特征方程](@entry_id:265849)为：
$$
\det \begin{pmatrix} 1-\lambda  -5 \\ 1  -1-\lambda \end{pmatrix} = (1-\lambda)(-1-\lambda) - (-5) = \lambda^2 - 1 + 5 = \lambda^2 + 4 = 0
$$
解得[特征值](@entry_id:154894)为 $\lambda = \pm 2\mathrm{i}$。这对共轭的纯虚数[特征值](@entry_id:154894)表明，系统[状态向量](@entry_id:154607)在[演化过程](@entry_id:175749)中会经历旋转和尺度的缩放。

#### 对角化、[代数重数与几何重数](@entry_id:151502)

一个关键问题是：我们能否找到一个由矩阵 $A$ 的[特征向量](@entry_id:151813)组成的基？如果可以，那么矩阵 $A$ 在这个基下的表示将是一个[对角矩阵](@entry_id:637782)，其对角[线元](@entry_id:196833)素就是对应的[特征值](@entry_id:154894)。这样的矩阵被称为**可对角化 (diagonalizable)** 的。

一个矩阵是否可[对角化](@entry_id:147016)，取决于其[特征值](@entry_id:154894)的**[代数重数](@entry_id:154240) (algebraic multiplicity)** 和 **[几何重数](@entry_id:155584) (geometric multiplicity)**。
*   一个[特征值](@entry_id:154894) $\lambda_i$ 的**[代数重数](@entry_id:154240)**是它作为[特征多项式](@entry_id:150909) $p(\lambda) = \det(A - \lambda I)$ 的根的次数。
*   一个[特征值](@entry_id:154894) $\lambda_i$ 的**[几何重数](@entry_id:155584)**是其对应[特征空间](@entry_id:638014) $E_{\lambda_i}$ 的维数，即 $\dim(\ker(A - \lambda_i I))$。

对于任何[特征值](@entry_id:154894)，其[几何重数](@entry_id:155584)总是小于或等于其[代数重数](@entry_id:154240) ($1 \le \text{GM} \le \text{AM}$)。一个 $n \times n$ 矩阵是可对角化的，当且仅当它拥有 $n$ 个线性无关的[特征向量](@entry_id:151813)。这等价于对它的每一个[特征值](@entry_id:154894)，其[几何重数](@entry_id:155584)都等于其[代数重数](@entry_id:154240)。

当一个[特征值](@entry_id:154894)的[几何重数](@entry_id:155584)严格小于其[代数重数](@entry_id:154240)时，该矩阵是**亏损的 (defective)**，并且不可对角化。一个经典的例子是[剪切变换](@entry_id:151272)。考虑一个由矩阵 $A = \begin{pmatrix} 1  -4 \\ 0  1 \end{pmatrix}$ 定义的水平剪切 [@problem_id:2168126]。
其[特征多项式](@entry_id:150909)为 $\det(A - \lambda I) = (1-\lambda)^2 = 0$，所以它只有一个[特征值](@entry_id:154894) $\lambda = 1$，[代数重数](@entry_id:154240)为2。
为了求其[几何重数](@entry_id:155584)，我们寻找[特征空间](@entry_id:638014) $E_1 = \ker(A-I)$：
$$
(A-I)\mathbf{v} = \begin{pmatrix} 0  -4 \\ 0  0 \end{pmatrix} \begin{pmatrix} x_1 \\ x_2 \end{pmatrix} = \begin{pmatrix} 0 \\ 0 \end{pmatrix}
$$
这给出了方程 $-4x_2=0$，即 $x_2=0$，$x_1$ 是自由的。因此，[特征空间](@entry_id:638014)由形如 $\begin{pmatrix} x_1 \\ 0 \end{pmatrix}$ 的向量组成，这是一个一维空间，由 $\begin{pmatrix} 1 \\ 0 \end{pmatrix}$ 张成。所以，$\lambda = 1$ 的[几何重数](@entry_id:155584)是1。
由于[代数重数](@entry_id:154240)（2）大于[几何重数](@entry_id:155584)（1），该矩阵不可对角化。这意味着我们无法找到一个由 $A$ 的[特征向量](@entry_id:151813)组成的 $\mathbb{R}^2$ 的基。

### [微分几何](@entry_id:145818)中的应用：形算子

[特征值](@entry_id:154894)和[特征向量](@entry_id:151813)的概念在微分几何中描述[曲面](@entry_id:267450)局部形状时起着核心作用。这里的关键工具是**形算子 (shape operator)**，也称为 Weingarten 映射。

对于嵌入在三维[欧几里得空间](@entry_id:138052) $\mathbb{R}^3$ 中的一个光滑[曲面](@entry_id:267450) $M$，在每一点 $p \in M$，我们有一个切平面 $T_pM$和一个[单位法向量](@entry_id:178851) $\mathbf{n}$。形算子 $S_p$ 是一个从切平面到自身的线性映射, $S_p: T_pM \to T_pM$。它描述了当我们沿切平面上的某个方向 $\mathbf{v}$ 移动时，[法向量](@entry_id:264185) $\mathbf{n}$是如何变化的。其定义为：
$$
S_p(\mathbf{v}) = -D_{\mathbf{v}}\mathbf{n}
$$
其中 $D_{\mathbf{v}}\mathbf{n}$ 是[法向量场](@entry_id:268853) $\mathbf{n}$ 在方向 $\mathbf{v}$ 上的方向导数。这个导数向量 $D_{\mathbf{v}}\mathbf{n}$ 衡量了[法向量](@entry_id:264185)的“倾斜”速率，一个基本结果是它总是位于[切平面](@entry_id:136914) $T_pM$ 内。

形算子 $S_p$ 是一个对称线性算子，因此它的[特征值](@entry_id:154894)是实数，并且存在一个由其[特征向量](@entry_id:151813)构成的[正交基](@entry_id:264024)。这些[特征向量](@entry_id:151813)和[特征值](@entry_id:154894)具有深刻的几何意义：
*   $S_p$ 的[特征向量](@entry_id:151813)被称为**主方向 (principal directions)**。
*   $S_p$ 的[特征值](@entry_id:154894)被称为**[主曲率](@entry_id:270598) (principal curvatures)**，通常记作 $k_1$ 和 $k_2$。

根据 $S_p(\mathbf{u}) = k \mathbf{u}$ 的定义，如果 $\mathbf{u}$ 是一个主方向（[特征向量](@entry_id:151813)），那么 $-D_{\mathbf{u}}\mathbf{n} = k\mathbf{u}$，或者 $D_{\mathbf{u}}\mathbf{n} = -k\mathbf{u}$。这揭示了一个关键的几何事实：当沿着一个主方向 $\mathbf{u}$ 移动时，法向量的变化率 $D_{\mathbf{u}}\mathbf{n}$ 与 $\mathbf{u}$ 平行 [@problem_id:1636421]。这意味着在[主方向](@entry_id:276187)上，[曲面](@entry_id:267450)“纯粹地”弯曲而没有任何扭曲。主曲率 $k_1$ 和 $k_2$ 分别量化了[曲面](@entry_id:267450)在两个相互正交的[主方向](@entry_id:276187)上的最大和最小弯曲程度。

从[主曲率](@entry_id:270598)可以导出两个最重要的[曲面](@entry_id:267450)[几何不变量](@entry_id:178611)：
*   **[高斯曲率](@entry_id:149725) (Gaussian curvature)** $K = k_1 k_2$
*   **[平均曲率](@entry_id:162147) (mean curvature)** $H = \frac{1}{2}(k_1 + k_2)$

由于 $k_1$ 和 $k_2$ 是形算子 $S_p$ 的[特征值](@entry_id:154894)，根据线性代数的知识，一个算子的[行列式](@entry_id:142978)等于其[特征值](@entry_id:154894)之积，而其迹等于其[特征值](@entry_id:154894)之和。因此，我们有以下重要的关系 [@problem_id:1636424]：
*   $K = \det(S_p)$
*   $H = \frac{1}{2}\operatorname{tr}(S_p)$

这提供了一个从形算子的任意[矩阵表示](@entry_id:146025)计算 $K$ 和 $H$ 的直接方法。例如，如果在某个[切平面](@entry_id:136914)的[标准正交基](@entry_id:147779)下，形算子的矩阵为 $[S_p] = \begin{pmatrix} 5  3 \\ 3  -3 \end{pmatrix}$，那么[高斯曲率](@entry_id:149725) $K = (5)(-3) - (3)(3) = -24$，平均曲率 $H = \frac{1}{2}(5 + (-3)) = 1$。

最后，必须强调一个微妙但重要的观点：形算子 $S_p$ 的**矩阵表示**依赖于所选择的[切平面](@entry_id:136914)基底，而基底又依赖于[曲面](@entry_id:267450)的参数化。改变[参数化](@entry_id:272587)会改变基底，从而改变形算子的矩阵 $[S_p]$。然而，形算子 $S_p$ 本身作为一个抽象的[线性变换](@entry_id:149133)，以及它的[特征值](@entry_id:154894)（[主曲率](@entry_id:270598)），是[曲面](@entry_id:267450)在点 $p$ 的**内在几何属性**，不随[参数化](@entry_id:272587)的选择而改变 [@problem_id:1636418]。例如，对于一个半径为2的圆柱面，无论我们使用标准的[柱坐标](@entry_id:271645)参数化还是其他复杂的参数化，计算出的主曲率始终是 $\{-\frac{1}{2}, 0\}$（一个对应于圆周方向，另一个对应于沿轴线的直线方向），尽管在不同基底下形算子的矩阵形式可能完全不同。这凸显了[特征值](@entry_id:154894)作为坐标无关[不变量](@entry_id:148850)的核心重要性。