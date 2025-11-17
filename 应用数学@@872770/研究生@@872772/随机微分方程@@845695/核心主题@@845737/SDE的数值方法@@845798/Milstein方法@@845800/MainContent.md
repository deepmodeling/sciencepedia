## 引言
在[随机过程](@entry_id:159502)的[数值模拟](@entry_id:137087)领域，精确且高效地求解[随机微分方程](@entry_id:146618)（SDE）是一项核心挑战。虽然基础的[Euler-Maruyama方法](@entry_id:199529)因其简单性而广受欢迎，但其较低的强[收敛阶](@entry_id:146394)（仅为0.5）在许多要求高路径精度的应用中显得力不从心。这便引出了一个关键问题：我们如何构建一个既保持[计算效率](@entry_id:270255)又能显著提升收敛精度的数值格式？[Milstein方法](@entry_id:142707)正是对这一问题的经典回答，它通过对[随机积分](@entry_id:198356)项进行更高阶的近似，成功地将强[收敛阶](@entry_id:146394)提升至1.0，成为连接基础方法与高级数值格式的重要桥梁。

本文将系统性地剖析[Milstein方法](@entry_id:142707)。我们将在第一部分“原理与机制”中，从SDE的严格定义和Itô-Taylor展开出发，详细推导[Milstein格式](@entry_id:140856)，分析其收敛性质，并探讨其在[多维系统](@entry_id:274301)中的推广。接下来的“应用与跨学科联系”部分将展示该方法在量化金融、物理、生物等领域的广泛应用，并揭示其与更高级计算技术及[随机分析](@entry_id:188809)核心理论的深刻联系。最后，在“动手实践”部分，读者将通过具体问题加深对方法特性及其应用边界的理解。通过这三章的学习，您将全面掌握[Milstein方法](@entry_id:142707)的理论精髓与实践要领。

## 原理与机制

本章旨在深入探讨[Milstein方法](@entry_id:142707)的数学原理与核心机制。在前一章对[随机微分方程](@entry_id:146618)（SDE）及其应用背景进行介绍之后，我们将聚焦于如何构建比基础的[Euler-Maruyama方法](@entry_id:199529)更精确的数值格式。本章将从Itô-[Taylor展开](@entry_id:145057)式出发，系统地推导出[Milstein方法](@entry_id:142707)，分析其[收敛阶](@entry_id:146394)，并将其推广至多维情形，最后通过一个具体的稳定性分析案例来展示其理论性质。

### 随机微分方程的严格定义

在构建任何[数值近似](@entry_id:161970)之前，我们必须首先精确地理解我们试图近似的对象。一个标量Itô型[随机微分方程](@entry_id:146618)通常被非正式地写作：
$$
\mathrm{d}X_t = a(X_t, t)\,\mathrm{d}t + b(X_t, t)\,\mathrm{d}W_t
$$
其中 $W_t$ 是一个标准的布朗运动（或[维纳过程](@entry_id:137696)）。然而，这个[微分形式](@entry_id:146747)只是一个简便的记号。其严格的数学意义由一个等价的[积分方程](@entry_id:138643)给出。一个[随机过程](@entry_id:159502) $X_t$ 被称为上述SDE的**[强解](@entry_id:198344)** (strong solution)，如果它满足以下几个条件。

首先，解过程 $X_t$ 必须是**适应的** (adapted)。这意味着在任何时刻 $t$，$X_t$ 的值只能依赖于布朗运动在 $t$ 时刻及之前（即 $\{W_s: 0 \le s \le t\}$）的历史信息，而不能依赖于未来的信息。这个“非预知性” (non-anticipativity) 的要求通过一个**滤子** (filtration) $\{\mathcal{F}_t\}_{t \ge 0}$ 来形式化，其中 $\mathcal{F}_t$ 代表了直到时刻 $t$ 的所有可用信息。$X_t$ 是适应的，意味着对任意 $t$，$X_t$ 都是 $\mathcal{F}_t$-可测的。

