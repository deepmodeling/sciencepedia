## 引言
在现代[科学计算](@entry_id:143987)与数据分析的核心，普遍存在着一类根本性挑战：求解维度高达数百万甚至数十亿的[线性方程组](@entry_id:148943) $Ax=b$ 或[特征值问题](@entry_id:142153) $Ax=\lambda x$。无论是模拟气候变化、设计下一代飞行器，还是从海量数据中提取模式，这些大规模问题都因其巨大的计算需求，使得传统的高斯消元等直接解法变得不切实际。这道鸿沟催生了迭代方法的兴起，而在众多迭代方法中，基于[克雷洛夫子空间](@entry_id:751067)（Krylov Subspace）的方法以其优雅的理论、卓越的效率和广泛的适用性，脱颖而出，成为现代数值线性代数的基石。

本文旨在为读者提供一份关于[克雷洛夫子空间](@entry_id:751067)的全面而深入的指南。我们将不仅仅停留在理论层面，而是将理论、应用与实践紧密结合，带领读者开启一场从抽象概念到具体应用的探索之旅。文章主体分为三个核心部分：
-   在第一章 **“原理与机制”** 中，我们将从第一性原理出发，系统阐述[克雷洛夫子空间](@entry_id:751067)的定义、关键性质，并深入剖析构建其标准正交基的核心算法——Arnoldi和[Lanczos过程](@entry_id:751124)。
-   接下来，在第二章 **“应用与交叉学科联系”** 中，我们将视野拓宽，展示克雷洛夫方法如何在[偏微分方程](@entry_id:141332)求解、计算化学、机器学习和控制理论等不同领域大放异彩，揭示其作为[通用计算](@entry_id:275847)[范式](@entry_id:161181)的强大生命力。
-   最后，在 **“动手实践”** 部分，我们精选了一系列计算问题，旨在通过具体的动手练习，将理论知识转化为可操作的技能，加深对CG、GMRES等经典算法内在逻辑的理解。

为了真正驾驭这些强大的工具，我们必须首先牢固掌握其基本原理。我们的探索之旅将从下一章开始，在那里我们将从零开始，解构克雷洛夫子空间的核心机制。

## 原理与机制

本章旨在深入探讨[克雷洛夫子空间](@entry_id:751067)的核心原理与内在机制。在前一章介绍其背景与重要性之后，我们将从第一性原理出发，系统地阐述[克雷洛夫子空间](@entry_id:751067)的定义、性质、构造方法及其在[求解大型线性系统](@entry_id:145591)和[特征值问题](@entry_id:142153)中的关键作用。我们将通过一系列精心设计的例子，逐步揭示这些[子空间](@entry_id:150286)何以成为现代计算科学中功能强大且应用广泛的工具。

### [克雷洛夫子空间](@entry_id:751067)的基本定义与性质

克雷洛夫子空间是迭代方法的核心，其定义简洁而深刻。对于一个 $n \times n$ 的方阵 $A$ 和一个非零向量 $b \in \mathbb{C}^n$，由 $A$ 和 $b$ 生成的 $m$ 阶 **[克雷洛夫子空间](@entry_id:751067) (Krylov subspace)**，记作 $\mathcal{K}_m(A, b)$，是由向量序列 $b, Ab, A^2b, \dots, A^{m-1}b$ 张成的[线性子空间](@entry_id:151815)：
$$
\mathcal{K}_m(A, b) = \operatorname{span}\{b, Ab, A^2b, \dots, A^{m-1}b\}
$$
这个定义表明，[克雷洛夫子空间](@entry_id:751067)捕捉了矩阵 $A$ 重复作用于初始向量 $b$ 所产生的动态行为。向量 $A^k b$ 可以看作是初始“信号” $b$ 经过一个由 $A$ 描述的[线性动力系统](@entry_id:150282)演化 $k$ 步之后的状态。因此，$\mathcal{K}_m(A, b)$ 是该系统在前 $m$ 步演化轨迹所处的[子空间](@entry_id:150286)。

#### [子空间](@entry_id:150286)的维度与最小多项式

