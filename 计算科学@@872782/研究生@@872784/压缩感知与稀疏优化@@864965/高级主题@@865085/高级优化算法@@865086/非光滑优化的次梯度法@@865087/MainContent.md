## 引言
在[现代机器学习](@entry_id:637169)、信号处理和统计学中，许多关键问题，如带有[L1正则化](@entry_id:751088)的LASSO回归，其[目标函数](@entry_id:267263)在某些点上并不可微。这种“非光滑”特性使得经典的梯度下降法失效，从而构成了一个核心的优化挑战。本文旨在系统性地介绍解决此类问题的基石——次梯度方法。我们不寻求回避非[光滑性](@entry_id:634843)，而是直面它，并利用它来构建更强大、更具解释性的模型。

为了带领读者从理论基础走向实际应用，本文分为三个循序渐进的章节。第一章 **“原理与机制”** 将深入探讨次梯度的数学定义、几何意义以及基于此构建的[次梯度](@entry_id:142710)算法，并剖析其与光滑优化的本质区别。第二章 **“应用与跨学科联系”** 将展示这些理论工具如何在压缩感知、图像恢复和[大规模机器学习](@entry_id:634451)等前沿领域中发挥关键作用，从而连接起抽象理论与具体实践。最后，在 **“动手实践”** 章节中，我们将通过一系列精心设计的编程练习，帮助您将理论知识转化为解决实际问题的能力。通过本次学习，您将掌握分析和求解[非光滑优化](@entry_id:167581)问题的核心技能。

## 原理与机制

本章旨在深入探讨[非光滑优化](@entry_id:167581)中的核心概念——次梯度，以及基于该概念构建的[优化算法](@entry_id:147840)。我们将从[凸函数](@entry_id:143075)的情形出发，严格定义次梯度及其几何意义，然后介绍基本的[次梯度](@entry_id:142710)方法，并剖析其与光滑优化中[梯度下降法](@entry_id:637322)的本质区别。随后，我们会将这些理论工具应用于[稀疏优化](@entry_id:166698)领域的两个经典问题：[LASSO](@entry_id:751223)（[最小绝对收缩和选择算子](@entry_id:751223)）与[基追踪](@entry_id:200728)（Basis Pursuit），以揭示次梯度在导出[最优性条件](@entry_id:634091)和[对偶理论](@entry_id:143133)中的关键作用。最后，我们将讨论更高级的算法思想，如邻近梯度法和[平滑技术](@entry_id:634779)，并对次梯度概念进行扩展，以处理更广泛的非凸问题。

### [次梯度](@entry_id:142710)：梯度的推广

在微积分中，梯度为我们描述[光滑函数](@entry_id:267124)在某点的[局部线性](@entry_id:266981)逼近和[最速上升方向](@entry_id:140639)提供了有力的工具。然而，在机器学习、信号处理和统计学的许多现代应用中，我们遇到的[目标函数](@entry_id:267263)往往是**非光滑 (nonsmooth)** 的，例如包含[绝对值函数](@entry_id:160606) $|x|$ 或 $\max$ 运算的函数。这些函数在某些点上不可微，梯度不存在，这使得经典的[基于梯度的优化](@entry_id:169228)方法失效。为了处理这类问题，[凸分析](@entry_id:273238)理论将梯度的概念推广为**[次梯度](@entry_id:142710) (subgradient)**。

#### [凸函数](@entry_id:143075)下的形式化定义

考虑一个定义在 $\mathbb{R}^n$ 上的**真闭凸函数 (proper, closed, convex function)** $f: \mathbb{R}^n \to \mathbb{R} \cup \{\infty\}$。对于其定义域 $\operatorname{dom} f = \{x \in \mathbb{R}^n : f(x)  \infty\}$ 内的一点 $x$，向量 $g \in \mathbb{R}^n$ 如果满足如下不等式，则被称为函数 $f$ 在点 $x$ 的一个次梯度：
$$
f(y) \ge f(x) + g^{\top}(y-x), \quad \forall y \in \mathbb{R}^n
$$
这个不等式是理解次梯度的核心。它表明，由次梯度 $g$ 定义的[仿射函数](@entry_id:635019) $h(y) = f(x) + g^{\top}(y-x)$ 在整个定义域上构成了原函数 $f(y)$ 的一个全局下界。

