## 引言
在现代信号处理、机器学习和统计学中，许多核心问题都依赖于优化方法。然而，当我们为了促进稀疏性等期望的解结构而引入诸如 $\ell_1$ 范数的正则项时，传统微积分中的梯度概念便显得力不从心，因为这些目标函数往往在某些点上并不可微。这种非光滑性（non-smoothness）构成了一个关键的知识鸿沟：我们如何系统地分析和求解这类优化问题？

为此，本文深入探讨了凸分析中的核心工具——**次梯度 (subgradient)** 和**次微分 (subdifferential)**。它们是对梯度概念的精妙推广，为处理非光滑凸函数提供了坚实的理论基础。通过本文，读者将全面掌握这些概念。首先，在“原理与机制”章节中，我们将从定义和几何直觉出发，建立次梯度微积分的运算法则。接着，在“应用与交叉学科联系”章节中，我们将展示这些理论如何在LASSO、矩阵恢复以及机器学习等前沿领域中提供深刻的洞见。最后，通过“动手实践”环节，你将有机会运用所学知识解决具体的优化问题，从而巩固理解。

## 原理与机制

在凸优化领域，尤其是在处理如稀疏优化和压缩感知中常见的非平滑目标函数时，经典微积分中的梯度概念已不足以完全描述函数的局部性质。许多关键函数，例如 $\ell_1$ 范数，虽然是凸的，但在某些点上并不可微。为了克服这一局限性，凸分析理论引入了**次梯度 (subgradient)** 和**次微分 (subdifferential)** 的概念，它们是对梯度概念的精妙推广。本章将深入探讨这些核心概念的定义、几何解释、运算法则及其在优化问题中的关键应用。

### 基本概念：次梯度与次微分

我们从一个简单的问题开始：一个凸函数在不可微的点处，其局部行为是怎样的？以一维绝对值函数 $f(t) = |t|$ 为例，它在 $t=0$ 处不可微。然而，我们可以画出无数条通过点 $(0,0)$ 且始终位于函数图像下方的直线，例如 $y=kt$，其中斜率 $k$ 必须在 $[-1, 1]$ 区间内。这些直线的斜率集合，恰当地刻画了函数在不可微点处的“方向”信息。

#### 形式化定义

这个直观想法可以被精确地形式化。对于一个在 $\mathbb{R}^n$ 上定义的凸函数 $f: \mathbb{R}^n \to \mathbb{R}$，一个向量 $g \in \mathbb{R}^n$ 被称为 $f$ 在点 $x$ 处的**次梯度**，如果它满足以下**次梯度不等式**：
$$
f(y) \geq f(x) + g^{\top}(y - x), \quad \text{对所有 } y \in \mathbb{R}^n
$$
这个不等式意味着，由向量 $g$ 定义的、通过点 $(x, f(x))$ 的仿射函数（一个超平面）是 $f$ 的一个全局下支撑。

在点 $x$ 处所有次梯度的集合被称为 $f$ 在该点的**次微分**，记作 $\partial f(x)$。如果次微分集合 $\partial f(x)$ 非空，则称 $f$ 在 $x$ **可次微分 (subdifferentiable)**。对于定义在整个 $\mathbb{R}^n$ 上的凸函数，它在每一点都是可次微分的。

如果 $f$ 在点 $x$ 处可微，那么其次微分是一个单点集，仅包含其梯度 $\nabla f(x)$。因此，次微分是梯度概念的直接推广。

#### 几何解释

次梯度的概念与函数图像的几何形状密切相关。一个函数的**上镜图 (epigraph)** 定义为集合 $\operatorname{epi}(f) = \{ (x, t) \in \mathbb{R}^n \times \mathbb{R} : t \ge f(x) \}$。对于凸函数 $f$，其上镜图是一个凸集。

