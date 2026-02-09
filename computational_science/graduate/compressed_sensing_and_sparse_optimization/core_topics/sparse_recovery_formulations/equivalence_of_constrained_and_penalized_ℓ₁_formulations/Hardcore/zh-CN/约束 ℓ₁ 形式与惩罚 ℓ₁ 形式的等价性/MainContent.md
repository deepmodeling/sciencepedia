## 引言
在信号处理、统计学和机器学习领域，从不完全或含噪的测量中恢复稀疏信号是一个核心挑战。ℓ₁范数正则化作为一种强大的工具，催生了多种优化框架，其中最著名的是罚函数形式（如LASSO）和约束形式（如BPDN）。尽管它们在形式上有所不同，导致研究者和实践者可能会面临模型选择的困惑，但这些框架背后存在着深刻的数学等价性。本文旨在系统地阐明这一核心原理，填补理论理解与实际应用之间的鸿沟。通过本文的学习，您将掌握这一等价性的内在机制，并学会如何利用它来指导模型构建和参数选择。在“原理与机制”一章中，我们将深入剖析不同形式的最优性条件，揭示它们之间的数学联系。接下来，“应用与交叉学科联系”将展示这一原理如何扩展到更复杂的模型，并与统计学、图像处理等领域产生联系。最后，“动手实践”部分将通过具体的编程练习，帮助您将理论知识转化为实践技能。

## 原理与机制

在稀疏优化领域，为从不完全或含噪的测量中恢复稀疏信号，发展了多种优化框架。这些框架虽然形式各异，但其核心思想都是在数据保真度与解的稀疏性之间寻求平衡。其中，最核心的三种形式是罚函数形式（LASSO）、$\ell_1$范数球约束的最小二乘（Constrained Least Squares, CLS）以及残差约束的基追踪降噪（Basis Pursuit Denoising, BPDN）。本章将深入探讨这三种形式之间的深刻等价性。我们将从各自的最优性条件出发，建立它们之间的数学联系，并通过几何直观和帕累托最优理论来加深理解。最后，我们将讨论解的唯一性条件和极限行为，这些是在实际应用和算法设计中必须考虑的关键问题。

### 优化的基石：$\ell_1$ 范数问题的最优性条件

理解不同形式之间等价性的第一步是精确地写出它们各自的最优性条件。这些条件源于凸优化理论中的Karush-Kuhn-Tucker (KKT) 条件，是判断一个解是否为最优解的必要且充分的准则。

#### LASSO：罚函数形式

最广为人知的罚函数形式是**最小绝对收缩与选择算子 (Least Absolute Shrinkage and Selection Operator, LASSO)** [@problem_id:3446579]。给定一个设计矩阵 $A \in \mathbb{R}^{m \times n}$ 和观测向量 $y \in \mathbb{R}^{m}$，LASSO 问题旨在求解：
$$
\min_{x \in \mathbb{R}^{n}} \left( \frac{1}{2}\|A x - y\|_2^2 + \lambda \|x\|_1 \right)
$$
其中 $\lambda \ge 0$ 是一个正则化参数，用于权衡二次损失项（数据保真度）和 $\ell_1$ 范数惩罚项（稀疏性）。

该目标函数是两个凸函数之和：光滑的二次损失函数 $f(x) = \frac{1}{2}\|Ax - y\|_2^2$ 和非光滑的 $\ell_1$ 范数 $g(x) = \lambda \|x\|_1$。对于这类问题，一个点 $x^\star$ 是最优解的充要条件是零向量属于目标函数在 $x^\star$ 处的**次微分**（subdifferential）。根据次微分的加法法则，我们得到：
$$
0 \in \nabla f(x^\star) + \partial g(x^\star)
$$
代入具体的函数形式，$\nabla f(x) = A^\top(Ax - y)$ 和 $\partial (\lambda \|x\|_1) = \lambda \partial \|x\|_1$，最优性条件可以写作：
$$
0 \in A^\top(Ax^\star - y) + \lambda \partial \|x^\star\|_1
$$
这意味着，存在一个向量 $s \in \partial \|x^\star\|_1$，使得 $A^\top(Ax^\star - y) + \lambda s = 0$ [@problem_id:3446579]。

