## 引言
在现代科学与工程计算中，求解形如 $A\mathbf{x} = \mathbf{b}$ 的[线性方程组](@entry_id:148943)是一项无处不在的基础任务。当[系数矩阵](@entry_id:151473) $A$ 具有大规模、稀疏且[对称正定](@entry_id:145886)（Symmetric Positive-Definite, SPD）的特性时，传统的直接求解方法（如高斯消元法）因巨大的内存开销和计算复杂度而变得不切实际。这一挑战催生了对更高效算法的需求，而[共轭梯度](@entry_id:145712)（Conjugate Gradient, CG）法正是应对这一挑战的黄金标准。它是一种优雅而强大的迭代方法，以其卓越的收敛速度和极低的内存占用，在众多计算领域中扮演着核心角色。

本文旨在系统性地剖析[共轭梯度法](@entry_id:143436)，从其深层的数学原理到广泛的实际应用。通过学习，读者将理解为何CG法对于特定类型的系统如此高效，并掌握其在不同学科背景下的应用模式。在接下来的内容中，我们将分三步深入探索CG方法。第一章**“原理与机制”**将揭示其深刻的数学基础，解释其为何高效，包括其与[优化问题](@entry_id:266749)、Krylov[子空间](@entry_id:150286)和[Lanczos算法](@entry_id:148448)的内在联系。第二章**“应用与跨学科联系”**将通过一系列来自[结构力学](@entry_id:276699)、数据科学、量子力学和计算机图形学等领域的实例，展示其解决实际问题的强大能力。最后，第三章**“动手实践”**将提供具体的计算练习，帮助读者将理论知识转化为解决问题的实践技能。

## 原理与机制

在数值计算领域，求解形如 $A\mathbf{x} = \mathbf{b}$ 的线性方程组是一个基本且普遍存在的问题。当系数矩阵 $A$ 是一个大规模、稀疏且[对称正定](@entry_id:145886) (Symmetric Positive-Definite, SPD) 的矩阵时，[共轭梯度](@entry_id:145712) (Conjugate Gradient, CG) 方法便成为首选的[迭代算法](@entry_id:160288)。这类问题广泛出现在科学与工程计算的各个分支，尤其是在使用[有限元法](@entry_id:749389)、有限差分法或[有限体积法](@entry_id:749372)离散化[偏微分方程](@entry_id:141332)时。本章将深入探讨[共轭梯度法](@entry_id:143436)的核心原理与内在机制，阐明其为何如此高效，并揭示其深刻的数学基础。

### [对称正定系统](@entry_id:172662)：基础与动机

在深入[共轭梯度法](@entry_id:143436)之前，我们必须首先理解其应用的特定问题类别：对称正定[线性系统](@entry_id:147850)。一个 $n \times n$ 的实数矩阵 $A$ 被称为**对称正定**矩阵，如果它满足两个条件：
1.  **对称性**：$A = A^T$。
2.  **正定性**：对于任意非[零向量](@entry_id:156189) $\mathbf{z} \in \mathbb{R}^n$，二次型 $\mathbf{z}^T A \mathbf{z}$ 恒为正，即 $\mathbf{z}^T A \mathbf{z} \gt 0$。

对称正定性是一个极其重要的性质，它并非凭空出现，而是深刻植根于许多物理问题的数学模型中。从根本上说，一个对称矩阵是正定的，其充要条件是它的所有[特征值](@entry_id:154894)均为实数且大于零 [@problem_id:2160083]。这一[光谱](@entry_id:185632)特性保证了矩阵 $A$ 是可逆的（因为没有零[特征值](@entry_id:154894)），从而线性系统 $A\mathbf{x} = \mathbf{b}$ 存在唯一解。更重要的是，这个特性为两类主要的求解算法——直接法和迭代法——提供了理论基础。例如，对于SPD矩阵，我们可以使用稳定且高效的**[Cholesky分解](@entry_id:147066)**（一种特殊的[LU分解](@entry_id:144767)，$A=LL^T$）来直接求解。同时，正如我们将看到的，[正定性](@entry_id:149643)也确保了共轭梯度法的收敛性 [@problem_id:2160083]。

