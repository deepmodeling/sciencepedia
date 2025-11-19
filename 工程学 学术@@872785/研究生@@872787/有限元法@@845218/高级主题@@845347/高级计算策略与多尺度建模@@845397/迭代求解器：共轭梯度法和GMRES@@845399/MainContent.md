## 引言
在科学与工程计算，尤其是有限元分析领域，求解形如 $A\mathbf{x} = \mathbf{b}$ 的大规模线性[代数方程](@entry_id:272665)组是一项核心且极具挑战性的任务。随着模型日益精细复杂，这些系统的维度可达数百万甚至数十亿，使得传统的高斯消元等直接求解法因其高昂的计算和内存开销而变得不切实际。[迭代求解器](@entry_id:136910)，特别是共轭梯度（CG）法和[广义最小残差](@entry_id:637119)（GMRES）法，为解决这一瓶颈提供了强大而高效的替代方案，构成了现代大规模计算的基石。然而，要高效地运用这些方法，必须深刻理解其内在机制以及它们与具体问题特性之间的紧密联系，这正是许多研究者和工程师面临的知识鸿沟。

本文旨在系统性地剖析CG和GMRES这两种主流的克雷洛夫子空间迭代法。通过学习本文，您将不仅掌握它们的基本算法流程，更能深入理解其背后的数学原理、收敛行为以及在不同应用场景下的选择依据。

- 在“**原理与机制**”一章中，我们将从[克雷洛夫子空间](@entry_id:751067)这一统一框架出发，详细推导CG和GMRES的算法，对比它们的优缺点，并阐明[预处理](@entry_id:141204)技术作为性能倍增器的关键作用。
- 接着，在“**应用与跨学科连接**”一章，我们将展示问题的物理背景（如力学、流体、化学）如何决定矩阵的性质，进而指导求解器的选择，并探讨这些方法在[非线性](@entry_id:637147)问题和优化设计等复杂计算流程中的高级应用。
- 最后，“**动手实践**”部分将提供具体的计算练习，引导您亲手实现和体验CG与[GMRES算法](@entry_id:749938)的核心步骤，将理论知识转化为实践技能。

现在，让我们从迭代求解器的基本构造单元——[克雷洛夫子空间](@entry_id:751067)开始，踏上探索这些强大数值工具的旅程。

## 原理与机制

本章旨在深入探讨[迭代求解器](@entry_id:136910)的核心原理与机制，特别关注共轭梯度（CG）法和[广义最小残差](@entry_id:637119)（GMRES）法。这些方法是有限元分析以及更广泛的科学计算领域中求解大规模线性系统的基石。我们将从[克雷洛夫子空间](@entry_id:751067)（Krylov subspace）的基本概念出发，系统地阐释这些方法的数学构造、收敛特性以及在实际应用中的考量。

### 基础：[克雷洛夫子空间](@entry_id:751067)与[投影法](@entry_id:144836)

在[有限元离散化](@entry_id:193156)后，我们通常面临求解形如 $A\mathbf{x} = \mathbf{b}$ 的大规模线性系统。直接法（如[LU分解](@entry_id:144767)）对于[大型稀疏矩阵](@entry_id:144372)而言，其计算成本和内存需求往往高得令人却步。[迭代法](@entry_id:194857)的核心思想则大相径庭：它们从一个初始猜测 $\mathbf{x}_0$ 出发，通过一系列迭代步骤生成一个解序列 $\mathbf{x}_1, \mathbf{x}_2, \dots$，并希望这个序列能快速收敛于真实解 $\mathbf{x}^* = A^{-1}\mathbf{b}$。

