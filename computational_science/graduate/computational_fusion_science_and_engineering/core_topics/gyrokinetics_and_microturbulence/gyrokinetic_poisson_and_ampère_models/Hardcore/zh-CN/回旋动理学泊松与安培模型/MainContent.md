## 引言
在[磁约束聚变](@entry_id:180408)研究中，理解等离子体内部的[湍流](@entry_id:151300)和输运是实现稳定燃烧的关键挑战。等离子体由海量带电粒子组成，其运动跨越多个时空尺度，从围绕磁力线的快速回旋到宏观尺度的慢速漂移。直接模拟这种复杂的动力学在计算上是不可承受的。为了解决这一难题，物理学家发展了回旋动理学理论——一个通过系统性地平均掉快速[回旋运动](@entry_id:204632)，从而极大地简化问题维度的强大框架。

本文深入探讨[回旋动理学理论](@entry_id:186998)的核心组成部分：[自洽场](@entry_id:136549)方程，即[回旋动理学泊松方程](@entry_id:1125862)与安培定律。这些方程构成了连接[粒子动力学](@entry_id:1129385)与电磁场演化的桥梁，是所有现代[回旋动理学模拟](@entry_id:181190)的基础。我们将分三个章节展开：第一章“原理与机制”将详细阐述这些方程如何从第一性原理导出，并揭示其背后的物理机制，如[准中性](@entry_id:197419)、[有限拉莫尔半径效应](@entry_id:1125111)和静电与电磁近似的界限。第二章“应用与跨学科联系”将展示这些模型如何应用于分析具体的等离子体不稳定性（如微撕裂模和动力学[气球模](@entry_id:195101)），并探讨其与流[体力](@entry_id:174230)学及计算科学的深刻联系。最后，在“动手实践”部分，我们将通过具体的编程和分析练习，将理论知识转化为解决实际问题的能力。通过这一结构化的学习路径，读者将全面掌握回旋动理学泊松与安培模型，并理解其在现代聚变科学研究中的核心地位。

## 原理与机制

在理解[磁化等离子体](@entry_id:201225)中低频现象（如[湍流](@entry_id:151300)和输运）的复杂动态时，一个关键的挑战在于处理跨越多个时空尺度的物理过程。带电粒子围绕磁力线的快速[回旋运动](@entry_id:204632)，其频率为[回旋频率](@entry_id:156231) $\Omega_s$，通常远快于等离子体中波和不稳定性演化的特征频率 $\omega$。[直接数值模拟](@entry_id:149543)这种快慢耦合的动力学在计算上是不可行的。[回旋动理学理论](@entry_id:186998)通过系统地分离这些尺度，提供了一个严谨且高效的降维模型，从而成为现代[聚变等离子体物理](@entry_id:749660)研究的基石。本章将深入探讨回旋动理学模型中泊松（Poisson）方程和安培（Ampère）定律的构建原理与核心机制。

### 从粒子到[导心](@entry_id:200181)：回旋动理学变换

回旋动理学方法的核心思想是将粒子的运动分解为两部分：沿着磁场引导中心（[导心](@entry_id:200181)）的慢速漂移运动和围绕导心的快速[回旋运动](@entry_id:204632)。为此，我们将描述粒子状态的相空间坐标从粒子坐标 $(\mathbf{r}, \mathbf{v})$ 变换为导心坐标 $(\mathbf{R}, v_\parallel, \mu, \theta)$。

