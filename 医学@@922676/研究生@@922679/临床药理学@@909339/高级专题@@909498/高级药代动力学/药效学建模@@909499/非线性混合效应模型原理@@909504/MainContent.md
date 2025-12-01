## 引言
在现代生物医学研究，尤其是临床药理学领域，我们面对的数据往往具有复杂的分层结构：来自不同个体的观测数据共同构成一个群体，而每个个体内部又包含多次重复测量。如何从这些稀疏或密集的纵向数据中提取有价值的信息，同时准确地描述和区分群体共性与个体差异，是非线性混合效应（Nonlinear Mixed-effects, NLME）模型旨在解决的核心问题。作为一种强大的统计分析工具，NL[ME模型](@entry_id:261918)为分析具有[多源](@entry_id:170321)变异性的数据提供了一个严谨而灵活的框架，已成为定量药理学、[药物开发](@entry_id:169064)和个体化医疗的基石。

本文旨在系统性地剖析NL[ME模型](@entry_id:261918)的原理、机制与应用。我们将带领读者穿越理论的深度与实践的广度，构建对这一复杂工具的全面理解。在第一章“原理与机制”中，您将学习到NL[ME模型](@entry_id:261918)的分层结构，理解它如何巧妙地将总变异分解为个体间变异和残差变异，并探讨参数估计所面临的根本挑战以及主流的解决方法。随后，在第二章“应用与交叉学科联系”中，我们将展示这些理论如何在药物动力学（PK）、药效学（PD）、特殊人群研究以及其他科学领域中转化为解决实际问题的有力工具。最后，通过第三章“动手实践”中的具体问题，您将有机会巩固所学知识，将理论应用于模拟的真实场景。这趟学习之旅将为您在未来的定量研究中运用NL[ME模型](@entry_id:261918)奠定坚实的基础。

## 原理与机制

本章旨在阐述非线性混合效应 (Nonlinear Mixed-effects, NLME) 模型的核心原理与关键机制。我们将从其分层结构开始，系统性地剖析模型如何区分变异的不同来源，探讨[参数估计](@entry_id:139349)所面临的根本挑战，介绍主流的估计算法，并最终讨论模型评估与诊断的关键概念。本章内容假定读者已对NL[ME模型](@entry_id:261918)在临床药理学等领域的重要性有初步了解。

### NL[ME模型](@entry_id:261918)的分层结构

群体数据的内在结构具有层次性：在每个个体内部存在多次测量，而众多独立的个体则共同构成一个群体。NL[ME模型](@entry_id:261918)通过其精巧的分层结构，精确地反映了这一现实。一个完整的NL[ME模型](@entry_id:261918)通常可以解构为两个核心部分：个体模型（第一阶段）和群体模型（第二阶段）。

#### 第一阶段：个体模型

个体模型描述了在单个受试者内部发生的生理或药理过程，并关联了该过程的理论预测与实际观测值。它包含两个关键组成部分：结构模型和残差变异模型。

**结构模型 (Structural Model)**

结构模型是描述核心动态过程的数学函数，通常以[微分](@entry_id:158422)方程或其解析解的形式出现。它定义了在没有测量误差和随机波动的情况下，个体的理论响应（如血药浓度）如何随时间等[自变量](@entry_id:267118)变化。我们将其表示为 $f(t_{ij}, \phi_i)$，其中 $t_{ij}$ 是个体 $i$ 在第 $j$ 个时间点的采样时间，而 $\phi_i$ 是一个向量，包含了描述个体 $i$ 独特生理特征的参数（例如，药物的清除率 $CL_i$ 或分布容积 $V_i$）。

**残差变异模型 (Residual Error Model)**

实际观测值 $y_{ij}$ 很少与理论预测值 $f(t_{ij}, \phi_i)$ 完全吻合。两者的差异被归因于 **残差不可解释变异 (residual unexplained variability, RUV)**，用符号 $\epsilon_{ij}$ 表示。这种变异涵盖了多种来源，包括测量误差、模型设定不准确、以及个体内部随时间发生的短期生理波动。观测模型因此写为：

