## 引言
在现代大规模数据科学和信号处理领域，从[欠定系统](@entry_id:148701)中恢复稀疏信号是一个核心挑战。[交替方向乘子法](@entry_id:163024)（Alternating Direction Method of Multipliers, [ADMM](@entry_id:163024)）作为一种强大而灵活的优化算法，已成为解决此类问题的基石工具。它巧妙地结合了对偶分解的良好收敛性质和[增广拉格朗日法](@entry_id:170637)的易解性，尤其擅长处理具有可分离目标函数或复杂约束的凸[优化问题](@entry_id:266749)。

本文聚焦于[ADMM](@entry_id:163024)在两个标志性[稀疏优化](@entry_id:166698)问题——[基追踪](@entry_id:200728)（Basis Pursuit, BP）和[LASSO](@entry_id:751223)——上的应用。尽管这两个问题目标相似，但其数学结构上的差异（约束问题 vs. 正则化问题）为ADMM的应用提供了不同的视角和挑战。本文旨在填补理论与实践之间的鸿沟，不仅推导算法，更阐明其背后的机制。

在接下来的内容中，我们将分三个章节展开：第一章“原理与机制”将深入剖析[ADMM](@entry_id:163024)应用于BP和LASSO的基本原理，通过变量分裂技术推导其迭代公式，并解释邻近算子、投影和对偶更新等核心概念。第二章“应用与[交叉](@entry_id:147634)学科联系”将展示[ADMM](@entry_id:163024)如何扩展到机器学习、[工程控制](@entry_id:177543)和网络科学等领域的实际问题中，并探讨提高[计算效率](@entry_id:270255)的策略。最后，第三章“动手实践”将通过一系列精心设计的练习，帮助读者巩固理论知识并掌握算法的实际应用技巧。通过本文的学习，读者将能够深刻理解并熟练运用ADMM来解决各类[稀疏优化](@entry_id:166698)问题。

## 原理与机制

本章节深入探讨了将交替方向乘子法 (Alternating Direction Method of Multipliers, ADMM) 应用于[稀疏优化](@entry_id:166698)中两个核心问题——[基追踪](@entry_id:200728) (Basis Pursuit, BP) 和 LASSO (Least Absolute Shrinkage and Selection Operator) 的基本原理和核心机制。我们将从问题的数学表述出发，通过变量分裂技术构建适用于 [ADMM](@entry_id:163024) 的形式，推导其迭代步骤，并阐明这些步骤背后的数学原理，包括邻近算子、投影、对偶上升和收敛性理论。

### [稀疏优化](@entry_id:166698)的基本模型：[基追踪](@entry_id:200728)与 [LASSO](@entry_id:751223)

在深入 ADMM 的具体细节之前，我们首先需要精确地区分两个在[稀疏恢复](@entry_id:199430)领域中占据核心地位的[优化问题](@entry_id:266749)：[基追踪](@entry_id:200728)和 [LASSO](@entry_id:751223)。尽管它们都旨在从[欠定线性系统](@entry_id:756304)中寻找[稀疏解](@entry_id:187463)，但其数学表述和内在逻辑有着本质区别。

**[基追踪](@entry_id:200728) (Basis Pursuit, BP)** 是一个约束优化问题。给定一个测量矩阵 $A \in \mathbb{R}^{m \times n}$（通常 $m \ll n$）和一个观测向量 $b \in \mathbb{R}^{m}$，[基追踪](@entry_id:200728)旨在寻找一个向量 $x \in \mathbb{R}^{n}$，它在所有满足[线性约束](@entry_id:636966) $Ax = b$ 的[可行解](@entry_id:634783)中，具有最小的 $\ell_1$ 范数。其数学形式为：
$$
\min_{x \in \mathbb{R}^{n}} \|x\|_{1} \quad \text{subject to} \quad A x = b
$$
这里的核心思想是，$\ell_1$ 范数是凸的，并且是 $\ell_0$ “范数”（即非零元素个数）的最佳凸近似，因此最小化 $\ell_1$ 范数通常能有效地引导解走向稀疏。约束 $Ax=b$ 是一个**硬约束**，要求解必须精确地满足[数据一致性](@entry_id:748190)。

