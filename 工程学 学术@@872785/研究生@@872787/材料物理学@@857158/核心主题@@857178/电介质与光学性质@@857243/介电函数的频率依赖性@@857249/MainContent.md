## 引言
[介电函数](@entry_id:136859)是描述材料如何响应外加[电场](@entry_id:194326)的关键物理量，是理解光与物质相互作用的核心。然而，这种响应并非一成不变，而是强烈地依赖于[电场](@entry_id:194326)变化的频率。理解[介电函数](@entry_id:136859)的频率依赖性，是从根本上揭示材料[电子结构](@entry_id:145158)、[晶格动力学](@entry_id:145448)以及[多体相互作用](@entry_id:751663)的窗口。本文旨在系统性地解决“材料的[介电响应](@entry_id:140146)为何及如何随频率变化”这一核心问题，为读者构建一个从基础原理到前沿应用的完整知识框架。

在接下来的内容中，我们将分三步深入探索这一主题。首先，在“原理与机制”一章中，我们将建立介电函数的宏观定义与微观物理图像，介绍Kramers-Kronig关系等基本约束，并详细阐述经典的Drude和[Lorentz模型](@entry_id:144803)，最后延伸至晶体中的[空间色散](@entry_id:141344)和[多体效应](@entry_id:173569)等复杂现象。随后，在“应用与跨学科交叉”一章中，我们将展示这些理论如何在电磁学、凝聚态物理、[材料科学](@entry_id:152226)、计算化学等多个领域中得到应用，以解决从金属[趋肤深度](@entry_id:270307)到超构[材料设计](@entry_id:160450)等实际问题。最后，通过“动手实践”环节，读者将有机会运用所学知识解决具体问题，加深对核心概念的理解。

## 原理与机制

本章旨在深入探讨材料介电函数的频率依赖性背后的基本原理与微观机制。在前一章介绍其重要性的基础上，我们将从宏观[电动力学](@entry_id:158759)的定义出发，逐步建立起连接[介电函数](@entry_id:136859)与材料内部[电荷](@entry_id:275494)动态响应的物理图像。我们将阐述描述[介电函数](@entry_id:136859)行为的基本约束，介绍核心的微观模型，并进一步探索在真实晶体中由[空间色散](@entry_id:141344)、局域场以及[多体相互作用](@entry_id:751663)等效应引入的复杂性。

### [介电响应](@entry_id:140146)的宏观描述

#### [复介电函数](@entry_id:143480)的定义 $\epsilon(\omega)$

在宏观电磁学中，材料对[电场](@entry_id:194326)的响应是通过引入[电位移矢量](@entry_id:197092) $\mathbf{D}$ 和[电极化强度](@entry_id:141475) $\mathbf{P}$ 来描述的。它们与[宏观电场](@entry_id:196409) $\mathbf{E}$ 的关系由以下两个基本方程给出：

$$
\mathbf{D}(t) = \epsilon_0 \mathbf{E}(t) + \mathbf{P}(t)
$$

$$
\mathbf{D}(t) = \epsilon_0 \epsilon \mathbf{E}(t)
$$

其中，$\epsilon_0$ 是[真空介电常数](@entry_id:204253)，而 $\epsilon$ 是材料的[相对介电常数](@entry_id:267815)（或介电函数）。对于[时变电场](@entry_id:197741)，材料的响应通常会有一个延迟，这导致 $\mathbf{P}(t)$ 与 $\mathbf{E}(t)$ 之间不再是简单的瞬时比例关系。这种延迟在[频域](@entry_id:160070)中表现为介电函数的频率依赖性。

对于一个线性、时不变、均匀且各向同性的介质，其响应可以方便地在[频域](@entry_id:160070)中描述。通过对时间变量进行[傅里叶变换](@entry_id:142120)（约定时间因子为 $e^{-i\omega t}$），上述关系式变为[代数方程](@entry_id:272665)。我们将频率相关的量表示为 $\mathbf{E}(\omega)$, $\mathbf{P}(\omega)$ 和 $\mathbf{D}(\omega)$。此时，**[复介电函数](@entry_id:143480)** $\epsilon(\omega)$ 被精确地定义为联系[电位移场](@entry_id:273493)和[电场](@entry_id:194326)的[比例因子](@entry_id:266678) [@problem_id:2825390]：

