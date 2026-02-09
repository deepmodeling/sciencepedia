## 引言
在线性回归分析中，一个核心假设是误差项彼此独立且方差恒定，即所谓的“球形误差”。然而，在经济学的时间序列、环境科学的空间数据或生物学的系统发育数据等众多实际应用中，这一理想假设常常被打破。数据点之间的内在联系导致误差项出现自相关或异方差，这种现象被称为误差相关。当这种情况发生时，我们惯用的普通最小二乘法（OLS）虽然可能仍是无偏的，但其估计效率会大大降低，更严重的是，其标准误计算会产生偏差，导致所有统计推断（如t检验和置信区间）都变得不可靠。

本文旨在解决这一关键问题，系统地介绍广义最小二乘法（GLS）作为应对相关误差的强大框架。通过学习本文，你将不再受限于传统的OLS假设，并能处理更复杂、更现实的数据结构。首先，在“原理与机制”一章中，我们将深入剖析OLS在误差相关时的具体失效表现，并详细阐述GLS如何通过巧妙的“白化”变换来恢复估计的有效性。接着，在“应用与跨学科联系”一章中，我们将展示GLS在经济学、工程学、演化生物学等多个领域的广泛应用，揭示其作为通用方法的强大生命力。最后，通过“动手实践”部分，你将有机会亲手实现和比较不同的估计方法，从而将理论知识转化为扎实的计算技能。

## 原理与机制

在经典的线性回归模型中，我们通常假设误差项是“球形”的，即它们是不相关且具有恒定方差的。数学上，这表示为 $\operatorname{Var}(\boldsymbol{\varepsilon}) = \sigma^2 \mathbf{I}$，其中 $\mathbf{I}$ 是单位矩阵。然而，在许多现实世界的应用中，尤其是在处理时间序列数据或面板数据时，这个假设往往被违背。误差项之间可能存在自相关（例如，今天的误差与昨天的误差相关）或异方差（不同观测值的误差方差不同）。当误差的协方差矩阵不再是单位矩阵的倍数，即 $\operatorname{Var}(\boldsymbol{\varepsilon}) = \boldsymbol{\Sigma}$，其中 $\boldsymbol{\Sigma}$ 是一个非对角矩阵时，我们就进入了广义线性模型的领域。本章将深入探讨误差相关性的后果，并介绍广义最小二乘法（Generalized Least Squares, GLS）作为解决这一问题的强大工具。

### OLS的失效：当误差不再独立

当误差项相关时，普通的最小二乘法（Ordinary Least Squares, OLS）会遇到两个主要问题。首先，虽然OLS估计量在某些条件下仍然是无偏的，但它不再是最佳线性无偏估计量（Best Linear Unbiased Estimator, BLUE）。其次，也是更严重的问题，标准的OLS方差估计量是有偏的，这导致所有基于它的统计推断（如t检验、F检验和置信区间）都变得无效。

#### 估计效率的损失

高斯-马尔可夫定理保证了在球形误差假设下OLS的有效性。当这个假设被打破，OLS估计量 $\hat{\boldsymbol{\beta}}_{\mathrm{OLS}}$ 就不再具有最小方差。存在其他线性无偏估计量，其方差更小。

考虑一个简单的例子 [@problem_id:3112090]，我们有三年的观测数据，模型为 $y = X\beta + \varepsilon$。假设真实误差遵循一阶自回归（AR(1)）过程，相关系数为 $\rho = 0.5$。这意味着相邻观测的误差是正相关的。如果我们忽略这种相关性并使用OLS，得到的回归系数估计量将不是最有效的。通过与考虑了相关性的GLS估计量进行比较，我们可以量化这种效率损失。在具体计算中，我们会发现 $\hat{\boldsymbol{\beta}}_{\mathrm{OLS}}$ 和 $\hat{\boldsymbol{\beta}}_{\mathrm{GLS}}$ 的值可能很接近，但它们的真实方差却有显著差异。例如，定义一个估计量相对于另一个估计量的相对效率为它们方差的迹之比。在 [@problem_id:3112090] 的设定下，GLS相对于OLS的效率增益可以计算出来，这个值大于1，明确表明GLS估计量具有更小的抽样变异性，因此更优。

