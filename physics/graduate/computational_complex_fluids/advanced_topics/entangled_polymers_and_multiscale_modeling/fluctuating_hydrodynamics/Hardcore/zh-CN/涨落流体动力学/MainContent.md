## 引言
在物理学的广阔图景中，涨落流体力学（Fluctuating Hydrodynamics）扮演着连接微观世界无序热运动与宏观世界确定性流动规律的独特桥梁。传统的流体力学，如纳维-斯托克斯（Navier-Stokes）方程，成功地描述了我们日常经验中的流体行为，但这些确定性方程在尺度缩小至微米或纳米级别时便显现出局限性。在这些介观尺度上，由分子碰撞引起的热涨落不再能被忽略，它们成为系统动力学中不可或缺的一部分，驱动着布朗运动、影响着化学反应速率，并主导着微纳器件中的输运过程。

本文旨在系统性地介绍涨落流体力学这一强大的理论框架，填补纯微观统计力学与宏观连续介质力学之间的知识鸿沟。我们将揭示，如何通过一种物理上自洽的方式，将随机性“重新”引入流体力学方程，从而捕捉到热噪声的本质效应。通过学习本文，读者将能够理解涨落的起源、其与耗散的深刻联系，以及如何运用这一理论来分析和模拟复杂的流体现象。

文章将分为三个核心章节。在“原理与机制”中，我们将深入探讨理论的基石——局域平衡假设与涨落-耗散定理，并展示如何推导出关键的随机应力项。接着，在“应用与跨学科联系”中，我们将展示该理论的强大威力，从解释布朗运动和“长时尾”等基本物理现象，到其在计算模拟、软物质物理和生物物理等前沿领域的广泛应用。最后，在“动手实践”部分，我们将通过一系列引导性问题，巩固核心理论概念，并将其应用于具体的计算和边界条件设定中，从而将理论知识转化为实践能力。

## 原理与机制

在“引言”章节中，我们已经了解，涨落流体力学旨在通过在确定性流体力学方程中引入随机项来描述介观尺度上的热涨落。本章将深入探讨支撑这一理论框架的核心原理和关键机制。我们将从基本假设出发，推导涨落与耗散之间的普适关系，并展示如何应用这些原理来分析和预测可观测的涨落现象。

### 局域平衡假设：涨落流体动力学的基石

涨落流体动力学的核心出发点是 **局域平衡假设** (local equilibrium assumption)。这一假设断言，尽管整个系统可能处于非平衡态，具有宏观的梯度和流动，但如果我们考察一个足够小（但仍包含大量分子）的流体单元，在足够短（但长于分子碰撞时间）的时间尺度内，这个流体单元自身可以被认为处于一个局域的热力学平衡态 [@problem_id:4088454]。

这个假设的合理性源于**时间尺度分离** (time-scale separation) 的概念。在一个流体系统中，存在两类截然不同的动力学过程。第一类是与守恒量（如质量、动量和能量）相关的慢变量，或称 **流体力学模式** (hydrodynamic modes)。由于守恒律的限制，这些量的变化只能通过在宏观尺度上的输运过程发生，因此其演化非常缓慢。第二类是所有其他微观自由度，它们不对应于守恒量，被认为是快变量。这些快变量的弛豫过程非常迅速，其弛豫时间 $\tau_{\text{micro}}$ 远小于流体力学模式的特征时间 $\tau_{\text{hydro}}$。

涨落流体力学正是建立在对这些介于 $\tau_{\text{micro}}$ 和 $\tau_{\text{hydro}}$ 之间的中间时间尺度 $\tau$ 进行粗粒化描述的基础之上。局域平衡假设意味着，在这样的时空尺度上观察，每个流体单元的状态完全由局域、瞬时的慢变量值（如质量密度 $\rho(\mathbf{r}, t)$ 和动量密度 $\rho(\mathbf{r}, t)\mathbf{v}(\mathbf{r}, t)$）所决定。因此，标准的热力学平衡关系，如状态方程，在每个流体单元内部局部成立。例如，局域压力 $p$ 和局域温度 $T$ 都是局域密度和内能的函数，即 $p = p(\rho, u)$ 和 $T = T(\rho, u)$。