$$
\mathbf{D}(\omega) = \epsilon_0 \epsilon(\omega) \mathbf{E}(\omega)
$$

结合两个定义式，我们可以得到[电极化强度](@entry_id:141475)与[电场](@entry_id:194326)之间的关系：

$$
\mathbf{P}(\omega) = \epsilon_0 (\epsilon(\omega) - 1) \mathbf{E}(\omega)
$$

这个关系式引入了另一个重要的[响应函数](@entry_id:142629)——**[电极化率](@entry_id:144209)** $\chi(\omega)$，其定义为 $\mathbf{P}(\omega) = \epsilon_0 \chi(\omega) \mathbf{E}(\omega)$。因此，[介电函数](@entry_id:136859)和[电极化率](@entry_id:144209)之间存在一个简单的关系 [@problem_id:2825390]：

$$
\epsilon(\omega) = 1 + \chi(\omega)
$$

值得注意的是，这个关系式是在[国际单位制](@entry_id:172547)（SI）下成立的。在某些旧文献中可能采用[高斯单位制](@entry_id:183405)（cgs），其关系式为 $\epsilon(\omega) = 1 + 4\pi \chi(\omega)$。在本书中，我们将统一使用[国际单位制](@entry_id:172547)。

由于响应的延迟，$\epsilon(\omega)$ 和 $\chi(\omega)$ 通常是复数，我们可以将其写为：

$$
\epsilon(\omega) = \epsilon_1(\omega) + i\epsilon_2(\omega)
$$

其中，$\epsilon_1(\omega)$ 和 $\epsilon_2(\omega)$ 分别是介电函数的实部和虚部。这两个部分各自具有明确的物理意义，分别对应材料对[电场](@entry_id:194326)的储能（电抗）和耗能（吸收）响应。

#### 物理诠释：能量储存与耗散

[复介电函数](@entry_id:143480)的实部和虚部直接关联到[电磁场](@entry_id:265881)与物质相互作用时的能量交换过程。

[电场](@entry_id:194326)对单位体积介质做功的[瞬时功率](@entry_id:174754)为 $\mathbf{E}(t) \cdot \frac{\partial \mathbf{D}(t)}{\partial t}$。对于一个单色[电场](@entry_id:194326) $\mathbf{E}(t) = \Re\{\mathbf{E}_0 e^{-i\omega t}\}$，在一个周期内对该功率进行时间平均，可以得到单位体积的平均[耗散功率](@entry_id:177328) $\langle p_{\text{loss}} \rangle$。通过严格的推导可以证明，这个[耗散功率](@entry_id:177328)完全由介电函数的虚部 $\epsilon_2(\omega)$ 决定 [@problem_id:2825386] [@problem_id:2825388]：

$$
\langle p_{\text{loss}} \rangle = \frac{1}{2} \omega \epsilon_0 \epsilon_2(\omega) |\mathbf{E}_0|^2
$$

对于**被动介质**（即不能自发产生能量的介质），能量只能被吸收而不能被创生，因此[耗散功率](@entry_id:177328)必须非负，即 $\langle p_{\text{loss}} \rangle \ge 0$。由于 $\omega > 0$ 且 $\epsilon_0 > 0$，这直接导出一个重要的物理约束：

$$
\epsilon_2(\omega) \ge 0 \quad (\text{for } \omega > 0)
$$

这意味着[介电函数](@entry_id:136859)的虚部表征了材料在频率 $\omega$ 处的吸收强度。$\epsilon_2(\omega) > 0$ 的区域对应材料的吸收谱，而 $\epsilon_2(\omega) = 0$ 的区域则表示材料在该频率下是透明的。

另一方面，[介电函数](@entry_id:136859)的实部 $\epsilon_1(\omega)$ 与储存在介质中的[电场能量](@entry_id:193072)有关。对于一个没有[色散](@entry_id:263750)（即 $\epsilon_1$ 不随频率变化）的理想介质，时间平均的[电场能量密度](@entry_id:261497)为 $u_e = \frac{1}{4}\epsilon_0 \epsilon_1 |\mathbf{E}_0|^2$。然而，在存在**[色散](@entry_id:263750)**（即 $\epsilon(\omega)$ 依赖于频率）的真实材料中，能量的定义变得更为复杂。严格的推导表明，[时间平均](@entry_id:267915)的[电场能量密度](@entry_id:261497)应为 [@problem_id:2825386]：