这种效率损失也出现在异方差的情况下。例如，在一个过原点的回归模型 $Y_i = \beta x_i + \epsilon_i$ 中，如果误差方差与回归量的平方成正比，即 $\operatorname{Var}(\epsilon_i) = \sigma^2 x_i^2$ [@problem_id:1914836]，那么OLS估计量的方差将依赖于回归量 $x_i$ 的一个复杂组合，而为这种情况设计的GLS估计量的方差则更为简洁且更小。OLS相对于GLS的相对效率将是 $\frac{(\sum_{i=1}^{n}x_{i}^{2})^{2}}{n\sum_{i=1}^{n}x_{i}^{4}}$，根据柯西-施瓦茨不等式，这个值总是小于或等于1，表明OLS的效率较低。

#### 推断的失效

比效率损失更严重的是，OLS的标准误差计算完全错误。标准的OLS方差估计量公式 $\widehat{\operatorname{Var}}(\hat{\boldsymbol{\beta}}_{\mathrm{OLS}}) = \hat{\sigma}^2(\mathbf{X}^{\top}\mathbf{X})^{-1}$ 是基于 $\operatorname{Var}(\boldsymbol{\varepsilon}) = \sigma^2\mathbf{I}$ 推导的。当 $\operatorname{Var}(\boldsymbol{\varepsilon}) = \boldsymbol{\Sigma} \neq \sigma^2\mathbf{I}$ 时，$\hat{\boldsymbol{\beta}}_{\mathrm{OLS}}$ 的真实方差是 $\operatorname{Var}(\hat{\boldsymbol{\beta}}_{\mathrm{OLS}}) = (\mathbf{X}^{\top}\mathbf{X})^{-1}\mathbf{X}^{\top}\boldsymbol{\Sigma}\mathbf{X}(\mathbf{X}^{\top}\mathbf{X})^{-1}$，这被称为“三明治”估计量。

更重要的是，误差方差的OLS估计量 $\hat{\sigma}^{2}_{\mathrm{OLS}} = \frac{\mathbf{e}^{\top}\mathbf{e}}{n-p}$ 本身也变得有偏。在一个具有AR(1)误差的简单模型中，我们可以精确地推导出这个偏差 [@problem_id:3112065]。例如，在一个包含截距和线性趋势项的模型中，如果真实误差相关系数为 $\rho$，那么 $\hat{\sigma}^{2}_{\mathrm{OLS}}$ 的期望值将是 $\mathbb{E}[\hat{\sigma}^{2}_{\mathrm{OLS}}] = \sigma^2 \frac{1}{3}(3-4\rho+\rho^2)$。当 $\rho \neq 0$ 时，这个期望值不等于真实的 $\sigma^2$。例如，如果 $\rho$ 是正的（这是时间序列数据中最常见的情况），$\hat{\sigma}^{2}_{\mathrm{OLS}}$ 会倾向于低估真实的误差方差。这种偏差直接导致标准误的计算错误，从而使t统计量和F统计量不可靠。

一个具体的例子 [@problem_id:3112133] 可以说明这一点。在一个检验回归系数是否为零的假设检验中，如果数据误差存在AR(1)相关性（$\rho=0.5$），但我们错误地使用了OLS F检验，我们可能会得到一个非常大的F值（例如464.4）。然而，如果我们使用为相关误差设计的正确GLS F检验，我们会得到一个显著不同且小得多的F值（例如182.2）。这表明OLS会严重夸大统计显著性，可能导致我们错误地拒绝原假设。

### 广义最小二乘法的原理：白化变换

GLS的核心思想不是发明一种全新的估计方法，而是通过一种巧妙的线性变换，将一个具有相关误差的“复杂”模型，转化为一个满足经典假设的“简单”模型，然后对这个新模型应用我们熟悉的OLS。这个过程被称为**白化（whitening）**。

