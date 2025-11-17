## 引言
在[随机模拟](@entry_id:168869)和计算科学领域，蒙特卡洛方法是一种不可或缺的强大工具，但其[收敛速度](@entry_id:636873)往往受到计算资源的限制。标准[蒙特卡洛估计](@entry_id:637986)的精度与样本量的平方根成正比，这意味着要将误差减半，就需要将计算量增加四倍。为了克服这一瓶颈，学术界发展了多种[方差缩减技术](@entry_id:141433)，旨在以更少的计算成本获得更精确的估计结果。对偶变量（Antithetic Variates）便是其中一种构思巧妙且应用广泛的高效方法。

本文旨在系统性地介绍对偶变量技术。它通过利用输入随机数的对称性，在模拟输出中主动引入负相关性，从而巧妙地“抵消”部分随机波动，达到缩减[方差](@entry_id:200758)的目的。这不仅提升了模拟效率，也为理解随机性与对称性之间的深刻联系提供了独特的视角。

在接下来的内容中，我们将分三个章节深入探索对偶变量的各个方面。在“原理与机制”一章中，我们将揭示其背后的数学原理，明确其有效性的条件（[单调性](@entry_id:143760)）与局限性（对称性），并讨论如何正确地估计其[方差](@entry_id:200758)。随后，在“应用与跨学科联系”一章，我们将展示该技术如何在计算金融、[运筹学](@entry_id:145535)、计算机图形学等多个领域解决实际问题，并探讨其如何与其他[方差缩减技术](@entry_id:141433)协同工作。最后，“动手实践”部分将通过一系列精心设计的问题，引导您将理论知识转化为解决实际问题的能力。

## 原理与机制

在[蒙特卡洛模拟](@entry_id:193493)中，一个核心目标是以尽可能少的计算成本获得尽可能精确的[期望值](@entry_id:153208)估计。标准[蒙特卡洛估计](@entry_id:637986)量的[方差](@entry_id:200758)随着样本量 $N$ 的增加而以 $1/N$ 的速率下降。[方差缩减技术](@entry_id:141433)（variance reduction techniques）旨在通过修改抽样过程或估计量本身，来获得一个比标准[蒙特卡洛方法](@entry_id:136978)在相同计算成本下具有更小[方差](@entry_id:200758)的[无偏估计量](@entry_id:756290)。对偶变量（antithetic variates）是一种优雅且强大的[方差缩减技术](@entry_id:141433)，它通过在输入随机数之间引入负相关性来达到此目的。本章将深入探讨对偶变量的数学原理、作用机制、适用条件以及实践中的注意事项。

### 核心原理：引入负相关性

让我们从[方差](@entry_id:200758)的基本性质出发。考虑两个[随机变量](@entry_id:195330) $Y_1$ 和 $Y_2$，它们的和的[方差](@entry_id:200758)为：
$$
\mathrm{Var}(Y_1 + Y_2) = \mathrm{Var}(Y_1) + \mathrm{Var}(Y_2) + 2\mathrm{Cov}(Y_1, Y_2)
$$
如果我们使用两个独立同分布的样本 $g(U_1)$ 和 $g(U_2)$ 来估计 $\theta = \mathbb{E}[g(U)]$，其中 $U_1, U_2 \stackrel{\text{i.i.d.}}{\sim} \mathrm{Unif}(0,1)$，那么一个简单的估计量是它们的平均值 $\hat{\theta} = \frac{1}{2}(g(U_1) + g(U_2))$。由于独立性，$\mathrm{Cov}(g(U_1), g(U_2)) = 0$，其[方差](@entry_id:200758)为：
$$
\mathrm{Var}(\hat{\theta}) = \frac{1}{4} (\mathrm{Var}(g(U_1)) + \mathrm{Var}(g(U_2))) = \frac{1}{2}\mathrm{Var}(g(U))
$$
现在，设想我们有能力生成一对**相依**的[随机变量](@entry_id:195330) $Y_1$ 和 $Y_2$，它们仍然满足 $\mathbb{E}[Y_1] = \mathbb{E}[Y_2] = \theta$，但它们之间存在协[方差](@entry_id:200758)。由这对样本构成的估计量 $\hat{\theta}_{\text{dep}} = \frac{1}{2}(Y_1 + Y_2)$ 的[方差](@entry_id:200758)将是：
$$
\mathrm{Var}(\hat{\theta}_{\text{dep}}) = \frac{1}{4}(\mathrm{Var}(Y_1) + \mathrm{Var}(Y_2) + 2\mathrm{Cov}(Y_1, Y_2))
$$
与[独立样本](@entry_id:177139)的情况相比，如果我们可以构造出一对样本使得它们的协[方差](@entry_id:200758) $\mathrm{Cov}(Y_1, Y_2)$ 为负，那么我们就能获得一个[方差](@entry_id:200758)更小的估计量。这就是对偶变量技术的核心思想：通过精心设计输入的随机数，在模拟的输出之间主动引入负相关性，从而达到**[方差缩减](@entry_id:145496)**的目的。

