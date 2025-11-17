## 引言
[随机过程](@entry_id:159502)是现代科学与工程中描述不确定性和动态演化现象的通用语言。在这宏大的理论体系中，[高斯过程](@entry_id:182192)与泊松过程如同两根基石，分别代表了连续变化和离散事件这两种最基本的随机性模式。[高斯过程](@entry_id:182192)以其优雅的数学结构和对[连续函数](@entry_id:137361)的强大建模能力，在机器学习、信号处理和金融领域占据核心地位；而泊松过程则以其对“纯粹随机”事件流的精确刻画，成为物理学、生物学和排队论等众多学科不可或缺的工具。然而，深入理解这两种过程的内在联系、本质区别以及如何将它们结合以应对更复杂的现实世界问题，仍然是许多研究者和实践者面临的挑战。

本文旨在系统性地剖析和比较[高斯过程](@entry_id:182192)与泊松过程。我们将带领读者穿越理论的深度与应用的广度，构建一幅关于这两个基本过程的完整图景。
- 在 **“原理与机制”** 一章中，我们将从第一性原理出发，严格构建这两种过程，推导它们的核心性质，并深入比较它们的统计结构，揭示其在[噪声模型](@entry_id:752540)和[随机微分方程](@entry_id:146618)层面上的根本差异。
- 接着，在 **“应用与跨学科联系”** 一章，我们将展示这些理论如何转化为强大的建模工具，应用于从[分子生物学](@entry_id:140331)的基因表达到数论中的[黎曼猜想](@entry_id:177083)等广泛的科学前沿问题。
- 最后，**“动手实践”** 部分将提供具体编码和推导练习，帮助读者将理论知识转化为实践技能。

通过这一结构化的学习路径，本文旨在为读者提供一个坚实的理论基础和广阔的应用视野，从而能够自信地运用这些强大的随机模型来解决其研究领域中的不确定性问题。让我们首先深入到这两种过程的数学核心。

## 原理与机制

继引言之后，本章深入探讨高斯过程与泊松过程的数学原理和核心机制。我们将分别构建这两种过程，阐明它们的定义性特征，并对比分析它们的样本[轨道](@entry_id:137151)特性、底层统计结构以及在构建更复杂随机模型中的作用。我们将从基本公理出发，推导出它们的关键性质，最终展示如何运用[测度变换](@entry_id:157887)等高等工具来操纵它们的动态行为。

### 高斯过程：相关性的世界

高斯过程（Gaussian Process, GP）是[随机过程](@entry_id:159502)理论的基石之一，其优雅之处在于它完全由其一阶和二阶矩决定。这使得[高斯过程](@entry_id:182192)在机器学习、空间统计和金融建模等领域得到了广泛应用。

#### 通过[有限维分布](@entry_id:197042)定义

一个[随机过程](@entry_id:159502) $\{X_t\}_{t \in T}$ 被称为 **高斯过程**，如果对于任何有限的时间索引集合 $\{t_1, t_2, \dots, t_d\} \subset T$，随机向量 $\boldsymbol{X} = (X_{t_1}, X_{t_2}, \dots, X_{t_d})^{\top}$ 都服从一个多元正态（高斯）[分布](@entry_id:182848)。

这一定义是高斯过程的核心。它意味着，一旦我们知道了过程在任意有限个点上的[联合分布](@entry_id:263960)，我们就掌握了该过程的全部信息。一个[多元正态分布](@entry_id:175229)完全由其[均值向量](@entry_id:266544) $\boldsymbol{\mu}$ 和[协方差矩阵](@entry_id:139155) $\Sigma$ 确定。因此，整个高斯过程也完全由其 **[均值函数](@entry_id:264860)** $m(t)$ 和 **[协方差函数](@entry_id:265031)** (或称 **[核函数](@entry_id:145324)**) $K(s, t)$ 确定：

- **[均值函数](@entry_id:264860)**: $m(t) = \mathbb{E}[X_t]$
- **[协方差函数](@entry_id:265031)**: $K(s, t) = \operatorname{Cov}(X_s, X_t) = \mathbb{E}[(X_s - m(s))(X_t - m(t))]$

