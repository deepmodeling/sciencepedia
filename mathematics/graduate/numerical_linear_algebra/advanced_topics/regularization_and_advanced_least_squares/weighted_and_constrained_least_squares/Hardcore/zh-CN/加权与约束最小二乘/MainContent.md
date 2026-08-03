## 引言
最小二乘法是数据科学与工程计算的基石，旨在通过最小化误差平方和来寻找数据的最佳函数匹配。然而，其一个基本假设——所有测量误差都具有相同的方差且互不相关——在现实世界中常常难以满足。当不同数据的可靠性存在差异，或解必须满足特定的物理定律时，标准方法便显得力不从心。为了解决这一知识鸿沟，本文系统地介绍了两种强大的扩展技术：加权最小二乘法（WLS）与约束最小二乘法（CLS），旨在为读者构建一个从理论到实践的完整知识体系。

在接下来的章节中，您将首先通过“原理与机制”深入学习WLS和CLS背后的统计学动机与代数结构，并重点掌握如何通过稳健的数值算法（如QR分解）来高效求解，以避免数值陷阱。随后，在“应用与交叉学科联系”一章，我们将跨越学科边界，展示这些理论在生物化学、计算金融、机器学习等领域的广泛应用，揭示它们如何作为一种通用语言将领域知识与实验数据相结合。最后，通过“动手实践”部分的编程练习，您将有机会把理论知识转化为解决实际问题的能力。

## 原理与机制

在前一章中，我们介绍了最小二乘法的基本概念，它旨在最小化模型预测与观测数据之间的欧几里得距离。然而，在许多科学与工程应用中，一个核心假设——即所有测量误差都是独立且同分布（i.i.d.）的——往往不成立。某些测量可能比其他测量更精确，或者不同测量之间的误差可能存在相关性。本章将深入探讨处理此类问题的两种高级技术：**加权最小二乘法（Weighted Least Squares, WLS）** 和 **约束最小二乘法（Constrained Least Squares）**。我们将从基本原理出发，阐明其统计学动机和代数结构，重点关注数值求解方法的稳定性和效率，并最终探讨如何将这些思想应用于等式约束下的优化问题。

### 加权最小二乘法 (Weighted Least Squares)

#### 从统计推断到加权范数 (From Statistical Inference to Weighted Norms)

标准最小二乘法旨在解决超定线性系统 $Ax \approx b$，其目标是最小化残差的欧几里得范数平方，即 $\min_{x} \|Ax - b\|_2^2$。这一目标的背后，隐含着一个统计假设：观测向量 $b$ 是由真实模型 $Ax_{true}$ 加上一个零均值、具有单位协方差矩阵（$Cov(\varepsilon) = \sigma^2 I$）的噪声向量 $\varepsilon$ 构成的，即 $b = Ax_{true} + \varepsilon$。在这种情况下，最小二乘估计量是最佳线性无偏估计量（Best Linear Unbiased Estimator, BLUE），并且与高斯噪声假设下的**最大似然估计（Maximum Likelihood Estimation, MLE）**等价。

然而，当测量误差既不等方差（异方差性，heteroscedasticity）也非不相关（correlation）时，噪声的协方差矩阵 $\Sigma$ 就不再是单位矩阵的倍数。假设噪声向量 $\varepsilon = b - Ax$ 服从均值为零、协方差矩阵为 $\Sigma$ 的多元高斯分布，即 $\varepsilon \sim \mathcal{N}(0, \Sigma)$。其概率密度函数为：
$$
p(\varepsilon) \propto \exp\left(-\frac{1}{2} \varepsilon^{\top} \Sigma^{-1} \varepsilon\right)
$$
为了找到最可能产生观测数据 $b$ 的参数 $x$，我们最大化似然函数 $L(x|b)$，这等价于最小化负对数似然函数。负对数似然函数与以下项成正比：
$$
(b - Ax)^{\top} \Sigma^{-1} (b - Ax)
$$
这个表达式被称为残差向量 $r(x) = b-Ax$ 的**马氏距离（Mahalanobis distance）**的平方。它自然地引出了加权最小二乘的目标函数。

