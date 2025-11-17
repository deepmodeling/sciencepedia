## 引言
[特征值与特征向量](@entry_id:748836)是线性代数中最深刻且应用最广泛的概念之一。它们不仅是理解线性变换几何本质的钥匙，更是剖析复杂动态系统、揭示高维数据结构和评估[网络影响力](@entry_id:269356)的强大数学工具。然而，许多学习者在掌握了其抽象的数学定义后，常常困惑于如何将这些概念应用于解决经济、金融及其他领域的实际问题。本文旨在填补理论与实践之间的鸿沟，为读者构建一个从原理到应用的完整知识体系。

为实现这一目标，本文将分为三个核心部分。我们将在第一章“原理与机制”中，从基本定义出发，系统地介绍[特征值与特征向量](@entry_id:748836)的计算方法、关键性质，并深入探讨[矩阵对角化](@entry_id:138930)乃至[若尔当标准型](@entry_id:155670)等高级主题，为后续应用奠定坚实的理论基础。随后，在第二章“应用与跨学科联系”中，我们将视野扩展到[计算经济学](@entry_id:140923)和金融学的具体场景，探索如何运用[特征值分析](@entry_id:273168)动态系统的稳定性、通过主成分分析（PCA）从金融数据中提取关键信息，以及衡量网络中的节点中心性。最后，在“动手实践”部分，我们将通过一系列精心设计的计算问题，引导读者亲手应用所学知识，将理论真正转化为解决问题的能力。让我们首先深入其核心，探究[特征值与特征向量](@entry_id:748836)的“原理与机制”。

## 原理与机制

在线性代数领域，[特征值](@entry_id:154894)和[特征向量](@entry_id:151813)是理解[线性变换](@entry_id:149133)、动力系统和[数据结构](@entry_id:262134)的核心概念。它们揭示了矩阵作用于[向量空间](@entry_id:151108)时最本质的特性。本章将深入探讨[特征值](@entry_id:154894)和[特征向量](@entry_id:151813)的定义、计算方法、关键性质以及它们在[矩阵对角化](@entry_id:138930)等高级应用中的作用。

### 核心思想：不变方向与缩放因子

一个 $n \times n$ 矩阵 $A$ 定义了一个从 $n$ 维空间 $\mathbb{R}^n$ 到自身的线性变换。对于空间中的任意向量 $\mathbf{v}$，其变换后的结果为 $A\mathbf{v}$。在大多数情况下，变换后的向量 $A\mathbf{v}$ 在方向和长度上都与原始向量 $\mathbf{v}$ 不同。然而，对于任何给定的变换，几乎总存在一些特殊的非零向量，当它们被矩阵 $A$ 变换时，其方向保持不变（或恰好反向）。变换的作用仅仅是对这些向量进行拉伸或压缩。

这些特殊的向量被称为矩阵 $A$ 的**[特征向量](@entry_id:151813)** (eigenvectors)。描述这种拉伸或压缩程度的标量因子，则被称为与该[特征向量](@entry_id:151813)对应的**[特征值](@entry_id:154894)** (eigenvalues)。这个基本关系可以用一个简洁的方程来描述：

$A\mathbf{v} = \lambda\mathbf{v}$

其中 $A$ 是一个 $n \times n$ 矩阵，$\mathbf{v}$ 是一个非零的 $n \times 1$ 列向量（[特征向量](@entry_id:151813)），而 $\lambda$ 是一个标量（[特征值](@entry_id:154894)）。

这个定义提供了一种直接检验一个向量是否为特定矩阵的[特征向量](@entry_id:151813)的方法。我们无需预先计算任何[特征值](@entry_id:154894)，只需将向量代入方程，看结果是否为原向量的一个标量倍。

例如，考虑一个描述两个相互作用物种[种群动态](@entry_id:136352)的简化模型[@problem_id:1360110]。设某年的种群向量为 $\mathbf{p}$，下一年则变为 $A\mathbf{p}$，其中 $A = \begin{pmatrix} 3  -1 \\ 2  0 \end{pmatrix}$。如果存在一个种群[分布](@entry_id:182848)，使得其相对比例年复一年保持不变，那么这个[分布](@entry_id:182848)就是一个“[平衡分布](@entry_id:263943)”。这意味着下一年的种群向量 $\mathbf{p}_{\text{next}}$ 与当前向量 $\mathbf{p}$ 的方向相同，即 $\mathbf{p}_{\text{next}} = \lambda \mathbf{p}$。这正是[特征向量](@entry_id:151813)的定义。

