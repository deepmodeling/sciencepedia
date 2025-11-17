## 引言
在优化科学领域，[非线性规划](@entry_id:636219)（NLP）问题无处不在，从工程设计到金融建模，其应用广泛而深刻。然而，由于[目标函数](@entry_id:267263)或约束条件的[非线性](@entry_id:637147)特性，直接求解这些问题往往极其困难。序列二次规划（SQP）作为一种强大而高效的[迭代算法](@entry_id:160288)，为解决此类难题提供了一条行之有效的路径。其核心思想并非直接攻击原始的复杂问题，而是通过一系列局部近似，将其转化为更易于处理的子问题。

本文聚焦于SQP方法的心脏——二次规划（QP）子问题。我们将系统性地解答一个关键的知识缺口：这些QP子问题是如何从一个复杂的[非线性](@entry_id:637147)问题中精确构建出来的？它们背后又蕴含着怎样的数学原理和理论支撑？通过深入理解QP子问题，读者将能掌握SQP算法的精髓。

在接下来的内容中，我们将分三步展开：首先，在“原理与机制”一章中，我们将深入剖析QP子问题的构建方法、求解过程以及其与[牛顿法](@entry_id:140116)的深刻联系，并探讨[算法稳健性](@entry_id:635315)的关键议题。接着，在“应用与[交叉](@entry_id:147634)学科联系”一章中，我们将通过丰富的案例，展示QP子问题如何在工程、数据科学、金融等多个交叉学科领域中发挥关键作用。最后，“动手实践”部分将提供具体的练习，帮助读者将理论知识转化为实践技能。让我们一同开始，揭开SQP方法中二次规划子问题的神秘面纱。

## 原理与机制

在[非线性规划](@entry_id:636219)（NLP）的求解中，序列二次规划（SQP）是一种功能强大且被广泛应用的迭代方法。其核心思想在于将一个复杂的[非线性](@entry_id:637147)、[非凸优化](@entry_id:634396)问题，通过在当前迭代点进行局部近似，转化为一系列更容易求解的二次规划（QP）子问题。本章将深入探讨这些二次规划子问题的构建原理、求解机制、理论基础以及在实践中可能遇到的关键问题。

### 二次规划子问题的基本构建

考虑一个一般的[非线性规划](@entry_id:636219)问题：
$$
\begin{align*}
\underset{x \in \mathbb{R}^n}{\text{minimize}}  \quad f(x) \\
\text{subject to}  \quad c(x) = 0 \\
 \quad g(x) \le 0
\end{align*}
$$
其中 $f: \mathbb{R}^n \to \mathbb{R}$ 是目标函数，$c: \mathbb{R}^n \to \mathbb{R}^m$ 和 $g: \mathbb{R}^n \to \mathbb{R}^r$ 分别代表[等式约束](@entry_id:175290)和[不等式约束](@entry_id:176084)。直接求解此问题通常非常困难，因为它可能包含[非线性](@entry_id:637147)的目标函数和约束。

SQP方法在每次迭代（第 $k$ 次）时，会基于当前点 $x_k$ 构建一个近似模型。这种近似的核心动机在于，我们可以用一个结构更简单、有高效成熟求解算法的问题来替代原始的NLP [@problem_id:2202046]。二次规划（QP）——即目标函数为二次函数、约束为线性函数——正是理想的选择。

具体而言，SQP子问题在当前点 $x_k$ 为一个关于步长（或称搜索方向）$p \in \mathbb{R}^n$ 的[优化问题](@entry_id:266749)，其中新的迭代点将通过 $x_{k+1} = x_k + p$（或通过线搜索 $x_{k+1} = x_k + \alpha_k p$）来确定。这个QP子问题的构建包含两个关键部分：

