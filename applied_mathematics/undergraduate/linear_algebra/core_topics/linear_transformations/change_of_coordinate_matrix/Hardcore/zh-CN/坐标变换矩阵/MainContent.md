## 引言
在研究向量空间时，我们常常通过一组基来为其建立一个坐标系，从而将抽象的向量用具体的数字坐标来描述。然而，基的选择并非唯一，同一个向量在不同的坐标系下会有不同的“地址”。那么，我们如何在这些不同的坐标表示之间自如切换？坐标变换矩阵（Change-of-coordinate Matrix）正是解答这一核心问题的关键。它不仅是线性代数中的一个基本计算工具，更是一种强大的思想，能帮助我们选择最优视角来简化和理解复杂的线性系统。

本文将带领读者全面掌握坐标变换矩阵。在“原理与机制”部分，我们将从基本定义出发，学习如何构造坐标变换矩阵，并深入理解其与线性变换矩阵之间的相似关系，特别是它在对角化过程中的核心作用。接下来，在“应用与交叉学科联系”部分，我们将走出纯粹的理论，探索坐标变换如何在计算机图形学、控制理论、函数分析乃至奇异值分解（SVD）等领域中，成为解决实际问题的有力武器。最后，通过“动手实践”环节，您将有机会巩固所学知识，将理论应用于具体计算中。通过这几部分的学习，您将深刻体会到坐标变换作为连接代数、几何与应用的桥梁所具有的独特魅力。

## 原理与机制

在向量空间中，一组基的选择相当于为这个空间建立了一个坐标系。一旦基确定，空间中的每一个向量都可以用一个唯一的坐标向量来表示。然而，对于同一个向量空间，我们可以选择不同的基。这就引出了一个核心问题：同一个向量，在不同坐标系下的“地址”或坐标之间，存在怎样的联系？我们如何从一个坐标系转换到另一个？本章将深入探讨坐标变换矩阵的原理与机制，它是连接不同视角、简化线性变换的关键工具。

### 坐标变换矩阵的定义与构造

想象一个抽象的向量 $\mathbf{x}$ 存在于向量空间 $V$ 中。如果我们有两组不同的基，$\mathcal{B} = \{\mathbf{b}_1, \mathbf{b}_2, \dots, \mathbf{b}_n\}$ 和 $\mathcal{C} = \{\mathbf{c}_1, \mathbf{c}_2, \dots, \mathbf{c}_n\}$，那么向量 $\mathbf{x}$ 可以分别表示为这两组基的线性组合：

$\mathbf{x} = d_1 \mathbf{b}_1 + d_2 \mathbf{b}_2 + \dots + d_n \mathbf{b}_n$

$\mathbf{x} = e_1 \mathbf{c}_1 + e_2 \mathbf{c}_2 + \dots + e_n \mathbf{c}_n$

这里的系数 $(d_1, \dots, d_n)$ 和 $(e_1, \dots, e_n)$ 就是向量 $\mathbf{x}$ 分别相对于基 $\mathcal{B}$ 和基 $\mathcal{C}$ 的坐标。我们用列向量的形式将它们记为 $[\mathbf{x}]_{\mathcal{B}}$ 和 $[\mathbf{x}]_{\mathcal{C}}$。

$[\mathbf{x}]_{\mathcal{B}} = \begin{pmatrix} d_1 \\ d_2 \\ \vdots \\ d_n \end{pmatrix}, \quad [\mathbf{x}]_{\mathcal{C}} = \begin{pmatrix} e_1 \\ e_2 \\ \vdots \\ e_n \end{pmatrix}$

我们的目标是找到一个矩阵，能够将任意向量的 $\mathcal{B}$-坐标转换为其 $\mathcal{C}$-坐标。这个矩阵被称为**从 $\mathcal{B}$ 到 $\mathcal{C}$ 的坐标变换矩阵** (change-of-coordinate matrix from $\mathcal{B}$ to $\mathcal{C}$)，记作 $P_{\mathcal{C} \leftarrow \mathcal{B}}$。它满足以下关系：

$[\mathbf{x}]_{\mathcal{C}} = P_{\mathcal{C} \leftarrow \mathcal{B}} [\mathbf{x}]_{\mathcal{B}}$

