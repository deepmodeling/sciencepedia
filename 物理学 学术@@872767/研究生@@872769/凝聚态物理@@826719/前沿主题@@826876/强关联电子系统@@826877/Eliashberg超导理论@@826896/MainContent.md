## 引言
超[导电性](@entry_id:137481)，作为一种零电阻和[完全抗磁性](@entry_id:203008)的[宏观量子现象](@entry_id:144018)，是凝聚态物理学中最深刻的主题之一。Bardeen-Cooper-Schrieffer (BCS) 理论基于[声子](@entry_id:140728)媒介的[库珀配对](@entry_id:195218)，为其提供了突破性的微观解释，并在弱耦合[超导体](@entry_id:191025)中取得了巨大成功。然而，随着实验探索的深入，人们发现许多材料——特别是那些具有更高临界温度的材料——其性质显著偏离了[BCS理论](@entry_id:144185)的预言。[BCS理论](@entry_id:144185)核心的瞬时相互作用近似，被证明不足以描述这些“强耦合”体系，这在我们对超导的理解中留下了一个关键的知识空白。

本文旨在深入探讨艾利希伯[格理论](@entry_id:147950)，它是BCS理论的强大推广，严谨地处理了[电子-声子相互作用](@entry_id:140708)的推迟（retarded）特性以及[配对机制](@entry_id:145844)完整的能量依赖性。通过超越简化的近似，艾利希伯格框架为理解真实世界中[超导体](@entry_id:191025)的丰富物理提供了一个定量的、可预测的工具。在本文中，我们将对这个现代[凝聚态理论](@entry_id:141958)的基石进行一次全面的探索。

第一章 **“原理与机制”** 将为我们奠定理论基础。我们将从基本的电子-[声子](@entry_id:140728)[哈密顿量](@entry_id:172864)出发，探究推迟相互作用的起源，并阐述关键的[Migdal定理](@entry_id:145760)的物理依据。这将引导我们推导出Nambu-Gor'kov形式下的核心[Eliashberg方程](@entry_id:147834)，并引入诸如[谱函数](@entry_id:147628)$\alpha^2F(\Omega)$、[质量重整化](@entry_id:139777)和[库仑赝势](@entry_id:145447)$\mu^*$等关键概念。

接下来，在 **“应用与跨学科交叉”** 一章中，我们将展示该理论的实际威力。我们将探讨艾利希伯[格理论](@entry_id:147950)如何与实验可观测量直接联系，从而能够解析隧道谱和[角分辨光电子能谱](@entry_id:139661)（ARPES）数据，以及它如何实现对[临界温度](@entry_id:146683)等[材料性质](@entry_id:146723)的第一性原理预测。我们还将考察其在各向异性、多带乃至非[声子](@entry_id:140728)媒介[超导体](@entry_id:191025)等更复杂系统中的推广应用。

最后，为了巩固您的理解，**“动手实践”** 部分将提供一系列引导性问题。这些练习旨在引导您从计算基本的[电子自能](@entry_id:148523)，到处理多元素[超导体中的同位素效应](@entry_id:264632)等高级课题，从而在理论概念与实际应用之间架起一座桥梁。

让我们首先从构成艾利希伯[格理论](@entry_id:147950)基础的基本原理与机制开始探索。

## 原理与机制

在上一章中，我们介绍了由[声子](@entry_id:140728)介导的吸引作用是传统超导电性微观理论的核心。然而，Bardeen-Cooper-Schrieffer (BCS) 理论所做的瞬时相互作用近似，虽然在[弱耦合](@entry_id:140994)极限下取得了巨大成功，但无法完全描述许多真实材料中观察到的现象，特别是在[电子-声子耦合](@entry_id:139197)较强的材料中。本章旨在深入探讨 Eliashberg 理论的原理和机制，该理论是 BCS 理论的推广，它严谨地处理了相互作用的推迟（retarded）特性及其对电子性质的深刻影响。我们将从[哈密顿量](@entry_id:172864)出发，逐步构建理论框架，揭示其核心方程，并阐述其关键的物理后果。

