## 引言
在原子尺度的世界里，[原子核](@entry_id:167902)的行为并非总是遵循我们熟悉的经典[牛顿定律](@entry_id:163541)。对于氢等轻元素，或在低温条件下，[零点能](@entry_id:142176)、量子隧穿和离域等[核量子效应](@entry_id:163357)（NQEs）变得至关重要，深刻影响着物质的结构、稳定性和反应性。传统的分子动力学（MD）模拟将[原子核](@entry_id:167902)视为经典粒子，因而无法捕捉这些纯粹的量子现象，导致在许多关键科学问题上预测失效。[路径积分分子动力学](@entry_id:188861)（Path Integral Molecular Dynamics, PIMD）的出现，正是为了填补这一理论与现实之间的鸿沟。它基于理查德·费曼的[路径积分表述](@entry_id:145051)，提供了一个严谨而巧妙的计算框架，将难以处理的[量子统计](@entry_id:143815)问题转化为一个等效的、可在计算机上求解的经典问题。

本文旨在系统性地介绍PIMD的理论精髓与实践应用。在“原理与机制”一章中，我们将深入探讨其理论基石——[量子-经典同构](@entry_id:201443)，揭示单个量子粒子如何转变为一个经典的环状聚合物，并讨论模拟收敛性、可观测量计算等核心技术细节。接着，在“应用与跨学科连接”一章中，我们将通过化学、物理学和[材料科学](@entry_id:152226)中的一系列实例，展示PIMD如何解释同位素效应、量化[化学反应](@entry_id:146973)中的隧穿，甚至揭示超导等复杂现象背后的量子机理。最后，“动手实践”部分将提供具体的计算练习，引导您将理论知识转化为实际的模拟技能。通过这一系列的学习，您将掌握一个连接量子理论与计算实践的强大工具，从而更深刻地理解和预测微观世界的奇妙行为。

## 原理与机制

本章在前一章“引言”的基础上，深入探讨[路径积分分子动力学](@entry_id:188861)（Path Integral Molecular Dynamics, PIMD）的理论基础和核心机制。我们将从[量子统计力学](@entry_id:140244)的基本原理出发，推导出将量子系统映射为经典[环状聚合物](@entry_id:147762)模型的数学形式，并探讨此映射的实际应用、收敛性问题、对不同[可观测量](@entry_id:267133)的高效估计方法，以及该框架下的高级扩展，如处理[全同粒子](@entry_id:142755)和近似模拟实时[量子动力学](@entry_id:138183)。

### [量子-经典同构](@entry_id:201443)：从[配分函数](@entry_id:193625)到环状聚合物

[路径积分](@entry_id:156701)方法的核心思想是将一个量子粒子的[统计力](@entry_id:194984)学问题，精确地映射为一个等价的经典体系的统计问题。这一过程始于量子[正则系综](@entry_id:142391)的[配分函数](@entry_id:193625) $Z$：

$Z = \mathrm{Tr}\left[e^{-\beta \hat{H}}\right]$

其中，$\hat{H} = \hat{T} + \hat{V}$ 是系统的[哈密顿算符](@entry_id:144286)，由[动能算符](@entry_id:265633) $\hat{T}$ 和势能算符 $\hat{V}$ 构成，$\beta = 1/(k_{\mathrm{B}} T)$ 是[逆温](@entry_id:140086)度。[算符的迹](@entry_id:185149)（Trace）运算保证了[配分函数](@entry_id:193625)对基的选取是无关的。为方便推导，我们选择在坐标表象中计算迹：

$Z = \int d\mathbf{r} \, \langle \mathbf{r} | e^{-\beta \hat{H}} | \mathbf{r} \rangle$

这里的积分遍历了系统的所有构型空间。直接计算算符指数 $e^{-\beta \hat{H}}$ 是困难的，因为 $\hat{T}$ 和 $\hat{V}$ 通常不对易（$[\hat{T}, \hat{V}] \neq 0$）。为了解决这个问题，我们利用 **Trotter 分解**（Trotter factorization）。我们将总的[虚时间传播](@entry_id:143151)步长 $\beta$ 分割成 $P$ 个小的时间片，每个时间片的长度为 $\tau = \beta/P$。于是，玻尔兹曼算符可以写成：