我们定义一个**加权最小二乘问题**，其目标是最小化残差的加权范数平方：
$$
\min_{x} \|Ax - b\|_{W}^{2} = (Ax - b)^{\top} W (Ax - b)
$$
其中，$W$ 是一个对称正定（Symmetric Positive Definite, SPD）的**权重矩阵**。从统计学的角度看，最优的权重矩阵是逆协方差矩阵，$W = \Sigma^{-1}$ [@problem_id:3601228]。直观地说，协方差矩阵 $\Sigma$ 的对角线元素较大表示该分量的噪声方差较大（即测量不确定性高），因此其在逆矩阵 $\Sigma^{-1}$ 中对应的权重较小。这确保了更精确的测量（低方差）在确定解 $x$ 时起更大作用，而噪声较大的测量（高方差）则被赋予较小的影响。

#### 预白化：将加权问题转化为标准问题 (Prewhitening: Transforming a Weighted Problem to a Standard One)

加权最小二乘问题虽然形式上有所不同，但可以通过一个精妙的代数变换回归到我们熟悉标准最小二乘问题。由于权重矩阵 $W$ 是对称正定的，它必然存在一个“平方根”分解，即可以找到一个可逆矩阵 $C$ 使得 $W = C^{\top}C$。例如，$W$ 的 **Cholesky 分解** $W = LL^{\top}$（$L$ 是下三角矩阵）可以提供这样一个矩阵（取 $C = L^{\top}$），或者通过谱分解得到的对称平方根 $W^{1/2}$ 也是一个选择。

利用这个分解，我们可以重写目标函数：
$$
(Ax - b)^{\top} W (Ax - b) = (Ax - b)^{\top} C^{\top} C (Ax - b) = (C(Ax - b))^{\top} (C(Ax - b)) = \|C(Ax - b)\|_{2}^{2}
$$
令 $\tilde{A} = CA$ 和 $\tilde{b} = Cb$，则原加权最小二乘问题等价于以下标准最小二乘问题 [@problem_id:3601203]：
$$
\min_{x} \|\tilde{A}x - \tilde{b}\|_{2}^{2}
$$
这个过程被称为**预白化（prewhitening）**或白化。其统计学意义在于，如果原始噪声 $\varepsilon$ 的协方差为 $\Sigma$，那么变换后的噪声 $\tilde{\varepsilon} = C\varepsilon$ 的协方差为 $C \Sigma C^{\top}$。若我们选择 $W = \Sigma^{-1}$，并通过 Cholesky 分解 $\Sigma = LL^{\top}$ 构造白化矩阵 $C=L^{-1}$，则新噪声的协方差为：
$$
\text{Cov}(\tilde{\varepsilon}) = L^{-1} \Sigma (L^{-1})^{\top} = L^{-1} (LL^{\top}) (L^{\top})^{-1} = I
$$
这意味着变换后的噪声分量是方差为1且互不相关的，即“白噪声”，这正是标准最小二乘法的理想假设环境 [@problem_id:3601228]。

### 加权最小二乘的数值解法与稳定性 (Numerical Solution and Stability of WLS)

预白化不仅为 WLS 提供了理论上的简化，更重要的是，它指明了一条通往数值稳健解法的道路。

#### 正规方程法及其数值陷阱 (The Normal Equations Method and its Numerical Pitfalls)

与标准最小二乘类似，我们可以通过对 WLS 目标函数求导并令其为零，得到**加权正规方程（weighted normal equations）**：
$$
(A^{\top} W A) x = A^{\top} W b
$$
当 $A$ 具有列满秩且 $W$ 为正定时，$A^{\top} W A$ 是可逆的，系统存在唯一解。然而，在有限精度浮点运算中，**显式地计算并求解正规方程是一种数值上不稳定的做法**。

其根本原因在于矩阵乘积 $A^{\top} W A$ 会“平方”问题的条件数。令 $\tilde{A} = C A$（其中 $W = C^{\top}C$），则正规方程的矩阵可以写作 $\tilde{A}^{\top}\tilde{A}$。对于任何列满秩矩阵 $\tilde{A}$，其 Gram 矩阵 $\tilde{A}^{\top}\tilde{A}$ 的谱条件数是 $\tilde{A}$ 本身条件数的平方 [@problem_id:3601199] [@problem_id:3601216]：
$$
\kappa_{2}(A^{\top} W A) = \kappa_{2}(\tilde{A}^{\top} \tilde{A}) = \kappa_{2}(\tilde{A})^{2} = \kappa_{2}(CA)^{2}
$$
条件数是衡量问题对输入扰动敏感度的指标。如果 $\kappa_{2}(\tilde{A}) = 10^k$，那么 $\kappa_{2}(A^{\top} W A) = 10^{2k}$。在双精度浮点数运算中（机器精度 $u \approx 10^{-16}$），如果 $\kappa_{2}(\tilde{A})$ 超过 $10^8$，那么 $\kappa_{2}(A^{\top} W A)$ 将接近 $10^{16}$，此时矩阵在计算上已与奇异矩阵无异，求解过程中会发生灾难性的精度损失。

