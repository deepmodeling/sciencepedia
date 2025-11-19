## 引言
热辐射是自然界最基本的[能量传递](@entry_id:174809)方式之一，但长久以来，其效率被认为受到普朗克黑体辐射定律的根本限制。然而，当物体间距缩减至纳米尺度时，一种突破性的物理现象——[近场](@entry_id:269780)热辐射——便显现出来，它不仅能够超越普朗克极限，更能实现对热能流前所未有的精确调控。这一现象为解决微纳系统中的[能量转换](@entry_id:165656)效率和[热管理](@entry_id:146042)等关键挑战开辟了全新的道路。本文旨在系统性地剖析[近场](@entry_id:269780)[热辐射](@entry_id:145102)的物理世界，填补经典[热力学](@entry_id:141121)与[纳米光子学](@entry_id:137892)之间的知识鸿沟。

本文将分为三个核心部分，带领读者层层深入。在“原理与机制”一章中，我们将从第一性原理出发，建立基于涨落电动力学的理论基础，揭示倏逝波如何主导[近场](@entry_id:269780)能量交换，并阐明[表面等离激元共振](@entry_id:137332)等关键增强机制。接着，在“应用与跨学科[交叉](@entry_id:147634)”一章中，我们将探讨这些理论如何在近场[热光](@entry_id:165211)伏、纳米热开关、高分辨率成像等前沿技术中转化为现实，并展示其与[材料科学](@entry_id:152226)、凝聚态物理等领域的深刻联系。最后，“动手实践”部分将提供具体的计算练习，帮助读者将理论知识应用于解决实际的分析与设计问题。通过本章的学习，您将全面掌握近场热辐射的核心概念、理论工具及其在未来科技中的巨大潜力。

## 原理与机制

本章旨在深入探讨[近场](@entry_id:269780)热辐射的核心物理原理与机制。我们将从[近场](@entry_id:269780)效应的基本概念出发，建立起基于涨落[电动力学](@entry_id:158759)的理论框架，推导计算热流的关键公式，并阐述该领域内重要的基本定律和对称性。最后，我们将讨论标准理论的局限性及其在前沿研究中的拓展。

### [近场辐射](@entry_id:153085)的基本概念：超越普朗克极限

经典[热辐射](@entry_id:145102)理论，以普朗克黑体辐射定律为基石，描述的是物体间距远大于[热辐射](@entry_id:145102)特征波长时的能量交换。在这种**远场（far-field）**情形下，能量由在真空中自由传播的[电磁波](@entry_id:269629)（即**行进波**）携带。对于两个相距遥远、温度分别为 $T_1$ 和 $T_2$ 的理想黑体，单位面积的净辐射热流谱密度由[普朗克定律](@entry_id:145765)给出，通常被称为**普朗克极限**。这是远场条件下，仅考虑行进波作为能量载体时，[辐射传热](@entry_id:149271)的理论最大值。其表达式为 [@problem_id:2511593]：

$$
q_{\omega}^{\mathrm{FF}} = \frac{\hbar \omega^3}{4\pi^2 c^2} \left[ \frac{1}{\exp\left(\frac{\hbar\omega}{k_{\mathrm{B}}T_1}\right) - 1} - \frac{1}{\exp\left(\frac{\hbar\omega}{k_{\mathrm{B}}T_2}\right) - 1} \right]
$$

其中，$\hbar$ 是约化普朗克常数，$c$ 是[真空中的光速](@entry_id:272753)，$k_{\mathrm{B}}$ 是[玻尔兹曼常数](@entry_id:142384)，$\omega$ 是[角频率](@entry_id:261565)。

然而，当两个物体的间距 $d$ 缩减至亚波长尺度时，即小于[热辐射](@entry_id:145102)的特征波长 $\lambda_T = \hbar c / (k_B T)$ 时，一种新的[传热机制](@entry_id:142474)变得至关重要，这便是**近场（near-field）**热辐射。在[近场](@entry_id:269780)区域，除了行进波，[电磁场](@entry_id:265881)的另一种解——**[倏逝波](@entry_id:156713)（evanescent waves）**——开始主导能量交换过程。

