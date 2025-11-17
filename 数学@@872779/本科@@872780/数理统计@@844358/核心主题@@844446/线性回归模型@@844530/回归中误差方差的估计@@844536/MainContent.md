## 引言
在数据分析领域，回归模型是理解和预测变量之间关系的不可或缺的工具。然而，任何模型都无法完美地捕捉现实。模型预测与实际观测之间的差距体现在误差项中，而这种误差的变异性——即[误差方差](@entry_id:636041)——是衡量模型固有不确定性的一个基本指标。准确地估计此[方差](@entry_id:200758)并非一个纯粹的技术细节；它对于评估模型的可靠性、进行有效的[统计推断](@entry_id:172747)和做出明智的决策至关重要。本文旨在全面探讨[误差方差](@entry_id:636041)的估计，以回答一个核心问题：我们如何可靠地量化[回归模型](@entry_id:163386)中的不确定性？

通过接下来的三个章节，您将对这一关键概念建立起坚实的理解。第一章 **“原理与机制”** 将奠定理论基础，定义[误差方差](@entry_id:636041)并推导其关键估计量，如[均方误差](@entry_id:175403)(MSE)。本章将深入探讨无偏性等重要的统计性质，并探索置信区间的构建方法。第二章 **“应用与跨学科联系”** 将从理论转向实践，展示[误差方差](@entry_id:636041)的估计如何被用于比较模型、处理[异方差性](@entry_id:136378)等非理想数据状况，以及它如何在不同科学领域的高级方法中扮演关键角色。最后，**“动手实践”** 章节将通过一系列有针对性的练习来巩固您的知识，挑战您将这些原理应用于具体的统计问题。这段学习旅程将使您不仅掌握计算方法，更能批判性地理解和应用[误差方差](@entry_id:636041)的概念于您自己的数据分析工作中。

## 原理与机制

在[回归分析](@entry_id:165476)中，我们旨在通过一个或多个预测变量来解释或预测一个响应变量。然而，任何模型都无法完美捕捉现实世界的复杂性。模型预测值与实际观测值之间的差异，即误差，是不可避免的。这些误差的变异性，通常用[误差方差](@entry_id:636041) $\sigma^2$ 来量化，是衡量模型固有不确定性或随机性的一个核心指标。准确估计 $\sigma^2$ 对于评估模型的[拟合优度](@entry_id:637026)、进行[假设检验](@entry_id:142556)以及构建[预测区间](@entry_id:635786)至关重要。本章将深入探讨估计误差[方差](@entry_id:200758)的基本原理与核心机制。

### 定义与解释

在线性回归模型 $Y = X\beta + \epsilon$ 中，$\epsilon$ 代表了无法被[模型解释](@entry_id:637866)的随机误差向量。我们通常假设这些误差项的期望为零，且具有一个恒定的[方差](@entry_id:200758) $\sigma^2$。这个 $\sigma^2$ 是一个未知的总体参数，代表了数据点围绕真实回归线的平均离散程度。由于我们无法直接观测到真实的误差 $\epsilon_i$，我们转而使用它们的样本对应物——残差 $e_i = Y_i - \hat{Y}_i$ 进行估计，其中 $\hat{Y}_i$ 是由[最小二乘法](@entry_id:137100)得到的拟合值。

所有残差的平方和被称为**[残差平方和](@entry_id:174395) (Residual Sum of Squares, RSS)**，也常被称为**[误差平方和](@entry_id:149299) (Sum of Squared Errors, SSE)**，其定义为：
$$
\text{SSE} = \sum_{i=1}^{n} e_i^2 = \sum_{i=1}^{n} (Y_i - \hat{Y}_i)^2
$$

