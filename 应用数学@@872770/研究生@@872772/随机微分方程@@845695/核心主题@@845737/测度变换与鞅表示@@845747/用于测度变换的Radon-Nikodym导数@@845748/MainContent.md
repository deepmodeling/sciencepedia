## 引言
[测度变换](@entry_id:157887)是现代概率论和[随机分析](@entry_id:188809)中一个极其强大且优雅的工具。其核心思想在于，我们可以通过一种严谨的数学方式改变随机事件发生的概率，从而将一个复杂的[随机系统](@entry_id:187663)转化为一个在不同“概率世界”中更易于分析的等价系统。这一概念的重要性不仅体现在其深刻的数学结构上，更在于它为金融、物理、信息论等多个领域的关键问题提供了统一的解决框架。然而，理解从静态的[拉东-尼科迪姆导数](@entry_id:158399)到动态的[吉尔萨诺夫定理](@entry_id:147068)的演进，以及它们如何从抽象理论走向实际应用，对许多学习者来说是一个挑战。

本文旨在系统性地填补这一认知鸿沟。我们将带领读者深入探索[测度变换](@entry_id:157887)的理论与实践，从数学基础到前沿应用。
- 在“原理与机制”一章中，我们将从[拉东-尼科迪姆定理](@entry_id:161238)出发，建立[测度变换](@entry_id:157887)的静态基础，并逐步过渡到[随机过程](@entry_id:159502)中动态的密度过程和[吉尔萨诺夫定理](@entry_id:147068)，揭示其如何改变[随机过程](@entry_id:159502)的“定律”。
- 随后的“应用与跨学科联系”一章将展示这些理论的巨大威力，我们将看到[测度变换](@entry_id:157887)如何成为金融[资产定价](@entry_id:144427)的基石、如何量化信息论中的[模型差异](@entry_id:198101)，以及如何解决信号处理中的滤波难题。
- 最后，“动手实践”部分提供了精选的练习，旨在通过具体计算加深读者对核心概念的理解。

通过这一结构化的学习路径，读者将不仅掌握[测度变换](@entry_id:157887)的数学精髓，更能领会其作为一种“通用语言”在不同学科间建立深刻联系的强大能力。

## 原理与机制

在本章中，我们将深入探讨[测度变换](@entry_id:157887)的核心理论与机制。[测度变换](@entry_id:157887)是[随机分析](@entry_id:188809)中的一个基本工具，它允许我们改变一个[随机过程](@entry_id:159502)的概率定律，例如，将一个无漂移的布朗运动转变为一个[带漂移的布朗运动](@entry_id:275071)。这一过程的数学基础是[Radon-Nikodym定理](@entry_id:161238)，而其在[随机过程](@entry_id:159502)中的实现则通过[Girsanov定理](@entry_id:147068)来完成。我们将从基本定义出发，系统地建立起这一理论框架，并展示其在包含跳跃的一般[半鞅](@entry_id:184490)中的应用。

### [Radon-Nikodym定理](@entry_id:161238)：[测度变换](@entry_id:157887)的基石

在讨论[随机过程](@entry_id:159502)的动态行为之前，我们必须首先理解其静态的[概率基础](@entry_id:187304)。[测度变换](@entry_id:157887)的整个理论都建立在[测度论](@entry_id:139744)中的一个基本结果之上：[Radon-Nikodym定理](@entry_id:161238)。

#### [绝对连续性](@entry_id:144513)与测度等价性

考虑一个[可测空间](@entry_id:189701) $(\Omega, \mathcal{F})$ 以及其上的两个概率测度 $\mathbb{P}$ 和 $\mathbb{Q}$。我们说测度 $\mathbb{Q}$ **关于** $\mathbb{P}$ 是**绝对连续的** (absolutely continuous)，记作 $\mathbb{Q} \ll \mathbb{P}$，如果对于任何事件 $A \in \mathcal{F}$，只要 $\mathbb{P}(A) = 0$，就有 $\mathbb{Q}(A) = 0$。直观地说，这意味着任何在 $\mathbb{P}$ 测度下不可能发生的事件，在 $\mathbb{Q}$ 测度下也必然不可能发生。[@problem_id:2992602]