几乎所有现代主流的迭代方法都属于**克雷洛夫子空间法**。这类方法在一个维度随迭代次数增长的特殊[子空间](@entry_id:150286)中寻找近似解。给定初始残差 $\mathbf{r}_0 = \mathbf{b} - A\mathbf{x}_0$，第 $k$ 阶**克雷洛夫子空间**定义为：
$$ \mathcal{K}_k(A, \mathbf{r}_0) = \mathrm{span}\{\mathbf{r}_0, A\mathbf{r}_0, A^2\mathbf{r}_0, \dots, A^{k-1}\mathbf{r}_0\} $$
这个[子空间](@entry_id:150286)具有非凡的意义。它的[基向量](@entry_id:199546)是通过反复将矩阵 $A$ 作用于初始残差得到的，因此，它蕴含了关于矩阵 $A$ 特性（如其[谱分布](@entry_id:158779)）和其对误差作用方式的丰富信息。一个关键的性质是 $A\mathcal{K}_k(A, \mathbf{r}_0) \subseteq \mathcal{K}_{k+1}(A, \mathbf{r}_0)$，这表明该[子空间](@entry_id:150286)序列是逐级嵌套和扩展的。[@problem_id:2570980]

当 $A^k \mathbf{r}_0$ 能够被 $\{\mathbf{r}_0, \dots, A^{k-1}\mathbf{r}_0\}$ [线性表示](@entry_id:139970)时，克雷洛夫子空间 $\mathcal{K}_k(A, \mathbf{r}_0)$ 就不再扩张，并成为一个 **$A$-[不变子空间](@entry_id:152829)**（即 $A\mathcal{K}_k \subseteq \mathcal{K}_k$）。这种情况发生的最小维度 $k$ 等于 $A$ 关于 $\mathbf{r}_0$ 的**极小多项式**的次数。如果初始残差 $\mathbf{r}_0$ 恰好位于一个维度为 $m$ 的 $A$-不变子空间 $\mathcal{S}$ 中，那么整个[克雷洛夫子空间](@entry_id:751067)序列都将包含在 $\mathcal{S}$ 内，这意味着迭代方法至多在 $m$ 步内就能找到精确解，因为此时解的修正量已经完全包含在搜索空间内。[@problem_id:2570980] [@problem_id:2570963]

[克雷洛夫子空间](@entry_id:751067)法通过**投影**（projection）思想在[仿射空间](@entry_id:152906) $\mathbf{x}_0 + \mathcal{K}_k(A, \mathbf{r}_0)$ 中寻找第 $k$ 步的近似解 $\mathbf{x}_k$。其核心是施加一个**[正交性条件](@entry_id:168905)**于残差 $\mathbf{r}_k = \mathbf{b} - A\mathbf{x}_k$。根据测试空间（test space）$\mathcal{L}_k$ 的选择，我们区分两种主要的投影方式：
1.  **伽辽金（Galerkin）法**: 要求残差与搜索空间自身正交，即 $\mathbf{r}_k \perp \mathcal{K}_k(A, \mathbf{r}_0)$。
2.  **[彼得罗夫-伽辽金](@entry_id:174072)（[Petrov-Galerkin](@entry_id:174072)）法**: 要求残差与另一个测试空间 $\mathcal{L}_k$ 正交，即 $\mathbf{r}_k \perp \mathcal{L}_k$，其中 $\mathcal{L}_k \ne \mathcal{K}_k(A, \mathbf{r}_0)$。

这两种投影方式分别构成了[共轭梯度法](@entry_id:143436)和[广义最小残差法](@entry_id:139566)的理论基础。

### 共轭梯度（CG）法：针对[对称正定系统](@entry_id:172662)

[共轭梯度法](@entry_id:143436)是求解[对称正定](@entry_id:145886)（Symmetric Positive Definite, SPD）线性系统的首选迭代方法。其卓越的性能源于其巧妙的数学构造，既可以从最优化角度理解，也可以从投影角度解释。

#### 从最优化到[A-共轭方向](@entry_id:152908)

