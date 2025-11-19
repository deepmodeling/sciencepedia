## 引言
在科学与工程计算领域，求解由物理模型离散化产生的大规模线性方程组是一项核心挑战。直接法虽然精确，但对于变量数以百万计的系统而言，其计算成本和内存需求往往令人望而却步。因此，[迭代法](@entry_id:194857)，特别是那些能够高效利用现代计算机体系结构的[迭代法](@entry_id:194857)，成为了不可或缺的工具。本文聚焦于一种经典而强大的迭代技术——**逐次超松弛（Successive Over-relaxation, SOR）**方法。尽管历史悠久，SOR及其变体至今仍在众多应用领域扮演着关键角色，但其背后的数学原理、收敛特性和应用技巧对初学者而言可能存在认知鸿沟。

本文旨在系统性地剖析SOR方法，带领读者从理论走向实践。文章将分为三个核心部分。在“**原理与机制**”一章中，我们将从SOR的迭代表达式入手，阐明其与[高斯-赛德尔法](@entry_id:145727)的内在联系，并建立其收敛性理论，探讨如何选择合适的参数以优化性能。随后，“**应用与跨学科联系**”一章将展示SOR方法如何在[偏微分方程](@entry_id:141332)求解、网络均衡分析、机器学习乃至[计算机图形学](@entry_id:148077)等多个领域中发挥作用，揭示其强大的跨学科生命力。最后，通过“**动手实践**”部分的引导性练习，您将有机会亲手应用所学知识，加深对算法执行细节和收敛特性的理解。通过这一结构化的学习路径，读者将能够全面掌握SOR方法的精髓，并具备将其应用于解决实际问题的能力。

## 原理与机制

在求解大型线性方程组 $A\mathbf{x} = \mathbf{b}$ 时，特别是那些由[偏微分方程离散化](@entry_id:175821)产生的[稀疏系统](@entry_id:168473)，迭代法是一种至关重要的计算工具。在本章中，我们将深入探讨一种经典且功能强大的迭代方法——**逐次超松弛（Successive Over-relaxation, SOR）**方法。我们将从其基本迭代表达式出发，揭示其与高斯-赛德尔（Gauss-Seidel）法的深刻联系，并通过几何直觉理解“松弛”的含义。随后，我们将建立该方法的矩阵理论，系统地分析其收敛性，并介绍确保其收敛的关键条件。最后，我们将讨论如何选择最优的松弛因子以达到最快[收敛速度](@entry_id:636873)，并探讨在现代[并行计算](@entry_id:139241)环境下，SOR方法所面临的挑战与应对策略。

### 逐次超松弛迭代公式

SOR方法的核心思想是对[高斯-赛德尔迭代](@entry_id:136271)步进行“加速”或“减速”调整。为了理解这一点，我们首先回顾[高斯-赛德尔法](@entry_id:145727)的思想：在计算解向量的第 $i$ 个分量 $x_i$ 的新近似值时，立即使用同一迭代步中已经计算出的新分量 $x_j^{(k+1)}$（其中 $j  i$）。

SOR方法在此基础上引入了一个**松弛因子（relaxation parameter）** $\omega$。对于线性系统 $A\mathbf{x} = \mathbf{b}$，其第 $i$ 个方程为：
$$ \sum_{j=1}^{n} a_{ij}x_j = b_i $$
我们可以将其改写为求解 $x_i$ 的形式：
$$ x_i = \frac{1}{a_{ii}} \left( b_i - \sum_{j \neq i} a_{ij}x_j \right) $$
[高斯-赛德尔法](@entry_id:145727)直接使用这个公式，并代入最新的可用分量值。SOR方法则首先计算出高斯-赛德尔更新量，然后将其与上一迭代步的值进行加权平均。具体而言，从第 $k$ 次迭代的解 $\mathbf{x}^{(k)}$ 更新至第 $k+1$ 次迭代的解 $\mathbf{x}^{(k+1)}$，其分量形式的更新规则如下：
$$ x_i^{(k+1)} = (1-\omega)x_i^{(k)} + \frac{\omega}{a_{ii}} \left( b_i - \sum_{j=1}^{i-1} a_{ij}x_j^{(k+1)} - \sum_{j=i+1}^{n} a_{ij}x_j^{(k)} \right) \quad \text{for } i=1, 2, \dots, n $$
在这个公式中，求和项 $\sum_{j=1}^{i-1} a_{ij}x_j^{(k+1)}$ 体现了SOR方法与[高斯-赛德尔法](@entry_id:145727)共同的核心特征：在更新 $x_i^{(k+1)}$ 时，立即利用在[本轮](@entry_id:169326)迭代中已经计算出的新分量值（即 $x_1^{(k+1)}, \dots, x_{i-1}^{(k+1)}$）。

