## 引言
独立成分分析（Independent Component Analysis, ICA）是一种强大的统计与计算技术，旨在从观测到的混合信号中揭示并分离出隐藏的、独立的源信号。在从遥感图像中分离不同地物信号，到从脑电信号中解析不同大脑活动等诸多科学与工程问题中，我们面对的往往是多个未知源[信号叠加](@entry_id:276221)后的结果。传统方法如主成分分析（PCA）在处理仅不相关而非独立的信号时会遇到瓶颈，这正是ICA发挥其独特价值所在，它通过利用信号的高阶统计特性，解决了这一更深层次的分离问题。

本文将系统性地引导读者深入理解ICA。在“原理与机制”一章中，我们将揭示其背后的数学模型、核心假设（[统计独立性](@entry_id:150300)与非高斯性）以及关键算法机制。随后的“应用与跨学科联系”一章将展示ICA如何在[环境遥感](@entry_id:1124564)、神经影像学等不同领域解决实际问题，突显其作为通用数据分析工具的强大威力。最后，在“动手实践”部分，我们准备了一系列练习，旨在将理论知识转化为实际操作能力。通过本文的学习，读者将掌握ICA的理论精髓，并了解其在多个学科中的应用范式。

## 原理与机制

独立成分分析 (Independent Component Analysis, ICA) 是一种强大的信号处理和数据分析技术，其核心目标是从观测到的混合信号中分离出统计独立的潜在源信号。本章将深入探讨支撑 ICA 的基本原理和核心机制，阐明其如何超越传统的二阶统计方法，并通过最大化非高斯性或最大化[似然](@entry_id:167119)来解决[盲源分离](@entry_id:196724)问题。我们将从生成模型出发，逐步揭示其理论基础、优化目标、实际算法流程以及模型固有的不确定性。

### ICA 的生成模型与核心假设

在许多遥感和环境建模问题中，我们观测到的信号是多个独立物理过程线性叠加的结果。例如，高光谱图像中的一个像素点的[反射率](@entry_id:172768)可能是地表上不同物质（如水体、植被、土壤）的[光谱特征](@entry_id:1132105)及其相应丰度的[线性组合](@entry_id:154743)。ICA 正是为解决此类问题而设计的。

其最基础的数学模型是一个线性瞬时[混合模型](@entry_id:266571)。假设我们有一个 $m$ 维的观测向量 $\mathbf{x} \in \mathbb{R}^m$（例如，一个像素在 $m$ 个光谱波段的测量值），它是由 $k$ 个未知的、独立的源信号 $s_1, s_2, \dots, s_k$ 线性混合而成。该模型可以表示为：

$$
\mathbf{x} = \mathbf{A}\mathbf{s} + \mathbf{n}
$$

其中：
- $\mathbf{s} \in \mathbb{R}^k$ 是 **源信号向量 (source vector)**，其分量 $s_i$ 代表潜在的、独立的物理过程。在遥感中，这可以被解释为不同地物（端元）的丰度或某种大气过程（如[气溶胶光学厚度](@entry_id:1120862)异常）的强度。
- $\mathbf{A} \in \mathbb{R}^{m \times k}$ 是 **混合矩阵 (mixing matrix)**，为一个未知的常数矩阵。它的每一列 $\mathbf{a}_i$ 代表第 $i$ 个源信号在 $m$ 个传感器上的“签名”或响应模式。在光[谱分解](@entry_id:173707)中，$\mathbf{a}_i$ 就对应于第 $i$ 个端元的[光谱特征](@entry_id:1132105)。
- $\mathbf{n} \in \mathbb{R}^m$ 是 **噪声向量 (noise vector)**，代表[传感器噪声](@entry_id:1131486)或模型未能完全捕捉的随机扰动。

ICA 的目标是在仅知道观测数据 $\mathbf{x}$ 的情况下，同时估计出[混合矩阵](@entry_id:1127969) $\mathbf{A}$ 和源信号 $\mathbf{s}$。这是一个典型的 **[盲源分离](@entry_id:196724) (Blind Source Separation, BSS)** 问题。为了使这个问题可解，ICA 引入了两个关键的、深刻的假设 ：

