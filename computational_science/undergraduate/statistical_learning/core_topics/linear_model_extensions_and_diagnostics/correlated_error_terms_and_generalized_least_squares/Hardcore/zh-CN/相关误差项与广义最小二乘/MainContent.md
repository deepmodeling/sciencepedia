## 引言
在[线性回归分析](@entry_id:166896)中，一个核心假设是误差项彼此独立且[方差](@entry_id:200758)恒定，即所谓的“球形误差”。然而，在经济学的时间序列、[环境科学](@entry_id:187998)的空间数据或生物学的[系统发育](@entry_id:137790)数据等众多实际应用中，这一理想假设常常被打破。数据点之间的内在联系导致误差项出现[自相关](@entry_id:138991)或异[方差](@entry_id:200758)，这种现象被称为误差相关。当这种情况发生时，我们惯用的[普通最小二乘法](@entry_id:137121)（OLS）虽然可能仍是无偏的，但其估计效率会大大降低，更严重的是，其标准误计算会产生偏差，导致所有[统计推断](@entry_id:172747)（如t检验和[置信区间](@entry_id:142297)）都变得不可靠。

本文旨在解决这一关键问题，系统地介绍[广义最小二乘法](@entry_id:272590)（GLS）作为应对[相关误差](@entry_id:268558)的强大框架。通过学习本文，你将不再受限于传统的[OLS假设](@entry_id:147063)，并能处理更复杂、更现实的数据结构。首先，在“原理与机制”一章中，我们将深入剖析OLS在误差相关时的具体失效表现，并详细阐述GLS如何通过巧妙的“白化”变换来恢复估计的有效性。接着，在“应用与跨学科联系”一章中，我们将展示GLS在经济学、工程学、[演化生物学](@entry_id:145480)等多个领域的广泛应用，揭示其作为通用方法的强大生命力。最后，通过“动手实践”部分，你将有机会亲手实现和比较不同的估计方法，从而将理论知识转化为扎实的计算技能。

## 原理与机制

在经典的[线性回归](@entry_id:142318)模型中，我们通常假设误差项是“球形”的，即它们是不相关且具有恒定[方差](@entry_id:200758)的。数学上，这表示为 $\operatorname{Var}(\boldsymbol{\varepsilon}) = \sigma^2 \mathbf{I}$，其中 $\mathbf{I}$ 是单位矩阵。然而，在许多现实世界的应用中，尤其是在处理时间[序列数据](@entry_id:636380)或面板数据时，这个假设往往被违背。误差项之间可能存在[自相关](@entry_id:138991)（例如，今天的误差与昨天的误差相关）或异[方差](@entry_id:200758)（不同观测值的[误差方差](@entry_id:636041)不同）。当误差的[协方差矩阵](@entry_id:139155)不再是[单位矩阵](@entry_id:156724)的倍数，即 $\operatorname{Var}(\boldsymbol{\varepsilon}) = \boldsymbol{\Sigma}$，其中 $\boldsymbol{\Sigma}$ 是一个非对角矩阵时，我们就进入了[广义线性模型](@entry_id:171019)的领域。本章将深入探讨[误差相关性](@entry_id:749076)的后果，并介绍[广义最小二乘法](@entry_id:272590)（Generalized Least Squares, GLS）作为解决这一问题的强大工具。

### OLS的失效：当误差不再独立

当误差项相关时，普通的最小二乘法（Ordinary Least Squares, OLS）会遇到两个主要问题。首先，虽然[OLS估计量](@entry_id:177304)在某些条件下仍然是无偏的，但它不再是[最佳线性无偏估计量](@entry_id:137602)（Best Linear Unbiased Estimator, BLUE）。其次，也是更严重的问题，标准的OLS[方差估计](@entry_id:268607)量是有偏的，这导致所有基于它的[统计推断](@entry_id:172747)（如t检验、[F检验](@entry_id:274297)和置信区间）都变得无效。

#### 估计效率的损失

