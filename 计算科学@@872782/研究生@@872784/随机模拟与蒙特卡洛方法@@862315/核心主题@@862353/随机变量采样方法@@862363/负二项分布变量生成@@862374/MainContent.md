## 引言
负二项分布是概率论与统计学中的一个核心[离散分布](@entry_id:193344)，因其能够灵活地对“过离散”计数数据进行建模而显得尤为重要。在[蒙特卡洛模拟](@entry_id:193493)、[计算统计学](@entry_id:144702)以及基因组学等数据密集型领域，高效且准确地生成服从[负二项分布](@entry_id:262151)的[随机变量](@entry_id:195330)是执行模拟实验和[贝叶斯推断](@entry_id:146958)的基础。

然而，从理论定义到稳健的计算实现之间存在着一道鸿沟。选择哪种生成算法？不同算法在效率和精度上有何权衡？这些问题是所有模拟实践者都必须面对的挑战。本文旨在系统性地解答这些问题，为读者提供一个关于负[二项随机变量生成](@entry_id:746810)的全面视角。

在接下来的内容中，我们将分步深入探讨这一主题。第一章“原理与机制”将从第一性原理出发，剖析[负二项分布](@entry_id:262151)的数学构造和核心生成算法，如几何分布求和法与强大的伽马-泊松混合法。第二章“应用与交叉学科联系”将视野扩展到实际应用，展示[负二项分布](@entry_id:262151)如何在[算法工程](@entry_id:635936)、[生物统计学](@entry_id:266136)和基因组学中解决真实世界的问题。最后，在“动手实践”部分，您将通过具体的编程练习，将理论知识转化为实践技能。

让我们从理解负二项分布的底层原理与机制开始，为后续的[算法设计](@entry_id:634229)与应用探索打下坚实的基础。

## 原理与机制

本章深入探讨负二项分布的数学原理及其[随机变量生成](@entry_id:756434)的核心机制。继引言之后，我们将从负二项分布的基本定义出发，阐述其不同的[参数化](@entry_id:272587)形式及其与相关[概率分布](@entry_id:146404)的联系。随后，我们将系统地介绍几种主要的生成算法，包括基于[分布](@entry_id:182848)构造的直接方法和更通用的数值方法。最后，本章将对这些算法的计算性能进行分析与比较，为在蒙特卡洛模拟实践中选择最优方法提供理论依据。

### 负二项分布的基本定义与性质

在深入研究生成算法之前，我们必须首先精确理解[负二项分布](@entry_id:262151)的定义。与其他[离散分布](@entry_id:193344)（如二项分布和泊松分布）相比，[负二项分布](@entry_id:262151)的独特之处在于其“[生成模型](@entry_id:177561)”（generative story）的设定。

#### [生成模型](@entry_id:177561)与两种参数化

[负二项分布](@entry_id:262151)源于对一系列[独立同分布](@entry_id:169067)的**伯努利试验**（Bernoulli trials）的观察，每次试验成功的概率为 $p \in (0,1)$。与在固定次数试验中计算成功次数的**[二项分布](@entry_id:141181)**（Binomial distribution）不同，[负二项分布](@entry_id:262151)的试验次数是随机的。其核心思想是，试验持续进行，直到观察到预先设定的成功次数 $r$ 为止。

在这一基本框架下，存在两种定义[随机变量](@entry_id:195330)的常见约定，即两种**[参数化](@entry_id:272587)**（parameterization）[@problem_id:3323104]：

1.  **失败次数[参数化](@entry_id:272587)**：[随机变量](@entry_id:195330) $X$ 定义为在达到第 $r$ 次成功之前所观察到的**失败次数**。在这种设定下，$X$ 的取值范围（即**支撑集**，support）为 $\{0, 1, 2, \dots\}$，因为在累积 $r$ 次成功之前，可能发生任意多次失败。

2.  **总试验次数[参数化](@entry_id:272587)**：[随机变量](@entry_id:195330) $T$ 定义为达到第 $r$ 次成功所需的**总试验次数**。由于至少需要 $r$ 次试验才能获得 $r$ 次成功，因此 $T$ 的支撑集为 $\{r, r+1, r+2, \dots\}$。

