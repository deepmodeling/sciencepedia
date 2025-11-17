## 引言
在[随机过程](@entry_id:159502)的广阔领域中，理解系统的长期行为是一个核心问题。由随机微分方程（SDEs）描述的系统无处不在，从物理学中粒子的布朗运动到金融学中资产价格的波动。一个自然而深刻的问题是：当时间趋于无穷时，这些系统会趋向于一个稳定的统计均衡状态吗？平稳分布和不变测度的概念正是为了精确回答这一问题而生。它们不仅为量化“平衡态”提供了严格的数学框架，也揭示了系统微观动力学与宏观统计规律之间的深刻联系。

本文旨在系统性地阐述[平稳分布](@entry_id:194199)与[不变测度](@entry_id:202044)的核心理论及其在众多学科中的应用。我们将解决如何从数学上定义、验证并保证一个随机系统存在统计均衡态的问题。读者将通过三个层次递进的章节，构建对这一重要理论的全面理解。

第一章“原理与机制”将深入探讨不变测度的数学基础，从其定义、无穷小判据（如Fokker-Planck方程）出发，到存在性（Foster-Lyapunov判据）、唯一性和遍历性的关键定理，最终讨论向均衡态收敛的速度问题。第二章“应用与跨学科联系”将展示这些抽象理论的强大生命力，通过实例揭示它们如何成为统计物理、[分子模拟](@entry_id:182701)、贝叶斯推断、种群遗传学乃至[平均场博弈](@entry_id:204131)等领域的理论基石。最后，在“动手实践”部分，读者将通过具体问题，将理论应用于分析不同情境下的平稳行为，从而巩固所学知识。

## 原理与机制

在本章中，我们将深入探讨随机微分方程（SDEs）的平稳分布和不变测度的核心理论。这些概念对于理解[随机系统的长期行为](@entry_id:186721)至关重要。我们将从[不变测度](@entry_id:202044)的基本定义出发，探索其[无穷小生成元](@entry_id:270424)和Fokker-Planck方程的等价描述，然后转向存在性、唯一性和遍历性的关键定理，最后讨论向均衡态收敛的速度问题。

### 不变性的定义：核心概念

在研究一个随机系统时，一个自然的问题是：是否存在一种“统计均衡”状态？也就是说，是否存在一个[概率分布](@entry_id:146404)，使得如果系统最初处于该[分布](@entry_id:182848)，那么在任何未来时刻，它在统计上都保持不变？这个概念在数学上被形式化为 **不变测度 (invariant measure)**。

考虑一个由[马尔可夫半群](@entry_id:191984) $(P_t)_{t \ge 0}$ 描述的时间齐次[马尔可夫过程](@entry_id:160396)，其状态空间为 $(E, \mathcal{B})$。算子 $P_t$ 作用于有界可测函数 $f: E \to \mathbb{R}$，其定义为 $(P_t f)(x) = \mathbb{E}_x[f(X_t)]$，即从状态 $x$ 出发，过程在 $t$ 时刻的函数 $f$ 的[期望值](@entry_id:153208)。与此对应，我们可以定义 $P_t$ 在测度上的一个对偶作用。给定一个初始[分布](@entry_id:182848) $\mu$，过程在 $t$ 时刻的[分布](@entry_id:182848) $\mu_t$ 由 $\mu P_t$ 给出。

一个概率测度 $\pi$ 被称为是 **不变的 (invariant)**，如果它在半群的对偶作用下保持不变，即对于所有 $t \ge 0$，都有 $\pi P_t = \pi$。如果一个[不变测度](@entry_id:202044)是概率测度，我们通常称之为 **平稳分布 (stationary distribution)**。

这个定义有几种等价的积分形式，它们在实际应用和理论推导中都非常有用 [@problem_id:2996754]。
1.  **对可测集的作用**: 对于所有 $t \ge 0$ 和所有[可测集](@entry_id:159173) $A \in \mathcal{B}$，两个测度 $\pi P_t$ 和 $\pi$ 对集合 $A$ 的度量是相同的。根据对偶作用的定义，这意味着：
    $$
    \int_E P_t(x, A) \, \pi(dx) = \pi(A)
    $$
    其中 $P_t(x, A)$ 是从 $x$ 出发在 $t$ 时刻转移到集合 $A$ 内的概率。这是不变性最直接的表达。

