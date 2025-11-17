## 引言
在一个相互作用的[量子多体系统](@entry_id:141221)中，[元激发](@entry_id:140859)或[准粒子](@entry_id:136584)是描述系统低能动力学的基石。然而，一个普遍但常被简化的事实是，这些[准粒子](@entry_id:136584)并非永恒存在，它们会通过相互作用而衰变，具有有限的寿命。理解这些衰变过程的微观机制，对于精确描述系统的动力学、输运性质和[相干性](@entry_id:268953)至关重要。本文旨在填补这一认知上的关键环节，系统地剖析导致[准粒子衰变](@entry_id:137436)的两种最基本的物理机制：内禀的[Beliaev阻尼](@entry_id:141908)和热驱动的[Landau阻尼](@entry_id:137619)。

为了构建一个完整而深入的理解框架，本文将分为三个核心部分。首先，在“原理与机制”一章中，我们将奠定理论基础，从谱函数的概念出发，将[准粒子寿命](@entry_id:145453)与[可观测量](@entry_id:267133)联系起来。随后，我们将详细辨析[Beliaev阻尼](@entry_id:141908)和[Landau阻尼](@entry_id:137619)的物理图像、运动学[守恒定律](@entry_id:269268)，以及它们在不同参数区域下的主导作用。接着，在“应用与[交叉](@entry_id:147634)学科联系”一章中，我们将展示这些理论的强大生命力，探讨它们如何在玻色-爱因斯坦凝聚体的杂质动力学、奇异量子气体、[拓扑激发](@entry_id:157702)等前沿问题中发挥作用，并追溯其在等离子体物理和凝聚态物理中的普适性根源。最后，“动手实践”部分将通过一系列计算问题，帮助读者巩固对阻尼过程[运动学](@entry_id:173318)和标度率的理解。通过这一层层深入的探索，读者将掌握分析[多体系统](@entry_id:144006)中耗散现象的核心工具。

## 原理与机制

继前一章对[玻色-爱因斯坦凝聚](@entry_id:144849)（BEC）中[元激发](@entry_id:140859)的基本描述之后，我们现在深入探讨这些[准粒子](@entry_id:136584)并非无限寿命这一重要事实。在一个相互作用的[量子多体系统](@entry_id:141221)中，[准粒子](@entry_id:136584)代表了系统真实本征态的近似描述。它们之间的[剩余相互作用](@entry_id:159129)，或与系统其他自由度的耦合，会导致它们衰变，从而获得有限的寿命。本章将系统地阐述导致[准粒子衰变](@entry_id:137436)的两种主要机制：**Beliaev 阻尼**和**Landau 阻尼**，并探讨它们的[运动学](@entry_id:173318)条件、物理起源以及在不同物理情境下的表现。

### [准粒子寿命](@entry_id:145453)与[谱函数](@entry_id:147628)

理解[准粒子衰变](@entry_id:137436)的第一步是将其与可观测量联系起来。一个[准粒子](@entry_id:136584)的有限寿命意味着其能量不是精确定义的。根据[能量-时间不确定性原理](@entry_id:148140)，一个寿命为 $\tau$ 的状态，其能量不确定度 $\Delta E \sim \hbar/\tau$。在[多体理论](@entry_id:169452)的框架中，这种能量展宽表现为[准粒子](@entry_id:136584)**自能（self-energy）** $\Sigma(\mathbf{p}, \omega)$ 的虚部。

系统的激发谱通常通过**[动态结构因子](@entry_id:143433)（dynamic structure factor）** $S(\mathbf{p}, \omega)$ 来探测，它与中子或光散射实验的[截面](@entry_id:154995)直接相关。在理论上，$S(\mathbf{p}, \omega)$ 与[准粒子](@entry_id:136584)**[谱函数](@entry_id:147628)（spectral function）** $A(\mathbf{p}, \omega)$ 成正比。谱函数本身由[准粒子](@entry_id:136584)的**[格林函数](@entry_id:147802)（Green's function）** $G(\mathbf{p}, \omega)$ 决定：

