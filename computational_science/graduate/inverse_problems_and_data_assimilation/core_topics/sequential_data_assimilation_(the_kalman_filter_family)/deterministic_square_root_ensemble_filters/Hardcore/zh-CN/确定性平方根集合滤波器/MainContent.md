## 引言
确定性平方根集合滤波器是数据同化领域一类功能强大且理论优雅的算法，广泛应用于地球科学、工程学等众多领域。它们旨在解决标准集合卡尔曼滤波器（EnKF）的一个核心局限性：通过对观测值进行随机扰动来更新集合成员时，会不可避免地引入额外的采样噪声，尤其是在集合规模有限时，这种噪声会降低分析的准确性。本文旨在为读者提供一个关于确定性平方根集合滤波器的全面而深入的理解。

为实现这一目标，本文将分为三个核心章节。在第一章“原理与机制”中，我们将从第一性原理出发，详细推导确定性更新的数学基础，阐明其相对于随机方法的优势，并探讨其内在的几何与统计特性。接着，在第二章“应用与交叉学科联系”中，我们将理论与实践相结合，探讨如何通过协方差膨胀、局域化、状态增广等技术，将该滤波器框架应用于解决高维、非线性以及模型不确定的复杂现实问题，并展示其与机器学习等前沿领域的交叉融合。最后，在第三章“动手实践”中，您将通过一系列精心设计的编程练习，亲手实现并诊断滤波器的行为，从而将理论知识转化为实践技能。现在，让我们首先深入其核心，探究确定性平方根集合滤波器的基本原理与精妙机制。

## 原理与机制

本章将深入探讨确定性平方根集合滤波器的核心原理与机制。与在前一章介绍的、依赖于随机扰动观测的标准集合卡尔曼滤波器（EnKF）不同，确定性方法旨在通过一种无随机性的方式来更新集合，从而避免因随机采样引入的额外误差。我们将从第一性原理出发，推导这些滤波器的数学基础，阐释其关键特性，并探讨其在理论和实践层面的一些高级主题。

### 从随机到确定：集合变换的基本思想

在经典的随机集合卡尔曼滤波器（Stochastic EnKF）中，分析步骤通过为每个集合成员同化一个经过独立随机扰动的数据来实现。具体而言，对于第 $i$ 个集合成员 $\mathbf{x}^f_i$，其更新所用的观测值为 $\mathbf{y}_i = \mathbf{y} + \boldsymbol{\varepsilon}_i$，其中 $\boldsymbol{\varepsilon}_i$ 是从观测误差分布 $\mathcal{N}(0, \mathbf{R})$ 中抽取的随机样本。虽然这种方法在期望意义上可以再现正确的分析协方差，但对于有限大小的集合，随机扰动 $\boldsymbol{\varepsilon}_i$ 会引入采样噪声。这种噪声不仅会污染分析协方差的估计，还会导致分析均值偏离其理论最优值，尤其是在集合规模 $m$ 较小或观测误差协方差 $\mathbf{R}$ 较小时，这一问题尤为突出 [@problem_id:3123851] [@problem_id:3375992]。

为了克服这一限制，**确定性平方根集合滤波器 (deterministic square-root ensemble filters)** 应运而生。其核心思想是放弃对观测值的随机扰动，转而直接对预报异常矩阵 $\mathbf{A}^f$ 进行一次确定性的线性变换。我们的目标是寻找一个变换矩阵 $\mathbf{T}$，使得经过变换后的分析异常矩阵 $\mathbf{A}^a = \mathbf{A}^f \mathbf{T}$ 所对应的样本协方差，能够精确地等于由卡尔曼滤波理论给出的分析后验协方差。这种方法完全消除了由观测扰动引入的采样误差，确保了在给定预报集合的条件下，分析协方差的更新是精确且可复现的 [@problem_id:3375992] [@problem_id:3123851]。

