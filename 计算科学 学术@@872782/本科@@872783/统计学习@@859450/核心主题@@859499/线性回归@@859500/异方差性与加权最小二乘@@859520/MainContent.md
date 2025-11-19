## 引言
在[线性回归分析](@entry_id:166896)中，我们常常假设模型的误差具有恒定的[方差](@entry_id:200758)，即“[同方差性](@entry_id:634679)”。然而，在现实世界的数据中，从金融市场的波动到生物实验的测量，误差的变异性往往随着预测变量的变化而变化——这种现象被称为“[异方差性](@entry_id:136378)”。[异方差性](@entry_id:136378)的存在不仅会降低我们模型估计的效率，还会使基于标准统计检验的结论变得不可靠，从而构成了一个亟待解决的统计难题。[加权最小二乘法](@entry_id:177517)（WLS）提供了一个强大而优雅的框架来应对这一挑战，但其背后的原理和广泛的应用价值往往需要更深入的探讨。

本文旨在系统地揭示[异方差性](@entry_id:136378)的本质，并全面介绍[加权最小二乘法](@entry_id:177517)。通过学习本文，您将能够理解WLS如何通过加权来纠正[异方差性](@entry_id:136378)，掌握其作为数据变换的巧妙机制及其几何解释；探索WLS如何在化学、生物、金融和机器学习等多个领域解决实际问题，并与其他统计概念产生深刻联系；以及将理论知识转化为处理真实世界数据的实用技能。

文章结构如下：**第一章：原理与机制**，深入探讨WLS的核心思想与工作机制；**第二章：应用与跨学科联系**，展示WLS在不同学科中的实际效用；**第三章：动手实践**，通过具体案例巩固理论学习。现在，让我们从[异方差性](@entry_id:136378)问题的根源出发，深入学习[加权最小二乘法](@entry_id:177517)。

## 原理与机制

在[线性回归](@entry_id:142318)的经典假设中，我们假定误差项的[方差](@entry_id:200758)是恒定的，即[同方差性](@entry_id:634679)（homoscedasticity）。然而，在许多实际应用中，数据点的[方差](@entry_id:200758)会随着预测变量的值而变化，这种现象被称为[异方差性](@entry_id:136378)（heteroscedasticity）。本章将深入探讨[异方差性](@entry_id:136378)的后果，并详细介绍[加权最小二乘法](@entry_id:177517)（Weighted Least Squares, WLS）作为一种有效的应对策略。我们将从其基本原理出发，揭示其内在机制，并讨论其在实践中的应用、诊断方法及重要注意事项。

### [异方差性](@entry_id:136378)问题

在[线性模型](@entry_id:178302) $y_i = \mathbf{x}_i^\top \boldsymbol{\beta} + \varepsilon_i$ 中，[异方差性](@entry_id:136378)意味着误差项 $\varepsilon_i$ 的[方差](@entry_id:200758)依赖于预测变量 $\mathbf{x}_i$，即 $\operatorname{Var}(\varepsilon_i \mid \mathbf{x}_i) = \sigma_i^2$。这一现象违背了[普通最小二乘法](@entry_id:137121)（Ordinary Least Squares, OLS）的关键假设之一。

[异方差性](@entry_id:136378)对 OLS 估计会产生两个主要后果：
1.  **效率损失**：尽管在异[方差](@entry_id:200758)存在的情况下，只要均值模型设定正确（即 $E[\varepsilon_i \mid \mathbf{x}_i] = 0$），OLS 估计量 $\hat{\boldsymbol{\beta}}_{\text{OLS}}$ 仍然是无偏和一致的 [@problem_id:3127984]，但它不再是[最佳线性无偏估计量](@entry_id:137602)（Best Linear Unbiased Estimator, BLUE）。这意味着存在其他线性[无偏估计量](@entry_id:756290)，其[方差比](@entry_id:162608) OLS 估计量更小。
2.  **推断失效**：OLS [方差](@entry_id:200758)的标准计算公式 $\sigma^2(\mathbf{X}^\top \mathbf{X})^{-1}$ 在异[方差](@entry_id:200758)情况下是错误的和有偏的。因此，基于此公式构建的置信区间、t检验和 F 检验都将变得不可靠，可能导致错误的科学结论。