一个更强的关系是**测度等价性** (measure equivalence)。如果 $\mathbb{Q} \ll \mathbb{P}$ 且 $\mathbb{P} \ll \mathbb{Q}$，我们称测度 $\mathbb{P}$ 和 $\mathbb{Q}$ 是等价的，记作 $\mathbb{Q} \sim \mathbb{P}$。这意味着两个测度拥有完全相同的[零测集](@entry_id:157694)，即对于任何事件 $A \in \mathcal{F}$，$\mathbb{P}(A) = 0$ 当且仅当 $\mathbb{Q}(A) = 0$。换言之，在两种测度下，“不可能”的事件是完全相同的。[@problem_id:2992602]

#### 定理与[Radon-Nikodym导数](@entry_id:158399)

[Radon-Nikodym定理](@entry_id:161238)为我们提供了一种在绝对连续条件下用一个测度来表示另一个测度的方法。

**[Radon-Nikodym定理](@entry_id:161238)**：令 $(\Omega, \mathcal{F})$ 为一个[可测空间](@entry_id:189701)，$\mu$ 和 $\nu$ 为其上的两个非负测度。如果 $\nu \ll \mu$ 并且 $\mu$ 是 **$\sigma$-有限的** ($\sigma$-finite)，那么存在一个非负的[可测函数](@entry_id:159040) $f: \Omega \to [0, \infty]$，使得对于所有 $A \in \mathcal{F}$，我们有：
$$
\nu(A) = \int_A f \, d\mu
$$
这个函数 $f$ 被称为 $\nu$ 关于 $\mu$ 的 **[Radon-Nikodym导数](@entry_id:158399)** (或密度)，记作 $f = \frac{d\nu}{d\mu}$。此外，这个函数在 $\mu$-几乎处处意义下是唯一的。[@problem_id:2992638]

在概率论的背景下，这个定理变得尤为简洁。我们考虑两个概率测度 $\mathbb{P}$ 和 $\mathbb{Q}$。由于任何概率测度都是[有限测度](@entry_id:183212)（$\mathbb{P}(\Omega) = 1  \infty$），它自动满足 $\sigma$-有限性条件。因此，应用[Radon-Nikodym定理](@entry_id:161238)的唯一关键前提就是[绝对连续性](@entry_id:144513) $\mathbb{Q} \ll \mathbb{P}$。当此条件满足时，存在一个非负的、$\mathcal{F}$-可测的[随机变量](@entry_id:195330) $Z$，我们称之为[Radon-Nikodym导数](@entry_id:158399)，使得对于所有 $A \in \mathcal{F}$：
$$
\mathbb{Q}(A) = \int_A Z \, d\mathbb{P} = \mathbb{E}_{\mathbb{P}}[Z \mathbf{1}_A]
$$
这里 $\mathbf{1}_A$ 是事件 $A$ 的指示函数。这个[随机变量](@entry_id:195330) $Z$ 在 $\mathbb{P}$-[几乎必然](@entry_id:262518)（$\mathbb{P}$-a.s.）意义下是唯一的。这意味着任何两个满足上述条件的[随机变量](@entry_id:195330) $Z$ 和 $Z'$，必然在概率为1的集合上相等，即 $\mathbb{P}(Z=Z')=1$。这个唯一性是相对于基测度 $\mathbb{P}$ 而言的。[@problem_id:2992632]

由于 $\mathbb{Q}$ 是一个概率测度，我们有 $\mathbb{Q}(\Omega) = 1$。将 $A = \Omega$ 代入上式，我们得到一个至关重要的性质：
$$
\mathbb{E}_{\mathbb{P}}[Z] = \int_\Omega Z \, d\mathbb{P} = \mathbb{Q}(\Omega) = 1
$$
因此，任何代表概率测度变换的[Radon-Nikodym导数](@entry_id:158399) $Z$ 必须是一个非负且在 $\mathbb{P}$ 测度下期望为1的[随机变量](@entry_id:195330)。