其次，SDE的严格定义是如下的[积分方程](@entry_id:138643)：
$$
X_t = X_0 + \int_0^t a(X_s, s)\,\mathrm{d}s + \int_0^t b(X_s, s)\,\mathrm{d}W_s
$$
这个方程对所有 $t \ge 0$ [几乎必然](@entry_id:262518)成立。这个表述要求方程中的两个积分都是良定义的。第一个积分是标准的Lebesgue积分，它要求被积过程 $s \mapsto a(X_s, s)$ 是可积的。第二个积分是Itô[随机积分](@entry_id:198356)，它有更严格的要求。为了确保[Itô积分](@entry_id:272774) $\int_0^t b(X_s, s)\,\mathrm{d}W_s$ 是良定义的，被积过程 $s \mapsto b(X_s, s)$ 不仅必须是适应的，还必须满足一个更强的**逐点[可测性](@entry_id:199191)** (progressively measurable) 条件，并且在平方意义下是可积的，即对于任意有限的时间 $T > 0$，满足：
$$
\mathbb{E}\left[\int_0^T |b(X_s, s)|^2\,\mathrm{d}s\right]  \infty
$$
这个平方[可积条件](@entry_id:158502)确保了[Itô积分](@entry_id:272774)是一个 $L^2$-鞅，具有良好的数学性质。因此，当我们讨论SDE的数值解时，我们实际上是在寻找一个[离散时间过程](@entry_id:274269)，它能以某种明确的方式逼近这个积分方程的解。[@problem_id:3002559]

### Itô-Taylor展开：高阶方法的基础

经典微积分中的Taylor展开为函数近似提供了强大的理论基础。在[随机分析](@entry_id:188809)中，一个类似但更为丰富的理论是**Itô-Taylor展开** (Itô-Taylor expansion)。它为SDE的解在一个小时间区间 $[t_n, t_{n+1}]$ 上的增量 $X_{t_{n+1}} - X_{t_n}$ 提供了一个展开式。这个展开式构成了包括[Milstein方法](@entry_id:142707)在内的所有高阶强收敛格式的基石。

考虑标量SDE $\mathrm{d}X_t = a(X_t)\,\mathrm{d}t + b(X_t)\,\mathrm{d}W_t$。其在 $[t_n, t_{n+1}]$ 上的积分形式为：
$$
X_{t_{n+1}} = X_{t_n} + \int_{t_n}^{t_{n+1}} a(X_s)\,\mathrm{d}s + \int_{t_n}^{t_{n+1}} b(X_s)\,\mathrm{d}W_s
$$
为了得到一个近似，我们可以将被积函数 $a(X_s)$ 和 $b(X_s)$ 在 $t_n$ 处展开。最简单的近似是使用常数近似 $a(X_s) \approx a(X_{t_n})$ 和 $b(X_s) \approx b(X_{t_n})$，这会导出[Euler-Maruyama方法](@entry_id:199529)。为了获得更高的精度，我们需要更精确地近似被积函数，特别是随机积分中的 $b(X_s)$。通过对 $b(X_s)$ 应用[Itô公式](@entry_id:634674)，我们可以得到它的展开：
$$
b(X_s) \approx b(X_{t_n}) + \int_{t_n}^s (L^0 b)(X_r)\,\mathrm{d}r + \int_{t_n}^s (L^1 b)(X_r)\,\mathrm{d}W_r
$$
其中 $L^0 = a \frac{\partial}{\partial x} + \frac{1}{2}b^2 \frac{\partial^2}{\partial x^2}$ 和 $L^1 = b \frac{\partial}{\partial x}$ 是与SDE相关的[微分算子](@entry_id:140145)。将这个展开代入原[积分方程](@entry_id:138643)，并保留到一定阶数的项，我们就得到了Itô-[Taylor展开](@entry_id:145057)。展开式中的项由一系列**多重随机积分** (multiple stochastic integrals) 构成。对于强收敛阶为1的方法，我们需要考虑以下基本积分（设时间步长为 $h=t_{n+1}-t_n$）：
$$
I_{(0)} = \int_{t_n}^{t_{n+1}} \mathrm{d}s = h, \quad I_{(1)} = \int_{t_n}^{t_{n+1}} \mathrm{d}W_s = \Delta W_n
$$
$$
I_{(1,1)} = \int_{t_n}^{t_{n+1}} \int_{t_n}^{s} \mathrm{d}W_r\,\mathrm{d}W_s, \quad I_{(1,0)} = \int_{t_n}^{t_{n+1}} \int_{t_n}^{s} \mathrm{d}r\,\mathrm{d}W_s, \quad I_{(0,1)} = \int_{t_n}^{t_{n+1}} \int_{t_n}^{s} \mathrm{d}W_r\,\mathrm{d}s
$$
一个数值方法的**强收敛阶** (strong order of convergence) 为 $\gamma$，意味着其[全局误差](@entry_id:147874)的[均方根](@entry_id:263605)（RMS）以 $O(h^\gamma)$ 的速度随步长 $h$ 减小。要构建一个强[收敛阶](@entry_id:146394)为1的方法，我们需要保留Itô-[Taylor展开](@entry_id:145057)中所有均方根大小为 $O(h)$ 或更大的项，而可以截断掉那些[均方根](@entry_id:263605)为 $O(h^{3/2})$ 或更小的项。通过[Itô等距](@entry_id:260731)性质等工具，我们可以计算这些基本积分的[均方根](@entry_id:263605)大小：
- $I_{(1)} = \Delta W_n$ 的[均方根](@entry_id:263605)是 $\sqrt{\mathbb{E}[(\Delta W_n)^2]} = \sqrt{h} = O(h^{1/2})$。
- $I_{(1,1)}$ 的均方根是 $\sqrt{\mathbb{E}[I_{(1,1)}^2]} = \sqrt{\frac{1}{2}h^2} = O(h)$。
- $I_{(1,0)}$ 和 $I_{(0,1)}$ 的[均方根](@entry_id:263605)大小均为 $O(h^{3/2})$。

