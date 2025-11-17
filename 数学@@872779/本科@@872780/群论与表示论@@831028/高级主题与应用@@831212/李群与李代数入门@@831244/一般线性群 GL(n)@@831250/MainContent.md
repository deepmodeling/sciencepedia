## 引言
[一般线性群](@entry_id:141275)，记作 GL(n, F)，是现代数学中最为核心和普适的[代数结构](@entry_id:137052)之一。它不仅是群论中的一个基本范例，更是[连接线](@entry_id:196944)性代数、几何学、拓扑学乃至物理学的关键桥梁。这个群由所有可逆的线性变换构成，捕捉了[向量空间](@entry_id:151108)对称性的本质。然而，对于初学者而言，其丰富的内涵和跨学科的重要性往往难以一窥全貌。本文旨在系统性地揭开[一般线性群](@entry_id:141275)的神秘面纱，从基本定义到深刻应用，为读者构建一个完整而连贯的知识框架。

为了实现这一目标，本文将分为三个章节，层层递进地展开讨论。在“**原理与机制**”一章中，我们将奠定坚实的基础，从形式化定义出发，深入剖析其[代数结构](@entry_id:137052)、关键[子群](@entry_id:146164)以及作为[李群的拓扑](@entry_id:191016)特性。随后的“**应用与跨学科联系**”一章将视野拓宽，展示 GL(n, F) 如何作为[几何变换](@entry_id:150649)群、[拓扑空间](@entry_id:155056)以及表示论的原型，在不同数学分支中发挥其威力。最后，“**动手实践**”部分将通过一系列精心设计的问题，引导读者将理论知识应用于具体计算，从而深化理解并锻炼解决问题的能力。通过这一结构化的学习路径，我们将一同探索[一般线性群](@entry_id:141275)的内在之美及其在科学世界中的深远影响。

## 原理与机制

本章将深入探讨[一般线性群](@entry_id:141275) $GL(n, \mathbb{F})$ 的基本原理与内部机制。我们将从其定义和基础性质出发，逐步揭示其丰富的[代数结构](@entry_id:137052)、拓扑特性以及作为变换群的核心作用。通过对这些内容的系统性学习，读者将能够理解为什么[一般线性群](@entry_id:141275)是现代数学，特别是线性代数、群论和[李群](@entry_id:137659)理论中的核心研究对象之一。

### [一般线性群](@entry_id:141275)的基本定义与性质

#### 形式化定义

**[一般线性群](@entry_id:141275) (General Linear Group)**，记作 $GL(n, \mathbb{F})$，是定义在域 $\mathbb{F}$（例如实数域 $\mathbb{R}$ 或复数域 $\mathbb{C}$）上的一个群。其元素由所有 $n \times n$ 的**可逆矩阵**组成，其中矩阵的每个元素都来自域 $\mathbb{F}$。该群的群运算是标准的**[矩阵乘法](@entry_id:156035)**。

一个[代数结构](@entry_id:137052)要成为一个群，必须满足四个基本公理：
1.  **封闭性 (Closure)**：对任意两个矩阵 $A, B \in GL(n, \mathbb{F})$，它们的乘积 $AB$ 仍然是一个 $n \times n$ 矩阵。由于 $\det(AB) = \det(A)\det(B)$，且 $\det(A) \neq 0$ 和 $\det(B) \neq 0$，因此 $\det(AB) \neq 0$。这意味着 $AB$ 也是可逆的，所以 $AB \in GL(n, \mathbb{F})$。
2.  **[结合律](@entry_id:151180) (Associativity)**：[矩阵乘法](@entry_id:156035)满足结合律，即对任意 $A, B, C \in GL(n, \mathbb{F})$，有 $(AB)C = A(BC)$。
3.  **单位元 (Identity Element)**：$n \times n$ 的单位矩阵 $I$ 是 $GL(n, \mathbb{F})$ 的单位元，因为对任意 $A \in GL(n, \mathbb{F})$，都有 $AI = IA = A$。单位[矩阵的[行列](@entry_id:148198)式](@entry_id:142978)为 $1$，因此它自身也是可逆的。
4.  **[逆元](@entry_id:140790) (Inverse Element)**：根据定义，$GL(n, \mathbb{F})$ 中的每个矩阵 $A$ 都是可逆的。这意味着存在一个唯一的逆矩阵 $A^{-1}$，它也属于 $GL(n, \mathbb{F})$（因为 $\det(A^{-1}) = 1/\det(A) \neq 0$），满足 $AA^{-1} = A^{-1}A = I$。

