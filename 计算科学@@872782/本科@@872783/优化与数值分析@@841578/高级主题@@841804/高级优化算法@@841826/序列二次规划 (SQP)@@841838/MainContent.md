## 引言
在科学、工程和经济学的众多领域中，我们常常面临一[类核](@entry_id:178267)心挑战：在满足一系列复杂约束的条件下，找到某个性能指标的最优解。这些问题被抽象为[非线性规划](@entry_id:636219)（NLP），而直接求解它们通常极为困难。序列二次规划（Sequential Quadratic Programming, SQP）正是一种为解决此类问题而生的、功能强大且应用广泛的迭代算法。SQP的核心思想极为巧妙，它将一个难以处理的[非线性](@entry_id:637147)问题，通过在每一步迭代中构建并求解一个更简单的“代理”问题——二次规划（QP）问题——来逐步逼近最优解。

本文将系统地引导你深入理解SQP方法。在“原理与机制”一章中，我们将剖析算法的理论基石，从[拉格朗日函数](@entry_id:174593)到QP子问题的构建，再到其与[牛顿法](@entry_id:140116)的深刻联系。接下来，在“应用与跨学科联系”一章，我们将展示SQP如何在工程设计、最优控制、科学计算等不同领域中解决真实世界的问题。最后，“动手实践”部分将提供具体的计算练习，帮助你巩固所学知识，将理论付诸实践。通过这一学习路径，你将全面掌握SQP的精髓及其解决复杂[优化问题](@entry_id:266749)的强大能力。

## 原理与机制

在[非线性规划](@entry_id:636219)（NLP）领域，序列二次规划（Sequential Quadratic Programming, SQP）是一类功能强大且应用广泛的[迭代算法](@entry_id:160288)。其核心思想是将一个复杂的非线性[约束优化](@entry_id:635027)问题，在当前迭代点附近，通过一系列简化模型进行近似，然后求解这些近似问题来逐步逼近原问题的解。本章将深入探讨SQP方法的基本原理、核心机制及其在实际应用中的关键组成部分。

### 拉格朗日函数：连接目标与约束的桥梁

在深入SQP算法的细节之前，我们必须首先理解**[拉格朗日函数](@entry_id:174593)（Lagrangian function）**，它是[约束优化理论](@entry_id:635923)的基石。对于一个一般的[非线性规划](@entry_id:636219)问题，其形式如下：
$$
\begin{align*}
\underset{x \in \mathbb{R}^n}{\text{minimize}}  \quad f(x) \\
\text{subject to}  \quad h_i(x) = 0, \quad i \in \mathcal{E} \\
 \quad g_j(x) \le 0, \quad j \in \mathcal{I}
\end{align*}
$$
其中 $f(x)$ 是[目标函数](@entry_id:267263)，$h_i(x)$ 是[等式约束](@entry_id:175290)，$g_j(x)$ 是[不等式约束](@entry_id:176084)。我们可以引入与每个约束相对应的**[拉格朗日乘子](@entry_id:142696)（Lagrange multipliers）**——$\lambda_i$ 对应[等式约束](@entry_id:175290)，$ \mu_j $ 对应[不等式约束](@entry_id:176084)——并将目标函数与约束函数组合成一个单一的函数，即[拉格朗日函数](@entry_id:174593) $L(x, \lambda, \mu)$。

例如，对于一个[目标函数](@entry_id:267263)为 $f(x_1, x_2) = \exp(x_1) + x_1 x_2^2 + 3x_2$，[等式约束](@entry_id:175290)为 $h(x_1, x_2) = x_1^2 + \sin(x_2) - 5 = 0$，[不等式约束](@entry_id:176084)为 $g(x_1, x_2) = x_1 + x_2 - 2 \le 0$ 的问题，其拉格朗日函数被定义为：
$$
L(x_1, x_2, \lambda, \mu) = f(x_1, x_2) + \lambda h(x_1, x_2) + \mu g(x_1, x_2)
$$
代入具体的函数表达式，我们得到：
$$
L(x_1, x_2, \lambda, \mu) = \exp(x_1) + x_1 x_2^2 + 3x_2 + \lambda(x_1^2 + \sin(x_2) - 5) + \mu(x_1 + x_2 - 2)
$$
[@problem_id:2202030]。拉格朗日函数将一个约束问题转化为对其[鞍点](@entry_id:142576)（saddle point）的寻找。最优解必须满足 [Karush-Kuhn-Tucker (KKT) 条件](@entry_id:176491)，这些条件描述了拉格朗日函数梯度为零、原始可行性以及[互补松弛性](@entry_id:141017)等性质。SQP算法的最终目标，正是要找到满足这些[KKT条件](@entry_id:185881)的点 $(x^*, \lambda^*, \mu^*)$。

