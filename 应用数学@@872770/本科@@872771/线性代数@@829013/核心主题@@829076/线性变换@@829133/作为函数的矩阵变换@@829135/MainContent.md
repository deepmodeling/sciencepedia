## 引言
在线性代数的世界里，矩阵不仅是组织数字的矩形阵列，更是描述空间变换的强大工具。将[矩阵变换](@entry_id:156789)理解为一种函数，是从代数计算到几何直观的关键一步，它揭示了向量、空间及其相互作用的深刻本质。然而，许多学习者常常停留在机械的矩阵乘法上，未能充分领会其作为一种映射所蕴含的丰富内涵和广泛应用价值。本文旨在填补这一认知鸿沟，系统性地将[矩阵变换](@entry_id:156789)置于函数框架下进行剖析。

在接下来的内容中，我们将分三个章节展开探索。第一章**“原则与机制”**将深入探讨[矩阵变换](@entry_id:156789)的定义、线性性质、[标准矩阵](@entry_id:151240)的构建，以及[核与值域](@entry_id:155506)等核心概念，为您构建坚实的理论基础。第二章**“应用与跨学科联系”**将带领您领略这些理论在计算机图形学、控制理论和[量子化学](@entry_id:140193)等前沿领域的实际应用，展示线性代数的强大生命力。最后，第三章**“动手实践”**提供了一系列精心设计的问题，帮助您巩固所学知识，并将理论付诸实践。通过本次学习，您将不仅掌握[矩阵变换](@entry_id:156789)的计算，更能以函数的视角洞察其背后的几何意义与应用逻辑。

## 原则与机制

在线性代数中，我们将[向量空间](@entry_id:151108)之间的映射（或函数）形式化为一种强大的结构，称为**线性变换 (linear transformation)**。当这些空间是有限维实数[向量空间](@entry_id:151108) $\mathbb{R}^n$ 和 $\mathbb{R}^m$ 时，这些变换可以具体地通过矩阵来表示。本章将深入探讨将[矩阵变换](@entry_id:156789)视为[函数的根](@entry_id:169486)本原则与核心机制。我们将从其定义和基本属性出发，探索其结构，并揭示其与矩阵[基本子空间](@entry_id:190076)之间的深刻联系。

### [矩阵变换](@entry_id:156789)的定义：函数视角

一个从 $\mathbb{R}^n$ 到 $\mathbb{R}^m$ 的**变换 (transformation)**（或称函数、映射）$T$，是一个规则，它将 $\mathbb{R}^n$ 中的每一个向量 $\mathbf{x}$ 与 $\mathbb{R}^m$ 中一个唯一的向量 $T(\mathbf{x})$ 对应起来。空间 $\mathbb{R}^n$ 被称为变换 $T$ 的**定义域 (domain)**，而 $\mathbb{R}^m$ 被称为**余定义域 (codomain)**。对于向量 $\mathbf{x} \in \mathbb{R}^n$，向量 $T(\mathbf{x}) \in \mathbb{R}^m$ 被称为 $\mathbf{x}$ 在变换 $T$下的**像 (image)**。

线性代数中最重要的一类变换是那些可以通过矩阵乘法定义的变换。对于一个给定的 $m \times n$ 矩阵 $A$，我们可以定义一个变换 $T: \mathbb{R}^n \to \mathbb{R}^m$，其规则为 $T(\mathbf{x}) = A\mathbf{x}$。这里，输入向量 $\mathbf{x}$ 必须是一个 $n \times 1$ 的列向量（即 $\mathbb{R}^n$ 中的一个元素），矩阵与向量的乘积 $A\mathbf{x}$ 的结果是一个 $m \times 1$ 的列向量（即 $\mathbb{R}^m$ 中的一个元素）。