为了更具体地理解这个过程，我们考虑一个 $3 \times 3$ 的[三对角系统](@entry_id:635799) [@problem_id:2207396]：
$$
\begin{pmatrix} d_1  u_1  0 \\ l_2  d_2  u_2 \\ 0  l_3  d_3 \end{pmatrix}
\begin{pmatrix} x_1 \\ x_2 \\ x_3 \end{pmatrix} =
\begin{pmatrix} b_1 \\ b_2 \\ b_3 \end{pmatrix}
$$
按照SOR的更新规则，第 $(k+1)$ 次迭代的三个分量依次计算如下：

1.  对于 $x_1^{(k+1)}$（$i=1$），其更新不依赖于[本轮](@entry_id:169326)其他新分量：
    $$ x_1^{(k+1)} = (1-\omega)x_1^{(k)} + \frac{\omega}{d_1} \left( b_1 - u_1 x_2^{(k)} \right) $$

2.  对于 $x_2^{(k+1)}$（$i=2$），其更新利用了刚刚算出的 $x_1^{(k+1)}$：
    $$ x_2^{(k+1)} = (1-\omega)x_2^{(k)} + \frac{\omega}{d_2} \left( b_2 - l_2 x_1^{(k+1)} - u_2 x_3^{(k)} \right) $$

3.  对于 $x_3^{(k+1)}$（$i=3$），其更新利用了已经算出的 $x_2^{(k+1)}$：
    $$ x_3^{(k+1)} = (1-\omega)x_3^{(k)} + \frac{\omega}{d_3} \left( b_3 - l_3 x_2^{(k+1)} \right) $$

观察SOR的通用公式可以发现一个重要的特例。如果我们将松弛因子设为 $\omega=1$，那么公式变为 [@problem_id:2207389]：
$$ x_i^{(k+1)} = (1-1)x_i^{(k)} + \frac{1}{a_{ii}} \left( b_i - \sum_{j=1}^{i-1} a_{ij}x_j^{(k+1)} - \sum_{j=i+1}^{n} a_{ij}x_j^{(k)} \right) $$
$$ x_i^{(k+1)} = \frac{1}{a_{ii}} \left( b_i - \sum_{j=1}^{i-1} a_{ij}x_j^{(k+1)} - \sum_{j=i+1}^{n} a_{ij}x_j^{(k)} \right) $$
这正是**高斯-赛德尔（Gauss-Seidel）方法**的迭代表达式。因此，SOR方法可以被视为[高斯-赛德尔法](@entry_id:145727)的一种推广。

### 松弛的几何诠释

参数 $\omega$ 的引入不仅仅是代数上的推广，它具有深刻的几何意义。我们可以将SOR的更新步骤看作一个从当前点 $\mathbf{x}^{(k)}$ 向某个目标点移动的过程。

让我们将SOR的更新公式重新整理一下。令 $y_i^{(k+1)}$ 表示纯粹的高斯-赛德尔更新分量：
$$ y_i^{(k+1)} = \frac{1}{a_{ii}} \left( b_i - \sum_{j=1}^{i-1} a_{ij}x_j^{(k+1)} - \sum_{j=i+1}^{n} a_{ij}x_j^{(k)} \right) $$
将此定义代入SOR公式，我们得到：
$$ x_i^{(k+1)} = (1-\omega)x_i^{(k)} + \omega y_i^{(k+1)} $$
这个表达式可以进一步写为：
$$ x_i^{(k+1)} = x_i^{(k)} + \omega \left( y_i^{(k+1)} - x_i^{(k)} \right) $$
这个形式清晰地揭示了SOR更新的几何本质 [@problem_id:3280188]。在每个分量 $i$ 的更新中，我们首先确定一个“目标”方向，即从当前值 $x_i^{(k)}$ 指向高斯-赛德尔更新值 $y_i^{(k+1)}$ 的向量 $(y_i^{(k+1)} - x_i^{(k)})$。然后，我们沿着这个方向移动，步长由松弛因子 $\omega$ 调节。

