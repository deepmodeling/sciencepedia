## 引言
在求解[非线性优化](@entry_id:143978)问题的广阔天地中，算法的选择往往是在[计算效率](@entry_id:270255)与收敛速度之间进行权衡。梯度下降法虽然简单，但收敛缓慢；牛顿法虽然收敛快，却需要计算和求逆代价高昂的Hessian矩阵。[拟牛顿法](@entry_id:138962)（Quasi-Newton Methods）正是在这两者之间找到了一个理想的[平衡点](@entry_id:272705)，成为现代优化领域最重要和最成功的算法之一。它巧妙地绕开了直接计算Hessian矩阵的难题，通过迭代更新一个近似矩阵，实现了超线性的收敛速度。

本文聚焦于拟牛顿法家族中两个里程碑式的成员：DFP（Davidon-Fletcher-Powell）和BFGS（Broyden-Fletcher-Goldfarb-Shanno）更新公式。我们将系统性地揭示这些强大算法背后的设计哲学与内在机制，解决“它们是如何在没有二阶信息的情况下有效模拟牛顿法”这一核心问题。

为实现这一目标，本文将分为三个部分。在“原理与机制”一章中，我们将从所有[拟牛顿法](@entry_id:138962)的基石——[割线条件](@entry_id:164914)出发，深入探讨DFP与BFGS公式的推导、它们的对偶关系，以及保证[算法稳定性](@entry_id:147637)的关键——曲率条件。接下来，在“应用与跨学科联系”一章，我们将走出理论，探索这些算法如何在机器学习、计算化学、[机器人学](@entry_id:150623)和[地球科学](@entry_id:749876)等前沿领域中发挥关键作用，并介绍其重要变体[L-BFGS](@entry_id:167263)如何应对大规模挑战。最后，“动手实践”部分将通过具体的计算练习，帮助您巩固理论知识，并深刻理解BFGS相比于DFP的实践优势。通过本次学习，您将全面掌握DFP与[BFGS方法](@entry_id:263685)的核心思想及其在解决现实世界问题中的强大威力。

## 原理与机制

在[非线性优化](@entry_id:143978)领域，拟牛顿法（Quasi-Newton methods）在求解效率和[数值稳定性](@entry_id:146550)之间取得了卓越的平衡，成为[无约束优化](@entry_id:137083)问题中最重要和最广泛使用的算法类别之一。与纯牛顿法需要计算和求逆[二阶导数](@entry_id:144508)（Hessian矩阵）不同，拟牛顿法通过迭代地构建并更新Hessian矩阵或其逆矩阵的近似来规避这一高昂的计算成本。本章将深入探讨两种最著名和最具影响力的拟牛顿更新公式——DFP（Davidon-Fletcher-Powell）和BFGS（Broyden-Fletcher-Goldfarb-Shanno）——背后的核心原理与关键机制。

我们将从所有[拟牛顿法](@entry_id:138962)的基础——[割线条件](@entry_id:164914)（secant condition）出发，揭示其如何捕捉函数曲率信息。随后，我们将探讨如何通过“最小变动原则”从不确定的[割线条件](@entry_id:164914)中导出唯一的更新公式。在此基础上，我们将详细介绍DFP和BFGS公式的结构、它们的对偶关系，以及将它们统一起来的Broyden族。最后，我们将重点分析保证[算法稳定性](@entry_id:147637)和高效收敛的关键——曲率条件，并讨论在实践中确保[算法稳健性](@entry_id:635315)的各种技术。

### [割线条件](@entry_id:164914)：拟牛顿法的基石

拟牛顿法的核心思想是，利用最近一步的迭代信息来改进对Hessian矩阵的近似。假设我们正致力于最小化一个[多元函数](@entry_id:145643) $f(\mathbf{x})$。在第 $k$ 次迭代中，我们从点 $\mathbf{x}_k$ 移动到点 $\mathbf{x}_{k+1}$。我们定义两个关键向量：

- **步长向量 (step vector)**: $\mathbf{s}_k = \mathbf{x}_{k+1} - \mathbf{x}_k$
- **梯度差向量 (gradient difference vector)**: $\mathbf{y}_k = \nabla f(\mathbf{x}_{k+1}) - \nabla f(\mathbf{x}_k)$

