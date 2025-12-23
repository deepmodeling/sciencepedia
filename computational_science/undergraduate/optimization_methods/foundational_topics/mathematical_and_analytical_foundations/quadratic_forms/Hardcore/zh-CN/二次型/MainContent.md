## 引言
二次型，作为变量的二次[齐次多项式](@entry_id:178156)，是线性代数中一个核心且优雅的概念。尽管其形式简洁，但它却是连接代数、几何与分析的强大桥梁，在从物理系统建模到现代数据科学的众多领域中扮演着不可或缺的角色。然而，许多学习者在掌握其基本定义后，往往难以深刻理解其内在结构与广泛应用的内在联系。本文旨在填补这一知识鸿沟，系统性地揭示二次型的理论精髓与实践价值。

在接下来的内容中，读者将踏上一段结构化的学习之旅。我们将通过三个章节来层层深入：在“原理与机制”中，您将掌握[二次型的矩阵](@entry_id:151206)表示、[正定性](@entry_id:149643)判别和[主轴定理](@entry_id:154703)等核心代数和几何工具；在“应用与交叉学科联系”中，您将看到这些理论如何在[优化问题](@entry_id:266749)、[几何分析](@entry_id:157700)、数值计算、工程控制和机器学习等真实场景中发挥关键作用；最后，“动手实践”部分将提供精选的练习，帮助您巩固理解并提升应用能力。

这个循序渐进的结构将确保您建立起对二次型全面而深刻的认识。现在，让我们从其最根本的“原理与机制”开始探索。

## 原理与机制

继前一章对二次型的初步介绍之后，本章将深入探讨其核心原理与内在机制。我们将从[二次型的矩阵](@entry_id:151206)表示法入手，揭示其与双线性型之间的深刻联系，并建立一套系统的分类方法。最终，我们将探讨这些理论在几何解释和[优化问题](@entry_id:266749)中的关键应用，展示二次型如何成为连接代数、几何与分析的桥梁。

### [二次型的矩阵](@entry_id:151206)表示

二次型是关于一组变量 $x_1, x_2, \dots, x_n$ 的二次[齐次多项式](@entry_id:178156)。任何一个这样的二次型 $q(\mathbf{x})$ 都可以用一种紧凑而强大的方式——[矩阵乘法](@entry_id:156035)来表示。如果我们把变量组织成一个列向量 $\mathbf{x} = [x_1, x_2, \dots, x_n]^T$，那么二次型可以写作：

$q(\mathbf{x}) = \mathbf{x}^T A \mathbf{x}$

其中，$A$ 是一个 $n \times n$ 的方阵，$\mathbf{x}^T$ 是 $\mathbf{x}$ 的[转置](@entry_id:142115)。虽然存在多个矩阵 $A$ 可以生成同一个二次型，但在整个线性代数和应用领域，我们几乎总是选择一个唯一的**[对称矩阵](@entry_id:143130)**来表示二次型。这种选择不仅是为了规范，更因为它能揭示二次型更深层次的几何与代数属性。

那么，如何从一个给定的多项式表达式找到这个唯一的对称矩阵 $A$ 呢？规则十分系统：

1.  平方项的系数：对于多项式中的 $x_i^2$ 项，其系数直接成为矩阵 $A$ 的对角线元素 $A_{ii}$。
2.  交叉项的系数：对于多项式中的[交叉](@entry_id:147634)项 $x_i x_j$（其中 $i \neq j$），其系数被均等地分配给矩阵中的两个对称位置 $A_{ij}$ 和 $A_{ji}$。也就是说，如果 $x_i x_j$ 的系数是 $c$，那么 $A_{ij} = A_{ji} = \frac{c}{2}$。

让我们通过一个三变量的通用例子来阐明这一点。考虑二次型 ：
$q(x_1, x_2, x_3) = a x_1^2 + b x_2^2 + c x_3^2 + d x_1 x_2 + e x_1 x_3 + f x_2 x_3$

根据上述规则，我们可以构建其对应的对称矩阵 $A$。
- 平方项 $ax_1^2, bx_2^2, cx_3^2$ 的系数 $a, b, c$ 构成了矩阵的主对角线。
- [交叉](@entry_id:147634)项 $dx_1x_2$ 的系数 $d$ 被平分，得到 $A_{12} = A_{21} = \frac{d}{2}$。
- [交叉](@entry_id:147634)项 $ex_1x_3$ 的系数 $e$ 被平分，得到 $A_{13} = A_{31} = \frac{e}{2}$。
- 交叉项 $fx_2x_3$ 的系数 $f$ 被平分，得到 $A_{23} = A_{32} = \frac{f}{2}$。