让我们检验向量 $\mathbf{v} = \begin{pmatrix} 1 \\ 1 \end{pmatrix}$ 是否代表一个[平衡分布](@entry_id:263943)：
$$
A\mathbf{v} = \begin{pmatrix} 3  -1 \\ 2  0 \end{pmatrix} \begin{pmatrix} 1 \\ 1 \end{pmatrix} = \begin{pmatrix} 3(1) - 1(1) \\ 2(1) + 0(1) \end{pmatrix} = \begin{pmatrix} 2 \\ 2 \end{pmatrix}
$$
变换后的向量是 $\begin{pmatrix} 2 \\ 2 \end{pmatrix}$，它可以被写成 $2 \begin{pmatrix} 1 \\ 1 \end{pmatrix}$。因此，我们发现 $A\mathbf{v} = 2\mathbf{v}$。这证实了 $\mathbf{v} = \begin{pmatrix} 1 \\ 1 \end{pmatrix}$ 是矩阵 $A$ 的一个[特征向量](@entry_id:151813)，其对应的[特征值](@entry_id:154894)是 $\lambda=2$。在这个生态系统中，如果两个物种的种群数量相等，那么在下一年，它们的数量将各自翻倍，但它们的相对比例（1:1）保持不变。

### 计算[特征值与特征向量](@entry_id:748836)

虽然直接验证很方便，但我们通常需要一个系统性的方法来找出矩阵的所有[特征值](@entry_id:154894)和[特征向量](@entry_id:151813)。

#### [特征方程](@entry_id:265849)

我们的出发点仍然是核心定义式 $A\mathbf{v} = \lambda\mathbf{v}$。为了求解它，我们将其改写：
$$
A\mathbf{v} - \lambda\mathbf{v} = \mathbf{0}
$$
引入单位矩阵 $I$，我们可以写出 $\lambda\mathbf{v} = \lambda I \mathbf{v}$，于是方程变为：
$$
(A - \lambda I)\mathbf{v} = \mathbf{0}
$$
这个方程描述了一个[齐次线性系统](@entry_id:153432)。根据定义，[特征向量](@entry_id:151813) $\mathbf{v}$ 是非零的。一个[齐次系统](@entry_id:150411)拥有非零解的充要条件是其系数矩阵 $(A - \lambda I)$ 是奇异的（singular），也就是说，它的[行列式](@entry_id:142978)为零。
$$
\det(A - \lambda I) = 0
$$
这个方程被称为**特征方程** (characteristic equation)。对于一个 $n \times n$ 矩阵，$p(\lambda) = \det(A - \lambda I)$ 是一个关于 $\lambda$ 的 $n$ 次多项式，称为**特征多项式** (characteristic polynomial)。这个[多项式的根](@entry_id:154615)就是矩阵 $A$ 的所有[特征值](@entry_id:154894)。

让我们通过一个例子来演示这个过程[@problem_id:2168104]。假设一个二维图形变换由矩阵 $A = \begin{pmatrix} 7  -2 \\ 4  1 \end{pmatrix}$ 表示。我们要寻找那些只被缩放而不改变方向的向量所对应的缩放因子，即[特征值](@entry_id:154894)。

首先，构建矩阵 $(A - \lambda I)$:
$$
A - \lambda I = \begin{pmatrix} 7  -2 \\ 4  1 \end{pmatrix} - \lambda \begin{pmatrix} 1  0 \\ 0  1 \end{pmatrix} = \begin{pmatrix} 7 - \lambda  -2 \\ 4  1 - \lambda \end{pmatrix}
$$
然后，计算其[行列式](@entry_id:142978)并令其为零：
$$
\det(A - \lambda I) = (7 - \lambda)(1 - \lambda) - (-2)(4) = 0
$$
展开这个表达式：
$$
7 - 8\lambda + \lambda^2 + 8 = \lambda^2 - 8\lambda + 15 = 0
$$
这是一个简单的二次方程，我们可以通过分解因式或求根公式来求解：
$$
(\lambda - 3)(\lambda - 5) = 0
$$
解得[特征值](@entry_id:154894)为 $\lambda_1 = 3$ 和 $\lambda_2 = 5$。这意味着该线性变换存在两个不变方向，一个方向上的向量被拉伸为原来的3倍，另一个方向上的向量被拉伸为原来的5倍。