[高斯-马尔可夫定理](@entry_id:138437)保证了在球形误差假设下OLS的有效性。当这个假设被打破，[OLS估计量](@entry_id:177304) $\hat{\boldsymbol{\beta}}_{\mathrm{OLS}}$ 就不再具有最小[方差](@entry_id:200758)。存在其他线性[无偏估计量](@entry_id:756290)，其[方差](@entry_id:200758)更小。

考虑一个简单的例子 ，我们有三年的观测数据，模型为 $y = X\beta + \varepsilon$。假设真实误差遵循一阶自回归（AR(1)）过程，[相关系数](@entry_id:147037)为 $\rho = 0.5$。这意味着相邻观测的误差是正相关的。如果我们忽略这种相关性并使用OLS，得到的[回归系数](@entry_id:634860)估计量将不是最有效的。通过与考虑了相关性的GLS估计量进行比较，我们可以量化这种效率损失。在具体计算中，我们会发现 $\hat{\boldsymbol{\beta}}_{\mathrm{OLS}}$ 和 $\hat{\boldsymbol{\beta}}_{\mathrm{GLS}}$ 的值可能很接近，但它们的真实[方差](@entry_id:200758)却有显著差异。例如，定义一个估计量相对于另一个[估计量的相对效率](@entry_id:172886)为它们[方差](@entry_id:200758)的迹之比。在  的设定下，GLS相对于OLS的效率增益可以计算出来，这个值大于1，明确表明GLS估计量具有更小的[抽样变异性](@entry_id:166518)，因此更优。

这种效率损失也出现在异[方差](@entry_id:200758)的情况下。例如，在一个过原点的回归模型 $Y_i = \beta x_i + \epsilon_i$ 中，如果[误差方差](@entry_id:636041)与回归量的平方成正比，即 $\operatorname{Var}(\epsilon_i) = \sigma^2 x_i^2$ ，那么[OLS估计量](@entry_id:177304)的[方差](@entry_id:200758)将依赖于回归量 $x_i$ 的一个复杂组合，而为这种情况设计的GLS[估计量的方差](@entry_id:167223)则更为简洁且更小。OLS相对于GLS的[相对效率](@entry_id:165851)将是 $\frac{(\sum_{i=1}^{n}x_{i}^{2})^{2}}{n\sum_{i=1}^{n}x_{i}^{4}}$，根据柯西-施瓦茨不等式，这个值总是小于或等于1，表明OLS的效率较低。

#### 推断的失效

比效率损失更严重的是，OLS的[标准误差](@entry_id:635378)计算完全错误。标准的OLS[方差估计](@entry_id:268607)量公式 $\widehat{\operatorname{Var}}(\hat{\boldsymbol{\beta}}_{\mathrm{OLS}}) = \hat{\sigma}^2(\mathbf{X}^{\top}\mathbf{X})^{-1}$ 是基于 $\operatorname{Var}(\boldsymbol{\varepsilon}) = \sigma^2\mathbf{I}$ 推导的。当 $\operatorname{Var}(\boldsymbol{\varepsilon}) = \boldsymbol{\Sigma} \neq \sigma^2\mathbf{I}$ 时，$\hat{\boldsymbol{\beta}}_{\mathrm{OLS}}$ 的真实[方差](@entry_id:200758)是 $\operatorname{Var}(\hat{\boldsymbol{\beta}}_{\mathrm{OLS}}) = (\mathbf{X}^{\top}\mathbf{X})^{-1}\mathbf{X}^{\top}\boldsymbol{\Sigma}\mathbf{X}(\mathbf{X}^{\top}\mathbf{X})^{-1}$，这被称为“三明治”估计量。

