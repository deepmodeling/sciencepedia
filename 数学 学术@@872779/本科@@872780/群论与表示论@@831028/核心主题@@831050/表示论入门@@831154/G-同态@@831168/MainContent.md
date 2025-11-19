## 引言
在[群表示论](@entry_id:141930)中，理解单个表示的结构固然重要，但探究不同表示之间的内在联系同样关键。[G-同态](@entry_id:143972)（G-homomorphisms），亦称缠结映射（intertwining maps），正是扮演这一角色的核心工具。它们是保持[群对称性](@entry_id:147821)结构的[线性映射](@entry_id:185132)，其地位堪比群论中的[群同态](@entry_id:140603)或线性代数中的[线性变换](@entry_id:149133)。本文旨在系统性地揭示[G-同态](@entry_id:143972)的本质，解决如何比较和关联不同表示这一基本问题。

通过本文的学习，你将全面掌握[G-同态](@entry_id:143972)的理论与实践。在“原理与机制”一章中，我们将从基本定义和矩阵形式入手，深入探讨其核心性质，并引出表示论的基石——[舒尔引理](@entry_id:136779)。接着，在“应用与跨学科联系”一章，我们将展示[G-同态](@entry_id:143972)如何作为一种通用语言，将表示论与量子力学、微分几何及同调代数等多个领域联系起来。最后，在“动手实践”部分，你将有机会通过具体问题来巩固和应用所学知识，将理论真正内化为解决问题的能力。

## 原理与机制

在研究[群表示](@entry_id:156757)时，我们不仅对单个表示的结构感兴趣，也对不同表示之间的关系感兴趣。连接不同表示的桥梁是那些保持群作用结构的[线性映射](@entry_id:185132)。这些特殊映射被称为 $G$-同态（$G$-homomorphisms）或缠结映射（intertwining maps），它们在表示论中扮演着核心角色，类似于群论中的[群同态](@entry_id:140603)或线性代数中的[线性变换](@entry_id:149133)。本章将系统地阐述 $G$-同态的定义、基本性质及其在[表示分解](@entry_id:139061)和[结构分析](@entry_id:153861)中的深刻应用。

### $G$-同态的定义与矩阵形式

让我们从形式化定义开始。设 $G$ 是一个群，$(\rho, V)$ 和 $(\sigma, W)$ 是 $G$ 在域 $F$ 上的两个[线性表示](@entry_id:139970)。一个从 $V$ 到 $W$ 的[线性映射](@entry_id:185132) $\phi: V \to W$ 如果对于所有 $g \in G$ 和 $v \in V$ 都满足以下条件，则称之为一个 **$G$-同态**：

$$
\phi(\rho(g)v) = \sigma(g)\phi(v)
$$

这个条件通常被称为 **缠结关系（intertwining relation）**。从直观上看，这意味着映射 $\phi$ 与群 $G$ 的作用是“可交换的”。无论我们是先对向量 $v$ 应用[群作用](@entry_id:268812) $\rho(g)$ 再通过 $\phi$ 映射，还是先将 $v$ 映射为 $\phi(v)$ 再应用群作用 $\sigma(g)$，结果都是相同的。

在处理有限维表示时，我们通常选择一组基，并将线性变换和群作用表示为矩阵。这一视角为理解和计算 $G$-同态提供了具体工具。假设 $V$ 和 $W$ 分别是 $n$ 维和 $m$ 维的，并且我们已经为它们选择了基。设线性映射 $\phi$ 对应的矩阵为 $M$（一个 $m \times n$ 矩阵），群元素 $g$ 在表示 $\rho$ 和 $\sigma$ 下的矩阵分别为 $D_V(g)$ 和 $D_W(g)$。那么，向量 $v$ 及其像 $\phi(v)$ 分别由列向量 $\mathbf{v}$ 和 $M\mathbf{v}$ 表示。[群作用](@entry_id:268812)则通过矩阵乘法实现：$\rho(g)v$ 对应 $D_V(g)\mathbf{v}$，$\sigma(g)\phi(v)$ 对应 $D_W(g)(M\mathbf{v})$。