这种精度损失可以用**后向误差（backward error）**的概念来量化。一个数值稳定的算法应该为一个问题计算出一个解 $\tilde{x}$，该解是某个稍有扰动的“邻近”问题的精确解。对于WLS问题，我们可以定义后向误差为使 $\tilde{x}$ 成为扰动问题 $W((A+\Delta A)\tilde{x} - (b+\Delta b)) = 0$ 精确解的最小相对扰动 $\|\Delta A, \Delta b\|$ [@problem_id:3601192]。通过正规方程法得到的解，其前向误差（即与真实解的差距）通常与 $\kappa_{2}(CA)^{2}$ 成正比，而更稳定的方法可以得到与 $\kappa_{2}(CA)$ 成正比的误差界 [@problem_id:3601247]。

尽管存在数值缺陷，但在某些特殊情况下，例如当 $A^{\top}WA$ 具有高度稀疏性且问题本身良态（$\kappa_{2}(CA)$很小）时，为了追求计算效率，正规方程法仍可能是一个可接受的选择 [@problem_id:3601247]。

#### 正交化方法：一种稳健的替代方案 (Orthogonalization Methods: A Robust Alternative)

鉴于正规方程的数值不稳定性，首选的稳健算法是基于预白化和**正交分解**。该方法避免了 Gram 矩阵的形成，其步骤如下：

1.  **分解权重矩阵**：对权重矩阵 $W$ 进行 Cholesky 分解，得到 $W = R^{\top}R$，其中 $R$ 是一个上三角矩阵。

2.  **预白化系统**：构造变换后的矩阵和向量 $\tilde{A} = RA$ 和 $\tilde{b} = Rb$。

3.  **求解标准最小二乘**：对变换后的问题 $\min_{x} \|\tilde{A}x - \tilde{b}\|_{2}^{2}$ 使用 **QR 分解**。即计算 $\tilde{A}$ 的 QR 分解 $\tilde{A} = QR_{qr}$（这里 $R_{qr}$ 是上三角阵，区别于 Cholesky 因子 $R$），然后通过求解三角系统 $R_{qr}x = Q^{\top}\tilde{b}$ 来得到解 $x$。

此方法的优越性在于 QR 分解是通过一系列正交变换（如 Householder 反射或 Givens 旋转）完成的，这些变换不会放大舍入误差。因此，整个求解过程的数值稳定性由 $\kappa_2(\tilde{A})$ 控制，而非其平方。

当矩阵 $A$（或 $\tilde{A}$）可能秩亏或接近秩亏时，应使用**带列主元的 QR 分解（QR with Column Pivoting, QRCP）**。QRCP 会在分解过程中对列进行重排，将线性无关性最强的列排在前面，从而可靠地揭示矩阵的数值秩，并计算出一个可靠的解 [@problem_id:3601199]。

一个值得注意的理论要点是，预白化[变换矩阵](@entry_id:151616) $C$ 的选择（例如，Cholesky 因子 $L^{\top}$ 或对称平方根 $W^{1/2}$）虽然会改变 $\tilde{A}$ 的具体形式，但不会改变其条件数。任何满足 $W = C^{\top}C$ 的两个矩阵 $C_1$ 和 $C_2$ 都通过一个正交矩阵 $U$ 相关联（$C_2 = UC_1$）。由于正交变换不改变奇异值，因此 $\kappa_2(C_1 A) = \kappa_2(C_2 A)$ [@problem_id:3601203]。这意味着预白化后的问题的内在敏感性是固定的，与“平方根”矩阵的具体选择无关。

### 半正定加权：处理非唯一解 (Semidefinite Weighting: Handling Non-unique Solutions)

在某些应用中，权重矩阵 $W$ 可能只是**半正定（Positive Semidefinite, PSD）**的，而非严格正定。这通常发生在某些测量完全不可信（方差无穷大）或根本不存在的情况下，此时 $W$ 的对角线上会出现零。