在任意一点 $x$，所有[次梯度](@entry_id:142710)的集合被称为 $f$ 在 $x$ 点的**[次微分](@entry_id:175641) (subdifferential)**，记作 $\partial f(x)$。即：
$$
\partial f(x) = \{ g \in \mathbb{R}^n : f(y) \ge f(x) + g^{\top}(y-x), \forall y \in \mathbb{R}^n \}
$$
[次微分](@entry_id:175641) $\partial f(x)$ 是一个闭凸集。如果 $f$ 在点 $x$ 可微，那么它的[次微分](@entry_id:175641)只包含一个元素，即该点的梯度 $\nabla f(x)$。因此，$\partial f(x) = \{\nabla f(x)\}$。这表明次梯度是梯度概念的直接推广 [@problem_id:3483126]。

#### 几何解释：[支撑超平面](@entry_id:274981)

次梯度的定义具有深刻的几何意义。一个函数的**上境图 (epigraph)** 是位于其图像上方或之上的点的集合，即 $\operatorname{epi} f = \{(y, t) \in \mathbb{R}^{n+1} : t \ge f(y)\}$。对于一个[凸函数](@entry_id:143075) $f$，其上境图是一个凸集。

在点 $x \in \operatorname{dom} f$ 处，点 $(x, f(x))$ 位于上境图的边界上。次梯度的定义不等式 $f(y) \ge f(x) + g^{\top}(y-x)$ 可以改写为 $f(x) + g^{\top}(y-x) \le f(y) \le t$ 对于所有 $(y, t) \in \operatorname{epi} f$ 均成立。这可以进一步表示为：
$$
\begin{pmatrix} -g \\ 1 \end{pmatrix}^{\top} \begin{pmatrix} y \\ t \end{pmatrix} \ge \begin{pmatrix} -g \\ 1 \end{pmatrix}^{\top} \begin{pmatrix} x \\ f(x) \end{pmatrix}
$$
这正是在 $\mathbb{R}^{n+1}$ 空间中，一个通过点 $(x, f(x))$、法向量为 $(-g, 1)$ 的超平面。该不等式表明，整个上境图 $\operatorname{epi} f$ 都位于这个[超平面](@entry_id:268044)的一侧。因此，由[次梯度](@entry_id:142710) $g$ 定义的[仿射函数](@entry_id:635019) $y \mapsto f(x) + g^{\top}(y-x)$ 恰好对应了上境图 $\operatorname{epi} f$ 在[边界点](@entry_id:176493) $(x, f(x))$ 处的一个**[支撑超平面](@entry_id:274981) (supporting hyperplane)** [@problem_id:3483126]。

当函数在某点非光滑时，例如 $f(x) = |x|$ 在 $x=0$ 处，可以有无数个[支撑超平面](@entry_id:274981)（在二维空间中是支撑线），例如斜率在 $[-1, 1]$ 之间的任何直线 $y=gx$ 都支撑着 $f(x)=|x|$ 的上境图。因此，在 $x=0$ 处，[次微分](@entry_id:175641)是区间 $\partial |0| = [-1, 1]$。

#### 关键示例：$\ell_1$ 范数