矩阵的维度直接决定了其对应变换的定义域和余定义域。如果一个矩阵 $A$ 有 $m$ 行和 $n$ 列（即 $A$ 是一个 $m \times n$ 矩阵），那么由 $T(\mathbf{x}) = A\mathbf{x}$ 定义的变换，其定义域的维数是 $n$，余定义域的维数是 $m$。这是因为要使乘积 $A\mathbf{x}$ 有意义，$\mathbf{x}$ 的维数必须与 $A$ 的列数匹配，而结果向量 $A\mathbf{x}$ 的维数则由 $A$ 的行数决定。例如，一个 $5 \times 3$ 的矩阵 $A$ 定义了一个从 $\mathbb{R}^3$ 到 $\mathbb{R}^5$ 的变换，因此其定义域维数为 3，余定义域维数为 5。[@problem_id:1378308]

### 线性：[变换的核](@entry_id:149509)心属性

[矩阵变换](@entry_id:156789)之所以在数学和应用中如此核心，是因为它们具有一个称为**线性 (linearity)** 的基本属性。一个变换 $T$ 被称为线性的，如果它满足以下两个条件：
1.  对于其定义域中的任意向量 $\mathbf{u}$ 和 $\mathbf{v}$，都有 $T(\mathbf{u} + \mathbf{v}) = T(\mathbf{u}) + T(\mathbf{v})$。（保持向量加法）
2.  对于其定义域中的任意向量 $\mathbf{u}$ 和任意标量 $c$，都有 $T(c\mathbf{u}) = cT(\mathbf{u})$。（保持标量乘法）

这两个条件可以合并为一个更通用的表达式：对于任意向量 $\mathbf{v}_1, \mathbf{v}_2, \dots, \mathbf{v}_p$ 和任意标量 $c_1, c_2, \dots, c_p$，线性变换满足：
$$
T(c_1\mathbf{v}_1 + c_2\mathbf{v}_2 + \dots + c_p\mathbf{v}_p) = c_1T(\mathbf{v}_1) + c_2T(\mathbf{v}_2) + \dots + c_pT(\mathbf{v}_p)
$$
这个性质被称为**[叠加原理](@entry_id:144649) (superposition principle)**，它构成了线性系统的基石。它意味着一个线性组合的像，等于其像的[线性组合](@entry_id:154743)。

所有形如 $T(\mathbf{x}) = A\mathbf{x}$ 的[矩阵变换](@entry_id:156789)都是线性的，这源于[矩阵乘法](@entry_id:156035)的分配律和[结合律](@entry_id:151180)。线性性质的威力在于，如果我们知道一个线性变换对少数几个基本向量的作用，我们就可以推断出它对整个[向量空间](@entry_id:151108)的作用。

设想一个信号处理单元，其内部机制未知，但已知它对输入信号的作用是线性的。通过测试，我们得知输入信号 $\mathbf{v}_1$ 产生输出 $\mathbf{y}_1 = T(\mathbf{v}_1)$，输入信号 $\mathbf{v}_2$ 产生输出 $\mathbf{y}_2 = T(\mathbf{v}_2)$。现在，如果我们输入一个新的组合信号 $\mathbf{v}_{\text{new}} = 2\mathbf{v}_1 + 5\mathbf{v}_2$，我们无需知道 $T$ 的具体形式，就可以利用其线性性质预测输出：
$$
\mathbf{y}_{\text{new}} = T(2\mathbf{v}_1 + 5\mathbf{v}_2) = 2T(\mathbf{v}_1) + 5T(\mathbf{v}_2) = 2\mathbf{y}_1 + 5\mathbf{y}_2
$$
如果我们已知 $\mathbf{y}_1 = \begin{pmatrix} 12 \\ -5 \\ 4 \end{pmatrix}$ 和 $\mathbf{y}_2 = \begin{pmatrix} -3 \\ 1 \\ 7 \end{pmatrix}$，那么新的输出就是 $2\begin{pmatrix} 12 \\ -5 \\ 4 \end{pmatrix} + 5\begin{pmatrix} -3 \\ 1 \\ 7 \end{pmatrix} = \begin{pmatrix} 9 \\ -5 \\ 43 \end{pmatrix}$。[@problem_id:1378310]