这种变换的定义如下：
1.  **导心位置** $\mathbf{R}$：粒子快速[回旋运动](@entry_id:204632)的中心，通过关系式 $\mathbf{r} = \mathbf{R} + \boldsymbol{\rho}$ 定义。其中 $\mathbf{r}$ 是粒子的瞬时位置，$\boldsymbol{\rho}$ 是从导心指向粒子的[拉莫尔半径](@entry_id:197083)矢量。
2.  **平行速度** $v_\parallel$：[粒子速度](@entry_id:196946) $\mathbf{v}$ 沿着磁场方向 $\hat{\mathbf{b}} \equiv \mathbf{B}/B$ 的分量，即 $v_\parallel \equiv \mathbf{v} \cdot \hat{\mathbf{b}}$。
3.  **磁矩** $\mu$：定义为 $\mu \equiv m_s v_\perp^2 / (2B)$，其中 $v_\perp = |\mathbf{v} - v_\parallel \hat{\mathbf{b}}|$ 是垂直速度的大小，$m_s$ 是[粒子质量](@entry_id:156313)。在缓慢变化的磁场中，磁矩是一个绝热不变量，即其随时间的变化非常缓慢，这使其成为描述慢动态的理想坐标。
4.  **回旋角** $\theta$：描述[拉莫尔半径](@entry_id:197083)矢量 $\boldsymbol{\rho}$ 或垂直速度矢量 $\mathbf{v}_\perp$ 在垂直于磁场的平面[内旋转](@entry_id:905479)的相位角。

在这种新坐标系下，动力学被清晰地分离开来。回旋角 $\theta$ 的演化是快速的，其变化率 $\dot{\theta}$ 近似等于[回旋频率](@entry_id:156231) $\Omega_s \equiv q_s B/m_s$（其中 $q_s$ 是粒子电荷）。相比之下，[导心](@entry_id:200181)坐标 $\mathbf{R}$、平行速度 $v_\parallel$ 和磁矩 $\mu$ 的演化则慢得多，其变化由漂移运动和沿磁力线的运动决定。

[回旋动理学理论](@entry_id:186998)的精髓在于利用这种时间尺度的分离。通过对描述[粒子分布函数](@entry_id:753202) $f_s(\mathbf{r}, \mathbf{v}, t)$ 的[动理学方程](@entry_id:751029)（如[弗拉索夫方程](@entry_id:161066)）在回旋角 $\theta$ 上进行平均，我们可以消除对快速[回旋运动](@entry_id:204632)的依赖。这个过程被称为**[回旋平均](@entry_id:1125848)**，它产生一个描述回旋平均分布函数 $F_s(\mathbf{R}, v_\parallel, \mu, t)$ 演化的降维方程——回旋动理学方程。至关重要的是，这个平均过程并非简单地忽略[回旋运动](@entry_id:204632)，而是系统地保留了其物理效应，如**[有限拉莫尔半径](@entry_id:1124992)（Finite Larmor Radius, FLR）**效应。

### 回旋动理学序：理论的基石

回旋动理学作为一个[渐近理论](@entry_id:162631)，其有效性建立在一套特定的[标度关系](@entry_id:273705)之上，这套关系被称为**回旋动理学序（gyrokinetic ordering）**。它定义了理论适用的物理场景，即强磁化等离子体中低频、短垂直波长的涨落。通常，我们引入一个小的[无量纲参数](@entry_id:169335) $\epsilon \ll 1$ 来统一描述这些标度关系：

*   **低频序**：涨落频率 $\omega$ 远小于回旋频率 $\Omega_s$：$\frac{\omega}{\Omega_s} \sim \epsilon$。
*   **各向异性序**：平[行波](@entry_id:1133416)长远大于垂直波长，即平[行波](@entry_id:1133416)数 $k_\parallel$ 远小于垂直波数 $k_\perp$：$\frac{k_\parallel}{k_\perp} \sim \epsilon$。
*   **小[拉莫尔半径](@entry_id:197083)序**：粒子[拉莫尔半径](@entry_id:197083) $\rho_s$ 远小于平衡参数（如密度、温度）变化的宏观尺度 $L$：$\frac{\rho_s}{L} \sim \epsilon$。
*   **短垂直波长**：涨落的垂直波长与粒子[拉莫尔半径](@entry_id:197083)相当：$k_\perp \rho_s \sim \mathcal{O}(1)$。

这些[序关系](@entry_id:138937)共同定义了回旋动理学模型的核心[适用范围](@entry_id:636189)。基于 $k_\perp \rho_s$ 的取值，我们可以进一步区分两种相关的动理学模型：