1.  **[统计独立性](@entry_id:150300) (Statistical Independence)**：源信号 $s_1, s_2, \dots, s_k$ 是相互统计独立的。这意味着任意一个源信号的信息都不能从其他源信号中推断出来。在数学上，这表示源向量 $\mathbf{s}$ 的[联合概率密度函数](@entry_id:267139) (PDF)可以分解为其边缘[概率密度函数](@entry_id:140610)的乘积：
    $$
    p_s(s_1, \dots, s_k) = \prod_{i=1}^k p_{s_i}(s_i)
    $$

2.  **[非高斯性](@entry_id:158327) (Non-Gaussianity)**：源信号的分布必须是非高斯分布。在所有源信号中，最多只允许有一个分量是高斯分布的。我们很快会看到，这个假设是区分 ICA 与其他方法（如主成分分析）并使问题可解的根本所在。

在理想的无噪声情况下（$\mathbf{n} = \mathbf{0}$），如果满足上述假设，并且混合矩阵 $\mathbf{A}$ 是列满秩的（即 $\operatorname{rank}(\mathbf{A}) = k$），且观测数量不少于源数量（$m \ge k$），那么就有可能找到一个 **解混矩阵 (unmixing matrix)** $\mathbf{W} \in \mathbb{R}^{k \times m}$ 来恢复源信号，即 $\mathbf{s} \approx \mathbf{W}\mathbf{x}$ 。

### 超越二阶统计：为何需要独立性？

传统的数据分析方法，如 **主成分分析 (Principal Component Analysis, PCA)**，主要依赖于数据的[二阶统计量](@entry_id:919429)，即[协方差矩阵](@entry_id:139155)。PCA 通过寻找使投影方差最大化的正交方向来对数据进行[降维](@entry_id:142982)和去相关。然而，仅仅做到 **不相关 (uncorrelated)** 并不等同于 **统计独立 (statistically independent)**。

不相关是一个较弱的条件，它仅仅意味着两个变量的协方差为零，即 $\operatorname{Cov}(U, V) = 0$。而统计独立则是一个强得多的条件，它要求[联合分布](@entry_id:263960)可分解。只有当变量服从[联合高斯](@entry_id:636452)分布时，不相关才等价于独立。对于非高斯的世界，仅依赖[二阶统计量](@entry_id:919429)会错失变量间更高阶的依赖关系。

让我们通过一个遥感场景来具体说明这一点 。假设一个光谱仪观测的两个波段[反射率](@entry_id:172768) $R_1$ 和 $R_2$ 都源于一个共同的潜在物理变量——地表的微面元坡度 $X$。假设 $X$ 是一个均值为零、[概率密度](@entry_id:175496)对称的[随机变量](@entry_id:195330)。$R_1$ 与坡度呈线性关系，如 $R_1 = \alpha X$；而 $R_2$ 由于更复杂的散射效应，呈现二次关系，如 $R_2 = \beta (X^2 - \sigma^2)$，其中 $\sigma^2$ 是 $X$ 的方差，这样构造可以使 $R_2$ 的均值为零。

我们可以计算这两个信号的协方差：
$$
\operatorname{Cov}(R_1, R_2) = E[R_1 R_2] = E[\alpha X \cdot \beta (X^2 - \sigma^2)] = \alpha \beta (E[X^3] - \sigma^2 E[X])
$$
由于 $X$ 的分布是对称的，其三阶矩 $E[X^3]$ 为零。又因为其均值 $E[X]$ 为零，我们最终得到 $\operatorname{Cov}(R_1, R_2) = 0$。这意味着 $R_1$ 和 $R_2$ 是不相关的。

