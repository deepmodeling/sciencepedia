## 引言
在贝叶斯统计的实践中，[先验分布](@entry_id:141376)的选择至关重要。当我们缺乏关于未知参数的先验知识，或希望分析尽可能“客观”时，我们如何选择一个能让数据“自己说话”的先验分布？这正是统计学中一个核心的挑战。杰弗里斯先验，由哈罗德·杰弗里斯提出，为这一问题提供了优雅的解决方案，它通过一个基于模型自身结构的形式化规则来构建先验，从而在客观贝叶斯方法中扮演着基石性的角色。

本文旨在全面地介绍这一强大工具。在第一章“原则与机制”中，我们将深入探讨杰弗里斯先验的数学定义，学习如何利用费雪信息来推导它，并理解其最重要的性质——[重参数化不变性](@entry_id:197540)。接下来，在第二章“应用与跨学科联系”中，我们将展示它在从经典[统计模型](@entry_id:165873)到化学、天体物理学等前沿科学领域的具体应用，揭示其理论与实践的紧密联系。最后，“动手实践”部分将提供一系列练习，帮助您将理论知识转化为实际的计算能力。通过这三个章节的学习，您将对杰弗里斯先验建立起一个系统而深入的认识。

## 原则与机制

在[贝叶斯推断](@entry_id:146958)的实践中，选择[先验分布](@entry_id:141376)是基石性的一步。当关于未知参数 $\theta$ 的先验知识匮乏或为了追求分析的“客观性”时，统计学家们寻求一种能够让数据“自己说话”的先验，即所谓的**[无信息先验](@entry_id:172418) (non-informative prior)**。然而，一个真正“无信息”的先验在理论上是不存在的。任何[先验分布](@entry_id:141376)都会对[后验分布](@entry_id:145605)产生影响。因此，目标转向于构建具有理想性质的、影响尽可能小的“客观”先验。哈罗德·杰弗里斯 (Harold Jeffreys) 提出的方法是这一领域的核心贡献之一，它通过一个优美的原则——**[不变性](@entry_id:140168) (invariance)**——来构建先验。本章将深入探讨杰弗里斯先验的定义、核心性质、计算方法及其在实践中的应用与局限。

### 杰弗里斯先验的定义：基于费雪信息

杰弗里斯先验的核心思想是，先验分布不应依赖于模型参数的特定表示方式。例如，对于一个[指数分布](@entry_id:273894)，我们可以用失效率 $\lambda$ 来参数化，也可以用[平均寿命](@entry_id:195236) $\tau = 1/\lambda$ 来参数化。这两种[参数化](@entry_id:272587)描述的是同一个物理过程，因此，我们对其中一个参数的先验信念，在经过适当的变换后，应当与直接对另一个参数设定的先验信念相一致。这种性质被称为**[重参数化不变性](@entry_id:197540) (reparameterization invariance)**。

为了实现这一目标，杰弗里斯提出将先验[概率密度函数](@entry_id:140610) $\pi(\theta)$ 定义为与**费雪信息 (Fisher Information)** 的平方根成正比。对于单个参数 $\theta$，杰弗里斯先验的形式为：

$$ \pi_J(\theta) \propto \sqrt{I(\theta)} $$

这里的 $I(\theta)$ 是单个观测值所包含的关于参数 $\theta$ 的[费雪信息](@entry_id:144784)量。其定义为[对数似然函数](@entry_id:168593)[二阶导数](@entry_id:144508)的负[期望值](@entry_id:153208)：

$$ I(\theta) = -E_{X|\theta}\left[ \frac{\partial^2}{\partial\theta^2} \ln f(x|\theta) \right] $$

其中，$f(x|\theta)$ 是给定参数 $\theta$ 时数据 $x$ 的概率（密度或质量）函数，$\ln f(x|\theta)$ 是[对数似然函数](@entry_id:168593)，期望 $E_{X|\theta}[\cdot]$ 是在 $f(x|\theta)$ 的[分布](@entry_id:182848)下计算的。

[费雪信息](@entry_id:144784)直观上衡量了[似然函数](@entry_id:141927)在参数[真值](@entry_id:636547)附近的“尖锐”程度。一个尖锐的似然函数意味着数据对参数 $\theta$ 的值提供了强有力的信息，微小的参数变动会导致似然函数值发生剧烈变化。因此，$I(\theta)$ 很大的区域，意味着数据对参数的约束很强；反之亦然。杰弗里斯先验正是利用了这种由数据模型本身所蕴含的结构信息，来构造一个“客观”的先验。