要构造这个矩阵，关键在于理解它如何作用于“旧”基 $\mathcal{B}$ 中的向量。考虑基向量 $\mathbf{b}_j$ 本身。它的 $\mathcal{B}$-坐标向量是一个标准单位向量 $\mathbf{e}_j$（第 $j$ 个分量为 1，其余为 0）。那么，根据变换关系，$\mathbf{b}_j$ 的 $\mathcal{C}$-坐标向量 $[\mathbf{b}_j]_{\mathcal{C}}$ 就是 $P_{\mathcal{C} \leftarrow \mathcal{B}}$ 乘以 $\mathbf{e}_j$，这恰好是 $P_{\mathcal{C} \leftarrow \mathcal{B}}$ 的第 $j$ 列。

因此，我们得到了构造坐标变换矩阵的核心方法：**矩阵 $P_{\mathcal{C} \leftarrow \mathcal{B}}$ 的第 $j$ 列是基向量 $\mathbf{b}_j$ 在基 $\mathcal{C}$ 下的坐标向量 $[\mathbf{b}_j]_{\mathcal{C}}$**。

$P_{\mathcal{C} \leftarrow \mathcal{B}} = \begin{pmatrix} [\mathbf{b}_1]_{\mathcal{C}}  [\mathbf{b}_2]_{\mathcal{C}}  \cdots  [\mathbf{b}_n]_{\mathcal{C}} \end{pmatrix}$

这个原理不仅适用于 $\mathbb{R}^n$ 空间，也适用于任何有限维向量空间，例如多项式空间。假设在一个二次多项式空间 $\mathbb{P}_2$ 中，有两组基 $\mathcal{B} = \{b_1, b_2, b_3\}$ 和 $\mathcal{C} = \{c_1, c_2, c_3\}$。如果我们知道如何用基 $\mathcal{C}$ 的向量来表示基 $\mathcal{B}$ 的向量，例如：

$b_1 = 1 \cdot c_1 + 2 \cdot c_2 + 0 \cdot c_3$
$b_2 = 0 \cdot c_1 - 1 \cdot c_2 + 3 \cdot c_3$
$b_3 = 4 \cdot c_1 + 0 \cdot c_2 - 2 \cdot c_3$

那么，基向量 $b_1, b_2, b_3$ 在基 $\mathcal{C}$ 下的坐标向量就直接给出了：
$[b_1]_{\mathcal{C}} = \begin{pmatrix} 1 \\ 2 \\ 0 \end{pmatrix}, \quad [b_2]_{\mathcal{C}} = \begin{pmatrix} 0 \\ -1 \\ 3 \end{pmatrix}, \quad [b_3]_{\mathcal{C}} = \begin{pmatrix} 4 \\ 0 \\ -2 \end{pmatrix}$

根据构造法则，将这些坐标向量作为列，我们就能立即写出坐标变换矩阵 [@problem_id:1352377]：
$P_{\mathcal{C} \leftarrow \mathcal{B}} = \begin{pmatrix} 1  0  4 \\ 2  -1  0 \\ 0  3  -2 \end{pmatrix}$

这个矩阵可以将任何一个多项式在 $\mathcal{B}$ 基下的坐标，精确地转换为它在 $\mathcal{C}$ 基下的坐标。

### 与标准基的转换

在 $\mathbb{R}^n$ 空间中，最常用的一类坐标变换是在某个非标准基 $\mathcal{B} = \{\mathbf{b}_1, \dots, \mathbf{b}_n\}$ 和标准基 $\mathcal{E} = \{\mathbf{e}_1, \dots, \mathbf{e}_n\}$ 之间进行。这类变换具有特别简洁的形式。

#### 从自定义基到标准基

假设我们有一个自定义的基 $\mathcal{B}$，并且基向量 $\mathbf{b}_j$ 都是用标准坐标表示的。这种情况在计算机图形学中非常普遍，其中对象的“局部坐标系”由基 $\mathcal{B}$ 定义，而场景的“世界坐标系”是标准坐标系 $\mathcal{E}$ [@problem_id:1352418]。

