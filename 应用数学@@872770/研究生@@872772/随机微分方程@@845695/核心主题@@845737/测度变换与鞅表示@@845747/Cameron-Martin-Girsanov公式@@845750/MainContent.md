## 引言
卡梅伦-马丁-吉尔萨诺夫（Cameron-Martin-Girsanov, CMG）公式是[随机分析](@entry_id:188809)领域的一项基石性定理，它为在不同[概率测度](@entry_id:190821)视角下研究[随机过程](@entry_id:159502)提供了严谨的数学框架。其核心贡献在于精确描述了如何通过改变一个[随机过程](@entry_id:159502)的漂移项来相应地变换其底层的[概率测度](@entry_id:190821)，反之亦然。这一能力解决了[随机建模](@entry_id:261612)中的一个根本问题：我们如何系统地将一个具有特定动态行为的过程（例如，带有预期回报的资产价格）转化为一个更易于分析的形式（例如，一个鞅），同时保持其内在的随机波动结构？CMG公式正是回答这一问题的关键。

本文将带领读者全面探索CMG公式。在“原理与机制”一章中，我们将深入其理论核心，从[测度变换](@entry_id:157887)和[Radon-Nikodym导数](@entry_id:158399)的基本概念出发，构建[Girsanov定理](@entry_id:147068)，并探讨其成立的条件与深刻内涵。随后，在“应用与[交叉](@entry_id:147634)学科联系”一章中，我们将展示该公式如何在[金融数学](@entry_id:143286)、统计推断和[滤波理论](@entry_id:186966)等领域发挥关键作用，将其从一个抽象的数学工具转化为解决实际问题的强大引擎。最后，“实践练习”部分将通过具体问题，帮助读者巩固理论知识并将其付诸实践。通过这一结构化的学习路径，读者将对CMG公式的理论深度和应用广度建立起一个完整而深刻的理解。

## 原理与机制

本章旨在深入探讨Cameron-Martin-Girsanov公式的核心原理与机制。我们将从[测度变换](@entry_id:157887)的基本框架出发，逐步构建[Girsanov定理](@entry_id:147068)在不同情境下的形式，阐明其成立的条件、关键推论及其在理论与应用中的深刻内涵与局限性。

### [测度变换](@entry_id:157887)的基本框架

在[随机过程](@entry_id:159502)理论中，我们常常需要从一个概率测度 $\mathbb{P}$ 的视角转换到另一个等价的[概率测度](@entry_id:190821) $\mathbb{Q}$ 的视角来分析问题。这种转换的核心工具是 **[Radon-Nikodym导数](@entry_id:158399)**。如果测度 $\mathbb{Q}$ 关于测度 $\mathbb{P}$ 是绝对连续的（记作 $\mathbb{Q} \ll \mathbb{P}$），那么存在一个非负的[随机变量](@entry_id:195330) $Z$，使得对于任何事件 $A$，都有 $\mathbb{Q}(A) = \mathbb{E}_{\mathbb{P}}[Z \cdot \mathbf{1}_A]$。这个 $Z$ 就是[Radon-Nikodym导数](@entry_id:158399)，记作 $Z = \frac{d\mathbb{Q}}{d\mathbb{P}}$。为了使 $\mathbb{Q}$ 成为一个[概率测度](@entry_id:190821)，即 $\mathbb{Q}(\Omega)=1$，我们必须有 $\mathbb{E}_{\mathbb{P}}[Z] = 1$。

在处理[连续时间过程](@entry_id:274437)时，我们通常将这一概念动态化。我们寻找一个[随机过程](@entry_id:159502) $(Z_t)_{t \in [0,T]}$，它本身是一个在测度 $\mathbb{P}$ 下的 **鞅**，并且满足 $Z_0=1$ 且 $Z_t \ge 0$。这样的过程被称为 **密度过程**。给定这样一个过程，我们可以在任意时刻 $t$ 的 $\sigma$-代数 $\mathcal{F}_t$ 上定义一个新的[概率测度](@entry_id:190821) $\mathbb{Q}$，其[Radon-Nikodym导数](@entry_id:158399)为 $Z_t$。

