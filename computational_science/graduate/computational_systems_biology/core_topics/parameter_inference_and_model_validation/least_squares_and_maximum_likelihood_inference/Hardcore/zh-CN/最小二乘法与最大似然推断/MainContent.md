## 引言
在[计算系统生物学](@entry_id:747636)等数据驱动的科学领域，数学模型是理解复杂现象的核心工具。然而，一个模型的价值很大程度上取决于其参数能否准确地反映现实世界的[生物过程](@entry_id:164026)。这就引出了一个根本性的问题：我们如何利用有限且带有噪声的实验数据，来推断出这些未知参数的最佳值？这一过程，即[参数推断](@entry_id:753157)，是连接理论模型与实验观测的桥梁，也是所有定量建模工作的基石。

本文旨在系统性地解决这一问题，聚焦于两种最基本、最强大且应用最广泛的推断框架：最小二乘法（Least-Squares, LS）和最大似然估计（Maximum Likelihood Estimation, MLE）。我们将揭示，这两种看似不同的方法实则有着深刻的内在联系。通过本文的学习，你将不仅掌握它们的理论基础，还能理解如何将这些原理应用于解决实际问题。

文章将分为三个核心部分。在“**原理与机制**”一章中，我们将从第一性原理出发，详细阐述最大似然估计的思想，并证明在特定（且常见）的噪声假设下，它如何自然地简化为经典的[最小二乘法](@entry_id:137100)。我们还将探讨如何求解这些估计问题，以及如何使用[费雪信息](@entry_id:144784)等工具来量化我们得到的结果的不确定性。随后，在“**应用与跨学科联系**”一章中，我们将通过生物化学、基因组学、[地球科学](@entry_id:749876)等多个领域的实例，展示这些核心原理在不同科学背景下的强大适用性与灵活性。最后，“**动手实践**”部分将提供一系列精心设计的练习，引导你将理论知识付诸实践，加深对关键概念的理解。

## 原理与机制

在[计算系统生物学](@entry_id:747636)中，我们的核心任务之一是利用实验数据构建和验证数学模型。这一过程的关键在于[参数推断](@entry_id:753157)——即确定模型的未知参数，使其能最佳地解释我们观测到的数据。本章将深入探讨两种最基本且相互关联的[参数推断](@entry_id:753157)框架：最大似然估计（Maximum Likelihood Estimation, MLE）和最小二乘法（Least-Squares, LS）。我们将从基本原理出发，阐明它们之间的深刻联系，并逐步介绍在实践中[量化不确定性](@entry_id:272064)、诊断问题以及解决常见挑战的机制。

### 最大似然估计原理

[参数推断](@entry_id:753157)的核心问题是：给定一组观测数据 $\mathbf{y}$ 和一个由参数 $\theta$ 描述的[概率模型](@entry_id:265150) $p(\mathbf{y} | \theta)$，我们应该如何选择 $\theta$ 的值？**[最大似然估计](@entry_id:142509)** (MLE) 提供了一个直观且强大的回答：我们应该选择能使观测数据出现的概率最大的那个参数值。

#### 似然函数与[对数似然函数](@entry_id:168593)

为了形式化这一思想，我们定义**[似然函数](@entry_id:141927) (likelihood function)**，记作 $L(\theta; \mathbf{y})$。它在数值上等于给定参数 $\theta$ 时观测到数据 $\mathbf{y}$ 的概率，但我们将其视为参数 $\theta$ 的函数，而数据 $\mathbf{y}$ 是固定的。

$L(\theta; \mathbf{y}) = p(\mathbf{y} | \theta)$

