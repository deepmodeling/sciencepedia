## 引言
在求解[非线性优化](@entry_id:143978)问题时，牛顿法以其二次[收敛速度](@entry_id:636873)展现了强大的威力。然而，对于现代科学与工程中常见的大规模问题，其对Hessian矩阵的计算、存储和求逆需求构成了难以逾越的计算瓶颈。这引出了一个核心问题：我们能否在保持快速收敛特性的同时，有效规避直接处理Hessian矩阵所带来的巨大开销？

拟牛顿法（Quasi-Newton Methods）正是为解决这一挑战而生。本文将系统地引导你深入理解这一类强大的[优化算法](@entry_id:147840)。在接下来的内容中，你将学习到：

在 **“原理与机制”** 一章中，我们将揭示拟[牛顿法](@entry_id:140116)的基石——[割线条件](@entry_id:164914)，并推导其如何从迭代信息中构建Hessian矩阵的有效近似，从而催生出著名的BFGS和DFP等算法。

接着，在 **“应用与跨学科联系”** 一章中，我们将探索拟牛顿法（特别是其内存受限变体[L-BFGS](@entry_id:167263)）如何在机器学习、[计算化学](@entry_id:143039)和工程设计等前沿领域中，解决拥有数百万变量的真实世界问题。

最后，通过 **“动手实践”** 部分，你将有机会将理论付诸实践，亲手实现并应用这些算法来解决具体的优化任务。

让我们从第一章开始，深入探究拟牛顿法的基本 **原理与机制**。

## 原理与机制

在上一章中，我们介绍了[优化问题](@entry_id:266749)的背景以及求解这些问题的基本思想。牛顿法因其二次收敛速度而成为一个强大的工具，但它的实际应用常常受限于一个关键的计算瓶颈：Hessian 矩阵的计算、存储和求逆。对于拥有成千上万个变量的现代[大规模优化](@entry_id:168142)问题，[牛顿法](@entry_id:140116)每一步迭代所需的 $O(n^3)$ 计算成本是难以承受的 。

本章将深入探讨拟牛顿法（Quasi-Newton Methods）的原理与机制。这类方法巧妙地绕过了直接计算 Hessian 矩阵的障碍，代之以一个在每次迭代中逐步完善的近似矩阵。通过这种方式，拟牛顿法在保持[超线性收敛](@entry_id:141654)（superlinear convergence）这一优良性质的同时，将每次迭代的计算成本显著降低至更为实际的 $O(n^2)$ 水平 。我们将从拟[牛顿法](@entry_id:140116)的核心方程——[割线条件](@entry_id:164914)（secant condition）出发，揭示其如何捕捉函数曲率信息，并进一步探讨如何从该条件推导出著名的 BFGS 和 DFP 等具体算法。

### [割线条件](@entry_id:164914)：捕捉曲率信息

所有拟[牛顿法](@entry_id:140116)的基石都是**[割线条件](@entry_id:164914)**。为了理解它，让我们首先定义两个关键的向量。假设我们从当前迭代点 $\mathbf{x}_k$ 移动到下一个点 $\mathbf{x}_{k+1}$，我们定义：

- **步长向量 (step vector)**: $\mathbf{s}_k = \mathbf{x}_{k+1} - \mathbf{x}_k$
- **梯度差向量 (gradient difference vector)**: $\mathbf{y}_k = \nabla f(\mathbf{x}_{k+1}) - \nabla f(\mathbf{x}_k)$

回顾[多元函数](@entry_id:145643)的泰勒展开式，梯度的变化可以近似表示为：
$$ \nabla f(\mathbf{x}_{k+1}) \approx \nabla f(\mathbf{x}_k) + \nabla^2 f(\mathbf{x}_k) (\mathbf{x}_{k+1} - \mathbf{x}_k) $$
整理上式，我们得到 $\mathbf{y}_k \approx \nabla^2 f(\mathbf{x}_k) \mathbf{s}_k$。这个关系式启发我们，可以用迭代中实际观测到的量（$\mathbf{s}_k$ 和 $\mathbf{y}_k$）来约束我们对 Hessian 矩阵的近似。

