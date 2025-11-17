## 引言
[凸优化](@entry_id:137441)已成为现代信号处理与数据科学领域不可或缺的基石。它提供了一个强大而统一的理论框架，能够为从通信、成像到机器学习的众多应用中的复杂问题找到具有全局最优性保证的解。其重要性在于，它将大量看似无关的问题归结为少数几类可被高效求解的标准形式，从而彻底改变了信号处理领域的设计[范式](@entry_id:161181)和研究方法。

然而，许多现实世界中的信号处理任务，如从不完整或带噪数据中恢复信号、设计满足严格规范的系统，本质上都是非凸或[组合性](@entry_id:637804)的难题，传统方法往往难以应对或只能提供次优解。本文旨在弥补这一差距，系统性地阐述如何利用[凸优化](@entry_id:137441)的语言来重新表述这些难题，并通过引入结构先验（如[稀疏性](@entry_id:136793)或低秩性）将其转化为易于处理的凸问题，从而获得在理论和实践上都表现优异的解决方案。

为了帮助读者全面掌握这一强大工具，本文将分三步展开。第一章“原理与机制”将首先构建理论基础，介绍凸集、凸函数、对偶性等核心概念，以及处理[优化问题](@entry_id:266749)的分析工具。随后，第二章“应用与跨学科联系”将展示这些理论如何在滤波器设计、[稀疏恢复](@entry_id:199430)、[矩阵补全](@entry_id:172040)以及鲁棒[波束成形](@entry_id:184166)等多样化应用中发挥作用。最后，“动手实践”部分将通过具体的编程练习，将理论知识转化为解决实际问题的能力。现在，让我们从构建[凸优化](@entry_id:137441)的基本语言开始，深入第一章的核心原理。

## 原理与机制

本章深入探讨[凸优化](@entry_id:137441)在信号处理领域应用的核心原理与机制。我们将从[凸集](@entry_id:155617)与凸函数的基本定义出发，逐步介绍分析和求解[优化问题](@entry_id:266749)的关键工具，如梯度、次梯度与对偶性。随后，我们将阐述如何将典型的信号处理问题构建为标准的[凸优化](@entry_id:137441)[范式](@entry_id:161181)，例如[二阶锥规划](@entry_id:165523)（SOCP）和[半定规划](@entry_id:268613)（SDP）。最后，我们将介绍解决这些问题的核心算法原理，并简要讨论这些方法在何种条件下能够保证成功恢复信号的理论依据。

### 凸性的语言：集合、函数与锥

[凸优化](@entry_id:137441)研究的核心是在**[凸集](@entry_id:155617)**上最小化**凸函数**。这些概念不仅是数学上的抽象，更在信号处理问题的建模中扮演着至关重要的角色。

#### [凸集](@entry_id:155617)、[仿射集](@entry_id:634284)与锥

一个集合 $\mathcal{S} \subseteq \mathbb{R}^n$ 被称为**[凸集](@entry_id:155617)**，如果连接集合中任意两点的线段完全包含在集合内。形式上，对于任意 $\mathbf{x}, \mathbf{y} \in \mathcal{S}$ 和任意 $\theta \in [0,1]$，点 $\theta \mathbf{x} + (1-\theta)\mathbf{y}$ 也必须属于 $\mathcal{S}$。

一个更具限制性的概念是**[仿射集](@entry_id:634284)**。一个集合 $\mathcal{A} \subseteq \mathbb{R}^n$ 是仿射的，如果穿过其任意两点的直线都完全位于集合内。这意味着对于任意 $\mathbf{x}, \mathbf{y} \in \mathcal{A}$ 和任意 $t \in \mathbb{R}$，点 $\mathbf{x} + t(\mathbf{y}-\mathbf{x})$ 也在 $\mathcal{A}$ 中。所有[仿射集](@entry_id:634284)都是[凸集](@entry_id:155617)，并且可以被刻画为一个[线性方程组的解集](@entry_id:150776)，形如 $\{\mathbf{x} \mid \mathbf{A}\mathbf{x} = \mathbf{b}\}$。

