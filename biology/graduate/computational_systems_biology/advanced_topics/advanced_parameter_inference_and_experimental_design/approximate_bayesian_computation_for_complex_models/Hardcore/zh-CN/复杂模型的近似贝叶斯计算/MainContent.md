## 引言
在探索复杂生物系统时，我们构建的机理模型往往伴随着一个难以处理或计算成本高昂的似然函数，这为传统的贝叶斯参数推断带来了巨大挑战。近似贝叶斯计算（Approximate Bayesian Computation, ABC）应运而生，它提供了一个强大的、不依赖于似然函数的模拟框架，使我们能够解锁对这些复杂模型的深刻洞见。本文旨在系统性地介绍ABC方法，解决在缺乏解析似然函数的情况下如何进行有效贝叶斯推断这一核心问题。

通过本文的学习，您将深入了解ABC的完整图景。在“原理与机制”一章中，我们将剖析ABC如何通过摘要统计量和容忍度来巧妙地近似后验分布，并探讨其内在的偏差-方差权衡。接着，在“应用与跨学科联系”一章中，我们将展示ABC在系统生物学（如建模细胞异质性）和进化生物学等前沿领域的强大应用，并讨论应对大规模计算的优化策略。最后，“动手实践”部分将通过具体的计算问题，让您亲身体验分层建模、效率优化等高级ABC概念。

让我们从ABC的核心原理开始，逐步揭开这个强大推断工具的神秘面纱。

## 原理与机制

在对复杂生物系统进行建模时，我们经常遇到似然函数难以处理或计算成本过高的情况。在这种情况下，近似贝叶斯计算（Approximate Bayesian Computation, ABC）提供了一个强大的、不依赖于似然函数的推断框架。本章旨在深入探讨驱动ABC方法的核心原理和内在机制，阐明其近似的性质、关键组成部分的选择以及其中固有的权衡。

### 核心机制：对似然函数的近似

ABC的根本思想是用一个基于模拟的接受/拒绝准则来替代对难以处理的似然函数 $p(\text{data}|\boldsymbol{\theta})$ 的直接评估。其最基本的形式，即**拒绝ABC**（rejection ABC），遵循一个简单直观的算法：从参数 $\boldsymbol{\theta}$ 的先验分布 $\pi(\boldsymbol{\theta})$ 中抽取一个样本，利用这个 $\boldsymbol{\theta}$ 从模型中模拟一个合成数据集 $\text{data}'$，然后比较合成数据与观测数据。如果两者足够“接近”，就接受这个 $\boldsymbol{\theta}$ 作为后验分布的一个样本；否则，就拒绝它。

在实践中，直接比较高维的原始数据集（如单细胞轨迹或基因组序列）既困难又计算效率低下。因此，我们将数据压缩成一组低维的**摘要统计量**（summary statistics），用 $\mathbf{s}(\text{data})$ 表示。比较随即在摘要统计量的空间中进行。算法接受一个参数提议 $\boldsymbol{\theta}$，条件是模拟摘要统计量 $\mathbf{s}_{\text{sim}}$ 与观测摘要统计量 $\mathbf{s}_{\text{obs}}$ 之间的距离小于某个预设的**容忍度**（tolerance） $\epsilon$：

$$
\rho(\mathbf{s}_{\text{sim}}, \mathbf{s}_{\text{obs}}) \le \epsilon
$$

这里，$\rho$ 是一个距离度量函数，例如欧氏距离。

这种方法的一个更平滑的变体是**核加权ABC**（kernel-weighted ABC）。它不采用硬性的接受/拒绝边界，而是根据 $\mathbf{s}_{\text{sim}}$ 与 $\mathbf{s}_{\text{obs}}$ 的接近程度，为每个参数提议 $\boldsymbol{\theta}$ 分配一个权重。这个权重由一个**接受核**（acceptance kernel）$K_{\epsilon}$ 决定，其带宽（bandwidth）由容忍度 $\epsilon$ 控制。通常，核函数是一个以零为中心、随着距离增加而递减的函数，例如高斯核。

### ABC似然及其解释

为了更深刻地理解ABC的近似性质，我们可以构建一个**有效ABC似然**（effective ABC likelihood）的概念。ABC算法实际上是在从一个近似后验分布 $\pi_{\text{ABC}}(\boldsymbol{\theta}|\mathbf{s}_{\text{obs}})$ 中采样，该分布正比于先验与有效ABC似然的乘积：