$$
u_e(\omega) = \frac{1}{4} \epsilon_0 \frac{\partial}{\partial \omega}[\omega \epsilon_1(\omega)] |\mathbf{E}_0|^2
$$

这个表达式揭示了储能过程不仅与 $\epsilon_1(\omega)$ 本身有关，还与其随频率的变化率有关。一个常见的误解是，当 $\epsilon_1(\omega) < 0$ 时（例如在金属的[等离子体频率](@entry_id:137429)以下），储存的能量会是负值。然而，根据上述正确的公式，能量密度由 $\frac{\partial}{\partial \omega}[\omega \epsilon_1(\omega)]$ 的符号决定。例如，对于一个简单的无碰撞金属模型（Drude模型），$\epsilon_1(\omega) = 1 - \omega_p^2/\omega^2$，虽然在 $\omega < \omega_p$ 时 $\epsilon_1(\omega)$ 为负，但 $\frac{\partial}{\partial \omega}[\omega \epsilon_1(\omega)] = 1 + \omega_p^2/\omega^2$ 始终为正。因此，即使在 $\epsilon_1(\omega)$ 为负的频率区域，[储存在电场中的能量](@entry_id:193072)密度依然是正的 [@problem_id:2825386]。

总而言之，介电函数的虚部 $\epsilon_2(\omega)$ 决定了能量的耗散，而实部 $\epsilon_1(\omega)$ 及其频率导数共同决定了能量的储存。储能和耗散是相互关联的，它们作为[复介电函数](@entry_id:143480)的两个部分，受到因果性的严格约束。

#### 基本约束：[因果性与解析性](@entry_id:196090)