为了更具体地理解这一点，让我们考虑一个等温的单组分牛顿流体。在这种情况下，能量被假定为能够极快地弛豫，使得系统温度始终保持恒定。因此，能量不再是一个慢的流体力学变量。此时，系统的慢变量仅剩下由质量和动量守恒所对应的质量密度 $\rho$ 和动量密度 $\rho\mathbf{v}$。所有其他的热力学变量，包括温度 $T$（及其等价的熵密度 $s$）、压力 $p$ 和化学势 $\mu$，都必须比流体力学模式弛豫得更快，因此被归类为快变量 [@problem_id:4088454]。这些快变量的值通过状态方程（例如 $p = p(\rho, T_0)$）代数地由慢变量决定。

### 涨落-耗散定理：连接涨落与耗散的桥梁

局域平衡假设为我们描述流体单元的状态提供了热力学基础，但它没有告诉我们如何刻画那些被平均掉的、快速的微观涨落。这些涨落通过随机流（如随机应力张量和随机热流）的形式被重新引入到流体力学方程中。描述这些随机流统计性质的核心物理原理，就是 **涨落-耗散定理** (Fluctuation-Dissipation Theorem, FDT)。

涨落-耗散定理的本质思想是，驱动一个系统离开平衡态的宏观耗散过程（如粘性和热传导）与系统在平衡态附近的热涨落源于相同的微观动力学。因此，随机流的强度（用其协方差衡量）必须与宏观输运系数（如粘度、热导率）之间存在一种深刻而普适的联系。

为了精确表述这一定理，我们首先需要借助线性不可逆热力学的框架。该框架指出，系统熵产率密度 $\dot{s}$ 可以表示为一系列 **热力学通量** ($\boldsymbol{J}_\alpha$) 与其 **共轭力** ($\boldsymbol{X}_\alpha$) 的双线性乘积之和：
$$
\dot{s} = \sum_\alpha \boldsymbol{J}_\alpha : \boldsymbol{X}_\alpha \ge 0
$$
熵产必须非负。在线性响应区域，通量与力呈线性关系，$\boldsymbol{J}_\alpha = \sum_\beta \boldsymbol{L}_{\alpha\beta} \boldsymbol{X}_\beta$，其中 $\boldsymbol{L}_{\alpha\beta}$ 是昂萨格 (Onsager) 关系矩阵。

涨落流体力学中的随机流 $\boldsymbol{J}_\alpha^{\mathrm{st}}$ 被假设为零均值的高斯过程。涨落-耗散定理给出了其协方差 [@problem_id:4088450]：
$$
\big\langle \boldsymbol{J}_\alpha^{\mathrm{st}}(\boldsymbol{r},t)\,\boldsymbol{J}_\beta^{\mathrm{st}}(\boldsymbol{r}',t') \big\rangle = k_B (\boldsymbol{L}_{\alpha\beta} + \boldsymbol{L}_{\beta\alpha})\,\delta(\boldsymbol{r}-\boldsymbol{r}')\,\delta(t-t')
$$
其中 $k_B$ 是玻尔兹曼常数。结合昂萨格倒易关系（$\boldsymbol{L}_{\alpha\beta} = \boldsymbol{L}_{\beta\alpha}^T$），上式简化为：
$$
\big\langle \boldsymbol{J}_\alpha^{\mathrm{st}}(\boldsymbol{r},t)\,\boldsymbol{J}_\beta^{\mathrm{st}}(\boldsymbol{r}',t') \big\rangle = 2\,k_B\,\boldsymbol{L}_{\alpha\beta}\,\delta(\boldsymbol{r}-\boldsymbol{r}')\,\delta(t-t')
$$

以下是流体中几个关键耗散过程的通量-力对及其对应的随机流协方差 [@problem_id:4088450]：

1.  **粘性动量输运**：
    *   通量：粘性应力张量 $\boldsymbol{\sigma}'$。
    *   共轭力：速度梯度张量与温度的组合，例如 $(\nabla \boldsymbol{v})/T$。
    *   随机应力张量 $\boldsymbol{\Sigma}$ 的协方差为：
        $$
        \big\langle \Sigma_{ij}(\boldsymbol{r},t)\,\Sigma_{kl}(\boldsymbol{r}',t')\big\rangle = 2\,k_B T\Big[\eta\big(\delta_{ik}\delta_{jl}+\delta_{il}\delta_{jk}\big) + \big(\zeta-\tfrac{2}{3}\eta\big)\delta_{ij}\delta_{kl}\Big]\delta(\boldsymbol{r}-\boldsymbol{r}')\,\delta(t-t')
        $$
        其中 $\eta$ 是剪切粘度，$\zeta$ 是体粘度。

