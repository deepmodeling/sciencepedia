## 引言
[最大似然](@entry_id:146147)分类（Maximum Likelihood Classification, MLC）是监督分类领域，尤其是在遥感科学中，一块历久弥新的基石。面对海量的[多维数据](@entry_id:189051)，如何建立一个既有坚实理论基础又能有效区分不同地物类别的自动化方法，是一个核心挑战。MLC正是基于概率论为这一问题提供了优雅且强大的解决方案。然而，要真正掌握并灵活运用这一方法，我们必须深入其内部，理解其工作原理、知晓其能力边界，并洞察其在不同学科中的应用智慧。本文旨在系统性地剖析[最大似然](@entry_id:146147)分类。在“原理与机制”一章中，我们将从贝叶斯理论出发，揭示其[概率模型](@entry_id:265150)和决策规则的数学本质。接着，在“应用与跨学科联系”一章中，我们将跨越遥感、医学和工程等多个领域，展示MLC作为一种基本思想的广泛影响力，并探讨其与[现代机器学习](@entry_id:637169)的深刻联系。最后，通过“动手实践”部分，读者将有机会亲手应用这些理论，将抽象的知识转化为解决实际问题的能力。让我们一同开启这次从理论到实践的探索之旅。

## 原理与机制

本章在前一章介绍性概述的基础上，深入探讨[最大似然](@entry_id:146147)分类（Maximum Likelihood Classification, MLC）的核心科学原理与作用机制。我们将从其[概率论基础](@entry_id:158925)出发，系统性地推导其决策规则，探讨[参数估计](@entry_id:139349)的实际方法，并分析在真实世界应用中遇到的关键挑战及其解决方案。最后，我们将把这些经典思想与现代机器学习中的高级概念联系起来。

### [概率分类](@entry_id:637254)的基础

[最大似然](@entry_id:146147)分类本质上是**[贝叶斯决策理论](@entry_id:909090)（Bayes' decision theory）** 的一个特例。贝叶斯理论旨在将一个[特征向量](@entry_id:151813) $\mathbf{x}$ 分配给能使后验概率 $P(\omega_i | \mathbf{x})$ 最大化的类别 $\omega_i$。根据贝叶斯公式，[后验概率](@entry_id:153467)可以表示为：

$P(\omega_i | \mathbf{x}) = \frac{p(\mathbf{x} | \omega_i) P(\omega_i)}{p(\mathbf{x})}$

其中，$p(\mathbf{x} | \omega_i)$ 是**类[条件概率密度函数](@entry_id:190422)（class-conditional probability density function）**，表示在给定类别 $\omega_i$ 的情况下观测到[特征向量](@entry_id:151813) $\mathbf{x}$ 的[概率密度](@entry_id:175496)；$P(\omega_i)$ 是类别 $\omega_i$ 的**[先验概率](@entry_id:275634)（prior probability）**；$p(\mathbf{x})$ 是证据因子，对所有类别是相同的。

在许多遥感应用中，我们可能没有关于地物类别先验分布的可靠信息，或者我们希望让数据本身驱动[分类结果](@entry_id:924005)。在这种情况下，我们通常会做出一个简化假设：所有类别的**先验概率相等**。此外，如果将所有错分情况的代价同等看待，那么最大化[后验概率](@entry_id:153467)的任务就简化为最大化类[条件概率密度](@entry_id:265457) $p(\mathbf{x} | \omega_i)$。这个过程就是**[最大似然](@entry_id:146147)分类**的核心。

为了计算方便，我们通常最大化其单调递增的对数形式，即**[对数似然](@entry_id:273783)（log-likelihood）**。因此，我们可以为每个类别 $\omega_i$ 定义一个**[判别函数](@entry_id:637860)（discriminant function）** $g_i(\mathbf{x})$：

$g_i(\mathbf{x}) = \ln p(\mathbf{x} | \omega_i) + \ln P(\omega_i)$

在忽略先验概率（或假设其相等）时，[判别函数](@entry_id:637860)简化为 $g_i(\mathbf{x}) = \ln p(\mathbf{x} | \omega_i)$。分类决策规则就是将像素 $\mathbf{x}$ 划分到使其[判别函数](@entry_id:637860)值最大的类别：

$\hat{\omega} = \arg\max_i g_i(\mathbf{x})$