另一类重要的凸集是**锥**。一个集合 $\mathcal{C} \subseteq \mathbb{R}^n$ 是锥，如果对于任意 $\mathbf{x} \in \mathcal{C}$ 和任意非负标量 $\tau \ge 0$，点 $\tau \mathbf{x}$ 也在 $\mathcal{C}$ 中。这意味着从原点出发穿过集合中任一点的射线都包含在集合内。如果一个锥同时也是[凸集](@entry_id:155617)，则称之为**[凸锥](@entry_id:635652)**。

为了将这些抽象概念具体化，我们可以考虑一个在信号处理中无处不在的例子：[有限脉冲响应](@entry_id:192542)（FIR）滤波器的设计 [@problem_id:2861527]。一个长度为 $n$ 的[FIR滤波器](@entry_id:262292)的系数向量为 $\mathbf{h} \in \mathbb{R}^n$。对于一个固定的输入序列，其输出是 $\mathbf{h}$ 的线性函数。因此，对输出施加的线性的等式或[不等式约束](@entry_id:176084)，会转化为对 $\mathbf{h}$ 的线性约束，从而定义了 $\mathbf{h}$ 的可行集。

-   **[凸集](@entry_id:155617)示例**：假设我们要求滤波器在某些时刻 $k$ 的输出值被限制在某个区间 $[L_k, U_k]$ 内。由于输出是 $\mathbf{h}$ 的[仿射函数](@entry_id:635019)，这个约束可以写成 $\mathbf{a}_k^\top \mathbf{h} \le U_k'$ 和 $-\mathbf{a}_k^\top \mathbf{h} \le -L_k'$ 的形式。这样的[线性不等式](@entry_id:174297)定义了一个半空间，而多个此类约束的交集（即一个[多面体](@entry_id:637910)）总是一个[凸集](@entry_id:155617)。

-   **[仿射集](@entry_id:634284)示例**：考虑设计一个具有单位[直流增益](@entry_id:267449)（$\sum h[i] = 1$）且具有线性相位（通过对称性 $h[i] = h[n-1-i]$ 实现）的滤波器。这些约束都是 $\mathbf{h}$ 的线性等式，例如 $\mathbf{1}^\top \mathbf{h} = 1$ 和 $h[i] - h[n-1-i] = 0$。因此，所有满足这些条件的滤波器系数 $\mathbf{h}$ 构成的集合是一个[仿射集](@entry_id:634284)。

-   **[凸锥](@entry_id:635652)示例**：如果我们施加的约束是齐次的（即等式或不等式的右侧为零），那么可行集就构成一个[凸锥](@entry_id:635652)。例如，考虑约束滤波器系数的部分和非负（$\sum_{i=0}^{k} h[i] \ge 0$）且[直流增益](@entry_id:267449)为零（$\sum_{i=0}^{n-1} h[i] = 0$）。对于任何满足这些约束的 $\mathbf{h}$，用一个非负标量 $\tau \ge 0$ 去缩放它，得到的新向量 $\tau\mathbf{h}$ 显然也满足这些齐次约束。因此，该可行集是一个[凸锥](@entry_id:635652) [@problem_id:2861527]。

#### [凸函数](@entry_id:143075)

一个函数 $f: \mathbb{R}^n \to \mathbb{R}$ 被称为**[凸函数](@entry_id:143075)**，如果其定义域为[凸集](@entry_id:155617)，并且对于其定义域中的任意两点 $\mathbf{x}, \mathbf{y}$ 和任意 $\theta \in [0,1]$，满足琴生（Jensen）不等式：
$$ f(\theta \mathbf{x} + (1-\theta)\mathbf{y}) \le \theta f(\mathbf{x}) + (1-\theta)f(\mathbf{y}) $$
几何上，这意味着[连接函数](@entry_id:636388)图像上任意两点的弦总是在这两点之间的函数图像上方。

