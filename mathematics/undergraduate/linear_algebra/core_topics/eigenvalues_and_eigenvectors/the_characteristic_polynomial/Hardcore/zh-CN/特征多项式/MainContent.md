## 引言
在线性代数的学习中，特征值与特征向量是理解线性变换几何本质的核心概念。它们描述了在变换作用下保持方向不变的“特殊”向量。然而，一个根本性的问题随之而来：对于一个给定的方阵，我们如何系统性地找出它所有的特征值？答案就蕴藏在一个名为**特征多项式 (Characteristic Polynomial)** 的强大代数工具之中。

本文将带领你深入探索特征多项式的世界。我们不仅要揭示它如何将寻找特征值的几何问题转化为求解多项式方程的代数问题，还将展示其自身所蕴含的丰富信息。通过本文的学习，你将能够：

1.  在 **“原理与机制”** 一章中，掌握特征多项式的定义，理解其系数与矩阵的迹、行列式等不变量的深刻联系，并学习凯莱-哈密顿定理等核心理论。
2.  在 **“应用与交叉学科联系”** 一章中，见证特征多项式如何作为桥梁，连接抽象代数与具体问题，在几何分析、控制理论、图谱论乃至机器学习等多个领域发光发热。
3.  在 **“动手实践”** 一章中，通过精选的练习题，将理论知识转化为解决实际问题的能力。

从基本定义到前沿应用，本文旨在为你构建一个关于特征多项式的完整知识框架，让你不仅学会如何计算，更能深刻理解其为何重要。

## 原理与机制

在上一章中，我们引入了特征值和特征向量的概念，它们揭示了线性变换在特定方向上的基本作用。一个核心问题是：如何系统地找到一个给定矩阵的所有特征值？本章将深入探讨这一问题的答案，它蕴含于一个被称为**特征多项式 (characteristic polynomial)** 的强大代数工具之中。我们将详细阐述其定义、基本性质，并揭示它与矩阵的迹、行列式等不变量之间的深刻联系。此外，我们还将探索特征多项式在矩阵变换和高级理论（如凯莱-哈密顿定理）中的关键作用。

### 特征多项式的定义

我们从特征值的基本定义出发：一个标量 $\lambda$ 是方阵 $A$ 的特征值，当且仅当存在一个非零向量 $\mathbf{x}$，使得：
$$ A\mathbf{x} = \lambda\mathbf{x} $$

为了求解 $\lambda$，我们将该方程重写为：
$$ A\mathbf{x} - \lambda\mathbf{x} = \mathbf{0} $$
$$ (A - \lambda I)\mathbf{x} = \mathbf{0} $$

其中 $I$ 是与 $A$ 相同维度的单位矩阵。这个方程是一个齐次线性方程组。根据线性代数的基本理论，要使该方程存在非零解 $\mathbf{x}$（即特征向量），其系数矩阵 $(A - \lambda I)$ 必须是奇异的 (singular)。一个方阵是奇异的，当且仅当其行列式为零。因此，特征值 $\lambda$ 必须满足以下方程：
$$ \det(A - \lambda I) = 0 $$

这个方程被称为**特征方程 (characteristic equation)**。左侧的表达式 $\det(A - \lambda I)$ 是一个关于变量 $\lambda$ 的多项式，我们将其定义为矩阵 $A$ 的**特征多项式**，记作 $p(\lambda)$ 或 $p_A(\lambda)$。

**定义：** 对于一个 $n \times n$ 矩阵 $A$，其特征多项式 $p(\lambda)$ 定义为：
$$ p(\lambda) = \det(A - \lambda I) $$

特征值正是特征多项式的根。这意味着，寻找一个矩阵的特征值等价于求解一个多项式方程。

在一些文献中，特征多项式可能被定义为 $c(\lambda) = \det(\lambda I - A)$。这两种定义本质上是等价的，因为 $\det(\lambda I - A) = \det(-1 \cdot (A - \lambda I)) = (-1)^n \det(A - \lambda I) = (-1)^n p(\lambda)$。因此，这两个多项式仅相差一个常数因子 $(-1)^n$，它们的根（即特征值）是完全相同的。在本文中，我们主要采用 $p(\lambda) = \det(A - \lambda I)$ 的定义。

