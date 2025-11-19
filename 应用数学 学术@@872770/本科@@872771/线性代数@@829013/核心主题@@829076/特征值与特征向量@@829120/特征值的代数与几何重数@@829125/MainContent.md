## 引言
[特征值](@entry_id:154894)是线性代数中最核心的概念之一，它揭示了线性变换在特定方向上的拉伸或压缩效应。然而，仅仅列出[特征值](@entry_id:154894)本身并不能完全揭示一个[线性变换](@entry_id:149133)的内在结构。一个[特征值](@entry_id:154894)可以“重复”出现，而这种重[复性](@entry_id:162752)背后隐藏着丰富的代数与几何信息。为了精确地捕捉这些信息，线性代数引入了两个核心概念：**[代数重数](@entry_id:154240)（algebraic multiplicity）**与**[几何重数](@entry_id:155584)（geometric multiplicity）**。

理解这两个[重数](@entry_id:136466)的定义、它们之间的深刻联系以及它们何时相等或不相等，是掌握[矩阵对角化](@entry_id:138930)、若尔当标准型乃至分析[线性动力系统](@entry_id:150282)行为的基石。这两个度量之间的差异或一致性，决定了一个系统是稳定的、可预测的，还是会展现出更复杂的共振行为。

本文将引导您深入探索这一核心主题。在**“原理与机制”**一章中，我们将从基本定义出发，揭示代数与[几何重数](@entry_id:155584)之间的基本不等式，并探讨它们与[矩阵对角化](@entry_id:138930)条件的决定性关系。接着，在**“应用与跨学科联系”**一章中，我们将展示这些理论概念如何在动力系统、[谱图论](@entry_id:150398)、量子力学等领域中发挥作用，连接抽象理论与具体问题。最后，通过**“动手实践”**环节，您将有机会应用所学知识解决具体问题，巩固理解。

## 原理与机制

在对线性算子和矩阵的结构进行深入分析时，[特征值](@entry_id:154894)的概念至关重要。然而，仅仅知道一个矩阵的[特征值](@entry_id:154894)是不够的。为了完全理解算子的行为，我们必须探究每个[特征值](@entry_id:154894)所携带的更深层次的结构信息。这些信息由两个关键的度量来量化：**[代数重数](@entry_id:154240)（algebraic multiplicity）**和**[几何重数](@entry_id:155584)（geometric multiplicity）**。本章将系统地阐述这两个概念的定义、它们之间的基本关系、以及它们在线性代数的核心问题——特别是矩阵的[对角化](@entry_id:147016)——中所扮演的决定性角色。

### 定义重数：代数与几何视角

让我们从形式化的定义开始。对于一个给定的 $n \times n$ 矩阵 $A$，其[特征值](@entry_id:154894)是通过求解特征方程 $\det(A - \lambda I) = 0$ 得到的。这个方程的左边是一个关于 $\lambda$ 的 $n$ 次多项式，称为 $A$ 的**[特征多项式](@entry_id:150909)**，记作 $p_A(\lambda)$。

**[代数重数](@entry_id:154240)（Algebraic Multiplicity, AM）**：一个[特征值](@entry_id:154894) $\lambda_0$ 的[代数重数](@entry_id:154240)，记作 $\text{AM}(\lambda_0)$，是 $\lambda_0$ 作为[特征多项式](@entry_id:150909) $p_A(\lambda)$ 的[根的重数](@entry_id:635479)。换言之，如果特征多项式可以被分解为 $p_A(\lambda) = (\lambda - \lambda_0)^k q(\lambda)$，其中 $q(\lambda_0) \neq 0$，那么 $\lambda_0$ 的[代数重数](@entry_id:154240)就是 $k$。所有[特征值](@entry_id:154894)的[代数重数](@entry_id:154240)之和等于矩阵的维数 $n$。