这里必须强调一个关键区别：[似然函数](@entry_id:141927) $L(\theta; \mathbf{y})$ **不是** 参数 $\theta$ 的[概率分布](@entry_id:146404)。它在 $\theta$ 的[参数空间](@entry_id:178581)上积分通常不为1。它衡量的是在不同参数值下，我们观测到的这组特定数据的“似真性”。这与[贝叶斯推断](@entry_id:146958)中的**[后验概率](@entry_id:153467)** (posterior probability) $p(\theta | \mathbf{y})$ 形成对比。根据贝叶斯定理，后验概率正比于[似然](@entry_id:167119)与[先验概率](@entry_id:275634) $\pi(\theta)$ 的乘积：$p(\theta | \mathbf{y}) \propto p(\mathbf{y} | \theta) \pi(\theta)$。后验概率确实是 $\theta$ 在给定数据后的[概率分布](@entry_id:146404)，但似然函数本身不是 。

在许多生物学实验中，例如单细胞[转录组](@entry_id:274025)测序，我们可以合理地假设在给定某个生物学参数（如平均表达水平 $\theta$）的条件下，来自 $n$ 个细胞的测量值 $y_1, \dots, y_n$ 是相互独立的。在这种情况下，整个数据集的联合概率是各个测量概率的乘积。因此，似然函数可以写成：

$L(\theta; \mathbf{y}) = \prod_{i=1}^{n} p(y_i | \theta)$

由于乘积形式在数学上通常难以处理，我们更倾向于使用**[对数似然函数](@entry_id:168593) (log-likelihood function)** $\ell(\theta; \mathbf{y})$，即似然函数的自然对数：

$\ell(\theta; \mathbf{y}) = \ln L(\theta; \mathbf{y}) = \sum_{i=1}^{n} \ln p(y_i | \theta)$

因为对数函数是单调递增的，最大化似然函数等价于最大化[对数似然函数](@entry_id:168593)。

**[最大似然估计量](@entry_id:163998) (Maximum Likelihood Estimator, MLE)**，记作 $\hat{\theta}_{\text{MLE}}$，就是使似然函数（或[对数似然函数](@entry_id:168593)）达到最大值的参数值：

$\hat{\theta}_{\text{MLE}} = \arg\max_{\theta} \ell(\theta; \mathbf{y})$

一个重要的性质是MLE的**不变性 (invariance property)**。如果 $\phi = g(\theta)$ 是参数的一一对应变换（可[逆变](@entry_id:192290)换），那么 $\phi$ 的[最大似然估计](@entry_id:142509)就是 $\theta$ 的最大似然估计经过同一变换得到的结果，即 $\hat{\phi} = g(\hat{\theta})$。这是因为我们只是对参数空间进行了重新坐标化，而似然函数本身作为数据概率的度量并没有改变，其[最大值点](@entry_id:634610)也相应地进行了映射。在进行这种重新参数化时，我们不需要像变换[概率密度](@entry_id:175496)那样引入[雅可比行列式](@entry_id:137120) 。

### 最大似然与最小二乘的联系

[最小二乘法](@entry_id:137100)是一种广泛应用的[参数估计](@entry_id:139349)方法，尤其在线性模型中。它与[最大似然估计](@entry_id:142509)之间存在深刻的联系，这种联系在处理生物数据时尤其重要。

#### 高斯噪声下的等价性

假设我们的测量过程受到独立同分布 (i.i.d.) 的高斯噪声影响。这意味着每个数据点 $y_i$ 都服从一个以模型预测值 $f(x_i; \theta)$ 为均值、[方差](@entry_id:200758)为 $\sigma^2$ 的正态分布：

$y_i \sim \mathcal{N}(f(x_i; \theta), \sigma^2)$

其中 $x_i$ 代表实验条件（如时间、[配体](@entry_id:146449)浓度等）。单个数据点的概率密度函数为：

$p(y_i | \theta) = \frac{1}{\sqrt{2\pi \sigma^2}} \exp\left(-\frac{(y_i - f(x_i; \theta))^2}{2\sigma^2}\right)$

根据独立性假设，整个数据集的[对数似然函数](@entry_id:168593)为：