对于任意时间点集合 $\boldsymbol{t} = (t_1, \dots, t_d)^\top$，对应的随机向量 $\boldsymbol{X}_{\boldsymbol{t}} = (X_{t_1}, \dots, X_{t_d})^\top$ 的[均值向量](@entry_id:266544)为 $\boldsymbol{m}_{\boldsymbol{t}} = (m(t_1), \dots, m(t_d))^\top$，协方差矩阵 $\Sigma_{\boldsymbol{t}}$ 的元素为 $(\Sigma_{\boldsymbol{t}})_{ij} = K(t_i, t_j)$。只要[协方差矩阵](@entry_id:139155) $\Sigma_{\boldsymbol{t}}$ 是可逆的，该向量的[联合概率密度函数](@entry_id:267139) (PDF) 就可以明确写出 [@problem_id:2978002]：
$$f_{\boldsymbol{X}_{\boldsymbol{t}}}(\boldsymbol{x}) = \frac{1}{(2\pi)^{d/2} (\det(\Sigma_{\boldsymbol{t}}))^{1/2}} \exp\left(-\frac{1}{2}(\boldsymbol{x}-\boldsymbol{m}_{\boldsymbol{t}})^\top \Sigma_{\boldsymbol{t}}^{-1} (\boldsymbol{x}-\boldsymbol{m}_{\boldsymbol{t}})\right)
$$
这个性质是高斯过程分析和应用的基石。

#### 条件性质与[高斯过程回归](@entry_id:276025)

[高斯过程](@entry_id:182192)最强大的应用之一是基于观测数据进行推断，这通常被称为 **[高斯过程回归](@entry_id:276025)**。假设我们已经观测到过程在时间点 $\boldsymbol{t} = (t_1, \dots, t_d)^\top$ 的值为 $\boldsymbol{x}$，我们希望预测过程在新的时间点 $t^\star$ 的值。

这个任务本质上是计算条件分布 $p(X_{t^\star} | \boldsymbol{X}_{\boldsymbol{t}} = \boldsymbol{x})$。由于高斯分布的优良性质，这个[条件分布](@entry_id:138367)仍然是[高斯分布](@entry_id:154414)。我们可以通过考察增广向量 $(X_{t^\star}, \boldsymbol{X}_{\boldsymbol{t}}^\top)^\top$ 的联合分布来推导其均值和[方差](@entry_id:200758)。该增广向量服从一个[联合高斯](@entry_id:636452)[分布](@entry_id:182848)，其[均值向量](@entry_id:266544)和协方差矩阵可以分块表示为：
$$
\boldsymbol{\mu}_{\text{joint}} = \begin{pmatrix} m(t^\star) \\ \boldsymbol{m}_{\boldsymbol{t}} \end{pmatrix}, \quad \Sigma_{\text{joint}} = \begin{pmatrix} K(t^\star, t^\star)  \boldsymbol{k}_{\star}^{\top} \\ \boldsymbol{k}_{\star}  \Sigma_{\boldsymbol{t}} \end{pmatrix}
$$
其中，$\boldsymbol{k}_{\star}$ 是一个列向量，包含了新点 $t^\star$ 与所有观测点之间的协[方差](@entry_id:200758)，即 $(\boldsymbol{k}_{\star})_i = K(t^\star, t_i)$。

利用[多元正态分布](@entry_id:175229)的条件公式（可以通过在联合PDF的指数项上[配方法](@entry_id:265480)或利用[分块矩阵求逆](@entry_id:148059)公式推导），我们可以得到条件分布的均值和[方差](@entry_id:200758) [@problem_id:2978002]：
$$
\mathbb{E}[X_{t^{\star}} \mid \boldsymbol{X}_{\boldsymbol{t}}=\boldsymbol{x}] = m(t^\star) + \boldsymbol{k}_{\star}^\top \Sigma_{\boldsymbol{t}}^{-1} (\boldsymbol{x} - \boldsymbol{m}_{\boldsymbol{t}})
$$
$$
\operatorname{Var}(X_{t^{\star}} \mid \boldsymbol{X}_{\boldsymbol{t}}=\boldsymbol{x}) = K(t^\star, t^\star) - \boldsymbol{k}_{\star}^\top \Sigma_{\boldsymbol{t}}^{-1} \boldsymbol{k}_{\star}
$$
条件均值给出了在给定观测数据 $\boldsymbol{x}$ 的情况下对 $X_{t^\star}$ 的“最佳”[点估计](@entry_id:174544)。这个估计直观地将先验均值 $m(t^\star)$ 与一个修正项结合起来，该修正项是观测残差 $(\boldsymbol{x} - \boldsymbol{m}_{\boldsymbol{t}})$ 的线性组合。权重由协[方差](@entry_id:200758)决定，有效地利用了数据点之间的相关性。[条件方差](@entry_id:183803)则量化了我们预测的不确定性，它等于先验[方差](@entry_id:200758) $K(t^\star, t^\star)$ 减去一个由观测数据提供的信息量所解释的[方差](@entry_id:200758)。