**[几何重数](@entry_id:155584)（Geometric Multiplicity, GM）**：一个[特征值](@entry_id:154894) $\lambda_0$ 的[几何重数](@entry_id:155584)，记作 $\text{GM}(\lambda_0)$，是其对应的[特征空间](@entry_id:638014)的维数。[特征空间](@entry_id:638014) $E_{\lambda_0}$ 定义为所有满足方程 $A\mathbf{v} = \lambda_0 \mathbf{v}$ 的[特征向量](@entry_id:151813) $\mathbf{v}$（以及[零向量](@entry_id:156189)）所构成的集合。这个集合是一个[向量子空间](@entry_id:151815)，可以等价地表示为矩阵 $(A - \lambda_0 I)$ 的[零空间](@entry_id:171336)，即 $E_{\lambda_0} = \ker(A - \lambda_0 I)$。因此，[几何重数](@entry_id:155584)就是这个[零空间](@entry_id:171336)的维数：$\text{GM}(\lambda_0) = \dim(\ker(A - \lambda_0 I))$。[几何重数](@entry_id:155584)告诉我们对于一个给定的[特征值](@entry_id:154894)，有多少个[线性无关](@entry_id:148207)的[特征向量](@entry_id:151813)。

为了阐明这些定义，我们来看一个具体的例子。假设一个 $4 \times 4$ 矩阵 $A$ 的[特征多项式](@entry_id:150909)为 $p_A(\lambda) = (\lambda - c)^4$，其中 $c$ 是一个实常数。根据定义，[特征值](@entry_id:154894) $c$ 作为[特征多项式的根](@entry_id:270910)出现了 4 次，因此其[代数重数](@entry_id:154240)为 $\text{AM}(c) = 4$。现在，假设我们进一步知道，矩阵 $A - cI$ 的零空间的维数是 2，即 $\dim(\ker(A - cI)) = 2$。根据[几何重数](@entry_id:155584)的定义，[特征值](@entry_id:154894) $c$ 的[几何重数](@entry_id:155584)就是这个维数，即 $\text{GM}(c) = 2$。在这个例子中，该[特征值](@entry_id:154894)的[代数重数](@entry_id:154240)为4，而其[几何重数](@entry_id:155584)为2 [@problem_id:502]。这个简单的例子清晰地展示了两种[重数](@entry_id:136466)是如何从矩阵的不同属性中导出的：一个来自代数计算（特征多项式），另一个来自几何结构（[特征空间](@entry_id:638014)）。

### 基本不等式及其推论

[代数重数](@entry_id:154240)和[几何重数](@entry_id:155584)之间存在一个至关重要的基本关系。对于任何方阵 $A$ 的任意一个[特征值](@entry_id:154894) $\lambda$，其[几何重数](@entry_id:155584)总是不大于其[代数重数](@entry_id:154240)：

$$1 \le \text{GM}(\lambda) \le \text{AM}(\lambda)$$

这个不等式的存在是合理的。[几何重数](@entry_id:155584) $\text{GM}(\lambda) = k$ 意味着我们可以找到 $k$ 个线性无关的[特征向量](@entry_id:151813) $\{\mathbf{v}_1, \dots, \mathbf{v}_k\}$。我们可以将这个基底扩展为整个 $n$ 维空间的一个基底 $\{\mathbf{v}_1, \dots, \mathbf{v}_k, \mathbf{w}_{k+1}, \dots, \mathbf{w}_n\}$。在此基底下，[线性算子](@entry_id:149003) $A$ 的[矩阵表示](@entry_id:146025)将呈现出分块上三角的形式：

$$A' = \begin{pmatrix} \lambda I_k  B \\ 0  C \end{pmatrix}$$

其中 $I_k$ 是 $k \times k$ 的[单位矩阵](@entry_id:156724)。该矩阵的[特征多项式](@entry_id:150909)为 $\det(A' - \lambda' I) = \det(\lambda I_k - \lambda' I_k) \det(C - \lambda' I) = (\lambda - \lambda')^k \det(C - \lambda' I)$。这表明 $\lambda$ 作为[特征多项式的根](@entry_id:270910)，其重数至少为 $k$。由于[相似矩阵](@entry_id:155833)具有相同的[特征多项式](@entry_id:150909)，因此对于原矩阵 $A$，$\text{AM}(\lambda) \ge k = \text{GM}(\lambda)$。不等式的下界 $1 \le \text{GM}(\lambda)$ 是因为根据定义，[特征值](@entry_id:154894)必须至少有一个非零的[特征向量](@entry_id:151813)。

