## 引言
在现代数据科学、机器学习和工程领域，我们面临的许多核心问题都可以被归结为[优化问题](@entry_id:266749)。特别是一类被称为“[复合优化](@entry_id:165215)”的问题尤为普遍，其[目标函数](@entry_id:267263)通常由两部分组成：一个代表[数据拟合](@entry_id:149007)优度的光滑项（如最小二乘损失），以及一个施加期望结构（如稀疏性或低秩性）的非光滑正则项。这种结构在构建可解释、鲁棒且能有效[防止过拟合](@entry_id:635166)的模型时至关重要。然而，正则项的非光滑性使得标准的梯度下降法在此失效，因为它依赖于目标函数处处可微的假设。这就引出了一个核心挑战：我们如何才能高效、稳定地求解这类包含非光滑成分的[优化问题](@entry_id:266749)？

邻近梯度法（Proximal Gradient Method）为解决这一挑战提供了一个优雅而强大的框架。它并非试图直接处理整个复杂的[非光滑函数](@entry_id:175189)，而是巧妙地将光滑部分与非光滑部分“分而治之”。本文将系统地引导读者深入理解这一重要算法。

- 在“**原理与机制**”一章中，我们将首先剖析非光滑性带来的困难，然后引入邻近梯度法的核心构件——邻近算子，并详细阐述算法的迭代步骤。我们还将从多种理论视角（如代理函数、[算子分裂](@entry_id:634210)）来诠释该方法，并探讨其收敛的理论保证。

- 接着，在“**应用与[交叉](@entry_id:147634)学科联系**”一章中，我们将展示该方法如何从理论走向实践，成为解决各类实际问题的关键工具。从统计学中的LASSO[稀疏回归](@entry_id:276495)，到[推荐系统](@entry_id:172804)中的[矩阵补全](@entry_id:172040)，再到信号处理和计算生物学中的具体案例，你将看到邻近梯度法作为一种通用技术所展现出的惊人适应性。

- 最后，“**动手实践**”部分提供了一系列精心设计的编程练习，让你有机会亲手实现和应用邻近梯度法，将理论知识转化为解决实际问题的能力。

通过本次学习，你将不仅掌握一个具体的[优化算法](@entry_id:147840)，更将领会一种处理复杂[优化问题](@entry_id:266749)的核心思想，为你未来在相关领域的研究与实践打下坚实的基础。

## 原理与机制

在优化理论与实践中，我们经常遇到需要最小化形如 $F(\mathbf{x}) = f(\mathbf{x}) + g(\mathbf{x})$ 的复合目标函数。其中，$f(\mathbf{x})$ 是一个光滑、可微的[凸函数](@entry_id:143075)，通常代表[数据拟合](@entry_id:149007)项或损失函数；而 $g(\mathbf{x})$ 是一个[凸函数](@entry_id:143075)，但可能是非光滑、不可微的，通常用作正则化项以引入先验知识，如稀疏性或低秩性。本章将深入探讨解决此类问题的核心算法——邻近梯度法（Proximal Gradient Method）的原理与机制。

### 非光滑性带来的挑战

对于光滑函数的[无约束优化](@entry_id:137083)问题 $\min f(\mathbf{x})$，标准的[梯度下降法](@entry_id:637322)是一种行之有效的方法，其迭代格式为 $\mathbf{x}_{k+1} = \mathbf{x}_k - \gamma \nabla f(\mathbf{x}_k)$，其中 $\gamma > 0$ 是步长。一个自然的想法是，能否将此方法直接应用于复合[目标函数](@entry_id:267263) $F(\mathbf{x})$，即采用 $\mathbf{x}_{k+1} = \mathbf{x}_k - \gamma \nabla F(\mathbf{x}_k) = \mathbf{x}_k - \gamma (\nabla f(\mathbf{x}_k) + \nabla g(\mathbf{x}_k))$ 的形式。

