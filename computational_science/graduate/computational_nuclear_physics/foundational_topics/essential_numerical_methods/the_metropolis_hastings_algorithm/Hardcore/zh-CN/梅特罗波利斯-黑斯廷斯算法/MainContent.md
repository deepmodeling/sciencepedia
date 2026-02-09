## 引言
在现代计算科学和统计推断领域，从复杂概率分布中进行有效采样是一项核心挑战。尤其是在贝叶斯分析中，后验分布往往是高维、多模态且没有解析形式的，这使得直接采样或积分变得不切实际。Metropolis-Hastings (MH) 算法，作为马尔可夫链蒙特卡洛（MCMC）方法的基石，为解决这一难题提供了强大而通用的框架。

本文旨在为读者提供一份关于MH算法的全面指南，从其深刻的理论基础到广泛的实际应用。通过本文的学习，你将不仅理解算法的运作方式，还将掌握如何将其应用于解决真实世界的研究问题。文章分为三个核心部分。在“原理与机制”一章中，我们将从第一性原理出发，推导MH算法的核心——接受概率，并探讨收敛性诊断、效率优化等关键实践考量。接着，“应用与跨学科连接”一章将展示MH算法及其变体如何在物理学、工程学、经济学等多个领域解决复杂的参数估计和模型选择问题。最后，“动手实践”部分将通过具体的编程练习，引导你亲手实现和应用这些先进的采样技术。

让我们从深入其核心机制开始，揭开Metropolis-Hastings算法的神秘面纱。

## 原理与机制

在本章中，我们将深入探讨Metropolis-Hastings (MH)算法的核心原理与基本机制。作为马尔可夫链蒙特卡洛（Markov Chain Monte Carlo, MCMC）方法的基石，MH算法为从复杂高维概率分布中进行采样提供了一个强大而灵活的框架。我们将从构建算法所依据的第一性原理——细致平衡条件——出发，系统地推导出其接受概率的普适形式。随后，我们将讨论算法在实际应用中的关键考虑因素，包括数值稳定性、收敛性诊断和效率优化。最后，我们将探索几种先进的MH变体，它们扩展了算法的应用范围，能够处理梯度信息、应对多模态分布的挑战，甚至在不同维度的模型空间之间进行跳转。

### 核心原理：细致平衡与Metropolis-Hastings接受率

MCMC方法的核心思想是构建一个马尔可夫链，使其状态的平稳分布恰好是我们希望采样的目标概率分布 $\pi(\boldsymbol{\theta})$。对于一个马尔可夫链，如果其从状态 $\boldsymbol{\theta}$ 转移到 $\boldsymbol{\theta}'$ 的转移核 $P(\boldsymbol{\theta}' \mid \boldsymbol{\theta})$ 满足**细致平衡条件 (detailed balance condition)**，那么 $\pi(\boldsymbol{\theta})$ 就是该链的平稳分布。该条件表述为：