这个基本不等式是理解矩阵结构和对角化问题的基石。两种[重数](@entry_id:136466)之间的差异，即 $\text{AM}(\lambda) - \text{GM}(\lambda)$，量化了矩阵在特定[特征值](@entry_id:154894)方向上的“[特征向量](@entry_id:151813)缺陷”。

### [重数](@entry_id:136466)与矩阵基本属性的联系

代数和[几何重数](@entry_id:155584)的概念与矩阵的其他基本属性（如秩和[转置](@entry_id:142115)）紧密相连。

#### 零[特征值](@entry_id:154894)与[矩阵的秩](@entry_id:155507)

当一个矩阵是奇异的（即不可逆）时，它必然有[特征值](@entry_id:154894) $0$。在这种情况下，[特征值](@entry_id:154894) $0$ 的[几何重数](@entry_id:155584)具有一个特别清晰的解释。根据定义，$\text{GM}(0) = \dim(\ker(A - 0I)) = \dim(\ker(A))$。这个值正是矩阵 $A$ 的**[零度](@entry_id:156285)（nullity）**。

根据线性代数中的**秩-零度定理**，对于一个作用于 $n$ 维[向量空间](@entry_id:151108)的线性算子 $T$（或一个 $n \times n$ 矩阵 $A$），其像的维数（秩）与核的维数（零度）之和等于空间的维数 $n$：

$$\dim(\operatorname{Im}(T)) + \dim(\operatorname{Ker}(T)) = n \quad \text{或} \quad \operatorname{rank}(A) + \operatorname{nullity}(A) = n$$

结合以上关系，我们可以直接将[特征值](@entry_id:154894) $0$ 的[几何重数](@entry_id:155584)与[矩阵的秩](@entry_id:155507) $r = \operatorname{rank}(A)$ 联系起来 [@problem_id:1347049]。

$$\text{GM}(0) = \dim(\ker(A)) = n - \operatorname{rank}(A)$$

这个关系在理论和应用中都非常有用。例如，如果我们知道一个 $3 \times 3$ 矩阵的秩为 1，并且它的[特征多项式](@entry_id:150909)是 $\lambda^3$，我们可以立即推断出相关信息。特征多项式 $\lambda^3$ 表明唯一的[特征值](@entry_id:154894)是 $0$，其[代数重数](@entry_id:154240)为 $\text{AM}(0)=3$。同时，根据[秩-零度定理](@entry_id:154441)，其[几何重数](@entry_id:155584)为 $\text{GM}(0) = 3 - \operatorname{rank}(A) = 3 - 1 = 2$ [@problem_id:961146]。

#### 矩阵的转置与左[特征向量](@entry_id:151813)

一个矩阵 $A$ 和它的[转置](@entry_id:142115) $A^T$ 共享许[多谱](@entry_id:200847)属性。首先，它们的[特征多项式](@entry_id:150909)是相同的，因为 $\det(A - \lambda I) = \det((A - \lambda I)^T) = \det(A^T - \lambda I^T) = \det(A^T - \lambda I)$。这意味着 $A$ 和 $A^T$ 拥有完全相同的[特征值](@entry_id:154894)，并且每个[特征值](@entry_id:154894)的[代数重数](@entry_id:154240)也完全相同。

那么[几何重数](@entry_id:155584)呢？一个[特征值](@entry_id:154894) $\lambda$ 对于 $A$ 的[几何重数](@entry_id:155584)是 $\text{GM}_A(\lambda) = \dim(\ker(A - \lambda I))$。对于 $A^T$，则是 $\text{GM}_{A^T}(\lambda) = \dim(\ker(A^T - \lambda I))$。利用秩-零度定理和[矩阵的秩](@entry_id:155507)等于其[转置](@entry_id:142115)的秩这一基本事实 ($\operatorname{rank}(M) = \operatorname{rank}(M^T)$)，我们可以证明它们的[几何重数](@entry_id:155584)也是相等的 [@problem_id:1347028]：

$$\text{GM}_A(\lambda) = n - \operatorname{rank}(A - \lambda I) = n - \operatorname{rank}((A - \lambda I)^T) = n - \operatorname{rank}(A^T - \lambda I) = \text{GM}_{A^T}(\lambda)$$