1.  **约束的线性化**：原始的非[线性约束](@entry_id:636966) $c(x)=0$ 和 $g(x) \le 0$ 被它们在 $x_k$ 处的一阶[泰勒展开](@entry_id:145057)所替代。对于步长 $p = x - x_k$，我们有：
    $$
    \begin{align*}
    c(x_k + p) \approx c(x_k) + J_c(x_k) p = 0 \\
    g(x_k + p) \approx g(x_k) + J_g(x_k) p \le 0
    \end{align*}
    $$
    其中 $J_c(x_k)$ 和 $J_g(x_k)$ 分别是约束函数 $c$ 和 $g$ 在 $x_k$ 处的雅可比矩阵。这种线性化是至关重要的，因为它将复杂的[非线性](@entry_id:637147)[可行域](@entry_id:136622)局部近似为一个多面体，这是QP的标准约束形式 [@problem_id:2202046]。

2.  **[目标函数](@entry_id:267263)的二次模型**：仅仅线性化约束是不够的，我们还需要一个能够捕捉原始问题曲率信息的目标函数。SQP方法使用一个对**[拉格朗日函数](@entry_id:174593)** $\mathcal{L}(x, \lambda, \mu) = f(x) + \lambda^T c(x) + \mu^T g(x)$ 的二次近似作为QP子问题的目标函数。在迭代点 $x_k$ 处，这个二次模型写作：
    $$
    \underset{p}{\text{minimize}} \quad q(p) = \nabla f(x_k)^T p + \frac{1}{2} p^T B_k p
    $$
    这里的 $\nabla f(x_k)^T p$ 是[目标函数](@entry_id:267263) $f(x)$ 在 $x_k$ 处沿方向 $p$ 的[方向导数](@entry_id:189133)，它捕捉了函数的一阶变化。矩阵 $B_k$ 是一个对称矩阵，它旨在近似[拉格朗日函数](@entry_id:174593)在 $(x_k, \lambda_k, \mu_k)$ 处的黑塞矩阵（Hessian matrix） $\nabla_{xx}^2 \mathcal{L}(x_k, \lambda_k, \mu_k)$。$B_k$ 包含了问题的二阶（曲率）信息，对于算法的收敛速度和性能至关重要。

综合起来，在第 $k$ 次迭代中，我们需要求解的**二次规划子问题**可以写成：
$$
\begin{align*}
\underset{p \in \mathbb{R}^n}{\text{minimize}}  \quad \nabla f(x_k)^T p + \frac{1}{2} p^T B_k p \\
\text{subject to}  \quad c(x_k) + J_c(x_k) p = 0 \\
 \quad g(x_k) + J_g(x_k) p \le 0
\end{align*}
$$
必须强调，这个QP子问题的解 $p_k$ 并不是原始NL[P问题](@entry_id:267898)的最终解。它仅仅是在当前点 $x_k$ 附近，基于局部模型计算出的一个最优**搜索方向**。SQP算法是一个迭代过程，在得到 $p_k$ 后，通常还需要一个[全局化策略](@entry_id:177837)（如线搜索或[信赖域方法](@entry_id:138393)）来确定一个合适的步长 $\alpha_k$，从而计算出下一个迭代点 $x_{k+1} = x_k + \alpha_k p_k$。因此，QP求解器在整个SQP框架中扮演的是一个计算核心步骤的子程序角色 [@problem_id:219997]。

### 求解二次规划子问题：[KKT系统](@entry_id:751047)

一旦QP子问题被构建，我们便可以利用标准的优化理论来求解它。对于一个有约束的[优化问题](@entry_id:266749)，其最优解必须满足[Karush-Kuhn-Tucker](@entry_id:634966)（KKT）条件。QP子问题的目标函数是二次的，约束是线性的，这使得其[KKT条件](@entry_id:185881)构成一个相对容易求解的系统。