直觉上，SSE 似乎是估计总体[方差](@entry_id:200758) $\sigma^2$ 的一个良好起点，因为它汇总了模型的所有“错误”。然而，直接使用 SSE 会低估 $\sigma^2$。为了得到一个无偏估计，我们必须将 SSE 除以其对应的**自由度 (degrees of freedom)**。在包含 $p$ 个待估参数（例如，对于 $Y = \beta_0 + \beta_1 X_1 + \dots + \beta_{p-1} X_{p-1}$ 的[多元回归](@entry_id:144007)，包含截距项在内共有 $p$ 个参数）的回归模型中，误差自由度为 $n-p$。因此，$\sigma^2$ 的[无偏估计量](@entry_id:756290)，即**[均方误差](@entry_id:175403) (Mean Squared Error, MSE)** 定义为：
$$
\hat{\sigma}^2 = \text{MSE} = \frac{\text{SSE}}{n-p}
$$

这个公式是[回归分析](@entry_id:165476)中[方差分析](@entry_id:275547)([ANOVA](@entry_id:275547))表的核心组成部分 [@problem_id:1915652]。自由度 $n-p$ 的直观解释是：我们从 $n$个独立的观测值开始，但在估计模型的 $p$ 个参数（$\beta_0, \beta_1, \dots, \beta_{p-1}$）时，我们“消耗”了 $p$ 个自由度。这是因为残差 $e_i$ 并非完全独立，它们受到 $p$ 个[线性约束](@entry_id:636966)（例如，在简单[线性回归](@entry_id:142318)中，$\sum e_i = 0$ 和 $\sum e_i x_i = 0$）。因此，只有 $n-p$ 个自由度可用于[估计误差](@entry_id:263890)的[方差](@entry_id:200758)。

虽然 MSE 是 $\sigma^2$ 的一个重要估计，但它的单位是响应变量单位的平方，这使得解释不够直观。为了解决这个问题，我们通常使用其平方根，即**[残差标准误](@entry_id:167844) (Residual Standard Error, RSE)**，有时也记为 $S$ 或 $\hat{\sigma}$：
$$
S = \sqrt{\text{MSE}} = \sqrt{\frac{\text{SSE}}{n-p}}
$$

RSE 的单位与响应变量 $Y$ 相同，它可以被解释为观测值偏离拟合回归线的“典型”或“平均”距离。

例如，假设一个机器人实验室正在测试一款新型无人机的续航能力 [@problem_id:1915669]。他们记录了5次不同载重 ($W$, 单位：克)下的[飞行时间](@entry_id:159471) ($T$, 单位：分钟)，并拟合了回归直线 $\hat{T} = 31.5 - 0.066 W$。通过计算每次飞行的预测飞行时间 $\hat{T}_i$ 和实际[飞行时间](@entry_id:159471) $T_i$ 之间的差异（即残差 $e_i$），我们可以得到[残差平方和](@entry_id:174395) SSE。假设计算得出 $\text{SSE} = 0.90$。在这个简单线性回归模型中，我们估计了两个参数（截距 $\beta_0$ 和斜率 $\beta_1$），所以 $p=2$。样本量 $n=5$，因此自由度为 $n-p = 5-2 = 3$。那么，[误差方差](@entry_id:636041)的估计为：
$$
\hat{\sigma}^2 = \text{MSE} = \frac{0.90}{3} = 0.30 \text{ (分钟)}^2
$$
[残差标准误](@entry_id:167844)为：
$$
S = \sqrt{0.30} \approx 0.548 \text{ 分钟}
$$
这个 $0.548$ 分钟的 RSE 值意味着，对于给定的载重，模型的预测[飞行时间](@entry_id:159471)与实际观测到的飞行时间之间的典型偏差大约是半分钟。这个数值为工程师提供了一个关于模型预测精度的具体、可解释的度量。

### 估计量的无偏性

一个优秀的[点估计量](@entry_id:171246)应具备无偏性，即其[期望值](@entry_id:153208)等于它所估计的总体参数。现在我们来严格证明 MSE 确实是 $\sigma^2$ 的[无偏估计量](@entry_id:756290)，即 $E[\text{MSE}] = \sigma^2$。这个证明揭示了为何分母必须是 $n-p$ 而非其他值 [@problem_id:1915699] [@problem_id:1915692]。

