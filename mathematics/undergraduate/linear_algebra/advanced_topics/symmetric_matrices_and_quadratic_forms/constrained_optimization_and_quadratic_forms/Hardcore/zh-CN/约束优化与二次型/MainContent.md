## 引言
在科学与工程的广阔领域中，从物理系统的能量到金融模型的风险，我们常常需要分析和优化那些由多个变量决定的复杂函数。这些函数的核心结构往往可以简化为一种优雅的数学形式——**二次型 (quadratic forms)**。然而，二次型表达式中普遍存在的“交叉项”常常掩盖了其内在的几何直觉，并使得寻找其在特定约束下的最大值或最小值成为一个非平凡的挑战。我们如何才能系统地揭示其结构，并高效地解决相关的优化问题呢？

本文旨在填补这一认知鸿沟，为您提供一个关于约束二次型优化的完整框架。我们将从线性代数的视角出发，揭示一个深刻而优美的联系：在约束条件下优化一个二次型，本质上等同于求解一个相关对称矩阵的特征值问题。通过本文的学习，您将掌握一套强大的分析工具。

- 在**原则与机理**一章中，我们将建立二次型的矩阵表示，探讨其与正定性的几何关系，并通过主轴定理找到消除交叉项的“自然”坐标系，最终将约束优化问题简化为特征值的计算。
- 接下来，在**应用与跨学科联系**一章，我们将跨越理论的边界，探索这些原理如何在物理学、信号处理、统计学和金融工程等多个领域中解决实际问题，展现其广泛的适用性。
- 最后，通过**动手实践**环节，您将有机会运用所学知识解决具体问题，从而巩固并深化您的理解。

现在，让我们首先进入第一章，深入探索二次型的基本原则与内在机理。

## 原则与机理

在线性代数的研究中，我们经常遇到描述物理系统能量、统计学中的方差或经济模型中的成本等数量的函数。这些函数往往呈现为变量的二次多项式形式。本章将深入探讨这类被称为**二次型 (quadratic forms)** 的函数，揭示其代数结构、几何形态以及在约束优化问题中的核心作用。我们将建立一个关键的联系：在特定约束下寻找二次型的极值，本质上等同于求解一个相关矩阵的特征值问题。

### 二次型：代数与几何的桥梁

一个在 $n$ 个变量 $x_1, x_2, \dots, x_n$ 上的**二次型**是一个所有项均为二次的齐次多项式。例如，一个二维系统（如晶格中的点缺陷）的势能可能是坐标 $x_1$ 和 $x_2$ 的函数 [@problem_id:1355871]：
$$ U(x_1, x_2) = 4x_1^2 + 4x_1x_2 + 7x_2^2 $$
这个表达式包含变量的平方项（$x_1^2, x_2^2$）和交叉项（$x_1x_2$）。线性代数的威力在于，我们可以用矩阵语言优雅地重写这个表达式。令向量 $\mathbf{x} = \begin{pmatrix} x_1 \\ x_2 \end{pmatrix}$，我们可以找到一个矩阵 $A$ 使得 $U(\mathbf{x}) = \mathbf{x}^T A \mathbf{x}$，其中 $\mathbf{x}^T = \begin{pmatrix} x_1  x_2 \end{pmatrix}$ 是 $\mathbf{x}$ 的转置。

对于一个一般的二维二次型 $q(x_1, x_2) = ax_1^2 + bx_1x_2 + cx_2^2$，其矩阵形式为：
$$ \mathbf{x}^T A \mathbf{x} = \begin{pmatrix} x_1  x_2 \end{pmatrix} \begin{pmatrix} a_{11}  a_{12} \\ a_{21}  a_{22} \end{pmatrix} \begin{pmatrix} x_1 \\ x_2 \end{pmatrix} = a_{11}x_1^2 + (a_{12}+a_{21})x_1x_2 + a_{22}x_2^2 $$
为了使多项式与矩阵表示唯一对应，我们通常选择一个**对称矩阵 (symmetric matrix)**，即 $A = A^T$。在这种情况下，$a_{12} = a_{21}$，交叉项的系数被均分到矩阵的两个非对角元素上。对于上述势能函数，我们有 $a_{11}=4$, $a_{22}=7$, 以及 $a_{12}+a_{21}=4$。通过选择对称矩阵，我们得到 $a_{12}=a_{21}=2$。因此，该二次型可以表示为：
$$ U(\mathbf{x}) = \mathbf{x}^T \begin{pmatrix} 4  2 \\ 2  7 \end{pmatrix} \mathbf{x} $$
这种矩阵表示不仅简化了记号，更重要的是，它将二次型的分析与矩阵的性质（特别是其特征值和特征向量）紧密联系起来。

