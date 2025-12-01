## 引言
在数据驱动的生物医学研究时代，从海量的基因组序列、临床试验数据和流行病学调查中提取可靠的科学结论，是研究人员面临的核心挑战。基于似然的推断（Likelihood-based Inference）正是应对这一挑战的基石，它为连接观测数据与底层生物学过程的[统计模型](@entry_id:755400)提供了一套强大而统一的理论框架。然而，许多研究人员虽然在日常工作中应用着基于似然的方法，却可能对其背后的核心原理、数学性质以及在复杂场景下的扩展缺乏系统性的理解。

本文旨在填补这一知识鸿沟，系统性地阐述基于似然的推断与[最大似然估计](@entry_id:142509)（Maximum Likelihood Estimation, MLE）的完整图景。读者将从理论的源头出发，逐步深入到前沿的应用领域。在“原理与机制”一章中，我们将奠定坚实的理论基础，详细解析[似然函数](@entry_id:141927)的定义、[最大似然估计](@entry_id:142509)的求解过程及其优良的统计性质。随后，在“应用与跨学科连接”一章中，我们将展示这些理论如何在现实世界中大放异彩，探讨其在基因组学建模、生存分析、[潜变量模型](@entry_id:174856)以及现代因果推断中的关键作用。最后，通过“动手实践”部分，读者将有机会将理论知识应用于解决具体的编程问题，从而巩固和深化所学。

让我们首先从第一章“原理与机制”开始，深入探索这一统计推断核心思想的精髓。

## 原理与机制

本章将深入探讨基于似然的推断的核心原理与关键机制。我们将从似然函数的严格定义出发，阐明其在统计推断中的独特角色，然后系统地介绍最大似然估计（Maximum Likelihood Estimation, MLE）的原理、求解方法及其重要的统计性质。最后，我们将讨论如何利用似然函数进行参数的[区间估计](@entry_id:177880)与假设检验，包括处理复杂的滋扰参数（nuisance parameters）的策略。

### [似然函数](@entry_id:141927)的定义与理解

在统计建模中，我们通常假设观测到的数据是一个[随机过程](@entry_id:268487)的实现，该过程由一个或多个未知参数决定的概率分布所描述。似然推断的核心思想是，利用观测到的数据，反过来评估不同参数值的“合理性”或“貌似程度”。

#### 似然：参数合理性的度量

给定一组[独立同分布](@entry_id:169067)（i.i.d.）的观测数据 $x_{1}, x_{2}, \dots, x_{n}$，假设它们来自一个由参数 $\theta$ 决定的[概率密度函数](@entry_id:140610)（PDF）或概率质量函数（PMF）$f(x; \theta)$。这组数据的[联合概率](@entry_id:266356)密度（或质量）函数为：

$$
P(x_{1:n}; \theta) = \prod_{i=1}^{n} f(x_i; \theta)
$$

这个函数，当被视为数据 $x_{1:n}$ 的函数（即 $\theta$ 固定）时，描述了在给定参数下观测到特定数据集的概率（密度）。然而，在[统计推断](@entry_id:172747)中，我们已经拥有了数据，而未知的是参数 $\theta$。此时，我们将视角转换，将这个表达式看作是参数 $\theta$ 的函数，数据 $x_{1:n}$ 则被视为固定的。这个关于 $\theta$ 的函数就被称为**[似然函数](@entry_id:141927) (likelihood function)**，记作 $L(\theta \mid x_{1:n})$。

$$
L(\theta \mid x_{1:n}) = \prod_{i=1}^{n} f(x_i; \theta)
$$

**似然函数** $L(\theta \mid x_{1:n})$ 度量了在已观测到数据 $x_{1:n}$ 的条件下，参数 $\theta$ 取不同值的相对合理性。某个参数值 $\theta_A$ 的似然值是另一个参数值 $\theta_B$ 的两倍，意味着在我们的模型下，数据由 $\theta_A$ 生成的可能性是由 $\theta_B$ 生成的两倍。