更重要的是，[误差方差](@entry_id:636041)的[OLS估计量](@entry_id:177304) $\hat{\sigma}^{2}_{\mathrm{OLS}} = \frac{\mathbf{e}^{\top}\mathbf{e}}{n-p}$ 本身也变得有偏。在一个具有AR(1)误差的简单模型中，我们可以精确地推导出这个偏差 。例如，在一个包含截距和线性趋势项的模型中，如果真实误差[相关系数](@entry_id:147037)为 $\rho$，那么 $\hat{\sigma}^{2}_{\mathrm{OLS}}$ 的[期望值](@entry_id:153208)将是 $\mathbb{E}[\hat{\sigma}^{2}_{\mathrm{OLS}}] = \sigma^2 \frac{1}{3}(3-4\rho+\rho^2)$。当 $\rho \neq 0$ 时，这个[期望值](@entry_id:153208)不等于真实的 $\sigma^2$。例如，如果 $\rho$ 是正的（这是[时间序列数据](@entry_id:262935)中最常见的情况），$\hat{\sigma}^{2}_{\mathrm{OLS}}$ 会倾向于低估真实的[误差方差](@entry_id:636041)。这种偏差直接导致标准误的计算错误，从而使[t统计量](@entry_id:177481)和[F统计量](@entry_id:148252)不可靠。

一个具体的例子  可以说明这一点。在一个检验[回归系数](@entry_id:634860)是否为零的[假设检验](@entry_id:142556)中，如果数据误差存在AR(1)相关性（$\rho=0.5$），但我们错误地使用了OLS [F检验](@entry_id:274297)，我们可能会得到一个非常大的[F值](@entry_id:178445)（例如464.4）。然而，如果我们使用为[相关误差](@entry_id:268558)设计的正确GLS [F检验](@entry_id:274297)，我们会得到一个显著不同且小得多的[F值](@entry_id:178445)（例如182.2）。这表明OLS会严重夸大[统计显著性](@entry_id:147554)，可能导致我们错误地拒绝[原假设](@entry_id:265441)。

### [广义最小二乘法](@entry_id:272590)的原理：[白化变换](@entry_id:637327)

GLS的核心思想不是发明一种全新的估计方法，而是通过一种巧妙的线性变换，将一个具有[相关误差](@entry_id:268558)的“复杂”模型，转化为一个满足经典假设的“简单”模型，然后对这个新模型应用我们熟悉的OLS。这个过程被称为**白化（whitening）**。

假设误差的协方差矩阵为 $\boldsymbol{\Sigma}$。因为 $\boldsymbol{\Sigma}$ 是对称正定矩阵，我们可以找到一个非奇异的**白化矩阵** $\mathbf{W}$，使得 $\mathbf{W}\boldsymbol{\Sigma}\mathbf{W}^{\top} = \sigma^2\mathbf{I}$。这意味着，如果我们用 $\mathbf{W}$ 左乘原始的回归方程 $ \mathbf{y}=\mathbf{X}\boldsymbol{\beta}+\boldsymbol{\varepsilon} $，我们得到一个新的[回归模型](@entry_id:163386)：
$$ \mathbf{W}\mathbf{y} = \mathbf{W}\mathbf{X}\boldsymbol{\beta} + \mathbf{W}\boldsymbol{\varepsilon} $$
或者写成：
$$ \mathbf{y}^* = \mathbf{X}^*\boldsymbol{\beta} + \boldsymbol{\varepsilon}^* $$
其中 $\mathbf{y}^* = \mathbf{W}\mathbf{y}$，$\mathbf{X}^* = \mathbf{W}\mathbf{X}$，$\boldsymbol{\varepsilon}^* = \mathbf{W}\boldsymbol{\varepsilon}$。

这个变换的神奇之处在于，新的误差项 $\boldsymbol{\varepsilon}^*$ 的[协方差矩阵](@entry_id:139155)是：
$$ \operatorname{Var}(\boldsymbol{\varepsilon}^*) = \operatorname{Var}(\mathbf{W}\boldsymbol{\varepsilon}) = \mathbf{W}\operatorname{Var}(\boldsymbol{\varepsilon})\mathbf{W}^{\top} = \mathbf{W}\boldsymbol{\Sigma}\mathbf{W}^{\top} = \sigma^2\mathbf{I} $$
新的误差项 $\boldsymbol{\varepsilon}^*$ 是球形的！它们不相关且具有恒定的[方差](@entry_id:200758)。因此，我们可以在变换后的模型 $(\mathbf{y}^*, \mathbf{X}^*)$ 上安全地使用OLS来估计 $\boldsymbol{\beta}$。对变换后模型应用OLS得到的估计量，就是原始模型的GLS估计量。