既然存在如[Cholesky分解](@entry_id:147066)这样鲁棒的直接法，为何我们还需要迭代法呢？答案在于问题的“大规模”和“稀疏”这两个特性。对于一个稠密矩阵，$n \times n$ 的高斯消元法或[Cholesky分解](@entry_id:147066)的计算复杂度约为 $\mathcal{O}(n^3)$。然而，在许多工程应用中，矩阵 $A$ 的维度 $n$ 可能达到数百万甚至数十亿，但其中绝大多数元素为零，即矩阵是稀疏的。虽然针对稀疏矩阵的直接法在理论上可以利用稀疏性来降低计算量，但它们面临一个致命的实践障碍：**填充（fill-in）**。在分解过程中（例如计算因子 $L$），许多在原始矩阵 $A$ 中为零的位置，在 $L$ 中可能会变为非零元素。对于大规模问题，这种填充效应可能导致存储 $L$ 所需的内存变得极其巨大，远超可用资源，使得直接法变得不可行。

相比之下，[迭代法](@entry_id:194857)（如[共轭梯度法](@entry_id:143436)）通常只涉及矩阵与向量的乘积运算 ($A\mathbf{p}$)。如果 $A$ 是稀疏的，这个运算的成本与 $A$ 的非零元素数量成正比，远低于 $\mathcal{O}(n^2)$。[迭代法](@entry_id:194857)避免了显式地[分解矩阵](@entry_id:146050) $A$，因此完全不受填充问题的影响，其内存占用主要由存储矩阵 $A$ 和少数几个辅助向量（如解、残差和搜索方向）决定。正是这种对内存的节约和对[稀疏性](@entry_id:136793)的高效利用，使得迭代法成为求解大规模[稀疏线性系统](@entry_id:174902)的必然选择 [@problem_id:1393682]。

### 作为[优化问题](@entry_id:266749)的[共轭梯度法](@entry_id:143436)

共轭梯度法最优雅的理解方式之一，是将其视为一个[优化问题](@entry_id:266749)。对于一个SPD系统 $A\mathbf{x} = \mathbf{b}$，我们可以构造一个二次泛函（或称为二次型）：

$$
\Pi(\mathbf{x}) = \frac{1}{2}\mathbf{x}^T A \mathbf{x} - \mathbf{b}^T \mathbf{x}
$$

在计算力学中，这个泛函通常对应于系统的**总势能** [@problem_id:2577331]。我们来研究这个函数的梯度。利用[矩阵微积分](@entry_id:181100)法则，并考虑到 $A$ 的对称性，我们得到：

$$
\nabla \Pi(\mathbf{x}) = \frac{1}{2}(A^T + A)\mathbf{x} - \mathbf{b} = A\mathbf{x} - \mathbf{b}
$$

为了找到泛函 $\Pi(\mathbf{x})$ 的最小值点，我们令其梯度为零，即 $\nabla \Pi(\mathbf{x}) = 0$，这恰好得到了我们最初要解的[线性方程组](@entry_id:148943) $A\mathbf{x} = \mathbf{b}$。由于 $A$ 是正定的，$\Pi(\mathbf{x})$ 的Hessian矩阵（即 $A$ 本身）是正定的，这保证了 $\Pi(\mathbf{x})$ 是一个严格[凸函数](@entry_id:143075)，其[驻点](@entry_id:136617)是唯一的[全局最小值](@entry_id:165977)点。因此，[求解线性系统](@entry_id:146035) $A\mathbf{x} = \mathbf{b}$ 与最小化二次泛函 $\Pi(\mathbf{x})$ 是等价的 [@problem_id:2577331]。

这个等价关系为迭代求解提供了清晰的思路。我们可以从一个初始猜测 $\mathbf{x}_0$ 出发，然后不断寻找新的方向，一步步走向[最小值点](@entry_id:634980)。一个自然的想法是沿着“最陡峭”的方向下降，即负梯度方向。在我们的问题中，负梯度恰好是系统的**残差 (residual)**：

$$
\mathbf{r}(\mathbf{x}) = \mathbf{b} - A\mathbf{x} = -\nabla \Pi(\mathbf{x})
$$

残差 $\mathbf{r}$ 不仅表示了当前解 $\mathbf{x}$ 在多大程度上不满足方程（即“误差”），也指明了能够最快降低势能 $\Pi(\mathbf{x})$ 的方向。仅使用负梯度作为搜索方向的算法被称为**[最速下降法](@entry_id:140448)**。然而，尽管[最速下降法](@entry_id:140448)在每一步都是局部最优的，但其[全局收敛](@entry_id:635436)路径往往呈现出效率低下的“Z”字形，尤其是在[病态问题](@entry_id:137067)中。