构造这样一个正[鞅](@entry_id:267779)的关键工具是 **[Doléans-Dade指数](@entry_id:272930)**（或称[随机指数](@entry_id:197698)）。对于一个[连续局部鞅](@entry_id:204638) $M$，其[Doléans-Dade指数](@entry_id:272930)定义为：
$$
\mathcal{E}(M)_t := \exp\left(M_t - \frac{1}{2}\langle M \rangle_t\right)
$$
其中 $\langle M \rangle_t$ 是 $M$ 的二次变差过程。可以证明，$\mathcal{E}(M)_t$ 本身是一个[局部鞅](@entry_id:186755)，其初值为 $\mathcal{E}(M)_0=1$。它满足[随机微分方程](@entry_id:146618)（SDE）：
$$
d\mathcal{E}(M)_t = \mathcal{E}(M)_t dM_t
$$
这个过程构成了[Girsanov定理](@entry_id:147068)的基石。

### [Girsanov定理](@entry_id:147068)：布朗运动下的漂移变换

为了精确地陈述[Girsanov定理](@entry_id:147068)，我们必须首先建立一个严谨的数学环境。这个环境通常是 **[维纳空间](@entry_id:184612) (Wiener Space)** [@problem_id:3000282]。它由以下三部分构成：
1.  [样本空间](@entry_id:275301) $C_0([0,T])$：所有从0出发的 $[0,T]$ 上的[连续函数](@entry_id:137361)构成的空间。
2.  $\sigma$-代数 $\mathcal{B}(C_0([0,T]))$：由一致范数拓扑生成的Borel $\sigma$-代数。
3.  概率测度 $\mathbb{P}$：即[维纳测度](@entry_id:189476)，在该测度下，典范过程 $W_t(\omega) = \omega(t)$ 是一个[标准布朗运动](@entry_id:197332)。

此外，[随机分析](@entry_id:188809)中的强大定理通常要求其所依赖的 **信息流**（即**滤子 (filtration)** $(\mathcal{F}_t)_{t \in [0,T]}$）满足所谓的 **通常条件 (usual conditions)**。这意味着滤子不仅要包含过程的历史信息（即自然滤子 $\mathcal{F}_t^W = \sigma(W_s: 0 \le s \le t)$），还必须经过 **增广**，使其包含所有 $\mathbb{P}$-[零测集](@entry_id:157694)（**完备性**）并且是 **右连续的**（即 $\mathcal{F}_t = \bigcap_{u>t} \mathcal{F}_u$）。这些技术条件确保了理论的健壮性。

在这样的设定下，[Girsanov定理](@entry_id:147068)的核心内容可以被表述如下 [@problem_id:3000333] [@problem_id:3000265]：

设 $W_t$ 是一个在满足通常条件的滤子[概率空间](@entry_id:201477) $(\Omega, \mathcal{F}, (\mathcal{F}_t), \mathbb{P})$ 上的 $d$-维标准布朗运动。令 $\theta = (\theta_t)_{t \in [0,T]}$ 是一个 $\mathbb{R}^d$-值的 **[可预测过程](@entry_id:262945)**，满足 $\int_0^T \|\theta_s\|^2 ds  \infty$（[几乎必然](@entry_id:262518)）。定义密度过程 $Z_t$ 为：
$$
Z_t = \mathcal{E}\left(\int_0^\cdot \theta_s^\top dW_s\right)_t = \exp\left(\int_0^t \theta_s^\top dW_s - \frac{1}{2}\int_0^t \|\theta_s\|^2 ds\right)
$$
假设 $Z_t$ 是一个真鞅（我们将在下一节讨论其条件），我们可以定义一个新的概率测度 $\mathbb{Q}$，使得 $\frac{d\mathbb{Q}}{d\mathbb{P}} \Big|_{\mathcal{F}_T} = Z_T$。[Girsanov定理](@entry_id:147068)断言，在新测度 $\mathbb{Q}$ 下，过程
$$
\widetilde{W}_t := W_t - \int_0^t \theta_s ds
$$
是一个 $d$-维标准布朗运动。

这个定理的本质是，通过一个精心构造的[测度变换](@entry_id:157887)，我们可以将一个布朗运动转变为一个[带漂移的布朗运动](@entry_id:275071)，反之亦然。原测度下的布朗运动 $W_t$ 在新测度下表现为一个带有漂移项 $\int_0^t \theta_s ds$ 的过程，其鞅部分则由新的 $\mathbb{Q}$-布朗运动 $\widetilde{W}_t$ 驱动。

值得强调的是，被积过程 $\theta$ 的 **可预测性 (predictability)** 是整个理论的基石 [@problem_id:2978186]。[可预测过程](@entry_id:262945)粗略地讲是在时刻 $t$ 的值可以由 $t$ 之前的历史信息所确定。[Itô积分](@entry_id:272774) $\int_0^t \theta_s dW_s$ 的构造依赖于用简单过程（在时间区间上取值为区间左端点信息可测的[随机变量](@entry_id:195330)）去逼近 $\theta$。正是这种“非预知性”(non-anticipating)的构造保证了Itô积分是一个（局部）[鞅](@entry_id:267779)。如果允许 $\theta_s$ 依赖于 $W_s$ 的瞬时信息，鞅的性质就会被破坏，[Girsanov定理](@entry_id:147068)的整个框架便无从谈起。