### 微观基础：电子-[声子](@entry_id:140728)[哈密顿量](@entry_id:172864)

传统超[导电性](@entry_id:137481)理论的出发点是描述[晶格](@entry_id:196752)中[传导电子](@entry_id:145260)与离子[振动](@entry_id:267781)（[声子](@entry_id:140728)）相互作用的微观模型。这个模型通常由 Fröhlich [哈密顿量](@entry_id:172864)给出，其形式如下：

$$
H = \sum_{k,\sigma} \epsilon_{k} c_{k,\sigma}^{\dagger}c_{k,\sigma} + \sum_{q,\nu} \Omega_{q,\nu} b_{q,\nu}^{\dagger}b_{q,\nu} + \sum_{k,q,\sigma,\nu} g_{k,q,\nu} c_{k+q,\sigma}^{\dagger}c_{k,\sigma} (b_{q,\nu} + b_{-q,\nu}^{\dagger})
$$

这个[哈密顿量](@entry_id:172864)包含三个部分 [@problem_id:2986485]：

1.  **电子动能项**：$H_{\text{el}} = \sum_{k,\sigma} \epsilon_{k} c_{k,\sigma}^{\dagger}c_{k,\sigma}$。该项描述了晶体中非相互作用电子的能量。其中，$c_{k,\sigma}^{\dagger}$ 和 $c_{k,\sigma}$ 分别是动量为 $\hbar k$、自旋为 $\sigma$ 的电子的产生和[湮灭算符](@entry_id:165390)，$\epsilon_k$ 是相对于化学势的电子能带[色散关系](@entry_id:140395)。

2.  **[声子](@entry_id:140728)能量项**：$H_{\text{ph}} = \sum_{q,\nu} \Omega_{q,\nu} b_{q,\nu}^{\dagger}b_{q,\nu}$（为简洁起见，我们省略了零点能）。该项描述了[晶格振动](@entry_id:140970)的能量，即[声子](@entry_id:140728)。$b_{q,\nu}^{\dagger}$ 和 $b_{q,\nu}$ 分别是[波矢](@entry_id:178620)为 $q$、属于[声子支](@entry_id:189965) $\nu$ 的[声子](@entry_id:140728)的产生和湮灭算符，$\Omega_{q,\nu}$ 是[声子](@entry_id:140728)的[色散关系](@entry_id:140395)。

3.  **[电子-声子相互作用](@entry_id:140708)项**：$H_{\text{el-ph}} = \sum_{k,q,\sigma,\nu} g_{k,q,\nu} c_{k+q,\sigma}^{\dagger}c_{k,\sigma} (b_{q,\nu} + b_{-q,\nu}^{\dagger})$。这是理论的核心。它描述了一个电子从动量为 $k$ 的态散射到动量为 $k+q$ 的态，同时伴随着吸收一个[波矢](@entry_id:178620)为 $q$ 的[声子](@entry_id:140728)（$b_{q,\nu}$ 项）或发射一个[波矢](@entry_id:178620)为 $-q$ 的[声子](@entry_id:140728)（$b_{-q,\nu}^{\dagger}$ 项）。矩阵元 $g_{k,q,\nu}$ 量化了这种耦合的强度。物理上，算符组合 $c_{k+q,\sigma}^{\dagger}c_{k,\sigma}$ 代表了波矢为 $q$ 的电子密度起伏，该起伏与由 $(b_{q,\nu} + b_{-q,\nu}^{\dagger})$ 代表的[晶格](@entry_id:196752)位移场相耦合。

### 有效相互作用的出现：[推迟效应](@entry_id:199612)

[哈密顿量](@entry_id:172864)中的相互作用项直接耦合了电子和[声子](@entry_id:140728)，但没有直接的[电子-电子相互作用](@entry_id:139900)项。然而，通过交换虚[声子](@entry_id:140728)，电子之间可以产生一种有效的相互作用。这个过程是理解[声子介导超导](@entry_id:202894)电性的关键。