### [标准矩阵](@entry_id:151240)：变换的蓝图

线性性质有一个更为深刻的推论：任何从 $\mathbb{R}^n$ 到 $\mathbb{R}^m$ 的[线性变换](@entry_id:149133)都可以唯一地表示为一个 $m \times n$ 矩阵的乘法。这个矩阵被称为该[线性变换](@entry_id:149133)的**[标准矩阵](@entry_id:151240) (standard matrix)**。

寻找[标准矩阵](@entry_id:151240)的方法非常直接。$\mathbb{R}^n$ 中的任何向量 $\mathbf{x}$ 都可以表示为其[标准基向量](@entry_id:152417) $\mathbf{e}_1, \mathbf{e}_2, \dots, \mathbf{e}_n$ 的线性组合，其中 $\mathbf{e}_j$ 是第 $j$ 个分量为 1，其余分量为 0 的向量：
$$
\mathbf{x} = \begin{pmatrix} x_1 \\ x_2 \\ \vdots \\ x_n \end{pmatrix} = x_1\mathbf{e}_1 + x_2\mathbf{e}_2 + \dots + x_n\mathbf{e}_n
$$
将线性变换 $T$ 应用于 $\mathbf{x}$，并利用线性性质，我们得到：
$$
T(\mathbf{x}) = T(x_1\mathbf{e}_1 + x_2\mathbf{e}_2 + \dots + x_n\mathbf{e}_n) = x_1T(\mathbf{e}_1) + x_2T(\mathbf{e}_2) + \dots + x_nT(\mathbf{e}_n)
$$
这个表达式揭示了一个关键事实。$T(\mathbf{x})$ 是向量 $T(\mathbf{e}_1), T(\mathbf{e}_2), \dots, T(\mathbf{e}_n)$ 的线性组合，其系数恰好是 $\mathbf{x}$ 的分量。这正是矩阵-向量乘法的定义。因此，我们可以构造一个矩阵 $A$，使其各列恰好是[标准基向量](@entry_id:152417)的像：
$$
A = \begin{pmatrix} T(\mathbf{e}_1)  T(\mathbf{e}_2)  \dots  T(\mathbf{e}_n) \end{pmatrix}
$$
这个矩阵 $A$ 就是 $T$ 的[标准矩阵](@entry_id:151240)，满足 $T(\mathbf{x}) = A\mathbf{x}$。这个矩阵就像是变换的“蓝图”，完全描述了变换的行为。

例如，考虑一个控制机械臂的系统，它将一个来自二维摇杆的输入 $\mathbf{u} \in \mathbb{R}^2$ 映射到机械臂末端在三维空间中的位置 $\mathbf{p} \in \mathbb{R}^3$。这个映射由一个线性变换 $T: \mathbb{R}^2 \to \mathbb{R}^3$ 实现。如果已知对标准输入 $\mathbf{e}_1 = (1, 0)$ 的响应是位置 $\mathbf{p}_1 = (2, 5, -1)$，对标准输入 $\mathbf{e}_2 = (0, 1)$ 的响应是 $\mathbf{p}_2 = (-3, 0, 4)$，那么该变换的[标准矩阵](@entry_id:151240) $A$ 的列就是这两个响应向量：
$$
A = \begin{pmatrix} T(\mathbf{e}_1)  T(\mathbf{e}_2) \end{pmatrix} = \begin{pmatrix} 2  -3 \\ 5  0 \\ -1  4 \end{pmatrix}
$$
有了这个矩阵，我们就可以计算任何复合输入（如 $\mathbf{v} = (4, -2)$）所对应的位置，只需计算 $A\mathbf{v}$ 即可。[@problem_id:1378316]

### 关键[子空间](@entry_id:150286)：值域与核

与任何函数一样，线性变换也有其值域。此外，[线性变换](@entry_id:149133)还有一个特殊的集合，称为核。这两个集合不仅是普通的点集，而且是具有特殊结构的**[子空间](@entry_id:150286) (subspaces)**。