一个向量 $\mathbf{x}$ 在基 $\mathcal{B}$ 下的坐标为 $[\mathbf{x}]_{\mathcal{B}} = (c_1, \dots, c_n)^T$，这意味着 $\mathbf{x} = c_1 \mathbf{b}_1 + \dots + c_n \mathbf{b}_n$。这个方程可以写成矩阵形式：
$\mathbf{x} = \begin{pmatrix} \mathbf{b}_1  \mathbf{b}_2  \cdots  \mathbf{b}_n \end{pmatrix} \begin{pmatrix} c_1 \\ c_2 \\ \vdots \\ c_n \end{pmatrix}$

由于 $\mathbf{x}$ 本身就是它在标准基 $\mathcal{E}$ 下的坐标向量（即 $\mathbf{x} = [\mathbf{x}]_{\mathcal{E}}$），我们可以看到，从 $\mathcal{B}$-坐标转换到标准坐标的矩阵 $P_{\mathcal{E} \leftarrow \mathcal{B}}$ 就是由基向量 $\mathbf{b}_j$ 作为列构成的矩阵。我们通常简记这个矩阵为 $P_{\mathcal{B}}$。

$P_{\mathcal{E} \leftarrow \mathcal{B}} = \begin{pmatrix} \mathbf{b}_1  \mathbf{b}_2  \cdots  \mathbf{b}_n \end{pmatrix}$

这个结论非常直观：它仅仅是将基向量的线性组合这个定义本身，重新表述为一次矩阵乘法。

#### 从标准基到自定义基

反向的变换，即将一个在标准坐标系下给出的向量，转换为它在自定义基 $\mathcal{B}$ 下的坐标，则需要更多的计算。根据关系 $\mathbf{x} = P_{\mathcal{E} \leftarrow \mathcal{B}} [\mathbf{x}]_{\mathcal{B}}$，我们可以通过求解线性方程组来找到 $[\mathbf{x}]_{\mathcal{B}}$。如果我们将变换写成 $[\mathbf{x}]_{\mathcal{B}} = P_{\mathcal{B} \leftarrow \mathcal{E}} \mathbf{x}$，那么显然，这个变换矩阵 $P_{\mathcal{B} \leftarrow \mathcal{E}}$ 必须是 $P_{\mathcal{E} \leftarrow \mathcal{B}}$ 的逆矩阵。

$P_{\mathcal{B} \leftarrow \mathcal{E}} = (P_{\mathcal{E} \leftarrow \mathcal{B}})^{-1}$

这个逆向变换在许多科学领域中至关重要，例如在材料科学中，实验数据通常在实验室的标准笛卡尔坐标系（标准基 $\mathcal{E}$）下获得，但理论分析则需要在与晶格结构相适应的非正交基（自定义基 $\mathcal{B}$）中进行 [@problem_id:1352432]。计算 $P_{\mathcal{B} \leftarrow \mathcal{E}}$ 就需要对矩阵 $P_{\mathcal{E} \leftarrow \mathcal{B}}$ 求逆。由于基向量是线性无关的，矩阵 $P_{\mathcal{E} \leftarrow \mathcal{B}}$ 的列向量线性无关，因此它总是可逆的。

### 坐标变换矩阵的基本性质

坐标变换矩阵遵循一系列代数性质，这些性质构成了它们运算的法则。

#### 逆变换性质

从基 $\mathcal{B}$ 到基 $\mathcal{C}$ 的变换由 $P_{\mathcal{C} \leftarrow \mathcal{B}}$ 实现，而从 $\mathcal{C}$ 反向变换回 $\mathcal{B}$ 则由 $P_{\mathcal{B} \leftarrow \mathcal{C}}$ 实现。这两次变换是互逆的。对任意向量 $\mathbf{x}$，我们有：
$[\mathbf{x}]_{\mathcal{C}} = P_{\mathcal{C} \leftarrow \mathcal{B}} [\mathbf{x}]_{\mathcal{B}}$
$[\mathbf{x}]_{\mathcal{B}} = P_{\mathcal{B} \leftarrow \mathcal{C}} [\mathbf{x}]_{\mathcal{C}}$

将第一个式子代入第二个，得到 $[\mathbf{x}]_{\mathcal{B}} = P_{\mathcal{B} \leftarrow \mathcal{C}} P_{\mathcal{C} \leftarrow \mathcal{B}} [\mathbf{x}]_{\mathcal{B}}$。由于这对所有 $[\mathbf{x}]_{\mathcal{B}}$ 都成立，所以 $P_{\mathcal{B} \leftarrow \mathcal{C}} P_{\mathcal{C} \leftarrow \mathcal{B}}$ 必须是单位矩阵 $I$。因此，我们有一般性的**逆变换性质**：