### 杰弗里斯先验的计算与实例

计算杰弗里斯先验通常遵循一个固定的流程：
1.  写出单个观测值的[对数似然函数](@entry_id:168593) $\ln f(x|\theta)$。
2.  计算[对数似然函数](@entry_id:168593)关于参数 $\theta$ 的[二阶偏导数](@entry_id:635213) $\frac{\partial^2}{\partial\theta^2} \ln f(x|\theta)$。
3.  计算该[二阶导数](@entry_id:144508)在数据[分布](@entry_id:182848) $X \sim f(x|\theta)$ 下的期望，并取负号，得到费雪信息 $I(\theta)$。
4.  取[费雪信息](@entry_id:144784)的平方根，即得到与杰弗里斯先验成正比的函数形式。

让我们通过几个经典的例子来掌握这一过程。

**实例一：指数分布的失效率**

假设一个电子元件的寿命 $T$ 服从[指数分布](@entry_id:273894)，其概率密度函数为 $f(t; \lambda) = \lambda \exp(-\lambda t)$，其中 $\lambda > 0$ 是失效率参数。为了给 $\lambda$ 设定一个[无信息先验](@entry_id:172418)，我们来计算其杰弗里斯先验 [@problem_id:1624948]。

[对数似然函数](@entry_id:168593)为 $\ell(\lambda) = \ln \lambda - \lambda t$。
其一阶和[二阶导数](@entry_id:144508)分别为：
$$ \frac{\partial \ell}{\partial \lambda} = \frac{1}{\lambda} - t $$
$$ \frac{\partial^2 \ell}{\partial \lambda^2} = -\frac{1}{\lambda^2} $$
注意到[二阶导数](@entry_id:144508)不依赖于观测值 $t$，因此其期望就是它本身。费雪信息为：
$$ I(\lambda) = -E\left[-\frac{1}{\lambda^2}\right] = \frac{1}{\lambda^2} $$
因此，$\lambda$ 的杰弗里斯先验为：
$$ \pi_J(\lambda) \propto \sqrt{I(\lambda)} = \sqrt{\frac{1}{\lambda^2}} = \frac{1}{\lambda} \quad (\text{for } \lambda > 0) $$

**实例二：[泊松分布](@entry_id:147769)的[率参数](@entry_id:265473)**

考虑一个服从泊松分布的[随机变量](@entry_id:195330) $K$，其[概率质量函数](@entry_id:265484)为 $P(k; \lambda) = \frac{\lambda^k e^{-\lambda}}{k!}$，其中 $\lambda > 0$ 是事件发生的[平均速率](@entry_id:147100)。我们来推导 $\lambda$ 的杰弗里斯先验 [@problem_id:815072]。

[对数似然函数](@entry_id:168593)为 $\ln P(k; \lambda) = k \ln \lambda - \lambda - \ln k!$。
其[二阶导数](@entry_id:144508)为 $\frac{\partial^2}{\partial\lambda^2} \ln P = -\frac{k}{\lambda^2}$。
为了计算费雪信息，我们需要对 $k$ 取期望。对于[泊松分布](@entry_id:147769)，我们知道 $E[k] = \lambda$。
$$ I(\lambda) = -E\left[-\frac{k}{\lambda^2}\right] = \frac{E[k]}{\lambda^2} = \frac{\lambda}{\lambda^2} = \frac{1}{\lambda} $$
于是，$\lambda$ 的杰弗里斯先验为：
$$ \pi_J(\lambda) \propto \sqrt{I(\lambda)} = \sqrt{\frac{1}{\lambda}} = \lambda^{-\frac{1}{2}} \quad (\text{for } \lambda > 0) $$
这个例子与指数分布的例子形成了有趣的对比，说明杰弗里斯先验的具体形式依赖于模型的概率结构。

**实例三：[伯努利试验](@entry_id:268355)的成功概率**

对于单次伯努利试验，结果 $X \in \{0, 1\}$，成功概率为 $p \in (0, 1)$。其[概率质量函数](@entry_id:265484)为 $f(x|p) = p^x (1-p)^{1-x}$。我们来确定参数 $p$ 的杰弗里斯先验 [@problem_id:1379701]。