这个结论非常重要。$A^T$ 的[特征向量](@entry_id:151813)通常被称为 $A$ 的**左[特征向量](@entry_id:151813)**，因为方程 $A^T\mathbf{w} = \lambda\mathbf{w}$ 等价于 $\mathbf{w}^T A = \lambda \mathbf{w}^T$。因此，上述结论表明，对于任何一个[特征值](@entry_id:154894) $\lambda$，其[线性无关](@entry_id:148207)的右[特征向量](@entry_id:151813)（即 $A$ 的普通[特征向量](@entry_id:151813)）的数量与[线性无关](@entry_id:148207)的左[特征向量](@entry_id:151813)的数量是完全相同的。

### 重数在[对角化](@entry_id:147016)中的决定性作用

对角化是线性代数的核心目标之一。一个 $n \times n$ 矩阵 $A$ 被称为**可[对角化](@entry_id:147016)的（diagonalizable）**，如果存在一个[可逆矩阵](@entry_id:171829) $P$ 和一个[对角矩阵](@entry_id:637782) $D$，使得 $A = PDP^{-1}$。这等价于说 $A$ 拥有一个由 $n$ 个线性无关的[特征向量](@entry_id:151813)构成的基底。

[代数重数](@entry_id:154240)和[几何重数](@entry_id:155584)为我们提供了判断一个矩阵是否可对角化的精确准则。

**对角化定理**：一个 $n \times n$ 矩阵 $A$ 是可[对角化](@entry_id:147016)的，当且仅当以下两个条件同时满足：
1. $A$ 的特征多项式在所考虑的[数域](@entry_id:155558)上完全分裂（即所有根都在该数域内）。对于[复数域](@entry_id:153768) $\mathbb{C}$，这个条件总是满足的。
2. 对于 $A$ 的每一个[特征值](@entry_id:154894) $\lambda$，其[几何重数](@entry_id:155584)等于其[代数重数](@entry_id:154240)，即 $\text{GM}(\lambda) = \text{AM}(\lambda)$。

这个定理的直观解释是：为了构成整个 $n$ 维空间的一个基底，我们需要 $n$ 个[线性无关](@entry_id:148207)的[特征向量](@entry_id:151813)。每个特征空间 $E_{\lambda_i}$ 贡献了 $\text{GM}(\lambda_i)$ 个[线性无关](@entry_id:148207)的[特征向量](@entry_id:151813)。来自不同特征空间的[特征向量](@entry_id:151813)总是[线性无关](@entry_id:148207)的。因此，我们能够获得的[线性无关](@entry_id:148207)[特征向量](@entry_id:151813)的总数是所有[几何重数](@entry_id:155584)之和 $\sum \text{GM}(\lambda_i)$。另一方面，所有[代数重数](@entry_id:154240)之和总是等于 $n$，即 $\sum \text{AM}(\lambda_i) = n$。结合基本不等式 $\text{GM}(\lambda_i) \le \text{AM}(\lambda_i)$，我们得到：

$$\sum \text{GM}(\lambda_i) \le \sum \text{AM}(\lambda_i) = n$$

要使左侧的总和达到 $n$（即可[对角化](@entry_id:147016)的条件），唯一的可能性是对于每一个[特征值](@entry_id:154894) $\lambda_i$，不等式都取等号，即 $\text{GM}(\lambda_i) = \text{AM}(\lambda_i)$。

让我们回到之前那个秩为 1 的 $3 \times 3$ 矩阵的例子 [@problem_id:961146]，其 $\text{AM}(0)=3$ 而 $\text{GM}(0)=2$。由于 $\text{GM}(0) \neq \text{AM}(0)$，我们立即可以断定该矩阵是不可对角化的。