这种几何关系引出了对不同 $\omega$ 值的直观理解：
*   当 $\omega=1$ 时， $x_i^{(k+1)} = y_i^{(k+1)}$。SOR退化为[高斯-赛德尔法](@entry_id:145727)，即迭代步长恰好达到高斯-赛德尔目标点。
*   当 $0  \omega  1$ 时，我们称之为**[欠松弛](@entry_id:756302)（under-relaxation）**。迭代步长小于到达高斯-赛德尔目标点所需的距离，新点 $x_i^{(k+1)}$ 位于 $x_i^{(k)}$ 和 $y_i^{(k+1)}$ 之间的线段上。这种策略通常用于改善某些不稳定迭代过程的收敛性。
*   当 $\omega  1$ 时，我们称之为**超松弛（over-relaxation）**。迭代步长超过了到达高斯-赛德尔目标点所需的距离，新点 $x_i^{(k+1)}$ 落在了以 $x_i^{(k)}$ 为起点、穿过 $y_i^{(k+1)}$ 的射线的延长线上。这种“超调”的策略如果使用得当，可以显著加速收敛，这也是SOR方法名称的由来。

让我们通过一个具体的例子来观察不同 $\omega$ 值的影响 [@problem_id:2207427]。考虑线性系统：
$$ \begin{pmatrix} 4  -1 \\ -1  4 \end{pmatrix} \begin{pmatrix} x_1 \\ x_2 \end{pmatrix} = \begin{pmatrix} 10 \\ 20 \end{pmatrix} $$
从初始猜测 $\mathbf{x}^{(0)} = \begin{pmatrix} 0 \\ 0 \end{pmatrix}$ 开始，我们计算第一次迭代的结果 $\mathbf{x}^{(1)}$。

更新公式为：
$$ x_1^{(1)} = (1-\omega)x_1^{(0)} + \frac{\omega}{4}(10 - (-1)x_2^{(0)}) = \frac{10\omega}{4} = \frac{5\omega}{2} $$
$$ x_2^{(1)} = (1-\omega)x_2^{(0)} + \frac{\omega}{4}(20 - (-1)x_1^{(1)}) = \frac{\omega}{4}(20 + x_1^{(1)}) = 5\omega + \frac{5}{8}\omega^2 $$

现在，我们代入三个不同的 $\omega$ 值进行计算：
1.  **[欠松弛](@entry_id:756302)** ($\omega=0.5$)：
    $x_1^{(1)} = \frac{5}{4}$, $x_2^{(1)} = 5(0.5) + \frac{5}{8}(0.5)^2 = \frac{5}{2} + \frac{5}{32} = \frac{85}{32} \approx 2.656$
2.  **高斯-赛德尔** ($\omega=1.0$)：
    $x_1^{(1)} = \frac{5}{2}$, $x_2^{(1)} = 5(1) + \frac{5}{8}(1)^2 = 5 + \frac{5}{8} = \frac{45}{8} = 5.625$
3.  **超松弛** ($\omega=1.5$)：
    $x_1^{(1)} = \frac{15}{4}$, $x_2^{(1)} = 5(1.5) + \frac{5}{8}(1.5)^2 = \frac{15}{2} + \frac{45}{32} = \frac{285}{32} \approx 8.906$

该系统的精确解为 $\mathbf{x} = \begin{pmatrix} 4 \\ 6 \end{pmatrix}$。可以看到，超松弛（$\omega=1.5$）的迭代结果在一次迭代后比[高斯-赛德尔法](@entry_id:145727)（$\omega=1$）更接近精确解的某些特征，尽管它在 $x_2$分量上有所“超调”。这个简单的例子直观地展示了 $\omega$ 如何影响迭代路径。

### 矩阵形式与收敛性理论