$\ell(\theta; \mathbf{y}) = \sum_{i=1}^{n} \ln \left( \frac{1}{\sqrt{2\pi \sigma^2}} \exp\left(-\frac{(y_i - f(x_i; \theta))^2}{2\sigma^2}\right) \right)$

$\ell(\theta; \mathbf{y}) = -\frac{n}{2}\ln(2\pi \sigma^2) - \frac{1}{2\sigma^2} \sum_{i=1}^{n} (y_i - f(x_i; \theta))^2$

为了找到[最大似然估计](@entry_id:142509) $\hat{\theta}$，我们需要最大化 $\ell(\theta; \mathbf{y})$。观察上式，第一项 $-\frac{n}{2}\ln(2\pi \sigma^2)$ 和因子 $-\frac{1}{2\sigma^2}$ 都不依赖于参数 $\theta$（假设 $\sigma^2$ 已知或与 $\theta$ 无关）。因此，最大化[对数似然函数](@entry_id:168593)就等价于最小化**[残差平方和](@entry_id:174395) (Sum of Squared Residuals, SSR)**：

$S(\theta) = \sum_{i=1}^{n} (y_i - f(x_i; \theta))^2$

这个结论至关重要：**在[独立同分布](@entry_id:169067)[高斯噪声](@entry_id:260752)的假设下，最大似然估计等价于[最小二乘估计](@entry_id:262764)**  。这为历史悠久且计算上易于处理的[最小二乘法](@entry_id:137100)提供了坚实的[概率论基础](@entry_id:158925)。

#### 异[方差](@entry_id:200758)噪声与加权最小二乘

在许多生物实验中，[测量误差](@entry_id:270998)的[方差](@entry_id:200758)并不是恒定的。例如，测量高丰度mRNA的仪器噪声可能比测量低丰度mRNA时更大。这种情况称为**[异方差性](@entry_id:136378) (heteroscedasticity)**，即每个数据点 $y_i$ 的噪声[方差](@entry_id:200758) $\sigma_i^2$ 不同。

$y_i \sim \mathcal{N}(f(x_i; \theta), \sigma_i^2)$

此时，[对数似然函数](@entry_id:168593)变为：

$\ell(\theta; \mathbf{y}) = \sum_{i=1}^{n} \left( -\frac{1}{2}\ln(2\pi \sigma_i^2) - \frac{(y_i - f(x_i; \theta))^2}{2\sigma_i^2} \right)$

同样，为了最大化 $\ell(\theta; \mathbf{y})$，我们需要最小化：

$S_W(\theta) = \sum_{i=1}^{n} \frac{1}{\sigma_i^2} (y_i - f(x_i; \theta))^2 = \sum_{i=1}^{n} w_i (y_i - f(x_i; \theta))^2$

这被称为**加权最小二乘 (Weighted Least Squares, WLS)**。这里的权重 $w_i = 1/\sigma_i^2$ 直观地反映了每个数据点的信息量：测量越精确（[方差](@entry_id:200758) $\sigma_i^2$ 越小），其在拟合中的权重就越大。例如，在分析一个线性时间进程 $y_i = x_1 + x_2 t_i$ 时，如果不同时间点 $t_i$ 的测量精度不同，使用WLS（即MLE）能够比[普通最小二乘法](@entry_id:137121)得到更准确的[参数估计](@entry_id:139349) 。

### 求解估计问题

确定了[目标函数](@entry_id:267263)（无论是[对数似然](@entry_id:273783)还是[残差平方和](@entry_id:174395)）后，下一步就是找到使其最优化的参数值。

#### 解析解：[得分函数](@entry_id:164520)

对于一些简单的模型，我们可以通过解析方法找到MLE。这需要计算[对数似然函数](@entry_id:168593)关于每个参数的[偏导数](@entry_id:146280)，并令其为零。这个[梯度向量](@entry_id:141180)被称为**[得分函数](@entry_id:164520) (score function)**：