为了理解这些向量如何提供曲率信息，我们可以回顾向量函数的泰勒展开。梯度函数 $\nabla f(\mathbf{x})$ 在 $\mathbf{x}_k$ 附近的一阶展开近似为：
$$ \nabla f(\mathbf{x}) \approx \nabla f(\mathbf{x}_k) + \nabla^2 f(\mathbf{x}_k) (\mathbf{x} - \mathbf{x}_k) $$
令 $\mathbf{x} = \mathbf{x}_{k+1}$，并用近似Hessian矩阵 $B_{k+1}$ 代替真实的Hessian矩阵 $\nabla^2 f(\mathbf{x}_k)$，我们得到：
$$ \nabla f(\mathbf{x}_{k+1}) \approx \nabla f(\mathbf{x}_k) + B_{k+1} (\mathbf{x}_{k+1} - \mathbf{x}_k) $$
整理后，即为：
$$ \mathbf{y}_k \approx B_{k+1} \mathbf{s}_k $$
拟牛顿法的核心要求就是将这个近似关系变为一个严格的等式，即要求新的Hessian近似矩阵 $B_{k+1}$ 必须精确满足：
$$ B_{k+1} \mathbf{s}_k = \mathbf{y}_k $$
这个方程被称为**[割线条件](@entry_id:164914)**或**[割线方程](@entry_id:164522)**。它的几何意义是，以 $B_{k+1}$ 构建的函数二次模型，其在 $\mathbf{s}_k$ 方向上的梯度变化与实际观测到的梯度变化完全一致。这确保了新的模型至少在最近的搜索方向上与真实函数行为保持了一阶一致性 。

这个条件也可以通过积分形式的[均值定理](@entry_id:141085)更严格地导出。根据微积分基本定理：
$$ \mathbf{y}_k = \nabla f(\mathbf{x}_{k+1}) - \nabla f(\mathbf{x}_k) = \int_0^1 \nabla^2 f(\mathbf{x}_k + \tau \mathbf{s}_k) \mathbf{s}_k \, d\tau = \left( \int_0^1 \nabla^2 f(\mathbf{x}_k + \tau \mathbf{s}_k) \, d\tau \right) \mathbf{s}_k $$
令路径平均Hessian矩阵为 $\bar{B}_k = \int_0^1 \nabla^2 f(\mathbf{x}_k + \tau \mathbf{s}_k) \, d\tau$，我们有精确关系 $\mathbf{y}_k = \bar{B}_k \mathbf{s}_k$。因此，[割线条件](@entry_id:164914) $B_{k+1}\mathbf{s}_k = \mathbf{y}_k$ 的本质是要求近似矩阵 $B_{k+1}$ 在 $\mathbf{s}_k$ 方向上的作用与路径平均的真实Hessian矩阵完全相同。值得注意的是，这仅仅约束了 $B_{k+1}$ 在一个方向上的行为。当变量维度 $n > 1$ 时，[割线方程](@entry_id:164522)是一个包含 $n$ 个标量方程的系统，而一个对称的 $B_{k+1}$ 矩阵有 $\frac{n(n+1)}{2}$ 个独立元素，因此这是一个[欠定系统](@entry_id:148701)，无法唯一确定 $B_{k+1}$ 。

在实际算法中，我们通常直接更新Hessian的[逆矩阵](@entry_id:140380) $H_k = B_k^{-1}$，因为这样可以避免[求解线性方程组](@entry_id:169069)来获得搜索方向 $\mathbf{p}_k = -H_k \nabla f(\mathbf{x}_k)$。通过左乘 $H_{k+1} = B_{k+1}^{-1}$，我们可以得到Hessian逆矩阵的[割线条件](@entry_id:164914) ：
$$ H_{k+1} \mathbf{y}_k = \mathbf{s}_k $$
这两种形式的[割线方程](@entry_id:164522)是等价的，并构成了所有拟牛顿更新公式的基础。

### 最小变动原则：铸造唯一的更新

为了从欠定的[割线方程](@entry_id:164522)中得到一个唯一的更新公式，我们需要引入额外的约束。一个非常自然且强大的思想是**最小变动原则**（least-change principle）。该原则指出，我们应该选择一个满足[割线条件](@entry_id:164914)的矩阵 $B_{k+1}$（或 $H_{k+1}$），使其与当前的近似矩阵 $B_k$（或 $H_k$）“尽可能地接近” 。

这个“接近”程度通常通过某种[矩阵范数](@entry_id:139520)来衡量。形式上，我们求解一个[约束优化](@entry_id:635027)问题：
$$ \min_{B} \| B - B_k \| \quad \text{subject to} \quad B \mathbf{s}_k = \mathbf{y}_k, \quad B = B^\top $$
对范数的不同选择，以及是更新 $B_k$ 还是更新其[逆矩阵](@entry_id:140380) $H_k$，将导致不同的拟牛顿更新公式。例如，DFP和BFGS更新都可以被看作是在特定的加权[Frobenius范数](@entry_id:143384)下，应用最小变动原则于 $H_k$ 或 $B_k$ 所得到的结果。由此产生的更新公式具有低秩（low-rank）修正的结构，通常是**秩-二（rank-two）**更新，因为它们是在原矩阵上加上两个秩-一矩阵 。这个原则提供了一个优雅的理论框架，用于生成唯一的、保留已有信息的、并吸收新信息的更新规则。