然而，这种直接的推广会遇到一个根本性的理论障碍：当 $g(\mathbf{x})$ 非光滑时，其梯度 $\nabla g(\mathbf{x})$ 可能在某些点上不存在。一个典型的例子是机器学习和统计学中广泛应用的 [LASSO](@entry_id:751223) (Least Absolute Shrinkage and Selection Operator) 问题，其目标函数为 $F(\mathbf{x}) = f(\mathbf{x}) + \lambda \|\mathbf{x}\|_1$，其中 $f(\mathbf{x})$ 通常是最小二乘损失，而 $g(\mathbf{x}) = \lambda \|\mathbf{x}\|_1$ 是 L1 范数正则化项。L1 范数 $\|\mathbf{x}\|_1 = \sum_i |x_i|$ 在任何一个分量 $x_i = 0$ 的点上都是不可微的。问题恰恰在于，L1 正则化的目的正是为了诱导稀疏解，即产生许多分量为零的解。因此，在迭代过程中，算法的评估点很可能会遇到或穿过这些不可微的点，导致标准梯度 $\nabla F(\mathbf{x})$ 未定义，从而使得梯度下降法在理论上失效，在实践中也无法稳定执行 [@problem_id:2195141]。

虽然我们可以使用次梯度（subgradient）的概念来处理非光滑项，即 $0 \in \nabla f(\mathbf{x}^*) + \partial g(\mathbf{x}^*)$，并构造[次梯度](@entry_id:142710)方法，但这类方法通常收敛速度较慢。邻近梯度法则提供了一种更高效、更稳定的替代方案，它巧妙地将光滑部分与非光滑部分分离开来处理。

### 邻近算子：一个关键的构造模块

邻近梯度法的核心思想在于，不对整个复合函数 $F(\mathbf{x})$ 进行梯度下降，而是将迭代过程分解为两个步骤：一个针对光滑部分 $f(\mathbf{x})$ 的显式梯度步骤，和一个针对非光滑部分 $g(\mathbf{x})$ 的隐式“校正”步骤。这个校正步骤是通过一个称为**邻近算子（proximal operator）**的工具来实现的。

对于一个闭、正常、[凸函数](@entry_id:143075) $g: \mathbb{R}^n \to \mathbb{R} \cup \{+\infty\}$ 和一个参数 $t > 0$，其邻近算子 $\text{prox}_{tg}$ 在点 $\mathbf{x}$ 的定义为：
$$
\text{prox}_{tg}(\mathbf{x}) = \arg\min_{\mathbf{u} \in \mathbb{R}^n} \left( g(\mathbf{u}) + \frac{1}{2t} \|\mathbf{u} - \mathbf{x}\|_2^2 \right)
$$
这个定义蕴含了深刻的直观意义。$\arg\min$ 中的[目标函数](@entry_id:267263)由两部分构成：$g(\mathbf{u})$ 和 $\frac{1}{2t} \|\mathbf{u} - \mathbf{x}\|_2^2$。前者驱使解 $\mathbf{u}$ 向着使 $g$ 值更小的方向移动；而后者是一个二次惩罚项，它惩罚 $\mathbf{u}$ 与输入点 $\mathbf{x}$ 之间的距离。因此，邻近算子的输出 $\text{prox}_{tg}(\mathbf{x})$ 是一个在“最小化 $g$”和“保持离 $\mathbf{x}$ 足够近”这两个目标之间进行权衡的最优解 [@problem_id:2195134]。

参数 $t$ 控制着这种权衡的力度。较小的 $t$ 意味着 $\frac{1}{2t}$ 较大，对距离的惩罚更重，从而使得输出更接近输入 $\mathbf{x}$；反之，较大的 $t$ 则允许输出 $\mathbf{u}$ 为了最小化 $g$ 而离 $\mathbf{x}$ 更远。

一个至关重要的性质是，即使 $g(\mathbf{u})$ 是非光滑的，定义邻近算子的子问题中的目标函数 $g(\mathbf{u}) + \frac{1}{2t} \|\mathbf{u} - \mathbf{x}\|_2^2$ 也是一个强[凸函数](@entry_id:143075)（因为它是[凸函数](@entry_id:143075)与强凸函数的和）。这保证了对于任意输入 $\mathbf{x}$，邻近算子的解都存在且唯一，使其成为一个定义良好且稳定的算子。

### 邻近梯度法算法

有了邻近算子这一工具，我们便可以构建邻近梯度法。该算法的迭代更新规则如下：
$$
\mathbf{x}_{k+1} = \text{prox}_{\gamma g}(\mathbf{x}_k - \gamma \nabla f(\mathbf{x}_k))
$$
其中 $\gamma > 0$ 是一个固定的步长。

我们可以将这一迭代过程分解为两个概念清晰的步骤：

