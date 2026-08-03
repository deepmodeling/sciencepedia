## 引言
在科学与工程计算领域，求解由偏微分方程离散化产生的大型稀疏线性系统是一个核心且普遍的挑战。共轭梯度（CG）法作为一种高效的迭代方法，尤其擅长处理这类对称正定（SPD）系统，是现代数值模拟工具箱中不可或缺的基石。尽管诸如最速下降法等简单迭代格式易于理解，但其缓慢的收敛性在面对大规模问题时往往力不从心。这凸显了对一种既能保证快速收敛又计算高效的算法的需求，而共轭梯度法正是为应对这一挑战而生。

本文旨在系统性地剖析共轭梯度法的性质与收敛性。我们将从**第一章“原理与机制”**出发，深入其作为优化问题的数学本质和算法推导；接着在**第二章“应用与交叉学科联系”**中，探讨其在偏微分方程求解、计算力学等领域的实际应用与挑战，并阐明预处理的关键作用；最后，**第三章“动手实践”**将提供一系列精心设计的计算问题，帮助您将理论知识转化为实践技能。通过这三个层次的递进学习，您将对共轭梯度法建立起从理论基础到应用实践的全面理解。

## 原理与机制

在求解源于偏微分方程离散化的大型稀疏线性系统 $A\mathbf{x}=\mathbf{b}$ 时，共轭梯度（CG）法是一种卓越的迭代方法，其中 $A$ 是一个对称正定（Symmetric Positive Definite, SPD）矩阵。本章将深入探讨共轭梯度法的基本原理与内在机制。我们将从其作为优化问题的最优性原理出发，推导出算法的具体形式，分析其收敛行为与谱分布的深刻联系，并最终讨论在有限精度计算中的实际考量。

### 共轭梯度法：一个优化视角

共轭梯度法的核心思想，并非仅仅是求解一个线性方程组，而是将其视为一个优化问题。对于一个SPD矩阵 $A$，求解 $A\mathbf{x}=\mathbf{b}$ 等价于寻找二次能量泛函 $J(\mathbf{x})$ 的唯一最小值点：

$$
J(\mathbf{x}) = \frac{1}{2}\mathbf{x}^\top A \mathbf{x} - \mathbf{b}^\top \mathbf{x}
$$

该泛函的梯度为 $\nabla J(\mathbf{x}) = A\mathbf{x} - \mathbf{b}$。当梯度为零时，即 $A\mathbf{x} = \mathbf{b}$，泛函达到最小值。因此，求解线性系统的任务转化为一个无约束的凸优化问题 [@problem_id:3436382]。

#### A-范数与能量最小化

为了量化迭代过程中的误差，我们引入一个与矩阵 $A$ 密切相关的范数，即 **A-范数**，或称能量范数。对于任意向量 $\mathbf{e}$，其A-范数定义为：

$$
\|\mathbf{e}\|_A = \sqrt{\mathbf{e}^\top A \mathbf{e}}
$$

由于 $A$ 是正定的，仅当 $\mathbf{e}=\mathbf{0}$ 时 $\|\mathbf{e}\|_A=0$。A-范数与能量泛函 $J(\mathbf{x})$ 之间存在直接联系。令 $\mathbf{x}_*$ 为方程的精确解，$\mathbf{x}$ 为任意向量，误差为 $\mathbf{e} = \mathbf{x}_* - \mathbf{x}$。我们可以证明，最小化能量泛函 $J(\mathbf{x})$ 等价于最小化误差的A-范数 $\|\mathbf{x}_* - \mathbf{x}\|_A$。具体来说，两者之间相差一个仅与 $\mathbf{x}_*$ 有关的常数：

$$
J(\mathbf{x}) = \frac{1}{2} (\mathbf{x}_* - \mathbf{e})^\top A (\mathbf{x}_* - \mathbf{e}) - \mathbf{b}^\top (\mathbf{x}_* - \mathbf{e}) = \frac{1}{2} \mathbf{e}^\top A \mathbf{e} - \frac{1}{2} \mathbf{x}_*^\top A \mathbf{x}_* = \frac{1}{2} \|\mathbf{e}\|_A^2 - J(\mathbf{x}_*)
$$

A-范数与我们更熟悉的欧几里得2-范数之间存在等价关系。这一关系由 $A$ 的谱特性决定。根据瑞利商的性质，对于任意非零向量 $\mathbf{x}$，我们有 $\lambda_{\min}(A) \le \frac{\mathbf{x}^\top A \mathbf{x}}{\mathbf{x}^\top \mathbf{x}} \le \lambda_{\max}(A)$。由此可直接推导出范数等价性 [@problem_id:3436366]：