因此，为了从[Euler-Maruyama方法](@entry_id:199529)（仅包含 $I_{(0)}$ 和 $I_{(1)}$ 的项，强[收敛阶](@entry_id:146394)为0.5）提升到强收敛阶为1.0的方法，我们必须精确地包含与 $I_{(1,1)}$ 相关的项，同时可以安全地忽略与 $I_{(1,0)}$ 和 $I_{(0,1)}$ 相关的项。[@problem_id:3002562]

### 标量[Milstein方法](@entry_id:142707)

#### 推导与公式

根据上述Itô-Taylor分析，一个强收敛阶为1.0的格式应该近似于以下展开：
$$
X_{t_{n+1}} - X_{t_n} \approx a(X_{t_n}) I_{(0)} + b(X_{t_n}) I_{(1)} + (L^1 b)(X_{t_n}) I_{(1,1)}
$$
代入算子 $L^1 b = b \frac{\partial b}{\partial x} = b b'$ 和积分 $I_{(0)}=h$, $I_{(1)}=\Delta W_n$，我们得到：
$$
X_{t_{n+1}} - X_{t_n} \approx a(X_{t_n})h + b(X_{t_n})\Delta W_n + b(X_{t_n})b'(X_{t_n})I_{(1,1)}
$$
这里的核心在于如何处理[多重积分](@entry_id:146170) $I_{(1,1)}$。通过对函数 $f(W_t) = W_t^2/2$ 应用[Itô公式](@entry_id:634674)，可以得到一个关键的恒等式：
$$
I_{(1,1)} = \int_{t_n}^{t_{n+1}} (W_s - W_{t_n})\,\mathrm{d}W_s = \frac{1}{2}\left( (W_{t_{n+1}} - W_{t_n})^2 - (t_{n+1} - t_n) \right) = \frac{1}{2}((\Delta W_n)^2 - h)
$$
这个恒等式允许我们用布朗运动增量 $\Delta W_n$ 的简单代数组合来精确表示 $I_{(1,1)}$，从而避免了直接模拟多重随机积分的复杂性。

将这个结果代回展开式，我们就得到了**[Milstein方法](@entry_id:142707)**的单步更新格式。记 $X_n$ 为 $X_{t_n}$ 的数值近似，则从 $X_n$ 到 $X_{n+1}$ 的更新规则为：
$$
X_{n+1} = X_n + a(X_n)h + b(X_n)\Delta W_n + \frac{1}{2} b(X_n)b'(X_n)\left( (\Delta W_n)^2 - h \right)
$$
其中：
- $h$ 是时间步长。
- $\Delta W_n = W_{t_{n+1}} - W_{t_n}$ 是布朗运动在一个步长内的增量，它是一个[正态分布](@entry_id:154414)的[随机变量](@entry_id:195330)，$\Delta W_n \sim \mathcal{N}(0, h)$。在模拟中，它通常通过 $\sqrt{h}Z_n$ 生成，其中 $Z_n$ 是一个标准正态[随机变量](@entry_id:195330)。不同时间步的增量 $\Delta W_n$ 和 $\Delta W_m$ ($n \ne m$) 是[相互独立](@entry_id:273670)的。
- $a(X_n)$ 和 $b(X_n)$ 是漂移和扩散系数在点 $X_n$ 的取值。
- $b'(X_n)$ 是[扩散](@entry_id:141445)系数函数 $b(x)$ 关于其[状态变量](@entry_id:138790) $x$ 的导数，并在点 $X_n$ 处求值。[@problem_id:3002627]

