## 引言
[机器学习势函数](@entry_id:138428)（MLPs）正以前所未有的精度和效率革新原子尺度的[材料模拟](@entry_id:176516)。然而，这些强大的模型在提供精确预测的同时，往往如同一个“黑箱”，未能告知我们其预测的可信度。当模拟探索到未知构型空间时，这种缺乏自我意识的预测可能导致灾难性的失败。因此，如何为MLPs的预测提供严谨的、量化的[置信度](@entry_id:267904)，即不确定性量化（Uncertainty Quantification, UQ），已成为将这些模型从学术研究推向可靠工程应用的关键瓶颈。

本文旨在系统性地解决这一挑战。通过学习本文，您将能够：首先，在“原理与机制”章节中，深入剖析不确定性的两大来源——认知不确定性和[偶然不确定性](@entry_id:154011)，并掌握实现量化的核心数学框架，如贝叶斯方法与[集成学习](@entry_id:637726)。接着，在“应用与[交叉](@entry_id:147634)学科联系”章节中，见证UQ如何在[主动学习](@entry_id:157812)、增强模拟可靠性、预测宏观材料属性等方面发挥关键作用。最后，“动手实践”部分将通过具体的编程问题，让您亲身体验UQ在解决实际问题中的威力。

通过这一系列的学习，本文将引导您构建起一套完整的知识体系，从而能够安全、有效地在您的研究中部署和利用带有不确定性量化的[机器学习势函数](@entry_id:138428)。

## 原理与机制

在[机器学习势函数](@entry_id:138428)（Machine-Learned Potentials, MLPs）领域，仅仅预测能量和力是不够的。为了在[原子模拟](@entry_id:199973)中可靠地部署这些模型，我们必须量化其预测的不确定性。这种[不确定性量化](@entry_id:138597)（Uncertainty Quantification, UQ）对于指导[主动学习](@entry_id:157812)、识别模型可能失效的构型、以及将[误差传播](@entry_id:147381)到宏观材料属性的预测中至关重要。本章深入探讨了为MLPs量化不确定性的基本原理和核心机制，为理解和应用这些技术提供了坚实的理论基础。

### 不确定性的基本概念

在[统计学习](@entry_id:269475)的框架下，模型预测的不确定性并非单一概念，而是源于两个截然不同的方面：**[认知不确定性](@entry_id:149866)（epistemic uncertainty）** 和 **偶然不确定性（aleatoric uncertainty）**。理解这两者的区别是有效进行UQ的第一步。

**认知不确定性**，又称[模型不确定性](@entry_id:265539)，源于我们对“正确”模型知识的缺乏。在MLPs的背景下，这通常是由于训练数据集有限，未能充分覆盖广阔的原子构型空间。当模型遇到远离其训练数据[分布](@entry_id:182848)的构型时（即“外推”），其预测的不确定性会显著增加。此外，如果模型本身的架构或表达能力不足以描述真实的物理规律（即模型设定不当），也会产生认知不确定性。原则上，[认知不确定性](@entry_id:149866)是**可约减的**：通过在信息稀疏的区域收集更多数据，或通过改进模型架构，我们可以让模型“学得更好”，从而降低这种不确定性。

**[偶然不确定性](@entry_id:154011)**，又称数据不确定性，反映了数据生成过程中固有的、随机的噪声或变异性。对于MLPs，训练数据通常来自密度泛函理论（Density Functional Theory, DFT）等[第一性原理计算](@entry_id:198754)。这些计算本身就存在数值误差，例如，由有限的$k$点网格、[自洽场](@entry_id:136549)（SCF）收敛的随机性、金属体系中电子的涂抹（smearing）选择或数值容差引起。这些因素导致即使对于完全相同的原子构型，每次DFT计算的能量和力标签也可能存在微小差异。这种不确定性被认为是数据内在的，因此，即使使用无限多的、在相同计算协议下生成的数据进行训练，它也**无法被消除**。此外，[偶然不确定性](@entry_id:154011)可能是**异[方差](@entry_id:200758)的（heteroscedastic）**，意味着其大小取决于原子构型本身，例如，某些复杂构型的DFT计算可能比简单构型的数值噪声更大 [@problem_id:3500243]。