$$
\pi_{\text{ABC}}(\boldsymbol{\theta}|\mathbf{s}_{\text{obs}}) \propto \pi(\boldsymbol{\theta}) L_{\text{ABC}}(\mathbf{s}_{\text{obs}}|\boldsymbol{\theta})
$$

这个有效似然 $L_{\text{ABC}}(\mathbf{s}_{\text{obs}}|\boldsymbol{\theta})$ 定义为，在给定参数 $\boldsymbol{\theta}$ 的条件下，对模拟摘要统计量 $p(\mathbf{s}|\boldsymbol{\theta})$ 的分布，计算接受核的期望值：

$$
L_{\text{ABC}}(\mathbf{s}_{\text{obs}}|\boldsymbol{\theta}) = \mathbb{E}_{\mathbf{s} \sim p(\mathbf{s}|\boldsymbol{\theta})} [K_{\epsilon}(\mathbf{s} - \mathbf{s}_{\text{obs}})] = \int p(\mathbf{s}|\boldsymbol{\theta}) K_{\epsilon}(\mathbf{s} - \mathbf{s}_{\text{obs}}) d\mathbf{s}
$$

这个表达式揭示了ABC的核心机制：它将真实的（但难以处理的）摘要统计量似然 $p(\mathbf{s}|\boldsymbol{\theta})$ 与接受核 $K_{\epsilon}$ 进行了卷积。这种卷积操作有效地平滑了真实似然，平滑的程度由容忍度 $\epsilon$ 控制。

我们可以通过一个具体的例子来阐明这一点 [@problem_id:3288572]。考虑一个随机基因表达模型，其摘要统计量 $S$（例如，对数mRNA丰度）在给定参数 $\theta$（例如，对数转录率）的条件下服从高斯分布，即 $S|\theta \sim \mathcal{N}(\theta, \sigma^2)$。如果我们采用一个高斯接受核 $K_{\epsilon}(u)$，它本身是 $\mathcal{N}(0, \epsilon^2)$ 分布的概率密度函数，那么有效ABC似然就是两个高斯分布的卷积。

两个独立高斯随机变量之和仍然是高斯分布，其均值为各自均值之和，方差为各自方差之和。因此，这个卷积的结果是一个新的高斯分布的概率密度函数。有效ABC似然 $L_{\text{ABC}}(s_{\text{obs}}|\theta)$ 对应于一个有效模型中的似然，其中观测值 $s_{\text{obs}}$ 服从以 $\theta$ 为均值、方差为 $\sigma^2 + \epsilon^2$ 的高斯分布：

$$
s_{\text{obs}} | \theta \sim \mathcal{N}(\theta, \sigma^2 + \epsilon^2)
$$

这个结果提供了一个极其深刻的见解：使用高斯核的ABC等价于在一个被扰动过的模型上进行**精确的贝叶斯推断**。这里的扰动表现为观测摘要统计量中增加了一个额外的噪声项，其方差由核的带宽 $\epsilon^2$ 决定。因此，容忍度 $\epsilon$ 不仅仅是一个算法参数，它直接量化了我们引入的近似误差的尺度。当 $\epsilon \to 0$ 时，ABC后验收敛于以 $s_{\text{obs}}$ 为条件的真实后验；而当 $\epsilon$ 增大时，后验分布会变得更宽，反映了更大的不确定性。

### 衡量差异：距离度量与容忍度设定

在多维摘要统计量的场景中，选择合适的距离度量 $\rho$ 至关重要。简单的欧氏距离可能不是最优选择，因为它同等对待所有摘要统计量，忽略了它们的尺度差异和相互之间的相关性。

一个更具统计学原理的选择是**马氏距离**（Mahalanobis distance）。它通过摘要统计量的协方差矩阵 $\boldsymbol{\Sigma}$ 对数据进行标准化和去相关，其定义如下：

$$
D(\mathbf{s}_{\text{sim}}, \mathbf{s}_{\text{obs}}) = \sqrt{(\mathbf{s}_{\text{sim}} - \mathbf{s}_{\text{obs}})^{\top} \boldsymbol{\Sigma}^{-1} (\mathbf{s}_{\text{sim}} - \mathbf{s}_{\text{obs}})}
$$

其中，协方差矩阵 $\boldsymbol{\Sigma}$ 通常通过初步的模拟运行来估计。使用马氏距离等同于在一个变换过的空间中计算欧氏距离，在这个空间里，摘要统计量的各个维度是独立的，并且方差为1。

