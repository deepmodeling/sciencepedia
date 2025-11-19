## 引言
在科学研究中，从实验数据中提取物理规律并量化其不确定性是一项核心挑战。卡方（χ²）最小化与[拟合优度检验](@entry_id:267868)是应对这一挑战的最基本也是最强大的统计方法之一，广泛应用于从粒子物理到天体物理，再到工程与社会科学的各个领域。然而，初学者常常只了解其最简形式，而对如何处理真实世界数据中的复杂情况，如[相关误差](@entry_id:268558)、系统不确定性以及理论假设的边界条件，缺乏系统性的认识。本文旨在填补这一知识鸿沟，为读者提供一个关于卡方方法的全面指南。

在接下来的内容中，我们将分三步深入探索。首先，在“原理与机制”一章中，我们将从最大似然原理出发，揭示卡方统计量的本质，并系统讲解参数估计、[拟合优度检验](@entry_id:267868)和不确定性评估的完整流程。接着，在“应用与跨学科联系”一章中，我们将通过高能物理及其他学科的丰富案例，展示该方法在解决实际问题中的灵活性与强大威力。最后，“动手实践”部分将提供具体的编程练习，帮助读者将理论知识转化为解决实际问题的能力，从而真正掌握这一关键的数据分析技术。

## 原理与机制

在对高能物理实验数据进行分析时，一个核心任务是将理论模型与观测数据进行比较，从而估计模型的自由参数并评估模型的有效性。$\chi^2$（卡方）最小化方法是实现这一目标的最基本、最强大的统计工具之一。本章将深入探讨$\chi^2$ 方法的原理与机制，从其统计基础出发，阐述参数估计和[拟合优度检验](@entry_id:267868)的实现，并讨论在实际分析中处理系统不确定性的高级技术。

### 从[最大似然](@entry_id:146147)到最小二乘法

$\chi^2$ 方法的理论基础源于统计学中的**[最大似然](@entry_id:146147)原理 (Principle of Maximum Likelihood)**。该原理指出，对于一组给定的观测数据，最优的模型参数是使这组数据出现的概率（即**似然 (Likelihood)**）达到最大的参数值。

考虑一个典型的测量场景：我们有 $N$ 个数据点（例如，一个能量谱的 $N$ 个区间），构成一个数据向量 $\mathbf{y} = (y_1, y_2, \dots, y_N)^T$。理论模型对这些数据点的[期望值](@entry_id:153208)作出预测，该预测依赖于一组参数 $\theta$，我们将其表示为向量 $\boldsymbol{\mu}(\theta) = (\mu_1(\theta), \mu_2(\theta), \dots, \mu_N(\theta))^T$。实验测量不可避免地伴随着随机涨落。在许多情况下，特别是当每个数据点的计数值很大时，根据中心极限定理，这些涨落可以很好地用**[多元正态分布](@entry_id:175229) (multivariate Gaussian distribution)** 来描述。

这种[分布](@entry_id:182848)由一个[均值向量](@entry_id:266544)（我们假设为理论预测 $\boldsymbol{\mu}(\theta)$）和一个 $N \times N$ 的**协方差矩阵 (covariance matrix)** $\mathbf{V}$ 共同定义。[协方差矩阵](@entry_id:139155)的对角元素 $V_{ii} = \sigma_i^2$ 表示第 $i$ 个数据点的[方差](@entry_id:200758)（即其不确定度的平方），而非对角元素 $V_{ij}$ 则表示第 $i$ 个和第 $j$ 个数据点测量值之间的协[方差](@entry_id:200758)，它量化了这两个测量值之间的相关性。

