## 引言
[测度变换](@entry_id:157887)是[随机分析](@entry_id:188809)中一个极为强大且优雅的工具，尤其在处理由随机微分方程（SDE）描述的扩散过程时，其重要性不言而喻。它允许我们通过改变概率定律的“视角”来简化复杂[随机过程](@entry_id:159502)的分析，这在理论研究和实际应用中都具有深远影响。例如，在金融衍生品定价或[稀有事件模拟](@entry_id:754079)中，直接分析过程的动态可能异常棘手。[测度变换](@entry_id:157887)技术提供了一条捷径，通过系统地改变过程的漂移项，将原问题转化为一个在新的、更便利的概率世界中可解的问题。

本文将带领读者全面掌握扩散过程的[测度变换](@entry_id:157887)技术。我们将从其数学基础出发，逐步深入到其在多个领域的应用。文章分为三个核心部分：
*   **原理与机制**：我们将首先构建[测度变换](@entry_id:157887)的理论框架，深入探讨[Radon-Nikodym导数](@entry_id:158399)，并聚焦于该领域基石性的成果——[吉尔萨诺夫定理](@entry_id:147068)。
*   **应用与跨学科联系**：随后，我们将探索该技术在数学金融（[风险中性定价](@entry_id:144172)）、计算科学（[重要性采样](@entry_id:145704)）以及与[偏微分方程理论](@entry_id:189232)的深刻联系。
*   **动手实践**：最后，通过一系列精心设计的问题，您将有机会亲手应用所学知识，巩固理解。

现在，让我们从第一部分开始，深入探究[测度变换](@entry_id:157887)技术的核心原理与机制。

## 原理与机制

在本章中，我们将深入探讨[测度变换](@entry_id:157887)技术的核心原理与机制。我们现在将系统地构建这一强大工具的理论基础，该工具使我们能够在不改变样本空间本身的情况下，改变[随机过程](@entry_id:159502)的概率定律。我们将从[测度变换](@entry_id:157887)的抽象框架开始，然后详细阐述[吉尔萨诺夫定理](@entry_id:147068)（Girsanov's theorem），最后讨论其深刻的推论和应用。

### [测度变换](@entry_id:157887)与[Radon-Nikodym导数](@entry_id:158399)

[测度变换](@entry_id:157887)的核心思想是，在给定的[可测空间](@entry_id:189701) $(\Omega, \mathcal{F})$ 上，我们可以从一个初始[概率测度](@entry_id:190821) $\mathbb{P}$ 转换到一个新的[概率测度](@entry_id:190821) $\mathbb{Q}$。这种转换是通过一个称为 **[Radon-Nikodym导数](@entry_id:158399)**（或密度）的非负[随机变量](@entry_id:195330) $Z$ 来实现的，该变量定义在 $\mathcal{F}$ 上。

#### [绝对连续性](@entry_id:144513)与等价性

一个测度 $\mathbb{Q}$ 被称为关于 $\mathbb{P}$ **绝对连续**（记为 $\mathbb{Q} \ll \mathbb{P}$），如果任何在 $\mathbb{P}$ 测度下的[零测集](@entry_id:157694)在 $\mathbb{Q}$ 测度下也为[零测集](@entry_id:157694)。也就是说，对于任意事件 $A \in \mathcal{F}$，若 $\mathbb{P}(A) = 0$，则必有 $\mathbb{Q}(A) = 0$。根据 **[Radon-Nikodym定理](@entry_id:161238)**，$\mathbb{Q} \ll \mathbb{P}$ 的充分必要条件是存在一个非负的、$\mathcal{F}$-可测的[随机变量](@entry_id:195330) $Z_T$，使得对于任意 $A \in \mathcal{F}_T$，
$$
\mathbb{Q}(A) = \int_A Z_T d\mathbb{P} = \mathbb{E}_{\mathbb{P}}[Z_T \mathbf{1}_A]
$$
其中 $\mathbb{E}_{\mathbb{P}}[\cdot]$ 表示在 $\mathbb{P}$ 测度下的期望。这个[随机变量](@entry_id:195330) $Z_T$ 被记为 $Z_T = \frac{d\mathbb{Q}}{d\mathbb{P}}\big|_{\mathcal{F}_T}$。

