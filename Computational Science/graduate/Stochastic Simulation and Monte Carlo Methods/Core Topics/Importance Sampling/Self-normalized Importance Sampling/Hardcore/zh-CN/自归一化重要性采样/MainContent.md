## 引言
在贝叶斯推断、计算物理到机器学习等众多科学计算领域，计算某个函数在特定[概率分布](@entry_id:146404)下的[期望值](@entry_id:153208)是一项核心任务。然而，一个普遍存在的挑战是，目标[概率分布](@entry_id:146404)通常只能被确定到一个未知的归一化常数，这使得标准[蒙特卡洛方法](@entry_id:136978)和重要性抽样直接失效。[自归一化](@entry_id:636594)重要性抽样 (Self-Normalized Importance Sampling, SNIS) 正是为了解决这一根本性难题而设计的强大统计工具。

本文旨在为您提供关于 SNIS 的全面理解，从其基本原理到其在跨学科前沿研究中的广泛应用。通过本文的学习，您将掌握：

*   **原理与机制**：我们将深入剖析SNIS如何通过巧妙的比率变换来规避未知[归一化常数](@entry_id:752675)，并探讨其独特的统计特性，如偏差与相合性，以及如何通过[有效样本量](@entry_id:271661)等工具诊断其可靠性。
*   **应用与跨学科联系**：我们将展示SNIS在贝叶斯后验推断、分子动力学模拟、离策略[强化学习](@entry_id:141144)等真实世界问题中的关键作用，揭示其作为连接不同[概率模型](@entry_id:265150)的计算桥梁的价值。
*   **动手实践**：通过一系列精心设计的问题，您将有机会亲手推导和分析SNIS的关键属性，从而将理论知识转化为实践技能。

现在，让我们首先进入第一章，深入探索[自归一化](@entry_id:636594)重要性抽样的基本原理与核心机制。

## 原理与机制

在“引言”章节中，我们了解了在许多科学计算领域（例如[贝叶斯推断](@entry_id:146958)、计算物理学）中，我们常常需要计算一个函数 $h(x)$ 在某个目标[概率分布](@entry_id:146404) $p(x)$ 下的[期望值](@entry_id:153208) $I = \mathbb{E}_p[h(X)]$。然而，在实践中，我们常常面临一个棘手的挑战：目标[概率密度函数](@entry_id:140610) $p(x)$ 仅在相差一个[归一化常数](@entry_id:752675)的意义下是已知的。本章将深入探讨为应对这一挑战而设计的核心方法——[自归一化](@entry_id:636594)重要性抽样 (Self-Normalized Importance Sampling, SNIS) 的原理与机制。

### 未归一化[分布](@entry_id:182848)的挑战

在许多实际问题中，目标[概率密度函数](@entry_id:140610) $p(x)$ 的精确形式是未知的。我们只知道它正比于一个已知的、非负的函数 $\tilde{p}(x)$，即 $p(x) = \tilde{p}(x) / Z$。这里的 $Z = \int \tilde{p}(x) dx$ 是一个归一化常数，它的计算本身可能极其困难，甚至比计算我们最初感兴趣的期望 $I$ 还要困难。例如，在贝叶斯统计中，后验分布通常是似然函数与先验分布的乘积，其归一化常数（即证据或[边际似然](@entry_id:636856)）的计算是一个核心难题。在[计算核物理](@entry_id:747629)中，中子能量的稳态分布也可能只知道其与某些物理过程[截面](@entry_id:154995)相关的未归一化形式 。

