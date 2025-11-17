## 引言
[标准特征值问题](@entry_id:755346)是线性代数和应用数学的基石，它为我们理解线性系统的基本行为提供了深刻的洞见。然而，在许多科学和工程领域，从[结构振动分析](@entry_id:177691)到[量子化学](@entry_id:140193)计算，系统的动态行为或内在属性由两个矩阵相互作用共同决定。这自然地引出了一个更为普适的概念——[广义特征值问题](@entry_id:151614)（GEP）。它不仅是标准问题的直接推广，更是一个强大的数学框架，能够捕捉和解释更为复杂的物理现象。本文旨在为读者提供一个关于[广义特征值问题](@entry_id:151614)的全面而深入的理解，弥合抽象理论与实际应用之间的差距。

为了系统地构建这一知识体系，本文将分为三个核心部分。首先，在“原理与机制”一章中，我们将奠定坚实的理论基础，从广义[特征值](@entry_id:154894)的基本定义出发，深入探讨[矩阵束](@entry_id:751760)、无限[特征值](@entry_id:154894)的概念，并借助Weierstrass和Kronecker[范式理论](@entry_id:169488)揭示其完整的[代数结构](@entry_id:137052)。接着，在“应用与跨学科联系”一章中，我们将展示这些理论如何在物理学、工程学、化学乃至数据科学等不同领域中“大显身手”，通过丰富的实例阐明其作为通用分析工具的强大威力。最后，“动手实践”部分将提供一系列精心设计的计算问题，帮助读者将理论知识转化为解决实际问题的能力。现在，让我们首先进入[广义特征值问题](@entry_id:151614)的核心，探索其精妙的原理与机制。

## 原理与机制

在介绍性章节之后，我们现在深入探讨[广义特征值问题](@entry_id:151614)的核心原理与机制。本章将从基本定义出发，系统地阐述该问题的[代数结构](@entry_id:137052)、[范式理论](@entry_id:169488)以及数值计算中的关键考量。我们的目标是建立一个严谨的理论框架，以便理解和解决科学与工程中出现的各种[广义特征值问题](@entry_id:151614)。

### [广义特征值问题](@entry_id:151614)的基本定义

标准的[特征值问题](@entry_id:142153)寻求一个标量 $\lambda$ 和一个非[零向量](@entry_id:156189) $x$，使得 $Ax = \lambda x$。[广义特征值问题](@entry_id:151614) (Generalized Eigenvalue Problem, GEP) 是这一概念的推广，它涉及两个矩阵 $A, B \in \mathbb{C}^{n \times n}$，其核心方程为：

$Ax = \lambda Bx$

与此问题相关联的核心对象是**[矩阵束](@entry_id:751760) (matrix pencil)**，即一个以参数 $\lambda$ 为变量的矩阵族 $A - \lambda B$。

一个关键的区分在于[矩阵束](@entry_id:751760)的**正则性 (regularity)**。一个[矩阵束](@entry_id:751760) $A - \lambda B$ 被称为**正则的 (regular)**，如果其[行列式](@entry_id:142978) $\det(A - \lambda B)$ 不恒为关于 $\lambda$ 的零多项式。这意味着存在至少一个复数 $\lambda_0$ 使得矩阵 $A - \lambda_0 B$ 是非奇异的（可逆的）。反之，如果对于所有的 $\lambda \in \mathbb{C}$，矩阵 $A - \lambda B$ 都是奇异的，即 $\det(A - \lambda B) \equiv 0$，则该[矩阵束](@entry_id:751760)被称为**奇异的 (singular)** [@problem_id:3587913]。在本章的大部分内容中，我们将首先关注更为常见和结构清晰的正则束。

对于一个正则束，**有限广义[特征值](@entry_id:154894) (finite generalized eigenvalue)** $\lambda$ 被定义为使得 $A - \lambda B$ 奇异的复数。根据矩阵理论，这等价于 $\det(A - \lambda B) = 0$。对于这样一个[特征值](@entry_id:154894) $\lambda$，存在一个相应的非[零向量](@entry_id:156189) $x \in \mathbb{C}^n$，称为**右[广义特征向量](@entry_id:152349) (right generalized eigenvector)**，它满足 $(A - \lambda B)x = 0$，即 $Ax = \lambda Bx$ [@problem_id:3587881]。所有有限[特征值](@entry_id:154894)的集合构成了特征多项式 $p(\lambda) = \det(A - \lambda B)$ 的根集。

