## 引言
[经典密度泛函理论](@entry_id:169942)（cDFT）是[物理化学](@entry_id:145220)和[软物质物理](@entry_id:145473)领域的一块基石，为我们提供了一个从微观粒子相互作用出发，精确描述[非均匀流体](@entry_id:187276)结构与[热力学性质](@entry_id:146047)的强大理论框架。从容器壁附近的液体分层，到[多孔材料](@entry_id:152752)内的[毛细凝聚](@entry_id:146904)，再到新相的成核生长，这些现象的共性在于流体密度的空间不均匀性。如何建立一个能够跨越从[分子尺](@entry_id:166706)度到宏观尺度的桥梁，定量预测这些复杂行为，正是cDFT旨在解决的核心问题。

本文将系统地引导读者深入cDFT的世界。我们将从第一章“原理与机制”开始，揭示其赖以建立的[变分原理](@entry_id:198028)和[亥姆霍兹自由能](@entry_id:136442)泛函的深刻内涵。随后，在第二章“应用与交叉学科联系”中，我们将展示该理论在解释[润湿](@entry_id:147044)、成核、[临界现象](@entry_id:144727)等多样化物理问题中的强大威力，并探讨其与[材料科学](@entry_id:152226)、化学工程等领域的联系。最后，在第三章“动手实践”部分，我们将通过具体的计算问题，将理论知识转化为解决实际问题的能力。通过这趟由理论基础到前沿应用的旅程，读者将全面掌握cDFT的核心思想和研究方法，并能将其应用于自己的研究领域。

## 原理与机制

[经典密度泛函理论](@entry_id:169942)（Classical Density Functional Theory, cDFT）为我们提供了一个强大而严谨的框架，用以在[分子尺](@entry_id:166706)度上理解和预测[非均匀流体](@entry_id:187276)的结构与[热力学性质](@entry_id:146047)。其核心思想是，系统的所有平衡性质都可以通过空间依赖的[单体](@entry_id:136559)数密度[分布](@entry_id:182848) $n(\mathbf{r})$ 来唯一确定。本章将深入探讨支撑这一理论的基本原理，并阐述构建实用密度泛函模型的关键机制。

### 变分原理与[巨势泛函](@entry_id:144711)

[经典密度泛函理论](@entry_id:169942)的基石是一个普适的变分原理。该原理指出，对于一个处于由温度 $T$、化学势 $\mu$ 和外部[势场](@entry_id:143025) $v_{\text{ext}}(\mathbf{r})$ 所确定的[热力学状态](@entry_id:755916)的流体，其平衡密度[分布](@entry_id:182848) $n_{\text{eq}}(\mathbf{r})$ 是使**[巨势泛函](@entry_id:144711)** $\Omega[n]$ 达到最小值的那个密度[分布](@entry_id:182848)。这个泛函是[单体](@entry_id:136559)[数密度](@entry_id:268986) $n(\mathbf{r})$ 的函数，其一般形式为 [@problem_id:2763879]：

$$
\Omega_v[n] = F[n] + \int n(\mathbf{r})\big(v_{\text{ext}}(\mathbf{r}) - \mu\big) d\mathbf{r}
$$

这个表达式由两部分构成。第一部分是**本征[亥姆霍兹自由能](@entry_id:136442)泛函** $F[n]$，它包含了流体内在的所有性质，例如粒子间的相互作用和熵效应。第二部分 $\int n(\mathbf{r})(v_{\text{ext}}(\mathbf{r}) - \mu) d\mathbf{r}$ 描述了流体与外部环境的耦合。具体来说，$\int n(\mathbf{r})v_{\text{ext}}(\mathbf{r})d\mathbf{r}$ 是粒子在外部[势场](@entry_id:143025)中的总势能，而 $-\int n(\mathbf{r})\mu d\mathbf{r}$ 则反映了系统与一个粒子和能量水库（由化学势 $\mu$ 表征）交换粒子所引起的自由能变化。

### 普适的[亥姆霍兹自由能](@entry_id:136442)泛函