给定参数 $\theta$ 时观测到数据 $\mathbf{y}$ 的似然函数 $L(\mathbf{y} | \theta)$ 为：
$$
L(\mathbf{y} | \theta) = \frac{1}{\sqrt{(2\pi)^N \det(\mathbf{V})}} \exp\left( -\frac{1}{2} (\mathbf{y} - \boldsymbol{\mu}(\theta))^T \mathbf{V}^{-1} (\mathbf{y} - \boldsymbol{\mu}(\theta)) \right)
$$
其中 $\mathbf{V}^{-1}$ 是协方差矩阵的逆。[最大似然估计](@entry_id:142509)的目标是寻找参数值 $\hat{\theta}$ 来最大化 $L(\mathbf{y} | \theta)$。由于对数函数是单调递增的，最大化似然函数等价于最大化其对数，即**[对数似然](@entry_id:273783) (log-likelihood)** $\ln L$。为了方便，我们通常转而最小化**[负对数似然](@entry_id:637801) (negative log-likelihood)** $-\ln L$：
$$
-\ln L(\theta) = \frac{N}{2}\ln(2\pi) + \frac{1}{2}\ln(\det(\mathbf{V})) + \frac{1}{2} (\mathbf{y} - \boldsymbol{\mu}(\theta))^T \mathbf{V}^{-1} (\mathbf{y} - \boldsymbol{\mu}(\theta))
$$
在这个表达式中，前两项与模型参数 $\theta$ 无关，因此最小化 $-\ln L(\theta)$ 就等价于最小化最后一项。我们习惯上将 $\chi^2$ 函数定义为[负对数似然](@entry_id:637801)中依赖于参数部分的两倍 [@problem_id:3507390]：
$$
\chi^2(\theta) = (\mathbf{y} - \boldsymbol{\mu}(\theta))^T \mathbf{V}^{-1} (\mathbf{y} - \boldsymbol{\mu}(\theta))
$$
这就是最通用的 $\chi^2$ 定义，它适用于具有相关高斯误差的测量。这个表达式在几何上可以理解为数据向量 $\mathbf{y}$ 与模型预测向量 $\boldsymbol{\mu}(\theta)$ 之间由 $\mathbf{V}^{-1}$ 定义的“距离”的平方。因此，在高斯误差的假设下，**最大似然估计等价于最小二乘法 (least squares)**，而 $\chi^2$ 最小化正是[加权最小二乘法](@entry_id:177517)的一种形式。

### $\chi^2$ 统计量的形式与假设

根据具体问题的假设，通用的 $\chi^2$ 定义可以简化为几种常用形式。

#### 独立测量
当各个数据点 $y_i$ 的测量误差是相互独立的，但各自的不确定度 $\sigma_i$ 不同时，[协方差矩阵](@entry_id:139155) $\mathbf{V}$ 是一个[对角矩阵](@entry_id:637782)，其对角元素为 $V_{ii} = \sigma_i^2$。此时，其[逆矩阵](@entry_id:140380) $\mathbf{V}^{-1}$ 也是[对角矩阵](@entry_id:637782)，对角元素为 $1/\sigma_i^2$。代入通用公式后，$\chi^2$ 函数简化为我们熟悉的形式 [@problem_id:3507444]：
$$
\chi^2(\theta) = \sum_{i=1}^{N} \frac{(y_i - \mu_i(\theta))^2}{\sigma_i^2}
$$
这个形式表示残差 $(y_i - \mu_i(\theta))$ 的平方根据其[方差](@entry_id:200758) $\sigma_i^2$进行加权求和。不确定度小的测量点会对 $\chi^2$ 的总值贡献更大，因此在拟合中拥有更高的权重。

#### 区间计数的泊松数据
在高能物理中，许多测量本质上是事件计数，遵循**泊松分布 (Poisson distribution)**。对于一个[期望值](@entry_id:153208)为 $\mu$ 的泊松过程，其[方差](@entry_id:200758)也为 $\mu$。当[期望计数](@entry_id:162854)值较大时（例如大于 10-20），泊松分布可以很好地被均值和[方差](@entry_id:200758)均为 $\mu$ 的[高斯分布](@entry_id:154414)近似。在这种情况下，我们可以构造近似的 $\chi^2$ 统计量，但如何选择[方差](@entry_id:200758)是关键 [@problem_id:3507398]。

- **皮尔逊 (Pearson) $\chi^2$**：这种方法使用模型预测值 $f_i(\theta)$ 作为[方差](@entry_id:200758)的估计，即 $\sigma_i^2 \approx f_i(\theta)$。这源于在[高斯近似](@entry_id:636047)中将[方差](@entry_id:200758)设为[期望值](@entry_id:153208) $\mu_i$。统计量形式为：
  $$
  \chi^2_P(\theta) = \sum_{i=1}^{N} \frac{(y_i - f_i(\theta))^2}{f_i(\theta)}
  $$
  这种形式在理论上性质良好，因为它使用了模型本身的期望作为[方差](@entry_id:200758)，并且其最小化与最大化泊松[似然](@entry_id:167119)在渐近上是等价的。

