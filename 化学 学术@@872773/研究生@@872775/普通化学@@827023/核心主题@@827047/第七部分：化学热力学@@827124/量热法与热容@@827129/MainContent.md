## 引言
[热容](@entry_id:137594)与[量热法](@entry_id:145378)是物理化学领域的核心概念，它们不仅是连接物质微观能量世界与宏观热学性质的桥梁，也是理解和预测物质行为的基石。从宏观上看，[热容](@entry_id:137594)描述了物质储存热能的能力；从微观上看，它反映了能量在分子内部各种自由度上的分配方式。尽管学生对[热容](@entry_id:137594)的基本定义（如恒压[热容](@entry_id:137594) $C_p$ 和恒容[热容](@entry_id:137594) $C_V$）并不陌生，但对于其深刻的物理内涵、在复杂体系（如[非理想溶液](@entry_id:142298)、高分子材料）中的表现，以及如何通过先进的量热技术应用于前沿科学研究，往往缺乏系统性的认识。

本文旨在填补这一知识鸿沟，为读者构建一个从基础理论到高级应用的完整知识框架。在接下来的章节中，我们将踏上一段探索热容奥秘的旅程。首先，在“原理与机制”一章中，我们将回归第一性原理，从宏观[热力学](@entry_id:141121)和微观[统计力](@entry_id:194984)学的角度剖析[热容](@entry_id:137594)的本质，并介绍描述气体和固体的经典模型。随后，在“应用与跨学科连接”一章中，我们将展示[量热学](@entry_id:145378)作为一种强大的分析工具，如何在生物物理、[材料科学](@entry_id:152226)、电化学等领域解决实际问题，揭示从[分子识别](@entry_id:151970)到[量子相变](@entry_id:146027)的各种现象。最后，在“动手实践”部分，读者将有机会通过具体问题来巩固和应用所学知识。通过这三章的学习，读者将深刻理解[热容](@entry_id:137594)这一物理量如何贯穿于理论与实验，并成为推动跨学科创新的关键。

## 原理与机制

本章旨在深入探讨热容的物理原理与基本机制。在前一章介绍性概述的基础上，我们将从宏观[热力学](@entry_id:141121)定义出发，逐步深入到其微观[统计力](@entry_id:194984)学根源，并最终将这些原理应用于气体、固体、混合物乃至动力学过程等复杂系统。

### 宏观[热力学](@entry_id:141121)基础

[热容](@entry_id:137594)是联系能量与温度的核心物理量，其定义植根于[热力学第一定律](@entry_id:146485)。对于一个封闭系统，其内能 $U$ 的无穷小变化 $dU$ 等于吸收的热量 $\delta q$ 与系统所做的功 $\delta w$ 之和。根据化学中通用的IUPAC符号约定（系统吸收能量为正），第一定律写作：

$dU = \delta q + \delta w$

这里，$d$ 表示[状态函数](@entry_id:137683)（如内能 $U$）的[全微分](@entry_id:171747)，其积分值仅依赖于初末态；而 $\delta$ 表示[路径函数](@entry_id:144689)（如热 $q$ 和功 $w$）的非[全微分](@entry_id:171747)，其积分值依赖于过程的具体路径。热容的测量通常在特定约束条件下进行，这使得热量这个[路径函数](@entry_id:144689)与某个状态函数的变化直接关联起来。

两种最基本的测量条件是恒容过程和恒压过程。

在恒容（isochoric）过程中，体积不变（$dV=0$）。如果系统只做压力-体积（$pV$）功（$\delta w = -p_{\text{ext}} dV$），那么功为零。此时，第一定律简化为 $dU = \delta q_V$。对于一个有限的过程，这意味着系统吸收的热量 $q_V$ 完[全等](@entry_id:273198)于其内能的变化 $\Delta U$：

$q_V = \Delta U$

因此，**恒容热容**（**heat capacity at constant volume**），$C_V$，被定义为内能随温度在恒定体积下的变化率：

$C_V \equiv \left(\frac{\partial U}{\partial T}\right)_V$

在恒压（isobaric）过程中，压力保持恒定。当系统只做 $pV$ 功时，$\delta w = -p dV$。第一定律变为 $dU = \delta q_p - p dV$，整理后得到 $\delta q_p = dU + p dV$。这个表达式恰好是焓（enthalpy）$H \equiv U + pV$ 在恒压下的微分形式（$dH = dU + p dV + V dp$，当 $dp=0$ 时 $dH_p = dU + p dV$）。因此，在恒压下，系统吸收的热量 $q_p$ 等于其[焓变](@entry_id:147639) $\Delta H$：