马氏距离的平方具有一个非常有用的统计特性 [@problem_id:3288579]。如果摘要统计量 $\mathbf{s}_{\text{sim}}$ 的分布在真实参数 $\boldsymbol{\theta}_0$ 附近可以由一个多元高斯分布 $\mathcal{N}(\mathbf{s}_{\text{obs}}, \boldsymbol{\Sigma})$ 来近似，那么其平方马氏距离 $D^2$ 将服从一个**卡方分布**（chi-squared distribution），其自由度 $d$ 等于摘要统计量向量的维数，即 $D^2 \sim \chi^2(d)$。

这一特性为设定容忍度阈值 $\tau$ 提供了一个非任意的、有原则的依据。我们可以不再盲目地选择 $\tau$，而是将其设定为 $\chi^2(d)$ 分布的某个分位数，以达到预期的**接受率**（acceptance rate） $\alpha$。例如，如果我们希望在真实参数值附近的接受率大约为 $20\%$（即 $\alpha = 0.2$），我们可以将阈值 $\tau$ 设定为 $\chi^2(d)$ 分布的第 $20$ 百分位数。具体来说，接受概率 $\mathbb{P}(D^2 \le \tau)$ 就是 $\chi^2(d)$ 分布在 $\tau$ 处的累积分布函数（CDF）值。对于 $d=2$ 的情况，$\chi^2(2)$ 分布恰好是一个指数分布，其CDF为 $1 - \exp(-\tau/2)$。设定 $1 - \exp(-\tau/2) = 0.2$，就可以解出相应的 $\tau$ 值 [@problem_id:3288579]。这种方法使得容忍度的选择更加透明和可重复。

### 摘要统计量的作用：信息与可识别性

在ABC中，最关键的设计选择之一是摘要统计量的选取。理想情况下，摘要统计量应当是模型参数的**充分统计量**（sufficient statistics），这意味着它们包含了数据中关于参数的所有信息。然而，对于复杂的系统生物学模型，找到充分统计量几乎是不可能的。因此，我们的目标是选择一组能够最大程度地捕获参数信息的“近似充分”的统计量。

摘要统计量的选择直接关系到参数的**可识别性**（identifiability）。如果两个不同的参数组合 $\boldsymbol{\theta}_1$ 和 $\boldsymbol{\theta}_2$ 产生了相同的摘要统计量向量，即 $\mathbf{s}(\boldsymbol{\theta}_1) = \mathbf{s}(\boldsymbol{\theta}_2)$，那么这两个参数组合就无法通过这些摘要统计量来区分。

我们可以通过分析摘要统计量函数 $\mathbf{s}(\boldsymbol{\theta})$ 的局部灵敏度来评估参数的局部可识别性。这种灵敏度由**雅可比矩阵**（Jacobian matrix）$J$ 来量化，其元素是摘要统计量对各个参数的偏导数 $J_{ij} = \partial s_i / \partial \theta_j$。雅可比矩阵的列向量张成了一个局部线性空间，描述了当参数发生微小变化时，摘要统计量向量会如何移动。如果雅可比矩阵的列是线性相关的，就意味着至少有一个参数方向的变动不会引起摘要统计量的独立变化，从而导致参数的局部不可识别。

更进一步，我们可以将雅可比矩阵与摘要统计量的噪声水平（由协方差矩阵 $\boldsymbol{\Sigma}$ 描述）结合起来，以评估后验分布的精度 [@problem_id:3288623]。在ABC的小容忍度极限下，近似后验分布在最大后验估计点附近可以用一个高斯分布来近似。这个高斯分布的**精度矩阵**（precision matrix），即协方差矩阵的逆，可以表示为：

$$
\mathbf{P} \approx \mathbf{J}^{\top} \boldsymbol{\Sigma}^{-1} \mathbf{J}
$$

这个矩阵在统计学中也被称为**费雪信息矩阵**（Fisher Information Matrix）。它综合了两个关键因素：摘要统计量对参数的灵敏度（由 $\mathbf{J}$ 捕获）和摘要统计量本身的精度（由 $\boldsymbol{\Sigma}^{-1}$ 捕获）。一个“信息丰富”的摘要统计量应该对参数变化敏感（$\mathbf{J}$ 的元素较大），并且自身噪声较低（$\boldsymbol{\Sigma}$ 的元素较小）。