#### 样本[轨道](@entry_id:137151)的正则性

高斯过程的另一个重要理论问题是其样本[轨道](@entry_id:137151)（即时间函数 $t \mapsto X(t, \omega)$）的性质，例如连续性或[光滑性](@entry_id:634843)。这些性质完全由[协方差函数](@entry_id:265031)在对角线附近的行为决定。

考虑一个中心平稳高斯过程（$m(t)=0, K(s,t)=K(t-s)$）。增量 $X(t) - X(s)$ 的[方差](@entry_id:200758)为：
$$
\mathbb{E}[(X(t) - X(s))^2] = \mathbb{E}[X(t)^2] + \mathbb{E}[X(s)^2] - 2\mathbb{E}[X(t)X(s)] = 2(K(0) - K(t-s))
$$
假设当时间差 $\tau \to 0$ 时，[协方差函数](@entry_id:265031)满足：
$$
K(0) - K(\tau) \approx c|\tau|^{\alpha}
$$
对于某些常数 $c > 0$ 和 $\alpha \in (0, 2]$。指数 $\alpha$ 描述了过程在短时间尺度上的去相关速度。$\alpha$ 越大，过程的样本[轨道](@entry_id:137151)就越光滑。

利用 **Kolmogorov–Chentsov [连续性定理](@entry_id:262016)**，我们可以将增量的矩与[轨道](@entry_id:137151)的[Hölder连续性](@entry_id:161357)联系起来。对于一个中心[高斯变量](@entry_id:276673) $Z \sim \mathcal{N}(0, \sigma^2)$，其 $p$ 阶绝对矩为 $\mathbb{E}[|Z|^p] = C_p \sigma^p$，其中 $C_p$ 是一个仅依赖于 $p$ 的常数。对于增量 $X(t)-X(s)$，其[方差](@entry_id:200758) $\sigma_{t-s}^2 \approx 2c|t-s|^\alpha$。因此，
$$
\mathbb{E}[|X(t) - X(s)|^p] \approx C_p (2c|t-s|^{\alpha})^{p/2} = C' |t-s|^{\alpha p / 2}
$$
Kolmogorov–Chentsov定理指出，若 $\mathbb{E}[|X(t) - X(s)|^p] \leq C |t-s|^{1+q}$ 对某些 $p, q > 0$ 成立，则过程的样本[轨道](@entry_id:137151)几乎必然是 $\gamma$-Hölder连续的，其中 $\gamma  q/p$。为了使 $\alpha p / 2 > 1$，我们必须选择足够大的 $p$。通过优化 $p$ 的选择，我们可以证明，对于任意 $\gamma  \alpha/2$，样本[轨道](@entry_id:137151)都是局部 $\gamma$-Hölder连续的。因此，[Hölder连续性](@entry_id:161357)的[上确界](@entry_id:140512)指数为 $\gamma^\star = \alpha/2$ [@problem_id:2977998]。

这个结果意义重大。例如，对于标准的[维纳过程](@entry_id:137696)（布朗运动），其协[方差](@entry_id:200758) $K(s,t)=\min(s,t)$，对于[平稳增量](@entry_id:263290)过程，这对应于 $\alpha=1$。因此，其Hölder指数上确界为 $1/2$，这证实了布朗运动[轨道](@entry_id:137151)是连续但处处不可微的著名事实。

### 泊松过程：跳跃的世界

与[高斯过程](@entry_id:182192)描述的连续变化形成鲜明对比，泊松过程是描述离散事件在时间（或空间）中随机发生的数学模型。它是最基本的[计数过程](@entry_id:260664)。

#### 通过增量定义

一个[计数过程](@entry_id:260664) $\{N_t\}_{t \geq 0}$ 被称为速率为 $\lambda > 0$ 的 **[齐次泊松过程](@entry_id:263782)**，如果它满足以下公理 [@problem_id:2978022]：