### DFP与BFGS更新公式：一枚硬币的两面

DFP和BFGS是遵循上述原理导出的两个最成功的拟牛顿更新公式。它们都满足[割线条件](@entry_id:164914)，保持Hessian近似的对称性，并且在特定条件下保持[正定性](@entry_id:149643)。

**DFP (Davidon-Fletcher-Powell) 更新**
DFP方法是历史上第一个成功的[拟牛顿法](@entry_id:138962)，它直接更新Hessian的[逆矩阵](@entry_id:140380) $H_k$。其更新公式为：
$$ H_{k+1}^{\text{DFP}} = H_k + \frac{\mathbf{s}_k \mathbf{s}_k^\top}{\mathbf{s}_k^\top \mathbf{y}_k} - \frac{H_k \mathbf{y}_k \mathbf{y}_k^\top H_k}{\mathbf{y}_k^\top H_k \mathbf{y}_k} $$
这是一个秩-二更新，因为它在 $H_k$ 的基础上加了两个秩-一矩阵 $\mathbf{s}_k \mathbf{s}_k^\top$ 和 $(H_k \mathbf{y}_k)(H_k \mathbf{y}_k)^\top$。

**BFGS (Broyden-Fletcher-Goldfarb-Shanno) 更新**
[BFGS方法](@entry_id:263685)通常被认为是目前最有效和最稳健的拟牛顿法。其[标准形式](@entry_id:153058)是更新Hessian矩阵 $B_k$：
$$ B_{k+1}^{\text{BFGS}} = B_k + \frac{\mathbf{y}_k \mathbf{y}_k^\top}{\mathbf{y}_k^\top \mathbf{s}_k} - \frac{B_k \mathbf{s}_k \mathbf{s}_k^\top B_k}{\mathbf{s}_k^\top B_k \mathbf{s}_k} $$
同样，这也是一个秩-二更新。

#### 对偶性：DFP与BFGS的深刻联系

仔细观察DFP和BFGS的更新公式，可以发现一种深刻的对称性，这被称为**对偶性**（duality）。BFGS对 $B_k$ 的更新公式，与DFP对 $H_k$ 的更新公式，在结构上是完全一样的，唯一的区别在于向量 $\mathbf{s}_k$ 和 $\mathbf{y}_k$ 的角色互换了 。

具体来说：
- [DFP更新](@entry_id:637803) $H_k$：$H_{k+1} = H_k + \text{Term}(\mathbf{s}_k, \mathbf{y}_k, H_k)$
- BFGS更新 $B_k$：$B_{k+1} = B_k + \text{Term}(\mathbf{y}_k, \mathbf{s}_k, B_k)$

这种对偶关系意味着，如果我们拥有一个更新 $H_k$ 的DFP公式，只需将 $H_k \leftrightarrow B_k$ 以及 $\mathbf{s}_k \leftrightarrow \mathbf{y}_k$ 进行互换，就能得到更新 $B_k$ 的BFGS公式。反之亦然。

这个对偶关系可以通过**Sherman-Morrison-Woodbury**矩阵求逆引理进行严格的数学证明。例如，对DFP的 $H_{k+1}$ 更新公式求逆，经过一系列代数运算，便可以得到BFGS的 $B_{k+1}$ 更新公式 。

基于对偶性，我们可以写出另外两种形式的更新公式：

- **逆BFGS更新 (Inverse BFGS)**，用于更新 $H_k$：
$$ H_{k+1}^{\text{BFGS}} = H_k + \left(1 + \frac{\mathbf{y}_k^\top H_k \mathbf{y}_k}{\mathbf{s}_k^\top \mathbf{y}_k}\right) \frac{\mathbf{s}_k \mathbf{s}_k^\top}{\mathbf{s}_k^\top \mathbf{y}_k} - \frac{\mathbf{s}_k \mathbf{y}_k^\top H_k + H_k \mathbf{y}_k \mathbf{s}_k^\top}{\mathbf{s}_k^\top \mathbf{y}_k} $$