$y_{ij} = f(t_{ij}, \phi_i) + \epsilon_{ij}$

残差误差通常被假定为均值为零，即 $E[\epsilon_{ij}] = 0$。然而，其方差结构对模型至关重要，因为它决定了每次观测在[参数估计](@entry_id:139349)中的权重。常见的残差误差模型有以下几种 [@problem_id:4568901]：

1.  **加性误差模型 (Additive Error Model)**:
    $y_{ij} = f_{ij} + \epsilon_{\mathrm{add},ij}$，其中 $\epsilon_{\mathrm{add},ij} \sim \mathcal{N}(0, \sigma_{\mathrm{add}}^2)$。
    在这种模型下，观测值的方差是恒定的：$\operatorname{Var}(y_{ij} | f_{ij}) = \sigma_{\mathrm{add}}^2$。这适用于在整个测量范围内，误差大小与预测值无关的情况。

2.  **比例误差模型 (Proportional Error Model)**:
    $y_{ij} = f_{ij}(1 + \epsilon_{\mathrm{prop},ij})$，其中 $\epsilon_{\mathrm{prop},ij} \sim \mathcal{N}(0, \sigma_{\mathrm{prop}}^2)$。
    观测值的方差与预测值的平方成正比：$\operatorname{Var}(y_{ij} | f_{ij}) = f_{ij}^2 \sigma_{\mathrm{prop}}^2$。这种模型的[变异系数](@entry_id:272423) (coefficient of variation, CV) 是恒定的，等于 $\sigma_{\mathrm{prop}}$，因此常用于描述误差随浓度升高而增大的情况。

3.  **组合误差模型 (Combined Error Model)**:
    $y_{ij} = f_{ij}(1 + \epsilon_{\mathrm{prop},ij}) + \epsilon_{\mathrm{add},ij}$，其中 $\epsilon_{\mathrm{add},ij}$ 和 $\epsilon_{\mathrm{prop},ij}$ 相互独立。
    其方差为 $\operatorname{Var}(y_{ij} | f_{ij}) = \sigma_{\mathrm{add}}^2 + f_{ij}^2 \sigma_{\mathrm{prop}}^2$。该模型兼具加性误差和比例误差的特点，在低浓度时由加性部分主导，在高浓度时由比例部分主导，具有很强的灵活性。

在[加权最小二乘法](@entry_id:177517) (Weighted Least Squares, WLS) 估计中，每个观测的权重 $w_{ij}$ 应与观测方差的倒数成正比。因此，对于加性误差模型，$w_{ij} \propto 1$；对于比例误差模型，$w_{ij} \propto 1/f_{ij}^2$；对于组合误差模型，$w_{ij} \propto 1/(\sigma_{\mathrm{add}}^2 + f_{ij}^2 \sigma_{\mathrm{prop}}^2)$ [@problem_id:4568901]。

#### 第二阶段：群体模型

个体模型描述了“个体内部的动态”，而群体模型则描述了“个体之间的差异”。它通过一个 **参数模型** 将个体参数 $\phi_i$ 与群体平均特征以及个体间的差异联系起来。

**固定效应、随机效应与协变量**

参数模型的一般形式为 $\phi_i = h(\theta, z_i, \eta_i)$，其中：
-   $\theta$ 是 **固定效应 (fixed effects)** 向量，代表了群体参数的“典型值” (typical value)。例如，群体平均的清除率。在频率学派框架下，$\theta$ 是一个未知的固定常数。
-   $z_i$ 是个体 $i$ 的 **协变量 (covariates)** 向量，如体重、年龄、肾功能指标等。协变量可以解释部分个体间的参数差异。
-   $\eta_i$ 是 **随机效应 (random effects)** 向量，代表了个体 $i$ 的参数相对于群体典型值的、未被协变量所解释的偏离。这部分变异被称为 **个体间变异 (inter-individual variability, IIV)**。