$$
\sqrt{\lambda_{\min}(A)} \|\mathbf{x}\|_2 \le \|\mathbf{x}\|_A \le \sqrt{\lambda_{\max}(A)} \|\mathbf{x}\|_2
$$

其中 $\lambda_{\min}(A)$ 和 $\lambda_{\max}(A)$ 分别是 $A$ 的最小和最大特征值。例如，若一个SPD矩阵 $A$ 的谱范围为 $[1, 100]$，则其A-范数与2-范数之间的等价常数为 $c=1$ 和 $C=10$。对于向量 $\mathbf{x} = (1, 1, 0, \dots, 0)^\top$，其2-范数为 $\|\mathbf{x}\|_2 = \sqrt{2}$，那么其A-范数的界限为 $\sqrt{2} \le \|\mathbf{x}\|_A \le 10\sqrt{2}$ [@problem_id:3436366]。这个关系量化了由矩阵 $A$ 定义的几何空间与标准欧几里得空间之间的“变形”程度。

#### 物理直觉：离散狄利克雷能量

当线性系统 $A\mathbf{x}=\mathbf{b}$ 源于偏微分方程（PDE）的离散化时，A-范数通常具有明确的物理意义。以二维泊松方程 $-\Delta u = f$ 在区域 $\Omega$ 上带齐次狄利克雷边界条件为例，其变分形式要求寻找一个函数 $u \in H_0^1(\Omega)$，最小化狄利克雷能量泛函：

$$
\mathcal{E}(u) = \frac{1}{2} \int_\Omega |\nabla u|^2 d\mathbf{x} - \int_\Omega f u \, d\mathbf{x}
$$

当我们采用标准的有限元方法（FEM）或有限差分方法（FDM）进行离散化时，得到的刚度矩阵 $A$ 正是源于变分形式中的双线性项 $\int_\Omega \nabla u \cdot \nabla v \, d\mathbf{x}$ 的离散化。对于一个代表离散函数 $u_h$ 的系数向量 $\mathbf{x}$，其二次型 $\frac{1}{2}\mathbf{x}^\top A \mathbf{x}$ 精确地对应于离散函数的狄利克雷能量 $\frac{1}{2}\int_\Omega |\nabla u_h|^2 d\mathbf{x}$，这正是离散的 $H^1$-半范数的平方 [@problem_id:3436360] [@problem_id:3436345]。

因此，共轭梯度法在每一步最小化误差的A-范数，从物理角度看，就是在寻找一个近似解，使得该近似解与真解之间的能量差最小。矩阵 $A$ 的对称性和正定性，正是连续问题中双线性形式对称性和矫顽性（coercivity）的直接体现 [@problem_id:3436360]。

### 算法：构建最优解序列

CG方法通过在一系列精心挑选的方向上进行精确线搜索，逐步逼近能量泛函的最小值点。最速下降法每一步都沿着负梯度方向（即残差方向）搜索，但这种策略常常导致收敛缓慢的“之”字形路径。CG方法的绝妙之处在于它选择了一组**A-共轭**（或称A-正交）的搜索方向 $\{\mathbf{p}_k\}$。

A-共轭性定义为：对于 $i \ne j$，有 $\mathbf{p}_i^\top A \mathbf{p}_j = 0$。这意味着，当我们在一个方向 $\mathbf{p}_k$上最小化能量泛函时，这个移动不会破坏之前在所有方向 $\{\mathbf{p}_0, \dots, \mathbf{p}_{k-1}\}$ 上已经达成的最优性。

#### 克雷洛夫子空间与最优性

CG方法在第 $k$ 步的迭代解 $\mathbf{x}_k$ 是在初始猜测 $\mathbf{x}_0$ 张成的仿射空间中寻找的，该空间由**克雷洛夫子空间**（Krylov subspace）定义：

$$
\mathbf{x}_k \in \mathbf{x}_0 + \mathcal{K}_k(A, \mathbf{r}_0)
$$

其中 $\mathbf{r}_0 = \mathbf{b} - A\mathbf{x}_0$ 是初始残差，克雷洛夫子空间为 $\mathcal{K}_k(A, \mathbf{r}_0) = \operatorname{span}\{\mathbf{r}_0, A\mathbf{r}_0, \dots, A^{k-1}\mathbf{r}_0\}$。