2.  **热传导**：
    *   通量：热通量 $\boldsymbol{q}$。
    *   共轭力：逆温度的梯度 $\nabla(1/T) = -(1/T^2)\nabla T$。
    *   随机热通量 $\boldsymbol{q}^{\mathrm{st}}$ 的协方差为：
        $$
        \big\langle q_i^{\mathrm{st}}(\boldsymbol{r},t)\\,q_j^{\mathrm{st}}(\boldsymbol{r}',t')\big\rangle = 2\,k_B\,T^2\,\kappa\,\delta_{ij}\,\delta(\boldsymbol{r}-\boldsymbol{r}')\,\delta(t-t')
        $$
        其中 $\kappa$ 是热导率。

3.  **示踪物质量扩散**（对于稀溶液）：
    *   通量：示踪物质量通量 $\boldsymbol{J}_c$。
    *   共轭力：化学势与温度之比的负梯度 $-\nabla(\mu/T)$。
    *   随机质量通量 $\boldsymbol{J}^{\mathrm{st}}$ 的协方差为：
        $$
        \big\langle J_i^{\mathrm{st}}(\boldsymbol{r},t)\\,J_j^{\mathrm{st}}(\boldsymbol{r}',t')\big\rangle = 2\,k_B\,\frac{Dc}{k_B}\,\delta_{ij}\delta(\boldsymbol{r}-\boldsymbol{r}')\delta(t-t') = 2\,D\,c\,\delta_{ij}\delta(\boldsymbol{r}-\boldsymbol{r}')\delta(t-t')
        $$
        其中 $D$ 是扩散系数，$c$ 是示踪物浓度。

这些关系是涨落流体力学模型的核心，它们确保了引入的随机项在物理上是一致的，即系统在没有外部驱动时会弛豫到正确的、遵循统计力学原理的热力学平衡态。

### 随机应力张量的推导

在所有随机流中，随机应力张量 $\boldsymbol{\Sigma}$（或记为 $\boldsymbol{\sigma}^{\mathrm{rand}}$）在流体力学中扮演着中心角色。我们可以从第一性原理出发，通过考察粘性耗散来推导其协方差，这为理解涨落-耗散定理提供了一个具体的范例。

在一个 $d$ 维的牛顿流体中，单位体积的粘性耗散率（即熵产率密度乘以温度 $T$）可以表示为应变率张量 $\boldsymbol{E}$ 的二次型，其中 $E_{ij} = \frac{1}{2}(\partial_i v_j + \partial_j v_i)$ [@problem_id:4088499, 4088509]。对于各向同性流体，确定性的粘性应力 $\boldsymbol{\sigma}^{\mathrm{visc}}$ 与应变率张量 $\boldsymbol{E}$ 之间的最一般线性关系为：
$$
\sigma^{\mathrm{visc}}_{ij} = 2\eta \left( E_{ij} - \frac{1}{d} \delta_{ij} E_{kk} \right) + \zeta \delta_{ij} E_{kk}
$$
这里，$E_{kk} = \nabla \cdot \boldsymbol{v}$ 是张量的迹，代表体积膨胀率。第一项是描述剪切变形的无迹部分，第二项是描述体积变化的各向同性部分。这个关系式可以整理为：
$$
\sigma^{\mathrm{visc}}_{ij} = 2\eta E_{ij} + \left( \zeta - \frac{2\eta}{d} \right) \delta_{ij} E_{kk}
$$
这个表达式定义了粘性应力（通量）和应变率（与力成正比）之间的关系。我们可以将其写成 $\sigma^{\mathrm{visc}}_{ij} = \mathcal{L}_{ijkl} (E_{kl}/T)$ 的形式，从而识别出四阶昂萨格动力学系数张量 $\mathcal{L}_{ijkl}$：
$$
\mathcal{L}_{ijkl} = T \left[ \eta(\delta_{ik}\delta_{jl} + \delta_{il}\delta_{jk}) + \left( \zeta - \frac{2\eta}{d} \right) \delta_{ij}\delta_{kl} \right]
$$
这个张量自动满足昂萨格倒易关系 $\mathcal{L}_{ijkl} = \mathcal{L}_{klij}$。