在许多应用中，我们需要一个更强的关系：**测度等价**（记为 $\mathbb{Q} \sim \mathbb{P}$）。这意味着 $\mathbb{Q} \ll \mathbb{P}$ 和 $\mathbb{P} \ll \mathbb{Q}$ 同时成立。测度等价的直观含义是两个测度拥有完全相同的[零测集](@entry_id:157694)。这当且仅当[Radon-Nikodym导数](@entry_id:158399) $Z_T$ 在 $\mathbb{P}$ 测度下几乎必然严格为正（即 $\mathbb{P}(Z_T > 0) = 1$）时成立 [@problem_id:3043699] [@problem_id:3043723]。

这种零测集的保持是一个至关重要的性质。许多[随机过程](@entry_id:159502)的性质，例如路径连续性，都是以“几乎必然”（almost surely, a.s.）的方式定义的，即该性质在某个测度为1的事件集上成立。如果两个测度是等价的，那么任何在 $\mathbb{P}$ 测度下[几乎必然](@entry_id:262518)成立的路径性质，在 $\mathbb{Q}$ 测度下也几乎必然成立。例如，我们知道布朗运动的样本路径在 $\mathbb{P}$ 测度下是几乎必然连续的。这意味着不连续路径的集合是一个 $\mathbb{P}$-[零测集](@entry_id:157694)。由于[等价测度](@entry_id:634447)共享[零测集](@entry_id:157694)，该集合在 $\mathbb{Q}$ 测度下也为[零测集](@entry_id:157694)，因此，过程的路径在 $\mathbb{Q}$ 测度下也几乎必然是连续的 [@problem_id:3043734]。

#### 期望的变换

[Radon-Nikodym导数](@entry_id:158399)最基本的功能是作为在两个测度下计算期望的桥梁。对于任何有界的 $\mathcal{F}_T$-可测[随机变量](@entry_id:195330) $X$，其在 $\mathbb{Q}$ 测度下的期望可以通过在 $\mathbb{P}$ 测度下对 $X$ 与密度 $Z_T$ 的乘积求期望来得到 [@problem_id:3043723]：
$$
\mathbb{E}_{\mathbb{Q}}[X] = \mathbb{E}_{\mathbb{P}}[Z_T X]
$$
由于 $\mathbb{Q}$ 是一个概率测度，总概率 $\mathbb{Q}(\Omega)$ 必须为1。将上式应用于 $X=1$ 可得一个必要条件：
$$
\mathbb{E}_{\mathbb{P}}[Z_T] = \mathbb{E}_{\mathbb{Q}}[1] = 1
$$
因此，任何有效的[概率密度](@entry_id:175496)过程的终端值 $Z_T$ 必须在原测度 $\mathbb{P}$ 下期望为1，并且必须非负 [@problem_id:3043723]。

对于条件期望，存在一个类似的变换法则，通常称为“抽象贝叶斯公式”。对于任何时刻 $t \in [0,T]$ 和有界 $\mathcal{F}_T$-可测[随机变量](@entry_id:195330) $X$，我们有：
$$
\mathbb{E}_{\mathbb{Q}}[X \mid \mathcal{F}_t] = \frac{\mathbb{E}_{\mathbb{P}}[Z_T X \mid \mathcal{F}_t]}{\mathbb{E}_{\mathbb{P}}[Z_T \mid \mathcal{F}_t]}
$$
定义**密度过程** $Z_t := \mathbb{E}_{\mathbb{P}}[Z_T \mid \mathcal{F}_t]$，上式可以更简洁地写为：
$$
Z_t \mathbb{E}_{\mathbb{Q}}[X \mid \mathcal{F}_t] = \mathbb{E}_{\mathbb{P}}[Z_T X \mid \mathcal{F}_t]
$$
这个关系式是在[测度变换](@entry_id:157887)下推导[鞅性质](@entry_id:261270)的核心工具 [@problem_id:3043723]。