将这些代入 $G$-同态的定义式，$\phi(\rho(g)v) = \sigma(g)\phi(v)$ 就转化为一个[矩阵方程](@entry_id:203695)：

$$
M(D_V(g)\mathbf{v}) = (D_W(g)M)\mathbf{v}
$$

由于这个等式对所有向量 $\mathbf{v}$ 都成立，我们得到矩阵的 **缠结关系**：

$$
M D_V(g) = D_W(g) M \quad \text{for all } g \in G
$$

这个方程是寻找 $G$-同态的[矩阵表示](@entry_id:146025)的出发点。我们只需要对群 $G$ 的所有生成元验证这个关系即可，因为如果它对生成元成立，它将自动对其乘积和[逆元](@entry_id:140790)成立，从而对整个群成立。

**示例：寻找 $D_3$ 表示间的缠结映射** [@problem_id:1620555]

考虑代表等边三角形对称性的六阶二面体群 $G = D_3$，它由旋转 $r$（逆时针旋转 $120^\circ$）和反射 $s$ 生成。设有两个在 $V = \mathbb{R}^2$ 上的二维表示 $(\rho_1, V)$ 和 $(\rho_2, V)$。在标准基下，它们由生成元的矩阵给出：
对于 $\rho_1$：
$D_1(r) = \begin{pmatrix} -1/2 & -\sqrt{3}/2 \\ \sqrt{3}/2 & -1/2 \end{pmatrix}$, $D_1(s) = \begin{pmatrix} 1 & 0 \\ 0 & -1 \end{pmatrix}$
对于 $\rho_2$：
$D_2(r) = \begin{pmatrix} -1/2 & -\sqrt{3}/2 \\ \sqrt{3}/2 & -1/2 \end{pmatrix}$, $D_2(s) = \begin{pmatrix} 0 & -1 \\ -1 & 0 \end{pmatrix}$

我们希望找到一个非零的 $G$-同态 $T: V \to V$。设其矩阵为 $M = \begin{pmatrix} a & b \\ c & d \end{pmatrix}$。根据缠结关系，我们必须满足 $M D_1(g) = D_2(g) M$ 对 $g=r$ 和 $g=s$ 都成立。

首先，对于 $g=r$，由于 $D_1(r) = D_2(r) = R$，条件变为 $MR=RM$，即 $M$ 必须与旋转矩阵 $R$ 可交换。通过计算矩阵乘积 $MR$ 和 $RM$ 并逐项比较，我们得到[方程组](@entry_id:193238)，其解为 $d=a$ 和 $c=-b$。因此，$M$ 必须具有形式 $\begin{pmatrix} a & b \\ -b & a \end{pmatrix}$。

接下来，对于 $g=s$，条件是 $M D_1(s) = D_2(s) M$。代入 $D_1(s)$ 和 $D_2(s)$ 的矩阵以及 $M$ 的形式，我们有：
$$
\begin{pmatrix} a & b \\ -b & a \end{pmatrix} \begin{pmatrix} 1 & 0 \\ 0 & -1 \end{pmatrix} = \begin{pmatrix} 0 & -1 \\ -1 & 0 \end{pmatrix} \begin{pmatrix} a & b \\ -b & a \end{pmatrix}
$$
计算得到：
$$
\begin{pmatrix} a & -b \\ -b & -a \end{pmatrix} = \begin{pmatrix} b & -a \\ -a & -b \end{pmatrix}
$$
比较[矩阵元](@entry_id:186505)素，我们得到 $a=b$。因此，$M$ 必须具有形式 $\begin{pmatrix} a & a \\ -a & a \end{pmatrix} = a \begin{pmatrix} 1 & 1 \\ -1 & 1 \end{pmatrix}$。这是一个一维的[解空间](@entry_id:200470)，意味着所有从 $\rho_1$ 到 $\rho_2$ 的 $G$-同态都是这个矩阵的标量倍。如果额外给定条件，如迹 $\text{tr}(M) = 2a = 2$，我们就能唯一确定 $a=1$，从而得到 $M = \begin{pmatrix} 1 & 1 \\ -1 & 1 \end{pmatrix}$。