一个自然的问题是：克雷洛夫子空间的维度 $\dim \mathcal{K}_m(A, b)$ 是如何随 $m$ 增长的？显然，$\mathcal{K}_1(A, b) \subseteq \mathcal{K}_2(A, b) \subseteq \dots$，且 $\dim \mathcal{K}_m(A, b) \le \min(m, n)$。维度的增长何时停止？

答案与向量 $b$ 关于矩阵 $A$ 的 **最小多项式 (minimal polynomial)** $\mu_{A,b}(x)$ 密切相关。$\mu_{A,b}(x)$ 是指次数最低的[首一多项式](@entry_id:152311)（最高次项系数为1），使得 $\mu_{A,b}(A)b = 0$。如果 $\mu_{A,b}(x)$ 的次数为 $d$，那么向量序列 $\{b, Ab, \dots, A^{d-1}b\}$ 是线性无关的，而 $A^d b$ 可以表示为该序[列的线性组合](@entry_id:150240)。这意味着 $\mathcal{K}_d(A, b)$ 的维度为 $d$，并且对于任何 $m > d$，$\mathcal{K}_m(A, b) = \mathcal{K}_d(A, b)$，维度不再增长。因此，$d = \dim \mathcal{K}_n(A, b)$ 是该克雷洛夫序列所能达到的最大维度。

一个简单的例子可以阐明这一点。考虑一个 $3 \times 3$ 矩阵 $A=\begin{bmatrix}3  1  0 \\ 0  3  1 \\ 0  0  3\end{bmatrix}$ 和起始向量 $b=e_1=\begin{bmatrix}1 \\ 0 \\ 0\end{bmatrix}$ [@problem_id:3554222]。直接计算可知 $Ab = \begin{bmatrix}3 \\ 0 \\ 0\end{bmatrix} = 3b$。这表明 $(A-3I)b = 0$。因此，[最小多项式](@entry_id:153598)为 $\mu_{A,b}(x) = x-3$，其次数为 $d=1$。这意味着向量序列 $\{b, Ab, A^2b, \dots\}$ 中的所有向量都是 $b$ 的标量倍。因此，对于任何 $m \ge 1$，$\mathcal{K}_m(A,b) = \operatorname{span}\{b\}$，其维度恒为 $1$。

为了更深刻地理解维度的增长与饱和，我们可以考察一个更一般的情形，即 $A$ 是一个 $J \times J$ 的单[若尔当块](@entry_id:155003) ([Jordan block](@entry_id:148136)) [@problem_id:3554217]。设 $A = J_J(\lambda)$，其[若尔当链](@entry_id:148736)为 $\{v_1, \dots, v_J\}$，其中 $(A-\lambda I)v_1 = 0$ 且 $(A-\lambda I)v_i = v_{i-1}$。令初始向量 $b = \sum_{i=1}^J c_i v_i$，并设 $s = \max\{i \mid c_i \neq 0\}$ 是 $b$ 在该链上最深的非零分量的索引。通过分析尼尔幂算子 $N = A - \lambda I$ 的作用，可以证明，向量组 $\{b, Nb, \dots, N^{s-1}b\}$ 是线性无关的，而 $N^s b = 0$。这意味着克雷洛夫子空间的维度将[线性增长](@entry_id:157553)直到第 $s$ 步，然后饱和。具体而言，维度的表达式为：
$$
\dim \mathcal{K}_k(A, b) = \min(k, s)
$$
这个结果清晰地表明，[克雷洛夫子空间](@entry_id:751067)的最终维度由初始向量 $b$ 在与矩阵 $A$ 的谱结构相关的基（即[若尔当链](@entry_id:148736)）中的“[有效长度](@entry_id:184361)” $s$ 决定。

#### 仿射变换下的[不变性](@entry_id:140168)