例如，考虑两个 $2 \times 2$ 矩阵 $A = \begin{pmatrix} 0  1 \\ 0  0 \end{pmatrix}$ 和 $B = \begin{pmatrix} 0  0 \\ 1  0 \end{pmatrix}$。它们的[矩阵束](@entry_id:751760)为 $A - \lambda B = \begin{pmatrix} 0  1 \\ -\lambda  0 \end{pmatrix}$。其[行列式](@entry_id:142978)为 $\det(A - \lambda B) = \lambda$。这是一个非零多项式，因此该束是正则的。而对于矩阵 $A = \begin{pmatrix} 1  0 \\ 0  0 \end{pmatrix}$ 和 $B = \begin{pmatrix} 2  0 \\ 0  0 \end{pmatrix}$，其[矩阵束](@entry_id:751760)为 $A - \lambda B = \begin{pmatrix} 1 - 2\lambda  0 \\ 0  0 \end{pmatrix}$，[行列式](@entry_id:142978)恒为零。因此，这是一个奇异束 [@problem_id:3587913]。

### 统一框架：射影表述

经典表述 $Ax = \lambda Bx$ 在处理 $B$ 奇异的情况时会遇到困难。例如，如果 $B$ 是奇异的，且 $x$ 位于 $B$ 的零空间中（即 $Bx=0$），那么方程可能对任何 $\lambda$ 都不成立（如果 $Ax \neq 0$），或者可能需要一个“无穷大”的[特征值](@entry_id:154894)。为了优雅地统一处理有限和无穷[特征值](@entry_id:154894)，我们引入**齐次射影表述 (homogeneous projective formulation)** [@problem_id:3587912]。

该表述寻找一个非零向量 $x \in \mathbb{C}^n$ 和一个非零的射影对 $(\alpha, \beta) \in \mathbb{C}^2 \setminus \{(0,0)\}$，使得：

$(\beta A - \alpha B)x = 0$

这里的对 $(\alpha, \beta)$ 是在射影意义上定义的，即它与任何非零标量 $\gamma$ 的乘积 $(\gamma\alpha, \gamma\beta)$ 代表同一个广义[特征值](@entry_id:154894)。

这种表述与经典表述的关系如下：
1.  如果 $\beta \neq 0$，我们可以将方程两边除以 $\beta$，得到 $A x - (\alpha/\beta) B x = 0$。令 $\lambda = \alpha/\beta$，我们就回到了经典形式 $(A - \lambda B)x=0$。因此，任何具有 $\beta \neq 0$ 的解对应一个有限[特征值](@entry_id:154894) $\lambda = \alpha/\beta$。反之，任何有限[特征值](@entry_id:154894) $\lambda$ 及其[特征向量](@entry_id:151813) $x$ 都可以通过选取 $(\alpha, \beta) = (\lambda, 1)$ 在射影框架中表示 [@problem_id:3587912]。
2.  如果 $\beta = 0$，由于 $(\alpha, \beta)$ 不能是[零向量](@entry_id:156189)，所以 $\alpha$ 必须非零。此时方程简化为 $-\alpha Bx = 0$，即 $Bx = 0$。这种情况对应于**无穷大[特征值](@entry_id:154894) (eigenvalue at infinity)**，记为 $\lambda = \infty$。因此，无穷大[特征值](@entry_id:154894)的存在性等价于矩阵 $B$ 的奇异性，其对应的[特征向量](@entry_id:151813)位于 $B$ 的[零空间](@entry_id:171336)中 [@problem_id:3587881] [@problem_id:3587870]。

这种射影方法提供了一个更加对称和完整的视角，自然地将无穷大[特征值](@entry_id:154894)纳入理论体系。

### 无穷大[特征值](@entry_id:154894)详解

让我们更深入地探讨无穷大[特征值](@entry_id:154894)。形式上，处理 $\lambda \to \infty$ 的标准方法是引入一个倒数变量 $\mu = 1/\lambda$，并考察当 $\mu \to 0$ 时的行为。将 $\lambda=1/\mu$ 代入原方程 $Ax = \lambda Bx$ 并乘以 $\mu$（假设 $\lambda \neq 0$），我们得到 $\mu Ax = Bx$，即：

$(B - \mu A)x = 0$

