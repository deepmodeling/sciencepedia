## 引言
矩阵多项式在科学与工程领域中无处不在，从机械结构的振动分析到现代控制系统的设计，它们为描述复杂的动态行为提供了自然的数学语言。这些模型常常引出一个核心的数学难题：多项式特征值问题（Polynomial Eigenvalue Problem, PEP）。直接求解这些高阶非线性问题在分析上和数值上都充满挑战，因此需要一种系统性的方法来攻克它们。

本文的核心正是解决这一挑战的强大技术：线性化。其本质思想是将一个看似棘手的非线性问题，转化为一个我们所熟知的、规模更大但结构更简单的线性代数问题，从而利用成熟的数值算法进行求解。这一转化是现代数值线性代数工具箱中不可或缺的一环。

本文将分为三个部分，系统地引导读者掌握这一工具。在“原理与机制”一章中，我们将建立线性化的严谨理论基础，从经典的伴随形式讲到更现代的线性化族。接下来，在“应用与交叉学科联系”中，我们将展示这些理论如何在结构动力学、系统稳定性分析等实际问题中发挥作用，并探讨其中的数值挑战与最佳实践。最后，“动手实践”部分将提供具体的计算练习，帮助读者将理论知识转化为解决实际问题的能力。

## 原理与机制

在本章中，我们将深入探讨矩阵多项式线性化的核心原理与机制。线性化是将高阶多项式特征值问题（Polynomial Eigenvalue Problem, PEP）转化为一个等价的、更大尺寸的广义特征值问题（Generalized Eigenvalue Problem, GEP）的基本技术。这一转化使得我们可以利用成熟的、数值稳定的线性代数算法来求解多项式特征值问题。我们将从基本定义出发，通过具体构造展示线性化的过程，并最终建立一个严谨的理论框架来保证其有效性。

### 矩阵多项式特征值问题的形式化定义

我们首先需要精确地定义研究的对象。一个 **矩阵多项式** $P(\lambda)$ 是一个以标量 $\lambda \in \mathbb{C}$ 为变量，矩阵为系数的多项式函数，其形式为：
$$
P(\lambda) = \sum_{i=0}^{d} A_i \lambda^i
$$
其中系数矩阵 $A_i \in \mathbb{C}^{n \times n}$ 是 $n \times n$ 的复矩阵。

在处理矩阵多项式时，区分 **阶（grade）** 和 **次数（degree）** 是至关重要的 [@problem_id:3556293]。

- **阶 ($d$)**：阶是一个表示上的参数，它定义了多项式表示中系数索引的范围 $\{0, 1, \dots, d\}$。选择一个阶 $d$ 意味着我们考虑的是一个由 $d+1$ 个系数矩阵 $\{A_0, \dots, A_d\}$ 构成的序列。阶可以大于多项式的实际次数，这意味着允许存在零前导系数矩阵（即 $A_d=0$）。

- **次数 ($k$)**：次数是多项式 $P(\lambda)$ 的一个内在属性，定义为非零系数矩阵的最高索引，即 $k = \max\{i \in \{0, \dots, d\} : A_i \neq 0\}$。如果所有系数矩阵都为零，则次数定义为 $-\infty$。

选择一个比次数大的阶（即 $d > k$）并不会改变 $P(\lambda)$ 作为 $\lambda$ 的函数，因此也不会改变其有限特征值。然而，阶的选择会影响无限特征值的描述以及标准线性化（如伴随形式）的规模，其尺寸通常为 $dn \times dn$。

**多项式特征值问题 (PEP)** 的目标是寻找一个标量 $\lambda \in \mathbb{C} \cup \{\infty\}$ 和一个非零向量 $x \in \mathbb{C}^n$，使得 $P(\lambda)x = 0$。这里的 $\lambda$ 称为 **特征值**，$x$ 称为相应的 **特征向量**。

根据其行列式的性质，矩阵多项式可以分为两类 [@problem_id:3556354]：

- **正则 (Regular) 矩阵多项式**：如果其行列式 $\det P(\lambda)$ 不是关于 $\lambda$ 的零多项式（即 $\det P(\lambda) \not\equiv 0$），则称 $P(\lambda)$ 是正则的。对于正则多项式，有限特征值是标量多项式 $\det P(\lambda) = 0$ 的根。

- **奇异 (Singular) 矩阵多项式**：如果 $\det P(\lambda) \equiv 0$，则称 $P(\lambda)$ 是奇异的。奇异多项式在整个复平面上都存在秩亏，其结构由最小指标（minimal indices）描述。