1.  **初始状态**: $N_0 = 0$。
2.  **[独立增量](@entry_id:262163)**: 对任意 $0 \le t_1  t_2  \dots  t_k$，增量 $N_{t_2} - N_{t_1}, N_{t_3} - N_{t_2}, \dots, N_{t_k} - N_{t_{k-1}}$ 是相互独立的[随机变量](@entry_id:195330)。
3.  **[平稳增量](@entry_id:263290)**: 任意长度为 $h$ 的时间区间内的事件数增量 $N_{t+h} - N_t$ 的[分布](@entry_id:182848)只依赖于 $h$，而与 $t$ 无关。
4.  **无穷小性质**: 在一个极小的时间区间 $h$ 内，恰好发生一次事件的概率近似与 $h$ 成正比，而发生两次或更多次事件的概率可以忽略不计。更精确地：
    - $\mathbb{P}(N_h = 1) = \lambda h + o(h)$
    - $\mathbb{P}(N_h \ge 2) = o(h)$
    由此可得 $\mathbb{P}(N_h = 0) = 1 - \lambda h + o(h)$。

这些公理刻画了一个“纯粹随机”的事件流：事件的发生没有记忆，且在任何时刻发生的可能性都是恒定的。

#### 推导[泊松分布](@entry_id:147769)

从这些基本公理出发，我们可以推导出在任意时刻 $t$，事件总数 $N_t$ 的[概率分布](@entry_id:146404)。令 $P_n(t) = \mathbb{P}(N_t = n)$。考虑在时刻 $t+h$ 的状态，其中 $h$ 是一个无穷小量。

对于 $n=0$ 的情况，事件 $\{N_{t+h}=0\}$ 发生的唯一方式是 $\{N_t=0\}$ 且在区间 $(t, t+h]$ 内没有事件发生。利用平稳和[独立增量](@entry_id:262163)性质：
$$P_0(t+h) = P_0(t) \mathbb{P}(N_h=0) = P_0(t)(1-\lambda h + o(h))
$$
整理并取极限 $h \to 0$，我们得到一个[微分方程](@entry_id:264184)：
$$
\frac{dP_0(t)}{dt} = -\lambda P_0(t)
$$
结合[初始条件](@entry_id:152863) $P_0(0)=1$（因为 $N_0=0$），我们解得 $P_0(t) = \exp(-\lambda t)$。

对于 $n \ge 1$，事件 $\{N_{t+h}=n\}$ 可以通过两种主要方式发生：
- 在时刻 $t$ 有 $n$ 个事件，且在 $(t, t+h]$ 内没有事件发生。概率为 $P_n(t)(1-\lambda h + o(h))$。
- 在时刻 $t$ 有 $n-1$ 个事件，且在 $(t, t+h]$ 内发生一个事件。概率为 $P_{n-1}(t)(\lambda h + o(h))$。
其他情况（如在 $(t, t+h]$ 内发生两次或更多事件）的概率都是 $o(h)$。

将这些加起来，我们得到：
$$P_n(t+h) \approx P_n(t)(1-\lambda h) + P_{n-1}(t)\lambda h
$$
整理并取极限，得到一个[微分](@entry_id:158718)-差分方程组 [@problem_id:2978022]：
$$
\frac{dP_n(t)}{dt} = \lambda P_{n-1}(t) - \lambda P_n(t)
$$
这个[方程组](@entry_id:193238)可以逐个求解。我们已经知道 $P_0(t)$，代入 $n=1$ 的方程可以解出 $P_1(t)$，以此类推。通过[数学归纳法](@entry_id:138544)，可以证明其通解为：
$$P_n(t) = \frac{(\lambda t)^n}{n!} \exp(-\lambda t)
$$
这正是期望为 $\lambda t$ 的[泊松分布](@entry_id:147769)的[概率质量函数](@entry_id:265484)。

#### 到达时间与无记忆性

我们也可以从事件之间的时间间隔角度来研究泊松过程。令 $\tau_k = \inf\{t > 0 : N_t \ge k\}$ 为第 $k$ 个事件的到达时间。

