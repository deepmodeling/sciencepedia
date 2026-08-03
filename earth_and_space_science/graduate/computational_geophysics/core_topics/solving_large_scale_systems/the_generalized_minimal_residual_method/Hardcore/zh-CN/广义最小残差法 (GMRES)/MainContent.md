## 引言
在科学与工程计算的广阔领域中，求解形如 $A\boldsymbol{x} = \boldsymbol{b}$ 的大规模线性方程组是一个无处不在的核心任务。然而，当系数矩阵 $A$ 不具备对称性或正定性时——这在模拟流体流动、波传播或各向异性扩散等复杂物理现象时屡见不鲜——诸如共轭梯度法等经典高效的迭代方法便无能为力。这为通用且稳健的求解器创造了巨大的需求缺口。广义最小残差方法（GMRES）正是为应对这一挑战而生，它已成为求解大规模非对称线性系统的基石算法之一。

本文旨在系统性地剖析 GMRES 方法。我们将跨越三个紧密相连的章节，引领读者从理论基础走向实际应用。
*   在第一章“**原理与机制**”中，我们将深入其数学心脏，揭示克雷洛夫子空间、残差最小化准则以及作为算法引擎的 Arnoldi 迭代过程。
*   随后的“**应用与跨学科联系**”一章将视野拓宽至真实世界，通过计算地球物理、流体力学等领域的具体案例，展示 GMRES 如何解决棘手的科学问题，并探讨其与其它算法和学科的深刻联系。
*   最后，在“**动手实践**”部分，通过一系列精心设计的计算练习，您将有机会亲手实现并验证所学理论，从而将抽象知识转化为牢固的计算直觉。

现在，让我们从探究GMRES背后的根本原理开始，踏上这段兼具理论深度与实践价值的旅程。

## 原理与机制

在上一章引言的基础上，本章将深入探讨广义最小残差方法（GMRES）的核心原理与算法机制。我们将从其基本的最优化准则出发，详细阐述其算法实现，分析其实际应用中的计算成本与收敛特性，并探讨其在面对不同类型线性系统时的行为。

### 核心思想：在克雷洛夫子空间上进行残差最小化

许多迭代方法的核心思想是在一个逐步扩大的搜索空间中寻找当前最优的近似解。对于形如 $A\boldsymbol{x} = \boldsymbol{b}$ 的线性系统，给定初始猜测 $\boldsymbol{x}_0$，其对应的初始残差为 $\boldsymbol{r}_0 = \boldsymbol{b} - A\boldsymbol{x}_0$。GMRES方法在第 $m$ 步寻找的近似解 $\boldsymbol{x}_m$ 属于一个特定的仿射子空间 $\boldsymbol{x}_0 + \mathcal{K}_m(A, \boldsymbol{r}_0)$。这里的 $\mathcal{K}_m(A, \boldsymbol{r}_0)$ 是由矩阵 $A$ 和初始残差 $\boldsymbol{r}_0$ 生成的 $m$ 维**克雷洛夫子空间**（Krylov subspace）。

**克雷洛夫子空间** $\mathcal{K}_m(A, \boldsymbol{r}_0)$ 定义为由向量序列 $\{\boldsymbol{r}_0, A\boldsymbol{r}_0, A^2\boldsymbol{r}_0, \dots, A^{m-1}\boldsymbol{r}_0\}$ 张成的线性子空间：
$$
\mathcal{K}_m(A, \boldsymbol{r}_0) = \operatorname{span}\{\boldsymbol{r}_0, A\boldsymbol{r}_0, A^2\boldsymbol{r}_0, \dots, A^{m-1}\boldsymbol{r}_0\}
$$
这个空间的构建是基于矩阵 $A$ 对初始残差的反复作用，它捕捉了残差在 $A$ 的作用下所传播和演变的信息。