### [吉尔萨诺夫定理](@entry_id:147068)（Girsanov's Theorem）

在[扩散过程](@entry_id:170696)的背景下，我们关心的是如何具体构建一个密度过程 $Z_t$，以实现对随机微分方程（SDE）解的定律的特定变换。[吉尔萨诺夫定理](@entry_id:147068)提供了一个精确的方法来改变一个过程的漂移项，而不改变其[扩散](@entry_id:141445)项。

#### [Doléans-Dade指数](@entry_id:272930)与密度过程

假设 $(\Omega, \mathcal{F}, (\mathcal{F}_t)_{t \ge 0}, \mathbb{P})$ 是一个满足“通常条件”的带滤概率空间，其上支撑一个标准 $\mathbb{P}$-布朗运动 $W = (W_t)_{t \ge 0}$。令 $\theta = (\theta_t)_{t \ge 0}$ 是一个逐点可测的[适应过程](@entry_id:187710)，满足一定的[可积性](@entry_id:142415)条件（例如 $\int_0^T \theta_s^2 ds < \infty$ a.s.）。我们定义一个称为 **[Doléans-Dade指数](@entry_id:272930)**或**[随机指数](@entry_id:197698)**的过程 $Z_t$：
$$
Z_t = \exp\left(\int_0^t \theta_s dW_s - \frac{1}{2}\int_0^t \theta_s^2 ds\right)
$$
这个特殊形式的选择并非偶然。首先，由于指数函数的参数是实数值的连续过程，所以 $Z_t$ [几乎必然](@entry_id:262518)是严格为正的。其次，通过应用[伊藤公式](@entry_id:159684)（Itô's formula），可以证明 $Z_t$ 满足随机微分方程 $dZ_t = Z_t \theta_t dW_t$。这个SDE的解没有漂移项，这意味着 $Z_t$ 是一个 **$\mathbb{P}$-[局部鞅](@entry_id:186755)** [@problem_id:3043739]。

为了使 $Z_T$ 能够定义一个合法的[概率测度](@entry_id:190821) $\mathbb{Q}$，我们需要 $\mathbb{E}_{\mathbb{P}}[Z_T]=1$。一个[局部鞅](@entry_id:186755)要成为一个真正的[鞅](@entry_id:267779)（即其期望恒为初始值），需要满足一个称为**[一致可积性](@entry_id:199715)** (uniform integrability) 的技术条件。如果 $(Z_t)_{t \in [0,T]}$ 是[一致可积](@entry_id:202893)的，那么它就是一个真鞅，从而 $\mathbb{E}_{\mathbb{P}}[Z_T] = Z_0 = 1$，并且 $Z_t = \mathbb{E}_{\mathbb{P}}[Z_T \mid \mathcal{F}_t]$ 成立。这个性质保证了测度定义的时间一致性 [@problem_id:3043735]。一个确保[一致可积性](@entry_id:199715)的著名充分条件是**[诺维科夫条件](@entry_id:634732)**（Novikov's condition）：
$$
\mathbb{E}_{\mathbb{P}}\left[\exp\left(\frac{1}{2}\int_0^T \theta_s^2 ds\right)\right] < \infty
$$
另一个更强的充分条件是 $\theta$ 过程是有界的 [@problem_id:3043735]。

#### 定理的陈述

**[吉尔萨诺夫定理](@entry_id:147068)**断言：假设[诺维科夫条件](@entry_id:634732)成立，我们通过 $d\mathbb{Q} = Z_T d\mathbb{P}$ 定义了一个与 $\mathbb{P}$ 等价的新概率测度 $\mathbb{Q}$。在此新测度 $\mathbb{Q}$ 下，过程
$$
W^{\mathbb{Q}}_t := W_t - \int_0^t \theta_s ds
$$
是一个关于原 filtration $(\mathcal{F}_t)$ 的标准布朗运动 [@problem_id:3043737]。