二次型与**双线性型 (bilinear forms)** 密切相关。一个双线性型 $B(\mathbf{u}, \mathbf{v})$ 是一个在两个向量上均为线性的函数。给定一个矩阵 $A$，我们可以定义一个双线性型 $B(\mathbf{u}, \mathbf{v}) = \mathbf{u}^T A \mathbf{v}$。显然，二次型是双线性型在两个输入相同时的特殊情况，即 $q(\mathbf{x}) = B(\mathbf{x}, \mathbf{x})$。

反过来，我们可以从二次型中恢复出其对应的对称双线性型，这一过程称为**极化 (polarization)**。考虑表达式 $q(\mathbf{u}+\mathbf{v})$ [@problem_id:1355898]：
$$ q(\mathbf{u}+\mathbf{v}) = (\mathbf{u}+\mathbf{v})^T A (\mathbf{u}+\mathbf{v}) = \mathbf{u}^T A \mathbf{u} + \mathbf{v}^T A \mathbf{u} + \mathbf{u}^T A \mathbf{v} + \mathbf{v}^T A \mathbf{v} $$
$$ q(\mathbf{u}+\mathbf{v}) = q(\mathbf{u}) + q(\mathbf{v}) + B(\mathbf{v}, \mathbf{u}) + B(\mathbf{u}, \mathbf{v}) $$
如果矩阵 $A$ 是对称的，那么 $B(\mathbf{u}, \mathbf{v}) = \mathbf{u}^T A \mathbf{v} = (\mathbf{u}^T A \mathbf{v})^T = \mathbf{v}^T A^T \mathbf{u} = \mathbf{v}^T A \mathbf{u} = B(\mathbf{v}, \mathbf{u})$。在这种情况下，我们得到一个类似于初等代数中二项式展开的恒等式：
$$ q(\mathbf{u}+\mathbf{v}) = q(\mathbf{u}) + q(\mathbf{v}) + 2B(\mathbf{u}, \mathbf{v}) $$

### 二次型的几何学：正定性与等值面

二次型的符号（正、负或零）蕴含着其几何形态的深刻信息。我们可以根据二次型 $q(\mathbf{x}) = \mathbf{x}^T A \mathbf{x}$ 的值域来对其进行分类，这个分类称为**正定性 (definiteness)**。

- **正定 (Positive definite)**: 对所有非零向量 $\mathbf{x} \neq \mathbf{0}$，都有 $q(\mathbf{x}) > 0$。
- **负定 (Negative definite)**: 对所有非零向量 $\mathbf{x} \neq \mathbf{0}$，都有 $q(\mathbf{x})  0$。
- **不定 (Indefinite)**: $q(\mathbf{x})$ 既能取正值也能取负值。
- **半正定 (Positive semi-definite)**: 对所有向量 $\mathbf{x}$，都有 $q(\mathbf{x}) \ge 0$，且存在某个非零向量 $\mathbf{x}_0$ 使得 $q(\mathbf{x}_0) = 0$。
- **半负定 (Negative semi-definite)**: 对所有向量 $\mathbf{x}$，都有 $q(\mathbf{x}) \le 0$，且存在某个非零向量 $\mathbf{x}_0$ 使得 $q(\mathbf{x}_0) = 0$。