**[LASSO](@entry_id:751223)** 则是一个[罚函数](@entry_id:638029)形式的无约束（或更准确地说，正则化）[优化问题](@entry_id:266749)。它通过一个[正则化参数](@entry_id:162917) $\lambda > 0$ 来平衡[数据拟合](@entry_id:149007)项与稀疏性促进项。其数学形式为：
$$
\min_{x \in \mathbb{R}^{n}} \frac{1}{2}\|A x - b\|_{2}^{2} + \lambda \|x\|_{1}
$$
与[基追踪](@entry_id:200728)不同，LASSO 允许[数据拟合](@entry_id:149007)存在一定的误差，即残差 $Ax-b$ 的 $\ell_2$ 范数不为零。正则化参数 $\lambda$ 控制着这种平衡：$\lambda$ 越大，对 $\ell_1$ 范数的惩罚越重，解 $x$ 就越稀疏，但可能会以牺牲[数据拟合](@entry_id:149007)度为代价；$\lambda$ 越小，解越倾向于最小化二乘误差，[稀疏性](@entry_id:136793)则相应减弱。因此，[LASSO](@entry_id:751223) 本质上是在**模型[稀疏性](@entry_id:136793)**与**数据保真度**之间进行权衡。将约束问题转化为[罚函数](@entry_id:638029)形式，是处理含噪数据时一种更稳健和自然的选择 。

### [ADMM](@entry_id:163024) 框架：分裂、增广与交替

[ADMM](@entry_id:163024) 是一种功能强大的算法，它专门用于求解具有可分离凸[目标函数](@entry_id:267263)和[线性约束](@entry_id:636966)的[优化问题](@entry_id:266749)。其通用形式为：
$$
\min_{x, z} f(x) + g(z) \quad \text{subject to} \quad Bx + Cz = c
$$
ADMM 的核心思想是**变量分裂** (variable splitting)：将一个复杂的原始问题（例如 LASSO）分解为两个或多个更简单的子问题，每个子问题只涉及 $f$ 或 $g$ 中的一个。这种分解是通过引入辅助变量和[等式约束](@entry_id:175290)来实现的。

为了处理这个约束，ADMM 采用了**[增广拉格朗日方法](@entry_id:165608)** (Augmented Lagrangian Method)。在其**尺度形式** (scaled form) 中，我们引入一个尺度对偶变量 $u$（它与标准拉格朗日乘子 $y$ 的关系是 $u = (1/\rho)y$）和罚参数 $\rho > 0$。增广[拉格朗日函数](@entry_id:174593)定义为：
$$
L_{\rho}(x, z, u) = f(x) + g(z) + \frac{\rho}{2}\|Bx + Cz - c + u\|_{2}^{2} - \frac{\rho}{2}\|u\|_{2}^{2}
$$
ADMM 的迭代过程包括三个步骤，它交替地最小化 $L_{\rho}$ 关于 $x$ 和 $z$，然后更新对偶变量 $u$：
1.  **$x$-更新**: $x^{k+1} := \arg\min_{x} L_{\rho}(x, z^k, u^k) = \arg\min_{x} \left\{ f(x) + \frac{\rho}{2}\|Bx + Cz^k - c + u^k\|_{2}^{2} \right\}$
2.  **$z$-更新**: $z^{k+1} := \arg\min_{z} L_{\rho}(x^{k+1}, z, u^k) = \arg\min_{z} \left\{ g(z) + \frac{\rho}{2}\|Bx^{k+1} + Cz - c + u^k\|_{2}^{2} \right\}$
3.  **[对偶变量](@entry_id:143282)更新**: $u^{k+1} := u^k + Bx^{k+1} + Cz^{k+1} - c$