#### 寻找[特征向量](@entry_id:151813)与[特征空间](@entry_id:638014)

一旦找到了[特征值](@entry_id:154894)，我们就可以通过求解[齐次系统](@entry_id:150411) $(A - \lambda I)\mathbf{v} = \mathbf{0}$ 来找到对应的[特征向量](@entry_id:151813)。对于每一个[特征值](@entry_id:154894) $\lambda$，其所有对应的[特征向量](@entry_id:151813)（以及[零向量](@entry_id:156189)）构成一个[向量子空间](@entry_id:151815)，称为 $\lambda$ 对应的**[特征空间](@entry_id:638014)** (eigenspace)，记作 $E_\lambda$。特征空间 $E_\lambda$ 就是矩阵 $(A - \lambda I)$ 的零空间 (null space)。

让我们为一个 $3 \times 3$ 矩阵寻找一个特征空间的基[@problem_id:1360138]。考虑矩阵 $A = \begin{pmatrix} 5  2  0 \\ 2  4  -1 \\ 0  -1  2 \end{pmatrix}$，已知其有一个[特征值](@entry_id:154894)为 $\lambda = 3$。为了找到对应的[特征空间](@entry_id:638014) $E_3$，我们需求解 $(A - 3I)\mathbf{v} = \mathbf{0}$。

首先，计算 $A - 3I$：
$$
A - 3I = \begin{pmatrix} 5-3  2  0 \\ 2  4-3  -1 \\ 0  -1  2-3 \end{pmatrix} = \begin{pmatrix} 2  2  0 \\ 2  1  -1 \\ 0  -1  -1 \end{pmatrix}
$$
设 $\mathbf{v} = \begin{pmatrix} x \\ y \\ z \end{pmatrix}$，则线性方程组为：
$$
\begin{cases}
2x + 2y = 0 \\
2x + y - z = 0 \\
-y - z = 0
\end{cases}
$$
从第一个方程得到 $x = -y$。从第三个方程得到 $z = -y$。将这两个关系代入第二个方程进行验证：$2(-y) + y - (-y) = -2y + y + y = 0$，此为恒等式，说明[方程组](@entry_id:193238)是相容的。

因此，所有满足条件的向量都可以写成 $\begin{pmatrix} -y \\ y \\ -y \end{pmatrix} = y \begin{pmatrix} -1 \\ 1 \\ -1 \end{pmatrix}$ 的形式，其中 $y$ 是任意实数。为了方便，我们可以令 $t = -y$，则[特征向量](@entry_id:151813)的形式为 $t \begin{pmatrix} 1 \\ -1 \\ 1 \end{pmatrix}$。
这个[特征空间](@entry_id:638014) $E_3$ 是一条穿过原点的直线，其基可以由任何一个非零的[特征向量](@entry_id:151813)构成，例如 $\left\{ \begin{pmatrix} 1 \\ -1 \\ 1 \end{pmatrix} \right\}$。

### [特征值](@entry_id:154894)的基本性质

[特征值](@entry_id:154894)并非孤立的数字，它们与矩阵的其他重要属性（如[迹和行列式](@entry_id:149685)）紧密相关。

#### 迹、[行列式](@entry_id:142978)与[特征值](@entry_id:154894)的关系

对于任意一个 $n \times n$ 矩阵 $A$，其[特征值](@entry_id:154894) $\lambda_1, \lambda_2, \dots, \lambda_n$ (计入[代数重数](@entry_id:154240)) 具有以下两个基本性质：

1.  **[特征值](@entry_id:154894)之和等于[矩阵的迹](@entry_id:139694) (Trace)**：
    $$
    \sum_{i=1}^{n} \lambda_i = \operatorname{tr}(A)
    $$
    矩阵的**迹**定义为其主对角线上元素的和。这个性质在验证[特征值计算](@entry_id:145559)的正确性时非常有用。例如，对于矩阵 $A = \begin{pmatrix} 5  3 \\ -4  -4 \end{pmatrix}$ [@problem_id:2168140]，其迹为 $\operatorname{tr}(A) = 5 + (-4) = 1$。其特征方程为 $\lambda^2 - \lambda - 8 = 0$，根据[韦达定理](@entry_id:150627)，两根之和为 $-(-1)/1 = 1$。这与迹相等。