一个关键且微妙的区别是，**似然函数不是参数 $\theta$ 的一个概率分布** [@problem_id:4578016]。作为一个关于 $\theta$ 的函数，它在[参数空间](@entry_id:178581)上的积分（或求和）通常不为1。例如，在一个基因组学应用中，我们对一个单[核苷](@entry_id:195320)酸变异（SNV）进行检测，得到 $n$ 次独立的伯努利试验结果 $x_1, \dots, x_n$（$x_i=1$ 表示检测到变异，$x_i=0$ 表示未检测到），其成功概率为 $p$。该模型的似然函数为：

$$
L(p \mid x_{1:n}) = p^{\sum x_i} (1-p)^{n - \sum x_i}
$$

如果我们对 $p$ 在其定义域 $[0,1]$ 上积分，会得到 $\int_{0}^{1} p^k (1-p)^{n-k} dp = \frac{k!(n-k)!}{(n+1)!}$（其中 $k = \sum x_i$），这个值通常不等于1。因此，不能将似然值直接解释为参数取该值的概率。在频率学派的框架中，参数 $\theta$被视为一个固定的未知常数，而非随机变量，因此它本身没有概率分布。似然函数是评估这个未知常数可[能值](@entry_id:187992)的一种工具。

#### 对数似然函数及其数值稳定性

在实际应用中，直接计算[似然函数](@entry_id:141927) $L(\theta)$ 常常会遇到数值计算的挑战，尤其是当样本量 $n$ 很大时。由于似然函数是多个概率（通常是小于1的数）的连乘积，其结果可能非常小，以至于超出标准[浮点数](@entry_id:173316)（如[IEEE 754](@entry_id:138908)[双精度](@entry_id:636927)）能够表示的范围，导致**数值[下溢](@entry_id:635171) (numerical underflow)** [@problem_id:4578098]。例如，在一个大型队列研究中，若有 $n=10^4$ 个独立的伯努利观测，即使每次观测的概率是 $0.5$，总的似然值 $(0.5)^{10000} \approx 10^{-3010}$ 也远小于计算机能表示的最小正数，计算结果会被错误地记为0。

为了解决这个问题并简化数学处理，我们通常使用**[对数似然函数](@entry_id:168593) (log-likelihood function)**，记作 $\ell(\theta)$：

$$
\ell(\theta \mid x_{1:n}) = \ln L(\theta \mid x_{1:n}) = \ln \left( \prod_{i=1}^{n} f(x_i; \theta) \right) = \sum_{i=1}^{n} \ln f(x_i; \theta)
$$

使用[对数似然函数](@entry_id:168593)有三大好处：
1.  **[数值稳定性](@entry_id:146550)**：将连乘变为连加，避免了数值[下溢](@entry_id:635171)或上溢的问题。对于前述例子，$\ell(p=0.5) = 10000 \times \ln(0.5) \approx -6931.47$，这是一个在计算机中可以精确表示的常规数值。
2.  **数学便利性**：求和形式的导数计算远比乘积形式的导数计算简单，这在后续的最大化求解中至关重要。
3.  **保持最值位置不变**：自然对数函数 $\ln(\cdot)$ 是一个严格单调递增函数，因此最大化 $L(\theta)$ 等价于最大化 $\ell(\theta)$。它们在相同的参数值 $\theta$ 处取得最大值。

### 最大似然估计原理

[似然函数](@entry_id:141927)为我们提供了一种评估参数值合理性的方法。基于此，一个非常自然的估计未知参数 $\theta$ 的策略是：选择那个能使观测数据出现的可能性（似然）达到最大的参数值。这就是**最大似然估计 (Maximum Likelihood Estimation, MLE)** 的核心思想。

#### [最大似然估计量](@entry_id:163998)

**[最大似然估计量](@entry_id:163998) (Maximum Likelihood Estimator, MLE)** $\hat{\theta}_{MLE}$ 是使得似然函数（或[对数似然函数](@entry_id:168593)）达到其最大值的参数值：