*   **漂移-动理学（Drift-Kinetic, DK）模型**：适用于长波极限，即 $k_\perp \rho_s \ll 1$。在此极限下，回旋平均算子近似为单位算子，[有限拉莫尔半径](@entry_id:1124992)（FLR）效应可以被忽略。FLR效应作为 $(k_\perp \rho_s)^2$ 阶的小量被舍去。

*   **回旋动理学（Gyrokinetic, GK）模型**：专为 $k_\perp \rho_s \sim \mathcal{O}(1)$ 的情况设计。此时，涨落的垂直波长与[拉莫尔半径](@entry_id:197083)相当，FLR效应是$\mathcal{O}(1)$阶的，必须被精确保留。这是研究大多数[微观不稳定性](@entry_id:1127873)的关键模型。

因此，GK模型是DK模型的推广，它通过系统地处理回旋平均，将FLR效应纳入理论框架。

### 场方程的简化：静电与电磁模型

回旋动理学序不仅简化了粒子运动的描述，也极大地简化了麦克斯韦场方程，从而定义了不同的理论模型。

#### [安培定律](@entry_id:140092)与位移电流

在[安培-麦克斯韦定律](@entry_id:266368) $\nabla \times \mathbf{B} = \mu_0 \mathbf{J} + \mu_0 \epsilon_0 \frac{\partial \mathbf{E}}{\partial t}$ 中，最后一项是[位移电流](@entry_id:190231)。在回旋动理学的低频序下，我们可以评估其相对重要性。通过法拉第定律 $\nabla \times \mathbf{E} = -\partial_t \mathbf{B}$，我们可以得到场涨落大小的标度关系 $|\mathbf{E}| \sim (\omega/k_\perp)|\mathbf{B}|$。位移电流的大小为 $|\mu_0 \epsilon_0 \partial_t \mathbf{E}| \sim \mu_0 \epsilon_0 \omega |\mathbf{E}|$，而安培定律中磁场旋度项的大小为 $|\nabla \times \mathbf{B}| \sim k_\perp |\mathbf{B}|$。

这两项的比值为：
$$
\frac{|\mu_0 \epsilon_0 \partial_t \mathbf{E}|}{|\nabla \times \mathbf{B}|} \sim \frac{\mu_0 \epsilon_0 \omega |\mathbf{E}|}{k_\perp |\mathbf{B}|} = \frac{1}{c^2} \frac{\omega}{k_\perp} \frac{|\mathbf{E}|}{|\mathbf{B}|} \sim \frac{1}{c^2} \left(\frac{\omega}{k_\perp}\right)^2 = \left(\frac{v_{\text{phase},\perp}}{c}\right)^2
$$
其中 $v_{\text{phase},\perp} = \omega/k_\perp$ 是波的垂直相速度，$c$ 是光速。对于等离子体中的低频波（如[阿尔芬波](@entry_id:261195)），其相速度远小于光速。因此，这个比值远小于1，位移电流项可以被安全地忽略。 这是一个基本近似，它将麦克斯韦方程组从双曲型（波动）简化为椭圆/抛物线型（扩散/约束）。

#### 静电极限及其有效性

最简单的[回旋动理学模型](@entry_id:1125859)是**静电模型**。该模型假设所有扰动都是由[标量势](@entry_id:276177) $\phi$ 引起的[静电场](@entry_id:268546) $\mathbf{E} = -\nabla \phi$ 产生的，完全忽略了磁场扰动，即矢量势 $A_\parallel = 0$ 和平行磁场涨落 $\delta B_\parallel = 0$。