### 对偶变量技术

对偶变量技术利用了[均匀分布](@entry_id:194597)的一个简单而优美的对称性质。如果一个[随机变量](@entry_id:195330) $U$ 服从 $[0,1]$ 上的[均匀分布](@entry_id:194597)（$U \sim \mathrm{Unif}(0,1)$），那么它的“对偶”[随机变量](@entry_id:195330) $1-U$ 也服从 $[0,1]$ 上的[均匀分布](@entry_id:194597)。我们可以通过检查其累积分布函数来验证这一点：
$$
\mathbb{P}(1-U \le v) = \mathbb{P}(U \ge 1-v) = 1 - \mathbb{P}(U  1-v) = 1 - (1-v) = v \quad \text{for } v \in [0,1]
$$
这正是 $\mathrm{Unif}(0,1)$ [分布](@entry_id:182848)的[累积分布函数](@entry_id:143135)。因此，$U$ 和 $1-U$ 是同[分布](@entry_id:182848)的。这意味着对于任何[可积函数](@entry_id:191199) $g$，都有 $\mathbb{E}[g(U)] = \mathbb{E}[g(1-U)] = \theta$。

此外，[随机变量](@entry_id:195330) $U$ 和 $1-U$ 是完全负相关的，它们的协[方差](@entry_id:200758)为：
$$
\mathrm{Cov}(U, 1-U) = \mathbb{E}[U(1-U)] - \mathbb{E}[U]\mathbb{E}[1-U] = \mathbb{E}[U-U^2] - (\frac{1}{2})(1-\frac{1}{2}) = (\frac{1}{2}-\frac{1}{3}) - \frac{1}{4} = \frac{1}{6}-\frac{1}{4} = -\frac{1}{12}
$$
由于 $\mathrm{Var}(U) = \mathrm{Var}(1-U) = 1/12$，它们的**[相关系数](@entry_id:147037)**（correlation coefficient）为：
$$
\mathrm{Corr}(U, 1-U) = \frac{\mathrm{Cov}(U, 1-U)}{\sqrt{\mathrm{Var}(U)\mathrm{Var}(1-U)}} = \frac{-1/12}{\sqrt{(1/12)(1/12)}} = -1
$$
这种输入之间的完美负相关正是我们希望利用的结构。