#### [Radon-Nikodym导数](@entry_id:158399)的性质

[Radon-Nikodym导数](@entry_id:158399) $Z = \frac{d\mathbb{Q}}{d\mathbb{P}}$ 的性质与两个测度之间的关系密切相关。
*   **[绝对连续性](@entry_id:144513)与非负性**：$\mathbb{Q} \ll \mathbb{P}$ 的存在性条件直接保证了 $Z \ge 0$ ($\mathbb{P}$-a.s.) 且 $\mathbb{E}_{\mathbb{P}}[Z] = 1$。
*   **等价性与严格正性**：测度等价性 $\mathbb{Q} \sim \mathbb{P}$ 的条件更为严格，它要求[Radon-Nikodym导数](@entry_id:158399)是**严格正的**。具体来说，$\mathbb{Q} \sim \mathbb{P}$ 当且仅当 $Z > 0$ ($\mathbb{P}$-a.s.)。[@problem_id:2992603]

为什么严格正性是等价性的关键？如果存在一个集合 $N = \{\omega \mid Z(\omega) = 0\}$ 且 $\mathbb{P}(N) > 0$，那么我们有 $\mathbb{Q}(N) = \int_N Z \, d\mathbb{P} = \int_N 0 \, d\mathbb{P} = 0$。这意味着一个在 $\mathbb{P}$ 下可能发生（概率大于0）的事件，在 $\mathbb{Q}$ 下却是不可能的（概率为0）。这就破坏了 $\mathbb{P} \ll \mathbb{Q}$ 的关系，因此两个测度不是等价的。反之，如果 $Z>0$ ($\mathbb{P}$-a.s.)，那么任何满足 $\mathbb{Q}(A)=0$ 的事件 $A$ 必然有 $\int_A Z \, d\mathbb{P} = 0$，这只有在 $\mathbb{P}(A)=0$ 时才可能成立，从而保证了 $\mathbb{P} \ll \mathbb{Q}$。

此外，如果 $\mathbb{Q} \sim \mathbb{P}$，那么我们不仅可以定义 $Z = \frac{d\mathbb{Q}}{d\mathbb{P}}$，还可以定义其逆导数 $Y = \frac{d\mathbb{P}}{d\mathbb{Q}}$。它们之间存在一个简单的关系：$Y = 1/Z$ ($\mathbb{P}$-a.s. 或 $\mathbb{Q}$-a.s.)。[@problem_id:2992602]

### [随机过程](@entry_id:159502)中的[测度变换](@entry_id:157887)

当我们将[测度变换](@entry_id:157887)的概念应用于[随机过程](@entry_id:159502)时，我们关注的是在连续时间流中的动态变化。这需要我们将[Radon-Nikodym导数](@entry_id:158399)从一个固定的[随机变量](@entry_id:195330)扩展到一个[随机过程](@entry_id:159502)。

#### 密度过程与[鞅性质](@entry_id:261270)

假设我们有一个带信息流 $(\mathcal{F}_t)_{t \ge 0}$ 的滤波概率空间。我们希望定义一个与 $\mathbb{P}$ 在每个 $\mathcal{F}_t$ 上都等价的测度 $\mathbb{Q}$。对于每个时刻 $t$，我们可以定义一个[Radon-Nikodym导数](@entry_id:158399) $Z_t = \frac{d\mathbb{Q}|_{\mathcal{F}_t}}{d\mathbb{P}|_{\mathcal{F}_t}}$，其中 $\mathbb{Q}|_{\mathcal{F}_t}$ 和 $\mathbb{P}|_{\mathcal{F}_t}$ 分别是测度 $\mathbb{Q}$ 和 $\mathbb{P}$ 在 $\sigma$-代数 $\mathcal{F}_t$ 上的限制。