这个方程定义了一个新的[广义特征值问题](@entry_id:151614)，其[矩阵束](@entry_id:751760) $B - \mu A$ 被称为原束 $A - \lambda B$ 的**倒转束 (reversed pencil)**。原问题在 $\lambda = \infty$ 处的特征结构，完全对应于倒转束在 $\mu = 0$ 处的特征结构 [@problem_id:3587870]。

基于此，我们可以精确定义与无穷大[特征值](@entry_id:154894)相关的**[代数重数](@entry_id:154240) (algebraic multiplicity)** 和 **[几何重数](@entry_id:155584) (geometric multiplicity)**。

-   **[几何重数](@entry_id:155584)**：对于任何[特征值](@entry_id:154894)（有限或无穷），其[几何重数](@entry_id:155584)定义为对应特征空间的维数。
    -   对于有限[特征值](@entry_id:154894) $\lambda_i$，[几何重数](@entry_id:155584)是 $\dim(\ker(A - \lambda_i B))$。
    -   对于无穷大[特征值](@entry_id:154894) $\lambda = \infty$，[几何重数](@entry_id:155584)是其在倒转束中对应于 $\mu=0$ 的[特征空间](@entry_id:638014)的维数，即 $\dim(\ker(B - 0 \cdot A)) = \dim(\ker(B))$ [@problem_id:3587881]。

-   **[代数重数](@entry_id:154240)**：
    -   对于有限[特征值](@entry_id:154894) $\lambda_i$，其[代数重数](@entry_id:154240)是它作为[特征多项式](@entry_id:150909) $p(\lambda) = \det(A - \lambda B)$ 的[根的重数](@entry_id:635479)。
    -   对于一个 $n \times n$ 的正则束，所有[特征值](@entry_id:154894)（包括有限和无穷，计入[代数重数](@entry_id:154240)）的总数是 $n$。如果 $p(\lambda)$ 的次数为 $d = \deg(p(\lambda))$，这意味着存在 $d$ 个有限[特征值](@entry_id:154894)（计入重数）。那么，剩下的 $n-d$ 个[特征值](@entry_id:154894)就被认为是无穷大[特征值](@entry_id:154894)。因此，无穷大[特征值](@entry_id:154894)的[代数重数](@entry_id:154240)定义为 $n - d$ [@problem_id:3587870]。可以证明，这个数恰好等于 $\mu=0$ 作为倒转束[特征多项式](@entry_id:150909) $\det(B - \mu A)$ 的[根的重数](@entry_id:635479)。
    -   当且仅当 $B$ 非奇异时，$\deg(\det(A - \lambda B)) = n$，此时不存在无穷大[特征值](@entry_id:154894)。若 $B$ 奇异，则次数 $d  n$，必然存在无穷大[特征值](@entry_id:154894) [@problem_id:3587870]。

需要强调的是，对于一个广义[特征值](@entry_id:154894)（无论是有限还是无穷），其[几何重数](@entry_id:155584)总是小于或等于其[代数重数](@entry_id:154240)。当[几何重数](@entry_id:155584)严格小于[代数重数](@entry_id:154240)时，该[特征值](@entry_id:154894)被称为**亏损的 (defective)**。

### [范式理论](@entry_id:169488)：揭示内在结构

为了彻底理解[矩阵束](@entry_id:751760)的结构，我们需要借助[范式理论](@entry_id:169488)。[范式](@entry_id:161181)是通过等价变换将[矩阵束](@entry_id:751760)化为最简形式，从而揭示其内在的[不变量](@entry_id:148850)。对于[矩阵束](@entry_id:751760)，最重要的[等价关系](@entry_id:138275)是**严格等价 (strict equivalence)**：若存在可逆矩阵 $P$ 和 $Q$，使得 $\tilde{A} = PAQ$ 且 $\tilde{B} = PBQ$，则称矩阵对 $(A,B)$ 与 $(\tilde{A},\tilde{B})$ 是严格等价的。严格等价保持了所有的广义[特征值](@entry_id:154894)及其完整的[代数结构](@entry_id:137052)。

#### 正则束的Weierstrass[范式](@entry_id:161181)

对于任意一个**正则**[矩阵束](@entry_id:751760) $A - \lambda B$，**Weierstrass[范式](@entry_id:161181) (Weierstrass Canonical Form, WCF)** 定理断言，它严格等价于一个特定的块[对角形式](@entry_id:264850)。具体来说，存在[可逆矩阵](@entry_id:171829) $P$ 和 $Q$ 以及一个[整数划分](@entry_id:139302) $n = f+r$，使得 [@problem_id:3587899]：

