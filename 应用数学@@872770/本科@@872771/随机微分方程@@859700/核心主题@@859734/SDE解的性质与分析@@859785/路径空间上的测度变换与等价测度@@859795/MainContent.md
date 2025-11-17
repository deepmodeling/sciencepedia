## 引言
在[随机分析](@entry_id:188809)领域，路径空间上的[测度变换](@entry_id:157887)是一个极其强大而优美的工具。它允许我们在不同的“概率世界”之间进行切换，从而极大地简化对复杂[随机过程](@entry_id:159502)的分析。许多[随机过程](@entry_id:159502)在“真实世界”的[概率测度](@entry_id:190821)下具有复杂的动态行为（例如，带有漂移），这给计算和分析带来了巨大挑战。本文旨在解决这一知识鸿沟，即如何系统地改变一个过程的动态，使其在新的概率测度下变得更易于处理，例如，变成一个标准的布朗运动。

通过本文的学习，读者将深入理解[测度变换](@entry_id:157887)的核心思想。在“原理与机制”一章中，我们将奠定理论基础，详细阐述[绝对连续性](@entry_id:144513)、[等价测度](@entry_id:634447)以及作为核心的[吉尔萨诺夫定理](@entry_id:147068)。随后的“应用与[交叉](@entry_id:147634)学科联系”一章将展示这些理论的巨大威力，探讨其如何成为[金融数学](@entry_id:143286)中[风险中性定价](@entry_id:144172)的基石，并应用于简化概率计算和证明随机微分方程的理论性质。最后，通过“动手实践”部分提供的练习，您将有机会亲手应用这些概念，巩固所学知识。

## 原理与机制

在上一章引言的基础上，本章将深入探讨路径空间上[测度变换](@entry_id:157887)的数学原理与核心机制。我们将从测度论的基本概念出发，系统地阐述如何通过[等价测度](@entry_id:634447)变换来改变[随机过程](@entry_id:159502)的漂移，同时保持其波动性不变。这一技术不仅是[随机分析](@entry_id:188809)理论的基石，也在[金融数学](@entry_id:143286)等应用领域扮演着至关重要的角色。

### [绝对连续性](@entry_id:144513)与测度等价

在[随机过程](@entry_id:159502)的分析中，我们常常需要在同一个[样本空间](@entry_id:275301)上考虑不同的概率测度。例如，一个过程在一种“真实世界”测度下可能具有某种复杂的动态，而在另一种精心构造的“风险中性”测度下，其动态可能变得更易于分析。连接不同测度的桥梁是测度论中的**[绝对连续性](@entry_id:144513)（absolute continuity）**与**测度等价（equivalence of measures）**的概念。

给定一个[可测空间](@entry_id:189701) $(\Omega, \mathcal{F})$ 上的两个概率测度 $\mathbb{P}$ 和 $\mathbb{Q}$，我们称 $\mathbb{Q}$ 关于 $\mathbb{P}$ 是**绝对连续的**，记作 $\mathbb{Q} \ll \mathbb{P}$，如果对于任何事件 $A \in \mathcal{F}$，只要 $\mathbb{P}(A) = 0$，就有 $\mathbb{Q}(A) = 0$。直观地说，这意味着在 $\mathbb{P}$ 测度下不可能发生的事件，在 $\mathbb{Q}$ 测度下也绝不可能发生。

一个更强的关系是**测度等价**，记作 $\mathbb{Q} \sim \mathbb{P}$。当 $\mathbb{Q} \ll \mathbb{P}$ 且 $\mathbb{P} \ll \mathbb{Q}$ 同时成立时，我们称这两个测度是等价的。测度等价的核心意义在于，两个测度拥有完全相同的**[零测集](@entry_id:157694)（null sets）**。换言之，对于任何事件 $A \in \mathcal{F}$，$\mathbb{P}(A) = 0$ 当且仅当 $\mathbb{Q}(A) = 0$。[@problem_id:3043580]