$\mathbf{S}(\theta) = \nabla_{\theta} \ell(\theta; \mathbf{y})$

令[得分函数](@entry_id:164520)为零得到的[方程组](@entry_id:193238) $\mathbf{S}(\hat{\theta}) = \mathbf{0}$ 称为**得分方程 (score equations)**。

一个经典的例子是估计正态分布的均值 $\mu$ 和[方差](@entry_id:200758) $\sigma^2$。对于i.i.d.样本 $y_1, \dots, y_n \sim \mathcal{N}(\mu, \sigma^2)$，[对数似然函数](@entry_id:168593)为：

$\ell(\mu, \sigma^2) = -\frac{n}{2}\ln(2\pi) - \frac{n}{2}\ln(\sigma^2) - \frac{1}{2\sigma^2} \sum_{i=1}^{n} (y_i - \mu)^2$

通过求解 $\frac{\partial \ell}{\partial \mu} = 0$ 和 $\frac{\partial \ell}{\partial \sigma^2} = 0$，我们可以得到我们所熟知的MLE解 ：

$\hat{\mu} = \frac{1}{n}\sum_{i=1}^{n} y_i = \bar{y} \quad (\text{样本均值})$

$\hat{\sigma}^2 = \frac{1}{n}\sum_{i=1}^{n} (y_i - \hat{\mu})^2 \quad (\text{有偏样本方差})$

#### [非线性模型](@entry_id:276864)的数值解：[高斯-牛顿法](@entry_id:173233)

在系统生物学中，绝大多数模型（如描述酶动力学、[信号转导](@entry_id:144613)或基因调控的模型）对于其参数都是[非线性](@entry_id:637147)的。例如，一个简单的[配体](@entry_id:146449)激活模型 $f(x; \theta) = \frac{\theta_1 x}{\theta_2 + x}$。在这种情况下，得分方程通常无法解析求解，我们必须依赖[数值优化](@entry_id:138060)算法。

对于源于最小二乘的问题（即[高斯噪声](@entry_id:260752)假设下的MLE），**[高斯-牛顿法](@entry_id:173233) (Gauss-Newton algorithm)** 是一种高效的迭代方法。其核心思想是在每一步迭代中，用线性函数来近似[非线性模型](@entry_id:276864)，然后解决这个简化的线性最小二乘问题来找到参数的更新方向。

具体来说，假设我们当前的参数估计为 $\theta_k$，我们希望找到一个更新量 $\delta$，使得新的参数 $\theta_{k+1} = \theta_k + \delta$ 能更好地最小化[残差平方和](@entry_id:174395) $S(\theta) = \frac{1}{2}\| \mathbf{r}(\theta) \|_2^2$，其中 $\mathbf{r}(\theta) = \mathbf{y} - \mathbf{f}(\mathbf{x}; \theta)$ 是[残差向量](@entry_id:165091)。

我们将[残差向量](@entry_id:165091)在 $\theta_k$ 附近进行一阶[泰勒展开](@entry_id:145057)：

$\mathbf{r}(\theta_k + \delta) \approx \mathbf{r}(\theta_k) + J(\theta_k) \delta$

其中 $J(\theta_k)$ 是[残差向量](@entry_id:165091)关于参数 $\theta$ 的**雅可比矩阵 (Jacobian matrix)**，也常被称为**敏感性矩阵 (sensitivity matrix)**。其元素 $J_{ij} = \frac{\partial r_i}{\partial \theta_j} = -\frac{\partial f_i}{\partial \theta_j}$，衡量了模型输出对参数变化的敏感程度。

我们将这个线性近似代入最小二乘[目标函数](@entry_id:267263)，得到一个关于 $\delta$ 的二次型问题。通过求解这个二次型问题的最优解，我们得到一个[线性方程组](@entry_id:148943)，称为**正规方程 (normal equations)**：

$(J(\theta_k)^\top J(\theta_k)) \delta = -J(\theta_k)^\top \mathbf{r}(\theta_k)$