2.  **对有界[可测函数](@entry_id:159040)的作用 ([弱形式](@entry_id:142897))**: 两个测度相等，当且仅当它们对所有有界[可测函数的积](@entry_id:194504)分都相等。因此，$\pi P_t = \pi$ 等价于：对于所有 $t \ge 0$ 和所有有界可测函数 $f: E \to \mathbb{R}$，
    $$
    \int_E f(x) \, (\pi P_t)(dx) = \int_E f(x) \, \pi(dx)
    $$
    通过[Fubini定理](@entry_id:136363)，左侧可以改写，从而得到另一个非常有用的等价形式：
    $$
    \int_E (P_t f)(x) \, \pi(dx) = \int_E f(x) \, \pi(dx)
    $$

对于由随机微分方程 $dX_t = b(X_t)dt + \sigma(X_t)dW_t$ 描述的[扩散过程](@entry_id:170696)，[平稳分布](@entry_id:194199)的直观意义是：如果初始状态 $X_0$ 是根据[概率测度](@entry_id:190821) $\pi$ 抽取的（记为 $X_0 \sim \pi$），那么在任何未来的时刻 $t > 0$，过程的状态 $X_t$ 也服从相同的[分布](@entry_id:182848)，即 $X_t \sim \pi$ [@problem_id:2996787]。

在这里，我们必须区分 **[平稳分布](@entry_id:194199)** 和 **严[平稳过程](@entry_id:196130) (strictly stationary process)** 这两个概念 [@problem_id:2996780]。平稳分布是状态空间上的一个概率测度，描述了系统在某一时刻的统计状态。而严[平稳过程](@entry_id:196130)是路径空间上的一个测度，其所有[有限维分布](@entry_id:197042)都具有[时移](@entry_id:261541)不变性。也就是说，对于任意时间点 $t_1, \dots, t_n$ 和任意时间平移 $h \ge 0$，随机向量 $(X_{t_1}, \dots, X_{t_n})$ 和 $(X_{t_1+h}, \dots, X_{t_n+h})$ 的[联合分布](@entry_id:263960)是相同的。对于时间齐次的[马尔可夫过程](@entry_id:160396)，这两个概念通过一个优美的定理联系在一起：**一个时间齐次的[马尔可夫过程](@entry_id:160396)是严平稳的，当且仅当其初始[分布](@entry_id:182848)是一个[平稳分布](@entry_id:194199)**。

值得注意的是，[平稳分布](@entry_id:194199)的概念内在地依赖于过程的时间齐次性，即漂移项 $b$ 和[扩散](@entry_id:141445)项 $\sigma$ 不显式依赖于时间 $t$。对于时间非齐次的SDE，例如 $dX_t = b(t, X_t)dt + \sigma(t, X_t)dW_t$，通常不存在一个单一的、不随时间变化的[平稳分布](@entry_id:194199)。在这种情况下，平稳性的概念被推广为所谓的 **演化测度族 (evolutionary family of measures)** $(\mu_t)_{t \ge 0}$，它满足 $\mu_s P_{s,t} = \mu_t$，其中 $P_{s,t}$ 是从时间 $s$ 到时间 $t$ 的转移算子 [@problem_id:2996787]。

### [不变性](@entry_id:140168)的无穷小判据

直接验证 $\pi P_t = \pi$ 对于所有 $t \ge 0$ 往往很困难。幸运的是，我们可以通过考察无穷小时间下的行为来简化这个问题，这引出了 **无穷小生成元 (infinitesimal generator)** $\mathcal{L}$。

对于一个定义在 $C_c^2(\mathbb{R}^d)$（具有[紧支集](@entry_id:276214)的二次[连续可微函数](@entry_id:200349)空间）上的扩散过程的生成元 $\mathcal{L}$，它由下式给出：
$$
\mathcal{L} f(x) = \sum_{i=1}^d b_i(x)\,\partial_i f(x) + \frac{1}{2}\sum_{i,j=1}^d a_{ij}(x)\,\partial_{ij} f(x), \quad a(x) = \sigma(x)\sigma(x)^\top
$$
生成元和半群的关系是 $P_t = \exp(t\mathcal{L})$，并且 $\frac{d}{dt} P_t f = P_t (\mathcal{L} f) = \mathcal{L} (P_t f)$。