这一性质具有深远的影响。在概率论中，许多重要的性质都是以“[几乎必然](@entry_id:262518)”（almost surely, a.s.）的方式成立的，即该性质在其不成立的样本点集合（一个[零测集](@entry_id:157694)）之外都成立。由于[等价测度](@entry_id:634447)共享相同的[零测集](@entry_id:157694)，一个在 $\mathbb{P}$ 测度下[几乎必然](@entry_id:262518)成立的性质，在任何与之等价的测度 $\mathbb{Q}$ 下也必然几乎必然成立。

一个典型的例子是[布朗运动路径](@entry_id:274361)的连续性。经典构造表明，[标准布朗运动](@entry_id:197332) $W = (W_t)_{t \in [0,T]}$ 的样本路径在 $\mathbb{P}$ 测度下是几乎必然连续的。这意味着，所有不连续的路径组成的集合是一个 $\mathbb{P}$-零测集。如果我们通过一个[等价测度](@entry_id:634447)变换得到一个新的测度 $\mathbb{Q}$，那么由于 $\mathbb{Q} \sim \mathbb{P}$，这个不连续路径的集合也必然是一个 $\mathbb{Q}$-零测集。因此，在新的测度 $\mathbb{Q}$ 下，过程 $W$ 的样本路径也几乎必然是连续的。[@problem_id:3043734] [等价测度](@entry_id:634447)变换保留了路径的拓扑性质。

根据**[拉东-尼科迪姆定理](@entry_id:161238)（Radon-Nikodým Theorem）**，如果 $\mathbb{Q} \ll \mathbb{P}$，那么存在一个非负的、$\mathcal{F}$-可测的[随机变量](@entry_id:195330) $Z$，称为**[拉东-尼科迪姆导数](@entry_id:158399)**（或密度），使得对于任意事件 $A \in \mathcal{F}$，我们有：
$$
\mathbb{Q}(A) = \mathbb{E}_{\mathbb{P}}[Z \cdot \mathbf{1}_A] = \int_A Z \,d\mathbb{P}
$$
其中 $\mathbf{1}_A$ 是事件 $A$ 的[示性函数](@entry_id:261577)。我们常记作 $Z = \frac{d\mathbb{Q}}{d\mathbb{P}}$。由于 $\mathbb{Q}$ 是一个[概率测度](@entry_id:190821)，令 $A=\Omega$ 可得 $\mathbb{E}_{\mathbb{P}}[Z] = \mathbb{Q}(\Omega) = 1$。反之，任何满足 $\mathbb{E}_{\mathbb{P}}[Z] = 1$ 的非负[随机变量](@entry_id:195330) $Z$ 都可以用来定义一个新的概率测度 $\mathbb{Q}$。

在此基础上，测度等价的条件可以简洁地用[拉东-尼科迪姆导数](@entry_id:158399)来刻画：$\mathbb{Q} \sim \mathbb{P}$ 当且仅当 $\frac{d\mathbb{Q}}{d\mathbb{P}} > 0$ 在 $\mathbb{P}$ 测度下几乎必然成立。[@problem_id:3043580] 这个严格为正的条件保证了我们可以定义反向的导数 $\frac{d\mathbb{P}}{d\mathbb{Q}} = \left(\frac{d\mathbb{Q}}{d\mathbb{P}}\right)^{-1}$，从而确保了 $\mathbb{P} \ll \mathbb{Q}$。

### Girsanov 定理：改变过程的漂移

Girsanov 定理是路径空间上[测度变换](@entry_id:157887)理论的核心，它精确地描述了如何通过一个[等价测度](@entry_id:634447)变换来为一个连续[随机过程](@entry_id:159502)（特别是布朗运动）引入一个可控的**漂移（drift）**，而保持其**波动性（volatility）**或二次变差结构不变。