对于一个正则的 $n \times n$ 矩阵多项式，其特征值的总数（计算代数重数并包含无限特征值）等于 $nd$，其中 $d$ 是其阶。有限特征值的总数等于 $\det P(\lambda)$ 的次数。当且仅当最高阶系数矩阵 $A_d$ 非奇异（即 $\det A_d \neq 0$）时，$\det P(\lambda)$ 的次数恰好为 $nd$，此时 $P(\lambda)$ 拥有 $nd$ 个有限特征值。如果 $A_d$ 是奇异的，则 $\det P(\lambda)$ 的次数将严格小于 $nd$，这意味着 $P(\lambda)$ 拥有少于 $nd$ 个有限特征值，缺失的特征值被认为是 **无限特征值** [@problem_id:3556354]。

### 线性化原理：从多项式到线性问题

解决 PEP 的核心策略是将其转化为一个结构更简单、但规模更大的 GEP。这个过程被称为 **线性化**。一个矩阵多项式 $P(\lambda)$ 的线性化是一个 **矩阵束 (matrix pencil)** $L(\lambda) = \mathcal{A} - \lambda \mathcal{B}$，其广义特征值与 $P(\lambda)$ 的特征值以某种精确的方式对应。

为了直观地理解这一过程，我们以一个二次矩阵多项式为例进行构造 [@problem_id:3556314]。考虑一个二次 PEP：
$$
P(\lambda)x = (A_2 \lambda^2 + A_1 \lambda + A_0)x = 0
$$
其中 $x \in \mathbb{C}^n$ 是非零特征向量。我们的目标是构建一个尺寸为 $2n \times 2n$ 的矩阵束 $L(\lambda)$，使其等价于这个二次问题。

我们可以引入一个新的向量变量，例如 $v_1 = \lambda x$。通过这个代换，二次方程可以被重写。原始方程可以变形为：
$$
(\lambda A_2 + A_1)(\lambda x) + A_0 x = 0
$$
将 $v_1 = \lambda x$ 和 $v_2 = x$ 代入，我们得到一个由两个向量方程组成的系统：
$$
\begin{cases}
    (\lambda A_2 + A_1)v_1 + A_0 v_2 = 0 \\
    -v_1 + \lambda v_2 = 0
\end{cases}
$$
这个系统可以写成一个 $2n \times 2n$ 的广义特征值问题的形式 $L(\lambda)v=0$，其中 $v = \begin{pmatrix} v_1 \\ v_2 \end{pmatrix}$，矩阵束 $L(\lambda)$ 为：
$$
L(\lambda) = \begin{pmatrix} \lambda A_2 + A_1 & A_0 \\ -I_n & \lambda I_n \end{pmatrix}
$$
这个矩阵束 $L(\lambda)$ 是 $\lambda$ 的一次函数，可以写成 $\mathcal{A} - \lambda \mathcal{B}$ 的形式，其中：
$$
\mathcal{A} = \begin{pmatrix} -A_1 & -A_0 \\ I_n & 0 \end{pmatrix}, \quad \mathcal{B} = \begin{pmatrix} A_2 & 0 \\ 0 & I_n \end{pmatrix}
$$
（注意：上述 $(\mathcal{A}, \mathcal{B})$ 对是 $L(\lambda)$ 的一种可能表示，通过对块行进行置换和变号可以得到不同的表示）。这个 $L(\lambda)$ 就是 $P(\lambda)$ 的一个线性化。通过块矩阵的行操作（这对应于左乘一个单位模矩阵），可以证明 $\det(L(\lambda))$ 与 $\det(P(\lambda))$ 成比例（在本例中，$\det(L(\lambda)) = \det(P(\lambda))$）。这意味着 $L(\lambda)$ 的有限特征值与 $P(\lambda)$ 的完全一致，包括它们的代数重数 [@problem_id:3556314]。

### 伴随线性化：一种经典构造

上述为二次多项式构造线性化的思想可以推广到任意阶 $d$ 的矩阵多项式，从而得到经典的 **伴随线性化 (companion linearizations)**。对于一个 $d$ 阶的 monic 矩阵多项式 $P(\lambda) = \lambda^d I + \sum_{i=0}^{d-1} A_i \lambda^i$，一个标准的伴随矩阵 $C$ 定义为 [@problem_id:3556335]：
$$
C = \begin{bmatrix}
0_n & 0_n & \cdots & 0_n & -A_0 \\
I_n & 0_n & \cdots & 0_n & -A_1 \\
0_n & I_n & \cdots & 0_n & -A_2 \\
\vdots & \vdots & \ddots & \vdots & \vdots \\
0_n & 0_n & \cdots & I_n & -A_{d-1}
\end{bmatrix}
$$
这是一个 $d \times d$ 的块矩阵，其中每个块是 $n \times n$ 的，总尺寸为 $dn \times dn$。该矩阵具有 **块上Hessenberg结构**，即第一块次对角线下方均为零块。