这个极限的有效性取决于两个条件：
1.  **忽略压缩性[磁涨落](@entry_id:1127582) ($\delta B_\parallel \approx 0$)的条件**: 垂直方向的[力平衡](@entry_id:267186)要求[等离子体动理学](@entry_id:187918)压力与磁压力之和的涨落为零，即 $\delta P_\perp + B \delta B_\parallel / \mu_0 \approx 0$。这导致 $\delta B_\parallel / B \sim \beta (e\phi/T)$，其中 $\beta \equiv 2\mu_0 n T / B^2$ 是等离子体贝塔值（[热压](@entry_id:159509)与[磁压](@entry_id:272413)之比）。为了使磁场涨落对粒子能量的贡献 $(\mu \delta B_\parallel)$ 远小于[电势能](@entry_id:260623) $(q_s\phi)$，必须满足 $\beta \ll 1$。

2.  **忽略剪切性[磁涨落](@entry_id:1127582) ($A_\parallel \approx 0$)的条件**: 该条件等价于要求静[电漂移](@entry_id:273751)波与[剪切阿尔芬波](@entry_id:1131551)[解耦](@entry_id:160890)。[漂移波](@entry_id:188488)的[特征频率](@entry_id:911376)约为 $\omega_{*e} \sim k_\perp \rho_s c_s / L_n$，而剪切阿尔芬波的频率为 $\omega_A = k_\parallel v_A$。[解耦](@entry_id:160890)条件为 $\omega_{*e} \ll \omega_A$。利用[阿尔芬速度](@entry_id:274944) $v_A \approx c_s \sqrt{2/\beta_e}$（对于$T_e \sim T_i$），并假设 $k_\perp \rho_s \sim 1$ 和 $k_\parallel \sim 1/L_n$，此条件最终简化为 $\beta (k_\perp \rho_s)^2 \ll 1$。

综上所述，静电极限在**低$\beta$**等离子体中（$\beta \ll 1$ 且 $\beta k_\perp^2 \rho_s^2 \ll 1$）是有效的。在此近似下，模型无法描述依赖于磁场涨落的物理现象，例如：[剪切阿尔芬波](@entry_id:1131551)、动理学阿尔芬波、磁场[抖动](@entry_id:200248)输运、微撕裂模和漂移撕裂模，以及与磁压平衡相关的效应（如动理学气球模）。当这些电磁效应变得重要时，必须采用包含 $A_\parallel$ 和/或 $\delta B_\parallel$ 演化的**电磁[回旋动理学模型](@entry_id:1125859)**。

### [回旋动理学泊松方程](@entry_id:1125862)：[准中性](@entry_id:197419)约束

在静电模型中，[标量势](@entry_id:276177) $\phi$ 由场方程决定。对于尺度远大于德拜长度（$k_\perp \lambda_D \ll 1$）的慢变过程，等离子体保持局部电荷[准中性](@entry_id:197419)。因此，[高斯定律](@entry_id:141493) $\nabla \cdot \mathbf{E} = \rho_c/\epsilon_0$ 被简化为一个代数[约束方程](@entry_id:138140)，即净电荷密度为零：
$$
\sum_s q_s \delta n_s = 0
$$
其中 $\delta n_s$ 是物种 $s$ 的粒子数[密度扰动](@entry_id:159546)。这个方程被称为**[回旋动理学泊松方程](@entry_id:1125862)**或**[准中性](@entry_id:197419)方程**。

为了求解该方程，我们需要将粒子密度扰动 $\delta n_s$ 用[导心](@entry_id:200181)[分布函数](@entry_id:145626) $F_s$ 表示。粒子密度是真实空间 $(\mathbf{r}, \mathbf{v})$ 中的分布函数 $f_s$ 的零阶[速度矩](@entry_id:1133763)。通过坐标变换，可以证明 $\delta n_s$ 由两部分构成，最终得到如下形式的[准中性](@entry_id:197419)方程：
$$
\sum_s q_s \int d^3v\, \langle \delta f_s \rangle - \sum_s \frac{n_{0s} q_s^2}{T_s} \left(1 - \Gamma_0(b_s)\right) \phi = 0
$$
这里 $n_{0s}$ 和 $T_s$ 是平衡密度和温度。这个方程的两个主要项具有明确的物理意义：
1.  **非绝[热导](@entry_id:189019)心[电荷密度](@entry_id:144672)** $\sum_s q_s \int d^3v\, \langle \delta f_s \rangle$：这是由导心[分布函数](@entry_id:145626)的非绝热部分产生的电荷密度。其中 $\langle \delta f_s \rangle$ 是[回旋平均](@entry_id:1125848)后的分布函数扰动，它由回旋动理学方程求解得到。
2.  **极化[电荷密度](@entry_id:144672)** $-\sum_s \frac{n_{0s} q_s^2}{T_s} (1 - \Gamma_0(b_s)) \phi$：这是由[有限拉莫尔半径效应](@entry_id:1125111)引起的有效电荷密度。它的物理来源是，在电场作用下，粒子围绕导心作[回旋运动](@entry_id:204632)，形成一个电荷环。这个环在电势中的平均位置与导心位置不同，导致了净电荷的偶极矩，从而产生了**极化密度**。