该精度矩阵的[行列式](@entry_id:142978) $\det(\mathbf{P})$ 是一个标量，它与后验分布体积的倒数成正比，因此可以作为参数整体可识别性的一个量化指标。正如在对一个随机基因表达模型的分析中所见 [@problem_id:3288623]，通过计算 $\det(\mathbf{P}) = (\det(\mathbf{J}))^2 \det(\boldsymbol{\Sigma}^{-1})$，我们可以定量地评估一组给定的摘要统计量（如稳态均值和自相关）对于推断模型参数（如生产速率 $k$ 和降解速率 $d$）提供了多少信息。一个更大的行列式值意味着后验分布更集中，参数估计更精确。

### 内在的权衡：偏差、方差与计算成本

ABC方法的实践充满了必须仔细平衡的权衡。其中最核心的权衡是在**偏差**（bias）和**方差**（variance）之间，而这个权衡由容忍度 $\epsilon$ 直接控制。

-   **较大的 $\epsilon$**：接受区域很大，导致接受率很高。在固定的总模拟次数（即计算预算）下，我们可以获得大量的后验样本。这使得对后验特征（如均值或分位数）的估计具有较低的**方差**。然而，由于接受了许多与观测数据差异较大的模拟，ABC后验分布 $\pi_{\text{ABC}}$ 会严重偏离真实的后验分布 $\pi(\boldsymbol{\theta}|\mathbf{s}_{\text{obs}})$，从而引入了巨大的**偏差**。

-   **较小的 $\epsilon$**：接受区域很小，ABC后验与真实后验非常接近，因此**偏差**很小。然而，这会导致极低的接受率。对于给定的计算预算，我们只能得到很少的后验样本，从而导致后验估计的**方差**非常高。这个问题会随着摘要统计量维数 $d$ 的增加而急剧恶化，因为高维空间中一个小球的体积会以 $\epsilon^d$ 的速度缩小，这就是所谓的**维度灾难**（curse of dimensionality）。

我们可以通过分析某个后验估计量（例如参数 $\phi(\boldsymbol{\theta})$ 的后验均值）的**均方误差**（Mean Squared Error, MSE）来形式化这一权衡 [@problem_id:3288593]。MSE 是偏差平方和方差的总和，$\text{MSE} = (\text{bias})^2 + \text{variance}$。在ABC的渐近理论中，对于小的 $\epsilon$，MSE可以近似地表示为：

$$
\operatorname{MSE}(\epsilon) \approx \beta\epsilon^{4} + \frac{\gamma}{N_{\text{acc}}}
$$

其中，$N_{\text{acc}}$ 是接受的样本数，$\beta$ 和 $\gamma$ 是依赖于模型和数据性质的常数。第一项 $\beta\epsilon^4$ 是由ABC近似引起的平方偏差，它随着 $\epsilon$ 的增大而增加。第二项是估计的方差，它与接受的样本数成反比。

考虑到接受率 $\alpha(\epsilon)$ 约等于 $k\epsilon^d$，则接受样本数 $N_{\text{acc}} = B \cdot \alpha(\epsilon) \approx B k \epsilon^d$，其中 $B$ 是总计算预算。代入MSE表达式，我们得到：

$$
\operatorname{MSE}(\epsilon) \approx \beta\epsilon^{4} + \frac{\gamma'}{B\epsilon^{d}}
$$

这个表达式清晰地揭示了 $\epsilon$ 的双重作用。为了最小化总误差，我们需要找到一个最优的 $\epsilon^*$ 来平衡这两个相互冲突的项。通过对上式关于 $\epsilon$ 求导并令其为零，我们可以解出最优容忍度 $\epsilon^*$ [@problem_id:3288593]：

$$
\epsilon^{*} = \left( \frac{d\gamma'}{4\beta B} \right)^{\frac{1}{d+4}}
$$

这个结果虽然依赖于一些未知的常数，但它提供了一个关于如何思考ABC调优的理论框架。它明确显示，最优容忍度依赖于摘要统计量的维数 $d$ 和可用的计算预算 $B$。例如，增加计算预算 $B$ 允许我们使用更小的 $\epsilon^*$，从而同时降低偏差和方差。这个问题也可以通过最大化**有效样本量**（Effective Sample Size, ESS）来表述，这在本质上是等价的，因为它与最小化MSE的目标一致。理解这些内在的权衡是成功应用ABC进行复杂模型推断的关键。