为了系统地分析[SOR方法的收敛性](@entry_id:164310)，我们需要将其表示为矩阵形式。我们将系数矩阵 $A$ 分解为三个部分：
$$ A = D + L + U $$
其中，$D$ 是 $A$ 的对角部分，$L$ 是 $A$ 的严格下三角部分（对角线以上元素均为零），$U$ 是 $A$ 的严格上三角部分（对角线以下元素均为零）。

利用这个分裂，SOR的分量形式更新规则可以被优雅地写成矩阵形式。首先，我们将所有带有上标 $(k+1)$ 的项移到等式左边，带有上标 $(k)$ 的项移到右边：
$$ a_{ii}x_i^{(k+1)} + \omega \sum_{j=1}^{i-1} a_{ij}x_j^{(k+1)} = (1-\omega)a_{ii}x_i^{(k)} - \omega \sum_{j=i+1}^{n} a_{ij}x_j^{(k)} + \omega b_i $$
将所有分量的[方程组](@entry_id:193238)合起来，我们可以得到：
$$ (D + \omega L) \mathbf{x}^{(k+1)} = \left( (1-\omega)D - \omega U \right) \mathbf{x}^{(k)} + \omega \mathbf{b} $$
为了得到标准的迭代形式 $\mathbf{x}^{(k+1)} = T \mathbf{x}^{(k)} + \mathbf{c}$，我们用 $(D + \omega L)^{-1}$ 左乘等式两边（由于 $D$ 的对角元素非零，$D+\omega L$ 是可逆的）：
$$ \mathbf{x}^{(k+1)} = (D + \omega L)^{-1} \left( (1-\omega)D - \omega U \right) \mathbf{x}^{(k)} + \omega (D + \omega L)^{-1} \mathbf{b} $$
由此，我们得到了SOR方法的**[迭代矩阵](@entry_id:637346)（iteration matrix）**，记为 $T_{SOR}(\omega)$：
$$ T_{SOR}(\omega) = (D + \omega L)^{-1} \left( (1-\omega)D - \omega U \right) $$
作为练习，我们可以为一个泛化的 $2 \times 2$ 矩阵 $A = \begin{pmatrix} a  b \\ c  d \end{pmatrix}$ 推导其[迭代矩阵](@entry_id:637346) [@problem_id:2207437]。根据定义，我们有：
$$ D = \begin{pmatrix} a  0 \\ 0  d \end{pmatrix}, \quad L = \begin{pmatrix} 0  0 \\ c  0 \end{pmatrix}, \quad U = \begin{pmatrix} 0  b \\ 0  0 \end{pmatrix} $$
首先计算 $(D + \omega L)$ 及其逆：
$$ D + \omega L = \begin{pmatrix} a  0 \\ \omega c  d \end{pmatrix} \implies (D + \omega L)^{-1} = \frac{1}{ad} \begin{pmatrix} d  0 \\ -\omega c  a \end{pmatrix} = \begin{pmatrix} 1/a  0 \\ -\omega c/(ad)  1/d \end{pmatrix} $$
接着计算 $((1-\omega)D - \omega U)$：
$$ (1-\omega)D - \omega U = \begin{pmatrix} (1-\omega)a  0 \\ 0  (1-\omega)d \end{pmatrix} - \begin{pmatrix} 0  \omega b \\ 0  0 \end{pmatrix} = \begin{pmatrix} (1-\omega)a  -\omega b \\ 0  (1-\omega)d \end{pmatrix} $$
最后，将两者相乘得到 $T_{SOR}(\omega)$：
$$ T_{SOR}(\omega) = \begin{pmatrix} 1/a  0 \\ -\omega c/(ad)  1/d \end{pmatrix} \begin{pmatrix} (1-\omega)a  -\omega b \\ 0  (1-\omega)d \end{pmatrix} = \begin{pmatrix} 1-\omega  -\frac{\omega b}{a} \\ \frac{-\omega c (1-\omega)}{d}  \frac{\omega^2 bc}{ad} + (1-\omega) \end{pmatrix} $$