我们将[回归模型](@entry_id:163386)写成矩阵形式 $Y = X\beta + \epsilon$，其中 $Y$ 是 $n \times 1$ 的响应向量，$X$ 是 $n \times p$ 的[设计矩阵](@entry_id:165826)，$\beta$ 是 $p \times 1$ 的系数向量，$\epsilon$ 是 $n \times 1$ 的误差向量，满足 $E[\epsilon] = 0$ 和 $\text{Var}(\epsilon) = \sigma^2 I_n$。

[最小二乘估计](@entry_id:262764)的拟合值向量为 $\hat{Y} = X\hat{\beta} = X(X^T X)^{-1}X^T Y$。我们可以定义一个重要的矩阵，即**[帽子矩阵](@entry_id:174084) (hat matrix)** $H = X(X^T X)^{-1}X^T$，它将观测向量 $Y$ “戴上帽子”变为拟合向量 $\hat{Y}$。因此，$\hat{Y} = HY$。

[残差向量](@entry_id:165091)可以表示为：
$$
e = Y - \hat{Y} = Y - HY = (I - H)Y
$$
这里 $I$ 是 $n \times n$ 的[单位矩阵](@entry_id:156724)。我们将矩阵 $M = I-H$ 称为**[残差生成](@entry_id:162977)矩阵 (residual-maker matrix)**。利用 $Y = X\beta + \epsilon$ 和一个关键性质 $MX = (I-H)X = X - HX = X-X=0$，我们可以将残差向量表示为：
$$
e = M(X\beta + \epsilon) = MX\beta + M\epsilon = 0 + M\epsilon = M\epsilon
$$
这个结果非常深刻：它表明残差仅仅是真实误差 $\epsilon$ 的[线性变换](@entry_id:149133)，与真实系数 $\beta$ 无关。

现在我们可以计算 SSE 的[期望值](@entry_id:153208)。注意到 $M$ 是对称且幂等的 ($M^T=M, M^2=M$)：
$$
\text{SSE} = e^T e = (M\epsilon)^T(M\epsilon) = \epsilon^T M^T M \epsilon = \epsilon^T M \epsilon
$$
利用二次型期望的迹技巧，我们有 $E[\epsilon^T A \epsilon] = \text{tr}(A \cdot \text{Var}(\epsilon)) + E[\epsilon]^T A E[\epsilon]$。由于 $E[\epsilon]=0$ 且 $\text{Var}(\epsilon) = \sigma^2 I_n$，该公式简化为 $E[\epsilon^T M \epsilon] = \text{tr}(M \sigma^2 I_n) = \sigma^2 \text{tr}(M)$。
$$
E[\text{SSE}] = E[\epsilon^T M \epsilon] = \sigma^2 \text{tr}(M)
$$
[帽子矩阵](@entry_id:174084) $H$ 也是对称幂等的，它的迹等于它的秩，即[设计矩阵](@entry_id:165826) $X$ 的列数 $p$。因此，$\text{tr}(H) = p$。于是：
$$
\text{tr}(M) = \text{tr}(I - H) = \text{tr}(I) - \text{tr}(H) = n - p
$$
将此结果代回，我们得到 SSE 的[期望值](@entry_id:153208)：
$$
E[\text{SSE}] = (n-p)\sigma^2
$$
最后，根据 MSE 的定义和[期望的线性](@entry_id:273513)性质：
$$
E[\text{MSE}] = E\left[\frac{\text{SSE}}{n-p}\right] = \frac{1}{n-p} E[\text{SSE}] = \frac{(n-p)\sigma^2}{n-p} = \sigma^2
$$
这就完成了证明。MSE 的[期望值](@entry_id:153208)恰好是 $\sigma^2$，所以它是[误差方差](@entry_id:636041)的[无偏估计量](@entry_id:756290)。这个推导清晰地表明，分母中的“$-p$”是为抵消因估计 $p$ 个模型参数而导致的对 SSE 的系统性低估所做的精确修正。