这个[随机过程](@entry_id:159502) $(Z_t)_{t \ge 0}$ 被称为**密度过程** (density process)。为了使在不同时间定义的测度系列 $(\mathbb{Q}|_{\mathcal{F}_t})$ 保持一致（即对于 $s  t$ 和任意 $A \in \mathcal{F}_s$，有 $\mathbb{Q}|_{\mathcal{F}_t}(A) = \mathbb{Q}|_{\mathcal{F}_s}(A)$），密度过程 $(Z_t)$ 必须是一个 **$\mathbb{P}$-鞅** (martingale)。这可以通过[条件期望](@entry_id:159140)的塔式性质来验证：
$$
\mathbb{Q}|_{\mathcal{F}_t}(A) = \mathbb{E}_{\mathbb{P}}[Z_t \mathbf{1}_A] = \mathbb{E}_{\mathbb{P}}[\mathbb{E}_{\mathbb{P}}[Z_t \mathbf{1}_A | \mathcal{F}_s]] = \mathbb{E}_{\mathbb{P}}[\mathbf{1}_A \mathbb{E}_{\mathbb{P}}[Z_t | \mathcal{F}_s]]
$$
而 $\mathbb{Q}|_{\mathcal{F}_s}(A) = \mathbb{E}_{\mathbb{P}}[Z_s \mathbf{1}_A]$。为了使两者相等，我们必须有 $Z_s = \mathbb{E}_{\mathbb{P}}[Z_t | \mathcal{F}_s]$ 对于所有 $s  t$ 成立，这正是鞅的定义。[@problem_id:2992602] [@problem_id:2992632]

#### [Doléans-Dade指数](@entry_id:272930)：密度过程的构建

一个核心问题是如何构建这样的密度鞅。答案由**[Doléans-Dade指数](@entry_id:272930)** (或[随机指数](@entry_id:197698)) 给出。对于任意一个 $\mathbb{P}$-[局部鞅](@entry_id:186755) $M$，其[Doléans-Dade指数](@entry_id:272930) $Z = \mathcal{E}(M)$ 是以下[随机微分方程](@entry_id:146618)的唯一解：
$$
dZ_t = Z_{t-} dM_t, \quad Z_0 = 1
$$
其中 $Z_{t-}$ 表示 $Z$ 在 $t$ 时刻的[左极限](@entry_id:139055)。这个过程 $Z_t$ 是一个[局部鞅](@entry_id:186755)。对于连续的[局部鞅](@entry_id:186755) $M_t$，解的形式特别简单：
$$
Z_t = \mathcal{E}(M)_t = \exp\left(M_t - \frac{1}{2}\langle M \rangle_t\right)
$$
其中 $\langle M \rangle_t$ 是 $M_t$ 的二次变差过程。只要 $M_t$ 的路径是连续的，$Z_t$ 作为一个实数的指数函数，必然是严格正的。[@problem_id:2992603]

对于可能存在跳跃的一般[半鞅](@entry_id:184490) $M_t$，要保证 $Z_t$ 严格为正，需要对 $M_t$ 的跳跃大小 $\Delta M_t := M_t - M_{t-}$ 施加一个条件：对于所有跳跃时刻 $t$，必须有 $1 + \Delta M_t > 0$，即 $\Delta M_t > -1$。如果某个跳跃使得 $\Delta M_t = -1$，那么 $Z_t$ 将会跳到0并永久保持为0。如果 $\Delta M_t  -1$，则 $Z_t$ 会变号，破坏其作为密度的非负性。[@problem_id:2992603]

#### 局部 vs. 全局[测度变换](@entry_id:157887)

一个微妙但至关重要的问题是：一个定义了局部[测度变换](@entry_id:157887)的密度过程 $(Z_t)$，是否能定义一个在无限时间域 $\mathcal{F}_\infty = \sigma(\cup_{t \ge 0} \mathcal{F}_t)$ 上的全局[概率测度](@entry_id:190821)？