$$
A(\mathbf{p}, \omega) = -\frac{1}{\pi} \text{Im}[G(\mathbf{p}, \omega)]
$$

在一个包含[自能修正](@entry_id:754667)的近似中，格林函数的形式为：

$$
G(\mathbf{p}, \omega) = \frac{Z_p}{\omega - E_p - \Sigma(\mathbf{p}, \omega)}
$$

其中 $E_p$ 是[准粒子](@entry_id:136584)的裸能量（例如，Bogoliubov [色散](@entry_id:263750)），$Z_p$ 是[准粒子权重](@entry_id:140100)。自能 $\Sigma(\mathbf{p}, \omega) = \Delta E_p(\omega) - i\Gamma_p(\omega)$ 是一个复数，其实部 $\Delta E_p$ 导致了[准粒子能量](@entry_id:173936)的移动，而其虚部 $\Gamma_p$ 则代表了总的**阻尼率（damping rate）**或[衰变率](@entry_id:156530)的半值。

为了看清阻尼率与实验观测的联系，我们考虑一个常见情形：在能量峰 $\tilde{E}_p = E_p + \Delta E_p$ 附近，自能的虚部 $\Gamma_p$ 可以近似为一个常数，即 $\Gamma_p(\omega) \approx \Gamma_p(\tilde{E}_p)$。在这种情况下，[谱函数](@entry_id:147628)呈现一个**[洛伦兹线型](@entry_id:165845)（Lorentzian profile）** [@problem_id:1229850]：

$$
A(\mathbf{p}, \omega) = -\frac{1}{\pi} \text{Im}\left[ \frac{Z_p}{(\omega - \tilde{E}_p) + i\Gamma_p} \right] = \frac{Z_p}{\pi} \frac{\Gamma_p}{(\omega - \tilde{E}_p)^2 + \Gamma_p^2}
$$

这是一个以 $\tilde{E}_p$ 为中心，宽度由 $\Gamma_p$ 决定的峰。其**半高全宽（Full Width at Half Maximum, FWHM）** 可以通过求解 $A(\mathbf{p}, \omega) = \frac{1}{2} A_{max}$ 来确定。峰值在 $\omega = \tilde{E}_p$ 处，值为 $A_{max} = Z_p / (\pi \Gamma_p)$。半高处的频率 $\omega$ 满足 $(\omega - \tilde{E}_p)^2 + \Gamma_p^2 = 2\Gamma_p^2$，即 $|\omega - \tilde{E}_p| = \Gamma_p$。因此，两个半高点之间的总宽度为：

$$
\text{FWHM} = 2\Gamma_p
$$

这个简单的关系是至关重要的：它直接将微观的[衰变率](@entry_id:156530) $\Gamma_p$ 与宏观可测的[谱线宽度](@entry_id:168313)联系起来。因此，通过测量[动态结构因子](@entry_id:143433)的谱峰宽度，我们可以实验性地确定[准粒子](@entry_id:136584)的寿命。接下来的部分将讨论贡献于 $\Gamma_p$ 的具体物理过程。

### Beliaev 阻尼：零温下的内禀衰变

即使在绝对[零度](@entry_id:156285)，当不存在[热激发](@entry_id:275697)时，一个[准粒子](@entry_id:136584)仍然可能是不稳定的。**Beliaev 阻尼（Beliaev damping）**描述的就是这样一个内禀的、$T=0$ 的衰变过程：一个[准粒子](@entry_id:136584)自发地衰变为两个其他[准粒子](@entry_id:136584)。

#### 运动学条件

这个 $1 \to 2$ 的衰变过程必须同时遵守[能量守恒](@entry_id:140514)和动量守恒。若一个初始动量为 $\mathbf{p}$ 的[准粒子衰变](@entry_id:137436)为两个动量分别为 $\mathbf{p}_1$ 和 $\mathbf{p}_2$ 的[准粒子](@entry_id:136584)，则必须满足：

$$
\mathbf{p} = \mathbf{p}_1 + \mathbf{p}_2
$$
$$
\epsilon_p = \epsilon_{p_1} + \epsilon_{p_2}
$$