假设误差的协方差矩阵为 $\boldsymbol{\Sigma}$。因为 $\boldsymbol{\Sigma}$ 是对称正定矩阵，我们可以找到一个非奇异的**白化矩阵** $\mathbf{W}$，使得 $\mathbf{W}\boldsymbol{\Sigma}\mathbf{W}^{\top} = \sigma^2\mathbf{I}$。这意味着，如果我们用 $\mathbf{W}$ 左乘原始的回归方程 $ \mathbf{y}=\mathbf{X}\boldsymbol{\beta}+\boldsymbol{\varepsilon} $，我们得到一个新的回归模型：
$$ \mathbf{W}\mathbf{y} = \mathbf{W}\mathbf{X}\boldsymbol{\beta} + \mathbf{W}\boldsymbol{\varepsilon} $$
或者写成：
$$ \mathbf{y}^* = \mathbf{X}^*\boldsymbol{\beta} + \boldsymbol{\varepsilon}^* $$
其中 $\mathbf{y}^* = \mathbf{W}\mathbf{y}$，$\mathbf{X}^* = \mathbf{W}\mathbf{X}$，$\boldsymbol{\varepsilon}^* = \mathbf{W}\boldsymbol{\varepsilon}$。

这个变换的神奇之处在于，新的误差项 $\boldsymbol{\varepsilon}^*$ 的协方差矩阵是：
$$ \operatorname{Var}(\boldsymbol{\varepsilon}^*) = \operatorname{Var}(\mathbf{W}\boldsymbol{\varepsilon}) = \mathbf{W}\operatorname{Var}(\boldsymbol{\varepsilon})\mathbf{W}^{\top} = \mathbf{W}\boldsymbol{\Sigma}\mathbf{W}^{\top} = \sigma^2\mathbf{I} $$
新的误差项 $\boldsymbol{\varepsilon}^*$ 是球形的！它们不相关且具有恒定的方差。因此，我们可以在变换后的模型 $(\mathbf{y}^*, \mathbf{X}^*)$ 上安全地使用OLS来估计 $\boldsymbol{\beta}$。对变换后模型应用OLS得到的估计量，就是原始模型的GLS估计量。

一个寻找白化矩阵 $\mathbf{W}$ 的常见方法是利用 $\boldsymbol{\Sigma}$ 的逆矩阵。因为 $\mathbf{W}\boldsymbol{\Sigma}\mathbf{W}^{\top}$ 正比于 $\mathbf{I}$，这意味着 $\mathbf{W}^{\top}\mathbf{W}$ 必须正比于 $\boldsymbol{\Sigma}^{-1}$。我们可以通过Cholesky分解找到这样一个矩阵。例如，我们可以分解 $\boldsymbol{\Sigma} = \mathbf{L}\mathbf{L}^{\top}$，其中 $\mathbf{L}$ 是下三角矩阵，然后取 $\mathbf{W} = \mathbf{L}^{-1}$。这样，$\mathbf{W}\boldsymbol{\Sigma}\mathbf{W}^{\top} = \mathbf{L}^{-1}(\mathbf{L}\mathbf{L}^{\top})(\mathbf{L}^{-1})^{\top} = \mathbf{I}$ [@problem_id:3112134]。