因此，对应的[对称矩阵](@entry_id:143130) $A$ 为：
$$
A = \begin{pmatrix} a & \frac{d}{2} & \frac{e}{2} \\ \frac{d}{2} & b & \frac{f}{2} \\ \frac{e}{2} & \frac{f}{2} & c \end{pmatrix}
$$
我们可以通过展开 $\mathbf{x}^T A \mathbf{x}$ 来验证这一点，结果将精确地还原为原始的 $q(x_1, x_2, x_3)$ 表达式。

在实践中，有时可能会遇到一个非对称的矩阵 $B$ 也能表示同一个二次型，即 $q(\mathbf{x}) = \mathbf{x}^T B \mathbf{x}$。例如，对于二次型 $q(x_1, x_2, x_3) = 5x_1^2 - 2x_2^2 + 8x_1x_3 - 6x_2x_3$，一个初学者可能会直接将[交叉](@entry_id:147634)项的系数放在一个非对角元素上，构造出[非对称矩阵](@entry_id:153254) $B = \begin{pmatrix} 5 & 0 & 8 \\ 0 & -2 & -6 \\ 0 & 0 & 0 \end{pmatrix}$ 。尽管 $\mathbf{x}^T B \mathbf{x}$ 确实等于给定的 $q(\mathbf{x})$，但这个表示不是标准的。为了得到唯一的对称表示 $A$，我们可以利用一个简单的“对称化”技巧。对于任何方阵 $M$，$\mathbf{x}^T M \mathbf{x}$ 的值都等于 $\mathbf{x}^T M^T \mathbf{x}$ 的值（因为它们都是标量，互为转置）。因此，$\mathbf{x}^T M \mathbf{x} = \frac{1}{2}(\mathbf{x}^T M \mathbf{x} + \mathbf{x}^T M^T \mathbf{x}) = \mathbf{x}^T \left(\frac{M+M^T}{2}\right) \mathbf{x}$。矩阵 $\frac{M+M^T}{2}$ 是一个[对称矩阵](@entry_id:143130)。将这个技巧应用于矩阵 $B$，我们就能找到唯一的[对称矩阵](@entry_id:143130) $A$：
$$
A = \frac{B+B^T}{2} = \frac{1}{2} \left( \begin{pmatrix} 5 & 0 & 8 \\ 0 & -2 & -6 \\ 0 & 0 & 0 \end{pmatrix} + \begin{pmatrix} 5 & 0 & 0 \\ 0 & -2 & 0 \\ 8 & -6 & 0 \end{pmatrix} \right) = \begin{pmatrix} 5 & 0 & 4 \\ 0 & -2 & -3 \\ 4 & -3 & 0 \end{pmatrix}
$$
这个结果与我们直接使用系数分配规则得到的结果完全一致。

### 与双线性型的联系：[极化恒等式](@entry_id:271819)

二次型与另一个重要的数学对象——**双线性型 (bilinear form)** 密切相关。双线性型是一个函数 $B: V \times V \to \mathbb{R}$，它在每个参数上都是线性的。也就是说，对于任意向量 $\mathbf{u}, \mathbf{v}, \mathbf{w}$ 和标量 $c$，满足：
$B(\mathbf{u}+\mathbf{v}, \mathbf{w}) = B(\mathbf{u}, \mathbf{w}) + B(\mathbf{v}, \mathbf{w})$
$B(c\mathbf{u}, \mathbf{v}) = cB(\mathbf{u}, \mathbf{v})$
（对第二个参数同样成立）。

如果一个双线性型还满足 $B(\mathbf{u}, \mathbf{v}) = B(\mathbf{v}, \mathbf{u})$，则称之为**对称[双线性](@entry_id:146819)型**。

二次型与对称[双线性](@entry_id:146819)型之间存在一一对应的关系。任何一个二次型 $q(\mathbf{v})$ 都可以通过在一个对称双线性型 $B$ 中令两个输入向量相等得到，即 $q(\mathbf{v}) = B(\mathbf{v}, \mathbf{v})$。反过来，给定一个二次型 $q$，我们如何找回它所对应的那个唯一的对称双线性型 $B$ 呢？答案是**[极化恒等式](@entry_id:271819) (polarization identity)**。