1.  **[梯度下降](@entry_id:145942)步骤 (Forward Step)**: 计算 $\mathbf{v}_k = \mathbf{x}_k - \gamma \nabla f(\mathbf{x}_k)$。这一步完全忽略了非光滑项 $g$，只对光滑项 $f$ 执行一次标准的[梯度下降](@entry_id:145942)。

2.  **邻近映射步骤 (Backward Step)**: 计算 $\mathbf{x}_{k+1} = \text{prox}_{\gamma g}(\mathbf{v}_k)$。这一步将前一步的结果 $\mathbf{v}_k$ 作为输入，通过邻近算子进行“校正”或“去噪”，以满足由非光滑项 $g$ 所施加的结构（如稀疏性）。

让我们通过一个具体的 LASSO 问题来演示这个过程 [@problem_id:2163980]。考虑最小化 $J(\mathbf{w}) = \frac{1}{2} \|\mathbf{X}\mathbf{w} - \mathbf{y}\|_2^2 + \lambda \|\mathbf{w}\|_1$。这里，$f(\mathbf{w}) = \frac{1}{2} \|\mathbf{X}\mathbf{w} - \mathbf{y}\|_2^2$，$g(\mathbf{w}) = \lambda \|\mathbf{w}\|_1$。对于 L1 范数，$g(\mathbf{w}) = \lambda \|\mathbf{w}\|_1$ 的邻近算子有一个解析形式，称为**[软阈值算子](@entry_id:755010) (soft-thresholding operator)** $S_{\tau}$，其对向量的每个分量独立作用：
$$
(\text{prox}_{\tau \|\cdot\|_1}(\mathbf{v}))_i = S_{\tau}(v_i) = \text{sign}(v_i) \max(|v_i| - \tau, 0)
$$
假设给定数据 $\mathbf{X} = \begin{pmatrix} 1  1 \\ 1  -1 \end{pmatrix}$，$\mathbf{y} = \begin{pmatrix} 5 \\ 1 \end{pmatrix}$，参数 $\lambda = 1$，步长 $\gamma = 0.5$，并从初始点 $\mathbf{w}_0 = \begin{pmatrix} 2 \\ 3 \end{pmatrix}$ 开始。

1.  **[梯度下降](@entry_id:145942)步骤**:
    首先计算 $f$ 在 $\mathbf{w}_0$ 处的梯度：$\nabla f(\mathbf{w}) = \mathbf{X}^T(\mathbf{X}\mathbf{w} - \mathbf{y})$。
    $\nabla f(\mathbf{w}_0) = \begin{pmatrix} 1  1 \\ 1  -1 \end{pmatrix} \left( \begin{pmatrix} 1  1 \\ 1  -1 \end{pmatrix} \begin{pmatrix} 2 \\ 3 \end{pmatrix} - \begin{pmatrix} 5 \\ 1 \end{pmatrix} \right) = \begin{pmatrix} -2 \\ 2 \end{pmatrix}$。
    然后执行[梯度下降](@entry_id:145942)：$\mathbf{v}_0 = \mathbf{w}_0 - \gamma \nabla f(\mathbf{w}_0) = \begin{pmatrix} 2 \\ 3 \end{pmatrix} - 0.5 \begin{pmatrix} -2 \\ 2 \end{pmatrix} = \begin{pmatrix} 3 \\ 2 \end{pmatrix}$。

2.  **邻近映射步骤**:
    应用[软阈值算子](@entry_id:755010)，阈值为 $\tau = \gamma \lambda = 0.5 \times 1 = 0.5$。
    $\mathbf{w}_1 = \text{prox}_{0.5 g}(\mathbf{v}_0) = S_{0.5}(\mathbf{v}_0) = \begin{pmatrix} \text{sign}(3) \max(|3| - 0.5, 0) \\ \text{sign}(2) \max(|2| - 0.5, 0) \end{pmatrix} = \begin{pmatrix} 2.5 \\ 1.5 \end{pmatrix}$。

经过一次迭代，解从 $\begin{pmatrix} 2 \\ 3 \end{pmatrix}$ 更新到了 $\begin{pmatrix} 2.5 \\ 1.5 \end{pmatrix}$。这个简单的例子清晰地展示了算法的执行机制。

### 诠释与关联

邻近梯度法之所以强大，不仅在于其有效性，还在于它可以从多个角度进行理解，并与其他重要的优化算法建立联系。