共轭梯度法的高明之处在于它选择了比梯度方向更“聪明”的搜索方向。这种方法的迭代性质也将其与另一类经典[迭代法](@entry_id:194857)——如Jacobi或[Gauss-Seidel法](@entry_id:145727)——区分开来。后者被称为**[定常迭代法](@entry_id:144014) (stationary iterative methods)**，因为它们的迭代格式可以写成 $\mathbf{x}^{(k+1)} = T \mathbf{x}^{(k)} + \mathbf{c}$ 的形式，其中[迭代矩阵](@entry_id:637346) $T$ 和向量 $\mathbf{c}$ 在整个过程中保持不变。相比之下，共轭梯度法是一种**非[定常迭代法](@entry_id:144014) (non-stationary iterative method)**，它的更新参数（如下文的 $\alpha_k$ 和 $\beta_k$）在每一步都会根据当前迭代状态（如残差）重新计算，从而实现更具适应性和效率的搜索 [@problem_id:2160060]。

### 共轭方向的机制

共轭梯度法的核心思想是沿着一组特殊的**[A-共轭](@entry_id:746179)**（或称A-正交）方向 $\mathbf{p}_0, \mathbf{p}_1, \dots, \mathbf{p}_{n-1}$ 进行搜索。两个向量 $\mathbf{p}_i$ 和 $\mathbf{p}_j$ ($i \neq j$) 被称为[A-共轭](@entry_id:746179)，如果它们满足：

$$
\mathbf{p}_i^T A \mathbf{p}_j = 0
$$

这可以被看作是在由 $A$ 定义的[内积空间](@entry_id:271570)中的正交性，该[内积](@entry_id:158127)定义为 $\langle \mathbf{u}, \mathbf{v} \rangle_A = \mathbf{u}^T A \mathbf{v}$。[A-共轭方向](@entry_id:152908)具有一个神奇的特性：如果我们从 $\mathbf{x}_k$ 出发，沿着方向 $\mathbf{p}_k$ 走最优化的一步到达 $\mathbf{x}_{k+1}$，那么这一步并不会破坏之前在 $\mathbf{p}_0, \dots, \mathbf{p}_{k-1}$ 方向上已经达成的优化效果。这意味着，如果我们拥有一组 $n$ 个线性无关的[A-共轭方向](@entry_id:152908)，我们至多需要 $n$ 步，每一步在一个新的共轭方向上进行精确的[一维搜索](@entry_id:172782)，就能到达二次泛函的全局最小值点，即系统的精确解。

假设在第 $k$ 步，我们已经有了一个解的近似值 $\mathbf{x}_k$ 和一个[A-共轭](@entry_id:746179)的搜索方向 $\mathbf{p}_k$。我们希望找到最佳的步长 $\alpha_k$，使得新的近似解 $\mathbf{x}_{k+1} = \mathbf{x}_k + \alpha_k \mathbf{p}_k$ 对应的势能 $\Pi(\mathbf{x}_{k+1})$ 最小。这相当于进行一次**[精确线搜索](@entry_id:170557) (exact line search)**：

$$
\alpha_k = \arg\min_{\alpha} \Pi(\mathbf{x}_k + \alpha \mathbf{p}_k)
$$

通过对 $\Pi(\mathbf{x}_k + \alpha \mathbf{p}_k)$ 关于 $\alpha$ 求导并令其为零，我们可以推导出[最优步长](@entry_id:143372)的表达式。这个求导过程等价于要求新的残差 $\mathbf{r}_{k+1}$ 与当前搜索方向 $\mathbf{p}_k$ 正交，即 $\mathbf{r}_{k+1}^T \mathbf{p}_k = 0$ [@problem_id:2577331]。最终得到的步长公式为：

$$
\alpha_k = \frac{\mathbf{r}_k^T \mathbf{p}_k}{\mathbf{p}_k^T A \mathbf{p}_k}
$$

注意到，在CG的标准实现中，由于 $\mathbf{p}_k$ 的构造方式，这个公式可以简化为 $\alpha_k = \frac{\mathbf{r}_k^T \mathbf{r}_k}{\mathbf{p}_k^T A \mathbf{p}_k}$。