#### 可逆性条件：[行列式](@entry_id:142978)

[可逆性](@entry_id:143146)的核心在于[行列式](@entry_id:142978)。一个 $n \times n$ 矩阵是可逆的，当且仅当其[行列式](@entry_id:142978)不为零。这个条件不仅是理论上的，也为我们提供了计算逆矩阵的具体方法。

以 $GL(2, \mathbb{R})$ 为例，考虑一个通用元素 $A = \begin{pmatrix} a  b \\ c  d \end{pmatrix}$，其中 $a, b, c, d \in \mathbb{R}$。其可逆的条件是 $\det(A) = ad - bc \neq 0$。我们可以通过求解方程 $A A^{-1} = I$ 来找到其逆矩阵 $A^{-1}$。设 $A^{-1} = \begin{pmatrix} x  y \\ z  w \end{pmatrix}$，则：
$$
\begin{pmatrix} a  b \\ c  d \end{pmatrix} \begin{pmatrix} x  y \\ z  w \end{pmatrix} = \begin{pmatrix} ax+bz  ay+bw \\ cx+dz  cy+dw \end{pmatrix} = \begin{pmatrix} 1  0 \\ 0  1 \end{pmatrix}
$$
这导向两个独立的[线性方程组](@entry_id:148943)。求解这些[方程组](@entry_id:193238)可得 $x, y, z, w$ 的表达式，最终得到一个广为人知的公式 [@problem_id:1649053]：
$$
A^{-1} = \frac{1}{ad-bc} \begin{pmatrix} d  -b \\ -c  a \end{pmatrix}
$$
这个公式清晰地展示了逆矩阵的存在性与非零[行列式](@entry_id:142978)之间的直接联系。

#### 最简单的情形：$GL(1, \mathbb{F})$

当维数 $n=1$ 时，[一般线性群](@entry_id:141275)的结构变得异常简单。$GL(1, \mathbb{F})$ 由所有 $1 \times 1$ 的[可逆矩阵](@entry_id:171829)组成。一个 $1 \times 1$ 矩阵形如 $[a]$，其中 $a \in \mathbb{F}$。其可逆性条件是 $\det([a]) = a \neq 0$。因此，$GL(1, \mathbb{F})$ 的元素集合等价于域 $\mathbb{F}$ 中所有非零元素的集合，记作 $\mathbb{F}^*$。

[矩阵乘法](@entry_id:156035) $[a][b] = [ab]$ 直接对应于域中元素的乘法。这表明存在一个从 $GL(1, \mathbb{F})$ 到 $\mathbb{F}^*$ 的自然映射 $\phi([a]) = a$。这个映射不仅是[一一对应](@entry_id:143935)的，而且保持了运算结构，即 $\phi([a][b]) = \phi([ab]) = ab = \phi([a])\phi([b])$。因此，$\phi$ 是一个[群同构](@entry_id:147371)。我们可以说 $GL(1, \mathbb{F})$ **同构 (isomorphic)** 于域 $\mathbb{F}$ 的乘法群 $\mathbb{F}^*$ [@problem_id:1649066]。例如，在 $GL(1, \mathbb{R})$ 中计算 $[\pi]^3 [e]^{-2}$，就相当于在 $\mathbb{R}^*$ 中计算 $\pi^3 e^{-2}$。

#### 交换性：一个[非阿贝尔群](@entry_id:141904)