如果我们将这组数据输入 PCA，由于[协方差矩阵](@entry_id:139155)已经是（或接近）对角矩阵，PCA 会认为这两个信号已经是“分离的”主成分，从而无法发现它们之间潜在的关联。然而，这两个信号显然不是独立的。我们知道 $R_2 = \frac{\beta}{\alpha^2} R_1^2 - \beta \sigma^2$，即 $R_2$ 是 $R_1$ 的一个确定性函数。它们之间存在着紧密的[非线性依赖](@entry_id:265776)关系。

这个例子清楚地表明，仅仅依赖于消除[二阶相关](@entry_id:190427)性的方法（如 PCA）无法分离出具有更高阶依赖关系的信号。而 ICA 的目标正是利用这种高阶统计信息来寻找真正独立的成分 。

### 核心原理：最大化非高斯性

ICA 得以工作的核心洞察源于 **中心极限定理 (Central Limit Theorem, CLT)**。CLT 指出，大量[独立随机变量](@entry_id:273896)之和的分布倾向于高斯分布，无论[原始变量](@entry_id:753733)自身的分布是什么 。

现在，让我们回到 ICA 模型。观测信号 $x_j$ (混合信号的任意一个分量) 是源信号 $s_i$ 的[线性组合](@entry_id:154743)：$x_j = \sum_i A_{ji} s_i$。同样，对观测数据 $\mathbf{x}$ 的任意一个投影 $y = \mathbf{w}^\top \mathbf{x}$，也是源信号的线性组合：
$$
y = \mathbf{w}^\top \mathbf{A} \mathbf{s} = \mathbf{v}^\top \mathbf{s} = \sum_i v_i s_i
$$
其中 $\mathbf{v} = \mathbf{A}^\top \mathbf{w}$。

根据 CLT，这个混合体 $y$ 的分布通常会比任何单个源信号 $s_i$ 的分布都“更接近”高斯分布。反过来看，如果我们能找到一个投影方向 $\mathbf{w}$，使得投影结果 $y$ 的分布**最不接近**高斯分布，那么这个投影就很可能已经消除了混合，仅仅反映了单个源信号的特征，即此时向量 $\mathbf{v}$ 中只有一个非零元素。

因此，ICA 的任务可以转化为一个优化问题：**寻找一个解混矩阵 $\mathbf{W}$，使得其行向量 $\mathbf{w}_i^\top$ 能够最大化投影 $\mathbf{w}_i^\top \mathbf{x}$ 的非高斯性**。

这个原理在一个经典场景下表现得尤为突出 。假设源信号 $s_1, s_2$ 独立、非高斯且已被标准化（零均值、单位方差），混合矩阵 $\mathbf{A}$ 恰好是一个[正交矩阵](@entry_id:169220)（例如旋转矩阵）。此时，观测信号 $\mathbf{x} = \mathbf{A}\mathbf{s}$ 的[协方差矩阵](@entry_id:139155)为：
$$
\operatorname{Cov}(\mathbf{x}) = \mathbf{A} \operatorname{Cov}(\mathbf{s}) \mathbf{A}^\top = \mathbf{A} \mathbf{I} \mathbf{A}^\top = \mathbf{A} \mathbf{A}^\top = \mathbf{I}
$$
这意味着观测信号本身已经是“白化的”——其分量不相关且方差为1。对于 PCA 来说，这种情况是灾难性的。由于协方差矩阵是单位阵，所有方向的方差都相等，不存在任何“主”方向。PCA 在此完全失效，无法确定任何有意义的旋转来分离信号。然而，ICA 却能解决这个问题。尽管 $\mathbf{x}$ 的分量不相关，但它们不是独立的。ICA 会通过寻找一个旋转，最大化输出信号的非高斯性，最终找到那个能抵消 $\mathbf{A}$ 的旋转，从而成功分离出源信号 $s_1$ 和 $s_2$ 。

### [非高斯性](@entry_id:158327)的度量

为了将“最大化非高斯性”的原理转化为可执行的算法，我们需要一个量化的度量指标。常用的非高斯性度量包括峰度 (Kurtosis) 和[负熵](@entry_id:194102) (Negentropy)。