理解克雷洛夫子空间的性质至关重要。首先，它显式地依赖于初始残差 $\boldsymbol{r}_0$。对于相同的矩阵 $A$，不同的初始残差会生成完全不同的克雷洛夫子空间序列 [@problem_id:3588192]。其次，克雷洛夫子空间通常不是矩阵 $A$ 的**不变子空间**（invariant subspace）。一个子空间 $\mathcal{S}$ 被称为 $A$ 的不变子空间，如果对于任意向量 $\boldsymbol{v} \in \mathcal{S}$，其像 $A\boldsymbol{v}$ 仍然属于 $\mathcal{S}$，即 $A\mathcal{S} \subseteq \mathcal{S}$。对于克雷洛夫子空间 $\mathcal{K}_m(A, \boldsymbol{r}_0)$，其基向量中次数最高的向量是 $A^{m-1}\boldsymbol{r}_0$。当 $A$ 作用于这个向量时，我们得到 $A(A^{m-1}\boldsymbol{r}_0) = A^m\boldsymbol{r}_0$。通常情况下，$A^m\boldsymbol{r}_0$ 不能被 $\{\boldsymbol{r}_0, \dots, A^{m-1}\boldsymbol{r}_0\}$ 线性表示，因此它不属于 $\mathcal{K}_m(A, \boldsymbol{r}_0)$。

然而，克雷洛夫子空间序列具有一个关键的嵌套和扩展属性：$A \mathcal{K}_m(A, \boldsymbol{r}_0) \subseteq \mathcal{K}_{m+1}(A, \boldsymbol{r}_0)$ [@problem_id:3588192]。这是因为 $\mathcal{K}_m$ 中的任意向量 $\boldsymbol{v}$ 都可以写成 $\boldsymbol{v} = \sum_{i=0}^{m-1} c_i A^i \boldsymbol{r}_0$ 的形式，从而 $A\boldsymbol{v} = \sum_{i=0}^{m-1} c_i A^{i+1} \boldsymbol{r}_0$，这个结果显然属于 $\mathcal{K}_{m+1}(A, \boldsymbol{r}_0)$。这个性质正是GMRES算法机制的基石，它保证了搜索空间是随着迭代次数系统性地增长的。只有在特殊情况下，例如克雷洛夫序列的维度在第 $m$ 步停止增长（即 $A^m \boldsymbol{r}_0$ 线性依赖于前面的向量），$\mathcal{K}_m(A, \boldsymbol{r}_0)$ 才会成为一个不变子空间。一个典型的例子是当初始残差 $\boldsymbol{r}_0$ 恰好是 $A$ 的一个特征向量时，$\mathcal{K}_m(A, \boldsymbol{r}_0)$ 对所有 $m \geq 1$ 都等于一维子空间 $\operatorname{span}\{\boldsymbol{r}_0\}$，而这个子空间是 $A$ 的不变子空间 [@problem_id:3588192]。

### GMRES 的最优化准则

在确定了搜索空间 $\boldsymbol{x}_0 + \mathcal{K}_m(A, \boldsymbol{r}_0)$ 后，下一个问题是如何在该空间中选择“最佳”的近似解 $\boldsymbol{x}_m$。不同的克雷洛夫子空间方法采用了不同的最优化准则。

**GMRES方法**的定义性准则是选择 $\boldsymbol{x}_m \in \boldsymbol{x}_0 + \mathcal{K}_m(A, \boldsymbol{r}_0)$，使得对应的残差 $\boldsymbol{r}_m = \boldsymbol{b} - A\boldsymbol{x}_m$ 的欧几里得范数（即 $2$-范数）达到最小 [@problem_id:3588153]。
$$
\boldsymbol{x}_m = \arg\min_{\boldsymbol{x} \in \boldsymbol{x}_0 + \mathcal{K}_m(A, \boldsymbol{r}_0)} \|\boldsymbol{b} - A\boldsymbol{x}\|_2
$$
这是一个**残差最小化**准则。这种方法的优势在于其普适性，它不要求矩阵 $A$ 具有任何特殊性质（如对称性或正定性），只需要 $A$ 是非奇异的即可。这使得GMRES成为求解来自流体力学、波传播模拟等领域的非对称线性系统的有力工具 [@problem_id:3616852]。

为了更深刻地理解GMRES，我们可以将其与为对称正定（SPD）矩阵设计的**共轭梯度法（CG）**进行对比。CG方法也在相同的克雷洛夫子空间中搜索解，但其最优化准则是最小化误差的**A-范数**（或称能量范数），即 $\|\boldsymbol{x}^* - \boldsymbol{x}_m\|_A = \sqrt{(\boldsymbol{x}^* - \boldsymbol{x}_m)^\top A (\boldsymbol{x}^* - \boldsymbol{x}_m)}$，其中 $\boldsymbol{x}^*$ 是精确解 [@problem_id:3588153, @problem_id:3616852]。