- **奈曼 (Neyman) $\chi^2$**：这种方法使用观测到的计数值 $y_i$ 作为[方差](@entry_id:200758)的估计，即 $\sigma_i^2 \approx y_i$。统计量形式为：
  $$
  \chi^2_N(\theta) = \sum_{i=1}^{N} \frac{(y_i - f_i(\theta))^2}{y_i}
  $$
  奈曼 $\chi^2$ 的一个严重缺点是，当某个区间的观测计数值 $y_i$ 很小甚至为零时，其权重 $1/y_i$ 会变得极大或无定义，这会导致对低统计量区间的过度加权和拟合偏倚。因此，在实践中，皮尔遜 $\chi^2$ 或直接使用泊松似然函数（尤其是在低计数组合的情况下）是更受青睐的方法。

值得注意的是，如果分析中涉及[背景扣除](@entry_id:190391)，例如 $y_i = (\text{观测总数})_i - (\text{背景估计})_i$，那么 $y_i$ 可能为负或非整数，此时它不再遵循[泊松分布](@entry_id:147769)。在这种情况下，必须使用更复杂的[似然函数](@entry_id:141927)来正确建模，例如结合泊松和高斯的混合似然，而不能简单套用上述 $\chi^2$ 公式 [@problem_id:3507398]。

#### 相关的系统不确定性
在现代高能物理实验中，除了独立的[统计不确定性](@entry_id:267672)，还存在影响多个数据点的**系统不确定性 (systematic uncertainties)**。例如，[对撞机](@entry_id:192770)的束流强度（亮度）不确定性会以相同比例影响所有区间的产额。这类不确定性导致了[协方差矩阵](@entry_id:139155)中非对角元素的出现。一个常见的模型是将总[协方差矩阵](@entry_id:139155) $\mathbf{V}$ 表示为统计协[方差](@entry_id:200758)与系统协[方差](@entry_id:200758)之和：$\mathbf{V} = \mathbf{V}_{\text{stat}} + \mathbf{V}_{\text{syst}}$。

例如，一个与数据大小成比例的、完全相关的系统不确定性 $\delta$ 可以建模为 $\mathbf{V}_{\text{syst}, ij} = \delta^2 y_i y_j$。在这种情况下，总[协方差矩阵](@entry_id:139155)变为 $\mathbf{V} = \mathbf{D} + \delta^2 \mathbf{y} \mathbf{y}^T$，其中 $\mathbf{D}$ 是对角的统计[协方差矩阵](@entry_id:139155)。处理这种非[对角矩阵](@entry_id:637782)是执行精确拟合的关键 [@problem_id:3507368]。

### 通过 $\chi^2$ 最小化进行[参数估计](@entry_id:139349)

参数估计的目标是找到使 $\chi^2(\theta)$ 最小的参数值 $\hat{\theta}$。

#### [线性模型](@entry_id:178302)的解析解
当模型对参数 $\theta$ 是线性的，即 $\boldsymbol{\mu}(\theta) = \mathbf{A}\theta$，其中 $\mathbf{A}$ 是一个已知的 $N \times p$ [设计矩阵](@entry_id:165826)，$p$是参数个数，我们可以找到 $\hat{\theta}$ 的解析解。让我们以最简单的一维[线性模型](@entry_id:178302) $\boldsymbol{\mu}(a) = a\mathbf{t}$ 为例，其中 $a$ 是待求的标量参数，$\mathbf{t}$ 是一个已知的模板向量 [@problem_id:3507390]。$\chi^2$ 函数为：
$$
\chi^2(a) = (\mathbf{y} - a\mathbf{t})^T \mathbf{V}^{-1} (\mathbf{y} - a\mathbf{t}) = a^2(\mathbf{t}^T \mathbf{V}^{-1} \mathbf{t}) - 2a(\mathbf{t}^T \mathbf{V}^{-1} \mathbf{y}) + (\mathbf{y}^T \mathbf V^{-1} \mathbf{y})
$$
这是一个关于 $a$ 的二次函数。通过对其求导并令导数为零，$\frac{d\chi^2}{da} = 0$，我们可以解出最佳估计值 $\hat{a}$：
$$
\hat{a} = \frac{\mathbf{t}^T \mathbf{V}^{-1} \mathbf{y}}{\mathbf{t}^T \mathbf{V}^{-1} \mathbf{t}}
$$
这个优雅的公式是[广义最小二乘法](@entry_id:272590)的核心结果。在实际计算中，例如在处理如前所述的系统不确定性时，矩阵求逆可能是计算瓶颈。对于特定结构的协方差矩阵，如 $\mathbf{V} = \mathbf{D} + \mathbf{u}\mathbf{v}^T$，可以使用 Sherman-Morrison 公式等数值技巧来高效地计算其逆矩阵 [@problem_id:3507368]。