通过求解这个[方程组](@entry_id:193238)得到更新量 $\delta$，我们便可以更新参数 $\theta_{k+1} = \theta_k + \delta$，并重复此过程直至收敛。[高斯-牛顿法](@entry_id:173233)是许多[非线性模型](@entry_id:276864)拟合软件的核心算法 。

### [量化不确定性](@entry_id:272064)与[模型诊断](@entry_id:136895)

得到参数的[点估计](@entry_id:174544)值（如MLE）是重要的第一步，但同样重要的是量化我们对这些估计值有多大的信心。一个具有极大不确定性的参数值在科学上是几乎无用的。

#### 费雪信息矩阵与[克拉默-拉奥下界](@entry_id:154412)

参数估计的不确定性与[对数似然函数](@entry_id:168593)在[最大值点](@entry_id:634610)附近的“尖锐程度”或“曲率”密切相关。如果似然函数非常尖锐，即使参数稍有偏离，似然值也会急剧下降，这表明数据对参数值有很强的约束，因此我们的估计是精确的。相反，一个平坦的[似然函数](@entry_id:141927)山峰意味着在一个很宽的参数范围内数据都同样“可能”，因此估计是不确定的。

这种曲率由[对数似然函数](@entry_id:168593)的[二阶导数](@entry_id:144508)（Hessian矩阵）来描述。**费雪信息矩阵 (Fisher Information Matrix, FIM)** $I(\theta)$ 被定义为负的[对数似然函数](@entry_id:168593)Hessian矩阵的[期望值](@entry_id:153208)：

$I(\theta) = - \mathbb{E} \left[ \nabla_{\theta}^2 \ell(\theta; \mathbf{y}) \right]$

在许多情况下，包括[最小二乘问题](@entry_id:164198)，[费雪信息矩阵](@entry_id:750640)可以近似为 $I(\hat{\theta}) \approx \frac{1}{\sigma^2} J(\hat{\theta})^\top J(\hat{\theta})$，这里的 $J$ 正是我们在[高斯-牛顿法](@entry_id:173233)中遇到的敏感性矩阵 。

[费雪信息矩阵](@entry_id:750640)的强大之处在于**[克拉默-拉奥下界](@entry_id:154412) (Cramér-Rao Bound, CRB)** 定理。该定理指出，对于任何[无偏估计量](@entry_id:756290) $\hat{\theta}$，其协方差矩阵 $Cov(\hat{\theta})$ 有一个下界，这个下界恰好是费雪信息矩阵的逆：

$Cov(\hat{\theta}) \ge I(\theta)^{-1}$

这意味着 $I(\theta)^{-1}$ 为我们提供了参数估计可能达到的最小[方差](@entry_id:200758)。因此，费雪信息矩阵是衡量一个实验设计能提供多少关于参数信息的核心指标。一个“信息量大”的实验（大的 $I(\theta)$）会产生低[方差](@entry_id:200758)的估计。我们可以通过计算正态分布 MLE 的[费雪信息矩阵](@entry_id:750640)来具体感受这一点 。

#### [可辨识性](@entry_id:194150)问题：结构与实践

在构建和拟合模型时，我们常会遇到**[可辨识性](@entry_id:194150) (identifiability)** 问题，即我们是否能够从数据中唯一地确定参数的值。
- **结构[可辨识性](@entry_id:194150) (Structural Identifiability)** 是模型的理论属性，它不考虑数据的数量和质量。一个模型如果存在两组或多组不同的参数值，却能在任何实验条件下产生完全相同的输出，那么它就是结构不可辨识的。这通常源于模型内在的对称性或冗余。例如，在一个两室模型中，我们或许可以唯一地确定[速率常数](@entry_id:196199)组合，如 $k_{10}+k_{12}+k_{21}$ 和 $k_{10}k_{21}$，但无法唯一地确定单个的 $k_{10}$、$k_{12}$ 和 $k_{21}$。通过分析模型的[传递函数](@entry_id:273897)或输入-输出[微分方程](@entry_id:264184)，我们可以检测这种缺陷。如果能够从输入-输出关系唯一地反解出模型参数，那么模型就是结构可辨识的 。
- **实践可辨識性 (Practical Identifiability)** 则是一个与具体实验数据相关的问题。即使一个模型在理论上是结构可辨识的，但在一个特定的、有限且带噪的实验数据下，我们可能仍然无法精确地估计某些参数或参数组合。这通常表现为费雪信息矩阵接近奇异（ill-conditioned），或者说[对数似然函数](@entry_id:168593)在某些方向上非常平坦，形成狭长的“山谷” 。