$PAQ = \begin{pmatrix} J_f  0 \\ 0  I_r \end{pmatrix}, \quad PBQ = \begin{pmatrix} I_f  0 \\ 0  N \end{pmatrix}$

因此，变换后的[矩阵束](@entry_id:751760)为：

$P(A - \lambda B)Q = \begin{pmatrix} J_f - \lambda I_f  0 \\ 0  I_r - \lambda N \end{pmatrix}$

这里的矩阵块具有明确的含义：
-   $J_f$ 是一个大小为 $f \times f$ 的[块对角矩阵](@entry_id:145530)，其对角块是与所有**有限**广义[特征值](@entry_id:154894) $\lambda_i$ 相关联的**若尔当块 (Jordan blocks)** $J_{k_i}(\lambda_i)$。$I_f$ 是相应大小的单位阵。$J_f - \lambda I_f$ 这部分捕捉了所有有限谱的结构。
-   $N$ 是一个大小为 $r \times r$ 的[块对角矩阵](@entry_id:145530)，其对角块是形如 $J_{m_j}(0)$ 的**零幂若尔当块 (nilpotent Jordan blocks)**。$I_r$ 是相应大小的单位阵。$I_r - \lambda N$ 这部分对应于**无穷大**[特征值](@entry_id:154894)。它的[行列式](@entry_id:142978)恒为1，不产生任何有限根，其结构完全由 $N$ 的零幂性决定。

Weierstrass[范式](@entry_id:161181)揭示了[亏损特征值](@entry_id:177573)与[若尔当块](@entry_id:155003)之间的深刻联系。一个 $k \times k$ 的[若尔当块](@entry_id:155003) $J_k(\lambda_i)$ 对应于一个长度为 $k$ 的**[若尔当链](@entry_id:148736) ([Jordan chain](@entry_id:153035))**。对于有限[特征值](@entry_id:154894) $\lambda$，一个长度为 $m$ 的右[广义特征向量链](@entry_id:192049)是一个向量序列 $\{x_1, \dots, x_m\}$，满足 [@problem_id:3587881]：
-   $(A - \lambda B)x_1 = 0$ ($x_1$ 是一个[特征向量](@entry_id:151813))
-   $(A - \lambda B)x_{j+1} = Bx_j$  对于 $j = 1, \dots, m-1$

无穷大[特征值](@entry_id:154894)的[若尔当链](@entry_id:148736)可以通过在倒转束上应用相同的定义来得到。

#### 奇异束的Kronecker[范式](@entry_id:161181)

对于**奇异**[矩阵束](@entry_id:751760)（即 $\det(A - \lambda B) \equiv 0$），其结构比正则束更丰富。**Kronecker[范式](@entry_id:161181) (Kronecker Canonical Form, KCF)** 将Weierstrass[范式](@entry_id:161181)推广到任意[矩阵束](@entry_id:751760)。KCF表明，任何[矩阵束](@entry_id:751760) $A-\lambda B$ 都严格等价于一个块[对角形式](@entry_id:264850)，其对角块除了包含代表有限和无穷[特征值](@entry_id:154894)的正则块（Weierstrass部分）外，还包含两种类型的**奇异块 (singular blocks)** [@problem_id:3587927]：

1.  **右奇异块**: 形如 $L_{\varepsilon}(\lambda)$ 的 $\varepsilon \times (\varepsilon+1)$ 矩阵，例如：
    $L_{\varepsilon}(\lambda) = \begin{bmatrix} -\lambda  1  0  \cdots  0 \\ 0  -\lambda  1  \ddots  \vdots \\ \vdots  \ddots  \ddots  \ddots  0 \\ 0  \cdots  0  -\lambda  1 \end{bmatrix}$
    这些块的存在表明[矩阵束](@entry_id:751760) $A - \lambda B$ 的[右零空间](@entry_id:183083)在[有理函数](@entry_id:154279)域 $\mathbb{C}(\lambda)$ 上是非平凡的。每个 $L_{\varepsilon}$ 块对应一个次数为 $\varepsilon$ 的多项式向量 $x(\lambda) = \sum_{i=0}^{\varepsilon} x_i \lambda^i$，它是[右零空间](@entry_id:183083)的一个[基向量](@entry_id:199546)。整数 $\varepsilon \ge 0$ 被称为**右最小指标 (right minimal index)**。$(A - \lambda B)x(\lambda) \equiv 0$ 的条件等价于一个向量链：$Ax_0=0, Ax_{i}=Bx_{i-1} \text{ for } i=1,\dots,\varepsilon, \text{ and } Bx_{\varepsilon}=0$。