#### [非线性模型](@entry_id:276864)的数值最小化
大多数现实世界中的物理模型都是[非线性](@entry_id:637147)的。对于[非线性模型](@entry_id:276864) $f(\theta)$，通常不存在解析解，必须依赖迭代的[数值优化](@entry_id:138060)算法来寻找 $\chi^2$ 的最小值。诸如梯度下降、[牛顿法](@entry_id:140116)、拟牛顿法（BFGS）等算法是实现这一目标的常用工具。这些算法的核心是利用 $\chi^2$ 函数的局部梯度和曲率信息来指导搜索方向。

- **梯度 (Gradient)**：梯度向量 $\nabla \chi^2(\theta)$ 指向 $\chi^2$ 函数值增长最快的方向。其第 $a$ 个分量为：
  $$
  (\nabla \chi^2(\theta))_a = \frac{\partial \chi^2}{\partial \theta_a} = -2 \sum_{i,j} \frac{\partial f_i(\theta)}{\partial \theta_a} (V^{-1})_{ij} (y_j - f_j(\theta))
  $$
  若以[雅可比矩阵](@entry_id:264467) $J_{ia}(\theta) = \frac{\partial f_i(\theta)}{\partial \theta_a}$ 和残差向量 $r(\theta) = y - f(\theta)$ 表示，则梯度可以紧凑地写为 $\nabla \chi^2(\theta) = -2 J(\theta)^T V^{-1} r(\theta)$。

- **[海森矩阵](@entry_id:139140) (Hessian Matrix)**：海森矩阵 $H_{ab}(\theta) = \frac{\partial^2 \chi^2}{\partial \theta_a \partial \theta_b}$ 描述了 $\chi^2$ 函数在最小值附近的局部曲率。其精确形式为 [@problem_id:3507483]：
  $$
  H_{ab}(\theta) = 2 \sum_{i,j} J_{ia}(\theta) (V^{-1})_{ij} J_{jb}(\theta) - 2 \sum_{i,j} \frac{\partial^2 f_i(\theta)}{\partial \theta_a \partial \theta_b} (V^{-1})_{ij} r_j(\theta)
  $$
  [海森矩阵](@entry_id:139140)在[牛顿法](@entry_id:140116)等[二阶优化](@entry_id:175310)算法中至关重要。同时，我们将在后面看到，它也直接关系到参数估计的不确定度。在最小值附近，残差 $r_j(\theta)$ 通常很小，因此海森矩阵的第二项常常被忽略。剩下的第一项被称为**[高斯-牛顿近似](@entry_id:749740) (Gauss-Newton approximation)**，它仅依赖于模型的[一阶导数](@entry_id:749425)。

### 结果的诠释：[拟合优度](@entry_id:637026)与参数不确定度

在找到最佳拟合参数 $\hat{\theta}$ 后，我们需要回答两个关键问题：1. 模型对数据的描述有多好？2. 参数 $\hat{\theta}$ 的不确定度是多少？

#### [拟合优度检验](@entry_id:267868)
**[拟合优度](@entry_id:637026) (Goodness-of-Fit, GoF)** 检验旨在评估“数据与模型在最佳拟合点的一致性”是否在统计涨落的预期范围内 [@problem_id:3507413]。

- **$\chi^2_k$ [分布](@entry_id:182848)**：Go[F检验](@entry_id:274297)的理论基础是**皮尔逊定理**。该定理指出，如果模型是正确的，且满足某些[正则性条件](@entry_id:166962)，那么在最佳拟合点计算出的 $\chi^2$ 最小值 $\chi^2_{\text{min}} = \chi^2(\hat{\theta})$ 会遵循一个自由度为 $k$ 的 $\chi^2$ [分布](@entry_id:182848)，记作 $\chi^2_k$。**自由度 (degrees of freedom)** $k$ 的计算方式为：
  $$
  k = N - p
  $$
  其中 $N$ 是数据点的数量，$p$ 是从数据中拟合出的自由参数的数量 [@problem_id:3507444]。$\chi^2_k$ [分布](@entry_id:182848)本身可以被定义为 $k$ 个独立的标准正态分布变量的平方和 [@problem_id:3507463]。

