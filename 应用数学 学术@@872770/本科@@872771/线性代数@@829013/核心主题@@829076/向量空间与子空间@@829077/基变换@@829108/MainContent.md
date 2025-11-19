## 引言
在线性代数中，“基”如同衡量[向量空间](@entry_id:151108)的标尺。而“[基变换](@entry_id:189626)”——即在不同标尺间切换视角的能力——是理解和解决众多高级问题的核心。它不仅是代数运算，更是一种强大的思维方式，让我们能以最简洁的形式洞察向量和变换的本质。然而，一个向量或[线性变换](@entry_id:149133)的坐标表示会因基的选择而异。这引出了一个根本问题：我们如何系统地在这些不同的表示之间进行转换，并理解哪些性质在转换中保持不变？

本文将带你深入探索[基变换](@entry_id:189626)的世界。在“原理与机制”章节，我们将揭示坐标转换和变换矩阵变化的数学法则。接着，在“应用与跨学科联系”章节，你将看到这些理论如何在几何、动力系统、信号处理和量子力学中大放异彩。最后，通过“动手实践”环节，你将巩固所学，将理论付诸实践。让我们从基变换最根本的原理开始，理解[向量的坐标](@entry_id:198852)究竟是如何随着我们选择的“度量尺”而变化的。

## 原理与机制

在线性代数的研究中，一个核心思想是将抽象的数学对象（如向量和[线性变换](@entry_id:149133)）通过一组选定的“度量尺”进行具象化。这组度量尺就是我们所说的 **基 (basis)**。然而，正如我们可以用米或英尺来测量长度一样，我们也可以为同一个[向量空间](@entry_id:151108)选择不同的基。改变视角——也就是从一个基转换到另一个基——是解决许多复杂问题的关键策略。本章将深入探讨基变换的根本原理与核心机制，阐明坐标如何变化，以及[线性变换的矩阵表示](@entry_id:162822)如何随之调整。

### [向量的坐标](@entry_id:198852)表示

一个[向量空间](@entry_id:151108) $V$ 中的向量 $\mathbf{v}$ 是一个独立于任何特定[坐标系](@entry_id:156346)存在的抽象实体。然而，为了进行计算，我们通常需要将其表示为一组数，即一个 **[坐标向量](@entry_id:153319) (coordinate vector)**。这个过程需要一个有序基。

考虑一个 $n$ 维[向量空间](@entry_id:151108) $V$。一个有序基 $\mathcal{B} = \{\mathbf{b}_1, \mathbf{b}_2, \dots, \mathbf{b}_n\}$ 是 $V$ 中一组[线性无关](@entry_id:148207)的向量，它们可以张成 (span) 整个空间 $V$。这意味着任何向量 $\mathbf{v} \in V$ 都可以唯一地表示为这些[基向量](@entry_id:199546)的线性组合：
$$
\mathbf{v} = c_1 \mathbf{b}_1 + c_2 \mathbf{b}_2 + \dots + c_n \mathbf{b}_n
$$
这些唯一的标量 $c_1, c_2, \dots, c_n$ 构成了向量 $\mathbf{v}$ 相对于基 $\mathcal{B}$ 的坐标。我们将这些坐标组织成一个列向量，称为 $\mathbf{v}$ 的 **$\mathcal{B}$-[坐标向量](@entry_id:153319) (coordinate vector of $\mathbf{v}$ relative to $\mathcal{B}$)**，记作 $[\mathbf{v}]_{\mathcal{B}}$:
$$
[\mathbf{v}]_{\mathcal{B}} = \begin{pmatrix} c_1 \\ c_2 \\ \vdots \\ c_n \end{pmatrix}
$$
在熟悉的[向量空间](@entry_id:151108) $\mathbb{R}^n$ 中，我们最常使用的是 **标准基 (standard basis)** $\mathcal{E} = \{\mathbf{e}_1, \dots, \mathbf{e}_n\}$，其中 $\mathbf{e}_j$ 是第 $j$ 个分量为 1，其余分量为 0 的向量。对于任意向量 $\mathbf{x} = \begin{pmatrix} x_1, \dots, x_n \end{pmatrix}^T$，它本身就是其在标准基下的[坐标向量](@entry_id:153319)，即 $[\mathbf{x}]_{\mathcal{E}} = \mathbf{x}$。