这两种不同的最优化准则导致了不同的正交性条件。对于GMRES，其一阶最优性条件可以表述为残差 $\boldsymbol{r}_m$ 与子空间 $A\mathcal{K}_m(A, \boldsymbol{r}_0)$ 正交，即 $\boldsymbol{r}_m \perp A\mathcal{K}_m(A, \boldsymbol{r}_0)$。这在几何上意味着，在将初始残差 $\boldsymbol{r}_0$ 向子空间 $A\mathcal{K}_m(A, \boldsymbol{r}_0)$ 做正交投影时，GMRES的残差 $\boldsymbol{r}_m$ 就是这个投影操作留下的正交分量。相比之下，CG方法的最优性条件是残差 $\boldsymbol{r}_m$ 与搜索空间 $\mathcal{K}_m(A, \boldsymbol{r}_0)$ 本身正交，即 $\boldsymbol{r}_m \perp \mathcal{K}_m(A, \boldsymbol{r}_0)$。只有当 $A$ 是单位矩阵的纯量倍数时，这两个准则才会对所有初始猜测都产生相同的迭代序列 [@problem_id:3588153]。

### 算法机制：Arnoldi 迭代

GMRES的核心挑战在于如何高效地求解上述范数最小化问题。直接处理这个 $n$ 维空间中的问题是困难的，但通过构建一个巧妙的基，可以将其转化为一个低维的、易于解决的问题。这个关键步骤由 **Arnoldi 过程** 完成。

Arnoldi 过程是一种迭代算法，用于为克雷洛夫子空间 $\mathcal{K}_m(A, \boldsymbol{r}_0)$ 构建一组标准正交基 $\{\boldsymbol{v}_1, \boldsymbol{v}_2, \dots, \boldsymbol{v}_m\}$ [@problem_id:3588177]。该过程从标准化的初始残差 $\boldsymbol{v}_1 = \boldsymbol{r}_0 / \|\boldsymbol{r}_0\|_2$ 开始。在第 $j$ 步，它计算向量 $A\boldsymbol{v}_j$，然后使用格拉姆-施密特（Gram-Schmidt）正交化方法将其与所有已生成的基向量 $\{\boldsymbol{v}_1, \dots, \boldsymbol{v}_j\}$ 正交，最后将结果标准化，得到新的基向量 $\boldsymbol{v}_{j+1}$。

经过 $m$ 步迭代，Arnoldi 过程生成了一个 $n \times (m+1)$ 的矩阵 $V_{m+1} = [\boldsymbol{v}_1, \dots, \boldsymbol{v}_{m+1}]$，其列向量是标准正交的，并且张成了空间 $\mathcal{K}_{m+1}(A, \boldsymbol{r}_0)$。同时，它还生成了一个 $(m+1) \times m$ 的**上Hessenberg矩阵** $\bar{H}_m$，其中包含了正交化过程中的系数。这些矩阵满足一个至关重要的关系式，即**Arnoldi关系**：
$$
A V_m = V_{m+1} \bar{H}_m
$$
其中 $V_m = [\boldsymbol{v}_1, \dots, \boldsymbol{v}_m]$。这个关系式表明，矩阵 $A$ 在由 $V_m$ 的列向量张成的子空间上的作用，可以用一个小的Hessenberg矩阵 $\bar{H}_m$ 来表示。

当矩阵 $A$ 是对称（或Hermitian）的时，Arnoldi 过程会简化。生成的Hessenberg矩阵会退化为一个对称三对角矩阵，其迭代关系也从一个长递推（需要所有先前的向量）简化为一个短的三项递推。这个特殊情况就是著名的**Lanczos过程**，它是共轭梯度法的基础 [@problem_id:3588177]。