与此伴随矩阵相关的矩阵束是 $L(\lambda) = \lambda I_{dn} - C$。可以证明，对于 monic 多项式，这个束满足 $\det(L(\lambda)) = \det(P(\lambda))$。因此，标准特征值问题 $Cv = \lambda v$ 的解 $\lambda$ 正是原多项式特征值问题 $P(\lambda)x=0$ 的特征值。这种构造将一个复杂的非线性（多项式）问题转化为了一个标准的线性特征值问题。

### 特征向量恢复：连接两个问题

求解线性化问题 $L(\lambda)v=0$ 只能得到特征值 $\lambda$ 和相应的特征向量 $v \in \mathbb{C}^{dn}$。然而，我们最终需要的是原多项式 $P(\lambda)$ 的特征向量 $x \in \mathbb{C}^n$。幸运的是，向量 $v$ 和 $x$ 之间存在简单的关系。

考虑另一种常见的伴随形式，即 **第一Frobenius伴随束** [@problem_id:3556338]。对于 $d$ 阶 monic 多项式 $P(\lambda)$，其伴随束为：
$$
L(\lambda) = \begin{bmatrix}
\lambda I_n & -I_n & 0 & \cdots & 0 \\
0 & \lambda I_n & -I_n & \cdots & 0 \\
\vdots & & \ddots & & \vdots \\
0 & \cdots & 0 & \lambda I_n & -I_n \\
A_0 & A_1 & \cdots & A_{d-2} & \lambda I_n + A_{d-1}
\end{bmatrix}
$$
如果 $(\lambda, v)$ 是 $L(\lambda)$ 的一个特征对，其中 $v = \begin{bmatrix} v_0^\top & v_1^\top & \cdots & v_{d-1}^\top \end{bmatrix}^\top$ 且 $v_i \in \mathbb{C}^n$，那么从 $L(\lambda)v=0$ 的前 $d-1$ 个块行方程可以推导出：
$$
\lambda v_0 - v_1 = 0 \implies v_1 = \lambda v_0 \\
\lambda v_1 - v_2 = 0 \implies v_2 = \lambda v_1 = \lambda^2 v_0 \\
\vdots \\
v_k = \lambda^k v_0 \quad \text{for } k=1, \dots, d-1
$$
这意味着 $L(\lambda)$ 的特征向量 $v$ 具有一种特殊的 **Vandermonde结构**：
$$
v = \begin{pmatrix} v_0 \\ \lambda v_0 \\ \lambda^2 v_0 \\ \vdots \\ \lambda^{d-1} v_0 \end{pmatrix}
$$
将这个结构代入 $L(\lambda)v=0$ 的最后一个块行方程，经过化简可得 $(\sum_{i=0}^d A_i \lambda^i) v_0 = P(\lambda)v_0 = 0$。由于 $v \neq 0$，可以证明其第一个块 $v_0$ 必定非零。因此，$v_0$ 就是对应于特征值 $\lambda$ 的 $P(\lambda)$ 的特征向量。

这个结论至关重要：通过求解线性化后的 GEP 得到特征向量 $v$，我们可以直接通过提取其第一个（或最后一个，取决于伴随形式） $n$ 维块来恢复原始 PEP 的特征向量 $x$ [@problem_id:3556338]。

### 强线性化：一个严谨的框架

到目前为止，我们的讨论主要集中在有限特征值上。一个完整的理论需要同时处理有限和无限特征值，以及奇异多项式的结构。这引出了 **强线性化 (strong linearization)** 的概念。

首先，我们用更严谨的方式来定义线性化。一个矩阵束 $L(\lambda)$ 是 $P(\lambda)$ 的线性化，如果存在 **单位模 (unimodular)** 矩阵多项式 $U(\lambda)$ 和 $V(\lambda)$（即它们的行列式为非零常数，因此在多项式环上可逆），使得：
$$
U(\lambda) L(\lambda) V(\lambda) = \begin{pmatrix} I_k & 0 \\ 0 & P(\lambda) \end{pmatrix}
$$
这个定义确保了 $L(\lambda)$ 和 $P(\lambda)$ 具有相同的有限特征结构。对于奇异多项式，它还保证了它们的 **左、右最小指标 (left and right minimal indices)** 相同，这些指标描述了其零空间的结构 [@problem_id:3556353]。