当引入一个新基时，核心问题就出现了：如果我们已知一个向量在某个基（例如标准基）下的坐标，如何找到它在另一个新基下的坐标？

假设在 $\mathbb{R}^2$ 中，我们有一个新基 $\mathcal{B} = \{\mathbf{b}_1, \mathbf{b}_2\}$。一个向量 $\mathbf{v}$ 在标准基下的坐标为 $\mathbf{v} = \begin{pmatrix} x \\ y \end{pmatrix}$。我们想找到它在 $\mathcal{B}$ 基下的坐标 $[\mathbf{v}]_{\mathcal{B}} = \begin{pmatrix} k_1 \\ k_2 \end{pmatrix}$。根据定义，这满足：
$$
\mathbf{v} = k_1 \mathbf{b}_1 + k_2 \mathbf{b}_2
$$
如果我们用标准坐标表示[基向量](@entry_id:199546) $\mathbf{b}_1 = \begin{pmatrix} a \\ c \end{pmatrix}$ 和 $\mathbf{b}_2 = \begin{pmatrix} b \\ d \end{pmatrix}$，上述向量方程就可以转化为一个[矩阵方程](@entry_id:203695) [@problem_id:1351877]：
$$
\begin{pmatrix} x \\ y \end{pmatrix} = k_1 \begin{pmatrix} a \\ c \end{pmatrix} + k_2 \begin{pmatrix} b \\ d \end{pmatrix} = \begin{pmatrix} a  b \\ c  d \end{pmatrix} \begin{pmatrix} k_1 \\ k_2 \end{pmatrix}
$$
这个方程揭示了寻找新坐标的直接方法：求解一个线性方程组。

### 坐标转换矩阵

上述关系是基变换理论的基石。我们可以将其推广并形式化。

#### 从一个基到另一个基的转换

令 $\mathcal{B} = \{\mathbf{b}_1, \dots, \mathbf{b}_n\}$ 和 $\mathcal{C} = \{\mathbf{c}_1, \dots, \mathbf{c}_n\}$ 是[向量空间](@entry_id:151108) $V$ 的两个基。对于任意向量 $\mathbf{x} \in V$，它同时拥有 $\mathcal{B}$-[坐标向量](@entry_id:153319) $[\mathbf{x}]_{\mathcal{B}}$ 和 $\mathcal{C}$-[坐标向量](@entry_id:153319) $[\mathbf{x}]_{\mathcal{C}}$。必定存在一个唯一的、可逆的 $n \times n$ 矩阵，记作 $P_{\mathcal{C} \leftarrow \mathcal{B}}$，它能将 $\mathcal{B}$-[坐标映射](@entry_id:747874)到 $\mathcal{C}$-坐标：
$$
[\mathbf{x}]_{\mathcal{C}} = P_{\mathcal{C} \leftarrow \mathcal{B}} [\mathbf{x}]_{\mathcal{B}}
$$
这个矩阵 $P_{\mathcal{C} \leftarrow \mathcal{B}}$ 被称为 **从 $\mathcal{B}$ 到 $\mathcal{C}$ 的坐标转换矩阵 (change-of-coordinates matrix from $\mathcal{B}$ to $\mathcal{C}$)**。