让我们从展开 $q(\mathbf{u}+\mathbf{v})$ 开始。假设 $q(\mathbf{x}) = \mathbf{x}^T A \mathbf{x}$，其中 $A$ 是[对称矩阵](@entry_id:143130)。那么对应的[双线性](@entry_id:146819)型是 $B(\mathbf{u}, \mathbf{v}) = \mathbf{u}^T A \mathbf{v}$。我们有：
$q(\mathbf{u}+\mathbf{v}) = (\mathbf{u}+\mathbf{v})^T A (\mathbf{u}+\mathbf{v}) = (\mathbf{u}^T + \mathbf{v}^T) A (\mathbf{u}+\mathbf{v})$
$= \mathbf{u}^T A \mathbf{u} + \mathbf{u}^T A \mathbf{v} + \mathbf{v}^T A \mathbf{u} + \mathbf{v}^T A \mathbf{v}$

因为 $A$ 是对称的（$A=A^T$），所以 $\mathbf{v}^T A \mathbf{u}$ 是一个标量，它的转置等于它自身：$(\mathbf{v}^T A \mathbf{u})^T = \mathbf{u}^T A^T \mathbf{v} = \mathbf{u}^T A \mathbf{v}$。因此 $\mathbf{v}^T A \mathbf{u} = \mathbf{u}^T A \mathbf{v}$，即 $B(\mathbf{v}, \mathbf{u}) = B(\mathbf{u}, \mathbf{v})$。于是上式可以写为：
$q(\mathbf{u}+\mathbf{v}) = q(\mathbf{u}) + q(\mathbf{v}) + 2B(\mathbf{u}, \mathbf{v})$

这个关系式是二次型版本的[二项式展开](@entry_id:269603)，它清楚地展示了 $q(\mathbf{u}+\mathbf{v})$、 $q(\mathbf{u})$、 $q(\mathbf{v})$ 以及相关的[双线性](@entry_id:146819)型之间的联系 。通过移项，我们就能得到[极化恒等式](@entry_id:271819)：
$$
B(\mathbf{x}, \mathbf{y}) = \frac{1}{2} (q(\mathbf{x}+\mathbf{y}) - q(\mathbf{x}) - q(\mathbf{y}))
$$
这个公式允许我们从任何二次型 $q$ 出发，唯一地确定其背后的对称双线性型 $B$。例如，给定二次型 $q(\mathbf{v}) = 5v_1^2 - v_2^2 + 2v_1v_2$ ，我们可以使用[极化恒等式](@entry_id:271819)来找到对应的 $B(\mathbf{x}, \mathbf{y})$。通过代数计算，可以得到：
$B(\mathbf{x}, \mathbf{y}) = 5x_1y_1 + x_1y_2 + x_2y_1 - x_2y_2$
另一种更快捷的方法是先写出 $q$ 的对称矩阵 $A = \begin{pmatrix} 5 & 1 \\ 1 & -1 \end{pmatrix}$，然后直接计算 $B(\mathbf{x}, \mathbf{y}) = \mathbf{x}^T A \mathbf{y}$，这会得到相同的结果。

### 二次型的分类：定性

二次型最重要的特性之一是其值的符号。给定一个二次型 $q(\mathbf{x})$，它的值是总是正的、总是负的，还是有正有负？这引出了二次型的**定性 (definiteness)** 分类，这个分类对于理解二次型的几何形状以及在优化中的应用至关重要。

-   **正定 (Positive definite)**: 对所有非[零向量](@entry_id:156189) $\mathbf{x} \neq \mathbf{0}$，都有 $q(\mathbf{x}) > 0$。
-   **负定 (Negative definite)**: 对所有非[零向量](@entry_id:156189) $\mathbf{x} \neq \mathbf{0}$，都有 $q(\mathbf{x}) < 0$。
-   **不定 (Indefinite)**: $q(\mathbf{x})$ 既能取到正值也能取到负值。
-   **半正定 (Positive semi-definite)**: 对所有向量 $\mathbf{x}$，都有 $q(\mathbf{x}) \ge 0$。
-   **半负定 (Negative semi-definite)**: 对所有向量 $\mathbf{x}$，都有 $q(\mathbf{x}) \le 0$。

注意，正定二次型一定是半正定的，但反之不成立。一个二次型是“半正定但非正定”，意味着它总是非负，但存在某个非[零向量](@entry_id:156189) $\mathbf{x}_0$ 使得 $q(\mathbf{x}_0) = 0$。