考虑一个赋有标准 $(\mathcal{F}_t)$-布朗运动 $W = (W_t)_{t \in [0,T]}$ 的滤波概率空间 $(\Omega, \mathcal{F}, (\mathcal{F}_t)_{t \in [0,T]}, \mathbb{P})$。设 $\theta = (\theta_t)_{t \in [0,T]}$ 是一个满足一定可积性条件的 $(\mathcal{F}_t)$-[适应过程](@entry_id:187710)。我们的目标是构造一个新的测度 $\mathbb{Q}$，使得在该测度下，过程 $W$ 表现为一个具有漂移项 $\theta$ 的过程。

Girsanov 定理指出，实现这一目标的[拉东-尼科迪姆导数](@entry_id:158399)过程 $Z_t = \frac{d\mathbb{Q}}{d\mathbb{P}}\big|_{\mathcal{F}_t}$ 应取为如下形式的**[随机指数](@entry_id:197698)（stochastic exponential）**，也称为**Doléans-Dade 指数**：
$$
Z_t = \mathcal{E}(M)_t := \exp\left(M_t - \frac{1}{2}\langle M \rangle_t\right)
$$
其中 $M_t = \int_0^t \theta_s dW_s$ 是一个[连续局部鞅](@entry_id:204638)，而 $\langle M \rangle_t = \int_0^t \theta_s^2 ds$ 是其二次变差过程。

在适当的技术条件下（我们将在后文讨论），过程 $(Z_t)_{t \in [0,T]}$ 是一个 $\mathbb{P}$-[鞅](@entry_id:267779)，且 $\mathbb{E}_{\mathbb{P}}[Z_T] = Z_0 = 1$。由于[指数函数](@entry_id:161417)恒为正，$Z_T > 0$ 几乎必然成立，因此由 $Z_T$ 定义的测度 $\mathbb{Q}$ 与 $\mathbb{P}$ 是等价的。

**Girsanov 定理**：设 $\mathbb{Q}$ 是由上述密度 $Z_T = \mathcal{E}(\int \theta_s dW_s)_T$ 定义的概率测度。那么，过程 $\widetilde{W} = (\widetilde{W}_t)_{t \in [0,T]}$，定义为：
$$
\widetilde{W}_t = W_t - \int_0^t \theta_s ds
$$
在测度 $\mathbb{Q}$ 下是一个标准布朗运动。

这个结论等价于，在新的测度 $\mathbb{Q}$ 下，原过程 $W$ 的动态可以表示为：
$$
dW_t = \theta_t dt + d\widetilde{W}_t
$$
其中 $\widetilde{W}$ 是一个 $\mathbb{Q}$-布朗运动。这表明，通过这次[测度变换](@entry_id:157887)，我们成功地为 $W$ 引入了一个由过程 $\theta$ 描述的瞬时漂移，而其随机扰动部分仍然是一个标准布朗运动的增量。[@problem_id:3043605] [@problem_id:3043585]

### Girsanov 定理背后的机制：二次变差的[不变性](@entry_id:140168)

Girsanov 定理为何能精确地实现漂移的改变而保持波动性不变？其深刻的机制在于**二次变差（quadratic variation）**的**路径性质（pathwise property）**。

首先，一个[连续半鞅](@entry_id:636909)的二次变差 $[X]_t$ 是通过其样本路径的平方增量和在分割加密时的极限来定义的。这意味着，$[X]_t$ 的值完全由单条样本路径 $\omega \mapsto X_s(\omega)$ for $s \in [0,t]$ 所决定，而与定义在[样本空间](@entry_id:275301)上的概率测度无关。

[等价测度](@entry_id:634447)变换 $\mathbb{Q} \sim \mathbb{P}$ 的本质是重新分配整个[样本空间](@entry_id:275301)中路径的“权重”或“概率”，但它并不会改变任何一条路径本身。因此，对于任何一条路径 $\omega$，其二次变差的计算结果是唯一的。一个在 $\mathbb{P}$ 测度下[几乎必然](@entry_id:262518)成立的路径恒等式，例如对于[标准布朗运动](@entry_id:197332) $W$ 有 $[W]_t = t$ 对所有 $t$ 成立，在任何[等价测度](@entry_id:634447) $\mathbb{Q}$ 下也必定[几乎必然](@entry_id:262518)成立。[@problem_id:3063557]