对于SPD矩阵 $A$，求解 $A\mathbf{x}=\mathbf{b}$ 等价于最小化二次泛函：
$$ J(\mathbf{x}) = \frac{1}{2}\mathbf{x}^{\top}A\mathbf{x} - \mathbf{b}^{\top}\mathbf{x} $$
这又等价于最小化误差的**[A-范数](@entry_id:746180)** $\| \mathbf{e} \|_A = \sqrt{\mathbf{e}^{\top}A\mathbf{e}}$，其中 $\mathbf{e} = \mathbf{x}^* - \mathbf{x}$ 是误差。

一个简单的迭代策略是**最速下降法**（Steepest Descent），它在每一步都沿着负梯度方向 $-\nabla J(\mathbf{x}_k) = \mathbf{r}_k$ 进行[线搜索](@entry_id:141607)。CG方法的第一次迭代与[最速下降法](@entry_id:140448)完全相同，即初始搜索方向 $\mathbf{p}_0 = \mathbf{r}_0$。[@problem_id:2570957] 然而，[最速下降法](@entry_id:140448)通常收敛缓慢，表现为“之”字形路径。其根本原因是，新一轮的搜索方向可能会破坏之前迭代步已达成的最优性。

CG方法通过引入**[A-共轭](@entry_id:746179)**（或称A-正交）方向的概念克服了这一缺陷。一组方向 $\{\mathbf{p}_0, \mathbf{p}_1, \dots, \mathbf{p}_{k-1}\}$ 被称为[A-共轭](@entry_id:746179)的，如果对于任意 $i \neq j$，满足 $\mathbf{p}_i^{\top}A\mathbf{p}_j = 0$。CG方法在每一步都构造一个与之前所有方向都[A-共轭](@entry_id:746179)的新搜索方向 $\mathbf{p}_k$。这意味着，当沿着新方向 $\mathbf{p}_k$ 最小化 $J(\mathbf{x})$ 时，不会影响在之前方向上已经达到的最优性。

CG算法通过一个巧妙的短递归关系式来生成这些[A-共轭方向](@entry_id:152908)：
$$ \mathbf{p}_k = \mathbf{r}_k + \beta_{k-1} \mathbf{p}_{k-1}, \quad \text{其中} \quad \beta_{k-1} = \frac{\mathbf{r}_k^{\top}\mathbf{r}_k}{\mathbf{r}_{k-1}^{\top}\mathbf{r}_{k-1}} $$
只有当 $\beta_k$ 系数在每一步都强制为零时，CG方法才退化为[最速下降法](@entry_id:140448)。[@problem_id:2570957]

#### 投影视角与[收敛理论](@entry_id:176137)

从投影的角度看，CG方法是一种[伽辽金法](@entry_id:749698)。它在仿射克雷洛夫子空间 $\mathbf{x}_0 + \mathcal{K}_k(A, \mathbf{r}_0)$ 中寻找的近似解 $\mathbf{x}_k$，恰好满足残差 $\mathbf{r}_k$ 与整个搜索空间 $\mathcal{K}_k(A, \mathbf{r}_0)$ 正交（在标准欧几里得[内积](@entry_id:158127)下）。这与最小化[A-范数](@entry_id:746180)误差的目标是等价的。[@problem_id:2570980] 此外，CG算法的一个关键副产品是所有[残差向量](@entry_id:165091)是相互正交的，即 $\mathbf{r}_i^{\top}\mathbf{r}_j = 0$ 对所有 $i \neq j$ 成立。