- **简约 $\chi^2$ (Reduced Chi-squared)**：一个 $\chi^2_k$ [分布](@entry_id:182848)的[期望值](@entry_id:153208)是 $k$。因此，我们可以定义**简约 $\chi^2$**：
  $$
  \chi^2_{\text{red}} = \frac{\chi^2_{\text{min}}}{k} = \frac{\chi^2_{\text{min}}}{N-p}
  $$
  作为一个快速的GoF诊断指标。一个“好”的拟合通常期望 $\chi^2_{\text{red}} \approx 1$。如果 $\chi^2_{\text{red}} \gg 1$，这强烈暗示模型本身有缺陷，或者实验不确定度被低估了。反之，如果 $\chi^2_{\text{red}} \ll 1$，这通常表明实验不确定度被高估了，或者模型过于灵活以至于拟合了统计噪声。

- **p值 (p-value)**：更定量的GoF度量是 [p值](@entry_id:136498)。它表示在假设模型正确的情况下，通过重复实验得到一个比当前观测到的 $\chi^2_{\text{min}}$ 更差（即更大）的 $\chi^2$ 值的概率。p值由 $\chi^2_k$ [分布](@entry_id:182848)的上尾积分给出 [@problem_id:3507463]：
  $$
  p\text{-value} = P(\chi^2_k \ge \chi^2_{\text{min}}) = \int_{\chi^2_{\text{min}}}^{\infty} f(x; k) dx
  $$
  其中 $f(x;k)$ 是 $\chi^2_k$ [分布](@entry_id:182848)的[概率密度函数](@entry_id:140610)。一个非常小的[p值](@entry_id:136498)（例如，$p  0.05$）通常被视为拒绝[原假设](@entry_id:265441)（即模型不适配数据）的证据。

重要的是要认识到，一个好的拟合（例如 $\chi^2_{\text{red}} \approx 1$）并不绝对保证参数估计是无偏的。如果模型具有足够的灵活性，它可能会“吸收”未被建模的系统效应，导致[拟合质量](@entry_id:637026)看起来很好，但参数值却被拉[向错](@entry_id:161223)误的地方。同样，如果[协方差矩阵](@entry_id:139155) $\mathbf{V}$ 本身不正确（例如，不确定度被夸大），也可能掩盖模型与数据之间的真实偏差 [@problem_id:3507413]。

#### 参数不确定度与[置信区间](@entry_id:142297)
$\chi^2$ 函数不仅给出了最佳参数值，其在最小值附近的“形状”或“曲率”也决定了这些参数的不确定度。一个在最小值附近陡峭变化的 $\chi^2$ 函数意味着参数被很好地约束，而不确定度小；反之，一个平坦的 $\chi^2$ 函数则表示参数约束很弱，不确定度大。

- **[海森矩阵](@entry_id:139140)与协[方差](@entry_id:200758)**：这种曲率由[海森矩阵](@entry_id:139140) $H$ 精确定量。在渐近极限下，[参数估计](@entry_id:139349)量 $\hat{\theta}$ 的[协方差矩阵](@entry_id:139155) $V_{\hat{\theta}}$ 与[海森矩阵](@entry_id:139140)的[逆矩阵](@entry_id:140380)直接相关：
  $$
  (V_{\hat{\theta}})^{-1} \approx \frac{1}{2} H(\hat{\theta})
  $$
  这建立了从 $\chi^2$ 曲率到参数不确定度的直接联系。这里的 $H$ 通常可以用其[高斯-牛顿近似](@entry_id:749740) $2 J^T V^{-1} J$ 来计算。这个关系是**[费雪信息矩阵](@entry_id:750640) (Fisher Information Matrix)** $I = E[\frac{1}{2}H]$ 在实际应用中的体现 [@problem_id:3507423]。