这个矩阵的构造方式非常直观。它的第 $j$ 列，正是旧[基向量](@entry_id:199546) $\mathbf{b}_j$ 在新基 $\mathcal{C}$ 下的[坐标向量](@entry_id:153319) [@problem_id:1351894]。
$$
P_{\mathcal{C} \leftarrow \mathcal{B}} = \begin{pmatrix} [\mathbf{b}_1]_{\mathcal{C}}  [\mathbf{b}_2]_{\mathcal{C}}  \cdots  [\mathbf{b}_n]_{\mathcal{C}} \end{pmatrix}
$$
要验证这一点，只需考虑一个向量 $\mathbf{x}$，其 $\mathcal{B}$-坐标为 $[\mathbf{x}]_{\mathcal{B}} = \begin{pmatrix} k_1, \dots, k_n \end{pmatrix}^T$。这意味着 $\mathbf{x} = \sum_{j=1}^n k_j \mathbf{b}_j$。由于[坐标映射](@entry_id:747874)是线性的，我们有：
$$
[\mathbf{x}]_{\mathcal{C}} = \left[ \sum_{j=1}^n k_j \mathbf{b}_j \right]_{\mathcal{C}} = \sum_{j=1}^n k_j [\mathbf{b}_j]_{\mathcal{C}} = \begin{pmatrix} [\mathbf{b}_1]_{\mathcal{C}}  \cdots  [\mathbf{b}_n]_{\mathcal{C}} \end{pmatrix} \begin{pmatrix} k_1 \\ \vdots \\ k_n \end{pmatrix} = P_{\mathcal{C} \leftarrow \mathcal{B}} [\mathbf{x}]_{\mathcal{B}}
$$
这个原理适用于任何[向量空间](@entry_id:151108)，不仅限于 $\mathbb{R}^n$。例如，在次数不超过2的[多项式空间](@entry_id:144410) $P_2(\mathbb{R})$ 中，我们可以定义不同的基，如 $\mathcal{B} = \{1, x+1, x^2+x+1\}$ 和 $\mathcal{C} = \{x^2-1, x, 2\}$。要找到坐标转换矩阵 $P_{\mathcal{C} \leftarrow \mathcal{B}}$，我们需要依次计算 $\mathcal{B}$ 中每个[基向量](@entry_id:199546)在 $\mathcal{C}$ 基下的坐标，并将它们作为列向量来构建矩阵 [@problem_id:1351845]。

在最常见的情形中，我们从一个自定义基 $\mathcal{B}$ 转换到标准基 $\mathcal{E}$。此时，矩阵 $P_{\mathcal{E} \leftarrow \mathcal{B}}$ 的构造特别简单：它的列就是[基向量](@entry_id:199546) $\mathbf{b}_j$ 本身（因为向量在标准基下的坐标就是它自己的分量）。这个矩阵通常简记为 $P_{\mathcal{B}}$。
$$
P_{\mathcal{E} \leftarrow \mathcal{B}} = \begin{pmatrix} \mathbf{b}_1  \mathbf{b}_2  \cdots  \mathbf{b}_n \end{pmatrix}
$$
因此，我们有 $\mathbf{x} = P_{\mathcal{B}} [\mathbf{x}]_{\mathcal{B}}$。要从标准坐标 $\mathbf{x}$ 找到 $\mathcal{B}$-坐标 $[\mathbf{x}]_{\mathcal{B}}$，我们只需计算：
$$
[\mathbf{x}]_{\mathcal{B}} = P_{\mathcal{B}}^{-1} \mathbf{x}
$$
这为我们最初的问题提供了一个优雅的矩阵解法 [@problem_id:2093]。

#### 坐标转换矩阵的性质

坐标转换矩阵具有两个关键性质：

1.  **[可逆性](@entry_id:143146) (Invertibility)**: 从 $\mathcal{B}$ 到 $\mathcal{C}$ 的转换矩阵 $P_{\mathcal{C} \leftarrow \mathcal{B}}$ 总是可逆的，其逆矩阵恰好是从 $\mathcal{C}$ 到 $\mathcal{B}$ 的转换矩阵。
    $$
    (P_{\mathcal{C} \leftarrow \mathcal{B}})^{-1} = P_{\mathcal{B} \leftarrow \mathcal{C}}
    $$
    这个性质是符合直觉的：如果你有一种方法将坐标从 $\mathcal{B}$ 转换到 $\mathcal{C}$，那么必然存在一种精确的方法将其转换回来。例如，在信号处理中，如果有一个用于“分析”的基 $\mathcal{B}$ 和一个用于“合成”的基 $\mathcal{C}$，那么从分析坐标到合成坐标的转换矩阵 $P_{\mathcal{C} \leftarrow \mathcal{B}}$ 的[逆矩阵](@entry_id:140380)，就提供了从合成坐标返回到分析坐标的途径 [@problem_id:1351888]。

2.  **复合性 (Composition)**: 坐标转换可以链接起来。如果你有三个基 $\mathcal{B}, \mathcal{C}, \mathcal{D}$，那么从 $\mathcal{B}$ 直接到 $\mathcal{D}$ 的转换矩阵等于从 $\mathcal{B}$ 到 $\mathcal{C}$ 再到 $\mathcal{D}$ 的转换矩阵的乘积。
    $$
    P_{\mathcal{D} \leftarrow \mathcal{B}} = P_{\mathcal{D} \leftarrow \mathcal{C}} P_{\mathcal{C} \leftarrow \mathcal{B}}
    $$
    注意矩阵相乘的顺序：它反映了变换作用的顺序。一个向量先被 $P_{\mathcal{C} \leftarrow \mathcal{B}}$ 从 $\mathcal{B}$-坐标转换到 $\mathcal{C}$-坐标，然后结果再被 $P_{\mathcal{D} \leftarrow \mathcal{C}}$ 转换到 $\mathcal{D}$-坐标。这个链式法在处理涉及多个[坐标系](@entry_id:156346)的复杂系统时非常有用，比如一个同时被着陆器、探测车和[轨道](@entry_id:137151)卫星跟踪的行星探测任务 [@problem_id:1351838]。