[对数似然函数](@entry_id:168593)为 $\ln f(X|p) = X \ln p + (1-X) \ln(1-p)$。
其[二阶导数](@entry_id:144508)为 $\frac{\partial^2}{\partial p^2} \ln f(X|p) = -\frac{X}{p^2} - \frac{1-X}{(1-p)^2}$。
在 $X \sim \text{Bernoulli}(p)$ 的[分布](@entry_id:182848)下，$E[X]=p$，因此费雪信息为：
$$ I(p) = -E\left[-\frac{X}{p^2} - \frac{1-X}{(1-p)^2}\right] = \frac{E[X]}{p^2} + \frac{E[1-X]}{(1-p)^2} = \frac{p}{p^2} + \frac{1-p}{(1-p)^2} = \frac{1}{p(1-p)} $$
杰弗里斯先验正比于：
$$ \pi_J(p) \propto \sqrt{\frac{1}{p(1-p)}} = p^{-1/2}(1-p)^{-1/2} $$
这个形式对应于参数为 $\alpha=1/2, \beta=1/2$ 的 **Beta [分布](@entry_id:182848)**，即 $\text{Beta}(1/2, 1/2)$。这与均匀先验 $\pi(p) \propto 1$ (即 $\text{Beta}(1, 1)$ [分布](@entry_id:182848)) 不同。杰弗里斯先验在 $p$ 接近 0 或 1 的地方给予了更高的先验权重，反映了在极端情况下（几乎总是成功或失败）需要更多的数据来改变看法。

### [重参数化不变性](@entry_id:197540)：杰弗里斯先验的基石

现在我们来正式阐述并验证杰弗里斯先验最引以为傲的性质——[重参数化不变性](@entry_id:197540)。假设我们有一个新参数 $\phi = g(\theta)$，其中 $g$ 是一个光滑的、一对一的函数。根据[概率密度](@entry_id:175496)的变量变换法则，$\theta$ 的先验 $\pi_J(\theta)$ 变换到 $\phi$ 的先验应为：
$$ \pi_J(\phi) = \pi_J(\theta(\phi)) \left| \frac{d\theta}{d\phi} \right| $$
杰弗里斯先验的优越之处在于，直接为 $\phi$ 计算出的杰弗里斯先验 $\pi_J'(\phi) \propto \sqrt{I(\phi)}$ 与通过上述变换得到的 $\pi_J(\phi)$ 具有相同的函数形式。

这是因为费雪信息在重[参数化](@entry_id:272587)下遵循一个特定的变换法则：
$$ I(\phi) = I(\theta) \left( \frac{d\theta}{d\phi} \right)^2 $$
因此，直接为 $\phi$ 计算的杰弗里斯先验为：
$$ \pi_J'(\phi) \propto \sqrt{I(\phi)} = \sqrt{I(\theta) \left( \frac{d\theta}{d\phi} \right)^2} = \sqrt{I(\theta)} \left| \frac{d\theta}{d\phi} \right| \propto \pi_J(\theta) \left| \frac{d\theta}{d\phi} \right| $$
这与通过变量变换法则得到的结果完全一致。

**[不变性](@entry_id:140168)实例：[指数分布](@entry_id:273894)的率与[平均寿命](@entry_id:195236)**

让我们回到指数分布的例子来验证这一美妙的性质。我们已经知道失效率 $\lambda$ 的杰弗里斯先验是 $\pi_J(\lambda) \propto 1/\lambda$ [@problem_id:1624948]。现在考虑[平均寿命](@entry_id:195236) $\tau = 1/\lambda$。我们直接为 $\tau$ 计算杰弗里斯先验 [@problem_id:1925889] [@problem_id:1925871]。