对偶更新步骤具有深刻的含义。令 $r^{k+1} = Bx^{k+1} + Cz^{k+1} - c$ 为第 $k+1$ 次迭代后的**原始残差** (primal residual)，即约束的违背程度。更新规则 $u^{k+1} = u^k + r^{k+1}$ 表明，对偶变量 $u$ 实际上是在累积历史上的原始残差。如果初始 $u^0 = 0$，那么 $u^k = \sum_{t=1}^{k} r^t$。这种机制类似于一个**[积分控制](@entry_id:270104)器**：只要约束没有被满足 (即 $r^t \neq 0$)，[对偶变量](@entry_id:143282)就会不断累积“误差”，从而在后续的 primal 更新中施加更强的校正力，迫使原始变量向满足约束的方向移动 。

### ADMM for [LASSO](@entry_id:751223)

我们将 ADMM 框架应用于 [LASSO](@entry_id:751223) 问题。通过引入辅助变量 $z \in \mathbb{R}^n$ 和约束 $x=z$，我们可以将 [LASSO](@entry_id:751223) 问题分裂为：
$$
\min_{x, z} \frac{1}{2}\|A x - b\|_{2}^{2} + \lambda \|z\|_{1} \quad \text{subject to} \quad x - z = 0
$$
这完美地匹配了 [ADMM](@entry_id:163024) 的一般形式，其中 $f(x) = \frac{1}{2}\|Ax-b\|_2^2$，$g(z) = \lambda \|z\|_1$，$B=I$，$C=-I$，$c=0$。现在我们推导 [ADMM](@entry_id:163024) 的三个迭代步骤。

#### $x$-更新
$x^{k+1}$ 的更新需要求解：
$$
x^{k+1} = \arg\min_{x} \left\{ \frac{1}{2}\|Ax-b\|_{2}^{2} + \frac{\rho}{2}\|x - z^k + u^k\|_{2}^{2} \right\}
$$
这是一个无约束的二次[优化问题](@entry_id:266749)。其目标函数是光滑且凸的，我们可以通过令其关于 $x$ 的梯度为零来找到最小值。梯度为：
$$
A^{\top}(Ax-b) + \rho(x - z^k + u^k) = 0
$$
整理后得到一个线性方程组：
$$
(A^{\top}A + \rho I)x = A^{\top}b + \rho(z^k - u^k)
$$
因此，$x$-更新需要求解这个线性系统来得到 $x^{k+1}$。一个关键的优点是，即使 $A$ 是病态的或非满秩的，矩阵 $A^{\top}A + \rho I$ 对于任何 $\rho > 0$ 都是正定的，因此总是可逆的。这保证了 $x$-更新步骤的稳定性和良定性 。

#### $z$-更新
$z^{k+1}$ 的更新需要求解：
$$
z^{k+1} = \arg\min_{z} \left\{ \lambda\|z\|_{1} + \frac{\rho}{2}\|x^{k+1} - z + u^k\|_{2}^{2} \right\}
$$
通过简单的代数变换，我们可以将其写成一个[标准形式](@entry_id:153058)：
$$
z^{k+1} = \arg\min_{z} \left\{ \lambda\|z\|_{1} + \frac{\rho}{2}\|z - (x^{k+1} + u^k)\|_{2}^{2} \right\}
$$
这正是**邻近算子** (proximal operator) 的定义。一个函数 $h$ 的邻近算子 $\text{prox}_{h}$ 定义为：
$$
\text{prox}_{h}(v) := \arg\min_{x} \left( h(x) + \frac{1}{2}\|x-v\|_2^2 \right)
$$
在我们的 $z$-更新中，$h(z) = (\lambda/\rho)\|z\|_1$，经过缩放后，更新可以写为：
$$
z^{k+1} = \text{prox}_{\lambda/\rho \cdot \|\cdot\|_1}(x^{k+1} + u^k)
$$
对于 $\ell_1$ 范数，其邻近算子有一个著名的闭式解，称为**[软阈值算子](@entry_id:755010)** (soft-thresholding operator)，记为 $S_{\kappa}$。对于一个向量 $v$ 和阈值 $\kappa > 0$，它的作用是分量的：
$$
(S_{\kappa}(v))_i = \text{sign}(v_i)\max\{|v_i| - \kappa, 0\}
$$
因此，$z$-更新步骤可以简洁地写为：
$$
z^{k+1} = S_{\lambda/\rho}(x^{k+1} + u^k)
$$
这个算子将 $x^{k+1} + u^k$ 的每个分量向零收缩 $\lambda/\rho$ 的距离，并将[绝对值](@entry_id:147688)小于 $\lambda/\rho$ 的分量直接设为零，从而引入[稀疏性](@entry_id:136793)。

