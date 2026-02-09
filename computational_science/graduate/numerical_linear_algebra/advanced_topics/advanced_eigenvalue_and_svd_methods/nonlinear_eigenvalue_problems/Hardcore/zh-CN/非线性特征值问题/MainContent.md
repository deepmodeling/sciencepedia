## 引言
非线性特征值问题（Nonlinear Eigenvalue Problems, NEP）是标准线性特征值问题 $Ax = \lambda x$ 的一个深刻而广泛的推广，在现代科学与工程计算中扮演着日益核心的角色。当一个物理系统的响应或参数依赖于其自身的状态频率或能量时，线性模型便显得力不从心，此时非线性特征值问题便应运而生。它为我们提供了一个强有力的数学框架，用以描述和分析从量子多体系统到宏观结构振动等一系列复杂现象。然而，从线性到非线性的跨越引入了全新的理论挑战和丰富的现象，例如谱的复杂结构、多样的特征值类型以及对扰动的高度敏感性。本文旨在系统性地梳理这一领域，为读者搭建一个从理论到应用的完整知识体系。

在接下来的内容中，我们将分三步深入探索非线性特征值问题的世界。首先，在“**原理与机制**”一章中，我们将奠定坚实的理论基础，从基本定义和分类出发，深入探讨谱的局部与全局性质、特征值的重数与若尔当链结构，以及衡量问题稳定性的关键工具——条件数与伪谱。其次，在“**应用与交叉学科联系**”一章中，我们将展示这些理论的强大生命力，通过量子化学的自洽场计算、结构工程的振动分析、计算电磁学中的色散模型以及数据科学中的张量分解等具体案例，揭示NEP如何成为连接不同学科的桥梁。最后，在“**动手实践**”部分，我们将通过一系列精心设计的计算练习，帮助您将理论知识转化为实际的分析与求解能力，巩固对核心概念的理解。让我们从最根本的原理开始，正式步入非线性特征值问题的研究之旅。

## 原理与机制

在介绍性章节之后，我们现在深入探讨非线性特征值问题（Nonlinear Eigenvalue Problem, NEP）背后的核心原理与机制。本章旨在为读者提供一个严谨的理论框架，从基本定义出发，逐步深入到高级概念，如谱的结构、局部谱理论以及解的稳定性。

### 非线性特征值问题的基本定义

与线性特征值问题 $Ax = \lambda x$ 不同，非线性特征值问题寻求的是一个标量 $\lambda \in \mathbb{C}$ 和一个非零向量 $x \in \mathbb{C}^n$，它们满足如下形式的方程：
$$
T(\lambda)x = 0
$$
其中 $T: \Omega \to \mathbb{C}^{n \times n}$ 是一个定义在复数域 $\Omega \subseteq \mathbb{C}$ 的一个开集上的矩阵值函数。满足该方程的数对 $(\lambda, x)$ 被称为**特征对 (eigenpair)**，其中 $\lambda$ 是**特征值 (eigenvalue)**，$x$ 是对应的**特征向量 (eigenvector)**。

一个自然的问题是，这个定义与我们更熟悉的标量方程 $\det(T(\lambda)) = 0$ 之间有何关系。根据线性代数的基本定理，对于任意一个固定的 $\lambda_0 \in \Omega$，$T(\lambda_0)x = 0$ 存在非零解 $x$ 的充要条件是矩阵 $T(\lambda_0)$ 是奇异的，即 $\det(T(\lambda_0)) = 0$。因此，在任何给定的点 $\lambda_0$ 上，这两个条件是完全等价的，无论函数 $T(\cdot)$ 是否具有解析性等良好性质。

然而，当我们考虑整个特征值集合（即**谱 (spectrum)**）的性质时，函数 $T(\cdot)$ 的全局属性就变得至关重要。