现在，我们可以利用Arnoldi关系来转化GMRES的最小化问题。近似解 $\boldsymbol{x}_m$ 可以表示为 $\boldsymbol{x}_m = \boldsymbol{x}_0 + V_m \boldsymbol{y}$，其中 $\boldsymbol{y} \in \mathbb{C}^m$ 是待求的坐标向量。对应的残差为：
$$
\boldsymbol{r}_m = \boldsymbol{b} - A\boldsymbol{x}_m = \boldsymbol{r}_0 - A(V_m \boldsymbol{y})
$$
利用 $\boldsymbol{r}_0 = \beta \boldsymbol{v}_1$（其中 $\beta = \|\boldsymbol{r}_0\|_2$）和 Arnoldi 关系，上式可以改写为：
$$
\boldsymbol{r}_m = \beta \boldsymbol{v}_1 - V_{m+1} \bar{H}_m \boldsymbol{y}
$$
由于 $\boldsymbol{v}_1$ 是 $V_{m+1}$ 的第一列，我们可以将其写成 $\boldsymbol{v}_1 = V_{m+1} \boldsymbol{e}_1$，其中 $\boldsymbol{e}_1 = (1, 0, \dots, 0)^\top$ 是一个 $(m+1)$ 维的标准单位向量。于是：
$$
\boldsymbol{r}_m = V_{m+1}(\beta \boldsymbol{e}_1 - \bar{H}_m \boldsymbol{y})
$$
GMRES的目标是最小化 $\|\boldsymbol{r}_m\|_2$。由于 $V_{m+1}$ 的列是标准正交的，它是一个等距同构映射，即乘以 $V_{m+1}$ 不改变向量的 $2$-范数。因此，原问题等价于求解一个小的、$(m+1) \times m$ 维的最小二乘问题 [@problem_id:3588177]：
$$
\min_{\boldsymbol{y} \in \mathbb{C}^m} \|\beta \boldsymbol{e}_1 - \bar{H}_m \boldsymbol{y}\|_2
$$
这个问题可以通过QR分解（例如，使用Givens旋转）高效求解。一旦求得最优的 $\boldsymbol{y}$，就可以计算出最终的近似解 $\boldsymbol{x}_m = \boldsymbol{x}_0 + V_m \boldsymbol{y}$。

为了使这个过程更加具体，我们考虑一个源于一维声波模型的例子 [@problem_id:3616892]。设矩阵 $A$ 和向量 $\boldsymbol{b}$ 分别为：
$$
A = \begin{pmatrix} 1 + i  -1  0 \\ -1  1 + i  -1 \\ 0  -1  1 + i \end{pmatrix}, \quad \boldsymbol{b} = \begin{pmatrix} 0 \\ 1 \\ 0 \end{pmatrix}
$$
从 $\boldsymbol{x}_0 = \boldsymbol{0}$ 开始，初始残差 $\boldsymbol{r}_0 = \boldsymbol{b} = (0, 1, 0)^\top$，其范数 $\|\boldsymbol{r}_0\|_2=1$。
第一步Arnoldi过程，我们得到 $\boldsymbol{v}_1 = \boldsymbol{r}_0 / \|\boldsymbol{r}_0\|_2 = (0, 1, 0)^\top$。
接着，计算 $\boldsymbol{w} = A\boldsymbol{v}_1 = (-1, 1+i, -1)^\top$。正交化得到 $h_{11} = \boldsymbol{v}_1^H \boldsymbol{w} = 1+i$ 和 $\tilde{\boldsymbol{w}} = \boldsymbol{w} - h_{11}\boldsymbol{v}_1 = (-1, 0, -1)^\top$。标准化后得到 $h_{21} = \|\tilde{\boldsymbol{w}}\|_2 = \sqrt{2}$ 和 $\boldsymbol{v}_2 = \tilde{\boldsymbol{w}}/h_{21} = (-1/\sqrt{2}, 0, -1/\sqrt{2})^\top$。
继续第二步，计算 $A\boldsymbol{v}_2$，并与 $\boldsymbol{v}_1, \boldsymbol{v}_2$ 正交，得到 $h_{12}=\sqrt{2}$ 和 $h_{22}=1+i$。在这一步中，我们发现正交化后的向量为零，这意味着 $h_{32}=0$。
这种情况被称为“幸运分解”（lucky breakdown），它表明克雷洛夫子空间 $\mathcal{K}_2(A, \boldsymbol{r}_0)$ 是一个不变子空间，并且精确解就位于仿射子空间 $\boldsymbol{x}_0 + \mathcal{K}_2(A, \boldsymbol{r}_0)$ 中。此时，Hessenberg矩阵变为 $\bar{H}_2 = \begin{pmatrix} 1+i  \sqrt{2} \\ \sqrt{2}  1+i \\ 0  0 \end{pmatrix}$。最小二乘问题 $\|\beta \boldsymbol{e}_1 - \bar{H}_2 \boldsymbol{y}\|_2$ 的残差可以被完全消除，即最小残差范数为 $0$。因此，对于这个问题，GMRES在两步内就能收敛到精确解，得到 $\|\boldsymbol{r}_2\|_2 = 0$ [@problem_id:3616892]。