$$
\hat{\theta}_{MLE} = \underset{\theta \in \Theta}{\arg\max} \, L(\theta \mid x_{1:n}) = \underset{\theta \in \Theta}{\arg\max} \, \ell(\theta \mid x_{1:n})
$$

其中 $\Theta$ 是[参数空间](@entry_id:178581)。

#### 似然函数的重要性质

在寻找MLE的过程中，我们可以利用[似然函数](@entry_id:141927)的一些关键性质来简化计算 [@problem_id:4578125]。

1.  **比例性与常数项的取舍**：[似然函数](@entry_id:141927)只在相差一个不依赖于参数 $\theta$ 的正常[数乘](@entry_id:155971)子下是唯一的。也就是说，如果 $L^*(\theta) = c(x) \cdot L(\theta)$，其中 $c(x)>0$ 且不依赖于 $\theta$，那么 $L^*(\theta)$ 和 $L(\theta)$ 会在同一点达到最大值。因此，在为**单个模型**进行参数估计时，我们可以从似然函数中舍去任何不含参数 $\theta$ 的乘法因子。

    例如，在分析[RNA测序](@entry_id:178187)数据时，若基因的读数计数 $X_i$ 被建模为独立的泊松分布 $X_i \sim \text{Poisson}(s_i \lambda)$，其中 $s_i$ 是已知的库大小因子，$\lambda$ 是未知的表达率。其[联合概率质量函数](@entry_id:184238)为 $\prod_{i=1}^n \frac{(s_i \lambda)^{x_i} \exp(-s_i \lambda)}{x_i!}$。在估计 $\lambda$ 时，我们可以将其重写为：
    $$
    L(\lambda \mid \mathbf{x}) = \left( \prod_{i=1}^n \frac{s_i^{x_i}}{x_i!} \right) \cdot \lambda^{\sum x_i} \exp(-\lambda \sum s_i)
    $$
    其中第一项括号内的部分仅与数据 $\mathbf{x}$ 和已知常数 $s_i$ 有关，与待估参数 $\lambda$ 无关。因此，为了最大化[似然函数](@entry_id:141927)，我们可以忽略这一项，只关注与 $\lambda$ 相关的部分，即 $L_{prop}(\lambda) \propto \lambda^{\sum x_i} \exp(-\lambda \sum s_i)$ [@problem_id:4578125]。

    **重要警告**：当需要在**不同模型间**进行比较时（例如，使用[赤池信息准则](@entry_id:139671)AIC或[贝叶斯信息准则](@entry_id:142416)BIC），这些常数项**绝对不能**舍去，因为它们的值依赖于模型的结构，对于模型的绝对拟合优度至关重要。

2.  **参数依赖的支撑集**：如果概率密度函数的支撑集（即函数值非零的区域）依赖于参数 $\theta$，那么定义支撑集的指示函数项不能被舍去。例如，若数据来自均匀分布 $U[0, \theta]$，其[似然函数](@entry_id:141927)为 $L(\theta) = \theta^{-n} \prod_{i=1}^n \mathbf{1}\{0 \le x_i \le \theta\}$。这个表达式可以写成 $L(\theta) = \theta^{-n} \mathbf{1}\{\theta \ge \max(x_i)\}$。[指示函数](@entry_id:186820) $\mathbf{1}\{\theta \ge \max(x_i)\}$ 明确依赖于 $\theta$，它将参数空间限制在 $[\max(x_i), \infty)$。若错误地舍弃它，最大化 $\theta^{-n}$ 将没有意义。保留该项后，我们知道 $\theta^{-n}$ 在其允许的定义域内是单调递减的，因此似然在 $\theta$ 取最小值，即 $\hat{\theta}_{MLE} = \max(x_i)$ 时达到最大 [@problem_id:4578125]。

3.  **[参数化](@entry_id:265163)不变性 (Reparameterization Invariance)**：最大似然估计有一个非常优美的性质，即它对参数的重新[参数化](@entry_id:265163)是保持不变的。如果 $\hat{\theta}$ 是 $\theta$ 的MLE，而 $\phi = g(\theta)$ 是一个函数（不一定是可逆的），那么 $\phi$ 的MLE就是 $\hat{\phi} = g(\hat{\theta})$。这个性质之所以成立，是因为似然函数本身被看作是参数空间上的一个函数剖面，其最大值的位置不随坐标系的改变而改变。这与概率密度函数在变量变换时需要乘以一个[雅可比行列式](@entry_id:137120)来保证积分守恒是截然不同的 [@problem_id:4578125]。