一个寻找白化矩阵 $\mathbf{W}$ 的常见方法是利用 $\boldsymbol{\Sigma}$ 的逆矩阵。因为 $\mathbf{W}\boldsymbol{\Sigma}\mathbf{W}^{\top}$ 正比于 $\mathbf{I}$，这意味着 $\mathbf{W}^{\top}\mathbf{W}$ 必须正比于 $\boldsymbol{\Sigma}^{-1}$。我们可以通过[Cholesky分解](@entry_id:147066)找到这样一个矩阵。例如，我们可以分解 $\boldsymbol{\Sigma} = \mathbf{L}\mathbf{L}^{\top}$，其中 $\mathbf{L}$ 是下三角矩阵，然后取 $\mathbf{W} = \mathbf{L}^{-1}$。这样，$\mathbf{W}\boldsymbol{\Sigma}\mathbf{W}^{\top} = \mathbf{L}^{-1}(\mathbf{L}\mathbf{L}^{\top})(\mathbf{L}^{-1})^{\top} = \mathbf{I}$ 。

以AR(1)误差过程为例，$\varepsilon_t = \rho \varepsilon_{t-1} + u_t$。这个[白化变换](@entry_id:637327)有一个非常直观的形式，被称为**准差分（quasi-differencing）** 。对于 $t \ge 2$ 的观测值，我们可以通过从当前观测值中减去前一期观测值的 $\rho$ 倍来变换数据：
$$ y_t - \rho y_{t-1} = (\mathbf{x}_t^{\top}\boldsymbol{\beta} + \varepsilon_t) - \rho(\mathbf{x}_{t-1}^{\top}\boldsymbol{\beta} + \varepsilon_{t-1}) = (\mathbf{x}_t^{\top} - \rho \mathbf{x}_{t-1}^{\top})\boldsymbol{\beta} + (\varepsilon_t - \rho \varepsilon_{t-1}) $$
由于 $\varepsilon_t - \rho \varepsilon_{t-1} = u_t$，而 $u_t$ 是不相关的白噪声，这个变换成功地消除了 $t=2, \dots, n$ 之间的[误差相关性](@entry_id:749076)。然而，为了确保所有变换后的误差都具有相同的[方差](@entry_id:200758) $\sigma_u^2$，第一个观测值需要特殊处理。在[平稳性假设](@entry_id:272270)下，$\operatorname{Var}(\varepsilon_1) = \frac{\sigma_u^2}{1-\rho^2}$。为了使变换后的[误差方差](@entry_id:636041)为 $\sigma_u^2$，我们需要将第一个观测方程乘以 $\sqrt{1-\rho^2}$。这个包含特殊处理第一个观测值的完整变换被称为**Prais-Winsten变换**。对经过Prais-Winsten变换的数据应用OLS，就等价于执行GLS。

### GLS估计量及其性质

通过对变换后的模型应用OLS，或者直接最小化**广义[残差平方和](@entry_id:174395)**，我们可以推导出GLS估计量的解析形式。广义[残差平方和](@entry_id:174395)（或称[马氏距离](@entry_id:269828)的平方）定义为：
$$ S(\boldsymbol{\beta}) = (\mathbf{y} - \mathbf{X}\boldsymbol{\beta})^{\top}\boldsymbol{\Sigma}^{-1}(\mathbf{y} - \mathbf{X}\boldsymbol{\beta}) $$
最小化这个[目标函数](@entry_id:267263)  会得到**广义[正规方程](@entry_id:142238)**（generalized normal equations）：
$$ (\mathbf{X}^{\top}\boldsymbol{\Sigma}^{-1}\mathbf{X})\hat{\boldsymbol{\beta}} = \mathbf{X}^{\top}\boldsymbol{\Sigma}^{-1}\mathbf{y} $$
如果矩阵 $\mathbf{X}^{\top}\boldsymbol{\Sigma}^{-1}\mathbf{X}$ 是可逆的（通常在 $\mathbf{X}$ [满列秩](@entry_id:749628)时成立），那么唯一的**GLS估计量**为：
$$ \hat{\boldsymbol{\beta}}_{\mathrm{GLS}} = (\mathbf{X}^{\top}\boldsymbol{\Sigma}^{-1}\mathbf{X})^{-1}\mathbf{X}^{\top}\boldsymbol{\Sigma}^{-1}\mathbf{y} $$
这个估计量具有优良的统计性质：