### 实际应用中的考量

#### 计算成本与内存需求

GMRES的一个显著特点是，对于一般的非对称矩阵，Arnoldi过程需要一个**长递推**关系。在第 $i$ 步，为了计算新的基向量 $\boldsymbol{v}_{i+1}$，需要将 $A\boldsymbol{v}_i$ 与所有先前生成的 $i$ 个基向量 $\boldsymbol{v}_1, \dots, \boldsymbol{v}_i$ 进行正交化。这导致GMRES的计算成本和内存需求随着迭代次数的增加而增长 [@problem_id:3588198]。

具体来说，在GMRES的第 $i$ 次迭代中，主要计算开销包括：
1.  一次稀疏矩阵-向量乘法（SpMV）：计算 $A\boldsymbol{v}_i$。
2.  $i$ 次向量内积和 $i$ 次向量加法（axpy）：用于格拉姆-施密特正交化。
3.  更新最小二乘问题：通常使用 $i$ 次Givens旋转。

经过 $m$ 步迭代，总的内存需求主要用于存储Arnoldi基向量 $V_m$，需要 $mn$ 个浮点数存储空间。总的计算量（浮点运算次数）大致为 $O(m \cdot \operatorname{nnz}(A) + \eta m^2 n)$，其中 $\operatorname{nnz}(A)$ 是 $A$ 中非零元素的数量，$\eta$ 是为了数值稳定性而进行的正交化遍数。与此相对，为对称正定矩阵设计的共轭梯度法（CG）得益于短递推关系，其每步迭代的计算量和内存需求是固定的，这使得CG在适用时通常比GMRES更高效 [@problem_id:3616852]。

#### 重启GMRES (GMRES(k))

为了解决计算成本和内存随迭代次数线性增长的问题，实践中几乎总是使用**重启GMRES**，记作GMRES(k)。该方法执行 $k$ 步标准的GMRES迭代，然后用得到的近似解作为新的初始猜测，并用其对应的残差重新开始一个包含 $k$ 步的新循环。这个过程会丢弃之前构建的整个克雷洛夫子空间 [@problem_id:3588189]。

重启策略有效地将每轮循环的内存和计算成本限制在一个固定的、可控的范围内。然而，这种策略是有代价的。每次重启都意味着丢弃了之前迭代中包含的关于矩阵 $A$ 的“长期”信息。从理论上看，这限制了算法寻找最优解的能力。

我们可以通过**残差多项式**的视角来理解这一点。在 $m$ 步之后，未重启的GMRES产生的残差可以表示为 $\boldsymbol{r}_m = p_m(A)\boldsymbol{r}_0$，其中 $p_m$ 是一个次数不超过 $m$ 且满足 $p_m(0)=1$ 的多项式，GMRES隐式地找到了使得 $\|p_m(A)\boldsymbol{r}_0\|_2$ 最小的那个 $p_m$。而经过 $s$ 轮的GMRES(k)后，总迭代步数为 $sk$，其最终残差可以表示为 $\boldsymbol{r}_{sk} = (\prod_{j=1}^s q_j(A)) \boldsymbol{r}_0$，其中每个 $q_j$ 都是一次 $k$ 步GMRES循环中找到的最优多项式（次数 $\le k, q_j(0)=1$）。尽管任何次数 $\le sk$ 且常数项为1的多项式原则上都可以分解为 $s$ 个次数 $\le k$ 的多项式之积，但GMRES(k)的优化过程是贪婪的、逐轮进行的。它在每一轮只寻找当前最优的 $q_j$，而不能进行全局优化来找到所有次数 $\le sk$ 多项式中的最佳者。这种次优性可能导致收敛速度减慢，甚至在某些情况下出现**停滞**（stagnation） [@problem_id:3588189, @problem_id:3588155]。

#### 预处理

对于许多具有挑战性的问题（如来自波传播模拟的高度非对称或不定系统），即使是GMRES也可能收敛缓慢。在这种情况下，**预处理**技术是必不可少的。预处理旨在通过一个近似的逆矩阵 $M^{-1}$ 来变换原系统，使得新系统的谱特性更有利于迭代求解。