CG的[收敛理论](@entry_id:176137)非常优美：
- **有限步收敛**：在精确算术下，由于我们无法在 $n$ 维空间中找到超过 $n$ 个相互正交的非零向量，CG方法最多在 $n$ 步内必然会得到精确解。[@problem_id:2570862]
- **提前收敛**：实际收敛步数由 $A$ 关于初始误差 $\mathbf{e}_0$ 的极小多项式的次数决定。该次数的[上界](@entry_id:274738)是矩阵 $A$ 的不同[特征值](@entry_id:154894)的数量 $r$。因此，如果 $A$ 只有 $r  n$ 个不同的[特征值](@entry_id:154894)，CG将在至多 $r$ 步内收敛。一个极端的例子是，如果 $A = \gamma I$（只有一个[特征值](@entry_id:154894) $\gamma$），CG仅需一步即可收敛。[@problem_id:2570957] [@problem_id:2570862] [@problem_id:2570963]
- **[收敛率](@entry_id:146534)**：在实际计算中，我们更关心达到一定精度所需的迭代次数。该次数主要由矩阵的谱条件数 $\kappa(A) = \lambda_{\max}/\lambda_{\min}$ 控制，近似与 $\sqrt{\kappa(A)}$ 成正比。

### [广义最小残差](@entry_id:637119)（GMRES）法：针对一般非对称系统

当有限元模型（如包含[对流](@entry_id:141806)项的输运问题）产生[非对称矩阵](@entry_id:153254)时，CG方法不再适用。[广义最小残差](@entry_id:637119)（GMRES）法是为此类问题设计的标准工具。

#### 最小化[残差范数](@entry_id:754273)

GMRES的核心思想与CG不同。它不寻求最小化某个加权范数下的误差，而是直接在仿射[克雷洛夫子空间](@entry_id:751067) $\mathbf{x}_0 + \mathcal{K}_k(A, \mathbf{r}_0)$ 中，寻找使欧几里得[残差范数](@entry_id:754273) $\|\mathbf{r}_k\|_2 = \|\mathbf{b} - A\mathbf{x}_k\|_2$ 最小化的近似解 $\mathbf{x}_k$。[@problem_id:2570963]

#### [Arnoldi过程](@entry_id:166662)与长递归

为了实现这一目标，GMRES需要为克雷洛夫子空间 $\mathcal{K}_k(A, \mathbf{r}_0)$ 构建一个[标准正交基](@entry_id:147779)。这个任务由**[Arnoldi过程](@entry_id:166662)**完成。[Arnoldi过程](@entry_id:166662)是一个改进的[Gram-Schmidt正交化](@entry_id:143035)过程，它从初始向量 $\mathbf{v}_1 = \mathbf{r}_0 / \|\mathbf{r}_0\|_2$ 开始，迭代地生成一组[标准正交向量](@entry_id:152061) $\{\mathbf{v}_1, \dots, \mathbf{v}_k\}$，构成 $\mathcal{K}_k(A, \mathbf{r}_0)$ 的基。

在构建基的过程中，[Arnoldi过程](@entry_id:166662)自然地产生了一个关键的矩阵关系式：
$$ A V_k = V_{k+1} \bar{H}_k $$
其中 $V_k = [\mathbf{v}_1, \dots, \mathbf{v}_k]$ 是 $n \times k$ 的矩阵，其列为标准正交基；$V_{k+1}$ 是 $V_k$ 增广一列 $\mathbf{v}_{k+1}$ 得到的矩阵；而 $\bar{H}_k$ 是一个 $(k+1) \times k$ 的**[上Hessenberg矩阵](@entry_id:756367)**。[@problem_id:2570963] 这个关系式是[GMRES算法](@entry_id:749938)的数学基石。与CG的短递归不同，[Arnoldi过程](@entry_id:166662)是一个**长递归**：为了计算 $\mathbf{v}_{j+1}$，需要使其与之前所有的向量 $\mathbf{v}_1, \dots, \mathbf{v}_j$ 正交。