- **直接[DFP更新](@entry_id:637803) (Direct DFP)**，用于更新 $B_k$：
$$ B_{k+1}^{\text{DFP}} = \left(I - \frac{\mathbf{y}_k \mathbf{s}_k^\top}{\mathbf{y}_k^\top \mathbf{s}_k}\right) B_k \left(I - \frac{\mathbf{s}_k \mathbf{y}_k^\top}{\mathbf{y}_k^\top \mathbf{s}_k}\right) + \frac{\mathbf{y}_k \mathbf{y}_k^\top}{\mathbf{y}_k^\top \mathbf{s}_k} $$

尽管DFP和BFGS在结构上如此紧密地联系在一起，但它们在数值性能上却有显著差异。对于相同的输入 $\mathbf{s}_k$ 和 $\mathbf{y}_k$，它们生成的矩阵是不同的 。

#### Broyden族：统一的视角

DFP与BFGS之间的对偶关系还可以通过**Broyden族**（Broyden Family）更新公式得到更统一的阐述。Broyden族是一个由参数 $\phi$ 控制的连续更新公式集合：
$$ B_{k+1}^\phi = (1-\phi) B_{k+1}^{\text{BFGS}} + \phi B_{k+1}^{\text{DFP}} $$
其中 $B_{k+1}^{\text{BFGS}}$ 和 $B_{k+1}^{\text{DFP}}$ 分别是通过BFGS和DFP规则更新得到的Hessian近似。这个族中的所有更新公式都满足[割线条件](@entry_id:164914)并保持对称性。

特别地：
- 当 $\phi=0$ 时，我们得到BFGS更新。
- 当 $\phi=1$ 时，我们得到[DFP更新](@entry_id:637803)。

Broyden族的存在表明，BFGS和DFP并非孤立的方法，而是处于一个包含无数可能性的更新谱系的两端 。

### 曲率条件：确保稳定与收敛的关键

为了使拟牛顿法有效，Hessian（或其逆）的近似矩阵 $B_k$（或 $H_k$）必须保持**正定性**（positive definite）。一个正定的 $B_k$ 保证了 $-B_k^{-1} \nabla f(\mathbf{x}_k)$ 是一个下降方向，从而保证算法能够向着函数值减小的方向前进。

DFP和BFGS更新公式能否保持正定性的关键，在于一个简单的标量条件——**曲率条件**（curvature condition）：
$$ \mathbf{s}_k^\top \mathbf{y}_k > 0 $$
这个条件的几何意义是，在步长方向 $\mathbf{s}_k$ 上，梯度的变化 $\mathbf{y}_k$ 与步长本身形成一个锐角。这意味着函数在该方向上的曲率是正的，这与我们正在接近一个（局部）[最小值点](@entry_id:634980)的期望是一致的。

可以证明，如果当前的近似 $B_k$（或 $H_k$）是正定的，那么新的近似 $B_{k+1}$（或 $H_{k+1}$）保持正定的充分必要条件就是满足曲率条件 $\mathbf{s}_k^\top \mathbf{y}_k > 0$ 。

那么，如何确保这个条件在每次迭代中都成立呢？这正是**线搜索**（line search）算法发挥作用的地方。在计算出搜索方向 $\mathbf{p}_k$ 后，我们并不总是取完整的[牛顿步](@entry_id:177069)，而是求解一个[一维优化](@entry_id:635076)问题来寻找[最优步长](@entry_id:143372) $\alpha_k$，即 $\mathbf{x}_{k+1} = \mathbf{x}_k + \alpha_k \mathbf{p}_k$。**[Wolfe条件](@entry_id:171378)**是一组广泛使用的[非精确线搜索](@entry_id:637270)准则，它不仅能保证函数值有足够的下降，其第二条准则（曲率条件）直接要求：
$$ \nabla f(\mathbf{x}_k + \alpha_k \mathbf{p}_k)^\top \mathbf{p}_k \ge c_2 \nabla f(\mathbf{x}_k)^\top \mathbf{p}_k \quad (0  c_1  c_2  1) $$
这个不等式经过简单的代数变换后，可以直接导出 $\mathbf{s}_k^\top \mathbf{y}_k  0$。因此，一个设计良好的[线搜索算法](@entry_id:139123)与拟牛顿更新公式是协同工作的：[线搜索](@entry_id:141607)保证了曲率条件的满足，而曲率条件又保证了拟牛顿更新的正定性，从而保证了整个算法的稳定下降。这种协同作用是现代优化软件成功的关键 。