当 $W$ 是奇异的，Hessian 矩阵 $A^{\top}WA$ 也可能是奇异的，即使 $A$ 本身是列满秩的。这会导致 WLS 问题的解不唯一。具体来说，如果 $A^{\top}WA$ 的零空间非平凡，即存在非零向量 $z$ 使得 $(A^{\top}WA)z = 0$，那么若 $x^*$ 是一个解，则 $x^* + \alpha z$ 对于任意标量 $\alpha$ 都是解。这是因为目标函数的值在 $x^*$ 和 $x^* + \alpha z$ 处是相同的：
$$
J(x^* + \alpha z) = (x^*+\alpha z)^{\top}(A^{\top}WA)(x^*+\alpha z) - \dots = J(x^*)
$$
这种情况的发生，是因为 $z$ 位于 $A^{\top}WA$ 的零空间，等价于 $z$ 位于 $W^{1/2}A$ 的零空间。这意味着向量 $Az$ 只在被 $W$ 完全忽略的那些分量上非零。例如，如果 $W = \text{diag}(1, 1, 0, 1)$，那么 $Az$ 的形式必然是 $(0, 0, c, 0)^{\top}$，其中 $c$ 是某个常数。解集因此形成一个仿射子空间 [@problem_id:3601200]。

为了从无限多的解中选择一个，我们需要引入一个额外的准则。最常见的选择是寻找所有解中**欧几里得范数最小**的解。这个唯一的最小范数解可以通过**摩尔-彭若斯广义逆（Moore-Penrose Generalized Inverse）**来表示：
$$
x^{\dagger} = (A^{\top} W A)^{\dagger} A^{\top} W b
$$
这个解是正规方程 $A^{\top}WAx=A^{\top}Wb$ 的所有解中唯一一个位于 $A^{\top}WA$ 的值域空间中的解，这等价于它与 $A^{\top}WA$ 的零空间正交 [@problem_id:3601200]。

### 约束最小二乘问题 (Constrained Least Squares Problems)

许多实际问题不仅要求我们最小化残差，还要求解满足一组线性等式约束。这类问题统称为**等式约束最小二乘（Equality Constrained Least Squares, ECLS）**问题。我们将讨论其两种主要形式及求解方法。

一个典型的 ECLS 问题形式如下：
$$
\min_{x \in \mathbb{R}^{n}} \|Ax - b\|_{W}^{2} \quad \text{subject to} \quad Cx = d
$$
其中 $C \in \mathbb{R}^{p \times n}$ 是约束矩阵，$d \in \mathbb{R}^{p}$ 是约束向量。通常假设 $C$ 具有行满秩，以保证约束是相容且非冗余的。

#### 拉格朗日乘子法与值域空间法 (Lagrange Multipliers and the Range-Space Method)

解决 ECLS 问题的经典方法是**拉格朗日乘子法**。我们构造拉格朗日函数：
$$
\mathcal{L}(x, \lambda) = \frac{1}{2}(Ax - b)^{\top} W (Ax - b) + \lambda^{\top}(Cx - d)
$$
其中 $\lambda \in \mathbb{R}^{p}$ 是拉格朗日乘子向量。通过对 $x$ 和 $\lambda$ 分别求偏导并令其为零，我们得到一阶最优性条件，即 **KKT (Karush-Kuhn-Tucker) 系统**：
$$
\begin{pmatrix}
A^{\top}WA  C^{\top} \\
C  0
\end{pmatrix}
\begin{pmatrix}
x \\
\lambda
\end{pmatrix}
=
\begin{pmatrix}
A^{\top}Wb \\
d
\end{pmatrix}
$$
这是一个对称但非正定的鞍点系统。**值域空间法（Range-Space Method）**通过从该系统中消去 $x$ 来求解。从第一行方程，我们得到（假设 $A^{\top}WA$ 可逆）：
$$
x = (A^{\top}WA)^{-1}(A^{\top}Wb - C^{\top}\lambda)
$$
将其代入第二行约束方程 $Cx=d$ 中，得到一个只关于 $\lambda$ 的 $p \times p$ 线性系统：
$$
\left(C(A^{\top}WA)^{-1}C^{\top}\right) \lambda = C(A^{\top}WA)^{-1}A^{\top}Wb - d
$$
这个系统的矩阵 $S = C(A^{\top}WA)^{-1}C^{\top}$ 被称为 KKT 矩阵关于 $A^{\top}WA$ 的**舒尔补（Schur complement）**。在 $A$ 列满秩和 $C$ 行满秩的条件下，$S$ 是对称正定的，因此可以用 Cholesky 分解等高效方法求解 [@problem_id:3601210]。求出 $\lambda$ 后，再代回即可求得 $x$。