想象一下这个过程的[时间演化](@entry_id:153943) [@problem_id:2986543]：一个电子穿过[晶格](@entry_id:196752)，其携带的负[电荷](@entry_id:275494)会吸引周围带正电的离子核，使[晶格](@entry_id:196752)发生局部畸变。这种畸变（即[声子](@entry_id:140728)云）并不会瞬时形成和消失，而是以[晶格](@entry_id:196752)的本征[响应时间](@entry_id:271485) $\tau_{\text{ph}} \sim 1/\Omega_D$（其中 $\Omega_D$ 是特征[声子频率](@entry_id:753407)，如[德拜频率](@entry_id:153821)）来演化。这个[响应时间](@entry_id:271485)远长于电子的[特征时间尺度](@entry_id:276738) $\tau_{\text{el}} \sim 1/E_F$（其中 $E_F$ 是[费米能](@entry_id:143977)）。由于 $E_F \gg \hbar\Omega_D$，我们有 $\tau_{\text{el}} \ll \tau_{\text{ph}}$。因此，当第一个电子已经离开该区域后，它留下的[晶格](@entry_id:196752)畸变（一个正[电荷](@entry_id:275494)过剩的“尾迹”）仍然存在。第二个电子在稍晚时刻到达时，就会被这个正[电荷](@entry_id:275494)尾迹所吸引。通过这种方式，两个电子之间产生了一种延迟的、有效的吸引作用。这种相互作用的非瞬时性被称为**推迟 (retardation)**。

在[多体理论](@entry_id:169452)的频率-[动量空间](@entry_id:148936)中，这种[推迟效应](@entry_id:199612)体现在[声子](@entry_id:140728)传播子 $D(q, i\Omega_m)$ 对频率的依赖性上 [@problem_id:2986483]。通过在微扰理论中对[声子](@entry_id:140728)自由度进行积分，我们可以得到由单[声子](@entry_id:140728)交换产生的有效[电子-电子相互作用](@entry_id:139900) $V_{\text{eff}}(q, i\Omega_m) = |g_q|^2 D(q, i\Omega_m)$。[声子](@entry_id:140728)[传播子](@entry_id:139558)在零温下的典型形式为 $D(q, \omega) = \frac{2\Omega_q}{(\omega+i\delta)^2 - \Omega_q^2}$。当两个电子之间交换的能量 $\hbar\omega$ 远小于[声子](@entry_id:140728)能量 $\hbar\Omega_q$ 时，分母近似为 $-\Omega_q^2$，使得 $V_{\text{eff}}$ 为负，即相互作用是**吸引**的。正是这种[推迟效应](@entry_id:199612)，使得原本无处不在的瞬时[库仑排斥](@entry_id:181876)作用可以在低能标下被[声子](@entry_id:140728)介导的吸引作用所克服。

相比之下，一个瞬时的相互作用，在时间上正比于 $\delta(\tau)$，其在频率空间中是常数。这种相互作用（如 [Hartree-Fock](@entry_id:142303) 近似中的[库仑相互作用](@entry_id:747947)）只会导致电子能量的静态移动，而不会产生 Eliashberg 理论中至关重要的频率依赖的自能效应和[质量重整化](@entry_id:139777) [@problem_id:2986483]。

### Migdal 定理：一个受控的近似

原则上，为了计算电子的完整性质，我们需要考虑所有可能的[费曼图](@entry_id:144373)，包括对[电子-声子相互作用](@entry_id:140708)顶角本身进行修正的图（即**顶角修正**）。这使得问题变得异常复杂。幸运的是，在大多数传统金属中，一个重要的定理——**Migdal 定理**——极大地简化了这个问题 [@problem_id:2986491]。