### 线性变换的基变换

[基变换](@entry_id:189626)的真正威力体现在它如何简化对[线性变换](@entry_id:149133)的描述。一个[线性变换](@entry_id:149133) $T: V \to V$ 是一个保持[向量加法](@entry_id:155045)和标量乘法的映射。一旦我们为 $V$ 选择一个基 $\mathcal{B}$，我们就可以将这个抽象的变换 $T$ 表示为一个具体的矩阵 $[T]_{\mathcal{B}}$。

这个 **$\mathcal{B}$-矩阵 ($B$-matrix)** 的定义是：它的第 $j$ 列是[基向量](@entry_id:199546) $\mathbf{b}_j$ 经过变换后得到的向量 $T(\mathbf{b}_j)$ 在基 $\mathcal{B}$ 下的坐标。
$$
[T]_{\mathcal{B}} = \begin{pmatrix} [T(\mathbf{b}_1)]_{\mathcal{B}}  [T(\mathbf{b}_2)]_{\mathcal{B}}  \cdots  [T(\mathbf{b}_n)]_{\mathcal{B}} \end{pmatrix}
$$
这个矩阵的作用是，它将一个向量的 $\mathcal{B}$-[坐标映射](@entry_id:747874)到其像的 $\mathcal{B}$-坐标：
$$
[T(\mathbf{x})]_{\mathcal{B}} = [T]_{\mathcal{B}} [\mathbf{x}]_{\mathcal{B}}
$$
一个自然的问题是：如果同一个[线性变换](@entry_id:149133) $T$ 在一个基 $\mathcal{A}$ 下的矩阵是 $[T]_{\mathcal{A}}$，在另一个基 $\mathcal{B}$ 下的矩阵是 $[T]_{\mathcal{B}}$，那么这两个矩阵之间有什么关系？

我们可以通过追踪一个[向量的坐标](@entry_id:198852)变换路径来找到答案。假设我们从向量 $\mathbf{x}$ 的 $\mathcal{B}$-坐标 $[\mathbf{x}]_{\mathcal{B}}$ 开始：
1.  首先，将 $\mathcal{B}$-坐标转换为 $\mathcal{A}$-坐标：$[\mathbf{x}]_{\mathcal{A}} = P_{\mathcal{A} \leftarrow \mathcal{B}} [\mathbf{x}]_{\mathcal{B}}$。
2.  然后，在 $\mathcal{A}$ 基中应用变换：$[T(\mathbf{x})]_{\mathcal{A}} = [T]_{\mathcal{A}} [\mathbf{x}]_{\mathcal{A}}$。
3.  最后，将结果的 $\mathcal{A}$-坐标转换回 $\mathcal{B}$-坐标：$[T(\mathbf{x})]_{\mathcal{B}} = P_{\mathcal{B} \leftarrow \mathcal{A}} [T(\mathbf{x})]_{\mathcal{A}}$。