#### 参数可识别性：一个基本前提

进行有意义的参数估计的一个基本前提是**参数可识别性 (identifiability)**。一个参数模型被称为可识别的，是指从参数到概率分布的映射是单射的。也就是说，如果 $\theta_1 \neq \theta_2$，那么它们所决定的概率分布 $P_{\theta_1}$ 和 $P_{\theta_2}$ 也必须不同。如果模型不可识别，意味着存在多个不同的参数值可以生成完全相同的观测数据分布，从而导致似然函数在这些不同的参数点上取值完全相同 [@problem_id:4578019]。

生物信息学中一个经典的不可识别性例子是**[高斯混合模型](@entry_id:634640) (Gaussian Mixture Model)**。例如，在分析[循环肿瘤DNA](@entry_id:274724)（ctDNA）片段长度分布时，常用一个双组分[高斯混合模型](@entry_id:634640)来区分凋亡和坏死来源的DNA片段。其密度函数为：
$$
f(x \mid \theta) = \pi \cdot \mathcal{N}(x \mid \mu_1, \sigma_1^2) + (1-\pi) \cdot \mathcal{N}(x \mid \mu_2, \sigma_2^2)
$$
其中参数 $\theta = (\pi, \mu_1, \sigma_1, \mu_2, \sigma_2)$。考虑一个“标签交换”后的参数 $\theta' = (1-\pi, \mu_2, \sigma_2, \mu_1, \sigma_1)$。由于加法是可交换的，我们发现 $f(x \mid \theta) = f(x \mid \theta')$ 对所有 $x$ 成立。这意味着，只要 $(\pi, \mu_1, \sigma_1) \neq (1-\pi, \mu_2, \sigma_2)$，我们就找到了两个不同的参数点，它们产生了完全相同的概率分布和似然函数值。

这种不可识别性导致似然函数曲面存在多个等价的[全局最大值](@entry_id:174153)，使得MLE的解不唯一。为了解决这个问题，通常需要施加额外的约束来打破对称性，例如，强制要求组分均值有序，如 $\mu_1  \mu_2$。另一种更强大的方法是引入额外的、能够区分不同组分的协变量信息（例如，特定于凋亡或坏死来源的DNA片段的甲基化标签），这可以在模型层面恢复可识别性 [@problem_id:4578019]。

### 求解[最大似然估计](@entry_id:142509)的机制

一旦我们写出了[对数似然函数](@entry_id:168593) $\ell(\theta)$，下一步就是找到其最大值。主要有两种方法：解析方法和数值方法。

#### 基于微积分的方法：得分函数与费雪信息

对于性质良好的函数，其[最大值点](@entry_id:634610)通常出现在导数为零的[驻点](@entry_id:136617)。

1.  **得分函数 (Score Function)**：对数似然函数关于参数 $\theta$ 的[一阶导数](@entry_id:749425)（梯度）被称为**[得分函数](@entry_id:164520)**，记为 $U(\theta)$：
    $$
    U(\theta) = \frac{\partial \ell(\theta)}{\partial \theta}
    $$
    在满足一定[正则性条件](@entry_id:166962)下，MLE $\hat{\theta}$ 满足得分方程 $U(\hat{\theta}) = 0$。此外，[得分函数](@entry_id:164520)在真实参数 $\theta_0$ 处的期望为零，即 $E_{\theta_0}[U(\theta_0)] = 0$。这表明，平均而言，[对数似然函数](@entry_id:168593)在真实参数处的斜率为零。