随机效应 $\eta_i$ 被假定为从一个群体分布中抽取的随机变量，最常见的假设是[多元正态分布](@entry_id:175229)，其均值为零，协方差矩阵为 $\Omega$：

$\eta_i \sim \mathcal{N}(0, \Omega)$

均值为零是因为任何系统性的偏移都应被纳入固定效应 $\theta$ 中。协方差矩阵 $\Omega$ 则量化了个体间变异的大小（对角线元素 $\omega_k^2$）以及不同参数之间变异的相关性（非对角[线元](@entry_id:196833)素）。

**参数模型的构建：以[对数正态模型](@entry_id:270159)为例**

许多药代动力学参数（如清除率、容积）在生理上必须为正值。为了在模型中确保这一点，常使用 **对数正态 (log-normal)** [参数化](@entry_id:265163) [@problem_id:4568856]。例如，个体清除率 $CL_i$ 可以建模为：

$CL_i = \theta_{CL} \exp(\eta_{i,CL})$

其中 $\theta_{CL}$ 是群体典型清除率，$\eta_{i,CL} \sim \mathcal{N}(0, \omega_{CL}^2)$。由于指数函数 $\exp(\eta_{i,CL})$ 永远为正，因此 $CL_i$ 也保证为正。这种模型结构也体现了 **[乘性](@entry_id:187940)变异 (multiplicative variability)**，即个体的差异是以相对于典型值的“比例”形式存在的。

在这种[参数化](@entry_id:265163)下，个体参数 $CL_i$ 服从对数正态分布。值得注意的是，固定效应 $\theta_{CL}$ 代表的是 $CL_i$ 分布的 **[几何均值](@entry_id:275527) (geometric mean)** 和 **中位数 (median)**，而不是算术均值。其算术均值为 $E[CL_i] = \theta_{CL} \exp(\omega_{CL}^2/2)$，由于 $\omega_{CL}^2 > 0$，该均值总是大于中位数 $\theta_{CL}$，这反映了[对数正态分布](@entry_id:261888)的右偏特性 [@problem_id:4568856]。

将这两个阶段结合起来，我们就得到了一个完整的NL[ME模型](@entry_id:261918)规范。它精确定义了每个参数的角色、随机变量的分布假设，以及模型中各个组件之间的独立性关系 [@problem_id:4568883]。

### 变异来源的分离

NL[ME模型](@entry_id:261918)的核心优势之一在于能够将数据的总变异分解为不同的、有生理学意义的组成部分。具体而言，它能够清晰地分离 **个体间变异 (IIV)** 和 **残差不可解释变异 (RUV)**。

根据[全方差公式](@entry_id:177482) (Law of Total Variance)，对于任意一个个体 $i$ 的观测 $Y_{ij}$，其总方差可以分解为 [@problem_id:4568925]：

$\operatorname{Var}(Y_{ij}) = \mathbb{E}[\operatorname{Var}(Y_{ij} \mid \eta_i)] + \operatorname{Var}(\mathbb{E}[Y_{ij} \mid \eta_i])$

让我们来解析这个公式的两个组成部分：
-   **第一项: $\mathbb{E}[\operatorname{Var}(Y_{ij} \mid \eta_i)]$**: 这是在给定个体随机效应 $\eta_i$ （即给定个体）的条件下，观测值 $Y_{ij}$ 的方差的期望。$\operatorname{Var}(Y_{ij} \mid \eta_i)$ 就是个体内部的残差方差 $\operatorname{Var}(\epsilon_{ij})$。因此，这一项代表了 **残差不可解释变异 (RUV)**。
-   **第二项: $\operatorname{Var}(\mathbb{E}[Y_{ij} \mid \eta_i])$**: 这是在给定 $\eta_i$ 条件下，$Y_{ij}$ 的期望的方差。$\mathbb{E}[Y_{ij} \mid \eta_i]$ 正是个体的理论预测曲线 $f(t_{ij}, \phi_i)$。因此，这一项衡量了个体预测曲线在群体中的波动程度，它源于个体参数 $\phi_i$ 的差异，即 **个体间变异 (IIV)**。