形式上，我们寻求一个变换矩阵 $\mathbf{T} \in \mathbb{R}^{m \times m}$（其中 $m$ 为集合大小），使得分析样本协方差 $\mathbf{P}^a_N$ 满足：
$$
\mathbf{P}^a_N = \frac{1}{m-1} \mathbf{A}^a (\mathbf{A}^a)^\top = \frac{1}{m-1} (\mathbf{A}^f \mathbf{T}) (\mathbf{A}^f \mathbf{T})^\top = \frac{1}{m-1} \mathbf{A}^f \mathbf{T} \mathbf{T}^\top (\mathbf{A}^f)^\top
$$
该式精确等于由预报样本协方差 $\mathbf{P}^f_N = \frac{1}{m-1} \mathbf{A}^f (\mathbf{A}^f)^\top$ 计算出的卡尔曼分析协方差：
$$
\mathbf{P}^a_{\text{Kalman}} = \mathbf{P}^f_N - \mathbf{P}^f_N \mathbf{H}^\top (\mathbf{H} \mathbf{P}^f_N \mathbf{H}^\top + \mathbf{R})^{-1} \mathbf{H} \mathbf{P}^f_N
$$
其中 $\mathbf{H}$ 是观测算子，$\mathbf{R}$ 是观测误差协方差。

### 对称平方根变换的推导

为了求解变换矩阵 $\mathbf{T}$，我们首先关注一类特殊的解：对称正定矩阵。这类解不仅在数学上性质优良，而且具有深刻的几何意义，我们将在后续章节中探讨。假设 $\mathbf{T}$ 是对称的，即 $\mathbf{T} = \mathbf{T}^\top$，则协方差匹配的条件变为：
$$
\frac{1}{m-1} \mathbf{A}^f \mathbf{T}^2 (\mathbf{A}^f)^\top = \mathbf{P}^a_{\text{Kalman}}
$$
将 $\mathbf{P}^f_N$ 的定义代入 $\mathbf{P}^a_{\text{Kalman}}$ 的表达式中，并进行整理，我们得到：
$$
\mathbf{A}^f \mathbf{T}^2 (\mathbf{A}^f)^\top = \mathbf{A}^f (\mathbf{A}^f)^\top - \mathbf{A}^f (\mathbf{A}^f)^\top \mathbf{H}^\top \left( \frac{1}{m-1} \mathbf{H} \mathbf{A}^f (\mathbf{A}^f)^\top \mathbf{H}^\top + \mathbf{R} \right)^{-1} \frac{1}{m-1} \mathbf{H} \mathbf{A}^f (\mathbf{A}^f)^\top
$$
为了简化此式，我们引入预报观测异常矩阵 $\mathbf{Y}^f = \mathbf{H} \mathbf{A}^f \in \mathbb{R}^{p \times m}$。上式可以重写为在 $m$ 维集合空间中的形式。通过应用 **Woodbury 矩阵恒等式**，可以证明右侧表达式等价于：
$$
\mathbf{A}^f \left( \mathbf{I}_m + \frac{1}{m-1} (\mathbf{Y}^f)^\top \mathbf{R}^{-1} \mathbf{Y}^f \right)^{-1} (\mathbf{A}^f)^\top
$$
通过比较系数，我们得到 $\mathbf{T}^2$ 的表达式：
$$
\mathbf{T}^2 = \left( \mathbf{I}_m + \frac{1}{m-1} (\mathbf{Y}^f)^\top \mathbf{R}^{-1} \mathbf{Y}^f \right)^{-1}
$$
因此，唯一的对称正定解 $\mathbf{T}_{\text{sym}}$ 是该矩阵的逆平方根 [@problem_id:3420567]：
$$
\mathbf{T}_{\text{sym}} = \left( \mathbf{I}_m + \frac{1}{m-1} (\mathbf{Y}^f)^\top \mathbf{R}^{-1} \mathbf{Y}^f \right)^{-1/2}
$$
这个矩阵 $\mathbf{T}_{\text{sym}}$ 通常被称为**对称平方根变换 (symmetric square-root transform)**。它提供了一种精确、确定且无偏（相对于给定的样本协方差）的方式来更新集合异常，从而避免了随机EnKF中的采样噪声问题。值得注意的是，在某些文献中，集合异常矩阵的定义不包含 $\frac{1}{\sqrt{m-1}}$ 因子（即 $\mathbf{P}^f = \mathbf{A}^f (\mathbf{A}^f)^\top$），此时 $\mathbf{T}_{\text{sym}}$ 的表达式中将不包含 $\frac{1}{m-1}$ 这一项 [@problem_id:3376050]。读者在查阅文献时应注意这些定义上的差异。

### 变换的诠释与性质

这个看似复杂的矩阵变换背后，蕴含着清晰的物理和几何意义。