### 算法的精妙之处：[三项递推](@entry_id:755957)

现在，关键问题变成了：如何经济地生成这样一组[A-共轭](@entry_id:746179)的搜索方向？一种标准的方法是使用格拉姆-施密特 (Gram-Schmidt) [正交化](@entry_id:149208)过程，但应用到A-[内积](@entry_id:158127)上。例如，我们可以从一组线性无关的[基向量](@entry_id:199546)（如Krylov[子空间的基](@entry_id:160685)）开始，然后逐步将它们A-正交化。然而，这种方法需要在每一步都访问所有先前生成的方向，导致存储需求随迭代次数 $k$ [线性增长](@entry_id:157553)，即 $\mathcal{O}(nk)$，这对于大规模问题是不可接受的 [@problem_id:2379113]。

这正是[共轭梯度法](@entry_id:143436)最精妙的地方。对于对称正定矩阵 $A$，存在一个令人惊讶的简化：新的[A-共轭方向](@entry_id:152908) $\mathbf{p}_{k+1}$ 可以通过一个简单的**[三项递推关系](@entry_id:176845)**，仅利用当前的残差 $\mathbf{r}_{k+1}$ 和前一个搜索方向 $\mathbf{p}_k$ 来生成：

$$
\mathbf{p}_{k+1} = \mathbf{r}_{k+1} + \beta_k \mathbf{p}_k
$$

其中，$\beta_k$ 是一个标量，其计算公式为 $\beta_k = \frac{\mathbf{r}_{k+1}^T \mathbf{r}_{k+1}}{\mathbf{r}_k^T \mathbf{r}_k}$。这个短[递推关系](@entry_id:189264)之所以成立，背后隐藏着一个深刻的性质：CG算法生成的残差序列 $\mathbf{r}_0, \mathbf{r}_1, \dots$ 在欧几里得[内积](@entry_id:158127)下是相互正交的（即 $\mathbf{r}_i^T \mathbf{r}_j = 0$ 对 $i \neq j$）。

这种短递推机制带来了巨大的计算优势。在算法的每一步，我们只需要存储当前解向量 $\mathbf{x}_k$、[残差向量](@entry_id:165091) $\mathbf{r}_k$、搜索[方向向量](@entry_id:169562) $\mathbf{p}_k$ 以及一个用于存放 $A\mathbf{p}_k$ 的临时向量。总的内存占用是常数个 $n$ 维向量，其存储复杂度为 $\mathcal{O}(n)$，与迭代步数 $k$ 无关。这种出色的内存效率是CG方法相对于其他需要长递推的Krylov[子空间方法](@entry_id:200957)（如用于非对称系统的GMRES）的决定性优势 [@problem_id:2379113]。

综上所述，标准的[共轭梯度算法](@entry_id:747694)流程如下：

1.  选择初始猜测 $\mathbf{x}_0$，计算 $\mathbf{r}_0 = \mathbf{b} - A\mathbf{x}_0$，并令 $\mathbf{p}_0 = \mathbf{r}_0$。
2.  对于 $k = 0, 1, 2, \dots$ 直到收敛：
    a.  计算步长：$\alpha_k = \frac{\mathbf{r}_k^T \mathbf{r}_k}{\mathbf{p}_k^T A \mathbf{p}_k}$
    b.  更新解：$\mathbf{x}_{k+1} = \mathbf{x}_k + \alpha_k \mathbf{p}_k$
    c.  更新残差：$\mathbf{r}_{k+1} = \mathbf{r}_k - \alpha_k A \mathbf{p}_k$
    d.  计算下一个搜索方向的系数：$\beta_k = \frac{\mathbf{r}_{k+1}^T \mathbf{r}_{k+1}}{\mathbf{r}_k^T \mathbf{r}_k}$
    e.  更新搜索方向：$\mathbf{p}_{k+1} = \mathbf{r}_{k+1} + \beta_k \mathbf{p}_k$

### 更深层次的理论基础

CG算法的简洁背后是坚实的数学理论，它与Krylov[子空间](@entry_id:150286)和[多项式逼近](@entry_id:137391)紧密相关。

#### Krylov[子空间](@entry_id:150286)与最优性