克雷洛夫子空间的一个非常重要的性质是其在矩阵的 **仿射变换 (affine transformation)** 下的不变性。对于任何非零标量 $\alpha$ 和标量 $\beta$，只要 $\alpha \neq 0$，我们有：
$$
\mathcal{K}_m(\alpha A + \beta I, b) = \mathcal{K}_m(A, b)
$$
这个结论可以从第一性原理推导得出 [@problem_id:3554240]。一方面，$(\alpha A + \beta I)b = \alpha(Ab) + \beta b$，它是 $b$ 和 $Ab$ 的线性组合，因此属于 $\mathcal{K}_2(A,b)$。通过归纳法，可以证明任何 $(\alpha A + \beta I)^k b$ 都在 $\mathcal{K}_{k+1}(A,b)$ 中，这意味着 $\mathcal{K}_m(\alpha A + \beta I, b) \subseteq \mathcal{K}_m(A, b)$。另一方面，由于 $\alpha \neq 0$，我们可以反向求解 $Ab = \frac{1}{\alpha}[(\alpha A + \beta I)b - \beta b]$，这表明 $Ab$ 属于 $\mathcal{K}_2(\alpha A + \beta I, b)$。类似地，可以证明 $\mathcal{K}_m(A, b) \subseteq \mathcal{K}_m(\alpha A + \beta I, b)$。

例如，对于矩阵 $A=\begin{bmatrix}0  1 \\ -2  -3\end{bmatrix}$ 和向量 $b=\begin{bmatrix}1 \\ 0\end{bmatrix}$，我们可以显式计算[基向量](@entry_id:199546)。
对于 $\mathcal{K}_2(A, b)$，[基向量](@entry_id:199546)是 $b = \begin{bmatrix}1 \\ 0\end{bmatrix}$ 和 $Ab = \begin{bmatrix}0 \\ -2\end{bmatrix}$。
对于 $\mathcal{K}_2(A+5I, b)$，[基向量](@entry_id:199546)是 $b = \begin{bmatrix}1 \\ 0\end{bmatrix}$ 和 $(A+5I)b = \begin{bmatrix}5 \\ -2\end{bmatrix}$。
对于 $\mathcal{K}_2(2A, b)$，[基向量](@entry_id:199546)是 $b = \begin{bmatrix}1 \\ 0\end{bmatrix}$ 和 $(2A)b = \begin{bmatrix}0 \\ -4\end{bmatrix}$。
在这三种情况下，尽管第二个[基向量](@entry_id:199546)不同，但它们张成的[子空间](@entry_id:150286)是相同的（都是 $\mathbb{R}^2$）。由这些[基向量](@entry_id:199546)构成的矩阵的行列式分别为 $-2, -2, -4$，均不为零，证实了它们都张成了二维空间 [@problem_id:3554240]。

这一不变性至关重要，因为它意味着许多基于[克雷洛夫子空间](@entry_id:751067)的方法（如[特征值计算](@entry_id:145559)）的结果，对于矩阵的平移和缩放是不变的。这使得我们可以通过“谱变换”（如移位求逆）来加速算法收敛，而无需改变底层的[子空间](@entry_id:150286)结构。

### 构建标准正交基：Arnoldi 过程

虽然克雷洛夫序列 $\{b, Ab, \dots, A^{m-1}b\}$ 定义了[子空间](@entry_id:150286)，但在数值计算中，这个基底通常是病态的，因为随着 $k$ 的增加，$A^k b$ 的方向会趋向于 $A$ 的[主特征向量](@entry_id:264358)方向。因此，我们需要一个稳健的算法来为 $\mathcal{K}_m(A, b)$ 构建一个 **标准正交基 (orthonormal basis)** $\{q_1, q_2, \dots, q_m\}$。**Arnoldi 过程 (Arnoldi process)** 正是实现这一目标的标准方法。

Arnoldi 过程本质上是对克雷洛夫序列进行 Gram-Schmidt 正交化。从 $q_1 = b / \|b\|_2$ 开始，该过程迭代地生成新的向量。在第 $j$ 步，它通过将 $A$ 应用于最新的正交基向量 $q_j$，然后将结果 $Aq_j$ 与所有已生成的[基向量](@entry_id:199546) $\{q_1, \dots, q_j\}$ 正交来产生下一个向量的方向。