Migdal 定理的物理基础正是我们之前讨论过的电子和离子运动的时间尺度（或[能量尺度](@entry_id:196201)）的巨大差异，即**[绝热近似](@entry_id:143074)**。电子质量 $m$ 远小于离子质量 $M$，其比值 $\eta = m/M$ 是一个自然的小参数。[声子](@entry_id:140728)能量 $\hbar\Omega_D$ 与费米能 $E_F$ 的比值尺度关系为：
$$
\frac{\hbar\Omega_D}{E_F} \sim \sqrt{\frac{m}{M}} = \eta^{1/2}
$$
这表明[声子](@entry_id:140728)能量远小于电子能量。顶角修正描述的是一个电子在与[声子](@entry_id:140728)相互作用的过程中，自身又发射和吸收了其他虚[声子](@entry_id:140728)。由于[声子](@entry_id:140728)的响应非常缓慢（声速 $v_s$ 远小于费米速度 $v_F$），当电子与一个[声子](@entry_id:140728)相互作用时，它自身产生的[声子](@entry_id:140728)云无法有效地、快速地反作用于它自己，从而改变这个相互作用顶角。形式上，最低阶顶角修正的大小相对于裸顶角而言，正比于小参数 $\hbar\Omega_D / E_F$ 或 $\eta^{1/2}$。

因此，Migdal 定理指出，在 $\hbar\Omega_D / E_F \ll 1$ 的条件下，顶角修正可以被安全地忽略。这使得[电子自能](@entry_id:148523)的计算变得可行，我们只需要考虑最简单的“自作用”图，而无需担心更复杂的顶角图。Eliashberg 理论正是建立在这一受控的近似之上。

然而，我们必须认识到该定理的适用范围。在某些物理情境下，Migdal 定理会失效 [@problem_id:2986519]。例如：
*   **非绝热体系**：在某些材料中，如低[费米能](@entry_id:143977)的极性[半导体](@entry_id:141536)或有效费米能极低的[重费米子体系](@entry_id:140736)，电子[能量尺度](@entry_id:196201) $E_F$ 可能与[声子](@entry_id:140728)能量 $\Omega$ 相当（$\Omega/E_F \gtrsim 1$）。此时，[绝热近似](@entry_id:143074)失效，顶角修正变得重要。
*   **[极化子形成](@entry_id:136337)**：在窄带氧化物等强耦合体系中，如果[电子-声子耦合](@entry_id:139197)极强，以至于由[晶格](@entry_id:196752)畸变带来的[极化子束缚能](@entry_id:198836) $E_p$ 大于或等于电[子带](@entry_id:154462)宽 $W$，电子就会被“自囚禁”形成[小极化子](@entry_id:145105)。此时，从自由电子出发的微扰论完全失效，Eliashberg 理论不再适用。

### Eliashberg 理论的形式化

在 Migdal 定理的保护下，我们可以构建一个严谨的理论框架来处理推迟的[电子-声子相互作用](@entry_id:140708)。

#### Nambu-Gor'kov 形式

超导态的[基态](@entry_id:150928)是一个宏观相干的库珀对凝聚体，其粒子数不守恒。为了方便地描述这个特性，我们采用 Nambu-Gor'kov 形式。我们引入一个二分量[旋量](@entry_id:158054)，称为 **Nambu [旋量](@entry_id:158054)** [@problem_id:2986487]：
$$
\Psi_k(\tau) = \begin{pmatrix} c_{k\uparrow}(\tau) \\ c_{-k\downarrow}^{\dagger}(\tau) \end{pmatrix}
$$
其中，上分量是湮灭一个 $(k, \uparrow)$ 电子的算符，下分量是产生一个 $(-k, \downarrow)$ 电子的算符，这等效于湮灭一个 $(k, \uparrow)$ 空穴。相应地，我们可以定义一个 $2 \times 2$ 的矩阵格林函数：
$$
\hat{G}(k, i\omega_n) = -\int_0^\beta d\tau e^{i\omega_n\tau} \langle T_\tau \Psi_k(\tau) \Psi_k^{\dagger}(0) \rangle = \begin{pmatrix} G(k, i\omega_n) & F(k, i\omega_n) \\ F^{\dagger}(k, i\omega_n) & -G(-k, -i\omega_n) \end{pmatrix}
$$
这里的 $i\omega_n$ 是[费米子](@entry_id:146235)[松原频率](@entry_id:197724)。矩阵的对角元 $G(k, i\omega_n)$ 是**正常[格林函数](@entry_id:147802)**，描述了单个[准粒子](@entry_id:136584)的传播。非对角元 $F(k, i\omega_n)$ 和 $F^{\dagger}(k, i\omega_n)$ 称为**[反常格林函数](@entry_id:141518)**，它们分别描述了湮灭和产生一个[库珀对](@entry_id:143370)的关联，是超导序的直接度量，仅在超导态下非零。