#### [有限拉莫尔半径效应](@entry_id:1125111)与 $\Gamma_0$ 因子

极化密度项中的关键因子是 $\Gamma_0(b_s)$。它精确地描述了FLR效应对电荷密度的修正。这个函数是通过对[回旋平均](@entry_id:1125848)算子（在傅里叶空间中为贝塞尔函数 $J_0$）在麦克斯韦速度分布上进行加权平均得到的：
$$
\Gamma_0(b_s) \equiv \langle J_0^2(k_\perp \rho_s) \rangle_{v,M} = I_0(b_s) e^{-b_s}
$$
其中 $b_s \equiv k_\perp^2 \rho_{ts}^2$（有时也定义为 $k_\perp^2 \rho_{ts}^2/2$），$\rho_{ts}$ 是物种 $s$ 的热[拉莫尔半径](@entry_id:197083)，$I_0$是第一类零阶[修正贝塞尔函数](@entry_id:184177)。

函数 $\Gamma_0(b_s)$ 的行为揭示了FLR效应的本质：
*   **长波极限 ($b_s \ll 1$)**：$\Gamma_0(b_s) \approx 1 - b_s + \frac{3}{4}b_s^2 + \dots$。此时，极化密度项中的因子 $1 - \Gamma_0(b_s) \approx b_s \approx k_\perp^2 \rho_{ts}^2$。这恢复了与流体模型中[极化漂移](@entry_id:187707)相关联的、正比于 $-k_\perp^2 \phi$ 的经典极化效应。
*   **短波极限 ($b_s \gg 1$)**：$\Gamma_0(b_s) \sim (2\pi b_s)^{-1/2}$，趋近于零。这意味着在波长远小于[拉莫尔半径](@entry_id:197083)时，粒子在其回旋轨道上感受到的电场被极大地平均掉了，导致其响应减弱。

因此，$\Gamma_0$ 因子是连接动理学效应和流体图像的桥梁，它精确地编码了所有尺度的FLR平滑效应。

#### 离子与[电子极化](@entry_id:145269)的比较

在离子尺度的[湍流](@entry_id:151300)中（$k_\perp \rho_i \sim 1$），由于质量差异巨大 ($m_i \gg m_e$)，即使温度相当 ($T_i \sim T_e$)，离子和电子的[拉莫尔半径](@entry_id:197083)也相差悬殊：$\rho_i \gg \rho_e$。具体而言，$\rho_e / \rho_i \approx \sqrt{m_e/m_i}$。

这导致了它们对极化密度的贡献截然不同：
*   **离子**：$k_\perp \rho_i \sim 1 \implies b_i \sim 1$。因此，离子的极化项 $1-\Gamma_0(b_i)$ 是一个 $\mathcal{O}(1)$ 的量。
*   **电子**：$k_\perp \rho_e \ll 1 \implies b_e \ll 1$。因此，电子的极化项 $1-\Gamma_0(b_e) \approx b_e = (k_\perp \rho_e)^2 = (k_\perp \rho_i)^2 (\rho_e/\rho_i)^2 \sim m_e/m_i$。