面对[异方差性](@entry_id:136378)，一种常见的“修补”策略是继续使用 OLS 估计量，但采用异[方差](@entry_id:200758)稳健的[标准误](@entry_id:635378)（Heteroscedasticity-Consistent Standard Errors），例如“三明治”估计量（sandwich estimator）[@problem_id:3128046]。这种方法可以修正[统计推断](@entry_id:172747)，但无法解决 OLS 估计量的效率损失问题。要从根本上解决问题，我们需要一种新的估计方法，它能在模型构建阶段就考虑[方差](@entry_id:200758)的[异质性](@entry_id:275678)。这正是[加权最小二乘法](@entry_id:177517)（WLS）的核心任务。

### [加权最小二乘法](@entry_id:177517)：核心思想

WLS 的基本思想非常直观：在拟合模型时，我们应该给予更可靠（即[方差](@entry_id:200758)更小）的观测点更大的权重，而给予更不可靠（即[方差](@entry_id:200758)更大）的观测点更小的权重。

我们可以通过一个简单的例子来理解这个原理 [@problem_id:3128020]。假设我们有 $n$ 个独立的传感器，用于测量一个未知的恒定物理量 $\mu$。每个传感器 $i$ 的读数为 $y_i$，其测量误差服从正态分布 $\varepsilon_i \sim \mathcal{N}(0, \sigma_i^2)$。因此，模型为 $y_i = \mu + \varepsilon_i$。由于每个传感器的精度不同，它们的[误差方差](@entry_id:636041) $\sigma_i^2$ 也各不相同。我们如何最优地整合这些读数来估计 $\mu$ 呢？

从[最大似然估计](@entry_id:142509)（MLE）的角度来看，整个数据集的[对数似然函数](@entry_id:168593)为：
$$
\ell(\mu, \{\sigma_i^2\}) = -\frac{n}{2}\ln(2\pi) - \frac{1}{2}\sum_{i=1}^n \ln(\sigma_i^2) - \frac{1}{2}\sum_{i=1}^n \frac{(y_i - \mu)^2}{\sigma_i^2}
$$
为了最大化该似然函数以求得 $\mu$ 的估计值，我们只需最小化其最后一项，即 $\sum_{i=1}^n \frac{1}{\sigma_i^2}(y_i - \mu)^2$。令权重 $w_i = 1/\sigma_i^2$，这等价于最小化加权[残差平方和](@entry_id:174395)（Weighted Sum of Squared Residuals）：
$$
S(\mu) = \sum_{i=1}^n w_i (y_i - \mu)^2
$$
对 $S(\mu)$ 关于 $\mu$ 求导并令其为零，我们得到[最优估计量](@entry_id:176428)：
$$
\hat{\mu} = \frac{\sum_{i=1}^n w_i y_i}{\sum_{i=1}^n w_i}
$$
这个结果正是读数 $y_i$ 的**加权平均值**，其中每个读数的权重 $w_i$ 与其[方差](@entry_id:200758)成反比。这个简单的例子揭示了 WLS 的本质：它通过赋予高精度观测（低[方差](@entry_id:200758)）更大的话语权，来获得对未知参数最有效的估计。

### WLS 估计量及其性质

将这一思想推广到一般[线性回归](@entry_id:142318)模型，WLS 的目标是寻找参数 $\boldsymbol{\beta}$ 以最小化加权[残差平方和](@entry_id:174395) [@problem_id:3128045]：
$$
J(\boldsymbol{\beta}) = \sum_{i=1}^n w_i (y_i - \mathbf{x}_i^\top \boldsymbol{\beta})^2 = (\mathbf{y} - \mathbf{X}\boldsymbol{\beta})^\top \mathbf{W} (\mathbf{y} - \mathbf{X}\boldsymbol{\beta})
$$
其中 $\mathbf{W}$ 是一个[对角矩阵](@entry_id:637782)，其对角线元素为权重 $w_i > 0$。