线性[迭代法](@entry_id:194857) $\mathbf{x}^{(k+1)} = T \mathbf{x}^{(k)} + \mathbf{c}$ 收敛于唯一解的充要条件是[迭代矩阵](@entry_id:637346)的**谱半径（spectral radius）**小于1，即 $\rho(T) = \max_i |\lambda_i|  1$，其中 $\lambda_i$ 是 $T$ 的[特征值](@entry_id:154894)。对于SOR方法，这意味着收敛性完全由 $\rho(T_{SOR}(\omega))$ 决定。

一个至关重要的结论是关于$\omega$取值范围的。可以证明，SOR方法收敛的一个**必要条件**是 $0  \omega  2$。这个结论可以通过考察迭代[矩阵的[行列](@entry_id:148198)式](@entry_id:142978)来巧妙证明 [@problem_id:2444344]。[迭代矩阵](@entry_id:637346)所有[特征值](@entry_id:154894)的乘积等于其[行列式](@entry_id:142978)：
$$ \det(T_{SOR}(\omega)) = \prod_i \lambda_i $$
利用[行列式](@entry_id:142978)的性质 $\det(AB) = \det(A)\det(B)$ 和 $\det(A^{-1}) = 1/\det(A)$，我们有：
$$ \det(T_{SOR}(\omega)) = \frac{\det((1-\omega)D - \omega U)}{\det(D + \omega L)} $$
由于 $D+\omega L$ 是下[三角矩阵](@entry_id:636278)，$ (1-\omega)D-\omega U$ 是[上三角矩阵](@entry_id:150931)，它们的[行列式](@entry_id:142978)都等于其对角元素之积。$L$ 和 $U$ 是严格三角矩阵，对角线均为零。因此：
$$ \det(D + \omega L) = \det(D) $$
$$ \det((1-\omega)D - \omega U) = \det((1-\omega)D) = (1-\omega)^n \det(D) $$
所以，
$$ \det(T_{SOR}(\omega)) = \frac{(1-\omega)^n \det(D)}{\det(D)} = (1-\omega)^n $$
[谱半径](@entry_id:138984)定义为模最大的[特征值](@entry_id:154894)，因此它必然大于或等于所有[特征值](@entry_id:154894)模的几何平均值。这意味着：
$$ \rho(T_{SOR}(\omega))^n \ge \left| \prod_i \lambda_i \right| = |\det(T_{SOR}(\omega))| = |(1-\omega)^n| $$
$$ \rho(T_{SOR}(\omega)) \ge |1-\omega| $$
为了使迭代收敛，我们必须有 $\rho(T_{SOR}(\omega))  1$。这必然要求 $|1-\omega|  1$，解此不等式得到 $0  \omega  2$。这个结论表明，任何在 $(0, 2)$ 区间之外的 $\omega$ 值都无法保证收敛。特别是当 $\omega \ge 2$ 时，$\rho(T_{SOR}(\omega)) \ge |1-\omega| \ge 1$，迭代过程必然是发散的。

### 收敛的充分条件

虽然我们知道了[收敛的必要条件](@entry_id:157681)是 $0  \omega  2$，但这并不意味着在此区间内任意选择 $\omega$ 都能保证收敛。确定谱半径通常很困难，因此在实践中，我们常常依赖于关于矩阵 $A$ 本身的、更易于验证的**充分条件**。

一个广泛应用的充分条件是**[严格对角占优](@entry_id:154277)（strictly diagonally dominant）**。如果一个矩阵 $A$ 的每一行，其对角元素的[绝对值](@entry_id:147688)都严格大于该行所有非对角元素[绝对值](@entry_id:147688)之和，则称该矩阵为[严格对角占优矩阵](@entry_id:198320)。数学上表示为：
$$ |a_{ii}|  \sum_{j \neq i} |a_{ij}| \quad \text{for all } i=1, \dots, n $$
一个重要的定理（Kahan定理）指出：如果矩阵 $A$ 是[严格对角占优](@entry_id:154277)的，那么对于任意的 $\omega \in (0, 2)$，SOR方法都收敛。

例如，我们来判断以下几个矩阵是否满足此条件 [@problem_id:2207416]：
*   $A = \begin{pmatrix} 4  1  -1 \\ 2  -5  1 \\ -1  1  3 \end{pmatrix}$
    *   行1: $|4|  |1| + |-1| \implies 4  2$ (成立)
    *   行2: $|-5|  |2| + |1| \implies 5  3$ (成立)
    *   行3: $|3|  |-1| + |1| \implies 3  2$ (成立)
    矩阵 $A$ 是[严格对角占优](@entry_id:154277)的。