以 $\tau$ 为参数的概率密度函数为 $f(t|\tau) = \frac{1}{\tau} \exp(-t/\tau)$。
[对数似然函数](@entry_id:168593)为 $\ln f(t|\tau) = -\ln \tau - t/\tau$。
[二阶导数](@entry_id:144508)为 $\frac{d^2}{d\tau^2} \ln f(t|\tau) = \frac{1}{\tau^2} - \frac{2t}{\tau^3}$。
对于该[参数化](@entry_id:272587)的[指数分布](@entry_id:273894)，我们有 $E[t] = \tau$。因此，[费雪信息](@entry_id:144784)为：
$$ I(\tau) = -E\left[\frac{1}{\tau^2} - \frac{2t}{\tau^3}\right] = -\left(\frac{1}{\tau^2} - \frac{2E[t]}{\tau^3}\right) = -\left(\frac{1}{\tau^2} - \frac{2\tau}{\tau^3}\right) = \frac{1}{\tau^2} $$
所以，$\tau$ 的杰弗里斯先验为：
$$ \pi_J(\tau) \propto \sqrt{I(\tau)} = \frac{1}{\tau} \quad (\text{for } \tau > 0) $$
现在我们来检验一致性。从 $\pi_J(\lambda) \propto 1/\lambda$ 出发，应用变量变换法则。因为 $\lambda = 1/\tau$，我们有 $|d\lambda/d\tau| = |-1/\tau^2| = 1/\tau^2$。
$$ \pi_J(\tau) = \pi_J(\lambda(\tau)) \left| \frac{d\lambda}{d\tau} \right| \propto \frac{1}{(1/\tau)} \cdot \frac{1}{\tau^2} = \tau \cdot \frac{1}{\tau^2} = \frac{1}{\tau} $$
两种方法得到的结果完全相同！这清晰地展示了杰弗里斯先验的[重参数化不变性](@entry_id:197540)，确保了无论我们选择哪种方便的参数化方式，最终的推断都是一致的。

### [位置参数](@entry_id:176482)与[尺度参数](@entry_id:268705)的先验

杰弗里斯先验在两类重要的参数族——位置族和尺度族——中表现出特别简洁和一致的形式。

#### [位置参数](@entry_id:176482) (Location Parameters)

一个**位置族**[分布](@entry_id:182848)的[概率密度函数](@entry_id:140610)可以写成 $p(x|\theta) = f(x-\theta)$ 的形式，其中 $\theta$ 是一个**[位置参数](@entry_id:176482)**，它仅仅将[分布](@entry_id:182848)的图形沿着[实数轴](@entry_id:147286)平移，而不改变其形状。例如，已知[方差](@entry_id:200758) $\sigma^2$ 的正态分布 $N(\mu, \sigma^2)$ 中的均值 $\mu$ 就是一个[位置参数](@entry_id:176482)。

对于任何正则的位置族，可以证明其费雪信息 $I(\theta)$ 是一个不依赖于 $\theta$ 的常数 [@problem_id:1925905]。这是因为在计算期望的积分中，可以通过变量代换 $z = x - \theta$ 将参数 $\theta$ 从积分中消除。因此，对于任何[位置参数](@entry_id:176482) $\theta$，其杰弗里斯先验总是：
$$ \pi_J(\theta) \propto \sqrt{I(\theta)} = \sqrt{\text{const}} \propto 1 $$
这对应于在整个[实数轴](@entry_id:147286)上的一个均匀先验。

以[方差](@entry_id:200758) $\sigma^2$ 已知的[正态分布](@entry_id:154414)均值 $\mu$ 为例 [@problem_id:1925902]，其对数似然的[二阶导数](@entry_id:144508)为 $\frac{\partial^2}{\partial \mu^2} \ln f(x|\mu) = -1/\sigma^2$，这是一个常数。因此，$I(\mu) = 1/\sigma^2$，其平方根也是常数，故 $\pi_J(\mu) \propto 1$。这为平移不变性的直觉提供了坚实的理论依据：我们对参数位置的先验知识不应随[坐标系](@entry_id:156346)原点的改变而改变。

#### [尺度参数](@entry_id:268705) (Scale Parameters)

一个**尺度族**[分布](@entry_id:182848)的[概率密度函数](@entry_id:140610)可以写成 $p(x|\sigma) = \frac{1}{\sigma}f(x/\sigma)$ 的形式，其中 $\sigma > 0$ 是一个**[尺度参数](@entry_id:268705)**，它控制[分布](@entry_id:182848)的展宽或压缩。[指数分布](@entry_id:273894)的平均寿命 $\tau$ 就是一个[尺度参数](@entry_id:268705)。