#### Eliashberg 方程

电子的性质由其[自能](@entry_id:145608) $\hat{\Sigma}(k, i\omega_n)$ 决定，它通过矩阵形式的 Dyson 方程与[格林函数](@entry_id:147802)联系起来：$\hat{G}^{-1}(k, i\omega_n) = \hat{G}_0^{-1}(k, i\omega_n) - \hat{\Sigma}(k, i\omega_n)$。在 Eliashberg 理论中，自能矩阵可以分解为：
$$
\hat{\Sigma}(k, i\omega_n) = i\omega_n[1 - Z(k, i\omega_n)]\hat{\tau}_0 + \phi(k, i\omega_n)\hat{\tau}_1 + \chi(k, i\omega_n)\hat{\tau}_3
$$
其中 $\hat{\tau}_i$ 是 Nambu 空间中的泡利矩阵。$Z(k, i\omega_n)$ 是**重整化函数**，$\phi(k, i\omega_n)$ 是**配对函数**。物理上可观测的**[能隙](@entry_id:191975)函数**定义为 $\Delta(k, i\omega_n) = \phi(k, i\omega_n) / Z(k, i\omega_n)$。

Eliashberg 理论的核心是求解 $Z$ 和 $\Delta$ 的一组自洽的[非线性](@entry_id:637147)积分方程。这些方程通过对所有动量和能量的虚[声子](@entry_id:140728)进行求和，将自能与格林函数和[相互作用核](@entry_id:193790)联系起来。为了将理论与具体材料联系起来，我们引入**Eliashberg 谱函数** $\alpha^2F(\Omega)$ [@problem_id:2986514]：
$$
\alpha^2F(\Omega) = \frac{1}{N(0)} \sum_{k,k',\nu} |g^{\nu}_{k,k'}|^2 \delta(\epsilon_k) \delta(\epsilon_{k'}) \delta(\Omega - \Omega_{k'-k,\nu})
$$
其中 $N(0)$ 是[费米面](@entry_id:137798)上的单自旋[电子态密度](@entry_id:182354)。$\alpha^2F(\Omega)$ 物理上是[声子态密度](@entry_id:199476)，但每个[声子模式](@entry_id:201212)都由其与[费米面](@entry_id:137798)上[电子耦合](@entry_id:192828)强度的平方进行了加权。它是连接微观相互作用与宏观[超导性](@entry_id:142943)质的桥梁，是 Eliashberg 理论的关键材料输入。

