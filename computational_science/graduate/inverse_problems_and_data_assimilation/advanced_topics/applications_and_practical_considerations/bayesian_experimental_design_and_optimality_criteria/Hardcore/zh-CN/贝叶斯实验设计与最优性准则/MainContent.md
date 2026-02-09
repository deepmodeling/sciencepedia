## 引言
在科学探索与工程实践中，我们如何才能最有效地收集数据以揭示未知世界的奥秘？面对有限的资源——无论是时间、金钱还是计算能力——每一个实验决策都至关重要。贝叶斯实验设计（Bayesian Experimental Design, BED）为这一根本问题提供了严谨的数学框架。它将实验设计视为一个在不确定性下进行理性决策的过程，其目标是主动选择能够最大程度减少我们对未知参数不确定性的数据采集方案。本文旨在系统地介绍贝叶斯实验设计的核心思想、关键方法及其在多学科交叉领域的广泛应用。

本文分为三个核心章节，将引导读者从理论基础走向实际应用。在“原则与机制”一章中，我们将深入探讨贝叶斯实验设计的决策论与信息论根基，阐明如预期信息增益（EIG）和A-最优性等核心效用准则的内涵与联系。随后的“应用与跨学科联系”一章将展示这些理论如何在传感器网络布局、动态系统追踪、稳健设计等真实场景中发挥作用，揭示其解决复杂问题的强大能力。最后，在“动手实践”部分，读者将通过具体问题练习，加深对收益递减、序贯决策等关键概念的理解。通过本次学习，您将掌握在不确定性下进行信息驱动决策的科学方法论。

## 原则与机制

在前一章中，我们介绍了贝叶斯实验设计的基本思想，即通过主动选择实验来最有效地减少对未知参数的不确定性。本章将深入探讨支撑这一思想的核心原则与机制。我们将首先建立贝叶斯实验设计的决策论和信息论基础，然后探讨如何在实践中应用这些理论，特别是在面对非线性和约束等复杂情况时。

### 贝叶斯实验设计的效用理论基础

贝叶斯实验设计的核心在于将其构建为一个决策问题。我们的目标是从一组可能的实验设计 $d \in \mathcal{D}$ 中，选择一个能够最大化某种**效用 (utility)** 的设计。效用函数 $U(d)$ 是一个标量函数，它量化了执行设计 $d$ 所带来的预期价值。一个好的实验设计应该能够最大程度地减少我们对未知参数 $\boldsymbol{\theta}$ 的不确定性。

我们可以从两个主要角度来定义效用函数：

1.  **基于损失的决策论方法 (Loss-Based Decision-Theoretic Approach)**：这种方法将实验设计的选择与最终的统计推断任务联系起来。我们首先定义一个**损失函数 (loss function)** $L(\hat{\boldsymbol{\theta}}, \boldsymbol{\theta})$，它量化了用估计值 $\hat{\boldsymbol{\theta}}$ 来代替真实值 $\boldsymbol{\theta}$ 所带来的成本。在进行实验并获得数据 $\mathbf{y}$ 后，我们会得到一个后验分布 $p(\boldsymbol{\theta}|\mathbf{y}, d)$。贝叶斯决策理论的目标是最小化**后验期望损失 (expected posterior loss)**。对于一个给定的实验设计 $d$，我们无法预知将观测到什么数据 $\mathbf{y}$，因此我们选择设计 $d$ 的依据是最小化在所有可能数据上的**贝叶斯风险 (Bayes risk)**，即期望的后验期望损失：
    $R(d) = \mathbb{E}_{\mathbf{y}|d} \left[ \inf_{\hat{\boldsymbol{\theta}}} \mathbb{E}_{\boldsymbol{\theta}|\mathbf{y}, d} [L(\hat{\boldsymbol{\theta}}, \boldsymbol{\theta})] \right]$
    其中，内部的期望是关于后验分布的，而外部的期望是关于数据的边缘分布 $p(\mathbf{y}|d)$ 的。一个常见的损失函数是**平方误差损失 (squared-error loss)**，$L(\hat{\boldsymbol{\theta}}, \boldsymbol{\theta}) = ||\hat{\boldsymbol{\theta}} - \boldsymbol{\theta}||^2_2$。在这种情况下，最小化后验期望损失的贝叶斯估计量是后验均值，而贝叶斯风险正比于后验协方差矩阵的迹 $\text{tr}(\boldsymbol{\Sigma}_{\text{post}})$。因此，基于平方误差损失的设计准则演变为选择一个设计 $d$ 来最小化预期的后验协方差矩阵的迹。这被称为**A-最优性 (A-optimality)**。