### SQP子问题：构建局部近似模型

SQP方法通过迭代求解一系列**二次规划（Quadratic Programming, QP）**子问题来逼近原NLP的解。在每个迭代步 $k$，给定当前解的估计 $x_k$，算法会构建一个关于步长 $p = x - x_k$ 的QP子问题。这个QP子问题是对原问题在 $x_k$ 附近的一个局部近似，其构建包含两个关键部分：

1.  **约束的线性化**：原始的非[线性约束](@entry_id:636966)（例如 $c(x)=0$）通常难以直接处理。SQP通过一阶[泰勒展开](@entry_id:145057)，在点 $x_k$ 处将它们线性化。对于一个步长 $p$，线性化约束变为：
    $$
    c(x_k) + J(x_k)p = 0
    $$
    其中 $J(x_k)$ 是约束函数 $c(x)$ 在 $x_k$ 处的雅可比矩阵（Jacobian matrix）。这个线性化步骤是至关重要的，因为它将复杂的非[线性约束](@entry_id:636966)[曲面](@entry_id:267450)近似为一个易于处理的线性[超平面](@entry_id:268044)。其主要的计算动机在于，[线性约束](@entry_id:636966)与二次目标函数的组合，恰好构成了一个**二次规划（QP）问题**。现代计算库中包含了许多高效且成熟的QP求解器，这使得求解子问题变得非常可行 [@problem_id:2202046]。

2.  **拉格朗日函数的二次模型**：SQP子问题的[目标函数](@entry_id:267263)并非简单地对原目标函数 $f(x)$ 进行二次近似，而是对**拉格朗日函数 $L(x, \lambda)$** 进行二次近似。这使得模型能够同时捕捉目标函数的变化和约束的影响。在第 $k$ 步，这个目标函数通常写成：
    $$
    \min_{p} \quad \nabla f(x_k)^T p + \frac{1}{2} p^T B_k p
    $$
    其中 $\nabla f(x_k)$ 是原目标函数在 $x_k$ 处的梯度，而矩阵 $B_k$ 是对[拉格朗日函数](@entry_id:174593)的[海森矩阵](@entry_id:139140)（Hessian matrix） $\nabla_{xx}^2 L(x_k, \lambda_k)$ 的一个近似。

将这两部分结合起来，一个典型的[等式约束](@entry_id:175290)SQP子问题就形成了：
$$
\begin{align*}
\underset{p \in \mathbb{R}^n}{\text{minimize}}  \quad \frac{1}{2} p^T B_k p + \nabla f(x_k)^T p \\
\text{subject to}  \quad \nabla c(x_k)^T p + c(x_k) = 0
\end{align*}
$$
这个QP子问题的解 $p_k$ 给出了从当前点 $x_k$ 到下一个估计点 $x_{k+1}$ 的**搜索方向（search direction）**。专门的QP求解器作为SQP算法的核心子程序，其功能正是在每个主迭代中计算出这个最优的搜索方向 $p_k$ [@problem_id:2201997]。

### SQP与[牛顿法](@entry_id:140116)的深刻联系

SQP方法之所以如此高效，一个深层的原因是它与[求解非线性方程](@entry_id:177343)组的**牛顿法（Newton's method）**之间存在紧密的联系。一个带[等式约束](@entry_id:175290)的NL[P问题](@entry_id:267898)的[KKT条件](@entry_id:185881)可以表示为一个非线性方程组：
$$
\begin{cases}
\nabla_x L(x, \lambda) = \nabla f(x) + \nabla c(x) \lambda = 0  \text{(Stationarity)} \\
c(x) = 0  \text{(Feasibility)}
\end{cases}
$$
我们可以将这个系统看作是关于变量 $(x, \lambda)$ 的[方程组](@entry_id:193238) $F(x, \lambda) = 0$。对这个系统应用牛顿法来求解，在一次迭代中，我们需要求解如下的[线性系统](@entry_id:147850)来获得更新步长 $(p, \delta_\lambda)$：
$$
J_F(x_k, \lambda_k) \begin{pmatrix} p \\ \delta_\lambda \end{pmatrix} = -F(x_k, \lambda_k)
$$
其中 $J_F$ 是 $F$ 的雅可比矩阵。展开后，这个[线性系统](@entry_id:147850)是：
$$
\begin{pmatrix}
\nabla_{xx}^2 L(x_k, \lambda_k) & \nabla c(x_k) \\
\nabla c(x_k)^T & 0
\end{pmatrix}
\begin{pmatrix}
p_k \\
\lambda_{k+1}
\end{pmatrix}
=
\begin{pmatrix}
-\nabla f(x_k) \\
-c(x_k)
\end{pmatrix}
$$
（这里我们将新的乘子估计写为 $\lambda_{k+1}$）。这恰好是前面定义的SQP子问题的[KKT条件](@entry_id:185881)，其中 $B_k$ 取为拉格朗日函数的精确[海森矩阵](@entry_id:139140) $\nabla_{xx}^2 L(x_k, \lambda_k)$ [@problem_id:2202015]。

