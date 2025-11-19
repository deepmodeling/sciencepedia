## 引言
凯莱-[哈密顿定理](@entry_id:193687)是线性代数中的一块基石，它以一种出人意料的方式揭示了任何方阵与其自身特征多项式之间的深刻联系。许多学生在学习线性代数时，常常将矩阵视为对向量进行操作的算子，而忽略了矩阵本身也可以构成一个丰富的代数系统。凯莱-[哈密顿定理](@entry_id:193687)正是连接这两种观点的桥梁，它解决了如何利用矩阵的内在属性来简化复杂矩阵运算（如高次幂和求逆）的难题。本文旨在为读者提供一个关于该定理的全面视角。在“原理与机制”一章中，我们将深入探讨定理的陈述、证明思路及其在核心计算中的威力。随后的“应用与跨学科联系”一章将展示该定理如何超越纯数学，在动力系统、连续介质力学和[微分几何](@entry_id:145818)等领域发挥关键作用。最后，通过“动手实践”部分，读者将有机会亲手应用所学知识解决具体问题，从而巩固理解。

## 原理与机制

在深入探讨凯莱-[哈密顿定理](@entry_id:193687)的原理与机制之前，我们假定读者已对矩阵、[特征值](@entry_id:154894)、[特征向量](@entry_id:151813)以及特征多项式等基本概念有所了解。本章将不再赘述这些基础知识，而是直接阐述定理的核心内容，并展示其在计算与理论层面上的强大威力。

### 凯莱-[哈密顿定理](@entry_id:193687)的陈述

线性代数的一个核心思想是将矩阵视为作用于[向量空间](@entry_id:151108)上的[线性算子](@entry_id:149003)。然而，我们也可以将矩阵本身视为代数系统中的对象，对其进行加法、乘法甚至多项式运算。凯莱-[哈密顿定理](@entry_id:193687)正是连接这两种观点的桥梁，它揭示了任何一个方阵都与其自身的特征多项式存在着深刻的内在联系。

对于一个 $n \times n$ 的方阵 $A$，其**特征多项式** (characteristic polynomial) 定义为 $p_A(\lambda) = \det(\lambda I - A)$，其中 $I$ 是 $n \times n$ 的[单位矩阵](@entry_id:156724)，$\lambda$ 是一个标量变量。这是一个关于 $\lambda$ 的 $n$ 次多项式。

**凯莱-[哈密顿定理](@entry_id:193687) (Cayley-Hamilton Theorem)** 断言：将矩阵 $A$ 本身“代入”其[特征多项式](@entry_id:150909) $p_A(\lambda)$ 中，得到的结果将是零矩阵。即：
$$
p_A(A) = \mathbf{0}
$$

这里需要特别强调，这种“代入”并非简单地在[行列式](@entry_id:142978)表达式 $\det(\lambda I - A)$ 中用 $A$ 替换 $\lambda$，因为 $\det(AI - A) = \det(\mathbf{0}) = 0$ 只是一个标量零，而非我们所需要的[零矩阵](@entry_id:155836)。正确的理解是，若[特征多项式](@entry_id:150909)为 $p_A(\lambda) = c_n \lambda^n + c_{n-1} \lambda^{n-1} + \dots + c_1 \lambda + c_0$，那么定理的结论是：
$$
c_n A^n + c_{n-1} A^{n-1} + \dots + c_1 A + c_0 I = \mathbf{0}
$$
其中 $A^k$ 是矩阵的 $k$ 次幂，$I$ 是[单位矩阵](@entry_id:156724)。

为了更直观地理解这一定理，我们从最简单的 $2 \times 2$ 矩阵入手。对于一个通用的 $2 \times 2$ 矩阵 $A = \begin{pmatrix} a  b \\ c  d \end{pmatrix}$，其特征多项式为：
$$
p_A(\lambda) = \det(\lambda I - A) = \det \begin{pmatrix} \lambda-a  -b \\ -c  \lambda-d \end{pmatrix} = (\lambda-a)(\lambda-d) - bc = \lambda^2 - (a+d)\lambda + (ad-bc)
$$
注意到其中的系数正是矩阵的**迹** (trace) $\text{tr}(A) = a+d$ 和**[行列式](@entry_id:142978)** (determinant) $\det(A) = ad-bc$。因此，$p_A(\lambda) = \lambda^2 - \text{tr}(A)\lambda + \det(A)$。