为简化讨论，我们考虑一个仅含[等式约束](@entry_id:175290)的QP子问题。其[拉格朗日函数](@entry_id:174593)为：
$$
\mathcal{L}_{QP}(p, \lambda_{k+1}) = \left( \nabla f(x_k)^T p + \frac{1}{2} p^T B_k p \right) + \lambda_{k+1}^T (c(x_k) + J_c(x_k) p)
$$
其中 $\lambda_{k+1}$ 是QP子问题线性约束对应的[拉格朗日乘子](@entry_id:142696)。其一阶[KKT条件](@entry_id:185881)（原始可行性和对偶可行性/梯度为零）为：
$$
\begin{align*}
B_k p + \nabla f(x_k) + J_c(x_k)^T \lambda_{k+1} = 0 \\
c(x_k) + J_c(x_k) p = 0
\end{align*}
$$
这是一个关于变量 $p$ 和 $\lambda_{k+1}$ 的线性方程组，可以写成矩阵形式：
$$
\begin{pmatrix} B_k & J_c(x_k)^T \\ J_c(x_k) & 0 \end{pmatrix} \begin{pmatrix} p \\ \lambda_{k+1} \end{pmatrix} = \begin{pmatrix} -\nabla f(x_k) \\ -c(x_k) \end{pmatrix}
$$
通过求解这个线性系统，我们便可以同时得到搜索方向 $p_k$ 和下一轮迭代的拉格朗日乘子估计值 $\lambda_{k+1}$。

**示例：求解一个QP子问题**

让我们通过一个具体的例子来演示这个过程 [@problem_id:2202023]。考虑问题：
$$
\begin{align*}
\text{Minimize}  \quad f(x_1, x_2) = x_1 + x_2^2 \\
\text{Subject to}  \quad c(x_1, x_2) = (x_1-1)^2 + x_2^2 - 1 = 0
\end{align*}
$$
假设当前迭代点为 $x_0 = (1, 1)$，并使用[单位矩阵](@entry_id:156724) $B_0 = I$ 作为Hessian近似。

1.  **计算所需导数和函数值**:
    在 $x_0=(1,1)$ 处，我们有：
    $c(x_0) = (1-1)^2 + 1^2 - 1 = 0$
    $\nabla f(x) = \begin{pmatrix} 1 \\ 2x_2 \end{pmatrix} \Rightarrow \nabla f(x_0) = \begin{pmatrix} 1 \\ 2 \end{pmatrix}$
    $\nabla c(x) = \begin{pmatrix} 2(x_1-1) \\ 2x_2 \end{pmatrix} \Rightarrow \nabla c(x_0) = \begin{pmatrix} 0 \\ 2 \end{pmatrix}$

2.  **构建并求解[KKT系统](@entry_id:751047)**:
    QP子问题的[KKT系统](@entry_id:751047)为：
    $$
    \begin{pmatrix} 1 & 0 & 0 \\ 0 & 1 & 2 \\ 0 & 2 & 0 \end{pmatrix} \begin{pmatrix} p_1 \\ p_2 \\ \lambda_1 \end{pmatrix} = \begin{pmatrix} -1 \\ -2 \\ 0 \end{pmatrix}
    $$
    从第三行我们得到 $2p_2=0 \Rightarrow p_2=0$。
    代入第一行，我们得到 $p_1 = -1$。
    代入第二行，我们得到 $p_2 + 2\lambda_1 = -2 \Rightarrow 0 + 2\lambda_1 = -2 \Rightarrow \lambda_1 = -1$。

因此，求解该QP子问题得到搜索方向 $p = \begin{pmatrix} -1 \\ 0 \end{pmatrix}$ [@problem_id:2202023] [@problem_id:2183102]。同时，我们还得到了新的拉格朗日乘子估计值为 $\lambda_1 = -1$。