现在，我们可以直接应用涨落-耗散定理的一般形式。假设随机应力是一个在时空中不相关的（马尔可夫）过程，其协方差由下式给出：
$$
\big\langle \sigma^{\mathrm{rand}}_{ij}(\boldsymbol{r},t) \sigma^{\mathrm{rand}}_{kl}(\boldsymbol{r}',t') \big\rangle = 2 k_B \mathcal{L}_{ijkl} \delta(\boldsymbol{r}-\boldsymbol{r}') \delta(t-t')
$$
将我们得到的 $\mathcal{L}_{ijkl}$ 代入，便得到了随机应力张量协方差的最终表达式 [@problem_id:4088509]：
$$
\big\langle \Sigma_{ij}(\boldsymbol{r},t)\,\Sigma_{kl}(\boldsymbol{r}',t') \big\rangle = 2 k_{B} T \left[ \eta \left( \delta_{ik} \delta_{jl} + \delta_{il} \delta_{jk} \right) + \left( \zeta - \frac{2\eta}{d} \right) \delta_{ij} \delta_{kl} \right] \delta(\boldsymbol{r}-\boldsymbol{r}') \delta(t-t')
$$
这个公式是涨落流体力学中的一个标志性结果。它精确地量化了热涨落的强度和张量结构，将其与流体的宏观输运性质（粘度 $\eta$ 和 $\zeta$）以及温度 $T$ 联系起来。

### 关联函数与动态结构因子

涨落流体力学不仅给出了随机源的统计特性，其最终目标是预测可观测的流体力学场（如密度、速度）本身的涨落行为。这些行为通常通过 **两点关联函数** (two-point correlation function) 来描述。对于一个涨落场 $\delta A(\mathbf{r},t) = A(\mathbf{r},t) - \langle A \rangle$，在统计平稳和空间均匀的系统中，其关联函数定义为 [@problem_id:4088422]：
$$
C_{AA}(\mathbf{r}, t) = \langle \delta A(\mathbf{r}, t)\,\delta A(\mathbf{0}, 0)\rangle
$$
这个函数描述了在空间相距 $\mathbf{r}$、时间相隔 $t$ 的两点处场的涨落之间的关联程度。

虽然关联函数包含了完整的统计信息，但在实验中（如中子或光散射实验）直接测量的量是其在傅里叶空间中的对应物——**动态结构因子** (dynamic structure factor) $S_{AA}(\mathbf{k}, \omega)$。它被定义为关联函数 $C_{AA}(\mathbf{r}, t)$ 的时空傅里叶变换：
$$
S_{AA}(\mathbf{k},\omega) \equiv \int_{-\infty}^{\infty}\mathrm{d}t\, e^{i\omega t}\int_{\mathbb{R}^d}\mathrm{d}\mathbf{r}\, e^{-i\mathbf{k}\cdot\mathbf{r}}\, C_{AA}(\mathbf{r},t)
$$
动态结构因子描述了系统的涨落在不同波矢 $\mathbf{k}$（对应空间尺度 $2\pi/k$）和不同频率 $\omega$（对应时间尺度 $2\pi/\omega$）上的能量分布。

动态结构因子与涨落场的傅里叶模式的谱密度直接相关。通过傅里叶变换和统计平均的运算，可以证明两者之间存在一个普适的关系，即 **维纳-辛钦定理** (Wiener-Khinchin theorem) [@problem_id:4088422]：
$$
\langle \delta A_{\mathbf{k}}(\omega)\,\delta A_{-\mathbf{k}}(-\omega) \rangle = (2\pi)^{d+1} S_{AA}(\mathbf{k},\omega)
$$
其中 $\delta A_{\mathbf{k}}(\omega)$ 是涨落场 $\delta A(\mathbf{r}, t)$ 的时空傅里叶变换。这个关系是连接理论计算与实验测量的桥梁：通过求解随机流体力学方程得到场的傅里叶模式的关联，我们就可以得到动态结构因子，进而与实验结果进行比较。

### 涨落流体动力学的应用实例

理论的威力在于其应用。下面我们通过几个具体的例子来展示如何运用上述原理来分析流体的涨落。

#### 实例一：纯热传导流体中的温度涨落