拟牛顿法的核心思想是，要求新的 Hessian 近似矩阵 $\mathbf{B}_{k+1}$ 满足以下方程：
$$ \mathbf{B}_{k+1} \mathbf{s}_k = \mathbf{y}_k $$
这就是**[割线条件](@entry_id:164914)**。它强制要求我们构建的二次模型在最近的搜索方向 $\mathbf{s}_k$ 上，其曲率能够匹配[目标函数](@entry_id:267263) $f$ 的真实曲率。

[割线条件](@entry_id:164914)具有深刻的几何意义 。在 $\mathbf{x}_{k+1}$ 点，我们构建一个二次模型 $m_{k+1}(\mathbf{p}) = f(\mathbf{x}_{k+1}) + \nabla f(\mathbf{x}_{k+1})^T \mathbf{p} + \frac{1}{2}\mathbf{p}^T \mathbf{B}_{k+1}\mathbf{p}$。根据构造，该模型的梯度在 $\mathbf{p}=\mathbf{0}$ 处（即 $\mathbf{x}_{k+1}$ 点）自然与真实函数梯度 $\nabla f(\mathbf{x}_{k+1})$ 相匹配。[割线条件](@entry_id:164914)则施加了一个额外的约束：它确保了该模型的梯度在 $\mathbf{p}=-\mathbf{s}_k$ 处（即上一个迭代点 $\mathbf{x}_k$）也与真实函数梯度 $\nabla f(\mathbf{x}_k)$ 相匹配。换言之，[割线条件](@entry_id:164914)使得我们的二次模型在 $\mathbf{x}_k$ 和 $\mathbf{x}_{k+1}$ 这两个点上都与[目标函数](@entry_id:267263) $f$ 实现了梯度上的一致性。

此外，向量 $\mathbf{s}_k$ 和 $\mathbf{y}_k$ 本身也蕴含了丰富的曲率信息。标量 $\frac{\mathbf{s}_k^T \mathbf{y}_k}{\mathbf{s}_k^T \mathbf{s}_k}$ 可以被解释为函数 $f$ 沿方向 $\mathbf{s}_k$ 的**平均曲率** 。对于二次函数 $f(\mathbf{x}) = \frac{1}{2}\mathbf{x}^T \mathbf{A} \mathbf{x} + \mathbf{b}^T \mathbf{x} + c$，我们有 $\mathbf{y}_k = \mathbf{A} \mathbf{s}_k$，此时该比值精确等于[瑞利商](@entry_id:137794)（Rayleigh quotient），即函数在该方向上的真实曲率。

### 更新公式的推导：最小变动原则

[割线条件](@entry_id:164914) $\mathbf{B}_{k+1} \mathbf{s}_k = \mathbf{y}_k$ 为我们提供了 $n$ 个[线性方程](@entry_id:151487)。然而，一个对称的 Hessian 近似矩阵 $\mathbf{B}_{k+1}$ 含有 $\frac{n(n+1)}{2}$ 个独立元素。当问题维度 $n > 1$ 时，这是一个欠定[方程组](@entry_id:193238)（underdetermined system），意味着有无穷多个矩阵 $\mathbf{B}_{k+1}$ 满足[割线条件](@entry_id:164914)。

为了从中选择一个唯一的、性质优良的矩阵，我们需要引入一个额外的准则。这个准则就是**最小变动原则**（least-change principle）。其核心思想是：在所有满足[割线条件](@entry_id:164914)的[对称矩阵](@entry_id:143130)中，我们选择与当前 Hessian 近似矩阵 $\mathbf{B}_k$“最接近”的那一个。这里的“接近”是通过某种合适的[矩阵范数](@entry_id:139520)来度量的。这个原则可以表述为一个[约束优化](@entry_id:635027)问题：
$$ \min_{\mathbf{B}} \|\mathbf{B} - \mathbf{B}_k\| \quad \text{subject to} \quad \mathbf{B} \mathbf{s}_k = \mathbf{y}_k, \quad \mathbf{B} = \mathbf{B}^T $$
通过选择不同的[矩阵范数](@entry_id:139520)，并决定是更新 Hessian 近似 $\mathbf{B}_k$ 还是其逆矩阵 $\mathbf{H}_k = \mathbf{B}_k^{-1}$，我们便可以推导出不同的拟牛顿更新公式，例如著名的 BFGS 和 DFP 算法。最终的更新公式通常是秩为 1 或 2 的修正，这使得更新计算非常高效。