次梯度不等式 $f(y) \geq f(x) + g^{\top}(y - x)$ 可以重写为 $g^{\top}x - f(x) \ge g^{\top}y - f(y)$。这表明超平面 $H = \{ (z,t) : t = f(x) + g^{\top}(z-x) \}$ 是 $\operatorname{epi}(f)$ 在点 $(x, f(x))$ 处的一个**支撑超平面 (supporting hyperplane)**。向量 $(g, -1)$ 是该超平面的一个法向量。因此，次微分 $\partial f(x)$ 可以被视为所有支撑 $\operatorname{epi}(f)$ 于 $(x, f(x))$ 的非垂直超平面的“斜率”集合。[@problem_id:3483533]

#### 核心范例：$\ell_1$ 范数

$\ell_1$ 范数定义为 $\|x\|_1 = \sum_{i=1}^n |x_i|$，是稀疏优化中的核心。由于其可分性，它的次微分是其各个分量 $|x_i|$ 次微分的笛卡尔积。

我们首先分析一维绝对值函数 $h(t) = |t|$：
-   若 $t_0 > 0$，$h(t)$ 可微，其导数为 $1$。因此 $\partial h(t_0) = \{1\} = \{\operatorname{sign}(t_0)\}$。
-   若 $t_0  0$，$h(t)$ 可微，其导数为 $-1$。因此 $\partial h(t_0) = \{-1\} = \{\operatorname{sign}(t_0)\}$。
-   若 $t_0 = 0$，次梯度不等式为 $|t| \ge g \cdot t$。这对于所有 $t \in \mathbb{R}$ 成立的充要条件是 $g \in [-1, 1]$。因此 $\partial h(0) = [-1, 1]$。

推广到 $n$ 维的 $\ell_1$ 范数，其在点 $x^\star$ 的次微分 $\partial \|x^\star\|_1$ 由所有满足 $g_i \in \partial |x^\star_i|$ 的向量 $g$ 组成。我们可以根据 $x^\star$ 的**支撑集 (support set)** $S = \{i : x^\star_i \neq 0\}$ 来更清晰地描述这个集合。[@problem_id:3483523]

一个向量 $g \in \mathbb{R}^n$ 属于 $\partial \|x^\star\|_1$ 的充要条件是：
-   对于所有在支撑集内的索引 $i \in S$，我们有 $g_i = \operatorname{sign}(x^\star_i)$。
-   对于所有不在支撑集内的索引 $j \notin S$（即 $x^\star_j = 0$），我们有 $g_j \in [-1, 1]$，也即 $|g_j| \le 1$。

这揭示了关于 $\partial \|x^\star\|_1$ 的几个重要性质。首先，除非 $x^\star$ 的所有分量都非零（即 $S = \{1, \dots, n\}$），否则次微分不是一个单点集。例如，若 $x^\star$ 含有零分量，$\partial \|x^\star\|_1$ 将是一个包含无穷多个向量的集合（一个超立方体），因此 $\|x\|_1$ 在这种情况下是不可微的。[@problem_id:3483523]

其次，在原点 $x^\star = 0$ 处，支撑集 $S$ 为空。此时，对所有分量 $j$ 都有 $|g_j| \le 1$。这等价于 $\|g\|_\infty \le 1$，其中 $\|\cdot\|_\infty$ 是无穷范数（或最大范数）。因此，
$$
\partial \|0\|_1 = \{g \in \mathbb{R}^n : \|g\|_\infty \le 1\}
$$
这个集合是与 $\ell_1$ 范数单位球对偶的 $\ell_\infty$ 范数**单位球**，而不是单位球面。[@problem_id:3483523]

### 次微分的运算法则

为了将次梯度应用于复杂的函数，我们需要一套运算法则，类似于普通微积分中的求和、链式法则等。