当约束数量 $p$ 远小于变量维度 $n$ 时 ($p \ll n$)，求解这个小的 $p \times p$ 系统通常比处理大的原始 KKT 系统更高效。此外，在迭代求解中，可以采用**无矩阵（matrix-free）**方法，通过共轭梯度法（CG）求解关于 $\lambda$ 的系统，而无需显式构造 $S$。每次 CG 迭代仅需要计算一次 $S$ 与向量的乘积，这可以通过求解一次形如 $(A^{\top}WA)z=v$ 的系统来完成 [@problem_id:3601210]。

#### 零空间法 (The Null-Space Method)

与值域空间法形成对偶的是**零空间法（Null-Space Method）**。该方法的核心思想是对可行集进行参数化。任何满足约束 $Cx=d$ 的解 $x$ 都可以表示为：
$$
x = x_0 + Nz
$$
其中，$x_0$ 是约束方程 $Cx=d$ 的一个**特解**（$Cx_0=d$），而 $N$ 是一个矩阵，其列向量构成了约束矩阵 $C$ 的**零空间（null space）**的一组基。如果 $C$ 的秩为 $p$，则其零空间的维度为 $n-p$，因此 $N \in \mathbb{R}^{n \times (n-p)}$，$z \in \mathbb{R}^{n-p}$ 是新的自由变量。

将此参数化代入 WLS 目标函数，原约束问题就转化为一个关于 $z$ 的无约束 WLS 问题：
$$
\min_{z \in \mathbb{R}^{n-p}} \|A(x_0 + Nz) - b\|_{W}^{2} = \min_{z} \|(AN)z - (b - Ax_0)\|_{W}^{2}
$$
这个问题可以通过前面讨论的稳健正交化方法求解。求得最优的 $z^*$ 后，原问题的解即为 $x^* = x_0 + Nz^*$ [@problem_id:3601246]。

零空间法在自由度数量 $n-p$ 远小于变量维度 $n$ 时（即约束非常多时）特别有效。此时，归约后的问题维度很小，求解成本低。

#### 方法选择与几何直观 (Method Selection and Geometric Intuition)

值域空间法和零空间法提供了解决 ECLS 问题的两种强大而互补的途径。选择哪种方法主要取决于问题的维度：
-   如果约束数量 $p$ 很小，则值域空间法更优，因为它归结为求解一个小的 $p \times p$ 系统。
-   如果约束数量 $p$ 很大（接近 $n$），从而自由度 $n-p$ 很小，则零空间法更优，因为它归结为求解一个小的 $(n-p) \times (n-p)$ 系统。

从几何角度看，约束 $Cx=d$ 定义了一个仿射子空间（例如，三维空间中的一条直线或一个平面）。约束最小二乘问题，就是在这个仿射子空间中寻找一个点 $x^*$，使其与无约束最小二乘问题的解“最近”。这里的“距离”是由加权范数 $\| \cdot \|_{A^{\top}WA}$ 定义的。

一个特别直观的例子是**加权最小范数问题**：$\min \|x\|_{W}^{2}$ s.t. $Ax=b$。这是一个在欠定系统 $Ax=b$ 的解空间中寻找“最小”解的问题。当 $W=I$ 时，问题是寻找离原点欧几里得距离最近的解，该解是原点到解空间的正交投影。当 $W \neq I$ 时，我们最小化的是加权范数，这相当于在由 $W$ 定义的椭球几何中寻找离原点最近的解。不同的 $W$ 改变了距离的定义，从而改变了“正交”和“投影”的几何概念，最终选出不同的最优解 [@problem_id:3601217]。

总之，加权与约束最小二乘法是解决现实世界中复杂数据拟合与优化问题的关键工具。理解其背后的统计原理、代数结构以及数值求解的微妙之处，对于任何从事科学计算与数据分析的研究者来说都至关重要。