这两种[参数化](@entry_id:272587)之间存在一个简单的[线性关系](@entry_id:267880)。总试验次数 $T$ 必然等于成功次数 $r$ 与失败次数 $X$ 之和，即 $T = X + r$。理解这一关系对于在不同文献或软件库之间转换参数至关重要。

让我们从第一性原理推导总试验次数[参数化](@entry_id:272587)下的**[概率质量函数](@entry_id:265484)**（Probability Mass Function, PMF）。事件 $\{T=t\}$ 意味着第 $t$ 次试验是第 $r$ 次成功。这等价于两个子事件同时发生：(1) 第 $t$ 次试验为成功；(2) 在前 $t-1$ 次试验中，恰好有 $r-1$ 次成功。

由于各次试验独立，事件 (1) 的概率为 $p$。对于事件 (2)，它描述了一个包含 $r-1$ 次成功和 $(t-1)-(r-1) = t-r$ 次失败的序列。从 $t-1$ 次试验中选择 $r-1$ 次成功的位置，组[合数](@entry_id:263553)为 $\binom{t-1}{r-1}$。任何一个特定序列的概率为 $p^{r-1}(1-p)^{t-r}$。因此，事件 (2) 的总概率为 $\binom{t-1}{r-1}p^{r-1}(1-p)^{t-r}$。

将两个独立子事件的概率相乘，我们得到 $T$ 的 PMF [@problem_id:332104]：
$$
\mathbb{P}(T=t) = \binom{t-1}{r-1} p^r (1-p)^{t-r}, \quad t \in \{r, r+1, \dots\}
$$
通过关系 $t = k+r$，我们可以推导出失败次数 $X$ 的 PMF。令 $X=k$，则 $T=k+r$。代入上式可得：
$$
\mathbb{P}(X=k) = \binom{k+r-1}{r-1} p^r (1-p)^k = \binom{k+r-1}{k} p^r (1-p)^k, \quad k \in \{0, 1, 2, \dots\}
$$
本书后续内容将主要采用失败次数参数化，记为 $X \sim \mathrm{NB}(r, p)$。

为了更清晰地定位负二项分布，我们可以对比它与二项分布和泊松分布的[生成模型](@entry_id:177561) [@problem_id:3323115]。
- **[二项分布](@entry_id:141181)** $\mathrm{Bin}(n,p)$：试验次数 $n$ 和成功概率 $p$ 是固定的，[随机变量](@entry_id:195330)是成功次数 $X$，其支撑集为有限的 $\{0, 1, \dots, n\}$。
- **[泊松分布](@entry_id:147769)** $\mathrm{Poisson}(\lambda)$：在一个固定的暴露区间（如时间或空间）内，事件发生率 $\lambda$ 是固定的，[随机变量](@entry_id:195330)是事件发生次数 $Y$，其支撑集为无限的 $\{0, 1, 2, \dots\}$。
- **负二项分布** $\mathrm{NB}(r,p)$：成功次数 $r$ 和成功概率 $p$ 是固定的，[随机变量](@entry_id:195330)是达到该目标所需的失败次数 $X$（或总试验次数 $T$），其支撑集是无限的 $\{0, 1, 2, \dots\}$。

#### 扩展至实数参数 $r$

在伯努利试验的经典解释中，参数 $r$（成功次数）自然是正整数。然而，在许多[统计建模](@entry_id:272466)应用（如[回归模型](@entry_id:163386)）和模拟算法中，将 $r$ 扩展到任意正实数 $r \in (0, \infty)$ 是非常有用的。这种扩展是通过使用**伽马函数**（Gamma function） $\Gamma(\cdot)$ 来推广组合数实现的 [@problem_id:3323032]。