主要有两种预处理策略 [@problem_id:3588169]：
1.  **左预处理**：求解变换后的系统 $(M^{-1}A)\boldsymbol{x} = M^{-1}\boldsymbol{b}$。在这种情况下，GMRES算法最小化的是**预处理后残差**的范数，即 $\|M^{-1}(\boldsymbol{b}-A\boldsymbol{x}_k)\|_2$。这意味着算法的收敛判据是基于变换后的残差，可能不直接反映原始问题的残差大小。
2.  **右预处理**：求解系统 $(AM^{-1})\boldsymbol{y} = \boldsymbol{b}$，然后通过 $\boldsymbol{x} = M^{-1}\boldsymbol{y}$ 恢复解。这种策略的一个显著优点是，GMRES最小化的量 $\| \boldsymbol{b} - (AM^{-1})\boldsymbol{y}_k \|_2$ 正好等于**原始残差**的范数 $\|\boldsymbol{b}-A\boldsymbol{x}_k\|_2$。这使得收敛监控更加直接和有意义，因此在实践中右预处理更受欢迎 [@problem_id:3616852]。

在计算地球物理学等领域，为频域波传播问题（如亥姆霍兹方程）设计的物理启发的预条件子，对于保证GMRES在面对复值、非对称且不定系统时的有效性至关重要 [@problem_id:3616852]。

### 收敛行为与停滞

GMRES的一个基本性质是其残差范数单调不减，即 $\|\boldsymbol{r}_{m+1}\|_2 \le \|\boldsymbol{r}_m\|_2$，因为每一步的搜索空间都是前一步的超集。然而，这并不能阻止**停滞**现象的发生，即在某一步 $m$ 之后，$\|\boldsymbol{r}_m\|_2 = \|\boldsymbol{r}_{m-1}\|_2 > 0$ [@problem_id:3588189]。

停滞的一种机制是当克雷洛夫子空间被“困”在一个特殊的 $A$-不变子空间 $S$ 中时。如果初始残差 $\boldsymbol{r}_0$ 属于 $S$，并且 $S$ 的像 $A(S)$ 与 $\boldsymbol{r}_0$ 正交，那么GMRES将无法在任何方向上减小残差。一个极端的例子是当 $\boldsymbol{r}_0$ 是矩阵 $A$ 对应于特征值0的特征向量（即 $\boldsymbol{r}_0$ 在 $A$ 的零空间中）。在这种情况下，$A\boldsymbol{r}_0 = \boldsymbol{0}$，导致所有克雷洛夫子空间都退化为 $\operatorname{span}\{\boldsymbol{r}_0\}$。因此，$A\mathcal{K}_m(A, \boldsymbol{r}_0) = \{\boldsymbol{0}\}$。GMRES试图最小化 $\|\boldsymbol{r}_0 - A\boldsymbol{y}\|_2$，其中 $A\boldsymbol{y}=\boldsymbol{0}$，这意味着最小残差就是 $\boldsymbol{r}_0$ 本身，其范数保持不变，算法完全停滞 [@problem_id:3588155]。

对于更一般的非正规矩阵，GMRES的收敛行为比特征值分布所暗示的要复杂得多。收敛速度由残差多项式范数 $\|p_m(A)\|_2$ 的下降速度决定。对于可对角化的矩阵 $A=X\Lambda X^{-1}$，我们有界：
$$
\|p(A)\|_2 \le \kappa_2(X) \max_i |p(\lambda_i)|
$$
其中 $\kappa_2(X) = \|X\|_2 \|X^{-1}\|_2$ 是特征向量矩阵 $X$ 的谱条件数 [@problem_id:3588158]。这个界表明，收敛不仅取决于特征值（影响 $\max|p(\lambda_i)|$），还强烈地依赖于矩阵的**非正规性**，由 $\kappa_2(X)$ 度量。一个高度非正规的矩阵（即 $\kappa_2(X) \gg 1$）即使其特征值分布良好（例如，远离原点），也可能导致 $\|p(A)\|_2$ 在初始阶段远大于纯谱理论预测的值。这表现为GMRES收敛曲线中初始的“驼峰”现象或平台期，即在残差开始显著下降之前，会经历一段缓慢收敛或停滞的阶段。因此，仅凭特征值来预测GMRES的性能是不可靠的；矩阵的非正规性是理解其复杂收敛行为的关键因素。