信号处理中最常见的[目标函数](@entry_id:267263)之一是**最小二乘**目标函数，用于衡量模型预测与观测数据之间的拟合程度。该函数形式为 $f(\mathbf{x}) = \frac{1}{2}\|\mathbf{A}\mathbf{x} - \mathbf{b}\|_2^2$，其中 $\mathbf{x}$ 是待估计的信号，$\mathbf{A}$ 是[系统矩阵](@entry_id:172230)，$\mathbf{b}$ 是观测向量。我们可以通过考察其[二阶导数](@entry_id:144508)（Hessian矩阵）来证明其凸性。从一阶导数（梯度） $\nabla f(\mathbf{x}) = \mathbf{A}^\top(\mathbf{A}\mathbf{x} - \mathbf{b})$ 出发，我们计算Hessian矩阵得到 $\nabla^2 f(\mathbf{x}) = \mathbf{A}^\top\mathbf{A}$ [@problem_id:2861528]。对于任意向量 $\mathbf{z} \in \mathbb{R}^n$，二次型 $\mathbf{z}^\top (\mathbf{A}^\top\mathbf{A}) \mathbf{z} = \|\mathbf{A}\mathbf{z}\|_2^2 \ge 0$。由于其Hessian矩阵是半正定的，该最小二乘函数是凸函数。

### 优化的分析工具

为了分析并求解凸[优化问题](@entry_id:266749)，我们需要一套数学工具来处理光滑和非光滑的凸函数，并理解问题的内在结构。

#### [光滑性](@entry_id:634843)与梯度[利普希茨连续性](@entry_id:142246)

对于像最小二乘这样可微的凸函数，梯度 $\nabla f(\mathbf{x})$ 提供了函数在点 $\mathbf{x}$ 处最陡峭的上升方向。许多优化算法（如梯度下降法）都依赖于梯度信息。这些算法的[收敛性分析](@entry_id:151547)通常要求梯度不能变化得太快。这个性质被**梯度[利普希茨连续性](@entry_id:142246)**（或称 $L$-光滑性）所刻画。

如果存在一个常数 $L > 0$，使得对于任意 $\mathbf{x}, \mathbf{y}$，不等式 $\|\nabla f(\mathbf{x}) - \nabla f(\mathbf{y})\|_2 \le L \|\mathbf{x} - \mathbf{y}\|_2$ 成立，我们就说函数 $f$ 是 $L$-光滑的。最小的这样的 $L$ 被称为[利普希茨常数](@entry_id:146583)。

对于最小二乘目标 $f(\mathbf{x}) = \frac{1}{2}\|\mathbf{A}\mathbf{x} - \mathbf{b}\|_2^2$，我们有 $\nabla f(\mathbf{x}) - \nabla f(\mathbf{y}) = \mathbf{A}^\top\mathbf{A}(\mathbf{x}-\mathbf{y})$。因此，$\|\nabla f(\mathbf{x}) - \nabla f(\mathbf{y})\|_2 \le \|\mathbf{A}^\top\mathbf{A}\|_2 \|\mathbf{x}-\mathbf{y}\|_2$，其中 $\|\cdot\|_2$ 表示矩阵的[算子范数](@entry_id:752960)（[谱范数](@entry_id:143091)）。[利普希茨常数](@entry_id:146583) $L$ 就是矩阵 $\mathbf{A}^\top\mathbf{A}$ 的最大[特征值](@entry_id:154894)，即其[谱半径](@entry_id:138984) $\rho(\mathbf{A}^\top\mathbf{A})$ [@problem_id:2861528]。

这个常数 $L$ 具有重要的物理意义。例如，如果 $\mathbf{A}$ 代表一个[循环卷积](@entry_id:147898)操作，其矩阵是一个[循环矩阵](@entry_id:143620)，那么 $\mathbf{A}$ 可以被离散傅里叶变换（DFT）对角化。其[特征值](@entry_id:154894)是该滤波器的离散频率响应 $H[k]$。在这种情况下，$L$ 就等于频率响应幅度的最大值的平方，即 $L = \max_k |H[k]|^2$。这个值直接关系到系统对某些频率分量的最大能量增益，从而决定了目标函数表面的最大曲率。

#### 非光滑性与次梯度

许多在现代信号处理中至关重要的函数，如用于促进稀疏性的 $\ell_1$-范数 $\|x\|_1 = \sum_i |x_i|$，都不是处处可微的（例如，在任何分量为零的点）。对于这[类函数](@entry_id:146970)，梯度的概念被**次梯度**（subgradient）所推广。