2.  **[费雪信息](@entry_id:144784) (Fisher Information)**：对数似然函数在多大程度上将参数集中在某个值附近，可以用其曲率来衡量。**[费雪信息](@entry_id:144784)** $I(\theta)$ 是衡量数据中关于未知参数 $\theta$ 含有多少信息的量。对于单参数模型，它有两种等价的定义：
    $$
    I(\theta) = E\left[ \left( \frac{\partial \ell(\theta)}{\partial \theta} \right)^2 \right] = \text{Var}(U(\theta))
    $$
    $$
    I(\theta) = -E\left[ \frac{\partial^2 \ell(\theta)}{\partial \theta^2} \right]
    $$
    第一种定义表明，费雪信息是[得分函数](@entry_id:164520)方差。得分函数的波动越大，表明数据对参数值的微小变化越敏感，信息量越大。第二种定义表明，费雪信息是负的[对数似然函数](@entry_id:168593)二阶导数的[期望值](@entry_id:150961)。一个大的[费雪信息](@entry_id:144784)值意味着对数似然函数在最大值附近非常“尖锐”，曲率很大，这使得最大值的位置被精确地确定下来，从而[参数估计](@entry_id:139349)的方差较小。

    以 $n$ 个来自泊松分布 $\text{Poisson}(\theta)$ 的i.i.d.观测为例，对数似然函数为 $\ell(\theta) = (\sum x_i) \ln(\theta) - n\theta - \sum \ln(x_i!)$。其得分函数为 $U(\theta) = \frac{\sum x_i}{\theta} - n$。二阶导数为 $\frac{\partial^2 \ell(\theta)}{\partial \theta^2} = -\frac{\sum x_i}{\theta^2}$。因此，总的[费雪信息](@entry_id:144784)为 $I(\theta) = -E[-\frac{\sum X_i}{\theta^2}] = \frac{E[\sum X_i]}{\theta^2} = \frac{n E[X_i]}{\theta^2} = \frac{n\theta}{\theta^2} = \frac{n}{\theta}$ [@problem_id:4578085]。[费雪信息](@entry_id:144784)与样本量 $n$ 成正比，与参数值 $\theta$ 成反比。

#### [数值优化方法](@entry_id:752811)：[牛顿-拉弗森法](@entry_id:140620)

在许多复杂的模型中（如广义线性模型、混合模型等），得分方程 $U(\theta)=0$ 没有解析解。此时，我们需要借助[数值优化](@entry_id:138060)算法来迭代地逼近MLE。**[牛顿-拉弗森法](@entry_id:140620) ([Newton-Raphson](@entry_id:177436) method)** 是一种常用且高效的方法。

该方法的基本思想是，在当前估计值 $\theta^{(t)}$ 附近，用一个二次函数来近似对数似然函数 $\ell(\theta)$，然后找到这个二次函数的[最大值点](@entry_id:634610)作为下一次的迭代值 $\theta^{(t+1)}$。这等价于对[得分函数](@entry_id:164520) $S(\theta) \equiv U(\theta)$ 进行一阶泰勒展开来寻找其根 [@problem_id:4578102]：
$$
S(\theta) \approx S(\theta^{(t)}) + S'(\theta^{(t)})(\theta - \theta^{(t)})
$$
令 $S(\theta^{(t+1)}) = 0$，并注意到 $S'(\theta) = \frac{d^2\ell}{d\theta^2}$ 是对数似然函数的二阶导数（Hessian矩阵的负值），我们得到更新规则：
$$
\theta^{(t+1)} = \theta^{(t)} - \left[ \frac{\partial^2 \ell(\theta^{(t)})}{\partial \theta^2} \right]^{-1} \frac{\partial \ell(\theta^{(t)})}{\partial \theta}
$$
这个迭代过程持续进行，直到 $\theta^{(t)}$ 收敛。在理想情况下（例如，初始值足够接近真实解，且Hessian矩阵在解附近非奇异），[牛顿法](@entry_id:139922)具有**二次[收敛速度](@entry_id:146534)**，非常快。