以AR(1)误差过程为例，$\varepsilon_t = \rho \varepsilon_{t-1} + u_t$。这个白化变换有一个非常直观的形式，被称为**准差分（quasi-differencing）** [@problem_id:3112108]。对于 $t \ge 2$ 的观测值，我们可以通过从当前观测值中减去前一期观测值的 $\rho$ 倍来变换数据：
$$ y_t - \rho y_{t-1} = (\mathbf{x}_t^{\top}\boldsymbol{\beta} + \varepsilon_t) - \rho(\mathbf{x}_{t-1}^{\top}\boldsymbol{\beta} + \varepsilon_{t-1}) = (\mathbf{x}_t^{\top} - \rho \mathbf{x}_{t-1}^{\top})\boldsymbol{\beta} + (\varepsilon_t - \rho \varepsilon_{t-1}) $$
由于 $\varepsilon_t - \rho \varepsilon_{t-1} = u_t$，而 $u_t$ 是不相关的白噪声，这个变换成功地消除了 $t=2, \dots, n$ 之间的误差相关性。然而，为了确保所有变换后的误差都具有相同的方差 $\sigma_u^2$，第一个观测值需要特殊处理。在平稳性假设下，$\operatorname{Var}(\varepsilon_1) = \frac{\sigma_u^2}{1-\rho^2}$。为了使变换后的误差方差为 $\sigma_u^2$，我们需要将第一个观测方程乘以 $\sqrt{1-\rho^2}$。这个包含特殊处理第一个观测值的完整变换被称为**Prais-Winsten变换**。对经过Prais-Winsten变换的数据应用OLS，就等价于执行GLS。

### GLS估计量及其性质

通过对变换后的模型应用OLS，或者直接最小化**广义残差平方和**，我们可以推导出GLS估计量的解析形式。广义残差平方和（或称马氏距离的平方）定义为：
$$ S(\boldsymbol{\beta}) = (\mathbf{y} - \mathbf{X}\boldsymbol{\beta})^{\top}\boldsymbol{\Sigma}^{-1}(\mathbf{y} - \mathbf{X}\boldsymbol{\beta}) $$
最小化这个目标函数 [@problem_id:2218053] 会得到**广义正规方程**（generalized normal equations）：
$$ (\mathbf{X}^{\top}\boldsymbol{\Sigma}^{-1}\mathbf{X})\hat{\boldsymbol{\beta}} = \mathbf{X}^{\top}\boldsymbol{\Sigma}^{-1}\mathbf{y} $$
如果矩阵 $\mathbf{X}^{\top}\boldsymbol{\Sigma}^{-1}\mathbf{X}$ 是可逆的（通常在 $\mathbf{X}$ 满列秩时成立），那么唯一的**GLS估计量**为：
$$ \hat{\boldsymbol{\beta}}_{\mathrm{GLS}} = (\mathbf{X}^{\top}\boldsymbol{\Sigma}^{-1}\mathbf{X})^{-1}\mathbf{X}^{\top}\boldsymbol{\Sigma}^{-1}\mathbf{y} $$
这个估计量具有优良的统计性质：

1.  **无偏性**：与OLS一样，只要误差项的期望为零且与回归量无关，GLS估计量就是无偏的，即 $\mathbb{E}[\hat{\boldsymbol{\beta}}_{\mathrm{GLS}}] = \boldsymbol{\beta}$。
2.  **方差**：GLS估计量的方差由下式给出：
    $$ \operatorname{Var}(\hat{\boldsymbol{\beta}}_{\mathrm{GLS}}) = (\mathbf{X}^{\top}\boldsymbol{\Sigma}^{-1}\mathbf{X})^{-1} $$
    需要注意的是，如果误差协方差矩阵写为 $\operatorname{Var}(\boldsymbol{\varepsilon}) = \sigma^2 \boldsymbol{\Omega}$，其中 $\boldsymbol{\Omega}$ 是已知的相关矩阵，而 $\sigma^2$ 未知，那么GLS估计量为 $\hat{\boldsymbol{\beta}}_{\mathrm{GLS}} = (\mathbf{X}^{\top}\boldsymbol{\Omega}^{-1}\mathbf{X})^{-1}\mathbf{X}^{\top}\boldsymbol{\Omega}^{-1}\mathbf{y}$，其方差为 $\operatorname{Var}(\hat{\boldsymbol{\beta}}_{\mathrm{GLS}}) = \sigma^2(\mathbf{X}^{\top}\boldsymbol{\Omega}^{-1}\mathbf{X})^{-1}$。
3.  **有效性**：**Aitken定理**（高斯-马尔可夫定理的推广）指出，GLS估计量是所有线性无偏估计量中方差最小的，即GLS是BLUE。