$q_p = \Delta H$

相应地，**恒压热容**（**heat capacity at constant pressure**），$C_p$，被定义为焓随温度在恒定压力下的变化率：

$C_p \equiv \left(\frac{\partial H}{\partial T}\right)_p$

这些关系是[量热学](@entry_id:145378)的基石。例如，一个密闭的[弹式量热计](@entry_id:141639)在恒定体积下运行，因此测得的热量直接对应 $\Delta U$。相反，在敞口烧杯中或使用带活塞的装置进行的反应，是在恒定大气压下进行的，测得的热效应对应 $\Delta H$。[@problem_id:2926471]

值得注意的是，如果系统可以做[非体积功](@entry_id:137402)（non-$pV$ work），$\delta w_{\text{non-}pV}$（如[电功](@entry_id:273970)），那么总功变为 $\delta w = -p dV + \delta w_{\text{non-}pV}$。在这种情况下，恒压热 $q_p$ 与焓变的关系修正为 $q_p = \Delta H - w_{\text{non-}pV}$。而在恒容条件下，由于 $pV$ 功仍为零，关系变为 $q_V = \Delta U - w_{\text{non-}pV}$。这表明，只有在不存在[非体积功](@entry_id:137402)的情况下，量热测定的热量才直接等于 $\Delta U$ 或 $\Delta H$。[@problem_id:2926471]

$C_p$ 和 $C_V$ 并非[相互独立](@entry_id:273670)，它们之间的差值深刻地揭示了物质的膨胀和压缩特性。通过严格的[热力学](@entry_id:141121)推导，可以证明：

$C_p - C_V = \frac{T V \alpha^2}{\kappa_T}$

其中，$T$ 是绝对温度，$V$ 是体积，$\alpha$ 是**[体膨胀](@entry_id:144241)系数**（**coefficient of thermal expansion**），$\kappa_T$ 是**[等温压缩率](@entry_id:140894)**（**isothermal compressibility**）。它们的定义分别为：

$\alpha \equiv \frac{1}{V}\left(\frac{\partial V}{\partial T}\right)_p$

$\kappa_T \equiv -\frac{1}{V}\left(\frac{\partial V}{\partial p}\right)_T$

这个关系式非常重要。首先，由于 $T, V, \kappa_T$ 均为正值（热力学稳定性要求），$C_p - C_V \ge 0$，这意味着 $C_p$ 总是大于或等于 $C_V$。其物理意义是，在恒压下加热物质，一部分能量用于提高内能（增加[分子动能](@entry_id:138083)和势能），另一部分则用于对外做膨胀功，因此需要更多的热量才能使温度升高同样的度数。差值的大小与热膨胀系数 $\alpha$ 的平方成正比，表明热膨胀越显著的材料，$C_p$ 和 $C_V$ 的差异也越大。对于[理想气体](@entry_id:200096)，该公式可以简化为 $C_{p,m} - C_{V,m} = R$（其中 $R$ 是[理想气体](@entry_id:200096)常数）。[@problem_id:2926521]

为了统一描述固体的热学和力学性质，引入了**[格林艾森参数](@entry_id:143264)**（**Grüneisen parameter**），$\gamma_G$。它是一个无量纲参数，有多种等价定义，其中一种将其与我们刚讨论过的响应函数联系起来：

$\gamma_G = \frac{V \alpha K_T}{C_V} = \frac{V \alpha}{C_V \kappa_T}$

这里 $K_T = 1/\kappa_T$ 是等温体模量。该参数建立了[热膨胀](@entry_id:137427)、压缩性与热容之间的联系，它在地球物理和[材料科学](@entry_id:152226)中尤为重要，因为它描述了晶格振动频率如何随体积变化，从而影响材料的[热压](@entry_id:159509)性质，例如在[绝热压缩](@entry_id:142708)过程中温度如何随压力变化。[@problem_id:2926465]

### [热容](@entry_id:137594)的微观起源