在统计中，一个相关的算法是**费雪得分法 (Fisher Scoring)**，它用观测到的Hessian矩阵的[期望值](@entry_id:150961)，即负的[费雪信息](@entry_id:144784) $-I(\theta^{(t)})$，来代替公式中的Hessian矩阵。对于某些模型（如广义线性模型中的典则连接函数），[观测信息](@entry_id:165764)和[期望信息](@entry_id:163261)是相等的，此时[牛顿法](@entry_id:139922)和费雪得分法是等价的。

例如，在分析肿瘤活检中的变异[等位基因频率](@entry_id:146872)时，我们将 $n$ 个读数中观测到 $y$ 个变异读数建模为[二项分布](@entry_id:141181) $Y \sim \text{Binomial}(n, p)$。为了将参数 $p \in (0,1)$ 变换到整个实数轴，我们使用logit链接函数进行重[参数化](@entry_id:265163)：$\eta = \ln(\frac{p}{1-p})$，即 $p = \frac{1}{1+\exp(-\eta)}$。针对参数 $\eta$ 的[对数似然函数](@entry_id:168593)，其得分函数为 $S(\eta) = y - np$，Hessian为 $H(\eta) = -np(1-p)$。[牛顿法](@entry_id:139922)的更新步骤就是 $\eta^{(t+1)} = \eta^{(t)} + \frac{y - np^{(t)}}{np^{(t)}(1-p^{(t)})}$ [@problem_id:4578102]。

### 最大似然估计的性质

[最大似然估计](@entry_id:142509)之所以在统计学中占据核心地位，是因为它在一系列温和的“[正则性条件](@entry_id:166962)”下拥有优良的大样本性质。

#### 一致性与[正则性条件](@entry_id:166962)

**一致性 (Consistency)** 是指当样本量 $n \to \infty$ 时，MLE $\hat{\theta}_n$ 会依概率收敛于真实的参数值 $\theta_0$。这意味着只要数据足够多，我们就能以任意高的精度估计出真实参数。

MLE的一致性并非无条件成立，它依赖于一系列**[正则性条件](@entry_id:166962) (regularity conditions)** [@problem_id:4578074]。这些条件确保了[似然函数](@entry_id:141927)具有良好的数学性质，其核心思想是保证样本平均对数似然函数 $\frac{1}{n}\ell(\theta)$ 能一致地收敛于其期望 $E_{\theta_0}[\ln f(X; \theta)]$，并且这个期望函数在真实参数 $\theta_0$ 处取得唯一的[全局最大值](@entry_id:174153)。关键的[正则性条件](@entry_id:166962)包括：
1.  **参数可识别性**：如前所述，这是唯一估计的基础。
2.  **[参数空间](@entry_id:178581)**：[参数空间](@entry_id:178581) $\Theta$ 是紧集（或可以通过论证将MLE的搜索范围限制在一个紧集内）。
3.  **似然[函数的连续性](@entry_id:193744)**：对数似然函数 $\ln f(x; \theta)$ 是 $\theta$ 的连续函数。
4.  **可积的[优势函数](@entry_id:635295)**：存在一个函数 $g(x)$ 使得 $|\ln f(x;\theta)| \le g(x)$ 对所有 $\theta$ 成立，且 $E_{\theta_0}[g(X)]  \infty$。这保证了强大数定律可以应用于对数似然函数。

对于许多标准分布族，如[指数族](@entry_id:263444)（包括正态分布、泊松分布、二项分布、[指数分布](@entry_id:273894)等），这些[正则性条件](@entry_id:166962)通常都是满足的 [@problem_id:4578074]。

#### [渐近正态性](@entry_id:168464)与效率

除了收敛到真实值，MLE的分布在大样本下也具有明确的形式。**[渐近正态性](@entry_id:168464) (Asymptotic Normality)** 指出，在[正则性条件](@entry_id:166962)下，MLE的分布会随着样本量的增加而逼近一个正态分布：

$$
\sqrt{n}(\hat{\theta}_n - \theta_0) \xrightarrow{d} \mathcal{N}\left(0, I_1(\theta_0)^{-1}\right)
$$