#### 与梯度下降的联系

邻近梯度法是标准梯度下降法的一种自然推广。考虑一个特殊情况，即非光滑部分 $g(\mathbf{x})$ 为零函数，$g(\mathbf{x}) = 0$。此时，邻近算子的定义变为：
$$
\text{prox}_{\gamma \cdot 0}(\mathbf{v}) = \arg\min_{\mathbf{u}} \left( 0 + \frac{1}{2\gamma} \|\mathbf{u} - \mathbf{v}\|_2^2 \right) = \mathbf{v}
$$
这意味着当 $g(\mathbf{x}) = 0$ 时，邻近算子是[恒等映射](@entry_id:634191)。代入邻近梯度法的更新公式，我们得到：
$$
\mathbf{x}_{k+1} = \text{prox}_{\gamma \cdot 0}(\mathbf{x}_k - \gamma \nabla f(\mathbf{x}_k)) = \mathbf{x}_k - \gamma \nabla f(\mathbf{x}_k)
$$
这正是标准[梯度下降法](@entry_id:637322)的迭代格式 [@problem_id:2195150]。因此，我们可以将[梯度下降法](@entry_id:637322)视为邻近梯度法在非光滑项消失时的特例。

#### 与[约束优化](@entry_id:635027)的联系：[投影梯度法](@entry_id:169354)

另一个重要的特例是当 $g(\mathbf{x})$ 是一个闭[凸集](@entry_id:155617) $C$ 的**指示函数 (indicator function)** 时。[指示函数](@entry_id:186820) $I_C(\mathbf{x})$ 定义为：
$$
I_C(\mathbf{x}) = \begin{cases} 0  \text{if } \mathbf{x} \in C \\ +\infty  \text{if } \mathbf{x} \notin C \end{cases}
$$
此时，邻近算子的定义变为：
$$
\text{prox}_{I_C}(\mathbf{v}) = \arg\min_{\mathbf{u}} \left( I_C(\mathbf{u}) + \frac{1}{2} \|\mathbf{u} - \mathbf{v}\|_2^2 \right) = \arg\min_{\mathbf{u} \in C} \frac{1}{2} \|\mathbf{u} - \mathbf{v}\|_2^2
$$
这个子问题正是寻找集合 $C$ 中离点 $\mathbf{v}$ 最近的点，其解即为 $\mathbf{v}$ 在集合 $C$ 上的**欧几里得投影 (Euclidean projection)**，记为 $P_C(\mathbf{v})$ [@problem_id:2195157]。例如，若 $C$ 是非负象限 $\mathbb{R}^n_+$，则投影操作就是将所有负分量置为零。

在这种情况下，邻近梯度法的迭代就变成了**[投影梯度法](@entry_id:169354) (Projected Gradient Method)**：
$$
\mathbf{x}_{k+1} = P_C(\mathbf{x}_k - \gamma \nabla f(\mathbf{x}_k))
$$
该算法首先在整个空间上沿负梯度方向移动，然后将结果投影回可行集 $C$。这揭示了邻近梯度法与约束优化之间的深刻联系。

#### 代理目标函数诠释

邻近梯度法的每一步迭代都可以被看作是对一个**代理[目标函数](@entry_id:267263) (surrogate objective function)** 的精确最小化。在当前点 $\mathbf{x}_k$，我们可以用一个二次函数来近似光滑部分 $f(\mathbf{x})$。具体来说，我们使用 $f$ 在 $\mathbf{x}_k$ 处的一阶泰勒展开，并添加一个二次的近端项：
$$
\hat{f}(\mathbf{x}; \mathbf{x}_k) = f(\mathbf{x}_k) + \langle \nabla f(\mathbf{x}_k), \mathbf{x} - \mathbf{x}_k \rangle + \frac{1}{2\gamma} \|\mathbf{x} - \mathbf{x}_k\|_2^2
$$
这个近似 $\hat{f}$ 构成了原函数 $F(\mathbf{x})$ 在 $\mathbf{x}_k$ 点的代理函数 $\hat{F}(\mathbf{x}; \mathbf{x}_k) = \hat{f}(\mathbf{x}; \mathbf{x}_k) + g(\mathbf{x})$。邻近梯度法的下一步迭代点 $\mathbf{x}_{k+1}$ 正是这个代理函数的最小化者：
$$
\mathbf{x}_{k+1} = \arg\min_{\mathbf{x}} \hat{F}(\mathbf{x}; \mathbf{x}_k) = \arg\min_{\mathbf{x}} \left( g(\mathbf{x}) + f(\mathbf{x}_k) + \langle \nabla f(\mathbf{x}_k), \mathbf{x} - \mathbf{x}_k \rangle + \frac{1}{2\gamma} \|\mathbf{x} - \mathbf{x}_k\|_2^2 \right)
$$
通过对上式中的二次项进行配方，可以证明这个最小化问题等价于邻近梯度法的更新公式 [@problem_id:2195125]。这一诠释非常重要，因为它表明算法在每一步都是在最小化一个原目标函数的（局部）上界模型，从而为算法的下降性质和收敛性提供了直观的解释。