1.  **无偏性**：与OLS一样，只要误差项的期望为零且与回归量无关，GLS估计量就是无偏的，即 $\mathbb{E}[\hat{\boldsymbol{\beta}}_{\mathrm{GLS}}] = \boldsymbol{\beta}$。
2.  **[方差](@entry_id:200758)**：GLS[估计量的方差](@entry_id:167223)由下式给出：
    $$ \operatorname{Var}(\hat{\boldsymbol{\beta}}_{\mathrm{GLS}}) = (\mathbf{X}^{\top}\boldsymbol{\Sigma}^{-1}\mathbf{X})^{-1} $$
    需要注意的是，如果[误差协方差矩阵](@entry_id:749077)写为 $\operatorname{Var}(\boldsymbol{\varepsilon}) = \sigma^2 \boldsymbol{\Omega}$，其中 $\boldsymbol{\Omega}$ 是已知的[相关矩阵](@entry_id:262631)，而 $\sigma^2$ 未知，那么GLS估计量为 $\hat{\boldsymbol{\beta}}_{\mathrm{GLS}} = (\mathbf{X}^{\top}\boldsymbol{\Omega}^{-1}\mathbf{X})^{-1}\mathbf{X}^{\top}\boldsymbol{\Omega}^{-1}\mathbf{y}$，其[方差](@entry_id:200758)为 $\operatorname{Var}(\hat{\boldsymbol{\beta}}_{\mathrm{GLS}}) = \sigma^2(\mathbf{X}^{\top}\boldsymbol{\Omega}^{-1}\mathbf{X})^{-1}$。
3.  **有效性**：**Aitken定理**（[高斯-马尔可夫定理](@entry_id:138437)的推广）指出，GLS估计量是所有线性[无偏估计量](@entry_id:756290)中[方差](@entry_id:200758)最小的，即GLS是BLUE。

我们可以通过一个具体的计算例子  来体会OLS和GLS的区别。给定一个包含截距和单个预测变量的3个观测值的数据集，以及一个AR(1)误差结构（$\rho=0.5$），我们可以分别计算OLS和GLS估计量。例如，我们可能得到 $\hat{\boldsymbol{\beta}}_{\mathrm{OLS}} = \begin{pmatrix} 7/6 & 3/2 \end{pmatrix}^{\top}$ 和 $\hat{\boldsymbol{\beta}}_{\mathrm{GLS}} = \begin{pmatrix} 11/10 & 3/2 \end{pmatrix}^{\top}$。虽然这两个[点估计](@entry_id:174544)在数值上可能相差不大，但它们背后的不确定性却大相径庭。通过计算它们的真实[方差](@entry_id:200758)矩阵，我们会发现 $\operatorname{tr}(\operatorname{Var}(\hat{\boldsymbol{\beta}}_{\mathrm{OLS}}))$ 明显大于 $\operatorname{tr}(\operatorname{Var}(\hat{\boldsymbol{\beta}}_{\mathrm{GLS}}))$。在本例中，效率增益 $\frac{\operatorname{tr}(\operatorname{Var}(\hat{\boldsymbol{\beta}}_{\mathrm{OLS}}))}{\operatorname{tr}(\operatorname{Var}(\hat{\boldsymbol{\beta}}_{\mathrm{GLS}}))} = \frac{245}{243} \approx 1.008$。虽然在这个小样本中增益看似不大，但在更强的相关性或更大的数据集中，这种差异会变得非常显著。