实践不[可辨识性](@entry_id:194150)问题与敏感性矩阵 $J$ 的列向量密切相关。如果 $J$ 的两列（或多个[列的线性组合](@entry_id:150240)）近似共线，这意味着改变相应的两个参数（或参数组合）对模型输出产生几乎相同的影响。数据将无法区分这两种效应，导致参数估计之间的高度相关和巨大的不确定性。这个问题的直接表现就是 $J^\top J$ 矩阵的一个或多个[特征值](@entry_id:154894)非常小，对应着似然函数的“平坦”方向 。

#### [最优实验设计](@entry_id:165340)

理解了费雪信息与不确定性之间的关系后，我们可以主动地利用它来指导实验。**[最优实验设计](@entry_id:165340) (Optimal Experimental Design)** 的目标就是[选择实验](@entry_id:187303)条件（如采样时间点、药物浓度等），以最大化我们能从实验中获得的关于参数的信息量，即最大化费雪信息矩阵（根据某种标量准则，如最大化其[行列式](@entry_id:142978)，即D-optimality）。

例如，在一个描述[mRNA合成](@entry_id:171184)与降解的线性[生灭过程](@entry_id:168595)中，我们可以通过求解一个[常微分方程](@entry_id:147024)得到mRNA的平均丰度 $\mu(t;\theta)$，其中降解率 $\theta$ 是未知参数。假设测量服从泊松分布，我们可以推导出费-信息 $I(\theta;t)$ 是采样时间 $t$ 的函数。通过最大化这个函数，我们可以找到能最精确估计 $\theta$ 的最优采样时间 $t^*$ 。这体现了如何将[统计推断](@entry_id:172747)原理转化为具体的、可操作的实验策略。

### 应对病态推断问题

在许多系统生物学应用中，尤其是在高维问题（例如从基因表达数据推断[转录因子](@entry_id:137860)活性网络）中，[参数推断](@entry_id:753157)问题常常是**病态的 (ill-posed or ill-conditioned)**。

#### 病态问题与[奇异值分解](@entry_id:138057)

一个线性最小二乘问题 $A\mathbf{x} \approx \mathbf{y}$ 是病态的，意味着对观测数据 $\mathbf{y}$ 的微小扰动（噪声）会导致解 $\mathbf{x}$ 发生巨大的变化。这种不稳定性可以用**[奇异值分解](@entry_id:138057) (Singular Value Decomposition, SVD)** 来深刻理解。任何矩阵 $A$ 都可以分解为 $A = U\Sigma V^\top$，其中 $U$ 和 $V$ 是正交矩阵，$\Sigma$ 是一个对角矩阵，其对角线上的元素是**[奇异值](@entry_id:152907) (singular values)** $\sigma_i$。

[最小二乘解](@entry_id:152054)可以表示为 $\hat{\mathbf{x}} = A^+ \mathbf{y}$，其中 $A^+ = V\Sigma^+ U^\top$ 是 $A$ 的**[伪逆](@entry_id:140762) (pseudoinverse)**。可以证明，解的相对误差受一个关键因子的放大：