利用这个关系，GMRES将原始的大规模最小化问题转化为一个小的、稠密的最小二乘问题。将 $\mathbf{x}_k = \mathbf{x}_0 + V_k \mathbf{y}$ 代入[残差范数](@entry_id:754273)，我们得到：
$$ \min_{\mathbf{y} \in \mathbb{R}^k} \|\mathbf{b} - A(\mathbf{x}_0 + V_k \mathbf{y})\|_2 = \min_{\mathbf{y} \in \mathbb{R}^k} \|\mathbf{r}_0 - AV_k \mathbf{y}\|_2 = \min_{\mathbf{y} \in \mathbb{R}^k} \|\mathbf{r}_0 - V_{k+1}\bar{H}_k \mathbf{y}\|_2 $$
由于 $\mathbf{r}_0 = \|\mathbf{r}_0\|_2 \mathbf{v}_1$ 且 $V_{k+1}$ 的列是标准正交的，该问题最终简化为求解一个 $(k+1) \times k$ 的最小二乘问题：
$$ \min_{\mathbf{y} \in \mathbb{R}^k} \| \|\mathbf{r}_0\|_2 \mathbf{e}_1 - \bar{H}_k \mathbf{y} \|_2 $$
其中 $\mathbf{e}_1 = [1, 0, \dots, 0]^{\top}$。这个问题可以用[Givens旋转](@entry_id:167475)等数值稳定方法高效求解。[@problem_id:2570963]

从投影的角度看，GMRES是一种[Petrov-Galerkin方法](@entry_id:753372)，其测试空间为 $\mathcal{L}_k = A\mathcal{K}_k(A, \mathbf{r}_0)$。因此，它施加的[正交性条件](@entry_id:168905)是 $\mathbf{r}_k \perp A\mathcal{K}_k(A, \mathbf{r}_0)$。[@problem_id:2570980]

#### [收敛理论](@entry_id:176137)与[非正规矩阵](@entry_id:752668)的挑战

与CG类似，GMRES在精确算术下也具有有限步收敛性，步数同样以极小多项式的次数为[上界](@entry_id:274738)。[@problem_id:2570963] 然而，其[收敛率](@entry_id:146534)分析要复杂得多，尤其是对于**[非正规矩阵](@entry_id:752668)**（non-normal matrices，即 $A A^{\ast} \ne A^{\ast} A$），这类矩阵正是应用GMRES的典型场景。

- **基于谱的界**：如果矩阵 $A$ 是可[对角化](@entry_id:147016)的（$A = V \Lambda V^{-1}$），则收敛界中会出现[特征向量](@entry_id:151813)矩阵的条件数 $\kappa_2(V)$：
$$ \frac{\|\mathbf{r}_k\|_2}{\|\mathbf{r}_0\|_2} \le \kappa_2(V) \min_{\substack{p \in \Pi_k \\ p(0)=1}} \max_{\lambda \in \Lambda(A)} |p(\lambda)| $$
对于高度非正规的矩阵，$\kappa_2(V)$ 可能非常大，导致这个界非常松散，无法解释GMRES的实际收敛行为。仅凭[特征值分布](@entry_id:194746)良好（例如，都远离原点）远不足以保证快速收敛。[@problem_id:2570979]
- **基于值域的界**：一个更稳健的分析工具是矩阵的**值域**（field of values），$W(A) = \{\mathbf{z}^*A\mathbf{z} : \|\mathbf{z}\|_2=1\}$。对任意矩阵，收敛界可以表示为：
$$ \frac{\|\mathbf{r}_k\|_2}{\|\mathbf{r}_0\|_2} \le 2 \min_{\substack{p \in \Pi_k \\ p(0)=1}} \sup_{z \in W(A)} |p(z)| $$
如果值域 $W(A)$ 被一个不包含原点的圆盘所包含，例如 $W(A) \subset \{z : |z-c| \le \rho\}$ 且 $|c| > \rho$，那么可以推导出线性的收敛速度 $\left(\frac{\rho}{|c|}\right)^k$。这种基于值域的分析对于理解[非正规矩阵](@entry_id:752668)的收敛性至关重要。[@problem_id:2570979]

### 选择合适的求解器：比较与决策

选择最高效的迭代求解器依赖于[系统矩阵](@entry_id:172230)的代数性质。除了CG和GMRES，**[最小残差法](@entry_id:752003)（[MINRES](@entry_id:752003)）** 也是一个重要的成员，它专为对称但可能不定的[系统设计](@entry_id:755777)。