在[贝叶斯建模](@entry_id:178666)框架下，这两种不确定性可以通过**[全方差定律](@entry_id:184705)（law of total variance）** 进行严格的数学分解。对于给定构型 $\mathbf{R}$ 和训练数据 $\mathcal{D}$，能量 $E$ 的总预测[方差](@entry_id:200758)可以分解为：
$$
\operatorname{Var}(E \mid \mathbf{R}, \mathcal{D}) = \mathbb{E}_{\boldsymbol{\theta} \mid \mathcal{D}}\! \left[ \operatorname{Var}(E \mid \mathbf{R}, \boldsymbol{\theta}) \right] + \operatorname{Var}_{\boldsymbol{\theta} \mid \mathcal{D}}\! \left( \mathbb{E}[E \mid \mathbf{R}, \boldsymbol{\theta}] \right)
$$
其中 $\boldsymbol{\theta}$ 是模型参数。

*   **第一项**，$\mathbb{E}_{\boldsymbol{\theta} \mid \mathcal{D}}\! \left[ \operatorname{Var}(E \mid \mathbf{R}, \boldsymbol{\theta}) \right]$，代表**[偶然不确定性](@entry_id:154011)**。它是在模型参数后验分布上，对数据噪声[方差](@entry_id:200758)的期望。$\operatorname{Var}(E \mid \mathbf{R}, \boldsymbol{\theta})$ 是由似然函数定义的、给定一组特定参数时预测的噪声[方差](@entry_id:200758)。
*   **第二项**，$\operatorname{Var}_{\boldsymbol{\theta} \mid \mathcal{D}}\! \left( \mathbb{E}[E \mid \mathbf{R}, \boldsymbol{\theta}] \right)$，代表**[认知不确定性](@entry_id:149866)**。$\mathbb{E}[E \mid \mathbf{R}, \boldsymbol{\theta}]$ 是由一组特定参数 $\boldsymbol{\theta}$ 给出的模型点预测。该项计算的是模型点预测值在参数后验分布上的[方差](@entry_id:200758)，反映了我们对“最佳”参数 $\boldsymbol{\theta}$ 的不确定性。当数据增多时，[后验分布](@entry_id:145605) $p(\boldsymbol{\theta} \mid \mathcal{D})$ 会变窄，从而使这一项减小 [@problem_id:3500243]。

在[材料科学](@entry_id:152226)应用中，这两种不确定性的尺度行为也不同。例如，由于$k$点采样不足导致的DFT总能量误差会随体系尺寸增大而累积，这意味着总能量的**偶然不确定性**可能与原子数成比例。然而，如果模型设计保证了**[广延性](@entry_id:144932)（extensivity）**（即总能量是局部原子环境贡献之和），并且训练数据充分覆盖了这些局部环境，那么单个原子能量的**[认知不确定性](@entry_id:149866)**则不必随体系尺寸增长 [@problem_id:3500243]。

### 不确定性量化的贝叶斯方法

贝叶斯方法为[量化不确定性](@entry_id:272064)提供了一个统一的概率框架。其核心思想不是寻找单一的最佳模型参数，而是推断出在给定数据下模型参数的整个[后验分布](@entry_id:145605)。预测时，通过对这个后验分布进行积分或采样，我们自然地得到了包含不确定性信息的[预测分布](@entry_id:165741)。

#### [高斯过程](@entry_id:182192)势

