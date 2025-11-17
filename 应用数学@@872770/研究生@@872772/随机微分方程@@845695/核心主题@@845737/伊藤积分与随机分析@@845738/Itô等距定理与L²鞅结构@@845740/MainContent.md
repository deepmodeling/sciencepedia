## 引言
伊藤积分是现代[随机分析](@entry_id:188809)的支柱，为理解和建模由随机噪声驱动的动态系统提供了根本性的工具。然而，与经典的[黎曼-斯蒂尔杰斯积分](@entry_id:136464)不同，对布朗运动这类路径极不规则的过程进行积分，需要一套全新的数学框架。本文旨在填补从直观概念到严谨理论之间的鸿沟，系统性地阐述[伊藤积分的构造](@entry_id:637486)机理及其深远的结构性内涵，其核心正是**[伊藤等距](@entry_id:637467)定理 (Itô Isometry)** 与**平方可积鞅 (L²-martingale)** 理论。

通过本文的学习，读者将踏上一条从基础到应用的认知之旅。在“**原理与机制**”一章中，我们将从最简单的分段常值过程出发，逐步构建起完整的[伊藤积分](@entry_id:272774)理论，揭示[伊藤等距](@entry_id:637467)定理如何成为将积分延拓至[希尔伯特空间](@entry_id:261193)的桥梁，并阐明积分过程的[鞅性质](@entry_id:261270)。接着，在“**应用与跨学科联系**”一章中，我们将展示这些抽象的数学原理如何在[金融数学](@entry_id:143286)、物理学和工程学等领域转化为强大的分析工具，例如通过[鞅表示定理](@entry_id:180851)理解完备市场，或利用推广的积分理论分析[随机偏微分方程](@entry_id:188292)。最后，“**动手实践**”部分将提供一系列精心设计的问题，帮助读者巩固理论知识，并将其应用于解决具体的[随机过程](@entry_id:159502)分析问题。

## 原理与机制

本章旨在深入探讨伊藤[随机积分](@entry_id:198356)的数学构造，重点阐述其两大理论基石：**[伊藤等距](@entry_id:637467)定理 (Itô Isometry)** 与**平方可积鞅 (Square-Integrable Martingale)** 的结构。我们将从最基本的简单过程出发，逐步构建起一套严谨的理论框架，该框架不仅适用于[标准布朗运动](@entry_id:197332)，也能自然地推广至更广泛的[连续局部鞅](@entry_id:204638)。通过本章的学习，读者将深刻理解[随机积分](@entry_id:198356)何以成为现代[随机分析](@entry_id:188809)的核心工具，并洞悉其背后的精妙数学机制。

### 从简单过程出发：[伊藤积分的构造](@entry_id:637486)基础

[随机积分](@entry_id:198356)的理论大厦始于其最简单的构件：对**简单[可预测过程](@entry_id:262945) (simple predictable processes)** 的积分。一个简单[可预测过程](@entry_id:262945) $H = (H_t)_{t \ge 0}$ 是一个分段常值函数，其形式如下：
$$
H_t = \sum_{k=0}^{n-1} H_k \mathbf{1}_{(t_k, t_{k+1}]}(t)
$$
其中 $0 = t_0  t_1  \dots  t_n = T$ 是时间区间 $[0, T]$ 的一个分割，$\mathbf{1}_{(t_k, t_{k+1}]}(t)$ 是区间 $(t_k, t_{k+1}]$ 上的[示性函数](@entry_id:261577)。此处的关键要求是“可预测性”，即在每个时间区间 $(t_k, t_{k+1}]$ 上，过程的取值 $H_k$ 是一个在区间开始时刻 $t_k$ 就已知的[随机变量](@entry_id:195330)。严格来说，$H_k$ 必须是 $\mathcal{F}_{t_k}$-可测的，其中 $(\mathcal{F}_t)_{t \ge 0}$ 是我们考虑的 filtration（信息流）。

对于这样一个简单过程 $H_t$ 以及一个标准布朗运动 $W_t$，我们仿照[黎曼-斯蒂尔杰斯积分](@entry_id:136464)的形式，自然地将其[伊藤积分](@entry_id:272774)定义为一个有限和：
$$
\int_0^T H_t \, dW_t := \sum_{k=0}^{n-1} H_k (W_{t_{k+1}} - W_{t_k})
$$
这个定义直观地体现了在每个小区间上，用该区间开始时的“策略” $H_k$ 乘以该区间的“随机噪声增量” $W_{t_{k+1}} - W_{t_k}$。