对于任何正则的[尺度参数](@entry_id:268705) $\sigma$，可以证明其杰弗里斯先验具有以下形式：
$$ \pi_J(\sigma) \propto \frac{1}{\sigma} $$
我们在[指数分布](@entry_id:273894)的平均寿命参数 $\tau$ 的例子中已经验证了这一点 [@problem_id:1925891]。另一个重要的例子是均值 $\mu$ 已知的正态分布的[方差](@entry_id:200758) $\sigma^2$ [@problem_id:1925894]。如果我们直接对参数 $\theta = \sigma^2$ 计算，可以得到 $I(\sigma^2) = 1/(2\sigma^4)$，因此先验为 $\pi_J(\sigma^2) \propto 1/\sigma^2$。这与对 $\sigma$ 的先验 $\pi_J(\sigma) \propto 1/\sigma$ 是完全一致的，通过变量变换即可验证：
$$ \pi_J(\sigma^2) = \pi_J(\sigma(\sigma^2)) \left| \frac{d\sigma}{d(\sigma^2)} \right| \propto \frac{1}{\sqrt{\sigma^2}} \cdot \frac{1}{2\sqrt{\sigma^2}} \propto \frac{1}{\sigma^2} $$
这种形式的先验通常也称为**对数均匀先验**，因为它等价于在 $\ln \sigma$ 上赋予均匀先验。这体现了[尺度不变性](@entry_id:180291)的思想：我们对尺度的先验知识不应依赖于度量单位的选择（例如，从米到厘米）。

### 实践中的考量与局限

尽管杰弗里斯先验具有优良的理论性质，但在实际应用中必须注意其几个关键[特征和](@entry_id:189446)潜在的陷阱。

#### [非正常先验](@entry_id:166066)与正常后验

我们推导出的许多杰弗里斯先验，如[位置参数](@entry_id:176482)的 $\pi(\theta) \propto 1$ 和[尺度参数](@entry_id:268705)的 $\pi(\sigma) \propto 1/\sigma$，都是**非正常的 (improper)**。这意味着它们在整个参数空间上的积分是发散的（即等于无穷大），因此它们本身并不是合法的[概率分布](@entry_id:146404)。

然而，[非正常先验](@entry_id:166066)在[贝叶斯分析](@entry_id:271788)中仍然非常有用。关键在于，只要结合了足够的数据（通过[似然函数](@entry_id:141927)），最终得到的**[后验分布](@entry_id:145605) $p(\theta|x) \propto p(x|\theta)\pi(\theta)$ 是正常的 (proper)**，即其[积分收敛](@entry_id:139742)为一。

例如，考虑为正态分布均值 $\mu$ （[方差](@entry_id:200758) $\sigma^2$ 已知）赋予[非正常先验](@entry_id:166066) $\pi(\mu) \propto 1$ [@problem_id:1925868]。在观测到一个数据点 $x$ 后，后验分布为：
$$ p(\mu|x) \propto \exp\left(-\frac{(x-\mu)^2}{2\sigma^2}\right) \cdot 1 = \exp\left(-\frac{(\mu-x)^2}{2\sigma^2}\right) $$
这正是以 $x$ 为均值、$\sigma^2$ 为[方差](@entry_id:200758)的正态分布的核。这是一个积分等于1的正常[概率分布](@entry_id:146404)。因此，尽管先验是概念上的抽象，但它成功地引导我们得到了一个关于 $\mu$ 的有效概率推断。只要后验分布是正常的，[贝叶斯推断](@entry_id:146958)的后续步骤（如计算[后验均值](@entry_id:173826)、[可信区间](@entry_id:176433)等）就是有效的。

#### 多维参数问题

当模型包含多个参数时，杰弗里斯先验的推广是 $\pi_J(\boldsymbol{\theta}) \propto \sqrt{\det(I(\boldsymbol{\theta}))}$，其中 $I(\boldsymbol{\theta})$ 是多维费雪信息矩阵。然而，这种直接的推广有时会产生与直觉不符且性质不佳的先验。