### 定理的有效性：何时密度过程是真[鞅](@entry_id:267779)？

[Girsanov定理](@entry_id:147068)的实际应用依赖于一个关键前提：由[Doléans-Dade指数](@entry_id:272930)定义的[局部鞅](@entry_id:186755) $Z_t$ 必须是一个 **真鞅**（并且通常要求是可积[鞅](@entry_id:267779)），这样才能保证 $\mathbb{E}_{\mathbb{P}}[Z_T]=1$，从而使 $\mathbb{Q}$ 成为一个合法的概率测度。

一个广泛使用的充分条件是 **[Novikov条件](@entry_id:634732)** [@problem_id:3000333] [@problem_id:3000265]：
$$
\mathbb{E}_{\mathbb{P}}\left[\exp\left(\frac{1}{2}\int_0^T \|\theta_s\|^2 ds\right)\right]  \infty
$$
如果[Novikov条件](@entry_id:634732)成立，那么 $Z_t$ 就是一个在 $[0,T]$ 上的可积鞅，Girsanov[测度变换](@entry_id:157887)是有效的。

[Novikov条件](@entry_id:634732)并非必要条件，存在更弱的条件。其中一个著名的是 **[Kazamaki条件](@entry_id:201768)**，它要求过程 $\exp(\frac{1}{2} \int \theta_s dW_s)$ 是一个[下鞅](@entry_id:263978)。可以证明，[Novikov条件](@entry_id:634732)蕴含了[Kazamaki条件](@entry_id:201768)，但反之不成立，因此[Kazamaki条件](@entry_id:201768)是更弱（即更一般）的准则 [@problem_id:3000256]。

如果这些条件不满足，密度过程 $Z_t$ 可能是一个 **[严格局部鞅](@entry_id:636161)**，这意味着它是一个非负的父[鞅](@entry_id:267779)但不是真[鞅](@entry_id:267779)，此时 $\mathbb{E}_{\mathbb{P}}[Z_T]  1$。在这种情况下，由 $d\mathbb{Q} = Z_T d\mathbb{P}$ 定义的“测度”的总质量将小于1，因此它不是一个[概率测度](@entry_id:190821)。

一个经典的例子可以清晰地揭示这一点 [@problem_id:3000325]。考虑一个从 $W_0=1$ 出发的布朗运动，并让它在首次到达0时停止。定义 Girsanov 核为 $\theta_t = - \mathbf{1}_{\{t  \tau_0\}}/W_t$，其中 $\tau_0$ 是首次击中0的时刻。可以计算出，在 $T=1$ 时对应的密度期望为 $\mathbb{E}[Z_1] = 2\Phi(1) - 1 \approx 0.6827$，其中 $\Phi$ 是[标准正态分布](@entry_id:184509)的累积分布函数。由于 $\mathbb{E}[Z_1]  1$，由此定义的 $\mathbb{Q}$ 不是一个概率测度。这个例子生动地说明了为何需要Novikov或类似的条件来确保[测度变换](@entry_id:157887)的有效性。

### [Girsanov定理](@entry_id:147068)的应用与推论

#### Cameron-Martin公式：确定性漂移

[Girsanov定理](@entry_id:147068)最简单也最直观的应用是处理确定性漂移，这通常被称为 **Cameron-Martin公式** [@problem_id:3000327]。假设我们想引入一个确定性的漂移 $h(t)$，其中 $h(t)$ 属于所谓的[Cameron-Martin空间](@entry_id:203032)，即 $h(t) = \int_0^t \dot{h}(s) ds$ 且 $\int_0^T \dot{h}(s)^2 ds  \infty$。