对于一个凸函数 $f$，在点 $\mathbf{x}$ 的一个次梯度是一个向量 $\mathbf{g}$，它定义的[仿射函数](@entry_id:635019) $f(\mathbf{x}) + \mathbf{g}^\top(\mathbf{y}-\mathbf{x})$ 是 $f$ 的一个全局下估计。也就是说，对于所有的 $\mathbf{y}$，都满足：
$$ f(\mathbf{y}) \ge f(\mathbf{x}) + \mathbf{g}^\top(\mathbf{y}-\mathbf{x}) $$
在点 $\mathbf{x}$ 处所有[次梯度](@entry_id:142710)的集合被称为 $f$ 在该点的**[次微分](@entry_id:175641)**（subdifferential），记作 $\partial f(\mathbf{x})$。如果 $f$ 在 $\mathbf{x}$ 处可微，那么其[次微分](@entry_id:175641)只包含一个元素，即梯度 $\nabla f(\mathbf{x})$。

$\ell_1$-范数是一个典型的例子 [@problem_id:2861543]。由于其可分离性，即 $\|x\|_1 = \sum_i |x_i|$，其在 $x$ 处的[次微分](@entry_id:175641)是各个分量函数 $|x_i|$ 在 $x_i$ 处[次微分](@entry_id:175641)的笛卡尔积。对于标量[绝对值函数](@entry_id:160606) $|t|$：
-   如果 $t \neq 0$，函数是可微的，其导数为 $\operatorname{sgn}(t)$（$t>0$ 时为 1，$t0$ 时为 -1）。因此，$\partial|t| = \{\operatorname{sgn}(t)\}$。
-   如果 $t=0$，函数在原点处不可微。根据定义，我们需要找到所有满足 $|y| \ge gy$ 的 $g$。这要求 $g$ 必须在 $[-1, 1]$ 区间内。因此，$\partial|0| = [-1, 1]$。

综合起来，向量 $\mathbf{g}$ 是 $\ell_1$-范数在点 $\mathbf{x}$ 处的次梯度的充要条件是其分量 $g_i$ 满足：
$$
g_i = \begin{cases}
\operatorname{sgn}(x_i)  \text{若 } x_i \neq 0 \\
\in [-1, 1]  \text{若 } x_i = 0
\end{cases}
$$
这个结果是推导[稀疏恢复](@entry_id:199430)问题（如[LASSO](@entry_id:751223)和[基追踪](@entry_id:200728)）[最优性条件](@entry_id:634091)的基础。

#### 对偶性

对偶性是[凸优化](@entry_id:137441)中的一个核心概念，它通过一个[对偶问题](@entry_id:177454)为原问题（primal problem）提供了一个不同的视角和深刻的见解。

##### 范数的对偶

每个范数 $\|\cdot\|$ 都有一个与之关联的**[对偶范数](@entry_id:200340)** $\|\cdot\|_*$，定义为：
$$ \|z\|_* \triangleq \sup_{\|x\| \le 1} z^\top x $$
这个定义在分析和优化中反复出现。一个基本且重要的对偶关系存在于 $\ell_1$-范数和 $\ell_\infty$-范数之间 [@problem_id:2861506]。
通过基本的不等式（如[Hölder不等式](@entry_id:140161)或直接推导），可以证明：
1.  **$\ell_1$-范数的对偶是 $\ell_\infty$-范数**：$\sup_{\|x\|_1 \le 1} z^\top x = \|z\|_\infty$。证明思路是，首先通过 $z^\top x = \sum z_i x_i \le \sum |z_i||x_i| \le \|z\|_\infty \sum |x_i| = \|z\|_\infty \|x\|_1 \le \|z\|_\infty$ 建立上界。然后，通过构造一个特定的 $x$（在 $z$ 的最大[绝对值](@entry_id:147688)分量对应的位置取值为 $\pm 1$，其余为 0），可以证明这个[上界](@entry_id:274738)是可以达到的。

2.  **$\ell_\infty$-范数的对偶是 $\ell_1$-范数**：$\sup_{\|x\|_\infty \le 1} z^\top x = \|z\|_1$。证明思路类似，[上界](@entry_id:274738)由 $z^\top x = \sum z_i x_i \le \sum |z_i||x_i| \le \sum |z_i| \cdot 1 = \|z\|_1$ 给出。然后，通过构造 $x_i = \operatorname{sgn}(z_i)$ 来证明此上界可达。

这些对偶关系在推导[稀疏优化](@entry_id:166698)问题的对偶问题时至关重要。