通过对 $J(\boldsymbol{\beta})$ 求梯度并使其为零，我们得到 WLS 的**正规方程**（normal equations）：
$$
(\mathbf{X}^\top \mathbf{W} \mathbf{X}) \hat{\boldsymbol{\beta}}_{\text{WLS}} = \mathbf{X}^\top \mathbf{W} \mathbf{y}
$$
如果矩阵 $\mathbf{X}^\top \mathbf{W} \mathbf{X}$ 可逆，则 WLS 估计量为：
$$
\hat{\boldsymbol{\beta}}_{\text{WLS}} = (\mathbf{X}^\top \mathbf{W} \mathbf{X})^{-1} \mathbf{X}^\top \mathbf{W} \mathbf{y}
$$
**广义[高斯-马尔可夫定理](@entry_id:138437)**（Generalized Gauss-Markov Theorem）指出，如果我们选择的权重与真实[误差方差](@entry_id:636041)成反比，即 $w_i \propto 1/\sigma_i^2$，那么 WLS 估计量 $\hat{\boldsymbol{\beta}}_{\text{WLS}}$ 是所有线性[无偏估计量](@entry_id:756290)中[方差](@entry_id:200758)最小的，即 $\hat{\boldsymbol{\beta}}_{\text{WLS}}$ 是[最佳线性无偏估计量](@entry_id:137602)（BLUE）[@problem_id:3128045]。

一个重要的性质是，WLS 估计量对权重的绝对尺度不敏感 [@problem_id:3127967]。如果我们将所有权重乘以一个正常数 $c > 0$，即 $w_i \to c \cdot w_i$，WLS 估计量保持不变：
$$
\hat{\boldsymbol{\beta}}(c\mathbf{W}) = (\mathbf{X}^\top (c\mathbf{W}) \mathbf{X})^{-1} \mathbf{X}^\top (c\mathbf{W}) \mathbf{y} = \frac{1}{c}(\mathbf{X}^\top \mathbf{W} \mathbf{X})^{-1} c(\mathbf{X}^\top \mathbf{W} \mathbf{y}) = \hat{\boldsymbol{\beta}}(\mathbf{W})
$$
这表明，决定 WLS 估计结果的是**相对权重**，而非其绝对大小。

### WLS 的机制：数据变换视角

要深刻理解 WLS 的工作原理，最有效的方法是将其视为对原始数据进行变换后应用 OLS 的过程 [@problem_id:3128045]。

考虑 WLS 的[目标函数](@entry_id:267263)：
$$
J(\boldsymbol{\beta}) = \sum_{i=1}^n w_i (y_i - \mathbf{x}_i^\top \boldsymbol{\beta})^2 = \sum_{i=1}^n \left(\sqrt{w_i}y_i - \sqrt{w_i}\mathbf{x}_i^\top \boldsymbol{\beta}\right)^2
$$
如果我们定义一组新的变换后的变量：
$$
\tilde{y}_i = \sqrt{w_i} y_i \quad \text{和} \quad \tilde{\mathbf{x}}_i = \sqrt{w_i} \mathbf{x}_i
$$
那么 WLS 的[目标函数](@entry_id:267263)就变成了最小化 $\sum_{i=1}^n (\tilde{y}_i - \tilde{\mathbf{x}}_i^\top \boldsymbol{\beta})^2$。这正是对变换后数据 $(\tilde{\mathbf{y}}, \tilde{\mathbf{X}})$ 进行 OLS 估计的目标函数。