这个定义的深刻内涵源于布朗运动的基本性质。回忆一下，一个标准 $(\mathcal{F}_t)$-布朗运动 $W_t$ 满足：
1.  $W_0=0$。
2.  样本[轨道](@entry_id:137151) $t \mapsto W_t$ 几乎必然连续。
3.  对于任意 $0 \le s  t$，增量 $W_t - W_s$ 服从均值为 $0$、[方差](@entry_id:200758)为 $t-s$ 的[正态分布](@entry_id:154414)，即 $W_t - W_s \sim \mathcal{N}(0, t-s)$。
4.  对于任意 $0 \le s  t$，增量 $W_t - W_s$ 独立于 $\mathcal{F}_s$（即过去的信息）。

基于这些性质，我们可以计算上述定义的[随机积分](@entry_id:198356)的二阶矩，这引出了随机积分理论的第一个核心结果——**[伊藤等距](@entry_id:637467)定理**。考虑积分 $I_H = \int_0^T H_t \, dW_t$，并假定每个 $H_k$ 都是平方可积的（即 $\mathbb{E}[H_k^2]  \infty$）。我们来计算其二阶矩 $\mathbb{E}[I_H^2]$。为简化记号，令 $\Delta W_k = W_{t_{k+1}} - W_{t_k}$。

$$
\mathbb{E}[I_H^2] = \mathbb{E}\left[ \left( \sum_{k=0}^{n-1} H_k \Delta W_k \right)^2 \right] = \sum_{j,k=0}^{n-1} \mathbb{E}[H_j H_k \Delta W_j \Delta W_k]
$$

这个双[重求和](@entry_id:275405)可以分为对角项（$j=k$）和非对角项（$j \ne k$）。这里的关键洞见源于布朗运动增量的独立性，这使得不同时间区间的积分项之间呈现出一种正交性。[@problem_id:2982173]

对于非对角项，假设 $j  k$。那么 $t_j  t_{j+1} \le t_k  t_{k+1}$。由于 $H_j$, $H_k$ 和 $\Delta W_j$ 都是 $\mathcal{F}_{t_k}$-可测的，我们可以使用[条件期望的塔性质](@entry_id:181314)：
$$
\mathbb{E}[H_j H_k \Delta W_j \Delta W_k] = \mathbb{E}\big[ \mathbb{E}[H_j H_k \Delta W_j \Delta W_k | \mathcal{F}_{t_k}] \big] = \mathbb{E}\big[ H_j H_k \Delta W_j \mathbb{E}[\Delta W_k | \mathcal{F}_{t_k}] \big]
$$
因为增量 $\Delta W_k = W_{t_{k+1}} - W_{t_k}$ 独立于 $\mathcal{F}_{t_k}$ 且均值为零，所以 $\mathbb{E}[\Delta W_k | \mathcal{F}_{t_k}] = \mathbb{E}[\Delta W_k] = 0$。这意味着所有非对角项的期望均为零。