考虑一个例子 ：$q(\mathbf{x}) = (x_1 - 2x_2)^2 + (3x_2 - x_3)^2$。
这个表达式是两个平方项之和，因此 $q(\mathbf{x})$ 的值永远不会是负数，即 $q(\mathbf{x}) \ge 0$ 对所有 $\mathbf{x}$ 成立。这表明该二次型至少是半正定的。
它是否是正定的呢？我们需要检查是否存在非零向量 $\mathbf{x}$ 使得 $q(\mathbf{x})=0$。$q(\mathbf{x})=0$ 的条件是两个平方项同时为零：
$x_1 - 2x_2 = 0$
$3x_2 - x_3 = 0$
这个线性方程组定义了一条穿过原点的直线。例如，令 $x_2=1$，我们可以解得 $x_1=2, x_3=3$。向量 $\mathbf{x}_0 = (2, 1, 3)$ 是一个非[零向量](@entry_id:156189)，但 $q(\mathbf{x}_0)=0$。因此，该二次型不是正定的。它的正确分类是**半正定但非正定**。

### [特征值](@entry_id:154894)判据

二次型的定性[分类问题](@entry_id:637153)有一个极其优美的代数判据，它完全由其[对称矩阵](@entry_id:143130) $A$ 的**[特征值](@entry_id:154894) (eigenvalues)** 决定。由于 $A$ 是对称矩阵，它的所有[特征值](@entry_id:154894)都是实数。

**定性与[特征值](@entry_id:154894)符号的对应关系：**

-   **正定** $\iff$ $A$ 的所有[特征值](@entry_id:154894)都大于 $0$。
-   **负定** $\iff$ $A$ 的所有[特征值](@entry_id:154894)都小于 $0$。
-   **不定** $\iff$ $A$ 至少有一个正[特征值](@entry_id:154894)和一个负[特征值](@entry_id:154894)。
-   **半正定** $\iff$ $A$ 的所有[特征值](@entry_id:154894)都大于等于 $0$（且至少有一个为零才不是正定）。
-   **半负定** $\iff$ $A$ 的所有[特征值](@entry_id:154894)都小于等于 $0$（且至少有一个为零才不是负定）。

这个判据为我们提供了一个纯粹的计算方法来确定二次型的定性。例如，如果一个 $2 \times 2$ 对称矩阵 $A$ 的[特征多项式](@entry_id:150909)为 $p(\lambda) = \lambda^2 + \lambda - 6$ ，我们可以通过求解 $p(\lambda) = (\lambda+3)(\lambda-2) = 0$ 来找到其[特征值](@entry_id:154894)。[特征值](@entry_id:154894)为 $\lambda_1 = 2$ 和 $\lambda_2 = -3$。由于存在一正一负两个[特征值](@entry_id:154894)，与该矩阵关联的二次型 $q(\mathbf{x}) = \mathbf{x}^T A \mathbf{x}$ 是**不定**的。

对于低维（特别是 $2 \times 2$）矩阵，我们甚至不需要直接计算[特征值](@entry_id:154894)。我们可以利用矩阵的**迹 (trace)** 和**[行列式](@entry_id:142978) (determinant)**，因为它们与[特征值](@entry_id:154894)有简单的关系：$\text{tr}(A) = \sum \lambda_i$ 和 $\det(A) = \prod \lambda_i$。对于一个 $2 \times 2$ 对称矩阵，我们可以使用以下快捷判据 ：

-   $\det(A) > 0$ 且 $\text{tr}(A) > 0 \implies \lambda_1, \lambda_2 > 0 \implies$ **正定**。
-   $\det(A) > 0$ 且 $\text{tr}(A) < 0 \implies \lambda_1, \lambda_2 < 0 \implies$ **负定**。
-   $\det(A) < 0 \implies \lambda_1, \lambda_2$ 异号 $\implies$ **不定**。
-   $\det(A) = 0 \implies$ 至少一个[特征值](@entry_id:154894)为零 $\implies$ **半定**（具体是半正定还是半负定由迹的符号决定，若迹为正则半正定，为负则半负定）。

### 几何解释：[主轴定理](@entry_id:154703)

[特征值](@entry_id:154894)判据之所以有效，根植于二次型的几何意义。**[主轴定理](@entry_id:154703) (Principal Axes Theorem)** 是沟通二次型代数形式与几何形状的核心。该定理指出，对于任意二次型 $q(\mathbf{x}) = \mathbf{x}^T A \mathbf{x}$，总能找到一个**[正交坐标](@entry_id:166074)变换** $\mathbf{x} = P\mathbf{y}$，将[二次型对角化](@entry_id:180341)，消除所有的[交叉](@entry_id:147634)项。