第一个事件的到达时间 $\tau_1$ 晚于 $t$ 的事件 $\{\tau_1 > t\}$ 等价于在 $[0, t]$ 时间内没有事件发生的事件 $\{N_t=0\}$。因此，$\tau_1$ 的生存函数为：
$$
\mathbb{P}(\tau_1 > t) = \mathbb{P}(N_t = 0) = \exp(-\lambda t)
$$
这表明 $\tau_1$ 服从参数为 $\lambda$ 的指数分布。其概率密度函数为 $f_{\tau_1}(t) = \lambda \exp(-\lambda t)$ [@problem_id:2978059]。

更有趣的是，所有事件间的间隔时间 $T_k = \tau_k - \tau_{k-1}$（其中 $\tau_0=0$）都是[相互独立](@entry_id:273670)且同[分布](@entry_id:182848)的指数[随机变量](@entry_id:195330)。这源于泊松过程的 **强马尔可夫性**。考虑在第 $k$ 个事件发生后，等待第 $k+1$ 个事件的时间。条件于直到 $\tau_k$ 为止的所有历史信息（记为 $\mathcal{F}_{\tau_k}$），过程的未来演化与过去无关，就如同一个新的泊松过程从时刻 $\tau_k$ 开始。因此，
$$
\mathbb{P}(\tau_{k+1} - \tau_k > s \mid \mathcal{F}_{\tau_k}) = \mathbb{P}(N(\tau_k+s) - N(\tau_k) = 0 \mid \mathcal{F}_{\tau_k}) = \mathbb{P}(N(s)=0) = \exp(-\lambda s)
$$
这个结果表明，无论我们已经等待了多久，未来还需要等待的时间的[分布](@entry_id:182848)保持不变。这就是指数分布的 **[无记忆性](@entry_id:201790)**，它是泊松过程“纯粹随机”特性的直接体现 [@problem_id:2978059]。

#### 扩展：[复合泊松过程](@entry_id:140283)

我们可以通过给泊松过程的每个事件附加一个随机的“大小”或“标记”来构建更丰富的模型。这便引出了 **[复合泊松过程](@entry_id:140283)**。一个[复合泊松过程](@entry_id:140283) $X_t$ 定义为：
$$X_t = \sum_{k=1}^{N_t} Y_k
$$
其中 $\{N_t\}$ 是一个速率为 $\lambda$ 的泊松过程，而 $\{Y_k\}$ 是一系列[独立同分布](@entry_id:169067)（i.i.d.）的[随机变量](@entry_id:195330)，代表每次跳跃的大小，且与 $\{N_t\}$ 过程独立。

我们可以使用全期望和[全方差公式](@entry_id:177482)来计算 $X_t$ 的矩。首先对 $N_t$ 取条件，然后对 $N_t$ 的[分布](@entry_id:182848)求期望 [@problem_id:2977996]。
$$
\mathbb{E}[X_t] = \mathbb{E}[\mathbb{E}[X_t | N_t]] = \mathbb{E}[N_t \mathbb{E}[Y_1]] = \mathbb{E}[N_t] \mathbb{E}[Y_1] = \lambda t \mathbb{E}[Y_1]
$$
$$
\operatorname{Var}(X_t) = \mathbb{E}[\operatorname{Var}(X_t | N_t)] + \operatorname{Var}(\mathbb{E}[X_t | N_t]) = \mathbb{E}[N_t \operatorname{Var}(Y_1)] + \operatorname{Var}(N_t \mathbb{E}[Y_1])
$$
$$
= \lambda t \operatorname{Var}(Y_1) + \lambda t (\mathbb{E}[Y_1])^2 = \lambda t (\operatorname{Var}(Y_1) + (\mathbb{E}[Y_1])^2) = \lambda t \mathbb{E}[Y_1^2]
$$
这两个结果被称为 **Wald 恒等式**。它们表明[复合泊松过程的均值和方差](@entry_id:261306)随时间[线性增长](@entry_id:157553)，其增长率分别由跳跃大小的一阶和二阶矩决定。

### 深度比较：[累积量](@entry_id:152982)与噪声

[高斯过程](@entry_id:182192)与泊松过程的根本差异体现在它们的统计结构中，特别是它们的[累积量](@entry_id:152982)。

#### [累积量生成函数](@entry_id:748109)