### [误差方差](@entry_id:636041)的[区间估计](@entry_id:177880)

[点估计](@entry_id:174544) $\hat{\sigma}^2$ 给出了[方差](@entry_id:200758)的最佳单值猜测，但它本身是一个[随机变量](@entry_id:195330)，会随样本而变。为了量化这种不确定性，我们需要构造一个**[置信区间](@entry_id:142297) (confidence interval)**。这需要我们了解 $\hat{\sigma}^2$ 的[抽样分布](@entry_id:269683)。

在标准[线性模型](@entry_id:178302)假设（误差独立、零均值、同[方差](@entry_id:200758)）的基础上，如果我们增加一个**[正态性假设](@entry_id:170614)**，即误差项服从[正态分布](@entry_id:154414) $\epsilon_i \sim N(0, \sigma^2)$，我们就可以推导出 SSE 的精确[分布](@entry_id:182848)。一个关键的统计学定理（Cochran定理的一个推论）告诉我们， pivotal quantity $\frac{\text{SSE}}{\sigma^2}$ 服从一个自由度为 $n-p$ 的**[卡方分布](@entry_id:165213) ($\chi^2$)** [@problem_id:1915686]。
$$
\frac{\text{SSE}}{\sigma^2} = \frac{(n-p)\text{MSE}}{\sigma^2} \sim \chi^2_{n-p}
$$
这个量的[分布](@entry_id:182848)不依赖于任何未知参数（除了它自身所包含的 $\sigma^2$），因此它是一个理想的[枢轴量](@entry_id:168397)，可以用来为 $\sigma^2$ 构建[置信区间](@entry_id:142297)。

一个 $(1-\alpha) \times 100\%$ 的[置信区间](@entry_id:142297)是通过找到两个卡方分布的临界值 $\chi^2_{1-\alpha/2, n-p}$ 和 $\chi^2_{\alpha/2, n-p}$ 来构造的，这两个值分别截断了[分布](@entry_id:182848)的左右 $\alpha/2$ 尾部面积。我们有：
$$
P\left( \chi^2_{1-\alpha/2, n-p} \le \frac{\text{SSE}}{\sigma^2} \le \chi^2_{\alpha/2, n-p} \right) = 1 - \alpha
$$
通过对不等式进行代数变换以分离 $\sigma^2$，我们得到 $\sigma^2$ 的[置信区间](@entry_id:142297)：
$$
\left[ \frac{\text{SSE}}{\chi^2_{\alpha/2, n-p}}, \frac{\text{SSE}}{\chi^2_{1-\alpha/2, n-p}} \right]
$$
值得注意的是，由于[卡方分布](@entry_id:165213)是不对称的，所以这个[置信区间](@entry_id:142297)关于[点估计](@entry_id:174544) $\hat{\sigma}^2$ 也是不对称的。

区间[上界](@entry_id:274738)与下界之比，$\frac{\chi^2_{\alpha/2, n-p}}{\chi^2_{1-\alpha/2, n-p}}$，仅取决于样本量 $n$、参数个数 $p$ 和[置信水平](@entry_id:182309) $\alpha$，而与具体的 SSE 值无关 [@problem_id:1915702]。这个比率揭示了置信区间的相对宽度，并显示出对于给定的[模型复杂度](@entry_id:145563)和[置信水平](@entry_id:182309)，我们对[方差估计](@entry_id:268607)的不确定性有多大。例如，在一个 $n=30, p=6$ 的实验中，$\sigma^2$ 的95%置信区间的[上界](@entry_id:274738)大约是下界的 $3.174$ 倍，这表明即使有30个观测值，对真实[误差方差](@entry_id:636041)的估计仍存在相当大的不确定性。