现在只剩下对角项：
$$
\mathbb{E}[I_H^2] = \sum_{k=0}^{n-1} \mathbb{E}[H_k^2 (\Delta W_k)^2]
$$
再次使用[条件期望的塔性质](@entry_id:181314)，并利用 $H_k$ 的 $\mathcal{F}_{t_k}$-可测性：
$$
\mathbb{E}[H_k^2 (\Delta W_k)^2] = \mathbb{E}\big[ \mathbb{E}[H_k^2 (\Delta W_k)^2 | \mathcal{F}_{t_k}] \big] = \mathbb{E}\big[ H_k^2 \mathbb{E}[(\Delta W_k)^2 | \mathcal{F}_{t_k}] \big]
$$
由于 $\Delta W_k$ 独立于 $\mathcal{F}_{t_k}$，其条件二阶矩等于其[方差](@entry_id:200758)，即 $\mathbb{E}[(\Delta W_k)^2 | \mathcal{F}_{t_k}] = \mathrm{Var}(\Delta W_k) = t_{k+1} - t_k$。代入上式得到：
$$
\mathbb{E}[I_H^2] = \sum_{k=0}^{n-1} \mathbb{E}[H_k^2] (t_{k+1} - t_k)
$$
观察这个结果的右边。对于我们的简单过程 $H_t$，有 $H_t^2 = \sum_{k=0}^{n-1} H_k^2 \mathbf{1}_{(t_k, t_{k+1}]}(t)$。因此，
$$
\mathbb{E}\left[ \int_0^T H_t^2 \, dt \right] = \mathbb{E}\left[ \int_0^T \sum_{k=0}^{n-1} H_k^2 \mathbf{1}_{(t_k, t_{k+1}]}(t) \, dt \right] = \sum_{k=0}^{n-1} \mathbb{E}[H_k^2] (t_{k+1} - t_k)
$$
比较两边的结果，我们得到了对简单[可预测过程](@entry_id:262945)成立的**[伊藤等距](@entry_id:637467)定理 (Itô Isometry)**：
$$
\mathbb{E}\left[ \left( \int_0^T H_t \, dW_t \right)^2 \right] = \mathbb{E}\left[ \int_0^T H_t^2 \, dt \right]
$$
这个等式是[伊藤积分](@entry_id:272774)理论的基石。它在[随机变量](@entry_id:195330)空间 $L^2(\Omega, \mathcal{F}, \mathbb{P})$ 中的范数与一个看似完全不同的、在时空乘积空间上的范数之间建立了一座桥梁。同时，通过类似的推导可以证明，积分过程 $M_t = \int_0^t H_s \, dW_s$ 是一个**平方可积[鞅](@entry_id:267779) (square-integrable martingale)** [@problem_id:2982166]。

### 拓展积分定义：[可预测被积函数](@entry_id:194063)的希尔伯特空间

为了将[伊藤积分](@entry_id:272774)从简单的分段常值过程推广到更广泛的函数类别，我们需要一个合适的[函数空间](@entry_id:143478)。这个空间必须足够大，以包含我们感兴趣的各种[随机过程](@entry_id:159502)；同时，它也必须具有良好的数学结构（如完备性），以便我们能够进行极限操作。这个理想的空间正是由**[可预测过程](@entry_id:262945) (predictable processes)** 构成的[希尔伯特空间](@entry_id:261193)。

一个[随机过程](@entry_id:159502) $H = (H_t(\omega))_{t \ge 0, \omega \in \Omega}$ 被称为**可预测的**，如果它作为 $(\omega, t)$ 的二元函数，是关于**可预测$\sigma$-代数 (predictable $\sigma$-algebra)** $\mathcal{P}$ 可测的。可预测$\sigma$-代数 $\mathcal{P}$ 是定义在乘积空间 $\Omega \times [0, T]$ 上的，它代表了在每个时刻 $t$ “刚刚到来之前” 可用的所有信息。这个概念可以通过两种等价的方式来精确定义 [@problem_id:2982178]：

1.  **由左连续过程生成**：$\mathcal{P}$ 是使得所有左连续且适应于 filtration $(\mathcal{F}_t)$ 的过程都成为可测函数的最小$\sigma$-代数。直观上，一个左连续过程在 $t$ 时刻的值 $X_t = \lim_{s \uparrow t} X_s$ 是由 $t$ 之前的路径完全决定的，因此是“可预测”的。

2.  **由可预测矩形生成**：$\mathcal{P}$ 是由形如 $A \times \{0\}$（其中 $A \in \mathcal{F}_0$）和 $A \times (s, t]$（其中 $0 \le s  t \le T$ 且 $A \in \mathcal{F}_s$）的集合（称为**可预测矩形 (predictable rectangles)**）生成的$\sigma$-代数。这个定义更具体地体现了“预测”的思想：在时间区间 $(s, t]$ 内发生的事件由截至时刻 $s$ 的信息 $A \in \mathcal{F}_s$ 所决定。