为了使该框架具有可操作性，我们必须为 $p(\mathbf{x} | \omega_i)$ 选择一个具体的数学模型。在遥感领域，一个经过充分检验且广泛应用的模型是**[多元正态分布](@entry_id:175229)（multivariate normal distribution）**，也称为高斯分布。该模型假设，对于给定的地物类别，其在多个光谱波段上的[反射率](@entry_id:172768)（构成了[特征向量](@entry_id:151813) $\mathbf{x}$）服从一个联合的正态分布。

一个 $d$ 维[多元正态分布](@entry_id:175229)由其**[均值向量](@entry_id:266544)（mean vector）** $\boldsymbol{\mu} \in \mathbb{R}^d$ 和**协方差矩阵（covariance matrix）** $\boldsymbol{\Sigma} \in \mathbb{R}^{d \times d}$ 完全定义。[均值向量](@entry_id:266544) $\boldsymbol{\mu}$ 代表了该类别在特征空间中的中心位置，而[协方差矩阵](@entry_id:139155) $\boldsymbol{\Sigma}$ 则描述了该类别数据点的离散程度、各个特征维度上的方差以及特征之间的相关性，共同决定了该类别数据簇的形状、大小和朝向。其[概率密度函数](@entry_id:140610)（PDF）为：

$p(\mathbf{x} | \boldsymbol{\mu}, \boldsymbol{\Sigma}) = \frac{1}{(2\pi)^{d/2} |\boldsymbol{\Sigma}|^{1/2}} \exp\left(-\frac{1}{2}(\mathbf{x} - \boldsymbol{\mu})^T \boldsymbol{\Sigma}^{-1} (\mathbf{x} - \boldsymbol{\mu})\right)$

其中 $|\boldsymbol{\Sigma}|$ 是协方差[矩阵的行列式](@entry_id:148198)。

### 决策边界：从二次到线性

将[多元正态分布](@entry_id:175229)模型代入[判别函数](@entry_id:637860)，我们可以揭示[最大似然](@entry_id:146147)分类器在[特征空间](@entry_id:638014)中划分区域的几何性质。对于类别 $\omega_i$，其参数为 $(\boldsymbol{\mu}_i, \boldsymbol{\Sigma}_i)$，忽略与类别无关的常数项后，其[对数似然](@entry_id:273783)[判别函数](@entry_id:637860)为：

$g_i(\mathbf{x}) = -\frac{1}{2}\ln|\boldsymbol{\Sigma}_i| - \frac{1}{2}(\mathbf{x} - \boldsymbol{\mu}_i)^T \boldsymbol{\Sigma}_i^{-1} (\mathbf{x} - \boldsymbol{\mu}_i)$

这是一个关于[特征向量](@entry_id:151813) $\mathbf{x}$ 的**二次函数**。两个类别 $\omega_i$ 和 $\omega_j$ 之间的**决策边界（decision boundary）** 是由满足 $g_i(\mathbf{x}) = g_j(\mathbf{x})$ 的所有点构成的集合。由于[判别函数](@entry_id:637860)是二次的，这个边界通常是一个**超[二次曲面](@entry_id:264390)（hyperquadric）**。在二维[特征空间](@entry_id:638014)中，这对应于圆、椭圆、抛物线或[双曲线](@entry_id:174213)。

考虑一个更一般的情形，即包含先验概率的贝叶斯[判别函数](@entry_id:637860) $g_i(\mathbf{x}) = \ln p(\mathbf{x} | \omega_i) + \ln P(\omega_i)$。两个类别（例如植被 $\mathcal{V}$ 和水体 $\mathcal{W}$）的[判别函数](@entry_id:637860)之差 $\Delta(\mathbf{x}) = g_{\mathcal{V}}(\mathbf{x}) - g_{\mathcal{W}}(\mathbf{x})$ 决定了[分类结果](@entry_id:924005)。如果 $\Delta(\mathbf{x}) > 0$，则将像素归为植被类，反之则归为水体类。其完整形式为 ：

$\Delta(\mathbf{x}) = \frac{1}{2}\left[ (\mathbf{x} - \boldsymbol{\mu}_{\mathcal{W}})^{\top} \boldsymbol{\Sigma}_{\mathcal{W}}^{-1} (\mathbf{x} - \boldsymbol{\mu}_{\mathcal{W}}) - (\mathbf{x} - \boldsymbol{\mu}_{\mathcal{V}})^{\top} \boldsymbol{\Sigma}_{\mathcal{V}}^{-1} (\mathbf{x} - \boldsymbol{\mu}_{\mathcal{V}}) \right] + \frac{1}{2}\ln\left(\frac{|\boldsymbol{\Sigma}_{\mathcal{W}}|}{|\boldsymbol{\Sigma}_{\mathcal{V}}|}\right) + \ln\left(\frac{P(\mathcal{V})}{P(\mathcal{W})}\right)$

