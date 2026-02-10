## 引言
[四元数](@keyword=quaternions|lang=zh-CN|style=Feynman)由威廉·罗恩·哈密顿（William Rowan Hamilton）发现，是一种扩展了复数的强大的四维数系。然而，其抽象的性质和非交换的[乘法规则](@keyword=multiplication_rule|lang=zh-CN|style=Feynman)使其难以直接理解和应用。这就产生了一个知识鸿沟：我们如何才能在一个更具体、更直观的框架中利用四元数的力量？解决方案在于找到一种[忠实表示](@keyword=faithful_representation|lang=zh-CN|style=Feynman)——一种将[四元数代数](@keyword=quaternion_algebras|lang=zh-CN|style=Feynman)转化为我们熟知的矩阵世界的方法。

本文旨在探索这座连接抽象代数与应用科学的强大桥梁。首先，在“原理与机制”一章中，我们将逐步构建[四元数](@keyword=quaternions|lang=zh-CN|style=Feynman)的标准2x2复[矩阵表示](@keyword=matrix_representations|lang=zh-CN|style=Feynman)。我们将揭示四元数性质与矩阵运算之间优美的相似之处，最终引出[单位四元数](@keyword=unit_quaternions|lang=zh-CN|style=Feynman)与量子力学中的[SU(2)群](@keyword=su(2)_group|lang=zh-CN|style=Feynman)之间的深刻联系。随后，“应用与跨学科联系”一章将展示这种表示法不仅仅是数学上的一个奇妙构造，更是在不同领域中的重要工具——从创建流畅的三维动画、导航无人机，到描述量子领域中粒子的基本自旋。

## 原理与机制

### 对具体形式的探寻

我们已经介绍了四元数，这种形式为 $q = a + bi + cj + dk$ 的奇特的四维数。威廉·罗恩·哈密顿（William Rowan Hamilton）的发现是代数想象力的一次飞跃，但它们的[乘法规则](@keyword=multiplication_rule|lang=zh-CN|style=Feynman)，特别是 $ij = -ji$ 这样的[反对易](@keyword=anti_commutation|lang=zh-CN|style=Feynman)性质，可能让人觉得抽象和笨拙。我们如何才能更直观地掌握它们？我们如何才能“看到”它们的作用？

在物理学和数学中，驯服一个抽象代数系统的一个强有力的策略是为它找到一个**表示**。可以把它看作一本翻译词典。我们将四元数这门陌生的语言翻译成一种更熟悉的语言：矩阵及其运算的语言。如果我们的翻译是好的——数学家称之为**[忠实表示](@keyword=faithful_representation|lang=zh-CN|style=Feynman)**——那么[四元数](@keyword=quaternions|lang=zh-CN|style=Feynman)世界中的每一条规则和关系都将在矩阵世界中有一个完美的对应。我们用矩阵进行的任何计算，都将为相应的四元数提供一个有效的结果。这不仅仅是一个巧妙的技巧；这是利用强大且易于理解的线性代数工具来探索新领域的一种方式。[@problem_id:1598224]

### 构建矩阵“伪装”

我们的目标是找到一组行为与[四元数](@keyword=quaternions|lang=zh-CN|style=Feynman)基元 $\{1, i, j, k\}$ 完全相同的矩阵。我们正在寻找满足定义关系 $\rho(i)^2 = \rho(j)^2 = \rho(k)^2 = \rho(i)\rho(j)\rho(k) = -\rho(1)$ 的矩阵，我们称之为 $\rho(1), \rho(i), \rho(j), \rho(k)$。

让我们尝试使用$2 \times 2$的复数矩阵来构建这种表示。这是一个合理的猜测，因为复数本身已经包含一个虚数单位。

首先，从简单的部分开始。[四元数](@keyword=quaternions|lang=zh-CN|style=Feynman) $1$ 是乘法单位元，所以它的[矩阵表示](@keyword=matrix_representations|lang=zh-CN|style=Feynman) $\rho(1)$ 必须是[单位矩阵](@keyword=identity_matrix|lang=zh-CN|style=Feynman)：
$$
\rho(1) = I = \begin{pmatrix} 1  0 \\ 0  1 \end{pmatrix}
$$