$e^{-\beta \hat{H}} = \left(e^{-\tau \hat{H}}\right)^P$

在 $P$ 趋于无穷大的极限下（即 $\tau \to 0$），我们可以使用对称的 Trotter-Suzuki 公式来近似处理每个短时[传播子](@entry_id:139558)：

$e^{-\tau \hat{H}} = e^{-\tau(\hat{T}+\hat{V})} \approx e^{-\tau \hat{V}/2} e^{-\tau \hat{T}} e^{-\tau \hat{V}/2} + O(\tau^3)$

这个近似的误差阶数为 $\tau^3$，对于足够大的 $P$ 是精确的。现在，我们在 $P$ 个传播子之间插入 $P-1$ 个[完备性关系](@entry_id:139077) $\hat{1} = \int d\mathbf{r} |\mathbf{r}\rangle\langle \mathbf{r}|$，[配分函数](@entry_id:193625) $Z$ 变为：

$Z = \int d\mathbf{r}_1 \int d\mathbf{r}_2 \dots \int d\mathbf{r}_P \, \langle \mathbf{r}_1 | e^{-\tau \hat{H}} | \mathbf{r}_2 \rangle \langle \mathbf{r}_2 | e^{-\tau \hat{H}} | \mathbf{r}_3 \rangle \dots \langle \mathbf{r}_P | e^{-\tau \hat{H}} | \mathbf{r}_1 \rangle$

由于迹运算的封闭性，路径的终点 $\mathbf{r}_1$ 和起点 $\mathbf{r}_1$ 是相同的，这形成了一个闭合的路径或“环”。

接下来，我们计算短时传播子的[矩阵元](@entry_id:186505) $\langle \mathbf{r}_s | e^{-\tau \hat{H}} | \mathbf{r}_{s+1} \rangle$。利用 Trotter 分解，并注意到[势能](@entry_id:748988)算符 $\hat{V}$ 在坐标表象中是对角的（即 $\hat{V}|\mathbf{r}\rangle = V(\mathbf{r})|\mathbf{r}\rangle$），我们得到：

$\langle \mathbf{r}_s | e^{-\tau \hat{H}} | \mathbf{r}_{s+1} \rangle \approx e^{-\frac{\tau}{2}(V(\mathbf{r}_s)+V(\mathbf{r}_{s+1}))} \langle \mathbf{r}_s | e^{-\tau \hat{T}} | \mathbf{r}_{s+1} \rangle$

对于一个质量为 $m$ 的单粒子，[动能算符](@entry_id:265633)为 $\hat{T} = \hat{\mathbf{p}}^2/(2m)$。其[矩阵元](@entry_id:186505)是自由粒子在虚时间中的[传播子](@entry_id:139558)，这是一个高斯函数：

$\langle \mathbf{r}_s | e^{-\tau \hat{T}} | \mathbf{r}_{s+1} \rangle = \left(\frac{m}{2\pi\hbar^2\tau}\right)^{d/2} \exp\left[-\frac{m|\mathbf{r}_s-\mathbf{r}_{s+1}|^2}{2\hbar^2\tau}\right]$

其中 $d$ 是空间的维度。将此式代回 $Z$ 的表达式，并将所有项合并，在 $P \to \infty$ 的极限下，[配分函数](@entry_id:193625) $Z$ 可以表示为一个经典体系的构型积分：

$Z \propto \int d\mathbf{r}_1 \dots d\mathbf{r}_P \, \exp\left[-\beta \sum_{s=1}^P \left( \frac{1}{2} m \omega_P^2 (\mathbf{r}_s-\mathbf{r}_{s+1})^2 + \frac{V(\mathbf{r}_s)}{P} \right)\right]$