2.  **左奇异块**: 形如 $L_{\eta}(\lambda)^{\mathsf{T}}$ 的 $(\eta+1) \times \eta$ 矩阵。它们对应于[左零空间](@entry_id:150506)的结构，其大小由**左最小指标 (left minimal indices)** $\eta \ge 0$ 决定。

KCF是[矩阵束](@entry_id:751760)理论的顶峰，它完全刻画了任何一对矩阵在严格等价下的所有代数[不变量](@entry_id:148850)：有限谱结构、无穷谱结构以及由最小指标描述的奇异（[零空间](@entry_id:171336)）结构。

### 非厄米问题的对偶性与[双正交性](@entry_id:746831)

当矩阵 $A$ 和 $B$ 不是厄米矩阵时，左右[特征向量](@entry_id:151813)的行为表现出重要的差异。**左[广义特征向量](@entry_id:152349) (left generalized eigenvector)** 定义为一个非零的**行向量** $y^\ast$ 满足：

$y^\ast A = \lambda y^\ast B$

取共轭转置后，上式等价于 $A^\ast y = \overline{\lambda} B^\ast y$，其中 $y = (y^\ast)^\ast$ 是一个列向量。这表明左[特征值](@entry_id:154894) $\lambda$ 的左[特征向量](@entry_id:151813) $y$ 是伴随束 $A^\ast - \overline{\lambda} B^\ast$ 的右[特征向量](@entry_id:151813)。对于非厄米问题，给定[特征值](@entry_id:154894) $\lambda$ 的左[特征向量](@entry_id:151813) $y$ 和右[特征向量](@entry_id:151813) $x$ 通常是不同的 [@problem_id:3587865]。

尽管左右[特征向量](@entry_id:151813)不同，它们之间存在一种重要的**[双正交性](@entry_id:746831) (biorthogonality)** 关系。设 $(\lambda_i, x_j)$ 和 $(\lambda_i, y_i)$ 分别是右、左特征对。对于两个**不同**的[特征值](@entry_id:154894) $\lambda_i \neq \lambda_j$，我们有：

$y_i^\ast A x_j = \lambda_j y_i^\ast B x_j$  (通过 $y_i^\ast$ 左乘 $Ax_j = \lambda_j Bx_j$)
$y_i^\ast A x_j = \lambda_i y_i^\ast B x_j$  (通过 $x_j$ 右乘 $y_i^\ast A = \lambda_i y_i^\ast B$)

两式相减得到 $(\lambda_i - \lambda_j) y_i^\ast B x_j = 0$。由于 $\lambda_i \neq \lambda_j$，我们必然得到：

$y_i^\ast B x_j = 0$

进而也得到 $y_i^\ast A x_j = 0$。这是[广义特征值问题](@entry_id:151614)的一个基本性质 [@problem_id:3587865]。

如果一个正则束是**可对角化**的（即存在一组 $n$ 个线性无关的右[特征向量](@entry_id:151813)），那么也存在一组 $n$ 个线性无关的左[特征向量](@entry_id:151813)。我们可以将它们分别作为矩阵 $X$ 和 $Y$ 的列。通过适当的归一化，可以使它们满足双正交条件 $Y^\ast B X = I$（单位阵）。在这种情况下，我们有如下的对角化关系 [@problem_id:3587865]：

$A X = B X \Lambda$
$Y^\ast A = \Lambda Y^\ast B$

其中 $\Lambda$ 是由[特征值](@entry_id:154894)构成的[对角矩阵](@entry_id:637782)。这为非厄米问题提供了一个类似于标准[谱分解](@entry_id:173707)的框架。

### 数值考量与结构保持

理论上的[范式](@entry_id:161181)在数值计算中往往难以直接实现。实际算法关注的是在[有限精度算术](@entry_id:142321)下的稳定性和结构保持。

#### 变换与[不变量](@entry_id:148850)