*   **正则解析情形**: 如果 $T(\lambda)$ 在 $\Omega$ 上是解析的（即其每个元素都是 $\lambda$ 的解析函数），并且是**正则 (regular)**的，意味着函数 $f(\lambda) = \det(T(\lambda))$ 在 $\Omega$ 上不恒为零，那么根据复分析中的恒等定理，该解析函数的零点集在 $\Omega$ 内是离散的。在这种标准且行为良好的情况下，特征值是孤立的。因此，寻找特征值就等价于寻找标量解析函数 $\det(T(\lambda))$ 的根 [@problem_id:3561634]。

*   **奇异情形**: 另一方面，如果 $T(\lambda)$ 的行列式在整个定义域 $\Omega$ 上恒为零，即 $\det(T(\lambda)) \equiv 0$ for all $\lambda \in \Omega$，那么对于 $\Omega$ 中的每一个 $\lambda$，$T(\lambda)$ 都是奇异矩阵。这意味着根据特征对的定义，$\Omega$ 中的每一个点都是一个特征值。此时，特征值的集合构成一个连续统，而标量函数 $\det(T(\lambda))$ 无法帮助我们定位任何特定的、离散的特征值。这种情况被称为**奇异问题 (singular problem)**，通常需要更精细的工具来定义有意义的特征值，例如，将特征值定义为那些使得 $\text{rank}(T(\lambda))$ 下降的点 [@problem_id:3561634]。

必须强调，点态等价性 $T(\lambda)x=0, x \neq 0 \iff \det(T(\lambda))=0$ 并不依赖于 $T$ 的解析性。然而，若 $T$ 不具备解析性，$\det(T(\lambda))$ 的零点可能不再是孤立的，例如，它们可以形成一条曲线或一个区域，这使得特征值的分析变得更加复杂。

### 非线性特征值问题的分类

根据矩阵值函数 $T(\lambda)$ 对 $\lambda$ 的依赖关系，NEP 可以被分为几个重要的类别。理解这些分类有助于我们识别问题的结构并选择合适的求解算法 [@problem_id:3561637]。

*   **多项式特征值问题 (Polynomial Eigenvalue Problems, PEP)**: 这是最著名的一类 NEP，其中 $T(\lambda)$ 是一个矩阵多项式：
    $$
    T(\lambda) = P(\lambda) = \sum_{k=0}^{d} \lambda^k A_k
    $$
    其中 $A_k \in \mathbb{C}^{n \times n}$ 是常数系数矩阵，$d$ 是多项式的次数。例如，一个二次特征值问题 (QEP) 具有形式 $T_p(\lambda) = A_0 + \lambda A_1 + \lambda^2 A_2$。

*   **有理特征值问题 (Rational Eigenvalue Problems, REP)**: 当 $T(\lambda)$ 是 $\lambda$ 的有理函数时，我们得到一个 REP。这类问题通常出现在包含频域响应的物理模型中。一个典型的例子是：
    $$
    T_r(\lambda) = A_0 + \lambda A_1 - A_2 (\lambda - \sigma)^{-1}
    $$
    其中 $\sigma$ 是有理函数的一个极点。只要 $\lambda$ 不是极点，问题就是良定义的。

*   **时滞/指数特征值问题 (Delay/Exponential Eigenvalue Problems)**: 这类问题源于对具有时滞效应的动力系统的稳定性分析。其 $T(\lambda)$ 包含形如 $e^{-\tau \lambda}$ 的指数项，其中 $\tau \ge 0$ 是时滞。一个例子是：
    $$
    T_d(\lambda) = A_0 + A_1 e^{-\tau \lambda} + A_2 e^{-2\tau \lambda}
    $$

*   **一般解析特征值问题 (General Analytic Eigenvalue Problems)**: 这是一个更广泛的类别，其中 $T(\lambda)$ 的元素是 $\lambda$ 的一般解析函数，不一定局限于多项式或有理函数。例如，函数中可能包含三角函数或更复杂的指数形式：
    $$
    T_a(\lambda) = A_0 + A_1 \sin(\lambda) + A_2 e^{\lambda^2}
    $$