2.  **[特征值](@entry_id:154894)之积等于矩阵的行列式 (Determinant)**：
    $$
    \prod_{i=1}^{n} \lambda_i = \det(A)
    $$
    这个性质将[矩阵的可逆性](@entry_id:204560)与[特征值](@entry_id:154894)联系起来：一个矩阵是可逆的，当且仅当它的[行列式](@entry_id:142978)非零，这等价于它没有任何为零的[特征值](@entry_id:154894)。以矩阵 $M = \begin{pmatrix} 5  2 \\ 2  1 \end{pmatrix}$ 为例 [@problem_id:2168138]，其[行列式](@entry_id:142978)为 $\det(M) = 5(1) - 2(2) = 1$。通过求解[特征方程](@entry_id:265849) $\lambda^2 - 6\lambda + 1 = 0$，我们得到[特征值](@entry_id:154894)为 $\lambda = 3 \pm 2\sqrt{2}$。它们的乘积是 $(3+2\sqrt{2})(3-2\sqrt{2}) = 3^2 - (2\sqrt{2})^2 = 9 - 8 = 1$，这恰好等于矩阵的行列式。

#### [特殊矩阵的特征值](@entry_id:195589)

- **对称矩阵**：[实对称矩阵](@entry_id:192806) (即 $A = A^T$) 在经济学和物理学中非常常见。它们具有优美的性质：
    1.  所有[特征值](@entry_id:154894)都是实数。
    2.  对应于**不同**[特征值](@entry_id:154894)的[特征向量](@entry_id:151813)是**正交**的 (orthogonal)。即如果 $A\mathbf{v}_1 = \lambda_1 \mathbf{v}_1$ 且 $A\mathbf{v}_2 = \lambda_2 \mathbf{v}_2$ 并且 $\lambda_1 \neq \lambda_2$，那么 $\mathbf{v}_1^T \mathbf{v}_2 = 0$。
    这个正交性是一个非常强的约束。例如，如果已知一个对称矩阵 $A = \begin{pmatrix} 8  b \\ b  2 \end{pmatrix}$ 的两个[特征向量](@entry_id:151813)分别是 $\mathbf{v}_1 = \begin{pmatrix} 3 \\ 1 \end{pmatrix}$ 和 $\mathbf{v}_2 = \begin{pmatrix} x \\ 3 \end{pmatrix}$，对应于不同的[特征值](@entry_id:154894)[@problem_id:1360132]。我们甚至不需要知道[特征值](@entry_id:154894)是多少，就可以利用正交性来求解未知参数。由于 $\mathbf{v}_1 \cdot \mathbf{v}_2 = 0$，我们有 $3x + 1(3) = 0$，从而得到 $x = -1$。

- **[复特征值](@entry_id:156384)**：虽然我们经常处理实数矩阵，但它们的[特征值](@entry_id:154894)不一定是实数。一个典型的例子是旋转。考虑一个将平面向量逆时针旋转 $90^\circ$ 的变换[@problem_id:1360131]。这个变换由矩阵 $A = \begin{pmatrix} 0  -1 \\ 1  0 \end{pmatrix}$ 表示。直观上看，除了零向量，没有任何向量在旋转后方向保持不变，因此我们预料它没有实[特征向量](@entry_id:151813)。让我们来计算[特征值](@entry_id:154894)：
    $$
    \det(A - \lambda I) = \det\begin{pmatrix} -\lambda  -1 \\ 1  -\lambda \end{pmatrix} = (-\lambda)(-\lambda) - (-1)(1) = \lambda^2 + 1 = 0
    $$
    这个方程的解是 $\lambda = \pm i$，其中 $i$ 是虚数单位。这证实了我们的直觉：对于一个纯[旋转变换](@entry_id:200017)，它的[特征向量](@entry_id:151813)和[特征值](@entry_id:154894)存在于复数域中。在经济周期模型或信号处理中，[复特征值](@entry_id:156384)通常与[振荡](@entry_id:267781)或周期性行为相关。

### [对角化](@entry_id:147016)及其应用