回顾组[合数](@entry_id:263553)的伽马函数形式：$\binom{n}{k} = \frac{\Gamma(n+1)}{\Gamma(k+1)\Gamma(n-k+1)}$。将此应用于负二项分布的 PMF 中的组合项 $\binom{k+r-1}{k}$，我们得到：
$$
\binom{k+r-1}{k} = \frac{\Gamma(k+r)}{\Gamma(k+1)\Gamma(r)}
$$
这个表达式对于任何正实数 $r$ 和非负整数 $k$ 都是良定义的，因为伽马函数 $\Gamma(z)$ 在 $z > 0$ 时有定义且为正。因此，我们可以定义一个适用于任意 $r > 0$ 和 $p \in (0,1)$ 的广义负二项分布 PMF：
$$
\mathbb{P}(X=k) = \frac{\Gamma(k+r)}{\Gamma(k+1)\Gamma(r)} p^r (1-p)^k, \quad k \in \{0, 1, 2, \dots\}
$$
为了证明这是一个合法的 PMF，我们需要验证其总和为 1。这可以通过广义二项定理 $\sum_{k=0}^\infty \binom{a+k-1}{k} z^k = (1-z)^{-a}$ (对于 $|z|1$) 来证明。令 $a=r$ 及 $z=1-p$，我们有：
$$
\sum_{k=0}^{\infty} \mathbb{P}(X=k) = p^r \sum_{k=0}^{\infty} \frac{\Gamma(k+r)}{\Gamma(k+1)\Gamma(r)} (1-p)^k = p^r (1-(1-p))^{-r} = p^r p^{-r} = 1
$$
由于 $p \in (0,1)$，故 $z = 1-p \in (0,1)$，满足[收敛条件](@entry_id:166121) $|z|1$。因此，该 PMF 对于任意 $r > 0$ 都是合法且规范的 [@problem_id:3323032]。这一扩展的理论基础将在后续讨论伽马-泊松混合法时进一步阐明。

### 核心生成构造与算法

理解了负二项分布的定义后，我们转向其核心问题：如何生成服从该[分布](@entry_id:182848)的[随机变量](@entry_id:195330)？多种算法源于其不同的数学构造。

#### 序列伯努利试验法

最直观的方法是直接模拟其原始的生成模型 [@problem_id:3323020]。该算法的步骤如下：
1.  初始化失败次数计数器 `failures = 0` 和成功次数计数器 `successes = 0`。
2.  当 `successes  r` 时，循环执行以下操作：
    a. 生成一个服从参数为 $p$ 的[伯努利分布](@entry_id:266933)的[随机变量](@entry_id:195330)（例如，生成一个 `Uniform(0,1)` 随机数 $U$，若 $U  p$ 则为成功，否则为失败）。
    b. 若试验成功，则 `successes` 加 1；若试验失败，则 `failures` 加 1。
3.  当 `successes` 达到 $r$ 时，循环终止。返回 `failures` 的最终值。

此方法简单明了，直接体现了[负二项分布](@entry_id:262151)的定义，但其计算效率与生成的[随机变量](@entry_id:195330)的值成正比，即与总试验次数成正比。当期望的失败次数很大时（例如 $p$很小），此方法可能非常耗时。

#### 几何分布求和法 (整数 $r$)

当 $r$ 为整数时，一个更高效的构造是利用**几何分布**（Geometric distribution）。几何分布 $\mathrm{Geom}(p)$ 描述了在第一次成功前所需的失败次数。其 PMF 为 $\mathbb{P}(G=k) = (1-p)^k p$，$k \in \{0,1,2,\dots\}$。