这些分类并非互斥，例如，多项式问题是有理问题的特例，而它们都是一般解析问题的特例。

### 谱对称性与问题结构

许多源于物理或工程应用的 NEP 具有特殊的代数结构。这些结构不仅是模型内在物理特性的数学体现，而且会导致其谱（特征值集合）具有特定的对称性。设计**保结构算法 (structure-preserving algorithms)** 对于精确保持这些谱对称性至关重要，因为这能确保计算结果的物理意义。以下是一些关键的结构化 NEP 类别 [@problem_id:3561670]。

*   **对称 NEP (Symmetric NEPs)**: 若 $T(\lambda)$ 对于所有 $\lambda$ 都满足 $T(\lambda) = T(\lambda)^{\top}$ 且系数矩阵均为实数，则该 NEP 是对称的。这种结构保证了其谱在复平面上关于实轴共轭对称：如果 $\lambda$ 是一个特征值，那么 $\overline{\lambda}$ 也必定是一个特征值。

*   **回文 NEP (Palindromic NEPs)**: 一类重要的多项式 NEP 是 `*`-回文问题，其系数矩阵满足 $P_k = P_{d-k}^{*}$，其中 $P_k$ 是 $P(\lambda) = \sum_{k=0}^{d} \lambda^k P_k$ 的系数矩阵，$d$ 是次数，$*$ 表示共轭转置。这种结构导致其谱具有**共轭倒数对称性**：如果 $\lambda \neq 0$ 是一个特征值，那么 $1/\overline{\lambda}$ 也必然是特征值。

*   **陀螺 NEP (Gyroscopic NEPs)**: 这类问题通常是二次的，$Q(\lambda) = \lambda^2 M + \lambda G + K$，其中 $M, G, K$ 是实矩阵，$M$（质量矩阵）和 $K$（刚度矩阵）是对称的（$M=M^{\top}, K=K^{\top}$），而 $G$（陀螺矩阵）是反对称的（$G=-G^{\top}$）。这种结构源于旋转动力系统，其谱具有关于虚轴的对称性：如果 $\lambda$ 是一个特征值，那么 $-\overline{\lambda}$ 也是一个特征值。

*   **阻尼振荡器 NEP (Damped-Oscillator NEPs)**: 这类问题也是二次的，$Q(\lambda) = \lambda^2 M + \lambda C + K$，其中 $M, C, K$ 都是实对称矩阵。在标准的振动模型中，$M$ 和 $K$ 是正定的（$M \succ 0, K \succ 0$），而 $C$（阻尼矩阵）是半正定的（$C \succeq 0$）。这些条件保证了系统的稳定性，其所有特征值都位于闭合的左半复平面，即 $\text{Re}(\lambda) \le 0$。

### 局部谱理论：重数与若尔当链

为了深刻理解单个特征值的性质，我们需要引入重数和若尔当链的概念，这构成了 NEP 的局部谱理论。

#### 简单特征值

最简单的情况是**简单特征值 (simple eigenvalue)**。一个特征值 $\lambda_\star$ 被认为是简单的，如果其对应的**右特征向量** $x_\star$ (满足 $T(\lambda_\star)x_\star = 0$) 和**左特征向量** $y_\star$ (满足 $y_\star^* T(\lambda_\star) = 0$) 在某种意义下是唯一的（取决于标量倍数），并且满足一个特定的横截性条件。