这个变换的精妙之处在于它对误差项的影响。原始模型的误差项为 $\varepsilon_i$，变换后的模型误差项为 $\tilde{\varepsilon}_i = \sqrt{w_i} \varepsilon_i$。其[方差](@entry_id:200758)为：
$$
\operatorname{Var}(\tilde{\varepsilon}_i) = \operatorname{Var}(\sqrt{w_i} \varepsilon_i) = w_i \operatorname{Var}(\varepsilon_i) = w_i \sigma_i^2
$$
如果我们明智地选择权重为真实[方差](@entry_id:200758)的倒数，即 $w_i = 1/\sigma_i^2$，那么变换后误差项的[方差](@entry_id:200758)将变为：
$$
\operatorname{Var}(\tilde{\varepsilon}_i) = \frac{1}{\sigma_i^2} \cdot \sigma_i^2 = 1
$$
这意味着，通过乘以 $\sqrt{w_i}$ 这个看似简单的操作，我们成功地将一个异[方差](@entry_id:200758)模型转化为了一个同[方差](@entry_id:200758)模型。在新模型中，所有误差项的[方差](@entry_id:200758)均为常数 1。此时，应用 OLS 是完全合理的，并且根据标准的[高斯-马尔可夫定理](@entry_id:138437)，它将产生[最佳线性无偏估计量](@entry_id:137602)。

这个变换视角也凸显了 WLS 相对于一些启发式方法的优越性。例如，有人可能认为可以通过复制“好”的观测点（低[方差](@entry_id:200758)）来增加其影响，然后对扩增的数据集运行 OLS [@problem_id:3128044]。这种“通过复制进行加权”的方法实际上等价于权重为整数的 WLS。然而，它无法精确表示非整数的理想权重，并且通过大量复制数据来近似理想权重在计算上是极其低效的。WLS 的数据变换方法则在不增加数据量的情况下，优雅且精确地实现了加权。

### WLS 的几何解释

数据变换的视角可以进一步深化为一种几何解释 [@problem_id:3128045]。我们可以定义一个**[加权内积](@entry_id:163877)**空间，其中任意两个向量 $\mathbf{u}, \mathbf{v} \in \mathbb{R}^n$ 的[内积](@entry_id:158127)为：
$$
\langle \mathbf{u}, \mathbf{v} \rangle_W = \mathbf{u}^\top \mathbf{W} \mathbf{v}
$$
这个[内积](@entry_id:158127)诱导出一个加权范数 $\|\mathbf{u}\|_W = \sqrt{\langle \mathbf{u}, \mathbf{u} \rangle_W}$。

在此几何框架下，WLS 的目标函数 $J(\boldsymbol{\beta}) = (\mathbf{y} - \mathbf{X}\boldsymbol{\beta})^\top \mathbf{W} (\mathbf{y} - \mathbf{X}\boldsymbol{\beta})$ 正是最小化向量 $\mathbf{y}$ 与由 $\mathbf{X}$ 的列[向量张成](@entry_id:152883)的[子空间](@entry_id:150286) $\text{col}(\mathbf{X})$ 中某向量 $\mathbf{X}\boldsymbol{\beta}$ 之间的加权距离的平方，即 $\|\mathbf{y} - \mathbf{X}\boldsymbol{\beta}\|_W^2$。

WLS 的解 $\hat{\mathbf{y}}_{\text{WLS}} = \mathbf{X}\hat{\boldsymbol{\beta}}_{\text{WLS}}$ 就是将观测向量 $\mathbf{y}$ **在[加权内积](@entry_id:163877)意义下**[正交投影](@entry_id:144168)到 $\text{col}(\mathbf{X})$ 上的结果。这意味着[残差向量](@entry_id:165091) $\mathbf{r} = \mathbf{y} - \hat{\mathbf{y}}_{\text{WLS}}$ 与 $\mathbf{X}$ 的每一列都**W-正交**。这可以用代数形式表示为：
$$
\mathbf{X}^\top \mathbf{W} \mathbf{r} = \mathbf{0}
$$
这与我们之[前推](@entry_id:158718)导出的 WLS [正规方程](@entry_id:142238)是等价的。因此，WLS 可以被理解为在一个根据观测精度调整了“距离”和“角度”定义的空间中进行的标准[正交投影](@entry_id:144168)。