负二项[随机变量](@entry_id:195330) $X \sim \mathrm{NB}(r, p)$ 可以被视为 $r$ 个独立的几何[随机变量](@entry_id:195330)之和。直观上，总的失败次数 $X$ 可以分解为：
$X = $ (第1次成功前的失败次数) + (第1次与第2次成功间的失败次数) + $\dots$ + (第 $(r-1)$ 次与第 $r$ 次成功间的失败次数)。
由于伯努利试验的独立性，每一段“成功间”的失败次数都独立地服从相同的[几何分布](@entry_id:154371) $\mathrm{Geom}(p)$。因此，我们可以将 $X$ 表示为：
$$
X = G_1 + G_2 + \dots + G_r, \quad \text{其中 } G_i \stackrel{\text{i.i.d.}}{\sim} \mathrm{Geom}(p)
$$
我们可以通过**[概率生成函数](@entry_id:190573)**（Probability Generating Function, PGF）来严格证明这两种构造的等价性 [@problem_id:3323020]。一个几何[随机变量](@entry_id:195330) $G$ 的 PGF 是 $\mathcal{G}_G(z) = E[z^G] = \frac{p}{1 - z(1-p)}$。根据 PGF 的性质，$r$ 个[独立同分布随机变量](@entry_id:270381)之和的 PGF 是单个变量 PGF 的 $r$ 次方：
$$
\mathcal{G}_X(z) = (\mathcal{G}_G(z))^r = \left(\frac{p}{1 - z(1-p)}\right)^r
$$
另一方面，直接从负二项分布的 PMF 定义出发，其 PGF 为 $\mathcal{G}_X(z) = \sum_{k=0}^{\infty} \binom{k+r-1}{k} p^r (1-p)^k z^k = p^r (1 - z(1-p))^{-r}$，这与上面的结果完全相同。由于 PGF 唯一确定了非负整数值[随机变量](@entry_id:195330)的[分布](@entry_id:182848)，两种构造是等价的。

这个构造引出了一种生成算法 [@problem_id:3323074] [@problem_id:3323020]：
1.  循环 $r$ 次。
2.  在每次循环中，生成一个服从 $\mathrm{Geom}(p)$ 的[随机变量](@entry_id:195330) $G_i$。
3.  将这 $r$ 个几何[随机变量](@entry_id:195330)求和，得到最终的负二项[随机变量](@entry_id:195330) $X$。

生成几何[随机变量](@entry_id:195330)本身可以通过[逆变换法](@entry_id:141695)高效完成。若 $U \sim \mathrm{Uniform}(0,1)$，则 $G = \lfloor \frac{\ln(U)}{\ln(1-p)} \rfloor$ 是一个服从 $\mathrm{Geom}(p)$ 的[随机变量](@entry_id:195330)（这里我们利用了若 $U \sim \mathrm{Uniform}(0,1)$, 则 $1-U$ 也服从 $\mathrm{Uniform}(0,1)$ 的性质）。此方法的计算成本与 $r$ 成正比，通常比序列伯努利法更高效，尤其是在 $p$ 较小时。

#### 伽马-泊松混合法 (实数 $r$)

上述两种方法要么效率不高，要么仅限于整数 $r$。一个极为强大且通用的方法是**伽马-泊松混合**（Gamma-Poisson mixture）构造，它自然地处理了任意正实数 $r$ 的情况 [@problem_id:3323085] [@problem_id:3323032]。

该方法将[负二项分布](@entry_id:262151)看作一个两阶段的生成过程：
1.  首先，生成一个随机[率参数](@entry_id:265473) $\Lambda$，它服从一个伽马[分布](@entry_id:182848) $\Lambda \sim \mathrm{Gamma}(\text{shape}=r, \text{rate}=\beta)$。
2.  然后，以这个生成的率 $\Lambda$ 为参数，生成一个泊松[随机变量](@entry_id:195330) $X \sim \mathrm{Poisson}(\Lambda)$。