如果我们对[不变性条件](@entry_id:171412) $\int P_t f \, d\pi = \int f \, d\pi$ 在 $t=0$ 处对时间 $t$ 求导，并假设可以交换积分和[微分](@entry_id:158718)的顺序，我们得到：
$$
\left. \frac{d}{dt} \int P_t f \, d\pi \right|_{t=0} = \int \left. \frac{d}{dt} P_t f \right|_{t=0} \, d\pi = \int \mathcal{L} f \, d\pi
$$
由于等式右边 $\int f \, d\pi$ 不依赖于 $t$，其导数为零。因此，我们得到了[不变测度](@entry_id:202044)的一个关键的无穷小判据 [@problem_id:2996787] [@problem_id:2996772]：
$$
\int_{\mathbb{R}^d} \mathcal{L} f(x) \, d\pi(x) = 0
$$
这个等式必须对[生成元定义域](@entry_id:202398)的一个核心（例如 $C_c^2(\mathbb{R}^d)$）中的所有函数 $f$ 成立。反过来，如果这个条件成立，可以证明 $\pi$ 是一个不变测度。这个判据将验证[不变性](@entry_id:140168)的问题从检查所有时间 $t$ 简化为检查一个与时间无关的积分条件。

### [Fokker-Planck方程](@entry_id:140155)：[偏微分方程](@entry_id:141332)视角

当一个不变测度 $\pi$ 关于勒贝格测度是绝对连续的，即它可以写成 $\pi(dx) = \rho(x)dx$ 的形式时，$\rho(x)$ 被称为 **平稳密度 (stationary density)**。在这种情况下，无穷小判据可以被转化为一个[偏微分方程](@entry_id:141332)。

无穷小判据变为：
$$
\int_{\mathbb{R}^d} (\mathcal{L} f)(x) \, \rho(x) \, dx = 0
$$
对于所有[检验函数](@entry_id:166589) $f \in C_c^2(\mathbb{R}^d)$ 成立 [@problem_id:2996778]。这个形式是算子 $\mathcal{L}$ 和函数 $\rho$ 之间对偶关系的[弱形式](@entry_id:142897)表达。通过对 $\mathcal{L}f$ 的表达式进行[分部积分](@entry_id:136350)（并利用 $f$ 的[紧支集](@entry_id:276214)性质使得边界项消失），我们可以将[微分算子](@entry_id:140145)从 $f$ 转移到 $\rho$ 上。这个过程定义了 $\mathcal{L}$ 的形式[伴随算子](@entry_id:140236) $\mathcal{L}^*$，也称为 **[Fokker-Planck](@entry_id:635508)算子** [@problem_id:2996772]：
$$
\int_{\mathbb{R}^d} (\mathcal{L} f)(x) \, \rho(x) \, dx = \int_{\mathbb{R}^d} f(x) \, (\mathcal{L}^* \rho)(x) \, dx
$$
其中
$$
\mathcal{L}^* \rho(x) = -\sum_{i=1}^d \partial_i\big(b_i(x)\rho(x)\big) + \frac{1}{2}\sum_{i,j=1}^d \partial_{ij}\big(a_{ij}(x)\rho(x)\big)
$$
因此，无穷小判据 $\int (\mathcal{L} f) \rho \, dx = 0$ 在[分布](@entry_id:182848)意义下等价于一个[偏微分方程](@entry_id:141332) [@problem_id:2996778]：
$$
\mathcal{L}^* \rho = 0
$$
这就是 **定常[Fokker-Planck方程](@entry_id:140155) (stationary [Fokker-Planck](@entry_id:635508) equation)**，也称为定常前向[Kolmogorov方程](@entry_id:270139)。寻找一个SDE的平稳密度就等价于求解这个[二阶偏微分方程](@entry_id:175326)，并附加条件 $\rho(x) \ge 0$ 和 $\int \rho(x) dx = 1$。