**对偶变量估计量** (antithetic variate estimator) 基于由 $(U, 1-U)$ 构成的**对偶对** (antithetic pair)。对于单次模拟，我们不生成两个独立的随机数，而是生成一个 $U_1 \sim \mathrm{Unif}(0,1)$，并构造其对偶 $1-U_1$。然后，我们计算两个输出 $g(U_1)$ 和 $g(1-U_1)$，并形成如下的单对估计量：
$$
\hat{\theta}_{\text{anti},1} = \frac{1}{2}(g(U_1) + g(1-U_1))
$$
为了构建一个总样本量为 $2n$ 的估计，我们独立地重复这个过程 $n$ 次，生成 $n$ 个对偶对 $(U_i, 1-U_i)$，其中 $U_1, \dots, U_n$ 是[独立同分布](@entry_id:169067)的。最终的估计量是这 $n$ 个单对估计量的平均值：
$$
\hat{\theta}_{\text{anti},n} = \frac{1}{n} \sum_{i=1}^{n} \frac{g(U_i) + g(1-U_i)}{2}
$$
这个估计量是一个**[无偏估计量](@entry_id:756290)** (unbiased estimator) [@problem_id:3288397]。我们可以通过其[期望值](@entry_id:153208)来验证：
$$
\mathbb{E}[\hat{\theta}_{\text{anti},n}] = \frac{1}{n} \sum_{i=1}^{n} \mathbb{E}\left[\frac{g(U_i) + g(1-U_i)}{2}\right] = \frac{1}{2n} \sum_{i=1}^{n} (\mathbb{E}[g(U_i)] + \mathbb{E}[g(1-U_i)])
$$
由于 $U_i$ 和 $1-U_i$ 同[分布](@entry_id:182848)，$\mathbb{E}[g(U_i)] = \mathbb{E}[g(1-U_i)] = \theta$。因此，
$$
\mathbb{E}[\hat{\theta}_{\text{anti},n}] = \frac{1}{2n} \sum_{i=1}^{n} (\theta + \theta) = \frac{1}{2n} (2n\theta) = \theta
$$
对偶变量技术保持了估计的无偏性，这是所有[方差缩减技术](@entry_id:141433)的一个理想特性 [@problem_id:3288406]。

### 方差分析与有效性条件

对偶变量[估计量的方差](@entry_id:167223)是多少？由于 $n$ 个对偶对是相互独立的，我们可以先计算单对估计量 $\hat{\theta}_{\text{anti},1}$ 的[方差](@entry_id:200758)，然后除以 $n$。
$$
\mathrm{Var}(\hat{\theta}_{\text{anti},n}) = \frac{1}{n}\mathrm{Var}(\hat{\theta}_{\text{anti},1}) = \frac{1}{n} \mathrm{Var}\left(\frac{g(U) + g(1-U)}{2}\right)
$$
$$
= \frac{1}{4n} \left[ \mathrm{Var}(g(U)) + \mathrm{Var}(g(1-U)) + 2\mathrm{Cov}(g(U), g(1-U)) \right]
$$
因为 $g(U)$ 和 $g(1-U)$ 同[分布](@entry_id:182848)，它们的[方差](@entry_id:200758)相等。令 $\sigma_g^2 = \mathrm{Var}(g(U))$，我们得到：
$$
\mathrm{Var}(\hat{\theta}_{\text{anti},n}) = \frac{1}{2n} \left[ \sigma_g^2 + \mathrm{Cov}(g(U), g(1-U)) \right]
$$
现在，我们将它与使用相同计算成本（即 $2n$ 次函数求值）的标准[蒙特卡洛估计](@entry_id:637986)量的[方差](@entry_id:200758)进行比较。标准估计量 $\hat{\theta}_{\text{ind}, 2n} = \frac{1}{2n}\sum_{j=1}^{2n}g(V_j)$（其中 $V_j$ [独立同分布](@entry_id:169067)）的[方差](@entry_id:200758)为：
$$
\mathrm{Var}(\hat{\theta}_{\text{ind}, 2n}) = \frac{\sigma_g^2}{2n}
$$
比较这两个[方差](@entry_id:200758)，我们发现对偶变量能够实现[方差缩减](@entry_id:145496)当且仅当：
$$
\mathrm{Cov}(g(U), g(1-U))  0
$$
这个条件是对偶变量技术有效的关键。