我们可以通过一个具体的计算例子 [@problem_id:3112090] 来体会OLS和GLS的区别。给定一个包含截距和单个预测变量的3个观测值的数据集，以及一个AR(1)误差结构（$\rho=0.5$），我们可以分别计算OLS和GLS估计量。例如，我们可能得到 $\hat{\boldsymbol{\beta}}_{\mathrm{OLS}} = \begin{pmatrix} 7/6 & 3/2 \end{pmatrix}^{\top}$ 和 $\hat{\boldsymbol{\beta}}_{\mathrm{GLS}} = \begin{pmatrix} 11/10 & 3/2 \end{pmatrix}^{\top}$。虽然这两个点估计在数值上可能相差不大，但它们背后的不确定性却大相径庭。通过计算它们的真实方差矩阵，我们会发现 $\operatorname{tr}(\operatorname{Var}(\hat{\boldsymbol{\beta}}_{\mathrm{OLS}}))$ 明显大于 $\operatorname{tr}(\operatorname{Var}(\hat{\boldsymbol{\beta}}_{\mathrm{GLS}}))$。在本例中，效率增益 $\frac{\operatorname{tr}(\operatorname{Var}(\hat{\boldsymbol{\beta}}_{\mathrm{OLS}}))}{\operatorname{tr}(\operatorname{Var}(\hat{\boldsymbol{\beta}}_{\mathrm{GLS}}))} = \frac{245}{243} \approx 1.008$。虽然在这个小样本中增益看似不大，但在更强的相关性或更大的数据集中，这种差异会变得非常显著。

### 实践中的GLS：可行GLS与假设检验

到目前为止，我们一直假设误差协方差矩阵 $\boldsymbol{\Sigma}$ 是已知的。但在实践中，我们几乎从不知道 $\boldsymbol{\Sigma}$ 的确切形式，我们只对其结构（如AR(1)）有所怀疑，并不知道其参数（如 $\rho$ 和 $\sigma^2$）。这就引出了**可行广义最小二乘法（Feasible Generalized Least Squares, FGLS）**。

#### 可行GLS（FGLS）

FGLS是一个多步骤的估计程序，其基本思想是用一个一致的估计量 $\hat{\boldsymbol{\Sigma}}$ 来代替未知的 $\boldsymbol{\Sigma}$。一个典型的FGLS迭代算法 [@problem_id:3112091] 如下：

1.  **初始化**：运行OLS得到初始的系数估计 $\hat{\boldsymbol{\beta}}^{(0)}$ 和残差 $\mathbf{r}^{(0)} = \mathbf{y} - \mathbf{X}\hat{\boldsymbol{\beta}}^{(0)}$。
2.  **估计协方差参数**：使用残差 $\mathbf{r}^{(0)}$ 来估计 $\boldsymbol{\Sigma}$ 的参数。例如，在AR(1)模型中，我们可以通过残差的样本自相关来估计 $\rho$，即 $\hat{\rho}^{(1)} = \frac{\sum_{t=2}^n r^{(0)}_t r^{(0)}_{t-1}}{\sum_{t=1}^{n-1} (r^{(0)}_t)^2}$。然后估计创新方差 $\sigma_u^2$。从而构造出协方差矩阵的估计 $\hat{\boldsymbol{\Sigma}}^{(1)}$。
3.  **GLS步骤**：使用 $\hat{\boldsymbol{\Sigma}}^{(1)}$ 来计算新的系数估计 $\hat{\boldsymbol{\beta}}^{(1)} = (\mathbf{X}^{\top}(\hat{\boldsymbol{\Sigma}}^{(1)})^{-1}\mathbf{X})^{-1}\mathbf{X}^{\top}(\hat{\boldsymbol{\Sigma}}^{(1)})^{-1}\mathbf{y}$。
4.  **迭代**：计算新的残差 $\mathbf{r}^{(1)} = \mathbf{y} - \mathbf{X}\hat{\boldsymbol{\beta}}^{(1)}$，然后返回第二步，用新的残差重新估计协方差参数，得到 $\hat{\boldsymbol{\Sigma}}^{(2)}$ 和 $\hat{\boldsymbol{\beta}}^{(2)}$。这个过程可以一直迭代下去。
5.  **收敛**：当系数估计 $\hat{\boldsymbol{\beta}}^{(k)}$ 和协方差参数估计 $\hat{\boldsymbol{\theta}}^{(k)}$（例如 $\hat{\rho}$ 和 $\hat{\sigma}^2$）在连续迭代中变化很小，或者当模型的对数似然函数值趋于稳定时，迭代停止。