#### 值域与列空间

变换 $T$ 的**值域 (range)**，记作 $\text{range}(T)$ 或 $\text{Im}(T)$，是其定义域中所有向量的像构成的集合。形式上，
$$
\text{range}(T) = \{ T(\mathbf{x}) \mid \mathbf{x} \in \mathbb{R}^n \}
$$
对于由矩阵 $A$ 定义的[线性变换](@entry_id:149133) $T(\mathbf{x}) = A\mathbf{x}$，其值域与矩阵 $A$ 的**[列空间](@entry_id:156444) (column space)**，记作 $\text{Col}(A)$，是完全相同的。[列空间](@entry_id:156444)被定义为 $A$ 的列向量的所有线性组合构成的集合。

这两者之间的等价关系源于矩阵-向量乘法的定义。如果 $A$ 的列是 $\mathbf{a}_1, \dots, \mathbf{a}_n$，$\mathbf{x}$ 的分量是 $x_1, \dots, x_n$，那么：
$$
T(\mathbf{x}) = A\mathbf{x} = x_1\mathbf{a}_1 + x_2\mathbf{a}_2 + \dots + x_n\mathbf{a}_n
$$
这个等式表明，变换的每一个输出 $T(\mathbf{x})$ 都不过是矩阵 $A$ 的列向量的一个[线性组合](@entry_id:154743)。因此，所有可能输出的集合（值域）就是所有可能的列向量[线性组合](@entry_id:154743)的集合（列空间）。这个概念是连接变换的几何行为与矩阵代数属性的桥梁。[@problem_id:1378300]

#### 核与[子空间](@entry_id:150286)性质

变换 $T$ 的**核 (kernel)** 或**[零空间](@entry_id:171336) (null space)**，记作 $\ker(T)$ 或 $\text{Nul}(A)$，是其定义域中所有被映射到余定义域中[零向量](@entry_id:156189) $\mathbf{0}$ 的向量集合。形式上，
$$
\ker(T) = \{ \mathbf{x} \in \mathbb{R}^n \mid T(\mathbf{x}) = \mathbf{0} \}
$$
在应用中，核代表了那些在变换下“消失”或被“压平”的输入。例如，在计算机图形学中，一个将三维物体投影到二维屏幕的变换，其核就可能对应于从观察者视点出发并穿过原点的视线上的所有点。[@problem_id:1378284]

核的一个关键性质是，它始终是定义域 $\mathbb{R}^n$ 的一个[子空间](@entry_id:150286)。要证明这一点，我们只需验证它对向量加法和标量乘法是封闭的。假设 $\mathbf{u}$ 和 $\mathbf{w}$ 都在 $\ker(T)$ 中，这意味着 $T(\mathbf{u}) = \mathbf{0}$ 且 $T(\mathbf{w}) = \mathbf{0}$。对于任意标量 $a$ 和 $b$，考虑[线性组合](@entry_id:154743) $a\mathbf{u} + b\mathbf{w}$：
$$
T(a\mathbf{u} + b\mathbf{w}) = aT(\mathbf{u}) + bT(\mathbf{w}) = a\mathbf{0} + b\mathbf{0} = \mathbf{0}
$$
这表明 $a\mathbf{u} + b\mathbf{w}$ 也在 $\ker(T)$ 中。因此，核是一个[子空间](@entry_id:150286)。[@problem_id:1378284]

### 变换的属性：[单射](@entry_id:183792)、满射与维数

通过研究值域和核，我们可以对线性变换进行更精细的分类，特别是关于它们是否为**[单射](@entry_id:183792) (one-to-one)** 或**满射 (onto)**。

#### 单射（一对一）变换