我们取Girsanov核为 $\theta_t = \dot{h}(t)$。由于 $\theta_t$ 是确定性的，[Novikov条件](@entry_id:634732) $\mathbb{E}_{\mathbb{P}}[\exp(\frac{1}{2} \int_0^T \dot{h}(s)^2 ds)] = \exp(\frac{1}{2} \int_0^T \dot{h}(s)^2 ds)  \infty$ 总是成立。因此，密度过程 $Z_t = \exp(\int_0^t \dot{h}(s) dW_s - \frac{1}{2} \int_0^t \dot{h}(s)^2 ds)$ 是一个真[鞅](@entry_id:267779)。根据[Girsanov定理](@entry_id:147068)，在由 $Z_T$ 定义的新测度 $\mathbb{Q}$ 下，过程 $\widetilde{W}_t = W_t - \int_0^t \dot{h}(s) ds = W_t - h(t)$ 是一个标准布朗运动。这表明，给布朗运动增加一个确定性漂移等价于进行一次Radon-Nikodym[测度变换](@entry_id:157887)。

#### SDE漂移项的变换

[Girsanov定理](@entry_id:147068)最强大的应用之一是改变一个一般[Itô过程](@entry_id:635897)的漂移项。假设一个过程 $X_t$ 在测度 $\mathbb{P}$ 下满足SDE：
$$
dX_t = b_t dt + \sigma_t dW_t
$$
我们使用与之前相同的Girsanov变换，从 $\mathbb{P}$ 转换到 $\mathbb{Q}$，使得 $\widetilde{W}_t = W_t - \int_0^t \theta_s ds$ 是 $\mathbb{Q}$-布朗运动。我们可以重写原SDE中的 $dW_t$ 项：$dW_t = d\widetilde{W}_t + \theta_t dt$。将其代入 $X_t$ 的方程中 [@problem_id:3000294] [@problem_id:3000333]：
$$
dX_t = b_t dt + \sigma_t (d\widetilde{W}_t + \theta_t dt) = (b_t + \sigma_t \theta_t) dt + \sigma_t d\widetilde{W}_t
$$
这个结果揭示了Girsanov[变换的核](@entry_id:149509)心机制：在从 $\mathbb{P}$ 到 $\mathbb{Q}$ 的[测度变换](@entry_id:157887)下，[Itô过程](@entry_id:635897) $X_t$ 的 **漂移项** 从 $b_t$ 变成了 $b_t + \sigma_t \theta_t$，而其 **[扩散](@entry_id:141445)项** $\sigma_t$ 保持不变，只是驱动它的布朗运动从 $W_t$ 变成了 $\widetilde{W}_t$。

#### 二次变差的[不变性](@entry_id:140168)

一个至关重要的推论是，[连续半鞅](@entry_id:636909)的 **二次变差 (quadratic variation)** 在[等价测度](@entry_id:634447)变换下是 **不变的**。二次变差是一个依赖于过程路径固有“粗糙度”的量，而不是依赖于衡量这些路径概率的测度。

例如，在上述SDE变换中，$X_t$ 在 $\mathbb{P}$ 下的二次变差是 $\langle X \rangle_t = \int_0^t \sigma_s^2 ds$。在 $\mathbb{Q}$ 下，其分解为漂移部分 $\int (b_s + \sigma_s \theta_s)ds$ 和[局部鞅](@entry_id:186755)部分 $\int \sigma_s d\widetilde{W}_s$。其二次变差由[局部鞅](@entry_id:186755)部分决定，仍然是 $\langle X \rangle_t = \int_0^t \sigma_s^2 ds$。这个原理对于任何[连续半鞅](@entry_id:636909)都成立，是一个深刻且普适的结论 [@problem_id:3000339]。

### 推广与深层联系

#### 面向一般[连续局部鞅](@entry_id:204638)的[Girsanov定理](@entry_id:147068)

[Girsanov定理](@entry_id:147068)可以被推广到由任意[连续局部鞅](@entry_id:204638) $M$ 驱动的情形，而不仅仅是布朗运动 [@problem_id:3000293]。

设 $M$ 是一个在 $\mathbb{P}$ 下的[连续局部鞅](@entry_id:204638)。我们使用由另一个[可预测过程](@entry_id:262945) $\theta$ 和 $M$ 本身构造的密度过程来进行[测度变换](@entry_id:157887)：
$$
Z_t = \mathcal{E}\left(\int_0^\cdot \theta_s dM_s\right)_t = \exp\left(\int_0^t \theta_s dM_s - \frac{1}{2}\int_0^t \theta_s^2 d\langle M \rangle_s\right)
$$
在由 $Z_T$ 定义的新测度 $\mathbb{Q}$ 下，原过程 $M$ 不再是[局部鞅](@entry_id:186755)。取而代之的是一个新的过程 $N_t$：
$$
N_t := M_t - \int_0^t \theta_s d\langle M \rangle_s
$$
它成为一个在 $\mathbb{Q}$ 下的[连续局部鞅](@entry_id:204638)。这个普适形式清楚地表明，漂移补偿项 $d\langle M \rangle_s$ 直接与原[鞅](@entry_id:267779)的二次变差（时间时钟）相关。当 $M$ 是标准布朗运动时，$\langle M \rangle_t = t$，我们就恢复了之前的形式。