考虑一个不可压缩、静态的流体，其中唯一的动力学过程是热传导。温度涨落 $T(\mathbf{r},t)$ 由随机热方程描述 [@problem_id:4088458]：
$$
\rho c_p \,\partial_t T - \kappa \nabla^2 T = -\nabla \cdot \mathbf{q}^{f}
$$
其中 $c_p$ 是定压比热，$\mathbf{q}^f$ 是随机热通量。我们将此方程进行时空傅里叶变换，利用 $\partial_t \to -i\omega$ 和 $\nabla \to i\mathbf{k}$（根据问题中傅里叶变换的定义），得到：
$$
(-i\omega \rho c_p + \kappa k^2) T(\mathbf{k},\omega) = -i\mathbf{k} \cdot \mathbf{q}^{f}(\mathbf{k},\omega)
$$
由此解出温度涨落的傅里叶模式：
$$
T(\mathbf{k},\omega) = \frac{-i\mathbf{k} \cdot \mathbf{q}^{f}(\mathbf{k},\omega)}{\kappa k^2 - i\omega \rho c_p}
$$
为了计算动态结构因子 $S_{TT}(k,\omega)$，我们计算 $\langle T(\mathbf{k},\omega) T(\mathbf{k}',\omega') \rangle$。利用前面给出的随机热通量协方差的涨落-耗散定理，经过一番代数运算，我们最终得到 [@problem_id:4088458]：
$$
S_{TT}(k,\omega) = \frac{2 k_B T^2 \kappa k^2}{(\rho c_p)^2(\omega^2 + \alpha^2 k^4)} = \frac{2 k_B T^2 \alpha k^2}{\rho c_p (\omega^2 + (\alpha k^2)^2)}
$$
其中 $\alpha = \kappa/(\rho c_p)$ 是热扩散系数。这个结果揭示了深刻的物理内涵：对于一个给定的波矢 $k$，温度涨落的谱密度是一个关于频率 $\omega$ 的 **洛伦兹函数** (Lorentzian)。其峰值位于 $\omega=0$，半高宽为 $\Gamma(k) = \alpha k^2$。这表明，一个空间尺度为 $2\pi/k$ 的温度涨落会以特征时间 $1/\Gamma(k) \sim 1/(\alpha k^2)$ 通过热扩散过程衰减掉，这正是宏观热传导理论所预期的结果。

#### 实例二：不可压缩流体中的速度涨落

接下来，考虑一个静止的不可压缩牛顿流体。速度场 $\mathbf{v}$ 的线性化涨落方程是随机斯托克斯方程 [@problem_id:4088485]：
$$
\rho \frac{\partial \mathbf{v}}{\partial t} = -\nabla p + \eta \nabla^2 \mathbf{v} + \nabla \cdot \boldsymbol{\Sigma}
$$
同时满足不可压缩条件 $\nabla \cdot \mathbf{v} = 0$。在傅里叶空间中，不可压缩条件变为 $\mathbf{k} \cdot \hat{\mathbf{v}}(\mathbf{k}) = 0$，意味着速度矢量必须垂直于波矢 $\mathbf{k}$。我们可以使用横向投影算子 $\mathbf{P}(\mathbf{k}) = \mathbf{I} - \mathbf{k}\mathbf{k}^{\top}/k^2$ 来消除压力项并分离出横向速度模式。

通过求解这个随机微分方程，并计算等时速度关联函数，可以得到一个非常优美的结果 [@problem_id:4088485]：
$$
\left\langle \hat{v}_{i}(\mathbf{k},t)\,\hat{v}_{j}(\mathbf{k}',t) \right\rangle = (2\pi)^3 \frac{k_B T}{\rho} P_{ij}(\mathbf{k}) \delta(\mathbf{k}+\mathbf{k}')
$$
这个结果表明，在热平衡状态下，每个独立的横向流体模式的动能（与 $\langle |\hat{\mathbf{v}}|^2 \rangle$ 成正比）的期望值为 $k_B T / \rho$。这正是统计力学中 **能量均分定理** (equipartition of energy) 在流体力学模式上的体现。值得注意的是，最终的平衡态关联函数与粘度 $\eta$ 无关，因为粘度只影响系统如何弛豫到平衡，而不改变平衡态本身的统计性质。

#### 实例三：可压缩流体中的耦合涨落