对于一个各向同性的 s-波[超导体](@entry_id:191025)，在对动量积分并假设费米能级附近的[电子态密度](@entry_id:182354)为常数后，我们得到一组只依赖于频率的 **Eliashberg 方程**（在[虚频](@entry_id:165180)轴上）[@problem_id:2985871]：
$$
Z(i\omega_n) = 1 + \frac{\pi T}{\omega_n} \sum_{m=-\infty}^{\infty} \lambda(\omega_n - \omega_m) \frac{\omega_m}{\sqrt{\omega_m^2 + \Delta^2(i\omega_m)}}
$$
$$
Z(i\omega_n)\Delta(i\omega_n) = \pi T \sum_{m=-\infty}^{\infty} \left[ \lambda(\omega_n - \omega_m) - \mu^*\theta(\omega_c - |\omega_m|) \right] \frac{\Delta(i\omega_m)}{\sqrt{\omega_m^2 + \Delta^2(i\omega_m)}}
$$
其中，[相互作用核](@entry_id:193790) $\lambda(\nu)$ 由 $\alpha^2F(\Omega)$ 决定：
$$
\lambda(\nu) = 2 \int_0^\infty d\Omega \, \alpha^2F(\Omega) \frac{\Omega}{\Omega^2 + \nu^2}
$$
这组方程必须自洽求解，以得到频率依赖的重整化函数 $Z(i\omega_n)$ 和[能隙](@entry_id:191975)函数 $\Delta(i\omega_n)$。

### 物理后果与关键概念

Eliashberg 方程的解揭示了超越 BCS 理论的丰富物理。

#### 质量增强与[准粒子](@entry_id:136584)阻尼

[重整化](@entry_id:143501)函数 $Z(\omega)$ 具有深刻的物理意义 [@problem_id:2986564]。解析延拓到实频轴后，其虚部和实部分别描述了[准粒子](@entry_id:136584)的不同性质。

*   **质量增强**：在低频极限下，$Z$ 的实部给出了电子[有效质量](@entry_id:142879)的增强因子，$m^*/m = \text{Re}[Z(\omega=0)] = 1 + \lambda_{\text{ep}}$。这里的 $\lambda_{\text{ep}} = \lambda(\nu=0) = 2\int_0^\infty d\Omega \, \frac{\alpha^2F(\Omega)}{\Omega}$ 是无量纲的[电子-声子耦合](@entry_id:139197)常数。这表示电子由于拖拽着一个[声子](@entry_id:140728)云而变得“更重”。

*   **[准粒子](@entry_id:136584)阻尼**：$Z(\omega)$ 的虚部 $\text{Im}[Z(\omega)]$ 与[准粒子](@entry_id:136584)的[散射率](@entry_id:143589)或阻尼率直接相关，决定了其有限的寿命。当能量 $\omega$ 超过某个阈值（例如[声子](@entry_id:140728)发射阈值）时，$\text{Im}[Z(\omega)]$ 变为非零，导致[准粒子](@entry_id:136584)[谱函数](@entry_id:147628)展宽。在超导态中，[能隙](@entry_id:191975)的存在会抑制低能下的散射，但一旦能量足够高，[准粒子](@entry_id:136584)仍然会因非弹性散射而衰减。

#### [库仑赝势](@entry_id:145447) $\mu^*$

Eliashberg 方程的[能隙方程](@entry_id:141924)中出现了一个关键参数 $\mu^*$，即**[库仑赝势](@entry_id:145447)**。它描述了在低能[声子](@entry_id:140728)能标范围内，瞬时[库仑排斥](@entry_id:181876)被有效削弱后的剩余效应。

这个削弱过程同样源于能量尺度的分离 [@problem_id:2986543]。[声子](@entry_id:140728)介导的吸引作用主要发生在费米面附近一个能量宽度约为 $\hbar\Omega_D$ 的窄窗口内，而库仑排斥作用则遍及整个[电子能带](@entry_id:175335)，直至费米能 $E_F$ 或等离体频率。对于参与低能配对的电子而言，那些在更高能量（从 $\hbar\Omega_D$ 到 $E_F$）的虚散射过程，只会感受到库仑排斥。当我们将这些高能自由度积分掉，把它们的效应折合到低能模型中时，它们起到了“屏蔽”作用，从而减弱了在配对窗口内的有效库仑排斥。