现在我们来考察 Girsanov 变换中的过程 $\widetilde{W}_t = W_t - \int_0^t \theta_s ds$。它的二次变差可以计算如下：
$$
[\widetilde{W}]_t = \left[W - \int_0^\cdot \theta_s ds\right]_t = [W]_t - 2\left[W, \int_0^\cdot \theta_s ds\right]_t + \left[\int_0^\cdot \theta_s ds\right]_t
$$
在 Girsanov 定理的条件下，$\int_0^t \theta_s ds$ 是一个**[有界变差](@entry_id:139291)过程（finite variation process）**。一个基本的性质是，任何连续[有界变差](@entry_id:139291)过程的二次变差为零，并且它与任何[连续局部鞅](@entry_id:204638)的二次协变差（quadratic covariation）也为零。因此，上式中的后两项均为零。我们得到一个关键的路径恒等式：
$$
[\widetilde{W}]_t = [W]_t
$$
由于在 $\mathbb{P}$ 测度下，$[W]_t = t$ 几乎必然成立，所以 $[\widetilde{W}]_t = t$ 这个路径关系也在 $\mathbb{P}$ 测度下[几乎必然](@entry_id:262518)成立。因为 $\mathbb{Q}$ 与 $\mathbb{P}$ 等价，这个关系在 $\mathbb{Q}$ 测度下同样[几乎必然](@entry_id:262518)成立。[@problem_id:3063557]

Girsanov 定理的精妙之处在于，它构造的密度过程 $Z_t$ 恰好能使得过程 $\widetilde{W}_t$ 在新测度 $\mathbb{Q}$ 下成为一个（局部）鞅。根据**Lévy 对布朗运动的刻画**，一个二次变差为 $[X]_t=t$ 的[连续局部鞅](@entry_id:204638)必定是一个标准布朗运动。因此，$\widetilde{W}_t$ 在 $\mathbb{Q}$ 下就是一个[标准布朗运动](@entry_id:197332)。

这个机制也揭示了[等价测度](@entry_id:634447)变换的局限性。例如，我们无法通过[等价测度](@entry_id:634447)变换将一个布朗运动 $W_t$（其二次变差密度为 $d[W]_t/dt = 1$）变成一个具有不同二次变差结构的过程，比如一个[时间变换](@entry_id:634205)后的布朗运动 $Y_t = W_{\tau(t)}$，其二次变差密度为 $d[Y]_t/dt = \dot{\tau}(t) \neq 1$。因为二次变差是路径的内禀属性，[等价测度](@entry_id:634447)变换无法改变它。任何试图改变波动率（二次变差密度）的变换，都将导致新旧测度之间不再等价。[@problem_id:3043592]

### 等价性与奇异性：一个根本性的二分法

综合以上讨论，我们可以总结出路径空间上[高斯测度](@entry_id:749747)变换的一个根本性二分法：改变漂移可以得到[等价测度](@entry_id:634447)，而改变波动率则会导致**奇异性（singularity）**。如果两个测度 $\mu$ 和 $\nu$ 是相互奇异的，意味着存在一个事件 $A$，使得 $\mu(A)=1$ 而 $\nu(A)=0$。

#### 情形一：改变漂移