尽管 $GL(1, \mathbb{F})$ 是交换的（因为它同构于域的[乘法群](@entry_id:155975)），但当维数 $n \ge 2$ 时，情况发生了根本性的变化。矩阵乘法通常是**[非交换](@entry_id:136599)的 (non-commutative)**，这意味着 $GL(n, \mathbb{F})$ 对于 $n \ge 2$ 是一个**[非阿贝尔群](@entry_id:141904) (non-abelian group)**。

要证明一个群是非阿贝尔的，我们只需找到一对元素 $A, B$，使得 $AB \neq BA$。考虑 $GL(2, \mathbb{R})$ 中的两个矩阵 [@problem_id:1649057]：
$$
A = \begin{pmatrix} 1  1 \\ 2  3 \end{pmatrix} \quad \text{和} \quad B = \begin{pmatrix} 1  0 \\ 1  1 \end{pmatrix}
$$
首先验证它们都属于 $GL(2, \mathbb{R})$：$\det(A) = 1 \cdot 3 - 1 \cdot 2 = 1 \neq 0$ 且 $\det(B) = 1 \cdot 1 - 0 \cdot 1 = 1 \neq 0$。现在我们计算它们的乘积：
$$
AB = \begin{pmatrix} 1  1 \\ 2  3 \end{pmatrix} \begin{pmatrix} 1  0 \\ 1  1 \end{pmatrix} = \begin{pmatrix} 1\cdot1+1\cdot1  1\cdot0+1\cdot1 \\ 2\cdot1+3\cdot1  2\cdot0+3\cdot1 \end{pmatrix} = \begin{pmatrix} 2  1 \\ 5  3 \end{pmatrix}
$$
$$
BA = \begin{pmatrix} 1  0 \\ 1  1 \end{pmatrix} \begin{pmatrix} 1  1 \\ 2  3 \end{pmatrix} = \begin{pmatrix} 1\cdot1+0\cdot2  1\cdot1+0\cdot3 \\ 1\cdot1+1\cdot2  1\cdot1+1\cdot3 \end{pmatrix} = \begin{pmatrix} 1  1 \\ 3  4 \end{pmatrix}
$$
显然，$AB \neq BA$。这一个反例就足以证明 $GL(2, \mathbb{R})$ 是非阿贝尔的。事实上，几乎任意随机选取的两个矩阵都是不可交换的，这反映了[线性变换](@entry_id:149133)复合的顺序依赖性。

### 关键[子群](@entry_id:146164)与[群结构](@entry_id:146855)

通过研究群的[子群](@entry_id:146164)，我们可以更深入地理解其结构。

#### [行列式同态](@entry_id:144744)与[特殊线性群](@entry_id:139538)

[行列式](@entry_id:142978)本身不仅仅是一个判断[可逆性](@entry_id:143146)的工具，它还定义了一个非常重要的**[群同态](@entry_id:140603) (group homomorphism)**。考虑映射 $\det: GL(n, \mathbb{F}) \to \mathbb{F}^*$，它将每个矩阵映射到其[行列式](@entry_id:142978)。由于 $\det(AB) = \det(A)\det(B)$，这个映射保持了群的乘法结构。

在群论中，同态的**核 (kernel)** 是一个极其重要的概念，它由所有被映射到目标群单位元的[元素组成](@entry_id:161166)。对于[行列式同态](@entry_id:144744)，目标群是 $\mathbb{F}^*$，其单位元是 $1$。因此，该[同态的核](@entry_id:145895)是 $GL(n, \mathbb{F})$ 中所有[行列式](@entry_id:142978)为 $1$ 的矩阵的集合 [@problem_id:1649033]。

这个核被称为**[特殊线性群](@entry_id:139538) (Special Linear Group)**，记作 $SL(n, \mathbb{F})$：
$$
SL(n, \mathbb{F}) = \{ A \in GL(n, \mathbb{F}) \mid \det(A) = 1 \}
$$
根据同态基本定理，任何[同态的核](@entry_id:145895)都是原群的一个**正规子群 (normal subgroup)**。因此，$SL(n, \mathbb{F})$ 是 $GL(n, \mathbb{F})$ 的一个[正规子群](@entry_id:147397)。从几何上看，$SL(n, \mathbb{F})$ 的元素对应于保持体积（或在 $\mathbb{R}^n$ 中保持定向和体积）的[线性变换](@entry_id:149133)。