向量 $s$ 被称为在 $x^\star$ 处的**次梯度**（subgradient）。$\ell_1$ 范数的次微分 $\partial \|x\|_1$ 具有清晰的分量结构，这正是 $\ell_1$ 范数能够诱导稀疏性的关键。对于任意向量 $x$，其次微分 $\partial \|x\|_1$ 是所有满足以下条件的向量 $s$ 的集合：
$$
s_i = \begin{cases} \operatorname{sign}(x_i),  & \text{if } x_i \neq 0 \\ v,  & \text{if } x_i = 0, \text{ where } v \in [-1, 1] \end{cases}
$$
将此结构代入最优性条件，我们可以得到一组更具体的逐分量条件 [@problem_id:3446579]：
- 对于 $x^\star$ 的任意非零分量 $x^\star_i \ne 0$（即在**支撑集** $S = \operatorname{supp}(x^\star)$ 内），我们有：
  $$
  (A^\top(Ax^\star - y))_i = - \lambda \operatorname{sign}(x^\star_i)
  $$
  这表明，在最优解的支撑集上，损失函数梯度与 $A$ 的对应列的内积必须达到一个固定的阈值 $\lambda$。
- 对于 $x^\star$ 的任意零分量 $x^\star_i = 0$（即在支撑集之外），我们有：
  $$
  |(A^\top(Ax^\star - y))_i| \le \lambda
  $$
  这表明，对于那些未被选入模型的特征，其与梯度的相关性不足以克服 $\lambda$ 所设定的阈值。正是这个条件使得许多系数被“压缩”为零，从而产生稀疏解。

#### 约束形式：CLS 与 BPDN

与罚函数方法等价的还有两种约束形式。

第一种是**约束最小二乘 (Constrained Least Squares, CLS)**，它将 $\ell_1$ 范数作为约束边界：
$$
\min_{x \in \mathbb{R}^{n}} \frac{1}{2}\|Ax - y\|_2^2 \quad \text{subject to} \quad \|x\|_1 \le \tau
$$
其中 $\tau \ge 0$ 是一个约束半径，代表了模型复杂度的“预算”。该问题的 KKT 条件与 LASSO 非常相似，只是正则化参数 $\lambda$ 被拉格朗日乘子所替代 [@problem_id:3446574]。

第二种是**基追踪降噪 (Basis Pursuit Denoising, BPDN)**，它最小化 $\ell_1$ 范数，同时将数据保真度作为约束：
$$
\min_{x \in \mathbb{R}^{n}} \|x\|_1 \quad \text{subject to} \quad \|Ax - y\|_2 \le \varepsilon
$$
其中 $\varepsilon \ge 0$ 是允许的数据拟合误差容忍度。为了导出其 KKT 条件，我们构建拉格朗日函数 [@problem_id:3446595]：
$$
L(x, \mu) = \|x\|_1 + \mu (\|Ax - y\|_2 - \varepsilon)
$$
其中 $\mu \ge 0$ 是对应于不等式约束的拉格朗日乘子。KKT 条件包括：
1.  **原始可行性 (Primal Feasibility)**: $\|Ax^\star - y\|_2 \le \varepsilon$
2.  **对偶可行性 (Dual Feasibility)**: $\mu^\star \ge 0$
3.  **互补松弛性 (Complementary Slackness)**: $\mu^\star (\|Ax^\star - y\|_2 - \varepsilon) = 0$
4.  **平稳性 (Stationarity)**: $0 \in \partial \|x^\star\|_1 + \mu^\star \partial_x (\|Ax^\star - y\|_2)$

平稳性条件中的 $\partial_x (\|Ax - y\|_2)$ 项需要特别注意。通过链式法则，它等于 $A^\top \partial_u (\|u\|_2)|_{u=Ax-y}$。$\ell_2$ 范数的次微分在非零点是唯一的梯度 $\frac{u}{\|u\|_2}$，在零点则是一个单位球。因此，假设残差 $r^\star = Ax^\star - y \ne 0$，平稳性条件可以写作 [@problem_id:3446595]：
$$
0 \in \partial \|x^\star\|_1 + \mu^\star \frac{A^\top(Ax^\star - y)}{\|Ax^\star - y\|_2}
$$
互补松弛性条件揭示了一个关键点：如果最优乘子 $\mu^\star > 0$，那么约束必须是**激活的 (active)**，即 $\|Ax^\star - y\|_2 = \varepsilon$。这意味着，除非问题是平凡的（例如，$x=0$ 是最优解），否则最优解总是在误差边界上取得。