[密度泛函理论](@entry_id:139027)的核心和威力在于 $F[n]$ 的**普适性**（universality）。对于一个给定的流体（即粒子间的相互作用势 $u(|\mathbf{r}-\mathbf{r}'|)$ 和温度 $T$ 已确定），$F[n]$ 的形式是唯一的，它**不依赖于**作用在系统上的任何外部势场 $v_{\text{ext}}(\mathbf{r})$ [@problem_id:2763879]。这意味着，一旦我们为某一特定流体找到了一个精确或足够准确的 $F[n]$，就可以用它来研究该流体在**任何**外部势场下的行为，无论是容器壁、[胶体](@entry_id:147501)颗粒还是其他外[力场](@entry_id:147325)。

为了便于分析和建模，本征亥姆霍兹自由能泛函 $F[n]$ 通常被分解为两部分：

$$
F[n] = F_{\text{id}}[n] + F_{\text{ex}}[n]
$$

其中，$F_{\text{id}}[n]$ 是**[理想气体](@entry_id:200096)[自由能泛函](@entry_id:184428)**。它描述了一个由无相互作用的粒子组成的、具有相同非均匀密度[分布](@entry_id:182848) $n(\mathbf{r})$ 的[参考系](@entry_id:169232)统的自由能。这个泛函具有精确的、已知的形式 [@problem_id:2763879]：

$$
F_{\text{id}}[n] = k_B T \int n(\mathbf{r})\left[\ln\big(n(\mathbf{r}) \Lambda^{3}\big)-1\right] d\mathbf{r}
$$

这里的 $k_B$ 是[玻尔兹曼常数](@entry_id:142384)，$\Lambda$ 是[热德布罗意波长](@entry_id:143992)（$\Lambda = h/\sqrt{2\pi m k_B T}$），它包含了粒子的量子统计起源，即使在[经典极限](@entry_id:148587)下也需保留。这个表达式本质上是对应于密度[分布](@entry_id:182848) $n(\mathbf{r})$ 的理想气体熵的积分。

另一部分，$F_{\text{ex}}[n]$，被称为**超额[自由能泛函](@entry_id:184428)**。它包含了所有由于粒子间相互作用而产生的非理想效应，是[经典密度泛函理论](@entry_id:169942)中最为复杂和关键的部分。正是 $F_{\text{ex}}[n]$ 决定了流体的[相行为](@entry_id:199883)、[界面现象](@entry_id:167796)和微观结构。由于粒子间相互作用的复杂性，$F_{\text{ex}}[n]$ 的精确形式对于大多数系统来说是未知的。因此，发展和选择合适的**近似**超额[自由能泛函](@entry_id:184428)，是cDFT研究的核心任务。

### 欧拉-拉格朗日方程：求解平衡密度

根据变分原理，平衡密度 $n_{\text{eq}}(\mathbf{r})$ 使得[巨势泛函](@entry_id:144711) $\Omega[n]$ 取最小值。在数学上，这意味着 $\Omega[n]$ 对 $n(\mathbf{r})$ 的一阶泛函变分（functional variation）在 $n = n_{\text{eq}}$ 处为零。对于任意一个密度 $n(\mathbf{r})$，其一阶泛函变分可以写作：

$$
\delta\Omega[n] = \int \frac{\delta \Omega[n]}{\delta n(\mathbf{r})} \delta n(\mathbf{r}) d\mathbf{r}
$$

其中 $\frac{\delta \Omega[n]}{\delta n(\mathbf{r})}$ 是泛函导数。为了使 $\delta\Omega$ 对任意微小的密度变化 $\delta n(\mathbf{r})$ 都为零，其泛函导数必须处处为零。我们对[巨势泛函](@entry_id:144711)的各项求泛函导数 [@problem_id:2763936]：

$$
\frac{\delta \Omega[n]}{\delta n(\mathbf{r})} = \frac{\delta F[n]}{\delta n(\mathbf{r})} + v_{\text{ext}}(\mathbf{r}) - \mu = 0
$$

这就是**[欧拉-拉格朗日方程](@entry_id:137827)**。我们可以定义一个依赖于密度的**本征化学势** $\mu_{\text{int}}[n](\mathbf{r}) \equiv \frac{\delta F[n]}{\delta n(\mathbf{r})}$，于是[欧拉-拉格朗日方程](@entry_id:137827)可以写成一个更具物理直观的形式：

$$
\mu_{\text{int}}[n](\mathbf{r}) + v_{\text{ext}}(\mathbf{r}) = \mu
$$

这个方程的物理意义是：在平衡状态下，系统中每一点的**总化学势**（由流体内部相互作用产生的本征部分和由外部环境施加的外部势之和）都必须等于粒子水库的化学势 $\mu$，即在整个系统中保持恒定。

将 $F[n]$ 分解为理想和超额部分，并代入[欧拉-拉格朗日方程](@entry_id:137827)，我们可以得到一个关于平衡密度 $n(\mathbf{r})$ 的[自洽方程](@entry_id:155949)。首先，我们定义**[超额化学势](@entry_id:749151)** $\mu_{\text{ex}}[n](\mathbf{r}) \equiv \frac{\delta F_{\text{ex}}[n]}{\delta n(\mathbf{r})}$。利用 $F_{\text{id}}[n]$ 的精确形式，我们有 $\frac{\delta F_{\text{id}}[n]}{\delta n(\mathbf{r})} = k_B T \ln(n(\mathbf{r})\Lambda^3)$。于是，[欧拉-拉格朗日方程](@entry_id:137827)变为：

$$
k_B T \ln(n(\mathbf{r})\Lambda^3) + \mu_{\text{ex}}[n](\mathbf{r}) + v_{\text{ext}}(\mathbf{r}) = \mu
$$

求解这个方程，我们可以得到平衡密度的表达式 [@problem_id:2763890]：

$$
n(\mathbf{r}) = \frac{1}{\Lambda^{3}} \exp\left( \frac{\mu - v_{\text{ext}}(\mathbf{r}) - \mu_{\text{ex}}[n](\mathbf{r})}{k_B T} \right)
$$

这个方程形式优美且富有洞察力。它表明，在给定位置的粒子密度由一个类[玻尔兹曼分布](@entry_id:142765)决定，其能量项不仅包含外部势能 $v_{\text{ext}}(\mathbf{r})$，还包含了一个由周围所有其他粒子共同作用产生的有效势场——[超额化学势](@entry_id:749151) $\mu_{\text{ex}}[n](\mathbf{r})$。由于 $\mu_{\text{ex}}$ 本身依赖于整个密度[分布](@entry_id:182848) $n(\mathbf{r})$，这是一个高度[非线性](@entry_id:637147)的[自洽方程](@entry_id:155949)，通常需要通过迭代方法求解。

### 与宏观[热力学](@entry_id:141121)的联系

一个成功的微观理论必须能够在适当的极限下回归到已知的宏观[热力学](@entry_id:141121)。对于[经典密度泛函理论](@entry_id:169942)，我们可以通过考虑一个没有外场（$v_{\text{ext}}=0$）的宏观均匀流体来检验其[自洽性](@entry_id:160889)。在这种情况下，由于[平移对称性](@entry_id:171614)，平衡密度必然是一个常数，即 $n(\mathbf{r}) = \rho_b$。

此时，[亥姆霍兹自由能](@entry_id:136442)泛函退化为一个普通的函数，与体积 $V$ 成正比：$F[n=\rho_b] = V f(\rho_b, T)$，其中 $f(\rho_b, T)$ 是单位体积的亥姆霍兹自由能密度。欧拉-拉格朗日方程也相应简化。本征化学势变为 $\mu_{\text{int}}(\rho_b) = \frac{\partial f(\rho_b, T)}{\partial \rho_b}$。因此，平衡条件 $\mu_{\text{int}}[n] = \mu$ 就变成了标准的[热力学](@entry_id:141121)关系 $\mu = \frac{\partial f}{\partial \rho_b}$，它隐式地定义了给定化学势 $\mu$ 下的平衡体相密度 $\rho_b$。

将平衡密度 $\rho_b$ 代入[巨势泛函](@entry_id:144711)的表达式中，我们可以得到平衡态的[巨势](@entry_id:136286) $\Omega_{\text{eq}}$ [@problem_id:2763952]：

$$
\Omega_{\text{eq}} = V f(\rho_b, T) - \mu \int \rho_b d\mathbf{r} = V (f(\rho_b, T) - \mu \rho_b)
$$

利用标准的[热力学关系式](@entry_id:139032)（[欧拉关系](@entry_id:180356)）$p = \mu \rho_b - f(\rho_b, T)$，其中 $p$ 是体相压力，我们最终得到一个非常简洁和重要的结果：

$$
\Omega_{\text{eq}} = -pV
$$

这个结果表明，[密度泛函理论](@entry_id:139027)的[巨势泛函](@entry_id:144711)在均匀极限下正确地还原为宏观[热力学](@entry_id:141121)中的[巨势](@entry_id:136286)。这一联系不仅证明了理论的内在一致性，也为从微观的[自由能泛函](@entry_id:184428)计算宏观热力学性质（如压力和相图）提供了途径。

### 流体结构与稳定性：[直接关联函数](@entry_id:158301)

超额[自由能泛函](@entry_id:184428) $F_{\text{ex}}[n]$ 不仅决定了系统的能量，还蕴含了关于流体微观结构的深刻信息。这些信息可以通过 $F_{\text{ex}}[n]$ 的高阶泛函导数来揭示。其中最重要的是二阶泛函导数，它定义了**[直接关联函数](@entry_id:158301)**（direct correlation function）$c^{(2)}(\mathbf{r}, \mathbf{r}')$ [@problem_id:2763928]：

$$
\frac{\delta^2 F_{\text{ex}}[n]}{\delta n(\mathbf{r}) \delta n(\mathbf{r}')} \equiv -k_B T c^{(2)}(\mathbf{r}, \mathbf{r}'; [n])
$$

$c^{(2)}(\mathbf{r}, \mathbf{r}')$ 描述了在位置 $\mathbf{r}'$ 的密度微小变化如何通过粒子间的相互作用影响到位置 $\mathbf{r}$ 的[超额化学势](@entry_id:749151)。对于一个均匀流体，由于平移和[旋转不变性](@entry_id:137644)，$c^{(2)}$ 只依赖于两点间的距离，记作 $c^{(2)}(|\mathbf{r}-\mathbf{r}'|)$。

[直接关联函数](@entry_id:158301)的重要性体现在它与[流体稳定性](@entry_id:268315)的联系上。我们可以通过在均匀密度 $\rho_b$ 附近对[巨势泛函](@entry_id:144711)进行泛函泰勒展开来研究这一点。展开到二阶，密度涨落 $\delta n(\mathbf{r}) = n(\mathbf{r}) - \rho_b$ 引起的[巨势](@entry_id:136286)变化为 [@problem_id:2763928]：

$$
\Delta\Omega^{(2)}[\delta n] = \frac{k_B T}{2} \iint d\mathbf{r} d\mathbf{r}' \left[ \frac{\delta(\mathbf{r}-\mathbf{r}')}{\rho_b} - c^{(2)}(|\mathbf{r}-\mathbf{r}'|) \right] \delta n(\mathbf{r}) \delta n(\mathbf{r}')
$$

为了更清晰地看到其物理意义，我们切换到傅里叶空间。上式可以写成：

$$
\Delta\Omega^{(2)}[\delta n] = \frac{k_B T}{2} \int \frac{d\mathbf{k}}{(2\pi)^3} \left[ \frac{1}{\rho_b} - \hat{c}^{(2)}(k) \right] |\delta n_{\mathbf{k}}|^2
$$

其中 $\delta n_{\mathbf{k}}$ 和 $\hat{c}^{(2)}(k)$ 分别是[密度涨落](@entry_id:143540)和[直接关联函数](@entry_id:158301)的[傅里叶变换](@entry_id:142120)。在[液体理论](@entry_id:152493)中，著名的 Ornstein-Zernike 关系将 $\hat{c}^{(2)}(k)$ 与可直接通过[散射实验](@entry_id:173304)测量的**[静态结构因子](@entry_id:141682)** $S(k)$ 联系起来：

$$
S(k) = \frac{1}{1 - \rho_b \hat{c}^{(2)}(k)}
$$

将此关系代入，我们得到一个极其重要的表达式：

$$
\Delta\Omega^{(2)}[\delta n] = \frac{k_B T}{2\rho_b} \int \frac{d\mathbf{k}}{(2\pi)^3} \frac{1}{S(k)} |\delta n_{\mathbf{k}}|^2
$$

为了使均匀流体状态是[热力学](@entry_id:141121)稳定的（即[巨势](@entry_id:136286)是局部最小值），对任何小的密度涨落，$\Delta\Omega^{(2)}$ 都必须是正的。这意味着，对于所有的[波矢](@entry_id:178620) $k$，我们必须有 $S(k) > 0$。[静态结构因子](@entry_id:141682) $S(k)$ 描述了波矢为 $k$ 的密度涨落的平均振幅。当系统接近一个[相变](@entry_id:147324)点时（例如气液[临界点](@entry_id:144653)），长波长的密度涨落会急剧增大，表现为 $S(k \to 0) \to \infty$。此时，抵抗这种涨落的“恢复力” $1/S(0)$ 趋于零，系统变得不稳定，表明二阶展开失效，高阶项变得至关重要。

### [线性响应理论](@entry_id:145737)

上述分析不仅关系到稳定性，也为我们理解流体如何响应外部扰动提供了基础，这就是**[线性响应理论](@entry_id:145737)**。考虑一个[均匀流](@entry_id:272775)体受到一个微弱的外部势场 $\delta v_{\text{ext}}(\mathbf{r})$ 的扰动。它会引起一个微小的线性密度响应 $\delta n(\mathbf{r})$。通过对欧拉-拉格朗日方程进行线性化，可以推导出密度响应和外场之间的关系 [@problem_id:2763905]：

$$
\delta n(\mathbf{r}) = \int d\mathbf{r}' \chi(\mathbf{r}-\mathbf{r}') \big(-\delta v_{\text{ext}}(\mathbf{r}')\big)
$$

这里的 $\chi(\mathbf{r}-\mathbf{r}')$ 是**[线性响应函数](@entry_id:160418)**或**磁化率**，它描述了在 $\mathbf{r}'$ 处的点状扰动如何在 $\mathbf{r}$ 处引起密度变化。这个卷积关系在傅里叶空间中变成了简单的乘法关系：

$$
\delta \tilde{n}(k) = \tilde{\chi}(k) \big(-\delta \tilde{v}_{\text{ext}}(k)\big)
$$

通过线性化欧拉-拉格朗日方程并利用 Ornstein-Zernike 关系，可以推导出 $\tilde{\chi}(k)$ 的一个精确表达式：

$$
\tilde{\chi}(k) = \frac{\rho_b S(k)}{k_B T}
$$

这个关系是涨落-耗散定理的一个体现。它优雅地揭示了一个深刻的物理原理：系统对外部扰动的响应（由 $\tilde{\chi}(k)$ 描述）与其内部自发的[热涨落](@entry_id:143642)（由 $S(k)$ 描述）直接相关。一个具有强烈内部涨落的模式（大的 $S(k)$）也最容易被相应[波矢](@entry_id:178620)的外部[势场](@entry_id:143025)所激发。

### 超额[自由能泛函](@entry_id:184428)的近似方法

理论的基石已经奠定，但我们面临着一个核心的实践挑战：$F_{\text{ex}}[n]$ 的具体形式是未知的。cDFT 的大部分研究工作都致力于发展和完善对 $F_{\text{ex}}[n]$ 的近似。下面我们介绍几种关键的近似策略。

#### [局域密度近似](@entry_id:138982)

最简单、最直观的近似是**[局域密度近似](@entry_id:138982)**（Local Density Approximation, [LDA](@entry_id:138982)）。LDA 的核心假设是，空间中某一点 $\mathbf{r}$ 的超额自由能密度只依赖于该点**局域**的粒子密度 $n(\mathbf{r})$。它将[均匀流](@entry_id:272775)体的[热力学性质](@entry_id:146047)“借用”到非均匀系统中：

$$
F_{\text{ex}}^{\text{LDA}}[n] = \int f_{\text{ex}}^{\text{hom}}(n(\mathbf{r})) d\mathbf{r}
$$

其中 $f_{\text{ex}}^{\text{hom}}(n)$ 是密度为 $n$ 的**均匀**流体的单位体积超额自由能，这是一个已知的、可以通过理论（如积分方程）或模拟得到的函数 [@problem_id:2763916]。例如，对于硬球流体，可以利用精确的 Carnahan-Starling [状态方程](@entry_id:274378)来积分得到 $f_{\text{ex}}^{\text{hom}}(n)$。

LDA 的优点是构造简单，并且能保证在均匀极限下正确地再现输入的[状态方程](@entry_id:274378)，满足基本的[热力学一致性](@entry_id:138886)。然而，它的物理图像是简化的，忽略了粒子间相互作用的有限程（range）所导致的[非局域关联](@entry_id:180194)效应。当密度变化梯度较大时（例如在[固液界面](@entry_id:201674)），[LDA](@entry_id:138982) 的预测通常不准确。

#### 非局域泛函与加权密度

为了超越 LDA 并描述粒子间的空间关联，我们需要构建**非局域**（non-local）泛函。一种强大而系统的方法是通过**加权密度**（weighted densities）来实现。其思想是，在点 $\mathbf{r}$ 的自由能密度不应只依赖于 $n(\mathbf{r})$，而应依赖于其周围一个邻域内的平均密度。这种平均是通过将密度场 $n(\mathbf{r})$ 与一个**权函数**（weight function）$w(\mathbf{r})$ 进行卷积得到的：

$$
\bar{n}(\mathbf{r}) = \int n(\mathbf{r}') w(\mathbf{r}-\mathbf{r}') d\mathbf{r}'
$$

这种卷积操作可以通过高效的快速傅里叶变换（FFT）算法来计算 [@problem_id:2629211]。超额[自由能泛函](@entry_id:184428)则被近似为这些加权密度的局域函数：

$$
F_{\text{ex}}[n] \approx \int \Phi\big(\{\bar{n}_\alpha(\mathbf{r})\}\big) d\mathbf{r}
$$

其中 $\{\bar{n}_\alpha\}$ 是一组通过不同权函数 $w_\alpha$ 计算得到的加权密度。

这一方法的巅峰之作是 Rosenfeld 提出的**基本度量理论**（Fundamental Measure Theory, FMT）[@problem_id:2629201]。FMT 专门为硬球流体设计，其权函数 $w_\alpha$ 精巧地与单个球体的基本几何度量（体积、表面积、曲率等）相联系。通过这种几何构造，FMT 泛函不仅在均匀极限下能再现非常精确的硬球[状态方程](@entry_id:274378)（例如 Percus-Yevick 方程），而且能够极其准确地描述硬球在极度受限空间中的复杂堆积行为和[相变](@entry_id:147324)，远超 LDA 和其他早期理论。FMT 的成功使其成为现代 cDFT 中处理硬排斥相互作用的标准工具。

#### 真实流体的微扰方法

真实流体的相互作用势通常比硬球复杂，例如 Lennard-Jones (LJ) 势，它既包含短程的强排斥，也包含长程的吸引。直接为这样的势构建一个精确的泛函非常困难。一种非常成功且广泛应用的策略是采用**[微扰理论](@entry_id:138766)**的思想 [@problem_id:2763951]。

这个方法的第一步是**分解**相互作用势 $u(r)$。一个经典方案是 **Weeks-Chandler-Andersen (WCA)** 分解，它将势在能量最低点 $r_m$ 处分割成一个纯排斥的参考部分 $u_{\text{rep}}(r)$ 和一个纯吸引的微扰部分 $u_{\text{att}}(r)$：

$$
u(r) = u_{\text{rep}}(r) + u_{\text{att}}(r)
$$

接下来，超额[自由能泛函](@entry_id:184428)也相应地被近似为两部分的和：

$$
F_{\text{ex}}[n] \approx F_{\text{ex}}^{\text{ref}}[n] + F_{\text{ex}}^{\text{pert}}[n]
$$

- **参考部分** $F_{\text{ex}}^{\text{ref}}[n]$：排斥部分 $u_{\text{rep}}(r)$ 通常是“软”的，但其行为主导了流体的结构。因此，它需要被精确处理。一种标准做法是将其映射到一个等效的硬球系统上，硬球的[有效直径](@entry_id:748809) $d(T)$ 根据某种准则（如 Barker-Henderson 准则）由 $u_{\text{rep}}(r)$ 和温度 $T$ 决定。然后，使用像 FMT 这样高质量的硬球泛函来计算 $F_{\text{ex}}^{\text{ref}}[n] \approx F_{\text{ex}}^{\text{HS}}[n; d(T)]$。

- **微扰部分** $F_{\text{ex}}^{\text{pert}}[n]$：长程的吸引部分 $u_{\text{att}}(r)$ 变化较为平缓，对它的处理可以采用更简单的近似。最常用的就是**[平均场近似](@entry_id:144121)**（mean-field approximation），它忽略了吸引作用下的[密度涨落](@entry_id:143540)关联：

$$
F_{\text{ex}}^{\text{pert}}[n] \approx \frac{1}{2} \iint n(\mathbf{r}) n(\mathbf{r}') u_{\text{att}}(|\mathbf{r}-\mathbf{r}'|) d\mathbf{r} d\mathbf{r}'
$$

这个平均场项是一个非局域的卷积项，描述了流体中所有粒子对之间的长程吸引能。综合起来，一个适用于 Lennard-Jones 流体的完整 cDFT 模型就构建完成了。它结合了处理排斥的几何精确性和处理吸引的物理直观性，为研究真实流体的界面、润湿和[成核](@entry_id:140577)等复杂现象提供了强大的理论工具。

### 推广至多组分体系

上述理论框架可以自然地推广到包含 $M$ 个组分的**混合物**体系 [@problem_id:2763890]。在这种情况下，系统状态由一组密度[分布](@entry_id:182848) $\{n_i(\mathbf{r})\}_{i=1}^M$、一组化学势 $\{\mu_i\}$ 和一组外部势 $\{v_i(\mathbf{r})\}$ 来描述。

[巨势泛函](@entry_id:144711)的形式与单组分情况类似，只是需要对所有组分进行求和：

$$
\Omega[\{n_i\}] = F[\{n_i\}] + \sum_{i=1}^{M} \int n_i(\mathbf{r})\big( v_i(\mathbf{r}) - \mu_i \big) d\mathbf{r}
$$

亥姆霍兹自由能泛函 $F[\{n_i\}]$ 现在依赖于所有组分的密度[分布](@entry_id:182848)，并同样可以分解为理想部分和超额部分。[理想气体](@entry_id:200096)项是各组分[理想气体](@entry_id:200096)自由能的简单加和。超额部分 $F_{\text{ex}}[\{n_i\}]$ 则包含了所有组分内和组分间的相互作用，变得更加复杂。

应用[变分原理](@entry_id:198028)，我们对每个组分的密度 $n_j(\mathbf{r})$ 分别求泛函导数并令其为零，从而得到一套**耦合的欧拉-拉格朗日方程**：

$$
k_B T \ln(n_j(\mathbf{r})\Lambda_j^3) + \mu_{j,\text{ex}}[\{n_i\}](\mathbf{r}) + v_j(\mathbf{r}) = \mu_j, \quad \text{for } j=1, \dots, M
$$

其中，**偏[超额化学势](@entry_id:749151)** $\mu_{j,\text{ex}}$ 定义为对整个超额泛函求关于组分 $j$ 的密度 $n_j$ 的泛函导数：

$$
\mu_{j,\text{ex}}[\{n_i\}](\mathbf{r}) \equiv \frac{\delta F_{\text{ex}}[\{n_i\}]}{\delta n_j(\mathbf{r})}
$$

这套耦合的[自洽方程](@entry_id:155949)必须被同时求解，以获得所有组分的平衡密度[分布](@entry_id:182848)。虽然在数学上更为复杂，但其基本物理原理和建模策略（如 [LDA](@entry_id:138982)、FMT、微扰理论）都可以从单组分体系继承和发展，使其成为研究合金、[胶体](@entry_id:147501)混合物、生物大分子溶液等[复杂流体](@entry_id:198415)体系的有力工具。