当每个类别拥有其独特的[协方差矩阵](@entry_id:139155)（即 $\boldsymbol{\Sigma}_{\mathcal{V}} \neq \boldsymbol{\Sigma}_{\mathcal{W}}$，称为**异方差性 (heteroscedasticity)**）时，$\mathbf{x}$ 的二次项 $(\mathbf{x}^T \boldsymbol{\Sigma}^{-1} \mathbf{x})$ 无法抵消，导致了二次决策边界。这允许分类器为不同形状和方向的数据簇建模。

然而，在一种重要的特殊情况下，分类器会大大简化。如果我们假设所有类别共享一个**共同的[协方差矩阵](@entry_id:139155)**（即 $\boldsymbol{\Sigma}_i = \boldsymbol{\Sigma}$ 对所有 $i$ 成立，称为**[同方差性](@entry_id:634679) (homoscedasticity)**），那么[判别函数](@entry_id:637860)中的二次项 $\mathbf{x}^T \boldsymbol{\Sigma}^{-1} \mathbf{x}$ 和行列式项 $\ln|\boldsymbol{\Sigma}|$ 对于所有类别都将相同，可以在比较中被忽略。此时，[判别函数](@entry_id:637860)之差 $\Delta(\mathbf{x})$ 简化为一个关于 $\mathbf{x}$ 的**线性函数** ：

$\Delta(\mathbf{x}) = (\boldsymbol{\mu}_{\mathcal{V}} - \boldsymbol{\mu}_{\mathcal{W}})^{\top}\boldsymbol{\Sigma}^{-1}\mathbf{x} - \frac{1}{2}\boldsymbol{\mu}_{\mathcal{V}}^{\top}\boldsymbol{\Sigma}^{-1}\boldsymbol{\mu}_{\mathcal{V}} + \frac{1}{2}\boldsymbol{\mu}_{\mathcal{W}}^{\top}\boldsymbol{\Sigma}^{-1}\boldsymbol{\mu}_{\mathcal{W}} + \ln\left(\frac{P(\mathcal{V})}{P(\mathcal{W})}\right)$

该函数形式为 $\mathbf{w}^T\mathbf{x} + b$，其中权重向量 $\mathbf{w} = \boldsymbol{\Sigma}^{-1}(\boldsymbol{\mu}_{\mathcal{V}} - \boldsymbol{\mu}_{\mathcal{W}})$，偏置项 $b$ 是不依赖于 $\mathbf{x}$ 的常数。[决策边界](@entry_id:146073) $\Delta(\mathbf{x})=0$ 成为一个**[超平面](@entry_id:268044)（hyperplane）**。这种简化版的分类器被称为**[线性判别分析](@entry_id:178689)（Linear Discriminant Analysis, LDA）**。

### 实践中的参数估计与分类

理论模型的确立离不开从真实数据中估计其参数 $(\boldsymbol{\mu}_i, \boldsymbol{\Sigma}_i)$ 的能力。这通常通过对已知地物类别的**训练样本（training samples）** 进行**[最大似然估计](@entry_id:142509)（Maximum Likelihood Estimation, MLE）** 来完成。

对于来自某个类别的一组 $N$ 个[独立同分布](@entry_id:169067)的训练样本 $\{\mathbf{x}_1, \dots, \mathbf{x}_N\}$，其均值和协方差的MLE被证明恰好是**样本均值**和**样本协方差** ：

$\hat{\boldsymbol{\mu}} = \frac{1}{N} \sum_{k=1}^{N} \mathbf{x}_k$

$\hat{\boldsymbol{\Sigma}} = \frac{1}{N} \sum_{k=1}^{N} (\mathbf{x}_k - \hat{\boldsymbol{\mu}})(\mathbf{x}_k - \hat{\boldsymbol{\mu}})^T$

一旦我们为每个类别 $\omega_i$ 估计出其参数 $\hat{\boldsymbol{\mu}}_i$ 和 $\hat{\boldsymbol{\Sigma}}_i$，我们就可以对任何一个新的、未标记的像素 $\mathbf{x}_{new}$ 进行分类。我们只需计算该像素在每个类别模型下的对数似然值，并将其归入似然值最高的类别。