这个例子清晰地表明，QP子问题的解不仅提供了 primal 变量的更新方向 $p_k$，也自然地给出了 dual 变量（拉格朗日乘子）的更新 $\lambda_{k+1}$ [@problem_id:2202012]。如果我们已经知道了步长 $p_k$，我们可以直接从KKT的第一个方程 $B_k p_k + \nabla f(x_k) + J_c(x_k)^T \lambda_{k+1} = 0$ 来反解 $\lambda_{k+1}$。例如，在另一个问题中，给定 $x_k = (2,2)^T$, $p_k = (-2.2, -0.4)^T$, $B_k=I$，以及 $\nabla f(x_k) = (4,4)^T$ 和 $\nabla c(x_k)=(1,2)^T$，我们可以建立方程：
$$
\begin{pmatrix} 1 & 0 \\ 0 & 1 \end{pmatrix} \begin{pmatrix} -2.2 \\ -0.4 \end{pmatrix} + \begin{pmatrix} 4 \\ 4 \end{pmatrix} + \lambda_{k+1} \begin{pmatrix} 1 \\ 2 \end{pmatrix} = \begin{pmatrix} 0 \\ 0 \end{pmatrix}
$$
该[方程组](@entry_id:193238)的解为 $\lambda_{k+1} = -1.8$ [@problem_id:2202012]。

### 理论基础：与牛顿法的联系

SQP方法之所以如此高效，尤其是在解的邻域内，是因为它与[求解非线性方程](@entry_id:177343)组的[牛顿法](@entry_id:140116)有着深刻的联系。这种联系揭示了SQP方法的理论根基。

原始NL[P问题](@entry_id:267898)的最优解 $(x^*, \lambda^*)$ 必须满足其[KKT条件](@entry_id:185881)。对于一个仅含[等式约束](@entry_id:175290)的问题，[KKT条件](@entry_id:185881)构成一个[非线性方程组](@entry_id:178110)：
$$
F(x, \lambda) = \begin{pmatrix} \nabla f(x) + J_c(x)^T \lambda \\ c(x) \end{pmatrix} = 0
$$
我们可以应用[牛顿法](@entry_id:140116)来求解这个关于变量 $(x, \lambda)$ 的[方程组](@entry_id:193238)。在当前点 $(x_k, \lambda_k)$，[牛顿法](@entry_id:140116)通过求解一个[线性系统](@entry_id:147850)来计算更新步长 $(\Delta x, \Delta \lambda)$:
$$
J_F(x_k, \lambda_k) \begin{pmatrix} \Delta x \\ \Delta \lambda \end{pmatrix} = -F(x_k, \lambda_k)
$$
其中 $J_F$ 是 $F(x, \lambda)$ 的雅可比矩阵。经过计算，该[雅可比矩阵](@entry_id:264467)为：
$$
J_F(x, \lambda) = \begin{pmatrix} \nabla_{xx}^2 \mathcal{L}(x, \lambda) & J_c(x)^T \\ J_c(x) & 0 \end{pmatrix}
$$
其中 $\nabla_{xx}^2 \mathcal{L}(x, \lambda)$ 是[拉格朗日函数](@entry_id:174593)的Hessian矩阵。因此，[牛顿步](@entry_id:177069) $(\Delta x, \Delta \lambda)$ 由以下[线性系统](@entry_id:147850)定义：
$$
\begin{pmatrix} \nabla_{xx}^2 \mathcal{L}_k & J_{c,k}^T \\ J_{c,k} & 0 \end{pmatrix} \begin{pmatrix} \Delta x \\ \Delta \lambda \end{pmatrix} = -\begin{pmatrix} \nabla_x \mathcal{L}_k \\ c_k \end{pmatrix}
$$
如果我们定义 $\lambda_{k+1} = \lambda_k + \Delta \lambda$，并令 $\Delta x = p$，上述系统可以重写为：
$$
\begin{pmatrix} \nabla_{xx}^2 \mathcal{L}_k & J_{c,k}^T \\ J_{c,k} & 0 \end{pmatrix} \begin{pmatrix} p \\ \lambda_{k+1} \end{pmatrix} = \begin{pmatrix} J_{c,k}^T \lambda_k - \nabla_x \mathcal{L}_k \\ -c_k \end{pmatrix} = \begin{pmatrix} -\nabla f_k \\ -c_k \end{pmatrix}
$$
这个系统与我们之[前推](@entry_id:158718)导出的QP子问题的[KKT系统](@entry_id:751047)是完全相同的，前提是我们选择QP的Hessian近似 $B_k$ 为[拉格朗日函数](@entry_id:174593)的**精确Hessian矩阵** $\nabla_{xx}^2 \mathcal{L}(x_k, \lambda_k)$ [@problem_id:2407307]。