### 等价性原理：连接不同形式的桥梁

现在我们已经为三种形式建立了各自的最优性条件，它们之间的等价性变得清晰可见。本质上，这三种形式只是在用不同的参数（$\lambda, \tau, \varepsilon$）来探索同一个解的集合。

比较 LASSO 和 BPDN 的平稳性条件。假设 BPDN 的解 $x^\star$ 满足激活的约束 $\|Ax^\star - y\|_2 = \varepsilon > 0$，其对应的乘子为 $\mu^\star > 0$。其平稳性条件为：
$$
0 \in \partial \|x^\star\|_1 + \frac{\mu^\star}{\varepsilon} A^\top(Ax^\star - y)
$$
LASSO 的平稳性条件可以重写为：
$$
0 \in \frac{1}{\lambda} A^\top(Ax^\star - y) + \partial \|x^\star\|_1
$$
通过比较这两个表达式，我们发现它们是完全相同的，只要参数满足以下关系 [@problem_id:3446599] [@problem_id:3446574]：
$$
\frac{1}{\lambda} = \frac{\mu^\star}{\varepsilon} \quad \iff \quad \lambda = \frac{\varepsilon}{\mu^\star}
$$
这个简单的公式建立了 LASSO 参数 $\lambda$ 和 BPDN 参数 $\varepsilon$ 之间的深刻联系。它表明，对于一个给定的 BPDN 问题（由 $\varepsilon$ 定义），只要其解的约束是激活的，总存在一个对应的 $\lambda$，使得同一个解也是 LASSO 问题的解。

类似地，LASSO 和 CLS 之间的等价性也来自 KKT 条件的比较。对于 CLS 问题的一个解 $x^\star_\tau$，如果约束是激活的（$\|x^\star_\tau\|_1 = \tau$），那么其 KKT 平稳性条件为 $-A^\top(Ax^\star_\tau - y) \in \nu^\star \partial\|x^\star_\tau\|_1$，其中 $\nu^\star$ 是 CLS 的拉格朗日乘子。这与 LASSO 的最优性条件形式完全一样。因此，我们可以建立对应关系：$\lambda = \nu^\star$ [@problem_id:3446574]。

这个等价性原理告诉我们：
- 对于任意给定的 $\lambda > 0$，其 LASSO 解 $x^\star_\lambda$ 同时也是 CLS 问题的解，只需设置 $\tau = \|x^\star_\lambda\|_1$。
- 对于任意给定的 $\tau > 0$，如果其 CLS 解 $x^\star_\tau$ 使得约束 $\|x\|_1 \le \tau$ 激活，那么存在一个 $\lambda \ge 0$（即对应的拉格朗日乘子），使得 $x^\star_\tau$ 也是 LASSO 问题的解。
- 类似的对应关系也存在于 BPDN 和 LASSO 之间。

这三种形式本质上是在描述同一个权衡问题的不同侧面，它们共享相同的最优解集，只是通过不同的参数来索引这些解。

### 等价性的几何诠释

除了代数上的 KKT 条件，我们还可以从几何角度来理解这种等价性，这为我们提供了强大的直观图像 [@problem_id:3446577]。

考虑 CLS 问题：$\min_x f(x)$ s.t. $\|x\|_1 \le \tau$，其中 $f(x) = \frac{1}{2}\|Ax - y\|_2^2$。在几何上，这个问题是在寻找 $f(x)$ 的一个水平集（level set），该水平集刚好与 $\ell_1$ 范数球 $B_1(\tau)=\{x: \|x\|_1 \le \tau\}$ 相切。在切点 $x^\star$ 处，两个集合的法向量必须是共线的。$f(x)$ 在 $x^\star$ 处的法向量由其梯度 $\nabla f(x^\star)$ 给出，而 $\ell_1$ 球在 $x^\star$ 处的法向量（更准确地说是法锥中的一个向量）则由次梯度 $s \in \partial\|x^\star\|_1$ 给出。因此，相切条件可以表示为：
$$
-\nabla f(x^\star) = \nu^\star s
$$
其中 $\nu^\star \ge 0$ 是一个标量。这正是 CLS 的 KKT 平稳性条件。