这里我们定义了[循环边界条件](@entry_id:262709) $\mathbf{r}_{P+1} = \mathbf{r}_1$。这个表达式在形式上等价于一个经典体系的[正则配分函数](@entry_id:154330)，该体系由 $P$ 个被称为**“珠子”**（beads）的经典粒子组成。这些珠子通过谐振弹簧相互连接，形成一个**[环状聚合物](@entry_id:147762)**（ring polymer）。每个珠子 $\mathbf{r}_s$ 受到一个被缩放了 $1/P$ 的原始物理势 $V(\mathbf{r}_s)$ 的作用。连接相邻珠子的谐振弹簧的角频率 $\omega_P$ 为：

$\omega_P = \frac{P}{\beta \hbar}$

这个从单一量子粒子到经典[环状聚合物](@entry_id:147762)的映射，就是所谓的 **[量子-经典同构](@entry_id:201443)**（quantum-classical isomorphism）[@problem_id:2773360]。它构成了所有路径积分方法（包括PIMD和[路径积分蒙特卡洛](@entry_id:161651)PIMC）的理论基石。每个量子粒子都被一个由 $P$ 个珠子构成的环状聚合物所替代，珠子之间的弹簧项来源于量子动能，而物理[势能](@entry_id:748988)则作用于每个珠子上。对于[多粒子系统](@entry_id:192694)，每个量子粒子都由其自身的[环状聚合物](@entry_id:147762)表示。

### 收敛性与实际考虑

上述同构关系只有在珠子数 $P \to \infty$ 时才是精确的。在实际计算中，我们必须使用有限的 $P$ 值，因此理解收敛性行为至关重要。

#### 珠子数 $P$ 的标度关系

选择一个足够大的 $P$ 值是确保模拟结果准确性的关键。一个可靠的[收敛判据](@entry_id:158093)是，环状聚合物内部最快的[振动](@entry_id:267781)模式必须远快于系统本身的物理[振动](@entry_id:267781)模式。[环状聚合物](@entry_id:147762)的自由[振动](@entry_id:267781)正规模频率为 $\Omega_k = 2\omega_P \sin(\frac{\pi k}{P})$，其中 $k=1, \dots, P-1$。其最高频率近似为 $\Omega_{\max} \approx 2\omega_P$。如果系统物理势中存在一个最高的特征频率 $\omega_{\max}$（例如，分子内的高频伸缩[振动](@entry_id:267781)），那么为了准确描述与该频率相关的量子效应，我们需要满足条件 $2\omega_P \gg \omega_{\max}$。将 $\omega_P = P/(\beta\hbar)$ 代入，我们得到：

$\frac{2P}{\beta\hbar} \gg \omega_{\max} \implies P \gg \frac{\beta\hbar\omega_{\max}}{2}$

因此，所需的珠子数 $P$ 与 $\beta$（与温度成反比）和系统的最高物理频率 $\omega_{\max}$ 成正比 [@problem_id:2773360]。这意味着，在低温下或对于包含高频[振动](@entry_id:267781)（如水分子的O-H伸缩）的系统，需要更多的珠子才能达到收敛。

我们可以通过一个精确可解的例子——谐振子——来定量地理解收敛性。对于[角频率](@entry_id:261565)为 $\omega$ 的[量子谐振子](@entry_id:140678)，其势能的精确量子[期望值](@entry_id:153208)为：
$\langle V \rangle_{\mathrm{exact}} = \frac{1}{4}\hbar\omega\coth\left(\frac{\beta\hbar\omega}{2}\right)$

而使用 $P$ 个珠子的[路径积分](@entry_id:156701)估算值则有解析表达式：
$\langle V \rangle_{P} = \frac{1}{2\beta}\frac{\omega^{2}}{P}\sum_{k=0}^{P-1}\frac{1}{\omega_{P}^{2}\lambda_{k} + \omega^{2}/P}$
其中 $\lambda_{k} = 4 \sin^{2}(\pi k / P)$。通过比较 $\langle V \rangle_{P}$ 和 $\langle V \rangle_{\mathrm{exact}}$ 的[相对误差](@entry_id:147538) $e(P)$，我们可以确定为达到特定精度 $\varepsilon$ 所需的最小 $P$ 值 [@problem_id:2914414]。这种分析证实了上述[标度关系](@entry_id:273705)，并为实际模拟提供了选择 $P$ 的指导。