#### 深入理解[软阈值算子](@entry_id:755010)：Moreau 分解
[软阈值算子](@entry_id:755010)的由来可以通过 Moreau 分解这一深刻的[凸分析](@entry_id:273238)工具来理解。Moreau 分解指出，对于任意正常闭[凸函数](@entry_id:143075) $f$，其共轭函数为 $f^*$，任何向量 $v$ 都可以唯一地分解为：
$$
v = \text{prox}_{f}(v) + \text{prox}_{f^*}(v)
$$
如果我们将此应用于函数 $f(x) = \kappa\|x\|_1$，我们有 $\text{prox}_{\kappa\|\cdot\|_1}(v) = v - \text{prox}_{(\kappa\|\cdot\|_1)^*}(v)$。函数 $\kappa\|\cdot\|_1$ 的 Fenchel 共轭是半径为 $\kappa$ 的 $\ell_\infty$ 范数球的指示函数，即 $I_{\{z : \|z\|_\infty \le \kappa\}}(y)$。而指示函数的邻近算子就是到该集合的欧氏投影 $P_{\{z : \|z\|_\infty \le \kappa\}}$。因此，我们得到了一个优美的关系：
$$
\text{prox}_{\kappa\|\cdot\|_1}(v) = v - P_{\{z : \|z\|_\infty \le \kappa\}}(v)
$$
利用[投影算子](@entry_id:154142)的尺度性质 $P_{\kappa C}(v) = \kappa P_C(v/\kappa)$，其中 $C$ 是单位 $\ell_\infty$球，该表达式可写作：
$$
\text{prox}_{\kappa\|\cdot\|_1}(v) = v - \kappa P_{\{z : \|z\|_\infty \le 1\}}(v/\kappa)
$$
这个公式揭示了 $\ell_1$ 范数的邻近算子（[软阈值](@entry_id:635249)）与 $\ell_\infty$ 范数球（$\ell_1$ 范数的[对偶范数](@entry_id:200340)球）的投影之间的深刻对偶关系 。

#### 对偶更新
最后，[对偶变量](@entry_id:143282)的更新遵循一般法则：
$$
u^{k+1} = u^k + (x^{k+1} - z^{k+1})
$$

### ADMM for [基追踪](@entry_id:200728)
对于[基追踪](@entry_id:200728)问题 $\min \|x\|_1$ s.t. $Ax=b$，我们同样可以使用变量分裂技术，并且有两种主流的 ADMM 公式。

#### 公式一：在目标函数中分裂
我们将问题重写为：
$$
\min_{x, z} \|z\|_1 \quad \text{subject to} \quad x=z, \quad Ax=b
$$
这个公式引入了两个约束，使得 ADMM 的结构稍微复杂一些。但一个更简洁和常见的方法是：
$$
\min_{x,z} \|z\|_1 + \iota_{\mathcal{C}}(x) \quad \text{subject to} \quad x-z=0
$$
其中 $\iota_{\mathcal{C}}(x)$ 是[仿射集](@entry_id:634284) $\mathcal{C}=\{x \in \mathbb{R}^n : Ax=b\}$ 的[指示函数](@entry_id:186820)（即当 $x \in \mathcal{C}$ 时为 $0$，否则为 $+\infty$）。

*   **$x$-更新**：求解 $\min_x \{\iota_{\mathcal{C}}(x) + \frac{\rho}{2}\|x - (z^k-u^k)\|_2^2\}$。这等价于将点 $v^k = z^k-u^k$ **投影到[仿射集](@entry_id:634284) $\mathcal{C}$ 上**。如果 $A$ 具有满行秩（这是典型情况），这个投影 $P_{\mathcal{C}}(v^k)$ 有一个[闭式](@entry_id:271343)解。投影点 $x^{k+1}$ 可以通过求解一个关于拉格朗日乘子 $\nu$ 的 $m \times m$ [线性系统](@entry_id:147850) $(AA^\top)\nu = A v^k - b$，然后设置 $x^{k+1} = v^k - A^\top\nu$ 来得到 。