让我们通过一个具体的例子来演示整个流程 。假设我们有两个类别——水体和植被，以及它们在三个波段（蓝、红、近红外）上的7个训练样本。我们的任务是分类一个新像素 $\mathbf{x} = (0.052, 0.031, 0.022)^T$。

1.  **参数估计**：
    *   对于水体类别，我们计算其样本均值和协方差矩阵，得到 $\hat{\boldsymbol{\mu}}_1 = (0.05, 0.03, 0.02)^T$ 和一个对角的协方差矩阵 $\hat{\boldsymbol{\Sigma}}_1$。
    *   同样地，我们为植被类别计算出 $\hat{\boldsymbol{\mu}}_2 = (0.06, 0.08, 0.45)^T$ 和 $\hat{\boldsymbol{\Sigma}}_2$。

2.  **计算[对数似然](@entry_id:273783)**：
    对于新像素 $\mathbf{x}$，我们分别计算其属于水体和植被的对数似然。这等价于计算[判别函数](@entry_id:637860) $g_i(\mathbf{x})$。两者的差值，即**[对数似然比](@entry_id:274622)（log-likelihood ratio）** $\Lambda(\mathbf{x}) = g_1(\mathbf{x}) - g_2(\mathbf{x})$，直接决定了[分类结果](@entry_id:924005)。
    
    $\Lambda(\mathbf{x}) = \frac{1}{2}\ln\left(\frac{|\hat{\boldsymbol{\Sigma}}_2|}{|\hat{\boldsymbol{\Sigma}}_1|}\right) - \frac{1}{2}\left( D_1^2(\mathbf{x}) - D_2^2(\mathbf{x}) \right)$
    
    其中 $D_i^2(\mathbf{x}) = (\mathbf{x}-\hat{\boldsymbol{\mu}}_i)^T \hat{\boldsymbol{\Sigma}}_i^{-1} (\mathbf{x}-\hat{\boldsymbol{\mu}}_i)$ 是像素 $\mathbf{x}$ 到类别 $i$ 中心的**马氏距离（Mahalanobis distance）** 的平方。

3.  **分类决策**：
    通过代入数值，我们发现像素 $\mathbf{x}$ 与水体中心的马氏距离非常小（$D_1^2 \approx 0.315$），而与植被中心的[马氏距离](@entry_id:269828)非常大（$D_2^2 \approx 266.35$）。这表明该像素在特征空间中与水体类别的数据分布极为吻合，而与植被类别格格不入。最终计算出的[对数似然比](@entry_id:274622)为一个很大的正数（$\Lambda(\mathbf{x}) \approx 136.4$），因此，该像素被坚定地分类为**水体**。

### 实际考量与[模型优化](@entry_id:637432)

将理论模型应用于现实世界的遥感数据时，会遇到一系列挑战，需要对基本模型进行调整和优化。

#### [数据预处理](@entry_id:197920)的影响

遥感数据在用于分类之前，通常需要进行[辐射定标](@entry_id:1130520)和[大气校正](@entry_id:1121189)等**预处理**步骤，将原始的数字量（DN）值转换为具有物理意义的[反射率](@entry_id:172768)或亮度值。这些[预处理](@entry_id:141204)步骤通常可以近似为对原始[特征向量](@entry_id:151813) $\mathbf{x}_r$ 的一次**[仿射变换](@entry_id:144885)（affine transformation）**：$\mathbf{x} = \mathbf{B}\mathbf{x}_r + \mathbf{c}$ 。

如果原始数据 $\mathbf{x}_r$ 服从正态分布 $\mathcal{N}(\boldsymbol{\mu}^{(r)}, \boldsymbol{\Sigma}^{(r)})$，那么经过线性变换后的数据 $\mathbf{x}$ 仍然服从正态分布，其参数会相应地变换：

$\boldsymbol{\mu}_{new} = \mathbf{B}\boldsymbol{\mu}^{(r)} + \mathbf{c}$

$\boldsymbol{\Sigma}_{new} = \mathbf{B}\boldsymbol{\Sigma}^{(r)}\mathbf{B}^T$

这意味着我们可以在原始数据域估计参数，然后将其转换到预处理后的空间，或者直接在预处理后的数据上进行[参数估计](@entry_id:139349)。理解这种变换关系对于确保模型在不同数据处理阶段的一致性至关重要。

#### 数值稳定性与正则化