形式上，$\lambda_\star$ 是一个简单特征值的条件是 $y_\star^* T'(\lambda_\star) x_\star \neq 0$，其中 $T'(\lambda)$ 是 $T(\lambda)$ 对 $\lambda$ 的导数 [@problem_id:3561639]。这个非零标量在 NEP 理论中扮演着核心角色。它允许我们对左右特征向量进行规范化，一个自然的选择是**双正交规范化 (biorthogonal normalization)**：
$$
y_\star^* T'(\lambda_\star) x_\star = 1
$$
这种规范化并非任意，它深刻地联系着问题的敏感性和 resolvent 的结构。例如，在上述规范化下，矩阵函数 $T(\lambda)^{-1}$ 在 $\lambda_\star$ 处的留数 (residue) 恰好是一个秩为1的矩阵 $x_\star y_\star^*$。此外，对于 $T(\lambda)$ 的一个小的解析扰动 $\Delta T(\lambda)$，特征值的一阶微扰由下式给出：
$$
\delta\lambda = - y_\star^* \Delta T(\lambda_\star) x_\star
$$
这表明 $y_\star^* T'(\lambda_\star) x_\star$ 的大小直接关系到特征值的条件数。

#### 代数重数与几何重数

当 $y_\star^* T'(\lambda_\star) x_\star = 0$ 或 $\dim(\ker(T(\lambda_\star))) > 1$ 时，情况变得更加复杂。我们需要更通用的重数定义 [@problem_id:3561678]。

*   **几何重数 (Geometric Multiplicity)**: 特征值 $\lambda_\star$ 的几何重数 $g$ 定义为 $T(\lambda_\star)$ 的零空间维度，即 $g = \dim(\ker(T(\lambda_\star)))$。它表示与 $\lambda_\star$ 相关联的线性无关的特征向量的数量。

*   **代数重数 (Algebraic Multiplicity)**: 对于解析 NEP，$\lambda_\star$ 的代数重数 $m$ 定义为它作为标量解析函数 $\det(T(\lambda))$ 的零点的阶数。

一般而言，我们总有 $g \le m$。当 $g  m$ 时，我们称该特征值为**亏损的 (defective)**。

#### 若尔当链

亏损特征值的结构通过**若尔当链 (Jordan chains)** 来描述。一条长度为 $\ell$ 的若尔当链是一个向量序列 $(x_0, x_1, \dots, x_{\ell-1})$，其中 $x_0$ 是一个特征向量 ($x_0 \in \ker(T(\lambda_\star)), x_0 \neq 0$)，并且该序列满足一组层次化的方程。这些方程可以通过考虑一个解析向量函数 $x(\lambda) = \sum_{k=0}^{\infty} x_k (\lambda-\lambda_\star)^k$ 并将其代入 $T(\lambda)x(\lambda)=0$ 推导得出。通过比较 $(\lambda-\lambda_\star)$ 的各次幂的系数，我们得到定义若尔当链的方程组 [@problem_id:3561678]：
$$
\sum_{j=0}^{k} \frac{1}{j!} T^{(j)}(\lambda_\star) x_{k-j} = 0, \quad k=0, 1, \dots, \ell-1
$$
其中 $T^{(j)}(\lambda_\star)$ 是 $T$ 在 $\lambda_\star$ 处的 $j$ 阶导数。

*   对于 $k=0$，我们得到 $T(\lambda_\star)x_0 = 0$，这确认了 $x_0$ 是一个特征向量。
*   对于 $k \ge 1$，我们可以递归地求解所谓的**广义特征向量 (generalized eigenvectors)** $x_k$。方程可以重写为：
    $$
    T(\lambda_\star) x_k = - \sum_{j=1}^{k} \frac{1}{j!} T^{(j)}(\lambda_\star) x_{k-j}
    $$
    这个线性方程组只有在右端向量位于 $T(\lambda_\star)$ 的值域内时才有解，这个可解性条件决定了从一个给定特征向量 $x_0$ 出发的若尔当链的最大可能长度。

与一个特征值 $\lambda_\star$ 相关联的，存在一个由 $g$ 条若尔当链组成的**典范系统**，其起始向量 $x_0^{(1)}, \dots, x_0^{(g)}$ 构成了 $\ker(T(\lambda_\star))$ 的一组基。这些链的长度 $\ell_1, \dots, \ell_g$ 被称为**部分重数 (partial multiplicities)**。代数重数就是所有部分重数的总和：$m = \sum_{i=1}^g \ell_i$。