有了可预测性的定义，我们便可以定义进行[伊藤积分](@entry_id:272774)的被积函数所在的[希尔伯特空间](@entry_id:261193)。这个空间通常记为 $L^2_{\text{pred}}(\Omega \times [0,T])$ 或 $\mathcal{H}^2$，它由所有满足下述条件的实值[可预测过程](@entry_id:262945) $H$ 构成：
$$
\mathbb{E}\left[ \int_0^T H_t^2 \, dt \right]  \infty
$$
这个空间配备了[内积](@entry_id:158127)：
$$
\langle H, G \rangle = \mathbb{E}\left[ \int_0^T H_t G_t \, dt \right]
$$
其诱导的范数为 $\|H\|_{\mathcal{H}^2} = \sqrt{\langle H, H \rangle} = \left(\mathbb{E}\left[ \int_0^T H_t^2 \, dt \right]\right)^{1/2}$。

一个至关重要的事实是，$L^2_{\text{pred}}(\Omega \times [0,T])$ 是一个**[希尔伯特空间](@entry_id:261193) (Hilbert space)**，即一个完备的[内积空间](@entry_id:271570) [@problem_id:2982154]。其完备性源于一个泛化的[测度论](@entry_id:139744)结果（Riesz-Fischer 定理），即在任何[测度空间](@entry_id:191702)上定义的 $L^2$ 空间都是完备的。在这里，我们的[测度空间](@entry_id:191702)是 $(\Omega \times [0,T], \mathcal{P}, \mu)$，其中测度 $\mu$ 是乘[积测度](@entry_id:266846) $\mathbb{P} \otimes dt$ 在可预测$\sigma$-代数 $\mathcal{P}$ 上的限制。空间的完备性意味着任何在此范数下的柯西序列都会收敛到空间中的一个元素。正是这个性质，使得我们可以将伊藤积分从简单过程的[稠密子集](@entry_id:264458)延拓到整个空间。

### [伊藤等距](@entry_id:637467)定理及其在一般积分构造中的应用

现在我们拥有了所有工具，可以将[伊藤积分](@entry_id:272774)的定义从简单[可预测过程](@entry_id:262945)推广到 $L^2_{\text{pred}}(\Omega \times [0,T])$ 中的任意过程 $H$。这个推广过程是一个标准的“三步曲” [@problem_id:282183]：

1.  **在[稠密子集](@entry_id:264458)上定义**: 我们已经在简单[可预测过程](@entry_id:262945)构成的空间上定义了[伊藤积分](@entry_id:272774)。测度论的一个基本结果告诉我们，简单[可预测过程](@entry_id:262945)的集合在 $L^2_{\text{pred}}(\Omega \times [0,T])$ 空间中是**稠密的**。这意味着对于任何 $H \in L^2_{\text{pred}}$，都存在一个简单[可预测过程](@entry_id:262945)序列 $(H^{(n)})_{n \ge 1}$，使得 $\|H^{(n)} - H\|_{\mathcal{H}^2} \to 0$。

2.  **利用等距性质**: 对于这个序列，我们考察其对应的积分序列 $I_n = \int_0^T H_t^{(n)} \, dW_t$。根据我们对简单过程导出的[伊藤等距](@entry_id:637467)定理，有：
    $$
    \mathbb{E}\left[ (I_n - I_m)^2 \right] = \mathbb{E}\left[ \left( \int_0^T (H_t^{(n)} - H_t^{(m)}) \, dW_t \right)^2 \right] = \mathbb{E}\left[ \int_0^T (H_t^{(n)} - H_t^{(m)})^2 \, dt \right] = \|H^{(n)} - H^{(m)}\|_{\mathcal{H}^2}^2
    $$
    由于 $(H^{(n)})$ 是 $\mathcal{H}^2$ 中的柯西序列，上式表明 $(I_n)$ 是 $L^2(\Omega, \mathcal{F}_T, \mathbb{P})$ 空间中的一个柯西序列。

3.  **延拓到[完备空间](@entry_id:159932)**: 因为 $L^2(\Omega, \mathcal{F}_T, \mathbb{P})$ 是一个完备的希尔伯特空间，柯西序列 $(I_n)$ 必有极限。我们便将这个极限定义为 $H$ 的伊藤积分：
    $$
    \int_0^T H_t \, dW_t := \lim_{n \to \infty} \int_0^T H_t^{(n)} \, dW_t \quad (\text{在 } L^2(\Omega) \text{ 中收敛})
    $$