#### [群的中心](@entry_id:141952)：标量矩阵

群的**中心 (center)**，记作 $Z(G)$，由群中所有能与任何其他元素交换的[元素组成](@entry_id:161166)。对于 $G = GL(n, \mathbb{F})$，其中心为：
$$
Z(GL(n, \mathbb{F})) = \{ A \in GL(n, \mathbb{F}) \mid AX = XA \text{ 对所有 } X \in GL(n, \mathbb{F}) \}
$$
直观上，什么样的线性变换能与所有其他线性变换交换顺序呢？答案是那些在所有方向上进行统一缩放的变换，即**标量矩阵 (scalar matrices)**，形如 $cI$，其中 $c \in \mathbb{F}^*$ 且 $I$ 是单位矩阵。

我们可以严格证明这一点。假设 $A \in Z(GL(n, \mathbb{F}))$。为了确定 $A$ 的结构，我们可以测试它与一些特殊[矩阵的交换性](@entry_id:263178)。对于任意 $k \neq l$，考虑矩阵 $B_{kl} = I + e_{kl}$，其中 $e_{kl}$ 是在 $(k, l)$ 位置为 $1$、其他位置为 $0$ 的矩阵单元。由于 $\det(B_{kl}) = 1$（因为它是一个三角矩阵，对角线元素全为1），所以 $B_{kl} \in GL(n, \mathbb{F})$。

由 $A$ 在中心，我们必须有 $A B_{kl} = B_{kl} A$，展开得到 $A(I + e_{kl}) = (I + e_{kl})A$，化简为 $A e_{kl} = e_{kl} A$。通过比较 $(A e_{kl})_{ij}$ 和 $(e_{kl} A)_{ij}$ 这两个矩阵在任意位置 $(i, j)$ 的元素，可以推导出对 $A=(a_{ij})$ 的约束条件 [@problem_id:1649045]。
$$
(A e_{kl})_{ij} = a_{ik} \delta_{lj} \quad \text{和} \quad (e_{kl} A)_{ij} = \delta_{ik} a_{lj}
$$
其中 $\delta$ 是克罗内克符号。令它们相等，$a_{ik} \delta_{lj} = \delta_{ik} a_{lj}$。
- 取 $j=l$ 且 $i \neq k$，我们得到 $a_{ik} = 0$。这意味着 $A$ 的所有非对角[线元](@entry_id:196833)素必须为零，即 $A$ 是一个对角矩阵。
- 取 $j=l$ 且 $i=k$，我们得到 $a_{kk} = a_{ll}$。这表明 $A$ 的所有对角[线元](@entry_id:196833)素必须相等。

综上所述，$A$ 必须是形如 $cI$ 的标量矩阵。由于 $A$ 必须是可逆的，所以 $c \neq 0$。因此，$Z(GL(n, \mathbb{F})) = \{ cI \mid c \in \mathbb{F}^* \}$。

#### GL(n, F) 的生成元：[初等矩阵](@entry_id:635817)

一个群可以由其一个[子集](@entry_id:261956)**生成 (generate)**，如果群中的每个元素都可以表示为该[子集](@entry_id:261956)中元素及其[逆元](@entry_id:140790)的有限乘积。对于 $GL(n, \mathbb{F})$，一个重要的结论是它由**[初等矩阵](@entry_id:635817) (elementary matrices)** 生成。[初等矩阵](@entry_id:635817)对应于三种基本的行变换：
1.  **行交换**：交换两行。
2.  **行[数乘](@entry_id:155971)**：将某一行乘以一个非零标量 $k$。
3.  **行加法**：将一行的 $c$ 倍加到另一行。

任何[可逆矩阵](@entry_id:171829)都可以通过一系列初等行变换化为[单位矩阵](@entry_id:156724)。这意味着 $A = E_k \dots E_2 E_1 I$，其中 $E_i$ 是[初等矩阵](@entry_id:635817)。因此，任何[可逆矩阵](@entry_id:171829) $A$ 都可以表示为[初等矩阵的乘积](@entry_id:155132)。