根据凯莱-[哈密顿定理](@entry_id:193687)，我们有：
$$
A^2 - \text{tr}(A)A + \det(A)I = \mathbf{0}
$$
我们可以通过一个具体的例子来验证这个关系。考虑矩阵 $A = \begin{pmatrix} 3  -2 \\ 4  -1 \end{pmatrix}$。它的迹是 $\text{tr}(A) = 3 + (-1) = 2$，[行列式](@entry_id:142978)是 $\det(A) = (3)(-1) - (-2)(4) = 5$。我们来计算表达式 $A^2 - \text{tr}(A)A$：
$$
A^2 = \begin{pmatrix} 3  -2 \\ 4  -1 \end{pmatrix} \begin{pmatrix} 3  -2 \\ 4  -1 \end{pmatrix} = \begin{pmatrix} 1  -4 \\ 8  -7 \end{pmatrix}
$$
$$
\text{tr}(A)A = 2A = \begin{pmatrix} 6  -4 \\ 8  -2 \end{pmatrix}
$$
因此，
$$
A^2 - \text{tr}(A)A = \begin{pmatrix} 1  -4 \\ 8  -7 \end{pmatrix} - \begin{pmatrix} 6  -4 \\ 8  -2 \end{pmatrix} = \begin{pmatrix} -5  0 \\ 0  -5 \end{pmatrix} = -5I
$$
这恰好等于 $-\det(A)I$。移项后我们得到 $A^2 - 2A + 5I = \mathbf{0}$，从而验证了 $2 \times 2$ 情形下的定理。[@problem_id:1351343]

### 定理的计算应用

凯莱-[哈密顿定理](@entry_id:193687)远不止是一个理论上的优美结论，它更是一个强大的计算工具，能够极大地简化涉及矩阵高次幂和逆的复杂计算。

#### 简化[高阶矩](@entry_id:266936)阵多项式

凯莱-[哈密顿定理](@entry_id:193687)的核心计算价值在于它提供了一个矩阵自身的**零化关系 (annihilation relation)**。对于一个 $n \times n$ 矩阵 $A$，关系式 $p_A(A) = \mathbf{0}$ 允许我们将 $A^n$ 表示为 $I, A, \dots, A^{n-1}$ 的线性组合。[@problem_id:1351330] 进而，任何高于 $n-1$ 次的[矩阵幂](@entry_id:264766) $A^k$ ($k \ge n$) 都可以被递归地降次，最终表示为 $I, A, \dots, A^{n-1}$ 的[线性组合](@entry_id:154743)。

这个过程在形式上等价于[多项式除法](@entry_id:151800)。假设我们需要计算一个矩阵多项式 $Q(A)$，其中 $Q(\lambda)$ 的次数可能很高。我们可以用 $Q(\lambda)$ 除以[特征多项式](@entry_id:150909) $p_A(\lambda)$，得到商 $S(\lambda)$ 和余数 $R(\lambda)$：
$$
Q(\lambda) = S(\lambda)p_A(\lambda) + R(\lambda), \quad \text{其中 } \deg(R)  \deg(p_A) = n
$$
将矩阵 $A$ 代入上式，由于 $p_A(A) = \mathbf{0}$，我们得到：
$$
Q(A) = S(A)p_A(A) + R(A) = S(A)\mathbf{0} + R(A) = R(A)
$$
这意味着计算高次多项式 $Q(A)$ 的问题被简化为计算一个次数小于 $n$ 的多项式 $R(A)$。

例如，假设一个 $2 \times 2$ 矩阵 $A$ 的迹为 $\text{tr}(A) = 5$，[行列式](@entry_id:142978)为 $\det(A) = 3$。其[特征多项式](@entry_id:150909)为 $p_A(\lambda) = \lambda^2 - 5\lambda + 3$。根据凯莱-[哈密顿定理](@entry_id:193687)，$A^2 - 5A + 3I = \mathbf{0}$，即 $A^2 = 5A - 3I$。现在，如果我们想计算 $P(A) = A^3 - 6A^2 + 10A + 2I$，我们无需计算 $A^3$ 和 $A^2$。只需利用 $A^2$ 的关系式：
$$
A^3 = A \cdot A^2 = A(5A - 3I) = 5A^2 - 3A = 5(5A - 3I) - 3A = 25A - 15I - 3A = 22A - 15I
$$
现在将 $A^2$ 和 $A^3$ 的表达式代入 $P(A)$：
$$
P(A) = (22A - 15I) - 6(5A - 3I) + 10A + 2I = (22 - 30 + 10)A + (-15 + 18 + 2)I = 2A + 5I
$$
这个结果表明，无论矩阵 $A$ 具体为何，只要它满足给定的[迹和行列式](@entry_id:149685)条件，其复杂的多项式表达式总能被简化为一个简单的[线性组合](@entry_id:154743)。[@problem_id:1351378]