Fokker-Planck方程可以被写成一个守恒律的形式 $\nabla \cdot \mathbf{J} = 0$，其中 $\mathbf{J}$ 是 **概率流 (probability flux)** 向量，其分量为：
$$
J_i(x) = b_i(x)\rho(x) - \frac{1}{2}\sum_{j=1}^d \partial_j\big(a_{ij}(x)\rho(x)\big)
$$
平稳状态意味着概率流是[无散度](@entry_id:190991)的（$\nabla \cdot \mathbf{J} = 0$），但这并不一定意味着[概率流](@entry_id:150949)本身为零（$\mathbf{J} \equiv 0$）[@problem_id:2996778]。一个系统如果满足 $\mathbf{J} \equiv 0$，则称其满足 **[细致平衡](@entry_id:145988) (detailed balance)** 条件，并且该过程是 **可逆的 (reversible)**。[可逆性](@entry_id:143146)是一个比平稳性更强的条件。

一个典型的例子是 **[过阻尼朗之万方程](@entry_id:138693) (overdamped Langevin equation)**，它描述了一个粒子在势场 $U(x)$ 中运动并受到随机力的影响：
$$
dX_t = -\nabla U(X_t) dt + \sqrt{2} dW_t
$$
这个过程是可逆的，其平稳密度是著名的吉布斯-[玻尔兹曼分布](@entry_id:142765) $\rho(x) \propto \exp(-U(x))$。只要[势场](@entry_id:143025) $U(x)$ 是强制的（即当 $|x| \to \infty$ 时 $U(x) \to \infty$），这个密度就是可归一化的，从而给出一个平稳[概率分布](@entry_id:146404) [@problem_id:2996770]。

### 不变测度的存在性：Foster-Lyapunov判据

到目前为止，我们讨论了不变测度的定义和性质。但一个根本的问题是：一个不变概率测度何时存在？对于一个SDE，其解的路径可能会漂移到无穷远处（称为 **瞬时 (transient)**），这种情况下，过程不会“稳定”在任何有限区域，也就不存在不变概率测度。

为了确保过程大部分时间停留在空间的某个有限部分，我们需要一种“[拉回](@entry_id:160816)”机制。**Foster-Lyapunov理论** 提供了一个强大的工具来证明这种稳定性。其核心思想是构造一个 **[Lyapunov函数](@entry_id:273986)** $V(x)$，它在无穷远处趋于无穷，并验证一个 **漂移条件 (drift condition)**。

一个常用且有效的漂移条件是 [@problem_id:2996758]：存在一个二次连续可微且强制的（$\lim_{|x|\to\infty} V(x) = \infty$）函数 $V: \mathbb{R}^d \to [1, \infty)$，一个紧集 $K \subset \mathbb{R}^d$，以及正常数 $c, C$，使得对于所有 $x \in \mathbb{R}^d$：
$$
\mathcal{L}V(x) \le -c + C \cdot \mathbf{1}_K(x)
$$
其中 $\mathbf{1}_K(x)$ 是集合 $K$ 的指示函数。这个条件意味着，在紧集 $K$ 之外（$x \in K^c$），我们有 $\mathcal{L}V(x) \le -c$。回顾一下，$\mathcal{L}V(X_t)$ 是 $V(X_t)$ [期望值](@entry_id:153208)的[瞬时变化率](@entry_id:141382)。因此，这个条件表明，当过程远离中心区域 $K$ 时，[Lyapunov函数](@entry_id:273986) $V$ 的[期望值](@entry_id:153208)会以一个不小于 $c$ 的速率减小，从而有效地将过程“[拉回](@entry_id:160816)”到 $K$。

这个漂移条件的一个直接后果是，从任何点 $x$ 出发，过程到达集合 $K$ 的期望时间 $\tau_K = \inf\{t \ge 0: X_t \in K\}$ 是有限的。通过Dynkin公式可以证明一个更精确的界 [@problem_id:2996758]：
$$
\mathbb{E}_x[\tau_K] \le \frac{1}{c}V(x)
$$
由于 $V(x)$ 在 $\mathbb{R}^d$ 上是无界的，这个期望时间通常不是一致有界的，而是依赖于起始点 $x$。