#### 强收敛与[误差分析](@entry_id:142477)

数值方法的质量通过其收敛性来衡量。对于SDE，主要有两种收敛性概念：**强收敛** (strong convergence) 和**[弱收敛](@entry_id:146650)** (weak convergence)。

**强收敛**关心的是数值解的样本路径是否能逐点地逼近真实解的样本路径。一个[数值格式](@entry_id:752822)被称为具有**强收敛阶** $\gamma > 0$，如果存在一个与步长 $h$ 和时间点 $n$ 无关的常数 $C$，使得在有限时间区间 $[0, T]$ 上，对于足够小的 $h$：
$$
\max_{0 \le n \le N} \left(\mathbb{E}\left[|X_{t_n} - X_n|^p\right]\right)^{1/p} \le C h^\gamma
$$
对某个 $p \ge 1$ 成立，其中 $N=T/h$。这个定义衡量了在所有离散时间点上，$L^p$ 范数意义下的误差的最大值。[@problem_id:3002644]

[Euler-Maruyama方法](@entry_id:199529)通过截断Itô-Taylor展开中的 $I_{(1,1)}$ 项（以及所有更高阶项）得到。被省略的主导误差项是 $\frac{1}{2} b(X_n)b'(X_n) ((\Delta W_n)^2 - h)$。这是一个以 $\mathcal{F}_{t_n}$ 为条件的零均值（即[鞅](@entry_id:267779)差）[随机变量](@entry_id:195330)，其均方根大小为 $O(h)$。在 $N = T/h$ 个时间步上，这些独立的、零均值的局部误差的累积行为类似于[随机游走](@entry_id:142620)，其总误差的[均方根](@entry_id:263605)大小约为 $\sqrt{N} \times O(h) = \sqrt{T/h} \times O(h) = O(h^{1/2})$。这解释了为什么[Euler-Maruyama方法](@entry_id:199529)的强收敛阶为 $\gamma=0.5$。[@problem_id:3002618]

[Milstein方法](@entry_id:142707)通过精确地包含这一项，消除了局部误差中的主导随机项。其剩余的局部误差由更高阶的积分（如 $I_{(1,0)}, I_{(0,1)}$ 等）贡献，这些项的均方根大小为 $O(h^{3/2})$。这种更高阶的局部[误差累积](@entry_id:137710)起来，得到的全局强收敛阶为 $\gamma=1.0$。[@problem_id:3002644]

与强收敛相对的是**[弱收敛](@entry_id:146650)** (weak convergence)，它不要求路径本身的逼近，而是要求数值解的[统计矩](@entry_id:268545)（或更一般地，关于测试函数的期望）能逼近真实解的[统计矩](@entry_id:268545)。[弱收敛](@entry_id:146650)阶 $\gamma$ 的定义是，对于足够光滑的测试函数 $\phi$：
$$
\sup_{0 \le n \le N} \left| \mathbb{E}[\phi(X_{t_n})] - \mathbb{E}[\phi(X_n)] \right| \le C h^\gamma
$$
强收敛比[弱收敛](@entry_id:146650)更强，即强收敛阶为 $\gamma$ 蕴含着（对于[Lipschitz连续的](@entry_id:267396)测试函数）[弱收敛](@entry_id:146650)阶也至少为 $\gamma$。然而，反之不成立。一个重要的例子是，对于典型的SDE，[Euler-Maruyama方法](@entry_id:199529)和[Milstein方法](@entry_id:142707)都具有 $\gamma=1.0$ 的[弱收敛](@entry_id:146650)阶。因此，[Milstein方法](@entry_id:142707)相对于[Euler-Maruyama方法](@entry_id:199529)的主要优势在于其更高的**强收敛**精度，这对于需要[精确模拟](@entry_id:749142)样本路径的应用（如[金融衍生品定价](@entry_id:181545)中的[路径依赖期权](@entry_id:140114)）至关重要。[@problem_id:3002569]

### 多维[Milstein方法](@entry_id:142707)：交换性的角色