CG方法的核心最优性原理可以表述为 [@problem_id:3436330] [@problem_id:3436345]：
**在第 $k$ 步，CG迭代解 $\mathbf{x}_k$ 是仿射子空间 $\mathbf{x}_0 + \mathcal{K}_k(A, \mathbf{r}_0)$ 中唯一能使误差的A-范数 $\|\mathbf{x}_* - \mathbf{x}\|_A$ 最小化的向量。**

这等价于说，误差向量 $\mathbf{e}_k = \mathbf{x}_* - \mathbf{x}_k$ 与子空间 $\mathcal{K}_k(A, \mathbf{r}_0)$ A-正交，或者说残差 $\mathbf{r}_k = \mathbf{b} - A\mathbf{x}_k$ 与子空间 $\mathcal{K}_k(A, \mathbf{r}_0)$（欧几里得）正交。这也被称为伽辽金（Galerkin）条件。

#### 算法的推导与形式

CG算法通过一个巧妙的三项递推关系来生成A-共轭的搜索方向和（欧几里得）正交的残差向量，而无需存储所有先前的向量。我们从迭代格式 $\mathbf{x}_{k+1} = \mathbf{x}_k + \alpha_k \mathbf{p}_k$ 开始。

1.  **步长 $\alpha_k$ 的确定**：步长 $\alpha_k$ 通过线搜索确定，即选择 $\alpha_k$ 来最小化 $J(\mathbf{x}_k + \alpha_k \mathbf{p}_k)$。这导致了 $\frac{d}{d\alpha} J(\mathbf{x}_k + \alpha \mathbf{p}_k)|_{\alpha=\alpha_k}=0$，从而推导出 [@problem_id:3436382]：
    $$
    \alpha_k = \frac{\mathbf{r}_k^\top \mathbf{p}_k}{\mathbf{p}_k^\top A \mathbf{p}_k}
    $$
    利用残差的正交性，这个公式可以简化为计算上更高效的形式。

2.  **搜索方向更新系数 $\beta_k$ 的确定**：新的搜索方向由当前残差和前一个搜索方向线性组合而成：$\mathbf{p}_{k+1} = \mathbf{r}_{k+1} + \beta_k \mathbf{p}_k$。系数 $\beta_k$ 的选择是为了保证新的搜索方向 $\mathbf{p}_{k+1}$ 与 $\mathbf{p}_k$ 是A-共轭的，即 $\mathbf{p}_{k+1}^\top A \mathbf{p}_k = 0$。通过这个条件，可以推导出 [@problem_id:3436382]：
    $$
    \beta_k = -\frac{\mathbf{r}_{k+1}^\top A \mathbf{p}_k}{\mathbf{p}_k^\top A \mathbf{p}_k}
    $$
    同样，利用已建立的正交关系，这个公式有多种等价且计算上更优的形式。

综合这些推导，标准的共轭梯度算法如下 [@problem_id:3436330]：

-   初始化：$\mathbf{r}_0 = \mathbf{b} - A\mathbf{x}_0$, $\mathbf{p}_0 = \mathbf{r}_0$
-   对于 $k=0, 1, 2, \dots$ 循环：
    -   $\alpha_k = \frac{\mathbf{r}_k^\top \mathbf{r}_k}{\mathbf{p}_k^\top A \mathbf{p}_k}$
    -   $\mathbf{x}_{k+1} = \mathbf{x}_k + \alpha_k \mathbf{p}_k$
    -   $\mathbf{r}_{k+1} = \mathbf{r}_k - \alpha_k A \mathbf{p}_k$
    -   $\beta_k = \frac{\mathbf{r}_{k+1}^\top \mathbf{r}_{k+1}}{\mathbf{r}_k^\top \mathbf{r}_k}$ （Fletcher-Reeves 形式）
    -   $\mathbf{p}_{k+1} = \mathbf{r}_{k+1} + \beta_k \mathbf{p}_k$

在精确算术下，该算法保证了残差的相互正交性（$\mathbf{r}_i^\top \mathbf{r}_j = 0$ for $i \ne j$）和搜索方向的A-共轭性（$\mathbf{p}_i^\top A \mathbf{p}_j = 0$ for $i \ne j$）。