这个过程得到的 $X$ 的无条件分布就是一个负二项分布。我们可以通过积分来推导其 PMF [@problem_id:3323044]。$X$ 的 PMF 是：
$$
\mathbb{P}(X=k) = \int_0^\infty \mathbb{P}(X=k | \Lambda=\lambda) f_\Lambda(\lambda) \,d\lambda
$$
其中 $f_\Lambda(\lambda) = \frac{\beta^r}{\Gamma(r)} \lambda^{r-1} e^{-\beta\lambda}$ 是 Gamma [分布](@entry_id:182848)的[概率密度函数](@entry_id:140610) (PDF)，而 $\mathbb{P}(X=k | \Lambda=\lambda) = \frac{e^{-\lambda}\lambda^k}{k!}$ 是 Poisson [分布](@entry_id:182848)的 PMF。代入并积分：
$$
\mathbb{P}(X=k) = \int_0^\infty \frac{e^{-\lambda}\lambda^k}{k!} \frac{\beta^r}{\Gamma(r)} \lambda^{r-1} e^{-\beta\lambda} \,d\lambda = \frac{\beta^r}{k!\Gamma(r)} \int_0^\infty \lambda^{k+r-1} e^{-(\beta+1)\lambda} \,d\lambda
$$
该积分是伽马函数核的形式，其值为 $\frac{\Gamma(k+r)}{(\beta+1)^{k+r}}$。代回得到：
$$
\mathbb{P}(X=k) = \frac{\Gamma(k+r)}{k!\Gamma(r)} \frac{\beta^r}{(\beta+1)^{k+r}} = \frac{\Gamma(k+r)}{k!\Gamma(r)} \left(\frac{\beta}{\beta+1}\right)^r \left(\frac{1}{\beta+1}\right)^k
$$
通过与负二项分布的 PMF $\mathbb{P}(X=k) = \frac{\Gamma(k+r)}{k!\Gamma(r)} p^r (1-p)^k$ 对比，我们发现，只需令 $p = \frac{\beta}{\beta+1}$，或者反解出 $\beta = \frac{p}{1-p}$，两种形式便完全等价。

这个构造不仅为实数 $r$ 提供了坚实的理论基础，还引出了一种重要的统计特性：**过离散性**（overdispersion）。我们可以利用**[全期望定律](@entry_id:265946)**和**[全方差定律](@entry_id:184705)**来计算该[混合分布](@entry_id:276506)的均值和[方差](@entry_id:200758) [@problem_id:3323034] [@problem_id:3323044]。
-   **均值**：$\mathbb{E}[X] = \mathbb{E}[\mathbb{E}[X|\Lambda]] = \mathbb{E}[\Lambda] = \frac{r}{\beta} = \frac{r(1-p)}{p}$。
-   **[方差](@entry_id:200758)**：$\mathrm{Var}(X) = \mathbb{E}[\mathrm{Var}(X|\Lambda)] + \mathrm{Var}(\mathbb{E}[X|\Lambda]) = \mathbb{E}[\Lambda] + \mathrm{Var}(\Lambda) = \frac{r}{\beta} + \frac{r}{\beta^2}$。
代入 $\beta = p/(1-p)$，[方差](@entry_id:200758)可表示为：
$$
\mathrm{Var}(X) = \frac{r(1-p)}{p} + \frac{r(1-p)^2}{p^2} = \frac{r(1-p)}{p^2}
$$
注意到[方差](@entry_id:200758)可以写成 $\mathrm{Var}(X) = \mathbb{E}[X] + \frac{(\mathbb{E}[X])^2}{r}$。由于 $\frac{(\mathbb{E}[X])^2}{r} > 0$，所以 $\mathrm{Var}(X) > \mathbb{E}[X]$。这与泊松分布中[方差](@entry_id:200758)严格等于均值的性质形成鲜明对比。这种[方差](@entry_id:200758)大于均值的现象即为过离散性，这也是负二项分布在[生物统计学](@entry_id:266136)、计量经济学等领域广泛用于建模计数数据的原因。其**[方差](@entry_id:200758)-均值比**为：
$$
\frac{\mathrm{Var}(X)}{\mathbb{E}[X]} = \frac{r(1-p)/p^2}{r(1-p)/p} = \frac{1}{p}
$$
这个比值总是大于1（因为 $p1$），直观地量化了过离散的程度 [@problem_id:3323034]。

伽马-泊松混合法对应的生成算法非常直接 [@problem_id:3323085] [@problem_id:3323074]：
1.  根据目标参数 $(r, p)$，计算出伽马[分布](@entry_id:182848)的参数：shape $\alpha = r$，rate $\beta = p/(1-p)$（或 scale $\theta = 1/\beta = (1-p)/p$）。
2.  生成一个伽马[随机变量](@entry_id:195330) $\Lambda \sim \mathrm{Gamma}(r, p/(1-p))$。
3.  以 $\Lambda$ 为参数，生成一个泊松[随机变量](@entry_id:195330) $X \sim \mathrm{Poisson}(\Lambda)$。
4.  返回 $X$。