现在来看虚数单位。我们需要平方为 $-I$ 的矩阵。对于 $\rho(i)$，一个自然的选择是使用复数 $i$ 本身：
$$
\rho(i) = \begin{pmatrix} i  0 \\ 0  -i \end{pmatrix}
$$
我们来验证一下：$\rho(i)^2 = \begin{pmatrix} i^2  0 \\ 0  (-i)^2 \end{pmatrix} = \begin{pmatrix} -1  0 \\ 0  -1 \end{pmatrix} = -I$。完全正确。

对于 $\rho(j)$，我们需要另一个平方为 $-I$ 的矩阵，但它还必须以正确的方式与 $\rho(i)$ 相互作用。让我们尝试一个简单的非[对角形式](@keyword=diagonal_form|lang=zh-CN|style=Feynman)：
$$
\rho(j) = \begin{pmatrix} 0  1 \\ -1  0 \end{pmatrix}
$$
快速验证可知 $\rho(j)^2 = \begin{pmatrix} 0  1 \\ -1  0 \end{pmatrix} \begin{pmatrix} 0  1 \\ -1  0 \end{pmatrix} = \begin{pmatrix} -1  0 \\ 0  -1 \end{pmatrix} = -I$。到目前为止一切顺利。

关键时刻在于 $k$。在[四元数代数](@keyword=quaternion_algebras|lang=zh-CN|style=Feynman)中，$k = ij$。如果我们的表示要成立，那么必须有 $\rho(k) = \rho(i)\rho(j)$。我们直接计算这个矩阵乘积：
$$
\rho(k) = \rho(i)\rho(j) = \begin{pmatrix} i  0 \\ 0  -i \end{pmatrix} \begin{pmatrix} 0  1 \\ -1  0 \end{pmatrix} = \begin{pmatrix} 0  i \\ i  0 \end{pmatrix}
$$
这就得到了我们用于 $k$ 的候选矩阵。[@problem_id:1652960] [@problem_id:1621666] 我们必须验证它是否满足所有必需的性质。它的平方是 $-I$ 吗？
$$
\rho(k)^2 = \begin{pmatrix} 0  i \\ i  0 \end{pmatrix} \begin{pmatrix} 0  i \\ i  0 \end{pmatrix} = \begin{pmatrix} i^2  0 \\ 0  i^2 \end{pmatrix} = \begin{pmatrix} -1  0 \\ 0  -1 \end{pmatrix} = -I
$$
是的！那么著名的反对易性呢？我们来检验一下 $\rho(j)\rho(i)$：
$$
\rho(j)\rho(i) = \begin{pmatrix} 0  1 \\ -1  0 \end{pmatrix} \begin{pmatrix} i  0 \\ 0  -i \end{pmatrix} = \begin{pmatrix} 0  -i \\ -i  0 \end{pmatrix} = -\rho(k)
$$
成立！我们为四元数基元找到了一组自洽的矩阵“伪装”。

现在，我们可以通过将这些基矩阵与相同的实系数相结合来表示*任何*四元数 $q = a + bi + cj + dk$：
$$
\rho(q) = a\rho(1) + b\rho(i) + c\rho(j) + d\rho(k)
$$
$$
\rho(q) = a\begin{pmatrix} 1  0 \\ 0  1 \end{pmatrix} + b\begin{pmatrix} i  0 \\ 0  -i \end{pmatrix} + c\begin{pmatrix} 0  1 \\ -1  0 \end{pmatrix} + d\begin{pmatrix} 0  i \\ i  0 \end{pmatrix}
$$
将这些合并成一个单一矩阵，我们得到了最终结果：
$$
\rho(a + bi + cj + dk) = \begin{pmatrix} a+bi  c+di \\ -c+di  a-bi \end{pmatrix}
$$
这个特定的矩阵结构就是四元数的标准表示。[@problem_id:1625370] [@problem_id:662051] 任何[四元数](@keyword=quaternions|lang=zh-CN|style=Feynman)都可以唯一地写成这种形式，并且任何这种形式的矩阵都对应一个唯一的[四元数](@keyword=quaternions|lang=zh-CN|style=Feynman)。我们的词典构建完成了。