### $G$-同态的空间：$\text{Hom}_G(V, W)$

$G$-同态不仅是孤立的映射，它们共同构成一个具有丰富结构的数学对象。给定两个 $G$-表示 $V$ 和 $W$，所有从 $V$ 到 $W$ 的 $G$-同态的集合记作 $\text{Hom}_G(V, W)$。这个集合不仅仅是一个集合，它还是一个**[向量空间](@entry_id:151108)**。

要证明这一点，我们只需验证它对线性组合是封闭的。设 $\phi_1, \phi_2 \in \text{Hom}_G(V, W)$，并设 $c_1, c_2$ 是域 $F$ 中的标量。我们需要证明线性组合 $\phi = c_1\phi_1 + c_2\phi_2$ 也是一个 $G$-同态。对于任意 $g \in G$ 和 $v \in V$：
$$
\begin{align*}
\phi(g \cdot v) & = (c_1\phi_1 + c_2\phi_2)(g \cdot v) \\
 &= c_1\phi_1(g \cdot v) + c_2\phi_2(g \cdot v) \quad \text{(线性映射的定义)} \\
 &= c_1(g \cdot \phi_1(v)) + c_2(g \cdot \phi_2(v)) \quad \text{($\phi_1, \phi_2$ 是 G-同态)} \\
 &= g \cdot (c_1\phi_1(v) + c_2\phi_2(v)) \quad \text{(群作用是线性的)} \\
 &= g \cdot \phi(v)
\end{align*}
$$
这证明了 $\phi$ 确实是一个 $G$-同态。因此，$\text{Hom}_G(V, W)$ 是包含所有从 $V$ 到 $W$ 的[线性映射](@entry_id:185132)的空间 $\text{Hom}(V, W)$ 的一个子[向量空间](@entry_id:151108)。[@problem_id:1620578]

### 基本性质：核、像与同构

$G$-同态的两个最基本的构造——核（kernel）与像（image）——并非普通的[子空间](@entry_id:150286)，它们本身继承了[群作用](@entry_id:268812)的结构，成为[子表示](@entry_id:141094)。

#### 核是[子表示](@entry_id:141094)

设 $\phi: V \to W$ 是一个 $G$-同态。它的**核**定义为 $\ker(\phi) = \{v \in V \mid \phi(v) = 0\}$。我们来证明 $\ker(\phi)$ 是 $V$ 的一个 **$G$-[子表示](@entry_id:141094)**（或称为 $G$-[不变子空间](@entry_id:152829)）。为此，只需证明它在群作用下是封闭的。取任意 $v \in \ker(\phi)$ 和 $g \in G$，我们需要检验 $g \cdot v$ 是否仍在 $\ker(\phi)$ 中。利用 $\phi$ 的缠结性质：
$$
\phi(g \cdot v) = g \cdot \phi(v) = g \cdot 0 = 0
$$
因此，$g \cdot v \in \ker(\phi)$。这表明 $\ker(\phi)$ 确实是一个[子表示](@entry_id:141094)。[@problem_id:1656747]