#### [单调性](@entry_id:143760)条件

那么，在什么条件下，被积函数 $g$ 能够保证负协[方差](@entry_id:200758)呢？一个非常普遍且重要的充分条件是**单调性** (monotonicity) [@problem_id:3288397]。如果函数 $g:[0,1] \to \mathbb{R}$ 是单调的（即单调非减或单调非增），那么 $g(U)$ 和 $g(1-U)$ 之间的协[方差](@entry_id:200758)是非正的。

我们可以直观地理解这一点：假设 $g$ 是单调非减的。当随机输入 $U$ 的取值较大时，$1-U$ 的取值就较小。由于 $g$ 的单调性，$g(U)$ 的值会相对较大，而 $g(1-U)$ 的值会相对较小。反之，当 $U$ 较小时，$1-U$ 较大，导致 $g(U)$ 较小而 $g(1-U)$ 较大。这种“一个高，另一个就低”的负向联动关系正是负协[方差](@entry_id:200758)的体现。除非 $g$ 在 $[0,1]$ 上几乎处处为常数，否则对于严格单调的函数，这个协[方差](@entry_id:200758)将严格为负 [@problem_id:3288471] [@problem_id:3288406]。

#### 定量示例

让我们通过一个具体的例子来量化[方差缩减](@entry_id:145496)的效果。考虑估计积分 $I = \int_0^1 u^2 du = 1/3$，即 $g(u)=u^2$。函数 $g(u)=u^2$ 在 $[0,1]$ 上是单调递增的，因此我们预期对偶变量会很有效。

首先计算 $\mathrm{Var}(g(U))$：
$$
\mathbb{E}[g(U)] = \mathbb{E}[U^2] = \int_0^1 u^2 du = \frac{1}{3}
$$
$$
\mathbb{E}[g(U)^2] = \mathbb{E}[U^4] = \int_0^1 u^4 du = \frac{1}{5}
$$
$$
\sigma_g^2 = \mathrm{Var}(g(U)) = \mathbb{E}[U^4] - (\mathbb{E}[U^2])^2 = \frac{1}{5} - (\frac{1}{3})^2 = \frac{4}{45}
$$
接下来计算协[方差](@entry_id:200758) $\mathrm{Cov}(g(U), g(1-U)) = \mathrm{Cov}(U^2, (1-U)^2)$：
$$
\mathbb{E}[U^2(1-U)^2] = \int_0^1 u^2(1-2u+u^2)du = \int_0^1 (u^2-2u^3+u^4)du = \frac{1}{3} - \frac{2}{4} + \frac{1}{5} = \frac{1}{30}
$$
$$
\mathrm{Cov}(U^2, (1-U)^2) = \mathbb{E}[U^2(1-U)^2] - \mathbb{E}[U^2]\mathbb{E}[(1-U)^2] = \frac{1}{30} - (\frac{1}{3})(\frac{1}{3}) = \frac{1}{30} - \frac{1}{9} = -\frac{7}{90}
$$
协[方差](@entry_id:200758)确实为负。现在，我们来比较使用一对[独立样本](@entry_id:177139) $(U_1, U_2)$ 的估计量 $\hat{I}_{\text{ind}} = \frac{1}{2}(U_1^2 + U_2^2)$ 和使用一对对偶样本 $(U, 1-U)$ 的估计量 $\hat{I}_{\text{anti}} = \frac{1}{2}(U^2 + (1-U)^2)$ 的[方差](@entry_id:200758) [@problem_id:3288402]。