这个深刻的联系表明，当使用精确的二阶信息时，SQP方法本质上是在对原问题的[KKT条件](@entry_id:185881)应用[牛顿法](@entry_id:140116)。这解释了SQP为何在解的邻域内能够表现出极快的**二次收敛速度**。同时，这也揭示了拉格朗日乘子是如何更新的：QP子问题的解不仅给出了步长 $p_k$，也直接给出了下一个迭代步的乘子估计 $\lambda_{k+1}$ [@problem_id:2201973]。

### 构建稳健的SQP算法

理论上的SQP模型非常优雅，但在实际应用中，还需要一些关键机制来确保算法的**[全局收敛性](@entry_id:635436)（global convergence）**和**计算效率（computational efficiency）**。

#### [全局化策略](@entry_id:177837)：价值函数与[线性搜索](@entry_id:633982)

QP子问题给出的搜索方向 $p_k$ 只是一个局部最优方向，直接执行一步完整的更新 $x_{k+1} = x_k + p_k$ 可能会导致迭代发散，特别是在远离最优解时。这是因为新点可能极大地增加了[目标函数](@entry_id:267263)值或约束违反度。为了确保每一步迭代都能取得“有意义”的进展，SQP算法引入了**[价值函数](@entry_id:144750)（merit function）**。

[价值函数](@entry_id:144750) $\phi(x; \rho)$ 是一个综合性指标，它将[目标函数](@entry_id:267263) $f(x)$ 的减小和约束违反度（如 $\|c(x)\|$）的减小这两个有时相互冲突的目标，通过一个惩罚参数 $\rho$ 结合起来。一个常见的例子是 $l_1$ 精确[价值函数](@entry_id:144750)：
$$
\phi(x; \rho) = f(x) + \rho \|c(x)\|_1
$$
在得到搜索方向 $p_k$ 后，算法会沿着这个方向进行**[线性搜索](@entry_id:633982)（line search）**，寻找一个步长 $\alpha_k \in (0, 1]$，使得价值函数得到充分下降，例如满足[Armijo条件](@entry_id:169106)：
$$
\phi(x_k + \alpha_k p_k; \rho) \le \phi(x_k; \rho) + c_1 \alpha_k D\phi(x_k; p_k)
$$
其中 $D\phi(x_k; p_k)$ 是价值函数在 $p_k$ 方向的[方向导数](@entry_id:189133)。通过这种方式，价值函数引导算法在朝着最优解前进的路上，巧妙地平衡了“降低目标函数”和“满足约束”这两个任务，即使在迭代点不可行的情况下也能保证[全局收敛性](@entry_id:635436) [@problem_id:2202029]。

#### [拟牛顿法](@entry_id:138962)：近似海森矩阵

计算和存储拉格朗日函数的精确海森矩阵 $\nabla_{xx}^2 L$ 在许多大规模问题中是不切实际的，有时甚至是不可能的。为了克服这一困难，**拟牛顿SQP（Quasi-Newton SQP）**方法应运而生。这类方法不计算精确的 $B_k$，而是通过一个相对廉价的更新公式来迭代地近似它。

最著名的更新公式是**BFGS (Broyden–Fletcher–Goldfarb–Shanno)** 更新。在完成一步从 $x_k$ 到 $x_{k+1}$ 的移动后，我们计算两个关键向量：
-   步长向量：$s_k = x_{k+1} - x_k = \alpha_k p_k$
-   拉格朗日梯度变化量：$y_k = \nabla_x L(x_{k+1}, \lambda_{k+1}) - \nabla_x L(x_k, \lambda_{k+1})$

向量 $y_k$ 包含了关于函数曲率的宝贵信息。BFGS公式利用 $s_k$ 和 $y_k$ 来更新[海森矩阵](@entry_id:139140)的近似 $B_k$：
$$
B_{k+1} = B_k - \frac{B_k s_k s_k^T B_k}{s_k^T B_k s_k} + \frac{y_k y_k^T}{y_k^T s_k}
$$
这个更新过程 [@problem_id:2202033] 巧妙地利用了过去迭代的信息，使得 $B_{k+1}$ 能够更好地模拟真实[海森矩阵](@entry_id:139140)的行为，同时保持了[正定性](@entry_id:149643)（在一定条件下）。这使得算法既能逼近[牛顿法](@entry_id:140116)的快速收敛性，又避免了[二阶导数](@entry_id:144508)的直接计算，极大地提高了SQP方法的实用性。