#### 前向-后向分裂诠释

从更抽象的[算子理论](@entry_id:139990)角度看，邻近梯度法是**前向-后向分裂 (Forward-Backward Splitting)** 算法的一个实例。[优化问题](@entry_id:266749) $\min f(\mathbf{x}) + g(\mathbf{x})$ 的[一阶最优性条件](@entry_id:634945)是找到一个点 $\mathbf{x}^*$ 使得 $0 \in \nabla f(\mathbf{x}^*) + \partial g(\mathbf{x}^*)$，其中 $\partial g$ 是 $g$ 的[次微分](@entry_id:175641)。这等价于求解算子包含问题：寻找 $\mathbf{x}^*$ 使得 $\mathbf{x}^* \in (\text{Id} + \gamma(\nabla f + \partial g))(\mathbf{x}^*)$。

前向-后向分裂算法将算子 $\nabla f + \partial g$ 分裂开来处理。令 $A = \nabla f$ 和 $B = \partial g$。算法的迭代格式为：
$$
\mathbf{x}_{k+1} = (I + \gamma B)^{-1} (I - \gamma A)(\mathbf{x}_k)
$$
其中 $(I - \gamma A)$ 对应于[梯度下降](@entry_id:145942)（前向步骤），而 $(I + \gamma B)^{-1}$ 称为 $B$ 的**[预解算子](@entry_id:271964) (resolvent operator)**。当 $B$ 是一个[凸函数](@entry_id:143075) $g$ 的[次微分](@entry_id:175641) $\partial g$ 时，其[预解算子](@entry_id:271964)恰好就是 $g$ 的邻近算子 $\text{prox}_{\gamma g}$ [@problem_id:2195126]。因此，前向-后向分裂的迭代式与邻近梯度法的迭代式完全相同。这种观点将邻近梯度法置于一个更广阔的[单调算子](@entry_id:637459)理论框架中，为分析其收敛性提供了强大的数学工具。

### 收敛性质

一个有效的[迭代算法](@entry_id:160288)必须具备良好的收敛保证。邻近梯度法在这方面有坚实的理论基础。

#### [不动点](@entry_id:156394)刻画

首先，我们需要明确算法的收敛目标是什么。一个点 $\mathbf{x}^*$ 是[复合优化](@entry_id:165215)问题 $\min f(\mathbf{x}) + g(\mathbf{x})$ 的解，当且仅当它满足[一阶最优性条件](@entry_id:634945) $0 \in \nabla f(\mathbf{x}^*) + \partial g(\mathbf{x}^*)$。这个条件可以等价地写为：
$$
\mathbf{x}^* - \gamma \nabla f(\mathbf{x}^*) \in \mathbf{x}^* + \gamma \partial g(\mathbf{x}^*) \iff \mathbf{x}^* - \gamma \nabla f(\mathbf{x}^*) \in (I + \gamma \partial g)(\mathbf{x}^*)
$$
两边同时作用[预解算子](@entry_id:271964) $(I + \gamma \partial g)^{-1} = \text{prox}_{\gamma g}$，我们得到：
$$
\text{prox}_{\gamma g}(\mathbf{x}^* - \gamma \nabla f(\mathbf{x}^*)) = \mathbf{x}^*
$$
这表明，一个点是[优化问题](@entry_id:266749)的解，当且仅当它是邻近梯度迭代算子的**[不动点](@entry_id:156394) (fixed point)** [@problem_id:2195144]。因此，算法的收敛过程可以看作是寻找这个迭代映射的[不动点](@entry_id:156394)的过程。例如，对于一维 LASSO 问题 $F(x) = \frac{1}{2}(ax - b)^2 + \lambda |x|$，在 $ab > \lambda$ 的条件下，其唯一解为 $x^* = \frac{ab - \lambda}{a^2}$。我们可以验证，这个解恰好满足[不动点方程](@entry_id:203270) $x^* = S_{\gamma \lambda}(x^* - \gamma (a^2x^* - ab))$。