### 估计方法的比较：无偏估计 vs. 最大似然估计

MSE 是通过矩法思想（匹配样本矩与[总体矩](@entry_id:170482)）和无偏性原则得到的，但它并非唯一的估计方法。另一个强大的估计[范式](@entry_id:161181)是**[最大似然估计](@entry_id:142509) (Maximum Likelihood Estimation, MLE)**。在误差服从正态分布的假设下，我们可以写出数据的[似然函数](@entry_id:141927)，并通过最大化该函数来求解所有模型参数，包括 $\sigma^2$。

对于简单[线性回归](@entry_id:142318)模型，[对数似然函数](@entry_id:168593)为：
$$
\ell(\beta_0, \beta_1, \sigma^2) = -\frac{n}{2}\ln(2\pi) - \frac{n}{2}\ln(\sigma^2) - \frac{1}{2\sigma^2}\sum_{i=1}^{n}(Y_i - \beta_0 - \beta_1 x_i)^2
$$
最大化此函数，我们首先发现 $\beta_0$ 和 $\beta_1$ 的MLE与最小二乗估计值 $\hat{\beta}_0, \hat{\beta}_1$ 相同。然后将它们代入并对 $\sigma^2$ 求导并设为零，可解得 $\sigma^2$ 的[最大似然估计量](@entry_id:163998) [@problem_id:1915662]：
$$
\hat{\sigma}^2_{ML} = \frac{1}{n} \sum_{i=1}^{n}(Y_i - \hat{\beta}_0 - \hat{\beta}_1 x_i)^2 = \frac{\text{SSE}}{n}
$$
这个估计量与[无偏估计量](@entry_id:756290) MSE 非常相似，唯一的区别在于分母是 $n$ 而不是 $n-p$（在简单回归中是 $n-2$）。由于 $n-p  n$，MLE 的值总是小于[无偏估计量](@entry_id:756290)。我们可以计算其[期望值](@entry_id:153208)来评估其偏误：
$$
E[\hat{\sigma}^2_{ML}] = E\left[\frac{\text{SSE}}{n}\right] = \frac{1}{n}E[\text{SSE}] = \frac{(n-p)\sigma^2}{n} = \left(1 - \frac{p}{n}\right)\sigma^2
$$
这表明 MLE 是一个**有偏**估计量，它系统性地低估了真实的[误差方差](@entry_id:636041)。

那么，我们应该总是选择[无偏估计量](@entry_id:756290)吗？不一定。评价估计量好坏的另一个重要标准是**[均方误差](@entry_id:175403) (Mean Squared Error)**，注意此处的MSE是指“估计量的均方误差”，不要与前述的“[均方误差](@entry_id:175403)MSE估计量”混淆。一个估计量 $\hat{\theta}$ 对参数 $\theta$ 的均方误差定义为：
$$
\text{MSE}(\hat{\theta}) = E[(\hat{\theta} - \theta)^2] = \text{Var}(\hat{\theta}) + (\text{Bias}(\hat{\theta}))^2
$$
它同时惩罚了[估计量的方差](@entry_id:167223)（不稳定性）和偏误（系统性误差）。在某些情况下，一个略有偏误的估计量可能因为其[方差](@entry_id:200758)更小，而具有更低的总体[均方误差](@entry_id:175403)。