这个定义是合理的，因为可以证明极限与逼近序列 $(H^{(n)})$ 的选择无关。通过这个极限过程，[伊藤等距](@entry_id:637467)定理也自然地延拓到了整个 $L^2_{\text{pred}}$ 空间。对于任意 $H \in L^2_{\text{pred}}$，我们有：
$$
\mathbb{E}\left[ \left( \int_0^T H_t \, dW_t \right)^2 \right] = \mathbb{E}\left[ \int_0^T H_t^2 \, dt \right]
$$
这就是[伊藤积分](@entry_id:272774)理论中最广为人知的**[伊藤等距](@entry_id:637467)定理**。通过[极化恒等式](@entry_id:271819)，我们还可以得到其更具一般性的[双线性形式](@entry_id:746794)：对于任意 $H, G \in L^2_{\text{pred}}$，
$$
\mathbb{E}\left[ \left(\int_0^T H_t \, dW_t\right) \left(\int_0^T G_t \, dW_t\right) \right] = \mathbb{E}\left[ \int_0^T H_t G_t \, dt \right]
$$
这个定理的本质是，伊藤积分映射 $I: H \mapsto \int_0^T H_t \, dW_t$ 是一个从希尔伯特空间 $L^2_{\text{pred}}(\Omega \times [0,T])$ 到 $L^2(\Omega, \mathcal{F}_T, \mathbb{P})$ 的**线性[等距映射](@entry_id:150881)**。

### 伊藤积分的结构与性质

#### [鞅性质](@entry_id:261270)与二次变差

[伊藤积分](@entry_id:272774)最重要的结构性质之一是它生成了鞅。对于任何 $H \in L^2_{\text{pred}}$，过程 $M_t = \int_0^t H_s \, dW_s$ 是一个关于 filtration $(\mathcal{F}_t)$ 的**平方可积[鞅](@entry_id:267779)**。这意味着：
1.  $M_t$ 对 $(\mathcal{F}_t)$ 是适应的。
2.  对所有 $t$，$\mathbb{E}[|M_t|]  \infty$ （实际上，$\mathbb{E}[M_t^2]  \infty$）。
3.  对于 $s  t$，有 $\mathbb{E}[M_t | \mathcal{F}_s] = M_s$。

此外，作为一种特殊的[连续鞅](@entry_id:185466)，[伊藤积分](@entry_id:272774)具有一个明确的**二次变差 (quadratic variation)**。[连续鞅](@entry_id:185466)的二次变差 $[M]_t$ 描述了鞅平方的“累计变化率”。一个深刻的结果是，$M_t^2 - [M]_t$ 是一个[鞅](@entry_id:267779)。对于伊藤积分 $M_t = \int_0^t H_s \, dW_s$，其二次变差（在这里也等于其可预测二次变差 $\langle M \rangle_t$）由一个非常简洁的公式给出 [@problem_id:2982183]：
$$
[M]_t = \langle M \rangle_t = \int_0^t H_s^2 \, ds
$$
这个公式直观地说明了随机积分 $M_t$ 的波动性或“变异性”完全由被积函数 $H_s$ 的平方在时间上的累积所决定。

#### 被积函数的唯一性

[伊藤等距](@entry_id:637467)定理的一个直接且重要的推论是被积函数的唯一性。假设我们有两个不同的[可预测过程](@entry_id:262945) $H, K \in \mathcal{H}^2$，它们生成的[鞅](@entry_id:267779)在某个时刻 $T$ 是相同的，即 $\int_0^T H_s \, dW_s = \int_0^T K_s \, dW_s$ 几乎必然成立。这意味着它们的差的积分为零：
$$
\int_0^T (H_s - K_s) \, dW_s = 0 \quad a.s.
$$
根据[伊藤等距](@entry_id:637467)定理，这个积分的二阶矩为零：
$$
\mathbb{E}\left[ \left( \int_0^T (H_s - K_s) \, dW_s \right)^2 \right] = 0
$$
这等价于：
$$
\mathbb{E}\left[ \int_0^T (H_s - K_s)^2 \, ds \right] = 0
$$
这个表达式正是 $H-K$ 在希尔伯特空间 $\mathcal{H}^2$ 中范数的平方。范数为零意味着 $H-K$ 是该空间中的零元素。在 $L^2$ 空间中，零元素对应的是[几乎处处](@entry_id:146631)为零的函数。因此，我们得出结论：
$$
H_t = K_t \quad \text{对于 } (\omega, t) \in \Omega \times [0,T] \text{ 几乎处处成立}
$$
这里的“[几乎处处](@entry_id:146631)”是相对于乘[积测度](@entry_id:266846) $\mathbb{P} \otimes dt$ 而言的。这意味着，给定一个由[伊藤积分](@entry_id:272774)表示的鞅，其对应的[可预测被积函数](@entry_id:194063)在 $L^2_{\text{pred}}$ 的意义下是唯一的 [@problem_id:2982186]。值得注意的是，这种唯一性是 $L^2$ 意义下的，并不保证两个过程的样本[轨道](@entry_id:137151)是完全相同的（即不可区分的），尽管在许多实际应用中，我们可以找到一个足够好的版本来保证后者。