这个过程，也常被称为**迭代重加权最小二乘（Iteratively Reweighted Least Squares, IRLS）**，在适当的条件下，得到的FGLS估计量具有与真实GLS估计量相同的优良大样本性质（即渐近有效性）。

#### 假设检验

在GLS框架下进行假设检验的逻辑与OLS类似，都是比较有约束模型和无约束模型的拟合优度。关键区别在于，“拟合优度”必须用**广义残差平方和（GRSS）**来衡量，即 $GRSS = \mathbf{e}^{\top}\boldsymbol{\Sigma}^{-1}\mathbf{e}$。

对于一个包含 $q$ 个线性约束的零假设 $H_0: \mathbf{R}\boldsymbol{\beta} = \mathbf{r}$，F统计量的形式为：
$$ F = \frac{(GRSS_R - GRSS_U)/q}{GRSS_U/(n-p)} $$
其中 $GRSS_R$ 和 $GRSS_U$ 分别是施加约束的（受限）模型和未施加约束的（非受限）模型的广义残差平方和。在实践中，我们用 $\hat{\boldsymbol{\Sigma}}$ 代替 $\boldsymbol{\Sigma}$。正如在 [@problem_id:3112133] 中看到的，使用这个正确的F统计量至关重要，因为忽略误差相关性而使用标准的OLS F检验会产生严重误导的结论。

#### 数值稳定性考量

在实现GLS或FGLS时，直接计算 $\boldsymbol{\Sigma}^{-1}$ 并形成正规方程 $(\mathbf{X}^{\top}\boldsymbol{\Sigma}^{-1}\mathbf{X})$ 在数值上可能是不稳定的，特别是当 $\boldsymbol{\Sigma}$ 是病态（ill-conditioned）矩阵时。这样做会使问题的条件数平方，从而放大舍入误差 [@problem_id:3112134]。一个更稳健的数值策略是：
1.  对 $\boldsymbol{\Sigma}$（或其估计 $\hat{\boldsymbol{\Sigma}}$）进行Cholesky分解，得到 $\boldsymbol{\Sigma} = \mathbf{L}\mathbf{L}^{\top}$。
2.  通过求解三角线性方程组来计算白化数据，例如，求解 $\mathbf{L}\mathbf{y}^*=\mathbf{y}$ 得到 $\mathbf{y}^* = \mathbf{L}^{-1}\mathbf{y}$（这避免了显式计算 $\mathbf{L}^{-1}$）。对 $\mathbf{X}$ 的每一列也做同样处理。
3.  对白化后的模型 $(\mathbf{y}^*, \mathbf{X}^*)$ 使用数值上更稳定的方法（如QR分解）来求解最小二乘问题。

这种方法避免了矩阵求逆和条件数的平方，是高质量统计软件中的标准实践。

### GLS的稳健性与局限性

虽然GLS是一个强大的工具，但它的有效性依赖于我们对误差协方差结构 $\boldsymbol{\Sigma}$ 的了解。同时，我们必须清楚GLS能解决什么问题，以及它不能解决什么问题。

#### 协方差结构的错误设定

如果我们对 $\boldsymbol{\Sigma}$ 的结构做出了错误的假设（例如，错误地认为误差是AR(1)过程，或者使用了错误的自相关系数 $\rho$），会发生什么？[@problem_id:3112125] 对此进行了深入分析。