在实际问题中，这个准则的应用非常直接。考虑一个依赖于参数 $\alpha$ 的[上三角矩阵](@entry_id:150931) [@problem_id:1355359]：
$$ A = \begin{pmatrix} -1  \alpha  2 \\ 0  -1  -4 \\ 0  0  7 \end{pmatrix} $$
由于 $A$ 是上三角矩阵，其[特征值](@entry_id:154894)就是对角线上的元素：$\lambda_1 = -1$ 和 $\lambda_2 = 7$。它们的[代数重数](@entry_id:154240)分别为 $\text{AM}(-1)=2$ 和 $\text{AM}(7)=1$。对于 $\lambda_2 = 7$，由于 $\text{AM}(7)=1$，我们必然有 $\text{GM}(7)=1$。因此，矩阵是否可[对角化](@entry_id:147016)完全取决于[特征值](@entry_id:154894) $-1$。$A$ 可对角化的充要条件是 $\text{GM}(-1) = \text{AM}(-1) = 2$。我们计算 $\text{GM}(-1) = \dim(\ker(A+I))$：
$$ A+I = \begin{pmatrix} 0  \alpha  2 \\ 0  0  -4 \\ 0  0  8 \end{pmatrix} $$
对这个[矩阵的零空间](@entry_id:152429)维数进行分析，我们发现只有当 $\alpha = 0$ 时，其[零度](@entry_id:156285)的维数才为 2。若 $\alpha \neq 0$，则零度为 1。因此，该矩阵仅在 $\alpha=0$ 时才是可[对角化](@entry_id:147016)的。

这个例子还揭示了一个深刻的现象：[对角化](@entry_id:147016)性质可能是不稳定的。考虑一个矩阵族 $M(\delta)$，它对于所有 $\delta > 0$ 都是可对角化的。然而，当 $\delta \to 0$ 时，极限矩阵 $M_0 = \lim_{\delta \to 0^+} M(\delta)$ 可能变得不可对角化 [@problem_id:1347027]。这种现象的根本原因在于，当参数连续变化时，[代数重数](@entry_id:154240)通常是稳定的，但[几何重数](@entry_id:155584)可能会发生“跳跃性”的下降，从而在[极限点](@entry_id:177089)上破坏 $\text{AM}=\text{GM}$ 的等式。

### 确保对角化的充分条件

尽管 $\text{AM}=\text{GM}$ 是判断[对角化](@entry_id:147016)的一般性准则，但在某些情况下，我们可以通过更简单的条件来保证矩阵是可[对角化](@entry_id:147016)的。
一个简单的例子是，如果一个 $n \times n$ 矩阵有 $n$ 个互不相同的[特征值](@entry_id:154894)，那么每个[特征值](@entry_id:154894)的[代数重数](@entry_id:154240)都是 1。根据基本不等式，其[几何重数](@entry_id:155584)也必须是 1。因此，$\text{AM}=\text{GM}$ 对所有[特征值](@entry_id:154894)都成立，矩阵必然是可对角化的。

一个更强大的工具是**最小多项式（minimal polynomial）**。矩阵 $A$ 的最小多项式 $m_A(x)$ 是次数最低的、首项系数为 1 的、且满足 $m_A(A)=0$（零矩阵）的多项式。一个基本结论是：**一个矩阵是可[对角化](@entry_id:147016)的，当且仅当其最小多项式没有[重根](@entry_id:151486)。**

这个工具可以优雅地证明某些类别的矩阵总是可对角化的。例如，考虑一个**[投影矩阵](@entry_id:154479)**，它满足 $A^2=A$ [@problem_id:1347029]。这个方程意味着多项式 $q(x) = x^2-x = x(x-1)$ 是 $A$ 的一个[零化多项式](@entry_id:155275)。由于[最小多项式](@entry_id:153598)必须整除任何[零化多项式](@entry_id:155275)，所以 $m_A(x)$ 必然是 $x$、$x-1$ 或 $x(x-1)$ 之一。无论哪种情况，最小多项式的根都是单根（没有重根）。因此，任何[投影矩阵](@entry_id:154479)都是可对角化的。这意味着它的所有[特征值](@entry_id:154894)（只能是 0 或 1）都满足 $\text{GM}(\lambda) = \text{AM}(\lambda)$。