- **确定性漂移 (Cameron-Martin 定理)**：考虑将标准布朗运动 $W_t$ 平移一个确定性函数 $h(t)$，得到新过程 $X_t = W_t + h(t)$。其对应的测度是否与[维纳测度](@entry_id:189476)等价？**Cameron-Martin 定理**给出了精确的回答：等价性成立当且仅当平移函数 $h(t)$ 属于一个特定的[希尔伯特空间](@entry_id:261193)，即 **Cameron-Martin 空间** $\mathcal{H}$。该空间由所有绝对连续且其导数的平方在 $[0,T]$上可积的函数构成：
  $$
  \mathcal{H} = \left\{ h \in C([0,T]; \mathbb{R}) : h(0)=0, h \text{ 绝对连续, 且 } \int_0^T |\dot{h}(t)|^2 dt  \infty \right\}
  $$
  如果 $h \in \mathcal{H}$，那么 $X_t$ 的测度与 $W_t$ 的测度是等价的，其[拉东-尼科迪姆导数](@entry_id:158399)为：
  $$
  \frac{d\nu_h}{d\mu_W}(\omega) = \exp\left( \int_0^T \dot{h}(t) \cdot dW_t(\omega) - \frac{1}{2} \int_0^T |\dot{h}(t)|^2 dt \right)
  $$
  如果 $h \notin \mathcal{H}$（例如，$h$ 不够光滑），那么这两个测度就是相互奇异的。[@problem_id:3043611] [@problem_id:3043606]

- **随机漂移 (Girsanov 定理)**：如前所述，如果漂移项 $\int_0^t \theta_s ds$ 是随机的，只要 $\theta$ 满足适当的条件（例如[Novikov条件](@entry_id:634732)），我们得到的测度仍然是等价的。[@problem_id:3043606]

#### 情形二：改变波动率

与改变漂移形成鲜明对比的是改变波动率。考虑过程 $X_t = \sigma W_t$，其中 $\sigma > 0$ 且 $\sigma \neq 1$。这个过程的二次变差为 $[X]_t = \sigma^2 [W]_t = \sigma^2 t$。描述 $W_t$ 的[维纳测度](@entry_id:189476) $\mu_1$ 将其全部“质量”赋予了二次变差为 $t$ 的路径集合上。而描述 $X_t$ 的测度 $\mu_\sigma$ 则将其全部“质量”赋予了二次变差为 $\sigma^2 t$ 的路径集合上。由于 $\sigma \neq 1$，这两个路径集合是互不相交的。因此，测度 $\mu_1$ 和 $\mu_\sigma$ 是相互奇异的。

这一结论是更广义的 **Feldman-Hajek [二分法](@entry_id:140816)定理** 的一个体现，该定理指出两个[高斯测度](@entry_id:749747)要么等价，要么相互奇异，不存在中间情况。对于中心化[高斯测度](@entry_id:749747)，其等价性取决于它们的协[方差](@entry_id:200758)算子之差是否为[希尔伯特-施密特算子](@entry_id:271274)。对于 $W_t$ 和 $\sigma W_t$，这个条件不满足，因此它们是奇异的。[@problem_id:3043606]

这个[二分法](@entry_id:140816)是理解[测度变换](@entry_id:157887)的关键：**[等价测度](@entry_id:634447)变换可以改变连续过程的漂移，但不能改变其[扩散](@entry_id:141445)系数或波动性**。

### 技术条件与进阶主题

#### 密度过程的鞅性

Girsanov 定理的应用依赖于一个关键的技术前提：密度过程 $Z_t = \mathcal{E}(M)_t$ 必须是一个真正的**鞅（martingale）**，而不仅仅是**[局部鞅](@entry_id:186755)（local martingale）**。任何非负的[局部鞅](@entry_id:186755)都是一个[超鞅](@entry_id:271504)，这意味着 $\mathbb{E}[Z_t] \le Z_0 = 1$。要使其成为一个合法的[概率密度](@entry_id:175496)，我们需要 $\mathbb{E}[Z_T]=1$，这等价于要求 $(Z_t)_{t \in [0,T]}$ 是一个（[一致可积](@entry_id:202893)的）真鞅。

有多个充分条件可以保证这一点，其中最著名的是 **Novikov 条件**和 **Kazamaki 条件**。

