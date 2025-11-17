## 引言
在统计分析中，我们经常从数据中计算出样本均值或比例等统计量来估计总体参数。然而，我们最终关注的量往往是这些基本参数的更复杂函数，例如根据平均体重和身高计算的身体[质量指数](@entry_id:190779)（BMI），或根据平均收益率和标准差计算的[夏普比率](@entry_id:136824)。一个根本性的挑战随之而来：我们如何对这些派生出的量进行[统计推断](@entry_id:172747)，比如构建[置信区间](@entry_id:142297)或进行假设检验？这需要我们了解其[抽样分布](@entry_id:269683)，特别是其[方差](@entry_id:200758)。多维[德尔塔方法](@entry_id:276272)（Multivariate Delta Method）正是为解决这一问题提供了强大而优雅的理论框架。

本文旨在提供一份关于多维[德尔塔方法](@entry_id:276272)的全面指南。我们将通过以下章节深入探讨：在“原理与机制”一章中，我们将从其核心思想——通过[泰勒展开](@entry_id:145057)进行线性近似——出发，逐步构建并推导出其核心公式。接着，“应用与跨学科联系”一章将通过探索其在经济学、工程学和生态学等领域的真实世界案例，展示其广泛的通用性。最后，“动手实践”一章将为您提供将该方法应用于具体问题的机会，以巩固您的理解。通过阅读本文，您不仅能掌握其理论，更能领会[德尔塔方法](@entry_id:276272)在现代数据分析中的实践力量。

## 原理与机制

在统计推断中，我们常常从样本数据中计算出某些统计量，例如样本均值或样本比例，以估计总体的相应参数。然而，我们所关心的最终量，往往是这些基本参数的一个更复杂的函数。例如，我们可能通过样本的平均体重和平均身高来估计群体的平均身体[质量指数](@entry_id:190779)（BMI），或者通过测量电路中的平均电压和电流来估计其[平均功率](@entry_id:271791)。为了对这些派生出的量进行[假设检验](@entry_id:142556)或构建[置信区间](@entry_id:142297)，我们必须了解其[抽样分布](@entry_id:269683)的性质，特别是其[方差](@entry_id:200758)。多维[德尔塔方法](@entry_id:276272)（Multivariate Delta Method）为此提供了一个强大而通用的理论框架。

本章将系统地阐述多维[德尔塔方法](@entry_id:276272)的原理和机制。我们将从其核心思想——基于泰勒展开的线性近似——出发，逐步推导出其主要公式，并通过一系列涵盖不同科学与工程领域的实例，展示该方法的具体应用步骤。

### 从一维到多维：核心思想的演进

理解多维[德尔塔方法](@entry_id:276272)的最佳途径是先回顾其在一维情境下的基本逻辑。假设我们有一个样本均值 $\bar{X}_n$，根据[中心极限定理](@entry_id:143108)（Central Limit Theorem），当样本量 $n$ 足够大时，其经过标准化后的[分布](@entry_id:182848)近似于正态分布：

$$
\sqrt{n}(\bar{X}_n - \mu) \xrightarrow{d} N(0, \sigma^2)
$$

其中 $\mu$ 是[总体均值](@entry_id:175446)，$\sigma^2$ 是总体[方差](@entry_id:200758)，$\xrightarrow{d}$ 表示[依分布收敛](@entry_id:275544)。

现在，如果我们对一个参数 $\mu$ 的函数 $g(\mu)$ 感兴趣，并用 $g(\bar{X}_n)$ 来估计它，那么 $g(\bar{X}_n)$ 的[抽样分布](@entry_id:269683)是怎样的呢？[德尔塔方法](@entry_id:276272)告诉我们，可以通过在 $\mu$ 点对函数 $g(x)$ 进行一阶泰勒展开来近似这个[分布](@entry_id:182848)：

$$
g(\bar{X}_n) \approx g(\mu) + g'(\mu)(\bar{X}_n - \mu)
$$

这个线性近似揭示了 $g(\bar{X}_n)$ 的变异性如何依赖于 $\bar{X}_n$ 的变异性。对上式进行移项和标准化，我们可以得到：

$$
\sqrt{n}(g(\bar{X}_n) - g(\mu)) \approx g'(\mu) \sqrt{n}(\bar{X}_n - \mu)
$$