这种保证过程会反复返回紧集 $K$ 的性质称为 **[正常返](@entry_id:195139) (positive recurrence)**。它防止了过程逃逸到无穷远，并确保了过程的 **[经验测度](@entry_id:181007) (empirical measure)** $\mu_T = \frac{1}{T}\int_0^T \delta_{X_s} ds$ 构成的族是 **紧的 (tight)**。根据 **Krylov-Bogoliubov定理**，一个紧的测度族必有[弱收敛](@entry_id:146650)子列，且其极限点是[不变测度](@entry_id:202044)。因此，[Foster-Lyapunov漂移条件](@entry_id:749534)是证明不变概率测度存在的有力工具。

### 唯一性与遍历性

即使我们证明了不变测度的存在，接下来的问题是：它是唯一的吗？以及，过程的长期行为是否真的会收敛到这个[不变测度](@entry_id:202044)？这些问题与 **遍历性 (ergodicity)** 的概念密切相关。

#### [遍历定理](@entry_id:261967)：[大数定律](@entry_id:140915)

遍历性的核心思想是 **[时间平均](@entry_id:267915)等于[空间平均](@entry_id:203499)**。对于一个可测函数 $f: \mathbb{R}^d \to \mathbb{R}$，其时间平均是沿一条轨迹的积分：
$$
A_T(f) = \frac{1}{T}\int_0^T f(X_t) \, dt
$$
其空间平均是函数 $f$ 关于[不变测度](@entry_id:202044) $\pi$ 的积分（期望）：$\int f \, d\pi$。

[遍历定理](@entry_id:261967)（或[马尔可夫过程](@entry_id:160396)的大数定律）指出，在一定条件下，当 $T \to \infty$ 时，时间平均[几乎必然收敛](@entry_id:265812)于空间平均。对于SDE描述的[扩散过程](@entry_id:170696)，关键的条件是过程为 **正常Harris返 (positive Harris recurrent)** [@problem_id:2996770]。正常Harris返是一种结合了[正常返](@entry_id:195139)和不可约性的强遍历性质。如果一个[扩散过程](@entry_id:170696)是正常Harris返的，那么它拥有一个唯一的[平稳分布](@entry_id:194199) $\pi$，并且对于任何 $f \in L^1(\pi)$ 和任意初始条件，我们有：
$$
\lim_{T\to\infty} A_T(f) = \int_{\mathbb{R}^d} f(x) \, \pi(dx) \quad \text{a.s.}
$$

#### 遍历分解

在某些情况下，一个[马尔可夫过程](@entry_id:160396)可能拥有多个[不变测度](@entry_id:202044)，这通常发生在过程不是 **不可约 (irreducible)** 的时候（即[状态空间](@entry_id:177074)可以被分解成几个互不连通的部分）。在这种情况下，遍历性的概念依然适用，但需要更精细的描述。

**[遍历分解定理](@entry_id:180571)** 提供了一个完整的结构性图像 [@problem_id:2996763]。可以证明，所有不变概率测度构成的集合 $\mathcal{I}$ 是一个[凸集](@entry_id:155617)。而 **遍历测度 (ergodic measures)** 正是这个凸集的 **极点 (extreme points)**。遍历测度的特征是，任何在该测度下几乎处处不变的集合，其测度必须为0或1。

[遍历分解定理](@entry_id:180571)表明，任何一个不变测度 $\mu \in \mathcal{I}$ 都可以被唯一地表示为所有遍历测度（极点）的一个“混合”或积分。这意味着存在一个定义在遍历测度集 $\mathcal{E}$ 上的概率测度 $\Pi_\mu$，使得：
$$
\mu = \int_{\mathcal{E}} \nu \, \Pi_\mu(d\nu)
$$
如果一个过程具有唯一的平稳分布 $\mu_*$，那么集合 $\mathcal{I}$ 只有一个元素 $\{\mu_*\}$。这个元素本身必然是极点，因此 $\mu_*$ 是遍历的 [@problem_id:2996763]。在这种情况下，遍历分解就退化为 $\mu_* = \mu_*$。对于扩散过程，**拓扑不可约性**（从任何点出发，以正概率到达任何非空开集）加上 **强[Feller性质](@entry_id:192501)**（转移算子将有界[可测函数](@entry_id:159040)映为有界[连续函数](@entry_id:137361)）是保证[不变测度](@entry_id:202044)唯一性的充分条件 [@problem_id:2996763]。