其中 $\xrightarrow{d}$ 表示[依分布收敛](@entry_id:275544)，$I_1(\theta_0)$ 是单个观测的费雪信息。这个定理是进行大样本推断的基石。它告诉我们：
-   $\hat{\theta}_n$ 是渐近无偏的（中心在 $\theta_0$）。
-   $\hat{\theta}_n$ 的方差约为 $\frac{1}{n I_1(\theta_0)} = I_n(\theta_0)^{-1}$，其中 $I_n$ 是 $n$ 个样本的总[费雪信息](@entry_id:144784)。方差随着样本量 $n$ 的增加而减小，且与[费雪信息](@entry_id:144784)成反比，这与我们对[费雪信息](@entry_id:144784)含义的直观理解相符。

更进一步，MLE还具有**[渐近效率](@entry_id:168529) (Asymptotic Efficiency)**，即它渐近地达到了[Cramér-Rao下界](@entry_id:154412)。这意味着在所有渐近无偏的估计量中，MLE拥有最小的[渐近方差](@entry_id:269933)。从某种意义上说，它是大样本下“最好”的估计量。

### 基于似然的[统计推断](@entry_id:172747)

获得了参数的点估计 $\hat{\theta}$ 及其[渐近分布](@entry_id:272575)后，我们就可以进行更复杂的[统计推断](@entry_id:172747)，如构建[置信区间](@entry_id:138194)和进行假设检验。

#### [Delta方法](@entry_id:276272)：估计量函数的分布

在生物医学数据分析中，我们常常对参数的某个函数 $g(\theta)$ 更感兴趣，例如，对数风险比 $\ln(\text{HR})$ 或方差稳定化变换后的参数。**[Delta方法](@entry_id:276272)**提供了一种计算 $\hat{\theta}$ 的函数 $g(\hat{\theta})$ 的[渐近分布](@entry_id:272575)的通用工具 [@problem_id:4578136]。