2.  **基于信息论的方法 (Information-Theoretic Approach)**：这种方法不直接与特定的估计任务挂钩，而是旨在最大化实验所能提供的信息量。其核心思想是，一个好的实验应该能最大程度地减少我们对 $\boldsymbol{\theta}$ 的“惊讶程度”或不确定性。这一思想的自然度量是**预期信息增益 (Expected Information Gain, EIG)**，也称为林德利测度 (Lindley's measure)。

在接下来的小节中，我们将详细探讨这两种方法及其相互关系。

### 信息论准则：预期信息增益

预期信息增益 (EIG) 是贝叶斯实验设计中最核心和最符合第一性原理的效用函数。它衡量了在进行一个实验后，我们期望对参数 $\boldsymbol{\theta}$ 的知识能增加多少。

形式上，EIG 定义为后验分布 $p(\boldsymbol{\theta}|\mathbf{y}, d)$ 相对于先验分布 $p(\boldsymbol{\theta})$ 的**Kullback-Leibler散度 (Kullback-Leibler, KL, divergence)** 在所有可能数据 $\mathbf{y}$ 上的期望值：
$$
U_{\text{EIG}}(d) = \mathbb{E}_{\mathbf{y}|d} \left[ D_{\text{KL}}(p(\boldsymbol{\theta}|\mathbf{y}, d) \,||\, p(\boldsymbol{\theta})) \right]
$$
其中 $D_{\text{KL}}(p||q) = \int p(x) \log \frac{p(x)}{q(x)} dx$。这个量有一个更直观且等价的解释：它等于参数 $\boldsymbol{\theta}$ 和数据 $\mathbf{y}$ 之间的**互信息 (mutual information)** $I(\boldsymbol{\theta}; \mathbf{y}|d)$。[@problem_id:3367042]

互信息可以从两个等价的角度来计算，这两个角度都为我们提供了深刻的洞见：

1.  **熵减少 (Entropy Reduction)**：互信息等于先验熵减去期望的后验熵。
    $$
    I(\boldsymbol{\theta}; \mathbf{y}|d) = H(\boldsymbol{\theta}) - \mathbb{E}_{\mathbf{y}|d}[H(\boldsymbol{\theta}|\mathbf{y}, d)]
    $$
    这里，$H(\boldsymbol{\theta}) = -\int p(\boldsymbol{\theta}) \log p(\boldsymbol{\theta}) d\boldsymbol{\theta}$ 是参数的先验微分熵，度量了我们开始实验前的不确定性。$H(\boldsymbol{\theta}|\mathbf{y}, d)$ 是给定数据 $\mathbf{y}$ 后的后验熵，度量了实验结束后的剩余不确定性。EIG 因此量化了实验平均能“消除”多少不确定性。[@problem_id:3367042] [@problem_id:3367054]

2.  **证据熵与噪声熵之差 (Difference between Evidence and Noise Entropy)**：互信息也等于数据的边缘熵减去其条件熵。
    $$
    I(\boldsymbol{\theta}; \mathbf{y}|d) = H(\mathbf{y}|d) - \mathbb{E}_{\boldsymbol{\theta}}[H(\mathbf{y}|\boldsymbol{\theta}, d)]
    $$
    这里，$H(\mathbf{y}|d)$ 是数据 $\mathbf{y}$ 的边缘分布（或称证据）的熵，它包含了来自参数不确定性和测量噪声不确定性的综合影响。而 $\mathbb{E}_{\boldsymbol{\theta}}[H(\mathbf{y}|\boldsymbol{\theta}, d)]$ 是在给定参数 $\boldsymbol{\theta}$ 的情况下的数据熵（即噪声熵）的期望。因此，EIG 也衡量了数据中由参数 $\boldsymbol{\theta}$ 引起的不确定性占总不确定性的比例。[@problem_id:3367042]

对于线性高斯模型，EIG 具有优美的闭式解。考虑一个线性观测模型 $\mathbf{y}_d = \mathbf{H}_d \boldsymbol{\theta} + \boldsymbol{\varepsilon}_d$，其中先验 $\boldsymbol{\theta} \sim \mathcal{N}(\boldsymbol{\mu}_{\text{pr}}, \boldsymbol{\Sigma}_{\text{pr}})$，噪声 $\boldsymbol{\varepsilon}_d \sim \mathcal{N}(\mathbf{0}, \mathbf{R}_d)$。利用上述第二种互信息表达形式，我们可以推导出 [@problem_id:3367054]：
$$
U_{\text{EIG}}(d) = \frac{1}{2} \ln \left( \det(\mathbf{I} + \mathbf{R}_d^{-1/2} \mathbf{H}_d \boldsymbol{\Sigma}_{\text{pr}} \mathbf{H}_d^{\top} \mathbf{R}_d^{-1/2}) \right) = \frac{1}{2} \ln \left( \frac{\det(\mathbf{H}_d \boldsymbol{\Sigma}_{\text{pr}} \mathbf{H}_d^{\top} + \mathbf{R}_d)}{\det(\mathbf{R}_d)} \right)
$$
这个公式揭示了信息增益取决于信噪比。具体来说，它取决于由先验不确定性传播到观测空间的信号协方差 $\mathbf{H}_d \boldsymbol{\Sigma}_{\text{pr}} \mathbf{H}_d^{\top}$ 与噪声协方差 $\mathbf{R}_d$ 的相对大小。例如，在一个简单标量问题中，观测 $y_d = h_d^{\top}\theta + \varepsilon_d$，其中先验 $\theta \sim \mathcal{N}(0, S)$，噪声 $\varepsilon_d \sim \mathcal{N}(0, r_d)$，信息增益为 $I(\theta; y_d|d) = \frac{1}{2} \ln(1 + \frac{h_d^{\top} S h_d}{r_d})$。[@problem_id:3367054] 假设我们有两个备选设计，设计 $d_1$ 的参数为 $h_{d_1} = \begin{pmatrix} 1 \\ 0 \end{pmatrix}$ 和 $r_{d_1}=0.5$，设计 $d_2$ 的参数为 $h_{d_2} = \begin{pmatrix} 1 \\ 1 \end{pmatrix}$ 和 $r_{d_2}=0.2$。若先验协方差为 $S = \begin{pmatrix} 2  1 \\ 1  3 \end{pmatrix}$，我们可以计算出设计1的信息增益为 $I_1 = \frac{1}{2}\ln(5)$，设计2的信息增益为 $I_2 = \frac{1}{2}\ln(36) = \ln(6)$。由于 $\ln(6) > \frac{1}{2}\ln(5)$，设计2是更优的选择，因为它能提供更多的信息。

### 基于损失的准则及其与经典设计的联系

现在我们回到基于损失的方法，并以 **A-最优性** 为例进行探讨。A-最优性旨在最小化后验协方差矩阵的迹，$\text{tr}(\boldsymbol{\Sigma}_{\text{post}})$，这对应于最小化所有参数估计的平均后验方差。

对于线性高斯模型，后验协方差矩阵 $\boldsymbol{\Sigma}_{\text{post}}$ 与先验协方差 $\boldsymbol{\Sigma}_{\text{pr}}$ 和由数据提供的**费雪信息矩阵 (Fisher Information Matrix, FIM)** $\mathbf{F}$ 相关联，其关系式为：
$$
\boldsymbol{\Sigma}_{\text{post}}^{-1} = \boldsymbol{\Sigma}_{\text{pr}}^{-1} + \mathbf{F} \quad \implies \quad \boldsymbol{\Sigma}_{\text{post}} = (\boldsymbol{\Sigma}_{\text{pr}}^{-1} + \mathbf{F})^{-1}
$$
贝叶斯 A-最优设计的目标就是选择一个设计 $d$ 以最小化 $\text{tr}((\boldsymbol{\Sigma}_{\text{pr}}^{-1} + \mathbf{F}(d))^{-1})$。

贝叶斯设计与经典的（频率学派）实验设计之间存在深刻的联系。频率学派的设计通常不考虑先验信息，其目标是基于数据本身最大化推断的精度。例如，频率学派的 A-最优性旨在最小化参数最大似然估计量 (MLE) 的渐近协方差矩阵的迹，该协方差矩阵由费雪信息矩阵的逆给出，即最小化 $\text{tr}(\mathbf{F}^{-1})$。

一个关键的理论结果是，在先验信息变得“无信息”的极限情况下，贝叶斯设计准则会收敛到其对应的频率学派准则。考虑一个简单的例子 [@problem_id:3367030]，我们要估计二维参数 $\boldsymbol{\theta}$，其先验为 $\boldsymbol{\theta} \sim \mathcal{N}(0, \tau^2 I_2)$。我们可以在两种传感器之间分配总共 $n$ 次观测。传感器1测量 $\theta_1$，噪声方差为 $\sigma_1^2$；传感器2测量 $\theta_2$，噪声方差为 $\sigma_2^2$。设计变量是分配给传感器1的观测比例 $w \in [0,1]$。贝叶斯 A-最优设计的目标是最小化后验协方差的迹。通过求解此优化问题，可以得到最优比例 $w^{\star}(\tau)$。当我们取先验方差 $\tau^2 \to \infty$（即先验变得平坦或无信息）的极限时，先验精度 $\boldsymbol{\Sigma}_{\text{pr}}^{-1} = \frac{1}{\tau^2}I_2 \to \mathbf{0}$。此时，后验协方差 $\boldsymbol{\Sigma}_{\text{post}}$ 近似于 $\mathbf{F}^{-1}$。最小化 $\text{tr}(\boldsymbol{\Sigma}_{\text{post}})$ 的问题就变成了最小化 $\text{tr}(\mathbf{F}^{-1})$。在这个极限下，最优设计比例收敛于：
$$
w^{\star}(\infty) = \frac{\sigma_1}{\sigma_1 + \sigma_2}
$$
这个结果完美地展示了贝叶斯方法是如何包含并推广经典方法的：当先验信息很弱时，数据的主导作用使贝叶斯设计趋向于经典设计。

### 费雪信息的作用与近似方法

在更一般的非线性问题中，计算完整的 EIG 或贝叶斯风险通常是困难的，因为后验分布可能没有闭式解。在这种情况下，**费雪信息矩阵 (FIM)** 和基于它的近似方法扮演了至关重要的角色。

对于一个由似然函数 $p(\mathbf{y}|\boldsymbol{\theta})$ 定义的模型，FIM 是一个 $p \times p$ 矩阵（$p$ 是参数维度），其元素为：
$$
[\mathbf{F}(\boldsymbol{\theta})]_{ij} = \mathbb{E}_{\mathbf{y}|\boldsymbol{\theta}}\left[ \left(\frac{\partial \log p(\mathbf{y}|\boldsymbol{\theta})}{\partial \theta_i}\right) \left(\frac{\partial \log p(\mathbf{y}|\boldsymbol{\theta})}{\partial \theta_j}\right) \right]
$$
FIM 衡量了数据 $\mathbf{y}$ 对参数 $\boldsymbol{\theta}$ 的局部敏感度。在许多情况下（例如高斯噪声），FIM 可以表示为 $\mathbf{F}(\boldsymbol{\theta}) = \mathbf{J}(\boldsymbol{\theta})^{\top} \mathbf{R}^{-1} \mathbf{J}(\boldsymbol{\theta})$，其中 $\mathbf{J}(\boldsymbol{\theta})$ 是前向模型关于参数的**雅可比矩阵 (Jacobian matrix)**，$\mathbf{R}$ 是噪声协方差。[@problem_id:3367033]

在**拉普拉斯近似 (Laplace approximation)**下，我们将后验分布近似为一个高斯分布，其中心位于后验模式（最大后验概率点，MAP），其精度矩阵（协方差的逆）由负对数后验的**海森矩阵 (Hessian matrix)** 在 MAP 点的值给出。这个海森矩阵可以分解为先验精度和 FIM 之和。因此，许多贝叶斯设计问题被近似为操作 FIM 的问题。这催生了一系列经典的、以字母命名的最优性准则：

*   **D-最优性 (D-optimality)**：最大化 $\det(\mathbf{F})$，等价于最小化参数估计渐近置信椭球的体积。
*   **A-最优性 (A-optimality)**：最小化 $\text{tr}(\mathbf{F}^{-1})$，等价于最小化参数估计的平均方差。
*   **E-最优性 (E-optimality)**：最大化 $\mathbf{F}$ 的最小特征值 $\lambda_{\min}(\mathbf{F})$，旨在改善最难估计的参数组合的方差。

另一个将 FIM 与贝叶斯设计联系起来的工具是**贝叶斯克拉默-拉奥下界 (Bayesian Cramér-Rao Bound, BCRB)**，也称为范特里斯不等式 (Van Trees inequality)。它为任何估计量的贝叶斯均方误差提供了一个下界：
$$
\mathbb{E}[(\hat{\boldsymbol{\theta}} - \boldsymbol{\theta})(\hat{\boldsymbol{\theta}} - \boldsymbol{\theta})^{\top}] \ge (\mathbb{E}_{\boldsymbol{\theta}}[\mathbf{F}(\boldsymbol{\theta})] + \mathbf{J}_{\text{pr}})^{-1}
$$
其中 $\mathbb{E}_{\boldsymbol{\theta}}[\mathbf{F}(\boldsymbol{\theta})]$ 是在先验分布上平均的 FIM，$\mathbf{J}_{\text{pr}}$ 是先验分布本身提供的信息。一个合理的设计目标是选择一个设计来最小化这个误差下界，这等价于最大化总信息 $\mathbb{E}_{\boldsymbol{\theta}}[\mathbf{F}(\boldsymbol{\theta})] + \mathbf{J}_{\text{pr}}$。由于先验信息 $\mathbf{J}_{\text{pr}}$ 与设计无关，这通常简化为最大化**期望费雪信息 (Expected Fisher Information, EFI)** $\mathbb{E}_{\boldsymbol{\theta}}[\mathbf{F}(\boldsymbol{\theta})]$。[@problem_id:3367082]

例如，考虑一个依赖于设计变量 $u$ 的模型，其 FIM 中的关键部分是信息比率 $\Phi(u) = h(u)^2 / v(u)$，其中 $h(u)$ 与信号强度有关，$v(u)$ 是噪声方差。通过求解 $\frac{d\Phi(u)}{du} = 0$，我们可以找到使期望信息最大化的最优设计 $u^\star$。[@problem_id:3367082]

### 非线性与约束问题中的挑战

虽然基于 FIM 的近似方法功能强大，但在面对强非线性或参数约束时，它们可能会失效。理解这些局限性对于高级应用至关重要。

#### 非线性效应：混叠与多峰性

当模型是高度非线性时，后验分布可能不再是单峰的，或者其形状与高斯分布相去甚远。基于局部曲率（如 FIM）的准则可能无法捕捉到这些全局特性。

考虑一个非线性模型 $y = \sin(\theta d) + \varepsilon$ [@problem_id:3367103]。
*   **观测费雪信息 (Observed Fisher Information, OFI)**：在某个名义参数 $\theta_0$ 处评估 FIM。这种方法非常脆弱。如果 $\theta_0$ 碰巧是前向模型对 $\theta$ 的一个驻点（例如，$\theta_0=0$ 且模型为 $f(\theta) = \theta^2 d$），那么 FIM 将为零，导致设计准则完全失效。[@problem_id:3367103]
*   **期望费雪信息 (Expected Fisher Information, EFI)**：通过在先验上对 FIM 进行平均，EFI 改善了 OFI 的局部性。然而，它仍然是一个“局部”测度在全局的平均，无法完全捕捉非单射性（多对一映射）的后果。在 $\sin(\theta d)$ 的例子中，随着 $d$ 的增大，多个不同的 $\theta$ 值可以产生非常相似的 $\sin(\theta d)$ 值。这种现象称为**混叠 (aliasing)**，会导致后验分布出现多个峰值（即**多峰性 (multimodality)**）。EFI 无法充分惩罚这种模糊性。
*   **完整的预期信息增益 (Full EIG)**：作为互信息，EIG 自然地、从第一性原理上就考虑了整个后验分布的形状。它能正确地量化混叠和多峰性导致的信息损失。因此，在强非线性模型中，由 EIG 指导的设计可能与由 EFI 指导的设计截然不同。

例如，对于一个二次模型 $y = \theta^2 + d\theta + \varepsilon$ [@problem_id:3367117]，即使只有一个参数 $\theta$，由于 $\theta$ 和 $-\theta-d$ 可能产生相同的 $y$ 值，后验分布很容易出现双峰。一个简单的、基于 EFI 的 D-最优性分数可能显示某个设计很好，但实际上该设计产生的后验是双峰的，使得参数估计非常模糊。只有完整的后验分析或基于 EIG 的设计才能揭示这一问题。

#### 参数约束的影响

在许多实际问题中，参数受到物理约束，例如浓度或扩散系数必须为正。这些不等式约束会深刻地改变后验的几何形状，并对设计准则产生微妙的影响 [@problem_id:3367025]。

*   **后验几何的改变**：约束将后验分布限制在一个子空间内。如果无约束的后验模式位于禁止区域，那么有约束的后验模式将被“推”到可行域的边界上。

*   **近似的失效**：标准的拉普拉斯近似假定后验是无约束的高斯分布，这在模式位于边界时显然是错误的。更糟糕的是，如果前向模型在边界处存在奇异性（例如，模型中包含 $\sqrt{\theta_1}$ 项，其导数在 $\theta_1=0$ 处发散），FIM 也会在该点发散。依赖于 FIM 的准则（如 D-最优性）可能会产生病态行为，即错误地偏爱那些将后验模式推向奇异边界的设计。[@problem_id:3367025]

*   **约束即信息**：约束本身就是一种信息来源。知道一个参数 $\theta_1 \ge 0$ 会“削尖”后验分布，减少其方差。E-最优性准则对这种效应特别敏感。它旨在改善最不确定的方向，因此可能会选择一个设计，该设计不一定为该参数提供最多的数据信息，但能有效地利用边界约束来“正则化”该参数的估计，从而提高最差情况下的推断精度。[@problem_id:3367025]

*   **参数变换**：处理正约束的一个常用方法是进行对数变换，例如令 $\phi_1 = \ln \theta_1$。这样，$\phi_1$ 就在整个实数轴上无约束。虽然这种方法在建模中很有用，但必须注意，非线性变换通常不会保持所有最优性准则。例如，A-最优性和 E-最优性在这样的变换下不是不变的，因此在不同参数化下进行优化可能会得到不同的最优设计。[@problem_id:3367025]

### 高级设计策略

最后，我们简要介绍两种超越静态、一次性设计的高级策略。

#### 序列与自适应设计

在许多情况下，我们不是一次性完成所有实验，而是可以分阶段进行。**序列设计 (sequential design)** 的思想是利用早期实验获得的信息来指导后续实验的设计。如果设计选择明确地依赖于之前观测到的数据，则称之为**自适应设计 (adaptive design)**。

其理论基础是互信息的链式法则。对于一个两阶段实验，总信息增益为：
$$
I(\boldsymbol{\theta}; y_1, y_2) = I(\boldsymbol{\theta}; y_1) + I(\boldsymbol{\theta}; y_2 | y_1)
$$
为了最大化总信息增益，我们不仅要考虑第一阶段本身的信息增益 $I(\boldsymbol{\theta}; y_1)$，还要最大化第二阶段的期望信息增益 $\mathbb{E}_{y_1}[I(\boldsymbol{\theta}; y_2 | y_1)]$。这意味着在第二阶段，我们需要根据第一阶段的观测数据 $y_1$ 来选择最优的设计 $h_2(y_1)$。[@problem_id:3367084]

这个过程可以向前迭代。在每个阶段 $k$，我们选择一个设计 $d_k$，它最大化当前阶段的期望信息增益，该期望是基于到阶段 $k-1$ 为止所有观测数据所形成的后验分布来计算的。这种“向前看”的策略是动态规划思想在实验设计中的体现。

#### 基于梯度的设计优化

当设计空间是连续的（例如，在空间中放置传感器的位置 $x_s$），我们可以使用数值优化算法（如梯度上升）来寻找最优设计。这需要计算效用函数相对于设计变量的梯度。

在复杂的、由偏微分方程（PDE）控制的逆问题中，计算这个梯度可能非常困难，因为它涉及到前向模型解对设计参数的敏感度。直接通过有限差分来近似梯度在计算上可能非常昂贵。

**伴随方法 (Adjoint Method)** 提供了一种极其高效的计算梯度的方式。通过求解一个与原（前向）问题相关的“伴随”方程，我们可以用一次额外的 PDE 求解的代价，计算出效用函数对所有设计变量的梯度。[@problem_id:3367075] 这种方法是大规模优化和设计问题的基石。例如，在确定扩散过程中传感器的最佳位置时，我们可以首先用伴随方法推导出效用函数（如 EIG）关于传感器位置 $x_s$ 的梯度 $\frac{dU}{dx_s}$ 的解析表达式，然后将其代入梯度上升算法中，迭代地更新传感器位置，直至收敛到局部最优解。