### 主要算法与更新策略

在实际应用中，拟[牛顿法](@entry_id:140116)主要有两种策略来利用 Hessian 近似矩阵 。

1.  **更新 Hessian 近似 $\mathbf{B}_k$**：在这种策略下，每一步迭代都需要[求解线性方程组](@entry_id:169069) $\mathbf{B}_k \mathbf{p}_k = -\nabla f(\mathbf{x}_k)$ 来获得搜索方向 $\mathbf{p}_k$。对于[稠密矩阵](@entry_id:174457)，这通常需要 $O(n^3)$ 的计算量（或通过更新矩阵的分解以 $O(n^2)$ 的代价来完成），这在一定程度上削弱了拟牛顿法的计算优势。

2.  **更新逆 Hessian 近似 $\mathbf{H}_k$**：这种更为流行的策略直接维护和更新 Hessian 的逆矩阵的近似 $\mathbf{H}_k$。如此一来，搜索方向的计算就简化为一个矩阵-向量乘法：$\mathbf{p}_k = -\mathbf{H}_k \nabla f(\mathbf{x}_k)$。这个操作的计算成本仅为 $O(n^2)$，从而完全避免了求解线性方程组的昂贵开销。这是大多数现代拟[牛顿法](@entry_id:140116)实现的首选方式。

下面我们介绍两种最经典的拟牛顿算法：BFGS 和 DFP。

#### Broyden–Fletcher–Goldfarb–Shanno (BFGS) 算法

BFGS 算法是目前公认的最有效、最流行的拟牛顿算法。它同样源于最小变动原则。

-   **BFGS 对 $\mathbf{B}_k$ 的更新公式**  如下：
    $$ \mathbf{B}_{k+1} = \mathbf{B}_k - \frac{\mathbf{B}_k \mathbf{s}_k \mathbf{s}_k^T \mathbf{B}_k}{\mathbf{s}_k^T \mathbf{B}_k \mathbf{s}_k} + \frac{\mathbf{y}_k \mathbf{y}_k^T}{\mathbf{y}_k^T \mathbf{s}_k} $$

-   **BFGS 对 $\mathbf{H}_k$ 的更新公式**  更为常用，形式如下：
    $$ \mathbf{H}_{k+1} = \left(\mathbf{I} - \rho_k \mathbf{s}_k \mathbf{y}_k^T\right) \mathbf{H}_k \left(\mathbf{I} - \rho_k \mathbf{y}_k \mathbf{s}_k^T\right) + \rho_k \mathbf{s}_k \mathbf{s}_k^T, \quad \text{其中 } \rho_k = \frac{1}{\mathbf{y}_k^T \mathbf{s}_k} $$

一次典型的 BFGS 迭代过程包括以下步骤  ：
1.  计算搜索方向：$\mathbf{p}_k = -\mathbf{H}_k \nabla f(\mathbf{x}_k)$。
2.  执行[线搜索](@entry_id:141607)：找到一个合适的步长 $\alpha_k$，使得 $f(\mathbf{x}_k + \alpha_k \mathbf{p}_k)$ 得到充分下降。
3.  更新位置：$\mathbf{x}_{k+1} = \mathbf{x}_k + \alpha_k \mathbf{p}_k$。
4.  计算 $\mathbf{s}_k = \mathbf{x}_{k+1} - \mathbf{x}_k$ 和 $\mathbf{y}_k = \nabla f(\mathbf{x}_{k+1}) - \nabla f(\mathbf{x}_k)$。
5.  使用上述 BFGS 公式，将 $\mathbf{H}_k$ 更新为 $\mathbf{H}_{k+1}$。

#### Davidon–Fletcher–Powell (DFP) 算法

DFP 算法是历史上第一个成功的拟牛顿法，它同样可以从最小变动原则导出。