*   $C = \begin{pmatrix} 5  2  1 \\ -1  4  -3 \\ 2  -1  7 \end{pmatrix}$
    *   行1: $|5|  |2| + |1| \implies 5  3$ (成立)
    *   行2: $|4|  |-1| + |-3| \implies 4  4$ (不成立，必须严格大于)
    矩阵 $C$ 不是[严格对角占优](@entry_id:154277)的。

另一个至关重要的条件与矩阵的对称性和正定性有关。如果矩阵 $A$ 是**[对称正定](@entry_id:145886)（Symmetric Positive-Definite, SPD）**的，那么[SOR方法的收敛性](@entry_id:164310)有非常明确的结论。一个矩阵是SPD的，需满足：
1.  **对称性**：$A = A^T$。
2.  **[正定性](@entry_id:149643)**：对于所有非零向量 $\mathbf{x}$，都有 $\mathbf{x}^T A \mathbf{x}  0$。一个等价且更易于操作的判据（[Sylvester准则](@entry_id:150939)）是：矩阵的所有主子式（leading principal minors）均为正。

**Ostrowski-Reich定理**指出：如果 $A$ 是一个[对称正定矩阵](@entry_id:136714)，那么SOR方法收敛的充要条件是 $0  \omega  2$。这是一个非常强大的结论，因为它将收敛性问题完全归结为 $\omega$ 的选择。

让我们来检验一个矩阵是否为SPD矩阵 [@problem_id:2207414]：
$A = \begin{pmatrix} 4  2 \\ 2  3 \end{pmatrix}$
1.  **对称性**: $a_{12} = 2, a_{21} = 2$。矩阵是对称的。
2.  **[正定性](@entry_id:149643)**:
    *   一阶主子式: $M_1 = 4  0$。
    *   二阶主子式: $M_2 = \det(A) = (4)(3) - (2)(2) = 12 - 4 = 8  0$。
由于所有主子式都为正，该矩阵是正定的。因此，矩阵 $A$ 是SPD矩阵，SOR方法对它收敛当且仅当 $\omega \in (0, 2)$。

### [最优松弛因子](@entry_id:166574)

既然SOR方法的[收敛速度](@entry_id:636873)依赖于 $\omega$，一个自然的问题是：是否存在一个**[最优松弛因子](@entry_id:166574)** $\omega_{opt}$，使得谱半径 $\rho(T_{SOR}(\omega))$ 最小，从而收敛最快？

答案是肯定的，尽管找到 $\omega_{opt}$ 通常非常困难。然而，对于一类在应用中非常重要的特殊矩阵——**一致有序（consistently ordered）**矩阵，存在关于 $\omega_{opt}$ 的优美理论。这类矩阵常见于用[中心差分格式](@entry_id:747203)离散二维或三维区域上的椭圆型[偏微分方程](@entry_id:141332)（如拉普拉斯方程）所得到的线性系统中。

对于这类矩阵，SOR[迭代矩阵](@entry_id:637346) $T_{SOR}$ 的[特征值](@entry_id:154894) $\lambda$ 与相应的雅可比（Jacobi）[迭代矩阵](@entry_id:637346) $B_J = -D^{-1}(L+U)$ 的[特征值](@entry_id:154894) $\mu$ 之间存在一个精确的关系（由David Young推导）：
$$ (\lambda + \omega - 1)^2 = \lambda \omega^2 \mu^2 $$
通过分析这个关系，可以找到最小化 $|\lambda|$ 的 $\omega$ 值。若[雅可比迭代](@entry_id:139235)收敛（即其谱半径 $\rho_J = \rho(B_J)  1$），且其[特征值](@entry_id:154894)均为实数，则[最优松弛因子](@entry_id:166574)由下式给出：
$$ \omega_{opt} = \frac{2}{1 + \sqrt{1 - \rho_J^2}} $$
此时，SOR方法的[谱半径](@entry_id:138984)为 $\rho(T_{SOR}(\omega_{opt})) = \omega_{opt} - 1$。