$\frac{\|\hat{\mathbf{x}} - \mathbf{x}_{\text{true}}\|_{2}}{\|\mathbf{x}_{\text{true}}\|_{2}} \le \kappa(A) \frac{\|\boldsymbol{\varepsilon}\|_{2}}{\|\mathbf{y}_{\text{true}}\|_{2}}$

这里的 $\kappa(A) = \sigma_{\max} / \sigma_{\min}$ 是矩阵 $A$ 的**[条件数](@entry_id:145150) (condition number)**，$\boldsymbol{\varepsilon}$ 是数据中的噪声。如果条件数非常大（即最大和最小奇异值差别悬殊），那么即使是很小的相对噪声也会被放大成巨大的解误差 。这与实践不[可辨识性](@entry_id:194150)问题紧密相连：一个巨大的条件数正是一个接近奇异的[费雪信息矩阵](@entry_id:750640)的体现。

#### 正则化：偏差-方差权衡

为了解决[病态问题](@entry_id:137067)，我们引入**正则化 (regularization)**。其核心思想是向原始目标函数中添加一个惩罚项，该项体现了我们对解的[先验信念](@entry_id:264565)（例如，我们相信解是“简单”的或“平滑”的）。

**[吉洪诺夫正则化](@entry_id:140094) (Tikhonov regularization)**，在线性回归背景下也称为**[岭回归](@entry_id:140984) (ridge regression)**，是一种最常见的[正则化方法](@entry_id:150559)。它修改最小二乘[目标函数](@entry_id:267263)为：

$\min_{\mathbf{x}} \quad \|\mathbf{y} - A\mathbf{x}\|_{2}^2 + \lambda^2 \|\mathbf{x}\|_{2}^2$

这里的 $\lambda > 0$ 是**正则化参数**，$\|\mathbf{x}\|_{2}^2$ 是惩罚项，它惩罚参数向量的欧几里得范数。这个惩罚项有效地稳定了解，即使 $A^\top A$ 是奇异的或接近奇异的，$(A^\top A + \lambda^2 I)$ 也是可逆且条件良好的。

正则化的代价是引入了**偏差 (bias)**。无正则化的[最小二乘解](@entry_id:152054)是无偏的，但[方差](@entry_id:200758)可能极大。正则化通过牺牲无偏性来换取[方差](@entry_id:200758)的大幅降低。这就是著名的**偏差-方差权衡 (bias-variance tradeoff)**。

我们可以利用SVD精确地刻画这一权衡。对于[Tikhonov正则化](@entry_id:140094)估计量的第 $i$ 个奇异分量，其均方误差 (Mean Squared Error, MSE) 可以分解为偏差的平方和[方差](@entry_id:200758)两部分 ：

$\mathbb{E}[(\hat{x}_{\lambda, i} - \theta_{i})^{2}] = \underbrace{\frac{\lambda^{4} \theta_{i}^{2}}{(s_{i}^{2} + \lambda^{2})^{2}}}_{\text{偏差平方}} + \underbrace{\frac{s_{i}^{2} \sigma^{2}}{(s_{i}^{2} + \lambda^{2})^{2}}}_{\text{方差}}$

其中 $\theta_i$ 是真实解在 $V$ 基下的分量，$s_i$ 是第 $i$ 个[奇异值](@entry_id:152907)。从这个式子可以看出：
- 当 $\lambda \to 0$ 时，偏差趋于0（恢复无偏性），但如果 $s_i$ 很小，[方差](@entry_id:200758)项会爆炸。
- 当 $\lambda$ 增大时，偏差项增加，但分母 $(s_i^2+\lambda^2)^2$ 增长得更快，从而有效地抑制了由小[奇异值](@entry_id:152907) $s_i$ 引起的[方差](@entry_id:200758)。

选择合适的 $\lambda$ 就是在这两者之间找到最佳[平衡点](@entry_id:272705)。正则化是处理高维、[共线性](@entry_id:270224)或数据不足等系统生物学中常见病态[逆问题](@entry_id:143129)的关键工具。