将这三步合并，我们得到：
$$
[T(\mathbf{x})]_{\mathcal{B}} = P_{\mathcal{B} \leftarrow \mathcal{A}} [T]_{\mathcal{A}} P_{\mathcal{A} \leftarrow \mathcal{B}} [\mathbf{x}]_{\mathcal{B}}
$$
由于这个关系对所有 $\mathbf{x}$ 都成立，我们便得到了矩阵之间的 **相似关系 (similarity relation)**：
$$
[T]_{\mathcal{B}} = P_{\mathcal{B} \leftarrow \mathcal{A}} [T]_{\mathcal{A}} P_{\mathcal{A} \leftarrow \mathcal{B}}
$$
利用 $(P_{\mathcal{A} \leftarrow \mathcal{B}})^{-1} = P_{\mathcal{B} \leftarrow \mathcal{A}}$，并令 $P = P_{\mathcal{A} \leftarrow \mathcal{B}}$（从新基到旧基的转换矩阵），上述公式通常写成：
$$
[T]_{\mathcal{B}} = P^{-1} [T]_{\mathcal{A}} P
$$
这个公式在实践中至关重要。例如，在数字设计中，一个变换 $T$ 可能在标准基 $\mathcal{E}$ 下有一个复杂的矩阵 $[T]_{\mathcal{E}}$。如果设计师在一个自定义的、倾斜的基 $\mathcal{B}$ 中工作，我们需要计算出变换在该基下的矩阵 $[T]_{\mathcal{B}}$，以确保效果符合预期。这可以通过计算 $P^{-1}[T]_{\mathcal{E}}P$ 来完成，其中 $P$ 的列是新[基向量](@entry_id:199546)在标准坐标下的表示 [@problem_id:1351855]。

这个过程反过来也同样强大。假设我们知道一个变换 $T$ 在某个特殊基 $\mathcal{B}$（例如由[特征向量](@entry_id:151813)组成的基）下的矩阵 $D=[T]_{\mathcal{B}}$ 非常简单（例如一个对角矩阵）。那么，它在标准基下的矩阵 $A=[T]_{\mathcal{E}}$ 就可以通过 $A = PDP^{-1}$ 得到，其中 $P$ 是从 $\mathcal{B}$ 到标准基的转换矩阵 [@problem_id:1351874]。这个过程被称为 **[对角化](@entry_id:147016) (diagonalization)**，它是理解线性变换几何本质的核心工具。

### [基变换](@entry_id:189626)下的[不变量](@entry_id:148850)

虽然向量和[线性变换的矩阵表示](@entry_id:162822)会随着基的选择而改变，但它们的一些内在属性是 **[不变量](@entry_id:148850) (invariants)**，即不随基的改变而改变。这些[不变量](@entry_id:148850)反映了对象固有的、几何或物理的性质，独立于我们描述它的语言（即[坐标系](@entry_id:156346)）。

对于一个[线性变换](@entry_id:149133) $T$，其最重要的[不变量](@entry_id:148850)包括 **迹 (trace)**、**[行列式](@entry_id:142978) (determinant)** 和 **[特征值](@entry_id:154894) (eigenvalues)**。

我们可以证明[特征值](@entry_id:154894)是基[不变量](@entry_id:148850)。假设 $\lambda$ 是 $T$ 的一个[特征值](@entry_id:154894)，对应于矩阵 $A = [T]_{\mathcal{A}}$，[特征向量](@entry_id:151813)为 $\mathbf{v}$。这意味着 $A\mathbf{v} = \lambda\mathbf{v}$。在另一个基 $\mathcal{B}$ 中，变换的矩阵为 $B = P^{-1}AP$。那么向量 $\mathbf{v}$ 在新基下的坐标为 $\mathbf{w} = P^{-1}\mathbf{v}$。现在我们看 $B$ 如何作用于 $\mathbf{w}$：
$$
B\mathbf{w} = (P^{-1}AP)(P^{-1}\mathbf{v}) = P^{-1}A(PP^{-1})\mathbf{v} = P^{-1}A\mathbf{v} = P^{-1}(\lambda\mathbf{v}) = \lambda(P^{-1}\mathbf{v}) = \lambda\mathbf{w}
$$
这表明 $B$ 拥有与 $A$ 完全相同的[特征值](@entry_id:154894) $\lambda$，只是对应的[特征向量](@entry_id:151813)变为了 $\mathbf{w}$。

这个[不变量](@entry_id:148850)性质具有深刻的物理意义。例如，在量子力学中，一个可观测物理量（如能量）由一个算符 $Q$ 表示。一次测量可能得到的结果，必须是该算符的某个[特征值](@entry_id:154894)。这些可测量的物理量是客观存在的，它们的值不应该因为物理学家选择在哪一个数学基（如“计算基”或“Hadamard基”）下进行计算而改变。因此，无论算符 $Q$ 在哪个基下表示为矩阵，其[特征值](@entry_id:154894)集合——即可能测得的能量值——必须是相同的 [@problem_id:2084052]。

### [对偶空间](@entry_id:146945)中的[基变换](@entry_id:189626)