对于**预处理共轭梯度法**（Preconditioned Conjugate Gradient, PCG），我们引入一个SPD预处理器 $M$，并应用于系统 $M^{-1}A\mathbf{x}=M^{-1}\mathbf{b}$。算法结构保持不变，但内积运算需要调整以适应预处理后的算子。这相当于在由 $M$ 定义的内积空间中进行CG。关键的递推系数变为 [@problem_id:3436382]：
-   $\alpha_k = \frac{\mathbf{r}_k^\top \mathbf{z}_k}{\mathbf{p}_k^\top A \mathbf{p}_k}$
-   $\beta_k = \frac{\mathbf{r}_{k+1}^\top \mathbf{z}_{k+1}}{\mathbf{r}_k^\top \mathbf{z}_k}$
其中 $\mathbf{z}_k = M^{-1}\mathbf{r}_k$ 是预处理残差。

### 收敛性分析：谱的角色

CG方法的收敛速度与矩阵 $A$ 的谱（特征值分布）密切相关。理解这一点需要从CG的多项式解释入手。

#### 多项式解释

CG的最优性原理（最小化A-范数误差）意味着在第 $k$ 步，CG方法找到了一个 $k$ 次多项式 $Q_k(\lambda)$，满足 $Q_k(0)=1$，使得 $\|\mathbf{e}_k\|_A = \|Q_k(A)\mathbf{e}_0\|_A$ 最小。换句话说，CG方法在每一步都在寻找一个最优的“误差衰减多项式”作用在初始误差上 [@problem_id:3436359]。

这个多项式的根（Ritz值）是由算法隐式进行的Lanczos过程中计算出来的，它们是 $A$ 的特征值在克雷洛夫子空间上的最佳近似。

#### 有限步终止与特征值分布

多项式解释直接导出一个惊人的结论：如果初始误差 $\mathbf{e}_0$ 的谱分解只包含 $A$ 的 $m$ 个不同特征值所对应的分量，那么CG方法将在最多 $m$ 步内终止（在精确算术下）。这是因为我们可以构造一个 $m$ 次多项式 $Q_m(\lambda)$，其根恰好是这 $m$ 个特征值，且 $Q_m(0)=1$。这样的多项式作用在 $\mathbf{e}_0$ 上会得到零向量 [@problem_id:3436359]。

例如，考虑一个 $5 \times 5$ 的对角矩阵 $A = \operatorname{diag}(4, 4, 4, 9, 9)$，它只有两个不同的特征值：4和9。如果从 $\mathbf{x}_0 = \mathbf{0}$ 开始，且右端项 $\mathbf{b}$ 在两个特征子空间中都有分量，那么初始误差 $\mathbf{e}_0 = A^{-1}\mathbf{b}$ 也将在这两个子空间中都有分量。因此，CG方法将在最多2步内收敛。如果 $\mathbf{b}$ 只在特征值为4的子空间中有分量，那么 $\mathbf{e}_0$ 也只在该子空间中，CG将在1步内收敛 [@problem_id:3436359]。这个性质说明，如果矩阵的特征值高度聚集，CG的收敛会非常快。

#### 条件数界

对于一般情况，我们无法指望有限步终止。收敛速度可以用矩阵的谱条件数 $\kappa(A) = \lambda_{\max}(A)/\lambda_{\min}(A)$ 来界定。通过将CG的最优多项式与在整个谱区间 $[\lambda_{\min}, \lambda_{\max}]$ 上最优的Chebyshev多项式进行比较，可以得到经典的收敛界 [@problem_id:3436330]：

$$
\|\mathbf{e}_k\|_A \le 2 \left(\frac{\sqrt{\kappa(A)}-1}{\sqrt{\kappa(A)}+1}\right)^k \|\mathbf{e}_0\|_A
$$

这个界表明，条件数越接近1，收敛因子 $\frac{\sqrt{\kappa(A)}-1}{\sqrt{\kappa(A)}+1}$ 越接近0，收敛越快。

让我们通过一个具体例子来理解这个界的影响。考虑一维泊松方程 $-u''=f$ 在 $(0,1)$ 上的有限差分逼近，网格尺寸为 $h$。得到的矩阵 $A$ 的条件数 $\kappa(A)$ 可以精确计算，并且当 $h \to 0$ 时，$\kappa(A) = \Theta(h^{-2})$ [@problem_id:3436361]。这意味着网格越密，$h$ 越小，条件数越大，CG收敛越慢。将 $\kappa(A) \approx C h^{-2}$ 代入收敛因子，对于小的 $h$，我们有 $\frac{\sqrt{\kappa}-1}{\sqrt{\kappa}+1} \approx 1 - 2/\sqrt{\kappa} \approx 1 - 2h/\sqrt{C}$。为了使误差衰减到 $\epsilon$，需要的迭代次数 $k$ 大致满足 $(1-2h/\sqrt{C})^k \approx \epsilon/2$，取对数可得 $k \approx O(h^{-1})$。这表明，要将网格分辨率提高一倍（$h \to h/2$），CG的迭代次数大约也要翻倍 [@problem_id:3436361]。