该过程可以概括如下：
1.  **初始化**: $q_1 = b / \|b\|_2$。
2.  **迭代**: 对于 $j = 1, 2, \dots, m$:
    a.  计算 $w = Aq_j$。
    b.  对于 $i = 1, \dots, j$，计算投影系数 $h_{ij} = q_i^T w$ 并从 $w$ 中减去相应的分量：$w \leftarrow w - h_{ij} q_i$。
    c.  计算下一个[基向量](@entry_id:199546)的模长 $h_{j+1,j} = \|w\|_2$。
    d.  如果 $h_{j+1,j} = 0$，则过程终止（发生 **击穿 (breakdown)**）。
    e.  否则，进行归一化：$q_{j+1} = w / h_{j+1,j}$。

经过 $m$ 步成功的迭代后，我们得到一个标准正交矩阵 $Q_{m+1} = [q_1, \dots, q_{m+1}]$ 和一个 $(m+1) \times m$ 的 **[上Hessenberg矩阵](@entry_id:756367)** $\bar{H}_m$，其元素为在过程中计算出的系数 $h_{ij}$。这些矩阵满足一个核心关系式，称为 **Arnoldi 分解 (Arnoldi decomposition)**：
$$
A Q_m = Q_{m+1} \bar{H}_m
$$
其中 $Q_m = [q_1, \dots, q_m]$。这个关系式表明，矩阵 $A$ 在克雷洛夫子空间 $\mathcal{K}_m(A,b)$ 上的作用，可以通过一个规模小得多的 Hessenberg 矩阵 $\bar{H}_m$ 来表示。更确切地说，如果我们只考虑 $Q_m$ 的[列空间](@entry_id:156444)，那么 $Q_m^T A Q_m = H_m$，其中 $H_m$ 是 $\bar{H}_m$ 的前 $m \times m$ 主子块。这说明 $H_m$ 是 $A$ 在 $\mathcal{K}_m(A,b)$ 上的 **正交投影 (orthogonal projection)**。

#### 对称情形：Lanczos 算法

当 $A$ 是一个实对称或复[共轭对称](@entry_id:144131)（Hermitian）矩阵时，Arnoldi 过程会简化。在这种情况下，[投影矩阵](@entry_id:154479) $H_m = Q_m^T A Q_m$ 也必须是对称的。由于 $H_m$ 也是 Hessenberg 矩阵，一个对称的 Hessenberg 矩阵必然是 **三对角矩阵 (tridiagonal matrix)**。这意味着对于 $i  j-1$，$h_{ij}=0$。这导致了一个更高效的[三项递推关系](@entry_id:176845)，即 **Lanczos 算法 (Lanczos algorithm)**。

在 Lanczos 算法中，生成 $q_{j+1}$ 只需要 $q_j$ 和 $q_{j-1}$ 的信息，大大减少了计算和存储成本。其核心递推式为：
$$
\beta_j q_{j+1} = A q_j - \alpha_j q_j - \beta_{j-1} q_{j-1}
$$
其中 $\alpha_j = q_j^T A q_j$ 是[三对角矩阵](@entry_id:138829) $T_m$ 的对角元素，$\beta_j = \|A q_j - \alpha_j q_j - \beta_{j-1} q_{j-1}\|_2$ 是次对角元素。

我们可以通过一个具体的例子来演示 Lanczos 算法的步骤 [@problem_id:3554237]。考虑[对称矩阵](@entry_id:143130) $A=\operatorname{diag}(1,2,4,8)$ 和初始向量 $b=\frac{1}{2}(e_1+e_2+e_3+e_4)$。由于 $\|b\|_2=1$，我们有 $q_1 = b$。
- **第1步**:
  - 计算 $\alpha_1 = q_1^T A q_1 = \frac{1}{4}(1+2+4+8) = \frac{15}{4}$。
  - 计算未归一化的下一个向量 $\tilde{q}_2 = A q_1 - \alpha_1 q_1 = \frac{1}{8}(-11, -7, 1, 17)^T$。
  - 计算 $\beta_1 = \|\tilde{q}_2\|_2 = \sqrt{\frac{1}{64}(121+49+1+289)} = \frac{\sqrt{460}}{8} = \frac{\sqrt{115}}{4}$。
  - 归一化得到 $q_2 = \tilde{q}_2 / \beta_1$。
- **第2步**:
  - 计算 $\alpha_2 = q_2^T A q_2 = \frac{507}{92}$。