#### 几何诠释：定向收缩

为了直观理解变换 $\mathbf{T}_{\text{sym}}$ 的作用，我们可以考虑一个单标量观测（$p=1$）的特例。在这种情况下，观测算子 $\mathbf{H}$ 简化为一个行向量 $\mathbf{h}^\top$，观测误差协方差 $\mathbf{R}$ 简化为一个标量方差 $r$。可以证明，变换矩阵 $\mathbf{T}_{\text{sym}}$ 具有一种非常特殊的结构：它沿着由向量 $\mathbf{v} = (\mathbf{Y}^f)^\top = (\mathbf{A}^f)^\top \mathbf{h}$ 定义的方向进行收缩，而在与 $\mathbf{v}$ 正交的子空间上表现为单位矩阵 [@problem_id:3376036]。

具体来说，$\mathbf{T}_{\text{sym}}$ 的作用是将集合空间中与观测信息相关的分量（由 $\mathbf{v}$ 代表）进行压缩，而保持与观测无关的分量不变。收缩的程度由一个因子 $c \in (0,1)$ 决定，其大小取决于预报在观测空间中的方差与观测误差方差的相对大小：
$$
c = \sqrt{\frac{r}{\mathbf{h}^\top \mathbf{P}^f_N \mathbf{h} + r}}
$$
这个因子 $c$ 衡量了分析步骤对预报不确定性的削减程度。当观测非常精确（$r \to 0$）时，$c \to 0$，表示不确定性被大幅削减；当观测非常不准（$r \to \infty$）时，$c \to 1$，表示几乎不更新，保留了原有的预报不确定性。这种定向收缩的特性，精确地反映了数据同化过程如何将新信息（观测）融合到现有知识（预报）中。

#### 集合塌缩：一个极端例子

当集合规模非常小时，例如 $m=2$，预报异常仅由一个向量 $\mathbf{v}$ 张成的子空间构成，此时预报协方差为秩一矩阵 $\mathbf{P}^f = \mathbf{v}\mathbf{v}^\top$。在这种情况下，分析协方差 $\mathbf{P}^a$ 仍与 $\mathbf{P}^f$ 共线，可以表示为 $\mathbf{P}^a = \alpha \mathbf{P}^f$。收缩系数 $\alpha$ 就等于我们上面讨论的方差缩减因子 $c^2$。例如，在一个具体的二维状态空间问题中，若 $\mathbf{v} = \begin{pmatrix} 3  1 \end{pmatrix}^\top$, $\mathbf{H} = \begin{pmatrix} 1  -1 \end{pmatrix}$, $r=0.04$，我们可以计算出 $\mathbf{h}^\top \mathbf{P}^f \mathbf{h} = 4$，因此 $\alpha = \frac{0.04}{4+0.04} = \frac{1}{101}$。这意味着分析协方差的唯一非零特征值是预报协方差特征值的 $1/101$ [@problem_id:3376052]。这个例子生动地展示了同化过程如何导致集合方差的“塌缩”(collapse)，这也是在实际应用中需要通过协方差膨胀等技术来缓解的问题。

#### 统计诠释：协方差收缩

从更广泛的统计学视角来看，卡尔曼更新可以被理解为一种**收缩估计 (shrinkage estimation)**。在一个理想化的场景中，假设预报协方差是各向同性的 $\mathbf{P}^f = \sigma_x^2 \mathbf{I}_n$，观测算子 $\mathbf{H}$ 是一个标准正交投影算子 $\mathbf{U}_r^\top$，且观测误差也是各向同性的 $\mathbf{R} = \sigma^2 \mathbf{I}_r$。在这种情况下，可以推导出分析协方差 $\mathbf{P}^a$ 是预报协方差 $\mathbf{P}^f$ 朝一个低秩目标 $\mathbf{P}_{\text{tgt}} = \sigma_x^2 (\mathbf{I}_n - \mathbf{U}_r \mathbf{U}_r^\top)$ 的一个凸组合 [@problem_id:3376059]：
$$
\mathbf{P}_a = (1-\lambda) \mathbf{P}_f + \lambda \mathbf{P}_{\text{tgt}}
$$
这里的收缩强度 $\lambda$ 被证明为：
$$
\lambda = \frac{\sigma_x^2}{\sigma_x^2 + \sigma^2}
$$
这个形式与统计学中著名的 Ledoit-Wolf 收缩估计如出一辙。它表明，分析协方差是通过将预报协方差（相当于“样本”信息）向一个结构化的先验目标（即在被观测的子空间内完全消除方差）进行“收缩”而得到的。收缩的程度 $\lambda$ 精确地由信噪比决定。这一观点为理解数据同化提供了一个深刻的统计学框架。