正定性由对称矩阵 $A$ 的**特征值 (eigenvalues)** 完全决定。由于 $A$ 是对称的，其所有特征值 $\lambda_i$ 都是实数。
- **正定** 当且仅当所有特征值 $\lambda_i  0$。
- **负定** 当且仅当所有特征值 $\lambda_i  0$。
- **不定** 当且仅当存在正负特征值。
- **半正定** 当且仅当所有特征值 $\lambda_i \ge 0$ 且至少有一个为零。
- **半负定** 当且仅当所有特征值 $\lambda_i \le 0$ 且至少有一个为零。

在二维空间中，我们可以通过矩阵的**行列式 (determinant)** 和**迹 (trace)** 快速判断正定性，因为对于 $2 \times 2$ 矩阵，$\det(A) = \lambda_1 \lambda_2$ 且 $\text{tr}(A) = \lambda_1 + \lambda_2$ [@problem_id:1355877]。
- 若 $\det(A)0$ 且 $\text{tr}(A)0$，则 $\lambda_1, \lambda_2$ 均为正，矩阵是**正定**的。
- 若 $\det(A)0$ 且 $\text{tr}(A)0$，则 $\lambda_1, \lambda_2$ 均为负，矩阵是**负定**的。
- 若 $\det(A)0$，则 $\lambda_1, \lambda_2$ 异号，矩阵是**不定**的。
- 若 $\det(A)=0$，则至少一个特征值为零，矩阵是**半定**的（具体是半正定还是半负定取决于迹的符号）。

二次型的正定性直接决定了其三维图像 $z = q(\mathbf{x})$ 的几何形状。例如，在研究经典力学系统在平衡点附近的势能时，势能曲面的形状至关重要 [@problem_id:1355857]。
- 如果二次型是**正定**的，例如 $A = \begin{pmatrix} 5  -2 \\ -2  2 \end{pmatrix}$（其主子式为 $50$ 和 $\det(A)=60$），则其图像 $z = 5x^2 - 4xy + 2y^2$ 是一个开口向上的**椭圆抛物面**（碗状），原点是势能的极小值点，对应一个**稳定平衡点**。
- 如果二次型是**负定**的，图像将是一个开口向下的椭圆抛物面（倒置的碗），原点是极大值点，对应**不稳定平衡点**。
- 如果二次型是**不定**的，图像将是一个**双曲抛物面**（马鞍状），原点是一个鞍点，同样对应**不稳定平衡点**。

当二次型是半定时，情况变得更加有趣。考虑一个材料的应变能模型 $U(\mathbf{x}) = (k_1 x_1 + k_2 x_2 + k_3 x_3)^2 = (\mathbf{k} \cdot \mathbf{x})^2$ [@problem_id:1355911]。显然，对于任何 $\mathbf{x}$，$U(\mathbf{x}) \ge 0$。然而，对于所有与向量 $\mathbf{k}$ 正交的非零向量 $\mathbf{x}$，我们有 $\mathbf{k} \cdot \mathbf{x} = 0$，从而 $U(\mathbf{x})=0$。这意味着该二次型是**半正定**的。其图像是一个沿着垂直于 $\mathbf{k}$ 的平面方向延伸的**抛物柱面**。

类似地，如果一个二次型 $q(\mathbf{w}) = \mathbf{w}^T \Sigma \mathbf{w}$ 的矩阵 $\Sigma$ 是奇异的（即 $\det(\Sigma)=0$），那么它至少有一个零特征值。如果矩阵是半正定的，例如投资组合分析中的协方差矩阵 $\Sigma = \begin{pmatrix} 4  -6 \\ -6  9 \end{pmatrix}$ [@problem_id:1355859]，那么方程 $q(\mathbf{w}) = 0$ 的非零解集是什么呢？由于 $q(\mathbf{w}) = \|R\mathbf{w}\|^2 \ge 0$（其中 $\Sigma=R^TR$），$q(\mathbf{w})=0$ 当且仅当 $\Sigma\mathbf{w}=\mathbf{0}$。因此，使二次型为零的非零向量集合恰好是矩阵 $\Sigma$ 的**零空间 (null space)**。对于这个 $2 \times 2$ 的奇异矩阵，零空间是一条穿过原点的直线，代表了风险为零的投资组合权重。

### 主轴定理：寻找自然的坐标系

