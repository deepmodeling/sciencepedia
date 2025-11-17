## 引言
在[磁约束](@entry_id:161852)[核聚变](@entry_id:139312)研究中，一个核心挑战是如何理解并控制等离子体中的[反常输运](@entry_id:746472)现象。实验观测到的粒子和能量损失远超经典和新经典理论的预测，这种额外的输运被归因于由等离子体自身梯度驱动的微观[湍流](@entry_id:151300)。准[线性[输运理](@entry_id:148235)论](@entry_id:143989)正是为了解决这一问题而发展的基石性框架，它旨在建立从微观尺度上的[电磁场](@entry_id:265881)涨落到宏观尺度上可观测的[输运系数](@entry_id:136790)之间的定量联系，从而揭示[湍流输运](@entry_id:150198)的物理本质。

本文旨在为读者系统性地介绍[准线性理论](@entry_id:182724)。我们将首先在“**原理与机制**”一章中，从弗拉索夫-麦克斯韦[动力学方程](@entry_id:751029)出发，通过尺度分离和[随机相位近似](@entry_id:754035)，揭示涨落如何通过波-粒共振机制驱动速度空间中的[扩散](@entry_id:141445)，并最终导致宏观输运。接着，在“**应用与跨学科联系**”一章中，我们将展示该理论在解决聚变等离子体中的实际问题，如粒子、热量与杂质输运、高能[粒子约束](@entry_id:148454)以及与剖面刚性和输运垒等现象的耦合方面的强大能力。最后，在“**动手实践**”部分，读者将通过具体计算，将理论知识应用于解决实际问题，加深对核心概念的理解。通过这三个层层递进的章节，读者将能够全面掌握[准线性理论](@entry_id:182724)的精髓及其在现代等离子体物理研究中的核心地位。

## 原理与机制

在“引言”章节中，我们已经了解到，[磁约束聚变](@entry_id:180408)等离子体中的[湍流输运](@entry_id:150198)是限制聚变装置性能的关键物理过程之一。[准线性理论](@entry_id:182724)为理解和定量描述由弱[湍流](@entry_id:151300)驱动的输运提供了一个基础框架。本章将深入探讨[准线性理论](@entry_id:182724)的核心原理与关键机制，从其动力学和统计基础出发，系统地建立波-粒相互作用和[湍流输运](@entry_id:150198)的物理图像。

### [准线性理论](@entry_id:182724)的动力学基础

理解[湍流输运](@entry_id:150198)的第一步是建立描述等离子体演化的数学物理模型。在对聚变等离子体芯部等高温、低密度区域的研究中，粒子间的[库仑碰撞](@entry_id:186273)频率远低于典型的波动频率和粒子动力学频率，因此可以近似为**[无碰撞等离子体](@entry_id:191924)**。在这种情况下，描述粒子在六维相空间（位置 $\mathbf{x}$ 和速度 $\mathbf{v}$）中[分布函数](@entry_id:145626) $f_s(\mathbf{x}, \mathbf{v}, t)$ 演化的基本方程是**[弗拉索夫方程](@entry_id:161066)（Vlasov equation）**。对于非相对论性的等离子体，该方程表达了[相空间密度](@entry_id:150180)沿粒子运动轨迹的守恒（刘维尔定理）：

$$
\frac{\partial f_s}{\partial t} + \mathbf{v}\cdot \nabla_{\mathbf{x}} f_s + \frac{q_s}{m_s}\left(\mathbf{E}+\mathbf{v}\times \mathbf{B}\right)\cdot \nabla_{\mathbf{v}} f_s = 0
$$

其中，下标 $s$ 代表粒子种类（如离子、电子），$q_s$ 和 $m_s$ 分别是其[电荷](@entry_id:275494)和质量。[电场](@entry_id:194326) $\mathbf{E}$ 和[磁场](@entry_id:153296) $\mathbf{B}$ 由**麦克斯韦方程组（Maxwell's equations）**描述，而[方程组](@entry_id:193238)的源项——[电荷密度](@entry_id:144672) $\rho$ 和[电流密度](@entry_id:190690) $\mathbf{J}$——又由分布函数 $f_s$ 的速度矩决定：

$$
\rho(\mathbf{x},t) = \sum_s q_s \int f_s(\mathbf{x},\mathbf{v},t)\, d^3 v, \qquad \mathbf{J}(\mathbf{x},t) = \sum_s q_s \int \mathbf{v}\, f_s(\mathbf{x},\mathbf{v},t)\, d^3 v
$$