#### [下降引理](@entry_id:636345)与单调性

邻近梯度法是一个下降算法，意味着在适当的条件下，[目标函数](@entry_id:267263)值在迭代过程中是单调不增的，即 $F(\mathbf{x}_{k+1}) \le F(\mathbf{x}_k)$。这是保证算法向着最小值前进的基本性质。只要步长 $\gamma$ 选择得当，就可以从代理函数解释中推导出这个下降性质 [@problem_id:2195107]。这个性质确保了算法不会发生[振荡](@entry_id:267781)或发散，而是稳定地向更优的解区域探索。

#### 收敛的步长条件

为了保证收敛，步长 $\gamma$ 的选择至关重要。一个关键的要求是，光滑部分 $f$ 的梯度 $\nabla f$ 是**Lipschitz 连续**的。这意味着存在一个常数 $L > 0$（称为 Lipschitz 常数），使得对于任意 $\mathbf{x}, \mathbf{y}$，都有 $\|\nabla f(\mathbf{x}) - \nabla f(\mathbf{y})\|_2 \le L \|\mathbf{x} - \mathbf{y}\|_2$。这个常数 $L$ 度量了梯度变化的最大速率。例如，对于二次函数 $f(\mathbf{w}) = \frac{1}{2}\mathbf{w}^T \mathbf{A} \mathbf{w} - \mathbf{b}^T \mathbf{w}$，其 Lipschitz 常数 $L$ 等于矩阵 $\mathbf{A}$ 的最大[特征值](@entry_id:154894) [@problem_id:2195136]。

对于具有 Lipschitz 常数为 $L$ 的 $\nabla f$，若采用固定的步长 $\gamma$，邻近梯度法的收敛性可以通过选择满足以下条件的步长来保证：
$$
0  \gamma  \frac{2}{L}
$$
通常在实践中，为了更稳健的收敛，会选择更保守的步长，如 $\gamma \le \frac{1}{L}$。这个条件确保了代理函数是原函数的一个[上界](@entry_id:274738)，从而保证了算法的下降性质和收敛性。

#### [稳态](@entry_id:182458)非扩[张性](@entry_id:141857)

收敛性证明的更深层次的数学原理来自于邻近算子的一个关键几何性质：**[稳态](@entry_id:182458)非扩[张性](@entry_id:141857) (firm non-expansiveness)**。一个算子 $T$ 被称为[稳态](@entry_id:182458)非扩张的，如果对于任意输入 $\mathbf{x}, \mathbf{y}$，都满足：
$$
\|T(\mathbf{x}) - T(\mathbf{y})\|_2^2 \le \langle \mathbf{x} - \mathbf{y}, T(\mathbf{x}) - T(\mathbf{y}) \rangle
$$
可以证明，任何闭、正常、凸函数 $g$ 的邻近算子 $\text{prox}_g$ 都具有这个性质 [@problem_id:2195116]。这个性质比普通的非扩[张性](@entry_id:141857)（$\|T(\mathbf{x}) - T(\mathbf{y})\|_2 \le \|\mathbf{x} - \mathbf{y}\|_2$）更强，它是证明[迭代算法](@entry_id:160288)（如邻近梯度法）收敛到[不动点](@entry_id:156394)的强大工具。结合步长条件，可以证明邻近梯度法的整个迭代算子是一个收缩映射或[平均算子](@entry_id:746605)，从而根据[巴拿赫不动点定理](@entry_id:146620)或相关的推广，保证了序列 $\{\mathbf{x}_k\}$ 会收敛到[优化问题](@entry_id:266749)的一个解。

综上所述，邻近梯度法通过邻近算子这一核心构件，巧妙地解决了[复合优化](@entry_id:165215)问题中的非光滑性挑战。它不仅具有清晰的算法结构和直观的物理解释，还拥有坚实的理论基础和收敛保证，使其成为现代优化、机器学习和信号处理领域中不可或缺的基础工具。