*   **$z$-更新**：与 [LASSO](@entry_id:751223) 中的情况完全相同，即 $z^{k+1} = S_{1/\rho}(x^{k+1}+u^k)$。

*   **$u$-更新**：$u^{k+1} = u^k + x^{k+1} - z^{k+1}$。

#### 公式二：在约束中分裂
另一种方法是直接分裂约束 $Ax=b$。我们将问题重写为：
$$
\min_{x, z} \|x\|_1 + \iota_{\{b\}}(z) \quad \text{subject to} \quad Ax - z = 0
$$
其中 $\iota_{\{b\}}(z)$ 是单点集 $\{b\}$ 的[指示函数](@entry_id:186820)。

*   **$x$-更新**：求解 $\min_x \{\|x\|_1 + \frac{\rho}{2}\|Ax - (z^k-u^k)\|_2^2\}$。这是一个 [LASSO](@entry_id:751223) 类型的子问题。除非 $A$ 具有特殊结构（例如 $A A^\top$ 是对角阵），否则这个问题通常没有[闭式](@entry_id:271343)解，需要通过迭代方法（如 FISTA 或[内点法](@entry_id:169727)）来近似求解 。

*   **$z$-更新**：求解 $\min_z \{\iota_{\{b\}}(z) + \frac{\rho}{2}\|Ax^{k+1} - z + u^k\|_2^2\}$。这等价于将点 $Ax^{k+1}+u^k$ 投影到集合 $\{b\}$ 上，其解显然是 $z^{k+1}=b$。这个步骤非常简单。

*   **$u$-更新**：$u^{k+1} = u^k + Ax^{k+1} - z^{k+1} = u^k + Ax^{k+1} - b$。

比较这两种公式，公式一的每个子问题都有闭式解（或涉及一个固定的线性系统求解），计算上更可预测。公式二的 $x$-更新可能需要一个内部迭代循环，计算成本可能更高，但它的 $z$-更新极为简单。选择哪种公式取决于矩阵 $A$ 的结构和问题的具体规模。

### 扩展：[ADMM](@entry_id:163024) for [基追踪降噪](@entry_id:191315) (BPDN)

ADMM 的灵活性在于它可以轻松地推广到更复杂的问题。考虑[基追踪降噪](@entry_id:191315) (BPDN) 问题：
$$
\min_{x \in \mathbb{R}^{n}} \|x\|_{1} \quad \text{subject to} \quad \|A x - b\|_{2} \le \tau
$$
我们可以引入多个辅助变量和约束来使其适应 ADMM 框架。例如，引入 $z$ 来分离 $\ell_1$ 范数，引入残差 $r$ 来处理 $\ell_2$ 范数约束：
$$
\min_{x,z,r} \|z\|_{1} + I_{\mathcal{B}_{2}(\tau)}(r) \quad \text{subject to} \quad x-z=0, \quad Ax+r=b
$$
其中 $\mathcal{B}_{2}(\tau)=\{r \in \mathbb{R}^m : \|r\|_2 \le \tau\}$ 是半径为 $\tau$ 的 $\ell_2$ 球。此问题现在涉及三个[原始变量](@entry_id:753733) $(x,z,r)$ 和两个[对偶变量](@entry_id:143282) $(u,s)$。ADMM 迭代将依次更新 $x$（求解一个线性系统）、$z$（[软阈值](@entry_id:635249)操作）和 $r$（投影到 $\ell_2$ 球上），然后更新两个对偶变量。这个例子充分展示了 ADMM 处理多块、多约束问题的能力 。

### 理论基础与解释

#### 收敛性保证
[ADMM](@entry_id:163024) 的一个显著优点是其收敛性理论要求非常宽松。对于形如 $\min f(x) + g(z)$ s.t. $Ax+Bz=c$ 的问题，[ADMM](@entry_id:163024) 的收敛性通常在以下条件下得到保证：
1.  函数 $f$ 和 $g$ 是**正常、闭、凸函数** (proper, closed, and convex)。
2.  与问题相关的（无增广项的）[拉格朗日函数](@entry_id:174593)存在一个**[鞍点](@entry_id:142576)**。