[独立样本](@entry_id:177139)[估计量的方差](@entry_id:167223)为：
$$
\mathrm{Var}(\hat{I}_{\text{ind}}) = \frac{1}{2}\mathrm{Var}(U^2) = \frac{1}{2} \cdot \frac{4}{45} = \frac{2}{45}
$$
对偶变量[估计量的方差](@entry_id:167223)为：
$$
\mathrm{Var}(\hat{I}_{\text{anti}}) = \frac{1}{2}(\mathrm{Var}(U^2) + \mathrm{Cov}(U^2, (1-U)^2)) = \frac{1}{2}(\frac{4}{45} - \frac{7}{90}) = \frac{1}{2}(\frac{8-7}{90}) = \frac{1}{180}
$$
[方差缩减](@entry_id:145496)的比率，或称**[有效样本量](@entry_id:271661)乘数** (Effective Sample Size multiplier)，为：
$$
\frac{\mathrm{Var}(\hat{I}_{\text{ind}})}{\mathrm{Var}(\hat{I}_{\text{anti}})} = \frac{2/45}{1/180} = 8
$$
这意味着，对于这个特定的问题，使用对偶变量的效率是标准[蒙特卡洛方法](@entry_id:136978)的8倍。换句话说，为了达到相同的精度，标准方法需要的样本量是对偶变量方法的8倍。

### 对称性的作用：从理想情况到不利情况

函数的**对称性** (symmetry) 决定了对偶变量的效果，其范围可以从实现零[方差](@entry_id:200758)的完美估计到反而增加[方差](@entry_id:200758)的灾难性后果。

#### 理想情况：零[方差](@entry_id:200758)

考虑一个线性函数 $g(u) = \alpha + \beta u$。其对偶估计量为：
$$
\hat{\theta}_{\text{anti},1} = \frac{1}{2}[(\alpha + \beta U) + (\alpha + \beta(1-U))] = \frac{1}{2}[2\alpha + \beta] = \alpha + \frac{\beta}{2}
$$
另一方面，真实的[期望值](@entry_id:153208)为 $\mathbb{E}[\alpha + \beta U] = \alpha + \beta\mathbb{E}[U] = \alpha + \beta/2$。我们发现，对于任何线性函数，对偶估计量 $\hat{\theta}_{\text{anti},1}$ 的值是一个与 $U$ 无关的常数，并且恰好等于真实的[期望值](@entry_id:153208) $\theta$。因此，其[方差](@entry_id:200758)为零 [@problem_id:3288397]。

这个结论可以推广到更一般的情况。如果一个函数 $g$ 关于点 $(1/2, \theta)$ **中心对称**，即满足 $g(u) + g(1-u) = 2\theta$ 对于几乎所有 $u \in [0,1]$ 成立，那么对偶估计量将总是等于 $\theta$，从而实现零[方差](@entry_id:200758)的完美估计 [@problem_id:3288406]。

#### 不利情况：[方差](@entry_id:200758)增加

与[单调性](@entry_id:143760)相反，如果函数 $g$ 关于 $u=1/2$ **轴对称**，即 $g(u) = g(1-u)$，那么对偶变量技术将适得其反。在这种情况下，$g(U)$ 和 $g(1-U)$ 是完全相同的[随机变量](@entry_id:195330)，它们的协[方差](@entry_id:200758)为：
$$
\mathrm{Cov}(g(U), g(1-U)) = \mathrm{Cov}(g(U), g(U)) = \mathrm{Var}(g(U)) = \sigma_g^2 > 0
$$
此时，对偶估计量（基于 $n$ 对，总共 $2n$ 次求值）的[方差](@entry_id:200758)为：
$$
\mathrm{Var}(\hat{\theta}_{\text{anti},n}) = \frac{1}{2n}(\sigma_g^2 + \sigma_g^2) = \frac{\sigma_g^2}{n}
$$
这比标准[蒙特卡洛估计](@entry_id:637986)量在相同计算成本下的[方差](@entry_id:200758) $\frac{\sigma_g^2}{2n}$ 要大一倍！这意味着在这种情况下，使用对偶变量会使估计的效率降低一半。