这套自洽的[方程组](@entry_id:193238)被称为**[弗拉索夫-麦克斯韦系统](@entry_id:756542)（Vlasov–Maxwell system）**，它是[准线性理论](@entry_id:182724)的出发点。

[湍流](@entry_id:151300)的本质特征是物理量在多个时空尺度上的剧烈波动。[准线性理论](@entry_id:182724)的核心思想正是基于这种尺度分离。我们将每个物理量（分布函数和[电磁场](@entry_id:265881)）分解为一个在宏观输运时间尺度上缓慢演化的**背景（或平衡）部分**和一个在微观波动时间尺度上快速[振荡](@entry_id:267781)的**涨落部分** [@problem_id:3715951]。以分布函数为例：

$$
f_s = F_{0s} + \tilde{f}_s, \qquad \mathbf{E} = \mathbf{E}_0 + \tilde{\mathbf{E}}, \qquad \mathbf{B} = \mathbf{B}_0 + \tilde{\mathbf{B}}
$$

这里，$F_{0s} = \langle f_s \rangle$ 和 $\mathbf{E}_0 = \langle \mathbf{E} \rangle, \mathbf{B}_0 = \langle \mathbf{B} \rangle$ 是通过某种平均操作 $\langle \cdot \rangle$（例如，系综平均、时间平均或[空间平均](@entry_id:203499)）得到的慢变量。涨落部分 $\tilde{f}_s, \tilde{\mathbf{E}}, \tilde{\mathbf{B}}$ 的平均值为零，即 $\langle \tilde{f}_s \rangle = 0$。此外，[准线性理论](@entry_id:182724)假设涨落是小振幅的，即存在一个小参数 $\epsilon \ll 1$，使得 $|\tilde{f}_s|/F_{0s} \sim O(\epsilon)$。

将此分解代入[弗拉索夫方程](@entry_id:161066)并进行平均，我们可以得到背景[分布函数](@entry_id:145626) $F_{0s}$ 的[演化方程](@entry_id:268137)。由于涨落项的线性平均为零，方程中将出现形如 $\langle \tilde{\mathbf{E}} \cdot \nabla_{\mathbf{v}} \tilde{f}_s \rangle$ 的二阶关联项。这个非零的关联项，被称为**[准线性](@entry_id:637689)项**，描述了涨落对背景[分布函数](@entry_id:145626)的净效应。它如同一个等效的“碰撞”项，驱动着宏观[分布函数](@entry_id:145626)的弛豫和相空间中的[扩散](@entry_id:141445)，这正是**[准线性](@entry_id:637689)输运**的来源。在 $O(\epsilon)$ 阶，我们得到描述涨落演化的线性化方程；而在 $O(\epsilon^2)$ 阶，我们得到包含[准线性](@entry_id:637689)项的背景演化方程。

### 涨落的统计描述：[随机相位近似](@entry_id:754035)

面对由大量模式构成的[湍流](@entry_id:151300)场，逐一追踪每个模式的相位演化是不现实的。弱[湍流理论](@entry_id:264896)采用统计方法，其核心是**[随机相位近似](@entry_id:754035)（Random Phase Approximation, RPA）** [@problem_id:3715956]。该近似假设湍谱由大量（$N \gg 1$）独立的、具有随机相位的波[模式叠加](@entry_id:168041)而成。

例如，一个静电[湍流](@entry_id:151300)的势涨落 $\tilde{\phi}(\mathbf{x}, t)$ 可以表示为：

$$
\tilde{\phi}(\mathbf{x},t) = \sum_{\mathbf{k}} \left[ A_{\mathbf{k}} e^{i(\mathbf{k}\cdot\mathbf{x} - \omega_{\mathbf{k}}t + \theta_{\mathbf{k}})} + \text{c.c.} \right]
$$

其中 $A_{\mathbf{k}}$ 是模式 $\mathbf{k}$ 的缓变[复振幅](@entry_id:164138)，$\omega_{\mathbf{k}}$ 是其线性频率，而 $\theta_{\mathbf{k}}$ 是在 $[0, 2\pi)$ 区间[均匀分布](@entry_id:194597)的随机相位。