##### [拉格朗日对偶](@entry_id:638042)

对于一个带约束的[优化问题](@entry_id:266749)，我们可以构造其**[拉格朗日对偶问题](@entry_id:637210)**。考虑一个典型的[稀疏恢复](@entry_id:199430)问题，称为**[基追踪](@entry_id:200728)**（Basis Pursuit）[@problem_id:2861540]：
$$ \min_{x \in \mathbb{R}^{n}} \|x\|_1 \quad \text{s.t.} \quad \mathbf{A}x = \mathbf{b} $$
我们引入[拉格朗日乘子](@entry_id:142696)（[对偶变量](@entry_id:143282)）$y \in \mathbb{R}^m$ 来构造拉格朗日函数：
$$ L(x, y) = \|x\|_1 + y^\top(\mathbf{A}x - \mathbf{b}) $$
对[偶函数](@entry_id:163605) $g(y)$ 是 $L(x,y)$ 关于 $x$ 的[下确界](@entry_id:140118)：
$$ g(y) = \inf_x L(x, y) = -y^\top\mathbf{b} + \inf_x (\|x\|_1 + (\mathbf{A}^\top y)^\top x) $$
利用 Fenchel 共轭的定义 $f^*(u) = \sup_z (u^\top z - f(z))$，我们发现 $\inf_x (f(x) + s^\top x) = -\sup_x (-s^\top x - f(x)) = -f^*(-s)$。这里 $f(x) = \|x\|_1$，$s = \mathbf{A}^\top y$。$\ell_1$-范数的共轭函数是 $\ell_\infty$-范数单位球的[指示函数](@entry_id:186820)。因此，当且仅当 $\|-\mathbf{A}^\top y\|_\infty \le 1$（等价于 $\|\mathbf{A}^\top y\|_\infty \le 1$）时，[下确界](@entry_id:140118)为 0，否则为 $-\infty$。

因此，对偶问题是最大化 $g(y)$，即：
$$ \max_{y \in \mathbb{R}^{m}} - \mathbf{b}^\top y \quad \text{s.t.} \quad \|\mathbf{A}^\top y\|_\infty \le 1 $$
**[弱对偶](@entry_id:163073)性**原理指出，任何对偶可行解的目标值都是原问题最优值的一个下界。如果能找到一个原问题的[可行解](@entry_id:634783) $\hat{x}$ 和一个[对偶问题](@entry_id:177454)的可行解 $\hat{y}$，使得它们的目标值相等，即 $\| \hat{x} \|_1 = -\mathbf{b}^\top \hat{y}$（零[对偶间隙](@entry_id:173383)），那么 $\hat{x}$ 就被证明是原问题的最优解。这样的 $\hat{y}$ 被称为最优性的**对偶证书**。

### 典型问题[范式](@entry_id:161181)

许多信号处理问题可以通过巧妙的建模，转化为少数几个标准的凸[优化问题](@entry_id:266749)类别，从而可以利用现成的、高效的求解器来解决。

#### [二阶锥规划](@entry_id:165523)（SOCP）

**[二阶锥规划](@entry_id:165523)**（SOCP）问题是最小化一个线性函数，其约束条件要求某些[仿射组合](@entry_id:276726)的变量属于一个或多个**[二阶锥](@entry_id:637114)**（也称[洛伦兹锥](@entry_id:637114)）。$k$ 维标准[二阶锥](@entry_id:637114) $\mathcal{Q}^k$ 定义为：
$$ \mathcal{Q}^k = \left\{ u = \begin{pmatrix} u_0 \\ \bar{u} \end{pmatrix} \in \mathbb{R}^k \mid u_0 \in \mathbb{R}, \bar{u} \in \mathbb{R}^{k-1}, \|\bar{u}\|_2 \le u_0 \right\} $$
一个常见的约束形式是[欧几里得范数](@entry_id:172687)不等式，例如在[信号去噪](@entry_id:275354)问题中，我们可能希望残差的范数有界：$\|\mathbf{A}x - \mathbf{b}\|_2 \le t$ [@problem_id:2861507]。这个约束可以通过引入辅助变量 $t$ 并将其置于[二阶锥](@entry_id:637114)的“标量”部分来表示。具体地，该约束等价于向量 $\begin{pmatrix} t \\ \mathbf{A}x - \mathbf{b} \end{pmatrix}$ 属于一个 $m+1$ 维的[二阶锥](@entry_id:637114) $\mathcal{Q}^{m+1}$。因此，一个旨在最小化[残差范数](@entry_id:754273)的问题，如 $\min t$ s.t. $\|\mathbf{A}x - \mathbf{b}\|_2 \le t$，就是一个 SOCP 问题。这种通过引入辅助变量将非线性约束转化为锥约束的技巧被称为**epigraph 形式**。