对于 LASSO 问题，最优性条件 $-\nabla f(x^\star) \in \lambda \partial\|x^\star\|_1$ 具有完全相同的几何意义。它同样要求损失函数的负梯度向量必须与在 $x^\star$ 处的 $\ell_1$ 范数的一个次梯度成正比。这再次表明，LASSO 的解 $x^\star$ 也是一个切点，只不过这次相切的 $\ell_1$ 球的半径 $\tau = \|x^\star\|_1$ 是由 $\lambda$ 隐式决定的 [@problem_id:3446577]。

对于 BPDN 问题，几何图像是：我们寻找一个半径最小的 $\ell_1$ 球，使其刚好与数据拟合约束集 $\mathcal{C}_\varepsilon = \{x: \|Ax-y\|_2 \le \varepsilon\}$ 相交。在最优解 $x^\star$ 处，这两个集合（$\ell_1$ 球和约束集 $\mathcal{C}_\varepsilon$）必然相切。同样，这意味着它们的法向量共线，这导出了 BPDN 的 KKT 条件 [@problem_id:3446577]。

因此，无论从哪个形式出发，最优解都出现在数据保真度（由 $f(x)$ 的水平集表示）和稀疏性（由 $\|x\|_1$ 的水平集表示）达到某种“相切”平衡的点。

### 帕累托最优曲线与解路径

我们可以将稀疏性与数据拟合误差之间的权衡关系形式化为一个**帕累托最优曲线 (Pareto optimal curve)**。

#### 解路径的性质

在深入帕累托曲线之前，我们先观察当调整正则化参数 $\lambda$ 时，LASSO 解的性质如何变化。这是一个关键的动态视角，描述了我们如何在不同的权衡点之间移动 [@problem_id:3446599]。

令 $x_\lambda$ 为对应于参数 $\lambda$ 的 LASSO 解。可以证明，随着 $\lambda$ 的增加：
1.  解的 $\ell_1$ 范数 $\|x_\lambda\|_1$ 是非增的。当 $\lambda$ 增大时，对非稀疏解的惩罚加重，迫使解变得更加稀疏（或其分量的绝对值更小），因此其 $\ell_1$ 范数会减小或保持不变。
2.  残差的 $\ell_2$ 范数 $\|Ax_\lambda - y\|_2$ 是非减的。当 $\lambda$ 增大时，优化目标中数据保真度的权重相对降低，优化器愿意牺牲更多的数据拟合度来换取更小的 $\ell_1$ 范数，因此残差会增大或保持不变。

当 $\lambda = 0$ 时，LASSO 问题退化为标准的最小二乘问题。当 $\lambda \to \infty$ 时，为了最小化 $\lambda\|x\|_1$ 项，解将被迫趋向于 $x=0$（只要 $y \ne 0$）。因此，通过从 0 到无穷大扫描 $\lambda$，我们实际上是在追踪一条从最小二乘解到零向量的**解路径 (solution path)**。这条路径上的每一个点都对应一个特定的稀疏性与拟合误差的权衡。

#### 帕累托曲线与参数映射

这条解路径可以用帕累托曲线来精确描述。考虑 CLS 问题的**值函数 (value function)** $\varphi(\tau)$，它给出了在给定的 $\ell_1$ 范数预算 $\tau$ 下，可实现的最小数据拟合误差 [@problem_id:3446581]：
$$
\varphi(\tau) = \min_{x \in \mathbb{R}^n} \left\{ \frac{1}{2}\|Ax - y\|_2^2 \quad \text{s.t.} \quad \|x\|_1 \le \tau \right\}
$$
这个函数 $\varphi(\tau)$ 是关于 $\tau$ 的凸函数且非增的。它的图像 $(\tau, \varphi(\tau))$ 就是帕累托最优曲线。曲线上的每一个点 $(\tau, \varphi(\tau))$ 都代表一个最优权衡：不可能在不增加数据误差（即 $\varphi(\tau)$）的情况下进一步减小 $\ell_1$ 范数（即小于 $\tau$）。