[特征值](@entry_id:154894)和[特征向量](@entry_id:151813)最强大的应用之一是**[矩阵对角化](@entry_id:138930)** (diagonalization)。

#### [对角化](@entry_id:147016)过程

如果一个 $n \times n$ 的矩阵 $A$ 拥有 $n$ 个[线性无关](@entry_id:148207)的[特征向量](@entry_id:151813) $\mathbf{v}_1, \dots, \mathbf{v}_n$，那么它就是**可[对角化](@entry_id:147016)的** (diagonalizable)。我们可以将这些[特征向量](@entry_id:151813)作为列，构成一个可逆矩阵 $P = \begin{pmatrix} \mathbf{v}_1  \mathbf{v}_2  \dots  \mathbf{v}_n \end{pmatrix}$。同时，我们可以将对应的[特征值](@entry_id:154894) $\lambda_1, \dots, \lambda_n$ 放在一个对角矩阵 $D$ 的对角线上：
$$
D = \begin{pmatrix} \lambda_1  0  \dots  0 \\ 0  \lambda_2  \dots  0 \\ \vdots  \vdots  \ddots  \vdots \\ 0  0  \dots  \lambda_n \end{pmatrix}
$$
这三个矩阵 $A, P, D$ 之间存在一个美妙的关系：
$$
A = PDP^{-1}
$$
这个分解的本质是进行了一次[基变换](@entry_id:189626)。在标准基下，变换 $A$ 可能很复杂（混合了旋转、拉伸和剪切）。但如果我们将[坐标系](@entry_id:156346)切换到由[特征向量](@entry_id:151813)构成的基，那么同一个变换就变得异常简单：它仅仅是在每个[基向量](@entry_id:199546)（[特征向量](@entry_id:151813)）方向上进行独立的缩放，缩放比例就是对应的[特征值](@entry_id:154894)。

让我们完整地[对角化](@entry_id:147016)一个矩阵 $A = \begin{pmatrix} 15  -8 \\ 24  -13 \end{pmatrix}$ [@problem_id:2168155]。
1.  **求[特征值](@entry_id:154894)**：特征方程为 $\lambda^2 - 2\lambda - 3 = 0$，解得 $\lambda_1 = 3, \lambda_2 = -1$。
2.  **求[特征向量](@entry_id:151813)**：
    -   对于 $\lambda_1 = 3$，求解 $(A-3I)\mathbf{v}=\mathbf{0}$，即 $\begin{pmatrix} 12  -8 \\ 24  -16 \end{pmatrix}\mathbf{v}=\mathbf{0}$，得到[特征向量](@entry_id:151813) $\mathbf{v}_1 = \begin{pmatrix} 2 \\ 3 \end{pmatrix}$。
    -   对于 $\lambda_2 = -1$，求解 $(A+I)\mathbf{v}=\mathbf{0}$，即 $\begin{pmatrix} 16  -8 \\ 24  -12 \end{pmatrix}\mathbf{v}=\mathbf{0}$，得到[特征向量](@entry_id:151813) $\mathbf{v}_2 = \begin{pmatrix} 1 \\ 2 \end{pmatrix}$。
3.  **构造 P 和 D**：按照 $\lambda_1 > \lambda_2$ 的顺序[排列](@entry_id:136432)，我们有：
    $$
    P = \begin{pmatrix} 2  1 \\ 3  2 \end{pmatrix}, \quad D = \begin{pmatrix} 3  0 \\ 0  -1 \end{pmatrix}
    $$
4.  **求 P 的逆**：对于 $2 \times 2$ 矩阵， $P^{-1} = \frac{1}{\det(P)} \begin{pmatrix} d  -b \\ -c  a \end{pmatrix} = \frac{1}{4-3} \begin{pmatrix} 2  -1 \\ -3  2 \end{pmatrix} = \begin{pmatrix} 2  -1 \\ -3  2 \end{pmatrix}$。
至此，我们完成了[对角化](@entry_id:147016)分解 $A = PDP^{-1}$。

#### 应用：矩阵的幂与动力系统