- **Novikov 条件**: 如果 $\mathbb{E}_{\mathbb{P}}\left[\exp\left(\frac{1}{2}\langle M \rangle_T\right)\right]  \infty$，则 $\mathcal{E}(M)$ 是一个真[鞅](@entry_id:267779)。

- **Kazamaki 条件**: 如果 $\exp(\frac{1}{2}M_t)$ 是一个[下鞅](@entry_id:263978)且 $\sup_{t \in [0,T]} \mathbb{E}_{\mathbb{P}}[\exp(\frac{1}{2}M_t)]  \infty$，则 $\mathcal{E}(M)$ 是一个真鞅。

Kazamaki 条件通常比 Novikov 条件更弱（即更通用）。例如，考虑 $M_t = \xi W_t$，其中 $\xi \sim \mathcal{N}(0, \sigma^2)$ 是一个独立于 $W$ 的[随机变量](@entry_id:195330)。在这种情况下，$\langle M \rangle_T = \xi^2 T$。通过计算可以发现，Novikov 条件成立当且仅当 $T  1/\sigma^2$，而 Kazamaki 条件成立当且仅当 $T  4/\sigma^2$。因此，在时间区间 $1/\sigma^2 \le T  4/\sigma^2$ 内，Novikov 条件失效，但 Kazamaki 条件仍然成立，保证了 $\mathcal{E}(M)$ 是一个真[鞅](@entry_id:267779)。[@problem_id:3043613]

#### 局部等价与全局等价

最后，我们需要区分**局部等价（local equivalence）**和**全局等价（global equivalence）**，尤其是在处理无限时间区间 $[0, \infty)$ 上的过程时。如果两个测度 $\mathbb{P}$ 和 $\mathbb{Q}$ 在每个有限时间区间的 $\sigma$-代数 $\mathcal{F}_t$ 上都是等价的，我们称它们是局部等价的。

然而，局部等价并不一定能“升级”为在**尾部 $\sigma$-代数（tail $\sigma$-algebra）** $\mathcal{T} = \bigcap_{t \ge 0} \sigma(X_s : s \ge t)$ 上的等价。尾部 $\sigma$-代数描述的是过程的长期渐近行为。

一个经典的例子再次来自 Girsanov 定理。设 $\mathbb{P}$ 为[维纳测度](@entry_id:189476)，$\mathbb{Q}$ 由密度过程 $Z_t = \exp(\mu W_t - \frac{1}{2}\mu^2 t)$ 定义，其中 $W_t$ 是 $\mathbb{P}$-布朗运动，$\mu \neq 0$。对于任何有限的 $t$，$\mathbb{P}$ 和 $\mathbb{Q}$ 在 $\mathcal{F}_t$ 上都是等价的，因此它们是局部等价的。然而，在无限时间上，这个密度[鞅](@entry_id:267779) $(Z_t)_{t \ge 0}$ 并不是[一致可积](@entry_id:202893)的，它会几乎必然地收敛到 $Z_\infty = 0$。这意味着在“无穷远处”，两个测度变得相互奇异。

这种奇异性体现在尾部事件的概率上。例如，考虑尾部事件 $A = \{ \lim_{t \to \infty} W_t/t = \mu \}$。根据布朗运动的强大数定律，在 $\mathbb{P}$ 测度下，$\lim_{t \to \infty} W_t/t = 0$ 几乎必然成立，因此 $\mathbb{P}(A)=0$。然而，在 $\mathbb{Q}$ 测度下，$W_t$ 是一个带有漂移 $\mu$ 的布朗运动，因此 $\lim_{t \to \infty} W_t/t = \mu$ [几乎必然](@entry_id:262518)成立，即 $\mathbb{Q}(A)=1$。由于我们找到了一个尾部事件 $A$，使得 $\mathbb{P}(A)=0$ 而 $\mathbb{Q}(A)=1$，这两个测度在尾部 $\sigma$-代数 $\mathcal{T}$ 上是相互奇异的。这个例子清晰地表明，局部等价是一个比在尾部代数上等价更弱的概念。[@problem_id:3043616]