结论是，在离子尺度的涨落中，[电子极化](@entry_id:145269)密度比[离子极化密度](@entry_id:1126726)小一个[质量比](@entry_id:167674)因子 $m_e/m_i$。因此，在研究离子尺度现象时，通常可以忽略电子的极化效应。然而，这个近似依赖于尺度。在研究电子尺度[湍流](@entry_id:151300)时（$k_\perp \rho_e \sim 1$），[电子极化](@entry_id:145269)变得至关重要，不可忽略。

### [回旋动理学安培定律](@entry_id:1125854)：平行电流的响应

在电磁模型中，除了求解 $\phi$ 的[准中性](@entry_id:197419)方程外，还必须求解决定矢量势 $A_\parallel$ 的[演化方程](@entry_id:268137)。这个方程就是平行方向的[安培定律](@entry_id:140092)。如前所述，[位移电流](@entry_id:190231)可以忽略，因此安培定律简化为 $\nabla \times \mathbf{B} = \mu_0 \mathbf{J}$。

利用 $\mathbf{B} = \nabla \times \mathbf{A}$ 和矢量恒等式 $\nabla \times (\nabla \times \mathbf{A}) = \nabla(\nabla \cdot \mathbf{A}) - \nabla^2 \mathbf{A}$，在[库仑规范](@entry_id:273044) $\nabla \cdot \mathbf{A} = 0$ 下，我们得到 $-\nabla^2 \mathbf{A} = \mu_0 \mathbf{J}$。取其平行分量，并利用回旋动理学序 $k_\parallel \ll k_\perp$ 来近似[拉普拉斯算子](@entry_id:146319) $\nabla^2 \approx \nabla_\perp^2$，我们得到**[回旋动理学安培定律](@entry_id:1125854)**：
$$
-\nabla_\perp^2 A_\parallel = \mu_0 J_\parallel
$$
这个方程是一个关于 $A_\parallel$ 的二维泊松型方程，其源项是平行电流密度 $J_\parallel$。

与[准中性](@entry_id:197419)方程类似，源项 $J_\parallel$ 必须由动理学理论给出。它是所有物种平行速度的一阶[速度矩](@entry_id:1133763)：
$$
J_\parallel = \sum_s q_s \int v_\parallel \langle \delta f_s \rangle d^3v
$$
其中，积分是在导心[速度空间](@entry_id:181216)中进行的，并且再次使用了回旋平均后的[分布函数](@entry_id:145626)。

值得强调的是，平行[位移电流](@entry_id:190231) $\epsilon_0 \partial_t E_\parallel$ 的忽略有更严格的理由。与平行传导电流 $J_\parallel$（主要由快速移动的电子携带）相比，其大小之比可以标度为 $\omega^2 / \omega_{pe}^2$，其中 $\omega_{pe}$ 是电子等离子体频率。由于在典型[聚变等离子体](@entry_id:1125407)中 $\omega \ll \omega_{pe}$，该项确实可以忽略不计。

### 物理的耦合：[广义欧姆定律](@entry_id:180191)与规范选择

在电磁模型中，电场和磁场通过势 $\phi$ 和 $\mathbf{A}$ 联系在一起。平行电场 $E_\parallel$ 是连接这两个势的关键物理量，其定义为：
$$
E_\parallel = -\nabla_\parallel \phi - \frac{\partial A_\parallel}{\partial t}
$$
这个关系式直接源于电场的定义 $\mathbf{E} = -\nabla\phi - \partial_t\mathbf{A}$。$E_\parallel$ 是一个[物理可观测量](@entry_id:154692)，它在电磁[规范变换](@entry_id:176521) $\phi \to \phi - \partial_t \chi$, $\mathbf{A} \to \mathbf{A} + \nabla \chi$ 下保持不变。

物理上，平行电场 $E_\parallel$ 受到等离子体响应的制约。通过取动理学方程的平行[速度矩](@entry_id:1133763)，可以得到一个描述 $E_\parallel$ 与平行电流 $j_\parallel$、压力梯度等关系的**广义欧姆定律**，例如：
$$
E_\parallel \approx \eta j_\parallel - \frac{1}{n_e e} \nabla_\parallel p_e - \frac{m_e}{e} \frac{du_{e\parallel}}{dt} + \dots
$$
其中包含电阻效应 $(\eta j_\parallel)$、电子压力梯度、电子惯性等项。