将[Milstein方法](@entry_id:142707)推广到多维情形会遇到新的挑战。考虑一个由 $m$ 个独立布朗运动驱动的 $d$ 维SDE：
$$
\mathrm{d}X_t = a(X_t)\,\mathrm{d}t + \sum_{j=1}^m b_j(X_t)\,\mathrm{d}W_t^{(j)}
$$
其中 $a$ 和 $b_j$ 现在是 $\mathbb{R}^d$ 上的向量场。多维Itô-[Taylor展开](@entry_id:145057)会引入一系列[多重积分](@entry_id:146170) $I_{(j,k)} = \int_{t_n}^{t_{n+1}} \int_{t_n}^s \mathrm{d}W_r^{(k)}\,\mathrm{d}W_s^{(j)}$。

当 $j=k$ 时，与标量情况一样，$I_{(j,j)} = \frac{1}{2}((\Delta W_n^{(j)})^2 - h)$。然而，当 $j \ne k$ 时，$I_{(j,k)}$ 和 $I_{(k,j)}$ 是不同的[随机变量](@entry_id:195330)。它们的反对称组合 $A_n^{(j,k)} = I_{(j,k)} - I_{(k,j)}$ 被称为**[Lévy面积](@entry_id:634943)** (Lévy area)，它不能仅由布朗增量 $\Delta W_n^{(j)}$ 和 $\Delta W_n^{(k)}$ 的代数组合来表示，需要专门的模拟算法。

#### 交换噪声情形

在一些特殊但重要的情形下，[Milstein方法](@entry_id:142707)可以避免模拟[Lévy面积](@entry_id:634943)。这发生在[扩散](@entry_id:141445)向量场 $b_j$ 满足**交换性条件** (commutativity condition) 时。两个向量场 $b_j$ 和 $b_k$ 的[交换性](@entry_id:140240)通过它们的**李括号** (Lie bracket) 来衡量。[李括号](@entry_id:636461)定义为：
$$
[b_j, b_k](x) = (L^k b_j)(x) - (L^j b_k)(x) = \nabla b_j(x) \cdot b_k(x) - \nabla b_k(x) \cdot b_j(x)
$$
其中 $L^j$ 是沿向量场 $b_j$ 的[方向导数](@entry_id:189133)算子，$\nabla b_j$ 是 $b_j$ 的雅可比矩阵。如果对于所有的 $j, k=1,\dots,m$，李括号恒为零，即 $[b_j, b_k] \equiv 0$，则称该SDE具有**交换噪声** (commutative noise)。[@problem_id:3002657]

在交换噪声的条件下，Itô-[Taylor展开](@entry_id:145057)中[Lévy面积](@entry_id:634943)项的系数 $([b_j,b_k])$ 恰好为零。这使得多维[Milstein方法](@entry_id:142707)急剧简化。利用恒等式 $I_{(j,k)} + I_{(k,j)} = \Delta W_n^{(j)}\Delta W_n^{(k)}$（对 $j \ne k$），可以证明完整的Milstein校正项可以写成一个只包含布朗增量的形式。最终，对于具有交换噪声的SDE，强收敛阶为1.0的[Milstein格式](@entry_id:140856)为：
$$
X_{n+1} = X_n + a(X_n)h + \sum_{j=1}^m b_j(X_n)\Delta W_n^{(j)} + \frac{1}{2} \sum_{j,k=1}^m (L^j b_k)(X_n) \left( \Delta W_n^{(j)}\Delta W_n^{(k)} - \delta_{jk}h \right)
$$
其中 $\delta_{jk}$ 是克罗内克符号。这个公式是可直接实现的，因为它只依赖于漂移、[扩散](@entry_id:141445)系数及其[一阶导数](@entry_id:749425)，以及易于生成的高斯[随机变量](@entry_id:195330) $\Delta W_n^{(j)}$。[@problem_id:3002663]

#### [非交换噪声](@entry_id:181267)的一般情形