对于更高阶的矩阵，这种简化方法的优势更为明显。考虑计算一个 $3 \times 3$ 矩阵 $A$ 的[五次多项式](@entry_id:753983) $B = A^5 - 2A^4 - A^3 + 3A^2 + A - 2I$。[@problem_id:1351376] 如果通过蛮力计算 $A^2, A^3, A^4, A^5$ 再进行组合，过程将极其繁琐且容易出错。而使用凯莱-[哈密顿定理](@entry_id:193687)，我们首先计算 $A$ 的[特征多项式](@entry_id:150909)，例如得到 $p_A(\lambda) = \lambda^3 - 2\lambda^2 - \lambda + 2$。这意味着 $A^3 - 2A^2 - A + 2I = \mathbf{0}$。然后我们进行[多项式长除法](@entry_id:272380)：
$$
\lambda^5 - 2\lambda^4 - \lambda^3 + 3\lambda^2 + \lambda - 2 = (\lambda^2)(\lambda^3 - 2\lambda^2 - \lambda + 2) + (\lambda^2 + \lambda - 2)
$$
因此，
$$
B = A^2(A^3 - 2A^2 - A + 2I) + (A^2 + A - 2I) = A^2(\mathbf{0}) + A^2 + A - 2I = A^2 + A - 2I
$$
计算任务从求解五次幂简化为仅需求解二次幂，计算量大大降低。

#### 计算[矩阵的逆](@entry_id:140380)

凯莱-[哈密顿定理](@entry_id:193687)还为计算[可逆矩阵](@entry_id:171829)的逆提供了一种优雅的方法，并深刻地揭示了[矩阵可逆性](@entry_id:152978)与其特征多项式常数项之间的联系。

让我们再次审视 $n \times n$ 矩阵 $A$ 的特征多项式 $p_A(\lambda) = \det(\lambda I - A)$。展开后，其一般形式为：
$$
p_A(\lambda) = \lambda^n + c_{n-1} \lambda^{n-1} + \dots + c_1 \lambda + c_0
$$
其中 $c_0 = p_A(0) = \det(0 \cdot I - A) = \det(-A) = (-1)^n \det(A)$。

根据定理，$p_A(A) = \mathbf{0}$，即：
$$
A^n + c_{n-1} A^{n-1} + \dots + c_1 A + c_0 I = \mathbf{0}
$$
如果矩阵 $A$ 是可逆的，即 $\det(A) \neq 0$，从而 $c_0 \neq 0$，我们可以将上式两边同时右乘 $A^{-1}$：
$$
A^{n-1} + c_{n-1} A^{n-2} + \dots + c_1 I + c_0 A^{-1} = \mathbf{0}
$$
现在，我们可以解出 $A^{-1}$：
$$
A^{-1} = -\frac{1}{c_0} \left[ A^{n-1} + c_{n-1} A^{n-2} + \dots + c_1 I \right]
$$
这个公式的意义是双重的：首先，它表明任何可逆矩阵的逆都可以表示为其自身幂次的一个多项式。其次，它清晰地展示了为什么奇异矩阵（singular matrix）不可逆。一个矩阵是奇异的，当且仅当其[行列式](@entry_id:142978)为零，即 $\det(A) = 0$，这意味着 $c_0 = 0$。在这种情况下，上述公式中的分母为零，导致表达式无意义，从而无法求出[逆矩阵](@entry_id:140380)。这也解释了为什么零是[奇异矩阵](@entry_id:148101)的一个[特征值](@entry_id:154894)。[@problem_id:1351345]

以一个 $3 \times 3$ 矩阵 $A = \begin{pmatrix} 1  2  0 \\ 0  1  1 \\ 1  0  1 \end{pmatrix}$ 为例，我们来求其逆。[@problem_id:1351381] 首先计算[特征多项式](@entry_id:150909)：
$$
p_A(\lambda) = \det(\lambda I - A) = \det \begin{pmatrix} \lambda-1  -2  0 \\ 0  \lambda-1  -1 \\ -1  0  \lambda-1 \end{pmatrix} = (\lambda-1)^3 - 2 = \lambda^3 - 3\lambda^2 + 3\lambda - 3
$$
这里常数项为 $-3$，即 $c_0 = -3 \neq 0$，所以 $A$ 可逆。根据凯莱-[哈密顿定理](@entry_id:193687)：
$$
A^3 - 3A^2 + 3A - 3I = \mathbf{0}
$$
两边右乘 $A^{-1}$：
$$
A^2 - 3A + 3I - 3A^{-1} = \mathbf{0}
$$
解出 $A^{-1}$：
$$
A^{-1} = \frac{1}{3}A^2 - A + I
$$
这样，我们就将求逆运算转化为了矩阵的幂和加法运算。