### 高级主题与实际考量

理论上的CG是完美的，但在实践中，我们需要考虑更复杂的行为和有限精度算术的影响。

#### 超线性收敛与预处理

条件数界往往是悲观的。实际中，CG经常表现出**超线性收敛**（superlinear convergence）——即收敛速度随着迭代的进行而加快。这再次与CG的自适应多项式性质有关。CG通过其内在的Lanczos过程，能够“感知”到谱的分布。如果谱中存在孤立的或成簇的特征值，CG会很快找到它们对应的Ritz值，并在其误差多项式中放置根来“消除”这些模态。一旦这些“棘手”的模态被处理掉，算法就好像在处理一个有效条件数更小的“剩余”问题，从而加速收敛 [@problem_id:3436395]。

这种自适应性是CG相比于非自适应多项式方法（如Chebyshev迭代）的巨大优势。Chebyshev迭代需要预先知道谱的界限，并使用一个固定的最优多项式，它无法像CG那样利用谱的内部结构 [@problem_id:3436395]。

一个好的预处理器 $M$ 旨在改善 $M^{-1}A$ 的谱分布，例如将大部分特征值聚集在1附近。这不仅减小了整体条件数，而且创造了有利于超线性收敛的谱结构 [@problem_id:3436367]。

#### 浮点算术的影响

在有限精度计算中，CG的理论性质（正交性、A-共轭性、有限终止性）都会被破坏。舍入误差的累积会导致所谓的**局部正交性损失**（local loss of orthogonality） [@problem_id:3436387]。这意味着计算出的残差 $\tilde{\mathbf{r}}_k$ 与其最近的几个前驱（如 $\tilde{\mathbf{r}}_{k-1}, \tilde{\mathbf{r}}_{k-2}$）仍然近似正交，但与更远的残差（如 $\tilde{\mathbf{r}}_0, \tilde{\mathbf{r}}_1$）的正交性会逐渐丧失。

这种影响的严重程度取决于一个关键参数：$\kappa(A)u$，其中 $u$ 是机器单位舍入。
-   当 $\kappa(A)u \ll 1$ 时，舍入误差的影响在初始阶段可以忽略，CG的行为接近于理论情况。
-   当 $\kappa(A)u \gtrsim 1$ 时，问题对于当前精度来说是病态的，舍入误差会迅速破坏算法的收敛性，可能导致收敛延迟、停滞甚至发散 [@problem_id:3436387]。

正交性的损失导致了一个重要的实际问题：**残差漂移**（residual drift）。算法中递推更新的残差 $\tilde{\mathbf{r}}_k = \tilde{\mathbf{r}}_{k-1} - \alpha_{k-1} A \mathbf{p}_{k-1}$ 会因为累积的舍入误差而逐渐偏离其真实定义 $\mathbf{r}_k^{\text{true}} = \mathbf{b} - A\mathbf{x}_k$ [@problem_id:3436397]。

因此，一个鲁棒的CG实现不能仅依赖于递推残差的范数 $\|\tilde{\mathbf{r}}_k\|$ 作为停机判据。一个常见的稳健策略是 [@problem_id:3436397]：
1.  主要监控廉价的递推残差 $\|\tilde{\mathbf{r}}_k\|$。
2.  当 $\|\tilde{\mathbf{r}}_k\|$ 达到一个预设的阈值时，计算一次昂贵的真实残差 $\mathbf{r}_k^{\text{true}} = \mathbf{b} - A\mathbf{x}_k$。
3.  使用真实残差的相对范数 $\|\mathbf{r}_k^{\text{true}}\|_2 / \|\mathbf{b}\|_2 \le \varepsilon$ 作为最终的停机判据。
4.  如果真实残差显示尚未收敛，说明发生了显著的残差漂移。此时，可以用真实的残差来“重置”递推的残差，即令 $\tilde{\mathbf{r}}_k \leftarrow \mathbf{r}_k^{\text{true}}$，然后继续迭代。这种**残差重置**（residual replacement）策略可以有效对抗漂移，提高算法的鲁棒性。