其中 $\epsilon_k$ 是动量为 $k$ 的[准粒子](@entry_id:136584)的能量（[色散关系](@entry_id:140395)）。这两个条件能否同时满足，完全取决于色散关系 $\epsilon_p$ 的函数形式。

一个普遍而直观的准则是，Beliaev 阻尼的发生需要[色散关系](@entry_id:140395)至少在某个动量区间内具有**向下弯曲（downward-bending）**的特性，即具有**[凹性](@entry_id:139843)（concavity）**，其数学条件为 $\epsilon''(p)  0$（其中 $p = |\mathbf{p}|$）。如果[色散曲线](@entry_id:197598)是处处**凸的（convex）**，即 $\epsilon''(p) \ge 0$ 对所有 $p$ 成立，那么[能量守恒](@entry_id:140514)条件 $\epsilon_p = \epsilon_{p_1} + \epsilon_{p_2}$ 将无法与[动量守恒](@entry_id:149964) $\mathbf{p} = \mathbf{p}_1 + \mathbf{p}_2$ 同时满足。这是因为对于凸函数，总有 $\epsilon_{p_1} + \epsilon_{p_2}  \epsilon_{p_1+p_2}$（不考虑矢量方向时）。

在准一维 BEC 中，由于横向限制效应，[元激发](@entry_id:140859)的色散关系可以呈现非平凡的形状。考虑一个由动量相关的相互作用导致的模型 [@problem_id:1229763]，其色散关系为：

$$
\epsilon(p) = \sqrt{\left(\frac{p^2}{2m}\right)^2 + \frac{\mu}{m} p^2 \left(1 - \frac{p^2}{\Lambda^2}\right)}
$$

其中 $\mu$ 是化学势，$\Lambda$ 是由横向囚禁决定的动量尺度。在此，我们可以通过分析 $\epsilon''(p)$ 的符号来判断 Beliaev 阻尼是否被允许。计算表明，只有当[色散](@entry_id:263750)函数存在拐点（$\epsilon''(p)=0$）并进入[凹性](@entry_id:139843)区域时，衰变才有可能。这要求系数 $(\frac{1}{4m^2} - \frac{\mu}{m\Lambda^2})$ 为负，从而给出了一个临界化学势 $\mu_c$。当 $\mu  \mu_c = \frac{\Lambda^2}{4m}$ 时，色散曲线在高动量区域出现[凹性](@entry_id:139843)，Beliaev 阻尼的[运动学](@entry_id:173318)条件得以满足。反之，若 $\mu \le \mu_c$，[色散曲线](@entry_id:197598)处处为凸，系统中的所有[准粒子](@entry_id:136584)都对 Beliaev 衰变稳定。这展示了如何通过调控一个宏观参数（化学势）来开启或关闭一个基本的衰变通道。

#### 衰变阈值

对于标准的三维均匀 BEC，Bogoliubov 理论给出的色散关系为 $\epsilon_p = \sqrt{c^2 p^2 + (p^2/2m)^2}$，其中 $c$ 是声速。这是一个严格的[凸函数](@entry_id:143075)，因此，在[Bogoliubov近似](@entry_id:145204)下，[准粒子](@entry_id:136584)是无限寿命的，不存在 Beliaev 阻尼。

然而，超出平均场理论的修正（Beyond-mean-field corrections）会改变色散关系，尤其是在高动量区域。这些修正通常会导致[色散曲线](@entry_id:197598)在高动量处“软化”或向下弯曲，从而为 Beliaev 阻尼打开通道。考虑一个[唯象模型](@entry_id:273816)，其中高动量行为被修正为 [@problem_id:1229847]：

$$
\epsilon_p = \sqrt{c^2 p^2 + \left(\frac{p^2}{2m}\right)^2 - A p^6}
$$