一个变换 $T$ 被称为**单射**的（或**一对一 (one-to-one)**、**内射 (injective)**），如果定义域中不同的向量总被映射到余定义域中不同的像。也就是说，如果 $\mathbf{u} \neq \mathbf{v}$，则 $T(\mathbf{u}) \neq T(\mathbf{v})$。一个等价的、在处理线性变换时更方便的判据是：$T$ 是单射的，当且仅当方程 $T(\mathbf{x}) = \mathbf{0}$ 只有唯一的解 $\mathbf{x} = \mathbf{0}$。换言之，$T$ 是[单射](@entry_id:183792)的当且仅当其核是平凡[子空间](@entry_id:150286) $\{\mathbf{0}\}$。

对于[矩阵变换](@entry_id:156789) $T(\mathbf{x}) = A\mathbf{x}$，这意味着方程 $A\mathbf{x}=\mathbf{0}$ 只有平凡解，这等价于矩阵 $A$ 的各列是[线性无关](@entry_id:148207)的。

如果一个变换是[单射](@entry_id:183792)的，那么对于值域中的任意一个向量 $\mathbf{b}$，方程 $A\mathbf{x} = \mathbf{b}$ 最多只有一个解。它可能有唯一的解（如果 $\mathbf{b}$ 在值域内），也可能没有解（如果 $\mathbf{b}$ 在值域外）。例如，一个由 $3 \times 2$ 矩阵 $A$（其列[线性无关](@entry_id:148207)）定义的变换 $T: \mathbb{R}^2 \to \mathbb{R}^3$ 是单射的，因为其核为 $\{\mathbf{0}\}$。这意味着对于任何目标位置 $\mathbf{b} \in \mathbb{R}^3$，最多只有一个输入 $\mathbf{x} \in \mathbb{R}^2$ 可以达到它。[@problem_id:1378302]

#### 满射（映上）变换

一个变换 $T: \mathbb{R}^n \to \mathbb{R}^m$ 被称为**满射**的（或**映上 (onto)**、**外射 (surjective)**），如果其值域覆盖了整个余定义域 $\mathbb{R}^m$。也就是说，对于余定义域中的任意向量 $\mathbf{b}$，都至少存在一个定义域中的向量 $\mathbf{x}$ 使得 $T(\mathbf{x}) = \mathbf{b}$。

对于[矩阵变换](@entry_id:156789) $T(\mathbf{x}) = A\mathbf{x}$，这等价于说矩阵 $A$ 的列[向量张成](@entry_id:152883)了整个余定义域 $\mathbb{R}^m$。

#### 维数的限制与秩-零度定理

一个变换能否成为单射或满射，常常受到其定义域和余定义域维数的严格限制。这些限制可以通过**[秩-零度定理](@entry_id:154441) (Rank-Nullity Theorem)** 来精确描述。该定理指出，对于任何由 $m \times n$ 矩阵 $A$ 代表的[线性变换](@entry_id:149133) $T: \mathbb{R}^n \to \mathbb{R}^m$：
$$
\dim(\text{Col}(A)) + \dim(\text{Nul}(A)) = n
$$
这里，$\text{rank}(A) = \dim(\text{Col}(A))$ 是矩阵的**秩**，即值域的维数；$\text{nullity}(A) = \dim(\text{Nul}(A))$ 是矩阵的**[零度](@entry_id:156285)**，即核的维数。定理可以简洁地写为：
$$
\text{秩} + \text{零度} = \text{列数}
$$

这个定理揭示了维数之间的深刻制约关系：
1.  **当定义域维数大于余定义域维数时 ($n  m$)**：考虑一个变换 $T: \mathbb{R}^4 \to \mathbb{R}^2$。其[标准矩阵](@entry_id:151240) $A$ 是一个 $2 \times 4$ 矩阵。值域是 $\mathbb{R}^2$ 的一个[子空间](@entry_id:150286)，所以其维数（秩）最多为 2，即 $\text{rank}(A) \le 2$。根据[秩-零度定理](@entry_id:154441)，核的维数（[零度](@entry_id:156285)）为 $\text{nullity}(A) = 4 - \text{rank}(A) \ge 4 - 2 = 2$。因为[零度](@entry_id:156285)至少为 2，核中必然包含非[零向量](@entry_id:156189)，所以该变换**不可能**是[单射](@entry_id:183792)的。[@problem_id:1378307]