为了处理无限特征值，我们引入 **逆转多项式 (reversal polynomial)**。对于一个阶为 $d$ 的矩阵多项式 $P(\lambda)$，其逆转多项式定义为 [@problem_id:3556312]：
$$
\operatorname{rev}_d P(\mu) = \mu^d P(1/\mu) = \sum_{i=0}^{d} A_i \mu^{d-i} = A_d + A_{d-1}\mu + \dots + A_0 \mu^d
$$
$P(\lambda)$ 的无限特征值被定义为 $\operatorname{rev}_d P(\mu)$ 在 $\mu=0$ 处的特征值。从定义可以看出，$\operatorname{rev}_d P(0) = A_d$。因此，$P(\lambda)$ 有无限特征值当且仅当 $\mu=0$ 是 $\operatorname{rev}_d P(\mu)$ 的特征值，这等价于其最高阶系数矩阵 $A_d$ 是奇异的 [@problem_id:3556312]。

现在，我们可以定义 **强线性化**。一个矩阵束 $L(\lambda)$（阶为1）被称为 $P(\lambda)$（阶为d）的强线性化，如果：
1. $L(\lambda)$ 是 $P(\lambda)$ 的线性化。
2. $L(\lambda)$ 的逆转束 $\operatorname{rev}_1 L(\mu)$ 是 $P(\lambda)$ 的逆转多项式 $\operatorname{rev}_d P(\mu)$ 的线性化。

这个双重条件确保了 $L(\lambda)$ 不仅完美地复制了 $P(\lambda)$ 的所有有限特征结构，还通过逆转关系忠实地复制了其无限特征结构。对于任何正则矩阵多项式，经典的伴随形式都是强线性化。

### 超越伴随形式：Fiedler族

经典的伴随形式虽然重要，但它们只是众多可能的线性化中的两种。一个更广泛和灵活的线性化家族是 **Fiedler束 (Fiedler pencils)** [@problem_id:3556306]。

Fiedler束的构造是基于对系数矩阵索引 $\{0, 1, \dots, d-1\}$ 的一个置换 $\sigma$。根据这个置换，可以构建一系列基本的块矩阵因子，将它们相乘便可得到一个与 $\sigma$ 对应的线性化束 $L_\sigma(\lambda)$。这个家族的强大之处在于：

1.  **普适性**：对于任何正则矩阵多项式 $P(\lambda)$，每一个Fiedler束都是其强线性化。
2.  **包含性**：经典的两种伴随形式本身就是Fiedler族中的特例，分别对应于恒等置换 $\sigma = (0, 1, \dots, d-1)$ 和逆序置换 $\sigma = (d-1, \dots, 1, 0)$ [@problem_id:3556306]。
3.  **结构多样性**：通过选择不同的置换，Fiedler束可以展现出不同的块结构，例如块对称、块三对角等，这些结构在特定应用中可能具有计算优势。

Fiedler族以及其他更广义的线性化空间（如 $\mathbb{L}_1$ 和 $\mathbb{L}_2$ 空间）的发现，极大地丰富了我们对线性化的理解和应用。

### 数值实现与计算考量

线性化理论的最终目的是为了数值计算。一旦我们将 PEP $P(\lambda)x=0$ 转化为 GEP $L(\lambda)v=0$（或等价的 $(\mathcal{A}-\lambda\mathcal{B})v=0$），我们就可以使用成熟的数值算法来求解。

对于中等规模的稠密矩阵束，标准的求解算法是 **QZ算法** [@problem_id:3556297]。QZ算法是一种向后稳定的迭代算法，它计算酉矩阵 $Q$ 和 $Z$，将矩阵束 $(\mathcal{A}, \mathcal{B})$ 同时化为上三角形式（广义Schur分解）。分解后，广义特征值 $\lambda$ 可以直接通过两个上三角矩阵对角元素的比值得到。

线性化策略的计算代价是需要重点考虑的。将一个 $n \times n$、阶为 $d$ 的PEP线性化为一个 $dn \times dn$ 的GEP，意味着问题规模显著增大。如果使用标准的稠密QZ算法，其计算复杂度约为 $\mathcal{O}((dn)^3)$ 次浮点运算，内存需求为 $\mathcal{O}((dn)^2)$ [@problem_id:3556297]。这是一个典型的权衡：我们通过扩大问题的维度，将一个非线性的、难以直接处理的问题，转化为了一个结构简单（线性）但规模更大的问题，从而使其能够被强大的标准算法所解决。对于具有特殊结构（如稀疏、对称等）的线性化，可以设计利用这些结构的特定算法以降低计算成本。