| 方法 | 矩阵要求 | 递归关系 | 迭代成本 | 内存需求 | 优化目标 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **CG** | 对称正定 (SPD) | 短递归 | 固定且低 | 固定且低 | 最小化[A-范数](@entry_id:746180)误差 |
| **[MINRES](@entry_id:752003)** | 对称（可不定） | 短递归 | 固定且低 | 固定且低 | 最小化欧氏[残差范数](@entry_id:754273) |
| **GMRES** | 任何非奇异矩阵 | 长递归 | 随迭代数[线性增长](@entry_id:157553) | 随迭代数线性增长 | 最小化欧氏[残差范数](@entry_id:754273) |

这个对比清晰地揭示了它们之间的权衡。CG和[MINRES](@entry_id:752003)效率高，但适用范围窄；GMRES普适性强，但代价是高昂的计算和存储成本。由于GMRES的成本随迭代增长，实际应用中通常使用**重启动的GMRES（[GMRES(m)](@entry_id:749937)）**，即每m次迭代后重置算法，以控制资源消耗。[@problem_id:2570884]

根据典型的有限元问题，我们可以建立一个决策流程 [@problem_id:2570921]：
- **[扩散](@entry_id:141445)问题（如Poisson方程）**：标准的Galerkin[有限元法](@entry_id:749389)产生SPD矩阵。应选择 **CG**。
- **[混合问题](@entry_id:634383)（如[Stokes流](@entry_id:138636)或[Darcy流](@entry_id:748165)）**：稳定的混合元格式通常产生对称不定（[鞍点](@entry_id:142576)）系统。CG方法会因矩阵不定而失效。此时应选择 **[MINRES](@entry_id:752003)**。[@problem_id:2570947]
- **[对流](@entry_id:141806)占优的输运问题**：为保证稳定性而采用的SUPG等方法会引入非对称项，导致矩阵非对称。应选择 **GMRES**。

### [预处理](@entry_id:141204)技术：加速收敛的关键

对于许多来自[偏微分方程](@entry_id:141332)的实际问题，尤其是网格加密后，矩阵的条件数会急剧恶化，导致[迭代求解器](@entry_id:136910)收敛极其缓慢。**预处理（Preconditioning）** 技术旨在通过变换原系统来改善其谱特性，从而加速收敛。

目标是将 $A\mathbf{x}=\mathbf{b}$ 变换为一个更容易求解的等价系统，如 $M^{-1}A\mathbf{x} = M^{-1}\mathbf{b}$（**[左预处理](@entry_id:165660)**）或 $AM^{-1}\mathbf{y} = \mathbf{b}, \mathbf{x}=M^{-1}\mathbf{y}$（**[右预处理](@entry_id:173546)**）。理想的预处理器 $M$ 应满足两个条件：(1) $M$ 在某种意义上“近似”于 $A$，使得[预处理](@entry_id:141204)后的矩阵 $M^{-1}A$ 或 $AM^{-1}$ 条件数接近1或其[谱分布](@entry_id:158779)更有利；(2) 求解形如 $M\mathbf{z}=\mathbf{r}$ 的线性系统要比求解原系统容易得多。

预处理器的选择会影响求解器的选用：
- **用于CG的[预处理器](@entry_id:753679)**：预处理CG（PCG）要求预处理后的算子仍然是SPD的。对于[左预处理](@entry_id:165660)，若 $A$ 是SPD，则要求[预处理器](@entry_id:753679) $M$ 本身也是SPD。这样，算子 $M^{-1}A$ 在由 $M$ 诱导的[内积](@entry_id:158127) $(\cdot, \cdot)_M = (\cdot)^{\top}M(\cdot)$ 下是[对称正定](@entry_id:145886)的。[@problem_id:2570954] 如果对一个SPD系统使用了一个非对称的预处理器（如[不完全LU分解](@entry_id:163424)，ILU），则必须放弃CG，转而使用GMRES。[@problem_id:2570921]
- **用于GMRES/[MINRES](@entry_id:752003)的预处理器**：GMRES对[预处理器](@entry_id:753679) $M$ 的唯一要求是其非奇异性，不要求对称或正定。[@problem_id:2570954] 而对于[MINRES](@entry_id:752003)，为保持其短递归结构，通常要求预处理后的算子对称，这同样可以通过选用SPD的[预处理器](@entry_id:753679) $M$ 来实现。[@problem_id:2570884]