这两步迭代生成了 $2 \times 2$ 的[对称三对角矩阵](@entry_id:755732) $T_2$：
$$
T_2 = \begin{pmatrix} \alpha_1  \beta_1 \\ \beta_1  \alpha_2 \end{pmatrix} = \begin{pmatrix} \frac{15}{4}  \frac{\sqrt{115}}{4} \\ \frac{\sqrt{115}}{4}  \frac{507}{92} \end{pmatrix}
$$
这个小矩阵 $T_2$ 包含了关于原矩阵 $A$ 在[子空间](@entry_id:150286) $\mathcal{K}_2(A,b)$ 中的谱信息的精确压缩。

#### Arnoldi 过程的击穿

当 Arnoldi 过程中的 $h_{j+1,j} = 0$ 时，过程终止。这被称为 **击穿 (breakdown)**。这种情况的发生具有深刻的理论意义：它意味着向量 $Aq_j$ 完全位于已经生成的[子空间](@entry_id:150286) $\mathcal{K}_j(A,b) = \operatorname{span}\{q_1, \dots, q_j\}$ 中。因此，$\mathcal{K}_j(A,b)$ 是 $A$ 的一个 **不变子空间 (invariant subspace)**。这也等价于说，初始向量 $b$ 的最小多项式 $\mu_{A,b}(x)$ 的次数恰好为 $j$。

一个清晰的例子是当初始向量 $b$ 本身就是 $A$ 的一个[特征向量](@entry_id:151813)时 [@problem_id:3554255]。考虑[对角矩阵](@entry_id:637782) $A = \operatorname{diag}(5, 3, 3)$ 和初始向量 $b=e_2$。
1.  **初始化**: $\|b\|_2=1$，所以 $q_1=e_2$。
2.  **第1步迭代**:
    - $w = Aq_1 = Ae_2 = 3e_2 = 3q_1$。
    - $h_{1,1} = q_1^T w = q_1^T(3q_1) = 3$。
    - $w \leftarrow w - h_{1,1}q_1 = 3q_1 - 3q_1 = 0$。
    - $h_{2,1} = \|w\|_2 = 0$。

由于 $h_{2,1}=0$，Arnoldi 过程在试图生成第二个[基向量](@entry_id:199546)时发生击穿。这表明一维[子空间](@entry_id:150286) $\mathcal{K}_1(A,b) = \operatorname{span}\{e_2\}$ 是 $A$ 的一个不变子空间。在这种情况下，Arnoldi 过程实际上找到了 $A$ 的一个精确的特征对：[特征值](@entry_id:154894) $\lambda=3$（即 $H_1=[3]$ 的[特征值](@entry_id:154894)）和[特征向量](@entry_id:151813) $q_1=e_2$。这个过程被称为 **通缩 (deflation)**，因为算法成功地将问题“缩小”到了一个[不变子空间](@entry_id:152829)上。

### Arnoldi 分解及其应用

Arnoldi 分解 $A Q_m = Q_{m+1} \bar{H}_m$ 是连接抽象的克雷洛夫子空间与具体[数值算法](@entry_id:752770)的桥梁。它构成了求解[大型稀疏线性系统](@entry_id:137968)和特征值问题的多种迭代方法的基础。这些方法的核心思想都是将原先在 $n$ 维空间中的问题，通过投影转换为在 $m$ 维克雷洛夫子空间上的一个小规模问题，其中 $m \ll n$。

#### 投影方法：[Petrov-Galerkin](@entry_id:174072) 框架

许多迭代方法可以被统一在 **[Petrov-Galerkin](@entry_id:174072) 框架**下 [@problem_id:3554235]。对于线性系统 $Ax=b$，我们寻求一个近似解 $x_m \in x_0 + \mathcal{K}_m(A, r_0)$（其中 $r_0=b-Ax_0$ 是初始残差），使得其残差 $r_m = b - Ax_m$ 与某个 $m$ 维的 **测试[子空间](@entry_id:150286) (test subspace)** $\mathcal{L}_m$ 正交，即 $r_m \perp \mathcal{L}_m$。