### 实践中的GLS：可行GLS与假设检验

到目前为止，我们一直假设[误差协方差矩阵](@entry_id:749077) $\boldsymbol{\Sigma}$ 是已知的。但在实践中，我们几乎从不知道 $\boldsymbol{\Sigma}$ 的确切形式，我们只对其结构（如AR(1)）有所怀疑，并不知道其参数（如 $\rho$ 和 $\sigma^2$）。这就引出了**[可行广义最小二乘法](@entry_id:634462)（Feasible Generalized Least Squares, FGLS）**。

#### 可行GLS（FGLS）

FGLS是一个多步骤的估计程序，其基本思想是用一个一致的估计量 $\hat{\boldsymbol{\Sigma}}$ 来代替未知的 $\boldsymbol{\Sigma}$。一个典型的FGLS迭代算法  如下：

1.  **初始化**：运行OLS得到初始的[系数估计](@entry_id:175952) $\hat{\boldsymbol{\beta}}^{(0)}$ 和残差 $\mathbf{r}^{(0)} = \mathbf{y} - \mathbf{X}\hat{\boldsymbol{\beta}}^{(0)}$。
2.  **估计协[方差](@entry_id:200758)参数**：使用残差 $\mathbf{r}^{(0)}$ 来估计 $\boldsymbol{\Sigma}$ 的参数。例如，在[AR(1)模型](@entry_id:265801)中，我们可以通过残差的样本自相关来估计 $\rho$，即 $\hat{\rho}^{(1)} = \frac{\sum_{t=2}^n r^{(0)}_t r^{(0)}_{t-1}}{\sum_{t=1}^{n-1} (r^{(0)}_t)^2}$。然后估计创新[方差](@entry_id:200758) $\sigma_u^2$。从而构造出协方差矩阵的估计 $\hat{\boldsymbol{\Sigma}}^{(1)}$。
3.  **GLS步骤**：使用 $\hat{\boldsymbol{\Sigma}}^{(1)}$ 来计算新的[系数估计](@entry_id:175952) $\hat{\boldsymbol{\beta}}^{(1)} = (\mathbf{X}^{\top}(\hat{\boldsymbol{\Sigma}}^{(1)})^{-1}\mathbf{X})^{-1}\mathbf{X}^{\top}(\hat{\boldsymbol{\Sigma}}^{(1)})^{-1}\mathbf{y}$。
4.  **迭代**：计算新的残差 $\mathbf{r}^{(1)} = \mathbf{y} - \mathbf{X}\hat{\boldsymbol{\beta}}^{(1)}$，然后返回第二步，用新的残差重新估计协[方差](@entry_id:200758)参数，得到 $\hat{\boldsymbol{\Sigma}}^{(2)}$ 和 $\hat{\boldsymbol{\beta}}^{(2)}$。这个过程可以一直迭代下去。
5.  **收敛**：当[系数估计](@entry_id:175952) $\hat{\boldsymbol{\beta}}^{(k)}$ 和协[方差](@entry_id:200758)[参数估计](@entry_id:139349) $\hat{\boldsymbol{\theta}}^{(k)}$（例如 $\hat{\rho}$ 和 $\hat{\sigma}^2$）在连续迭代中变化很小，或者当模型的[对数似然函数](@entry_id:168593)值趋于稳定时，迭代停止。

这个过程，也常被称为**迭代重加权最小二乘（Iteratively Reweighted Least Squares, IRLS）**，在适当的条件下，得到的FGLS估计量具有与真实GLS估计量相同的优良大样本性质（即[渐近有效](@entry_id:167883)性）。

#### 假设检验