RPA 的关键推论是：
1.  **一阶矩（平均场）为零**：由于大量模式的相位随机且不相关，它们在求和时会因相干相消（dephasing）而使平均场为零。数学上，$\langle e^{i\theta_{\mathbf{k}}} \rangle = \frac{1}{2\pi} \int_0^{2\pi} e^{i\theta} d\theta = 0$，因此 $\langle \tilde{\phi} \rangle = 0$。
2.  **二阶矩（关联函数）不为零**：在计算二点关联函数如 $\langle \tilde{\phi}(\mathbf{x},t) \tilde{\phi}(\mathbf{x}',t') \rangle$ 时，会涉及到形如 $\langle e^{i(\theta_{\mathbf{k}} - \theta_{\mathbf{k}'})} \rangle$ 的项。由于不同模式的相位独立，当 $\mathbf{k} \neq \mathbf{k}'$ 时，该平均为 $\langle e^{i\theta_{\mathbf{k}}} \rangle \langle e^{-i\theta_{\mathbf{k}'}} \rangle = 0$。只有当 $\mathbf{k} = \mathbf{k}'$ 时，相位差为零，平均值不为零。这可以用克罗内克符号表示为 $\langle e^{i(\theta_{\mathbf{k}} - \theta_{\mathbf{k}'})} \rangle = \delta_{\mathbf{k}\mathbf{k}'}$。因此，只有对角项（自相关）得以保留，使得二阶关联函数不为零，并由波的**[能谱](@entry_id:181780)密度** $\langle |A_{\mathbf{k}}|^2 \rangle$ 决定。

这个结果至关重要：尽管平均场为零，但涨落的二阶统计特性（如[能谱](@entry_id:181780)）得以保留，并成为描述[准线性](@entry_id:637689)输运的关键量。

### 波-粒相互作用的核心：共振条件

[无碰撞等离子体](@entry_id:191924)中，粒子与波动之间的能量和动量交换并非持续发生，而是集中在满足特定**[共振条件](@entry_id:754285)**的粒子上。只有当粒子感受到的波的频率与其自身的某种固有运动频率相匹配时，才能发生持续的、净的能量交换。

在一个均匀[磁场](@entry_id:153296) $\mathbf{B} = B \hat{\mathbf{z}}$ 中，粒子的运动是沿磁力线的匀速直线运动和垂直于磁力线的[匀速圆周运动](@entry_id:178264)（回旋运动）的叠加，形成螺旋线轨迹。其固有频率是**回旋频率** $\Omega = qB/m$。当一个平面波（频率 $\omega$，波矢 $\mathbf{k}$）存在时，一个以平行速度 $v_\parallel$ 运动的粒子在其引导中心[参考系](@entry_id:169232)中感受到的波的频率是[多普勒频移](@entry_id:158041)后的频率 $\omega - k_\parallel v_\parallel$。共振发生在多普勒频移的频率与[回旋频率](@entry_id:156231)的整数倍相匹配时 [@problem_id:3715970]：

$$
\omega - k_\parallel v_\parallel - n\Omega = 0, \quad n \in \mathbb{Z}
$$

这个通用的共振条件涵盖了两种主要的相互作用机制：
-   **[朗道共振](@entry_id:751126)（Landau Resonance, $n=0$）**：条件简化为 $\omega = k_\parallel v_\parallel$，即粒子的平行速度等于波的平行相速度 $v_{\text{ph},\parallel} = \omega/k_\parallel$。这好比粒子在波的[势阱](@entry_id:151413)中“冲浪”。这种相互作用主要通过波的平行[电场](@entry_id:194326) $E_\parallel$ 对粒子做功，改变其平行动能，从而导致速度空间中沿 $v_\parallel$ 方向的[扩散](@entry_id:141445)。

-   **[回旋共振](@entry_id:139685)（Cyclotron Resonance, $n \neq 0$）**：此时，多普勒频移的波频与[回旋频率](@entry_id:156231)的某个谐波匹配。这种相互作用需要波具有有限的垂直[波矢](@entry_id:178620) $k_\perp$，以便粒子在其回旋[轨道](@entry_id:137151)上能感受到变化的波场。相互作用主要通过波的垂直[电场](@entry_id:194326) $E_\perp$ 对粒子做功，改变其垂直动能，导致沿 $v_\perp$ 方向的[扩散](@entry_id:141445)。波的极化方向在此起着关键作用，例如，左旋极化波主要与离子的[基频](@entry_id:268182)[回旋共振](@entry_id:139685)（$n=1$）耦合，而右旋极化波则与电子的[基频](@entry_id:268182)[回旋共振](@entry_id:139685)（$n=-1$，因为电子[电荷](@entry_id:275494)为负）耦合。这正是[离子回旋共振加热](@entry_id:267305)（ICRH）和[电子回旋共振加热](@entry_id:748908)（ECRH）等辅助加热技术的物理基础。

在更真实的环形几何（如托卡马克）中，由于[磁场强度](@entry_id:197932)的变化，部分粒子会被[磁镜效应](@entry_id:171262)捕获，成为**[捕获粒子](@entry_id:756145)**。它们的运动不再是简单的螺旋线，而是在两个“拐点”之间来回反弹的**[香蕉轨道](@entry_id:202619)**，同时伴随着缓慢的环向**进动**。对于这些粒子，[共振条件](@entry_id:754285)需要进一步修正，包含它们的**反弹频率** $\omega_b$ 和**进动频率** $\omega_p$ [@problem_id:3715922]。例如，对于与[捕获电子模](@entry_id:756143)（TEM）相互作用的捕获电子，其[基频](@entry_id:268182)共振条件近似为：

$$
\omega - \omega_p - n_b \omega_b \approx 0
$$

其中 $n_b$ 是反弹谐波数。这表明，在环形几何中，粒子与波动的共振变得更加丰富和复杂。

### [准线性](@entry_id:637689)[扩散张量](@entry_id:748421)

结合涨落的统计描述和波-粒共振机制，我们可以推导出描述[准线性](@entry_id:637689)输运的核心数学工具——**[速度空间扩散](@entry_id:199003)张量** $D_{ij}(\mathbf{v})$。背景分布函数 $F_0$ 的演化方程可以写成一个[福克-普朗克方程](@entry_id:140155)的形式：

$$
\frac{\partial F_0}{\partial t} = \frac{\partial}{\partial v_i} \left( D_{ij}(\mathbf{v}) \frac{\partial F_0}{\partial v_j} \right)
$$

[扩散张量](@entry_id:748421) $D_{ij}$ 本质上是粒子在单位时间内速度变化的二阶矩，它由[电场](@entry_id:194326)涨落的自相关函数沿无扰粒子[轨道](@entry_id:137151)的积分给出。对于均匀[磁化等离子体](@entry_id:201225)中的静电涨落，其完整形式为 [@problem_id:3715990]：

$$
D_{ij}(\mathbf{v}) = \frac{2 \pi q^2}{m^2 \epsilon_0} \sum_{n=-\infty}^{\infty} \int d^3\mathbf{k} \, \hat{k}_i \hat{k}_j \, J_n^2\left(\frac{k_\perp v_\perp}{\Omega}\right) \, W(\mathbf{k}) \, \delta\left(\omega_{\mathbf{k}} - k_\parallel v_\parallel - n \Omega \right)
$$

这个表达式精确地包含了[准线性理论](@entry_id:182724)的全部物理要素：
-   **粒子响应**：由 $(q/m)^2$ 因子体现。
-   **涨落谱**：由波能谱密度 $W(\mathbf{k})$ 体现，这里 $W(\mathbf{k}) = \epsilon_0 |\mathbf{E}_{\mathbf{k}}|^2 / 2$。对于[静电波](@entry_id:196551)，[电场](@entry_id:194326)极化方向与波矢平行，故有 $\hat{k}_i \hat{k}_j$ 因子。
-   **回旋[轨道](@entry_id:137151)效应**：由 $n$ 阶贝塞尔函数 $J_n$ 的平方项体现。其宗量 $\lambda = k_\perp v_\perp / \Omega$ 表示粒子[回旋半径](@entry_id:261534)与垂直波长的比值，描述了[有限拉莫尔半径效应](@entry_id:204257)。
-   **共振条件**：由狄拉克 $\delta$ 函数体现，确保只有满足共振条件的波和粒子才能对[扩散](@entry_id:141445)有贡献。

这个[扩散张量](@entry_id:748421)描述了粒子在速度空间中的[随机行走](@entry_id:142620)过程。正是这个过程，导致了宏观尺度上的粒子、动量和热量的输运。

### [湍流输运](@entry_id:150198)的产生与特征

有了[速度空间扩散](@entry_id:199003)张量，我们如何理解真[实空间](@entry_id:754128)中的粒子和热量输运？宏观输运流（如径向[粒子流](@entry_id:753205) $\Gamma_x$）是由涨落量之间的关联决定的。在静电[湍流](@entry_id:151300)中，[径向速度](@entry_id:159824)涨落主要是由 $\mathbf{E} \times \mathbf{B}$ 漂移引起，即 $\tilde{v}_x = - (1/B) \partial_y \tilde{\phi}$。因此，径向粒子流为：

$$
\Gamma_x = \langle \tilde{n} \tilde{v}_x \rangle
$$

要使这个平均值不为零，密度涨落 $\tilde{n}$ 和[径向速度](@entry_id:159824)涨落 $\tilde{v}_x$（或等效地，势涨落 $\tilde{\phi}$）之间必须存在特定的**相移** [@problem_id:3716005]。如果 $\tilde{n}$ 和 $\tilde{\phi}$ 完全同相或反相，那么通过[傅里叶分析](@entry_id:137640)可以证明 $\Gamma_x=0$。具体来说，输运流的大小正比于 $\tilde{n}$ 和 $\tilde{\phi}$ 之间相移 $\delta$ 的正弦，即 $\Gamma_x \propto \sin(\delta)$。

这个关键的相移从何而来？它源于等离子体响应中的**非厄米部分**，即与能量耗散或增长相关的部分。在一个理想的无[耗散系统](@entry_id:151564)中（例如，电子绝热响应 $\tilde{n}/n_0 = e\tilde{\phi}/T_e$），[响应函数](@entry_id:142629)是实数，相移为零，没有输运。然而，当存在[朗道阻尼](@entry_id:137619)、碰撞或其他驱动/阻尼机制时，等离子体的[介电响应](@entry_id:140146)函数会包含虚部。这个虚部导致了 $\tilde{n}$ 和 $\tilde{\phi}$ 之间的非零相移，从而打开了输运的通道。在共振点附近，相移趋近于 $\pm\pi/2$，使得输运效率最高。

在[托卡马克](@entry_id:182005)中，驱动这些涨落的能量来源主要是背景等离子体的**密度和温度梯度**。几种主要的微观不稳定性包括 [@problem_id:3715923]：
-   **[离子温度梯度模](@entry_id:750906) (ITG)**：由[离子温度](@entry_id:191275)梯度驱动，发生在离子[回旋半径](@entry_id:261534)尺度（$k_\perp \rho_i \sim 1$），主要引起离子热量向外输运。
-   **[捕获电子模](@entry_id:756143) (TEM)**：由捕获电子的动力学与背景密度/温度梯度耦合驱动，也发生在离子尺度，能够驱动显著的电子热量和粒子输运。
-   **[电子温度梯度模](@entry_id:749097) (ETG)**：由[电子温度梯度](@entry_id:748914)驱动，发生在电子[回旋半径](@entry_id:261534)尺度（$k_\perp \rho_e \sim 1$），主要引起电子热量输运，而离子由于[回旋半径](@entry_id:261534)过大几乎不参与。

这些不稳定性从梯度中汲取自由能，使涨落增长，并通过上述的[准线性](@entry_id:637689)机制将能量转化为跨越[磁面](@entry_id:204802)的粒子和热量输运。

### [湍流](@entry_id:151300)的自持与调控

一个完整的输运图像不仅要解释输运如何产生，还要说明[湍流](@entry_id:151300)涨落本身是如何维持在一个统计饱和状态的。涨落的演化可以用**波动态能学方程（Wave Kinetic Equation）**来描述 [@problem_id:3715921]：

$$
\frac{\partial W_{\mathbf{k}}}{\partial t} = 2\gamma_{\mathbf{k}} W_{\mathbf{k}} - 2\nu_{\mathrm{nl},\mathbf{k}} W_{\mathbf{k}} + S_{\mathbf{k}} - L_{\mathbf{k}}
$$

这里，$W_{\mathbf{k}}$ 是波[谱能量密度](@entry_id:168013)。方程右侧各项分别代表：
-   $2\gamma_{\mathbf{k}} W_{\mathbf{k}}$：线性增长项。$\gamma_{\mathbf{k}} > 0$ 表示模式 $\mathbf{k}$ 是线性不稳定的，从背景梯度中获取能量。因子 $2$ 源于能量与振幅的平方关系。
-   $-2\nu_{\mathrm{nl},\mathbf{k}} W_{\mathbf{k}}$：[非线性](@entry_id:637147)饱和项。$\nu_{\mathrm{nl},\mathbf{k}}$ 代表[非线性](@entry_id:637147)过程（如波-波相互作用、共振展宽等）导致的[退相干](@entry_id:145157)或能量转移率，它限制了涨落的无限增长。
-   $S_{\mathbf{k}}$ 和 $L_{\mathbf{k}}$：外部能量源和汇，如天线驱动或碰撞耗散。

在饱和状态下，$\partial W_{\mathbf{k}} / \partial t = 0$，[线性增长](@entry_id:157553)与[非线性](@entry_id:637147)饱和及耗散达到平衡。

在[托卡马克](@entry_id:182005)等离子体中，一个极其重要的[非线性](@entry_id:637147)饱和机制是**带状流（Zonal Flows）**的产生 [@problem_id:3715975]。带状流是一种特殊的[静电势](@entry_id:188370)结构，它具有径向变化但环向和极向对称（即 $k_y=0, k_z=0$）。它本身不直接引起径向输运，但它产生的径向变化的极向 $\mathbf{E} \times \mathbf{B}$ 漂移，即**剪切流**，能够有效地“撕裂”和“拉长”背景中的湍流涡胞。

这种**剪切[退相干](@entry_id:145157)**机制会缩短湍流涡胞的相干时间 $\tau_c$，从而抑制输运。当剪切率足够强时，[输运系数](@entry_id:136790) $D \sim \langle \tilde{v}_x^2 \rangle \tau_c$ 会被显著压低。因此，带状流被认为是[湍流](@entry_id:151300)的一种**自发调节机制**，它由[湍流](@entry_id:151300)本身[非线性](@entry_id:637147)地产生，反过来又抑制[湍流](@entry_id:151300)的强度，形成一个复杂的“捕食者-被捕食者”式的动态平衡系统。

### [准线性理论](@entry_id:182724)的[适用范围](@entry_id:636189)

最后，我们必须认识到[准线性理论](@entry_id:182724)是一个[近似理论](@entry_id:138536)，它的有效性依赖于一系列条件。这些条件共同定义了**弱[湍流](@entry_id:151300)**状态。核心的判据可以由三个特征频率（或速率）的大小关系来确定 [@problem_id:3715953]：
1.  **线性增长率 $\gamma$**：描述不稳定性驱动涨落的速率。
2.  **[退相干](@entry_id:145157)率 $\nu_{\mathrm{dec}}$**：描述涨落相位被[随机化](@entry_id:198186)的速率，它设定了涨落的[相干时间](@entry_id:176187) $\tau_c \sim 1/\nu_{\mathrm{dec}}$。
3.  **[非线性](@entry_id:637147)周转率 $k_\perp \tilde{v}_E$**：描述粒子被湍流涡胞“捕获”或“翻转”的速率。

[准线性理论](@entry_id:182724)的两个基本要求是：
1.  **随机相位**：涨落的增长不能太快，以至于某个模式主导整个系统，破坏随机相位假设。这要求 $\gamma \lesssim \nu_{\mathrm{dec}}$。
2.  **弱相互作用**：粒子与波的相互作用应是多次、微弱、不相关的“碰撞”之和，而不是被单个大涡胞捕获。这要求粒子在一个相干时间内被涡胞引起的轨迹偏折很小，即[非线性](@entry_id:637147)[周转时间](@entry_id:756237)远长于相干时间，等价于 $k_\perp \tilde{v}_E \ll \nu_{\mathrm{dec}}$。

综上，[准线性理论](@entry_id:182724)的适用条件为：
$$
\gamma \lesssim \nu_{\mathrm{dec}} \quad \text{且} \quad k_\perp \tilde{v}_E \ll \nu_{\mathrm{dec}}
$$

当这些条件不满足时，例如当 $k_\perp \tilde{v}_E \gtrsim \nu_{\mathrm{dec}}$ 时，系统进入**强[湍流](@entry_id:151300)**状态。此时，粒子捕获、涡胞-涡胞相互作用等强[非线性](@entry_id:637147)效应变得重要，[准线性理论](@entry_id:182724)失效，需要更复杂的理论工具（如[重整化理论](@entry_id:160488)或[直接数值模拟](@entry_id:149543)）来描述。