在一般情况下，SDE的噪声结构是[非交换](@entry_id:136599)的，即至少存在一对 $(j,k)$ 使得 $[b_j, b_k] \not\equiv 0$。在这种情况下，Itô-Taylor展开中[Lévy面积](@entry_id:634943)项的系数非零。完整的强收敛阶为1.0的[Milstein格式](@entry_id:140856)（有时也称为Platen格式）必须包含这些项：
$$
\begin{aligned}
X_{n+1} = X_n + a(X_n)h + \sum_{j=1}^m b_j(X_n)\Delta W_n^{(j)} + \frac{1}{2} \sum_{j,k=1}^m (L^j b_k)(X_n) (\Delta W_n^{(j)}\Delta W_n^{(k)} - \delta_{jk}h) \\
- \frac{1}{2} \sum_{1 \le j  k \le m} [b_j, b_k](X_n) A_n^{(j,k)}
\end{aligned}
$$
其中 $A_n^{(j,k)}$ 是[Lévy面积](@entry_id:634943)。由于[Lévy面积](@entry_id:634943)项的随机量级为 $O(h)$，如果忽略它们（即使用交换情形下的简化公式），将会引入一个 $O(h)$ 的局部误差，导致全局强[收敛阶](@entry_id:146394)退化回与[Euler-Maruyama方法](@entry_id:199529)相同的 $\gamma=0.5$。因此，对于[非交换噪声](@entry_id:181267)SDE，要达到强[收敛阶](@entry_id:146394)1.0，模拟或近似[Lévy面积](@entry_id:634943)是不可避免的，这大大增加了算法的实现复杂度。[@problem_id:3002570]

### 应用：[均方稳定性](@entry_id:165904)分析

除了收敛性，**稳定性** (stability) 是评价数值方法的另一个关键指标。它研究的是当时间步数增多时，数值解的误差是否保持有界。对于SDE，一个重要的概念是**[均方稳定性](@entry_id:165904)** (mean-square stability)，即要求数值解的二阶矩 $\mathbb{E}[|X_n|^2]$ 保持有界。

我们以一个经典的测试方程——[几何布朗运动](@entry_id:137398)——为例来分析[Milstein方法](@entry_id:142707)的稳定性：
$$
\mathrm{d}X_t = \lambda X_t\,\mathrm{d}t + \mu X_t\,\mathrm{d}W_t
$$
这里的系数为 $a(x) = \lambda x$ 和 $b(x) = \mu x$。因此，$b'(x) = \mu$。将这些代入标量[Milstein格式](@entry_id:140856)，我们得到该SDE的特定更新规则：
$$
X_{n+1} = X_n + \lambda X_n h + \mu X_n \Delta W_n + \frac{1}{2}(\mu X_n)(\mu)((\Delta W_n)^2 - h) = X_n \left( 1 + \lambda h + \mu \Delta W_n + \frac{1}{2}\mu^2((\Delta W_n)^2 - h) \right)
$$
为了分析[均方稳定性](@entry_id:165904)，我们计算 $X_{n+1}$ 的二阶矩。利用增量 $\Delta W_n$ 独立于 $X_n$ 的性质，以及[高斯变量](@entry_id:276673)的各阶矩（$\mathbb{E}[\Delta W_n]=0$, $\mathbb{E}[(\Delta W_n)^2]=h$, $\mathbb{E}[(\Delta W_n)^3]=0$, $\mathbb{E}[(\Delta W_n)^4]=3h^2$），我们可以得到：
$$
\mathbb{E}[|X_{n+1}|^2] = \mathbb{E}[X_n^2] \cdot \mathbb{E}\left[ \left( 1 + \lambda h + \mu \Delta W_n + \frac{1}{2}\mu^2((\Delta W_n)^2 - h) \right)^2 \right]
$$
经过直接但略显繁琐的计算，可以求得括号内期望的值。最终，我们得到一个关系式：
$$
\mathbb{E}[|X_{n+1}|^2] = G(\lambda, \mu, h) \mathbb{E}[|X_n|^2]
$$
其中**均方放大因子** (mean-square amplification factor) $G(\lambda, \mu, h)$ 为：
$$
G(\lambda, \mu, h) = 1 + (2\lambda + \mu^2)h + (\lambda^2 + \frac{1}{2}\mu^4) h^2
$$
[数值格式](@entry_id:752822)是均方稳定的，当且仅当这个放大因子的大小不大于1，即 $|G(\lambda, \mu, h)| \le 1$。对于严格稳定性（即二阶矩随时间衰减），则要求 $|G(\lambda, \mu, h)|  1$。这个不等式定义了在[参数空间](@entry_id:178581) $(\lambda, \mu, h)$ 中的一个区域，称为**均方稳定区域** (region of mean-square stability)。只有当参数组合落在这个区域内时，[Milstein方法](@entry_id:142707)应用于该SDE的数值解才不会在均方意义下发散。这种分析是检验和比较不同数值格式[长期行为](@entry_id:192358)的有力工具。[@problem_id:3002528]