对于对称不定的[鞍点系统](@entry_id:754480)，**分块预处理器**尤为有效。例如，对于形如 $K = \begin{bmatrix} A  B^{\top} \\ B  0 \end{bmatrix}$ 的系统，理想的**分块对角[预处理器](@entry_id:753679)** $P = \mathrm{diag}(A, S)$（其中 $S = BA^{-1}B^{\top}$ 是舒尔补）可以将预处理后[算子的谱](@entry_id:272027)聚集在三个固定的值 $\left\{1, \frac{1 \pm \sqrt{5}}{2}\right\}$ 上，使得[MINRES](@entry_id:752003)在几步内即可收敛，且收敛速度与网格无关。理想的**分块三角预处理器** $P = \begin{bmatrix} A  0 \\ B  -S \end{bmatrix}$ 甚至更优，它能使预处理后算子的所有[特征值](@entry_id:154894)都为1，从而GMRES在两步内收敛。在实践中，我们会使用 $A$ 和 $S$ 的谱等价近似来构造这些预处理器，以达到接近理想情况的、稳健的收敛效果。[@problem_id:2570947]

### 现实世界的考量：[有限精度算术](@entry_id:142321)

以上讨论大多基于精确算术。在计算机的浮点运算中，舍入误差会显著影响迭代方法的行为。

- **对CG的影响**：CG的短递归对舍入误差非常敏感。在[浮点运算](@entry_id:749454)中，残差的全局正交性和搜索方向的[A-共轭](@entry_id:746179)性会逐渐丢失。这导致了几个后果：
    1.  **收敛停滞**：可达到的最高精度受限于 $\varepsilon_{\text{mach}} \kappa(A)$，其中 $\varepsilon_{\text{mach}}$ 是机器精度。对于病态问题，这意味着真实残差可能远大于机器精度。[@problem_id:2571002]
    2.  **残差漂移**：递归更新的残差会与真实残差 $\mathbf{b}-A\mathbf{x}_k$ 产生偏差。因此，可靠的[停止准则](@entry_id:136282)需要周期性地显式重算真实残差。[@problem_id:2571002]
    3.  **[超线性收敛](@entry_id:141654)性丧失**：精确算术中的“[收敛加速](@entry_id:165787)”现象（[超线性收敛](@entry_id:141654)）会因正交性丢失而减弱甚至消失。[@problem_id:2571002]
    4.  CG方法不是**后向稳定**的，即其[浮点](@entry_id:749453)行为不等价于在某个微扰的固定矩阵上执行的精确算法。[@problem_id:2571002]

- **对GMRES的影响**：GMRES的长递归使其对正交性的要求更加严格。如果[Arnoldi过程](@entry_id:166662)中不执行**重正交化**（reorthogonalization），生成的[基向量](@entry_id:199546)会迅速失去正交性，导致整个最小残差的性质完全失效。因此，在实践中，为了保证GMRES的有效性和鲁棒性，重正交化（如使用修正的Gram-Schmidt法两次）是必不可少的。[@problem_id:2571002]

综上所述，虽然CG和GMRES等克雷洛夫子空间法具有优美的数学理论，但它们在有限元分析中的成功应用，离不开对[矩阵代数](@entry_id:153824)性质的深刻理解、对预处理技术的精妙运用，以及对[有限精度效应](@entry_id:193932)的审慎处理。