### 理论的深化与推广

#### 从布朗运动到[连续局部鞅](@entry_id:204638)

到目前为止，我们的讨论都围绕着对布朗运动的积分。然而，伊藤积分理论的强大之处在于它可以被推广到对更一般的**[连续局部鞅](@entry_id:204638) (continuous local martingales)** 进行积分。

一个过程 $M_t$ 被称为[连续局部鞅](@entry_id:204638)，如果它是一个具有[连续路径](@entry_id:187361)的[适应过程](@entry_id:187710)，并且存在一个递增且[几乎必然收敛](@entry_id:265812)于无穷的停时序列 $(\tau_n)_{n \ge 1}$，使得每个停过程 $M_{t \wedge \tau_n}$ 都是一个（真）[鞅](@entry_id:267779)。

对于一个[连续局部鞅](@entry_id:204638) $M$，我们可以通过[Doob-Meyer分解](@entry_id:187728)定理定义其**可预测二次变差 (predictable quadratic variation)** $\langle M \rangle_t$。它是唯一的一个连续、递增、可预测的过程，满足 $\langle M \rangle_0 = 0$ 且 $M_t^2 - \langle M \rangle_t$ 是一个[局部鞅](@entry_id:186755) [@problem_id:2982188]。

有了这个概念，我们可以为对 $M$ 的积分定义相应的被积[函数空间](@entry_id:143478) $L^2(M)$，它由所有满足下述条件的[可预测过程](@entry_id:262945) $H$ 构成：
$$
\mathbb{E}\left[ \int_0^T H_s^2 \, d\langle M \rangle_s \right]  \infty
$$
对 $H \in L^2(M)$ 的积分 $\int_0^t H_s \, dM_s$ 同样可以通过简单过程逼近来构造，并且满足一个推广的[伊藤等距](@entry_id:637467)定理：
$$
\mathbb{E}\left[ \left( \int_0^T H_s \, dM_s \right)^2 \right] = \mathbb{E}\left[ \int_0^T H_s^2 \, d\langle M \rangle_s \right]
$$
这个推广是极其强大的，它将随机积分从布朗运动这一特定驱动力的框架中解放出来，使其适用于由任何[连续局部鞅](@entry_id:204638)驱动的系统。

此外，**局部化 (localization)** 技术使我们能够为那些不满足全局平方[可积条件](@entry_id:158502)，而仅仅是“局部”平方可积的被积函数定义积分 [@problem_id:2982172]。如果 $H$ 是一个[可预测过程](@entry_id:262945)，且存在一个[停时](@entry_id:261799)序列 $\tau_n \uparrow \infty$ 使得对每个 $n$，$\mathbb{E}[\int_0^{\tau_n} H_s^2 d\langle M \rangle_s]  \infty$，我们仍然可以定义积分 $I_t = \int_0^t H_s \, dM_s$。其结果 $I_t$ 不再保证是一个真[鞅](@entry_id:267779)，而是一个[连续局部鞅](@entry_id:204638)，其二次变差仍然是 $\langle I \rangle_t = \int_0^t H_s^2 d\langle M \rangle_s$。

#### 结构性视角：[维纳混沌](@entry_id:181915)与[鞅表示定理](@entry_id:180851)