-   **非负数乘：** 对于 $\alpha > 0$，$\partial (\alpha f)(x) = \alpha \, \partial f(x)$。
-   **求和法则：** 对于两个凸函数 $f_1$ 和 $f_2$，其次微分的和是它们各自次微分的**闵可夫斯基和 (Minkowski sum)**：
    $$
    \partial(f_1 + f_2)(x) = \partial f_1(x) + \partial f_2(x) = \{g_1 + g_2 : g_1 \in \partial f_1(x), g_2 \in \partial f_2(x)\}
    $$
    此法则成立需要满足一个**正则性条件 (regularity condition)**，例如，其中一个函数在另一个函数定义域的相对内部 (relative interior) 中是连续的。在稀疏优化中，我们遇到的函数（如范数、二次函数）通常在整个空间 $\mathbb{R}^n$ 上连续，因此该法则广泛适用。[@problem_id:3483533]

    作为一个例子，考虑函数 $f(x) = \lambda \|x\|_1 + \frac{\gamma}{2}\|x\|_2^2$，其中 $\lambda, \gamma > 0$。第一项是 $\ell_1$ 范数，第二项是光滑的二次函数。在任意点 $x^\star$，$\frac{\gamma}{2}\|x\|_2^2$ 的次微分是其梯度 $\{\gamma x^\star\}$。因此，根据求和法则：
    $$
    \partial f(x^\star) = \lambda \, \partial \|x^\star\|_1 + \{\gamma x^\star\}
    $$
    这个集合的几何形状是 $\lambda \, \partial \|x^\star\|_1$（一个以原点为中心的超立方体）平移向量 $\gamma x^\star$ 后的结果。平移不改变集合的几何尺寸，例如，该集合的欧几里得直径仅由 $\ell_1$ 部分决定。具体来说，如果 $x^\star$ 有 $m$ 个零分量，则该次微分集合的直径为 $2\lambda\sqrt{m}$。[@problem_id:3483574]

-   **仿射复合链式法则：** 考虑复合函数 $f(x) = h(Ax-b)$，其中 $h$ 是凸函数，$A$ 是矩阵，$b$ 是向量。其次微分由下式给出：
    $$
    \partial f(x) = A^{\top} \partial h(Ax-b) = \{A^{\top}g : g \in \partial h(Ax-b)\}
    $$
    这个法则是分析许多机器学习和信号处理模型的基础，在这些模型中，数据通常经过线性变换。例如，对于函数 $f(x) = \|Ax\|_1$，其次微分是 $\partial f(x) = A^{\top} \partial \|Ax\|_1$。[@problem_id:3483553]

通过组合这些基本法则，我们可以计算更复杂的目标函数的次微分。考虑一个综合性的例子 [@problem_id:3483536]：
$$
f(x) = \mu\|Ax - b\|_2 + \frac{1}{2}\|Fx - c\|_2^2 + \lambda\|x\|_1 + \iota_B(x)
$$
其中 $\iota_B(x)$ 是一个凸集 $B$ 的示性函数。在 $B$ 的内部一点 $\bar{x}$，$\partial \iota_B(\bar{x}) = \{0\}$。函数 $f$ 的次微分是四个部分次微分的闵可夫斯基和。我们可以通过对每一项分别应用适当的法则（梯度、链式法则、$\ell_1$ 次微分）来计算出一个次梯度。

### 优化中的次梯度

次梯度理论的真正威力在于它为非光滑凸优化问题提供了最优性条件。

#### 费马最优性条件

对于一个凸函数 $f$，点 $x^\star$ 是其全局最小值的充要条件是**零向量**属于其在该点的次微分：
$$
0 \in \partial f(x^\star)
$$
这个条件直观地意味着，在最小值点，函数图像下方存在一个水平的支撑超平面。这是对光滑函数最优性条件 $\nabla f(x^\star) = 0$ 的完美推广。

#### 约束优化与法锥

为了处理约束优化问题，如 $\min_{x \in C} f(x)$，其中 $C$ 是一个凸集，我们可以利用**示性函数 (indicator function)** $\delta_C(x)$ 将其转化为无约束问题：
$$
\min_{x \in \mathbb{R}^n} f(x) + \delta_C(x)
$$
示性函数的定义为：若 $x \in C$，则 $\delta_C(x)=0$；若 $x \notin C$，则 $\delta_C(x)=+\infty$。