例如，考虑 $S_3$ 在 $\mathbb{C}^3$ 上的[置换表示](@entry_id:142960) $V$，其作用是[置换](@entry_id:136432)标准基 $\{e_1, e_2, e_3\}$。同时考虑一维[平凡表示](@entry_id:141357) $W=\mathbb{C}$，其中每个群元素的作用都是恒等映射。定义一个[线性映射](@entry_id:185132) $\phi: V \to W$ 为 $\phi(c_1e_1 + c_2e_2 + c_3e_3) = c_1+c_2+c_3$。这个映射是一个 $G$-同态，因为坐标的求和对于坐标的任意[置换](@entry_id:136432)都是不变的。它的核是 $\ker(\phi) = \{ (c_1, c_2, c_3) \in \mathbb{C}^3 \mid c_1+c_2+c_3=0 \}$。这个[子空间](@entry_id:150286)正是 $S_3$ 的二维标准[不可约表示](@entry_id:263310)，它由像 $\{e_1-e_2, e_2-e_3\}$ 这样的向量张成。

#### 像是[子表示](@entry_id:141094)

同样地，$\phi$ 的**像** $\text{im}(\phi) = \{\phi(v) \mid v \in V\}$ 是 $W$ 的一个 $G$-[子表示](@entry_id:141094)。取任意 $w \in \text{im}(\phi)$，则存在 $v \in V$ 使得 $w = \phi(v)$。对于任意 $g \in G$，我们有：
$$
g \cdot w = g \cdot \phi(v) = \phi(g \cdot v)
$$
由于 $g \cdot v$ 仍然是 $V$ 中的一个向量，所以 $\phi(g \cdot v)$ 属于 $\text{im}(\phi)$。因此，$\text{im}(\phi)$ 在[群作用](@entry_id:268812)下是封闭的，构成 $W$ 的一个[子表示](@entry_id:141094)。[@problem_id:1620594]

#### G-同构

如果一个 $G$-同态 $\phi: V \to W$ 是一个双射（即[向量空间的同构](@entry_id:154761)），那么我们称之为一个 **$G$-同构**。在这种情况下，我们说表示 $V$ 和 $W$ 是**同构的**或**等价的**，记作 $V \cong W$。这意味着从[表示论](@entry_id:137998)的角度看，$V$ 和 $W$ 是无法区分的；它们具有完全相同的结构，只是可能在不同的[向量空间](@entry_id:151108)中实现。

一个重要的性质是，如果 $\phi: V \to W$ 是一个 $G$-同构，那么它的逆映射 $\phi^{-1}: W \to V$ 也自动成为一个 $G$-同构。[@problem_id:1620583] 证明如下：
我们从 $\phi$ 的缠结关系 $\phi(\rho(g)v) = \sigma(g)\phi(v)$ 出发。由于 $\phi$ 可逆，我们可以用 $\phi^{-1}$ 从左侧复合等式两边：
$$
\phi^{-1}(\phi(\rho(g)v)) = \phi^{-1}(\sigma(g)\phi(v)) \implies \rho(g)v = \phi^{-1}(\sigma(g)\phi(v))
$$
现在，令 $w = \phi(v)$，则 $v = \phi^{-1}(w)$。将此代入上式，我们得到对于任意 $w \in W$：
$$
\rho(g)\phi^{-1}(w) = \phi^{-1}(\sigma(g)w)
$$
这正是 $\phi^{-1}: W \to V$ 作为 $G$-同态的定义。由于 $\phi^{-1}$ 作为线性映射已经是双射，所以它是一个 $G$-同构。

### [舒尔引理](@entry_id:136779)：表示论的基石