#### [峰度](@entry_id:269963) (Kurtosis)

峰度是衡量概率分布“尾部”重量或“尖峰”程度的四阶统计量。对于一个经过[标准化](@entry_id:637219)（零均值，单位方差）的[随机变量](@entry_id:195330) $y$，其 **[超额峰度](@entry_id:908640) (excess kurtosis)** 定义为 [@problem crammed-learning-strategy-based-problem-solving-technique-for-the-independent-component-analysis-3822212]：

$$
\kappa(y) = E[y^4] - 3
$$

这个定义以高斯分布为基准，因为标准高斯分布的四阶矩 $E[Z^4] = 3$，其[超额峰度](@entry_id:908640)为 0。峰度的正负号揭示了分布的形态：

-   **$\kappa(y) > 0$ (超高斯, Super-Gaussian 或 Leptokurtic)**：分布比高斯分布更“尖峭”，尾部更“重”。这意味着极端值（远离均值的值）出现的概率更高。在遥感中，稀疏的、脉冲式的信号，如间歇性污染源的排放羽流，通常是超高斯分布的。

-   **$\kappa(y)  0$ (亚高斯, Sub-Gaussian 或 Platykurtic)**：分布比高斯分布更“平坦”，尾部更“轻”。这类分布通常是有限的、更接近均匀分布。例如，一片均匀背景的[反射率](@entry_id:172768)波动可能呈现亚高斯特性。

因此，ICA 的一个简单实现就是寻找投影方向 $\mathbf{w}$ 来最大化[超额峰度](@entry_id:908640)的绝对值 $|\kappa(\mathbf{w}^\top \mathbf{x})|$。这会引导算法找到最能体现超高斯或亚高斯特性的投影，这些投影对应于独立的源信号 [@problem crammed-learning-strategy-based-problem-solving-technique-for-the-independent-component-analysis-3822212] [@problem crammed-learning-strategy-based-problem-solving-technique-for-the-independent-component-analysis-3822136]。

#### [负熵](@entry_id:194102) (Negentropy)

虽然峰度在概念上简单，但它对异常值非常敏感，可能不够稳健。一个在理论上更优越的度量是 **[负熵](@entry_id:194102)**。它基于信息论中的 **[微分熵](@entry_id:264893) (differential entropy)**，定义为：

$$
H(y) = - \int p_y(u) \ln p_y(u) du
$$

信息论的一个基本结论是：**在所有具有相同方差的[连续随机变量](@entry_id:166541)中，高斯分布的变量具有最大的[微分熵](@entry_id:264893)** [@problem crammed-learning-strategy-based-problem-solving-technique-for-the-independent-component-analysis-3822245]。这为我们提供了一个完美的非高斯性度量。[负熵](@entry_id:194102) $J(y)$ 定义为具有相同方差的[高斯变量](@entry_id:276673) $y_{\text{Gauss}}$ 的熵与 $y$ 的熵之差：

$$
J(y) = H(y_{\text{Gauss}}) - H(y)
$$

根据熵的最大化性质，$J(y) \ge 0$，并且当且仅当 $y$ 是高斯分布时等号成立。因此，[负熵](@entry_id:194102)是一个恒为非负的量，它的大小直接反映了变量 $y$ 与高斯分布的偏离程度，使其成为一个理想的[非高斯性](@entry_id:158327)度量。最大化[负熵](@entry_id:194102) $J(y)$ 是 ICA 的一个核心优化目标，它与最大化[峰度](@entry_id:269963)在精神上一脉相承，但通常具有更好的数学性质和稳健性。

### 概率框架：作为最大似然估计的 ICA

除了作为一种投影寻踪技术，ICA 也可以被置于一个更严谨的概率框架中，即 **最大似然估计 (Maximum Likelihood Estimation, MLE)** [@problem crammed-learning-strategy-based-problem-solving-technique-for-the-independent-component-analysis-3822134]。这种观点不仅为 ICA 提供了坚实的理论基础，也揭示了先验知识如何影响分离过程。