这个定理的威力在于它对一般SDE的影响。考虑一个在 $\mathbb{P}$ 测度下由下式驱动的过程 $X_t$：
$$
dX_t = b_t dt + \sigma_t dW_t
$$
我们可以将 $dW_t$ 替换为 $dW^{\mathbb{Q}}_t + \theta_t dt$。代入SDE后，我们得到 $X_t$ 在 $\mathbb{Q}$ 测度下的动态：
$$
dX_t = b_t dt + \sigma_t (dW^{\mathbb{Q}}_t + \theta_t dt) = (b_t + \sigma_t \theta_t) dt + \sigma_t dW^{\mathbb{Q}}_t
$$
在新的测度下，[扩散](@entry_id:141445)系数 $\sigma_t$ 保持不变，而漂移项从 $b_t$ 变为 $b_t + \sigma_t \theta_t$ [@problem_id:3043737]。

### 核心机制与重要推论

#### Lévy[特征化](@entry_id:161672)定理的角色

[吉尔萨诺夫定理](@entry_id:147068)的证明优雅地展示了现代[随机分析](@entry_id:188809)工具的威力，其核心是 **Lévy对布朗运动的[特征化](@entry_id:161672)定理**。该定理的一个强形式是：任何一个初始值为零的[连续局部鞅](@entry_id:204638) $M_t$，如果其二次变差为 $[M]_t = t$，那么 $M_t$ 必定是一个标准布朗运动 [@problem_id:3043747]。

为了证明 $W^{\mathbb{Q}}_t = W_t - \int_0^t \theta_s ds$ 是一个 $\mathbb{Q}$-布朗运动，我们需要验证它满足Lévy[特征化](@entry_id:161672)定理的条件：
1.  **连续性与初始值**：$W_t$ 是连续的，并且 $\int_0^t \theta_s ds$ 也是一个连续的[有界变差](@entry_id:139291)过程。因此，$W^{\mathbb{Q}}_t$ 是连续的，且 $W^{\mathbb{Q}}_0 = 0$。
2.  **二次变差**：二次变差对于加上一个[有界变差](@entry_id:139291)过程是不变的。因此，$[W^{\mathbb{Q}}]_t = [W]_t = t$。这个性质在[等价测度](@entry_id:634447)变换下也保持不变，我们稍后会详细讨论。
3.  **$\mathbb{Q}$-[局部鞅](@entry_id:186755)性质**：这是证明中最关键的部分。通过使用前述的抽象贝叶斯公式，可以证明 $W^{\mathbb{Q}}_t$ 在 $\mathbb{Q}$ 测度下确实是一个[局部鞅](@entry_id:186755)。

由于 $W^{\mathbb{Q}}_t$ 满足Lévy[特征化](@entry_id:161672)定理的所有条件，我们得出结论：它在 $\mathbb{Q}$ 测度下是一个[标准布朗运动](@entry_id:197332) [@problem_id:3043747]。

#### [扩散](@entry_id:141445)系数的不变性

[吉尔萨诺夫定理](@entry_id:147068)一个深刻的推论是，[等价测度](@entry_id:634447)变换只能改变SDE的漂移项，而不能改变其[扩散](@entry_id:141445)系数。其根本原因在于**二次变差**的性质。对于一个[伊藤过程](@entry_id:635897) $dX_t = b_t dt + \sigma_t dW_t$，其二次变差由下式路径化地给出：
$$
[X]_t = \int_0^t \sigma_s^2 ds
$$
这意味着对于几乎每一条样本路径 $\omega$，这个等式都成立。它是一个**路径性质**，衡量的是路径的“粗糙度”，而不是这条路径发生的概率。

由于[等价测度](@entry_id:634447) $\mathbb{P}$ 和 $\mathbb{Q}$ 共享相同的[零测集](@entry_id:157694)，一个在 $\mathbb{P}$ 测度下[几乎必然](@entry_id:262518)成立的路径等式，在 $\mathbb{Q}$ 测度下也必然几乎成立。因此，无论我们使用哪个测度，二次变差过程 $[X]_t$ 对于每个样本路径都是相同的。由于[扩散](@entry_id:141445)系数 $\sigma_t$ 本质上是由二次变差的时间导数（即 $\sigma_t^2 = d[X]_t/dt$）所决定的，所以它在[等价测度](@entry_id:634447)变换下必须保持不变 [@problem_id:3043700]。