当训练样本数量有限或特征之间高度相关时，估计出的样本协方差矩阵 $\hat{\boldsymbol{\Sigma}}$ 可能变得**病态（ill-conditioned）** 或接近奇异，导致其行列式接近于零且其逆矩阵 $\hat{\boldsymbol{\Sigma}}^{-1}$ 的计算变得极不稳定。这会严重破坏分类器的性能。

一个常见的解决方案是**正则化（regularization）**。**岭正则化（Ridge regularization）** 是一种简单而有效的方法，它通过向协方差矩阵添加一个小的单位矩阵“扰动”来改善其条件数 ：

$\boldsymbol{\Sigma}_{\lambda} = \hat{\boldsymbol{\Sigma}} + \lambda\mathbf{I}$

其中 $\lambda > 0$ 是[正则化参数](@entry_id:162917)，$\mathbf{I}$ 是[单位矩阵](@entry_id:156724)。此操作会使 $\hat{\boldsymbol{\Sigma}}$ 的所有特征值 $\mu_i$ 都增加 $\lambda$，变为 $\mu_i + \lambda$。矩阵的**[条件数](@entry_id:145150)** $\kappa(\boldsymbol{\Sigma}) = \mu_{\max} / \mu_{\min}$ 是衡量其病态程度的指标，值越大表示越病态。正则化后的条件数变为 $\kappa(\boldsymbol{\Sigma}_{\lambda}) = (\mu_{\max}+\lambda)/(\mu_{\min}+\lambda)$。由于 $\mu_{\max} > \mu_{\min}$，这个函数是关于 $\lambda$ 的单调递减函数。因此，通过选择合适的 $\lambda$，我们可以将[条件数](@entry_id:145150)控制在一个可接受的范围内（例如，$\kappa^{\star} \leq 250$），从而确保数值计算的稳定性。所需的最小 $\lambda$ 可以通过求解方程 $\kappa(\boldsymbol{\Sigma}_{\lambda}) = \kappa^{\star}$ 推导得出：

$\lambda = \frac{\mu_{\max} - \kappa^{\star} \mu_{\min}}{\kappa^{\star} - 1}$

这个公式为在实践中选择正则化强度提供了一个有原则的依据。

#### 对异常值的稳健性：[学生t分布](@entry_id:267063)

标准MLC对**异常值（outliers）** 非常敏感。训练样本中的一个极端异[常点](@entry_id:164624)就可能极大地扭曲样本均值和样本协方差的估计，从而导致决策边界的严重偏移。

为了提高分类器的**稳健性（robustness）**，我们可以用**多元[学生t分布](@entry_id:267063)（multivariate Student-t distribution）** 替代正态分布 。[学生t分布](@entry_id:267063)拥有比正态分布更“重”的尾部，这意味着它能更好地容纳远离数据中心的点，而不会对核心分布的[参数估计](@entry_id:139349)产生过大影响。

[学生t分布](@entry_id:267063)的概率密度函数形式更为复杂，其参数（位置、[尺度矩阵](@entry_id:172232)和自由度 $\nu$）的MLE没有[闭式](@entry_id:271343)解，通常需要通过[迭代算法](@entry_id:160288)（如**[期望最大化](@entry_id:273892)（Expectation-Maximization, EM）算法**）来求解。在EM框架下，这表现为一个**迭代重加权方案**：在每次迭代中，根据每个样本点到当前分布中心的马氏距离来计算其权重。距离越远的点（潜在的异常值）获得的权重越低。然后，使用这些权重来更新参数的估计值。这个过程反复进行，直到参数收敛。最终得到的分类器对[训练集](@entry_id:636396)中的异常值具有更强的抵抗力。

### 高级主题与扩展

最大似然分类的原理框架可以扩展到更复杂的场景，并与现代机器学习领域的前沿思想相连接。

#### 维度灾难与特征[可分性](@entry_id:143854)

一个自然的问题是：使用更多的光谱波段（即增加特征空间的维度 $d$）是否总能提高分类精度？答案并非如此简单，这涉及到**[维度灾难](@entry_id:143920)（curse of dimensionality）** 的概念 。

从理论上讲，如果我们知道每个类别真实的概率分布，那么增加一个包含区分信息的特征（即该特征在不同类别间的分布有差异），分类的**渐进[贝叶斯误差](@entry_id:1121477)（asymptotic Bayes error）**（即理论上的最小可能误差）绝不会增加，只会保持不变或降低。像**巴氏距离（Bhattacharyya distance）** 这样的类别**[可分性](@entry_id:143854)（separability）** 度量，在条件独立特征下是可加的，这意味着增加有用的特征总会提升理论上的[可分性](@entry_id:143854)。