其原理基于[泰勒展开](@entry_id:145057)。如果 $\sqrt{n}(\hat{\theta}_n - \theta_0) \xrightarrow{d} \mathcal{N}(0, \sigma^2)$ 并且函数 $g(\cdot)$ 在 $\theta_0$ 处可微且导数 $g'(\theta_0) \neq 0$，则：
$$
\sqrt{n}(g(\hat{\theta}_n) - g(\theta_0)) \xrightarrow{d} \mathcal{N}\left(0, [g'(\theta_0)]^2 \sigma^2\right)
$$
对于MLE，我们已知 $\sigma^2 = I_1(\theta_0)^{-1}$。因此，$g(\hat{\theta})$ 的[渐近方差](@entry_id:269933)为 $[g'(\theta_0)]^2 I_1(\theta_0)^{-1}$。例如，对于泊松分布的MLE $\hat{\lambda}$，我们知道 $\sqrt{n}(\hat{\lambda} - \lambda) \xrightarrow{d} \mathcal{N}(0, \lambda)$。如果我们关心 $\ln(\hat{\lambda})$ 的分布，取 $g(\lambda)=\ln(\lambda)$，则 $g'(\lambda) = 1/\lambda$。应用Delta方法，$\sqrt{n}(\ln(\hat{\lambda}) - \ln(\lambda))$ 的[渐近方差](@entry_id:269933)为 $(1/\lambda)^2 \cdot \lambda = 1/\lambda$ [@problem_id:4578136]。

#### [置信区间](@entry_id:138194)构建

1.  **Wald[置信区间](@entry_id:138194)**：直接利用MLE的[渐近正态性](@entry_id:168464)，一个 $(1-\alpha)$ 的Wald[置信区间](@entry_id:138194)为 $\hat{\theta} \pm z_{1-\alpha/2} \cdot \text{se}(\hat{\theta})$，其中 $\text{se}(\hat{\theta}) = \sqrt{I_n(\hat{\theta})^{-1}}$ 是[标准误](@entry_id:635378)的估计值。这种方法简单直观，但在小样本或参数接近边界时表现不佳。

2.  **基于[似然比](@entry_id:170863)的[置信区间](@entry_id:138194)**：这是一种更可靠和推荐的方法，其理论基础是**[威尔克斯定理](@entry_id:169826) (Wilks' Theorem)**。该定理指出，对于一个待检验的假设 $H_0: \theta = \theta_0$，**[似然比](@entry_id:170863)统计量 (likelihood ratio statistic)**：
    $$
    W(\theta_0) = 2(\ell(\hat{\theta}) - \ell(\theta_0))
    $$
    在大样本下近似服从自由度为参数维数的卡方分布（对于单参数，即 $\chi^2_1$ 分布）。

    基于此，一个 $(1-\alpha)$ 的[置信区间](@entry_id:138194)可以被构造为所有“无法被似然比检验拒绝”的参数值 $\theta_0$ 的集合 [@problem_id:4578130]：
    $$
    \{ \theta : 2(\ell(\hat{\theta}) - \ell(\theta)) \le \chi^2_{1, 1-\alpha} \}
    $$
    其中 $\chi^2_{1, 1-\alpha}$ 是 $\chi^2_1$ 分布的 $(1-\alpha)$ [分位数](@entry_id:178417)（例如，对于95%置信度，该值为3.84）。这个区间的端点需要通过数值方法求解方程 $2(\ell(\hat{\theta}) - \ell(\theta)) = \chi^2_{1, 1-\alpha}$。相比[Wald区间](@entry_id:173132)，似然比区间的形状由数据自适应决定，不对称性更强，且对参数变换保持不变，通常具有更好的覆盖率表现。

#### 对滋扰参数的处理：[剖面似然](@entry_id:269700)

在许多实际问题中，模型可能包含多个参数 $\theta = (\psi, \lambda)$，但我们只对其中一部分参数 $\psi$（**兴趣参数 (parameter of interest)**）感兴趣，而其余的 $\lambda$（**滋扰参数 (nuisance parameters)**）只是为了构建一个更真实的模型所必需的。

直接对[联合似然](@entry_id:750952)函数 $L(\psi, \lambda)$ 进行推断是困难的。**[剖面似然](@entry_id:269700) (profile likelihood)** 是一种优雅地处理滋扰参数的有效方法 [@problem_id:4578070]。其思想是，对于每一个给定的兴趣参数值 $\psi$，我们通过最大化[似然函数](@entry_id:141927)来“优化掉”滋扰参数 $\lambda$。

对于给定的 $\psi$，我们先找到使似然最大化的 $\lambda$ 值，记为 $\hat{\lambda}(\psi) = \arg\max_{\lambda} L(\psi, \lambda)$。然后，将这个值代回原似然函数，得到只关于 $\psi$ 的[剖面似然](@entry_id:269700)函数 $L_p(\psi)$：
$$
L_p(\psi) = L(\psi, \hat{\lambda}(\psi))
$$
例如，对于来自正态分布 $\mathcal{N}(\mu, \sigma^2)$ 的数据，如果我们只关心均值 $\mu$（兴趣参数），而方差 $\sigma^2$ 是滋扰参数。对于任意固定的 $\mu$，使似然最大化的 $\sigma^2$ 是 $\hat{\sigma}^2(\mu) = \frac{1}{n}\sum(x_i - \mu)^2$。将其代入正态[似然函数](@entry_id:141927)，即可得到 $\mu$ 的[剖面似然](@entry_id:269700) $L_p(\mu)$ [@problem_id:4578070]。

[剖面似然](@entry_id:269700)函数 $L_p(\psi)$ 在很多方面可以像一个真正的似然函数一样使用。例如，[剖面似然](@entry_id:269700)函数的最大化点就是 $\psi$ 的全局MLE $\hat{\psi}$。更重要的是，基于[剖面似然](@entry_id:269700)的[似然比](@entry_id:170863)统计量 $2(\ell_p(\hat{\psi}) - \ell_p(\psi_0))$ 在大样本下也近似服从[卡方分布](@entry_id:165213)，因此可以用于构建关于 $\psi$ 的[置信区间](@entry_id:138194)和进行[假设检验](@entry_id:142556)，即使在存在滋扰参数的情况下。