让我们来考察这个多项式的一般形式。考虑一个 $n \times n$ 矩阵 $A - \lambda I$：
$$
A - \lambda I = \begin{pmatrix}
a_{11} - \lambda & a_{12} & \dots & a_{1n} \\
a_{21} & a_{22} - \lambda & \dots & a_{2n} \\
\vdots & \vdots & \ddots & \vdots \\
a_{n1} & a_{n2} & \dots & a_{nn} - \lambda
\end{pmatrix}
$$

根据行列式的莱布尼兹展开式，$\det(A - \lambda I)$ 是由矩阵元素乘积组成的和。其中，包含 $\lambda$ 的最高次项只能来自对角线元素的乘积，即 $(a_{11} - \lambda)(a_{22} - \lambda)\cdots(a_{nn} - \lambda)$。展开此项，$\lambda$ 的最高次幂项为 $(-\lambda)^n = (-1)^n \lambda^n$。任何其他乘积项最多只包含 $n-2$ 个对角元素，因此其 $\lambda$ 的次数严格小于 $n$。这意味着它们不会影响 $\lambda^n$ 的系数。

因此，我们得到了特征多项式的两个基本属性 [@problem_id:1393355]：
1.  对于一个 $n \times n$ 矩阵 $A$，其特征多项式 $p(\lambda)$ 的**次数 (degree)** 恒为 $n$。
2.  其**首项系数 (leading coefficient)**，即 $\lambda^n$ 的系数，恒为 $(-1)^n$。

### 特征多项式的系数：迹与行列式

特征多项式的魅力不仅在于它的根是特征值，它的系数本身也编码了矩阵的基本不变量，特别是**迹 (trace)** 和**行列式 (determinant)**。

让我们将 $n \times n$ 矩阵 $A$ 的特征多项式写成一般形式：
$$ p(\lambda) = (-1)^n \lambda^n + c_{n-1} \lambda^{n-1} + \dots + c_1 \lambda + c_0 $$

首先考虑常数项 $c_0$。通过在多项式中令 $\lambda = 0$ 得到：
$$ c_0 = p(0) = \det(A - 0 \cdot I) = \det(A) $$
这表明，**特征多项式的常数项等于矩阵的行列式**。

例如，如果一个 $4 \times 4$ 矩阵 $B$ 的特征多项式由 $\det(\lambda I - B)$ 定义，并给出为 $p(\lambda) = \lambda^4 - 2\lambda^3 + 5\lambda - 15$，我们可以立即求出其行列式。根据 $p(\lambda) = \det(\lambda I - B)$，我们有 $p(0) = \det(-B) = (-1)^4 \det(B) = \det(B)$。因此，$\det(B) = p(0) = -15$ [@problem_id:1393367]。

接下来，我们考察 $\lambda^{n-1}$ 项的系数。通过更仔细地分析行列式的展开，可以证明该项的系数与矩阵对角线元素之和（即迹）有关。对于 $p(\lambda) = \det(A - \lambda I)$，$\lambda^{n-1}$ 的系数 $c_{n-1}$ 等于 $(-1)^{n-1} \text{tr}(A)$。其中 $\text{tr}(A) = \sum_{i=1}^n a_{ii}$。

这一关系非常实用。例如，给定一个 $3 \times 3$ 矩阵 $A$ 的特征多项式为 $p(\lambda) = 1 - 7\lambda + 4\lambda^2 - \lambda^3$。我们可以将其与标准形式 $p(\lambda) = -\lambda^3 + (\text{tr}A)\lambda^2 - s_2\lambda + \det A$ 进行比较（这里 $n=3$，所以 $(-1)^{3-1}=1$）。通过比较 $\lambda^2$ 的系数，我们直接得到 $\text{tr}(A) = 4$ [@problem_id:1393321]。