一个典型的例子是函数 $g(u) = \cos(4\pi u)$ [@problem_id:3288408]。由于 $\cos(4\pi(1-u)) = \cos(4\pi - 4\pi u) = \cos(-4\pi u) = \cos(4\pi u)$，该函数是[轴对称](@entry_id:173333)的。因此，使用对偶变量将导致[方差](@entry_id:200758)加倍。

另一个重要的例子来自[金融工程](@entry_id:136943)，例如估计一个简单的数字期权的价格。其收益函数可以表示为 $H = \mathbf{1}\{|Z| \le a\}$，其中 $Z \sim \mathcal{N}(0,1)$。通过[逆变换法](@entry_id:141695) $Z=\Phi^{-1}(U)$，我们估计的函数是 $f(u) = \mathbf{1}\{|\Phi^{-1}(u)| \le a\}$。由于[标准正态分布](@entry_id:184509)的quantile函数具有对称性 $\Phi^{-1}(1-u) = -\Phi^{-1}(u)$，我们有 $|-\Phi^{-1}(u)| = |\Phi^{-1}(u)|$。因此，$f(u) = f(1-u)$，这个函数也是轴对称的。应用对偶变量将同样导致[方差](@entry_id:200758)加倍 [@problem_id:3288418]。

这些反例警示我们，对偶变量并非万能药。在使用前，必须对被积函数的性质进行分析，至少要确保它不是对称的，并且最好是单调的。

### 推广与高级视角

对偶变量的思想可以被推广到更广泛的场景。

#### 对非[均匀分布](@entry_id:194597)的应用

该技术不仅限于[均匀分布](@entry_id:194597)。通过**[逆变换法](@entry_id:141695)** (inversion method)，它可以应用于任何可以由[均匀分布](@entry_id:194597)生成的[随机变量](@entry_id:195330)。一个重要的例子是标准正态分布 $X \sim \mathcal{N}(0,1)$，它可以通过 $X = \Phi^{-1}(U)$ 生成，其中 $\Phi$ 是标准正态的累积分布函数。由于 $\Phi^{-1}(1-U) = -\Phi^{-1}(U)$，来自 $[0,1]$ 上的对偶对 $(U, 1-U)$ 在正态空间中映射为对偶对 $(X, -X)$ [@problem_id:3288472]。

因此，为了估计 $\mu = \mathbb{E}[h(X)]$，我们可以使用对偶估计量 $\frac{1}{2}(h(X) + h(-X))$。
- 如果 $h$ 是一个**[奇函数](@entry_id:173259)**（$h(-x) = -h(x)$），那么 $\mathbb{E}[h(X)]=0$，而对偶估计量 $\frac{1}{2}(h(X) - h(X)) = 0$。估计量总是等于真值，[方差](@entry_id:200758)为零。
- 如果 $h$ 是一个**[偶函数](@entry_id:163605)**（$h(-x) = h(x)$），那么 $h(X) = h(-X)$，我们再次遇到了[方差](@entry_id:200758)增加的情况。
- 如果 $h$ 是**单调函数**，例如 $h(x) = \exp(tx)$（$t \ne 0$），那么 $h(X)$ 和 $h(-X)$ 之间会产生负相关，从而实现[方差缩减](@entry_id:145496)。

#### 多维对偶变量

对偶变量可以自然地推广到多维情况。如果要估计 $\mathbb{E}[g(U_1, \dots, U_d)]$，其中 $U_i \stackrel{\text{i.i.d.}}{\sim} \mathrm{Unif}(0,1)$，我们可以使用[对偶向量](@entry_id:161217)。给定一个随机向量 $\boldsymbol{U} = (U_1, \dots, U_d)$，其[对偶向量](@entry_id:161217)定义为 $\mathbf{1}-\boldsymbol{U} = (1-U_1, \dots, 1-U_d)$。如果 $g: [0,1]^d \to \mathbb{R}$ 在每个坐标上都是单调的，那么可以证明 $\mathrm{Cov}(g(\boldsymbol{U}), g(\mathbf{1}-\boldsymbol{U})) \le 0$，从而保证了[方差缩减](@entry_id:145496) [@problem_id:3288406]。这对于处理[高维积分](@entry_id:143557)，如金融衍生品定价中的问题，尤其有用。