$P_{\mathcal{B} \leftarrow \mathcal{C}} = (P_{\mathcal{C} \leftarrow \mathcal{B}})^{-1}$

这个性质在实际应用中非常有用，例如，在计算机图形学中，如果已知从“世界”坐标系到“相机”坐标系的变换矩阵，那么其逆矩阵就是将相机空间中的坐标变换回世界坐标系所需的矩阵 [@problem_id:1352406]。

一个自然的推论是，从一个基到其自身的坐标变换矩阵必定是单位矩阵 $I$ [@problem_id:1352402]：
$P_{\mathcal{B} \leftarrow \mathcal{B}} = I$

这符合直觉：如果不改变坐标系，坐标自然也保持不变。

#### 复合变换性质（链式法则）

如果坐标变换涉及三个或更多的基，我们可以通过矩阵乘法将它们串联起来。假设我们有三组基 $\mathcal{A}$, $\mathcal{B}$, $\mathcal{C}$。从 $\mathcal{A}$-坐标到 $\mathcal{B}$-坐标的变换是 $[\mathbf{x}]_{\mathcal{B}} = P_{\mathcal{B} \leftarrow \mathcal{A}} [\mathbf{x}]_{\mathcal{A}}$，从 $\mathcal{B}$-坐标到 $\mathcal{C}$-坐标的变换是 $[\mathbf{x}]_{\mathcal{C}} = P_{\mathcal{C} \leftarrow \mathcal{B}} [\mathbf{x}]_{\mathcal{B}}$。

将前者代入后者，我们得到：
$[\mathbf{x}]_{\mathcal{C}} = P_{\mathcal{C} \leftarrow \mathcal{B}} (P_{\mathcal{B} \leftarrow \mathcal{A}} [\mathbf{x}]_{\mathcal{A}}) = (P_{\mathcal{C} \leftarrow \mathcal{B}} P_{\mathcal{B} \leftarrow \mathcal{A}}) [\mathbf{x}]_{\mathcal{A}}$

这表明，从 $\mathcal{A}$ 直接到 $\mathcal{C}$ 的变换矩阵 $P_{\mathcal{C} \leftarrow \mathcal{A}}$ 等于两个中间变换矩阵的乘积。这个**链式法则** (chain rule) 是：

$P_{\mathcal{C} \leftarrow \mathcal{A}} = P_{\mathcal{C} \leftarrow \mathcal{B}} P_{\mathcal{B} \leftarrow \mathcal{A}}$

这个法则在处理复杂的坐标系统网络时非常强大。例如，如果我们知道从基 $\mathcal{A}$ 到 $\mathcal{B}$ 和从基 $\mathcal{A}$ 到 $\mathcal{C}$ 的变换矩阵，我们可以通过组合它们来找到从 $\mathcal{B}$ 到 $\mathcal{C}$ 的变换矩阵 [@problem_id:1352396]：
$P_{\mathcal{C} \leftarrow \mathcal{B}} = P_{\mathcal{C} \leftarrow \mathcal{A}} P_{\mathcal{A} \leftarrow \mathcal{B}} = P_{\mathcal{C} \leftarrow \mathcal{A}} (P_{\mathcal{B} \leftarrow \mathcal{A}})^{-1}$

#### 坐标变换与恒等映射

坐标变换矩阵还有一个更深层次的抽象理解。我们可以将坐标变换视为**恒等线性变换** (identity linear transformation) $I: V \to V$（即 $I(\mathbf{x}) = \mathbf{x}$）在不同基下的矩阵表示。

通常，一个线性变换 $T: V \to W$ 的矩阵表示 $[T]_{\mathcal{C} \leftarrow \mathcal{B}}$ 的列向量是 $T$ 作用于输入空间基 $\mathcal{B}$ 的向量后，在输出空间基 $\mathcal{C}$ 中的坐标。如果我们将这个概念应用于恒等变换 $I: V \to V$，并为定义域和到达域选择不同的基 $\mathcal{B}$ 和 $\mathcal{C}$，那么其矩阵表示 $[I]_{\mathcal{C} \leftarrow \mathcal{B}}$ 的第 $j$ 列就是 $I(\mathbf{b}_j) = \mathbf{b}_j$ 在基 $\mathcal{C}$ 下的坐标向量 $[\mathbf{b}_j]_{\mathcal{C}}$。