这些系数与特征值之间也存在着深刻的联系，这由韦达定理 (Viète's formulas) 揭示。如果 $\lambda_1, \lambda_2, \dots, \lambda_n$ 是矩阵 $A$ 的特征值（即 $p(\lambda)$ 的根），那么：
$$ \sum_{i=1}^n \lambda_i = \text{tr}(A) $$
$$ \prod_{i=1}^n \lambda_i = \det(A) $$

这两个关系为我们提供了一种强大的工具来验证计算或推断信息。例如，假设我们知道一个 $3 \times 3$ 线性算子 $T$ 的特征多项式为 $p(\lambda) = -\lambda^3 + 9\lambda^2 - 20\lambda + 12$，并且已经知道其两个特征值为 $1$ 和 $6$。我们可以利用迹的关系来找到第三个特征值 $\lambda_3$。从多项式中我们可知 $\text{tr}(T) = 9$。因此，$1 + 6 + \lambda_3 = 9$，解得 $\lambda_3 = 2$。现在我们知道了所有特征值：$1, 2, 6$。于是，该算子的行列式就是所有特征值的乘积：$\det(T) = 1 \cdot 2 \cdot 6 = 12$。我们也可以通过检查多项式的常数项来验证这一点：$p(0) = 12$，这与我们的计算结果一致 [@problem_id:1393343]。

### 特征多项式的性质与变换

特征多项式在各种矩阵变换下表现出优雅而可预测的行为。理解这些性质对于理论分析和实际计算都至关重要。

**相似变换**：如果矩阵 $B$ 与 $A$ 相似，即存在可逆矩阵 $P$ 使得 $B = P^{-1}AP$，那么它们具有相同的特征多项式。
$$
p_B(\lambda) = \det(B - \lambda I) = \det(P^{-1}AP - \lambda P^{-1}IP) = \det(P^{-1}(A - \lambda I)P)
$$
$$
= \det(P^{-1}) \det(A - \lambda I) \det(P) = \det(A - \lambda I) = p_A(\lambda)
$$
这一性质至关重要，因为它意味着特征值是矩阵的内在属性，不随坐标系的改变而改变。

**转置**：一个矩阵和它的转置矩阵拥有相同的特征多项式。这是因为矩阵的行列式等于其转置的行列式。
$$
p_{A^T}(\lambda) = \det(A^T - \lambda I) = \det(A^T - (\lambda I)^T) = \det((A - \lambda I)^T) = \det(A - \lambda I) = p_A(\lambda)
$$

**标量变换**：对矩阵进行标量平移和缩放会以一种可预测的方式改变其特征多项式。
-   **平移 (Shift)**：考虑矩阵 $B = A - kI$。它的特征多项式为：
    $$ p_B(\lambda) = \det(B - \lambda I) = \det((A - kI) - \lambda I) = \det(A - (\lambda + k)I) = p_A(\lambda + k) $$
    这意味着矩阵 $A-kI$ 的特征值是 $A$ 的特征值减去 $k$，这直观上是合理的 [@problem_id:1393304]。

-   **复合变换**：我们可以组合这些性质来分析更复杂的变换。例如，考虑矩阵 $B = k A^T + c I$，其中 $k, c$ 是非零标量。其特征多项式 $p_B(\mu)$ 可以表示为：
    $$
    p_B(\mu) = \det(B - \mu I) = \det(k A^T + c I - \mu I) = \det(k A^T - (\mu - c)I)
    $$
    利用行列式的性质 $\det(\alpha M) = \alpha^n \det(M)$，我们提出因子 $k$：
    $$
    p_B(\mu) = k^n \det\left(A^T - \frac{\mu - c}{k} I\right)
    $$
    由于转置不改变特征多项式，这等于：
    $$
    p_B(\mu) = k^n p_{A^T}\left(\frac{\mu - c}{k}\right) = k^n p_A\left(\frac{\mu - c}{k}\right)
    $$
    这个结果优美地将 $B$ 的特征多项式与 $A$ 的特征多项式联系起来 [@problem_id:1393319]。

-   **逆矩阵 (Inverse)**：如果矩阵 $A$ 可逆，其特征值为 $\lambda_1, \dots, \lambda_n$（均非零），那么 $A^{-1}$ 的特征值为 $1/\lambda_1, \dots, 1/\lambda_n$。$A^{-1}$ 的特征多项式与 $A$ 的特征多项式之间也存在一个确定的关系。使用 $c(t) = \det(tI - M)$ 的定义，可以推导出：
    $$
    c_{A^{-1}}(t) = \frac{(-t)^n}{\det(A)} c_A\left(\frac{1}{t}\right)
    $$
    例如，如果一个可逆 $3 \times 3$ 矩阵 $A$ 的特征多项式为 $c_A(t) = t^3 - 7t^2 + 14t - 8$，我们知道 $\det(A) = -c_A(0) = 8$。利用上述公式，可以计算出 $A^{-1}$ 的特征多项式为 $c_{A^{-1}}(t) = t^3 - \frac{7}{4}t^2 + \frac{7}{8}t - \frac{1}{8}$ [@problem_id:1393346]。

### 凯莱-哈密顿定理

特征多项式最令人惊叹的性质之一是**凯莱-哈密顿定理 (Cayley-Hamilton Theorem)**。该定理指出，任何方阵都满足其自身的特征方程。

**定理 (Cayley-Hamilton)：** 如果 $p(\lambda) = c_n \lambda^n + \dots + c_1 \lambda + c_0$ 是矩阵 $A$ 的特征多项式，那么将 $\lambda$ 替换为矩阵 $A$ 会得到零矩阵：
$$ p(A) = c_n A^n + \dots + c_1 A + c_0 I = \mathbf{0} $$
注意，常数项 $c_0$ 被替换为 $c_0 I$。

这个定理提供了一种计算矩阵高次幂的有效方法，因为它建立了一个 $n$ 次的矩阵多项式关系，可以将任何高于 $n-1$ 次的 $A$ 的幂降解为 $A$ 的低次幂的线性组合。

让我们通过一个离散动力系统的例子来感受其威力 [@problem_id:1393332]。一个系统的状态由 $\mathbf{x}_{k+1} = A \mathbf{x}_k$ 描述，其中 $A = \begin{pmatrix} 5 & 1 \\ -2 & 2 \end{pmatrix}$。我们需要计算一个性能向量 $\mathbf{y} = \mathbf{x}_2 - 7\mathbf{x}_1 + 13\mathbf{x}_0$。

一种方法是直接计算：从 $\mathbf{x}_0$ 出发，计算出 $\mathbf{x}_1$ 和 $\mathbf{x}_2$，然后代入表达式。然而，我们可以使用凯莱-哈密顿定理来简化问题。首先，计算 $A$ 的特征多项式：
$$
p(\lambda) = \det(A - \lambda I) = \det\begin{pmatrix} 5-\lambda & 1 \\ -2 & 2-\lambda \end{pmatrix} = (5-\lambda)(2-\lambda) - (-2) = \lambda^2 - 7\lambda + 12
$$
根据凯莱-哈密顿定理，$p(A) = A^2 - 7A + 12I = \mathbf{0}$。现在我们来处理表达式 $\mathbf{y}$：
$$
\mathbf{y} = \mathbf{x}_2 - 7\mathbf{x}_1 + 13\mathbf{x}_0 = A^2\mathbf{x}_0 - 7A\mathbf{x}_0 + 13I\mathbf{x}_0 = (A^2 - 7A + 13I)\mathbf{x}_0
$$
我们可以将括号内的矩阵多项式重写为：
$$
A^2 - 7A + 13I = (A^2 - 7A + 12I) + I
$$
由于 $A^2 - 7A + 12I = \mathbf{0}$，上式简化为 $\mathbf{0} + I = I$。因此：
$$
\mathbf{y} = I \mathbf{x}_0 = \mathbf{x}_0
$$
如果初始状态是 $\mathbf{x}_0 = \begin{pmatrix} 3 \\ -1 \end{pmatrix}$，那么性能向量就是 $\mathbf{y} = \begin{pmatrix} 3 \\ -1 \end{pmatrix}$。这个优雅的解法完全避免了复杂的矩阵乘法，凸显了凯莱-哈密顿定理的理论力量和计算优势。

### 特征多项式能告诉我们什么，不能告诉我们什么

总结一下，一个矩阵的特征多项式是一个信息宝库。通过分析它，我们可以唯一地确定 [@problem_id:1393372]：

1.  **特征值 (Eigenvalues)**：它们是多项式的根。
2.  **行列式 (Determinant)**：等于多项式的常数项 $p(0)$。
3.  **迹 (Trace)**：与 $\lambda^{n-1}$ 的系数直接相关。
4.  **可对角化性 (Diagonalizability) 的部分信息**：如果一个 $n \times n$ 矩阵的特征多项式有 $n$ 个不同的实数根，那么该矩阵在实数域上是可对角化的。

然而，特征多项式并非万能。一个至关重要的信息是它**无法唯一确定**的：

-   **特征向量 (Eigenvectors)**：特征多项式相同（即特征值相同）的矩阵可以有完全不同的特征向量。例如，所有与对角矩阵 $D$ 相似的矩阵 $A = P^{-1}DP$ 都具有与 $D$ 相同的特征多项式，但它们的特征向量依赖于变换矩阵 $P$。因此，仅凭特征多项式，我们无法重建矩阵的完整几何结构。

### 高级主题：不变子空间与商空间

特征多项式的概念可以推广到更抽象的线性算子和向量空间。一个特别深刻的结果涉及**不变子空间 (invariant subspace)**。

设 $T: V \to V$ 是一个线性算子， $W$ 是 $V$ 的一个子空间。如果对于所有 $\mathbf{w} \in W$，都有 $T(\mathbf{w}) \in W$，那么我们称 $W$ 是 **$T$-不变的**。

当 $W$ 是一个 $T$-不变子空间时，我们可以定义两个新的算子：
1.  **限制算子 (Restriction Operator)** $T|_W: W \to W$，其定义为 $T|_W(\mathbf{w}) = T(\mathbf{w})$。
2.  **诱导算子 (Induced Operator)** $\bar{T}: V/W \to V/W$，作用于商空间 $V/W$（由形如 $\mathbf{v} + W$ 的陪集构成），其定义为 $\bar{T}(\mathbf{v} + W) = T(\mathbf{v}) + W$。

这三个算子 $T, T|_W, \bar{T}$ 的特征多项式之间存在一个美妙的关系：
$$ \chi_T(\lambda) = \chi_{T|_W}(\lambda) \cdot \chi_{\bar{T}}(\lambda) $$
这里我们使用 $\chi(\lambda)$ 符号以强调这是一般算子的特征多项式。

这个定理在理论上非常重要，因为它将一个复杂算子的谱（特征值集合）分解为更小子空间上的算子谱的组合。它也提供了一个强大的计算工具。

例如，考虑作用于三次多项式空间 $V = P_3(\mathbb{R})$ 的微分算子 $T(p(x)) = (x^2-1)p''(x) + (2x+1)p'(x)$ [@problem_id:1393331]。可以验证，一次多项式子空间 $W = P_1(\mathbb{R})$ 是 $T$-不变的。如果我们想求诱导算子 $\bar{T}$ 在商空间 $V/W$ 上的特征多项式，直接计算会很繁琐。但利用上述定理，我们可以通过计算 $\chi_T(\lambda)$ 和 $\chi_{T|_W}(\lambda)$，然后做多项式除法来得到：
$$ \chi_{\bar{T}}(\lambda) = \frac{\chi_T(\lambda)}{\chi_{T|_W}(\lambda)} $$
通过在合适的基下计算 $T$ 和 $T|_W$ 的矩阵表示，我们可以得到：
-   $\chi_T(\lambda) = \lambda(\lambda-2)(6-\lambda)(12-\lambda)$
-   $\chi_{T|_W}(\lambda) = \lambda(\lambda-2)$

因此，诱导算子的特征多项式为：
$$ \chi_{\bar{T}}(\lambda) = \frac{\lambda(\lambda-2)(6-\lambda)(12-\lambda)}{\lambda(\lambda-2)} = (6-\lambda)(12-\lambda) = \lambda^2 - 18\lambda + 72 $$
这个例子展示了如何利用不变子空间的结构来简化特征多项式的计算，揭示了线性算子更深层次的代数结构。