**示例：构造一条若尔当链**

考虑一个具体的 NEP 示例 [@problem_id:3561684]，其中 $T(\lambda) = A + \lambda B + \lambda^{-1} C$，矩阵为
$$
A = \begin{pmatrix} -3  2 \\ -2  0 \end{pmatrix}, \quad
B = \begin{pmatrix} 3  0 \\ 1  0 \end{pmatrix}, \quad
C = \begin{pmatrix} 0  0 \\ 1  0 \end{pmatrix}
$$
我们可以验证 $\lambda_0 = 1$ 是一个特征值。首先计算 $T(1) = A+B+C = \begin{pmatrix} 0  2 \\ 0  0 \end{pmatrix}$。它的行列式为0，并且其零空间由向量 $x_1 = \begin{pmatrix} 1 \\ 0 \end{pmatrix}$ 张成。因此，几何重数 $g=1$。
为了检查它是否为亏损特征值，我们计算 $\det(T(\lambda))$。
$$
T(\lambda) = \begin{pmatrix} -3+3\lambda  2 \\ -2+\lambda+\lambda^{-1}  0 \end{pmatrix} \implies \det(T(\lambda)) = -2(-2+\lambda+\lambda^{-1}) = \frac{-2(\lambda^2-2\lambda+1)}{\lambda} = \frac{-2(\lambda-1)^2}{\lambda}
$$
由于 $(\lambda-1)^2$ 是因子，$\lambda_0=1$ 是一个二重根，所以代数重数 $m=2$。因为 $g=1  m=2$，所以 $\lambda_0=1$ 是一个亏损特征值，它应该有一条长度为2的若尔当链。

我们已经有链的第一个向量 $x_1 = \begin{pmatrix} 1 \\ 0 \end{pmatrix}$。为了找到第二个向量 $x_2$，我们求解方程 $T(1)x_2 = -T'(1)x_1$。
$T'(\lambda) = B - \lambda^{-2}C$，所以 $T'(1) = B-C = \begin{pmatrix} 3  0 \\ 0  0 \end{pmatrix}$。
方程变为：
$$
\begin{pmatrix} 0  2 \\ 0  0 \end{pmatrix} x_2 = - \begin{pmatrix} 3  0 \\ 0  0 \end{pmatrix} \begin{pmatrix} 1 \\ 0 \end{pmatrix} = \begin{pmatrix} -3 \\ 0 \end{pmatrix}
$$
设 $x_2 = \begin{pmatrix} u \\ v \end{pmatrix}$，我们得到方程组 $2v = -3$ 和 $0=0$。这给出了 $v = -3/2$。$u$ 的值没有被约束，为了得到一个唯一解，可以施加一个额外的规范化条件，例如 $e_1^{\top} x_2 = u = 0$。因此，一个合法的广义特征向量是 $x_2 = \begin{pmatrix} 0 \\ -3/2 \end{pmatrix}$。
因此，在 $\lambda_0=1$ 处的一条长度为2的若尔当链是 $\left\{ \begin{pmatrix} 1 \\ 0 \end{pmatrix}, \begin{pmatrix} 0 \\ -3/2 \end{pmatrix} \right\}$。

### 全局谱理论与子空间表示

从对单个特征值的局部视图扩展开来，全局理论关心的是整个谱的分布以及如何同时表示多个特征对。

#### 谱的有限性

在有界域内，特征值的数量是有限的还是无限的？对于解析NEP，答案取决于边界行为。一个核心结果是 [@problem_id:3561649]：
若 $T: \mathcal{U} \to \mathbb{C}^{n \times n}$ 是在一个包含有界闭区域 $\overline{\Omega}$ 的开集 $\mathcal{U}$ 上的解析函数，并且 $T(\lambda)$ 在 $\Omega$ 的边界 $\Gamma = \partial\Omega$ 上处处可逆（非奇异），那么在 $\Omega$ 内部的特征值数量是有限的。