### 自由度：正交旋转的不确定性

我们推导出的对称变换 $\mathbf{T}_{\text{sym}}$ 只是众多可能的确定性变换中的一种。事实上，存在无穷多个变换矩阵都能满足协方差匹配的条件。

可以证明，如果 $\mathbf{T}_{\text{sym}}$ 是一个有效的变换，那么对于任何满足以下两个条件的正交矩阵 $\mathbf{Q} \in \mathbb{R}^{m \times m}$，新的变换 $\mathbf{T} = \mathbf{T}_{\text{sym}} \mathbf{Q}$ 同样有效 [@problem_id:3376057]：
1.  $\mathbf{Q}$ 是正交的，即 $\mathbf{Q}^\top \mathbf{Q} = \mathbf{I}_m$。
2.  $\mathbf{Q}$ 保持集合均值不变，这意味着它必须满足 $\mathbf{Q} \mathbf{1} = \mathbf{1}$，其中 $\mathbf{1}$ 是全一向量。

这是因为分析协方差的计算依赖于 $\mathbf{T}\mathbf{T}^\top$ 这一项：
$$
\mathbf{T}\mathbf{T}^\top = (\mathbf{T}_{\text{sym}}\mathbf{Q})(\mathbf{T}_{\text{sym}}\mathbf{Q})^\top = \mathbf{T}_{\text{sym}} \mathbf{Q} \mathbf{Q}^\top \mathbf{T}_{\text{sym}}^\top = \mathbf{T}_{\text{sym}} \mathbf{I}_m \mathbf{T}_{\text{sym}}^\top = \mathbf{T}_{\text{sym}}^2
$$
由于 $\mathbf{T}\mathbf{T}^\top$ 不变，所以最终的分析协方差也不变。而第二个条件 $\mathbf{Q} \mathbf{1} = \mathbf{1}$ 保证了分析异常的均值仍然为零，从而使分析集合的均值正确地保持为卡尔曼分析均值。

这种不确定性意味着，虽然所有合格的确定性平方根滤波器都能生成具有相同均值和协方差的分析集合，但各个集合成员的具体位置是不同的。不同的正交矩阵 $\mathbf{Q}$ 对应于将分析不确定性在集合成员之间进行不同“分配”的方式。例如，集合变换卡尔曼滤波器（ETKF）通常使用对称变换，而集合调整卡尔曼滤波器（EAKF）则采用一种不同的、旨在实现观测局域化的变换，这些都可以被视为在这个正交变换的自由度框架下的不同选择。

### 高级视角与实践考量

#### Bures-Wasserstein 几何观点

对称平方根变换 $\mathbf{T}_{\text{sym}}$ 的特殊地位可以通过信息几何的观点来理解。对称正定（SPD）矩阵的空间可以被赋予一种称为 **Bures-Wasserstein 度量**的黎曼度量。在这种度量下，两个零均值高斯分布之间的最短路径（测地线）具有明确的数学形式。

可以证明，对称平方根更新过程 $\mathbf{A}^a = \mathbf{A}^f \mathbf{T}_{\text{sym}}$ 恰好对应于将预报高斯分布 $\mathcal{N}(0, \mathbf{P}^f_N)$ 沿着 SPD 矩阵流形上的测地线，移动到分析高斯分布 $\mathcal{N}(0, \mathbf{P}^a_{\text{Kalman}})$ 的终点。变换矩阵 $\mathbf{T}_{\text{sym}}$ 本身可以被解释为从预报分布到分析分布的**最优输运映射 (optimal transport map)** [@problem_id:3376027]。其表达式为：
$$
\mathbf{T}_{\text{sym}} = (\mathbf{C}_f)^{-1/2} \left( (\mathbf{C}_f)^{1/2} \mathbf{C}_a (\mathbf{C}_f)^{1/2} \right)^{1/2} (\mathbf{C}_f)^{-1/2}
$$
其中 $\mathbf{C}_f$ 和 $\mathbf{C}_a$ 分别是预报和分析协方差。这个观点揭示了对称平方根滤波器不仅仅是代数上的权宜之计，它在几何上是最“直接”或最“经济”的更新方式。