让我们比较一下[无偏估计量](@entry_id:756290) $S^2 = \frac{\text{SSE}}{n-p}$ 和 MLE $\hat{\sigma}^2_{ML} = \frac{\text{SSE}}{n}$ 的均方误差 [@problem_id:1915689]。利用 $\frac{\text{SSE}}{\sigma^2} \sim \chi^2_{n-p}$ 的性质，我们知道 $E[\frac{\text{SSE}}{\sigma^2}] = n-p$ 和 $\text{Var}(\frac{\text{SSE}}{\sigma^2}) = 2(n-p)$。
对于[无偏估计量](@entry_id:756290) $S^2$（以简单回归 $p=2$ 为例）：
$$
\text{MSE}(S^2) = \text{Var}(S^2) + 0^2 = \text{Var}\left(\frac{\text{SSE}}{n-2}\right) = \frac{1}{(n-2)^2}\text{Var}(\text{SSE}) = \frac{\sigma^4}{(n-2)^2}\text{Var}\left(\frac{\text{SSE}}{\sigma^2}\right) = \frac{2(n-2)\sigma^4}{(n-2)^2} = \frac{2\sigma^4}{n-2}
$$
对于MLE $\hat{\sigma}^2_{ML}$：
$$
\text{MSE}(\hat{\sigma}^2_{ML}) = \text{Var}(\hat{\sigma}^2_{ML}) + (\text{Bias}(\hat{\sigma}^2_{ML}))^2 = \text{Var}\left(\frac{\text{SSE}}{n}\right) + \left(-\frac{2\sigma^2}{n}\right)^2 = \frac{2(n-2)\sigma^4}{n^2} + \frac{4\sigma^4}{n^2} = \frac{2n\sigma^4}{n^2} = \frac{2\sigma^4}{n}
$$
比较两者，我们发现比率 $\frac{\text{MSE}(\hat{\sigma}^2_{ML})}{\text{MSE}(S^2)} = \frac{2\sigma^4/n}{2\sigma^4/(n-2)} = \frac{n-2}{n}  1$。这意味着，尽管MLE是有偏的，但它具有更小的均方误差。它用引入微小的偏误为代价，换来了更低的[方差](@entry_id:200758)，从而在“平均”意义上更接近真实值 $\sigma^2$。这个例子是经典的**偏误-[方差](@entry_id:200758)权衡 (bias-variance tradeoff)** 的体现。在实践中，由于无偏性是一个非常理想的统计性质，且当 $n$ 很大时两者差异很小，所以标准回归输出通常报告[无偏估计量](@entry_id:756290) $S^2$。

### 模型假设的重要性

$\hat{\sigma}^2 = \frac{\text{SSE}}{n-p}$ 的良好性质（如无偏性）以及基于它的推断（如[置信区间](@entry_id:142297)）都严格依赖于一系列模型假设。当这些假设被违背时，我们对[误差方差](@entry_id:636041)的估计可能会出现严重偏差，导致错误的科学结论。

#### [模型设定错误](@entry_id:170325)

一个常见的错误是**[模型设定错误](@entry_id:170325) (model misspecification)**，即选择了错误的函数形式来描述变量间的关系。例如，假设数据的真实关系是二次的，但分析师错误地拟合了一个简单的[线性模型](@entry_id:178302) [@problem_id:1915676]。
$$
\text{真实模型: } Y_i = \beta_0 + \beta_1 x_i + \beta_2 x_i^2 + \epsilon_i \quad (\beta_2 \ne 0)
$$
$$
\text{拟合模型: } Y_i = \alpha_0 + \alpha_1 x_i + u_i
$$
在这种情况下，[线性模型](@entry_id:178302)拟合得到的残差 $e_i$ 不再仅仅反映[随机误差](@entry_id:144890) $\epsilon_i$。它们还必须“吸收”由模型形式不匹配造成的**系统性偏差 (lack of fit)**。具体来说，真实模型中的 $\beta_2 x_i^2$ 项是[线性模型](@entry_id:178302)无法捕捉的结构性信息，这部分未被解释的变异会被错误地归入残差中。