在更一般的情况下，例如可压缩流体，密度、速度和温度的涨落是相互耦合的。线性化的质量、动量和能量守恒方程构成一个耦合的随机微分方程组。在傅里叶空间中，这可以写成一个矩阵形式 [@problem_id:4088474]：
$$
\frac{d}{dt} \begin{pmatrix} \hat{\rho} \\ \hat{u}_\parallel \\ \hat{T} \end{pmatrix} = 
\mathbf{M}(\mathbf{k})
\begin{pmatrix} \hat{\rho} \\ \hat{u}_\parallel \\ \hat{T} \end{pmatrix}
+
\mathbf{f}(\mathbf{k}, t)
$$
其中 $\hat{u}_\parallel$ 是沿波矢 $\mathbf{k}$ 方向的纵向速度分量，$\mathbf{M}(\mathbf{k})$ 是动力学矩阵，$\mathbf{f}(\mathbf{k}, t)$ 是由随机应力和随机热流构成的随机力项。动力学矩阵的非对角元代表了不同模式间的耦合，例如压力梯度将密度和温度涨落与速度涨落耦合起来。这个矩阵的本征值和本征向量决定了流体涨落的谱线结构，即著名的瑞利-布里渊散射谱，它包含对应于声波传播的布里渊峰和对应于热扩散的瑞利中心峰。

### 流体动力学噪声的本质：从连续介质到计算模型

涨落-耗散定理给出的随机流协方差中，$\delta(\mathbf{r}-\mathbf{r}')$ 和 $\delta(t-t')$ 这两个狄拉克 delta 函数具有特殊的物理意义。它们表明，对于一个牛顿流体，随机流在空间和时间上都是 **白色噪声** (white noise)，即在任何不同时空点上的取值都是不相关的 [@problem_id:4088455]。

这种 **马尔可夫近似** (Markovian approximation) 的物理基础是，牛顿流体的本构关系是局域和瞬时的——应力只取决于同一点、同一时刻的应变率，没有空间关联和时间记忆。根据涨落-耗散定理，耗散过程的无记忆性直接导致了涨落的无记忆性（即白噪声）。

这个连续介质模型在计算中带来了挑战，因为 delta 函数意味着无穷大的方差。在数值模拟中，时空离散化自然地提供了一个紫外截断。对于一个体积为 $\Delta V$、时间步长为 $\Delta t$ 的离散单元，其中的平均随机变量的方差必须满足以下关键的标度律 [@problem_id:4088455]：
$$
\text{Var}(\bar{\Sigma}) \propto \frac{1}{\Delta V \Delta t}
$$
这意味着，随着网格加密（$\Delta V, \Delta t \to 0$），随机数的振幅会发散。这个标度律确保了注入系统的总涨落能量与离散化方式无关，从而得到物理上正确的连续介质极限。

然而，马尔可夫近似并非总是成立。当流体本身的响应时间尺度并非无穷快时，噪声就会呈现 **有色** (colored) 的特征，摩擦也会表现出 **记忆效应** (memory effect)。这种情况的发生与否，取决于对系统时间尺度的仔细分析 [@problem_id:4088461]。

考虑一个半径为 $a$ 的胶体颗粒在流体中运动。其动力学涉及多个时间尺度：
*   **颗粒动量弛豫时间** $t_p \sim m/\zeta_0$：颗粒因摩擦而丧失动量的特征时间。
*   **流体粘性扩散时间** $t_\nu(\ell) \sim \ell^2/\nu$：动量通过粘性在尺度 $\ell$上传播的时间。这代表了流体动力学记忆的持续时间。在颗粒尺度上为 $t_\nu(a)$，在受限体系的尺度 $H$ 上为 $t_H$。
*   **声学传播时间** $t_s \sim a/c$：声波穿过颗粒的时间，与可压缩性有关。

马尔可夫近似（白噪声）成立的条件是，所有流体响应时间尺度都远小于我们所关心的动力学时间尺度（如 $t_p$ 和计算时间步 $\Delta t$）。在一个具体的例子中，我们可能会发现 $t_s \ll \Delta t$，因此可以忽略声学记忆效应；但同时 $t_\nu(a)$ 和 $t_H$ 可能与 $t_p$ 或 $T_{\text{obs}}$（总观测时间）相当甚至更长。在这种情况下，流体动力学记忆就变得至关重要，必须在模型中保留，这意味着摩擦力变成了一个含有记忆核的积分项，而随机力也相应地变成了一个有色噪声过程 [@problem_id:4088461]。同样，对于本身就具有内禀记忆的粘弹性流体（如麦克斯韦流体），其随机应力也自然是时间上有色的 [@problem_id:4088455]。

总之，涨落流体力学的原理和机制为我们提供了一个从微观涨落到宏观可观测现象的完整理论框架。它建立在局域平衡假设之上，通过涨落-耗散定理将涨落与耗散联系起来，并允许我们计算各种物理量的关联函数和动态结构因子。同时，对该框架基本假设（如马尔可夫近似）的批判性审视，是将其正确应用于复杂流体计算模型的关键。