$G$-同态最深刻和最有力的性质体现在处理**[不可约表示](@entry_id:263310)**时，这些性质被概括在**[舒尔引理](@entry_id:136779) (Schur's Lemma)** 中。不可约表示（irreducible representation, or irrep）是没有非平凡[子表示](@entry_id:141094)（即除了 $\{0\}$ 和自身之外没有其他[不变子空间](@entry_id:152829)）的表示。它们是表示论的“原子”。

[舒尔引理](@entry_id:136779)（在[代数闭域](@entry_id:151836)如 $\mathbb{C}$ 上）有两个关键部分：
1.  设 $V$ 和 $W$ 是 $G$ 的两个不可约表示。
    *   如果 $V$ 和 $W$ 不可同构 ($V \not\cong W$)，则它们之间唯一的 $G$-同态是零映射，即 $\text{Hom}_G(V, W) = \{0\}$。
    *   如果 $V$ 和 $W$ 同构 ($V \cong W$)，则 $\text{Hom}_G(V, W)$ 是一维的。这意味着任何两个非零的 $G$-同态都互为标量倍。

2.  设 $V$ 是 $G$ 在 $\mathbb{C}$ 上的一个有限维[不可约表示](@entry_id:263310)。那么，任何从 $V$ 到自身的 $G$-同态 $\phi: V \to V$ 必定是一个标量乘以恒等映射。即 $\phi = \lambda \cdot \text{id}_V$ 对于某个复数 $\lambda \in \mathbb{C}$。因此，$\text{Hom}_G(V, V) \cong \mathbb{C}$。

[舒尔引理](@entry_id:136779)的威力在于它极大地限制了不可约表示之间的可能映射。第二部分尤其强大：它意味着在不可约表示的世界里，唯一能与所有[群作用](@entry_id:268812)交换的[线性算子](@entry_id:149003)就是简单的缩放。

**示例：[一维表示](@entry_id:136509)上的同态** [@problem_id:1620575]
考虑[循环群](@entry_id:138668) $G = C_6$ 和它在一维[复向量空间](@entry_id:264355) $V = \mathbb{C}$ 上的一个表示，其中生成元 $g$ 的作用是乘以一个复数 $\omega = \exp(i\pi/3)$。因为 $V$ 是一维的，它必然是不可约的。根据[舒尔引理](@entry_id:136779)的第二部分，任何 $G$-同态 $\Phi: V \to V$ 都必须是乘以某个标量 $\lambda$。
现在，让我们构造一个算子 $\Phi = \rho(g) + \rho(g^2) + \rho(g^3)$。由于[群表示](@entry_id:156757) $\rho$ 是一个同态，$\rho(g^k)$ 就是 $\rho(g)$ 的 $k$ 次方。$\rho(g^k)$ 本身也是一个与群作用可交换的算子，因此是一个 $G$-同态。由于 $\text{Hom}_G(V,V)$ 是一个[向量空间](@entry_id:151108)，$\Phi$ 作为三个 $G$-同态的和，其本身也是一个 $G$-同态。因此，$\Phi$ 的作用必然是乘以一个标量 $\lambda$。这个标量就是定义中各个算子对应标量的和：
$$
\lambda = \omega + \omega^2 + \omega^3 = \exp(i\pi/3) + \exp(i2\pi/3) + \exp(i\pi)
$$
计算这些复数的值并求和，我们得到 $\lambda = (\frac{1}{2} + i\frac{\sqrt{3}}{2}) + (-\frac{1}{2} + i\frac{\sqrt{3}}{2}) + (-1) = -1 + i\sqrt{3}$。

### [舒尔引理](@entry_id:136779)的应用

[舒尔引理](@entry_id:136779)不仅是一个理论上的优美结果，它也是分析和分解表示的强大工具。

#### 计算[不可约表示的重数](@entry_id:141777)

对于[有限群](@entry_id:139710)，任何在[复数域](@entry_id:153768)上的有限维表示都是**完全可约的**（[马施克定理](@entry_id:142097)，Maschke's Theorem），这意味着它可以分解为[不可约表示](@entry_id:263310)的[直和](@entry_id:156782)。设 $V$ 是一个完全[可约表示](@entry_id:137110)，其分解形式为：
$$
V \cong \bigoplus_{i=1}^k m_i W_i
$$
其中 $\{W_i\}_{i=1}^k$是一组互不同构的不可约表示，$m_i \ge 0$ 是整数，称为 $W_i$ 在 $V$ 中的**重数（multiplicity）**。我们如何确定这些[重数](@entry_id:136466) $m_j$？[舒尔引理](@entry_id:136779)给出了一个优雅的答案。[@problem_id:1607734]

考虑空间 $\text{Hom}_G(W_j, V)$，其中 $W_j$ 是某个特定的[不可约表示](@entry_id:263310)。利用 $\text{Hom}$ 函子在第二个变量上保持[直和](@entry_id:156782)的性质，我们有：
$$
\text{Hom}_G(W_j, V) \cong \text{Hom}_G\left(W_j, \bigoplus_{i=1}^k m_i W_i\right) \cong \bigoplus_{i=1}^k \text{Hom}_G(W_j, m_i W_i) \cong \bigoplus_{i=1}^k m_i \text{Hom}_G(W_j, W_i)
$$
根据[舒尔引理](@entry_id:136779)，当 $i \neq j$ 时，$\text{Hom}_G(W_j, W_i) = \{0\}$；当 $i = j$ 时，$\text{Hom}_G(W_j, W_j) \cong \mathbb{C}$。因此，[直和](@entry_id:156782)中只有第 $j$ 项存活下来：
$$
\text{Hom}_G(W_j, V) \cong m_j \text{Hom}_G(W_j, W_j) \cong \mathbb{C}^{m_j}
$$
取两边的维数，我们得到一个计算重数的关键公式：
$$
m_j = \dim(\text{Hom}_G(W_j, V))
$$
类似地，可以证明 $m_j = \dim(\text{Hom}_G(V, W_j))$。这个结果意味着，一个[不可约表示](@entry_id:263310) $W_j$ 在 $V$ 中出现的次数，精确地等于从 $W_j$ 到 $V$（或从 $V$ 到 $W_j$）的[线性无关](@entry_id:148207)的 $G$-同态的数量。

#### 不变子空间

考虑最简单的非[平凡表示](@entry_id:141357)——一维[平凡表示](@entry_id:141357) $(\mathbb{C}, \tau)$，其中对所有 $g \in G$ 和 $z \in \mathbb{C}$，有 $g \cdot z = z$。从这个[平凡表示](@entry_id:141357)到任意表示 $V$ 的 $G$-同态空间是什么样的？[@problem_id:1620601]

设 $\phi: \mathbb{C} \to V$ 是一个 $G$-同态。由于 $\phi$ 是线性的，它完全由它在[基向量](@entry_id:199546) $1 \in \mathbb{C}$ 上的像 $v = \phi(1) \in V$ 决定。$G$-同态的条件 $\phi(g \cdot 1) = g \cdot \phi(1)$ 变为 $\phi(1) = g \cdot \phi(1)$，即 $v = g \cdot v$。这个条件对所有 $g \in G$ 都成立，这意味着 $v$ 是一个 **$G$-不变向量**。所有 $G$-不变向量构成了 $V$ 的一个[子空间](@entry_id:150286)，称为**不变子空间**，记作 $V^G$。

反之，任何一个不变向量 $v \in V^G$ 都可以定义一个 $G$-同态 $\phi_v: \mathbb{C} \to V$，其定义为 $\phi_v(z) = z \cdot v$。因此，我们建立了一个[一一对应](@entry_id:143935)关系，它实际上是一个[向量空间同构](@entry_id:196183)：
$$
\text{Hom}_G(\mathbb{C}, V) \cong V^G
$$
这提供了一个深刻的联系：从[平凡表示](@entry_id:141357)出发的同态，其本质就是寻找目标表示中的不变元素。

#### [投影算子](@entry_id:154142)与[表示分解](@entry_id:139061)

如果一个 $G$-同态 $\phi: V \to V$ 还是一个**投影算子**（即满足 $\phi^2 = \phi$），那么它就能将表示 $V$ 分解为两个子[表示的[直](@entry_id:138310)和](@entry_id:156782)。[@problem_id:1620621]

任何[投影算子](@entry_id:154142)都能将[向量空间分解](@entry_id:194743)为 $V = \text{im}(\phi) \oplus \ker(\phi)$。我们已经知道，因为 $\phi$ 是 $G$-同态，所以 $\text{im}(\phi)$ 和 $\ker(\phi)$ 都是 $G$-[不变子空间](@entry_id:152829)，即它们本身就是[子表示](@entry_id:141094)。因此，这个分解不仅仅是[向量空间](@entry_id:151108)的直和，更是 **$G$-[表示的直和](@entry_id:138310)**。这意味着 $V$ 的任何元素都可以唯一地写成一个来自 $\text{im}(\phi)$ 的向量和一个来自 $\ker(\phi)$ 的向量之和，并且群 $G$ 的作用分别在这两个分量上独立进行。

这个性质是[完全可约性](@entry_id:144429)理论的基石。[马施克定理](@entry_id:142097)的证明本质上就是构造一个这样的 $G$-不变投影算子。给定 $V$ 的任意一个[子表示](@entry_id:141094) $W$，我们可以找到一个普通的线性投影 $\pi: V \to W$。这个 $\pi$ 可能不是 $G$-同态。但是，通过在群上对 $\pi$进行“平均化”，可以构造一个新的映射 $\phi(v) = \frac{1}{|G|} \sum_{g \in G} g \cdot \pi(g^{-1} \cdot v)$，这个 $\phi$ 就是一个满足条件的 $G$-不变投影，从而证明了 $V$ 可以分解。

### 进阶主题：[张量积](@entry_id:140694)与同态空间

$G$-同态的概念可以推广到更复杂的构造中，例如张量积。给定两个 $G$-表示 $U$ 和 $V$，它们的[张量积](@entry_id:140694) $U \otimes V$ 也是一个 $G$-表示，[群作用](@entry_id:268812)定义为 $g \cdot (u \otimes v) = (g \cdot u) \otimes (g \cdot v)$。

在线性代数中，有一个重要的自然同构，称为[张量-同态伴随](@entry_id:154749)（tensor-hom adjunction）：
$$
\text{Hom}(U \otimes V, W) \cong \text{Hom}(U, \text{Hom}(V, W))
$$
其中 $\text{Hom}(V, W)$ 是从 $V$ 到 $W$ 的所有[线性映射](@entry_id:185132)构成的[向量空间](@entry_id:151108)。这个同构在[表示论](@entry_id:137998)的范畴中也成立，但需要仔细处理[群作用](@entry_id:268812)。为了使 $\text{Hom}(V, W)$ 成为一个 $G$-表示，我们需要定义一个群作用。对于 $\psi \in \text{Hom}(V, W)$，其被 $g \in G$ 作用后的结果 $g \cdot \psi$ 是一个新的[线性映射](@entry_id:185132)，定义为：
$$
(g \cdot \psi)(v) = g \cdot (\psi(g^{-1} \cdot v)) \quad \text{for all } v \in V
$$
有了这个定义，上述自然同构可以提升为 $G$-同构：
$$
\text{Hom}_G(U \otimes V, W) \cong \text{Hom}_G(U, \text{Hom}(V, W))
$$
这个同构 $\Psi$ 的具体形式为：给定一个 $T \in \text{Hom}_G(U \otimes V, W)$，它对应的 $\Psi(T) \in \text{Hom}_G(U, \text{Hom}(V, W))$ 是一个映射，它将 $u \in U$ 映到线性映射 $[\Psi(T)(u)]: V \to W$，该映射由 $[\Psi(T)(u)](v) = T(u \otimes v)$ 定义。这个强大的工具允许我们在不同的同态空间之间转换，有时能极大地简化计算。[@problem_id:1620573]

总之，$G$-同态是研究和比较[群表示](@entry_id:156757)的基本工具。它们的结构由[舒尔引理](@entry_id:136779)严格约束，并为我们提供了分解表示、计算[重数](@entry_id:136466)以及理解表示内部结构（如[不变子空间](@entry_id:152829)）的系统性方法。掌握 $G$-同态的原理与机制，是深入学习表示论的关键一步。