根据优化理论中的**包络定理 (Envelope Theorem)**，值函数的导数与约束的拉格朗日乘子直接相关。在我们的例子中，如果 $\varphi(\tau)$ 在某点 $\tau$ 可微，那么它的导数等于该点最优解所对应的拉格朗日乘子（取负号） [@problem_id:3446576] [@problem_id:3446581]：
$$
\varphi'(\tau) = -\nu^\star
$$
我们已经知道，在等价性原理中，这个拉格朗日乘子 $\nu^\star$ 正是对应的 LASSO 问题中的正则化参数 $\lambda$。因此，我们得到了一个优美的关系：
$$
\lambda = -\varphi'(\tau)
$$
这个关系在几何上非常直观：帕累托曲线上某一点的斜率的负值，给出了要获得该点解（其 $\ell_1$ 范数为 $\tau$）所需的 LASSO 正则化参数 $\lambda$。这为在不同形式之间转换参数提供了坚实的理论基础。

#### 一个精确的二维示例

为了让这些抽象概念更具体，我们考虑一个简单的二维例子 [@problem_id:3446581]。设 $A=I_2$（单位矩阵），$y = (3, 1)^\top$。

- **LASSO 解路径**: 问题是可分离的，解为 $x_1(\lambda) = \max(3-\lambda, 0)$ 和 $x_2(\lambda) = \max(1-\lambda, 0)$。
  - 当 $0 \le \lambda \le 1$ 时, $x(\lambda) = (3-\lambda, 1-\lambda)^\top$。
  - 当 $1  \lambda \le 3$ 时, $x(\lambda) = (3-\lambda, 0)^\top$。
  - 当 $\lambda > 3$ 时, $x(\lambda) = (0, 0)^\top$。

- **CLS 解路径与值函数**: 求解 CLS 问题 $\min \frac{1}{2}\|x-y\|_2^2$ s.t. $\|x\|_1 \le \tau$。
  - 当 $2 \le \tau \le 4$ 时，可以解出 $x(\tau) = (\frac{\tau+2}{2}, \frac{\tau-2}{2})^\top$。此时值函数为 $\varphi(\tau) = \frac{1}{4}(\tau-4)^2$，其导数为 $\varphi'(\tau) = \frac{\tau-4}{2}$。
  - 当 $0 \le \tau  2$ 时，可以解出 $x(\tau) = (\tau, 0)^\top$。此时值函数为 $\varphi(\tau) = \frac{1}{2}((\tau-3)^2 + 1)$，其导数为 $\varphi'(\tau) = \tau-3$。

- **验证关系**: 我们来验证 $\lambda = -\varphi'(\tau)$。
  - 考虑 $\tau=3$，它属于区间 $[2,4]$。此时 $-\varphi'(3) = -(\frac{3-4}{2}) = \frac{1}{2}$。所以对应的 $\lambda$ 应该是 $0.5$。根据 LASSO 解路径，当 $\lambda=0.5$ 时，解为 $x(0.5) = (3-0.5, 1-0.5)^\top = (2.5, 0.5)^\top$。
  - 同时，根据 CLS 解路径，当 $\tau=3$ 时，解为 $x(3) = (\frac{3+2}{2}, \frac{3-2}{2})^\top = (2.5, 0.5)^\top$。
  - 两个解完全相同，验证了理论的正确性。

### 解的唯一性与极限情况

尽管三种形式在理论上是等价的，但在实际应用中，我们还需要关心解的性质，特别是唯一性。

#### LASSO解的唯一性

LASSO 问题的目标函数是严格凸的吗？这取决于矩阵 $A$。如果 $A$ 有非平凡的零空间（即 $A$ 不是列满秩的），那么损失函数 $\frac{1}{2}\|Ax-y\|_2^2$ 就不是严格凸的。即使如此，由于 $\ell_1$ 范数的“尖角”效应，解在很多情况下仍然是唯一的。

LASSO 解 $x^\star$ 是否唯一，取决于一个关键的集合，称为**等相关集 (equicorrelation set)** [@problem_id:3446586]。它定义为所有与残差 $r^\star = y-Ax^\star$ 相关性达到最大值 $\lambda$ 的特征的索引集合：
$$
E = \{j : |A_j^\top (Ax^\star - y)| = \lambda\}
$$
根据最优性条件，我们知道支撑集 $S$ 必然是等相关集 $E$ 的一个子集（$S \subseteq E$）。