例如，考虑矩阵 $A = \begin{pmatrix} 2  3 \\ 5  8 \end{pmatrix} \in GL(2, \mathbb{R})$。我们可以通过一系列行变换将[单位矩阵](@entry_id:156724) $I$ 变为 $A$，从而找到一个[初等矩阵](@entry_id:635817)分解 [@problem_id:1649088]。这个过程的逆过程——高斯消元法——更为人熟知，它通过左乘[初等矩阵](@entry_id:635817)的逆将 $A$ 变为 $I$。这表明 $A$ 本身就是这些[初等矩阵的乘积](@entry_id:155132)。这个事实揭示了 $GL(n, \mathbb{F})$ 的元素可以由一些最简单的、具有清晰几何意义的变换构建而成。

### 拓扑与几何结构

当域 $\mathbb{F}$ 是实数域 $\mathbb{R}$ 或[复数域](@entry_id:153768) $\mathbb{C}$ 时，$GL(n, \mathbb{F})$ 不仅是一个代数群，还是一个拓扑空间，其拓扑结构源于矩阵元素所在的 $\mathbb{R}^{n^2}$ 或 $\mathbb{C}^{n^2}$。事实上，它是一个**[李群](@entry_id:137659) (Lie Group)**，即一个光滑流形，其群运算是光滑的。

#### 连通性：GL(n, R) 的两个分支

在拓扑学中，**[路径连通性](@entry_id:142695) (path-connectedness)** 是一个重要的概念。一个空间是路径连通的，如果其中任意两点都可以用一条连续路径连接。

$GL(n, \mathbb{R})$ 并不是一个路径连通的空间。我们可以通过[行列式](@entry_id:142978)函数 $\det: GL(n, \mathbb{R}) \to \mathbb{R}^*$ 来证明这一点。[行列式](@entry_id:142978)是[矩阵元](@entry_id:186505)素的[连续函数](@entry_id:137361)。$\mathbb{R}^* = (-\infty, 0) \cup (0, \infty)$ 本身是不连通的。

考虑两个矩阵，[单位矩阵](@entry_id:156724) $A=I$ 和一个反射矩阵 $B = \begin{pmatrix} -1  0 \\ 0  1 \end{pmatrix}$（对于 $n=2$ 的情况）。我们有 $\det(A) = 1 > 0$ 和 $\det(B) = -1  0$。假设存在一条从 $A$ 到 $B$ 的[连续路径](@entry_id:187361) $P(t)$，其中 $t \in [0, 1]$，$P(0) = A$, $P(1) = B$，并且对于所有 $t$，$P(t) \in GL(2, \mathbb{R})$。

那么，函数 $f(t) = \det(P(t))$ 是一个从 $[0, 1]$ 到 $\mathbb{R}^*$ 的[连续函数](@entry_id:137361)。我们有 $f(0) = 1$ 和 $f(1) = -1$。根据**[介值定理](@entry_id:145239) (Intermediate Value Theorem)**，必然存在某个 $t^* \in (0, 1)$ 使得 $f(t^*) = 0$。这意味着 $\det(P(t^*))=0$，即 $P(t^*)$ 是一个奇异矩阵，不属于 $GL(2, \mathbb{R})$。这与路径始终位于 $GL(2, \mathbb{R})$ 内的假设相矛盾 [@problem_id:1649040]。

这个论证表明，任何[行列式](@entry_id:142978)为正的矩阵与任何[行列式](@entry_id:142978)为负的矩阵之间都不存在连续路径。因此，$GL(n, \mathbb{R})$ 至少有两个[路径连通分支](@entry_id:275432)：
- $GL^+(n, \mathbb{R}) = \{ A \in GL(n, \mathbb{R}) \mid \det(A) > 0 \}$
- $GL^-(n, \mathbb{R}) = \{ A \in GL(n, \mathbb{R}) \mid \det(A)  0 \}$

#### GL+(n, R) 的结构