#### [半定规划](@entry_id:268613)（SDP）

**[半定规划](@entry_id:268613)**（SDP）是更为广泛的一类问题，它在**半正定锥**（所有[对称半正定矩阵](@entry_id:163376)的集合）上最小化线性函数，并附加线性等式或[不等式约束](@entry_id:176084)。SDP 在控制理论、组合优化以及信号处理中有诸多应用。

一个引人注目的例子是**相位恢复**（phase retrieval），其目标是从一系列二次幅值测量 $b_i = |a_i^\top x|^2$ 中恢复未知信号 $x \in \mathbb{R}^n$ [@problem_id:2861512]。这是一个非凸的二次方程组问题。通过一个称为**提升**（lifting）的技巧，我们可以将其松弛为一个凸的 SDP。

这个技巧的核心是，我们将变量从向量 $x$ 提升到一个矩阵 $X = xx^\top$。这个矩阵 $X$ 天然具有两个性质：它是半正定的 ($X \succeq 0$) 并且是秩为 1 的。测量方程可以重写为 $X$ 的线性函数：
$$ b_i = (a_i^\top x)^2 = x^\top (a_i a_i^\top) x = \operatorname{trace}((a_i a_i^\top)(xx^\top)) = \operatorname{trace}((a_i a_i^\top)X) $$
原始问题等价于寻找一个秩为 1 的[半正定矩阵](@entry_id:155134) $X$ 满足这些线性约束。秩约束是非凸的，难以处理。[PhaseLift](@entry_id:753386) 方法通过丢弃这个非凸的秩约束，将其松弛为一个纯粹的凸问题：寻找一个[半正定矩阵](@entry_id:155134) $X$ 满足上述[线性约束](@entry_id:636966)。

为了引导解趋向于低秩，我们添加一个目标函数。对于[半正定矩阵](@entry_id:155134)，其**[核范数](@entry_id:195543)**（奇异值之和，是秩函数的最佳凸代理）恰好等于其**迹**（trace）。因此，我们通过最小化 $\operatorname{trace}(X)$ 来间接最小化秩。最终的 [PhaseLift](@entry_id:753386) [优化问题](@entry_id:266749)是一个 SDP：
$$ \min_{X \succeq 0} \operatorname{trace}(X) \quad \text{s.t.} \quad \operatorname{trace}(a_i a_i^\top X) = b_i, \quad \forall i $$
如果这个 SDP 的解 $X^*$ 恰好是秩为 1 的，我们就可以通过[特征分解](@entry_id:181333) $X^* = x^*(x^*)^\top$ 成功恢复出原始信号 $x$（相差一个全局符号）。这个方法可以自然地推广到复数域，只需将 $X=xx^\top$ 替换为 $X=xx^*$（其中 $x^*$ 是[共轭转置](@entry_id:147909)）。

#### [原子范数](@entry_id:746563)最小化

在许多[稀疏恢复](@entry_id:199430)问题中，我们假设信号可以由一个字典中的少数几个“原子”线性组合而成。传统的 [LASSO](@entry_id:751223) 或[基追踪](@entry_id:200728)方法使用一个离散的、预先固定的字典。例如，在[谱估计](@entry_id:262779)中，我们可以用一个覆盖频率轴的精细网格上的傅里叶原子来构建字典。然而，这种方法存在一个固有的缺陷，称为**基不匹配**（basis mismatch）[@problem_id:2861533]。如果真实信号的频率分量恰好落在网格点之间，离散模型就无法精确表示它，导致恢复的[频谱](@entry_id:265125)出现展宽和伪峰。