这个[正交性条件](@entry_id:168905) $W_m^T r_m = 0$（其中 $W_m$ 是 $\mathcal{L}_m$ 的一组基）给出了一个用于确定近似解 $x_m = x_0 + Q_m y_m$ 中系数向量 $y_m$ 的 $m \times m$ 线性系统。不同的测试[子空间](@entry_id:150286)选择，导致了不同的[克雷洛夫子空间方法](@entry_id:144111)。

- **FOM (Full Orthogonalization Method)**: 该方法选择测试[子空间](@entry_id:150286)与 **搜索[子空间](@entry_id:150286) (search subspace)** 相同，即 $\mathcal{L}_m = \mathcal{K}_m(A, r_0)$。这被称为 **Galerkin 条件**。在这种情况下，$r_m \perp \mathcal{K}_m(A, r_0)$。利用 Arnoldi 分解，可以推导出求解系数 $y_m$ 的简化系统为：
$$
H_m y_m = \beta e_1
$$
其中 $\beta = \|r_0\|_2$，$H_m$ 是 Arnoldi 过程生成的 $m \times m$ Hessenberg 矩阵。

- **GMRES (Generalized Minimal Residual Method)**: GMRES 的目标是直接最小化残差的[欧几里得范数](@entry_id:172687)，即在 $x_0 + \mathcal{K}_m(A, r_0)$ 中寻找使 $\|r_m\|_2 = \|b-Ax_m\|_2$ 最小的 $x_m$。这个最小化问题可以利用 Arnoldi 分解转化为一个 $m$ 维的小型最小二乘问题 [@problem_id:3554256]：
$$
\min_{y_m \in \mathbb{C}^m} \|\beta e_1 - \bar{H}_m y_m\|_2
$$
其中 $\bar{H}_m$ 是 $(m+1) \times m$ 的 Hessenberg 矩阵。这个最小二乘问题的解，其残差向量 $(\beta e_1 - \bar{H}_m y_m)$ 必然与 $\bar{H}_m$ 的[列空间](@entry_id:156444)正交。通过转换回原空间，这等价于一个不同的[正交性条件](@entry_id:168905)：$r_m \perp A\mathcal{K}_m(A, r_0)$ [@problem_id:3554235]。因此，GMRES 也可以看作是一个 [Petrov-Galerkin](@entry_id:174072) 方法，其测试[子空间](@entry_id:150286)为 $\mathcal{L}_m = A\mathcal{K}_m(A, r_0)$。

这两种方法定义了不同的近似解，其残差满足不同的正交性。FOM 强制残差与整个[克雷洛夫子空间](@entry_id:751067)正交，而 GMRES 强制残差与该[子空间](@entry_id:150286)在 $A$ 下的像正交，这恰好是最小化[残差范数](@entry_id:754273)的条件。

#### [特征值](@entry_id:154894)近似：Ritz 值与 Ritz 向量

Arnoldi 过程不仅对[求解线性系统](@entry_id:146035)至关重要，它也是一类最强大的[特征值算法](@entry_id:139409)的基础。其思想是，$A$ 在克雷洛夫子空间 $\mathcal{K}_m(A,b)$ 上的投影 $H_m = Q_m^T A Q_m$ 的谱性质，会近似于 $A$ 自身的谱性质。

$H_m$ 的[特征值](@entry_id:154894)被称为 **Ritz 值 (Ritz values)**，它们是 $A$ 的[特征值](@entry_id:154894)的近似。如果 $(\theta, z)$ 是 $H_m$ 的一个特征对，即 $H_m z = \theta z$，那么向量 $y = Q_m z$ 就被称为对应的 **Ritz 向量 (Ritz vector)**。Ritz 向量 $y$ 是 $A$ 的[特征向量](@entry_id:151813)的近似。