### 表示法中的奥秘

这种矩阵形式不仅仅是为了记法上的方便。它揭示了四元数的抽象规则与矩阵的具体性质之间惊人的一致性。让我们来探索其中一些奇妙的联系。

#### 范数变为[行列式](@keyword=determinant|lang=zh-CN|style=Feynman)

四元数的**范数** $|q|$ 是它在四维空间中的“大小”或“长度”，其平方由 $|q|^2 = a^2 + b^2 + c^2 + d^2$ 给出。让我们计算其[矩阵表示](@keyword=matrix_representations|lang=zh-CN|style=Feynman) $\rho(q)$ 的[行列式](@keyword=determinant|lang=zh-CN|style=Feynman)：
$$
\det(\rho(q)) = (a+bi)(a-bi) - (c+di)(-c+di)
$$
$$
= (a^2+b^2) - (-c^2-d^2) = a^2+b^2+c^2+d^2 = |q|^2
$$
这是一个非凡的结果。[四元数范数](@keyword=quaternion_norm|lang=zh-CN|style=Feynman)的平方这个抽象概念，与我们熟悉的[矩阵行列式](@keyword=matrix_determinant|lang=zh-CN|style=Feynman)完全相同。这并非偶然；它表明我们的表示捕捉到了[四元数代数](@keyword=quaternion_algebras|lang=zh-CN|style=Feynman)的深层结构。

#### 共轭变为伴随

每个四元数 $q = a + bi + cj + dk$ 都有一个**共轭** $q^* = a - bi - cj - dk$。在我们的矩阵世界里，这个运算是什么样的呢？让我们找出 $q^*$ 对应的矩阵：
$$
\rho(q^*) = \begin{pmatrix} a-bi  -c-di \\ c-di  a+bi \end{pmatrix}
$$
现在，让我们取原始矩阵 $\rho(q)$ 并计算其**[共轭转置](@keyword=conjugate_transpose|lang=zh-CN|style=Feynman)**（或[埃尔米特伴随](@keyword=hermitian_adjoint|lang=zh-CN|style=Feynman)），用匕首符号 $\dagger$ 表示。该运算包括先进行转置，然后对每个元素取复共轭。
$$
\rho(q)^\dagger = \begin{pmatrix} a+bi  c+di \\ -c+di  a-bi \end{pmatrix}^\dagger = \begin{pmatrix} \overline{a+bi}  \overline{-c+di} \\ \overline{c+di}  \overline{a-bi} \end{pmatrix} = \begin{pmatrix} a-bi  -c-di \\ c-di  a+bi \end{pmatrix}
$$
它们是完全相同的！$\rho(q^*) = \rho(q)^\dagger$。四元数共轭这一代数规则，与取相应矩阵的[共轭转置](@keyword=conjugate_transpose|lang=zh-CN|style=Feynman)完全一样。[@problem_id:2271921]

#### 逆的揭示

这种平行的结构为我们找到四元数的逆提供了一种优美的方法。对于任何非零[四元数](@keyword=quaternions|lang=zh-CN|style=Feynman) $q$，其逆由公式 $q^{-1} = \frac{q^*}{|q|^2}$ 给出。让我们利用新发现将其转化为矩阵语言：
$$
\rho(q)^{-1} = \rho(q^{-1}) = \rho\left(\frac{q^*}{|q|^2}\right) = \frac{1}{|q|^2}\rho(q^*) = \frac{\rho(q)^\dagger}{\det(\rho(q))}
$$
这正是这种形式的 $2 \times 2$ [矩阵求逆](@keyword=matrix_inversion|lang=zh-CN|style=Feynman)的标准公式！寻找[四元数逆](@keyword=quaternion_inverse|lang=zh-CN|style=Feynman)的抽象代数规则，完美地反映在[矩阵代数](@keyword=matrix_algebra|lang=zh-CN|style=Feynman)的一个具体过程中。[@problem_id:1361617]

### 皇冠上的明珠：旋转与[SU(2)群](@keyword=su(2)_group|lang=zh-CN|style=Feynman)