### 理论意义与关联

除了实用的计算价值，凯莱-[哈密顿定理](@entry_id:193687)在理论上也扮演着至关重要的角色，它将矩阵的代数性质与谱性质（与[特征值](@entry_id:154894)相关的性质）联系起来。

#### 与[特征值](@entry_id:154894)的关系

凯莱-[哈密顿定理](@entry_id:193687)与[特征值](@entry_id:154894)之间存在一个微妙但基础的联系。如果 $\mathbf{v}$ 是矩阵 $A$ 对应于[特征值](@entry_id:154894) $\lambda$ 的一个[特征向量](@entry_id:151813)，那么根据定义有 $A\mathbf{v} = \lambda\mathbf{v}$。这个关系可以推广到任何关于 $A$ 的多项式 $Q(A)$：
$$
A^2\mathbf{v} = A(A\mathbf{v}) = A(\lambda\mathbf{v}) = \lambda(A\mathbf{v}) = \lambda^2\mathbf{v}
$$
以此类推，对于任何多项式 $Q(t) = \sum c_k t^k$，我们有 $Q(A)\mathbf{v} = (\sum c_k A^k)\mathbf{v} = \sum c_k (A^k \mathbf{v}) = \sum c_k (\lambda^k \mathbf{v}) = (\sum c_k \lambda^k) \mathbf{v} = Q(\lambda)\mathbf{v}$。

现在，让我们将这个性质应用于特征多项式 $p_A(\lambda)$。我们有：
$$
p_A(A)\mathbf{v} = p_A(\lambda)\mathbf{v}
$$
由于[特征值](@entry_id:154894) $\lambda$ 是[特征多项式的根](@entry_id:270910)，所以 $p_A(\lambda) = 0$。因此，对于 $A$ 的任何一个[特征向量](@entry_id:151813) $\mathbf{v}$，我们必然有：
$$
p_A(A)\mathbf{v} = 0 \cdot \mathbf{v} = \mathbf{0}
$$
这意味着[矩阵算子](@entry_id:269557) $p_A(A)$ 会将 $A$ 的所有[特征向量](@entry_id:151813)映射到零向量。这个结论本身就很有力。例如，若有一个多项式 $q(\lambda) = p_A(\lambda) + 12$，那么对于 $A$ 的一个[特征向量](@entry_id:151813) $\mathbf{v}$，我们有 $q(A)\mathbf{v} = (p_A(A) + 12I)\mathbf{v} = p_A(A)\mathbf{v} + 12I\mathbf{v} = \mathbf{0} + 12\mathbf{v} = 12\mathbf{v}$。[@problem_id:1351374]

如果一个矩阵 $A$ 是**可[对角化](@entry_id:147016)的 (diagonalizable)**，这意味着它拥有一组[线性无关](@entry_id:148207)的[特征向量](@entry_id:151813)，足以构成整个[向量空间的基](@entry_id:191509)。既然 $p_A(A)$ 将这个基中的每一个向量都映为[零向量](@entry_id:156189)，那么它必然将空间中的任何向量（这些[基向量](@entry_id:199546)的[线性组合](@entry_id:154743)）都映为[零向量](@entry_id:156189)。这直接导致 $p_A(A)$ 必须是零矩阵。这为[可对角化矩阵](@entry_id:150100)的情况提供了一个清晰的证明思路。

#### [零化多项式](@entry_id:155275)与[最小多项式](@entry_id:153598)

[特征多项式](@entry_id:150909) $p_A(\lambda)$ 是一个使得 $p_A(A) = \mathbf{0}$ 的多项式，我们称这样的多项式为 $A$ 的一个**[零化多项式](@entry_id:155275) (annihilating polynomial)**。然而，它不一定是满足该条件的次数最低的多项式。