一个[随机变量](@entry_id:195330)的 **[累积量生成函数 (CGF)](@entry_id:203926)** 是其[矩生成函数 (MGF)](@entry_id:199360) 的对数，记为 $K(\theta) = \ln \mathbb{E}[\exp(\theta Z)]$。它的[泰勒展开](@entry_id:145057)系数是该[随机变量](@entry_id:195330)的累积量。第一[累积量](@entry_id:152982)是均值，第二[累积量](@entry_id:152982)是[方差](@entry_id:200758)，第三[累积量](@entry_id:152982)是偏度的度量，等等。[高斯分布](@entry_id:154414)的一个显著特征是其所有三阶及以上的累积量均为零。

我们可以通过考察对一个确定性函数 $f(t)$ 的积分来对比这两种过程 [@problem_id:2977997]。

- **高斯情况**: 考虑积分 $I_G = \int_0^T f(t)X(t)dt$，其中 $X(t)$ 是一个中心[高斯过程](@entry_id:182192)。由于 $I_G$ 是[高斯过程](@entry_id:182192)的线性泛函，它本身也是一个高斯[随机变量](@entry_id:195330)。其均值为零，[方差](@entry_id:200758)为 $\sigma_G^2 = \int_0^T \int_0^T f(t)f(s)K(t,s)dsdt$。因此，其CGF是：
  $$
  K_G(\theta) = \frac{1}{2} \sigma_G^2 \theta^2 = \frac{1}{2}\theta^2 \int_0^T \int_0^T f(t)f(s)K(t,s)dsdt
  $$
  这是一个关于 $\theta$ 的二次函数，反映了[高斯分布](@entry_id:154414)只有前两个累积量非零的事实。

- **泊松情况**: 考虑积分 $I_P = \int_0^T f(t)dN(t) = \sum_k f(\tau_k)$，其中 $N(t)$ 是一个强度为 $\lambda(t)$ 的非[齐次泊松过程](@entry_id:263782)。通过将积分近似为离散和，并利用泊松增量的独立性及其MGF，可以证明 $I_P$ 的CGF是：
  $$
  K_P(\theta) = \int_0^T (\exp(\theta f(t)) - 1) \lambda(t) dt
  $$
  对这个表达式关于 $\theta$ 求导，可以发现所有阶的[累积量](@entry_id:152982)通常都是非零的。这个积分形式的CGF是莱维-辛钦公式的一个特例，它深刻地揭示了泊松过程作为一种[跳跃过程](@entry_id:180953)的本质，其统计特性无法仅由前两个矩完全描述。

#### [噪声模型](@entry_id:752540)：[白噪声](@entry_id:145248)与散粒噪声

在物理和工程学中，“噪声”通常被非正式地理解为像布朗运动或泊松过程这样的[随机过程](@entry_id:159502)的时间导数。这种导数在经典意义上不存在，但可以在[广义函数](@entry_id:182848)（[分布](@entry_id:182848)）的框架下被严格定义。

- **[高斯白噪声](@entry_id:749762)**: [高斯白噪声](@entry_id:749762) $\eta(t)$ 是布朗运动 $W_t$（一种高斯过程）的[分布导数](@entry_id:181138)。它不是一个取值为函数的经典[随机过程](@entry_id:159502)，而是一个随机广义过程，其作用于检验函数 $\varphi(t)$ 的方式由随机积分定义：$\langle \eta, \varphi \rangle = \int \varphi(t)dW_t$ [@problem_id:2978067]。其关键特征是它的[自相关函数](@entry_id:138327)是狄拉克 $\delta$ 函数：
  $$
  \mathbb{E}[\eta(t)\eta(s)] = 2D \delta(t-s)
  $$
  其中 $D$ 是噪声强度。这表示在任何不同时刻的噪声值都是不相关的。由于其高斯性，所有高阶累积量都为零。

- **泊松[散粒噪声](@entry_id:140025)**: 类似地，泊松散粒噪声 $\xi(t)$ 是[复合泊松过程](@entry_id:140283)的[分布导数](@entry_id:181138)。对于一个速率为 $\lambda$，跳跃大小恒为 $a$ 的[齐次泊松过程](@entry_id:263782)，其导数是一个[脉冲序列](@entry_id:753864) $\xi(t) = \sum_k a \delta(t-t_k)$。其中心化后的噪声 $\tilde{\xi}(t) = \xi(t) - \lambda a$ 的自相关函数也是一个 $\delta$ 函数 [@problem_id:2815965]：
  $$
  \mathbb{E}[\tilde{\xi}(t)\tilde{\xi}(s)] = \lambda a^2 \delta(t-s)
  $$