假设真实的协方差矩阵是 $\boldsymbol{\Sigma}_0$，但我们使用了一个错误的 $\boldsymbol{\Sigma}$ 来进行GLS估计。结果是：
1.  **估计量仍然无偏**：只要回归量 $\mathbf{X}$ 是外生的（即与真实误差不相关），即使 $\boldsymbol{\Sigma}$ 被错误设定，GLS估计量 $\hat{\boldsymbol{\beta}}_{\mathrm{GLS}}(\boldsymbol{\Sigma})$ 仍然是无偏的。
2.  **效率损失**：这个估计量不再是BLUE。其真实方差会大于使用正确 $\boldsymbol{\Sigma}_0$ 的有效GLS估计量的方差。在 [@problem_id:3112125] 的例子中，使用 $\rho = 1/5$ 而真实值为 $\rho_0=1/2$ 时，效率损失因子（错误设定估计量的方差与有效估计量方差之比）为 $73/72$，意味着方差增加了约 $1.4\%$。
3.  **标准误错误**：更糟糕的是，如果我们天真地使用基于错误 $\boldsymbol{\Sigma}$ 的方差公式 $\operatorname{Var}(\hat{\boldsymbol{\beta}}) = (\mathbf{X}^{\top}\boldsymbol{\Sigma}^{-1}\mathbf{X})^{-1}$ 来计算标准误，得到的结果将是有偏的，可能高估或低估真实的不确定性。

这强调了在FGLS中仔细诊断和选择误差协方差模型的重要性。

#### GLS与内生性：一个重要的区别

学生们最常犯的错误之一是混淆**误差相关**和**内生性**。这两个是完全不同的问题，需要不同的解决方案。
*   **误差相关**（Correlated Errors）意味着误差项之间彼此相关（$\mathbb{E}[\varepsilon_i \varepsilon_j] \neq 0$），但它们与回归量 $\mathbf{X}$ 仍然不相关（$\mathbb{E}[\boldsymbol{\varepsilon}|\mathbf{X}] = \mathbf{0}$）。GLS是为解决这个问题而设计的。
*   **内生性**（Endogeneity）意味着误差项与一个或多个回归量相关（$\mathbb{E}[\boldsymbol{\varepsilon}|\mathbf{X}] \neq \mathbf{0}$）。这可能是由于遗漏变量、测量误差或联立性造成的。

GLS无法修正由内生性引起的偏误。考虑一个存在**测量误差**的模型 [@problem_id:3112066]。假设真实模型为 $y_t = \beta_0 + \beta_1 x_t^* + \varepsilon_t$，但我们只能观测到带有误差的 $X_t = x_t^* + u_t$。我们实际回归的模型是 $y_t = \beta_0 + \beta_1 X_t + (\varepsilon_t - \beta_1 u_t)$。复合误差项 $(\varepsilon_t - \beta_1 u_t)$ 与回归量 $X_t$ 相关，因为它们都包含了 $u_t$。这是一个内生性问题。

即使真实误差 $\varepsilon_t$ 自身也存在序列相关，应用GLS（或FGLS）也无济于事。GLS的白化变换旨在处理 $\varepsilon_t$ 的相关性，但它无法消除 $X_t$ 和 $u_t$ 之间的根本关联。变换后的回归量仍然会与变换后的误差项相关，因此GLS估计量仍然是有偏和不一致的。

解决内生性问题需要完全不同的工具，最典型的是**工具变量（Instrumental Variables, IV）**法。如 [@problem_id:3112066] 所述，如果能找到一个与真实变量 $x_t^*$ 相关、但与测量误差 $u_t$ 和结构误差 $\varepsilon_t$ 都不相关的外部工具变量 $Z_t$，那么就可以通过两阶段最小二乘法（2SLS）等方法得到一致的估计。

总之，GLS是处理非球形误差的基石，它通过白化变换恢复了OLS的优良性质。然而，它的成功依赖于对误差协方差结构的正确识别，并且我们必须时刻警惕，不要指望它能解决由内生性引起的更深层次的偏误问题。