此方法的效率取决于 underlying 的伽马和泊松生成器的效率。对于现代统计软件中高度优化的生成器，该方法通常非常高效且通用。

### 通用高效生成算法

除了基于特定构造的方法，一些通用算法也可以应用于负二项分布，其中[逆变换采样法](@entry_id:142402)尤为重要。

#### [逆变换采样法](@entry_id:142402)

**[逆变换采样](@entry_id:139050)**（Inverse Transform Sampling）是一种适用于任何具有已知**[累积分布函数](@entry_id:143135)**（Cumulative Distribution Function, CDF）的[分布](@entry_id:182848)的通用方法。对于一个[离散随机变量](@entry_id:163471) $X$，其 CDF 为 $F(k) = \mathbb{P}(X \le k)$。该方法的基本步骤是 [@problem_id:3323074]：
1.  生成一个标准[均匀分布](@entry_id:194597)随机数 $U \sim \mathrm{Uniform}(0,1)$。
2.  寻找满足 $F(k-1)  U \le F(k)$ 的最小非负整数 $k$。这个 $k$ 就是我们所求的[随机变量](@entry_id:195330)。

在实践中，这意味着我们需要从 $k=0$ 开始，逐个计算 PMF $f(k)=\mathbb{P}(X=k)$，并累加得到 CDF $F(k) = F(k-1) + f(k)$，直到 $F(k) \ge U$ 为止。

直接计算每个 $f(k) = \frac{\Gamma(k+r)}{\Gamma(k+1)\Gamma(r)} p^r (1-p)^k$ 中的伽马函数和阶乘可能导致数值不稳定或计算成本高。一个更稳健、高效的策略是使用**递推关系**来更新 PMF [@problem_id:3323031]。我们已经推导出：
$$
f(k) = f(k-1) \cdot \frac{k+r-1}{k} \cdot (1-p), \quad \text{for } k \ge 1
$$
递推的起点是 $f(0) = p^r$。

基于此递推的[逆变换采样](@entry_id:139050)算法如下：
1.  给定参数 $(r, p)$ 和一个均匀随机数 $U$。
2.  初始化 $k=0$，`pmf_current` $= p^r$，`cdf_current` $= p^r$。
3.  当 `cdf_current  U` 时，循环执行：
    a. $k \leftarrow k+1$。
    b. 更新 `pmf_current` $\leftarrow$ `pmf_current` $\times \frac{k+r-1}{k} \times (1-p)$。
    c. 更新 `cdf_current` $\leftarrow$ `cdf_current` + `pmf_current`。
4.  返回当前的 $k$。

此方法的计算成本与最终生成的[随机变量](@entry_id:195330) $k$ 的值成正比。对于均值较小的[分布](@entry_id:182848)，此方法非常有效。但对于均值很大的[分布](@entry_id:182848)（例如 $p$ 极小），搜索过程可能很长。

### 算法性能与实践考量

在实际应用中，选择哪种生成算法取决于多个因素，包括参数 $(r, p)$ 的范围、所需样本量 $N$ 以及对预计算时间和内存的容忍度 [@problem_id:3323026]。

#### 不同方法的计算复杂度

让我们对前面讨论的主要算法的计算复杂度进行一番比较，假设[目标分布](@entry_id:634522)的均值为 $\mu = r(1-p)/p$。

- **序列伯努利试验法**：每次试验需要一次[随机数生成](@entry_id:138812)和比较。总试验次数的期望为 $\mathbb{E}[T] = \mathbb{E}[X+r] = \mu+r$。因此，单次生成的[期望时间复杂度](@entry_id:634638)为 $\Theta(\mu+r)$。

- **几何分布求和法 (整数 $r$)**：需要生成 $r$ 个几何[随机变量](@entry_id:195330)。如果每个几何变量的生成时间为 $\Theta(1)$（例如使用[逆变换法](@entry_id:141695)），则总时间复杂度为 $\Theta(r)$。