二次型中的交叉项，如 $C(x, y) = 5x^2 - 6xy + 5y^2$ 中的 $-6xy$ 项 [@problem_id:1355892]，在几何上意味着什么？它们表明二次型的等值线（例如，所有成本为常数的点 $(x, y)$ 构成的曲线）相对于标准坐标轴 $(x, y)$ 是倾斜的。对于这个成本函数，等值线是倾斜的椭圆。

一个核心问题是：我们能否通过旋转坐标系来消除交叉项？答案是肯定的，这正是**主轴定理 (Principal Axis Theorem)** 的精髓。该定理指出，对于任何与对称矩阵 $A$ 相关的二次型 $q(\mathbf{x}) = \mathbf{x}^T A \mathbf{x}$，总存在一个**正交**坐标变换 $\mathbf{x} = P\mathbf{y}$，使得在新坐标系 $\mathbf{y}$ 中，二次型没有交叉项：
$$ q(\mathbf{y}) = \mathbf{y}^T (P^T A P) \mathbf{y} = \lambda_1 y_1^2 + \lambda_2 y_2^2 + \dots + \lambda_n y_n^2 $$
这里的矩阵 $P$ 是一个正交矩阵（$P^T P = I$），其列向量是矩阵 $A$ 的一组标准正交**特征向量 (eigenvectors)**。$\lambda_1, \dots, \lambda_n$ 是对应的特征值。$P^T A P$ 是一个对角矩阵，对角线上的元素正是这些特征值。

新的坐标轴，即 $\mathbf{y}$ 坐标系的方向，被称为二次型的**主轴 (principal axes)**。它们指向 $A$ 的特征向量的方向。在这些“自然”的坐标系中，二次型的几何结构变得异常清晰。例如，在问题 [@problem_id:1355892] 中，为了消除成本函数 $C(x, y)$ 的交叉项，我们需要找到其关联矩阵 $A = \begin{pmatrix} 5  -3 \\ -3  5 \end{pmatrix}$ 的特征向量。通过计算可知，将坐标系逆时针旋转 $45^\circ$ 即可与主轴对齐，从而在新坐标 $(x', y')$ 下，成本函数变为对角形式 $C(x', y') = \lambda_1 (x')^2 + \lambda_2 (y')^2$。

### 核心原理：约束优化与特征值

现在我们来探讨本章最核心的问题：如何找到二次型 $q(\mathbf{x}) = \mathbf{x}^T A \mathbf{x}$ 在单位球（或圆）约束 $\|\mathbf{x}\|^2 = 1$ 下的最大值和最小值？

这个问题在物理学、工程学和数据科学中无处不在。例如，寻找单位形变下材料的最大应变能 [@problem_id:1355876]，或者在总位移平方为1的约束下系统的最大/最小势能 [@problem_id:1355871]。

答案出人意料地简洁：

**定理（瑞利商原理）：** 对于一个实对称矩阵 $A$，二次型 $q(\mathbf{x}) = \mathbf{x}^T A \mathbf{x}$ 在约束 $\mathbf{x}^T \mathbf{x} = 1$ 下的最大值等于 $A$ 的最大特征值 $\lambda_{\max}$，最小值等于 $A$ 的最小特征值 $\lambda_{\min}$。此外，最大值在对应于 $\lambda_{\max}$ 的单位特征向量处取得，最小值在对应于 $\lambda_{\min}$ 的单位特征向量处取得。

我们可以通过主轴变换来直观地理解这个原理。在主轴坐标系 $\mathbf{y}$ 中，问题转化为最大化/最小化 $\sum_{i=1}^n \lambda_i y_i^2$，约束条件为 $\sum_{i=1}^n y_i^2 = 1$。假设特征值排序为 $\lambda_{\min} = \lambda_n \le \dots \le \lambda_1 = \lambda_{\max}$。
$$ q(\mathbf{y}) = \sum \lambda_i y_i^2 \le \sum \lambda_{\max} y_i^2 = \lambda_{\max} \sum y_i^2 = \lambda_{\max} $$
当且仅当我们将所有“权重”放在与最大特征值相关的分量上时，即令对应于 $\lambda_{\max}$ 的 $y_k= \pm 1$ 而所有其他 $y_i=0$ 时，等号成立。这对应于原始坐标系中的单位特征向量。同样地，可以证明最小值为 $\lambda_{\min}$。