#### 时间步长的限制

在PIMD中，我们对[环状聚合物](@entry_id:147762)的经典体系进行[分子动力学模拟](@entry_id:160737)。[数值积分](@entry_id:136578)算法（如[Verlet算法](@entry_id:150873)）的稳定性取决于模拟体系中最高[振动频率](@entry_id:199185)。[环状聚合物](@entry_id:147762)的引入带来了新的高频内部[振动](@entry_id:267781)模式，其最高频率 $\Omega_{\max} \approx 2\omega_P = 2P/(\beta\hbar)$。为了保证[积分算法](@entry_id:192581)的稳定，[积分时间步长](@entry_id:162921) $\Delta t$ 必须满足 $\Delta t \lesssim 2/\Omega_{\max}$。这意味着：

$\Delta t \propto \frac{\beta\hbar}{P}$

随着珠子数 $P$ 的增加或温度的降低（$\beta$ 增大），[环状聚合物](@entry_id:147762)的内部模式变得越来越“硬”，从而要求使用更小的[积分时间步长](@entry_id:162921) [@problem_id:2452072]。这是PIMD模拟的一个重要计算成本来源，通常需要使用[多时间步](@entry_id:752313)[积分算法](@entry_id:192581)或特殊的坐标变换（如正规模或分级坐标）来缓解这一问题。

### 动力学与采样：PIMD与PIMC

[量子-经典同构](@entry_id:201443)将[量子统计](@entry_id:143815)问题转化为了对一个经典环状聚合物体系进行采样的问题。[路径积分蒙特卡洛](@entry_id:161651)（PIMC）通过[马尔可夫链蒙特卡洛方法](@entry_id:137183)在构型空间中进行采样。而[路径积分分子动力学](@entry_id:188861)（PIMD）则引入了虚构的动量，通过分子动力学方法来探索[构型空间](@entry_id:149531)。

#### PIMD的运动方程与控温需求

为了进行MD模拟，我们为每个珠子 $i$ 的每个维度引入一个虚构的动量 $\mathbf{p}_i^{(k)}$ 和一个虚构的质量 $m'_i$（通常取为物理质量 $m_i$）。环状聚合物体系的[哈密顿量](@entry_id:172864) $H_P$ 可以写为：