在第 $k$ 步，CG算法生成的解 $\mathbf{x}_k$ 位于一个由初始点 $\mathbf{x}_0$ 和一个[向量子空间](@entry_id:151815)构成的[仿射空间](@entry_id:152906)中。这个[子空间](@entry_id:150286)就是由初始残差 $\mathbf{r}_0$ 和矩阵 $A$ 生成的 $k$ 阶**Krylov[子空间](@entry_id:150286)**：

$$
\mathcal{K}_k(A, \mathbf{r}_0) = \mathrm{span}\{\mathbf{r}_0, A\mathbf{r}_0, \dots, A^{k-1}\mathbf{r}_0\}
$$

CG方法的一个核心性质是，在第 $k$ 步，它找到的解 $\mathbf{x}_k \in \mathbf{x}_0 + \mathcal{K}_k(A, \mathbf{r}_0)$ 是该[仿射空间](@entry_id:152906)中“最好”的近似解。这里的“最好”有精确的含义：$\mathbf{x}_k$ 是在 $\mathbf{x}_0 + \mathcal{K}_k(A, \mathbf{r}_0)$ 中使**误差的[A-范数](@entry_id:746180)** $\| \mathbf{x}_\ast - \mathbf{x} \|_A$ 最小化的解，其中 $\mathbf{x}_\ast$ 是真实解 [@problem_id:2570995] [@problem_id:2577331]。误差的[A-范数](@entry_id:746180)定义为 $\|\mathbf{e}\|_A = \sqrt{\mathbf{e}^T A \mathbf{e}}$。最小化误差的[A-范数](@entry_id:746180)等价于最小化我们之前定义的[势能](@entry_id:748988)泛函 $\Pi(\mathbf{x})$。

对于有限元等应用背景，这种最优性具有特别的意义。由双线性形式 $a(u,v)$ 诱导的**[能量范数](@entry_id:274966)** $\|v\|_a = \sqrt{a(v,v)}$，与离散化后系数向量的[A-范数](@entry_id:746180)精确对应：$\|u_h(\mathbf{x})\|_a^2 = \mathbf{x}^T A \mathbf{x}$。因此，CG方法在每一步都在不断扩展的Krylov[子空间](@entry_id:150286)中，寻找在[能量范数](@entry_id:274966)意义下与真实解误差最小的近似解 [@problem_id:2570995]。这表明CG的收敛过程与问题内在的物理性质（能量）是相容的。

#### 有限步收敛性

在理论上（即在精确算术下），CG方法被认为是一种直接法，因为它保证在至多 $n$ 步内找到 $n \times n$ 系统的精确解。这一性质源于其与[多项式逼近](@entry_id:137391)的深刻联系。可以证明，第 $k$ 步的误差向量 $\mathbf{e}_k = \mathbf{x}_\ast - \mathbf{x}_k$ 可以表示为：

$$
\mathbf{e}_k = P_k(A) \mathbf{e}_0
$$

其中 $\mathbf{e}_0$ 是初始误差，而 $P_k$ 是一个次数至多为 $k$ 的多项式，且满足 $P_k(0)=1$。CG方法在每一步都隐式地寻找这样一个多项式，使得 $\|P_k(A)\mathbf{e}_0\|_A$ 最小。根据[Cayley-Hamilton定理](@entry_id:150551)，存在一个次数不高于 $n$ 的关于 $A$ 的**极小多项式** $m_A(\lambda)$，使得 $m_A(A)=0$。利用这个多项式，我们可以构造一个满足 $P_m(0)=1$ 的 $m$ 次多项式 $P_m(\lambda)$，使得 $P_m(A)\mathbf{e}_0 = 0$。因为CG在每一步都寻找最优多项式，它必然能在第 $m$ 步（其中 $m \le n$）或之前找到这个能使误差为零的多项式，从而达到精确解 [@problem_id:2379081]。

#### 与[Lanczos算法](@entry_id:148448)的关系