一个经典的应用场景是求解单位正方形区域上的[拉普拉斯方程](@entry_id:143689)，使用五点差分格式，并将内部[区域划分](@entry_id:748628)为 $n \times n$ 的网格 [@problem_id:2207399]。对于这种情况，可以证明[雅可比迭代](@entry_id:139235)矩阵的[谱半径](@entry_id:138984)为：
$$ \rho_J = \cos\left(\frac{\pi}{n+1}\right) $$
将此代入 $\omega_{opt}$ 的公式，我们得到：
$$ \omega_{opt} = \frac{2}{1 + \sqrt{1 - \cos^2\left(\frac{\pi}{n+1}\right)}} = \frac{2}{1 + \sin\left(\frac{\pi}{n+1}\right)} $$
例如，如果一个网格有 $n=99$ 个内部点，那么[最优松弛因子](@entry_id:166574)为：
$$ \omega_{opt} = \frac{2}{1 + \sin\left(\frac{\pi}{100}\right)} \approx \frac{2}{1 + 0.03141} \approx 1.939 $$
这个值非常接近[收敛区间](@entry_id:146678)的[上界](@entry_id:274738)2。事实上，当 $n$ 很大时，$\sin(\pi/(n+1)) \approx \pi/(n+1)$，$\omega_{opt}$ 渐近于 $2 - \frac{2\pi}{n+1}$。使用这个最优值可以极大地加速收敛，相比于[高斯-赛德尔法](@entry_id:145727)（$\omega=1$），其收敛所需的迭代次数可以减少一个[数量级](@entry_id:264888)。

### 并行性与数据依赖

在现代计算中，利用多处理器进行[并行计算](@entry_id:139241)是提高求解速度的关键。然而，不同迭代算法的并行性有很大差异。

[雅可比方法](@entry_id:270947)的更新公式为：
$$ x_i^{(k+1)} = \frac{1}{a_{ii}} \left( b_i - \sum_{j \neq i} a_{ij}x_j^{(k)} \right) $$
注意到，在计算第 $k+1$ 步的所有新分量时，[雅可比法](@entry_id:147508)**只**依赖于第 $k$ 步的旧值。这意味着所有分量 $x_i^{(k+1)}$ 的计算是相互独立的，可以同时在不同的处理器上进行。这种特性使得[雅可比法](@entry_id:147508)具有天然的高度并行性，或称“尴尬并行”（embarrassingly parallel）。

相比之下，SOR方法的[并行化](@entry_id:753104)则要复杂得多 [@problem_id:2207422]。回顾其更新公式：
$$ x_i^{(k+1)} = \dots - \frac{\omega}{a_{ii}} \sum_{j=1}^{i-1} a_{ij}x_j^{(k+1)} - \dots $$
计算 $x_i^{(k+1)}$ 依赖于在**同一次迭代**中已经计算出的 $x_1^{(k+1)}, \dots, x_{i-1}^{(k+1)}$。这种**迭代内[数据依赖](@entry_id:748197)（intra-iteration data dependency）**是SOR方法顺序性的根源。如果采用自然排序（例如，对二维网格按行逐点编号），计算第 $i$ 个点的值必须等待第 $i-1$ 个点计算完成。这种依赖关系形成了一个计算“[波前](@entry_id:197956)”，它必须按顺序扫过整个计算域，从而严重限制了并行度。

为了克服这种顺序性限制，研究人员开发了不同的更新顺序。其中最著名的是**[红黑排序](@entry_id:147172)（red-black ordering）**。在二维网格问题中，我们可以像棋盘一样将节点交替染成“红色”和“黑色”。一个红色节点的所有邻居都是黑色节点，反之亦然。这样，更新所有红色节点时，它们各自的计算只依赖于旧的黑色节点值，因此所有红色节点可以完全并行地更新。在所有红色节点更新完毕后，再并行地更新所有黑色节点，因为它们的计算现在依赖于刚刚更新的红色节点值。这种策略将一次完全串行的扫描分解为两次并行的半扫描，从而在[并行计算](@entry_id:139241)机上恢复了大量的计算效率，使得SOR方法及其变种在[高性能计算](@entry_id:169980)中仍占有一席之地。