一个非负的[局部鞅](@entry_id:186755) $(Z_t)$ 总是定义了一个在任何有界停时 $\tau$ 上的有效[概率测度](@entry_id:190821)变换，因为被停的[局部鞅](@entry_id:186755)是一个真鞅，满足 $\mathbb{E}_{\mathbb{P}}[Z_\tau] = Z_0 = 1$。这被称为**局部[绝对连续性](@entry_id:144513)**。

然而，要将这个一致的测度族 $(\mathbb{Q}|_{\mathcal{F}_t})$ 扩展为 $\mathcal{F}_\infty$ 上的一个单一[概率测度](@entry_id:190821) $\mathbb{Q}$，使得 $d\mathbb{Q}/d\mathbb{P} = Z_\infty := \lim_{t\to\infty} Z_t$，我们需要一个更强的条件：[鞅](@entry_id:267779) $(Z_t)_{t\ge 0}$ 必须是**[一致可积](@entry_id:202893)的** (uniformly integrable)。

[一致可积性](@entry_id:199715)是保证鞅在 $L^1$ 范数下收敛的充要条件，它确保了期望的收敛性：$\mathbb{E}_{\mathbb{P}}[Z_\infty] = \lim_{t\to\infty}\mathbb{E}_{\mathbb{P}}[Z_t]$。由于我们要求 $\mathbb{E}_{\mathbb{P}}[Z_\infty] = 1$ 从而使 $\mathbb{Q}$ 成为一个概率测度，而 $\mathbb{E}_{\mathbb{P}}[Z_t]=1$（假设 $Z_t$ 是真鞅），那么[一致可积性](@entry_id:199715)就成了关键。如果 $(Z_t)$ 不是[一致可积](@entry_id:202893)的，即使它是一个真鞅，其极限的期望也可能小于1，即 $\mathbb{E}_{\mathbb{P}}[Z_\infty]  1$。这被称为“质量泄露到无穷远”，此时通过 $Z_\infty$ 定义的测度 $\mathbb{Q}$ 是一个总质量小于1的次[概率测度](@entry_id:190821)。[@problem_id:2992609]

一个经典的例子是与三维[Bessel过程](@entry_id:200005) $(R_t)_{t\ge 0}$ 相关的密度过程。三维[Bessel过程](@entry_id:200005)是方程 $dR_t = dW_t + \frac{1}{R_t} dt$ 的解，它以概率1是瞬时的，即 $\lim_{t\to\infty} R_t = \infty$。考虑密度过程 $Z_t = 1/R_t$。可以证明 $(Z_t)$ 是一个严格正的[局部鞅](@entry_id:186755)。对于任何有界停时 $\tau$，$\mathbb{E}_{\mathbb{P}}[Z_\tau]=1$，定义了一个有效的局部[测度变换](@entry_id:157887)。然而，由于 $R_t \to \infty$，我们有 $Z_\infty = \lim_{t\to\infty} 1/R_t = 0$。因此，$\mathbb{E}_{\mathbb{P}}[Z_\infty] = 0$。在这种情况下，尽管局部[测度变换](@entry_id:157887)处处有效，但无法在 $\mathcal{F}_\infty$ 上定义一个等价的全局[概率测度](@entry_id:190821)。在极限情况下，两个测度变得相互奇异。[@problem_id:2992590]

### [Girsanov定理](@entry_id:147068)：变换的引擎

[Girsanov定理](@entry_id:147068)是[测度变换](@entry_id:157887)理论在[随机过程](@entry_id:159502)中的核心应用，它精确地描述了在[测度变换](@entry_id:157887)下，特定[随机过程](@entry_id:159502)（如布朗运动）的定律如何改变。

#### 典范情形：为布朗运动增加漂移

[Girsanov定理](@entry_id:147068)最广为人知的形式是关于布朗运动的。它指出，通过一个恰当的[测度变换](@entry_id:157887)，我们可以将一个[标准布朗运动](@entry_id:197332)转变为一个[带漂移的布朗运动](@entry_id:275071)。