这一重要的等价性告诉我们：当使用精确的二阶信息时，SQP方法本质上是在对原始问题的[KKT条件](@entry_id:185881)应用牛顿法。这解释了为什么SQP方法在理想条件下（如解的邻域内，[正则性条件](@entry_id:166962)满足）能够实现二次收敛——这是牛顿法的标志性特征。当使用[拟牛顿法](@entry_id:138962)（Quasi-Newton methods）来近似 $B_k$ 时，算法通常能实现[超线性收敛](@entry_id:141654)。

### 子问题的高级议题与稳健性

尽管SQP的理论基础坚实，但在实际应用中，QP子问题本身可能面临一些挑战。一个稳健的SQP算法必须能够妥善处理这些情况。

#### 可行性问题

SQP算法的一个基本假设是，在每一步迭代中，我们都能够成功求解QP子问题。然而，QP子问题的[可行域](@entry_id:136622)，即满足线性化约束的步长 $p$ 的集合，可能为空。这意味着QP子问题是**不可行的**（infeasible）。

例如，考虑在点 $x_0 = (0,0)$ 处，对两个非[线性[不等](@entry_id:174297)式约束](@entry_id:176084)进行线性化，得到如下关于步长 $p=(p_1, p_2)$ 的约束 [@problem_id:2202038]：
$$
\begin{align*}
-1 + p_2 \ge 0 \quad \Rightarrow \quad p_2 \ge 1 \\
-1 - p_2 \ge 0 \quad \Rightarrow \quad p_2 \le -1
\end{align*}
$$
这两个条件显然是相互矛盾的，不存在任何 $p_2$ 能同时满足它们。因此，这个QP子问题没有可行解，标准的SQP迭代在此处会失败。这种情况在迭代点距离原始问题的[可行域](@entry_id:136622)较远时，或者当约束的几何形状比较“扭曲”时，都可能发生。

为了确保QP子问题至少是可行的，原始问题的约束需要满足一定的**[约束规范](@entry_id:635836)性条件**（Constraint Qualifications, CQs）。这些是关于在可行点处[有效约束](@entry_id:635234)（active constraints）梯度行为的数学条件。
*   **[线性无关约束规范](@entry_id:634117)（LICQ）**：要求在某点所有[有效约束](@entry_id:635234)的[梯度向量](@entry_id:141180)是[线性无关](@entry_id:148207)的。这是一个较强的条件。
*   **Mangasarian-Fromovitz[约束规范](@entry_id:635836)（MFCQ）**：要求[等式约束](@entry_id:175290)的梯度线性无关，并且存在一个方向 $d$，它严格下降所有[有效不等式](@entry_id:170492)约束，同时与[等式约束](@entry_id:175290)梯度正交。

LICQ是比MFCQ更强的条件，即LICQ成立则MFCQ一定成立 [@problem_id:3169637]。MFCQ的一个重要作用是，如果它在点 $x_k$ 成立，那么在该点构建的QP子问题的线性化[约束系统](@entry_id:164587)是可行的。例如，对于约束 $g_1(x)=x_1\le 0$ 和 $g_2(x)=2x_1\le 0$，在原点 $(0,0)$，两个约束的梯度分别为 $(1,0)^T$ 和 $(2,0)^T$，它们线性相关，违反了LICQ。但是，我们可以找到方向 $d=(-1,0)^T$ 使得 $\nabla g_1^T d  0$ 和 $\nabla g_2^T d  0$，因此MFCQ成立 [@problem_id:3169637]。在这种情况下，QP子问题的可行性仍然得到保证。