$$\pi(\boldsymbol{\theta}) P(\boldsymbol{\theta}' \mid \boldsymbol{\theta}) = \pi(\boldsymbol{\theta}') P(\boldsymbol{\theta} \mid \boldsymbol{\theta}')$$

此方程的物理意义是，在平稳状态下，系统在任意两个状态 $\boldsymbol{\theta}$ 和 $\boldsymbol{\theta}'$ 之间沿任一方向转移的“概率流”是相等的。

Metropolis-Hastings算法巧妙地通过一个“提议-接受/拒绝”机制来构建满足细致平衡的转移核。对于不同于当前状态 $\boldsymbol{\theta}$ 的新状态 $\boldsymbol{\theta}'$，总转移概率 $P(\boldsymbol{\theta}' \mid \boldsymbol{\theta})$ 可以分解为两步：首先根据一个**提议分布 (proposal distribution)** $q(\boldsymbol{\theta}' \mid \boldsymbol{\theta})$ 提议一个候选状态 $\boldsymbol{\theta}'$，然后以一定的**接受概率 (acceptance probability)** $\alpha(\boldsymbol{\theta} \to \boldsymbol{\theta}')$ 接受这个提议。因此，转移概率可以写作 $P(\boldsymbol{\theta}' \mid \boldsymbol{\theta}) = q(\boldsymbol{\theta}' \mid \boldsymbol{\theta}) \alpha(\boldsymbol{\theta} \to \boldsymbol{\theta}')$。将此表达式代入细致平衡条件，我们得到：

$$\pi(\boldsymbol{\theta}) q(\boldsymbol{\theta}' \mid \boldsymbol{\theta}) \alpha(\boldsymbol{\theta} \to \boldsymbol{\theta}') = \pi(\boldsymbol{\theta}') q(\boldsymbol{\theta} \mid \boldsymbol{\theta}') \alpha(\boldsymbol{\theta}' \to \boldsymbol{\theta})$$

为了求解接受概率，我们可以整理上式：

$$\frac{\alpha(\boldsymbol{\theta} \to \boldsymbol{\theta}')}{\alpha(\boldsymbol{\theta}' \to \boldsymbol{\theta})} = \frac{\pi(\boldsymbol{\theta}')}{\pi(\boldsymbol{\theta})} \frac{q(\boldsymbol{\theta} \mid \boldsymbol{\theta}')}{q(\boldsymbol{\theta}' \mid \boldsymbol{\theta})}$$

Metropolis和Hastings提出的标准解法，既满足此关系又使接受率最大化，其形式如下：

$$\alpha(\boldsymbol{\theta} \to \boldsymbol{\theta}') = \min \left( 1, \frac{\pi(\boldsymbol{\theta}') q(\boldsymbol{\theta} \mid \boldsymbol{\theta}')}{\pi(\boldsymbol{\theta}) q(\boldsymbol{\theta}' \mid \boldsymbol{\theta})} \right)$$

这个表达式是Metropolis-Hastings算法的核心。它由三个关键部分组成：

1.  **目标分布比率 (target ratio)**: $\frac{\pi(\boldsymbol{\theta}')}{\pi(\boldsymbol{\theta})}$。该项确保了采样最终将倾向于访问目标分布中概率密度较高的区域。

2.  **提议分布比率 (proposal ratio)** 或 **Hastings修正项 (Hastings correction)**: $\frac{q(\boldsymbol{\theta} \mid \boldsymbol{\theta}')}{q(\boldsymbol{\theta}' \mid \boldsymbol{\theta})}$。该项用于修正提议分布的不对称性。如果从 $\boldsymbol{\theta}$ 提议 $\boldsymbol{\theta}'$ 比从 $\boldsymbol{\theta}'$ 提议 $\boldsymbol{\theta}$ 更容易，即 $q(\boldsymbol{\theta}' \mid \boldsymbol{\theta}) > q(\boldsymbol{\theta} \mid \boldsymbol{\theta}')$，那么这个修正项会相应地降低接受概率，以维持细致平衡。

3.  **雅可比行列式 (Jacobian determinant)**: 在更一般的情况下，如果状态转移涉及维度变化（我们将在后续的RJMCMC部分讨论），此处还会出现一个雅可比行列式项。

一个重要的特例是当提议分布为对称分布时，即 $q(\boldsymbol{\theta}' \mid \boldsymbol{\theta}) = q(\boldsymbol{\theta} \mid \boldsymbol{\theta}')$。此时Hastings修正项为1，接受概率简化为：

$$\alpha(\boldsymbol{\theta} \to \boldsymbol{\theta}') = \min \left( 1, \frac{\pi(\boldsymbol{\theta}')}{\pi(\boldsymbol{\theta})} \right)$$

这便是最初的**Metropolis算法**。然而，更普适的Metropolis-Hastings形式允许使用任意提议分布，极大地扩展了算法的灵活性。

在贝叶斯推断的典型应用中，目标分布 $\pi(\boldsymbol{\theta})$ 是参数 $\boldsymbol{\theta}$ 的后验分布 $p(\boldsymbol{\theta} \mid \mathcal{D})$。根据贝叶斯定理，$p(\boldsymbol{\theta} \mid \mathcal{D}) = \frac{p(\mathcal{D} \mid \boldsymbol{\theta}) p(\boldsymbol{\theta})}{p(\mathcal{D})}$，其中 $p(\mathcal{D} \mid \boldsymbol{\theta})$ 是似然函数，$p(\boldsymbol{\theta})$ 是先验分布，$p(\mathcal{D})$ 是证据或边缘似然。由于 $p(\mathcal{D})$ 是一个与 $\boldsymbol{\theta}$ 无关的归一化常数，它在目标分布比率中会被消去：

$$\frac{\pi(\boldsymbol{\theta}')}{\pi(\boldsymbol{\theta})} = \frac{p(\boldsymbol{\theta}' \mid \mathcal{D})}{p(\boldsymbol{\theta} \mid \mathcal{D})} = \frac{p(\mathcal{D} \mid \boldsymbol{\theta}')}{p(\mathcal{D} \mid \boldsymbol{\theta})} \frac{p(\boldsymbol{\theta}')}{p(\boldsymbol{\theta})}$$

因此，在贝叶斯框架下，完整的MH接受概率表达式为：

$$\alpha(\boldsymbol{\theta} \to \boldsymbol{\theta}') = \min \left( 1, \frac{p(\mathcal{D} \mid \boldsymbol{\theta}')}{p(\mathcal{D} \mid \boldsymbol{\theta})} \frac{p(\boldsymbol{\theta}')}{p(\boldsymbol{\theta})} \frac{q(\boldsymbol{\theta} \mid \boldsymbol{\theta}')}{q(\boldsymbol{\theta}' \mid \boldsymbol{\theta})} \right)$$

例如，在核物理中，我们可能需要使用球形光学模型来校准模型参数 $\boldsymbol{\theta} = (V, W, r_0)$，以拟合中子弹性散射的实验数据 $\mathcal{D}$。假设我们采用高斯似然和高斯先验，并使用一个非对称的提议分布，如带有固定漂移向量 $\boldsymbol{b}$ 的高斯提议 $q_{\mathrm{A}}(\boldsymbol{\theta}' \mid \boldsymbol{\theta}) = \mathcal{N}(\boldsymbol{\theta}'; \boldsymbol{\theta} + \boldsymbol{b}, \mathbf{\Sigma}_q)$。在这种情况下，接受概率必须包含似然比、先验比以及由非对称提议分布产生的非单位Hastings修正项 $q_{\mathrm{A}}(\boldsymbol{\theta} \mid \boldsymbol{\theta}') / q_{\mathrm{A}}(\boldsymbol{\theta}' \mid \boldsymbol{\theta})$。忽略任何一项都将导致算法无法收敛到正确的后验分布 [@problem_id:3604497]。

### 实践中的考量与诊断

理论上的正确性是MH算法的基石，但在实际应用中，确保其有效和高效地运行同样至关重要。这涉及数值稳定性、收敛性诊断和性能调优等多个方面。

#### 数值稳定性与参数变换

在计算接受率时，尤其是当目标分布的概率密度值可能跨越多个数量级时，直接计算概率值很容易导致浮点数的上溢或下溢。一个标准的做法是在**对数域 (log-domain)** 中进行所有计算。接受概率的比较 $u  \frac{\pi' q_{rev}}{\pi q_{fwd}}$ （其中 $u \sim \mathcal{U}(0,1)$）等价于 $\ln(u)  \ln(\pi') + \ln(q_{rev}) - \ln(\pi) - \ln(q_{fwd})$。这种方法将乘法和除法转换为加法和减法，从而极大地提升了数值稳定性 [@problem_id:3604531]。

此外，许多物理参数本身具有约束，例如必须为正的密度或散射截面。为了自然地处理这些约束，我们可以对参数进行**变换 (transformation)**。例如，对于一个必须为正的参数 $\sigma_0$，我们可以对它的对数 $\theta_0 = \ln(\sigma_0)$ 进行采样。这样，$\theta_0$ 可以在整个实数轴上取值，而其反变换 $\sigma_0 = \exp(\theta_0)$ 自动满足了正性约束。采样过程在无约束的变换空间中进行，使得高斯随机游走等标准提议分布更易于应用 [@problem_id:3604531]。

#### 收敛、混合与效率

MCMC算法的最终目标是生成来自平稳分布的样本。然而，从任意起始点出发的马尔可夫链需要一定的时间才能“忘记”其初始状态并收敛到平稳分布。

**预烧期 (Burn-in)**：马尔可夫链的**遍历性定理 (ergodic theorem)** 保证了，对于一个不可约且非周期的链，其状态分布将收敛到唯一的平稳分布，无论初始状态 $\boldsymbol{\theta}_0$ 如何。因此，我们通常会丢弃链初始阶段的一部分样本，这个阶段被称为**预烧期**。预烧期的目的是减少初始状态带来的偏差。需要强调的是，初始状态的选择并不会改变平稳分布本身，而只会影响达到平稳分布所需的时间 [@problem_id:3604493]。预烧期的长度并没有一个绝对的标准，通常需要通过观察链的轨迹图（trace plot）等诊断工具来主观判断。

**调优与接受率 (Tuning and Acceptance Rate)**：对于随机游走MH算法，提议分布的步长（或方差）是一个关键的调节参数。步长选择存在一个权衡：
*   如果步长太大，提议的移动会非常“大胆”，频繁地跳到目标概率很低的区域，导致绝大多数提议被拒绝，接受率接近0。链几乎不移动，混合（mixing）极差。
*   如果步长太小，提议的移动非常“保守”，几乎总是在当前状态附近，导致目标概率比接近1，接受率接近1。然而，链每次只移动一小步，像是在原地踏步，探索参数空间极其缓慢，导致样本间具有高度的自相关性。

最优的混合效率通常在适中的接受率下达到。理论研究和实践经验表明，对于高维问题，目标接受率通常在 $0.2$ 到 $0.4$ 之间（一个经典结果是，对于高斯目标，高维极限下的最优接受率为 $0.234$）。因此，如果观察到的接受率过高（例如 $0.85$）或过低（例如 $0.12$），都表明提议步长设置不当，需要调整以提高采样效率 [@problem_id:3604493] [@problem_id:3604538]。

**自相关与有效样本量 (Autocorrelation and Effective Sample Size)**：MCMC生成的样本序列通常是相关的，即一个样本与其紧邻的样本在数值上很接近。这种相关性可以通过**自相关函数 (autocorrelation function, ACF)** $c(\tau)$ 来量化。强自相关意味着链的混合速度慢。为了度量这种相关性的影响，我们定义**积分自相关时间 (integrated autocorrelation time, IAT)** $\tau_{\text{int}}$：

$$\tau_{\text{int}} = 1 + 2 \sum_{\tau=1}^{\infty} c(\tau)$$

$\tau_{\text{int}}$ 的直观意义是，需要多少个相关样本才能获得一个等效的独立样本。如果一个后预烧期的链有 $M$ 个样本，其**有效样本量 (effective sample size, ESS)** $N_{\text{eff}}$ 由下式给出：

$$N_{\text{eff}} = \frac{M}{\tau_{\text{int}}}$$

例如，如果一个长度为 $45,000$ 的样本链，其自相关函数近似为 $c(\tau) \approx 0.95^\tau$，那么其积分自相关时间 $\tau_{\text{int}} \approx 39$。这意味着有效样本量仅为 $45,000 / 39 \approx 1,154$，远小于名义上的样本数。计算ESS对于准确评估后验估计的不确定性至关重要 [@problem_id:3604493] [@problem_id:3604538]。

#### 收敛诊断与模型验证

如何判断链是否已经收敛？除了观察轨迹图，一个广泛使用的方法是运行多条从不同、分散的初始点开始的独立马尔可夫链。**Gelman-Rubin诊断**（或称为**潜在尺度缩减因子, potential scale reduction factor** $\hat{R}$）通过比较链间方差与链内方差来评估收敛性。如果所有链都收敛到同一个平稳分布，那么链间方差应该与链内方差相当，$\hat{R}$ 值会趋近于1。通常，$\hat{R}  1.1$ 被认为是收敛的合理证据 [@problem_id:3604538]。

最后，MCMC分析不仅关乎参数估计，也提供了验证模型本身的工具。**后验预测检验 (posterior predictive check)** 是一种有效的方法。我们利用从后验分布中抽取的参数样本来生成“复制”数据集，然后将这些复制数据集的统计特性与观测到的真实数据进行比较。如果模型能很好地再现观测数据，这会增加我们对模型假设的信心 [@problem_id:3604538]。

### 先进的Metropolis-Hastings变体

标准随机游走MH算法的简单性和普适性是其优点，但在处理复杂问题时，其效率可能不足。为此，研究人员开发了多种先进的变体，以提高混合效率或扩展其应用领域。

#### 基于梯度的提议：Metropolis调整的朗之万算法 (MALA)

随机游走是“盲目”的，因为它不使用任何关于目标分布景观的信息。**Metropolis调整的朗之万算法 (Metropolis-Adjusted Langevin Algorithm, MALA)** 通过利用目标分布的**梯度信息** $\nabla \ln \pi(\boldsymbol{\theta})$ 来构建更智能的提议。其提议步骤是对过阻尼朗之万随机微分方程（SDE）的欧拉-丸山离散化：

$$\boldsymbol{\theta}' = \boldsymbol{\theta} + \frac{h}{2} \nabla \ln \pi(\boldsymbol{\theta}) + \sqrt{h} \boldsymbol{\xi}$$

其中 $h$ 是步长，$\boldsymbol{\xi} \sim \mathcal{N}(0, \mathbf{I})$ 是高斯噪声。这个提议会“漂移”向目标概率密度增加的方向，因此更有可能被接受。然而，由于离散化误差和梯度计算中可能存在的噪声，仅使用这个更新步骤（即“未调整的”朗之万算法）通常不会精确地以 $\pi(\boldsymbol{\theta})$ 为其平稳分布，会导致系统性偏差 [@problem_id:3604520]。

MALA的精髓在于，它将这个基于梯度的提议嵌入到Metropolis-Hastings框架中。由于该提议分布是非对称的，我们必须计算相应的Hastings修正项并应用标准的MH接受步骤。这个接受/拒绝步骤精确地纠正了离散化带来的偏差，确保最终的马尔可夫链严格收敛到目标分布 $\pi(\boldsymbol{\theta})$。当处理带有边界约束（如参数非负性）的问题时，MALA可以与反射边界条件结合。这种情况下，提议机制变得更加复杂，可能需要使用投影梯度，并且其提议密度会演变成一个折叠高斯分布，以精确地满足细致平衡条件 [@problem_id:3604515]。

#### 用于增强混合的非可逆采样器

细致平衡是确保正确平稳分布的一个*充分*但*非必要*条件。放弃细致平衡，构建**非可逆 (non-reversible)** 马尔可夫链，有时可以显著改善采样器的混合性能，尤其是在面对多模态分布时。

一个典型的例子是**提升的 (lifted)** MH采样器。该方法通过引入一个辅助的“动量”或“速度”变量（例如，$v \in \{-1, +1\}$）来扩充状态空间。采样器根据当前速度 $v_t$ 的方向进行确定性的提议移动 $\boldsymbol{\theta}' = \boldsymbol{\theta}_t + v_t \boldsymbol{\delta}$。然后根据标准的Metropolis准则决定是否接受。关键的区别在于拒绝时的操作：如果提议被拒绝，参数位置保持不变，但速度变量被翻转 $v_{t+1} = -v_t$。

这种“拒绝-翻转”机制打破了细致平衡，因为从 $(\boldsymbol{\theta}, v)$ 到 $(\boldsymbol{\theta}, -v)$ 的转移只在拒绝时发生，而反向转移则不然。这种非可逆的动力学行为使得采样器能够保持一个方向上的持续运动，从而更有力地穿越不同模态之间的低概率区域。这在处理例如由相等的核势能参数化导致的多模态后验分布时尤其有效，能够显著提高模态间的切换率 [@problem_id:3604494]。

#### 通过增广状态空间处理约束

MH框架的灵活性还体现在它能够通过**增广状态空间 (augmented state space)** 的方法来处理复杂的参数约束。例如，在核物质理论中，我们可能希望强制能量-密度关系 $E(\boldsymbol{\theta})/A$ 精确等于某个经验值 $E_0$。一种方法是引入一个拉格朗日乘子 $\lambda$，并将它作为模型的一个额外参数。然后，我们将目标分布修改为增广后验：

$$\pi(\boldsymbol{\theta}, \lambda) \propto p(\mathcal{D} \mid \boldsymbol{\theta}) p(\boldsymbol{\theta}) p(\lambda) \exp\left[-\lambda\left(\frac{E(\boldsymbol{\theta})}{A} - E_0\right)\right]$$

通过在这个增广空间 $(\boldsymbol{\theta}, \lambda)$ 上运行MCMC，算法会自动调整 $\lambda$ 的值，以使采样出的 $\boldsymbol{\theta}$ 倾向于满足约束条件。当为正的拉格朗日乘子 $\lambda$ 设计提议分布时（例如，在对数空间中进行随机游走），必须小心地在Hastings修正项中包含相应的雅可比行列式因子，以确保细致平衡 [@problem_id:3604490]。

### 跨维度MCMC：可逆跳转Metropolis-Hastings (RJMCMC)

在许多科学问题中，我们不仅关心单个模型内的参数值，还希望比较具有不同结构和不同参数数量的多个模型。例如，在核力研究中，我们可能想比较一个仅包含两体力（2N）的模型 $M_1$ 与一个同时包含两体和三体力（2N+3N）的模型 $M_2$。由于 $M_1$ 和 $M_2$ 的参数空间维度不同，标准的MH算法无法在它们之间进行跳转。

**可逆跳转Metropolis-Hastings (Reversible Jump Metropolis-Hastings, RJMCMC)** 算法通过允许马尔可夫链在不同维度的空间之间移动，解决了这个问题。它将模型本身视为一个离散的随机变量，在联合分布 $p(\text{模型}, \text{参数} \mid \mathcal{D})$上进行采样。

RJMCMC的核心思想是设计跨维度的“**生 (birth)**”和“**死 (death)**”移动。一个“生”移动会提议从一个低维模型（如$M_1$）跳转到一个高维模型（如$M_2$），同时增加参数的数量。一个“死”移动则执行相反的操作。

为了维持细致平衡，跨维度提议必须精心设计。以从模型 $M_1$（参数 $\boldsymbol{\theta}_1$，维度 $d_1$）到模型 $M_2$（参数 $\boldsymbol{\theta}_2$，维度 $d_2 > d_1$）的“生”移动为例：

1.  **维度匹配 (Dimension Matching)**：我们必须从一个辅助变量分布 $q_{aux}(u)$ 中抽取一个随机向量 $\boldsymbol{u}$，其维度为 $d_2 - d_1$。
2.  **确定性映射 (Deterministic Mapping)**：然后，通过一个可逆的确定性函数 $\boldsymbol{\theta}_2 = g(\boldsymbol{\theta}_1, \boldsymbol{u})$ 来构造高维参数。这个映射必须是双射，以确保逆向的“死”移动可以唯一地从 $\boldsymbol{\theta}_2$ 恢复出 $(\boldsymbol{\theta}_1, \boldsymbol{u})$。

有了这个构造，从 $(\boldsymbol{\theta}_1, \boldsymbol{u})$ 到 $\boldsymbol{\theta}_2$ 的变换就成了一个维度匹配的双射。RJMCMC的接受概率此时扩展为：

$$\alpha(\text{birth}) = \min \left( 1, \frac{p(M_2, \boldsymbol{\theta}_2 \mid \mathcal{D})}{p(M_1, \boldsymbol{\theta}_1 \mid \mathcal{D})} \frac{r_{21} q_{21}(\cdot \mid \boldsymbol{\theta}_2)}{r_{12} q_{12}(\boldsymbol{u} \mid \boldsymbol{\theta}_1)} |\mathbf{J}| \right)$$

这个表达式中的关键组成部分包括：

*   **后验比率**: $\frac{p(M_2, \boldsymbol{\theta}_2 \mid \mathcal{D})}{p(M_1, \boldsymbol{\theta}_1 \mid \mathcal{D})}$。它不仅包括似然比和参数先验比，还包括**模型先验比** $\frac{p(M_2)}{p(M_1)}$。
*   **提议比率**: $\frac{r_{21} q_{21}(\cdot \mid \boldsymbol{\theta}_2)}{r_{12} q_{12}(\boldsymbol{u} \mid \boldsymbol{\theta}_1)}$。其中 $r_{12}$ 和 $r_{21}$ 是选择“生”移动和“死”移动的概率，$q_{12}$ 是提议辅助变量 $\boldsymbol{u}$ 的密度。逆向“死”移动可能是确定性的，此时其提议密度为1。
*   **雅可比行列式**: $|\mathbf{J}| = \left| \frac{\partial \boldsymbol{\theta}_2}{\partial (\boldsymbol{\theta}_1, \boldsymbol{u})} \right|$。这是维度匹配映射 $g$ 的雅可比行列式的绝对值，它解释了由于变量变换引起的体积变化。

例如，在比较2N力模型 $M_1$（参数 $\boldsymbol{\theta}_1=(C_S, C_T)$）和2N+3N力模型 $M_2$（参数 $\boldsymbol{\theta}_2=(C_S, C_T, c_E)$）时，一个“生”移动可以通过从某个分布 $q_{12}(u)$ 中抽取一个值 $u$ 并设定 $c_E = u$ 来实现。计算接受概率时，必须精确地包含似然比、参数先验（特别是对新参数 $c_E$ 的先验）、模型先验比、辅助变量的提议密度以及雅可比行列式（在此例中通常为1）[@problem_id:3604527]。

RJMCMC的原理同样适用于更复杂的离散结构，例如对核子进行聚类划分。在这种情况下，分裂（生）和合并（死）移动会改变聚类的数量，从而改变参数空间的维度。提议概率必须仔细地计入所有离散选择的组合因子，例如选择哪个聚类进行分裂，或选择哪一对聚类进行合并，以确保细致平衡得以满足 [@problem_id:3604483]。