我们可以评估这种近似的质量。Ritz 对 $(\theta, y)$ 的[残差范数](@entry_id:754273)为 $\|Ay - \theta y\|_2$。利用 Arnoldi 分解，可以导出一个非常简洁和强大的公式来计算这个[残差范数](@entry_id:754273)，而无需显式计算高维向量 $y$ [@problem_id:3554225]：
$$
\|Ay - \theta y\|_2 = |h_{m+1,m}| \cdot |e_m^T z|
$$
其中 $z$ 是归一化的 $H_m$ 的[特征向量](@entry_id:151813)。这个公式表明，Ritz 对的[残差范数](@entry_id:754273)直接由 Arnoldi 过程中的下一个子对角元素 $h_{m+1,m}$ 和 $H_m$ 的[特征向量](@entry_id:151813)的最后一个分量决定。如果 $h_{m+1,m}$ 很小，或者 $|e_m^T z|$ 很小，那么我们已经找到了一个很好的[特征值](@entry_id:154894)近似。特别地，如果发生击穿（$h_{m+1,m}=0$），那么残差为零，这意味着 Ritz 值是 $A$ 的一个精确[特征值](@entry_id:154894)。

以矩阵 $A = \begin{bmatrix} 4  1  0 \\ 1  3  1 \\ 0  1  2 \end{bmatrix}$ 和 $b=e_1$ 为例，经过两步 Arnoldi 迭代，我们得到 $H_2 = \begin{bmatrix} 4  1 \\ 1  3 \end{bmatrix}$ 和 $h_{3,2}=1$。$H_2$ 的[特征值](@entry_id:154894)（Ritz 值）为 $\theta_{1,2} = \frac{7 \pm \sqrt{5}}{2}$。利用上述公式，可以计算出对应的[残差范数](@entry_id:754273)，分别为 $\sqrt{\frac{5 \mp \sqrt{5}}{10}}$ [@problem_id:3554225]。这些非零但较小的残差表明，Ritz 值已经是原[矩阵特征值](@entry_id:156365)的良好近似。

### 作为[多项式空间](@entry_id:144410)的克雷洛夫方法

对[克雷洛夫子空间方法](@entry_id:144111)的理解可以提升到一个更抽象但更强大的层次：多项式观点 [@problem_id:3554244]。任何在 $x_0 + \mathcal{K}_m(A, r_0)$ 中的近似解 $x_m$ 所对应的残差 $r_m$，都可以表示为一个作用在初始残差 $r_0$ 上的矩阵多项式的形式：
$$
r_m = p_m(A)r_0
$$
其中 $p_m(x)$ 是一个次数至多为 $m$ 的多项式，并且满足 $p_m(0)=1$。这个约束来自 $x_m - x_0 \in \mathcal{K}_m(A, r_0)$ 的构造。

从这个角度看，不同的克雷洛夫方法就是为 $p_m(x)$ 施加了不同的约束或优化目标。
- **GMRES** 在所有满足 $p_m(0)=1$ 的 $m$ 次多项式中，寻找使得[残差范数](@entry_id:754273) $\|p_m(A)r_0\|_2$ 最小的那个多项式。

这个多项式观点为分析算法的收敛性提供了强大的理论工具。例如，对于 GMRES，我们有以下范数界：
$$
\|r_m\|_2 = \min_{p_m \in \Pi_m, p_m(0)=1} \|p_m(A)r_0\|_2 \le \|p_m(A)\|_2 \|r_0\|_2
$$
对于任何满足条件的 $p_m$。如果我们能找到一个在 $A$ 的谱上取值很小的多项式 $p_m$，就可以得到一个很好的收敛界。