[数值算法](@entry_id:752770)通常采用**酉严格等价 (unitary strict equivalence)** 变换，即 $(A,B) \mapsto (Q^\ast A Z, Q^\ast B Z)$，其中 $Q$ 和 $Z$ 是酉矩阵。这种变换具有优良的[数值稳定性](@entry_id:146550)。在这种变换下，许多关键性质是不变的，包括 [@problem_id:3587921]：
-   完整的广义[特征值](@entry_id:154894)谱（有限和无穷，包括[代数重数](@entry_id:154240)）。
-   Weierstrass和Kronecker[范式](@entry_id:161181)的结构（若尔当块和奇异块的大小与数量）。
-   如果 $B$ 可逆，则 $B^{-1}A$ 的谱。

值得注意的是，矩阵 $A$ 或 $B$ 单独的[特征值](@entry_id:154894)在这种变换下**不是**[不变量](@entry_id:148850)。

#### 厄米-定问题

一个特别重要且结构良好的子类是**厄米-定 (Hermitian-definite)** 问题，其中 $A$ 是[厄米矩阵](@entry_id:155147) ($A=A^\ast$)，$B$ 是厄米[正定矩阵](@entry_id:155546) ($B=B^\ast \succ 0$)。这类问题保证了所有[特征值](@entry_id:154894)都是实数，并且[特征向量](@entry_id:151813)可以选为关于 $B$ 正交的 ($x_i^\ast B x_j = \delta_{ij}$)。

一个常见的数值陷阱是显式计算 $B^{-1}$ 然后形成矩阵 $B^{-1}A$。即使在精确算术中，$B^{-1}A$ 通常也不是[厄米矩阵](@entry_id:155147)（除非 $A$ 和 $B$ 可交换）。在[浮点](@entry_id:749453)算术中，这个过程会放大[舍入误差](@entry_id:162651)并彻底破坏问题的对称性。

正确的**[保结构方法](@entry_id:755566)**是利用 $B$ 的正定性，计算其**[Cholesky分解](@entry_id:147066)** $B = LL^\ast$，其中 $L$ 是下[三角矩阵](@entry_id:636278)。原问题 $Ax = \lambda LL^\ast x$ 可以转化为一个等价的标准厄米[特征值问题](@entry_id:142153) [@problem_id:3587902]：

$L^{-1} A L^{-\ast} y = \lambda y, \quad \text{其中 } y = L^\ast x$

矩阵 $C = L^{-1} A L^{-\ast}$ 是厄米矩阵，可以应用高效稳定的厄ми[特征值算法](@entry_id:139409)求解。求得 $y$ 后，通过求解三角系统 $L^\ast x = y$ 即可得到原问题的[特征向量](@entry_id:151813) $x$。这个过程避免了求逆，并全程保持了问题的厄米结构。

#### [QZ算法](@entry_id:753987)的向后稳定性

对于一般的非厄米[广义特征值问题](@entry_id:151614)，**[QZ算法](@entry_id:753987)**是标准的数值方法。它通过一系列[酉变换](@entry_id:152599)，将矩阵对 $(A,B)$ 化为**广义舒尔形式 (generalized Schur form)**：

$Q^\ast A Z = S, \quad Q^\ast B Z = T$

其中 $Q, Z$ 是酉矩阵，$S, T$ 是上三角矩阵。变换后的[特征值](@entry_id:154894)可以通过 $S$ 和 $T$ 的对角元素之比 $s_{ii}/t_{ii}$ 简单得到。

[QZ算法](@entry_id:753987)是**向后稳定 (backward stable)** 的。这意味着在浮点算术中，虽然计算出的 $\widehat{S}, \widehat{T}$ 可能不是原始 $(A,B)$ 的精确舒尔形式，但它们是某个**邻近矩阵对** $(A+\Delta A, B+\Delta B)$ 的精确舒尔形式。这里的扰动 $\Delta A$ 和 $\Delta B$ 的范数很小，其大小与机器精度 $u$ 和原始矩阵的范数成正比 [@problem_id:3587918]。

这个性质至关重要：它保证了算法的输出（计算出的[特征值](@entry_id:154894)）是某个略微扰动问题的精确解 [@problem_id:3587918]。然而，必须明确，向后稳定性不等于高精度。如果原始问题本身是**病态的 (ill-conditioned)**（即[特征值](@entry_id:154894)对输入的微小扰动非常敏感），即使算法是向后稳定的，计算出的[特征值](@entry_id:154894)与真实[特征值](@entry_id:154894)之间也可能有很大差异。[前向误差](@entry_id:168661)（解的误差）约等于问题的[条件数](@entry_id:145150)乘以[后向误差](@entry_id:746645)（输入的等效扰动）。