这个结论源于复分析。由于 $T(\lambda)$ 在紧集 $\Gamma$ 上连续且可逆，$\det(T(\lambda))$ 在 $\Gamma$ 上有界且不为零。由于 $\det(T(\lambda))$ 在 $\Omega$ 内解析，其零点（即特征值）必须是孤立的。一个紧集只能包含有限个孤立点，因此 $\Omega$ 内的特征值数量是有限的。

更进一步，利用矩阵版本的**辐角原理 (Argument Principle)**，我们可以精确计算出在 $\Omega$ 内的特征值数量（计入代数重数）：
$$
N = \frac{1}{2\pi i} \int_{\Gamma} \text{tr}(T(\lambda)^{-1} T'(\lambda)) \,d\lambda
$$
这个公式是Keldysh定理的一个推论，它将问题转化为一个复积分，对于数值计算非常有用。这一原理可以推广到无穷维巴拿赫空间中的弗雷德霍姆算子 (Fredholm operators) [@problem_id:3561649]。

#### 不变对

在数值线性代数中，我们经常希望计算一个谱的子集，而不仅仅是单个特征对。**不变对 (invariant pair)** 的概念将线性问题中的不变子空间思想推广到了 NEP [@problem_id:3561636]。

一个**不变对** $(X, S)$ 由一个矩阵 $X \in \mathbb{C}^{n \times p}$ 和一个方阵 $S \in \mathbb{C}^{p \times p}$ 组成，它们满足一个推广的特征值方程。对于多项式 NEP $P(\lambda) = \sum_{k=0}^d A_k \lambda^k$，不变对条件是：
$$
\sum_{k=0}^d A_k X S^k = 0
$$
这个方程通常通过矩阵的**泛函演算 (functional calculus)** 来理解，并记作 $\mathbf{P}(X,S)=0$ 或 $P(S)X=0$。

不变对的核心性质在于它封装了一部分 NEP 的谱信息。具体来说，如果 $(X, S)$ 是一个不变对，并且 $X$ 是列满秩的，那么 $S$ 的每一个特征值 $\mu$ 也是原 NEP $T(\lambda)$ 的一个特征值。如果 $Sy = \mu y$，那么对应的 NEP 特征向量是 $z = Xy$。这可以通过后乘以 $y$ 来验证：
$$
\left(\sum_{k=0}^d A_k X S^k\right) y = \sum_{k=0}^d A_k X (\mu^k y) = \left(\sum_{k=0}^d A_k \mu^k\right) (Xy) = P(\mu) (Xy) = 0
$$
对于标准的线性特征值问题 $T(\lambda) = A - \lambda I$，不变对条件 $A X S^0 + (-I) X S^1 = 0$简化为熟悉的西尔维斯特方程 $AX - XS = 0$，这正是定义 $A$ 的不变子空间 $\text{range}(X)$ 的方程。

### 特征值的稳定性：条件数与伪谱

最后，我们探讨特征值对扰动的敏感性，这是一个在实际应用中至关重要的问题。

#### 特征值条件数

一个简单特征值 $\lambda$ 的**条件数 (condition number)** 量化了当问题数据 $T(\lambda)$ 受到微小扰动时，$\lambda$ 会发生多大变化。对于一个由系数矩阵 $A_i$ 定义的 NEP，其扰动模型通常定义为 $\Delta A_i$ 的范数有界。例如，对于 $P(\lambda)=\sum \lambda^i A_i$，一个规范化的条件数可以定义为：
$$
\kappa_P(\lambda) = \frac{\left(\sum_{i=0}^d |\lambda|^i \|A_i\|_2\right) \|y\|_2 \|x\|_2}{|y^* P'(\lambda) x|}
$$
其中 $x,y$ 是归一化的右、左特征向量。

在求解 PEP 时，一种常用技术是**线性化 (linearization)**，即将 $n \times n$ 的 $d$ 次 PEP 转化为 $dn \times dn$ 的广义线性特征值问题 (GEP) $L(\lambda)z = (\lambda M - N)z = 0$。虽然 GEP 的特征值与原 PEP 完全相同，但它们的条件数可能不同。这是因为线性化过程引入了特定的结构和约束，并且 GEP 的自然扰动模型与原 PEP 的扰动模型并不等价。

例如，对于一个二次问题 $P(\lambda)$ 及其一阶伴随线性化 $L(\lambda)$，即使我们只考虑简单特征值，我们通常会发现 $\kappa_L(\lambda) \neq \kappa_P(\lambda)$ [@problem_id:3561645]。在给定的例子 $P(\lambda) = \lambda^2 I + \operatorname{diag}(-1,-4)$ 中，对于特征值 $\lambda=1$，线性化的条件数是多项式形式条件数的两倍。这意味着线性化后的问题对于某些类型的扰动可能表现出更高的敏感性。选择一个“良好”的线性化（即条件数与原问题相近的线性化）是该领域的一个活跃研究课题。

#### 伪谱

对于非正规问题（其中 $T(\lambda)T(\lambda)^* \neq T(\lambda)^*T(\lambda)$），特征值条件数可能无法完全捕捉系统对扰动的动态响应。**伪谱 (pseudospectrum)** 提供了一个更全面的视图。给定一个容差 $\epsilon > 0$ 和一个权重函数 $\omega(\lambda) > 0$，加权 $\epsilon$-伪谱 $\Lambda_\epsilon^\omega(T)$ 定义为复平面上所有“接近”真实特征值的点的集合。这个“接近”有几个等价的定义 [@problem_id:3561682]：

1.  **基于最小奇异值的定义**: $\lambda$ 属于伪谱，如果 $T(\lambda)$ 接近一个奇异矩阵。矩阵到最近奇异矩阵的距离由其最小奇异值 $\sigma_{\min}$ 度量。因此，
    $$
    \Lambda_{\epsilon}^{\omega}(T) = \{ \lambda \in \Omega : \sigma_{\min}(T(\lambda)) \le \epsilon \,\omega(\lambda) \}
    $$

2.  **基于扰动的定义**: $\lambda$ 属于伪谱，如果它是一个“附近”问题的真实特征值。
    $$
    \Lambda_{\epsilon}^{\omega}(T) = \bigcup_{\|\Delta T(\lambda)\|_2 \le \epsilon \,\omega(\lambda)} \text{spectrum}(T(\lambda)+\Delta T(\lambda))
    $$
    这里的 $\Delta T(\lambda)$ 是一个点态定义的扰动，它不必是 $\lambda$ 的解析函数。

3.  **基于 resolvent 范数的定义**: 如果 $T(\lambda)$ 可逆，$\lambda$ 属于伪谱，如果其 resolvent $(T(\lambda))^{-1}$ 的范数很大。
    $$
    \Lambda_{\epsilon}^{\omega}(T) = \{ \lambda \in \Omega : \|T(\lambda)^{-1}\|_2 \ge (\epsilon \,\omega(\lambda))^{-1} \}
    $$
    （这里约定如果 $T(\lambda)$ 奇异，则 $\|T(\lambda)^{-1}\|_2 = \infty$）。

这些定义是等价的，并为分析非正规 NEP 的稳定性和动态行为提供了强有力的工具。伪谱的形状可以揭示特征值对扰动的潜在巨大敏感性，即使它们的条件数看起来不大。权重函数 $\omega(\lambda)$ 的引入允许我们根据问题的具体情况调整“扰动大小”的度量，例如，在多项式问题中，通常选择 $\omega(\lambda) = \sum |\lambda|^i \|A_i\|_2$。