包含单位矩阵的 $GL^+(n, \mathbb{R})$ 本身是[路径连通](@entry_id:148704)的。这意味着任何两个[行列式](@entry_id:142978)为正的矩阵都可以通过一条[连续路径](@entry_id:187361)相连。要证明这一点，只需证明任何 $A \in GL^+(n, \mathbb{R})$ 都与单位矩阵 $I$ [路径连通](@entry_id:148704)。

一个标准的构造方法分两步 [@problem_id:1649037]：
1.  **QR分解**：任何 $A \in GL^+(n, \mathbb{R})$ 都有唯一的分解 $A=QR$，其中 $Q \in SO(n, \mathbb{R})$ 是一个**特殊[正交矩阵](@entry_id:169220)**（即 $Q^T Q = I$ 且 $\det(Q)=1$），$R$ 是一个对角[线元](@entry_id:196833)素均为正的[上三角矩阵](@entry_id:150931)。我们可以构造一条路径 $P_R(t) = Q((1-t)R + tI)$，当 $t$ 从 $0$ 变到 $1$ 时，它将 $A=QR$ 连续地变为 $Q$。由于 $R$ 的对角[线元](@entry_id:196833)素为正，凸组合 $(1-t)R + tI$ 的对角线元素也始终为正，因此其[行列式](@entry_id:142978)为正，路径上的所有矩阵都属于 $GL^+(n, \mathbb{R})$。
2.  **矩阵指数**：任何特殊[正交矩阵](@entry_id:169220) $Q \in SO(n, \mathbb{R})$ 都可以表示为 $Q = \exp(S)$，其中 $S$ 是一个[斜对称矩阵](@entry_id:155998)（$S^T = -S$）。我们可以构造路径 $P_S(t) = \exp((1-t)S)$，当 $t$ 从 $0$ 变到 $1$ 时，它将 $Q = \exp(S)$ 连续地变为 $I = \exp(0)$。

通过拼接这两条路径，我们证明了任何 $A \in GL^+(n, \mathbb{R})$ 都与 $I$ [路径连通](@entry_id:148704)。

#### 全局拓扑：极分解

**极分解 (polar decomposition)** 提供了另一种理解 $GL(n, \mathbb{R})$ 几何结构的强大工具。该定理指出，任何[可逆矩阵](@entry_id:171829) $A \in GL(n, \mathbb{R})$ 都可以唯一地分解为 $A=RS$，其中 $R$ 是一个**[正交矩阵](@entry_id:169220)**（$R \in O(n)$, $R^T R = I$），$S$ 是一个**[对称正定矩阵](@entry_id:136714)**（$S^T = S$，且所有[特征值](@entry_id:154894)为正）。

这个分解在几何上非常直观：任何[可逆线性变换](@entry_id:149915)都可以看作是一个旋转/反射（由 $R$ 代表）和一个在相互正交方向上的拉伸/压缩（由 $S$ 代表）的复合。

从拓扑上看，这个分解意味着 $GL(n, \mathbb{R})$ 作为[流形](@entry_id:153038)是**[微分同胚](@entry_id:147249) (diffeomorphic)** 于[笛卡尔积](@entry_id:154642)空间 $O(n) \times \mathcal{P}_n$ 的，其中 $\mathcal{P}_n$ 是所有 $n \times n$ [对称正定矩阵](@entry_id:136714)的空间。

[正交群](@entry_id:152531) $O(n)$ 本身有两个连通分支（$\det = 1$ 的 $SO(n)$ 和 $\det = -1$ 的部分），这与 $GL(n, \mathbb{R})$ 的两个分支相对应。而 $\mathcal{P}_n$ 空间是路径连通的，并且可以证明它[微分同胚](@entry_id:147249)于一个[欧几里得空间](@entry_id:138052) $\mathbb{R}^k$。$k$ 的维数等于独立[对称矩阵](@entry_id:143130)的元素个数 [@problem_id:1649046]，即：
$$
k = n + \binom{n}{2} = \frac{n(n+1)}{2}
$$
因此，从拓扑角度看，$GL(n, \mathbb{R})$ 的结构可以被理解为[正交群](@entry_id:152531) $O(n)$ 与一个[欧几里得空间](@entry_id:138052)的乘积。