**高斯过程（Gaussian Process, GP）** 是一种非参数贝叶斯方法，它不直接定义参数化的函数形式，而是在[函数空间](@entry_id:143478)上定义一个先验分布。一个GP由一个[均值函数](@entry_id:264860)和一个[协方差函数](@entry_id:265031)（或称**[核函数](@entry_id:145324)** $k(\mathbf{R}, \mathbf{R}')$）完全确定。核函数定义了在不同构型 $\mathbf{R}$ 和 $\mathbf{R}'$ 处的函数值之间的关联性，从而编码了关于函数（在此即[势能面](@entry_id:147441)）的先验信念，如光滑度等。

对于原子势，一个常见的建模策略是将总能量视为各个原子局部环境贡献之和。我们可以为每个原子的能量贡献 $f(a)$ 定义一个GP先验，其中 $a$ 代表一个局部原子环境。例如，我们可以使用基于原子位置光滑重叠（Smooth Overlap of Atomic Positions, SOAP）描述符 $\mathbf{s}(a)$ 的[核函数](@entry_id:145324) [@problem_id:3500242]：
$$
k(a, a') = \sigma_{f}^{2} \left( \frac{ \mathbf{s}(a) \cdot \mathbf{s}(a') }{ \|\mathbf{s}(a)\| \, \|\mathbf{s}(a')\| } \right)^{\zeta}
$$
其中 $\sigma_{f}^{2}$ 是信号[方差](@entry_id:200758)，$\zeta$ 控制[非线性](@entry_id:637147)程度。

由于GP在求和等线性运算下是封闭的，一个包含 $N(S)$ 个原子的结构 $S$ 的总能量 $E(S) = \sum_{i=1}^{N(S)} f(a_i)$ 同样是一个GP。两个不同结构 $S$ 和 $S'$ 的总能量之间的协[方差](@entry_id:200758)可以通过对所有原子对的[核函数](@entry_id:145324)求和得到 [@problem_id:3500242]：
$$
\operatorname{Cov}(E(S), E(S')) = \sum_{i=1}^{N(S)} \sum_{j=1}^{N(S')} k(a_i, a'_j) = \sigma_{f}^{2} \sum_{i=1}^{N(S)} \sum_{j=1}^{N(S')} \left( \hat{\mathbf{s}}(a_{i}) \cdot \hat{\mathbf{s}}(a'_{j}) \right)^{\zeta}
$$
其中 $\hat{\mathbf{s}}(a)$ 是归一化的[SOAP描述符](@entry_id:189760)。

在MLPs中，利用力数据进行训练至关重要，因为力是[势能面](@entry_id:147441)的梯度，提供了更丰富的局部信息。GP框架可以优雅地整合**导数观测值**。由于求导是线性算子，如果能量 $E(\mathbf{R})$ 是一个GP，那么力 $\mathbf{F}(\mathbf{R}) = -\nabla_{\mathbf{R}} E(\mathbf{R})$ 也是一个GP。能量和力之间的联合分布仍然是高斯的，其协[方差](@entry_id:200758)结构完全由能量核函数 $k(\mathbf{R}, \mathbf{R}')$ 及其导数决定 [@problem_id:3500223]。例如，在一维情况下，能量-力协[方差](@entry_id:200758)和力-力协[方差](@entry_id:200758)分别为：
$$
k_{E,F}(x, x') = \operatorname{Cov}(E(x), F(x')) = -\frac{\partial k(x, x')}{\partial x'}
$$
$$
k_{F,F}(x, x') = \operatorname{Cov}(F(x), F(x')) = \frac{\partial^2 k(x, x')}{\partial x \partial x'}
$$
这一性质使得我们可以构建一个包含能量-能量、能量-力、力-力块的巨大协方差矩阵，从而在能量和力数据上联合训练GP模型。

GP模型的一个深刻特性是，对函数值的观测和对其导数值的观测提供的信息是不同的。考虑这样一种情况：我们在构型 $\mathbf{R}^*$ 处进行了一次**无噪声**的能量观测。这会使该点的能量预测[方差](@entry_id:200758)降为零。然而，这并不意味着该点力的预测[方差](@entry_id:200758)也为零。一般而言，知道一个函数在某一点的值并不足以完全确定该点的梯度。除非核函数具有特殊的、导致能量和力之间存在确定性[线性关系](@entry_id:267880)的病态形式，否则力的预测[方差](@entry_id:200758)将保持为正值。这说明，即使能量在一个点上是确定的，我们对其在该点的局部斜率（即力）仍然可以存在不确定性 [@problem_id:3500252]。

#### [贝叶斯神经网络](@entry_id:746725)及其近似

**[贝叶斯神经网络](@entry_id:746725)（Bayesian Neural Networks, BNNs）** 将贝叶斯思想应用于[神经网](@entry_id:276355)络，通过在网络权重 $\mathbf{w}$ 上放置先验分布（如[高斯先验](@entry_id:749752) $p(\mathbf{w}) = \mathcal{N}(\mathbf{0}, \alpha^{-1} \mathbf{I})$）来捕捉[认知不确定性](@entry_id:149866)。然而，权重的精确[后验分布](@entry_id:145605) $p(\mathbf{w} \mid \mathcal{D})$ 通常是无法解析计算的。因此，需要采用[近似推断](@entry_id:746496)方法。

**[变分推断](@entry_id:634275)（Variational Inference, VI）** 是一种主流的近似方法。VI的目标是寻找一个简单的、可[参数化](@entry_id:272587)的[概率分布](@entry_id:146404) $q(\mathbf{w})$（例如，所有权重独立的均场[高斯分布](@entry_id:154414)），使其尽可能地接近真实的后验分布。这种“接近”是通过最小化两者之间的**Kullback–Leibler (KL) 散度** $\mathrm{KL}(q(\mathbf{w}) \,\|\, p(\mathbf{w} \mid \mathcal{D}))$ 来实现的。在实践中，这等价于最大化一个称为“[证据下界](@entry_id:634110)”（Evidence Lower Bound, ELBO）的[目标函数](@entry_id:267263)。ELBO由两部分组成：一部分是期望[对数似然](@entry_id:273783)，衡量模型对数据的拟合程度；另一部分是负的KL散度项 $\mathrm{KL}(q(\mathbf{w}) \,\|\, p(\mathbf{w}))$，作为对先验的正则化项，惩罚变分后验与先验的偏离 [@problem_id:3500173]。

由于训练完整的BNN成本高昂，研究者开发了更实用、可扩展的近似方法，它们能够在标准[神经网](@entry_id:276355)络的训练和预测框架内有效地估计[认知不确定性](@entry_id:149866)。

**1. [集成方法](@entry_id:635588)（Ensemble Methods）**
这是最直接且非常有效的方法之一。其核心思想是独立训练多个（例如 $M$ 个）[神经网](@entry_id:276355)络，构成一个**委员会（committee）**。每个网络的独立性可以通过不同的随机[权重初始化](@entry_id:636952)、不同的数据抽样（例如，对训练集进行[自助法](@entry_id:139281)（bootstrap）重采样）等方式来保证。在预测时，对于一个给定的输入构型 $x$，委员会中的每个网络 $m$ 都会给出一个预测值 $y_m(x)$。这些预测值的[分布](@entry_id:182848)被用来估计认知不确定性。

假设这 $M$ 个预测值 $\{y_m(x)\}_{m=1}^M$ 是来自某个潜在[分布](@entry_id:182848)的独立同分布样本，那么：
*   **预测均值** $\bar{y}(x)$ 由样本均值给出：
    $$
    \bar{y}(x) = \frac{1}{M} \sum_{m=1}^{M} y_{m}(x)
    $$
*   **预测[方差](@entry_id:200758)**（[认知不确定性](@entry_id:149866)）由无偏样本[方差](@entry_id:200758)给出：
    $$
    s^{2}(x) = \frac{1}{M-1} \sum_{m=1}^{M} \left( y_{m}(x) - \bar{y}(x) \right)^{2}
    $$
这个过程同样适用于能量和力。由于力是能量的导数，而求导是确定性操作，因此独立训练的能量函数 $\{E_m(x)\}$ 会产生一组独立的力函数 $\{ \mathbf{F}_m(x) = -\nabla E_m(x) \}$。所以，上述统计公式[对力](@entry_id:159909)的分量同样适用 [@problem_id:3500187]。

**2. [蒙特卡洛](@entry_id:144354) Dropout（MC Dropout）**
Dropout 是一种在[神经网](@entry_id:276355)络训练中广泛使用的[正则化技术](@entry_id:261393)。一个惊人的理论发现表明，在测试时继续使用 Dropout，等价于在某个特定的 BNN 中进行近似[贝叶斯推断](@entry_id:146958) [@problem_id:3500238]。具体来说，在训练好的网络上进行 $K$ 次带有随机 Dropout 掩码的[前向传播](@entry_id:193086)，可以看作是从近似的权重[后验分布](@entry_id:145605) $q(\mathbf{W})$ 中抽取了 $K$ 个样本。

因此，我们可以通过以下 **MC Dropout** 流程来估计[认知不确定性](@entry_id:149866)：
1.  对于给定的测试构型 $\mathbf{R}_\star$，进行 $K$ 次随机[前向传播](@entry_id:193086)。在每次传播 $k=1, \dots, K$ 中，应用一个新的随机 Dropout 掩码 $\mathbf{z}_k$，并计算对应的能量 $E(\mathbf{R}_\star; \mathbf{W} \odot \mathbf{z}_k)$ 和力 $\mathbf{F}_k = -\nabla_{\mathbf{R}} E(\mathbf{R}_\star; \mathbf{W} \odot \mathbf{z}_k)$。
2.  将得到的 $K$ 个力向量 $\{\mathbf{F}_k\}$ 视为从[预测分布](@entry_id:165741)中抽取的样本。
3.  通过计算这些样本的均值和协[方差](@entry_id:200758)来估计[预测分布](@entry_id:165741)的矩：
    *   **预测均力**: $\hat{\boldsymbol{\mu}}_{\mathbf{F}} = \frac{1}{K} \sum_{k=1}^K \mathbf{F}_k$
    *   **认知不确定性协[方差](@entry_id:200758)**: $\hat{\boldsymbol{\Sigma}}_{\mathbf{F}} = \frac{1}{K-1} \sum_{k=1}^K (\mathbf{F}_k - \hat{\boldsymbol{\mu}}_{\mathbf{F}})(\mathbf{F}_k - \hat{\boldsymbol{\mu}}_{\mathbf{F}})^{\top}$
如果模型还考虑了恒定的偶然不确定性（例如，假设力标签服从精度为 $\tau$ 的[高斯噪声](@entry_id:260752)），则总的预测协[方差](@entry_id:200758)应为认知和偶然分量之和：$\hat{\boldsymbol{\Sigma}}_{\mathbf{F}, \text{total}} = \hat{\boldsymbol{\Sigma}}_{\mathbf{F}} + \tau^{-1} \mathbf{I}$ [@problem_id:3500238]。

### 高级主题与实践考量

#### 对称性与[等变性](@entry_id:636671)

物理定律具有对称性，将这些对称性融入模型架构是构建数据高效且泛化能力强的MLPs的关键。对于原子势，[旋转不变性](@entry_id:137644)（能量）和**[等变性](@entry_id:636671)（equivariance）**（力）尤为重要。一个旋转等变的力模型 $f(x)$ 满足 $f(Rx) = R f(x)$，其中 $R$ 是一个[旋转操作](@entry_id:140575)。

在贝叶斯模型（如GP）中施加[等变性](@entry_id:636671)，相当于在函数空间上定义一个具有对称性的先验。这会极大地提高数据效率。考虑一个等变的GP先验，其协[方差](@entry_id:200758)满足 $K(Rx, Rx') = R K(x, x') R^{\top}$。如果我们在一个构型 $x$ 上观测到一个数据点，该信息会通过这个结构化的[协方差传播](@entry_id:747989)到由[对称操作](@entry_id:143398)生成的整个[轨道](@entry_id:137151) $\{Rx \mid R \in \mathrm{SO}(3)\}$ 上。这意味着，在[轨道](@entry_id:137151)上的任何一点 $Rx$ 处，后验不确定性的减小程度与在 $x$ 点处完全相同。相比之下，一个不具备[等变性](@entry_id:636671)的通用模型，在观测到 $x$ 之后，其在 $Rx$ 点的不确定性几乎不会降低。因此，对于一个具有 $| \mathcal{G} |$ 个元素的有限[对称群](@entry_id:146083) $\mathcal{G}$，在[轨道](@entry_id:137151)上的一个代表点上训练等变模型，其效果类似于在一个非等变模型上使用所有 $| \mathcal{G} |$ 个对称副本进行[数据增强](@entry_id:266029) [@problem_id:3500195]。

#### 无[分布](@entry_id:182848)假设的置信区间：[共形预测](@entry_id:635847)

贝叶斯方法虽然强大，但其[不确定性估计](@entry_id:191096)的可靠性依赖于模型假设（如先验和似然）的正确性。**[共形预测](@entry_id:635847)（Conformal Prediction）** 提供了一种截然不同的思路，它是一种无[分布](@entry_id:182848)假设的框架，能够为预测提供严格的边际覆盖率保证。

**切分[共形预测](@entry_id:635847)（Split Conformal Prediction）** 的工作流程如下：
1.  将数据分为[训练集](@entry_id:636396)和**校准集（calibration set）**。
2.  在[训练集](@entry_id:636396)上训练一个点预测模型。对于力预测，这个模型可以输出一个[均值向量](@entry_id:266544) $\boldsymbol{\mu}(x)$ 和一个[协方差矩阵](@entry_id:139155) $\boldsymbol{\Sigma}(x)$。
3.  定义一个**非符合性分数（nonconformity score）** $s(x, y)$，用于衡量一个观测值 $y$ 与模型在 $x$ 处的预测的“奇异程度”。一个好的选择是利用模型自身预测的协[方差](@entry_id:200758)，计算残差的**[马氏范数](@entry_id:751651)（Mahalanobis norm）**：
    $$
    s(x, y) = \sqrt{(y - \boldsymbol{\mu}(x))^{\top} \boldsymbol{\Sigma}(x)^{-1} (y - \boldsymbol{\mu}(x))}
    $$
4.  在校准集上计算每个样本的非符合性分数 $\{s_i\}$。
5.  为了获得至少 $1-\alpha$ 的覆盖率，找到这些分数的分位数 $\hat{q}$，即第 $\lceil (n_{\text{cal}}+1)(1-\alpha) \rceil$ 小的分数值。
6.  对于一个新的测试点 $x_{\text{test}}$，其预测集 $S_{\alpha}(x_{\text{test}})$ 由所有满足 $s(x_{\text{test}}, y) \le \hat{q}$ 的可能输出 $y$ 组成。

这个预测集 $S_{\alpha}(x_{\text{test}})$ 是一个以 $\boldsymbol{\mu}(x_{\text{test}})$ 为中心、由 $\boldsymbol{\Sigma}(x_{\text{test}})$ 和 $\hat{q}$ 决定的椭球。该框架的强大之处在于，只要数据是可交换的（exchangeable），它就能保证真实的力向量以至少 $1-\alpha$ 的概率落入这个预测集中，而无需假设预测误差服从任何特定[分布](@entry_id:182848) [@problem_id:3500220]。

#### 评估[不确定性估计](@entry_id:191096)的质量：校准

最后，一个至关重要的问题是：“我们如何知道模型给出的[不确定性估计](@entry_id:191096)是可靠的？” 这引出了**校准（calibration）** 的概念。一个经过良好校准的[概率模型](@entry_id:265150)，其预测的概率应该与真实的观测频率相匹配。

对于连续变量的回归问题，校准可以通过**[概率积分变换](@entry_id:262799)（Probability Integral Transform, PIT）** 来诊断。如果一个模型是完美校准的，那么对于每个测试观测值 $y_i$，其在其对应的预测[累积分布函数](@entry_id:143135)（CDF）$F_i$ 下的值 $U_i = F_i(y_i)$，应该服从**[均匀分布](@entry_id:194597) $\mathrm{Uniform}(0,1)$** [@problem_id:3500250]。我们可以通过绘制PIT值的直方图或[经验CDF](@entry_id:276747)来直观地检查其是否偏离[均匀分布](@entry_id:194597)。

为了量化评估校准性和预测质量，可以使用以下指标：
*   **[负对数似然](@entry_id:637801)（Negative Log-Likelihood, NLL）**: 这是一个严格的**固有评分规则（proper scoring rule）**，它同时评估预测的准确性和[不确定性估计](@entry_id:191096)。对于一个高斯预测 $\mathcal{N}(\mu_i, \sigma_i^2)$，其值为 $\frac{1}{2}\log(2\pi \sigma_i^2) + \frac{(y_i - \mu_i)^2}{2\sigma_i^2}$。
*   **连续分级概率分数（Continuous Ranked Probability Score, CRPS）**: 这是另一个固有评分规则，可视为[均方根误差](@entry_id:170440)向概率预测的推广。其定义为 $\mathrm{CRPS}(F,y) = \int_{-\infty}^{\infty} ( F(z) - \mathbf{1}\{z \ge y\} )^2 \, dz$。
*   **期望校准误差（Expected Calibration Error, ECE）**: 这是一个直接衡量校准程度的指标。例如，可以通过计算PIT值的[经验CDF](@entry_id:276747)与理想的均匀CDF之间的平均偏差来定义一个基于PIT的ECE [@problem_id:3500250]。

通过结合这些原理和工具，我们可以为[机器学习势函数](@entry_id:138428)建立起一套强大而严谨的[不确定性量化](@entry_id:138597)框架，从而在科学发现和工程设计中更安全、更有效地利用这些强大的模型。