宏观[热力学](@entry_id:141121)定义了热容并揭示了其与其他宏观性质的关系，但要理解热容的根本来源——物质为何具有特定的[热容](@entry_id:137594)值，以及[热容](@entry_id:137594)为何随温度变化——我们必须转向微观层面，即[统计力](@entry_id:194984)学。

[统计力](@entry_id:194984)学的核心思想是，宏观性质是大量微观粒子行为的系综平均。一个处于[平衡态](@entry_id:168134)的系统，其能量不是一个固定值，而是在一个平均值附近涨落。**涨落-响应定理**（**fluctuation-response theorem**）深刻地指出，系统对外界微扰的宏观响应（如[热容](@entry_id:137594)）与系统在没有微扰时自发的微观涨落（如[能量涨落](@entry_id:148029)）直接相关。

对于一个与温度为 $T$ 的[热库](@entry_id:143608)接触的恒容系统（正则系综），其恒容[热容](@entry_id:137594) $C_V$ 与系统内能 $U$ 的方均根涨落 $\langle (\Delta U)^2 \rangle = \langle (U - \langle U \rangle)^2 \rangle$ 之间存在精确关系：

$C_V = \frac{\langle (\Delta U)^2 \rangle}{k_B T^2}$

类似地，对于一个同时与热库和压力为 $p$ 的压力库接触的系统（[等温等压系综](@entry_id:143530)），其恒压[热容](@entry_id:137594) $C_p$ 与焓 $H$ 的涨落相关：

$C_p = \frac{\langle (\Delta H)^2 \rangle}{k_B T^2}$

其中 $k_B$ 是[玻尔兹曼常数](@entry_id:142384)。这些关系表明，[热容](@entry_id:137594)越大，意味着系统在给定温度下储存和交换能量的微观模式越多，导致其能量（或焓）的自发涨落越剧烈。一个系统的[热容](@entry_id:137594)本质上是其内部能量自由度数量和可及性的量度。[@problem_id:2926449]

#### [气体的热容](@entry_id:153522)

对于由独立分子组成的气体，总[热容](@entry_id:137594)是分子平动、转动和[振动](@entry_id:267781)贡献的总和。根据经典**[能量均分定理](@entry_id:136972)**（**equipartition theorem**），在足够高的温度下，能量表达式中每个二次项（如 $\frac{1}{2}mv_x^2$ 或 $\frac{1}{2}I\omega_y^2$）对[摩尔热容](@entry_id:144045)的贡献是 $\frac{1}{2}R$。

然而，量子力学揭示了能量并非连续的。[分子转动](@entry_id:172532)和[振动能级](@entry_id:193001)是量子化的，只有当热能 $k_B T$ 与[能级间距](@entry_id:181168) $\Delta E$ 相当或更大时，这些模式才能被有效激发，从而对[热容](@entry_id:137594)做出贡献。我们可以定义**特征温度**（**characteristic temperature**）$\theta = \Delta E / k_B$ 来表征激发所需的温标。

以[双原子分子](@entry_id:148655)为例，其[热容](@entry_id:137594)随温度的变化是一个经典的多步过程 [@problem_id:2926485]：
1.  **[平动](@entry_id:187700)**：分子有3个[平动自由度](@entry_id:140257)。其[能级间距](@entry_id:181168)极小，在任何实际温度下都可视为经典模式，因此始终贡献 $\frac{3}{2}R$ 的摩尔恒容[热容](@entry_id:137594)。在低温下，当只有平动模式被激发时，[热容](@entry_id:137594)达到第一个平台，即 $C_V = \frac{3}{2}R$ 和 $C_p = C_V + R = \frac{5}{2}R$。
2.  **转动**：线性分子有2个[转动自由度](@entry_id:141502)。转动能级间距由转动常数 $B$ 决定，特征温度 $\theta_{\text{rot}} = hc\tilde{B}/k_B$ 通常只有几开尔文。当温度 $T$ 远大于 $\theta_{\text{rot}}$ 时，转动被完全激发，对 $C_V$ 贡献 $2 \times \frac{1}{2}R = R$。此时 $C_V \to \frac{5}{2}R$，$C_p \to \frac{7}{2}R$。
3.  **[振动](@entry_id:267781)**：双原子分子有1个[振动](@entry_id:267781)模式。[振动能级](@entry_id:193001)间距由[振动频率](@entry_id:199185) $\nu$ 决定，特征温度 $\theta_{\text{vib}} = h\nu/k_B$ 通常高达数千开尔文。当温度 $T$ 远大于 $\theta_{\text{vib}}$ 时，[振动](@entry_id:267781)模式被完全激发。由于[振动](@entry_id:267781)包含动能和[势能](@entry_id:748988)两个二次项，它对 $C_V$ 贡献 $2 \times \frac{1}{2}R = R$。此时 $C_V \to \frac{7}{2}R$，$C_p \to \frac{9}{2}R$。