这种未知归一化常数 $Z$ 的存在，使得标准[蒙特卡洛方法](@entry_id:136978)失效。首先，我们无法直接从 $p(x)$ 中抽样，因为生成随机数的算法通常需要知道密度的精确形式。其次，即使我们转而使用标准的重要性抽样 (Importance Sampling, IS)，也会遇到障碍。标准重要性抽样的核心是引入一个我们能够抽样的**[提议分布](@entry_id:144814)** (proposal distribution) $q(x)$，并通过权重 $w(x) = p(x)/q(x)$ 来修正期望的计算。其估计量为：
$$
\hat{I}_{\mathrm{IS}} = \frac{1}{N} \sum_{i=1}^{N} \frac{p(X_i)}{q(X_i)} h(X_i), \quad X_i \sim q(x)
$$
然而，权重的计算需要 $p(x)$ 的精确值。当我们只知道 $p(x) \propto \tilde{p}(x)$ 时，权重变为 $w(x) = \frac{\tilde{p}(x)}{Z q(x)}$，其中包含了未知的 $Z$。因此，$\hat{I}_{\mathrm{IS}}$ 无法被直接计算。在某些情况下，甚至提议分布本身也可能仅被指定到相差一个常数，即 $q(x) = \tilde{q}(x)/Z_q$，其中 $Z_q$ 未知。此时，真实的权重 $w(x) = \frac{Z_q}{Z_p} \frac{\tilde{p}(x)}{\tilde{q}(x)}$ 涉及两个未知常数的比率，标准的重要性[抽样方法](@entry_id:141232)彻底失效 。

为了克服这一根本性困难，我们需要一种能够在只知道 $\tilde{p}(x)$ 和 $\tilde{q}(x)$ 的情况下估计 $I$ 的方法。[自归一化](@entry_id:636594)重要性抽样应运而生。

### [自归一化](@entry_id:636594)原理

[自归一化](@entry_id:636594)重要性抽样的巧妙之处在于将目标期望 $I$ 表示为一个比率，从而在计算中消除未知的[归一化常数](@entry_id:752675)。其推导过程基于以下基本思想：

首先，我们将期望 $I$ 的定义式展开，并用未归一化的密度 $\tilde{p}(x)$ 和未知的常数 $Z$ 来表示：
$$
I = \mathbb{E}_p[h(X)] = \int h(x) p(x) dx = \int h(x) \frac{\tilde{p}(x)}{Z} dx = \frac{\int h(x) \tilde{p}(x) dx}{\int \tilde{p}(x) dx}
$$
这个简单的代数变换是核心。它将 $I$ 表示为两个积分的比值。分子是函数 $h(x)\tilde{p}(x)$ 的积分，分母则是 $\tilde{p}(x)$ 自身的积分（即[归一化常数](@entry_id:752675) $Z$）。现在，我们的任务从计算一个期望转变为估计这两个积分的比值。

接下来，我们对分子和分母的积分分别使用重要性抽样。引入一个我们能够从中抽样的[提议分布](@entry_id:144814) $q(x)$，我们将分子和分母都改写为在 $q(x)$ [分布](@entry_id:182848)下的期望：
$$
\text{分子} = \int h(x) \tilde{p}(x) dx = \int h(x) \frac{\tilde{p}(x)}{q(x)} q(x) dx = \mathbb{E}_q\left[ h(X) \frac{\tilde{p}(X)}{q(X)} \right]
$$
$$
\text{分母} = \int \tilde{p}(x) dx = \int \frac{\tilde{p}(x)}{q(x)} q(x) dx = \mathbb{E}_q\left[ \frac{\tilde{p}(X)}{q(X)} \right]
$$
在这里，我们定义一个可计算的**未归一化权重** (unnormalized weight)，它只依赖于已知的函数 $\tilde{p}(x)$ 和 $q(x)$：
$$
\tilde{w}(x) = \frac{\tilde{p}(x)}{q(x)}
$$
于是，目标期望 $I$ 可以精确地表示为两个在 $q$ [分布](@entry_id:182848)下的期望的比值：
$$
I = \frac{\mathbb{E}_q[h(X) \tilde{w}(X)]}{\mathbb{E}_q[\tilde{w}(X)]}
$$
注意到，即使提议分布本身也是未归一化的，例如 $q(x) = \tilde{q}(x)/Z_q$，那么未归一化权重就变成 $\tilde{w}(x) = \tilde{p}(x)/\tilde{q}(x)$。在这种情况下，$I$ 的表达式变为：
$$
I = \frac{\mathbb{E}_q[h(X) (\tilde{p}(X)/\tilde{q}(X))]}{\mathbb{E}_q[\tilde{p}(X)/\tilde{q}(X)]} = \frac{\int h(x) (\tilde{p}(x)/\tilde{q}(x)) (\tilde{q}(x)/Z_q) dx}{\int (\tilde{p}(x)/\tilde{q}(x)) (\tilde{q}(x)/Z_q) dx} = \frac{(1/Z_q)\int h(x)\tilde{p}(x)dx}{(1/Z_q)\int \tilde{p}(x)dx}
$$
未知的常数 $Z_q$ 在分子和分母中同时出现并被约掉 。这揭示了[自归一化](@entry_id:636594)方法的一个强大特性。