-   **DFP 对 $\mathbf{H}_k$ 的更新公式**  如下：
    $$ \mathbf{H}_{k+1} = \mathbf{H}_k + \frac{\mathbf{s}_k \mathbf{s}_k^T}{\mathbf{s}_k^T \mathbf{y}_k} - \frac{\mathbf{H}_k \mathbf{y}_k \mathbf{y}_k^T \mathbf{H}_k}{\mathbf{y}_k^T \mathbf{H}_k \mathbf{y}_k} $$

有趣的是，DFP 算法与 BFGS 算法存在一种“对偶”关系。DFP 对 $\mathbf{H}_k$ 的更新公式在形式上与 BFGS 对 $\mathbf{B}_k$ 的更新公式非常相似，反之亦然。

### 实际属性与性能

理论上的优美推导必须经受实践的检验。在实际应用中，一些关键属性决定了拟牛顿算法的稳定性和效率。

#### 曲率条件

在 BFGS 和 DFP 的更新公式中，分母上都出现了 $\mathbf{y}_k^T \mathbf{s}_k$ 这一项。为了使更新过程有意义且数值稳定，我们需要保证该项不为零。更进一步，为了保证算法的优良性质，我们需要满足**曲率条件**（curvature condition）：
$$ \mathbf{s}_k^T \mathbf{y}_k > 0 $$
这个条件有着至关重要的作用。对于 BFGS 算法，可以证明，如果初始近似 $\mathbf{H}_0$ 是对称正定的，并且在每次迭代中都满足曲率条件，那么后续所有的近似矩阵 $\mathbf{H}_k$ 都将保持[对称正定](@entry_id:145886)性。

保持 $\mathbf{H}_k$ 的正定性至关重要，因为它确保了搜索方向 $\mathbf{p}_k = -\mathbf{H}_k \nabla f(\mathbf{x}_k)$ 是一个**下降方向**，即 $\nabla f(\mathbf{x}_k)^T \mathbf{p}_k  0$（只要 $\nabla f(\mathbf{x}_k) \neq \mathbf{0}$）。这保证了只要步长 $\alpha_k$ 足够小，函数值就一定会下降，从而使得算法稳定地朝向极小点前进。

在实践中，曲率条件通常通过线搜索来保证。标准的[线搜索算法](@entry_id:139123)，如满足 Wolfe 条件的[线搜索](@entry_id:141607)，其设计目标之一就是找到一个能同时保证函数值充分下降和曲率条件成立的步长 $\alpha_k$。如果在线搜索过程中无法找到满足条件的步长，通常会选择跳过此次对 Hessian 近似矩阵的更新。

#### 性能比较与自校正特性

尽管 BFGS 和 DFP 都源于相似的理论基础，但它们在实际应用中的表现却有显著差异。大量的数值实验和理论分析表明，**BFGS 算法在综合性能上通常优于 DFP 算法** 。

BFGS 的优势主要体现在其鲁棒性上。它对[线搜索](@entry_id:141607)的精度不那么敏感。在实际计算中，我们几乎总是使用[非精确线搜索](@entry_id:637270)（inexact line search）。在这种情况下，BFGS 依然能够保持稳健，而 DFP 则可能因为[线搜索](@entry_id:141607)的不精确而导致 Hessian 近似矩阵丧失正定性，从而使得算法性能退化甚至失败。

这种鲁棒性与 BFGS 算法的**自校正特性**（self-correcting property）密切相关 。这意味着即使在某几步迭代中，Hessian 近似矩阵 $\mathbf{H}_k$ 变得不太准确（例如，与真实的逆 Hessian 矩阵相差甚远），BFGS 算法也有能力在后续的迭代中自动修正这种偏差，逐步生成更好的近似。例如，即便我们从一个非常粗糙的初始猜测 $\mathbf{H}_0 = \mathbf{I}$（[单位矩阵](@entry_id:156724)）开始，BFGS 也能迅速地从迭代信息中学习到函数真实的曲率结构。正是这种卓越的适应性和稳定性，使得 BFGS 成为当今[非线性优化](@entry_id:143978)领域中应用最广泛的算法之一。