在凸集 $C$ 内一点 $x$ 处，示性函数的次微分被定义为 $C$ 在 $x$ 处的**法锥 (normal cone)** $N_C(x)$：
$$
\partial \delta_C(x) = N_C(x) = \{v \in \mathbb{R}^n : v^{\top}(y-x) \le 0, \text{ for all } y \in C\}
$$
法锥包含了所有从点 $x$ 指出并与集合 $C$ 形成钝角的向量。如果 $x$ 在 $C$ 的内部，法锥只包含零向量 $N_C(x)=\{0\}$。如果 $x$ 在边界上，法锥则非平凡。

应用费马法则和次微分求和法则，约束问题的最优性条件变为：
$$
0 \in \partial f(x^\star) + N_C(x^\star)
$$
这可以写成 $-g \in N_C(x^\star)$，其中 $g$ 是 $f$ 在 $x^\star$ 的某个次梯度。

#### 应用 1：到 $\ell_1$ 球上的投影

一个经典问题是将一个点 $y$ 投影到 $\ell_1$ 球 $B_\tau = \{x : \|x\|_1 \le \tau\}$ 上。这等价于求解：
$$
\min_{x \in \mathbb{R}^n} \frac{1}{2}\|x - y\|_2^2 \quad \text{s.t.} \quad x \in B_\tau
$$
利用示性函数，目标是 $\min_x \frac{1}{2}\|x-y\|_2^2 + \delta_{B_\tau}(x)$。最优解 $x^\star$ 必须满足最优性条件：
$$
0 \in (x^\star - y) + N_{B_\tau}(x^\star) \implies y - x^\star \in N_{B_\tau}(x^\star)
$$
如果 $y$ 在 $B_\tau$ 外部（即 $\|y\|_1 > \tau$），那么投影点 $x^\star$ 必定在球的边界上，即 $\|x^\star\|_1 = \tau$。在这种情况下，法锥与 $\ell_1$ 范数的次微分密切相关：$N_{B_\tau}(x^\star) = \{\theta g : \theta \ge 0, g \in \partial\|x^\star\|_1\}$。因此，最优性条件意味着存在一个非负标量 $\theta$ (拉格朗日乘子)，使得 $y-x^\star = \theta g$。这最终导出一个关于 $x^\star$ 分量的逐分量关系，即著名的**软阈值算子 (soft-thresholding operator)** 的变体：
$$
x^\star_i = \operatorname{sgn}(y_i) \max(|y_i| - \theta, 0)
$$
其中，阈值 $\theta$ 是通过满足约束 $\|x^\star\|_1 = \tau$ 来唯一确定的。例如，对于数据 $y=(4, -3, 2, 1, -0.5, 0.5, -0.1)^\top$ 和 $\tau=6$，我们可以精确地解出 $\theta=1$。[@problem_id:3483534]

#### 应用 2：基追踪 (Basis Pursuit) 与 LASSO

次梯度最优性条件是理解和解决稀疏恢复核心问题的关键。

-   **基追踪 (BP):** 问题为 $\min \|x\|_1$ subject to $Ax=b$。约束集 $C=\{x: Ax=b\}$ 是一个仿射子空间。其在任意可行点 $x^\star$ 的法锥是 $A^\top$ 的值域，即 $N_C(x^\star) = \operatorname{range}(A^\top)$。最优性条件 $0 \in \partial\|x^\star\|_1 + N_C(x^\star)$ 意味着存在一个次梯度 $g \in \partial\|x^\star\|_1$ 和一个法向量 $v \in N_C(x^\star)$ 使得 $g+v=0$。这等价于存在一个对偶向量 $y \in \mathbb{R}^m$ 使得 $A^\top y \in \partial\|x^\star\|_1$。这个条件是判断一个基追踪解是否最优的“对偶证书”。[@problem_id:3483523]