最后，根据大数定律，我们可以使用从 $q(x)$ 抽取的 $N$ 个独立同分布样本 $\{X_1, \dots, X_N\}$ 来估计分子和分母的期望。我们计算每个样本的未归一化权重 $\tilde{w}_i = \tilde{w}(X_i)$。
分子期望的[蒙特卡洛估计](@entry_id:637986)为 $\frac{1}{N}\sum_{i=1}^{N} h(X_i) \tilde{w}_i$。
分母期望的[蒙特卡洛估计](@entry_id:637986)为 $\frac{1}{N}\sum_{i=1}^{N} \tilde{w}_i$。

将这两个估计量相除，常数 $1/N$ 被约掉，我们便得到了**[自归一化](@entry_id:636594)重要性抽样 (SNIS) 估计量** $\hat{I}_{\mathrm{SNIS}}$：
$$
\hat{I}_{\mathrm{SNIS}} = \frac{\sum_{i=1}^{N} h(X_i) \tilde{w}_i}{\sum_{j=1}^{N} \tilde{w}_j}
$$
这个估计量也可以写成加权平均的形式：$\hat{I}_{\mathrm{SNIS}} = \sum_{i=1}^{N} \bar{w}_i h(X_i)$，其中 $\bar{w}_i = \frac{\tilde{w}_i}{\sum_{j=1}^{N} \tilde{w}_j}$ 是**归一化权重** (normalized weights)。顾名思义，这些权重之和为1，即 $\sum_{i=1}^{N} \bar{w}_i = 1$。这种结构使得 SNIS 估计量对未归一化权重的任意缩放都是不变的。如果我们用 $c\tilde{w}_i$ (其中 $c>0$ 为常数) 替换 $\tilde{w}_i$，归一化权重 $\bar{w}_i$ 和最终的估计值 $\hat{I}_{\mathrm{SNIS}}$ 均保持不变  。这正是该方法在只知道函数比例形式时依然定义良好的根本原因。