给定观测模型 $\mathbf{s} = \mathbf{W}\mathbf{x}$，其中 $\mathbf{W}$ 是待估计的解混矩阵。我们可以利用变量代换公式推导出观测数据 $\mathbf{x}$ 的概率密度函数 $p_x(\mathbf{x})$：
$$
p_x(\mathbf{x}) = p_s(\mathbf{W}\mathbf{x}) |\det(\mathbf{W})|
$$
由于源信号 $s_i$ 是独立的，其联合概率密度 $p_s(\mathbf{s})$ 可以分解为 $\prod_i p_i(s_i)$。因此，对于单个数据点 $\mathbf{x}_t$，其[对数似然](@entry_id:273783)为：
$$
\ln p_x(\mathbf{x}_t | \mathbf{W}) = \ln |\det(\mathbf{W})| + \sum_{i=1}^m \ln p_i((\mathbf{W}\mathbf{x}_t)_i)
$$
对于整个数据集 $\\{\mathbf{x}_t\\}_{t=1}^T$，平均对数似然函数 $\ell(\mathbf{W})$ 为：
$$
\ell(\mathbf{W}) = \ln |\det(\mathbf{W})| + \frac{1}{T}\sum_{t=1}^T \sum_{i=1}^m \ln p_i((\mathbf{W}\mathbf{x}_t)_i)
$$
ICA 的任务就变成了找到一个矩阵 $\mathbf{W}$ 来最大化这个对数似然函数。

在这个框架下，我们必须为每个源信号 $s_i$ 假设一个先验的概率分布 $p_i$。这个选择至关重要，因为它定义了我们期望分离出的信号具有何种统计特性。例如，如果我们相信源信号是稀疏的、脉冲式的（超高斯），我们可以选择[拉普拉斯分布](@entry_id:266437)作为先验。如果我们相信信号是有界的（亚高斯），我们可以选择均匀分布。

通过对[似然函数](@entry_id:921601)求梯度，可以得到一个用于优化的更新规则。梯度表达式为 [@problem crammed-learning-strategy-based-problem-solving-technique-for-the-independent-component-analysis-3822134]：
$$
\nabla_{\mathbf{W}} \ell(\mathbf{W}) = (\mathbf{W}^{-1})^\top - E[\mathbf{\psi}(\mathbf{W}\mathbf{x}) \mathbf{x}^\top]
$$
其中，$\mathbf{\psi}(s) = [\psi_1(s_1), \dots, \psi_m(s_m)]^\top$ 是一个向量，其分量 $\psi_i(u) = \frac{d}{du}\ln p_i(u)$ 被称为 **[得分函数](@entry_id:164520) (score function)**。这个梯度表达式明确显示，学习过程（对 $\mathbf{W}$ 的调整）直接由得分函数 $\mathbf{\psi}$驱动，而得分函数又完全由我们选择的源信号先验分布 $p_i$ 决定。这为将关于信号物理特性的先验知识融入算法提供了正式途径。

### 实用机制：预处理与算法流程

典型的 ICA 算法包含两个关键的[预处理](@entry_id:141204)步骤：中心化和白化。

1.  **中心化 (Centering)**：这是最简单的步骤，即从数据中减去其[均值向量](@entry_id:266544)，$\mathbf{x} \leftarrow \mathbf{x} - E[\mathbf{x}]$。这使得处理后的数据具有零均值，简化了后续的计算。

2.  **白化 (Whitening)**：白化是一个更重要的步骤，它对数据进行[线性变换](@entry_id:149133)，使得变换后的数据 $\mathbf{z}$ 的[协方差矩阵](@entry_id:139155)为单位矩阵，即 $\operatorname{Cov}(\mathbf{z}) = \mathbf{I}$ [@problem crammed-learning-strategy-based-problem-solving-technique-for-the-independent-component-analysis-3822209]。这意味着白化后的数据各分量是不相关的，并且方差为1。