因此，随着温度从低到高，双原子理想气体的 $C_p$ 会依次经历从 $\frac{5}{2}R$ 到 $\frac{7}{2}R$ 再到 $\frac{9}{2}R$ 的平台跃迁，这些跃迁清晰地反映了[量子化能级](@entry_id:140911)被逐级热激发的物理图像。

#### [固体的热容](@entry_id:144937)

在晶体中，原子并非独立运动，而是以集体[振动](@entry_id:267781)的形式存在，这些[振动](@entry_id:267781)的量子被称为**[声子](@entry_id:140728)**（**phonons**）。[固体的热容](@entry_id:144937)主要来自于这些[晶格振动](@entry_id:140970)的热激发。

描述晶格振动的关键是**[声子态密度](@entry_id:199476)**（**phonon density of states**），$g(\omega)$，它定义了单位频率间隔内的[振动](@entry_id:267781)模式数量。系统的总内能是通过对所有频率的[振动](@entry_id:267781)模式的平均能量进行积分得到的。一个频率为 $\omega$ 的[量子谐振子](@entry_id:140678)的平均热能为 $\hbar\omega / (\exp(\hbar\omega/k_B T) - 1)$。值得强调的是，[谐振子](@entry_id:155622)的零点能 $\frac{1}{2}\hbar\omega$ 是一个与温度无关的常数，因此它对内能有贡献，但其对温度的导数为零，故**零点能不贡献热容**。

固体的总恒容热容 $C_V$ 可以表示为对[声子态密度](@entry_id:199476)的积分 [@problem_id:2926523]：

$C_V(T) = \int_0^\infty g(\omega) \left[ k_B \left(\frac{\hbar\omega}{k_B T}\right)^2 \frac{\exp(\hbar\omega/k_B T)}{(\exp(\hbar\omega/k_B T) - 1)^2} \right] d\omega$

括号中的项是单个频率为 $\omega$ 的[谐振子](@entry_id:155622)对热容的贡献，常被称为**爱因斯坦热容函数**。整个公式表明，[固体的热容](@entry_id:144937)是所有[声子模式](@entry_id:201212)贡献的加权总和。

由于直接确定 $g(\omega)$ 很困难，人们发展了简化模型：
-   **爱因斯坦模型**（**Einstein model**）：假设所有 $3N$ 个[振动](@entry_id:267781)模式都具有相同的频率 $\omega_E$。这对应于一个针状的态密度 $g(\omega) \propto \delta(\omega - \omega_E)$。该模型在高温下能正确预言[热容](@entry_id:137594)趋于**[杜隆-珀蒂定律](@entry_id:191078)**（**Dulong-Petit law**）的极限值 $3R$，但在低温下，它预言 $C_V$ 随温度呈指数衰减（$e^{-\Theta_E/T}$），这与实验不符。[@problem_id:2926448]
-   **[德拜模型](@entry_id:141712)**（**Debye model**）：将固体视为弹性连续介质，假设[声子态密度](@entry_id:199476)与频率的平方成正比（$g(\omega) \propto \omega^2$），直到一个[截止频率](@entry_id:276383) $\omega_D$。该模型在低温下给出了著名的**德拜 $T^3$ 定律**：

$C_V(T) \propto T^3 \quad (T \ll \Theta_D)$

其中 $\Theta_D = \hbar\omega_D/k_B$ 是[德拜温度](@entry_id:140328)。这个 $T^3$ 行为与实验非常吻合，因为它正确地描述了低能量（长波长）声学声子的主导作用。在高温下，[德拜模型](@entry_id:141712)同样回归到 $3R$ 的极限。[@problem_id:2926448]