为了更深刻地理解[伊藤积分](@entry_id:272774)的结构，我们可以将其置于由布朗运动生成的所有[随机变量](@entry_id:195330)构成的空间 $L^2(\Omega, \mathcal{F}_T^B, \mathbb{P})$ 中来考察。

首先考虑一个特殊情况：当被积函数 $h(t)$ 是一个确定性函数（而非[随机过程](@entry_id:159502)），且 $h \in L^2([0,T], dt)$ 时，伊藤积分 $I(h) = \int_0^T h(t) \, dW_t$ 是一个定义明确的[随机变量](@entry_id:195330)。[伊藤等距](@entry_id:637467)定理此时简化为：
$$
\mathbb{E}[I(h)^2] = \int_0^T h(t)^2 \, dt = \|h\|_{L^2([0,T])}^2
$$
这个结果表明，积分映射 $I$ 是从确定性函数空间 $L^2([0,T])$ 到[随机变量](@entry_id:195330)空间 $L^2(\Omega)$ 的一个等距映射。其像空间，即所有形如 $I(h)$ 的[随机变量](@entry_id:195330)构成的集合，被称为**第一[维纳混沌](@entry_id:181915) (first Wiener chaos)**，记为 $\mathcal{C}_1$。这个空间本质上是由布朗运动 $(W_t)_{t \in [0,T]}$ 张成的（闭）高斯[子空间](@entry_id:150286)。[伊藤积分](@entry_id:272774)映射 $I: L^2([0,T]) \to \mathcal{C}_1$ 是一个[等距同构](@entry_id:273188) [@problem_id:2982159]。根据**维纳-伊藤混沌分解定理 (Wiener-Itô chaos decomposition)**，整个 $L^2(\Omega, \mathcal{F}_T^B, \mathbb{P})$ 空间可以被[正交分解](@entry_id:148020)为无穷多个混沌[子空间之和](@entry_id:180324) $L^2(\Omega) = \bigoplus_{k=0}^\infty \mathcal{C}_k$，其中 $\mathcal{C}_0$ 是常数，$\mathcal{C}_1$ 是我们刚刚讨论的第一混沌，$\mathcal{C}_k$（$k \ge 2$）则对应于 $k$ 重随机积分。伊藤积分为我们提供了理解这个基本结构的第一块拼图。

最后，一个自然的问题是：在由布朗运动生成的 filtration $\mathcal{F}^B$ 下，是否所有的（平方可积）鞅都可以表示为关于该布朗运动的伊藤积分？答案是肯定的。这就是著名的**[鞅表示定理](@entry_id:180851) (Martingale Representation Theorem)**。该定理指出，任何关于布朗 filtration $\mathcal{F}^B$ 的平方可积鞅 $M_t$ 都可以唯一地表示为：
$$
M_t = M_0 + \int_0^t H_s \, dW_s
$$
其中 $H$ 是一个满足适当可积性的[可预测过程](@entry_id:262945)。这个定理表明，在布朗世界中，所有的“意外”或“创新”都源于布朗运动自身。没有任何独立于布朗运动的随机性来源可以生成一个新的鞅。

然而，这个强大的性质是 filtration 的特殊属性，而非普适规律。如果 filtration 包含了除布朗运动之外的其他独立信息源，[表示定理](@entry_id:637872)就不再成立。例如，如果我们用一个独立的[随机变量](@entry_id:195330) $Y$ 来扩大布朗 filtration，得到新的 filtration $\mathcal{G}_t = \mathcal{F}_t^B \vee \sigma(Y)$，那么过程 $M_t = Y - \mathbb{E}[Y]$ 就是一个非平凡的 $\mathcal{G}$-[鞅](@entry_id:267779)。然而，由于 $M_t$ 的样本[轨道](@entry_id:137151)是常数，其二次变差为零。如果它能被表示为 $\int_0^t H_s \, dW_s$，那么其二次变差应为 $\int_0^t H_s^2 \, ds$，这将迫使 $H$ [几乎处处](@entry_id:146631)为零，从而积分也为零。这说明 $M_t$ 无法被表示为关于 $W$ 的积分。这个例子凸显了**[可预测表示性质](@entry_id:637685) (Predictable Representation Property, PRP)** 是布朗 filtration 的一个深刻结构特征，它保证了信息来源的单一性 [@problem_id:2982161]。