由于 $\sqrt{n}(\bar{X}_n - \mu)$ 渐近服从均值为 0、[方差](@entry_id:200758)为 $\sigma^2$ 的[正态分布](@entry_id:154414)，那么它的[线性变换](@entry_id:149133)也将渐近服从正态分布。其[渐近方差](@entry_id:269933)为：

$$
\text{Var}(g'(\mu) \sqrt{n}(\bar{X}_n - \mu)) = [g'(\mu)]^2 \text{Var}(\sqrt{n}(\bar{X}_n - \mu)) = [g'(\mu)]^2 \sigma^2
$$

这就是**一维[德尔塔方法](@entry_id:276272)**的核心结果。它表明，转换后统计量的[渐近方差](@entry_id:269933)是原统计量[渐近方差](@entry_id:269933)乘以在总体参数处导数平方的因子。

当我们的目标量是多个参数的函数时，这个思想可以自然地推广到多维空间。假设我们有一个 $k$ 维的参数向量 $\boldsymbol{\theta} = (\theta_1, \dots, \theta_k)^T$ 和其对应的估计量向量 $\hat{\boldsymbol{\theta}}_n = (\hat{\theta}_{n,1}, \dots, \hat{\theta}_{n,k})^T$（通常是样本[均值向量](@entry_id:266544)）。**多维中心极限定理 (Multivariate Central Limit Theorem, MCLT)** 指出，在大样本下：

$$
\sqrt{n}(\hat{\boldsymbol{\theta}}_n - \boldsymbol{\theta}) \xrightarrow{d} N(\mathbf{0}, \Sigma)
$$

这里，$\mathbf{0}$ 是一个 $k$ 维零向量，而 $\Sigma$ 是一个 $k \times k$ 的**[协方差矩阵](@entry_id:139155)**，其对角线元素是各个[估计量的方差](@entry_id:167223)，非对角线元素是它们之间的协[方差](@entry_id:200758)。

现在，考虑一个[可微函数](@entry_id:144590) $g: \mathbb{R}^k \to \mathbb{R}$。我们希望找到 $g(\hat{\boldsymbol{\theta}}_n)$ 的[渐近分布](@entry_id:272575)。与一维情况类似，我们对 $g(\hat{\boldsymbol{\theta}}_n)$ 在 $\boldsymbol{\theta}$ 点进行一阶[泰勒展开](@entry_id:145057)：

$$
g(\hat{\boldsymbol{\theta}}_n) \approx g(\boldsymbol{\theta}) + (\nabla g(\boldsymbol{\theta}))^T (\hat{\boldsymbol{\theta}}_n - \boldsymbol{\theta})
$$

其中，$\nabla g(\boldsymbol{\theta})$ 是 $g$ 在点 $\boldsymbol{\theta}$ 的**梯度 (gradient)** 向量，定义为：

$$
\nabla g(\boldsymbol{\theta}) = \begin{pmatrix} \frac{\partial g}{\partial \theta_1} \\ \vdots \\ \frac{\partial g}{\partial \theta_k} \end{pmatrix}_{\boldsymbol{\theta}}
$$

移项并乘以 $\sqrt{n}$，我们得到：

$$
\sqrt{n}(g(\hat{\boldsymbol{\theta}}_n) - g(\boldsymbol{\theta})) \approx (\nabla g(\boldsymbol{\theta}))^T \sqrt{n}(\hat{\boldsymbol{\theta}}_n - \boldsymbol{\theta})
$$

右侧是渐近多维正态分布随机向量的[线性组合](@entry_id:154743)，其结果仍然服从正态分布。其[渐近方差](@entry_id:269933)为：

$$
V_{\text{asym}} = \text{Var}((\nabla g(\boldsymbol{\theta}))^T \sqrt{n}(\hat{\boldsymbol{\theta}}_n - \boldsymbol{\theta})) = (\nabla g(\boldsymbol{\theta}))^T \Sigma (\nabla g(\boldsymbol{\theta}))
$$

这就是**多维[德尔塔方法](@entry_id:276272)**的核心公式。它将一维情况下的“导数平方”推广为一个二次型 $(\nabla g)^T \Sigma (\nabla g)$。这个公式优雅地将函数对参数的敏感度（由梯度 $\nabla g$ 捕捉）与估计量自身的不确定性及其内部相关性（由[协方差矩阵](@entry_id:139155) $\Sigma$ 捕捉）结合起来，从而给出了转换后统计量的[渐近方差](@entry_id:269933)。

### 应用方法：分步指南与实例

应用多维[德尔塔方法](@entry_id:276272)的流程是系统性的，可以归纳为以下五个步骤：

1.  **确定估计量向量与参数向量**：明确你的估计量向量 $\hat{\boldsymbol{\theta}}_n = (\hat{\theta}_{n,1}, \dots, \hat{\theta}_{n,k})^T$ 以及它们所估计的总体参数向量 $\boldsymbol{\theta} = (\theta_1, \dots, \theta_k)^T$。
2.  **确定渐近协方差矩阵**：根据多维[中心极限定理](@entry_id:143108)，确定 $\sqrt{n}(\hat{\boldsymbol{\theta}}_n - \boldsymbol{\theta})$ 的渐近[协方差矩阵](@entry_id:139155) $\Sigma$。对于样本[均值向量](@entry_id:266544)，$\Sigma$ 就是单个观测向量的总体协方差矩阵。
3.  **定义变换函数**：写出将参数向量 $\boldsymbol{\theta}$ 映射到你最终感兴趣的标量 $g(\boldsymbol{\theta})$ 的函数 $g$。
4.  **计算梯度**：计算函数 $g$ 的梯度 $\nabla g$，并在总体参数 $\boldsymbol{\theta}$ 处求值。
5.  **计算[渐近方差](@entry_id:269933)**：将梯度向量和协方差矩阵代入核心公式 $V = (\nabla g(\boldsymbol{\theta}))^T \Sigma (\nabla g(\boldsymbol{\theta}))$，计算最终的[渐近方差](@entry_id:269933)。

下面我们通过几个具体的例子来演示这个过程。

#### 示例1：均值之积（面积或功率）

在许多物理和工程问题中，我们关心的量是两个或多个量的乘积。例如，矩形的面积是长和宽的乘积，电路的功率是电压和电流的乘积。

考虑一个半导体制造的场景，其中生产的集成电路是矩形的。质量控制部门需要监控其平均面积。设电路的长度和宽度分别为[随机变量](@entry_id:195330) $L$ 和 $W$，其[总体均值](@entry_id:175446)为 $\mu_L$ 和 $\mu_W$，[方差](@entry_id:200758)为 $\sigma_L^2$ 和 $\sigma_W^2$，[相关系数](@entry_id:147037)为 $\rho$。从一个大样本中，我们得到样本均值 $\bar{L}_n$ 和 $\bar{W}_n$。我们使用 $\hat{A}_n = \bar{L}_n \bar{W}_n$ 来估计平均面积 $A = \mu_L \mu_W$。我们的目标是找到 $\sqrt{n}(\hat{A}_n - A)$ 的[渐近方差](@entry_id:269933) [@problem_id:1403157] [@problem_id:1403170]。

1.  **估计量向量与参数向量**：
    $\hat{\boldsymbol{\theta}}_n = \begin{pmatrix} \bar{L}_n \\ \bar{W}_n \end{pmatrix}$，$\boldsymbol{\theta} = \begin{pmatrix} \mu_L \\ \mu_W \end{pmatrix}$。

2.  **渐近协方差矩阵**：
    根据多维[中心极限定理](@entry_id:143108)，$\sqrt{n}(\hat{\boldsymbol{\theta}}_n - \boldsymbol{\theta})$ 的渐近协方差矩阵 $\Sigma$ 等于单个观测向量 $(L, W)^T$ 的[协方差矩阵](@entry_id:139155)。我们知道 $\text{Cov}(L, W) = \rho \sigma_L \sigma_W$。因此：
    $$
    \Sigma = \begin{pmatrix} \sigma_L^2  \rho \sigma_L \sigma_W \\ \rho \sigma_L \sigma_W  \sigma_W^2 \end{pmatrix}
    $$

3.  **变换函数**：
    面积是长度和宽度的乘积，所以 $g(\mu_L, \mu_W) = \mu_L \mu_W$。

4.  **计算梯度**：
    $g(l, w) = lw$ 的[偏导数](@entry_id:146280)是 $\frac{\partial g}{\partial l} = w$ 和 $\frac{\partial g}{\partial w} = l$。在[总体均值](@entry_id:175446)处求值，我们得到梯度向量：
    $$
    \nabla g(\mu_L, \mu_W) = \begin{pmatrix} \mu_W \\ \mu_L \end{pmatrix}
    $$

5.  **计算[渐近方差](@entry_id:269933)**：
    将梯度和协方差矩阵代入公式：
    $$
    \begin{align*}
    V = (\nabla g(\boldsymbol{\theta}))^T \Sigma (\nabla g(\boldsymbol{\theta})) \\
     = \begin{pmatrix} \mu_W  \mu_L \end{pmatrix} \begin{pmatrix} \sigma_L^2  \rho \sigma_L \sigma_W \\ \rho \sigma_L \sigma_W  \sigma_W^2 \end{pmatrix} \begin{pmatrix} \mu_W \\ \mu_L \end{pmatrix} \\
     = \begin{pmatrix} \mu_W  \mu_L \end{pmatrix} \begin{pmatrix} \mu_W \sigma_L^2 + \mu_L \rho \sigma_L \sigma_W \\ \mu_W \rho \sigma_L \sigma_W + \mu_L \sigma_W^2 \end{pmatrix} \\
     = \mu_W(\mu_W \sigma_L^2 + \mu_L \rho \sigma_L \sigma_W) + \mu_L(\mu_W \rho \sigma_L \sigma_W + \mu_L \sigma_W^2) \\
     = \mu_W^2 \sigma_L^2 + \mu_L^2 \sigma_W^2 + 2 \rho \mu_L \mu_W \sigma_L \sigma_W
    \end{align*}
    $$
    这个结果清晰地表明，估计面积的[方差](@entry_id:200758)不仅取决于长度和宽度的[方差](@entry_id:200758)，还取决于它们之间的协[方差](@entry_id:200758)。如果长度和宽度正相关（$\rho > 0$），那么估计面积的[方差](@entry_id:200758)会更大，反之亦然。

#### 示例2：均值之比（长宽比或角度）

在生物学、金融学和许多其他领域，比率是一个重要的度量。例如，植物叶片的[长宽比](@entry_id:177707)可以作为[物种分类](@entry_id:263396)的指标。

一位植物学家研究某种植物叶片的物理特性，估计其平均长宽比 $R = \mu_L / \mu_W$。他使用样本均值的比率 $\hat{R}_n = \bar{L}_n / \bar{W}_n$ 作为估计量。假设相关的总体参数已知，我们想求 $\sqrt{n}(\hat{R}_n - R)$ 的[渐近方差](@entry_id:269933) [@problem_id:1403187]。

1.  **估计量与参数**：与上例相同，$\hat{\boldsymbol{\theta}}_n = (\bar{L}_n, \bar{W}_n)^T$，$\boldsymbol{\theta} = (\mu_L, \mu_W)^T$。
2.  **协方差矩阵**：与上例相同。
3.  **变换函数**：$g(\mu_L, \mu_W) = \mu_L / \mu_W$。
4.  **计算梯度**：
    $g(l, w) = l/w$ 的偏导数是 $\frac{\partial g}{\partial l} = 1/w$ 和 $\frac{\partial g}{\partial w} = -l/w^2$。在[总体均值](@entry_id:175446)处求值：
    $$
    \nabla g(\mu_L, \mu_W) = \begin{pmatrix} 1/\mu_W \\ -\mu_L/\mu_W^2 \end{pmatrix}
    $$
5.  **计算[渐近方差](@entry_id:269933)**：
    将梯度和 $\Sigma$ 代入公式，经过矩阵乘法和代数化简，可得[渐近方差](@entry_id:269933)为：
    $$
    V = \frac{\sigma_L^2}{\mu_W^2} + \frac{\mu_L^2 \sigma_W^2}{\mu_W^4} - \frac{2 \rho \mu_L \sigma_L \sigma_W}{\mu_W^3}
    $$
    这个结果可以用给定的数值计算。例如，若 $\mu_L=10, \mu_W=4, \sigma_L^2=2.25, \sigma_W^2=0.25, \rho=0.6$，则[渐近方差](@entry_id:269933)约为 $0.0977$。
    一个类似但函数形式稍有不同的问题是估计直角三角形的平均角度，其估计量为 $\hat{\theta}_n = \arctan(\bar{O}_n/\bar{A}_n)$ [@problem_id:1403159]。其求解过程完全相同，只是变换函数变为 $g(o, a) = \arctan(o/a)$，需要计算一个不同的梯度。

#### 示例3：更复杂的函数（身体[质量指数](@entry_id:190779)BMI）

多维[德尔塔方法](@entry_id:276272)可以轻松处理更复杂的函数。例如，身体[质量指数](@entry_id:190779)（BMI）定义为体重（kg）除以身高（m）的平方。

一项[公共卫生](@entry_id:273864)调查旨在估计某成年人群的平均BMI，即 $\theta = \mu_W / \mu_H^2$。分析师使用 $\hat{\theta}_n = \bar{W}_n / (\bar{H}_n)^2$ 作为估计量。我们需要确定 $\hat{\theta}_n$ 的[渐近方差](@entry_id:269933) [@problem_id:1403143]。

这里的变换函数是 $g(w, h) = w/h^2$。其梯度为：
$$
\nabla g(w, h) = \begin{pmatrix} \partial g / \partial w \\ \partial g / \partial h \end{pmatrix} = \begin{pmatrix} 1/h^2 \\ -2w/h^3 \end{pmatrix}
$$
在[总体均值](@entry_id:175446) $(\mu_W, \mu_H)$ 处求值后，将此[梯度向量](@entry_id:141180)与体重和身高的协方差矩阵 $\Sigma$ 一起代入二次型公式 $(\nabla g)^T \Sigma (\nabla g)$，即可得到BMI估计量的[渐近方差](@entry_id:269933)。这个过程虽然代数上可能更繁琐，但原理完全一致。

### 特殊情况：[不相关与独立](@entry_id:264327)的估计量

当估计量向量中的分量互不相关时，协方差矩阵 $\Sigma$ 成为一个[对角矩阵](@entry_id:637782)。这大大简化了[渐近方差](@entry_id:269933)的计算。

如果 $\Sigma = \text{diag}(\sigma_1^2, \dots, \sigma_k^2)$，那么[渐近方差](@entry_id:269933)公式变为：
$$
V = (\nabla g)^T \Sigma (\nabla g) = \sum_{i=1}^k \left(\frac{\partial g}{\partial \theta_i}\right)^2 \sigma_i^2
$$
这意味着，转换后统计量的[渐近方差](@entry_id:269933)等于每个分量的[方差](@entry_id:200758)与其对应偏导数平方的乘积之和。

#### 示例4a：[不相关变量](@entry_id:261964)（粒子速度）

在一次粒子物理实验中，探测器测量了[粒子流](@entry_id:753205)的速度分量 $(V_x, V_y)$。已知[总体均值](@entry_id:175446)为 $E[V_x] = \mu_x, E[V_y] = 0$，且速度分量不相关，即 $\text{Cov}(V_x, V_y) = 0$。研究者对平均速度向量的模方 $S = \bar{V}_x^2 + \bar{V}_y^2$ 感兴趣，并希望找到 $\sqrt{n}(S - \mu_x^2)$ 的[渐近方差](@entry_id:269933) [@problem_id:1403195]。

1.  **估计量与参数**：$\hat{\boldsymbol{\theta}}_n = (\bar{V}_x, \bar{V}_y)^T$，$\boldsymbol{\theta} = (\mu_x, 0)^T$。
2.  **协方差矩阵**：由于分量不相关，$\Sigma = \begin{pmatrix} \sigma_x^2  0 \\ 0  \sigma_y^2 \end{pmatrix}$。
3.  **变换函数**：$g(v_x, v_y) = v_x^2 + v_y^2$。
4.  **计算梯度**：$\nabla g(v_x, v_y) = (2v_x, 2v_y)^T$。在 $\boldsymbol{\theta} = (\mu_x, 0)$ 处求值，得到 $\nabla g(\mu_x, 0) = (2\mu_x, 0)^T$。
5.  **计算[渐近方差](@entry_id:269933)**：
    $$
    V = \begin{pmatrix} 2\mu_x  0 \end{pmatrix} \begin{pmatrix} \sigma_x^2  0 \\ 0  \sigma_y^2 \end{pmatrix} \begin{pmatrix} 2\mu_x \\ 0 \end{pmatrix} = (2\mu_x)^2 \sigma_x^2 + 0^2 \cdot \sigma_y^2 = 4\mu_x^2 \sigma_x^2
    $$
    这个结果有一个有趣的启示：尽管统计量 $S$ 本身包含 $\bar{V}_y^2$，但其[渐近方差](@entry_id:269933)却与 $\sigma_y^2$ 无关。这是因为函数 $g$ 对第二个分量的偏导数在均值点 $( \mu_x, 0)$ 处为零，表明在这一点附近，$g$ 的值对第二个分量的微小变化不敏感。

#### 示例4b：[独立样本](@entry_id:177139)（[对数优势比](@entry_id:141427)）

当我们的估计量来自**相互独立的样本**时，它们之间自然也是不相关的。这种情况在比较两组或多组数据时非常常见。

假设两项独立的民意调查分别在A、B两市进行，得到政策支持率的样本比例 $\hat{p}_1$ 和 $\hat{p}_2$。分析师希望比较两市的[对数优势比](@entry_id:141427)（log-odds），即研究统计量 $\Delta = \text{logit}(\hat{p}_1) - \text{logit}(\hat{p}_2)$ 的性质，其中 $\text{logit}(p) = \ln(p/(1-p))$ [@problem_id:1403177]。

1.  **估计量与参数**：$\hat{\boldsymbol{\theta}} = (\hat{p}_1, \hat{p}_2)^T$，$\boldsymbol{\theta} = (p_1, p_2)^T$。注意这里我们直接讨论 $\hat{\boldsymbol{\theta}}$ 的[渐近分布](@entry_id:272575)，而不是标准化的形式。
2.  **[协方差矩阵](@entry_id:139155)**：根据中心极限定理，$\hat{p}_1$ 的[渐近方差](@entry_id:269933)为 $p_1(1-p_1)/n_1$，$\hat{p}_2$ 的[渐近方差](@entry_id:269933)为 $p_2(1-p_2)/n_2$。由于样本独立，它们的协[方差](@entry_id:200758)为0。因此，$\hat{\boldsymbol{\theta}}$ 的渐近[协方差矩阵](@entry_id:139155)为：
    $$
    \boldsymbol{\Sigma}_{\hat{\boldsymbol{\theta}}} = \begin{pmatrix} \frac{p_1(1-p_1)}{n_1}  0 \\ 0  \frac{p_2(1-p_2)}{n_2} \end{pmatrix}
    $$
3.  **变换函数**：$g(p_1, p_2) = \ln(\frac{p_1}{1-p_1}) - \ln(\frac{p_2}{1-p_2})$。
4.  **计算梯度**：$\text{logit}(p)$ 的导数是 $1/(p(1-p))$。因此，
    $$
    \nabla g(p_1, p_2) = \begin{pmatrix} 1/(p_1(1-p_1)) \\ -1/(p_2(1-p_2)) \end{pmatrix}
    $$
5.  **计算[渐近方差](@entry_id:269933)**：
    由于协方差矩阵是对角阵，$\Delta$ 的[渐近方差](@entry_id:269933) $\text{Var}(\Delta)$ 就是：
    $$
    \begin{align*}
    \text{Var}(\Delta) \approx \left(\frac{1}{p_1(1-p_1)}\right)^2 \text{Var}(\hat{p}_1) + \left(\frac{-1}{p_2(1-p_2)}\right)^2 \text{Var}(\hat{p}_2) \\
     = \left(\frac{1}{p_1(1-p_1)}\right)^2 \frac{p_1(1-p_1)}{n_1} + \left(\frac{1}{p_2(1-p_2)}\right)^2 \frac{p_2(1-p_2)}{n_2} \\
     = \frac{1}{n_1 p_1(1-p_1)} + \frac{1}{n_2 p_2(1-p_2)}
    \end{align*}
    $$
    这个结果非常简洁且具有启发性：[对数优势比](@entry_id:141427)差异的[方差](@entry_id:200758)，等于各自[对数优势比](@entry_id:141427)[方差](@entry_id:200758)之和。这是比较两组比例时一个极其有用的标准结果。

### 高级应用：矩的函数

[德尔塔方法](@entry_id:276272)的强大之处在于，它不仅限于样本均值的函数，而是适用于任何渐近正态的估计量向量。一个重要的扩展是将其应用于**样本矩 (sample moments)** 的函数。

#### 示例5：[变异系数](@entry_id:272423) (Coefficient of Variation)

[变异系数](@entry_id:272423) $CV = \sigma/\mu$ 是一个衡量数据相对离散程度的无量纲指标。其样本估计量通常定义为 $T_n = S_n / \bar{X}_n$，其中 $S_n$ 是样本标准差。我们可以用[德尔塔方法](@entry_id:276272)推导 $T_n$ 的[渐近方差](@entry_id:269933) [@problem_id:1403165]。

为了应用[德尔塔方法](@entry_id:276272)，我们需要将 $T_n$ 表示为一组简单的、满足中心极限定理的统计量的函数。注意到 $S_n^2 = \overline{X^2}_n - (\bar{X}_n)^2$ (这里使用除以 $n$ 的样本[方差](@entry_id:200758))，我们可以将 $T_n$ 写成样本一阶矩（样本均值）$\bar{X}_n$ 和样本二阶[原点矩](@entry_id:165197) $\overline{X^2}_n = \frac{1}{n}\sum X_i^2$ 的函数。

1.  **估计量向量与参数向量**：
    设 $Y_n = \begin{pmatrix} \bar{X}_n \\ \overline{X^2}_n \end{pmatrix}$。这是一个样本[均值向量](@entry_id:266544)，其对应的总体参数向量为 $\boldsymbol{\theta} = \begin{pmatrix} E[X] \\ E[X^2] \end{pmatrix} = \begin{pmatrix} \mu \\ \sigma^2+\mu^2 \end{pmatrix}$。

2.  **渐近[协方差矩阵](@entry_id:139155)**：
    我们需要计算 $\sqrt{n}(Y_n - \boldsymbol{\theta})$ 的渐近[协方差矩阵](@entry_id:139155) $\Sigma$，也就是随机向量 $(X, X^2)^T$ 的[协方差矩阵](@entry_id:139155)。这需要知道 $X$ 的前四阶矩。
    $$
    \Sigma = \begin{pmatrix} \text{Var}(X)  \text{Cov}(X, X^2) \\ \text{Cov}(X, X^2)  \text{Var}(X^2) \end{pmatrix} = \begin{pmatrix} E[X^2] - (E[X])^2  E[X^3] - E[X]E[X^2] \\ E[X^3] - E[X]E[X^2]  E[X^4] - (E[X^2])^2 \end{pmatrix}
    $$
    如果假设 $X$ 服从正态分布 $N(\mu, \sigma^2)$，这些矩可以被计算出来，得到 $\Sigma = \begin{pmatrix} \sigma^2  2\mu\sigma^2 \\ 2\mu\sigma^2  2\sigma^4 + 4\mu^2\sigma^2 \end{pmatrix}$。

3.  **变换函数**：
    $T_n$ 可以表示为 $g(\bar{X}_n, \overline{X^2}_n)$，其中 $g(y_1, y_2) = \frac{\sqrt{y_2 - y_1^2}}{y_1}$。

4.  **计算梯度**：
    计算 $g(y_1, y_2)$ 对 $y_1$ 和 $y_2$ 的[偏导数](@entry_id:146280)，并在 $\boldsymbol{\theta}=(\mu, \sigma^2+\mu^2)$ 处求值。

5.  **计算[渐近方差](@entry_id:269933)**：
    将梯度和[协方差矩阵](@entry_id:139155) $\Sigma$ 代入公式 $(\nabla g)^T \Sigma (\nabla g)$。经过一番复杂的代数化简，可以得到一个关于 $\mu$ 和 $\sigma$ 的表达式。一个更为优雅的结果是，当用[变异系数](@entry_id:272423) $CV = \sigma/\mu$ 表示时，$\sqrt{n}(T_n - CV)$ 的[渐近方差](@entry_id:269933)为：
    $$
    V = CV^4 + \frac{CV^2}{2}
    $$
    这个例子完美地展示了多维[德尔塔方法](@entry_id:276272)的通用性：通过巧妙地构造估计量向量，我们可以处理看似非常复杂的统计量，并推导出其在大样本下的性质。

总之，多维[德尔塔方法](@entry_id:276272)是统计理论中的一块基石。它通过线性化，将[中心极限定理](@entry_id:143108)从简单的均值或比例扩展到这些基本估计量的任意复杂函数，为现代统计推断中构建置信区间和进行[假设检验](@entry_id:142556)提供了核心的理论依据。