CG算法中残差的正交性和搜索方向的短递推关系并非偶然。它们是CG方法与**[Lanczos算法](@entry_id:148448)**之间紧密联系的直接结果。[Lanczos算法](@entry_id:148448)是一个用于将对称矩阵[三对角化](@entry_id:138806)的过程，它同样在Krylov[子空间](@entry_id:150286)中进行操作。当[Lanczos算法](@entry_id:148448)以[标准化](@entry_id:637219)的初始残差 $\mathbf{q}_1 = \mathbf{r}_0 / \|\mathbf{r}_0\|$ 为起始向量应用于矩阵 $A$ 时，它会生成一个正交基 $\{ \mathbf{q}_1, \dots, \mathbf{q}_k \}$ 来张成 $\mathcal{K}_k(A, \mathbf{r}_0)$。可以证明，CG算法的第 $k$ 个残差 $\mathbf{r}_k$ 与[Lanczos算法](@entry_id:148448)的第 $k+1$ 个[基向量](@entry_id:199546) $\mathbf{q}_{k+1}$ 是平行的。此外，CG的解 $\mathbf{x}_k$ 可以通过求解一个由[Lanczos过程](@entry_id:751124)生成的 $k \times k$ 的三对角小系统来得到 [@problem_id:2379110]。正是[Lanczos过程](@entry_id:751124)的[三项递推关系](@entry_id:176845)，映射到了CG算法中，才产生了其高效的短递推结构。

### 实际应用中的考量

#### 适用范围

标准CG方法的核心要求是矩阵 $A$ 必须[对称正定](@entry_id:145886)。如果 $A$ 不是对称的，但仍然可逆，我们是否就[无能](@entry_id:201612)为力了呢？一种常见的方法是将其转化为一个等价的SPD系统。通过左乘 $A^T$，原始系统 $A\mathbf{x} = \mathbf{b}$ 变为所谓的**正规方程 (normal equations)**：

$$
(A^T A) \mathbf{x} = A^T \mathbf{b}
$$

只要 $A$ 是可逆的，矩阵 $A^T A$ 就必然是对称正定的，因此可以应用CG方法求解。类似地，也可以求解 $(A A^T)\mathbf{y} = \mathbf{b}$，然后通过 $\mathbf{x} = A^T \mathbf{y}$ 得到解。然而，这种方法的代价是新系统的[条件数](@entry_id:145150) $\kappa(A^T A) = \kappa(A)^2$。条件数的平方会急剧恶化收敛速度，因此除非别无选择，通常会避免使用[正规方程](@entry_id:142238)。对于非对称系统，更合适的算法是GMRES或BiCGSTAB等 [@problem_id:2210994]。

#### [预处理](@entry_id:141204)

在实际应用中，由于[有限精度算术](@entry_id:142321)的影响，CG很少能在 $n$ 步内收敛。它被用作一种纯粹的[迭代法](@entry_id:194857)，其[收敛速度](@entry_id:636873)严重依赖于矩阵 $A$ 的**[条件数](@entry_id:145150)** $\kappa(A)$（最大[特征值](@entry_id:154894)与最小特征值之比）。条件数越大，收敛越慢。为了加速收敛，我们采用**预处理 (preconditioning)** 技术。

[预处理](@entry_id:141204)的目标是找到一个[可逆矩阵](@entry_id:171829) $P$（称为**[预处理器](@entry_id:753679)**），它在某种意义上近似于 $A$，并且形如 $P\mathbf{z}=\mathbf{d}$ 的线性系统容易求解。然后，我们将原始系统变换为一个谱特性更好（即条件数更接近1）的等价系统。例如，通过**[左预处理](@entry_id:165660)**，我们求解：

$$
(P^{-1}A)\mathbf{x} = P^{-1}\mathbf{b}
$$

然而，这里有一个陷阱：即使 $A$ 和 $P$ 都是对称的，它们的乘积 $M = P^{-1}A$ 通常**不是对称的**（除非 $P$ 和 $A$ 可交换，即 $PA=AP$）。例如，一个简单的**雅可比预处理器**，$P$ 取为 $A$ 的对角部分，就会导致 $P^{-1}A$ 非对称 [@problem_id:2194438]。非对称的系数矩阵破坏了CG算法的理论基础，使其不再适用。

为了解决这个问题，研究人员设计了**[预处理](@entry_id:141204)共轭梯度 (Preconditioned Conjugate Gradient, PCG)** 算法。PCG巧妙地对一个对称的[预处理](@entry_id:141204)系统 $C^{-1}AC^{-T}(C^T\mathbf{x}) = C^{-1}\mathbf{b}$（其中 $P=CC^T$）应用标准CG，并通过变量代换，最终得到一个只涉及求解预处理器系统 $P\mathbf{z}=\mathbf{r}$ 的算法。PCG保留了CG的效率和短递推结构，同时有效地改善了收敛性，是现代科学与工程计算中求解大规模SPD系统的标准工具。