从分析的角度，这个问题可以通过拉格朗日乘子法解决。我们定义拉格朗日函数：
$$ \mathcal{L}(\mathbf{x}, \lambda) = \mathbf{x}^T A \mathbf{x} - \lambda (\mathbf{x}^T \mathbf{x} - 1) $$
对其关于 $\mathbf{x}$ 求梯度并令其为零，得到 $\nabla_{\mathbf{x}} \mathcal{L} = 2A\mathbf{x} - 2\lambda\mathbf{x} = \mathbf{0}$，这直接导出了**特征值方程** $A\mathbf{x} = \lambda\mathbf{x}$。这表明，极值点必须是 $A$ 的特征向量。在这些点上，二次型的值为 $q(\mathbf{x}) = \mathbf{x}^T A \mathbf{x} = \mathbf{x}^T (\lambda\mathbf{x}) = \lambda (\mathbf{x}^T\mathbf{x}) = \lambda$。因此，极值就是特征值。

在问题 [@problem_id:1355871], [@problem_id:1355876] 和 [@problem_id:1355902] 中，我们都应用了这一强大原理。无论是二维势能函数还是三维应变能，我们首先将函数写成矩阵形式 $\mathbf{x}^T A \mathbf{x}$，然后计算对称矩阵 $A$ 的特征值。最大的特征值即为函数在单位球上的最大值，最小的特征值即为最小值。

### 推广与应用：瑞利商的逐级优化特性

瑞利商原理还可以进一步推广，这在主成分分析 (PCA) 等数据降维技术中至关重要。假设我们已经找到了对应于最大特征值 $\lambda_1$ 的“主方向” $\mathbf{v}_1$。如果我们想寻找在与 $\mathbf{v}_1$ 正交的子空间中的“次要”主方向，该怎么办？

这引出了**瑞利-里兹定理 (Rayleigh-Ritz Theorem)** 的一个重要推论（有时也与 Courant-Fischer 极小极大原理相关联）。令矩阵 $A$ 的特征值按降序排列为 $\lambda_1 \ge \lambda_2 \ge \dots \ge \lambda_n$，对应的标准正交特征向量为 $\mathbf{v}_1, \mathbf{v}_2, \dots, \mathbf{v}_n$。

- $\lambda_1 = \max_{\|\mathbf{x}\|=1} \mathbf{x}^T A \mathbf{x}$。
- $\lambda_2 = \max_{\|\mathbf{x}\|=1, \mathbf{x} \perp \mathbf{v}_1} \mathbf{x}^T A \mathbf{x}$。
- ...
- $\lambda_k = \max_{\|\mathbf{x}\|=1, \mathbf{x} \perp \mathbf{v}_1, \dots, \mathbf{v}_{k-1}} \mathbf{x}^T A \mathbf{x}$。

换言之，第二大特征值 $\lambda_2$ 是二次型在与第一特征向量正交的所有单位向量上能取到的最大值。这个最大值在第二特征向量 $\mathbf{v}_2$ 处取得。这个过程可以持续下去，依次找到方差最大（或能量最高等）的相互正交的方向。

问题 [@problem_id:1355882] 提供了一个清晰的例子。一个 $4 \times 4$ 矩阵 $A$ 的特征值为 $12, 8, 5, -3$。二次型 $Q(\mathbf{x})$ 在整个单位球上的最大值是 $12$。如果我们将与该值相关的主特征方向移除，即在所有与该特征向量正交的单位向量中寻找 $Q(\mathbf{x})$ 的最大值，那么根据上述定理，这个最大值就是第二大特征值，即 $8$。

总结来说，二次型和对称矩阵构成了理解多变量函数局部行为、几何形态和优化问题的基石。主轴定理揭示了其固有的“自然”坐标系，而瑞利商原理则将复杂的约束优化问题简化为代数上更易于处理的特征值计算，充分展示了线性代数在连接几何直觉与代数运算方面的强大威力。