**示例**
让我们通过一个具体的例子来理解这个过程 。假设目标分布的未归一化密度为 $\tilde{p}(x) = \exp(-x^4/2)$，我们希望估计 $h(x)=x^2$ 的期望。我们选择标准正态分布 $\mathcal{N}(0,1)$ 作为[提议分布](@entry_id:144814)，其密度为 $q(x) = \frac{1}{\sqrt{2\pi}}\exp(-x^2/2)$。
首先，计算未归一化权重函数：
$$
\tilde{w}(x) = \frac{\tilde{p}(x)}{q(x)} = \frac{\exp(-x^4/2)}{\frac{1}{\sqrt{2\pi}}\exp(-x^2/2)} = \sqrt{2\pi} \exp\left(\frac{1}{2}x^2 - \frac{1}{2}x^4\right)
$$
假设我们从 $q(x)$ 中抽取了样本 $X_1, \dots, X_n$。SNIS 估计量为：
$$
\hat{I}_{\mathrm{SNIS}} = \frac{\sum_{i=1}^{n} h(X_i) \tilde{w}(X_i)}{\sum_{j=1}^{n} \tilde{w}(X_j)} = \frac{\sum_{i=1}^{n} X_i^2 \left[ \sqrt{2\pi} \exp\left(\frac{1}{2}X_i^2 - \frac{1}{2}X_i^4\right) \right]}{\sum_{j=1}^{n} \left[ \sqrt{2\pi} \exp\left(\frac{1}{2}X_j^2 - \frac{1}{2}X_j^4\right) \right]}
$$
由于常数 $\sqrt{2\pi}$ 出现在分子和分母的每一项中，它可以被完全约去。最终的估计量为：
$$
\hat{I}_{\mathrm{SNIS}} = \frac{\sum_{i=1}^{n} X_i^2 \exp\left(\frac{1}{2}X_i^2 - \frac{1}{2}X_i^4\right)}{\sum_{j=1}^{n} \exp\left(\frac{1}{2}X_j^2 - \frac{1}{2}X_j^4\right)}
$$
这个表达式只依赖于样本 $X_i$ 和已知的函数形式，完全不依赖于任何未知的[归一化常数](@entry_id:752675)，展示了[自归一化](@entry_id:636594)机制的威力。

### [SNIS估计量](@entry_id:754991)的统计特性

虽然 SNIS 估计量巧妙地解决了归一化常数未知的问题，但其比率结构也引入了与标准 IS 估计量不同的统计特性。理解这些特性对于正确使用和评估该方法至关重要。

#### 偏差与相合性

一个估计量的理想属性是**无偏性** (unbiasedness)，即其[期望值](@entry_id:153208)等于我们想要估计的真实值。对于标准 IS 估计量（假设 $Z$ 已知），这是成立的：
$$
\mathbb{E}_q[\hat{I}_{\mathrm{IS}}] = \mathbb{E}_q\left[\frac{1}{N}\sum_{i=1}^{N} w(X_i) h(X_i)\right] = \mathbb{E}_q[w(X)h(X)] = \mathbb{E}_p[h(X)] = I
$$
然而，SNIS 估计量 $\hat{I}_{\mathrm{SNIS}}$ 是两个[随机变量](@entry_id:195330)（分子和分母的样本均值）的比值。一般而言，**比率的期望不等于期望的比率**，即 $\mathbb{E}[\hat{A}/\hat{B}] \neq \mathbb{E}[\hat{A}]/\mathbb{E}[\hat{B}]$。因此，对于有限的样本量 $N$，SNIS 估计量通常是**有偏的** (biased)   。
$$
\mathbb{E}_q[\hat{I}_{\mathrm{SNIS}}] = \mathbb{E}_q\left[ \frac{\sum \tilde{w}_i h(X_i)}{\sum \tilde{w}_j} \right] \neq \frac{\mathbb{E}_q[\sum \tilde{w}_i h(X_i)]}{\mathbb{E}_q[\sum \tilde{w}_j]} = \frac{N \cdot Z \cdot I}{N \cdot Z} = I
$$
尽管有偏，但 SNIS 估计量拥有另一个重要的优良性质：**相合性** (consistency)。只要满足适当的[矩条件](@entry_id:136365)（例如 $\mathbb{E}_q[|\tilde{w}(X)|]  \infty$ 和 $\mathbb{E}_q[|\tilde{w}(X)h(X)|]  \infty$），根据[大数定律](@entry_id:140915)，当样本量 $N \to \infty$ 时，分子和分母的样本均值会分别收敛到它们的真实期望。因此，它们的比率会收敛到期望的比率  ：
$$
\hat{I}_{\mathrm{SNIS}} = \frac{\frac{1}{N}\sum \tilde{w}_i h(X_i)}{\frac{1}{N}\sum \tilde{w}_j} \xrightarrow{N \to \infty} \frac{\mathbb{E}_q[\tilde{w}(X)h(X)]}{\mathbb{E}_q[\tilde{w}(X)]} = \frac{Z \cdot I}{Z} = I
$$
这意味着只要样本量足够大，SNIS 估计量就会任意接近真实值 $I$。