**[原子范数](@entry_id:746563)**（atomic norm）方法通过使用一个连续的、无限的原[子集](@entry_id:261956) $\mathcal{A}$ 来从根本上解决这个问题。对于一个给定的原[子集](@entry_id:261956) $\mathcal{A}$（例如，所有[归一化频率](@entry_id:171939)对应的傅里叶向量的集合），一个信号 $x$ 的[原子范数](@entry_id:746563)被定义为其最稀疏的原子分解的 $\ell_1$ 范数：
$$ \|x\|_{\mathcal{A}} = \inf \left\{ \sum_k |c_k| \mid x = \sum_k c_k a_k, a_k \in \mathcal{A} \right\} $$
几何上，[原子范数](@entry_id:746563)是原[子集](@entry_id:261956) $\mathcal{A}$ 的凸包的**[规范函数](@entry_id:749731)**（gauge function）。由于它使用了连续参数化的原[子集](@entry_id:261956)，[原子范数](@entry_id:746563)最小化（一个凸问题）能够避免基不匹配，从而实现“无网格”的超分辨率恢复。对于正弦和问题，[原子范数](@entry_id:746563)最小化可以被精确地重构为一个 SDP，使其在计算上是可行的。

### 核心算法原理

一旦问题被表述为[凸优化](@entry_id:137441)形式，我们就需要算法来求解它。对于许多大规模信号处理问题，通用求解器可能不够高效，需要利用问题结构的专用算法。

#### [近端算法](@entry_id:174451)与 Moreau 分解

许多[优化问题](@entry_id:266749)可以写成一个光滑项和一个非光滑项之和的形式，例如 $f(x) + g(x)$，其中 $f$ 光滑（如最小二乘），$g$ 非光滑（如 $\ell_1$-范数）。**[近端算法](@entry_id:174451)**（proximal algorithms）是处理这类问题的强大框架。其核心是**[近端算子](@entry_id:635396)**（proximal operator），定义为：
$$ \operatorname{prox}_{\gamma g}(v) = \arg\min_x \left( g(x) + \frac{1}{2\gamma} \|x-v\|_2^2 \right) $$
[近端算子](@entry_id:635396)可以看作是对点 $v$ 的一种正则化投影或收缩。例如，$\ell_1$-范数的[近端算子](@entry_id:635396)是**[软阈值算子](@entry_id:755010)**（soft-thresholding operator），$S_\gamma(v)_i = \operatorname{sgn}(v_i) \max(|v_i|-\gamma, 0)$。

一个深刻而优美的理论工具是 **Moreau 分解** [@problem_id:2861574]，它将任意一个向量 $v$ 分解为两部分，一部分与函数 $f$ 的[近端算子](@entry_id:635396)有关，另一部分与其共轭函数 $f^*$ 的[近端算子](@entry_id:635396)有关：
$$ v = \operatorname{prox}_{\gamma f}(v) + \gamma \operatorname{prox}_{f^*/\gamma}(v/\gamma) $$
这个恒等式揭示了[近端算子](@entry_id:635396)与对偶性之间的深刻联系。例如，令 $f(x) = \|x\|_\infty$，其共轭 $f^*$ 是 $\ell_1$ [单位球](@entry_id:142558)的[指示函数](@entry_id:186820) $I_{B_1}(y)$。那么，$\operatorname{prox}_{\gamma f^*} (v)$ 就是到 $\ell_1$ 球上的欧几里得投影 $P_{B_1}(v)$。Moreau 分解告诉我们，$\|x\|_\infty$ 的[近端算子](@entry_id:635396)可以通过到 $\ell_1$ 球的投影来计算：$\operatorname{prox}_{\gamma\|\cdot\|_\infty}(v) = v - \gamma P_{B_1}(v/\gamma)$。

#### [交替方向乘子法](@entry_id:163024)（ADMM）