物理世界的一个基本法则是**因果性**：响应不能先于激励。在[介电响应](@entry_id:140146)的语境下，这意味着[电极化强度](@entry_id:141475) $\mathbf{P}(t)$ 只能由过去时刻的[电场](@entry_id:194326) $\mathbf{E}(t' \le t)$ 决定。这一物理原理对[介电函数](@entry_id:136859) $\epsilon(\omega)$ 的数学性质施加了深刻的约束。

根据数学中的 Titchmarsh 定理，时间域中的因果性等价于其[傅里叶变换](@entry_id:142120)（即响应函数 $\chi(\omega)$ 或 $\epsilon(\omega)$）在复频率平面的上半平面（$\text{Im}\,\omega > 0$）是解析的 [@problem_id:2825390]。函数的解析性意味着它的实部和虚部不是独立的，而是通过一组[积分变换](@entry_id:186209)相互关联。这组关系被称为 **Kramers-Kronig (KK) 关系**。对于介电函数，它的一般形式为：

$$
\epsilon_1(\omega) - 1 = \frac{2}{\pi} \mathcal{P} \int_0^\infty \frac{\omega' \epsilon_2(\omega')}{(\omega')^2 - \omega^2} d\omega'
$$

$$
\epsilon_2(\omega) = -\frac{2\omega}{\pi} \mathcal{P} \int_0^\infty \frac{\epsilon_1(\omega') - 1}{(\omega')^2 - \omega^2} d\omega'
$$

其中 $\mathcal{P}$ 表示[柯西主值](@entry_id:192761)积分。

KK 关系具有极其重要的意义：它表明，如果我们知道了材料在所有频率下的吸收谱（即 $\epsilon_2(\omega)$），我们原则上就可以计算出它在任意频率下的[色散](@entry_id:263750)（即 $\epsilon_1(\omega)$），反之亦然。这为实验数据的分析和理论模型的检验提供了强大的工具。

KK 关系的一个重要推论是**求和规则** (sum rule)。例如，我们可以通过分析 KK 关系在高频极限 ($\omega \to \infty$)下的行为，来约束 $\epsilon_1(\omega)$。假设在非常高的频率下，所有[电荷](@entry_id:275494)都无法跟上[电场](@entry_id:194326)的变化，表现得像[自由粒子](@entry_id:148748)，此时材料的响应应趋近于真空，即 $\epsilon(\omega) \to 1$。通过对 KK 关系式中的积分核进行泰勒展开，可以推导出 $\epsilon_1(\omega)$ 在高频下的渐近行为 [@problem_id:2825417]：

$$
\epsilon_1(\omega) - 1 \simeq -\frac{1}{\omega^2} \left( \frac{2}{\pi} \int_0^\infty \omega' \epsilon_2(\omega') d\omega' \right) + \mathcal{O}\left(\frac{1}{\omega^4}\right)
$$

这个结果表明，$\epsilon_1(\omega)$ 趋近于 1 的方式是由 $\epsilon_2(\omega')$ 的一阶矩（即吸收谱的加权积分）决定的。这个积分通常与材料的总载流子密度有关，被称为 $f$-求和规则。它深刻地揭示了材料在不同能区的光学响应是如何通过因果性联系在一起的。

### [介电响应](@entry_id:140146)的微观模型

为了理解介电函数的具体频率依赖形式，我们需要建立材料内部[电荷](@entry_id:275494)响应的微观模型。最经典的模型将材料中的[电荷](@entry_id:275494)分为两类：金属中的自由载流子和绝缘体中的束缚[电荷](@entry_id:275494)。

#### 自由载流子的响应：Drude 模型

在金属或[半导体](@entry_id:141536)中，存在可以自由运动的导电电子（或空穴）。**Drude 模型**是描述这些自由载流子响应的最简单而有效的模型。它将载流子视为在[晶格](@entry_id:196752)背景中自由运动、受外[电场](@entry_id:194326)驱动并与[晶格缺陷](@entry_id:270099)或[声子](@entry_id:140728)发生碰撞而产生阻尼的经典粒子。

在一个简化的无碰撞图像中，一个[电荷](@entry_id:275494)为 $-e$、有效质量为 $m^*$ 的载流子在[电场](@entry_id:194326) $\mathbf{E}(t) = \mathbf{E}_0 e^{-i\omega t}$ 的驱动下的运动方程为牛顿第二定律：$m^* \ddot{\mathbf{x}}(t) = -e \mathbf{E}(t)$。求解这个方程可以得到载流子的位移 $\mathbf{x}(\omega)$，进而得到由 $n$ 个载流子单位体积贡献的[宏观极化](@entry_id:141855)强度 $\mathbf{P}(\omega) = -ne\mathbf{x}(\omega)$。最终，我们可以推导出[介电函数](@entry_id:136859)的形式 [@problem_id:2825391]：

$$
\epsilon(\omega) = 1 - \frac{\omega_p^2}{\omega^2}
$$

其中，$\omega_p$ 是一个特征频率，被称为**等离子体频率**（plasma frequency），其平方定义为：

$$
\omega_p^2 = \frac{ne^2}{\epsilon_0 m^*}
$$

这个频率正比于载流子浓度的平方根，是表征[金属光学](@entry_id:268790)性质最重要的参数。在 $\omega > \omega_p$ 时, $\epsilon(\omega) > 0$，金属对[电磁波](@entry_id:269629)是透明的；在 $\omega < \omega_p$ 时, $\epsilon(\omega) < 0$，[电磁波](@entry_id:269629)被完全反射，这解释了金属为什么具有光泽。

更实际的 Drude 模型需要考虑载流子在运动过程中受到的阻尼，这可以通过在运动方程中引入一个与速度成正比的摩擦项 $-m^* \gamma \dot{\mathbf{x}}(t)$ 来实现，其中 $\gamma$ 是碰撞频率或阻尼率。加入该项后，[介电函数](@entry_id:136859)变为 [@problem_id:2825388]：

$$
\epsilon(\omega) = 1 - \frac{\omega_p^2}{\omega(\omega + i\gamma)} = \left(1 - \frac{\omega_p^2}{\omega^2 + \gamma^2}\right) + i \left(\frac{\omega_p^2 \gamma}{\omega(\omega^2 + \gamma^2)}\right)
$$

此时，介电函数的虚部 $\epsilon_2(\omega)$ 不再为零，这代表了由于碰撞引起的能量吸收。在直流极限下（$\omega \to 0$），这种吸收对应于欧姆定律描述的焦耳热。

#### 束缚[电荷](@entry_id:275494)的响应：Lorentz [振子](@entry_id:271549)模型

在绝缘体或[半导体](@entry_id:141536)中，电子被束缚在[原子核](@entry_id:167902)周围，不能自由移动。**Lorentz [振子](@entry_id:271549)模型**将这种束缚[电荷](@entry_id:275494)的响应类比为一个受外[电场](@entry_id:194326)驱动的[阻尼谐振子](@entry_id:276848)。除了驱动力和阻尼力外，电子还受到一个指向其平衡位置的恢复力，其形式为 $-m^* \omega_0^2 \mathbf{x}(t)$，其中 $\omega_0$ 是[振子](@entry_id:271549)的固有谐振频率。

包含这三项力的[运动方程](@entry_id:170720)的解，可以导出 Lorentz 模型的[电极化率](@entry_id:144209)，并最终得到[介电函数](@entry_id:136859) [@problem_id:2825388]：

$$
\epsilon(\omega) = \epsilon_{\infty} + \frac{\omega_{p,L}^2}{\omega_0^2 - \omega^2 - i\gamma_L \omega}
$$

这里的 $\epsilon_{\infty}$ 代表了在远高于[谐振频率](@entry_id:265742) $\omega_0$ 时，由更高能量的电子跃迁贡献的一个背景[介电常数](@entry_id:146714)。$\omega_{p,L}^2$ 是一个与[振子强度](@entry_id:147221)（oscillator strength）和密度相关的量，$\gamma_L$ 是[振子](@entry_id:271549)的阻尼率。

该模型的 $\epsilon_2(\omega)$ 在谐振频率 $\omega_0$ 附近呈现一个吸收峰，峰的宽度由阻尼率 $\gamma_L$ 决定。这种形式很好地描述了绝缘体中由于[声子](@entry_id:140728)吸收（在红外波段）或电子的[带间跃迁](@entry_id:138793)（在可见光或紫外波段）引起的光学吸收。

一个真实材料的[介电函数](@entry_id:136859)通常可以看作是 Drude 模型（对于自由载流子）和多个 Lorentz 模型（对于不同能量的束缚跃迁）的叠加。

#### [静态极限](@entry_id:262480) ($\omega \to 0$)：[金属与绝缘体](@entry_id:148635)

Drude 和 Lorentz 模型在低频极限下的不同行为，深刻地揭示了[金属与绝缘体](@entry_id:148635)在静电响应上的本质区别 [@problem_id:2825414]。

对于绝缘体（Lorentz 模型），当频率趋于零时，介电函数趋于一个有限的正值：

$$
\epsilon_{\text{insulator}}(0) = \epsilon_{\infty} + \frac{\omega_{p,L}^2}{\omega_0^2} > 1
$$

这个有限的**静态[介电常数](@entry_id:146714)** $\epsilon(0)$ 意味着绝缘体只能部分地屏蔽外[电场](@entry_id:194326)。外加[电场](@entry_id:194326)会在材料内部感生一个有限的极化，从而使内部总场减弱为外部场强的 $1/\epsilon(0)$ 倍。

而对于金属（Drude 模型），当 $\omega \to 0$ 时，[介电函数](@entry_id:136859)的实部会发散到负无穷：

$$
\text{Re}\,\epsilon_{\text{metal}}(\omega) \approx -\frac{\omega_p^2}{\omega^2} \to -\infty
$$

这意味着理想金属的静态[介电常数](@entry_id:146714)是无穷大的。这一发散行为是**[完美屏蔽](@entry_id:146940)** (perfect screening) 的体现：金属中的自由载流子会重新排布，以完全抵消掉进入其内部的宏观静电场。在更精确的包含波矢 $q$ 的理论中，金属的静态纵向[介电函数](@entry_id:136859) $\epsilon_L(q, 0)$ 在长波极限下 ($q \to 0$) 表现为 $1/q^2$ 的发散，例如在 [Thomas-Fermi 近似](@entry_id:143139)中，$\epsilon_L(q, 0) \approx 1 + \kappa_{\text{TF}}^2/q^2$，其中 $\kappa_{\text{TF}}$ 是 [Thomas-Fermi 屏蔽](@entry_id:145372)波矢。这种发散正是[完美屏蔽](@entry_id:146940)的数学表达，它导致置于金属中的[电荷](@entry_id:275494)所产生的[库仑势](@entry_id:154276)被屏蔽成短程的汤川势 $e^{-\kappa_{\text{TF}} r}/r$ [@problem_id:2825414]。

### 晶体固体中的[空间色散](@entry_id:141344)与各向异性

前面的模型假设介质是均匀的。然而，晶体具有周期性的原子结构，这给[介电响应](@entry_id:140146)带来了新的复杂性，即[空间色散](@entry_id:141344)和[局域场效应](@entry_id:141628)。

#### 非局域响应：依赖于[波矢](@entry_id:178620)的介电函数

在原子尺度上，晶体是不均匀的。因此，在某一点 $\mathbf{r}$ 的[电极化强度](@entry_id:141475)不仅取决于该点的[电场](@entry_id:194326) $\mathbf{E}(\mathbf{r})$，还可能受到其邻近点[电场](@entry_id:194326)的影响。这种响应的**非局域性** (nonlocality) 在傅里叶空间中表现为[介电函数](@entry_id:136859)不仅依赖于频率 $\omega$，还依赖于[波矢](@entry_id:178620) $\mathbf{q}$，即 $\epsilon(\mathbf{q}, \omega)$。这种对 $\mathbf{q}$ 的依赖性被称为**[空间色散](@entry_id:141344)**。

#### 纵向与横向响应

当[介电函数](@entry_id:136859)依赖于[波矢](@entry_id:178620) $\mathbf{q}$ 时，即使宏观上材料是各向同性的，$\mathbf{q}$ 的存在也引入了一个优选方向。因此，[介电响应](@entry_id:140146)必须被描述为一个张量 $\epsilon_{ij}(\mathbf{q}, \omega)$。对于各向同性介质，这个张量可以基于与 $\mathbf{q}$ 平行（纵向）和垂直（横向）的方向进行分解 [@problem_id:2825378]：

$$
\epsilon_{ij}(\mathbf{q}, \omega) = \epsilon_T(q, \omega) \left(\delta_{ij} - \frac{q_i q_j}{q^2}\right) + \epsilon_L(q, \omega) \frac{q_i q_j}{q^2}
$$

这里，$\epsilon_L(q, \omega)$ 和 $\epsilon_T(q, \omega)$ 分别是**纵向介电函数**和**横向[介电函数](@entry_id:136859)**，它们是两个独立的标量函数。

这种分解有深刻的物理后果，因为纵向和横向[电场](@entry_id:194326)分量在电磁学中扮演着不同的角色：

- **纵向[介电函数](@entry_id:136859) $\epsilon_L(q, \omega)$** 描述了材料对纵向[电场](@entry_id:194326)（即 $\mathbf{E} \parallel \mathbf{q}$）的响应。根据麦克斯韦方程中的高斯定律 $i\mathbf{q} \cdot \mathbf{D} = \rho_{\text{ext}}$，$\epsilon_L$ 直接决定了材料如何屏蔽外部[电荷](@entry_id:275494) $\rho_{\text{ext}}$。此外，材料中可能存在的本征纵向[集体激发](@entry_id:145026)模式（如等离子体激元，即 plasmon）的色散关系由条件 $\epsilon_L(q, \omega) = 0$ 决定 [@problem_id:2825378]。

- **横向介电函数 $\epsilon_T(q, \omega)$** 描述了材料对横向[电场](@entry_id:194326)（即 $\mathbf{E} \perp \mathbf{q}$）的响应。横向[电磁波](@entry_id:269629)（即光）在介质中的传播由 $\epsilon_T$ 控制。其[色散关系](@entry_id:140395)由[波动方程](@entry_id:139839) $q^2 c^2 = \omega^2 \epsilon_T(q, \omega)$ 给出 [@problem_id:2825378]。

在大多数情况下（特别是长波极限 $q \to 0$），$\epsilon_L(q, \omega)$ 和 $\epsilon_T(q, \omega)$ 的值会趋于一致，但在需要考虑[空间色散](@entry_id:141344)的场合（例如研究[激子极化激元](@entry_id:192304)或非局域效应时），区分两者至关重要。

#### 微观与宏观响应：[局域场效应](@entry_id:141628)

在[晶格](@entry_id:196752)的周期性势场中，即使外加一个宏观均匀的[电场](@entry_id:194326)（对应[波矢](@entry_id:178620) $\mathbf{q} \to \mathbf{0}$），在原子尺度上感生出的总[电场](@entry_id:194326)也是不均匀的。作用在某个特定原子上的[电场](@entry_id:194326)（**局域场**）会不同于整个样品的宏观平均场。这种差异来源于其他所有原子被极化后产生的附加[电场](@entry_id:194326)。

为了精确描述这种效应，理论上引入了**微观[介电矩阵](@entry_id:144203)** $\epsilon_{\mathbf{G}\mathbf{G}'}(\mathbf{q}, \omega)$，其中 $\mathbf{G}$ 和 $\mathbf{G}'$ 是[倒易晶格矢量](@entry_id:263351)。该矩阵的对角元 $\epsilon_{\mathbf{GG}}$ 描述了具有[波矢](@entry_id:178620) $\mathbf{q}+\mathbf{G}$ 的[电势](@entry_id:267554)分量如何响应自身，而非对角元 $\epsilon_{\mathbf{G}\mathbf{G}'}$ ($\mathbf{G} \neq \mathbf{G}'$) 则描述了不同[波矢](@entry_id:178620)分量之间的耦合，这正是**[局域场效应](@entry_id:141628)** (local-field effects) 的数学体现 [@problem_id:2825407]。

实验上测量的宏观介电函数 $\epsilon_M(\omega)$ 对应于对宏观场的响应。它与微观[介电矩阵](@entry_id:144203)的关系并非简单地取其 $(\mathbf{G}=\mathbf{0}, \mathbf{G}'=\mathbf{0})$ 分量，而是需要通过对整个[矩阵求逆](@entry_id:636005)来获得。这个关系被称为 **Adler-Wiser 公式** [@problem_id:2825407]：

$$
\epsilon_M(\omega) = \lim_{\mathbf{q} \to \mathbf{0}} \frac{1}{[\epsilon^{-1}]_{\mathbf{G}=\mathbf{0}, \mathbf{G}'=\mathbf{0}}(\mathbf{q}, \omega)}
$$

这个公式表明，宏观[介电函数](@entry_id:136859)是通过矩阵求逆过程，将所有微观尺度的耦合（[局域场效应](@entry_id:141628)）“[重整化](@entry_id:143501)”到宏观响应中的结果。只有在理想的均匀介质中（即所有非对角元为零），宏观[介电函数](@entry_id:136859)才等于微观矩阵的 $(0,0)$ 元。因此，理解[局域场效应](@entry_id:141628)是连接[第一性原理计算](@entry_id:198754)与宏观实验测量值的关键。

### 前沿课题：介电函数中的[多体效应](@entry_id:173569)

最后，我们讨论电子之间的相互作用如何进一步修正[介电函数](@entry_id:136859)的图像，这些是理解现代凝聚态材料（如[强关联电子体系](@entry_id:183796)）光学性质的核心。

#### 阻尼的微观起源：[朗道阻尼](@entry_id:137619)

在 Drude 和 Lorentz 模型中，阻尼 $\gamma$ 是一个唯象参数。然而，即使在一个没有杂质和[声子](@entry_id:140728)的完美电子气中，也存在一种内在的、无碰撞的阻尼机制，称为**[朗道阻尼](@entry_id:137619)** (Landau damping)。

这种阻尼的根源在于，一个[集体激发](@entry_id:145026)模式（如等离子体激元）可以将其能量和动量转移给单个电子，从而激发一个**电子-空穴对**。在零温下，这种过程只有在能量和动量都守恒，并且满足[泡利不相容原理](@entry_id:141850)（即电子从费米海内部的一个占据态跃迁到[费米海](@entry_id:136725)外部的一个未占据态）时才能发生。

所有可能满足这些条件的 $(\mathbf{q}, \omega)$ 组合构成了所谓的**电子-空穴对连续谱** (particle-hole continuum)。对于三维抛物线性能带的[电子气](@entry_id:140692)，这个区域的边界可以被精确计算出来 [@problem_id:2825428]。在长波极限下 ($q \to 0$)，等离子体激元的能量远高于[电子-空穴对](@entry_id:142506)[连续谱](@entry_id:155477)的上限，因此它是一个稳定的、无阻尼的模式。然而，随着波矢 $q$ 的增加，等离子体激元的[色散曲线](@entry_id:197598)会下降，最终在某个临界波矢 $q_c$ 处进入电子-空穴对连续谱。

一旦进入[连续谱](@entry_id:155477)，等离子体激元就可以通过激发电子-空穴对而衰变，从而获得一个有限的寿命。这种衰变机制就是[朗道阻尼](@entry_id:137619)。在[光谱](@entry_id:185632)上，它表现为能量损失函数 $\text{Im}\{-1/\epsilon(q, \omega)\}$ 中的等离子体峰从一个尖锐的 $\delta$-函数[峰展宽](@entry_id:183067)为一个具有有限宽度的洛伦兹峰 [@problem_id:2825428]。

#### [电子-电子相互作用](@entry_id:139900)与[谱权重转移](@entry_id:146476)

在真实材料中，电子之间的[库仑相互作用](@entry_id:747947)会显著地影响其动力学行为。在 **[朗道费米液体理论](@entry_id:151062)** 的框架下，相互作用将裸电子“缀饰”成了行为类似但性质被重整化的**[准粒子](@entry_id:136584)**。这些[准粒子](@entry_id:136584)的主要特征包括[有效质量](@entry_id:142879) $m^*$（通常不同于能带质量 $m_b$）和[准粒子权重](@entry_id:140100) $Z$（$0  Z \le 1$），其中 $Z$ 衡量了裸电子成分在[准粒子](@entry_id:136584)[波函数](@entry_id:147440)中的占比，$Z1$ 意味着[强相互作用](@entry_id:159198)。

电子相互作用对[介电函数](@entry_id:136859)的影响，取决于系统是否具有伽利略不变性 [@problem_id:2825402]。
- 在一个理想的[均匀电子气](@entry_id:163911)（具有伽利略[不变性](@entry_id:140168)）中，由于沃德等式的保护，等离子体频率严格由总载流子密度 $n$ 和裸电子质量 $m_e$ 决定，不受相互作用细节的影响。
- 然而，在[晶格](@entry_id:196752)中，伽利略[不变性](@entry_id:140168)被破坏。此时，相互作用会引起所谓的**[谱权重转移](@entry_id:146476)**。

描述光学吸收的 $f$-求和规则指出，$\text{Re}\{\sigma(\omega)\}$ 在全频率范围内的积分（即总[谱权重](@entry_id:144751)）是一个[守恒量](@entry_id:150267)，由总电子数决定。但在[晶格](@entry_id:196752)上的相互作用电子体系中，这个总权重会被重新分配。具体来说，对应于[准粒子](@entry_id:136584)相干运动的 Drude 峰（在 $\omega=0$ 处的 $\delta$-函数峰）的[谱权重](@entry_id:144751) $D_{\text{coh}}$ 会被相互作用所压制，其大小近似正比于[准粒子权重](@entry_id:140100) $Z$。而“失去”的[谱权重](@entry_id:144751) $(1-D_{\text{coh}})$ 并不会消失，而是被转移到有限频率处，形成一个宽阔的**非相干背景**，对应于无法用单[准粒子](@entry_id:136584)图像描述的复杂多体激发。

因此，在[强关联材料](@entry_id:198946)中（$Z \ll 1$），即使载流子浓度不变，我们也会观察到低频[电导](@entry_id:177131)（和相应的 Drude 响应）被急剧压制，而高频（例如中红外）区域则出现宽泛的吸收。这一效应深刻地影响了介电函数 $\epsilon(\omega)$ 的低频行为，因为 $\text{Re}\{\epsilon(\omega)\} \approx \epsilon_{\text{bkgd}} - 2D_{\text{coh}}/(\pi\epsilon_0\omega^2)$。随着相互作用增强（$Z$ 减小），Drude 权重 $D_{\text{coh}}$ 减小，导致 $\text{Re}\{\epsilon(\omega)\}$ 在低频区的负发散行为减弱 [@problem_id:2825402]。这是从光学响应中探测[量子材料](@entry_id:136741)中电子关联强度的重要途径。