对于这个有限样本偏差，我们可以通过泰勒展开（即[Delta方法](@entry_id:276272)）进行更深入的分析。可以证明，在适当的[矩条件](@entry_id:136365)下，偏差的大小与 $N^{-1}$ 成正比，即 $\mathbb{E}[\hat{I}_{\mathrm{SNIS}}] - I = O(1/N)$。偏差的[主导项](@entry_id:167418)可以表示为  ：
$$
\text{Bias}_n \approx \frac{1}{n} \left( I \cdot \mathrm{Var}_q(\tilde{w}(X)/Z) - \mathrm{Cov}_q(\tilde{w}(X)h(X)/Z, \tilde{w}(X)/Z) \right) = \frac{1}{n} \mathbb{E}_q[w(X)^2 (I - h(X))]
$$
其中 $w(x) = \tilde{w}(x)/Z$ 是真实的（但不可计算的）权重。这个结果表明，偏差随着样本量的增加而减小，并且其符号和大小取决于真实值 $I$ 与函数值 $h(X)$ 之间的加权协[方差](@entry_id:200758)。

#### [渐近方差](@entry_id:269933)

估计量的另一个关键性能指标是其**[方差](@entry_id:200758)** (variance)，它衡量了估计值围绕其均值的波动程度。同样，通过应用多元中心极限定理和[Delta方法](@entry_id:276272)，我们可以推导出 SNIS 估计量的**[渐近方差](@entry_id:269933)** (asymptotic variance) 。

结果表明，当 $N$ 很大时，$\hat{I}_{\mathrm{SNIS}}$ 的[分布](@entry_id:182848)近似为正态分布，其[方差](@entry_id:200758)为：
$$
\mathrm{Var}(\hat{I}_{\mathrm{SNIS}}) \approx \frac{1}{N} \mathrm{Var}_q(w(X)(h(X)-I))
$$
其中 $w(x)=p(x)/q(x)$ 是真实权重。由于 $\mathbb{E}_q[w(X)(h(X)-I)] = \mathbb{E}_p[h(X)-I] = I-I = 0$，[方差](@entry_id:200758)可以简化为二阶矩：
$$
\mathrm{Var}(\hat{I}_{\mathrm{SNIS}}) \approx \frac{1}{N} \mathbb{E}_q[w(X)^2 (h(X) - I)^2]
$$
这个重要的公式揭示了 SNIS [估计量方差](@entry_id:263211)的来源。它取决于真实权重 $w(X)$ 的平方以及函数 $h(X)$ 相对于其真实均值 $I$ 的加权平方偏差。如果权重 $w(X)$ 的波动很大（即 $q(x)$ 与 $p(x)$ 差异很大），或者 $h(X)$ 的值在重要区域（$w(X)$ 大的区域）远离其均值 $I$，那么[方差](@entry_id:200758)就会很大。

#### 理想情况：提议分布与[目标分布](@entry_id:634522)一致