这恰恰就是我们之前定义的坐标变换矩阵 $P_{\mathcal{C} \leftarrow \mathcal{B}}$。因此：

$P_{\mathcal{C} \leftarrow \mathcal{B}} = [I]_{\mathcal{C} \leftarrow \mathcal{B}}$

这个视角统一了线性变换矩阵和坐标变换矩阵的概念，揭示了后者是前者在恒等变换下的一个特例 [@problem_id:1352374]。

### 坐标变换与线性变换的矩阵表示

坐标变换矩阵最强大的应用之一，是研究同一个线性变换在不同基下的矩阵表示之间的关系。选择一个合适的基，往往可以极大地简化线性变换的矩阵形式。

假设有一个线性变换 $T: V \to V$，它在基 $\mathcal{B}$ 下的矩阵表示是 $[T]_{\mathcal{B}}$，在基 $\mathcal{C}$ 下的表示是 $[T]_{\mathcal{C}}$。我们希望找到这两个矩阵之间的联系。

考虑一个向量 $\mathbf{x} \in V$，令 $\mathbf{y} = T(\mathbf{x})$。在基 $\mathcal{B}$ 中，这个变换表示为 $[\mathbf{y}]_{\mathcal{B}} = [T]_{\mathcal{B}} [\mathbf{x}]_{\mathcal{B}}$。我们的目标是推导出在基 $\mathcal{C}$ 中的类似关系。

我们可以通过坐标变换来“绕道”：
1.  从 $\mathcal{C}$-坐标开始，用 $P_{\mathcal{B} \leftarrow \mathcal{C}}$ 转换到 $\mathcal{B}$-坐标：$[\mathbf{x}]_{\mathcal{B}} = P_{\mathcal{B} \leftarrow \mathcal{C}} [\mathbf{x}]_{\mathcal{C}}$。
2.  在 $\mathcal{B}$-坐标系中执行变换：$[\mathbf{y}]_{\mathcal{B}} = [T]_{\mathcal{B}} [\mathbf{x}]_{\mathcal{B}} = [T]_{\mathcal{B}} P_{\mathcal{B} \leftarrow \mathcal{C}} [\mathbf{x}]_{\mathcal{C}}$。
3.  将结果从 $\mathcal{B}$-坐标转换回 $\mathcal{C}$-坐标：$[\mathbf{y}]_{\mathcal{C}} = P_{\mathcal{C} \leftarrow \mathcal{B}} [\mathbf{y}]_{\mathcal{B}}$。

将这三步结合起来，我们得到：
$[\mathbf{y}]_{\mathcal{C}} = P_{\mathcal{C} \leftarrow \mathcal{B}} [T]_{\mathcal{B}} P_{\mathcal{B} \leftarrow \mathcal{C}} [\mathbf{x}]_{\mathcal{C}}$

由于 $[\mathbf{y}]_{\mathcal{C}} = [T]_{\mathcal{C}} [\mathbf{x}]_{\mathcal{C}}$，我们得到了两个矩阵表示之间的**相似变换** (similarity transformation) 关系：

$[T]_{\mathcal{C}} = P_{\mathcal{C} \leftarrow \mathcal{B}} [T]_{\mathcal{B}} P_{\mathcal{B} \leftarrow \mathcal{C}}$

令 $P = P_{\mathcal{C} \leftarrow \mathcal{B}}$，则 $P_{\mathcal{B} \leftarrow \mathcal{C}} = P^{-1}$，上式可以写成更简洁的形式：

$[T]_{\mathcal{C}} = P [T]_{\mathcal{B}} P^{-1}$

这个公式是线性代数的核心之一 [@problem_id:1352378]。它表明，同一线性变换在不同基下的矩阵表示是相似的。

#### 对角化：一种特殊的坐标变换

相似变换最重要的应用是**对角化** (diagonalization)。如果一个线性变换 $T$ 在标准基 $\mathcal{E}$ 下的矩阵是 $A$，我们能否找到一个基 $\mathcal{B}$，使得 $T$ 在这个新基下的矩阵 $[T]_{\mathcal{B}}$ 是一个对角矩阵 $D$？