当我们考虑范数为1的**[单位四元数](@keyword=unit_quaternions|lang=zh-CN|style=Feynman)**时，这种表示的真正威力与美感才得以最充分地展现。正是这些四元数，能够优雅地描述三维空间中的旋转。

在我们的矩阵世界里，一个[四元数](@keyword=quaternions|lang=zh-CN|style=Feynman)的范数为1意味着什么？这仅仅意味着它的[矩阵表示](@keyword=matrix_representations|lang=zh-CN|style=Feynman)的[行列式](@keyword=determinant|lang=zh-CN|style=Feynman)必须为1。
$$
|q|=1 \quad \iff \quad \det(\rho(q)) = 1
$$
此外，对于[单位四元数](@keyword=unit_quaternions|lang=zh-CN|style=Feynman)，其逆就是其共轭，即 $q^{-1} = q^*$。让我们看看这对它的矩阵意味着什么：
$$
\rho(q)^{-1} = \rho(q^*) = \rho(q)^\dagger
$$
所以，对于一个[单位四元数](@keyword=unit_quaternions|lang=zh-CN|style=Feynman)，其矩阵的逆就是它自身的[共轭转置](@keyword=conjugate_transpose|lang=zh-CN|style=Feynman)。一个具有这种性质 $U^{-1} = U^\dagger$ 的矩阵 $U$ 被称为**酉矩阵**。

综上所述，所有[单位四元数](@keyword=unit_quaternions|lang=zh-CN|style=Feynman)的集合对应于所有**酉**且**[行列式](@keyword=determinant|lang=zh-CN|style=Feynman)为1**的 $2 \times 2$ [复矩阵](@keyword=complex_matrices|lang=zh-CN|style=Feynman)的集合。这是一个非常重要且被深入研究的矩阵集合，称为**2次[特殊酉群](@keyword=special_unitary_group|lang=zh-CN|style=Feynman)**，即 $SU(2)$。[@problem_id:1625370]

这是一个深刻而优美的联系。由[单位四元数](@keyword=unit_quaternions|lang=zh-CN|style=Feynman)编码的[三维旋转](@keyword=3d_rotations|lang=zh-CN|style=Feynman)代数，在数学上与 $SU(2)$ 群等同。而这个 $SU(2)$ 群正位于量子力学的核心，用于描述电子等基本粒子的[内禀角动量](@keyword=intrinsic_angular_momentum|lang=zh-CN|style=Feynman)，即“自旋”。Hamilton 为理解三维空间而设计的抽象代数，在一个世纪后，在量子领域找到了其最基本的物理应用。

### 更深层次的分类

有人可能会想，我们是否可以使用更简单的矩阵，比如只包含实数的矩阵。事实证明，对于我们找到的这种紧凑、优美的表示，复数是必不可少的。来自群论的高级工具，如**Frobenius-Schur 指示子**，可以对表示进行分类。对于[四元数群](@keyword=quaternion_group|lang=zh-CN|style=Feynman)（$Q_8$，所有[四元数](@keyword=quaternions|lang=zh-CN|style=Feynman)的一个小型有限[子集](@keyword=subset|lang=zh-CN|style=Feynman)），该指示子为 $-1$。[@problem_id:1630085] 这个值表示一种“四元数型”或“伪实数型”的表示类型。这意味着该表示与其复[共轭表示](@keyword=conjugate_representation|lang=zh-CN|style=Feynman)等价，但不能被化为实数值。[@problem_id:1615900] 在某种意义上，其结构与[四元数](@keyword=quaternions|lang=zh-CN|style=Feynman)的本性紧密相连，以至于它无法被简化为同样大小的纯实数形式。

我们*可以*使用实矩阵来表示四元数，但我们必须转向更高的维度。例如，任何[四元数](@keyword=quaternions|lang=zh-CN|style=Feynman)都可以用一个 $4 \times 4$ 的实矩阵来表示。[@problem_id:986950] 虽然这种 $4 \times 4$ 的表示在某些计算应用中很有用，但它失去了与复群 $SU(2)$ 那种奇妙、直接且优美的联系，而正是这种联系揭示了代数、几何与物理学基本定律之间的深刻统一。