在这个变换下，二次型在新[坐标系](@entry_id:156346) $\{y_i\}$ 中呈现为一个简单的平方和形式：
$q(\mathbf{y}) = \mathbf{y}^T (P^T A P) \mathbf{y} = \mathbf{y}^T D \mathbf{y} = \lambda_1 y_1^2 + \lambda_2 y_2^2 + \dots + \lambda_n y_n^2$

这里的构成要素是：
-   $P$ 是一个**正交矩阵**（$P^T P = I$），它的列向量是矩阵 $A$ 的一组标准[正交特征向量](@entry_id:155522)。
-   $D$ 是一个[对角矩阵](@entry_id:637782)，其对角线上的元素 $\lambda_1, \dots, \lambda_n$ 正是矩阵 $A$ 的[特征值](@entry_id:154894)。

这个变换在几何上对应于对原[坐标系](@entry_id:156346)的一次旋转（或反射），使得新坐标轴（称为**主轴**）恰好对齐二次型等高线的[对称轴](@entry_id:177299)。例如，在二维空间中，如果 $q(x_1, x_2) = c$ 的等高线是一个椭圆，那么[主轴](@entry_id:172691)就是这个椭圆的长轴和短轴方向。[特征值](@entry_id:154894) $\lambda_i$ 的大小决定了在第 $i$ 个主轴方向上[曲面](@entry_id:267450)的“陡峭”程度。

考虑二次型 $q(x_1, x_2) = x_1^2 + 8x_1x_2 + x_2^2$ 。其[对称矩阵](@entry_id:143130)为 $A = \begin{pmatrix} 1 & 4 \\ 4 & 1 \end{pmatrix}$。
我们已经知道其[特征值](@entry_id:154894)为 $\lambda_1 = 5$ 和 $\lambda_2 = -3$。对应的标准[正交特征向量](@entry_id:155522)（满足特定方向和[行列式](@entry_id:142978)约束）可以求得为 $\mathbf{p}_1 = \frac{1}{\sqrt{2}}\begin{pmatrix} 1 \\ 1 \end{pmatrix}$ 和 $\mathbf{p}_2 = \frac{1}{\sqrt{2}}\begin{pmatrix} -1 \\ 1 \end{pmatrix}$。
构建[正交矩阵](@entry_id:169220) $P = [\mathbf{p}_1 \ \mathbf{p}_2] = \frac{1}{\sqrt{2}}\begin{pmatrix} 1 & -1 \\ 1 & 1 \end{pmatrix}$。通过坐标变换 $\mathbf{x} = P\mathbf{y}$，原二次型被转化为：
$q(y_1, y_2) = 5y_1^2 - 3y_2^2$
这个形式非常直观：沿着 $\mathbf{p}_1$ 方向（新的 $y_1$ 轴），二次型呈抛物线开口向上；而沿着 $\mathbf{p}_2$ 方向（新的 $y_2$ 轴），它呈抛物线开口向下。这正是“不定”二次型（马鞍面）的典型特征。

### 在[优化问题](@entry_id:266749)中的应用

二次型的理论在优化领域扮演着至关重要的角色，无论是[约束优化](@entry_id:635027)还是[无约束优化](@entry_id:137083)。

#### 约束优化与瑞利商

一个经典问题是：在[单位球](@entry_id:142558)（或单位圆）上，一个二次型 $q(\mathbf{x})$ 能达到的最大值和最小值是多少？这个问题在物理学的[应力分析](@entry_id:168804)、[振动分析](@entry_id:146266)等领域很常见。例如，一个晶体在单位形变下的[应变能密度](@entry_id:200085)可以用二次型 $U(\mathbf{x})$ 表示，我们关心的是能量的最大值 。

这个问题的答案由**[瑞利商](@entry_id:137794) (Rayleigh Quotient)** 给出。对于对称矩阵 $A$，其[瑞利商](@entry_id:137794)定义为 $R_A(\mathbf{x}) = \frac{\mathbf{x}^TA\mathbf{x}}{\mathbf{x}^T\mathbf{x}}$。一个非凡的结论是：
-   [瑞利商](@entry_id:137794) $R_A(\mathbf{x})$ 的**最大值**等于矩阵 $A$ 的**最大[特征值](@entry_id:154894)** $\lambda_{\max}$。
-   瑞利商 $R_A(\mathbf{x})$ 的**最小值**等于矩阵 $A$ 的**[最小特征值](@entry_id:177333)** $\lambda_{\min}$。