这种变异的[分离能](@entry_id:754696)力并非凭空而来，它依赖于研究设计。如果每个个体只有一个观测数据点，那么IIV和RUV的贡献就会混淆在一起，我们只能估计它们的总和，而无法区分彼此。只有当每个个体提供 **多个观测数据** 时，我们才能表征个体内部的变异（RUV），并将其与个体之间的变异（IIV）区分开来。在一个设计良好的研究中，增加每个个体的样本数量和优化采样时间点，能够提供更丰富的信息，从而更精确地估计 $\Omega$ (IIV) 和残差方差参数 (RUV) [@problem_id:4568925]。

### 参数估计：[边际似然](@entry_id:636856)的挑战

在NL[ME模型](@entry_id:261918)中，我们的目标是估计群体的固定效应参数 ($\theta$) 和方差参数 ($\Omega$ 和残差方差 $\sigma^2$）。由于随机效应 $\eta_i$ 是未观测到的潜变量，我们不能直接使用基于 $p(y_i, \eta_i)$ 的全数据似然。相反，我们必须通过对随机效应的所有可[能值](@entry_id:187992)进行积分，来得到观测数据 $y_i$ 的 **边际似然 (marginal likelihood)**。

对于单个个体 $i$，其[边际似然](@entry_id:636856) $L_i$ 定义为：

$L_i(\theta, \Omega, \Sigma) = p(y_i | \theta, \Omega, \Sigma) = \int p(y_i, \eta_i | \theta, \Omega, \Sigma) \,d\eta_i = \int p(y_i | \eta_i, \theta, \Sigma) \, p(\eta_i | \Omega) \,d\eta_i$

由于假定个体之间相互独立，整个群体的边际[对数似然](@entry_id:273783) (marginal log-likelihood) 就是所有个体边际[对数似然](@entry_id:273783)的总和：

$\ell(\theta, \Omega, \Sigma) = \sum_{i=1}^N \log L_i(\theta, \Omega, \Sigma) = \sum_{i=1}^N \log \left[ \int p(y_i | \eta_i, \theta, \Sigma) \, p(\eta_i | \Omega) \,d\eta_i \right]$

在假定正态分布的随机效应和残差误差下，这个积分的显式形式为 [@problem_id:4568851]：

$\ell(\theta,\Omega,\Sigma) = \sum_{i=1}^N \log \int_{\mathbb{R}^q} \mathcal{N}(y_i; f_i(\theta,\eta_i), \Sigma_i(\theta)) \cdot \mathcal{N}(\eta_i; 0, \Omega) \,d\eta_i$

这里的 $\mathcal{N}(\cdot)$ 表示正态分布的概率密度函数。这个积分是NLME[模型[参数估](@entry_id:752080)计](@entry_id:139349)的核心挑战。

**为何积分通常是难解的？**

积分是否具有解析解（closed-form solution），完全取决于结构模型 $f_i(\theta, \eta_i)$ 对于随机效应 $\eta_i$ 的形式 [@problem_id:4568927]。

-   **在线性混合效应模型 (LME)** 中，结构模型是 $\eta_i$ 的线性函数，例如 $f_i(\theta, \eta_i) = X_i\theta + Z_i\eta_i$。在这种情况下，观测值 $y_i$ 是两个正态变量（$Z_i\eta_i$ 和 $\epsilon_i$）的[线性组合](@entry_id:155091)，其结果仍然是正态分布。[边际似然](@entry_id:636856)可以被解析计算。

-   **在非线性混合效应模型 (NLME)** 中，结构模型 $f_i(\theta, \eta_i)$ 是 $\eta_i$ 的非线性函数，例如前面提到的 $CL_i = \theta_{CL} \exp(\eta_{i,CL})$。这将导致被积函数（integrand）中的指数项不再是 $\eta_i$ 的二次型。因此，被积函数不是一个正态分布的核，整个积分通常没有解析解。例如，在一个 $y_i = \exp(\theta + \eta_i) + \epsilon_i$ 的简化模型中，观测值 $y_i$ 是一个对数正态变量和一个正态变量之和，其分布的[概率密度函数](@entry_id:140610)没有简单的解析表达式 [@problem_id:4568927]。

正因为[边际似然](@entry_id:636856)的积分是难解的，NLME的参数估计必须依赖于各种[近似算法](@entry_id:139835)。

### 主流估计算法

为了解决[边际似然](@entry_id:636856)的积分难题，研究者们开发了多种算法，主要可分为两大类：基于[似然函数](@entry_id:141927)近似的算法和基于[期望最大化](@entry_id:273892)思想的算法。

#### 基于似然近似的算法

这类方法通过对模型或[似然函数](@entry_id:141927)本身进行近似，将难解的积分转化为可以计算的形式。

-   **一阶法 (First Order, FO)**: FO方法通过在随机效应等于其均值（即 $\eta=0$）处对非线性结构模型 $f(\theta, \eta)$进行一阶泰勒展开来线性化模型。这个近似将NL[ME模型](@entry_id:261918)转化为一个近似的L[ME模型](@entry_id:261918)，其[边际似然](@entry_id:636856)是可解的。然而，FO方法忽略了个体的数据，在所有个体上都使用相同的展开点，因此当个体间变异较大或模型非线性较强时，会产生显著的偏差。

-   **[一阶条件](@entry_id:140702)估计法 (First Order Conditional Estimation, FOCE)**: FOCE方法是对FO的重大改进。它不是在 $\eta=0$ 处，而是在每个个体数据的 **条件[后验众数](@entry_id:174279) (conditional posterior mode)** $\hat{\eta}_i$ 处对模型进行线性化。$\hat{\eta}_i$ 是在给定个体数据 $y_i$ 和当前群体参数下，$\eta_i$ 最可能的值。通过以个体化的方式选择展开点，FOCE能够更好地捕捉个体特征，通常比FO法提供更准确的参数估计。

-   **[拉普拉斯近似](@entry_id:636859) (Laplace Approximation)**: 与其线性化结构模型，[拉普拉斯近似](@entry_id:636859)直接处理边际似然积分。它通过在条件[后验众数](@entry_id:174279) $\hat{\eta}_i$ 处对被积函数的对数进行二阶泰勒展开，将被积[函数近似](@entry_id:141329)为一个正态分布的密度函数。这个近似包含了关于似然函数在 $\hat{\eta}_i$ 处 **曲率 (curvature)** 的信息（通过Hessian矩阵），因此通常比FOCE更准确，尤其是在随机效应的后验分布接近正态时。FOCE可以被视为[拉普拉斯近似](@entry_id:636859)的一个简化版本 [@problem_id:4568919]。

#### [随机近似](@entry_id:270652)[期望最大化算法](@entry_id:165054) (SAEM)

SAEM是另一类强大的估计算法，它属于随机[EM算法](@entry_id:274778)家族。EM（Expectation-Maximization）算法通过迭代执行E步（计算全数据[对数似然](@entry_id:273783)的期望）和[M步](@entry_id:178892)（最大化该期望）来处理含潜变量的模型。在NLME中，标准的E步是难解的。SAEM通过引入模拟步骤来解决这个问题 [@problem_id:4568902]。SA[EM算法](@entry_id:274778)的每一次迭代包含三个核心步骤：

1.  **模拟步 (S-step)**: 在给定当前参数估计 $(\theta^{(k-1)}, \Omega^{(k-1)}, \Sigma^{(k-1)})$ 和个体数据 $y_i$ 的条件下，从每个个体随机效应的后验分布 $p(\eta_i | y_i, \dots)$ 中抽取一个样本 $\eta_i^{(k)}$。由于该后验分布也没有解析形式，通常使用[马尔可夫链蒙特卡洛 (MCMC)](@entry_id:137985) 方法（如[Metropolis-Hastings算法](@entry_id:146870)）进行抽样。

2.  **[随机近似](@entry_id:270652)步 (SA-step)**: 更新全数据[对数似然](@entry_id:273783)的充分统计量 $S$ 的一个 running estimate $S_k$。更新规则为：
    $S_k = S_{k-1} + \gamma_k (S(y, \eta^{(k)}) - S_{k-1})$
    其中 $S(y, \eta^{(k)})$ 是用当前模拟的 $\eta^{(k)}$ 计算出的充分统计量，$\gamma_k$ 是一个步长序列。为了保证算法收敛，$\gamma_k$ 必须满足特定条件（例如，$\sum \gamma_k = \infty$ 且 $\sum \gamma_k^2  \infty$）。通常，在算法初期（burn-in阶段）$\gamma_k=1$，之后平滑地减小。

3.  **最大化步 (M-step)**: 基于更新后的充分统计量 $S_k$，最大化近似的期望全数据[对数似然](@entry_id:273783)，以更新[参数估计](@entry_id:139349)值 $(\theta^{(k)}, \Omega^{(k)}, \Sigma^{(k)})$。

SAEM通过将复杂的积分问题转化为一个更易于处理的模拟和优化序列，在许多NLME问题中表现出良好的收敛性和准确性。

#### 贝叶斯方法

与上述基于最大似然的频率学派方法不同，**贝叶斯方法 (Bayesian methods)** 将所有未知量（包括固定效应 $\theta$、方差参数 $\Omega$ 和 $\Sigma$）都视为随机变量，并为它们指定 **先验分布 (prior distributions)** [@problem_id:4568855]。

一个完整的贝叶斯NL[ME模型](@entry_id:261918)包含：
1.  与频率学派模型相同的[似然函数](@entry_id:141927) $p(y_i | \eta_i, \theta, \Sigma)$ 和随机效应分布 $p(\eta_i | \Omega)$。
2.  为群体参数指定的先验分布 $p(\theta)$、$p(\Omega)$ 和 $p(\Sigma)$。先验的选择应符合参数的定义域（例如，为正值参数选择对数正态先验，为方差选择逆伽马先验，为协方差矩阵选择逆威沙特先验）。

然后，根据[贝叶斯定理](@entry_id:151040)，结合似然和先验，可以得到所有未知量（包括参数和随机效应）的 **联合后验分布 (joint posterior distribution)**：

$p(\theta, \Omega, \Sigma, \{\eta_i\} | \{y_i\}) \propto p(\theta) p(\Omega) p(\Sigma) \prod_{i=1}^n \left[ p(\eta_i | \Omega) \prod_{j=1}^{m_i} p(y_{ij} | \eta_i, \theta, \Sigma) \right]$

由于这个后验分布通常非常复杂，无法解析求解，因此贝叶斯推断依赖于MCMC等采样技术（如Gibbs抽样、Metropolis-Hastings）从后验分布中抽取大量样本，然后基于这些样本对参数进行推断（例如，计算[后验均值](@entry_id:173826)、中位数和[可信区间](@entry_id:176433)）。

### 模型评估与诊断

在拟合了一个或多个NL[ME模型](@entry_id:261918)后，必须对其进行评估和诊断，以确保模型的可靠性并选择最佳模型。

#### [模型选择](@entry_id:155601)：AIC与BIC

当比较两个或多个非嵌套 (non-nested) 模型时，似然比检验 (LRT) 不再适用。此时，**[信息准则](@entry_id:636495) (Information Criteria)**，如[赤池信息准则 (AIC)](@entry_id:193149) 和[贝叶斯信息准则 (BIC)](@entry_id:181959)，成为主要的工具 [@problem_id:4568936]。

-   **AIC (Akaike Information Criterion)**:
    $AIC = -2\ell_{max} + 2k$

-   **BIC (Bayesian Information Criterion)**:
    $BIC = -2\ell_{max} + k \log(N)$

其中，$\ell_{max}$ 是最大化的边际[对数似然](@entry_id:273783)值，$k$ 是模型中自由估计参数的总数（包括所有固定效应、$\Omega$ 和 $\Sigma$ 中的唯一元素），$N$ 是 **独立单元的数量**，在群体分析中即为 **受试者总数**。

AIC和BIC都旨在[平衡模型](@entry_id:636099)的 **拟合优度 (goodness-of-fit)**（由 $-2\ell_{max}$ 体现）和 **模型复杂度 (complexity)**（由惩罚项 $2k$ 或 $k\log(N)$ 体现）。BIC对参数数量的惩罚比AIC更重，因此倾向于选择更简洁的模型。在[模型比较](@entry_id:266577)中，AIC或BIC值 **更低** 的模型被认为是更优的模型。

一个关键的技术要点是：当使用AIC或BIC比较包含不同固定效应（如不同协变量）的模型时，必须使用 **[最大似然](@entry_id:146147)法 (ML)** 得到的 $\ell_{max}$。这是因为限制性[最大似然](@entry_id:146147)法 (REML) 的似然值在不同固定效应结构的模型之间不具有可比性 [@problem_id:4568936]。

#### Shrinkage（收缩）及其对诊断的影响

在[模型拟合](@entry_id:265652)后，我们可以得到每个个体随机效应 $\eta_i$ 的估计值，通常称为 **[经验贝叶斯](@entry_id:171034)估计 (Empirical Bayes Estimates, EBEs)**。这些EBEs是基于群体[先验信息](@entry_id:753750)和个体数据信息得到的后验估计。

**Shrinkage (收缩)** 是指当个体数据信息不足时（例如，采样点稀疏或残差噪音大），EBEs会向其先验均值（即0）“收缩”的现象 [@problem_id:4568905]。收缩程度可以用一个统计量来量化：$s \approx 1 - \operatorname{Var}(\hat{\eta}) / \hat{\Omega}$。当收缩程度高时（$s$ 接近1），$\hat{\eta}_i$ 的分布方差远小于估计的群体方差 $\hat{\Omega}$，说明EBEs主要反映的是群体信息，而非个体信息。

高收缩对[模型诊断](@entry_id:136895)和应用有严重影响：

1.  **掩盖协变量关系**: 协变量探索常通过绘制EBEs（$\hat{\eta}_i$）与协变量（如体重）的散点图来完成。高收缩会使所有的 $\hat{\eta}_i$ 都聚集在0附近，从而压缩散点图的垂直范围，掩盖或减弱本应存在的真实关系，导致更高的II型错误率（即未能发现真实的协变量效应）[@problem_id:4568905]。

2.  **降低诊断图的价值**: 许多诊断图依赖于EBEs。例如，**个体预测值 (IPRED)** 是使用EBEs计算的，而 **群体预测值 (PRED)** 则将所有随机效应设为0。高收缩导致 $\hat{\eta}_i \to 0$，从而使 IPRED $\to$ PRED。这使得“观测值(DV) vs. IPRED”图与“DV vs. PRED”图看起来几乎一样，失去了评估个体层面拟合情况的价值。

3.  **使EBEs不可靠**: 当收缩程度高时，EBEs和IPREDs主要由群体先验驱动，而非个体数据。因此，将这些收缩严重的估计用于个体化决策（如剂量调整）是不可靠的。

与依赖EBEs的诊断图不同，**基于模拟的诊断工具**，如 **可视化预测检验 (Visual Predictive Check, VPC)**，对收缩现象具有鲁棒性。VPC通过从已拟合的群体模型（使用 $\hat{\theta}$, $\hat{\Omega}$, $\hat{\Sigma}$）中模拟出全新的数据集来评估模型性能，这一过程不依赖于原始数据的EBEs。因此，在高收缩的情况下，VPC是评估模型预测性能的更可靠的工具 [@problem_id:4568905]。