如果可以，那么根据相似变换公式（从 $\mathcal{B}$ 变换到 $\mathcal{E}$），我们有：
$[T]_{\mathcal{E}} = P_{\mathcal{E} \leftarrow \mathcal{B}} [T]_{\mathcal{B}} (P_{\mathcal{E} \leftarrow \mathcal{B}})^{-1}$
$A = P D P^{-1}$

这里的 $P = P_{\mathcal{E} \leftarrow \mathcal{B}}$ 是从新基 $\mathcal{B}$ 变换到标准基的矩阵。这个基 $\mathcal{B}$ 必须由 $A$ 的特征向量组成，而对角矩阵 $D$ 的对角元则是对应的特征值。因此，对角化过程本质上是进行一次坐标变换：从标准基变换到一个由特征向量组成的“理想”基，在这个基里，线性变换的作用仅仅是在各个基向量方向上进行缩放 [@problem_id:1352412]。

#### 基不变量

相似变换关系揭示了某些量是线性算符的内在属性，不随基的选择而改变，这些量被称为**基不变量** (basis invariants)。行列式就是其中一个重要的例子。
利用行列式的乘法性质，我们有：
$\det([T]_{\mathcal{C}}) = \det(P [T]_{\mathcal{B}} P^{-1}) = \det(P) \det([T]_{\mathcal{B}}) \det(P^{-1})$

因为 $\det(P^{-1}) = 1/\det(P)$，所以：
$\det([T]_{\mathcal{C}}) = \det([T]_{\mathcal{B}})$

这证明了线性算符的行列式是一个内在属性，其值与我们选择用哪个基来计算它无关 [@problem_id:1352408]。其他不变量还包括迹 (trace) 和特征值。

### 几何解释

最后，坐标变换矩阵的行列式具有深刻的几何意义。在 $\mathbb{R}^n$ 中，一组基向量 $\{\mathbf{b}_1, \dots, \mathbf{b}_n\}$ 张成一个平行多面体。这个多面体的（有向）体积由矩阵 $P_{\mathcal{E} \leftarrow \mathcal{B}} = \begin{pmatrix} \mathbf{b}_1  \cdots  \mathbf{b}_n \end{pmatrix}$ 的行列式给出。

$\text{Volume}(\mathcal{B}) = \det(P_{\mathcal{E} \leftarrow \mathcal{B}})$

现在考虑两个基 $\mathcal{B}$ 和 $\mathcal{C}$ 之间的变换矩阵 $P_{\mathcal{C} \leftarrow \mathcal{B}}$。利用链式法则 $P_{\mathcal{E} \leftarrow \mathcal{B}} = P_{\mathcal{E} \leftarrow \mathcal{C}} P_{\mathcal{C} \leftarrow \mathcal{B}}$，并取两边的行列式：
$\det(P_{\mathcal{E} \leftarrow \mathcal{B}}) = \det(P_{\mathcal{E} \leftarrow \mathcal{C}}) \det(P_{\mathcal{C} \leftarrow \mathcal{B}})$

这导出了一个优美的结果：
$\det(P_{\mathcal{C} \leftarrow \mathcal{B}}) = \frac{\det(P_{\mathcal{E} \leftarrow \mathcal{B}})}{\det(P_{\mathcal{E} \leftarrow \mathcal{C}})} = \frac{\text{Volume}(\mathcal{B})}{\text{Volume}(\mathcal{C})}$

因此，**坐标变换矩阵 $P_{\mathcal{C} \leftarrow \mathcal{B}}$ 的行列式，是基 $\mathcal{B}$ 张成的“单位体积”与基 $\mathcal{C}$ 张成的“单位体积”之比** [@problem_id:1352437]。它衡量了从一个坐标系到另一个坐标系时，体积度量的相对变化。如果行列式的绝对值大于1，说明从 $\mathcal{B}$ 坐标到 $\mathcal{C}$ 坐标的转换会“放大”体积的数值；如果小于1，则会“缩小”。符号的正负则反映了两个基的定向（手性）是否相同。

综上所述，坐标变换矩阵不仅是一个计算工具，它还深刻地联系了向量空间的不同代数表示，揭示了线性变换的内在结构，并具有清晰的几何意义。掌握其原理和机制，是深入理解线性代数的关键一步。