#### 实例：计算一次SQP迭代

让我们通过一个例子来具体看一次SQP迭代的计算过程。考虑最小化 $f(x_1, x_2) = x_1^2 + \exp(x_2)$，约束为 $c(x_1, x_2) = x_1^2 + x_2^2 - 1 = 0$。从初始点 $x_0 = (1, 1)^T$ 开始，并使用[单位矩阵](@entry_id:156724) $B_0 = I$ 作为[海森矩阵](@entry_id:139140)的初始近似。

1.  **计算所需量**：在 $x_0 = (1, 1)^T$ 处，我们有：
    $\nabla f(x_0) = \begin{pmatrix} 2 \\ \exp(1) \end{pmatrix}$, $c(x_0) = 1^2 + 1^2 - 1 = 1$, $\nabla c(x_0) = \begin{pmatrix} 2 \\ 2 \end{pmatrix}$。
2.  **构建QP子问题**：
    $$
    \begin{align*}
    \underset{p \in \mathbb{R}^2}{\text{minimize}}  \quad \frac{1}{2} p^T I p + \begin{pmatrix} 2 & \exp(1) \end{pmatrix} p \\
    \text{subject to}  \quad \begin{pmatrix} 2 & 2 \end{pmatrix} p + 1 = 0
    \end{align*}
    $$
3.  **求解QP子问题**：通过求解该QP子问题的[KKT系统](@entry_id:751047)，我们可以得到搜索方向 $p_0$ [@problem_id:2202032]。这个过程最终得到 $p_0 = \begin{pmatrix} \frac{2 \exp(1) - 5}{4} \\ \frac{3 - 2 \exp(1)}{4} \end{pmatrix}$。

这个 $p_0$ 便是从点 $(1,1)^T$ 出发的第一步搜索方向。接下来，算法将使用[价值函数](@entry_id:144750)和[线性搜索](@entry_id:633982)来确定最佳步长 $\alpha_0$，并更新点的位置 $x_1 = x_0 + \alpha_0 p_0$。

### 算法的终止与[异常处理](@entry_id:749149)

一个完整的SQP算法还需要处理两种特殊情况：如何判断算法已经收敛，以及当子问题无解时该怎么办。

#### 终止条件

如果某次迭代中，QP子问题的解为零向量，即 $p_k=0$，这意味着什么？我们将 $p_k=0$ 代入QP子问题的[KKT条件](@entry_id:185881)：
-   约束可行性：$\nabla c(x_k)^T (0) + c(x_k) = 0 \implies c(x_k) = 0$
-   梯度平稳性：$B_k (0) + \nabla f(x_k) + \nabla c(x_k) \nu_k = 0 \implies \nabla f(x_k) + \nabla c(x_k) \nu_k = 0$
其中 $\nu_k$ 是QP子问题的[拉格朗日乘子](@entry_id:142696)。这两个条件——原始可行性和梯度平稳性——正是原NL[P问题](@entry_id:267898)在点 $x_k$ 处的[KKT条件](@entry_id:185881)，其对应的拉格朗日乘子为 $\nu_k$。因此，当 $p_k=0$ 时，我们已经找到了原问题的一个KKT点 $x_k$ [@problem_id:2201970]。这为SQP算法提供了一个自然的**终止判据**。

#### 可行性恢复

在某些情况下，即使原NL[P问题](@entry_id:267898)是可行的，其在某点 $x_k$ 处的线性化约束也可能相互矛盾，导致QP子问题**不可行（infeasible）**。例如，线性化后的[等式约束](@entry_id:175290)可能代表永不相交的[平行线](@entry_id:169007)。在这种情况下，一个稳健的SQP求解器不会立即宣告失败，而是会进入一个所谓的**可行性恢复（feasibility restoration）**阶段。

该阶段的目标是暂时忽略优化目标，转而专注于寻找一个能最小化约束违反度的步长。这通常通过求解一个辅助的[优化问题](@entry_id:266749)来实现，例如，一个最小化原始非线性约束违反度的 $l_1$ 范数的线性规划（LP）问题。一旦通过这个辅助问题找到了一个约束违反度更小的点，算法就会从这个新点重新开始常规的SQP迭代 [@problem_id:2202017]。这种机制大大增强了SQP算法在面对具有复杂约束几何形状问题时的鲁棒性。

综上所述，序列二次规划方法通过一系列精心设计的机制——将原问题近似为QP[子序列](@entry_id:147702)、使用牛顿法的理论洞察力、通过价值函数实现[全局收敛](@entry_id:635436)、利用拟牛顿法提高[计算效率](@entry_id:270255)，以及处理异常情况的稳健策略——构成了一套强大而灵活的[非线性优化](@entry_id:143978)求解框架。