[对角化](@entry_id:147016)的一个直接应用是高效地计算矩阵的幂。例如，计算 $A^k$：
$$
A^k = (PDP^{-1})^k = (PDP^{-1})(PDP^{-1})\dots(PDP^{-1}) = PD(P^{-1}P)D\dots DP^{-1} = PD^kP^{-1}
$$
计算对角矩阵的幂非常简单，只需将对角线上的每个元素取 $k$ 次方即可：$D^k = \begin{pmatrix} \lambda_1^k  0 \\ 0  \lambda_2^k \end{pmatrix}$。这使得计算 $A^k$ 从 $k-1$ 次[矩阵乘法](@entry_id:156035)简化为两次矩阵乘法和一次[对角矩阵](@entry_id:637782)求幂。

这在分析[离散动力系统](@entry_id:154936) $\mathbf{x}_{k+1} = A\mathbf{x}_k$ 时至关重要。系统的[长期行为](@entry_id:192358)由 $\mathbf{x}_k = A^k \mathbf{x}_0$ 决定。考虑一个由对角矩阵 $A = \begin{pmatrix} 2  0 \\ 0  3 \end{pmatrix}$ 驱动的系统，初始状态为 $\mathbf{v}_0 = \begin{pmatrix} 3 \\ 2 \end{pmatrix}$ [@problem_id:2168102]。
第 $k$ 步的状态为：
$$
\mathbf{v}_k = A^k \mathbf{v}_0 = \begin{pmatrix} 2^k  0 \\ 0  3^k \end{pmatrix} \begin{pmatrix} 3 \\ 2 \end{pmatrix} = \begin{pmatrix} 3 \cdot 2^k \\ 2 \cdot 3^k \end{pmatrix}
$$
向量 $\mathbf{v}_k$ 与 $x$ 轴正方向的夹角 $\theta_k$ 的正切值为 $\tan(\theta_k) = \frac{2 \cdot 3^k}{3 \cdot 2^k} = \frac{2}{3} \left(\frac{3}{2}\right)^k$。
当 $k \to \infty$ 时，由于 $3/2 > 1$，该比值趋向于无穷大。因此，$\lim_{k \to \infty} \theta_k = \lim_{t \to \infty} \arctan(t) = \frac{\pi}{2}$。
这个结果直观地表明，系统的[状态向量](@entry_id:154607)会越来越偏向于与**最大[特征值](@entry_id:154894)**（这里是 $\lambda=3$）相关联的[特征向量](@entry_id:151813)（即 $y$ 轴方向的 $\begin{pmatrix} 0 \\ 1 \end{pmatrix}$）的方向。这是分析动力系统稳定性和长期趋势的一个普遍原则。

### 超越[对角化](@entry_id:147016)：[若尔当标准型](@entry_id:155670)

我们已经看到，当一个 $n \times n$ 矩阵有 $n$ 个线性无关的[特征向量](@entry_id:151813)时，它是可对角化的。但如果不是呢？

一个[特征值](@entry_id:154894)的**[代数重数](@entry_id:154240)** (algebraic multiplicity) 是它作为特征多项式根的次数。它的**[几何重数](@entry_id:155584)** (geometric multiplicity) 是其对应[特征空间](@entry_id:638014)的维数（即线性无关的[特征向量](@entry_id:151813)的数量）。一个矩阵是可[对角化](@entry_id:147016)的，当且仅当它的每一个[特征值](@entry_id:154894)的[代数重数](@entry_id:154240)都等于其[几何重数](@entry_id:155584)。

当一个矩阵的某个[特征值](@entry_id:154894)的[几何重数](@entry_id:155584)小于其[代数重数](@entry_id:154240)时，该矩阵被称为**亏损的** (defective)，并且**不可对角化**。在这种情况下，我们无法找到一个由[特征向量](@entry_id:151813)组成的基。

幸运的是，我们仍然可以找到一个与之相似的、结构几乎和对角矩阵一样简单的矩阵，这就是**[若尔当标准型](@entry_id:155670)** (Jordan Canonical Form)。矩阵 $A$ 可以被分解为 $A = PJP^{-1}$，其中 $J$ 是一个**若尔当矩阵**。它是一个分[块对角矩阵](@entry_id:145530)，每个块（称为若尔当块）的形式为：
$$
J_\lambda = \begin{pmatrix} \lambda  1   \\  \lambda  1  \\   \ddots  1 \\    \lambda \end{pmatrix}
$$
对角线上是[特征值](@entry_id:154894) $\lambda$，紧邻对角线上方（超对角线）的元素是1，其他地方都是0。[可对角化矩阵](@entry_id:150100)的若尔当标准型就是其对角矩阵 $D$。