#### [对称与反对称分解](@entry_id:204005)

从一个更抽象的视角，任何函数 $g$ 都可以分解为其关于[对偶变换](@entry_id:137576) $T(u)=1-u$ 的对称部分 $g_s$ 和反对称部分 $g_a$ [@problem_id:3288452]：
$$
g(u) = g_s(u) + g_a(u)
$$
其中，
$$
g_s(u) = \frac{g(u) + g(1-u)}{2}, \quad g_a(u) = \frac{g(u) - g(1-u)}{2}
$$
对偶估计量 $\hat{\theta}_{\text{anti},1}$ 正是 $g_s(U)$。由于 $g_a(U)$ 的期望为零，$\mathbb{E}[g_s(U)] = \mathbb{E}[g(U)] = \theta$。因此，对偶变量方法本质上是通过对函数进行对称化来估计期望，同时丢弃了期望为零的反对称部分。[估计量的方差](@entry_id:167223)就是 $\mathrm{Var}(g_s(U)) = \frac{1}{2}(\mathrm{Var}(g(U)) + \mathrm{Cov}(g(U), g(1-U)))$，这为我们之[前推](@entry_id:158718)导的[方差](@entry_id:200758)公式提供了另一种解释。

### 实际应用：估计[估计量的方差](@entry_id:167223)

最后，一个关键的实践问题是：我们如何估计对偶变量估计量自身的[方差](@entry_id:200758)，以便构建[置信区间](@entry_id:142297)？

假设我们生成了 $n$ 个对偶对，并计算了 $n$ 个单对估计值 $Y_i = \frac{1}{2}(g(U_i) + g(1-U_i))$。我们的最终[点估计量](@entry_id:171246)是这些值的样本均值 $\hat{\theta}_{\text{anti},n} = \bar{Y} = \frac{1}{n}\sum_{i=1}^n Y_i$。

这里的关键在于，尽管我们的模拟总共使用了 $2n$ 个函数求值，我们应该将数据视为包含 $n$ 个[独立同分布](@entry_id:169067)的样本 $\{Y_1, \dots, Y_n\}$。因此，估计 $\mathrm{Var}(\hat{\theta}_{\text{anti},n})$ 的正确方法是计算这 $n$ 个 $Y_i$ 值的样本[方差](@entry_id:200758) $S_Y^2 = \frac{1}{n-1}\sum_{i=1}^n(Y_i - \bar{Y})^2$，然后[估计量的方差](@entry_id:167223)估计为 $S_Y^2/n$。

一个常见的错误是，将所有 $2n$ 个输出值 $\{g(U_1), g(1-U_1), \dots, g(U_n), g(1-U_n)\}$ 混合在一起（pooling），然后像对待 $2n$ 个[独立样本](@entry_id:177139)一样计算样本[方差](@entry_id:200758) $S_{\text{pool}}^2$，并使用 $S_{\text{pool}}^2/(2n)$ 作为[方差](@entry_id:200758)的估计。这种方法是错误的，因为它忽略了对偶对内部的负相关性。实际上，这种“混合”方法会高估真实[方差](@entry_id:200758)，因为它未能捕捉到对偶变量带来的[方差缩减](@entry_id:145496)效果。这将导致我们构建的置信区间比应有的更宽，从而无法在报告中体现出该方法的效率提升 [@problem_id:3288413]。

总之，对偶变量是一种概念简单但效果显著的[方差缩减技术](@entry_id:141433)。它的成功依赖于被积函数与输入随机数对称性之间的相互作用，特别是单调性。正确理解其适用条件和局限性，以及在实践中如何正确估计其[方差](@entry_id:200758)，是有效利用该方法的关键。