### 收敛速率：[谱隙](@entry_id:144877)与[几何遍历性](@entry_id:191361)

[遍历定理](@entry_id:261967)告诉我们过程会收敛到平稳分布，但没有说明收敛有多快。在许多应用中，收敛速率至关重要。

#### [几何遍历性](@entry_id:191361)

如果收敛是以指数速率发生的，我们称之为 **[几何遍历性](@entry_id:191361) (geometric ergodicity)**。Harris定理的一个版本给出了[几何遍历性](@entry_id:191361)的充分条件，它需要一个更强的漂移条件和一个混合条件 [@problem_id:2996775]。对于扩散过程，混合条件（称为 **小集上的次要化条件 (minorization condition on a small set)**）通常由[扩散](@entry_id:141445)项的非退化性（例如 $\sigma\sigma^\top$ 一致正定）自动满足。关键在于一个 **几何漂移条件**：
$$
\mathcal{L}V(x) \le -\lambda V(x) + b \cdot \mathbf{1}_C(x)
$$
其中 $V$ 是一个Lyapunov函数，$C$ 是一个[紧集](@entry_id:147575)，$\lambda > 0, b  \infty$ 是常数。这个条件表明，在 $C$ 之外，$V(X_t)$ 的[期望值](@entry_id:153208)以与其自身大小成正比的速率指数衰减。这确保了过程不仅会返回中心区域，而且返回得非常快。满足这些条件的过程，其转移概率 $P^t(x, \cdot)$ 会以指数速率收敛到唯一的[平稳分布](@entry_id:194199) $\pi$。

#### [谱隙](@entry_id:144877)与[可逆过程](@entry_id:276625)

对于一类特别重要且结构良好的过程——**可逆过程**（例如朗之万方程），收敛速率可以通过生成元 $\mathcal{L}$ 的谱性质来精确刻画。对于一个关于[平稳分布](@entry_id:194199) $\pi$ 可逆的过程，其生成元 $\mathcal{L}$ 是[希尔伯特空间](@entry_id:261193) $L^2(\pi)$ 上的一个[自伴算子](@entry_id:152188)。

由于 $\mathcal{L}$ 是一个非[正算子](@entry_id:263696)，其谱位于 $(-\infty, 0]$。[常数函数](@entry_id:152060)是[特征值](@entry_id:154894)为0的特征函数。如果过程是遍历的，0是一个孤立的、单重的[特征值](@entry_id:154894)。**谱隙 (spectral gap)** $\lambda_1$ 定义为 $-\mathcal{L}$ 的最小正[特征值](@entry_id:154894) [@problem_id:2996742]。它量化了0[特征值](@entry_id:154894)与谱的其他部分之间的距离。[谱隙](@entry_id:144877)可以通过[Rayleigh商](@entry_id:137794)来定义：
$$
\lambda_1 = \inf \left\{ \frac{-\langle \mathcal{L}f, f \rangle_\pi}{\|f - \int f d\pi\|_2^2} : f \in \mathrm{Dom}(\mathcal{L}), f \text{ is not constant} \right\}
$$
其中 $\langle \cdot, \cdot \rangle_\pi$ 和 $\|\cdot\|_2$ 分别表示 $L^2(\pi)$ 空间中的[内积](@entry_id:158127)和范数。

[谱隙](@entry_id:144877)的存在性（$\lambda_1 > 0$）直接导致了在 $L^2(\pi)$ 范数下的[指数收敛](@entry_id:142080)。具体来说，对于任何函数 $f \in L^2(\pi)$，我们有 [@problem_id:2996742]：
$$
\|P_t f - \int f \, d\pi\|_{L^2(\pi)} \le e^{-\lambda_1 t} \|f - \int f \, d\pi\|_{L^2(\pi)}
$$
这个优美的结果将[随机过程](@entry_id:159502)的收敛行为与泛函分析中的谱理论紧密地联系在一起。[谱隙](@entry_id:144877)越大，过程向其平稳分布的收敛就越快。