实践中，当QP子问题不可行时，算法通常会进入一个“可行性恢复”阶段，或者采用所谓的“弹性模式”，即通过引入[松弛变量](@entry_id:268374)并惩罚它们，来寻找一个尽可能减少约束违反的步长。

#### 曲率问题

另一个关键问题是QP子问题目标函数的**曲率**，由矩阵 $B_k$ 决定。如果 $B_k$ 是正定的，QP[目标函数](@entry_id:267263)就是严格凸的，子问题有唯一的全局最优解。然而，拉格朗日函数的Hessian矩阵 $\nabla_{xx}^2 \mathcal{L}$ 即使在最优点，也**不一定是正定的**。当原始问题包含非凸约束时，$\nabla_{xx}^2 \mathcal{L}$ 很可能是**不定**的（即同时有正负[特征值](@entry_id:154894)）。

例如，考虑在 $x_k=(1,0)$ 处，对一个具有凹陷边界的约束 $g(x)=-x_2^2+1-x_1 \le 0$ 进行分析 [@problem_id:3169634]。即使[目标函数](@entry_id:267263) $f(x)$ 是凸的，计算出的拉格朗日Hessian矩阵也可能是 $\nabla_{xx}^2 \mathcal{L}(x_k, \lambda_k) = \begin{pmatrix} 2  0 \\ 0  -1 \end{pmatrix}$，这是一个[不定矩阵](@entry_id:634961)。如果QP子问题的Hessian矩阵是不定的，而其约束又允许在负曲率方向上移动，那么子问题可能是无界的，算法同样会失败。

幸运的是，我们不需要 $B_k$ 在整个空间 $\mathbb{R}^n$ 上都是正定的。我们只需要保证在**线性化约束的[可行方向](@entry_id:635111)**上，曲率是非负的。具体来说，我们需要所谓的**曲率条件**成立：$d^T B_k d \ge 0$ 对于所有满足 $J_c(x_k)d=0$ 且 $J_{g_A}(x_k)d=0$ 的方向 $d$ 都成立（其中 $g_A$ 是QP子问题中的[有效不等式](@entry_id:170492)约束）。这个条件确保了QP在约束的切空间上是凸的，从而保证子问题有界 [@problem_id:2202016]。

如果这个条件不满足，例如在上例 [@problem_id:3169634] 中，在[切空间](@entry_id:199137)方向 $d=(0, d_2)^T$ 上，曲率为 $d^T B_k d = -d_2^2  0$，我们就必须对 $B_k$ 进行修正。一种常见的策略是向其增加一个正的对角项（类似于[Levenberg-Marquardt方法](@entry_id:635267)）：
$$
B_k(\tau) = B_k + \tau I, \quad \tau \ge 0
$$
我们需要找到最小的 $\tau$，使得修正后的矩阵 $B_k(\tau)$ 满足曲率条件。在上例中，我们需要 $d^T B_k(\tau) d = d_2^2(-1+\tau) \ge 0$，这要求 $\tau \ge 1$。因此，通过将 $B_k$ 修正为 $B_k(1)$，我们就可以确保QP子问题是良定义的。

另一种流行的策略是使用拟牛顿更新（如BFGS），它通过迭代的方式构造一个始终保持正定的Hessian近似矩阵 $B_k$，从而从根本上避免了处理不定性的复杂性，并依然能获得快速的收敛。

综上所述，二次规划子问题是SQP方法的心脏。理解其构建原理、求解机制，以及如何处理可能出现的可行性和曲率问题，对于掌握SQP算法并成功应用于实际问题至关重要。