Morel 和 Anderson 推导出的[赝势](@entry_id:170389)公式为：
$$
\mu^* \approx \frac{\mu}{1 + \mu \ln(E_F / \Omega_D)}
$$
其中 $\mu$ 是在整个能带上平均的、已被部分屏蔽的[库仑相互作用](@entry_id:747947)参数。由于 $E_F \gg \Omega_D$，对数项很大，导致 $\mu^*$ 显著小于 $\mu$。例如，对于一个典型的金属，如果 $\mu=0.2$, $E_F=5\,\text{eV}$, $\Omega_D=25\,\text{meV}$，那么 $E_F/\Omega_D = 200$，$\ln(200) \approx 5.3$。计算可得 $\mu^* \approx 0.2 / (1 + 0.2 \times 5.3) \approx 0.097$。超导的发生条件是[声子](@entry_id:140728)介导的吸引作用强度 $\lambda_{\text{ep}}$ 必须大于这个剩余的排斥作用 $\mu^*$，即 $\lambda_{\text{ep}} > \mu^*$。

### 强耦合效应：理论预言与实验证据

Eliashberg 理论最重要的贡献在于它能准确描述强耦合 (strong-coupling) [超导体](@entry_id:191025)（即 $\lambda_{\text{ep}} \gtrsim 1$）的行为，这些行为与 BCS 理论的预言有显著差异 [@problem_id:2986458]。

#### 热力学性质的偏离

BCS 理论预言了一系列普适的无量纲比值，而 Eliashberg 理论表明这些比值在强耦合下会系统性地偏离，并且依赖于具体的材料（通过 $\alpha^2F(\Omega)$ 和 $\mu^*$）。
*   **[能隙](@entry_id:191975)与临界温度之比**：$2\Delta_0 / (k_B T_c)$ 的值会大于 BCS 的普适值 $3.53$。例如，[强耦合超导体](@entry_id:140567)铅 (Pb) 的该比值约为 $4.3$。
*   **比热跳变**：在 $T_c$ 处的比热跳变 $\Delta C / C_n$ 也会大于 BCS 的普适值 $1.43$。例如，铅的该比值约为 $2.7$。
*   **[同位素效应](@entry_id:164159)**：由于 $\mu^*$ 的存在，[同位素效应指数](@entry_id:142752) $\alpha$（定义为 $T_c \propto M^{-\alpha}$）会小于 BCS 理论的理想值 $0.5$。

#### 谱学特征

Eliashberg 理论最引人注目的成功之一是它对超导态谱学测量的精确定量解释。
*   **隧道谱**：通过扫描隧道显微镜 (STM) 测量的[微分](@entry_id:158718)[电导](@entry_id:177131) $dI/dV$ 正比于超导态的[准粒子](@entry_id:136584)态密度 $N_s(\omega)$。在 Eliashberg 理论中，$N_s(\omega)$ 不再是 BCS 理论中在[能隙](@entry_id:191975)边 $\Delta_0$ 处的尖锐奇异峰。由于[准粒子](@entry_id:136584)阻尼，该峰会被展宽。更重要的是，在能量为 $\Delta_0 + \hbar\Omega$ 的位置（其中 $\hbar\Omega$ 是 $\alpha^2F(\Omega)$ 的峰值能量），$N_s(\omega)$ 会出现额外的结构，如著名的“**dip-hump**”特征。这些结构是[准粒子](@entry_id:136584)通过发射真实[声子](@entry_id:140728)进行衰变的直接反映，它们就像是配对“胶水”——[声子](@entry_id:140728)——的指纹，为电子-[声子](@entry_id:140728)机制提供了决定性的证据。
*   **光学和光[电子能谱](@entry_id:160814)**：类似地，在红外[光谱](@entry_id:185632)和角分辨光电子能谱 (ARPES) 中，也可以观察到与[声子](@entry_id:140728)能量相关的类似结构，它们都是由频率依赖的自能函数 $\Sigma(\omega)$ 所导致的。

综上所述，Eliashberg 理论通过严谨处理相互作用的推迟特性，不仅为 BCS 理论提供了坚实的微观基础，更将其推广到强耦合领域，成功解释了大量偏离 BCS 理论的实验现象，并深刻揭示了电子与晶格振动之间复杂的动力学关系。