### 实践应用与诊断

#### 已知[方差](@entry_id:200758)与效率增益

在理想情况下，我们知道每个观测的真实[误差方差](@entry_id:636041) $\sigma_i^2$，可以直接使用最优权重 $w_i = 1/\sigma_i^2$。根据广义[高斯-马尔可夫定理](@entry_id:138437)，此时的 WLS 估计量是 BLUE，其[方差](@entry_id:200758)小于任何其他线性[无偏估计量](@entry_id:756290)，包括 OLS 估计量。

这种效率的提升直接体现在更精确的预测上。在构建[预测区间](@entry_id:635786)时，预测误差的[方差](@entry_id:200758)包含两部分：模型均值估计的不确定性和新观测自身的随机波动。由于 WLS 提供了对模型均值更精确的估计，其[预测区间](@entry_id:635786)通常比使用 OLS 结合异[方差](@entry_id:200758)[稳健标准误](@entry_id:146925)所得到的区间更窄，尤其是在预测变量取值导致[方差](@entry_id:200758)较大或较小的区域 [@problem_id:3128046]。

#### 未知[方差](@entry_id:200758)：[可行广义最小二乘法](@entry_id:634462)（FGLS）

在绝大多数实际问题中，真实的 $\sigma_i^2$ 是未知的。此时，我们需要先对异[方差](@entry_id:200758)的结构进行建模和估计，然后使用估计出的[方差](@entry_id:200758)来构造权重。这个多步骤过程被称为**[可行广义最小二乘法](@entry_id:634462)**（Feasible Generalized Least Squares, FGLS）[@problem_id:3128021]。一个典型的 FGLS 流程如下：

1.  **运行 OLS**：首先对原始数据运行 OLS，得到初始的[参数估计](@entry_id:139349)和残差 $r_i$。
2.  **建模[方差](@entry_id:200758)**：假设[方差](@entry_id:200758)与预测变量之间存在某种函数关系，例如，[乘性](@entry_id:187940)异[方差](@entry_id:200758)模型 $\operatorname{Var}(\varepsilon_i \mid \mathbf{x}_i) = \sigma^2 \exp(\mathbf{x}_i^\top \boldsymbol{\alpha})$。对该模型取对数，我们得到 $\ln(\sigma_i^2) = \ln(\sigma^2) + \mathbf{x}_i^\top \boldsymbol{\alpha}$。由于 $E[r_i^2] \approx \sigma_i^2$，我们可以通过回归 $\ln(r_i^2)$ 对 $\mathbf{x}_i$ 来估计参数 $\boldsymbol{\alpha}$。
3.  **估计权重**：利用上一步得到的[方差](@entry_id:200758)模型，为每个观测点计算估计的[方差](@entry_id:200758) $\hat{\sigma}_i^2$，并构造权重 $\hat{w}_i = 1/\hat{\sigma}_i^2$。
4.  **运行 WLS**：使用这些估计的权重 $\hat{w}_i$ 来执行 WLS 回归，得到最终的 FGLS 参数估计。

在决定是否需要采用 WLS/FGLS 之前，通常会进行异[方差](@entry_id:200758)检验。**怀特检验**（White's test）是一种常用的通用检验方法，它不要求预先指定异[方差](@entry_id:200758)的具体形式。该检验通过一个辅助回归，将 OLS 的残差平方 $r_i^2$ 对原始预测变量、它们的平方以及交叉乘积项进行回归，然后检验这些预测变量的联合显著性 [@problem_id:3128021]。

#### 模型评估与[影响诊断](@entry_id:167943)