在[数值模拟](@entry_id:146043)中，虽然 $E_\parallel$ 本身是规范不变的，但它的两个组成部分 $-\nabla_\parallel\phi$ 和 $-\partial_t A_\parallel$ 却依赖于规范选择。这意味着[数值算法](@entry_id:752770)可以利用这种自由度。例如，通过选择特定的[规范函数](@entry_id:749731) $\chi$，可以将产生 $E_\parallel$ 的“责任”在求解 $\phi$ 的[椭圆方程](@entry_id:169190)和求解 $A_\parallel$ 的时间[演化方程](@entry_id:268137)之间进行分配。这种选择不改变最终的物理结果，但会深刻影响数值求解器的稳定性、收敛性和[计算效率](@entry_id:270255)。

### [非线性](@entry_id:637147)机制：相空间中的[湍流](@entry_id:151300)输运

线性的回旋动理学模型描述了小扰动（波）的[色散关系](@entry_id:140395)和[线性不稳定性](@entry_id:1127282)。然而，[等离子体湍流](@entry_id:186467)本质上是一个[非线性饱和](@entry_id:1128869)过程。[非线性](@entry_id:637147)项在[回旋动理学方程](@entry_id:1125856)中表现为相空间中的对流项，它描述了分布函数如何被涨落的场平流。

主要的[非线性](@entry_id:637147)项是**$\mathbf{E} \times \mathbf{B}$ 对流**和**磁场[抖动](@entry_id:200248)输运**。在[回旋动理学方程](@entry_id:1125856)中，这个[非线性](@entry_id:637147)对流项可以紧凑地写成一个泊松括号的形式：
$$
\left(\frac{c}{B} \mathbf{b} \times \nabla \langle \chi_s \rangle\right) \cdot \nabla h_s
$$
其中 $h_s$ 是[分布函数](@entry_id:145626)的非绝热部分，$\langle \cdot \rangle$ 代表[回旋平均](@entry_id:1125848)。这里的[广义势](@entry_id:175268) $\chi_s = \phi - \frac{v_\parallel}{c} A_\parallel$ 巧妙地结合了静电和电磁效应。

*   当只考虑 $\phi$ 时，该项退化为熟悉的**$\mathbf{E} \times \mathbf{B}$ 涡旋**，即 $\frac{c}{B}(\mathbf{b} \times \nabla \langle \phi \rangle) \cdot \nabla h_s$。它描述了[分布函数](@entry_id:145626)被电场漂移[涡旋拉伸](@entry_id:271418)和卷曲，从而将能量从大尺度输运到小尺度。

*   $A_\parallel$ 部分则引入了**磁场[抖动](@entry_id:200248)输运**，即 $-\frac{v_\parallel}{B}(\mathbf{b} \times \nabla \langle A_\parallel \rangle) \cdot \nabla h_s$。这对应于粒子沿着被扰动磁力线（由 $\delta \mathbf{B}_\perp = \nabla \times (A_\parallel \hat{\mathbf{b}})$ 描述）运动时产生的径向输运。

这些[非线性](@entry_id:637147)过程构成了[湍流](@entry_id:151300)的核心反馈回路。它们输运分布函数 $h_s$，在相空间中产生[精细结构](@entry_id:1124953)。演化后的 $h_s$ 的[速度矩](@entry_id:1133763)（电荷密度和电流密度）又通过[回旋动理学泊松方程](@entry_id:1125862)和安培定律，反过来决定了场 $\phi$ 和 $A_\parallel$ 的[时空结构](@entry_id:158931)。正是这个自洽的[非线性](@entry_id:637147)循环，最终决定了[湍流](@entry_id:151300)的饱和水平和相关的[反常输运](@entry_id:746472)。