我们定义**[最小多项式](@entry_id:153598)** (minimal polynomial) $m_A(\lambda)$ 为使得 $m_A(A) = \mathbf{0}$ 的次数最低的[首一多项式](@entry_id:152311)（最高次项系数为1）。[最小多项式](@entry_id:153598)是唯一的，并且它具有一个关键性质：任何其他[零化多项式](@entry_id:155275) $q(\lambda)$（包括[特征多项式](@entry_id:150909) $p_A(\lambda)$）都必须是 $m_A(\lambda)$ 的倍数。即 $m_A(\lambda)$ 整除 $p_A(\lambda)$。

这一概念为我们分析矩阵性质提供了更精细的工具。考虑一个 $5 \times 5$ 矩阵 $A$ 满足 $A^3 - 4A^2 + 3A = \mathbf{0}$。[@problem_id:1351339] 这告诉我们多项式 $q(\lambda) = \lambda^3 - 4\lambda^2 + 3\lambda = \lambda(\lambda-1)(\lambda-3)$ 是 $A$ 的一个[零化多项式](@entry_id:155275)。
由于 $A$ 的[特征值](@entry_id:154894) $\lambda$ 必须是任何[零化多项式](@entry_id:155275)的根（因为 $q(A)\mathbf{v} = q(\lambda)\mathbf{v} = \mathbf{0}$ 且 $\mathbf{v} \neq \mathbf{0}$），所以 $A$ 的所有[特征值](@entry_id:154894)必定来自集合 $\{0, 1, 3\}$。
更进一步，由于 $m_A(\lambda)$ 必须整除 $q(\lambda) = \lambda(\lambda-1)(\lambda-3)$，而 $q(\lambda)$ 的根都是单根，所以 $m_A(\lambda)$ 的根也必然是单根。一个重要的定理指出，一个矩阵在某个域上可[对角化](@entry_id:147016)的充要条件是其最小多项式在该域上可以分解为不同线性因子的乘积（即没有重根）。因此，我们可以断定该矩阵 $A$ 是可对角化的。
基于此，我们可以推断出更多结论：$A$ 的迹 $\text{tr}(A)$ 是其五个[特征值](@entry_id:154894)的和，每个[特征值](@entry_id:154894)都是 $0, 1, 3$ 之一，所以迹必为整数。同样，$\det(A)$ 是[特征值](@entry_id:154894)的乘积，也必为整数。

#### 与[矩阵不变量](@entry_id:195012)的联系

特征多项式的系数本身就是矩阵的重要**[不变量](@entry_id:148850) (invariants)**，即在[相似变换](@entry_id:152935)下保持不变的量。对于 $n \times n$ 矩阵 $A$，其特征多项式 $p_A(\lambda) = \det(\lambda I - A)$ 可以写成：
$$
p_A(\lambda) = \lambda^n - \text{tr}(A)\lambda^{n-1} + \dots + (-1)^n \det(A)
$$
凯莱-[哈密顿定理](@entry_id:193687)将矩阵 $A$ 的代数行为 ($A^n$ 等) 与这些基本[不变量](@entry_id:148850)（[迹和行列式](@entry_id:149685)）直接联系起来。

例如，若已知一个 $3 \times 3$ 矩阵的[特征多项式](@entry_id:150909)为 $p(\lambda) = \lambda^3 - 5\lambda^2 + 2\lambda - 8$。[@problem_id:1351341] 我们可以立刻读出 $\text{tr}(A) = 5$ 和 $(-1)^3 \det(A) = -8$，即 $\det(A) = 8$。由于 $\det(A) \neq 0$，矩阵 $A$ 可逆。我们甚至可以求出 $A^{-1}$ 的迹。设 $A$ 的[特征值](@entry_id:154894)为 $\lambda_1, \lambda_2, \lambda_3$，那么 $A^{-1}$ 的[特征值](@entry_id:154894)为 $1/\lambda_1, 1/\lambda_2, 1/\lambda_3$。我们有：
$$
\text{tr}(A) = \lambda_1 + \lambda_2 + \lambda_3 = 5
$$
$$
\lambda_1\lambda_2 + \lambda_1\lambda_3 + \lambda_2\lambda_3 = 2
$$
$$
\det(A) = \lambda_1\lambda_2\lambda_3 = 8
$$
而 $A^{-1}$ 的迹为：
$$
\text{tr}(A^{-1}) = \frac{1}{\lambda_1} + \frac{1}{\lambda_2} + \frac{1}{\lambda_3} = \frac{\lambda_2\lambda_3 + \lambda_1\lambda_3 + \lambda_1\lambda_2}{\lambda_1\lambda_2\lambda_3} = \frac{2}{8} = \frac{1}{4}
$$
这个例子优美地展示了如何通过特征多项式，结合凯莱-[哈密顿定理](@entry_id:193687)的理论框架，推导出矩阵的深层属性。