$H_{P} = \sum_{k=1}^{P}\sum_{i=1}^{N} \left[ \frac{(\mathbf{p}_{i}^{(k)})^{2}}{2 m'_{i}} + \frac{1}{2} m_{i}\omega_{P}^{2}\left|\mathbf{r}_{i}^{(k)}-\mathbf{r}_{i}^{(k+1)}\right|^{2} \right] + \sum_{k=1}^{P} \frac{1}{P}V\left(\mathbf{r}_{1}^{(k)}, \dots, \mathbf{r}_{N}^{(k)}\right)$

根据哈密顿力学，珠子坐标 $\mathbf{r}_{i}^{(k)}$ 和动量 $\mathbf{p}_{i}^{(k)}$ 的[运动方程](@entry_id:170720)为：

$\dot{\mathbf{r}}_{i}^{(k)} = \frac{\partial H_{P}}{\partial \mathbf{p}_{i}^{(k)}} = \frac{\mathbf{p}_{i}^{(k)}}{m'_{i}}$

$\dot{\mathbf{p}}_{i}^{(k)} = -\frac{\partial H_{P}}{\partial \mathbf{r}_{i}^{(k)}} = -m_{i}\omega_{P}^{2}\left(2 \mathbf{r}_{i}^{(k)}-\mathbf{r}_{i}^{(k-1)}-\mathbf{r}_{i}^{(k+1)}\right) - \frac{1}{P}\nabla_{\mathbf{r}_{i}^{(k)}} V(\mathbf{r}^{(k)})$

这里，力的第一项是来自相邻珠子的弹簧力，第二项是来自（按 $1/P$ 缩放的）物理势的力 [@problem_id:2659186]。

一个至关重要的概念是，由上述哈密顿方程产生的动力学（[微正则系综](@entry_id:141513)，NVE）会守恒 $H_P$ 的总能量。然而，我们的目标是采样与量子[正则系综](@entry_id:142391)对应的经典正则系综，其[概率分布](@entry_id:146404)应为 $e^{-\beta H_P}$。直接的NVE动力学无法保证生成正确的正则[分布](@entry_id:182848)。因此，**在PIMD中必须使用控温器**（thermostat），如Langevin或Nosé–Hoover链方法。控温器通过与体系[交换能](@entry_id:137069)量，确保模拟轨迹能够正确地采样相空间的正则[分布](@entry_id:182848) [@problem_id:2659186]。

#### 作为采样器的PIMD

需要强调的是，PIMD中的动力学是**虚构的**，其唯一目的是作为一种有效的采样工具，以计算**静态平衡性质**。只要控温器是各向异性的（ergodic）并且能够生成正确的正则[分布](@entry_id:182848)，那么计算出的静态平均值（如能量、结构[分布](@entry_id:182848)等）将收敛到精确的量子结果（在 $P\to\infty$ 和模拟时间足够长的极限下）。虚构的珠子质量 $m'_i$ 和控温器的参数只会影响采样的**效率**（即收敛速度和关联时间），而不会改变最终的平衡平均值 [@problem_id:2914430]。

### [可观测量](@entry_id:267133)与估计子

在获得了正确的环状聚合物构型采样后，下一步是如何从这些构型中计算[量子可观测量](@entry_id:151505)的[期望值](@entry_id:153208)。

#### 坐标依赖的[可观测量](@entry_id:267133)

对于一个仅依赖于坐标的算符 $\hat{A} = A(\hat{\mathbf{q}})$，其量子[期望值](@entry_id:153208)可以通过对所有珠子上的经典量进行平均来估计：

$\langle \hat{A} \rangle \approx \left\langle \frac{1}{P} \sum_{k=1}^P A(\mathbf{q}^{(k)}) \right\rangle_{PIMD}$

其中 $\langle \dots \rangle_{PIMD}$ 表示在PIMD模拟中对环状聚合物构型进行的系综平均。这个被称为“[热力学](@entry_id:141121)估计子”的表达式在 $P \to \infty$ 的极限下是无偏的 [@problem_id:2914430]。一个重要的结论是，在 $P \to \infty$ 极限下，任何单个珠子的位置[分布](@entry_id:182848)都收敛于精确的量子位置[概率密度](@entry_id:175496)，即 Wigner 函数的位置[边际分布](@entry_id:264862) $\int d\mathbf{p} \, W_{\beta}(\mathbf{q},\mathbf{p})$ [@problem_id:2914449]。

#### 收敛速率差异：[势能](@entry_id:748988) vs. 动能

在PIMD模拟中，一个普遍观察到的现象是，势能的[期望值](@entry_id:153208)通常比动能的[期望值](@entry_id:153208)收敛得更快，即达到同样的精度所需的珠子数 $P$ 更少。这可以通过正规模分析来理解。势能估计子 $\langle V \rangle \approx \langle \frac{1}{P}\sum_k V(\mathbf{q}_k) \rangle$ 对[环状聚合物](@entry_id:147762)的“形状”不敏感。对于一个平滑的势 $V(\mathbf{q})$，这个平均值主要由聚合物的质心位置（零频率模式）决定，而受高频内部[振动](@entry_id:267781)模式的影响较小，因为这些[高频模式](@entry_id:750297)的振幅随着 $P$ 的增加而迅速衰减（振幅平方 $\propto 1/P^2$）。

相比之下，动能与路径的“曲折度”或“扭结度”直接相关。动能估计子（如下所述）明确地依赖于珠子间的相对位移或弹簧能量，这些量对所有内部[振动](@entry_id:267781)模式都敏感，特别是那些决定路径局部曲率的[高频模式](@entry_id:750297)。由于这些[高频模式](@entry_id:750297)需要更大的 $P$ 才能被准确描述，因此动能的收敛也相应变慢 [@problem_id:2459911]。

#### 动能估计子

计算动能[期望值](@entry_id:153208) $\langle \hat{T} \rangle$ 比计算势能要复杂，存在多种估计子，它们在[统计效率](@entry_id:164796)上差异显著 [@problem_id:291745]。

1.  **原始（[热力学](@entry_id:141121)）估计子 (Primitive Estimator)**：
    $\langle \hat{T} \rangle_{\mathrm{prim}} = \frac{dN}{2\beta} - \frac{1}{2P}\sum_{i=1}^N \sum_{k=1}^P m_i \omega_P^2 \left\langle \left|\mathbf{q}_{i,k} - \mathbf{q}_{i,k+1}\right|^2 \right\rangle$
    该估计子是经典动能与平均弹簧[势能](@entry_id:748988)之差。它虽然形式简单且不需计算物理力的导数，但其[方差](@entry_id:200758)随 $P$ [线性增长](@entry_id:157553)，[统计效率](@entry_id:164796)很差。

2.  **维里（Virial）估计子 (Virial Estimator)**：
    $\langle \hat{T} \rangle_{\mathrm{vir}} = \frac{dN}{2\beta} + \frac{1}{2P}\sum_{i=1}^N \sum_{k=1}^P \left\langle \mathbf{q}_{i,k} \cdot \mathbf{F}_{i,k} \right\rangle$
    其中 $\mathbf{F}_{i,k}$ 是作用在珠子 $k$ 上的物理力。该估计子的[方差](@entry_id:200758)不随 $P$ 发散，在统计上远优于原始估计子。但对于非束缚体系（如气相分子），珠子坐标 $\mathbf{q}_{i,k}$ 会随[质心](@entry_id:265015)漂移，导致大的涨落。

3.  **[质心](@entry_id:265015)-维里（Centroid-Virial）估计子 (Centroid-Virial Estimator)**：
    $\langle \hat{T} \rangle_{\mathrm{cv}} = \frac{dN}{2\beta} + \frac{1}{2P}\sum_{i=1}^N \sum_{k=1}^P \left\langle \left(\mathbf{q}_{i,k}-\bar{\mathbf{q}}_i\right) \cdot \mathbf{F}_{i,k} \right\rangle$
    其中 $\bar{\mathbf{q}}_i$ 是粒子 $i$ 的[环状聚合物](@entry_id:147762)的[质心](@entry_id:265015)。通过减去[质心](@entry_id:265015)坐标，该估计子只依赖于[环状聚合物](@entry_id:147762)相对于其自身中心的内部构型。这消除了质心漂移带来的问题，使其对于束缚和非束缚体系都具有良好的[统计效率](@entry_id:164796)（[方差](@entry_id:200758)与 $P$ 无关）。这使其成为实践中最常用和最鲁棒的动能估计子。

### 高级主题与扩展

PIMD框架可以被扩展以处理更复杂的物理现象。

#### 全同粒子与交换效应

当系统包含全同粒子（如多个质子或电子）时，量子力学的不可区分性原理要求[波函数](@entry_id:147440)（或密度矩阵）具有特定的[交换对称性](@entry_id:151892)。对于[玻色子](@entry_id:138266)，交换任意两个粒子，[波函数](@entry_id:147440)不变；对于[费米子](@entry_id:146235)，[波函数](@entry_id:147440)反号。在[路径积分](@entry_id:156701)形式中，这表现为需要对所有 $N!$ 个粒子标签的[排列](@entry_id:136432) $P$ 进行求和：

$Z = \frac{1}{N!} \sum_{P} (\sigma_P)^s \int d\mathbf{R} \langle \mathbf{R} | e^{-\beta \hat{H}} | P\mathbf{R} \rangle$

其中 $s=0$ 对应[玻色子](@entry_id:138266)， $s=1$ 对应[费米子](@entry_id:146235)，$\sigma_P$ 是[排列](@entry_id:136432)的奇偶性。路径积分的边界条件变为 $\mathbf{r}_i(\beta) = \mathbf{r}_{P(i)}(0)$。这意味着[环状聚合物](@entry_id:147762)可以连接不同的粒子，形成跨越多个粒子的**[排列](@entry_id:136432)循环**（permutation cycles） [@problem_id:2914426]。

-   **[玻色子](@entry_id:138266)**：所有[排列](@entry_id:136432)的贡献都是正的，因此路径积分的权重非负。采样可以包含聚合物的连接和断开（对应不同的[排列](@entry_id:136432)循环），这虽然增加了构型空间的复杂性，但没有根本性的“[符号问题](@entry_id:155213)”。
-   **[费米子](@entry_id:146235)**：奇数[排列](@entry_id:136432)的贡献为负，导致路径积分的被积函数符号交替。这导致了著名的**[费米子符号问题](@entry_id:144472)**，即[配分函数](@entry_id:193625)表现为两个几乎相等的大数之差，导致[统计误差](@entry_id:755391)随粒子数 $N$ 或 $\beta$ 的增加呈指数级增长，使得模拟极其困难。

需要注意的是，交换效应的重要性取决于[热德布罗意波长](@entry_id:143992)与粒子间平均距离的比值。对于[轻核](@entry_id:751275)（如氢），即使在室温下，该效应也可能不可忽略，尤其是在高密度环境中 [@problem_id:2914426]。

#### 从虚时间到实时间：RPMD与CMD

虽然PIMD的动力学是虚构的，但其背后的[环状聚合物](@entry_id:147762)[哈密顿量](@entry_id:172864) $H_P$ 催生了近似模拟**实时**[量子动力学](@entry_id:138183)的方法。

-   **[环状聚合物分子动力学](@entry_id:147033) (RPMD)**：RPMD 的核心假设是，由 $H_P$ 生成的经典[哈密顿动力学](@entry_id:156273)可以近似真实的[量子动力学](@entry_id:138183)。具体而言，它被用来计算 Kubo 变换形式的[时间相关函数](@entry_id:144636)。在RPMD中，系统首先通过控温的PIMD进行平衡，以从[正则系综](@entry_id:142391)中抽取初始构型和动量。然后，**关闭控温器**，在微正则（NVE）系综下演化轨迹，并在此轨迹上计算[时间相关函数](@entry_id:144636)。在[演化过程](@entry_id:175749)中施加控温会破坏其理论基础并引入偏差 [@problem_id:2921724]。

-   **[质心分子动力学](@entry_id:186883) (CMD)**：CMD是另一种近似方法，它假设系统的[量子动力学](@entry_id:138183)主要由环状聚合物的[质心运动](@entry_id:178374)来体现。质心在一个由其他珠子积分掉后产生的有效势（[平均力势](@entry_id:137947)）上运动。标准CMD在描述非[绝热过程](@entry_id:138150)（如电子转移）时存在局限，因为它本质上是在单一的平均[势能面](@entry_id:147441)上运动，无法描述电子态之间的跃迁和相干性 [@problem_id:2793591]。

这些实时方法的共同挑战是，[环状聚合物](@entry_id:147762)的内部模式可能与系统的物理[振动](@entry_id:267781)发生[伪共振](@entry_id:755262)，在谱学计算中产生伪峰。一种称为**恒温RPMD** (Thermostatted RPMD, [TRPMD](@entry_id:756189)) 的实用技术通过在[演化过程](@entry_id:175749)中仅对内部模式施加控温来抑制这些伪峰，但这会以牺牲部分短时动力学的准确性为代价 [@problem_id:2921724]。

#### [非绝热动力学](@entry_id:189808)

将PIMD框架扩展到包含多个电子态的非绝热系统是一个活跃的研究领域。这通常通过将离散的电子态映射到连续的经典自由度（例如，使用Meyer-Miller-Stock-Thoss (MMST) 映射）来实现，然后对核坐标和这些映射变量同时进行路径积分处理。然而，这些方法也面临挑战，包括前面提到的[伪共振](@entry_id:755262)问题，以及经典的映射变量与核自由度之间可能发生的非物理能量交换，即**[零点能泄漏](@entry_id:188364)**（zero-point energy leakage）问题，这可能导致动力学的严重错误 [@problem_id:2793591]。