区分爱因斯坦模型和德拜模型的关键在于低温区的行为。精确的低温量热数据，特别是对 $C_V$ 与 $T$ 的对数-对数图进行[幂律](@entry_id:143404)拟合，可以有效地检验系统是否遵循 $T^3$ 定律。从实践上看，由量热数据 $C_V(T)$ 反演得到[声子态密度](@entry_id:199476) $g(\omega)$ 是一个数学上的“[不适定问题](@entry_id:182873)”（ill-posed problem），微小的[实验误差](@entry_id:143154)可能导致 $g(\omega)$ 出现巨大的、不符合物理实际的[振荡](@entry_id:267781)。因此，为了获得可靠的 $g(\omega)$，通常需要结合其他实验手段，如**[非弹性中子散射](@entry_id:140691)**（**inelastic neutron scattering, INS**），它能提供关于 $g(\omega)$ 的直接信息（如[声子谱](@entry_id:753408)的边界、[色散关系](@entry_id:140395)等），作为正则化约束条件来稳定拟合过程。[@problem_id:2926523]

### 混合物与复杂体系的热容

将热容的概念应用于混合物时，我们需要区分**[广延性质](@entry_id:145410)**（**extensive properties**）和**[强度性质](@entry_id:181209)**（**intensive properties**）。总热容 $C_{p, \text{tot}}$ 是一个广延量，它与系统的[物质的量](@entry_id:140225)成正比；而[摩尔热容](@entry_id:144045) $C_{p,m} = C_{p, \text{tot}}/n$ 和比热容 $c_p = C_{p, \text{tot}}/m$ 则是强度量，不依赖于系统的大小。[@problem_id:2926516]

对于一个由互不相互作用的组分构成的宏观混合体系，其总热容是各组分热容的简单加和。然而，当组分在[分子尺](@entry_id:166706)度上混合形成溶液时，情况变得复杂。

对于**[理想溶液](@entry_id:148303)**（**ideal solution**），其一个关键特征是[混合焓](@entry_id:158999) $\Delta H_{\text{mix}}$ 为零。由于混合物的摩尔焓 $H_{\text{mix}}$ 等于纯组分摩尔焓的[摩尔分数](@entry_id:145460)加权平均值，即 $H_{\text{mix}} = \sum_i x_i H_i$，对其求温度的偏导数可得：

$C_{p, \text{mix}} = \left(\frac{\partial H_{\text{mix}}}{\partial T}\right)_{p,x} = \sum_i x_i \left(\frac{\partial H_i}{\partial T}\right)_p = \sum_i x_i C_{p,i}$

因此，对于[理想溶液](@entry_id:148303)，其[摩尔热容](@entry_id:144045)是纯组分[摩尔热容](@entry_id:144045)的摩尔分数加权平均值。[@problem_id:2926452] [@problem_id:2926516]

对于**[非理想溶液](@entry_id:142298)**，混合过程伴随着[分子间相互作用](@entry_id:263767)力的改变，导致[混合焓](@entry_id:158999) $\Delta H_{\text{mix}}$ 不为零。混合物的摩尔焓为 $H_{\text{mix}} = \sum_i x_i H_i + \Delta H_{\text{mix}}$。其[摩尔热容](@entry_id:144045)相应地变为：

$C_{p, \text{mix}} = \sum_i x_i C_{p,i} + \left(\frac{\partial \Delta H_{\text{mix}}}{\partial T}\right)_{p,x}$

与理想行为的偏差由一个额外的项——**超额热容**（**excess heat capacity**），$C_p^E$——来描述：

$C_p^E \equiv C_{p, \text{mix}} - \sum_i x_i C_{p,i} = \left(\frac{\partial \Delta H_{\text{mix}}}{\partial T}\right)_{p,x}$

超额热容的存在意味着混合物的热容通常不等于组分热容的简单加权平均。它的物理根源在于，[分子间相互作用](@entry_id:263767)的强度随温度变化，从而影响了系统储存热能的方式。如果[混合焓](@entry_id:158999) $\Delta H_{\text{mix}}$ 具有明显的温度依赖性，$C_p^E$ 就会很大。例如，如果一个放热混合过程（$\Delta H_{\text{mix}}  0$）的放热量随温度升高而减小（即 $(\partial \Delta H_{\text{mix}} / \partial T)  0$），那么该混合物就会有正的超额热容。[@problem_id:2926452] 此外，超额[热容](@entry_id:137594)还与[超额吉布斯能](@entry_id:172602) $G^E$ 存在一个重要的[热力学](@entry_id:141121)关系 $C_p^E = -T(\partial^2 G^E / \partial T^2)_{p,x}$，这为通过其他[热力学](@entry_id:141121)测量（如[气液平衡](@entry_id:147234)）推算[热容](@entry_id:137594)提供了途径。[@problem_id:2926452]