对于 LASSO 和[基追踪](@entry_id:200728)问题，这些条件通常都是满足的。$\ell_1$ 范数、凸二次函数以及[仿射集](@entry_id:634284)或凸球的指示函数都是正常闭凸函数。只要原始问题有解（对于 [LASSO](@entry_id:751223) 总是如此，对于[基追踪](@entry_id:200728)，只要 $Ax=b$ 可行），[鞍点](@entry_id:142576)的存在性就能得到保证。重要的是，[ADMM](@entry_id:163024) 的收敛**不要求**[目标函数](@entry_id:267263)是光滑的或强凸的，也不对矩阵 $A$ 或 $B$ 提出强烈的假设（如满秩）。这使得 ADMM 的适用范围非常广泛 。

#### ADMM [不动点](@entry_id:156394)与 KKT 条件
[ADMM](@entry_id:163024) 算法的迭代过程最终会收敛到一个[不动点](@entry_id:156394) $(x^\star, z^\star, u^\star)$。理论分析表明，这个[不动点](@entry_id:156394)精确地满足原始[优化问题](@entry_id:266749)的 [Karush-Kuhn-Tucker (KKT) 条件](@entry_id:176491)。例如，对于[基追踪](@entry_id:200728)问题，[ADMM](@entry_id:163024) 的[不动点](@entry_id:156394)将满足 $Ax^\star=b$（原始可行性）以及 $A^\top y^\star \in \partial\|x^\star\|_1$（对偶可行性和平稳性），其中 $y^\star$ 是与约束 $Ax=b$ 相关的对偶最优解。

这个[平稳性条件](@entry_id:191085) $A^\top y^\star \in \partial\|x^\star\|_1$ 揭示了[非光滑优化](@entry_id:167581)中的**互补松弛** (complementary slackness) 条件。$\ell_1$ 范数的次梯度定义为：
$$
(\partial \|x\|_1)_i = \begin{cases} \text{sign}(x_i)  \text{if } x_i \neq 0 \\ [-1, 1]  \text{if } x_i = 0 \end{cases}
$$
因此，KKT 条件意味着：
-   如果解的第 $i$ 个分量 $x^\star_i \neq 0$，那么对偶变量的相关分量必须饱和，即 $(A^\top y^\star)_i = \text{sign}(x^\star_i)$。
-   如果 $x^\star_i = 0$，那么[对偶变量](@entry_id:143282)的相关分量必须在 $[-1, 1]$ 区间内，即 $|(A^\top y^\star)_i| \le 1$。
这建立了原始解的稀疏支撑集与[对偶变量](@entry_id:143282)取值之间的精确联系 。

#### 与 Douglas-Rachford 分裂的联系
[ADMM](@entry_id:163024) 与另一个经典的分裂算法——Douglas-Rachford (DR) 分裂算法——有着深刻的联系。对于求解 $\min f(x)+g(x)$ 的问题，[ADMM](@entry_id:163024) 应用于其共识分裂形式（即 $\min f(x)+g(z)$ s.t. $x=z$），在代数上等价于 Douglas-Rachford 算法应用于[对偶问题](@entry_id:177454)。从另一个角度看，ADMM 的迭代步骤可以通过变量代换，直接映射为作用于某个单一[状态变量](@entry_id:138790) $y$ 的 DR 迭代：
$$
y^{k+1} = \frac{1}{2}(I + R_{\gamma g}R_{\gamma f}) y^k
$$
其中 $R_{\gamma f}(y) = 2 \text{prox}_{\gamma f}(y) - y$ 是函数 $f$ 的**反射邻近算子** (reflected proximal operator)。这个算子具有明确的几何意义：它将一个点 $y$ 关于其在 $f$ 定义的[凸集](@entry_id:155617)上的投影点进行反射。例如，对于[基追踪](@entry_id:200728)问题，$\text{prox}_{\gamma f}$ 是到[仿射集](@entry_id:634284) $\{x: Ax=b\}$ 的投影，$R_{\gamma f}$ 则是跨越该[仿射空间](@entry_id:152906)的反射。而 $\text{prox}_{\gamma g}$ 是[软阈值算子](@entry_id:755010)，$R_{\gamma g}$ 则是关于收缩操作的反射。因此，ADMM 的过程可以被看作是交替地在一个[仿射空间](@entry_id:152906)和一个由 $\ell_1$ 范数诱导的几何结构之间进行反射的序列，这种观点为理解算法的行为提供了强大的几何直觉 。