[基变换](@entry_id:189626)的概念也可以推广到更抽象的结构，例如 **[对偶空间](@entry_id:146945) (dual space)**。对于一个[向量空间](@entry_id:151108) $V$，其[对偶空间](@entry_id:146945) $V^*$ 由所有从 $V$ 到其标量域的线性映射（称为 **[线性泛函](@entry_id:276136) (linear functionals)**）组成。

如果 $V$ 有一个基 $\mathcal{B} = \{\mathbf{b}_1, \dots, \mathbf{b}_n\}$，那么 $V^*$ 也存在一个相应的 **对偶基 (dual basis)** $\mathcal{B}^* = \{f^1, \dots, f^n\}$，其定义为 $f^i(\mathbf{b}_j) = \delta_{ij}$，其中 $\delta_{ij}$ 是克罗内克 δ 符号。

现在假设我们有两个基 $\mathcal{B}$ 和 $\mathcal{C}$，以及它们对应的对偶基 $\mathcal{B}^*$ 和 $\mathcal{C}^*$。我们已知向量坐标的变换规则：$[\mathbf{v}]_{\mathcal{C}} = P_{\mathcal{C} \leftarrow \mathcal{B}} [\mathbf{v}]_{\mathcal{B}}$。那么，一个[线性泛函](@entry_id:276136) $g \in V^*$ 的坐标是如何从 $\mathcal{B}^*$ 变换到 $\mathcal{C}^*$ 的呢？

我们可以利用一个[不变量](@entry_id:148850)来推导这个关系：泛函 $g$ 作用于向量 $\mathbf{v}$ 的结果 $g(\mathbf{v})$ 是一个标量，它不依赖于任何基的选择。利用坐标表示，我们有：
$$
g(\mathbf{v}) = \left( [g]_{\mathcal{B}^*} \right)^{\mathsf{T}} [\mathbf{v}]_{\mathcal{B}} = \left( [g]_{\mathcal{C}^*} \right)^{\mathsf{T}} [\mathbf{v}]_{\mathcal{C}}
$$
将 $[\mathbf{v}]_{\mathcal{C}} = P_{\mathcal{C} \leftarrow \mathcal{B}} [\mathbf{v}]_{\mathcal{B}}$ 代入上式右侧，我们得到：
$$
\left( [g]_{\mathcal{B}^*} \right)^{\mathsf{T}} [\mathbf{v}]_{\mathcal{B}} = \left( [g]_{\mathcal{C}^*} \right)^{\mathsf{T}} P_{\mathcal{C} \leftarrow \mathcal{B}} [\mathbf{v}]_{\mathcal{B}}
$$
由于这个等式对所有向量 $\mathbf{v}$ 都成立，因此系数必须相等：
$$
\left( [g]_{\mathcal{B}^*} \right)^{\mathsf{T}} = \left( [g]_{\mathcal{C}^*} \right)^{\mathsf{T}} P_{\mathcal{C} \leftarrow \mathcal{B}}
$$
对整个方程取转置，我们得到：
$$
[g]_{\mathcal{B}^*} = (P_{\mathcal{C} \leftarrow \mathcal{B}})^{\mathsf{T}} [g]_{\mathcal{C}^*}
$$
这个公式告诉我们如何将 $\mathcal{C}^*$-坐标转换到 $\mathcal{B}^*$-坐标。我们通常更关心从 $\mathcal{B}^*$ 到 $\mathcal{C}^*$ 的转换，这可以通过求解 $[g]_{\mathcal{C}^*}$ 得到：
$$
[g]_{\mathcal{C}^*} = \left( (P_{\mathcal{C} \leftarrow \mathcal{B}})^{\mathsf{T}} \right)^{-1} [g]_{\mathcal{B}^*} = \left( P_{\mathcal{C} \leftarrow \mathcal{B}}^{-1} \right)^{\mathsf{T}} [g]_{\mathcal{B}^*}
$$
因此，从 $\mathcal{B}^*$ 到 $\mathcal{C}^*$ 的坐标转换矩阵是 $Q_{\mathcal{C}^* \leftarrow \mathcal{B}^*} = ( P_{\mathcal{C} \leftarrow \mathcal{B}}^{-1} )^{\mathsf{T}}$ [@problem_id:1351891]。这个结果揭示了[向量空间](@entry_id:151108)与其对偶空间之间深刻而优美的对称性，展示了[基变换](@entry_id:189626)理论的广泛适用性。