然而，在实践中，我们总是使用**有限的训练样本**来估计模型参数。[协方差矩阵](@entry_id:139155) $\boldsymbol{\Sigma}$ 的参数数量随维度 $d$ 以 $O(d^2)$ 的速度增长。当 $d$ 增加时，为了准确估计这些参数，所需的训练样本数量会急剧增加。对于固定的[训练集](@entry_id:636396)大小，维度过高会导致参数估计的误差非常大，这种[估计误差](@entry_id:263890)带来的负面影响最终会超过新增维度所提供的信息增益。这种现象被称为**[休斯现象](@entry_id:1126204)（Hughes phenomenon）**。其结果是，分类精度会随着维度的增加先上升，在达到某个最佳维度 $d^\star$ 后，反而开始下降。

#### 混合像元建模

在遥感影像中，一个像素的地面覆盖往往不是单一纯净的，而是多种地物的混合，这就是**混合像元（mixed pixel）** 问题。例如，一个像素可能部分是植被，部分是土壤。简单的MLC假设每个像素属于单一类别，无法妥善处理这种情况。

我们可以通过构建更复杂的生成模型来应对。一个常用的方法是**[线性混合模型](@entry_id:895469)（linear mixture model）** 。该模型假设一个混合像元的观测向量 $\mathbf{x}$ 是其组成端元（endmembers，即纯净地物）的光谱特征 $\boldsymbol{\mu}_i$ 的[线性组合](@entry_id:154743)，加上噪声 $\boldsymbol{\varepsilon}$：

$\mathbf{x} = f \boldsymbol{\mu}_{V} + (1 - f)\boldsymbol{\mu}_{S} + \boldsymbol{\varepsilon}$

这里，$f$ 是植被的**亚像元丰度（sub-pixel fraction）**。我们可以将[分类问题](@entry_id:637153)构建为一个[假设检验](@entry_id:142556)问题：例如，检验像素是纯植被（$H_V$）还是植被与土壤的混合物（$H_M$）。由于 $H_M$ 包含未知参数 $f$，我们可以使用**广义[似然比检验](@entry_id:1127231)（generalized likelihood ratio test）**。具体做法是，在 $H_M$ 假设下，找到使[似然函数](@entry_id:921601)最大化的最优丰度值 $\hat{f}$，然后比较 $H_M$ 在 $\hat{f}$ 下的最大似然与 $H_V$ 的似然。这种方法将MLC从简单的类别分配扩展到了更精细的亚像元组分分析。

#### [半监督学习](@entry_id:636420)与[EM算法](@entry_id:274778)

在许多实际应用中，获取大量带有精确标签的训练样本成本高昂，而未标记的样本则唾手可得。**[半监督学习](@entry_id:636420)（Semi-supervised learning）** 旨在同时利用少量有标签数据和大量无标签数据来提升学习性能。

最大似然分类的框架可以很自然地扩展到半监督场景中，尤其是当与[EM算法](@entry_id:274778)结合时 。我们可以将整个数据集（有标签和无标签）看作一个[高斯混合模型](@entry_id:634640)（GMM）的观测。

**[EM算法](@entry_id:274778)**在此场景下的工作流程如下：
1.  **初始化**：使用少量有标签数据来初步估计每个类别（[混合模型](@entry_id:266571)的每个组件）的参数 $(\boldsymbol{\mu}_i, \boldsymbol{\Sigma}_i)$ 以及[混合比](@entry_id:1127970)例（即先验概率） $\pi_i$。
2.  **E-步（期望步）**：对于所有**无标签**数据点，根据当前的模型参数，计算它们分别属于每个类别的后验概率（称为**责任（responsibilities）**）。这些责任值可以看作是“软”标签。
3.  **M-步（最大化步）**：使用**所有**数据来重新估计模型参数。对于有标签数据，其类别归属是确定的（责任为1或0）；对于无标签数据，则使用E-步计算出的[软标签](@entry_id:1131857)进行加权。例如，更新[混合比](@entry_id:1127970)例 $\pi_i$ 时，其分子是类别 $i$ 的有标签样本数，加上所有无标签样本对类别 $i$ 的责任之和。
4.  **迭代**：重复E-步和M-步，直到模型参数收敛。

通过这种方式，大量无标签数据中蕴含的关于数据整体分布结构的信息被用来辅助和修正仅从少量有标签数据中获得的[参数估计](@entry_id:139349)，从而得到一个更准确、更具泛化能力的分类器。