#### 逆问题：[鞅表示定理](@entry_id:180851)的联系

[Girsanov定理](@entry_id:147068)通常用于从给定的核 $\theta$ 构建新测度。但反过来，如果我们给定了一个目标[概率测度](@entry_id:190821) $\mathbb{Q}$（或其密度 $Z_T$），我们能否找到对应的Girsanov核 $\theta$？答案是肯定的，而这恰恰揭示了[Girsanov定理](@entry_id:147068)与另一个深刻结果——**[鞅表示定理](@entry_id:180851) (Martingale Representation Theorem, MRT)** 之间的密切联系 [@problem_id:3000272]。

在布朗运动滤子下，MRT表明，任何（平方可积的）[鞅](@entry_id:267779) $M_t$ 都可以被表示为一个关于该布朗运动的[Itô积分](@entry_id:272774)。具体来说，如果我们定义密度[鞅](@entry_id:267779) $M_t = \mathbb{E}_{\mathbb{P}}[Z_T | \mathcal{F}_t]$，那么MRT保证存在一个唯一的[可预测过程](@entry_id:262945) $\xi_t$，使得：
$$
dM_t = \xi_t^\top dW_t
$$
这是一个 **加法** 表示。而我们寻找的Girsanov SDE $dM_t = M_t (\theta_t^\top dW_t)$ 是一个 **乘法** 结构。通过比较这两个表达式，只要 $M_t  0$（这通常由 $Z_T0$ 保证），我们就可以立即确定Girsanov核：
$$
\theta_t = \xi_t / M_t
$$
（符号取决于约定）。因此，MRT为我们提供了一种从给定的[鞅](@entry_id:267779)密度中“提取”出Girsanov核的系统方法，展示了[随机分析](@entry_id:188809)理论内部的和谐统一。

### 局限性与统计推断

[Girsanov定理](@entry_id:147068)的一个关键应用是在统计学中为[随机过程模型](@entry_id:272197)构造 **[似然比](@entry_id:170863) (likelihood ratio)**。然而，这个应用有一个根本性的限制 [@problem_id:2989893]。

考虑两个由SDE描述的模型：
$$
\text{模型 0: } dX_t = b_0(X_t) dt + \sigma_0(X_t) dW_t
$$
$$
\text{模型 1: } dX_t = b_1(X_t) dt + \sigma_1(X_t) dW_t
$$
如果这两个模型的 **[扩散](@entry_id:141445)系数不同**，即 $\sigma_0 \not\equiv \sigma_1$，那么它们在路径空间上生成的测度 $\mathbb{P}_0$ 和 $\mathbb{P}_1$ 是 **相互奇异的 (mutually singular)**。

原因在于二次变差的不变性。对于一个连续观测到的路径 $(X_t)_{t \in [0,T]}$，我们可以（在理论上）计算出其二次变差 $\langle X \rangle_T = \int_0^T \sigma^2(X_s) ds$。这个值是路径的一个确定性泛函。如果 $\sigma_0 \neq \sigma_1$，那么一个路径的二次变差要么符合模型0，要么符合模型1，但几乎不可能同时符合两者。这意味着，支持 $\mathbb{P}_0$ 的路径集合与支持 $\mathbb{P}_1$ 的路径集合是完全不相交的。

相互奇异的测度之间不存在[Radon-Nikodym导数](@entry_id:158399)，因此也就不存在似然比。[Girsanov定理](@entry_id:147068)描述的是 **等价** 测度之间的变换，它无法连接两个相互奇异的测度。结论是：**[Girsanov定理](@entry_id:147068)不能用于比较具有不同[扩散](@entry_id:141445)系数的SDE模型**。

在这种情况下，[统计推断](@entry_id:172747)必须依赖于离散观测数据。通过对过程进行离散采样，我们可以构建一个近似的 **拟似然函数**（例如，使用Euler-Maruyama近似的转移密度），从而进行参数估计和[模型比较](@entry_id:266577)。对于高频数据，可以通过计算[已实现二次变差](@entry_id:188084)来非常精确地估计[扩散](@entry_id:141445)参数。一旦[扩散](@entry_id:141445)系数被确定，我们就可以在具有相同[扩散](@entry_id:141445)系数的模型族内，应用[Girsanov定理](@entry_id:147068)来比较不同的漂移项。