### 实践中的考量

#### [停止准则](@entry_id:136282)
在实际应用中，ADMM 需要一个可靠的[停止准则](@entry_id:136282)。由于算法同时迭代原始变量和[对偶变量](@entry_id:143282)，一个好的准则应该同时监控原始可行性和对偶可行性的收敛。对于 $x-z=0$ 的共识形式，我们定义：
-   **原始残差 (Primal Residual)**: $r^k = x^k - z^k$
-   **对偶残差 (Dual Residual)**: $s^k = \rho (z^k - z^{k-1})$

对偶残差衡量了连续的 $z$ 迭代值之间的变化，与对偶变量的[平稳性条件](@entry_id:191085)相关。算法的终止条件通常是当这两个残差的范数都变得足够小时，即：
$$
\|r^k\|_2 \le \varepsilon_{\text{pri}} \quad \text{and} \quad \|s^k\|_2 \le \varepsilon_{\text{du}}
$$
其中，停止阈值 $\varepsilon_{\text{pri}}$ 和 $\varepsilon_{\text{du}}$ 通常结合了绝对公差 $\varepsilon_{\text{abs}}$ 和相对[公差](@entry_id:275018) $\varepsilon_{\text{rel}}$，以适应不同尺度的问题：
$$
\varepsilon_{\text{pri}} = \sqrt{n}\,\varepsilon_{\text{abs}} + \varepsilon_{\text{rel}} \cdot \max\{\|x^k\|_2, \|z^k\|_2\}
$$
$$
\varepsilon_{\text{du}} = \sqrt{n}\,\varepsilon_{\text{abs}} + \varepsilon_{\text{rel}} \cdot \|\rho u^k\|_2
$$
这种尺度自适应的准则是 [ADMM](@entry_id:163024) 稳健实现的关键 。

#### 性能与陷阱：罚参数 $\rho$ 的影响
ADMM 的[收敛速度](@entry_id:636873)在很大程度上取决于罚参数 $\rho$ 的选择。$\rho$ 在 $x$-更新和 $z$-更新之间起到了平衡作用。一个不当的 $\rho$ 值可能导致收敛非常缓慢。

一个常见的性能问题是 ADMM 在识别正确稀疏支撑集时的**停滞** (stalling) 现象。考虑一个简单情景，LASSO 问题中 $A=I$。此时，真实解是 $x^\star = S_\lambda(y)$。假设对于某个分量 $i$，我们有 $|y_i| = \beta > \lambda$，所以 $x^\star_i \neq 0$。然而，在 [ADMM](@entry_id:163024) 的第一次迭代中（从零初始化），$z_i^1$ 被设为 $S_{\lambda/\rho}(x_i^1)$。如果 $\rho$ 过小，则 $x_i^1 = y_i / (1+\rho)$ 的幅度可能不足以越过[软阈值算子](@entry_id:755010)的门槛 $\lambda/\rho$，导致 $z_i^1$ 被错误地设为 0。可以推导出，发生这种错误停滞的临界条件是 $\rho \le \lambda / (\beta - \lambda)$。

这意味着，如果 $\rho$ 相对于信噪比（由 $\beta-\lambda$ 体现）过小，[ADMM](@entry_id:163024) 可能需要很多次迭代才能“唤醒”一个非零系数。这个问题启发了许多高级技术，例如**自适应 $\rho$ 策略**（在迭代过程中调整 $\rho$）和**支撑集精炼步骤**，即在 ADMM 迭代中周期性地检查 KKT 条件，并强制激活那些被错误置零的系数，从而加速收敛 。