**[Girsanov定理](@entry_id:147068) (布朗运动形式)**：令 $(W_t)_{t \in [0,T]}$ 为 $\mathbb{P}$ 测度下的一个 $d$-维标准布朗运动。设 $(\theta_t)_{t \in [0,T]}$ 是一个适应的 $\mathbb{R}^d$-值的过程，满足 $\int_0^T \|\theta_s\|^2 ds  \infty$ ($\mathbb{P}$-a.s.)。定义[局部鞅](@entry_id:186755) $M_t = \int_0^t \theta_s \cdot dW_s$ 及其[Doléans-Dade指数](@entry_id:272930) $Z_t = \mathcal{E}(M)_t$。
$$
Z_t = \exp\left(\int_0^t \theta_s \cdot dW_s - \frac{1}{2} \int_0^t \|\theta_s\|^2 ds\right)
$$
如果我们假设 $(Z_t)$ 是一个真[鞅](@entry_id:267779)（即 $\mathbb{E}_{\mathbb{P}}[Z_T]=1$），并定义新的概率测度 $\mathbb{Q}$ 为 $\frac{d\mathbb{Q}}{d\mathbb{P}} = Z_T$，那么过程
$$
W_t^{\mathbb{Q}} := W_t - \int_0^t \theta_s ds, \quad t \in [0, T]
$$
在测度 $\mathbb{Q}$ 下是一个 $d$-维标准布朗运动。[@problem_id:2992586]

这个定理的强大之处在于它建立了一个精确的对应关系：密度过程中的[随机积分](@entry_id:198356)项 $\int \theta_s \cdot dW_s$ 对应于新布朗运动所“消除”的漂移项 $\int \theta_s ds$。

#### [鞅](@entry_id:267779)条件：Novikov与Kazamaki

[Girsanov定理](@entry_id:147068)的一个关键假设是密度过程 $(Z_t)$ 是一个真鞅，以保证 $\mathbb{Q}$ 是一个总质量为1的[概率测度](@entry_id:190821)。由于 $Z_t$ 通常只是一个[局部鞅](@entry_id:186755)，我们需要额外的条件来确保它是一个（[一致可积](@entry_id:202893)的）真鞅。

一个著名且实用的充分条件是**[Novikov条件](@entry_id:634732)**：
$$
\mathbb{E}_{\mathbb{P}}\left[\exp\left(\frac{1}{2} \int_0^T \|\theta_s\|^2 ds\right)\right]  \infty
$$
如果[Novikov条件](@entry_id:634732)成立，则 $(Z_t)_{t \in [0,T]}$ 是一个[一致可积](@entry_id:202893)的鞅，[Girsanov定理](@entry_id:147068)的所有前提都得到满足。[@problem_id:2992586]

然而，[Novikov条件](@entry_id:634732)并非必要条件。存在一些情况，虽然[Novikov条件](@entry_id:634732)不满足，但 $(Z_t)$ 仍然是一个真鞅。一个更弱（因此更普适）的充分条件是**[Kazamaki条件](@entry_id:201768)**：
$$
\sup_{t \in [0,T]} \mathbb{E}_{\mathbb{P}}\left[\exp\left(\frac{1}{2} M_t\right)\right]  \infty
$$
其中 $M_t = \int_0^t \theta_s \cdot dW_s$。

考虑一个例子：设 $W_t$ 是一维布朗运动，$X \sim \mathcal{N}(0,1)$ 是一个独立于 $W_t$ 的[随机变量](@entry_id:195330)，并定义 $\theta_t = X$ 在时间区间 $[0,3]$ 上。此时 Novikov 条件要求 $\mathbb{E}[\exp(\frac{1}{2} \int_0^3 X^2 ds)] = \mathbb{E}[\exp(\frac{3}{2} X^2)]$ 有限，但这显然是发散的。然而，可以计算出 Kazamaki 条件中的[期望值](@entry_id:153208)为 $\mathbb{E}[\exp(\frac{1}{2} X W_t)] = \frac{2}{\sqrt{4-t}}$，在 $[0,3]$ 上的上确界为2，是有限的。因此，[Kazamaki条件](@entry_id:201768)成立，保证了[测度变换](@entry_id:157887)的有效性。这个例子清晰地表明，即使在[Novikov条件](@entry_id:634732)失效时，[测度变换](@entry_id:157887)仍可能是有效的。[@problem_id:2992627]