为了理解这两种波的区别，我们可以将[电磁场](@entry_id:265881)在平行于表面的平面内进行[傅里叶分解](@entry_id:160101)，用平[行波](@entry_id:185008)矢 $\mathbf{k}_\parallel$ 来标记不同的平面波分量。在真空中，[波矢](@entry_id:178620)的法向分量 $k_z$ 与平行分量 $k_\parallel$ 满足[色散关系](@entry_id:140395) $k_\parallel^2 + k_z^2 = k_0^2 = (\omega/c)^2$。根据 $k_\parallel$ 的大小，我们可以区分两种模式 [@problem_id:2511591]：

1.  **行进波（Propagating Waves）**: 当 $k_\parallel  k_0$ 时，$k_z = \sqrt{k_0^2 - k_\parallel^2}$ 是实数。这些模式对应于在真空中可以自由传播的[平面波](@entry_id:189798)，它们构成了[远场辐射](@entry_id:265518)的全部内容。

2.  **倏逝波（Evanescent Waves）**：当 $k_\parallel > k_0$ 时，$k_z = i\sqrt{k_\parallel^2 - k_0^2} \equiv i\kappa_z$ 是纯虚数。这些模式的[电磁场](@entry_id:265881)在垂直于表面的方向上呈指数衰减，其形式为 $\exp(-\kappa_z z)$。单个物体表面的[倏逝波](@entry_id:156713)并不会将能量辐射到远方，其能量被束缚在表面附近。

当另一个物体进入到这个[倏逝场](@entry_id:165393)的衰减长度（约 $1/\kappa_z$）之内时，两个物体的[倏逝场](@entry_id:165393)可以发生耦合。这种耦合过程，常被形象地称为**[光子](@entry_id:145192)隧穿（photon tunneling）**，为能量从高温物体传递到低温物体开辟了新的通道。由于倏逝波的平[行波](@entry_id:185008)矢 $k_\parallel$ 可以取大于 $k_0$ 的任意值，这极大地增加了可用于热传递的[电磁模式](@entry_id:260856)数量。这种模式数量的增加，在更专业的术语中，被称为**局域电磁[态密度](@entry_id:147894)（Local Density of States, [LDOS](@entry_id:136852)）**的增强。

因此，近场热辐射之所以能够**超越普朗克极限**，并非因为它违反了任何热力学定律，而是因为它利用了远场理论所忽略的额外传热通道（倏逝波通道）。每个单一模式的能量传输仍然遵循[热力学第二定律](@entry_id:142732)，即能量从高温物体的模式流向低温物体的相应模式，且在 $T_1 = T_2$ 时净热流为零。总热流的巨大增强来源于对数量庞大的倏逝波模式的贡献求和的结果 [@problem_id:2511593]。

### 涨落[电动力学](@entry_id:158759)：热辐射的微观起源

为了从第一性原理精确描述近场[热辐射](@entry_id:145102)，我们需要一个能够涵盖所有[电磁模式](@entry_id:260856)（包括行进波和[倏逝波](@entry_id:156713)）的统一理论。这个理论就是由 Rytov 等人发展的**涨落[电动力学](@entry_id:158759)（Fluctuational Electrodynamics）**。其核心思想是：任何有温度、有耗散的介质内部，由于热搅动，微观的[电荷](@entry_id:275494)和电流时刻在做无规运动，形成**涨落电流源（fluctuating current sources）** $\mathbf{J}(\mathbf{r}, t)$。这些涨落电流源正是[热辐射](@entry_id:145102)的微观起源。

**涨落-耗散定理（Fluctuation-Dissipation Theorem, FDT）**是涨落电动力学的基石，它将宏观材料的光学响应（耗散）与微观的涨落强度联系起来。对于一个处于局域热力学平衡（温度为 $T$）、线性的、各向同性的、局域响应的介质，其涨落电流源的二阶关联函数（在频率域中表示为交叉谱密度）由 FDT 给出 [@problem_id:2511615]：

$$
\langle J_i(\mathbf{r},\omega) J_j^*(\mathbf{r}',\omega') \rangle = \frac{2\omega\epsilon_0}{\pi} \operatorname{Im}\{\epsilon(\omega)\} \Theta(\omega,T) \delta_{ij} \delta(\mathbf{r}-\mathbf{r}') \delta(\omega-\omega')
$$

这个公式的每个部分都有深刻的物理含义：

*   **耗散部分**: $\operatorname{Im}\{\epsilon(\omega)\}$ 是介电函数 $\epsilon(\omega)$ 的虚部，代表了材料吸收[电磁能](@entry_id:264720)量的能力（焦耳热）。FDT 表明，一个材料必须有耗散（$\operatorname{Im}\{\epsilon(\omega)\} > 0$），才能成为热辐射的源。没有耗散的完美透明介质既不吸收也不发射[热辐射](@entry_id:145102)。