其中 $A  0$ 是一个小的正常数，代表了超出-Bogoliubov 近似的效应。由于这个修正项，色散曲线在高动量下可能出现[凹性](@entry_id:139843)。衰变通道的开启存在一个**阈值动量（threshold momentum）** $p_{th}$。通常，能量上最容易满足的衰变过程是共线衰变，即产生的两个[准粒子](@entry_id:136584)与原[准粒子](@entry_id:136584)动量方向相同。其中最简单的情形是衰变为两个动量相等的粒子，$\mathbf{p}_1 = \mathbf{p}_2 = \mathbf{p}/2$。该过程的阈值由[能量守恒](@entry_id:140514)的临界条件 $\epsilon_{p_{th}} = 2\epsilon_{p_{th}/2}$ 给出。

对于上述色散关系，我们有：

$$
c^2 p_{th}^2 + \frac{p_{th}^4}{4m^2} - A p_{th}^6 = 4 \left[ c^2 \left(\frac{p_{th}}{2}\right)^2 + \frac{1}{4m^2}\left(\frac{p_{th}}{2}\right)^4 - A \left(\frac{p_{th}}{2}\right)^6 \right]
$$

化简后得到 $3p_{th}^4 = 15Am^2p_{th}^6$。解出非零的阈值动量为：

$$
p_{th} = \frac{1}{m\sqrt{5A}}
$$

当一个[准粒子](@entry_id:136584)的动量 $p  p_{th}$ 时，$\epsilon_p  2\epsilon_{p/2}$，衰变通道打开；而当 $p  p_{th}$ 时，衰变在[运动学](@entry_id:173318)上被禁止。其他形式的唯象修正，例如将自由粒子能量项 $p^2/2m$ 修改为 $p^2/2m - \alpha p^4$ [@problem_id:1229745]，也会得到类似的结果：即存在一个由超出平均场效应决定的临界动量，标志着 Beliaev 阻尼的开启。

#### 运动学条件的微妙之处

值得注意的是，“[凹性](@entry_id:139843)”是 Beliaev 阻尼发生的一个充分条件，但并非绝对必要。更精确的判据是，是否存在 $\mathbf{p}_1, \mathbf{p}_2$ 使得 $\mathbf{p} = \mathbf{p}_1 + \mathbf{p}_2$ 且 $\epsilon_p = \epsilon_{p_1} + \epsilon_{p_2}$。考虑一个假想的凸色散关系 $\epsilon_p = C p^{3/2}$（其中 $C  0$）[@problem_id:1160790]。尽管 $\epsilon''(p) = \frac{3}{4} C p^{-1/2}  0$ 处处为正，但衰变仍然是可能的。这是因为该[色散关系](@entry_id:140395)的**相速度** $\epsilon_p/p = C p^{1/2}$ 是动量 $p$ 的增函数。在这种情况下，虽然曲线是凸的，但它向上弯曲得“不够快”，以至于一个高能[准粒子](@entry_id:136584)的能量仍然可以等于两个低能[准粒子能量](@entry_id:173936)之和。这提醒我们，在分析[准粒子](@entry_id:136584)稳定性时，必须仔细检验能量和动量守恒定律，而不能仅仅依赖于色散曲线的局部曲率。

### Landau 阻尼：热效应与碰撞

与 $T=0$ 的内禀 Beliaev 衰变不同，**Landau 阻尼（Landau damping）**是一种依赖于环境的阻尼机制。在有限温度下，系统中存在一个由热激发的[准粒子](@entry_id:136584)（[声子](@entry_id:140728)）组成的气体。Landau 阻尼的本质是一个[准粒子](@entry_id:136584)与这些热[声子](@entry_id:140728)发生**碰撞（scattering）**而改变其状态的过程。

#### 物理机制

在低温下的 BEC 中，最主要的 Landau 阻尼过程是目标[准粒子](@entry_id:136584)（动量 $\mathbf{p}$）与一个热[声子](@entry_id:140728)（动量 $\mathbf{q}_{th}$）的散射：

$$
\text{quasiparticle}(\mathbf{p}) + \text{phonon}(\mathbf{q}_{th}) \leftrightarrow \text{quasiparticle}(\mathbf{p}') + \text{phonon}(\mathbf{q}'_{th})
$$

这是一个 $2 \to 2$ 的散射过程。由于它依赖于热[声子](@entry_id:140728)的存在，其速率强烈依赖于温度。当温度趋于零时，热[声子](@entry_id:140728)密度消失，Landau 阻尼也随之消失。