2.  **当定义域维数小于余定义域维数时 ($n  m$)**：考虑一个变换 $T: \mathbb{R}^2 \to \mathbb{R}^4$。其[标准矩阵](@entry_id:151240) $A$ 是一个 $4 \times 2$ 矩阵。值域由 $A$ 的两列张成，所以其维数最多为 2，即 $\text{rank}(A) \le 2$。由于余定义域 $\mathbb{R}^4$ 的维数是 4，值域的维数严格小于余定义域的维数。因此，值域不可能是整个 $\mathbb{R}^4$，该变换**不可能**是满射的。一个由二维摇杆控制的四关节机械臂，其所有可达的构型（值域）最多形成 $\mathbb{R}^4$ 中的一个二维平面（或一条线），而无法覆盖所有可能的四维[构型空间](@entry_id:149531)。[@problem_id:1378283]

### [变换的复合](@entry_id:149828)与逆

#### [变换的复合](@entry_id:149828)

如同普通函数一样，线性变换也可以进行**复合 (composition)**。如果我们有两个线性变换，$T: \mathbb{R}^n \to \mathbb{R}^k$ 和 $S: \mathbb{R}^k \to \mathbb{R}^m$，我们可以定义复合变换 $(S \circ T): \mathbb{R}^n \to \mathbb{R}^m$，其作用为 $(S \circ T)(\mathbf{x}) = S(T(\mathbf{x}))$。这意味着先对 $\mathbf{x}$ 应用 $T$，再对结果应用 $S$。

如果 $T$ 和 $S$ 分别由矩阵 $A$ (一个 $k \times n$ 矩阵) 和 $B$ (一个 $m \times k$ 矩阵) 表示，那么复合变换 $S \circ T$ 也是一个线性变换，其[标准矩阵](@entry_id:151240)恰好是矩阵乘积 $BA$。
$$
(S \circ T)(\mathbf{x}) = S(T(\mathbf{x})) = B(A\mathbf{x}) = (BA)\mathbf{x}
$$

#### 可逆变换

一个[线性变换](@entry_id:149133) $T: \mathbb{R}^n \to \mathbb{R}^n$ 被称为**可逆的 (invertible)**，如果存在一个变换 $S: \mathbb{R}^n \to \mathbb{R}^n$ 使得对于所有 $\mathbf{x} \in \mathbb{R}^n$，$S(T(\mathbf{x})) = \mathbf{x}$ 和 $T(S(\mathbf{x})) = \mathbf{x}$ 都成立。这个变换 $S$ 被称为 $T$ 的**逆 (inverse)**，记作 $T^{-1}$。

一个[线性变换](@entry_id:149133)是可逆的，当且仅当它是[单射](@entry_id:183792)且满射的。对于方阵变换 $T: \mathbb{R}^n \to \mathbb{R}^n$，这等价于其[标准矩阵](@entry_id:151240) $A$ 是一个可逆矩阵，也等价于 $\det(A) \neq 0$。从[核与值域](@entry_id:155506)的角度看，$T$ 可逆等价于 $\ker(T) = \{\mathbf{0}\}$（零度为0），并且根据[秩-零度定理](@entry_id:154441)，这又等价于 $\text{rank}(T) = n$，即值域为整个 $\mathbb{R}^n$。

如果一个[变换的核](@entry_id:149509)是非平凡的（即包含非零向量），那么该变换不可能是[单射](@entry_id:183792)的，因此也不可逆。例如，一个信号处理系统 $T: \mathbb{R}^5 \to \mathbb{R}^5$ 如果其核是一个一维[子空间](@entry_id:150286)（一条穿过原点的直线），那么其零度为 1。根据秩-零度定理，其秩为 $5-1=4$。这意味着该变换既不是[单射](@entry_id:183792)的（因为核非平凡），也不是满射的（因为值域维数是4，小于余定义域维数5）。因此该变换不可逆。对于任何一个可实现的输出信号 $\mathbf{w}$，产生它的所有输入信号的集合将构成一条与核平行的仿射直线。[@problem_id:1378265]