在GLS框架下进行[假设检验](@entry_id:142556)的逻辑与OLS类似，都是比较有约束模型和无约束模型的[拟合优度](@entry_id:637026)。关键区别在于，“[拟合优度](@entry_id:637026)”必须用**广义[残差平方和](@entry_id:174395)（GRSS）**来衡量，即 $GRSS = \mathbf{e}^{\top}\boldsymbol{\Sigma}^{-1}\mathbf{e}$。

对于一个包含 $q$ 个线性约束的零假设 $H_0: \mathbf{R}\boldsymbol{\beta} = \mathbf{r}$，[F统计量](@entry_id:148252)的形式为：
$$ F = \frac{(GRSS_R - GRSS_U)/q}{GRSS_U/(n-p)} $$
其中 $GRSS_R$ 和 $GRSS_U$ 分别是施加约束的（受限）模型和未施加约束的（非受限）模型的广义[残差平方和](@entry_id:174395)。在实践中，我们用 $\hat{\boldsymbol{\Sigma}}$ 代替 $\boldsymbol{\Sigma}$。正如在  中看到的，使用这个正确的[F统计量](@entry_id:148252)至关重要，因为忽略[误差相关性](@entry_id:749076)而使用标准的OLS [F检验](@entry_id:274297)会产生严重误导的结论。

#### 数值稳定性考量

在实现GLS或FGLS时，直接计算 $\boldsymbol{\Sigma}^{-1}$ 并形成正规方程 $(\mathbf{X}^{\top}\boldsymbol{\Sigma}^{-1}\mathbf{X})$ 在数值上可能是不稳定的，特别是当 $\boldsymbol{\Sigma}$ 是病态（ill-conditioned）矩阵时。这样做会使问题的[条件数](@entry_id:145150)平方，从而放大[舍入误差](@entry_id:162651) 。一个更稳健的数值策略是：
1.  对 $\boldsymbol{\Sigma}$（或其估计 $\hat{\boldsymbol{\Sigma}}$）进行[Cholesky分解](@entry_id:147066)，得到 $\boldsymbol{\Sigma} = \mathbf{L}\mathbf{L}^{\top}$。
2.  通过求解三角[线性方程组](@entry_id:148943)来计算白化数据，例如，求解 $\mathbf{L}\mathbf{y}^*=\mathbf{y}$ 得到 $\mathbf{y}^* = \mathbf{L}^{-1}\mathbf{y}$（这避免了显式计算 $\mathbf{L}^{-1}$）。对 $\mathbf{X}$ 的每一列也做同样处理。
3.  对白化后的模型 $(\mathbf{y}^*, \mathbf{X}^*)$ 使用数值上更稳定的方法（如[QR分解](@entry_id:139154)）来求解[最小二乘问题](@entry_id:164198)。

这种方法避免了矩阵求逆和[条件数](@entry_id:145150)的平方，是高质量统计软件中的标准实践。

### GLS的稳健性与局限性

虽然GLS是一个强大的工具，但它的有效性依赖于我们对[误差协方差](@entry_id:194780)结构 $\boldsymbol{\Sigma}$ 的了解。同时，我们必须清楚GLS能解决什么问题，以及它不能解决什么问题。

#### 协[方差](@entry_id:200758)结构的错误设定

如果我们对 $\boldsymbol{\Sigma}$ 的结构做出了错误的假设（例如，错误地认为误差是[AR(1)过程](@entry_id:746502)，或者使用了错误的自[相关系数](@entry_id:147037) $\rho$），会发生什么？ 对此进行了深入分析。