### 动态与频率依赖的[热容](@entry_id:137594)

我们目前讨论的[热容](@entry_id:137594)都是**静态**（**static**）或**平衡**（**equilibrium**）性质。然而，在许多材料中，特别是聚合物、玻璃和其他无序体系中，分子重排和[构象变化](@entry_id:185671)需要一定的时间，这些过程是[动力学控制](@entry_id:154879)的。当我们以有限的速率加热这类材料时，系统可能无法即时达到[热力学平衡](@entry_id:141660)。

**调温[差示扫描量热法](@entry_id:151282)**（**Temperature-Modulated Differential Scanning Calorimetry, TMDSC**）是一种强大的技术，用于研究这类动力学过程。它在传统的线性升温速率上叠加一个小的正弦温度[振荡](@entry_id:267781)：$T(t) = T_0 + \beta t + \Delta T \cos(\omega t)$。通过分析系统对这个正弦扰动的响应——即测量的热流速率 $P(t)$ 的振幅和相位——我们可以获得关于体系动力学的信息。

为了描述这种频率依赖的响应，我们引入**复数热容**（**complex heat capacity**），$C_p^*(\omega)$。它是在[频域](@entry_id:160070)中对热容概念的推广。对于一个小的正弦温度扰动 $\tilde{T}(\omega)e^{i\omega t}$，它引起的焓响应为 $\tilde{H}(\omega)e^{i\omega t}$。而热流是焓的时间导数，$\tilde{P}(\omega) = i\omega \tilde{H}(\omega)$。复数热容被严谨地定义为：

$C_p^*(\omega) = \frac{\tilde{H}(\omega)}{\tilde{T}(\omega)} = \frac{\tilde{P}(\omega)}{i\omega \tilde{T}(\omega)}$

复数[热容](@entry_id:137594)通常写作 $C_p^*(\omega) = C_p'(\omega) - i C_p''(\omega)$。其实部和虚部分别具有明确的物理意义 [@problem_id:2926459]：
-   $C_p'(\omega)$ 是**[储能](@entry_id:264866)[热容](@entry_id:137594)**（**storage heat capacity**），它与热流中和温度扰动**异相**（out-of-phase，相差 $90^\circ$）的部分成正比。它代表了系统在振荡周期内可逆储存和释放热能的能力，类似于静态热容。
-   $C_p''(\omega)$ 是**损耗热容**（**loss heat capacity**），它与热流中和温度扰动**同相**（in-phase）的部分成正比。它代表了在[振荡](@entry_id:267781)过程中由于不可逆的弛豫过程而耗散的能量。根据热力学第二定律，损耗必须为正值，即 $C_p''(\omega) \ge 0$。

在一个典型的TMDSC实验中，如果温度输入是 $\Delta T \cos(\omega t)$，测得的热流响应是 $P_0 \cos(\omega t + \varphi)$，那么 $C_p'$ 和 $C_p''$ 可以通过测得的振幅 $P_0$、$\Delta T$ 和相位角 $\varphi$ 计算得出：

$C_p'(\omega) = \frac{P_0}{\omega \Delta T} \sin\varphi$

$C_p''(\omega) = \frac{P_0}{\omega \Delta T} \cos\varphi$

对于一个具有单一弛豫时间 $\tau$ 的简单动力学过程（例如，[Debye弛豫](@entry_id:160383)），复数热容的形式为：

$C_p^*(\omega) = \frac{C_0}{1 + i\omega\tau}$

其中 $C_0$ 是低频极限下的平衡热容。其实部和虚部分别为：

$C_p'(\omega) = \frac{C_0}{1 + (\omega\tau)^2}$

$C_p''(\omega) = \frac{C_0 \omega\tau}{1 + (\omega\tau)^2}$

$C_p''(\omega)$ 在 $\omega\tau=1$ 时达到峰值。通过在不同频率下测量 $C_p^*(\omega)$，我们可以确定材料内部动力学过程的特征时间 $\tau$ 及其温度依赖性，这对于研究[玻璃化转变](@entry_id:142461)等现象至关重要。[@problem_id:2926459]