-   **LASSO:** 问题为 $\min_x \frac{1}{2}\|Ax-b\|_2^2 + \lambda\|x\|_1$。这是一个无约束问题。直接应用费马法则，最优解 $x^\star$ 必须满足：
    $$
    0 \in A^\top(Ax^\star-b) + \lambda \partial\|x^\star\|_1
    $$
    或者等价地：
    $$
    A^\top(b - Ax^\star) \in \lambda \partial\|x^\star\|_1
    $$
    这个条件蕴含了丰富的结构。它告诉我们，残差向量 $r=b-Ax^\star$ 与 $A$ 的转置相乘后，得到的向量 $A^\top r$ 必须是 $\lambda \|x\|_1$ 在 $x^\star$ 处的一个次梯度。通过分析这个条件，我们可以精确地推断解的性质。例如，我们可以确定在给定的支撑集和符号模式下，解 $x^\star(\lambda)$ 能够成为最优解的正则化参数 $\lambda$ 的取值范围。这种分析对于理解解路径算法（如 LARS）至关重要。[@problem_id:3483535]

### 高级视角与应用

次梯度理论还为现代优化中的两种强大工具——近端算子和对偶理论——提供了基础。

#### 近端算子

**近端算子 (proximal operator)** 定义为：
$$
\operatorname{prox}_{\tau f}(v) = \underset{x \in \mathbb{R}^n}{\arg\min} \left\{ \frac{1}{2}\|x - v\|_2^2 + \tau f(x) \right\}
$$
这个算子可以看作是对函数 $f$ 的一种正则化平滑，在许多迭代算法（如近端梯度法）中扮演着核心角色。其最优解 $x^\star = \operatorname{prox}_{\tau f}(v)$ 满足的最优性条件是 $0 \in (x^\star - v) + \tau \partial f(x^\star)$，即 $v-x^\star \in \tau \partial f(x^\star)$。

我们可以利用这个条件推导出许多重要函数的近端算子。例如，对于一个形如 $g(x) = \|W(Ux-a)\|_1$ 的函数，其中 $U$ 是正交阵，$W$ 是正定对角阵，通过变量代换 $z=Ux$ 并利用次梯度最优性条件，可以证明其近端算子问题可以分解为一系列独立的一维标量问题。每个标量问题的解正是软阈值算子。这最终给出了一个优美的闭式解，展示了次梯度理论在算法设计中的力量。[@problem_id:3483559]

#### 对偶性与次梯度

次梯度与**Fenchel对偶 (Fenchel duality)** 之间存在深刻的联系。考虑一个一般形式的原始问题 $\min_x f(z) + g(x)$ subject to $Ax-z=0$。利用Fenchel共轭的定义 $f^\ast(u) = \sup_z \{u^\top z - f(z)\}$，可以推导出其对偶问题。

对于LASSO去噪问题（即 $\min_x \frac{1}{2}\|x-b\|_2^2 + \lambda\|x\|_1$），可以证明其对偶问题是在一个 $\ell_\infty$ 范数球（一个超立方体）内最小化一个二次函数。[@problem_id:3483566]
$$
\min_{v \in \mathbb{R}^{n}} \frac{1}{2}\|v\|^2 - v^{\top}b \quad \text{subject to} \quad \|v\|_{\infty} \le \lambda
$$
强对偶性成立时，原始问题和对偶问题的最优值相等。更重要的是，原始最优解 $x^\star$ 和对偶最优解 $u^\star$ 通过次梯度关系联系在一起：
1.  $-A^\top u^\star \in \partial g(x^\star)$
2.  $u^\star \in \partial f(Ax^\star)$

对于 $A=I$ 的LASSO问题，这些条件简化为 $u^\star = x^\star - b$ 和 $-u^\star \in \lambda \partial \|x^\star\|_1$，这再次导出了我们已经熟悉的软阈值解 $x^\star_i = \operatorname{sgn}(b_i)\max(|b_i|-\lambda, 0)$。这不仅为求解原始问题提供了另一条途径，也揭示了优化问题背后优美的对称结构。

综上所述，次梯度和次微分是分析和解决非光滑凸优化问题的不可或缺的工具。它们不仅为不可微函数提供了梯度的替代品，还构成了最优性条件、对偶理论和现代优化算法的基石。