在[稀疏优化](@entry_id:166698)和[压缩感知](@entry_id:197903)中，$\ell_1$ 范数 $f(x) = \lambda \|x\|_1 = \lambda \sum_{i=1}^n |x_i|$（其中 $\lambda > 0$）扮演着至关重要的角色。由于 $\ell_1$ 范数是可分的，其在点 $x$ 的[次微分](@entry_id:175641)是其各个分量 $\lambda |x_i|$ [次微分](@entry_id:175641)的[笛卡尔积](@entry_id:154642)。对于单变量函数 $\phi(t) = \lambda|t|$：
- 若 $t \ne 0$，$\phi(t)$ 可微，其导数为 $\lambda \operatorname{sign}(t)$。因此 $\partial \phi(t) = \{\lambda \operatorname{sign}(t)\}$。
- 若 $t = 0$，根据定义，我们需要寻找所有满足 $\lambda|y| \ge 0 + g(y-0)$ 的 $g$。这要求 $g \in [-\lambda, \lambda]$。因此 $\partial \phi(0) = [-\lambda, \lambda]$。

综合起来，函数 $f(x) = \lambda \|x\|_1$ 的[次微分](@entry_id:175641) $\partial f(x)$ 由所有满足以下条件的向量 $g$ 构成 [@problem_id:3483132]：
$$
g_i \in \begin{cases}
\{\lambda \operatorname{sign}(x_i)\}   \text{if } x_i \neq 0 \\
[-\lambda, \lambda]   \text{if } x_i = 0
\end{cases}
$$
这个结果是后续讨论许多[稀疏优化](@entry_id:166698)问题的基础。

### 次梯度方法：一种迭代策略

有了[次梯度](@entry_id:142710)的定义，我们可以构建一个简单的迭代算法来最小化一个凸函数 $f$，即**[次梯度](@entry_id:142710)方法 (subgradient method)**。

#### 算法更新规则

给定当前迭代点 $x_k$，次梯度方法的更新规则如下：
1.  计算一个在 $x_k$ 处的[次梯度](@entry_id:142710) $g_k \in \partial f(x_k)$。
2.  根据步长 $\alpha_k > 0$ 更新迭代点：
    $$
    x_{k+1} = x_k - \alpha_k g_k
    $$
这个形式与[梯度下降法](@entry_id:637322)极其相似，但其行为却有本质不同。

#### 核心机制：非下降方向

在[梯度下降法](@entry_id:637322)中，负梯度方向 $- \nabla f(x_k)$ 保证了在足够小的步长下是函数值的[下降方向](@entry_id:637058)。然而，对于次梯度方法，$-g_k$ **不一定是下降方向**。这意味着，即使我们选择了一个有效的[次梯度](@entry_id:142710)，也完全有可能出现 $f(x_{k+1}) > f(x_k)$ 的情况 [@problem_id:3483150]。

我们可以通过一个简单的例子来阐明这一点。考虑一维分段线性[凸函数](@entry_id:143075) $f(x) = \max\{2x+1, -x+1\}$。该函数在 $x=0$ 处非光滑，其值为 $f(0)=1$。在这一点，两个线性部分都处于激活状态，因此其[次微分](@entry_id:175641)为两个斜率的[凸包](@entry_id:262864)，即 $\partial f(0) = \operatorname{conv}\{2, -1\} = [-1, 2]$。

假设我们从 $x_k=0$ 开始迭代，并选择次梯度 $g_k=2 \in \partial f(0)$。对于任意步长 $\alpha > 0$，下一个迭代点为 $x_{k+1} = 0 - \alpha(2) = -2\alpha$。由于 $x_{k+1}  0$，函数值由第二部分决定：$f(x_{k+1}) = f(-2\alpha) = -(-2\alpha)+1 = 2\alpha+1$。与初始值相比，函数值的增量为 $f(x_{k+1}) - f(x_k) = (2\alpha+1) - 1 = 2\alpha > 0$。这清楚地表明，一次有效的[次梯度](@entry_id:142710)步骤导致了[目标函数](@entry_id:267263)值的增加 [@problem_id:3483150]。

那么，如果[次梯度](@entry_id:142710)方法不保证函数值下降，它为何能收敛呢？其收敛性依赖于一个更微妙的性质：尽管 $f(x_{k+1})$ 可能增加，但从平均意义上讲，迭代点 $x_k$ 会越来越接近最优解集。具体来说，每一步都保证了到任意一个最优点 $x^\star$ 的欧氏距离平方的[上界](@entry_id:274738)有所减小。