为了更好地理解这些性质，我们可以考虑一个理想化的基准情况：如果我们能够直接从目标分布 $p(x)$ 中抽样，即选择[提议分布](@entry_id:144814) $q(x)=p(x)$  。
在这种情况下，真实权重 $w(x) = p(x)/p(x) = 1$。
标准 IS 估计量变为：
$$
\hat{I}_{\mathrm{IS}} = \frac{1}{N} \sum_{i=1}^{N} 1 \cdot h(X_i) = \frac{1}{N} \sum_{i=1}^{N} h(X_i), \quad X_i \sim p(x)
$$
这正是标准的[蒙特卡洛估计](@entry_id:637986)量。
对于 SNIS 估计量，未归一化权重为 $\tilde{w}(x) = \tilde{p}(x)/p(x) = Z$。所有权重都是常数 $Z$。
$$
\hat{I}_{\mathrm{SNIS}} = \frac{\sum_{i=1}^{N} Z \cdot h(X_i)}{\sum_{j=1}^{N} Z} = \frac{Z \sum h(X_i)}{N \cdot Z} = \frac{1}{N} \sum_{i=1}^{N} h(X_i), \quad X_i \sim p(x)
$$
两种估计量都退化为标准的样本均值。此时，由于样本直接来自 $p(x)$，估计量是**精确无偏**的，并且其偏差为零。这个特例不仅是一个有用的健全性检查，也为我们提供了一个目标：一个好的[提议分布](@entry_id:144814) $q(x)$ 应该尽可能地接近[目标分布](@entry_id:634522) $p(x)$，以减小权重[方差](@entry_id:200758)，从而降低[估计量的偏差](@entry_id:168594)和[方差](@entry_id:200758)。

### 估计量可靠性的实践诊断

SNIS 估计量的统计特性，特别是其[方差](@entry_id:200758)，严重依赖于提议分布 $q(x)$ 的选择。一个糟糕的 $q(x)$ 会导致权重[分布](@entry_id:182848)出现极端的变异性，使得少数几个样本的权重远大于其他样本，从而支配整个估计。这会导致估计量非常不稳定且不可靠。因此，在实践中，对权重[分布](@entry_id:182848)进行诊断至关重要。

#### [有效样本量](@entry_id:271661)

一个直观的诊断工具是**[有效样本量](@entry_id:271661)** (Effective Sample Size, ESS)，记作 $N_{\mathrm{eff}}$。其思想是量化在重要性抽样中，由于权重不均所造成的等效样本损失。$N_{\mathrm{eff}}$ 被定义为需要从目标分布 $p(x)$ 中直接抽取多少个[独立样本](@entry_id:177139)，才能获得与我们当前 SNIS 估计量相当的[方差](@entry_id:200758)。

一种常用的 $N_{\mathrm{eff}}$ 推导方法是基于一个启发式模型，它将 SNIS [估计量的方差](@entry_id:167223)近似为 $\mathrm{Var}(\hat{I}_{\mathrm{SN}}) \approx (\sum \bar{w}_i^2) \sigma_p^2$，而标准[蒙特卡洛估计](@entry_id:637986)量的[方差](@entry_id:200758)为 $\sigma_p^2 / N_{\mathrm{eff}}$，其中 $\sigma_p^2 = \mathrm{Var}_p(h(X))$。通过令这两个[方差](@entry_id:200758)相等，我们可以解出 $N_{\mathrm{eff}}$ ：
$$
\frac{\sigma_p^2}{N_{\mathrm{eff}}} = \left(\sum_{i=1}^{N} \bar{w}_i^2\right) \sigma_p^2 \implies N_{\mathrm{eff}} = \frac{1}{\sum_{i=1}^{N} \bar{w}_i^2}
$$
用未归一化的权重 $\tilde{w}_i$ 表示，这个公式变为：
$$
N_{\mathrm{eff}} = \frac{(\sum_{i=1}^{N} \tilde{w}_i)^2}{\sum_{i=1}^{N} \tilde{w}_i^2}
$$
$N_{\mathrm{eff}}$ 的取值范围是 $1 \le N_{\mathrm{eff}} \le N$。如果所有权重都相等，$\bar{w}_i = 1/N$，那么 $N_{\mathrm{eff}} = N$，表示没有效率损失。如果权重高度集中在一个样本上，$\bar{w}_k \approx 1$ 而其他 $\bar{w}_{i \ne k} \approx 0$，那么 $N_{\mathrm{eff}} \approx 1$，表示估计几乎完全由一个样本决定，非常不可靠。在实践中，通常将 $\mathrm{ESS}/N$ 的比率作为诊断指标，如果该比率过低（例如低于0.1），则提示重要性抽样的效率很低。