*   **热能部分**: $\Theta(\omega,T)$ 是频率为 $\omega$、温度为 $T$ 的量子谐振子的[平均能量](@entry_id:145892)：
    $$
    \Theta(\omega, T) = \frac{\hbar\omega}{\exp(\hbar\omega/k_B T) - 1}
    $$
    在某些定义中，也会包含[零点能](@entry_id:142176)项 $\hbar\omega/2$。这个函数决定了[热涨落](@entry_id:143642)的强度。在[经典极限](@entry_id:148587)下（$\hbar\omega \ll k_B T$），$\Theta(\omega,T) \approx k_B T$；在零温极限下（$T \to 0$），$\Theta(\omega,T) \to 0$（若不计[零点能](@entry_id:142176)）。

*   **对称性与局域性**:
    *   **时间[平稳性](@entry_id:143776)** ($\delta(\omega-\omega')$): 涨落的统计特性不随时间改变，导致不同频率的涨落不相关。
    *   **空间局域性** ($\delta(\mathbf{r}-\mathbf{r}')$): 假设材料的响应是局域的，即一点的极化仅取决于同一点的[电场](@entry_id:194326)。这导致不同空间点的微观涨落源是不相关的。我们将在后续章节探讨此假设失效的情形。
    *   **各向同性** ($\delta_{ij}$): 材料在所有方向上光学性质相同，导致不同笛卡尔分量的电流涨落是不相关的，且强度相同。

一旦知道了涨落电流源的统计特性，就可以通过求解[麦克斯韦方程组](@entry_id:150940)，计算出这些源在周围空间（包括[近场](@entry_id:269780)区域）产生的[电磁场](@entry_id:265881)，并最终得到辐射热流。

### 热流计算的形式化理论

基于涨落电动力学，我们可以推导出计算[近场](@entry_id:269780)热流的普适公式。

#### Landauer-like 公式

一个极具物理洞察力的表述形式是 **Landauer-like 公式**。它将总热通量 $\Phi$ 表示为所有独立电磁通道对热流贡献的总和 [@problem_id:2511607]：

$$
\Phi = \int_0^\infty \frac{d\omega}{2\pi} \left[ \Theta(\omega,T_1) - \Theta(\omega,T_2) \right] \sum_m \mathcal{T}_m(\omega)
$$

这个公式的形式非常直观：总热流是温差[驱动项](@entry_id:165986) $[\Theta(\omega,T_1) - \Theta(\omega,T_2)]$ 与所有通道的**透射系数（transmission coefficient）** $\mathcal{T}_m(\omega)$ 之和的乘积，再对所有频率积分。这里的 $m$ 代表一个独立的电磁通道，例如在平面几何中，一个通道由频率 $\omega$、平[行波](@entry_id:185008)矢 $\mathbf{k}_\parallel$ 和偏振态（$s$ 或 $p$）共同定义。

#### Polder-van Hove 公式

对于两个平行半无限大平面这种标准模型，Landauer 公式可以具体写成 **Polder-van Hove 公式** [@problem_id:2511643] [@problem_id:2511607]。它明确地给出了每个通道的[透射系数](@entry_id:756126)，并区分为行进波和倏逝波两部分的贡献。总热流谱密度 $\Phi(\omega)$ 为：

$$
\Phi(\omega) = \frac{\Theta(\omega,T_1) - \Theta(\omega,T_2)}{4\pi^2} \sum_{p=s,p} \left[ \int_{k_\parallel  k_0} \mathcal{T}_p^{\text{prop}}(k_\parallel) d^2k_\parallel + \int_{k_\parallel > k_0} \mathcal{T}_p^{\text{evan}}(k_\parallel) d^2k_\parallel \right]
$$

其中，行进波 ($k_\parallel  k_0$) 和[倏逝波](@entry_id:156713) ($k_\parallel > k_0$) 的[透射系数](@entry_id:756126)分别为：

$$
\mathcal{T}_p^{\text{prop}}(k_\parallel) = \frac{(1-|r_{1p}|^2)(1-|r_{2p}|^2)}{|1 - r_{1p}r_{2p}e^{2ik_z d}|^2}
$$

$$
\mathcal{T}_p^{\text{evan}}(k_\parallel) = \frac{4 \operatorname{Im}\{r_{1p}\} \operatorname{Im}\{r_{2p}\} e^{-2\kappa_z d}}{|1 - r_{1p}r_{2p}e^{-2\kappa_z d}|^2}
$$

这里，$r_{jp}$ 是从真空中看向介质 $j$ 的菲涅尔[反射系数](@entry_id:194350)（$p$ 代表 $s$ 或 $p$ 偏振），$d$ 是间距，$k_z = \sqrt{k_0^2-k_\parallel^2}$，$i\kappa_z = i\sqrt{k_\parallel^2-k_0^2}$。由于各向同性，积分可以简化为对 $k_\parallel$ 的一维积分 $\int_0^\infty (\dots) \frac{k_\parallel dk_\parallel}{2\pi}$ [@problem_id:2511643]。

这些公式的结构揭示了深刻的物理：
*   分母 $|1 - r_{1p}r_{2p}e^{i\phi}|^2$ 描述了在两表面间发生多次反射形成的**法布里-珀罗（Fabry-Pérot）谐振**。当分母趋近于零时，透射被急剧增强。
*   行进波透射系数的分子 $(1-|r|^2)$ 与材料的[吸收率](@entry_id:144520)/[发射率](@entry_id:143288)直接相关。
*   倏逝波[透射系数](@entry_id:756126)的分子 $\operatorname{Im}\{r\}$ 表明，能量转移必须通过有耗散的介质才能实现。指数项 $e^{-2\kappa_z d}$ 则反映了倏逝波[耦合强度](@entry_id:275517)随距离的指数衰减。

#### [表面等离激元共振](@entry_id:137332)

近场热辐射最引人注目的现象之一，就是当材料支持**[表面等离激元](@entry_id:145851)（Surface Polaritons）**时，热流可以得到几个[数量级](@entry_id:264888)的增强。[表面等离激元](@entry_id:145851)是束缚在介质表面的、由[电磁场](@entry_id:265881)与材料中[电荷](@entry_id:275494)或[晶格振动](@entry_id:140970)集体激发耦合而成的特殊模式（例如金属中的表面等离激元 SPP，或极性[电介质](@entry_id:147163)中的表面[声子](@entry_id:140728)[等离激元](@entry_id:146184) SPhP）。

当两个支持表面等离激元的表面彼此靠近时，它们各自的表面模式会发生耦合，形成新的、能量高度集中的耦合模式。这种耦合在 Polder-van Hove 公式的分母中体现为一种强烈的谐振。具体来说，对于 p-偏振的倏逝波，当满足表面等离激元色散关系时，反射系数 $r_p$ 的分母会趋近于零，导致 $|r_p|$ 变得非常大。

考虑一个典型的共振条件，例如对于极性材料，在某个频率 $\omega_0$ 附近，[介电函数](@entry_id:136859) $\operatorname{Re}\{\epsilon(\omega_0)\} \approx -1$。在这种[准静态近似](@entry_id:264812)下 ($k_\parallel \gg k_0$)，p-偏振[反射系数](@entry_id:194350) $r_p \approx (\epsilon-1)/(\epsilon+1)$。当 $\epsilon \approx -1 + i\epsilon''$ 且损耗 $\epsilon'' \ll 1$ 时，$r_p$ 的值会变得非常大。此时，[倏逝波](@entry_id:156713)透射系数 $\mathcal{T}_p^{\text{evan}}$ 的分母 $|1-r_p^2 e^{-2k_\parallel d}|^2$ 可以在某个特定的 $k_\parallel^*$ 处达到极小值，从而使 $\mathcal{T}_p^{\text{evan}}$ 达到一个峰值。理论分析可以证明，在理想条件下，这个峰值可以达到其理论最大值 1 [@problem_id:2511598]。这意味着在该特定频率和[波矢](@entry_id:178620)的通道中，能量传输效率达到了 100%。正是这种**[共振光子隧穿](@entry_id:156806)**现象，导致了[近场](@entry_id:269780)[热辐射](@entry_id:145102)谱通常呈现出由表面等离激元主导的、非常尖锐的单色峰，其强度远超同等温度下的黑体辐射。

### 基本对称性与广义[基尔霍夫定律](@entry_id:180785)

涨落电[动力学理论](@entry_id:136901)不仅提供了计算工具，还揭示了深刻的物理对称性和定律。

#### 洛伦兹互易性

**洛伦兹互易性（Lorentz Reciprocity）**是线性电磁学中的一个基本原理。对于由满足对称性 $\boldsymbol{\varepsilon}^T = \boldsymbol{\varepsilon}$ 和 $\boldsymbol{\mu}^T = \boldsymbol{\mu}$ 的材料构成的系统（即使材料有损耗），该原理成立。它指出，交换点源和观测点的位置，电磁响应具有特定的对称性。互易性原理的一个重要推论是，[电场](@entry_id:194326)的**格林函数张量（Dyadic Green's Function, DGF）**满足转置对称性 [@problem_id:2511622]：

$$
\mathbf{G}(\mathbf{r}, \mathbf{r}'; \omega) = \mathbf{G}^T(\mathbf{r}', \mathbf{r}; \omega)
$$

这个关系式表明，从点 $\mathbf{r}'$ 的 $j$ 方向电流源到点 $\mathbf{r}$ 的 $i$ 方向[电场](@entry_id:194326)响应，等于从点 $\mathbf{r}$ 的 $i$ 方向[电流源](@entry_id:275668)到点 $\mathbf{r}'$ 的 $j$ 方向[电场](@entry_id:194326)响应。这一[基本对称性](@entry_id:161256)贯穿于整个电磁学，无论是[近场](@entry_id:269780)还是远场，行进波还是[倏逝波](@entry_id:156713)，都必须遵守。

在[近场热传递](@entry_id:149379)中，互易性直接导致了热流透射函数的对称性，即从物体1到物体2的透射函数等于从物体2到物体1的透射函数 [@problem_id:2511622]：

$$
\mathcal{T}_{1\to 2}(\omega) = \mathcal{T}_{2\to 1}(\omega)
$$

这个结论非常重要，因为它保证了无论物体的几何形状和材料如何复杂，只要满足互易性，我们计算热流时只需考虑一个方向的透射函数。

#### 广义基尔霍夫定律

经典的[基尔霍夫热辐射定律](@entry_id:144588)指出，在[热平衡](@entry_id:141693)时，一个物体在给定方向和频率上的[发射率](@entry_id:143288)等于其[吸收率](@entry_id:144520)。涨落[电动力学](@entry_id:158759)将这个定律推广到了一个更普遍、更强大的形式，即**广义[基尔霍夫定律](@entry_id:180785)**。

该定律指出，对于一个处于局域热力学平衡的互易物体，对于**任意一个**电[磁通](@entry_id:191239)道（可以是行进波通道，也可以是倏逝波通道），其**模式选择性发射率（mode-selective emissivity）** $\mathcal{E}_{\text{channel}}$ 精确等于其**模式选择性吸收率（mode-selective absorptivity）** $\mathcal{A}_{\text{channel}}$ [@problem_id:2511654]：

$$
\mathcal{E}_{\text{channel}}(\omega) = \mathcal{A}_{\text{channel}}(\omega)
$$

这个等式的成立，源于发射和吸收过程的共同物理根源。根据 FDT，发射功率正比于一个涉及场[分布](@entry_id:182848)和材料耗散部分的积分。而根据电磁理论，[吸收功率](@entry_id:265908)也正比于同一个积分。具体来说，两者都可以表示为如下形式的二次型积分 [@problem_id:2511654]：

$$
\int_V \mathbf{E}_{\text{rec}}^*(\mathbf{r},\omega) \cdot \operatorname{Im}\{\boldsymbol{\varepsilon}(\mathbf{r},\omega)\} \cdot \mathbf{E}_{\text{rec}}(\mathbf{r},\omega) d^3\mathbf{r}
$$

其中 $\mathbf{E}_{\text{rec}}$ 是由该通道的外部源在物体内部产生的[电场](@entry_id:194326)。因为[发射率](@entry_id:143288)和[吸收率](@entry_id:144520)最终都与同一个物理量成正比，经过恰当的归一化后，它们必然相等。这个定律对于理解和设计纳米尺度下的[热辐射](@entry_id:145102)器件至关重要。

值得注意的是，如果系统不满足互易性（例如，在静[磁场](@entry_id:153296)偏置下的磁光材料），则上述等式不再成立。取而代之的是一个修正的关系：在偏置场为 $\mathbf{B}_0$ 时的[发射率](@entry_id:143288)等于在[反向偏置](@entry_id:160088)场 $-\mathbf{B}_0$ 时的吸收率，即 $\mathcal{E}(\mathbf{B}_0) = \mathcal{A}(-\mathbf{B}_0)$ [@problem_id:2511654]。

### 高级主题与理论局限

尽管基于局域响应和局域[热力学平衡](@entry_id:141660)的涨落[电动力学](@entry_id:158759)取得了巨大成功，但在某些极端条件下，其基本假设会失效。

#### 格林函数张量形式理论

Polder-van Hove 公式适用于简单的[平行平面](@entry_id:165919)几何。对于任意形状的物体，计算近场热辐射需要更普适的工具——**格林函数张量（DGF）** 形式理论。DGF $\mathbf{G}(\mathbf{r}, \mathbf{r}'; \omega)$ 是描述从 $\mathbf{r}'$ 处的点[电流源](@entry_id:275668)到 $\mathbf{r}$ 处产生的[电场](@entry_id:194326)的[线性响应函数](@entry_id:160418)，它满足一个矢量[亥姆霍兹方程](@entry_id:149977) [@problem_id:2511639]：

$$
[\nabla \times \nabla \times - k_0^2 \varepsilon(\mathbf{r},\omega)] \mathbf{G}(\mathbf{r}, \mathbf{r}'; \omega) = \mathbf{I}\delta(\mathbf{r}-\mathbf{r}')
$$

一旦求出系统的[格林函数](@entry_id:147802)，总热流就可以通过一个包含[格林函数](@entry_id:147802)和材料[介电函数](@entry_id:136859)的积分表达式来计算。对于像多层膜这样的分层介质，可以利用其横向平移不变性，将 DGF 分解为平面[波的叠加](@entry_id:166456)，即**外尔（Weyl）分解**，这大大简化了计算 [@problem_id:2511639]。

#### 局域近似的失效

标准理论假设材料的响应是**局域的**，即一点的极化只取决于该点的[电场](@entry_id:194326)。这个假设在[电磁场](@entry_id:265881)的空间变化尺度远大于材料内部载流子（电子、[声子](@entry_id:140728)）的[平均自由程](@entry_id:139563) $\ell$ 时是成立的。然而，在近场热辐射中，当间距 $d$ 变得极小（例如 $d$ 小于几纳米）时，起主导作用的[倏逝波](@entry_id:156713)的平[行波](@entry_id:185008)矢 $k_\parallel \sim 1/d$ 会非常大。这意味着[电磁场](@entry_id:265881)在空间上以 $\sim d$ 的尺度剧烈变化。

当 $d$ 小于或接近载流子[平均自由程](@entry_id:139563) $\ell$ 时，局域近似失效 [@problem_id:2511641]。载流子在一个碰撞周期内会“感受”到大片区域内变化的[电磁场](@entry_id:265881)，因此材料的响应变为**非局域的（nonlocal）**。此时，[介电函数](@entry_id:136859)不再是一个只依赖于频率 $\omega$ 的标量或张量，而是一个同时依赖于频率 $\omega$ 和[波矢](@entry_id:178620) $\mathbf{k}$ 的函数，即 $\varepsilon(\omega, \mathbf{k})$。空间非局域性效应修正了对大波矢 $k_\parallel$ 模式的描述，它提供了一个自然的物理截止，从而消除了局域理论在 $d \to 0$ 时可能出现的非物理发散，使热流在极小间距下饱和到一个有限值 [@problem_id:2511641]。

此外，极高的[近场](@entry_id:269780)[热流密度](@entry_id:138471)也可能打破**局域[热力学平衡](@entry_id:141660)（LTE）**的假设。例如，在金属中，[近场辐射](@entry_id:153085)能量主要被电子吸收。如果能量输入速率超过[电子-声子散射](@entry_id:138098)的[能量弛豫](@entry_id:136820)速率，电子系统的温度 $T_e$ 将会显著高于[晶格](@entry_id:196752)（[声子](@entry_id:140728)）温度 $T_l$。在这种**非平衡**状态下，应用 FDT 时必须小心区分：与电子运动相关的涨落[电流源](@entry_id:275668)应由[电子温度](@entry_id:180280) $T_e$ 决定，而与[晶格振动](@entry_id:140970)相关的涨落则应由 $T_l$ 决定。这种更精细的描述，例如**[双温模型](@entry_id:180856)（Two-Temperature Model, TTM）**，对于精确预测极端[近场](@entry_id:269780)条件下的热传递是必需的 [@problem_id:2511641]。