#### 步长选择与收敛性

[次梯度](@entry_id:142710)方法的收敛性对步长 $\alpha_k$ 的选择非常敏感。经典的步长[选择规则](@entry_id:140784)要求步长序列是**递减但非平方可和**的，例如：
$$
\alpha_k > 0, \quad \sum_{k=1}^{\infty} \alpha_k = \infty, \quad \sum_{k=1}^{\infty} \alpha_k^2  \infty
$$
一个典型的例子是 $\alpha_k = c/k$ 或 $\alpha_k = c/\sqrt{k}$，其中 $c$ 是一个正常数。在这些条件下，对于[凸函数](@entry_id:143075)，[次梯度](@entry_id:142710)方法可以保证收敛到最优值。值得注意的是，这种收敛保证对于[次微分](@entry_id:175641)集合中任意元素的选取都成立 [@problem_id:3483132]。

回到 $\ell_1$ 范数的例子，当某个分量 $x_{k,i}=0$ 时，我们可以在 $[-\lambda, \lambda]$ 区间内任意选择次梯度分量 $g_{k,i}$。虽然理论收敛性不受具体选择的影响，但在实践中，选择 $g_{k,i}=0$ 是一种有原则的策略。这样做会使得 $x_{k+1,i} = x_{k,i} - \alpha_k g_{k,i} = 0 - 0 = 0$，即保持了该分量的[稀疏性](@entry_id:136793)。这种选择对应于[次微分](@entry_id:175641)集合 $\partial f(x_k)$ 中范数最小的元素，有助于稳定算法并促进稀疏解的形成 [@problem_id:3483132]。

### [最优性条件](@entry_id:634091)与应用

[次梯度](@entry_id:142710)的一个核心应用是刻画非光滑凸问题的[最优性条件](@entry_id:634091)，它为我们判断一个点是否为解以及如何求解提供了理论依据。

#### 费马法则与LASSO问题