当我们将 $\mathbf{x}$ 限制在单位球上时（$\mathbf{x}^T\mathbf{x} = \|\mathbf{x}\|^2 = 1$），$q(\mathbf{x}) = R_A(\mathbf{x})$。因此，**二次型 $q(\mathbf{x})$ 在单位球上的最大值就是 $\lambda_{\max}$，最小值就是 $\lambda_{\min}$**。这些极值在对应的[特征向量](@entry_id:151813)方向上取得。对于问题  中给出的能量密度函数，其[关联矩阵](@entry_id:263683)的[特征值](@entry_id:154894)为 $\\{18, 12, 6\\}$。因此，该材料在单位形变下可能存储的最大能量密度就是 $18$。

#### [无约束优化](@entry_id:137083)与Hessian矩阵

在微积分中，我们使用[二阶导数](@entry_id:144508)来判断单变量函数的[临界点](@entry_id:144653)是[局部极大值](@entry_id:137813)、局部极小值还是拐点。对于[多变量函数](@entry_id:145643) $f: \mathbb{R}^n \to \mathbb{R}$，这个角色由**Hessian矩阵**扮演。Hessian矩阵 $H$ 是一个由 $f$ 的所有[二阶偏导数](@entry_id:635213)组成的[对称矩阵](@entry_id:143130)：$(H)_{ij} = \frac{\partial^2 f}{\partial x_i \partial x_j}$。

在函数的[临界点](@entry_id:144653) $\mathbf{p}$（即梯度 $\nabla f(\mathbf{p}) = \mathbf{0}$ 的点），函数在 $\mathbf{p}$ 附近的局部行为可以用以 $H(\mathbf{p})$ 为[关联矩阵](@entry_id:263683)的二次型来近似。具体来说，根据[泰勒展开](@entry_id:145057)，在[临界点](@entry_id:144653)附近，$\Delta \mathbf{x} = \mathbf{x} - \mathbf{p}$ 很小时，
$f(\mathbf{x}) \approx f(\mathbf{p}) + \frac{1}{2} (\Delta \mathbf{x})^T H(\mathbf{p}) (\Delta \mathbf{x})$

这个近似表明，[临界点](@entry_id:144653)的性质完全由 Hessian 矩阵 $H(\mathbf{p})$ 的定性决定：

-   如果 $H(\mathbf{p})$ 是**正定**的，那么二次型项 $(\Delta \mathbf{x})^T H(\mathbf{p}) (\Delta \mathbf{x}) > 0$，函数在 $\mathbf{p}$ 处有一个碗状的“底部”，因此 $\mathbf{p}$ 是一个**局部极小点**。
-   如果 $H(\mathbf{p})$ 是**负定**的，那么二次型项 $< 0$，函数在 $\mathbf{p}$ 处有一个倒扣碗状的“顶部”，因此 $\mathbf{p}$ 是一个**局部极大点**。
-   如果 $H(\mathbf{p})$ 是**不定**的，那么在某些方向上函数值增加，在另一些方向上减少，形成一个马鞍形状，因此 $\mathbf{p}$ 是一个**[鞍点](@entry_id:142576)**。
-   如果 $H(\mathbf{p})$ 是**半定**的，[二阶导数](@entry_id:144508)测试无法得出结论，需要更高阶的信息。

在某些复杂的物理或工程模型中，我们需要确保一个系统在某个[平衡点](@entry_id:272705)（[临界点](@entry_id:144653)）是稳定的，这通常要求该点的势能函数取局部极小值。这等价于要求[势能函数](@entry_id:200753)的 Hessian 矩阵在该点是正定的 。例如，考虑一个由参数 $\alpha$ 和维度 $n$ 描述的系统，其在原点的 Hessian 矩阵 $H_n(\alpha)$ 是一个[三对角矩阵](@entry_id:138829)。为了保证原点对任意维度 $n \ge 2$ 都是一个稳定的局部极小点，我们需要 $H_n(\alpha)$ 对所有 $n$ 都是正定的。这要求其最小特征值对所有 $n$ 都为正。通过分析该矩阵族的最小特征值如何随 $n$ 变化，可以发现，当 $n \to \infty$ 时，最小特征值趋近于 $\alpha-2$。为了保证对所有 $n$ 最小特征值都大于零，我们需要 $\alpha$ 大于这个极限情况下的值，即 $\alpha > 2$。这个例子展示了二次型定性分析在保证高维[系统稳定性](@entry_id:273248)中的强大作用。