白化可以通过数据的协方差矩阵 $\mathbf{C} = \operatorname{Cov}(\mathbf{x})$ 的[特征值分解](@entry_id:272091)来实现。设 $\mathbf{C} = \mathbf{U}\mathbf{\Lambda}\mathbf{U}^\top$，其中 $\mathbf{U}$ 是[特征向量](@entry_id:151813)组成的[正交矩阵](@entry_id:169220)，$\mathbf{\Lambda}$ 是特征值组成的[对角矩阵](@entry_id:637782)。白化矩阵 $\mathbf{V}$ 可以定义为：
$$
\mathbf{V} = \mathbf{\Lambda}^{-1/2} \mathbf{U}^\top
$$
其中 $\mathbf{\Lambda}^{-1/2}$ 是对角线上元素为 $1/\sqrt{\lambda_i}$ 的对角矩阵。变换后的数据为 $\mathbf{z} = \mathbf{V}\mathbf{x}$。

白化的关键作用在于它极大地简化了 ICA 问题。原始的[混合模型](@entry_id:266571)是 $\mathbf{x} = \mathbf{A}\mathbf{s}$。白化后的模型变为 $\mathbf{z} = \mathbf{V}\mathbf{x} = (\mathbf{V}\mathbf{A})\mathbf{s}$。可以证明，新的[混合矩阵](@entry_id:1127969) $\mathbf{A'} = \mathbf{V}\mathbf{A}$ 是一个**[正交矩阵](@entry_id:169220)** [@problem crammed-learning-strategy-based-problem-solving-technique-for-the-independent-component-analysis-3822209]。这意味着，白化之后，剩下的混合效应仅仅是一个旋转（或反射）。因此，寻找任意可逆解混矩阵 $\mathbf{W}$ 的复杂问题，被简化为寻找一个[正交矩阵](@entry_id:169220)（旋转矩阵）$\mathbf{R}$ 的问题，使得 $\mathbf{s} \approx \mathbf{R}\mathbf{z}$。这显著减小了参数的搜索空间，提高了算法的效率和稳定性。此外，在白化空间中，所有投影的方差都为1，这使得最大化[负熵](@entry_id:194102) $J(y)$ 等价于最小化熵 $H(y)$，进一步简化了优化目标 [@problem crammed-learning-strategy-based-problem-solving-technique-for-the-independent-component-analysis-3822245]。

### 固有不确定性与标准化

尽管 ICA 功能强大，但它无法完全唯一地确定源信号。其解存在三个固有的不确定性或模糊性 [@problem crammed-learning-strategy-based-problem-solving-technique-for-the-independent-component-analysis-3822138]：

1.  **置换不确定性 (Permutation Ambiguity)**：我们无法确定恢复出的源信号的顺序。如果 $\mathbf{W}$ 是一个有效的解混矩阵，那么对于任意[置换矩阵](@entry_id:136841) $\mathbf{P}$，$\mathbf{P}\mathbf{W}$ 同样有效，它只是将恢复出的源信号重新排序。

2.  **尺度不确定性 (Scaling Ambiguity)**：我们无法确定源信号的真实幅度。对于任意非零常数 $c$，我们可以将一个源信号 $s_i$ 乘以 $c$，同时将其对应的[混合矩阵](@entry_id:1127969)列 $\mathbf{a}_i$ 除以 $c$，而它们的乘积 $\mathbf{a}_i s_i$ 保持不变，从而观测值 $\mathbf{x}$ 也不变。

3.  **符号不确定性 (Sign Ambiguity)**：这是尺度不确定性的一个特例（$c=-1$）。我们可以同时反转一个源信号及其对应混合向量的符号，而不会改变观测值。

这些不确定性是 ICA 模型的内在属性，而非算法的缺陷。为了得到一个确定的、可解释的解，我们必须引入 **[标准化](@entry_id:637219) (Normalization)** 约定。一个常见且在遥感中特别有用的标准化方案是 [@problem crammed-learning-strategy-based-problem-solving-technique-for-the-independent-component-analysis-3822138]：

-   **固定尺度**：强制要求每个恢复出的源信号 $s_i$ 具有单位方差（$\operatorname{Var}(s_i) = 1$）。这解决了尺度不确定性，并使得源信号成为无量纲的“强度”或“丰度”变量。因此，混合矩阵的列 $\mathbf{a}_i$ 便承载了所有的物理单位（如[反射率](@entry_id:172768)或辐射亮度），成为可物理解释的[光谱特征](@entry_id:1132105)。

-   **固定符号**：引入一个确定性的规则来选择符号。例如，可以要求每个混合向量 $\mathbf{a}_i$ 与观测数据的[均值向量](@entry_id:266544) $\boldsymbol{\mu}_\mathbf{x}$ 的[内积](@entry_id:750660)为非负。在[反射率](@entry_id:172768)或辐射亮度数据中，$\boldsymbol{\mu}_\mathbf{x}$ 的所有分量都是非负的，这个约定倾向于产生具有物理意义的、主导为正的[光谱特征](@entry_id:1132105)。

置换不确定性通常无法通过简单的数学约定解决，需要在后续的解译阶段，通过与先验知识或地面真值对比来为分离出的成分赋予物理意义。

### [模型选择](@entry_id:155601)：确定源的数量 $k$

在实际应用中，源信号的数量 $k$ 通常是未知的。选择一个合适的 $k$ 是一个关键的[模型选择](@entry_id:155601)问题。如果 $k$ 太小，模型将无法捕捉所有独立的物理过程（[欠拟合](@entry_id:634904)）；如果 $k$ 太大，算法可能会开始拟合噪声，产生虚假的、难以解释的成分（[过拟合](@entry_id:139093)）。

在 PCA 与 ICA 结合的流水线中，通常首先通过 PCA 将数据[降维](@entry_id:142982)到 $k$ 维。这个 $k$ 的选择可以通过信息论准则来指导，如 **赤池[信息量](@entry_id:272315)准则 (Akaike Information Criterion, AIC)**、**贝叶斯信息准则 (Bayesian Information Criterion, BIC)** 或 **[最小描述长度](@entry_id:261078) (Minimum Description Length, MDL)** [@problem crammed-learning-strategy-based-problem-solving-technique-for-the-independent-component-analysis-3822231]。

这些准则都在模型的[拟合优度](@entry_id:176037)（通常用最大化[似然](@entry_id:167119)值衡量）和模型复杂度（用自由参数的数量衡量）之间进行权衡。它们的通用形式是：

$$
\text{Criterion} = -2 \ln(\text{Likelihood}) + \text{Penalty}
$$

其中，AIC 的惩罚项是 $2p$，而 BIC 和 MDL 的惩罚项是 $p \ln(n)$，这里 $p$ 是模型的自由参数数量，$n$ 是样本数量。

在 PCA-ICA 框架中，我们不仅要考虑 PCA 阶段的参数，还要考虑 ICA 阶段的参数。ICA 阶段是在一个 $k$ 维子空间中寻找一个旋转矩阵，其自由参数的数量为 $k(k-1)/2$ [@problem crammed-learning-strategy-based-problem-solving-technique-for-the-independent-component-analysis-3822231]。

对于拥有大量样本（$n$ 很大）的遥感数据，BIC 和 MDL 的惩罚项（与 $\ln(n)$ 成正比）比 AIC 的惩罚项增长得快得多。这意味着 BIC 和 MDL 会更倾向于选择更简单的模型（更小的 $k$），因此它们在[防止过拟合](@entry_id:635166)方面更为保守和稳健，这在高[信噪比](@entry_id:271861)不是特别高的高维数据中是一个理想的特性 [@problem crammed-learning-strategy-based-problem-solving-technique-for-the-independent-component-analysis-3822231]。在许多条件下，BIC 和 MDL 在大样本极限下是[渐近等价](@entry_id:273818)的，并且都是“一致的”，即当样本数趋于无穷时，它们有能力以概率 1 选择出真实模型。