对于[复合变换的逆](@entry_id:197534)，其顺序会反转，这类似于穿鞋和袜子的顺序：要撤销“先穿袜子，再穿鞋”的动作，必须“先脱鞋，再脱袜子”。数学上，如果 $S$ 和 $T$ 都是可逆的[线性变换](@entry_id:149133)，那么它们的复合 $S \circ T$ 也是可逆的，且其逆为：
$$
(S \circ T)^{-1} = T^{-1} \circ S^{-1}
$$
设想一个2D图形变换，先对一个点进行旋转 $T$，再进行缩放 $S$。要撤销这个总变换 $L = S \circ T$，必须先撤销最后施加的缩放（应用 $S^{-1}$），然后再撤销旋转（应用 $T^{-1}$）。因此，正确的“撤销”操作是先进行反向缩放，再进行反向旋转。[@problem_id:1378319]

### [基本子空间](@entry_id:190076)的正交性

最后，我们将[变换的核](@entry_id:149509)与一个更广阔的图景联系起来，即矩阵的[四个基本子空间](@entry_id:154834)。对于任意 $m \times n$ 矩阵 $A$，有四个与之相关的[基本子空间](@entry_id:190076)：
1.  **[列空间](@entry_id:156444) (Column Space)** $\text{Col}(A)$，是 $\mathbb{R}^m$ 的[子空间](@entry_id:150286)。
2.  **零空间 (Null Space)** $\text{Nul}(A)$，是 $\mathbb{R}^n$ 的[子空间](@entry_id:150286)。
3.  **[行空间](@entry_id:148831) (Row Space)** $\text{Row}(A)$，是 $\mathbb{R}^n$ 的[子空间](@entry_id:150286)，由 $A$ 的行[向量张成](@entry_id:152883)。
4.  **[左零空间](@entry_id:150506) (Left Null Space)** $\text{Nul}(A^T)$，是 $\mathbb{R}^m$ 的[子空间](@entry_id:150286)。

我们已经知道，对于变换 $T(\mathbf{x})=A\mathbf{x}$，$\text{range}(T) = \text{Col}(A)$ 且 $\ker(T) = \text{Nul}(A)$。

[线性代数基本定理](@entry_id:190797)的一个核心部分揭示了这些[子空间](@entry_id:150286)之间的[正交关系](@entry_id:145540)。特别地，一个[矩阵的行空间](@entry_id:154476)是其[零空间](@entry_id:171336)在 $\mathbb{R}^n$ 中的**正交补 (orthogonal complement)**。记作：
$$
(\text{Nul}(A))^{\perp} = \text{Row}(A)
$$
这意味着，$\mathbb{R}^n$ 中的每一个向量 $\mathbf{w}$，如果它与[零空间](@entry_id:171336) $\text{Nul}(A)$ 中的**所有**向量都正交，那么 $\mathbf{w}$ 必须位于[行空间](@entry_id:148831) $\text{Row}(A)$ 中，反之亦然。

这个深刻的联系具有实际的计算意义。假设我们正在寻找一个向量 $\mathbf{w} \in \mathbb{R}^4$，它满足两个条件：(1) 它与某个 $3 \times 4$ 矩阵 $A$ 的[零空间](@entry_id:171336)中的所有向量都正交；(2) 它的某些分量是已知的。根据上述定理，条件(1)等价于说“$\mathbf{w}$ 必须是 $A$ 的行向量的一个[线性组合](@entry_id:154743)”。这个事实提供了一组[代数方程](@entry_id:272665)，结合已知的向量分量（条件(2)），我们便可以唯一地确定出向量 $\mathbf{w}$ 的其余未知分量。[@problem_id:1378272] 这一原理将变换的几何性质（如正交性）与矩阵的[代数结构](@entry_id:137052)（如[行空间](@entry_id:148831)）紧密地联系在一起，展示了线性代数内在的和谐与统一。