### GL(n, F) 的作用：[表示论](@entry_id:137998)简介

群论的一个核心应用是研究群如何作用于其他数学对象，这构成了**[表示论](@entry_id:137998) (Representation Theory)** 的基础。

#### 定义表示

$GL(n, \mathbb{F})$ 最自然的作用是它对[向量空间](@entry_id:151108) $\mathbb{F}^n$ 的线性作用。对于任何矩阵 $g \in GL(n, \mathbb{F})$ 和向量 $v \in \mathbb{F}^n$，作用定义为矩阵-向量乘法 $v \mapsto gv$。这个作用被称为 $GL(n, \mathbb{F})$ 的**定义表示 (defining representation)** 或**标准表示 (standard representation)**。

#### 伴随表示

除了作用于向量，$GL(n, \mathbb{F})$ 还可以作用于其他空间，例如它自身所在的[矩阵空间](@entry_id:261335) $M_n(\mathbb{F})$。一个非常重要的作用是通过**共轭 (conjugation)** 定义的：
$$
A \mapsto gAg^{-1} \quad \text{对于 } g \in GL(n, \mathbb{F}), A \in M_n(\mathbb{F})
$$
这个作用被称为**伴随表示 (adjoint representation)**。从线性变换的角度看，这对应于基底变换对一个线性算子（由矩阵 $A$ 表示）的影响。

#### 伴随[表示的分解](@entry_id:147581)

在伴随表示下，整个[矩阵空间](@entry_id:261335) $M_n(\mathbb{C})$（以复数域为例）可以被分解为两个在[群作用](@entry_id:268812)下不变的[子空间](@entry_id:150286)，即**不变子空间 (invariant subspaces)**。

1.  **标量矩阵[子空间](@entry_id:150286)**：考虑形如 $\lambda I$ 的标量矩阵。对于任何 $g \in GL(n, \mathbb{C})$，我们有 $g(\lambda I)g^{-1} = \lambda (gIg^{-1}) = \lambda I$。这意味着标量矩阵在[共轭作用](@entry_id:143328)下保持不变。这个一维[子空间](@entry_id:150286) $\mathbb{C}I$ 是一个不变子空间。在这个[子空间](@entry_id:150286)上，群的作用是平凡的。

2.  **无迹矩阵[子空间](@entry_id:150286)**：考虑迹为零的矩阵构成的空间，即 $sl(n, \mathbb{C}) = \{ A \in M_n(\mathbb{C}) \mid \operatorname{tr}(A)=0 \}$。利用[迹的循环性质](@entry_id:153103) $\operatorname{tr}(XYZ) = \operatorname{tr}(ZXY)$，我们有 $\operatorname{tr}(gAg^{-1}) = \operatorname{tr}((gA)g^{-1}) = \operatorname{tr}(g^{-1}gA) = \operatorname{tr}(A)$。这意味着如果一个矩阵的迹为零，那么它在[共轭作用](@entry_id:143328)下的像的迹也为零。因此，$sl(n, \mathbb{C})$ 也是一个[不变子空间](@entry_id:152829)。

整个[矩阵空间](@entry_id:261335)可以分解为这两个[子空间](@entry_id:150286)的直和：
$$
M_n(\mathbb{C}) = \mathbb{C}I \oplus sl(n, \mathbb{C})
$$
因为 $M_n(\mathbb{C})$ 的维数是 $n^2$，而 $\mathbb{C}I$ 的维数是 $1$，所以无迹矩阵[子空间](@entry_id:150286) $sl(n, \mathbb{C})$ 的维数是 $n^2 - 1$ [@problem_id:1649079]。例如，当 $n=3$ 时，该[子空间](@entry_id:150286)的维数是 $3^2 - 1 = 8$。这个分解在[李代数](@entry_id:137954)理论中至关重要，$sl(n, \mathbb{C})$ 正是李群 $SL(n, \mathbb{C})$ 对应的[李代数](@entry_id:137954)。