更重要的是，满足[Wolfe条件](@entry_id:171378)的[非精确线搜索](@entry_id:637270)足以保证在相当宽松的条件下（如函数有下界、梯度Lipschitz连续），算法[全局收敛](@entry_id:635436)到[稳定点](@entry_id:136617)（即梯度为零的点）。而且，对于[BFGS方法](@entry_id:263685)，与Wolfe线搜索结合可以被证明具有**[超线性收敛](@entry_id:141654)**（superlinear convergence）速率，这意味着它不需要进行昂贵的[精确线搜索](@entry_id:170557)就能实现快速的局部收敛 。

### 实践性能与稳健性改进

尽管DFP和BFGS在理论上如此相似，但在实践中，它们的表现却有云泥之别。

#### BFGS的优越性

大量的数值实验和理论分析表明，**BFGS通常显著优于DFP**。BFGS被认为具有更好的“自我修正”能力。如果某一步的Hessian近似不佳，BFGS更有可能在后续迭代中进行修正。相比之下，DFP对[非精确线搜索](@entry_id:637270)的容忍度较低，更容易产生数值不稳定或[条件数](@entry_id:145150)很差的Hessian近似，导致收敛缓慢甚至失败。因此，在现代优化实践中，BFGS是默认的、也是首选的拟牛顿方法 。

#### 应对曲率条件失效

在处理非凸问题时，即使使用[线搜索](@entry_id:141607)，也可能遇到无法满足曲率条件 $\mathbf{s}_k^\top \mathbf{y}_k  0$ 的情况。例如，考虑非[凸函数](@entry_id:143075) $f(x_1, x_2) = x_1^2 - x_2^2$，其Hessian矩阵 $\begin{pmatrix} 2  0 \\ 0  -2 \end{pmatrix}$ 不是正定的。如果我们沿方向 $\mathbf{s}_k = (0, 1)^\top$ 移动，就会发现 $\mathbf{s}_k^\top \mathbf{y}_k = -2  0$。在这种情况下，直接应用BFGS或[DFP更新公式](@entry_id:170404)会导致新的Hessian近似失去正定性，算法可能会崩溃 。

为了处理这种情况，实践中通常采用两种策略：
1.  **跳过更新**：如果 $\mathbf{s}_k^\top \mathbf{y}_k$ 不满足某个正阈值，则简单地放弃本次更新，令 $B_{k+1} = B_k$。
2.  **阻尼策略 (Damping)**：对向量 $\mathbf{y}_k$ 进行修正，以强制满足曲率条件。一种常用的方法（由Powell提出）是，用一个[凸组合](@entry_id:635830) $\bar{\mathbf{y}}_k = \theta \mathbf{y}_k + (1-\theta) B_k \mathbf{s}_k$ 来代替 $\mathbf{y}_k$，其中 $\theta \in [0,1]$ 的选择要确保 $\mathbf{s}_k^\top \bar{\mathbf{y}}_k  0$。这种方法通过将观测到的梯度变化与当前模型预测的梯度变化进行混合，有效地“阻尼”了[负曲率](@entry_id:159335)的影响，从而恢复了更新的稳定性 。

#### DFP的内在数值问题

DFP还有一个更微妙的数值缺陷，这进一步解释了为何它不如BFGS受欢迎。在[DFP更新公式](@entry_id:170404)中，存在一个分母项 $\mathbf{y}_k^\top H_k \mathbf{y}_k$。尽管理论上只要 $H_k$ 是正定的，这一项就恒为正，但在有限精度计算中，如果 $H_k$ 的[条件数](@entry_id:145150)很大（即病态的），那么对于某些特定的 $\mathbf{y}_k$，这个分母项可能会变得非常小，导致计算结果溢出或产生巨大的[舍入误差](@entry_id:162651)。这个问题可以通过分析 $\mathbf{y}_k$ 与 $H_k \mathbf{y}_k$ 之间的夹角来理解。当 $H_k$ 病态时，这个夹角可能非常接近 $90^\circ$，从而使得[内积](@entry_id:158127) $\mathbf{y}_k^\top H_k \mathbf{y}_k$ 相对于向量的模长来说极小。通过变量变换（预处理）等技术可以缓解这个问题，但它暴露了DFP公式在数值上的内在脆弱性 。BFGS的更新公式则没有这个特定的问题，这也是其数值稳健性更强的原因之一。

综上所述，DFP和[BFGS方法](@entry_id:263685)虽然源于相同的基本原理——[割线条件](@entry_id:164914)和最小变动原则，并且通过对偶性紧密相连，但它们在[数值稳定性](@entry_id:146550)和实际效率上存在显著差异。[BFGS方法](@entry_id:263685)，特别是与满足[Wolfe条件](@entry_id:171378)的线搜索相结合，提供了一个强大、高效且稳健的框架，构成了现代连续优化领域不可或缺的基石。