LASSO 解 $x^\star$ 是唯一的**必要且充分条件**是：由等相关集 $E$ 的列构成的子矩阵 $A_E$ 是**列满秩**的（即其列线性无关）[@problem_id:3446586]。

这个条件意味着，如果存在一个特征 $j \notin S$，它与残差的相关性也达到了最大值 $\lambda$，并且 $A_j$ 可以被 $A_S$ 中的列线性表示，那么解就可能不是唯一的。直观上，这意味着优化器可以在不改变损失函数值和 $\ell_1$ 范数值的情况下，将解的能量从 $S$ 中的某些分量“移动”到分量 $j$ 上。

#### 当唯一性失效时：一个反例

考虑一个简单的例子，其中唯一性条件不满足 [@problem_id:3446575]。设 $A=[1, 1]$ 和 $y=1$。这里的两列是线性相关的。LASSO 问题为：
$$
\min_{x_1, x_2} \frac{1}{2}(x_1+x_2-1)^2 + \lambda(|x_1|+|x_2|)
$$
可以证明，对于 $0 \le \lambda  1$，最优的 $x_1+x_2$ 之和为 $t^\star = 1-\lambda$。任何满足 $x_1+x_2=1-\lambda$ 且 $x_1, x_2 \ge 0$ 的解都是最优解。例如，$x=(1-\lambda, 0)^\top$ 和 $x=(0, 1-\lambda)^\top$ 都是最优解。事实上，连接这两点的线段上的所有点都是最优解。

这种非唯一性对参数 $\varepsilon$ 和 $\lambda$ 之间的映射有重要影响。对于 $0 \le \lambda  1$ 范围内的任意 $\lambda$，所有解的残差范数都是 $\|(x_1+x_2)-1\|_2 = |(1-\lambda)-1| = \lambda$。这意味着从 $\varepsilon$ 到 $\lambda$ 的映射是 $\lambda = \varepsilon$，这是一个一对一的映射。然而，解集本身是多值的。

当 $\lambda \ge 1$ 时，唯一的解是 $x=(0,0)^\top$。此时的残差范数为 $\|0-1\|_2 = 1$。这意味着，对于所有 $\lambda \in [1, \infty)$，它们都对应于同一个 BPDN 问题，即 $\varepsilon=1$。因此，从 $\varepsilon$ 到 $\lambda$ 的映射是**一对多**的。在这种情况下，解向量是唯一的，但参数之间的对应关系不再唯一 [@problem_id:3446575]。

#### 极限行为：与基追踪的联系

最后，我们探讨当正则化参数趋于零时 LASSO 解的行为。这连接到了理想的无噪声情况。无噪声的**基追踪 (Basis Pursuit, BP)** 问题定义为：
$$
\min_{x \in \mathbb{R}^n} \|x\|_1 \quad \text{subject to} \quad Ax=y
$$
假设 $Ax=y$ 有解（即 $y$ 在 $A$ 的值域内），BP 问题旨在寻找其中具有最小 $\ell_1$ 范数的解。

可以证明，在非常普遍的条件下，当 $\lambda \to 0^+$ 时，LASSO 解序列 $\{x_\lambda\}$ 的任何聚点都是 BP 问题的解 [@problem_id:3446589]。这意味着 LASSO 在低噪声（小 $\lambda$）极限下会收敛到理想的稀疏解。更进一步，如果 BP 问题的解 $x^\star_{BP}$ 是唯一的，那么 LASSO 解会直接收敛到这个解：
$$
\lim_{\lambda \to 0^+} x_\lambda = x^\star_{BP}
$$
这个收敛性是稀疏恢复理论的基石之一，它保证了 LASSO 在处理接近无噪声数据时的有效性。其证明不依赖于像**受限等距性质 (Restricted Isometry Property, RIP)** 这样的强条件，而仅仅依赖于基本的凸分析原理 [@problem_id:3446589]。确保 BP 解唯一性的充分条件，例如支撑集上的子矩阵 $A_S$ 列满秩以及严格的对偶可行性，也同样保证了 LASSO 解的这种良好收敛行为。

总之，本章通过分析 KKT 条件、几何图像和帕累托最优理论，系统地阐明了罚函数和约束形式 $\ell_1$ 优化问题之间的深刻等价性。理解这些原理和机制，对于在特定应用中选择合适的模型、调整参数以及设计高效的求解算法都至关重要。