我们可以精确地量化这种影响。从错误的简单[线性模型](@entry_id:178302)中计算出的[方差估计](@entry_id:268607)量 $\hat{\sigma}_{SLR}^2$，其[期望值](@entry_id:153208)为：
$$
E[\hat{\sigma}_{SLR}^2] = \sigma^2 + \frac{\beta_2^2}{n-2} \left\|(I - P_X)x^{\circ 2}\right\|^2
$$
其中 $x^{\circ 2}$ 是 $x_i^2$ 组成的向量，$P_X$ 是简单线性模型的[设计矩阵](@entry_id:165826)所对应的[投影矩阵](@entry_id:154479)。因为 $\beta_2 \ne 0$ 且二次项 $x^{\circ 2}$ 不能被常数项和 $x$ [线性表示](@entry_id:139970)，所以右边的第二项是一个严格的正数。这意味着：
$$
E[\hat{\sigma}_{SLR}^2]  \sigma^2
$$
结论是，当[模型设定错误](@entry_id:170325)（即“[欠拟合](@entry_id:634904)”）时，[误差方差](@entry_id:636041)的估计量会被系统性地**高估**。模型看起来比实际上“更嘈杂”，因为模型的结构性缺陷被错误地当作了随机噪声。这会降低我们对模型预测能力的信心，并可能掩盖预测变量的真实显著性。

#### [异方差性](@entry_id:136378)

另一个至关重要的假设是**[同方差性](@entry_id:634679) (homoscedasticity)**，即所有误差项具有相同的[方差](@entry_id:200758) $\text{Var}(\epsilon_i) = \sigma^2$。如果这个假设不成立，我们就遇到了**[异方差性](@entry_id:136378) (heteroscedasticity)**，即 $\text{Var}(\epsilon_i) = \sigma_i^2$，每个观测的[误差方差](@entry_id:636041)都可能不同。

在[异方差性](@entry_id:136378)的情况下，标准OLS估计的[方差](@entry_id:200758)公式 $s^2 = \frac{\text{SSE}}{n-p}$ 的[期望值](@entry_id:153208)会发生什么变化？它还是某个有意义的“平均”[方差](@entry_id:200758)的无偏估计吗？答案是否定的 [@problem_id:1915684]。其[期望值](@entry_id:153208)变为：
$$
E[s^2] = \frac{1}{n-p} \sum_{i=1}^{n} (1-h_{ii})\sigma_i^2
$$
其中 $h_{ii}$ 是[帽子矩阵](@entry_id:174084) $H$ 的第 $i$ 个对角元素，被称为观测 $i$ 的**[杠杆值](@entry_id:172567) (leverage)**。这个表达式揭示了几个严重的问题：
1.  $E[s^2]$ 不再等于一个简单的常数 $\sigma^2$ 或所有 $\sigma_i^2$ 的简单平均值 $\frac{1}{n}\sum \sigma_i^2$。
2.  这个[期望值](@entry_id:153208)是一个关于真实个体[方差](@entry_id:200758) $\sigma_i^2$的复杂加权平均，权重为 $(1-h_{ii})$。[高杠杆点](@entry_id:167038)（$x_i$ 远离其均值）对 $E[s^2]$ 的贡献权重 $(1-h_{ii})$ 反而更小。
3.  由于 $E[s^2]$ 的值依赖于 $\sigma_i^2$ 的未知模式与预测变量 $x_i$ [分布](@entry_id:182848)的特定组合，我们无法预测 $s^2$ 会高估还是低估“平均”[方差](@entry_id:200758)。它成为了一个有偏且不稳定的估计量。

因此，当[同方差性](@entry_id:634679)假设被违背时，标准[误差[方差估](@entry_id:167285)计](@entry_id:268607)量 $s^2$ 便失去了其清晰的解释和良好的统计性质。所有基于它的标准推断，例如对[回归系数](@entry_id:634860)的 $t$检验和 $F$检验，以及[置信区间](@entry_id:142297)和[预测区间](@entry_id:635786)，都变得不再可靠。这凸显了在应用回归模型后进行残差诊断以检验模型假设（包括[同方差性](@entry_id:634679)）的极端重要性，并在必要时采用对[异方差性](@entry_id:136378)稳健的估计方法。