- **伽马-泊松混合法**：该方法的复杂度取决于其组成部分。
    - 伽马生成器：现代算法（如 Marsaglia 和 Tsang 的 ziggurat 算法）通常被认为是期望 $\Theta(1)$ 时间。
    - 泊松生成器：
        - 对于小的 $\Lambda$，简单的乘法/搜索法（Knuth 算法）期望时间为 $\Theta(\Lambda)$。
        - 对于大的 $\Lambda$，存在更复杂的算法（如基于[正态近似](@entry_id:261668)的[接受-拒绝法](@entry_id:263903)），其期望时间为 $\Theta(1)$。
    如果使用最先进的组件，伽马-泊松混合法的[期望时间复杂度](@entry_id:634638)为 $\mathbb{E}[\Theta(1) + \Theta(1)] = \Theta(1)$，与参数 $(r,p)$ 无关，这使其在均值 $\mu$ 很大时具有显著优势。然而，如果使用简单的泊松生成器，其[期望时间复杂度](@entry_id:634638)将是 $\mathbb{E}[\Theta(\Lambda)] = \Theta(\mathbb{E}[\Lambda]) = \Theta(\mu)$，与朴素的[逆变换法](@entry_id:141695)相当 [@problem_id:3323026]。

- **[逆变换采样法](@entry_id:142402) (递推)**：如前所述，搜索过程的期望步数是 $\mathbb{E}[X]+1 = \mu+1$，因此[期望时间复杂度](@entry_id:634638)为 $\Theta(\mu)$。

#### 预计算与单次生成成本的权衡

对于需要大量样本 $N$ 的情况，我们可以考虑带有**预计算**（precomputation）阶段的算法，以降低单次采样的成本。

一种常见策略是**表查找[逆变换法](@entry_id:141695)**。该方法首先计算并存储 CDF 直到一个足够大的截断点 $k_{\max}$，使得 $\mathbb{P}(X > k_{\max})$ 极小。$k_{\max}$ 的选择通常基于[分布](@entry_id:182848)的均值和[方差](@entry_id:200758)，例如 $k_{\max} \approx \mu + c\sqrt{\mathrm{Var}(X)}$，其中 $c$ 是某个常数。
- **预计算阶段**：构建大小为 $\Theta(k_{\max})$ 的 CDF 表，时间成本为 $\Theta(k_{\max})$，内存成本也为 $\Theta(k_{\max})$。
- **采样阶段**：对于每个样本，在预计算的 CDF 表上使用**二分搜索**（binary search）找到对应的 $k$。单次采样的时间成本为 $\Theta(\log k_{\max})$。

生成 $N$ 个样本的总时间为 $T_{\text{table}} = \Theta(k_{\max}) + N \cdot \Theta(\log k_{\max})$。相比之下，朴素的递推[逆变换法](@entry_id:141695)总时间为 $T_{\text{seq}} = N \cdot \Theta(\mu)$。

当 $N$ 足够大时，预计算的固定成本 $ \Theta(k_{\max})$ 被摊销，使得表查找法更优。具体来说，当 $N$ 远大于某个阈值 $N^\star$ 时，表查找法更快。这个阈值 $N^\star$ 约等于两种方法成本相等时的样本量，忽略对数项，即 $N^\star \cdot \mu \approx k_{\max}$。由于 $k_{\max}$ 通常与 $\mu$ 的[数量级](@entry_id:264888)相同，所以这个阈值 $N^\star$ 可能很小。这个分析表明，在需要大量样本的仿真场景中，牺牲一定的初始时间和内存进行预计算，可以显著提高整体效率 [@problem_id:3323026]。

总结而言，负二项[随机变量](@entry_id:195330)的生成展现了[随机模拟](@entry_id:168869)中[算法设计](@entry_id:634229)的多样性与权衡。从直接模拟其物理过程，到利用其深刻的数学构造（如与几何、伽马、泊松分布的联系），再到应用通用的数值方法，每种策略都在不同的参数范围和应用场景下各有优劣。对这些原理与机制的深入理解，是成为一名优秀[蒙特卡洛方法](@entry_id:136978)实践者的基石。