假设真实的协方差矩阵是 $\boldsymbol{\Sigma}_0$，但我们使用了一个错误的 $\boldsymbol{\Sigma}$ 来进行GLS估计。结果是：
1.  **估计量仍然无偏**：只要回归量 $\mathbf{X}$ 是外生的（即与真实误差不相关），即使 $\boldsymbol{\Sigma}$ 被错误设定，GLS估计量 $\hat{\boldsymbol{\beta}}_{\mathrm{GLS}}(\boldsymbol{\Sigma})$ 仍然是无偏的。
2.  **效率损失**：这个估计量不再是BLUE。其真实[方差](@entry_id:200758)会大于使用正确 $\boldsymbol{\Sigma}_0$ 的有效GLS[估计量的方差](@entry_id:167223)。在  的例子中，使用 $\rho = 1/5$ 而真实值为 $\rho_0=1/2$ 时，效率损失因子（错误设定[估计量的方差](@entry_id:167223)与[有效估计量](@entry_id:271983)[方差](@entry_id:200758)之比）为 $73/72$，意味着[方差](@entry_id:200758)增加了约 $1.4\%$。
3.  **标准误错误**：更糟糕的是，如果我们天真地使用基于错误 $\boldsymbol{\Sigma}$ 的[方差](@entry_id:200758)公式 $\operatorname{Var}(\hat{\boldsymbol{\beta}}) = (\mathbf{X}^{\top}\boldsymbol{\Sigma}^{-1}\mathbf{X})^{-1}$ 来计算[标准误](@entry_id:635378)，得到的结果将是有偏的，可能高估或低估真实的不确定性。

这强调了在FGLS中仔细诊断和选择[误差协方差](@entry_id:194780)模型的重要性。

#### GLS与[内生性](@entry_id:142125)：一个重要的区别

学生们最常犯的错误之一是混淆**误差相关**和**[内生性](@entry_id:142125)**。这两个是完全不同的问题，需要不同的解决方案。
*   **误差相关**（Correlated Errors）意味着误差项之间彼此相关（$\mathbb{E}[\varepsilon_i \varepsilon_j] \neq 0$），但它们与回归量 $\mathbf{X}$ 仍然不相关（$\mathbb{E}[\boldsymbol{\varepsilon}|\mathbf{X}] = \mathbf{0}$）。GLS是为解决这个问题而设计的。
*   **[内生性](@entry_id:142125)**（Endogeneity）意味着误差项与一个或多个回归量相关（$\mathbb{E}[\boldsymbol{\varepsilon}|\mathbf{X}] \neq \mathbf{0}$）。这可能是由于遗漏变量、[测量误差](@entry_id:270998)或联立性造成的。

GLS无法修正由[内生性](@entry_id:142125)引起的偏误。考虑一个存在**测量误差**的模型 。假设真实模型为 $y_t = \beta_0 + \beta_1 x_t^* + \varepsilon_t$，但我们只能观测到带有误差的 $X_t = x_t^* + u_t$。我们实际回归的模型是 $y_t = \beta_0 + \beta_1 X_t + (\varepsilon_t - \beta_1 u_t)$。复合误差项 $(\varepsilon_t - \beta_1 u_t)$ 与回归量 $X_t$ 相关，因为它们都包含了 $u_t$。这是一个[内生性](@entry_id:142125)问题。

即使真实误差 $\varepsilon_t$ 自身也存在序列相关，应用GLS（或FGLS）也无济于事。GLS的[白化变换](@entry_id:637327)旨在处理 $\varepsilon_t$ 的相关性，但它无法消除 $X_t$ 和 $u_t$ 之间的根本关联。变换后的回归量仍然会与变换后的误差项相关，因此GLS估计量仍然是有偏和不一致的。

解决[内生性](@entry_id:142125)问题需要完全不同的工具，最典型的是**工具变量（Instrumental Variables, IV）**法。如  所述，如果能找到一个与真实变量 $x_t^*$ 相关、但与[测量误差](@entry_id:270998) $u_t$ 和结构误差 $\varepsilon_t$ 都不相关的外部工具变量 $Z_t$，那么就可以通过[两阶段最小二乘法](@entry_id:140182)（2SLS）等方法得到一致的估计。

总之，GLS是处理非球形误差的基石，它通过[白化变换](@entry_id:637327)恢复了OLS的优良性质。然而，它的成功依赖于对[误差协方差](@entry_id:194780)结构的正确识别，并且我们必须时刻警惕，不要指望它能解决由[内生性](@entry_id:142125)引起的更深层次的偏误问题。