尽管两种噪声的自相关函数形式相似（都是“白”的），但它们的底层统计结构完全不同。泊松[散粒噪声](@entry_id:140025)的所有阶累积量均非零。

这种差异对[随机微分方程](@entry_id:146618)的性质有深远影响。一个由[加性高斯白噪声](@entry_id:269320)驱动的系统的[概率密度](@entry_id:175496)演化由一个[二阶偏微分方程](@entry_id:175326)——**[福克-普朗克方程](@entry_id:140155)** 描述。这是因为高斯噪声的所有高阶（$n \ge 3$）[累积量](@entry_id:152982)为零，导致描述概率密度演化的 **[Kramers-Moyal 展开](@entry_id:159458)** 在二阶之后精确截断。相反，由泊松散粒噪声驱动的系统，由于其所有阶累积量均非零，其Kramers-Moyal展开不会截断，[演化方程](@entry_id:268137)是一个更复杂的积分-[微分方程](@entry_id:264184)，即 **主方程** [@problem_id:2815965]。

### 操纵动态：[测度变换](@entry_id:157887)一瞥

在[随机分析](@entry_id:188809)中，一个极其强大的工具是 **[测度变换](@entry_id:157887)**，它允许我们改变底层[概率空间](@entry_id:201477)的测度，从而改变[随机过程](@entry_id:159502)的统计性质。**Girsanov 定理** 是这一领域的核心结果。

假设我们有一个定义在概率空间 $(\Omega, \mathcal{F}, \mathbb{P})$ 上的标准布朗运动 $W_t$ 和一个具有 $\mathbb{P}$-可料强度 $\lambda_t$ 的点过程 $N_t$，且两者在 $\mathbb{P}$ 下独立。我们可以定义一个新的[概率测度](@entry_id:190821) $\mathbb{Q}$，使得：
1.  在 $\mathbb{Q}$ 下，$W_t$ 具有一个漂移项 $\theta_t$，即 $\tilde{W}_t = W_t - \int_0^t \theta_s ds$ 成为一个标准布朗运动。
2.  在 $\mathbb{Q}$ 下，点过程 $N_t$ 的强度变为一个新的可料过程 $\tilde{\lambda}_t$。

从 $\mathbb{P}$ 到 $\mathbb{Q}$ 的变换由 Radon-Nikodym 导数 $\frac{d\mathbb{Q}}{d\mathbb{P}}$ 描述。其对数，即[对数似然比](@entry_id:274622) $\ell_T = \log(\frac{d\mathbb{Q}}{d\mathbb{P}}|_{\mathcal{F}_T})$，可以被明确计算出来。由于 $W_t$ 和 $N_t$ 在 $\mathbb{P}$ 下是独立的，总的[对数似然比](@entry_id:274622)是两部分贡献之和 [@problem_id:2978014]：
$$
\ell_T = \ell_T^W + \ell_T^N
$$
- **高斯部分 (Girsanov 定理)**: 改变布朗运动的漂移对应的[对数似然比](@entry_id:274622)为：
  $$
  \ell_T^W = \int_0^T \theta_t dW_t - \frac{1}{2} \int_0^T \theta_t^2 dt
  $$
- **泊松部分 (点过程的[Girsanov定理](@entry_id:147068))**: 改变点过程的强度对应的[对数似然比](@entry_id:274622)为：
  $$
  \ell_T^N = \int_0^T \log\left(\frac{\tilde{\lambda}_t}{\lambda_t}\right) dN_t - \int_0^T (\tilde{\lambda}_t - \lambda_t) dt
  $$
  其中，[随机积分](@entry_id:198356) $\int_0^T \log(\dots)dN_t$ 实际上是在所有跳跃时刻 $\tau_k$ 对函数 $\log(\tilde{\lambda}_{\tau_k}/\lambda_{\tau_k})$ 的求和。

最终，总的[对数似然比](@entry_id:274622)为：
$$
\ell_T = \int_0^T \theta_t dW_t - \frac{1}{2} \int_0^T \theta_t^2 dt + \sum_{0  \tau_k \le T} \log\left(\frac{\tilde{\lambda}_{\tau_k}}{\lambda_{\tau_k}}\right) - \int_0^T (\tilde{\lambda}_t - \lambda_t) dt
$$