- **如果 $A$ 是[正规矩阵](@entry_id:185943)**，则 $\|p_m(A)\|_2 = \max_{\lambda \in \sigma(A)} |p_m(\lambda)|$。因此，GMRES 的收敛性问题转化为一个经典的[多项式逼近](@entry_id:137391)问题：
$$
\frac{\|r_m\|_2}{\|r_0\|_2} \le \min_{p_m \in \Pi_m, p_m(0)=1} \max_{\lambda \in \sigma(A)} |p_m(\lambda)|
$$
- **如果 $A$ 的谱 $\sigma(A)$ 包含在一个实数区间 $[\alpha, \beta]$ 内** (且 $0 \notin [\alpha, \beta]$)，这个极小极大问题的解由 **切比雪夫多项式 (Chebyshev polynomials)** 给出。最优的衰减因子可以通过一个缩放和平移的[切比雪夫多项式](@entry_id:145074)得到，这为许多实际问题提供了尖锐的收敛估计 [@problem_id:3554244, option B]。
- **如果 $A$ 是非正规但可对角化的** ($A=V \Lambda V^{-1}$)，收敛界会变差，并引入一个与[特征向量基](@entry_id:163721)的[条件数](@entry_id:145150) $\kappa(V) = \|V\|_2 \|V^{-1}\|_2$ 相关的因子：
$$
\frac{\|r_m\|_2}{\|r_0\|_2} \le \kappa(V) \min_{p_m \in \Pi_m, p_m(0)=1} \max_{\lambda \in \sigma(A)} |p_m(\lambda)|
$$
这个界是一个[上界](@entry_id:274738)，而非等式 [@problem_id:3554244, option C]，它解释了为什么[非正规矩阵](@entry_id:752668)的收敛行为可能比仅从其[谱分布](@entry_id:158779)预测的要复杂得多。

### 扩展：块[克雷洛夫子空间](@entry_id:751067)

[克雷洛夫子空间](@entry_id:751067)的概念可以自然地推广到 **块 (block)** 的情形。如果我们不是从单个向量 $b$ 开始，而是从一个有 $s$ 列的块（矩阵）$B \in \mathbb{C}^{n \times s}$ 开始，那么块[克雷洛夫子空间](@entry_id:751067)的定义为：
$$
\mathcal{K}_m(A, B) = \operatorname{span}\{B, AB, A^2B, \dots, A^{m-1}B\}
$$
这里的张成空间是指由构成这些矩阵块的所有列[向量张成](@entry_id:152883)的空间。块克雷洛夫方法在处理多个右端项的[线性系统](@entry_id:147850)、寻找[特征值](@entry_id:154894)的[重数](@entry_id:136466)或[特征向量](@entry_id:151813)簇时特别有用。

相应地，Arnoldi 和 Lanczos 算法也有其块版本。在块 Arnoldi 过程中，我们生成一系列标准正交的块 $Q_1, Q_2, \dots$，其中每个 $Q_j$ 是一个 $n \times s$ 的矩阵且 $Q_j^T Q_i = \delta_{ij} I_s$。

与单向量情况一样，块克雷洛夫子空间的维度也可能提前饱和。这发生在块克雷洛夫序列 $A^k B$ 的列向量变得与之前生成的向量线性相关时。这种情况被称为 **[秩亏](@entry_id:754065) (rank deficiency)** 或块击穿。

考虑矩阵 $A=\begin{bmatrix} 2  1  0 \\ 0  2  1 \\ 0  0  2 \end{bmatrix}$ 和块 $B = [e_1, e_2]$ [@problem_id:3554223]。
- 第一个块是 $B = \begin{bmatrix} 1  0 \\ 0  1 \\ 0  0 \end{bmatrix}$。其列空间是 $xy$-平面。
- 第二个块是 $AB = \begin{bmatrix} 2  1 \\ 0  2 \\ 0  0 \end{bmatrix}$。我们可以发现 $AB$ 的两列向量 $Ae_1=2e_1$ 和 $Ae_2=e_1+2e_2$ 都可以由 $B$ 的列向量 $e_1, e_2$ [线性表示](@entry_id:139970)。
这意味着 $AB$ 的列空间完全包含在 $B$ 的列空间之内。因此，[子空间](@entry_id:150286) $\mathcal{K}_2(A,B)$ 的维度与 $\mathcal{K}_1(A,B)$ 相同，均为 $2$。这个维度小于理论上的最大可能维度 $\min(n, ms) = \min(3, 2 \times 2) = 3$。这表明，由 $B$ 的列向量张成的[子空间](@entry_id:150286)是 $A$ 的一个[不变子空间](@entry_id:152829)，导致了块克雷洛夫序列的维度增长提前停止。

综上所述，[克雷洛夫子空间](@entry_id:751067)及其相关算法构成了一个优雅而强大的理论和计算框架。通过将大规模问题投影到精心构造的低维[子空间](@entry_id:150286)上，这些方法能够在可接受的计算成本内，为极其广泛的科学与工程应用提供高效的解决方案。