这也解释了为什么由具有不同[扩散](@entry_id:141445)系数的SDE所生成的测度是**相互奇异**（mutually singular）的，而非等价的。如果两个SDE的[扩散](@entry_id:141445)系数不同（例如 $\sigma$ 和 $\tilde{\sigma}$），那么在第一个测度下，二次变差几乎必然是 $\int_0^t \sigma_s^2 ds$，而在第二个测度下几乎必然是 $\int_0^t \tilde{\sigma}_s^2 ds$。这意味着第一个测度将概率1赋予了第二个测度看来概率为0的路径集合，反之亦然。因此，它们不可能是等价的 [@problem_id:3043699]。

#### 过滤的“通常条件”

在整个理论框架中，我们假设 filtration $(\mathcal{F}_t)$ 满足“通常条件”，即它是完备的且右连续的。这些技术条件在[测度变换](@entry_id:157887)中扮演着微妙但重要的角色。为了应用Lévy[特征化](@entry_id:161672)定理并确保新过程 $W^{\mathbb{Q}}$ 具有标准布朗运动的所有良好性质（如强马尔可夫性），filtration $(\mathcal{F}_t)$ 必须在**新测度 $\mathbb{Q}$**下也满足通常条件。
- **[右连续性](@entry_id:170543)** ($\mathcal{F}_t = \cap_{s>t} \mathcal{F}_s$) 是 filtration 本身的拓扑性质，与测度无关。
- **完备性**（即所有零测[子集](@entry_id:261956)都包含在 filtration 中）是依赖于测度的。然而，由于 $\mathbb{P}$ 和 $\mathbb{Q}$ 是等价的，它们有相同的零测集。因此，如果 filtration 相对于 $\mathbb{P}$ 是完备的，它也自动相对于 $\mathbb{Q}$ 是完备的。

因此，“通常条件”的初始假设确保了在[测度变换](@entry_id:157887)后，我们仍然拥有一个行为良好的概率空间，使得所有理论工具都能继续适用 [@problem_id:3043719]。

### [卡梅伦-马丁定理](@entry_id:635399)（Cameron-Martin Theorem）

[卡梅伦-马丁定理](@entry_id:635399)是[吉尔萨诺夫定理](@entry_id:147068)一个优美且重要的特例，它处理的是一个确定性函数的平移。考虑[维纳测度](@entry_id:189476) $\mu$（即[标准布朗运动](@entry_id:197332) $W$ 的定律），并考虑一个平移后的过程 $W+h$，其中 $h$ 是一个确定的函数。[卡梅伦-马丁定理](@entry_id:635399)回答了这样一个问题：对于什么样的函数 $h$，平移后过程的定律 $\mu_h$ 与原始[维纳测度](@entry_id:189476) $\mu$ 是等价的？

答案是，这种等价性成立当且仅当 $h$ 属于一个特定的[函数空间](@entry_id:143478)，即**[卡梅伦-马丁空间](@entry_id:203032)** $H$。这个空间由所有满足 $h(0)=0$ 的[绝对连续函数](@entry_id:158609)组成，其导数（在勒贝格意义下）是平方可积的，即 $\dot{h} \in L^2([0,T])$。

当 $h \in H$ 时，[卡梅伦-马丁定理](@entry_id:635399)给出了[Radon-Nikodym导数](@entry_id:158399)的显式表达式。这实际上是吉尔萨诺夫公式在 $\theta_t = \dot{h}(t)$（一个确定性过程）下的直接应用 [@problem_id:3043698]：
$$
\frac{d\mu_h}{d\mu}(W) = \exp\left(\int_0^T \dot{h}(t) dW_t - \frac{1}{2}\int_0^T \dot{h}(t)^2 dt\right)
$$
这个结果在[随机分析](@entry_id:188809)和无穷维分析中具有基础性的重要地位，它精确地刻画了[维纳测度](@entry_id:189476)在何种“方向”上可以平移而不破坏其[绝对连续性](@entry_id:144513)。