#### 数值稳定性

在实际计算变换矩阵 $\mathbf{T}_{\text{sym}}$ 时，数值稳定性是一个关键问题。我们有两种主要方法来计算它 [@problem_id:3376010]：
1.  **特征分解法**：直接构造矩阵 $\mathbf{S}_+ = \mathbf{I}_m + \frac{1}{m-1} (\mathbf{Y}^f)^\top \mathbf{R}^{-1} \mathbf{Y}^f$，然后对其进行特征分解 $\mathbf{S}_+ = \mathbf{Q} \mathbf{\Lambda} \mathbf{Q}^\top$，最后得到 $\mathbf{T}_{\text{sym}} = \mathbf{Q} \mathbf{\Lambda}^{-1/2} \mathbf{Q}^\top$。
2.  **奇异值分解（SVD）法**：对矩阵 $\tilde{\mathbf{Y}}^f = \frac{1}{\sqrt{m-1}} \mathbf{R}^{-1/2} \mathbf{Y}^f$ 进行奇异值分解 $\tilde{\mathbf{Y}}^f = \mathbf{U} \mathbf{\Sigma} \mathbf{V}^\top$。然后可以直接在奇异值空间中构造 $\mathbf{T}_{\text{sym}}$。

当集合规模 $m$ 远大于观测维数 $p$ 时，矩阵 $(\mathbf{Y}^f)^\top \mathbf{R}^{-1} \mathbf{Y}^f$ 是低秩的，导致 $\mathbf{S}_+$ 具有许多接近于 1 的特征值。在这种情况下，直接构造并分解 $\mathbf{S}_+$ 在数值上可能不稳定，容易受到舍入误差的影响，甚至可能产生非物理的负特征值。相比之下，SVD 方法直接作用于更小的矩阵 $\tilde{\mathbf{Y}}^f$，并能更稳健地处理秩亏问题。因此，在高质量的实现中，通常推荐使用基于 SVD 的方法。

#### 有限集合效应与偏差修正

最后，必须认识到确定性平方根滤波器虽然能够精确匹配由*样本*协方差 $\mathbf{S}$ 导出的卡尔曼更新，但 $\mathbf{S}$ 本身只是真实预报方差 $p$ 的一个估计，它具有自身的统计波动。对于有限集合，$S$ 是一个随机变量，其分布服从 $\chi^2$ 分布。

分析方差的更新公式 $P^a(S) = \frac{rS}{S+r}$ 是一个关于 $S$ 的严格凹函数。根据**琴生不等式 (Jensen's inequality)**，对于任何凹函数 $f$，有 $\mathbb{E}[f(X)] \leq f(\mathbb{E}[X])$。这意味着，由样本方差计算出的分析方差的期望值，会系统性地低于由真实方差计算出的分析方差：
$$
\mathbb{E}[P^a(S)] \leq P^a(\mathbb{E}[S]) = P^a(p)
$$
通过对 $P^a(S)$ 进行二阶泰勒展开，可以推导出这种负偏差的主导项（至 $(m-1)^{-1}$ 阶）[@problem_id:3375997]：
$$
\text{Bias} = \mathbb{E}[P^a(S)] - P^a(p) \approx \frac{-2p^2 r^2}{(m-1)(p+r)^3}
$$
这个偏差是集合规模 $m$ 的反函数，在 $m$ 较小时尤为显著。它会导致滤波器系统性地低估分析不确定性，可能引发滤波器发散。

为了缓解这个问题，可以采用一种混合方法，即在应用平方根变换之前，先对样本方差 $\mathbf{S}$ 进行一次收缩修正，例如：
$$
\mathbf{S}_{\eta} = (1-\eta) \mathbf{S} + \eta \mathbf{P}_{\text{clim}}
$$
其中 $\mathbf{P}_{\text{clim}}$ 是一个更稳健的先验估计（如气候学方差 $p$），$\eta \in [0,1]$ 是一个依赖于集合大小 $m$ 的收缩参数。这种方法通过牺牲估计的无偏性来换取方差的减小，从而减小了由于非线性更新函数导致的偏差，提高了小集合下滤波器的性能。