#### 权重[分布](@entry_id:182848)与尾部行为

[有效样本量](@entry_id:271661)提供了一个宏观的诊断，而更深入的分析则需要考察权重本身的[分布](@entry_id:182848)。权重 $\tilde{w}(X)$ 的[分布](@entry_id:182848)，特别是其尾部行为，直接决定了 SNIS 估计量的收敛性质。

一个有用的[启发式](@entry_id:261307)模型是假设权重的对数 $\log \tilde{w}(X)$ 近似服从高斯分布，即权重 $\tilde{w}(X)$ 近似服从[对数正态分布](@entry_id:261888) 。如果 $\mathrm{Var}_q(\log w(X)) = \sigma^2$（其中 $w(x)$ 是真实权重），可以证明，渐近地，归一化的[有效样本量](@entry_id:271661)满足：
$$
\frac{\mathrm{ESS}}{N} \approx \exp(-\sigma^2)
$$
这个关系清晰地表明，对数权重的[方差](@entry_id:200758)越大，[有效样本量](@entry_id:271661)的损失就越严重。我们可以设定一个效率阈值 $\tau \in (0,1)$，当 $\mathrm{ESS}/N  \tau$ 时认为权重发生“退化”。发生退化的最小[方差](@entry_id:200758)为 $\sigma^2_{\mathrm{deg}} = -\ln(\tau)$。

更根本的诊断来自于[极值理论](@entry_id:140083)。权重[分布](@entry_id:182848)的尾部行为决定了其矩的存在性。特别是，SNIS 估计量的[渐近方差](@entry_id:269933)是否有限，取决于真实权重二阶矩 $\mathbb{E}_q[w(X)^2]$ 是否有限。如果这个矩是无限的，那么[中心极限定理](@entry_id:143108)的标准形式将不适用，SNIS 估计量的[收敛速度](@entry_id:636873)会慢于标准的 $1/\sqrt{N}$，并且估计会极其不稳定。

**帕累托平滑重要性抽样 (Pareto-Smoothed Importance Sampling, PSIS)** 提供了一个强大的诊断工具来评估这个问题 。该方法通过将[广义帕累托分布](@entry_id:137241) (Generalized Pareto Distribution, GPD)拟合到权重[分布](@entry_id:182848)的上尾部（即最大的那些权重），并估计其**尾部形状参数** (tail shape parameter) $k$。根据[极值理论](@entry_id:140083)，权重[分布](@entry_id:182848)的 $m$ 阶矩是有限的，当且仅当 $k  1/m$。

这个结论为我们提供了关键的诊断准则：
- 如果 $k  0.5$：这意味着权重的二阶矩 $\mathbb{E}_q[w(X)^2]$ 是有限的。因此，SNIS 估计量的[渐近方差](@entry_id:269933)是有限的，[中心极限定理](@entry_id:143108)成立，估计量是可靠的。
- 如果 $k > 0.5$：这意味着权重的二阶矩是**无限的**。这是极其危险的信号。它表明 SNIS [估计量的方差](@entry_id:167223)是无限的，其收敛行为不再良好。在实践中，这意味着估计值将对少数几个极端权重样本异常敏感，导致结果极度不可靠。因此，当 PSIS 诊断报告 $k > 0.5$（特别是大于0.7）时，我们必须对 SNIS 的结果保持高度警惕，这通常意味着提议分布 $q(x)$ 对于目标 $p(x)$ 而言是一个非常糟糕的近似（通常是 $q(x)$ 的尾部比 $p(x)$ 的尾部更“轻”）。

总之，[自归一化](@entry_id:636594)重要性抽样是一种强大而必要的工具，用于处理在科学计算中普遍存在的未归一化[分布](@entry_id:182848)问题。然而，它的应用必须伴随着对其统计特性（尤其是有偏性）的理解和对权重[分布](@entry_id:182848)的仔细诊断，以确保最终得到的估计是可靠和稳定的。