一个经典的例子是同时估计[正态分布](@entry_id:154414)的均值 $\mu$ 和标准差 $\sigma$ [@problem_id:1925853]。该模型的费雪信息矩阵是对角的，$I(\mu, \sigma) = \text{diag}(1/\sigma^2, 2/\sigma^2)$。其[行列式](@entry_id:142978)为 $\det(I(\mu,\sigma)) = 2/\sigma^4$。因此，多维杰弗里斯先验为：
$$ \pi_J(\mu, \sigma) \propto \sqrt{\frac{2}{\sigma^4}} \propto \frac{1}{\sigma^2} $$
这个结果令人不安。基于单参数的分析，我们期望[位置参数](@entry_id:176482) $\mu$ 的先验为 $\pi(\mu) \propto 1$，[尺度参数](@entry_id:268705) $\sigma$ 的先验为 $\pi(\sigma) \propto 1/\sigma$，组合起来应得到 $\pi(\mu, \sigma) = \pi(\mu)\pi(\sigma) \propto 1/\sigma$。显然，多维杰弗里斯先验 $1/\sigma^2$ 与此不同。在实践中，人们更倾向于使用 $1/\sigma$ 作为“标准”的[无信息先验](@entry_id:172418)。

为了解决这类问题，Berger 和 Bernardo 发展了**[参考先验](@entry_id:171432) (reference prior)** 理论。这是一种更为复杂的构造方法，它通过最大化先验和后验之间的预期[信息增益](@entry_id:262008)来定义先验。[参考先验](@entry_id:171432)通常能避免多维杰弗里斯先验的一些问题。对于[正态分布](@entry_id:154414)的例子，当 $\mu$ 是我们主要关心的参数而 $\sigma$ 是次要的“滋扰参数”时，[参考先验](@entry_id:171432)恰好是 $\pi_R(\mu, \sigma) \propto 1/\sigma$，这与直觉和实践标准相符 [@problem_id:1925853]。

#### [杰弗里斯-林德利悖论](@entry_id:175448)

杰弗里斯先验在参数估计中表现出色，但在**[假设检验](@entry_id:142556)**，特别是涉及点[零假设](@entry_id:265441)（例如 $H_0: \theta = \theta_0$）的检验中，会引发严重问题。这就是著名的**[杰弗里斯-林德利悖论](@entry_id:175448) (Jeffreys-Lindley paradox)**。

悖论的核心在于，当使用[非正常先验](@entry_id:166066)来检验点[零假设](@entry_id:265441)时，[贝叶斯因子](@entry_id:143567) $B_{01} = p(\text{data}|H_0) / p(\text{data}|H_1)$ 会极度偏向于[零假设](@entry_id:265441)，尤其是在大样本情况下。

考虑一个场景：检验正态均值是否为零，即 $H_0: \mu = 0$ 对阵 $H_1: \mu \neq 0$ [@problem_id:1925849]。在 $H_1$ 下，我们为 $\mu$ 赋予一个先验，比如一个弥散但正常的先验 $N(0, \tau^2)$。悖论的一个表现形式是，即使我们获得的数据在频率派框架下具有固定的“边际显著性”（例如，$z$ 统计量始终为 $z_c=1.96$，对应 $p=0.05$），随着样本量 $n$ 的增大，支持 $H_0$ 的[贝叶斯因子](@entry_id:143567) $B_{01}$ 也会趋向于无穷大。可以证明，在这种情况下，$B_{01}$ 的增长速度与 $\sqrt{n}$ 成正比。

这意味着，对于一个固定的、看似“显著”的效应，只要样本量足够大，贝叶斯检验总会得出“强烈支持[零假设](@entry_id:265441)”的结论。其直观解释是，一个非正常的（或非常弥散的）先验将其总概率质量分散在一个无限（或极大）的[参数空间](@entry_id:178581)上，这使得任何特定点（如 $\mu=0$）附近的备择假设区域所获得的[先验概率](@entry_id:275634)极小，从而在与点[零假设](@entry_id:265441)的竞争中处于极端不利的地位。

这个悖论告诫我们：**[非正常先验](@entry_id:166066)（包括杰弗里斯先验）不应被直接用于计算涉及点零假设的[贝叶斯因子](@entry_id:143567)或进行[模型选择](@entry_id:155601)**。在这类问题中，必须使用正常的、经过审慎考虑的[先验分布](@entry_id:141376)。

总之，杰弗里斯先验是贝叶斯统计中一个强大而优雅的工具，它为构造“客观”先验提供了基于信息论的坚实基础。其[重参数化不变性](@entry_id:197540)是一个极其重要的理论性质。然而，作为使用者，我们必须清醒地认识到它的非正常性质、在多维问题中的潜在缺陷以及在假设检验中的严重局限性，从而在实践中明智地加以运用。