对于形如 $\min_x f(x) + g(\mathbf{A}x)$ 的[复合优化](@entry_id:165215)问题，一个非常流行且有效的算法是**[交替方向乘子法](@entry_id:163024)**（[ADMM](@entry_id:163024)）[@problem_id:2861535]。[ADMM](@entry_id:163024) 通过**变量分裂**（variable splitting）将问题转化为一个带[线性约束](@entry_id:636966)的等价问题：
$$ \min_{x, z} f(x) + g(z) \quad \text{s.t.} \quad \mathbf{A}x - z = 0 $$
然后，它为这个问题构造**增广[拉格朗日函数](@entry_id:174593)**，并交替地最小化关于 $x$ 和 $z$ 的函数，然后更新对偶变量。使用一个缩放的[对偶变量](@entry_id:143282) $u$，ADMM 的迭代步骤如下：
1.  **$x$-更新**：$x^{k+1} = \arg\min_x \left( f(x) + \frac{\rho}{2} \|\mathbf{A}x - z^k + u^k\|_2^2 \right)$
2.  **$z$-更新**：$z^{k+1} = \arg\min_z \left( g(z) + \frac{\rho}{2} \|\mathbf{A}x^{k+1} - z + u^k\|_2^2 \right)$
3.  **对偶更新**：$u^{k+1} = u^k + \mathbf{A}x^{k+1} - z^{k+1}$

这里 $\rho > 0$ 是一个惩罚参数。$x$-更新和 $z$-更新通常比原问题更容易求解。特别是，$z$-更新步经常可以被解析地表示为 $g$ 的[近端算子](@entry_id:635396)，即 $z^{k+1} = \operatorname{prox}_{g/\rho}(\mathbf{A}x^{k+1} + u^k)$。ADMM 将一个复杂问题分解为一系列更简单的子问题，使其非常适用于[分布式计算](@entry_id:264044)和大规模应用。

### 理论保证一瞥：为何松弛有效？

[凸松弛](@entry_id:636024)方法（如[核范数最小化](@entry_id:634994)和[原子范数](@entry_id:746563)最小化）的一个惊人之处在于，在某些条件下，它们不仅能找到原非凸问题的近似解，还能精确地恢复出真实的、低维度的信号结构。这些理论保证是现代信号处理的基石之一。

以**[矩阵补全](@entry_id:172040)**（matrix completion）问题为例，其目标是从少量[随机采样](@entry_id:175193)的元素中恢复一个低秩矩阵 $M$ [@problem_id:2861572]。恢复方法是[核范数最小化](@entry_id:634994)：
$$ \min_X \|X\|_* \quad \text{s.t.} \quad \mathcal{P}_\Omega(X) = \mathcal{P}_\Omega(M) $$
其中 $\mathcal{P}_\Omega$ 是在采样点集合 $\Omega$ 上的[投影算子](@entry_id:154142)。理论分析表明，如果低秩矩阵 $M$ 满足某些**非[相干性](@entry_id:268953)**（incoherence）条件，并且采样数量 $|\Omega|$ 足够大，那么以高概率可以精确恢复 $M$。

-   **非相干性**：这个条件本质上要求矩阵的奇异向量不是“尖峰状”的，即它们的能量不能集中在少数几个分量上。如果[奇异向量](@entry_id:143538)是“弥散”的，那么矩阵的能量会均匀地[分布](@entry_id:182848)在所有元素中，这样[随机采样](@entry_id:175193)才能有效地“看到”矩阵的整体结构。标准的非[相干性](@entry_id:268953)假设要求 $M$ 的左、[右奇异向量](@entry_id:754365)矩阵 $U, V$ 的所有行的范数都有界，例如 $\|U^\top e_i\|_2^2 \le \frac{\mu r}{n}$，其中 $r$ 是秩，$n$ 是维度，$\mu$ 是一个小的非[相干性](@entry_id:268953)参数。

-   **采样复杂度**：一个秩为 $r$ 的 $n \times n$ 矩阵大约有 $2nr - r^2 \approx \mathcal{O}(nr)$ 个自由度。因此，任何成功的恢复都至少需要这么多的样本。精确的理论结果表明，所需的样本数量接近这个信息论下界，通常的形式为：
    $$ |\Omega| \ge C \cdot \mu \cdot n \cdot r \cdot \log n $$
    其中 $C$ 是一个常数，$\log n$ 因子来源于概率理论中用于证明恢复的[集中不等式](@entry_id:273366)。

这些结果表明，只要信号模型具有良好的几何结构（非相干性），并且我们拥有足够多的（但仍是稀疏的）随机观测，[凸优化](@entry_id:137441)就能奇迹般地找到隐藏在海量可能性中的那个唯一的、简单的真实解。