- **$\Delta\chi^2$ 方法**：一个更通用且强大的确定[置信区间](@entry_id:142297)的方法是利用 $\Delta\chi^2 = \chi^2(\theta) - \chi^2_{\text{min}}$ 的[分布](@entry_id:182848)特性。根据**[威尔克斯定理](@entry_id:169826) (Wilks' Theorem)**，在许多标准假设下（如大样本、模型正确等），$\Delta\chi^2$ 的[分布](@entry_id:182848)近似为一个自由度为 $\nu$ 的 $\chi^2$ [分布](@entry_id:182848)，其中 $\nu$ 是被固定或考察的参数数量 [@problem_id:3507372]。
  - **一维置信区间 ($\nu=1$)**：要确定单个参数 $\theta_1$ 的[置信区间](@entry_id:142297)，我们在固定 $\theta_1$ 的同时，最小化（即**剖析 (profile)**）$\chi^2$ 函数关于所有其他参数的值。然后，我们寻找使 $\Delta\chi^2(\theta_1) \le q$ 的 $\theta_1$ 的范围。其中 $q$ 是 $\chi^2_1$ [分布](@entry_id:182848)的上[分位数](@entry_id:178417)。常用的阈值有：
    - $q=1.00$ 对应 $68.3\%$ [置信水平](@entry_id:182309) (CL)。
    - $q=3.84$ 对应 $95\%$ [置信水平](@entry_id:182309) (CL)。
  - **二维置信区域 ($\nu=2$)**：要确定两个参数 $(\theta_1, \theta_2)$ 的联合置信区域，我们寻找使 $\Delta\chi^2(\theta_1, \theta_2) \le q$ 的[参数空间](@entry_id:178581)区域，其中 $q$ 来自 $\chi^2_2$ [分布](@entry_id:182848)。常用的阈值有：
    - $q=2.30$ 对应 $68.3\%$ [置信水平](@entry_id:182309) (CL)。
    - $q=5.99$ 对应 $95\%$ [置信水平](@entry_id:182309) (CL)。
  这种基于 $\Delta\chi^2$ 的方法非常强大，因为它自然地处理了[非线性模型](@entry_id:276864)和参数之间的相关性。然而，其有效性依赖于[威尔克斯定理](@entry_id:169826)的假设，例如真实参数值不能位于参数空间的边界上。

### 高级主题：处理[讨厌参数](@entry_id:171802)

在多数实际分析中，模型参数可以分为两类：我们感兴趣的**物理参数 (parameters of interest, POI)** $\theta$，以及描述探测器响应、背景模型等辅助效应的**[讨厌参数](@entry_id:171802) (nuisance parameters, NP)** $\eta$。正确处理[讨厌参数](@entry_id:171802)对于获得可靠的物理结果至关重要。

一种标准方法是通过独立的[辅助测量](@entry_id:143842)或理论计算来约束[讨厌参数](@entry_id:171802)。如果这些约束可以用[高斯分布](@entry_id:154414)来描述（例如，$\eta_j$ 的期望为0，[标准差](@entry_id:153618)为 $\sigma_{\eta_j}$），那么它们可以通过向总 $\chi^2$ 函数添加惩罚项的方式被纳入拟合中 [@problem_id:3507489] [@problem_id:3507423]：
$$
\chi^2_{\text{total}}(\theta, \eta) = \chi^2_{\text{data}}(\theta, \eta) + \chi^2_{\text{penalty}}(\eta) = \sum_{i=1}^{N} \frac{(y_i - \mu_i(\theta, \eta))^2}{\sigma_i^2} + \sum_{j=1}^{m} \left(\frac{\eta_j}{\sigma_{\eta_j}}\right)^2
$$
在进行参数估计时，我们对[讨厌参数](@entry_id:171802) $\eta$ 进行**剖析 (profiling)**，即对每一个固定的 $\theta$ 值，找到使 $\chi^2_{\text{total}}$ 最小的 $\hat{\eta}(\theta)$，从而得到一个只依赖于 $\theta$ 的**剖析$\chi^2$函数** $\chi^2_{\text{prof}}(\theta)$。最终对 POI 的估计和[置信区间](@entry_id:142297)的确定都基于这个剖析函数。

剖析过程正确地将[讨厌参数](@entry_id:171802)的[不确定性传播](@entry_id:146574)到了物理参数的不确定性中。这通常会导致 POI 的不确定性增加，因为模型必须在[讨厌参数](@entry_id:171802)允许的范围内变化。在一个线性化的模型中，可以证明剖析掉由协[方差](@entry_id:200758) $V_\eta$ 约束的[讨厌参数](@entry_id:171802)，其效应等价于在[数据协方差](@entry_id:748192)矩阵中增加一个系统不确定性项 $A V_\eta A^T$，其中 $A$ 是模型对[讨厌参数](@entry_id:171802)的敏感度矩阵 [@problem_id:3507489]。如果[讨厌参数](@entry_id:171802)完全不受约束（$\sigma_{\eta_j} \to \infty$），剖析过程会有效地将模型在该参数方向上的变化投影掉，从而失去对相应物理效应的敏感性。

在正确的模型假设下，这种包含高斯约束并进行剖析的联合拟合方法会产生对物理参数 $\theta$ 的无偏估计。拟合后得到的[讨厌参数](@entry_id:171802)最佳值 $\hat{\eta}_j$ (常被称为“pulls”)不为零，这本身并不意味着偏倚，而是反映了数据与约束之间的平衡，以及不同参数之间的相关性 [@problem_id:3507489]。