**加权 R-平方**：在 WLS 中，标准 $R^2$ 的解释变得模糊。一个更合适的度量是**加权 R-平方** ($R_W^2$) [@problem_id:3128051]，其定义为：
$$
R_W^2 = 1 - \frac{\sum_{i=1}^{n} w_i (y_i - \hat{y}_i)^2}{\sum_{i=1}^{n} w_i (y_i - \bar{y}_W)^2}
$$
其中 $\bar{y}_W = (\sum w_i y_i) / (\sum w_i)$ 是响应变量的加权均值。当模型包含截距项时，$R_W^2$ 具有良好的性质：它的取值范围在 $[0, 1]$ 之间，并且等于观测值 $y_i$ 和拟合值 $\hat{y}_i$ 之间的加权[皮尔逊相关系数](@entry_id:270276)的平方。

**[影响诊断](@entry_id:167943)**：在 WLS 中，一个观测点的影响力不仅取决于其[杠杆值](@entry_id:172567)，还取决于其权重。[方差](@entry_id:200758)极大（权重极小）的观测点，即使其[杠杆值](@entry_id:172567)很高，对最终拟合结果的影响也可能微乎其微。我们可以通过**加权[库克距离](@entry_id:175103)**（Weighted Cook's Distance）来量化这种影响 [@problem_id:3128037]。其推导表明，当一个点的权重趋向于零时，其[库克距离](@entry_id:175103)也趋向于零。这从数学上证实了 WLS 能够有效降低高噪声数据点对[模型参数估计](@entry_id:752080)的过度影响。

在进行诊断时，需要注意权重的尺度问题。虽然 $\hat{\boldsymbol{\beta}}_{\text{WLS}}$ 对权重的整体缩放不变，但许多诊断统计量，如加权[残差平方和](@entry_id:174395)（WRSS）和标准化加权残差，会随权重尺度变化而变化 [@problem_id:3127967]。因此，为了使诊断结果具有可比性，通常建议对权重进行标准化处理（例如，使它们的和等于样本量 $n$）。

### 高级议题与注意事项

#### WLS 与模型偏误

必须强调，WLS 的主要功能是**提高估计效率**（减小[方差](@entry_id:200758)），而不是**消除偏误**。只要均值模型设定正确，OLS 和 WLS 都是无偏的 [@problem_id:3127984]。

然而，如果模型存在遗漏变量偏误，WLS 不仅无法解决这个问题，甚至可能使其恶化 [@problem_id:3127963]。遗漏变量偏误的大小取决于被遗漏变量与模型中包含的预测变量之间的相关性。WLS 会对这种相关性进行加权平均。如果这种相关性恰好在权重较大（即[误差方差](@entry_id:636041)较小）的观测点中更强，那么 WLS 将放大这种相关性，从而导致比 OLS 更严重的遗漏变量偏误。反之，WLS 也可能减小偏误。这提醒我们，在解决异[方差](@entry_id:200758)问题的同时，不能忽视对均值模型设定正确性的检验。

#### 权重的伦理考量

WLS 通过赋予不同观测点不同的权重来优化估计。当某个观测点的权重变得极小时，它在模型拟合过程中的作用就相当于被部分或完全排除了 [@problem_id:3127984]。

在应用领域，这引出了重要的伦理问题。如果[误差方差](@entry_id:636041)的差异与特定人群或条件系统性地相关（例如，来自资源较差地区的测量工具精度较低，导致数据噪声更大），那么机械地应用 WLS 会系统性地降低这些[代表性](@entry_id:204613)不足群体的“话语权”。这可能导致最终建立的模型无法准确反映这些群体的情况，甚至在应用于他们时产生不公平的后果，从而固化或加剧了现有的结构性不平等。

因此，一个负责任的数据分析师不应将 WLS 视为一个纯粹的技术修复工具。在应用 WLS 之前，必须深入探究异[方差](@entry_id:200758)的来源。如果异[方差](@entry_id:200758)源于可控的测量差异，那么更根本的解决方案可能是改进数据收集过程、设计更稳健的测量方案，或者采用对模型假设不那么敏感的[稳健回归](@entry_id:139206)方法，而不是默认地将“嘈杂”的数据点降权处理。