对于一个凸函数 $f$，其全局最小点 $x^\star$ 的一个充分必要条件是**费马法则 (Fermat's Rule)** 的推广形式：
$$
0 \in \partial f(x^\star)
$$
这意味着，最优点的[次微分](@entry_id:175641)集合必须包含[零向量](@entry_id:156189)。

让我们将此法则应用于著名的 **[LASSO](@entry_id:751223) (Least Absolute Shrinkage and Selection Operator)** 问题。其[目标函数](@entry_id:267263)为：
$$
f(x) = \frac{1}{2}\|Ax-b\|_2^2 + \lambda\|x\|_1
$$
该函数是光滑二次项 $g(x)=\frac{1}{2}\|Ax-b\|_2^2$ 和非光滑 $\ell_1$ 正则项 $h(x)=\lambda\|x\|_1$ 的和。由于 $g(x)$ 处处可微，我们可以使用次梯度的加法法则：$\partial f(x) = \nabla g(x) + \partial h(x)$。
$\nabla g(x) = A^\top(Ax-b)$，而 $\partial h(x) = \lambda \partial\|x\|_1$。因此，最优解 $x^\star$ 必须满足：
$$
0 \in A^\top(Ax^\star - b) + \lambda \partial \|x^\star\|_1
$$
这等价于存在一个向量 $s^\star \in \partial\|x^\star\|_1$，使得 $A^\top(Ax^\star - b) + \lambda s^\star = 0$。这个[方程组](@entry_id:193238)就是 [LASSO](@entry_id:751223) 问题的**[一阶最优性条件](@entry_id:634945)**（或称 KKT 条件）[@problem_id:3483155]。

我们可以对这些条件进行更细致的解读。令残差为 $r^\star = Ax^\star - b$，矩阵 $A$ 的第 $i$ 列为 $a_i$。[最优性条件](@entry_id:634091)的分量形式为 $a_i^\top r^\star = -\lambda s_i^\star$。
- **对于非零解分量 ($x_i^\star \neq 0$)**: $s_i^\star = \operatorname{sign}(x_i^\star)$ 是唯一确定的。因此，我们得到一个等式：$a_i^\top r^\star = -\lambda \operatorname{sign}(x_i^\star)$。这意味着特征 $a_i$ 与残差的**相关性**大小恰好为 $\lambda$。
- **对于零解分量 ($x_i^\star = 0$)**: $s_i^\star$ 可以是 $[-1, 1]$ 内的任意值。因此，我们得到一个不等式：$|a_i^\top r^\star| \le \lambda$。这意味着未被模型选中的特征，其与残差的**相关性**大小不能超过 $\lambda$。

这些条件提供了一个深刻的洞见：LASSO 通过一个阈值 $\lambda$ 来控制[特征选择](@entry_id:177971)。一个非常有趣的应用是，我们可以确定使得解恰好为 $x^\star=0$ 的最小 $\lambda$ 值。此时，对所有 $i$ 都必须满足 $|a_i^\top(-b)| \le \lambda$，这等价于 $\lambda \ge \|A^\top b\|_\infty$。因此，当正则化参数 $\lambda$ 大于或等于 $\|A^\top b\|_\infty$ 时，[LASSO](@entry_id:751223) 问题会得到一个全零的[稀疏解](@entry_id:187463) [@problem_id:3483155]。

#### [基追踪](@entry_id:200728)与对偶认证

另一个密切相关的问题是**[基追踪](@entry_id:200728) (Basis Pursuit, BP)**：
$$
\min_{x \in \mathbb{R}^{n}} \|x\|_{1} \quad \text{subject to} \quad A x = b
$$
通过[拉格朗日对偶](@entry_id:638042)理论，我们可以导出其对偶问题和[最优性条件](@entry_id:634091)。最优 primal-dual 对 $(x^\star, y^\star)$ 必须满足 KKT 条件，其中包括 $A^\top y^\star \in \partial \|x^\star\|_1$。

这个条件不仅是理论上的，它还提供了一种强大的验证工具。如果我们有一个候选解 $x^\star$（满足 $Ax^\star=b$），并且能找到一个**对偶证书 (dual certificate)** $y$，使得 $A^\top y$ 满足[次梯度](@entry_id:142710)条件（即对 $x_i^\star \ne 0$ 的分量有 $(A^\top y)_i = \operatorname{sign}(x_i^\star)$，对 $x_i^\star = 0$ 的分量有 $|(A^\top y)_i| \le 1$），那么我们就可以断定 $x^\star$ 是一个最优解。

例如，对于问题 [@problem_id:3483183] 中给出的 $A, b$ 和候选解 $x^\star = (1, -2, 0)^\top$，我们可以通过[求解方程组](@entry_id:152624)和不等式来构造一个[对偶向量](@entry_id:161217) $y^\star=(1, -1)^\top$。这个 $y^\star$ 满足 $A^\top y^\star = (1, -1, 0)^\top$，而这个向量确实是 $\|x^\star\|_1$ 在 $x^\star$ 处的次梯度（因为 $s_1=1, s_2=-1, |s_3| \le 1$）。因此，$x^\star$ 的最优性得到了证明。

### 超越次梯度：高级方法与比较

尽管[次梯度](@entry_id:142710)方法具有普遍性，但其[收敛速度](@entry_id:636873)通常很慢。对于具有特定结构的问题，更高效的算法应运而生。

#### 邻近梯度法

许多[优化问题](@entry_id:266749)可以写成**复合形式 (composite form)**：$f(x) = g(x) + h(x)$，其中 $g(x)$ 是光滑凸函数，而 $h(x)$ 是凸但可能非光滑的函数（例如 $\ell_1$ 范数）。对于这类问题，我们可以使用**邻近梯度法 (proximal gradient method)**，其著名实例是 **ISTA (Iterative Shrinkage-Thresholding Algorithm)**。

其迭代步骤为：
$$
x^{k+1} = \mathrm{prox}_{t h}(x^k - t \nabla g(x^k))
$$
其中 $t$ 是步长，$\mathrm{prox}_{th}$ 是函数 $h$ 的**邻近算子 (proximal operator)**，定义为：
$$
\mathrm{prox}_{t h}(y) = \arg\min_{u} \left\{ h(u) + \frac{1}{2t}\|u-y\|^2 \right\}
$$
邻近算子可以看作是处理非光滑项 $h$ 的一种“向后”步骤，而梯度步 $x^k - t \nabla g(x^k)$ 则是处理光滑项 $g$ 的“向前”步骤。

与次梯度方法相比，邻近梯度法在[收敛速度](@entry_id:636873)上有显著优势 [@problem_id:3483133]：
- **迭代复杂度**：对于一般凸问题，为达到 $\varepsilon$ 精度，[次梯度法](@entry_id:164760)需要 $\mathcal{O}(1/\varepsilon^2)$ 次迭代，而邻近梯度法仅需 $\mathcal{O}(1/\varepsilon)$ 次。对于强凸问题，邻近梯度法可以达到[线性收敛](@entry_id:163614)速度 $\mathcal{O}(\log(1/\varepsilon))$，而[次梯度法](@entry_id:164760)最好也只能达到 $\mathcal{O}(1/\varepsilon)$。
- **计算成本权衡**：邻近梯度法的巨大优势是有条件的：邻近算子 $\mathrm{prox}_{th}$ 的计算必须是高效的。幸运的是，对于许多重要的[非光滑函数](@entry_id:175189)，如 $\ell_1$ 范数（其邻近算子是**[软阈值](@entry_id:635249) (soft-thresholding)**）、组稀疏正则项或简单凸集的指示函数，其邻近算子具有[闭式](@entry_id:271343)解或可以快速计算。在这些情况下，其单次迭代成本与[次梯度法](@entry_id:164760)相当，但迭代次数大大减少，从而在总计算复杂度上胜出。

#### [平滑技术](@entry_id:634779)与加速

另一种处理非光滑项的强大技术是**平滑 (smoothing)**。其思想是用一个光滑函数 $h_\mu$ 来逼近[非光滑函数](@entry_id:175189) $h$，其中 $\mu > 0$ 是平滑参数。然后，我们可以对整个光滑化的[目标函数](@entry_id:267263) $f_\mu = g + h_\mu$ 应用快速的梯度方法，例如 **Nesterov 加速梯度法**。

然而，这种方法引入了新的权衡 [@problem_id:3483147]：
- **优化误差**：对 $f_\mu$ 进行优化的误差。
- **逼近误差**：由 $h_\mu$ 替换 $h$ 引入的误差，即 $|f(x) - f_\mu(x)|$。

总误差是这两者之和。平滑参数 $\mu$ 在其中扮演了“偏置-[方差](@entry_id:200758)”权衡的角色：
- 较小的 $\mu$ 使 $h_\mu$ 更接近 $h$，从而**减小逼近误差（偏置）**。但同时，$\nabla h_\mu$ 的 Lipschitz 常数会变得很大（通常是 $\mathcal{O}(1/\mu)$），导致**优化更困难，优化误差（[方差](@entry_id:200758)）增加**。
- 较大的 $\mu$ 使 $f_\mu$ 更光滑，优化更容易，但逼近误差也更大。

为了获得最佳性能，需要明智地选择 $\mu$ 来平衡这两个误差源。例如，在 [@problem_id:3483147] 的分析中，通过对 [LASSO](@entry_id:751223) 问题的 Huber 平滑进行细致分析，可以推导出在固定迭代次数 $T$ 下，最小化总误差[上界](@entry_id:274738)的最佳平滑参数为 $\mu^\star = \mathcal{O}(1/\sqrt{T})$。

当我们将[平滑技术](@entry_id:634779)与 Nesterov 加速相结合时，可以得到更快的[收敛速度](@entry_id:636873)，例如 $\mathcal{O}(1/\sqrt{\varepsilon})$。然而，这种加速效果并非无条件的。详细的[复杂度分析](@entry_id:634248) [@problem_id:3483151] 表明，只有在精度要求不高（即 $\varepsilon$ 较大）的区域，这种方法才能体现出相对于 ISTA 的优势。在高精度区域，由平滑引入的误差项会主导复杂度，使其退化为 $\mathcal{O}(1/\varepsilon)$。

### 扩展至非凸问题

现实世界中的许多问题本质上是**非凸 (nonconvex)** 的。[次梯度](@entry_id:142710)的概念可以被推广，以处理更广泛的局部 Lipschitz [连续函数](@entry_id:137361)，即使它们不是凸函数。

#### Clarke [次微分](@entry_id:175641)

对于一个局部 Lipschitz [连续函数](@entry_id:137361) $f$（不一定是凸函数），我们可以定义**Clarke 广义方向导数 (Clarke generalized directional derivative)**：
$$
f^{\circ}(x; d) = \limsup_{y \to x, t \downarrow 0} \frac{f(y+td) - f(y)}{t}
$$
基于此，**Clarke [次微分](@entry_id:175641) (Clarke subdifferential)** $\partial^c f(x)$ 定义为所有满足 $g^\top d \le f^\circ(x;d)$ 的向量 $g$ 的集合。$\partial^c f(x)$ 仍然是一个非空、紧、凸集。

一个关键性质是，如果 $f$ 是[凸函数](@entry_id:143075)，那么其 Clarke [次微分](@entry_id:175641)与我们之前定义的凸[次微分](@entry_id:175641)是完全一致的 [@problem_id:3483123]。例如，对于 $f(x)=\|x\|_2$，其在 $x=0$ 处的 Clarke [次微分](@entry_id:175641)和凸[次微分](@entry_id:175641)都是单位欧氏球 $\{g: \|g\|_2 \le 1\}$。

#### 在[非凸优化](@entry_id:634396)中的应用与局限

Clarke [次微分](@entry_id:175641)的一个重要应用领域是**差分凸 (Difference of Convex, DC)** 函数规划，其[目标函数](@entry_id:267263)形如 $f(x) = f_1(x) - f_2(x)$，其中 $f_1, f_2$ 均为凸函数。例如，一个用于促进更强稀疏性的非凸正则项是 $f(x)=\|x\|_1 - \|x\|_2$。对于这类函数，Clarke [次微分](@entry_id:175641)可以方便地计算为 $\partial^c f(x) = \partial f_1(x) - \partial f_2(x)$ [@problem_id:3483134]。

对于非凸[目标函数](@entry_id:267263) $J(x)$，一个点 $x^\star$ 成为局部最小点的必要条件是它是一个 **Clarke 稳定点 (Clarke stationary point)**，即 $0 \in \partial^c J(x^\star)$。

然而，将次梯度方法直接应用于非凸问题时，我们会遇到许多在凸情况下不存在的困难 [@problem_id:3483134]：
- **收敛性**：算法不再保证收敛到全局或局部最小值。它最多只能保证其[聚点](@entry_id:177089)是 Clarke 稳定点，而稳定点可能是局部最小、局部最大甚至是[鞍点](@entry_id:142576)。
- **非下降性**：函数值非单调的现象会更加普遍。
- **发散与循环**：步长选择不当可能导致算法发散或陷入循环。

因此，尽管[次梯度](@entry_id:142710)概念为我们分析非凸问题提供了理论工具，但设计稳定且高效的[非凸优化](@entry_id:634396)算法需要更精巧的策略，例如 DC 算法、[近端梯度法](@entry_id:634891)的变体或[基于模型的优化](@entry_id:635801)方法。[次梯度](@entry_id:142710)方法在非凸领域更多地扮演了基础分析工具和算法设计的起点。