#### 微观起源与阻尼率

Landau 阻尼率的大小最终由[准粒子](@entry_id:136584)间的散射截面决定。在 BEC 的[声学](@entry_id:265335)（phonon）区域，[准粒子](@entry_id:136584)具有线性[色散](@entry_id:263750) $\epsilon_p = cp$。两个这样的[声子](@entry_id:140728)可以相互散射。这个过程是 BEC 中实现热平衡和产生[流体动力学](@entry_id:136788)行为（如声波衰减）的基础。

考虑两个[声子](@entry_id:140728)以相对动量 $2p$ 碰撞。其[微分散射截面](@entry_id:172304)可以从微扰理论计算得出。对于一个三维[弱相互作用](@entry_id:157579) BEC，在[质心系](@entry_id:168444)中，该[截面](@entry_id:154995)具有以下形式 [@problem_id:1229832]：

$$
\frac{d\sigma}{d\Omega} = K p^6 |1 + u \cos^2\theta|^2
$$

其中 $K$ 是与[相互作用强度](@entry_id:192243)和凝聚体密度相关的常数，$u$ 是一个无量纲参数（对于 Gross-Pitaevskii 方程描述的 BEC，$u=2$），$\theta$ 是散射角。通过对所有[立体角](@entry_id:154756)积分，可以得到[总散射截面](@entry_id:168963) $\sigma$。这个[截面](@entry_id:154995) $\sigma \propto p^6$ 的强烈动量依赖性，反映了低能[声子](@entry_id:140728)之间相互作用的弱性。

这个微观的散射截面构成了计算宏观 Landau 阻尼率 $\Gamma_L$ 的基础。通过[玻尔兹曼方程](@entry_id:141554)或费米黄金法则，可以将散射截面与温度和粒子动量联系起来，得到阻尼率的标度律。

#### 不同阻尼机制的比较

Beliaev 阻尼和 Landau 阻尼源于不同的物理过程，并表现出截然不同的依赖关系。在低温 ($k_B T \ll mc^2$) 和低动量 ($p \ll mc$) 的三维 BEC 中，它们各自的阻尼率近似为 [@problem_id:1160786]：

-   **Beliaev Damping**: $\Gamma_B(p) \propto p^5$。此过程与温度无关，但在低动量下被 $p^5$ 的高次幂强烈抑制。
-   **Landau Damping**: $\Gamma_L(p) \propto p T^4$。此过程正比于动量 $p$，并强烈依赖于温度（$T^4$ 源于三维[声子态密度](@entry_id:199476)和占据数）。

由于它们的标度律不同，这两种机制在不同的参数区域占据主导地位。在固定温度下，当动量 $p$ 很小时，线性的 $p$ 依赖使得 Landau 阻尼占优。而当动量 $p$ 增大时，$p^5$ 的快速增长会使 Beliaev 阻尼最终超过 Landau 阻尼（前提是 $p$ 已超过 Beliaev 阻尼的阈值 $p_{th}$）。

我们可以通过令 $\Gamma_B(p) = \Gamma_L(p)$ 来求解**[交叉](@entry_id:147634)动量（crossover momentum）** $p_{cross}$：

$$
\frac{3 p_{cross}^5}{640 \pi m \hbar^4 n_0} = \frac{3\pi p_{cross} (k_B T)^4}{10 m n_0 \hbar^4 c^4}
$$

解得：

$$
p_{cross} = \frac{2 \sqrt{2 \pi} k_B T}{c}
$$

这个结果清晰地展示了两种阻尼机制的竞争与共存：对于动量 $p \ll p_{cross}$ 的[准粒子](@entry_id:136584)，其寿命主要由与[热浴](@entry_id:137040)的碰撞决定（Landau 阻尼）；而对于动量 $p \gg p_{cross}$ 的高能[准粒子](@entry_id:136584)，其主要衰变通道是自发的 Beliaev 衰变。

### 相互作用与高等修正

#### Beliaev 阻尼与超流