类似地，如果一个[复矩阵](@entry_id:190650) $A$ 满足 $A^k=I$ (单位矩阵) 对于某个整数 $k > 1$ [@problem_id:1347041]，那么它的[最小多项式](@entry_id:153598)必然整除 $x^k-1$。在[复数域](@entry_id:153768)上，$x^k-1$ 的根是 $k$ 个不同的单位根。由于[最小多项式](@entry_id:153598)的根也必须是单根，该矩阵必然是可对角化的。因此，其所有[特征值](@entry_id:154894)的[几何重数](@entry_id:155584)都等于[代数重数](@entry_id:154240)。例如，若已知一个满足 $A^3=I$ 的 $5 \times 5$ 矩阵，其特征多项式为 $p(\lambda) = -(\lambda-1)^3(\lambda-\omega)^2$，我们可以立即得出 $\text{AM}(1)=3$。由于矩阵是可[对角化](@entry_id:147016)的，我们无需计算即可断定 $\text{GM}(1)=3$，即 $\dim(\ker(A-I)) = 3$。

### 当等式不成立时：若尔当标准型的启示

当一个矩阵不可对角化时，意味着至少存在一个[特征值](@entry_id:154894) $\lambda$ 使得 $\text{GM}(\lambda)  \text{AM}(\lambda)$。这表示对应于 $\lambda$ 的[线性无关](@entry_id:148207)的[特征向量](@entry_id:151813)不足以张成其[代数重数](@entry_id:154240)所暗示的“维度”。

在这种情况下，矩阵无法化为[对角形式](@entry_id:264850)，但可以化为一种接近[对角形式](@entry_id:264850)的结构，即**[若尔当标准型](@entry_id:155670)（Jordan Normal Form）**。若尔当标准型是一个分[块对角矩阵](@entry_id:145530)，其对角线上的块是所谓的**[若尔当块](@entry_id:155003)（Jordan blocks）**。一个与[特征值](@entry_id:154894) $\lambda$ 相关的 $k \times k$ 若尔当块形如：

$$ J_k(\lambda) = \begin{pmatrix} \lambda  1   \\  \lambda  1  \\   \ddots  1 \\    \lambda \end{pmatrix} $$

[代数重数](@entry_id:154240)和[几何重数](@entry_id:155584)为我们精确地描述了一个矩阵的若尔当标准型的结构 [@problem_id:1361918]：

- **[代数重数](@entry_id:154240) $\text{AM}(\lambda)$** 等于与[特征值](@entry_id:154894) $\lambda$ 相关的所有若尔当块的尺寸之和。
- **[几何重数](@entry_id:155584) $\text{GM}(\lambda)$** 等于与[特征值](@entry_id:154894) $\lambda$ 相关的若尔当块的数量。

例如，如果一个 $5 \times 5$ 矩阵的[特征值](@entry_id:154894) $\lambda=4$ 满足 $\text{AM}(4)=3$ 和 $\text{GM}(4)=2$，这意味着若尔当标准型中有 2 个与 $\lambda=4$ 相关的若尔当块，它们的尺寸之和为 3。唯一的可能性是一个 $2 \times 2$ 的块和一个 $1 \times 1$ 的块。如果另一个[特征值](@entry_id:154894) $\lambda=-1$ 满足 $\text{AM}(-1)=2$ 和 $\text{GM}(-1)=1$，则意味着只有一个与 $\lambda=-1$ 相关的[若尔当块](@entry_id:155003)，其尺寸必须为 2。

更进一步，我们还可以利用最小多项式来获得关于若尔当块尺寸的更多信息。一个[特征值](@entry_id:154894) $\lambda$ 在最小多项式 $m_A(t)$ 中的[重数](@entry_id:136466) $s$，即 $m_A(t) = (t-\lambda)^s \dots$，决定了与 $\lambda$ 相关的**最大[若尔当块](@entry_id:155003)的尺寸**。

综合这些信息，我们可以对[几何重数](@entry_id:155584)的可能取值范围进行限定。给定一个[特征值](@entry_id:154894) $\lambda$ 的[代数重数](@entry_id:154240) $a$ 和其在[最小多项式](@entry_id:153598)中的[重数](@entry_id:136466) $s$（即最大若尔当块尺寸），其[几何重数](@entry_id:155584) $g$ 必须满足以下不等式 [@problem_id:1347039]：

$$ \lceil a/s \rceil \le g \le a-s+1 $$

这个关系深刻地揭示了[代数重数](@entry_id:154240)、[几何重数](@entry_id:155584)、[最小多项式](@entry_id:153598)和若尔当块结构之间的内在联系，为我们提供了一个全面理解线性算子内在结构的强大框架。