#### 对[半鞅](@entry_id:184490)的推广

[Girsanov定理](@entry_id:147068)的威力远不止于布朗运动。它可以被推广到一般的[半鞅](@entry_id:184490)，为处理带跳跃的[随机过程](@entry_id:159502)提供了强大的工具。

##### [跳跃过程](@entry_id:180953)

考虑一个强度为 $\lambda_t$ 的点过程 $(N_t)_{t \ge 0}$，其对应的 $\mathbb{P}$-鞅是 $N_t - \int_0^t \lambda_s ds$。我们可以通过一个密度过程来改变它的强度。如果密度过程 $Z_t$ 的形式为 $dZ_t = Z_{t-} (\theta_t - 1) (dN_t - \lambda_t dt)$，其中 $\theta_t$ 是一个严格正的[可预测过程](@entry_id:262945)，那么在新的测度 $\mathbb{Q}$下，点过程 $(N_t)$ 的强度将变为 $\tilde{\lambda}_t = \theta_t \lambda_t$。这意味着新的 $\mathbb{Q}$-鞅是 $N_t - \int_0^t \theta_s \lambda_s ds$。强度变换是[乘性](@entry_id:187940)的，这为金融和保险中的[信用风险](@entry_id:146012)和事件建模提供了基础。[@problem_id:2992587]

##### 一般定理与[特征三元组](@entry_id:635937)

对于一个一般的一维特殊[半鞅](@entry_id:184490) $S$，其在 $\mathbb{P}$ 测度下的行为可以由其**[特征三元组](@entry_id:635937)** $(B, C, \nu)$ 完全刻画。这里：
- $B$ 是一个可预测的[有限变差过程](@entry_id:635841)，代表了 $S$ 的可预测漂移。
- $C_t = \langle S^c \rangle_t$ 是 $S$ 的[连续局部鞅](@entry_id:204638)部分 $S^c$ 的二次变差。
- $\nu(dt, dx)$ 是 $S$ 的跳跃测度的可预测补偿测度，描述了跳跃的“强度”。

Girsanov的一般定理精确地描述了在由密度[鞅](@entry_id:267779) $Z = \mathcal{E}(M)$ 定义的[测度变换](@entry_id:157887)下，这个[特征三元组](@entry_id:635937)如何从 $(B, C, \nu)$ 变换为新的三元组 $(B^{\mathbb{Q}}, C^{\mathbb{Q}}, \nu^{\mathbb{Q}})$。
假设驱动密度过程的[鞅](@entry_id:267779) $M$ 可以表示为 $M_t = \int_0^t b_s dS_s^c + \int_0^t \int_{\mathbb{R}} (Y(s,x)-1) (\mu^S - \nu)(ds,dx)$，其中 $\mu^S$ 是 $S$ 的跳跃测度。那么变换规则如下：
1.  **连续二次变差**：$C^{\mathbb{Q}} = C$。二次变差是一个路径性质，在[等价测度](@entry_id:634447)变换下保持不变。
2.  **跳跃补偿测度**：$\nu^{\mathbb{Q}}(dt,dx) = Y(t,x) \nu(dt,dx)$。跳跃强度被乘性地调整。
3.  **漂移**：$dB^{\mathbb{Q}}_t = dB_t + b_t dC_t + \int_{\mathbb{R}} h(x) (Y(t,x)-1) \nu(dt,dx)$。新的漂移项由三部分组成：原始漂移、来自连续部分变换的额外漂移、以及来自跳跃部分变换的额外漂移（其中 $h(x)$ 是一个截断函数）。

这个一般形式统一了连续过程和[跳跃过程](@entry_id:180953)的[测度变换](@entry_id:157887)，展示了其深刻的数学结构。[@problem_id:2992592]