为了构建矩阵 $P$，除了需要[特征向量](@entry_id:151813)外，我们还需要**[广义特征向量](@entry_id:152349)** (generalized eigenvectors)。如果一个[特征向量](@entry_id:151813) $\mathbf{u}$ 满足 $(A-\lambda I)\mathbf{u} = \mathbf{0}$，那么一个一阶[广义特征向量](@entry_id:152349) $\mathbf{w}$ 满足 $(A-\lambda I)\mathbf{w} = \mathbf{u}$。

考虑一个由矩阵 $A = \begin{pmatrix} 3  -1  1 \\ 2  0  1 \\ 1  -1  2 \end{pmatrix}$ 描述的动力系统 $\mathbf{x}_{k+1} = A \mathbf{x}_k$ [@problem_id:2168090]。
1.  **[特征值](@entry_id:154894)**：[特征方程](@entry_id:265849)为 $(\lambda-1)(\lambda-2)^2=0$，所以[特征值](@entry_id:154894)为 $\lambda_1=1$（[代数重数](@entry_id:154240)1）和 $\lambda_2=2$（[代数重数](@entry_id:154240)2）。
2.  **[特征空间](@entry_id:638014)**：
    -   对于 $\lambda_1=1$，特征空间 $E_1$ 的维数为1。
    -   对于 $\lambda_2=2$，通过求解 $(A-2I)\mathbf{v}=\mathbf{0}$，我们发现其[解空间](@entry_id:200470)只有一维，由 $\begin{pmatrix} 1 \\ 1 \\ 0 \end{pmatrix}$ 张成。因此，$\lambda=2$ 的[几何重数](@entry_id:155584)是1，小于其[代数重数](@entry_id:154240)2。矩阵 $A$ 不可[对角化](@entry_id:147016)。
3.  **寻找[广义特征向量](@entry_id:152349)**：我们需要找到一个向量 $\mathbf{w}$ 使得 $(A-2I)\mathbf{w} = \mathbf{u}$，其中 $\mathbf{u} = \begin{pmatrix} 1 \\ 1 \\ 0 \end{pmatrix}$ 是一个[特征向量](@entry_id:151813)。解此方程可得一个解 $\mathbf{w} = \begin{pmatrix} 0 \\ 0 \\ 1 \end{pmatrix}$。
4.  **构造 J 和 P**：我们有一个普通[特征向量](@entry_id:151813) $\mathbf{s}=\begin{pmatrix} 0 \\ 1 \\ 1 \end{pmatrix}$ 对应 $\lambda=1$，一个[特征向量](@entry_id:151813) $\mathbf{u}$ 和一个[广义特征向量](@entry_id:152349) $\mathbf{w}$ 对应 $\lambda=2$。由此构造：
    $$
    P = \begin{pmatrix} \mathbf{u}  \mathbf{w}  \mathbf{s} \end{pmatrix} = \begin{pmatrix} 1  0  0 \\ 1  0  1 \\ 0  1  1 \end{pmatrix}, \quad J = \begin{pmatrix} 2  1  0 \\ 0  2  0 \\ 0  0  1 \end{pmatrix}
    $$
5.  **计算 $A^k$**：与对角化类似，$A^k = P J^k P^{-1}$。关键在于计算 $J^k$。对于若尔当块 $J_2(2) = \begin{pmatrix} 2  1 \\ 0  2 \end{pmatrix}$，其 $k$ 次幂为 $\begin{pmatrix} 2^k  k 2^{k-1} \\ 0  2^k \end{pmatrix}$。因此，$J^k = \begin{pmatrix} 2^k  k 2^{k-1}  0 \\ 0  2^k  0 \\ 0  0  1^k \end{pmatrix}$。
通过这个过程，即使对于不可[对角化](@entry_id:147016)的矩阵，我们依然可以得到 $A^k$ 的封闭表达式，从而分析其驱动的动力系统的演化。表达式中出现的 $k 2^{k-1}$ 项表明，当存在亏损的[重复特征值](@entry_id:154579)时，系统的行为不仅包含[指数增长](@entry_id:141869)/衰减项（$2^k$），还包含与 $k$ 呈[线性关系](@entry_id:267880)的项，这在经济和金融模型的共振或不稳定分析中具有重要意义。