一个重要且需澄清的概念是 Beliaev 阻尼与**超流（superfluidity）**的 Landau 判据之间的关系 [@problem_id:1160805]。Landau 判据指出，[超流体](@entry_id:180718)能够无耗散地流动，只要其速度 $v$ 低于[临界速度](@entry_id:161155) $v_c = \min_p (\epsilon_p / p)$。这个判据保证了从超流体[基态](@entry_id:150928)**产生**一个[准粒子](@entry_id:136584)在能量上是不被允许的。

Beliaev 阻尼描述的是一个**已经存在**的[准粒子](@entry_id:136584)的**衰变**，而不是从[基态](@entry_id:150928)产生一个[准粒子](@entry_id:136584)。这两个是截然不同的物理过程。即使系统中存在动量高于 $p_{c}$ 的[准粒子](@entry_id:136584)，它们会通过 Beliaev 阻尼衰变，但这并不意味着超流体本身是不稳定的。只要流速 $v  v_c$，[超流体](@entry_id:180718)背景就无法产生任何新的[元激发](@entry_id:140859)，从而保持其无耗散特性。因此，Beliaev 阻尼的存在**不违反**超流的 Landau 判据。

#### 对阻尼阈值的修正

我们之前讨论的 Beliaev 阻尼阈值是基于简化的模型。在更精确的理论中，必须考虑[多体效应](@entry_id:173569)对[色散关系](@entry_id:140395)的修正。一个重要的效应是**量子耗尽（quantum depletion）**。即使在 $T=0$，原子间的相互作用也会导致一部分原子被“踢出”凝聚体，形成一个非凝聚的原子云。

在 Popov 近似下，三维 BEC 的量子耗尽密度 $n_{dep}$ 正比于 $(gn)^{3/2}$。这意味着真实的凝聚体密度 $n_0$ 小于总原子密度 $n$，即 $n_0 = n - n_{dep}$。如果色散关系的参数依赖于凝聚体密度 $n_0$（例如声速 $c(n_0)$），那么量子耗尽就会间接地修正[色散曲线](@entry_id:197598)，从而移动 Beliaev 阻尼的阈值 [@problem_id:1229776]。例如，在一个[色散](@entry_id:263750)为 $\omega_k = c(n_0) k + A(n_0) k^2 - B k^3$ 的模型中，阈值 $k_{th}$ 正比于 $A(n_0) \propto 1/\sqrt{n_0}$。由于量子耗尽使得 $n_0$ 减小，阈值动量 $k_{th}$ 将会有一个正向的移动。这体现了[多体理论](@entry_id:169452)中不同效应之间深刻的自洽性：[基态](@entry_id:150928)的[量子涨落](@entry_id:154889)（耗尽）会反过来影响激发谱的稳定性和动力学。

#### 阻尼过程的阻尼

最后，我们考虑一个更为精细的效应：Beliaev 阻尼和 Landau 阻尼之间的相互作用。Beliaev 阻尼是一个 $1 \to 2$ 的过程，其中产生的两个[准粒子](@entry_id:136584)是“[虚粒子](@entry_id:147959)”，它们只在衰变过程中短暂存在。然而，在有限温度下，这两个[虚粒子](@entry_id:147959)本身也浸润在[热浴](@entry_id:137040)中，并会经历 Landau 阻尼。

这个“阻尼过程的阻尼”可以通过更高级的[场论](@entry_id:155241)方法来描述 [@problem_id:1229760]。在计算 Beliaev 阻尼率的自能图中，中间态[准粒子](@entry_id:136584)的[传播子](@entry_id:139558)（propagator）会获得一个由 Landau 阻尼率 $\Gamma_L$ 决定的虚部。这导致最终计算出的 Beliaev 阻尼率 $\Gamma_B$ 本身也获得了温度依赖性。在 $T=0$ 的衰变阈值附近，这种效应引入了一个正比于 $1/T^2$ 的对[Beliaev阻尼](@entry_id:141908)率的热修正。这揭示了在相互作用[多体系统](@entry_id:144006)中，各种阻尼机制并非孤立存在，而是以复杂而有趣的方式相互交织在一起。