### 证明思路探究

尽管凯莱-[哈密顿定理](@entry_id:193687)的陈述简洁明了，其严格证明却并非 trivial。如前所述，简单地将 $\lambda$ 替换为 $A$ 的想法是错误的。

对于可对角化的矩阵，证明是直接的：如果 $A$ 可[对角化](@entry_id:147016)，它就有一组构成空间基的[特征向量](@entry_id:151813) $\{\mathbf{v}_1, \dots, \mathbf{v}_n\}$。我们已经证明，对于每个 $\mathbf{v}_i$，都有 $p_A(A)\mathbf{v}_i = \mathbf{0}$。既然 $p_A(A)$ 将基中的所有向量都变为零向量，那么它作用于空间中任何向量的结果都将是零向量。因此，$p_A(A)$ 必须是[零矩阵](@entry_id:155836)。

然而，并非所有矩阵都可[对角化](@entry_id:147016)。对于一般的矩阵（特别是在[复数域](@entry_id:153768) $\mathbb{C}$ 中），一个标准的证明策略是利用**稠密性论证 (density argument)**。其核心思想是，任何一个 $n \times n$ [复矩阵](@entry_id:190650)都可以被一个序列的[可对角化矩阵](@entry_id:150100)任意逼近。

具体来说，在所有 $n \times n$ [复矩阵](@entry_id:190650)构成的空间中，[可对角化矩阵](@entry_id:150100)是**稠密的 (dense)**。这意味着对于任何矩阵 $A$（无论是否可[对角化](@entry_id:147016)），我们都能找到一个序列的[可对角化矩阵](@entry_id:150100) $\{A_k\}$，使得当 $k \to \infty$ 时，$A_k \to A$。

这个证明思路如下：
1.  对于序列中的每一个[可对角化矩阵](@entry_id:150100) $A_k$，凯莱-[哈密顿定理](@entry_id:193687)成立，即 $p_{A_k}(A_k) = \mathbf{0}$。
2.  矩阵的特征多项式的系数是[矩阵元](@entry_id:186505)素的[连续函数](@entry_id:137361)。因此，当 $A_k \to A$ 时，特征多项式 $p_{A_k}(\lambda)$ 的系数也会收敛到 $p_A(\lambda)$ 的系数。
3.  将 $A$ 代入 $p_{A_k}(\lambda)$ 中，得到矩阵 $p_{A_k}(A)$。由于[矩阵乘法](@entry_id:156035)和加法是连续运算，我们可以得到：
    $$
    \lim_{k \to \infty} p_{A_k}(A_k) = p_A(A)
    $$
4.  因为对于所有的 $k$，$p_{A_k}(A_k) = \mathbf{0}$，所以它们的极限也必然是零矩阵。
    $$
    p_A(A) = \lim_{k \to \infty} \mathbf{0} = \mathbf{0}
    $$

这种方法将一个对所有矩阵都成立的定理的证明，转化为了先证明一个“良好”[子集](@entry_id:261956)（[可对角化矩阵](@entry_id:150100)）成立，然后利用分析中的极限和连续性思想将其推广到整个空间。

一个有趣的计算实例可以帮助我们理解这个逼近过程。[@problem_id:1388659] 考虑一个不可对角化的矩阵 $A = \begin{pmatrix} 1  1  0 \\ 0  1  1 \\ 0  0  1 \end{pmatrix}$。我们可以构造一个可[对角化](@entry_id:147016)的矩阵序列 $A_k = \begin{pmatrix} 1 + \frac{3}{k}  1  0 \\ 0  1 + \frac{2}{k}  1 \\ 0  0  1 + \frac{1}{k} \end{pmatrix}$，它在 $k \to \infty$ 时收敛到 $A$。$A_k$ 的特征多项式为 $p_k(t) = (t-1-\frac{3}{k})(t-1-\frac{2}{k})(t-1-\frac{1}{k})$。根据定理，$p_k(A_k) = \mathbf{0}$。如果我们计算 $p_k(A)$（注意不是 $p_A(A)$ 或 $p_k(A_k)$），我们会发现其结果并非[零矩阵](@entry_id:155836)，但其所有元素都包含 $1/k$ 的因子，当 $k \to \infty$ 时，这些元素都趋于零。这从计算上直观地展示了当 $A_k \to A$ 时，$p_{A_k}(A)$ 如何收敛到 $p_A(A)=\mathbf{0}$ 的过程。